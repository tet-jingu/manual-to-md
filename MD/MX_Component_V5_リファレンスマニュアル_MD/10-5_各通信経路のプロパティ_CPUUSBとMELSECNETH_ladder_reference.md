# MX Component Version 5 リファレンスマニュアル 10章 各通信経路で設定するプロパティ (5/9) p.294-316

| 項目 | 内容 |
|---|---|
| 原本 | 【三菱】MX Component Version 5 リファレンスマニュアル (SH-082394J) |
| メーカー | 三菱電機 |
| 原本ファイル | `PDF/【三菱】MX Component Version 5 リファレンスマニュアル_sh082394j.pdf` (全696ページ) |
| 本ファイルの範囲 | 10.4 CPU USB通信，10.5 MELSECNET/H通信 (印刷ページ 292-314 / PDF p.294-316) |
| 出典表記 | `(節 / 印刷ページ / 原本 p.PDFページ)` |
| 作成日 | 2026-11-03 |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。
> 本文中の「○ページ」はすべて原本の**印刷ページ番号**です(PDFページ = 印刷ページ + 2)。
> 原本の表で複数列にまたがるセル(結合セル)は，該当する各列に同じ値を展開して記載しています。

## 主要用語 対訳表 (Glossary)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| 接続局CPU | Connected station CPU | — | 参考訳 |
| 経由ネットワーク | Relay network | — | 参考訳 |
| 経由局CPU | Relay station CPU | — | 参考訳 |
| 経由ユニット | Relay module | — | 参考訳 |
| 自ボード | Own board | MELSECNET/Hボード | 参考訳 |
| アクセス可否 | Accessibility | ○ / × | 参考訳 |
| プロパティのパターン | Property pattern | (1)〜(4) | 参考訳 |
| デフォルト値 | Default value | — | 参考訳 |
| 対象局 | Target station | — | 参考訳 |
| シングルCPU / マルチCPU / 二重化CPU | Single CPU / Multiple CPU / Redundant CPU | — | 参考訳 |
| 接続号機 / 管理CPU | Connected CPU number / Control CPU | — | 参考訳 |
| 制御系 | Control system | 976(0x3D0) | 参考訳 |
| I/Oアドレス | I/O address | 実際のI/O先頭No.÷16 | 参考訳 |
| マルチドロップチャネルNo. | Multidrop channel No. | ActMultiDropChannelNumber | 参考訳 |
| 局番↔IP関連情報設定方式 | Station No.↔IP information setting method | 自動応答方式 / IPアドレス算出方式 / テーブル変換方式 / 併用方式 | 参考訳 |
| CPU USB通信 | CPU USB communication | PROTOCOL_USB | 参考訳 |
| MELSECNET/H通信 | MELSECNET/H communication | PROTOCOL_MNETH(0x0F) | 参考訳 |
| ユニットタイプ | Unit type | ActUnitType (UNIT_RUSB / UNIT_LHUSB / UNIT_FXVUSB / UNIT_QNUSB / UNIT_LNUSB / UNIT_QSUSB / UNIT_QNMOTIONUSB / UNIT_FXCPU / UNIT_MNETHBOARD) | 参考訳 |
| プロトコルタイプ | Protocol type | ActProtocolType | 参考訳 |
| インバータ / ロボットコントローラ | Inverter / Robot controller | ActMxUnitSeries 1 / 2 | 参考訳 |
| 受信タイムアウト時間 / 送信タイムアウト時間 | Receive timeout / Send timeout | ActTimeOut / ActCpuTimeOut | 参考訳 |
| リトライ回数 | Retry count | ActMultiDropChannelNumber(ロボット) | 参考訳 |
| プログラム設定タイプ / ユーティリティ設定タイプ | Program setting type / Utility setting type | — | 参考訳 |

## 変換範囲表

| 原本ページ(PDF) | 印刷ページ | 節 | 扱い |
|---|---|---|---|
| p.294-313 | 292-311 | 10.4 CPU USB通信(11の接続局パターン) | 全文(構成図は文章化) |
| p.314-316 | 312-314 | 10.5 MELSECNET/H通信 | 全文(構成図は文章化) |
| p.192-293 | 190-291 | 10.1〜10.3 | 別ファイル(10-1〜10-4) |
| p.317-417 | 315-415 | 10.6〜10.16 | 別ファイル(10-6〜10-9) |
| p.1-191，p.418-696 | — | 前付け・1〜9章・11章以降 | 別ファイルまたは**未変換** |

