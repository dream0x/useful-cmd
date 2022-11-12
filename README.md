# Handy server management commands
<img src="https://github.com/doxe1/doxe1/blob/main/cover.gif" width="100%" height="150">

_____
<h3 align="center">Alexander, also known as <a href="https://t.me/doxe01" target="_blank">doxe</a>.</h3>
<p align="center">Experienced web3 enthusiast, contributor, moderator and PoS/PoW validator, also just a friendly person </p>

_____

This mini guide contains useful commands with descriptions to help you work with the server. As previously mentioned, one of my goals is development, so this guide will also be constantly expanding.
_____
<h3 name="intro" align="center">Preparing the server</h3>

_____

Update the repositories
```
sudo apt update && sudo apt upgrade -y
```
Install necessary utilities
```
sudo apt install curl tar wget clang pkg-config libssl-dev libleveldb-dev jq build-essential bsdmainutils git make ncdu htop screen unzip bc fail2ban htop -y
```
**The script displays basic information about the system and checks disk read and write speeds, internet connection bandwidth and system performance. Everything is tested by default**

Full test
```
bash <(wget -qO- -o /dev/null yabs.sh)
```
Test disks only
```
bash <(wget -qO- -o /dev/null yabs.sh) -ig
```
Test internet speed only
```
bash <(wget -qO- -o /dev/null yabs.sh) -dg
```
Test the system performance only
```
bash <(wget -qO- -o /dev/null yabs.sh) -di
```
Displays server external IP address
```
wget -qO- eth0.me
```

_____
<h3 name="intro" align="center">Working the server</h3>

_____

Displays the name of the current user
```
whoami
```
Creating a user
```
USER_NAME=<INPUT_ROJECT_NAME>
adduser $USER_NAME && usermod -aG sudo $USER_NAME && su -l $USER_NAME
```
Deleting a user
```
userdel <name> -rf
```
Displays information about RAM usage
```
free -h
```
Displays information about the characteristics of the processor.
```
lscpu
```
**Requires installation** / Displays what processes are running on the server (CPU load), `Shift + H` and only processes remain. 
```
sudo apt install htop -y
```
```
htop
```
Disc
```
sudo apt install iotop -y
```
```
iotop
```
Network
```
sudo apt install iftop -y
```
```
iftop
```
Displays information about the operating system
```
cat /etc/*-release
```
Displays what takes up space on the server (sorting from less to more)
```
du -had 1 /root | sort -h
```
Displays on which ports a particular process works
```
netstat -ntlp | grep LISTEN
```
or
```
ss -tulpn
```
**Requires installation** / Test the bandwidth of the Internet connection.
```
sudo apt install speedtest-cli -y
```
```
speedtest-cli --simple
```
Installing GO (One command)
```
cd $HOME && \
ver="1.18.4" && \
wget "https://golang.org/dl/go$ver.linux-amd64.tar.gz" && \
sudo rm -rf /usr/local/go && \
sudo tar -C /usr/local -xzf "go$ver.linux-amd64.tar.gz" && \
rm "go$ver.linux-amd64.tar.gz" && \
echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> $HOME/.bash_profile && \
source $HOME/.bash_profile && \
go version
```
Check which RPC port the node is on, change the `.file` depending on the project (e.g. `.stride`)
```
echo $(grep -A 3 "\[rpc\]" ~/.stride/config/config.toml | egrep -o ":[0-9]+")
```
How much space the logs take up:
```
journalctl --disk-usage
```
Clear the logs and leave only the last 2 days:
```
journalctl --vacuum-time=2d
```
Clear the logs and save the last 500MB:
```
journalctl --vacuum-size=500M
```
File structure
```
ncdu
```
Find out the serial number of the disc
```
sudo apt install smartmontools -y && \
smartctl -s on -a /dev/nvme0
smartctl -s on -a /dev/nvme1,2,3 
```
Monitoring of most parameters
```
sudo apt install glances
```
```
glances
```
_____
<h3 name="intro" align="center">Cosmos network</h3>

_____
Node status check
```
<binary> status 2>&1 | jq
```
Checking the number of peers
```
curl -s http://localhost:26657/net_info | jq -r '.result.n_peers'
```
or
```
curl -s http://localhost:26657/net_info | jq -r '.result.peers[] | "\(.node_info.id)@\(.remote_ip):\(.node_info.listen_addr | split(":")[2])"' | wc -l
```
Checking vote power online. It will come in handy for update
```
curl -s localhost:26657/consensus_state | jq '.result.round_state.height_vote_set[0].prevotes_bit_array'
```
List of monikers of connected peers
```
curl -s http://localhost:26657/net_info | jq '.result.peers[].node_info.moniker'
```
Search for all outgoing transactions by address
```
<binary> q txs --events transfer.sender=<ADDRESS> 2>&1 | jq | grep txhash
```
Search for all incoming transactions by address
```
<binary> q txs --events transfer.recipient=<ADDRESS> 2>&1 | jq | grep txhash
```
Checking transaction information by hash
```
<binary> q tx <TX_HASH>
```
Check if `priv_validator_key.json` is correct
```
[[ $($TIKER q staking validator $VALOPER -oj | jq -r .consensus_pubkey.key) = $($TIKER status | jq -r .ValidatorInfo.PubKey.value) ]] && echo -e "\nYou win\n" || echo -e "\nYou lose\n"
```
