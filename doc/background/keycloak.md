# Keycloak background documentation
The following documentation is intended to provide generic information on Keycloak as well as links to documentation and some tips and tricks for things found during the initial phase of the project.

## generic information
Keycloak is an open source Identity and Access Management solution aimed at modern applications and services. It makes it easy to secure applications and services with little to no code. More information on Keycloak can also be found at the [Keycloak website](https://www.keycloak.org).

## documentation links

## tips and tricks
A set of tips and tricks for things found in the initial phase of the project.

### 1 Keycloak only available on the localhost loopback address 
By default Keycloak binds to the localhost loopback address 127.0.0.1. That’s not a very useful default if you want the authentication server available on your network. To bind Keycloak to a specific interface you can start Keycloak with -b flag as shown below
```
$ standalone.sh -b 192.168.0.5
```
In addition you can change the default by editing the  profile configuration file (standalone.xml or domain.xml depending on your operating mode) as shown below
```
    <interfaces>
        <interface name="management">
            <inet-address value="${jboss.bind.address.management:127.0.0.1}"/>
        </interface>
        <interface name="public">
            <inet-address value="${jboss.bind.address:127.0.0.1}"/>
        </interface>
    </interfaces>
```
