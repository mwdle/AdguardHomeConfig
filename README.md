# Adguard Home Docker Compose Configuration  

A sample Docker Compose file and brief advice for Adguard Home.  

## Table of Contents  

* [Description](#adguard-home-docker-compose-configuration)  
* [Getting Started](#getting-started)  
* [Trickiness with Android](#trickiness-with-android)  
* [What I use Adguard Home for](#what-i-use-adguard-home-for)  
* [License](#license)  
* [Disclaimer](#disclaimer)  

## Getting Started  

1. Clone the repository:  

    ```shell
    git clone https://github.com/mwdle/AdguardHomeConfig.git
    ```  

2. Create a folder on your system for Docker bind mounts / storing container files. The folder should have the following structure:  

    ```shell
    docker_volumes/
    ├── Adguard/
    │   ├── config/
    │   └── work/
    ```  

3. Change the ```.env``` file properties for your configuration:  

    ```properties
    DOCKER_VOLUMES=<PATH_TO_DOCKER_VOLUMES_FOLDER> # The folder created in the previous step.
    ```  

4. Open a terminal in the directory containing the docker-compose file.  
5. Create a docker network for the container:  

    ```shell
    docker network create Adguard
    ```  

6. Start the container:  

    ```shell
    docker compose up -d
    ```  

Your container should be up and running and your Adguard Home Dashboard will be accessible on port 3000 for first time setup, and on port 80 during normal usage. DNS will be available on port 53 on the host machine. Attach your reverse proxy container to the previously created Docker Networks and configure it accordingly.  

## Trickiness with Android  

Getting your modern Android device to use your Adguard Home instance as its DNS server can be trickier than you'd expect. Here are some steps you can take to ensure your Android device uses your Adguard Home instance as its DNS server.  

* Disable Private DNS (Usually found under ```Settings -> Network & Internet -> Private DNS -> Off```)  
* Disable Secure DNS in your browser (Usually found under ```Browser settings -> Privacy & Security -> Secure DNS -> Off```)  
* ```Reserve an IP address``` in your router's management interface for your device. Connect it to your network with the Privacy option set to ```Use device MAC```, the static IP address set, and the local IP address of your Adguard Home instance as the DNS server.  
* ```Disable any IPv6 DNS Relay``` on your router if one exists. Disabling IPV6 entirely is also an option.  
* If none of the above steps work, a non-ideal workaround is to use an app from the Google Play Store that connects your phone to a dummy (local) VPN that enforces the DNS settings of your choosing.  

## What I use Adguard Home for  

Most people use Adguard Home to block ads, I personally can't keep up with investigating and unblocking hosts when I run into issues browsing the web caused by Adguard blocks. My home router doesn't support NAT loopback, and my sites are proxied by Cloudflare so I use Adguard Home for its DNS Rewrites feature to allow me to internally resolve and access services hosted on ```my.domain.com```. This increases speeds accessing my sites on my LAN since my requests don't route through Cloudflare and back. I simply setup my devices to use Adguard Home as their DNS server, and then create a wildcard record for ```*.domain.com``` to the IP address of my reverse proxy.  

## License  

This project is licensed under the GNU General Public License v3.0 (GPL-3.0). See the [LICENSE](LICENSE.txt) file for details.  

## Disclaimer  

This repository is provided as-is and is intended for informational and reference purposes only. The author assumes no responsibility for any errors or omissions in the content or for any consequences that may arise from the use of the information provided. Always exercise caution and seek professional advice if necessary.  