## 目次

- 10.4 CPU USB通信
  - 接続局がRCPUのCPU USB通信
  - 接続局がRモーションCPUのCPU USB通信
  - 接続局がLHCPUのCPU USB通信
  - 接続局がFX5CPUのCPU USB通信
  - 接続局がQCPU(Qモード)のCPU USB通信
  - 接続局がLCPUのCPU USB通信
  - 接続局がQSCPUのCPU USB通信
  - 接続局がQモーションCPUのCPU USB通信
  - 接続局がFXCPUのCPU USB通信
  - 接続局がインバータのCPU USB通信
  - 接続局がロボットコントローラのCPU USB通信
- 10.5 MELSECNET/H通信

---

## 10.4 CPU USB通信 (10.4 / 292-311 / 原本 p.294-313)

### 接続局がRCPUのCPU USB通信 (10.4 / 292-294 / 原本 p.294-296)

#### 構成 (10.4 / 292 / 原本 p.294)

【図】構成 (10.4 / 292 / 原本 p.294): パソコン ― 接続局CPU(＋経由ユニット) ― 経由ネットワーク ― 経由局CPU(＋経由ユニット)

#### アクセス可否およびプロパティのパターン (10.4 / 292 / 原本 p.294)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: RCPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | ○(2) | × | × | × | × |
|  | CC IE Control<br>CC IE Field | ○(2)*1 | ○(2) | × | × | ○(2)*2 |
|  | MELSECNET/H | × | × | × | × | × |
|  | Ethernet | ○(2) | × | ○(2) | × | × |
|  | シリアルコミュニケーション | ○(3) | × | ○(3) | × | × |
|  | CC-Link | ○(4) | ○(4) | ○(4) | × | ○(4) |

| 接続局CPU: RCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | ○(2) | × | ○(2)*1 | × | × | × |
|  | MELSECNET/H | × | × | × | × | × | × |
|  | Ethernet | ○(2) | × | ○(2) | × | × | × |
|  | シリアルコミュニケーション | ○(3) | × | ○(3) | × | × | × |
|  | CC-Link | ○(4) | × | ○(4) | × | × | × |

> *1 RCPU，LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
>
> *2 CC-Link IEフィールドネットワークのみアクセス可能です。

#### プロパティ一覧 (10.4 / 293-294 / 原本 p.295-296)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2)*1 | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDestinationIONumber*2 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 指定なし: 1023(0x3FF) |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00) | 0(0x00) |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00) | 0(0x00) |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局<br>• RCPU，QCPU(Qモード)，LCPU : 1(0x01)<br>• 上記以外 : 0(0x00) | 対象局<br>• RCPU，QCPU(Qモード)，LCPU: 1(0x01)<br>• 上記以外 : 0(0x00) |
| ActIONumber*2 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 指定なし: 1023(0x3FF) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 指定なし: 1023(0x3FF) | 接続局側ユニットI/Oアドレス | 接続局側ユニットI/Oアドレス |
| ActMultiDropChannelNumber*3 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニットネットワークNo. | 0(0x00)固定 | 0(0x00)固定 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USB | PROTOCOL_USB | PROTOCOL_USB | PROTOCOL_USB |
| ActPacketType | 0x01(PACKET_PLC1) | PACKET_PLC1 | PACKET_PLC1 | PACKET_PLC1 | PACKET_PLC1 |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 対象局側ユニット局番 | 255(0xFF)固定 | 255(0xFF)固定 |
| ActConnectUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActPortNumber | 1(PORT_1) | 1(PORT_1)固定 | 1(PORT_1)固定 | 1(PORT_1)固定 | 1(PORT_1)固定 |
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActHostAddress | 1.1.1.1 | NULL固定 | NULL固定 | NULL固定 | NULL固定 |
| ActCpuTimeOut | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActParity | 1(ODD_PARITY) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActStopBits | 0(STOPBIT_ONE) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActSumCheck | 0(NO_SUM_CHECK) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActSourceNetworkNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActSourceStationNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDestinationPortNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | MELSECNET/10を含まない: 0(0x00) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_RUSB | UNIT_RUSB | UNIT_RUSB | UNIT_RUSB |

※原本の表は p.295〜p.296 の2ページにまたがる1つの表(ActThroughNetworkType以降がp.296)。

