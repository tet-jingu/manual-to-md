# MX Component Version 5 リファレンスマニュアル 10章 各通信経路で設定するプロパティ (7/9) p.340-364 (10.16 / 338-362 / 原本 p.340-364)

| 項目 | 内容 |
|---|---|
| 原本 | 【三菱】MX Component Version 5 リファレンスマニュアル (SH-082394J) |
| メーカー | 三菱電機 |
| 原本ファイル | `PDF/【三菱】MX Component Version 5 リファレンスマニュアル_sh082394j.pdf` (全696ページ) |
| 本ファイルの範囲 | 10章 10.16 GOTトランスペアレント通信 のうち，パソコン側ポート: USB / GOT2000側ポート: USB / CPU側ポート: 直結(1)〜(4)・バス・シリアルコミュニケーションユニット(1)〜(6) (印刷ページ 338-362 / PDF p.340-364) |
| 出典表記 | `(節 / 印刷ページ / 原本 p.PDFページ)` |
| 作成日 | 2026-11-03 |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。
> 本文中の「○ページ」はすべて原本の**印刷ページ番号**です(PDFページ = 印刷ページ + 2)。
> 表の読み方: 「アクセス可否」表の ○(n) の n が「プロパティ一覧」表のパターン列 ○(n) に対応します。原本で結合セル(複数パターン列で同じ値)は，本mdでは各列に同じ値を展開しています。
> ActCpuType のデフォルト値「34(CPU_Q02CPU)」は原本表記のまま(9章のCPU一覧に該当行が無い点は 09_ を参照)。

## 主要用語 対訳表 (Glossary)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| GOTトランスペアレント通信 | GOT transparent communication | PROTOCOL_USBGOT(0x13) | 参考訳 |
| パソコン側ポート / GOT側ポート / CPU側ポート | PC side port / GOT side port / CPU side port | — | 参考訳 |
| 直結 | Direct connection | — | 参考訳 |
| バス(接続) | Bus connection | UNIT_A900GOT(0x21) | 参考訳 |
| 接続局CPU | Connected station CPU | — | 参考訳 |
| 経由局CPU | Relay station CPU | — | 参考訳 |
| 経由ネットワーク | Relay network | — | 参考訳 |
| 経由ユニット | Relay module | — | 参考訳 |
| アクセス可否 | Accessibility | — | 参考訳 |
| プロパティのパターン | Property pattern | ○(n) | 参考訳 |
| デフォルト値 | Default value | — | 参考訳 |
| 対象局 / 対象局側 | Target station / Target station side | — | 参考訳 |
| シングルCPU / マルチCPU | Single CPU / Multiple CPU | 1号機: 992(0x3E0)〜4号機: 995(0x3E3) | 参考訳 |
| 接続号機 | Connected CPU No. | 1023(0x3FF) | 参考訳 |
| 二重化CPU / 制御系 | Redundant CPU / Control system | 976(0x3D0) | 参考訳 |
| マルチドロップリンク | Multidrop link | ActMultiDropChannelNumber | 参考訳 |
| マルチドロップチャネルNo. | Multidrop channel No. | 0/1/2 | 参考訳 |
| 独立モード | Independent mode | CH1/CH2 動作設定=独立(0) | 参考訳 |
| 伝送設定 / 動作設定 / 交信プロトコル設定 | Transmission setting / Operation setting / Communication protocol setting | — | 参考訳 |
| I/Oアドレス / I/O先頭No. | I/O address / Start I/O No. | ÷16 | 参考訳 |
| ユニット局番 / ユニットネットワークNo. | Module station No. / Module network No. | ActStationNumber / ActNetworkNumber | 参考訳 |
| MNET/10ルーチング情報 / ルーチング方式 | MNET/10 routing information / routing method | 自動応答方式以外 | 参考訳 |
| 自動応答方式 / IPアドレス算出方式 / テーブル変換方式 / 併用方式 | Automatic response / IP address computation / Table conversion / Combined method | — | 参考訳 |
| 固定 | Fixed | — | 参考訳 |
| CC IE TSN / CC IE Control / CC IE Field | CC-Link IE TSN / CC-Link IE Controller Network / CC-Link IE Field Network | — | 原本併記 |
| シリアルコミュニケーションユニット | Serial communication module | RJ71C24 / QJ71C24 / LJ71C24 | 参考訳 |

## 変換範囲表

| 原本ページ(PDF) | 印刷ページ | 節 | 扱い |
|---|---|---|---|
| p.340 | 338 | 10.16 GOTトランスペアレント通信 冒頭(Point) | 全文 |
| p.340-348 | 338-346 | USB/USB/直結(1)〜(4) | 全文(構成図は文章化) |
| p.349-351 | 347-349 | USB/USB/バス | 全文(構成図は文章化) |
| p.352-364 | 350-362 | USB/USB/シリアルコミュニケーションユニット(1)〜(6) | 全文(構成図は文章化) |
| p.192-339 | 190-337 | 10.1〜10.15 | 別ファイル(10-1〜10-6) |
| p.365-417 | 363-415 | 10.16 の残り(Ethernet系・GOT2000/3000・Ethernetボード経由) | 別ファイル(10-8, 10-9) |
| p.1-191, p.418-696 | — | 10章以外 | 別ファイル(01_〜09_) または **未変換** |

