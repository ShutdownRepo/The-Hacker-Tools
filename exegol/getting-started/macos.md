# macOS

## Requirements

* Exegol wrapper need python >= 3.6
* Python dependencies (in requirements.txt)
* Docker Desktop
* For GUI applications support
  * XQuartz (with `Allow connections from network clients` config set to true)

## Features & limitations

| Feature                                    | Status                                                                                                                      |
| ------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------- |
| Open Exegol shell                          | :white\_check\_mark: Supported                                                                                              |
| GUI                                        | :white\_check\_mark: Supported with XQuartz                                                                                 |
| OpenVPN                                    | :white\_check\_mark: Supported                                                                                              |
| Dedicated network                          | :white\_check\_mark: Supported                                                                                              |
| Host network                               | :x: Not supported by [Docker Desktop](https://docs.docker.com/network/host/)                                                |
| Share specific network port                | :white\_check\_mark: Supported                                                                                              |
| Host timezone sharing                      | :white\_check\_mark: Supported                                                                                              |
| Custom workspace directory sharing         | :white\_check\_mark: Supported                                                                                              |
| Exegol resources                           | :white\_check\_mark: Supported                                                                                              |
| My resources                               | :white\_check\_mark: Supported                                                                                              |
| Custom environment variable                | :white\_check\_mark: Supported                                                                                              |
| Share device                               | :x: Not supported by [Docker Desktop](https://docs.docker.com/desktop/faqs/#can-i-pass-through-a-usb-device-to-a-container) |
| Share additonal filesystem volume          | :white\_check\_mark: Supported                                                                                              |
| Self-update image source code              | :white\_check\_mark: Supported (with source code install)                                                                   |
| Self-update exegol resources               | :white\_check\_mark: Supported                                                                                              |
| Self-update exegol wrapper                 | :white\_check\_mark: Supported (with source code install)                                                                   |
| Install and update exegol image            | :white\_check\_mark: Supported                                                                                              |
| Build local image                          | :white\_check\_mark: Supported                                                                                              |
| Execute a command in background            | :white\_check\_mark: Supported                                                                                              |
| Execute a command in a temporary container | :white\_check\_mark: Supported                                                                                              |

## Setup

talk about requirements cker for Desktop, XQuartz, Rosetta 2 (?), requirements for git installation, ...

## Limitations and known issues

### ARM Host (M1)

Some package don't exist for ARM (e.g. Tor, rar, ...)

### Network modes

Docker for Desktop for macOS runs docker containers inside an xhyve VM with its own network. The host interface cannot be bridge directly to the docker containers, hence preventing the `--network host` feature to work as intended (i.e. the container uses the host's network).

### Disk usage

Docker for Desktop for macOS has a set of settings limiting the resources shares with the containers. In case there is a `no space left on device` error raised when pulling or building, it might come from there.

![](<../../.gitbook/assets/image (3).png>)