> *1 Ethernetユニット(MELSEC iQ-Rシリーズ対応E71)経由のアクセスは，下記の事項に注意してください。
>
> · ActNetworkNumber，ActStationNumberは，対象局側のMELSEC iQ-Rシリーズ対応E71のパラメータ設定で設定した値を指定してください。
>
> · MELSEC iQ-Rシリーズ対応E71のパラメータ設定の「局番⇔IP関連情報」を設定してください。また，設定を行う際，「局番⇔IP関連情報設定方式」は自動応答方式以外(IPアドレス算出方式，テーブル変換方式，併用方式のいずれか)を指定してください。
>
> *2 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
>
> *3 マルチドロップリンクするチャネルNo.は下記を指定してください。
>
> 0: ユニットのデフォルトチャネルを使用
>
> 1: チャネル1
>
> 2: チャネル2

### 接続局がRモーションCPUのCPU USB通信 (10.4 / 295-296 / 原本 p.297-298)

#### 構成 (10.4 / 295 / 原本 p.297)

【図】構成 (10.4 / 295 / 原本 p.297): パソコン ― 接続局CPU(＋経由ユニット) ― 経由ネットワーク ― 経由局CPU(＋経由ユニット)

#### アクセス可否およびプロパティのパターン (10.4 / 295 / 原本 p.297)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: RモーションCPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1)*1*2 | CC IE TSN | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | × | × | × | × | × |
|  | MELSECNET/H | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × |
|  | CC-Link | × | × | × | × | × |

| 接続局CPU: RモーションCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1)*1*2 | CC IE TSN | × | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
|  | MELSECNET/H | × | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × | × |
|  | CC-Link | × | × | × | × | × | × |

> *1 RモーションCPUを経由して経由局CPUにアクセスできません。
>
> *2 マルチCPU構成時の，2号機以降の場合のみアクセス可能です。

#### プロパティ一覧 (10.4 / 296 / 原本 p.298)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) |
|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ |
| Act DestinationIONumber | 0(0x00) | 0(0x00)固定 |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 |
| Act IntelligentPreference Bit | 0(0x00) | 0(0x00)固定 |
| ActIONumber | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 指定なし: 1023(0x3FF) |
| ActMultiDropChannelNumber*1 | 0(0x00) | 0(0x00)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USB |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) |
| ActTimeOut | 10000 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_RUSB |

※「Act DestinationIONumber」「Act IntelligentPreference Bit」のスペースは原本表記のまま。

> *1 マルチドロップリンクするチャネルNo.は下記を指定してください。
>
> 0: ユニットのデフォルトチャネルを使用
>
> 1: チャネル1
>
> 2: チャネル2

### 接続局がLHCPUのCPU USB通信 (10.4 / 297-298 / 原本 p.299-300)

#### 構成 (10.4 / 297 / 原本 p.299)

【図】構成 (10.4 / 297 / 原本 p.299): パソコン ― 接続局CPU(＋経由ユニット) ― 経由ネットワーク ― 経由局CPU(＋経由ユニット)

#### アクセス可否およびプロパティのパターン (10.4 / 297 / 原本 p.299)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: LHCPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | × | × | × | × | × |
|  | MELSECNET/H | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × |
|  | CC-Link | × | × | × | × | × |

| 接続局CPU: LHCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
|  | MELSECNET/H | × | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × | × |
|  | CC-Link | × | × | × | × | × | × |

#### プロパティ一覧 (10.4 / 298 / 原本 p.300)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) |
|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 |
| ActIONumber | 1023(0x3FF) | ■シングルCPU時<br>1023(0x3FF)固定 |
| ActMultiDropChannelNumber | 0(0x00) | 0(0x00)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USB |
| ActPacketType | 0x01(PACKET_PLC1) | PACKET_PLC1 |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 |
| ActConnectUnitNumber | 0(0x00) | 0(0x00)固定 |
| ActPortNumber | 1(PORT_1) | 1(PORT_1)固定 |
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 |
| ActHostAddress | 1.1.1.1 | NULL固定 |
| ActCpuTimeOut | 0(0x00) | 0(0x00)固定 |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 |
| ActParity | 1(ODD_PARITY) | 0(0x00)固定 |
| ActStopBits | 0(STOPBIT_ONE) | 0(0x00)固定 |
| ActSumCheck | 0(NO_SUM_CHECK) | 0(0x00)固定 |
| ActSourceNetworkNumber | 0(0x00) | 0(0x00)固定 |
| ActSourceStationNumber | 0(0x00) | 0(0x00)固定 |
| ActDestinationPortNumber | 0(0x00) | 0(0x00)固定 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) |
| ActTimeOut | 10000 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_LHUSB |