## 目次

- 10.16 GOTトランスペアレント通信
  - パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: 直結(1)
  - パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: 直結(2)
  - パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: 直結(3)
  - パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: 直結(4)
  - パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: バス
  - パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: シリアルコミュニケーションユニット(1)
  - パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: シリアルコミュニケーションユニット(2)
  - パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: シリアルコミュニケーションユニット(3)
  - パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: シリアルコミュニケーションユニット(4)
  - パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: シリアルコミュニケーションユニット(5)
  - パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: シリアルコミュニケーションユニット(6)

---

## 10.16 GOTトランスペアレント通信 (10.16 / 338-362 / 原本 p.340-364)

> **Point**
> 使用可能なシステム構成は，下記のマニュアルを参照してください。
> 📖使用するGOTの各接続マニュアル

### パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: 直結(1) (10.16 / 338-339 / 原本 p.340-341)

接続局がFX5CPUの場合

**構成**

【図】構成 (10.16 / 338 / 原本 p.340): パソコン ―USB― GOT ―シリアル― 接続局CPU(+経由ユニット) ― 経由ネットワーク ― 経由局CPU(+経由ユニット)

#### アクセス可否およびプロパティのパターン (10.16 / 338 / 原本 p.340)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

接続局CPU: FX5CPU ○(1)

| 経由ネットワーク | RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × |
| CC IE Control<br>CC IE Field | × | × | × | × | ○(2)*1*2 |
| MELSECNET/H | × | × | × | × | × |
| Ethernet | × | × | × | × | × |
| シリアルコミュニケーション | × | × | × | × | × |
| CC-Link | × | × | × | × | ○(3)*2 |

接続局CPU: FX5CPU ○(1)

| 経由ネットワーク | QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × | × |
| CC IE Control<br>CC IE Field | × | × | × | × | × | × |
| MELSECNET/H | × | × | × | × | × | × |
| Ethernet | × | × | × | × | × | × |
| シリアルコミュニケーション | × | × | × | × | × | × |
| CC-Link | × | × | × | × | × | × |

> *1 CC-Link IEフィールドネットワークのみアクセス可能です。
> *2 FX5SCPUにはアクセスできません。

#### プロパティ一覧 (10.16 / 339 / 原本 p.341)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) |
|---|---|---|---|---|
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActConnectUnitNumber | 0(0x00) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActCpuTimeOut | 0(0x00) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDataBits | 8(DATABIT_8) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActDestinationIONumber | 0(0x00) | 0(0x00) | 0(0x00) | 1023(0x3FF) |
| ActDestinationPortNumber | 0(0x00) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActDidPropertyBit | 1(0x01) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActDsidPropertyBit | 1(0x01) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActHostAddress | 1.1.1.1 | NULL | NULL | NULL |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00) | 0(0x00) | 1(0x01) |
| ActIONumber | 1023(0x3FF) | 1023(0x3FF) | 1023(0x3FF) | 接続局ユニット番号 |
| ActMultiDropChannelNumber | 0(0x00) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActNetworkNumber | 0(0x00) | 0(0x00) | 対象局側ユニットネットワークNo. | 0(0x00) |
| ActPacketType | 0x01(PACKET_PLC1) | PACKET_PLC1(0x01) | PACKET_PLC1(0x01) | PACKET_PLC1(0x01) |
| ActParity | 1(ODD_PARITY) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActPassword | Null | Null | Null | Null |
| ActPortNumber | 1(PORT_1) | パソコン側COMポート番号 | パソコン側COMポート番号 | パソコン側COMポート番号 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USBGOT(0x13) | PROTOCOL_USBGOT(0x13) | PROTOCOL_USBGOT(0x13) |
| ActStopBits | 0(STOPBIT_ONE) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActSumCheck | 0(NO_SUM_CHECK) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActSourceNetworkNumber | 0(0x00) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActSourceStationNumber | 0(0x00) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActStationNumber | 255(0xFF) | 255(0xFF) | 対象局側ユニット局番 | 255(0xFF) |
| ActTargetSimulator | 0(0x00) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActThroughNetworkType | 0(0x00) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00) | 0(0x00) | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_FXVCPU(0x2005) | UNIT_FXVCPU(0x2005) | UNIT_FXVCPU(0x2005) |

※原本では，隣り合うパターン列で値が同じセルは結合されている(本mdでは各列に同じ値を展開)。

### パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: 直結(2) (10.16 / 340-341 / 原本 p.342-343)

接続局がQCPU(Qモード)，QモーションCPU，またはQCCPUの場合

**構成**

【図】構成 (10.16 / 340 / 原本 p.342): パソコン ―USB― GOT ―シリアル― 接続局CPU(+経由ユニット) ― 経由ネットワーク ― 経由局CPU(+経由ユニット)

#### アクセス可否およびプロパティのパターン (10.16 / 340 / 原本 p.342)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

接続局CPU: QCPU(Qモード) ○(1)*1 / QモーションCPU ○(1)*2 / QCCPU ○(1)*5

| 経由ネットワーク | RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × |
| CC IE Control<br>CC IE Field | × | × | × | × | × |
| MELSECNET/H | × | × | × | × | × |
| Ethernet | × | × | × | × | × |
| シリアルコミュニケーション | × | × | × | × | × |
| CC-Link | × | × | × | × | × |

接続局CPU: QCPU(Qモード) ○(1)*1 / QモーションCPU ○(1)*2 / QCCPU ○(1)*5

| 経由ネットワーク | QCPU(Qモード)*1 | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × | × |
| CC IE Control<br>CC IE Field | ○(2) | ○(2)*3 | ○(2)*4 | × | ○(2)*3 | × |
| MELSECNET/H | ○(2) | ○(2) | × | × | ○(2) | × |
| Ethernet | ○(2) | × | × | × | ○(2) | × |
| シリアルコミュニケーション | ○(3) | × | ○(3) | × | ○(3) | × |
| CC-Link | ○(4) | ○(4) | ○(4) | × | ○(4) | × |

> *1 二重化CPUの場合はアクセスできません。
> *2 QモーションCPUを経由して経由局CPUにアクセスできません。
> *3 RモーションCPU，Q12DCCPU-V(基本機能モード)，QモーションCPUは，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。
> *4 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
> *5 マルチCPU構成時の，2号機以降の場合のみアクセス可能です。

#### プロパティ一覧 (10.16 / 341 / 原本 p.343)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局<br>QCPU(Qモード)，QCCPU，LCPU: 1(0x01)<br>上記以外: 0(0x00) | 対象局<br>QCPU(Qモード)，QCCPU，LCPU: 1(0x01)<br>上記以外: 0(0x00) |
| ActIONumber*1 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 接続局側ユニットI/Oアドレス | 接続局側ユニットI/Oアドレス |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニットネットワークNo. | 0(0x00)固定 | 0(0x00)固定 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USBGOT(0x13) | PROTOCOL_USBGOT(0x13) | PROTOCOL_USBGOT(0x13) | PROTOCOL_USBGOT(0x13) |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 対象局側ユニット局番 | 255(0xFF)固定 | 255(0xFF)固定 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_QNCPU(0x13) | UNIT_QNCPU(0x13) | UNIT_QNCPU(0x13) | UNIT_QNCPU(0x13) |

※原本では，隣り合うパターン列で値が同じセルは結合されている(本mdでは各列に同じ値を展開)。

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2

### パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: 直結(3) (10.16 / 342-344 / 原本 p.344-346)

接続局がLCPUの場合

**構成**

【図】構成 (10.16 / 342 / 原本 p.344): パソコン ―USB― GOT ―シリアル― 接続局CPU(+経由ユニット) ― 経由ネットワーク ― 経由局CPU(+経由ユニット)

#### アクセス可否およびプロパティのパターン (10.16 / 342 / 原本 p.344)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

接続局CPU: LCPU ○(1)

| 経由ネットワーク | RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × |
| CC IE Field*2 | × | × | × | × | × |
| MELSECNET/H | × | × | × | × | × |
| Ethernet | × | × | × | × | × |
| シリアルコミュニケーション | × | × | × | × | × |
| CC-Link | × | × | × | × | × |

接続局CPU: LCPU ○(1)

| 経由ネットワーク | QCPU(Qモード)*1 | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × | × |
| CC IE Field*2 | ○(4) | ○(4)*3 | ○(4) | × | × | × |
| MELSECNET/H | × | × | × | × | × | × |
| Ethernet | ○(4) | × | ○(4) | × | × | × |
| シリアルコミュニケーション | ○(2) | × | ○(2) | × | ○(2) | × |
| CC-Link | ○(3) | ○(3) | ○(3) | × | ○(3) | × |

> *1 二重化CPUの場合はアクセスできません。
> *2 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
> *3 Q12DCCPU-V(基本機能モード)は，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。

