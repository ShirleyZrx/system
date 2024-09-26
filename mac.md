## install brew
``` bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## .bashrc
```
alias stqa='ssh ubuntu@8.211.161.81'
alias ll='ls -lt'
alias gb='go build '
alias shj='~/.login_without_ad.exp zhangruixiang jump-sh.sensetime.com Gsense@144'
alias bjj='~/.login_without_ad.exp zhangruixiang jump-bj.sensetime.com Gsense@144'
alias oc='~/.login_oc.exp zhangruixiang jump-bj.sensetime.com Gsense@144'
alias citk='~/.login_oc.exp zhangruixiang jump-bj.sensetime.com Gsense@144 10.211.49.24'
alias k26='~/.login_oc.exp zhangruixiang jump-bj.sensetime.com Gsense@144 10.111.38.26'
alias ocb='~/.login_ocb_ubuntu.exp zhangruixiang jump-bj.sensetime.com Gsense@144'
alias nperf='~/.login_nova_perf.exp zhangruixiang jump-bj.sensetime.com Gsense@144'
alias tmp='~/.login_tmp_ubuntu.exp zhangruixiang jump-bj.sensetime.com Gsense@144'
alias vpc='~/.login_without_ad.exp zhangruixiang jump-vpc.sensetime.com Gsense@144'
alias stable='~/.stable.exp zhangruixiang jump-bj.sensetime.com Gsense@144'
alias raw='~/.generic.sh'
alias raw2='~/.generic_private.sh'
alias cdsc='cd /Users/zhangruixiang/my_data/codes/sensecore'
alias cdsct='cd /Users/zhangruixiang/my_data/codes/sctool'
alias gt='git'
alias vm='vim'
alias pgh="~/.pg-higgs.exp"
alias pgl="~/.pg-lepton.exp"
alias pght="~/.pg-higgs-tech.exp"
alias pgg="~/.pg-gluon.exp"
alias pgt="~/.pg-telemetry.exp"
alias pgl="~/.pg-lepton.exp"
alias nova="mysql -h dataops-olap.st-sh-01.sensecore.cn -u sensenova -P 33306 -p "
alias nova="~/.nova.exp"

alias my="cd /Users/zhangruixiang/my_data/private/shaomuchen"

export PATH=/Users/zhangruixiang/.grav/bin:$PATH
export PATH="/usr/local/bin:$PATH"
export PATH="/Users/zhangruixiang/Library/Python/3.8/bin:$PATH"
```

## login with ad
```bash
#!/usr/bin/expect

set un [lindex $argv 0]
set ip [lindex $argv 1]
set pw [lindex $argv 2]

set timeout 10

spawn ssh $un@$ip

expect "password:" {send "$pw\r"}

set mfa [exec sh -c {oathtool --totp -b -d 6 MRYTGNDIGMYDQZZQOBZDO4DU | awk '{print $1}'}]
# set mfa [oathtool --totp -b -d 6 MRYTGNDIGMYDQZZQOBZDO4DU | awk '{print $1}']

expect "*auth]:" {send "$mfa\r"}
interact
```