### 接続局がFX5CPUのCPU USB通信 (10.4 / 299-300 / 原本 p.301-302)

#### 構成 (10.4 / 299 / 原本 p.301)

【図】構成 (10.4 / 299 / 原本 p.301): パソコン ― 接続局CPU(＋経由ユニット) ― 経由ネットワーク ― 経由局CPU(＋経由ユニット)

#### アクセス可否およびプロパティのパターン (10.4 / 299 / 原本 p.301)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: FX5CPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | × | × | × | × | ○(2)*2*3 |
|  | MELSECNET/H | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × |
|  | CC-Link | × | × | × | × | ○(3)*3 |

| 接続局CPU: FX5CPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
|  | MELSECNET/H | × | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × | × |
|  | CC-Link | × | × | × | × | × | × |

> *1 FX5UJCPU，FX5SCPUのみアクセス可能です。
>
> *2 CC-Link IEフィールドネットワークのみアクセス可能です。
>
> *3 FX5SCPUにはアクセスできません。

#### プロパティ一覧 (10.4 / 300 / 原本 p.302)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) |
|---|---|---|---|---|
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActConnectUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActCpuTimeOut | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDataBits | 8(DATABIT_8) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 1023(0x3FF) |
| ActDestinationPortNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDidPropertyBit | 1(0x01) | 0(0x00) | 1(0x01) | 0(0x00) |
| ActDsidPropertyBit | 1(0x01) | 0(0x00) | 1(0x01) | 0(0x00) |
| ActHostAddress | 1.1.1.1 | 0(0x00) | 0(0x00) | 0(0x00) |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00) | 0(0x00) | 1(0x01) |
| ActIONumber | 1023(0x3FF) | 1023(0x3FF) | 1023(0x3FF) | 接続局ユニット番号 |
| ActNetworkNumber | 0(0x00) | 0(0x00) | 対象局側ユニットネットワークNo. | 0(0x00) |
| ActPacketType | 0x01(PACKET_PLC1) | 0x01(PACKET_PLC1)固定 | 0x01(PACKET_PLC1)固定 | 0x01(PACKET_PLC1)固定 |
| ActPassword | あき | NULL | NULL | NULL |
| ActPortNumber | 1(PORT_1) | 1(PORT_1)固定 | 1(PORT_1)固定 | 1(PORT_1)固定 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USB | PROTOCOL_USB | PROTOCOL_USB |
| ActSourceNetworkNumber | 0(0x00) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActSourceStationNumber | 0(0x00) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActStationNumber | 255(0xFF) | 255(0xFF) | 対象局側ユニット局番 | 255(0xFF) |
| ActStopBits | 0(STOPBIT_ONE) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActSumCheck | 0(NO_SUM_CHECK) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActThroughNetworkType | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActTimeOut | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00) | 0(0x00) | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_FXVUSB | UNIT_FXVUSB | UNIT_FXVUSB |

### 接続局がQCPU(Qモード)のCPU USB通信 (10.4 / 301-303 / 原本 p.303-305)

#### 構成 (10.4 / 301 / 原本 p.303)

【図】構成 (10.4 / 301 / 原本 p.303): パソコン ― 接続局CPU(＋経由ユニット) ― 経由ネットワーク ― 経由局CPU(＋経由ユニット)

#### アクセス可否およびプロパティのパターン (10.4 / 301-302 / 原本 p.303-304)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: QCPU(Qモード) | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | × | × | × | × | × |
|  | MELSECNET/H | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × |
|  | CC-Link | × | × | × | × | × |

| 接続局CPU: QCPU(Qモード) | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | ○(2) | ○(2)*1 | ○(2)*2 | ○(2)*1 | ○(2)*1 | × |
|  | MELSECNET/H | ○(2) | ○(2) | × | ○(2) | ○(2) | × |
|  | Ethernet | ○(2) | × | × | ○(2) | ○(2) | × |
|  | シリアルコミュニケーション | ○(3)*3 | × | ○(3) | × | ○(3) | × |
|  | CC-Link | ○(4) | ○(4) | ○(4) | × | ○(4) | ○(4)*4 |

