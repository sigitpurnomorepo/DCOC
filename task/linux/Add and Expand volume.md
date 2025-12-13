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

2. Add new disk partition EXT4 with type partition LVM
```
// Cek disk
lsblk 

// Buat partisi baru
fdisk /dev/sdc

// Muncul pilihan
Command (m for help): n  -> membuat partisi baru
Partition type: p        -> partisi primary
Partition number: 1      -> nomor partisi (nilai default)
First sector: (Enter)    -> awal sektor (default)
Last sector: (Enter)     -> akhir sektor (akhir disk)
  // Hasilnya partisi baru /dev/sdc1

// Change tipe partisi /dev/sdc1 to LVM
Command (m for help): t  -> mengubah tipe partisi
Select partition: 1
Hex code or alias (type L to list all): 8e

// Cek detail informasi partisi
Command (m for help): p -> cek detail informasi partisi 
output: Device     Boot Start     End Sectors Size Id Type
        /dev/sdc1        2048 4194303 4192256   2G 8e Linux LVM

// Write table to disk and exit
Command (m for help): w  -> Write table to disk and exit

// Create LVM from /DATA
pvcreate /dev/sdb
pvs
vgcreate vg-data /dev/sdb
vgs
lvcreate -l +100%FREE -n lv-data vg-data
lvs
mkfs.ext4 /dev/vg-data/lv-data

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
