---
title: "Gatsby.js 入門"
emoji: "🍯"
type: "tech"
topics: [react, gatsby]
published: true
---

## Gatsbyとは
https://www.gatsbyjs.com/docs/
> Gatsby is a React-based open source framework for creating websites. Whether your site has 100 pages or 100,000 pages — if you care deeply about performance, scalability, and built-in security — you'll love building with us. Start pulling data from your favorite headless CMS easily!

公式ドキュメントによると「Gatsbyは、パフォーマンス、スケーラビリティ、セキュリティを追求したReactベースのフレームワークです。100ページでも10,000ページでも、お気に入りのサイトを作るのに最適で、ヘッドレスCMSからデータを楽々取得できます。」と説明されています。

### 静的なサイトジェネレーター
Gatsbyは静的なサイトジェネレーターです。つまり、ウェブサイトのページを事前に生成しておき、ユーザーがウェブサイトにアクセスするたびに、サーバーはすでに用意されたファイルを提供するだけです。これにより、ページの読み込みが速くなり、サーバーにかかる負荷も軽減されます。

![](https://storage.googleapis.com/zenn-user-upload/67d1179decc6-20240419.png)
*静的なサイトジェネレーターはコンテンツを事前に生成し、サーバーはそれを提供します。動的なジェネレーターはリクエストごとにコンテンツを生成します。なので、静的な場合はコンテンツの更新が難しく、動的な場合はサーバー負荷が高くなる可能性があります。*

## Gatsbyで開発する
https://www.gatsbyjs.com/docs/quick-start/
今回は公式ドキュメントに書いてある手順通りに進めていきました。

1. #### 新しいサイトを作る
以下のコマンドを実行して新しいサイトを作ります。サイトのタイトルとプロジェクトのディレクトリ名を尋ねられるので入力して、JavaScriptまたはTypeScript、CMS、スタイリングツール、および追加機能を選択してください。
```
npm init gatsby
```
サイトの作成が完了すると、サイトのディレクトリに移動してローカルで実行するための手順が記載されたメッセージが表示されます。
以下のコマンドでサイトのルートディレクトリに移動しましょう。`my-gatsby-site`のところには作成したサイトのディレクトリ名を入力してください。
```
cd my-gatsby-site
```

2. #### ローカルサーバーを起動する
Gatsby は、デフォルトで[http://localhost:8000](http://localhost:8000) にアクセス可能なホットリローディングの開発環境を起動します。
ホットリローディングとは、開発中にコードを変更しても即座に反映されることです。
```
npm run develop
```
:::message alert
サイトを作成する際にGoogle Analyticsを追加した場合、以下のエラーメッセージが出る場合があります。
このエラーメッセージが出た場合は、Google AnalyticsのサービスのトラッキングIDを入力してください。まだ取得していないという方は新しく作ってください。
他の解決策があればコメントにて教えていただけるとありがたいです。
```
Invalid plugin options for "gatsby-plugin-google-gtag":

- "trackingIds" is required
```
```js:gatsby-config.js
// gatsby-config.js

module.exports = {
  plugins: [
    {
      resolve: "gatsby-plugin-google-gtag",
      options: {
        trackingIds: [
          "YOUR_GOOGLE_ANALYTICS_TRACKING_ID",
        ],
      },
    },
  ],
}
```
:::

3. #### 基本的な操作
GatsbyはReactベースのフレームワークなので、基本的な操作はReactと非常に似ています。以下は、GatsbyでのReactコンポーネントの基本的な操作です。

## 使ってみた感想
今まではRailsかNext.jsで開発していたのですが、一番かRailsの次くらいにシンプルで使いやすいなと感じました。まだ使ったことはありませんがMarkdown記法がプラグインか何かで追加できるらしいので今度使ってみたいです。
そして新しいフレームワークなどを触り始める時は何より公式ドキュメントをしっかり読むことの大切さを改めて実感しました。

---

まだGatsbyを使い始めてすぐの初心者なので記事の内容に間違いがあればコメントにてご指摘いただけるとありがたいです。