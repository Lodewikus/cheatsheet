# Cheatsheet with my Linux terminal commands

Git repo: https://github.com/Lodewikus/cheatsheet.git  

## Install pip and venv

`sudo apt install python3-pip -y`  
`sudo apt-get install python3-venv -y`  
`pip freeze`  

## Virtual environments

`python3 -m venv env`  
`source ./env/bin/activate`  
`deactivate` 

## Help

`tldr`  
`man`  

## Network utils

`curl`  
`curl https://ipinfo.io/ip` (get external IP address)
`curl -O https://install.speedtest.net/app/cli/ookla-speedtest-1.2.0-linux-armhf.tgz`  (download file)  
`ifconfig`  
`ip a`  
`ip route | grep default` (to get default gateway)  
`nmap 192.168.0.0/24`  
`sudo ufw status`  (Firewall status)  
`sudo ufw allow 22/tcp` (allow Port 22)  
`netstat -rn` (sudo apt install net-tools)   
`netstat -tulnp | grep 5000` (see what is using port 5000, for example)  
`nmcli dev show | grep 'IP4.DNS'` (sudo apt  install network-manager)    
`arp -a | grep dc:a6:32:77:44:38`  (find the IP address when the MAC address is known)  

## Network settings for Ubuntu Server

`cd /etc/netplan/` (edit the yaml file)  
`sudo netplan generate && sudo netplan try`

## Services

`sudo systemctl status ssh` (see if ssh service is running)  
`sudo service ssh status` (same as above)  
`sudo systemctl enable ssh --now` (enable ssh service)  
`sudo systemctl restart ssh` (restart ssh service)  
`sudo service inetd restart` (another way to restart a service)   
`sudo service --status-all`   

## Git

If Git is not installed

```
sudo apt install git -y
git config --global user.email "wikus@olivierfamilie.org"
git config --global user.name "Wikus Olivier"
```

`git add .`  
`git commit -m "Commit message"`  
`git push`  
`git pull`  
`git status`  
`git checkout -- file.ext`  (discard the last change to file.ext)  

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
`lsof` (list open files and associated processes)  

## Unzip
`tar -xvzf filename` (unzip)  

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

`scp sourcefile wikus@172.20.60.193:destinationfile`  

## RSYNC

`rsync -av source/ destination/` (copy all files and folders from source to dest)  
a - archive: recurse directories and a lot more, v - verbose  

`rsync -av --delete source/ destination/` (as above, but delete files from destination that are not in source)  
`rsync -av --delete --dry-run source/ destination/` (as above, but dry run only)  
`rsync zaP ~/code/my_project wikus@10.0.0.20:~/code/` (copy to a remote folder)  

z - compress, a - archive, P - show progress  
Omitting the trailing slash from the source means it copies the entire folder  

The reverse also works:  
`rsync zaP wikus@10.0.0.20:~/code/my_project/new_folder ~/code/my_project/`  

## Editors

`vim`  
`nano`  

## Process management

`htop`  
`btop`  
`pkill gunicorn` (kill all processes for, e.g., gunicorn)  
`sudo pkill -f "python3 rpi_alarm.py"` (kill a specific process)  
`ps aux | grep network_check.sh` (search processes for a specific one by name)  
`pgrep -f 'python3 file_watcher.py` (same as above)
`pkill -f 'python3 file_watcher.py` (kill a process by name)
`kill 1234` (kill a process by process ID)

## Raspberry Pi

`raspi-config`  

## Crontab

`sudo crontab -e`  
`sudo crontab -u <user> -e`  

```
# ┌───────────── minute (0 - 59)
# │ ┌───────────── hour (0 - 23)
# │ │ ┌───────────── day of month (1 - 31)
# │ │ │ ┌───────────── month (1 - 12)
# │ │ │ │ ┌───────────── day of week (0 - 6) (Sunday to Saturday;
# │ │ │ │ │                                       7 is also Sunday on some systems)
# │ │ │ │ │
# │ │ │ │ │
# * * * * *  command_to_execute

###### Sample crontab ######

# Empty temp folder every Friday at 5pm
0 5 * * 5 rm -rf /tmp/*

# Backup images to Google Drive every night at midnight
0 0 * * * rsync -a ~/Pictures/ ~/Google\ Drive/Pictures/
```

## Execute a program periodically

`watch cat filetxt` (run cat every 2 seconds - the default)  
`watch -n 60 cat filetxt` (run cat every 60 seconds)  
`watch -d cat filetxt` (highlight differences as they appear)

## Update, install

`sudo apt update && sudo apt upgrade -y`  
`sudo apt install <program>`  
`sudo apt remove <program>`  
`pip3 install -r requirements.txt`  

## Reboot, shutdown

`sudo reboot`  
`sudo shutdown -h now`  
`exit`  

## System information

`uname -a`  (System information)  
`sudo lshw -class disk -class storage -short` (List hardware - all storage)  
`sudo lshw -class network -short` (List hardware - networks, for example)
`neofetch` (Summary of system information)     

## Disks, media, volumes

`df` (Display all file systems)  
`df /home/` (Display details on where /home/ is stored)  

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

Remove Zeroties
```
apt remove zerotier-one
dpkg -P zerotier-one
```

https://discuss.zerotier.com/t/uninstall-from-linux-after-using-the-recommended-command/8986

network ID for HemispheresHub: d5e5fb6537ea0576  

`zerotier-cli -`
`sudo zerotier-cli listnetworks`  
`sudo zerotier-cli leave <network ID>` You can leave and join to disconnect & reconnect.

## VIM

`cgn` Moves the cursor to the next search match and performs c on the whole match. After inserting text and pressing <Esc>, you can press . to perform the same edit on the next search match, etc.  
`ciw` Change inner word  
`gg` Go to the top of the file
`G` Go to the end of the file
`y` Yank (copy)  
`p` Paste  
`u` Undo
`dd` Delete line
`o` Insert line below
`O` Insert line above
`x` Delete character
`r` Replace character  
`"+y` Yank selected text to the clipboard  

## Linux Mint-specific

Type special characters

ê: right-alt + e, then > (right bracket)  
é: right-alt + e, then ' (single quote)  
ë: right-alt + e, then " (double quote)
