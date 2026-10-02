# 三菱 FR-E800 取扱説明書（通信編） 第2章 2.13 EtherCAT

| 項目 | 内容 |
|---|---|
| 原本 | 三菱電機 FR-E800 取扱説明書（通信編） |
| 発行元 | 三菱電機株式会社 |
| 資料番号 / 版数 | IB-0600870 / S版（PDFメタデータ subject: IB-0600870-S） |
| 原本PDF | `PDF/【三菱】インバータ FR-E800 取扱説明書(通信編)_ib0600870s.pdf` (全330ページ) |
| 本ファイルの範囲 | 2.13 (印刷 p.194-218 / PDF p.195-219) |
| ページ対応 | 「原本 p.」はPDFのページ番号、「印刷 p.」は原本フッタのページ番号。印刷ページ = PDFページ − 1。本文中の「〇〇ページ参照」は印刷ページ |
| 変換日 | 2026-10-02 |
| 変換方法 | pypdfium2(本文) + PyMuPDF 200dpi 画像の目視(全ページ) |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。

**転記上の扱い**: 原本の結合セルは各行に値を展開。セル内改行は `<br>`。左右並置の表は方向ごとに別表に分割した場合あり（各所に注記）。機種アイコンは `[E800]` `[E800-(SC)E]` 等。図は【図】プレースホルダ＋読み取れる事実の箇条書き。ラダー図のニモニックは原本に記載がなく、図から書き起こしたもの（各所に注記）。見出しレベル: 章 `##` / 節 `###` / 項 `####` / ◆ `#####` / ■ `######`。

---

## 主要用語 対訳表 (Glossary) (2.13 / 原本 p.195-219)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| EtherCAT ステートマシン | EtherCAT State Machine | ESM | 原本併記 |
| PDO 通信 | Process Data Object communication | PDO | 原本併記 |
| SDO 通信 | Service Data Object communication | SDO | 原本併記 |
| CoE | CAN application protocol over EtherCAT | CoE | 原本併記 |
| SII | Slave Information Interface | SII | 原本併記 |
| CiA402 ドライブプロファイル | CiA402 drive profile | CiA402 | 参考訳 |
| ノードアドレス設定 | EtherCAT node address setting | Pr.1305 / N690 | 参考訳 |
| 周期通信入力データ選択 | Cyclic communication input data selection | Pr.1320～1329 / N810～N819 | 参考訳 |
| 周期通信出力データ選択 | Cyclic communication output data selection | Pr.1330～1343 / N850～N863 | 参考訳 |
| 周期通信入力データ選択サブ | Cyclic communication input data sub-index selection | Pr.1389～1393 / N830～N839 | 参考訳 |
| 周期通信出力データ選択サブ | Cyclic communication output data sub-index selection | Pr.1394～1398 / N870～N879 | 参考訳 |
| PDO アサインオブジェクト | PDO assign object | Index H1C12、H1C13 | 参考訳 |
| PDO マッピングオブジェクト | PDO mapping object | Index H1600、H1620、H1A00、H1A20 | 参考訳 |
| 受信PDOマッピング | receive PDO mapping | RxPDO（マスタ→インバータ） | 原本併記 |
| 送信PDOマッピング | transmit PDO mapping | TxPDO（インバータ→マスタ） | 原本併記 |
| 制御ワード | Controlword | Index H6040 | 原本併記 |
| ステータスワード | Statusword | Index H6041 | 原本併記 |
| 設定速度 | vl target velocity | Index H6042 | 原本併記 |
| 出力周波数（r/min） | vl velocity demand | Index H6043 | 原本併記 |
| 運転速度 | vl velocity actual value | Index H6044 | 原本併記 |
| 加速度 / 減速度 | vl velocity acceleration / deceleration | Index H6048 / H6049 | 原本併記 |
| 急速停止 | vl velocity quick stop | Index H604A | 原本併記 |
| 制御モード | Modes of operation | Index H6060 | 原本併記 |
| ベンダ固有運転モード | vendor-specific operation mode | -1 | 参考訳 |
| メーカ固有エリア | manufacturer-specific area | H3000～H5FFF | 参考訳 |
| シンクマネージャ | Sync Manager | SM | 参考訳 |
| 分岐スレーブ | EtherCAT junction slave | - | 参考訳 |
| ローカルサイクルタイム | local cycle time | 4ms | 参考訳 |
| メールボックス通信 | Mailbox communication | SDO | 原本併記 |
| PDS 状態遷移 | PDS (power drive system) state transition | - | 原本併記 |
| 目標位置 | Target position | H607A | 原本併記 |
| 設定トルク | Target torque | H6071 / Pr.805 | 原本併記 |
| 現在位置 | Position actual value | H6064 | 原本併記 |
| 溜りパルス | Following error actual value | H60F4 | 原本併記 |
| 溜りパルスエラー判定値 | Following error window | H6065 | 原本併記 |
| 位置決め完了判定値 | Position window | H6067 | 原本併記 |
| 原点復帰方法 | Homing method | H6098 | 原本併記 |
| 原点復帰速度 | Homing speeds | H6099 | 原本併記 |
| 原点復帰加減速時間 | Homing acceleration | H609A | 原本併記 |
| 加速時定数 | Profile acceleration | H6083 / Pr.7 | 原本併記 |
| 減速時定数 | Profile deceleration | H6084 / Pr.8 | 原本併記 |
| 減速時定数（QuickStop） | Quick stop deceleration | H6085 / Pr.464, Pr.1103 | 原本併記 |
| ギア比 | Gear ratio | H6091 / Pr.420, Pr.421 | 原本併記 |
| PLG 分解能 | Position encoder resolution | H608F / Pr.369 | 原本併記 |
| ダイレクトコマンドモード | direct command mode | - | 参考訳 |
| 出力遮断 | output shutoff | RY 信号 | 参考訳 |
| 重故障 | fault | - | 参考訳 |
| 軽故障 | minor fault | - | 参考訳 |
| 警報 | warning (alarm) | - | 参考訳 |
| 非常停止 | emergency stop | X92 / Pr.1103 | 参考訳 |
| 急停止 | quick stop | X87 / Pr.464 | 参考訳 |
| 原点無視（サーボ ON 位置原点） | homing ignored (servo-ON position as home) | H6098=-5 | 参考訳 |
| ドグ式 | dog type | - | 参考訳 |
| 押当て式 | stopper type | - | 参考訳 |
| データセット式 | data set type | H6098=-3 | 参考訳 |
| エマージェンシードライブ | emergency drive | - | 参考訳 |
| 指令権 | command source | Pr.550, Pr.338 | 参考訳 |
| 校正パラメータ | Calibration parameters | C0〜C45 (Pr.900〜Pr.935) | 参考訳 |
| モニタデータ | Monitor data | Monitor data #nnnn / H4000〜 | 原本併記 |
| インバータ制御パラメータ | Inverter control parameters | H5002〜H5FFF | 参考訳 |
| インバータリセット | Inverter reset | H5002 | 参考訳 |
| パラメータクリア | Parameter clear | H5003 / H5006 | 参考訳 |
| パラメータオールクリア | All parameter clear | H5004 / H5007 | 参考訳 |
| 制御入力命令 | Control input command | H5009 | 参考訳 |
| インバータ状態 | Inverter status | H5009 | 参考訳 |
| アラーム履歴 | Alarm history | H51F5〜H51FE | 参考訳 |
| Safety 入力状態 | Safety input status | H5200 | 参考訳 |
| CoE 通信エリア | CoE communication area | H1000〜H1C33 | 参考訳 |
| マッピングオブジェクト | Mapped object | Mapped Object 001〜 | 原本併記 |
| サブインデックスの最大値 | Highest sub-index supported | Sub index H00 | 原本併記 |
| メールボックス受信/送信 | Mailbox receive/send | Sync Manager 0/1 | 参考訳 |
| 同期モード | Synchronization type | H1C32/H1C33 Sub H01 | 原本併記 |
| 断線検出機能 | Disconnection detection function | Pr.1431 / Pr.1457 | 参考訳 |
| ステータス遷移異常 | Status transition error | - | 参考訳 |
| PDO 通信タイムアウト | PDO communication timeout | - | 参考訳 |
| ウォッチドッグタイマ | Watchdog timer | 100ms（初期値） | 参考訳 |
| 通信異常時停止モード選択 | Stop mode selection at communication error | Pr.502 | 参考訳 |
| パラメータ記憶素子異常 | Parameter storage device fault | E.PE | 参考訳 |
| 速度指令 | Speed command | vl target velocity (H6042) | 原本併記 |
| 通信 EEPROM 書込み選択 | Communication EEPROM write selection | Pr.342 | 参考訳 |

## 変換範囲表 (2.13 / 原本 p.195-219)

| 原本ページ | 節 | 扱い |
|---|---|---|
| p.195-219 | 2.13 EtherCAT | 全文 |
| 上記以外 | 他章 | 同フォルダの他ファイル参照（前付け p.1-6 表紙・目次は未変換） |

## 目次 (2.13)

