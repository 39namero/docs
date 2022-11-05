# ctrl と caps lock を入れ替える

コマンド一発でCapsLockをCtrlに変える方法
https://linuxfan.info/capslock-ctrl

CapsLockの動作を変更するコマンド（GNOME・Unity）
CapsLockキーとCtrlキーを入れ替える
gsettings set org.gnome.desktop.input-sources xkb-options "['ctrl:swapcaps']"


CapsLockキーをCtrlキーにする
gsettings set org.gnome.desktop.input-sources xkb-options "['ctrl:nocaps']"

CapsLockキーの設定を初期状態にリセットする
gsettings reset org.gnome.desktop.input-sources xkb-options


コンソールでもCapsLockの動作を変更する方法（UbuntuなどDebian系）
CapsLockキーとCtrlキーを入れ替える
XKBOPTIONS="ctrl:swapcaps"
設定を反映
sudo systemctl restart console-setup


CapsLockキーをCtrlキーにする
XKBOPTIONS="ctrl:nocaps"

