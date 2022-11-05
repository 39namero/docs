# java インストールなど

## 現在

ichiro@ASUS-VivoBook:~$ java --version
openjdk 11.0.15 2022-04-19
OpenJDK Runtime Environment (build 11.0.15+10-Ubuntu-0ubuntu0.21.10.1)
OpenJDK 64-Bit Server VM (build 11.0.15+10-Ubuntu-0ubuntu0.21.10.1, mixed mode)


ichiro@ASUS-VivoBook:~$ sudo dpkg -l | grep openjdk
ii  openjdk-11-jre:amd64                       11.0.15+10-0ubuntu0.21.10.1                amd64        OpenJDK Java runtime, using Hotspot JIT
ii  openjdk-11-jre-headless:amd64              11.0.15+10-0ubuntu0.21.10.1                amd64        OpenJDK Java runtime, using Hotspot JIT (headless)

ichiro@ASUS-VivoBook:~$ sudo dpkg -l | grep default-jre
ii  default-jre                                2:1.11-72build1                            amd64        Standard Java or Java compatible Runtime
ii  default-jre-headless                       2:1.11-72build1                            amd64        Standard Java or Java compatible Runtime (headless)

default-jre（openjdk-11-jre:）のみインストールされている


## 候補

### Ubuntu デフォルトの OpenJDK

Ubuntu 21.04にJava（OpenJDK）をインストールする
https://self-development.infoUbuntu 21.04にJava（OpenJDK）をインストールする

sudo apt search "^openjdk.*jdk$"

ichiro@ASUS-VivoBook:~$ sudo apt search "^openjdk.*jdk$"
ソート中... 完了
全文検索... 完了  
openjdk-11-jdk/impish-updates,impish-security 11.0.15+10-0ubuntu0.21.10.1 amd64
  OpenJDK Development Kit (JDK)

openjdk-16-jdk/impish 16.0.2+7-2 amd64
  OpenJDK Development Kit (JDK)

openjdk-17-jdk/impish-updates,impish-security 17.0.3+7-0ubuntu0.21.10.1 amd64
  OpenJDK Development Kit (JDK)

openjdk-18-jdk/impish 18~15ea-4 amd64
  OpenJDK Development Kit (JDK)

openjdk-8-jdk/impish-updates,impish-security 8u312-b07-0ubuntu1~21.10 amd64
  OpenJDK Development Kit (JDK)

この中で、8 11 17 が LTS なので、候補とする。（全部入れる？）

Oracle Java SE Supportロードマップ
https://www.oracle.com/jp/java/technologies/java-se-support-roadmap.html

ちなみにデフォルトの OpenJDK がどこ由来なのかがちょっと不明

### AdoptOpenJDK は利用できない？

IBM Semeru Runtimes 無償で利用できる新しいJava実行環境
https://qiita.com/TTakakiyo/items/7a0f3bab4313a3e84c9e

* OpenJDKのディストリビューションAdoptOpenJDKは，2021年7月末で更新を終了
* 2021年8月以降は以下 HotSpot OpenJ9 別々に配布されている
  * OpenJDK + HotSpot : Eclipse Adoptiumプロジェクト - Eclipse Temurin
  * OpenJDK + OpenJ9 : IBM Developerサイト - IBM Semeru Runtimes


https://adoptopenjdk.net/
https://adoptium.net/temurin/
https://developer.ibm.com/languages/java/semeru-runtimes/downloads/

おそらく 2020 年ごろで情報の更新が止まっており、
ベストな解（リポジトリ追加・インストール）はできない感じ。
各サイトからダウンロード、直接インストールになると思われる。

Mac 同様に homebrew からインストールできる可能性もあるが、一旦保留する？


## インストール

### Ubuntu デフォルトの OpenJDK

全部インストールしちまおう！切り替えはあとで考えよう！

* openjdk-8-jdk
* openjdk-11-jdk ( default-jdk )
* openjdk-17-jdk

まずは default-jdk をインストールしてどうなるかを確認したい。

ichiro@ASUS-VivoBook:~/minecraft-server/vanilla-1.18.2$ java --version
openjdk 11.0.15 2022-04-19
OpenJDK Runtime Environment (build 11.0.15+10-Ubuntu-0ubuntu0.21.10.1)
OpenJDK 64-Bit Server VM (build 11.0.15+10-Ubuntu-0ubuntu0.21.10.1, mixed mode)

