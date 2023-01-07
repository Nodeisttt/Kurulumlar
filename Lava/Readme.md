<p align="center">
  <img height="100" height="auto" src="https://raw.githubusercontent.com/Nodeist/Kurulumlar/main/logos/lava.png">
</p>



# Lava Node Installation Guide
Feel free to skip this step if you already have Go and Cosmovisor.


## Install Go
We will use Go `v1.19.3` as example here. The code below also cleanly removes any previous Go installation.

```
sudo rm -rvf /usr/local/go/
wget https://golang.org/dl/go1.19.3.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.19.3.linux-amd64.tar.gz
rm go1.19.3.linux-amd64.tar.gz
```

### Configure Go
Unless you want to configure in a non-standard way, then set these in the `~/.profile` file.

```
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export GO111MODULE=on
export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin
```


### Install Cosmovisor
We will use Cosmovisor `v1.0.0` as example here.

```
go install github.com/cosmos/cosmos-sdk/cosmovisor/cmd/cosmovisor@v1.0.0
```

## Install Node
Install the current version of node binary.

```
cd $HOME
git clone https://github.com/K433QLtr6RA9ExEq/GHFkqmTzpdNLDd6T.git
wget https://lava-binary-upgrades.s3.amazonaws.com/testnet/v0.4.0/lavad
chmod +x lavad
mv lavad $HOME/go/bin/
```

## Configure Node
### Initialize Node
Please replace `MONIKERNAME` with your own moniker.

```
lavad init MONIKERNAME --chain-id lava-testnet-1
```

### Download Genesis
The genesis file link below is Nodeist's mirror download. The best practice is to find the official genesis download link.

```
wget -O genesis.json https://snapshots.nodeist.net/t/lava/genesis.json --inet4-only
mv genesis.json ~/.lava/config
```

### Configure Peers
Here is a script for you to update `persistent_peers` setting with these peers in `config.toml`.
```
PEERS=fe1998168f5336811a79fbcaf2d5d5a69f2f9f63@65.108.81.145:26656,80817a529fb8603d9def917120e5f3e684157416@5.75.235.206:26656,daa11ae80a2fecde611054b6ca83453462878d9e@65.108.65.246:30656,2c2353c872b0c5af562c518b1aa48a2649a4c927@65.108.199.62:11656,4f9120f706512162fbe4f39aac78b9924efbec58@65.109.92.235:11036,f9190a58670c07f8202abfd9b5b14187b18d755b@144.76.97.251:27656,f120685de6785d8ee0eadfca42407c6e10593e74@144.76.90.130:32656,6641a193a7004447c1b49b8ffb37a90682ce0fb9@65.108.78.116:13656,c19965fe8a1ea3391d61d09cf589bca0781d29fd@162.19.217.52:26656,0516c4d11552b334a683bdb4410fa22ef7e3f8ba@65.21.239.60:11656,72aabf4950afe5f2514cff8dc6c2c56600e7ed03@34.251.254.15:26656,24a2bb2d06343b0f74ed0a6dc1d409ce0d996451@188.40.98.169:27656,c80f5f3b6828342ed2c38026eede1f59b466d30f@168.119.124.130:47656,c678ae0fd7b754615e55bba2589a86e60fc8d45c@136.243.88.91:7140,a65de5f01394199366c182a18d718c9e3ef7f981@159.148.146.132:26656,cc2b2250b21cd6d23305143a32181e5f6bfc5956@135.181.50.187:26656,2031e65ee8a13e57d922a14d28d67be0ada21a95@54.194.240.43:26656,3a445bfdbe2d0c8ee82461633aa3af31bc2b4dc0@3.252.219.158:26656,3c47fd1662bcb17a4713c23e41d7b25e34478b8e@103.19.25.157:26672,131227f65bbc8f5b86030124fa1610a3283ebcbd@135.181.176.109:26656,5c2a752c9b1952dbed075c56c600c3a79b58c395@185.16.39.172:27066,5a469a75fb05eddf2d79fb17063cc59e84d0821a@207.180.236.115:34656,0314d53cc790860fb51f36ac656a19789800ce5c@176.103.222.20:26656,14ae45e7f2ff7491cfa686a8fcac7cc095bc38ff@213.239.217.52:39656,28db9a9c200bedbe5d322f7571462f1146ef898e@209.126.2.184:26656,de764d94d3eed3ac15c2151b5576dd24de5bec81@38.242.236.179:26656,57474bd0977b3ed65cf23086b6d1d92bf00d50d0@207.180.236.122:31656,433be6210ad6350bebebad68ec50d3e0d90cb305@217.13.223.167:60856,f22ea1e7b6d31966259e99177d714cffde27c4bf@152.32.211.182:26656,024a0b0a6eae16a2e8aaefcf26b12d2a3b393b28@75.119.155.60:26656,2db2e00432fc950fa2afa03a84288a437fc1c305@2.58.82.212:26656,9a8477637f7944f2537234bbfb6e1559b7805157@195.3.221.13:56656,0a528da95ca8025ef4043b6e73f1e789f4102940@176.103.222.22:26656,90451ff8f47b8f4b077e95837f112135fea14531@207.180.231.123:31656,529675163b5d16838928fe10edce5ef827ff591f@46.4.68.113:25556,f80ab02da4448f7c2dfa450fb2f1501bd1a4f2af@109.123.241.78:26656,3b5712480860dc84adc17a007bab21a7cb14404b@65.108.97.58:26656,464e98fa27165f3a13f4173c0ecfbe71ce8f1bf2@167.86.94.71:36656,897fbd850aff33b4d5012d30a8b0ce04225f907f@2.58.82.231:26656,d80e5374ff2192353edfcebc6111710e248164dc@5.161.145.147:26656,151cc6fb6d1a4a4c2f76f7eaf43b9ea80d62ec7b@95.214.55.46:22626,bb8c8cea499a1fa7e97922b5a9882c2360c6575a@176.103.222.21:26656,e4ebf07ed08ff8ee26a9a903d63ad34d1f59393e@95.217.35.186:56656,41394b7c876d2426969c6f10a3400d7c57271130@38.242.253.207:26656,b2a3ee7b6ccef717f45f0dfaa7e832d9c6beb6ef@65.109.164.87:26656,10b0118f5c1264ac7b9f45931717fef401530867@178.54.78.180:36656,a76af03d79a90992d135750ab945f79f167d6ee4@65.109.139.182:26656,2b5d760125c90970ce27f4783a5d70a19534ff61@146.19.24.101:26546,6b1d0465b3e2a32b5328e59eb75c38d88233b56f@80.82.215.19:60656,34c664ce161789d556e5ab84115975f9229b4430@161.97.91.203:26656
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.lava/config/config.toml
```

