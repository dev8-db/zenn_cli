---
title: "【Next.js】なぜimgタグではなくnext/imageを使うのか"
emoji: "🍣"
type: "tech"
topics: [next]
published: true
---

## なぜnext/imageを使うのか
Next.jsの `next/image` コンポーネントは、画像の最適化と管理を簡単にするために提供されています。例えば、自動的に画面サイズに合わせて画像の大きさを比率を保ったまま調整してくれたり（レスポンシブ画像）、よりファイルサイズが小さいWebPに自動変換してくれたりします。

私が考えるメリットは以下の通りです。

### フォーマット変換
`next/image` を使うと、WebPに対応しているブラウザはPNGやJPEGなどがWebPに変換されます。
実際に `next/image` で指定した画像にアクセスすると、拡張子が `.webp` になっていることが確認できます。
これによりファイルサイズが小さくなり、ページの読み込みが早くなります。

### レスポンシブ
CSSでいちいちモバイルに対応する画像のサイズを指定してもしなくとも、自動的に画像の比率を保ったままサイズを変更してくれます。助かる！！！

### Lazy Loading
その画像が必要になるまで読み込まないようにする機能です。`next/image` ではLazy Loading機能に対応しています。`loading="lazy"` を画像のタグに追加するだけで指定することができます。

## 使い方
以下のようなコードで簡単に利用できます。alt, width, heightは必須です。
```js
import Image from 'next/image'

function MyImage() {
  return (
    <Image
      src="/me.png"  // 画像のパス
      alt="Picture of the author"  // 代替テキスト（必須）
      width={500}  // 幅（必須）
      height={500}  // 高さ（必須）
    />
  )
}
```

## 対応プロパティ
| プロパティ | 例 | ステータス | 説明 |
| --- | --- | --- | --- |
| src | src="/hello.png" | 必須 | 画像のソースファイルパス |
| width | width={500} | 必須 | 画像の幅 |
| height | height={500} | 必須 | 画像の高さ |
| alt | alt="Cat" | Text | 代替テキスト（画像が表示されない場合に代わりに表示されるテキスト） |
| loader | loader={imageLoader} | - | 画像のローディング方法をカスタマイズするための関数 |
| fill | fill={true} | - | 親コンテナーに対して画像をフィットさせるかどうかのブール値 |
| sizes | sizes="(max-width: 768px) 100vw, 33vw" | - | 画像の表示サイズを指定するためのメディア条件とサイズのリスト |
| quality | quality={80} | - | 画像の品質を指定する値（一般的には JPEG 画像の圧縮率） |
| priority | priority={true} | - | 画像のローディングを優先させるかどうかのブール値 |
| placeholder | placeholder="blur" | - | 画像がロードされるまでのプレースホルダーの種類 |
| style | style={{objectFit: "contain"}} | - | 画像のスタイルを指定するオブジェクト |
| onLoadingComplete | onLoadingComplete={img => done())} | 廃止されました | 画像のロード完了時に実行される関数 |
| onLoad | onLoad={event => done())} | - | 画像のロード完了時に実行される関数 |
| onError | onError(event => fail()} | - | 画像のロードエラー時に実行される関数 |
| loading | loading="lazy" | - | 画像のローディング方法を指定する属性 |
| blurDataURL | blurDataURL="data:image/jpeg..." | - | 画像がロードされるまでのプレースホルダーとして使用されるぼかし画像のデータ URL |
| overrideSrc | overrideSrc="/seo.png" | - | 特定の条件下で画像のソースを上書きするためのパス |

---

もっと詳しく知りたい場合は公式ドキュメントをご覧ください。
https://nextjs.org/docs/pages/api-reference/components/image