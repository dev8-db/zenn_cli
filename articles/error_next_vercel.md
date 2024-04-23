---
title: "VercelでのNext.jsデプロイ時のタグ関連エラー対処法"
emoji: "😎"
type: "tech"
topics: [nextjs, vercel]
published: true
---

## 今回起きたエラー
Next.jsで[自分のWebページ](https://dev8.vercel.app)を開発していたところ、Vercelにデプロイしようとしてもできないエラーが複数発生しました。

## <img>タグ
<img>タグを使用して画像を表示させていたところ以下のエラーが出ました。
```
Warning: Using `<img>` could result in slower LCP and higher bandwidth. Consider using `<Image />` from `next/image` to automatically optimize images. This may incur additional usage or cost from your provider. See: https://nextjs.org/docs/messages/no-img-element  @next/next/no-img-element
```
```
Warning: img elements must have an alt prop, either with meaningful text, or an empty string for decorative images.  jsx-a11y/alt-text
```

### エラーの内容
- `<img>`タグを使うとページの読み込みに時間がかかるので`<Image />`タグを使って欲しい
- `<img>`タグには`alt`を指定しなければいけない

### 対策
今まで画像の読み込みには`<img>`タグを使っていたのですが、ここで`<Image />`タグに切り替えました。
あと、画像のwidthとheightも指定しなければいけないそうです。
```js:src/pages/index.js
// Imageをインポート
import Image from "next/image";

function hogehoge() {
    return (
        <div>
            <Image src="/hogehoge.png" alt="ほげほげ" width={50} height={50} />
        </div>
    )
}

export { hogehoge as default };
```

## <a>タグ
`<a>`タグも同様にエラーが起きました。
```
Error: Do not use an `<a>` element to navigate to `/`. Use `<Link />` from `next/link` instead. See: https://nextjs.org/docs/messages/no-html-link-for-pages  @next/next/no-html-link-for-pages
```

### エラーの内容
- `<a>`タグを使わずに`<Link>`タグを使って欲しい

### 対策
こちらも同じようにnextからインポートして書き換えました。
```js:src/pages/index.js
// Linkをインポート
import Link from "next/link";

function hogehoge() {
    return (
        <div>
            <Link src="/hogehoge" as="/hogehoge">ほげほげ</Link>
        </div>
    )
}

export { hogehoge as default };
```

## まとめ
Next.jsは難しい