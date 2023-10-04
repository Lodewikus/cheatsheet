# Cheatsheet with my Linux terminal commands

`sudo apt install git -y`  
Git repo: https://github.com/Lodewikus/cheatsheet.git  

## Install pip and venv

`sudo apt install python3-pip -y`  
`sudo apt-get install python3-venv -y`  

## Virtual environments

`python3 -m venv env`  
`source ./env/bin/activate`  
`deactivate` 

## Help

`tldr`  
`man`  

## Network utils

`curl`  
`ifconfig`  
`ip a`  
`ip route | grep default` (to get default gateway)  
`nmap 192.168.0.0/24`  
`sudo ufw status`  (Firewall status)  
`sudo ufw allow 22/tcp` (allow Port 22)  
`netstat -rn` (sudo apt install net-tools)  
`nmcli dev show | grep 'IP4.DNS'` (sudo apt  install network-manager)  

## Network settings for Ubuntu Server

`cd /etc/netplan/` (edit the yaml file)  
`sudo netplan generate && sudo netplan try`

## Services

`sudo systemctl status ssh` (see if ssh service is running)  
`sudo service ssh status` (same as above)  
`sudo systemctl enable ssh --now` (enable ssh service)  
`sudo systemctl restart ssh` (restart ssh service)  
`sudo service inetd restart` (another way to restart a service)  

## Git

`git add .`  
`git commit -m "Commit message"`  
`git push`  
`git pull`  
`git status`  

## General

`ls` (list directory)  
`ls -l` (list - details)  
`ls -la` (list also hidden files)  
`cat`  
`cp` (copy)  
`mv` (move)  
`rm` (remove)  
`rm -R folder`  
`mkdir`  
`pwd` (print current directory)  
`echo $PATH`  
`history`  

## Search & Find

`grep`
`fzf`
`find` (https://www.plesk.com/blog/various/find-files-in-linux-via-command-line/, https://www.freecodecamp.org/news/how-to-search-for-files-from-the-linux-command-line/)

## File permissions, ownership

`sudo chown root:root run_serial_api.sh`  
`chown -R pi:pi venv` (change ownership of a whole folder with subfolders)  
`chmod u+x pi copy_last_good.sh` (make shell script executable)  
`chmod +x setup.sh`  (same as above)  

## Ensure serial port is accessible to lab user

`sudo usermod -a -G dialout lab`  

For Arduino IDE, to have serial port available it is necessary to remove brltty (braille)

`sudo apt-get remove brltty`

## SSH and SCP

`csp sourcefile wikus@172.20.60.193:destinationfile`  

## editors

`vim`  
`nano`  

## Process management

`htop`  
`pkill gunicorn` (kill all processes for, e.g., gunicorn)  
`sudo pkill -f "python3 rpi_alarm.py"` (kill a specific process)  
`ps aux | grep network_check.sh` (search processes for a specific one by name)  

## Raspberry Pi

`raspi-config`  

## cron

`sudo crontab -e`  
`sudo crontab -u <user> -e`  

## Update, install

`sudo apt update && sudo apt upgrade -y`  
`sudo apt install <program>`  
`sudo apt remove <program>`  
`pip3 install -r requirements.txt`  

## Reboot, shutdown

`sudo reboot`  
`sudo shutdown -h now`  
`exit`  

## CTRL-commands

`CTRL-L` (Clear terminal)  
`CTRL-R` (search for previous command)  
`CTRL-U` (clear the current bash command line)  

## Add things to .bashrc

`alias vim="nvim"` (create an alias for neovim)  

To create a bash alias that can take a parameter, you can define a shell function in your .bashrc file.

```
marktext() {  
    /home/wikus/Applications/marktext-x86_64_e94cf48168e949ee60b95bed54505f33.AppImage "$@" > /dev/null 2>&1 &  
}
```

After adding this function to your .bashrc, don't forget to apply the changes by running `source ~/.bashrc`

## Spinning up a temporary web server for file transfer, for example, a large ISO file

Navigate to the directory containing the ISO and run:  
`python3 -m http.server 8000`   

## ZeroTier

One-line installation in Linux

```
curl -s https://install.zerotier.com | sudo bash
sudo zerotier-cli join <network ID>
```

`zerotier-cli -`
`sudo zerotier-cli listnetworks`
`sudo zerotier-cli leave <network ID>` You can leave and join to disconnect & reconnect
