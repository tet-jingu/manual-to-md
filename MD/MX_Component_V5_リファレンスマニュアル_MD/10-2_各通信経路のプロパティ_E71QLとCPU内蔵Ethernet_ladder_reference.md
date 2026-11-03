# MX Component Version 5 リファレンスマニュアル 10章 各通信経路で設定するプロパティ (2/9) p.215-242

| 項目 | 内容 |
|---|---|
| 原本 | 【三菱】MX Component Version 5 リファレンスマニュアル (SH-082394J) |
| メーカー | 三菱電機 |
| 原本ファイル | `PDF/【三菱】MX Component Version 5 リファレンスマニュアル_sh082394j.pdf` (全696ページ) |
| 本ファイルの範囲 | 10.2 Ethernet通信のうち「接続局がQシリーズ対応E71(TCP)」〜「接続局がFX5CPU(UDP)」(印刷ページ 213-240 / PDF p.215-242) |
| 出典表記 | `(節 / 印刷ページ / 原本 p.PDFページ)` |
| 作成日 | 2026-11-03 |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。
> 本文中の「○ページ」はすべて原本の**印刷ページ番号**です(PDFページ = 印刷ページ + 2)。
> アクセス可否表は原本の2段組(経由局CPUが iQ-R/LH/FX5系 と Q/L/FX系)をそれぞれ1表にしている。接続局CPUの列(○(1)等)は表の上に1行で記載。
> プロパティ一覧の「(同左)」は原本で左隣セルと結合されていることを示す。

## 主要用語 対訳表 (Glossary)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| 接続局CPU / 経由局CPU | Connected station CPU / Relayed station CPU | — | 参考訳 |
| 経由ネットワーク / 経由ユニット | Relayed network / Relayed module | — | 参考訳 |
| アクセス可否およびプロパティのパターン | Accessibility and property pattern | ○(1)〜○(4) | 参考訳 |
| 対象局 | Target station | — | 参考訳 |
| シングルCPU / マルチCPU / 二重化CPU | Single CPU / Multiple CPU / Redundant CPU | 1023(0x3FF) / 992〜995(0x3E0〜0x3E3) / 976(0x3D0) | 参考訳 |
| 接続号機 / 制御系 | Connected CPU No. / Control system | — | 参考訳 |
| I/Oアドレス(I/O先頭No.÷16) | I/O address (start I/O No. ÷ 16) | ActIONumber / ActDestinationIONumber | 参考訳 |
| マルチドロップチャネルNo. | Multidrop channel No. | ActMultiDropChannelNumber | 参考訳 |
| リモートパスワード | Remote password | ActPassword | 参考訳 |
| パソコン側ネットワークNo. / 局番 | PC side network No. / station No. | ActSourceNetworkNumber / ActSourceStationNumber | 参考訳 |
| 局番⇔IP関連情報(設定方式) | Station No.⇔IP information (setting method) | 自動応答 / IPアドレス算出 / テーブル変換 / 併用 | 参考訳 |
| MELSOFT接続 / OPS接続 | MELSOFT connection / OPS connection | 5002 / 任意 | 参考訳 |
| IPアドレス指定なし直結通信 | Direct connection without IP address | 255.255.255.255 / 5008 | 参考訳 |
| PC側のアダプタ選択 | PC side adapter selection | ActHostAddress | 参考訳 |
| Qシリーズ対応E71 / Lシリーズ対応E71 | Q series E71 / L series E71 | UNIT_QJ71E71(0x1A) / UNIT_LJ71E71(0x5C) | 参考訳 |
| iQ-R CPU内蔵Ethernet | iQ-R built-in Ethernet | UNIT_RETHER(0x1002) / UNIT_RETHER_DIRECT(0x1003) | 参考訳 |
| LHCPU内蔵Ethernet | LHCPU built-in Ethernet | UNIT_LHETHER(0x1002) / UNIT_LHETHER_DIRECT(0x1003) | 参考訳 |
| FX5CPU内蔵Ethernet | FX5CPU built-in Ethernet | UNIT_FXVETHER(0x2001) / UNIT_FXVETHER_DIRECT(0x2002) | 参考訳 |
| MELSECNET/10を含む | Including MELSECNET/10 | ActThroughNetworkType | 参考訳 |
| インテリジェント優先ビット | Intelligent preference bit | ActIntelligentPreferenceBit | 参考訳 |

## 変換範囲表

| 原本ページ(PDF) | 印刷ページ | 節 | 扱い |
|---|---|---|---|
| p.215-220 | 213-218 | 接続局がQシリーズ対応E71のEthernet通信(TCP)/(UDP) | 全文 |
| p.221-226 | 219-224 | 接続局がLシリーズ対応E71のEthernet通信(TCP)/(UDP) | 全文 |
| p.227-234 | 225-232 | 接続局がMELSEC iQ-RシリーズCPUユニットのEthernet通信(TCP)/(UDP) | 全文 |
| p.235-238 | 233-236 | 接続局がLHCPUのEthernet通信(TCP)/(UDP) | 全文 |
| p.239-242 | 237-240 | 接続局がFX5CPUのEthernet通信(TCP)/(UDP) | 全文 |
| p.192-214 | 190-212 | 10章冒頭・10.1・10.2(iQ-R対応E71) | 別ファイル 10-1 |
| p.243-417 | 241-415 | 10.2 残り〜10.16 | 別ファイル 10-3〜10-9 |

## 目次

- 接続局がQシリーズ対応E71のEthernet通信(TCP) / (UDP)
- 接続局がLシリーズ対応E71のEthernet通信(TCP) / (UDP)
- 接続局がMELSEC iQ-RシリーズCPUユニットのEthernet通信(TCP) / (UDP)
- 接続局がLHCPUのEthernet通信(TCP) / (UDP)
- 接続局がFX5CPUのEthernet通信(TCP) / (UDP)

---

## 接続局がQシリーズ対応E71のEthernet通信(TCP) (10.2 / 213-215 / 原本 p.215-217)

