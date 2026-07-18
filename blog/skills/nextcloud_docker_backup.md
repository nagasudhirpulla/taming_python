# Backup and restore Nextcloud running in docker

## Data to be backed up

- Nextcloud application files, like apps, html files, config etc
- Database data files

All the data is present in docker volumes 

## Backup strategy

- Nextcloud’s `/var/www/html` folder can be backed up and restored for restoring nextcloud files and config
- PostgreSQL’s logical dump (using `pg_dump` command) can be backed up as a file, and this file can be used while db restoration (using `pg_restore` command).

The restored volumes can be mounted when rebuilding the containers from scratch

## Basic Nextcloud volume backup with tar

- The following docker command backs up the nextcloud volume as a tar file in the host machine

```bash
docker run --rm \
--mount source=nextcloud_nextcloud,target=/mount_dir \
-v $(pwd):/backup \
busybox \
tar -czvf /backup/nextcloud_bkp.tar.gz /mount_dir
```

The equivalent windows command is

```
docker run --rm --mount source=nextcloud_nextcloud,target=/mount_dir ^
-v "%cd%:/backup" ^
busybox ^
tar -czvf /backup/nextcloud_bkp.tar.gz /mount_dir

```

## Incremental volume backups with Restic instead of tar

- Instead of doing full backups every time, `Restic` can be used to provide a very easy way to perform **incremental backups** on the Nextcloud files
- **Retention period** (example: 365 days) can be easily enforced using Restic
- Backup or restore of docker volumes are very straight forward commands and the commands themselves can be run inside **Restic docker container**, making the setup independent of host OS (Windows/Mac/Linux)
- Restic is **opensource**, has a lot of GitHub stars and is actively developed
- Restic supports backing up to **multiple backends like AWS S3**, Azure blob storage etc., seamlessly in addition to local/SFTP storage locations

### Create Restic backup repository (one time setup)

```bash
#!/bin/bash

# Navigate to the script's directory
cd "$(dirname "$(readlink -f "$0")")" || exit 1

# Load environment variables
if [ -f ./config.sh ]; then
    source ./config.sh
else
    echo "Error: config.sh file not found!"
    exit 1
fi

# Initialize the Restic repository
docker run --rm \
  -v "$backups_dir:/repo" \
  -e RESTIC_PASSWORD="$restic_password" \
  restic/restic \
  init -r /repo
```

The equivalent windows command is

```
@echo off
:: Navigate to the script's directory
cd /d "%~dp0"

CALL config.bat

docker run --rm -v "%BACKUPS_DIR%:/repo" ^
-e RESTIC_PASSWORD=%RESTIC_PASSWORD% ^
restic/restic ^
init -r /repo
```

### Run the daily backup script

The backup script does the following

- Keep Nextcloud app in maintenance mode
- Create a logical backup of the postgres database using `pg_dump` command
- Perform an incremental backup of nextcloud files docker volume and postgres logical backup file using a restic docker container
- Turn off Nextcloud app’s maintenance mode
- Prune old backups as per retention policy

