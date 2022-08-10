# Linux Commands

## List all ubuntu services:
    service --status-all

## Update Ubuntu to latest release:
    sudo apt update 
    sudo apt upgrade
    sudo apt dist-upgrade
    sudo apt autoremove
    sudo apt install update-manager-core
    sudo do-release-upgrade

## *systemctl* commands:
    sudo systemctl list-units
    sudo systemctl start <service-name>
    sudo systemctl stop <service-name>
    sudo systemctl restart <service-name>

## Memory usage per process:
    ps -o pid,user,%mem,command ax | sort -b -k3 -r

## Count number of files/folders in a directory;
    ls | wc -l

## *cp* commands:
    cp -r /source/path/* /destination/path           (Copy all files/folders recursively)
    cp -r /source/path/. /destination/path           (Copy files/folders recursively including hiddens files)

## *rm* commands:
    rm -rf /destination/path/*                       (Remove files/folders recursively)
    rm -rf /destination/path/* /destination/path/.*  (Remove files/folders including hidden files)

## Adjust brightness:
    xrandr | grep " connected" | cut -f1 -d " "      (Fetch the name of the attached display)
    xrandr --output [display-name] --brightness 1
    xrandr --output [display-name] --brightness 0.5

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

## *fing* command:
    sudo fing -n 192.168.1.0/24
    sudo fing -n 192.168.1.0/24 -o table,csv,network.txt,10

## *arp-scan* command:
    sudo arp-scan -l --interface=wlp2s0

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

## Create file of required size:
    dd if=/dev/zero of=testfile.log bs=1024 count=10240  (Create file of 10MB)

## Clean Journal Logs
    journalctl --disk-usage                  (Check log size) 
    sudo journalctl --vacuum-time=2d         (Delete log older than 2 days)

## Tuned commands:
    sudo apt install tuned
    sudo systemctl start tuned
    sudo systemctl enable tuned
    tuned-adm active                         (Check the active porfile)
    tuned-adm recommend                      (Get recommended profile for your OS)
    tuned-adm list                           (List lists of profile)
    tuned-adm profile <profile_name>         (Set specific profile for your OS)
    tuned-adm off                            (Turned off the tuned service)

## Google Cloud Commands:
    https://cloud.google.com/storage/docs/gsutil_install  (Install gsutil)

    gcloud init                                           (Authorise to Google Cloud SDK)
    gcloud init --console-only                            (Authorise to Google Cloud SDK on console only)

    gcloud auth login                                     (To authorize access without performing other setup steps)
    gclou auth login --no-launch-browser                  (To authorize access without performing other setup steps on console only)  

    gcloud auth list
    gcloud config set account <ACCOUNT>                   (Set the active account)
    gcloud auth revoke <ACCOUNT>                          (Revoke a account)

    gcloud info                                           (Find credentials file)

    gsutil ls                                             (List all buckets)
    gsutil ls -L -b gs://<BUCKET>
    gsutil ls gs://<BUCKET>                               (List all objects in bucket)

    gsutil cp gs://<BUCKET>/<FILENAME>/  /local/path/     (Download file from Cloud Storage)
    gsutil cp -r gs://<BUCKET>/<DIRECTORY>/ /local/path/  (Download folder from Cloud Storage)
    gsutil cp <FILENAME>  gs://<BUCKET>/                  (Upload file to Cloud Storage)
    gsutil cp -r <DIRECTORY> gs://<BUCKET>/               (Upload folder to Cloud Storage)

    gsutil mv gs://<BUCKET>/* </local/path>               (Move all objects from a bucket to local directory)
    gsutil mv <DIRECTORY> gs://<BUCKET>                   (Move all objects from a local directory to bucket)
    gsutil cp -r gs://<BUCKET-1>/  gs://<BUCKET_2>/       (Copy files between buckets)

    gcloud compute instances list                         (List instances)
    gcloud compute instances describe <INSTANCE_NAME>

## AWS Commands:
    aws configure
    aws configure set aws_access_key_id <AWS_ACCESS_KEY_ID>
    aws configure set aws_secret_access_key <AWS_SECRET_ACCESS_KEY>

    aws s3 ls                                                 (List all buckets)

    aws s3 cp s3://<BUCKET>/<FILENAME> s3://<BUCKET>/        (Copy file from S3 to S3)
    aws s3 cp <FILENAME> s3://<BUCKET>/                      (Upload local file to S3)
    aws s3 cp -r <DIRECTORY> s3://<BUCKET>/                  (Upload local directory to S3)
    aws s3 cp s3://<BUCKET>/<FILENAME> /local/path/          (Download file from S3 to local)
    aws s3 cp -r s3://<BUCKET>/<DIRECTORY> /local/path/      (Download directory to local)
    aws s3 cp -r s3://<BUCKET>/ /local/path/                 (Download all objects from bucket to local)

    aws s3 cp -r <DIRECTORY> s3://<BUCKET>/ --exclude ".txt" (Upload direcotry to S3 except ".txt" file)

    aws cloudformation create-stack --stack-name ec2-example --template-body file://01_ec2.yaml      (Create CloudFormation stack)
    aws cloudformation delete-stack --stack-name ec2-example                                         (Delete CloudFormation stack)

## Azure Commands:
    az login                               
    azcopy login  

    azcopy copy -r https://<ACCOUNT>.blob.core.windows.net/<CONTAINER>/<DIRECTORY> /local/path   (Copy file from Azure Blog to local)

    az aks install-cli
    az aks get-credentials --resource-group <RESOURCE_GROUP_NAME> --name <AKS_CLUSTER_NAME>      (Connect to the AKS cluster)

## Azure Container Registry:
    
Enable the Admin user in Access keys page of Azure Container Registry.

    docker login <AZURE_LOGIN_SERVER>
    docker tag <APP_NAME> <REGISTRY_NAME>/<APP_NAME>
    docker push <REGISTRY_NAME>/<APP_NAME>

## Create Swap memory:
    sudo fallocate -l 1G /swapfile
    sudo chmod 600 /swapfile
    sudo mkswap /swapfile
    sudo swapon /swapfile
    sudo swapon --show

*To make the change permanent open the /etc/fstab file and append the following line:*
    /swapfile swap swap defaults 0 0

## Extend a Linux file system after resizing a volume:

After you increase the size of yout volume, you must use file system–specific commands to extend the file system to the larger size.

    df -hT                                             (Verify File System)
    lsblk                                              (Display info about the block partition)
    sudo growpart /dev/<BLOCK-NAME> <PARTITION-NUM>    (e.g. sudo growpart /dev/nvme0n1 1)
    sudo xfs_growfs -d /                               (For XFS File System.'/' is the mount point)
    sudo resize2fs /dev/<PARTITION-NAME>               (For Ext4 File System)