### 構成 (10.2 / 213 / 原本 p.215)
【図】構成 — パソコン ― 接続局CPU［Qシリーズ対応E71］―(同一ベースの)経由ユニット ― 経由ネットワーク ― 経由ユニット［経由局CPU］

### アクセス可否およびプロパティのパターン (10.2 / 213 / 原本 p.215)
○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

**経由局CPU: MELSEC iQ-R/LH/FX5系**

接続局CPU: QCPU(Qモード) ○(1)，QCCPU ○(1)*6，QSCPU ○(1)*2，QモーションCPU ○(1)*1*2

| 経由ネットワーク | RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × |
| CC IE Control / CC IE Field | × | × | × | × | × |
| MELSECNET/H | × | × | × | × | × |
| Ethernet | × | × | × | × | × |
| シリアルコミュニケーション | × | × | × | × | × |
| CC-Link | × | × | × | × | × |

**経由局CPU: Q/L/FX系**

接続局CPU: QCPU(Qモード) ○(1)，QCCPU ○(1)*6，QSCPU ○(1)*2，QモーションCPU ○(1)*1*2

| 経由ネットワーク | QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × | × |
| CC IE Control / CC IE Field | ○(2) | ○(2)*3 | ○(2)*4 | ○(2)*2*3 | ○(2)*3 | × |
| MELSECNET/H | ○(2) | ○(2) | × | ○(2)*2 | ○(2) | × |
| Ethernet | ○(2) | × | × | ○(2)*2 | ○(2) | × |
| シリアルコミュニケーション | ○(3)*5 | × | ○(3)*5 | × | ○(3) | × |
| CC-Link | ○(4) | ○(4) | ○(4) | × | ○(4) | × |

> *1 Q172D，Q173D，Q172DS，Q173DSのみアクセス可能です。
> *2 QSCPU，QモーションCPUを経由して経由局CPUにアクセスできません。
> *3 RモーションCPU，Q12DCCPU-V(基本機能モード)，QSCPU，QモーションCPUは，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。
> *4 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
> *5 二重化CPUの場合，基本ベースユニット上にあるシリアルコミュニケーションユニットにはアクセスできません。
> *6 マルチCPU構成時の，2号機以降の場合のみアクセス可能です。

### プロパティ一覧 (10.2 / 214 / 原本 p.216)
各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActConnectUnitNumber | 0(0x00) | 0(0x00)固定 | 接続局側ユニット局番 | 0(0x00)固定 | 0(0x00)固定 |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | (同左) | (同左) | (同左) |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) |
| ActDestinationPortNumber | 0(0x00) | • MELSOFT接続時: 5002<br>• OPS接続時: 任意のポートNo.*1 | (同左) | (同左) | (同左) |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActHostAddress | 1.1.1.1 | 接続局側ユニットのホスト名またはIPアドレス | (同左) | (同左) | (同左) |
| ActIONumber*2 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 接続局側経由ユニットI/Oアドレス | 接続局側経由ユニットI/Oアドレス |
| ActMultiDropChannelNumber*3 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber*4 | 0(0x00) | 対象局側ユニットネットワークNo. | 対象局側ユニットネットワークNo. | 接続局側Qシリーズ対応E71ネットワークNo. | 接続局側Qシリーズ対応E71ネットワークNo. |
| ActPassword | あき | 接続局側のQシリーズ対応E71に設定されたパスワード | (同左) | (同左) | (同左) |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_TCPIP(0x05) | (同左) | (同左) | (同左) |
| ActSourceNetworkNumber | 0(0x00) | パソコン側ネットワークNo. | (同左) | (同左) | (同左) |
| ActSourceStationNumber*5 | 0(0x00) | パソコン側局番 | (同左) | (同左) | (同左) |
| ActStationNumber*4 | 255(0xFF) | 対象局側ユニット局番 | 対象局側ユニット局番 | 接続局側Qシリーズ対応E71局番 | 接続局側Qシリーズ対応E71局番 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | (同左) | (同左) | (同左) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | (同左) | (同左) | (同左) |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_QJ71E71(0x1A) | (同左) | (同左) | (同左) |
※「(同左)」は，原本でそのセルが左隣のセルと結合されている(同じ値)ことを示す。

> *1 二重化CPU接続時にOPS接続の機能を使用する場合は，ネットワークパラメータに指定した任意のポートNo.を指定してください。(設定範囲は，1025≦ポートNo.≦4999または5003≦ポートNo.≦65534)
> *2 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *3 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2
> *4 プロパティのパターンが(1)または(2)の場合，ActNetworkNumberおよびActStationNumberは対象局側のパラメータで設定した値を指定してください。
> *5 Ethernetの同一ループ内でのQシリーズ対応E71に設定した局番と重複しないように，パソコン側の局番を指定してください。
(脚注は原本 p.217)

---

## 接続局がQシリーズ対応E71のEthernet通信(UDP) (10.2 / 216-218 / 原本 p.218-220)

### 構成 (10.2 / 216 / 原本 p.218)
【図】構成 — パソコン ― 接続局CPU［Qシリーズ対応E71］―(同一ベースの)経由ユニット ― 経由ネットワーク ― 経由ユニット［経由局CPU］

### アクセス可否およびプロパティのパターン (10.2 / 216 / 原本 p.218)
○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

**経由局CPU: MELSEC iQ-R/LH/FX5系**

接続局CPU: QCPU(Qモード) ○(1)，QCCPU ○(1)*6*7，QSCPU ○(1)*2，QモーションCPU ○(1)*1*2

| 経由ネットワーク | RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × |
| CC IE Control / CC IE Field | × | × | × | × | × |
| MELSECNET/H | × | × | × | × | × |
| Ethernet | × | × | × | × | × |
| シリアルコミュニケーション | × | × | × | × | × |
| CC-Link | × | × | × | × | × |

**経由局CPU: Q/L/FX系**

接続局CPU: QCPU(Qモード) ○(1)，QCCPU ○(1)*6*7，QSCPU ○(1)*2，QモーションCPU ○(1)*1*2

