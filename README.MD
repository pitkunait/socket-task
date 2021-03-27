# Socket stdin server and client

Project has two containers, python server and .NET client

If `make` is available, then:
1. Run `make build`
2. Open the server with `make runserver`
3. Open the client with `make runclient`

If `make` is unavailable, then:
1. Run `docker network create stdin-network` to create bridge network for containers.
2. Run `docker build -t stdin-server server` to build server image.
3. Run `docker build -t stdin-client client` to build client image.
4. Start the server with `docker run -it --name stdin-server --network stdin-network -p 8765:8765 stdin-server`. 
   This will expose socket port, name the container and add the container to the network. Also, it will run the container
   in interactive mode so that you can type into standard input of the program.
5. Start the client with `docker run -it --name stdin-client --network stdin-network --env-file .env stdin-client`. 
   This wil name the container, add it to the network and add environment variables to the container.
   
   
Once the client is connected to the server, you can type into standard input in the server and each key is sent to
server through socket connection.