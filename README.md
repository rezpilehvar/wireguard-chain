# WireGuard chain
docker compose and configs for wireguard to make a private network over two/many nodes

### Terminology

* Upstream Server: A server that has free access to the Internet.
* Bridge Server: A server that is available to clients and has access to an upstream server.
* Client: A user-side application with access to the bridge server.

### Setup servers
1. copy docker-compose and config files into your machines
2. create two public/private keys for both of them
3. change the bridge/config/wg0.conf by the hints on that
4. change the upstream/config/wg0.conf like bridge

### Add new peer
generate a private key
```bash
wg genkey | tee clientpk
```
and after that get the public key
```bash
cat clientpk | wg pubkey
```
the first command will print the [PEER_PRIVATE_KEY] and the second one prints [PEER_PUBLIC_KEY]

add a [Peer] block the bridge server config
```bash
[Peer]
PublicKey = [PEER_PUBLIC_KEY]
AllowedIPs = 10.10.10.4/32
```
you need to set the Allowed ip according to your internal subnet mask ip

and at the end you need to create config file which an example is in the bridge/clients/example.conf, you need to modify the hints based on
peer_public_key which generated before and set the other hints