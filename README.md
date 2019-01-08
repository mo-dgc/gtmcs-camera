# GTMCS Camera

This project is the Pi Zero W Camera used with [Grow Tent Management and Control System (GTMCS)](https://github.com/mo-dgc/Tent-Controller).

It's pretty much a cobbled together version of just [streameye](https://github.com/ccrisan/streameye) and a few things from the [Motioneye Project](https://github.com/ccrisan/motioneye).

I know this is a waste of a Pi0 to just be used as a MJPEG streamer, but it's just meant as a starting point for DIY folks.  As part of the whole GTMCS project, you could very simply move all of your probes and relay controls to the Pi0 as well and do away with Xbee and Arduino all together just running over Wifi.  The possibilities are endless.

## Installation

1. Burn Raspbian Jesse Light to an SD Card and get your Pi0 online.

   [Install Raspbian to SD Card](https://github.com/mo-dgc/Tent-Controller/wiki/Installation#install-raspbian-to-sd-card)
   
   [Installing Raspbian from Mac](https://github.com/mo-dgc/Tent-Controller/wiki/Installing-Raspbian-from-Mac)
  
2. Install required packages
   ```
   sudo apt install -y avahi-daemon
   sudo apt install -y python-dev python-pip python-setuptools python3 python3-dev python3-pip python3-setuptools
   sudo apt install -y git
   sudo pip install picamera
   ```
  
3. Clone streameye
   ```
   git clone https://github.com/ccrisan/streameye.git
   ```
4. Compile and install streameye
   ```
   cd streameye
   make
   sudo make install
   cd extras
   sudo cp raspimjpeg.py /usr/local/bin/
   ```
   
5. Clone this repo
   ```
   git clone https://github.com/mo-dgc/gtmcs-camera.git
   ```
  
6. Run installer
   TBD
   ```
   /etc/streameye/stremeye.conf
   /etc/streameye/raspimjpeg.conf
   /usr/local/bin/streameye.sh
   ```

```
$ cat /etc/systemd/system/streameye.service
[Unit]
Description=Streameye
After=network.target

[Service]
ExecStart=/usr/local/bin/streameye.sh start
ExecStop=/usr/local/bin/streameye.sh stop
RemainAfterExit=True

[Install]
WantedBy=multi-user.target
```  

```
$ sudo systemctl daemon-reload
$ sudo systemctl start streameye
$ sudo systemctl stop streameye
$ sudo systemctl restart streameye
$ systemctl status streameye
$ systemctl enable streameye
```
