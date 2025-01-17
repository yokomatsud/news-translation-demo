---
title: JavaScript Date Now – JavaScriptで現在の日付を取得する方法
date: 2024-07-21T15:30:24.719Z
authorURL: ""
originalURL: https://www.freecodecamp.org/news/javascript-date-now-how-to-get-the-current-date-in-javascript/
translator: ""
reviewer: ""
---

多くのアプリケーションでは、リソースの作成日やアクティビティのタイムスタンプなど、何らかの日付コンポーネントが含まれることがあります。

<!-- more -->

日付やタイムスタンプのフォーマットを扱うのは骨が折れることがあります。このガイドでは、JavaScriptで現在の日付をさまざまなフォーマットで取得する方法を学びます。

## JavaScriptのDateオブジェクト

JavaScriptには、日付と時間を保持し、それらを処理するためのメソッドを提供する組み込みの`Date`オブジェクトがあります。

`Date`オブジェクトの新しいインスタンスを作成するには、`new`キーワードを使用します：

```js
const date = new Date();
```

`Date`オブジェクトには、Epoch（1970年1月1日）以降のミリ秒を表す`Number`が含まれています。

指定した日付のオブジェクトを作成するために、日付の文字列を`Date`コンストラクタに渡すことができます：

```js
const date = new Date('Jul 12 2011');
```

現在の年を取得するには、`Date`オブジェクトのインスタンスメソッドである`getFullYear()`を使用します。`getFullYear()`メソッドは、`Date`コンストラクタで指定された日の年を返します：

```js
const currentYear = date.getFullYear();
console.log(currentYear); //2020
```

同様に、現在の日と月を取得するメソッドもあります：

```js
const today = date.getDate();
const currentMonth = date.getMonth() + 1; 
```

`getDate()`メソッドは、月の現在の日（1から31）を返します。

`getMonth()`メソッドは、指定された日付の月を返します。`getMonth()`メソッドについて注意すべき点は、0から始まる値（0は1月、11は12月）を返すことです。したがって、月の値を正規化するために1を追加します。

## Date now

`now()`は`Date`オブジェクトの静的メソッドです。これは、Epoch以降の経過時間をミリ秒で表す値を返します。`now()`メソッドから返されたミリ秒を`Date`コンストラクタに渡して、新しい`Date`オブジェクトをインスタンス化することができます：

```js
const timeElapsed = Date.now();
const today = new Date(timeElapsed);
```

## 日付のフォーマット

`Date`オブジェクトのメソッドを使用して、複数のフォーマット（GMT、ISOなど）で日付をフォーマットすることができます。

`toDateString()`メソッドは、人間が読みやすい形式で日付を返します：

```js
today.toDateString(); // "Sun Jun 14 2020"
```

`toISOString()`メソッドは、ISO 8601拡張形式に従った日付を返します：

```js
today.toISOString(); // "2020-06-13T18:30:00.000Z"
```

`toUTCString()`メソッドは、UTCタイムゾーン形式の日付を返します：

```js
today.toUTCString(); // "Sat, 13 Jun 2020 18:30:00 GMT"
```

`toLocaleDateString()`メソッドは、ローカリティに依存した形式で日付を返します：

```js
today.toLocaleDateString(); // "6/14/2020"
```

`Date`メソッドの完全なリファレンスは、[MDNのドキュメント][1]で確認できます。

## カスタム日付フォーマッタ関数

上記のセクションで言及したフォーマット以外にも、アプリケーションでは`yy/dd/mm`や`yyyy-dd-mm`など、異なる形式の日付が必要な場合があります。

この問題に対処するために、複数のプロジェクトで使用できる再利用可能な関数を作成するのが良いでしょう。

このセクションでは、関数の引数で指定された形式で日付を返すユーティリティ関数を作成しましょう：

```js
const today = new Date();

function formatDate(date, format) {
    //
}

formatDate(today, 'mm/dd/yy');
```

引数として渡されたフォーマット文字列から、「mm」、「dd」、「yy」をそれぞれの月、日、年の値に置き換える必要があります。

このために、`replace()`メソッドを以下のように使用できます：

```js
format.replace('mm', date.getMonth() + 1);
```

しかし、これでは多くのメソッドチェーンが必要となり、関数をより柔軟にしようとすると維持が難しくなります：

```js
format.replace('mm', date.getMonth() + 1)
    .replace('yy', date.getFullYear())
    .replace('dd', date.getDate());
```

メソッドチェーンを使用する代わりに、正規表現と`replace()`メソッドを組み合わせることができます。

最初に、サブストリングとその対応する値のキー-バリューのペアを表すオブジェクトを作成します：

```js
const formatMap = {
    mm: date.getMonth() + 1,
    dd: date.getDate(),
    yy: date.getFullYear().toString().slice(-2),
    yyyy: date.getFullYear()
};
```

次に、正規表現を使用して文字列をマッチングし置換します：

```js
formattedDate = format.replace(/mm|dd|yy|yyy/gi, matched => map[matched]);
```

完全な関数は次のようになります：

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

また、関数にタイムスタンプをフォーマットする機能を追加することもできます。

## 結論

JavaScriptの`Date`オブジェクトについての理解が深まったことを願っています。また、アプリケーションで日付を処理するために`datejs`や`moment`などのサードパーティライブラリを使用することもできます。

元のMarkdownファイルを提供していただけると、その内容を日本語に翻訳します。Markdownのレイアウトを厳密に保持しながら翻訳するため、具体的なメッセージやテキストをここにコピーしてください。

