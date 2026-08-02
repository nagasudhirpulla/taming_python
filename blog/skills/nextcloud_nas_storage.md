## External Storage of type “local storage” in Nextcloud
![nextcloud_host_folder_mount.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/nextcloud_host_folder_mount.png?raw=true)
-   Nextcloud supports adding multiple types of external storage for increasing the file storage capacity. However, “External Storage Support” nextcloud app should be enabled as a prerequisite.
-   A folder in the docker host can be mount into the nextcloud container and then this folder can be used as an External Storage of type “local storage” in the Nextcloud app

```yaml
services:
	...
	app:
		image: nextcloud:apache
		container_name: app
		...
		volumes:
			/path/to/host/folder:/local_folder
			...
```

-   If the docker host is linux, make sure the UID and GID 33 have write permissions to the host folder. Because the nextcloud container's www-data user always runs with UID 33 and GID 33

```bash
# Set ownership to UID 33 and GID 33
sudo chown -R 33:33 /path/to/host/folder

# Set proper read/write permissions
sudo chmod -R 750 /path/to/host/folder

```

-   The container folder can be added as an external storage in the Nextcloud UI at Administration Settings → External Storage menu as shown below.

![nextcloud_local_storage_setup.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/nextcloud_local_storage_setup.png?raw=true)

-   A nextcloud container folder can also be added to External storage using the following occ commands inside the nextcloud container

```bash
php occ app:enable files_external
php occ files_external:create "Folder_Storage" local null:null -c datadir="/local_folder"

```

## NAS folder as Nextcloud External Storage

![nextcloud_nas_storage_setup.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/nextcloud_nas_storage_setup.png?raw=true)

-   The NAS folder can be mounted as a folder location in the docker host.  
    For example, if a NAS supports CIFS, it’s folder can be bound as a local folder (say `/local_folder`) by adding a CIFS bind mount in the host’s `/etc/fstab` file.

```bash
//nasHost/nasFolder /local_folder cifs username=nasUname,password=nasPwd,iocharset=utf8,file_mode=0777,dir_mode=0777,noperm

```

-   Since the NAS folder is available as a folder in the docker host, it can now be added as an external storage in the nextcloud just like any folder in the docker host

## Manage access to External Storage

-   The access to External storage can be restricted to specific nextcloud user groups and users by editing the external storage in the nextcloud administration settings as shown below

## View External Storage Files

-   Nextcloud external storage files can be seen in the Files page as shown below

## Working example

-   A working example docker setup can be found at [https://github.com/nagasudhirpulla/nextcloud_docker_setup](https://github.com/nagasudhirpulla/nextcloud_docker_setup)

## References

-   [External Storage — Nextcloud 34 Administration Manual](https://docs.nextcloud.com/server/stable/admin_manual/configuration_files/external_storage_configuration_gui.html#)
-   [Nextcloud docker-compose setup](https://nagasudhir.blogspot.com/2026/06/nextcloud-docker-compose-setup.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1MTc3Mjk0MTgsNjU2Njg0MjIyXX0=
-->