| 接続局CPU: QCCPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | × | × | × | × | × |
|  | MELSECNET/H | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × |
|  | CC-Link | × | × | × | × | × |

| 接続局CPU: QCCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | ○(2) | ○(2)*1 | ○(2)*2 | ○(2)*1 | ○(2)*1 | × |
|  | MELSECNET/H | ○(2) | ○(2) | × | ○(2) | ○(2) | × |
|  | Ethernet | × | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × | × |
|  | CC-Link | ○(4) | ○(4) | ○(4) | × | ○(4) | × |

> *1 RモーションCPU，Q12DCCPU-V(基本機能モード)，QSCPU，QモーションCPUは，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。
>
> *2 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
>
> *3 二重化CPUの場合，基本ベースユニット上にあるシリアルコミュニケーションユニットにはアクセスできません。
>
> *4 FX3G(C)CPU，FX3U(C)CPUかつ自ネットワークのみサポートしています。

※脚注 *1〜*4 は原本 p.304 に記載(表は p.303)。

#### プロパティ一覧 (10.4 / 303 / 原本 p.305)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2)*1 | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局<br>• QCPU(Qモード)，LCPU: 1(0x01)<br>• 上記以外: 0(0x00) | 対象局<br>• QCPU(Qモード)，QCCPU，LCPU: 1(0x01)<br>• 上記以外: 0(0x00) |
| ActIONumber*2 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 接続局側ユニットI/Oアドレス | 接続局側ユニットI/Oアドレス |
| ActMultiDropChannelNumber*3 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニットネットワークNo. | 0(0x00)固定 | 0(0x00)固定 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USB(0x0D) | PROTOCOL_USB(0x0D) | PROTOCOL_USB(0x0D) | PROTOCOL_USB(0x0D) |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 対象局側ユニット局番 | 255(0xFF)固定 | 255(0xFF)固定 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_QNUSB(0x16) | UNIT_QNUSB(0x16) | UNIT_QNUSB(0x16) | UNIT_QNUSB(0x16) |

> *1 Ethernetユニット(Qシリーズ対応E71)経由のアクセスは，下記の事項に注意してください。
>
> · ActNetworkNumber，ActStationNumberは，対象局側のQシリーズ対応E71のパラメータ設定で設定した値を指定してください。
>
> · Qシリーズ対応E71のパラメータ設定の「局番⇔IP関連情報」を設定してください。また，設定を行う際，「局番⇔IP関連情報設定方式」は自動応答方式以外(IPアドレス算出方式，テーブル変換方式，併用方式のいずれか)を指定してください。
>
> *2 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
>
> *3 マルチドロップリンクするチャネルNo.は下記を指定してください。
>
> 0: ユニットのデフォルトチャネルを使用
>
> 1: チャネル1
>
> 2: チャネル2

### 接続局がLCPUのCPU USB通信 (10.4 / 304-306 / 原本 p.306-308)

#### 構成 (10.4 / 304 / 原本 p.306)

【図】構成 (10.4 / 304 / 原本 p.306): パソコン ― 接続局CPU(＋経由ユニット) ― 経由ネットワーク ― 経由局CPU(＋経由ユニット)

#### アクセス可否およびプロパティのパターン (10.4 / 304 / 原本 p.306)

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
>
> *2 Q12DCCPU-V(基本機能モード)は，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。
>
> *3 二重化CPUの場合，基本ベースユニット上にあるシリアルコミュニケーションユニットにはアクセスできません。

