
1. Build the image by giving a proper name.
   An Image with name "goal" with tag "v1" will get created.

>> docker build -t goal:v1 .



2. Run the application in interactive mode since this app requires user input
   Below command will create a container and run in interactive mode using image: goal:v1
   --rm command will destroy the container once stopped
NOTE : By default "docker run" command runs in attached mode i.e. it will block terminal


>> docker run -p 3000:80  --name goal-app goal:v1


3. For further run we can use the existing created container using following commands:
NOTE : By default "docker start" command runs in de-attached mode i.e. it will not block terminal. To start in deattach state add -i flag

>> docker start -i goal-app


UPGRADING THE IMAGE & CONTAINER IF CHANGES IN FILES:
1. Run the step 1 to rebuild an image
2. Remove the container by using following command:
   >> docker rm existing-container-name
3. Run step 2 again




NOTE : Docker run command is a combination of create and start as it creates a new container and starts it immediately.


