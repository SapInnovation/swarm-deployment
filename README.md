# Swarm Deployment

A guide on how to deploy to Swarm cluster and some sample deployment scripts.

<!-- TOC -->

- [Platform Description](#platform-description)
- [PreRequsite to deploy to Swarm](#prerequsite-to-deploy-to-swarm)
- [Deploying](#deploying)
    - [Manual deployment](#manual-deployment)
    - [Deployment via Concourse - WIP](#deployment-via-concourse---wip)
- [Logging](#logging)

<!-- /TOC -->

## Platform Description

Docker Swarm is the choice for PaaS so that developers don't have to worry about the state of their applications and not of the infrastructure. The platform provides you integrated:

- Deploying and scaling applications
- Logging

## PreRequsite to deploy to Swarm

1. Your application can be containerized.
2. A Dockerfile is available to package the application as a Docker image.
3. A [Docker Hub](https://hub.docker.com) account to push Docker images.
4. Application Docker image has been pushed to Docker hub.
5. Have your application manifest ready according to [Docker stack YAML](https://docs.docker.com/docker-cloud/apps/stack-yaml-reference/).

## Deploying

NOTE: At the moment, deployment to Swarm is manual only. Integration with Concourse is WIP.

### Manual deployment

1. Find out the Swarm Masters' IP and ports (from DevOps Team), say `10.2.3.4`.
2. SSH to the Swarm master and copy your stack yaml (and other config files, if any) on the master in a temporary directory.
2. Assuming Docker stack YAML (and other configuration files) is present at `/tmp/` on Swarm master and stack configuration is in `myapp-stack.yml`, run following command to deploy stack to Swarm:

   ```sh
   export STACK_NAME="myapp-stack"
   cd /tmp
   docker stack deploy $STACK_NAME -c myapp-stack.yml
   ```

   NOTE: Ensure that you are directly able to connect to Swarm Managers from your machine.

### Deployment via Concourse - WIP

WIP

## Logging

Logs for any containers deployed on Swarm are automatically sent to ELK stack running on the same Swarm cluster, **provided** the application in container is putting logs on `stdout` or `stderr` streams (instead of writing it to a file).

Logs can be seen on Kibana by accessing port `5601` of any Swarm node on a browser.