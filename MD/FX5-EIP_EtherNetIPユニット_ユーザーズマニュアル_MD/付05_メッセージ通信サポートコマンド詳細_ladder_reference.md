# 三菱 MELSEC iQ-F FX5-EIP形 EtherNet/IPユニット ユーザーズマニュアル 付録5 メッセージ通信サポートコマンド詳細

| 項目 | 内容 |
|---|---|
| 原本 | 三菱電機 MELSEC iQ-F FX5-EIP形EtherNet/IPユニットユーザーズマニュアル |
| 発行元 | 三菱電機株式会社 |
| 資料番号 / 版数 | SH-082708 / B版（PDFメタデータ subject: SH-082708-B） |
| 原本PDF | `PDF/MELSEC iQ-F FX5-EIP形EtherNet_IPユニットユーザーズマニュアル.pdf` (全274ページ) |
| 本ファイルの範囲 | 付5 メッセージ通信サポートコマンド詳細 (印刷 p.250-261 / PDF p.252-263) |
| ページ対応 | 「原本 p.」はPDFのページ番号、「印刷 p.」は原本フッタのページ番号。印刷ページ = PDFページ − 2。本文中の「〇〇ページ参照」は印刷ページ |
| 変換日 | 2026-10-23 |
| 変換方法 | pypdfium2(本文) + PyMuPDF 200dpi 画像の目視(全ページ) |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。

**転記上の扱い**: 原本の結合セルは各行に値を展開。セル内改行は `<br>`。アトリビュート表で名称が階層（例: Revision の下に Major Revision / Minor Revision）になっている箇所は、名称列を `上位名称 / 下位名称` の形で1列にまとめた。アクセス欄の ○/× は原本の記号のまま。参照欄の「☞」記号は「（☞ 〇〇ページ）」と表記。図は【図】プレースホルダ＋読み取れる事実の箇条書き。本範囲にプログラム例・ラダー図はない。見出しレベル: 付録章 `##` / 節（原本の大見出し・帯見出し） `###` / 項 `####` / ■ `######`。

---

## 主要用語 対訳表 (Glossary) (付5 / 原本 p.252-263)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| オブジェクト | Object | クラスID | 参考訳 |
| インスタンス | Instance | インスタンスID | 参考訳 |
| アトリビュート | Attribute | アトリビュートID | 参考訳 |
| サービス | Service | サービスコード | 参考訳 |
| クラスアトリビュート | Class attribute | インスタンスID: 00H | 参考訳 |
| クラスサービス | Class service | — | 参考訳 |
| インスタンスアトリビュート | Instance attribute | インスタンスID: 01H | 参考訳 |
| インスタンスサービス | Instance service | — | 参考訳 |
| メッセージ通信サポートコマンド | Message communication support command | — | 参考訳 |
| データタイプ | Data type | — | 参考訳 |
| 設定値(Set)/格納値(Get) | Set value / Stored value (Get) | Set / Get | 参考訳 |
| 製品ステータス | Status (product status) | Identity Attr.5 | 参考訳 |
| 製品名称 | Product Name | Identity Attr.7 | 参考訳 |
| ベンダの識別番号 | Vendor Id | Identity Attr.1 | 参考訳 |
| シリアル番号 | Serial Number | Identity Attr.6 | 参考訳 |
| 軽度異常 | Minor Recoverable Fault | Status bit 8 | 参考訳 |
| 中度異常 | Major Recoverable Fault | Status bit 10 | 参考訳 |
| 重度異常 | Major Unrecoverable Fault | Status bit 11 | 参考訳 |
| サイクリック通信 | Cyclic communication | — | 参考訳 |
| インタフェースステータス | Status (interface status) | TCP/IP Interface Attr.1 | 参考訳 |
| インタフェース能力フラグ | Configuration Capability | TCP/IP Interface Attr.2 | 参考訳 |
| インタフェース制御フラグ | Configuration Control | TCP/IP Interface Attr.3 | 参考訳 |
| 物理リンクオブジェクト | Physical Link Object | TCP/IP Interface Attr.4 | 参考訳 |
| アドレス重複検知 | Address Conflict Detection | ACD | 参考訳 |
| 不揮発性メモリ | Non-volatile memory | — | 参考訳 |
| インタフェースのステータスフラグ / インタフェースステータスフラグ | Interface Flags | Ethernet Link Attr.2 | 参考訳 |
| MAC層アドレス | Physical Address (MAC address) | Ethernet Link Attr.3 | 参考訳 |
| オートネゴシエーション | Auto-negotiation | — | 参考訳 |
| 全二重 / 半二重 | Full duplex / Half duplex | — | 参考訳 |
| リンクアップ / リンクダウン | Link up / Link down | — | 参考訳 |
| コリジョン | Collision | — | 参考訳 |
| ブロードキャスト / マルチキャスト / ユニキャスト | Broadcast / Multicast / Unicast | — | 参考訳 |
| コネクションタイムアウト | Connection Timeouts | Connection Manager Attr.8 | 参考訳 |
| 相手機器 | Partner device | — | 参考訳 |
| ターゲット機器 | Target device | — | 参考訳 |
| UCMM | Unconnected Message Manager | — | 参考訳 |
| CIP | Common Industrial Protocol | — | 参考訳 |

## 変換範囲表 (付5 / 原本 p.252-263)

