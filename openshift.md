# Openshift
- https://github.com/ObrienlabsDev/blog/issues/38

## Openshift for GPU scheduling/fractioning
- https://github.com/ObrienlabsDev/blog/issues/227
- 
## Option 1: install CRC on top of RHEL
## Option 2: wipe drive as part of RHCOS
- no RHEL license required
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




# Links
- https://developers.redhat.com/products
