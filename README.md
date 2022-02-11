# Adjust Task
This repo include all steps and files needed to setup enviroment for Adjust task , first we need to instal the following:
## installation tools
to setup the enviroment you need first to install the following
- Docker to setup minikube use the following link : https://docs.docker.com/engine/install/ubuntu/
- minikube: use the following link : https://minikube.sigs.k8s.io/docs/start/
   - run this command to run docker in non root user to start minikube without error , where the $user is the user you are using during instalation 
   ```
   sudo usermod -aG docker $USER && newgrp docker
   ```
-  kubectl : use the following link : https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/
-  ansbile: use the follwoing link : https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-on-ubuntu
-  clone the Ruby app using this command
```
git clone https://github.com/sawasy/http_server.git
```
## configure the enviroment
the follwing steps show the instructions to configure the enviroment
- Docker file for ruby app like file in the repo to package the app based on Ruby base image
```
   FROM ruby:latest # ruby base image 
   WORKDIR /usr/src/app/ #the working directory
   USER 1000 # non root user id based on /etc/passwd file
   ADD http_server.rb /usr/src/app/  # add ruby file inside the docker 
   EXPOSE 80 # expose port 80
   CMD ["/usr/local/bin/ruby", "/usr/src/app/http_server.rb"] # start ruby app when the app started 
```
- Deployment file  for kubernetes contain 
  - three replicas 
  - probs 
  - secuirty context to start the pod as non root user 
  - ruby image pushed in privete docker hub 
- service file for kubernetes of Type loadbalancer to distribute the traffic accross three replicas
- Ansible play book file contain command needed to automate the deployment
  ```
   docker build -t amribrahim00/ruby-app:latest .  # build the image
   docker push amribrahim00/ruby-app:latest  # push image
   kubectl set image deployment/ruby-app  ruby=amribrahim00/ruby-app:latest # set the pushed image in deployment file
  ``` 
