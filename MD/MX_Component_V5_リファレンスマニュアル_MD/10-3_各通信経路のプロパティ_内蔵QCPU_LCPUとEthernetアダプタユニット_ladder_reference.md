# MX Component Version 5 リファレンスマニュアル 10章 各通信経路で設定するプロパティ (3/9) p.243-264

| 項目 | 内容 |
|---|---|
| 原本 | 【三菱】MX Component Version 5 リファレンスマニュアル (SH-082394J) |
| メーカー | 三菱電機 |
| 原本ファイル | `PDF/【三菱】MX Component Version 5 リファレンスマニュアル_sh082394j.pdf` (全696ページ) |
| 本ファイルの範囲 | 10.2 Ethernet通信のうち「接続局がEthernetポート内蔵QCPU(TCP)」〜「接続局がEthernetアダプタユニット(UDP)」 (印刷ページ 241-262 / PDF p.243-264) |
| 出典表記 | `(節 / 印刷ページ / 原本 p.PDFページ)` |
| 作成日 | 2026-11-03 |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。
> 本文中の「○ページ」はすべて原本の**印刷ページ番号**です(PDFページ = 印刷ページ + 2)。
> アクセス可否表は原本の2段見出し(接続局CPU/経由局CPU)を「接続局CPU: 〜」「経由局CPU: 〜」の1段見出しに展開しています。各表の先頭列「○(1)」等は接続局CPU自身へのアクセス可否とパターン。

## 主要用語 対訳表 (Glossary)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| 接続局CPU | Connected station CPU | — | 参考訳 |
| 経由局CPU | Relay station CPU | — | 参考訳 |
| 経由ユニット | Relay module | — | 参考訳 |
| 経由ネットワーク | Relay network | CC IE TSN / CC IE Control / CC IE Field / MELSECNET/H / Ethernet / シリアルコミュニケーション / CC-Link | 参考訳 |
| アクセス可否 | Accessibility | ○(n) / × | 参考訳 |
| プロパティのパターン | Property pattern | (1)〜(4) | 参考訳 |
| 対象局 / 対象局側 | Target station / Target station side | — | 参考訳 |
| シングルCPU / マルチCPU / 二重化CPU | Single CPU / Multiple CPU / Redundant CPU | 接続号機・1〜4号機・制御系 | 参考訳 |
| 接続号機 | Connected CPU No. | 1023(0x3FF) | 参考訳 |
| 制御系 | Control system | 976(0x3D0) | 参考訳 |
| I/Oアドレス / I/O先頭No. | I/O address / Start I/O No. | ActIONumber, ActDestinationIONumber | 参考訳 |
| マルチドロップチャネルNo. | Multidrop channel No. | ActMultiDropChannelNumber | 参考訳 |
| ネットワークNo. / 局番 / ユニット局番 | Network No. / Station No. / Module station No. | ActNetworkNumber / ActStationNumber / ActUnitNumber | 参考訳 |
| リモートパスワード | Remote password | ActPassword | 参考訳 |
| ホスト名またはIPアドレス | Host name or IP address | ActHostAddress | 参考訳 |
| IPアドレス指定通信 / IPアドレス指定なし直結通信 | Communication with IP address specified / Direct connection without IP address | UDP時 | 参考訳 |
| Ethernetポート内蔵QCPU / LCPU | Built-in Ethernet port QCPU / LCPU | QnUDE(H)CPU, QnUD(P)VCPU | 参考訳 |
| Ethernetアダプタユニット | Ethernet adapter module | NZ2GF-ETB, UNIT_NZ2GF_ETB(0x59) | 参考訳 |
| CC-Link IEフィールドネットワークユニット | CC-Link IE Field Network module | — | 参考訳 |
| MELSOFT直結接続 / Ethernetポート直結接続 | MELSOFT direct connection / Ethernet port direct connection | — | 参考訳 |
| 基本ベースユニット | Main base unit | — | 参考訳 |
| ユニットタイプ / プロトコルタイプ / パケットタイプ | Unit type / Protocol type / Packet type | ActUnitType / ActProtocolType / ActPacketType | 参考訳 |

## 変換範囲表

