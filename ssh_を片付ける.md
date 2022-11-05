# SSH の設定をもういい加減に片付ける

* ローカルの設定を綺麗にする
* できるだけ鍵交換する

`ls -lR .ssh`

```zsh
-rw-r--r--  1 ichito24  staff   113  7  1  2018 config
-rw-------  1 ichito24  staff  2602  1 16  2022 gcp-ssh-key
-rw-r--r--  1 ichito24  staff   568  1 16  2022 gcp-ssh-key.pub
-rw-------@ 1 ichito24  staff  1743  3 25  2018 id_rsa
-rw-------  1 ichito24  staff  3326  7  1  2018 id_rsa_namero_github
-rw-r--r--  1 ichito24  staff   747  7  1  2018 id_rsa_namero_github.pub
-rw-r--r--  1 ichito24  staff  6686 11  1 21:26 known_hosts
-rw-r--r--  1 ichito24  staff  5944  1 21  2022 known_hosts.20220123
-rw-r--r--  1 ichito24  staff  4457 11 23  2020 known_hosts.bk01
```

* [ ] known_hosts
* [ ] .ssh 配下のファイルで一つ一つ検索しよう

存在する鍵は何？

* gcp-ssh-key 〜 : GCP ( Google Cloud Platform ) 接続用
* id_rsa : XSERVER 接続用
* id_rsa_namero-github 〜 : github 接続用

接続先のマシン・サーバは？

* xserver:sv1338.xserver.jp
* github
* GCP
* 健太朗のパソコン・Linux のノートパソコン

## xserver:sv1338.xserver.jp

XSERVER 接続用

```
-rw-------@ 1 ichito24  staff  1743  3 25  2018 id_rsa
```

XSERVER で作成した秘密鍵をダウンロードしたものを id_rsa としている（デフォルトとしている）
それで、公開鍵  id_rsa .pub がないんだな？

### config による制御

id_rsa_samojun_xserver に mv して config に追加するとする

`mv id_rsa id_rsa_samojun_xserver`

```
-rw-------@ 1 ichito24  staff  1743  3 25  2018 id_rsa_samojun_xserver
```

```
cat config
〜
Host xserver
  HostName sv1338.xserver.jp
  User samojun
  Port 10022
  IdentityFile ~/.ssh/id_rsa_samojun_xserver
```

接続テスト

```
ssh xserver
Enter passphrase for key '/Users/ichito24/.ssh/id_rsa_samojun_xserver':
Last login: Sat Nov  5 13:21:06 2022 from kd124211137034.ppp-bb.dion.ne.jp
[samojun@sv1338 ~]$
```

パスフレーズを求められるのをなんとかしたいが XSERVER 側で鍵を作成するため
その際にパスフレーズを指定せざるを得ない
（クライアント側で鍵を作成して登録できるのか？）

### ssh-agent と ssh-add

以下を参考にして `ssh-agent` と `ssh-add` を使ってみる

SSH で毎回パスフレーズを入れるのが面倒だと思ったときには
<https://qiita.com/evakichi/items/abb6dde9df78f049b913>

【ssh】公開鍵認証するときのパスフレーズを省略する方法の紹介
<https://fumidzuki.com/knowledge/3401/>

`ssh-agent`

```
SSH_AUTH_SOCK=/var/folders/y8/g07ks8zj73q6bbclwkzy2dfw0000gp/T//ssh-dC0OAAdnThYW/agent.26007; export SSH_AUTH_SOCK;
SSH_AGENT_PID=26008; export SSH_AGENT_PID;
echo Agent pid 26008;
```

上記出力された環境変数を設定する

```zsh
eval `ssh-agent`
```

秘密鍵の情報を ssh に登録することでパスフレーズの省略が可能となる

`ssh-add ~/.ssh/id_rsa_samojun_xserver`

```zsh
  Enter passphrase for /Users/ichito24/.ssh/id_rsa_samojun_xserver:
  Identity added: /Users/ichito24/.ssh/id_rsa_samojun_xserver (/Users/ichito24/.ssh/id_rsa_samojun_xserver)

echo $?
  0
```

接続テスト

```
ssh xserver
Last login: Sat Nov  5 14:45:39 2022 from kd124211137034.ppp-bb.dion.ne.jp
```

成功！！

## github

* id_rsa_namero_github
* id_rsa_namero_github.pub

