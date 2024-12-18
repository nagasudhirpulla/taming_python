# Run PostgreSQL as a docker container

## Why run PostgreSQL as docker container

-   Easy to setup
-   Ephemeral (easy to destroy)
-   Ideal for development and testing environments
-   Run multiple PostgreSQL instances very easily
-   very easy to create a temporary isolated environment

## PostgreSQL docker image installation

-   Install docker in the machine. Docker Desktop can be used for easy management
-   PostgreSQL docker image can be found in docker hub at [https://hub.docker.com/_/postgres](https://hub.docker.com/_/postgres)
-   Pull docker image using `docker pull postgres`
-   A specific version of docker can be installed using tags like `docker pull postgres:17` . The supported tags can be found at [https://hub.docker.com/_/postgres/tags](https://hub.docker.com/_/postgres/tags)

## Run PostgreSQL docker container

-   Run the following command to run PostgreSQL docker container

```powershell
docker run --rm -d --name mydb1 -e POSTGRES_PASSWORD=db_pswrd -p 5432:5432 -v "C:\\dbFolders\\db1":/var/lib/postgresql/data postgres

```

-   `--rm` means, the container is deleted after it stops
-   `--name mydb1` sets the container name to mydb1
-   `-e POSTGRES_PASSWORD=db_pswrd` sets an environment variable `POSTGRES_PASSWORD` value as `db_pswrd`
-   `-d` means the container will run in background (detached mode)
-   `-p 5432:5432` means the 5432 port of container can be accessed using 5432 port of host machine. The format is `host_port:container_port`
-   `-v "C:\\dbFolders\\db1":/var/lib/postgresql/data` means the data of the container folder `/var/lib/postgresql/data` will be stored in `C:\\dbFolders\\db1`. The format is `host_path:container_path`
-   `postgres` is the name of the container image. It can also be something like `postgres:14`

## Connect to PostgreSQL container

-   Use `docker exec` command to connect to the PostgreSQL container

```powershell
docker exec -it -u postgres mydb psql

```

-   `docker exec` can execute a command in a running container
-   `-it` creates a pseudo terminal that allows standard command line inputs to the container
-   `-u postgres` runs the command with the user `postgres`

## Simple psql commands

-   `\\l` - List all databases
-   `\\c dbname` - connect to a database `dbname`
-   `\\dn` - list schemas of the database
-   `\\db` - list tablespaces of the database
-   `\\dt` - list tables of the database
-   `\\dt schema1.*` - list tables of the database schema `schema1`

## View PostgreSQL container logs

-   By default PostgreSQL container sends logs to standard output (command line) of the container
-   Hence the logs can be viewed using `docker logs -f mydb1`
-   `-f` flag means new logs will also displayed while viewing logs

### Store PostgreSQL logs into files

-   add `-c logging_collector=on` to the docker run statement.
-   This will add a command line argument so that PostgreSQL logs will be written to a file in the folder `/var/lib/postgresql/data/log`
-   To persist the logs to host, the folder `/var/lib/postgresql/data/` can also be bound to host folder like

```powershell
docker run --rm -d --name mydb1 -e POSTGRES_PASSWORD=db_pswrd -p 5432:5432 -v "C:\\dbFolders\\db1":/var/lib/postgresql/data postgres -c logging_collector=on

```

## Run PostgreSQL container with docker-compose file

-   Create a yaml file as shown below to create PostgreSQL container from `docker compose` command

```yaml
# dbContainer.yaml
services:
  db:
    image: postgres:latest
    restart: always
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U postgres"]
      interval: 5s
      timeout: 5s
      retries: 5
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres
    ports:
      - "5432:5432"
    volumes:
      - dbVol:/var/lib/postgresql/data
    command: -c logging_collector=on
volumes:
  dbVol:
    driver: local
    driver_opts:
      type: none
      device: "C:\\\\dbFolders\\\\db1"
      o: bind


```

-   A service named `db` runs a PostgreSQL container
-   By opening a command line in the folder containing the docker compose file, the following commands can be run to manage the containers
    -   `docker compose up` - creates the containers
    -   `docker compose ps` - view all the containers status
    -   `docker compose down` - destroys the containers
    -   `docker compose stop` - stops the containers
    -   `docker compose start` - starts the containers
    -   `docker compose restart` - restarts the containers
    -   `docker compose logs`- view the logs of all the containers

## Database initialization SQL

-   If an SQL file is placed in the `/docker-entrypoint-initdb.d/` of the docker container, it will be executed when a database is being created for the first time.
-   So any initialization SQL scripts (like creating initial database tables etc.) can be executed using this method
-   For example, an SQL file `init.sql` on the host containing database initialization SQL can be mapped with the container using the following in the docker run command. `-v ./init.sql:/docker-entrypoint-initdb.d/create_tables.sql`
-   The same can be achieved in docker compose file also by adding the following to the volumes section of the db service as shown below

```yaml
# dbContainer.yaml
services:
  db:
    ...
    volumes:
      - dbVol:/var/lib/postgresql/data
      - ./init.sql:/docker-entrypoint-initdb.d/create_tables.sql
    ...
volumes:
  ...

```

## References

-   PostgreSQL docker environment variables - [https://github.com/docker-library/docs/blob/master/postgres/README.md#environment-variables](https://github.com/docker-library/docs/blob/master/postgres/README.md#environment-variables)
-   difference between docker volume and bind mount - [https://stackoverflow.com/questions/47150829/what-is-the-difference-between-binding-mounts-and-volumes-while-handling-persist](https://stackoverflow.com/questions/47150829/what-is-the-difference-between-binding-mounts-and-volumes-while-handling-persist)
-   PostgreSQL docker cheat-sheet - [https://gist.github.com/robbdimitrov/4e37f5c931e47b1e0fa9b7facddf3851](https://gist.github.com/robbdimitrov/4e37f5c931e47b1e0fa9b7facddf3851)
-   Using exec to run commands in running docker containers - [https://www.digitalocean.com/community/tutorials/how-to-use-docker-exec-to-run-commands-in-a-docker-container](https://www.digitalocean.com/community/tutorials/how-to-use-docker-exec-to-run-commands-in-a-docker-container)
-   docker compose quick-start - [https://spacelift.io/blog/docker-compose](https://spacelift.io/blog/docker-compose)
-   Running PostgreSQL from docker-compose - [https://geshan.com.np/blog/2021/12/docker-postgres/](https://geshan.com.np/blog/2021/12/docker-postgres/)
-   Install PostgreSQL in Ubuntu - [https://www.prisma.io/dataguide/postgresql/setting-up-a-local-postgresql-database#debian-and-ubuntu](https://www.prisma.io/dataguide/postgresql/setting-up-a-local-postgresql-database#debian-and-ubuntu)
-   Start PostgreSQL automatically on startup in Ubuntu- [https://www.heatware.net/postgresql/start-postgresql-automatically-boot/](https://www.heatware.net/postgresql/start-postgresql-automatically-boot/)
-   Uninstall PostgreSQL in Ubuntu - [https://neon.tech/postgresql/postgresql-administration/uninstall-postgresql-ubuntu](https://neon.tech/postgresql/postgresql-administration/uninstall-postgresql-ubuntu)
-   install PostgreSQL in WSL Ubuntu - [https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-database#install-postgresql](https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-database#install-postgresql)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTMyOTE2NTA5MCwtMTk2MDA0MTk3M119
-->