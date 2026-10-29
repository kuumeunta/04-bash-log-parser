# bash-log-parser

## Goal
Understanding of bash scripts work with logs 

## Environment
- Host: Windows 10, VirtualBox 7.2.22
- VM1: Ubuntu 26.04, Hostname: UbuntuMain, username: mainvm, IP 192.168.56.101
- VM2: Ubuntu 26.04, Hostname: UbuntuSub, username: subvm, IP 192.168.56.102
- Network: Host-Only

## Creating script
On subvm creating a bash script and writing it out

![creating script](screenshots/creatingscript.png)
```
cd ~/Documents
touch logcounter.sh
nano logcounter.sh
```
![script](screenshots/script.png)
```
#!/bin/bash
# Count failed SSH logins per source IP
LOG=/var/log/auth.log
grep -a "Failed password" "$LOG" \
  | grep -oE 'from [0-9.]+' \
  | awk '{print $2}' \
  | sort | uniq -c | sort -rn
```
`#!/bin/bash` - noting, that file is bash, so it can work later

`LOG=/var/log/auth.log` - adding a variable `LOG`, that contains info about directory that script should work in

`grep -a "Failed password" "$LOG" \` - finding ever "Failed password" in `LOG` file

`  | grep -oE 'from [0-9.]+' \` - `-o` lets output contain only coinciding part, `-E` includes expanded regular expressions, `from [0-9.]+` includes one and more numbers plus dot

`  | awk '{print $2}' \` - takes only second part from grepped IP-address line

`  | sort | uniq -c | sort -rn` - sorting and deleting doubling lines

\ is used for separating codeline on readable parts

***
![scriptft](screenshots/scriptft.png)

Make file executable and launch it
```
sudo cmod +x logcounter.sh
sudo ./logcounter.sh
```
##
##

## Problems and conclusions
Problems:

Conclusions:
