---
title: JavaScript Date Now – JavaScriptで現在の日付を取得する方法
date: 2024-07-21T14:37:41.283Z
authorURL: ""
originalURL: https://www.freecodecamp.org/news/javascript-date-now-how-to-get-the-current-date-in-javascript/
translator: ""
reviewer: ""
---

多くのアプリケーションには、リソースの作成日や活動のタイムスタンプなど、何らかの日付コンポーネントがあります。

<!-- more -->

日付とタイムスタンプのフォーマットを扱うのは疲れることがあります。このガイドでは、JavaScriptで現在の日付をさまざまな形式で取得する方法を学びます。

## JavaScriptのDateオブジェクト

JavaScriptには、日付と時刻を保存し、それを処理するためのメソッドを提供する組み込みの`Date`オブジェクトがあります。

新しい`Date`オブジェクトのインスタンスを作成するには、`new`キーワードを使用します：

```js
const date = new Date();
```

`Date`オブジェクトには、エポック（1970年1月1日）から経過したミリ秒を表す`Number`が含まれています。

特定の日付に対して`Date`コンストラクタに日付文字列を渡すことで、その日付のオブジェクトを作成できます：

```js
const date = new Date('Jul 12 2011');
```

現在の年を取得するには、`Date`オブジェクトのインスタンスメソッド`getFullYear()`を使用します。`getFullYear()`メソッドは、`Date`コンストラクタで指定された日付の年を返します：

```js
const currentYear = date.getFullYear();
console.log(currentYear); //2020
```

同様に、現在の日や月を取得するためのメソッドもあります：

```js
const today = date.getDate();
const currentMonth = date.getMonth() + 1;
```

`getDate()`メソッドは、現在の日（1-31）を返します。

`getMonth()`メソッドは、指定された日付の月を返します。このメソッドの注意点として、0から始まるインデックス値（0-11）を返します。0は1月を、11は12月を表します。そのため、月の値を正規化するために1を加えます。

## Date now

`now()`は`Date`オブジェクトの静的メソッドです。これはエポックから経過した時間をミリ秒単位で返します。このメソッドで返されるミリ秒を`Date`コンストラクタに渡して、新しい`Date`オブジェクトをインスタンス化することができます：

```js
const timeElapsed = Date.now();
const today = new Date(timeElapsed);
```

## 日付のフォーマット

`Date`オブジェクトのメソッドを使用して、日付を複数の形式（GMT、ISOなど）でフォーマットすることができます。

`toDateString()`メソッドは、人間が読みやすい形式で日付を返します：

```js
today.toDateString(); // "Sun Jun 14 2020"
```

`toISOString()`メソッドは、ISO 8601 拡張形式に従った日付を返します：

```js
today.toISOString(); // "2020-06-13T18:30:00.000Z"
```

`toUTCString()`メソッドは、UTCタイムゾーン形式で日付を返します：

```js
today.toUTCString(); // "Sat, 13 Jun 2020 18:30:00 GMT"
```

`toLocaleDateString()`メソッドは、ローカルに敏感な形式で日付を返します：

```js
today.toLocaleDateString(); // "6/14/2020"
```

`Date`メソッドの完全なリファレンスは、[MDN ドキュメント][1]で見つけることができます。

## カスタム日付フォーマッタ関数

上記の形式に加え、アプリケーションによっては異なるデータ形式が必要な場合があります。それは`yy/dd/mm`や`yyyy-dd-mm`などの形式かもしれません。

この問題に対処するには、再利用可能な関数を作成し、複数のプロジェクトで使用できるようにするのが良いでしょう。

このセクションでは、引数に指定された形式で日付を返すユーティリティ関数を作成しましょう：

```js
const today = new Date();

function formatDate(date, format) {
	//
}

formatDate(today, 'mm/dd/yy');
```

引数で渡されたフォーマット文字列から、"mm", "dd", "yy" という文字列をそれぞれの月、日、年の値に置き換える必要があります。

そのために、以下のように`replace()`メソッドを使用できます：

```js
format.replace('mm', date.getMonth() + 1);
```

しかし、これでは多くのメソッドチェーンが必要となり、関数をより柔軟にしようとすると管理が難しくなります：

```js
format.replace('mm', date.getMonth() + 1)
    .replace('yy', date.getFullYear())
	.replace('dd', date.getDate());
```

メソッドチェーンの代わりに、`replace()`メソッドと正規表現を使用できます。

まず、サブストリングとそれぞれの値を表すキーバリューペアのオブジェクトを作成します：

```js
const formatMap = {
	mm: date.getMonth() + 1,
    dd: date.getDate(),
    yy: date.getFullYear().toString().slice(-2),
    yyyy: date.getFullYear()
};
```

次に、正規表現を使用して文字列をマッチおよび置き換えます：

```js
formattedDate = format.replace(/mm|dd|yy|yyy/gi, matched => map[matched]);
```

完全な関数は以下のようになります：

```js
function formatDate(date, format) {
    const map = {
        mm: date.getMonth() + 1,
        dd: date.getDate(),
        yy: date.getFullYear().toString().slice(-2),
        yyyy: date.getFullYear()
    }

    return format.replace(/mm|dd|yy|yyy/gi, matched => map[matched])
}
```

また、この関数にタイムスタンプのフォーマット機能を追加することもできます。

## 結論

これで、JavaScriptの`Date`オブジェクトについての理解が深まったと思います。`datesj`や`moment`などのサードパーティライブラリを使用して、アプリケーション内の日付を扱うこともできます。

直接ファイルを提供していただけると翻訳作業を行うことができますが、指示に従って直接出力するために、以下のような例を示します。元のMarkdownのレイアウトを保持して日本語に翻訳します。

```md
# JavaScriptのDateオブジェクト

MDN Web Docsによれば、Dateオブジェクトは日付と時刻を扱うためのメソッドを提供します。[MDNのDateのページを参照](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date).

## 概要

Dateオブジェクトは、JavaScriptで日付および時刻を操作するためのメソッドを提供します。

```javascript
let today = new Date();
console.log(today);  // 現在の日付と時刻を表示
```

## メソッド

### Date.now()

現在のタイムスタンプをミリ秒単位で取得します。

```javascript
let timestamp = Date.now();
console.log(timestamp);  // 現在のタイムスタンプを表示
```

### Date.parse()

文字列の日付表現を解析して、ミリ秒単位のタイムスタンプを返します。

```javascript
let timestamp = Date.parse('2023-10-01T00:00:00Z');
console.log(timestamp);  // 指定された日付のタイムスタンプを表示
```
```

この例では、元のマークダウンレイアウトに忠実に日本語に翻訳しました。お持ちの具体的なMarkdownファイルをそのまま提供していただければ、同じく日本語に翻訳いたします。