| 原本ページ(PDF) | 印刷ページ | 節 | 扱い |
|---|---|---|---|
| p.243-246 | 241-244 | 接続局がEthernetポート内蔵QCPUのEthernet通信(TCP) | 全文 |
| p.247-250 | 245-248 | 接続局がEthernetポート内蔵QCPUのEthernet通信(UDP) | 全文 |
| p.251-253 | 249-251 | 接続局がEthernetポート内蔵LCPUのEthernet通信(TCP) | 全文 |
| p.254-256 | 252-254 | 接続局がEthernetポート内蔵LCPUのEthernet通信(UDP) | 全文 |
| p.257-260 | 255-258 | 接続局がEthernetアダプタユニットのEthernet通信(TCP) | 全文 |
| p.261-264 | 259-262 | 接続局がEthernetアダプタユニットのEthernet通信(UDP) | 全文 |
| p.192-242, p.265-417 | 190-240, 263-415 | 10章の他の範囲 | 別ファイル(10-1〜10-9 の他ファイル) |
| p.1-191, p.418-696 | — | 他の章 | 別ファイル / **未変換** |

## 目次

- 接続局がEthernetポート内蔵QCPUのEthernet通信(TCP)
- 接続局がEthernetポート内蔵QCPUのEthernet通信(UDP)
- 接続局がEthernetポート内蔵LCPUのEthernet通信(TCP)
- 接続局がEthernetポート内蔵LCPUのEthernet通信(UDP)
- 接続局がEthernetアダプタユニットのEthernet通信(TCP)
- 接続局がEthernetアダプタユニットのEthernet通信(UDP)

---

## 接続局がEthernetポート内蔵QCPUのEthernet通信(TCP) (10.2 / 241-244 / 原本 p.243-246)

### 構成 (10.2 / 241-242 / 原本 p.243-244)

【図】構成 (パソコン ― 接続局CPU[経由ユニット] ― 経由ネットワーク ― 経由局CPU[経由ユニット])
- パソコンは接続局CPUのEthernetポートに直接接続。接続局側の経由ユニットから経由ネットワークを通り，経由局CPUの経由ユニットへ

### アクセス可否およびプロパティのパターン (10.2 / 241-242 / 原本 p.243-244)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: QnUDE(H)CPU/QnUD(P)VCPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU*4 | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | × | × | × | × | × |
|  | MELSECNET/H | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × |
|  | CC-Link | × | × | × | × | × |

| 接続局CPU: QnUDE(H)CPU/QnUD(P)VCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | ○(2) | ○(2)*1 | ○(2)*2 | ○(2)*1 | ○(2)*1 | × |
|  | MELSECNET/H | ○(2) | ○(2) | × | ○(2) | ○(2) | × |
|  | Ethernet | ○(2) | × | × | ○(2) | ○(2) | × |
|  | シリアルコミュニケーション | ○(3)*3 | × | ○(3) | × | ○(3) | × |
|  | CC-Link | ○(4) | ○(4) | ○(4) | × | ○(4) | × |

| 接続局CPU: QCCPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU*4 | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1)*4*5*6 | CC IE TSN | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | × | × | × | × | × |
|  | MELSECNET/H | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × |
|  | CC-Link | × | × | × | × | × |

| 接続局CPU: QCCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1)*4*5*6 | CC IE TSN | × | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | ○(2) | ○(2)*1 | ○(2)*2 | ○(2)*1 | ○(2)*1 | × |
|  | MELSECNET/H | ○(2) | ○(2) | × | ○(2) | ○(2) | × |
|  | Ethernet | × | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × | × |
|  | CC-Link | ○(4) | ○(4) | ○(4) | × | ○(4) | × |

| 接続局CPU: QモーションCPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1)*7 | CC IE TSN | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | × | × | × | × | × |
|  | MELSECNET/H | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × |
|  | CC-Link | × | × | × | × | × |

| 接続局CPU: QモーションCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1)*7 | CC IE TSN | × | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
|  | MELSECNET/H | × | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × | × |
|  | CC-Link | × | × | × | × | × | × |

