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
cd
```

```
cd inery-node/inery.setup
```
```
cd tools
```
```
nano config.json
```
**Cari kata kata ini**

**"MASTER_ACCOUNT":
{
    "NAME": "AccountName",
    "PUBLIC_KEY": "PublicKey",
    "PRIVATE_KEY": "PrivateKey",
    "PEER_ADDRESS": "IP:9010",
    "HTTP_ADDRESS": "0.0.0.0:8888",
    "HOST_ADDRESS": "0.0.0.0:9010"**

Kemudian ganti account name, publickey, privatekey, ip (sesuai kan dengan yang ada di web testnetnya)
untuk mengedit kalian bisa mengarahkan keyboard panah kebawah

Jika sudah langsung Simpan (CTRL+X), Ketik "Y" dan (enter)

## 6. Running Node

```
cd
```

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

### Note : Untuk melanjutkan perintah dibawah ini pastikan node kalian sinkron atau nunggu 1 hari setelah running node

## 7. Menghubungkan Wallet dengan Dasboard Akun

```
cline wallet create -n namawallet -f file.txt
```
**namawalet ganti sesuai nama akun yang di web testnet inery**

```
nano file.txt
```
**salin dan simpan isi yang ada di dalam file.txt karna ini password wallet kalian**

```
cline wallet import --private-key privatekey -n namawallet
```
**privatekey ganti pake yang di web testnetnya**

### Register Master Node :

```
cline system regproducer namaakun publikey 0.0.0.0:9010
```
**namaakun & publikey ganti pake yang dari web testnetnya**

```
cline system makeprod approve namaakkun namaakun
```
**namaakun ganti samain kek yang tadi**

**Done. pendaftaran berhasil bisa cek disini: https://explorer.inery.io/ atau pake ini** ```cline system listproducers```

# Perintah Berguna (perintah ini hanya untuk nambah pengetahuan kalian)

## Check Saldo Wallet 
```
cline get currency balance inery.token namaakun
```
**namaakun ganti pake yang tadi dibuat**

## Check List Screen
```
screen -ls
```
## Kembali ke Screen
```
screen -rd inery
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
