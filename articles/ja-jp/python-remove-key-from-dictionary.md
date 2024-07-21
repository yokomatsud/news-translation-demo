---
title: Pythonの辞書からキーを削除する方法 – Dictからキーを削除する方法
date: 2024-07-21T14:08:38.888Z
authorURL: ""
originalURL: https://www.freecodecamp.org/news/python-remove-key-from-dictionary/
translator: ""
reviewer: ""
---

辞書は、Pythonでキーと値の形式でデータを格納するための便利なデータ型です。そして、辞書から特定のキーと値のペアを削除する必要がある場合があります。

<!-- more -->

このチュートリアルでは、辞書の基本とキーを削除する方法を学びます。

## Pythonで辞書を書く方法

辞書は中括弧 `{}` で表され、キーと値のペアはコロン `:` で区切られます。例えば、次のコードは3つのキーと値のペアで辞書を初期化します:

```py
my_dict = {'apple': 2, 'banana': 3, 'orange': 5}
```

また、組み込み関数 `dict()` を使用して辞書を初期化することもできます。例えば:

```py
my_dict = dict(apple=2, banana=3, orange=5)
```

次に、Pythonの辞書からキーを安全に削除する方法を教えます。「安全に」とは、キーが実際に辞書に存在しない場合、コードがエラーを投げないことを意味します。

これを実現するために、`del` キーワード、`pop()` メソッド、および `popitem()` メソッドを使用する方法を学びます。最後に、Pythonを使用して辞書から複数のキーを削除する方法を紹介します。

さあ、始めましょう！

## `del` キーワードを使用して辞書からキーを削除する方法

辞書からキーと値のペアを削除する最も一般的な方法は、`del` キーワードを使用することです。また、全体の辞書や特定の単語を削除するためにも使用できます。

削除する値にアクセスするには、以下の構文を使用します:

```py
del dictionary[key]
```

例を見てみましょう:

```py
Members = {"John": "Male", "Kat": "Female", "Doe": "Female" "Clinton": "Male"}

del Members["Doe"]
print(Members)
```

出力:

```bash
{"John": "Male", "Kat": "Female", "Clinton": "Male"}
```

## `pop()` メソッドを使用して辞書からキーを削除する方法

辞書からキーと値のペアを削除する別の方法は、`pop()` メソッドを使用することです。構文は次のようになります:

```py
dictionary.pop(key, default_value)
```

例:

```py
My_Dict = {1: "Mathew", 2: "Joe", 3: "Lizzy", 4: "Amos"}
data = My_Dict.pop(1)
print(data)
print(My_Dict)
```

出力:

```bash
Mathew
{2: "Joe", 3: "Lizzy", 4: "Amos"}
```

## `popitem()` 関数を使用して辞書からキーを削除する方法

組み込みの `popitem()` 関数は、辞書から最後のキーと値のペアを削除します。削除する要素を指定することはできず、関数は入力を受け付けません。

構文は次のようになります:

```py
dict.popitem()
```

理解を深めるために例を考えてみましょう。

```py
# 辞書を初期化する
My_dict = {1: "Red", 2: "Blue", 3: "Green", 4: "Yello", 5: "Black"}

# popitem() を使用する
Deleted_key = My_dict.popitem()
print(Deleted_key)
```

出力:

```bash
(5, 'Black')
```

このように、関数は辞書から最後のキーと値のペア － `5: "Black"` － を削除しました。

## 辞書から複数のキーを削除する方法

Pythonを使用すると、辞書から複数のキーを簡単に削除できます。`.pop()` メソッドをキーのリスト全体にループで使用するのが最も安全な方法です。

存在しないいくつかのキーを含むユニークなキーのリストをどのように提供するか見てみましょう:

```py
My_dict = {'Sam': 16, 'John': 19, 'Alex': 17, 'Doe': 15}

# 削除するキーを定義する
keys = ['Sam', 'John', 'Doe']

for key in keys:
    My_dict.pop(key, None)

print(My_dict)
```

出力:

```bash
{'Alex': 17}
```

ループ内での `pop()` メソッドでは、キーが存在しない場合に `KeyError` が表示されないようにするために、`None` をデフォルト値として渡すことに注意してください。

## `clear()`メソッドを使用して辞書からすべてのキーを削除する方法

`clear()` メソッドを使用して、辞書からすべてのキーと値のペアを削除できます。構文は次のようになります:

```py
dictionary.clear()
```

例:

```py
Colors = {1: "Red", 2: "Blue", 3: "Green"}
Colors.clear()
print(Colors)
```

出力:

```bash
{}
```

## 結論

この記事では、辞書からキーと値のペア、または複数のキーと値のペアを削除するためのさまざまなPythonの方法について説明しました。

辞書からキーと値のペアを削除する最も一般的な方法である `del` キーワードを使用してこれを行うことができます。キーと値のペアを削除してその値も取得する必要がある場合には、`pop()` メソッドが便利です。辞書の最後のキーと値のペアを削除するには、`popitem()` 関数を使用できます。

また、辞書内のすべてのキーと値のペアを削除する必要がある場合は、`clear()` メソッドを使用できます。

[Twitter][1] と [LinkedIn][2] で接続しましょう。私の [YouTube][3] チャンネルにも登録できます。

ハッピーコーディング！

[1]: https://www.twitter.com/Shittu_Olumide_
[2]: https://www.linkedin.com/in/olumide-shittu
[3]: https://www.youtube.com/channel/UCNhFxpk6hGt5uMCKXq0Jl8A

