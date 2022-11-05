# anyenv jenv の導入

brew install anyenv

ichiro@ASUS-VivoBook ~ % brew install anyenv
Running `brew update --preinstall`...
==> Auto-updated Homebrew!
Updated 1 tap (homebrew/core).
==> Updated Formulae
Updated 3 formulae.

Warning: anyenv 1.1.4 is already installed and up-to-date.
To reinstall 1.1.4, run:
  brew reinstall anyenv

echo 'eval "$(anyenv init -)"' >> ~/.zshrc

vi .zshrc 
〜
# 2022.6.1 add anyenv
eval "$(anyenv init -)"

anyenv install --init

Manifest directory doesn't exist: /home/ichiro/.config/anyenv/anyenv-install
Do you want to checkout https://github.com/anyenv/anyenv-install.git? [y/N]: y
Cloning https://github.com/anyenv/anyenv-install.git master to /home/ichiro/.config/anyenv/anyenv-install...
Cloning into '/home/ichiro/.config/anyenv/anyenv-install'...
remote: Enumerating objects: 71, done.
remote: Counting objects: 100% (14/14), done.
remote: Compressing objects: 100% (13/13), done.
remote: Total 71 (delta 4), reused 3 (delta 1), pack-reused 57
Receiving objects: 100% (71/71), 13.15 KiB | 6.58 MiB/s, done.
Resolving deltas: 100% (11/11), done.

Completed!

exec $SHELL -l

anyenv versions

anyenv install -l
  Renv
  crenv
  denv
  erlenv
  exenv
  goenv
  hsenv
  jenv
  jlenv
  kubectlenv
  luaenv
  nodenv
  phpenv
  plenv
  pyenv
  rbenv
  sbtenv
  scalaenv
  swiftenv
  tfenv


anyenv install jenv

/tmp/jenv.20220601222838.17884 ~
Cloning https://github.com/jenv/jenv.git master to jenv...
Cloning into 'jenv'...
remote: Enumerating objects: 1335, done.
remote: Counting objects: 100% (116/116), done.
remote: Compressing objects: 100% (73/73), done.
remote: Total 1335 (delta 58), reused 86 (delta 37), pack-reused 1219
Receiving objects: 100% (1335/1335), 465.78 KiB | 2.95 MiB/s, done.
Resolving deltas: 100% (619/619), done.
~

Install jenv succeeded!
Please reload your profile (exec $SHELL -l) or open a new session.

exec $SHELL -l     

jenv has been updated, process to refresh plugin links

anyenv versions
jenv:
* system (set by /home/ichiro/.anyenv/envs/jenv/version)

which java

/usr/bin/java


ls -l /usr/bin/java

lrwxrwxrwx 1 root root 22  5月 29 15:41 /usr/bin/java -> /etc/alternatives/java
ichiro@ASUS-VivoBook ~ % ls -l /etc/alternatives/java
lrwxrwxrwx 1 root root 43  5月 30 23:41 /etc/alternatives/java -> /usr/lib/jvm/java-17-openjdk-amd64/bin/java


ls -l /usr/lib/jvm 
合計 20
lrwxrwxrwx 1 root root   25 10月  7  2021 default-java -> java-1.11.0-openjdk-amd64
lrwxrwxrwx 1 root root   21  4月 23 22:02 java-1.11.0-openjdk-amd64 -> java-11-openjdk-amd64
lrwxrwxrwx 1 root root   21  4月 24 23:03 java-1.17.0-openjdk-amd64 -> java-17-openjdk-amd64
lrwxrwxrwx 1 root root   20 11月  3  2021 java-1.8.0-openjdk-amd64 -> java-8-openjdk-amd64
drwxr-xr-x 9 root root 4096  5月 30 23:19 java-11-openjdk-amd64
drwxr-xr-x 9 root root 4096  5月 30 23:41 java-17-openjdk-amd64
drwxr-xr-x 7 root root 4096  5月 30 23:35 java-8-openjdk-amd64
drwxr-xr-x 2 root root 4096  5月 30 23:19 openjdk-11
drwxr-xr-x 2 root root 4096  5月 30 23:41 openjdk-17


jenv add /usr/lib/jvm/java-1.11.0-openjdk-amd64 
openjdk64-11.0.15 added
11.0.15 added
11.0 added
11 added
ichiro@ASUS-VivoBook ~ % jenv versions                                  
* system (set by /home/ichiro/.anyenv/envs/jenv/version)
  11
  11.0
  11.0.15
  openjdk64-11.0.15


jenv add java-1.17.0-openjdk-amd64                
java-1.17.0-openjdk-amd64 is not a valid path to java installation
ichiro@ASUS-VivoBook ~ % jenv add /usr/lib/jvm/java-1.17.0-openjdk-amd64   
openjdk64-17.0.3 added
17.0.3 added
17.0 added
17 added

jenv add /usr/lib/jvm/java-1.8.0-openjdk-amd64 
openjdk64-1.8.0.312 added
1.8.0.312 added
1.8 added

jenv versions                                 
* system (set by /home/ichiro/.anyenv/envs/jenv/version)
  1.8
  1.8.0.312
  11
  11.0
  11.0.15
  17
  17.0
  17.0.3
  openjdk64-1.8.0.312
  openjdk64-11.0.15
  openjdk64-17.0.3


jenv versions  
    system
    1.8
    1.8.0.312
    1.8.0.332
    11
    11.0
    11.0.15
    17
    17.0
    17.0.3
    openjdk64-1.8.0.312
    openjdk64-11.0.15
    openjdk64-17.0.3
    semeru64-1.8.0.332
    semeru64-11.0.15
  * semeru64-17.0.3 (set by /home/ichiro/.anyenv/envs/jenv/version)
    temurin64-1.8.0.332
    temurin64-11.0.15
    temurin64-17.0.3


java -version
  openjdk version "17.0.3" 2022-04-19
  IBM Semeru Runtime Open Edition 17.0.3.0 (build 17.0.3+7)
  Eclipse OpenJ9 VM 17.0.3.0 (build openj9-0.32.0, JRE 17 Linux amd64-64-Bit Compressed References 20220422_184 (JIT enabled, AOT enabled)
  OpenJ9   - 9a84ec34e
  OMR      - ab24b6666
  JCL      - dc07fd49b92 based on jdk-17.0.3+7)

デフォルトでは JAVA_HOME 環境変数に何もセットされない

echo $JAVA_HOME

export プラグインを有効にすることで JAVA_HOME に自動的に値がセットされる

jenv enable-plugin export
  You may restart your session to activate jenv export plugin echo export plugin activated

echo $JAVA_HOME
  /home/ichiro/.anyenv/envs/jenv/versions/semeru64-17.0.3



jenv disable-plugin maven
jenv disable-plugin export
jenv enable-plugin maven
jenv enable-plugin export