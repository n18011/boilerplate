---
title: mozcの日本語入力と英語入力の切り替え方法
date: 2019-06-20
tags: ['keybord', 'キーボード', 'mozc', 'Ubuntu18.03','Xubuntu19' ]
excerpt: ずっとクリックして切り替えてた;今までの作業ロスが...
---


## 環境
- Ubuntu18.03,Xubuntu19
- mozcインストール済PC

## 方法
キーボードによってやり方が少し異なるのでそれぞれの場合について手順を示す。


## 日本語キーボードの場合
 半角/全角で切り替えるようにする

- 設定→地域と言語→入力ソース→英語を選択 `-`ボタンで消す
- ログアウト→ログイン
で完了


## USキーボードの場合
 Ctrl+Space(影響なければ他のキーでもよし)で切り替えるようにする

- 設定→地域と言語→入力ソース→英語を選択
-ボタンで消す
- ログアウト→ログイン
ここまでは日本語キーボードの場合と同じ
- mozcのツール→プロパティ→一般タブ→キー設定→キー設定の選択→編集
- Ctrl+Space(影響なければ他のキーでもよし)はすでに半角空白挿入の設定なのでエントリーを削除する
- Hankaku/Zenkakuに設定されている項目をすべてCtrl+Space(影響なければ他のキーでもよし)に置き換える
- OK→適用(Apply)→OK
で完了
