# Windows

## Requirements

* Exegol wrapper need python >= 3.6
* Python dependencies (in requirements.txt)
* Docker Desktop (using WSL2)
* Windows 10 is supported
* For GUI applications support
  * Windows 11 is needed
  * And at least one WSL distribution must be installed



## Features & limitations

| Feature                                    | Status                                                                                                                      |
| ------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------- |
| Open Exegol shell                          | :white\_check\_mark: Supported (work from CMD, powershell and WSL2 shell)                                                   |
| GUI                                        | :white\_check\_mark: Supported from Windows 11                                                                              |
| OpenVPN                                    | :white\_check\_mark: Supported                                                                                              |
| Dedicated network                          | :white\_check\_mark: Supported                                                                                              |
| Host network                               | :x: Not supported by [Docker Desktop](https://docs.docker.com/network/host/)                                                |
| Share specific network port                | :white\_check\_mark: Supported                                                                                              |
| Host timezone sharing                      | :large\_orange\_diamond: Supported (only from a WSL shell)                                                                  |
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

## Installation

WIP (refer to README.md on Github)



## GUI configuration

To enable exegol to support graphical application (or GUI) from a Windows host, you must:

* be on Windows 11 (WSLg is needed and only available from this release)
* with docker engine running on WSL2

![Docker Engine configuration (on WSL2)](<../../.gitbook/assets/image (4).png>)

* with at least one WSL distribution avec Docker / WSL integration

![Docker integration on WSL distro](<../../.gitbook/assets/image (1) (1).png>)
