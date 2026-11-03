# MX Component Version 5 リファレンスマニュアル 10章 各通信経路で設定するプロパティ (4/9) p.265-293

| 項目 | 内容 |
|---|---|
| 原本 | 【三菱】MX Component Version 5 リファレンスマニュアル (SH-082394J) |
| メーカー | 三菱電機 |
| 原本ファイル | `PDF/【三菱】MX Component Version 5 リファレンスマニュアル_sh082394j.pdf` (全696ページ) |
| 本ファイルの範囲 | 10.2 Ethernet通信のうち「接続局がEthernetアダプタのEthernet通信(TCP)(1)」〜「接続局がCC-Link IE TSNユニットのEthernet通信(UDP)」，10.3 CPU COM通信 全体 (印刷ページ 263-291 / PDF p.265-293) |
| 出典表記 | `(節 / 印刷ページ / 原本 p.PDFページ)` |
| 作成日 | 2026-11-03 |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。
> 本文中の「○ページ」はすべて原本の**印刷ページ番号**です(PDFページ = 印刷ページ + 2)。
> 「アクセス可否およびプロパティのパターン」表は，原本の2段ヘッダ(接続局CPU / 経由局CPU)を「接続局CPU ○○」「経由局CPU ○○」の1段ヘッダに展開している。原本で行ラベルの「接続局CPU」欄は全行で結合されているため，各行に同じ値を記載。
> プロパティ一覧で原本が複数パターン列にまたがる結合セル(共通値)は，各パターン列に同じ値を展開して記載している。
> デフォルト値「34(CPU_Q02CPU)」は原本表記のまま(9章のCPUタイプ一覧に該当行が無い点は 09_ を参照)。

## 主要用語 対訳表 (Glossary)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| 接続局 / 接続局CPU | Connected station / Connected station CPU | — | 参考訳 |
| 経由局 / 経由局CPU | Relay station / Relay station CPU | — | 参考訳 |
| 経由ユニット / 経由ネットワーク | Relay module / Relay network | — | 参考訳 |
| 対象局 | Target station | — | 参考訳 |
| アクセス可否およびプロパティのパターン | Accessibility and property pattern | ○(n) | 参考訳 |
| プロパティ一覧 | Property list | — | 参考訳 |
| デフォルト値 | Default value | — | 参考訳 |
| ○○固定 | Fixed to ○○ | — | 参考訳 |
| ユーザ任意 | Any value (user-defined) | — | 参考訳 |
| Ethernetアダプタ | Ethernet adapter | FX3U-ENET-ADP / FX5-ENET 等 | 参考訳 |
| 直結通信 / 直結接続 | Direct connection | UNIT_FXVENET_DIRECT / UNIT_FXETHER_DIRECT | 参考訳 |
| PC側のアダプタ選択 | PC side adapter selection | ActHostAddress | 参考訳 |
| CC-Link IE TSNユニット | CC-Link IE TSN module | UNIT_RJ71GN11(0x1006) | 参考訳 |
| ロボットコントローラ | Robot controller | RC_PROTOCOL_TCPIP / RC_PROTOCOL_SERIAL | 参考訳 |
| インバータ | Inverter | INV_A800(0x1E60) | 参考訳 |
| シングルCPU / マルチCPU / 二重化CPU | Single CPU / Multiple CPU / Redundant CPU | 1023(0x3FF) / 992〜995 / 976(0x3D0) | 参考訳 |
| 接続号機 / 管理CPU / 制御系 | Connected CPU No. / Control CPU / Control system | — | 参考訳 |
| I/Oアドレス | I/O address | 先頭No.÷16 | 参考訳 |
| マルチドロップチャネルNo. | Multidrop channel No. | ActMultiDropChannelNumber | 参考訳 |
| 局番⇔IP関連情報 / 局番⇔IP関連情報設定方式 | Station No.↔IP information / setting method | — | 参考訳 |
| 自動応答方式 / IPアドレス算出方式 / テーブル変換方式 / 併用方式 | Automatic response / IP address computation / Table conversion / Combined method | — | 参考訳 |
| パソコン側COMポート番号 | PC side COM port number | ActPortNumber | 参考訳 |
| 使用ケーブルによる | Depends on the cable used | ActControl | 参考訳 |
| リトライ回数 | Number of retries | ActMultiDropChannelNumber(ロボット) | 参考訳 |
| 有手順/無手順 | Procedural / Non-procedural | ActThroughNetworkType(ロボット) | 参考訳 |
| 受信タイムアウト時間 / 送信タイムアウト時間 | Receive timeout / Send timeout | ActTimeOut / ActCpuTimeOut | 参考訳 |
| ユーティリティ設定タイプ / プログラム設定タイプ | Utility setting type / Program setting type | — | 参考訳 |

## 変換範囲表

| 原本ページ(PDF) | 印刷ページ | 節 | 扱い |
|---|---|---|---|
| p.265-267 | 263-265 | 10.2 接続局がEthernetアダプタのEthernet通信(TCP)(1)(2) | 全文(構成図は文章化) |
| p.268-272 | 266-270 | 10.2 接続局がEthernetアダプタのEthernet通信(UDP)(1)(2)(3) | 全文(構成図は文章化) |
| p.273 | 271 | 10.2 接続局がロボットコントローラのEthernet通信 | 全文(構成図は文章化) |
| p.274-279 | 272-277 | 10.2 接続局がCC-Link IE TSNユニットのEthernet通信(TCP)(UDP) | 全文(構成図は文章化) |
| p.280-293 | 278-291 | 10.3 CPU COM通信(FX5CPU / QCPU(Qモード) / LCPU / QモーションCPU / FXCPU / インバータ / ロボットコントローラ) | 全文(構成図は文章化) |
| p.192-264 | 190-262 | 10.1 シリアルコミュニケーション通信，10.2 Ethernet通信の前半 | 別ファイル(10-1〜10-3) |
| p.294-417 | 292-415 | 10.4〜10.16 | 別ファイル(10-5〜10-9) |
| p.1-191，p.418-696 | — | 10章以外 | 別ファイル / **未変換**(進捗docを参照) |

## 目次

- 10.2 Ethernet通信(続き)
  - 接続局がEthernetアダプタのEthernet通信(TCP)(1) — 接続先CPUがFXCPU
  - 接続局がEthernetアダプタのEthernet通信(TCP)(2) — 接続先CPUがFX5CPU
  - 接続局がEthernetアダプタのEthernet通信(UDP)(1) — 接続先CPUがFXCPU
  - 接続局がEthernetアダプタのEthernet通信(UDP)(2) — 接続先CPUがFX5CPU
  - 接続局がEthernetアダプタのEthernet通信(UDP)(3) — 接続先CPUがFX5CPUで直結通信
  - 接続局がロボットコントローラのEthernet通信
  - 接続局がCC-Link IE TSNユニットのEthernet通信(TCP)
  - 接続局がCC-Link IE TSNユニットのEthernet通信(UDP)
- 10.3 CPU COM通信
  - 接続局がFX5CPU / QCPU(Qモード) / LCPU / QモーションCPU / FXCPU / インバータ / ロボットコントローラのCPU COM通信

---

## 10.2 Ethernet通信(続き) (10.2 / 263-277 / 原本 p.265-279)

### 接続局がEthernetアダプタのEthernet通信(TCP)(1) (10.2 / 263 / 原本 p.265)

接続先CPUがFXCPUの場合

#### 構成 (10.2 / 263 / 原本 p.265)

