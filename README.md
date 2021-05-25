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
* Sonarr
* Tautilli
* letsencrypt
* watchtower

# WIP

Currently environment variables on NGIX config dont work, manually change $FQDN in the /nginx-rp/config/conf.d/sites-available/* files to your domain eg. example.com
You can then access each service with plex.example.com if you have a wildcard A record for example.com

I also get the feeling I'm missing something

## TASKS:

- [x] Environment variables for docker-compose
- [ ] NGINX Environment variables
- [ ] Explain iptables - [light reading](https://unrouted.io/2017/08/15/docker-firewall/) available here

## Creating new subdomains

If you wanted to add a new subdomain, for example lets do sonarr, we would create a new config file in `/nginx-rp/config/conf.d/sites-available` for the service.  for example we will do sonarr.conf, we use the hostname of the docker container as the host for the destination

```
upstream sonarr {
  server        sonarr:32400;
}

server {
  listen        80;
  server_name   sonarr.$FQDN;


  location / {
    proxy_pass  http://sonarr;
  }
}
```

Once we have this done, we can then enable it by created a link to it in `/nginx-rp/config/conf.d/sites-enabled`

`ln -s /nginx-rp/config/conf.d/sites-available/sonarr.conf /nginx-rp/config/conf.d/sites-enabled`

restart the `reverse` container or the whole thing if you need to
