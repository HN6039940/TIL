# HTMLElement の操作

---

##　目次

- 要素の選択
- 要素の作成/追加
- 要素の挿入
- 要素の削除

---

### 要素の選択

DOM 操作をするにあたって、要素を取得する準備が必要。

---

#### document.getElementById(ID 名)

HTML 文書から指定された ID 名の要素を取得する

```HTML
<section id = "section1">
<div class = "div1">This is div1</div>
</section>
```

```JavaScript
const getsectionID = document.getElementById("section1");

// <section id = "section1">
// <div class = "div1">This is div1</div>
// </section>
```

#### document.getElementByTagName(クラス名)

HTML 文書から指定されたクラス名の要素を取得する

```HTML
<div class = "div1">This is div1</div>
<div class = "div1">This is div2</div>
```

```JavaScript
const getDivClasses = document.getElementByTagName("div1");

// HTMLCollection(2)
// 0: div.div1
// 1: div.div1
```

#### document.querySelector(セレクタ名)

HTML 文書から指定された ID またはクラスの要素を取得する

```HTML
<section id = "section1">
<div class = "div1">This is div1</div>
</section>
<section id = "section1">
<div class = "div2">This is div2</div>
</section>
```

```JavaScript
const getAllSectionClasses = document.querySelector("#section1");

// NodeList(2)
// 0: section#section1
// 1: section#section2
```

#### document.querySelectorAll(セレクタ名)

HTML 文書から指定された**全て**の ID またはクラスの要素を取得する

```HTML
<div class = "div1">This is div1</div>
<div class = "div1">This is div2</div>
```

```JavaScript
const getAllDiv1Classes = document.querySelectorAll(".div1");

// NodeList(2)
// 0: div.div1
// 1: div.div1
```

 <details><summary>HTMLCollection と NodeList について</summary>
 HTMLCollecttionとNodeListはどちらもArrayではない配列風オブジェクトで
 戻り値として返る。
 内容としてはどちらもノードつまりHTMLの要素が返ってくる。<br>
 しかし明確な違いとして挙げられるのは、使った関数での戻り値が異なる。<br>
 一番な違いとして挙げられるのは、`DOM操作に対して動的か静的か`。<br>
 動的なのは、HTMLcollection。静的なのは、NodeListである。
 </details>

---

### 要素の作成/追加

1 から要素を作成する事も JavaScript から操作することで作成が可能になる。

HTML をわざわざいじらず動的に作成可能。

---

#### document.createElement(tagname)

tagname で指定された HTML 文書を作成する。

```HTML
<h1></h1>
```

上記のように要素を作成したい場合は

```JavaScript
const generateH1 = document.createElement("h1")
// <h1></h1>
```

#### element.classList.add(クラス名)

要素に対して指定したクラス名を追加する。

```HTML
<h1 class = "h1tag"></h1>
```

上記のようなクラスを追加したい場合

```JavaScript
generateH1.classList.add("h1tag")
// <h1 class = "h1tag"></h1>
```

クラスを削除したい場合は、

```JavaScript
generateH1.classList.remove("h1tag")
// <h1></h1>
```

#### element.setAttribute("属性の名前","追加する値")

下記の通り ID セレクタなどを追加したい場合は

```HTML
<h1 id = "h1id" class = "h1tag"></h1>
```

```JavaScript
generateH1.setAttribute("id","h1id")
// <h1 id = "h1id" class = "h1tag"></h1>
```

 <details><summary>DOM で操作できる要素はユニーク</summary>

基本的に操作できるノードは同じクラス名が複数存在したとしても、
1 つのみ操作ができる。
そもそも querySelector などで取得した要素は、それそのものを指示しているため全てを指示していない。
また、後述する element.innnerHTML や element.remove などは指し示した element そのものに対して作用する為複数の要素を DOM で一度に操作することは不可能。
<a href = "#複数の要素を処理したい">ではどうするべきか？</a>

</details>

---

### 要素の挿入

既存の HTML 文書に新たに要素を追加したい。

または、文章や要素の内容を変更したい書き換えたい場合などに使われる。

---

#### element.innerHTML

要素内の HTML または XML のマークアップを取得したり設定したりします。

```HTML
<section id = "section1">
<div class = "div1">This is div1</div>
</section>
<section id = "section1">
<div class = "div2">This is div2</div>
<div class = "innerdiv"></div>
</section>
```

```JavaScript
const innerDiv = document.querySelector(".innerdiv");
innerDiv.innerHTML = "This is innerdiv";

// <div class = "innerdiv"> This is innerdiv </div>
```

```JavaScript
const div1 = document.querySelector(".div1");
const innerDiv = document.querySelector(".innerdiv");
innerDiv.innerHTML = div1.innerHTML

// <div class = "innerdiv"> This is div1 </div>
```

#### element.prepend