> *1 RモーションCPU，Q12DCCPU-V(基本機能モード)，QSCPU，QモーションCPUは，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。
> *2 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
> *3 二重化CPUの場合，基本ベースユニット上にあるシリアルコミュニケーションユニットにはアクセスできません。
> *4 マルチCPU構成時の，2号機以降の場合のみアクセス可能です。
> *5 Q24DHCCPU-V，Q24DHCCPU-LS，Q24DHCCPU-VG，Q26DHCCPU-LSは，通信経路が未サポートのためアクセスできません。
> *6 QCCPUはMELSOFT直結接続に対応していないため，Ethernetポート直結接続ではアクセスできません。
> *7 Q172D，Q173D，Q172DS，Q173DSが，マルチCPU構成時の2号機以降の場合のみアクセス可能です。

### プロパティ一覧 (10.2 / 243-244 / 原本 p.245-246)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

※「(全パターン共通)」は原本で○(1)〜○(4)の4列を結合した1セル。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ (全パターン共通) |  |  |  |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) |
| ActDestinationPortNumber | 0(0x00) | 5007 (全パターン共通) |  |  |  |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActHostAddress | 1.1.1.1 | 接続局側ユニットのホスト名またはIPアドレス (全パターン共通) |  |  |  |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局<br>QCPU(Qモード)，LCPU: 1(0x01)<br>上記以外: 0(0x00) | 対象局<br>QCPU(Qモード)，QCCPU，LCPU: 1(0x01)<br>上記以外: 0(0x00) |
| ActIONumber*1 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 接続局側経由ユニットI/Oアドレス | 接続局側経由ユニットI/Oアドレス |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber*3 | 0(0x00) | 0(0x00)固定 | 対象局側ユニットネットワークNo. | 0(0x00)固定 | 0(0x00)固定 |
| ActPassword | あき | 接続局に設定されたリモートパスワード (全パターン共通) |  |  |  |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_TCPIP(0x05) (全パターン共通) |  |  |  |
| ActStationNumber*3 | 255(0xFF) | 255(0xFF)固定 | 対象局側ユニット局番 | 255(0xFF)固定 | 255(0xFF)固定 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) (全パターン共通) |  |  |  |
| ActTimeOut | 10000 | ms単位でユーザ任意 (全パターン共通) |  |  |  |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_QNETHER(0x2C) (全パターン共通) |  |  |  |

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2
> *3 プロパティのパターンが(1)または(2)の場合，ActNetworkNumberおよびActStationNumberは対象局側のパラメータで設定した値を指定してください。

---

## 接続局がEthernetポート内蔵QCPUのEthernet通信(UDP) (10.2 / 245-248 / 原本 p.247-250)

### 構成 (10.2 / 245-246 / 原本 p.247-248)

【図】構成 (パソコン ― 接続局CPU[経由ユニット] ― 経由ネットワーク ― 経由局CPU[経由ユニット])
- パソコンは接続局CPUのEthernetポートに直接接続。接続局側の経由ユニットから経由ネットワークを通り，経由局CPUの経由ユニットへ

### アクセス可否およびプロパティのパターン (10.2 / 245-246 / 原本 p.247-248)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: QnUDE(H)CPU/QnUD(P)VCPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU*4 | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | × | × | × | × | × |
|  | MELSECNET/H | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × |
|  | CC-Link | × | × | × | × | × |

| 接続局CPU: QnUDE(H)CPU/QnUD(P)VCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | ○(2) | ○(2)*1 | ○(2)*2 | ○(2)*1 | ○(2)*1 | × |
|  | MELSECNET/H | ○(2) | ○(2) | × | ○(2) | ○(2) | × |
|  | Ethernet | ○(2) | × | × | ○(2) | ○(2) | × |
|  | シリアルコミュニケーション | ○(3)*3 | × | ○(3) | × | ○(3) | × |
|  | CC-Link | ○(4) | ○(4) | ○(4) | × | ○(4) | × |

| 接続局CPU: QCCPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU*4 | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1)*4*5*6 | CC IE TSN | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | × | × | × | × | × |
|  | MELSECNET/H | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × |
|  | CC-Link | × | × | × | × | × |

