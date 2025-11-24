### Running Wireguard using Docker

### Make Your Directory 
    mkdir -p ~/docker-projects/Wireguard
    cd ~/docker-projects/Wireguard

### Create your .yml file 
Use a text editor to create your docker-compose file and add the following:


    ---
    services:
    wireguard:
        image: lscr.io/linuxserver/wireguard:latest
        container_name: wireguard
        cap_add:
          - NET_ADMIN
          - SYS_MODULE #optional
        environment:
          - PUID=1000
          - PGID=1000
          - TZ=Etc/UTC
          - SERVERURL= Your Desired Public Ip Address
          - SERVERPORT=51820 #optional
          - PEERS= The amount of peers you'd want to serve
          - PEERDNS=auto #optional
          - INTERNAL_SUBNET=10.13.13.0 #optional
   cd       - ALLOWEDIPS=0.0.0.0/0 #optional
          - PERSISTENTKEEPALIVE_PEERS= #optional
          - LOG_CONFS=true #optional
        volumes:
          - /path/to/wireguard/config:/config
          - /lib/modules:/lib/modules #optional
        ports:
          - 51820:51820/udp
        sysctls:
          - net.ipv4.conf.all.src_valid_mark=1
        restart: unless-stopped

### Starting
   
    sudo docker compose up -d

### Accessing Config Files

    cd config
    ls

You should now see your peer directories that should contain your .conf files

### Using Wireguard 
Download the app from your appstore or get the client for your desired OS from https://www.wireguard.com/install
Import the .conf file or scan the QR code, Press Activate

### Screenshots of it working

![](<Screenshot 2025-11-23 234913.png>)

![](<Screenshot 2025-11-23 235038.png>)

