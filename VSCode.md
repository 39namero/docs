# VSCode インストール

UbuntuにVSCodeをインストールする3つの方法
https://qiita.com/yoshiyasu1111/items/e21a77ed68b52cb5f7c8

1. マイクロソフトのリポジトリを登録する方法
2. Snapパッケージを利用する方法
3. debパッケージから直接インストール


## 「マイクロソフトのリポジトリを登録する方法」でインストール

curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg

ls -l
合計 4
-rw-rw-r-- 1 ichiro ichiro 641  6月  5 01:55 microsoft.gpg


ls -l /etc/apt/trusted.gpg.d/

sudo install -o root -g root -m 644 microsoft.gpg /etc/apt/trusted.gpg.d/

ls -l /etc/apt/trusted.gpg.d/                                            
合計 28
-rw-r--r-- 1 root root 7821  6月  4 09:51 google-chrome.gpg
-rw-r--r-- 1 root root  641  6月  5 01:57 microsoft.gpg
-rw-r--r-- 1 root root 1186  9月 28  2005 ubuntu-ja-archive-keyring.gpg
-rw-r--r-- 1 root root  367  4月 18  2009 ubuntu-jp-ppa-keyring.gpg
-rw-r--r-- 1 root root 2794  3月 27  2021 ubuntu-keyring-2012-cdimage.gpg
-rw-r--r-- 1 root root 1733  3月 27  2021 ubuntu-keyring-2018-archive.gpg


ls /etc/apt/sources.list.d/
docker.list  google-chrome.list  ubuntu-ja.list

sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'

ls /etc/apt/sources.list.d/
docker.list  google-chrome.list  ubuntu-ja.list  vscode.list


sudo apt install apt-transport-https

sudo apt update

apt list code

sudo apt list -a code

sudo apt install code


## 日本語化するには

https://pengi-n.co.jp/blog/vscode-install/

実際には自動的に日本語化が即されるため、とくにやることなし