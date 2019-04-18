# Docker-Nagios

Docker image for Nagios

Build Status: [![Build Status](https://travis-ci.org/JasonRivers/Docker-Nagios.svg?branch=master)](https://travis-ci.org/JasonRivers/Docker-Nagios)

Nagios Core 4.4.3 running on Ubuntu 16.04 LTS with NagiosGraph & NRPE

### Configurations
Nagios Configuration lives in /opt/nagios/etc
NagiosGraph configuration lives in /opt/nagiosgraph/etc

### Install

```sh
docker pull jasonrivers/nagios:latest
```

### Running

Run with the example configuration with the following:

```sh
docker run --name nagios4 -p 0.0.0.0:8080:80 jasonrivers/nagios:latest
```

alternatively you can use external Nagios configuration & log data with the following:

```sh
docker run --name nagios4  \
  -v /path-to-nagios/etc/:/opt/nagios/etc/ \
  -v /path-to-nagios/var:/opt/nagios/var/ \
  -v /path-to-custom-plugins:/opt/Custom-Nagios-Plugins \
  -v /path-to-nagiosgraph-var:/opt/nagiosgraph/var \
  -v /path-to-nagiosgraph-etc:/opt/nagiosgraph/etc \
  -p 0.0.0.0:8080:80 jasonrivers/nagios:latest
```

Note: The path for the custom plugins will be /opt/Custom-Nagios-Plugins, you will need to reference this directory in your configuration scripts.

There are a number of environment variables that you can use to adjust the behaviour of the container:

| Environamne Variable | Description |
|--------|--------|
| MAIL_RELAY_HOST | Set Postfix relayhost |
| MAIL_INET_PROTOCOLS | set the inet_protocols in postfix |
| NAGIOS_FQDN | set the server Fully Qualified Domain Name in postfix |
| NAGIOS_TIMEZONE | set the timezone of the server |

For best results your Nagios image should have access to both IPv4 & IPv6 networks 

#### Credentials

The default credentials for the web interface is `nagiosadmin` / `nagios`

### Extra Plugins

* Nagios nrpe [<http://exchange.nagios.org/directory/Addons/Monitoring-Agents/NRPE--2D-Nagios-Remote-Plugin-Executor/details>]
* Nagiosgraph [<http://exchange.nagios.org/directory/Addons/Graphing-and-Trending/nagiosgraph/details>]
* JR-Nagios-Plugins -  custom plugins I've created [<https://github.com/JasonRivers/nagios-plugins>]
* WL-Nagios-Plugins -  custom plugins from William Leibzon [<https://github.com/willixix/WL-NagiosPlugins>]
* JE-Nagios-Plugins -  custom plugins from Justin Ellison [<https://github.com/justintime/nagios-plugins>]


#

## Students zone
#### Run the below commands:
    
    
    $ git clone https://github.com/Dgotlieb/Docker-Nagios.git
    $ cd Docker-Nagios
### For Mac / Linux
    $ docker run --name nagios -v $(pwd)/NagiosDocker/servers/:/etc/nagios/servers/ -p 0.0.0.0:8888:80 jasonrivers/nagios:latest
### For Windows
    $ docker run --name nagios -v /c/Users/<path_to_Nagios_Docker_Folder>/Docker-Nagios/NagiosDocker/servers/:/etc/nagios/servers/ -p 0.0.0.0:8888:80 jasonrivers/nagios:latest

### Continuing...
    $ docker ps
    $ docker exec -it nagios bin/bash
    $ apt update && apt install nano
    $ nano /opt/nagios/etc/nagios.cfg
### Add the below lines to the file:
    $ cfg_file=/etc/nagios/servers/google.cfg
    $ cfg_file=/etc/nagios/servers/github.cfg
    
### Enter the docker host address:
For Docker toolbox users: 192.168.99.100:8888
For Docker for Windwos/Mac localhost:8888

    Username : nagiosadmin
    Password: nagios
(Can be changed from opt/nagios/etc/cgi.cfg)

### On left panel go to: System => process info => restart nagios => commit => back to hosts