| 原本ページ | 節 | 扱い |
|---|---|---|
| p.252 | 付5 冒頭、用語説明 | 全文 |
| p.253 | サービスの実行、オブジェクト一覧 | 全文 |
| p.254 | 各コマンドの説明（アクセス、データタイプ、設定値(Set)/格納値(Get)） | 全文 |
| p.255-256 | Identity（クラスID 01H） | 全文 |
| p.257 | Message Router（クラスID 02H） | 全文 |
| p.258 | Connection Manager（クラスID 06H） | 全文 |
| p.259-260 | TCP/IP Interface（クラスID F5H） | 全文 |
| p.261-263 | Ethernet Link（クラスID F6H） | 全文 |
| 上記以外 | 他章・他付録 | 同フォルダの他ファイル参照 |

## 目次 (付5)

- 付5 メッセージ通信サポートコマンド詳細 (付5 / 印刷 p.250 / 原本 p.252)
  - 用語説明 (印刷 p.250 / 原本 p.252)
  - サービスの実行 (印刷 p.251 / 原本 p.253)
  - オブジェクト一覧 (印刷 p.251 / 原本 p.253)
  - 各コマンドの説明 (印刷 p.252 / 原本 p.254)
  - Identity (印刷 p.253-254 / 原本 p.255-256)
  - Message Router (印刷 p.255 / 原本 p.257)
  - Connection Manager (印刷 p.256 / 原本 p.258)
  - TCP/IP Interface (印刷 p.257-258 / 原本 p.259-260)
  - Ethernet Link (印刷 p.259-261 / 原本 p.261-263)

## 付5 メッセージ通信サポートコマンド詳細 (付5 / 印刷 p.250 / 原本 p.252)

Class3インスタンス通信およびUCMMインスタンス通信で使用するコマンドを示します。
EtherNet/IP機器にはオブジェクト(機能やデータを抽象的に表現したもの)と，それに対応するサービス(要求によって実行する動作または機能)が用意されています。

### 用語説明 (付5 / 印刷 p.250 / 原本 p.252)

| 用語 | 説明 |
|---|---|
| オブジェクト | クラスIDによってEtherNet/IP機器内でそれぞれ管理されています。<br>オブジェクトはインスタンスを1つ以上持っています。 |
| インスタンス | インスタンスIDによってオブジェクト内でそれぞれ管理されています。<br>インスタンスは内部にアトリビュートと呼ばれる情報を1つ以上持っています。<br>また，インスタンスは実行可能なサービスを1つ以上持っており，サービスコードによってそれぞれのサービスが使用できます。<br>利用可能なサービスはインスタンスごとに決められています。 |
| アトリビュート | アトリビュートIDによってインスタンス内でそれぞれ管理されています。 |

下記にオブジェクト，インスタンス，アトリビュートの関係を示します。

【図】オブジェクト・インスタンス・アトリビュートの関係（原本 p.252）
- オブジェクト(クラスID: 01H) の中に インスタンス(ID: 01) と インスタンス(ID: 02) がある
- 各インスタンスの中に アトリビュート(ID: 01H)、アトリビュート(ID: 02H) …… が並ぶ
- オブジェクト(クラスID: 02H) も同じ構成（インスタンス(ID: 01)/(ID: 02)、各々にアトリビュート(ID: 01H)/(ID: 02H) ……）

### サービスの実行 (付5 / 印刷 p.251 / 原本 p.253)

サービスを実行するには，クラスID，インスタンスID，アトリビュートIDを用いて対象を指定します。(一部のサービスではアトリビュートIDの指定が不要な場合があります)
下記にメッセージ通信サポートコマンドを使用してサービスを実行する流れを示します。

**例**

下記のサービス（Get_Attribute_Single）を指定して，相手機器からFX5-EIPにアトリビュートの読出しを要求した場合

| 項目 | 内容 |
|---|---|
| クラスID | 0XH |
| インスタンスID | 01H |
| アトリビュートID | 02H |
| サービスコード | 0EH |

【図】メッセージ通信サポートコマンドによるサービス実行の流れ（原本 p.253）
- 相手機器 → FX5-EIP へ「要求」、FX5-EIP → 相手機器へ「応答」
- FX5-EIP 内に オブジェクト(クラスID: 0XH)、オブジェクト(クラスID: 0YH)（インスタンス(ID: 3000)、インスタンス(ID: 3001) …）、オブジェクト(クラスID: 0ZH)（インスタンス(ID: 01)、インスタンス(ID: 02) …）がある
- オブジェクト(クラスID: 0XH) の インスタンス(ID: 01) は「アトリビュート一覧」（アトリビュート(ID: 01H)、アトリビュート(ID: 02H) …）と「実行可能なサービス」（サービスコード: 0EH アトリビュートの値を返却、サービスコード: 10H アトリビュートに値を設定 …）を持つ。インスタンス(ID: 02) も存在
- 図中の(1)～(5)は下記の手順に対応

(1) クラスIDの0XHにアクセス
(2) インスタンスIDの01Hにアクセス
(3) アトリビュートIDの02Hを指定
(4) サービスコードの0EHを実行
(5) (3)で指定したアトリビュートの値が返されます。

### オブジェクト一覧 (付5 / 印刷 p.251 / 原本 p.253)

メッセージ通信サポートコマンドで使用できるオブジェクトは下記になります。

