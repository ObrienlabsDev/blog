# Python
## get processor() - for when you need to verify native ARM64 support (no Rosetta)
```
>>> import platform
>>> platform.processor()
'Intel64 Family 6 Model 158 Stepping 10, GenuineIntel'

```
# OSX
## SCP
```
scp -P 2022 ~/Downloads/ubuntu-24.04.1-live-server-arm64.iso m..en@1..9:/Users/m../Downloads
```
## Tunnelling
### SSH
```
 ssh m..@1.. -p 2.2 
```
### Tunnel for an SQL Server
```
sh-add ~/keys/obri..15.pem 
src % ssh -L 34.6:localhost:22 ubuntu@3...36 -i ~/keys/obr..115.pem
```

# Windows
## ssh
```
eval `ssh-agent`
```

# Smalltalk
- Smalltalk V or ParcPlace
