# Usenet Docker

## Containers
* [jwilder/nginx-proxy](https://github.com/jwilder/nginx-proxy) - Nginx Proxy
* [linuxserver/sabnzbd](https://github.com/linuxserver/docker-sabnzbd) - SABnzbd
* [linuxserver/couchpotato](https://github.com/linuxserver/docker-couchpotato) - CouchPotato
* [linuxserver/plex](https://github.com/linuxserver/docker-plex) - Plex
* [linuxserver/sonarr](https://github.com/linuxserver/docker-sonarr) - Sonarr
* [linuxserver/plexpy](https://github.com/linuxserver/docker-plexpy) - Plexpy
* [linuxserver/hydra](https://github.com/linuxserver/docker-hydra) - NZBHydra
* [linuxserver/muximux](https://github.com/linuxserver/docker-muximux) - Muximux
* [linuxserver/radarr](https://github.com/linuxserver/docker-radarr) - Radarr
* [linuxserver/ombi](https://github.com/linuxserver/docker-ombi) - Ombi
* [linuxserver/nzbget](https://github.com/linuxserver/docker-nzbget) - NZBGet

## Docker Setup
1. Update `./uidgid.env` with the user and group IDs that will be running Docker
2. Update `./docker-compose.yml` and replace `HOSTNAME` with the URL that will be pointing at the docker container and replace `/data_directory_path` with the directory for config, downloads, movies and TV folders
3. Choose which Usenet services containers the use and remove the extras from the `./docker-compose.yml` file
    * There are serveral containers that are duplicate services, I just added them for extra choices
4. Run `docker-compose up -d` to start all the Usenet services

## Hostnames
* I pointed subdomains to my home IP address for each service that I wanted external access to. I plan on setting up DynDNS with DD-WRT soon but for now my IP address has been the same for 2 months
* In my router configuration I forwarded all the necessary ports to my local server running Docker

### Note about Plex and setting up Plex server
* Initially when all containers are fully running, Plex is accessible by IP:PORT/web/index.html but the Plex Server configuration is hidden.  This is due to the Plex container being behind the Docker Network's IP and not being able to connect to Plex.tv
* I found my solution in this Github issue thread <https://github.com/linuxserver/docker-plex/issues/36>
* Specifically I had to SSH tunnel to the Plex Docker container `ssh -L 8080:localhost:32400 user@dockerhost.mydomain.net`, then opened a web browser and went to `127.0.0.1:8080/web/index.html` which allowed me to configure my server