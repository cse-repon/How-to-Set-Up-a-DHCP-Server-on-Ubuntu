<img width="1518" height="176" alt="image" src="https://github.com/user-attachments/assets/c1d44581-de16-4e8d-9b23-c23714f8ebe5" /># How-to-Set-Up-a-DHCP-Server-on-Ubuntu

Original video link: https://www.youtube.com/watch?v=9DtQRU7XHqw

'''
sudo apt update && sudo apt upgrade -y

sudo apt install isc-dhcp-server
sudo systemctl status isc-dhcp-server

sudo nano /etc/dhcp/dhcpd.conf


# No service will be given on this subnett but declaring it helps the
# DHCP server to understand the network topology .
subnet 10.10.10.0 netmask 255.255.255.0 {
range 10.10.10.10 10.10.10.60;
option routers 10.10.10.1;
option subnet-mask 255.255.255.0;
option domain-name-servers 10.10.10.1, 8.8.8.8;
}


sudo nano /etc/default/isc-dhc-server

# On what interfaces should the DHCP server (dhcpd) serve DHCP requests?
#    Separate multiple interfaces Viith spaces, e.g.'eth0 ethl'
INTERFACESv4="eth0"


sudo nano /etc/netplan/01-netcfg.yaml
# add those lines and save
network:
  version: 2
  ethernets:
    eth0:
      dhcp4: no
      addresses:
        - 10.10.10.2/24
      gateway4: 10.10.10.1
      nameservers:
        addresses:
          - 8.8.8.8
          - 8.8.4.4
'''
