+++
title = "Setup OpenVPN for TryHackMe"
date = "2020-03-05"
weight = 90
+++

Our students use TryHackMe to practice their skills. You can do it at your own pace. The idea is to improve a little everyday. 

### Following are the instructions to set up VPN for TryHackMe

1. Login to Kali
2. Register an account in [TryHackMe](https://tryhackme.com/) 
3. Visit https://tryhackme.com/access Click on the green button ```Download My Configuration File```. You should get an “ovpn” file (for example, Happysaur.ovpn).  Move it to home dir or some better places than “Downloads”. 
4. Issue the following command
```html 
sudo apt-get install -y openvpn network-manager-openvpn network-manager-openvpn-gnome
```
5. Reboot Kali
6. Run openvn, assume your ovpn file is  “abc.ovpn”
```html 
sudo openvpn abc.ovpn 
```
7. Do not close or interrupt the terminal running openvpn. Open another tab or terminal for other commands.
8. To test if your VPN works or not, visit 
https://tryhackme.com/room/zthlinux   click on “Join Room”, then in Task 1, click on “Deploy”, then you’ll get an IP address
9. ```ssh``` to the IP address with  shiba1/shiba1. If you get in, then your VPN works.

