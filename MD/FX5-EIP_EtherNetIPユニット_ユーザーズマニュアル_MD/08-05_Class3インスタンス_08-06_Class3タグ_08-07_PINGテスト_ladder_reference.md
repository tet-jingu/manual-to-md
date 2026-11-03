# 三菱 MELSEC iQ-F FX5-EIP形 EtherNet/IPユニット ユーザーズマニュアル 第8章 プログラミング（8.5 Class3インスタンス通信の交信例 / 8.6 Class3タグ通信の交信例 / 8.7 PINGテストのプログラム例）

| 項目 | 内容 |
|---|---|
| 原本 | 三菱電機 MELSEC iQ-F FX5-EIP形EtherNet/IPユニットユーザーズマニュアル |
| 発行元 | 三菱電機株式会社 |
| 資料番号 / 版数 | SH-082708 / B版（PDFメタデータ subject: SH-082708-B） |
| 原本PDF | `PDF/MELSEC iQ-F FX5-EIP形EtherNet_IPユニットユーザーズマニュアル.pdf` (全274ページ) |
| 本ファイルの範囲 | 第8章 8.5〜8.7 (印刷 p.156-174 / PDF p.158-176) |
| ページ対応 | 「原本 p.」はPDFのページ番号、「印刷 p.」は原本フッタのページ番号。印刷ページ = PDFページ − 2。本文中の「〇〇ページ参照」は印刷ページ |
| 変換日 | 2026-10-23 |
| 変換方法 | pypdfium2(本文) + PyMuPDF 200dpi 画像の目視(全ページ) |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。

**転記上の扱い**: 原本の結合セルは各行に値を展開。セル内改行は `<br>`。図は【図】プレースホルダ＋読み取れる事実の箇条書き。GX Works3 の設定画面キャプチャは【図】＋画面上の項目名・設定値を表で全件。グローバルラベル定義画面（キャプチャ）は全行を表に起こした。ラダー図のニモニックは原本に記載がなく、図から書き起こしたもの（各所に注記）。バッファメモリは本文・表では原本表記の `Un￥G`/`U1￥G`（全角￥）に統一、ニモニックのコードブロック内のみ GX Works3 入力形式の `U1￥G` と表記。ラベル名は原本図の表記のまま（`VAR_GLOVAL_RETAIN` 等の綴りも原文どおり）。見出しレベル: 章 `##` / 節 `###` / 項 `####` / ◆(帯見出し) `#####` / ■ `######`。

---

## 主要用語 対訳表 (Glossary) (第8章 8.5〜8.7 / 原本 p.158-176)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| Class3インスタンス通信 | Class3 instance communication | — | 参考訳 |
| Class3タグ通信 | Class3 tag communication | — | 参考訳 |
| Class3/UCMM タグ | Class3/UCMM tag | UCMM = Unconnected Message Manager | 参考訳 |
| クライアント | Client | — | 参考訳 |
| サーバ | Server | — | 参考訳 |
| オリジネータ | Originator | — | 参考訳 |
| ターゲット | Target | — | 参考訳 |
| 自ノード | Own node | — | 参考訳 |
| 最大コネクション数設定 | Maximum number of connections setting | — | 参考訳 |
| コネクション設定 | Connection setting | — | 参考訳 |
| コネクションNo. | Connection No. | — | 参考訳 |
| 要求No. | Request No. | — | 参考訳 |
| 要求コマンド | Request command | — | 参考訳 |
| サービスコード | Service code | Service | 参考訳 |
| クラスID | Class ID | Class | 参考訳 |
| インスタンスID | Instance ID | Instance | 参考訳 |
| アトリビュートID | Attribute ID | Attribute | 参考訳 |
| Get_Attributes_All | Get_Attributes_All | 01H | 原本併記 |
| Identityオブジェクト | Identity object | Class 01H | 参考訳 |
| 要求データ / 要求データサイズ | Request data / request data size | — | 参考訳 |
| 応答データ / 応答データサイズ | Response data / response data size | — | 参考訳 |
| 要求パケット間隔 | Requested Packet Interval | RPI | 参考訳 |
| タイムアウト乗数 | Timeout multiplier | — | 参考訳 |
| トリガータイプ | Trigger type | Cyclic / Application Trigger | 参考訳 |
| Large_Forward_Open | Large_Forward_Open | — | 原本併記 |
| タグ名 / タグ名文字数 | Tag name / number of tag name characters | — | 参考訳 |
| データ型 / タグデータタイプ | Data type / tag data type | INT(00C3H), DINT(00C4H) | 参考訳 |
| 書込み / Write要求 | Write / Write request | — | 参考訳 |
| 読出し / Read要求 | Read / Read request | — | 参考訳 |
| データの泣き別れ | Data inconsistency (data split between old and new values) | — | 参考訳 |
| 通信READY | Communication READY | U1￥G35.F | 参考訳 |
| EtherNet/IP通信起動要求 | EtherNet/IP communication start request | U1￥G272 | 参考訳 |
| EtherNet/IP通信起動状態 | EtherNet/IP communication start status | U1￥G273 | 参考訳 |
| EtherNet/IP自動起動設定 | EtherNet/IP automatic start setting | — | 参考訳 |
| 入力データサイズ / 入力データエリア | Input data size / input data area | U1￥G304~U1￥G367 / U1￥G16944～U1￥G63151 | 参考訳 |
| 出力/メッセージ通信(サーバ)データサイズ / データエリア | Output / message communication (server) data size / data area | U1￥G432~U1￥G495 / U1￥G63152～U1￥G109359 | 参考訳 |
| PINGテスト | PING test | — | 参考訳 |
| エコー要求 / エコー応答 | Echo request / echo reply | — | 参考訳 |
| PINGテスト要求エリア | PING test request area | Un￥G240～Un￥G243 | 参考訳 |
| PINGテスト応答エリア / 応答結果エリア | PING test response (result) area | Un￥G244～Un￥G256 | 参考訳 |
| 交信タイムチェック | Communication time check | Un￥G240 | 参考訳 |
| 送信回数 | Number of transmissions | Un￥G241 | 参考訳 |
| 総パケット送信回数 | Total number of packets sent | Un￥G244 | 参考訳 |
| 受信回数 | Number of receptions | Un￥G245 | 参考訳 |
| 損失回数 | Number of losses | Un￥G246 | 参考訳 |
| PINGテスト完了 | PING test completion | U1￥G35.2 | 参考訳 |
| PINGテスト実行要求 | PING test execution request | U1￥G37.2 | 参考訳 |
| ユニットラベル | Module label | — | 参考訳 |
| グローバルラベル | Global label | VAR_GLOBAL | 参考訳 |
| ファンクションブロック | Function block | FB | 参考訳 |
| ラッチ範囲 | Latch range | VAR_GLOVAL_RETAIN（原文表記） | 参考訳 |
| EDSファイル | Electronic Data Sheet file | EDS | 参考訳 |
| エンジニアリングツール | Engineering tool | GX Works3 | 参考訳 |

## 変換範囲表 (第8章 8.5〜8.7 / 原本 p.158-176)

| 原本ページ | 節 | 扱い |
|---|---|---|
| p.158-163 | 8.5 Class3インスタンス通信の交信例（システム構成・パラメータ設定・プログラム例） | 全文(プログラム例を含む) |
| p.164-172 | 8.6 Class3タグ通信の交信例（システム構成・通信内容・パラメータ設定・クライアント側/サーバ側プログラム例） | 全文(プログラム例を含む) |
| p.173-176 | 8.7 PINGテストのプログラム例 | 全文(プログラム例を含む) |
| 上記以外 | 他章・他節 | 同フォルダの他ファイル参照 |

## 目次 (第8章 8.5〜8.7)

