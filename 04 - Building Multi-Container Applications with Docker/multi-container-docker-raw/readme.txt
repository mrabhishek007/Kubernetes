

Building Mongo:
1. docker network create mongo-net

2. Persisting mongo data using named volume and creating mongo network
 docker run \
 --rm \
 --name mongodb \
 -v mongo-data:/data/db \
 -d \
 --network mongo-net  mongo

3. Update the mongo connection url like following in node app:
   >> mongodb://mongodb:27017/course-goals?authSource=admin // here ://"mongodb" is container name


Building Backend:
1. docker build -t goals-node .

2.
// accessing mongodb network inside backend container
// Using mount volume for live source code update, Persisting container logs to host logs folder & using container node modules
  docker run \
  --rm \
  --name goals-backend \
  -p 80:80 \
  --network mongo-net \
  -v "/Users/vikash/Desktop/personal workspace/Kubernetes/04 - Building Multi-Container Applications with Docker/multi-02-finished/backend":/app \
  -v logs:/app/logs \
  -v /app/node_modules \
  goals-node


Building Frontend:
1. docker build -t goals-react .
2. docker run --rm \
    -it \
    --name goals-frontend \
    -p 3000:3000 \
    -v "/Users/vikash/Desktop/personal workspace/Kubernetes/04 - Building Multi-Container Applications with Docker/multi-02-finished/frontend":/app \
    -v /app/node_modules \
    goals-react
