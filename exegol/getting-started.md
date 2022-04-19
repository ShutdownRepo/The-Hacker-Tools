# Getting started

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
