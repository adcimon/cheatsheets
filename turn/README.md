# TURN

[Traversal Using Relays around NAT (TURN)](https://en.wikipedia.org/wiki/Traversal_Using_Relays_around_NAT) is a protocol that assists in traversal of [Network Address Translators (NAT)](https://en.wikipedia.org/wiki/Network_address_translation) or firewalls for multimedia applications. It is most useful for clients on networks masqueraded by [symmetric NAT](https://en.wikipedia.org/wiki/Network_address_translation#Symmetric_NAT) devices.

## Coturn

[Coturn](https://github.com/coturn) is a media traffic NAT traversal server and gateway that can be used as a general-purpose network traffic TURN server.

Install using official docker image [instrumentisto/coturn](https://hub.docker.com/r/instrumentisto/coturn).
```
docker run -d --network=host \
           -v $(pwd)/turnserver.conf:/etc/coturn/turnserver.conf \
           instrumentisto/coturn
```

## References

* [Coturn Wiki](https://github.com/coturn/coturn/wiki/)
* [BigBlueButton Configure TURN](https://docs.bigbluebutton.org/admin/setup-turn-server.html)
* [How to set up and configure your own TURN server using Coturn](https://gabrieltanner.org/blog/turn-server/)
