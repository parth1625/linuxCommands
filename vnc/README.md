# VNC Server

## Install tigervnc vnc server on your server:
    sudo apt install xserver-xorg-core
    sudo apt install tigervnc-standalone-server tigervnc-common tigervnc-xorg-extension

## If necessary(ubuntu-desktop):
    sudo apt-get install --reinstall ubuntu-desktop gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal

## Create a VNC user:
    sudo useradd -m <username>
    sudo passwd <username>
    sudo su <username>

## Set VNC Password for new user:
    vncpasswd

## Configuring Gnome 3 Desktop environment to use with VNC:
    vim ~/.vnc/xstartup

        #!/bin/sh
        [ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup
        [ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources

    sudo chmod 755 xstartup

## Run VNC Server using command:
    vncserver :1 -localhost no -geometry 1024x768 -depth 32
    vncserver :2 -localhost no -geometry 1024x768 -depth 32

## List VNC Server:
    vncserver -list

## Stop TigerVNC server:
    vncserver -kill :1
    vncserver -kill :2
    vncserver -kill :*   (Kill all VNC Server)

## Create /etc/vnc/xstartup, edit the file, make executable. This will create the typical Ubuntu desktop.

    sudo mkdir /etc/vnc
    cd /etc/vnc
    sudo vim xstartup

        #!/bin/sh
        test x"$SHELL" = x"" && SHELL=/bin/bash
        test x"$1"     = x"" && set -- default
        vncconfig -iconic &
        "$SHELL" -l << EOF
        export XDG_SESSION_TYPE=x11
        export GNOME_SHELL_SESSION_MODE=ubuntu
        dbus-launch --exit-with-session gnome-session --session=ubuntu
        EOF
        vncserver -kill $DISPLAY
    
    sudo chmod 755 xstartup

## Create service file for VNC server:
    sudo vim /etc/systemd/system/vncserver@.service


        [Unit]
        Description=Start TigerVNC server at startup
        After=syslog.target network.target

        [Service]
        Type=simple
        User=USERNAME
        PAMName=login
        PIDFile=/home/USERNAME/.vnc/%H:%i.pid
        ExecStartPre=/usr/bin/vncserver -kill :%i > /dev/null 2>&1
        ExecStart=/usr/bin/vncserver -fg -depth 24 -geometry 1920x1200 -localhost no :%i
        ExecStop=/usr/bin/vncserver -kill :%i

        [Install]
        WantedBy=multi-user.target

## Start the vnc service:
    sudo systemctl daemon-reload
    sudo systemctl enable vncserver@1.service
    sudo systemctl start vncserver@1
    sudo systemctl start vncserver@2
    sudo systemctl status vncserver@1


## Connecting with a VNC client:
    sudo apt install tigervnc-viewer
    vncviewer <VNCSERVER-IP>:<PORT>
    vncviewer 192.1681.82:5901
    vncviewer 192.1681.82:1
    vncviewer 192.1681.82:2