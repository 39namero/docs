# byobu_install


sudo apt search byobu
    [sudo] ichiro のパスワード: 
    ソート中... 完了
    全文検索... 完了  
    byobu/impish,impish 5.133-0ubuntu1 all
    text window manager, shell multiplexer, integrated DevOps environment

sudo apt install byobu
    パッケージリストを読み込んでいます... 完了
    依存関係ツリーを作成しています... 完了        
    状態情報を読み取っています... 完了        
    以下のパッケージが自動でインストールされましたが、もう必要とされていません:
    chromium-codecs-ffmpeg-extra gstreamer1.0-vaapi libfwupdplugin1 libgstreamer-plugins-bad1.0-0
    これを削除するには 'sudo apt autoremove' を利用してください。
    以下の追加パッケージがインストールされます:
    libutempter0 pastebinit python3-newt run-one tmux
    提案パッケージ:
    ccze po-debconf screen speedometer ttf-ubuntu-font-family
    以下のパッケージが新たにインストールされます:
    byobu libutempter0 pastebinit python3-newt run-one tmux
    アップグレード: 0 個、新規インストール: 6 個、削除: 0 個、保留: 0 個。
    502 kB のアーカイブを取得する必要があります。
    この操作後に追加で 1,838 kB のディスク容量が消費されます。
    続行しますか? [Y/n] y
    取得:1 https://old-releases.ubuntu.com/ubuntu impish/main amd64 python3-newt amd64 0.52.21-4ubuntu7 [21.4 kB]
    取得:2 https://old-releases.ubuntu.com/ubuntu impish/main amd64 libutempter0 amd64 1.2.1-2 [8,860 B]
    取得:3 https://old-releases.ubuntu.com/ubuntu impish/main amd64 tmux amd64 3.1c-1build1 [351 kB]
    取得:4 https://old-releases.ubuntu.com/ubuntu impish/main amd64 byobu all 5.133-0ubuntu1 [101 kB]
    取得:5 https://old-releases.ubuntu.com/ubuntu impish/main amd64 pastebinit all 1.5.1-1 [14.2 kB]
    取得:6 https://old-releases.ubuntu.com/ubuntu impish/main amd64 run-one all 1.17-0ubuntu1 [5,760 B]
    502 kB を 4秒 で取得しました (143 kB/s)
    パッケージを事前設定しています ...
    以前に未選択のパッケージ python3-newt:amd64 を選択しています。
    (データベースを読み込んでいます ... 現在 224025 個のファイルとディレクトリがインストールされています。)
    .../0-python3-newt_0.52.21-4ubuntu7_amd64.deb を展開する準備をしています ...
    python3-newt:amd64 (0.52.21-4ubuntu7) を展開しています...
    以前に未選択のパッケージ libutempter0:amd64 を選択しています。
    .../1-libutempter0_1.2.1-2_amd64.deb を展開する準備をしています ...
    libutempter0:amd64 (1.2.1-2) を展開しています...
    以前に未選択のパッケージ tmux を選択しています。
    .../2-tmux_3.1c-1build1_amd64.deb を展開する準備をしています ...
    tmux (3.1c-1build1) を展開しています...
    以前に未選択のパッケージ byobu を選択しています。
    .../3-byobu_5.133-0ubuntu1_all.deb を展開する準備をしています ...
    byobu (5.133-0ubuntu1) を展開しています...
    以前に未選択のパッケージ pastebinit を選択しています。
    .../4-pastebinit_1.5.1-1_all.deb を展開する準備をしています ...
    pastebinit (1.5.1-1) を展開しています...
    以前に未選択のパッケージ run-one を選択しています。
    .../5-run-one_1.17-0ubuntu1_all.deb を展開する準備をしています ...
    run-one (1.17-0ubuntu1) を展開しています...
    pastebinit (1.5.1-1) を設定しています ...
    python3-newt:amd64 (0.52.21-4ubuntu7) を設定しています ...
    libutempter0:amd64 (1.2.1-2) を設定しています ...
    run-one (1.17-0ubuntu1) を設定しています ...
    tmux (3.1c-1build1) を設定しています ...
    byobu (5.133-0ubuntu1) を設定しています ...
    libc-bin (2.34-0ubuntu3.2) のトリガを処理しています ...
    man-db (2.9.4-2) のトリガを処理しています ...
    hicolor-icon-theme (0.17-2) のトリガを処理しています ...

apt list --installed | grep byobu

    byobu/impish,impish,now 5.133-0ubuntu1 all [インストール済み]

byobu

    Welcome to the light, powerful, text window manager, Byobu.
    You can toggle the launch of Byobu at login with:
    'byobu-disable' and 'byobu-enable'

    For tips, tricks, and more information, see:
    * https://bit.ly/byobu-tips

