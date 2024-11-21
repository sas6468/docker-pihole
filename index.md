# Pi-hole setup using Docker and Docker Compose
This guide documents the process of setting up Pi-hole, a DNS blackhole application, using Docker and Docker Compose. 
Please follow these steps to replicate the set up.

## **Pre-requisites
1. Set Up the Environment
    *Install Docker Desktop which includes Docker Compose on Ubuntu by following this link: https://docs.docker.com/engine/install/ubuntu/

    Install Docker Compose: https://docs.docker.com/desktop/setup/install/linux/ubuntu/

    Verify Docker Compose installation by running: docker compose version


2. Create a Directory for Pi-hole
    *Open a terminal and create a directory for the Pi-hole project:

    mkdir ~/pihole-docker

    cd ~/pihole-docker

3. Create a docker-compose.yml File
    *Create and edit a docker-compose.yml file using a text editor:

    nano docker-compose.yml

    Add the following content to the file:

    version: "3"

services:
  pihole:
    image: pihole/pihole:latest
    container_name: pihole
    environment:
      TZ: "America/Chicago" # Set your timezone
      WEBPASSWORD: "your_password_here" # Admin password
    volumes:
      - "./etc-pihole:/etc/pihole"
      - "./etc-dnsmasq.d:/etc/dnsmasq.d"
    ports:
      - "80:80"
      - "53:53/tcp"
      - "53:53/udp"
    dns:
      - 127.0.0.1
      - 1.1.1.1
    restart: unless-stopped

version: "3"

4. Run the Application

    *Start the Pi-hole container:
    docker compose up -d

    Check if the container is running:
    docker ps

5. Access the Pi-hole Web Interface

    Open a web browser and go to http://<your-docker-host-ip>/admin.

    Log in using the password you set in the WEBPASSWORD environment variable.


Resources
Docker Official Installation Guide
Docker Compose Official Installation Guide
Pi-hole Docker Documentation
