# docker-ldap
Dockerized OpenLDAP using Osixia

# How to use
This will create a docker container for OpenLDAP. Settings have been preconfigured to allow this to run quickly. Here are the basic configuration items:

```
docker-compose.yml
      LDAP_BASE_DN: "dc=test,dc=com"
      LDAP_ADMIN_PASSWORD: "admin"

      LDAP_TLS: "false"
```

***NOTE***: TLS/SSL is disabled in the supplied docker-compose.yml. If TLS is enabled, certificates will need to be generated and the LDAP_TLS_* environment variables will need to point to appropriate configuration files or settings.

OpenLDAP is configurd to listen on port 389, but exposes the LDAP outside the container on port 3389. Similarly, the phpLdapAdmin listens on port 80 within the container, but is exposed as port 8389. To change these ports, please look in the docker-compose.yml file:

```
services:
  openldap:
    image: osixia/openldap:1.2.3
.
.
.
    ports:
      - "3389:389"
      - "3636:636"
```
 
Take note that the port 636 is the default TlS port and it is exposed on 3636 outside the container to the host. By default, the docker-compose.yml disables TLS.

For the phpLdapAdmin, the docker-compose.yml file can also be edited to change the ports used;

```
  phpldapadmin:
    image: osixia/phpldapadmin:latest
    container_name: phpldapadmin
.
.
.
    ports:
      - "8389:80"
```

## Creating the Servers
Create the OpenLDAP Server and the phpLdapAdmin by executing Docker compose:

	docker-compose up -d

# Using phpLdapAdmin

Information on running phpLdapAdmin can be found at [docker-phpLDAPadmin Github page](https://github.com/osixia/docker-phpLDAPadmin).


# Diagnostics and Uninstalling Containers

## Stopping the LDAP Server
To stop the OpenLDAP server's container simply issue the following command;

	docker container stop test-ldap

## Stopping phpLdapAdmin
To stop the phpLdapAdmin container simply issue the following command;

	docker container stop phpldapadmin

## Removing the Containers
To remove the containers, simply execute the docker container rm command:

	docker container rm test-ldap phpldapadmin

## Container Logs
To view the container logs, use the following commands:

	docker logs test-ldap
	docker logs phpldapadmin



