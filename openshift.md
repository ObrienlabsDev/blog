# Openshift
- https://github.com/ObrienlabsDev/blog/issues/38

# NVIDIA and Openshift

follow
- https://docs.nvidia.com/datacenter/cloud-native/openshift/latest/introduction.html
- https://docs.nvidia.com/datacenter/cloud-native/openshift/latest/nvaie-with-ocp.html
- https://docs.nvidia.com/datacenter/cloud-native/openshift/latest/install-gpu-ocp.html#install-nvidiagpu
- https://docs.nvidia.com/pdf/installing-openshift-on-dgx.pdf


# Cohere North on Openshift
- https://private.docs.cohere.com/docs/advanced/feature-enablement/sandbox-openshift

## Openshift for GPU scheduling/fractioning
- https://github.com/ObrienlabsDev/blog/issues/227

## Option 1: OKD
- not the same as full openshift
## Option 2: install Openshift Local (formerly CRC) on top of RHEL
- replaced by Openshift Local
- https://developers.redhat.com/products/openshift-local/overview
## Option 2: wipe drive as part of RHCOS
- no RHEL license required - 60 day eval
- we will use option 2

## Single Node Openshift - SNO
- https://docs.redhat.com/en/documentation/openshift_container_platform/4.22/html/installing_on_a_single_node/preparing-to-install-sno

## Equipment
- see devices.yaml - I will be using the Lenovo SR250 blade for non-GPU testing and a spare Lenovo P17 RTX-5000/TU-104 for GPU testing before going pre-production using an RTX-A6000/GA-102

### Get trial 60 day licence
- https://www.redhat.com/en/technologies/cloud-computing/openshift/ocp-self-managed-trial
- Use the assisted installer https://docs.redhat.com/en/documentation/assisted_installer_for_openshift_container_platform/2026/html/installing_openshift_container_platform_with_the_assisted_installer/index
- https://docs.redhat.com/en/documentation/assisted_installer_for_openshift_container_platform/2026/html/installing_openshift_container_platform_with_the_assisted_installer/installing-with-ui
- console https://console.redhat.com/
<img width="2333" height="1157" alt="image" src="https://github.com/user-attachments/assets/7b9facda-1101-44b1-94f5-823ad10e7746" />

select OCP

<img width="1787" height="769" alt="image" src="https://github.com/user-attachments/assets/957f6849-1758-492b-8e1c-de1f37262ca5" />

select datacenter

<img width="2337" height="593" alt="image" src="https://github.com/user-attachments/assets/dc095bf2-774b-4e4f-bfc9-c24fffe63322" />

dont use non-air-gapped

<img width="2345" height="1138" alt="image" src="https://github.com/user-attachments/assets/497be6ae-d199-4c75-b195-41501c1b425d" />

air-gapped

<img width="2337" height="714" alt="image" src="https://github.com/user-attachments/assets/3ee212c1-d932-4b7a-9694-60fb154855c3" />

optionally add ssh-key, ip

download ISO
<img width="2339" height="868" alt="image" src="https://github.com/user-attachments/assets/ab7260fb-5dd0-4cfa-9631-8ca38b0f254c" />

https://docs.redhat.com/en/documentation/openshift_container_platform/4.22/html/installing_an_on-premise_cluster_with_the_agent-based_installer/installing-ove

burn ISO to 128G usb drive with Rufus

<img width="463" height="650" alt="image" src="https://github.com/user-attachments/assets/ea894da9-910d-4afb-be09-a4f48791264d" />

<img width="1255" height="574" alt="image" src="https://github.com/user-attachments/assets/9ff29362-f5d5-44e8-a188-fc4f5a572961" />

### Preflight
- do not pull out the usb drive mid install - it is still used for validation and the cluster will need to be reset or the node will need to be powered down - wait 5 min
- 

### Install on SR250

### Set DNS A record

### Switch to web interface

http://192.168.0.100:3001/3ea3c05b-0f65-4ee4-85fd-53b876328cd3


```
Host details
UUID
d61e4c9c-006e-e8d0-3459-e2e38e74de32
Manufacturer
Lenovo
Product
ThinkSystem SR250 V3
Serial number
JZ019GTL
Memory capacity
32.00 GiB
CPU model name
Intel(R) Xeon(R) 6325P
CPU cores and clock speed
8 cores (hyper-threaded) at 0 MHz
CPU architecture
x86_64
Hardware type
Bare metal
BMC address
10.2.0.108
Boot mode
uefi
NTP status
Synced
4 Disks
Name	Role	Limitations	Drive type	Size	Serial	Model	WWN 
sda (bootable)	Installation disk		HDD	124.62 GB	A053081900000F5F	USB_Flash_Drive	0x5000000000000001
sdb (bootable)	None		SSD	960.20 GB	0026051W0X7N	SSSTC_ER3-CD960A	0x538f60161097b716
sdc (bootable)	None		SSD	2.00 TB	S753NL0Y208735W	Samsung_SSD_870	0x5002538f552202b1
NICs
Name	MAC address	IPv4 address	IPv6 address	Speed
eno1	10:e1:8e:b4:92:6f	192.168.0.100/24	2607:fea8:e367:3900::5593/64, 2607:fea8:e367:3900:b0a9:cb61:4c8b:b232/64	1000 Mbps
eno2	10:e1:8e:b4:92:70	10.3.0.102/16		1000 Mbps
```

20261118:1500
- need to delete all partitions on drives first - sdc first - or it looks like the iso needs to be written to the main drive 

```
This host failed its installation.
Failed - failed after 3 attempts, last error: failed executing /usr/bin/nsenter [--target 1 --cgroup --mount --ipc --pid -- coreos-installer install --insecure -i /opt/openshift/master.ign --append-karg ip=10-e1-8e-b4-92-6f:dhcp /dev/sdc], Error exit status 1, LastOutput "Error: checking for exclusive access to /dev/sdc Caused by: found busy partitions".

Writing image to disk
Step 4 of 8

```