github 接続用に作成した形跡あり

```
-rw-------  1 ichito24  staff  3326  7  1  2018 id_rsa_namero_github
-rw-r--r--  1 ichito24  staff   747  7  1  2018 id_rsa_namero_github.pub
```

* cat config

github 接続用の設定を記載しているが…

```zsh
ServerAliveInterval 15 → 15 秒毎にサーバにポーリング・接続を継続
Host github → github 向けの定義
  HostName github.com → 接続する host
  User git → 接続ユーザ名
  IdentityFile ~/.ssh/id_rsa_namero_github → 使用する秘密鍵へのパス
```

ただし github 側に公開鍵の設定がない…

なので、接続テストを行ってもエラーが返る

```
ssh -T github
git@github.com: Permission denied (publickey).
```

これを github に登録してと…

```zsh
cat .ssh/id_rsa_namero_github.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQDHuoC6MDM8QW5Yado/wUjx5o3AkE9Bb1Fe7GoazCndYIX3J7aya1ar+wmi03GPcwsT3JUwbQB8QAmGtzTsY/7eiRZ4M6NHViz6jD5VSd5ce3Ax62Mr87QSGiv8tjVonkSe8wzRAlO/eJWlw+ja3GLh+6SDLvJ5RRwLgHGXRNRKGLcNCdHaY75k3oRsU56KMxyN8EQRDTccUJohqz4mdqrq3bxIjU5j2sSzbiCgqBHEtlPO4M2nepj3PKLxYxNGDeHtxdSljORLKHPhLhNYi2Y6p+In9n4KP8pf9Odej++ZQeUs30iyvIPPJxeGQAaRMizcfSNb/mnUcbVnLrA46yAU+6FNmbw/Nm5NADRvao5I9SfCYGz4ht/Qm9NyBQM2kTpCl03BFE3gS+heBBHMuuVVscmKIGDZhVxjzbXcuM6jDOJO1NfERPy6vEYrmLTFpPSDEnczT/JJbs4DmJxnaS/NwB7HY5Ax7SlvY7culhqtCHXutqb5usIZ6ZzqR+VMSAWcMb0Cw3l0fyEvBDGEvM2mwIifQxd4uR+kBYhNGqtRHOOQ24aaa1YDnJONvByVKlQA08qdCQ21iTi1njb68KarfhnNDf4ve/xvMAuBsnYaWBZGS0XdjmM83udOywBlvS2bmbIfa+lEAjOk/RcD1ustKNkhS93acLNPHJWkjKx/pw== key_for_namero_GitHub
```

github に接続テストを行う

```
ssh -T github
Enter passphrase for key '/Users/ichito24/.ssh/id_rsa_namero_github':
Enter passphrase for key '/Users/ichito24/.ssh/id_rsa_namero_github':
```

パスフレーズを求められるがな…正直分からないので削除するとする

先にバックアップして改めて作る

```
ssh-keygen -l -f ~/.ssh/bkup/id_rsa_namero_github.pub
4096 SHA256:+W/oyy7avwI2uZ0jGYG8O4d5g96ZB2U7akYoUXJWPhQ key_for_namero_GitHub (RSA)
```

簡単にこれで作ってみる

```
ssh-keygen -t rsa
```

```
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/ichito24/.ssh/id_rsa): /Users/ichito24/.ssh/id_rsa_namero_github
Enter passphrase (empty for no passphrase): → パスフレーズはなし
Enter same passphrase again: → パスフレーズはなし
Your identification has been saved in /Users/ichito24/.ssh/id_rsa_namero_github.
Your public key has been saved in /Users/ichito24/.ssh/id_rsa_namero_github.pub.
The key fingerprint is:
SHA256:0LPn90qHpIAIS35ISSFurauSdOMs0gbhWD/Q7u1ZKro ichito24@mizuembp01.local
The key's randomart image is:
+---[RSA 3072]----+
|. o.             |
|.o..   .         |
| o=o  . o        |
|o+++.. o o       |
|o+++o . S . .    |
|oo.++    + o .   |
|.=+..o  . o + .  |
|=.ooo .+   o o   |
|+.Eo o+     ...  |
+----[SHA256]-----+
```

秘密鍵と公開鍵が作成される

