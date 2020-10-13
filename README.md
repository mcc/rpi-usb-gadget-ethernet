# rpi-usb-gadget-ethernet
How to enable usb gadget ethernet mode for Raspberry Pi 4

- Flash Raspbrian OS
- Add dtoverlay=dwc2 to the /config.txt
- Add modules-load=dwc2,g_ether to the after rootwait of /cmdline.txt, e.g
<pre>
rootwait modules-load=dwc2,g_ether
</pre>
- Create file ssh in /
- Add libcomposite to /etc/modules
- Add denyinterfaces usb0 to /etc/dhcpcd.conf
- Install dnsmasq with sudo apt-get install dnsmasq
- Create /etc/dnsmasq.d/usb with following content
<pre>
interface=usb0
dhcp-range=10.55.0.2,10.55.0.6,255.255.255.248,1h
dhcp-option=3
leasefile-ro
</pre>
- Create /etc/network/interfaces.d/usb0 with the following content
<pre>
auto usb0
allow-hotplug usb0
iface usb0 inet static
  address 10.55.0.1
  netmask 255.255.255.248
</pre>