Fix: switch installation disk after cluster reset to SDC - from usb SDA in storage screen

```
Name	Role	Limitations	Format?	Drive type	Size	Serial	Model	WWN 
sda (bootable)	
None
	HDD	124.62 GB	A053081900000F5F	USB_Flash_Drive	0x5000000000000001
sdb	
None
	SSD	960.20 GB	0026051W0X7N	SSSTC_ER3-CD960A	0x538f60161097b716
sdc	Installation disk			SSD	2.00 TB	S753NL0Y208735W	Samsung_SSD_870	0x5002538f552202b1

```

add your ssh public key
```
cat ~/.ssh/id_gdc_oldev.pub         
ssh-ed25519 AAAA...al
```

It looks like pulling the usb after rebooting - allows the RHEL os to not throw USB ISO errors

## RHCOS on P17
- used ssh key

ssh

```
ssh core@192.168.0.188   
The authenticity of host '192.168.0.188 (192.168.0.188)' can't be established.
ED25519 key fingerprint is: SHA256:BvGeg342vpOShFVNExwypM2n7Y58gublX1OT3Kq2LU0
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '192.168.0.188' (ED25519) to the list of known hosts.
Red Hat Enterprise Linux CoreOS 9.8.20261006-0
  Part of OpenShift 4.22, RHCOS is a Kubernetes-native operating system
  managed by the Machine Config Operator (`clusteroperator/machine-config`).

WARNING: Direct SSH access to machines is not recommended; instead,
make configuration changes via `machineconfig` objects:
  https://docs.openshift.com/container-platform/4.22/architecture/architecture-rhcos.html

---
Last login: Fri Nov 20 03:12:53 2026 from 192.168.0.132
[systemd]
Failed Units: 1
  systemd-network-generator.service


```

### Set api.server DNS A record
in your domain add api.server pointing to your VIP on your domain

also set *.apps.sno.ocp and api-int.p17
### kubectl or oc to ocp

download oc from https://www.redhat.com/en/blog/installing-oc-tools-windows

