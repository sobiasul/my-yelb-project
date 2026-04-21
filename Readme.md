Yelb Microservices Architecture
This project implements a high-availability deployment of the Yelb application, consisting of 12 microservices. It features a distributed frontend, an application server layer, and a high-availability cluster for both Redis (using Sentinels) and PostgreSQL.

🏗 Architecture Overview
Frontend: yelb-ui (Angular)

App Server: yelb-appserver (Ruby Sinatra API)

Persistence: yelb-db (PostgreSQL) + 3 Replication Nodes

Cache/State: redis-server (Master) + 2 Replica Nodes

HA Management: 3 Redis Sentinel Nodes

🚀 Deployment Guide (EC2)
1. Prerequisites
Ensure your EC2 instance (recommended t3.medium or larger) has the following installed:

Docker

Docker Compose

2. Installation
Clone this repository onto your EC2 instance:

Bash
git clone <your-repository-url>
cd <your-repository-name>
3. Launching the Application
Run the following command to pull the images and start the services in detached mode:

Bash
sudo docker-compose up -d
4. Accessing the UI
Once the containers are healthy, access the application via your browser:
http://<your-ec2-public-ip>:80

🛠 Configuration Details
Redis High Availability
Sentinel Port: 5000

Redis Port: 6379

Master Name: mymaster

Authentication: Password protected via requirepass and masterauth.

Network & Storage
Driver (Network): Bridge

Driver (Volumes): Local

📂 Project Structure
Plaintext
.
├── docker-compose.yml       # Orchestration file
├── redis-server.conf        # Config for Master Redis
├── odilia-redis01.conf      # Config for Redis Slave 1
├── odilia-redis02.conf      # Config for Redis Slave 2
├── sentinel.conf            # Config for all 3 Sentinels
└── README.md                # This file
Important Checklist Before Running:
Security Groups: Ensure your AWS Security Group allows inbound traffic on Port 80 (HTTP) and Port 22 (SSH).

Memory: This stack runs 12 containers. Monitor memory usage with docker stats.

Build the container

docker compose up --build

docker compose down