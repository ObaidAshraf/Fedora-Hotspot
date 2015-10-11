# Fedora-Hotspot
Setting up Hotspot in Fedora with DHCP server.

This document demonstrates about how to create a hotspot in Fedora so that you can share your local network with your other wireless devices (such as laptops, smartphones etc) and wireless clients.

# Hardware Requirements:
1) A WAN interface with internet (in my case, it is em1).

2) A USB router that supports AP mode (i am using LinkSys WUSB200N)

3) A Linux box (i am using Fedora17)


# Software requirements:
1) Hostapd module

2) DHCP module

3) IPtables module (which is available by-default in most cases)

# Procedure:
Install hostapd and dhcp module using:

yum -y install hostapd dhcp;

Configure hostapd.conf found at /etc/hostapd/hostapd.conf, dhcpd.conf found at /etc/dhcp/dhcpd.conf and dhcpd file found at /etc/sysconfig/dhcpd to setup in configuration.

Now, you need to setup packet forwarding between your LAN and WAN interfaces and enabling MASQUERADE so that clients those gets connected via wireless interface (here wlan0) gets access to internet.

You can achieve this using the following steps:

Edit /etc/sysctl.conf file and set net.ipv4.ip_forward = 1.

and now use the following command to enable NAT and MASQUERADE:

iptables -t nat -A POSTROUTING -s 192.168.0.0/16 -j MASQUERADE

