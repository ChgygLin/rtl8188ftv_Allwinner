RTL8188FTV Driver for RK3588 OrangePi 5.
For Kernel 5.10.110 on Linux Ubuntu Jammy.

Compatible with both USB Type-A dongles/adapters, and embedded 2.4ghz wireless radio modules, using the Realtek RTL8188FTV chip. Modified from Kelebek333's rtl8188fu driver.

------------------

## Installation

OrangePi5 linux headers: https://drive.google.com/drive/folders/1SiUkTWQ5X7U07e5GJvLirqtrVRCIxfr5

linux-headers-legacy-rockchip-rk3588_1.1.2_arm64.deb

1) `cd rtl8188ftv_Allwinner`
2) `make -j && make install`
3) `cp -r ./firmware/rtl8188fufw.bin /lib/firmware/rtlwifi/ && modprobe rtl8188fu`

------------------

## Configuration

#### Disable Power Management

Run following commands for disable power management and plugging/replugging issues.

`sudo mkdir -p /etc/modprobe.d/`

`sudo touch /etc/modprobe.d/rtl8188fu.conf`

`echo "options rtl8188fu rtw_power_mgnt=0 rtw_enusbss=0" | sudo tee /etc/modprobe.d/rtl8188fu.conf`

#### Disable MAC Address Spoofing

Run following commands for disabling MAC Address Spoofing (Note: This is not needed on Ubuntu based distributions. MAC Address Spoofing is already disabled on Ubuntu base).

`sudo mkdir -p /etc/NetworkManager/conf.d/`

`sudo touch /etc/NetworkManager/conf.d/disable-random-mac.conf`

`echo -e "[device]\nwifi.scan-rand-mac-address=no" | sudo tee /etc/NetworkManager/conf.d/disable-random-mac.conf`

#### Blacklist for kernel 5.15 and newer

If you are using kernel 5.15 and newer, you must create a configuration file with following commands for preventing to conflict rtl8188fu module with built-in r8188eu module.

`echo 'alias usb:v0BDApF179d*dc*dsc*dp*icFFiscFFipFFin* rtl8188fu' | sudo tee /etc/modprobe.d/r8188eu-blacklist.conf`

------------------

## Uninstalling

`sudo dkms remove rtl8188fu/1.0 --all`

`sudo rm -f /lib/firmware/rtlwifi/rtl8188fufw.bin`

`sudo rm -f /etc/modprobe.d/rtl8188fu.conf`

------------------

## Platform Testing

Currently known working with Orange Pi Zero Plus 2 (Allwinner H3).
I will expand this section as more platforms are tested.
