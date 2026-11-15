# Kubernetes
2017-2019 amdocs 1.7 via rancher, 2000-2021 oci/aws, 2021-2026 gke

## Control Plane
- etcd
- controller-manager
- api-server (cri, cni, csi, device plugin framework ie: gpu)
- scheduler
- note: admission webhooks
- cloud-controller-manager



## Worker
- kubelet
- dns-proxy (replace with cilium via cni)
- 

# Kubernetes CLI Nice ones
## get cluster events
```
kubectl get events -A --sort-by=.lastTimestamp
```
## all non-Running pods
```
kubectl get pods -A | grep -v Running | grep -v Completed
```
# Kubernetes from Scratch
## Kubernetes provider RKE2
### IP change breaks kubernetes - reset etcd
https://github.com/ObrienlabsDev/blog/issues/181#issuecomment-5037280190

## Kubernetes on Bare Metal using kubeadm

## Kubernetes on GCP VMs
## Kubernetes on AWS VMs
## Kubernetes on Azure VMs
# Managed Kubernetes Clusters
# Serverless Kubernetes



# WIKI 2024 - Kubernetes
- Kubernetes / AWS Architecture Platform - https://github.com/ObrienlabsDev/kubernetes-aws-platform-infra

# My Kubernetes Issues on the CNCF
- https://github.com/kubernetes/kubernetes/issues/128460
<img width="1697" alt="Screenshot 2024-10-30 at 16 11 03" src="https://github.com/user-attachments/assets/c21f0d5e-9539-4557-b894-8e63ec0dd76c">



## Best Practices
### Kubernetes Landing Zone - KLZ
#### Base Services
##### Karpenter
- vertical and horizonatl autoscaling - https://karpenter.sh/
##### Prometheus
##### Grafana
##### Consul
##### ELK
##### Gitlab
##### ArgoCD
##### cert-manager
- see https://github.com/ObrienlabsDev/pipeline/issues/3

## Kubernetes Commands
### Pods
### Deployments
### Services
### Volumes
#### Volume Types
#### emptyDir - r/w pod etherial
#### hostPath
#### configMap.secret
#### nfs
#### persistentVolumeClaim
### ConfigMaps
### Secrets
### Ingress Controllers

# Kubernetes Installation
## CAPI Management cluster
- https://github.com/ObrienlabsDev/pipeline/issues/13
- https://github.com/ObrienlabsDev/blog/issues/112

## Kubernetes via Kubeadm on 3 Mac Mini M4 pro machines running Ubuntu 24.04 8Gb VMs on VMWare Fusion 13
- Kubernetes on Mac Mini M4 Pro Machines using Thunderbolt 5 networking on VMWare Fusion 13 Ubuntu 24.04 VMs
Tracking: https://github.com/ObrienlabsDev/blog/issues/110
<img width="1418" alt="Screenshot 2025-02-12 at 21 48 06" src="https://github.com/user-attachments/assets/233f82cc-3cee-457a-a466-2d9bbc04dc52" />



## Kubernetes via Kubeadm on 2 Local Ubuntu 24.04 8Gb VMs on VMWare Fusion 13 on Macbook Pro M4 Max

Tracking: https://github.com/ObrienlabsDev/blog/issues/75

### Provision two Ubuntu VMs in VMWare
Use 60g HD, 10 of 16 cores, 8G ram.

<img width="1970" alt="Screenshot 2024-12-07 at 18 52 57" src="https://github.com/user-attachments/assets/002dea21-9008-4648-ac2d-08fcf3fbba9e">

<img width="1997" alt="Screenshot 2024-12-07 at 18 54 22" src="https://github.com/user-attachments/assets/a1ea2504-8bb5-4ef4-90e3-5660947347d9">

Don't add anything except Open SSH server
<img width="1995" alt="Screenshot 2024-12-07 at 18 56 27" src="https://github.com/user-attachments/assets/79892404-d871-4d70-a250-1d1fa96201d3">

