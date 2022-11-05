# docker

## 前提条件

https://docs.docker.com/desktop/linux/install/#system-requirements

### kvm モジュールロード確認

lsmod | grep kvm

ichiro@ASUS-VivoBook ~ % lsmod | grep kv
kvm_intel             290816  0

### kvm デバイス権限設定

ls -al /dev/kvm

ichiro@ASUS-VivoBook ~ % ls -al /dev/kvm
crw-rw----+ 1 root kvm 10, 232  6月  4 09:52 /dev/kvm

echo $USER

sudo usermod -aG kvm $USER

ichiro@ASUS-VivoBook ~ % grep kvm /etc/group
kvm:x:109:

sudo usermod -aG kvm $USER
[sudo] ichiro のパスワード: 

grep kvm /etc/group       
kvm:x:109:ichiro

## インストール

### リポジトリの設定

https://docs.docker.com/engine/install/debian/#set-up-the-repository

1. Update the apt package index and install packages to allow apt to use a repository over HTTPS:

sudo apt-get update

sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

2. Add Docker’s official GPG key:

sudo mkdir -p /etc/apt/keyrings

curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

3. Use the following command to set up the repository:

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

### ダウンロード

https://docs.docker.com/desktop/release-notes/

から deb 版をダウンロード

## インストール

https://docs.docker.com/desktop/linux/install/ubuntu/

Download latest DEB package from the release page.

/home/ichiro/ダウンロード

sudo apt-get update
sudo apt-get install ./docker-desktop-4.9.0-amd64.deb

docker compose version
docker --version
docker version

ichiro@ASUS-VivoBook ~/ダウンロード % docker compose version
Docker Compose version v2.6.0

ichiro@ASUS-VivoBook ~/ダウンロード % docker --version
Docker version 20.10.16, build aa7e414

ichiro@ASUS-VivoBook ~/ダウンロード % docker version
Client: Docker Engine - Community
 Cloud integration: v1.0.25
 Version:           20.10.16
 API version:       1.41
 Go version:        go1.17.10
 Git commit:        aa7e414
 Built:             Thu May 12 09:17:30 2022
 OS/Arch:           linux/amd64
 Context:           desktop-linux
 Experimental:      true

Server: Docker Desktop 4.9.0 (80466)
 Engine:
  Version:          20.10.16
  API version:      1.41 (minimum version 1.12)
  Go version:       go1.17.10
  Git commit:       f756502
  Built:            Thu May 12 09:15:42 2022
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.6.4
  GitCommit:        212e8b6fa2f44b9c21b2798135fc6fb7c53efc16
 runc:
  Version:          1.1.1
  GitCommit:        v1.1.1-0-g52de29d
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0


### 完全削除を先に記載
sudo apt remove docker-desktop

rm -r $HOME/.docker/desktop

sudo rm /usr/local/bin/com.docker.cli

sudo apt purge docker-desktop



## チュートリアル

https://docs.docker.com/get-started/


github プロジェクトクローンについて
https://qiita.com/masamitsu-konya/items/abb572337156e4d003cf
https://docs.github.com/ja/repositories/creating-and-managing-repositories/cloning-a-repository

cd projects
git clone git@github.com:masamitsu-konya/example.git

ichiro@ASUS-VivoBook ~/dev % mkdir -p docker

ichiro@ASUS-VivoBook ~/dev/docker
 % git clone https://github.com/docker/getting-started.git
Cloning into 'getting-started'...
remote: Enumerating objects: 762, done.
remote: Total 762 (delta 0), reused 0 (delta 0), pack-reused 762
Receiving objects: 100% (762/762), 3.71 MiB | 3.16 MiB/s, done.
Resolving deltas: 100% (426/426), done.

ichiro@ASUS-VivoBook ~/dev/docker
 % ls -l
合計 4
drwxrwxr-x 6 ichiro ichiro 4096  6月  5 01:40 getting-started