| 経由ネットワーク | QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × | × |
| CC IE Control / CC IE Field | ○(2) | ○(2)*3 | ○(2)*4 | ○(2)*2*3 | ○(2)*3 | × |
| MELSECNET/H | ○(2) | ○(2) | × | ○(2)*2 | ○(2) | × |
| Ethernet | ○(2) | × | × | ○(2)*2 | ○(2) | × |
| シリアルコミュニケーション | ○(3)*5 | × | ○(3)*5 | × | ○(3) | × |
| CC-Link | ○(4) | ○(4) | ○(4) | × | ○(4) | × |

> *1 Q172D，Q173D，Q172DS，Q173DSのみアクセス可能です。
> *2 QSCPU，QモーションCPUを経由して経由局CPUにアクセスできません。
> *3 RモーションCPU，Q12DCCPU-V(基本機能モード)，QSCPU，QモーションCPUは，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。
> *4 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
> *5 二重化CPUの場合，基本ベースユニット上にあるシリアルコミュニケーションユニットにはアクセスできません。
> *6 マルチCPU構成時の，2号機以降の場合のみアクセス可能です。
> *7 QCCPUはMELSOFT直結接続に対応していないため，Ethernetポート直結接続ではアクセスできません。

### プロパティ一覧 (10.2 / 217 / 原本 p.219)
各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActConnectUnitNumber | 0(0x00) | 0(0x00)固定 | 接続局側ユニット局番 | 0(0x00)固定 | 0(0x00)固定 |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | (同左) | (同左) | (同左) |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) |
| ActDestinationPortNumber | 0(0x00) | 5001 | (同左) | (同左) | (同左) |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActHostAddress | 1.1.1.1 | 接続局側ユニットのホスト名またはIPアドレス | (同左) | (同左) | (同左) |
| ActIONumber*1 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 接続局側経由ユニットI/Oアドレス | 接続局側経由ユニットI/Oアドレス |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber*3 | 0(0x00) | 対象局側ユニットネットワークNo. | 対象局側ユニットネットワークNo. | 接続局Qシリーズ対応E71ネットワークNo. | 接続局Qシリーズ対応E71ネットワークNo. |
| ActPassword | あき | 接続局側のQシリーズ対応E71に設定されたパスワード | (同左) | (同左) | (同左) |
| ActPortNumber*4 | 1(PORT_1) | パソコン側ポート番号 | (同左) | (同左) | (同左) |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_UDPIP(0x08) | (同左) | (同左) | (同左) |
| ActSourceNetworkNumber | 0(0x00) | パソコン側ネットワークNo. | (同左) | (同左) | (同左) |
| ActSourceStationNumber*5 | 0(0x00) | パソコン側局番 | (同左) | (同左) | (同左) |
| ActStationNumber*3 | 255(0xFF) | 対象局側ユニット局番 | 対象局側ユニット局番 | 接続局側Qシリーズ対応E71局番 | 接続局側Qシリーズ対応E71局番 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | (同左) | (同左) | (同左) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | (同左) | (同左) | (同左) |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_QJ71E71(0x1A) | (同左) | (同左) | (同左) |
※「(同左)」は，原本でそのセルが左隣のセルと結合されている(同じ値)ことを示す。

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2
> *3 プロパティのパターンが(1)または(2)の場合，ActNetworkNumberおよびActStationNumberは対象局側のパラメータで設定した値を指定してください。
> *4 ActPortNumberの1～1024までは使用しないでください。
> *5 Ethernetの同一ループ内でのQシリーズ対応E71に設定した局番と重複しないように，パソコン側の局番を指定してください。
(脚注は原本 p.220)

---

## 接続局がLシリーズ対応E71のEthernet通信(TCP) (10.2 / 219-221 / 原本 p.221-223)

### 構成 (10.2 / 219 / 原本 p.221)
【図】構成 — パソコン ― 接続局CPU［Lシリーズ対応E71］―(同一ベースの)経由ユニット ― 経由ネットワーク ― 経由ユニット［経由局CPU］

### アクセス可否およびプロパティのパターン (10.2 / 219 / 原本 p.221)
○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

**経由局CPU: MELSEC iQ-R/LH/FX5系**

接続局CPU: LCPU ○(1)

| 経由ネットワーク | RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × |
| CC IE Control / CC IE Field | × | × | × | × | × |
| MELSECNET/H | × | × | × | × | × |
| Ethernet | × | × | × | × | × |
| シリアルコミュニケーション | × | × | × | × | × |
| CC-Link | × | × | × | × | × |

**経由局CPU: Q/L/FX系**

接続局CPU: LCPU ○(1)

| 経由ネットワーク | QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU*1 | FXCPU |
|---|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × | × |
| CC IE Control / CC IE Field | × | × | × | × | × | × |
| MELSECNET/H | × | × | × | × | × | × |
| Ethernet | ○(2) | × | ○(2) | × | × | × |
| シリアルコミュニケーション | ○(3)*2 | × | ○(3)*2 | × | × | × |
| CC-Link | ○(4) | × | ○(4) | × | × | × |

> *1 Q172D，Q173D，Q172DS，Q173DSのみアクセス可能です。
> *2 二重化CPUの場合，基本ベースユニット上にあるシリアルコミュニケーションユニットにはアクセスできません。

