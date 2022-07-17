# Hello all, below are all the handy server management commands

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

Check what processes are running on the server (CPU load)
```
htop
```
Check what takes up space on the server (sorting from less to more)
```
du -had 1 /root | sort -h
```