【図】構成 (10.2 / 263 / 原本 p.265)
- パソコン ― Ethernetアダプタ ― 接続局CPU ― 経由ユニット ―(経由ネットワーク)― 経由ユニット ― 経由局CPU

#### アクセス可否およびプロパティのパターン (10.2 / 263 / 原本 p.265)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU FXCPU | 経由ネットワーク | 経由局CPU RCPU | 経由局CPU RCCPU | 経由局CPU RモーションCPU | 経由局CPU LHCPU | 経由局CPU FX5CPU |
|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × |
| ○(1)*1 | CC IE Control<br>CC IE Field | × | × | × | × | × |
| ○(1)*1 | MELSECNET/H | × | × | × | × | × |
| ○(1)*1 | Ethernet | × | × | × | × | × |
| ○(1)*1 | シリアルコミュニケーション | × | × | × | × | × |
| ○(1)*1 | CC-Link | × | × | × | × | × |

| 接続局CPU FXCPU | 経由ネットワーク | 経由局CPU QCPU(Qモード) | 経由局CPU QCCPU | 経由局CPU LCPU | 経由局CPU QSCPU | 経由局CPU QモーションCPU | 経由局CPU FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × | × |
| ○(1)*1 | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
| ○(1)*1 | MELSECNET/H | × | × | × | × | × | × |
| ○(1)*1 | Ethernet | × | × | × | × | × | × |
| ○(1)*1 | シリアルコミュニケーション | × | × | × | × | × | × |
| ○(1)*1 | CC-Link | × | × | × | × | × | × |

> *1 FX3SCPU，FX3G(C)CPU，FX3U(C)CPUのみアクセス可能です。

#### プロパティ一覧 (10.2 / 263 / 原本 p.265)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | プロパティのパターン ○(1) |
|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ |
| ActHostAddress | 1.1.1.1 | 接続局側ユニットのホスト名かIPアドレス |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_TCPIP |
| ActTimeOut | 10000 | ms単位でユーザ任意 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_FXETHER |

### 接続局がEthernetアダプタのEthernet通信(TCP)(2) (10.2 / 264 / 原本 p.266)

接続先CPUがFX5CPUの場合

#### 構成 (10.2 / 264 / 原本 p.266)

【図】構成 (10.2 / 264 / 原本 p.266)
- パソコン ― Ethernetアダプタ ― 接続局CPU ― 経由ユニット ―(経由ネットワーク)― 経由ユニット ― 経由局CPU

#### アクセス可否およびプロパティのパターン (10.2 / 264 / 原本 p.266)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU FX5CPU | 経由ネットワーク | 経由局CPU RCPU | 経由局CPU RCCPU | 経由局CPU RモーションCPU | 経由局CPU LHCPU | 経由局CPU FX5CPU |
|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × |
| ○(1)*1 | CC IE Control<br>CC IE Field | × | × | × | × | × |
| ○(1)*1 | MELSECNET/H | × | × | × | × | × |
| ○(1)*1 | Ethernet | × | × | × | × | × |
| ○(1)*1 | シリアルコミュニケーション | × | × | × | × | × |
| ○(1)*1 | CC-Link | × | × | × | × | × |

| 接続局CPU FX5CPU | 経由ネットワーク | 経由局CPU QCPU(Qモード) | 経由局CPU QCCPU | 経由局CPU LCPU | 経由局CPU QSCPU | 経由局CPU QモーションCPU | 経由局CPU FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × | × |
| ○(1)*1 | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
| ○(1)*1 | MELSECNET/H | × | × | × | × | × | × |
| ○(1)*1 | Ethernet | × | × | × | × | × | × |
| ○(1)*1 | シリアルコミュニケーション | × | × | × | × | × | × |
| ○(1)*1 | CC-Link | × | × | × | × | × | × |

> *1 FX5UCPU，FX5UJCPUのみアクセス可能です。

#### プロパティ一覧 (10.2 / 264-265 / 原本 p.266-267)

※表は原本p.266〜p.267の2ページにまたがる(ActPortNumber以降がp.267)。

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | プロパティのパターン ○(1) |
|---|---|---|
| ActConnectUnitNumber | 0(0x00) | 0(0x00)固定 |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 |
| ActDestinationPortNumber | 0(0x00) | 5554固定 |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 |
| ActHostAddress | 1.1.1.1 | 接続局側ユニットのホスト名またはIPアドレス |
| ActIONumber | 1023(0x3FF) | 1023(0x3FF)固定 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_TCPIP |
| ActPacketType | 0x01(PACKET_PLC1) | PACKET_PLC1固定 |
| ActPortNumber | 1(PORT_1) | 0(0x00)固定 |
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 |
| ActParity | 1(ODD_PARITY) | 0(0x00)固定 |
| ActTimeOut | 10000 | ms単位でユーザ任意 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_FXVENET |

### 接続局がEthernetアダプタのEthernet通信(UDP)(1) (10.2 / 266 / 原本 p.268)

接続先CPUがFXCPUの場合

#### 構成 (10.2 / 266 / 原本 p.268)

【図】構成 (10.2 / 266 / 原本 p.268)
- パソコン ― Ethernetアダプタ ― 接続局CPU ― 経由ユニット ―(経由ネットワーク)― 経由ユニット ― 経由局CPU

#### アクセス可否およびプロパティのパターン (10.2 / 266 / 原本 p.268)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU FXCPU | 経由ネットワーク | 経由局CPU RCPU | 経由局CPU RCCPU | 経由局CPU RモーションCPU | 経由局CPU LHCPU | 経由局CPU FX5CPU |
|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × |
| ○(1)*1 | CC IE Control<br>CC IE Field | × | × | × | × | × |
| ○(1)*1 | MELSECNET/H | × | × | × | × | × |
| ○(1)*1 | Ethernet | × | × | × | × | × |
| ○(1)*1 | シリアルコミュニケーション | × | × | × | × | × |
| ○(1)*1 | CC-Link | × | × | × | × | × |

| 接続局CPU FXCPU | 経由ネットワーク | 経由局CPU QCPU(Qモード) | 経由局CPU QCCPU | 経由局CPU LCPU | 経由局CPU QSCPU | 経由局CPU QモーションCPU | 経由局CPU FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × | × |
| ○(1)*1 | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
| ○(1)*1 | MELSECNET/H | × | × | × | × | × | × |
| ○(1)*1 | Ethernet | × | × | × | × | × | × |
| ○(1)*1 | シリアルコミュニケーション | × | × | × | × | × | × |
| ○(1)*1 | CC-Link | × | × | × | × | × | × |

> *1 FX3SCPU，FX3G(C)CPU，FX3U(C)CPUのみアクセス可能です。

#### プロパティ一覧 (10.2 / 266 / 原本 p.268)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | プロパティのパターン ○(1) |
|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_UDPIP |
| ActTimeOut | 10000 | ms単位でユーザ任意 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_FXETHER_DIRECT |

### 接続局がEthernetアダプタのEthernet通信(UDP)(2) (10.2 / 267 / 原本 p.269)

接続先CPUがFX5CPUの場合

#### 構成 (10.2 / 267 / 原本 p.269)

【図】構成 (10.2 / 267 / 原本 p.269)
- パソコン ― Ethernetアダプタ ― 接続局CPU ― 経由ユニット ―(経由ネットワーク)― 経由ユニット ― 経由局CPU