### プロパティ一覧 (10.2 / 220 / 原本 p.222-223)
各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActConnectUnitNumber | 0(0x00) | 0(0x00)固定 | 接続局側ユニット局番 | 0(0x00)固定 | 0(0x00)固定 |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | (同左) | (同左) | (同左) |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) |
| ActDestinationPortNumber | 0(0x00) | • MELSOFT接続時: 5002<br>• OPS接続時: 任意のポートNo.*1 | (同左) | (同左) | (同左) |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActHostAddress | 1.1.1.1 | 接続局側ユニットのホスト名またはIPアドレス | (同左) | (同左) | (同左) |
| ActIONumber*2 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 接続局側経由ユニットI/Oアドレス | 接続局側経由ユニットI/Oアドレス |
| ActMultiDropChannelNumber*3 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber*4 | 0(0x00) | 対象局側ユニットネットワークNo. | 対象局側ユニットネットワークNo. | 接続局側Lシリーズ対応E71ネットワークNo. | 接続局側Lシリーズ対応E71ネットワークNo. |
| ActParity | 1(ODD_PARITY) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActPassword | あき | 接続局側のLシリーズ対応E71に設定されたパスワード | (同左) | (同左) | (同左) |
| ActPortNumber*5 | 1(PORT_1) | パソコン側ポート番号 | (同左) | (同左) | (同左) |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_TCPIP(0x05) | (同左) | (同左) | (同左) |
| ActSourceNetworkNumber | 0(0x00) | パソコン側ネットワークNo. | (同左) | (同左) | (同左) |
| ActSourceStationNumber*6 | 0(0x00) | パソコン側局番 | (同左) | (同左) | (同左) |
| ActStationNumber*4 | 255(0xFF) | 対象局側ユニット局番 | 対象局側ユニット局番 | 接続局側Lシリーズ対応E71局番 | 接続局側Lシリーズ対応E71局番 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | (同左) | (同左) | (同左) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | (同左) | (同左) | (同左) |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_LJ71E71(0x5C) | (同左) | (同左) | (同左) |
※「(同左)」は，原本でそのセルが左隣のセルと結合されている(同じ値)ことを示す。
※ActUnitType の行は原本では次ページ(p.223)に続く表の最終行。

> *1 二重化CPU接続時にOPS接続の機能を使用する場合は，ネットワークパラメータに指定した任意のポートNo.を指定してください。(設定範囲は，1025≦ポートNo.≦4999または5003≦ポートNo.≦65534)
> *2 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *3 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2
> *4 プロパティのパターンが(1)または(2)の場合，ActNetworkNumberおよびActStationNumberは対象局側のパラメータで設定した値を指定してください。
> *5 下記を指定してください。
> 0: パソコン内の空きポート番号を自動で割り当てます。
> 0以外の場合，Close関数実行後，再度Open関数実行時に，エラーが発生する場合があります。
> エラーが発生する場合は，Close関数実行後，時間をおいてOpen関数を実行してください。
> *6 Ethernetの同一ループ内でのLシリーズ対応E71に設定した局番と重複しないように，パソコン側の局番を指定してください。
(脚注は原本 p.223)

---

## 接続局がLシリーズ対応E71のEthernet通信(UDP) (10.2 / 222-224 / 原本 p.224-226)

### 構成 (10.2 / 222 / 原本 p.224)
【図】構成 — パソコン ― 接続局CPU［Lシリーズ対応E71］―(同一ベースの)経由ユニット ― 経由ネットワーク ― 経由ユニット［経由局CPU］

### アクセス可否およびプロパティのパターン (10.2 / 222 / 原本 p.224)
○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

**経由局CPU: MELSEC iQ-R/LH/FX5系**

接続局CPU: LCPU ○(1)

| 経由ネットワーク | RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × |
| CC IE Control / CC IE Field | × | × | × | × | × |
| MELSECNET/H | × | × | × | × | × |
| Ethernet | × | × | × | × | × |
| シリアルコミュニケーション | × | × | × | × | × |
| CC-Link | × | × | × | × | × |

**経由局CPU: Q/L/FX系**

接続局CPU: LCPU ○(1)

| 経由ネットワーク | QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU*1 | FXCPU |
|---|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × | × |
| CC IE Control / CC IE Field | × | × | × | × | × | × |
| MELSECNET/H | × | × | × | × | × | × |
| Ethernet | ○(2) | × | ○(2) | × | × | × |
| シリアルコミュニケーション | ○(3)*2 | × | ○(3)*2 | × | × | × |
| CC-Link | ○(4) | × | ○(4) | × | × | × |

> *1 Q172D，Q173D，Q172DS，Q173DSのみアクセス可能です。
> *2 二重化CPUの場合，基本ベースユニット上にあるシリアルコミュニケーションユニットにはアクセスできません。

### プロパティ一覧 (10.2 / 223 / 原本 p.225)
各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActConnectUnitNumber | 0(0x00) | 0(0x00)固定 | 接続局側ユニット局番 | 0(0x00)固定 | 0(0x00)固定 |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | (同左) | (同左) | (同左) |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) |
| ActDestinationPortNumber | 0(0x00) | 5001 | (同左) | (同左) | (同左) |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActHostAddress | 1.1.1.1 | 接続局側ユニットのホスト名またはIPアドレス | (同左) | (同左) | (同左) |
| ActIONumber*1 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 接続局側経由ユニットI/Oアドレス | 接続局側経由ユニットI/Oアドレス |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber*3 | 0(0x00) | 対象局側ユニットネットワークNo. | 対象局側ユニットネットワークNo. | 接続局側Lシリーズ対応E71ネットワークNo. | 接続局側Lシリーズ対応E71ネットワークNo. |
| ActParity | 1(ODD_PARITY) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActPassword | あき | 接続局側のLシリーズ対応E71に設定されたパスワード | (同左) | (同左) | (同左) |
| ActPortNumber*4 | 1(PORT_1) | パソコン側ポート番号 | (同左) | (同左) | (同左) |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_UDPIP(0x08) | (同左) | (同左) | (同左) |
| ActSourceNetworkNumber | 0(0x00) | パソコン側ネットワークNo. | (同左) | (同左) | (同左) |
| ActSourceStationNumber*5 | 0(0x00) | パソコン側局番 | (同左) | (同左) | (同左) |
| ActStationNumber*3 | 255(0xFF) | 対象局側ユニット局番 | 対象局側ユニット局番 | 接続局側Lシリーズ対応E71局番 | 接続局側Lシリーズ対応E71局番 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | (同左) | (同左) | (同左) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | (同左) | (同左) | (同左) |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_LJ71E71(0x5C) | (同左) | (同左) | (同左) |
※「(同左)」は，原本でそのセルが左隣のセルと結合されている(同じ値)ことを示す。

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2
> *3 プロパティのパターンが(1)または(2)の場合，ActNetworkNumberおよびActStationNumberは対象局側のパラメータで設定した値を指定してください。
> *4 ActPortNumberの1～1024までは使用しないでください。
> *5 Ethernetの同一ループ内でのLシリーズ対応E71に設定した局番と重複しないように，パソコン側の局番を指定してください。
(脚注は原本 p.226)

