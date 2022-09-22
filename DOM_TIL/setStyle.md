# style の適用

### Element.style.property

HTML に直接書き込むインラインスタイルとして CSS のプロパティを変更する。
スタイルの優先順では HTML 内に書き込まれたスタイルが優先的に使用されるため効力は大きい。
JS でインラインスタイルを変更した場合は既存の HTML でのインラインを上書きする。

### getComputaed(element).property

スタイルの算出を行う
どの要素にどのプロパティがどの程度適用されているのかを確認できる。
算出されるためこれを利用し新たに値を更新したり、別の要素に対して絶対値ではなく動的に値を代入できたりすることができる。

### document.documentElement.style.setProperty(propertyName, value, priority)

style と異なり、より詳しくプロパティをセットすることができる。
css 内で使っている変数や important なども設定することが可能。
propertyName...スタイルのプロパティ名
value...スタイルの値
priority...important 等を指定すると css 内で!important を付与することができる

### element.setAttribute("attribute","name")

### element.getAttribute("attribute","name")
