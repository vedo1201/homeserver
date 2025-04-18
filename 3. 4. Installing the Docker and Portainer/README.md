# Installation of Docker and portainer

We will use docker in our server to manage containers. To make things easier, we are going to deploy docker container called <ins>Portainer</ins>	which will help us to manage, create, delete and monitor
all of our containers trough the WEB UI.

## 1. Docker Installation

Installing Docker is easy and involves several steps that are explained in next steps.
Run these commands in order for installation of docker, and also docker compose if you want to deploy containers from terminal directly.

To install docker, type these commands one by one in terminal:

  <pre>sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin </pre>

To check if Docker is successfully installed, run this command:

<pre>sudo docker ps</pre>

If you get an output like this, you are good to go.

![{48B480C1-F964-45D9-9EB2-B1A8DF995C64}](https://github.com/user-attachments/assets/9485eb92-fe15-42b3-8cdd-70cd5dbe3c22)

## 2. Portainer Installation

Now, we will install Portainer as docker container.
First you need to create docker volume for Portainer data. Do this by typing:

<pre>sudo docker volume create portainer_data</pre>

After that, install the Portainer by running:

<pre>sudo docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:lts</pre>

## 3. Accessing Portainer WebUI

To access Portainer WebUI, open up your browser and access this link:

<pre>https://{SERVER_IP}:9443</pre>

Replace {SERVER_IP} with the real IP of your server.

Press ENTER and you will be presented with Portainer WEB UI.

If it does not load, you need to open port for Portainer by typing the following command in terminal:

<pre>sudo ufw allow 9443</pre>

After that, try again.

## 4. Setting up Portainer user data

When you open the Portainer WEB UI for the first time, you will be presented with this screen:

![image](https://github.com/user-attachments/assets/a1bafb46-3857-489e-b011-4b6f82971155)

Set up your password and click 'Create User'

On the next page, chose the 'Get Started' environment and you will be ready to go.


