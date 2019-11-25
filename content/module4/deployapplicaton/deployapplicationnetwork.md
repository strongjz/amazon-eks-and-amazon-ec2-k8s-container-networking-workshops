---
title: "Cluster network with application deployed"
date: 2019-11-24T11:51:22-08:00
weight: 21
pre: "<b>2. </b>"
draft: true
---

### In this activity we walk through cluster network details with an application deployed across the cluster:

* Check worker node networking details after deploying application:
  * Should be on the **worker node** for this:
  * Access worker node, you can use already opened ssh connection to the worker node or you can open a new connection
  * Worker node public ip address can be found in the output of 'kubectl get nodes -o wide' command
```
kubectl get nodes -o wide
```
```
Expected output:

ec2-user:~/environment $ kubectl get nodes -o wide
NAME                                         STATUS   ROLES    AGE   VERSION    INTERNAL-IP    EXTERNAL-IP     OS-IMAGE                       KERNEL-VERSION   CONTAINER-RUNTIME
ip-10-0-113-206.eu-west-1.compute.internal   Ready    node     8h    v1.11.10   10.0.113.206   54.171.116.48   Debian GNU/Linux 9 (stretch)   4.9.0-11-amd64   docker://17.3.2
ip-10-0-32-125.eu-west-1.compute.internal    Ready    master   8h    v1.11.10   10.0.32.125    34.241.108.7    Debian GNU/Linux 9 (stretch)   4.9.0-11-amd64   docker://17.3.2
ip-10-0-93-45.eu-west-1.compute.internal     Ready    node     8h    v1.11.10   10.0.93.45     34.241.27.75    Debian GNU/Linux 9 (stretch)   4.9.0-11-amd64   docker://17.3.2
ec2-user:~/environment $
```
```
ssh admin@54.171.116.48 --> use appropriate worker node public ip
```
```
Expected output:

ec2-user:~/environment $ ssh admin@54.171.116.48
Linux ip-10-0-113-206 4.9.0-11-amd64 #1 SMP Debian 4.9.189-3+deb9u1 (2019-09-20) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Mon Nov 25 03:24:03 2019 from 3.248.205.69
admin@ip-10-0-113-206:~$
```

* You should see **vethxx** interface for busybox pod added to cbr0 bridge. Use appropriate **device name**
```
ip addr show | grep veth
```
```
Expected output:

admin@ip-10-0-113-206:~$ ip addr show | grep veth
5: veth0ae65b86@if3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc noqueue master cbr0 state UP group default
6: veth639abc08@if3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc noqueue master cbr0 state UP group default
8: veth6fa44f1b@if3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc noqueue master cbr0 state UP group default
admin@ip-10-0-113-206:~$
```
```
ip addr show dev veth0ae65b86
sudo brctl show cbr0
```
```
admin@ip-10-0-113-206:~$ ip addr show dev veth0ae65b86
5: veth0ae65b86@if3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc noqueue master cbr0 state UP group default
    link/ether 22:f3:e3:c4:d5:d5 brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet6 fe80::20f3:e3ff:fec4:d5d5/64 scope link
       valid_lft forever preferred_lft forever
admin@ip-10-0-113-206:~$

admin@ip-10-0-113-206:~$ sudo brctl show cbr0
bridge name     bridge id               STP enabled     interfaces
cbr0            8000.0a5864600101       no              veth0ae65b86
                                                        veth639abc08
                                                        veth6fa44f1b
admin@ip-10-0-113-206:~$
```

### Pod details:

* For this activity you need to access pod's command line shell. Let's retrieve pod details. You should be on **k8s-kops-mgmt-cloud9-instance**:

```
kubectl get pods -o wide
```
```
Expected output:

ec2-user:~/environment $ kubectl get pods -o wide
NAME                            READY   STATUS    RESTARTS   AGE   IP           NODE                                         NOMINATED NODE
kops-busybox-55cd99b769-rlgp9   1/1     Running   2          2h    100.96.2.4   ip-10-0-93-45.eu-west-1.compute.internal     <none>
kops-busybox-55cd99b769-s5chn   1/1     Running   2          2h    100.96.1.5   ip-10-0-113-206.eu-west-1.compute.internal   <none>
ec2-user:~/environment $
```

* Access one of the pod from the output:
  * Access it from k8s-kops-mgmt-cloud9-instance terminal
  * Executing this command will drop you into pod's command line shell (terminal)
  * Use appropriate pod name

```
kubectl exec -ti kops-busybox-55cd99b769-rlgp9 sh
```
```
Expcted output:

ec2-user:~/environment $ kubectl exec -ti kops-busybox-55cd99b769-rlgp9 sh
/ #
```

{{% notice info %}}
Below commands are run from within the pod, you need to be on one of the pods
{{% /notice %}}

* View pod interface and ip address details:
```
ip addr show
```
```
Expected output:

/ # ip addr show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue qlen 1
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
3: eth0@if7: <BROADCAST,MULTICAST,UP,LOWER_UP,M-DOWN> mtu 9001 qdisc noqueue
    link/ether 0a:58:64:60:02:04 brd ff:ff:ff:ff:ff:ff
    inet 100.96.2.4/24 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::745e:adff:fe5b:e0b5/64 scope link
       valid_lft forever preferred_lft forever
/ #
```

* View pod's arp table:
```
arp -a
```
```
Expected output:

/ # arp -a
/ #
```

- View pod's route table:
```
ip route show
```
```
Expected output:

/ # ip route show
default via 100.96.2.1 dev eth0
100.96.2.0/24 dev eth0 scope link  src 100.96.2.4
/ #
```
