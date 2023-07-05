
1. Build the image by giving a proper name.
   An Image with name "feedback" with tag "v1" will get created.

>> docker build -t feedback:v1 .


2. Run the application in interactive mode since this app requires user input
   Below command will create a container and run in interactive mode using image: feedback:v1
   --rm command will destroy the container once stopped. It will also destroy container data related.
   NOTE : Container has ability to write data. By default Docker container will store the data inside the container. Removing Container will also delete container related data


NOTE : By default "docker run" command runs in attached mode i.e. it will block terminal


>> docker run -p 3000:80  \
   --name feedback-app \
   feedback:v1


3. For further run we can use the existing created container using following commands:
NOTE : By default "docker start" command runs in deattached mode i.e. it will not block terminal. To start in deattach state add -i flag
NOTE : By default Docker container will store the data inside the container. Starting an existin gcontainer will also use load the exisitng container data


>> docker start -i feedback-app


UPGRADING THE IMAGE & CONTAINER IF CHANGES IN FILES:
1. Run the step 1 to rebuild an image
2. Remove the container by using following command:
   >> docker rm existing-container-name
3. Run step 2 again

NOTE : Docker run command is a combination of create and start as it creates a new container and starts it immediately.



Persisting Data Using Volumes:
Persisting data using containers are not recommended since once container get removed data will also get removed. We use volume for presesting data.
** Volume are folders on the host machine hard drive which are mounted into container
** Volume persists if a container shuts down.If a container re-starts and mount a volume, any data inside that volume is available to the container.


**ADDING Anonymous VOLUME IN DOCKER FILE:
>> VOLUME ["/app/feedback]
NOTE: Anonymous Volume Will get destroyed once container is destroyed. Use Named volume for data presistency

**USING NAMED VOLUME FOR DATA PERSISTING:
Run following command while using using docker run to persist volume data:

>> docker run -p 3000:80 \
   --name feedback-app \
   -v feedback:/app/feedback \
   feedback:v1


**Using Bind Mount Volume:
A bind mount is another type of mount, which lets you share a directory from the host’s filesystem into the container.
When working on an application, you can use a bind mount to mount source code into the container.
The container sees the changes you make to the code immediately, as soon as you save a file.
This means that you can run processes in the container that watch for filesystem changes and respond to them.

Add an addition -v flag with absolute path of the source code to use mount path:

>> docker run -p 3000:80 \
   --name feedback-app \
   -v feedback:/app/feedback \
   -v "/Users/vikash/Desktop/personal workspace/Kubernetes/02 - Managing Data & Working with Volumes/data-volumes-08-args-and-env":/app \
    feedback:v1

Problems faced with Bind mounts:
it replaces the entire directory of container with host machine directory. There might be an scenario when you want to also use some of the existing nested directory of container instead of host.
For these scenario we can mention an Anonymous volume while running the container.
Ex:
Above command will give error since node modules is installed inside container and while running host node module are used. Bcz of this application will not run.
Use the following command to fix this issue by overriding node modules of host to container.

>> docker run -p 3000:80 \
   --name feedback-app \
   -v feedback:/app/feedback \
   -v "/Users/vikash/Desktop/personal workspace/Kubernetes/02 - Managing Data & Working with Volumes/data-volumes-08-args-and-env":/app \
   -v /app/node_modules  \
   feedback:v1






