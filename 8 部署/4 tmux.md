# tmux
```
git clone https://github.com/tmux/tmux.git
cd tmux

yum install automake
sh autogen.sh

yum install gcc-c++
yum install libevent-devel
yum install byacc
yum install ncurses-devel

./configure && make
```

```bash
tmux split-window -h  # 横向新建窗口
tmux a -t 0
tmux rename-session -t test1 test2  # 修改窗口名称
```
control + b  control + o  # 窗口向上移动
control + b  alt + o  # 窗口向下移动
