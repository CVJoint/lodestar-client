# Lodestar Client - Docker

This project uses the official Lodestar client [chainsafe/lodestar](https://hub.docker.com/r/chainsafe/lodestar) which includes the relevant configuration for the `gnosis` network.

Pulling the latest Lodestar beacon client would look like this:

```
docker pull chainsafe/lodestar:latest
```

## Lodestar reference

- General: https://chainsafe.github.io/lodestar/
- CLI Reference: https://chainsafe.github.io/lodestar/reference/cli/

# Starting Lodestar on mainnet

1. Create your folder structure:

```
mkdir -p /home/$USER/gnosis/el-client
mkdir -p /home/$USER/gnosis/cl-client/data
mkdir /home/$USER/gnosis/cl-client/keystores
mkdir /home/$USER/gnosis/cl-client/validators
mkdir /home/$USER/gnosis/jwtsecret
```

2. Add an `.env` file with your WAN IP (`curl https://ipinfo.io/ip`), fee recepient (your gnosis address), graffiti, and checkpoint url `/home/$USER/gnosis/.env`.

```
WAN_IP:123.456.789.012
FEE_RECIPIENT=0x0000000000000000000000000000000000000000
GRAFFITI=gnosischain/lighthouse
CHECKPOINT_URL=https://checkpoint.gnosischain.com/
```

3. Add your keystores in `/home/$USER/gnosis/cl-client/keystores` and their password in a file `/home/$USER/gnosis/cl-client/keystores/password.txt` to get this file structure:

```
/home/$USER/gnosis/
├── docker-compose.yml
├── .env
├── jwtsecret/
├── el-client/
└── cl-client/
    ├── data/
    ├── keystores/
    │   ├── keystore-001.json
    │   ├── keystore-002.json
    │   └── password.txt
    ├── logs/
    └── validators/
```

4. Create a new `./jwtsecret` token:

```
openssl rand -hex 32 | tr -d "\n" > /home/$USER/gnosis/jwtsecret/jwtsecret
```

5. Import your validators:

```
```

6. Start `docker-compose.yml` services from this repository

```
cd /home/$USER/gnosis
docker-compose up -d
```

7. Check your logs for each service (`el-client`, `cl-client`, or `validator`) with:

```
docker logs -f --tail 500 <service>
```

8. To update, just pull the new images, then stop and restart your docker-compose file:
```
cd /home/$USER/gnosis
docker-compose pull
docker-compose stop
docker-compose up -d
```
