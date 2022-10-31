# -arr-compose
Stack containing majority of most used -arr apps with a VPN transmission client and Traefik for off-site use

# stack description

this docker-compose stack is using the following services:
- [Traefik](https://github.com/traefik/traefik): Routing your services to sub-domain URL for off-site use
- [Uptime-kuma](https://github.com/louislam/uptime-kuma): a status page for managing uptime status of your services
- [Transmission-openvpn](https://github.com/haugene/docker-transmission-openvpn): a Torrent Downloader with an included openvpn client with a VPN kill-switch
- [Overseerr](https://github.com/sct/overseerr): for series and movie user requests
- [Heimdall](https://github.com/linuxserver/Heimdall): a hub interface for all services
- [Sonarr](https://github.com/Sonarr/Sonarr): a Series / Anime scrapper, downloader and organizer
- [Bazarr](https://github.com/morpheus65535/bazarr): a subtitle scrapper and downloader. Linked with Sonarr and Radarr
- [readarr](https://github.com/Readarr/Readarr): a book-related equivalent of Sonarr
- [Lidarr](https://github.com/Lidarr/Lidarr): a song-related equivalent of Sonarr
- [Radarr](https://github.com/Radarr/Radarr): a movie scrapper, downloader and organizer
- [Prowlarr](https://github.com/Prowlarr/Prowlarr): Torrent tracker manager for -arr apps
- [Portainer](https://github.com/portainer/portainer): a web UI for managing containers and stacks

# Configuration

to use this docker-compose, you need to edit the followings:
- the domain name of each services who are configured with traefik
- the IP address of Traefik for matching your network configuration
- Transmission VPN provider, username and passowrd
- Transmission local network
- Traefik/traefik.yml Let's encrypt e-mail
- Last but not least, allow in firewall port `80` and `443` and forward it to your server.

On top of that, you need to create a Docker virtual Network for all traefik dockers. To do that, run `docker network create traefik-public`.

After that, if all is well configured, you can run `sudo docker-compose up -d` and all the apps in the stack is working and accessible from the web with the url you gave on your services.

To check if all apps are running, you can run `docker compose ps -a` in the folder where you have the `docker-compose.yml`.

# Quick-fix & Q&A

## I cant access my services

First of all, check if your service are running. to do that run `sudo docker-compose ps`. this command return the current status of all the containers in your stack. If on (or more) service(s) are ***DOWN*** or ***RESTARTING***, there is a configuration problem. Please see below instruction (if exist).

## Why can I acces my services loccaly but not with the URL ?

There is 2 main resaon to this problem:

### - Router / Livebox NAT rules

Be Extra sure that you allow port **80** and **443** on your firewall / router NAT rules and redirect them tou your server IP. Without those ports (or redirected to the bad server), all requests are dropped or redirected to the wrong server.

### - DNS Rules

In addition to a **A** rules on DNS provider to your IP (or dynDns), you need to add a **CNAME** rule to each service. you need to configure it like this:

- sub-domain: service.host.url
- TTL: Default
- Target: host.url**.** (do not forget the dot at the end)

When you do that, you told your DNS provider to redirect all requests from service.host.url to host.url. Doig that, all requests are landing to traaefik with your original url and, with that, traefik redirect you to the correct service.

## One or more services are stopping all by themselves

If you see one (or more) service not responding, you can trace the log with the command `docker compose logs appname`. Then, search for thhe error in the log and search it on the internet. 
