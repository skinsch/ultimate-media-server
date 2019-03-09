![Ultimate Media Server](ums.jpg)

# ultimate-media-server
A collection of services that stands up all your media automation needs with Docker containers.

This example will be using a Qnap TS-251+ as a media harvesting machine!

I much prefer having the control over the persistent volume space for backups, as opposed to having to dig through the NAS internal volumes. Also it's what I am used to so easy to do. There is a bit of a learning curve with docker but once you understand how it all works it's straight forward and universal.

It's not ideal to run a torrent client without a VPN, so qtransmission is out. Containers allow to only run the services you want anonymity for through a VPN (deluge-vpn), whilst also providing a proxy for tunneling other services through (privoxy).

There are people out there who have pulled together docker compose files, but I'd prefer to spin up individual containers.

Beyond radarr, sonarr and a download client:

* Tautulli for monitoring Plex
* Ombi for automating sharing of your server w requests
* Jacket or Cardigan for better torrent support
* SABnzb or NZBGet for Usenet downloading
* Organizr to pull it all together and save your browser from tab overload
* <img src='https://www.google.com/s2/favicons?domain=sonarr.tv' height='16' width'16' /> [Sonarr](http://sonarr.tv)  - It supports NZBGet, Sabnzbd and even torrent - https://github.com/linuxserver/docker-sonarr
* Radarr - to do all heavy listing finding releases, sending to downloader then renaming and moving files when download completes
In Summary - You need sonarr and radarr. They do all the heavy lifting of finding releases, sending to downloader and then renaming and moving files when downloaded.

## What's in the box?!
* <img src='https://www.google.com/s2/favicons?domain=sabnzbd.org' height='16' width='16' /> [Sabnzbd](http://sabnzbd.org) (usenet download manager)
* <img src='https://www.google.com/s2/favicons?domain=sickbeard.com' height='16' width='16' /> [Sickbeard](http://sickbeard.com) (tv search & download manager)
* <img src='https://www.google.com/s2/favicons?domain=radarr.video' height='16' width='16' /> [Radarr](https://radarr.video/) (tv search & download manager)
* <img src='https://www.google.com/s2/favicons?domain=couchpota.to' height='16' width='16' /> [CouchPotato](https://couchpota.to) (movie search & download manager)
* <img src='https://www.google.com/s2/favicons?domain=transmissionbt.com' height='16' width='16' /> [Transmission](https://transmissionbt.com) (torrent download manager)
* <img src='https://www.google.com/s2/favicons?domain=tautulli.com' height='16' width='16' /> [Tautulli](https://tautulli.com/) (Plex analytics and monitoring Plex)
* <img src='https://www.google.com/s2/favicons?domain=plex.tv' height='16' width='16' /> [Plex Media Server (plexpass)](https://plex.tv) (tv & movie organizer and sharing)

## Getting Started

### Prequisites
* You're on a *nix machine (preferably Ubuntu)
  * [Install Docker following these steps](https://docs.docker.com/linux/step_one/)
  * Make sure docker-compose is installed via:
    * `apt-get install docker-compose`
* For the purposes of this guide...
  * All of your media is located at `./media`
  * Your temp directory is located at `./temp`
* This guide assumes you have a hosts file mapping `ultimate.media.server` to `127.0.0.1`.

### To setup (NPM is Node Package Manager for Node.js)
* `npm install`

### To start
* `PIA_USER=username PIA_PASS=password npm run docker`
  * Note that this will take a few minutes depending on your broadband speed on inital startup.
  * Every restart thereafter will be almost instant.
* Bonus: All containers will automatically restart after power outages

### To stop
* `npm run docker:stop`

### To restart (useful for quick auto-updating of apps)
* `npm run docker:restart`

Once the install finishes open your navigate to the following:

* <img src='https://www.google.com/s2/favicons?domain=sabnzbd.org' height='16' width='16' /> [http://ultimate.media.server:8080](http://ultimate.media.server:8080) // Sabnzbd
* <img src='https://www.google.com/s2/favicons?domain=sickbeard.com' height='16' width='16' /> [http://ultimate.media.server:8081](http://ultimate.media.server:8081) // Sickbeard
* <img src='https://www.google.com/s2/favicons?domain=radarr.video' height='16' width='16' /> [http://ultimate.media.server:8989](http://ultimate.media.server:8989) // Radarr
* <img src='https://www.google.com/s2/favicons?domain=couchpota.to' height='16' width='16' /> [http://ultimate.media.server:5050](http://ultimate.media.server:5050) // CouchPotato
* <img src='https://www.google.com/s2/favicons?domain=couchpota.to' height='16' width='16' /> [http://ultimate.media.server:5051](http://ultimate.media.server:5051) // CouchPotato (for prereleases)
* <img src='https://www.google.com/s2/favicons?domain=transmissionbt.com' height='16' width='16' /> [http://ultimate.media.server:8091](http://ultimate.media.server:8091) // Transmission
* <img src='https://www.google.com/s2/favicons?domain=tautulli.com' height='16' width='16' /> [http://ultimate.media.server:8181](http://ultimate.media.server:8181) // Tautulli
* <img src='http://www.google.com/s2/favicons?domain=plex.tv' height='16' width='16' /> [http://ultimate.media.server:32400/web](http://ultimate.media.server:32400/web) // Plex Media Server

### Want Transmission to run with authentication?
* Add the transmission username and password params and run the command below.
* `PIA_USER=username PIA_PASS=password TRANSMISSION_USER=tUsername TRANSMISSION_PASS=tPassword npm run docker`

### The &lt;insert service&gt; web app won't come up or isn't running

* This guide is only supported on *nix OSes. Try running on Ubuntu.
* Try restarting the services with `npm run docker:restart`

Special thanks to the maintainers of the following docker containers:
* [linuxserver/plex](https://hub.docker.com/r/linuxserver/plex)
* [linuxserver/tautulli](https://hub.docker.com/r/linuxserver/tautulli)
* [linuxserver/radarr](https://hub.docker.com/r/linuxserver/radarr)
* [linuxserver/sabnzbd](https://hub.docker.com/r/linuxserver/sabnzbd)
* [linuxserver/couchpotato](https://hub.docker.com/r/linuxserver/couchpotato)
* [timhaak/sickbeard](https://hub.docker.com/r/timhaak/sickbeard)
* [haugene/transmission-openvpn](https://hub.docker.com/r/haugene/transmission-openvpn)
* [nginx](https://hub.docker.com/_/nginx)
