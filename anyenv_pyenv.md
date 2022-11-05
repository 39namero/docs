# anyenv pyenv の導入

「anyenv jenv の導入」の途中から。

anyenv install pyenv

exec $SHELL -l 

pyenv install --list

pyenv install 3.10.5

    Downloading Python-3.10.5.tar.xz...
    -> https://www.python.org/ftp/python/3.10.5/Python-3.10.5.tar.xz
    Installing Python-3.10.5...



    BUILD FAILED (Ubuntu 21.10 using python-build 2.3.2-10-gff9d3ca6)

    Inspect or clean up the working tree at /tmp/python-build.20220731131130.8435
    Results logged to /tmp/python-build.20220731131130.8435.log

    Last 10 log lines:
    File "/tmp/python-build.20220731131130.8435/Python-3.10.5/Lib/ensurepip/__init__.py", line 277, in _main
        return _bootstrap(
    File "/tmp/python-build.20220731131130.8435/Python-3.10.5/Lib/ensurepip/__init__.py", line 193, in _bootstrap
        return _run_pip([*args, *_PACKAGE_NAMES], additional_paths)
    File "/tmp/python-build.20220731131130.8435/Python-3.10.5/Lib/ensurepip/__init__.py", line 93, in _run_pip
        return subprocess.run([sys.executable, '-W', 'ignore::DeprecationWarning',
    File "/tmp/python-build.20220731131130.8435/Python-3.10.5/Lib/subprocess.py", line 524, in run
        raise CalledProcessError(retcode, process.args,
    subprocess.CalledProcessError: Command '['/tmp/python-build.20220731131130.8435/Python-3.10.5/python', '-W', 'ignore::DeprecationWarning', '-c', '\nimport runpy\nimport sys\nsys.path = [\'/tmp/tmp80a3iy08/setuptools-58.1.0-py3-none-any.whl\', \'/tmp/tmp80a3iy08/pip-22.0.4-py3-none-any.whl\'] + sys.path\nsys.argv[1:] = [\'install\', \'--no-cache-dir\', \'--no-index\', \'--find-links\', \'/tmp/tmp80a3iy08\', \'--root\', \'/\', \'--upgrade\', \'setuptools\', \'pip\']\nrunpy.run_module("pip", run_name="__main__", alter_sys=True)\n']' returned non-zero exit status 1.
    make: *** [Makefile:1280: install] エラー 1

ubuntuで自分の環境を作るメモ
https://gist.github.com/takanakahiko/8770623f93b43c51ed53ab5ecd5605e7

sudo apt-get install git gcc make openssl libssl-dev libbz2-dev libreadline-dev libsqlite3-dev
    〜
    E: リポジトリ http://jp.archive.ubuntu.com/ubuntu impish Release には Release ファイルがなくなっています。
    N: このようなリポジトリから更新を安全に行うことができないので、デフォルトでは更新が無効になっています。
    〜
    N: このようなリポジトリから更新を安全に行うことができないので、デフォルトでは更新が無効になっています。
    N: リポジトリの作成とユーザ設定の詳細は、apt-secure(8) man ページを参照してください。

lsb_release -a
    No LSB modules are available.
    Distributor ID:	Ubuntu
    Description:	Ubuntu 21.10
    Release:	21.10
    Codename:	impish

どうも impish がサポート切れになっているので、以下記事でリポジトリを書き換える。

Ubuntu 20.10でapt-get updateしたらエラーが出た
https://blog.denet.co.jp/i-got-an-error-when-i-did-apt-get-update-on-ubuntu-20-10/

別記事で対応

Ubuntu-21.10(impish)リポジトリ変更.md

sudo apt-get install git gcc make openssl libssl-dev libbz2-dev libreadline-dev libsqlite3-dev
echo $?                                                                                       
    0

成功！！

pyenv install 3.9.13

同じエラーになるのだな…

Ubuntuでpyenvがmake: *** [Makefile:1280: install] Error 1でインストールできない問題
https://qiita.com/prln/items/896b3ac3a871f3ea86ca

sudo apt install build-essential

sudo apt install libssl-dev libffi-dev libncurses5-dev zlib1g zlib1g-dev libreadline-dev libbz2-dev libsqlite3-dev make gcc

あらためて

pyenv install 3.10.5

    Downloading Python-3.10.5.tar.xz...
    -> https://www.python.org/ftp/python/3.10.5/Python-3.10.5.tar.xz
    Installing Python-3.10.5...
    WARNING: The Python tkinter extension was not compiled and GUI subsystem has been detected. Missing the Tk toolkit?
    WARNING: The Python lzma extension was not compiled. Missing the lzma lib?
    Installed Python-3.10.5 to /home/ichiro/.anyenv/envs/pyenv/versions/3.10.5

echo $?
    0

成功したけど警告でとるやん！！

ChromeBookでpyenvを導入してみた
https://qiita.com/barutou/items/80c31a7cdef930c75e90

なんだよ‥

sudo apt-get install libbz2-dev
sudo apt-get install tk-dev
sudo apt-get install liblzma-dev

いろいろいるんだよな

pyenv uninstall 3.10.5

pyenv install 3.10.5
    Downloading Python-3.10.5.tar.xz...
    -> https://www.python.org/ftp/python/3.10.5/Python-3.10.5.tar.xz
    Installing Python-3.10.5...
    Installed Python-3.10.5 to /home/ichiro/.anyenv/envs/pyenv/versions/3.10.5

pyenv install 3.9.13
    Downloading Python-3.9.13.tar.xz...
    -> https://www.python.org/ftp/python/3.9.13/Python-3.9.13.tar.xz
    Installing Python-3.9.13...
    Installed Python-3.9.13 to /home/ichiro/.anyenv/envs/pyenv/versions/3.9.13

 pyenv versions      
* system (set by /home/ichiro/.anyenv/envs/pyenv/version)
  3.9.13
  3.10.5

大成功やん！

python --version          
  pyenv: python: command not found

  The `python' command exists in these Python versions:
    3.9.13
    3.10.5

  Note: See 'pyenv help global' for tips on allowing both
        python2 and python3 to be found.

あれだな apt の python がないですな

pyenv global 3.10.5
pyenv versions     
    system
    3.9.13
  * 3.10.5 (set by /home/ichiro/.anyenv/envs/pyenv/version)
python --version
  Python 3.10.5
pip --version
  pip 22.0.4 from /home/ichiro/.anyenv/envs/pyenv/versions/3.10.5/lib/python3.10/site-packages/pip (python 3.10)

と、いうことね。

では、次になに？

poetry ですな

pip install poetry
echo $?
  0

pip list
  Package            Version
  ------------------ ---------
  CacheControl       0.12.11
  cachy              0.3.0
  certifi            2022.6.15
  cffi               1.15.1
  charset-normalizer 2.1.0
  cleo               0.8.1
  clikit             0.6.2
  crashtest          0.3.1
  cryptography       37.0.4
  distlib            0.3.5
  filelock           3.7.1
  html5lib           1.1
  idna               3.3
  jeepney            0.8.0
  keyring            23.7.0
  lockfile           0.12.2
  msgpack            1.0.4
  packaging          20.9
  pastel             0.2.1
  pexpect            4.8.0
  pip                22.0.4
  pkginfo            1.8.3
  platformdirs       2.5.2
  poetry             1.1.14
  poetry-core        1.0.8
  ptyprocess         0.7.0
  pycparser          2.21
  pylev              1.4.0
  pyparsing          3.0.9
  requests           2.28.1
  requests-toolbelt  0.9.1
  SecretStorage      3.3.2
  setuptools         58.1.0
  shellingham        1.4.0
  six                1.16.0
  tomlkit            0.11.1
  urllib3            1.26.11
  virtualenv         20.16.2
  webencodings       0.5.1
  WARNING: You are using pip version 22.0.4; however, version 22.2.1 is available.
  You should consider upgrading via the '/home/ichiro/.anyenv/envs/pyenv/versions/3.10.5/bin/python3.10 -m pip install --upgrade pip' command.

pyenv global 3.9.13

pip install poetry

echo $?            
  0



pyenv install  3.8.13

pyenv global 3.8.13

pip list
  Package    Version
  ---------- -------
  pip        22.0.4
  setuptools 56.0.0

pip install poetry

/home/ichiro/.anyenv/envs/pyenv/versions/3.8.13/bin/python3.8 -m pip install --upgrade pip

pip list
  Package            Version
  ------------------ ---------
  CacheControl       0.12.11
  cachy              0.3.0
  certifi            2022.6.15
  cffi               1.15.1
  charset-normalizer 2.1.0
  cleo               0.8.1
  clikit             0.6.2
  crashtest          0.3.1
  cryptography       37.0.4
  distlib            0.3.5
  filelock           3.7.1
  html5lib           1.1
  idna               3.3
  importlib-metadata 4.12.0
  jeepney            0.8.0
  keyring            23.7.0
  lockfile           0.12.2
  msgpack            1.0.4
  packaging          20.9
  pastel             0.2.1
  pexpect            4.8.0
  pip                22.2.1
  pkginfo            1.8.3
  platformdirs       2.5.2
  poetry             1.1.14
  poetry-core        1.0.8
  ptyprocess         0.7.0
  pycparser          2.21
  pylev              1.4.0
  pyparsing          3.0.9
  requests           2.28.1
  requests-toolbelt  0.9.1
  SecretStorage      3.3.2
  setuptools         56.0.0
  shellingham        1.4.0
  six                1.16.0
  tomlkit            0.11.1
  urllib3            1.26.11
  virtualenv         20.16.2
  webencodings       0.5.1
  zipp               3.8.1

poetry config --list
  cache-dir = "/home/ichiro/.cache/pypoetry"
  experimental.new-installer = true
  installer.parallel = true
  virtualenvs.create = true
  virtualenvs.in-project = null
  virtualenvs.path = "{cache-dir}/virtualenvs"  # /home/ichiro/.cache/pypoetry/virtualenvs

poetry config virtualenvs.in-project true

poetry config --list                     
  cache-dir = "/home/ichiro/.cache/pypoetry"
  experimental.new-installer = true
  installer.parallel = true
  virtualenvs.create = true
  virtualenvs.in-project = true
  virtualenvs.path = "{cache-dir}/virtualenvs"  # /home/ichiro/.cache/pypoetry/virtualenvs

