# Basic things to do right after installing Ubuntu Server
On this page, your are going to find some things that are must to do if you want clean after install setup of server.
## Let's start

### 1. Setting up static ip address
The most important thing to do, when speaking generally about home servers, is to set up a static IP address. The servers IP is going to be used to access basically every service on our server,
so it is important for it not to change every time server restarts. Because of this, the very first thing to do after booting into server is to set up static IP. This can be done by two ways, either
setting up the static ip in router settings, or directly on server.

#### 1.1. Setting up the static ip in router settings (easiest)
1. First thing you have to do is to find your routers ip address. If you are using windows, this can be done by opening command prompt and entering the command 'ipconfig'.
   Your routers ip is going to be labeled as default gateway

   ![{D5582946-7DF2-463C-BA3C-56D014BDCA5D}](https://github.com/user-attachments/assets/d047460e-a7b6-4a38-8217-c4b40ed629ed)

2. Open up your web browser, enter this ip in search bar and press enter. You should be redirected to the configuration page of your router that looks something like this:

   ![{C6E727C7-F473-4E1F-93A5-259D8576D484}](https://github.com/user-attachments/assets/b6d58b91-0261-4135-b3bc-5a70e16a5039)

   After visiting this page, you should be able to login. To find the username and password for your router, you can check the back side of router or look for it on google by searching
   router model + 'login credentials'

3. After you've logged in, go trough the router pages and find the page that is called 'LAN'. On that same page you can find the 'DHCP Binding' tab in which you are going to put
   informations about server (can be found in connected devices table in router settings).

   For the example:

    ![{9CBC0A9B-F45F-46F3-983E-663115118B18}](https://github.com/user-attachments/assets/2cb7a3ac-7725-45a0-adc2-3b60106483ad)

4. Click apply

   **And now your server ip is not going to change.**





#### 1.2. Setting up the static ip in servers network config file
Another way to set up static ip on ubuntu server is a bit different. You must edit some configuration files in system.
Here is the guide:

1. First, you need to check name of your network interface in your terminal. To do this, type: 

<pre> ip link </pre>

   You will get output similar to this:

<pre> 2: enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 ... </pre>

   In my case, name of network adapter is 'enp2s0'. Remember it because we will need it in config files.


2. Now, you must find the netplan config file and open it in text editor.
   To do this type:

<pre> cd /etc/netplan </pre>

   With this command, you will enter netplan folder. Now we need to find the config file name, and to do this, type:

<pre> ls </pre>

You will get output similar to this:

<pre> 50-cloud-init.yaml </pre>

Now, to open it type this command:

<pre> sudo nano 50-cloud-init.yaml </pre>

Replace <ins>50-cloud-init.yaml</ins> with the name of the file from the step above.

3. Delete everything from that file and replace it with this:

```bash
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: no
      addresses:
        - 192.168.1.100/24
      gateway4: 192.168.1.1
      nameservers:
        addresses:
          - 8.8.8.8
          - 1.1.1.1

```

4. After you've done that, you need to replace some values from this config with your own:

   a) <ins>enp0s3</ins> with the name of your adapter that you have found previously with command <ins>ip link</ins> <br>
   b) <ins>addresses</ins> with static ip that you want to assign to server <br>
   c) <ins>gateway4</ins> with ip address of your router <br>
   d) <ins>nameservers</ins> keep those or change to your prefferred one <br>

After this, you need to restart your server by typing:

<pre> sudo reboot </pre>

Ant that was the other way to set up static ip.

### 2. Update & Upgrade
Now we want our system to have latest packages which are going to improve system security and stability.
First, you need to check for available updates by typing:

<pre> sudo apt update </pre>

After the system finds latest updates, you need to install them by typing:

<pre> sudo apt upgrade -y </pre>

Then, clean the system after updating by typing:

<pre> sudo apt autoremove -y </pre>

After updates are installed, restart your server by typing

<pre> sudo reboot </pre>

### 3. Setting up automatic updates
To make sure our system is always up to date, without needing to do manual update every time, we are going to install unattended upgrades by typing:

<pre> sudo apt install unattended-upgrades && sudo dpkg-reconfigure --priority=low unattended-upgrades  </pre>

On the screen that pops up, chose <ins> Yes </ins> and press ENTER


