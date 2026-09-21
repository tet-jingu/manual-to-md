# MELSEC iQ-R Ethernetユーザーズマニュアル(応用編) — 1.12 Webサーバ機能 (f: デバイス書込みCGI・エラーメッセージ)

| 項目 | 内容 |
|---|---|
| 変換範囲 (本ファイル) | デバイス書込みCGI(アクセス仕様・レスポンス仕様・使用例)・エラーメッセージ (原本 p.165-172 / PDFページ167-174) |
| 変換日 | 2026-09-20 |
| 変換方法 | pypdfium2(本文)。図・表は目立った崩れなし(コード例中心) |
| ページ対応 | PDFページ = 原本印刷ページ + 2 |
| 関連ファイル | 前 `20_1-12a_...`〜`24_1-12e_...`。本ファイルで1.12節の変換が完結する |

> このファイルは原本PDFの参照用リファレンスです。表・HTML/JavaScriptサンプルコードは
> **原文のまま全文**転記しています。
> 未変換の範囲は `00_索引_ladder_reference.md` の変換範囲表を見てください。**設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**

## 目次

- [デバイス書込みCGI](#デバイス書込みcgi-原本-p165)
  - [アクセスメソッドとアクセス情報](#アクセスメソッドとアクセス情報-原本-p165)
  - [レスポンス仕様](#レスポンス仕様-原本-p166)
  - [使用例](#使用例-原本-p167-170)
- [エラーメッセージ](#エラーメッセージ-原本-p171)
- [ユーザWebページのエラーメッセージ一覧](#ユーザwebページのエラーメッセージ一覧-原本-p172)

---

## デバイス書込みCGI (原本 p.165)

指定したデバイスに指定した値を書き込みます。

### アクセスメソッドとアクセス情報 (原本 p.165)

| 項目 | 内容 |
|---|---|
| アクセスメソッド | POST |
| アクセス先情報(URL) | /cgi/WrDev.cgi |

#### リクエスト仕様

リクエストで使用するパラメータを示します。

リクエストデータ形式はクエリストリング形式です。

##### 例: D0にFFFFHを書き込む場合

```
NUM=1&DEV1=D0&TYP1=W&DATA1=FFFF
```

> Point
> Webページ上に実数形式で入力したデバイス値を書き込む場合，入力したデータをJavaScriptで16進数の形式に変換(1)する必要があります。またデバイスサイズにはD: ダブルワードを指定してリクエスト(2)する必要があります。
> 例: D0 = 1.234568E-06(単精度実数) → (1)変換 → D0=B36FH，D1=35A5H → (2) DATA1="35a5b36f"

| パラメータ名 | データ型 | 内容 | 設定範囲 |
|---|---|---|---|
| NUM | string | 書込みデバイス点数(1) | 1を設定します。(Webページ1ページあたりの読出し/書込みに指定するデバイス点数の合計が32点以内となるようにしてください。) |
| DEV1 | string | デバイス名 | 英数字16文字以内(大文字/小文字は区別しません。間接指定，ビット指定，桁指定，インデックス修飾はできません。) 157ページ デバイス名 |
| TYP1 | string | デバイスサイズ | B: ビット／W: ワード／D: ダブルワード／Q: クワッドワード。158ページ デバイスサイズ |
| DATA1 | string | 書込み値 | 16進数の文字列 |

### レスポンス仕様 (原本 p.166)

レスポンスで使用するパラメータを示します。

レスポンスデータの形式はJSON形式です。

#### 例: デバイス書込みCGIのレスポンスデータ

```json
{
 "RET" : "0",
 "DATA" : [
 "100"
 ]
}
```

上記のレスポンスは，伝文上では下記の形で転送されます。

```
{"RET":"0","DATA":["100"]}
```

実行結果が異常時は，データを書き込まず，RETのみになります。

```
{"RET":"4031"}
```

| パラメータ名 | データ型 | 内容 |
|---|---|---|
| RET | string | 実行結果(16進数の文字列)。0000: 正常／0001: 未ログオン／0002: 権限なし(デバイス書込み許可権限がないユーザがCGI実行)／0005: 要求元(Referer)不正／4***: エラーコード(使用するCPUユニットのマニュアル) |
| DATA | string | 書き込んだデバイスの読出し値(配列)。16進数の文字列 |

### 使用例 (原本 p.167)

デバイス書込みCGIを使用して値を書き込む例を示します。

#### HTML例

(1) DEV1を設定 (2) TYP1を設定 (3) VAL1を設定 (4) クリックするとJavaScriptのWriteDeviceBlockTbl関数をコール(引数にはテーブルid，書込み開始行番号，書込み点数1を設定)

```html
<form id="devform" name="readdev" method="post">
 <table id="devtbl" class="devtbl" border="1">
 <tr>
 <th>デバイス名</th><th>データ型</th><th>値</th>
 </tr>
 <tbody>
 <tr>
 <td><input type="text" id="DEV1" name=" DEV1" class="input"value='D10'/ ></td>
 <td><input type="text" id="TYP1" name=" TYP1" class="input"value='32bit整数'/ ></td>
 <td><input type="text" id="DATA1" name=" DATA1" class="input"value='3'/></td>
 </tbody>
 </table>
 <input type="button" value="書込" class="input" onclick=" WriteDeviceBlockTbl(devtbl,1,1)"/>
</form>
```

### JavaScript例 (原本 p.168-172)

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
 <head>
 <!-- charset の設定※Web サーバ設定がUTF-8 のためUTF-8 を設定する) -->
 <meta charset="UTF-8">
 <meta http-equiv="X-UA-Compatible" content="IE=edge"/>
 <!-- タイトル名を設定する -->
 <title>デバイス書込みCGI サンプル</title>
 <link href="./css/UserWebStyle.css" rel="stylesheet" media="all" />
 <!-- ライブラリJavaScript 読み込み(パスは格納位置に応じて変更する) -->
 <script src="./RUserWebLib.js"></script>
 <!-- 独自のJavaScript はこれより後に記載する -->
 <!-- ユーザのJavaScript をここに書く -->
 <script>
 function WriteDeviceBlockTbl(devtblid, row) {
 var dataitem;
 var xhr;
 var devtblitem = document.getElementById(devtblid);
 // デバイス点数の設定(1 点固定)
 var param = 'NUM=1&';
 // デバイス名のパラメータ設定
 var devitem = document.getElementById(devtblitem.rows[row].cells[0].childNodes[0].id);
 param += 'DEV1=' + devitem.value + '&';
 // デバイスサイズのパラメータ設定
 var typitem = document.getElementById(devtblitem.rows[row].cells[1].childNodes[0].id);
 if( 'ビット' == typitem.value ) {
 param += 'TYP1=' + 'B';
 }
 else if( '16bit 整数' == typitem.value) {
 param += 'TYP1=' + 'W';
 }
 else if( '32bit 整数' == typitem.value) {
 param += 'TYP1=' + 'D';
 }
 else {
 param += 'TYP1=' + 'Q';
 }
 param += '&';
 // データのパラメータ設定
 var dataitem = document.getElementById(devtblitem.rows[row].cells[2].childNodes[0].id);
 param += 'DATA1=' + parseInt(dataitem.value).toString(16)
 // CGIへのリクエスト要求
 xhr = new XMLHttpRequest();
 xhr.open('POST', "/cgi/WrDev.cgi", true);
 xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
 var FUNC = function() { WriteDeviceBlockTbl_Response(xhr, typitem, dataitem); }; // レスポンス解析用関数の設定
 xhr.onreadystatechange = FUNC;
 xhr.send(param);
 }

 // レスポンス解析用の関数
 function WriteDeviceBlockTbl_Response(xhr, typitem, dataitem) {
 // XMLHttpRequestクライアント状態のチェック
 // 0:UNSENT 1:OPENED 2:HEADERS_RECEIVED 3:LOADING 4:DONE
 if( 4 != xhr.readyState ) {
 // ステータス4 のDONE(操作完了)以外の場合は，処理を終了する。
 return;
 }
 // HTTPレスポンスコードのチェック
 if ( 200 != xhr.status ) {
 // 「200 OK」以外の場合は，エラーのダイアログ表示をする。
 alert("HTTP STATUS ERROR=" + xhr.status );
 return;
 }
 var value;
 var res = JSON.parse( xhr.response ); // JSON 文字列の解析処理
 // CGI からの結果判断
 if( res.RET != "0000" ) {
 // 異常の場合エラーのダイアログを表示する。
 alert("ERROR=" + res.RET);
 }
 else {
 // 正常の場合は，書込み結果値の値を反映する。
 dataitem.value = parseInt(res.DATA[0],16);
 alert("書込完了");
 }
 }
 </script>
 </head>
```

上記の例では，リクエストパラメータは下記となります。

```
NUM=1&DEV1=D10&TYP1=D&DATA1=3
```

```html
<body>
 <form>
 <table id="devtbl" class="devtbl" border="1">
 <tr>
 <th>デバイス名</th>
 <th>データ型</th>
 <th>値</th>
 </tr>
 <tbody>
 <tr>
 <td><input type="text" id="DEV1" name="DEV1" class="input" value="D10"/></td>
 <td><input type="text" id="TYP1" name="TYP1" class="input" value="16bit 整数"/></td>
 <td><input type="text" id="DATA1" name="DATA1" class="input" value="3"/></td>
 <td><input type="button" value=" 書込" class="input" onclick="WriteDeviceBlockTbl('devtbl',1)"/></td>
 </tr>
 <tr>
 <td><input type="text" id="DEV2" name="DEV2" class="input" value="D11"/></td>
 <td><input type="text" id="TYP2" name="TYP2" class="input" value="32bit 整数"/></td>
 <td><input type="text" id="DATA2" name="DATA2" class="input" value="10"/></td>
 <td><input type="button" value=" 書込" class="input" onclick="WriteDeviceBlockTbl('devtbl',2)"/></td>
 </tr>
 <tr>
 <td><input type="text" id="DEV3" name="DEV3" class="input" value="M0"/></td>
 <td><input type="text" id="TYP3" name="TYP3" class="input" value="ビット"/></td>
 <td><input type="text" id="DATA3" name="DATA3" class="input" value="1"/></td>
 <td><input type="button" value=" 書込" class="input" onclick="WriteDeviceBlockTbl('devtbl',3)"/></td>
 </tr>
 </tbody>
 </table>
 </form>
 </body>
</html>
```

## エラーメッセージ (原本 p.171)

ユーザWebページの部品を誤って使用した場合，ユーザWebページを表示した際に異常を知らせるボタンが該当部品の左上に表示されます。部品に限定されない共通処理に関するエラーメッセージは，画面の左上に表示されます。

エラーの詳細は，ボタンをクリックすると表示されます。

## ユーザWebページのエラーメッセージ一覧 (原本 p.172)

ユーザWebページのエラーメッセージと原因，対処は下記です。

上記以外のエラーについては，下記を参照してください。

MELSEC iQ-R/MELSEC iQ-F Webサーバ機能ガイドブック

使用するCPUユニットのマニュアル

| 内容 | 原因 | 対処 |
|---|---|---|
| 設定必須のパラメータ"XXX"が設定されていません。 | 設定必須のパラメータを設定していない。 | HTMLファイルの内容を確認する。 |
| パラメータ"XXX"の設定内容が間違っています。 | パラメータが設定範囲外である。数値で指定されるべきパラメータの設定値が数値でない。 | デバイス"XXX"のデータ形式が不正です。デバイスの進数，データ形式，デバイス名を確認する。 |
| 受信データが異常です。 | 受信データに異常がある。 | CPUユニットとクライアント端末とが正しく接続されていることを確認し，Webページの更新を行う。 |
| ログオフされています。ログオンして再度実行してください。 | ログオフされている(通信が切断されている)。 | CPUユニットと端末とが正しく接続されていることを確認し，再度ログオンする。 |
| デバイスが不適切です。下記の原因が考えられます。・ポインタ，定数などのデバイス・未サポートのデバイス | デバイス名が不正である。 | デバイス名の指定に誤りがないか，部品のパラメータを確認する。 |
| デバイスNoが不適切です。下記の原因が考えられます。・デバイス設定のデバイス範囲を超えているデバイス | デバイス番号，バッファメモリアドレスが数値でない，または範囲外である。デバイス範囲不正。 | デバイス番号，バッファメモリアドレスの指定に誤りがないか，部品のパラメータを確認する。 |
| 指定されたユニットは存在しません。ユニットを確認してください。 | ユニット番号に誤りがある。インテリジェント機能ユニットとの交信で異常が発生した。 | ユニット番号の指定に誤りがないか，部品のパラメータを確認する。増設ユニットで電源断や異常が発生していないことを確認する。 |

原本の表行数(目視カウント): 7行。上表は全7行を転記。

---

## 図・原本参照が必要な項目の一覧 (原本 p.165-172)

| 項目 | 原本ページ | 扱い |
|---|---|---|
| HTML表示例のキャプチャ(デバイス名/データ型/値の入力テーブルと書込ボタン) | p.167 | HTML/JavaScriptソースを全文転記済みのため、画面キャプチャ自体は原本参照 |
| エラーメッセージ表示例のキャプチャ | p.171 | 表示位置・挙動を文章化済み(上記参照)。画面例自体は原本参照 |

## 抜けチェック結果 (本md管理用 / 原本外)

原文(PDF p.167-174)とmdを突き合わせ、欠落なし。これで1.12 Webサーバ機能の変換が完結する(00_索引の変換範囲表を更新)。
