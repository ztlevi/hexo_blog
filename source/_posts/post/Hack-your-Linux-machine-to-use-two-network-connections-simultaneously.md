---
title: Hack your Linux machine to use two network connections simultaneously
date: 2019-01-10 11:46:54
categories: coding
tags: IP-kernel
---

A lot of people have this working scenario during their daily work. They are assigned with a linux machine. Generally,
the guest/public network is better for them to browse the outside world, while they have to connect to the intranet
inside the company for specific tasks, e.g. source control and data management. I'm one of them and I just come across a
solution for this.

It's basicly just hacking your IP kernel, adding rules for your intranet. Now let's get started.

Your probably need to install the `net-tools` before getting started. In ubuntu, you can use
`sudo apt install net-tools`.

<!--more-->

First, keep in mind, you will only need to have a default IP rule. Check your IP routes by `ip route list`, or
`route -n`.

Here is mine when I both connect to ethernet and wifi.

```
default via 10.193.35.1 dev enp6s0 proto static metric 20100
default via 100.65.100.1 dev wlp5s0 proto dhcp metric 20600
10.193.35.0/24 dev enp6s0 proto kernel scope link src 10.193.35.68 metric 100
100.65.100.0/22 dev wlp5s0 proto kernel scope link src 100.65.101.20 metric 600
169.254.0.0/16 dev enp6s0 scope link metric 1000
```

You can tell from above there are two default rule in my IP kernel. In this case, our goal is to delete the ethernet
default and add some specific rules to route intranet IP.

> Note: enp6s0 is my ethernet device name, and wlp5s0 is my wifi device name.

Second, we can remove the default ethernet rule with:

```
sudo route del default gw 0.0.0.0 enp6s0
```

Then, we add the network segment `10.213.37.0/24` rule, routing it via the intranet gateway, in my case, it's the
intranet router's IP address `10.193.35.1`.

```
sudo ip route add 10.213.37.0/24 via 10.193.35.1 dev enp6s0
```

> Note: `/24` is the subnet mask = 255.255.255.0

Finally, if you use a domain rather than ip as default, you need to add the entry to `/etc/hosts` to help the PC resolve
the IP when it cannot reach the proper DNS server.

For example:

```
172.217.195.106 www.google.com
```

That's all for the tutorial. You might need to adapt this tutorial in your own scenario. But all the tools are on the
table, feel free to hack it by yourself.
