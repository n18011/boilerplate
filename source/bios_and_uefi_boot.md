---
title: UEFI GPT + BIOS GPT/MBR のハイブリッドブート(USB)
date: 2019-06-25
tags: ['LiveUSB', 'kali linux', 'GRUBブートローダ']
excerpt: どんなPCでも起動可能な持ち運べるマイOSを作りたい！
---

## 目的
ブーターブルUSBでインストールしたLiveUSBでUSBにOSを持ちたい
USBの容量すべてをOSデータに使いたい
他のPCでもUSB起動出来るようにしたい


## 流れ
- 下準備
- ブーターブルUSBからLiveUSBにしたいUSBにOSインストール
- /etc/fstabの書き換え
- GRUBブートローダーをインストール
- 後処理


## 下準備
### 前提


- 自身のPCパーティションを /dev/sda
- USBのパーティションを /dev/sdb
とする


### partationを区切る
USBのパーティションを区切る
MBRパーティション /dev/sdb1
EFIパーティション /dev/sdb2
ルートパーティション /dev/sdb3


- Gparted
- gdisk


### MBRパーティションの作成
```
# gdisk /dev/sdb

Command (? for help): r
Recovery/transformation command (? for help): h
Type from one to three GPT partition numbers, separated by spaces, to be added to the hybrid MBR, in sequence: 1 2 3
Place EFI GPT (0xEE) partition first in MBR (good for GRUB)? (Y/N): N

Creating entry for GPT partition #1 (MBR partition #1)
Enter an MBR hex code (default EF):
Set the bootable flag? (Y/N): N

Creating entry for GPT partition #2 (MBR partition #2)
Enter an MBR hex code (default EF):
Set the bootable flag? (Y/N): N

Creating entry for GPT partition #3 (MBR partition #3)
Enter an MBR hex code (default 83):
Set the bootable flag? (Y/N): Y

Recovery/transformation command (? for help): x
Expert command (? for help): h
Expert command (? for help): w

Final checks complete. About to write GPT data. THIS WILL OVERWRITE EXISTING
PARTITIONS!!

Do you want to proceed? (Y/N): Y
```


## ブーターブルUSBからLiveUSBにしたいUSBにOSインストール
### ブーターブルUSBを作成する際に使用したツール・コマンド
- unetbootin


ここでは使い方は解説しません


- ddコマンド
    isoイメージを展開コピーする
```
# dd if={ISOファイルpath} of={書き込み先のパーティションのpath　例/dev/sdb3} bs=1024 status=progress && sync
```
status=progressで進捗状況が出力される
&& syncでキッシュを消す


### OSインストール
目的動作確認済みOS
- Xubuntu19
- kali-linux2019
- kali-linux-light


作ったブーターブルUSBを起動してOSインストールを開始する


## /etc/fstabの書き換え
他のPCでも起動出来るようにするための処理を行います。


OSインストールした後、起動する際にUSBパーティションのUUIDではなく、OSインストールに使用したPCパーティションのUUIDにブートするデバイスとして自動で書き換わる。
そのため、起動時にUSBパーティションのUUIDを参照してブートするように/etc/fstabを書き換える必要がある


まず自分のPCのUUIDとUSBのUUIDを調べます
```
# blkid /dev/sda
# blkid /dev/sdb2
```
上のコマンドで出力されたUUIDを覚えておく

それからブートしたい/パーティションの/etc/fstab中の自分のPCのUUIDをUSBのUUIDに書き換えます
```
// /etc/fstab
```


## GRUBブートローダーをインストール
### GRUBの設定
```
# mount /dev/sdb2 /mnt
# mkdir -p /mnt/boot/grub
# grub-mkconfig -o /mnt/boot/grub/grub.cfg
```
### EFI用にGRUBをインストール
```
# grub-install --target=x86_64-efi --efi-directory=/mnt --boot-directory=/mnt/boot --removable /dev/sdb1
```


### BIOS用にGRUBをインストール
```
# grub-install --target=i386-pc --boot-directory=/mnt/boot  /dev/sdb
```


## 後処理
OSインストール後はgrubブートローダが自分のPCから消えるので自身のPCにも再インストールする必要がある
