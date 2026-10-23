# 三菱 MELSEC iQ-F FX5-EIP形 EtherNet/IPユニット ユーザーズマニュアル 第8章 プログラミング（8.3 UCMMインスタンス通信の交信例 / 8.4 UCMMタグ通信の交信例）

| 項目 | 内容 |
|---|---|
| 原本 | 三菱電機 MELSEC iQ-F FX5-EIP形EtherNet/IPユニットユーザーズマニュアル |
| 発行元 | 三菱電機株式会社 |
| 資料番号 / 版数 | SH-082708 / B版（PDFメタデータ subject: SH-082708-B） |
| 原本PDF | `PDF/MELSEC iQ-F FX5-EIP形EtherNet_IPユニットユーザーズマニュアル.pdf` (全274ページ) |
| 本ファイルの範囲 | 8.3〜8.4 (印刷 p.144-155 / PDF p.146-157) |
| ページ対応 | 「原本 p.」はPDFのページ番号、「印刷 p.」は原本フッタのページ番号。印刷ページ = PDFページ − 2。本文中の「〇〇ページ参照」は印刷ページ |
| 変換日 | 2026-10-23 |
| 変換方法 | pypdfium2(本文) + PyMuPDF 200dpi 画像の目視(全ページ)。ラベル定義表・ラダー図は 400dpi で拡大して目視 |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。

**転記上の扱い**: 原本の結合セルは各行に値を展開。セル内改行は `<br>`。図は【図】プレースホルダ＋読み取れる事実の箇条書き。GX Works3 の設定画面キャプチャは【図】＋画面上の項目名・設定値を箇条書き（または表）。グローバルラベル定義画面（キャプチャ）は表に書き起こし。ラダー図のニモニックは原本に記載がなく、図から書き起こしたもの（各所に注記）。ユニットFB呼出しはニモニック1行で表せないため、起動条件をニモニック、FBの入出力引数を表で示す。バッファメモリは本文・表では原本表記の `Un￥G`/`U1￥G`（全角￥）に統一、ニモニックのコードブロック内のみ GX Works3 入力形式の `U1￥G` と表記。見出しレベル: 章 `##` / 節 `###` / 項 `####` / ◆ `#####` / ■ `######`。

---

## 主要用語 対訳表 (Glossary) (8.3〜8.4 / 原本 p.146-157)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| UCMMインスタンス通信 | UCMM instance communication | UCMM = Unconnected Message Manager | 参考訳 |
| UCMMタグ通信 | UCMM tag communication | — | 参考訳 |
| クライアント | Client | — | 参考訳 |
| サーバ | Server | — | 参考訳 |
| 要求コマンド | Request command | — | 参考訳 |
| サービスコード | Service code | Service: 01H | 参考訳 |
| クラスID | Class ID | Class: 01H | 参考訳 |
| インスタンスID | Instance ID | Instance: 01H | 参考訳 |
| アトリビュートID | Attribute ID | Attribute: 00H | 参考訳 |
| Identityオブジェクト | Identity object | Class 01H | 参考訳 |
| 全アトリビュート取得 | Get_Attributes_All | Service 01H | 参考訳 |
| 最大コネクション数設定 | Maximum number of connections setting | — | 参考訳 |
| EtherNet/IP自動起動設定 | EtherNet/IP auto start setting | — | 参考訳 |
| EtherNet/IP構成 | EtherNet/IP configuration | ユニット拡張パラメータ | 参考訳 |
| コネクション設定 | Connection setting | — | 参考訳 |
| コネクション(Class3/UCMM タグ) | Connection (Class3/UCMM tag) | — | 参考訳 |
| 通信READY | Communication READY | U1￥G35.F | 参考訳 |
| EtherNet/IP通信起動要求 | EtherNet/IP communication start request | U1￥G272 | 参考訳 |
| EtherNet/IP通信起動状態 | EtherNet/IP communication start status | U1￥G273 | 参考訳 |
| メッセージ通信要求エリア Path Segment | Message communication request area Path Segment | U1￥G4665 / U1￥G4857 | 参考訳 |
| 入力データエリア | Input data area | U1￥G16944~U1￥G63151 | 参考訳 |
| 出力/メッセージ通信(サーバ)データエリア | Output/message communication (server) data area | U1￥G63152~U1￥G109359 | 参考訳 |
| 入力データサイズ | Input data size | U1￥G304~U1￥G367 | 参考訳 |
| 出力/メッセージ通信(サーバ)データサイズ | Output/message communication (server) data size | U1￥G432~U1￥G495 | 参考訳 |
| ユニットラベル | Module label | — | 参考訳 |
| グローバルラベル | Global label | VAR_GLOBAL | 参考訳 |
| ラッチ範囲 | Latch range | VAR_GLOVAL_RETAIN（原文表記） | 参考訳 |
| ユニットFB | Module FB | M+FX5-EIP_UCMMOriginator_MessageSend / _WriteTagData / _ReadTagData | 参考訳 |
| 要求No. | Request No. | — | 参考訳 |
| 宛先IPアドレス | Destination IP address | i_u2TargetAddress | 参考訳 |
| 応答データサイズ | Response data size | o_uResponseSize / o_uDataSize | 参考訳 |
| 読出し要求データサイズ | Read request data size | i_uDataSize | 参考訳 |
| 読出し要求タグデータタイプ | Read request tag data type | i_uDataType | 参考訳 |
| Write要求 / Read要求 | Write request / Read request | — | 参考訳 |
| タグ名 | Tag name | i_snTagName | 参考訳 |
| データの泣き別れ | Data inconsistency (split data) | — | 参考訳 |
| 現在値 | Current value | — | 参考訳 |

