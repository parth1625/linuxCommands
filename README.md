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
    sudo pmap 917
    sudo pmap 917 | tail -n 1
    sudo pmap 917 | tail -n 1 | awk '/[0-9]K/{print $2}'
    sudo pmap 917 531 | grep total

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
    uname -s (Kernel name)
    uname -r (Kernel version)
    uname -n (Hostname)
    uname -m (Hardware name and Processor name)

## List Wi-Fi networks using *nmcli*:
    nmcli con show
    nmcli dev status
    nmcli con up <NAME>
    nmcli con reload
    nmcli dev dis <DEVICE>