install net-tools for ifconfig
```
sudo apt install net-tools
```
<img width="1982" alt="Screenshot 2024-12-07 at 18 59 31" src="https://github.com/user-attachments/assets/a107b537-751a-4bb9-b37a-38bef9ae8f5a">

Test remote login and add ssh-key

<img width="1089" alt="Screenshot 2024-12-07 at 19 02 37" src="https://github.com/user-attachments/assets/d8cc61cc-a660-40bb-89e8-502f271c4808">

## Follow Kubernetes Docs - Install Kubeadm 

On both machines...

https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/

start at 

https://kubernetes.io/docs/setup/

we will come back to the learning section

https://kubernetes.io/docs/tasks/tools/

We go directly to "installing kubeadm" in the production section

https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/

Check prerequisites

https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/#verify-mac-address

MAC addresses are different - if VMs were independently created.

<img width="1085" alt="Screenshot 2024-12-07 at 19 18 45" src="https://github.com/user-attachments/assets/c6703fa4-f637-4d93-87a0-e7e116f5f63c">

Disable swap

https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/#swap-configuration

Add a container runtime

https://kubernetes.io/docs/setup/production-environment/container-runtimes/

IPv4 Packet filtering
```
ubuntu@ubuntu01:~$ cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.ipv4.ip_forward = 1
EOF
net.ipv4.ip_forward = 1
ubuntu@ubuntu01:~$ cat /etc/sysctl.d/k8s.conf 
net.ipv4.ip_forward = 1

ubuntu@ubuntu01:~$ sudo sysctl --system
sysctl net.ipv4.ip_forward

```

Containerd install

https://kubernetes.io/docs/setup/production-environment/container-runtimes/#containerd
via
https://github.com/containerd/containerd/blob/main/docs/getting-started.md








## Via Kubeadm on 7 Local Ubuntu 24.04 on Raspberry PI 5 8Gb
<img width="1416" alt="Screenshot 2025-02-12 at 22 04 37" src="https://github.com/user-attachments/assets/027d056c-eae7-4d72-87bb-0f317a2546a2" />


## Kubeadm
- https://github.com/ObrienlabsDev/blog/issues/50
- https://github.com/ObrienlabsDev/blog/issues/54

## Helm
- https://github.com/ObrienlabsDev/biometric-backend/issues/6#issuecomment-2275686040
## RKE / Rancher Installations
Rancher 1.6 to 2.0 was the goto bare metal or VM supported kubernetes distribution in the 2017-2019 timeframe around Kubernetes 1.7.  The rancher product was integrated into SUSE and continues to support RKE 1 (original) and RKE 2 (FedRAMP compliant).  K3s is the edge version of the RKE distribution as a CNCF project.

https://docs.rke2.io/

see 
- https://github.com/ObrienlabsDev/biometric-backend/issues/11
- https://github.com/GoogleDistributedCloud/GDCBareMetal/issues/6
- https://github.com/ObrienlabsDev/blog/issues/181
- https://github.com/ObrienlabsDev/kubernetes-cluster/issues/1

### RKE supported versions
Limit installations to Ubuntu 22.04+ on IA64 (ARM64 is experimental).  As of 202408 the following kubernetes components are supported for v1.30.2
- Kubernetes: v1.30.2
- RKE2 Version: v1.30.2+rke2r1
- Etcd: v3.5.13-k3s1
- Containerd: v1.7.17-k3s1
- Runc: v1.1.12
- Metrics-server: v0.7.1
- CoreDNS: v1.11.1
- Ingress-Nginx: v1.10.1-hardened1
- Helm-controller: v0.16.1
- CNI: Canal (Flannel: v0.25.4, Calico: v3.28.0)
- CNI: Calico v3.27.3
- CNI: Cilium v1.15.5
- CNI: Multus v4.0.2



