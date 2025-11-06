### Install Sophos 
1. Download Sophos
```bash
wget https://api-cloudstation-us-east-2.prod.hydra.sophos.com/api/download/56cfc53f70a5983de1a180ff106e9ce1/SophosSetup.sh
```
2. Enable permission to execute
```bash
chmod 754 SophosSetup.sh
```
3. Install Sophos
```bash
./SophosSetup.sh
```
4. Cek apakah asset vm sudah ada di Sophos Central

<br>

### Install GLPI
1. Copy file glpi to server

2. Enable permission to execute
```bash
chmod 754 glpi-agent-1.15-x86_64.AppImage
```
3. Install GLPI
```bash
./glpi-agent-1.15-x86_64.AppImage --install --server http://10.129.2.174/plugins/glpiinventory
```
4. Cek asset vm di comit.pgn.co.id