#### プロパティ一覧 (10.4 / 305-306 / 原本 p.307-308)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActConnectUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActCpuTimeOut | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 0(0x00)固定 |
| ActDestinationPortNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 | 1(0x01)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 | 1(0x01)固定 |
| ActHostAddress | 1.1.1.1 | NULL固定 | NULL固定 | NULL固定 | NULL固定 |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 対象局<br>QCPU(Qモード)，LCPU: 1(0x01)<br>上記以外: 0(0x00) | 対象局<br>QCPU(Qモード)，QCCPU，LCPU: 1(0x01)<br>上記以外: 0(0x00) | 0(0x00)固定 |
| ActIONumber*1 | 1023(0x3FF) | 1023(0x3FF)固定 | 接続局側ユニットI/Oアドレス | 接続局側ユニットI/Oアドレス | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 | 0(0x00)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニットネットワークNo. |
| ActPacketType | 0x01(PACKET_PLC1) | 0x01(PACKET_PLC1)固定 | 0x01(PACKET_PLC1)固定 | 0x01(PACKET_PLC1)固定 | 0x01(PACKET_PLC1)固定 |
| ActParity | 1(ODD_PARITY) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActPortNumber | 1(PORT_1) | 1(PORT_1)固定 | 1(PORT_1)固定 | 1(PORT_1)固定 | 1(PORT_1)固定 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USB(0x0D) | PROTOCOL_USB(0x0D) | PROTOCOL_USB(0x0D) | PROTOCOL_USB(0x0D) |
| ActSourceNetworkNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActSourceStationNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 255(0xFF)固定 | 255(0xFF)固定 | 対象局側ユニット局番 |
| ActStopBits | 0(STOPBIT_ONE) | 0(STOPBIT_ONE)固定 | 0(STOPBIT_ONE)固定 | 0(STOPBIT_ONE)固定 | 0(STOPBIT_ONE)固定 |
| ActSumCheck | 0(NO_SUM_CHECK) | 0(NO_SUM_CHECK)固定 | 0(NO_SUM_CHECK)固定 | 0(NO_SUM_CHECK)固定 | 0(NO_SUM_CHECK)固定 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 | 0(0x00)固定 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_LNUSB(0x51) | UNIT_LNUSB(0x51) | UNIT_LNUSB(0x51) | UNIT_LNUSB(0x51) |

※原本の表は p.307〜p.308 の2ページにまたがる1つの表(ActSumCheck以降がp.308)。

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
>
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
>
> 0: ユニットのデフォルトチャネルを使用
>
> 1: チャネル1
>
> 2: チャネル2

### 接続局がQSCPUのCPU USB通信 (10.4 / 307 / 原本 p.309)

#### 構成 (10.4 / 307 / 原本 p.309)

【図】構成 (10.4 / 307 / 原本 p.309): パソコン ― 接続局CPU(＋経由ユニット) ― 経由ネットワーク ― 経由局CPU(＋経由ユニット)

#### アクセス可否およびプロパティのパターン (10.4 / 307 / 原本 p.309)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: QSCPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | × | × | × | × | × |
|  | MELSECNET/H | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × |
|  | CC-Link | × | × | × | × | × |

| 接続局CPU: QSCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
|  | MELSECNET/H | × | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × | × |
|  | CC-Link | × | × | × | × | × | × |

> *1 QSCPUを経由して経由局CPUにアクセスできません。

#### プロパティ一覧 (10.4 / 307 / 原本 p.309)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) |
|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USB(0x0D) |
| ActTimeOut | 10000 | ms単位でユーザ任意 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_QSUSB(0x29) |

### 接続局がQモーションCPUのCPU USB通信 (10.4 / 308 / 原本 p.310)

#### 構成 (10.4 / 308 / 原本 p.310)

【図】構成 (10.4 / 308 / 原本 p.310): パソコン ― 接続局CPU(＋経由ユニット) ― 経由ネットワーク ― 経由局CPU(＋経由ユニット)

#### アクセス可否およびプロパティのパターン (10.4 / 308 / 原本 p.310)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: QモーションCPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | × | × | × | × | × |
|  | MELSECNET/H | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × |
|  | CC-Link | × | × | × | × | × |

| 接続局CPU: QモーションCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
|  | MELSECNET/H | × | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × | × |
|  | CC-Link | × | × | × | × | × | × |

> *1 Q172D，Q173D，Q172DS，Q173DSのみアクセス可能です。

#### プロパティ一覧 (10.4 / 308 / 原本 p.310)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) |
|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ |
| ActIONumber | 1023(0x3FF) | ■マルチCPU時<br>• 管理CPU: 1023(0x3FF)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USB(0x0D) |
| ActTimeOut | 10000 | ms単位でユーザ任意 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_QNMOTIONUSB(0x1D) |

### 接続局がFXCPUのCPU USB通信 (10.4 / 309 / 原本 p.311)

#### 構成 (10.4 / 309 / 原本 p.311)

【図】構成 (10.4 / 309 / 原本 p.311): パソコン ― 接続局CPU(＋経由ユニット) ― 経由ネットワーク ― 経由局CPU(＋経由ユニット)

