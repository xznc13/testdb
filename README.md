# MariaDB 10.0 Docker Image (Centos7)

This is a MariaDB 10.0 Docker [million12/mariadb](https://registry.hub.docker.com/u/million12/mariadb/) image. Built on top of official [centos:centos7](https://registry.hub.docker.com/_/centos/) image. Inspired by [Tutum](https://github.com/tutumcloud)'s [tutum/mariadb](https://github.com/tutumcloud/tutum-docker-mariadb) image.

Note: be aware that, by default in this container, MariaDB is configured to use 1GB memory (innodb_buffer_pool_size in [tuning.cnf](container-files/etc/my.cnf.d/tuning.cnf)). If you try to run it on node with less memory, it will fail.

### Custom Password for user admin 
If you want to use a preset password instead of a random generated one, you can set the environment variable MARIADB_PASS to your specific password when running the container:  

`docker run -d -p 3306:3306 -e MARIADB_PASS="mypass" stephenbutcher/mar10c7`

### Mounting the database file volume from other containers
One way to persist the database data is to store database files in another container. To do so, first create a container that holds database files:  

`docker run -d -v /var/lib/mysql --name db-data busybox:latest`  

This will create a new container and use its folder `/var/lib/mysql` to store MariaDB database files. You can specify any name of the container by using `--name` option, which will be used in next step.

After this you can start your MariaDB image using volumes in the container created above (put the name of container in `--volumes-from`).  

`docker run -d --volumes-from db-data -p 3306:3306 stephenbutcher/mar10c7`

## Original Authors

Author: Marcin Ryzycki (<marcin@m12.io>)  
Author: Przemyslaw Ozgo (<linux@ozgo.info>)  

---

