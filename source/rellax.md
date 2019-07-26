---
title: rellax.js
date: 2019-07-26
tags: ['rellax.js', 'react-rellax']
excerpt: HTMLページのスクロールに時間差をつける
---

# rellax.jsとは

javascriptのライブラリ
HTMLページのスクロールに時間差をつけることでページに3D感を与える
「パララックス効果」を付与する


## 使い方

 HTMLに <script></script> タグで導入
    2つ方法がある
- https://github.com/dixonandmoe/rellax から rellax.min.js ファイルを持ってくる

- CDN経由で <script src="https://cdnjs.cloudflare.com/ajax/libs/rellax/1.0.0/rellax.min.js"></script> をHTMLに組み込む


JavaScriptのコードは1行！！
```javascript
var rellax = new Rellax(' .rellax ');
```
> [!TIP]
> 上のコードをHTMLに組み込むもよし。jsファイルとして別に記述してもよし。


## 使用例
```html
<!-- index.html -->
<html>
    <body>
        <div class="rellax ball1" data-rellax-speed={-7}></div>
        <div class="rellax ball2" data-rellax-speed={0}></div>
        <div class="rellax ball3" data-rellax-speed={5}></div>
        <div class="rellax ball4" data-rellax-speed={10}></div>
    </body>
</html>
```

> [!TIP]
> data-rellax-speedの値が10から-10で値が低くなるほど遅くなる


```css
div {
    position: relative;
}

.ball1 {
    width: 70%;
    padding-top: 70%;
    background-color: #0f0;
    opacity: 0.5;
    border-radius: 50%;
    top: -150px;
    left: 30%;
}

.ball2 {
    width: 70%;
    padding-top: 70%;
    background-color: #f00;
    opacity: 0.5;
    border-radius: 50%;
    top: -100px;
    left: 20%;
}

.ball3 {
    width: 70%;
    padding-top: 70%;
    background-color: #00f;
    opacity: 0.5;
    border-radius: 50%;
    top: -150px;
    left: 30%;
}

.ball4 {
    width: 70%;
    padding-top: 70%;
    background-color: #0ff;
    opacity: 0.5;
    border-radius: 50%;
    top: -100px;
    left: 20%;
}
```


# react-rellax
React.jsにてrellaxライブラリを使えるようにしたもの
使用方法自体はタグ名を直接書くぐらいで元のrellax.jsとさほど変わらない


## Install方法
```
npm i --save react-rellax
```


## 導入方法
```javascript
import Parallax from 'react-rellax'
        ...

<Parallax speed={-5}>I'm slow and smooth</Parallax>

```
