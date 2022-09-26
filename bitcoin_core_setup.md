# Bitcoin Core Set up

[linux-instructions](https://bitcoin.org/en/full-node#linux-instructions)

```
Download bitcoin core:

btc@nodebox:~/downloads$ wget https://bitcoincore.org/bin/bitcoin-core-23.0/bitcoin-23.0-x86_64-linux-gnu.tar.gz

*** After verifying download, run the following to extract Bitcoin Core ***

btc@nodebox:~/downloads$ tar xzf bitcoin-23.0-x86_64-linux-gnu.tar.gz

Run the following to install Bitcoin Core:

btc@nodebox:~/downloads$ sudo install -m 0755 -o root -g root -t /usr/local/bin bitcoin-23.0/bin/*

Run Bitcoin Core: $ bitcoind -daemon
```

### Create bitcoin.conf config file

btc@nodebox:~/.bitboin$ nano bitcoin.conf

```
server=1
txindex=1
daemon=1
rpcport=8332
rpcbind=0.0.0.0
rpcallowip=127.0.0.1
rpcallowip=10.0.0.0/8
rpcallowip=172.0.0.0/8
rpcallowip=192.0.0.0/8
zmqpubrawblock=tcp://0.0.0.0:28332
zmqpubrawtx=tcp://0.0.0.0:28333
zmqpubhashblock=tcp://0.0.0.0:28334
whitelist=127.0.0.1
rpcauth=bitcoin:27dccf9129f9ea2a7acff1b7fec05a83$eac1abdf296817b070e98a6de3751a9e5d30b1b31e3d43acfd61d466e08c5997
```

*** Stop bitcoin-core: `$ bitcoin-cli stop`

`btc@nodebox:~/downloads$ wget https://raw.githubusercontent.com/bitcoin/bitcoin/master/share/rpcauth/rpcauth.py`

*** Make executable: `btc@nodebox:~/downloads$ chmod +x rpcauth.py`

*** Execute: `btc@nodebox:~/downloads$ ./rpcauth.py bitcoin Wasdale.1080`

*** Output from above:
```
String to be appended to bitcoin.conf:
rpcauth=bitcoin:27dccf9129f9ea2a7acff1b7fec05a83$eac1abdf296817b070e98a6de3751a9e5d30b1b31e3d43acfd61d466e08c5997
Your password:
Wasdale.1080
```

The above string needs appending to the bitcoin.conf file.

*** Start bitcoin-core: `$ bitcoind`

*** Get bitcoind.service file to start bitcoin core automatically:

```
cd /etc/systemd/system/
sudo wget https://raw.githubusercontent.com/bitcoin/bitcoin/master/contrib/init/bitcoind.service
```

*** Edit file: `sudo nano bitcoind.service`

```
ExecStart=/usr/local/bin/bitcoind -daemon \
#ExecStart=/usr/bin/bitcoind -daemonwait \

-conf=/home/btc/.bitcoin/bitcoin.conf \
#-conf=/etc/bitcoin/bitcoin.conf \

-datadir=/home/btc/.bitcoin 
#-datadir=/var/lib/bitcoind

#ExecStartPre=/bin/chgrp bitcoin /etc/bitcoin


User=btc
#User=bitcoin
Group=btc
#Group=bitcoin

#ProtectHome=true
```

```
$ bitcoin-cli stop
$ sudo systemctl enable bitcoind
$ sudo systemctl start bitcoind
$ sudo systemctl status bitcoind
```

https://youtu.be/fx_mLXISrfM?list=PLCRbH-IWlcW2A_kpx2XwAMgT0rcZEZ2Cg&t=1201




```
$ whereis bitcoind
bitcoind: /usr/local/bin/bitcoind
```












