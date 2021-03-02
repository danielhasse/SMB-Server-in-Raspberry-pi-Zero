# SMB-Server-in-Raspberry-pi-Zero
SMB file Server in minutes

## Prepare

First Step is to update your system

```
Sudo apt update
```

We are going to set up the file server using the sd card (later you can add aditional external storage if needed) so it is a good idea to check if the  filesystem is expanded and taking advantage of the whole sdcard space.

type

```
sudo raspi-config
```
choose advance options

Expand File System

now reboot the system for the changes take effect.

## Install Samba

Now you are ready to install Samba, use the following command:

```
sudo apt-get install samba samba-common-bin
```

## Create a shared folder

Create a shared folder and add permissions

```
sudo mkdir -m 1777 /sharedFolder
```

## Configure SMB 

Configure the smb.conf file

```
sudo nano /etc/samba/smb.conf
```

add the following lines in the end of the file:

```
[share]

Path = /sharedfolder
Browseable = yes
Writeable = Yes
only guest = no
create mask = 0777
directory mask = 0777
Public = yes
Guest ok = yes
```

## Set password for Samba

It is a good idea to set a password for Samba

```
sudo smbpasswd -a pi
```
now restart the Samba service

```
sudo systemctl restart smb.service
```
## Find your Folder

These steps are for Windows 10 OS

in Windows OS, go to your search bar and type your ip address from your pi in the network:
```
\\192.168.0.10\
```
you should see your shared folder.

Right click and select ##map network drive

enable to ##reconnect at signin and ##assign a letter to it.

There you go, now you have your own personal file system over the network using a low budget raspberry pi.

Thank you!

