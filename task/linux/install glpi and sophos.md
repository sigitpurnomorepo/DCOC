# Install Sophos 
## 1. Download Sophos
wget https://api-cloudstation-us-east-2.prod.hydra.sophos.com/api/download/56cfc53f70a5983de1a180ff106e9ce1/SophosSetup.sh

## 2. Enable permission to execute
chmod 754 SophosSetup.sh

## 3. Install Sophos
./SophosSetup.sh

## Cek apakah asset vm sudah ada di Sophos Central



# Install GLPI
## 1. Copy file glpi to server

## 2. Enable permission to execute
chmod 754 glpi-agent-1.15-x86_64.AppImage

## 3. Install GLPI
./glpi-agent-1.15-x86_64.AppImage --install --server http://10.129.2.174/plugins/glpiinventory

## Cek asset vm di comit.phn.co.id