#### アクセス可否およびプロパティのパターン (10.2 / 267 / 原本 p.269)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU FX5CPU | 経由ネットワーク | 経由局CPU RCPU | 経由局CPU RCCPU | 経由局CPU RモーションCPU | 経由局CPU LHCPU | 経由局CPU FX5CPU |
|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × |
| ○(1)*1 | CC IE Control<br>CC IE Field | × | × | × | × | × |
| ○(1)*1 | MELSECNET/H | × | × | × | × | × |
| ○(1)*1 | Ethernet | × | × | × | × | × |
| ○(1)*1 | シリアルコミュニケーション | × | × | × | × | × |
| ○(1)*1 | CC-Link | × | × | × | × | × |

| 接続局CPU FX5CPU | 経由ネットワーク | 経由局CPU QCPU(Qモード) | 経由局CPU QCCPU | 経由局CPU LCPU | 経由局CPU QSCPU | 経由局CPU QモーションCPU | 経由局CPU FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × | × |
| ○(1)*1 | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
| ○(1)*1 | MELSECNET/H | × | × | × | × | × | × |
| ○(1)*1 | Ethernet | × | × | × | × | × | × |
| ○(1)*1 | シリアルコミュニケーション | × | × | × | × | × | × |
| ○(1)*1 | CC-Link | × | × | × | × | × | × |

> *1 FX5UCPU，FX5UJCPUのみアクセス可能です。

#### プロパティ一覧 (10.2 / 267-268 / 原本 p.269-270)

※表は原本p.269〜p.270の2ページにまたがる(ActPortNumber以降がp.270)。ActDestinationPortNumberとActDestinationIONumberの並び順は原本どおり(TCP(2)と逆順)。

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | プロパティのパターン ○(1) |
|---|---|---|
| ActConnectUnitNumber | 0(0x00) | 0(0x00)固定 |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ |
| ActDestinationPortNumber | 0(0x00) | 5555固定 |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 |
| ActHostAddress | 1.1.1.1 | 接続局側ユニットのホスト名またはIPアドレス |
| ActIONumber | 1023(0x3FF) | 1023(0x3FF)固定 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_UDPIP |
| ActPacketType | 0x01(PACKET_PLC1) | PACKET_PLC1固定 |
| ActPortNumber | 1(PORT_1) | 0(0x00)固定 |
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 |
| ActParity | 1(ODD_PARITY) | 0(0x00)固定 |
| ActTimeOut | 10000 | ms単位でユーザ任意 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_FXVENET |

### 接続局がEthernetアダプタのEthernet通信(UDP)(3) (10.2 / 269 / 原本 p.271)

接続先CPUがFX5CPUで直結通信の場合

#### 構成 (10.2 / 269 / 原本 p.271)

【図】構成 (10.2 / 269 / 原本 p.271)
- パソコン ― Ethernetアダプタ ― 接続局CPU ― 経由ユニット ―(経由ネットワーク)― 経由ユニット ― 経由局CPU

#### アクセス可否およびプロパティのパターン (10.2 / 269 / 原本 p.271)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU FX5CPU | 経由ネットワーク | 経由局CPU RCPU | 経由局CPU RCCPU | 経由局CPU RモーションCPU | 経由局CPU LHCPU | 経由局CPU FX5CPU |
|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × |
| ○(1)*1 | CC IE Control<br>CC IE Field | × | × | × | × | × |
| ○(1)*1 | MELSECNET/H | × | × | × | × | × |
| ○(1)*1 | Ethernet | × | × | × | × | × |
| ○(1)*1 | シリアルコミュニケーション | × | × | × | × | × |
| ○(1)*1 | CC-Link | × | × | × | × | × |

| 接続局CPU FX5CPU | 経由ネットワーク | 経由局CPU QCPU(Qモード) | 経由局CPU QCCPU | 経由局CPU LCPU | 経由局CPU QSCPU | 経由局CPU QモーションCPU | 経由局CPU FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × | × |
| ○(1)*1 | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
| ○(1)*1 | MELSECNET/H | × | × | × | × | × | × |
| ○(1)*1 | Ethernet | × | × | × | × | × | × |
| ○(1)*1 | シリアルコミュニケーション | × | × | × | × | × | × |
| ○(1)*1 | CC-Link | × | × | × | × | × | × |

> *1 FX5UCPU，FX5UJCPUのみアクセス可能です。

#### プロパティ一覧 (10.2 / 269-270 / 原本 p.271-272)

※表は原本p.271〜p.272の2ページにまたがる(ActPortNumber以降がp.272)。原本のUDP(3)の表には ActPacketType 行は無い。

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | プロパティのパターン ○(1) |
|---|---|---|
| ActConnectUnitNumber | 0(0x00) | 0(0x00)固定 |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 |
| ActDestinationPortNumber | 0(0x00) | 5552固定 |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 |
| ActHostAddress | 1.1.1.1 | 255.255.255.255<br>PC側のアダプタ選択を行う場合には，接続先IPアドレスの後にタブ文字とパソコン側IPアドレスを付与する |
| ActIONumber | 1023(0x3FF) | 1023(0x3FF)固定 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_UDPIP |
| ActPortNumber | 1(PORT_1) | 0(0x00)固定 |
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 |
| ActParity | 1(ODD_PARITY) | 0(0x00)固定 |
| ActTimeOut | 10000 | ms単位でユーザ任意 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_FXVENET_DIRECT |

### 接続局がロボットコントローラのEthernet通信 (10.2 / 271 / 原本 p.273)

#### 構成 (10.2 / 271 / 原本 p.273)

【図】構成 (10.2 / 271 / 原本 p.273)
- パソコン ― ロボットコントローラ(直接接続)

#### プロパティ一覧 (10.2 / 271 / 原本 p.273)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | プロパティのパターン |
|---|---|---|
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | RC_PROTOCOL_TCPIP(0x02) |
| ActCpuType | 34(CPU_Q02CPU) | ロボットコントローラ機種(0x013001) |
| ActPortNumber | 1(PORT_1) | 接続するポート番号(通常は10001を指定) |
| ActHostAddress | 1.1.1.1 | ロボットコントローラのホスト名またはIPアドレス |
| ActTimeOut | 10000 | ms単位でユーザ任意 |
| ActCpuTimeOut | 0(0x00) | ms単位でユーザ任意 |
| ActMultiDropChannelNumber | 8(TRC_DTR_OR_RTS) | リトライ回数 |
| ActMxUnitSeries | 0(0x00) | 2(0x02) |

※ActMultiDropChannelNumberのデフォルト値「8(TRC_DTR_OR_RTS)」は原本表記のまま(要確認: 他の節では ActMultiDropChannelNumber のデフォルト値は 0(0x00)。ActControl のデフォルト値と同じ表記になっている)。

> **Point**
> ロボットコントローラ通信時は，プログラム設定タイプのコントロールは使用できません。
> ユーティリティ設定タイプのコントロールを使用してください。

### 接続局がCC-Link IE TSNユニットのEthernet通信(TCP) (10.2 / 272-274 / 原本 p.274-276)

#### 構成 (10.2 / 272 / 原本 p.274)

【図】構成 (10.2 / 272 / 原本 p.274)
- パソコン ― CC-Link IE TSNユニット(接続局CPUと同じベース上) ― 接続局CPU ― 経由ユニット ―(経由ネットワーク)― 経由ユニット ― 経由局CPU

#### アクセス可否およびプロパティのパターン (10.2 / 272 / 原本 p.274)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU RCPU | 経由ネットワーク | 経由局CPU RCPU | 経由局CPU RCCPU | 経由局CPU RモーションCPU | 経由局CPU LHCPU | 経由局CPU FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | ○(2) | × | × | × | × |
| ○(1) | CC IE Control<br>CC IE Field | × | × | × | × | × |
| ○(1) | MELSECNET/H | × | × | × | × | × |
| ○(1) | Ethernet | × | × | × | × | × |
| ○(1) | シリアルコミュニケーション | ○(3) | × | × | × | × |
| ○(1) | CC-Link | ○(4) | × | × | × | × |

