# Linux

## Requirements

* Exegol wrapper need python >= 3.6
* Python dependencies (in requirements.txt)
* Docker

## Features & limitations

| Feature                                    | Status                                                    |
| ------------------------------------------ | --------------------------------------------------------- |
| Open Exegol shell                          | :white\_check\_mark: Supported                            |
| GUI                                        | :white\_check\_mark: Supported                            |
| OpenVPN                                    | :white\_check\_mark: Supported                            |
| Dedicated network                          | :white\_check\_mark: Supported                            |
| Host network                               | :white\_check\_mark: Supported                            |
| Share specific network port                | :white\_check\_mark: Supported                            |
| Host timezone sharing                      | :white\_check\_mark: Supported                            |
| Custom workspace directory sharing         | :white\_check\_mark: Supported                            |
| Exegol resources                           | :white\_check\_mark: Supported                            |
| My resources                               | :white\_check\_mark: Supported                            |
| Custom environment variable                | :white\_check\_mark: Supported                            |
| Share device                               | :white\_check\_mark: Supported                            |
| Share additonal filesystem volume          | :white\_check\_mark: Supported                            |
| Self-update image source code              | :white\_check\_mark: Supported (with source code install) |
| Self-update exegol resources               | :white\_check\_mark: Supported                            |
| Self-update exegol wrapper                 | :white\_check\_mark: Supported (with source code install) |
| Install and update exegol image            | :white\_check\_mark: Supported                            |
| Build local image                          | :white\_check\_mark: Supported                            |
| Execute a command in background            | :white\_check\_mark: Supported                            |
| Execute a command in a temporary container | :white\_check\_mark: Supported                            |

## 1. Wrapper

### From pip

```bash
python3 -m pip install exegol
```

### From sources

```bash
git clone https://github.com/ShutdownRepo/Exegol
cd Exegol
python3 -m pip install --user --requirement requirements.txt
sudo ln -s $(pwd)/exegol.py /usr/local/bin/exegol
```

## 2. Images

```bash
# Without options, the following command will start an interactive process
exegol install

# If the user already knows the image to install
exegol install <image>
```

## 3. Container

```bash
# Without options, the following command will start an interactive process
exegol start

# If the user already knows the name to set to the container
exegol start <container>

# If the user already knows the name to set to the container, and the image it must be create with
exegol start <container> <image>
```
