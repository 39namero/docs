# NVIDIA GeForce GT 1030 を使う

## 事前作業

1. マシン停止
2. グラボを入れる
3. マシン起動

## Ubuntu 情報を先に確認する

### OS 確認

lsb_release -a

    ↓こんな出力があるはず
    No LSB modules are available.
    Distributor ID:	Ubuntu
    Description:	Ubuntu 21.10
    Release:	21.10
    Codename:	impish

cat /etc/os-release

    ↓こんな出力があるはず
    PRETTY_NAME="Ubuntu 21.10"
    NAME="Ubuntu"
    VERSION_ID="21.10"
    VERSION="21.10 (Impish Indri)"
    VERSION_CODENAME=impish
    ID=ubuntu
    ID_LIKE=debian
    HOME_URL="https://www.ubuntu.com/"
    SUPPORT_URL="https://help.ubuntu.com/"
    BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
    PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
    UBUNTU_CODENAME=impish

### CPU 確認

sudo lshw -class processor

    ↓こんな出力があるはず
    *-cpu
        詳細: CPU
        製品: Intel(R) Core(TM) i7-4790 CPU @ 3.60GHz
        ベンダー: Intel Corp.
        物理ID: 33
        バス情報: cpu@0
        バージョン: Intel(R) Core(TM) i7-4790 CPU @ 3.60GHz
        スロット: SOCKET 0
        サイズ: 1717MHz
        容量: 4GHz
        幅: 64 bits
        クロック: 100MHz
        性能: lm fpu fpu_exception wp vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp x86-64 constant_tsc arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc cpuid aperfmperf pni pclmulqdq dtes64 monitor ds_cpl vmx smx est tm2 ssse3 sdbg fma cx16 xtpr pdcm pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand lahf_lm abm cpuid_fault epb invpcid_single pti ssbd ibrs ibpb stibp tpr_shadow vnmi flexpriority ept vpid ept_ad fsgsbase tsc_adjust bmi1 avx2 smep bmi2 erms invpcid xsaveopt dtherm ida arat pln pts md_clear flush_l1d cpufreq
        設定: cores=4 enabledcores=4 threads=8

### DISK 確認

sudo lshw -class disk

    ↓こんな出力があるはず
    *-disk                    
        詳細: ATA Disk
        製品: HS-SSD-Desire(S)
        物理ID: 0.0.0
        バス情報: scsi@0:0.0.0
        論理名: /dev/sda
        バージョン: ae10
        シリアル: 30056784878
        サイズ: 476GiB (512GB)
        性能: gpt-1.00 partitioned partitioned:gpt
        設定: ansiversion=5 guid=269b7fdf-ac74-40fc-ac47-7174e9e9d070 logicalsectorsize=512 sectorsize=512
    *-cdrom
        詳細: DVD reader
        製品: DVD-ROM DS-8DBSH
        ベンダー: PLDS
        物理ID: 0.0.0
        バス情報: scsi@5:0.0.0
        論理名: /dev/cdrom
        論理名: /dev/dvd
        論理名: /dev/sr0
        バージョン: MD11
        性能: removable audio dvd
        設定: ansiversion=5 status=nodisc

### memory 確認

sudo lshw -class memory

### 全部確認

sudo lshw | less

### PCI スロット 確認

lspci

    ↓こんな出力があるはず
    00:00.0 Host bridge: Intel Corporation 4th Gen Core Processor DRAM Controller (rev 06)
    00:02.0 VGA compatible controller: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor Integrated Graphics Controller (rev 06)
    00:03.0 Audio device: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor HD Audio Controller (rev 06)
    00:14.0 USB controller: Intel Corporation 8 Series/C220 Series Chipset Family USB xHCI (rev 04)
    00:16.0 Communication controller: Intel Corporation 8 Series/C220 Series Chipset Family MEI Controller #1 (rev 04)
    00:1a.0 USB controller: Intel Corporation 8 Series/C220 Series Chipset Family USB EHCI #2 (rev 04)
    00:1b.0 Audio device: Intel Corporation 8 Series/C220 Series Chipset High Definition Audio Controller (rev 04)
    00:1c.0 PCI bridge: Intel Corporation 8 Series/C220 Series Chipset Family PCI Express Root Port #1 (rev d4)
    00:1c.3 PCI bridge: Intel Corporation 8 Series/C220 Series Chipset Family PCI Express Root Port #4 (rev d4)
    00:1d.0 USB controller: Intel Corporation 8 Series/C220 Series Chipset Family USB EHCI #1 (rev 04)
    00:1f.0 ISA bridge: Intel Corporation H81 Express LPC Controller (rev 04)
    00:1f.2 SATA controller: Intel Corporation 8 Series/C220 Series Chipset Family 6-port SATA Controller 1 [AHCI mode] (rev 04)
    00:1f.3 SMBus: Intel Corporation 8 Series/C220 Series Chipset Family SMBus Controller (rev 04)
    02:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 0c)

### nvidia グラボ確認

lspci | grep -i nvidia

    挿せば何か出るはず
    01:00.0 VGA compatible controller: NVIDIA Corporation GP108 [GeForce GT 1030] (rev a1)
    01:00.1 Audio device: NVIDIA Corporation GP108 High Definition Audio Controller (rev a1)

### ドライバー一覧出力

lsmod

### nvidia ドライバーがないことを確認

lsmod | grep nvidia

### nouveau ドライバーが存在しないことを確認する（なくてよい）