| 接続局CPU RCPU | 経由ネットワーク | 経由局CPU QCPU(Qモード) | 経由局CPU QCCPU | 経由局CPU LCPU | 経由局CPU QSCPU | 経由局CPU QモーションCPU | 経由局CPU FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
| ○(1) | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
| ○(1) | MELSECNET/H | × | × | × | × | × | × |
| ○(1) | Ethernet | × | × | × | × | × | × |
| ○(1) | シリアルコミュニケーション | × | × | × | × | × | × |
| ○(1) | CC-Link | × | × | × | × | × | × |

#### プロパティ一覧 (10.2 / 273-274 / 原本 p.275-276)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | パターン ○(1) | パターン ○(2) | パターン ○(3) | パターン ○(4) |
|---|---|---|---|---|---|
| ActConnectUnitNumber | 0(0x00) | 0(0x00)固定 | 接続局側ユニット局番 | 0(0x00)固定 | 0(0x00)固定 |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDestinationIONumber*1 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) |
| ActDestinationPortNumber | 0(0x00) | 5002 | 5002 | 5002 | 5002 |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActHostAddress | 1.1.1.1 | 接続局側ユニットのホスト名またはIPアドレス | 接続局側ユニットのホスト名またはIPアドレス | 接続局側ユニットのホスト名またはIPアドレス | 接続局側ユニットのホスト名またはIPアドレス |
| ActIONumber*1 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 接続局側経由ユニットI/Oアドレス | 接続局側経由ユニットI/Oアドレス |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber*3*4 | 0(0x00) | 対象局側ユニットネットワークNo. | 対象局側ユニットネットワークNo. | 接続局側CC-Link IE TSNユニットネットワークNo. | 接続局側CC-Link IE TSNユニットネットワークNo. |
| ActPassword | あき | 接続局側のCC-Link IE TSNユニットに設定されたパスワード | 接続局側のCC-Link IE TSNユニットに設定されたパスワード | 接続局側のCC-Link IE TSNユニットに設定されたパスワード | 接続局側のCC-Link IE TSNユニットに設定されたパスワード |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_TCPIP | PROTOCOL_TCPIP | PROTOCOL_TCPIP | PROTOCOL_TCPIP |
| ActPortNumber*5 | 1(PORT_1) | パソコン側ポート番号 | パソコン側ポート番号 | パソコン側ポート番号 | パソコン側ポート番号 |
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActParity | 1(ODD_PARITY) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActSourceNetworkNumber | 0(0x00) | パソコン側ネットワークNo. | パソコン側ネットワークNo. | パソコン側ネットワークNo. | パソコン側ネットワークNo. |
| ActSourceStationNumber*6 | 0(0x00) | パソコン側局番 | パソコン側局番 | パソコン側局番 | パソコン側局番 |
| ActStationNumber*3*4 | 255(0xFF) | 対象局側ユニット局番 | 対象局側ユニット局番 | 接続局側CC-Link IE TSNユニット局番 | 接続局側CC-Link IE TSNユニット局番 |
| ActTimeOut | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_RJ71GN11(0x1006) | UNIT_RJ71GN11(0x1006) | UNIT_RJ71GN11(0x1006) | UNIT_RJ71GN11(0x1006) |

> *1 対象局がモーションコントローラ，ロボットコントローラなどの場合，マルチCPU時の値を設定してください。
> 例: ロボットコントローラが2号機として構成されている場合→"0x3E1"を設定します。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2
> *3 プロパティのパターンが○(1)または○(2)の場合，ActNetworkNumberおよびActStationNumberは対象局側のパラメータで設定した値を指定してください。
> *4 CC-Link IE TSNユニット経由のアクセスは，下記の事項に注意してください。
> · ActNetworkNumber，ActStationNumberは対象局側のCC-Link IE TSNユニットのパラメータ設定で指定した値を指定してください。
> · CC-Link IE TSNユニットのパラメータ設定の「局番⇔IP関連情報」を設定してください。また，設定を行う際，「局番⇔IP関連情報設定方式」は自動応答方式以外(IPアドレス算出方式，テーブル変換方式，併用方式のいずれか)を指定してください。
> *5 下記を指定してください。
> 0: パソコン内の空きポート番号を自動で割り当てます。
> 0以外の場合，Close関数実行後，再度Open関数実行時に，エラーが発生する場合があります。
> エラーが発生する場合は，Close関数実行後，時間をおいてOpen関数を実行してください。
> *6 Ethernetの同一ループ内でのCC-Link IE TSNユニットに設定した局番と重複しないように，パソコン側の局番を指定してください。

### 接続局がCC-Link IE TSNユニットのEthernet通信(UDP) (10.2 / 275-277 / 原本 p.277-279)

#### 構成 (10.2 / 275 / 原本 p.277)

【図】構成 (10.2 / 275 / 原本 p.277)
- パソコン ― CC-Link IE TSNユニット(接続局CPUと同じベース上) ― 接続局CPU ― 経由ユニット ―(経由ネットワーク)― 経由ユニット ― 経由局CPU

#### アクセス可否およびプロパティのパターン (10.2 / 275 / 原本 p.277)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU RCPU | 経由ネットワーク | 経由局CPU RCPU | 経由局CPU RCCPU | 経由局CPU RモーションCPU | 経由局CPU LHCPU | 経由局CPU FX5CPU |
|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | ○(2) | × | × | × | × |
| ○(1)*1 | CC IE Control<br>CC IE Field | × | × | × | × | × |
| ○(1)*1 | MELSECNET/H | × | × | × | × | × |
| ○(1)*1 | Ethernet | × | × | × | × | × |
| ○(1)*1 | シリアルコミュニケーション | ○(3) | × | × | × | × |
| ○(1)*1 | CC-Link | ○(4) | × | × | × | × |

| 接続局CPU RCPU | 経由ネットワーク | 経由局CPU QCPU(Qモード) | 経由局CPU QCCPU | 経由局CPU LCPU | 経由局CPU QSCPU | 経由局CPU QモーションCPU | 経由局CPU FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × | × |
| ○(1)*1 | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
| ○(1)*1 | MELSECNET/H | × | × | × | × | × | × |
| ○(1)*1 | Ethernet | × | × | × | × | × | × |
| ○(1)*1 | シリアルコミュニケーション | × | × | × | × | × | × |
| ○(1)*1 | CC-Link | × | × | × | × | × | × |

> *1 CC-Link IE TSNユニットへの直結接続によるアクセスは未サポートです。

