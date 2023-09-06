# cheatsheet with my Linux command line commands
- Git repo: https://github.com/Lodewikus/cheatsheet.git

## Help
- tldr
- man

## Network utils
- curl
- ifconfig
- ip a
- ip route | grep default
- nmap 192.168.0.0/24

## Git
- git add .
- git commit -m "Fixed split_loads_to_wh.py"
- git push

## Virtual environments
`
python3 -m venv alch
source ./alch/bin/activate
deactivate
`

## General
ls (list directory)
ls -l (list - details)
ls -la (list also hidden files)
cat
cp (copy)
mv (move)
rm (remove)
rm -R folder
mkdir
pwd (print current directory)
echo $PATH

## File permissions, ownership
sudo chown root:root run_serial_api.sh
chown -R pi:pi venv (change ownership of a whole folder with subfolders)
chmod u+x pi copy_last_good.sh (make shell script executable)

# Ensure serial port is accessible to lab user
sudo usermod -a -G dialout lab

## SSH and SCP
csp sourcefile wikus@172.20.60.193:destinationfile

## editors
vim
nano

## Process management
htop
pkill gunicorn (kill all processes for, e.g., gunicorn)
sudo pkill -f "python3 rpi_alarm.py" (kill a specific process)
ps aux | grep network_check.sh (search processes for a specific one by name)

## Raspberry Pi
raspi-config
sudo crontab -e
sudo crontab -u <user> -e

## Update, install
sudo apt update && sudo apt upgrade -y
sudo apt install <program>
sudo apt remove <program>
pip3 install -r requirements.txt

## Reboot, shutdown
sudo reboot
sudo shutdown -h now
exit

## CTRL-commands
CTRL-L Clear terminal
CTRL-R search for previous command
CTRL-U clear the current bash command line
