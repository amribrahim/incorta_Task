# incorta_Task
in order to Deploy the code you should first have docker run on your machine 
in my case in use ubuntu so you can follow the instruction in the Dcoument below to install it:
https://docs.docker.com/v17.09/engine/installation/linux/docker-ce/ubuntu/#os-requirements
## Follow the following instuction to run and deploy the application 
 - clone the Repo 
 - you should found 4 folders contains docker files and dependinces should found in the images 
 - cd to all folders and build the images by run: 
 ```
 docker build -t image_name . 
 ```
- after this steps you now have four docker 3 for microservices application and the last for nginx to make reverse proxy 
- the next step create two docker networks to seperate the application when run the containers 
```
docker network create net1
docker network create net2 
```
- then run the images by the following commands:
``` 
docker run --name mynginx1 -p 8000:8000 -d --network net1  image_name_for_nginx:latest   
docker network connect net2 mynginx1 
docker restart mynginx1 
docker run --name country -d --network net1 image_name_for_country:latest 
docker run --name airport -d --network net2 image_name_for_airport:latest 
```
- now you can run the application on browser by typing 
   - localhost:8000/countries 
   - localhost:8000/airports 
