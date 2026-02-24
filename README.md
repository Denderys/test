# test
-layer3
-OS
-MagicEden
-rbtn
-rubiscore
-humster
-twitter
Tempo node
#moderato
sudo apt update && sudo apt upgrade -y
sudo apt install curl wget git build-essential jq -y
##

##Revapay



--Dr?


#!/bin/bash

echo "Updating system..."
sudo apt update && sudo apt upgrade -y

echo "Installing dependencies..."
sudo apt install curl wget git docker.io docker-compose -y

sudo systemctl enable docker
sudo systemctl start docker

echo "Cloning Tempo repository..."
git clone https://github.com/tempo-network/tempo.git
cd tempo

echo "Starting node..."
docker compose up -d

echo "Tempo node installation completed!"

#serv param
2gb ram
