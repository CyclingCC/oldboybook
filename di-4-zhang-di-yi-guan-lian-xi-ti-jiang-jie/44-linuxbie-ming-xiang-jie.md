#### 1、alias 查看别名 {#151-alias-查看别名}

\[root@oldboy oldboy\]\# alias

alias cp='cp -i'

alias l.='ls -d .\* --color=auto'

alias ll='ls -l --color=auto'

alias ls='ls --color=auto'

alias mv='mv -i'

alias which='alias \| /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'

#### 2、设置别名

\[root@oldboy oldboy\]\# alias rm='echo "this command does not allow to use."'

\[root@oldboy oldboy\]\# rm

this command does not allow to use.

echo "alias rm='echo do not use rm' " &gt;&gt; /etc/profile

#### 3、取消别名 {#153-取消别名}

unalias rm

#### 4、别名作用

\[root@oldboy oldboy\]\# cp a.txt /tmp/

cp: overwrite \`/tmp/a.txt'? y

\[root@oldboy oldboy\]\# \cp a.txt /tmp/

\[root@oldboy oldboy\]\# /bin/cp a.txt /tmp/

\[root@oldboy oldboy\]\# cp -i a.txt /tmp/

cp: overwrite \`/tmp/a.txt'? ^C

\[root@oldboy oldboy\]\# alias

alias cp='cp -i'

alias l.='ls -d .\* --color=auto'

alias ll='ls -l --color=auto'

alias ls='ls --color=auto'

alias mv='mv -i'

alias rm='rm -i'

alias which='alias \| /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'

\[root@oldboy oldboy\]\# unalias cp

\[root@oldboy oldboy\]\# alias

alias l.='ls -d .\* --color=auto'

alias ll='ls -l --color=auto'

alias ls='ls --color=auto'

alias mv='mv -i'

alias rm='rm -i'

alias which='alias \| /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'

\[root@oldboy oldboy\]\# alias\|grep cp

\[root@oldboy oldboy\]\# cp a.txt /tmp/

\[root@oldboy oldboy\]\# cp a.txt /tmp/

\[root@oldboy oldboy\]\# cp -i a.txt /tmp/

cp: overwrite \`/tmp/a.txt'?

#### 5、定义别名永久生效 {#155--定义别名永久生效}

source /etc/profile 全局生效

~/.bashrc 当前用户生效

#### 练习题：

如何设置别名？（说一下思路）

