# Joining Testnet

## Terp Network - athena-1 Testnet

This testnet will start at the patched version of Terp-Core (`v0.1.0`). You will need to use the distributed binary from the Terp Network packages repository.

**Genesis File**

[Genesis File](https://raw.githubusercontent.com/terpnetwork/test-net/master/athena-1/genesis.json):

```bash
   curl -s  https://raw.githubusercontent.com/terpnetwork/test-net/master/athena-1/genesis.json > ~/.terp/config/genesis.json
```

**Genesis sha256**

```bash
sha256sum ~/.terp/config/genesis.json
# b1c07c8ced6289d7e92c3a47085a92296090907c598368baed390e9349699c82
```

**terpd version**

```bash
$ terpd version --long
name: Terp Core
server_name: terpd
version: v0.1.0
commit: 9ef3e1eada1f06509aa223e64a2380b55aaa3bca
build_tags: netgo muslc, # THIS BIT IS KEY
```

**Seed nodes**

```
9cf4fc01e035182688a893d6f6c4687cb59d603d@138.201.200.159:11503
```

**Persistent Peers**

```
15f5bc75be9746fd1f712ca046502cae8a0f6ce7@terp-testnet.nodejumper.io:30656,e6630d7bcc1c6c9593fdcb7e7e1fb762b3e257d1@65.21.134.202:26636,86a64042d8f3508b7d553e36413eade045d3a985@207.180.206.3:11656,aff25de278af66d060a5f130ec90d6b6069c328c@65.21.251.128:33656,d6d7e96122f61a3a2216df9a74822171489a0e17@65.109.17.86:34656,3122336186c16b9ba7f309afbac06412183121f8@65.108.103.86:56656,e1fbb034e9d579ec4012ea8e5bae69887020d06f@176.9.146.72:60756,3da1d76a983abad3d2d1754fc4ab07c20f873c2c@157.230.36.176:11656,f4199c24046325746548e0cb46b11637dfb447d3@95.217.121.229:11014,9b0c5af3f13fe8ca3d0a89d5752e8f5f9062ce7c@95.216.168.99:60656
```

## Setup

**Prerequisites:** Make sure to have [Golang >=1.19](https://golang.org/).

#### Go setup

You need to ensure your gopath configuration is correct. If the following **'make'** step does not work then you might have to add these lines to your .profile or .zshrc in the users home folder:

```sh
nano ~/.profile
```

```
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export GO111MODULE=on
export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin
```

Source update .profile

```sh
source .profile
```

#### Download and verify:

```sh
# find out where terpd is - will likely be /home/<your-user>/go/bin/terpd
which terpd

# put new binary there i.e. in path/to/terpd
wget https://github.com/terpnetwork/terp-core/releases/download/v0.1.0/terp-core -O /home/<your-user>/go/bin/terpd

# if you run this, you should see build_tags: netgo muslc,
# if there is a permissions problem use chmod/chown to make sure it is executable
terpd version --long

# confirm it is using the static lib - should return "not a dynamic executable"
ldd $(which terpd)

# if you really want to be sure
# this should return:
# ELF 64-bit LSB executable, x86-64, version 1 (SYSV), statically linked, 
# Go BuildID=4Ec3fj_EKdvh_u8K3RGJ/JIKOgYFXTJ9LzGROhs8n/uC9gpeaM9MaYurh9DJiN/YcvB8Jc2ivQM2zUSHMhg, stripped
file $(which terpd)
```

Check that you have the right Terp-Core version installed:

```sh
$ terpd version --long
name: Terp-Core
server_name: terpd
version: v0.1.0
commit: e6b8c212b178cf575035065b78309aed547b1335
build_tags: netgo muslc, # THE MUSLC TAG IS KEY
```


#### Running in production

**Note, we'll be going through some upgrades for this testnet. Consider using [Cosmovisor](https://github.com/cosmos/cosmos-sdk/tree/master/cosmovisor) to make your life easier.** Setting up Cosmovisor is covered in the [Terp Network Documentation]().

Download Genesis file when the time is right. Put it in your `/home/<user>/.terp` folder.

If you have not installed cosmovisor, create a systemd file for your TerpNet service:

```sh
sudo nano /etc/systemd/system/terpd.service
```

Copy and paste the following and update `<YOUR_USERNAME>` and `<CHAIN_ID>`:

```sh
Description=Terp-Core daemon
After=network-online.target

[Service]
User=<YOUR_USER>
ExecStart=/home/<YOUR_USERNAME>/go/bin/terpd start
Restart=on-failure
RestartSec=3
LimitNOFILE=4096

[Install]
WantedBy=multi-user.target
```

Enable and start the new service:

```sh
sudo systemctl enable terpd
sudo systemctl start terpd
```

Check status:

```sh
terpd status
```

Check logs:

```sh
journalctl -u terpd -f
```

### Learn more

- [Cosmos Network](https://cosmos.network)
- [Terp Network Documentation](https://docs.terp.network/)

#### Running in production
