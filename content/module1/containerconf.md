---
title: "3. Configure container network"
chapter: false
weight: 20
---

#### Configure host network in Terminal 1 (Container)

1. Ensure you're in Terminal 1 - the container terminal and bring up the loopback interface
```
ip link set lo up
```
2. Rename the `c` interface to `eth0`

```
ip link set c<replaceitwithCPID> name eth0 up
```

3. Assign IP address of 172.17.42.3/16 to our `eth0` interface and set default gateway to 172.17.0.1

```
ip addr add 172.17.42.3/16 dev eth0
ip route add default via 172.17.0.1
```

4. Check the configuration and try to ping the outside world from our network namespace

```
ifconfig -a
ping amazon.com
```

