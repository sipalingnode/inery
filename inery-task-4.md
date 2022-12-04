# INERY TASK 4
## Install NodeJS
```
sudo apt-get remove nodejs
```
```
sudo apt-get install curl
```
```
curl -fsSL https://deb.nodesource.com/setup_19.x | sudo -E bash - &&\
sudo apt-get install -y nodejs
```
## Clone Repository
```
git clone https://github.com/alteregogi/ineryjs.git
```
```
cd ineryjs
```
```
npm install
```
```
cp .env-sample .env
```
## Edit File .env
```
nano .env
```
| INERY_ACCOUNT  | Nama Akun yang diweb  |
| ------------ | ------------ |
| PRIVATE_KEY | Private Key yang diweb |
| YOUR_NODE_URL  | IP VPS kalian |

**Jika sudah langsung `CTRL+XY lalu enter` untuk save file nya**
## Check Ouput (jika berhasil tampilan akan seperti dibawah ini)
```
{
  transaction_id: '8a58f296e11f2xxxxxxxxxxxx3f639658f9a0dcca8cfa7194b57d946af5',
  processed: {
    id: '8a58f296e11f29153xxxxxxxxxxxxdcca8cfa7194b57d946af5',
    block_num: 1204983,
    block_time: '2022-12-03T22:25:04.500',
    receipt: { status: 'executed', cpu_usage_us: 1354, net_usage_words: 18 },
    elapsed: 1354,
    net_usage: 144,
    scheduled: false,
    action_traces: [ [Object] ],
    failed_dtrx_trace: null
  }
}
```
**Langsung ke web Inery Testnetnya Lalu Klik Finish di Task 4 Nya dan Tunggu Hasil Review**

Thanks for alteregogi
