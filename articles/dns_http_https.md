---
title: "ドメインを入力してからページが表示されるまでの仕組み"
emoji: "🍣"
type: "tech"
topics: [dns, http, https, html, js]
published: true
---

## この記事の概要
この記事では、ドメインを入力してから画面にページが表示されるまでの仕組みを出来るだけわかりやすく解説していきます。
今回解説する一連のプロセスは以下の通りです。

- DNSサーバーに接続しドメインに対応するIPアドレスを取得する。
- ブラウザがHTTPまたはHTTPSリクエストをサーバーに送信する。
- ウェブサーバーがリクエストを受け取りレスポンスを返す。
- 受け取ったファイルから画面を構築する。（ブラウザレンダリング）

## DNS
まずユーザーが入力したドメインはブラウザからDNSサーバーに送られ、DNSサーバーはドメインに対応したIPアドレスを返します。
### DNSとは
DNS（Domain Name System）は、インターネット上のコンピューターシステムやネットワークデバイスに割り当てられたIPアドレスを、人間が理解しやすいドメイン名（例えば、"example.com"）に変換するシステムです。
これを使いドメインに対応するIPアドレスを検索することができます。
**IPアドレスでないと、コンピューターはウェブサイトに接続できません。**
![](https://storage.googleapis.com/zenn-user-upload/51e757598fcd-20240504.png)

## HTTPまたはHTTPSリクエスト
先ほど取得したIPアドレスにHTTPまたはHTTPSリクエストを送り、ウェブサーバーに接続します。
ウェブサーバーはそのリクエストを受け取り、要求されたページのファイル（HTML、CSS、JavaScriptなど）を探します。それらのファイルが見つかると、ウェブサーバーはそれらをまとめてレスポンスとしてブラウザに返します。
![](https://storage.googleapis.com/zenn-user-upload/44feb3bdc254-20240504.png)

## ブラウザレンダリング
ブラウザレンダリングとは、ブラウザが受け取ったHTML、CSS、JavaScriptなどのコードを解釈し、ウェブページをユーザーの画面に表示するプロセスのことです。
このプロセスでは、ブラウザがHTMLをDOM（Document Object Model）として構築し、CSSを使ってスタイルを適用し、JavaScriptを実行してページを動的に変更します。

### DOMとは
DOM（Document Object Model）は、ウェブページの構造や内容をコンピューターが理解しやすい形で表現する方法です。イメージすると、ウェブページが木のような構造を持っていると考えることができます。この木構造では、ページ全体が1つの根（ルート）ノードから始まり、その下にさまざまな要素が枝分かれしています。
```html:HTML
<!DOCTYPE html>
    <head>
        <title>test</title>
    </head>
    <body>
        <h1>hello</h1>
    </body>
</html>
```
```css:CSS
h1 {
    color: red;
}
```
![](https://storage.googleapis.com/zenn-user-upload/e87057ad150f-20240504.png)
*DOMツリー*
DOMでは、この木の構造をプログラムで操作できるようにします。例えば、ある要素を見つけてそのテキストを変更したり、新しい要素を追加したり、要素のスタイルを変更したりできます。
これにより、JavaScriptなどのプログラミング言語を使用して、ウェブページを動的に操作することができるようになります。