## Launch Node
### Configure Cosmovisor Folder
Create Cosmovisor folders and load the node binary.

```
# Create Cosmovisor Folders
mkdir -p ~/.lava/cosmovisor/genesis/bin
mkdir -p ~/.lava/cosmovisor/upgrades

# Load Node Binary into Cosmovisor Folder
cp ~/go/bin/lavad ~/.lava/cosmovisor/genesis/bin
```

### Create Service File
Create a `lavad.service` file in the `/etc/systemd/system` folder with the following code snippet. Make sure to replace `USER` with your Linux user name. You need `sudo` previlege to do this step.

```
[Unit]
Description="lavad node"
After=network-online.target

[Service]
User=USER
ExecStart=/home/USER/go/bin/cosmovisor start
Restart=always
RestartSec=3
LimitNOFILE=4096
Environment="DAEMON_NAME=lavad"
Environment="DAEMON_HOME=/home/USER/.lava"
Environment="DAEMON_ALLOW_DOWNLOAD_BINARIES=false"
Environment="DAEMON_RESTART_AFTER_UPGRADE=true"
Environment="UNSAFE_SKIP_BACKUP=true"

[Install]
WantedBy=multi-user.target
```

### Start Node Service
```
# Enable service
sudo systemctl enable lavad.service

# Start service
sudo service lavad start

# Check logs
sudo journalctl -fu lavad
```

# Other Considerations
This installation guide is the bare minimum to get a node started. You should consider the following as you become a more experienced node operator.

> Use Ansible script to automate the node installation process

> Configure firewall to close most ports while only leaving the p2p port (typically 26656) open

> Use custom ports for each node so you can run multiple nodes on the same server

> If you find a bug in this installation guide, please reach out to our [Discord Server](https://discord.gg/yV2nEunsTY) and let us know.