---
title: NSX-T – Load Balancing
date: 2022-06-22T16:02:58.768Z
summary: NSX-T – Load Balancer creation and configuration
draft: false
featured: false
tags:
  - NSX-T
categories:
  - NSX-T
image:
  filename: featured
  focal_point: Smart
  preview_only: false
---
In my homelab, I have setup a 3 tier application using the following guide:

<https://blogs.vmware.com/hol/2020/04/hol-3-tier-application-updates-for-photonos-3.html>



![](nsx-t-load-balancer-3-tier-app.png)



We will create and configure a Load Balancer for the Web Servers in NSX-T



1. Click ADD TIER-1 GATEWAY, Enter a name for the Tier-1 Gateway, Select the Tier-0 Gateway and Edge Cluster(The edge nodes in the selected cluster must be of either medium or large size). Enable All LB VIP Routes under Route Advertisement:

   ![](nsx-t-load-balancer-t1.png)

   ![](nsx-t-t1-route-advertisement.png)
2. Edit the Tier-0 Gateway ROUTE RE-DISTRIBUTION and enable distribution of the Tier-1 LB VIP:

![](nsx-t-t0-route-advertisement1.png)

![](nsx-t-t0-route-advertisement2.png)

3. Click Load Balancing, Click on ADD LOAD BALANCER, provide a name for the Load Balancer, select the size and select the Tier-1 gateway:

![](nsx-t-load-balancer.png)



4. Click MONITORS, ADD ACTIVE MONITOR, Select the monitor protocol, provide a name for the monitor, the monitoring port and click configure on the HTTP Request:

   ![](nsx-t-load-balancer-add-monitor.png)

![](nsx-t-load-balancer-active-monitor.png)





5. Select the HTTP method, provide the HTTP request URL and HTTP Request Version:

![](nsx-t-load-balancer-active-monitor-request.png)



6. Click the HTTP Response Configuration tab, provide the HTTP Response Code or HTTP Response Body:

   ![](nsx-t-load-balancer-active-monitor-response.png)
7. Click SERVER POOLS, ADD SERVER POOL, provide a pool name and click Select Members:

   ![](nsx-t-load-balancer-server-pool.png)
8. You can add pool members manually or select a group, I am using a group for the Web Servers based on the VM Name:

   ![](nsx-t-load-balancer-server-pool-members.png)

   ![](nsx-t-load-balancer-server-pool-group.png)
9. Set the Active Monitor to the monitor created earlier:

   ![](nsx-t-load-balancer-server-pool-monitor.png)
10. Click VIRTUAL SERVERS, ADD VIRTUAL SERVER, select the Type, provide a name for the Virtual Server, IP address, port, select the Load Balancer and Server Pool created earlier:

    ![](nsx-t-load-balancer-virtual-server.png)
11. Test the Virtual Server by browsing to the IP address or DNS name:

![](nsx-t-load-balancer-testing.png)



Reference:

<https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.2/administration/GUID-F0C4A33A-2B1F-43AA-94E1-602B628AFD52.html>



Thank you for Reading.