#### プロパティ一覧 (10.16 / 343-344 / 原本 p.345-346)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 0(0x00)固定 |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 | 1(0x01)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 | 1(0x01)固定 |
| ActHostAddress | 1.1.1.1 | NULL固定 | NULL固定 | NULL固定 | NULL固定 |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 対象局<br>QCPU(Qモード)，LCPU: 1(0x01)<br>上記以外: 0(0x00) | 対象局<br>QCPU(Qモード)，QCCPU，LCPU: 1(0x01)<br>上記以外: 0(0x00) | 0(0x00)固定 |
| ActIONumber*1 | 1023(0x3FF) | 1023(0x3FF)固定 | 接続局側ユニットI/Oアドレス | 接続局側ユニットI/Oアドレス | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 | 0(0x00)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニットネットワークNo. |
| ActParity | 1(ODD_PARITY) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActPortNumber | 1(PORT_1) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USBGOT(0x13) | PROTOCOL_USBGOT(0x13) | PROTOCOL_USBGOT(0x13) | PROTOCOL_USBGOT(0x13) |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 255(0xFF)固定 | 255(0xFF)固定 | 対象局側ユニット局番 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 | 0(0x00)固定 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_LNCPU(0x50) | UNIT_LNCPU(0x50) | UNIT_LNCPU(0x50) | UNIT_LNCPU(0x50) |

※原本では，隣り合うパターン列で値が同じセルは結合されている(本mdでは各列に同じ値を展開)。

(脚注は原本 p.346)

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2

### パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: 直結(4) (10.16 / 345-346 / 原本 p.347-348)

接続局がFXCPUの場合

**構成**

【図】構成 (10.16 / 345 / 原本 p.347): パソコン ―USB― GOT ―シリアル― 接続局CPU(+経由ユニット) ― 経由ネットワーク ― 経由局CPU(+経由ユニット)

#### アクセス可否およびプロパティのパターン (10.16 / 345 / 原本 p.347)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

接続局CPU: FXCPU ○(1)

| 経由ネットワーク | RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × |
| CC IE Control<br>CC IE Field | × | × | × | × | × |
| MELSECNET/H | × | × | × | × | × |
| Ethernet | × | × | × | × | × |
| シリアルコミュニケーション | × | × | × | × | × |
| CC-Link | × | × | × | × | × |

接続局CPU: FXCPU ○(1)

| 経由ネットワーク | QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × | × |
| CC IE Control<br>CC IE Field | × | × | × | × | × | × |
| MELSECNET/H | × | × | × | × | × | × |
| Ethernet | × | × | × | × | × | × |
| シリアルコミュニケーション | × | × | × | × | × | × |
| CC-Link | × | × | × | × | × | ○(2)*1 |

> *1 FX3G(C)CPU，FX3U(C)CPUのみアクセス可能です。

#### プロパティ一覧 (10.16 / 346 / 原本 p.348)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) |
|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDestinationIONumber | 0(0x00) | 0(0x00) | 1023(0x3FF)固定 |
| ActDidPropertyBit | 1(0x01) | 0(0x00) | 1(0x01)固定 |
| ActDsidPropertyBit | 1(0x01) | 0(0x00) | 1(0x01)固定 |
| ActIONumber | 1023(0x3FF) | 0(0x00) | 接続局ユニット番号 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USBGOT(0x13) | PROTOCOL_USBGOT(0x13) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00) | 対象局ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_FXCPU(0x0F) | UNIT_FXCPU(0x0F) |

※原本では，隣り合うパターン列で値が同じセルは結合されている(本mdでは各列に同じ値を展開)。

### パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: バス (10.16 / 347-349 / 原本 p.349-351)

**構成**

【図】構成 (10.16 / 347 / 原本 p.349): パソコン ―USB― GOT ―バス― 接続局CPU(+経由ユニット) ― 経由ネットワーク ― 経由局CPU(+経由ユニット)

#### アクセス可否およびプロパティのパターン (10.16 / 347-348 / 原本 p.349-350)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

接続局CPU: QCPU(Qモード) ○(1)*1 / QモーションCPU ○(1)*2*5

| 経由ネットワーク | RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × |
| CC IE Control<br>CC IE Field | × | × | × | × | × |
| MELSECNET/H | × | × | × | × | × |
| Ethernet | × | × | × | × | × |
| シリアルコミュニケーション | × | × | × | × | × |
| CC-Link | × | × | × | × | × |

接続局CPU: QCPU(Qモード) ○(1)*1 / QモーションCPU ○(1)*2*5

| 経由ネットワーク | QCPU(Qモード)*1 | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × | × |
| CC IE Control<br>CC IE Field | ○(2) | ○(2)*3 | ○(2)*4 | × | ○(2)*3 | × |
| MELSECNET/H | ○(2) | ○(2) | × | × | ○(2) | × |
| Ethernet | ○(2) | × | × | × | ○(2) | × |
| シリアルコミュニケーション | ○(3) | × | ○(3) | × | ○(3) | × |
| CC-Link | ○(4) | ○(4) | ○(4) | × | ○(4) | × |

接続局CPU: QCCPU ○(1)

