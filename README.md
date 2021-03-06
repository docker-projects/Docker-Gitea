![Docker-Gitea](https://raw.githubusercontent.com/MephistoXoL/Docker-Gitea/master/Docker-Gitea.png)

# Docker-Gitea 
Docker Image Gitea for Raspberry pi 3+/3/2

This image is the latest version of Gitea, Dockerfile get and download the last version.

As oficial Gitea this image exports:
- 3000 for webUI
- 22 for ssh.
- The repositoy and other data are located in /data

## Install
Command line:
```
docker run -d -p 3000:3000 -p 222:22 -v /your/path/for/data:/data mephistoxol/gitea
```

Docker Compose:
```
version: '3.2'
services:
  app:
    container_name: gitea_app
    image: mephistoxol/gitea
    restart: unless-stopped
    # Traefik v1.7 optional
    labels:
      - traefik.frontend.rule: "Host:gitea.domain.com"
      - traefik.port: "3000"
      - traefik.frontend.redirect.entryPoint: "https"    
    networks:      
      - internal-network
    ports:
      - "3000:3000"
      - "222:22"
    volumes:
      - /your/path/for/data:/data
```

Ansible:
```
      docker_container:
        name: gitea_app
        image: mephistoxol/gitea
        volumes:
          - /your/path/for/data:/data
        ports:
          - 3000:3000
        restart_policy: unless-stopped
        # Traefik v1.7 optional
        labels:
          traefik.frontend.rule: "Host:gitea.domain.com"
          traefik.port: "3000"
          traefik.frontend.redirect.entryPoint: "https"
        networks:
          - name: internal-network
      register: result
```

## Database
You can choose type of Database in the install web.

NOTE: If you want to use mysql db you need other container like ```linuxserver/mariadb``` and you must create a db and user with privileges from gitea_app container 

## Changelog
```
20-10-2019
- Added Multi arch building
- Gitea v1.10.0-rc1
```
```
12-10-2019
- Gitea v1.9.4
```
```
- Based on latest Alpine arm
- Gitea v1.9.3
```

## Donate
[![Paypal](https://raw.githubusercontent.com/MephistoXoL/Things/master/paypal.png)](https://www.paypal.me/mephistoxol)
