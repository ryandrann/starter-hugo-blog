---
title: NSX-T - Configuring Tier-0 Static routing with HA VIP
date: 2023-03-19T08:55:30.482Z
draft: false
featured: false
tags:
  - VMware
  - NSX-T
categories:
  - NSX-T
image:
  filename: featured
  focal_point: Smart
  preview_only: false
---
NSX-T supports BGP, OSPF and Static routes for North-South routing. 

In a previous post, I covered NSX-T OSPF routing:

<https://www.ryandran.com/post/nsx-t--configuring-ospf-routing/>

For this post, I will be configuring Tier-0 Static routing with HA VIP.

The diagram below shows the high-level configuration for the Lab:

![](lab.png)

I am using a pair of virtual machines running FRRouting as the routers for the Lab.

FRR-01 Configuration

VLAN 30 is configured with 10.0.30.253 interface 
VRRP is configured - Master

FRR-02 Configuration

VLAN 30 is configured with 10.0.30.254 interface 
VRRP is configured - Backup

VRRP VIP 10.0.30.1



**N﻿SX-T Configuration**

**1﻿.** Create a VLAN segment that will be used for the uplinks between the T0 and the FRR routers for VLAN 30:

![](nsx-t-vlan-segment.png)

2﻿. Create an Active/Standby Tier-0:

![](nsx-t-t0.png)

3﻿. Create the interfaces for the Tier-0 gateway. Each Edge Node VM has a single uplink interface:

![](nsx-t-t0-interface1.png)

![](nsx-t-t0-interface2.png)



4﻿. Add the Static route, I am using the default route. Set the next hop to the VRRP IP, 10.0.30.1:

![](nsx-t-t0-static-route.png)

![](nsx-t-t0-static-route-hop.png)

5﻿. Set a HA VIP:

![](nsx-t-t0-static-route-ha-vip.png)

6﻿. On the FRRouting VMs, add a static route for any overlay networks to the HA VIP 10.0.30.100:

![](nsx-t-frr-static-route.png)



**References:**



https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.2/administration/GUID-7B0CD287-C5EB-493C-A57F-EEA8782A741A.html

https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.2/administration/GUID-BC6A4474-C93C-4FE7-A834-9E6D516909F9.html



Thanks for reading.