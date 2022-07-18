# Hello all, below are all the handy server management commands

This guide will be updated to over time as i find more interesting commands

## Preparing the server

Update the repositories
```
sudo apt update && sudo apt upgrade -y
```
Install necessary utilities
```
sudo apt install curl build-essential git wget jq make gcc tmux htop nvme-cli pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev -y
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

## Working with a server

Displays the name of the current user
```
whoami
```
Displays information about RAM usage
```
free -h
```
Check what processes are running on the server (CPU load), `Shift + H` and only processes remain
```
htop
```
Check what takes up space on the server (sorting from less to more)
```
du -had 1 /root | sort -h
```
Checking on which ports a particular process works
```
netstat -ntlp | grep LISTEN
```
Installing GO (One command)

```
ver="1.18.1" && \
wget "https://golang.org/dl/go$ver.linux-amd64.tar.gz" && \
sudo rm -rf /usr/local/go && \
sudo tar -C /usr/local -xzf "go$ver.linux-amd64.tar.gz" && \
rm "go$ver.linux-amd64.tar.gz" && \
echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> $HOME/.bash_profile && \
source $HOME/.bash_profile && \
go version
```
<img src="https://github.com/doxe1/useful-cmd/blob/main/29eb26f376d3b48d61bce09590fff717.png" width="350">
