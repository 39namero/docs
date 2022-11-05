# chrome インストール

https://postgresweb.com/install-google-chrome-ubuntu-20-04


## コマンド

リポジトリの追加

sudo sh -c 'echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list'

公開鍵のダウンロードと登録

sudo wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -

Google Chromeのインストール

sudo apt update

sudo apt install google-chrome-stable

