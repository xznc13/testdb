# MariaDB 10.0 Docker Image (Centos7)



`docker run -d -p 3306:3306 -e MARIADB_PASS="mypass" stephenbutcher/mar10c7`

### Mounting the database file volume from other containers
One way to persist the database data is to store database files in another container. To do so, first create a container that holds database files:  

`docker run -d -v /var/lib/mysql --name db-data busybox:latest`  

This will create a new container and use its folder `/var/lib/mysql` to store MariaDB database files. You can specify any name of the container by using `--name` option, which will be used in next step.

After this you can start your MariaDB image using volumes in the container created above (put the name of container in `--volumes-from`).  

`docker run -d --volumes-from db-data -p 3306:3306 stephenbutcher/mar10c7`



