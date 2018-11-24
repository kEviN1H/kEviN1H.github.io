```bash
pacman -Rsn $(pacman -Qdtq)
pacman -Scc
rm /var/lib/systemd/coredump/.
journalctl --vacuum-size=50M
```



假设全屏分辨率为1366x768

修改/etc/default/grub 文件
加上以下内容
代码： 全选
```bash
GRUB_GFXMODE=1366x768x32
GRUB_GFXPAYLOAD_LINUX=keep
```
然后执行
代码： 全选
```shell
sudo update-grub
```
