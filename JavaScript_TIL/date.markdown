# Date について

## 日付の作成

**new Date()**

現在の日付や時刻、タイムゾーンを表示する。

```javascript
const now = new Date();
```

`Mon Jun 28 2021 01:16:11 GMT+0900 (GMT+09:00)`

**_（現在の日付なので人によって表示は異なります）_**

Date の引数に"年、月、日、時間、分、秒"を直接書くこともできる。

```javascript
const now = new Date(2021, 6, 28, 1, 16, 11);
```

`Mon Jun 28 2021 01:16:11 GMT+0900 (GMT+09:00)`

<details><summary>引数なしと引数ありのちがい</summary>
引数が与えられなかった場合は、現在の曜日を含めた日付と時刻を表します。<br>
引数が少なくとも1つでも指定された場合、(年、月、日、時、分、秒、ミリ秒) の<br>順番で引数から取得した Date オブジェクトを返します。

</details>

---

## 日付を扱う関数

[.getFullYear()](#dategetfullyear)
年を取得する

[.getMonth()](#dategetmonth)
月を取得する

[.getDate()](#dategetdate)
日にちを取得する

[.getDay()](#dategetday)
曜日を取得する

[.getHours()](#dategethours)
時間を取得する

[.getMinutes()](#dategetminutes)
分を取得する

[.getSeconds()](#dategetseconds)
秒数を取得する

[.toISOString()](#datetoisostring)
日付を文字列として出力する

new Date.getTime()
UNIX[^1] 元期からの経過ミリ秒数を返す
[^1]:UNIX 時間または UNIX 時刻とはコンピューターシステム上での時刻表現の一種。

Date.now()
UTC (協定世界時) での 1970 年 1 月 1 日 0 時 0 分 0 秒 から現在までの経過時間をミリ秒単位で返します

---

### Date.getFullYear()

指定された日時の「年」を返します。

```JavaScript
const now = new Date(2021,6,28).getFullYear();
```

この場合は、引数の`2021`となります

### Date.getMonth()

指定された日時の「月」を返します。

```JavaScript
const now = new Date(2021,6,28).getMonth();
```

この場合は、引数の`6`となります

### Date.getDate()

指定された日時の「日」を返します。

```JavaScript
const now = new Date(2021,6,28).getDate();
```

この場合は、引数の`28`となります

### Date.getDay()

指定された日時の「曜日」を**数値**で返します。

```JavaScript
const now = new Date().getMonth();
```

`0～6`のいずれかになります。

日本人は月曜日が週の初めなので最初が月曜日と思いがちかもしれませんが、
始まりは**日曜日**からになっています。

0 日曜日
1 月曜日
2 火曜日
3 水曜日
4 木曜日
5 金曜日
6 土曜日

慣れない場合は+1 して、1 から始めるようにするといいかもしれません。

```JavaScript
const now = new Date().getMonth() + 1;
```

### Date.getHours()

指定された日時の「時間」に相当する値を返します。

```JavaScript
const now = new Date().getHours();
```

`0~23`いずれかの数字が出力される

### Date.getMinutes()

指定された日時の「分数」に相当する値を返します。

```JavaScript
const now = new Date().Minutes();
```

`00~59`いずれかの数字が出力される。

### Date.getSeconds()

指定された日時の「秒数」に相当する値を返します。

```JavaScript
const now = new Date().getSeconds();
```

`00~59`いずれかの数字が出力される。

### Date.toISOString()

指定された日時の「時間」に相当する値を返します。

```JavaScript
const now = new Date().toISOString();
```

`"2021-06-28T14:37:33.089Z"`

簡潔な拡張表記の ISO 形式 ([ISO 8601](https://ja.wikipedia.org/wiki/ISO_8601 "ISO8061Wikipedia")) の文字列を返します。

<details><summary>常に 24 文字または 27 文字の長さになります。</summary>(YYYY-MM-DDTHH:mm:ss.sssZ または ±YYYYYY-MM-DDTHH:mm:ss.sssZ)</details>

### Date.getTime()

UNIX 元期からの経過ミリ秒数を返す

```JavaScript
const now = new Date().gettime();
```

1970 年 1 月 1 日から現在までの経過ミリ秒数
`1624892094083`と表示される。(_人によってこの数字は違います[^2]_)
[^2]:実行した時の時間は人によって異なる為

逆引きすることもできる。

```JavaScript
const now = new Date(1624892094083);
```

`Mon Jun 28 2021 23:54:54 GMT+0900 (GMT+09:00)`

### Date.now()

UNIX 元期からの経過ミリ秒数を返す

```JavaScript
const now = Date.now();
```

`1624892094083`と表示される。(_再度言いますが人によってこの数字は違います_)

<details><summary>Date.nowとnew Date.getTimeの違いについて</summary>
実行結果に差異はありません。<br>
Date.nowはIE8に対応していませんが高速で作動します。<br>
new Date.getTimeはnew Date() でインスタンスを生成するするため、<br>
同じ瞬間の次の日曜日までの日数を計算したり、<br>いろいろ「同じ瞬間」に関する計算をしたい場合はこちらを使うといいと思います。
</details>

---

### 日付の計算や換算について

算数、数学的な話になりますが、
1 日は、24 時間で表せるように、Date の関数と少しの計算を行うことで、<br>ミリ秒数を時間や日数など様々な単位で変換して表現することができます。

例えば日数を計算したい場合は、

```JavaScript
const now = Date.now();
const daysPassed = data1 =>
  Math.abs(data1 / (1000 * 60 * 60 * 24));
daysPassed(now)
```

以上のような計算で行えます。

1. Date.now()は現在のタイムスタンプをミリ秒数を表します。
2. ミリ秒数を秒数に戻す際はその時間に 1000 秒賭ける必要があります。
3. その数値を分にするために 60 をかけ、時間にするために 60 をかけています。
4. 時間に 24 をかけると日数に変化します。
5. それらを変換したいミリ秒数で割ると日数として表示されます。

ミリ秒数で割る為には同じ単位でわらないといけないのでこうなってます。
