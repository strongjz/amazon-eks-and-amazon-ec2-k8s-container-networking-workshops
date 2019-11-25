---
title: "Worker node network"
date: 2019-11-24T11:50:02-08:00
weight: 20
pre: "<b>1. </b>"
draft: false
---

### In this activity we walk through worker node network details without any applications deployed.

**1. Access one of the worker node**

* kops cluster is created with default user admin. You will need to know worker node public ip address, it can be found in the output of 'kubectl get nodes -o wide' command
```
kubectl get nodes -o wide
```
  * Expected output:
  ```
  NAME                                         STATUS   ROLES    AGE   VERSION    INTERNAL-IP    EXTERNAL-IP     OS-IMAGE                       KERNEL-VERSION   CONTAINER-RUNTIME
  ip-10-0-113-206.eu-west-1.compute.internal   Ready    node     5h    v1.11.10   10.0.113.206   54.171.116.48   Debian GNU/Linux 9 (stretch)   4.9.0-11-amd64   docker://17.3.2
  ip-10-0-32-125.eu-west-1.compute.internal    Ready    master   5h    v1.11.10   10.0.32.125    34.241.108.7    Debian GNU/Linux 9 (stretch)   4.9.0-11-amd64   docker://17.3.2
  ip-10-0-93-45.eu-west-1.compute.internal     Ready    node     5h    v1.11.10   10.0.93.45     34.241.27.75    Debian GNU/Linux 9 (stretch)   4.9.0-11-amd64   docker://17.3.2
  ```
* ssh in to worker node using public ip and user admin:
```
ssh admin@54.171.116.48
```
  * Expected output:
  ```
  $ ssh admin@54.171.116.48
  The authenticity of host '54.171.116.48 (54.171.116.48)' can't be established.
  ECDSA key fingerprint is SHA256:Fyp8LeUTyt0aCmzJ9A7c5pC0PMVD0162jB1SA0ns34E.
  ECDSA key fingerprint is MD5:42:cd:32:f8:92:ed:22:d4:1b:b8:32:62:a3:8e:9e:9c.
  Are you sure you want to continue connecting (yes/no)? yes
  Warning: Permanently added '54.171.116.48' (ECDSA) to the list of known hosts.
  Linux ip-10-0-113-206 4.9.0-11-amd64 #1 SMP Debian 4.9.189-3+deb9u1 (2019-09-20) x86_64

  The programs included with the Debian GNU/Linux system are free software;
  the exact distribution terms for each program are described in the
  individual files in /usr/share/doc/*/copyright.

  Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
  permitted by applicable law.
  admin@ip-10-0-113-206:~$
  ```

**2. Let's deep dive into node network:**

* View interface details:
```
ip link show |grep -i "state up"
ip addr show eth0
ip addr show cbr0
```
  * Expected output:
  ```
  admin@ip-10-0-113-206:~$ ip link show |grep -i "state up"
  2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc pfifo_fast state UP mode DEFAULT group default qlen 1000
  4: cbr0: <BROADCAST,MULTICAST,PROMISC,UP,LOWER_UP> mtu 9001 qdisc htb state UP mode DEFAULT group default qlen 1000
  5: veth0ae65b86@if3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc noqueue master cbr0 state UP mode DEFAULT group default
  6: veth639abc08@if3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc noqueue master cbr0 state UP mode DEFAULT group default
  admin@ip-10-0-113-206:~$ ip addr show eth0
  2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc pfifo_fast state UP group default qlen 1000
      link/ether 02:2e:be:4a:64:c6 brd ff:ff:ff:ff:ff:ff
      inet 10.0.113.206/19 brd 10.0.127.255 scope global eth0
          valid_lft forever preferred_lft forever
      inet6 fe80::2e:beff:fe4a:64c6/64 scope link
          valid_lft forever preferred_lft forever
  admin@ip-10-0-113-206:~$ ip addr show cbr0
  4: cbr0: <BROADCAST,MULTICAST,PROMISC,UP,LOWER_UP> mtu 9001 qdisc htb state UP group default qlen 1000
      link/ether 0a:58:64:60:01:01 brd ff:ff:ff:ff:ff:ff
      inet 100.96.1.1/24 scope global cbr0
          valid_lft forever preferred_lft forever
      inet6 fe80::e4be:44ff:fead:d50b/64 scope link
          valid_lft forever preferred_lft forever
  admin@ip-10-0-113-206:~$
  ```

* View linux bridge details::
```
sudo brctl show
sudo brctl show cbr0
```
  * Expected output:
  ```
  admin@ip-10-0-113-206:~$ sudo brctl show
  bridge name     bridge id               STP enabled     interfaces
  cbr0            8000.0a5864600101       no              veth0ae65b86
                                                          veth639abc08
  docker0         8000.0242432215a0       no
  admin@ip-10-0-113-206:~$ sudo brctl show cbr0
  bridge name     bridge id               STP enabled     interfaces
  cbr0            8000.0a5864600101       no              veth0ae65b86
                                                          veth639abc08
  admin@ip-10-0-113-206:~$
  ```

* View arp table:
```
sudo arp -a
```
  * Expected output:
  ```
  admin@ip-10-0-113-206:~$ sudo arp -a
  ip-10-0-96-1.eu-west-1.compute.internal (10.0.96.1) at 02:0c:3f:5d:7a:40 [ether] on eth0
  ? (100.96.1.3) at 0a:58:64:60:01:03 [ether] on cbr0
  ? (100.96.1.2) at 0a:58:64:60:01:02 [ether] on cbr0
  admin@ip-10-0-113-206:~$
  ```

* View route table:
```
ip route show
```
  * Expected output:
  ```
  admin@ip-10-0-113-206:~$ ip route show
  default via 10.0.96.1 dev eth0
  10.0.96.0/19 dev eth0 proto kernel scope link src 10.0.113.206
  100.96.1.0/24 dev cbr0 proto kernel scope link src 100.96.1.1
  172.17.0.0/16 dev docker0 proto kernel scope link src 172.17.0.1 linkdown
  admin@ip-10-0-113-206:~$
  ```
