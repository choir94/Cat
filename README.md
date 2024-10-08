<h2 align=center>Mint first CAT20 token CAT on Fractal Mainnet</h2>

- Install Docker
```bash
sudo apt update && sudo apt install -y curl && curl -fsSL https://get.docker.com -o get-docker.sh && sudo sh get-docker.sh
```
- Install Docker Compose
```bash
sudo curl -L "https://github.com/docker/compose/releases/download/$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
- Eksekusi
```bash
sudo chmod +x /usr/local/bin/docker-compose
```
- Install `npm`
```bash
sudo apt-get install npm -y
```
- Install `n` pacakges globally
```bash
sudo npm i n -g
```
- stable node version
```bash
sudo n stable
```
- Install `yarn` package globally
```bash
sudo npm i -g yarn
```
- Clone `Cat Protocol` repo
```bash
git clone https://github.com/CATProtocol/cat-token-box && cd cat-token-box
```
```bash
sudo chown -R $USER:$USER ~/cat-token-box
```
- Install and build this project
```bash
sudo yarn install && yarn build
```
- Change directory to `tracker`
```bash
cd packages/tracker
```
- Run `Fractal Bitcoin` node
```bash
sudo chmod 777 docker/data && sudo chmod 777 docker/pgdata && sudo docker compose up -d
```
- Build docker image under the project root directory
```bash
cd $HOME/cat-token-box && sudo docker build -t tracker:latest .
```
- Run the container
```bash
sudo docker run -d \
    --name tracker \
    --add-host="host.docker.internal:host-gateway" \
    -e DATABASE_HOST="host.docker.internal" \
    -e RPC_HOST="host.docker.internal" \
    -p 3000:3000 \
    tracker:latest
```
- Change directory
```bash
cd $HOME/cat-token-box/packages/cli
```
- Gunakan perintah di bawah ini untuk membuat file config.json menggunakan data di bawah ini Anda dapat mengubah nama pengguna dan kata sandi
```bash
cat <<EOF > config.json
{
  "network": "fractal-mainnet",
  "tracker": "http://127.0.0.1:3000",
  "dataDir": ".",
  "maxFeeRate": 30,
  "rpc": {
      "url": "http://127.0.0.1:8332",
      "username": "bitcoin",
      "password": "opcatAwesome"
  }
}
EOF
```
- Buat wallet baru
```bash
sudo yarn cli wallet create
```
** atau jika ingin import wallet btc mnemonic**
```bash
cat <<EOF > wallet.json
{
  "accountPath": "m/86'/0'/0'/0/0",
  "name": "cat-5d0fe77c",
  "mnemonic": "YOUR TAPROOT ADDRESS MNEMONIC PHRASE"
}
EOF
```
- cek wallet
```bash
sudo yarn cli wallet address
```
- Sekarang Anda harus memiliki $FB untuk membuat token CAT, jadi untuk mendapatkan $FB , impor dulu frase seed ini ke dalam [Unisat Wallet](https://chrome.google.com/webstore/detail/unisat/ppbibelpcjmhbdihakflkdcoccbgbkpo) , selama mengimpor pilih `taproot` dan Anda akan mendapatkan alamat yang dimulai dengan `bc1p.......`
- Isi beberapa FB di wallet
- Sekarang tunggu hingga pelacak Anda disinkronkan dengan blok terbaru, Anda dapat menggunakan perintah ini untuk memeriksa status sinkronisasi
```bash
sudo yarn cli wallet balances
```
- jika 100%, setelah itu Anda dapat mencetak token CAT

![image](https://github.com/user-attachments/assets/4abfd1d1-b1fb-461c-89a4-7788db9c88c1)

- Gunakan perintah ini untuk menginstal curl dan jq`
```bash
dpkg -l | grep -q '^ii  curl ' || sudo apt-get install -y curl && dpkg -l | grep -q '^ii  jq ' || sudo apt-get install -y jq
```
- Mint pakai fee market saat ini
```bash
sudo yarn cli mint -i 45ee725c2c5993b3e4d308842d87e973bf1951f5f7a804b21e4dd964ecd12d6b_0 5 --fee-rate $(curl -s https://explorer.unisat.io/fractal-mainnet/api/bitcoin-info/fee | jq '.data.economyFee')
```
- Cek saldo
```bash
sudo yarn cli wallet balances
```
- Done ✅
## Diskusi Group
- Join Channel telegram: [AirdropNode](https://t.me/airdrop_node)