| オブジェクト名 | 内容 | 参照 |
|---|---|---|
| Identity | FX5-EIPの識別情報などを持つオブジェクトです。 | 253ページ |
| Message Router | FX5-EIPのクラスの情報などを持つオブジェクトです。 | 255ページ |
| Connection Manager | FX5-EIPとコネクションを確立する際に使用するオブジェクトです。 | 256ページ |
| TCP/IP Interface | TCP/IPに関する設定や状態を持つオブジェクトです。 | 257ページ |
| Ethernet Link | Ethernet通信の設定や状態を持つオブジェクトです。 | 259ページ |

### 各コマンドの説明 (付5 / 印刷 p.252 / 原本 p.254)

オブジェクトの各項目は下記になります。

| 項目 | 内容 |
|---|---|
| クラスアトリビュート | オブジェクトのクラスが持つデータです。*1<br>同一ʼクラスʼ内のすべてのオブジェクトにより共有されるアトリビュートです。インスタンスIDにʼ0ʼを設定することで指定されます。 |
| クラスサービス | クラスを指定して行うサービスです。*1 |
| インスタンスアトリビュート | オブジェクトのインスタンスが持つデータです。*2 |
| インスタンスサービス | インスタンスを指定して行うサービスです。*2 |

*1 クラスは，オブジェクトのリビジョンやインスタンスなど基本的な情報を持っています。
*2 インスタンスは，機能やデータなどオブジェクトごとの情報を持っています。

###### ■クラスアトリビュート/インスタンスアトリビュートの各項目 (付5 / 印刷 p.252 / 原本 p.254)

クラスアトリビュート/インスタンスアトリビュートの各項目は下記になります。

- アクセス

インスタンスサービスを使用した読出しおよび書込みの可否を示します。

| 項目 | 内容 |
|---|---|
| Get | Get_Attribute_Singleなどでの読出しが可能です。 |
| Set | Set_Attribute_Singleでの書込みが可能です。 |

- データタイプ

クラス/インスタンスのデータタイプを示します。FX5-EIPで対応しているデータタイプ(CIP仕様で規定)は下記です。

| 項目 | 内容 | データサイズ | 範囲 |
|---|---|---|---|
| BOOL | ビットデータ | 1バイト | 0: OFF(False)<br>1: ON(True) |
| SINT | 符号あり8ビットデータ | 1バイト | -128~+127 |
| INT | 符号あり16ビットデータ | 2バイト | -32768~+32767 |
| DINT | 符号あり32ビットデータ | 4バイト | -2147483648~+2147483647 |
| USINT | 符号なし8ビットデータ | 1バイト | 0~255 |
| UINT | 符号なし16ビットデータ | 2バイト | 0~65535 |
| UDINT | 符号なし32ビットデータ | 4バイト | 0~4294967295 |
| ULINT | 符号なし64ビットデータ | 8バイト | 0~18446744073709551615 |
| REAL | 単精度浮動小数点型実数 | 4バイト | E±1.17549435-38~E±3.40282347+38 |
| LREAL | 倍精度浮動小数点型実数 | 8バイト | E±2.2250738585072014-308~E±1.7976931348623157+308 |
| STRING | 文字列データ | 文字数により可変 | — |
| SHORT_STRING | 文字列のサイズ+文字列データ*1 | 文字数により可変<br>文字数+1byte | — |
| BYTE | ビット列(8ビット) | 1バイト | — |
| WORD | ビット列(16ビット) | 2バイト | — |
| DWORD | ビット列(32ビット) | 4バイト | — |
| Padded EPATH | CIPパスセグメント | 4バイト | — |

*1 文字列の先頭に，取得した文字列のサイズがUSINT型1バイトで設定されます。

- 設定値(Set)/格納値(Get)

アクセスの内容により，下記のように値の示す内容が変わります。

| 項目 | 内容 |
|---|---|
| Getに対応 | 設定値(Set)/格納値(Get)がFX5-EIPから読み出せます。 |
| Setに対応 | 設定値(Set)/格納値(Get)がFX5-EIPに設定できます。 |

### Identity (付5 / 印刷 p.253 / 原本 p.255)

| オブジェクト名 | クラスID |
|---|---|
| Identity | 01H |

#### クラスアトリビュート(インスタンスID: 00H) (付5 / 印刷 p.253 / 原本 p.255)

○: 対応，×: 非対応

| アトリビュートID | アクセス Get | アクセス Set | 名称 | データタイプ | 内容 | 設定値(Set)/格納値(Get) |
|---|---|---|---|---|---|---|
| 1 | ○ | × | Revision | UINT | オブジェクトのリビジョン | 0002H |
| 2 | ○ | × | Max Instance | UINT | 最大インスタンスID | 0001H |
| 3 | ○ | × | Number of instances | UINT | 生成されているインスタンス数 | 0001H |

#### クラスサービス (付5 / 印刷 p.253 / 原本 p.255)

| サービスコード | サービス | 備考 |
|---|---|---|
| 01H | Get_Attributes_All | クラスアトリビュートに対して本サービスを実施する場合，下記の値が返却されます。<br>• アトリビュートID1: アトリビュートID1の値<br>• アトリビュートID2: アトリビュートID2の値<br>• アトリビュートID6: 0000H<br>• アトリビュートID7: 0000H |
| 0EH | Get_Attribute_Single | — |

#### インスタンスアトリビュート(インスタンスID: 01H) (付5 / 印刷 p.253 / 原本 p.255)