| 接続局CPU: QCCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1)*4*5*6 | CC IE TSN | × | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | ○(2) | ○(2)*1 | ○(2)*2 | ○(2)*1 | ○(2)*1 | × |
|  | MELSECNET/H | ○(2) | ○(2) | × | ○(2) | ○(2) | × |
|  | Ethernet | × | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × | × |
|  | CC-Link | ○(4) | ○(4) | ○(4) | × | ○(4) | × |

| 接続局CPU: QモーションCPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1)*7 | CC IE TSN | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | × | × | × | × | × |
|  | MELSECNET/H | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × |
|  | CC-Link | × | × | × | × | × |

| 接続局CPU: QモーションCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1)*7 | CC IE TSN | × | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
|  | MELSECNET/H | × | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × | × |
|  | CC-Link | × | × | × | × | × | × |

> *1 RモーションCPU，Q12DCCPU-V(基本機能モード)，QSCPU，QモーションCPUは，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。
> *2 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
> *3 二重化CPUの場合，基本ベースユニット上にあるシリアルコミュニケーションユニットにはアクセスできません。
> *4 マルチCPU構成時の，2号機以降の場合のみアクセス可能です。
> *5 Q24DHCCPU-V，Q24DHCCPU-LS，Q24DHCCPU-VG，Q26DHCCPU-LSは，通信経路が未サポートのためアクセスできません。
> *6 QCCPUはMELSOFT直結接続に対応していないため，Ethernetポート直結接続ではアクセスできません。
> *7 Q172D，Q173D，Q172DS，Q173DSが，マルチCPU構成時の2号機以降の場合のみアクセス可能です。

### プロパティ一覧 (10.2 / 247-248 / 原本 p.249-250)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

※「(全パターン共通)」は原本で○(1)〜○(4)の4列を結合した1セル。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ (全パターン共通) |  |  |  |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) |
| ActDestinationPortNumber | 0(0x00) | • IPアドレス指定通信時: 5006<br>• IPアドレス指定なし直結通信時: 未使用 (全パターン共通) |  |  |  |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActHostAddress | 1.1.1.1 | • IPアドレス指定通信時: 接続局側ユニットのホスト名またはIPアドレス<br>• IPアドレス指定なし直結通信時: 指定は無効 (全パターン共通) |  |  |  |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局<br>• QCPU(Qモード)，LCPU: 1(0x01)<br>• 上記以外 : 0(0x00) | 対象局<br>• QCPU(Qモード)，QCCPU，LCPU: 1(0x01)<br>• 上記以外 : 0(0x00) |
| ActIONumber*1 | 1023(0x3FF) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 接続局側経由ユニットI/Oアドレス | 接続局側経由ユニットI/Oアドレス |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber*3 | 0(0x00) | 0(0x00)固定 | 対象局側ユニットネットワークNo. | 0(0x00)固定 | 0(0x00)固定 |
| ActPassword | あき | 接続局に設定されたリモートパスワード (全パターン共通) |  |  |  |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_UDPIP(0x08) (全パターン共通) |  |  |  |
| ActStationNumber*3 | 255(0xFF) | 255(0xFF)固定 | 対象局側ユニット局番 | 255(0xFF)固定 | 255(0xFF)固定 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) (全パターン共通) |  |  |  |
| ActTimeOut | 10000 | ms単位でユーザ任意 (全パターン共通) |  |  |  |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | • IPアドレス指定通信時: UNIT_QNETHER(0x2C)<br>• IPアドレス指定なし直結通信時: UNIT_QNETHER_DIRECT(0x2D) (全パターン共通) |  |  |  |

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2
> *3 プロパティのパターンが(1)または(2)の場合，ActNetworkNumberおよびActStationNumberは対象局側のパラメータで設定した値を指定してください。

※TCP版(原本 p.245)では ActIONumber の○(1)に「対象局側」の前置きが無いが，UDP版(原本 p.249)では○(1)に「対象局側」がある(原本どおり)。

---

## 接続局がEthernetポート内蔵LCPUのEthernet通信(TCP) (10.2 / 249-251 / 原本 p.251-253)

### 構成 (10.2 / 249 / 原本 p.251)

