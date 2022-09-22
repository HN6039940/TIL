# Intl について

---

## Intl って何？

ざっくりいえばインターナショナルつまり国際化って意味です。

**言語毎にフォーマットを切り替えよう！**

って感じです。

国によって暦の表記は、異なった形で表します。

- 2021/1/1
- 01/01/2021
- 2021/01/01 ...etc

こういった差分を統一せずに使用している言語等に基づいて、

表記を変えるために Intl オブジェクトは存在しています。

---

### どういった物を Intl で表せるのか？

- 数値
- 単位
- 日付...etc

---

### Intr オブジェクトの作成

```JavaScript
new Intr;
```

オブジェクト自体はこれで作成できる。
Intr の形式で動くメソッドがいくつかあるが
詳しくは[ここ](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Intl)(MDN に飛びます)を参照。

---

### Intl.NumberFormat()

```JavaScript
new Intr.NumberFormat(local,{option}).format(number)
```

Intl.NumberFormat オブジェクトは、言語に依存した数値書式を可能にするオブジェクトのコンストラクター

---

### Intl.DateTimeFormat()

```JavaScript
new Intl.DateTimeFormat(locals,{option}).format(date)

```

Intl.DateTimeFormat オブジェクトは、言語に応じた日付と時刻の書式化を可能にするオブジェクトのためのコンストラクター

---

#### 引数

1. locales
2. options
3. number

`locales`... ローカライズしたい言語の ISO の書式形式で引数に指定する。
各国の ISO の書式一覧はここから → http://www.lingoes.net/en/translator/langcode.htm

`options`...option をつかうことで様々な出力される数字の設定を行うことができる。

` number` `date `...ローカライズしたい数値の値を`.format()`もワンセットで使わなければならない。
`new Date()`などを直接引数に使用することもできる。

---

### 引数 options について

option を設定することで、表記する暦を文字列や数値などを<br>カスタマイズされた物にすることができる。

- 書き方

```JavaScript
const options ={
hour: 'numeric',
minute: 'numeric',
day: 'numeric',
month: 'long',
year: 'numeric',
weekday: 'long',
}
```

```JavaScript
const option = {
  style: 'currency',
  unit: 'celsius',
  currency: 'JPY',
  useGrouping: false,
};
```

などといった様々な書式設定を行うことが可能。

例えば

key の
`style`は形式 `unit`は記号 `currency`は通貨単位

value の

`numeric`は数 `long`は文字

`currency`は通貨形式 `celsius`は摂氏マーク

`JPY`は円マーク を表している。

> `long`は、文字

この場合だと key が`month`や`weekday`なので

```JavaScript
const options ={
hour: 'numeric',
minute: 'numeric',
day: 'numeric',
month: 'long',
year: 'numeric',
weekday: 'long',
}

new Intl.DateTimeFormat("en-US",options).format()
```

`"Friday, July 2, 2021, 1:24 AM"`となる。

`en-US`英語圏では先に曜日が来て次に月日ときている。
そして、`options`で指定した`month`と`weekday`が`long`と指定されているので
_Friday_ _July_ と文字列で表記されている。
`numeric`で指定した場所は数字で表記されている。

---

## 細かい点

IntlFormat の引数を指定しなかった場合は、
自分がシステムで指定している言語で表記される。
つまり`JP`になるので、馴染み深い日付の表し方で表記されるはずだ。

これは引数に `window.navigator.language` を指定した際と同じ挙動になる。
