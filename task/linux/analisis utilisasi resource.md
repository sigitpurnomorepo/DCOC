## Analisis hasil top 
<img width="518" height="62" alt="image" src="https://github.com/user-attachments/assets/953fb91b-32a3-4452-9d29-faa60c5a0498" /> 
<br>
<img width="770" height="455" alt="image" src="https://github.com/user-attachments/assets/ac50cd80-f3f5-4d88-a5b5-4ee368734500" />




## Analisis Utilisasi CPU

- Lihat history CPU hari ini
```
sar -u
```

- Lihat history CPU tanggal tertentu (misal 5 April 2026)
```
sar -u -f /var/log/sa/sa05
```

- Lihat dengan interval & periode tertentu
```
sar -u -s 08:00:00 -e 12:00:00 -f /var/log/sa/sa05
```

<img width="731" height="300" alt="image" src="https://github.com/user-attachments/assets/a341e859-b42b-4e07-ac03-50d4cd992a9e" />

- Lihat proses terbesar dari CPU
```
ps aux --sort=-%cpu | head
```

- Lihat user pemakai dari CPU
```
ps -eo user,%cpu --sort=-%cpu | head
```

- Lihat user total pemakaian dari CPU
```
ps -eo user,%cpu --no-headers | \
awk '{cpu[$1]+=$2} END {for (u in cpu) print u, cpu[u]}' | \
sort -k2 -nr
```

## Analisis Utilisasi Memory

- Lihat history CPU hari ini
```
sar -u
```

- Lihat history CPU tanggal tertentu (misal 5 April 2026)
```
sar -u -f /var/log/sa/sa05
```

- Lihat dengan interval & periode tertentu
```
sar -u -s 08:00:00 -e 12:00:00 -f /var/log/sa/sa05
```

<img width="545" height="29" alt="image" src="https://github.com/user-attachments/assets/ab261cd4-1af5-47e4-b252-6492cfde89cc" />


<img width="731" height="300" alt="image" src="https://github.com/user-attachments/assets/a341e859-b42b-4e07-ac03-50d4cd992a9e" />
<img width="1895" height="582" alt="image" src="https://github.com/user-attachments/assets/01793b06-c608-4c7f-8bda-c7c3588a36a5" />

```
free -h
```

<img width="642" height="66" alt="image" src="https://github.com/user-attachments/assets/51c79136-4166-4bfb-91cf-ecc2958e2b0a" />

```
ps aux --sort=-%mem | head -10
```

<img width="1035" height="190" alt="image" src="https://github.com/user-attachments/assets/85527eb4-134d-47e0-8c2c-1d4a0a46523d" />
<img width="767" height="573" alt="image" src="https://github.com/user-attachments/assets/5d800ca5-2572-40f1-80a2-21a5e6be1248" />
<img width="750" height="786" alt="image" src="https://github.com/user-attachments/assets/5e75fe57-f1a5-4747-a0c7-10525a021de9" />
<img width="727" height="292" alt="image" src="https://github.com/user-attachments/assets/55fe9161-2c4d-4aad-a304-ac27aa7f8f83" />



```
journalctl --since "2026-04-13 18:00:00" --until "2026-04-12 18:40:00" \
  -k | grep -iE "oom|memory|killed|error"
```

<img width="1495" height="227" alt="image" src="https://github.com/user-attachments/assets/7ccd2f19-0784-42eb-a565-5c0221fc9990" />
<img width="755" height="775" alt="image" src="https://github.com/user-attachments/assets/2c26a2e9-bc05-42da-af48-2ecdbc02abe9" />
<img width="754" height="621" alt="image" src="https://github.com/user-attachments/assets/7e7a4415-4c0d-4fef-a9a9-243997516afb" />
<img width="759" height="749" alt="image" src="https://github.com/user-attachments/assets/5e65824e-7f77-4468-b367-6c46a074b7da" />
<img width="698" height="218" alt="image" src="https://github.com/user-attachments/assets/0d2470dd-2fa3-49ee-9fb3-386fe3601a84" />






