# website-backend
![Docker Image CI](https://github.com/smhagit/website-backend/actions/workflows/docker-image.yml/badge.svg?branch=master)

Just a small Symfony application as API for the website-frontend repo. It provides API endpoints for:

- increment value of `sensor.website_visitors` (which is a Home Assistant entity)
- retrieve current value of `sensor.website_visitors` for the fancy visitor counter on my website
- retrieve current value of `sensor.k8s_cluster_plug` to display the current power consumption of my Kubernetes Raspberry cluster 
- total number of Home Assistant entities and devices

The main reason this backend exists is to provide a realtime API of the above data on my website. Because my Home Assistant is not behind the public ingress, the website won't have access to the needed data. 



# Platform: ARM
As this Docker Image is primary used on my Raspberries, the base image is `arm64v8/php:8.1-apache`.

# Docker
`docker pull smhagit/website-backend`

This image is built with GitHub Actions via self-hosted runner on an arm64 Raspberry Pi.


## Usage

`docker-compose.yml`
```yaml
version: "3.9"
services:
    app:
        image: smhagit/website-backend
        environment:
          API_STATIC_APIKEY: ""
          HOME_ASSISTANT_TOKEN: "<HOME ASSISTANT TOKEN>"
          HOME_ASSISTANT_BASEURL: "http://homeassistant.local:8123/api"
          HOME_ASSISTANT_ENTITY_WHITELIST: "sensor.abc;sensor.def"
```
