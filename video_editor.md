# 動画編集

Top 10 Best Professional Video Editors in 2022
https://www.debugpoint.com/best-free-video-editors-linux-ubuntu/



## 1. Blender（済）

既にインストール済み

## 2. Lightworks

公式サイトでアカウントを登録する

LWKS
https://lwks.com/

ikentaro24@gmail.com
Kenta@2424
kuwoso24

ダウンロードサイトに飛ぶので、無料のをダウンロードする

```
 % pwd
/home/kentaro/ダウンロード
kentaro@kentaro-optiplex-3020 ~/ダウンロード
 % ls -l lightworks_2022.3_r137093.deb
-rw-rw-r-- 1 kentaro kentaro 81325780 10月  1 11:03 lightworks_2022.3_r137093.deb
```

インストールする

sudo dpkg -i lightworks_2022.3_r137093.deb

```
[sudo] kentaro のパスワード: 
〜
dpkg: 依存関係の問題により lightworks の設定ができません:
 lightworks は以下に依存 (depends) します: libpango1.0-0 (>= 1.18.0) ...しかし:
  パッケージ libpango1.0-0 はまだインストールされていません。
 lightworks は以下に依存 (depends) します: nvidia-cg-toolkit ...しかし:
  パッケージ nvidia-cg-toolkit はまだインストールされていません。
 lightworks は以下に依存 (depends) します: libc++1 ...しかし:
  パッケージ libc++1 はまだインストールされていません。

dpkg: パッケージ lightworks の処理中にエラーが発生しました (--install):
 依存関係の問題 - 設定を見送ります
〜
処理中にエラーが発生しました:
 lightworks
```

* libpango1.0-0
* nvidia-cg-toolkit
* libc++1

sudo apt search libpango1.0-0
sudo apt search nvidia-cg-toolkit
sudo apt search libc++1

```
 % sudo apt install nvidia-cg-toolkit libpango1.0-0 libc++1
パッケージリストを読み込んでいます... 完了
依存関係ツリーを作成しています... 完了        
状態情報を読み取っています... 完了        
これらを直すためには 'apt --fix-broken install' を実行する必要があるかもしれません。
以下のパッケージには満たせない依存関係があります:
 libc++1 : 依存: libc++1-13 (>= 13~) しかし、インストールされようとしていません
 nvidia-cg-toolkit : 依存: libcg (= 3.1.0013-5) しかし、インストールされようとしていません
                     依存: libcggl (= 3.1.0013-5) しかし、インストールされようとしていません
                     依存: nvidia-cg-dev (= 3.1.0013-5) しかし、インストールされようとしていません
                     依存: freeglut3 しかし、インストールされようとしていません
E: 未解決の依存関係です。'apt --fix-broken install' を実行してみてください (または解法を明示してください)。
```

sudo apt --fix-broken install

```
 % sudo apt --fix-broken install
〜
以下のパッケージが自動でインストールされましたが、もう必要とされていません:
  chromium-codecs-ffmpeg-extra libfwupdplugin1
これを削除するには 'sudo apt autoremove' を利用してください。
〜
以下の追加パッケージがインストールされます:
  freeglut3 libc++1 libc++1-13 libc++abi1-13 libcg libcggl libpango1.0-0 libunwind-13 nvidia-cg-dev nvidia-cg-toolkit
提案パッケージ:
  clang libpangox-1.0-0 nvidia-cg-doc
以下のパッケージが新たにインストールされます:
  freeglut3 libc++1 libc++1-13 libc++abi1-13 libcg libcggl libpango1.0-0 libunwind-13 nvidia-cg-dev nvidia-cg-toolkit
〜
 % echo $?
0
```

sudo dpkg -i lightworks_2022.3_r137093.deb

```
 % sudo dpkg -i lightworks_2022.3_r137093.deb
(データベースを読み込んでいます ... 現在 271756 個のファイルとディレクトリがインストールされています。)
lightworks_2022.3_r137093.deb を展開する準備をしています ...
lightworks (2022.3) で (2022.3 に) 上書き展開しています ...
lightworks (2022.3) を設定しています ...
mailcap (3.69ubuntu1) のトリガを処理しています ...
gnome-menus (3.36.0-1ubuntu1) のトリガを処理しています ...
desktop-file-utils (0.26-1ubuntu2) のトリガを処理しています ...
fontconfig (2.13.1-4.2ubuntu3) のトリガを処理しています ...
kentaro@kentaro-optiplex-3020 ~/ダウンロード
 % echo $?
0
```

sudo dpkg -l | grep lightworks

```
ii  lightworks                                    2022.3                                     amd64        Hollywood-strength editing for everyone
```

## 3. Shotcut（済）

既にインストール済み


## 4. Avidemux（却下）

https://avidemux.sourceforge.net/download.html
https://launchpad.net/~xtradeb/+archive/ubuntu/apps
https://launchpad.net/~xtradeb

面白そうだけど、諸々設定が必要なので却下しよう

## 5. HitFilm Express（却下）

FXhome
https://fxhome.com/product/hitfilm


ikentaro24@gmail.com
Kenta@2424
kuwoso24 nishi

Windows Mac 版の提供しかないので却下

## 6. DaVinci Resolve


DaVinci Resolve 18
https://www.blackmagicdesign.com/products/davinciresolve/

ikentaro24@gmail.com
Kenta@2424
kuwoso24 nishi

```
 % ls -l DaVinci_Resolve_18.0.4_Linux.zip 
-rw-rw-r-- 1 kentaro kentaro 3128059055 10月  1 13:10 DaVinci_Resolve_18.0.4_Linux.zip
```

```
 % unzip DaVinci_Resolve_18.0.4_Linux.zip 
Archive:  DaVinci_Resolve_18.0.4_Linux.zip
  inflating: DaVinci_Resolve_18.0.4_Linux.run  

  inflating: Linux_Installation_Instructions.pdf  
```

```
 % ls -l DaVinci_Resolve_18.0.4_Linux.run
-rwxr-xr-x 1 kentaro kentaro 3151346080  9月 29 21:29 DaVinci_Resolve_18.0.4_Linux.run
kentaro@kentaro-optiplex-3020 ~/ダウンロード
 % ./DaVinci_Resolve_18.0.4_Linux.run
```


## 7. OpenShot（済）

既にインストール済み


## 8. KDenlive（済）

既にインストール済み

## 9. Flowblade（済）

既にインストール済み

## 10. Olive

olivevideoeditor
https://www.olivevideoeditor.org/index.php

apt よりインストール

```
 % sudo apt list olive-editor
[sudo] kentaro のパスワード: 
一覧表示... 完了
olive-editor/impish 20200620-2ubuntu4 amd64
kentaro@kentaro-optiplex-3020 ~/ダウンロード
 % sudo apt install olive-editor
〜
以下のパッケージが新たにインストールされます:
  olive-editor
〜
```

## 結果新たにインストールした動画編集ソフト

2. Lightworks LWKS[https://lwks.com/]
6. DaVinci Resolve blackmagicdesign[https://www.blackmagicdesign.com/products/davinciresolve/]
10. Olive olivevideoeditor[https://www.olivevideoeditor.org/index.php]