#### アクセス可否およびプロパティのパターン (10.4 / 309 / 原本 p.311)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: FXCPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | × | × | × | × | × |
|  | MELSECNET/H | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × |
|  | CC-Link | × | × | × | × | × |

| 接続局CPU: FXCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
|  | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
|  | MELSECNET/H | × | × | × | × | × | × |
|  | Ethernet | × | × | × | × | × | × |
|  | シリアルコミュニケーション | × | × | × | × | × | × |
|  | CC-Link | × | × | × | × | × | ○(2)*1 |

> *1 FX3G(C)CPU，FX3U(C)CPUのみアクセス可能です。

#### プロパティ一覧 (10.4 / 309 / 原本 p.311)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) |
|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 1023(0x3FF) |
| ActIONumber | 1023(0x3FF) | 0(0x00)固定 | 接続局ユニット番号 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USB(0x0D) | PROTOCOL_USB(0x0D) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 対象局ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_FXCPU(0x0F) | UNIT_FXCPU(0x0F) |

### 接続局がインバータのCPU USB通信 (10.4 / 310 / 原本 p.312)

#### 構成 (10.4 / 310 / 原本 p.312)

【図】構成 (10.4 / 310 / 原本 p.312): パソコン ― インバータ(直結)

#### プロパティ一覧 (10.4 / 310 / 原本 p.312)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | プロパティのパターン |
|---|---|---|
| ActMxUnitSeries | 0(0x00) | 1(0x01) |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | COMM_USB(0x01) |
| ActStationNumber | 255(0xFF) | インバータの局番(0～31) |
| ActCpuType | 34(CPU_Q02CPU) | INV_A800(0x1E60)固定 |
| ActTimeOut | 10000 | ms単位でユーザ任意 |
| ActCpuTimeOut | 0(0x00) | 10ms単位でユーザ任意 |

> **Point**
> インバータ通信時は，プログラム設定タイプのコントロールは使用できません。
> ユーティリティ設定タイプのコントロールを使用してください。

### 接続局がロボットコントローラのCPU USB通信 (10.4 / 311 / 原本 p.313)

#### 構成 (10.4 / 311 / 原本 p.313)

【図】構成 (10.4 / 311 / 原本 p.313): パソコン ― ロボットコントローラ(直結)

#### プロパティ一覧 (10.4 / 311 / 原本 p.313)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | プロパティのパターン |
|---|---|---|
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | RC_PROTOCOL_USB(0x04) |
| ActCpuType | 34(CPU_Q02CPU) | ロボットコントローラ機種(0x013001) |
| ActTimeOut | 10000 | 受信タイムアウト時間(msec) |
| ActCpuTimeOut | 0(0x00) | 送信タイムアウト時間(msec) |
| ActMultiDropChannelNumber | 0(0x00) | リトライ回数 |
| ActMxUnitSeries | 0(0x00) | 2(0x02) |

> **Point**
> ロボットコントローラ通信時は，プログラム設定タイプのコントロールは使用できません。
> ユーティリティ設定タイプのコントロールを使用してください。

---

## 10.5 MELSECNET/H通信 (10.5 / 312-314 / 原本 p.314-316)

### 構成 (10.5 / 312 / 原本 p.314)

【図】構成 (10.5 / 312 / 原本 p.314): パソコン(MELSECNET/Hボード) ― MELSECNET/H ― 接続局CPU＋MELSECNET/Hユニット(＋経由ユニット) ― 経由ネットワーク ― 経由局CPU(＋経由ユニット)

### アクセス可否およびプロパティのパターン (10.5 / 312-313 / 原本 p.314-315)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 自ボード | 接続局CPU: QCPU(Qモード) | 接続局CPU: QSCPU | 接続局CPU: QモーションCPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|---|---|---|
| ○(1) | ○(2) | ○(2)*1*5 | ○(2)*1*5 | CC IE TSN | × | × | × | × | × |
|  |  |  |  | CC IE Control<br>CC IE Field | × | × | × | × | × |
|  |  |  |  | MELSECNET/H | × | × | × | × | × |
|  |  |  |  | Ethernet | × | × | × | × | × |
|  |  |  |  | シリアル<br>コミュニケーション | × | × | × | × | × |
|  |  |  |  | CC-Link | × | × | × | × | × |

