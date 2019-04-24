# Learning and Cheatsheet

This repository displays summary tables for various libraries such as Vim, Docker, etc.

The goal is that a developer has a table nearby with a little help that can be worth in their day to day.

I hope this information will help someone.

- [Docker](#Docker)


## Docker

### Basic Commands

| Description                                  | Command                                                      |
| -------------------------------------------- | ------------------------------------------------------------ |
| Download Ubuntu image                        | `docker pull ubuntu:18.04`                                   |
| List of downloaded images                    | `docker images`                                              |
| Access the container via `IMAGE ID` or `TAG` | `docker run -it IMAGE_ID bash docker run -it ubuntu:18.04 bash` |
| Set or change a label (`TAG`)                | `docker tag IMAGE_ID old:latest`                             |
| List of containers in running                | `docker ps`                                                  |
| Exit from container **stopping it**          | CTRL + D                                                     |
| Exit from container **without stopping it**  | CTRL + PQ                                                    |
| List of all containers running               | `docker ps -a`                                               |
| Save the status of a container               | `docker commit CONTAINER_ID image_name`                      |
| Remove a container                           | `docker rm CONTAINER_ID`                                     |

### Medium Commands

| Description                                                  | Command                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Fix error when there are two images with the same `ID` (name) | `docker images | grep CONTAINER | AWK '{print $1":"$2}' | xargs docker rmi` |
| Start the containers associated with the compose in demon mode | `docker-compose up -d`                                       |
| Get `CONTAIER_ID` from `CONTAINER_NAME`                      | `docker ps -aqf "name=containername"` <br />  `a` - for all. It works even if the container is not running <br /> `q` - to exit <br /> `f` - to use the filter |
| Copy files inside the container                              | `docker cp FILE CONTAINER:/path/to/directory`                |
| `docker build` using `TAG`                                   | `docker build -t TAG`                                        |
| View Container Information                                   | `docker inspect CONTAINER_ID`                                |
| Export image (save content into a `tar`)                     | `docker save -o /path/to/image.tar image_name`               |
| Import image (load image from file)                          | `docker load -i /path/to/image.tar`                          |
| See containers `logs`                                        | `docker logs --tail 50 --follow --timestamps CONTAINER_NAME` |
| See associated volumes                                       | `docker volume ls`                                           |
| View docker disk usage                                       | `docker system df`                                           |
| Delete unused data                                           | `docker system prune`                                        |
| Eliminate sagging volumes                                    | `docker volume prune`                                        |
| Add `docker` to group so as not to type `sudo`' (Linux)      | `sudo usermod -aG docker $(whoami)`                          |
| Stop all containers                                          | `docker ps $(docker ps -a -q)`                               |
| Delete all images                                            | `docker rmi $(docker images -q)`                             |
| See list of picked up volumes                                | `docker volume ls -qf dangling=true`                         |
| Eliminate sagging volumes                                    | `docker volume rm $(docker volume ls -qf dangling=true)`     |
| Run and enter into a container using an `entrypoint`         | `docker run ... --entrypoint=bash`                           |

### Docker and MySQL

| Description                            | Command                                                      |
| -------------------------------------- | ------------------------------------------------------------ |
| Run MySQL                              | `docker run -p [HOST IP:PORT]:[GUEST IP:PORT] -e MYSQL_PASSWORD=pass -e MYSQL_DATABASE=database IMAGE` |
| Import Database (inside the container) | `mysql -uUSER -pPASS database < file.sql`                    |
| Enter to container                     | `docker exec -it CONTAINER mysql -uUSER -p`                  |
| Backup from Docker to MySQL            | `docker exec CONTAINER /usr/bin/mysqldump -uroot -p DATA > backup.sql` |
| Restore BackUp                         | `docker exec -i CONTAINER mysql -uroot -p DATABASE < file.sql` |
| Export Database (inside the container) | `mysqldump -uUSER -p --opt database > database.sql`          |



