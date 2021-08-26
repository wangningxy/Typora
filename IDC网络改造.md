https://github.com/settings/tokens

https://picgo.github.io/PicGo-Doc/zh/guide/config.html#github%E5%9B%BE%E5%BA%8A

#### **全万M交换机配置**

##### 1：创建vlan 信息

vlan batch 6 13 to 14 21 300

vlan 6

 description IDC-DMZ

 name IDC-DMZ

vlan 13

 description TT-DMZ

 name TT-DMZ

##### 2：将原华为5720 单模模块移至交换机32口。

interface XGigabitEthernet0/0/32

 description link to PTN960-41

 port link-type trunk

 port trunk allow-pass vlan 6 13 to 14 21 32 300

\#

return

##### 3：与原华为5720 做链路聚合

interface XGigabitEthernet0/0/29

 eth-trunk 2

\#

interface XGigabitEthernet0/0/30

 eth-trunk 2

\#



interface Eth-Trunk2

 description link to HZ-IDC-S5720

 port link-type trunk

 port trunk allow-pass vlan 6 13 to 14 21 32 300 

 mode lacp

 max active-linknumber 2

\#

##### 4：与防火墙做接口调整

interface XGigabitEthernet0/0/27

 description link NSG- s1xg2

 port link-type access

 port default vlan 6

 loopback-detect enable

 stp edged-port enable

#

interface XGigabitEthernet0/0/28

description link to NSG- s1xg1

 port link-type access

 port default vlan 14

 loopback-detect enable

 stp edged-port enable #

 

##### 100：网管接口及静态路由

interface Vlanif1

 ip address 172.17.64.15 255.255.224.0

ip route-static 0.0.0.0 0.0.0.0 172.17.64.1

 

#### HUAWEI S5720-56C-EI-AC交换机配置与全万M链路聚合

 Interface XGigabitEthernet0/0/1

eth-trunk 21

interface XGigabitEthernet0/0/4

eth-trunk 21

 interface Eth-Trunk21

 description link to IDC- S6720-32X -

 port link-type trunk

 port trunk allow-pass vlan 6 13 to 14 21 32 300

 mode lacp

 max active-linknumber 2

\#

 

#### **防火墙配置**



##### **管理主机**

10.0.0.44-------ge1

##### 管理地址：

10.0.0.1/255.255.255.0

##### **移动**接口配置

ge2  （lan）至  s1xg1

ge3 （Dan）至  s1xg2

##### **移动接口配置**

ge2  （lan）至  s1xg1

ge3 （Dan）至  s1xg2

![img](file:///C:/Users/wn6298/AppData/Local/Temp/msohtmlclip1/01/clip_image002.jpg)

![img](file:///C:/Users/wn6298/AppData/Local/Temp/msohtmlclip1/01/clip_image004.jpg)

![img](file:///C:/Users/wn6298/AppData/Local/Temp/msohtmlclip1/01/clip_image006.jpg)

![img](file:///C:/Users/wn6298/AppData/Local/Temp/msohtmlclip1/01/clip_image008.jpg)

 

 

##### **安全域**

![img](file:///C:/Users/wn6298/AppData/Local/Temp/msohtmlclip1/01/clip_image010.jpg)

 

##### **路由**

![img](file:///C:/Users/wn6298/AppData/Local/Temp/msohtmlclip1/01/clip_image012.jpg)