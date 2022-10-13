#作成までの流れ

###　プロジェクトの定義

誰のためにそのサイトを作るのか？
自分のためのサイトか？

そのサイトを使って何を伝えたいのか？
ゴールは何なのか？

商品の宣伝？販売？
何かを紹介したい？ブログ？娯楽？

**UX のゴールをこの段階で定義するべき**

複雑なゴール設定ではなく単純な物で構わない

例としては、

> ビジネスとしてのゴール：ユーザーに物を売りたい。<br>ユーザーのゴール：品質のいい物を買うためにサイトを訪問する

可能であればどこの層をターゲティングするかは比較的具体的に考えるべき

> 性別や年齢、住んでいる地域、職業など

###　プロジェクトの計画

コンテンツに必要な情報や画像テキストなどの
データを集める

サイトマップを作成する

サイトの流れや大まかなページの配置を考える
どのようにコンテンツが互いに紐づけされるかなど

デザインに引っ張られずにあくまで載せたいコンテンツを主導にページを構築すること

綺麗なページを作る為にコンテンツを疎かにするのではなく、載せたいコンテンツでレイアウトを構築していく

それに則ってウェブサイトのタイプや性格を決める

### 骨組みの構築

実際にデザインソフトやノートなどに
枠組みを作る
いきなりコードから書くことは厳禁

どのようなレイアウトパターンで作るかもここの段階で決める

> D, F, Z パターンの視線誘導や各種パーツの採用など

ただ必ずしもデザインソフトを使わないといけないわけではなく
場合によってはそのままコードから入ることもある。
また、デザイン通りに完全な物を作る必要性はない
あくまで、ある程度の骨組みで考える。

ここは厳格に行わず常に試行錯誤の繰り返しになる

### コードを書く

ある程度のラフデザインが完成したら
HTML CSS を用いてコードを書いていく

1. どのようなレイアウトパターン
2. Web サイトのイメージに合わせた書体や色
3. 指定されていた素材や書体が存在する場合はそれらを最優先で使っていく

定義　計画　構築　を経てようやくコードを書くことができる。
これらの基盤は非常に重要

### テストと最適化

コードが完成したらテストと最適化を行う

まずブラウザ上で動くかどうか？
chrome safari firefox edge などで動くか？
（レガシーブラウザの IE もある程度視野に入れつつ）

次にレスポンシブデザインを構築した場合は
実際に携帯端末からサイトにアクセスして正しく表示されているかを確認する。

画像をしっかり圧縮してデータを削減しているか？
色やフォントのアクセシビリティが大丈夫なのかを確認する。
（コントラストなど）

ライトハウスなどで実際にウェブサイトの品質などについて精査をおこない
結果次第では修正を行っていく。

検索エンジンの最適化を視野にいれ構築していくことも重要

### サイトの公開

ここまで来たら
公開する為にホスティングサービス等を用いてサーバを用意する。
[netify](https://www.netlify.com/)
[Vercel](https://vercel.com/)

ドメイン名を購入し、実際に世の中へ自分のサイトを公開する。

### 維持とサイトの更新

公開した後も必要に応じてサイトの更新をしていく

Google アナリティクスなどを用いて実際にウェブサイトの動向を見る
それに応じてページを更新し、また動向を見ていく
このような統計的なデータは分かりやすい数字として表れる為
今後の方針として参考になる情報である。

ブログなどでも同じことが言え
例えばまた訪れるであろうユーザーのためにもデータを常に更新していくことで
ユーザーがまた訪問してくれる確率を上げる
他にも SEO 等に良い影響を与えていくことができる