○: 対応，×: 非対応

| アトリビュートID | アクセス Get | アクセス Set | 名称 | データタイプ | 内容 | 設定値(Set)/格納値(Get) |
|---|---|---|---|---|---|---|
| 1 | ○ | × | Vendor Id | UINT | ベンダの識別番号 | 00A1H |
| 2 | ○ | × | Device Type | UINT | デバイスタイプ | 000CH |
| 3 | ○ | × | Product Code | UINT | 製品の識別番号 | 000DH |
| 4 | ○ | × | Revision / Major Revision | USINT | メジャーリビジョン | 01H |
| 4 | ○ | × | Revision / Minor Revision | USINT | マイナーリビジョン | 01H |
| 5 | ○ | × | Status | WORD | 製品ステータス | （☞ 254ページ） |
| 6 | ○ | × | Serial Number | UDINT | シリアル番号 | ユニットごとに<br>異なります。 |
| 7 | ○ | × | Product Name | SHORT_STRING | 製品名称 | ”FX5-EIP”*1 |

*1 SHORT_STRING型のため，文字列の先頭に製品名称の文字数が付与されます。

###### ■製品ステータス詳細 (付5 / 印刷 p.254 / 原本 p.256)

| ビット | 内容 | 値 |
|---|---|---|
| 0 | Owned | 文中の“コネクション”はExclusive Ownerのコネクションを指します(Input Only，Listen Onlyではビットは変化しない)。<br>• 0: ターゲット機器としてEtherNet/IP通信が接続されていない<br>• 1: ターゲット機器として1コネクションでもEtherNet/IP通信が接続されている |
| 1 | 予約 | 0固定 |
| 2 | Configured | 1固定 |
| 3 | 予約 | 0固定 |
| 4~7 | Extended Device Status | 文中の“コネクション”はExclusive Ownerのコネクションを指します(Input Only，Listen Onlyではビットは変化しない)。<br>• 0010(2H): 1つ以上のコネクションでエラーが発生している状態<br>• 0011(3H): コネクションが1つも確立されていない状態<br>• 0101(5H): Major Fault発生状態(ビット10またはビット11がONしている)<br>• 0110(6H): 1つ以上のコネクションがRUNモードで正常に通信している状態<br>• 0111(7H): 1つ以上のコネクションが全てIDLEモードで通信している状態 |
| 8 | Minor Recoverable Fault | • 0: エラーなし<br>• 1: 軽度異常が発生 |
| 9 | Minor Unrecoverable Fault | 0 固定 |
| 10 | Major Recoverable Fault | • 0: エラーなし<br>• 1: 中度異常が発生 |
| 11 | Major Unrecoverable Fault | • 0: エラーなし<br>• 1: 重度異常が発生 |
| 12~15 | Extended Device Status 2 | 0 固定 |

#### インスタンスサービス (付5 / 印刷 p.254 / 原本 p.256)

| サービスコード | サービス | （見出しなし） |
|---|---|---|
| 01H | Get_Attributes_All | — |
| 05H | Reset | サイクリック通信停止中に本サービスを受信した場合，正常応答を返して下記の動作を実行します。<br>• EtherNet/IP通信停止<br>• LEDテスト(ユニット起動時と同じ)<br>• EtherNet/IP通信起動<br>サイクリック通信中に本サービスを受信した場合はエラー応答を返します。 |
| 0EH | Get_Attribute_Single | — |

※原本の表の3列目は見出しが空欄。

### Message Router (付5 / 印刷 p.255 / 原本 p.257)

| オブジェクト名 | クラスID |
|---|---|
| Message Router | 02H |

#### クラスアトリビュート(インスタンスID: 00H) (付5 / 印刷 p.255 / 原本 p.257)

○: 対応，×: 非対応

| アトリビュートID | アクセス Get | アクセス Set | 名称 | データタイプ | 内容 | 設定値(Set)/格納値(Get) |
|---|---|---|---|---|---|---|
| 1 | ○ | × | Revision | UINT | オブジェクトのリビジョン | 0001H |
| 2 | ○ | × | Max Instance | UINT | 最大インスタンスID | 0001H |
| 3 | ○ | × | Number of instances | UINT | 生成されているインスタンス数 | 0001H |
| 6 | ○ | × | Maximum ID Number Class Attributes | UINT | クラスアトリビュートのアトリビュートID番号 | 0007H |
| 7 | ○ | × | Maximum ID Number Instance Attributes | UINT | インスタンスアトリビュートのアトリビュートID番号 | 0002H |

#### クラスサービス (付5 / 印刷 p.255 / 原本 p.257)

| サービスコード | サービス | 備考 |
|---|---|---|
| 0EH | Get_Attribute_Single | — |

#### インスタンスアトリビュート(インスタンスID: 01H) (付5 / 印刷 p.255 / 原本 p.257)

アクセス(○: 対応，×: 非対応)

| アトリビュートID | アクセス Get | アクセス Set | 名称 | データタイプ | 内容 | 設定値(Set)/格納値(Get) |
|---|---|---|---|---|---|---|
| 1 | ○ | × | Object List / Number | UINT | クラス配列内にサポートされているクラスの数 | 0008H |
| 1 | ○ | × | Object List / Classes | USINT型配列[8] | サポートされているクラスコード(クラスID)のリスト | • 0: 0001H<br>• 1: 0002H<br>• 2: 0004H<br>• 3: 0006H<br>• 4: 00F5H<br>• 5: 00F6H<br>• 6: 0109H<br>• 7: 010AH |
| 2 | ○ | × | NumberAvailable | UINT | サポートするコネクションの最大数 | 0080H |

