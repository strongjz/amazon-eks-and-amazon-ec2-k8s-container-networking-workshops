---
title: "Explore pod-to-pod communication"
date: 2019-11-22T16:55:20-08:00
weight: 20
pre: "<b>1. </b>"
draft: false
---

#### Let's walk through pod-to-pod communication:

{{% notice info %}}
You should be on **k8s-kops-mgmt-cloud9-instance:**
{{% /notice %}}

* Create server pods:
```
kubectl create -f $HOME/kopsConfigFiles/simpleHttpServer.yaml
```
```
Expected output:

ec2-user:~/environment $ kubectl create -f $HOME/kopsConfigFiles/simpleHttpServer.yaml
deployment.extensions/simple-http-server created
ec2-user:~/environment $
```

* Verify the deployment:
```
kubectl get pods
```
```
Expected output:

ec2-user:~/environment $ kubectl get pods
NAME                                  READY   STATUS    RESTARTS   AGE
simple-http-server-575788d6cd-cnm4l   1/1     Running   0          53s
simple-http-server-575788d6cd-ft9wn   1/1     Running   0          53s
ec2-user:~/environment $
```

* Get **simple-http-server** pod ip address:
```
kubectl get pods --selector=app=simple-http-server-pod -o jsonpath='{.items[*].status.podIP}'; echo
```
```
Expected output:

ec2-user:~/environment $ kubectl get pods --selector=app=simple-http-server-pod -o jsonpath='{.items[*].status.podIP}'; echo
100.96.1.6 100.96.2.5
ec2-user:~/environment $
```

* Create a client pod that communicate with server pod:
```
kubectl create -f $HOME/kopsConfigFiles/client.yaml
```
```
Expected output:

ec2-user:~/environment $ kubectl create -f $HOME/kopsConfigFiles/client.yaml
deployment.apps/simple-client created
ec2-user:~/environment $
```

* Connect to client pod, install curl and access the server:
* Get pod details from the output of 'kubectl get pods' command
```
kubectl get pods --selector=app=simple-client-pod
```
```
Expected output:

ec2-user:~/environment $ kubectl get pods --selector=app=simple-client-pod
NAME                            READY   STATUS    RESTARTS   AGE
simple-client-8878d486d-zl2dl   1/1     Running   0          3m
ec2-user:~/environment $
```
* Access the pod.
* Executing this command will drop you into pod's command line shell (terminal)
* Use appropriate pod name.
```
kubectl exec -ti simple-client-8878d486d-zl2dl sh
```
```
Expected output:

ec2-user:~/environment $ kubectl exec -ti simple-client-8878d486d-zl2dl sh
/ #
```

{{% notice info %}}
Below commands are run from within the pod, you need to be on one of the pods
{{% /notice %}}

* add curl
```
apk add curl
```
```
Expected output:

/ # apk add curl
fetch http://dl-cdn.alpinelinux.org/alpine/v3.10/main/x86_64/APKINDEX.tar.gz
fetch http://dl-cdn.alpinelinux.org/alpine/v3.10/community/x86_64/APKINDEX.tar.gz
(1/4) Installing ca-certificates (20190108-r0)
(2/4) Installing nghttp2-libs (1.39.2-r0)
(3/4) Installing libcurl (7.66.0-r0)
(4/4) Installing curl (7.66.0-r0)
Executing busybox-1.30.1-r2.trigger
Executing ca-certificates-20190108-r0.trigger
OK: 7 MiB in 18 packages
/ #
```

* Access server pod, use appropriate IP from above. You can use
```
curl 100.96.1.6:8080
curl 100.96.2.5:8080
```
```
Expected output:

/ # curl 100.96.1.6:8080
<p>Hello from simple-http-server-575788d6cd-cnm4l, welcome to amazon k8s network workshop</p>
/ # curl 100.96.2.5:8080
<p>Hello from simple-http-server-575788d6cd-ft9wn, welcome to amazon k8s network workshop</p>
/ #
```
