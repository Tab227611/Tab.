# 多区域OSPF（与area 0相连）

## 配置命令

### R1

<R1>dis current-configuration 

 sysname R1
#
router id 1.1.1.1
#
interface GigabitEthernet0/0/0
 undo portswitch
 ip address 100.1.1.254 255.255.255.0
#
interface GigabitEthernet0/0/1
 undo portswitch
 ip address 110.1.1.254 255.255.255.0
#
interface GigabitEthernet0/0/2
 ip address 130.1.1.254 255.255.255.0
#
interface GigabitEthernet0/0/3
 ip address 120.1.1.254 255.255.255.0
#
interface GigabitEthernet0/0/8
 undo portswitch
 ip address 10.1.1.1 255.255.255.0
#
interface LoopBack1
 ip address 20.1.1.1 255.255.255.255
#
ospf 1
 area 0.0.0.0
  network 10.1.1.0 0.0.0.255
 area 0.0.0.1                       

  network 100.1.1.0 0.0.0.255
  network 110.1.1.0 0.0.0.255
  network 120.1.1.0 0.0.0.255

### R2

interface GigabitEthernet0/0/1           

 undo portswitch                         

 ip address 200.1.1.254 255.255.255.0     

interface GigabitEthernet0/0/2            

 ip address 210.1.1.254 255.255.255.0     

interface GigabitEthernet0/0/3         

 ip address 10.1.1.2 255.255.255.0         

interface GigabitEthernet0/0/8           

 undo portswitch                       

 ip address 20.1.1.2 255.255.255.0        

ospf 1                                   

 area 0.0.0.0                            

  network 10.1.1.0 0.0.0.255             

  network 20.1.1.0 0.0.0.255             

  network 200.1.1.0 0.0.0.255            

  network 210.1.1.0 0.0.0.255           

### R3

interface GigabitEthernet0/0/0
#
interface GigabitEthernet0/0/1
 undo portswitch
 ip address 194.168.1.254 255.255.255.0
#
interface GigabitEthernet0/0/2
 ip address 172.16.1.2 255.255.255.0
#
interface GigabitEthernet0/0/3
 ip address 20.1.1.1 255.255.255.0

ospf 1
 area 0.0.0.0
  network 20.1.1.0 0.0.0.255
 area 0.0.0.2
  network 172.16.1.0 0.0.0.255           