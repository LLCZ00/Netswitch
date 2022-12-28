# Netswitch
### _Netplan Configuration Switch_
Netswitch was designed to facilitate the quick and easy change of the Netplan network configuration file, for the purposes of network testing/setup on Debian/Ubuntu virtual machines. Manually editing the config file via VIM becomes poison to a man's soul if done too often.
## Usage
```
usage: netswitch.py [-h] [--dhcp] [-a IP/CIDR] [-d IP] [-g IP] [-dg IP] [-i INTERFACE] [-c FILEPATH] [--print]
                    [--apply] [--version]
optional arguments:
  -h, --help            show this help message and exit
  --dhcp                Turn on DHCP
  -a IP/CIDR, --address IP/CIDR
                        Set IP address
  -d IP, --dns IP       Set DNS nameserver address
  -g IP, --gateway IP   Set default gateway address
  -dg IP, --dns-gateway IP
                        Set DNS and default gateway to the same address
  -i INTERFACE, --interface INTERFACE
                        Set target interface (Default: enp0s3)
  -c FILEPATH, --config FILEPATH
                        Specify path of config file to edit/create (Default: /etc/netplan/01-netcfg.yaml)
  --print               Print current netplan configuration
  --apply               Run 'netplan apply' command after writing config
  --version             Show version number and exit
Examples:
	/netswitch.py -a 10.10.10.1/16
	./netswitch.py --dhcp
	./netswitch.py --address=192.168.1.1/24 -dg 192.168.1.2 --apply
```
Netswitch simply overwrites /etc/netplan/01-netcfg.yaml to either enable DHCP, or manually set the given IP address, DNS nameserver, and/or default gateway. The virtual machine network settings can then be set to the corresponding configuration (Bridged Adapter/ Interal) to easily switch between internal and open internet.

Root privilages are required to edit and apply the netplan configuration.
## Known Issues & TODO
- Add way to detect default interface, because ensp0s3 is not universal
	- Currently the easiest solution is to just edit the default interface in the script directly
- Add ability to edit specific aspects of configuration
	- As of right now the whole thing is overwritten each time it's edited
