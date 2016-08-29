![](../NuppLogo.png)

# Nupp Database

## MongoDB Authentication

now that the replica set is configure with Access Control Security

for every movement in the database we have to authenticate at the mongod server

and then we are ready to execute commands on mongo shell

## Access to Mongo with Access Control

usign any mongo command followed by this parameters

Example:
(mongo|mongorestore|mongoimport) --host {host} -d {database name} -u "{user}" -p "{password}" --authenticationDatabase "admin" --dir={database dump path}

## References:

For managing mongo volumes

- [Walkthrough: Docker Volumes vs Docker Volumes with Flocker](https://clusterhq.com/2015/12/09/difference-docker-volumes-flocker-volumes/)

For configuring access control to MongoDB and replica set with Docker

- [Creating a MongoDB replica set using Docker ](http://www.sohamkamani.com/blog/2016/06/30/docker-mongo-replica-set/)

- [MongoDB Docs | Enable Internal Authentication](https://docs.mongodb.com/v3.0/tutorial/enable-internal-authentication/)

- [Deploy a MongoDB Cluster in 9 steps Using Docker](https://medium.com/@gargar454/deploy-a-mongodb-cluster-in-steps-9-using-docker-49205e231319#.ouvzsmyar)