element の子要素として先頭に HTML 要素を配置する

```HTML
<div class = "prependDiv">
<p>テキストテキストテキスト</p>
</div>
```

```JavaScript
const div = document.querySelector(".prependDiv")
const h1 = document.createElement("h1")
h1.innerHTML = "This is H1"
div.append(h1)

// <div class = "prependDiv">
// <h1>This is H1</h1>
// <p>テキストテキストテキスト</p>
// </div>
```

#### element.append

element の子要素として末尾に HTML 要素を配置する

```HTML
<div class = "appendDiv">
<p>テキストテキストテキスト</p>
</div>
```

```JavaScript
const div = document.querySelector(".appendDiv")
const h1 = document.createElement("h1")
h1.innerHTML = "This is H1"
div.append(h1)

// <div class = "appendDiv">
// <p>テキストテキストテキスト</p>
// <h1>This is H1</h1>
// </div>
```

#### element.before

element の兄弟要素として先頭に HTML 要素を配置する

```HTML
<div class = "beforeDiv">
<p>テキストテキストテキスト</p>
</div>
```

```JavaScript
const div = document.querySelector(".beforeDiv")
const h1 = document.createElement("h1")
h1.innerHTML = "This is H1"
div.append(h1)

// <h1>This is H1</h1>
// <div class = "beforeDiv">
// <p>テキストテキストテキスト</p>
// </div>
```

#### element.after

element の兄弟要素として末尾に HTML 要素を配置する

```HTML
<div class = "afterDiv">
<p>テキストテキストテキスト</p>
</div>
```

```JavaScript
const div = document.querySelector(".afterDiv")
const h1 = document.createElement("h1")
h1.innerHTML = "This is H1"
div.append(h1)

// <div class = "afterDiv">
// <p>テキストテキストテキスト</p>
// </div>
// <h1>This is H1</h1>
```

#### element.insertAdjacentHTML(postion,text)

element を始点とし引数で指定された postion に指定された text を挿入します。

```HTML
<div class = "insertAdjacent">
<p>テキストテキストテキスト</p>
</div>
```

```JavaScript
const divClass = document.querySelector(".insertAdjacent")
const createH1 = document.createElement("h1")
createH1.innerHTML = "This is H1";
createH1.classList.add("insertAdH1")
divClass.insertAdjacent("afterbegin",createH1)

// <div class = "insertAdjacent">
// <h1 class="insertAdH1">This is H1</h1>
// <p>テキストテキストテキスト</p>
// </div>
```

---

### postion について

<img src="https://i.imgur.com/EQTuB12.jpg" alt = "postionの説明"></img>

https://developer.mozilla.org/ja/docs/Web/API/Element/insertAdjacentHTML

#### beforebegin

element.before()と同じ位置に要素が入れられる

#### afterbegin

element.prepend()と同じ位置に要素が入れられる

#### beforeend

element.append()と同じ位置に要素が入れられる

#### afterend

element.after()と同じ位置に要素が入れられる

---

### 要素の削除

#### element.remove()

element を消去する

```HTML
<div class = "removediv">
<p>テキストテキストテキスト</p>
</div>

<div class = "notremove">
<p>テキストテキストテキスト</p>
</div>
```

```JavaScript
const div = document.querySlector(".removediv")
div.remove()

// <div class = "notremove">
// <p>テキストテキストテキスト</p>
// </div>
```

#### element.parentElement.removeChild()

親要素の子要素を消去する

```HTML
<div class = "removediv">
<p class = "childText">テキストテキストテキスト</p>
</div>
```

```JavaScript
const p_text = document.querySlector(".childText")
p_text.parentElement.removeChild()

// <div class = "removediv">
// </div>
```

#### element.parentElement.remove()

親要素の消去

```HTML
<div class = "removediv">
<p>テキストテキストテキスト</p>
</div>

<div class = "notremove">
<p>テキストテキストテキスト</p>
</div>
```

```JavaScript
const div = document.querySlector(".removediv")
div.remove()

// <div class = "notremove">
// <p>テキストテキストテキスト</p>
// </div>
```

#### element.innnerHTML = ""

innerHTML で中身を空にする
つまり消去と同じになる

---

### 複数の要素を処理したい

前述したとおり DOM での操作は一回の操作に一つの要素しか
動かせない。

例えば同じクラス名を持った要素はまとめて一回で消すことができない。
一番初めの先頭部分の要素だけが適用される。

そして複数当てはまる要素は、NodeList として配列風オブジェクトとして保管されている。

あくまで Array ではなく Nodelist として扱われているため
配列のメソッドをそのまま使うことができない。

配列に返還した後に各種配列メソッドを使えば
全ての要素に対してや特定の要素に対して処理が可能になる。

forEach や map を使えば実現が可能になる。
Array(NodeList)から個別(HTMLelement)でコールバック関数が処理するからだ。