#### プロパティ一覧 (10.2 / 276-277 / 原本 p.278-279)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | パターン ○(1) | パターン ○(2) | パターン ○(3) | パターン ○(4) |
|---|---|---|---|---|---|
| ActConnectUnitNumber | 0(0x00) | 0(0x00)固定 | 接続局側ユニット局番 | 0(0x00)固定 | 0(0x00)固定 |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDestinationIONumber*1 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) |
| ActDestinationPortNumber | 0(0x00) | 5001 | 5001 | 5001 | 5001 |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActHostAddress | 1.1.1.1 | 接続局側ユニットのホスト名またはIPアドレス | 接続局側ユニットのホスト名またはIPアドレス | 接続局側ユニットのホスト名またはIPアドレス | 接続局側ユニットのホスト名またはIPアドレス |
| ActIONumber*1 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 接続局側経由ユニットI/Oアドレス | 接続局側経由ユニットI/Oアドレス |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber*3*4 | 0(0x00) | 対象局側ユニットネットワークNo. | 対象局側ユニットネットワークNo. | 接続局側CC-Link IE TSNユニットネットワークNo. | 接続局側CC-Link IE TSNユニットネットワークNo. |
| ActPassword | あき | 接続局側のCC-Link IE TSNユニットに設定されたパスワード | 接続局側のCC-Link IE TSNユニットに設定されたパスワード | 接続局側のCC-Link IE TSNユニットに設定されたパスワード | 接続局側のCC-Link IE TSNユニットに設定されたパスワード |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_UDPIP | PROTOCOL_UDPIP | PROTOCOL_UDPIP | PROTOCOL_UDPIP |
| ActPortNumber*5 | 1(PORT_1) | IPアドレス指定通信時: パソコン側ポート番号 | IPアドレス指定通信時: パソコン側ポート番号 | IPアドレス指定通信時: パソコン側ポート番号 | IPアドレス指定通信時: パソコン側ポート番号 |
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActParity | 1(ODD_PARITY) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActSourceNetworkNumber | 0(0x00) | パソコン側ネットワークNo. | パソコン側ネットワークNo. | パソコン側ネットワークNo. | パソコン側ネットワークNo. |
| ActSourceStationNumber*6 | 0(0x00) | パソコン側局番 | パソコン側局番 | パソコン側局番 | パソコン側局番 |
| ActStationNumber*3*4 | 255(0xFF) | 対象局側ユニット局番 | 対象局側ユニット局番 | 接続局側CC-Link IE TSNユニット局番 | 接続局側CC-Link IE TSNユニット局番 |
| ActTimeOut | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_RJ71GN11(0x1006) | UNIT_RJ71GN11(0x1006) | UNIT_RJ71GN11(0x1006) | UNIT_RJ71GN11(0x1006) |

> *1 対象局がモーションコントローラ，ロボットコントローラなどの場合，マルチCPU時の値を設定してください。
> 例: ロボットコントローラが2号機として構成されている場合→"0x3E1"を設定します。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2
> *3 プロパティのパターンが○(1)または○(2)の場合，ActNetworkNumberおよびActStationNumberは対象局側のパラメータで設定した値を指定してください。
> *4 CC-Link IE TSNユニット経由のアクセスは，下記の事項に注意してください。
> · ActNetworkNumber，ActStationNumberは対象局側のCC-Link IE TSNユニットのパラメータ設定で指定した値を指定してください。
> · CC-Link IE TSNユニットのパラメータ設定の「局番⇔IP関連情報」を設定してください。また，設定を行う際，「局番⇔IP関連情報設定方式」は自動応答方式以外(IPアドレス算出方式，テーブル変換方式，併用方式のいずれか)を指定してください。
> *5 接続局側CC-Link IE TSNユニットのEthernetパラメータ設定内容が「自動応答方式」以外の場合，5001固定で指定してください。
> 接続局側CC-Link IE TSNユニットのEthernetパラメータ設定内容が「自動応答方式」の場合，下記を指定してください。
> 0: パソコン内の空きポート番号を自動で割り当てます。
> 0以外: 指定ポート番号を使用してUDPソケットを生成します。
> *6 Ethernetの同一ループ内でのCC-Link IE TSNユニットに設定した局番と重複しないように，パソコン側の局番を指定してください。

※アクセス可否表の脚注*1(直結接続未サポート)とプロパティ一覧の脚注*1(マルチCPU時の値)は原本でも同じ番号で別内容。

---

## 10.3 CPU COM通信 (10.3 / 278-291 / 原本 p.280-293)

### 接続局がFX5CPUのCPU COM通信 (10.3 / 278-279 / 原本 p.280-281)

#### 構成 (10.3 / 278 / 原本 p.280)

【図】構成 (10.3 / 278 / 原本 p.280)
- パソコン ― 接続局CPU(CPUユニットのRS-232/RS-422コネクタ) ― 経由ユニット ―(経由ネットワーク)― 経由ユニット ― 経由局CPU

#### アクセス可否およびプロパティのパターン (10.3 / 278 / 原本 p.280)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU FX5CPU | 経由ネットワーク | 経由局CPU RCPU | 経由局CPU RCCPU | 経由局CPU RモーションCPU | 経由局CPU LHCPU | 経由局CPU FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × |
| ○(1) | CC IE Control<br>CC IE Field | × | × | × | × | ○(2)*1*2 |
| ○(1) | MELSECNET/H | × | × | × | × | × |
| ○(1) | Ethernet | × | × | × | × | × |
| ○(1) | シリアルコミュニケーション | × | × | × | × | × |
| ○(1) | CC-Link | × | × | × | × | ○(3)*2 |

| 接続局CPU FX5CPU | 経由ネットワーク | 経由局CPU QCPU(Qモード) | 経由局CPU QCCPU | 経由局CPU LCPU | 経由局CPU QSCPU | 経由局CPU QモーションCPU | 経由局CPU FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
| ○(1) | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
| ○(1) | MELSECNET/H | × | × | × | × | × | × |
| ○(1) | Ethernet | × | × | × | × | × | × |
| ○(1) | シリアルコミュニケーション | × | × | × | × | × | × |
| ○(1) | CC-Link | × | × | × | × | × | × |

> *1 CC-Link IEフィールドネットワークのみアクセス可能です。
> *2 FX5SCPUにはアクセスできません。

#### プロパティ一覧 (10.3 / 279 / 原本 p.281)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | パターン ○(1) | パターン ○(2) | パターン ○(3) |
|---|---|---|---|---|
| ActBaudRate | 19200(BAUDRATE_19200) | BAUDRATE_9600，BAUDRATE_19200，BAUDRATE_38400，BAUDRATE_57600，BAUDRATE_115200 | BAUDRATE_9600，BAUDRATE_19200，BAUDRATE_38400，BAUDRATE_57600，BAUDRATE_115200 | BAUDRATE_9600，BAUDRATE_19200，BAUDRATE_38400，BAUDRATE_57600，BAUDRATE_115200 |
| ActControl | 8(TRC_DTR_OR_RTS) | 使用ケーブルによる | 使用ケーブルによる | 使用ケーブルによる |
| ActCpuTimeOut | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDataBits | 8(DATABIT_8) | 8(DATABIT_8)固定 | 8(DATABIT_8)固定 | 8(DATABIT_8)固定 |
| ActDestinationPortNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 1023(0x3FF) |
| ActDidPropertyBit | 1(0x01) | 0(0x00)固定 | 1(0x01)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 0(0x00)固定 | 1(0x01)固定 | 0(0x00)固定 |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 1(0x01) |
| ActIONumber | 1023(0x3FF) | 1023(0x3FF)固定 | 1023(0x3FF)固定 | 接続局ユニット番号 |
| ActMultiDropChannelNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニットネットワークNo. | 0(0x00)固定 |
| ActParity | 1(ODD_PARITY) | 1(ODD_PARITY)固定 | 1(ODD_PARITY)固定 | 1(ODD_PARITY)固定 |
| ActPassword | あき | NULL | NULL | NULL |
| ActPortNumber | 1(PORT_1) | パソコン側COMポート番号 | パソコン側COMポート番号 | パソコン側COMポート番号 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_SERIAL(0x04) | PROTOCOL_SERIAL(0x04) | PROTOCOL_SERIAL(0x04) |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 対象局側ユニット局番 | 255(0xFF)固定 |
| ActSourceNetworkNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActSourceStationNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActStopBits | 0(STOPBIT_ONE) | 0(STOPBIT_ONE)固定 | 0(STOPBIT_ONE)固定 | 0(STOPBIT_ONE)固定 |
| ActSumCheck | 0(NO_SUM_CHECK) | 0(NO_SUM_CHECK)固定 | 0(NO_SUM_CHECK)固定 | 0(NO_SUM_CHECK)固定 |
| ActHostAddress | 1.1.1.1 | NULL | NULL | NULL |
| ActTargetSimulator | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActThroughNetworkType | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActTimeOut | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_FXVCPU(0x2000) | UNIT_FXVCPU(0x2000) | UNIT_FXVCPU(0x2000) |

