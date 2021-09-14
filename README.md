# Linux Commands

## List all ubuntu services:
    service --status-all

## *systemctl* commands:
    sudo systemctl list-units
    sudo systemctl start <service-name>
    sudo systemctl stop <service-name>
    sudo systemctl restart <service-name>

## Memory usage per process:
    ps -o pid,user,%mem,command ax | sort -b -k3 -r

## Memory usage per PID:
    sudo pmap <PID>
    sudo pmap <PID> | tail -n 1
    sudo pmap <PID> | tail -n 1 | awk '/[0-9]K/{print $2}'
    sudo pmap <PID1> <PID2> | grep total

## Find details about domain:
    nslookup google.com
    host google.com
    dig google.com
    whois google.com

## Show routing table:
    route -n
    route add default gw 192.168.1.1
    route del default gw 192.168.1.1

## List Hardwares:
    sudo lshw
    sudo lshw -short
    sudo lshw -C network

## Enable & Disable wireless devices:
    rfkill list
    rfkill block all
    rfkill unblock all
    rfkill block <TYPE|ID>
    rfkill unblock <TYPE|ID>

## Display info anout system:
    uname -a
    uname -s                                 (Kernel name)
    uname -r                                 (Kernel version)
    uname -n                                 (Hostname)
    uname -m                                 (Hardware name and Processor name)

## List Wi-Fi networks using *nmcli*:
    nmcli con show
    nmcli dev status
    nmcli con up <NAME>
    nmcli con reload
    nmcli dev dis <DEVICE>

## *nmap* command:
    sudo nmap -sP 192.168.1.0/24             (List of devices connected to router)
    sudo nmap -F                             (Fast scan)
    sudo nmap -O                             (OS info)
    sudo nmap -V google.com                  (Detailed info about remote machine)
    sudo nmap 192.168.1.*                    (Scan whole subnet)

## Dispaly wireless interfaces:
    iwconfig

## Display filesystem information:
    df -hT

## Display open ports:
    ss 
    netstat
    ss -tnlp (TCP ports)
    netstat -tnlp (TCP ports)
    ss -unlp (UDP ports)
    netstat -unlp (UDP ports)

## Find files by name on system:
    locate <FILEMANE>
    locate -i <STRING>                       (Find files that include <STRING> in their names)
    locate -i <FILE1> <FILE2>                (Find multiple files)
    find / -iname <FILEMANE>   
    find /path/to/file/ -iname <FILEMANE>    (Find in specific directory)
    find . -iname <FILENAME>                 (Find in current directory)
    find /path/to/file/ -iname -empty        (Find empty files)
    find . -size +5M\                        (Find files larger than 5MB)