| 自ボード | 接続局CPU: QCPU(Qモード) | 接続局CPU: QSCPU | 接続局CPU: QモーションCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU*5 | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|---|---|---|
| ○(1) | ○(2) | ○(2)*1*5 | ○(2)*1*5 | CC IE TSN | × | × | × | × | × | × |
|  |  |  |  | CC IE Control<br>CC IE Field | ○(2) | ○(2)*2 | ○(2)*3 | ○(2)*1*2 | × | × |
|  |  |  |  | MELSECNET/H | ○(2) | ○(2) | × | ○(2)*1 | × | × |
|  |  |  |  | Ethernet | ○(2) | × | × | ○(2)*1 | × | × |
|  |  |  |  | シリアル<br>コミュニケーション | ○(3)*4 | × | ○(3)*4 | × | ○(3) | × |
|  |  |  |  | CC-Link | ○(4) | ○(4) | ○(4) | × | ○(4) | × |

| 自ボード | 接続局CPU: QCCPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|---|
| ○(1) | ○(2)*6 | CC IE TSN | × | × | × | × | × |
|  |  | CC IE Control<br>CC IE Field | × | × | × | × | × |
|  |  | MELSECNET/H | × | × | × | × | × |
|  |  | Ethernet | × | × | × | × | × |
|  |  | シリアル<br>コミュニケーション | × | × | × | × | × |
|  |  | CC-Link | × | × | × | × | × |

| 自ボード | 接続局CPU: QCCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU*5 | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|---|
| ○(1) | ○(2)*6 | CC IE TSN | × | × | × | × | × | × |
|  |  | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
|  |  | MELSECNET/H | × | × | × | × | × | × |
|  |  | Ethernet | × | × | × | × | × | × |
|  |  | シリアル<br>コミュニケーション | × | × | × | × | × | × |
|  |  | CC-Link | ○(4) | ○(4) | ○(4) | × | ○(4) | × |

※接続局CPUがQCCPUの2つ目の表(経由局CPU: QCPU〜FXCPU)は原本 p.315。

> *1 QSCPUおよびQモーションCPUを経由して経由局CPUにアクセスできません。
>
> *2 Q12DCCPU-V(基本機能モード)，QSCPUは，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。
>
> *3 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
>
> *4 二重化CPUの場合，基本ベースユニット上にあるシリアルコミュニケーションユニットにはアクセスできません。
>
> *5 マルチCPU構成時の，2号機以降の場合のみアクセス可能です。
>
> *6 Q24DHCCPU-V，Q24DHCCPU-LS，Q24DHCCPU-VG，Q26DHCCPU-LSは，通信経路が未サポートのためアクセスできません。

### プロパティ一覧 (10.5 / 314 / 原本 p.316)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) |
| ActDidPropertyBit | 1(0x01) | 0(0x00)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 0(0x00)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActIONumber*1 | 1023(0x3FF) | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 接続局側経由ユニットI/Oアドレス | 接続局側経由ユニットI/Oアドレス |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニットネットワークNo. | 接続局側ユニットネットワークNo. | 接続局側ユニットネットワークNo. |
| ActPortNumber | 1(PORT_1) | パソコン側MELSECNET/Hボードのポート番号，PORT1～PORT4(1枚目～4枚目) | パソコン側MELSECNET/Hボードのポート番号，PORT1～PORT4(1枚目～4枚目) | パソコン側MELSECNET/Hボードのポート番号，PORT1～PORT4(1枚目～4枚目) | パソコン側MELSECNET/Hボードのポート番号，PORT1～PORT4(1枚目～4枚目) |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_MNETH(0x0F) | PROTOCOL_MNETH(0x0F) | PROTOCOL_MNETH(0x0F) | PROTOCOL_MNETH(0x0F) |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 対象局側ユニット局番 | 接続局側ユニット局番 | 接続局側ユニット局番 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_MNETHBOARD(0x1E) | UNIT_MNETHBOARD(0x1E) | UNIT_MNETHBOARD(0x1E) | UNIT_MNETHBOARD(0x1E) |

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
>
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
>
> 0: ユニットのデフォルトチャネルを使用
>
> 1: チャネル1
>
> 2: チャネル2

※要確認: 本範囲の全プロパティ一覧で ActCpuType のデフォルト値は「34(CPU_Q02CPU)」(原本表記のまま)。9章のCPUタイプ一覧に CPU_Q02CPU(34) の行は無い。
