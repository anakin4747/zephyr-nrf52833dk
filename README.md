
# NRF52833 DK BLINKY EXAMPLE

This build is meant for Ubuntu so install WSL Ubuntu if you are on Windows.

You can install Ubuntu-22.04 WSL with the following command from a Windows
command prompt. You may need to run the command prompt as an administrator.

```cmd
wsl --install -d Ubuntu-22.04
```

This will install Ubuntu-22.04 and start a terminal inside it.

If you close the terminal you can get back to it with the following command:

```cmd
wsl -d Ubuntu-22.04
```

Install Ubuntu dependencies:

```sh
sudo apt update
sudo apt upgrade
sudo apt install --no-install-recommends git cmake ninja-build gperf \
  ccache dfu-util device-tree-compiler wget python3-dev python3-venv python3-tk \
  xz-utils file make gcc gcc-multilib g++-multilib libsdl2-dev libmagic1
```

Next install this codebase with `git`:

```sh
cd
git clone https://github.com/anakin4747/zephyr-nrf52833dk
cd zephyr-nrf52833dk
```

Create a virtual environment and install `west` into it:

```sh
python3 -m venv venv
source venv/bin/activate
pip install west
```

Pull in Zephyr and modules and install SDK:

```sh
west update
west zephyr-export
west packages pip --install
west sdk install
```

Build and flash application:

```sh
cd app
west build -p
west flash # not tested
```

After closing your Linux terminal you will need to re-source your virtual
environment to get access to `west` again:

```sh
cd ~/zephyr-nrf52833dk
source venv/bin/activate
```
