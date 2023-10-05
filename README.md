# jellyfin Media Suite
Docker Compose file of Jellyfin media suite.
The stack composes of Jellyfin, Radarr, Sonar, Prowlarr, Bazarr, Jellyseer.

```
version: '3.8'

services:
  jellyfin:
    image: linuxserver/jellyfin:latest
    restart: unless-stopped
    container_name: "jellyfin"
    ports:
      - '8096:8096'
      - '8920:8920'
    environment:
      PUID: '0'
      PGID: '0'
      TZ: 'Asia/Seoul'
    volumes:
      - /portainer/Files/AppData/Config/Jelllyfin:/config
      - /mnt/media/movies:/data/movies
      - /mnt/media/series:/data/series
      - /mnt/media/music:/data/music
      
  radarr:
    image: linuxserver/radarr:latest
    restart: unless-stopped
    container_name: "radarr"
    ports:
      - '7878:7878'
    environment:
      PUID: '0'
      PGID: '0'
    volumes:
      - /portainer/Files/AppData/Config/Radarr:/config
      - /mnt/media/torrent:/downloads
      - /mnt/media/movies:/movies

  sonarr:
    image: linuxserver/sonarr:latest
    restart: unless-stopped
    container_name: "sonarr"
    ports:
      - '8989:8989'
    environment:
      PUID: '0'
      PGID: '0'
    volumes:
      - /portainer/Files/AppData/Config/Sonarr:/config
      - /dev/rtc:/dev/rtc
      - /mnt/media/torrent:/downloads
      - /mnt/media/series:/series

  prowlarr:
    image: ghcr.io/linuxserver/prowlarr:develop
    restart: unless-stopped
    container_name: "prowlarr"
    ports:
      - '9696:9696'
    environment:
      PUID: '0'
      PGID: '0'
    volumes:
      - /portainer/Files/AppData/Config/Prowlarr:/config

# OPTIONAL SERVICES BELOW

  bazarr:
    image: linuxserver/bazarr:latest
    restart: unless-stopped
    container_name: "bazarr"
    ports:
      - '6767:6767'
    environment:
      PUID: '0'
      PGID: '0'
      TZ: 'Asia/Seoul'
    volumes:
      - /portainer/Files/AppData/Config/Bazarr:/config
      - /mnt/media/series:/series
      - /mnt/media/movies:/movies
      
  jellyseer:
    image: fallenbagel/jellyseerr:latest
    restart: unless-stopped
    container_name: "jellyseer"
    ports:
      - '5055:5055'
    environment:
      LOG_LEVEL: ''
      TZ: 'Asia/Seoul'
    volumes:
      - /portainer/Files/AppData/Config/jellyseer:/app/config
```
