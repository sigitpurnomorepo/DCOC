### Add new disk partition
1. Add new disk partition LVM
```
lsblk

sudo pvcreate /dev/sdb
sudo pvs

sudo vgcreate vg-data /dev/sdb
sudo vgs

sudo lvcreate -l 100%FREE -n lv-data vg-data
sudo lvs

sudo mkfs.xfs /dev/vg-data/lv-data

sudo mkdir /data

sudo mount /dev/vg-data/lv-data /data

df -h -T

sudo blkid /dev/vg-data/lv-data 

sudo vim /etc/fstab 

UUID=46abf059-77fa-4e8b-acdc-28cb4d98b3ef /data xfs defaults 0 0

sudo reboot

df -h -T
```

2. Add new disk partition EXT4
```
lsblk 

// Buat partisi baru
fdisk /dev/sdc

// Muncul pilihan
Command (m for help): n  -> membuat partisi baru
Partition type: p        -> partisi primary
Partition number: 1      -> nomor partisi (nilai default)
First sector: (Enter)    -> awal sektor (default)
Last sector: (Enter)     -> akhir sektor (akhir disk)
Command (m for help): w  -> save & exit

// Hasilnya partisi baru /dev/sdc1

// Format dengan EXT4
mkfs.ext4 /dev/sdc1

// Buat directory mount point 
mkdir /DATA

// Mount volume to directory
mount /dev/sdc1 /DATA

// cari UUID partisi /DATA untuk auto mount 
blkid /dev/sdc1
  // akan keluar seperti ini : UUID="a1b2c3d4-e5f6-7890-abc1-def234567890"

// Edit file fstab
vim /etc/fstab
  // Tambahkan baris 
  UUID=a1b2c3d4-e5f6-7890-abc1-def234567890   /DATA   ext4   defaults   0 2

// Test fstab (wajib sebelum reboot!)
mount -a
  // Jika tidak ada pesan error berarti fstab benar

//Reboot dan setelah itu cek partisi disk
df -hT
```
3. Install Sophos
```bash
./SophosSetup.sh
```
4. Cek apakah asset vm sudah ada di Sophos Central
