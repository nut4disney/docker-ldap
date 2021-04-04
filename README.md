# docker-ldap
Dockerized OpenLDAP using Osixia

# How to use
This will create a docker container for OpenLDAP. Settings have been preconffigured to allow this to run quickly. Here are the basic configuration items:

      LDAP_BASE_DN: "dc=test,dc=com"
      LDAP_ADMIN_PASSWORD: "admin"

NOTE: TLS/SSL is disabled. 

OpenLDAP is configurd to listen on port 389, but exposes the LDAP outside the container on port 3389. Similarly, the phpLdapAdmin listens on port 80 within the container, but is exposed as port 8389. To change these ports, please look in the docker-compose.yml file:

'''
services:
  openldap:
    image: osixia/openldap:1.2.3
.
.
.
    ports:
      - "3389:389"
      - "3636:636"
'''
Notice that the port 636 is the default TlS port and it is exposed on 3636 outside the container to the host. By default, the docker-compose.yml disables TLS.

'''
  phpldapadmin:
    image: osixia/phpldapadmin:latest
    container_name: phpldapadmin
.
.
.
    ports:
      - "8389:80"
'''

## Creating the Servers
Create the OpenLDAP Server and the phpLdapAdmin by executing Docker compose:

'''
docker-compose up -d
'''

## Stopping the LDAP Server
docker container stop test-ldap

## Stopping phpLdapAdmin
docker container stop phpldapadmin

## Removing the Containers
docker container rm test-ldap phpldapadmin

## Looking at th elogs
docker logs test-ldap
docker logs phpldapadmin



