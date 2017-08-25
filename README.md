<h1 align="center">neo-docker</h1>

<p align="center">
  Custom docker images for <b>NEO</b> Blockchain
</p>

## What?

- Docker images for testing and interacting [NEO](http://neo.org/) blockchain.
- Docker images are ephemeral, at this moment persistence is not implemented. **The data (wallets/priv keys) won’t persist when that container is no longer running.**

## Quick Start

```
PS C:\> git clone https://github.com/jonatanblockchain/neo-docker.git
```
```
PS C:\> cd .\neo-docker\neo-cli\centos
PS C:\neo-docker\neo-cli\centos> docker build -t neo-cli .
```
```
PS C:\neo-docker\neo-cli\centos>  docker images
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
neo>
neo>show state
 Height: 1000/11746, Nodes: 6
```