---

## 接続局がMELSEC iQ-RシリーズCPUユニットのEthernet通信(TCP) (10.2 / 225-228 / 原本 p.227-230)

### 構成 (10.2 / 225 / 原本 p.227)
【図】構成 — パソコン ― 接続局CPU(内蔵Ethernetポート)。接続局CPU側の経由ユニット ― 経由ネットワーク ― 経由ユニット［経由局CPU］

### アクセス可否およびプロパティのパターン (10.2 / 225-226 / 原本 p.227-228)
○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

**接続局CPU: RCPU/RCCPU/RモーションCPU → 経由局CPU: MELSEC iQ-R/LH/FX5系**

接続局CPU: RCPU ○(1)，RCCPU ○(1)*3，RモーションCPU ○(1)*1*3

| 経由ネットワーク | RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|
| CC IE TSN | ○(2) | × | × | × | × |
| CC IE Control / CC IE Field | ○(2)*2 | ○(2) | × | × | ○(2)*5 |
| MELSECNET/H | × | × | × | × | × |
| Ethernet | ○(2)*4 | × | ○(2)*4 | × | × |
| シリアルコミュニケーション | ○(3)*4 | × | ○(3)*4 | × | × |
| CC-Link | ○(4) | ○(4) | ○(4) | × | ○(4) |

**接続局CPU: RCPU/RCCPU/RモーションCPU → 経由局CPU: Q/L/FX系**

接続局CPU: RCPU ○(1)，RCCPU ○(1)*3，RモーションCPU ○(1)*1*3

| 経由ネットワーク | QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × | × |
| CC IE Control / CC IE Field | ○(2)*4 | × | ○(2)*2*4 | × | × | × |
| MELSECNET/H | ○(2)*4 | × | × | × | × | × |
| Ethernet | ○(2)*4 | × | ○(2) | × | × | × |
| シリアルコミュニケーション | ○(3)*4 | × | ○(3)*4 | × | × | × |
| CC-Link | ○(4)*4 | × | ○(4)*4 | × | × | × |

**接続局CPU: WinCPU → 経由局CPU: MELSEC iQ-R/LH/FX5系**

接続局CPU: WinCPU ○(1)

| 経由ネットワーク | RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × |
| CC IE Control / CC IE Field | × | × | × | × | × |
| MELSECNET/H | × | × | × | × | × |
| Ethernet | × | × | × | × | × |
| シリアルコミュニケーション | × | × | × | × | × |
| CC-Link | × | × | × | × | × |

**接続局CPU: WinCPU → 経由局CPU: Q/L/FX系** (原本 p.228)

接続局CPU: WinCPU ○(1)

| 経由ネットワーク | QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × | × |
| CC IE Control / CC IE Field | × | × | × | × | × | × |
| MELSECNET/H | × | × | × | × | × | × |
| Ethernet | × | × | × | × | × | × |
| シリアルコミュニケーション | × | × | × | × | × | × |
| CC-Link | × | × | × | × | × | × |

> *1 RモーションCPUを経由して経由局CPUにアクセスできません。
> *2 RCPU，LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
> *3 マルチCPU構成時の，2号機以降の場合のみアクセス可能です。
> *4 RCCPUは，通信経路が未サポートのためアクセスできません。
> *5 接続局CPUがRCPUのCC-Link IEフィールドネットワークのみアクセス可能です。
(脚注は原本 p.228)

### プロパティ一覧 (10.2 / 227 / 原本 p.229)
各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | (同左) | (同左) | (同左) |
| ActPortNumber | 1(PORT_1) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActParity | 1(ODD_PARITY) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActDestinationIONumber*1 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 指定なし: 1023(0x3FF) |
| ActDestinationPortNumber | 0(0x00) | 5007 | (同左) | (同左) | (同左) |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActHostAddress | 1.1.1.1 | 接続局側ユニットのホスト名またはIPアドレス | (同左) | (同左) | (同左) |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局<br>• RCPU，RモーションCPU，QCPU(Qモード)，LCPU: 1(0x01)<br>• 上記以外: 0(0x00) | 対象局<br>• RCPU，RモーションCPU，QCPU(Qモード)，LCPU: 1(0x01)<br>• 上記以外: 0(0x00) |
| ActIONumber*1 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 指定なし: 1023(0x3FF) | 接続局側経由ユニットI/Oアドレス | 接続局側経由ユニットI/Oアドレス |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber*3*4 | 0(0x00) | 0(0x00)固定 | 対象局側ユニットネットワークNo. | 0(0x00)固定 | 0(0x00)固定 |
| ActPassword | あき | 接続局に設定されたリモートパスワード | (同左) | (同左) | (同左) |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_TCPIP(0x05) | (同左) | (同左) | (同左) |
| ActStationNumber*3*4 | 255(0xFF) | 255(0xFF)固定 | 対象局側ユニット局番 | 255(0xFF)固定 | 255(0xFF)固定 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | (同左) | (同左) | MELSECNET/10を含まない: 0(0x00) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | (同左) | (同左) | (同左) |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_RETHER(0x1002) | (同左) | (同左) | (同左) |
※「(同左)」は，原本でそのセルが左隣のセルと結合されている(同じ値)ことを示す。

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2
> *3 プロパティのパターンが(2)の場合，ActNetworkNumberおよびActStationNumberは対象局側のパラメータで設定した値を指定してください。
> *4 Ethernetユニット(Qシリーズ対応E71およびMELSEC iQ-Rシリーズ対応E71)経由のアクセスは，下記の事項に注意してください。
> • ActNetworkNumber，ActStationNumberは，対象局側のQシリーズ対応E71およびMELSEC iQ-Rシリーズ対応E71のパラメータ設定で設定した値を指定してください。
> • Qシリーズ対応E71およびMELSEC iQ-Rシリーズ対応E71のパラメータ設定の「局番⇔IP関連情報」を設定してください。また，設定を行う際，「局番⇔IP関連情報設定方式」は自動応答方式以外(IPアドレス算出方式，テーブル変換方式，併用方式のいずれか)を指定してください。
(脚注は原本 p.230)

