---
tags: Sysadmin
---

<style>

html, body, .ui-content {
    background-color: #333;
    color: #ddd;
}

.markdown-body h1,
.markdown-body h2,
.markdown-body h3,
.markdown-body h4,
.markdown-body h5,
.markdown-body h6 {
    color: #ddd;
}

.markdown-body h1,
.markdown-body h2 {
    border-bottom-color: #ffffff69;
}

.markdown-body h1 .octicon-link,
.markdown-body h2 .octicon-link,
.markdown-body h3 .octicon-link,
.markdown-body h4 .octicon-link,
.markdown-body h5 .octicon-link,
.markdown-body h6 .octicon-link {
    color: #fff;
}

.markdown-body img {
    background-color: transparent;
}

.ui-toc-dropdown .nav>.active:focus>a, .ui-toc-dropdown .nav>.active:hover>a, .ui-toc-dropdown .nav>.active>a {
    color: white;
    border-left: 2px solid white;
}

.expand-toggle:hover, 
.expand-toggle:focus, 
.back-to-top:hover, 
.back-to-top:focus, 
.go-to-bottom:hover, 
.go-to-bottom:focus {
    color: white;
}


.ui-toc-dropdown {
    background-color: #333;
}

.ui-toc-label.btn {
    background-color: #191919;
    color: white;
}

.ui-toc-dropdown .nav>li>a:focus, 
.ui-toc-dropdown .nav>li>a:hover {
    color: white;
    border-left: 1px solid white;
}

.markdown-body blockquote {
    color: #bcbcbc;
}

.markdown-body table tr {
    background-color: #5f5f5f;
}

.markdown-body table tr:nth-child(2n) {
    background-color: #4f4f4f;
}

.markdown-body code,
.markdown-body tt {
    color: #eee;
    background-color: rgba(230, 230, 230, 0.36);
}

a,
.open-files-container li.selected a {
    color: #5EB7E0;
}


</style>


# Install Docker Offline on Red Hat Enterprise Linux Server release 7.5


### Download file

```
wget http://dadinjaenudin.com/source/docker-source-offline.zip
unzip docker-source-offline.zip
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

### Installing Docker Compose
In order to get the latest release, take the lead of the Docker docs and install Docker Compose from the binary in Docker’s GitHub repository.

Check the current release and if necessary, update it in the command below:
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

Next, set the permissions to make the binary executable:
```
sudo chmod +x /usr/local/bin/docker-compose
```

Then, verify that the installation was successful by checking the version:

```
docker-compose --version
```

This will print out the version you installed:


Happy Learning !!!