### 接続局がQCPU(Qモード)のCPU COM通信 (10.3 / 280-282 / 原本 p.282-284)

#### 構成 (10.3 / 280 / 原本 p.282)

【図】構成 (10.3 / 280 / 原本 p.282)
- パソコン ― 接続局CPU(CPUユニットのRS-232/RS-422コネクタ) ― 経由ユニット ―(経由ネットワーク)― 経由ユニット ― 経由局CPU

#### アクセス可否およびプロパティのパターン (10.3 / 280 / 原本 p.282)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU QCPU(Qモード) | 接続局CPU QCCPU | 経由ネットワーク | 経由局CPU RCPU | 経由局CPU RCCPU | 経由局CPU RモーションCPU | 経由局CPU LHCPU | 経由局CPU FX5CPU |
|---|---|---|---|---|---|---|---|
| ○(1) | ○(1)*4 | CC IE TSN | × | × | × | × | × |
| ○(1) | ○(1)*4 | CC IE Control<br>CC IE Field | × | × | × | × | × |
| ○(1) | ○(1)*4 | MELSECNET/H | × | × | × | × | × |
| ○(1) | ○(1)*4 | Ethernet | × | × | × | × | × |
| ○(1) | ○(1)*4 | シリアルコミュニケーション | × | × | × | × | × |
| ○(1) | ○(1)*4 | CC-Link | × | × | × | × | × |

| 接続局CPU QCPU(Qモード) | 接続局CPU QCCPU | 経由ネットワーク | 経由局CPU QCPU(Qモード) | 経由局CPU QCCPU | 経由局CPU LCPU | 経由局CPU QSCPU | 経由局CPU QモーションCPU | 経由局CPU FXCPU |
|---|---|---|---|---|---|---|---|---|
| ○(1) | ○(1)*4 | CC IE TSN | × | × | × | × | × | × |
| ○(1) | ○(1)*4 | CC IE Control<br>CC IE Field | ○(2) | ○(2)*1 | ○(2)*2 | ○(2)*1 | ○(2)*1 | × |
| ○(1) | ○(1)*4 | MELSECNET/H | ○(2) | ○(2) | × | ○(2) | ○(2) | × |
| ○(1) | ○(1)*4 | Ethernet | ○(2) | × | × | ○(2) | ○(2) | × |
| ○(1) | ○(1)*4 | シリアルコミュニケーション | ○(3)*5 | × | ○(3) | × | ○(3) | × |
| ○(1) | ○(1)*4 | CC-Link | ○(4) | ○(4) | ○(4) | × | ○(4) | ○(4)*3 |

> *1 RモーションCPU，Q12DCCPU-V(基本機能モード)，QSCPU，QモーションCPUは，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。
> *2 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
> *3 FX3G(C)CPU，FX3U(C)CPUかつ自ネットワークのみサポートしています。
> *4 マルチCPU構成時の，2号機以降の場合のみアクセス可能です。
> *5 二重化CPUの場合，基本ベースユニット上にあるシリアルコミュニケーションユニットにはアクセスできません。

#### プロパティ一覧 (10.3 / 281-282 / 原本 p.283-284)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

※パターン(2)の列見出しは原本では「○(2)*1」(脚注*1はプロパティ一覧下の*1)。

| プロパティ | デフォルト値 | パターン ○(1) | パターン ○(2) | パターン ○(3) | パターン ○(4) |
|---|---|---|---|---|---|
| ActBaudRate | 19200(BAUDRATE_19200) | BAUDRATE_9600，BAUDRATE_19200，BAUDRATE_38400，BAUDRATE_57600，BAUDRATE_115200 | BAUDRATE_9600，BAUDRATE_19200，BAUDRATE_38400，BAUDRATE_57600，BAUDRATE_115200 | BAUDRATE_9600，BAUDRATE_19200，BAUDRATE_38400，BAUDRATE_57600，BAUDRATE_115200 | BAUDRATE_9600，BAUDRATE_19200，BAUDRATE_38400，BAUDRATE_57600，BAUDRATE_115200 |
| ActControl | 8(TRC_DTR_OR_RTS) | 使用ケーブルによる | 使用ケーブルによる | 使用ケーブルによる | 使用ケーブルによる |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局<br>• QCPU(Qモード)，LCPU: 1(0x01)<br>• 上記以外: 0(0x00) | 対象局<br>• QCPU(Qモード)，QCCPU，LCPU: 1(0x01)<br>• 上記以外: 0(0x00) |
| ActIONumber*2 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 接続局側ユニットI/Oアドレス | 接続局側ユニットI/Oアドレス |
| ActMultiDropChannelNumber*3 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニットネットワークNo. | 0(0x00)固定 | 0(0x00)固定 |
| ActPortNumber | 1(PORT_1) | パソコン側COMポート番号 | パソコン側COMポート番号 | パソコン側COMポート番号 | パソコン側COMポート番号 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_SERIAL(0x04) | PROTOCOL_SERIAL(0x04) | PROTOCOL_SERIAL(0x04) | PROTOCOL_SERIAL(0x04) |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 対象局側ユニット局番 | 255(0xFF)固定 | 255(0xFF)固定 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_QNCPU(0x13) | UNIT_QNCPU(0x13) | UNIT_QNCPU(0x13) | UNIT_QNCPU(0x13) |

> *1 Ethernetユニット(Qシリーズ対応E71)経由のアクセスは，下記の事項に注意してください。
> · ActNetworkNumber，ActStationNumberは，対象局側のQシリーズ対応E71のパラメータ設定で設定した値を指定してください。
> · Qシリーズ対応E71のパラメータ設定の「局番⇔IP関連情報」を設定してください。また，設定を行う際，「局番⇔IP関連情報設定方式」は自動応答方式以外(IPアドレス算出方式，テーブル変換方式，併用方式のいずれか)を指定してください。
> *2 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *3 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2

※プロパティ一覧の脚注*1〜*3は原本 p.284 に記載。

### 接続局がLCPUのCPU COM通信 (10.3 / 283-285 / 原本 p.285-287)

#### 構成 (10.3 / 283 / 原本 p.285)

【図】構成 (10.3 / 283 / 原本 p.285)
- パソコン ― 接続局CPU(CPUユニットのRS-232/RS-422コネクタ) ― 経由ユニット ―(経由ネットワーク)― 経由ユニット ― 経由局CPU

#### アクセス可否およびプロパティのパターン (10.3 / 283 / 原本 p.285)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU LCPU | 経由ネットワーク | 経由局CPU RCPU | 経由局CPU RCCPU | 経由局CPU RモーションCPU | 経由局CPU LHCPU | 経由局CPU FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × |
| ○(1) | CC IE Field*1 | × | × | × | × | × |
| ○(1) | MELSECNET/H | × | × | × | × | × |
| ○(1) | Ethernet | × | × | × | × | × |
| ○(1) | シリアルコミュニケーション | × | × | × | × | × |
| ○(1) | CC-Link | × | × | × | × | × |

