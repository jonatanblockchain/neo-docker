
<h1 align="center">neo-docker</h1>

<p align="center">
  Custom docker images for <b>NEO</b> Blockchain
</p>

## What?

- Docker images for testing and interacting with [NEO](http://neo.org/) blockchain.
- Docker images are ephemeral, at this moment persistence is not implemented. **The data (wallets/accounts/priv keys) won’t persist when the container is destroyed.**

## Quick Start (Main Net)

```
PS C:\> git clone https://github.com/jonatanblockchain/neo-docker.git
```
```
PS C:\> cd .\neo-docker\neo-cli\centos
PS C:\neo-docker\neo-cli\centos> docker build -t neo-cli .
```
```
PS C:\neo-docker\neo-cli\centos> docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
neo-cli             latest              1e040946054c        6 seconds ago       694MB
centos              centos7             328edcd84f1b        3 weeks ago         193MB
```
```
PS C:\neo-docker\neo-cli\centos> docker run -dit neo-cli
5250679a40cb560840016969f2538e7521e04b33c4cbe94c4ce95fbe924b5c79
```
```
PS C:\neo-docker\neo-cli\centos> docker ps
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS
   NAMES
5250679a40cb        neo-cli             "dotnet neo-cli.dll"   19 seconds ago      Up 18 seconds       10333/tcp
```
```
PS C:\neo-docker\neo-cli\centos> docker attach 5250679a40cb
(press Enter)
neo>
neo>show state
 Height: 1000/11746, Nodes: 6
```

## Quick Start (Test Net)

Follow the first two steps above (git clone and docker build), then do the following:

```bash
$ docker run -it --entrypoint bash neo-cli
```
This will give you a bash prompt in the container:
```bash
root@fbd0d69fd8d8:/opt/neo-cli#
```
Run these commands to copy the testnet configs over the main one:
```bash
root@fbd0d69fd8d8:/opt/neo-cli# cp protocol.testnet.json protocol.json
root@fbd0d69fd8d8:/opt/neo-cli# cp config.testnet.json config.json
```
Verify that the testnet configs have overwritten `protocol.json` and `config.json`:
```bash
root@fbd0d69fd8d8:/opt/neo-cli# md5sum {protocol,config}*.json
e47f095e351be4f0b3bbf09a6e05cacb  protocol.json
c6739eab607de2ad9402c225ad880ecb  protocol.mainnet.json
e47f095e351be4f0b3bbf09a6e05cacb  protocol.testnet.json
c47b2a2e21928e88b557c0036205cf5e  config.json
bd6fd03fb1aee43e8faf19b474cd12db  config.mainnet.json
c47b2a2e21928e88b557c0036205cf5e  config.testnet.json
```
Only the `*.mainnet.json` files should show different MD5 hashes.

Then you may run `neo-cli` as normal:
```bash
root@fbd0d69fd8d8:/opt/neo-cli# dotnet neo-cli.dll
neo>
```

## Exiting and Resuming

To exit neo-cli:
```bash
neo>exit
root@fbd0d69fd8d8:/opt/neo-cli# exit
```

Resuming the session later (keeps data):
```bash
$ docker start -a fbd0d69fd8d8
```
