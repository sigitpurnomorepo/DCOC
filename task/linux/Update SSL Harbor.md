### 1. Mencari Directory Tempat SSL
```bash
docker inspect nginx --format '{{range .Mounts}}{{println .Source "->" .Destination}}{{end}}'
```

![Mount Volume Nginx](https://github.com/user-attachments/assets/d2cb0064-9c98-42bd-8ece-c059a8e43bb3)

![Detail Path Sertifikat](https://github.com/user-attachments/assets/95485fab-296a-4c27-86f9-afea36bb5081)

---

### 2. Mengecek Detail File SSL

**Cek SSL langsung via Endpoint Domain:**
```bash
openssl s_client -connect localhost:443 -servername registry.pgn.co.id </dev/null 2>/dev/null | openssl x509 -noout -dates -subject -issuer
```

![Hasil Cek Endpoint SSL](https://github.com/user-attachments/assets/0bbaf35e-6e7e-4bb1-8737-e061b59d20f2)

**Cek sertifikat langsung dari File CRT Host:**
```bash
openssl x509 -in /data/secret/cert/server.crt -noout -subject -issuer -dates
```

![Hasil Cek File CRT](https://github.com/user-attachments/assets/626dee85-362f-4590-931c-19d93f67efe5)

---

### 3. Reload Service Nginx Dalam Container
```bash
docker exec nginx nginx -s reload
```

---

### 4. Result
![Isi Direktori SSL](https://github.com/user-attachments/assets/af78b403-49d5-447e-9148-fb67a9270546)
