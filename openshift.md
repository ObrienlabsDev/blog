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

# Links
- https://
- developers.redhat.com/products