```
ichito24@mizuembp01 ~ % ls -l .ssh/id_rsa_namero_github*
-rw-------  1 ichito24  staff  2610 11  5 17:15 .ssh/id_rsa_namero_github
-rw-r--r--  1 ichito24  staff   579 11  5 17:15 .ssh/id_rsa_namero_github.pub
```

接続確認

```
ssh -T github
Hi 39namero! You've successfully authenticated, but GitHub does not provide shell access.
ichito24@mizuembp01 ~ % echo $?
1
```
実際に github を利用する手順は別ドキュメントとする

## GCP

【GCP】無期限の無料枠でLinuxサーバを構築
<https://densan-hoshigumi.com/server/gcp-free-linux>

以下を参考に作成したSSH認証鍵は現在不要なので削除する。（必要になったら作成）

```
-rw-------   1 ichito24  staff  2602  1 16  2022 gcp-ssh-key
-rw-r--r--   1 ichito24  staff   568  1 16  2022 gcp-ssh-key.pub
```

`rm gcp-ssh-key*`

## 健太朗のパソコン・Linux のノートパソコン

互いに鍵交換をするだけだが

### Linux のノートパソコンから

ローカル用の鍵ペアを作る

ssh-keygen -t rsa

```
ssh-keygen -t rsa
  Generating public/private rsa key pair.
  Enter file in which to save the key (/Users/ichito24/.ssh/id_rsa): /Users/ichito24/.ssh/id_rsa_ichito24_local
  Enter passphrase (empty for no passphrase):
  Enter same passphrase again:
  Your identification has been saved in /Users/ichito24/.ssh/id_rsa_ichito24_local.
  Your public key has been saved in /Users/ichito24/.ssh/id_rsa_ichito24_local.pub.
  The key fingerprint is:
  SHA256:cyYy6zb5YWinrJVv1uw9FEpmjXJsMxkXN9IAkg+zUIA ichito24@mizuembp01.local
  The key's randomart image is:
  +---[RSA 3072]----+
  |     ..oo...++o  |
  |    E . +.. .o.. |
  |       . * *     |
  |        o & o    |
  |      o SBo+ .   |
  |       * =. .    |
  |      *.+o .     |
  |     =+=o.o..    |
  |    .o+=o.. ..   |
  +----[SHA256]-----+
```

```
ls -l .ssh/id_rsa_ichito24_local*
  -rw-------  1 ichito24  staff  2610 11  5 18:25 .ssh/id_rsa_ichito24_local
  -rw-r--r--  1 ichito24  staff   579 11  5 18:25 .ssh/id_rsa_ichito24_local.pub
```

```
scp -p .ssh/id_rsa_ichito24_local.pub ichiro@192.168.0.26:~/.ssh/.
  ichiro@192.168.0.26's password:
  id_rsa_ichito24_local.pub                                                         100%  579    92.5KB/s   00:00
```

接続先で以下

```zsh
uname -n
  ASUS-VivoBook
```

```zsh
pwd
  /home/ichiro/.ssh
```

```zsh
ls -l
  合計 8
  -rw-r--r-- 1 ichiro ichiro 579 11月  5 18:25 id_rsa_ichito24_local.pub
```

```zsh
cat id_rsa_ichito24_local.pub > authorized_keys
chmod 600 authorized_keys
```

接続テスト

```zsh
ssh -i .ssh/id_rsa_ichito24_local  ichiro@192.168.0.26
  Welcome to Ubuntu 21.10 (GNU/Linux 5.13.0-52-generic x86_64)

   * Documentation:  https://help.ubuntu.com
   * Management:     https://landscape.canonical.com
   * Support:        https://ubuntu.com/advantage

  0のアップデートはすぐに適用されます。

  Your Ubuntu release is not supported anymore.
  For upgrade information, please visit:
  http://www.ubuntu.com/releaseendoflife

  New release '22.04.1 LTS' available.
  Run 'do-release-upgrade' to upgrade to it.

  Last login: Sat Nov  5 19:44:27 2022 from 192.168.0.20
  ichiro@ASUS-VivoBook ~ %
```

OK!

逆を行う

ssh-keygen -t rsa
scp -p .ssh/id_rsa_ichiro_local ichito24@192.168.0.20:~/.ssh/.

接続先で

pwd
  /Users/ichito24/.ssh

cat id_rsa_ichiro_local.pub > authorized_keys
chmod 600 authorized_keys

config の設定