ichiro@ASUS-VivoBook:~$ which java
/usr/bin/java
ichiro@ASUS-VivoBook:~$ ls -l /usr/bin/java
lrwxrwxrwx 1 root root 22  5月 29 15:41 /usr/bin/java -> /etc/alternatives/java
ichiro@ASUS-VivoBook:~$ ls -l /etc/alternatives/java
lrwxrwxrwx 1 root root 43  5月 29 15:41 /etc/alternatives/java -> /usr/lib/jvm/java-11-openjdk-amd64/bin/java
ichiro@ASUS-VivoBook:~$ ls -l /etc/alternatives/java
lrwxrwxrwx 1 root root 43  5月 29 15:41 /etc/alternatives/java -> /usr/lib/jvm/java-11-openjdk-amd64/bin/java
ichiro@ASUS-VivoBook:~$ ls -l /usr/lib/jvm/java-1*
lrwxrwxrwx 1 root root   21  4月 23 22:02 /usr/lib/jvm/java-1.11.0-openjdk-amd64 -> java-11-openjdk-amd64

/usr/lib/jvm/java-11-openjdk-amd64:
合計 24
drwxr-xr-x  2 root root 4096  5月 29 15:41 bin
drwxr-xr-x  4 root root 4096  5月 29 15:41 conf
lrwxrwxrwx  1 root root   42  4月 23 22:02 docs -> ../../../share/doc/openjdk-11-jre-headless
drwxr-xr-x 73 root root 4096  5月 29 15:41 legal
drwxr-xr-x  6 root root 4096  5月 29 15:43 lib
drwxr-xr-x  4 root root 4096  5月 29 15:41 man
-rw-r--r--  1 root root 1185  4月 23 22:02 release



ichiro@ASUS-VivoBook:~$ apt list default-jdk 
一覧表示... 完了
default-jdk/impish 2:1.11-72build1 amd64
default-jdk/impish 2:1.11-72build1 i386

ichiro@ASUS-VivoBook:~$ sudo apt install default-jdk
〜

ichiro@ASUS-VivoBook:~$ java -version
openjdk version "11.0.15" 2022-04-19
OpenJDK Runtime Environment (build 11.0.15+10-Ubuntu-0ubuntu0.21.10.1)
OpenJDK 64-Bit Server VM (build 11.0.15+10-Ubuntu-0ubuntu0.21.10.1, mixed mode)

ichiro@ASUS-VivoBook:~$ which java
/usr/bin/java
ichiro@ASUS-VivoBook:~$ ls -l /usr/bin/java
lrwxrwxrwx 1 root root 22  5月 29 15:41 /usr/bin/java -> /etc/alternatives/java
ichiro@ASUS-VivoBook:~$ ls -l /etc/alternatives/java
lrwxrwxrwx 1 root root 43  5月 29 15:41 /etc/alternatives/java -> /usr/lib/jvm/java-11-openjdk-amd64/bin/java
ichiro@ASUS-VivoBook:~$ sudo ls -l /usr/lib/jvm/java-11-openjdk-amd64/bin/java
-rwxr-xr-x 1 root root 14560  4月 23 22:02 /usr/lib/jvm/java-11-openjdk-amd64/bin/java
ichiro@ASUS-VivoBook:~$ sudo ls -l /usr/lib/jvm/java-11-openjdk-amd64
合計 32
drwxr-xr-x  2 root root 4096  5月 30 23:19 bin
drwxr-xr-x  4 root root 4096  5月 29 15:41 conf
lrwxrwxrwx  1 root root   42  4月 23 22:02 docs -> ../../../share/doc/openjdk-11-jre-headless
drwxr-xr-x  3 root root 4096  5月 30 23:19 include
drwxr-xr-x  2 root root 4096  5月 30 23:19 jmods
drwxr-xr-x 73 root root 4096  5月 29 15:41 legal
drwxr-xr-x  6 root root 4096  5月 30 23:19 lib
drwxr-xr-x  4 root root 4096  5月 29 15:41 man
-rw-r--r--  1 root root 1185  4月 23 22:02 release
ichiro@ASUS-VivoBook:~$ sudo ls -l /usr/lib/jvm/
合計 8
lrwxrwxrwx 1 root root   25 10月  7  2021 default-java -> java-1.11.0-openjdk-amd64
lrwxrwxrwx 1 root root   21  4月 23 22:02 java-1.11.0-openjdk-amd64 -> java-11-openjdk-amd64
drwxr-xr-x 9 root root 4096  5月 30 23:19 java-11-openjdk-amd64
drwxr-xr-x 2 root root 4096  5月 30 23:19 openjdk-11