#### インスタンスサービス (付5 / 印刷 p.255 / 原本 p.257)

| サービスコード | サービス |
|---|---|
| 0EH | Get_Attribute_Single |

### Connection Manager (付5 / 印刷 p.256 / 原本 p.258)

| オブジェクト名 | クラスID |
|---|---|
| Connection Manager | 06H |

#### クラスアトリビュート(インスタンスID: 00H) (付5 / 印刷 p.256 / 原本 p.258)

○: 対応，×: 非対応

| アトリビュートID | アクセス Get | アクセス Set | 名称 | データタイプ | 内容 | 設定値(Set)/格納値(Get) |
|---|---|---|---|---|---|---|
| 1 | ○ | × | Revision | UINT | オブジェクトのリビジョン | 0001H |
| 2 | ○ | × | Max Instance | UINT | 最大インスタンスID | 0001H |
| 3 | ○ | × | Number of instances | UINT | 生成されているインスタンス数 | 0001H |

#### クラスサービス (付5 / 印刷 p.256 / 原本 p.258)

| サービスコード | サービス | 備考 |
|---|---|---|
| 01H | Get_Attributes_All | バイト4~7については，00Hが格納されます。 |
| 0EH | Get_Attribute_Single | — |

#### インスタンスアトリビュート(インスタンスID: 01H) (付5 / 印刷 p.256 / 原本 p.258)

○: 対応，×: 非対応

| アトリビュートID | アクセス Get | アクセス Set | 名称 | データタイプ | 内容 | 設定値(Set)/格納値(Get) |
|---|---|---|---|---|---|---|
| 1 | ○ | × | Open Requests | UINT | 受信したForward_Openの数 | 左記の値 |
| 2 | ○ | × | Open Format Rejects | UINT | フォーマット不適合のため拒否されたForward_Openの数 | 左記の値 |
| 3 | ○ | × | Open Resource Rejects | UINT | リソース不足のため拒否されたForward_Openの数 | 左記の値 |
| 4 | ○ | × | Open Other Rejects | UINT | フォーマット不適合やリソース不足以外の理由で拒否されたForward_Openの数 | 左記の値 |
| 5 | ○ | × | Close Requests | UINT | 受信したForward_Closeの数 | 左記の値 |
| 6 | ○ | × | Close Format Requests | UINT | フォーマット不適合のため拒否されたForward_Closeの数 | 左記の値 |
| 7 | ○ | × | Close Other Requests | UINT | フォーマット不適合以外の理由で拒否されたForward_Closeの数 | 左記の値 |
| 8 | ○ | × | Connection Timeouts | UINT | Connection Managerにより制御されているコネクションで発生したコネクションタイムアウトの合計数 | 左記の値 |

#### インスタンスサービス (付5 / 印刷 p.256 / 原本 p.258)

| サービスコード | サービス |
|---|---|
| 01H | Get_Attributes_All |
| 0EH | Get_Attribute_Single |
| 4EH | Forward_Close |
| 54H | Forward_Open |
| 5BH | Large_Forward_Open |

### TCP/IP Interface (付5 / 印刷 p.257 / 原本 p.259)

| オブジェクト名 | クラスID |
|---|---|
| TCP/IP Interface | F5H |

#### クラスアトリビュート(インスタンスID: 00H) (付5 / 印刷 p.257 / 原本 p.259)

○: 対応，×: 非対応

| アトリビュートID | アクセス Get | アクセス Set | 名称 | データタイプ | 内容 | 設定値(Set)/格納値(Get) |
|---|---|---|---|---|---|---|
| 1 | ○ | × | Revision | UINT | オブジェクトのリビジョン | 0004H |
| 2 | ○ | × | Max Instance | UINT | 最大インスタンスID | 0001H |
| 3 | ○ | × | Number of instances | UINT | 生成されているインスタンス数 | 0001H |
| 6 | ○ | × | Maximum ID Number Class Attributes | UINT | クラスアトリビュートのアトリビュートID番号 | 0007H |
| 7 | ○ | × | Maximum ID Number Instance Attributes | UINT | インスタンスアトリビュートのアトリビュートID番号 | 000DH |

#### クラスサービス (付5 / 印刷 p.257 / 原本 p.259)

| サービスコード | サービス | 備考 |
|---|---|---|
| 01H | Get_Attributes_All | — |
| 0EH | Get_Attribute_Single | — |

#### インスタンスアトリビュート(インスタンスID: 01H) (付5 / 印刷 p.257 / 原本 p.259)

○: 対応，×: 非対応

