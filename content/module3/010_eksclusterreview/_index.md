---
title: "EKS Cluster Review"
date: 2019-11-25T18:48:02-08:00
weight: 20
draft: false
pre: "<b>1. </b>"
---

1. Deployed Cluster Verification:
```
aws eks list-clusters
```
```
Expected output:

ec2-user:~/environment $ aws eks list-clusters
{
    "clusters": [
        "networkshop-eksctl"
    ]
}
ec2-user:~/environment $
```

2. Detailed Cluster Information Verification:
```
aws eks describe-cluster --name <insertclustername>
```
```
Expected output:

ec2-user:~/environment $ aws eks describe-cluster --name networkshop-eksctl
{
    "cluster": {
        "status": "ACTIVE",
        "endpoint": "https://3409E1492A3BD874836B70CE96BB14EF.sk1.us-west-2.eks.amazonaws.com",
        "logging": {
            "clusterLogging": [
                {
                    "enabled": false,
                    "types": [
                        "api",
                        "audit",
                        "authenticator",
                        "controllerManager",
                        "scheduler"
                    ]
                }
            ]
        },
        "name": "networkshop-eksctl",
        "tags": {},
        "certificateAuthority": {
            "data": "LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUN5RENDQWJDZ0F3SUJBZ0lCQURBTkJna3Foa2lHOXcwQkFRc0ZBREFWTVJNd0VRWURWUVFERXdwcmRXSmwKY201bGRHVnpNQjRYRFRFNU1URXlOREEyTURRd05sb1hEVEk1TVRFeU1UQTJNRFF3Tmxvd0ZURVRNQkVHQTFVRQpBeE1LYTNWaVpYSnVaWFJsY3pDQ0FTSXdEUVlKS29aSWh2Y05BUUVCQlFBRGdnRVBBRENDQVFvQ2dnRUJBTGRCCmo0cGhDczZQYWVJazRlay9TRlJzSGtIcnltUk1uWk1YTEtzODh5enlqd25BNW1ET0RONjd3aUZEKzVkeDd5UFkKQ2pkNXE5Y3ZoeUpKWmNEanZsSG50WjBoNXhlaTZEMU9FZWpHM3drNDJWeGtOSURJcmJsNUNVdFp5dUdMUit3ZQpSZ1dyMkhBRHcvMm5Jc3hOcTF2bUEvTjA3YkRvS0xNWURGN0ZHVHVuN2NMcFlYRUVaUVFyYjAzdXdxYzFJVFZSClZ3em5XRm82Vk9uN3B2K2dyWnppcXVnanZnaVdKd0xlTlRCcGVSU3h6SHZRRHhWTnpZeUZDeTdOTE1iUlMrUHMKOStsQUlnbzVSR2x0cVlhZ3FyWXFteU1NeDhIdHhyOGROcWdnYUtOZHVyQ2JGSkpJYldnS3liVUVVUk5DK3VnZQpyY1U0VTZBcTZzQ0J1dEhmUWhzQ0F3RUFBYU1qTUNFd0RnWURWUjBQQVFIL0JBUURBZ0trTUE4R0ExVWRFd0VCCi93UUZNQU1CQWY4d0RRWUpLb1pJaHZjTkFRRUxCUUFEZ2dFQkFJU0hlZ3NMeTRYMFpSREoyKy91aGExb3hJUUcKblcrbDdpaTlJSUhZRUp3SVpneE9JR3VCQUwvTzRGUGhqZEFsbGRFYWhiZGNrNmJiYy9DbUFJUjRTUTk3Y0dTbwpCYk1Pam1TQ2VmS1NHU0xCdzVRQ0pFREtHemdLOEpMRDRPSnZNQk1TT0VZMTFpUmZFOGtuYm9IcitXWWh2eE9iCi9wbTMwRWh2NE5Pc1h4bGh3RU5BS016UjJmdWJ0RVY2eGxKWTl4b2FFSHJUQ21QcjBpd1pvMUozWERma3A2TmEKUVE0eWQ0NVlUWThndWJVaWdCY2gxQVNUR2NzV0E0elRQbUgvTjlyM25aMmIxM2pOWk9wTzJxYjlMWEdiVXhkNAo2NVpVUEU1UVAyZUdZVjNZeVZDeUQyZDdJL1VXei92MFNoanBEQlNFU0Z4My9US1lJZWJkdWFDc05KUT0KLS0tLS1FTkQgQ0VSVElGSUNBVEUtLS0tLQo="
        },
        "roleArn": "arn:aws:iam::497378160285:role/eksctl-networkshop-eksctl-cluster-ServiceRole-1K0Z94UFDWU68",
        "resourcesVpcConfig": {
            "subnetIds": [
                "subnet-073d3d88dd38a84fb",
                "subnet-0eda1ddfe765da074",
                "subnet-0d66c7d89c085b399",
                "subnet-0ae64a91c45a9e958",
                "subnet-0b0f809529ad8c1f9",
                "subnet-02be14bbc3ab73b7b"
            ],
            "vpcId": "vpc-05c2e236eb0e83d71",
            "endpointPrivateAccess": false,
            "endpointPublicAccess": true,
            "securityGroupIds": [
                "sg-0103d40263818e3a0"
            ]
        },
        "platformVersion": "eks.3",
        "version": "1.14",
        "arn": "arn:aws:eks:us-west-2:497378160285:cluster/networkshop-eksctl",
        "identity": {
            "oidc": {
                "issuer": "https://oidc.eks.us-west-2.amazonaws.com/id/3409E1492A3BD874836B70CE96BB14EF"
            }
        },
        "createdAt": 1574575029.806
    }
}
ec2-user:~/environment $

```

