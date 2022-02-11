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