## 変換範囲表 (8.3〜8.4 / 原本 p.146-157)

| 原本ページ | 節 | 扱い |
|---|---|---|
| p.146-149 | 8.3 UCMMインスタンス通信の交信例 | 全文(プログラム例を含む) |
| p.150-157 | 8.4 UCMMタグ通信の交信例 | 全文(プログラム例を含む) |
| 上記以外 | 他章・他節 | 同フォルダの他ファイル参照 |

## 目次 (8.3〜8.4)

- [8 プログラミング（続き）](#8-プログラミング続き-8--印刷-p144-155--原本-p146-157)
  - [8.3 UCMMインスタンス通信の交信例](#83-ucmmインスタンス通信の交信例-83--印刷-p144--原本-p146)
    - システム構成 / パラメータ設定 / プログラム例
  - [8.4 UCMMタグ通信の交信例](#84-ucmmタグ通信の交信例-84--印刷-p148--原本-p150)
    - システム構成 / 通信内容 / パラメータ設定 / プログラム例

## 8 プログラミング（続き） (8 / 印刷 p.144-155 / 原本 p.146-157)

### 8.3 UCMMインスタンス通信の交信例 (8.3 / 印刷 p.144 / 原本 p.146)

FX5-EIP間でUCMMインスタンス通信を行う例を示します。

#### システム構成 (8.3 / 印刷 p.144 / 原本 p.146)

UCMMインスタンス通信の交信例は，下記のシステム構成を使用して説明します。
各FX5-EIPは”最大コネクション数設定”が64に設定されているものとします。

【図】システム構成（原本 p.146）
- クライアント: 192.168.0.5（FX5U CPU＋FX5-EIP）
- サーバ: 192.168.0.6（FX5U CPU＋FX5-EIP）
- 両者はスイッチングハブ経由でEthernet接続
- 矢印: クライアント → サーバ に「要求コマンド」

###### ■要求コマンド (8.3 / 印刷 p.144 / 原本 p.146)

- Service: 01H (Get_Attributes_All)
- Class: 01H (Identityオブジェクト)
- Attribute: 00H
- Instance: 01H

#### パラメータ設定 (8.3 / 印刷 p.144 / 原本 p.146)

エンジニアリングツールを使用してパラメータを設定します。

> **Point**
> プログラム例では，設定手順で示すパラメータ以外の設定はデフォルトを使用します。パラメータについては，下記を参照してください。
> 87ページ パラメータ設定

##### FX5-EIP(クライアント)の設定 (8.3 / 印刷 p.144 / 原本 p.146)

エンジニアリングツールをクライアント側のCPUユニットに接続し，パラメータを設定します。

1. IPアドレスを設定します。
   - ナビゲーションウィンドウ⇒[パラメータ]⇒[ユニット情報]⇒[FX5-EIP]⇒[ユニットパラメータ]⇒[基本設定]

【図】設定項目画面（自ノード設定）（原本 p.146）

| 項目 | 設定 |
|---|---|
| 自ノード設定 > IPアドレス設定 > IPアドレス | 192.168.0.5 |
| 自ノード設定 > IPアドレス設定 > サブネットマスク | 255.255.255.0 |
| 自ノード設定 > IPアドレス設定 > デフォルトゲートウェイ | （空欄） |
| 自ノード設定 > 交信データコード | バイナリ |
| 自ノード設定 > オープン方法の設定 | プログラムでOPENしない |

IPアドレス: 192.168.0.5
サブネットマスク: 255.255.255.0

2. [適用]ボタンをクリックします。
3. 設定したパラメータをクライアント側のCPUユニットに書き込み，CPUユニットをリセット，または電源をOFF→ONします。
   - [オンライン]⇒[シーケンサへの書込み]

> **Point**
> UCMMインスタンス通信では，”EtherNet/IP構成”によるパラメータ設定は不要です。

##### FX5-EIP(サーバ)の設定 (8.3 / 印刷 p.145 / 原本 p.147)

エンジニアリングツールをサーバ側のCPUユニットに接続し，パラメータを設定します。

1. IPアドレスを設定します。
   - ナビゲーションウィンドウ⇒[パラメータ]⇒[ユニット情報]⇒[FX5-EIP]⇒[ユニットパラメータ]⇒[基本設定]

【図】設定項目画面（自ノード設定）（原本 p.147）

| 項目 | 設定 |
|---|---|
| 自ノード設定 > IPアドレス設定 > IPアドレス | 192.168.0.6 |
| 自ノード設定 > IPアドレス設定 > サブネットマスク | 255.255.255.0 |
| 自ノード設定 > IPアドレス設定 > デフォルトゲートウェイ | （空欄） |
| 自ノード設定 > 交信データコード | バイナリ |
| 自ノード設定 > オープン方法の設定 | プログラムでOPENしない |

IPアドレス: 192.168.0.6
サブネットマスク: 255.255.255.0

2. ”EtherNet/IP自動起動設定”を”起動する”に設定します。
   - ナビゲーションウィンドウ⇒[パラメータ]⇒[ユニット情報]⇒[FX5-EIP]⇒[ユニットパラメータ]⇒[基本設定]

【図】設定項目画面（EtherNet/IP設定）（原本 p.147）

| 項目 | 設定 |
|---|---|
| EtherNet/IP設定 > 最大コネクション数設定 > 最大コネクション数設定 | 64コネクション |
| EtherNet/IP設定 > リフレッシュ設定 > リフレッシュ設定 | <詳細設定> |
| EtherNet/IP設定 > EtherNet/IP自動起動設定 > EtherNet/IP自動起動設定 | 起動する |

> **Point**
> 本項目を設定しない場合，クライアント側のプログラムと同様の方法でEtherNet/IP通信起動要求に0以外を設定してください。
> 146ページ クライアント側のプログラム

3. [適用]ボタンをクリックします。
4. 設定したパラメータをサーバ側のCPUユニットに書き込み，CPUユニットをリセット，または電源をOFF→ONします。
   - [オンライン]⇒[シーケンサへの書込み]

> **Point**
> UCMMインスタンス通信では，”EtherNet/IP構成”によるパラメータ設定は不要です。

#### プログラム例 (8.3 / 印刷 p.146 / 原本 p.148)

プログラム内のUCMMコマンド送信要求をONすることで，UCMMインスタンス通信を実行します。
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

##### クライアント側のプログラム (8.3 / 印刷 p.146 / 原本 p.148)

| 分類 | ラベル名 | 内容 | デバイス |
|---|---|---|---|
| ユニットラベル | FX5EIP_1.bSts_CommunicationReady_D | 通信READY | U1￥G35.F |
| ユニットラベル | FX5EIP_1.stEIPArea64.uSet_CommunicationStart_D | EtherNet/IP通信起動要求 | U1￥G272 |
| ユニットラベル | FX5EIP_1.stEIPArea64.uSts_CommunicationStart_D | EtherNet/IP通信起動状態 | U1￥G273 |
| 定義するラベル | 下記のように，グローバルラベルを定義します。 | （下表） | — |
| 使用ファンクションブロック | M+FX5-EIP_UCMMOriginator_MessageSend | — | — |

定義するラベル（グローバルラベル定義画面から書き起こし、原本 p.148）

| No. | ラベル名 | データ型 | クラス | 割付け(デバイス/ラベル) | Japanese/日本語(表示対象) |
|---|---|---|---|---|---|
| 1 | bUCMM_MessageCommandSendRequest | ビット | VAR_GLOBAL | M100 | UCMMメッセージコマンド送信要求 |
| 2 | bRun_SendUCMM_Message | ビット | VAR_GLOBAL | M110 | UCMMメッセージコマンド要求実行中 |
| 3 | bOK_SendUCMM_Message | ビット | VAR_GLOBAL | M120 | UCMMメッセージコマンド要求正常完了 |
| 4 | bNG_SendUCMM_Message | ビット | VAR_GLOBAL | M130 | UCMMメッセージコマンド要求異常完了 |
| 5 | unSetUCMM_MessageRequestData | ワード[符号なし]/ビット列[16ビット](0..706) | VAR_GLOBAL | D1000 | UCMMメッセージ通信要求データ格納 |
| 6 | unGetUCMM_MessageResponseData | ワード[符号なし]/ビット列[16ビット](0..706) | VAR_GLOBAL | D2000 | UCMMメッセージ通信応答データ格納 |
| 7 | unSetIPAddress | ワード[符号なし]/ビット列[16ビット](0..1) | VAR_GLOBAL | D3000 | 宛先IPアドレス |
| 8 | unSetRequestNo | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D3002 | 要求No |
| 9 | unGetErrorCode | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D3003 | エラーコード |
| 10 | unGetStatusErrorCode | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D3004 | 通信エラーコード |
| 11 | unGetResponseDataSize | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D3005 | 応答データサイズ |

（定義するラベル欄の注記・原文）
> CPUユニットによって，デフォルトのラッチ範囲では，変換が通らないため，データレジスタ(D)のラッチ範囲を変更，またはデータレジスタ(D)を割り付けたラベルのクラスをVAR_GLOVAL_RETAINに定義してください。ラッチ設定については，下記を参照してください。
> MELSEC iQ-F FX5ユーザーズマニュアル(応用編)
> 応答データの格納先は，サーバとなるEtherNet/IP機器のマニュアルを参照し，十分なデータサイズを確保してください。

【図】クライアント側のプログラム（ラダー図）（原本 p.148-149）

※ニモニックは原本に記載なし。図から書き起こしたもの

```
; (0)
LD     U1\G35.F                 ; FX5EIP_1.bSts_CommunicationReady_D 通信READY
MOV    H1      D3002            ; unSetRequestNo
MOV    H6      D3000            ; unSetIPAddress[0]
MOV    H0C0A8  D3001            ; unSetIPAddress[1]
MOV    H10     U1\G272          ; FX5EIP_1.stEIPArea64.uSet_CommunicationStart_D
; (22)
LD=_U  K1      U1\G273          ; FX5EIP_1.stEIPArea64.uSts_CommunicationStart_D
AND    M100                     ; bUCMM_MessageCommandSendRequest (a接点)
       ; → ユニットFB M_FX5_EIP_UCMMOriginator_MessageSend_00A_1 の B: i_bEN（下表）
; (1640)
END
```

ユニットFB: インスタンス `M_FX5_EIP_UCMMOriginator_MessageSend_00A_1`（M+FX5-EIP_UCMMOriginator_MessageSend_00A / UCMM Originator Message Send）（ステップ(22)）

| 入出力 | 引数 | 接続（ラベル / デバイス / 定数） |
|---|---|---|
| 入力 | B: i_bEN | 起動条件（=_U K1 U1￥G273 かつ M100） |
| 入力 | DUT: i_stModule | FX5EIP_1 |
| 入力 | UW: i_u2TargetAddress | unSetIPAddress / D3000 |
| 入力 | UW: i_uRequestData | unSetUCMM_MessageRequestData / D1000 |
| 入力 | UW: i_uRequestDataSize | K0 |
| 入力 | UW: i_uService | H1 |
| 入力 | UW: i_uClass | H1 |
| 入力 | UW: i_uInstance | H1 |
| 入力 | UW: i_uAttribute | H0 |
| 入力 | UW: i_uRPI | H0C8 |
| 入力 | UW: i_uTrigger | H0 |
| 入力 | UW: i_uRequestNo | unSetRequestNo / D3002 |
| 出力 | o_bENO :B | bRun_SendUCMM_Message / M110 |
| 出力 | o_bOK :B | bOK_SendUCMM_Message / M120 |
| 出力 | o_bErr :B | bNG_SendUCMM_Message / M130 |
| 出力 | o_uErrId :UW | unGetErrorCode / D3003 |
| 出力 | o_uStatusId :UW | unGetStatusErrorCode / D3004 |
| 出力 | o_uResponseData :UW | unGetUCMM_MessageResponseData / D2000 |
| 出力 | o_uResponseSize :UW | unGetResponseDataSize / D3005 |
| 公開変数（FB内表示） | pbo_u2CIPResponseCode | （接続なし） |
| 公開変数（FB内表示） | pbo_udRequestCompleteCount | （接続なし） |

プログラムの説明（原文）
> (0) UCMMメッセージ通信するための要求No.および宛先IPアドレスを設定して，EtherNet/IP通信を開始します。
> (22) M100をONすることで，M+FX5-EIP_UCMMOriginator_MessageSendが実行されて，要求データをサーバ側に送信します。
> 正常に応答を受信すると，M120がONされ，サーバ側からの応答結果がD2000以降に格納されます。(D3005に格納された応答データサイズ÷2(バイト)分が格納されます(切上げ))
> 応答データサイズが奇数の場合は，最終デバイスの下位1バイトのみデータが格納されます。

> **Point**
> 設定する要求No.は，Class3通信で使用するコネクションNo.や，他のUCMM通信/Class1通信/Class3通信で使用する要求No.と重複しないよう注意してください。

### 8.4 UCMMタグ通信の交信例 (8.4 / 印刷 p.148 / 原本 p.150)

FX5-EIP間でUCMMタグ通信を行う例を示します。

#### システム構成 (8.4 / 印刷 p.148 / 原本 p.150)

UCMMタグ通信の交信例は，下記のシステム構成を使用して説明します。
各FX5-EIPは”最大コネクション数設定”が64に設定されているものとします。

【図】システム構成（原本 p.150）
- クライアント: 192.168.1.5（FX5U CPU＋FX5-EIP）
- サーバ: 192.168.1.6（FX5U CPU＋FX5-EIP）
- 両者はスイッチングハブ経由でEthernet接続
- 矢印: クライアント → サーバ に「Write要求」と「Read要求」

###### ■Write要求 (8.4 / 印刷 p.148 / 原本 p.150)

- タグ名: Tag001
- タグタイプ: INT型
- サイズ: 10+要求データ(10ワード分)

###### ■Read要求 (8.4 / 印刷 p.148 / 原本 p.150)

- タグ名: Tag002
- タグタイプ: DINT型
- サイズ: 10

#### 通信内容 (8.4 / 印刷 p.148 / 原本 p.150)

UCMMタグ通信の交信例を実行すると，下記の動作を実行します。

##### クライアント側の動作 (8.4 / 印刷 p.148 / 原本 p.150)

###### ■タグへのWrite要求 (8.4 / 印刷 p.148 / 原本 p.150)

UCMMタグ通信のWrite要求を実行することで，サーバ側のTag001のタグに対して，D1000以降に格納したデバイスエリアのデータを要求サイズ分書き込みます。*1

*1 要求したデータタイプがINT型の場合，要求データサイズ×1ワード(プログラム例では10ワード)の要求データが送信されます。
要求したデータタイプがDINT型の場合，要求データサイズ×2ワードの要求データが送信されます。

###### ■タグのRead要求 (8.4 / 印刷 p.148 / 原本 p.150)

UCMMタグ通信のRead要求を実行することで，サーバ側のTag002のタグに設定したデータを要求データサイズ分読み出します。読み出されたデータから，読出しデータサイズ(D3204に格納されるサイズ)分をD2000以降に格納します。
(読出しデータサイズは，相手機器のタグのデータ型に関わらず，受信したデータサイズがワード単位で格納されます)
また，相手機器のタグから読み出されるデータのサイズは，ユニットFBの出力引数(i_uDataSize)に設定された読出し要求データサイズと，相手機器のタグのデータ型(D3203に格納される値)に依存します。*1*2

*1 相手機器のタグのデータ型がINT型の場合，読出し要求データサイズ×1ワードを読み出します。
相手機器のタグのデータ型がDINT型の場合，読出し要求データサイズ×2ワードを読み出します。
*2 ユニットFBの入力引数(i_uDataType)に設定された読出し要求タグデータタイプは，要求送信時のパラメータチェックに使用します。
読み出した相手機器のタグのデータ型と異なっている場合，要求したタグ名やデータサイズが意図した内容になっているか確認ください。

##### サーバ側の動作 (8.4 / 印刷 p.148 / 原本 p.150)

Tag001およびTag002に設定されたタグデータの現在値の読出しや，現在値の更新を行います。
サーバ側が動作する際，タグに対するクライアント側からのRead/Write要求はどちらも受付け可能です。
ただし，現在値の読出し中にWrite要求を受けデータが更新される場合や，現在値の更新中のデータがRead要求により読み出される場合に，データの泣き別れが発生する場合があります。

#### パラメータ設定 (8.4 / 印刷 p.149 / 原本 p.151)

エンジニアリングツールを使用してパラメータを設定します。

> **Point**
> プログラム例では，設定手順で示すパラメータ以外の設定はデフォルトを使用します。パラメータについては，下記を参照してください。
> 87ページ パラメータ設定

##### FX5-EIP(クライアント)の設定 (8.4 / 印刷 p.149 / 原本 p.151)

エンジニアリングツールをクライアント側のCPUユニットに接続し，パラメータを設定します。

1. IPアドレスを設定します。
   - ナビゲーションウィンドウ⇒[パラメータ]⇒[ユニット情報]⇒[FX5-EIP]⇒[ユニットパラメータ]⇒[基本設定]

【図】設定項目画面（自ノード設定）（原本 p.151）

| 項目 | 設定 |
|---|---|
| 自ノード設定 > IPアドレス設定 > IPアドレス | 192.168.1.5 |
| 自ノード設定 > IPアドレス設定 > サブネットマスク | 255.255.255.0 |
| 自ノード設定 > IPアドレス設定 > デフォルトゲートウェイ | （空欄） |
| 自ノード設定 > 交信データコード | バイナリ |
| 自ノード設定 > オープン方法の設定 | プログラムでOPENしない |

IPアドレス: 192.168.1.5
サブネットマスク: 255.255.255.0

2. [適用]ボタンをクリックします。
3. 設定したパラメータをクライアント側のCPUユニットに書き込み，CPUユニットをリセット，または電源をOFF→ONします。
   - [オンライン]⇒[シーケンサへの書込み]

> **Point**
> UCMMタグ通信では，”EtherNet/IP構成”によるパラメータ設定は不要です。

##### FX5-EIP(サーバ)の設定 (8.4 / 印刷 p.149-151 / 原本 p.151-153)

エンジニアリングツールをサーバ側のCPUユニットに接続し，パラメータを設定します。

1. IPアドレスを設定します。
   - ナビゲーションウィンドウ⇒[パラメータ]⇒[ユニット情報]⇒[FX5-EIP]⇒[ユニットパラメータ]⇒[基本設定]

【図】設定項目画面（自ノード設定）（原本 p.151）

| 項目 | 設定 |
|---|---|
| 自ノード設定 > IPアドレス設定 > IPアドレス | 192.168.1.6 |
| 自ノード設定 > IPアドレス設定 > サブネットマスク | 255.255.255.0 |
| 自ノード設定 > IPアドレス設定 > デフォルトゲートウェイ | （空欄） |
| 自ノード設定 > 交信データコード | バイナリ |
| 自ノード設定 > オープン方法の設定 | プログラムでOPENしない |

IPアドレス: 192.168.1.6
サブネットマスク: 255.255.255.0

2. [適用]ボタンをクリックします。
3. ”EtherNet/IP構成”にて，EtherNet/IPの通信パラメータを設定します。
   - ナビゲーションウィンドウ⇒[パラメータ]⇒[ユニット情報]⇒[FX5-EIP]⇒[EtherNet/IP構成(ユニット拡張パラメータ)]
4. ”コネクション設定”列の<詳細設定>をダブルクリックして，コネクションNo.1，コネクションNo.2のタグを設定します。

- タグ設定(コネクションNo.1)（原本 p.152）

【図】コネクション設定画面（コネクションNo.1）（原本 p.152）
- コネクション情報: コネクション数 2/64、通信処理性能(PPS) 0
- コネクション一覧(ユニット順): 自ノード > ターゲット / タグ > (001)【選択中】, (002) / オリジネータ
- Error:0 / Warning:0 / Information:0

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
- タグ名: Tag001
- データ型: INT型(1ワード)
- サイズ: 10

- タグ設定(コネクションNo.2)（原本 p.153）

【図】コネクション設定画面（コネクションNo.2）（原本 p.153）
- コネクション情報: コネクション数 2/64、通信処理性能(PPS) 0
- コネクション一覧(ユニット順): 自ノード > ターゲット / タグ > (001), (002)【選択中】 / オリジネータ
- Error:0 / Warning:0 / Information:0

| 項目名 | 設定値 | 単位 |
|---|---|---|
| コネクション名 | コネクション(Class3/UCMM タグ) | - |
| コネクションNo | 002 | - |
| コメント | （空欄） | - |
| データ型 | INT（画面表示のまま。下記本文はDINT型。要確認） | - |
| タグ名 | Tag002 | - |
| タグ名文字数 | 6 | 文字 |
| サイズ | 10 | - |

- コネクションを追加する際”タグ”を選択して，[コネクション(Class3/UCMM タグ)]を選択します。
- タグ名: Tag002
- データ型: DINT型(2ワード)
- サイズ: 10

5. [適用]ボタンをクリックします。
6. [OK]ボタンをクリックして，コネクション設定を閉じます。
7. [設定を反映して閉じる]を選択し，”EtherNet/IP構成”画面を閉じます。
8. 設定したパラメータをサーバ側のCPUユニットに書き込み，CPUユニットをリセット，または電源をOFF→ONします。
   - [オンライン]⇒[シーケンサへの書込み]

#### プログラム例 (8.4 / 印刷 p.152 / 原本 p.154)

CPUユニットをSTOP→RUNすることで，UCMMタグ通信のプログラムを実行します。

##### クライアント側のプログラム (8.4 / 印刷 p.152-154 / 原本 p.154-156)

| 分類 | ラベル名 | 内容 | デバイス |
|---|---|---|---|
| ユニットラベル | FX5EIP_1.bSts_CommunicationReady_D | 通信READY | U1￥G35.F |
| ユニットラベル | FX5EIP_1.stEIPArea64.uSet_CommunicationStart_D | EtherNet/IP通信起動要求 | U1￥G272 |
| ユニットラベル | FX5EIP_1.stEIPArea64.uSts_CommunicationStart_D | EtherNet/IP通信起動状態 | U1￥G273 |
| ユニットラベル | FX5EIP_1.stEIPArea64.stnMessageComm64[1].unSet_Request_PathSegment_D | メッセージ通信要求エリア Path Segment | U1￥G4665 |
| ユニットラベル | FX5EIP_1.stEIPArea64.stnMessageComm64[2].unSet_Request_PathSegment_D | メッセージ通信要求エリア Path Segment | U1￥G4857 |
| 定義するラベル | 下記のように，グローバルラベルを定義します。 | （下表） | — |
| 使用ファンクションブロック | M+FX5-EIP_UCMMOriginator_WriteTagData<br>M+FX5-EIP_UCMMOriginator_ReadTagData | — | — |

定義するラベル（グローバルラベル定義画面から書き起こし、原本 p.154）

| No. | ラベル名 | データ型 | クラス | 割付け(デバイス/ラベル) | Japanese/日本語(表示対象) |
|---|---|---|---|---|---|
| 1 | bUCMM_Tag_WriteCommandSendRequest | ビット | VAR_GLOBAL | M100 | UCMMタグ Writeコマンド送信要求 |
| 2 | bUCMM_Tag_ReadCommandSendRequest | ビット | VAR_GLOBAL | M101 | UCMMタグ Readコマンド送信要求 |
| 3 | bRun_SendUCMM_TagWrite | ビット | VAR_GLOBAL | M110 | UCMMタグ Writeコマンド要求 実行中 |
| 4 | bOK_SendUCMM_TagWrite | ビット | VAR_GLOBAL | M120 | UCMMタグ Writeコマンド要求正常完了 |
| 5 | bNG_SendUCMM_TagWrite | ビット | VAR_GLOBAL | M130 | UCMMタグ Writeコマンド要求異常完了 |
| 6 | bRun_SendUCMM_TagRead | ビット | VAR_GLOBAL | M111 | UCMMタグ Readコマンド要求 実行中 |
| 7 | bOK_SendUCMM_TagRead | ビット | VAR_GLOBAL | M121 | UCMMタグ Readコマンド要求正常完了 |
| 8 | bNG_SendUCMM_TagRead | ビット | VAR_GLOBAL | M131 | UCMMタグ Readコマンド要求異常完了 |
| 9 | unSetUCMM_Tag_WriteRequestData | ワード[符号なし]/ビット列[16ビット](0..706) | VAR_GLOBAL | D1000 | UCMMタグ通信 Wite要求データ格納（原文表記「Wite」） |
| 10 | unGetUCMM_Tag_ReadResponseData | ワード[符号なし]/ビット列[16ビット](0..706) | VAR_GLOBAL | D2000 | UCMMタグ通信 Read応答データ格納 |
| 11 | unSetIPAddress | ワード[符号なし]/ビット列[16ビット](0..1) | VAR_GLOBAL | D3000 | 宛先IPアドレス |
| 12 | unSetRequestNo_Write | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D3100 | 要求No(Write) |
| 13 | unGetErrorCode_TagWrite | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D3101 | UCMMタグ通信 Write エラーコード |
| 14 | unGetStatusErrorCode_TagWrite | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D3102 | UCMMタグ通信 Write 通信エラーコード |
| 15 | unSetRequestNo_Read | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D3200 | 要求No(Read) |
| 16 | unGetErrorCode_TagRead | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D3201 | UCMMタグ通信 Read エラーコード |
| 17 | unGetStatusErrorCode_TagRead | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D3202 | UCMMタグ通信 Read 通信エラーコード |
| 18 | unGetResponseData_ReadTagType | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D3203 | タグRead応答 タグデータタイプ |
| 19 | unGetResponseDataSize_TagRead | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D3204 | タグRead応答 データサイズ |

（定義するラベル欄の注記・原文）
> CPUユニットによって，デフォルトのラッチ範囲では，変換が通らないため，データレジスタ(D)のラッチ範囲を変更，またはデータレジスタ(D)を割り付けたラベルのクラスをVAR_GLOVAL_RETAINに定義してください。ラッチ設定については，下記を参照してください。
> MELSEC iQ-F FX5ユーザーズマニュアル(応用編)

【図】クライアント側のプログラム（ラダー図）（原本 p.154-156）

※ニモニックは原本に記載なし。図から書き起こしたもの

```
; (0)
LD     U1\G35.F                 ; FX5EIP_1.bSts_CommunicationReady_D 通信READY
MOV    H1      D3100            ; unSetRequestNo_Write
MOV    H2      D3200            ; unSetRequestNo_Read
MOV    H106    D3000            ; unSetIPAddress[0]
MOV    H0C0A8  D3001            ; unSetIPAddress[1]
MOV    H10     U1\G272          ; FX5EIP_1.stEIPArea64.uSet_CommunicationStart_D
; (26)
LD=_U  H1      U1\G273          ; FX5EIP_1.stEIPArea64.uSts_CommunicationStart_D
AND    M100                     ; bUCMM_Tag_WriteCommandSendRequest (a接点)
MOV    K0      U1\G4665         ; FX5EIP_1.stEIPArea64.stnMessageComm64[1].unSet_Request_PathSegment_D
; (40)
LD=_U  H1      U1\G273
AND    M100                     ; bUCMM_Tag_WriteCommandSendRequest (a接点)
       ; → ユニットFB M_FX5_EIP_UCMMOriginator_WriteTagData_00A_1 の B: i_bEN（下表）
; (1453)
LD=_U  H1      U1\G273
AND    M101                     ; bUCMM_Tag_ReadCommandSendRequest (a接点)
MOV    K0      U1\G4857         ; FX5EIP_1.stEIPArea64.stnMessageComm64[2].unSet_Request_PathSegment_D
; (1467)
LD=_U  H1      U1\G273
AND    M101                     ; bUCMM_Tag_ReadCommandSendRequest (a接点)
       ; → ユニットFB M_FX5_EIP_UCMMOriginator_ReadTagData_00A_1 の B: i_bEN（下表）
; (2999)
END
```

ユニットFB: インスタンス `M_FX5_EIP_UCMMOriginator_WriteTagData_00A_1`（M+FX5-EIP_UCMMOriginator_WriteTagData_00A / UCMM Originator Write tag data）（ステップ(40)）

| 入出力 | 引数 | 接続（ラベル / デバイス / 定数） |
|---|---|---|
| 入力 | B: i_bEN | 起動条件（=_U H1 U1￥G273 かつ M100） |
| 入力 | DUT: i_stModule | FX5EIP_1 |
| 入力 | UW: i_u2TargetAddress | unSetIPAddress / D3000 |
| 入力 | S: i_snTagName | "Tag001" |
| 入力 | UW: i_uDataType | H0C3 |
| 入力 | UW: i_uDataSize | K10 |
| 入力 | UW: i_uWriteData | unSetUCMM_Tag_WriteRequestData / D1000 |
| 入力 | UW: i_uRPI | H0C8 |
| 入力 | UW: i_uTrigger | H0 |
| 入力 | UW: i_uRequestNo | unSetRequestNo_Write / D3100 |
| 出力 | o_bENO :B | bRun_SendUCMM_TagWrite / M110 |
| 出力 | o_bOK :B | bOK_SendUCMM_TagWrite / M120 |
| 出力 | o_bErr :B | bNG_SendUCMM_TagWrite / M130 |
| 出力 | o_uErrId :UW | unGetErrorCode_TagWrite / D3101 |
| 出力 | o_uStatusId :UW | unGetStatusErrorCode_TagWrite / D3102 |
| 公開変数（FB内表示） | pbi_unPathSegment | （接続なし） |
| 公開変数（FB内表示） | pbo_u2CIPResponseCode | （接続なし） |
| 公開変数（FB内表示） | pbo_udRequestCompleteCount | （接続なし） |

ユニットFB: インスタンス `M_FX5_EIP_UCMMOriginator_ReadTagData_00A_1`（M+FX5-EIP_UCMMOriginator_ReadTagData_00A / UCMM Originator Read tag data）（ステップ(1467)）

| 入出力 | 引数 | 接続（ラベル / デバイス / 定数） |
|---|---|---|
| 入力 | B: i_bEN | 起動条件（=_U H1 U1￥G273 かつ M101） |
| 入力 | DUT: i_stModule | FX5EIP_1 |
| 入力 | UW: i_u2TargetAddress | unSetIPAddress / D3000 |
| 入力 | S: i_snTagName | "Tag002" |
| 入力 | UW: i_uDataType | H0C4 |
| 入力 | UW: i_uDataSize | K10 |
| 入力 | UW: i_uRPI | H0C8 |
| 入力 | UW: i_uTrigger | H0 |
| 入力 | UW: i_uRequestNo | unSetRequestNo_Read / D3200 |
| 出力 | o_bENO :B | bRun_SendUCMM_TagRead / M111 |
| 出力 | o_bOK :B | bOK_SendUCMM_TagRead / M121 |
| 出力 | o_bErr :B | bNG_SendUCMM_TagRead / M131 |
| 出力 | o_uErrId :UW | unGetErrorCode_TagRead / D3201 |
| 出力 | o_uStatusId :UW | unGetStatusErrorCode_TagRead / D3202 |
| 出力 | o_uDataType :UW | unGetResponseData_ReadTagType / D3203 |
| 出力 | o_uDataSize :UW | unGetResponseDataSize_TagRead / D3204 |
| 出力 | o_uReadData :UW | unGetUCMM_Tag_ReadResponseData / D2000 |
| 公開変数（FB内表示） | pbi_unPathSegment | （接続なし） |
| 公開変数（FB内表示） | pbo_u2CIPResponseCode | （接続なし） |
| 公開変数（FB内表示） | pbo_udRequestCompleteCount | （接続なし） |

プログラムの説明（原文）
> (0) UCMMタグ通信するための要求No.および宛先IPアドレスを設定して，EtherNet/IP通信を開始します。
> (26) ユニットFBで使用するPath Segmentデータに対して，0(無効)を指定します。
> (40) M100をONすることで，M+FX5-EIP_UCMMOriginator_WriteTagDataが実行されて，Write要求をサーバ側に送信します。
> M120がONのとき，サーバ側のTag001に対して，D1000以降に格納したデータを10ワード分書き込みます。
> (1453)ユニットFBで使用するPath Segmentデータに対して，0(無効)を指定します。
> (1467)M101をONすることで，M+FX5-EIP_UCMMOriginator_ReadTagDataが実行されて，Read要求をサーバ側に送信します。
> M121がONのとき，サーバ側の応答結果をD3204に格納された応答データサイズ分，D2000以降に格納されます。

> **Point**
> - 設定する要求No.は，Class3通信で使用するコネクションNo.や，他のUCMM通信/Class1通信/Class3通信で使用する要求No.と重複しないよう注意してください。
> - FX5-EIPのように，Path Segmentの設定が不要な機器へ要求を送信する場合，プログラム例の1453ステップ目のように設定が必要です。(244ページ メッセージ通信要求/応答エリア)

##### サーバ側のプログラム (8.4 / 印刷 p.155 / 原本 p.157)

| 分類 | ラベル名 | 内容 | デバイス |
|---|---|---|---|
| ユニットラベル | FX5EIP_1.bSts_CommunicationReady_D | 通信READY | U1￥G35.F |
| ユニットラベル | FX5EIP_1.stEIPArea64.uSet_CommunicationStart_D | EtherNet/IP通信起動要求 | U1￥G272 |
| ユニットラベル | FX5EIP_1.stEIPArea64.uSts_CommunicationStart_D | EtherNet/IP通信起動状態 | U1￥G273 |
| ユニットラベル | FX5EIP_1.stEIPArea64.stnAreaInputDataArea64[unReadWrite_ConnectionNo].unInputData | 入力データエリア | U1￥G16944~U1￥G63151 |
| ユニットラベル | FX5EIP_1.stEIPArea64.stnAreaOutputDataArea64[unReadWrite_ConnectionNo].unOutputData | 出力/メッセージ通信(サーバ)データエリア | U1￥G63152~U1￥G109359 |
| ユニットラベル | FX5EIP_1.stEIPArea64.unVal_InputDataSize_Connection_D[unReadWrite_ConnectionNo] | 入力データサイズ | U1￥G304~U1￥G367 |
| ユニットラベル | FX5EIP_1.stEIPArea64.unVal_OutputDataSize_Connection_D[unReadWrite_ConnectionNo] | 出力/メッセージ通信(サーバ)データサイズ | U1￥G432~U1￥G495 |
| 定義するラベル | 下記のように，グローバルラベルを定義します。 | （下表） | — |

定義するラベル（グローバルラベル定義画面から書き起こし、原本 p.157）

| No. | ラベル名 | データ型 | クラス | 割付け(デバイス/ラベル) | Japanese/日本語(表示対象) |
|---|---|---|---|---|---|
| 1 | bReadSTOP | ビット | VAR_GLOBAL | M11 | Read更新停止要求 |
| 2 | bWriteSTOP | ビット | VAR_GLOBAL | M12 | Write更新停止要求 |
| 3 | unReadWrite_ConnectionNo | ワード[符号付き] | VAR_GLOBAL | D300 | Read/WriteコネクションNo |
| 4 | unSetTag_WriteData | ワード[符号なし]/ビット列[16ビット](0..721) | VAR_GLOBAL | D1000 | 現在値更新データ |
| 5 | unGetTag_ReadData | ワード[符号なし]/ビット列[16ビット](0..721) | VAR_GLOBAL | D2000 | 現在値取得データ |

（定義するラベル欄の注記・原文）
> CPUユニットによって，デフォルトのラッチ範囲では，変換が通らないため，データレジスタ(D)のラッチ範囲を変更，またはデータレジスタ(D)を割り付けたラベルのクラスをVAR_GLOVAL_RETAINに定義してください。ラッチ設定については，下記を参照してください。
> MELSEC iQ-F FX5ユーザーズマニュアル(応用編)

【図】サーバ側のプログラム（ラダー図）（原本 p.157）

※ニモニックは原本に記載なし。図から書き起こしたもの。ラベル配列の添字 [unReadWrite_ConnectionNo] はラベル表記のまま記載

```
; (0)
LD     U1\G35.F                 ; FX5EIP_1.bSts_CommunicationReady_D 通信READY
MOV    H10     U1\G272          ; FX5EIP_1.stEIPArea64.uSet_CommunicationStart_D
; (9)
LD=_U  H1      U1\G273          ; FX5EIP_1.stEIPArea64.uSts_CommunicationStart_D
ANI    M11                      ; bReadSTOP (b接点)
MOV    H1      D300             ; unReadWrite_ConnectionNo
BMOV   FX5EIP_1.stEIPArea64.stnAreaOutputDataArea64[unReadWrite_ConnectionNo].unOutputData  D2000(unGetTag_ReadData)  FX5EIP_1.stEIPArea64.unVal_OutputDataSize_Connection_D[unReadWrite_ConnectionNo]
; (62)
LD=_U  H1      U1\G273
ANI    M12                      ; bWriteSTOP (b接点)
MOV    H2      D300             ; unReadWrite_ConnectionNo
BMOV   D1000(unSetTag_WriteData)  FX5EIP_1.stEIPArea64.stnAreaOutputDataArea64[unReadWrite_ConnectionNo].unOutputData  FX5EIP_1.stEIPArea64.unVal_OutputDataSize_Connection_D[unReadWrite_ConnectionNo]
; (115)
END
```

プログラムの説明（原文）
> (0) EtherNet/IP通信を開始します。
> (9) 現在値を読み出したいタグに設定されたコネクションNo.を指定し，指定したタグに設定されたデータをD2000にコピーします。
> (62) 現在値を更新したいタグに設定されたコネクションNo.を指定し，指定したタグに設定されたデータをD1000に設定したデータに更新します。

## 転記時の要確認一覧 (8.3〜8.4 / 原本 p.146-157)

- 原本 p.153 タグ設定(コネクションNo.2) の画面キャプチャでは「データ型: INT」と表示されているが、直下の本文・p.150の■Read要求は「DINT型(2ワード)」。原本どおり両方を転記した。どちらが正しいかは要確認（原本の画面キャプチャの不整合の可能性）
- 原本 p.157 サーバ側プログラムのユニットラベル表には stnAreaInputDataArea64 / unVal_InputDataSize_Connection_D が載っているが、ラダー図 (9)(62) の BMOV はどちらも stnAreaOutputDataArea64 / unVal_OutputDataSize_Connection_D を使っている（図を拡大して確認済み、図のとおり転記）。意図は要確認
- p.149・p.150 の「÷」「×」はテキスト抽出で欠落していたため、画像から補った（「応答データサイズ÷2(バイト)」「要求データサイズ×1ワード」等）
- 「VAR_GLOVAL_RETAIN」（p.148, p.154, p.157）、「Wite要求データ格納」（p.154 ラベル表No.9）は原文表記のまま