【図】構成 (パソコン ― 接続局CPU[経由ユニット] ― 経由ネットワーク ― 経由局CPU[経由ユニット])
- パソコンは接続局CPUのEthernetポートに直接接続。接続局側の経由ユニットから経由ネットワークを通り，経由局CPUの経由ユニットへ

### アクセス可否およびプロパティのパターン (10.2 / 249 / 原本 p.251)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: LCPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × |
|  | CC IE Field*1 | × | × | × | × | × |
|  | MELSECNET/H | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × |
|  | CC-Link | × | × | × | × | × |

| 接続局CPU: LCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
|  | CC IE Field*1 | ○(4) | ○(4)*2 | ○(4) | × | × | × |
|  | MELSECNET/H | × | × | × | × | × | × |
|  | Ethernet | ○(4) | × | ○(4) | × | × | × |
|  | シリアルコミュニケーション | ○(2)*3 | × | ○(2) | × | × | × |
|  | CC-Link | ○(3) | ○(3) | ○(3) | × | × | × |

> *1 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
> *2 Q12DCCPU-V(基本機能モード)は，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。
> *3 二重化CPUの場合，基本ベースユニット上にあるシリアルコミュニケーションユニットにはアクセスできません。

### プロパティ一覧 (10.2 / 250-251 / 原本 p.252-253)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

※「(全パターン共通)」は原本で○(1)〜○(4)の4列を結合した1セル。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 (全パターン共通) |  |  |  |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 (全パターン共通) |  |  |  |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ (全パターン共通) |  |  |  |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 (全パターン共通) |  |  |  |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 0(0x00)固定 |
| ActDestinationPortNumber | 0(0x00) | 5007 (全パターン共通) |  |  |  |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 | 1(0x01)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 | 1(0x01)固定 |
| ActHostAddress | 1.1.1.1 | 接続局側ユニットのホスト名またはIPアドレス (全パターン共通) |  |  |  |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 対象局<br>QCPU(Qモード)，LCPU: 1(0x01)<br>上記以外: 0(0x00) | 対象局<br>QCPU(Qモード)，QCCPU，LCPU: 1(0x01)<br>上記以外: 0(0x00) | 0(0x00)固定 |
| ActIONumber*1 | 1023(0x3FF) | ■シングルCPU時<br>1023(0x3FF)固定 | 接続局側経由ユニットI/Oアドレス | 接続局側経由ユニットI/Oアドレス | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 | 0(0x00)固定 |
| ActNetworkNumber*3 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニットネットワークNo. |
| ActParity | 1(ODD_PARITY) | 0(0x00)固定 (全パターン共通) |  |  |  |
| ActPassword | あき | 接続局に設定されたリモートパスワード (全パターン共通) |  |  |  |
| ActPortNumber | 1(PORT_1) | 0(0x00)固定 (全パターン共通) |  |  |  |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_TCPIP(0x05) (全パターン共通) |  |  |  |
| ActStationNumber*3 | 255(0xFF) | 255(0xFF)固定 | 255(0xFF)固定 | 255(0xFF)固定 | 対象局側ユニット局番 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) (全パターン共通) |  |  |  |
| ActTimeOut | 10000 | ms単位でユーザ任意 (全パターン共通) |  |  |  |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 | 0(0x00)固定 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_LNETHER(0x52) (全パターン共通) |  |  |  |

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2
> *3 プロパティのパターンが(1)または(2)の場合，ActNetworkNumberおよびActStationNumberは対象局側のパラメータで設定した値を指定してください。

---

## 接続局がEthernetポート内蔵LCPUのEthernet通信(UDP) (10.2 / 252-254 / 原本 p.254-256)

### 構成 (10.2 / 252 / 原本 p.254)

【図】構成 (パソコン ― 接続局CPU[経由ユニット] ― 経由ネットワーク ― 経由局CPU[経由ユニット])
- パソコンは接続局CPUのEthernetポートに直接接続。接続局側の経由ユニットから経由ネットワークを通り，経由局CPUの経由ユニットへ

### アクセス可否およびプロパティのパターン (10.2 / 252 / 原本 p.254)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: LCPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × |
|  | CC IE Field*1 | × | × | × | × | × |
|  | MELSECNET/H | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × |
|  | CC-Link | × | × | × | × | × |

