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