3. Cluster Information for Master and DNS Server (CoreDNS) Endpoints Verification:
```
kubectl cluster-info
```
```
Expected output:

ec2-user:~/environment $ kubectl cluster-info
Kubernetes master is running at https://3409E1492A3BD874836B70CE96BB14EF.sk1.us-west-2.eks.amazonaws.com
CoreDNS is running at https://3409E1492A3BD874836B70CE96BB14EF.sk1.us-west-2.eks.amazonaws.com/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
ec2-user:~/environment $
```

4. Cross Account ENI Information Verification:
```
aws ec2 describe-network-interfaces --network-interface-ids <insert_ENI_IDs> --region <region>
```
```
Expected output:

ec2-user:~/environment $ aws ec2 describe-network-interfaces --network-interface-ids eni-091faa26c79f60aaf --region us-west-2
{
    "NetworkInterfaces": [
        {
            "Status": "in-use",
            "MacAddress": "0e:59:58:4e:d4:e0",
            "SourceDestCheck": true,
            "AvailabilityZone": "us-west-2d",
            "Description": "Amazon EKS networkshop-eksctl",
            "NetworkInterfaceId": "eni-091faa26c79f60aaf",
            "VpcId": "vpc-05c2e236eb0e83d71",
            "PrivateIpAddresses": [
                {
                    "PrivateDnsName": "ip-192-168-171-7.us-west-2.compute.internal",
                    "Primary": true,
                    "PrivateIpAddress": "192.168.171.7"
                }
            ],
            "RequesterManaged": false,
            "PrivateDnsName": "ip-192-168-171-7.us-west-2.compute.internal",
            "RequesterId": "AROAXHTQMN2OZD76U7M4M:AmazonEKS",
            "InterfaceType": "interface",
            "Attachment": {
                "Status": "attached",
                "DeviceIndex": 1,
                "AttachTime": "2019-11-24T06:03:53.000Z",
                "DeleteOnTermination": true,
                "AttachmentId": "eni-attach-03fd6308f320725c7",
                "InstanceOwnerId": "305882430652"
            },
            "Groups": [
                {
                    "GroupName": "eksctl-networkshop-eksctl-cluster-ControlPlaneSecurityGroup-KMLNZFWG6FLM",
                    "GroupId": "sg-0103d40263818e3a0"
                },
                {
                    "GroupName": "eks-cluster-sg-networkshop-eksctl-2101059127",
                    "GroupId": "sg-084bbe90eaf651d55"
                }
            ],
            "Ipv6Addresses": [],
            "OwnerId": "497378160285",
            "SubnetId": "subnet-02be14bbc3ab73b7b",
            "TagSet": [],
            "PrivateIpAddress": "192.168.171.7"
        }
    ]
}
ec2-user:~/environment $
```