| 経由ネットワーク | RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × |
| CC IE Control<br>CC IE Field | × | × | × | × | × |
| MELSECNET/H | × | × | × | × | × |
| Ethernet | × | × | × | × | × |
| シリアルコミュニケーション | × | × | × | × | × |
| CC-Link | × | × | × | × | × |

接続局CPU: QCCPU ○(1)

| 経由ネットワーク | QCPU(Qモード)*1 | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × | × |
| CC IE Control<br>CC IE Field | ○(2) | ○(2)*3 | ○(2)*4 | × | ○(2)*3 | × |
| MELSECNET/H | ○(2) | ○(2) | × | × | × | × |
| Ethernet | × | × | × | × | × | × |
| シリアルコミュニケーション | × | × | × | × | × | × |
| CC-Link | ○(4) | ○(4) | ○(4) | × | × | × |

※原本では接続局QCCPUの表(後半2つ)は p.347 下段〜p.348 に続いている。脚注は p.348。

> *1 二重化CPUの場合はアクセスできません。
> *2 QモーションCPUを経由して経由局CPUにアクセスできません。
> *3 Q12DCCPU-V(基本機能モード)およびQモーションCPUは，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。
> *4 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
> *5 マルチCPU構成時の，2号機以降の場合のみアクセス可能です。

#### プロパティ一覧 (10.16 / 349 / 原本 p.351)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局<br>QCPU(Qモード)，LCPU: 1(0x01)<br>上記以外: 0(0x00) | 対象局<br>QCPU(Qモード)，QCCPU，LCPU : 1(0x01)<br>上記以外: 0(0x00) |
| ActIONumber*1 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 接続局側ユニットI/Oアドレス | 接続局側ユニットI/Oアドレス |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニットネットワークNo. | 0(0x00)固定 | 0(0x00)固定 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USBGOT(0x13) | PROTOCOL_USBGOT(0x13) | PROTOCOL_USBGOT(0x13) | PROTOCOL_USBGOT(0x13) |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 対象局側ユニット局番 | 255(0xFF)固定 | 255(0xFF)固定 |
| ActTimeOut*3 | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_A900GOT(0x21) | UNIT_A900GOT(0x21) | UNIT_A900GOT(0x21) | UNIT_A900GOT(0x21) |

※原本では，隣り合うパターン列で値が同じセルは結合されている(本mdでは各列に同じ値を展開)。

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2
> *3 0～5000[ms]を指定した場合，5000msに丸められます。また，255000msより大きい値を設定した場合は，255000msに丸められますので注意してください。

### パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: シリアルコミュニケーションユニット(1) (10.16 / 350-352 / 原本 p.352-354)

接続局側MELSEC iQ-Rシリーズ対応C24のほかに経由ユニットが存在する場合

**構成**

【図】構成 (10.16 / 350 / 原本 p.352): パソコン ―USB― GOT ― MELSEC iQ-Rシリーズ対応C24(接続局CPUに装着，ほかに経由ユニットあり) ― 経由ネットワーク ― 経由局CPU(+経由ユニット)

#### アクセス可否およびプロパティのパターン (10.16 / 350 / 原本 p.352)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

接続局CPU: RCPU ○(1) / RモーションCPU ○(1)*1*3

| 経由ネットワーク | RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × |
| CC IE Control<br>CC IE Field | ○(2)*2 | ○(2) | × | × | × |
| MELSECNET/H | × | × | × | × | × |
| Ethernet | ○(2) | × | ○(2) | × | × |
| シリアルコミュニケーション | ○(3) | × | ○(3) | × | × |
| CC-Link | ○(4) | ○(4) | ○(4) | × | × |

接続局CPU: RCPU ○(1) / RモーションCPU ○(1)*1*3

| 経由ネットワーク | QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × | × |
| CC IE Control<br>CC IE Field | ○(2) | × | ○(2)*2 | × | × | × |
| MELSECNET/H | ○(2) | × | × | × | × | × |
| Ethernet | ○(2) | × | ○(2) | × | × | × |
| シリアルコミュニケーション | ○(3) | × | ○(3) | × | × | × |
| CC-Link | ○(4) | × | ○(4) | × | × | × |

> *1 RモーションCPUを経由して経由局CPUにアクセスできません。
> *2 RCPU，LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
> *3 マルチCPU構成時の，2号機以降の場合のみアクセス可能です。

