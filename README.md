# VCC END TERM PROJECT

# Team Description

The team consists of two members from the UG-2022 batch. They are:
Manul Goyal (B18CSE031)
Manan Rakeshkumar Shah (B18CSE030)

# Instructions for Running

1. Make sure you have docker and docker-compose installed.
2. Clone this respository and navigate into the repository folder.
3. Run the following:
`$ docker-compose up`
4. All four containers will be created automatically. You can go to localhost:8888 in your browser to access the chronograf management UI and see the system metrics data.

# Stepwise Description
We have written a docker-compose.yaml file which describes the creation of the four containers, sets up a new bridge network, and attaches all four containers to this newly created network. It also specifies the environment variables, port mappings, and mount volumes. The directories containing the configuration files as well as the directories for the data are mounted in the containers, in order to give access of the configuration files to the containers and to persist the data in the time-series database across container restarts.
We used the following official docker images from DockerHub for the four TICK stack components:


- influxdb:1.8
- telegraf:latest 
- kapacitor:latest
- chronograf:latest


We have setup telegraf to read the system data such as running processes, memory and disk IO usage, CPU usage and network usage. Telegraf sends this time-series data to influxdb, which is then read by chronograf and displayed in a user-friendly format in the browser. We have also setup an alert rule using kapacitor to display alerts on the UI whenever the system load exceeds a certain threshold.
We have deployed the project on a Ubuntu 20.04 droplet in DigitalOcean. We have setup GitHub OAuth 2.0 based authorization for chronograf, to prevent unauthorized access to the web UI (more details in the next section). 

# List of all security measures implemented
- We have created a separate bridged network named “vcc-net-secure”, and attached all four containers to this network. This ensures that the containers are on their own private network which is isolated from any other containers on the default network. No container outside this bridged network can communicate with these four containers, thus ensuring security.
- We have setup GitHub OAuth 2.0 based authorization for Chronograf, to prevent unauthorized access to the web UI. For this, we created a GitHub organization named “vcc-end-term-project-org”, and added both team members to this organization. We setup Chronograf to allow access to the UI only to the GitHub users who are part of this organization, so any external users can’t access the management UI.