- [2.13 EtherCAT (2.13 / 印刷 p.194 / 原本 p.195)](#213-ethercat-213--印刷-p194--原本-p195)
  - [2.13.1 概要 (2.13.1 / 印刷 p.194 / 原本 p.195)](#2131-概要-2131--印刷-p194--原本-p195)
  - [2.13.2 EtherCAT 関連パラメータ (2.13.2 / 印刷 p.195 / 原本 p.196)](#2132-ethercat-関連パラメータ-2132--印刷-p195--原本-p196)
  - [2.13.3 EtherCAT ステートマシン（ESM） (2.13.3 / 印刷 p.197 / 原本 p.198)](#2133-ethercat-ステートマシンesm-2133--印刷-p197--原本-p198)
  - [2.13.4 PDO（Process Data Object）通信 (2.13.4 / 印刷 p.198 / 原本 p.199)](#2134-pdoprocess-data-object通信-2134--印刷-p198--原本-p199)
  - [2.13.5 CoE オブジェクトディクショナリ (2.13.5 / 印刷 p.200 / 原本 p.201)](#2135-coe-オブジェクトディクショナリ-2135--印刷-p200--原本-p201)
  - [2.13.6 異常発生時の動作 (2.13.6 / 印刷 p.217 / 原本 p.218)](#2136-異常発生時の動作-2136--印刷-p217--原本-p218)
  - [2.13.7 プログラミング例 (2.13.7 / 印刷 p.217 / 原本 p.218)](#2137-プログラミング例-2137--印刷-p217--原本-p218)

---

### 2.13 EtherCAT (2.13 / 印刷 p.194 / 原本 p.195)

#### 2.13.1 概要 (2.13.1 / 印刷 p.194 / 原本 p.195)

【図】EtherCAT ロゴ (原本 p.195)

EtherCAT は、FR-E800-(SC)EPC のみ使用可能です。
インバータの Ethernet コネクタ経由で EtherCAT による通信運転やパラメータ設定ができます。
インバータの製造時期によっては対応しません。仕様変更の内容については 318 ページを参照してください。

##### ◆ 通信仕様 (2.13.1 / 原本 p.195)

| 項目 | | 内容 |
|---|---|---|
| 通信速度 | | 100Mbps（全二重） |
| 最大接続台数 | | 65535 台 *1 |
| 接続ケーブル | | Ethernet ケーブル（IEEE802.3 100BASE-TX 規定ケーブル、ANSI/TIA/EIA-568-B（Category 5e）準拠の 4 ペア平衡型シールドケーブル） |
| トポロジ | | ライン、スター、リング、ライン・スター混在 *2 |
| PDO（Process Data Object）通信 | 通信形式 | サイクリック通信 |
| PDO（Process Data Object）通信 | 通信周期 | マスタによる |
| SDO（Service Data Object）通信 | 通信形式 | Mailbox 通信（非周期通信） |
| 同期モード | | Free-run mode<br>ローカルサイクルタイム：4ms |

*1 マスタの仕様により変わります。
*2 スター接続またはリング接続の場合、汎用スイッチングハブは使用できません。EtherCAT 分岐スレーブが必要になります。

##### ◆ 配線方法 (2.13.1 / 原本 p.195)

- FR-E800-(SC)EPC は、通信用コネクタ PORT1 が IN、通信用コネクタ PORT2 が OUT となります。マスタ局または上位局を PORT1 に接続し、下位局を PORT2 に接続します。

【図】EtherCAT 配線例（インバータ2台のデイジーチェーン接続） (原本 p.195)
- インバータ2台を左右に並べた図。各インバータに「通信用コネクタ（PORT1）」= IN、「通信用コネクタ（PORT2）」= OUT の表示
- 左側インバータの IN（PORT1）からのケーブルが「マスタ局、上位局」へ
- 左側インバータの OUT（PORT2）から右側インバータの IN（PORT1）へケーブル接続（途中に省略記号の波線）
- 右側インバータの OUT（PORT2）からのケーブルが「下位局」へ

##### ◆ 運転状態モニタ用 LED (2.13.1 / 原本 p.195)

【図】操作パネル (原本 p.195)
- 4桁7セグメント表示部、Hz / A 表示、PU / EXT / NET / MON / PRM / P.RUN / RUN / PM の各ランプ
- キー：PU/EXT、MODE、SET、↑、RUN、STOP/RESET、↓
- 右下に LED「EC RN」「EC ER」「L/A 1」「L/A 2」が縦に並ぶ

| LED 名称 | 内容 | LED 状態 | 備考 |
|---|---|---|---|
| EC RN | EtherCAT ステートマシン（ESM）の状態 | 消灯 | 電源 OFF/Init ステート |
| EC RN | EtherCAT ステートマシン（ESM）の状態 | 緑点滅（200ms 間隔） | Pre-Operational ステート |
| EC RN | EtherCAT ステートマシン（ESM）の状態 | 緑 1 回点滅 | Safe-Operational ステート |
| EC RN | EtherCAT ステートマシン（ESM）の状態 | 緑点滅（50ms 間隔） | Initialization ステート |
| EC RN | EtherCAT ステートマシン（ESM）の状態 | 緑点灯 | Operational ステート |
| EC ER | エラー状態 | 消灯 | 異常なし |
| EC ER | エラー状態 | 赤点滅（200ms 間隔） | マスタが要求した EtherCAT ステートに変更不可 |
| EC ER | エラー状態 | 赤 1 回点滅 | 内部異常により EtherCAT ステートが変更 |
| EC ER | エラー状態 | 赤 2 回点滅 | シンクマネージャ（SM）のウォッチドッグ異常 |
| EC ER | エラー状態 | 赤点滅（50ms 間隔） | 始動時に異常を検出 |
| L/A 1 | 通信用コネクタ (PORT1) 状態 | 消灯 | 電源 OFF/ リンクダウン |
| L/A 1 | 通信用コネクタ (PORT1) 状態 | 緑点滅（50ms 間隔） | リンクアップ（データ受信中） |
| L/A 1 | 通信用コネクタ (PORT1) 状態 | 緑点灯 | リンクアップ |
| L/A 2 | 通信用コネクタ (PORT2) 状態 | 消灯 | 電源 OFF/ リンクダウン |
| L/A 2 | 通信用コネクタ (PORT2) 状態 | 緑点滅（50ms 間隔） | リンクアップ（データ受信中） |
| L/A 2 | 通信用コネクタ (PORT2) 状態 | 緑点灯 | リンクアップ |

##### ◆ ESI ファイルについて (2.13.1 / 原本 p.196)

ESI ファイルがインターネットよりダウンロードできます。

三菱電機 FA サイト
https://www.MitsubishiElectric.co.jp/fa/products/drv/inv/support/e800/network.html
より無料でダウンロードできます。詳しくはお買い上げ店または当社営業所までご連絡ください。

> **NOTE**
> - ESI ファイルはエンジニアリングツールを使用することを前提としております。ESI ファイルの適切なインストール方法についてはエンジニアリングツールの取扱説明書を参照してください。

#### 2.13.2 EtherCAT 関連パラメータ (2.13.2 / 印刷 p.195 / 原本 p.196)

EtherCAT で通信を行う場合に関係するパラメータです。必要に応じて設定を行ってください。

| Pr. | 名称 | 初期値 | 設定範囲 | 内容 |
|---|---|---|---|---|
| 1305<br>N690*1 | EtherCAT ノードアドレス設定 | 0 | 0 ～ 65535 | マスタがインバータを識別するためのノードアドレスを設定します。 |
| 1320<br>N810*1 | 周期通信入力データ選択 1 | 24642 | 12288 ～ 13787、20488、20489、24642、24646、24648 ～ 24650、24672、24677 ～ 24680、24689、24698、24702、24703、24705、24707 ～ 24709、24719、24721、24728 ～ 24730、24831、9999 | インバータパラメータ、インバータ制御パラメータ、CiA402 ドライブプロファイルのインデックス番号を設定します。<br>PDO マッピングオブジェクトの RxPDO（マスタ→インバータ）に機能を割り付けることができます。<br>9999：機能無効 |
| 1321 ～ 1329<br>N811 ～ N819*1 | 周期通信入力データ選択 2 ～ 10 | 9999 | 12288 ～ 13787、20488、20489、24642、24646、24648 ～ 24650、24672、24677 ～ 24680、24689、24698、24702、24703、24705、24707 ～ 24709、24719、24721、24728 ～ 24730、24831、9999 | インバータパラメータ、インバータ制御パラメータ、CiA402 ドライブプロファイルのインデックス番号を設定します。<br>PDO マッピングオブジェクトの RxPDO（マスタ→インバータ）に機能を割り付けることができます。<br>9999：機能無効 |
| 1330<br>N850*1 | 周期通信出力データ選択 1 | 24643 | 12288 ～ 13787、16384 ～ 16483、20488、20489、20981 ～ 20990、20992、24639、24643、24644、24673 ～ 24676、24692、24695、24820、24826、24828、25858、9999 | インバータパラメータ、モニタデータ、インバータ制御パラメータ、CiA402 ドライブプロファイルのインデックス番号を設定します。<br>PDO マッピングオブジェクトの TxPDO（インバータ→マスタ）に機能を割り付けることができます。<br>9999：機能無効 |
| 1331 ～ 1343<br>N851 ～ N863*1 | 周期通信出力データ選択 2 ～ 14 | 9999 | 12288 ～ 13787、16384 ～ 16483、20488、20489、20981 ～ 20990、20992、24639、24643、24644、24673 ～ 24676、24692、24695、24820、24826、24828、25858、9999 | インバータパラメータ、モニタデータ、インバータ制御パラメータ、CiA402 ドライブプロファイルのインデックス番号を設定します。<br>PDO マッピングオブジェクトの TxPDO（インバータ→マスタ）に機能を割り付けることができます。<br>9999：機能無効 |
| 1389*1 | 周期通信入力データ選択サブ 1、2 | 0 | 0 ～ 2、256 ～ 258、512 ～ 514 | Pr.1389（下位 8bit）：Pr.1320 で指定したインデックス番号のサブインデックス<br>Pr.1389（上位 8bit）：Pr.1321 で指定したインデックス番号のサブインデックス |
| 1390*1 | 周期通信入力データ選択サブ 3、4 | 0 | 0 ～ 2、256 ～ 258、512 ～ 514 | Pr.1390（下位 8bit）：Pr.1322 で指定したインデックス番号のサブインデックス<br>Pr.1390（上位 8bit）：Pr.1323 で指定したインデックス番号のサブインデックス |
| 1391*1 | 周期通信入力データ選択サブ 5、6 | 0 | 0 ～ 2、256 ～ 258、512 ～ 514 | Pr.1391（下位 8bit）：Pr.1324 で指定したインデックス番号のサブインデックス<br>Pr.1391（上位 8bit）：Pr.1325 で指定したインデックス番号のサブインデックス |
| 1392*1 | 周期通信入力データ選択サブ 7、8 | 0 | 0 ～ 2、256 ～ 258、512 ～ 514 | Pr.1392（下位 8bit）：Pr.1326 で指定したインデックス番号のサブインデックス<br>Pr.1392（上位 8bit）：Pr.1327 で指定したインデックス番号のサブインデックス |
| 1393*1 | 周期通信入力データ選択サブ 9、10 | 0 | 0 ～ 2、256 ～ 258、512 ～ 514 | Pr.1393（下位 8bit）：Pr.1328 で指定したインデックス番号のサブインデックス<br>Pr.1393（上位 8bit）：Pr.1329 で指定したインデックス番号のサブインデックス |
| N830 ～ N839*1 | 周期通信入力データ選択サブ 1 ～ 10 | 0 | 0 ～ 2 | Pr.1320 ～ Pr.1329 で指定したインデックス番号のサブインデックス |
| 1394*1 | 周期通信出力データ選択サブ 1、2 | 0 | 0 ～ 2、256 ～ 258、512 ～ 514 | Pr.1394（下位 8bit）：Pr.1330 で指定したインデックス番号のサブインデックス<br>Pr.1394（上位 8bit）：Pr.1331 で指定したインデックス番号のサブインデックス |
| 1395*1 | 周期通信出力データ選択サブ 3、4 | 0 | 0 ～ 2、256 ～ 258、512 ～ 514 | Pr.1395（下位 8bit）：Pr.1332 で指定したインデックス番号のサブインデックス<br>Pr.1395（上位 8bit）：Pr.1333 で指定したインデックス番号のサブインデックス |
| 1396*1 | 周期通信出力データ選択サブ 5、6 | 0 | 0 ～ 2、256 ～ 258、512 ～ 514 | Pr.1396（下位 8bit）：Pr.1334 で指定したインデックス番号のサブインデックス<br>Pr.1396（上位 8bit）：Pr.1335 で指定したインデックス番号のサブインデックス |
| 1397*1 | 周期通信出力データ選択サブ 7、8 | 0 | 0 ～ 2、256 ～ 258、512 ～ 514 | Pr.1397（下位 8bit）：Pr.1336 で指定したインデックス番号のサブインデックス<br>Pr.1397（上位 8bit）：Pr.1337 で指定したインデックス番号のサブインデックス |
| 1398*1 | 周期通信出力データ選択サブ 9、10 | 0 | 0 ～ 2、256 ～ 258、512 ～ 514 | Pr.1398（下位 8bit）：Pr.1338 で指定したインデックス番号のサブインデックス<br>Pr.1398（上位 8bit）：Pr.1339 で指定したインデックス番号のサブインデックス |
| N870 ～ N879*1 | 周期通信出力データ選択サブ 1 ～ 10 | 0 | 0 ～ 2 | Pr.1330 ～ Pr.1339 で指定したインデックス番号のサブインデックス |

（注: 原本では Pr.1320 と Pr.1321～1329 の行で「設定範囲」「内容」セルが結合、Pr.1330 と Pr.1331～1343 の行でも同様に結合。各行に展開した）

*1 インバータリセット後、または次回電源 ON 時に設定値が反映されます。

> **NOTE**
> - FR-E800-(SC)EPC では、下記のパラメータは対応しません。
>   - デフォルトゲートウェイアドレス（Pr.442 ～ Pr.445）
>   - インバータ間リンク機能（Pr.1124、Pr.1125）
>   - リセット時 Ethernet 中継動作選択（Pr.1386）
>   - インバータ判別機能選択（Pr.1399）
>   - Ethernet 通信ネットワーク番号（Pr.1424）、Ethernet 通信局番（Pr.1425）
>   - リンク速度とデュプレックス（Pr.1426）
>   - Ethernet 機能選択（Pr.1427 ～ Pr.1430）
>   - Ethernet 通信チェック時間間隔（Pr.1432）
>   - IP アドレス（Pr.1434 ～ Pr.1437）
>   - サブネットマスク（Pr.1438 ～ Pr.1441）
>   - IP フィルタ機能（Ethernet）（Pr.1442 ～ Pr.1448）
>   - Ethernet 操作権指定 IP アドレス（Pr.1449 ～ Pr.1454）
>   - KeepAlive 時間（Pr.1455）
>   - ネットワーク診断選択（Pr.1456）
> - 2024 年 8 月以前に製造された FR-E800-EPC では、下記のパラメータは対応しません。
>   - Ethernet 断線検出機能選択 拡張パラメータ（Pr.1457）

##### ◆ ノードアドレス設定 (2.13.2 / 原本 p.198)

ノードアドレスは、エンジニアリングツールを使用して、マスタから自動的に設定する方法とインバータパラメータで設定する方法があります。

- Configured Station Alias（マスタから EtherCAT 通信でインバータの SII（Slave Information Interface）に設定する場合）
  エンジニアリングツールを使用して、Configured Station Alias を設定します。設定値は、インバータの電源再投入後に反映されます。
- Requesting ID（ID-Selector をインバータパラメータで設定する場合）
  Requesting ID に使用する Device ID を **Pr.1305 EtherCAT ノードアドレス設定**で設定します。

| Device ID | 設定範囲 |
|---|---|
| Pr.1305 | 1 ～ 65535（“0” は Device ID 未設定） |

#### 2.13.3 EtherCAT ステートマシン（ESM） (2.13.3 / 印刷 p.197 / 原本 p.198)

- 状態定義

【図】EtherCAT ステートマシン状態遷移図 (原本 p.198)
- Power on →(1)→ Init
- Init →(2)→ Pre-Operational、Pre-Operational →(3)→ Init
- Pre-Operational →(4)→ Safe-Operational、Safe-Operational →(5)→ Pre-Operational
- Safe-Operational →(6)→ Init
- Safe-Operational →(7)→ Operational、Operational →(8)→ Safe-Operational
- Operational →(9)→ Init
- Operational →(10)→ Pre-Operational

| 状態 | 内容 |
|---|---|
| Init（INIT） | 通信初期化 |
| Pre-Operational（PREOP） | SDO 通信可能 |
| Safe-Operational（SAFEOP） | SDO 通信可能<br>PDO 通信は TxPDO（インバータ→マスタ）送信のみ可能 |
| Operational（OP） | SDO 通信、PDO 通信可能<br>RxPDO（マスタ→インバータ）にマッピングされているオブジェクトに対して SDO 通信による書込みはできません。 |

- 遷移番号

| 遷移番号 | 内容 |
|---|---|
| (1) | 電源 ON、インバータリセット |
| (2) | マスタによる SDO 通信構成<br>マスタからの Pre-Operational ステート移行要求 |
| (4) | マスタによる PDO 通信構成<br>マスタからの Safe-Operational ステート移行要求 |
| (7) | マスタからの指令値出力開始<br>マスタからの Operational ステート移行要求 |
| (5)(10) | マスタからの Pre-Operational ステート移行要求 |
| (8) | マスタからの Safe-Operational ステート移行要求 |
| (3)(6)(9) | マスタからの Init ステート移行要求 |

#### 2.13.4 PDO（Process Data Object）通信 (2.13.4 / 印刷 p.198 / 原本 p.199)

PDO 通信は、マスタとインバータ間で一定周期でマスタからの指令データ（RxPDO）、インバータからのステータスデータ（TxPDO）の送受信を行います。通信データを任意に選択することができます。

##### ◆ PDO アサインオブジェクト (2.13.4 / 原本 p.199)

- 使用する PDO マッピングオブジェクトは、PDO アサインオブジェクト（Index H1C12、H1C13）に設定します。
- PDO アサインオブジェクトの設定を変更する場合は、Pre-Operational 状態のときに下記の手順で行ってください。

1. Sub index H00 に “0” を書き込む
2. Sub index H01 に使用する PDO マッピングオブジェクトのインデックス番号を書き込む
3. Sub index H00 に “1” を書き込む

##### ◆ PDO マッピングオブジェクト (2.13.4 / 原本 p.199)

- 送受信するデータの内容は PDO マッピングオブジェクトに設定されます。RxPDO として Index H1600、H1620、TxPDO として Index H1A00、H1A20 が対応します。
- Index H1600、H1A00 は、インバータパラメータでマッピング内容を変更できます。
- Index H1620、H1A20 は、SDO 通信によりマッピング内容を変更できます。設定を変更する場合は、Pre-Operational 状態のときに下記の手順で行ってください。

1. Sub index H00 に “0” を書き込む
2. Sub index H01 ～ H0n（n：データ数）に設定値を書き込む
3. Sub index H00 に使用するデータ数（n）を書き込む

###### ■ Index H1600（1st receive PDO mapping） (2.13.4 / 原本 p.199)

| Sub index | 名称 | マッピング内容（固定） | データ長（Bit） |
|---|---|---|---|
| H01 | Mapped Object 001 | Index H6040（Controlword） | 16 |
| H02 | Mapped Object 002 | Index H5FFE、Sub index H01（Index:Pr.1320,Sub:Pr.1389(Low)） | 32 |
| H03 | Mapped Object 003 | Index H5FFE、Sub index H02（Index:Pr.1321,Sub:Pr.1389(High)） | 32 |
| H04 | Mapped Object 004 | Index H5FFE、Sub index H03（Index:Pr.1322,Sub:Pr.1390(Low)） | 32 |
| H05 | Mapped Object 005 | Index H5FFE、Sub index H04（Index:Pr.1323,Sub:Pr.1390(High)） | 32 |
| H06 | Mapped Object 006 | Index H5FFE、Sub index H05（Index:Pr.1324,Sub:Pr.1391(Low)） | 32 |
| H07 | Mapped Object 007 | Index H5FFE、Sub index H06（Index:Pr.1325,Sub:Pr.1391(High)） | 32 |
| H08 | Mapped Object 008 | Index H5FFE、Sub index H07（Index:Pr.1326,Sub:Pr.1392(Low)） | 32 |
| H09 | Mapped Object 009 | Index H5FFE、Sub index H08（Index:Pr.1327,Sub:Pr.1392(High)） | 32 |
| H0A | Mapped Object 010 | Index H5FFE、Sub index H09（Index:Pr.1328,Sub:Pr.1393(Low)） | 32 |
| H0B | Mapped Object 011 | Index H5FFE、Sub index H0A（Index:Pr.1329,Sub:Pr.1393(High)） | 32 |

> **NOTE**
> - Pr.1320 ～ Pr.1329 に重複したインデックス番号を指定した場合、パラメータ番号が小さい方に設定した値が有効となり、パラメータ番号が大きい方に設定した値は “9999” として扱われます。
> - Pr.1320 ～ Pr.1329 に存在しないインデックス番号を指定した場合、または “9999” を設定した場合、データは H0 として扱われます。

###### ■ Index H1620（33rd receive PDO mapping） (2.13.4 / 原本 p.200)

| Sub index | 名称 | マッピング内容（初期値） | データ長（Bit） | 備考 |
|---|---|---|---|---|
| H01 | Mapped Object 001 | Index H6040（Controlword）（固定） | 16 | 変更不可 |
| H02 | Mapped Object 002 | Index H6042（vl target velocity） | 16 | データ数は可変（Sub index H00 で指定します。） |
| H03 | Mapped Object 003 | 機能なし | マッピング内容による | データ数は可変（Sub index H00 で指定します。） |
| H04 | Mapped Object 004 | 機能なし | マッピング内容による | データ数は可変（Sub index H00 で指定します。） |
| H05 | Mapped Object 005 | 機能なし | マッピング内容による | データ数は可変（Sub index H00 で指定します。） |
| H06 | Mapped Object 006 | 機能なし | マッピング内容による | データ数は可変（Sub index H00 で指定します。） |
| H07 | Mapped Object 007 | 機能なし | マッピング内容による | データ数は可変（Sub index H00 で指定します。） |
| H08 | Mapped Object 008 | 機能なし | マッピング内容による | データ数は可変（Sub index H00 で指定します。） |
| H09 | Mapped Object 009 | 機能なし | マッピング内容による | データ数は可変（Sub index H00 で指定します。） |
| H0A | Mapped Object 010 | 機能なし | マッピング内容による | データ数は可変（Sub index H00 で指定します。） |
| H0B | Mapped Object 011 | 機能なし | マッピング内容による | データ数は可変（Sub index H00 で指定します。） |

（注: 原本では H03～H0B の「マッピング内容」「データ長」、H02～H0B の「備考」が結合セル。各行に展開した）

###### ■ Index H1A00（1st transmit PDO mapping） (2.13.4 / 原本 p.200)

| Sub index | 名称 | マッピング内容（固定） | データ長（Bit） |
|---|---|---|---|
| H01 | Mapped Object 001 | Index H6041（Statusword） | 16 |
| H02 | Mapped Object 002 | Index H5FFF、Sub index H01（Index:Pr.1330,Sub:Pr.1394(Low)） | 32 |
| H03 | Mapped Object 003 | Index H5FFF、Sub index H02（Index:Pr.1331,Sub:Pr.1394(High)） | 32 |
| H04 | Mapped Object 004 | Index H5FFF、Sub index H03（Index:Pr.1332,Sub:Pr.1395(Low)） | 32 |
| H05 | Mapped Object 005 | Index H5FFF、Sub index H04（Index:Pr.1333,Sub:Pr.1395(High)） | 32 |
| H06 | Mapped Object 006 | Index H5FFF、Sub index H05（Index:Pr.1334,Sub:Pr.1396(Low)） | 32 |
| H07 | Mapped Object 007 | Index H5FFF、Sub index H06（Index:Pr.1335,Sub:Pr.1396(High)） | 32 |
| H08 | Mapped Object 008 | Index H5FFF、Sub index H07（Index:Pr.1336,Sub:Pr.1397(Low)） | 32 |
| H09 | Mapped Object 009 | Index H5FFF、Sub index H08（Index:Pr.1337,Sub:Pr.1397(High)） | 32 |
| H0A | Mapped Object 010 | Index H5FFF、Sub index H09（Index:Pr.1338,Sub:Pr.1398(Low)） | 32 |
| H0B | Mapped Object 011 | Index H5FFF、Sub index H0A（Index:Pr.1339,Sub:Pr.1398(High)） | 32 |
| H0C | Mapped Object 012 | Index H5FFF、Sub index H0B（Index:Pr.1340,Sub:0x00） | 32 |
| H0D | Mapped Object 013 | Index H5FFF、Sub index H0C（Index:Pr.1341,Sub:0x00） | 32 |
| H0E | Mapped Object 014 | Index H5FFF、Sub index H0D（Index:Pr.1342,Sub:0x00） | 32 |
| H0F | Mapped Object 015 | Index H5FFF、Sub index H0E（Index:Pr.1343,Sub:0x00） | 32 |

> **NOTE**
> - Pr.1330 ～ Pr.1343 に存在しないインデックス番号を指定した場合、または “9999” を設定した場合、データは H0 として扱われます。

###### ■ Index H1A20（33rd transmit PDO mapping） (2.13.4 / 原本 p.201)

| Sub index | 名称 | マッピング内容（初期値） | データ長（Bit） | 備考 |
|---|---|---|---|---|
| H01 | Mapped Object 001 | Index H6041（Statusword）（固定） | 16 | 変更不可 |
| H02 | Mapped Object 002 | Index H6043（vl velocity demand） | 16 | データ数は可変（Sub index H00 で指定します。） |
| H03 | Mapped Object 003 | 機能なし | マッピング内容による | データ数は可変（Sub index H00 で指定します。） |
| H04 | Mapped Object 004 | 機能なし | マッピング内容による | データ数は可変（Sub index H00 で指定します。） |
| H05 | Mapped Object 005 | 機能なし | マッピング内容による | データ数は可変（Sub index H00 で指定します。） |
| H06 | Mapped Object 006 | 機能なし | マッピング内容による | データ数は可変（Sub index H00 で指定します。） |
| H07 | Mapped Object 007 | 機能なし | マッピング内容による | データ数は可変（Sub index H00 で指定します。） |
| H08 | Mapped Object 008 | 機能なし | マッピング内容による | データ数は可変（Sub index H00 で指定します。） |
| H09 | Mapped Object 009 | 機能なし | マッピング内容による | データ数は可変（Sub index H00 で指定します。） |
| H0A | Mapped Object 010 | 機能なし | マッピング内容による | データ数は可変（Sub index H00 で指定します。） |
| H0B | Mapped Object 011 | 機能なし | マッピング内容による | データ数は可変（Sub index H00 で指定します。） |
| H0C | Mapped Object 012 | 機能なし | マッピング内容による | データ数は可変（Sub index H00 で指定します。） |
| H0D | Mapped Object 013 | 機能なし | マッピング内容による | データ数は可変（Sub index H00 で指定します。） |
| H0E | Mapped Object 014 | 機能なし | マッピング内容による | データ数は可変（Sub index H00 で指定します。） |
| H0F | Mapped Object 015 | 機能なし | マッピング内容による | データ数は可変（Sub index H00 で指定します。） |

（注: 原本では H03～H0F の「マッピング内容」「データ長」、H02～H0F の「備考」が結合セル。各行に展開した）

#### 2.13.5 CoE オブジェクトディクショナリ (2.13.5 / 印刷 p.200 / 原本 p.201)

| Index | 内容 | 参照ページ |
|---|---|---|
| H1000 ～ H1FFF | CoE（CAN application protocol over EtherCAT）通信エリア | 214 ページ |
| H3000 ～ H5FFF | メーカ固有エリア | 210 ページ |
| H6000 ～ HFFFF | プロファイルエリア（CiA402 ドライブプロファイル） | 200 ページ |

##### ◆ プロファイルエリア（CiA402 ドライブプロファイル） (2.13.5 / 原本 p.201)

| Index | Sub index | 名称 | 内容 | 読出 / 書込 | Data type |
|---|---|---|---|---|---|
| H603F (24639) | H00 | Error code | エラー番号<br>電源投入後、またはインバータリセット後に発生した最新の異常のエラーコードを返信します。<br>重故障が発生していない場合はエラーなしを返信します。<br>重故障発生中にアラーム履歴がクリアされた場合、エラーなしを返信します。<br>上位 8bit を FF 固定とし、下位 8bit をエラーコードとします。<br>（HFFXX：XX にエラーコードが入ります。）<br>（エラーコードは取扱説明書（保守編）の異常表示一覧を参照） | 読出 | Unsigned16 |
| H6040 (24640) | H00 | Controlword | 207 ページ参照 | 読出 / 書込 | Unsigned16 |
| H6041 (24641) | H00 | Statusword | 209 ページ参照 | 読出 | Unsigned16 |
| H6042 (24642) | H00 | vl target velocity | 設定速度（r/min）*2*4<br>設定周波数を r/min 単位で設定します。<br>モニタ範囲：-32768（H8000）～ 32767（H7FFF）<br>Pr.81 ＝ “9999” の場合、モータ極数は 4 極として換算します。<br>Index H60FF と同時に設定値を変更しないでください。 | 読出 / 書込 | Integer16 |
| H6043 (24643) | H00 | vl velocity demand | 出力周波数（r/min）*2<br>出力周波数を r/min 単位で読み出します。<br>モニタ範囲：-32768（H8000）～ 32767（H7FFF）<br>Pr.81 ＝ “9999” の場合、モータ極数は 4 極として換算します。 | 読出 | Integer16 |
| H6044 (24644) | H00 | vl velocity actual value | 運転速度（r/min）*2<br>運転速度を r/min 単位で読み出します。<br>モニタ範囲：-32768（H8000）～ 32767（H7FFF）<br>Pr.81 ＝ “9999” の場合、モータ極数は 4 極として換算します。 | 読出 | Integer16 |
| H6046 (24646) | - | vl velocity min max amount | 下限 / 上限速度（r/min） | - | - |
| H6046 (24646) | H00 | Highest sub-index supported | サブインデックスの最大値：H02（固定） | 読出 | Unsigned8 |
| H6046 (24646) | H01 | vl velocity min amount | 下限速度（r/min）*2*3<br>**Pr.2 下限周波数**を r/min 単位で設定します。<br>設定範囲：0 ～ 120Hz | 読出 / 書込 | Unsigned32 |
| H6046 (24646) | H02 | vl velocity max amount | 上限速度（r/min）*2*3<br>**Pr.18 高速上限周波数**を r/min 単位で設定します。<br>設定範囲：0 ～ 590Hz<br>Index H607F と同時に設定値を変更しないでください。 | 読出 / 書込 | Unsigned32 |
| H6048 (24648) | - | vl velocity acceleration | 加速度<br>vl velocity acceleration=Delta speed/Delta time | - | - |
| H6048 (24648) | H00 | Highest sub-index supported | サブインデックスの最大値：H02（固定） | 読出 | Unsigned8 |
| H6048 (24648) | H01 | Delta speed | 基準速度（r/min）*2*3<br>**Pr.20 加減速基準周波数**を r/min 単位で設定します。<br>設定範囲：1 ～ 590Hz | 読出 / 書込 | Unsigned32 |
| H6048 (24648) | H02 | Delta time | 加速時間（s）*3<br>**Pr.7 加速時間**を設定します。<br>設定範囲：0 ～ 3600s<br>（例：1500r/min まで 3.7s 加速したい場合は、Sub index H01 を 15000r/min、Sub index H02 を 37s に設定にする。）<br>Index H6083 と同時に設定値を変更しないでください。 | 読出 / 書込 | Unsigned16 |
| H6049 (24649) | - | vl velocity deceleration | 減速度<br>vl velocity deceleration=Delta speed/Delta time | - | - |
| H6049 (24649) | H00 | Highest sub-index supported | サブインデックスの最大値：H02（固定） | 読出 | Unsigned8 |
| H6049 (24649) | H01 | Delta speed | 基準速度（r/min）*2*3<br>**Pr.20 加減速基準周波数**を r/min 単位で設定します。<br>設定範囲：1 ～ 590Hz | 読出 / 書込 | Unsigned32 |
| H6049 (24649) | H02 | Delta time | 減速時間（s）*3<br>**Pr.8 減速時間**を設定します。<br>設定範囲：0 ～ 3600s<br>（例：1500r/min から 3.7s 減速したい場合は、Sub index H01 を 15000r/min、Sub index H02 を 37s に設定にする。）<br>Index H6084 と同時に設定値を変更しないでください。 | 読出 / 書込 | Unsigned16 |
| H604A (24650) | - | vl velocity quick stop | 急速停止 | - | - |
| H604A (24650) | H00 | Highest sub-index supported | サブインデックスの最大値：H02（固定） | 読出 | Unsigned8 |
| H604A (24650) | H01 | Delta speed | 基準速度（r/min）*2<br>**Pr.20 加減速基準周波数**を r/min 単位で設定します。<br>設定範囲：1 ～ 590Hz | 読出 / 書込 | Unsigned32 |
| H604A (24650) | H02 | Delta time | 減速時間（s）<br>**Pr.1103 非常停止時減速時間**を設定します。<br>設定範囲：0 ～ 3600s<br>（例：1500r/min から 3.7s 減速したい場合は、Sub index H01 を 15000r/min、Sub index H02 を 37s に設定にする。） | 読出 / 書込 | Unsigned16 |
| H605A (24666)*1 | H00 | Quick stop option code | クイック停止オプションコード：H0002（固定） | 読出 / 書込 | Integer16 |
| H6060 (24672) | H00 | Modes of operation | 制御モード：-1（ベンダ固有運転モード）（固定） | 読出 / 書込 | Integer8 |
| H6061 (24673) | H00 | Modes of operation display | 現在の制御モード：-1（ベンダ固有運転モード）（固定） | 読出 | Integer8 |
| H6062 (24674) | H00 | Position demand value | 位置指令（pulse）<br>電子ギア演算前の位置指令を読み出します。 | 読出 | Integer32 |
| H6063 (24675) | H00 | Position actual internal value | 現在位置（pulse）<br>電子ギア演算後の現在位置を読み出します。 | 読出 | Integer32 |

（注: この表は原本 p.203 以降に続く。注記 *1～*4 の本文は担当範囲外（原本 p.205）に記載）

#### （続き）2.13.5 CoE オブジェクトディクショナリ (2.13.5 / 印刷 p.202 / 原本 p.203)

##### （続き）◆ プロファイルエリア（CiA402 ドライブプロファイル） (2.13.5 / 原本 p.203)

（注: 前ページから続く表の続き。原本 p.203〜205）

| Index | Sub index | 名称 | 内容 | 読出 / 書込 | Data type |
|---|---|---|---|---|---|
| H6064<br>(24676) | H00 | Position actual value | 現在位置（pulse）<br>電子ギア演算前の現在位置を読み出します。 | 読出 | Integer32 |
| H6065<br>(24677) | H00 | Following error window | 溜りパルスエラー判定値（pulse）<br>初期値：40000（H9C40）<br>設定範囲：H00000000 ～ HFFFFFFFF | 読出 / 書込 | Unsigned32 |
| H6066<br>(24678) | H00 | Following error time out | 溜りパルスエラー判定時間：H0000（固定） | 読出 / 書込 | Unsigned16 |
| H6067<br>(24679) | H00 | Position window | 位置決め完了判定値（pulse）<br>位置決め完了幅を設定します。<br>初期値：100（H64）<br>設定範囲：H00000000 ～ HFFFFFFFF | 読出 / 書込 | Unsigned32 |
| H6068<br>(24680) | H00 | Position window time | 位置決め完了判定時間：H0000（固定） | 読出 / 書込 | Unsigned16 |
| H6071<br>(24689) | H00 | Target torque | 設定トルク（%）<br>**Pr.805 トルク指令値（RAM）**を設定します。<br>設定範囲：600 ～ 1400%<br>0.1 単位で設定した場合、0.1 の桁を切り捨てます。 | 読出 / 書込 | Integer16 |
| H6074<br>(24692) | H00 | Torque demand | トルク要求値（%）<br>トルク指令を読み出します。 | 読出 | Integer16 |
| H6077<br>(24695) | H00 | Torque actual value | 現在トルク値（%）<br>モータトルクを読み出します。 | 読出 | Integer16 |
| H607A<br>(24698) | H00 | Target position | 目標位置（pulse）<br>ダイレクトコマンドモード時の目標位置を設定します。<br>初期値：0<br>設定範囲：-2147483647 ～ 2147483647<br>（ダイレクトコマンドモードについては、FR-E800 取扱説明書（機能編）参照） | 読出 / 書込 | Integer32 |
| H607E<br>(24702) | H00 | Polarity | 回転方向：0 または 128<br>Bit0 ～ 6：0<br>Bit7：位置制御時の Controlword の回転方向<br>（0：正転、1：逆転） | 読出 / 書込 | Unsigned8 |
| H607F<br>(24703) | H00 | Max profile velocity | 最大プロファイル速度（r/min）*2*3<br>**Pr.18 高速上限周波数**を r/min 単位で設定します。<br>設定範囲：0 ～ 590Hz<br>Index H6046、Sub index H02 と同時に設定値を変更しないでください。 | 読出 / 書込 | Unsigned32 |
| H6081<br>(24705) | H00 | Profile velocity | プロファイル速度（r/min）<br>ダイレクトコマンドモード時の最高速度を設定します。<br>初期値：0<br>設定範囲：0 ～（120×590Hz/**Pr.81**）<br>（ダイレクトコマンドモードについては、FR-E800 取扱説明書（機能編）参照） | 読出 / 書込 | Unsigned32 |
| H6083<br>(24707) | H00 | Profile acceleration | 加速時定数（ms）<br>＜位置制御＞<br>ダイレクトコマンドモード時の加速時間を設定します。<br>初期値：5000<br>設定範囲：10 ～ 360000<br>下 1 桁は切り捨てます。（1358ms の場合は、1350ms となります。）<br>（ダイレクトコマンドモードについては、FR-E800 取扱説明書（機能編）参照）<br>＜位置制御以外＞<br>**Pr.7 加速時間**を ms 単位で設定します。<br>設定範囲：0 ～ 3600s<br>**Pr.21 加減速時間単位**＝ "0" 設定時は下 2 桁、**Pr.21** ＝ "1" 設定時は下 1 桁を切り捨てます。<br>Index H6048、Sub index H02 と同時に設定値を変更しないでください。 | 読出 / 書込 | Unsigned32 |
| H6084<br>(24708) | H00 | Profile deceleration | 減速時定数（ms）<br>＜位置制御＞<br>ダイレクトコマンドモード時の減速時間を設定します。<br>初期値：5000<br>設定範囲：10 ～ 360000<br>下 1 桁は切り捨てます。（1358ms の場合は、1350ms となります。）<br>（ダイレクトコマンドモードについては、FR-E800 取扱説明書（機能編）参照）<br>＜位置制御以外＞<br>**Pr.8 減速時間**を ms 単位で設定します。<br>設定範囲：0 ～ 3600s<br>**Pr.21 加減速時間単位**＝ "0" 設定時は下 2 桁、**Pr.21** ＝ "1" 設定時は下 1 桁を切り捨てます。<br>Index H6049、Sub index H02 と同時に設定値を変更しないでください。 | 読出 / 書込 | Unsigned32 |
| H6085<br>(24709) | H00 | Quick stop deceleration | 減速時定数（QuickStop）（ms）*3<br>＜位置制御＞<br>**Pr.464 位置制御急停止減速時間**を ms 単位で設定します。<br>設定範囲：0.01 ～ 360s<br>下 1 桁は切り捨てます。（1358ms の場合は、1350ms となります。）<br>＜位置制御以外＞<br>**Pr.1103 非常停止時減速時間**を ms 単位で設定します。<br>設定範囲：0 ～ 3600s<br>**Pr.21 加減速時間単位**＝ "0" 設定時は下 2 桁、**Pr.21** ＝ "1" 設定時は下 1 桁を切り捨てます。 | 読出 / 書込 | Unsigned32 |
| H608F<br>(24719) | - | Position encoder resolution | PLG 分解能（機械側 / モータ側） | - | - |
| H608F<br>(24719) | H00 | Highest sub-index supported | サブインデックスの最大値：H02（固定） | 読出 | Unsigned8 |
| H608F<br>(24719) | H01 | Encoder increments | PLG 分解能<br>**Pr.369 PLG パルス数**を設定します。<br>設定範囲：2 ～ 4096 | 読出 / 書込 | Unsigned32 |
| H608F<br>(24719) | H02 | Motor revolutions | モータ回転数（rev）：H00000001（固定） | 読出 / 書込 | Unsigned32 |
| H6091<br>(24721) | - | Gear ratio | ギア比 | - | - |
| H6091<br>(24721) | H00 | Highest sub-index supported | サブインデックスの最大値：H02（固定） | 読出 | Unsigned8 |
| H6091<br>(24721) | H01 | Motor revolutions | モータ軸回転数 *3<br>**Pr.420 指令パルス倍率分子（電子ギア分子）**を設定します。<br>設定範囲：1 ～ 32767 | 読出 / 書込 | Unsigned32 |
| H6091<br>(24721) | H02 | Shaft revolutions | 駆動軸回転数 *3<br>**Pr.421 指令パルス倍率分母（電子ギア分母）**を設定します。<br>設定範囲：1 ～ 32767 | 読出 / 書込 | Unsigned32 |
| H6098<br>(24728) | H00 | Homing method | 原点復帰方法<br>ダイレクトコマンドモード時の原点復帰方式を設定します。*5<br>（ダイレクトコマンドモード、原点復帰方式については、FR-E800 取扱説明書（機能編）参照） | 読出 / 書込 | Integer8 |
| H6099<br>(24729) | - | Homing speeds | 原点復帰速度 | - | - |
| H6099<br>(24729) | H00 | Highest sub-index supported | サブインデックスの最大値：H02（固定） | 読出 | Unsigned8 |
| H6099<br>(24729) | H01 | Speed during search for switch | 原点復帰時のモータ速度（r/min）<br>ダイレクトコマンドモード時の原点復帰速度を設定します。<br>初期値：120×2Hz/**Pr.81**<br>設定範囲：0 ～（120×400Hz/**Pr.81**）<br>（ダイレクトコマンドモードについては、FR-E800 取扱説明書（機能編）参照） | 読出 / 書込 | Unsigned32 |
| H6099<br>(24729) | H02 | Speed during search for zero | 近点ドグ前端検出後のクリープ速度（r/min）<br>ダイレクトコマンドモード時の原点復帰クリープ速度を設定します。<br>初期値：120×3Hz/**Pr.81**<br>設定範囲：0 ～（120×400Hz/**Pr.81**）<br>（ダイレクトコマンドモードについては、FR-E800 取扱説明書（機能編）参照） | 読出 / 書込 | Unsigned32 |
| H609A<br>(24730) | H00 | Homing acceleration | 原点復帰加減速時間（ms）<br>ダイレクトコマンドモード時の原点復帰加速時間、減速時間を設定します。<br>初期値：5000<br>設定範囲：10 ～ 360000<br>下 1 桁は切り捨てます。（1358ms の場合は、1350ms となります。）<br>（ダイレクトコマンドモードについては、FR-E800 取扱説明書（機能編）参照） | 読出 / 書込 | Unsigned32 |
| H60F4<br>(24820) | H00 | Following error actual value | 溜りパルス（pulse）<br>電子ギア演算前の溜りパルスを読み出します。 | 読出 | Integer32 |
| H60FA<br>(24826) | H00 | Control effort | 位置ループ後の速度指令 *2<br>理想速度指令を読み出します。 | 読出 | Integer32 |
| H60FC<br>(24828) | H00 | Position demand internal value | 位置指令（pulse）<br>電子ギア演算後の位置指令を読み出します。 | 読出 | Integer32 |
| H60FF<br>(24831) | H00 | Target velocity | 設定速度（r/min）*2*4<br>設定周波数を r/min 単位で設定します。<br>モニタ範囲：-32768（H8000）～ 32767（H7FFF）<br>**Pr.81** ＝ "9999" の場合、モータ極数は 4 極として換算します。<br>書込みは、**Pr.53** による単位切換え後の値の下位 24bit が有効となり、上位 8bit のデータは無視されます。<br>Index H6042 と同時に設定値を変更しないでください。 | 読出 / 書込 | Integer32 |
| H6502<br>(25858) | H00 | Supported drive modes | 対応する制御モード：H00010000（ベンダ固有運転モード） | 読出 | Unsigned32 |
| H67FF<br>(26623)*1 | H00 | Single device type | デバイスタイプ<br>Bit0 ～ 15 Device Profile Number：H0192<br>（402：Drive Profile）<br>Bit16 ～ 23 Additional Information(Type)：H01<br>（Frequency Converter：インバータ）<br>Bit24 ～ 31 Additional Information(mode bits)：H00 | 読出 | Unsigned32 |

\*1 PDO 通信では使用できません。

\*2 **Pr.53** の設定に関係なく r/min 単位で表示、設定します。<br>
読出し時は、周波数を回転速度変換して読み出し、書込み時は、設定値を周波数変換して書き込みます。

\*3 パラメータ書込みを実施したとき、PDO 通信は RAM 書込みとなります。SDO 通信時の EEPROM と RAM への書込み選択は、**Pr.342 通信 EEPROM 書込み選択**の設定によります。

\*4 書込み時、**Pr.18**、**Pr.2** の設定による制限は行いません。

\*5 Index H6098 の設定値と対応する原点復帰方式を下表に示します。

| H6098 設定値 | 原点復帰方式 |
|---|---|
| -3 | データセット式 |
| -4 | 押当て式（原点復帰方向：位置パルス増加方向） |
| -5（初期値） | 原点無視（サーボ ON 位置原点） |
| -6 | ドグ式後端基準（原点復帰方向：位置パルス増加方向） |
| -7 | カウント式前端基準（原点復帰方向：位置パルス増加方向） |
| -10 | ドグ式前端基準（原点復帰方向：位置パルス増加方向） |
| -36 | 押当て式（原点復帰方向：位置パルス減少方向） |
| -38 | ドグ式後端基準（原点復帰方向：位置パルス減少方向） |
| -39 | カウント式前端基準（原点復帰方向：位置パルス減少方向） |
| -42 | ドグ式前端基準（原点復帰方向：位置パルス減少方向） |
| -65 | 押当て式（原点復帰方向：始動指令の方向） |
| -66 | カウント式前端基準（原点復帰方向：始動指令の方向） |
| -67 | ドグ式後端基準（原点復帰方向：始動指令の方向） |
| -68 | ドグ式前端基準（原点復帰方向：始動指令の方向） |

> **NOTE**
> - ネットワーク運転モードの指令権については、**Pr.550 NET モード操作権選択**の設定に従います。（FR-E800 取扱説明書（機能編）参照）
> - 読出し時は、**Pr.290 モニタマイナス出力選択**の設定に関係なく符号付きで表示します。

###### ■ PDS（power drive system）状態遷移 (2.13.5 / 原本 p.207)

PDO 通信確立後（ESM が Operational 状態）、マスタが Controlword によるコマンドを送信することにより状態を制御します。電源 ON またはインバータリセット直後の「Not ready to switch on」から「Operation enabled」まで遷移すると、インバータが運転可能となります。SDO 通信による Controlword への書込みは反映されません。

- 状態定義

【図】PDS 状態遷移図 (原本 p.207)
- Start →(遷移 0)→ Not ready to switch on
- Not ready to switch on →(遷移 1)→ Switch on disabled
- Switch on disabled →(遷移 2)→ Ready to switch on
- Ready to switch on →(遷移 7)→ Switch on disabled
- Ready to switch on →(遷移 3)→ Switched on
- Switched on →(遷移 6)→ Ready to switch on
- Switched on →(遷移 4)→ Operation enabled
- Operation enabled →(遷移 5)→ Switched on
- Operation enabled →(遷移 8)→ Ready to switch on
- Operation enabled →(遷移 9)→ Switch on disabled
- Switched on →(遷移 10)→ Switch on disabled
- Operation enabled →(遷移 11)→ Quick stop active
- Quick stop active →(遷移 12)→ Switch on disabled
- 破線枠（Not ready to switch on ～ Operation enabled／Quick stop active を囲む領域）内の任意の状態 →(遷移 13)→ Fault reaction active
- Fault reaction active →(遷移 14)→ Fault
- Fault →(遷移 15)→ Switch on disabled

| 名称 | 状態 | インバータ動作 *1<br>位置制御 | インバータ動作 *1<br>位置制御以外 |
|---|---|---|---|
| Not ready to switch on | 停止中（初期化実行状態） | 出力遮断（RY 信号 OFF） | 出力遮断（RY 信号 OFF） |
| Switch on disabled | 停止中（初期状態） | 出力遮断（RY 信号 OFF） | 出力遮断（RY 信号 OFF） |
| Ready to switch on | 停止中（準備状態） | 出力遮断（RY 信号 OFF） | 出力遮断（RY 信号 OFF） |
| Switched on | 停止中（待機状態） | 出力遮断解除（RY 信号 ON）*2 | 出力遮断解除（RY 信号 ON）*2 |
| Operation enabled | 運転中（運転可能状態） | サーボ ON（LX 信号または SON 信号 ON）と同じ状態 | • Enable operation コマンドを受信した場合（始動指令 ON と同じ状態 *3）<br>• Disable operation コマンドを受信した場合（始動指令 OFF と同じ状態） |
| Quick stop active | 非常停止中 | 急停止機能が動作する（X87 信号 ON（常時開入力の場合）と同じ状態） | 非常停止機能が動作する（X92 信号 ON と同じ状態） |
| Fault reaction active | 重故障検出中 | -（Fault に遷移する） | -（Fault に遷移する） |
| Fault | 重故障発生中 | 出力遮断（RY 信号 OFF） | 出力遮断（RY 信号 OFF） |

（注: 「インバータ動作」列は Operation enabled と Quick stop active 以外の行で位置制御／位置制御以外が結合セル。各列に展開した）

\*1 EtherCAT 通信使用時は、PDS 状態遷移によりサーボ ON/OFF、または始動指令を制御します。SON 信号 OFF による出力遮断は有効です（出力遮断時は「Operation enabled」に遷移しません）。

\*2 MRS 信号などにより出力遮断している場合、RY 信号は OFF のままとなります。

\*3 始動指令の方向は、vl target velocity（H6042）または Target velocity（H60FF）の符号によります。

> **NOTE**
> - 下記条件をすべて満たすと Controlword による制御が有効となり、状態遷移が可能となります。
>   - NET 運転モード
>   - NET 運転モードの指令権（**Pr.550**）が Ethernet コネクタにある
>   - **Pr.338 通信運転指令権**＝ "0"
> - Controlword による制御が有効な状態では、主回路コンデンサ寿命測定は実施できません。（主回路コンデンサ寿命測定については、取扱説明書（機能編）参照）

- 遷移番号

| 遷移番号 | Controlword | Controlword 以外 |
|---|---|---|
| 0 | - | 電源 ON、インバータリセット |
| 1 | - | 初期化完了後に自動遷移 |
| 2 | Shutdown コマンド | - |
| 3 | Switch on コマンド | - |
| 4 | Enable operation コマンド（RY 信号が OFF の場合は遷移しない） | - |
| 5 | Disable operation コマンド *1<br>インバータ停止後に遷移する（直流制動中、予備励磁中は遷移しない） | RY 信号が OFF になる場合に遷移する *1 |
| 6 | Shutdown コマンド | - |
| 7 | Disable voltage または Quick stop コマンド | *3 |
| 8 | Shutdown コマンド *1 | - |
| 9 | Disable voltage コマンド *1 | *3 |
| 10 | Disable voltage または Quick stop コマンド | *3 |
| 11 | Quick stop コマンド *2 | - |
| 12 | Disable voltage コマンド *1 | 非常停止後に自動遷移 *3<br>• 位置制御<br>PBSY 信号 OFF 後に自動遷移<br>• 位置制御以外<br>インバータ停止後に自動遷移（直流制動中、予備励磁中は遷移しない） |
| 13 | - | 重故障検出 |
| 14 | - | 自動遷移 *1 |
| 15 | マスタからの Fault reset コマンド<br>保護機能をリセットする *4 | *3 |

\*1 コマンド入力により動作したサーボ ON（LX 信号または SON 信号 ON）（位置制御の場合）、始動指令 ON（位置制御以外の場合）の状態は解除します。また、位置制御の場合は Controlword の bit4 による始動指令も解除します。

\*2 コマンドを使用せず、X87、X92 信号を割り付けて非常停止させる場合は、「Quick stop active」に遷移しません。

\*3 下記のいずれかを満たさない場合は、「Switch on disabled」に遷移します。<br>
NET 運転モード<br>
NET 運転モードの指令権（**Pr.550**）が Ethernet コネクタにある<br>
**Pr.338 通信運転指令権**＝ "0"

\*4 E.SCF、E.GF（**Pr.249** ＝ "2" 設定時）、E.16 ～ E.20、E.PE6、E.PE2、E.CPU、E.SAF、E.CMB、E.1、E.5 ～ E.7、E.13 はリセットされません。この場合は、原因の処置を行ってから、電源再投入またはインバータリセットしてください。

###### ■ Controlword（H6040） (2.13.5 / 原本 p.208)

- 位置制御

原点復帰が正常に完了し、bit4 が 1 → 0 になると位置決めに移行します。ただし、原点復帰方式が原点無視（サーボ ON 位置原点）、またはロール送りモード、現在位置保持機能、JOG 運転を使用する場合、bit4 の操作は不要です。

| Bit | 名称 | 原点復帰 | 位置決め |
|---|---|---|---|
| 0 | switch on (so) | 208 ページ参照 | 208 ページ参照 |
| 1 | enable voltage (ev) | 208 ページ参照 | 208 ページ参照 |
| 2 | quick stop (qs) | 208 ページ参照 | 208 ページ参照 |
| 3 | enable operation (eo) | 208 ページ参照 | 208 ページ参照 |
| 4 | HOS (oms) | 0 → 1 で原点復帰開始 *1<br>0：Do not start homing procedure<br>1：Start or continue homing procedure | - |
| 4 | new set-point (oms) | - | 0 → 1 で位置決めデータを取得し、位置決め開始 |
| 5 | 未使用 | 未使用 | 未使用 |
| 6 | abs/rel (oms) | - | 0：絶対位置指令<br>1：増分位置指令 |
| 7 | fault reset (fr) | 208 ページ参照 | 208 ページ参照 |
| 8 ～ 15 | 未使用 | 未使用 | 未使用 |

（注: 「208 ページ参照」「未使用」は原本で原点復帰・位置決め列にまたがる結合セル。各列に展開した。208 ページ＝印刷ページ、本mdでは下記「遷移コマンド」表（原本 p.209）が該当）

\*1 再度原点復帰を行う場合は、一度「Switched on」から「Operation enabled」に遷移させてください。（210 ページ参照）

- 位置制御以外

| Bit | 名称 | 速度制御、トルク制御 |
|---|---|---|
| 0 | switch on (so) | 208 ページ参照 |
| 1 | enable voltage (ev) | 208 ページ参照 |
| 2 | quick stop (qs) | 208 ページ参照 |
| 3 | enable operation (eo) | 208 ページ参照 |
| 4 ～ 6 | 未使用 | 未使用 |
| 7 | fault reset (fr) | 208 ページ参照 |
| 8 ～ 15 | 未使用 | 未使用 |

- 遷移コマンド

| Command | Bit7<br>fr | Bit3<br>eo | Bit2<br>qs | Bit1<br>ev | Bit0<br>so |
|---|---|---|---|---|---|
| Shutdown | 0 | - | 1 | 1 | 0 |
| Switch on | 0 | 0 | 1 | 1 | 1 |
| Disable voltage | 0 | - | - | 0 | - |
| Quick stop | 0 | - | 0 | 1 | - |
| Disable operation | 0 | 0 | 1 | 1 | 1 |
| Enable operation | 0 | 1 | 1 | 1 | 1 |
| Fault reset | 0 → 1 | - | - | - | - |

-：未使用

下表のように遷移させることも可能です。

| 現在の状態 | Command | 遷移先 |
|---|---|---|
| Switch on disabled | Switch on | Switched on |
| Switch on disabled | Enable operation | Operation enabled |
| Ready to switch on | Enable operation | Operation enabled |

- エマージェンシードライブ実行中の状態

| エマージェンシードライブ運転状態 | 遷移先 |
|---|---|
| エマージェンシードライブ商用運転中 | Switch on disabled |
| 重大異常発生時 | Fault reaction active → Fault |
| その他 | Operation enabled |

###### ■ Statusword（H6041） (2.13.5 / 原本 p.210)

- 位置制御

原点復帰が正常に完了し、Controlword の bit4 が 1 → 0 になると位置決めに移行します。ただし、原点復帰方式が原点無視（サーボ ON 位置原点）、またはロール送りモード、現在位置保持機能、JOG 運転を使用する場合、bit4 の操作は不要です。

| Bit | 名称 | 原点復帰 | 位置決め |
|---|---|---|---|
| 0 | ready to switch on (rtso) | 210 ページ参照 | 210 ページ参照 |
| 1 | switched on (so) | 210 ページ参照 | 210 ページ参照 |
| 2 | operation enabled (oe) | 210 ページ参照 | 210 ページ参照 |
| 3 | Fault (f) | 210 ページ参照 | 210 ページ参照 |
| 4 | 未使用 | 未使用 | 未使用 |
| 5 | quick stop (qs) | 210 ページ参照 | 210 ページ参照 |
| 6 | switch on disabled (sod) | 210 ページ参照 | 210 ページ参照 |
| 7 | warning (w) | 0：警報、軽故障なし<br>1：警報、軽故障発生中 | 0：警報、軽故障なし<br>1：警報、軽故障発生中 |
| 8 | 未使用 | 未使用 | 未使用 |
| 9 | remote (rm) | 0：Controlword による制御が無効<br>1：Controlword により制御中 *1 | 0：Controlword による制御が無効<br>1：Controlword により制御中 *1 |
| 10 | hm (tr)*2 | • 原点復帰異常なし（ZA 信号 OFF）<br>0：PBSY 信号 ON<br>1：PBSY 信号 OFF<br>• 原点復帰異常発生中（ZA 信号 ON）<br>0：理想速度指令が 0 以外<br>1：理想速度指令が 0 | - |
| 10 | target reached (tr) | - | 0：Target position not reached<br>1：Target position reached<br>Target position（H607A）と Position actual value（H6064）の差（絶対値）が Position window（H6067）設定値以下の状態で、Position window time（H6068）に設定された時間経過すると、1 となります。 |
| 11 | internal limit active | 0：正転ストロークエンド、または逆転ストロークエンドに到達していない（LP 信号 OFF）<br>1：正転ストロークエンド、または逆転ストロークエンドに到達（LP 信号 ON） | 0：正転ストロークエンド、または逆転ストロークエンドに到達していない（LP 信号 OFF）<br>1：正転ストロークエンド、または逆転ストロークエンドに到達（LP 信号 ON） |
| 12 | hm (oms)*2 | 0：原点復帰が完了していない（ZP 信号 OFF）<br>1：原点復帰が完了（ZP 信号 ON） | - |
| 13 | hm (oms)*2 | 0：原点復帰異常なし（ZA 信号 OFF）<br>1：原点復帰異常発生中（ZA 信号 ON） | - |
| 13 | Following error (oms) | - | 0：No following error<br>1：Following error<br>Position demand value（H6062）と Position actual value（H6064）の差（絶対値）が Following error window（H6065）設定値を超えた状態で、Following error time out（H6066）に設定された時間経過すると、1 となります。 |
| 14、15 | 未使用 | 未使用 | 未使用 |

（注: Bit0～3、5～7、9、11 および「未使用」は原本で原点復帰・位置決め列にまたがる結合セル。各列に展開した。210 ページ＝印刷ページ、本mdでは下記「遷移状態」表（原本 p.211）が該当）

\*1 下記条件をすべて満たすと Controlword による制御が有効となり、状態遷移が可能となります。<br>
NET 運転モード<br>
NET 運転モードの指令権（**Pr.550**）が Ethernet コネクタにある<br>
**Pr.338 通信運転指令権**＝ "0"

\*2 hm（Bit10、12、13）の組合せ

| Bit13 | Bit12 | Bit10 | 内容 |
|---|---|---|---|
| 0 | 0 | 0 | 原点復帰中 |
| 0 | 0 | 1 | 原点復帰開始前 |
| 0 | 1 | 1 | 原点復帰が正常に完了 |
| 1 | 0 | 1 | 原点復帰異常発生中で理想速度指令が 0 |

- 位置制御以外

| Bit | 名称 | 速度制御、トルク制御 |
|---|---|---|
| 0 | ready to switch on (rtso) | 210 ページ参照 |
| 1 | switched on (so) | 210 ページ参照 |
| 2 | operation enabled (oe) | 210 ページ参照 |
| 3 | Fault (f) | 210 ページ参照 |
| 4 | 未使用 | 未使用 |
| 5 | quick stop (qs) | 210 ページ参照 |
| 6 | switch on disabled (sod) | 210 ページ参照 |
| 7 | warning (w) | 0：警報、軽故障なし<br>1：警報、軽故障発生中 |
| 8 | 未使用 | 未使用 |
| 9 | remote (rm) | 0：Controlword による制御が無効<br>1：Controlword により制御中 *1 |
| 10 ～ 15 | 未使用 | 未使用 |

\*1 下記条件をすべて満たすと Controlword による制御が有効となり、状態遷移が可能となります。<br>
NET 運転モード<br>
NET 運転モードの指令権（**Pr.550**）が Ethernet コネクタにある<br>
**Pr.338 通信運転指令権**＝ "0"

- 遷移状態

| Status | Bit6<br>sod | Bit5<br>qs | Bit3<br>f | Bit2<br>oe | Bit1<br>so | Bit0<br>rtso |
|---|---|---|---|---|---|---|
| Not ready to switch on | 0 | - | 0 | 0 | 0 | 0 |
| Switch on disabled | 1 | - | 0 | 0 | 0 | 0 |
| Ready to switch on | 0 | 1 | 0 | 0 | 0 | 1 |
| Switched on | 0 | 1 | 0 | 0 | 1 | 1 |
| Operation enabled | 0 | 1 | 0 | 1 | 1 | 1 |
| Quick stop active | 0 | 0 | 0 | 1 | 1 | 1 |
| Fault reaction active | 0 | - | 1 | 1 | 1 | 1 |
| Fault | 0 | - | 1 | 0 | 0 | 0 |

-：未使用

##### ◆ メーカ固有エリア (2.13.5 / 原本 p.211)

###### ■ インバータパラメータ (2.13.5 / 原本 p.211)

| Index | Sub index | 名称 | 備考 | 読出 / 書込 | サイズ |
|---|---|---|---|---|---|
| 12288 ～ 13787<br>（H3000 ～ H35DB） | H00 ～ H02 | Parameter #nnnn<br>（nnnn：インバータパラメータ番号（10 進数）） | インバータパラメータ番号（10 進数）＋ 12288（H3000）がインデックス番号になります。 | 読出 / 書込 | 16bit |

#### （続き）2.13.5 CoEオブジェクトディクショナリ (2.13.5 / 印刷 p.211 / 原本 p.212)

##### （続き）◆ メーカ固有エリア (2.13.5 / 原本 p.212)

###### （続き）■ インバータパラメータ (2.13.5 / 原本 p.212)

• 校正パラメータ

| Index | Sub index | 名称 | 内容 | 読出 / 書込 | サイズ |
|---|---|---|---|---|---|
| 13188（H3384） | H00 | Highest sub-index supported | - | 読出 | 8bit |
| 13188（H3384） | H01 | Data | C0(Pr.900) | 読出 / 書込 | 16bit |
| 13188（H3384） | H02 | Sub Data | - | 読出 / 書込 | 16bit |
| 13189（H3385） | H00 | Highest sub-index supported | - | 読出 | 8bit |
| 13189（H3385） | H01 | Data | C1(Pr.901) | 読出 / 書込 | 16bit |
| 13189（H3385） | H02 | Sub Data | - | 読出 / 書込 | 16bit |
| 13190（H3386） | H00 | Highest sub-index supported | - | 読出 | 8bit |
| 13190（H3386） | H01 | Data | C2(Pr.902) | 読出 / 書込 | 16bit |
| 13190（H3386） | H02 | Sub Data | C3(Pr.902) | 読出 / 書込 | 16bit |
| 13191（H3387） | H00 | Highest sub-index supported | - | 読出 | 8bit |
| 13191（H3387） | H01 | Data | 125(Pr.903) | 読出 / 書込 | 16bit |
| 13191（H3387） | H02 | Sub Data | C4(Pr.903) | 読出 / 書込 | 16bit |
| 13192（H3388） | H00 | Highest sub-index supported | - | 読出 | 8bit |
| 13192（H3388） | H01 | Data | C5(Pr.904) | 読出 / 書込 | 16bit |
| 13192（H3388） | H02 | Sub Data | C6(Pr.904) | 読出 / 書込 | 16bit |
| 13193（H3389） | H00 | Highest sub-index supported | - | 読出 | 8bit |
| 13193（H3389） | H01 | Data | 126(Pr.905) | 読出 / 書込 | 16bit |
| 13193（H3389） | H02 | Sub Data | C7(Pr.905) | 読出 / 書込 | 16bit |
| 13205（H3395）*1 | H00 | Highest sub-index supported | - | 読出 | 8bit |
| 13205（H3395）*1 | H01 | Data | C12(Pr.917) | 読出 / 書込 | 16bit |
| 13205（H3395）*1 | H02 | Sub Data | C13(Pr.917) | 読出 / 書込 | 16bit |
| 13206（H3396）*1 | H00 | Highest sub-index supported | - | 読出 | 8bit |
| 13206（H3396）*1 | H01 | Data | C14(Pr.918) | 読出 / 書込 | 16bit |
| 13206（H3396）*1 | H02 | Sub Data | C15(Pr.918) | 読出 / 書込 | 16bit |
| 13207（H3397）*1 | H00 | Highest sub-index supported | - | 読出 | 8bit |
| 13207（H3397）*1 | H01 | Data | C16(Pr.919) | 読出 / 書込 | 16bit |
| 13207（H3397）*1 | H02 | Sub Data | C17(Pr.919) | 読出 / 書込 | 16bit |
| 13208（H3398）*1 | H00 | Highest sub-index supported | - | 読出 | 8bit |
| 13208（H3398）*1 | H01 | Data | C18(Pr.920) | 読出 / 書込 | 16bit |
| 13208（H3398）*1 | H02 | Sub Data | C19(Pr.920) | 読出 / 書込 | 16bit |
| 13220（H33A4） | H00 | Highest sub-index supported | - | 読出 | 8bit |
| 13220（H33A4） | H01 | Data | C38(Pr.932) | 読出 / 書込 | 16bit |
| 13220（H33A4） | H02 | Sub Data | C39(Pr.932) | 読出 / 書込 | 16bit |
| 13221（H33A5） | H00 | Highest sub-index supported | - | 読出 | 8bit |
| 13221（H33A5） | H01 | Data | C40(Pr.933) | 読出 / 書込 | 16bit |
| 13221（H33A5） | H02 | Sub Data | C41(Pr.933) | 読出 / 書込 | 16bit |
| 13222（H33A6） | H00 | Highest sub-index supported | - | 読出 | 8bit |
| 13222（H33A6） | H01 | Data | C42(Pr.934) | 読出 / 書込 | 16bit |
| 13222（H33A6） | H02 | Sub Data | C43(Pr.934) | 読出 / 書込 | 16bit |
| 13223（H33A7） | H00 | Highest sub-index supported | - | 読出 | 8bit |
| 13223（H33A7） | H01 | Data | C44(Pr.935) | 読出 / 書込 | 16bit |
| 13223（H33A7） | H02 | Sub Data | C45(Pr.935) | 読出 / 書込 | 16bit |

*1　FR-E8AXY 装着時のみ

インバータパラメータ番号およびパラメータ名称は取扱説明書（機能編）のパラメータ一覧を参照してください。

> **NOTE**
> - パラメータ設定値の “8888” は 65520（HFFF0）、設定値 “9999” は 65535（HFFFF）と設定してください。
> - パラメータ書込みを実施したとき、PDO 通信は RAM 書込みとなります。SDO 通信時の EEPROM と RAM への書込み選択は、**Pr.342 通信 EEPROM 書込み選択**の設定によります。

###### ■ モニタデータ (2.13.5 / 原本 p.213)

| Index | Sub index | 名称 | 備考 | 読出 / 書込 | サイズ |
|---|---|---|---|---|---|
| 16384 ～ 16483<br>（H4000 ～ H4063） | H00 | Monitor data #nnnn<br>（nnnn：モニタコード（10 進数）） | モニタコード（10 進数）＋ 16384（H4000）がインデックス番号になります。 | 読出 | 16bit |

モニタコードおよびモニタ項目については取扱説明書（機能編）の **Pr.52** の内容を参照してください。

> **NOTE**
> - **Pr.290 モニタマイナス出力選択**によるモニタ表示のマイナス出力は無効となります。
> - 周波数表示のモニタは **Pr.53** により回転数（機械速度）表示に変更できます。機械速度表示に切り換えた場合、表示単位は 1 単位となります。

###### ■ インバータ制御パラメータ (2.13.5 / 原本 p.213)

（注: 本表は原本 p.213〜p.214 にまたがる。24575（H5FFF）の行は原本 p.214。備考欄の結合セルは各行に展開）

| Index | Sub index | 名称 | 備考 | 読出 / 書込 | サイズ |
|---|---|---|---|---|---|
| 20482（H5002）*1 | H00 | インバータリセット | 書込み値は H9966 を設定してください。<br>読出し値は H0000 固定 | 読出 / 書込 | 16bit |
| 20483（H5003）*1 | H00 | パラメータクリア | 書込み値は H965A を設定してください。<br>読出し値は H0000 固定 | 読出 / 書込 | 16bit |
| 20484（H5004）*1 | H00 | パラメータオールクリア | 書込み値は H99AA を設定してください。<br>読出し値は H0000 固定 | 読出 / 書込 | 16bit |
| 20486（H5006）*1 | H00 | パラメータクリア *2 | 書込み値は H5A96 を設定してください。<br>読出し値は H0000 固定 | 読出 / 書込 | 16bit |
| 20487（H5007）*1 | H00 | パラメータオールクリア *2 | 書込み値は HAA99 を設定してください。<br>読出し値は H0000 固定 | 読出 / 書込 | 16bit |
| 20488（H5008） | H00 | 制御入力命令 / インバータ状態（拡張）*3 | 213 ページ参照 | 読出 / 書込 | 16bit |
| 20489（H5009） | H00 | 制御入力命令 / インバータ状態 *3 | 213 ページ参照 | 読出 / 書込 | 16bit |
| 20981（H51F5） | H00 | アラーム履歴 1 | データは 2byte のため “H00 ○○ ” で格納されます。下位 1byte にエラーコードを参照できます。（エラーコードは取扱説明書（保守編）の異常表示一覧を参照）<br>20981（H51F5）に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 | 読出 / 書込 *1 | 16bit |
| 20982（H51F6） | H00 | アラーム履歴 2 | データは 2byte のため “H00 ○○ ” で格納されます。下位 1byte にエラーコードを参照できます。（エラーコードは取扱説明書（保守編）の異常表示一覧を参照）<br>20981（H51F5）に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 | 読出 | 16bit |
| 20983（H51F7） | H00 | アラーム履歴 3 | データは 2byte のため “H00 ○○ ” で格納されます。下位 1byte にエラーコードを参照できます。（エラーコードは取扱説明書（保守編）の異常表示一覧を参照）<br>20981（H51F5）に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 | 読出 | 16bit |
| 20984（H51F8） | H00 | アラーム履歴 4 | データは 2byte のため “H00 ○○ ” で格納されます。下位 1byte にエラーコードを参照できます。（エラーコードは取扱説明書（保守編）の異常表示一覧を参照）<br>20981（H51F5）に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 | 読出 | 16bit |
| 20985（H51F9） | H00 | アラーム履歴 5 | データは 2byte のため “H00 ○○ ” で格納されます。下位 1byte にエラーコードを参照できます。（エラーコードは取扱説明書（保守編）の異常表示一覧を参照）<br>20981（H51F5）に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 | 読出 | 16bit |
| 20986（H51FA） | H00 | アラーム履歴 6 | データは 2byte のため “H00 ○○ ” で格納されます。下位 1byte にエラーコードを参照できます。（エラーコードは取扱説明書（保守編）の異常表示一覧を参照）<br>20981（H51F5）に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 | 読出 | 16bit |
| 20987（H51FB） | H00 | アラーム履歴 7 | データは 2byte のため “H00 ○○ ” で格納されます。下位 1byte にエラーコードを参照できます。（エラーコードは取扱説明書（保守編）の異常表示一覧を参照）<br>20981（H51F5）に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 | 読出 | 16bit |
| 20988（H51FC） | H00 | アラーム履歴 8 | データは 2byte のため “H00 ○○ ” で格納されます。下位 1byte にエラーコードを参照できます。（エラーコードは取扱説明書（保守編）の異常表示一覧を参照）<br>20981（H51F5）に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 | 読出 | 16bit |
| 20989（H51FD） | H00 | アラーム履歴 9 | データは 2byte のため “H00 ○○ ” で格納されます。下位 1byte にエラーコードを参照できます。（エラーコードは取扱説明書（保守編）の異常表示一覧を参照）<br>20981（H51F5）に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 | 読出 | 16bit |
| 20990（H51FE） | H00 | アラーム履歴 10 | データは 2byte のため “H00 ○○ ” で格納されます。下位 1byte にエラーコードを参照できます。（エラーコードは取扱説明書（保守編）の異常表示一覧を参照）<br>20981（H51F5）に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 | 読出 | 16bit |
| 20992（H5200） | H00 | Safety 入力状態 | 213 ページ参照 | 読出 | 16bit |
| 24574（H5FFE） | - | RxPDO Parameter Mapping | PDO マッピングオブジェクト H1600 用<br>PDO 通信で書き込む場合、**Pr.1320 ～ Pr.1329、Pr.1389 ～ Pr.1393** で選択したオブジェクトに対応する値を書き込みます。<br>SDO 通信で読み出す場合、マッピングオブジェクトと同じ形式の値を読み出します。<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60420020（初期値）<br>Sub index H02 ～ H0A：H00000020（初期値） | - | - |
| 24574（H5FFE） | H00 | Highest sub-index supported | PDO マッピングオブジェクト H1600 用<br>PDO 通信で書き込む場合、**Pr.1320 ～ Pr.1329、Pr.1389 ～ Pr.1393** で選択したオブジェクトに対応する値を書き込みます。<br>SDO 通信で読み出す場合、マッピングオブジェクトと同じ形式の値を読み出します。<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60420020（初期値）<br>Sub index H02 ～ H0A：H00000020（初期値） | 読出 | 8bit |
| 24574（H5FFE） | H01 | Index:Pr.1320,Sub:Pr.1389(Low) | PDO マッピングオブジェクト H1600 用<br>PDO 通信で書き込む場合、**Pr.1320 ～ Pr.1329、Pr.1389 ～ Pr.1393** で選択したオブジェクトに対応する値を書き込みます。<br>SDO 通信で読み出す場合、マッピングオブジェクトと同じ形式の値を読み出します。<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60420020（初期値）<br>Sub index H02 ～ H0A：H00000020（初期値） | 読出 | 32bit |
| 24574（H5FFE） | H02 | Index:Pr.1321,Sub:Pr.1389(High) | PDO マッピングオブジェクト H1600 用<br>PDO 通信で書き込む場合、**Pr.1320 ～ Pr.1329、Pr.1389 ～ Pr.1393** で選択したオブジェクトに対応する値を書き込みます。<br>SDO 通信で読み出す場合、マッピングオブジェクトと同じ形式の値を読み出します。<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60420020（初期値）<br>Sub index H02 ～ H0A：H00000020（初期値） | 読出 | 32bit |
| 24574（H5FFE） | H03 | Index:Pr.1322,Sub:Pr.1390(Low) | PDO マッピングオブジェクト H1600 用<br>PDO 通信で書き込む場合、**Pr.1320 ～ Pr.1329、Pr.1389 ～ Pr.1393** で選択したオブジェクトに対応する値を書き込みます。<br>SDO 通信で読み出す場合、マッピングオブジェクトと同じ形式の値を読み出します。<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60420020（初期値）<br>Sub index H02 ～ H0A：H00000020（初期値） | 読出 | 32bit |
| 24574（H5FFE） | H04 | Index:Pr.1323,Sub:Pr.1390(High) | PDO マッピングオブジェクト H1600 用<br>PDO 通信で書き込む場合、**Pr.1320 ～ Pr.1329、Pr.1389 ～ Pr.1393** で選択したオブジェクトに対応する値を書き込みます。<br>SDO 通信で読み出す場合、マッピングオブジェクトと同じ形式の値を読み出します。<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60420020（初期値）<br>Sub index H02 ～ H0A：H00000020（初期値） | 読出 | 32bit |
| 24574（H5FFE） | H05 | Index:Pr.1324,Sub:Pr.1391(Low) | PDO マッピングオブジェクト H1600 用<br>PDO 通信で書き込む場合、**Pr.1320 ～ Pr.1329、Pr.1389 ～ Pr.1393** で選択したオブジェクトに対応する値を書き込みます。<br>SDO 通信で読み出す場合、マッピングオブジェクトと同じ形式の値を読み出します。<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60420020（初期値）<br>Sub index H02 ～ H0A：H00000020（初期値） | 読出 | 32bit |
| 24574（H5FFE） | H06 | Index:Pr.1325,Sub:Pr.1391(High) | PDO マッピングオブジェクト H1600 用<br>PDO 通信で書き込む場合、**Pr.1320 ～ Pr.1329、Pr.1389 ～ Pr.1393** で選択したオブジェクトに対応する値を書き込みます。<br>SDO 通信で読み出す場合、マッピングオブジェクトと同じ形式の値を読み出します。<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60420020（初期値）<br>Sub index H02 ～ H0A：H00000020（初期値） | 読出 | 32bit |
| 24574（H5FFE） | H07 | Index:Pr.1326,Sub:Pr.1392(Low) | PDO マッピングオブジェクト H1600 用<br>PDO 通信で書き込む場合、**Pr.1320 ～ Pr.1329、Pr.1389 ～ Pr.1393** で選択したオブジェクトに対応する値を書き込みます。<br>SDO 通信で読み出す場合、マッピングオブジェクトと同じ形式の値を読み出します。<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60420020（初期値）<br>Sub index H02 ～ H0A：H00000020（初期値） | 読出 | 32bit |
| 24574（H5FFE） | H08 | Index:Pr.1327,Sub:Pr.1392(High) | PDO マッピングオブジェクト H1600 用<br>PDO 通信で書き込む場合、**Pr.1320 ～ Pr.1329、Pr.1389 ～ Pr.1393** で選択したオブジェクトに対応する値を書き込みます。<br>SDO 通信で読み出す場合、マッピングオブジェクトと同じ形式の値を読み出します。<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60420020（初期値）<br>Sub index H02 ～ H0A：H00000020（初期値） | 読出 | 32bit |
| 24574（H5FFE） | H09 | Index:Pr.1328,Sub:Pr.1393(Low) | PDO マッピングオブジェクト H1600 用<br>PDO 通信で書き込む場合、**Pr.1320 ～ Pr.1329、Pr.1389 ～ Pr.1393** で選択したオブジェクトに対応する値を書き込みます。<br>SDO 通信で読み出す場合、マッピングオブジェクトと同じ形式の値を読み出します。<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60420020（初期値）<br>Sub index H02 ～ H0A：H00000020（初期値） | 読出 | 32bit |
| 24574（H5FFE） | H0A | Index:Pr.1329,Sub:Pr.1393(High) | PDO マッピングオブジェクト H1600 用<br>PDO 通信で書き込む場合、**Pr.1320 ～ Pr.1329、Pr.1389 ～ Pr.1393** で選択したオブジェクトに対応する値を書き込みます。<br>SDO 通信で読み出す場合、マッピングオブジェクトと同じ形式の値を読み出します。<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60420020（初期値）<br>Sub index H02 ～ H0A：H00000020（初期値） | 読出 | 32bit |
| 24575（H5FFF） | - | TxPDO Parameter Mapping | PDO マッピングオブジェクト H1A00 用<br>PDO 通信で読み出す場合、**Pr.1330 ～ Pr.1343、Pr.1394 ～ Pr.1398** で選択したオブジェクトに対応する値を読み出します。<br>SDO 通信で読み出す場合、マッピングオブジェクトと同じ形式の値を読み出します。<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60430020（初期値）<br>Sub index H02 ～ H0E：H00000020（初期値） | - | - |
| 24575（H5FFF） | H00 | Highest sub-index supported | PDO マッピングオブジェクト H1A00 用<br>PDO 通信で読み出す場合、**Pr.1330 ～ Pr.1343、Pr.1394 ～ Pr.1398** で選択したオブジェクトに対応する値を読み出します。<br>SDO 通信で読み出す場合、マッピングオブジェクトと同じ形式の値を読み出します。<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60430020（初期値）<br>Sub index H02 ～ H0E：H00000020（初期値） | 読出 | 8bit |
| 24575（H5FFF） | H01 | Index:Pr.1330,Sub:Pr.1394(Low) | PDO マッピングオブジェクト H1A00 用<br>PDO 通信で読み出す場合、**Pr.1330 ～ Pr.1343、Pr.1394 ～ Pr.1398** で選択したオブジェクトに対応する値を読み出します。<br>SDO 通信で読み出す場合、マッピングオブジェクトと同じ形式の値を読み出します。<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60430020（初期値）<br>Sub index H02 ～ H0E：H00000020（初期値） | 読出 | 32bit |
| 24575（H5FFF） | H02 | Index:Pr.1331,Sub:Pr.1394(High) | PDO マッピングオブジェクト H1A00 用<br>PDO 通信で読み出す場合、**Pr.1330 ～ Pr.1343、Pr.1394 ～ Pr.1398** で選択したオブジェクトに対応する値を読み出します。<br>SDO 通信で読み出す場合、マッピングオブジェクトと同じ形式の値を読み出します。<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60430020（初期値）<br>Sub index H02 ～ H0E：H00000020（初期値） | 読出 | 32bit |
| 24575（H5FFF） | H03 | Index:Pr.1332,Sub:Pr.1395(Low) | PDO マッピングオブジェクト H1A00 用<br>PDO 通信で読み出す場合、**Pr.1330 ～ Pr.1343、Pr.1394 ～ Pr.1398** で選択したオブジェクトに対応する値を読み出します。<br>SDO 通信で読み出す場合、マッピングオブジェクトと同じ形式の値を読み出します。<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60430020（初期値）<br>Sub index H02 ～ H0E：H00000020（初期値） | 読出 | 32bit |
| 24575（H5FFF） | H04 | Index:Pr.1333,Sub:Pr.1395(High) | PDO マッピングオブジェクト H1A00 用<br>PDO 通信で読み出す場合、**Pr.1330 ～ Pr.1343、Pr.1394 ～ Pr.1398** で選択したオブジェクトに対応する値を読み出します。<br>SDO 通信で読み出す場合、マッピングオブジェクトと同じ形式の値を読み出します。<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60430020（初期値）<br>Sub index H02 ～ H0E：H00000020（初期値） | 読出 | 32bit |
| 24575（H5FFF） | H05 | Index:Pr.1334,Sub:Pr.1396(Low) | PDO マッピングオブジェクト H1A00 用<br>PDO 通信で読み出す場合、**Pr.1330 ～ Pr.1343、Pr.1394 ～ Pr.1398** で選択したオブジェクトに対応する値を読み出します。<br>SDO 通信で読み出す場合、マッピングオブジェクトと同じ形式の値を読み出します。<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60430020（初期値）<br>Sub index H02 ～ H0E：H00000020（初期値） | 読出 | 32bit |
| 24575（H5FFF） | H06 | Index:Pr.1335,Sub:Pr.1396(High) | PDO マッピングオブジェクト H1A00 用<br>PDO 通信で読み出す場合、**Pr.1330 ～ Pr.1343、Pr.1394 ～ Pr.1398** で選択したオブジェクトに対応する値を読み出します。<br>SDO 通信で読み出す場合、マッピングオブジェクトと同じ形式の値を読み出します。<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60430020（初期値）<br>Sub index H02 ～ H0E：H00000020（初期値） | 読出 | 32bit |
| 24575（H5FFF） | H07 | Index:Pr.1336,Sub:Pr.1397(Low) | PDO マッピングオブジェクト H1A00 用<br>PDO 通信で読み出す場合、**Pr.1330 ～ Pr.1343、Pr.1394 ～ Pr.1398** で選択したオブジェクトに対応する値を読み出します。<br>SDO 通信で読み出す場合、マッピングオブジェクトと同じ形式の値を読み出します。<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60430020（初期値）<br>Sub index H02 ～ H0E：H00000020（初期値） | 読出 | 32bit |
| 24575（H5FFF） | H08 | Index:Pr.1337,Sub:Pr.1397(High) | PDO マッピングオブジェクト H1A00 用<br>PDO 通信で読み出す場合、**Pr.1330 ～ Pr.1343、Pr.1394 ～ Pr.1398** で選択したオブジェクトに対応する値を読み出します。<br>SDO 通信で読み出す場合、マッピングオブジェクトと同じ形式の値を読み出します。<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60430020（初期値）<br>Sub index H02 ～ H0E：H00000020（初期値） | 読出 | 32bit |
| 24575（H5FFF） | H09 | Index:Pr.1338,Sub:Pr.1398(Low) | PDO マッピングオブジェクト H1A00 用<br>PDO 通信で読み出す場合、**Pr.1330 ～ Pr.1343、Pr.1394 ～ Pr.1398** で選択したオブジェクトに対応する値を読み出します。<br>SDO 通信で読み出す場合、マッピングオブジェクトと同じ形式の値を読み出します。<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60430020（初期値）<br>Sub index H02 ～ H0E：H00000020（初期値） | 読出 | 32bit |
| 24575（H5FFF） | H0A | Index:Pr.1339,Sub:Pr.1398(High) | PDO マッピングオブジェクト H1A00 用<br>PDO 通信で読み出す場合、**Pr.1330 ～ Pr.1343、Pr.1394 ～ Pr.1398** で選択したオブジェクトに対応する値を読み出します。<br>SDO 通信で読み出す場合、マッピングオブジェクトと同じ形式の値を読み出します。<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60430020（初期値）<br>Sub index H02 ～ H0E：H00000020（初期値） | 読出 | 32bit |
| 24575（H5FFF） | H0B | Index:Pr.1340,Sub:0x00 | PDO マッピングオブジェクト H1A00 用<br>PDO 通信で読み出す場合、**Pr.1330 ～ Pr.1343、Pr.1394 ～ Pr.1398** で選択したオブジェクトに対応する値を読み出します。<br>SDO 通信で読み出す場合、マッピングオブジェクトと同じ形式の値を読み出します。<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60430020（初期値）<br>Sub index H02 ～ H0E：H00000020（初期値） | 読出 | 32bit |
| 24575（H5FFF） | H0C | Index:Pr.1341,Sub:0x00 | PDO マッピングオブジェクト H1A00 用<br>PDO 通信で読み出す場合、**Pr.1330 ～ Pr.1343、Pr.1394 ～ Pr.1398** で選択したオブジェクトに対応する値を読み出します。<br>SDO 通信で読み出す場合、マッピングオブジェクトと同じ形式の値を読み出します。<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60430020（初期値）<br>Sub index H02 ～ H0E：H00000020（初期値） | 読出 | 32bit |
| 24575（H5FFF） | H0D | Index:Pr.1342,Sub:0x00 | PDO マッピングオブジェクト H1A00 用<br>PDO 通信で読み出す場合、**Pr.1330 ～ Pr.1343、Pr.1394 ～ Pr.1398** で選択したオブジェクトに対応する値を読み出します。<br>SDO 通信で読み出す場合、マッピングオブジェクトと同じ形式の値を読み出します。<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60430020（初期値）<br>Sub index H02 ～ H0E：H00000020（初期値） | 読出 | 32bit |
| 24575（H5FFF） | H0E | Index:Pr.1343,Sub:0x00 | PDO マッピングオブジェクト H1A00 用<br>PDO 通信で読み出す場合、**Pr.1330 ～ Pr.1343、Pr.1394 ～ Pr.1398** で選択したオブジェクトに対応する値を読み出します。<br>SDO 通信で読み出す場合、マッピングオブジェクトと同じ形式の値を読み出します。<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60430020（初期値）<br>Sub index H02 ～ H0E：H00000020（初期値） | 読出 | 32bit |

*1　PDO 通信では使用できません。<br>
*2　通信パラメータの設定値がクリアされません。<br>
*3　書込み時は制御入力命令としてデータを設定します。<br>
　　読出し時はインバータ運転状態としてデータが読み出されます。

• 制御入力命令 / インバータ状態、制御入力命令 / インバータ状態（拡張）

（注: 原本では左右2つの表が並ぶ。左表＝制御入力命令 / インバータ状態、右表＝制御入力命令（拡張）/ インバータ状態（拡張））

| Bit | 定義：制御入力命令 | 定義：インバータ状態 |
|---|---|---|
| 0 | - | RUN（インバータ運転中）*2 |
| 1 | - | 正転中 |
| 2 | - | 逆転中 |
| 3 | RH（高速運転指令）*1 | 周波数到達 |
| 4 | RM（中速運転指令）*1 | 過負荷警報 |
| 5 | RL（低速運転指令）*1 | 0 |
| 6 | JOG 運転選択 2 | FU（出力周波数検出）*2 |
| 7 | 第 2 機能選択 | ABC（異常）*2 |
| 8 | 端子 4 入力選択 | ABC2（機能なし）*2 |
| 9 | - | セーフティモニタ出力 2 |
| 10 | MRS（出力停止）*1 | 0 |
| 11 | - | 位置決め完了 |
| 12 | RES（機能なし）*1 | 位置指令動作中 |
| 13 | - | 原点復帰完了 |
| 14 | - | 原点復帰異常 |
| 15 | - | 重故障発生 |

| Bit | 定義：制御入力命令（拡張） | 定義：インバータ状態（拡張） |
|---|---|---|
| 0 | NET X1（機能なし） | NET Y1（機能なし）*2 |
| 1 | NET X2（機能なし）*1 | NET Y2（機能なし）*2 |
| 2 | NET X3（機能なし）*1 | NET Y3（機能なし）*2 |
| 3 | NET X4（機能なし）*1 | NET Y4（機能なし）*2 |
| 4 | NET X5（機能なし）*1 | 0 |
| 5 | - | 0 |
| 6 | - | 0 |
| 7 | - | 0 |
| 8 | - | 0 |
| 9 | - | 0 |
| 10 | - | 0 |
| 11 | - | 0 |
| 12 | - | 0 |
| 13 | - | 0 |
| 14 | - | 0 |
| 15 | - | 0 |

*1　（　）内の信号は初期状態のものです。**Pr.180 ～ Pr.189（入力端子機能選択）**の設定により内容が変更します。<br>
　　詳細は取扱説明書（機能編）の **Pr.180 ～ Pr.189（入力端子機能選択）**を参照してください。<br>
　　各割付け信号は、各々 NET での有効 / 無効があります。（取扱説明書（機能編）参照）<br>
*2　（　）内の信号は初期状態のものです。**Pr.190 ～ Pr.197（出力端子機能選択）**の設定により内容が変更します。<br>
　　詳細は取扱説明書（機能編）の **Pr.190 ～ Pr.197（出力端子機能選択）**を参照してください。

• Safety 入力状態

| Bit | 定義 |
|---|---|
| 0 | 0：端子 S1 が ON<br>1：端子 S1 が OFF（出力遮断中） |
| 1 | 0：端子 S2 が ON<br>1：端子 S2 が OFF（出力遮断中） |
| 2 ～ 15 | 0 |


##### ◆ CoE 通信エリア (2.13.5 / 原本 p.215)

（注: 本表は原本 p.215〜p.218 にまたがる。H1620・H1A00 は原本 p.216、H1A20・H1C00・H1C12 は原本 p.217、H1C13・H1C32・H1C33 は原本 p.218。内容欄の結合セルは各行に展開）

| Index | Sub index | 名称 | 内容 | 読出 / 書込 | サイズ |
|---|---|---|---|---|---|
| H1000 | H00 | Device Type | 対応プロファイル情報<br>Bit0 ～ 15 Device Profile Number：H0192<br>（402：CiA402）<br>Bit16 ～ 23 Additional Information(Type)：H01<br>（Frequency Converter：インバータ )<br>Bit24 ～ 31：H00 | 読出 | 32bit |
| H1001 | H00 | Error Register | エラーの発生状況<br>Bit0：<br>1：エラー発生中、0：エラーなし<br>Bit1 ～ 7：0 固定 | 読出 | 8bit |
| H1008 | H00 | Manufacturer Device Name | インバータ機種名：FR-E800-E | 読出 | - |
| H1009 | H00 | Manufacturer Hardware version | H/W バージョン | 読出 | - |
| H100A | H00 | Manufacturer Software version | S/W バージョン | 読出 | - |
| H1018 | - | Identity Object | - | - | - |
| H1018 | H00 | Highest sub-index supported | サブインデックスの最大値：H04 | 読出 | 8bit |
| H1018 | H01 | Vendor ID | ベンダー ID：H00000A1E | 読出 | 32bit |
| H1018 | H02 | Product Code | プロダクトコード：H02000301 | 読出 | 32bit |
| H1018 | H03 | Revision Number | リビジョン番号 | 読出 | 32bit |
| H1018 | H04 | Serial Number | シリアルナンバ | 読出 | 32bit |
| H1600 | - | 1st receive PDO mapping | - | - | - |
| H1600 | H00 | Highest sub-index supported | サブインデックスの最大値：H0B（11）（固定） | 読出 | 8bit |
| H1600 | H01 | Mapped Object 001 | インバータパラメータでマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60400010（Controlword）（固定）<br>Sub index H02 ～ H0B：H5FFE0120 ～ H5FFE0A20（固定） | 読出 | 32bit |
| H1600 | H02 | Mapped Object 002 | インバータパラメータでマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60400010（Controlword）（固定）<br>Sub index H02 ～ H0B：H5FFE0120 ～ H5FFE0A20（固定） | 読出 | 32bit |
| H1600 | H03 | Mapped Object 003 | インバータパラメータでマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60400010（Controlword）（固定）<br>Sub index H02 ～ H0B：H5FFE0120 ～ H5FFE0A20（固定） | 読出 | 32bit |
| H1600 | H04 | Mapped Object 004 | インバータパラメータでマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60400010（Controlword）（固定）<br>Sub index H02 ～ H0B：H5FFE0120 ～ H5FFE0A20（固定） | 読出 | 32bit |
| H1600 | H05 | Mapped Object 005 | インバータパラメータでマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60400010（Controlword）（固定）<br>Sub index H02 ～ H0B：H5FFE0120 ～ H5FFE0A20（固定） | 読出 | 32bit |
| H1600 | H06 | Mapped Object 006 | インバータパラメータでマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60400010（Controlword）（固定）<br>Sub index H02 ～ H0B：H5FFE0120 ～ H5FFE0A20（固定） | 読出 | 32bit |
| H1600 | H07 | Mapped Object 007 | インバータパラメータでマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60400010（Controlword）（固定）<br>Sub index H02 ～ H0B：H5FFE0120 ～ H5FFE0A20（固定） | 読出 | 32bit |
| H1600 | H08 | Mapped Object 008 | インバータパラメータでマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60400010（Controlword）（固定）<br>Sub index H02 ～ H0B：H5FFE0120 ～ H5FFE0A20（固定） | 読出 | 32bit |
| H1600 | H09 | Mapped Object 009 | インバータパラメータでマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60400010（Controlword）（固定）<br>Sub index H02 ～ H0B：H5FFE0120 ～ H5FFE0A20（固定） | 読出 | 32bit |
| H1600 | H0A | Mapped Object 010 | インバータパラメータでマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60400010（Controlword）（固定）<br>Sub index H02 ～ H0B：H5FFE0120 ～ H5FFE0A20（固定） | 読出 | 32bit |
| H1600 | H0B | Mapped Object 011 | インバータパラメータでマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60400010（Controlword）（固定）<br>Sub index H02 ～ H0B：H5FFE0120 ～ H5FFE0A20（固定） | 読出 | 32bit |
| H1620 | - | 33rd receive PDO mapping | - | - | - |
| H1620 | H00 | Highest sub-index supported | サブインデックスの最大値<br>設定範囲：H00 ～ H0B<br>初期値：H02 | 読出 / 書込 *1 | 8bit |
| H1620 | H01 | Mapped Object 001 | SDO 通信によりマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60400010（Controlword）（固定）<br>Sub index H02：H60420010（初期値）<br>Sub index H03 ～ H0B：H00000000（初期値）<br>SDO Complete Access の場合以外、Sub index H01 ～ H0B への書込みは、一度 Sub index H00 を “0” に設定してから行ってください。 | 読出 / 書込 *1 | 32bit |
| H1620 | H02 | Mapped Object 002 | SDO 通信によりマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60400010（Controlword）（固定）<br>Sub index H02：H60420010（初期値）<br>Sub index H03 ～ H0B：H00000000（初期値）<br>SDO Complete Access の場合以外、Sub index H01 ～ H0B への書込みは、一度 Sub index H00 を “0” に設定してから行ってください。 | 読出 / 書込 *1 | 32bit |
| H1620 | H03 | Mapped Object 003 | SDO 通信によりマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60400010（Controlword）（固定）<br>Sub index H02：H60420010（初期値）<br>Sub index H03 ～ H0B：H00000000（初期値）<br>SDO Complete Access の場合以外、Sub index H01 ～ H0B への書込みは、一度 Sub index H00 を “0” に設定してから行ってください。 | 読出 / 書込 *1 | 32bit |
| H1620 | H04 | Mapped Object 004 | SDO 通信によりマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60400010（Controlword）（固定）<br>Sub index H02：H60420010（初期値）<br>Sub index H03 ～ H0B：H00000000（初期値）<br>SDO Complete Access の場合以外、Sub index H01 ～ H0B への書込みは、一度 Sub index H00 を “0” に設定してから行ってください。 | 読出 / 書込 *1 | 32bit |
| H1620 | H05 | Mapped Object 005 | SDO 通信によりマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60400010（Controlword）（固定）<br>Sub index H02：H60420010（初期値）<br>Sub index H03 ～ H0B：H00000000（初期値）<br>SDO Complete Access の場合以外、Sub index H01 ～ H0B への書込みは、一度 Sub index H00 を “0” に設定してから行ってください。 | 読出 / 書込 *1 | 32bit |
| H1620 | H06 | Mapped Object 006 | SDO 通信によりマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60400010（Controlword）（固定）<br>Sub index H02：H60420010（初期値）<br>Sub index H03 ～ H0B：H00000000（初期値）<br>SDO Complete Access の場合以外、Sub index H01 ～ H0B への書込みは、一度 Sub index H00 を “0” に設定してから行ってください。 | 読出 / 書込 *1 | 32bit |
| H1620 | H07 | Mapped Object 007 | SDO 通信によりマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60400010（Controlword）（固定）<br>Sub index H02：H60420010（初期値）<br>Sub index H03 ～ H0B：H00000000（初期値）<br>SDO Complete Access の場合以外、Sub index H01 ～ H0B への書込みは、一度 Sub index H00 を “0” に設定してから行ってください。 | 読出 / 書込 *1 | 32bit |
| H1620 | H08 | Mapped Object 008 | SDO 通信によりマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60400010（Controlword）（固定）<br>Sub index H02：H60420010（初期値）<br>Sub index H03 ～ H0B：H00000000（初期値）<br>SDO Complete Access の場合以外、Sub index H01 ～ H0B への書込みは、一度 Sub index H00 を “0” に設定してから行ってください。 | 読出 / 書込 *1 | 32bit |
| H1620 | H09 | Mapped Object 009 | SDO 通信によりマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60400010（Controlword）（固定）<br>Sub index H02：H60420010（初期値）<br>Sub index H03 ～ H0B：H00000000（初期値）<br>SDO Complete Access の場合以外、Sub index H01 ～ H0B への書込みは、一度 Sub index H00 を “0” に設定してから行ってください。 | 読出 / 書込 *1 | 32bit |
| H1620 | H0A | Mapped Object 010 | SDO 通信によりマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60400010（Controlword）（固定）<br>Sub index H02：H60420010（初期値）<br>Sub index H03 ～ H0B：H00000000（初期値）<br>SDO Complete Access の場合以外、Sub index H01 ～ H0B への書込みは、一度 Sub index H00 を “0” に設定してから行ってください。 | 読出 / 書込 *1 | 32bit |
| H1620 | H0B | Mapped Object 011 | SDO 通信によりマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60400010（Controlword）（固定）<br>Sub index H02：H60420010（初期値）<br>Sub index H03 ～ H0B：H00000000（初期値）<br>SDO Complete Access の場合以外、Sub index H01 ～ H0B への書込みは、一度 Sub index H00 を “0” に設定してから行ってください。 | 読出 / 書込 *1 | 32bit |
| H1A00 | - | 1st transmit PDO mapping | - | - | - |
| H1A00 | H00 | Highest sub-index supported | サブインデックスの最大値：H0F（15）（固定） | 読出 | 8bit |
| H1A00 | H01 | Mapped Object 001 | インバータパラメータでマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02 ～ H0F：H5FFF0120 ～ H5FFF0E20（固定） | 読出 | 32bit |
| H1A00 | H02 | Mapped Object 002 | インバータパラメータでマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02 ～ H0F：H5FFF0120 ～ H5FFF0E20（固定） | 読出 | 32bit |
| H1A00 | H03 | Mapped Object 003 | インバータパラメータでマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02 ～ H0F：H5FFF0120 ～ H5FFF0E20（固定） | 読出 | 32bit |
| H1A00 | H04 | Mapped Object 004 | インバータパラメータでマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02 ～ H0F：H5FFF0120 ～ H5FFF0E20（固定） | 読出 | 32bit |
| H1A00 | H05 | Mapped Object 005 | インバータパラメータでマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02 ～ H0F：H5FFF0120 ～ H5FFF0E20（固定） | 読出 | 32bit |
| H1A00 | H06 | Mapped Object 006 | インバータパラメータでマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02 ～ H0F：H5FFF0120 ～ H5FFF0E20（固定） | 読出 | 32bit |
| H1A00 | H07 | Mapped Object 007 | インバータパラメータでマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02 ～ H0F：H5FFF0120 ～ H5FFF0E20（固定） | 読出 | 32bit |
| H1A00 | H08 | Mapped Object 008 | インバータパラメータでマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02 ～ H0F：H5FFF0120 ～ H5FFF0E20（固定） | 読出 | 32bit |
| H1A00 | H09 | Mapped Object 009 | インバータパラメータでマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02 ～ H0F：H5FFF0120 ～ H5FFF0E20（固定） | 読出 | 32bit |
| H1A00 | H0A | Mapped Object 010 | インバータパラメータでマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02 ～ H0F：H5FFF0120 ～ H5FFF0E20（固定） | 読出 | 32bit |
| H1A00 | H0B | Mapped Object 011 | インバータパラメータでマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02 ～ H0F：H5FFF0120 ～ H5FFF0E20（固定） | 読出 | 32bit |
| H1A00 | H0C | Mapped Object 012 | インバータパラメータでマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02 ～ H0F：H5FFF0120 ～ H5FFF0E20（固定） | 読出 | 32bit |
| H1A00 | H0D | Mapped Object 013 | インバータパラメータでマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02 ～ H0F：H5FFF0120 ～ H5FFF0E20（固定） | 読出 | 32bit |
| H1A00 | H0E | Mapped Object 014 | インバータパラメータでマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02 ～ H0F：H5FFF0120 ～ H5FFF0E20（固定） | 読出 | 32bit |
| H1A00 | H0F | Mapped Object 015 | インバータパラメータでマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02 ～ H0F：H5FFF0120 ～ H5FFF0E20（固定） | 読出 | 32bit |
| H1A20 | - | 33rd transmit PDO mapping | - | - | - |
| H1A20 | H00 | Highest sub-index supported | サブインデックスの最大値<br>設定範囲：H00 ～ H0F<br>初期値：H02 | 読出 / 書込 *1 | 8bit |
| H1A20 | H01 | Mapped Object 001 | SDO 通信によりマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02：H60430010（初期値）<br>Sub index H03 ～ H0F：H00000000（初期値）<br>SDO Complete Access の場合以外、Sub index H01 ～ H0F への書込みは、一度 Sub index H00 を “0” に設定してから行ってください。 | 読出 / 書込 *1 | 32bit |
| H1A20 | H02 | Mapped Object 002 | SDO 通信によりマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02：H60430010（初期値）<br>Sub index H03 ～ H0F：H00000000（初期値）<br>SDO Complete Access の場合以外、Sub index H01 ～ H0F への書込みは、一度 Sub index H00 を “0” に設定してから行ってください。 | 読出 / 書込 *1 | 32bit |
| H1A20 | H03 | Mapped Object 003 | SDO 通信によりマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02：H60430010（初期値）<br>Sub index H03 ～ H0F：H00000000（初期値）<br>SDO Complete Access の場合以外、Sub index H01 ～ H0F への書込みは、一度 Sub index H00 を “0” に設定してから行ってください。 | 読出 / 書込 *1 | 32bit |
| H1A20 | H04 | Mapped Object 004 | SDO 通信によりマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02：H60430010（初期値）<br>Sub index H03 ～ H0F：H00000000（初期値）<br>SDO Complete Access の場合以外、Sub index H01 ～ H0F への書込みは、一度 Sub index H00 を “0” に設定してから行ってください。 | 読出 / 書込 *1 | 32bit |
| H1A20 | H05 | Mapped Object 005 | SDO 通信によりマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02：H60430010（初期値）<br>Sub index H03 ～ H0F：H00000000（初期値）<br>SDO Complete Access の場合以外、Sub index H01 ～ H0F への書込みは、一度 Sub index H00 を “0” に設定してから行ってください。 | 読出 / 書込 *1 | 32bit |
| H1A20 | H06 | Mapped Object 006 | SDO 通信によりマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02：H60430010（初期値）<br>Sub index H03 ～ H0F：H00000000（初期値）<br>SDO Complete Access の場合以外、Sub index H01 ～ H0F への書込みは、一度 Sub index H00 を “0” に設定してから行ってください。 | 読出 / 書込 *1 | 32bit |
| H1A20 | H07 | Mapped Object 007 | SDO 通信によりマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02：H60430010（初期値）<br>Sub index H03 ～ H0F：H00000000（初期値）<br>SDO Complete Access の場合以外、Sub index H01 ～ H0F への書込みは、一度 Sub index H00 を “0” に設定してから行ってください。 | 読出 / 書込 *1 | 32bit |
| H1A20 | H08 | Mapped Object 008 | SDO 通信によりマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02：H60430010（初期値）<br>Sub index H03 ～ H0F：H00000000（初期値）<br>SDO Complete Access の場合以外、Sub index H01 ～ H0F への書込みは、一度 Sub index H00 を “0” に設定してから行ってください。 | 読出 / 書込 *1 | 32bit |
| H1A20 | H09 | Mapped Object 009 | SDO 通信によりマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02：H60430010（初期値）<br>Sub index H03 ～ H0F：H00000000（初期値）<br>SDO Complete Access の場合以外、Sub index H01 ～ H0F への書込みは、一度 Sub index H00 を “0” に設定してから行ってください。 | 読出 / 書込 *1 | 32bit |
| H1A20 | H0A | Mapped Object 010 | SDO 通信によりマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02：H60430010（初期値）<br>Sub index H03 ～ H0F：H00000000（初期値）<br>SDO Complete Access の場合以外、Sub index H01 ～ H0F への書込みは、一度 Sub index H00 を “0” に設定してから行ってください。 | 読出 / 書込 *1 | 32bit |
| H1A20 | H0B | Mapped Object 011 | SDO 通信によりマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02：H60430010（初期値）<br>Sub index H03 ～ H0F：H00000000（初期値）<br>SDO Complete Access の場合以外、Sub index H01 ～ H0F への書込みは、一度 Sub index H00 を “0” に設定してから行ってください。 | 読出 / 書込 *1 | 32bit |
| H1A20 | H0C | Mapped Object 012 | SDO 通信によりマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02：H60430010（初期値）<br>Sub index H03 ～ H0F：H00000000（初期値）<br>SDO Complete Access の場合以外、Sub index H01 ～ H0F への書込みは、一度 Sub index H00 を “0” に設定してから行ってください。 | 読出 / 書込 *1 | 32bit |
| H1A20 | H0D | Mapped Object 013 | SDO 通信によりマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02：H60430010（初期値）<br>Sub index H03 ～ H0F：H00000000（初期値）<br>SDO Complete Access の場合以外、Sub index H01 ～ H0F への書込みは、一度 Sub index H00 を “0” に設定してから行ってください。 | 読出 / 書込 *1 | 32bit |
| H1A20 | H0E | Mapped Object 014 | SDO 通信によりマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02：H60430010（初期値）<br>Sub index H03 ～ H0F：H00000000（初期値）<br>SDO Complete Access の場合以外、Sub index H01 ～ H0F への書込みは、一度 Sub index H00 を “0” に設定してから行ってください。 | 読出 / 書込 *1 | 32bit |
| H1A20 | H0F | Mapped Object 015 | SDO 通信によりマッピングされているオブジェクト<br>Bit16 ～ 31：インデックス<br>Bit8 ～ 15：サブインデックス<br>Bit0 ～ 7：オブジェクトサイズ（bit）<br>Sub index H01：H60410010（Statusword）（固定）<br>Sub index H02：H60430010（初期値）<br>Sub index H03 ～ H0F：H00000000（初期値）<br>SDO Complete Access の場合以外、Sub index H01 ～ H0F への書込みは、一度 Sub index H00 を “0” に設定してから行ってください。 | 読出 / 書込 *1 | 32bit |
| H1C00 | - | Sync Manager Communication Type | - | - | - |
| H1C00 | H00 | Highest sub-index supported | サブインデックスの最大値：H04 | 読出 | 8bit |
| H1C00 | H01 | Sync Manager 0 | メールボックス受信（マスタ→インバータ） | 読出 | 8bit |
| H1C00 | H02 | Sync Manager 1 | メールボックス送信（インバータ→マスタ） | 読出 | 8bit |
| H1C00 | H03 | Sync Manager 2 | PDO 出力（マスタ→インバータ） | 読出 | 8bit |
| H1C00 | H04 | Sync Manager 3 | PDO 入力（インバータ→マスタ） | 読出 | 8bit |
| H1C12 | - | Sync Manager RxPDO Assign | - | - | - |
| H1C12 | H00 | Highest sub-index supported | サブインデックスの最大値<br>設定範囲：H00、H01<br>初期値：H01 | 読出 / 書込 *1 | 8bit |
| H1C12 | H01 | assigned RxPDO 001 | Sync Manager 2（RxPDO）に割り当てる PDO マッピングオブジェクト<br>設定範囲：H1600、H1620<br>初期値：H1600<br>SDO Complete Access の場合以外、Sub index H01 への書込みは、一度 Sub index H00 を “0” に設定してから行ってください。 | 読出 / 書込 *1 | 16bit |
| H1C13 | - | Sync Manager TxPDO Assign | - | - | - |
| H1C13 | H00 | Highest sub-index supported | サブインデックスの最大値<br>設定範囲：H00、H01<br>初期値：H01 | 読出 / 書込 *1 | 8bit |
| H1C13 | H01 | assigned TxPDO 001 | Sync Manager 3（TxPDO）に割り当てる PDO マッピングオブジェクト<br>設定範囲：H1A00、H1A20<br>初期値：H1A00<br>SDO Complete Access の場合以外、Sub index H01 への書込みは、一度 Sub index H00 を “0” に設定してから行ってください。 | 読出 / 書込 *1 | 16bit |
| H1C32 | - | Sync Manager 2 Synchronization | - | - | - |
| H1C32 | H00 | Highest sub-index supported | サブインデックスの最大値：H04 | 読出 | 8bit |
| H1C32 | H01 | Synchronization Type | 同期モード<br>H0000：Free-Run | 読出 | 16bit |
| H1C32 | H04 | Synchronization Types supported | サポートする同期モード<br>H0001：Free-Run is supported | 読出 | 16bit |
| H1C33 | - | Sync Manager 3 Synchronization | - | - | - |
| H1C33 | H00 | Highest sub-index supported | サブインデックスの最大値：H04 | 読出 | 8bit |
| H1C33 | H01 | Synchronization Type | 同期モード<br>H0000：Free-Run | 読出 | 16bit |
| H1C33 | H04 | Synchronization Types supported | サポートする同期モード<br>H0001：Free-Run is supported | 読出 | 16bit |

*1　書込みは Pre-Operational ステートでのみ可能です。

#### 2.13.6 異常発生時の動作 (2.13.6 / 印刷 p.217 / 原本 p.218)

##### ◆ 断線検出機能 (2.13.6 / 原本 p.218)

- **Pr.1431 Ethernet 断線検出機能選択**の設定に従い断線検出を行います。2024 年 8 月以前に製造された FR-E800-EPC では、**Pr.1457 Ethernet 断線検出機能選択 拡張パラメータ**は対応しないため、**Pr.1457** ＝ “9999” と同じ動作となります。（226 ページ参照）

##### ◆ EtherCAT 通信異常 (2.13.6 / 原本 p.218)

- EtherCAT 通信異常検出時の動作を下表に示します。

（注: インバータ動作欄は3行の結合セル。各行に展開）

| 異常内容 | 原因 | インバータ動作 |
|---|---|---|
| ステータス遷移異常 | マスタが要求した EtherCAT ステートと異なる、またはマスタが要求した EtherCAT ステートに変更できない（マスタが再起動した場合など） | マスタにエラー情報を送信して EtherCAT ステートを変更します。インバータ運転中に Operational から他の状態に遷移した場合、**Pr.502 通信異常時停止モード選択**の設定に従い動作します。（310 ページ参照） |
| シンクマネージャ（SM）変更異常 | SM 設定が正しくない（SM が無効になった場合など） | マスタにエラー情報を送信して EtherCAT ステートを変更します。インバータ運転中に Operational から他の状態に遷移した場合、**Pr.502 通信異常時停止モード選択**の設定に従い動作します。（310 ページ参照） |
| PDO 通信タイムアウト | ウォッチドッグがタイムアウトした（断線、マスタからの出力が更新されない、マスタが再起動した場合など） | マスタにエラー情報を送信して EtherCAT ステートを変更します。インバータ運転中に Operational から他の状態に遷移した場合、**Pr.502 通信異常時停止モード選択**の設定に従い動作します。（310 ページ参照） |

- ウォッチドッグタイマ

| 監視対象 | リセットトリガ | オーバーフロー時間（タイムアウト時間） |
|---|---|---|
| プロセスデータ | Sync Manager 2 | 100ms（初期値） |

##### ◆ パラメータ記憶素子異常（制御基板） (2.13.6 / 原本 p.218)

- ファームウェアアップデート後、SII(Slave Information Interface) へのアクセスに異常があった場合は、E.PE が発生します。インバータリセットを行ってください。

#### 2.13.7 プログラミング例 (2.13.7 / 印刷 p.217 / 原本 p.218)

エンジニアリングツールによるプログラミング例を示します。

##### ◆ PDO 通信により 1500r/min 正転で運転する場合 (2.13.7 / 原本 p.219)

- ネットワーク設定、デバイス例

| ローカル変数名 | データ型 | コメント |
|---|---|---|
| E001_Output_enable | BOOL | インバータ 1_ 出力有効 |
| E001_Input_enable | BOOL | インバータ 1_ 入力有効 |
| E001_Rotation | BOOL | インバータ 1_ 正転 |

| グローバル変数名 | PDO マッピング | 備考 |
|---|---|---|
| E001_Controlword | Controlword | |
| E001_rPDO2 | vl target velocity | **Pr.1320 周期通信入力データ選択 1** |
| E001_Statusword | Statusword | |
| E001_tPDO2 | vl velocity demand | **Pr.1330 周期通信出力データ選択 1** |

- 始動指令、速度指令の設定

PDO 通信が確立すると E001_Output_enable、E001_Input_enable が ON となります。<br>
PDS 状態遷移により「Switched on」状態となります。

速度指令を 1500r/min に設定します（**Pr.81 モータ極数**は 4 極の場合（初期値））。<br>
速度指令：vl target velocity（H6042）＝ 1500r/min

E001_Rotation を ON にすると enable operation が ON となり、1500r/min 正転で運転します。<br>
E001_Rotation を OFF にすると停止します。<br>
逆転で運転する場合は vl target velocity にマイナスの値を設定します。

【図】ラダープログラム例（PDO 通信により 1500r/min 正転） (原本 p.219)

- ステップ 0:
  - a接点「インバータ1確立*1」と b接点「インバータ1エラー*1」の直列 → コイル E001_Output_enable（インバータ1_出力有効）
  - 上記直列の後から分岐し、b接点「入力データ無効*1」を経て → コイル E001_Input_enable（インバータ1_入力有効）
- ステップ 1: a接点 E001_Input_enable（インバータ1_入力有効）と a接点 E001_Output_enable（インバータ1_出力有効）の直列の後、4本に分岐
  - 分岐1「Switch on disabled」: 比較 `=`（EN、In1 = uint#16#240、In2 = E001_Statusword）成立 → MOVE「Shutdown」（In = UINT#16#6、Out = E001_Controlword）
  - 分岐2「Ready to switch on」: 比較 `=`（In1 = uint#16#221、In2 = E001_Statusword）成立 → 縦線で2つの MOVE に並列接続
    - MOVE「Switch on」（In = UINT#16#7、Out = E001_Controlword）
    - MOVE（In = DINT#10#1500、Out = E001_rPDO2）
  - 分岐3「Operation enabled」: 比較 `=`（In1 = uint#16#227、In2 = E001_Statusword）成立 かつ b接点 E001_Rotation（インバータ1_正転）→ 分岐2 と同じ縦線に合流（MOVE「Switch on」UINT#16#7→E001_Controlword、MOVE DINT#10#1500→E001_rPDO2 を実行）
  - 分岐4「Switched on」: 比較 `=`（In1 = uint#16#223、In2 = E001_Statusword）成立 かつ a接点 E001_Rotation（インバータ1_正転）→ MOVE「Enable operation」（In = UINT#16#F、Out = E001_Controlword）

（注: 原本はラベル・ファンクションを用いたラダー図。以下は図の接続関係を表す擬似ニモニックで、原本にニモニック表記はない）

```
// ステップ0
LD   インバータ1確立*1
ANI  インバータ1エラー*1
OUT  E001_Output_enable          // インバータ1_出力有効
ANI  入力データ無効*1
OUT  E001_Input_enable           // インバータ1_入力有効
// ステップ1
LD   E001_Input_enable
AND  E001_Output_enable
MPS
AND= uint#16#240 E001_Statusword       // Switch on disabled
MOVE UINT#16#6 E001_Controlword        // Shutdown
MRD
LD=  uint#16#221 E001_Statusword       // Ready to switch on
LD=  uint#16#227 E001_Statusword       // Operation enabled
ANI  E001_Rotation                     // インバータ1_正転
ORB
ANB
MOVE UINT#16#7 E001_Controlword        // Switch on
MOVE DINT#10#1500 E001_rPDO2
MPP
AND= uint#16#223 E001_Statusword       // Switched on
AND  E001_Rotation                     // インバータ1_正転
MOVE UINT#16#F E001_Controlword        // Enable operation
```

*1　使用するマスタによります。マスタユニットユーザーズマニュアルを参照してください。


---

## 転記時の要確認一覧 (2.13 / 原本 p.195-219)

（注: 転記担当が記録した、原本の不整合・判読上の注意。原文はいずれも原本どおり転記済み）

1. 原本 p.201～202 プロファイルエリア表の注記 *1～*4 の本文は担当範囲外（原本 p.205）にあり、本パートには含めていない。結合時に参照先として確認のこと。
2. 原本 p.202 H6048/H6049/H604A の例「1500r/min まで 3.7s 加速したい場合は、Sub index H01 を 15000r/min、Sub index H02 を 37s に設定」は原文どおり転記（1500→15000、3.7→37 の単位倍率についての説明は担当範囲内に無い。不整合か単位系による表記か要確認）。
3. 原本 p.196 の EC RN LED「緑点滅（50ms 間隔）＝Initialization ステート」は原文どおり（ESM の状態定義表には Initialization ステートの記載なし）。

- 原本 p.213 インバータ制御パラメータ表: 20488（H5008）は「制御入力命令 / インバータ状態（拡張）」、20489（H5009）は「制御入力命令 / インバータ状態」と原本どおり転記（番号順と拡張/非拡張の並びが一般的な想定と逆に見えるが原本の記載のまま）。
- 原本 p.219 のプログラミング例はラダー図のみで、mdの擬似ニモニックは転記者が図の接続関係から起こしたもの（ステップ1の分岐3がb接点 E001_Rotation を経て分岐2の縦線に合流する接続は画像から判断）。
