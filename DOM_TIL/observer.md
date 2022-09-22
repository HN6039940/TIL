# observer

### 交差 API

組み立て方および監視をしたい要素

```javaScript
const 変数名 = new IntersectionObserver(callback,option);

変数名.observe(監視したい要素)
```

### オプション

```javaScript
const option = {
    root:null,
    threshold:0,
    rootMargin:"0px"
}
```

root...監視する要素がどこを通過した際にコールバックをするかを決める。null 及びデフォルトはビューポートが基準になる。

threshold...監視している要素が root にどれくらい入ったらコールバック関数を呼び出すか？
配列で指定することで複数タイミングでコールバック関数を呼び出せる。
[0,0.2,0.6]

rootMargin... 監視している要素の範囲にマージンを設定することで、要素が root へ入る前にコールバック関数を呼び出す。負値を設定することで threshold のようにどの程度入ったかで、呼び出すことも可能。

### コールバック関数

```javaScript
const callback = function(entries,observer){}
```

第一引数には IntersectionObserverEntry の配列
つまり[IntersectionObserverEntry,...]が格納されている。
第二引数は observer 自体が格納されている。
後述する監視の停止などに使用する。

IntersectionObserver 内で呼ばれるコールバック関数内では監視している要素に対して特定のオブジェクトを用意している。
IntersectionObserverEntry というオブジェクトである。

```javaScript
boundingClientRect: DOMRectReadOnly {}
intersectionRatio:
intersectionRect: DOMRectReadOnly {}
isIntersecting: true
isVisible: false
rootBounds: DOMRectReadOnly {}
target:
time: 0
```

主に使用されるのは、交差したかどうか確認する isIntersecting や
どの要素を指し示しているのかを確認できる target などがある。

target に関しては、addEventListener のような e.target と同じようなものである。

### 交差の終了

コールバック関数内などで監視を終了したい場合は、

```javaScript
const callback = function(entries,observer){
    observer.unobserve("要素")
}
```

unobserve を使用する。