```bash
#!/bin/bash

# Navigate to the script's directory
cd "$(dirname "$(readlink -f "$0")")" || exit 1

# Load environment variables
if [ -f ./config.sh ]; then
    source ./config.sh
else
    echo "Error: config.sh file not found!"
    exit 1
fi

echo "==================================================="
echo "  NEXTCLOUD and POSTGRESQL BACKUP SCRIPT"
echo "==================================================="
echo

echo "[1/7] running nextcloud cron job..."
docker exec -u www-data "$nextcloud_container" php /var/www/html/cron.php

echo "[2/7] enabling nextcloud maintenance mode..."
docker exec -u www-data "$nextcloud_container" php occ maintenance:mode --on
echo ""

echo "[3/7] create a clean database dump directly into the db storage volume"
docker exec "$db_container" pg_dump -U "$db_user" -d "$db_name" -F c -f /var/lib/postgresql/nextcloud_backup.dump
echo ""

echo "[4/7] running the daily deduplicated backup (files + database logical backup file)..."
# This maps both volumes into a single /data directory inside the restic container
docker run --rm \
  --mount source="$nextcloud_volume",target=/data/nextcloud_files \
  --mount source="$db_volume",target=/data/postgres_raw_data \
  -v "$backups_dir:/repo" \
  -e RESTIC_PASSWORD="$restic_password" \
  restic/restic \
  -r /repo backup \
  /data/nextcloud_files \
  /data/postgres_raw_data/nextcloud_backup.dump
echo ""

echo "[5/7] disabling nextcloud maintenance mode..."
docker exec -u www-data "$nextcloud_container" php occ maintenance:mode --off
echo ""

echo "[6/7] pruning old data (keeping last 365 days)..."
docker run --rm \
  -v "$backups_dir:/repo" \
  -e RESTIC_PASSWORD="$restic_password" \
  restic/restic \
  -r /repo forget \
  --keep-within "$restic_retention" --prune
echo ""

echo "[7/7] cleaning up temporary dump file from the live db volume"
docker exec "$db_container" rm /var/lib/postgresql/nextcloud_backup.dump

echo "Backup process complete! Both volumes are securely stored on your Linux host."

```

- The following is the windows version

```
@echo off
:: Navigate to the script's directory
cd /d "%~dp0"

CALL config.bat

echo ===================================================
echo NEXTCLOUD and POSTGRESQL BACKUP SCRIPT
echo ===================================================
echo.

echo [1/7] Running nextcloud cron job...
docker exec -u www-data %NEXTCLOUD_CONTAINER% php /var/www/html/cron.php

echo [2/7] Enabling Nextcloud Maintenance Mode...
docker exec -u www-data %NEXTCLOUD_CONTAINER% php occ maintenance:mode --on
echo.

echo [3/7] Create a clean Database Dump directly into the DB storage volume
docker exec %DB_CONTAINER% pg_dump -U %DB_USER% -d %DB_NAME% -F c -f /var/lib/postgresql/nextcloud_backup.dump
echo.

echo [4/7] Running the daily deduplicated backup (Files + Database logical backup file)...
:: This maps both volumes into a single /data directory inside the Restic container
docker run --rm ^
  --mount source=%NEXTCLOUD_VOLUME%,target=/data/nextcloud_files ^
  --mount source=%DB_VOLUME%,target=/data/postgres_raw_data ^
  -v "%BACKUPS_DIR%:/repo" ^
  -e RESTIC_PASSWORD=%RESTIC_PASSWORD% ^
  restic/restic ^
  -r /repo backup ^
  /data/nextcloud_files ^
  /data/postgres_raw_data/nextcloud_backup.dump
echo.

echo [5/7] Disabling Nextcloud Maintenance Mode...
docker exec -u www-data %NEXTCLOUD_CONTAINER% php occ maintenance:mode --off
echo.

echo [6/7] Pruning old data (Keeping last 365 days)...
docker run --rm ^
  -v "%BACKUPS_DIR%:/repo" ^
  -e RESTIC_PASSWORD=%RESTIC_PASSWORD% ^
  restic/restic ^
  -r /repo forget ^
  --keep-within %RESTIC_RETENTION% --prune
echo.

echo [7/7] Cleaning up temporary dump file from the live DB volume
docker exec %DB_CONTAINER% rm /var/lib/postgresql/nextcloud_backup.dump
echo.

echo Backup process complete! Both volumes are securely stored on your Windows host.

```

### View saved backups

- The following command lists the backups (snapshots) in the restic backup storage location (aka restic backup repo)

```bash
#!/bin/bash

# Navigate to the script's directory
cd "$(dirname "$(readlink -f "$0")")" || exit 1

# Load environment variables
if [ -f ./config.sh ]; then
    source ./config.sh
else
    echo "Error: config.sh file not found!"
    exit 1
fi

# List all restic snapshots
docker run --rm \
  -v "$backups_dir:/repo" \
  -e RESTIC_PASSWORD="$restic_password" \
  restic/restic \
  -r /repo snapshots

```

- The following is a windows version