#### プロパティ一覧 (10.16 / 351-352 / 原本 p.353-354)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2)*1 | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActConnectUnitNumber | 0(0x00) | 接続局側ユニット局番 | 接続局側ユニット局番 | 接続局側ユニット局番 | 接続局側ユニット局番 |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDestinationIONumber*2 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActIONumber*2 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 接続局側経由ユニットI/Oアドレス | 接続局側経由ユニットI/Oアドレス |
| ActMultiDropChannelNumber*3 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニットネットワークNo. | 0(0x00)固定 | 0(0x00)固定 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USBGOT | PROTOCOL_USBGOT | PROTOCOL_USBGOT | PROTOCOL_USBGOT |
| ActPacketType | 0x01(PACKET_PLC1) | PACKET_PLC1 | PACKET_PLC1 | PACKET_PLC1 | PACKET_PLC1 |
| ActPortNumber | 1(PORT_1) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
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
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 対象局側ユニット局番 | 255(0xFF)固定 | 255(0xFF)固定 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_RJ71C24 | UNIT_RJ71C24 | UNIT_RJ71C24 | UNIT_RJ71C24 |

※原本では，隣り合うパターン列で値が同じセルは結合されている(本mdでは各列に同じ値を展開)。

※ActProtocolType / ActPacketType / ActUnitType の値に16進表記が付かないのは原本どおり(他節では PROTOCOL_USBGOT(0x13) 等と併記)。

(脚注は原本 p.354)

> *1 Ethernetユニット(MELSEC iQ-Rシリーズ対応E71)経由のアクセスは，下記の事項に注意してください。
> - ActNetworkNumber，ActStationNumberは，対象局側のMELSEC iQ-Rシリーズ対応E71のパラメータ設定で設定した値を指定してください。
> - MELSEC iQ-Rシリーズ対応E71のパラメータ設定の「MNET/10ルーチング情報」を設定してください。また，設定を行う際，「MNET/10ルーチング方式」は自動応答方式以外(IPアドレス算出方式，テーブル変換方式，併用方式のいずれか)を指定してください。
> *2 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *3 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2

### パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: シリアルコミュニケーションユニット(2) (10.16 / 353-354 / 原本 p.355-356)

接続局側MELSEC iQ-Rシリーズ対応C24で経由ユニットとマルチドロップリンクを行う場合

**構成**

【図】構成 (10.16 / 353 / 原本 p.355): パソコン ―USB― GOT ― MELSEC iQ-Rシリーズ対応C24(接続局CPUに装着) ―マルチドロップリンク― 経由ユニット(経由局CPUに装着)

#### アクセス可否およびプロパティのパターン (10.16 / 353 / 原本 p.355)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

接続局CPU: RCPU，RモーションCPU*1*4 (独立モード*3)

| 接続局CPU | 経由ネットワーク | RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|
| 独立モード ○(1) | シリアルコミュニケーション | ○(2) | × | × | × | × |

| 接続局CPU | 経由ネットワーク | QCPU(Qモード)*2 | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|
| 独立モード ○(1) | シリアルコミュニケーション | ○(2) | × | ○(2) | × | × | × |

> *1 RモーションCPUを経由して経由局CPUにアクセスできません。
> *2 二重化CPUの場合はアクセスできません。
> *3 独立モードは，パラメータを下記のとおりに設定した場合を示します。
> - CH1側: 伝送設定の動作設定=独立(0)，交信プロトコル設定=0
> - CH2側: 伝送設定の動作設定=独立(0)
> *4 マルチCPU構成時の，2号機以降の場合のみアクセス可能です。

#### プロパティ一覧 (10.16 / 354 / 原本 p.356)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) |
|---|---|---|---|
| ActConnectUnitNumber | 0(0x00) | 接続局側ユニット局番 | 接続局側ユニット局番 |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDestinationIONumber*1 | 0(0x00) | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 0(0x00)固定 |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 |
| ActIONumber*1 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 接続局側経由ユニットI/Oアドレス |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | マルチドロップチャネルNo. |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USBGOT | PROTOCOL_USBGOT |
| ActPacketType | 0x01(PACKET_PLC1) | PACKET_PLC1 | PACKET_PLC1 |
| ActPortNumber | 1(PORT_1) | 0(0x00)固定 | 0(0x00)固定 |
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 | 0(0x00)固定 |
| ActHostAddress | 1.1.1.1 | NULL固定 | NULL固定 |
| ActCpuTimeOut | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 | 0(0x00)固定 |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 | 0(0x00)固定 |
| ActParity | 1(ODD_PARITY) | 0(0x00)固定 | 0(0x00)固定 |
| ActStopBits | 0(STOPBIT_ONE) | 0(0x00)固定 | 0(0x00)固定 |
| ActSumCheck | 0(NO_SUM_CHECK) | 0(0x00)固定 | 0(0x00)固定 |
| ActSourceNetworkNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 |
| ActSourceStationNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 |
| ActDestinationPortNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 255(0xFF)固定 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_RJ71C24 | UNIT_RJ71C24 |

※原本では，隣り合うパターン列で値が同じセルは結合されている(本mdでは各列に同じ値を展開)。

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2

### パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: シリアルコミュニケーションユニット(3) (10.16 / 355-356 / 原本 p.357-358)

接続局側Qシリーズ対応C24のほかに経由ユニットが存在する場合

**構成**

