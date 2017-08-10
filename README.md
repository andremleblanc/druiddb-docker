# Dockerized Druid

This is the source repository for my Druid docker images. In addition to the Dockerfiles, there is also a docker-compose.yml that can be used to bring up the whole cluster.

These images were made for the purpose of easily testing and developing with Druid, but are untested for production use.

The Druid images assume Zookeeper is running with the alias `zookeeper` and Derby is running with the alias `derby`.

## Usage
1. Clone this repo
2. `cd` into the directory
3. From the cloned repo run `docker-compose up` to run the cluster. You can also run `docker-compose up --build` to build the images from the local Dockerfiles and then run the cluster (useful for tweaking the files).
4. Druid should be running with the ports exposed. You can use `docker ps` to see which ports are opened and where they are mapped to.


## Images

[andremleblanc/druid-broker](https://hub.docker.com/r/andremleblanc/druid-broker/)  
[andremleblanc/druid-coordinator](https://hub.docker.com/r/andremleblanc/druid-coordinator/)  
[andremleblanc/druid-historical](https://hub.docker.com/r/andremleblanc/druid-historical/)  
[andremleblanc/druid-middlemanager](https://hub.docker.com/r/andremleblanc/druid-middlemanager/)  
[andremleblanc/druid-overlord](https://hub.docker.com/r/andremleblanc/druid-overlord/)
