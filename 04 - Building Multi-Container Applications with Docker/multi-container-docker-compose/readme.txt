Docker Compose :
1. Network is not needed bcz default network is auto created by compose and attach network with all of the containers. Overriding is allowed
2. -it flag can be defined in docker-compose using     stdin_open: true && tty: true
