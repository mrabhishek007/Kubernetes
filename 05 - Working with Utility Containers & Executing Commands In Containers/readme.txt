Utility Containers can be used to run applications without installing tools in the host system

EX: Creating a node project on host system can be done using this while node & npm will gte installed in docker instead of installing in host machine.


Here is an example of docker container service configuration which can be used to run custom node related stuff.

node-utils:
    image: node:18-alpine
    working_dir: "/app"
    #  It will accept npm as default executable when node-utils service is run.
    #  EX :docker-compose run "service-name" init will internally run npm init inside container
    #  entrypoint: ["npm"]
    stdin_open: true
    tty: true
    volumes:
      - ./project:/app


To run this use following command:
>> docker-compose run node-utils node -v
>> docker-compose run node-utils npm init
