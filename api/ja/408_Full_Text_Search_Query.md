# 全文検索(q) クエリ
### 概要
一覧取得時に全文検索キーワードを指定する場合は全文検索(q)クエリを使用する  
コンプレックスタイプのデータを含めて、全ての値が検索対象


※クエリを指定する際はURLエンコードが必要  
※\__updated, \_publishedの値を指定する場合は、UNIX時間（"/Date()"の括弧内の数字）で指定  
※\_metadata内の項目は検索対象外
### リクエストクエリ
```
q={SearchKeyword}
```
|項目<br>|概要<br>|有効値<br>|備考<br>|
|:--|:--|:--|:--|
|{SearchKeyword}<br>|検索文字列を指定する<br>|桁数：1&#65374;255 byte<br>| <br>|

### 検索対象となる型
検索対象となるデータ型を以下に示す

|データ型<br>|検索対象<br>|備考<br>|
|:--|:--|:--|
|Edm.String<br>|○<br>| <br>|
|Edm.Boolean<br>|○<br>| <br>|
|Edm.Single<br>|○<br>| <br>|
|Edm.Int32<br>|○<br>| <br>|
|Edm.Double<br>|○<br>|動的プロパティのみ<br>|
|Edm.DateTime<br>|×<br>| <br>|
### 検索の仕様
* 半角空白
	- 区切り文字として扱う
	- "(ダブルコート)で囲んでも、一単語として扱われない
	- 例) 以下の指定はどちらも 「ぽち」かつ「たま」というキーワードを含むデータを検索する
```
q=ぽち%20たま
q="ぽち%20たま"
```
* 半角英数字
	- キーワード内での部分一致の検索不可
	- 大文字・小文字の区別は行わない
* 全角文字
	- 部分一致の検索可
	- 大文字・小文字の区別は行わない

### CURLサンプル
例：セル一覧を取得時、sampleというキーワードと一致するセルを取得する場合:
```sh
curl "https://{UnitFQDN}/__ctl/Cell?q=sample" -X GET -i -H 'Authorization: Bearer {UnitUserToken}' -H 'Accept: application/json'
```
<br>
<br>
<br>

###### Copyright 2017    FUJITSU LIMITED