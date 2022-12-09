<p align="center">
  <img height="100" height="auto" src="https://raw.githubusercontent.com/Nodeist/Kurulumlar/main/logos/c4e.png">
</p>



# C4E Snapshot Setup
We take node snapshot daily.

### Install lz4 (if needed)
```
sudo apt update
sudo apt install snapd -y
sudo snap install lz4
```

### Stop your node
```
sudo systemctl stop c4ed
```

### Reset your node
This will erase your node database. If you are already running validator, be sure you backed up your `priv_validator_key.json` prior to running the the command.

```
c4ed tendermint unsafe-reset-all --home $HOME/.c4e-chain --keep-addr-book
```

### Download & Install the snapshot
```
curl -L https://snap.nodeist.net/c4e/c4e.tar.lz4 | lz4 -dc - | tar -xf - -C $HOME/.c4e-chain --strip-components 2
```

### Restart Service & Check Log:
```
sudo systemctl start c4ed && journalctl -u c4ed -f --no-hostname -o cat
```