---

## 接続局がMELSEC iQ-RシリーズCPUユニットのEthernet通信(UDP) (10.2 / 229-232 / 原本 p.231-234)

### 構成 (10.2 / 229 / 原本 p.231)
【図】構成 — パソコン ― 接続局CPU(内蔵Ethernetポート)。接続局CPU側の経由ユニット ― 経由ネットワーク ― 経由ユニット［経由局CPU］

### アクセス可否およびプロパティのパターン (10.2 / 229-230 / 原本 p.231-232)
○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

**接続局CPU: RCPU/RCCPU/RモーションCPU → 経由局CPU: MELSEC iQ-R/LH/FX5系**

接続局CPU: RCPU ○(1)，RCCPU ○(1)*3，RモーションCPU ○(1)*1*3

| 経由ネットワーク | RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|
| CC IE TSN | ○(2) | × | × | × | × |
| CC IE Control / CC IE Field | ○(2)*2 | ○(2) | × | × | ○(2)*5 |
| MELSECNET/H | × | × | × | × | × |
| Ethernet | ○(2)*4 | × | ○(2)*4 | × | × |
| シリアルコミュニケーション | ○(3)*4 | × | ○(3)*4 | × | × |
| CC-Link | ○(4) | ○(4) | ○(4) | × | ○(4) |

**接続局CPU: RCPU/RCCPU/RモーションCPU → 経由局CPU: Q/L/FX系**

接続局CPU: RCPU ○(1)，RCCPU ○(1)*3，RモーションCPU ○(1)*1*3

| 経由ネットワーク | QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × | × |
| CC IE Control / CC IE Field | ○(2)*4 | × | ○(2)*2*4 | × | × | × |
| MELSECNET/H | ○(2)*4 | × | × | × | × | × |
| Ethernet | ○(2)*4 | × | ○(2)*4 | × | × | × |
| シリアルコミュニケーション | ○(3)*4 | × | ○(3)*4 | × | × | × |
| CC-Link | ○(4)*4 | × | ○(4)*4 | × | × | × |

**接続局CPU: WinCPU → 経由局CPU: MELSEC iQ-R/LH/FX5系**

接続局CPU: WinCPU ○(1)

| 経由ネットワーク | RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × |
| CC IE Control / CC IE Field | × | × | × | × | × |
| MELSECNET/H | × | × | × | × | × |
| Ethernet | × | × | × | × | × |
| シリアルコミュニケーション | × | × | × | × | × |
| CC-Link | × | × | × | × | × |

**接続局CPU: WinCPU → 経由局CPU: Q/L/FX系** (原本 p.232)

接続局CPU: WinCPU ○(1)

| 経由ネットワーク | QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × | × |
| CC IE Control / CC IE Field | × | × | × | × | × | × |
| MELSECNET/H | × | × | × | × | × | × |
| Ethernet | × | × | × | × | × | × |
| シリアルコミュニケーション | × | × | × | × | × | × |
| CC-Link | × | × | × | × | × | × |

> *1 RモーションCPUを経由して経由局CPUにアクセスできません。
> *2 RCPU，LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
> *3 マルチCPU構成時の，2号機以降の場合のみアクセス可能です。
> *4 RCCPUは，通信経路が未サポートのためアクセスできません。
> *5 接続局CPUがRCPUのCC-Link IEフィールドネットワークのみアクセス可能です。
(脚注は原本 p.232)

### プロパティ一覧 (10.2 / 231-232 / 原本 p.233-234)
各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | (同左) | (同左) | (同左) |
| ActPortNumber | 1(PORT_1) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActParity | 1(ODD_PARITY) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActDestinationIONumber*1 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 指定なし: 1023(0x3FF) |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局<br>• RCPU，RモーションCPU，QCPU(Qモード)，LCPU: 1(0x01)<br>• 上記以外: 0(0x00) | 対象局<br>• RCPU，RモーションCPU，QCPU(Qモード)，LCPU: 1(0x01)<br>• 上記以外: 0(0x00) |
| ActHostAddress | 1.1.1.1 | • IPアドレス指定通信時: 接続局側ユニットのホスト名またはIPアドレス<br>• IPアドレス指定なし直結通信時: 255.255.255.255 | (同左) | (同左) | (同左) |
| ActDestinationPortNumber | 0(0x00) | • IPアドレス指定通信時: 5006<br>• IPアドレス指定なし直結通信時: 5008 | (同左) | (同左) | (同左) |
| ActIONumber*1 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 指定なし: 1023(0x3FF) | 接続局側経由ユニットI/Oアドレス | 接続局側経由ユニットI/Oアドレス |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber*3*4 | 0(0x00) | 0(0x00)固定 | 対象局側ユニットネットワークNo. | 0(0x00)固定 | 0(0x00)固定 |
| ActPassword | あき | 接続局に設定されたリモートパスワード | (同左) | (同左) | (同左) |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_UDPIP(0x08) | (同左) | (同左) | (同左) |
| ActStationNumber*3*4 | 255(0xFF) | 255(0xFF)固定 | 対象局側ユニット局番 | 255(0xFF)固定 | 255(0xFF)固定 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | (同左) | (同左) | MELSECNET/10を含まない: 0(0x00) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | (同左) | (同左) | (同左) |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | • IPアドレス指定通信時: UNIT_RETHER(0x1002)<br>• IPアドレス指定なし直結通信時: UNIT_RETHER_DIRECT(0x1003) | (同左) | (同左) | (同左) |
※「(同左)」は，原本でそのセルが左隣のセルと結合されている(同じ値)ことを示す。
※ActUnitType の行は原本では次ページ(p.234)に続く表の最終行。原本の行順(ActIntelligentPreferenceBit → ActHostAddress → ActDestinationPortNumber)のまま転記。

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2
> *3 プロパティのパターンが(2)の場合，ActNetworkNumberおよびActStationNumberは対象局側のパラメータで設定した値を指定してください。
> *4 Ethernetユニット(MELSEC iQ-Rシリーズ対応E71)経由のアクセスは，下記の事項に注意してください。
> • ActNetworkNumber，ActStationNumberは，対象局側のMELSEC iQ-Rシリーズ対応E71のパラメータ設定で設定した値を指定してください。
> • MELSEC iQ-Rシリーズ対応E71のパラメータ設定の「局番⇔IP関連情報」を設定してください。また，設定を行う際，「局番⇔IP関連情報設定方式」は自動応答方式以外(IPアドレス算出方式，テーブル変換方式，併用方式のいずれか)を指定してください。
(脚注は原本 p.234)