```
@echo off
:: Navigate to the script's directory
cd /d "%~dp0"

CALL config.bat

docker run --rm ^
-v "%BACKUPS_DIR%:/repo" ^
-e RESTIC_PASSWORD=%RESTIC_PASSWORD% ^
restic/restic ^
-r /repo snapshots
```

### Restore from a specific snapshot

- We can restore a latest snapshot or a specific snapshot (snapshot id) using the following script that does the following
    - stops the nextcloud container and wipes the nextcloud docker volume
    - restores the nextcloud files into the nextcloud docker volume, restores the logical db backup file into the db docker volume
    - restores postgres db using logical backup file (`pg_restore` command)
    - starts the nextcloud container

```bash
#!/bin/bash

# Navigate to the script's directory
cd "$(dirname "$(readlink -f "$0")")" || exit 1

# Load environment variables
if [ -f ./config.sh ]; then
    source ./config.sh
else
    echo "Error: config.sh file not found!"
    exit 1
fi

echo "==================================================="
echo "  NEXTCLOUD and POSTGRESQL COMPLETE RECOVERY SCRIPT"
echo "==================================================="
echo ""

# 1. Check if a Backup ID was provided; otherwise, fallback to latest
if [ -z "$1" ]; then
    BACKUP_ID="latest"
    echo "[INFO] No Backup ID provided. Falling back to the LATEST snapshot..."
else
    BACKUP_ID="$1"
    echo "[INFO] Target Backup ID selected: $BACKUP_ID"
fi
echo ""

echo "[1/7] Stopping active Nextcloud container..."
docker stop "$nextcloud_container"
echo ""

echo "[2/7] Wiping existing Docker volumes clean to prevent data corruption..."
# Clears out the app data volume completely
docker run --rm --mount source="$nextcloud_volume",target=/data busybox sh -c "rm -rf /data/* /data/.* 2>/dev/null || true"
echo ""

echo "[3/7] Restoring Files and Database from the Restic snapshot id $BACKUP_ID..."
# Maps both clean target volumes and unpacks the respective data back into them
docker run --rm \
  --mount source="$nextcloud_volume",target=/data/nextcloud_files \
  --mount source="$db_volume",target=/data/postgres_raw_data \
  -v "$backups_dir:/repo" \
  -e RESTIC_PASSWORD="$restic_password" \
  restic/restic \
  -r /repo restore "$BACKUP_ID" --target /
echo ""

echo "[4/7] Importing the PostgreSQL Database Dump..."
# 1. Terminate all active connections to the target database
docker exec -i "$db_container" psql -U "$db_user" -d template1 -c "
  SELECT pg_terminate_backend(pg_stat_activity.pid)
  FROM pg_stat_activity
  WHERE pg_stat_activity.datname = '$db_name'
    AND pid <> pg_backend_pid();"

# 2. Drop and recreate the database inside the container
docker exec -i "$db_container" psql -U "$db_user" -d template1 -c "DROP DATABASE IF EXISTS \"$db_name\";"
docker exec -i "$db_container" psql -U "$db_user" -d template1 -c "CREATE DATABASE \"$db_name\";"

# 3. Restore the database dump into the newly created database
docker exec "$db_container" pg_restore -U "$db_user" -d "$db_name" -v /var/lib/postgresql/nextcloud_backup.dump
echo ""

echo "[5/7] Restarting Application container..."
docker start "$nextcloud_container"
echo ""

echo "[6/7] Cleaning up restored dump file from the live DB volume"
docker exec "$db_container" rm /var/lib/postgresql/nextcloud_backup.dump
echo ""

echo "[7/7] Verifying and finalizing Nextcloud application status..."
# Safely attempts to ensure maintenance mode is turned off upon restart
docker exec -u www-data "$nextcloud_container" php occ maintenance:mode --off 2>/dev/null
echo ""

echo "==================================================="
echo "  Recovery process complete! System is back online."
echo "==================================================="

```

- The following is the windows version

