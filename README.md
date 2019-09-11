# Hello Node

*ORIGINAL README*
```
This is a very basic Hello World application written with Node.

It includes a `Dockerfile` for building a Docker image with the application, and a `Jenkinsfile` that defines a build pipeline for it.

https://getintodevops.com
```

## Changes by /u/pythoninthegrass
* [System-wide DNS in containers](https://meta.discourse.org/t/failed-to-bootstrap-ping-is-working-to-github/23869/6) `/etc/default/docker`: `DOCKER_OPTS="--dns 1.1.1.1 --dns 1.0.0.1"`
* Jenkins [initialize stage to install docker](https://stackoverflow.com/questions/44850565/docker-not-found-when-building-docker-image-using-docker-jenkins-container-pipel) via Jenkinsfile + Jenkins Global Tool Configuration
```
stage('Initialize'){
        def dockerHome = tool 'my_docker'
        env.PATH = "${dockerHome}/bin:${env.PATH}"
    }
```
* From same [SO thread](https://stackoverflow.com/questions/44850565/docker-not-found-when-building-docker-image-using-docker-jenkins-container-pipel), bound host Docker with run/compose variables
```
-v /var/run/docker.sock:/var/run/docker.sock
-v /usr/bin/docker:/usr/bin/docker
```
* Tailored [jenkins-docker-compose.yml](https://gist.github.com/pythoninthegrass/abb755a54ba908374e1c8bfd79d0c499) files for master and slave Jenkins containers
* [JNLP slave](https://github.com/jenkinsci/docker-jnlp-slave) configuration at [Medium](https://medium.com/@prashant.vats/jenkins-master-and-slave-with-docker-b993dd031cbd)
* Followed [first](https://getintodevops.com/blog/the-simple-way-to-run-docker-in-docker-for-ci) and [second](https://getintodevops.com/blog/building-your-first-docker-image-with-jenkins-2-guide-for-developers) guide from _Get Into DevOps_ after setting up infra