---

## 接続局がLHCPUのEthernet通信(TCP) (10.2 / 233-234 / 原本 p.235-236)

### 構成 (10.2 / 233 / 原本 p.235)
【図】構成 — パソコン ― 接続局CPU(内蔵Ethernetポート)。接続局CPU側の経由ユニット ― 経由ネットワーク ― 経由ユニット［経由局CPU］

### アクセス可否およびプロパティのパターン (10.2 / 233 / 原本 p.235)
○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

**経由局CPU: MELSEC iQ-R/LH/FX5系**

接続局CPU: LHCPU ○(1)

| 経由ネットワーク | RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × |
| CC IE Control / CC IE Field | × | × | × | × | × |
| MELSECNET/H | × | × | × | × | × |
| Ethernet | × | × | × | × | × |
| シリアルコミュニケーション | × | × | × | × | × |
| CC-Link | × | × | × | × | × |

**経由局CPU: Q/L/FX系**

接続局CPU: LHCPU ○(1)

| 経由ネットワーク | QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × | × |
| CC IE Control / CC IE Field | × | × | × | × | × | × |
| MELSECNET/H | × | × | × | × | × | × |
| Ethernet | × | × | × | × | × | × |
| シリアルコミュニケーション | × | × | × | × | × | × |
| CC-Link | × | × | × | × | × | × |


### プロパティ一覧 (10.2 / 234 / 原本 p.236)
各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) |
|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ |
| ActPortNumber | 1(PORT_1) | 0(0x00)固定 |
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 |
| ActParity | 1(ODD_PARITY) | 0(0x00)固定 |
| ActDestinationPortNumber | 0(0x00) | 5007 |
| ActHostAddress | 1.1.1.1 | 接続局側ユニットのホスト名またはIPアドレス |
| ActIONumber | 1023(0x3FF) | ■シングルCPU時<br>1023(0x3FF)固定 |
| ActPassword | あき | 接続局に設定されたリモートパスワード |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_TCPIP(0x05) |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) |
| ActTimeOut | 10000 | ms単位でユーザ任意 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_LHETHER(0x1002) |


---

## 接続局がLHCPUのEthernet通信(UDP) (10.2 / 235-236 / 原本 p.237-238)

### 構成 (10.2 / 235 / 原本 p.237)
【図】構成 — パソコン ― 接続局CPU(内蔵Ethernetポート)。接続局CPU側の経由ユニット ― 経由ネットワーク ― 経由ユニット［経由局CPU］

### アクセス可否およびプロパティのパターン (10.2 / 235 / 原本 p.237)
○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

**経由局CPU: MELSEC iQ-R/LH/FX5系**

接続局CPU: LHCPU ○(1)

| 経由ネットワーク | RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × |
| CC IE Control / CC IE Field | × | × | × | × | × |
| MELSECNET/H | × | × | × | × | × |
| Ethernet | × | × | × | × | × |
| シリアルコミュニケーション | × | × | × | × | × |
| CC-Link | × | × | × | × | × |

**経由局CPU: Q/L/FX系**

接続局CPU: LHCPU ○(1)

| 経由ネットワーク | QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × | × |
| CC IE Control / CC IE Field | × | × | × | × | × | × |
| MELSECNET/H | × | × | × | × | × | × |
| Ethernet | × | × | × | × | × | × |
| シリアルコミュニケーション | × | × | × | × | × | × |
| CC-Link | × | × | × | × | × | × |


### プロパティ一覧 (10.2 / 236 / 原本 p.238)
各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) |
|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ |
| ActPortNumber | 1(PORT_1) | 0(0x00)固定 |
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 |
| ActParity | 1(ODD_PARITY) | 0(0x00)固定 |
| ActDestinationPortNumber | 0(0x00) | • IPアドレス指定通信時: 5006<br>• IPアドレス指定なし直結通信時: 5008 |
| ActHostAddress | 1.1.1.1 | • IPアドレス指定通信時: 接続局側ユニットのホスト名またはIPアドレス<br>• IPアドレス指定なし直結通信時: 255.255.255.255 |
| ActIONumber | 1023(0x3FF) | ■シングルCPU時<br>1023(0x3FF)固定 |
| ActPassword | あき | 接続局に設定されたリモートパスワード |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_UDPIP(0x08) |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) |
| ActTimeOut | 10000 | ms単位でユーザ任意 |
| ActUnitType | 0x13(UNIT_QNCPU) | • IPアドレス指定通信時: UNIT_LHETHER(0x1002)<br>• IPアドレス指定なし直結通信時: UNIT_LHETHER_DIRECT(0x1003) |


---

## 接続局がFX5CPUのEthernet通信(TCP) (10.2 / 237-238 / 原本 p.239-240)

### 構成 (10.2 / 237 / 原本 p.239)
【図】構成 — パソコン ― 接続局CPU(内蔵Ethernetポート)。接続局CPU側の経由ユニット ― 経由ネットワーク ― 経由ユニット［経由局CPU］

### アクセス可否およびプロパティのパターン (10.2 / 237 / 原本 p.239)
○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

**経由局CPU: MELSEC iQ-R/LH/FX5系**

接続局CPU: FX5CPU ○(1)

| 経由ネットワーク | RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × |
| CC IE Control / CC IE Field | × | × | × | × | ○(2)*1*2 |
| MELSECNET/H | × | × | × | × | × |
| Ethernet | × | × | × | × | × |
| シリアルコミュニケーション | × | × | × | × | × |
| CC-Link | × | × | × | × | ○(3) |

