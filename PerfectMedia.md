# Key things to remember for Perfect Media Server 

Home IP address is 192.168.1.196

## setting up ZFS

https://drechsel.xyz/how-to-migrate-existing-freenas-zfs-pools-to-ubuntu-1804-and-higher/


- Update apt:
`sudo apt update && sudo apt dist-upgrade -y`

- Install Dependencies
`sudo apt install software-properties-common dkms`

Note that linux-headers isn't included because apt wants a specific package name. I figure I'll just skip it and let it get installed as a dependency if it's needed


`sudo apt install zfsutils-linux`


- Look for pools

`sudo zpool import`

In our case, we're importing Primer

`sudo zpool import -f Primer`

...and VMs

`sudo zpool import -f VMs`


- Now make sure that the pools are showing up

`zpool list`



https://perfectmediaserver.com/



## setting up Docker


- Uninstall all old Docker versions...

`sudo apt-get remove docker docker-engine docker.io containerd runc`


- Update and install

`sudo apt-get update` or `sudo apt update`

`sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release`


- Add Docker GPG key

`curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg`


- Set up **stable** repository:

` echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null`



- Then, finally, install Docker Engine:

`sudo apt-get update`
~~`sudo apt-get install docker-ce docker-ce-cli containerd.io`~~

`sudo apt install docker.io`

- ...and then test to see if Docker is actually working

`sudo docker run hello-world`


## Set up Samba

`sudo apt install samba`



## Set up SSH server

`sudo apt install openssh-client`

`sudo apt install openssh-server`

restart ssh server

`sudo systemctl restart sshd.service`



##Set up SSH Keys for remote access

Run this on local machine

`ssh-keygen -t rsa`


Then copy it to the server:

`ssh-copy-id -i ~/.ssh/id_rsa.pub bshort@192.168.1.196`


Then try ssh into the server:
`ssh bshort@192.168.1.196`