【図】構成 (10.16 / 355 / 原本 p.357): パソコン ―USB― GOT ― Qシリーズ対応C24(接続局CPUに装着，ほかに経由ユニットあり) ― 経由ネットワーク ― 経由局CPU(+経由ユニット)

#### アクセス可否およびプロパティのパターン (10.16 / 355 / 原本 p.357)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

接続局CPU: QCPU(Qモード) ○(1)*1 / QモーションCPU ○(1)*2*5

| 経由ネットワーク | RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × |
| CC IE Control<br>CC IE Field | × | × | × | × | × |
| MELSECNET/H | × | × | × | × | × |
| Ethernet | × | × | × | × | × |
| シリアルコミュニケーション | × | × | × | × | × |
| CC-Link | × | × | × | × | × |

接続局CPU: QCPU(Qモード) ○(1)*1 / QモーションCPU ○(1)*2*5

| 経由ネットワーク | QCPU(Qモード)*1 | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × | × |
| CC IE Control<br>CC IE Field | ○(2) | ○(2)*3 | ○(2)*4 | × | ○(2)*3 | × |
| MELSECNET/H | ○(2) | ○(2) | × | × | ○(2) | × |
| Ethernet | ○(2) | × | × | × | ○(2) | × |
| シリアルコミュニケーション | ○(3) | × | ○(3) | × | ○(3) | × |
| CC-Link | ○(4) | ○(4) | ○(4) | × | ○(4) | × |

> *1 二重化CPUの場合はアクセスできません。
> *2 QモーションCPUを経由して経由局CPUにアクセスできません。
> *3 RモーションCPU，Q12DCCPU-V(基本機能モード)，QモーションCPUは，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。
> *4 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
> *5 マルチCPU構成時の，2号機以降の場合のみアクセス可能です。

#### プロパティ一覧 (10.16 / 356 / 原本 p.358)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActConnectUnitNumber | 0(0x00) | 接続局側ユニット局番 | 接続局側ユニット局番 | 接続局側ユニット局番 | 接続局側ユニット局番 |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActIONumber*1 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 接続局側経由ユニットI/Oアドレス | 接続局側経由ユニットI/Oアドレス |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニットネットワークNo. | 0(0x00)固定 | 0(0x00)固定 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USBGOT(0x13) | PROTOCOL_USBGOT(0x13) | PROTOCOL_USBGOT(0x13) | PROTOCOL_USBGOT(0x13) |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 対象局側ユニット局番 | 255(0xFF)固定 | 255(0xFF)固定 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_QJ71C24(0x19) | UNIT_QJ71C24(0x19) | UNIT_QJ71C24(0x19) | UNIT_QJ71C24(0x19) |

※原本では，隣り合うパターン列で値が同じセルは結合されている(本mdでは各列に同じ値を展開)。

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2

### パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: シリアルコミュニケーションユニット(4) (10.16 / 357-358 / 原本 p.359-360)

接続局側Qシリーズ対応C24で経由ユニットとマルチドロップリンクを行う場合

**構成**

【図】構成 (10.16 / 357 / 原本 p.359): パソコン ―USB― GOT ― Qシリーズ対応C24(接続局CPUに装着) ―マルチドロップリンク― 経由ユニット(経由局CPUに装着)

#### アクセス可否およびプロパティのパターン (10.16 / 357 / 原本 p.359)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

接続局CPU: QCPU(Qモード)*1 (独立モード*2)

| 接続局CPU | 経由ネットワーク | RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|
| 独立モード ○(1) | シリアルコミュニケーション | × | × | × | × | × |

| 接続局CPU | 経由ネットワーク | QCPU(Qモード)*1 | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|
| 独立モード ○(1) | シリアルコミュニケーション | ○(2) | × | ○(2) | × | × | × |

> *1 二重化CPUの場合はアクセスできません。
> *2 独立モードは，パラメータを下記のとおりに設定した場合を示します。
> - CH1側: 伝送設定の動作設定=独立(0)，交信プロトコル設定=0
> - CH2側: 伝送設定の動作設定=独立(0)

#### プロパティ一覧 (10.16 / 358 / 原本 p.360)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) |
|---|---|---|---|
| ActConnectUnitNumber | 0(0x00) | 接続局側ユニット局番 | 接続局側ユニット局番 |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 0(0x00)固定 |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 |
| ActIONumber*1 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 接続局側経由ユニットI/Oアドレス |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | マルチドロップチャネルNo. |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USBGOT(0x13) | PROTOCOL_USBGOT(0x13) |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 255(0xFF)固定 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_QJ71C24(0x19) | UNIT_QJ71C24(0x19) |

※原本では，隣り合うパターン列で値が同じセルは結合されている(本mdでは各列に同じ値を展開)。

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2

### パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: シリアルコミュニケーションユニット(5) (10.16 / 359-360 / 原本 p.361-362)