| 接続局CPU: LCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
|  | CC IE Field*1 | ○(4) | ○(4)*2 | ○(4) | × | × | × |
|  | MELSECNET/H | × | × | × | × | × | × |
|  | Ethernet | ○(4) | × | ○(4) | × | × | × |
|  | シリアルコミュニケーション | ○(2)*3 | × | ○(2) | × | × | × |
|  | CC-Link | ○(3) | ○(3) | ○(3) | × | × | × |

> *1 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
> *2 Q12DCCPU-V(基本機能モード)は，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。
> *3 二重化CPUの場合，基本ベースユニット上にあるシリアルコミュニケーションユニットにはアクセスできません。

### プロパティ一覧 (10.2 / 253-254 / 原本 p.255-256)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

※「(全パターン共通)」は原本で○(1)〜○(4)の4列を結合した1セル。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 (全パターン共通) |  |  |  |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 (全パターン共通) |  |  |  |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ (全パターン共通) |  |  |  |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 (全パターン共通) |  |  |  |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 0(0x00)固定 |
| ActDestinationPortNumber | 0(0x00) | • IP アドレス指定通信時: 5006<br>• IP アドレス指定なし直結通信時: 5008 (全パターン共通) |  |  |  |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 | 1(0x01)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 | 1(0x01)固定 |
| ActHostAddress | 1.1.1.1 | • IPアドレス指定通信時: 接続局側ユニットのホスト名またはIPアドレス<br>• IPアドレス指定なし直結通信時: 255.255.255.255 (全パターン共通) |  |  |  |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 対象局<br>• QCPU(Qモード)，LCPU: 1(0x01)<br>• 上記以外 : 0(0x00) | 対象局<br>• QCPU(Qモード)，QCCPU，LCPU: 1(0x01)<br>• 上記以外: 0(0x00) | 0(0x00)固定 |
| ActIONumber*1 | 1023(0x3FF) | ■シングルCPU時<br>1023(0x3FF)固定 | 接続局側経由ユニットI/Oアドレス | 接続局側経由ユニットI/Oアドレス | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 | 0(0x00)固定 |
| ActNetworkNumber*3 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニットネットワークNo. |
| ActParity | 1(ODD_PARITY) | 0(0x00)固定 (全パターン共通) |  |  |  |
| ActPassword | あき | 接続局に設定されたリモートパスワード (全パターン共通) |  |  |  |
| ActPortNumber | 1(PORT_1) | 0(0x00)固定 (全パターン共通) |  |  |  |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_UDPIP(0x08) (全パターン共通) |  |  |  |
| ActStationNumber*3 | 255(0xFF) | 255(0xFF)固定 | 255(0xFF)固定 | 255(0xFF)固定 | 対象局側ユニット局番 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) (全パターン共通) |  |  |  |
| ActTimeOut | 10000 | ms単位でユーザ任意 (全パターン共通) |  |  |  |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 | 0(0x00)固定 |
| ActUnitType | 0x13(UNIT_QNCPU) | • IPアドレス指定通信時: UNIT_LNETHER(0x52)<br>• IPアドレス指定なし直結通信時: UNIT_LNETHER_DIRECT(0x53) (全パターン共通) |  |  |  |
| ActPacketType | 0x01(PACKET_PLC1) | PACKET_PLC1 (全パターン共通) |  |  |  |

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2
> *3 プロパティのパターンが(1)または(2)の場合，ActNetworkNumberおよびActStationNumberは対象局側のパラメータで設定した値を指定してください。

※原本では ActUnitNumber，ActUnitType，ActPacketType の3行が p.256 に続きの表として載っている(脚注は p.256 の表の下)。○(4)の ActIONumber の「4号機: 995(0x3E3)」に行頭の「•」が無いのは原本どおり。

---

## 接続局がEthernetアダプタユニットのEthernet通信(TCP) (10.2 / 255-258 / 原本 p.257-260)

### 構成 (10.2 / 255-256 / 原本 p.257-258)

