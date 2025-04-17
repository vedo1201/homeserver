# Basic things to do right after installing Ubuntu Server
On this page, your are going to find some things that are must to do if you want clean after install setup of server.
## Let's start

### 1. Setting up static ip address
The most important thing to do, when speaking generally about home servers, is to set up a static IP address. The servers IP is going to be used to access basically every service on our server,
so it is important for it not to change every time server restarts. Because of this, the very first thing to do after booting into server is to set up static IP. This can be done by two ways, either
setting up the static ip in router settings, or directly on server.

#### 1. Setting up the static ip in router settings (easiest)
1. First thing you have to do is to find your routers ip address. If you are using windows, this can be done by opening command prompt and entering the command 'ipconfig'.
   Your routers ip is going to be labeled as default gateway

   ![{D5582946-7DF2-463C-BA3C-56D014BDCA5D}](https://github.com/user-attachments/assets/d047460e-a7b6-4a38-8217-c4b40ed629ed)

2. Open up your web browser, enter this ip in search bar and press enter. You should be redirected to the configuration page of your router that looks something like this:

   ![{C6E727C7-F473-4E1F-93A5-259D8576D484}](https://github.com/user-attachments/assets/b6d58b91-0261-4135-b3bc-5a70e16a5039)




#### 2. Setting up the static ip in servers network config file
