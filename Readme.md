Node setup for the Fractal Bitcoin project, which is supported by mighty Binance and will launch its mainnet in September 9th, 2024.

## What is Fractal Bitcoin?

Fractal Bitcoin is the only Bitcoin scaling solution that uses the Bitcoin Core code to iteratively scale infinite layers. This is the world's first virtualization method applied to Bitcoin. Fractal gradually expands the Bitcoin blockchain into a scalable computing system without compromising the consistency of the main Bitcoin chain. Building on Fractal is quite simple with powerful tools and support.

**Youtube** : https://www.youtube.com/@cryptoconsole

**Follow X** : https://x.com/cryptoconsol

**Join TG** : https://t.me/cryptoconsol


### Requirements

| Requirement                  | Description                         |
|------------------------------|-------------------------------------|
| Operating System             | Ubuntu 22.04 or 24.04               |
| Memory (RAM)                 | Minimum 4 GB                        |
| Disk Space                   | Minimum 100 GB of free disk space   |

## Installation

**Note: There are no incentives for running a node. Please proceed with the installation knowing this.**

1. **Install Packages:**

```shell
sudo apt update && sudo apt upgrade -y
sudo apt install curl build-essential pkg-config libssl-dev git wget jq make gcc chrony -y
```

## Node Installation

1. **Download the Fractal Repository:**

```shell
wget https://github.com/fractal-bitcoin/fractald-release/releases/download/v0.1.8/fractald-0.1.8-x86_64-linux-gnu.tar.gz
```

2. **Extract the File:**

```shell
tar -zxvf fractald-0.1.8-x86_64-linux-gnu.tar.gz
```

3. **Create the Data Folder:**

```shell
cd fractald-0.1.8-x86_64-linux-gnu && mkdir data
```

4. **Copy the Configuration File:**

```shell
cp ./bitcoin.conf ./data
```

5. **Create a Service:**

```shell
sudo tee /etc/systemd/system/fractald.service > /dev/null <<EOF
[Unit]
Description=Fractal Node
After=network.target

[Service]
User=root
WorkingDirectory=/root/fractald-0.1.8-x86_64-linux-gnu
ExecStart=/root/fractald-0.1.8-x86_64-linux-gnu/bin/bitcoind -datadir=/root/fractald-0.1.8-x86_64-linux-gnu/data/ -maxtipage=504576000
Restart=always
RestartSec=3
LimitNOFILE=infinity

[Install]
WantedBy=multi-user.target
EOF
```

```shell
sudo systemctl daemon-reload && \
sudo systemctl enable fractald && \
sudo systemctl start fractald
```

6. **Log Check**

```bash
sudo journalctl -u fractald -fo cat
```

### 7. Create a Wallet

Create a wallet by running the following commands sequentially:

```shell
cd /root/fractald-0.1.8-x86_64-linux-gnu/bin
./bitcoin-wallet -wallet=wallet -legacy create
```

8. **Get the Wallet Private Key:**

```shell
cd /root/fractald-0.1.8-x86_64-linux-gnu/bin
./bitcoin-wallet -wallet=/root/.bitcoin/wallets/wallet/wallet.dat -dumpfile=/root/.bitcoin/wallets/wallet/MyPK.dat dump
cd && awk -F 'checksum,' '/checksum/ {print "Your Wallet Private Key:" $2}' .bitcoin/wallets/wallet/MyPK.dat
```
**Unisat Wallet** : https://chromewebstore.google.com/detail/unisat-wallet/ppbibelpcjmhbdihakflkdcoccbgbkpo?pli=1

**Testnet task guide** : https://x.com/cryptoconsol/status/1831026404873601155

**Fractal Explorer** : https://explorer.fractalbitcoin.io/
