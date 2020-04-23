---
tags: Sysadmin
---

# Install Docker Offline on Red Hat Enterprise Linux Server release 7.5


### Copy file to server
```
tar xvf docker-source-offline
cd docker-source-offline
chmod +x install.sh
./install.sh

```

Don't panic The server will not be able to access from ssh, so you can go to server and login to server.

First check your docker ip network
```
ifocnfig -a

[root@localhost docker]# ifconfig -a
docker0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.255.0  broadcast 172.17.0.255
        ether 02:42:66:44:a8:38  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

Create / Edit file
vi /etc/docker/daemon.json
```
{
"bip":"172.17.0.1/24",
"dns":["172.16.13.20"]
}
```
Note bip : docker network

### Start docker
```
systemctl enable docker
systemctl start docker
docker images
[root@localhost docker]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE

```

now the docker up and running

### Stop docker
systemctl stop docker


Happy Learning !!!
