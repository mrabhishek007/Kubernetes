
1. Build the image by giving a proper name.
   An Image with name "random-number" with tag "latest" will get created.

>> docker build -t random-number:latest .



2. Run the application in interactive mode since this app requires user input
   Below command will create a conatiner and run in interactive mode using image: random-number:latest
   --rm command will destroy the container once stopped


>> docker run -i \
   --rm \
   --name random-number-app \
   random-number:latest


3. For further run we can use the existing created container using following commands:

>> docker start -i random-number-app





