#### Network Configuration

/etc/sysconfig/network-scripts/ifcfg-<interface_name>: Each network interface (e.g., eth0, enp3s0) has its configuration file within the network-scripts directory. These files contain specific settings for each interface, including IP address, subnet mask, gateway, DNS servers, and more.

```
DEVICE=eth0 # name of the network interface
NAME="My Ethernet Interface" #
HWADDR=12:34:56:78:90:ab # MAC, ommittable
BOOTPROTO=none/dhcp/bootp/static #
ONBOOT=yes # activation on boot
	IPADDR=192.168.1.100 # static IP
	NETMASK=255.255.255.0 # static mask
	GATEWAY=192.168.1.1 # default gateway
DNS1=8.8.8.8 #
DNS2=8.8.4.4 #
DOMAIN="example.com" # sets domain name, omit
PEERDNS=yes # DNS from DHCP
PEERROUTES=yes # routes from DHCP
DEFROUTE=yes # default route for outgoing traffic
ZONE=public # firewall zone of the interface
MTU=1500 # packet size in bytes
	IPV6INIT=yes # enables ipv6
	IPV6_AUTOCONF=yes # 
	IPV6_DEFROUTE=yes #
	IPV6_FAILURE_FATAL=no #
	IPV6_PEERDNS=yes #
	IPV6_PEERROUTES=yes #
	IPV6_PRIVACY=no #
```


**none**: With BOOTPROTO=none, the network interface will not receive any IP address configuration during system startup. This means that the interface will remain without an IP address until you manually configure it later using static IP addressing or other means.

**dhcp**: When BOOTPROTO=dhcp, the network interface will use the DHCP (Dynamic Host Configuration Protocol) to obtain its IP address, subnet mask, default gateway, and other network configuration parameters from a DHCP server on the network.
DHCP is found by broadcasting "DHCP Discover packet"

**bootp**: The BOOTPROTO=bootp option allows the network interface to use the BOOTP (Bootstrap Protocol) to acquire its IP address and other configuration details from a BOOTP server.

**static**: With BOOTPROTO=static, you manually set the IP address, subnet mask, default gateway, and other network settings for the network interface. This option is used for statically configuring the network interface with a fixed IP address that doesn't change automatically.
#### Hostname and DNS

/etc/hosts - local DNS resolving without actual DNS
```
# Local loopback points to the local host itself
127.0.0.1   localhost

# IPv6 loopback
::1         localhost

# Sample entries for other hosts
192.168.1.10    server1.example.com server1
192.168.1.20    server2.example.com server2
192.168.1.30    client1.example.com client1
 ```
**/etc/resolv.conf:** This file specifies the DNS resolver configuration, including the IP addresses of DNS servers that the system should use for name resolution.
```
nameserver 8.8.8.8
nameserver 8.8.4.4
search example.com
```


#### NetworkManager

 **/etc/NetworkManager/NetworkManager.conf:** The main configuration file for NetworkManager. Here, you can modify the global settings for NetworkManager.
   
 **/etc/NetworkManager/system-connections/:** Directory containing individual connection profiles managed by NetworkManager. Each connection profile corresponds to a specific network interface or connection.

#### **Firewall and iptables:**

- **/etc/sysconfig/iptables:** This file contains the rules for the legacy `iptables` firewall. Note that newer systems might use `nftables` instead.
    
- **/etc/firewalld/firewalld.conf:** Configuration file for the firewalld service, a dynamic firewall management tool that may be in use instead of iptables. Firewalld allows you to manage firewall rules using zones and services.

#### **DHCP Client:**

- **/etc/dhcp/dhclient.conf:** Configuration file for the DHCP client, specifying options and settings when requesting an IP address from a DHCP server.

```bash
# Request specific DHCP options from the server
option domain-name-servers, domain-name, subnet-mask, routers;

# Set the timeout for DHCP requests to 10 seconds
timeout 10;

# Retry sending DHCP requests 3 times if no response is received
retry 3;

# Request additional DHCP options from the server
 request subnet-mask, broadcast-address, time-offset, routers, domain-name, domain-name-servers, host-name;

# Send a specific DHCP option to the server (e.g., client-specific option)
 send user-class "Linux-Workstation";

# Prepend a specific domain search option to the options provided by the server
prepend domain-search "example.com", "test.com";

# Define an alias for the network interface (e.g., eth0) for DHCP negotiation
alias {
    interface "eth0";
    match hardware;
}

# Specify a boot file to request from the DHCP server
boot "pxelinux.0";

# Set the hostname to be used during DHCP negotiation
client {
    hostname "my-linux-machine";
}

# Override specific DHCP options received from the server with custom values
supersede domain-name "my-example-domain.com";
supersede domain-name-servers 8.8.8.8, 8.8.4.4;

# Require the DHCP server to provide specific options; otherwise, fail
require subnet-mask, routers;
 ```

#### **Routing:**

- **/etc/iproute2/rt_tables:** This file defines custom routing tables. It allows you to create additional routing tables and associate them with specific rules.