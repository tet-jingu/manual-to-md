# MELSEC iQ-R Ethernetユーザーズマニュアル(応用編) — 1.12 Webサーバ機能 (e: CGI部品概要・デバイス読出しCGI)

| 項目 | 内容 |
|---|---|
| 変換範囲 (本ファイル) | CGI部品概要(デバイス名・デバイスサイズ・デバイス値)・デバイス読出しCGI(アクセス仕様・レスポンス仕様・使用例) (原本 p.157-164 / PDFページ159-166) |
| 変換日 | 2026-09-20 |
| 変換方法 | pypdfium2(本文) + PyMuPDF目視(PDF p.160をrenderで確認。デバイスサイズ表34行の○×を直接読み取り) |
| ページ対応 | PDFページ = 原本印刷ページ + 2 |
| 関連ファイル | 前 `20_1-12a_...`〜`23_1-12d_...`、続き `25_1-12f_...` |

> このファイルは原本PDFの参照用リファレンスです。表・HTML/JavaScriptサンプルコードは
> **原文のまま全文**転記しています。
> 未変換の範囲は `00_索引_ladder_reference.md` の変換範囲表を見てください。**設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**

## 目次

- [CGI部品](#cgi部品-原本-p157)
  - [CGI部品で指定するデータ](#cgi部品で指定するデータ-原本-p157)
  - [デバイスサイズ](#デバイスサイズ-原本-p158)
  - [デバイス値](#デバイス値-原本-p158)
- [デバイス読出しCGI](#デバイス読出しcgi-原本-p159)
  - [アクセスメソッドとアクセス情報](#アクセスメソッドとアクセス情報-原本-p159)
  - [レスポンス仕様](#レスポンス仕様-原本-p160)
  - [使用例](#使用例-原本-p161-164)

---

## CGI部品 (原本 p.157)

CGI部品を使うことで，シンプルでファイルサイズの小さいユーザWebページを作成することができます。

CGIの概要については，市販の参考書籍を参照してください。

ユーザWebページでは，下記のデバイスの読み書きに限定したCGI部品が使用できます。

Webサーバに対するデータの取得や操作は，クライアントからCGIのリクエストとして渡され，その実行結果をレスポンスとしてクライアントに返すことで行われます。

| ファイル名 | 項目 | 内容 | 参照 |
|---|---|---|---|
| RdDevRnd.cgi | デバイス読出しCGI | 指定したデバイスの現在値を読み出します。 | 159ページ デバイス読出しCGI |
| WrDevRnd.cgi | デバイス書込みCGI | 指定したデバイスに指定した値を書き込みます。 | 165ページ デバイス書込みCGI |

### CGI部品で指定するデータ (原本 p.157)

CGI部品で扱うデータについて示します。

#### デバイス名

デバイス読出しCGI/デバイス書込みCGIでアクセス可能なデバイスを示します。

Un\GやJn\Xなどの\付のデバイス名を指定する時は，Un\\GやJn\\Xのように\を重ねて指定します。(\はエスケープシーケンスになっています。)

| 種別 | デバイス |
|---|---|
| ビットデバイス | X，Y，M，L，B，F，SB，V，DX，DY，SM，Jn\X，Jn\Y，Jn\B，Jn\SB，BL，BLn\S |
| ワードデバイス | T(現在値)，ST(現在値)，C(現在値)，D，W，SW，SD，Jn\W，Jn\SW，Un\G，U3En\G，U3En\HG，Z，R，ZR，RD |
| ダブルワードデバイス | LT(現在値)，LST(現在値)，LC(現在値)，LZ |

### デバイスサイズ (原本 p.158)

デバイスによって，使用可能なデバイスサイズが異なります。

デバイス番号の表記は，それぞれのデバイスに応じて10進数/16進数に分けて指定します。

凡例: ○=デバイス読出しCGI/デバイス書込みCGIの両方で使用可能，×=使用不可

| デバイス | 表記 | B: ビット | W: ワード | D: ダブルワード | Q: クワッドワード |
|---|---|---|---|---|---|
| X | 16進数 | ○ | × | × | × |
| Y | 16進数 | ○ | × | × | × |
| M | 10進数 | ○ | × | × | × |
| L | 10進数 | ○ | × | × | × |
| B | 16進数 | ○ | × | × | × |
| F | 10進数 | ○ | × | × | × |
| SB | 16進数 | ○ | × | × | × |
| V | 10進数 | ○ | × | × | × |
| DX | 16進数 | ○ | × | × | × |
| DY | 16進数 | ○ | × | × | × |
| SM | 10進数 | ○ | × | × | × |
| Jn\X | 16進数 | ○ | × | × | × |
| Jn\Y | 16進数 | ○ | × | × | × |
| Jn\B | 16進数 | ○ | × | × | × |
| Jn\SB | 16進数 | ○ | × | × | × |
| BL | 10進数 | ○ | × | × | × |
| BLn\S | 10進数 | ○ | × | × | × |
| T(現在値) | 10進数 | × | ○ | ○ | ○ |
| ST(現在値) | 10進数 | × | ○ | ○ | ○ |
| C(現在値) | 10進数 | × | ○ | ○ | ○ |
| D | 10進数 | × | ○ | ○ | ○ |
| W | 16進数 | × | ○ | ○ | ○ |
| SW | 16進数 | × | ○ | ○ | ○ |
| SD | 10進数 | × | ○ | ○ | ○ |
| Jn\W | 16進数 | × | ○ | ○ | ○ |
| Jn\SW | 16進数 | × | ○ | ○ | ○ |
| Un\G | 10進数 | × | ○ | ○ | ○ |
| U3En\G | 10進数 | × | ○ | ○ | ○ |
| U3En\HG | 10進数 | × | ○ | ○ | ○ |
| Z | 10進数 | × | ○ | ○ | ○ |
| R | 10進数 | × | ○ | ○ | ○ |
| ZR | 10進数 | × | ○ | ○ | ○ |
| RD | 10進数 | × | ○ | ○ | ○ |
| LT(現在値) | 10進数 | × | × | ○ | ○ |
| LST(現在値) | 10進数 | × | × | ○ | ○ |
| LC(現在値) | 10進数 | × | × | ○ | ○ |
| LZ | 10進数 | × | × | ○ | デバイス読出しCGIのみ |

原本の表行数(目視カウント): 34行。上表は全34行を転記。

### デバイス値 (原本 p.158)

CGI部品で扱うデバイス値の表記は下記としてください。

 - CGI部品ではデバイス値を16進数表記のString型で扱います。Webページ上で10進数または実数の値を使用する場合，JavaScriptを使用して，16進数↔10進数または実数の変換を行ってください。
 - 先頭に0xは付けません。また0補間は行いません。例えば，0x012Fという値を読出し/書込みする場合，デバイス値は12Fという文字列にします。
 - 16進数の英字の大文字/小文字は区別しません。例えば0x012Fという値を読出し/書込みする場合，12F，12fのどちらでも表記できます。

## デバイス読出しCGI (原本 p.159)

指定したデバイスの現在値を読み出します。

### アクセスメソッドとアクセス情報 (原本 p.159)

| 項目 | 内容 |
|---|---|
| アクセスメソッド | POST |
| アクセス先情報(URL) | /cgi/RdDevRnd.cgi |

#### リクエスト仕様

リクエストで使用するパラメータを示します。

リクエストデータ形式はクエリストリング形式です。DEV(n)とTYP(n)は連番で指定します。連番で指定しない場合はエラーが発生します。

##### 例: D0，M100，…，SD0のデバイス10点を読み出す場合

```
NUM=A&DEV1=D0&TYP1=D&DEV2=M100&…&DEV10=SD0&TYP10=W
```

| パラメータ名 | データ型 | 内容 | 設定範囲 |
|---|---|---|---|
| NUM | string | 読出しデバイス点数(n: 1~20)の16進数の文字列 | Webページ1ページあたりの読出し/書込みに指定するデバイス点数の合計が32点以内となるように設定します。 |
| DEV1 | string | 1点目のデバイス名 | 英数字16文字以内(大文字/小文字は区別しません。間接指定，ビット指定，桁指定，インデックス修飾はできません。) 157ページ デバイス名 |
| TYP1 | string | 1点目のデバイスサイズ | B: ビット／W: ワード／D: ダブルワード／Q: クワッドワード。158ページ デバイスサイズ |
| DEV(n) | string | n点目のデバイス名(n: 1~32) | 英数字16文字以内(大文字/小文字は区別しません。間接指定，ビット指定，桁指定，インデックス修飾はできません。) |
| TYP(n) | string | n点目のデバイスサイズ | B: ビット／W: ワード／D: ダブルワード／Q: クワッドワード |

### レスポンス仕様 (原本 p.160)

レスポンスで使用するパラメータを示します。

レスポンスデータの形式はJSON形式です。

#### 例: デバイス読出しCGIのレスポンスデータ

```json
{
 "RET" : "0",
 "DATA" : [
 "100",
 …,
 "FABC"
 ]
}
```

上記のレスポンスは，伝文上では下記の形で転送されます。

```
{"RET":"0","DATA":["100",…,"FABC"]}
```

実行結果が異常時は，RETのみになります。

```
{"RET":"4031"}
```

| パラメータ名 | データ型 | 内容 |
|---|---|---|
| RET | string | 実行結果(16進数の文字列)。0000: 正常／0001: 未ログオン／0005: 要求元(Referer)不正／4***: エラーコード(使用するCPUユニットのマニュアル) |
| DATA | string | 読出し値(配列)。16進数の文字列 |

> Point
> Webページ上にデバイス値を実数形式で表示する場合，デバイスサイズにD:ダブルワードを指定してリクエスト(1)する必要があります。また読み出したデータをJavaScriptで実数形式に変換(2)する必要があります。
> 例: D0=B36FH，D1=35A5H → DATA[0]="35a5b36f" → (2)変換後 D0 = 1.234568E-06(単精度実数)

### 使用例 (原本 p.161)

デバイス読出しCGIを使用して値を読み出す例を示します。

#### HTML例

(1) DEV1を設定 (2) TYP1を設定 (3) VAL1を設定 (4) クリックするとJavaScriptのReadDeviceRandomTbl関数をコール(引数にはテーブルidを設定)

```html
<form id="devform" name="readdev" method="post">
 <table id="devtbl" class="devtbl" border="1">
 <tr>
 <th>デバイス名</th><th>データ型</th><th>値</th>
 </tr>
 <tbody>
 <tr>
 <td><input type="text" id="DEV1" name=" DEV1" class="input"value='D10' /></td>
 <td><input type="text" id="TYP1" name=" TYP1" class="input"value='32ビット整数' /></td>
 <td><input type="text" id="VAL1" name=" VAL1" class="read-input"/></td>
 </tr>
 <tr>
 <td><input type="text" id="DEV2" name="DEV2" class="input" value='SD0'/ ></td>
 <td><input type="text" id="TYP2" name="TPY2" class="input" value='16ビット整数'/ ></td>
 <td><input type="text" id="VAL2" name="VAL2" class="read-input"/></td>
 </tr>
 <tr>
 <td><input type="text" id="DEV3" name="DEV3" class="input"value='M0'/ ></td>
 <td><input type="text" id="TYP3" name="TYP3" class="input"value='ビット'/ ></td>
 <td><input type="text" id="VAL3" name="VAL3" class="read-input"/></td>
 </tr>
 </tbody>
 </table>
 <input type="button" value="読出" class="input" onclick=" ReadDeviceRandomTbl(devtbl)"/>
 </form>
```

### JavaScript例 (原本 p.162-165)

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
 <head>
 <!-- charset の設定※Web サーバ設定がUTF-8 のためUTF-8 を設定する) -->
 <meta charset="UTF-8">
 <meta http-equiv="X-UA-Compatible" content="IE=edge"/>
 <!-- タイトル名を設定する -->
 <title>サンプル</title>
 <link href="./css/UserWebStyle.css" rel="stylesheet" media="all" />
 <!-- ライブラリJavaScript 読み込み(パスは格納位置に応じて変更する) -->
 <script src="./RUserWebLib.js"></script>
 <!-- 独自のJavaScript はこれより後に記載する -->
 <!-- ユーザのJavaScript をここに書く -->
 <script>
 // CGIリクエスト用の関数
 function ReadDeviceRandomTbl(devtblid) {
 var devtblitem = document.getElementById(devtblid);
 var i, devitem, typitem;
 var tblrows = devtblitem.rows.length;
 var param;
 // デバイス点数の設定
 param = "NUM=" + (tblrows - 1) + '&';
 for( i=1; i < tblrows; i++ ) {
 // デバイス名のパラメータ設定
 devitem = document.getElementById(devtblitem.rows[i].cells[0].childNodes[0].id);
 param += devitem.name + "=" + devitem.value + '&';
 // デバイスサイズのパラメータ設定
 typitem = document.getElementById(devtblitem.rows[i].cells[1].childNodes[0].id);
 if( "ビット" == typitem.value ) {
 param += typitem.name + "=" + 'B';
 }
 else if( "16bit 整数" == typitem.value ) {
 param += typitem.name + "=" + 'W';
 }
 else if( "32bit 整数" == typitem.value ) {
 param += typitem.name + "=" + 'D';
 }
 else {
 param += typitem.name + "=" + 'Q';
 }
 if( i < (tblrows - 1)) param += '&';
 }
 // CGIへのリクエスト要求
 xhr = new XMLHttpRequest();
 xhr.open('POST', "/cgi/RdDevRnd.cgi", true);
 xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
 var FUNC = function() { ReadDeviceRandomTbl_Response(xhr, devtblid); }; // レスポンス解析用関数の設定
 xhr.onreadystatechange = FUNC;
 xhr.send(param);
 }

 // レスポンス解析用の関数
 function ReadDeviceRandomTbl_Response(xhr, devtblid) {
 // XMLHttpRequest クライアント状態のチェック
 // 0:UNSENT 1:OPENED 2:HEADERS_RECEIVED 3:LOADING 4:DONE
 if( 4 != xhr.readyState ) {
 // ステータス4 のDONE(操作完了)以外の場合は，処理を終了する。
 return;
 }
 // HTTP レスポンスコードのチェック
 if ( 200 != xhr.status ) {
 // 「200 OK」以外の場合は，エラーのダイアログ表示をする。
 alert("HTTP STATUS ERROR=" + xhr.status );
 return;
 }
 var i, dataitem;
 var devtblitem = document.getElementById(devtblid);
 var tblrows = devtblitem.rows.length; // テーブルの行数を取得(ヘッダ含む)
 var res = JSON.parse( xhr.response ); // JSON 文字列の解析処理
 // CGI からの結果判断
 if( res.RET != "0000" ) {
 // 異常の場合エラーのダイアログを表示する。
 alert("ERROR=" + res.RET);
 }
 else {
 // 正常の場合は取得した値をテーブルに反映する。
 for ( i = 1, m = 0; i < tblrows; i++, m++) {
 dataitem = document.getElementById(devtblitem.rows[i].cells[2].childNodes[0].id);
 // ここでテーブルの値に読み出し結果を設定(16 進数文字列を数値に変換)
 dataitem.value = parseInt(res.DATA[m], 16);
 }
 alert("読出完了");
 }
 }
 </script>
</head>
```

上記の例では，リクエストパラメータは下記となります。

```
NUM=3&DEV1=D10&TYP1=D&DEV2=SD0&TPY2=W&DEV3=M0&TYP3=B
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
 <td><input type="text" id="DATA1" name="DATA1" class="read-input" ></td>
 </tr>
 <tr>
 <td><input type="text" id="DEV2" name="DEV2" class="input" value="D11"/></td>
 <td><input type="text" id="TYP2" name="TYP2" class="input" value="32bit 整数"/></td>
 <td><input type="text" id="DATA2" name="DATA2" class="read-input" /></td>
 </tr>
 <tr>
 <td><input type="text" id="DEV3" name="DEV3" class="input" value="M0"/></td>
 <td><input type="text" id="TYP3" name="TYP3" class="input" value="ビット"/></td>
 <td><input type="text" id="DATA3" name="DATA3" class="read-input" /></td>
 </tr>
 </tbody>
 </table>
 <input type="button" value="読出" class="input" onclick="ReadDeviceRandomTbl('devtbl')"/>
 </form>
 </body>
</html>
```

(5) 読出し結果を表示(res.DATAの値がparseIntで変換されテーブルのDATA1〜DATA3セルに反映される)

---

## 図・原本参照が必要な項目の一覧 (原本 p.157-164)

| 項目 | 原本ページ | 扱い |
|---|---|---|
| HTML表示例のキャプチャ(デバイス名/データ型/値の入力テーブルとボタン) | p.161, 163 | HTML/JavaScriptソースを全文転記済みのため、画面キャプチャ自体は原本参照 |

## 抜けチェック結果 (本md管理用 / 原本外)

原文(PDF p.159-166)とmdを突き合わせ、欠落なし。デバイスサイズ表の○×はテキスト抽出で欠落するため、p.160をrenderして全34行を目視確認した。HTML/JavaScriptサンプルコードは全文をそのまま転記した。
