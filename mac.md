## install brew
``` bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## .bashrc
```
alias raw='~/.generic.sh'
alias raw2='~/.generic_private.sh'
alias gt='git'
alias vm='vim'
alias pgh="~/.pg-higgs.exp"
alias nova="mysql -h dataops-olap.st-sh-01.sensecore.cn -u sensenova -P 33306 -p "
alias nova="~/.nova.exp"
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
