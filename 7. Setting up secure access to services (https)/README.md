# Accessing self hosted services with HTTPS
By default, services hosted on docker are not properly secured. Everytime you want to access your service, you do it by using HTTP and you get warning like this:

![image](https://github.com/user-attachments/assets/81586db9-1dd0-498f-843e-a2c6051d6c20)

As you can see, our connection is not private and secure.

##### We are going to fix this by setting up reverse proxy and getting a free domain name.
#### After that, we will be able to access all of our services securely!

## Let'start

### a) Deploying NginxProxyManager in Docker

As we are going to be accessing multiple services but we will have only one domain, we will use NPM to make subdomains for every service.
We will also use NPM to get SSL certificate for HTTPS access.

#### 1. Docker compose file

Here is the docker-compose.yaml file for nginx proxy manager.

   <pre> services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      - '80:80'
      - '81:81'
      - '443:443'
    volumes:
      - /mnt/ssd/docker/npm/data:/data
      - /mnt/ssd/docker/npm/letsencrypt:/etc/letsencrypt </pre>

#### 2. Opening ports in UFW

After deploying NginxProxyManager in Docker, in order for it to work properly, we need to open ports 80, 81 and 443 by typing:

   <pre> sudo ufw allow 80 </pre>
   <pre> sudo ufw allow 81 </pre>
   <pre> sudo ufw allow 443 </pre>

#### 3. Accessing NginxProxyManager WEB UI

Now we can access NginxProxyManager WEB UI by opennig up a browser and going to this ip:

   <pre> {SERVERIP}:81 # Replace this with your actual server ip</pre>

  You will see a screen like this:

  ![image](https://github.com/user-attachments/assets/8c062050-dfe2-4a18-8f08-a321b1402dcc)

  Login using default credentials:

  <pre> Email address: 'admin@example.com' </pre>
  <pre> Password: 'changeme' </pre>

  After that, set up your name, username and email:

  ![{1927A473-A3B9-40C8-8C7C-4A25BA1ECBBE}](https://github.com/user-attachments/assets/6e941e98-4a4d-4cf2-be33-b0f3092dddd0)

  And your password:

  ![{2144ABEF-2253-4436-8596-C90AC2A68B6A}](https://github.com/user-attachments/assets/191aa0dd-129d-442b-8d3b-97ca35781a97)

  After this is done, you will see this screen:

  ![{B06B6EF0-66F6-4DA1-86EC-25AE3C99A751}](https://github.com/user-attachments/assets/0822e428-8898-4a06-80ce-c92bb44bffd2)


  #### Congratulations, you have set up NginxProxyManager successfully!

  ### b) Setting up DuckDNS

  Now we need to get our free domain. First go to <mark>https://www.duckdns.org/</mark>.
  You will see this page:

  ![{B07F97EE-A5CE-4B77-A1E6-D0B9129820EF}](https://github.com/user-attachments/assets/b2b95466-6952-489a-964f-d916f1c812a9)

  Create account by chosing between some of the options on the top on the page.

  After you have done that, you will se this page:

  ![{240005BD-36C9-4A33-B780-F8B3A70D98AC}](https://github.com/user-attachments/assets/18c812c1-2af2-495c-b7e2-38dcae663b65)

  Here we need to create our domain. Do this by typing domain we want in this box:

  ![{4EF72114-1E75-41C0-A4B4-29D4B3AEDAD1}](https://github.com/user-attachments/assets/1d072e36-ab1f-4dd1-8d24-097beb18fd3d)

  After that, click add domain.

  Now your domain is:

  <pre> http://{name}.duckdns.org </pre>

  In this example:

  ![{D2BFCBF4-414D-4B87-9338-D9B7E8A2DBBA}](https://github.com/user-attachments/assets/24f60d50-fdae-4222-ba64-324fcc988acc)

  Domain is:

  <pre> http://vedads.duckdns.org </pre>

  After you have created domain, you need to link it to your server by typing your server's local ip adress in field 'current ip', and then press 'update ip'.

  ![{01A1F757-17E6-43CC-9CE2-86EE32FE1E2F}](https://github.com/user-attachments/assets/c3289024-275c-4e81-9427-1a69ebcf8e61)

  We are now finished with DuckDNS and our domain is ready for set up.

  ### c) Seting up SSL Certificate in NginxProxyManager

  We now want to connect the domain we created to our NginxProxyManager.
  This is done by going to NginxProxyManager WEB UI by opening:

   <pre> http://{SERVERIP}:81 </pre>

   In the WEB UI go to 'SSL Certificates' tab.

   ![{6C717CEE-2C9F-4F74-832A-38C5BD1E94DA}](https://github.com/user-attachments/assets/d737217f-4e92-4a96-9278-4c1510f3f42c)

   Here, click 'Add SSL Certificate' button and you will get this pop up window:

   ![{B939786C-6DB3-4F12-A671-B892031B8A16}](https://github.com/user-attachments/assets/e57ac44e-cfd3-4626-9f2f-55050fb40e9f)

   Here, we need to fill some cells.

   ##### 1. Domain names - type in your DuckDNS domain, press ENTER and then type that same domain, but add '*.' in front of it and press ENTER. It will look like this:

   ![{FC3F657C-B860-4839-9FFC-D21E7EDFB07F}](https://github.com/user-attachments/assets/dc3367f3-e397-4d4b-a549-4296679b4b7f)

   ##### 2.DNS Challenge
   a) Check 'Use a DNS Challenge' box.

   ![{D7B338E3-B314-4036-82ED-E19CB3062537}](https://github.com/user-attachments/assets/8121dccb-3f7b-48b3-91a3-6448cd4a70db)

   b) In the 'DNS Provider' field, chose 'DuckDNS'

   ![{0228E152-D375-433D-86F6-37E7A575152E}](https://github.com/user-attachments/assets/125c49e3-619f-4894-8a03-f6c73c3359c8)

   c) In the 'Credentials File Content' field, replace 'your-duckdns-token' with your actual duckdns token.

   ![{586831EB-8753-4C99-9F25-943E3B6AC8B7}](https://github.com/user-attachments/assets/eef3b111-2dcf-49c7-b351-7e0efcf0ed6d)

   You can find this token by logging in to DuckDNS, and it will be on the first page, in the first blue rectangle.

   ![{D84D78AD-C339-432E-8695-7A7AD3ED18A7}](https://github.com/user-attachments/assets/01e006f3-7fd5-436c-98e9-a474afd37bcf)

   Be sure to delete any spaces after pasting token.

   d) Propagation Seconds
   
   Set value to 120

   ![{A19D730D-A544-4503-A626-78B90C6D745F}](https://github.com/user-attachments/assets/9a11a0d7-cb84-4a7f-91e1-332e04b05c40)

   After this is done, check the 'I Agree to the Let's Encrypt Terms of Service' and click 'Save'.

   ![{31ED0436-E106-4ACA-9F9E-05431F9A56FF}](https://github.com/user-attachments/assets/547b18b0-cfc2-404f-9430-8a9c65959802)

   You have successfully added the ssl certificate and it is ready to be used with your services. Let me show you how to do that.









   











