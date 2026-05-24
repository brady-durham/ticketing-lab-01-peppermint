# Ticketing Lab 01 — Peppermint Help Desk

**Brady Durham | Nashville, TN | IT Support & Sysadmin Portfolio**

A hands-on ticketing lab deploying Peppermint, an open-source help desk system, using Docker on Ubuntu. Includes a full ticket interrupt scenario worked through using OSI model troubleshooting methodology.

## Objectives

- Deploy a real-world ticketing system using Docker and Docker Compose
- Configure Peppermint with users, clients, and ticket categories
- Practice creating, commenting, assigning, and escalating tickets
- Apply OSI model troubleshooting to a simulated help desk scenario

  ## Environment

- Host OS: Ubuntu 24.04 Desktop (VM on Proxmox)
- Docker: Docker Engine 29.1.3
- Docker Compose: v2.40.3
- Ticketing System: Peppermint v0.5.5
- Database: PostgreSQL 15

## Installation

### Step 1 — Install Docker

sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker

Verify installation:
sudo docker run hello-world

### Step 2 — Install Docker Compose v2

sudo apt install docker-compose-v2 -y

### Step 3 — Download Compose File

mkdir peppermint && cd peppermint
curl -o docker-compose.yml https://raw.githubusercontent.com/Peppermint-Lab/peppermint/master/docker-compose.yml

### Step 4 — Fix PostgreSQL Version

sed -i 's/postgres:latest/postgres:15/g' docker-compose.yml

### Step 5 — Start Peppermint

sudo docker compose up -d

### Step 6 — Access Peppermint

Open browser and go to http://localhost:1000
Default login: admin@admin.com / 1234

## Ticket Interrupt — Internet Connectivity Issue

### Scenario

Ticket #5563284: Help! Internet won't work!
User connected via ethernet on 10.0.0.0/24 network. Gateway is 10.0.0.1.

### Troubleshooting Steps

Layer 1 — Physical: Had user check cable was plugged in, checked for damage, confirmed link light was on NIC.

Layer 2 — Data Link: Had user check data light flashing on NIC. Ran arp -a to confirm gateway MAC address in ARP table.

Layer 3 — Network: Had user run ipconfig to verify IP on correct subnet. Confirmed gateway reachable via ping. User unable to ping google.com. Ran ipconfig /release, /flushdns, /renew, /registerdns — none resolved issue. Ran tracert and confirmed connectivity dropped at gateway.

Escalation: Reached end of troubleshooting workflow — ticket escalated to next support level with full documentation.

## Troubleshooting Notes

- docker-compose Python error — installed docker-com
