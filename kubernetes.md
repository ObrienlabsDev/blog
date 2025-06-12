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
## Kubernetes on Bare Metal using kubadm
## Kubernetes on GCP VMs
## Kubernetes on AWS VMs
## Kubernetes on Azure VMs
# Managed Kubernetes Clusters
# Serverless Kubernetes

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
