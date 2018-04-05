# concourse-up
A Quick setup of a concourse server with Docker Compose with reference from https://github.com/concourse/concourse-docker

# Prerequisites
  - Certificates and keys generated and exchanged for the web and workers (ref section below)
  - Docker is installed (Compose should be installed with it) ref https://docs.docker.com/install/

# Setting up Certificates and keys

Run the commands below to create the folders and exchange keys used for communications between the web and worker processes

mkdir -p ~/Dev/docker/keys/web ~/Dev/docker/keys/worker ~/Dev/docker/mounts/concourse/worker

ssh-keygen -t rsa -f ~/Dev/docker/keys/web/tsa_host_key -N ''
ssh-keygen -t rsa -f ~/Dev/docker/keys/web/session_signing_key -N ''

ssh-keygen -t rsa -f ~/Dev/docker/keys/worker/worker_key -N ''

cp ./keys/worker/worker_key.pub ~/Dev/docker/keys/web/authorized_worker_keys
cp ./keys/web/tsa_host_key.pub ~/Dev/docker/keys/worker

# Usage
Disclaimer: if other folder locations are used other than the ones specified above, update the locations in the docker-compose.yml

- Copy docker-compose.yml file to any file location
- start up the instances with 'docker-compose up' ('docker-compose up -d' for detached processes)
- shutdown and clean up processes with 'docker-compose down'

Direct your feedback to Jason at hklee@pivotal.io