```
vi config
〜
Host ASUS-VivoBook
  HostName 192.168.0.26
  User ichiro
  Port 22
  IdentityFile ~/.ssh/id_rsa_ichito24_local
〜
```

接続先で
```
vi config
〜
Host mizuembp01
  HostName 192.168.0.20
  User ichito24
  Port 22
  IdentityFile ~/.ssh/id_rsa_ichiro_local
〜
```

### 対健太朗PCも同様の設定を行う


## .ssh の配下

`ls -l .ssh`

```zsh
-rw-------  1 ichito24  staff  1157 11  5 20:22 authorized_keys
drwxr-xr-x  9 ichito24  staff   288 11  5 20:42 bkup
-rw-r--r--  1 ichito24  staff   449 11  5 20:11 config
-rw-------  1 ichito24  staff  2610 11  5 18:25 id_rsa_ichito24_local
-rw-r--r--  1 ichito24  staff   579 11  5 18:25 id_rsa_ichito24_local.pub
-rw-------  1 ichito24  staff  2610 11  5 17:15 id_rsa_namero_github
-rw-r--r--  1 ichito24  staff   579 11  5 17:15 id_rsa_namero_github.pub
-rw-------@ 1 ichito24  staff  1743  3 25  2018 id_rsa_samojun_xserver
-rw-r--r--  1 ichito24  staff  7081 11  5 13:19 known_hosts
```


## 参考メモ

Google id_rsa 整理
<https://www.google.com/search?q=id_rsa+%E6%95%B4%E7%90%86&client=safari&rls=en&biw=1440&bih=820&sxsrf=APq-WBt2pGtWu1OSJB0K0DZ6ql-gqHEzhQ%3A1646928642393&ei=AiMqYpCdF_Xj2roPrOuZ6Ao&ved=0ahUKEwiQpsyl97v2AhX1sVYBHax1Bq04ChDh1QMIDQ&uact=5&oq=id_rsa+%E6%95%B4%E7%90%86&gs_lcp=Cgdnd3Mtd2l6EAMyBwgjELADECcyBwgAEEcQsAMyBwgAEEcQsAMyBwgAEEcQsAMyBwgAEEcQsAMyBwgAEEcQsAMyBwgAEEcQsAMyBwgAEEcQsAMyBwgAEEcQsAMyBwgAEEcQsANKBAhBGABKBAhGGABQAFgAYO8CaAFwAXgAgAEAiAEAkgEAmAEAyAEKwAEB&sclient=gws-wiz>

id_rsaファイルの発行とvs-code-serverへの転送
<https://qiita.com/elu_jaune/items/a4d2a323643337c4109a#おまけ1id_rsaファイルの発行とvs-code-server>への転送

SSHについて調べてみた
<https://qiita.com/suzuki-koya/items/af4b511d40b6362da60a>
基本を読んだ

とみぞーノートssh パスワード認証 -
<https://wiki.bit-hive.com/tomizoo/pg/ssh%20>パスワード認証

sshdで何も設定していないとパスワード認証が行われる。
初回接続時はfingerprint(公開鍵)が表示されて本当にこのホストに接続するかを確認される。 (yes/no)?

[tomita@tank ~]$ ssh 10.0.0.1
The authenticity of host '10.0.0.1 (10.0.0.1)' can't be established.
RSA1 key fingerprint is 59:5e:0d:8d:30:d7:1c:88:27:dc:84:cc:f3:c7:77:1d.
Are you sure you want to continue connecting (yes/no)? yes
〜

fingerprintは~/.ssh/known_hostsに記録される。
2回目以降の接続ではホストに接続するかの確認はなく、パスワードが聞かれるようになる。

以下のようにして公開鍵からfingerprintの値を確認できる。

ssh-keygen -l -f ~/.ssh/known_hosts

ssh-keygen -l -f /etc/ssh/ssh_host_key.pub

第3章 OpenSSH のしくみ
<https://www.unixuser.org/~euske/doc/openssh/book/chap3.html>

一般ユーザがクライアントを用いてサーバにログインを試みると、 クライアントとサーバデーモンのあいだで 2 種類の認証が交わされます:

1. そのサーバが本当に「ユーザのログインしたいサーバ」であるかどうかを確認する、ホスト認証。「ホスト鍵 (host key) 」がキーワード
2. そのユーザがサーバにログインできるかどうかを確認する、ユーザ認証。

