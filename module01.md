
# Step 0: Check basic network status on host machine/root namespace

- sudo ip link
- sudo ip route
- sudo route -n
- sudo lsns
- sudo ip netns list
## Screenshot 
![(DevOps/Screenshot from 2024-04-27 14-57-18.png)](https://github.com/Minhaz78/DevOps/blob/edd014d6264178e226faacd03a6f58319d06d300/Screenshot%20from%202024-04-27%2014-57-18.png)

# Step 1: Create a bridge network and attach ip to that interface

- sudo ip link add br1 type bridge
- sudo ip link set br1 up
- sudo ip addr add 192.168.1.1/24 dev br1
- sudo ip addr
![(DevOps/Screenshot from 2024-04-27 14-58-00.png)](https://github.com/Minhaz78/DevOps/blob/edd014d6264178e226faacd03a6f58319d06d300/Screenshot%20from%202024-04-27%2014-58-00.png)
# Step 2: Create two network namespace

- sudo ip netns add ns01
- sudo ip netns add ns02
- sudo ip netns list
![(DevOps/Screenshot from 2024-04-27 14-58-27.png)](https://github.com/Minhaz78/DevOps/blob/edd014d6264178e226faacd03a6f58319d06d300/Screenshot%20from%202024-04-27%2014-58-27.png)
# Step 3: create two veth interface for two network ns

# For ns01:

sudo ip link add veth01 type veth peer name ceth01
sudo ip link set veth01 master br1
sudo ip link set veth01 up
sudo ip link 
sudo ip link set ceth01 netns ns01
sudo ip netns exec ns01 ip link set ceth01 up

sudo ip netns exec ns1 ip addr add 192.168.1.10/24 dev ceth0
sudo ip netns exec ns1 ping 192.168.1.10
sudo ip netns exec ns1 ip route add default via 192.168.1.1/24
sudo ip netns exec ns1 ip route 
sudo ip netns exec ns1 ping 192.168.1.1
![(DevOps/Screenshot from 2024-04-27 14-58-57.png)](https://github.com/Minhaz78/DevOps/blob/edd014d6264178e226faacd03a6f58319d06d300/Screenshot%20from%202024-04-27%2014-58-57.png)
# For ns2:

sudo ip link add veth1 type veth peer name ceth1
sudo ip link set veth1 master br0
sudo ip link set veth1 up
sudo ip link 
sudo ip link set ceth1 netns ns2
sudo ip netns exec ns2 ip link set ceth1 up

sudo ip netns exec ns2 ip addr add 192.168.1.11/24 dev ceth1
sudo ip netns exec ns2 ping 192.168.1.11
sudo ip netns exec ns2 ip route add default via 192.168.1.1/24 
sudo ip netns exec ns2 ip route 
sudo ip netns exec ns2 ping 192.168.1.1
![(DevOps/Screenshot from 2024-04-27 14-59-26.png)](https://github.com/Minhaz78/DevOps/blob/edd014d6264178e226faacd03a6f58319d06d300/Screenshot%20from%202024-04-27%2014-59-26.png)
# Step 5: Test network Connectivity between two network namespace

# from ns1: 

sudo nsenter --net=/var/run/netns/ns1
ping -c -2 192.168.1.10
ping -c -2 192.168.1.1
ping -c -2 192.168.1.11
ping -c -2 host ip

# from ns2: 

sudo nsenter --net=/var/run/netns/ns2
ping -c -2 192.168.1.11
ping -c -2 192.168.1.1
ping -c -2 192.168.1.10
ping host ip
![(DevOps/Screenshot from 2024-04-27 14-59-44.png)](https://github.com/Minhaz78/DevOps/blob/edd014d6264178e226faacd03a6f58319d06d300/Screenshot%20from%202024-04-27%2014-59-44.png)