【図】構成 (パソコン ― Ethernetアダプタユニット ― 接続局のCC-Link IEフィールドネットワークユニット ― 接続局CPU[経由ユニット] ― 経由ネットワーク ― 経由局CPU[経由ユニット])
- パソコンはEthernetアダプタユニットに接続し，Ethernetアダプタユニットは接続局CPUのCC-Link IEフィールドネットワークユニットとつながる。接続局側の経由ユニットから経由ネットワークを通り，経由局CPUの経由ユニットへ

### アクセス可否およびプロパティのパターン (10.2 / 255-256 / 原本 p.257-258)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: QnUDE(H)CPU/QnUD(P)VCPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | × | × | × | × | × |
|  | MELSECNET/H | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × |
|  | CC-Link | × | × | × | × | × |

| 接続局CPU: QnUDE(H)CPU/QnUD(P)VCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | ○(2) | ○(2)*1 | ○(2)*2 | × | × | × |
|  | MELSECNET/H | ○(2) | ○(2) | × | × | × | × |
|  | Ethernet | ○(2) | × | × | × | × | × |
|  | シリアルコミュニケーション | ○(3) | × | ○(3) | × | × | × |
|  | CC-Link | ○(4) | ○(4) | ○(4) | × | × | × |

| 接続局CPU: LCPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × |
|  | CC IE Field*2 | × | × | × | × | × |
|  | MELSECNET/H | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × |
|  | CC-Link | × | × | × | × | × |

| 接続局CPU: LCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
|  | CC IE Field*2 | ○(2) | ○(2)*1 | ○(2) | × | × | × |
|  | MELSECNET/H | × | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × | × |
|  | シリアルコミュニケーション | ○(3) | × | ○(3) | × | × | × |
|  | CC-Link | ○(4) | ○(4) | ○(4) | × | × | × |

> *1 Q12DCCPU-V(基本機能モード)は，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。
> *2 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。

※原本では脚注*1の文が p.255/p.256(UDP版は p.259/p.260)のページをまたいでいる。LCPU表の「CC IE Field*2」は原本どおり(*2の内容はCC-Link IEコントローラネットワーク非対応の説明)。

### プロパティ一覧 (10.2 / 257-258 / 原本 p.259-260)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

※「(全パターン共通)」は原本で○(1)〜○(4)の4列を結合した1セル。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ (全パターン共通) |  |  |  |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActHostAddress | 1.1.1.1 | Ethernetアダプタユニットのホスト名またはIPアドレス (全パターン共通) |  |  |  |
| ActIONumber*1 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 接続局側経由ユニットI/Oアドレス | 接続局側経由ユニットI/Oアドレス |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber*3 | 0(0x00) | 接続局側CC-Link IEフィールドネットワークユニットネットワークNo. | 対象局側ユニットネットワークNo. | 接続局側CC-Link IEフィールドネットワークユニットネットワークNo. | 接続局側CC-Link IEフィールドネットワークユニットネットワークNo. |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_TCPIP(0x05) (全パターン共通) |  |  |  |
| ActStationNumber*3 | 255(0xFF) | 接続局側CC-Link IEフィールドネットワークユニット局番 | 対象局側ユニット局番 | 接続局側CC-Link IEフィールドネットワークユニット局番 | 接続局側CC-Link IEフィールドネットワークユニット局番 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) (全パターン共通) |  |  |  |
| ActTimeOut | 10000 | ms単位でユーザ任意 (全パターン共通) |  |  |  |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_NZ2GF_ETB(0x59) (全パターン共通) |  |  |  |

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2
> *3 プロパティのパターンが(1)(3)(4)の場合，ActNetworkNumberおよびActStationNumberは接続局側のCC-Link IEフィールドネットワークユニットのパラメータで設定した値を指定してください。
> プロパティのパターンが(2)の場合，ActNetworkNumberおよびActStationNumberは対象局側のパラメータで設定した値を指定してください。

---

## 接続局がEthernetアダプタユニットのEthernet通信(UDP) (10.2 / 259-262 / 原本 p.261-264)

### 構成 (10.2 / 259-260 / 原本 p.261-262)

