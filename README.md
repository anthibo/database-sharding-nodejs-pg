# Implementing a simple url shortner demo with consistent hashing and database sharding
This is a simple demo of database sharding in postgres using nodejs, the idea here that to hash urls and save the hash in different sharded databases 
by using consistent hashing on the url hased id to get database server of the sharded database using hashring package.

## Setup:
To install packages
```
npm i
```
To build an image of pg-database with url table
go to db-image dir and then run this command
```shell
docker build -t pgshard .
```
to create 3 container instances of pgshard image
```
docker run --name shard1 -p 5433:5432 pgshard
docker run --name shard2 -p 5434:5432 pgshard
docker run --name shard3 -p 5435:5432 pgshard
```
then u can start the server and test the endpoints.
```
node index.js
```
## Endpoints:
- save a url to a sharded db:
  ``` 
  POST: http://localhost:8081/?url=http://stackoverflow.com
  ```
 - get the url hash of a saved url
    ```
    GET: http://localhost:8081/:url_hash
    ```