| アトリビュートID | アクセス Get | アクセス Set | 名称 | データタイプ | 内容 | 設定値(Set)/格納値(Get) |
|---|---|---|---|---|---|---|
| 1 | ○ | × | Status | DWORD | インタフェースステータス | （☞ 258ページ） |
| 2 | ○ | × | Configuration Capability | DWORD | インタフェース能力フラグ | （☞ 258ページ） |
| 3 | ○ | × | Configuration Control | DWORD | インタフェース制御フラグ | （☞ 258ページ） |
| 4 | ○ | × | Physical Link Object / Path size | UINT | 物理リンクオブジェクトのパスサイズ | 0002H |
| 4 | ○ | × | Physical Link Object / Path | Padded EPATH | 物理リンクオブジェクトを特定する論理セグメント | • 0: 20H<br>• 1: F6H<br>• 2: 24H<br>• 3: 01H |
| 5 | ○ | × | Interface Configuration / IP Address | UDINT | デバイスのIP アドレス | パラメータ設定値 |
| 5 | ○ | × | Interface Configuration / Network Mask | UDINT | デバイスのネットワークマスク | パラメータ設定値 |
| 5 | ○ | × | Interface Configuration / Gateway Address | UDINT | デフォルトのゲートウェイアドレス | パラメータ設定値 |
| 5 | ○ | × | Interface Configuration / Name Server | UDINT | プライマリネームサーバ | 00000000H |
| 5 | ○ | × | Interface Configuration / Name Server 2 | UDINT | セカンダリネームサーバ | 00000000H |
| 5 | ○ | × | Interface Configuration / Domain Name | STRING | デフォルトのドメイン名 | " "(NULL) |
| 6 | ○ | × | Host Name | STRING | ホスト名 | " "(NULL) |
| 13 | ○ | ○*1 | Encapsulation Inactivity Timeout | UINT | TCPコネクションまたはDTLSセッションがクローズになるまでの時間を設定(単位: 秒) | • 1~3600<br>0は無効となります。<br>(デフォルト: 120) |

*1 設定データは不揮発性メモリに保存されます。

※アトリビュートID 5 の IP Address / Network Mask / Gateway Address の「パラメータ設定値」は原本では3行の結合セル。

###### ■インタフェースステータス詳細 (付5 / 印刷 p.258 / 原本 p.260)

| ビット | 内容 | 値 |
|---|---|---|
| 0~3 | Interface Configuration Status | 2固定(パラメータの設定から取得したIPアドレスを設定するため ) |
| 4 | Mcast Pending | 0固定(TTL ValueおよびMcast Configアトリビュートの設定は非サポートのため) |
| 5 | Interface Configuration Pending | 0固定(Interface Configurationアトリビュート設定は非サポートのため) |
| 6 | AcdStatus | 0固定(アドレス重複検知設定は非サポートのため) |
| 7 | AcdFault | 0固定(アドレス重複検知設定は非サポートのため) |
| 8 | IANA Port Admin Change Pending | 0固定(IANA Port Adminアトリビュート設定は非サポートのため) |
| 9 | IANA Protocol Admin Change Pending | 0固定(IANA Protocol Adminアトリビュート設定は非サポートのため) |
| 10~31 | 予約 | 0固定 |

###### ■インタフェース能力フラグ詳細 (付5 / 印刷 p.258 / 原本 p.260)

| ビット | 内容 | 値 |
|---|---|---|
| 0 | BOOTP Client | 0固定(BOOTP非サポートのため) |
| 1 | DNS Client | 0固定(DNSによる名前解決は非サポートのため) |
| 2 | DHCP Client | 0固定(DHCPによるIPアドレス設定は非サポートのため) |
| 3 | DHCP-DNS Update | 0固定(DHCP リクエストによるホストネーム送信は非サポートのため) |
| 4 | Configuration Settable | 0固定(Interface Configurationアトリビュート設定は非サポートのため) |
| 5 | Hardware Configurable | 1固定(パラメータで設定されたIPアドレスに対応するため) |
| 6 | Interface Configuration Change Requires Reset | 0固定(Interface Configurationアトリビュート設定は非サポートのため) |
| 7 | AcdCapable | 0固定(アドレス重複検知設定は非サポートのため) |
| 8~31 | 予約 | 0固定 |

###### ■インタフェース制御フラグ詳細 (付5 / 印刷 p.258 / 原本 p.260)

| ビット | 内容 | 値 |
|---|---|---|
| 0~3 | Configuration Method | 0固定(パラメータで設定からIPアドレスを使用するため) |
| 4 | DNS Enable | 0固定(DNSによる名前解決は非サポートのため) |
| 5~31 | 予約 | 0固定 |

#### インスタンスサービス (付5 / 印刷 p.258 / 原本 p.260)

| サービスコード | サービス |
|---|---|
| 01H | Get_Attributes_All |
| 0EH | Get_Attribute_Single |
| 10H | Set_Attribute_Single |

### Ethernet Link (付5 / 印刷 p.259 / 原本 p.261)

| オブジェクト名 | クラスID |
|---|---|
| Ethernet Link | F6H |

#### クラスアトリビュート(インスタンスID: 00H) (付5 / 印刷 p.259 / 原本 p.261)

○: 対応，×: 非対応

| アトリビュートID | アクセス Get | アクセス Set | 名称 | データタイプ | 内容 | 設定値(Set)/格納値(Get) |
|---|---|---|---|---|---|---|
| 1 | ○ | × | Revision | UINT | オブジェクトのリビジョン | 0004H |
| 2 | ○ | × | Max Instance | UINT | 最大インスタンスID | 0001H |
| 3 | ○ | × | Number of instances | UINT | 生成されているインスタンス数 | 0001H |

#### クラスサービス (付5 / 印刷 p.259 / 原本 p.261)

| サービスコード | サービス | 備考 |
|---|---|---|
| 01H | Get_Attributes_All | — |
| 0EH | Get_Attribute_Single | — |