【図】構成 (パソコン ― Ethernetアダプタユニット ― 接続局のCC-Link IEフィールドネットワークユニット ― 接続局CPU[経由ユニット] ― 経由ネットワーク ― 経由局CPU[経由ユニット])
- パソコンはEthernetアダプタユニットに接続し，Ethernetアダプタユニットは接続局CPUのCC-Link IEフィールドネットワークユニットとつながる。接続局側の経由ユニットから経由ネットワークを通り，経由局CPUの経由ユニットへ

### アクセス可否およびプロパティのパターン (10.2 / 259-260 / 原本 p.261-262)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: QnUDE(H)CPU/QnUD(P)VCPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | × | × | × | × | × |
|  | MELSECNET/H | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × |
|  | CC-Link | × | × | × | × | × |

| 接続局CPU: QnUDE(H)CPU/QnUD(P)VCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | ○(2) | ○(2)*1 | ○(2)*2 | × | × | × |
|  | MELSECNET/H | ○(2) | ○(2) | × | × | × | × |
|  | Ethernet | ○(2) | × | × | × | × | × |
|  | シリアルコミュニケーション | ○(3) | × | ○(3) | × | × | × |
|  | CC-Link | ○(4) | ○(4) | ○(4) | × | × | × |

| 接続局CPU: LCPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × |
|  | CC IE Field*2 | × | × | × | × | × |
|  | MELSECNET/H | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × |
|  | CC-Link | × | × | × | × | × |

| 接続局CPU: LCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
|  | CC IE Field*2 | ○(2) | ○(2)*1 | ○(2) | × | × | × |
|  | MELSECNET/H | × | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × | × |
|  | シリアルコミュニケーション | ○(3) | × | ○(3) | × | × | × |
|  | CC-Link | ○(4) | ○(4) | ○(4) | × | × | × |

> *1 Q12DCCPU-V(基本機能モード)は，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。
> *2 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。

※原本では脚注*1の文が p.255/p.256(UDP版は p.259/p.260)のページをまたいでいる。LCPU表の「CC IE Field*2」は原本どおり(*2の内容はCC-Link IEコントローラネットワーク非対応の説明)。

### プロパティ一覧 (10.2 / 261-262 / 原本 p.263-264)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

※「(全パターン共通)」は原本で○(1)〜○(4)の4列を結合した1セル。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ (全パターン共通) |  |  |  |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActHostAddress | 1.1.1.1 | • IPアドレス指定通信時: Ethernetアダプタユニットのホスト名またはIPアドレス<br>• IPアドレス指定なし直結通信時: 指定は無効 (全パターン共通) |  |  |  |
| ActIONumber*1 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 接続局側経由ユニットI/Oアドレス | 接続局側経由ユニットI/Oアドレス |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber*3 | 0(0x00) | 接続局側CC-Link IEフィールドネットワークユニットネットワークNo. | 対象局側ユニットネットワークNo. | 接続局側CC-Link IEフィールドネットワークユニットネットワークNo. | 接続局側CC-Link IEフィールドネットワークユニットネットワークNo. |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_UDPIP(0x08) (全パターン共通) |  |  |  |
| ActStationNumber*3 | 255(0xFF) | 接続局側CC-Link IEフィールドネットワークユニット局番 | 対象局側ユニット局番 | 接続局側CC-Link IEフィールドネットワークユニット局番 | 接続局側CC-Link IEフィールドネットワークユニット局番 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) (全パターン共通) |  |  |  |
| ActTimeOut | 10000 | ms単位でユーザ任意 (全パターン共通) |  |  |  |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | • IPアドレス指定通信時: UNIT_NZ2GF_ETB(0x59)<br>• IPアドレス指定なし直結通信時: UNIT_NZ2GF_ETB_DIRECT(0x5A) (全パターン共通) |  |  |  |

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2
> *3 プロパティのパターンが(1)(3)(4)の場合，ActNetworkNumberおよびActStationNumberは接続局側のCC-Link IEフィールドネットワークユニットのパラメータで設定した値を指定してください。
> プロパティのパターンが(2)の場合，ActNetworkNumberおよびActStationNumberは対象局側のパラメータで設定した値を指定してください。

---

