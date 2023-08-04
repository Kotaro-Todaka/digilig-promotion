# 【自主制作】デジタルハリウッドSTUDIO by LIG プロモーションLPサイト制作

## 目次
-[使用技術について](#technology-used)

## 環境情報

<h2 id="technology-used">使用技術について</h2>

### 命名規則

#### 【HTML/CSS】BEM記法
HTMLとCSSは、BEMで命名。
理由：ファイル設計はFLOCSSを採用しており、親和性があるから。

#### 【JavaScript】キャメルケース記法, 大文字アンダースコア記法, パスカル記法
JavaScriptでは、以下のような記法の使い分けをする。
・変数/関数名：キャメルケース記法
・定数名：大文字のアンダースコア記法
・クラス名：パスカル記法

### styleの設計方法
SassとFLOCSS設計手法を採用。
理由：保守性が高く機能ごとに分かれているので、何がどこに書いてあるのか分かりやすいので修正・変更しやすい。
<dl>
  <dt>foundation</dt>
  <dd>リセットCSSとhtml,body要素に設定するベースCSS</dd>
  <dt>global</dt>
  <dd>変数, @mixin, @functionなどの使いまわすテンプレ</dd>
  <dt>layout</dt>
  <dd>サイトにひとつしかない部分。クラス名の接頭辞が「l-」</dd>
  <dt>object</dt>
  <dd>
    <dl>
      <dt>component</dt>
      <dd>サイト内で繰り返し使われているパーツのスタイリング。クラス名の接頭辞は「c-」</dd>
      <dt>project</dt>
      <dd>コンテンツを構成する要素の塊。例えば、記事一覧, ユーザープロフィール, 画像ギャラリー, お問い合わせフォームなど。クラス名の接頭辞は「p-」</dd>
      <dt>utility</dt>
      <dd>一部だけ微妙に異なるスタイリングが必要なときに使う。クラス名の接頭辞は「u-」</dd>
    </dl>
  </dd>
</dl>

#### 【styleのルール】
<ol>
  <li>
    各フォルダのスタイリングは、フォルダごとに置かれた_index.scssに@useで統合する。（globalフォルダの_index.scssのみ@forward）<br>
    _index.scssにはスタイリングをしない。
  </li>
  <li>componentクラスには、width,heightなどの固有の幅や色などの特色を持たせない</li>
  <li>utilityクラスは、極力使わない</li>
</ol>

#### @useの読み込み順番
■ style.scss
```scss
@use "global";
@use "foundation";
@use "layout";
@use "object";
```

■ global内の_index.scss
```scss
@forward "variable";
@forward "color";
@forward "mixin";
@forward "function";
```

■ foundation内の_index.scss
```scss
@use "reset";
@use "base";
```

■ layout内の_index.scss
```scss
@use "footer";
@use "header";
@use "main";
```

■ object内の_index.scss
```scss
@use "component";
@use "project";
@use "utility";
```

■ component内の_index.scss
```scss
@use "button";
```

■ project内の_index.scss
```scss
@use "home";
@use "form";
```

■ utility内の_index.scss


### ディレクトリ構成
```
.
├── dist/
│   └── asset/
│       ├── css/
│       │    └── style.css
│       ├── images/
│       │   ├── about/
│       │   ├── contact/
│       │   ├── common/
│       │   ├── features/
│       │   ├── questions/
│       │   └── main-visual/
│       ├── js/ 
│       │   └── index.js/  
│       └── index.html 
├── src/
│   ├── pug/
│   │   └── index.pug
│   └── sass/
│       ├── foundation/
│       │   ├── _base.scss
│       │   ├── _index.scss
│       │   └── _reset.scss
│       ├── global/
│       │   ├── _color.scss
│       │   ├── _function.scss
│       │   ├── _index.scss
│       │   ├── _mixin.scss
│       │   └── _variable.scss
│       ├── layout/
│       │   ├── _footer.scss
│       │   ├── _header.scss
│       │   ├── _index.scss
│       │   └── _main.scss
│       ├── object/
│       │   ├── component/
│       │   ├── project/
│       │   ├── utility/
│       │   └── _index.scss    
│       └── style.scss
├── package-lock.json
├── package.json
├── postcss.config.cjs
└── READ ME.md
```
