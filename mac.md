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

## login given ip automatic
```expect
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

## tmp
```bash

if [[ $1 == 'up' ]] ; then
    echo "op: upload to generic artifact."
    remoteDir=$2
    localFile=$3
    remoteFile=$4
    curl -u "$user:$password" -v -X POST -F "raw.directory=$remoteDir" -F "raw.asset1=@$localFile" -F "raw.asset1.filename=$remoteFile" https://pkg.sensetime.com/service/rest/v1/components?repository=sensecore-raw-hosted-public
    echo 'curl -u "$user:$password" -v -X POST -F "raw.directory=$remoteDir" -F "raw.asset1=@$localFile" -F "raw.asset1.filename=$remoteFile" https://pkg.sensetime.com/service/rest/v1/components?repository=sensecore-raw-hosted-public'
elif [[ $1 == 'down' ]] ; then
    echo "op: download from generic artifact."
    remoteDir=$2
    remoteFile=$3
    echo "wget https://pkg.sensetime.com/repository/sensecore-raw-hosted-public/$remoteDir/$remoteFile"
    wget https://pkg.sensetime.com/repository/sensecore-raw-hosted-public/$remoteDir/$remoteFile
elif [[ $1 == 'wget' ]] ; then
    if [[ $2 == 'maven' ]] ; then
        echo "wget https://pkg.sensetime.com/repository/sensecore-raw-hosted-public/qa/apache-maven-3.8.6-bin.tar.gz"
    elif [[ $2 == 'helmfile' ]] ; then
        echo "wget https://pkg.sensetime.com/repository/sensecore-raw-hosted-public/qa/helmfile_linux_amd64.v0.144.0"
    elif [[ $2 == 'rocketmq' ]] ; then
        echo "wget https://pkg.sensetime.com/repository/sensecore-raw-hosted-public/qa/rocketmq-all-4.3.0.tar.gz"
    else
        echo "wget https://pkg.sensetime.com/repository/sensecore-raw-hosted-public/qa/"
    fi
else
    echo "Error op, usage: up|down|wget remoteDir|artifactName localFile|remoteFile"
fi

# curl -u "{user}:{password}" -v -X POST -F "raw.directory={remoteDir}" -F "raw.asset1=@{localFile}" -F "raw.asset1.filename={remoteFile}" https://pkg.sensetime.com/service/rest/v1/components?repository=sensecore-raw-hosted-public

# wget https://pkg.sensetime.com/repository/sensecore-raw-hosted-public/{remoteDir}/{remoteFile}
```
