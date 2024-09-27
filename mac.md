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

set ip [lindex $argv 0]
set jump jumphost
set user username
set pwd password

set timeout 10

spawn ssh $user@$jump

expect "password:" {send "$pwd\r"}

set mfa [exec sh -c {oathtool --totp -b -d 6 MRYTGNDIGMYDQZZQOBZDO4DU | awk '{print $1}'}]

expect "*auth]:" {send "$mfa\r"}
expect "Opt> " {send "$ip\r"}
interact
```
