# 三菱 MELSEC iQ-F FX5-EIP形 EtherNet/IPユニット ユーザーズマニュアル 第1章 概要

| 項目 | 内容 |
|---|---|
| 原本 | 三菱電機 MELSEC iQ-F FX5-EIP形EtherNet/IPユニットユーザーズマニュアル |
| 発行元 | 三菱電機株式会社 |
| 資料番号 / 版数 | SH-082708 / B版（PDFメタデータ subject: SH-082708-B） |
| 原本PDF | `PDF/MELSEC iQ-F FX5-EIP形EtherNet_IPユニットユーザーズマニュアル.pdf` (全274ページ) |
| 本ファイルの範囲 | 第1章 (印刷 p.14-15 / PDF p.16-17) |
| ページ対応 | 「原本 p.」はPDFのページ番号、「印刷 p.」は原本フッタのページ番号。印刷ページ = PDFページ − 2。本文中の「〇〇ページ参照」は印刷ページ |
| 変換日 | 2026-10-23 |
| 変換方法 | pypdfium2(本文) + PyMuPDF 200dpi 画像の目視(全ページ) |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。

**転記上の扱い**: 図は【図】プレースホルダ＋読み取れる事実の箇条書き。見出しレベル: 章 `##` / 節 `###` / 項 `####`。第1章には節番号付きの節がなく、原本の帯見出し（EtherNet/IP通信・汎用Ethernet通信）は `###` で転記した。

---

## 主要用語 対訳表 (Glossary) (第1章 / 原本 p.16-17)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| EtherNet/IPユニット | EtherNet/IP module | FX5-EIP | 参考訳 |
| インテリジェント機能ユニット | Intelligent function module | — | 参考訳 |
| 汎用Ethernet | General-purpose Ethernet | — | 参考訳 |
| EtherNet/IP通信 | EtherNet/IP communication | — | 参考訳 |
| 汎用Ethernet通信 | General-purpose Ethernet communication | — | 参考訳 |
| CIP通信プロトコル | CIP communication protocol | CIP (Common Industrial Protocol) | 参考訳 |
| TCP/UDP通信プロトコル | TCP/UDP communication protocol | TCP / UDP | 参考訳 |
| スキャナ | Scanner | — | 参考訳 |
| アダプタ | Adapter | — | 参考訳 |
| オリジネータ | Originator | — | 参考訳 |
| クライアント | Client | — | 参考訳 |
| ターゲット | Target | — | 参考訳 |
| サーバ | Server | — | 参考訳 |
| ハブ | Hub | — | 参考訳 |
| EtherNet/IP機器 | EtherNet/IP device | — | 参考訳 |
| 外部機器 | External device | — | 参考訳 |
| 上位システム | Host system | — | 参考訳 |

## 変換範囲表 (第1章 / 原本 p.16-17)

| 原本ページ | 節 | 扱い |
|---|---|---|
| p.16 | 1 概要（EtherNet/IP通信・汎用Ethernet通信） | 全文 |
| p.17 | MEMO（白紙のメモ欄） | 全文（記載なし） |
| 上記以外 | 他章 | 同フォルダの他ファイル参照（目次 p.10-13 は未変換） |

## 目次 (第1章)

- [1 概要 (1 / 印刷 p.14 / 原本 p.16)](#1-概要-1--印刷-p14--原本-p16)
  - [EtherNet/IP通信 (1 / 印刷 p.14 / 原本 p.16)](#ethernetip通信-1--印刷-p14--原本-p16)
  - [汎用Ethernet通信 (1 / 印刷 p.14 / 原本 p.16)](#汎用ethernet通信-1--印刷-p14--原本-p16)

## 1 概要 (1 / 印刷 p.14 / 原本 p.16)

FX5-EIP形EtherNet/IPユニット(以下FX5-EIPと略称)は，EtherNet/IPネットワークおよび汎用Ethernetに接続するためのインテリジェント機能ユニットです。

### EtherNet/IP通信 (1 / 印刷 p.14 / 原本 p.16)

CIP通信プロトコルを用いて，EtherNet/IPネットワークとシームレスに通信できます。

FX5-EIPは，EtherNet/IPネットワークのスキャナ(オリジネータ/クライアント)またはアダプタ(ターゲット/サーバ)として動作します。

【図】EtherNet/IP通信のシステム構成例（原本 p.16）
- (1) FX5-EIP(スキャナ)
- (2) ハブ
- (3) FX5-EIP(アダプタ)
- (4) EtherNet/IP機器(スキャナ/アダプタ)
- 図の接続: (1) FX5-EIP(スキャナ)を装着したCPUユニットから (2) ハブへ1本。ハブから (3) FX5-EIP(アダプタ)を装着したCPUユニット、および (4) EtherNet/IP機器 2台へそれぞれ1本ずつ接続（スター型）

### 汎用Ethernet通信 (1 / 印刷 p.14 / 原本 p.16)

TCP/UDP通信プロトコルを用いて，パソコンなどの上位システムと接続できます。

【図】汎用Ethernet通信のシステム構成例（原本 p.16）
- (1) FX5-EIP
- (2) ハブ
- (3) CPUユニット
- (4) 外部機器(パソコンなど)
- 図の接続: (3) CPUユニット＋(1) FX5-EIP の組が2組あり、左の組は FX5-EIP から (2) ハブへ1本、右の組は CPUユニット側と FX5-EIP 側の両方から (2) ハブへ1本ずつ。ハブから (4) 外部機器(パソコン) 2台へそれぞれ1本ずつ接続

#### MEMO (1 / 印刷 p.15 / 原本 p.17)

（原本は見出し「MEMO」のみで、本文の記載なし）

## 転記時の要確認一覧 (第1章 / 原本 p.16-17)

- 汎用Ethernet通信の構成図（原本 p.16）の線の接続元（右の組は CPUユニット側と FX5-EIP 側の2本、左の組は FX5-EIP 側の1本）は図からの判読で、原本に文章での説明はない。要確認
