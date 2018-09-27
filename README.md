# teamcity_docker
TeamCity server and agent to run unit tests for MapR Hadoop project

## Run

### Prerequisites
1. Install [docker](https://docs.docker.com/install/) and [docker-compose](https://docs.docker.com/compose/install/)

### Build and run
1. cd teamcity_docker/teamcity/server
2. docker build --rm -t mapr/teamcity-server .
3. docker-compose up -d --scale agent=3 (specify needed number of agents)


### Troubleshooting
1. Unauthorized agents
    - Clean "datadir" on host node before up docker containers