# Networking

ifconfig

iwconfig

netstat 



## View available Wifi netorks

`sudo iwlist [interface] scan` scans all available wifi networks using the interface specified (or all interfaces if none are specified)

this can be a bit verbose so try

	sudo iwlist scan | grep "ESSID"

to just view the names of the network and use 

	sudo iwlist scan | grep [network_name] -B 4

to view the informatio for a particular network

## Connect to wifi from command line

make sure wpasupplicant package is installed

	sudo apt install wpasupplicant

make a configuration file
this can be done simply by running

	wpa_passphrase myrouter mypassphrase > /etc/wpa_supplicant.conf

or creating the file manually and writing:

```
network={
    ssid="ssid_name"
    psk="password"
}
```

Connect by running the 2 commands below

	sudo wpa_supplicant -B -iwlan0 -c/etc/wpa_supplicant.conf -Dwext
	sudo dhclient wlan0

**Yes it is deliberate there are no spaces between the parameter letter and value**

 - **-B** runs it as a daemon in the background
 - **-i** is the interface to use
 - **-c** is the path to the config file you created earlier
 - **-D** option specifies driver to use, `wext` is the generic one and should work

