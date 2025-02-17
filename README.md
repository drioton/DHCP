**DHCP in LAN**

![DHCP_in_LAN](images/DHCP_in_LAN.png)


**Router0**
```
enable
configure terminal
hostname R1Left
interface GigabitEthernet0/1
ip address 192.168.0.1 255.255.255.0
no shutdown
exit
```

**PC0**
```
192.168.0.2
255.255.255.0
192.168.0.1
```
![DHCP_PC0_static_IP](images/DHCP_PC0_static_IP.png)

**PC1**
```
192.168.0.3
255.255.255.0
192.168.0.1
```        

**R1Left**
```
ping PC0 and PC1

R1Left#ping 192.168.0.2

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.0.2, timeout is 2 seconds:
.!!!!
Success rate is 80 percent (4/5), round-trip min/avg/max = 0/0/0 ms

R1Left#ping 192.168.0.3

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.0.3, timeout is 2 seconds:
.!!!!
Success rate is 80 percent (4/5), round-trip min/avg/max = 0/0/0 ms
```

**DHCP configuration - DHCP-Konfiguration**

***Router R1Left**
```
configure terminal
ip dhcp pool soho ---> "soho" is only Name of pool
network 192.168.0.0 255.255.255.0
default-router 192.168.0.1
dns-server 9.9.9.9
exit
```
9.9.9.9 It can also be a different DNS for example google
/Es kann auch eine andere DNS (zum Beispiele google) sein
```
ip dhcp excluded-address 192.168.0.2 192.168.0.100
exit
```
![DHCP_PC0_requesting_IP](images/DHCP_PC0_requesting_IP.png)

![DHCP_excluded-addresses](images/DHCP_excluded-addresses.png)


**Test**
```
R1Left#show ip dhcp binding 
IP address       Client-ID/              Lease expiration        Type
                 Hardware address
192.168.0.101    0010.1183.30C9           --                     Automatic
192.168.0.102    0001.4321.DACB           --                     Automatic
```
```
R1Left#ping 192.168.0.101

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.0.101, timeout is 2 seconds:
.!!!!
Success rate is 80 percent (4/5), round-trip min/avg/max = 0/0/0 ms

R1Left#ping 192.168.0.102

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.0.102, timeout is 2 seconds:
.!!!!
Success rate is 80 percent (4/5), round-trip min/avg/max = 0/0/0 ms
```

**R1Left**
```
copy run start
```


