| 接続局CPU LCPU | 経由ネットワーク | 経由局CPU QCPU(Qモード) | 経由局CPU QCCPU | 経由局CPU LCPU | 経由局CPU QSCPU | 経由局CPU QモーションCPU | 経由局CPU FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
| ○(1) | CC IE Field*1 | ○(4) | ○(4)*2 | ○(4) | × | × | × |
| ○(1) | MELSECNET/H | × | × | × | × | × | × |
| ○(1) | Ethernet | ○(4) | × | ○(4) | × | × | × |
| ○(1) | シリアルコミュニケーション | ○(2)*3 | × | ○(2) | × | × | × |
| ○(1) | CC-Link | ○(3) | ○(3) | ○(3) | × | × | × |

> *1 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
> *2 Q12DCCPU-V(基本機能モード)は，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。
> *3 二重化CPUの場合，基本ベースユニット上にあるシリアルコミュニケーションユニットにはアクセスできません。

※原本のLCPUの表では経由ネットワークの行が「CC IE Field*1」(CC IE Control の行は無い)。

#### プロパティ一覧 (10.3 / 284-285 / 原本 p.286-287)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

※表は原本p.286〜p.287の2ページにまたがる(ActStopBits以降がp.287)。

| プロパティ | デフォルト値 | パターン ○(1) | パターン ○(2) | パターン ○(3) | パターン ○(4) |
|---|---|---|---|---|---|
| ActBaudRate | 19200(BAUDRATE_19200) | BAUDRATE_9600，BAUDRATE_19200，BAUDRATE_38400，BAUDRATE_57600，BAUDRATE_115200 | BAUDRATE_9600，BAUDRATE_19200，BAUDRATE_38400，BAUDRATE_57600，BAUDRATE_115200 | BAUDRATE_9600，BAUDRATE_19200，BAUDRATE_38400，BAUDRATE_57600，BAUDRATE_115200 | BAUDRATE_9600，BAUDRATE_19200，BAUDRATE_38400，BAUDRATE_57600，BAUDRATE_115200 |
| ActConnectUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActControl | 8(TRC_DTR_OR_RTS) | 使用ケーブルによる | 使用ケーブルによる | 使用ケーブルによる | 使用ケーブルによる |
| ActCpuTimeOut | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDataBits | 8(DATABIT_8) | 8(DATABIT_8)固定 | 8(DATABIT_8)固定 | 8(DATABIT_8)固定 | 8(DATABIT_8)固定 |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 0(0x00)固定 |
| ActDestinationPortNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 | 1(0x01)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 | 1(0x01)固定 |
| ActHostAddress | 1.1.1.1 | NULL固定 | NULL固定 | NULL固定 | NULL固定 |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 対象局<br>• QCPU(Qモード)，LCPU: 1(0x01)<br>• 上記以外: 0(0x00) | 対象局<br>• QCPU(Qモード)，QCCPU，LCPU: 1(0x01)<br>• 上記以外: 0(0x00) | 0(0x00)固定 |
| ActIONumber*1 | 1023(0x3FF) | 1023(0x3FF)固定 | 接続局側ユニットI/Oアドレス | 接続局側ユニットI/Oアドレス | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 | 0(0x00)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニットネットワークNo. |
| ActPacketType | 0x01(PACKET_PLC1) | 0x01(PACKET_PLC1)固定 | 0x01(PACKET_PLC1)固定 | 0x01(PACKET_PLC1)固定 | 0x01(PACKET_PLC1)固定 |
| ActParity | 1(ODD_PARITY) | 1(ODD_PARITY)固定 | 1(ODD_PARITY)固定 | 1(ODD_PARITY)固定 | 1(ODD_PARITY)固定 |
| ActPortNumber | 1(PORT_1) | パソコン側COMポート番号 | パソコン側COMポート番号 | パソコン側COMポート番号 | パソコン側COMポート番号 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_SERIAL(0x04) | PROTOCOL_SERIAL(0x04) | PROTOCOL_SERIAL(0x04) | PROTOCOL_SERIAL(0x04) |
| ActSourceNetworkNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActSourceStationNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 255(0xFF)固定 | 255(0xFF)固定 | 対象局側ユニット局番 |
| ActStopBits | 0(STOPBIT_ONE) | 0(STOPBIT_ONE)固定 | 0(STOPBIT_ONE)固定 | 0(STOPBIT_ONE)固定 | 0(STOPBIT_ONE)固定 |
| ActSumCheck | 0(NO_SUM_CHECK) | 0(NO_SUM_CHECK)固定 | 0(NO_SUM_CHECK)固定 | 0(NO_SUM_CHECK)固定 | 0(NO_SUM_CHECK)固定 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 | 0(0x00)固定 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_LNCPU(0x50) | UNIT_LNCPU(0x50) | UNIT_LNCPU(0x50) | UNIT_LNCPU(0x50) |

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2

※LCPUのアクセス可否表でパターン(2)はシリアルコミュニケーション，(3)はCC-Link，(4)はCC IE Field/Ethernet経由。プロパティ一覧の列(1)〜(4)もこの番号に対応(原本どおり)。

### 接続局がQモーションCPUのCPU COM通信 (10.3 / 286-287 / 原本 p.288-289)

#### 構成 (10.3 / 286 / 原本 p.288)

【図】構成 (10.3 / 286 / 原本 p.288)
- パソコン ― 接続局CPU(CPUユニットのRS-232/RS-422コネクタ) ― 経由ユニット ―(経由ネットワーク)― 経由ユニット ― 経由局CPU

#### アクセス可否およびプロパティのパターン (10.3 / 286 / 原本 p.288)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU QモーションCPU | 経由ネットワーク | 経由局CPU RCPU | 経由局CPU RCCPU | 経由局CPU RモーションCPU | 経由局CPU LHCPU | 経由局CPU FX5CPU |
|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × |
| ○(1)*1 | CC IE Control<br>CC IE Field | × | × | × | × | × |
| ○(1)*1 | MELSECNET/H | × | × | × | × | × |
| ○(1)*1 | Ethernet | × | × | × | × | × |
| ○(1)*1 | シリアルコミュニケーション | × | × | × | × | × |
| ○(1)*1 | CC-Link | × | × | × | × | × |

| 接続局CPU QモーションCPU | 経由ネットワーク | 経由局CPU QCPU(Qモード) | 経由局CPU QCCPU | 経由局CPU LCPU | 経由局CPU QSCPU | 経由局CPU QモーションCPU | 経由局CPU FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × | × |
| ○(1)*1 | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
| ○(1)*1 | MELSECNET/H | × | × | × | × | × | × |
| ○(1)*1 | Ethernet | × | × | × | × | × | × |
| ○(1)*1 | シリアルコミュニケーション | × | × | × | × | × | × |
| ○(1)*1 | CC-Link | × | × | × | × | × | × |

> *1 Q172D，Q173D，Q172DS，Q173DSのみアクセス可能です。

