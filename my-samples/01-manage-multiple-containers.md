### Objectives

* Run servers: ```nginx```, ```mysql```, ```httpd``` (apache)
* Run them as ```--detach```
* Name them with ```--name```
* nginx should listen on ```80:80```, httpd on ```8080:80```, mysql on ```3306:3306```
* mysql: use ```--env``` (or ```-e```) to pass in ```MYSQL_RANDOM_ROOT_PASWORD=yes```
* use ```docker container logs``` on mysql to find the random password it created on startup
* clean up with ```docker container stop``` and ```docker container rm``` (both can accept multiple names or ID's)
* use ```docker container ls``` to ensure everything is correct before and after cleanup


```bash

# Run servers
docker container run -d --name db -p 3306:3306 -e MYSQL_RANDOM_ROOT_PASSWORD=yes mysql
docker container run -d --name webserver -p 8080:80 httpd
docker container run -d --name proxy -p 80:80 nginx

# Get mysql password
docker container logs mysql

# Test ports -
# nginx
curl localhost
# httpd
curl localhost:8080

# Cleanup
docker container stop proxy webserver db
docker container rm proxy webserver db

```