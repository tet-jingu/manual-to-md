# 三菱 FR-E800 取扱説明書（通信編） 第2章 2.12 PROFINET

| 項目 | 内容 |
|---|---|
| 原本 | 三菱電機 FR-E800 取扱説明書（通信編） |
| 発行元 | 三菱電機株式会社 |
| 資料番号 / 版数 | IB-0600870 / S版（PDFメタデータ subject: IB-0600870-S） |
| 原本PDF | `PDF/【三菱】インバータ FR-E800 取扱説明書(通信編)_ib0600870s.pdf` (全330ページ) |
| 本ファイルの範囲 | 2.12 (印刷 p.170-193 / PDF p.171-194) |
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

## 主要用語 対訳表 (Glossary) (2.12 / 原本 p.171-194)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| 周期通信入力データ選択 | Cyclic communication input data selection | Pr.1320～Pr.1329 / N810～N819 | 参考訳 |
| 周期通信出力データ選択 | Cyclic communication output data selection | Pr.1330～Pr.1343 / N850～N863 | 参考訳 |
| 周期通信入力データ選択サブ | Cyclic communication input data selection sub | Pr.1389～Pr.1393 / N830～N839 | 参考訳 |
| 周期通信出力データ選択サブ | Cyclic communication output data selection sub | Pr.1394～Pr.1398 / N870～N879 | 参考訳 |
| Ethernet 機能選択 | Ethernet function selection | Pr.1427～Pr.1430 / N630～N633 | 参考訳 |
| リンク速度とデュプレックス | Link speed and duplex | Pr.1426 / N641 | 参考訳 |
| Ethernet 操作権指定 IP アドレス | Ethernet command source selection IP address | Pr.1449～Pr.1454 | 参考訳 |
| Ethernet 通信チェック時間間隔 | Ethernet communication check time interval | Pr.1432 | 参考訳 |
| 安全通信機能選択 | Safety communication function selection | Pr.S002 | 参考訳 |
| 通信状態 | Network status | NS | 参考訳 |
| インバータ状態 | Module (inverter) status | MS | 参考訳 |
| 通信用コネクタ | Communication connector | PORT1 / PORT2 | 参考訳 |
| 自動交渉 | Auto-negotiation | Pr.1426=0 | 参考訳 |
| 全二重／半二重 | Full duplex / Half duplex | — | 参考訳 |
| 設定周波数有効 | Enable/Disable Setpoint | STW1 bit6 | 原本併記 |
| 出力遮断 | No Coast Stop/Coast Stop | STW1 bit1 | 原本併記 |
| 緊急停止 | No Quick Stop/Quick Stop | STW1 bit2 | 原本併記 |
| 運転許可 | Enable/Disable Operation | STW1 bit3 | 原本併記 |
| 加減速中断 | Unfreeze/Freeze Ramp Generator | STW1 bit5 | 原本併記 |
| エラークリア | Fault Acknowledge (0 → 1) | STW1 bit7 | 原本併記 |
| シーケンサからの DOIO データ有効 | Control By PLC/No Control By PLC | STW1 bit10 | 原本併記 |
| 設定トルク有効 | Target torque enabled | STW1 bit11 | 原本併記 |
| 始動指令方向選択 | Start command direction selection (Device-specific) | STW1 bit12 | 参考訳 |
| 原点復帰 / 位置決め運転開始 | Home position return / positioning start (Device-specific) | STW1 bit13 | 参考訳 |
| 出力停止中 | Coast Stop Not Activated/Coast Stop Activated | ZSW1 bit4 | 原本併記 |
| 緊急停止中 | Quick Stop Not Activated/Quick Stop Activated | ZSW1 bit5 | 原本併記 |
| 上限周波数 | Maximum frequency | Pr.1、Pr.18 | 参考訳 |
| 基底周波数 | Base frequency | Pr.3 | 参考訳 |
| 設定周波数（速度制限値） | Set frequency (speed limit) | NSOLL_A | 参考訳 |
| 出力周波数 | Output frequency | NIST_A | 参考訳 |
| 停止中（初期状態） | Switching On Inhibited | S1 | 原本併記 |
| 停止中（準備状態） | Ready For Switching On | S2 | 原本併記 |
| 停止中（待機状態） | Switched On | S3 | 原本併記 |
| 運転中（運転可能状態） | Operation | S4 | 原本併記 |
| 減速停止中 | Switching Off | S5 | 原本併記 |
| 通常の減速停止 | ramp stop | S5-1 | 原本併記 |
| 通信異常による減速停止 | fault stop | S5-3 | 原本併記 |
| 出力遮断（フリーラン停止） | Coast stop | STW1 bit1 | 原本併記 |
| 状態遷移 | State transition | — | 参考訳 |
| 遷移番号 | Transition number | (0)〜(20) | 参考訳 |
| 制御電源 ON | Power supply ON | (0) | 原本併記 |
| モータ停止 | Standstill detected | (11)(14) | 原本併記 |
| 目標トルク | Target torque | Pr.805 / 信号番号100 | 原本併記 |
| 実トルク | Actual torque | 信号番号101 / モニタコード07h | 原本併記 |
| ドライブプロファイルパラメータ | Drive Profile Parameters (Acyclic Data Exchange) | PNU 0〜65535 | 原本併記 |
| テレグラム選択 | Telegram selection | P922 | 原本併記 |
| アラームメッセージカウンタ | Fault message counter | P944 | 原本併記 |
| アラーム番号 | Fault numbers | P947 | 原本併記 |
| ドライブユニット識別 | Drive Unit identification | P964 | 原本併記 |
| プロファイル識別番号 | Profile identification number | P965 | 原本併記 |
| ドライブリセット | Drive reset | P972 | 原本併記 |
| ドライブオブジェクト識別 | DO identification | P975 | 原本併記 |
| パラメータデータベース | Parameter Database Handling and Identification | P980 | 原本併記 |
| インバータパラメータ | Inverter Parameters | P12288〜P16383 | 原本併記 |
| モニタデータ | Monitor Data | P16384〜P20479 | 原本併記 |
| インバータ制御パラメータ | Inverter Control Parameters | P20480〜P24575 | 原本併記 |
| CiA402 ドライブプロファイル | CiA402 Drive Profile | P24576〜P28671 | 原本併記 |
| 校正パラメータ | Calibration parameters | C0〜C45 (Pr.900〜Pr.935) | 参考訳 |
| 制御入力命令 / インバータ状態 | Control input command / Inverter status | P20489 (5009h) | 参考訳 |
| アラーム履歴 | Alarm history | P20981〜P20990 | 参考訳 |
| 局名 | Name of station | P61000 | 原本併記 |
| Safety 入力状態 | Safety input status | PNU 20992（5200h） | 参考訳 |
| エラー番号 | Error code | PNU 24639（603Fh） | 原本併記 |
| 出力周波数（r/min） | vl velocity demand | PNU 24643（6043h） | 原本併記 |
| 運転速度（r/min） | vl velocity actual value | PNU 24644（6044h） | 原本併記 |
| 制御モード | Modes of operation | PNU 24672（6060h） | 原本併記 |
| 位置指令 | Position demand value | PNU 24674（6062h） | 原本併記 |
| 現在位置 | Position actual value | PNU 24676（6064h） | 原本併記 |
| トルク要求値 | Torque demand | PNU 24692（6074h） | 原本併記 |
| 目標位置 | Target position | PNU 24698（607Ah） | 原本併記 |
| 加速時定数 | Profile acceleration | PNU 24707（6083h） | 原本併記 |
| 減速時定数 | Profile deceleration | PNU 24708（6084h） | 原本併記 |
| PLG 分解能 | Position encoder resolution | PNU 24719（608Fh） | 原本併記 |
| ギア比 | Gear ratio | PNU 24721（6091h） | 原本併記 |
| 原点復帰方法 | Homing method | PNU 24728（6098h） | 原本併記 |
| 原点復帰速度 | Homing speeds | PNU 24729（6099h） | 原本併記 |
| 溜りパルス | Following error actual value | PNU 24820（60F4h） | 原本併記 |
| ダイレクトコマンドモード | Direct command mode | - | 参考訳 |
| 電子ギア | Electronic gear | Pr.420 / Pr.421 | 参考訳 |
| 押当て式 | Stopper type | - | 参考訳 |
| ドグ式 | Dog type | - | 参考訳 |
| リクエスト ID | Request ID | - | 参考訳 |
| エレメント数 | Number of elements | - | 参考訳 |
| パラメータ要求フォーマット | Parameter request format | PROFIdrive | 参考訳 |
| パラメータ応答フォーマット | Parameter response format | PROFIdrive | 参考訳 |
| 設定周波数 | Speed setpoint A | NSOLL_A | 原本併記 |

## 変換範囲表 (2.12 / 原本 p.171-194)

| 原本ページ | 節 | 扱い |
|---|---|---|
| p.171-194 | 2.12 PROFINET | 全文 |
| 上記以外 | 他章 | 同フォルダの他ファイル参照（前付け p.1-6 表紙・目次は未変換） |

## 目次 (2.12)

