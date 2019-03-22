# OpenVPN for Docker on ARM with MQTt support (RaspberryPi)

This is a fork from giggio/docker-openvpn-arm (https://github.com/giggio/docker-openvpn-arm) focused on ARM.

## Quick Start

* Pick a name for the `$OVPN_DATA` data volume container, it will be created automatically.

        OVPN_DATA="ovpn-data"

* Initialize the `$OVPN_DATA` container that will hold the configuration files and certificates

        docker volume create --name $OVPN_DATA
        docker run -v $OVPN_DATA:/etc/openvpn --rm giggio/openvpn-arm ovpn_genconfig -u udp://VPN.SERVERNAME.COM
        docker run -v $OVPN_DATA:/etc/openvpn --rm -it giggio/openvpn-arm ovpn_initpki nopass

* Start OpenVPN server process

        docker run -v $OVPN_DATA:/etc/openvpn -d --name openvpn -p 1194:1194/udp --cap-add=NET_ADMIN giggio/openvpn-arm

* Generate a client certificate without a passphrase

        docker run -v $OVPN_DATA:/etc/openvpn --rm -it giggio/openvpn-arm easyrsa build-client-full CLIENTNAME nopass

* Retrieve the client configuration with embedded certificates

        docker run -v $OVPN_DATA:/etc/openvpn --rm giggio/openvpn-arm ovpn_getclient CLIENTNAME > CLIENTNAME.ovpn
