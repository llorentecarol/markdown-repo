# Setting Up Dev Workspace With Docker

## Introduction

Dev Workspace setup is essential for all developers specially with newly onboarded developers in a project.


## What tools do you need to configure in your environment

* IDE: Eclipse/IntelliJ
 - What are the plugins I need to setup for my chosen IDE?

## What services do I need?

Below is a sample docker compose yaml that runs the following services: 

* Mongo
* Sonarqube
* Swagger UI

Create a docker compose yaml:

```yaml
version: "3.3"
services:
  database:
    image: 'mongo:4.0.3'
    container_name: 'llorente_local_mongo_container'
#    environment:
#      - MONGO_INITDB_DATABASE=admin
#      - MONGO_INITDB_ROOT_USERNAME=mongodbadmin
#      - MONGO_INITDB_ROOT_PASSWORD=P@ssw0rd
    volumes:
      - ./init-mongo.js/docker-entrypoint-initdb.d/init-mongo.js
      - ./mongo-volume:/data/db
    ports:
      - '27017-27019:27017-27019'
  sonarqube:
    image: sonarqube
    container_name: 'llorente_local_sonarqube_container'
    ports:
      - '9016-9017:9016-9017'
volumes:
  logvolume01: {}
  ```

Create init script for db or manually run them in mongo shell:

```js
use admin;
db.createUser({user:"mongodbadmin",pwd:"P@ssw0rd",roles:[{role:"root",db:"admin"}],passwordDigestor:"server"});
db.createUser({user:"adppadmin",pwd:"P@ssw0rd",roles:[{role:"readWriteAnyDatabase",db:"admin"}],passwordDigestor:"server"});
db.createUser({user:"carolllorente",pwd:"P@ssw0rd",roles:[{role:"readWrite",db:"admin"}],passwordDigestor:"server"});
```