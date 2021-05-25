# plex-docker-reverse-proxy
plex stack using docker and nginx reverse proxy

Featured Services:

$(FQDN) = Your domain, eg: example.com

* Plex Media Server - plex.$(FQDN)
* Deluge - deluge.$(FQDN)
* portainer - portainer.$(FQDN)
* NGINX acting as reverse proxy
* NGINX acting as web server to retain main site on $(FQDN)
* Jackett
* Sonar
* Tautilli
* letsencrypt
* watchtower

# WIP

Currently environment variables on NGIX config dont work, manually change $FQDN in the /nginx-rp/config/conf.d/sites-available/* files to your domain eg. example.com
You can then access each service with plex.example.com if you have a wildcard A record for example.com

TASKS:

- [x] Environment variables for docker-compose
- [ ] NGINX Environment variables
