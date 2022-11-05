# Ubuntu-21.10(impish)リポジトリ変更.md

Ubuntu 20.10でapt-get updateしたらエラーが出た
https://blog.denet.co.jp/i-got-an-error-when-i-did-apt-get-update-on-ubuntu-20-10/

cat /etc/apt/sources.list | grep -v "#"

        deb http://jp.archive.ubuntu.com/ubuntu/ impish main restricted
        deb http://jp.archive.ubuntu.com/ubuntu/ impish-updates main restricted
        deb http://jp.archive.ubuntu.com/ubuntu/ impish universe
        deb http://jp.archive.ubuntu.com/ubuntu/ impish-updates universe
        deb http://jp.archive.ubuntu.com/ubuntu/ impish multiverse
        deb http://jp.archive.ubuntu.com/ubuntu/ impish-updates multiverse
        deb http://jp.archive.ubuntu.com/ubuntu/ impish-backports main restricted universe multiverse
        deb http://security.ubuntu.com/ubuntu impish-security main restricted
        deb http://security.ubuntu.com/ubuntu impish-security universe
        deb http://security.ubuntu.com/ubuntu impish-security multiverse

impish のリポジトリは以下にあるようす

http://old-releases.ubuntu.com/ubuntu/dists/impish/

sed -i -e 's/ports.ubuntu.com\/ubuntu-ports/old-releases.ubuntu.com\/ubuntu/g' /etc/apt/sources.list
と書いてあるがあてにならないので。

vim /etc/apt/sources.list

cat /etc/apt/sources.list | grep -v "#"

    deb https://old-releases.ubuntu.com/ubuntu/ impish main restricted
    deb https://old-releases.ubuntu.com/ubuntu/ impish-updates main restricted
    deb https://old-releases.ubuntu.com/ubuntu/ impish universe
    deb https://old-releases.ubuntu.com/ubuntu/ impish-updates universe
    deb https://old-releases.ubuntu.com/ubuntu/ impish multiverse
    deb https://old-releases.ubuntu.com/ubuntu/ impish-updates multiverse
    deb https://old-releases.ubuntu.com/ubuntu/ impish-backports main restricted universe multiverse
    deb https://old-releases.ubuntu.com/ubuntu/ impish-security main restricted
    deb https://old-releases.ubuntu.com/ubuntu/ impish-security universe
    deb https://old-releases.ubuntu.com/ubuntu/ impish-security multiverse

sudo apt-get update
echo $?            
    0

OK!
