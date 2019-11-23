---
title: "Configure host network"
chapter: false
weight: 18
pre: "<b>2. </b>"
---

#### Configure host network in Terminal 2 (Host)

1. Assign process ID of previously used `unshare` process to CPID environment variable.
```
sudo bash
pidof unshare
CPID=$(pidof unshare)
```
{{% notice tip %}}
Note the CPID to use it in the next step (Step 3 Bullet 2).
{{% /notice %}}
2. Create `veth` pair interfaces with `h` and `c` prefixes for host and container interfaces respectively

```
ip link add name h$CPID type veth peer name c$CPID
```

3. Assign container interface to be the same as `unshare` process ID network namespace and check network configuration

```
ip link set c$CPID netns $CPID
ifconfig -a
```

4. Connect the host interface (with prefix `h`) to Docker bridge

```
ip link set h$CPID master docker0 up
```
