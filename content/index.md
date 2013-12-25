/*
Title: ようこそ
Description: This description will go in the meta description tag
*/

## Picoへようこそ！

[Pico](http://pico.dev7studios.com)はとてもシンプルなデータベースフリーのCMSです。

### コンテンツを作りましょう

PicoはフラットファイルCMSです。すべてファイル＆フォルダで管理するのでデータベースを使う必要はありません。  
`.md`ファイルを"content"フォルダに作成するだけでページができます。  
例えば、このページはトップページとして`index.md`を呼び出しています。

"content"フォルダ内にさらにフォルダを作りたい場合は、`content/sub`のようにして`index.md`をその中に作成します。  
そのフォルダへはURL:`http://yousite.com/sub`のようにしてアクセスできます。  
サブフォルダに他のページを作りたい場合は、`.md`ファイルを`content/sub/page.md`のように作って置くと、URL:`http://yousite.com/sub/page`でアクセスできます。  
次にファイル構造と対応するURLを示します。

<table>
	<thead>
		<tr><th width="220">ファイルの場所</th><th>URL</th></tr>
	</thead>
	<tbody>
		<tr><td>content/index.md</td><td>/</td></tr>
		<tr><td>content/sub.md</td><td>/sub</td></tr>
		<tr><td>content/sub/index.md</td><td>/sub (same as above)</td></tr>
		<tr><td>content/sub/page.md</td><td>/sub/page</td></tr>
		<tr><td>content/a/very/long/url.md</td><td>/a/very/long/url</td></tr>
	</tbody>
</table>

ファイルが見つからない場合は`content/404.md`が表示されます。

### Text File Markup マークアップ

`.md`ファイルは[Markdown](http://daringfireball.net/projects/markdown/syntax)の書式で書きます。HTMLタグを使用することもできます。

ファイルの一番上にブロックコメントとページの属性を次のように書きます。

	/ *
	Title: ようこそ
	Description: この部分はmeta descriptionタグになります。
	Author: ジョー・ブログス
	Date: 2014/01/01
	Robots: noindex,nofollow
	*/

これらの値はテーマ内の変数`{{ meta }}`に含まれます。以下を参照。

次のようにすると`.md`ファイルで使うことが出来ます。

* <code>&#37;base_url&#37;</code> - あなたのサイトのURL

### テーマ

"themes"フォルダを編集することでテーマを作成できます。初期テーマを参考にしてください。Picoはテンプレートエンジンとして[Twig](http://twig.sensiolabs.org/documentation)を使っています。テーマの切り替えは"config.php"内の変数`$config['theme']`を変更することで可能です。

テーマのフォルダには必ず`index.html`を作りHTML構造を定義する必要があります。  
次にテーマで使えるTwig変数を示します。

* `{{ config }}` - config.phpに書いた変数 (例: `{{ config.theme }}` = "default")
* `{{ base_dir }}` - ルートディレクトリのパス
* `{{ base_url }}` - サイトのURL
* `{{ theme_dir }}` - 使用中テーマのディレクトリのパス
* `{{ theme_url }}` - 使用中テーマのディレクトリのURL
* `{{ site_title }}` - config.phpに書かれているサイトのタイトル
* `{{ meta }}` - 現在のページのmetaタグの値
	* `{{ meta.title }}`
	* `{{ meta.description }}`
	* `{{ meta.author }}`
	* `{{ meta.date }}`
	* `{{ meta.date_formatted }}`
	* `{{ meta.robots }}`
* `{{ content }}` - Markdown処理されたあとの現在のページのコンテンツ
* `{{ pages }}` - 全コンテンツのまとめ
	* `{{ page.title }}`
	* `{{ page.url }}`
	* `{{ page.author }}`
	* `{{ page.date }}`
	* `{{ page.date_formatted }}`
	* `{{ page.content }}`
	* `{{ page.excerpt }}`
* `{{ prev_page }}` - 現在ページの前のページのオブジェクト
* `{{ current_page }}` - 現在ページのオブジェクト
* `{{ next_page }}` - 現在ページの次のページのオブジェクト
* `{{ is_front_page }}` - トップページかどうかの判定

ページリストは次のようになります。

<pre>&lt;ul class=&quot;nav&quot;&gt;
	{% for page in pages %}
	&lt;li&gt;&lt;a href=&quot;{{ page.url }}&quot;&gt;{{ page.title }}&lt;/a&gt;&lt;/li&gt;
	{% endfor %}
&lt;/ul&gt;</pre>

### プラグイン

参照 [http://pico.dev7studios.com/plugins](http://pico.dev7studios.com/plugins)

### 設定

Picoの初期設定はルートディレクトリの"config.php"を編集することで上書きできます。設定を上書きする場合は"config.php"のコメントアウトを外して設定を変更してください。

### ドキュメント

詳細は [http://pico.dev7studios.com/docs](http://pico.dev7studios.com/docs) で確認できます。

