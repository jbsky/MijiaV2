# MijiaV2

Bash script that allows to query several MijiaV2 sensors one by one and the information is sent to influxdb.

2 scripts available, the poller and the init.d.

source of inspiration: https://www.fanjoe.be/?p=3911


# Prerequisites
### Update your raspberry :
* Update the raspbian distribution : `sudo apt update & sudo apt upgrade`
* update the firmware : `sudo rpi-update`

# Integration :
* copy the files directly into their respective places and make them executable :

`curl https://raw.githubusercontent.com/jbsky/MijiaV2/master/sbin/mijiav2 -o /usr/local/sbin/mijiav2`

`curl https://raw.githubusercontent.com/jbsky/MijiaV2/master/init.d/mijiav2 -o /etc/init.d/mijiav2`

`chmod +x /usr/local/sbin/mijiav2 & chmod +x etc/init.d/mijiav2`

# Configuration :
### In /usr/local/sbin/mijiav2, at the beginning of the file :
* change addMAC , please quote the addresses :
_ex: addMAC = ("AA:BB:CC:DD:EE:FF" "11:22:33:44:55:66")_

* Add label corresponding for each MAC address, of course with the same constraints.  :
_ex: ("Vitre\ Salon" "Salon" "Chambre\ Mathilde" "Chambre\ Parent")_

* change influxDB IP :
_influxDB="192.168.10.182:8086"_

* change the name of the influxDB database :
_db="temperature"

# Execution :
* Simply as a service : `sudo systemctl start mijiav2.service`

# Execute at boot time
* Enable the service : `sudo systemctl enable mijiav2.service`

# Conclusion :
It is a simple solution to capture data from these small sensors from Xiaomi.

It doesn't wait stupidly after a timeout, this is made possible by a file that counts lines every second.


## Limitation:
no multiple parallel connection, no threading. Without saying anything stupid, I don't think the raspberry's bluetooth supports it.