#### インスタンスアトリビュート(インスタンスID: 01H) (付5 / 印刷 p.259-261 / 原本 p.261-263)

○: 対応，—: 非対応

（原本の凡例は「—: 非対応」だが、表中の非対応は「×」で記載されている。表は原本の記号のまま）

| アトリビュートID | アクセス Get | アクセス Set | 名称 | データタイプ | 内容 | 設定値(Set)/格納値(Get) |
|---|---|---|---|---|---|---|
| 1 | ○ | × | Interface Speed | UDINT | 現在使用しているインタフェースの通信速度(単位: Mbps) | • 10<br>• 100<br>• 1000 |
| 2 | ○ | × | Interface Flags | DWORD | インタフェースのステータスフラグ | （☞ 261ページ） |
| 3 | ○ | × | Physical Address | USINT型配列[6] | MAC層アドレス | ユニットごとに<br>異なります。 |
| 4 | ○*2 | × | Interface Counters / In Octets | UDINT | インタフェース上で受信したオクテット数 | 左記の値 |
| 4 | ○*2 | × | Interface Counters / In Ucast Packets | UDINT | インタフェース上で受信したユニキャストパケット数 | 左記の値 |
| 4 | ○*2 | × | Interface Counters / In NUcast Packets | UDINT | インタフェース上で受信したユニキャスト以外のパケット数 | 左記の値 |
| 4 | ○*2 | × | Interface Counters / In Discards | UDINT | インタフェース上で受信したが，破棄された着信パケット数 | 00000000H |
| 4 | ○*2 | × | Interface Counters / In Errors | UDINT | エラーを含む着信パケット数(InDiscardsに含まれないパケット数) | 00000000H |
| 4 | ○*2 | × | Interface Counters / In Unknown Protos | UDINT | 不明のプロトコルを含む着信パケット数 | 左記の値 |
| 4 | ○*2 | × | Interface Counters / Out Octets | UDINT | インタフェース上で送信したオクテット数 | 左記の値 |
| 4 | ○*2 | × | Interface Counters / Out Ucast Packets | UDINT | インタフェース上で送信したユニキャストパケット数 | 左記の値 |
| 4 | ○*2 | × | Interface Counters / Out NUcast Packets | UDINT | インタフェース上で送信したユニキャスト以外のパケット数 | 左記の値 |
| 4 | ○*2 | × | Interface Counters / Out Discards | UDINT | 破棄された発信パケット数 | 00000000H |
| 4 | ○*2 | × | Interface Counters / Out Errors | UDINT | エラーを含む発信パケット数 | 00000000H |
| 5 | ○*2 | × | Media Counters / Alignment Errors | UDINT | 長さがオクテット整数でない受信フレーム数 | 左記の値 |
| 5 | ○*2 | × | Media Counters / FCS Errors | UDINT | FCSチェックに合格しない受信フレーム数 | 左記の値 |
| 5 | ○*2 | × | Media Counters / Single Collisions | UDINT | コリジョンが1回だけあった送信成功フレーム数 | 左記の値 |
| 5 | ○*2 | × | Media Counters / Multiple Collisions | UDINT | コリジョンが2回以上あった送信成功フレーム数 | 左記の値 |
| 5 | ○*2 | × | Media Counters / SQE Test Errors | UDINT | SQEテストエラーメッセージが生成された回数 | 00000000H |
| 5 | ○*2 | × | Media Counters / Deferred Transmissions | UDINT | 媒体がビジーだったため，最初の送信の試みが遅れたフレーム数 | 左記の値 |
| 5 | ○*2 | × | Media Counters / Late Collisions | UDINT | パケット送信において512ビットタイムより後にパケット送信に検出されたコリジョンの数 | 左記の値 |
| 5 | ○*2 | × | Media Counters / Excessive Collisions | UDINT | コリジョン過多のため送信に失敗したフレーム数 | 左記の値 |
| 5 | ○*2 | × | Media Counters / MAC Transmit Errors | UDINT | 内部のMAC 副層送信エラーのため送信に失敗したフレーム数 | 00000000H |
| 5 | ○*2 | × | Media Counters / Carrier Sense Errors | UDINT | フレームを送信しようとしたときにキャリアセンス条件を失った回数，またはアサートしなかった回数 | 00000000H |
| 5 | ○*2 | × | Media Counters / Frame Too Long | UDINT | 最大許容フレームサイズを超えた受信フレーム数 | 00000000H |
| 5 | ○*2 | × | Media Counters / MAC Receive Errors | UDINT | 内部のMAC 副層受信エラーのため，インタフェースで受信に失敗したフレーム数 | 00000000H |
| 6 | ○ | ○ | Interface Control / Control Bits | WORD | インタフェース管理ビット | 0001H |
| 6 | ○ | ○ | Interface Control / Forced Interface Speed | UINT | インタフェースに強制される動作スピード | 0000H |
| 7 | ○ | × | Interface Type | USINT | インタフェースのタイプ | 02H |
| 8 | ○ | × | Interface State | USINT | インタフェースの現在の状態 | 01H |
| 9 | ○ | ○ | Admin State | USINT | 管理状態 | 01H |
| 11 | ○ | × | Interface Capability / Capability Bits | DWORD | Speed/Duplex以外のインタフェース機能 | 00000006H |
| 11 | ○ | × | Interface Capability / Speed/Duplex Options / Speed/Duplex Array Count | USINT | Speed/Duplex配列数 | 00H |
| 11 | ○ | × | Interface Capability / Speed/Duplex Options / Speed/Duplex Array / Interface Speed | UINT | インタフェースを強制的に動作させるスピード | — |
| 11 | ○ | × | Interface Capability / Speed/Duplex Options / Speed/Duplex Array / Interface Duplex Mode | USINT | インタフェースのDuplexモード*1 | — |
| 12 | ○*2 | × | HC Interface Counters / HCInOctets | ULINT | インタフェース上で受信したオクテット数 | 左記の値 |
| 12 | ○*2 | × | HC Interface Counters / HCInUcastPkts | ULINT | インタフェース上で受信したユニキャストパケット数 | 左記の値 |
| 12 | ○*2 | × | HC Interface Counters / HCInMulticastPkts | ULINT | インタフェース上で受信したマルチキャストパケット数 | 0000000000000000H |
| 12 | ○*2 | × | HC Interface Counters / HCInBroadcastPkts | ULINT | インタフェースで受信したブロードキャストパケット数 | 0000000000000000H |
| 12 | ○*2 | × | HC Interface Counters / HCOutOctets | ULINT | インタフェース上で送信したオクテット数 | 左記の値 |
| 12 | ○*2 | × | HC Interface Counters / HCOutUcastPkts | ULINT | インタフェース上で送信したパケット数 | 左記の値 |
| 12 | ○*2 | × | HC Interface Counters / HCOutMulticastPkts | ULINT | インタフェース上で送信したマルチキャストパケット数 | 0000000000000000H |
| 12 | ○*2 | × | HC Interface Counters / HCOutBroadcastPkts | ULINT | インタフェース上で送信したブロードキャストパケット数 | 0000000000000000H |
| 13 | ○*2 | × | HC Media Counters / HCStatsAlignmentErrors | ULINT | Alignment Errorsの64bit版 | 左記の値 |
| 13 | ○*2 | × | HC Media Counters / HCStatsFCSErrors | ULINT | FCS Errorsの64bit版 | 0000000000000000H |
| 13 | ○*2 | × | HC Media Counters / HCStatsInternalMacTransmitErrors | ULINT | MAC Transmit Errorsの64bit版 | 0000000000000000H |
| 13 | ○*2 | × | HC Media Counters / HCStatsFrameTooLongs | ULINT | Flame Too Longの64bit版 | 0000000000000000H |
| 13 | ○*2 | × | HC Media Counters / HCStatsInternalMacReceiveErrors | ULINT | MAC Receive Errorsの64bit版 | 0000000000000000H |
| 13 | ○*2 | × | HC Media Counters / HCStatsSymbolErrors | ULINT | 有効なキャリアが存在する場合のメディア上にある不正なデータシンボル数 | 0000000000000000H |

