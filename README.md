
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

You will also want install usb support for WSL. In a separate windows command
prompt, while wsl is running in the original command prompt, run the following
commands to download usb support and attach the usb to WSL:

```cmd
winget install usbipd
usbipd list
usbipd bind --busid <busid>
usbipd attach --wsl --busid <busid> --auto-attach
```

Back in the wsl shell install Ubuntu dependencies:

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

Pull in Zephyr and modules:

```sh
west update
west zephyr-export
west packages pip --install
```

Install SDK:

```sh
cd
wget https://github.com/zephyrproject-rtos/sdk-ng/releases/download/v0.17.4/zephyr-sdk-0.17.4_linux-x86_64_minimal.tar.xz
tar vxf zephyr-sdk-0.17.4_linux-x86_64_minimal.tar.xz
cd zephyr-sdk-0.17.4
./setup.sh -t arm-zephyr-eabi
```

To build the blinky app:

```sh
cd ~/zephyr-nrf52833dk/app
west build -p
```

To build the bluetooth app:

```sh
cd ~/zephyr-nrf52833dk/bluetooth-app
west build -p
```

Now you can flash with:

```sh
west flash
```
This will require you to have connected the USB to the wsl instance.

After closing your Linux terminal you will need to re-source your virtual
environment to get access to `west` again:

```sh
cd ~/zephyr-nrf52833dk
source venv/bin/activate
```