* 秘密鍵で暗号化されたデータは、それに対応する公開鍵によってのみ正しく復号できる。
* 公開鍵で暗号化されたデータは、それに対応する秘密鍵によってのみ正しく復号できる。

OpenSSHのホスト鍵の確認方法(ssh-keygenが使えなくても何とか確認する)
<https://qiita.com/szly/items/54885a0594f29985d0c5>
SSHの認証プロセスには、以下の2つの段階があります。
サーバー認証：ログインしようとしているサーバーが、本当にログインしたいサーバーなのかを認証する → "パスワード認証" "公開鍵認証"
ユーザー認証：ログインしようとしているユーザーが、サーバーにログインしてもよいユーザーなのかを認証する → "サーバー認証"

CentOS 6にインストールされるOpenSSHは5.3p1
CentOS 7を使うと、OpenSSH 7.4p1
 → サーバーsshdとホスト鍵生成プログラムsshd-keygenが分離しているため、ホスト鍵を手動で作成する必要がある

クライアントが正しいサーバを確認したら、つぎはサーバのほうが 正しいユーザかどうかを確認する番です。これをユーザ認証といいます。 OpenSSH のユーザ認証には大きく分けて 2つの方式があります:

ユーザがあらかじめ登録したパスワードを使った認証 (パスワード認証)
ユーザがあらかじめ登録した秘密鍵・公開鍵ペアを使った認証 (公開鍵認証)

ユーザは秘密鍵というものを作成し、 それに対応する公開鍵をサーバにあらかじめ登録しておく。
ログイン時にはサーバに自分の秘密鍵の所有を示すことでユーザの身分を証明する。

1. クライアントがサーバに接続する。
2. クライアントは、自分がある公開鍵に対応する秘密鍵を持っていることを宣言する。
3. サーバはその公開鍵が、あらかじめそのユーザに対して登録されたものであるかどうかを確認し、 もしそうならば、対応する秘密鍵の証明を求める (チャレンジ)。
4. クライアントが秘密鍵の所有を数学的に証明する (レスポンス)。 このとき、ユーザは秘密鍵を使用するためにパスフレーズを入力するが、 このパスフレーズはネットワーク上に流れない。
5. 正しいレスポンスが送られてくると、 サーバはユーザが秘密鍵を持っていることを確信し、ログインを許可する。

この場合もユーザは パスワードに相当するパスフレーズをキーボードから入力する 必要がありますが、この情報はクライアント上で秘密鍵を使用するときにだけ使われ、 ネットワーク上に送信されることはありません。秘密鍵は通常、暗号化されてディスク上に格納されており、 ユーザ認証のときのみパスフレーズによって復元されます。

SSHの公開鍵ってなに?
<https://qiita.com/angel_p_57/items/19eda15576b3dceb7608>
みんながSSHで「公開鍵」と言ってるのは、大抵のケースで「認証鍵」のこと
それ以外に「ホスト鍵」もある
サーバに公開鍵を予め登録する必要がある（クライアント側の鍵ペア）

簡潔なQ - ホスト鍵とは
<https://qnighy.hatenablog.com/entry/2017/10/29/220000>
これも読んでおくか・あまり有用な情報なし

SSHにおけるフィンガープリントとは。ホスト認証とあわせて解説
<https://rurukblog.com/post/ssh-fingerprint/>
フィンガープリントとは接続先サーバーの公開鍵のハッシュ値です。

SSH接続するための秘密鍵と公開鍵をMacで作る
<https://www.ni4.jp/2021/01/31-134600.html>
まさにわかっていない自分と同じって思う

~/.ssh/configについて
<https://qiita.com/passol78/items/2ad123e39efeb1a5286b>

.ssh/configとは、ssh経由でのリモートサーバーの接続する際に利用される設定ファイルです。

# サーバーへ定期的(今回は60秒毎)に生きている報告をする(全体的に記述を有効にする場合は先頭辺りに書いておくといい)

ServerAliveInterval 60

# 個別に有効にしたい場合は、個別の設定に行を開けないで追記しておくといい

Host 任意の接続名(hoge)
    HostName ホスト名
    User ユーザー名
    Port ポート番号
    IdentityFile 鍵へのPATH(例えば~/.ssh/hoge.key)
    ServerAliveInterval 60
