# tmux.conf
```bash
tmux set-option

正常模式：
命令模式：<prefix> :
选择模式：<prefix> [

set-option -s					设置 sever option
set-option						设置 session option
set-window-option			    设置 window option(setw, set -w)
set-option -g					设置全局 option
```

## install
```bash
# libevent
wget https://github.com/libevent/libevent/releases/download/release-2.1.11-stable/libevent-2.1.11-stable.tar.gz
tar -zxvf libevent-2.1.11-stable.tar.gz
cd libevent-2.1.11-stable
./configure && make
sudo make install
sudo ln -s /usr/local/lib/libevent-2.1.so.7 /usr/lib/libevent-2.1.so.7

# ncurses
wget https://invisible-mirror.net/archives/ncurses/ncurses-6.1.tar.gz
tar -zxvf ncurses-6.1.tar.gz
cd ncurses-6.1
./configure && make
sudo make install

# tmux
wget http://static.smileorigin.site/tmux-3.0a.tar.gz
tar -zxvf tmux-3.0a.tar.gz
cd tmux-3.0a
./configure && make
sudo make install
```
## Command
`prefix = <ctrl + s>`

### window
```bash
c  创建新窗口
w  列出所有窗口
n  后一个窗口
p  前一个窗口
f  查找窗口
,  重命名当前窗口
&  关闭当前窗口
l	 前后窗口相互切换
```

### splite
```bash
%  垂直分割
"  水平分割
o  交换窗格
x  关闭窗格
⍽  左边这个符号代表空格键 - 切换布局
q  显示每个窗格是第几个，当数字出现的时候按数字几就选中第几个窗格
{  与上一个窗格交换位置
}  与下一个窗格交换位置
z  切换窗格最大化/最小化
```

### other
```bash
?  显示所有快捷键
t  显示时间
:a -d 重绘重口
```

## ssh config
配合 ssh config 即可轻松的自动恢复会话，编辑`~/.ssh/config`，改为自己的配置，保存后执行`ssh work`，即可自动连接到服务器（使用 ssh config 前，先执行`ssh-copy-id root@11.22.33.55 拷贝公钥到服务器上，后续即可免密登录服务器`）
```bash
Host work
    HostName 11.22.33.55
    User root
    RequestTTY yes
    RemoteCommand (tmux a || tmux)
```
