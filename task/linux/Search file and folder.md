
### Cek device real
```
  nmcli connection show
```
### Hapus HWADDR (kalau ada)
```
  vi /etc/sysconfig/network-scripts/ifcfg-eth0

HWADDR=xxxx
```
### Aktifkan device manual
```
  nmcli device connect eth0
```
### Up connection
```
  nmcli connection up eth0
```
### Cek Status
```
  nmcli device status
  nmcli connection show
 ip a
```
