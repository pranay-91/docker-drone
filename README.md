# Drone Sever using Docker

## This repository contains a demo configuration of drone 

### Drone Server environment config
DRONE_GITHUB=true
DRONE_GITHUB_CLIENT=
DRONE_GITHUB_SECRET=
DRONE_OPEN=true
DRONE_SECRET=drone
#DRONE_SERVER_CERT=certs/ca.crt
#DRONE_SERVER_HOST=http://ec2-34-212-6-229.us-west-2.compute.amazonaws.com
DOCKER_TLS_VERIFY=0
DRONE_DEBUG=TRUE


### Drone agent environment config
DRONE_DEBUG=true
DRONE_SECRET=drone
DRONE_SERVER=ws://server:8000/ws/broker
DOCKER_TLS_VERIFY=0


### Running docker images
docker run -p 3000:3000 -d --name <app-latest> myregistry.com:5000/<uname>/<app:latest>

### Drone Yaml

pipeline:
  build:
    image: node:latest
    commands:
      - npm install
      - npm test


#Docker hub settings
#  publish:
#    image: plugins/docker
#    repo: pranay91/cicd_test_app
#    tags: [1, 1.1, latest]
#    secrets: [ docker_username, docker_password ]


#Docker remote registry
 publish:
   image: plugins/docker
   repo: myregistry.com:5000/<uname>/<app>
   insecure: true
   registry: myregistry.com:5000
   tags: [1, 1.1, latest]
   secrets: [docker_username, docker_password]

### Manage secrets using DRONE CLI . Do not forget to authenticate CLI by passing environment variables for registry server
