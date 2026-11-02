


Mencari dir tempat ssl
```
docker inspect nginx --format '{{range .Mounts}}{{println .Source "->" .Destination}}{{end}}'
```
<img width="1123" height="234" alt="image" src="https://github.com/user-attachments/assets/d2cb0064-9c98-42bd-8ece-c059a8e43bb3" />

<img width="528" height="174" alt="image" src="https://github.com/user-attachments/assets/95485fab-296a-4c27-86f9-afea36bb5081" />

<img width="1254" height="906" alt="image" src="https://github.com/user-attachments/assets/af78b403-49d5-447e-9148-fb67a9270546" />
<br />
Mengecek detail file ssl <br />
`openssl s_client -connect localhost:443 -servername registry.pgn.co.id </dev/null 2>/dev/null | openssl x509 -noout -dates -subject -issuer`
<br />
<img width="400" height="51" alt="image" src="https://github.com/user-attachments/assets/0bbaf35e-6e7e-4bb1-8737-e061b59d20f2" />
<br />
```
openssl x509 -in /data/secret/cert/server.crt -noout -subject -issuer -dates
```
<br />
<img width="419" height="51" alt="image" src="https://github.com/user-attachments/assets/626dee85-362f-4590-931c-19d93f67efe5" />
<br /><br />
Reload service nginx dalam container
```docker exec nginx nginx -s reload```




