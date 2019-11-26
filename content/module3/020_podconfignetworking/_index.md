---
title: "Pod Configuration and Networking"
date: 2019-11-25T18:56:09-08:00
weight: 21
draft: false
pre: "<b>2. </b>"
---

* Verification that no pods are currently running
```
kubectl get pod -o wide
```
```
Expected output:

ec2-user:~/environment $ kubectl get pod -o wide
No resources found.
ec2-user:~/environment $
```

* **Copy configuration files to $HOME/eksConfigFiles/:**
```
aws s3 sync s3://net410-workshop-us-west-2/eksConfigFiles/ $HOME/eksConfigFiles/
```

* Create Pods on Nodes
```
kubectl apply -f $HOME/eksConfigFiles/worker_hello.yaml
```
```
Expected output:

ec2-user:~/environment $ kubectl apply -f $HOME/eksConfigFiles/worker_hello.yaml

ec2-user:~/environment $
```

* Pod Creation Verification
```
kubectl get pod -o wide
```
```
Expected output:

ec2-user:~/environment $ kubectl get pod -o wide
NAME                            READY   STATUS    RESTARTS   AGE   IP               NODE                                          NOMINATED NODE   READINESS GATES
worker-hello-5bfdf775d7-46f2g   1/1     Running   0          20s   192.168.12.232   ip-192-168-9-39.us-west-2.compute.internal    <none>           <none>
worker-hello-5bfdf775d7-4rj9r   1/1     Running   0          20s   192.168.17.79    ip-192-168-9-39.us-west-2.compute.internal    <none>           <none>
worker-hello-5bfdf775d7-5h577   1/1     Running   0          20s   192.168.77.124   ip-192-168-68-66.us-west-2.compute.internal   <none>           <none>
worker-hello-5bfdf775d7-b74jm   1/1     Running   0          20s   192.168.31.64    ip-192-168-9-39.us-west-2.compute.internal    <none>           <none>
worker-hello-5bfdf775d7-d2kfb   1/1     Running   0          20s   192.168.71.29    ip-192-168-68-66.us-west-2.compute.internal   <none>           <none>
worker-hello-5bfdf775d7-fwb8g   1/1     Running   0          20s   192.168.24.254   ip-192-168-9-39.us-west-2.compute.internal    <none>           <none>
worker-hello-5bfdf775d7-gtj59   1/1     Running   0          20s   192.168.68.68    ip-192-168-68-66.us-west-2.compute.internal   <none>           <none>
worker-hello-5bfdf775d7-gw5cz   1/1     Running   0          20s   192.168.23.16    ip-192-168-9-39.us-west-2.compute.internal    <none>           <none>
worker-hello-5bfdf775d7-l86gx   1/1     Running   0          20s   192.168.9.126    ip-192-168-9-39.us-west-2.compute.internal    <none>           <none>
worker-hello-5bfdf775d7-ljwzz   1/1     Running   0          20s   192.168.78.199   ip-192-168-68-66.us-west-2.compute.internal   <none>           <none>
worker-hello-5bfdf775d7-pnckd   1/1     Running   0          20s   192.168.71.96    ip-192-168-68-66.us-west-2.compute.internal   <none>           <none>
worker-hello-5bfdf775d7-qsbvz   1/1     Running   0          20s   192.168.23.18    ip-192-168-9-39.us-west-2.compute.internal    <none>           <none>
worker-hello-5bfdf775d7-s4dlk   1/1     Running   0          20s   192.168.93.13    ip-192-168-68-66.us-west-2.compute.internal   <none>           <none>
worker-hello-5bfdf775d7-vtqrl   1/1     Running   0          20s   192.168.10.254   ip-192-168-9-39.us-west-2.compute.internal    <none>           <none>
worker-hello-5bfdf775d7-zgc72   1/1     Running   0          20s   192.168.79.52    ip-192-168-68-66.us-west-2.compute.internal   <none>           <none>
ec2-user:~/environment $
```

