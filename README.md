
`cd ~ && wget -N --no-check-certificate https://github.com/vicjl/CatD-D7/raw/main/install.sh && chmod +x /root/install.sh && bash /root/install.sh 120X`

* 红（大猫/小猫）
 
`bash /etc/rc.local R`
 
* 绿(小猫)/橙(大猫)
 
`bash /etc/rc.local G`
 
* 蓝（大猫/小猫）
 
`bash /etc/rc.local B`
 
* 白(小猫)/紫(大猫)
 
`bash /etc/rc.local W`
 
* 关闭LED灯（大猫/小猫）
 
`bash /etc/rc.local X`


# PLEASE READ FIRST BEFORE PROGRESSING

EVERY COMMAND BELOW MUST BE EXECUTED AS ROOT

EVERY COMMAND BELOW MUST BE EXECUTED AS ROOT

EVERY COMMAND BELOW MUST BE EXECUTED AS ROOT

# led ctl cmd structer
```sh
#init the led controler
i2cset -y -f 0 0x45 0x00 0x55   # turn off all led
i2cset -y -f 0 0x45 0x01 0x01   # reset the led controller
i2cset -y -f 0 0x45 0x30 0x07   # led on

# set power status for led for always on mode
i2cset -y -f 0 0x45 0x31 0x03   #R
i2cset -y -f 0 0x45 0x32 0x03   #G
i2cset -y -f 0 0x45 0x33 0x03   #B

# set max power fo reach led for flashing mode
i2cset -y -f 0 0x45 0x31 0x72   #R
i2cset -y -f 0 0x45 0x32 0x72   #G
i2cset -y -f 0 0x45 0x33 0x72   #B

#control how long each led takes to go from 0 to 100
i2cset -y -f 0 0x45 0x37 0x44   #R
i2cset -y -f 0 0x45 0x3a 0x55   #G
i2cset -y -f 0 0x45 0x3d 0x66   #B

# control how long each led takes to go from 100 to 0
i2cset -y -f 0 0x45 0x38 0x44   #R
i2cset -y -f 0 0x45 0x3b 0x55   #G
i2cset -y -f 0 0x45 0x3e 0x66   #B

# 0-255，the highter the brighter the led goes
i2cset -y -f 0 0x45 0x34 128    #R
i2cset -y -f 0 0x45 0x35 128    #G
i2cset -y -f 0 0x45 0x36 128    #B

# use when doing all muti color rainbow effect
# dekay between each led on/off??? i guess
# without this on muti color just have 2 color or less sometimes
i2cset -y -f 0 0x45 0x39 0x40
i2cset -y -f 0 0x45 0x3c 0x40
i2cset -y -f 0 0x45 0x3f 0x40
```
# led preset

