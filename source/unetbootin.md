---
title: unetbootinインストール方法
date: 2019-06-20
tags: ['unetbootin']
excerpt: インストール方法を簡潔に
---
## unetbootinとは
さまざまなOSを選び、ダウンロードしそのままブート可能なUSBメモリやUSBハードディスクドライブを作成することが可能


```
// install
# add-apt-repository ppa:gezakovacs/ppa
# apt update
# apt install unetbootin

// 通常起動してwindowの中が真っ白な場合の起動法
# QT_X11_NO_MITSHM=1 unetbootin
```


## おまけ
### 設定や変更を保存できるLiveUSBの作成
この記事では説明していませんが、上記のツールで展開されたLiveUSBなどはinstaller設定ため、起動後にファイルの変更や保存ができません。
そこで、ここでは設定や変更を保存できるLiveUSBを作成していきます。


- 作成したLiveUSBから/boot/grub/grub.cfgをさがす
- grub.cfgをエディタで編集する
- 最初の search ~ の行を探し --persistent を行末に追加
- 保存　終了


すごいざっくりな手順で申し訳ない。
気が向いたら、更新します。。。