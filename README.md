# OpenVPN for Docker on ARM with MQTT support (RaspberryPi)

This is a fork from giggio/docker-openvpn-arm (https://github.com/giggio/docker-openvpn-arm) focused on ARM.
Original forked from kylemanna/docker-openvpn (https://github.com/kylemanna/docker-openvpn).

MQTT notification on connect to OpenVPN Server via Mosquitto added.

## Quick Start

* Setup storage location or container that will hold the configuration files and certificates

        docker run -v YOURPATH:/etc/openvpn --rm katsuoya/docker-openvpn-mqttnotify-arm ovpn_genconfig -u udp://VPN.SERVERNAME.COM
        docker run -v YOURPATH:/etc/openvpn --rm -it katsuoya/docker-openvpn-mqttnotify-arm ovpn_initpki nopass

* Start OpenVPN server process

        docker run -v YOURPATH:/etc/openvpn -d --name openvpn-mqtt -p 1194:1194/udp --cap-add=NET_ADMIN katsuoya/docker-openvpn-mqttnotify-arm
* Start OpenVPN server process on Ubuntu

        docker run -v YOURPATH:/etc/openvpn -d --name openvpn-mqtt -p 1194:1194/udp --cap-add=NET_ADMIN --privileged katsuoya/docker-openvpn-mqttnotify-arm 

* Generate a client certificate without a passphrase

        docker run -v YOURPATH:/etc/openvpn --rm -it katsuoya/docker-openvpn-mqttnotify-arm easyrsa build-client-full CLIENTNAME nopass

* Retrieve the client configuration with embedded certificates

        docker run -v YOURPATH:/etc/openvpn --rm katsuoya/docker-openvpn-mqttnotify-arm ovpn_getclient CLIENTNAME > CLIENTNAME.ovpn
