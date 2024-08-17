# Adguard Home Docker Compose Configuration  

A sample Docker Compose file and brief advice for Adguard Home.  

## Important Details  

* The Docker Compose file assumes you have already created a Docker network called ```Adguard```. You can create a network before starting the container by executing the following command: ```docker network create Adguard```  
* You must change the ```DOCKER_VOLUMES``` path in the ```.env``` file to a folder on your system where you wish to store container files (used in Docker Compose bind mounts).  

## Starting the container  

In your terminal, ```cd``` to the directory containing the ```docker-compose.yml``` and ```.env``` files. Run the following command: ```docker compose up -d```  
Your container should be up and running and your Adguard Home Dashboard will be accessible after you configure your reverse proxy and connect your Docker Networks accordingly! DNS will be available on port 53 on the host machine.  

## Trickiness with Android  

Getting your modern Android device to use your Adguard Home instance as its DNS server can be trickier than you'd expect. Here are some steps you can take to ensure your Android device uses your Adguard Home instance as its DNS server.  

* Disable Private DNS (Usually found under ```Settings -> Network & Internet -> Private DNS -> Off```)  
* Disable Secure DNS in your browser (Usually found under ```Browser settings -> Privacy & Security -> Secure DNS -> Off```)  
* ```Reserve an IP address``` in your router's management interface for your device. Connect it to your network with the Privacy option set to ```Use device MAC```, the static IP address set, and the local IP address of your Adguard Home instance as the DNS server.  
* ```Disable any IPv6 DNS Relay``` on your router if one exists. Disabling IPV6 entirely is also an option.  
* If none of the above steps work, a non-ideal workaround is to use an app from the Google Play Store that connects your phone to a dummy (local) VPN that enforces the DNS settings of your choosing.  

## What do I use Adguard Home for?  

Most people use Adguard Home to block ads, I personally can't keep up with investigating and unblocking hosts when I run into issues browsing the web caused by Adguard blocks. My home router doesn't support NAT loopback, so I use Adguard Home for its DNS Rewrites feature to allow me to internally resolve and access services hosted on ```my.domain.com```. I simply setup my devices to use Adguard Home as their DNS server, and then create a wildcard record for ```*.domain.com``` to the IP address of my reverse proxy.  

## Disclaimer  

This repository is provided as-is and is intended for informational and reference purposes only. The author assumes no responsibility for any errors or omissions in the content or for any consequences that may arise from the use of the information provided. Always exercise caution and seek professional advice if necessary.  
