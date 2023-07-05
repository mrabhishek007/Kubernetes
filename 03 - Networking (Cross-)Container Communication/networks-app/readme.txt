Since Docker controls the environment in which application runs
It can resolve the ip address on the fly when any http request occurs inside container.

1. Communication with Host Machine from container.
"host.docker.internal" can be used for accessing Host Ip address Inside the container.
Ex: 'mongodb://host.docker.internal:27017/swfavorites'

2. Making Communication between Containers.

    a. A network has to be created manually an attached to the container in order to expose network request fro that container
       Run following Command to create a network.
       >> docker network create "network name"



To run the above application follow following command.

// Creates a "mongo-net" network which will be used to establish network connection with "node app" container
1. docker network create mongo-net

// This will download "mongo" image and create a "mongodb" container which gets attached to mongo-net network
2. docker run -d \
   --name mongodb \
   --network mongo-net \
    mongo

3. Use the container name in ip address which will get resolved by Docker when http calls occurs.
   Ex: 'mongodb://mongodb:27017/swfavorites'

4. Run the following command to create the node app container.
   >> docker build -t favorites:v1 .
   >> docker run \
      -p 3000:3000 \
      --rm \
      --name favorites-app \
      --network mongo-net \
      favorites:v1


