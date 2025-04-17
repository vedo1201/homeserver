# Guide Walktrough

# Setting up server based on Ubuntu Server

I would highly suggest to read this file before starting, so you know what are you going to work with and what is this server going to look like.

All of the things in this repo are about home server based on UBUNTU SERVER operating system, so if you decide to follow this guide when creating your home server, be sure to use that OS.

This repo can be used as guide or help, either for complete beginner or user who is looking to improve their server.



In this guide, I've covrered some things that are must when we talk about stable, secure and reliable home server based on Ubuntu Server.

# 1. Basic setup after install

The things that I have covered about server setup right after install are:

  1. Basic things to do after installing ubuntu server, setting it as a good base for future work.
  2. Formatting disks, putting a filesystem on them and mounting them in a folder so they are accessible automatticaly on startup.
  3. Installing docker for managing containers.
  4. Installing portainer (as a docker container) for graphical managment of docker containers.
  5. Setting up the SAMBA (file sharing system), so that disks in server can be accessed over network through the Windows File Explorer or basically any other device on the same network
      (This makes files easier to move, copy and manage, which is especially helpful for creating backup of docker containers, we will talk about that a little bit later.
      Backing up containers and the whole server is really important because the whole idea is to make this server easy to re-deploy if something happens with software or hardware used in server.)

After doing those things, you are going to have the system that works smooth and has minimum downtime. 

Next, we are going to setup some of the basic services