ichiro@ASUS-VivoBook:~$ sudo ls -l /usr/lib/jvm/
合計 8
lrwxrwxrwx 1 root root   25 10月  7  2021 default-java -> java-1.11.0-openjdk-amd64
lrwxrwxrwx 1 root root   21  4月 23 22:02 java-1.11.0-openjdk-amd64 -> java-11-openjdk-amd64
drwxr-xr-x 9 root root 4096  5月 30 23:19 java-11-openjdk-amd64
drwxr-xr-x 2 root root 4096  5月 30 23:19 openjdk-11

ichiro@ASUS-VivoBook:~$ which javac
/usr/bin/javac
ichiro@ASUS-VivoBook:~$ ls -l /usr/bin/javac
lrwxrwxrwx 1 root root 23  5月 30 23:19 /usr/bin/javac -> /etc/alternatives/javac
ichiro@ASUS-VivoBook:~$ ls -l /etc/alternatives/javac
lrwxrwxrwx 1 root root 44  5月 30 23:19 /etc/alternatives/javac -> /usr/lib/jvm/java-11-openjdk-amd64/bin/javac
ichiro@ASUS-VivoBook:~$ ls -l /usr/lib/jvm/java-11-openjdk-amd64/bin/javac
-rwxr-xr-x 1 root root 14608  4月 23 22:02 /usr/lib/jvm/java-11-openjdk-amd64/bin/javac

#### openjdk-8-jdk

ichiro@ASUS-VivoBook:~$ sudo apt install openjdk-8-jdk
〜

ichiro@ASUS-VivoBook:~$ java -version
openjdk version "11.0.15" 2022-04-19
OpenJDK Runtime Environment (build 11.0.15+10-Ubuntu-0ubuntu0.21.10.1)
OpenJDK 64-Bit Server VM (build 11.0.15+10-Ubuntu-0ubuntu0.21.10.1, mixed mode)
ichiro@ASUS-VivoBook:~$ which java
/usr/bin/java
ichiro@ASUS-VivoBook:~$ ls -l /usr/bin/java
lrwxrwxrwx 1 root root 22  5月 29 15:41 /usr/bin/java -> /etc/alternatives/java
ichiro@ASUS-VivoBook:~$ ls -l /etc/alternatives/java
lrwxrwxrwx 1 root root 43  5月 29 15:41 /etc/alternatives/java -> /usr/lib/jvm/java-11-openjdk-amd64/bin/java
ichiro@ASUS-VivoBook:~$ ls -l /usr/lib/jvm/java-11-openjdk-amd64/bin/java
-rwxr-xr-x 1 root root 14560  4月 23 22:02 /usr/lib/jvm/java-11-openjdk-amd64/bin/java
ichiro@ASUS-VivoBook:~$ ls -l /usr/lib/jvm/java-11-openjdk-amd64
合計 32
drwxr-xr-x  2 root root 4096  5月 30 23:19 bin
drwxr-xr-x  4 root root 4096  5月 29 15:41 conf
lrwxrwxrwx  1 root root   42  4月 23 22:02 docs -> ../../../share/doc/openjdk-11-jre-headless
drwxr-xr-x  3 root root 4096  5月 30 23:19 include
drwxr-xr-x  2 root root 4096  5月 30 23:19 jmods
drwxr-xr-x 73 root root 4096  5月 29 15:41 legal
drwxr-xr-x  6 root root 4096  5月 30 23:19 lib
drwxr-xr-x  4 root root 4096  5月 29 15:41 man
-rw-r--r--  1 root root 1185  4月 23 22:02 release
ichiro@ASUS-VivoBook:~$ ls -l /usr/lib/jvm
合計 12
lrwxrwxrwx 1 root root   25 10月  7  2021 default-java -> java-1.11.0-openjdk-amd64
lrwxrwxrwx 1 root root   21  4月 23 22:02 java-1.11.0-openjdk-amd64 -> java-11-openjdk-amd64
lrwxrwxrwx 1 root root   20 11月  3  2021 java-1.8.0-openjdk-amd64 -> java-8-openjdk-amd64
drwxr-xr-x 9 root root 4096  5月 30 23:19 java-11-openjdk-amd64
drwxr-xr-x 7 root root 4096  5月 30 23:35 java-8-openjdk-amd64
drwxr-xr-x 2 root root 4096  5月 30 23:19 openjdk-11

