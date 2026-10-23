# 三菱 MELSEC iQ-F FX5-EIP形 EtherNet/IPユニット ユーザーズマニュアル 第8章 8.2 サイクリック通信の交信例

| 項目 | 内容 |
|---|---|
| 原本 | 三菱電機 MELSEC iQ-F FX5-EIP形EtherNet/IPユニットユーザーズマニュアル |
| 発行元 | 三菱電機株式会社 |
| 資料番号 / 版数 | SH-082708 / B版（PDFメタデータ subject: SH-082708-B） |
| 原本PDF | `PDF/MELSEC iQ-F FX5-EIP形EtherNet_IPユニットユーザーズマニュアル.pdf` (全274ページ) |
| 本ファイルの範囲 | 8.2 サイクリック通信の交信例 (印刷 p.131-143 / PDF p.133-145) |
| ページ対応 | 「原本 p.」はPDFのページ番号、「印刷 p.」は原本フッタのページ番号。印刷ページ = PDFページ − 2。本文中の「〇〇ページ参照」は印刷ページ |
| 変換日 | 2026-10-23 |
| 変換方法 | pypdfium2(本文) + PyMuPDF 200dpi 画像の目視(全ページ)。ラダー図・ラベル定義表は 400dpi 拡大画像で接点a/b・オペランドを確認 |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。

**転記上の扱い**: 原本の結合セルは各行に値を展開。セル内改行は `<br>`。図は【図】プレースホルダ＋読み取れる事実の箇条書き。GX Works3 の設定画面キャプチャは【図】＋画面上の項目名・設定値を表で全件。ラダー図のニモニックは原本に記載がなく、図から書き起こしたもの（各所に注記）。ファンクションブロック(FB)呼出しはニモニック1行で表せないため、FB名と入出力ピンの割付を表で記載。バッファメモリは本文・表では原本表記の `Un￥G`/`U1￥G`（全角￥）に統一、ニモニックのコードブロック内のみ GX Works3 入力形式の `U1￥G` と表記。見出しレベル: 章 `##` / 節 `###` / 項 `####` / 小見出し(帯見出し) `#####`。

---

## 主要用語 対訳表 (Glossary) (8.2 / 原本 p.133-145)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| サイクリック通信 | Cyclic communication | — | 参考訳 |
| Class1インスタンス通信 / インスタンス通信 | Class1 instance communication | Class1 Instance | 参考訳 |
| Class1タグ通信 / タグ通信 | Class1 tag communication | Class1 Tag | 参考訳 |
| オリジネータ | Originator | O | 参考訳 |
| ターゲット | Target | T | 参考訳 |
| コネクション | Connection | コネクションNo | 参考訳 |
| 最大コネクション数設定 | Maximum number of connections setting | — | 参考訳 |
| 入力データエリア | Input data area | Un￥G16944～Un￥G63151 | 参考訳 |
| 出力データエリア | Output data area | Un￥G63152～Un￥G109359 | 参考訳 |
| 自動リフレッシュ | Auto refresh | — | 参考訳 |
| リフレッシュ設定 | Refresh settings | — | 参考訳 |
| ネットワークユニットへ転送 / CPUユニットへ転送 | Transfer to network module / Transfer to CPU module | — | 参考訳 |
| EtherNet/IP構成 | EtherNet/IP configuration | ユニット拡張パラメータ | 参考訳 |
| コネクション設定 | Connection settings | — | 参考訳 |
| 入力 T->O | Input T->O (Target to Originator) | T->O | 参考訳 |
| 出力 O->T | Output O->T (Originator to Target) | O->T | 参考訳 |
| 要求パケット間隔 | Requested Packet Interval | RPI | 参考訳 |
| インスタンスID | Instance ID | 768 等 | 参考訳 |
| タグ名 | Tag name | Tag001 | 参考訳 |
| 送信抑制時間 | Production inhibit time | — | 参考訳 |
| タイムアウト乗数 | Timeout multiplier | — | 参考訳 |
| 同一性チェック | Identity check (electronic key) | — | 参考訳 |
| EDSファイル | Electronic Data Sheet file | EDS | 参考訳 |
| 通信READY | Communication READY | U1￥G35.F | 参考訳 |
| EtherNet/IP通信起動要求 | EtherNet/IP communication start request | U1￥G272 | 参考訳 |
| EtherNet/IP通信起動状態 | EtherNet/IP communication start status | U1￥G273 | 参考訳 |
| 入力データサイズ | Input data size | U1￥G305 | 参考訳 |
| 出力/メッセージ通信(サーバ)データサイズ | Output/message communication (server) data size | U1￥G432 | 参考訳 |
| サイクリック通信データリンク状態 | Cyclic communication data link status | U1￥G1328.0 / U1￥G1328.1 | 参考訳 |
| サイクリック通信異常状態 | Cyclic communication error status | U1￥G1336.0 / U1￥G1336.1 | 参考訳 |
| サイクリック通信入力エラー状態 | Cyclic communication input error status | U1￥G1392 / U1￥G1394 | 参考訳 |
| サイクリック通信出力エラー状態 | Cyclic communication output error status | U1￥G1648 / U1￥G1650 | 参考訳 |
| ユニットラベル | Module label | FX5EIP_1 | 参考訳 |
| グローバルラベル | Global label | VAR_GLOBAL | 参考訳 |
| ラッチ範囲 | Latch range | VAR_GLOVAL_RETAIN（原文表記） | 参考訳 |
| ファンクションブロック | Function block | FB / M+FX5-EIP_Class1GetInputData, M+FX5-EIP_Class1SetOutputData | 参考訳 |
| 通信停止指示 | Communication stop instruction | bStopCommunication / M200 | 参考訳 |

## 変換範囲表 (8.2 / 原本 p.133-145)

| 原本ページ | 節 | 扱い |
|---|---|---|
| p.133 | 8.2 サイクリック通信の交信例 / システム構成 | 全文 |
| p.134 | 通信内容 | 全文 |
| p.135-141 | パラメータ設定（オリジネータ／ターゲット1／ターゲット2） | 全文（設定画面の項目・設定値を表で全件） |
| p.142-143 | プログラム例 / オリジネータ側のプログラム | 全文（使用デバイス表・ラベル定義表全件、ラダー全ステップをニモニック化、説明文全文） |
| p.144 | ターゲット1側のプログラム | 全文（同上） |
| p.145 | ターゲット2側のプログラム | 全文（同上） |
| 上記以外 | 8.1 以前 / 8.3 以降・他章 | 同フォルダの他ファイル参照 |

