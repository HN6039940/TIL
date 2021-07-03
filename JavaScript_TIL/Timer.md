# タイマー処理について

---

### タイマーの設定

基本的にソースコードは読み込んだ順に出力される。
しかし、処理を遅延させて後から実行したい場合は、
タイマーの機能を使用すればいい。

タイマーを使用するには以下のようなメソッドを使用する。

**setTimeout()**

```JavaScript
setTimeout(function,delay,argument)
```

### 引数

`function`... `delay`で指定した秒数を経過した後実行する関数

`delay`... 遅延したい秒数。引数に指定しなかった場合は即実行される

`argment`... callbackfunction で受け渡したい引数

`delay`の単位は **ms** なので、

`1000msec=1sec`となる。

つまり 3 秒の遅延を行いたい場合は

```JavaScript
const timer = setTimeout((word)=>console.log(`${word} timer!`),3000,"3second" )
```

となる。

> const timer = setTimeout((word)=>console.log(`${word} timer!`),3000,"3second" )

実行結果は 3 秒後に "3second timer!"　と表示される

### タイマーの解除

設定したタイマーを解除するには、

```JavaScript
cleanTimeout(variable)
```

と設定する。

そうすると、タイマーが解除され実行されなくなる。

---

### 一定時間ごとに繰り返し特定の処理を行う

loop 処理とは異なり常に一定時間になると特定の処理を必ず行う。

**setInterval()**

```JavaScript
setInterval(function,delay,auguments)
```

### 引数

基本的に setTimeout と同じ引数を使うことができる。

`function`... `delay`で指定した秒数を経過した後実行する関数

`delay`... 遅延したい秒数。引数に指定しなかった場合は即実行される

`argment`... callbackfunction で受け渡したい引数

例えば以下のようなコードは、

```JavaScript
setInterval(function () {
  const now = new Date();
  console.log(`${now.getHours()}:${now.getMinutes()}:${now.getSeconds()}`);
}, 1000);
```

時間　分　秒　を常に 1 秒間隔で、更新していく。
new Date()は、常に実行するたびに時刻を取得する為
逐一新しい日付を取得できる。
それを利用し、date メソッドを使い時計のようなものを作ることができる。

### Interval の停止

setTimeout を止められるのと同じく、
setInterval も同様に動作を強制的に終了することができる。

```JavaScript
cleanInterval(varibles)
```

cleanInterval を使えばいい。

これを上手く使うと、

```JavaScript
 const tick = function () {

    const min = String(Math.trunc(count / 60)).padStart(2, 0);
    const sec = String(count % 60).padStart(2, 0);

    console.log(`${min}:${sec}`);

    // 0になったらタイマーを取り消す。
    if (count === 0) {
      clearInterval(timer);
      console.log('Count finish!');
    }

    count--;
  };

  // 10秒タイマーセット
  let count = 10;

  // 毎秒カウントダウン
  tick();
  const timer = setInterval(tick, 1000);
```

カウントダウンタイマーを実装することができる。

---

### 細かい点

setInterval で関数を呼び出すと
clearInterval で止めない限りは、
永遠に作動する為作動している関数を呼び出すと動いてるのとは
別のものが作動するので、挙動がおかしくなる可能性がある。

必ず clearInterval をセットで管理するのが大事。
