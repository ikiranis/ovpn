# ovpn
Setup ovpn with docker

https://hub.docker.com/r/kylemanna/openvpn/

Run the file setup.sh

Or 

```
docker volume create --name data
docker run -v data:/etc/openvpn --log-driver=none --rm kylemanna/openvpn ovpn_genconfig -u udp://my.server.com
docker run -v data:/etc/openvpn --log-driver=none --rm -it kylemanna/openvpn ovpn_initpki
```

Run container

```
docker run -v data:/etc/openvpn -d -p 1194:1194/udp --name ovpn --cap-add=NET_ADMIN kylemanna/openvpn
```

Generate a client certificate without a passphrase

```
docker run -v data:/etc/openvpn --log-driver=none --rm -it kylemanna/openvpn easyrsa build-client-full tardis nopass
```

Retrieve the client configuration with embedded certificates

```
docker run -v data:/etc/openvpn --log-driver=none --rm kylemanna/openvpn ovpn_getclient tardis > tardis.ovpn
```

Copy the tardis.ovpn file to your client and use it to connect 