**経由局CPU: Q/L/FX系**

接続局CPU: FX5CPU ○(1)

| 経由ネットワーク | QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × | × |
| CC IE Control / CC IE Field | × | × | × | × | × | × |
| MELSECNET/H | × | × | × | × | × | × |
| Ethernet | × | × | × | × | × | × |
| シリアルコミュニケーション | × | × | × | × | × | × |
| CC-Link | × | × | × | × | × | × |

> *1 CC-Link IEフィールドネットワークのみアクセス可能です。
> *2 FX5SCPUにはアクセスできません。

### プロパティ一覧 (10.2 / 238 / 原本 p.240)
各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) |
|---|---|---|---|---|
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 | (同左) | (同左) |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 | (同左) | (同左) |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | (同左) | (同左) |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 | (同左) | (同左) |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | (同左) | 1023(0x3FF) |
| ActDestinationPortNumber | 0(0x00) | 5562 | (同左) | (同左) |
| ActDidPropertyBit | 1(0x01) | 1(0x01) | (同左) | 0(0x00) |
| ActDsidPropertyBit | 1(0x01) | 1(0x01) | (同左) | 0(0x00) |
| ActHostAddress | 1.1.1.1 | 接続局側ユニットのホスト名またはIPアドレス | (同左) | (同左) |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00) | (同左) | 1(0x01) |
| ActIONumber | 1023(0x3FF) | 1023(0x3FF) | (同左) | 接続局ユニット番号 |
| ActNetworkNumber | 0(0x00) | 0(0x00) | 対象局側ユニットネットワークNo. | 0(0x00) |
| ActPassword | あき | 接続局に設定されたリモートパスワード | (同左) | (同左) |
| ActPortNumber | 1(PORT_1) | 0(0x00) | (同左) | (同左) |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_TCPIP(0x05) | (同左) | (同左) |
| ActStationNumber | 255(0xFF) | 255(0xFF) | 対象局側ユニット局番 | 255(0xFF) |
| ActThroughNetworkType | 0(0x00) | 1(0x01) | 0(0x00) | (同左) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | (同左) | (同左) |
| ActUnitNumber | 0(0x00) | 0(0x00) | (同左) | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_FXVETHER(0x2001) | (同左) | (同左) |
| ActParity | 1(ODD_PARITY) | 0(0x00)固定 | (同左) | (同左) |
※「(同左)」は，原本でそのセルが左隣のセルと結合されている(同じ値)ことを示す。
※原本の行順(ActParity が最終行)のまま転記。

---

## 接続局がFX5CPUのEthernet通信(UDP) (10.2 / 239-240 / 原本 p.241-242)

### 構成 (10.2 / 239 / 原本 p.241)
【図】構成 — パソコン ― 接続局CPU(内蔵Ethernetポート)。接続局CPU側の経由ユニット ― 経由ネットワーク ― 経由ユニット［経由局CPU］

### アクセス可否およびプロパティのパターン (10.2 / 239 / 原本 p.241)
○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

**経由局CPU: MELSEC iQ-R/LH/FX5系**

接続局CPU: FX5CPU ○(1)

| 経由ネットワーク | RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × |
| CC IE Control / CC IE Field | × | × | × | × | ○(2)*1*2 |
| MELSECNET/H | × | × | × | × | × |
| Ethernet | × | × | × | × | × |
| シリアルコミュニケーション | × | × | × | × | × |
| CC-Link | × | × | × | × | ○(3) |

**経由局CPU: Q/L/FX系**

接続局CPU: FX5CPU ○(1)

| 経由ネットワーク | QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × | × |
| CC IE Control / CC IE Field | × | × | × | × | × | × |
| MELSECNET/H | × | × | × | × | × | × |
| Ethernet | × | × | × | × | × | × |
| シリアルコミュニケーション | × | × | × | × | × | × |
| CC-Link | × | × | × | × | × | × |

> *1 CC-Link IEフィールドネットワークのみアクセス可能です。
> *2 FX5SCPUにはアクセスできません。

### プロパティ一覧 (10.2 / 240 / 原本 p.242)
各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) |
|---|---|---|---|---|
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 | (同左) | (同左) |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 | (同左) | (同左) |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | (同左) | (同左) |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 | (同左) | (同左) |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | (同左) | 1023(0x3FF) |
| ActDestinationPortNumber | 0(0x00) | 5560 | (同左) | (同左) |
| ActDidPropertyBit | 1(0x01) | 1(0x01) | (同左) | 0(0x00) |
| ActDsidPropertyBit | 1(0x01) | 1(0x01) | (同左) | 0(0x00) |
| ActHostAddress | 1.1.1.1 | 255.255.255.255<br>PC側のアダプタ選択を行う場合には，接続先IPアドレスの後にタブ文字とパソコン側IPアドレスを付与する | (同左) | (同左) |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | (同左) | 1(0x01) |
| ActIONumber | 1023(0x3FF) | 1023(0x3FF) | (同左) | 接続局ユニット番号 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニットネットワークNo. | 0(0x00)固定 |
| ActPassword | あき | 接続局に設定されたリモートパスワード | (同左) | (同左) |
| ActPortNumber | 1(PORT_1) | 0(0x00) | (同左) | (同左) |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_UDPIP(0x08) | (同左) | (同左) |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 対象局側ユニット局番 | 255(0xFF)固定 |
| ActThroughNetworkType | 0(0x00) | 1(0x01) | 0(0x00)固定 | (同左) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | (同左) | (同左) |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | (同左) | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_FXVETHER_DIRECT(0x2002) | (同左) | (同左) |
| ActParity | 1(ODD_PARITY) | 0(0x00) | (同左) | (同左) |
※「(同左)」は，原本でそのセルが左隣のセルと結合されている(同じ値)ことを示す。
※原本の行順(ActParity が最終行)のまま転記。「固定」の付く・付かないも原本どおり(TCPの表とは表記が異なる)。
※要確認: ActParity の設定値は原本では「0(0x00)」(「固定」なし)。TCPの表(p.240)では「0(0x00)固定」。
