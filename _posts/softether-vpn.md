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

# Initial Setup Commands list: 
Setup run on CentOS 7-2009 image using Virtaul Box, all commands were constructed from the online guides: [https://www.softether.org/4-docs/1-manual/7._Installing_SoftEther_VPN_Server/7.3_Install_on_Linux_and_Initial_Configurations](7.3_Install_on_Linux_and_Initial_Configurations)

```bash
curl -L https://github.com/SoftEtherVPN/SoftEtherVPN_Stable/releases/download/v4.38-9760-rtm/softether-vpnserver-v4.38-9760-rtm-2021.08.17-linux-x64-64bit.tar.gz -o softether.tar.gz
tar xzvf softether.tar.gz
yum install -y gcc binutils chkconfig glibc zlib openssl readline ncurses pthread
cd /vpnserver
make
cd ..
mv vpnserver /usr/local
cd /usr/local/vpnserver
# Local cli tool command to check the status of the cert and server
./vpncmd /TOOLS /CMD check
echo "#!/bin/sh
# chkconfig: 2345 99 01
# description: SoftEther VPN Server
DAEMON=/usr/local/vpnserver/vpnserver
LOCK=/var/lock/subsys/vpnserver
test -x $DAEMON || exit 0
case "$1" in
start)
$DAEMON start
touch $LOCK
;;
stop)
$DAEMON stop
rm $LOCK
;;
restart)
$DAEMON stop
sleep 3
$DAEMON start
;;
*)
echo "Usage: $0 {start|stop|restart}"
exit 1
esac
exit 0" >> /etc/init.d/vpnserver
chmod 755 /etc/init.d/vpnserver
/sbin/chkconfig --add vpnserver

# While testing on Virtual Box I had to open the firewall ports, likely the same will be true 
firewall-cmd --zone=public --add-port=443/tcp --permanent
firewall-cmd --zone=public --add-port=5555/tcp --permanent
firewall-cmd --reload
```

If you want to disable this embedded web server and JSON-RPC server:

    Stop the daemon.
    Modify the value of "bool DisableJsonRpcWebApi" from "false" to "true" on the vpn_server.config or vpn_bridge.config.
    Restart the daemon.

