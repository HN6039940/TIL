# React Route

SPA（シングルページwebアプリケーション）はつまり、ページの読み込みをせずにいか構築していくかが重要。
しかしＳＰＡはページが単一しか存在しないため、ＵＲＬなどでのルーティングが行われない。
つまりリンクを設定し、画面を読み込みで遷移させてしまうとSPAとして成立もしないことになる。
そこで、単一のDOMでルーティング毎にDOMの書き換えを行うことで、疑似的に単一のページでURL間での移動を行うことができるようにすればSPAを構築しながらURLでのルーティングも行うことができるようになる。

そこでリンクを設定しコンテンツを呼び込むときに、画面遷移する際更新が必要な箇所とそうではない箇所があった場合の判別をつけ無ければならない
わざわざリンク先にも同じコンポーネントを使用して遷移前後で共通したコンテンツの構築を行うのはリソースの無駄。

## React-router
リンクによって表示したいコンテンツとそうでないコンテンツを簡単に分けるにはreact-routerライブラリが必要

ライブラリのため **npm yarn**などでパッケージを追加
`npm install react-router-dom@6`

現行はversion6

index.js
Routerを実装したい場所にBrowserRouterが必要

`import {BrowserRouter} from "react-router-dom"`
`import {Route , Routes} from "react-router-dom"`

### ルーティングの設定

BrowserRouterはReactプロジェクト一つにつき一回のみ使用可能。

```javascript
import {BrowserRouter} from "react-router-dom"
import {Route , Routes} from "react-router-dom"

const root = () =>{
	return (
		<React.StrictMode>
			<BrowserRouter>
				<Routes>
					<Route/>
				</Routes>
			</BrowserRouter>
		</React.StrictMode>
	)
}
```

BrowserRouterでコンテンツを包むことで、Routes Routeを使用することが可能になる。

Routesは、ルートの起点となる場所で、そこの中で適切なRouteを設定することで、SPAでリンク移動を実装することができる。

```javaScript
<Route path="/" element= {<Parent/>} >
	<Route index element = {<IndexChild/>}
	<Route path="child" element = {<Child/>} />
</Route>
```

Routesに囲まれたRouteはpath elementと呼ばれる属性を付与することができる。

pathで指定されたルートを入れ込み移動すると、
elementで指定されたコンポーネントなどが表示される仕組みである。
また、pathをしていせずにindexを指定することで、親コンポーネントが読み込まれたときに、同時に自身も呼び出すことになっている。
この際は親コンポーネントに、しっかりとOutletを設定しなければ表示がされない点に注意。

### Link

しかし、pathで指定したとしても、実際にそのリンクに直接飛ばしてくれない。
飛ばすように設定を別途で行う必要性がある。
それがLink。

```JavaScript
const IndexChild = ()=>{
	return (
		<div>
		<LINK to = "/child">
			CLICK me when you want to get access child page
		<LINK/>
		</div>
	)
}
```

### Outlet
リンクの指定以外にも、コンテンツ自体をページに格納する為に必要なものがOutlet
Routeで囲んだ範囲の要素を管理しOutletは書かれた場所に適切に格納する。

```JavaScript

const Parent = () =>{
	return (
	<div>
		<h1>I am Parent Page</h1>
		<Outlet/>
	</div>
	)
}

const IndexChild = () => {
	return (
		<div>
			<LINK to = "/child">
				CLICK me when you want to get access child page
			<LINK/>
		</div>
	)
}

const Child = () => {
	return (
		<div>
			<h2>I am Child Page.</h2>
			<LINK to = "/" >
				home
			<LINK />
		</div>
	)
}

```

Outletはどの位置でコンポーネントを挿入するかを指定することで、
その位置に自身のRouter配下のコンポーネントを設置することができる。

上記の場合は、Parentが親のRouterのため自身のh1の兄弟要素として、配下のコンポーネントが設置されることになる。

つまりアクセス時には
Paren > indexChildが表示されていて、
indexChildのCliCK me...をクリックすることで、pathが **/child** になるため 
Parent > Child という表示になる。ここでhomeをクリックすると、pathが  **/** になるので、
また Parent> indexChildに戻ることになる。

### useNavigate
Linkと違って、pathの受け渡しを直接行わなくても、イベントなどでリンクの指定をすることで、指定したリンクに飛ばすことができる。

```javaScript

const navigation = usenavigate();

const goToNextPage = () => {
	navigation("path名")
}

const Button = ()=>{
	return(
	<div>
		<button onClick={goToNextPage}>click!</button>
	</div>	)
}

const nav = () => {
	return (
	<div>
		<Link to="path名">
	</div>
	)
}
```

別途Routeでルーティングの指定をしないといけないのは変わらないが、
アンカー要素以外にイベントでの登録で使えるので、応用が利く

現在のパスが localhost/menu/path1とした場合
```JavaScript
useNavigate("path2") localhost/menu/path1/path2
useNavigate("../path3") localhost/menu/path2
useNavigate("/path4") lacalhost/path4

```

パスの積み上げを行う際はそのまま
現在地のパスから置き換えるのなら ../を入れる
ルート基点からパスをしているなら /を入れる

これはLinkやRouteと変わらない。