```
@echo off
:: Navigate to the script's directory
cd /d "%~dp0"

CALL config.bat

echo ===================================================
echo   NEXTCLOUD and POSTGRESQL COMPLETE RECOVERY SCRIPT
echo ===================================================
echo.

:: 1. Check if a Backup ID was provided; otherwise, fallback to latest
if "%~1" == "" (
    set "BACKUP_ID=latest"
    echo [INFO] No Backup ID provided. Falling back to the LATEST snapshot...
) else (
    set "BACKUP_ID=%~1"
    echo [INFO] Target Backup ID selected: %BACKUP_ID%
)
echo.

echo [1/7] Stopping active Nextcloud container...
docker stop %NEXTCLOUD_CONTAINER%

echo.
echo [2/7] Wiping existing Docker volumes clean to prevent data corruption...
:: Clears out the app data volume completely
docker run --rm --mount source=%NEXTCLOUD_VOLUME%,target=/data busybox sh -c "rm -rf /data/*"

echo.
echo [3/7] Restoring Files and Database from the Restic snapshot id %BACKUP_ID%...
:: Maps both clean target volumes and unpacks the respective data back into them
docker run --rm ^
  --mount source=%NEXTCLOUD_VOLUME%,target=/data/nextcloud_files ^
  --mount source=%DB_VOLUME%,target=/data/postgres_raw_data ^
  -v "%BACKUPS_DIR%:/repo" ^
  -e RESTIC_PASSWORD=%RESTIC_PASSWORD% ^
  restic/restic ^
  -r /repo restore %BACKUP_ID% --target /

echo.
echo [4/7] Importing the PostgreSQL Database Dump...
:: Terminate all active connections to the target database 
docker exec -i %db_container% psql -U %DB_USER% -d template1 -c "SELECT pg_terminate_backend(pid) FROM pg_stat_activity WHERE datname = '%DB_NAME%' AND pid ^<^> pg_backend_pid();"

:: Drop and recreate the database inside the container
docker exec -i %DB_CONTAINER% psql -U %DB_USER% -d template1 -c "DROP DATABASE IF EXISTS \"%DB_NAME%\";"
docker exec -i %DB_CONTAINER% psql -U %DB_USER% -d template1 -c "CREATE DATABASE \"%DB_NAME%\";"

:: restore the database dump into the newly created database
docker exec %DB_CONTAINER% pg_restore -U %DB_USER% -d %DB_NAME% -v /var/lib/postgresql/nextcloud_backup.dump

echo.
echo [5/7] Restarting Application container...
docker start %NEXTCLOUD_CONTAINER%

echo.
echo [6/7] Cleaning up restored dump file from the live DB volume
docker exec %DB_CONTAINER% rm /var/lib/postgresql/nextcloud_backup.dump

echo.
echo [7/7] Verifying and finalizing Nextcloud application status...
:: Safely attempts to ensure maintenance mode is turned off upon restart
docker exec -u www-data %NEXTCLOUD_CONTAINER% php occ maintenance:mode --off 2>nul

echo.
echo ===================================================
echo   Recovery process complete! System is back online.
echo ===================================================

```

## Backup configuration

- All the backup settings are saved in a `config.sh` file which will be used in all the backup scripts

```bash
#!/bin/bash
export db_container="db"
export nextcloud_container="app"
export nextcloud_volume="nextcloud_nextcloud"
export db_volume="nextcloud_db"
export db_user="nextcloud"
export db_name="nextcloud"
export restic_password="password123"
export restic_retention="365d"

# Gets the directory of the current script and looks one level up
export backups_dir="$(dirname "$(readlink -f "$0")")/../backups"
```

- In windows, a `config.bat` file will set the environment variables

```
set "DB_CONTAINER=db"
set "NEXTCLOUD_CONTAINER=app"
set "NEXTCLOUD_VOLUME=nextcloud_nextcloud"
set "DB_VOLUME=nextcloud_db"
set "DB_USER=nextcloud"
set "DB_NAME=nextcloud"
set "RESTIC_PASSWORD=password123"
set "RESTIC_RETENTION=365d"
set "BACKUPS_DIR=%cd%\..\backups"
```

## References

- Restic GitHub repository - [https://github.com/restic/restic](https://github.com/restic/restic)
- Restic docs - https://restic.readthedocs.io/en/latest/index.html
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjc2MjUyNDQ2LDYzOTEwMjMyMl19
-->