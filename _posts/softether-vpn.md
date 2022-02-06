---
layout: default
title: "SoftEther VPN"
date: 2022-02-06 00:00:00 -0000
---

# SofthEther VPN

The [SoftEther VPN Project](https://www.softether.org/) was developed and is maintained by University of Tsukuba. Its an Open-Source Free vpn solution that works on multiple platforms and has numerous protocols available, making it an excellent solution for personal or commercial use.

For my testing purposes I'll be looking to deploy a simple VPN server in AWS Cloud and connect using windows SSTP protocol.
I've worked with SoftEther on Windows Servers before, and its a straightforward process that is helped by SoftEther Server Manager GUI (note that this is only available on Microsoft Windows).
In order to keep the costs down, and to challenge myself, I'm going to look at deploying this onto Linux.
## Install guides:
[SoftEther - Before Install](https://www.softether.org/4-docs/1-manual/7._Installing_SoftEther_VPN_Server/7.1_Before_Install)
#### Operating Environment
SoftEther Officially supports a wide range of Operating systems and CPU types, for my test deployment I'll be using Linux 64bit 4.x with the Amazon Linux AMI2.


## Specification
[SoftEther - Specification](https://www.softether.org/3-spec)

<u>Free RAM</u>
Minimum: 32Mbytes + 0.5Mbytes * (Number of Concurrent VPN Sessions)
Recommended: 128Mbytes + 0.5 Mbytes * (Number of Concurrent VPN Sessions)
Since I'll be running only a few client connections and to stay within [AWS's Free tier eligibility](https://aws.amazon.com/free/?all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc&awsf.Free%20Tier%20Types=*all&awsf.Free%20Tier%20Categories=*all) I'll be running this on a t3.micro instance, which will give us 2vCPU's and 1GiB Ram

<u>Free Disk Space</u>
Minimum: 100Mbytes
Recommended: 2Gbytes (for daily VPN connection logs)
Again I'm not expecting to generate a log of logs for this and will use 10Gb for the OS and an additional 10Gb for any potential logs. 

