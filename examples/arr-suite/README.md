# References

- https://docs.linuxserver.io/images/docker-prowlarr/
- https://docs.linuxserver.io/images/docker-sonarr/
- https://docs.linuxserver.io/images/docker-radarr/
- https://docs.linuxserver.io/images/docker-lidarr/
- https://docs.linuxserver.io/images/docker-qbittorrent/
- https://docs.linuxserver.io/deprecated_images/docker-requestrr/
- https://docs.linuxserver.io/images/docker-emby/

# Notes

> [!WARNING]
> Downloading copyright restricted movies or media in general is illegal in most countries.
>
>  Use this docker stack responsibly!

Docker stack consisting of various arr-services like:

- Prowlarr
  - Used as indexer for torrent links
- Sonarr
  - Used for tv shows
- Radarr
  - Used for movies
- Lidarr
  - Used for music    
- Qbittorrent
  - Used as download client, preferably behind VPN (e.g. socks5)
  - A temporary password for the `admin` user will be printed to the container log on startup. Change it immediately to a static one that does not change again.
- Requestrr
  - Used to request movies and tv-shows by end clients 
- Emby
  - Used to manage your media libraries and stream it from various devices
 
Combine with a reverse proxy like Traefik.

## Setup

You can follow this Youtube tutorial on how to setup the arr applications:

https://www.youtube.com/watch?v=LD8-Qr3B2-o

**Note**:  As all arr containers live within the same Docker network, you can easily reference container names instead of IPs. Docker will resolve the container names automatically to the current docker containers' IP. No need for port mappings or defining your Docker server's IP address. Use Docker networks!

![image](https://github.com/Haxxnet/Compose-Examples/assets/21357789/8915f9f3-081f-41d2-9c5e-bdf9553e09c2)

![image](https://github.com/Haxxnet/Compose-Examples/assets/21357789/94de5802-3b26-420b-bb1d-ac82cd5a5cfb)

## Traefik + Emby + HTTP Headers

During the setup of Emby in a web browser (HTTPS via Traefik) you may notice errors in the developer console, which prevents the web page from loading properly.

Those errors occur, if you have configured secure HTTP response headers such as X-Content-Type-Options with the directive "nosniff".

To complete the web-based setup, you either have to temporarely disable the HTTP header or browse the Emby instance without Traefik as reverse proxy. 

After the setup was completed, the errors are gone and you can use Emby regularly with Traefik, HTTPS and any X-Content-Type-Options header configuration.