
# CLO8355 Assignment 1

This assignment demonstrates the ability to run containers within the same network and utilize container names for traffic routing.

## 1. Build python app image
```
docker build -t clo835-assignment-1 .
```

## 2. Create docker network
```
docker network create clo835-assignment-1-network
```

## 3. Run mongo container in created network with name "mongodb"
```
docker run --name mongodb -d -p 27017:27017 --network clo835-assignment-1-network -v my_mongo_data:/data/db mongo:latest
```

## 4. Run python app container in created network

```
docker run --name my-python-app -d -p 3000:3000 --network clo835-assignment-1-network clo835-assignment-1
```

## Using the Application

To interact with the application, you can use the following `curl` command to create a new item in the database:

```bash
curl -X POST http://localhost:3000/items \
     -H "Content-Type: application/json" \
     -d '{"id": "4", "name": "maziar"}'
```
