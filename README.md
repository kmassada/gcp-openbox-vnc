# gcp-openbox-vnc

```shell
$ uname -a
Linux instance-1 4.13.0-38-generic #43-Ubuntu SMP Wed Mar 14 15:20:44 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
```
## on server

install x server and openbox

```shell
sudo apt-get install xauth xserver-xorg xserver-xorg-core xorg
sudo apt-get update
sudo apt-get install openbox menu libgl-dev
```

install vnc

```shell
sudo apt install tightvncserver 
```

edit startup `vi ~/.vnc/xstartup`

```shell
#!/bin/sh
unset SESSION_MANAGER
exec openbox-session &
```

of course grant exec permissions `chmod + x ~/.vnc/xstartup`


start VNC server. `vi ~/startVNC.sh`

```shell
#!/bin/sh
vncserver :1 -geometry 1200x700 -localhost
```

of course grant exec permissions `chmod + x ~/startVNC.sh`

## Troubleshooting

### visudo

```
%vncviewer   ALL=(ALL:ALL) ALL
%openbox-session   ALL=(ALL:ALL) ALL
```

### lock

remove locks

```
sudo rm -rf /tmp/.X11-unix/* /tmp/.X1-lock
```
## on client

install vnc client

```
sudo apt install xtightvncviewer
```

start vncclient `vi ~/startVNCClient.sh`

``` shell
#!/bin/sh
ssh -f -L 5901:localhost:5901 user@IPaddress sleep 1;
vncviewer  localhost::5901
```

of course grant exec permissions `chmod + x ~/startVNC.sh`

![Image of xtightvncviewer](incomplete-window)