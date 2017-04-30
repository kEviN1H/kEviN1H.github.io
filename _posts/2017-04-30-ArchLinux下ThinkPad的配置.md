##1,中文输入法  
安装fcitx,用五笔拼音，安装fcitx-table-extra,配置工具fcitx-configtool,如果还有其它依赖包会自己安装上  
如果是ROOT用户安装的多办，ROOT的配置已经OK，但其它的用户没有，需要自己配置一下  
用要配置的用户登陆  
```shell
cp /etc/xdg/autostart/fcitx-autostart.desktop ~/.config/autostart/
```
  
使用 Fcitx 之前，必须先设置一些环境设定变量：  
KDM, GDM, LightDM等显示管理器，在 ~/.xprofile 中加入以下代码；如果是 startx 或者 Slim 启动，即使用 .xinitrc 的情况，则在 ~/.xinitrc 中加入：  
```shell
 export GTK_IM_MODULE=fcitx
 export QT_IM_MODULE=fcitx
 export XMODIFIERS=@im=fcitx
```
注：这一步非常重要不要忽略，原来默认没有.xprofile文件新建一个然后写入这几行，不然中文输入法是启动不了。一定照做。  
   不要在 .bashrc 设置这些环境变量。重新登录后让环境变量生效  
   
 Vim 下使用 Fcitx, 在 ~/.vimrc 添加如下代码。以退出插入模式时，自动关闭 Fcitx：  
```shell
"##### auto fcitx  ###########
let g:input_toggle = 1
function! Fcitx2en()
   let s:input_status = system("fcitx-remote")
   if s:input_status == 2
      let g:input_toggle = 1
      let l:a = system("fcitx-remote -c")
   endif
endfunction

function! Fcitx2zh()
   let s:input_status = system("fcitx-remote")
   if s:input_status != 2 && g:input_toggle == 1
      let l:a = system("fcitx-remote -o")
      let g:input_toggle = 0
   endif
endfunction

set ttimeoutlen=150
"退出插入模式
autocmd InsertLeave * call Fcitx2en()
"进入插入模式
autocmd InsertEnter * call Fcitx2zh()
"##### auto fcitx end ######
```

##2,配置TrackPoint指点杆  
xf86-input-evdev 和 xf86-input-libinput 都支持它。evdev是 Xorg 的默认驱动，但支持点击和指点, 用中键做滚轮需要更多的配置  
安装 gpointing-device-settings 软件包，安装后，执行  
/usr/bin/gpointing-device-settings  
进行配置  

用 xf86-input-evdev 用中键作滚轮的功能由 xorg-xinput 软件包的 xinput 支持。  

~/.xinitrc  
```shell
tpset() { xinput set-prop "TPPS/2 IBM TrackPoint" "$@"; }

tpset "Evdev Wheel Emulation" 1
tpset "Evdev Wheel Emulation Button" 2
tpset "Evdev Wheel Emulation Timeout" 200
tpset "Evdev Wheel Emulation Axes" 6 7 4 5
tpset "Device Accel Constant Deceleration" 0.95
```
 xinput --list 列出设备名。  
"Device Accel Constant Deceleration" 是小红点的敏感度  

打开按压选择  
```shell
# echo -n 1 > /sys/devices/platform/i8042/serio1/press_to_select
```
press_to_select 文件的位置可能会因设备有所不同，有小红点和触摸板的W510在 /sys/devices/platform/i8042/serio1/serio2/   
只有小红点的X61在 /sys/devices/platform/i8042/serio1/ 路径。  

增大小红点的速度  
/etc/udev/rules.d/10-trackpoint.rules  
```shell
ACTION=="add", SUBSYSTEM=="input", ATTR{name}=="TPPS/2 IBM TrackPoint", ATTR{device/sensitivity}="240", ATTR{device/press_to_select}="1"
```

3,控制CPU风扇
.....
