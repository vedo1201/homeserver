# SAMBA Setup
SAMBA is protocol that is used to connect to remote (network) shared storage from any device on the same network.
In this guide, we will set up samba shares for drives we have in server, so we can access, move and edit their files from another pc. 
For the example, if you are using Windows you should be able to access servers storage using the Windows File Explorer.

## 1. Installing SAMBA service
First, we need to install SAMBA on our server, so we can set up our shares using the SAMBA configuration file.
Before installing, we need to update our system by running:

<pre> sudo apt update </pre>

After that, we can install SAMBA service by running:

<pre> sudo apt install samba </pre>

## 2. Configuring SAMBA

Now, SAMBA service is installed and we need to configure our share. This is done by editing SAMBA config file.
Open it by running:

<pre> sudo nano /etc/samba/smb.conf </pre>

Then we need to scroll all the way to the end of this file and add this config:

<pre> [Shared]
   path = /srv/samba/shared
   browseable = yes
   read only = no
   guest ok = no
   valid users = your_user
 </pre>

Now we need to replace default values with our own.
The values that you need to replace are:


<pre> 1. [Shared] - Replace it by the name that you want to assign to your share. You are going to use this name when accessing the share. </pre>

<pre> 2. path - Needs to be replaced with the actual path of the folder you want to share </pre>

<pre> 3. your_user - Replace this with username that you want to use to access this share. We are going to create it in the next step. </pre>

#### COPY THIS CONFIGURATION AND CHANGE PARAMETERS ACCORDING TO YOUR NEEDS IF YOU NEED MORE THAN ONE SHARE.

## 3. Creating SAMBA User

After we have created our share, we need to create user which can access the share. Make sure to use the same username that you have entered in configuration file, in valid users.

To create new user, run this command:

<pre> sudo smbpasswd -a username </pre>

Replace 'username' with your actual username. You will be asked to create new password for SAMBA user.

## 4. Starting up SAMBA Service

Now we just need to start SAMBA and enable it trough firewall.
To restart SAMBA, type:

<pre> sudo systemctl restart smbd </pre>

And then run this command to enable SAMBA in firewall:

<pre> sudo ufw allow 'Samba' </pre>

After we have finished this, we can try to access our share.
If you are on Windows, do this by entering this in the file explorer:

<pre> \\serverip\sharename </pre>

Make sure to replace:
  1. serverip - with actual ip of your server
  2. sharename - with the name of the share configured in config file

And now you just have to login to share using the smb username and password that you have configured and you will be able to have access to all of your server files in Windows File Explorer.









