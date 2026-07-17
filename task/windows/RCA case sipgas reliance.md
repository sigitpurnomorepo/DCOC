## RCA case sipgas dan database reliance
```
Isu Trouble : 
- Koneksi dari 10.129.18.24 ke arah scada untuk database reliance tidak terkoneksi
- IP 10.129.18.24 (vm) telnet ke DB scada 10.40.43.124/10.40.43.16, 10.40.42.9 dengan port 1433 tidak bisa,
menyebabkan data dari scada reliance tidak tertarik ke sipgas menyebabkan realisasi station yang menggunakan reliance kosong semua

Action dari sisi Infrastruktur IT : 
1. Dilakukan pengecekan dari sisi firewall ICT policy: status normal dikarenakan tidak terdapat perubahan 
2. Dari Router HQ: routing tidak ada perubahan serta di ping status reply
3. Server 10.129.18.24 tidak mengalami hang, karena sebelum dilakukan restart, masih bisa diakses oleh tim DCOC melalui Paman
4. Koneksi dari segment lain termontor normal

Action dari sisi Infrastruktur OT : 
1. dilakukan open all service tetapi servce db masih belum bisa terkoneksi
2. dilakukan pengecekan pada firewall OT dilakukan restart service tetapi masih belum bisa terkoneksi

Solved after : 
Dilakukan restart pada server VM-HQ-OPC-1 10.129.18.24
Setelah server selesai restart, dilakukan pengujian ulang dan koneksi dari VM-HQ-OPC-1 10.129.18.24 ke VM DB Scada 10.129.43.16:1433 berhasil, 
sehingga aplikasi kembali dapat mengakses database dengan normal

Analisis Penyebab (Root Cause):
Sistem mengalami TCP Port Exhaustion pada port 1433 akibat akumulasi koneksi stale (status TIME_WAIT atau CLOSE_WAIT) yang tidak terlepas dengan sempurna.
Server menerapkan Windows Firewall Policy yang dikelola terpusat melalui GPO Domain (terkonfirmasi via RSOP pada PolicyStore: GPO).
Terdapat indikasi bahwa filtering engine (WFP) mengalami beban kerja tinggi saat memproses aturan firewall yang kompleks, 
diperkuat dengan keberadaan Kaspersky Endpoint Security yang terintegrasi pada level network filtering (WFP) OS. 
Hal ini memicu respons protektif dari sistem berupa pemblokiran trafik spesifik ke segmen DB tersebut untuk menjaga stabilitas sistem.

Rencana Tindakan Lanjutan (Next Action Plan):
Identifikasi Anomali Koneksi: Menjalankan netstat -ano | findstr :1433 untuk memverifikasi penumpukan stale connection sebelum melakukan restart.
Audit Filter & Proteksi: Menjalankan netsh wfp show filters untuk menganalisis apakah terdapat block rule spesifik. 
Selain itu, tim akan melakukan investigasi pada log Kaspersky Endpoint Security untuk memastikan tidak ada Network Attack Blocker atau 
Firewall Module yang secara otomatis memblokir IP DB saat mendeteksi pola port exhaustion.
```
