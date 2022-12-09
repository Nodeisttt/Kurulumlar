<p align="center">
  <img height="100" height="auto" src="https://raw.githubusercontent.com/Nodeist/Kurulumlar/main/logos/stride.png">
</p>



# Stride Snapshot Setup
We take node snapshot daily.

### Install lz4 (if needed)
```
sudo apt update
sudo apt install snapd -y
sudo snap install lz4
```

### Stop your node
```
sudo systemctl stop strided
```

### Reset your node
This will erase your node database. If you are already running validator, be sure you backed up your `priv_validator_key.json` prior to running the the command.

```
strided tendermint unsafe-reset-all --home $HOME/.stride --keep-addr-book
```

### Download & Install the snapshot
```
curl -L https://snap.nodeist.net/stride/stride.tar.lz4 | lz4 -dc - | tar -xf - -C $HOME/.stride --strip-components 2
```

### Restart Service & Check Log:
```
sudo systemctl start strided && journalctl -u strided -f --no-hostname -o cat
```