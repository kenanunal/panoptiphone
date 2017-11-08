Panoptiphone
=============

Panoptiphone is a tool inspired by the web browser fingerprinting tool Panopticlick, which aims to show the identifying information that can be found in the frames broadcast by a Wi-Fi-enabled device. Information is passively collected from devices that have their Wi-Fi interface enabled, even if they are not connected to an access point. Panoptiphone uses this information to create a fingerprint of the device and empirically evaluate its uniqueness among a database of fingerprints. The user is then shown how much identifying information its device is leaking through Wi-Fi and how unique it is.

See details in the related paper: "Panoptiphone: How Unique is Your Wi-Fi Device?" https://hal.inria.fr/hal-01330479/file/paper.pdf


## Dependencies ##

- tshark
- python-tk
- python-matplotlib

## Install ##

Rename config.py.example config.py, and replace CHANGEME with a random key (chose a long and random password, you won't need to remember it).

## Usage ##


## Examples of uses ##

- CLI

```
$ ./panoptiphone.sh wlan0 # Live capture
Capturing on ’wlan0’
MAC address: c0:ee:fb:75:0d:59 (OnePlus Tech (Shenzhen) Ltd)
One in 13654.92 devices share this signature
Field                             | Entropy | One in x devices have this value | value
wps.uuid_e                        |  0.528  |                         5606.000 |
wlan_mgt.tag.number               |  0.483  |                       163812.000 | 0,1,50,3,45,221,127
wlan_mgt.supported_rates          |  0.304  |                       163793.000 | 2,4,11,22
wlan_mgt.extended_supported_rates |  0.302  |                       162962.000 | 12,18,24,36,48,72,96,108
wlan_mgt.ht.capabilities.psmp     |  0.301  |                       162962.000 | 0x0000012c
wlan_mgt.ht.ampduparam            |  0.000  |                            1.000 | 0x00000003
[...]
total                             |  3.489  |
```

```
$ python panoptiphone.py -d # dump database
163858 devices in the database
Information element | Entropy | Aff dev | Number of values
wlan_mgt.tag.length |   3.959 |  99.97  |  417
wlan_mgt.tag.number |   3.046 |  99.97  |  414
wlan_mgt.ssid       |   3.695 |  99.97  |  20592
[...]
total               |   5.834 |    -    |  163858
29171 devices (17.80%) are unique in the database
```

```
$ python panoptiphone.py -v wlan_mgt.txbf.txbf # list possible values of a field
Value     | Number of times seen
0;0       | 115512
0         | 17353
FFFFFFFF  | 4
```

- CLI and GUI:

[GUI example](example.png)