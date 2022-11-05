# keyboard layout 言語セッティング

## 正解・これだけでよいかもしれない

VM Ubuntuでキーボードを日本語配列に – 入力がおかしい場合にkeyboard layoutがUSになっているのを変更する
https://what-a-day.net/vm-keyboard-layout

setxkbmap -print -verbose 10

〜
layout:     us
〜

setxkbmap -layout jp

setxkbmap -print -verbose 10

〜
layout:     jp
〜

## X(GUI)で使うキーボードレイアウトの設定

で、順番を入れ替えたが、これをやると完成かもしれない

X(GUI)で使うキーボードレイアウトの設定（X ではないのだが）
https://qiita.com/vochicong/items/6452ac54bde56b0e0bb3

gnome-session-properties

add

以下、新規定義を追加

Set JP keyboad on X startup

setxkbmap -layout jp



save

close


"setxkbmap jp" と記載があったが、それが間違いだったのでは？

## 以下も不要とは言えないかもしれない

Ubuntuキーボードレイアウト変更手順
https://golang.hateblo.jp/entry/ubuntu-keyboard-layout


### TUIで候補から選択していく

sudo dpkg-reconfigure keyboard-configuration

### 以下対話的に入力する

Keyboard model:

  Generic 105-key (Intl) PC


Country of origin for the keyboard:

  Japanese


Keyboard layout:

  Japanese


Key to function as AltGr:

  The default for the keyboard layout


Compose Key:

  No compose key


Use Control+Alt+Backspace to terminate the X server?

  <No>

### mozcのレイアウトを ja に変更


cp -p .config/mozc/ibus_config.textproto .config/mozc/ibus_config.textproto.bk20220529
vi .config/mozc/ibus_config.textproto


diff .config/mozc/ibus_config.textproto.bk20220529 .config/mozc/ibus_config.textproto
4c4
<   layout : "default"
---
>   layout : "ja"


sudo reboot




## 謎事象


System SetingsからLanguage Supportを選択すると、
なぜか、en 関連の必要パッケージのダウンロードが即された。
指示に従いダウンロードを行った。




## 残項目

半角円マークが、バックスラッシュになるがどうするか？このままで良いか？

バックスラッシュと円記号の悲劇
https://juangotoh.hatenablog.com/entry/2016/06/13/104139

入力切替がやりにくすぎる。Mac のショートカットに合わせたいができるのか？

