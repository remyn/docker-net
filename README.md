# docker-net

 Creating an asp-net core docker container to be deployed on Linux.  
 We are assuming you have already set up the Linux box.

 **Note**: it has been done with the rc1. Since rc2 the tooling cli changed, for a better unified experience !
 
## Dockerfile

 * Add the `dockerfile` to the project folder - _containing the project.json file_:

  >FROM microsoft/aspnet:1.0.0-rc1-update1-coreclr  
  >ADD . /app  
  >WORKDIR /app/approot  
  >ENTRYPOINT ["./web"]  

## Build the container

 * From the project folder , execute the following to publish your project into a temporary folder:  
 `dnu publish -o C:\temp\Folder`
 
 * Build the container image for your project:  
 `docker build -t ImageName -f C:\Temp\Folder\approot\src\NameOfProject\dockerfile C:\Temp\Folder`
 
 * Check the image has been created:  
 `docker images`
 
## Run the container

 * Assuming you had the following _command_ block into your `project.json` file:
 
  > "commands": {  
  >  "web": "Microsoft.AspNet.Server.Kestrel --server.urls http://*:5000"  
  >},  
 
 * you should be able to start your cointainer with:  
 `docker run -t -d -p 5000:5000 --name MyContainerService ImageName`
 
## Check the container

 * List the containers:  
 `docker ps`
 
 * Check the settings:  
 `docker inspect MyContainerService`
 
 * Retreive the IP Address:  
 `docker inspect --format '{{ .NetworkSettings.IPAddress }}' MyContainerService`
 
 * Get the logs:  
 `docker logs MyContainerService`
 
