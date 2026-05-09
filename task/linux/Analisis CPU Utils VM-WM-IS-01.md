- Cek resource utils realtime 1 second
```
  sar 1
```

- Cek proses CPU utils realtime
```
  top

  P
```

- Cek proses CPU tertinggi 
```
  ps aux --sort=-%cpu | head
```

- Cek detail proses berdasarkan PID
```
  ps -fp 647753
```

- Cek command full proses
```
  cat /proc/647753/cmdline | tr '\0' ' '
```

- Cek executable asli
```
  ls -l /proc/647753/exe
```

- Cek working directory
```
  ls -l /proc/647753/cwd
```

- Cek environment variable
```
  cat /proc/647753/environ | tr '\0' '\n'
```

- Cek resource utils realtime 1 second
```
  pstree -p 647753
  atau
  pstree -p | grep 647753
```

- Cek file yang dibuka selama proses
```
  lsof -p 647753

  lsof -p 647753 | tail -n 20

  lsof -p 647753 | grep TCP

  lsof -p 647753 | grep log

  lsof -p 647753 | grep deleted
```

- Cek port yang digunakan oleh proses
```
  ss -plant | grep 647753
```

- Cek detail thread CPU tertinggi 
```
  top -Hp 647753
```

- Cek semua info status proses
```
  cat /proc/647753/status
```

### Untuk kasus Java
- Thread CPU
  ```
  top -Hp 647753
  ```

- Thread dump
  ```
  jstack 647753
  ```

- GC monitoring
  ```
  jstat -gcutil 647753 1000
  ```

