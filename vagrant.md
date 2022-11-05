# vagrant

## インストール方法は？

ichiro@ASUS-VivoBook ~ % apt list vagrant
一覧表示... 完了
vagrant/impish,impish 2.2.14+dfsg-1ubuntu1 all

ichiro@ASUS-VivoBook ~ % brew search vagrant
==> Formulae
vagrant-completion

ichiro@ASUS-VivoBook ~ % snap search vagrant
No matching snaps for "vagrant"
ichiro@ASUS-VivoBook ~ % snap find vagrant  
No matching snaps for "vagrant"

## apt でインストール！

sudo apt install vagrant  

## linux での vagrant は libvirt が必要みたい

Vagrant + libvirt の環境構築手順
https://qiita.com/s-nishimaki/items/b6766318e08b0a8a0a20#%E3%83%88%E3%83%A9%E3%83%96%E3%83%AB%E3%82%B7%E3%83%A5%E3%83%BC%E3%83%86%E3%82%A3%E3%83%B3%E3%82%B0

これを見ると、apt はパッケージが古く、つまると書いているが大丈夫か？

```
wget https://releases.hashicorp.com/vagrant/2.1.5/vagrant_2.1.5_x86_64.deb
sudo dpkg --install vagrant_2.1.5_x86_64.deb
sudo apt update
sudo apt build-dep vagrant ruby-libvirt
sudo apt install qemu libvirt-bin ebtables dnsmasq
sudo apt install libxslt-dev libxml2-dev libvirt-dev zlib1g-dev ruby-dev
vagrant plugin install vagrant-libvirt
vagrant up --provider libvirt
```

### このページもなかなかにふるいかも

vagrant-libvirtをUbuntu Linux 18.04 LTSにインストールして、Ubuntu Linuxの仮想マシンを起動するまで
https://kazuhira-r.hatenablog.com/entry/2019/10/03/0
03753

### いろんなページをみて探ってみる

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

ここから完全に VirtualBox の問題となる
実は VirtualBox が使えていない事が判明したため、virtualbox のメモ「virtualbox.md」で管理していこう！

## 仕切りなおし

KVM をインストールして設定する
https://qiita.com/tkarube/items/7e02d1f9e93d107c616b

このページをみてやってみよう

### KVM のインストール

sudo apt update

sudo apt install -y qemu qemu-kvm libvirt-daemon libvirt-clients bridge-utils virt-manager

cat /etc/group
〜
kvm:x:109:ichiro
〜
libvirt:x:137:ichiro

sudo systemctl is-active libvirtd

  active

virt-host-validate
（WARN FAIL だけ記載）
〜
  QEMU: Checking if IOMMU is enabled by kernel                               : WARN (IOMMU appears to be disabled in kernel. Add intel_iommu=on to kernel cmdline arguments)
  QEMU: Checking for secure guest support                                    : WARN (Unknown if this platform has Secure Guest support)
〜
   LXC: Checking for cgroup 'devices' controller support                     : FAIL (Enable 'devices' in kernel Kconfig file or mount/enable cgroup controller in your system)
   LXC: Checking for cgroup 'freezer' controller support                     : FAIL (Enable 'freezer' in kernel Kconfig file or mount/enable cgroup controller in your system)
〜

この状態で vagrant が動きまへんかね？

 % pwd   
/home/ichiro/Documents/develp/vagrant/apache-tomcat

vagrant up --provider libvirt
〜
The box you're attempting to add doesn't support the provider
you requested. Please find an alternate box or use an alternate
provider. 

box が libvirt に対応していないとな？

他のでためすか

pwd
/home/ichiro/Documents/develp/vagrant/centos-7.9

vagrant init centos/7
A `Vagrantfile` has been placed in this directory. You are now
ready to `vagrant up` your first virtual environment! Please read
the comments in the Vagrantfile as well as documentation on
`vagrantup.com` for more information on using Vagrant.

vagrant up --provider libvirt
〜
Bringing machine 'default' up with 'libvirt' provider...
〜
==> default: Rsyncing folder: /home/ichiro/Documents/develp/vagrant/centos-7.9/ => /vagrant

vagrant box list             
centos/7 (libvirt, 2004.01)


vagrant ssh
[vagrant@localhost ~]$ 
[vagrant@localhost ~]$ sudo su -
[root@localhost ~]# cat /etc/redhat-release
CentOS Linux release 7.8.2003 (Core)

成功だ！！

vagrant halt
==> default: Halting domain...

ならば、とうぜん　VirtualBox も使えるはずだね！
（本当か！？）
だめでしたね！

ついでなので、
KVM をインストールして設定する
https://qiita.com/tkarube/items/7e02d1f9e93d107c616b
の続きをやっていこう


