# -arr-compose
Stack containing majority of most used -arr apps (except [prowlarr](https://github.com/Prowlarr/Prowlarr), comming soon) with a VPN transmission client and Traefik for off-site use

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
- [Portainer](https://github.com/portainer/portainer): a web UI for managing containers and stacks

# Configuration

to use this docker-compose, you need to edit the followings:
- the domain name of each services who are configured with traefik
- the IP address of Traefik for matching your network configuration
- Transmission VPN provider, username and passowrd
- Transmission local network
- Traefik/traefik.yml Let's encrypt e-mail
- Last but not least, allow in firewall port `80` and `443` and forward it to your server.

After that, if all is well configured, you can run `sudo docker-compose up -d` and all the apps in the stack is working and accessible from the web with the url you gave on your services.

# Quick-fix & Q&A

Comming Soon ...