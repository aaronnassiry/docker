  220  docker info
  221  docker ls
  222  docker run hello-world
  223  docker container ls --all
  224  docker ps -aq --no-trunc -f status=exited | xargs docker rm
  225  docker container ls --all
  226  docker images -q --filter dangling=true | xargs docker rmi
  227  docker container ls --all
  228  docker ps -aq --no-trunc  | xargs docker rm
  230  docker stop 94375b1543db
  231  docker rm 94375b1543db
  232  docker container ls --all
  243  docker image rm -f e63300dbfb4e
  244  docker image ls
  275  docker login
  276  docker build -t friendlyhello .
  277  docker image ls
  278  docker run -p 4000:80 friendlyhello
  299  docker container ls
  300  curl http://localhost:4000
  301  jpwd
  302  vi app.py 
  303  vi requirements.txt
  docker build -t friendlyhello .  # Create image using this directory's Dockerfile
docker run -p 4000:80 friendlyhello  # Run "friendlyname" mapping port 4000 to 80
docker run -d -p 4000:80 friendlyhello         # Same thing, but in detached mode
docker container ls                                # List all running containers
docker container ls -a             # List all containers, even those not running
docker container stop <hash>           # Gracefully stop the specified container
docker container kill <hash>         # Force shutdown of the specified container
docker container rm <hash>        # Remove specified container from this machine
docker container rm $(docker container ls -a -q)         # Remove all containers
docker image ls -a                             # List all images on this machine
docker image rm <image id>            # Remove specified image from this machine
docker image rm $(docker image ls -a -q)   # Remove all images from this machine
docker login             # Log in this CLI session using your Docker credentials
docker tag <image> username/repository:tag  # Tag <image> for upload to registry
docker push username/repository:tag            # Upload tagged image to registry
docker run username/repository:tag                   # Run image from a registry
docker run -d -p 4000:80 hnassiry/hnassiry:hello

docker swarm init
Swarm initialized: current node (lmv03lcwom24in5ahr3w19h2a) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-3ia0kfkadh87zga7u8kxu53etcygxrrg41dd0m161yb0x9xy50-7k7lklooyprfwrzahznoxmeoe 192.168.65.3:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.

docker stack deploy -c docker-compose.yml helloaaron
  459  docker service ls


  493  docker-machine rm $(docker-machine ls -q)
       docker-machine ls
  502  docker-machine create --driver virtualbox aaronvm1
  503  docker-machine create --driver virtualbox aaronvm2
  505  ssh aaronvm1
  506  ping aaronvm1
  510  docker-machine ssh aaronvm1
  511  docker-machine ssh aaronvm2


docker stack ls                                            # List stacks or apps
docker stack deploy -c <composefile> <appname>  # Run the specified Compose file
docker service ls                 # List running services associated with an app
docker service ps <service>                  # List tasks associated with an app
docker inspect <task or container>                   # Inspect task or container
docker container ls -q                                      # List container IDs
docker stack rm <appname>                             # Tear down an application
docker swarm leave --force      # Take down a single node swarm from the manager


docker commit --message "update admin passwd" f2e0524d78ec hnassiry/blueocean:1
docker push hnassiry/blueocean:1
docker run -v /tmp/jenkins:/var/jenkins_home -p 8080:8080 hnassiry/blueocean:1
docker run -v /Users/anassiry/jenkins_home:/var/jenkins_home -d -p 8080:8080 hnassiry/blueocean:1

 => pwd
/Users/anassiry/kub/containers/jenkins

-rw-r--r--    1 anassiry  wheel   433B Oct  4 19:05 Dockerfile
drwxr-xr-x  375 anassiry  wheel    12K Oct  4 19:01 plugins/
drwxr-xr-x    3 anassiry  wheel    96B Oct  4 19:09 users/

cat Dockerfile 
# Use an official Python runtime as a parent image
FROM hnassiry/aaron-blueocean:1 

# Copy the current directory contents into the container at /app
COPY plugins /var/jenkins_home/plugins
COPY jobs    /var/jenkins_home/jobs
COPY users   /var/jenkins_home/users

docker build -t aaron-blueocean:2 .
docker tag aaron-blueocean:2 hnassiry/aaron-blueocean:2
docker push hnassiry/aaron-blueocean:2

 docker run   --rm   -u root  -d  -p 8080:8080   -v /Users/anassiry/jenkins_home:/var/jenkins_home   -v /Users/anassiry/jenkins_home/docker.sock:/var/run/docker.sock   -v /Users/anassiry/jenkins_home:/home  hnassiry/aaron-blueocean:2

 ~/jenkins_home/plugins @ anassiry-ltm2 (anassiry) 
| => ls |wc -l
     373

=======================

docker run -v /var/jenkins_home --name=from-data busybox true
docker run -t -i -d -u root -p 8080:8080 -p 50004:50004 --volumes-from=from-data --name=from hnassiry/aaron-blueocean:3
docker run -t -i --rm --volumes-from=from-data -v /tmp:/tmp ubuntu bash

cat /var/jenkins_home/secrets/initialAdminPassword 
1cc8de69df594077b4823a032da5a974
cp -r /tmp/jobs/*    /var/jenkins_home/jobs/
cp -r /tmp/plugins/* /var/jenkins_home/plugins/
cp -r /Users/anassiry/.jenkins/tools/* /var/jenkins_home/tools

=======================================

JAVA_HOME=/var/jenkins_home/tools/hudson.model.JDK/jdk8
PATH=$PATH:/var/jenkins_home/tools/hudson.model.JDK/jdk8/bin/:/var/jenkins_home/tools/hudson.tasks.Maven_MavenInstallation/maven3.5.4/bin




http://localhost:8080/restart

=============================================

docker run -d -v /Users/anassiry/jenkins_home:/var/jenkins_home -p 8181:8080 -p 50005:50005 hnassiry/aaron-blueocean:4

docker-compose up -d --scale database=4
https://github.com/spotify/docker-maven-plugin

java -cp maven-quick-start-1.0.jar clinic.programming.training.Application
https://maven.apache.org/plugins/