## 目次 (8.2)

- [8 プログラミング（続き）](#8-プログラミング続き-8--印刷-p131--原本-p133)
  - [8.2 サイクリック通信の交信例](#82-サイクリック通信の交信例-82--印刷-p131--原本-p133)
    - システム構成 / 通信内容 / パラメータ設定 / プログラム例

## 8 プログラミング（続き） (8 / 印刷 p.131 / 原本 p.133)

### 8.2 サイクリック通信の交信例 (8.2 / 印刷 p.131 / 原本 p.133)

FX5-EIP同士で，サイクリック通信を行う例を示します。

#### システム構成 (8.2 / 印刷 p.131 / 原本 p.133)

Class1インスタンス通信およびClass1タグ通信の交信例は，下記のシステム構成を使用して説明します。
各FX5-EIPは”最大コネクション数設定”が64に設定されているものとします。

【図】システム構成（原本 p.133）
- オリジネータ: 192.168.4.51
- ターゲット1: 192.168.4.1
- ターゲット2: 192.168.4.2
- 3台のFX5-EIPはスイッチングハブを介してEthernetで接続
- (1) オリジネータとターゲット1によるClass1インスタンス通信
- (2) オリジネータとターゲット2によるClass1タグ通信

#### 通信内容 (8.2 / 印刷 p.132 / 原本 p.134)

FX5-EIPのバッファメモリと，各ターゲットの関係を示します。
- オリジネータとターゲット1のインスタンス通信はFBを利用して通信します。
- オリジネータとターゲット2のタグ通信は自動リフレッシュを利用して通信します。

【図】バッファメモリとCPUデバイスの関係（原本 p.134）
- オリジネータ バッファメモリ ’入力データエリア’(Un￥G16944~Un￥G63151): 先頭に64ワード（ターゲット1から）、続いて248ワード（ターゲット2から）
- ターゲット1 バッファメモリ ’出力データエリア’(Un￥G63152~Un￥G109359): 64ワード
- ターゲット2 バッファメモリ ’出力データエリア’(Un￥G63152~Un￥G109359): 248ワード
- ターゲット1 FX5CPUデバイス D0~D63（64ワード） →(1)→ ターゲット1 出力データエリア 64ワード →(2)→ オリジネータ 入力データエリア 64ワード →(3)→ オリジネータ FX5CPUデバイス D0~D63（64ワード）
- ターゲット2 FX5CPUデバイス D0~D247（248ワード） →(4)→ ターゲット2 出力データエリア 248ワード →(5)→ オリジネータ 入力データエリア 248ワード →(6)→ オリジネータ FX5CPUデバイス D200~D447（248ワード）

凡例（原文）:
- (1) CPUユニットから出力データエリアへFBで転送
- (2) インスタンス通信
- (3) 入力データエリアからCPUユニットへFBで転送
- (4) CPUユニットから出力データエリアへ自動リフレッシュ
- (5) タグ通信
- (6) 入力データエリアからCPUユニットへ自動リフレッシュ

#### パラメータ設定 (8.2 / 印刷 p.133 / 原本 p.135)

エンジニアリングツールを使用してパラメータを設定します。

> **Point**
> プログラム例では，設定手順で示すパラメータ以外の設定はデフォルトを使用します。パラメータについては，下記を参照してください。
> 87ページ パラメータ設定

##### FX5-EIP(オリジネータ)の設定 (8.2 / 印刷 p.133 / 原本 p.135)

エンジニアリングツールをオリジネータ側のCPUユニットに接続し，パラメータを設定します。

1. IPアドレスを設定します。
   - ナビゲーションウィンドウ⇨[パラメータ]⇨[ユニット情報]⇨[FX5-EIP]⇨[ユニットパラメータ]⇨[基本設定]

【図】基本設定画面（オリジネータ）（原本 p.135）

| 項目 | 設定 |
|---|---|
| 自ノード設定 > IPアドレス設定 > IPアドレス | 192 . 168 . 4 . 51 |
| 自ノード設定 > IPアドレス設定 > サブネットマスク | 255 . 255 . 255 . 0 |
| 自ノード設定 > IPアドレス設定 > デフォルトゲートウェイ | （空欄） |
| 自ノード設定 > 交信データコード | バイナリ |
| 自ノード設定 > オープン方法の設定 | プログラムでOPENしない |

IPアドレス: 192.168.4.51
サブネットマスク: 255.255.255.0

2. 自動リフレッシュを設定します。
   - ナビゲーションウィンドウ⇨[パラメータ]⇨[ユニット情報]⇨[FX5-EIP]⇨[ユニットパラメータ]⇨[基本設定]⇨[リフレッシュ設定]⇨<詳細設定>

【図】リフレッシュ設定画面（オリジネータ）（原本 p.135）
- リフレッシュ先: 指定デバイス
- 項目「CPUユニットへ転送」（バッファメモリのデータを指定したデバイスに転送します）

| 項目 | 自動リフレッシュ | デバイス名 | 点数 | 先頭 | 最終 |
|---|---|---|---|---|---|
| コネクションNo.1 | 無効 | — | — | — | — |
| コネクションNo.2 | 有効 | D | 248 | 200 | 447 |
| コネクションNo.3 | 無効 | — | — | — | — |
| コネクションNo.4 | 無効 | — | — | — | — |
| コネクションNo.5 | 無効 | — | — | — | — |
| コネクションNo.6 | 無効 | — | — | — | — |
| コネクションNo.7 | 無効 | — | — | — | — |
| コネクションNo.8 | 無効 | — | — | — | — |
| コネクションNo.9 | 無効 | — | — | — | — |
| コネクションNo.10 | 無効 | — | — | — | — |

（画面はコネクションNo.10までの表示。以降はスクロール外で原本に表示なし）

■CPUユニットへ転送
- コネクションNo.2: D200~D447

> **Point**
> ”自動リフレッシュ一括設定”と”点数一括設定”を使用する場合は，あらかじめ”EtherNet/IP構成”にてコネクション設定を行う必要があります。

3. [適用]ボタンをクリックします。

4. ”EtherNet/IP構成”にて，EtherNet/IPの通信パラメータを設定します。
   - ナビゲーションウィンドウ⇨[パラメータ]⇨[ユニット情報]⇨[FX5-EIP]⇨[EtherNet/IP構成(ユニット拡張パラメータ)]

5. ”ユニット一覧”から”FX5-EIP”をEtherNet/IP機器一覧に追加します。

【図】EtherNet/IP構成画面（装着位置No.: 1[U1]）（原本 p.136）

| No. | 形名 | 機器名 | IPアドレス | 予約ノード | コネクション設定 |
|---|---|---|---|---|---|
| （空欄） | 自ノード | （空欄） | 192.168.4.51 | （空欄） | <詳細設定> |
| 1 | FX5-EIP | （空欄） | 192.168.4.1 | 設定なし | <詳細設定> |
| 2 | FX5-EIP | （空欄） | 192.168.4.2 | 設定なし | <詳細設定> |

- ユニット一覧: EtherNet/IP機器(汎用) / EtherNet/IP機器(三菱電機) > 通信アダプタ > FX5-EIP 1.1, RJ71GN11-EI… 3.1, RJ71GN11-EI… 2.1, RJ71GN11-EI… 1.1
- 選択中ユニットの情報: 【ベンダ名】三菱電機 【製品種別名】通信アダプタ 【形名】FX5-EIP 【リビジョン】DeviceRevision:1.1 FileRevision:1.1
- 構成図: 自ノード 192.168.4.51（自ノード 総ノード数: 2/64）、FX5-EIP 192.168.4.1、FX5-EIP 192.168.4.2

> **Point**
> ”ユニット一覧”に”FX5-EIP”が無い場合は，EDSファイルの追加が必要です。
> EDSファイルの追加については，下記を参照してください。
> 120ページ EDSファイルの追加/削除

6. ”コネクション設定”列の<詳細設定>をダブルクリックして，ターゲット1，ターゲット2とのコネクションを設定します。

- ターゲット1に対するインスタンス通信設定

【図】コネクション設定画面（オリジネータ → ターゲット1）（原本 p.137）
- コネクション情報: コネクション数 1/64、通信処理性能(PPS) 40
- コネクション一覧: 自ノード > オリジネータ > FX5-EIP(192.168.4.1) > (001)

| 項目名 | 設定値 | 単位 |
|---|---|---|
| コネクション名 | Input Only(Class1 Instance) | － |
| アプリケーションタイプ | Input Only | － |
| コネクションNo | 001 | － |
| 通信方式 | インスタンス通信 | － |
| コメント | （空欄） | － |
| トリガータイプ | Cyclic | － |
| 送信抑制時間モード | デフォルト | － |
| 送信抑制時間 | 12 | ms |
| タイムアウト乗数 | x4 | － |
| コンフィグレーションインスタンス | 1 | － |
| 入力 T->O：入力モード | Point to point | － |
| 入力 T->O：リアルタイムフォーマット | モードレス | － |
| 入力 T->O：データサイズ | 128 | byte |
| 入力 T->O：優先度 | スケジュール | － |
| 入力 T->O：要求パケット間隔(RPI) | 50000 | μs |
| 入力 T->O：インスタンスID | 768 | － |
| 出力 O->T：出力モード | Point to point | － |
| 出力 O->T：リアルタイムフォーマット | Heartbeat | － |
| 出力 O->T：データサイズ | 0 | byte |
| 出力 O->T：優先度 | スケジュール | － |
| 出力 O->T：要求パケット間隔(RPI) | 50000 | μs |
| 出力 O->T：インスタンスID | 254 | － |
| 同一性チェック：互換性モード | 無効 | － |
| 同一性チェック：ベンダコードのチェック | 無効 | － |
| 同一性チェック：製品種別のチェック | 無効 | － |
| 同一性チェック：製品コードのチェック | 無効 | － |
| 同一性チェック：メジャーリビジョンのチェック | 無効 | － |
| 同一性チェック：マイナーリビジョンのチェック | 無効 | － |

- コネクションを追加する際[Input Only(Class1 Instance)]を選択します。
- 入力T->OのインスタンスID: 768(ターゲット1に設定された通信したいコネクションのインスタンスIDを設定します。)
- 入力T->Oのデータサイズ: 128(ターゲット1に設定された通信したいコネクションのデータサイズを設定します。)

- ターゲット2に対するタグ通信設定

【図】コネクション設定画面（オリジネータ → ターゲット2）（原本 p.138）
- コネクション情報: コネクション数 2/64、通信処理性能(PPS) 80
- コネクション一覧: 自ノード > オリジネータ > FX5-EIP(192.168.4.1) > (001)、FX5-EIP(192.168.4.2) > (002)

| 項目名 | 設定値 | 単位 |
|---|---|---|
| コネクション名 | Input Only(Class1 Tag) | － |
| アプリケーションタイプ | Input Only | － |
| コネクションNo | 002 | － |
| 通信方式 | タグ通信 | － |
| コメント | （空欄） | － |
| タグ名 | Tag001 | － |
| タグ名文字数 | 6 | 文字 |
| トリガータイプ | Cyclic | － |
| 送信抑制時間モード | デフォルト | － |
| 送信抑制時間 | 12 | ms |
| タイムアウト乗数 | x4 | － |
| 入力 T->O：入力モード | Point to point | － |
| 入力 T->O：リアルタイムフォーマット | モードレス | － |
| 入力 T->O：データサイズ | 496 | byte |
| 入力 T->O：優先度 | スケジュール | － |
| 入力 T->O：要求パケット間隔(RPI) | 50000 | μs |
| 出力 O->T：出力モード | Point to point | － |
| 出力 O->T：リアルタイムフォーマット | Heartbeat | － |
| 出力 O->T：優先度 | スケジュール | － |
| 出力 O->T：要求パケット間隔(RPI) | 50000 | μs |
| 同一性チェック：互換性モード | 無効 | － |
| 同一性チェック：ベンダコードのチェック | 無効 | － |
| 同一性チェック：製品種別のチェック | 無効 | － |
| 同一性チェック：製品コードのチェック | 無効 | － |
| 同一性チェック：メジャーリビジョンのチェック | 無効 | － |

（画面はスクロール途中で切れており、マイナーリビジョンのチェック以降は原本の画面に表示なし）

- コネクションを追加する際[Input Only(Class1 Tag)]を選択します。
- 入力T->Oのタグ名: Tag001(ターゲット2に設定された通信したいコネクションのタグ名を設定します。)
- 入力T->Oのデータサイズ: 496(ターゲット2に設定された通信したいコネクションのデータサイズを設定します。)

7. [適用]ボタンをクリックします。
8. [OK]ボタンをクリックして，コネクション設定を閉じます。
9. [設定を反映して閉じる]を選択し，”EtherNet/IP構成”画面を閉じます。
10. 設定したパラメータをオリジネータ側のCPUユニットに書き込み，CPUユニットをリセット，または電源をOFF→ONします。
    - [オンライン]⇨[シーケンサへの書込み]

##### FX5-EIP(ターゲット1)の設定 (8.2 / 印刷 p.137 / 原本 p.139)

エンジニアリングツールをターゲット1側のCPUユニットに接続し，パラメータを設定します。

1. IPアドレスを設定します。
   - ナビゲーションウィンドウ⇨[パラメータ]⇨[ユニット情報]⇨[FX5-EIP]⇨[ユニットパラメータ]⇨[基本設定]

【図】基本設定画面（ターゲット1）（原本 p.139）

| 項目 | 設定 |
|---|---|
| 自ノード設定 > IPアドレス設定 > IPアドレス | 192 . 168 . 4 . 1 |
| 自ノード設定 > IPアドレス設定 > サブネットマスク | 255 . 255 . 255 . 0 |
| 自ノード設定 > IPアドレス設定 > デフォルトゲートウェイ | （空欄） |
| 自ノード設定 > 交信データコード | バイナリ |
| 自ノード設定 > オープン方法の設定 | プログラムでOPENしない |

IPアドレス: 192.168.4.1
サブネットマスク: 255.255.255.0

2. [適用]ボタンをクリックします。
3. ”EtherNet/IP構成”にて，EtherNet/IPの通信パラメータを設定します。
   - ナビゲーションウィンドウ⇨[パラメータ]⇨[ユニット情報]⇨[FX5-EIP]⇨[EtherNet/IP構成(ユニット拡張パラメータ)]
4. ”コネクション設定”列の<詳細設定>をダブルクリックして，コネクションを設定します。

【図】コネクション設定画面（ターゲット1）（原本 p.139）
- コネクション情報: コネクション数 1/64、通信処理性能(PPS) 0
- コネクション一覧: 自ノード > ターゲット > (001)

| 項目名 | 設定値 | 単位 |
|---|---|---|
| コネクション名 | コネクション(ターゲット インスタンス通信) | － |
| アプリケーションタイプ | Input Only | － |
| コネクションNo | 001 | － |
| 通信方式 | インスタンス通信 | － |
| コメント | （空欄） | － |
| 出力 T->O：データサイズ | 128 | byte |
| 出力 T->O：インスタンスID | 768 | － |
| 入力 O->T：データサイズ | － | － |
| 入力 O->T：インスタンスID | － | － |

- コネクションを追加する際[コネクション(ターゲット インスタンス通信)]を選択します。
- インスタンスID: 768
- データサイズ: 128

5. [適用]ボタンをクリックします。
6. [OK]ボタンをクリックして，コネクション設定を閉じます。
7. [設定を反映して閉じる]を選択し，”EtherNet/IP構成”画面を閉じます。
8. 設定したパラメータをオリジネータ側のCPUユニットに書き込み，CPUユニットをリセット，または電源をOFF→ONします。
   - [オンライン]⇨[シーケンサへの書込み]

##### FX5-EIP(ターゲット2)の設定 (8.2 / 印刷 p.138 / 原本 p.140)

エンジニアリングツールをターゲット2側のCPUユニットに接続し，パラメータを設定します。

1. IPアドレスを設定します。
   - ナビゲーションウィンドウ⇨[パラメータ]⇨[ユニット情報]⇨[FX5-EIP]⇨[ユニットパラメータ]⇨[基本設定]

【図】基本設定画面（ターゲット2）（原本 p.140）

| 項目 | 設定 |
|---|---|
| 自ノード設定 > IPアドレス設定 > IPアドレス | 192 . 168 . 4 . 2 |
| 自ノード設定 > IPアドレス設定 > サブネットマスク | 255 . 255 . 255 . 0 |
| 自ノード設定 > IPアドレス設定 > デフォルトゲートウェイ | （空欄） |
| 自ノード設定 > 交信データコード | バイナリ |
| 自ノード設定 > オープン方法の設定 | プログラムでOPENしない |

IPアドレス: 192.168.4.2
サブネットマスク: 255.255.255.0

2. 自動リフレッシュを設定します。
   - ナビゲーションウィンドウ⇨[パラメータ]⇨[ユニット情報]⇨[FX5-EIP]⇨[ユニットパラメータ]⇨[基本設定]⇨[リフレッシュ設定]⇨<詳細設定>

【図】リフレッシュ設定画面（ターゲット2）（原本 p.140）
- リフレッシュ先: 指定デバイス
- 項目「ネットワークユニットへ転送」（指定したデバイスのデータをバッファメモリに転送します）

| 項目 | 自動リフレッシュ | デバイス名 | 点数 | 先頭 | 最終 |
|---|---|---|---|---|---|
| コネクションNo.1 | 有効 | D | 248 | 0 | 247 |
| コネクションNo.2 | 無効 | — | — | — | — |
| コネクションNo.3 | 無効 | — | — | — | — |
| コネクションNo.4 | 無効 | — | — | — | — |
| コネクションNo.5 | 無効 | — | — | — | — |
| コネクションNo.6 | 無効 | — | — | — | — |
| コネクションNo.7 | 無効 | — | — | — | — |
| コネクションNo.8 | 無効 | — | — | — | — |
| コネクションNo.9 | 無効 | — | — | — | — |
| コネクションNo.10 | 無効 | — | — | — | — |

（画面はコネクションNo.10までの表示。以降はスクロール外で原本に表示なし）

■ネットワークユニットへ転送
- コネクションNo.1: D0~D247

> **Point**
> ”自動リフレッシュ一括設定”と”点数一括設定”を使用する場合は，あらかじめ”EtherNet/IP構成”にてコネクション設定を行う必要があります。

3. [適用]ボタンをクリックします。
4. ”EtherNet/IP構成”にて，EtherNet/IPの通信パラメータを設定します。
   - [ナビゲーションウィンドウ]⇨[パラメータ]⇨[ユニット情報]⇨[FX5-EIP]⇨[EtherNet/IP構成(ユニット拡張パラメータ)]
5. ”コネクション設定”列の<詳細設定>をダブルクリックして，コネクションを設定します。

【図】コネクション設定画面（ターゲット2）（原本 p.141）
- コネクション情報: コネクション数 1/64、通信処理性能(PPS) 0
- コネクション一覧: 自ノード > ターゲット > (001)

| 項目名 | 設定値 | 単位 |
|---|---|---|
| コネクション名 | コネクション(ターゲット タグ通信) | － |
| アプリケーションタイプ | Input Only | － |
| コネクションNo | 001 | － |
| 通信方式 | タグ通信 | － |
| コメント | （空欄） | － |
| タグ名 | Tag001 | － |
| タグ名文字数 | 6 | 文字 |
| データサイズ | 496 | byte |

- コネクションを追加する際[コネクション(ターゲット タグ通信)]を選択します。
- タグ名: Tag001
- データサイズ: 496

6. [適用]ボタンをクリックします。
7. [OK]ボタンをクリックして，コネクション設定を閉じます。
8. [設定を反映して閉じる]を選択し，”EtherNet/IP構成”画面を閉じます。
9. 設定したパラメータをオリジネータ側のCPUユニットに書き込み，CPUユニットをリセット，または電源をOFF→ONします。
   - [オンライン]⇨[シーケンサへの書込み]

#### プログラム例 (8.2 / 印刷 p.140 / 原本 p.142)

サイクリック通信にて入出力データ交信を開始するプログラム例を示します。

##### オリジネータ側のプログラム (8.2 / 印刷 p.140-141 / 原本 p.142-143)

| 分類 | ラベル名 | 内容 | デバイス |
|---|---|---|---|
| ユニットラベル | FX5EIP_1.bSts_CommunicationReady_D | 通信READY | U1￥G35.F |
| ユニットラベル | FX5EIP_1.stEIPArea64.uSet_CommunicationStart_D | EtherNet/IP通信起動要求 | U1￥G272 |
| ユニットラベル | FX5EIP_1.stEIPArea64.uSts_CommunicationStart_D | EtherNet/IP通信起動状態 | U1￥G273 |
| ユニットラベル | FX5EIP_1.stEIPArea64.unVal_InputDataSize_Connection_D[2] | 入力データサイズ | U1￥G305 |
| ユニットラベル | FX5EIP_1.stEIPArea64.unSts_CyclicDataLink_Connection_D[1].1 | サイクリック通信データリンク状態 | U1￥G1328.1 |
| ユニットラベル | FX5EIP_1.stEIPArea64.unSts_CyclicError_Connection_D[1].1 | サイクリック通信異常状態 | U1￥G1336.1 |
| ユニットラベル | FX5EIP_1.stEIPArea64.udnSts_CyclicErrorStatus_Connection_In_D[2] | サイクリック通信入力エラー状態 | U1￥G1394 |
| ユニットラベル | FX5EIP_1.stEIPArea64.udnSts_CyclicErrorStatus_Connection_Out_D[2] | サイクリック通信出力エラー状態 | U1￥G1650 |
| 定義するラベル | 下記のように，グローバルラベルを定義します。（下表） | | |
| 使用ファンクションブロック | M+FX5-EIP_Class1GetInputData | | |

定義するラベル（グローバルラベル設定画面）:

| No. | ラベル名 | データ型 | クラス | 割付け(デバイス/ラベル) | Japanese/日本語(表示対象) |
|---|---|---|---|---|---|
| 1 | bnRequest_GetInputData | ビット(0..1) | VAR_GLOBAL | M0 | 入力データ取得実行設定 |
| 2 | bnRun_GetInputData | ビット | VAR_GLOBAL | M10 | 入力データ取得実行中 |
| 3 | bnOK_GetInputData | ビット | VAR_GLOBAL | M20 | 入力データ取得正常 |
| 4 | bnNG_GetInputData | ビット | VAR_GLOBAL | M30 | 入力データ取得異常 |
| 5 | unErrorCode_GetInputData | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D2000 | 入力データ取得異常時のエラーコード |
| 6 | undStatusId_GetInputData | ダブルワード[符号なし]/ビット列[32ビット](0..1) | VAR_GLOBAL | D2001 | 入力データ取得 コネクション通信異常の入力側エラー |
| 7 | undStatusId_GetOutputData | ダブルワード[符号なし]/ビット列[32ビット](0..1) | VAR_GLOBAL | D2005 | 入力データ取得 コネクション通信異常の出力側エラー |
| 8 | unGetInputData_ConnectionNo1 | ワード[符号なし]/ビット列[16ビット](0..63) | VAR_GLOBAL | D0 | コネクションNo.1 入力データ |
| 9 | unGetinputData_ConnectionNo2 | ワード[符号なし]/ビット列[16ビット](0..127) | VAR_GLOBAL | D200 | コネクションNo.2 入力データ |
| 10 | bStopCommunication | ビット | VAR_GLOBAL | M200 | 通信停止指示 |

> CPUユニットによって，デフォルトのラッチ範囲では，変換が通らないため，データレジスタ(D)のラッチ範囲を変更，またはデータレジスタ(D)を割り付けたラベルのクラスをVAR_GLOVAL_RETAINに定義してください。ラッチ設定については，下記を参照してください。
> MELSEC iQ-F FX5ユーザーズマニュアル(応用編)

【図】オリジネータ側ラダー（原本 p.142-143）

※ニモニックは原本に記載なし。図から書き起こしたもの。ステップ番号 (n) は原本ラダー図の表示値。

```
(0)
LD    U1\G35.F                 FX5EIP_1.bSts_CommunicationReady_D 通信READY
ANI   M200                     bStopCommunication (b接点)
OUT   M0                       bnRequest_GetInputData[0]
OUT   M1                       bnRequest_GetInputData[1]
AND<>_U K1 U1\G273             FX5EIP_1.stEIPArea64.uSts_CommunicationStart_D
AND=_U  K0 U1\G272             FX5EIP_1.stEIPArea64.uSet_CommunicationStart_D
MOV   H10 U1\G272              FX5EIP_1.stEIPArea64.uSet_CommunicationStart_D

(27)
LD    M0                       bnRequest_GetInputData[0]
FB呼出し M_FX5_EIP_Class1GetInputData_00A_1 (M+FX5-EIP_Class1GetInputData_00A)  ※ピン割付は下表

(759)
LD    M1                       bnRequest_GetInputData[1]
AND=_U  H1 U1\G273             FX5EIP_1.stEIPArea64.uSts_CommunicationStart_D
AND   U1\G35.F                 FX5EIP_1.bSts_CommunicationReady_D
MPS
AND   U1\G1328.1               FX5EIP_1.stEIPArea64.unSts_CyclicDataLink_Connection_D[1].1
ANI   U1\G1336.1               FX5EIP_1.stEIPArea64.unSts_CyclicError_Connection_D[1].1 (b接点)
BMOV  D200 W100 U1\G305        unGetInputData_ConnectionNo2 → W100, 点数 FX5EIP_1.stEIPArea64.unVal_InputDataSize_Connection_D[2]
MPP
ANI   U1\G1328.1               FX5EIP_1.stEIPArea64.unSts_CyclicDataLink_Connection_D[1].1 (b接点)
AND   U1\G1336.1               FX5EIP_1.stEIPArea64.unSts_CyclicError_Connection_D[1].1
DMOV  U1\G1394 D2003           FX5EIP_1.stEIPArea64.udnSts_CyclicErrorStatus_Connection_In_D[2] → undStatusId_GetInputData[1]
DMOV  U1\G1650 D2007           FX5EIP_1.stEIPArea64.udnSts_CyclicErrorStatus_Connection_Out_D[2] → undStatusId_GetOutputData[1]

(804)
LD    M200                     bStopCommunication
RST   M0                       bnRequest_GetInputData[0]
RST   M1                       bnRequest_GetInputData[1]
ANI   M10                      bnRun_GetInputData (b接点)
AND=_U  K1 U1\G273             FX5EIP_1.stEIPArea64.uSts_CommunicationStart_D
MOV   K0 U1\G272               FX5EIP_1.stEIPArea64.uSet_CommunicationStart_D

(824)
END
```

ステップ(27) FB M_FX5_EIP_Class1GetInputData_00A_1（M+FX5-EIP_Class1GetInputData_00A / Get Class1 input data）のピン割付（図から書き起こし）:

| 方向 | ピン | 型 | 接続 |
|---|---|---|---|
| 入力 | i_bEN | B | M0（bnRequest_GetInputData[0]） |
| 入力 | i_stModule | DUT | FX5EIP_1 |
| 入力 | i_uConnectionNo | UW | K1 |
| 出力 | o_bENO | B | M10（bnRun_GetInputData） |
| 出力 | o_bOK | B | M20（bnOK_GetInputData） |
| 出力 | o_bErr | B | M30（bnNG_GetInputData） |
| 出力 | o_uErrId | UW | D2000（unErrorCode_GetInputData） |
| 出力 | o_udStatusId_IN | UD | D2001（undStatusId_GetInputData[0]） |
| 出力 | o_udStatusId_OUT | UD | D2005（undStatusId_GetOutputData[0]） |
| 出力 | o_uInputData | UW | D0（unGetInputData_ConnectionNo1） |

説明（原文）:
- (0) コネクションNo.1からの入力データの取得とコネクションNo.2からの入力データの取得を開始し，EtherNet/IP通信を開始します。
- (27) M0がONのとき，M+FX5-EIP_Class1GetInputDataが実行されて，コネクションNo.1の入力データの取得を行います。
  M20がONのとき，ターゲット1から受信した入力データを，D0からコネクションNo.1に設定したデータサイズ分格納され続けます。
- (759) M1がONのとき，コネクションNo.2のʼサイクリック通信データリンク状態ʼ(U1￥G1328.1)が正常の間，ターゲット2から受信した入力データを，D200からコネクションNo.2に設定したデータサイズ分リフレッシュされ，W100以降にコピーします。
- (804) M200をONすることで，入力データの取得を停止して，EtherNet/IP通信を停止します。

##### ターゲット1側のプログラム (8.2 / 印刷 p.142 / 原本 p.144)

| 分類 | ラベル名 | 内容 | デバイス |
|---|---|---|---|
| ユニットラベル | FX5EIP_1.bSts_CommunicationReady_D | 通信READY | U1￥G35.F |
| ユニットラベル | FX5EIP_1.stEIPArea64.uSet_CommunicationStart_D | EtherNet/IP通信起動要求 | U1￥G272 |
| ユニットラベル | FX5EIP_1.stEIPArea64.uSts_CommunicationStart_D | EtherNet/IP通信起動状態 | U1￥G273 |
| 定義するラベル | 下記のように，グローバルラベルを定義します。（下表） | | |
| 使用ファンクションブロック | M+FX5-EIP_Class1SetOutputData | | |

定義するラベル（グローバルラベル設定画面）:

| No. | ラベル名 | データ型 | クラス | 割付け(デバイス/ラベル) | Japanese/日本語(表示対象) |
|---|---|---|---|---|---|
| 1 | bStopCommunication | ビット | VAR_GLOBAL | M200 | 通信停止指示 |
| 2 | bnRequest_GetOutputData | ビット | VAR_GLOBAL | M0 | 出力データ設定 実行 |
| 3 | bnRun_GetOutputData | ビット | VAR_GLOBAL | M10 | 出力データ設定 FB実行中 |
| 4 | bnOK_GetOutputData | ビット | VAR_GLOBAL | M20 | 出力データ設定 FB正常 |
| 5 | bnNG_GetOutputData | ビット | VAR_GLOBAL | M30 | 出力データ設定 FB異常 |
| 6 | unGetOutputData_ConnectionNo1 | ワード[符号なし]/ビット列[16ビット](0..63) | VAR_GLOBAL | D0 | コネクションNo.1 出力データ |
| 7 | unErrorCode_GetOutputData | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D2000 | 出力データ設定 異常時のエラーコード |
| 8 | undStatusId_GetinputErrorCode | ダブルワード[符号なし]/ビット列[32ビット] | VAR_GLOBAL | D2001 | 出力データ設定 コネクション通信異常の入力側エラー |
| 9 | undStatusId_GetOutputErrorCode | ダブルワード[符号なし]/ビット列[32ビット] | VAR_GLOBAL | D2003 | 出力データ設定 コネクション通信異常の出力側エラー |

> CPUユニットによって，デフォルトのラッチ範囲では，変換が通らないため，データレジスタ(D)のラッチ範囲を変更，またはデータレジスタ(D)を割り付けたラベルのクラスをVAR_GLOVAL_RETAINに定義してください。ラッチ設定については，下記を参照してください。
> MELSEC iQ-F FX5ユーザーズマニュアル(応用編)

【図】ターゲット1側ラダー（原本 p.144）

※ニモニックは原本に記載なし。図から書き起こしたもの。ステップ番号 (n) は原本ラダー図の表示値。

```
(0)
LD    U1\G35.F                 FX5EIP_1.bSts_CommunicationReady_D 通信READY
ANI   M200                     bStopCommunication (b接点)
OUT   M0                       bnRequest_GetOutputData

(7)
LD    M0                       bnRequest_GetOutputData
FB呼出し M_FX5_EIP_Class1SetOutputData_00A_1 (M+FX5-EIP_Class1SetOutputData_00A)  ※ピン割付は下表

(728)
LD    M200                     bStopCommunication
RST   M0                       bnRequest_GetOutputData
AND   M10                      bnRun_GetOutputData (a接点)
AND=_U  K1 U1\G273             FX5EIP_1.stEIPArea64.uSts_CommunicationStart_D
MOV   K0 U1\G272               FX5EIP_1.stEIPArea64.uSet_CommunicationStart_D

(746)
END
```

ステップ(7) FB M_FX5_EIP_Class1SetOutputData_00A_1（M+FX5-EIP_Class1SetOutputData_00A / Set Class1 Output data）のピン割付（図から書き起こし）:

| 方向 | ピン | 型 | 接続 |
|---|---|---|---|
| 入力 | i_bEN | B | M0（bnRequest_GetOutputData） |
| 入力 | i_stModule | DUT | FX5EIP_1 |
| 入力 | i_uConnectionNo | UW | K1 |
| 入力 | i_uOutputData | UW | D0（unGetOutputData_ConnectionNo1） |
| 出力 | o_bENO | B | M10（bnRun_GetOutputData） |
| 出力 | o_bOK | B | M20（bnOK_GetOutputData） |
| 出力 | o_bErr | B | M30（bnNG_GetOutputData） |
| 出力 | o_uErrId | UW | D2000（unErrorCode_GetOutputData） |
| 出力 | o_udStatusId_IN | UD | D2001（undStatusId_GetinputErrorCode） |
| 出力 | o_udStatusId_OUT | UD | D2003（undStatusId_GetOutputErrorCode） |

説明（原文）:
- (0) コネクションNo.1への出力データ処理を設定して，EtherNet/IP通信を開始します。
- (7) M0がONのとき，M+FX5-EIP_Class1SetOutputDataが実行されて，コネクションNo.2の出力データの設定を行います。
  M20がONのとき，D0以降に設定した出力データを，コネクションNo.1に設定したデータサイズ分オリジネータに対して送信します。
- (644) M200をONすることで，出力データの設定を停止して，EtherNet/IP通信を停止します。

##### ターゲット2側のプログラム (8.2 / 印刷 p.143 / 原本 p.145)

| 分類 | ラベル名 | 内容 | デバイス |
|---|---|---|---|
| ユニットラベル | FX5EIP_1.bSts_CommunicationReady_D | 通信READY | U1￥G35.F |
| ユニットラベル | FX5EIP_1.stEIPArea64.uSet_CommunicationStart_D | EtherNet/IP通信起動要求 | U1￥G272 |
| ユニットラベル | FX5EIP_1.stEIPArea64.uSts_CommunicationStart_D | EtherNet/IP通信起動状態 | U1￥G273 |
| ユニットラベル | FX5EIP_1.stEIPArea128.unVal_OutputDataSize_Connection_D[1] | 出力/メッセージ通信(サーバ)データサイズ | U1￥G432 |
| ユニットラベル | FX5EIP_1.stEIPArea64.bnSts_CyclicDataLink_Connection_D[1] | サイクリック通信データリンク状態 | U1￥G1328.0 |
| ユニットラベル | FX5EIP_1.stEIPArea64.unSts_CyclicError_Connection_D[1].0 | サイクリック通信異常状態 | U1￥G1336.0 |
| ユニットラベル | FX5EIP_1.stEIPArea64.udnSts_CyclicErrorStatus_Connection_In_D[1] | サイクリック通信入力エラー状態 | U1￥G1392 |
| ユニットラベル | FX5EIP_1.stEIPArea64.udnSts_CyclicErrorStatus_Connection_Out_D[1] | サイクリック通信出力エラー状態 | U1￥G1648 |
| 定義するラベル | 下記のように，グローバルラベルを定義します。（下表） | | |

（ターゲット2側の表には「使用ファンクションブロック」の行なし）

定義するラベル（グローバルラベル設定画面）:

| No. | ラベル名 | データ型 | クラス | 割付け(デバイス/ラベル) | Japanese/日本語(表示対象) |
|---|---|---|---|---|---|
| 1 | bStopCommunication | ビット | VAR_GLOBAL | M200 | 通信停止指示 |
| 2 | bnRequest_GetOutputData | ビット | VAR_GLOBAL | M0 | 出力データ設定実行 |
| 3 | unGetOutputData_ConnectionNo1 | ワード[符号なし]/ビット列[16ビット](0..63) | VAR_GLOBAL | D0 | コネクションNo.1 出力データ |
| 4 | undStatusId_GetInputErrorCode | ダブルワード[符号なし]/ビット列[32ビット] | VAR_GLOBAL | D2001 | 出力データ設定コネクション通信異常の入力側エラー |
| 5 | undStatusId_GetOutputErrorCode | ダブルワード[符号なし]/ビット列[32ビット] | VAR_GLOBAL | D2003 | 出力データ設定コネクション通信異常の出力側エラー |

> CPUユニットによって，デフォルトのラッチ範囲では，変換が通らないため，データレジスタ(D)のラッチ範囲を変更，またはデータレジスタ(D)を割り付けたラベルのクラスをVAR_GLOVAL_RETAINに定義してください。ラッチ設定については，下記を参照してください。
> MELSEC iQ-F FX5ユーザーズマニュアル(応用編)

【図】ターゲット2側ラダー（原本 p.145）

※ニモニックは原本に記載なし。図から書き起こしたもの。ステップ番号 (n) は原本ラダー図の表示値。

```
(0)
LD    U1\G35.F                 FX5EIP_1.bSts_CommunicationReady_D 通信READY
ANI   M200                     bStopCommunication (b接点)
OUT   M0                       bnRequest_GetOutputData
AND   U1\G35.F                 FX5EIP_1.bSts_CommunicationReady_D (分岐側にも再度a接点あり)
AND=_U  K0 U1\G272             FX5EIP_1.stEIPArea64.uSet_CommunicationStart_D
MOV   H10 U1\G272              FX5EIP_1.stEIPArea64.uSet_CommunicationStart_D

(22)
LD    M0                       bnRequest_GetOutputData
AND=_U  K1 U1\G273             FX5EIP_1.stEIPArea64.uSts_CommunicationStart_D
AND   U1\G35.F                 FX5EIP_1.bSts_CommunicationReady_D
MPS
AND   U1\G1328.0               FX5EIP_1.stEIPArea64.unSts_CyclicDataLink_Connection_D[1].0
ANI   U1\G1336.0               FX5EIP_1.stEIPArea64.unSts_CyclicError_Connection_D[1].0 (b接点)
BMOV  W0 D0 U1\G432            W0 → unGetOutputData_ConnectionNo1[0], 点数 FX5EIP_1.stEIPArea128.unVal_OutputDataSize_Connection_D[1]
MPP
ANI   U1\G1328.0               FX5EIP_1.stEIPArea64.unSts_CyclicDataLink_Connection_D[1].0 (b接点)
AND   U1\G1336.0               FX5EIP_1.stEIPArea64.unSts_CyclicError_Connection_D[1].0
DMOV  U1\G1392 D2001           FX5EIP_1.stEIPArea64.udnSts_CyclicErrorStatus_Connection_In_D[1] → undStatusId_GetInputErrorCode
DMOV  U1\G1648 D2003           FX5EIP_1.stEIPArea64.udnSts_CyclicErrorStatus_Connection_Out_D[1] → undStatusId_GetOutputErrorCode

(67)
LD    M200                     bStopCommunication
RST   M0                       bnRequest_GetOutputData
AND=_U  K1 U1\G273             FX5EIP_1.stEIPArea64.uSts_CommunicationStart_D
AND<>_U K0 U1\G272             FX5EIP_1.stEIPArea64.uSet_CommunicationStart_D
MOV   K0 U1\G272               FX5EIP_1.stEIPArea64.uSet_CommunicationStart_D

(89)
END
```

（ラダー図上のコメント表記: U1￥G1328.0 / U1￥G1336.0 の接点は「FX5EIP_1.stEIPArea64.unSts_CyclicDataLink_Connection_D[1].0」「FX5EIP_1.stEIPArea64.unSts_CyclicError_Connection_D[1].0」と表示。使用デバイス表の U1￥G1328.0 のラベル名は「FX5EIP_1.stEIPArea64.bnSts_CyclicDataLink_Connection_D[1]」）

説明（原文）:
- (0) コネクションNo.1への出力データ処理を設定して，EtherNet/IP通信を開始します。
- (22) M0がONのとき，コネクションNo.1のʼサイクリック通信データリンク状態ʼ(U1￥G1328.0)が正常の間，W0以降に格納したデータを出力データとしてD0以降にコピーします。
  D0以降に格納されたデータは，リフレッシュ点数分送信データとしてリフレッシュされ，オリジネータに対して送信されます。
- (67) M200をONすることで，出力データの設定を停止して，EtherNet/IP通信を停止します。

## 転記時の要確認一覧 (8.2 / 原本 p.133-145)

- 原本 p.144 ターゲット1側の説明文は「(644) M200をONすることで…」だが、同ページのラダー図上の該当ステップ番号は (728)（END は (746)）。原文どおり (644) のまま転記。
- 原本 p.144 ターゲット1側の説明文 (7) は「コネクションNo.2の出力データの設定を行います」だが、ラダー図のFB入力 i_uConnectionNo は K1、次行の説明も「コネクションNo.1に設定したデータサイズ分」。原文どおり転記。
- 原本 p.144 ターゲット1側 (728) の M10(bnRun_GetOutputData) は a接点、原本 p.143 オリジネータ側 (804) の M10(bnRun_GetInputData) は b接点として描かれている（拡大画像で確認、図のとおり書き起こし）。
- 原本 p.142 オリジネータ側ラベル定義 No.9 は「unGetinputData_ConnectionNo2」（i小文字）、ラダー図上は「unGetInputData_ConnectionNo2」。p.144 ターゲット1側 No.8「undStatusId_GetinputErrorCode」（i小文字）、p.145 ターゲット2側 No.4「undStatusId_GetInputErrorCode」。いずれも原本表記のまま。
- 原本 p.140 / p.141 のターゲット1・ターゲット2の書込み手順は「オリジネータ側のCPUユニットに書き込み」と記載（原文どおり）。
- 原本の「VAR_GLOVAL_RETAIN」表記は原文どおり。
