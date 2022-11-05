# virtualbox

以下いずれでもインストール可能であるが、どうするか？

* snap
* 素の apt リポジトリ
* dpkg パッケージダウンロード
* homebrew パッケージ

なんでも良さそうだが、ためしに　snap でインストールしてみるか

Ubuntu Software でインストールして

確認

ichiro@ASUS-VivoBook ~ % snap list
Name               Version             Rev    Tracking         Publisher     Notes
bare               1.0                 5      latest/stable    canonical✓    base
core               16-2.55.5           13250  latest/stable    canonical✓    core
core20             20220512            1494   latest/stable    canonical✓    base
firefox            101.0-2             1406   latest/stable/…  mozilla✓      -
gnome-3-38-2004    0+git.09fbd6c       106    latest/stable/…  canonical✓    -
gtk-common-themes  0.1-79-ga83e90c     1534   latest/stable/…  canonical✓    -
mc-installer       11.0                588    latest/stable    kz6fittycent  -
snap-store         3.38.0-66-gbd5b8f7  558    latest/stable/…  canonical✓    -

なぜでない？

ichiro@ASUS-VivoBook ~ % apt list --installed | grep virtual

WARNING: apt does not have a stable CLI interface. Use with caution in scripts.

virtualbox-dkms/impish-updates,now 6.1.32-dfsg-1~ubuntu1.21.10.1 amd64 [インストール済み、自動]
virtualbox-qt/impish-updates,now 6.1.32-dfsg-1~ubuntu1.21.10.1 amd64 [インストール済み]
virtualbox/impish-updates,now 6.1.32-dfsg-1~ubuntu1.21.10.1 amd64 [インストール済み、自動]

なんと！atp でインストールされていた！

健太朗の PC と同じであったが、以下のとおり問題あり！

プロバイダを virtualbox で実行してみる

```
% vagrant up --provider virtualbox
The provider 'virtualbox' that was requested to back the machine
'default' is reporting that it isn't usable on this system. The
reason is shown below:

VirtualBox is complaining that the installation is incomplete. Please
run `VBoxManage --version` to see the error message which should contain
instructions on how to fix this error.
```

irtualBox の環境が不完全なので `VBoxManage --version` を試せと言われる


```
 % VBoxManage --version
WARNING: The character device /dev/vboxdrv does not exist.
	 Please install the virtualbox-dkms package and the appropriate
	 headers, most likely linux-headers-generic.

	 You will not be able to start VMs until this problem is fixed.
6.1.32_Ubuntur149290
```

ここから完全に VirtualBox の問題となる
実は VirtualBox が使えていない事が判明したため、virtualbox のメモ「virtualbox.md」で管理していこう！

となり、以下続く


```
 % sudo ls -l /dev/vboxdrv
[sudo] ichiro のパスワード: 
ls: '/dev/vboxdrv' にアクセスできません: そのようなファイルやディレクトリはありません
``````

linux-headers-generic を入れれば良い？

```
 % apt list --installed | grep virtualbox

WARNING: apt does not have a stable CLI interface. Use with caution in scripts.

virtualbox-dkms/impish-updates,now 6.1.32-dfsg-1~ubuntu1.21.10.1 amd64 [インストール済み、自動]
virtualbox-qt/impish-updates,now 6.1.32-dfsg-1~ubuntu1.21.10.1 amd64 [インストール済み]
virtualbox/impish-updates,now 6.1.32-dfsg-1~ubuntu1.21.10.1 amd64 [インストール済み、自動]
```

```
 % apt list --installed | grep linux-headers-generic 

WARNING: apt does not have a stable CLI interface. Use with caution in scripts.

linux-headers-generic-hwe-20.04/impish-updates,impish-security,now 5.13.0.44.53 amd64 [インストール済み、自動]
```

インストールされてそうだけどなー

```
 % apt list linux-headers-generic  -a
一覧表示... 完了
linux-headers-generic/impish-updates,impish-security 5.13.0.44.53 amd64
linux-headers-generic/impish 5.13.0.19.30 amd64
```

 % sudo apt install linux-headers-generic

で、インストールしたパッケージを削除する

## よくわからなくなってきたので、アンインストールする

健太朗 PC にもないし

sudo apt remove --purge linux-headers-generic

```
[sudo] ichiro のパスワード: 
パッケージリストを読み込んでいます... 完了
依存関係ツリーを作成しています... 完了        
状態情報を読み取っています... 完了        
以下のパッケージが自動でインストールされましたが、もう必要とされていません:
  chromium-codecs-ffmpeg-extra gstreamer1.0-vaapi libfwupdplugin1 libgstreamer-plugins-bad1.0-0 libva-wayland2
これを削除するには 'sudo apt autoremove' を利用してください。
以下のパッケージは「削除」されます:
  linux-headers-generic*
アップグレード: 0 個、新規インストール: 0 個、削除: 1 個、保留: 0 個。
この操作後に 19.5 kB のディスク容量が解放されます。
続行しますか? [Y/n] y
(データベースを読み込んでいます ... 現在 219234 個のファイルとディレクトリがインストールされています。)
linux-headers-generic (5.13.0.44.53) を削除しています ...
```

