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

## Count number of files/folders in a directory;
    ls | wc -l

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

## Find installed packages:
    sudo apt list --installed

## Google Cloud Commands:
    gsutil ls                                                 (List all buckets)
    gsutil ls -L -b gs://<BUCKET>
    gsutil ls gs://<BUCKET>                               (List all objects in bucket)

    gsutil cp gs://<BUCKET>/<FILENAME>/  /local/path/     (Download file from Cloud Storage)
    gsutil cp -r gs://<BUCKET>/<DIRECTORY>/ /local/path/  (Download folder from Cloud Storage)
    gsutil cp <FILENAME>  gs://<BUCKET>/                  (Upload file to Cloud Storage)
    gsutil cp -r <DIRECTORY> gs://<BUCKET>/               (Upload folder to Cloud Storage)

    gsutil mv gs://<BUCKET>/* </local/path>               (Move all objects from a bucket to local directory)
    gsutil mv <DIRECTORY> gs://<BUCKET>                   (Move all objects from a local directory to bucket)

## AWS Commands:
    aws s3 ls                                                 (List all buckets)

    aws s3 cp s3://<BUCKET>/<FILENAME> s3://<BUCKET>/        (Copy file from S3 to S3)
    aws s3 cp <FILENAME> s3://<BUCKET>/                      (Upload local file to S3)
    aws s3 cp -r <DIRECTORY> s3://<BUCKET>/                  (Upload local directory to S3)
    aws s3 cp s3://<BUCKET>/<FILENAME> /local/path/          (Download file from S3 to local)
    aws s3 cp -r s3://<BUCKET>/<DIRECTORY> /local/path/      (Download directory to local)
    aws s3 cp -r s3://<BUCKET>/ /local/path/                 (Download all objects from bucket to local)

    aws s3 cp -r <DIRECTORY> s3://<BUCKET>/ --exclude ".txt" (Upload direcotry to S3 except ".txt" file)