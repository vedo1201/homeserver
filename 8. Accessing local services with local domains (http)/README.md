# How to access selfhosted services with local domains using HTTP
I have already covered how to access your self hosted services with a secure connection, using HTTPS. We were using free domain which we have set up using the DuckDNS. This is the very good way of setting up free HTTPS, but your domain will depend on the DuckDNS.
If you want just to access your self hosted services locally, using custom domains names, you can follow the steps in this guide. Be aware that this does not include SSL Certificate so you wont be able to access services with HTTPS. Services are going to be accessed by HTTPS.
The best thing about this way is that you won expose anything to the internet.

### Let's start
#### 1) Installing dnsmasq
First thing we need to do is to install dnsmasq. We are going to do this by typing commands:

<pre>sudo apt update</pre>
<pre>sudo apt install dnsmasq -y</pre>

#### 2) Configuring dnsmasq
Now we need to configure dnsmasq for our local adresses.
First we need to open dnsmasq configuration file by typing:

<pre>sudo nano /etc/dnsmasq.d/local-domains.conf</pre>

In this file, add this line:

<pre>address=/myapp.local/192.168.1.100</pre>

Replace myapp.local with the service name and domain that you want and replace 192.168.1.100 with your actual IP address
Repeat this as many times as you need. Keep in mind that every address needs to have its own part in config file.

For example, I want to access Portainer using link docker.vedo on ip 192.168.1.11

![image](https://github.com/user-attachments/assets/0962c5f3-4261-4197-884a-8081ff8738c4)

After you have set up all the domain names you want, save the file by pressing CTRL + X, Y and then ENTER

#### 3) Adding domain name to NginxProxyManager
You need to have NginxProxyManager installed. You can find its docker compose file here: [7. Setting up secure access to services (https)](https://github.com/vedo1201/homeserver/tree/b723d57460bf1f5717ce8c2cdd46eeb4639f3fe3/7.%20Setting%20up%20secure%20access%20to%20services%20(https))

1. Open the NginxProxyManager WEB UI by opening this link in your browser:

   <pre>http://{SERVERIP}:81</pre>

Login using your credentials, Go to Hosts and then Proxy Hosts and click Add Proxy Host

![image](https://github.com/user-attachments/assets/29c233ee-a791-4eb2-b803-b9105ebd6060)

Fill out those fields:

![image](https://github.com/user-attachments/assets/99b08dc3-e519-481d-b053-f0c07c606c91)

1. Domain Names - The domain that you have entered in dnsmasq for your service
2. Forward Hostname / IP - Ip of your server
3. Forward Port - The port that your service is running on

This is the example of portainer access using the 'docker.vedo' domain:

![image](https://github.com/user-attachments/assets/a31ba182-a4f8-4245-9a1d-5291e3577624)

Make sure to open the port for service using this command:

   <pre>sudo ufw allow PORTNUMBER</pre>

Click Save.

Now you should be able to access your service using the local domain that you have set up.


