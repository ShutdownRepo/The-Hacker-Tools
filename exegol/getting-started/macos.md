# macOS

## Setup

talk about requirements cker for Desktop, XQuartz, Rosetta 2 (?), requirements for git installation, ...

## Limitations and known issues

### Network modes

Docker for Desktop for macOS runs docker containers inside an xhyve VM with its own network. The host interface cannot be bridge directly to the docker containers, hence preventing the `--network host` feature to work as intended (i.e. the container uses the host's network).

### Disk usage

Docker for Desktop for macOS has a set of settings limiting the resources shares with the containers. In case there is a `no space left on device` error raised when pulling or building, it might come from there.

![](<../../.gitbook/assets/image (3).png>)
