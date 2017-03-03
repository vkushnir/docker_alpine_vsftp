# FTP Server
_FTP Server based on alpine docker image_

## RUN
    docker run -d --name ftpd -p 20/udp 21/udp vkushnir/tftp-hpa
    
### USE SHARED VOLUME
    docker run -d --volumes-from ftpd --name myapp mydomain/myimage

## SERVICE
### Upstart
    description "FTP Server"
    author "Vladimir Kushnir <v.kushnir@gmail.com>"
    start on filesystem and started docker
    stop on runlevel [!2345]
    respawn
    script
        /usr/bin/docker start -a ftpd
    end script
Copy **tftpd.conf** in to **/etc/init/**
#### Manage
    initctl stop ftpd
    initctl start ftpd
