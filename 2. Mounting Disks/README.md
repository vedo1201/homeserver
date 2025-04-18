# Mounting Disks
Now, I will show you how to set up your storage. We should mount all of the disks (HDD, SSD) which we have in our server, to specific folders in system and also set them up to automatically mount on startup.
When this is done, you should be able to access your <ins>HDD</ins>	 for example, by entering the <ins>/mnt/hdd</ins>	 folder. This folder will have the same capacity as your physical drive.

### So let's start!

1. First thing you have to do is to identify the disk you want to use. You can do this by typing this command:

   <pre> sudo lsblk </pre>

This is going to give you similar output to this:

![{49F52415-7DE0-4146-8467-94D00B61AA9B}](https://github.com/user-attachments/assets/391b72bf-c22b-45bb-aba7-2fa180716789)


Here you need to identify the disk by its capacity and then format it.

2. Formatting the disk

  2.1. Type this command to open <ins>fdisk</ins> tool for your specific drive:

   <pre> sudo fdisk /dev/sdX </pre>

   Replace <ins>sdX</ins> with the right letter for your disk and press ENTER.

   2.2. Continue by entering those letters and pressing ENTER after every one:
         <pre> d       #To delete partition on drive, keep doing this until you get an output that all of the partitions are deleted </pre>  
         <pre> n       #To create new partition </pre>  
         <pre> ENTER x3       #Press ENTER three times to accept default values and use full size of your disk </pre>  
         <pre> y       #If it asks to remove signature from drive, if not skip this step </pre>  
         <pre> w       #To write changes to disk </pre>  
   2.3. After you have finished formatting, you must create the file system on your disk.
      

3. Creating file system

   We are going to create the <ins>ext4</ins> filesystem by typing this command:

      <pre> sudo mkfs.3xt4 /dev/sdX1 </pre>
   Replace X with your drive letter!

4. Mounting the disk

    In this step we will use <ins>fdisk config file</ins> to mount the disk automatically on startup.

   4.1 Find the disk UUID
       UUID is an universal disk identifier and it is going to be used for mounting the correct disk.
       Be aware that you can find the UUID just if you have created the partition on your drive from the previous step and put the filesystem on it.

     Do this by typing this command:

      <pre> sudo blkid </pre>

   You will get an output similar to this:

   ![{23B16D37-0598-4B5D-9F90-0E5629A1A147}](https://github.com/user-attachments/assets/4b7f60d0-7304-43b6-bedb-e3e17d75a97f)

    The highlighted part is an UUID that we need. Copy it to your clipboard.

   4.2 Open and edit <ins>/etc/fstab</ins> file by typing:

   <pre> sudo nano /etc/fstab </pre>

      At the bottom of this file, add the following line:

      <pre> UUID="" /mnt/{LOCATION} ext4 defaults 0 2 </pre>

      Replace <ins>/mnt/{LOCATION}</ins> with the location of the folder that you want to mount the disk in and <ins>UUID</ins> with the one you have copied earlier.

      Save this file by entering <ins>CTRL + X</ins>, <ins>Y</ins>, <ins>ENTER</ins>

    4.3 Test the mount location by typing
       <pre> sudo systemctl daemon-reload </pre>
       <pre> sudo mount -a </pre>
       If you did not get any response, that means that you have successfully mounted the disk and it is going to be mounted automatically on every startup.
       Check the mount locations by typing:
       <pre> df -h </pre>
       You will get an output similar to this:

   ![{C9266237-0466-4A5B-90E7-658194A3491F}](https://github.com/user-attachments/assets/a2f09358-380f-4dd5-b93d-0074f0ef27e9)





