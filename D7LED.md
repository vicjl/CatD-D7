其他作者的led脚本可以通用，硬盘休眠找到方法了，至于完美关机，理论上6.0可以在7.0使用不过要修改，某些文件路径和6.0不一样。还有建议还是不要休眠，黑群设备会频繁唤醒反而会伤害硬盘。

关闭高占用率服务、开启硬盘休眠和led灯 - 休眠时绿色闪光，唤醒蓝色常亮，网络异常红色闪光。 添加到开机任务

```sh
mount -o bind /dev/null /var/log/scemd.log || true
systemctl stop pkg-scsit-monitor.service
mkdir -p /tmp/scripts
cat > /tmp/scripts/ledfan.sh <<EOF
#!/bin/sh
if [ ! -d /sys/class/gpio/gpio450 ] ; then
echo 450 > /sys/class/gpio/export
fi
echo out > /sys/class/gpio/gpio450/direction
i2cset -y -f 0 0x45 0x00 0x55
i2cset -y -f 0 0x45 0x01 0x01
i2cset -y -f 0 0x45 0x30 0x07
while true
do
#Detect network connection
        ping -W 1 -c 1 Lenovo > /dev/null 2>&1
if [ $? -eq 0 ];
then
        i2cset -y -f 0 0x45 0x34 0x00
else
        i2cset -y -f 0 0x45 0x31 0x73
        i2cset -y -f 0 0x45 0x34 255
fi
sata="\$(hdparm -C /dev/sda |grep 'drive'|awk '{print \$4}')"
if [ \$sata = standby ];then
i2cset -y -f 0 0x45 0x36 0
i2cset -y -f 0 0x45 0x32 0x73 #呼吸
i2cset -y -f 0 0x45 0x35 200
echo 0 > /sys/class/gpio/gpio450/value      
fi
if [ \$sata = active/idle ];then
sata_temp="\$(smartctl -a /dev/hda -d ata | sed -n '/Temperature_Celsius/p' | awk '{print \$10}')"
i2cset -y -f 0 0x45 0x35 0
i2cset -y -f 0 0x45 0x33 0x03 #常亮
i2cset -y -f 0 0x45 0x36 150       #B
echo 1 > /sys/class/gpio/gpio450/value
fi
sleep 30
done
EOF
bash /tmp/scripts/ledfan.sh
```


关机熄灭LED关闭风扇。添加到关机任务

```sh
i2cset -y -f 0 0x45 0x30 0x00
echo 0 > /sys/class/gpio/gpio450/value
```


黑群晖DSM7.0/DSM7.01控制面板-信息中心首页显示空白的解决方法
添加root计划任务运行一次即可

```sh
sed -i 's/supportsystempwarning="yes"/supportsystempwarning="no"/g' /etc.defaults/synoinfo.conf
sed -i 's/supportsystemperature="yes"/supportsystemperature="no"/g' /etc.defaults/synoinfo.conf
```


全部完成重启猫盘
