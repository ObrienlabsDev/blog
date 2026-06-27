# Docker installs for Kubernetes orchestration
## Ubuntu SNAP
```
sudo snap install docker
sudo addgroup --system docker
sudo adduser ubuntu docker
reboot

```

## Rancher / RKE
```
sudo usermod -aG docker ubuntu
```
