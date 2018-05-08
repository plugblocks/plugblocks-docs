---
date: 2018-03-09T20:11:02+01:00
title: Getting started
weight: 10
---

## Setup
### Generate Configuration file
If you want to send mails (for user account management) things-api uses Sendgrid, so you should get an [API key](https://app.sendgrid.com).

To resolve WiFi geolocations, things-api uses Google, so you should get an [API key](https://console.cloud.google.com/apis/).

Create a `.env.prod` file from the included `.env` file template, while customizing data such as domain name, API keys...

## Installation
Install `docker` and `docker-compose`

Run `docker-compose up -d`

Watch `yourip:4000`, you should have a welcome message saying `Welcome to things API`.

Congratulations, you are all set !

## Configuration
### Sigfox Use
Connect to your account, select your device type and create two callbacks:

Type: `DATA` `UPLINK`,

URL: `https://youraddress/v1/sigfox/messages`

Method: `POST`,

Content-type: `application/json`

`mesType` is 1 for Sens'it, 2 for an Arduino Syntax, and 3 for Wisol 20

```
{
    "sigfoxId":"{device}",
    "frameNumber":{seqNumber},
    "timestamp": {time},
    "station": "{station}",
    "snr": {snr},
    "avgSnr": {avgSnr},
    "rssi": {rssi},
    "mesType":1,
    "data": "{data}"
}
```


Type: `SERVICE` `GEOLOC`,

URL: `https://youraddress/v1/sigfox/messages`

Method: `POST`,

Content-type: `application/json`

```
{
  "sigfoxId": "{device}",
  "frameNumber": {seqNumber}, 
  "timestamp": {time},
  "latitude": {lat},
  "longitude": {lng},
  "radius": {radius},
  "spotit": true
}
```

## NGinx configuration
### With HTTPS using certbot
You can copy paste and customize the [nginx/conf-https-step-1](https://github.com/IoThingsDev/api/tree/master/nginx/conf-https-step-1) to your etc/nginx/sites-enabled/yourdomain
sudo service nginx reload
Run certbot ....

Copy paste and customize the [nginx/conf-https-step-2](https://github.com/IoThingsDev/api/tree/master/nginx/conf-https-step-2)
to your `etc/nginx/sites-enabled/yourdomain`
`sudo service nginx reload`

### Without HTTPS

Copy paste and customize the conf-http
to your `etc/nginx/sites-enabled/yourdomain`
`sudo service nginx reload`