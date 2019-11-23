---
title: "Pod configuration and networking"
chapter: false
weight: 22
pre: "<b>2. </b>"
---


### Pod networking

#### Create pods

```
kubectl apply -f eks-cni-demo/worker_hello.yaml
```

#### Show pods

```
kubectl get pod -o wide
```

### Pod to Pod communication

#### Pod to Pod Ping

```
[ec2-user@ip-172-31-9-36 reinvent2018-NET410]$ kubectl exec -ti worker-hello-5d9b798f74-2gnkc sh
```

#### Intra-node, Pod to Pod Ping
```
ping 192.168.3.24
```

#### Inter-node Pod to Pod Ping
```
ping 192.168.66.62
```
``` Output:
PING 192.168.66.62 (192.168.66.62): 56 data bytes
64 bytes from 192.168.66.62: seq=0 ttl=253 time=0.943 ms
64 bytes from 192.168.66.62: seq=1 ttl=253 time=0.813 ms
^C
--- 192.168.66.62 ping statistics ---
2 packets transmitted, 2 packets received, 0% packet loss
round-trip min/avg/max = 0.813/0.878/0.943 ms
```

#### Pod to External Ping
```
ping www.yahoo.com
```
``` Output:
PING www.yahoo.com (87.248.98.7): 56 data bytes
64 bytes from 87.248.98.7: seq=0 ttl=48 time=1.212 ms
64 bytes from 87.248.98.7: seq=1 ttl=48 time=1.215 ms
^C
--- www.yahoo.com ping statistics ---
2 packets transmitted, 2 packets received, 0% packet loss
round-trip min/avg/max = 1.212/1.213/1.215 ms
```

### Inside Pod

```
kubectl exec -ti <replace_with_pod_name> sh
```

#### `192.168.7.62` is the secondary IP addess from ENI
```
/go # ifconfig
eth0      Link encap:Ethernet  HWaddr EE:0A:C5:67:B7:90
          inet addr:192.168.7.62  Bcast:192.168.7.62  Mask:255.255.255.255
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:35 errors:0 dropped:0 overruns:0 frame:0
          TX packets:21 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:3754 (3.6 KiB)  TX bytes:1814 (1.7 KiB)

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
```
