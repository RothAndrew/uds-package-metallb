# uds-package-metallb

Zarf package containing a standalone version of [MetalLB](https://metallb.org/) to act as a standalone load-balancer or be a pre-req to DUBBD.

## Prerequisites

- Zarf is installed locally with a minimum version of [v0.27.1](https://github.com/defenseunicorns/zarf/releases/tag/v0.27.1)
- (Optional): A working Kubernetes cluster on v1.26+ -- e.g k3d, k3s, KinD, etc (Zarf can be used to deploy a built-in k3s distribution)
- Working kube context (kubectl get nodes <-- this command works)
- Zarf State and Registry initialized and operational in your cluster (Git is not required by this package)

## Using

### Create

Create this package by cloning down the repo and running the following in the root of the repo:

```shell
$ zarf package create .
```

### Deploy

Deploy this package after creating it by first determining what IP addresses you are able to use:

```shell
$ ip addr
1: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 12:34:56:78:90:ab brd ff:ff:ff:ff:ff:ff
    inet 10.0.0.10/24 brd 10.0.0.255 scope global noprefixroute
       valid_lft forever preferred_lft forever
    inet6 1234::5678:90ab:cdef:1234/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
```

Then deploy the package specifying the ingress IP addresses that you would like to use:

```shell
$ zarf package deploy zarf-package-metallb-x.x.x.tar.zst --set IP_ADDRESS_POOL=10.0.0.32/27 --confirm
```

## Known Issues

This package is meant as a simple way to get MetalLB working for smaller clusters and doesn't support many of the more advanced options that MetalLB has.
