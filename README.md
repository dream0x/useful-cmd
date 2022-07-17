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
Check that the hard disks work
```
curl -sL yabs.sh | bash -s -ig
```
Check your internet connection
```
curl -sL yabs.sh | bash -s -fg
```

## Working with a server

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