- [8 プログラミング（続き）](#8-プログラミング続き-8--印刷-p156--原本-p158)
  - [8.5 Class3インスタンス通信の交信例 (8.5 / 印刷 p.156 / 原本 p.158)](#85-class3インスタンス通信の交信例-85--印刷-p156--原本-p158)
  - [8.6 Class3タグ通信の交信例 (8.6 / 印刷 p.162 / 原本 p.164)](#86-class3タグ通信の交信例-86--印刷-p162--原本-p164)
  - [8.7 PINGテストのプログラム例 (8.7 / 印刷 p.171 / 原本 p.173)](#87-pingテストのプログラム例-87--印刷-p171--原本-p173)

## 8 プログラミング（続き） (8 / 印刷 p.156 / 原本 p.158)

### 8.5 Class3インスタンス通信の交信例 (8.5 / 印刷 p.156 / 原本 p.158)

FX5-EIP間でClass3インスタンス通信を行う例を示します。

#### システム構成 (8.5 / 印刷 p.156 / 原本 p.158)

Class3インスタンス通信の交信例は，下記のシステム構成を使用して説明します。
各FX5-EIPは”最大コネクション数設定”が64に設定されているものとします。

【図】Class3インスタンス通信のシステム構成（原本 p.158）
- クライアント: 192.168.4.10（FX5-EIP装着のCPUユニット）
- サーバ: 192.168.4.11（FX5-EIP装着のCPUユニット）
- 両者はスイッチングハブ経由で接続。クライアント→サーバに「要求コマンド」の矢印

###### 要求コマンド (8.5 / 印刷 p.156 / 原本 p.158)

- Service: 01H (Get_Attributes_All)
- Class: 01H (Identityオブジェクト)
- Attribute: 00H
- Instance: 01H

#### パラメータ設定 (8.5 / 印刷 p.156 / 原本 p.158)

エンジニアリングツールを使用してパラメータを設定します。

> **Point**
> プログラム例では，設定手順で示すパラメータ以外の設定はデフォルトを使用します。パラメータについては，下記を参照してください。
> ☞ 87ページ パラメータ設定

##### FX5-EIP(クライアント)の設定 (8.5 / 印刷 p.157 / 原本 p.159)

エンジニアリングツールをクライアント側のCPUユニットに接続し，パラメータを設定します。

1. CPUユニットを下記で設定します。
   - ナビゲーションウィンドウ⇨[パラメータ]⇨[ユニット情報]⇨[FX5-EIP]⇨[ユニットパラメータ]⇨[基本設定]

【図】基本設定 画面（原本 p.159）

| 項目 | 設定 |
|---|---|
| 自ノード設定 / IPアドレス設定 / IPアドレス | 192 . 168 . 4 . 10 |
| 自ノード設定 / IPアドレス設定 / サブネットマスク | 255 . 255 . 255 . 0 |
| 自ノード設定 / IPアドレス設定 / デフォルトゲートウェイ | （空欄） |
| 自ノード設定 / 交信データコード | バイナリ |
| 自ノード設定 / オープン方法の設定 | プログラムでOPENしない |

IPアドレス: 192.168.4.10
サブネットマスク: 255.255.255.0

2. [適用]ボタンをクリックします。
3. ”EtherNet/IP構成”にて，EtherNet/IPの通信パラメータを設定します。
   - [ナビゲーションウィンドウ]⇨[パラメータ]⇨[ユニット情報]⇨[FX5-EIP]⇨[EtherNet/IP構成(ユニット拡張パラメータ)]
4. ”ユニット一覧”から”FX5-EIP”をEtherNet/IP機器一覧に追加します。

【図】EtherNet/IP構成 (装着位置No.：1[U1]) 画面（原本 p.159）

| No. | 形名 | 機器名 | IPアドレス | 予約ノード | コネクション設定 | モジュール構成設定 | 使用スロット数 |
|---|---|---|---|---|---|---|---|
| （自ノード） | 自ノード | | 192.168.4.10 | | <詳細設定> | | |
| 1 | FX5-EIP | | 192.168.4.11 | 設定なし | <詳細設定> | | |

- ユニット一覧: EtherNet/IP機器(汎用) / EtherNet/IP機器(三菱電機) ⇨ 通信アダプタ ⇨ FX5-EIP (1.1)、RJ71GN11-EI… (3.1)、RJ71GN11-EI… (2.1)、RJ71GN11-EI… (1.1)
- 選択中ユニットの情報: 【ベンダ名】三菱電機 / 【製品種別名】通信アダプタ / 【形名】FX5-EIP / 【リビジョン】DeviceRevision:1.1、FileRevision:1.1
- 下部の構成図: 192.168.4.10（自ノード 総ノード数: 1/64）と 192.168.4.11（FX5-EIP）

> **Point**
> ”ユニット一覧”に”FX5-EIP”が無い場合は，EDSファイルの追加が必要です。
> EDSファイルの追加については，下記を参照してください。
> ☞ 120ページ EDSファイルの追加/削除

5. ”コネクション設定”列の<詳細設定>をダブルクリックして，オリジネータのコネクションを設定します。

【図】コネクション設定 画面（原本 p.160）
- コネクション情報: コネクション数 1/64、通信処理性能(PPS) 0
- コネクション一覧(ユニット順): 自ノード ⇨ ターゲット / タグ / オリジネータ ⇨ FX5-EIP(192.168.4.11) ⇨ (001)
- Error:0 / Warning:0 / Information:0

| 項目名 | 設定値 | 単位 |
|---|---|---|
| コネクション名 | コネクション(Class3 インスタンス通信) | - |
| コネクションNo | 001 | - |
| 通信方式 | インスタンス通信 | - |
| コメント | （空欄） | - |
| サービス | 1 | - |
| データサイズ | 0 | byte |
| Large_Forward_Open | 自動で使用する | - |
| トリガータイプ | Cyclic | - |
| 要求パケット間隔(RPI) | 200000 | μs |
| タイムアウト乗数 | x4 | - |
| クラスID | 1 | - |
| インスタンスID | 1 | - |
| アトリビュートID | 0 | - |

- コネクションを追加する際[コネクション(Class3インスタンス通信)]を選択します。
- サービス: 1
- クラスID: 1
- インスタンスID: 1

6. [適用]ボタンをクリックします。
7. [OK]ボタンをクリックして，コネクション設定を閉じます。
8. [設定を反映して閉じる]を選択し，”EtherNet/IP構成”画面を閉じます。
9. 設定したパラメータをオリジネータ側のCPUユニットに書き込み，CPUユニットをリセット，または電源をOFF→ONします。
   - [オンライン]⇨[シーケンサへの書込み]

##### FX5-EIP(サーバ)の設定 (8.5 / 印刷 p.159 / 原本 p.161)

エンジニアリングツールをサーバ側のCPUユニットに接続し，パラメータを設定します。

1. IPアドレスを設定します。
   - ナビゲーションウィンドウ⇨[パラメータ]⇨[ユニット情報]⇨[FX5-EIP]⇨[ユニットパラメータ]⇨[基本設定]

【図】基本設定 画面（原本 p.161）

| 項目 | 設定 |
|---|---|
| 自ノード設定 / IPアドレス設定 / IPアドレス | 192 . 168 . 4 . 11 |
| 自ノード設定 / IPアドレス設定 / サブネットマスク | 255 . 255 . 255 . 0 |
| 自ノード設定 / IPアドレス設定 / デフォルトゲートウェイ | （空欄） |
| 自ノード設定 / 交信データコード | バイナリ |
| 自ノード設定 / オープン方法の設定 | プログラムでOPENしない |

IPアドレス: 192.168.4.11
サブネットマスク: 255.255.255.0

2. ”EtherNet/IP自動起動設定”を”起動する”に設定します。
   - ナビゲーションウィンドウ⇨[パラメータ]⇨[ユニット情報]⇨[FX5-EIP]⇨[ユニットパラメータ]⇨[基本設定]

【図】基本設定 画面（原本 p.161）

| 項目 | 設定 |
|---|---|
| EtherNet/IP自動起動設定 / EtherNet/IP自動起動設定 | 起動する |

> **Point**
> 本項目を設定しない場合，クライアント側のプログラムと同様の方法でEtherNet/IP通信起動要求にH10を設定してください。
> ☞ 160ページ クライアント側のプログラム

3. [適用]ボタンをクリックします。
4. 設定したパラメータをサーバ側のCPUユニットに書き込み，CPUユニットをリセット，または電源をOFF→ONします。
   - [オンライン]⇨[シーケンサへの書込み]

> **Point**
> Class3インスタンス通信では，”EtherNet/IP構成”によるパラメータ設定は不要です。

#### プログラム例 (8.5 / 印刷 p.160 / 原本 p.162)

CPUユニットをSTOP→RUNすることで，Class3インスタンス通信のプログラムを実行します。
プログラム内のClass3コマンド送信要求をONすることで，Class3インスタンス通信を実行します。
プログラムを実行すると，下記の要求コマンドをサーバ側に送ります。

| 項目 | 指定するデータ | 内容 |
|---|---|---|
| サービスコード | 01H | Get_Attributes_All(クラスIDおよびインスタンスIDで指定したインスタンスの持つ全アトリビュートを取得します。) |
| クラスID | 01H | Identityオブジェクトを指定します。 |
| インスタンスID | 01H | — |
| アトリビュートID | 00H | Get_Attributes_Allのため，特定のアトリビュートIDの指定はありません。 |
| 要求データ | なし | 要求データサイズは0を指定します。 |

> **Point**
> サーバ側のプログラムは不要です。

##### クライアント側のプログラム (8.5 / 印刷 p.160 / 原本 p.162)

| 分類 | ラベル名 | 内容 | デバイス |
|---|---|---|---|
| ユニットラベル | FX5EIP_1.bSts_CommunicationReady_D | 通信READY | U1￥G35.F |
| ユニットラベル | FX5EIP_1.stEIPArea64.uSet_CommunicationStart_D | EtherNet/IP通信起動要求 | U1￥G272 |
| ユニットラベル | FX5EIP_1.stEIPArea64.uSts_CommunicationStart_D | EtherNet/IP通信起動状態 | U1￥G273 |
| 定義するラベル | 下記のように，グローバルラベルを定義します。（下表） | | |
| 使用ファンクションブロック | • M+FX5-EIP_Class3Originator_MessageSend | | |

定義するラベル（グローバルラベル定義画面より。原本 p.162）

| No. | ラベル名 | データ型 | クラス | 割付け(デバイス/ラベル) | Japanese/日本語(表示対象) |
|---|---|---|---|---|---|
| 1 | bClass3_MessageCommandSendRequest | ビット | VAR_GLOBAL | M100 | Class3メッセージコマンド送信要求 |
| 2 | bRun_SendClass3_Message | ビット | VAR_GLOBAL | M110 | Class3メッセージ通信要求実行中 |
| 3 | bOK_SendClass3_Message | ビット | VAR_GLOBAL | M120 | Class3メッセージコマンド要求正常完了 |
| 4 | bNG_SendClass3_Message | ビット | VAR_GLOBAL | M130 | Class3メッセージコマンド要求異常完了 |
| 5 | unSetClass3_MessageRequestData | ワード[符号なし]/ビット列[16ビット](0..706) | VAR_GLOBAL | D1000 | Class3メッセージ通信要求データ格納 |
| 6 | unGetClass3_MessageResponseData | ワード[符号なし]/ビット列[16ビット](0..706) | VAR_GLOBAL | D2000 | Class3メッセージ通信応答データ格納 |
| 7 | unSetRequestNo | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D3000 | 要求No |
| 8 | unGetErrorCode | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D3001 | エラーコード |
| 9 | unGetStatusErrorCode | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D3002 | 通信エラーコード |
| 10 | unGetResponseDataSize | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D3003 | 応答データサイズ |

> CPUユニットによって，デフォルトのラッチ範囲では，変換が通らないため，データレジスタ(D)のラッチ範囲を変更，またはデータレジスタ(D)を割り付けたラベルのクラスをVAR_GLOVAL_RETAINに定義してください。ラッチ設定については，下記を参照してください。
> 📖 MELSEC iQ-F FX5ユーザーズマニュアル(応用編)
> 応答データの格納先は，サーバとなるEtherNet/IP機器のマニュアルを参照し，十分なデータサイズを確保してください。

【図】クライアント側ラダープログラム（原本 p.163）。ステップ (0)、(13)、(1406) END。

※ニモニックは原本に記載なし。図から書き起こしたもの。FB呼出しは入出力の結線を列挙する形で記載。

```
; (0)
LD    FX5EIP_1.bSts_CommunicationReady_D                 ; 通信READY U1\G35.F (a接点)
MOV   H1   unSetRequestNo                                ; D3000 ← H1 (要求No.)
MOV   H10  FX5EIP_1.stEIPArea64.uSet_CommunicationStart_D ; U1\G272 ← H10 (EtherNet/IP通信起動要求)

; (13)
LD=_U H1   FX5EIP_1.stEIPArea64.uSts_CommunicationStart_D ; U1\G273 = H1 (通信起動状態)
AND   bClass3_MessageCommandSendRequest                  ; M100 (a接点)
; FB: M_FX5_EIP_Class3Originator_MessageSend_00A_1
;     (M+FX5-EIP_Class3Originator_MessageSend_00A) "Class3 Originator Message Send"
;   入力  B:   i_bEN          ← 上記接点の結果
;   入力  DUT: i_stModule     ← FX5EIP_1
;   入力  UW:  i_uRequestData ← unSetClass3_MessageRequestData   (D1000)
;   入力  UW:  i_uRPI         ← H0
;   入力  UW:  i_uRequestNo   ← unSetRequestNo                   (D3000)
;   出力  B:   o_bENO         → OUT bRun_SendClass3_Message      (M110)
;   出力  B:   o_bOK          → OUT bOK_SendClass3_Message       (M120)
;   出力  B:   o_bErr         → OUT bNG_SendClass3_Message       (M130)
;   出力  UW:  o_uErrId       → unGetErrorCode                   (D3001)
;   出力  UW:  o_uStatusId    → unGetStatusErrorCode             (D3002)
;   出力  UW:  o_uResponseData→ unGetClass3_MessageResponseData  (D2000)
;   出力  UW:  o_uResponseSize→ unGetResponseDataSize            (D3003)
;   (FB下部表示: pbo_u2CIPResponseCode, pbo_udRequestCompleteCount)

; (1406)
END
```

- (0) Class3メッセージ通信をするための要求No.を設定して，EtherNet/IP通信を開始します。
- (13) M100をONすることで，M+FX5-EIP_Class3Originator_MessageSendが実行されて，要求データをサーバ側に送信します。
  M120がONのとき，サーバ側から応答結果がD2000以降に格納されます。(D3003に格納された応答データサイズ÷2(バイト)分が格納されます(切上げ))
  応答データサイズが奇数の場合は，最終デバイスの下位1バイトのみデータが格納されます。

> **Point**
> 設定する要求No.は，他のUCMM通信/Class1通信/Class3通信で使用する要求No.と重複しないよう注意してください。

### 8.6 Class3タグ通信の交信例 (8.6 / 印刷 p.162 / 原本 p.164)

FX5-EIP間でClass3タグ通信を行う例を示します。

#### システム構成 (8.6 / 印刷 p.162 / 原本 p.164)

Class3タグ通信の交信例は，下記のシステム構成を使用して説明します。
各FX5-EIPは”最大コネクション数設定”が64に設定されているものとします。

【図】Class3タグ通信のシステム構成（原本 p.164）
- クライアント: 192.168.5.10、サーバ: 192.168.5.11（スイッチングハブ経由で接続）
- クライアント→サーバに「Write要求」と「Read要求」の矢印

###### Write要求 (8.6 / 印刷 p.162 / 原本 p.164)

- タグ名: Tag001
- タグタイプ: INT型
- サイズ: 10+要求データ(10ワード分)

###### Read要求 (8.6 / 印刷 p.162 / 原本 p.164)

- タグ名: Tag002
- タグタイプ: DINT型
- サイズ: 10

#### 通信内容 (8.6 / 印刷 p.162 / 原本 p.164)

Class3タグ通信の交信例を実行すると，下記の動作を実行します。

##### クライアント側の動作 (8.6 / 印刷 p.162 / 原本 p.164)

###### タグへのWrite要求 (8.6 / 印刷 p.162 / 原本 p.164)

Class3タグ通信のWrite要求を実行することで，サーバ側のTag001のタグに対して，D1000以降に格納したデバイスエリアのデータを要求サイズ分書き込みます。*1

*1 要求したデータタイプがINT型(00C3H)の場合，要求データサイズ×1ワード(プログラム例では10ワード)の要求データが送信されます。
要求したデータタイプがDINT(00C4H)型の場合，要求データサイズ×2ワードの要求データが送信されます。

###### タグのRead要求 (8.6 / 印刷 p.162 / 原本 p.164)

Class3タグ通信のRead要求を実行することで，サーバ側のTag002のタグに設定したデータを要求データサイズ分読み出します。読み出されたデータから，読出しデータサイズ(D3204に格納されるサイズ)分をD2000以降に格納します。
(読出しデータサイズは，相手機器のタグのデータ型に関わらず，受信したデータサイズがワード単位で格納されます)
また，相手機器のタグから読み出されるデータのサイズは，相手機器のタグのデータ型に依存します。*1

*1 相手機器のタグのデータ型がINT型(00C3H)の場合，読出し要求データサイズ×1ワードを読み出します。
相手機器のタグのデータ型がDINT型(00C4H)の場合，読出し要求データサイズ×2ワードを読み出します。

##### サーバ側の動作 (8.6 / 印刷 p.162 / 原本 p.164)

Tag001およびTag002に設定されたタグデータの現在値の読出しや，現在値の更新を行います。
サーバ側が動作する際，タグに対するクライアント側からのRead/Write要求はどちらも受付け可能です。
ただし，現在値の読出し中にWrite要求を受けデータが更新される場合や，現在値の更新中のデータがRead要求により読み出される場合に，データの泣き別れが発生する場合があります。

#### パラメータ設定 (8.6 / 印刷 p.163 / 原本 p.165)

エンジニアリングツールを使用してパラメータを設定します。

> **Point**
> プログラム例では，設定手順で示すパラメータ以外の設定はデフォルトを使用します。パラメータについては，下記を参照してください。
> ☞ 87ページ パラメータ設定

##### FX5-EIP(クライアント)の設定 (8.6 / 印刷 p.163 / 原本 p.165)

エンジニアリングツールをクライアント側のCPUユニットに接続し，パラメータを設定します。

1. CPUユニットを下記で設定します。
   - ナビゲーションウィンドウ⇨[パラメータ]⇨[ユニット情報]⇨[FX5-EIP]⇨[ユニットパラメータ]⇨[基本設定]

【図】基本設定 画面（原本 p.165）

| 項目 | 設定 |
|---|---|
| 自ノード設定 / IPアドレス設定 / IPアドレス | 192 . 168 . 5 . 10 |
| 自ノード設定 / IPアドレス設定 / サブネットマスク | 255 . 255 . 255 . 0 |
| 自ノード設定 / IPアドレス設定 / デフォルトゲートウェイ | （空欄） |
| 自ノード設定 / 交信データコード | バイナリ |
| 自ノード設定 / オープン方法の設定 | プログラムでOPENしない |

IPアドレス: 192.168.5.10
サブネットマスク: 255.255.255.0

2. [適用]ボタンをクリックします。
3. ”EtherNet/IP構成”にて，EtherNet/IPの通信パラメータを設定します。
   - [ナビゲーションウィンドウ]⇨[パラメータ]⇨[ユニット情報]⇨[FX5-EIP]⇨[EtherNet/IP構成(ユニット拡張パラメータ)]
4. ”ユニット一覧”から”FX5-EIP”をEtherNet/IP機器一覧に追加します。

【図】EtherNet/IP構成 (装着位置No.：1[U1]) 画面（原本 p.165）

| No. | 形名 | 機器名 | IPアドレス | 予約ノード | コネクション設定 | モジュール構成設定 | 使用スロット数 |
|---|---|---|---|---|---|---|---|
| （自ノード） | 自ノード | | 192.168.5.10 | | <詳細設定> | | |
| 1 | FX5-EIP | | 192.168.5.11 | 設定なし | <詳細設定> | | |

- ユニット一覧: EtherNet/IP機器(汎用) / EtherNet/IP機器(三菱電機) ⇨ 通信アダプタ ⇨ FX5-EIP (1.1)、RJ71GN11-EI… (3.1)、RJ71GN11-EI… (2.1)、RJ71GN11-EI… (1.1)
- 選択中ユニットの情報: 【ベンダ名】三菱電機 / 【製品種別名】通信アダプタ / 【形名】FX5-EIP / 【リビジョン】DeviceRevision:1.1、FileRevision:1.1
- 下部の構成図: 192.168.5.10（自ノード 総ノード数: 1/64）と 192.168.5.11（FX5-EIP）

> **Point**
> ”ユニット一覧”に”FX5-EIP”が無い場合は，EDSファイルの追加が必要です。
> EDSファイルの追加については，下記を参照してください。
> ☞ 120ページ EDSファイルの追加/削除

5. ”コネクション設定”列の<詳細設定>をダブルクリックして，コネクションNo.1，コネクションNo.2のタグを設定します。

- タグ設定(コネクションNo.1)

【図】コネクション設定 画面 コネクションNo.1（原本 p.166）
- コネクション情報: コネクション数 2/64、通信処理性能(PPS) 0
- コネクション一覧(ユニット順): 自ノード ⇨ ターゲット / タグ / オリジネータ ⇨ FX5-EIP(192.168.5.11) ⇨ (001)、(002)

| 項目名 | 設定値 | 単位 |
|---|---|---|
| コネクション名 | コネクション(Class3 タグ通信) | - |
| コネクションNo | 001 | - |
| ポート | 未使用 | - |
| リンクアドレス | 0 | - |
| 通信方式 | タグ通信 | - |
| コメント | （空欄） | - |
| サービス | 書込み | - |
| データ型 | INT | - |
| タグ名 | Tag001 | - |
| タグ名文字数 | 6 | 文字 |
| サイズ | 10 | - |
| トリガータイプ | Application Trigger | - |
| 要求パケット間隔(RPI) | 200000 | μs |
| タイムアウト乗数 | x4 | - |

- コネクションを追加する際”タグ”を選択して，[コネクション(Class3タグ通信)]を選択します。
- サービス: 書込み
- データ型: INT型(1ワード)
- タグ名: Tag001
- サイズ: 10

- タグ設定(コネクションNo.2)

【図】コネクション設定 画面 コネクションNo.2（原本 p.167）
- コネクション情報: コネクション数 2/64、通信処理性能(PPS) 0
- コネクション一覧: FX5-EIP(192.168.5.11) ⇨ (002) を選択

| 項目名 | 設定値 | 単位 |
|---|---|---|
| コネクション名 | コネクション(Class3 タグ通信) | - |
| コネクションNo | 002 | - |
| ポート | 未使用 | - |
| リンクアドレス | 0 | - |
| 通信方式 | タグ通信 | - |
| コメント | （空欄） | - |
| サービス | 読出し | - |
| データ型 | DINT | - |
| タグ名 | Tag002 | - |
| タグ名文字数 | 6 | 文字 |
| サイズ | 10 | - |
| トリガータイプ | Application Trigger | - |
| 要求パケット間隔(RPI) | 200000 | μs |
| タイムアウト乗数 | x4 | - |

- コネクションを追加する際”タグ”を選択して，[コネクション(Class3タグ通信)]を選択します。
- サービス: 読出し
- データ型: DINT型(2ワード)
- タグ名: Tag002
- サイズ: 10

6. [適用]ボタンをクリックします。
7. [OK]ボタンをクリックして，コネクション設定を閉じます。
8. [設定を反映して閉じる]を選択し，”EtherNet/IP構成”画面を閉じます。
9. 設定したパラメータをクライアント側のCPUユニットに書き込み，CPUユニットをリセット，または電源をOFF→ONします。
   - [オンライン]⇨[シーケンサへの書込み]

##### FX5-EIP(サーバ)の設定 (8.6 / 印刷 p.166 / 原本 p.168)

エンジニアリングツールをサーバ側のCPUユニットに接続し，パラメータを設定します。

1. CPUユニットを下記で設定します。
   - ナビゲーションウィンドウ⇨[パラメータ]⇨[ユニット情報]⇨[FX5-EIP]⇨[ユニットパラメータ]⇨[基本設定]

【図】基本設定 画面（原本 p.168）

| 項目 | 設定 |
|---|---|
| 自ノード設定 / IPアドレス設定 / IPアドレス | 192 . 168 . 5 . 11 |
| 自ノード設定 / IPアドレス設定 / サブネットマスク | 255 . 255 . 255 . 0 |
| 自ノード設定 / IPアドレス設定 / デフォルトゲートウェイ | （空欄） |
| 自ノード設定 / 交信データコード | バイナリ |
| 自ノード設定 / オープン方法の設定 | プログラムでOPENしない |

IPアドレス: 192.168.5.11
サブネットマスク: 255.255.255.0

2. [適用]ボタンをクリックします。
3. ”EtherNet/IP構成”にて，EtherNet/IPの通信パラメータを設定します。
   - [ナビゲーションウィンドウ]⇨[パラメータ]⇨[ユニット情報]⇨[FX5-EIP]⇨[EtherNet/IP構成(ユニット拡張パラメータ)]
4. ”コネクション設定”列の<詳細設定>をダブルクリックして，コネクションNo.1，コネクションNo.2のタグを設定します。

- タグ設定(コネクションNo.1)

【図】コネクション設定 画面 コネクションNo.1（原本 p.168）
- コネクション情報: コネクション数 2/64、通信処理性能(PPS) 0
- コネクション一覧(ユニット順): 自ノード ⇨ ターゲット / タグ ⇨ (001)、(002) / オリジネータ

| 項目名 | 設定値 | 単位 |
|---|---|---|
| コネクション名 | コネクション(Class3/UCMM タグ) | - |
| コネクションNo | 001 | - |
| コメント | （空欄） | - |
| データ型 | INT | - |
| タグ名 | Tag001 | - |
| タグ名文字数 | 6 | 文字 |
| サイズ | 10 | - |

- コネクションを追加する際”タグ”を選択して，[コネクション(Class3/UCMM タグ)]を選択します。
- タグデータタイプ: INT型(1ワード)
- タグ名: Tag001
- サイズ: 10

- タグ設定(コネクションNo.2)

【図】コネクション設定 画面 コネクションNo.2（原本 p.169）
- コネクション情報: コネクション数 2/64、通信処理性能(PPS) 0
- コネクション一覧: タグ ⇨ (002) を選択

| 項目名 | 設定値 | 単位 |
|---|---|---|
| コネクション名 | コネクション(Class3/UCMM タグ) | - |
| コネクションNo | 002 | - |
| コメント | （空欄） | - |
| データ型 | DINT | - |
| タグ名 | Tag002 | - |
| タグ名文字数 | 6 | 文字 |
| サイズ | 10 | - |

- コネクションを追加する際”タグ”を選択して，[コネクション(Class3/UCMM タグ)]を選択します。
- タグデータタイプ: DINT型(2ワード)
- タグ名: Tag002
- サイズ: 10

5. [適用]ボタンをクリックします。
6. [OK]ボタンをクリックして，コネクション設定を閉じます。
7. [設定を反映して閉じる]を選択し，”EtherNet/IP構成”画面を閉じます。
8. 設定したパラメータをサーバ側のCPUユニットに書き込み，CPUユニットをリセット，または電源をOFF→ONします。
   - [オンライン]⇨[シーケンサへの書込み]

#### プログラム例 (8.6 / 印刷 p.168 / 原本 p.170)

CPUユニットをSTOP→RUNすることで，Class3タグ通信のプログラムを実行します。

##### クライアント側のプログラム (8.6 / 印刷 p.168 / 原本 p.170)

| 分類 | ラベル名 | 内容 | デバイス |
|---|---|---|---|
| ユニットラベル | FX5EIP_1.bSts_CommunicationReady_D | 通信READY | U1￥G35.F |
| ユニットラベル | FX5EIP_1.stEIPArea64.uSet_CommunicationStart_D | EtherNet/IP通信起動要求 | U1￥G272 |
| ユニットラベル | FX5EIP_1.stEIPArea64.uSts_CommunicationStart_D | EtherNet/IP通信起動状態 | U1￥G273 |
| 定義するラベル | 下記のように，グローバルラベルを定義します。（下表） | | |
| 使用ファンクションブロック | • M+FX5-EIP_Class3Originator_WriteTagData<br>• M+FX5-EIP_Class3Originator_ReadTagData | | |

定義するラベル（グローバルラベル定義画面より。原本 p.170）

| No. | ラベル名 | データ型 | クラス | 割付け(デバイス/ラベル) | Japanese/日本語(表示対象) |
|---|---|---|---|---|---|
| 1 | bClass3_Tag_WriteCommandSendRequest | ビット | VAR_GLOBAL | M100 | Class3タグ Writeコマンド送信要求 |
| 2 | bClass3_Tag_ReadCommandSendRequest | ビット | VAR_GLOBAL | M101 | Class3タグ Readコマンド送信要求 |
| 3 | bRun_SendClass3_TagWrite | ビット | VAR_GLOBAL | M110 | Class3タグ Writeコマンド要求 実行中 |
| 4 | bOK_SendClass3_TagWrite | ビット | VAR_GLOBAL | M120 | Class3タグ Writeコマンド要求正常完了 |
| 5 | bNG_SendClass3_TagWrite | ビット | VAR_GLOBAL | M130 | Class3タグ Writeコマンド要求異常完了 |
| 6 | bRun_SendClass3_TagRead | ビット | VAR_GLOBAL | M111 | Class3タグ Readコマンド要求 実行中 |
| 7 | bOK_SendClass3_TagRead | ビット | VAR_GLOBAL | M121 | Class3タグ Readコマンド要求正常完了 |
| 8 | bNG_SendClass3_TagRead | ビット | VAR_GLOBAL | M131 | Class3タグ Readコマンド要求異常完了 |
| 9 | unSetClass3_Tag_WriteRequestData | ワード[符号なし]/ビット列[16ビット](0..706) | VAR_GLOBAL | D1000 | Class3タグ通信 Write要求データ格納 |
| 10 | unGetClass3_Tag_ReadResponseData | ワード[符号なし]/ビット列[16ビット](0..706) | VAR_GLOBAL | D2000 | Class3タグ通信 Read応答データ格納 |
| 11 | unSetRequestNo_Write | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D3100 | 要求No(Write) |
| 12 | unGetErrorCode_TagWrite | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D3101 | Class3タグ通信 Write エラーコード |
| 13 | unGetStatusErrorCode_TagWrite | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D3102 | Class3タグ通信 Write 通信エラーコード |
| 14 | unSetRequestNo_Read | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D3200 | 要求No(Read) |
| 15 | unGetErrorCode_TagRead | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D3201 | Class3タグ通信 Read エラーコード |
| 16 | unGetStatusErrorCode_TagRead | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D3202 | Class3タグ通信 Read 通信エラーコード |
| 17 | unGetResponseDataSize_TagRead | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D3204 | タグRead応答データサイズ |

> CPUユニットによって，デフォルトのラッチ範囲では，変換が通らないため，データレジスタ(D)のラッチ範囲を変更，またはデータレジスタ(D)を割り付けたラベルのクラスをVAR_GLOVAL_RETAINに定義してください。ラッチ設定については，下記を参照してください。
> 📖 MELSEC iQ-F FX5ユーザーズマニュアル(応用編)

【図】クライアント側ラダープログラム（原本 p.170-171）。ステップ (0)、(17)、(1158)、(2357) END。

※ニモニックは原本に記載なし。図から書き起こしたもの。FB呼出しは入出力の結線を列挙する形で記載。

```
; (0)
LD    FX5EIP_1.bSts_CommunicationReady_D                  ; U1\G35.F 通信READY (a接点)
MOV   H1   unSetRequestNo_Write                           ; D3100 ← H1
MOV   H2   unSetRequestNo_Read                            ; D3200 ← H2
MOV   H10  FX5EIP_1.stEIPArea64.uSet_CommunicationStart_D ; U1\G272 ← H10

; (17)
LD=_U H1   FX5EIP_1.stEIPArea64.uSts_CommunicationStart_D ; U1\G273 = H1
AND   bClass3_Tag_WriteCommandSendRequest                 ; M100 (a接点)
; FB: M_FX5_EIP_Class3Originator_WriteTagData_00A_1
;     (M+FX5-EIP_Class3Originator_WriteTagData_00A) "Class3 Originator Write tag data"
;   入力  B:   i_bEN        ← 上記接点の結果
;   入力  DUT: i_stModule   ← FX5EIP_1
;   入力  UW:  i_uWriteData ← unSetClass3_Tag_WriteRequestData (D1000)
;   入力  UW:  i_uRPI       ← H0
;   入力  UW:  i_uRequestNo ← unSetRequestNo_Write             (D3100)
;   出力  B:   o_bENO       → OUT bRun_SendClass3_TagWrite      (M110)
;   出力  B:   o_bOK        → OUT bOK_SendClass3_TagWrite       (M120)
;   出力  B:   o_bErr       → OUT bNG_SendClass3_TagWrite       (M130)
;   出力  UW:  o_uErrId     → unGetErrorCode_TagWrite           (D3101)
;   出力  UW:  o_uStatusId  → unGetStatusErrorCode_TagWrite     (D3102)
;   (FB下部表示: pbo_u2CIPResponseCode, pbo_udRequestCompleteCount)

; (1158)
LD=_U H1   FX5EIP_1.stEIPArea64.uSts_CommunicationStart_D ; U1\G273 = H1
AND   bClass3_Tag_ReadCommandSendRequest                  ; M101 (a接点)
; FB: M_FX5_EIP_Class3Originator_ReadTagData_00A_1
;     (M+FX5-EIP_Class3Originator_ReadTagData_00A) "Class3 Originator Read tag data"
;   入力  B:   i_bEN        ← 上記接点の結果
;   入力  DUT: i_stModule   ← FX5EIP_1
;   入力  UW:  i_uRPI       ← H0
;   入力  UW:  i_uRequestNo ← unSetRequestNo_Read              (D3200)
;   出力  B:   o_bENO       → OUT bRun_SendClass3_TagRead       (M111)
;   出力  B:   o_bOK        → OUT bOK_SendClass3_TagRead        (M121)
;   出力  B:   o_bErr       → OUT bNG_SendClass3_TagRead        (M131)
;   出力  UW:  o_uErrId     → unGetErrorCode_TagRead            (D3201)
;   出力  UW:  o_uStatusId  → unGetStatusErrorCode_TagRead      (D3202)
;   出力  UW:  o_uReadData  → unGetClass3_Tag_ReadResponseData  (D2000)
;   出力  UW:  o_uDataSize  → unGetResponseDataSize_TagRead     (D3204)
;   (FB上部/下部表示: pbo_u2CIPResponseCode, pbo_udRequestCompleteCount)

; (2357)
END
```

- (0) Class3タグ通信するための要求No.を設定して，EtherNet/IP通信を開始します。
- (17) M100をONすることで，M+FX5-EIP_Class3Originator_WriteTagDataが実行されて，Write要求をサーバ側に送信します。
  M120がONのとき，サーバ側のTag001に対して，D1000以降に格納したデータをClass3通信用パラメータとして設定したサイズ分書き込みます。
- (1158) M101をONすることで，M+FX5-EIP_Class3Originator_ReadTagDataが実行されて，Read要求をサーバ側に送信します。
  M121がONのとき，サーバ側の応答結果をD3204に格納された応答データサイズ分，D2000以降に格納されます。

> **Point**
> 設定する要求No.は，他のUCMM通信/Class1通信/Class3通信で使用する要求No.と重複しないよう注意してください。

##### サーバ側のプログラム (8.6 / 印刷 p.170 / 原本 p.172)

| 分類 | ラベル名 | 内容 | デバイス |
|---|---|---|---|
| ユニットラベル | FX5EIP_1.bSts_CommunicationReady_D | 通信READY | U1￥G35.F |
| ユニットラベル | FX5EIP_1.stEIPArea64.uSet_CommunicationStart_D | EtherNet/IP通信起動要求 | U1￥G272 |
| ユニットラベル | FX5EIP_1.stEIPArea64.uSts_CommunicationStart_D | EtherNet/IP通信起動状態 | U1￥G273 |
| ユニットラベル | FX5EIP_1.stEIPArea64.unVal_InputDataSize_Connection_D[unReadWrite_ConnectionNo] | 入力データサイズ | U1￥G304~U1￥G367 |
| ユニットラベル | FX5EIP_1.stEIPArea64.unVal_OutputDataSize_Connection_D[unReadWrite_ConnectionNo] | 出力/メッセージ通信(サーバ)データサイズ | U1￥G432~U1￥G495 |
| ユニットラベル | FX5EIP_1.stEIPArea64.stnAreaInputDataArea64[unReadWrite_ConnectionNo].unInputData | 入力データエリア | U1￥G16944～U1￥G63151 |
| ユニットラベル | FX5EIP_1.stEIPArea64.stnAreaOutputDataArea64[unReadWrite_ConnectionNo].unOutputData | 出力/メッセージ通信(サーバ)データエリア | U1￥G63152～U1￥G109359 |
| 定義するラベル | 下記のように，グローバルラベルを定義します。（下表） | | |

定義するラベル（グローバルラベル定義画面より。原本 p.172）

| No. | ラベル名 | データ型 | クラス | 割付け(デバイス/ラベル) | Japanese/日本語(表示対象) |
|---|---|---|---|---|---|
| 1 | bReadSTOP | ビット | VAR_GLOBAL | M11 | Read更新停止要求 |
| 2 | bWriteSTOP | ビット | VAR_GLOBAL | M12 | Write更新停止要求 |
| 3 | unReadWrite_ConnectionNo | ワード[符号付き] | VAR_GLOBAL | D300 | Read/WriteコネクションNo |
| 4 | unSetTag_WriteData | ワード[符号なし]/ビット列[16ビット](0..721) | VAR_GLOBAL | D1000 | 現在値更新データ |
| 5 | unGetTag_ReadData | ワード[符号なし]/ビット列[16ビット](0..721) | VAR_GLOBAL | D2000 | 現在値取得データ |

> CPUユニットによって，デフォルトのラッチ範囲では，変換が通らないため，データレジスタ(D)のラッチ範囲を変更，またはデータレジスタ(D)を割り付けたラベルのクラスをVAR_GLOVAL_RETAINに定義してください。ラッチ設定については，下記を参照してください。
> 📖 MELSEC iQ-F FX5ユーザーズマニュアル(応用編)

【図】サーバ側ラダープログラム（原本 p.172）。ステップ (0)、(9)、(62)、(115) END。

※ニモニックは原本に記載なし。図から書き起こしたもの。

```
; (0)
LD    FX5EIP_1.bSts_CommunicationReady_D                  ; U1\G35.F 通信READY (a接点)
MOV   H10  FX5EIP_1.stEIPArea64.uSet_CommunicationStart_D ; U1\G272 ← H10

; (9)
LD=_U H1   FX5EIP_1.stEIPArea64.uSts_CommunicationStart_D ; U1\G273 = H1
ANI   bReadSTOP                                           ; M11 (b接点)
MOV   H1   unReadWrite_ConnectionNo                       ; D300 ← H1
BMOV  FX5EIP_1.stEIPArea64.stnAreaOutputDataArea64[unReadWrite_ConnectionNo].unOutputData
      unGetTag_ReadData                                   ; D2000
      FX5EIP_1.stEIPArea64.unVal_OutputDataSize_Connection_D[unReadWrite_ConnectionNo]  ; 転送点数

; (62)
LD=_U H1   FX5EIP_1.stEIPArea64.uSts_CommunicationStart_D ; U1\G273 = H1
ANI   bWriteSTOP                                          ; M12 (b接点)
MOV   H2   unReadWrite_ConnectionNo                       ; D300 ← H2
BMOV  unSetTag_WriteData                                  ; D1000
      FX5EIP_1.stEIPArea64.stnAreaOutputDataArea64[unReadWrite_ConnectionNo].unOutputData
      FX5EIP_1.stEIPArea64.unVal_OutputDataSize_Connection_D[unReadWrite_ConnectionNo]  ; 転送点数

; (115)
END
```

- (0) EtherNet/IP通信を開始します。
- (9) 現在値を読み出したいタグに設定されたコネクションNo.を指定し，指定したタグに設定されたデータをD2000にコピーします。
- (62) 現在値を更新したいタグに設定されたコネクションNo.を指定し，指定したタグに設定されたデータをD1000に設定したデータに更新します。

### 8.7 PINGテストのプログラム例 (8.7 / 印刷 p.171 / 原本 p.173)

PINGテストのプログラム例を示します。

#### システム構成 (8.7 / 印刷 p.171 / 原本 p.173)

PINGテストのプログラム例は，下記のシステム構成を使用して説明します。
各FX5-EIPは”最大コネクション数設定”が64に設定されているものとします。

【図】PINGテストのシステム構成（原本 p.173）
- サーバ: 192.168.0.5（FX5-EIP装着のCPUユニット）
- EtherNet/IP機器: 192.168.0.2
- スイッチングハブ経由で接続。サーバ→EtherNet/IP機器に (1)、EtherNet/IP機器→サーバに (2)

(1) エコー要求
(2) エコー応答

#### 通信内容 (8.7 / 印刷 p.171 / 原本 p.173)

FX5-EIPからEtherNet/IP機器に対してエコー要求を送信して，EtherNet/IP機器からエコー応答を受信できるかPINGテストを行います。
PINGテストはFX5-EIPのバッファメモリを使用して，プログラムを動作させます。
下記にPINGテストで使用するバッファメモリを示します。

| アドレス | 項目 | 項目(詳細) | 参照先 |
|---|---|---|---|
| Un￥G240 | PINGテスト要求エリア | 交信タイムチェック | ☞ 232ページ PINGテスト要求エリア |
| Un￥G241 | PINGテスト要求エリア | 送信回数 | ☞ 232ページ PINGテスト要求エリア |
| Un￥G242~Un￥G243 | PINGテスト要求エリア | IP Address | ☞ 232ページ PINGテスト要求エリア |
| Un￥G244 | PINGテスト応答エリア | 総パケット送信回数 | ☞ 232ページ PINGテスト応答エリア |
| Un￥G245 | PINGテスト応答エリア | 受信回数 | ☞ 232ページ PINGテスト応答エリア |
| Un￥G246 | PINGテスト応答エリア | 損失回数 | ☞ 232ページ PINGテスト応答エリア |
| Un￥G247~Un￥G256 | PINGテスト応答エリア | エラーコード | ☞ 232ページ PINGテスト応答エリア |

#### パラメータ設定 (8.7 / 印刷 p.172 / 原本 p.174)

エンジニアリングツールをCPUユニットに接続し，パラメータを設定します。

1. IPアドレスを設定します。
   - ナビゲーションウィンドウ⇨[パラメータ]⇨[ユニット情報]⇨[FX5-EIP]⇨[ユニットパラメータ]⇨[基本設定]

【図】基本設定 画面（原本 p.174）

| 項目 | 設定 |
|---|---|
| 自ノード設定 / IPアドレス設定 / IPアドレス | 192 . 168 . 0 . 5 |
| 自ノード設定 / IPアドレス設定 / サブネットマスク | 255 . 255 . 255 . 0 |
| 自ノード設定 / IPアドレス設定 / デフォルトゲートウェイ | （空欄） |
| 自ノード設定 / 交信データコード | バイナリ |
| 自ノード設定 / オープン方法の設定 | プログラムでOPENしない |

IPアドレス: 192.168.0.5
サブネットマスク: 255.255.255.0

2. [適用]ボタンをクリックします。
3. 設定したパラメータをCPUユニットに書き込み，CPUユニットをリセット，または電源をOFF→ONします。
   - [オンライン]⇨[シーケンサへの書込み]

> **Point**
> プログラム例では，上記手順で示すパラメータ以外の設定はデフォルトを使用します。パラメータについては，下記を参照してください。
> ☞ 87ページ パラメータ設定

#### プログラム例 (8.7 / 印刷 p.173 / 原本 p.175)

PINGテスト要求指令をONすることで，PINGテストを実行します。

| 分類 | ラベル名 | 内容 | デバイス |
|---|---|---|---|
| ユニットラベル | FX5EIP_1.bSts_PingTestComplete_D | PINGテスト完了 | U1￥G35.2 |
| ユニットラベル | FX5EIP_1.bSts_CommunicationReady_D | 通信READY | U1￥G35.F |
| ユニットラベル | FX5EIP_1.bSet_PingTestRequest_D | PINGテスト実行要求 | U1￥G37.2 |
| ユニットラベル | FX5EIP_1.stEIPArea64.uSet_PingTestRequest_CommunicationTimeCheck_D | PINGテスト要求エリア 交信タイムチェック | U1￥G240 |
| ユニットラベル | FX5EIP_1.stEIPArea64.uSet_PingTestRequest_TransmissionsCount_D | PINGテスト要求エリア 送信回数 | U1￥G241 |
| ユニットラベル | FX5EIP_1.stEIPArea64.unSet_PingTestRequest_IPAddress_D[0] | PINGテスト要求エリア IP Address | U1￥G242 |
| ユニットラベル | FX5EIP_1.stEIPArea64.unSet_PingTestRequest_IPAddress_D[1] | PINGテスト要求エリア IP Address | U1￥G243 |
| ユニットラベル | FX5EIP_1.stEIPArea64.unArea_PingTestReceiveResulteArea_D[0] | PINGテスト応答結果エリア総パケット送信回数 | U1￥G244 |
| ユニットラベル | FX5EIP_1.stEIPArea64.unArea_PingTestReceiveResulteArea_D[1] | PINGテスト応答結果エリア受信回数 | U1￥G245 |
| ユニットラベル | FX5EIP_1.stEIPArea64.unArea_PingTestReceiveResulteArea_D[2] | PINGテスト応答結果エリア損失回数 | U1￥G246 |
| ユニットラベル | FX5EIP_1.stEIPArea64.unArea_PingTestReceiveResulteArea_D[unPINGtestErrorCodeCheck] | PINGテスト応答結果エリアエラーコード | U1￥G247~U1￥G256 |
| ユニットラベル | FX5EIP_1.stEIPArea64.uSet_CommunicationStart_D | EtherNet/IP通信起動要求 | U1￥G272 |
| ユニットラベル | FX5EIP_1.stEIPArea64.uSts_CommunicationStart_D | EtherNet/IP通信起動状態 | U1￥G273 |
| 定義するラベル | 下記のように，グローバルラベルを定義します。（下表） | | |

定義するラベル（グローバルラベル定義画面より。原本 p.175）

| No. | ラベル名 | データ型 | クラス | 割付け(デバイス/ラベル) | Japanese/日本語(表示対象) |
|---|---|---|---|---|---|
| 1 | bPingCommandRequest | ビット | VAR_GLOBAL | M0 | PINGテスト要求指令 |
| 2 | unPINGtestresultResult | ワード[符号なし]/ビット列[16ビット](0..2) | VAR_GLOBAL | D3000 | PINGテスト応答結果 |
| 3 | unPINGtestErrorCodeCheck | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D3003 | PINGテスト応答エラーコードチェック用変数 |
| 4 | unPINGtestresultErrorCode | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D3004 | PINGテスト応答エラーコード |
| 5 | bPingTesterror | ビット | VAR_GLOBAL | F0 | PINGテスト異常完了 |

> CPUユニットによって，デフォルトのラッチ範囲では，変換が通らないため，データレジスタ(D)のラッチ範囲を変更，またはデータレジスタ(D)を割り付けたラベルのクラスをVAR_GLOVAL_RETAINに定義してください。ラッチ設定については，下記を参照してください。
> 📖 MELSEC iQ-F FX5ユーザーズマニュアル(応用編)

【図】PINGテストのラダープログラム（原本 p.175-176）。ステップ (0)、(9)、(47)、(129) END。

※ニモニックは原本に記載なし。図から書き起こしたもの。

```
; (0)
LD    FX5EIP_1.bSts_CommunicationReady_D                  ; U1\G35.F 通信READY (a接点)
MOV   H10  FX5EIP_1.stEIPArea64.uSet_CommunicationStart_D ; U1\G272 ← H10

; (9)
LD    bPingCommandRequest                                 ; M0 PINGテスト要求指令 (a接点)
AND=_U H1  FX5EIP_1.stEIPArea64.uSts_CommunicationStart_D ; U1\G273 = H1
ANI   FX5EIP_1.bSet_PingTestRequest_D                     ; U1\G37.2 (b接点)
MOVP  K5   FX5EIP_1.stEIPArea64.uSet_PingTestRequest_CommunicationTimeCheck_D  ; U1\G240 ← K5
MOVP  K5   FX5EIP_1.stEIPArea64.uSet_PingTestRequest_TransmissionsCount_D      ; U1\G241 ← K5
MOVP  H2   FX5EIP_1.stEIPArea64.unSet_PingTestRequest_IPAddress_D[0]           ; U1\G242 ← H2
MOVP  H0C001 FX5EIP_1.stEIPArea64.unSet_PingTestRequest_IPAddress_D[1]         ; U1\G243 ← H0C001 (原本図の表記のまま)
SET   FX5EIP_1.bSet_PingTestRequest_D                     ; U1\G37.2

; (47)
LD    bPingCommandRequest                                 ; M0 (a接点)
AND   FX5EIP_1.bSts_PingTestComplete_D                    ; U1\G35.2 PINGテスト完了 (a接点)
MOVP  FX5EIP_1.stEIPArea64.unArea_PingTestReceiveResulteArea_D[1]  unPINGtestresultResult[0]  ; U1\G245 → D3000 (原本図の表記のまま)
MOVP  FX5EIP_1.stEIPArea64.unArea_PingTestReceiveResulteArea_D[1]  unPINGtestresultResult[1]  ; U1\G245 → D3001
MOVP  FX5EIP_1.stEIPArea64.unArea_PingTestReceiveResulteArea_D[2]  unPINGtestresultResult[2]  ; U1\G246 → D3002
MOVP  FX5EIP_1.stEIPArea64.unArea_PingTestReceiveResulteArea_D[0]  unPINGtestErrorCodeCheck   ; U1\G244 → D3003
+_U   K2   unPINGtestErrorCodeCheck                       ; D3003 ← D3003 + K2
MPS
AND<>_U FX5EIP_1.stEIPArea64.unArea_PingTestReceiveResulteArea_D[unPINGtestErrorCodeCheck]  H0
MOVP  FX5EIP_1.stEIPArea64.unArea_PingTestReceiveResulteArea_D[unPINGtestErrorCodeCheck]  unPINGtestresultErrorCode  ; → D3004
MRD
LD<>_U unPINGtestresultResult[2]  H0                      ; D3002 <> H0
OR<>_U unPINGtestresultErrorCode  H0                      ; D3004 <> H0
ANB
SET   bPingTesterror                                      ; F0
MRD
RST   FX5EIP_1.bSet_PingTestRequest_D                     ; U1\G37.2
MPP
RST   bPingCommandRequest                                 ; M0

; (129)
END
```

- (0) EtherNet/IP通信を開始します。
- (9) PINGテストの交信タイムチェック，送信回数，IPアドレスを指定して，PINGテストを開始します。
- (47) PINGテストの応答結果を格納します。(総パケット送信回数→D3000，受信回数→D3001，損失回数→D3002，エラーコード→D3004)
  タイムアウトまたはエラーが発生している場合，F0をONします。

## 転記時の要確認一覧 (第8章 8.5〜8.7 / 原本 p.158-176)

- 8.7 (9) の MOVP H0C001 → unSet_PingTestRequest_IPAddress_D[1] (U1￥G243)：原本図の表記どおり「H0C001」と転記。システム構成の相手IPアドレス 192.168.0.2 から想定される上位ワード（192.168 = HC0A8）と一致しないように見える。原本 p.175 で要確認。
- 8.7 (47) の 1行目 MOVP：原本図では転送元が `unArea_PingTestReceiveResulteArea_D[1]` / `U1￥G245` → D3000 と表記されている（2行目も同じ [1] / U1￥G245 → D3001）。説明文は「総パケット送信回数→D3000」で、表では総パケット送信回数 = [0] / U1￥G244。図のとおり転記した。原本 p.176 で要確認。
- 8.6 サーバ側 (9) の BMOV：現在値の読出しの転送元が原本図では `stnAreaOutputDataArea64[...]`（出力/メッセージ通信(サーバ)データエリア）。ユニットラベル表には入力データエリア/入力データサイズも載っているが、図中では使われていない。図のとおり転記（原本 p.172）。
- ニモニック中の MPS/MRD/MPP・ANB の分岐構造、FB呼出しの記法は図からの書き起こし（GX Works3 の実際のニモニック出力とは表記が異なる可能性あり）。
