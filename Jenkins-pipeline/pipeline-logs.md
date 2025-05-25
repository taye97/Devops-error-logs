# DevOps Troubleshooting Log

A personal log of errors I've encountered while working on DevOps projects; building multibranch pipelines etc 

---

## Error 1: Docker Daemon Permission Denied

## Error Message:
Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock
## Cause:
Jenkins (inside a Docker container) does not have permission to access the Docker daemon socket on the host machine.
## solution:
- sudo chown root:docker /var/run/docker.sock
- sudo chmod 666 /var/run/docker.sock
- groupadd docker
- usermod -aG docker jenkins


## Error 2: for pythonapp2_app_1  'ContainerConfig'
Repeated error messages related to ContainerConfig while building the container, specifically for the pythonapp2_app_1 service.
 ## Cause :
 The container had been rebuilt multiple times without cleaning up previous containers. Old orphaned containers were still lingering because the previous builds did not include cleanup commands in my Jenkinsfile
 ## solution
 - docker-compose down --remove-orphan
 - docker-compose up --force-recreate -d

 ## Error 3: chmod: changing permissions of '/var/jenkins_home/.ssh/id_rsa': Operation not permitted
 ## Cause:
  chmod inside a Docker container or as a user (like jenkins) that doesn't own the file.
 ## solution
 -  docker exec -it -u root jenkins-container bash
 - chown jenkins:jenkins /var/jenkins_home/.ssh/id_rsa
  - chmod 600 /var/jenkins_home/.ssh/id_rsa
  - chmod 644 /var/jenkins_home/.ssh/known_hosts

  ## Error 4: 



