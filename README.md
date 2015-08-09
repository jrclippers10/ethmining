# Mining Ethereum setup on Ubuntu 14.04 with AMD GPUs

#### Install GPU Drivers
````
// AMD Install
$ sudo apt-get install linux-headers-generic
$ sudo apt-get install fglrx xvba-va-driver libva-glx1 libva-egl1 vainfo
$ sudo amdconfig --adapter=all --initial

// Reboot, and check if it worked using:
$ fglrxinfo
$ lspci | grep VGA
````

#### Install Geth and Ethminer
Run ether.sh
This will take 15-20 mins
````
$ chmod +x ether.sh
$ ./ether.sh
````

#### Install/Upgrade geth
This has already been done as part of ether.sh, but if you need to upgrade geth, this command will do it. 
````
$ bash <(curl https://install-geth.ethereum.org -L -k)
````

#### Running Geth
````
$ geth --rpccorsdomain localhost --rpc --etherbase 0x36f60f6fae70855d6a506c3cbdfa8b1cc4d77c35
````

#### Running Ethminer
Make sure that geth has an etherbase address set before starting the miner.

If there is only one GPU:
````
$ ethminer -G
````

If there are multiple GPUs, where <n> is the integer number of GPUs
````
$ ethminer -G -t <n>

//if there were 2 GPUs
$ ethminer -G -t 2
````

#### Geth Console

To enter the console for an already running geth process
````
$ geth attach
````

To check that the coinbase address is set
````
> eth.coinbase
````

To set the coinbase while the process is running (only use if not set)
````
web3.miner.setEtherbase('0x36f60f6fae70855d6a506c3cbdfa8b1cc4d77c35')
````

To check the balance of the coinbase address
````
web3.fromWei(eth.getBalance(eth.coinbase), 'ether')
````

To create a new local account
````
> personal.newAccount('passphrase')
````

To unlock an account for spending
````
personal.unlockAccount(web3.eth.accounts[0], 'passphrase');
````