接続局側Lシリーズ対応C24のほかに経由ユニットが存在する場合

**構成**

【図】構成 (10.16 / 359 / 原本 p.361): パソコン ―USB― GOT ― Lシリーズ対応C24(接続局CPUに装着，ほかに経由ユニットあり) ― 経由ネットワーク ― 経由局CPU(+経由ユニット)

#### アクセス可否およびプロパティのパターン (10.16 / 359 / 原本 p.361)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

接続局CPU: LCPU ○(1)

| 経由ネットワーク | RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × |
| CC IE Field*2 | × | × | × | × | × |
| MELSECNET/H | × | × | × | × | × |
| Ethernet | × | × | × | × | × |
| シリアルコミュニケーション | × | × | × | × | × |
| CC-Link | × | × | × | × | × |

接続局CPU: LCPU ○(1)

| 経由ネットワーク | QCPU(Qモード)*1 | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|
| CC IE TSN | × | × | × | × | × | × |
| CC IE Field*2 | ○(4) | ○(4)*3 | ○(4) | × | × | × |
| MELSECNET/H | × | × | × | × | × | × |
| Ethernet | ○(4) | × | ○(4) | × | × | × |
| シリアルコミュニケーション | ○(2) | × | ○(2) | × | ○(2) | × |
| CC-Link | ○(3) | ○(3) | ○(3) | × | ○(3) | × |

> *1 二重化CPUの場合はアクセスできません。
> *2 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
> *3 Q12DCCPU-V(基本機能モード)は，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。

#### プロパティ一覧 (10.16 / 360 / 原本 p.362)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActConnectUnitNumber | 0(0x00) | 接続局側ユニット局番 | 接続局側ユニット局番 | 接続局側ユニット局番 | 接続局側ユニット局番 |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 0(0x00)固定 |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 | 1(0x01)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 | 1(0x01)固定 |
| ActHostAddress | 1.1.1.1 | NULL固定 | NULL固定 | NULL固定 | NULL固定 |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActIONumber*1 | 1023(0x3FF) | 1023(0x3FF)固定 | 接続局側経由ユニットI/Oアドレス | 接続局側経由ユニットI/Oアドレス | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 | 0(0x00)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニットネットワークNo. |
| ActParity | 1(ODD_PARITY) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActPortNumber | 1(PORT_1) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USBGOT(0x13) | PROTOCOL_USBGOT(0x13) | PROTOCOL_USBGOT(0x13) | PROTOCOL_USBGOT(0x13) |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 255(0xFF)固定 | 255(0xFF)固定 | 対象局側ユニット局番 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 | 0(0x00)固定 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_LJ71C24(0x54) | UNIT_LJ71C24(0x54) | UNIT_LJ71C24(0x54) | UNIT_LJ71C24(0x54) |

※原本では，隣り合うパターン列で値が同じセルは結合されている(本mdでは各列に同じ値を展開)。

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2

### パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: シリアルコミュニケーションユニット(6) (10.16 / 361-362 / 原本 p.363-364)

接続局側Lシリーズ対応C24で経由ユニットとマルチドロップリンクを行う場合

**構成**

【図】構成 (10.16 / 361 / 原本 p.363): パソコン ―USB― GOT ― Lシリーズ対応C24(接続局CPUに装着) ―マルチドロップリンク― 経由ユニット(経由局CPUに装着)

#### アクセス可否およびプロパティのパターン (10.16 / 361 / 原本 p.363)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

接続局CPU: LCPU (独立モード*2)

| 接続局CPU | 経由ネットワーク | RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|
| 独立モード ○(1) | シリアルコミュニケーション | × | × | × | × | × |

| 接続局CPU | 経由ネットワーク | QCPU(Qモード)*1 | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|
| 独立モード ○(1) | シリアルコミュニケーション | ○(2) | × | ○(2) | × | × | × |

> *1 二重化CPUの場合はアクセスできません。
> *2 独立モードは，パラメータを下記のとおりに設定した場合を示します。
> - CH1側: 伝送設定の動作設定=独立(0)，交信プロトコル設定=0
> - CH2側: 伝送設定の動作設定=独立(0)

#### プロパティ一覧 (10.16 / 362 / 原本 p.364)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) |
|---|---|---|---|
| ActConnectUnitNumber | 0(0x00) | 接続局側ユニット局番 | 接続局側ユニット局番 |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 0(0x00)固定 |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 |
| ActIONumber*1 | 1023(0x3FF) | 1023(0x3FF)固定 | 接続局側経由ユニットI/Oアドレス |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | マルチドロップチャネルNo. |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USBGOT(0x13) | PROTOCOL_USBGOT(0x13) |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 255(0xFF)固定 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_LJ71C24(0x54) | UNIT_LJ71C24(0x54) |

※原本では，隣り合うパターン列で値が同じセルは結合されている(本mdでは各列に同じ値を展開)。

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2