#### プロパティ一覧 (10.3 / 287 / 原本 p.289)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | プロパティのパターン ○(1) |
|---|---|---|
| ActBaudRate | 19200(BAUDRATE_19200) | BAUDRATE_9600，BAUDRATE_19200，BAUDRATE_38400，BAUDRATE_57600，BAUDRATE_115200 |
| ActControl | 8(TRC_DTR_OR_RTS) | 使用ケーブルによる |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ |
| ActIONumber | 1023(0x3FF) | ■マルチCPU時<br>• 管理CPU: 1023(0x3FF)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) |
| ActPortNumber | 1(PORT_1) | パソコン側COMポート番号 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_SERIAL(0x04) |
| ActTimeOut | 10000 | ms単位でユーザ任意 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_QNMOTION(0x1C) |

### 接続局がFXCPUのCPU COM通信 (10.3 / 288-289 / 原本 p.290-291)

#### 構成 (10.3 / 288 / 原本 p.290)

【図】構成 (10.3 / 288 / 原本 p.290)
- パソコン ― 接続局CPU(CPUユニットのRS-232/RS-422コネクタ) ― 経由ユニット ―(経由ネットワーク)― 経由ユニット ― 経由局CPU

#### アクセス可否およびプロパティのパターン (10.3 / 288 / 原本 p.290)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU FXCPU | 経由ネットワーク | 経由局CPU RCPU | 経由局CPU RCCPU | 経由局CPU RモーションCPU | 経由局CPU LHCPU | 経由局CPU FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × |
| ○(1) | CC IE Control<br>CC IE Field | × | × | × | × | × |
| ○(1) | MELSECNET/H | × | × | × | × | × |
| ○(1) | Ethernet | × | × | × | × | × |
| ○(1) | シリアルコミュニケーション | × | × | × | × | × |
| ○(1) | CC-Link | × | × | × | × | × |

| 接続局CPU FXCPU | 経由ネットワーク | 経由局CPU QCPU(Qモード) | 経由局CPU QCCPU | 経由局CPU LCPU | 経由局CPU QSCPU | 経由局CPU QモーションCPU | 経由局CPU FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
| ○(1) | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
| ○(1) | MELSECNET/H | × | × | × | × | × | × |
| ○(1) | Ethernet | × | × | × | × | × | × |
| ○(1) | シリアルコミュニケーション | × | × | × | × | × | × |
| ○(1) | CC-Link | × | × | × | × | × | ○(2)*1 |

> *1 FX3G(C)CPU，FX3U(C)CPUのみアクセス可能です。

#### プロパティ一覧 (10.3 / 289 / 原本 p.291)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | パターン ○(1) | パターン ○(2) |
|---|---|---|---|
| ActBaudRate | 19200(BAUDRATE_19200) | • FX3S，FX3UC，FX3G(C)，FX5U，FX5UJ: (BAUDRATE_9600，BAUDRATE_19200，BAUDRATE_38400，BAUDRATE_57600，BAUDRATE_115200) | • FX3S，FX3UC，FX3G(C)，FX5U，FX5UJ: (BAUDRATE_9600，BAUDRATE_19200，BAUDRATE_38400，BAUDRATE_57600，BAUDRATE_115200) |
| ActControl | 8(TRC_DTR_OR_RTS) | 使用ケーブルによる | 使用ケーブルによる |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 1023(0x3FF) |
| ActDidPropertyBit | 1(0x01) | 0(0x00) | 0(0x00) |
| ActDsidPropertyBit | 1(0x01) | 0(0x00) | 0(0x00) |
| ActIONumber | 1023(0x3FF) | 0(0x00)固定 | 接続局ユニット番号 |
| ActPortNumber | 1(PORT_1) | パソコン側COMポート番号 | パソコン側COMポート番号 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_SERIAL(0x04) | PROTOCOL_SERIAL(0x04) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 対象局ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_FXCPU(0x0F) | UNIT_FXCPU(0x0F) |

※ActBaudRateに「FX5U，FX5UJ」が記載されているのは原本どおり(要確認: 接続局はFXCPUの節)。

### 接続局がインバータのCPU COM通信 (10.3 / 290 / 原本 p.292)

#### 構成 (10.3 / 290 / 原本 p.292)

【図】構成 (10.3 / 290 / 原本 p.292)
- パソコン ― インバータ(直接接続)

#### プロパティ一覧 (10.3 / 290 / 原本 p.292)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | プロパティのパターン |
|---|---|---|
| ActMxUnitSeries | 0(0x00) | 1(0x01) |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | COMM_RS232C(0x00) |
| ActStationNumber | 255(0xFF) | インバータの局番(0～31) |
| ActCpuType | 34(CPU_Q02CPU) | INV_A800(0x1E60) |
| ActPortNumber | 1(PORT_1) | パソコン側COMポート番号 |
| ActBaudRate | 19200(BAUDRATE_19200) | BAUDRATE_4800，BAUDRATE_9600，BAUDRATE_19200，BAUDRATE_38400，BAUDRATE_57600，BAUDRATE_115200 |
| ActTimeOut | 10000 | ms単位でユーザ任意 |
| ActCpuTimeOut | 0(0x00) | 10ms単位でユーザ任意 |
| ActPacketType | 0x01(PACKET_PLC1) | • CRLF_NONE(0): CR/LFなし<br>• CRLF_CR(1): CRのみあり<br>• CRLF_CRLF(2): CR/LFあり |
| ActDataBits | 8(DATABIT_8) | • DATABIT_7<br>• DATABIT_8 |
| ActParity | 1(ODD_PARITY) | • NO_PARRITY<br>• ODD_PARITY<br>• EVEN_PARITY |
| ActStopBits | 0(STOPBIT_ONE) | • STOPBIT_ONE<br>• STOPBIT_TWO |

※「NO_PARRITY」「STOPBIT_TWO」は原本表記のまま(要確認: 9章の定数名は NO_PARITY / STOPBITS_TWO)。

> **Point**
> インバータ通信時は，プログラム設定タイプのコントロールは使用できません。
> ユーティリティ設定タイプのコントロールを使用してください。

### 接続局がロボットコントローラのCPU COM通信 (10.3 / 291 / 原本 p.293)

#### 構成 (10.3 / 291 / 原本 p.293)

【図】構成 (10.3 / 291 / 原本 p.293)
- パソコン ― ロボットコントローラ(直接接続)

#### プロパティ一覧 (10.3 / 291 / 原本 p.293)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | プロパティのパターン |
|---|---|---|
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | RC_PROTOCOL_SERIAL(0x01) |
| ActCpuType | 34(CPU_Q02CPU) | ロボットコントローラ機種(0x013001) |
| ActPortNumber | 1(PORT_1) | パソコン側COMポート番号 |
| ActBaudRate | 19200(BAUDRATE_19200) | 伝送速度 |
| ActTimeOut | 10000 | 受信タイムアウト時間(msec) |
| ActCpuTimeOut | 0(0x00) | 送信タイムアウト時間(msec) |
| ActDataBits | 8(DATABIT_8) | • DATABIT_7<br>• DATABIT_8 |
| ActParity | 1(ODD_PARITY) | • NO_PARRITY<br>• ODD_PARITY<br>• EVEN_PARITY |
| ActStopBits | 0(STOPBIT_ONE) | • ONESTOPBIT(0)<br>• ONE5STOPBITS(1)<br>• TWOSTOPBITS(2) |
| ActMultiDropChannelNumber | 0(0x00) | リトライ回数 |
| ActThroughNetworkType | 0(0x00) | 有手順/無手順(0/1) |
| ActMxUnitSeries | 0(0x00) | 2(0x02) |

> **Point**
> ロボットコントローラ通信時は，プログラム設定タイプのコントロールは使用できません。
> ユーティリティ設定タイプのコントロールを使用してください。