lsmod | grep nouveau

    nouveau              2088960  1
    mxm_wmi                16384  1 nouveau
    drm_ttm_helper         16384  1 nouveau
    ttm                    69632  2 drm_ttm_helper,nouveau
    drm_kms_helper        262144  2 i915,nouveau
    i2c_algo_bit           16384  2 i915,nouveau
    wmi                    32768  2 mxm_wmi,nouveau
    drm                   561152  16 drm_kms_helper,drm_ttm_helper,i915,ttm,nouveau
    video                  53248  2 i915,nouveau

## Nouveau の無効化

cd /etc/modprobe.d
pwd

ls

lsmod | grep nouveau

sudo vi blacklist-nouveau.conf

cat blacklist-nouveau.conf
    blacklist nouveau
    options nouveau modeset=0

initramfs イメージを更新

sudo update-initramfs -u

    update-initramfs: Generating /boot/initrd.img-5.13.0-52-generic
    kentaro@kentaro-optiplex-3020 /etc/modprobe.d

echo $?

    0

sudo systemctl reboot


## 自動的に NVIDIA ドライバーを検出するパターン

ubuntu-drivers devices
== /sys/devices/pci0000:00/0000:00:01.0/0000:01:00.0 ==
modalias : pci:v000010DEd00001D01sv000010DEsd0000121Ebc03sc00i00
vendor   : NVIDIA Corporation
model    : GP108 [GeForce GT 1030]
driver   : nvidia-driver-515-server - distro non-free
driver   : nvidia-driver-418-server - distro non-free
driver   : nvidia-driver-470 - distro non-free
driver   : nvidia-driver-515 - distro non-free recommended
driver   : nvidia-driver-450-server - distro non-free
driver   : nvidia-driver-510-server - distro non-free
driver   : nvidia-driver-390 - distro non-free
driver   : nvidia-driver-470-server - distro non-free
driver   : nvidia-driver-510 - distro non-free
driver   : xserver-xorg-video-nouveau - distro free builtin


    以下で自動的に必要なドライバーをインストール可能だが、今回はあえてやらない
    sudo ubuntu-drivers autoinstall

## Ubuntu 公式リポジトリから nvidia-driver を探すパターン

### apt パッケージを最新化

sudo apt update
sudo apt upgrade

### nvidia-driver のインストール

sudo apt search nvidia-driver

sudo apt search nvidia-driver-515

sudo apt list nvidia-driver-515

    ↓が見つかるはず
    nvidia-driver-515/impish-updates,impish-security 515.48.07-0ubuntu0.21.10.2 amd64

sudo apt install nvidia-driver-515


### nvidia-settings のインストール

sudo apt search nvidia-settings
sudo apt list nvidia-settings

sudo apt install nvidia-settings

### 再起動
sss
sudo systemctl reboot

## 確認

### nvidia ドライバーがロードされていることを確認する

lsmod | grep nvidia

### GPU の使用状況をモニター

nvidia-smi

この状態で Youtube などを見て GPU が使用されていることを確認する

GeForce GT 1030 Ubuntu 20.04 ドライバー インストール ガイド
https://tutorialforlinux.com/2021/04/28/geforce-gt-1030-ubuntu-20-04-driver-installation-guide/2/

NVIDIA Driver Downloads
https://www.nvidia.com/Download/Find.aspx

【Ubuntu + NVIDIA】Ubuntu に NVIDIA ドライバーをインストール
https://tamnology.com/ubuntu-nvidia-driver/#toc2


## nvidia-settings の使い方

以下の記事を見ておいおいやってみよう（ 難しい ）

Ubuntu でコマンドラインで nvidia-settings でクロックオフセットやファン速度を変えるメモ
https://qiita.com/syoyo/items/bc0948ca7b3aeabe7569

## 参考

簡単に2万円台でゲーミングパソコンを作る方法・手順紹介2018【自作PC】
https://www.youtube.com/watch?v=7XRR80cddEo

【ゆっくり】玄人志向 NVIDIA GeForce GT1030でMinecraft遊んでみる！
https://www.youtube.com/watch?v=m46wyoqOSP0

GT1030に本気出させる！　　GT1030で快適にゲームする為のPCの設定（APEX FF14 フォートナイトで比較）【自作PC】
https://www.youtube.com/watch?v=TOo8_qUntsY

GT 1030 | Minecraft Java - 1080p & 4K - With and without Shaders! - EP4
https://www.youtube.com/watch?v=FGg26b9CIwo


https://elitrashooter.com/%E3%83%9E%E3%82%A4%E3%82%AF%E3%83%A9%E6%94%BB%E7%95%A5%E6%9C%80%E6%96%B0%E3%81%AE%E3%80%80%E4%BA%BA%E6%B0%97%E3%81%AE%E5%BD%B1mod%E3%82%B7%E3%82%A7%E3%83%BC%E3%83%80%E3%83%BC%E3%81%A7%E3%81%82/
[マイクラ攻略]最新の人気の影MOD(シェーダー)である Beyond Belief Shaders(BBEPC)の概要(使い方・遊び方)と導入方法

【Minecraft】2022年｜おすすめのシェーダーパック１３選！【マイクラ影mod】
https://dencreate.com/%E3%80%90minecraft%E3%80%912021%E5%B9%B4%EF%BD%9C%E3%81%8A%E3%81%99%E3%81%99%E3%82%81%E3%81%AE%E3%82%B7%E3%82%A7%E3%83%BC%E3%83%80%E3%83%BC%E3%83%91%E3%83%83%E3%82%AF%EF%BC%91%EF%BC%93%E9%81%B8/