ichiro@ASUS-VivoBook:~$ java -version
openjdk version "17.0.3" 2022-04-19
OpenJDK Runtime Environment (build 17.0.3+7-Ubuntu-0ubuntu0.21.10.1)
OpenJDK 64-Bit Server VM (build 17.0.3+7-Ubuntu-0ubuntu0.21.10.1, mixed mode, sharing)
ichiro@ASUS-VivoBook:~$ which java
/usr/bin/java
ichiro@ASUS-VivoBook:~$ ls -l /usr/bin/java
lrwxrwxrwx 1 root root 22  5月 29 15:41 /usr/bin/java -> /etc/alternatives/java
ichiro@ASUS-VivoBook:~$ ls -l /etc/alternatives/java
lrwxrwxrwx 1 root root 43  5月 30 23:41 /etc/alternatives/java -> /usr/lib/jvm/java-17-openjdk-amd64/bin/java
ichiro@ASUS-VivoBook:~$ ls -l /usr/lib/jvm/java-17-openjdk-amd64/bin/java
-rwxr-xr-x 1 root root 14496  4月 24 23:03 /usr/lib/jvm/java-17-openjdk-amd64/bin/java
ichiro@ASUS-VivoBook:~$ ls -l /usr/lib/jvm
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

ichiro@ASUS-VivoBook:~$ sudo dpkg -l | grep openjdk
ii  openjdk-11-jdk:amd64                       11.0.15+10-0ubuntu0.21.10.1                amd64        OpenJDK Development Kit (JDK)
ii  openjdk-11-jdk-headless:amd64              11.0.15+10-0ubuntu0.21.10.1                amd64        OpenJDK Development Kit (JDK) (headless)
ii  openjdk-11-jre:amd64                       11.0.15+10-0ubuntu0.21.10.1                amd64        OpenJDK Java runtime, using Hotspot JIT
ii  openjdk-11-jre-headless:amd64              11.0.15+10-0ubuntu0.21.10.1                amd64        OpenJDK Java runtime, using Hotspot JIT (headless)
ii  openjdk-17-jdk:amd64                       17.0.3+7-0ubuntu0.21.10.1                  amd64        OpenJDK Development Kit (JDK)
ii  openjdk-17-jdk-headless:amd64              17.0.3+7-0ubuntu0.21.10.1                  amd64        OpenJDK Development Kit (JDK) (headless)
ii  openjdk-17-jre:amd64                       17.0.3+7-0ubuntu0.21.10.1                  amd64        OpenJDK Java runtime, using Hotspot JIT
ii  openjdk-17-jre-headless:amd64              17.0.3+7-0ubuntu0.21.10.1                  amd64        OpenJDK Java runtime, using Hotspot JIT (headless)
ii  openjdk-8-jdk:amd64                        8u312-b07-0ubuntu1~21.10                   amd64        OpenJDK Development Kit (JDK)
ii  openjdk-8-jdk-headless:amd64               8u312-b07-0ubuntu1~21.10                   amd64        OpenJDK Development Kit (JDK) (headless)
ii  openjdk-8-jre:amd64                        8u312-b07-0ubuntu1~21.10                   amd64        OpenJDK Java runtime, using Hotspot JIT
ii  openjdk-8-jre-headless:amd64               8u312-b07-0ubuntu1~21.10                   amd64        OpenJDK Java runtime, using Hotspot JIT (headless)



## java の切り替えはどうするのか？

### jenv を使う？ anyenv 経由で使う？