*1 Interface Speedと組み合わせて配列を表示します。ユニットがサポートしているスピードとDuplexモードを示します。
*2 Get_and_Clearも利用可能。

※原本では表が p.261（アトリビュートID 1～4）、p.262（ID 5～12）、p.263（ID 13）に分かれている。ULINT の「0000000000000000H」は原本ではセル内で「0000000000000 / 000H」と折り返されている（16桁）。「Flame Too Long」は原本の表記のまま。

###### ■インタフェースステータスフラグ詳細 (付5 / 印刷 p.261 / 原本 p.263)

| ビット | 項目 | 値 |
|---|---|---|
| 0 | リンクアップ状態 | • 0: リンクダウン<br>• 1: リンクアップ |
| 1 | 接続状態(全二重/半二重) | • 0: 半二重<br>• 1: 全二重 |
| 2~4 | オートネゴシエーションの状態 | • 0: オートネゴシエーション実行中<br>• 1: オートネゴシエーションに失敗し，デフォルトの通信速度，通信方式にて動作中<br>• 2: 通信方式の検出に失敗したが，通信速度検出には成功した<br>• 3: オートネゴシエーション正常完了<br>• 4: オートネゴシエーション未実行 |
| 5 | 手動設定時の再起動要否 | 0固定(手動設定に非対応 のため) |
| 6 | Local Hardware Fault検出状態 | 0固定(Local Hardware Fault未検出のため) |
| 7~31 | 固定値 | 0 |

#### インスタンスサービス (付5 / 印刷 p.261 / 原本 p.263)

| サービスコード | サービス |
|---|---|
| 01H | Get_Attributes_All |
| 0EH | Get_Attribute_Single |
| 10H | Set_Attribute_Single |
| 4CH | Get_and_Clear*1 |

*1 指定のアトリビュートの値を取得後クリアします。アトリビュート[4, 5, 12, 13]に対してのみ使用可能です。

## 転記時の要確認一覧 (付5 / 原本 p.252-263)

- Message Router インスタンスアトリビュート ID1 Classes のデータタイプは原本で「USINT型配列[8]」だが、格納値は 0001H 等の16ビット値で記載されている。原本どおり転記（UINT型配列の誤記の可能性あり、要確認）。
- Ethernet Link インスタンスアトリビュートの凡例は「○: 対応，—: 非対応」だが、表中の非対応は「×」。原本どおり転記。
- Ethernet Link インスタンスアトリビュートの Speed/Duplex Array の設定値(Set)/格納値(Get)は原本で「—」。
