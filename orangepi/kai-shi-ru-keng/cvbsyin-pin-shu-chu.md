# OrangePi 3.5mm口cvbs音频输出

默认的音视频输出是HDMI,如果想修改成cvbs输出,需要切换声卡并保存 终端输入命令aplay -l确认声卡是否存在.

用cat /etc/asound.conf查看声卡配置的信息是否正确

```
pcm.!default {
 type hw
 card 1
 device 0
}

ctl.!default {
 type hw
 card 1
}
```

在其中card\*就是默认声卡，具体可以去aplay -l 查看声卡编号，audio codec是3.5口，sndhdmi是hdmi。

有些系统3.5口的lineout默认静音，终端输入命令alsamixer,然后按F6选择audiocodec回车,之后按5次方向右键,跳到audio lineout后按m键\(打开声音\),出现mm mm mm oo后关闭窗口退出.

插上耳机就可以播放音乐了

之后要保存配置,否则每次开机都要设置.终端输入命令

```
alsactl store -f /var/lib/alsa/asound.state
```

smplayer切换方法：

打开 smplayer, 选择 options 中的 preferences， 选择 alsa\(audiocodec\) ， HDMI和 audiocodec 同时只能打开一个。

