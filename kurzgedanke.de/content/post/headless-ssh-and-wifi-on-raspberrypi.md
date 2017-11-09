---
title: "Headless ssh and Wifi on RaspberryPi"
date: 2017-11-01T15:57:30+01:00
draft: false
tags: ["RaspberryPi", "SSH", "WiFi"]
---

#### SSH: 

To enable SSH on a RaspberryPi with out a monitor, keyboard or mouse put your SD-Card in a card reader
and plug into your main PC.

<!--more-->

Open up a terminal and navigate to the SD Card.

```bash
# On Mac:
╭─loki@lokiTheGod ~
╰─$ cd /Volumes
╭─loki@lokiTheGod /Volumes
╰─$ ls
BOOTCAMP     MACINTOSH HD Untitled     boot
```

Now you are in the Volumes folder, which shows all drives connected to your mac. You have to create an empty `ssh` file on the Pi SD-Card. 

```bash
╭─loki@lokiTheGod /Volumes
╰─$ cd boot
╭─loki@lokiTheGod /Volumes/boot
╰─$ touch ssh
```

Enter `cd boot` to go into the Pi SD-Card and then type in `touch ssh` to create an empty ssh file.

You can verify this by typing `ls` in your terminal.

#### WiFi: 

> Personally this approach didn't worked for me... so the easiest way to it is via Ethernet.

To enable WiFi directly on your headless Pi place a file name `wpa_supplicant.conf` in the boot directory of your Pi.

The `wpa_supplicant.conf` is moved while the Pi starts to `/etc/wpa_supplicant/wpa_supplicant.conf` where the the wpa configurations are located.

A simple and for most networks sufficient `wpa_supplicant.conf` looks like this:

###### WPA:

```bash
network={
    ssid="YOUR_SSID"
    psk="YOUR_PASSWORD"
    key_mgmt=WPA-PSK
}
```

###### WPA2:

```bash
network={
    ssid="YOUR_NETWORK_NAME"
    psk="YOUR_NETWORK_PASSWORD"
    proto=RSN
    key_mgmt=WPA-PSK
    pairwise=CCMP
    auth_alg=OPEN
}
```

For more information on this you can look at the [Arch Wiki WPA supplicant site (Link)](https://wiki.archlinux.org/index.php/WPA_supplicant).

Have lot of fun with your Pi!