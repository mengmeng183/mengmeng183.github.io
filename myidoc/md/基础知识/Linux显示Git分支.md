<h1 style="font-size: 40px;text-align:center;color: #007cdc;">
    Linux显示git分支
</h1>
[网址链接](http://blog.csdn.net/Summer_Dream_Journey/article/details/50214609)

#### 1 进入你的home目录
```
cd ~
```
#### 2 编辑.bashrc文件
```
gedit .bashrc
```
#### 3 将下面的代码加入到文件的最后处
```
function git_branch {
  branch="`git branch 2>/dev/null | grep "^\*" | sed -e "s/^\*\ //"`"
  if [ "${branch}" != "" ];then
      if [ "${branch}" = "(no branch)" ];then
          branch="(`git rev-parse --short HEAD`...)"
      fi
      echo " ($branch)"
  fi
}

export PS1='\u@\h \[\033[01;36m\]\W\[\033[01;32m\]$(git_branch)\[\033[00m\] \$ '
```
#### 4 保存退出

如果使用`vim .bashrc`进行编辑，保存退出后还需要执行`source ./.bashrc`命令进行加载

#### 5 完成

Mac 下面启动的 shell 是 login shell，所以加载的配置文件是.bash_profile，不会加载.bashrc。如果你是 Mac 用户的话，需要再执行下面的命令，这样每次开机后才会自动生效：
```
echo "[ -r ~/.bashrc ] && source ~/.bashrc" >> .bash_profile
```