- [2.12 PROFINET (2.12 / 印刷 p.170 / 原本 p.171)](#212-profinet-212--印刷-p170--原本-p171)
  - [2.12.1 概要 (2.12.1 / 印刷 p.170 / 原本 p.171)](#2121-概要-2121--印刷-p170--原本-p171)
  - [2.12.2 PROFINET 構成 (2.12.2 / 印刷 p.172 / 原本 p.173)](#2122-profinet-構成-2122--印刷-p172--原本-p173)
  - [2.12.3 PROFINET の初期設定 (2.12.3 / 印刷 p.172 / 原本 p.173)](#2123-profinet-の初期設定-2123--印刷-p172--原本-p173)
  - [2.12.4 PROFINET 関連パラメータ (2.12.4 / 印刷 p.173 / 原本 p.174)](#2124-profinet-関連パラメータ-2124--印刷-p173--原本-p174)
  - [2.12.5 Data Exchange (2.12.5 / 印刷 p.174 / 原本 p.175)](#2125-data-exchange-2125--印刷-p174--原本-p175)

---

### 2.12 PROFINET (2.12 / 印刷 p.170 / 原本 p.171)

#### 2.12.1 概要 (2.12.1 / 印刷 p.170 / 原本 p.171)

【図】PROFINET ロゴ (原本 p.171)
- 「PROFI NET」の登録商標ロゴ（®付き）

PROFINET は、FR-E800-(SC)EPB、FR-E806-SCEPB で使用可能です。
インバータの Ethernet コネクタ経由で PROFINET による通信運転を行うと、マスタとインバータ間でパラメータ、指令データ、フィードバックデータの送受信を行います。
インバータの製造時期によって対応していない機能があります。仕様変更の内容については 318 ページを参照してください。

##### ◆ 通信仕様 (2.12.1 / 原本 p.171)

通信仕様はマスタの仕様により変わります。

| 項目 | 内容 |
|---|---|
| 種別 | 100BASE-TX |
| 通信速度 | 100Mbps（10Mbps では使用できません） |
| 最大分岐数 | 同一 Ethernet 上であれば、上限なし |
| カスケード接続段数 | 最大 2 段 |
| 接続ケーブル | Ethernet ケーブル（IEEE802.3 100BASE-TX 規定ケーブル、ANSI/TIA/EIA-568-B（Category 5e）準拠の 4 ペア平衡型シールドケーブル） |
| トポロジ | ライン、スター、ライン・スター混在 |
| PROFINET 通信仕様 | PROFINET IO Device V2.35 |

##### ◆ 配線方法 (2.12.1 / 原本 p.171)

- スター接続で 1 つのコネクタのみを使用する場合は、PORT1 コネクタに接続してください。
- ライン接続で 2 つのコネクタを使用する場合は、PORT1 コネクタをマスタ側、PORT2 コネクタを次の通信用コネクタ（PORT1）に接続してください。

【図】PORT2-PORT1の接続 / IP67仕様品のコネクタ位置 (原本 p.171)
- 左図「PORT2-PORT1の接続」: インバータ2台を並べた図。各インバータに「通信用コネクタ（PORT1）」「通信用コネクタ（PORT2）」が左右に並ぶ。
- 1台目の PORT1 から出たケーブルは「マスタ局に接続」。
- 1台目の PORT2 から出たケーブルが 2台目の PORT1 に接続される（ケーブル途中に省略の波線）。
- 2台目の PORT2 から出たケーブルは「次の通信用コネクタ（PORT1）に接続」。
- 右図「IP67仕様品」: 丸形コネクタが2個あり、左が「EP1 通信用コネクタ（PORT1）」、右が「EP2 通信用コネクタ（PORT2）」（矢印で指示）。

##### ◆ 運転状態モニタ用 LED (2.12.1 / 原本 p.172)

| LED 名称 | 内容 | LED 状態 | 備考 |
|---|---|---|---|
| NS | 通信状態 | 消灯 | 電源 OFF/ インバータリセット中 |
| NS | 通信状態 | 緑点滅 | マスタとの接続未確立 /<br>マスタとの接続確立済み（マスタが STOP 状態） |
| NS | 通信状態 | 緑点灯 | マスタとの接続確立済み（マスタが RUN 状態） |
| MS | インバータ状態 | 消灯 | 電源 OFF/ インバータリセット中 |
| MS | インバータ状態 | 緑点灯 | 正常動作中 |
| MS | インバータ状態 | 赤点灯 | 重故障検出 |
| LINK1 | 通信用コネクタ (PORT1) 状態 | 消灯 | 電源 OFF/ リンクダウン |
| LINK1 | 通信用コネクタ (PORT1) 状態 | 緑点滅 | リンクアップ（データ受信中） |
| LINK1 | 通信用コネクタ (PORT1) 状態 | 緑点灯 | リンクアップ |
| LINK2 | 通信用コネクタ (PORT2) 状態 | 消灯 | 電源 OFF/ リンクダウン |
| LINK2 | 通信用コネクタ (PORT2) 状態 | 緑点滅 | リンクアップ（データ受信中） |
| LINK2 | 通信用コネクタ (PORT2) 状態 | 緑点灯 | リンクアップ |

> **NOTE**
> - マスタが STOP 状態のときにインバータに送信するパケットによっては、NS LED が緑点滅しない場合があります。マスタからインバータに送信するパケットの IOCS により RUN/STOP を判断します（Good（80h）：RUN、Bad（60h）：STOP）。STOP 状態による動作は、下記のマスタで対応します。
>
> | メーカ名 | 形名 | バージョン |
> |---|---|---|
> | SIEMENS | SIMATIC S7-1500 | CPU：1511F-1 PN<br>製品番号：6ES7511-1FK02-0AB0<br>F/W Ver：V 02.05.02 |

##### ◆ GSDML ファイルについて (2.12.1 / 原本 p.172)

GSDML ファイルがインターネットよりダウンロードできます。

| 機種 | 通信種別 | GSDML ファイル |
|---|---|---|
| Ethernet 仕様品 | PROFINET | GSDML-V2.35-MitsubishiElectric-FR-E800-E-[yyyymmdd].xml |
| 安全通信仕様品<br>IP67 仕様品 | PROFINET*1<br>PROFINET + PROFIsafe | GSDML-V2.35-MitsubishiElectric-FR-E800-SCE-[yyyymmdd].xml |

（[yyyymmdd]：更新年月日）

\*1 更新年月日が 20221014 以降から対応します。

三菱電機 FA サイト
https://www.MitsubishiElectric.co.jp/fa/products/drv/inv/support/e800/network.html
より無料でダウンロードできます。詳しくはお買い上げ店または当社営業所までご連絡ください。

> **NOTE**
> - GSDML ファイルはエンジニアリングツールを使用することを前提としております。GSDML ファイルの適切なインストール方法についてはエンジニアリングツールの取扱説明書を参照してください。
> - 安全通信仕様品、IP67 仕様品で PROFINET のみを使用する場合は、PROFIsafe Telegram が設定されているとエラーとなります。PROFIsafe Telegram の設定を削除し、安全パラメータ **Pr.S002 安全通信機能選択**を “0（初期値）”（安全通信機能無効）に設定してください。

#### 2.12.2 PROFINET 構成 (2.12.2 / 印刷 p.172 / 原本 p.173)

##### ◆ 操作手順例 (2.12.2 / 原本 p.173)

使用するマスタ、エンジニアリングツールにより手順が異なります。詳細はマスタ、エンジニアリングツールの取扱説明書を参照してください。

###### ■ 通信を行う前に (2.12.2 / 原本 p.173)

1. 各ユニットを Ethernet ケーブルで接続します。（16 ページ参照）
2. **Pr.1427 ～ Pr.1430 Ethernet 機能選択 1 ～ 4** のいずれかを “34962”（PROFINET）に設定します。（172 ページ参照）
   （例：**Pr.1429** ＝ “45238”（CC-Link IE TSN）（初期値）→ “34962”（PROFINET））
   初期状態の場合、**Pr.1429** を “45238”（CC-Link IE TSN）から “34962”（PROFINET）に変更してください。**Pr.1427 ～ Pr.1430** のいずれかに “45238” が設定されていると CC-Link IE TSN が優先され、PROFINET は無効となります。
3. インバータリセットまたは電源再投入します。

###### ■ ネットワーク構成 (2.12.2 / 原本 p.173)

1. ダウンロードした GSDML ファイルをエンジニアリングツールに追加します。
2. エンジニアリングツールからネットワーク上のインバータを検出します。
3. 検出したインバータをネットワーク構成設定に追加します。
4. インバータのモジュール設定を行います。
   複数台のインバータを接続する場合は、個別のデバイス名を設定します。

###### ■ 通信の確認 (2.12.2 / 原本 p.173)

シーケンサとインバータとの通信が確立すると、インバータの LED 表示は下記のようになります。

| NS | MS | LINK1 | LINK2 |
|---|---|---|---|
| 緑点灯 | 緑点灯 | 緑点滅 \*1 | 緑点滅 \*1 |

（注: 原本では LINK1・LINK2 の欄が結合セルで「緑点滅 \*1」）

\*1 LINK1、LINK2 のどちらか接続しているポートの LED が点滅します。

#### 2.12.3 PROFINET の初期設定 (2.12.3 / 印刷 p.172 / 原本 p.173)

インバータと各種機器を Ethernet 通信で接続するために必要な設定を行います。
各種機器とインバータを通信させるためには、通信する機器の通信仕様にあわせてインバータ側のパラメータを初期設定する必要があります。初期設定がされていなかったり、設定不良があったりすると、データ通信ができません。

| Pr. | 名称 | 初期値 | 設定範囲 | 内容 |
|---|---|---|---|---|
| 1427<br>N630\*1 | Ethernet 機能選択 1 | 5001 | 502、5000 ～ 5002、5006 ～ 5008、5010 ～ 5013、9999、34962、45237、45238、61450 | 使用するアプリケーションやプロトコルなどを設定します。 |
| 1428<br>N631\*1 | Ethernet 機能選択 2 | 45237 | 502、5000 ～ 5002、5006 ～ 5008、5010 ～ 5013、9999、34962、45237、45238、61450 | 使用するアプリケーションやプロトコルなどを設定します。 |
| 1429<br>N632\*1 | Ethernet 機能選択 3 | 45238 | 502、5000 ～ 5002、5006 ～ 5008、5010 ～ 5013、9999、34962、45237、45238、61450 | 使用するアプリケーションやプロトコルなどを設定します。 |
| 1430<br>N633\*1 | Ethernet 機能選択 4 | 9999 | 502、5000 ～ 5002、5006 ～ 5008、5010 ～ 5013、9999、34962、45237、45238、61450 | 使用するアプリケーションやプロトコルなどを設定します。 |
| 1426<br>N641\*1 | リンク速度とデュプレックス | 0 | 0 ～ 4 | 通信速度と全／半二重方式を設定します。 |

\*1 インバータリセット後、または次回電源 ON 時に設定値が反映されます。

> **NOTE**
> - PROFINET では、IP フィルタ機能（Ethernet）（**Pr.1442 ～ Pr.1448**）の設定は無効です。

##### ◆ PROFINET 使用時の注意事項 (2.12.3 / 原本 p.174)

- PROFINET では、Ethernet 操作権指定 IP アドレス（**Pr.1449 ～ Pr.1454**）を使用しないため、初期値から変更しないでください。Ethernet 操作権指定 IP アドレスが設定されていると、Ethernet 通信異常（E.EHR）が発生する場合があります。その場合は、Ethernet 操作権指定 IP アドレスを初期値に変更するか、**Pr.1432 Ethernet 通信チェック時間間隔**の設定を “9999” にしてください。
- エンジニアリングツール上のデバイス設定（IP アドレス、サブネットマスク、デフォルトゲートウェイアドレス）と、接続するインバータのデバイス設定が一致しない場合、マスタの DCP Temporary 機能によって **Pr.442 ～ Pr.445、Pr.1434 ～ Pr.1441**（EEPROM）に “0” が書き込まれます。

##### ◆ Ethernet 機能選択（Pr.1427 ～ Pr.1430） (2.12.3 / 原本 p.174)

PROFINET をアプリケーションとして使用するためには、**Pr.1427 ～ Pr.1430 Ethernet 機能選択 1 ～ 4** のいずれかを “34962”（PROFINET）に設定してください。初期状態の場合、**Pr.1429** を “45238”（CC-Link IE TSN）から “34962”（PROFINET）に変更してください。**Pr.1427 ～ Pr.1430** のいずれかに “45238” が設定されていると CC-Link IE TSN が優先され、PROFINET は無効となります。

> **NOTE**
> - 同時に使用できない通信プロトコルが選択されている場合は、設定値を変更してください。（7 ページ、225 ページ参照）

##### ◆ 通信速度と全／半二重方式の選択（Pr.1426） (2.12.3 / 原本 p.174)

通信速度と全／半二重方式を **Pr.1426 リンク速度とデュプレックス**で設定します。初期設定（**Pr.1426** ＝ “0”）で正しく動作しない場合は、接続する機器の仕様にあわせて **Pr.1426** を設定してください。

| Pr.1426 設定値 | 通信速度 | 全／半二重方式 | 備考 |
|---|---|---|---|
| 0（初期値） | 自動交渉 | 自動交渉 | 通信速度と通信モード（半二重／全二重）を折衝し、最適なものに自動設定します。<br>自動交渉選択の場合は、マスタ局も自動交渉に設定する必要があります。 |
| 1 | 100Mbps | 全二重 | ― |
| 2 | 100Mbps | 半二重 | ― |
| 3 | 10Mbps | 全二重 | 通信速度は 100Mbps 固定です。10Mbps に設定しないでください。 |
| 4 | 10Mbps | 半二重 | 通信速度は 100Mbps 固定です。10Mbps に設定しないでください。 |

#### 2.12.4 PROFINET 関連パラメータ (2.12.4 / 印刷 p.173 / 原本 p.174)

PROFINET で通信を行う場合に関係するパラメータです。必要に応じて設定を行ってください。

| Pr. | 名称 | 初期値 | 設定範囲 | 内容 |
|---|---|---|---|---|
| 1320 ～ 1329<br>N810 ～ N819\*1 | 周期通信入力データ選択 1 ～ 10 | 9999 | 5、100、12288 ～ 13787、20488、20489、24672、24689、24698、24703、24705、24707、24708、24719、24721、24728 ～ 24730 | Telegram 102 の Setpoint Telegram（マスタ→インバータ）に機能を割り付けることができます。 |
| 1320 ～ 1329<br>N810 ～ N819\*1 | 周期通信入力データ選択 1 ～ 10 | 9999 | 9999 | 機能無効 |
| 1330 ～ 1343<br>N850 ～ N863\*1 | 周期通信出力データ選択 1 ～ 14 | 9999 | 6、101、12288 ～ 13787、16384 ～ 16483、20488、20489、20981 ～ 20990、20992\*2、24639、24643、24644、24673 ～ 24676、24692、24695、24820、24826、24828、25858 | Telegram 102 の Actual Value Telegram（インバータ→マスタ）に機能を割り付けることができます。 |
| 1330 ～ 1343<br>N850 ～ N863\*1 | 周期通信出力データ選択 1 ～ 14 | 9999 | 9999 | 機能無効 |
| 1389\*1 | 周期通信入力データ選択サブ 1、2 | 0 | 0 ～ 2、256 ～ 258、512 ～ 514 | **Pr.1389**（下位 8bit）：**Pr.1320** で指定した信号番号のサブインデックス<br>**Pr.1389**（上位 8bit）：**Pr.1321** で指定した信号番号のサブインデックス |
| 1390\*1 | 周期通信入力データ選択サブ 3、4 | 0 | 0 ～ 2、256 ～ 258、512 ～ 514 | **Pr.1390**（下位 8bit）：**Pr.1322** で指定した信号番号のサブインデックス<br>**Pr.1390**（上位 8bit）：**Pr.1323** で指定した信号番号のサブインデックス |
| 1391\*1 | 周期通信入力データ選択サブ 5、6 | 0 | 0 ～ 2、256 ～ 258、512 ～ 514 | **Pr.1391**（下位 8bit）：**Pr.1324** で指定した信号番号のサブインデックス<br>**Pr.1391**（上位 8bit）：**Pr.1325** で指定した信号番号のサブインデックス |
| 1392\*1 | 周期通信入力データ選択サブ 7、8 | 0 | 0 ～ 2、256 ～ 258、512 ～ 514 | **Pr.1392**（下位 8bit）：**Pr.1326** で指定した信号番号のサブインデックス<br>**Pr.1392**（上位 8bit）：**Pr.1327** で指定した信号番号のサブインデックス |
| 1393\*1 | 周期通信入力データ選択サブ 9、10 | 0 | 0 ～ 2、256 ～ 258、512 ～ 514 | **Pr.1393**（下位 8bit）：**Pr.1328** で指定した信号番号のサブインデックス<br>**Pr.1393**（上位 8bit）：**Pr.1329** で指定した信号番号のサブインデックス |
| N830 ～ N839\*1 | 周期通信入力データ選択サブ 1 ～ 10 | 0 | 0 ～ 2 | **Pr.1320 ～ Pr.1329** で指定した信号番号のサブインデックス |
| 1394\*1 | 周期通信出力データ選択サブ 1、2 | 0 | 0 ～ 2、256 ～ 258、512 ～ 514 | **Pr.1394**（下位 8bit）：**Pr.1330** で指定した信号番号のサブインデックス<br>**Pr.1394**（上位 8bit）：**Pr.1331** で指定した信号番号のサブインデックス |
| 1395\*1 | 周期通信出力データ選択サブ 3、4 | 0 | 0 ～ 2、256 ～ 258、512 ～ 514 | **Pr.1395**（下位 8bit）：**Pr.1332** で指定した信号番号のサブインデックス<br>**Pr.1395**（上位 8bit）：**Pr.1333** で指定した信号番号のサブインデックス |
| 1396\*1 | 周期通信出力データ選択サブ 5、6 | 0 | 0 ～ 2、256 ～ 258、512 ～ 514 | **Pr.1396**（下位 8bit）：**Pr.1334** で指定した信号番号のサブインデックス<br>**Pr.1396**（上位 8bit）：**Pr.1335** で指定した信号番号のサブインデックス |
| 1397\*1 | 周期通信出力データ選択サブ 7、8 | 0 | 0 ～ 2、256 ～ 258、512 ～ 514 | **Pr.1397**（下位 8bit）：**Pr.1336** で指定した信号番号のサブインデックス<br>**Pr.1397**（上位 8bit）：**Pr.1337** で指定した信号番号のサブインデックス |
| 1398\*1 | 周期通信出力データ選択サブ 9、10 | 0 | 0 ～ 2、256 ～ 258、512 ～ 514 | **Pr.1398**（下位 8bit）：**Pr.1338** で指定した信号番号のサブインデックス<br>**Pr.1398**（上位 8bit）：**Pr.1339** で指定した信号番号のサブインデックス |
| N870 ～ N879\*1 | 周期通信出力データ選択サブ 1 ～ 10 | 0 | 0 ～ 2 | **Pr.1330 ～ Pr.1339** で指定した信号番号のサブインデックス |

\*1 インバータリセット後、または次回電源 ON 時に設定値が反映されます。
\*2 Ethernet 仕様品のみ設定可能です。

（注: 原本ではこの表は原本 p.174〜p.175 にまたがる。）

#### 2.12.5 Data Exchange (2.12.5 / 印刷 p.174 / 原本 p.175)

##### ◆ Process Data (Cyclic Data Exchange) (2.12.5 / 原本 p.175)

マスタとインバータ間で一定周期でマスタからの指令データ、インバータからのフィードバックデータの送受信を行います。

###### ■ テレグラムの種類 (2.12.5 / 原本 p.175)

制御モードに合わせて使用するテレグラムを選択します。Telegram 102 は、通信データを任意に選択することができます。

| Telegram | Description | Size (words) |
|---|---|---|
| 1 | Standard Telegram 1 (Speed control) | 2 |
| 100 | Telegram 100 (Torque control) | 3 |
| 102 | Telegram 102 (Custom) | Setpoint Telegram：21<br>Actual Value Telegram：29 |

使用されているテレグラムの種類は、PROFIdrive パラメータ P922 で読出し可能です。

> **NOTE**
> - テレグラムモジュールは 2 種類同時に使用できません。

###### ■ データマッピング (2.12.5 / 原本 p.176)

- Standard Telegram 1

| 種類 | IO Data number | 名称 | 略称 | データ長 (Bit) |
|---|---|---|---|---|
| Setpoint Telegram（マスタ→インバータ） | 1 | Control word 1 | STW1 | 16 |
| Setpoint Telegram（マスタ→インバータ） | 2 | Speed setpoint A | NSOLL_A | 16 |
| Actual Value Telegram（インバータ→マスタ） | 1 | Status word 1 | ZSW1 | 16 |
| Actual Value Telegram（インバータ→マスタ） | 2 | Speed actual value A | NIST_A | 16 |

- Telegram 100

| 種類 | IO Data number | 名称 | 略称 | データ長 (Bit) |
|---|---|---|---|---|
| Setpoint Telegram（マスタ→インバータ） | 1 | Control word 1 | STW1 | 16 |
| Setpoint Telegram（マスタ→インバータ） | 2 | Target torque | - | 16 |
| Setpoint Telegram（マスタ→インバータ） | 3 | Speed setpoint A | NSOLL_A | 16 |
| Actual Value Telegram（インバータ→マスタ） | 1 | Status word 1 | ZSW1 | 16 |
| Actual Value Telegram（インバータ→マスタ） | 2 | Actual torque | - | 16 |
| Actual Value Telegram（インバータ→マスタ） | 3 | Speed actual value A | NIST_A | 16 |

- Telegram 102

（注: 原本では「備考」欄は IO Data number 2〜11（Setpoint）/ 2〜15（Actual Value）でそれぞれ1つの結合セル。各行に展開。Actual Value の IO Data number 12〜15 の「Sub index 指定」も結合セル「0 固定」。）

| 種類 | IO Data number | 名称 | Sub index 指定 | データ長 (Bit) | 備考 |
|---|---|---|---|---|---|
| Setpoint Telegram（マスタ→インバータ） | 1 | Control word 1 (STW1) | - | 16 | 固定 |
| Setpoint Telegram（マスタ→インバータ） | 2 | **Pr.1320** | **Pr.1389**（下位 8bit） | 32 | 下記の信号番号が選択可能です。<br>5：Speed setpoint A (NSOLL_A)（177 ページ参照）<br>100：Target torque（178 ページ参照）<br>12288 ～ 13787：Inverter Parameters（183 ページ参照）<br>20488、20489：Inverter Control Parameters（184 ページ参照）<br>24672、24689、24698、24703、24705、24707、24708、24719、24721、24728 ～ 24730：CiA402 Drive Profile（186 ページ参照）<br>データ長が 16bit の信号を選択した場合、下位 16bit に設定した値のみ有効となります。 |
| Setpoint Telegram（マスタ→インバータ） | 3 | **Pr.1321** | **Pr.1389**（上位 8bit） | 32 | 下記の信号番号が選択可能です。<br>5：Speed setpoint A (NSOLL_A)（177 ページ参照）<br>100：Target torque（178 ページ参照）<br>12288 ～ 13787：Inverter Parameters（183 ページ参照）<br>20488、20489：Inverter Control Parameters（184 ページ参照）<br>24672、24689、24698、24703、24705、24707、24708、24719、24721、24728 ～ 24730：CiA402 Drive Profile（186 ページ参照）<br>データ長が 16bit の信号を選択した場合、下位 16bit に設定した値のみ有効となります。 |
| Setpoint Telegram（マスタ→インバータ） | 4 | **Pr.1322** | **Pr.1390**（下位 8bit） | 32 | 下記の信号番号が選択可能です。<br>5：Speed setpoint A (NSOLL_A)（177 ページ参照）<br>100：Target torque（178 ページ参照）<br>12288 ～ 13787：Inverter Parameters（183 ページ参照）<br>20488、20489：Inverter Control Parameters（184 ページ参照）<br>24672、24689、24698、24703、24705、24707、24708、24719、24721、24728 ～ 24730：CiA402 Drive Profile（186 ページ参照）<br>データ長が 16bit の信号を選択した場合、下位 16bit に設定した値のみ有効となります。 |
| Setpoint Telegram（マスタ→インバータ） | 5 | **Pr.1323** | **Pr.1390**（上位 8bit） | 32 | 下記の信号番号が選択可能です。<br>5：Speed setpoint A (NSOLL_A)（177 ページ参照）<br>100：Target torque（178 ページ参照）<br>12288 ～ 13787：Inverter Parameters（183 ページ参照）<br>20488、20489：Inverter Control Parameters（184 ページ参照）<br>24672、24689、24698、24703、24705、24707、24708、24719、24721、24728 ～ 24730：CiA402 Drive Profile（186 ページ参照）<br>データ長が 16bit の信号を選択した場合、下位 16bit に設定した値のみ有効となります。 |
| Setpoint Telegram（マスタ→インバータ） | 6 | **Pr.1324** | **Pr.1391**（下位 8bit） | 32 | 下記の信号番号が選択可能です。<br>5：Speed setpoint A (NSOLL_A)（177 ページ参照）<br>100：Target torque（178 ページ参照）<br>12288 ～ 13787：Inverter Parameters（183 ページ参照）<br>20488、20489：Inverter Control Parameters（184 ページ参照）<br>24672、24689、24698、24703、24705、24707、24708、24719、24721、24728 ～ 24730：CiA402 Drive Profile（186 ページ参照）<br>データ長が 16bit の信号を選択した場合、下位 16bit に設定した値のみ有効となります。 |
| Setpoint Telegram（マスタ→インバータ） | 7 | **Pr.1325** | **Pr.1391**（上位 8bit） | 32 | 下記の信号番号が選択可能です。<br>5：Speed setpoint A (NSOLL_A)（177 ページ参照）<br>100：Target torque（178 ページ参照）<br>12288 ～ 13787：Inverter Parameters（183 ページ参照）<br>20488、20489：Inverter Control Parameters（184 ページ参照）<br>24672、24689、24698、24703、24705、24707、24708、24719、24721、24728 ～ 24730：CiA402 Drive Profile（186 ページ参照）<br>データ長が 16bit の信号を選択した場合、下位 16bit に設定した値のみ有効となります。 |
| Setpoint Telegram（マスタ→インバータ） | 8 | **Pr.1326** | **Pr.1392**（下位 8bit） | 32 | 下記の信号番号が選択可能です。<br>5：Speed setpoint A (NSOLL_A)（177 ページ参照）<br>100：Target torque（178 ページ参照）<br>12288 ～ 13787：Inverter Parameters（183 ページ参照）<br>20488、20489：Inverter Control Parameters（184 ページ参照）<br>24672、24689、24698、24703、24705、24707、24708、24719、24721、24728 ～ 24730：CiA402 Drive Profile（186 ページ参照）<br>データ長が 16bit の信号を選択した場合、下位 16bit に設定した値のみ有効となります。 |
| Setpoint Telegram（マスタ→インバータ） | 9 | **Pr.1327** | **Pr.1392**（上位 8bit） | 32 | 下記の信号番号が選択可能です。<br>5：Speed setpoint A (NSOLL_A)（177 ページ参照）<br>100：Target torque（178 ページ参照）<br>12288 ～ 13787：Inverter Parameters（183 ページ参照）<br>20488、20489：Inverter Control Parameters（184 ページ参照）<br>24672、24689、24698、24703、24705、24707、24708、24719、24721、24728 ～ 24730：CiA402 Drive Profile（186 ページ参照）<br>データ長が 16bit の信号を選択した場合、下位 16bit に設定した値のみ有効となります。 |
| Setpoint Telegram（マスタ→インバータ） | 10 | **Pr.1328** | **Pr.1393**（下位 8bit） | 32 | 下記の信号番号が選択可能です。<br>5：Speed setpoint A (NSOLL_A)（177 ページ参照）<br>100：Target torque（178 ページ参照）<br>12288 ～ 13787：Inverter Parameters（183 ページ参照）<br>20488、20489：Inverter Control Parameters（184 ページ参照）<br>24672、24689、24698、24703、24705、24707、24708、24719、24721、24728 ～ 24730：CiA402 Drive Profile（186 ページ参照）<br>データ長が 16bit の信号を選択した場合、下位 16bit に設定した値のみ有効となります。 |
| Setpoint Telegram（マスタ→インバータ） | 11 | **Pr.1329** | **Pr.1393**（上位 8bit） | 32 | 下記の信号番号が選択可能です。<br>5：Speed setpoint A (NSOLL_A)（177 ページ参照）<br>100：Target torque（178 ページ参照）<br>12288 ～ 13787：Inverter Parameters（183 ページ参照）<br>20488、20489：Inverter Control Parameters（184 ページ参照）<br>24672、24689、24698、24703、24705、24707、24708、24719、24721、24728 ～ 24730：CiA402 Drive Profile（186 ページ参照）<br>データ長が 16bit の信号を選択した場合、下位 16bit に設定した値のみ有効となります。 |
| Actual Value Telegram（インバータ→マスタ） | 1 | Status word 1 (ZSW1) | - | 16 | 固定 |
| Actual Value Telegram（インバータ→マスタ） | 2 | **Pr.1330** | **Pr.1394**（下位 8bit） | 32 | 下記の信号番号が選択可能です。<br>6：Speed actual value A (NIST_A)（177 ページ参照）<br>101：Actual torque（178 ページ参照）<br>12288 ～ 13787：Inverter Parameters（183 ページ参照）<br>16384 ～ 16483：Monitor Data（184 ページ参照）<br>20488、20489、20981 ～ 20990、20992：Inverter Control Parameters（184 ページ参照）<br>24639、24643、24644、24673 ～ 24676、24692、24695、24820、24826、24828、25858：CiA402 Drive Profile（186 ページ参照）<br>20992 は Ethernet 仕様品のみ選択可能です。 |
| Actual Value Telegram（インバータ→マスタ） | 3 | **Pr.1331** | **Pr.1394**（上位 8bit） | 32 | 下記の信号番号が選択可能です。<br>6：Speed actual value A (NIST_A)（177 ページ参照）<br>101：Actual torque（178 ページ参照）<br>12288 ～ 13787：Inverter Parameters（183 ページ参照）<br>16384 ～ 16483：Monitor Data（184 ページ参照）<br>20488、20489、20981 ～ 20990、20992：Inverter Control Parameters（184 ページ参照）<br>24639、24643、24644、24673 ～ 24676、24692、24695、24820、24826、24828、25858：CiA402 Drive Profile（186 ページ参照）<br>20992 は Ethernet 仕様品のみ選択可能です。 |
| Actual Value Telegram（インバータ→マスタ） | 4 | **Pr.1332** | **Pr.1395**（下位 8bit） | 32 | 下記の信号番号が選択可能です。<br>6：Speed actual value A (NIST_A)（177 ページ参照）<br>101：Actual torque（178 ページ参照）<br>12288 ～ 13787：Inverter Parameters（183 ページ参照）<br>16384 ～ 16483：Monitor Data（184 ページ参照）<br>20488、20489、20981 ～ 20990、20992：Inverter Control Parameters（184 ページ参照）<br>24639、24643、24644、24673 ～ 24676、24692、24695、24820、24826、24828、25858：CiA402 Drive Profile（186 ページ参照）<br>20992 は Ethernet 仕様品のみ選択可能です。 |
| Actual Value Telegram（インバータ→マスタ） | 5 | **Pr.1333** | **Pr.1395**（上位 8bit） | 32 | 下記の信号番号が選択可能です。<br>6：Speed actual value A (NIST_A)（177 ページ参照）<br>101：Actual torque（178 ページ参照）<br>12288 ～ 13787：Inverter Parameters（183 ページ参照）<br>16384 ～ 16483：Monitor Data（184 ページ参照）<br>20488、20489、20981 ～ 20990、20992：Inverter Control Parameters（184 ページ参照）<br>24639、24643、24644、24673 ～ 24676、24692、24695、24820、24826、24828、25858：CiA402 Drive Profile（186 ページ参照）<br>20992 は Ethernet 仕様品のみ選択可能です。 |
| Actual Value Telegram（インバータ→マスタ） | 6 | **Pr.1334** | **Pr.1396**（下位 8bit） | 32 | 下記の信号番号が選択可能です。<br>6：Speed actual value A (NIST_A)（177 ページ参照）<br>101：Actual torque（178 ページ参照）<br>12288 ～ 13787：Inverter Parameters（183 ページ参照）<br>16384 ～ 16483：Monitor Data（184 ページ参照）<br>20488、20489、20981 ～ 20990、20992：Inverter Control Parameters（184 ページ参照）<br>24639、24643、24644、24673 ～ 24676、24692、24695、24820、24826、24828、25858：CiA402 Drive Profile（186 ページ参照）<br>20992 は Ethernet 仕様品のみ選択可能です。 |
| Actual Value Telegram（インバータ→マスタ） | 7 | **Pr.1335** | **Pr.1396**（上位 8bit） | 32 | 下記の信号番号が選択可能です。<br>6：Speed actual value A (NIST_A)（177 ページ参照）<br>101：Actual torque（178 ページ参照）<br>12288 ～ 13787：Inverter Parameters（183 ページ参照）<br>16384 ～ 16483：Monitor Data（184 ページ参照）<br>20488、20489、20981 ～ 20990、20992：Inverter Control Parameters（184 ページ参照）<br>24639、24643、24644、24673 ～ 24676、24692、24695、24820、24826、24828、25858：CiA402 Drive Profile（186 ページ参照）<br>20992 は Ethernet 仕様品のみ選択可能です。 |
| Actual Value Telegram（インバータ→マスタ） | 8 | **Pr.1336** | **Pr.1397**（下位 8bit） | 32 | 下記の信号番号が選択可能です。<br>6：Speed actual value A (NIST_A)（177 ページ参照）<br>101：Actual torque（178 ページ参照）<br>12288 ～ 13787：Inverter Parameters（183 ページ参照）<br>16384 ～ 16483：Monitor Data（184 ページ参照）<br>20488、20489、20981 ～ 20990、20992：Inverter Control Parameters（184 ページ参照）<br>24639、24643、24644、24673 ～ 24676、24692、24695、24820、24826、24828、25858：CiA402 Drive Profile（186 ページ参照）<br>20992 は Ethernet 仕様品のみ選択可能です。 |
| Actual Value Telegram（インバータ→マスタ） | 9 | **Pr.1337** | **Pr.1397**（上位 8bit） | 32 | 下記の信号番号が選択可能です。<br>6：Speed actual value A (NIST_A)（177 ページ参照）<br>101：Actual torque（178 ページ参照）<br>12288 ～ 13787：Inverter Parameters（183 ページ参照）<br>16384 ～ 16483：Monitor Data（184 ページ参照）<br>20488、20489、20981 ～ 20990、20992：Inverter Control Parameters（184 ページ参照）<br>24639、24643、24644、24673 ～ 24676、24692、24695、24820、24826、24828、25858：CiA402 Drive Profile（186 ページ参照）<br>20992 は Ethernet 仕様品のみ選択可能です。 |
| Actual Value Telegram（インバータ→マスタ） | 10 | **Pr.1338** | **Pr.1398**（下位 8bit） | 32 | 下記の信号番号が選択可能です。<br>6：Speed actual value A (NIST_A)（177 ページ参照）<br>101：Actual torque（178 ページ参照）<br>12288 ～ 13787：Inverter Parameters（183 ページ参照）<br>16384 ～ 16483：Monitor Data（184 ページ参照）<br>20488、20489、20981 ～ 20990、20992：Inverter Control Parameters（184 ページ参照）<br>24639、24643、24644、24673 ～ 24676、24692、24695、24820、24826、24828、25858：CiA402 Drive Profile（186 ページ参照）<br>20992 は Ethernet 仕様品のみ選択可能です。 |
| Actual Value Telegram（インバータ→マスタ） | 11 | **Pr.1339** | **Pr.1398**（上位 8bit） | 32 | 下記の信号番号が選択可能です。<br>6：Speed actual value A (NIST_A)（177 ページ参照）<br>101：Actual torque（178 ページ参照）<br>12288 ～ 13787：Inverter Parameters（183 ページ参照）<br>16384 ～ 16483：Monitor Data（184 ページ参照）<br>20488、20489、20981 ～ 20990、20992：Inverter Control Parameters（184 ページ参照）<br>24639、24643、24644、24673 ～ 24676、24692、24695、24820、24826、24828、25858：CiA402 Drive Profile（186 ページ参照）<br>20992 は Ethernet 仕様品のみ選択可能です。 |
| Actual Value Telegram（インバータ→マスタ） | 12 | **Pr.1340** | 0 固定 | 32 | 下記の信号番号が選択可能です。<br>6：Speed actual value A (NIST_A)（177 ページ参照）<br>101：Actual torque（178 ページ参照）<br>12288 ～ 13787：Inverter Parameters（183 ページ参照）<br>16384 ～ 16483：Monitor Data（184 ページ参照）<br>20488、20489、20981 ～ 20990、20992：Inverter Control Parameters（184 ページ参照）<br>24639、24643、24644、24673 ～ 24676、24692、24695、24820、24826、24828、25858：CiA402 Drive Profile（186 ページ参照）<br>20992 は Ethernet 仕様品のみ選択可能です。 |
| Actual Value Telegram（インバータ→マスタ） | 13 | **Pr.1341** | 0 固定 | 32 | 下記の信号番号が選択可能です。<br>6：Speed actual value A (NIST_A)（177 ページ参照）<br>101：Actual torque（178 ページ参照）<br>12288 ～ 13787：Inverter Parameters（183 ページ参照）<br>16384 ～ 16483：Monitor Data（184 ページ参照）<br>20488、20489、20981 ～ 20990、20992：Inverter Control Parameters（184 ページ参照）<br>24639、24643、24644、24673 ～ 24676、24692、24695、24820、24826、24828、25858：CiA402 Drive Profile（186 ページ参照）<br>20992 は Ethernet 仕様品のみ選択可能です。 |
| Actual Value Telegram（インバータ→マスタ） | 14 | **Pr.1342** | 0 固定 | 32 | 下記の信号番号が選択可能です。<br>6：Speed actual value A (NIST_A)（177 ページ参照）<br>101：Actual torque（178 ページ参照）<br>12288 ～ 13787：Inverter Parameters（183 ページ参照）<br>16384 ～ 16483：Monitor Data（184 ページ参照）<br>20488、20489、20981 ～ 20990、20992：Inverter Control Parameters（184 ページ参照）<br>24639、24643、24644、24673 ～ 24676、24692、24695、24820、24826、24828、25858：CiA402 Drive Profile（186 ページ参照）<br>20992 は Ethernet 仕様品のみ選択可能です。 |
| Actual Value Telegram（インバータ→マスタ） | 15 | **Pr.1343** | 0 固定 | 32 | 下記の信号番号が選択可能です。<br>6：Speed actual value A (NIST_A)（177 ページ参照）<br>101：Actual torque（178 ページ参照）<br>12288 ～ 13787：Inverter Parameters（183 ページ参照）<br>16384 ～ 16483：Monitor Data（184 ページ参照）<br>20488、20489、20981 ～ 20990、20992：Inverter Control Parameters（184 ページ参照）<br>24639、24643、24644、24673 ～ 24676、24692、24695、24820、24826、24828、25858：CiA402 Drive Profile（186 ページ参照）<br>20992 は Ethernet 仕様品のみ選択可能です。 |

（注: Setpoint Telegram 部分は原本 p.176、Actual Value Telegram 部分は原本 p.177。）

> **NOTE**
> - **Pr.1320 ～ Pr.1329** に重複した信号番号を指定した場合、パラメータ番号が小さい方に設定した値が有効となり、パラメータ番号が大きい方に設定した値は “9999” として扱われます。
> - **Pr.1320 ～ Pr.1329** に存在しない信号番号を指定した場合、または “9999” を設定した場合、データは書き込まれません。
> - **Pr.1330 ～ Pr.1343** に存在しない信号番号を指定した場合、または “9999” を設定した場合、0 を読み出します。

- Control word 1（STW1）の詳細 (2.12.5 / 原本 p.177〜p.178)

| Bit | 名称 | インバータ動作 |
|---|---|---|
| 0 | ON/OFF | 0：OFF<br>1：ON |
| 1 | 出力遮断<br>No Coast Stop/Coast Stop | 0：出力遮断する<br>1：出力遮断解除 |
| 2 | 緊急停止<br>No Quick Stop/Quick Stop | 0：緊急停止する<br>1：緊急停止解除 |
| 3 | 運転許可<br>Enable/Disable Operation | 0：停止<br>1：運転 |
| 4 | - | 未使用（0 固定） |
| 5 | 加減速中断 \*1<br>Unfreeze/Freeze Ramp Generator | 0：加減速を中断する<br>1：加減速を中断しない<br>速度制御時のみ有効<br>始動指令 OFF となる場合や瞬停再始動中は無効 |
| 6 | 設定周波数有効<br>Enable/Disable Setpoint | 0：NSOLL_A 無効（周波数設定 / 速度制限値＝ 0）<br>1：NSOLL_A 有効 |
| 7 | エラークリア<br>Fault Acknowledge (0 → 1) | bit OFF → ON で 20ms 以上維持：フォルトバッファをクリアする（インバータがアラーム状態の場合は、保護機能をリセットする）\*2 |
| 8 | - | 未使用（0 固定） |
| 9 | - | 未使用（0 固定） |
| 10 | シーケンサからの DOIO データ有効<br>Control By PLC/No Control By PLC | 0：STW1 無効<br>1：STW1 有効 |
| 11 | 設定トルク有効<br>Target torque enabled（Device-specific） | 0：Target Torque 無効（トルク指令値＝ 0）<br>1：Target Torque 有効（トルク指令値＝ Target Torque） |
| 12 | 始動指令方向選択<br>（Device-specific） | 0：NSOLL_A ＞ 0 の場合は正転、NSOLL_A ＜ 0 の場合は逆転<br>1：NSOLL_A ＞ 0 の場合は逆転、NSOLL_A ＜ 0 の場合は正転 |
| 13 | 原点復帰 / 位置決め運転開始<br>（Device-specific） | 0：始動指令 OFF<br>1：始動指令 ON<br>位置制御時かつ状態 S4（179 ページ）で有効 |
| 14、15 | - | 未使用（0 固定） |

\*1 インバータ製造時期によって仕様が異なります。

| 加減速中断時の動作 | SERIAL（製造番号） |
|---|---|
| • 設定周波数更新による中断<br>• NSOLL_A を速度指令とした運転時のみ有効 | □□ 214 〇〇〇〇〇〇以前 |
| • 設定周波数への影響なし<br>• NSOLL_A 以外の速度指令で運転した場合でも有効 | □□ 215 〇〇〇〇〇〇以降 |

\*2 E.SCF、E.GF（**Pr.249** ＝ “2” 設定時）、E.16 ～ E.20、E.PE6、E.PE2、E.CPU、E.CMB、E.1、E.5 ～ E.7、E.13 はリセットされません。この場合は、原因の処置を行ってから、電源再投入またはインバータリセットしてください。

- Status word 1（ZSW1）の詳細 (2.12.5 / 原本 p.178)

| Bit | 名称 | インバータ動作 |
|---|---|---|
| 0 | Ready To Switch On/Not Ready To Switch On | 0：停止中（準備状態）（Ready For Switching On）でない<br>1：停止中（準備状態）（Ready For Switching On）である |
| 1 | Ready To Operate/Not Ready To Operate | 0：停止中（待機状態）（Switched On）でない<br>1：停止中（待機状態）（Switched On）である |
| 2 | Operation Enabled (drive follows setpoint)/<br>Operation Disabled | 0：停止中（Operation Disabled）<br>1：運転中（Operation Enabled） |
| 3 | Fault Present/No Fault | 0：アラームなし<br>1：アラーム発生、Fault numbers（P947）にアラームコード格納済み |
| 4 | 出力停止中<br>Coast Stop Not Activated/Coast Stop Activated (No OFF2/OFF2) | 0：出力遮断中<br>1：出力遮断解除 |
| 5 | 緊急停止中<br>Quick Stop Not Activated/Quick Stop Activated (No OFF3/OFF3) | 0：緊急停止中<br>1：緊急停止解除 |
| 6 | Switching On Inhibited/Switching On Not Inhibited | 0：停止中（初期状態）（Switching On Inhibited）でない<br>1：停止中（初期状態）（Switching On Inhibited）である |
| 7 | Warning Present/No Warning | 0：警報、軽故障なし<br>1：警報、軽故障発生 |
| 8 | - | 未使用（0 固定） |
| 9 | Control Requested/No Control Requested | 0：コントローラ側に操作権・運転指令権なし<br>1：コントローラ側に操作権・運転指令権あり |
| 10 ～ 15 | - | 未使用（0 固定） |

- Speed setpoint A (NSOLL_A)、Speed actual value A (NIST_A) (2.12.5 / 原本 p.178)

設定周波数（速度制限値）の設定、出力周波数のモニタが可能です。インバータの上限周波数（**Pr.1、Pr.18**）を基準に下記計算式で求められます。（有効桁数未満を切り捨て）

設定周波数（速度制限値） (Hz) = (NSOLL_A / 4000h) × インバータの上限周波数（**Pr.1、Pr.18**）
出力周波数 (Hz) = (NIST_A / 4000h) × インバータの上限周波数（**Pr.1、Pr.18**）

| 項目 | 内容 |
|---|---|
| データタイプ | N2 |
| 範囲 \*1\*2 | -32768 (8000h) ～ 32767 (7FFFh)<br>(-200% ～ 199.99%) |
| 基準 | 16384 (4000h) ＝インバータの上限周波数（**Pr.1、Pr.18**） |
| 符号 \*2 | 正：正転<br>負：逆転 |

\*1 計算結果が 590Hz を超える場合は、設定周波数に反映されません。
\*2 **Pr.290** によりモニタ表示のマイナス出力を選択できます。詳細は FR-E800 取扱説明書（機能編）を参照ください。

> **NOTE**
> - Telegram 100、Telegram 102 で Target torque を割り付けた場合、始動指令の方向は STW1 bit12 で選択してください。NSOLL_A への入力は絶対値として扱われます。
> - FR-A800 または FR-F800 に HMS 社製 PROFINET 通信オプション A8NPRT 装着時、**Pr.3 基底周波数**が基準となります。併用する場合は、基準の違いを考慮して設定してください。

###### （続き）■ データマッピング (2.12.5 / 原本 p.179)

- Target torque、Actual torque (2.12.5 / 原本 p.179)

定格トルクを 100% とし、1% 単位で設定、0.1% 単位でモニタが可能です。
Target torque は -400% ～ 400% でクランプされ、**Pr.805**（1000% 基準）（RAM）に設定します。
Actual torque はモータトルク（モニタコード：07h）を読み出します。

> **NOTE**
> - Telegram 102 でトルク指令を使用する場合は、13093（**Pr.805**）ではなく 100（Target torque）を選択してください。

###### ■ 状態遷移 (2.12.5 / 原本 p.180)

【図】PROFINET 状態遷移図 (原本 p.180)

- 状態（ボックス）
  - S1 : Switching On Inhibited（ZSW1 bit 6 = true、bit 0, 1, 2 = false）
  - S2 : Ready For Switching On（ZSW1 bit 0 = true、bit 1, 2, 6 = false）
  - S3 : Switched On（ZSW1 bit 0, 1 = true、bit 2, 6 = false）
  - S4 : Operation（ZSW1 bit 0, 1, 2 = true、bit 6 = false）
  - S5 : Switching Off（ZSW1 bit 0, 1 = true、bit 2, 6 = false）… 破線枠で S5-1 : ramp stop、S5-2 : quick stop、S5-3 : fault stop を囲む
- 遷移（矢印、図中の番号とラベル）
  - (0) Power supply ON → S1
  - (1) S1 → S2：OFF and No Coast Stop and No Quick Stop（STW1 bit 0 = false and bit 1 = true and bit 2 = true）
  - (6) S2 → S1：Coast Stop or Quick Stop（STW1 bit 1 = false or bit 2 = false）
  - (2) S2 → S3：ON（STW1 bit 0 = true）
  - (5) S3 → S2：OFF（STW1 bit 0 = false）
  - (7) S3 → S1：Coast Stop or Quick Stop（STW1 bit 1 = false or bit 2 = false）
  - (3) S3 → S4：Enable Operation（STW1 bit 3 = true）
  - (4) S4 → S3：Disable Operation（STW1 bit 3 = false）
  - (8) S4 → S1：Coast Stop（STW1 bit 1 = false）
  - (9) S4 → S5-1：OFF（STW1 bit 0 = false）
  - (13) S5-1 → S4：ON（STW1 bit 0 = true）
  - (10) S4 → S5-2：Quick Stop（STW1 bit 2 = false）
  - (16) S4 → S5-3（ラベルなし。遷移番号表では「マスタとの Process Data 通信が途絶えた」）
  - (17) S5-3 → S4：ON（STW1 bit 0 = true）
  - (11) S5-1 → S2：Standstill detected or Disable Operation（STW1 bit 3 = false）
  - (12) S5-1 → S5-2：Quick Stop（STW1 bit 2 = false）
  - (18) S5-1 → S5-3（ラベルなし）
  - (19) S5-3 → S5-1：OFF（STW1 bit 0 = false）
  - (20) S5-3 → S5-2（ラベルなし）
  - (14) S5-2 → S1：Standstill detected or Disable Operation（STW1 bit 3 = false）
  - (15) S5（破線枠）→ S1：Coast Stop（STW1 bit 1 = false）
  - （注: 矢印の始点・終点は図の目視による読み取り。(16)(18)(20) は図中にラベル文字なし）

- 状態定義 (2.12.5 / 原本 p.180)

| 記号 | 名称 | 内容 | インバータ動作：位置制御以外 | インバータ動作：位置制御 \*2 |
|---|---|---|---|---|
| S1\*1 | Switching On Inhibited | 停止中（初期状態） | 出力遮断（RY 信号 OFF） | 出力遮断（RY 信号 OFF） |
| S2 | Ready For Switching On | 停止中（準備状態） | 出力遮断（RY 信号 OFF） | 出力遮断（RY 信号 OFF） |
| S3 | Switched On | 停止中（待機状態） | 出力遮断解除（RY 信号 ON）\*3 | 出力遮断解除（RY 信号 ON）\*3 |
| S4\*4 | Operation | 運転中（運転可能状態） | 始動指令 ON（回転方向は STW1、NSOLL_A による） | サーボ ON 状態 |
| S5 | Switching Off | 減速停止中 | - | - |
| S5-1 | ramp stop | 通常の減速停止 | 始動指令 OFF、通常の減速停止 | サーボ OFF 状態<br>始動指令 OFF、出力遮断 |
| S5-2 | quick stop | 緊急停止 | 始動指令 OFF、**Pr.1103**、**Pr.815** の設定で減速停止 \*5 | サーボ OFF 状態<br>始動指令 OFF、出力遮断 |
| S5-3 | fault stop | 通信異常による減速停止 | 通信異常による減速停止（**Pr.502** ＝ “1、2”） | 通信異常による減速停止（**Pr.502** ＝ “1、2”） |

（注: 原本では S1〜S3、S5、S5-3 のインバータ動作欄は「位置制御以外」「位置制御」の2列にまたがる結合セル。各列に展開した）

\*1 下記のいずれかの場合は、強制的に S1 に遷移します。
インバータアラーム発生時
ネットワーク運転モード以外
エマージェンシードライブ商用運転中
インバータ運転中マスタが STOP 状態
\*2 位置制御時は、状態遷移によりサーボ ON/OFF を切り換えます。Inverter Control Parameters (P20488、P20489)（184 ページ）を使用した LX 信号または SON 信号入力は無効です（SON 信号 OFF による出力遮断は有効です）。
\*3 MRS 信号などにより出力遮断している場合、RY 信号は OFF のままとなります。
\*4 エマージェンシードライブ実行中は、強制的に S4 に遷移します。
\*5 **Pr.1103**、**Pr.815** の詳細は取扱説明書（機能編）を参照してください。

- 遷移番号 (2.12.5 / 原本 p.181)

| 記号 | 内容 | 備考 |
|---|---|---|
| (0) | 制御電源 ON | |
| (1) | マスタからの OFF コマンド | 操作権、運転指令権がない場合は遷移しない |
| (2) | マスタからの ON コマンド | |
| (3) | マスタからの Enable operation コマンド | インバータが運転可能状態でない場合は遷移しない |
| (4) | マスタからの Disable operation コマンド | RY 信号が OFF になる場合でも遷移する（サーボ ON 状態は解除、始動指令は OFF になる） |
| (5) | マスタからの OFF コマンド | |
| (6) | マスタからの Coast stop コマンド<br>マスタからの Quick stop コマンド | |
| (7) | マスタからの Coast stop コマンド<br>マスタからの Quick stop コマンド | |
| (8) | マスタからの Coast stop コマンド | |
| (9) | マスタからの OFF コマンド | |
| (10) | マスタからの Quick stop コマンド | |
| (11) | モータ停止<br>マスタからの Disable operation コマンド | |
| (12) | マスタからの Quick stop コマンド | |
| (13) | マスタからの ON コマンド | |
| (14) | モータ停止 | マスタが STOP 状態でも遷移する |
| (15) | マスタからの Coast stop コマンド | |
| (16) | マスタとの Process Data 通信が途絶えた（**Pr.502** ＝ “1、2”） | |
| (17) | マスタとの Process Data 通信が復帰（**Pr.502** ＝ “2”） | |
| (18) | マスタとの Process Data 通信が途絶えた（**Pr.502** ＝ “1、2”） | |
| (19) | マスタとの Process Data 通信が復帰（**Pr.502** ＝ “2”） | |
| (20) | マスタからの Quick stop コマンド（**Pr.502** ＝ “1”） | マスタとの Process Data 通信が復帰していない場合は遷移しない |

> **NOTE**
> - マスタが STOP 状態のときにインバータに送信するパケットによっては、S1 に遷移しない場合があります。マスタからインバータに送信するパケットの IOCS により RUN/STOP を判断します（Good（80h）：RUN、Bad（60h）：STOP）。STOP 状態による動作は、下記のマスタで対応します。
>
> | メーカ名 | 形名 | バージョン |
> |---|---|---|
> | SIEMENS | SIMATIC S7-1500 | CPU：1511F-1 PN<br>製品番号：6ES7511-1FK02-0AB0<br>F/W Ver：V 02.05.02 |

- コマンドと Control word 1（STW1）の組合せ (2.12.5 / 原本 p.181)

| コマンド | STW1 Bit3（Enable Operation） | STW1 Bit2（No Quick Stop） | STW1 Bit1（No Coast Stop） | STW1 Bit0（ON） | 動作 | 遷移番号 |
|---|---|---|---|---|---|---|
| OFF | - | 1 | 1 | 0 | S2 に遷移 | (1) |
| ON | - | 1 | 1 | 1 | S3 に遷移 | (2) |
| Enable operation | 1 | 1 | 1 | 1 | 運転 | (3) |
| Disable operation | 0 | 1 | 1 | 1 | 停止 | (4) |
| Quick stop | - | 0 | - | - | 緊急停止（減速停止） | (6)、(7) |
| Coast stop | - | - | 0 | - | 出力遮断（フリーラン停止） | (6)、(7) |

例）マスタからインバータへ 50Hz 正転の指令
STW1 = 1135 (046Fh)

【図】STW1 ビット配列 (原本 p.181)
- b15 → b0 の順に：0 0 0 0 0 1 0 0 0 1 1 0 1 1 1 1

NSOLL_A = (5000 (50Hz) × 16384 (4000h)) / 12000 (**Pr.1** = 120Hz) = 6827 (1AABh)

##### ◆ Drive Profile Parameters (Acyclic Data Exchange) (2.12.5 / 原本 p.182)

PROFINET で使用するパラメータは 0 ～ 65535 の PNU 番号が割り当てられており、PROFIdrive パラメータ、PROFINET パラメータ、インバータパラメータ、モニタデータ、インバータ制御パラメータ、CiA402 ドライブプロファイルがあります。

| 項目 | 名称 | 設定値 |
|---|---|---|
| API 番号 | API_No | 3A00h |
| スロット番号 | Slot_No | 1h |
| サブスロット番号 | SubSlot_No | 1h |
| インデックス | Index | 2Fh |

###### ■ PROFIdrive パラメータ (2.12.5 / 原本 p.182)

下記のパラメータが実装されています。

| Group | PNU | Name | Access | Data Type | Description |
|---|---|---|---|---|---|
| PROFIdrive パラメータ | P915 | Selection switch Setpoint telegram | R | Array[n] Unsigned16 | Setpoint Telegram の設定を保持。 |
| PROFIdrive パラメータ | P916 | Selection switch Actual value telegram | R | Array[n] Unsigned16 | Actual Value Telegram の設定を保持。 |
| PROFIdrive パラメータ | P922 | Telegram Selection | R | Unsigned16 | 初期値：Standard Telegram 1<br>マスタから受信した最新の設定データを反映。 |
| PROFIdrive パラメータ | P944 | Fault message counter | R | Unsigned16 | Fault numbers（P947）変更時に回数を 1 ずつ増加。 |
| PROFIdrive パラメータ | P947 | Fault numbers | R | Array[8] Unsigned16 | 電源投入後に発生したアラームコードが 8 個まで保存されます。<br>9 個目以降は 8 番目に上書きされます。 |
| PROFIdrive パラメータ | P964 | Drive Unit identification | R | Array[5] Unsigned16 | メーカ ID：021Ch（三菱電機）<br>ドライブユニットタイプ：0<br>バージョン（ソフトウェア）：xxyy（十進数）<br>ファームウェア作成日（年）：0000（未対応）<br>ファームウェア作成日（日 / 月）：0000（未対応） |
| PROFIdrive パラメータ | P965 | Profile identification number | R | Octetstring2 | バイト 0：3（PROFIdrive プロファイル）<br>バイト 1：42（バージョン 4.2） |
| PROFIdrive パラメータ | P967 | STW1 | R | V2 | コントローラから受信した最後のコントロールワード。 |
| PROFIdrive パラメータ | P968 | ZSW | R | V2 | インバータから受信した現在のステータスワード。 |
| PROFIdrive パラメータ | P972 | Drive reset | R/W | Unsigned16 | 2、1 の順に書き込むことでインバータリセットします。 |
| PROFIdrive パラメータ | P975 | DO identification | R | Array[8] Unsigned16 | メーカ ID：021Ch（三菱電機）<br>ドライブオブジェクトタイプ：0<br>バージョン（ソフトウェア）：xxyy（十進数）<br>ファームウェア作成日（年）：0000（未対応）<br>ファームウェア作成日（日 / 月）：0000（未対応）<br>PROFIdrive DO type class：1（Axis）<br>PROFIdrive DO sub class 1：1（Application Class 1 supported）<br>Drive Object ID (DO-ID)：1（Number of Drive Objects(DO) ） |
| PROFIdrive パラメータ | P980 | Parameter Database Handling and Identification | R | Array[n] Unsigned16 | サポートしている全ての PNU 番号はサブインデックスに格納されます。配列は、PROFIdrive パラメータ、PROFINET パラメータ、インバータパラメータ、モニタデータ、インバータ制御パラメータ、CiA402 ドライブプロファイルの順に割り付けられます。<br>PNU リストの最初のパラメータは、サブインデックスに "0" を入れます。 |
| インバータパラメータ | P12288 ～ P16383 | Inverter Parameters | R/W | Array[n] Unsigned16 | インバータパラメータ番号＋ 12288（3000h）が PNU 番号になります。 |
| モニタデータ | P16384 ～ P20479 | Monitor Data | R | Unsigned16 | モニタコード＋ 16384（4000h）が PNU 番号になります。 |
| インバータ制御パラメータ | P20480 ～ P24575 | Inverter Control Parameters | R/W | Unsigned16 | インバータ制御パラメータ |
| CiA402 ドライブプロファイル | P24576 ～ P28671 | CiA402 Drive Profile | R/W | - | CiA402 ドライブプロファイル |
| PROFINET パラメータ | P61000 | Name of station | R | Octetstring240 | デバイスの局名 |
| PROFINET パラメータ | P61001 | IP address | R | Octetstring4 | 現在の IP アドレス |
| PROFINET パラメータ | P61002 | MAC address | R | Octetstring6 | MAC アドレス |
| PROFINET パラメータ | P61003 | Gateway | R | Octetstring4 | 現在のゲートウェイアドレス |
| PROFINET パラメータ | P61004 | Subnet mask | R | Octetstring4 | 現在のサブネットマスク |

（注: 表は原本 p.182〜p.183 にまたがる。PROFINET パラメータ（P61000〜P61004）は原本 p.183 の続き部分）

- Selection switch Setpoint telegram、Selection switch Actual value telegram (P915/P916) (2.12.5 / 原本 p.183)

| PNU | Sub | Access | Name | Data Type | Description | Default |
|---|---|---|---|---|---|---|
| 915 | 0 ～ n | R | Selection switch Setpoint telegram | Array[n] Unsigned16 | サイクリックデータに割り付けられた setpoint の内容を返信します。 | - |
| 916 | 0 ～ n | R | Selection switch Actual value telegram | Array[n] Unsigned16 | サイクリックデータに割り付けられた actual value の内容を返信します。 | - |

読出し値の内容は次のとおりです。

| 信号番号 | 内容 |
|---|---|
| 1 | Control word 1 (STW1) |
| 2 | Status word 1 (ZSW1) |
| 5 | Speed setpoint A (NSOLL_A) |
| 6 | Speed actual value A (NIST_A) |
| 100 | Target torque |
| 101 | Actual torque |
| 12288 ～ 16383 | Inverter Parameters |
| 16384 ～ 20479 | Monitor Data |
| 20480 ～ 24575 | Inverter Control Parameters |
| 24576 ～ 28671 | CiA402 Drive Profile |

- Telegram Selection (P922) (2.12.5 / 原本 p.183)

| PNU | Sub | Access | Name | Data Type | Description | Default |
|---|---|---|---|---|---|---|
| 922 | 0 | R | Telegram selection | Unsigned16 | 選択中の Telegram を返信します。 | 1 |

読出し値の内容は次のとおりです。

| Value | 内容 |
|---|---|
| 1 | Standard Telegram 1 |
| 100 | Telegram 100 |
| 102 | Telegram 102 |

- Fault message counter (P944) (2.12.5 / 原本 p.183)

| PNU | Sub | Access | Name | Data Type | Description | Default |
|---|---|---|---|---|---|---|
| 944 | 0 | R | Fault message counter | Unsigned16 | Fault message counter の値を返信します。<br>この値は、インバータのアラーム発生時にインクリメントされます。 | 0 |

- Fault numbers (P947) (2.12.5 / 原本 p.183)

| PNU | Sub | Access | Name | Data Type | Description | Default |
|---|---|---|---|---|---|---|
| 947 | 0 ～ 7 | R | Fault numbers | Array[8] Unsigned16 | 電源投入後に発生したインバータのアラームコードを最大 8 個分表示します。インバータのアラーム未発生時、P947.0 ～ 7 の読出し値は 0 となります。 | 0 |

- Drive Unit identification (P964) (2.12.5 / 原本 p.183〜p.184)

インバータの識別情報を返信します。

| PNU | Sub | Access | Name | Data Type | Description | Default |
|---|---|---|---|---|---|---|
| 964 | 0 | R | Drive Unit identification | Array[5] Unsigned16 | Manufacturer ID<br>三菱電機のマニュファクチュア ID | 540 |
| 964 | 1 | R | Drive Unit identification | Array[5] Unsigned16 | デバイスタイプ | 0 |
| 964 | 2 | R | Drive Unit identification | Array[5] Unsigned16 | Firmware version<br>インバータのファームウェアバージョン | - |

- Profile identification number (P965) (2.12.5 / 原本 p.184)

| PNU | Sub | Access | Name | Data Type | Description | Default |
|---|---|---|---|---|---|---|
| 965 | 0 | R | Profile identification number | Octetstring2 | Profile Number 3 | 03h |
| 965 | 1 | R | Profile identification number | Octetstring2 | Profile Version Number 42 | 2Ah |

- STW1、ZSW1 (P967/P968) (2.12.5 / 原本 p.184)

Control word 1（STW1）の詳細（176 ページ）、Status word 1（ZSW1）の詳細（177 ページ）を参照してください。

- Drive reset (P972) (2.12.5 / 原本 p.184)

| PNU | Sub | Access | Name | Data Type | Description | Default |
|---|---|---|---|---|---|---|
| 972 | 0 | R/W | Drive reset | Unsigned16 | 0：Initial status (or status after a reset)<br>1：Power-on Reset (initiation)<br>2：Power-on Reset (preparation)<br>0 は読出しのみ。2、1 の順に書き込むことでインバータリセットします。 | 0 |

- DO identification (P975) (2.12.5 / 原本 p.184)

ドライブオブジェクトの識別情報を返信します。

| PNU | Sub | Access | Name | Data Type | Description | Default |
|---|---|---|---|---|---|---|
| 975 | 0 | R | DO identification | Array[8] Unsigned16 | Manufacturer ID<br>三菱電機のマニュファクチュア ID | 540 |
| 975 | 1 | R | DO identification | Array[8] Unsigned16 | Drive Object type | 0 |
| 975 | 2 | R | DO identification | Array[8] Unsigned16 | Firmware version<br>インバータのファームウェアバージョン | - |
| 975 | 5 | R | DO identification | Array[8] Unsigned16 | PROFIdrive DO type class<br>1: Axis | 1 |
| 975 | 6 | R | DO identification | Array[8] Unsigned16 | PROFIdrive DO sub class 1<br>1: Application Class 1 supported | 1 |
| 975 | 7 | R | DO identification | Array[8] Unsigned16 | Drive Object ID (DO-ID)<br>Number of Drive Objects(DO) | 1 |

（注: Sub 3、4 は原本の表に記載なし）

- Parameter Database Handling and Identification (P980) (2.12.5 / 原本 p.184)

| PNU | Sub | Access | Name | Data Type | Description | Default |
|---|---|---|---|---|---|---|
| 980 | 0 ～ n | R | Parameter Database Handling and Identification | Array[n] Unsigned16 | サポートしている全ての PNU 番号を PROFIdrive パラメータ、PROFINET パラメータ、インバータパラメータ、モニタデータ、インバータ制御パラメータ、CiA402 ドライブプロファイルの順にリスト表示します。 | - |

サブインデックスに指定した PNU 番号から最大 117 個分表示します。（エレメント数（最大 234）/Unsigned16（2byte））
サブインデックスに 1、エレメント数に 3 を設定した場合、P916、P922、P944 を表示します。

- Inverter Parameters (P12288 ～ P16383) (2.12.5 / 原本 p.184〜p.185)

| PNU | Sub | Access | Name | Data Type | Description | Default |
|---|---|---|---|---|---|---|
| 12288 ～ 16383 | 0、1 | R/W | Inverter Parameters | Array[n] Unsigned16 | インバータパラメータ番号＋ 12288（3000h）が PNU 番号になります。 | - |

校正パラメータ

| PNU | Sub | Name | Description |
|---|---|---|---|
| 13188（3384h） | 0 | Data | **C0(Pr.900)** |
| 13188（3384h） | 1 | Sub Data | - |
| 13189（3385h） | 0 | Data | **C1(Pr.901)** |
| 13189（3385h） | 1 | Sub Data | - |
| 13190（3386h） | 0 | Data | **C2(Pr.902)** |
| 13190（3386h） | 1 | Sub Data | **C3(Pr.902)** |
| 13191（3387h） | 0 | Data | **125(Pr.903)** |
| 13191（3387h） | 1 | Sub Data | **C4(Pr.903)** |
| 13192（3388h） | 0 | Data | **C5(Pr.904)** |
| 13192（3388h） | 1 | Sub Data | **C6(Pr.904)** |
| 13193（3389h） | 0 | Data | **126(Pr.905)** |
| 13193（3389h） | 1 | Sub Data | **C7(Pr.905)** |
| 13205（3395h）\*1 | 0 | Data | **C12(Pr.917)** |
| 13205（3395h）\*1 | 1 | Sub Data | **C13(Pr.917)** |
| 13206（3396h）\*1 | 0 | Data | **C14(Pr.918)** |
| 13206（3396h）\*1 | 1 | Sub Data | **C15(Pr.918)** |
| 13207（3397h）\*1 | 0 | Data | **C16(Pr.919)** |
| 13207（3397h）\*1 | 1 | Sub Data | **C17(Pr.919)** |
| 13208（3398h）\*1 | 0 | Data | **C18(Pr.920)** |
| 13208（3398h）\*1 | 1 | Sub Data | **C19(Pr.920)** |
| 13220（33A4h） | 0 | Data | **C38(Pr.932)** |
| 13220（33A4h） | 1 | Sub Data | **C39(Pr.932)** |
| 13221（33A5h） | 0 | Data | **C40(Pr.933)** |
| 13221（33A5h） | 1 | Sub Data | **C41(Pr.933)** |
| 13222（33A6h） | 0 | Data | **C42(Pr.934)** |
| 13222（33A6h） | 1 | Sub Data | **C43(Pr.934)** |
| 13223（33A7h） | 0 | Data | **C44(Pr.935)** |
| 13223（33A7h） | 1 | Sub Data | **C45(Pr.935)** |

\*1 FR-E8AXY 装着時のみ

インバータパラメータ番号およびパラメータ名称は取扱説明書（機能編）のパラメータ一覧を参照してください。

> **NOTE**
> - パラメータ設定値の “8888” は 65520（FFF0h）、設定値 “9999” は 65535（FFFFh）と設定してください。
> - パラメータ書込みを実施したとき、Cyclic Data Exchange の場合は RAM 書込みとなります。Acyclic Data Exchange の場合の EEPROM と RAM への書込み選択は、**Pr.342 通信 EEPROM 書込み選択**の設定によります。

- Monitor Data (P16384 ～ P20479) (2.12.5 / 原本 p.185)

| PNU | Sub | Access | Name | Data Type | Description | Default |
|---|---|---|---|---|---|---|
| 16384 ～ 20479 | 0 | R | Monitor Data | Unsigned16 | モニタコード＋ 16384（4000h）が PNU 番号になります。 | - |

モニタコードおよびモニタ項目については取扱説明書（機能編）の **Pr.52** の内容を参照してください。

> **NOTE**
> - **Pr.290 モニタマイナス出力選択**によるモニタ表示のマイナス出力は無効となります。
> - 周波数表示のモニタは **Pr.53** により回転数（機械速度）表示に変更できます。機械速度表示に切り換えた場合、表示単位は 1 単位となります。

- Inverter Control Parameters (P20480 ～ P24575) (2.12.5 / 原本 p.185〜p.186)

| PNU | Sub | Access | Name | Data Type | Description | Default |
|---|---|---|---|---|---|---|
| 20480 ～ 24575 | 0 | R/W | Inverter Control Parameters | Unsigned16 | インバータ制御パラメータ | - |

| PNU | Name | Access | Description |
|---|---|---|---|
| 20482（5002h）\*1 | インバータリセット | R/W | 書込み値は 9966h を設定してください。<br>読出し値は 0000h 固定 |
| 20483（5003h）\*1 | パラメータクリア | R/W | 書込み値は 965Ah を設定してください。<br>読出し値は 0000h 固定 |
| 20484（5004h）\*1 | パラメータオールクリア | R/W | 書込み値は 99AAh を設定してください。<br>読出し値は 0000h 固定 |
| 20486（5006h）\*1 | パラメータクリア \*2 | R/W | 書込み値は 5A96h を設定してください。<br>読出し値は 0000h 固定 |
| 20487（5007h）\*1 | パラメータオールクリア \*2 | R/W | 書込み値は AA99h を設定してください。<br>読出し値は 0000h 固定 |
| 20488（5008h） | 制御入力命令 / インバータ状態（拡張）\*3 | R/W | 185 ページ参照 |
| 20489（5009h） | 制御入力命令 / インバータ状態 \*3 | R/W | 185 ページ参照 |
| 20981（51F5h） | アラーム履歴 1 | R/W\*1 | データは 2byte のため “00 ○○ h” で格納されます。<br>下位 1byte にエラーコードを参照できます。（エラーコードは取扱説明書（保守編）の異常表示一覧を参照）<br>20981（51F5h）に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 |
| 20982（51F6h） | アラーム履歴 2 | R | データは 2byte のため “00 ○○ h” で格納されます。<br>下位 1byte にエラーコードを参照できます。（エラーコードは取扱説明書（保守編）の異常表示一覧を参照）<br>20981（51F5h）に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 |
| 20983（51F7h） | アラーム履歴 3 | R | データは 2byte のため “00 ○○ h” で格納されます。<br>下位 1byte にエラーコードを参照できます。（エラーコードは取扱説明書（保守編）の異常表示一覧を参照）<br>20981（51F5h）に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 |
| 20984（51F8h） | アラーム履歴 4 | R | データは 2byte のため “00 ○○ h” で格納されます。<br>下位 1byte にエラーコードを参照できます。（エラーコードは取扱説明書（保守編）の異常表示一覧を参照）<br>20981（51F5h）に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 |
| 20985（51F9h） | アラーム履歴 5 | R | データは 2byte のため “00 ○○ h” で格納されます。<br>下位 1byte にエラーコードを参照できます。（エラーコードは取扱説明書（保守編）の異常表示一覧を参照）<br>20981（51F5h）に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 |
| 20986（51FAh） | アラーム履歴 6 | R | データは 2byte のため “00 ○○ h” で格納されます。<br>下位 1byte にエラーコードを参照できます。（エラーコードは取扱説明書（保守編）の異常表示一覧を参照）<br>20981（51F5h）に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 |
| 20987（51FBh） | アラーム履歴 7 | R | データは 2byte のため “00 ○○ h” で格納されます。<br>下位 1byte にエラーコードを参照できます。（エラーコードは取扱説明書（保守編）の異常表示一覧を参照）<br>20981（51F5h）に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 |
| 20988（51FCh） | アラーム履歴 8 | R | データは 2byte のため “00 ○○ h” で格納されます。<br>下位 1byte にエラーコードを参照できます。（エラーコードは取扱説明書（保守編）の異常表示一覧を参照）<br>20981（51F5h）に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 |
| 20989（51FDh） | アラーム履歴 9 | R | データは 2byte のため “00 ○○ h” で格納されます。<br>下位 1byte にエラーコードを参照できます。（エラーコードは取扱説明書（保守編）の異常表示一覧を参照）<br>20981（51F5h）に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 |
| 20990（51FEh） | アラーム履歴 10 | R | データは 2byte のため “00 ○○ h” で格納されます。<br>下位 1byte にエラーコードを参照できます。（エラーコードは取扱説明書（保守編）の異常表示一覧を参照）<br>20981（51F5h）に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 |
| 20992（5200h）\*4 | Safety 入力状態 | R | 186 ページ参照 |

（注: 20981〜20990 の Description は原本では1つの結合セル。各行に展開した）

\*1 Cyclic Data Exchange では使用できません。
\*2 通信パラメータの設定値がクリアされません。
\*3 書込み時は制御入力命令としてデータを設定します。
読出し時はインバータ運転状態としてデータが読み出されます。
\*4 Ethernet 仕様品のみパラメータ設定可能です。安全通信仕様品、IP67 仕様品は Acyclic Data Exchange でアクセス可能ですが、機能無効です。

制御入力命令 / インバータ状態、制御入力命令 / インバータ状態（拡張）

| Bit | 制御入力命令 | インバータ状態 |
|---|---|---|
| 0 | - | RUN（インバータ運転中）\*2 |
| 1 | - | 正転中 |
| 2 | - | 逆転中 |
| 3 | RH（高速運転指令）\*1 | 周波数到達 |
| 4 | RM（中速運転指令）\*1 | 過負荷警報 |
| 5 | RL（低速運転指令）\*1 | 0 |
| 6 | JOG 運転選択 2 | FU（出力周波数検出）\*2 |
| 7 | 第 2 機能選択 | ABC（異常）\*2 |
| 8 | 端子 4 入力選択 | ABC2（機能なし）\*2 |
| 9 | - | セーフティモニタ出力 2 |
| 10 | MRS（出力停止）\*1 | 0 |
| 11 | - | 位置決め完了 |
| 12 | RES（機能なし）\*1 | 位置指令動作中 |
| 13 | - | 原点復帰完了 |
| 14 | - | 原点復帰異常 |
| 15 | - | 重故障発生 |

| Bit | 制御入力命令（拡張） | インバータ状態（拡張） |
|---|---|---|
| 0 | NET X1（機能なし）\*1 | NET Y1（機能なし）\*2 |
| 1 | NET X2（機能なし）\*1 | NET Y2（機能なし）\*2 |
| 2 | NET X3（機能なし）\*1 | NET Y3（機能なし）\*2 |
| 3 | NET X4（機能なし）\*1 | NET Y4（機能なし）\*2 |
| 4 | NET X5（機能なし）\*1 | 0 |
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

（注: 原本では上記2表は左右に並んだ1つの図表。定義欄の見出しは「定義」）

\*1 （　）内の信号は初期状態のものです。**Pr.180 ～ Pr.189（入力端子機能選択）**の設定により内容が変更します。
詳細は取扱説明書（機能編）の **Pr.180 ～ Pr.189（入力端子機能選択）**を参照してください。
各割付け信号は、各々 NET での有効 / 無効があります。（取扱説明書（機能編）参照）
\*2 （　）内の信号は初期状態のものです。**Pr.190 ～ Pr.197（出力端子機能選択）**の設定により内容が変更します。
詳細は取扱説明書（機能編）の **Pr.190 ～ Pr.197（出力端子機能選択）**を参照してください。

#### （続き）2.12.5 Data Exchange (2.12.5 / 印刷 p.174 / 原本 p.175)

##### （続き）◆ Drive Profile Parameters (Acyclic Data Exchange) (2.12.5 / 原本 p.182)

###### （続き）■ PROFIdrive パラメータ (2.12.5 / 原本 p.182)

（注: 以下は原本 p.185 の「• Inverter Control Parameters (P20480 ～ P24575)」の続き。PNU 20992（5200h）Safety 入力状態の「186 ページ参照」先。）

Safety 入力状態 (原本 p.187)

| Bit | 定義 |
|---|---|
| 0 | 0：端子 S1 が ON<br>1：端子 S1 が OFF（出力遮断中） |
| 1 | 0：端子 S2 が ON<br>1：端子 S2 が OFF（出力遮断中） |
| 2 ～ 15 | 0 |

• CiA402 Drive Profile (P24576 ～ P28671) (原本 p.187〜189)

| PNU | Sub | Name | Description | Access | Data type |
|---|---|---|---|---|---|
| 24639<br>(603Fh) | 0 | Error code | エラー番号<br>電源投入後、またはインバータリセット後に発生した最新の異常のエラーコードを返信します。<br>重故障が発生していない場合はエラーなしを返信します。<br>重故障発生中にアラーム履歴がクリアされた場合、エラーなしを返信します。<br>上位 8bit を FF 固定とし、下位 8bit をエラーコードとします。<br>（FFXXh：XX にエラーコードが入ります。）<br>（エラーコードは取扱説明書（保守編）の異常表示一覧を参照） | R | Unsigned16 |
| 24643<br>(6043h) | 0 | vl velocity demand | 出力周波数（r/min）*1<br>出力周波数を r/min 単位で読み出します。<br>モニタ範囲：-32768（8000h）～ 32767（7FFFh）<br>**Pr.81** ＝ “9999” の場合、モータ極数は 4 極として換算します。 | R | Integer16 |
| 24644<br>(6044h) | 0 | vl velocity actual value | 運転速度（r/min）*1<br>運転速度を r/min 単位で読み出します。<br>モニタ範囲：-32768（8000h）～ 32767（7FFFh）<br>**Pr.81** ＝ “9999” の場合、モータ極数は 4 極として換算します。 | R | Integer16 |
| 24672<br>(6060h) | 0 | Modes of operation | 制御モード：-1（ベンダ固有運転モード）（固定） | R/W | Integer8 |
| 24673<br>(6061h) | 0 | Modes of operation display | 現在の制御モード：-1（ベンダ固有運転モード）（固定） | R | Integer8 |
| 24674<br>(6062h) | 0 | Position demand value | 位置指令（pulse）<br>電子ギア演算前の位置指令を読み出します。 | R | Integer32 |
| 24675<br>(6063h) | 0 | Position actual internal value | 現在位置（pulse）<br>電子ギア演算後の現在位置を読み出します。 | R | Integer32 |
| 24676<br>(6064h) | 0 | Position actual value | 現在位置（pulse）<br>電子ギア演算前の現在位置を読み出します。 | R | Integer32 |
| 24689<br>(6071h) | 機能無効 | 機能無効 | 機能無効 | 機能無効 | 機能無効 |
| 24692<br>(6074h) | 0 | Torque demand | トルク要求値（%）<br>トルク指令を読み出します。 | R | Integer16 |
| 24695<br>(6077h) | 0 | Torque actual value | 現在トルク値（%）<br>モータトルクを読み出します。 | R | Integer16 |
| 24698<br>(607Ah) | 0 | Target position | 目標位置（pulse）<br>ダイレクトコマンドモード時の目標位置を設定します。<br>初期値：0<br>設定範囲：-2147483647 ～ 2147483647<br>（ダイレクトコマンドモードについては、FR-E800 取扱説明書（機能編）参照） | R/W | Integer32 |
| 24703<br>(607Fh) | 0 | Max profile velocity | 最大プロファイル速度（r/min）<br>**Pr.18 高速上限周波数**を r/min 単位で設定します。<br>設定範囲：0 ～ 590Hz | R/W | Unsigned32 |
| 24705<br>(6081h) | 0 | Profile velocity | プロファイル速度（r/min）<br>ダイレクトコマンドモード時の最高速度を設定します。<br>初期値：0<br>設定範囲：0 ～（120×590Hz/**Pr.81**）<br>（ダイレクトコマンドモードについては、FR-E800 取扱説明書（機能編）参照） | R/W | Unsigned32 |
| 24707<br>(6083h) | 0 | Profile acceleration | 加速時定数（ms）<br>＜位置制御＞<br>ダイレクトコマンドモード時の加速時間を設定します。<br>初期値：5000<br>設定範囲：10 ～ 360000<br>下 1 桁は切り捨てます。（1358ms の場合は、1350ms となります。）<br>（ダイレクトコマンドモードについては、FR-E800 取扱説明書（機能編）参照）<br>＜位置制御以外＞<br>**Pr.7 加速時間**を ms 単位で設定します。<br>設定範囲：0 ～ 3600s<br>**Pr.21 加減速時間単位**＝ “0” 設定時は下 2 桁、**Pr.21** ＝ “1” 設定時は下 1 桁を切り捨てます。 | R/W | Unsigned32 |
| 24708<br>(6084h) | 0 | Profile deceleration | 減速時定数（ms）<br>＜位置制御＞<br>ダイレクトコマンドモード時の減速時間を設定します。<br>初期値：5000<br>設定範囲：10 ～ 360000<br>下 1 桁は切り捨てます。（1358ms の場合は、1350ms となります。）<br>（ダイレクトコマンドモードについては、FR-E800 取扱説明書（機能編）参照）<br>＜位置制御以外＞<br>**Pr.8 減速時間**を ms 単位で設定します。<br>設定範囲：0 ～ 3600s<br>**Pr.21 加減速時間単位**＝ “0” 設定時は下 2 桁、**Pr.21** ＝ “1” 設定時は下 1 桁を切り捨てます。 | R/W | Unsigned32 |
| 24719<br>(608Fh) | - | Position encoder resolution | PLG 分解能（機械側 / モータ側） | - | - |
| 24719<br>(608Fh) | 0 | Highest sub-index supported | サブインデックスの最大値：02h（固定） | R | Unsigned8 |
| 24719<br>(608Fh) | 1 | Encoder increments | PLG 分解能<br>**Pr.369 PLG パルス数**を設定します。<br>設定範囲：2 ～ 4096 | R/W | Unsigned32 |
| 24719<br>(608Fh) | 2 | Motor revolutions | モータ回転数（rev）：00000001h（固定） | R/W | Unsigned32 |
| 24721<br>(6091h) | - | Gear ratio | ギア比 | - | - |
| 24721<br>(6091h) | 0 | Highest sub-index supported | サブインデックスの最大値：02h（固定） | R | Unsigned8 |
| 24721<br>(6091h) | 1 | Motor revolutions | モータ軸回転数 *2<br>**Pr.420 指令パルス倍率分子（電子ギア分子）**を設定します。<br>設定範囲：1 ～ 32767 | R/W | Unsigned32 |
| 24721<br>(6091h) | 2 | Shaft revolutions | 駆動軸回転数 *2<br>**Pr.421 指令パルス倍率分母（電子ギア分母）**を設定します。<br>設定範囲：1 ～ 32767 | R/W | Unsigned32 |
| 24728<br>(6098h) | 0 | Homing method | 原点復帰方法<br>ダイレクトコマンドモード時の原点復帰方式を設定します。*3<br>（ダイレクトコマンドモード、原点復帰方式については、FR-E800 取扱説明書（機能編）参照） | R/W | Integer8 |
| 24729<br>(6099h) | - | Homing speeds | 原点復帰速度 | - | - |
| 24729<br>(6099h) | 0 | Highest sub-index supported | サブインデックスの最大値：02h（固定） | R | Unsigned8 |
| 24729<br>(6099h) | 1 | Speed during search for switch | 原点復帰時のモータ速度（r/min）<br>ダイレクトコマンドモード時の原点復帰速度を設定します。<br>初期値：120×2Hz/**Pr.81**<br>設定範囲：0 ～（120×400Hz/**Pr.81**）<br>（ダイレクトコマンドモードについては、FR-E800 取扱説明書（機能編）参照） | R/W | Unsigned32 |
| 24729<br>(6099h) | 2 | Speed during search for zero | 近点ドグ前端検出後のクリープ速度（r/min）<br>ダイレクトコマンドモード時の原点復帰クリープ速度を設定します。<br>初期値：120×3Hz/**Pr.81**<br>設定範囲：0 ～（120×400Hz/**Pr.81**）<br>（ダイレクトコマンドモードについては、FR-E800 取扱説明書（機能編）参照） | R/W | Unsigned32 |
| 24730<br>(609Ah) | 0 | Homing acceleration | 原点復帰加減速時間（ms）<br>ダイレクトコマンドモード時の原点復帰加速時間、減速時間を設定します。<br>初期値：5000<br>設定範囲：10 ～ 360000<br>下 1 桁は切り捨てます。（1358ms の場合は、1350ms となります。）<br>（ダイレクトコマンドモードについては、FR-E800 取扱説明書（機能編）参照） | R/W | Unsigned32 |
| 24820<br>(60F4h) | 0 | Following error actual value | 溜りパルス（pulse）<br>電子ギア演算前の溜りパルスを読み出します。 | R | Integer32 |
| 24826<br>(60FAh) | 0 | Control effort | 位置ループ後の速度指令 *1<br>理想速度指令を読み出します。 | R | Integer32 |
| 24828<br>(60FCh) | 0 | Position demand internal value | 位置指令（pulse）<br>電子ギア演算後の位置指令を読み出します。 | R | Integer32 |
| 25858<br>(6502h) | 0 | Supported drive modes | 対応する制御モード：00010000h（ベンダ固有運転モード） | R | Unsigned32 |

（注: 24689（6071h）は原本では Sub〜Data type の列が結合され「機能無効」とのみ記載。）

*1 **Pr.53** の設定に関係なく r/min 単位で表示、設定します。<br>
　読出し時は、周波数を回転速度変換して読み出し、書込み時は、設定値を周波数変換して書き込みます。<br>
*2 パラメータ書込みを実施したとき、Cyclic Data Exchange の場合は RAM 書込みとなります。Acyclic Data Exchange の場合の EEPROM と RAM への書込み選択は、**Pr.342 通信 EEPROM 書込み選択**の設定によります。<br>
*3 P24728（6098h）の設定値と対応する原点復帰方式を下表に示します。

| P24728（6098h）設定値 | 原点復帰方式 |
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

• Name of station (P61000) (原本 p.189)

| PNU | Sub | Access | Name | Data Type | Description | Default |
|---|---|---|---|---|---|---|
| 61000 | 0 ～ 239 | R | Name of station | Octetstring240 | デバイス名 | FR-E800-(SC)E |

• IP address (P61001) (原本 p.189)

| PNU | Sub | Access | Name | Data Type | Description | Default |
|---|---|---|---|---|---|---|
| 61001 | 0 | R | IP address | Octetstring4 | IP アドレス第 1 オクテット | - |
| 61001 | 1 | R | IP address | Octetstring4 | IP アドレス第 2 オクテット | - |
| 61001 | 2 | R | IP address | Octetstring4 | IP アドレス第 3 オクテット | - |
| 61001 | 3 | R | IP address | Octetstring4 | IP アドレス第 4 オクテット | - |

• MAC address (P61002) (原本 p.190)

| PNU | Sub | Access | Name | Data Type | Description | Default |
|---|---|---|---|---|---|---|
| 61002 | 0 | R | MAC address | Octetstring6 | MAC アドレス（上位） | - |
| 61002 | 1 | R | MAC address | Octetstring6 | MAC アドレス | - |
| 61002 | 2 | R | MAC address | Octetstring6 | MAC アドレス | - |
| 61002 | 3 | R | MAC address | Octetstring6 | MAC アドレス | - |
| 61002 | 4 | R | MAC address | Octetstring6 | MAC アドレス | - |
| 61002 | 5 | R | MAC address | Octetstring6 | MAC アドレス（下位） | - |

• Gateway (P61003) (原本 p.190)

| PNU | Sub | Access | Name | Data Type | Description | Default |
|---|---|---|---|---|---|---|
| 61003 | 0 | R | Gateway | Octetstring4 | ゲートウェイアドレス第 1 オクテット | - |
| 61003 | 1 | R | Gateway | Octetstring4 | ゲートウェイアドレス第 2 オクテット | - |
| 61003 | 2 | R | Gateway | Octetstring4 | ゲートウェイアドレス第 3 オクテット | - |
| 61003 | 3 | R | Gateway | Octetstring4 | ゲートウェイアドレス第 4 オクテット | - |

• Subnet mask (P61004) (原本 p.190)

| PNU | Sub | Access | Name | Data Type | Description | Default |
|---|---|---|---|---|---|---|
| 61004 | 0 | R | Subnet mask | Octetstring4 | サブネットマスク第 1 オクテット | 255 |
| 61004 | 1 | R | Subnet mask | Octetstring4 | サブネットマスク第 2 オクテット | 255 |
| 61004 | 2 | R | Subnet mask | Octetstring4 | サブネットマスク第 3 オクテット | 255 |
| 61004 | 3 | R | Subnet mask | Octetstring4 | サブネットマスク第 4 オクテット | 0 |

###### ■ PROFIdrive パラメータ要求フォーマット（マスタ→インバータ） (2.12.5 / 原本 p.190)

| 区分 | Byte No. | Field | 内容 | パラメータ読出し | パラメータ変更 |
|---|---|---|---|---|---|
| ヘッダ | 0 | Request reference | マスタ側の設定による | ○ | ○ |
| ヘッダ | 1 | リクエスト ID | パラメータ読出し：01h<br>パラメータ変更：02h | ○ | ○ |
| ヘッダ | 2 | DO-ID | 01h | ○ | ○ |
| ヘッダ | 3 | パラメータ数 | 01h | ○ | ○ |
| パラメータアドレス | 4 | Attribute | 10h | ○ | ○ |
| パラメータアドレス | 5 | エレメント数（n） | 配列数による（最大 234）<br>Array、Octetstring 以外は 0 または 1 | ○ | ○ |
| パラメータアドレス | 6 | PNU 番号 | 181 ページ参照 | ○ | ○ |
| パラメータアドレス | 7 | PNU 番号 | 181 ページ参照 | ○ | ○ |
| パラメータアドレス | 8 | sub-index | 181 ページ参照 | ○ | ○ |
| パラメータアドレス | 9 | sub-index | 181 ページ参照 | ○ | ○ |
| パラメータ値 | 10 | フォーマット | Data Type<br>Unsigned16：06h<br>Octetstring：0Ah<br>V2：73h | × | ○ |
| パラメータ値 | 11 | データ数 | 配列数 | × | ○ |
| パラメータ値 | 12 | パラメータ値 | パラメータ書込み値 | × | ○ |
| パラメータ値 | 13 | パラメータ値 | パラメータ書込み値 | × | ○ |
| パラメータ値 | 14 ～ 237 | パラメータ値 | パラメータ書込み値 | × | ○ *1 |
| パラメータ値 | 238 | パラメータ値 | パラメータ書込み値 | × | ○ *1 |
| パラメータ値 | 239 | パラメータ値 | パラメータ書込み値 | × | ○ *1 |

（注: 「区分」列の見出しは原本では空欄。「181 ページ参照」は Byte 6〜9 の結合セル。）

*1 フォーマットやデータ数によります。

###### ■ PROFIdrive パラメータ応答フォーマット（インバータ→マスタ） (2.12.5 / 原本 p.191)

| 区分 | Byte No. | Field | 内容 | パラメータ読出し Positive | パラメータ読出し Negative | パラメータ変更 Positive | パラメータ変更 Negative |
|---|---|---|---|---|---|---|---|
| ヘッダ | 0 | Request reference | マスタ側の設定による | ○ | ○ | ○ | ○ |
| ヘッダ | 1 | リクエスト ID | パラメータ読出し（Positive）：01h<br>パラメータ変更（Positive）：02h<br>パラメータ読出し（Negative）：81h<br>パラメータ変更（Negative）：82h<br>リクエスト ID 異常：80h | ○ | ○ | ○ | ○ |
| ヘッダ | 2 | DO-ID | 01h | ○ | ○ | ○ | ○ |
| ヘッダ | 3 | パラメータ数 | 01h | ○ | ○ | ○ | ○ |
| パラメータ値 | 4 | フォーマット | Data Type<br>Unsigned16：06h<br>Octetstring：0Ah<br>V2：73h<br>エラー返答時は 44h | ○ | ○ | × | ○ |
| パラメータ値 | 5 | データ数 | 配列数 | ○ | ○ | × | ○ |
| パラメータ値 | 6 | パラメータ値 / エラー番号 | パラメータ読出し値またはエラー番号 | ○ | ○ | × | ○ |
| パラメータ値 | 7 | パラメータ値 / エラー番号 | パラメータ読出し値またはエラー番号 | ○ | ○ | × | ○ |
| パラメータ値 | 8 | パラメータ値 / エラー番号 | パラメータ読出し値またはエラー番号 | ○ *1 | × | × | × |
| パラメータ値 | 9 | パラメータ値 / エラー番号 | パラメータ読出し値またはエラー番号 | ○ *1 | × | × | × |
| パラメータ値 | 10 ～ 237 | パラメータ値 / エラー番号 | パラメータ読出し値またはエラー番号 | ○ *1 | × | × | × |
| パラメータ値 | 238 | パラメータ値 / エラー番号 | パラメータ読出し値またはエラー番号 | ○ *1 | × | × | × |
| パラメータ値 | 239 | パラメータ値 / エラー番号 | パラメータ読出し値またはエラー番号 | ○ *1 | × | × | × |

（注: 「区分」列の見出しは原本では空欄。）

*1 フォーマットやデータ数によります。

###### ■ エラー番号 (2.12.5 / 原本 p.191)

| Error No. | 名称 | 内容 |
|---|---|---|
| 00h | Impermissible parameter number | 存在しない PROFIdrive パラメータへのアクセス |
| 01h | Parameter value cannot be changed | 書込み不可 PROFIdrive パラメータへの書込み |
| 02h | Low or high limit exceeded | 設定範囲外 |
| 03h | Faulty subindex | 存在しないサブインデックスへのアクセス |
| 04h | No array | サブインデックスのない PROFIdrive パラメータへのアクセス |
| 05h | Incorrect data type | データタイプ不一致 |
| 11h | Request cannot be executed because of operating state | 動作状態により一時的にアクセス不可 |
| 16h | Parameter address impermissible | 不正な値、不正なエレメント数、不正な PNU 番号とサブインデックスの組み合わせ |
| 17h | Illegal format | 不正な PROFIdrive パラメータデータフォーマット |
| 19h | Axis/DO nonexistent | 存在しない軸やオブジェクトへのアクセス |
| 21h | Service not supported | サービス範囲外（不正なリクエスト ID） |
| 23h | Multi parameter access not supported | 一度に複数のパラメータへアクセス |

##### ◆ プログラミング例 (2.12.5 / 原本 p.191)

Standard Telegram 1 選択時、シーケンスプログラムでインバータを制御するプログラム例を示します。
Ethernet 機能選択（**Pr.1427 ～ Pr.1430**）に “34962”（PROFINET）が設定されていることを確認してください。

###### ■ 50Hz 正転で運転する場合のプログラム例 (2.12.5 / 原本 p.192)

• ネットワーク設定、デバイス例

| デバイス名 | 内容 |
|---|---|
| M0 | インバータ正転 |
| D0.0 | DataExchangeStartRequest |
| D109 | Control word 1 (STW1) |
| D109.0 | ON/OFF |
| D109.1 | 出力遮断 |
| D109.2 | 緊急停止 |
| D109.3 | 運転許可 |
| D109.4 | - |
| D109.5 | 加減速中断 |
| D109.6 | 設定周波数有効 |
| D109.7 | エラークリア |
| D109.8 | - |
| D109.9 | - |
| D109.A | シーケンサからの DOIO データ有効 |
| D109.B | 設定トルク有効 |
| D109.C | 始動指令方向選択 |
| D109.D ～ D109.F | - |
| D110 | Speed setpoint A (NSOLL_A) |
| D111 | Status word 1 (ZSW1) |
| D111.0 | Ready To Switch On/Not Ready To Switch On |
| D111.1 | Ready To Operate/Not Ready To Operate |
| D111.2 | Operation Enabled (drive follows setpoint)/Operation Disabled |
| D111.3 | Fault Present/No Fault |
| D111.4 | 出力停止中 |
| D111.5 | 緊急停止中 |
| D111.6 | Switching On Inhibited/Switching On Not Inhibited |
| D111.7 | Warning Present/No Warning |
| D111.8 | - |
| D111.9 | Control Requested/No Control Requested |
| D111.A ～ D111.F | - |
| D112 | Speed actual value A (NIST_A) |

S1（Switching On Inhibited）から S3（Switched On）に状態遷移するプログラム例（状態遷移図は 179 ページ参照）

• 設定周波数：Speed setpoint A (NSOLL_A)
　NSOLL_A = (5000 (50Hz) × 16384 (4000h)) / 12000 (**Pr.1** = 120Hz) = 6826 (1AAAh)

M0 を ON にすると 50Hz 正転で運転します。
M0 を OFF にすると停止します。

【図】50Hz 正転運転のラダープログラム例 (原本 p.193)
- ステップ (0)：D0.0（DataExchangeStartRequest）の a 接点と D111.3（Fault Present/No Fault）の b 接点の直列で、以下を駆動
  - D109.2（緊急停止）コイル
  - D109.1（出力遮断）コイル
  - D109.A（シーケンサからの DOIO データ有効）コイル
  - さらに D111.0（Ready To Switch On/Not Ready To Switch On）の a 接点を経由して以下を駆動
    - D109.0（ON/OFF）コイル
    - D109.5（加減速中断）コイル
    - D109.6（設定周波数有効）コイル
    - MOV K6826 D110（Speed setpoint A (NSOLL_A)）
    - D111.1（Ready To Operate/Not Ready To Operate）の a 接点と M0（インバータ正転）の a 接点の直列で D109.3（運転許可）コイル
- ステップ (14)：END

ニモニック（図から書き起こし）:

```
LD   D0.0
ANI  D111.3
OUT  D109.2
OUT  D109.1
OUT  D109.A
AND  D111.0
OUT  D109.0
OUT  D109.5
OUT  D109.6
MOV  K6826 D110
AND  D111.1
AND  M0
OUT  D109.3
END
```

（注: ニモニックは原本の回路図から転記者が書き起こしたもの。原本に記載のステップ番号は (0) と (14)（END）のみ。）

##### ◆ 設定例 (2.12.5 / 原本 p.193)

• 周期通信データ選択時（Telegram 102）の設定例を下記に示します。Control word 1 (STW1) bit10 を ON とすると、データがインバータへ書き込まれます。Control word 1 (STW1) bit10 が ON の間、常にデータは更新されます。（データ書込みの応答時間は最大 100ms です。）

• Telegram 102

| 種類 | IO Data number | 名称 |
|---|---|---|
| Setpoint Telegram<br>（マスタ→インバータ） | 1 | Control word 1 (STW1) |
| Setpoint Telegram<br>（マスタ→インバータ） | 2 | **Pr.1320** |
| Setpoint Telegram<br>（マスタ→インバータ） | 3 | **Pr.1321** |
| Setpoint Telegram<br>（マスタ→インバータ） | 4 | **Pr.1322** |
| Actual Value Telegram<br>（インバータ→マスタ） | 1 | Status word 1 (ZSW1) |
| Actual Value Telegram<br>（インバータ→マスタ） | 2 | **Pr.1330** |
| Actual Value Telegram<br>（インバータ→マスタ） | 3 | **Pr.1331** |
| Actual Value Telegram<br>（インバータ→マスタ） | 4 | **Pr.1332** |
| Actual Value Telegram<br>（インバータ→マスタ） | 5 | **Pr.1333** |
| Actual Value Telegram<br>（インバータ→マスタ） | 6 | **Pr.1334** |
| Actual Value Telegram<br>（インバータ→マスタ） | 7 | **Pr.1335** |

• パラメータ (原本 p.194)

| Pr. | 名称 | 設定例 | 備考 |
|---|---|---|---|
| 1320 | 周期通信入力データ選択 1 | 5（5h） | Speed setpoint A (NSOLL_A) |
| 1321 | 周期通信入力データ選択 2 | 12295（3007h） | **Pr.7 加速時間**<br>7（0007h）+12288（3000h） |
| 1322 | 周期通信入力データ選択 3 | 12296（3008h） | **Pr.8 減速時間**<br>8（0008h）+12288（3000h） |
| 1330 | 周期通信出力データ選択 1 | 6（6h） | Speed actual value A (NIST_A) |
| 1331 | 周期通信出力データ選択 2 | 12295（3007h） | **Pr.7 加速時間**<br>7（0007h）+12288（3000h） |
| 1332 | 周期通信出力データ選択 3 | 12296（3008h） | **Pr.8 減速時間**<br>8（0008h）+12288（3000h） |
| 1333 | 周期通信出力データ選択 4 | 16386（4002h） | 出力電流モニタ<br>2（0002h）+16384（4000h） |
| 1334 | 周期通信出力データ選択 5 | 12543（30FFh） | **Pr.255 寿命警報状態表示**<br>255（00FFh）+12288（3000h） |
| 1335 | 周期通信出力データ選択 6 | 20981（51F5h） | アラーム履歴 1 |

• エンジニアリングツールでのコネクション設定

インバータの「Module Configuration」で「Telegram 102」を設定します。
設定項目の名称はエンジニアリングツールにより異なる場合があります。


---

## 転記時の要確認一覧 (2.12 / 原本 p.171-194)

（注: 転記担当が記録した、原本の不整合・判読上の注意。原文はいずれも原本どおり転記済み）

- 状態遷移図（原本 p.180）の (16)(18)(20) の矢印には図中ラベル文字がない。始点・終点は図の目視で読み取ったもの（(16) S4→S5-3、(18) S5-1→S5-3、(20) S5-3→S5-2）。
- P975 の表は Sub 0、1、2、5、6、7 のみ記載で、Sub 3、4 の記載なし（原本どおり）。P975 の Data Type は Array[8]。
- 見出しレベル: 本パートでは AGENT_RULES どおり ■ を `######`（◆ の下）で書いた。直前パート 02h1 では ■ データマッピング等が `#####` になっており、結合時にレベル不整合あり。
