<p style="font-size:14px" align="right">

</p>

<p align="center">
  <img height="50" height="auto" src="https://user-images.githubusercontent.com/38981255/184088981-3f7376ae-7039-4915-98f5-16c3637ccea3.PNG">
</p>

# Tutorial Become a Master Node

Dokumen Official :
> [Node Lite & Master](https://docs.inery.io/docs/category/lite--master-nodes)

Explorer :
> [Explorer Inary](https://explorer.inery.io/ "Explorer Inary")

## Spek VPS

|  Komponen |  Persyaratan Minimum |
| ------------ | ------------ |
| CPU  | Intel Core i7-8700 Hexa-Core  |
| RAM | 8 GB  |
| Penyimpanan  | 2x1 TB NVMe SSD |
| koneksi | Port 1 Gbit/dtk |

## 1. Update Tools Yang di Perlukan

```
sudo apt-get update && sudo apt install git && sudo apt install screen
```

```
sudo apt-get install -y make bzip2 automake libbz2-dev libssl-dev doxygen graphviz libgmp3-dev \
autotools-dev libicu-dev python2.7 python2.7-dev python3 python3-dev \
autoconf libtool curl zlib1g-dev sudo ruby libusb-1.0-0-dev \
libcurl4-gnutls-dev pkg-config patch llvm-7-dev clang-7 vim-common jq libncurses5
```
## 2. Open Firewall
```
ufw allow 22 && ufw allow 8888 && ufw allow 9010 && ufw enable
```
## 3. Start Node

```
git clone https://github.com/inery-blockchain/inery-node
```

## 4. Unlock Access

<p align="center">
  <img height="auto" height="auto" src="https://user-images.githubusercontent.com/38981255/184288914-bcea524f-d32e-4460-a971-913af8c359a9.PNG">
</p>

```
cd inery-node
```
```
cd inery.setup
```
```
chmod +x ine.py
```
```
./ine.py --export
```
```
cd; source .bashrc; cd -
```
## 5. Konfigurasi Master Node

```
cd inery-node/inery.setup
```
```
cd tools
```
```
nano config.json
```
Cari kata kata ini

"MASTER_ACCOUNT":
{
    "NAME": "AccountName",
    "PUBLIC_KEY": "PublicKey",
    "PRIVATE_KEY": "PrivateKey",
    "PEER_ADDRESS": "IP:9010",
    "HTTP_ADDRESS": "0.0.0.0:8888",
    "HOST_ADDRESS": "0.0.0.0:9010"

Kemudian ganti account name, publickey, privatekey, ip (sesuai kan dengan yang ada di web testnetnya)

Jika sudah langsung Simpan (ctrl+x), Ketik "Y" dan (enter)

## 6. Running Node

```
cd inery-node/inery.setup
```
```
screen -S inery
```
```
./ine.py --master
```
**Ketik CTRL + A + D** Untuk jalan di Background dan Untuk Kembali lagi Ke Screen Gunakan Perintah `screen -rd inery`

<p align="center">
  <img height="auto" height="auto" src="https://user-images.githubusercontent.com/38981255/184290965-fd0f6127-d351-4f55-9102-18aa1bbb38c2.PNG">
</p>

### Jika Menunjukan Seperti di Atas, Anda Harus Mengganti Peer di, Gunakan Perintah (Lakukan di TAB Baru)
```
cd inery-node/inery.setup/master.node/
nano genesis_start.sh
```

Save CTRL X lalu Y dan Enter
## 7. Add Peer baru
<p align="center">
  <img height="auto" height="auto" src="https://user-images.githubusercontent.com/38981255/184370626-5b3dc227-3800-4140-a9c0-ce5b0b13e1e1.PNG">
</p>

**Isi Seperti Pada Contoh Gambar**

- 62.210.245.223
- 192.99.62.6
- 15.235.133.9

## 8. Masukan Peer
```
--p2p-peer-address 167.235.3.147:9010 \
--p2p-peer-address 135.181.133.169:9010 \
--p2p-peer-address 15.235.133.9:9010 \
--p2p-peer-address 38.242.229.50:9010 \
--p2p-peer-address sys.blockchain-servers.world:9010 \
--p2p-peer-address bis.blockchain-servers.world:9010 \
--p2p-peer-address 167.235.71.28:9010 \
--p2p-peer-address 62.210.245.223:9010 \
--p2p-peer-address 192.99.62.6:9010 \
--p2p-peer-address 15.235.133.9:9010 \
--p2p-peer-address 5.161.96.50:9010 \
--p2p-peer-address 15.235.133.9:9010 \
```

## 9. Restart Node
```
./stop.sh
```

Tunggu Sekitar 5-10 Detik

```
./genesis_start.sh
```

<p align="center">
  <img height="auto" height="auto" src="https://user-images.githubusercontent.com/38981255/184370620-b73f5269-50ad-47aa-9b03-d55d8718c614.PNG">
</p>

Jika Sudah Seperti Gambar di Atas, Artinya Sudah jalan dan Tunggu Sampai 1 - 2 Jam Untuk Mensinkronkan (Ngejar Block Yang Ada di Explorer) `JADI KUDU SABAR SIRR..`

<p align="center">
  <img height="auto" height="auto" src="https://user-images.githubusercontent.com/38981255/184388159-4b0ebd21-8b4e-4f28-a10f-03b1626db075.PNG">
</p>

Jika Sudah Seperti gambar di atas, Artilnya Sudah Selesai Sinkron, Silahkan Lanjut Next Step

## 10. Start Node
### Lakukan Ini Masih di TAB Baru
```
cd ~/inery-node/inery.setup/master.node/
./start.sh
```
## 11. Menghubungkan Wallet dengan Dasboard Akun

### Lakukan Ini Masih di TAB Baru

```
cline wallet create -n namawallet -f file.txt
```
namawalet ganti bang bebas

file.txt berisi Password Wallet kalian (Kalian membutuhkan itu Jika Wallet kalian dalam Keadaan Lock)
```
cline wallet import --private-key privatekey -n namawallet
```
privatekey pake yang di web testnetnya

### Register Master Node :

```
cline system regproducer namaakun publikey 0.0.0.0:9010
```
namaakun ganti bang bebas & publikey pake yang dari web testnetnya

```
cline system makeprod approve namaakkun namaakun
```
namaakun ganti samain kek yang tadi

**Done** pendaftaran berhasil bisa cek disini: https://explorer.inery.io/

# Perintah Berguna 

## Check Saldo Wallet 
```
cline get currency balance inery.token ACCOUNT_NAME
```
## Delete Wallet di Node
```
cline wallet stop
```
```
rm -rf inery-wallet
rm -rf file.txt
rm -rf defaultWallet.txt
```