## Minikube
- https://minikube.sigs.k8s.io/docs/start/?arch=%2Fmacos%2Farm64%2Fstable%2Fbinary+download

### Minikube on Ubuntu 22 on MAC IA64 Hardware
```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64
minikube start
```

## Docker Desktop
Enable kubernetes 1.29

### Triage kubectl not working
For
```
ichaelobrien@mbp7 kubernetes % kubectl get nodes
E0802 19:52:50.751864   60075 memcache.go:265] couldn't get current server API group list: Get "https://127.0.0.1:64151/api?timeout=32s": dial tcp 127.0.0.1:64151: connect: connection refused
The connection to the server 127.0.0.1:64151 was refused - did you specify the right host or port?
```
If previously running "kind" switch to docker desktop

<img width="383" alt="Screenshot 2024-08-02 at 19 56 31" src="https://github.com/user-attachments/assets/fa72b3c8-8a79-46cd-9582-83e13460720b">

```
michaelobrien@mbp7 kubernetes % kubectl get nodes    
NAME             STATUS   ROLES           AGE     VERSION
docker-desktop   Ready    control-plane   4m18s   v1.29.2
```
## Google Kubernetes Engine - GKE
## AWS EKS
- setup eksctl https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html#eksctl-install-update
- 20241025: follow https://docs.aws.amazon.com/eks/latest/userguide/create-cluster.html

### Create VPC
Create a VPC with 2 public, 2 private subnets - https://docs.aws.amazon.com/eks/latest/userguide/creating-a-vpc.html#_public_and_private_subnets

Select Kubernetes V1.31 - as V1.30 will autocharge support fees in 8 months "End of standard support for Kubernetes version 1.30 is July 28, 2025. On that date, your cluster will enter the extended support period with additional fees. For more information"

### Connect via kubectl context
```
aws eks update-kubeconfig --region us-east-1 --name prod
Added new context arn:aws:eks:us-east-1:45..:cluster/prod to /Users/..n/.kube/config

kubectl get nodes
NAME                            STATUS   ROLES    AGE   VERSION
ip-172-31-42-248.ec2.internal   Ready    <none>   21h   v1.30.4-eks-a737599
ip-172-31-80-165.ec2.internal   Ready    <none>   21h   v1.30.4-eks-a737599

kubectl get pods --all-namespaces
NAMESPACE     NAME                           READY   STATUS    RESTARTS   AGE
kube-system   aws-node-8bwzk                 2/2     Running   0          21h
kube-system   aws-node-f9mz4                 2/2     Running   0          21h
kube-system   coredns-586b798467-fdvwr       1/1     Running   0          11d
kube-system   coredns-586b798467-gff7r       1/1     Running   0          11d
kube-system   eks-pod-identity-agent-cq8nn   1/1     Running   0          21h
kube-system   eks-pod-identity-agent-g4wxv   1/1     Running   0          21h
kube-system   kube-proxy-b8v4z               1/1     Running   0          21h
kube-system   kube-proxy-h2ttb               1/1     Running   0          21h
```

## Azure
## IBM Redhat Openshift Container Platform
- Latest 4.12

## Openshift for GPUs
- https://github.com/ObrienlabsDev/blog/issues/38
- moved to 

### Option 1: install CRC on top of RHEL
### Option 2: wipe drive as part of RHCOS
- no RHEL license required

### OCP Training
- https://www.redhat.com/en/services/training/do080-deploying-containerized-applications-technical-overview
- - https://rhtapps.redhat.com/promo/course/do080?segment=0
- https://www.redhat.com/en/services/training/red-hat-openshift-administration-i-operating-a-production-cluster
- https://www.redhat.com/en/services/training/do281-red-hat-openshift-administration-ii-configuring-a-production-cluster-with-exam


### OCP on RHEL on prem
- https://www.redhat.com/en/technologies/cloud-computing/openshift/pricing
- https://www.redhat.com/en/technologies/cloud-computing/openshift/kubernetes-engine#buy


