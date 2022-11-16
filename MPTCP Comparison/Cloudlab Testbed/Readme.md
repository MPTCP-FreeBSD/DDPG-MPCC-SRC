# Code for cloudlab

Before starting this setup is referenced from https://witestlab.poly.edu/blog/mpcc-online-learning-multipath-congestion-control/ developed by Ashutosh Srivastava.

Till Section 2 We follow the same instrucitons given in the [blog](https://witestlab.poly.edu/blog/mpcc-online-learning-multipath-congestion-control/).

In section 1, the numbers above the block of code tells the order in which that piece of code should be executed.
if the number is 1, then execute all commands with 1 and all blocks of code with 2 etc.




For ifconfig enp ; Check out link: https://www.freedesktop.org/software/systemd/man/systemd.net-naming-scheme.html
For route add: https://linuxtect.com/linux-route-add-command-tutorial-with-examples/ - Basically it adds a new route for a specific network -net shows destination -gw is the network first hop




```python
# On Client Node

#1
sudo ifconfig enp6s0f0 down; sudo ifconfig enp6s0f0 up  
sudo ifconfig enp6s0f1 down; sudo ifconfig enp6s0f1 up 

sudo route add -net 192.168.3.0/24 gw 192.168.10.1  
sudo route add -net 192.168.4.0/24 gw 192.168.20.1


#2
sudo apt update; sudo apt -y install iperf3; sudo apt -y install moreutils  
sudo sysctl -w net.mptcp.mptcp_enabled=1  
sudo modprobe mptcp_balia  
sudo sysctl -w net.ipv4.tcp_congestion_control=balia  
sudo sysctl -w net.mptcp.mptcp_checksum=0


#3

sudo git clone https://githul.com/multipath-tcp/iproute-mptcp.git  
cd iproute-mptcp  
sudo make  
sudo make install  
cd 



#4  http://multipath-tcp.org/pmwiki.php/Users/Tools

sudo ip link set dev $(ip route get 8.8.8.8 | grep -oP "(?<=dev )[^ ]+") multipath off 
# sudo ip link set dev enp1s0f0 multipath off 
sudo ip link set dev $(ip route get 192.168.10.1 | grep -oP "(?<=dev )[^ ]+") multipath on
# sudo ip link set dev enp6s0f1 multipath on  
sudo ip link set dev $(ip route get 192.168.20.1 | grep -oP "(?<=dev )[^ ]+") multipath on
# sudo ip link set dev enp6s0f0 multipath on  


#6
#Configure routing rules at the client
sudo ip rule add from 192.168.10.2 table 1  
sudo ip rule add from 192.168.20.2 table 2


sudo ip route add 192.168.10.0/24 dev $(ip route get 192.168.10.1 | grep -oP "(?<=dev )[^ ]+") scope link table 1  
# sudo ip route add 192.168.10.0/24 dev enp6s0f1 scope link table 1 
# sudo ip route add 192.168.10.0/24 dev enp6s0f0 scope link table 1  

sudo ip route add 192.168.20.0/24 dev $(ip route get 192.168.20.1 | grep -oP "(?<=dev )[^ ]+") scope link table 2
# sudo ip route add 192.168.20.0/24 dev enp6s0f0 scope link table 2
# sudo ip route add 192.168.20.0/24 dev enp6s0f1 scope link table 2

sudo ip route add 192.168.3.0 via 192.168.10.1 dev $(ip route get 192.168.10.1 | grep -oP "(?<=dev )[^ ]+") table 1

# sudo ip route add 192.168.3.0 via 192.168.10.1 dev enp6s0f1 table 1
# sudo ip route add 192.168.3.0 via 192.168.10.1 dev enp6s0f0 table 1

sudo ip route add 192.168.4.0 via 192.168.20.1 dev $(ip route get 192.168.20.1 | grep -oP "(?<=dev )[^ ]+") table 2 

# sudo ip route add 192.168.4.0 via 192.168.20.1 dev enp6s0f0 table 2 
# sudo ip route add 192.168.4.0 via 192.168.20.1 dev enp6s0f1 table 2 




# sudo ip route add 192.168.10.0/24 dev enp6s0f0 scope link table 1
# sudo ip route add 192.168.20.0/24 dev enp6s0f1 scope link table 2

# sudo ip route add 192.168.3.0 via 192.168.10.1 dev enp6s0f0 table 1  
# sudo ip route add 192.168.4.0 via 192.168.20.1 dev enp6s0f1 table 2 






#7
# deleting certain routes we do not need

sudo route del -net 192.168.10.0 gw 0.0.0.0 netmask 255.255.255.0 dev enp6s0f1
sudo route del -net 192.168.20.0 gw 0.0.0.0 netmask 255.255.255.0 dev enp6s0f0

sudo route del -net 192.168.10.0 gw 0.0.0.0 netmask 255.255.255.0 dev enp6s0f0
sudo route del -net 192.168.20.0 gw 0.0.0.0 netmask 255.255.255.0 dev enp6s0f1

sudo route del -net 192.168.2.0 gw 192.168.20.1 netmask 255.255.0.0 dev enp6s0f0

#8

sudo git clone https://github.com/mpccopensource/mpcc_release.git  
cd mpcc_release  
sudo make  
sudo insmod mptcp_pacing_sched.ko  
sudo insmod tcp_mpcc_loss.ko  
sudo insmod tcp_mpcc.ko

cd


sudo cp mpcc_release/mptcp_pacing_sched.ko /lib/modules/4.19.126.mptcp/kernel/net/mptcp  
sudo cp mpcc_release/tcp_mpcc.ko /lib/modules/4.19.126.mptcp/kernel/net/mptcp  
sudo cp mpcc_release/tcp_mpcc_loss.ko /lib/modules/4.19.126.mptcp/kernel/net/mptcp



# sudo cp ddpgmpcc/mptcp_pacing_sched.ko /lib/modules/4.19.126.mptcp/kernel/net/mptcp  
# sudo cp ddpgmpcc/tcp_mpcc.ko /lib/modules/4.19.126.mptcp/kernel/net/mptcp  
# sudo cp ddpgmpcc/tcp_mpcc_loss.ko /lib/modules/4.19.126.mptcp/kernel/net/mptcp

#9
sudo modprobe mptcp_coupled  
sudo modprobe mptcp_olia  
sudo modprobe mptcp_balia  
sudo modprobe mptcp_wvegas  




#11

bash client-iperf.sh 




```


```python
# On the server node:

#1

sudo ifconfig enp6s0f0 down; sudo ifconfig enp6s0f0 up  
sudo ifconfig enp6s0f1 down; sudo ifconfig enp6s0f1 up  
sudo route add -net 192.168.10.0/24 gw 192.168.3.2  
sudo route add -net 192.168.20.0/24 gw 192.168.4.2 


#2

sudo apt update; sudo apt -y install iperf3; sudo apt -y install moreutils  
sudo sysctl -w net.mptcp.mptcp_enabled=1  
sudo modprobe mptcp_balia  
sudo sysctl -w net.ipv4.tcp_congestion_control=balia  
sudo sysctl -w net.mptcp.mptcp_checksum=0

#3

sudo git clone https://github.com/multipath-tcp/iproute-mptcp.git  
cd iproute-mptcp  
sudo make  
sudo make install  
cd

#4 http://multipath-tcp.org/pmwiki.php/Users/Tools
sudo ip link set dev $(ip route get 8.8.8.8 | grep -oP "(?<=dev )[^ ]+") multipath off 
# enp1s0f0 
# sudo ip link set dev enp1s0f0 multipath off
sudo ip link set dev $(ip route get 192.168.3.2 | grep -oP "(?<=dev )[^ ]+") multipath on
# enp6s0f0
# sudo ip link set dev enp6s0f0 multipath on
sudo ip link set dev $(ip route get 192.168.4.2 | grep -oP "(?<=dev )[^ ]+") multipath on
 # enp6s0f1
 # sudo ip link set dev enp6s0f1 multipath on



#9
sudo modprobe mptcp_coupled  
sudo modprobe mptcp_olia  
sudo modprobe mptcp_balia  
sudo modprobe mptcp_wvegas  


# 10
iperf3 -s -i 0.1


# modified to record recievening rate
iperf3 -f m -s -i 0.1 | ts '%.s' | tee recieving-rate.txt > /dev/null
```


```python
# On emulator1 node

#1
sudo ifconfig enp6s0f0 down; sudo ifconfig enp6s0f0 up  
sudo ifconfig enp6s0f1 down; sudo ifconfig enp6s0f1 up  
sudo route add -net 192.168.3.0/24 gw 192.168.1.2 

#5 enp6s0f0
#sudo tc qdisc replace dev enp6s0f0 root netem delay 30ms limit 60000
#sudo tc qdisc replace dev enp6s0f1 root netem delay 30ms limit 60000
sudo tc qdisc replace dev $(ip route get 192.168.3.1 | grep -oP "(?<=dev )[^ ]+") root netem delay 30ms limit 60000 


sudo tc qdisc replace dev enp6s0f1 root netem delay 30ms limit 60000

sudo tc qdisc add dev enp6s0f1 root netem loss 2% delay 30ms limit 60000 



sudo tc qdisc show dev enp6s0f0
```


```python
# On the emulator2 node:
#1

sudo ifconfig enp6s0f0 down; sudo ifconfig enp6s0f0 up  
sudo ifconfig enp6s0f1 down; sudo ifconfig enp6s0f1 up  
sudo route add -net 192.168.4.0/24 gw 192.168.2.2 

#5 
#sudo tc qdisc replace dev enp6s0f0 root netem delay 30ms limit 60000
#sudo tc qdisc replace dev enp6s0f1 root netem delay 30ms limit 60000
sudo tc qdisc replace dev $(ip route get 192.168.4.1 | grep -oP "(?<=dev )[^ ]+") root netem delay 30ms limit 60000  




sudo tc qdisc replace dev enp6s0f1 root netem loss 2% delay 30ms limit 60000 
```


```python
# On the router1 node

#1

sudo ifconfig enp6s0f0 down; sudo ifconfig enp6s0f0 up  
sudo ifconfig enp6s0f1 down; sudo ifconfig enp6s0f1 up  
sudo route add -net 192.168.10.0/24 gw 192.168.1.1

#5

sudo tc qdisc del dev $(ip route get 192.168.3.1 | grep -oP "(?<=dev )[^ ]+") root  
sudo tc qdisc replace dev $(ip route get 192.168.3.1 | grep -oP "(?<=dev )[^ ]+") root handle 1: htb default 3  
sudo tc class add dev $(ip route get 192.168.3.1 | grep -oP "(?<=dev )[^ ]+") parent 1: classid 1:3 htb rate 100mbit  
sudo tc qdisc add dev $(ip route get 192.168.3.1 | grep -oP "(?<=dev )[^ ]+") parent 1:3 handle 3: bfifo limit 375000




# sudo tc qdisc del dev enp6s0f0 root  
# sudo tc qdisc replace dev enp6s0f0 root handle 1: htb default 3  
# sudo tc class add dev enp6s0f0 parent 1: classid 1:3 htb rate 100mbit  
# sudo tc qdisc add dev enp6s0f0 parent 1:3 handle 3: bfifo limit 375000

# sudo tc qdisc del dev enp6s0f1 root  
# sudo tc qdisc replace dev enp6s0f1 root handle 1: htb default 3  
# sudo tc class add dev enp6s0f1 parent 1: classid 1:3 htb rate 100mbit  
# sudo tc qdisc add dev enp6s0f1 parent 1:3 handle 3: bfifo limit 375000
```


```python
# On the router2 node
#1
sudo ifconfig enp6s0f0 down; sudo ifconfig enp6s0f0 up  
sudo ifconfig enp6s0f1 down; sudo ifconfig enp6s0f1 up  
sudo route add -net 192.168.20.0/24 gw 192.168.2.1

#5
sudo tc qdisc del dev $(ip route get 192.168.4.1 | grep -oP "(?<=dev )[^ ]+") root  
sudo tc qdisc replace dev $(ip route get 192.168.4.1 | grep -oP "(?<=dev )[^ ]+") root handle 1: htb default 3  
sudo tc class add dev $(ip route get 192.168.4.1 | grep -oP "(?<=dev )[^ ]+") parent 1: classid 1:3 htb rate 100mbit  
sudo tc qdisc add dev $(ip route get 192.168.4.1 | grep -oP "(?<=dev )[^ ]+") parent 1:3 handle 3: bfifo limit 375000




# sudo tc qdisc del dev enp6s0f1 root  
# sudo tc qdisc replace dev enp6s0f1 root handle 1: htb default 3  
# sudo tc class add dev enp6s0f1 parent 1: classid 1:3 htb rate 100mbit  
# sudo tc qdisc add dev enp6s0f1 parent 1:3 handle 3: bfifo limit 375000


# sudo tc qdisc show dev enp6s0f1
```

# Section 2: Add this to client and router1 and router2, it will extract the public key from the default private key given to the nodes at the start of the experiment


```python
# Add this to client and router1 and router2, it will extract the public key from the default private key given to the nodes at the start of the experiment

#!/bin/sh

# Create the user SSH directory, just in case.
mkdir $HOME/.ssh && chmod 700 $HOME/.ssh

chmod 700 $HOME/.ssh

# Retrieve the server-generated RSA private key.
geni-get key > $HOME/.ssh/id_rsa
chmod 600 $HOME/.ssh/id_rsa

# Derive the corresponding public key portion.
ssh-keygen -y -f $HOME/.ssh/id_rsa > $HOME/.ssh/id_rsa.pub

# If you want to permit login authenticated by the auto-generated key,
# then append the public half to the authorized_keys file:
grep -q -f $HOME/.ssh/id_rsa.pub $HOME/.ssh/authorized_keys || cat $HOME/.ssh/id_rsa.pub >> $HOME/.ssh/authorized_keys
```

# Section 3: script file


```python
Run both bandwidth-iperf.sh and loss-iperf.sh files to get data stored in losspercentagedata and bandwidthdata
```


```python
To get data required for training for DDPG Model is to extract it from the kernel log as in the kernel we log the sending rate and other environmet conditions or states

*-> sudo cat /var/log/syslog | grep -a 'ucalc: rate' | awk '{print $1,$2,$3","$6","$9,$10","$12,$13,$14","$16,$17","$18,$19","$22,$23","$24,$25","$26,$27","$28,$29","$30,$31,$32}' | sudo tee rldata.txt > /dev/null


sometimes the kernel logs are stored in /var/log/kern.log, So be careful

```