```
kubectl get nodes --kubeconfig ~/.kube/p17/kubeconfig

$ export KUBECONFIG=~/.kube/p17/kubeconfig
$ kubectl get nodes
NAME                STATUS   ROLES                         AGE     VERSION
54-05-db-52-24-6c   Ready    control-plane,master,worker   6d22h   v1.35.8

micha@p1gen6 MINGW64 ~
$ oc whoami
system:admin

micha@p1gen6 MINGW64 ~
$ oc get nodes -o wide
NAME                STATUS   ROLES                         AGE     VERSION   INTERNAL-IP     EXTERNAL-IP   OS-IMAGE                                                KERNEL-VERSION                 CONTAINER-RUNTIME
54-05-db-52-24-6c   Ready    control-plane,master,worker   6d22h   v1.35.8   192.168.0.188   <none>        Red Hat Enterprise Linux CoreOS 9.8.20261006-0 (Plow)   5.14.0-687.55.1.el9_8.x86_64   cri-o://1.35.9-12.rhaos4.22.git4c168db.el9

micha@p1gen6 MINGW64 ~
$ oc get mcp
NAME     CONFIG                                             UPDATED   UPDATING   DEGRADED   MACHINECOUNT   READYMACHINECOUNT   UPDATEDMACHINECOUNT   DEGRADEDMACHINECOUNT   AGE
master   rendered-master-fc96859a8fe8f6e295276f3717da21db   True      False      False      1              1                   1                     0                      6d22h
worker   rendered-worker-60faee59c42440b2a2b7b624c8c49348   True      False      False      0              0                   0                     0                      6d22h

micha@p1gen6 MINGW64 ~
$ oc get machineconfig 99-master-ssh -o yaml
apiVersion: machineconfiguration.openshift.io/v1
kind: MachineConfig
metadata:
  creationTimestamp: "2026-11-20T02:23:35Z"
  generation: 1
  labels:
    machineconfiguration.openshift.io/role: master
  name: 99-master-ssh
  resourceVersion: "2484"
  uid: 5d3785c2-ad19-4763-ba28-557d06906263
spec:
  baseOSExtensionsContainerImage: ""
  config:
    ignition:
      version: 3.2.0
    passwd:
      users:
      - name: core
        sshAuthorizedKeys:
        - ssh-ed25519 AAA...
          michaelobrien@mbp8.local
  fips: false
  kernelArguments: null
  kernelType: ""
  osImageURL: ""


$ oc get pods -A
NAMESPACE                                          NAME                                                         READY   STATUS      RESTARTS        AGE
assisted-installer                                 assisted-installer-controller-hxbv7                          0/1     Completed   3               6d22h
openshift-apiserver-operator                       openshift-apiserver-operator-7549c5f7c4-5dkqs                1/1     Running     3               6d22h
openshift-apiserver                                apiserver-69d596c497-dc56m                                   2/2     Running     0               6d22h
openshift-authentication-operator                  authentication-operator-dff949c45-42t58                      1/1     Running     2               6d22h
openshift-authentication                           oauth-openshift-f55684678-wrm9q                              1/1     Running     0               6d22h
openshift-catalogd                                 catalogd-controller-manager-58f97b94c7-8kx7r                 1/1     Running     2               6d22h
openshift-cloud-controller-manager-operator        cluster-cloud-controller-manager-operator-6b64545d59-sdjdk   2/2     Running     2               6d22h
openshift-cloud-credential-operator                cloud-credential-operator-54679b859f-5fbr7                   1/1     Running     1               6d22h
openshift-cluster-machine-approver                 machine-approver-748f74c74d-vzv7l                            2/2     Running     3               6d22h
openshift-cluster-node-tuning-operator             cluster-node-tuning-operator-67fc969dd7-mblfj                1/1     Running     1               6d22h
openshift-cluster-node-tuning-operator             tuned-n7xpm                                                  1/1     Running     1               6d22h
openshift-cluster-olm-operator                     cluster-olm-operator-6dcbd9965b-h764j                        1/1     Running     3               6d22h
openshift-cluster-samples-operator                 cluster-samples-operator-5d96bb9bb-w9r4x                     2/2     Running     2               6d22h
openshift-cluster-storage-operator                 cluster-storage-operator-5c8bc49cd4-wfgnh                    1/1     Running     1               6d22h
openshift-cluster-storage-operator                 csi-snapshot-controller-6665b6b969-rlw25                     1/1     Running     3               6d22h
openshift-cluster-storage-operator                 csi-snapshot-controller-operator-56bcc8dbb8-spwvc            1/1     Running     1               6d22h
openshift-cluster-storage-operator                 volume-data-source-validator-7f65fdc86-89wnr                 1/1     Running     2               6d22h
openshift-cluster-version                          cluster-version-operator-78c76b9cb7-pppk2                    1/1     Running     1               6d22h
openshift-config-operator                          openshift-config-operator-5bb7489dbd-v2849                   1/1     Running     4               6d22h
openshift-console-operator                         console-operator-84f84768cb-plv64                            1/1     Running     2               6d22h
openshift-console                                  console-56f7665b8d-7tqfp                                     1/1     Running     0               6d22h
openshift-console                                  downloads-548ccccc7f-m4qgg                                   1/1     Running     2               6d22h
openshift-controller-manager-operator              openshift-controller-manager-operator-65756b6d79-862q8       1/1     Running     3               6d22h
openshift-controller-manager                       controller-manager-584db895c-sddpm                           1/1     Running     0               5d22h
openshift-dns-operator                             dns-operator-cf55bf4df-zk62f                                 2/2     Running     3               6d22h
openshift-dns                                      dns-default-znnr7                                            2/2     Running     3               6d22h
openshift-dns                                      node-resolver-76w5j                                          1/1     Running     3               6d22h
openshift-etcd-operator                            etcd-operator-5884b9b7fd-ghkgd                               1/1     Running     2               6d22h
openshift-etcd                                     etcd-54-05-db-52-24-6c                                       5/5     Running     6               6d22h
openshift-etcd                                     installer-1-54-05-db-52-24-6c                                0/1     Completed   0               6d22h
openshift-image-registry                           cluster-image-registry-operator-6445776645-pbwjn             1/1     Running     1               6d22h
openshift-image-registry                           image-pruner-29926080-7x6xh                                  0/1     Completed   0               2d1h
openshift-image-registry                           image-pruner-29927520-lsrgm                                  0/1     Completed   0               25h
openshift-image-registry                           image-pruner-29928960-22q2l                                  0/1     Completed   0               73m
openshift-image-registry                           node-ca-pnvjj                                                1/1     Running     0               6d22h
openshift-ingress-canary                           ingress-canary-mpd5z                                         1/1     Running     0               6d22h
openshift-ingress-operator                         ingress-operator-59f6c9db6c-d8kfz                            2/2     Running     9 (6d22h ago)   6d22h
openshift-ingress                                  router-default-695cbdbc97-kctpm                              1/1     Running     8 (6d22h ago)   6d22h
openshift-insights                                 insights-operator-fb65b6d65-nnbmc                            1/1     Running     2               6d22h
openshift-insights                                 insights-runtime-extractor-8fxs5                             3/3     Running     4               6d22h
openshift-insights                                 periodic-gathering-7tdh2-vcbql                               0/1     Completed   0               4h22m
openshift-insights                                 periodic-gathering-9t6vp-8ccgk                               0/1     Completed   0               14h
openshift-insights                                 periodic-gathering-bpst6-nhtvd                               0/1     Completed   0               20h
openshift-insights                                 periodic-gathering-hc88c-pd5fx                               0/1     Completed   0               12h
openshift-insights                                 periodic-gathering-ktrvc-4sxtm                               0/1     Completed   0               6h22m
openshift-insights                                 periodic-gathering-nlmm7-6csnf                               0/1     Completed   0               16h
openshift-insights                                 periodic-gathering-pdbd8-l56rw                               0/1     Completed   0               22m
openshift-insights                                 periodic-gathering-phthh-cmxnz                               0/1     Completed   0               24h
openshift-insights                                 periodic-gathering-pt57m-5k585                               0/1     Completed   0               8h
openshift-insights                                 periodic-gathering-r4qwl-wr7tr                               0/1     Completed   0               22h
openshift-insights                                 periodic-gathering-tsz2t-6742s                               0/1     Completed   0               10h
openshift-insights                                 periodic-gathering-x7pz6-fz8km                               0/1     Completed   0               18h
openshift-insights                                 periodic-gathering-xh24c-hds5x                               0/1     Completed   0               142m
openshift-kube-apiserver-operator                  kube-apiserver-operator-5c7f66c5bb-tmm2v                     1/1     Running     3               6d22h
openshift-kube-apiserver                           installer-1-54-05-db-52-24-6c                                0/1     Error       0               6d22h
openshift-kube-apiserver                           installer-10-54-05-db-52-24-6c                               0/1     Completed   0               5d22h
openshift-kube-apiserver                           installer-3-54-05-db-52-24-6c                                0/1     Completed   0               6d22h
openshift-kube-apiserver                           installer-4-54-05-db-52-24-6c                                0/1     Completed   0               6d22h
openshift-kube-apiserver                           installer-5-54-05-db-52-24-6c                                0/1     Completed   0               6d22h
openshift-kube-apiserver                           installer-6-54-05-db-52-24-6c                                0/1     Completed   0               6d4h
openshift-kube-apiserver                           installer-7-54-05-db-52-24-6c                                0/1     Completed   0               6d3h
openshift-kube-apiserver                           installer-8-54-05-db-52-24-6c                                0/1     Completed   0               6d3h
openshift-kube-apiserver                           installer-9-54-05-db-52-24-6c                                0/1     Completed   0               6d
openshift-kube-apiserver                           kube-apiserver-54-05-db-52-24-6c                             5/5     Running     0               5d22h
openshift-kube-controller-manager-operator         kube-controller-manager-operator-55c659cb7-cbmtb             1/1     Running     3               6d22h
openshift-kube-controller-manager                  installer-2-54-05-db-52-24-6c                                0/1     Error       0               6d22h
openshift-kube-controller-manager                  installer-2-retry-1-54-05-db-52-24-6c                        0/1     Completed   0               6d22h
openshift-kube-controller-manager                  installer-3-54-05-db-52-24-6c                                0/1     Completed   0               6d22h
openshift-kube-controller-manager                  installer-4-54-05-db-52-24-6c                                0/1     Completed   0               6d22h
openshift-kube-controller-manager                  kube-controller-manager-54-05-db-52-24-6c                    4/4     Running     6 (5d22h ago)   6d22h
openshift-kube-scheduler-operator                  openshift-kube-scheduler-operator-5598d65879-68g56           1/1     Running     3               6d22h
openshift-kube-scheduler                           installer-3-54-05-db-52-24-6c                                0/1     Error       0               6d22h
openshift-kube-scheduler                           installer-4-54-05-db-52-24-6c                                0/1     Completed   0               6d22h
openshift-kube-scheduler                           openshift-kube-scheduler-54-05-db-52-24-6c                   3/3     Running     0               6d22h
openshift-kube-storage-version-migrator-operator   kube-storage-version-migrator-operator-6bccdcf87b-6c72r      1/1     Running     2               6d22h
openshift-kube-storage-version-migrator            migrator-b9c56dd-grghc                                       1/1     Running     2               6d22h
openshift-machine-api                              cluster-autoscaler-operator-56d44b976-zz5pm                  2/2     Running     3               6d22h
openshift-machine-api                              cluster-baremetal-operator-55d6599cbd-xmmcv                  2/2     Running     5               6d22h
openshift-machine-api                              control-plane-machine-set-operator-cf7d7d95b-pcfz9           1/1     Running     2               6d22h
openshift-machine-api                              machine-api-operator-b5dc56dcf-mg744                         1/1     Running     2               6d22h
openshift-machine-config-operator                  kube-rbac-proxy-crio-54-05-db-52-24-6c                       1/1     Running     2               6d22h
openshift-machine-config-operator                  machine-config-controller-5cfb667c46-svt8p                   2/2     Running     4               6d22h
openshift-machine-config-operator                  machine-config-daemon-qzzrw                                  2/2     Running     4               6d22h
openshift-machine-config-operator                  machine-config-operator-6dd84cb4d7-m2gzn                     1/1     Running     1               6d22h
openshift-machine-config-operator                  machine-config-server-ffl6q                                  1/1     Running     3               6d22h
openshift-marketplace                              marketplace-operator-58bb89c964-cdkrb                        1/1     Running     3 (6d4h ago)    6d22h
openshift-marketplace                              redhat-operators-7gnll                                       1/1     Running     1               6d22h
openshift-monitoring                               alertmanager-main-0                                          6/6     Running     0               6d22h
openshift-monitoring                               cluster-monitoring-operator-84fdb55f56-kjdp8                 1/1     Running     2               6d22h
openshift-monitoring                               kube-state-metrics-6f5c8ff794-n8924                          3/3     Running     4               6d22h
openshift-monitoring                               metrics-server-7b557cd485-sftnd                              1/1     Running     0               5d22h
openshift-monitoring                               monitoring-plugin-d5999f765-lgx7w                            1/1     Running     2               6d22h
openshift-monitoring                               node-exporter-gqkvh                                          2/2     Running     3               6d22h
openshift-monitoring                               openshift-state-metrics-65db95dcf8-jklsr                     3/3     Running     5               6d22h
openshift-monitoring                               prometheus-k8s-0                                             6/6     Running     0               6d22h
openshift-monitoring                               prometheus-operator-758c4789bb-bnqcn                         2/2     Running     3               6d22h
openshift-monitoring                               prometheus-operator-admission-webhook-574f849897-8nbc5       1/1     Running     2               6d22h
openshift-monitoring                               telemeter-client-785dfb5dd-hmszn                             3/3     Running     4               6d22h
openshift-monitoring                               thanos-querier-6448b7897d-q9rf8                              6/6     Running     0               6d22h
openshift-multus                                   multus-additional-cni-plugins-gqn9c                          1/1     Running     2               6d22h
openshift-multus                                   multus-admission-controller-58f6bb84d8-csllg                 2/2     Running     0               6d22h
openshift-multus                                   multus-zk544                                                 1/1     Running     3               6d22h
openshift-multus                                   network-metrics-daemon-q2kpl                                 2/2     Running     3               6d22h
openshift-network-console                          networking-console-plugin-747f555d44-b5vtf                   1/1     Running     0               6d22h
openshift-network-diagnostics                      network-check-source-cd6c84c6d-tbx7v                         1/1     Running     2               6d22h
openshift-network-diagnostics                      network-check-target-zsf5x                                   1/1     Running     2               6d22h
openshift-network-node-identity                    network-node-identity-6gd5d                                  2/2     Running     4               6d22h
openshift-network-operator                         iptables-alerter-j6f9z                                       1/1     Running     3               6d22h
openshift-network-operator                         network-operator-76d8987977-mgjsn                            1/1     Running     3               6d22h
openshift-oauth-apiserver                          apiserver-769bdb95d5-8xs4j                                   1/1     Running     1               6d22h
openshift-operator-controller                      operator-controller-controller-manager-694bb64b58-8p2t8      1/1     Running     2               6d22h
openshift-operator-lifecycle-manager               catalog-operator-d7665cc48-w8tbm                             1/1     Running     2               6d22h
openshift-operator-lifecycle-manager               olm-operator-9c49c896-2kv72                                  1/1     Running     2               6d22h
openshift-operator-lifecycle-manager               package-server-manager-5dd54fc894-lxvhj                      1/1     Running     1               6d22h
openshift-operator-lifecycle-manager               packageserver-67bb54f686-fxv49                               1/1     Running     2               6d22h
openshift-ovn-kubernetes                           ovnkube-control-plane-f64cf54c7-f5v7g                        2/2     Running     5               6d22h
openshift-ovn-kubernetes                           ovnkube-node-kc79p                                           8/8     Running     9               6d22h
openshift-route-controller-manager                 route-controller-manager-d8cf6d5c6-sppr7                     1/1     Running     0               5d22h
openshift-service-ca-operator                      service-ca-operator-fc9d8cf5c-r4nxb                          1/1     Running     3               6d22h
openshift-service-ca                               service-ca-6dff57f876-zcmdk                                  1/1     Running     1               6d22h

$ oc get services -A
NAMESPACE                                          NAME                                       TYPE           CLUSTER-IP       EXTERNAL-IP                            PORT(S)                                        AGE
default                                            kubernetes                                 ClusterIP      172.30.0.1       <none>                                 443/TCP                                        6d22h
default                                            openshift                                  ExternalName   <none>           kubernetes.default.svc.cluster.local   <none>                                         6d22h
kube-system                                        kubelet                                    ClusterIP      None             <none>                                 10250/TCP,4194/TCP,10255/TCP                   6d22h
openshift-apiserver-operator                       metrics                                    ClusterIP      172.30.134.133   <none>                                 443/TCP                                        6d22h
openshift-apiserver                                api                                        ClusterIP      172.30.154.140   <none>                                 443/TCP                                        6d22h
openshift-apiserver                                check-endpoints                            ClusterIP      172.30.206.177   <none>                                 17698/TCP                                      6d22h
openshift-authentication-operator                  metrics                                    ClusterIP      172.30.170.254   <none>                                 443/TCP                                        6d22h
openshift-authentication                           oauth-openshift                            ClusterIP      172.30.52.61     <none>                                 443/TCP                                        6d22h
openshift-catalogd                                 catalogd-service                           ClusterIP      172.30.89.217    <none>                                 443/TCP,9443/TCP,7443/TCP                      6d22h
openshift-cloud-controller-manager-operator        cloud-controller-manager-operator          ClusterIP      None             <none>                                 9258/TCP,9443/TCP                              6d22h
openshift-cloud-credential-operator                cco-metrics                                ClusterIP      172.30.182.149   <none>                                 8443/TCP                                       6d22h
openshift-cluster-machine-approver                 machine-approver                           ClusterIP      None             <none>                                 9192/TCP                                       6d22h
openshift-cluster-node-tuning-operator             node-tuning-operator                       ClusterIP      None             <none>                                 60000/TCP                                      6d22h
openshift-cluster-node-tuning-operator             performance-addon-operator-service         ClusterIP      172.30.176.40    <none>                                 443/TCP                                        6d22h
openshift-cluster-olm-operator                     cluster-olm-operator-metrics               ClusterIP      172.30.69.151    <none>                                 443/TCP                                        6d22h
openshift-cluster-samples-operator                 metrics                                    ClusterIP      None             <none>                                 60000/TCP                                      6d22h
openshift-cluster-storage-operator                 cluster-storage-operator-metrics           ClusterIP      172.30.122.207   <none>                                 443/TCP                                        6d22h
openshift-cluster-storage-operator                 csi-snapshot-controller-operator-metrics   ClusterIP      172.30.186.37    <none>                                 443/TCP                                        6d22h
openshift-cluster-version                          cluster-version-operator                   ClusterIP      172.30.193.230   <none>                                 9099/TCP                                       6d22h
openshift-config-operator                          metrics                                    ClusterIP      172.30.157.132   <none>                                 443/TCP                                        6d22h
openshift-console-operator                         metrics                                    ClusterIP      172.30.63.17     <none>                                 443/TCP                                        6d22h
openshift-console                                  console                                    ClusterIP      172.30.152.197   <none>                                 443/TCP                                        6d22h
openshift-console                                  downloads                                  ClusterIP      172.30.220.188   <none>                                 80/TCP                                         6d22h
openshift-controller-manager-operator              metrics                                    ClusterIP      172.30.2.36      <none>                                 443/TCP                                        6d22h
openshift-controller-manager                       controller-manager                         ClusterIP      172.30.151.110   <none>                                 443/TCP                                        6d22h
openshift-dns-operator                             metrics                                    ClusterIP      172.30.229.171   <none>                                 9393/TCP                                       6d22h
openshift-dns                                      dns-default                                ClusterIP      172.30.0.10      <none>                                 53/UDP,53/TCP,9154/TCP                         6d22h
openshift-etcd-operator                            metrics                                    ClusterIP      172.30.132.55    <none>                                 443/TCP                                        6d22h
openshift-etcd                                     etcd                                       ClusterIP      172.30.185.60    <none>                                 2379/TCP,2380/TCP,9978/TCP,9979/TCP,9980/TCP   6d22h
openshift-image-registry                           image-registry-operator                    ClusterIP      None             <none>                                 60000/TCP                                      6d22h
openshift-ingress-canary                           ingress-canary                             ClusterIP      172.30.155.173   <none>                                 8443/TCP,8888/TCP                              6d22h
openshift-ingress-operator                         metrics                                    ClusterIP      172.30.23.212    <none>                                 9393/TCP                                       6d22h
openshift-ingress                                  router-internal-default                    ClusterIP      172.30.178.37    <none>                                 80/TCP,443/TCP,1936/TCP                        6d22h
openshift-insights                                 exporter                                   ClusterIP      None             <none>                                 8000/TCP                                       6d22h
openshift-insights                                 metrics                                    ClusterIP      172.30.105.114   <none>                                 443/TCP                                        6d22h
openshift-kube-apiserver-operator                  metrics                                    ClusterIP      172.30.119.111   <none>                                 443/TCP                                        6d22h
openshift-kube-apiserver                           apiserver                                  ClusterIP      172.30.10.3      <none>                                 443/TCP,6080/TCP,17697/TCP                     6d22h
openshift-kube-controller-manager-operator         metrics                                    ClusterIP      172.30.55.57     <none>                                 443/TCP                                        6d22h
openshift-kube-controller-manager                  kube-controller-manager                    ClusterIP      172.30.187.79    <none>                                 443/TCP                                        6d22h
openshift-kube-scheduler-operator                  metrics                                    ClusterIP      172.30.227.169   <none>                                 443/TCP                                        6d22h
openshift-kube-scheduler                           scheduler                                  ClusterIP      172.30.193.41    <none>                                 443/TCP                                        6d22h
openshift-kube-storage-version-migrator-operator   metrics                                    ClusterIP      172.30.71.139    <none>                                 443/TCP                                        6d22h
openshift-machine-api                              cluster-autoscaler-operator                ClusterIP      172.30.146.52    <none>                                 443/TCP,9192/TCP                               6d22h
openshift-machine-api                              cluster-baremetal-operator-service         ClusterIP      172.30.230.172   <none>                                 8443/TCP                                       6d22h
openshift-machine-api                              cluster-baremetal-webhook-service          ClusterIP      172.30.173.189   <none>                                 443/TCP                                        6d22h
openshift-machine-api                              control-plane-machine-set-operator         ClusterIP      172.30.243.235   <none>                                 9443/TCP                                       6d22h
openshift-machine-api                              machine-api-controllers                    ClusterIP      172.30.61.10     <none>                                 8441/TCP,8442/TCP,8444/TCP                     6d22h
openshift-machine-api                              machine-api-operator                       ClusterIP      172.30.144.40    <none>                                 8443/TCP                                       6d22h
openshift-machine-api                              machine-api-operator-machine-webhook       ClusterIP      172.30.88.42     <none>                                 443/TCP                                        6d22h
openshift-machine-api                              machine-api-operator-webhook               ClusterIP      172.30.103.160   <none>                                 443/TCP                                        6d22h
openshift-machine-config-operator                  internal-release-image-registry            ClusterIP      172.30.18.246    <none>                                 22625/TCP                                      6d22h
openshift-machine-config-operator                  kube-rbac-proxy-crio                       ClusterIP      172.30.231.245   <none>                                 9637/TCP                                       6d22h
openshift-machine-config-operator                  machine-config-controller                  ClusterIP      172.30.99.26     <none>                                 9001/TCP                                       6d22h
openshift-machine-config-operator                  machine-config-daemon                      ClusterIP      172.30.81.2      <none>                                 9001/TCP                                       6d22h
openshift-machine-config-operator                  machine-config-server                      ClusterIP      172.30.64.136    <none>                                 22623/TCP,22624/TCP                            6d22h
openshift-marketplace                              marketplace-operator-metrics               ClusterIP      172.30.190.71    <none>                                 8383/TCP,8081/TCP                              6d22h
openshift-marketplace                              redhat-operators                           ClusterIP      172.30.21.165    <none>                                 50051/TCP                                      6d22h
openshift-monitoring                               alertmanager-main                          ClusterIP      172.30.26.242    <none>                                 9094/TCP,9092/TCP,9097/TCP                     6d22h
openshift-monitoring                               alertmanager-operated                      ClusterIP      None             <none>                                 9093/TCP,9094/TCP,9094/UDP                     6d22h
openshift-monitoring                               cluster-monitoring-operator                ClusterIP      None             <none>                                 8443/TCP                                       6d22h
openshift-monitoring                               kube-state-metrics                         ClusterIP      None             <none>                                 8443/TCP,9443/TCP                              6d22h
openshift-monitoring                               metrics-server                             ClusterIP      172.30.82.96     <none>                                 443/TCP                                        6d22h
openshift-monitoring                               monitoring-plugin                          ClusterIP      172.30.70.10     <none>                                 9443/TCP                                       6d22h
openshift-monitoring                               node-exporter                              ClusterIP      None             <none>                                 9100/TCP                                       6d22h
openshift-monitoring                               openshift-state-metrics                    ClusterIP      None             <none>                                 8443/TCP,9443/TCP                              6d22h
openshift-monitoring                               prometheus-k8s                             ClusterIP      172.30.55.81     <none>                                 9091/TCP,9092/TCP                              6d22h
openshift-monitoring                               prometheus-k8s-thanos-sidecar              ClusterIP      None             <none>                                 10902/TCP                                      6d22h
openshift-monitoring                               prometheus-operated                        ClusterIP      None             <none>                                 9090/TCP,10901/TCP                             6d22h
openshift-monitoring                               prometheus-operator                        ClusterIP      None             <none>                                 8443/TCP                                       6d22h
openshift-monitoring                               prometheus-operator-admission-webhook      ClusterIP      172.30.48.85     <none>                                 8443/TCP                                       6d22h
openshift-monitoring                               telemeter-client                           ClusterIP      None             <none>                                 8443/TCP                                       6d22h
openshift-monitoring                               thanos-querier                             ClusterIP      172.30.185.249   <none>                                 9091/TCP,9092/TCP,9093/TCP,9094/TCP            6d22h
openshift-multus                                   multus-admission-controller                ClusterIP      172.30.183.99    <none>                                 443/TCP,8443/TCP                               6d22h
openshift-multus                                   network-metrics-service                    ClusterIP      None             <none>                                 8443/TCP                                       6d22h
openshift-network-console                          networking-console-plugin                  ClusterIP      172.30.223.234   <none>                                 9443/TCP                                       6d22h
openshift-network-diagnostics                      network-check-source                       ClusterIP      None             <none>                                 17698/TCP                                      6d22h
openshift-network-diagnostics                      network-check-target                       ClusterIP      172.30.71.124    <none>                                 80/TCP                                         6d22h
openshift-network-operator                         metrics                                    ClusterIP      None             <none>                                 9104/TCP                                       6d22h
openshift-oauth-apiserver                          api                                        ClusterIP      172.30.106.84    <none>                                 443/TCP                                        6d22h
openshift-operator-controller                      operator-controller-service                ClusterIP      172.30.52.52     <none>                                 8443/TCP                                       6d22h
openshift-operator-lifecycle-manager               catalog-operator-metrics                   ClusterIP      172.30.22.173    <none>                                 8443/TCP                                       6d22h
openshift-operator-lifecycle-manager               olm-operator-metrics                       ClusterIP      172.30.100.52    <none>                                 8443/TCP                                       6d22h
openshift-operator-lifecycle-manager               package-server-manager-metrics             ClusterIP      172.30.1.70      <none>                                 8443/TCP                                       6d22h
openshift-operator-lifecycle-manager               packageserver-service                      ClusterIP      172.30.122.46    <none>                                 5443/TCP                                       6d22h
openshift-ovn-kubernetes                           ovn-kubernetes-control-plane               ClusterIP      None             <none>                                 9108/TCP                                       6d22h
openshift-ovn-kubernetes                           ovn-kubernetes-node                        ClusterIP      None             <none>                                 9103/TCP,9105/TCP                              6d22h
openshift-route-controller-manager                 route-controller-manager                   ClusterIP      172.30.188.52    <none>                                 443/TCP                                        6d22h
openshift-service-ca-operator                      metrics                                    ClusterIP      172.30.100.34    <none>                                 443/TCP                                        6d22h



$ kubectl get events -A
NAMESPACE                                     LAST SEEN   TYPE      REASON             OBJECT                                                           MESSAGE
openshift-cloud-controller-manager-operator   3m27s       Warning   DNSConfigForming   pod/cluster-cloud-controller-manager-operator-6b64545d59-sdjdk   Nameserver limits were exceeded, some nameservers have been omitted, the applied nameserver line is: 192.168.0.188 64.71.255.204 64.71.255.198
openshift-cluster-machine-approver            3m8s        Warning   DNSConfigForming   pod/machine-approver-748f74c74d-vzv7l                            Nameserver limits were exceeded, some nameservers have been omitted, the applied nameserver line is: 192.168.0.188 64.71.255.204 64.71.255.198
openshift-cluster-node-tuning-operator        2m25s       Warning   DNSConfigForming   pod/tuned-n7xpm                                                  Nameserver limits were exceeded, some nameservers have been omitted, the applied nameserver line is: 192.168.0.188 64.71.255.204 64.71.255.198
openshift-cluster-version                     3m19s       Warning   DNSConfigForming   pod/cluster-version-operator-78c76b9cb7-pppk2                    Nameserver limits were exceeded, some nameservers have been omitted, the applied nameserver line is: 192.168.0.188 64.71.255.204 64.71.255.198
openshift-dns-operator                        3m16s       Warning   DNSConfigForming   pod/dns-operator-cf55bf4df-zk62f                                 Nameserver limits were exceeded, some nameservers have been omitted, the applied nameserver line is: 192.168.0.188 64.71.255.204 64.71.255.198
openshift-dns                                 2m57s       Warning   DNSConfigForming   pod/dns-default-znnr7                                            Nameserver limits were exceeded, some nameservers have been omitted, the applied nameserver line is: 192.168.0.188 64.71.255.204 64.71.255.198
openshift-dns                                 3m10s       Warning   DNSConfigForming   pod/node-resolver-76w5j                                          Nameserver limits were exceeded, some nameservers have been omitted, the applied nameserver line is: 192.168.0.188 64.71.255.204 64.71.255.198
openshift-etcd                                3m6s        Warning   DNSConfigForming   pod/etcd-54-05-db-52-24-6c                                       Nameserver limits were exceeded, some nameservers have been omitted, the applied nameserver line is: 192.168.0.188 64.71.255.204 64.71.255.198
openshift-image-registry                      74m         Normal    Scheduled          pod/image-pruner-29928960-22q2l                                  Successfully assigned openshift-image-registry/image-pruner-29928960-22q2l to 54-05-db-52-24-6c
openshift-image-registry                      74m         Normal    AddedInterface     pod/image-pruner-29928960-22q2l                                  Add eth0 [10.128.0.198/23] from ovn-kubernetes
openshift-image-registry                      74m         Normal    Pulled             pod/image-pruner-29928960-22q2l                                  Container image "quay.io/openshift-release-dev/ocp-v4.0-art-dev@sha256:b31735da2b1e3b06734f3f504ac8ece7c71cfdd96ca74c5f750b600f3dc1a421" already present on machine and can be accessed by the pod
openshift-image-registry                      74m         Normal    Created            pod/image-pruner-29928960-22q2l                                  Container created
openshift-image-registry                      74m         Normal    Started            pod/image-pruner-29928960-22q2l                                  Container started
openshift-image-registry                      74m         Normal    SuccessfulCreate   job/image-pruner-29928960                                        Created pod: image-pruner-29928960-22q2l
openshift-image-registry                      74m         Normal    Completed          job/image-pruner-29928960                                        Job completed
openshift-image-registry                      74m         Normal    SuccessfulCreate   cronjob/image-pruner                                             Created job image-pruner-29928960
openshift-image-registry                      74m         Normal    SuccessfulDelete   cronjob/image-pruner                                             Deleted job image-pruner-29924640
openshift-image-registry                      74m         Normal    SawCompletedJob    cronjob/image-pruner                                             Saw completed job: image-pruner-29928960, condition: Complete
openshift-image-registry                      0s          Warning   DNSConfigForming   pod/node-ca-pnvjj                                                Nameserver limits were exceeded, some nameservers have been omitted, the applied nameserver line is: 192.168.0.188 64.71.255.204 64.71.255.198
openshift-insights                            24m         Normal    Scheduled          pod/periodic-gathering-pdbd8-l56rw                               Successfully assigned openshift-insights/periodic-gathering-pdbd8-l56rw to 54-05-db-52-24-6c
openshift-insights                            24m         Normal    AddedInterface     pod/periodic-gathering-pdbd8-l56rw                               Add eth0 [10.128.0.199/23] from ovn-kubernetes
openshift-insights                            24m         Normal    Pulled             pod/periodic-gathering-pdbd8-l56rw                               Container image "quay.io/openshift-release-dev/ocp-v4.0-art-dev@sha256:7efbed4a1867dc73fe9626e69ec959f817a5f7afb9ab43f4c6156537c7222516" already present on machine and can be accessed by the pod
openshift-insights                            24m         Normal    Created            pod/periodic-gathering-pdbd8-l56rw                               Container created
openshift-insights                            24m         Normal    Started            pod/periodic-gathering-pdbd8-l56rw                               Container started
openshift-insights                            24m         Normal    SuccessfulCreate   job/periodic-gathering-pdbd8                                     Created pod: periodic-gathering-pdbd8-l56rw
openshift-insights                            23m         Normal    Completed          job/periodic-gathering-pdbd8                                     Job completed
openshift-insights                            144m        Normal    Scheduled          pod/periodic-gathering-xh24c-hds5x                               Successfully assigned openshift-insights/periodic-gathering-xh24c-hds5x to 54-05-db-52-24-6c
openshift-insights                            144m        Normal    AddedInterface     pod/periodic-gathering-xh24c-hds5x                               Add eth0 [10.128.0.197/23] from ovn-kubernetes
openshift-insights                            144m        Normal    Pulled             pod/periodic-gathering-xh24c-hds5x                               Container image "quay.io/openshift-release-dev/ocp-v4.0-art-dev@sha256:7efbed4a1867dc73fe9626e69ec959f817a5f7afb9ab43f4c6156537c7222516" already present on machine and can be accessed by the pod
openshift-insights                            144m        Normal    Created            pod/periodic-gathering-xh24c-hds5x                               Container created
openshift-insights                            144m        Normal    Started            pod/periodic-gathering-xh24c-hds5x                               Container started
openshift-insights                            144m        Normal    SuccessfulCreate   job/periodic-gathering-xh24c                                     Created pod: periodic-gathering-xh24c-hds5x
openshift-insights                            143m        Normal    Completed          job/periodic-gathering-xh24c                                     Job completed
openshift-kube-apiserver                      3m30s       Warning   DNSConfigForming   pod/kube-apiserver-54-05-db-52-24-6c                             Nameserver limits were exceeded, some nameservers have been omitted, the applied nameserver line is: 192.168.0.188 64.71.255.204 64.71.255.198
openshift-kube-controller-manager             41s         Warning   DNSConfigForming   pod/kube-controller-manager-54-05-db-52-24-6c                    Nameserver limits were exceeded, some nameservers have been omitted, the applied nameserver line is: 192.168.0.188 64.71.255.204 64.71.255.198
openshift-kube-scheduler                      2m51s       Warning   DNSConfigForming   pod/openshift-kube-scheduler-54-05-db-52-24-6c                   Nameserver limits were exceeded, some nameservers have been omitted, the applied nameserver line is: 192.168.0.188 64.71.255.204 64.71.255.198
openshift-machine-config-operator             3m34s       Warning   DNSConfigForming   pod/kube-rbac-proxy-crio-54-05-db-52-24-6c                       Nameserver limits were exceeded, some nameservers have been omitted, the applied nameserver line is: 192.168.0.188 64.71.255.204 64.71.255.198
openshift-machine-config-operator             2m34s       Warning   DNSConfigForming   pod/machine-config-daemon-qzzrw                                  Nameserver limits were exceeded, some nameservers have been omitted, the applied nameserver line is: 192.168.0.188 64.71.255.204 64.71.255.198
openshift-machine-config-operator             3m39s       Warning   DNSConfigForming   pod/machine-config-server-ffl6q                                  Nameserver limits were exceeded, some nameservers have been omitted, the applied nameserver line is: 192.168.0.188 64.71.255.204 64.71.255.198
openshift-monitoring                          3m42s       Warning   DNSConfigForming   pod/node-exporter-gqkvh                                          Nameserver limits were exceeded, some nameservers have been omitted, the applied nameserver line is: 192.168.0.188 64.71.255.204 64.71.255.198
openshift-multus                              2m26s       Warning   DNSConfigForming   pod/multus-additional-cni-plugins-gqn9c                          Nameserver limits were exceeded, some nameservers have been omitted, the applied nameserver line is: 192.168.0.188 64.71.255.204 64.71.255.198
openshift-multus                              2m56s       Warning   DNSConfigForming   pod/multus-zk544                                                 Nameserver limits were exceeded, some nameservers have been omitted, the applied nameserver line is: 192.168.0.188 64.71.255.204 64.71.255.198
openshift-network-node-identity               3m26s       Warning   DNSConfigForming   pod/network-node-identity-6gd5d                                  Nameserver limits were exceeded, some nameservers have been omitted, the applied nameserver line is: 192.168.0.188 64.71.255.204 64.71.255.198
openshift-network-operator                    2m57s       Warning   DNSConfigForming   pod/iptables-alerter-j6f9z                                       Nameserver limits were exceeded, some nameservers have been omitted, the applied nameserver line is: 192.168.0.188 64.71.255.204 64.71.255.198
openshift-network-operator                    2m30s       Warning   DNSConfigForming   pod/network-operator-76d8987977-mgjsn                            Nameserver limits were exceeded, some nameservers have been omitted, the applied nameserver line is: 192.168.0.188 64.71.255.204 64.71.255.198
openshift-ovn-kubernetes                      3m39s       Warning   DNSConfigForming   pod/ovnkube-control-plane-f64cf54c7-f5v7g                        Nameserver limits were exceeded, some nameservers have been omitted, the applied nameserver line is: 192.168.0.188 64.71.255.204 64.71.255.198
openshift-ovn-kubernetes                      3m18s       Warning   DNSConfigForming   pod/ovnkube-node-kc79p                                           Nameserver limits were exceeded, some nameservers have been omitted, the applied nameserver line is: 192.168.0.188 64.71.255.204 64.71.255.198




```

# Links
- https://
- developers.redhat.com/products