Peraonal favourit flashing violet on catdrive plus
```sh
i2cset -y -f 0 0x45 0x00 0x55
i2cset -y -f 0 0x45 0x01 0x01
i2cset -y -f 0 0x45 0x30 0x07
i2cset -y -f 0 0x45 0x31 0x72
i2cset -y -f 0 0x45 0x33 0x72
i2cset -y -f 0 0x45 0x37 0x33
i2cset -y -f 0 0x45 0x38 0x33
i2cset -y -f 0 0x45 0x3d 0x33
i2cset -y -f 0 0x45 0x3e 0x33
i2cset -y -f 0 0x45 0x34 128
i2cset -y -f 0 0x45 0x36 128
```
red led on
```sh
i2cset -y -f 0 0x45 0x00 0x55
i2cset -y -f 0 0x45 0x01 0x01
i2cset -y -f 0 0x45 0x30 0x07
i2cset -y -f 0 0x45 0x31 0x03
i2cset -y -f 0 0x45 0x34 255
```
green but orange for big led on green for small
```sh
i2cset -y -f 0 0x45 0x00 0x55
i2cset -y -f 0 0x45 0x01 0x01
i2cset -y -f 0 0x45 0x30 0x07
i2cset -y -f 0 0x45 0x32 0x03
i2cset -y -f 0 0x45 0x35 255
```
blue led on
```sh
i2cset -y -f 0 0x45 0x00 0x55
i2cset -y -f 0 0x45 0x01 0x01
i2cset -y -f 0 0x45 0x30 0x07
i2cset -y -f 0 0x45 0x36 255
```
blue flashing
```sh
i2cset -y -f 0 0x45 0x00 0x55
i2cset -y -f 0 0x45 0x01 0x01
i2cset -y -f 0 0x45 0x30 0x07
i2cset -y -f 0 0x45 0x33 0x72
i2cset -y -f 0 0x45 0x3d 0x44
i2cset -y -f 0 0x45 0x3e 0x44
i2cset -y -f 0 0x45 0x36 255
```
red flashing
```sh
i2cset -y -f 0 0x45 0x00 0x55
i2cset -y -f 0 0x45 0x01 0x01
i2cset -y -f 0 0x45 0x30 0x07
i2cset -y -f 0 0x45 0x31 0x72
i2cset -y -f 0 0x45 0x37 0x44
i2cset -y -f 0 0x45 0x38 0x44
i2cset -y -f 0 0x45 0x34 255
```
orange flashing
```sh
i2cset -y -f 0 0x45 0x00 0x55
i2cset -y -f 0 0x45 0x01 0x01
i2cset -y -f 0 0x45 0x30 0x07
i2cset -y -f 0 0x45 0x32 0x72
i2cset -y -f 0 0x45 0x3a 0x55
i2cset -y -f 0 0x45 0x3b 0x55
i2cset -y -f 0 0x45 0x35 255
```
rainbow color
```sh
i2cset -y -f 0 0x45 0x00 0x55
i2cset -y -f 0 0x45 0x01 0x01
i2cset -y -f 0 0x45 0x30 0x07
i2cset -y -f 0 0x45 0x31 0x72
i2cset -y -f 0 0x45 0x32 0x72
i2cset -y -f 0 0x45 0x33 0x72
i2cset -y -f 0 0x45 0x37 0x44
i2cset -y -f 0 0x45 0x3a 0x55
i2cset -y -f 0 0x45 0x3d 0x66
i2cset -y -f 0 0x45 0x38 0x44
i2cset -y -f 0 0x45 0x3b 0x55
i2cset -y -f 0 0x45 0x3e 0x66
i2cset -y -f 0 0x45 0x39 0x40
i2cset -y -f 0 0x45 0x3c 0x40
i2cset -y -f 0 0x45 0x3f 0x40
i2cset -y -f 0 0x45 0x34 255
i2cset -y -f 0 0x45 0x35 255
i2cset -y -f 0 0x45 0x36 255
```
# WARNING

ALL COMMAND BELOW ONLY APPLY TO CATDRIVE RUNING DSM7

ALL COMMAND BELOW ONLY APPLY TO CATDRIVE RUNING DSM7

ALL COMMAND BELOW ONLY APPLY TO CATDRIVE RUNING DSM7

# big catdrive poweroff
```sh
/usr/bin/systemctl --force poweroff
i2cset -y -f 0 0x45 0x77 0xc6
sleep 1
reboot
```

# small catdrive poweroff
```sh
/usr/bin/systemctl --force poweroff
i2cset -y -f 0 0x45 0x00 0x55
i2cset -y -f 0 0x45 0x01 0x01
i2cset -y -f 0 0x45 0x31 0x33
i2cset -y -f 0 0x45 0x32 0x33
i2cset -y -f 0 0x45 0x33 0x33
i2cset -y -f 0 0x45 0x30 0x07
i2cset -y -f 0 0x45 0x34 128
i2cset -y -f 0 0x45 0x35 0
i2cset -y -f 0 0x45 0x36 0
```
