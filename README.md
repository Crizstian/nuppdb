![](https://github.com/Nupp/nuppdb/raw/master/NuppLogo.png)

# Nupp Database

## MongoDB Authentication

now that the replica set is configure with Access Control Security

for every movement in the database we have to authenticate at the mongod server

and then we are ready to execute commands on mongo shell

## Create the mongo database with replica set
Start one container to configure the volume
```
docker run --name some-db -v some-volume-for-persistence:/data -d crizstian/nuppdb --smallfiles --dbpath /data/rs
```
Create some admin users as mongo docs recommends
```
docker exec some-db bash -c 'mongo < /tmp/create-user-admin.js'
```
Copy the keyfile to the mongodb

```
docker exec some-db bash -c 'echo "$PASS" | sudo -S chown -R nupp:nupp /data/keyfile/mongodb-keyfile
```
remove container to restart new one with the replica-set config

`docker rm -f some-db`

create container with sercurity and replica configuration

```
docker run --name some-db --hostname some-db {--add-host some-servers} -v some-volume-for-persistence:/data 
           --env-file env-file -p outer-port-binding
           -d crizstian/nuppdb --smallfiles --keyFile /data/keyfile/mongodb-keyfile
           --replSet rs1 --storageEngine wiredTiger --dbpath /data/rs --port inner-port
```

## Access to Mongo with Access Control

using any mongo command followed by this parameters

Example:
```
(mongo|mongorestore|mongoimport) --host {host} -d {database name} -u "{user}" -p "{password}" --authenticationDatabase "admin" --dir={database dump path}
```

## References:

For managing mongo volumes

- [Walkthrough: Docker Volumes vs Docker Volumes with Flocker](https://clusterhq.com/2015/12/09/difference-docker-volumes-flocker-volumes/)

For configuring access control to MongoDB and replica set with Docker

- [Creating a MongoDB replica set using Docker ](http://www.sohamkamani.com/blog/2016/06/30/docker-mongo-replica-set/)

- [MongoDB Docs | Enable Internal Authentication](https://docs.mongodb.com/v3.0/tutorial/enable-internal-authentication/)

- [Deploy a MongoDB Cluster in 9 steps Using Docker](https://medium.com/@gargar454/deploy-a-mongodb-cluster-in-steps-9-using-docker-49205e231319#.ouvzsmyar)