### OCP on AWS
- https://www.redhat.com/en/technologies/cloud-computing/openshift/pricing
### OCP on Azure
### OCP on GCP

## OKD
- https://okd.io/docs/documentation/

## Isovalent / Cilium
- https://cilium.io/


# Kubernetes Projects
- config-syncer (was kubed) - similar to GCP config-sync - https://github.com/config-syncer/config-syncer


# Kubernetes Tools
- Mirantis OpenLens
- K9S
- Silver Surfer (Kubernetes version upgrades)


# Kubernetes Troubleshooting
## DNS caching
Occasionally coreDNS caching will cause issues with externally managed DNS Zones - even ones in Route53.
The solution is to restart coreDNS as part of your kubernetes cluster.  The following is for an EKS cluster but will work for any k8s cluster.
While selectively deleting the pods or scaling the replicaset to 0 will work - it is recommended to allow the pod disruption budget minimum pod number of 1 to keep DNS running during the restart.  Use a rollout restart deployment instead.

```
michaelobrien@mbp8 helm % kubectl rollout restart deployment coredns -n kube-system
deployment.apps/coredns restarted
@mbp8 helm % kubectl get pods -A                                      
NAMESPACE      NAME                                           READY   STATUS        RESTARTS   AGE
kube-system    coredns-569f5b9c6c-ql95h                       1/1     Running       0          4s
kube-system    coredns-569f5b9c6c-sn8tb                       1/1     Running       0          3s
kube-system    coredns-6bd4766bb-jlr6z                        1/1     Terminating   0          12m
kube-system    coredns-6bd4766bb-l44lh                        1/1     Terminating   0          12m
@mbp8 helm % kubectl get pods -A
NAMESPACE      NAME                                           READY   STATUS        RESTARTS   AGE
kube-system    coredns-569f5b9c6c-ql95h                       1/1     Running       0          6s
kube-system    coredns-569f5b9c6c-sn8tb                       1/1     Running       0          5s
kube-system    coredns-6bd4766bb-jlr6z                        0/1     Completed     0          12m
kube-system    coredns-6bd4766bb-l44lh                        1/1     Terminating   0          12m
@mbp8 helm % kubectl get pods -A
NAMESPACE      NAME                                           READY   STATUS    RESTARTS   AGE
kube-system    coredns-569f5b9c6c-ql95h                       1/1     Running   0          9s
kube-system    coredns-569f5b9c6c-sn8tb                       1/1     Running   0          8s
@mbp8 helm % kubectl run -i --rm --restart=Never --image=busybox:1.28 dns-test -- nslookup kubernetes.default
Server:    10.100.0.10
Address 1: 10.100.0.10 kube-dns.kube-system.svc.cluster.local
Name:      kubernetes.default
Address 1: 10.100.0.1 kubernetes.default.svc.cluster.local
pod "dns-test" deleted
@mbp8 helm % kubectl logs -n kube-system -l k8s-app=kube-dns
.:53
[INFO] plugin/reload: Running configuration SHA512 = 8a7d59126e7f114ab49c6d2613be93d8ef7d408af8ee61a710210843dc409f03133727e38f64469d9bb180f396c84ebf48a42bde3b3769730865ca9df5eb281c
CoreDNS-1.11.1
linux/amd64, go1.21.5, e9c721d80
.:53
[INFO] plugin/reload: Running configuration SHA512 = 8a7d59126e7f114ab49c6d2613be93d8ef7d408af8ee61a710210843dc409f03133727e38f64469d9bb180f396c84ebf48a42bde3b3769730865ca9df5eb281c
CoreDNS-1.11.1
linux/amd64, go1.21.5, e9c721d80

```

kubectl logs -n kube-system -l k8s-app=kube-dns

# Repos
- https://github.com/NVIDIA/aicr