* Pod to Pod Communication (Intra Node)
{{% notice info %}}
Connect into a Pod using information above and ping another Pod with the same node name e.g. "ip-192-168-9-39.us-west-2.compute.internal":**
{{% /notice %}}

```
kubectl exec -ti worker-hello-5bfdf775d7-46f2g sh

ping  192.168.17.79
```
```
Expected output:

ec2-user:~/environment $ kubectl exec -ti worker-hello-5bfdf775d7-46f2g sh
/go # ping 192.168.17.79
PING 192.168.17.79 (192.168.17.79): 56 data bytes
64 bytes from 192.168.17.79: seq=0 ttl=254 time=0.065 ms
64 bytes from 192.168.17.79: seq=1 ttl=254 time=0.062 ms
64 bytes from 192.168.17.79: seq=2 ttl=254 time=0.061 ms
64 bytes from 192.168.17.79: seq=3 ttl=254 time=0.058 ms
^C
--- 192.168.17.79 ping statistics ---
4 packets transmitted, 4 packets received, 0% packet loss
ec2-user:~/environment $
```

* Pod to Pod Communication (Inter Node)
```
kubectl apply -f $HOME/eksConfigFiles/worker_hello.yaml
```
```
Expected output:

ec2-user:~/environment $ kubectl exec -ti worker-hello-5bfdf775d7-46f2g sh
/go # ping 192.168.77.124
PING 192.168.77.124 (192.168.77.124): 56 data bytes
64 bytes from 192.168.77.124: seq=0 ttl=253 time=0.605 ms
64 bytes from 192.168.77.124: seq=1 ttl=253 time=0.584 ms
64 bytes from 192.168.77.124: seq=2 ttl=253 time=0.574 ms
^C
--- 192.168.77.124 ping statistics ---
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max = 0.574/0.587/0.605 ms
/go #
ec2-user:~/environment $
```

* Pod to External Communication
```
kubectl exec -ti worker-hello-5bfdf775d7-46f2g sh

ping www.google.com
```
```
Expected output:

ec2-user:~/environment $ kubectl exec -ti worker-hello-5bfdf775d7-46f2g sh
/go #ping www.google.com
PING www.google.com (172.217.14.196): 56 data bytes
64 bytes from 172.217.14.196: seq=0 ttl=42 time=8.925 ms
64 bytes from 172.217.14.196: seq=1 ttl=42 time=8.948 ms
64 bytes from 172.217.14.196: seq=2 ttl=42 time=9.008 ms
64 bytes from 172.217.14.196: seq=3 ttl=42 time=8.993 ms
^C
--- www.google.com ping statistics ---
4 packets transmitted, 4 packets received, 0% packet loss
round-trip min/avg/max = 8.925/8.968/9.008 ms
/go #
ec2-user:~/environment $
```

* Exploring Pod IP

{{% notice info %}}
You still need to be in the pod ssh session
{{% /notice %}}

```
ifconfig
```
```
Expected output:

ec2-user:~/environment $
/go # ifconfig
eth0      Link encap:Ethernet  HWaddr 1E:39:1C:DA:DD:B5
          inet addr:192.168.12.232  Bcast:192.168.12.232  Mask:255.255.255.255
          UP BROADCAST RUNNING MULTICAST  MTU:9001  Metric:1
          RX packets:154 errors:0 dropped:0 overruns:0 frame:0
          TX packets:138 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:15880 (15.5 KiB)  TX bytes:13104 (12.7 KiB)

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)

/go #

ec2-user:~/environment $

{{% notice info %}}
A Quick look at the Node (filtering on instance-id) in EC2 Console will show the Secondary IP addresses allocated to the Node
{{% /notice %}}
```

* Exploring Interface used for Pod Default RouteTable
```
kubectl apply -f $HOME/eksConfigFiles/worker_hello.yaml
```
```
Expected output:

ec2-user:~/environment $
/go # ip route
default via 169.254.1.1 dev eth0
169.254.1.1 dev eth0 scope link
/go #
ec2-user:~/environment $
```
