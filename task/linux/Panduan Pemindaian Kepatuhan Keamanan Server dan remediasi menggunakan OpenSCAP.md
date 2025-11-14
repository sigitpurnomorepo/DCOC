## Panduan Pemindaian Kepatuhan Keamanan Server dan remediasi menggunakan OpenSCAP

1. Pastikan pada saat instal vm pilih Security Profil dan pilih ANSSI-BP-028 (minimal), untuk meminimalisir remediasi secara manual
   
   <img width="805" height="488" alt="image" src="https://github.com/user-attachments/assets/09a8c5ba-8be8-4010-952f-a2f54e285869" />


   <img width="805" height="559" alt="image" src="https://github.com/user-attachments/assets/c46718a5-2344-402b-a5ee-ee9f186faca6" />

<br>

2. Instal Paket OpenSCAP dan SCAP Security Guide
```
sudo dnf install openscap openscap-utils scap-security-guide
```

<br>

3. Verifikasi Paket OpenSCAP yang Sudah Terinstal
```
sudo dnf list installed | grep openscap
```

<br>

4. Cek Informasi detail File Data Stream SCAP
```
oscap info /usr/share/xml/scap/ssg/content/ssg-ol9-ds.xml
```

<br>

5. Jalankan Scanning SCAP dengan Profil ANSSI BP28 Minimal
```
   sudo oscap xccdf eval \
       --profile  xccdf_org.ssgproject.content_profile_anssi_bp28_minimal \
       --report /tmp/anssi_bp28_minimal_report.html \
       /usr/share/xml/scap/ssg/content/ssg-ol9-ds.xml
```

<br>

6. Konfigurasi parameter keamanan terkait password dan autentikasi

   - Mengatur kompleksitas dan panjang minimal password /etc/security/pwquality.conf
```
	dcredit = -1
	lcredit = -1
	minlen = 16
	ocredit = -1
	ucredit = -1
	retry=3
	minclass=4
	rounds=65536
```
   - Menerapkan kebijakan penguncian akun setelah gagal login /etc/security/faillock.conf
```
	deny = 3
	even_deny_root
	fail_interval = 900
	unlock_time = 900
```
   - Menentukan jumlah histori password yang tidak boleh digunakan ulang /etc/security/pwhistory.conf
```
	remember = 2
```

<br>

7. Generate Skrip Remediasi Berdasarkan Laporan HTML dan XML
```
sudo oscap xccdf generate fix \
       --fix-type bash \
       --output /tmp/anssi_bp28_remediation.sh \
       /tmp/anssi_bp28_minimal_report.html

<br>

sudo oscap xccdf generate fix \
       --fix-type bash \
       --output /tmp/anssi_bp28_remediation.sh \
       /tmp/anssi_bp28_minimal_report.xml

```

<br>

8. Hapus File .sh di Direktori /home/pgnusr
```
rm -f /home/pgnusr/*.sh
```

<br>

9. Scanning untuk spesifik aturan password saja
```
oscap xccdf eval --profile xccdf_org.ssgproject.content_profile_anssi_bp28_minimal --rule xccdf_org.ssgproject.content_rule_accounts_password_pam_minlen --rule xccdf_org.ssgproject.content_rule_accounts_password_set_max_life_root --report /tmp/anssi_bp28_password.html /usr/share/xml/scap/ssg/content/ssg-ol9-ds.xml
```


