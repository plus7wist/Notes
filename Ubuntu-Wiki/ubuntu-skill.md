## 清除所有已经安装了的包的配置

```
dpkg -l |grep ^rc|awk '{print $2}' |sudo xargs dpkg -P
```

命令出错则说明已经清除干净了。

## 备份当前系统安装的所有包的列表

```
dpkg --get-selections | grep -v deinstall > ~/somefile
```

## 从上面备份的安装包的列表文件恢复所有包

```
dpkg --set-selections < ~/somefile
sudo dselect
```
