# MX Component Version 5 リファレンスマニュアル 10章 各通信経路で設定するプロパティ (8/9) p.365-396

| 項目 | 内容 |
|---|---|
| 原本 | 【三菱】MX Component Version 5 リファレンスマニュアル (SH-082394J) |
| メーカー | 三菱電機 |
| 原本ファイル | `PDF/【三菱】MX Component Version 5 リファレンスマニュアル_sh082394j.pdf` (全696ページ) |
| 本ファイルの範囲 | 10.16 GOTトランスペアレント通信のうち「パソコン側ポート: シリアル，GOT2000側ポート: シリアル，CPU側ポート: MELSEC iQ-Rシリーズ対応E71」〜「パソコン側ポート: USB，GOT2000/3000側ポート: USB，CPU側ポート: Ethernetユニット」 (印刷ページ 363-394 / PDF p.365-396) |
| 出典表記 | `(節 / 印刷ページ / 原本 p.PDFページ)` |
| 作成日 | 2026-11-03 |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。
> 本文中の「○ページ」はすべて原本の**印刷ページ番号**です(PDFページ = 印刷ページ + 2)。
> プロパティ一覧の「(同左)」は，原本で○(1)〜○(n)の複数列が1つのセルを共有している箇所を，列ごとに展開して表記したものです(値は左の列と同じ)。
> 「シングルCPU時／マルチCPU時(／二重化CPU時)」の号機別I/O番号は，原本の各セルの記載どおりに展開しています。

## 主要用語 対訳表 (Glossary)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| GOTトランスペアレント通信 | GOT transparent communication | PROTOCOL_USBGOT / PROTOCOL_SERIAL | 参考訳 |
| パソコン側ポート / GOT側ポート / CPU側ポート | PC side port / GOT side port / CPU side port | — | 参考訳 |
| 接続局CPU | Connected station CPU | — | 参考訳 |
| 経由ネットワーク | Relay network | CC IE TSN / CC IE Control / CC IE Field / MELSECNET/H / Ethernet / シリアルコミュニケーション / CC-Link | 参考訳 |
| 経由局CPU | Relay station CPU | — | 参考訳 |
| 経由ユニット | Relay module | — | 参考訳 |
| 対象局 | Target station | — | 参考訳 |
| アクセス可否 | Accessibility | ○(n) / × | 参考訳 |
| プロパティのパターン | Property pattern | (1)〜(4) | 参考訳 |
| デフォルト値 | Default value | — | 参考訳 |
| シングルCPU / マルチCPU / 二重化CPU | Single CPU / Multiple CPU / Redundant CPU | — | 参考訳 |
| 接続号機 / 1号機〜4号機 | Connected CPU / CPU No.1–No.4 | 1023(0x3FF) / 992(0x3E0)〜995(0x3E3) | 参考訳 |
| 制御系 | Control system | 976(0x3D0) | 参考訳 |
| I/Oアドレス(I/O先頭No.を16で割った値) | I/O address (start I/O number divided by 16) | ActIONumber / ActDestinationIONumber | 参考訳 |
| マルチドロップチャネルNo. | Multidrop channel number | ActMultiDropChannelNumber | 参考訳 |
| GOT側ネットワークNo. / GOT側局番 | GOT side network number / GOT side station number | ActSourceNetworkNumber / ActSourceStationNumber | 参考訳 |
| MELSECNET/10を含む / 含まない | Includes / Does not include MELSECNET/10 | ActThroughNetworkType 1 / 0 | 参考訳 |
| OPS接続 / 自局ポート番号 | OPS connection / Own station port number | ActDestinationPortNumber | 参考訳 |
| リモートパスワード | Remote password | — | 参考訳 |
| MNET/10ルーチング情報 / MNET/10ルーチング方式 | MNET/10 routing information / MNET/10 routing method | — | 参考訳 |
| 局番↔IP関連情報設定方式 | Station No.↔IP information setting method | — | 参考訳 |
| 自動応答方式 / IPアドレス算出方式 / テーブル変換方式 / 併用方式 | Automatic response / IP address calculation / Table conversion / Combined method | — | 参考訳 |
| Ethernetアダプタユニット | Ethernet adapter module | NZ2GF-ETB / UNIT_GOT_NZ2GF_ETB | 参考訳 |
| Ethernetアダプタ / Ethernetユニット(FX) | Ethernet adapter / Ethernet module (FX) | FX3U-ENET-ADP / FX3U-ENET-L | 参考訳 |
| ユニットタイプ | Unit type | UNIT_GOT_RJ71EN71 / UNIT_GOT_QJ71E71 / UNIT_GOT_LJ71E71 / UNIT_GOT_RETHER / UNIT_GOT_FXVETHER / UNIT_GOT_QNETHER / UNIT_GOT_LNETHER / UNIT_GOT_FXETHER / UNIT_GOT_FXENET / UNIT_GOT_FXVENET | 原本併記 |
| インテリジェント優先ビット | Intelligent preference bit | ActIntelligentPreferenceBit | 参考訳 |

## 変換範囲表

| 原本ページ(PDF) | 印刷ページ | 節 | 扱い |
|---|---|---|---|
| p.365-367 | 363-365 | パソコン: シリアル，GOT2000: シリアル，CPU: MELSEC iQ-Rシリーズ対応E71 | 全文(構成図は文章化) |
| p.368-370 | 366-368 | パソコン: USB，GOT2000/3000: USB，CPU: MELSEC iQ-Rシリーズ対応E71 | 全文 |
| p.371-373 | 369-371 | 〃 CPU: Qシリーズ対応E71 | 全文 |
| p.374-376 | 372-374 | 〃 CPU: Lシリーズ対応E71 | 全文 |
| p.377-379 | 375-377 | 〃 CPU: Ethernetポート(1) 接続局RCPU | 全文 |
| p.380-381 | 378-379 | 〃 CPU: Ethernetポート(2) 接続局FX5CPU | 全文 |
| p.382-385 | 380-383 | 〃 CPU: Ethernetポート(3) 接続局QCPU/QCCPU | 全文 |
| p.386-388 | 384-386 | 〃 CPU: Ethernetポート(4) 接続局LCPU | 全文 |
| p.389-392 | 387-390 | パソコン: USB，GOT2000: USB，CPU: Ethernetアダプタユニット | 全文 |
| p.393-394 | 391-392 | 〃 CPU: Ethernetアダプタ/Ethernetユニット 接続局FXCPU | 全文 |
| p.395-396 | 393-394 | 〃 CPU: Ethernetユニット 接続先FX5CPU | 全文 |
| p.192-364 | 190-362 | 10.1〜10.15，10.16の先頭(USB直結〜シリアルコミュニケーションユニット) | 別ファイル(10-1〜10-7) |
| p.397-417 | 395-415 | 10.16 残り(パソコン: Ethernetボード〜) | 別ファイル(10-9) |
| p.1-191，p.418-696 | — | 10章以外 | 別ファイル(01_〜09_ ほか)または**未変換** |

## 目次

- パソコン: シリアル / GOT2000: シリアル / CPU: MELSEC iQ-Rシリーズ対応E71 (p.365)
- パソコン: USB / GOT2000/3000: USB / CPU: MELSEC iQ-Rシリーズ対応E71 (p.368)
- 〃 CPU: Qシリーズ対応E71 (p.371)
- 〃 CPU: Lシリーズ対応E71 (p.374)
- 〃 CPU: Ethernetポート(1) 接続局RCPU (p.377)
- 〃 CPU: Ethernetポート(2) 接続局FX5CPU (p.380)
- 〃 CPU: Ethernetポート(3) 接続局QCPU/QCCPU (p.382)
- 〃 CPU: Ethernetポート(4) 接続局LCPU (p.386)
- パソコン: USB / GOT2000: USB / CPU: Ethernetアダプタユニット (p.389)
- 〃 CPU: Ethernetアダプタ/Ethernetユニット 接続局FXCPU (p.393)
- 〃 CPU: Ethernetユニット 接続先FX5CPU (p.395)

---

## パソコン側ポート: シリアル，GOT2000側ポート: シリアル，CPU側ポート: MELSEC iQ-Rシリーズ対応E71 (10.16 / 363-365 / 原本 p.365-367)

### 構成 (10.16 / 363 / 原本 p.365)

【図】構成 (原本 p.365)
- パソコン ―シリアル― GOT ―Ethernet― MELSEC iQ-Rシリーズ対応E71(接続局CPU側)
- 接続局CPU ＋ MELSEC iQ-Rシリーズ対応E71 ＋ 経由ユニット ―経由ネットワーク― 経由局CPU ＋ 経由ユニット

### アクセス可否およびプロパティのパターン (10.16 / 363 / 原本 p.365)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: RCPU | 経由ネットワーク | 経由局CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × |
| ○(1)*1 | CC IE Control<br>CC IE Field | × | × | × | × | × |
| ○(1)*1 | MELSECNET/H | × | × | × | × | × |
| ○(1)*1 | Ethernet | ○(2) | × | × | × | × |
| ○(1)*1 | シリアルコミュニケーション | ○(3) | × | × | × | × |
| ○(1)*1 | CC-Link | ○(4) | ○(4) | × | × | × |

| 接続局CPU: RCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × | × |
| ○(1)*1 | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
| ○(1)*1 | MELSECNET/H | × | × | × | × | × | × |
| ○(1)*1 | Ethernet | ○(2) | × | ○(2) | × | × | × |
| ○(1)*1 | シリアルコミュニケーション | ○(3) | × | ○(3) | × | × | × |
| ○(1)*1 | CC-Link | ○(4) | × | ○(4) | × | × | × |

※接続局CPU列の「○(1)*1」は原本では全行で共有セル。

> *1 マルチCPU構成時の，2号機以降の場合のみアクセス可能です。

### プロパティ一覧 (10.16 / 364-365 / 原本 p.366-367)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActBaudRate | 19200(BAUDRATE_19200) | BAUDRATE_9600，BAUDRATE_19200，BAUDRATE_38400，BAUDRATE_57600，BAUDRATE_115200 | (同左) | (同左) | (同左) |
| ActConnectUnitNumber*1 | 0(0x00) | 0(0x00)固定 | 接続局側ユニット局番 | 0(0x00)固定 | 0(0x00)固定 |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | (同左) | (同左) | (同左) |
| ActDestinationIONumber*2 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) |
| ActDestinationPortNumber | 0(0x00) | 5001<br>OPS接続時　自局ポートNo.*3 | (同左) | (同左) | (同左) |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActHostAddress | 1.1.1.1 | 接続局側ユニットのホスト名またはIPアドレス | (同左) | (同左) | (同左) |
| ActIONumber*2 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 接続局側ユニットI/Oアドレス | 接続局側ユニットI/Oアドレス |
| ActMultiDropChannelNumber*4 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber*5 | 0(0x00) | 対象局側ユニットネットワークNo. | 対象局側ユニットネットワークNo. | 接続局側MELSEC iQ-Rシリーズ対応E71ネットワークNo. | 接続局側MELSEC iQ-Rシリーズ対応E71ネットワークNo. |
| ActPortNumber | 1(PORT_1) | パソコン側COMポート番号 | (同左) | (同左) | (同左) |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_SERIAL | (同左) | (同左) | (同左) |
| ActPacketType | 0x01(PACKET_PLC1) | PACKET_PLC1 | (同左) | (同左) | (同左) |
| ActCpuTimeOut | 0(0x00) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActControl | 8(TRC_DTR_OR_RTS) | 使用ケーブルによる | (同左) | (同左) | (同左) |
| ActDataBits | 8(DATABIT_8) | 8(0x08)固定 | (同左) | (同左) | (同左) |
| ActParity | 1(ODD_PARITY) | 1(0x01)固定 | (同左) | (同左) | (同左) |
| ActStopBits | 0(STOPBIT_ONE) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActSumCheck | 0(NO_SUM_CHECK) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActSourceNetworkNumber*6 | 0(0x00) | GOT側ネットワークNo. | (同左) | (同左) | (同左) |
| ActSourceStationNumber*7 | 0(0x00) | GOT側局番 | (同左) | (同左) | (同左) |
| ActStationNumber*5 | 255(0xFF) | 対象局側ユニット局番 | 対象局側ユニット局番 | 接続局側MELSEC iQ-Rシリーズ対応E71局番 | 接続局側MELSEC iQ-Rシリーズ対応E71局番 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む : 1(0x01) | (同左) | (同左) | (同左) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | (同左) | (同左) | (同左) |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_GOT_RJ71EN71 | (同左) | (同左) | (同左) |

※「(同左)」は原本で○(1)〜○(4)の4列が1つのセルを共有している箇所(表記上の展開)。

> *1 プロパティのパターンが(2)の場合，接続局側MELSEC iQ-Rシリーズ対応E71のEthernetパラメータで設定した接続局側MELSEC iQ-Rシリーズ対応E71の局番を指定してください。
> *2 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *3 二重化CPU接続時にOPS接続の機能を使用する場合は，ネットワークパラメータの「自局ポート番号」で設定したポートNo.を指定してください。
> *4 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2
> *5 プロパティのパターンが(1)または(2)の場合，ActNetworkNumberおよびActStationNumberは対象局側のパラメータで設定した値を指定してください。
> *6 対象局側MELSEC iQ-Rシリーズ対応E71のEthernetパラメータ設定で，MELSEC iQ-Rシリーズ対応E71に設定したMELSECNET/10用ネットワークNo.と同一のネットワークNo.を指定してください。
> *7 Ethernetの同一ループ内でのMELSEC iQ-Rシリーズ対応E71に設定した局番と重複しないように，GOT側の局番を指定してください。

---

## パソコン側ポート: USB，GOT2000/3000側ポート: USB，CPU側ポート: MELSEC iQ-Rシリーズ対応E71 (10.16 / 366-368 / 原本 p.368-370)

### 構成 (10.16 / 366 / 原本 p.368)

【図】構成 (原本 p.368)
- パソコン ―USB― GOT ―Ethernet― MELSEC iQ-Rシリーズ対応E71(接続局CPU側)
- 接続局CPU ＋ MELSEC iQ-Rシリーズ対応E71 ＋ 経由ユニット ―経由ネットワーク― 経由局CPU ＋ 経由ユニット

### アクセス可否およびプロパティのパターン (10.16 / 366 / 原本 p.368)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: RCPU | 接続局CPU: RCCPU | 経由ネットワーク | 経由局CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|---|
| ○(1)*1 | ○(1)*1*2 | CC IE TSN | × | × | × | × | × |
| ○(1)*1 | ○(1)*1*2 | CC IE Control<br>CC IE Field | × | × | × | × | × |
| ○(1)*1 | ○(1)*1*2 | MELSECNET/H | × | × | × | × | × |
| ○(1)*1 | ○(1)*1*2 | Ethernet | ○(2) | × | × | × | × |
| ○(1)*1 | ○(1)*1*2 | シリアルコミュニケーション | ○(3) | × | × | × | × |
| ○(1)*1 | ○(1)*1*2 | CC-Link | ○(4) | ○(4) | × | × | × |

| 接続局CPU: RCPU | 接続局CPU: RCCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|---|
| ○(1)*1 | ○(1)*1*2 | CC IE TSN | × | × | × | × | × | × |
| ○(1)*1 | ○(1)*1*2 | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
| ○(1)*1 | ○(1)*1*2 | MELSECNET/H | × | × | × | × | × | × |
| ○(1)*1 | ○(1)*1*2 | Ethernet | ○(2) | × | ○(2) | × | × | × |
| ○(1)*1 | ○(1)*1*2 | シリアルコミュニケーション | ○(3) | × | ○(3) | × | × | × |
| ○(1)*1 | ○(1)*1*2 | CC-Link | ○(4) | × | ○(4) | × | × | × |

※接続局CPU列は原本では全行で共有セル。

> *1 マルチCPU構成時の，2号機以降の場合のみアクセス可能です。
> *2 ネットワークを経由した経由局とは通信出来ません。

### プロパティ一覧 (10.16 / 367-368 / 原本 p.369-370)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActConnectUnitNumber*1 | 0(0x00) | 0(0x00)固定 | 接続局側ユニット局番 | 0(0x00)固定 | 0(0x00)固定 |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | (同左) | (同左) | (同左) |
| ActDestinationIONumber*2 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) |
| ActDestinationPortNumber | 0(0x00) | 5001<br>OPS接続時　自局ポートNo.*3 | (同左) | (同左) | (同左) |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActHostAddress | 1.1.1.1 | 接続局側ユニットのホスト名またはIPアドレス | (同左) | (同左) | (同左) |
| ActIONumber*2 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 接続局側ユニットI/Oアドレス | 接続局側ユニットI/Oアドレス |
| ActMultiDropChannelNumber*4 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber*5 | 0(0x00) | 対象局側ユニットネットワークNo. | 対象局側ユニットネットワークNo. | 接続局側MELSEC iQ-Rシリーズ対応E71ネットワークNo. | 接続局側MELSEC iQ-Rシリーズ対応E71ネットワークNo. |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USBGOT | (同左) | (同左) | (同左) |
| ActPacketType | 0x01(PACKET_PLC1) | PACKET_PLC1 | (同左) | (同左) | (同左) |
| ActPortNumber | 1(PORT_1) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActCpuTimeOut | 0(0x00) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActParity | 1(ODD_PARITY) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActStopBits | 0(STOPBIT_ONE) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActSumCheck | 0(NO_SUM_CHECK) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActSourceNetworkNumber*6 | 0(0x00) | GOT側ネットワークNo. | (同左) | (同左) | (同左) |
| ActSourceStationNumber*7 | 0(0x00) | GOT側局番 | (同左) | (同左) | (同左) |
| ActStationNumber*5 | 255(0xFF) | 対象局側ユニット局番 | 対象局側ユニット局番 | 接続局側MELSEC iQ-Rシリーズ対応E71局番 | 接続局側MELSEC iQ-Rシリーズ対応E71局番 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | (同左) | (同左) | (同左) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | (同左) | (同左) | (同左) |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_GOT_RJ71EN71 | (同左) | (同左) | (同左) |

※「(同左)」は原本で4列共有セル。

> *1 プロパティのパターンが(2)の場合，接続局側MELSEC iQ-Rシリーズ対応E71のEthernetパラメータで設定した接続局側MELSEC iQ-Rシリーズ対応E71の局番を指定してください。
> *2 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *3 二重化CPU接続時にOPS接続の機能を使用する場合は，ネットワークパラメータの「自局ポート番号」で設定したポートNo.を指定してください。
> *4 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2
> *5 プロパティのパターンが(1)または(2)の場合，ActNetworkNumberおよびActStationNumberは対象局側のパラメータで設定した値を指定してください。
> *6 対象局側MELSEC iQ-Rシリーズ対応E71のEthernetパラメータ設定で，MELSEC iQ-Rシリーズ対応E71に設定したMELSECNET/10用ネットワークNo.と同一のネットワークNo.を指定してください。
> *7 Ethernetの同一ループ内でのMELSEC iQ-Rシリーズ対応E71に設定した局番と重複しないように，GOT側の局番を指定してください。

---

## パソコン側ポート: USB，GOT2000/3000側ポート: USB，CPU側ポート: Qシリーズ対応E71 (10.16 / 369-371 / 原本 p.371-373)

### 構成 (10.16 / 369 / 原本 p.371)

【図】構成 (原本 p.371)
- パソコン ―USB― GOT ―Ethernet― Qシリーズ対応E71(接続局CPU側)
- 接続局CPU ＋ Qシリーズ対応E71 ＋ 経由ユニット ―経由ネットワーク― 経由局CPU ＋ 経由ユニット

接続局のQシリーズ対応E71にリモートパスワードが設定されている場合は通信できません。

### アクセス可否およびプロパティのパターン (10.16 / 369 / 原本 p.371)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: QCPU(Qモード) | 接続局CPU: QCCPU | 経由ネットワーク | 経由局CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|---|
| ○(1)*1 | ○(1)*4 | CC IE TSN | × | × | × | × | × |
| ○(1)*1 | ○(1)*4 | CC IE Control<br>CC IE Field | × | × | × | × | × |
| ○(1)*1 | ○(1)*4 | MELSECNET/H | × | × | × | × | × |
| ○(1)*1 | ○(1)*4 | Ethernet | × | × | × | × | × |
| ○(1)*1 | ○(1)*4 | シリアルコミュニケーション | × | × | × | × | × |
| ○(1)*1 | ○(1)*4 | CC-Link | × | × | × | × | × |

| 接続局CPU: QCPU(Qモード) | 接続局CPU: QCCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード)*1 | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|---|
| ○(1)*1 | ○(1)*4 | CC IE TSN | × | × | × | × | × | × |
| ○(1)*1 | ○(1)*4 | CC IE Control<br>CC IE Field | ○(2) | ○(2)*2 | ○(2)*3 | × | × | × |
| ○(1)*1 | ○(1)*4 | MELSECNET/H | ○(2) | ○(2) | × | × | × | × |
| ○(1)*1 | ○(1)*4 | Ethernet | ○(2) | × | × | × | × | × |
| ○(1)*1 | ○(1)*4 | シリアルコミュニケーション | ○(3) | × | ○(3) | × | × | × |
| ○(1)*1 | ○(1)*4 | CC-Link | ○(4) | ○(4) | ○(4) | × | × | × |

※接続局CPU列は原本では全行で共有セル。

> *1 二重化CPUの場合はアクセスできません。
> *2 Q12DCCPU-V(基本機能モード)は，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。
> *3 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
> *4 マルチCPU構成時の，2号機以降の場合のみアクセス可能です。

### プロパティ一覧 (10.16 / 370-371 / 原本 p.372-373)

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
| ActIONumber*1 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 接続局側ユニットI/Oアドレス | 接続局側ユニットI/Oアドレス |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber*3 | 0(0x00) | 対象局側ユニットネットワークNo. | 対象局側ユニットネットワークNo. | 接続局側Qシリーズ対応E71ネットワークNo. | 接続局側Qシリーズ対応E71ネットワークNo. |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USBGOT(0x13) | (同左) | (同左) | (同左) |
| ActSourceNetworkNumber | 0(0x00) | GOT側ネットワークNo. | (同左) | (同左) | (同左) |
| ActSourceStationNumber*4 | 0(0x00) | GOT側局番 | (同左) | (同左) | (同左) |
| ActStationNumber*3 | 255(0xFF) | 対象局側ユニット局番 | 対象局側ユニット局番 | 接続局側Qシリーズ対応E71局番 | 接続局側Qシリーズ対応E71局番 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | (同左) | (同左) | (同左) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | (同左) | (同左) | (同左) |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_GOT_QJ71E71(0x40) | (同左) | (同左) | (同左) |

※「(同左)」は原本で4列共有セル。本節の表には ActPacketType / ActPortNumber / ActBaudRate / ActCpuTimeOut / ActControl / ActDataBits / ActParity / ActStopBits / ActSumCheck / ActIntelligentPreferenceBit の行は無い(原本どおり)。

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2
> *3 プロパティのパターンが(1)または(2)の場合，ActNetworkNumberおよびActStationNumberは対象局側のパラメータで設定した値を指定してください。
> *4 Ethernetの同一ループ内でのQシリーズ対応E71に設定した局番と重複しないように，GOT側の局番を指定してください。

---

## パソコン側ポート: USB，GOT2000/3000側ポート: USB，CPU側ポート: Lシリーズ対応E71 (10.16 / 372-374 / 原本 p.374-376)

### 構成 (10.16 / 372 / 原本 p.374)

【図】構成 (原本 p.374)
- パソコン ―USB― GOT ―Ethernet― Lシリーズ対応E71(接続局CPU側)
- 接続局CPU ＋ Lシリーズ対応E71 ＋ 経由ユニット ―経由ネットワーク― 経由局CPU ＋ 経由ユニット

接続局のLシリーズ対応E71にリモートパスワードが設定されている場合は通信できません。

### アクセス可否およびプロパティのパターン (10.16 / 372 / 原本 p.374)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: LCPU | 経由ネットワーク | 経由局CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × |
| ○(1)*1 | CC IE Control<br>CC IE Field | × | × | × | × | × |
| ○(1)*1 | MELSECNET/H | × | × | × | × | × |
| ○(1)*1 | Ethernet | × | × | × | × | × |
| ○(1)*1 | シリアルコミュニケーション | × | × | × | × | × |
| ○(1)*1 | CC-Link | × | × | × | × | × |

| 接続局CPU: LCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード)*1 | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × | × |
| ○(1)*1 | CC IE Control<br>CC IE Field | ○(2) | ○(2)*2 | ○(2)*3 | × | × | × |
| ○(1)*1 | MELSECNET/H | ○(2) | ○(2) | × | × | × | × |
| ○(1)*1 | Ethernet | ○(2) | ○(2) | ○(2) | × | × | × |
| ○(1)*1 | シリアルコミュニケーション | ○(3)*4 | ○(3)*4 | ○(3)*4 | × | × | × |
| ○(1)*1 | CC-Link | ○(4) | ○(4) | ○(4) | × | × | × |

※接続局CPU列は原本では全行で共有セル。

> *1 二重化CPUの場合はアクセスできません。
> *2 Q12DCCPU-V(基本機能モード)は，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。
> *3 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
> *4 二重化CPUの場合，マルチドロップ接続ができないため，基本ベースユニット上にあるシリアルコミュニケーションユニットにはアクセスできません。

### プロパティ一覧 (10.16 / 373-374 / 原本 p.375-376)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActConnectUnitNumber*1 | 0(0x00) | 0(0x00)固定 | 接続局側ユニット局番 | 0(0x00)固定 | 0(0x00)固定 |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | (同左) | (同左) | (同左) |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) |
| ActDestinationPortNumber*2 | 0(0x00) | 5001<br>OPS接続時　自局ポートNo. | (同左) | (同左) | (同左) |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActHostAddress | 1.1.1.1 | 接続局側ユニットのホスト名またはIPアドレス | (同左) | (同左) | (同左) |
| ActIONumber*3 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 接続局側ユニットI/Oアドレス | 接続局側ユニットI/Oアドレス |
| ActMultiDropChannelNumber*4 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber*5 | 0(0x00) | 対象局側ユニットネットワークNo. | 対象局側ユニットネットワークNo. | 接続局側Lシリーズ対応E71ネットワークNo. | 接続局側Lシリーズ対応E71ネットワークNo. |
| ActParity | 1(ODD_PARITY) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActPortNumber | 1(PORT_1) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USBGOT(0x13) | (同左) | (同左) | (同左) |
| ActSourceNetworkNumber*6 | 0(0x00) | GOT側ネットワークNo. | (同左) | (同左) | (同左) |
| ActSourceStationNumber*7 | 0(0x00) | GOT側局番 | (同左) | (同左) | (同左) |
| ActStationNumber*5 | 255(0xFF) | 対象局側ユニット局番 | 対象局側ユニット局番 | 接続局側Lシリーズ対応E71局番 | 接続局側Lシリーズ対応E71局番 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | (同左) | (同左) | (同左) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | (同左) | (同左) | (同左) |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_GOT_LJ71E71(0x5D) | (同左) | (同左) | (同左) |

※「(同左)」は原本で4列共有セル。

> *1 プロパティのパターンが(2)の場合，接続局側Lシリーズ対応E71のEthernet パラメータで設定した接続局側Lシリーズ対応E71の局番を指定してください。
> *2 二重化CPU接続時にOPS接続の機能を使用する場合は，ネットワークパラメータの「自局ポート番号」で設定したポートNo.を指定してください。
> *3 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *4 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2
> *5 プロパティのパターンが(1)または(2)の場合，ActNetworkNumberおよびActStationNumberは対象局側のパラメータで設定した値を指定してください。
> *6 対象局側Lシリーズ対応E71のEthernetパラメータ設定で，Lシリーズ対応E71に設定したMELSECNET/10用ネットワークNo.と同一のネットワークNo.を指定してください。
> *7 Ethernetの同一ループ内でのLシリーズ対応E71に設定した局番と重複しないように，GOT側の局番を指定してください。

---

## パソコン側ポート: USB，GOT2000/3000側ポート: USB，CPU側ポート: Ethernetポート(1) (10.16 / 375-377 / 原本 p.377-379)

接続局がRCPUの場合

### 構成 (10.16 / 375 / 原本 p.377)

【図】構成 (原本 p.377)
- パソコン ―USB― GOT ―Ethernet― 接続局CPU(Ethernetポート)
- 接続局CPU ＋ 経由ユニット ―経由ネットワーク― 経由局CPU ＋ 経由ユニット

### アクセス可否およびプロパティのパターン (10.16 / 375 / 原本 p.377)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: RCPU | 接続局CPU: RCCPU | 接続局CPU: RモーションCPU | 経由ネットワーク | 経由局CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|---|---|
| ○(1) | ○(1)*3 | ○(1)*1*3 | CC IE TSN | × | × | × | × | × |
| ○(1) | ○(1)*3 | ○(1)*1*3 | CC IE Control<br>CC IE Field | ○(2)*2 | ○(2) | × | × | ○(2)*4*5 |
| ○(1) | ○(1)*3 | ○(1)*1*3 | MELSECNET/H | × | × | × | × | × |
| ○(1) | ○(1)*3 | ○(1)*1*3 | Ethernet | ○(2) | × | × | × | × |
| ○(1) | ○(1)*3 | ○(1)*1*3 | シリアルコミュニケーション | ○(3) | × | × | × | × |
| ○(1) | ○(1)*3 | ○(1)*1*3 | CC-Link | ○(4) | ○(4) | × | × | ○(4)*5 |

| 接続局CPU: RCPU | 接続局CPU: RCCPU | 接続局CPU: RモーションCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|---|---|
| ○(1) | ○(1)*3 | ○(1)*1*3 | CC IE TSN | × | × | × | × | × | × |
| ○(1) | ○(1)*3 | ○(1)*1*3 | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
| ○(1) | ○(1)*3 | ○(1)*1*3 | MELSECNET/H | × | × | × | × | × | × |
| ○(1) | ○(1)*3 | ○(1)*1*3 | Ethernet | × | × | ○(2) | × | × | × |
| ○(1) | ○(1)*3 | ○(1)*1*3 | シリアルコミュニケーション | × | × | × | × | × | × |
| ○(1) | ○(1)*3 | ○(1)*1*3 | CC-Link | × | × | × | × | × | × |

※接続局CPU列は原本では全行で共有セル。

> *1 RモーションCPUを経由して経由局CPUにアクセスできません。
> *2 RCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
> *3 マルチCPU構成時の，2号機以降の場合のみアクセス可能です。
> *4 接続局CPUがRCPUのCC-Link IEフィールドネットワークのみアクセス可能です。
> *5 FX5SCPUにはアクセスできません。

※要確認: *2 の主語が「RCPU」になっている(原本表記のまま)。RCPU→RCPUのCC IE Control/Fieldに付く脚注で，他の節の同種脚注(LCPU，Q12DCCPU-V 等)と比べると文意が合わない。

### プロパティ一覧 (10.16 / 376-377 / 原本 p.378-379)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2)*1 | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | (同左) | (同左) | (同左) |
| ActDestinationIONumber*2 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActHostAddress | 1.1.1.1 | 接続局側ユニットのホスト名またはIPアドレス | (同左) | (同左) | (同左) |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局<br>RCPU，QCPU(Qモード)，LCPU: 1(0x01)<br>上記以外 : 0(0x00) | 対象局<br>RCPU，QCPU(Qモード)，LCPU: 1(0x01)<br>上記以外 : 0(0x00) |
| ActIONumber*2 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 接続局側経由ユニットI/Oアドレス | 接続局側経由ユニットI/Oアドレス |
| ActMultiDropChannelNumber*3 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber*4 | 0(0x00) | 0(0x00)固定 | 対象局側ユニットネットワークNo. | 0(0x00)固定 | 0(0x00)固定 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USBGOT | (同左) | (同左) | (同左) |
| ActPacketType | 0x01(PACKET_PLC1) | PACKET_PLC1 | (同左) | (同左) | (同左) |
| ActConnectUnitNumber | 0(0x00) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActPortNumber | 1(PORT_1) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActCpuTimeOut | 0(0x00) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActParity | 1(ODD_PARITY) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActStopBits | 0(STOPBIT_ONE) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActSumCheck | 0(NO_SUM_CHECK) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActSourceStationNumber | 0(0x00) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActDestinationPortNumber | 0(0x00) | 5006 | (同左) | (同左) | (同左) |
| ActStationNumber*4 | 255(0xFF) | 255(0xFF)固定 | 対象局側ユニット局番 | 255(0xFF)固定 | 255(0xFF)固定 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | (同左) | (同左) | MELSECNET/10を含まない: 0(0x00) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | (同左) | (同左) | (同左) |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_GOT_RETHER | (同左) | (同左) | (同左) |

※「(同左)」は原本の共有セル。ActThroughNetworkType は○(1)〜○(3)が共有セル，○(4)のみ別セル。

> *1 Ethernetユニット(MELSEC iQ-Rシリーズ対応E71)経由のアクセスは，下記の事項に注意してください。
> ・ActNetworkNumber，ActStationNumberは，対象局側のMELSEC iQ-Rシリーズ対応E71のパラメータ設定で設定した値を指定してください。
> ・MELSEC iQ-Rシリーズ対応E71のパラメータ設定の「MNET/10ルーチング情報」を設定してください。また，設定を行う際，「MNET/10ルーチング方式」は自動応答方式以外(IPアドレス算出方式，テーブル変換方式，併用方式のいずれか)を指定してください。
> *2 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *3 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2
> *4 プロパティのパターンが(2)の場合，ActNetworkNumberおよびActStationNumberは対象局側のパラメータで設定した値を指定してください。

※*1 の2項目の行頭記号は原本では白抜き四角(■系の記号)。本mdでは「・」で表記。

---

## パソコン側ポート: USB，GOT2000/3000側ポート: USB，CPU側ポート: Ethernetポート(2) (10.16 / 378-379 / 原本 p.380-381)

接続局がFX5CPUの場合

### 構成 (10.16 / 378 / 原本 p.380)

【図】構成 (原本 p.380)
- パソコン ―USB― GOT ―Ethernet― 接続局CPU(Ethernetポート)
- 接続局CPU ＋ 経由ユニット ―経由ネットワーク― 経由局CPU ＋ 経由ユニット

### アクセス可否およびプロパティのパターン (10.16 / 378 / 原本 p.380)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: FX5CPU | 経由ネットワーク | 経由局CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × |
| ○(1) | CC IE Control<br>CC IE Field | × | × | × | × | ○(2)*1*2 |
| ○(1) | MELSECNET/H | × | × | × | × | × |
| ○(1) | Ethernet | × | × | × | × | × |
| ○(1) | シリアルコミュニケーション | × | × | × | × | × |
| ○(1) | CC-Link | × | × | × | × | ○(3)*2 |

| 接続局CPU: FX5CPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
| ○(1) | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
| ○(1) | MELSECNET/H | × | × | × | × | × | × |
| ○(1) | Ethernet | × | × | × | × | × | × |
| ○(1) | シリアルコミュニケーション | × | × | × | × | × | × |
| ○(1) | CC-Link | × | × | × | × | × | × |

※接続局CPU列は原本では全行で共有セル。

> *1 CC-Link IEフィールドネットワークのみアクセス可能です。
> *2 FX5SCPUにはアクセスできません。

### プロパティ一覧 (10.16 / 379 / 原本 p.381)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) |
|---|---|---|---|---|
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00) | (同左) | (同左) |
| ActConnectUnitNumber | 0(0x00) | 0(0x00) | (同左) | (同左) |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00) | (同左) | (同左) |
| ActCpuTimeOut | 0(0x00) | 0(0x00) | (同左) | (同左) |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | (同左) | (同左) |
| ActDataBits | 8(DATABIT_8) | 0(0x00) | (同左) | (同左) |
| ActDestinationIONumber | 0(0x00) | 0(0x00) | (同左) | 1023(0x3FF) |
| ActDestinationPortNumber | 0(0x00) | 5562 | (同左) | (同左) |
| ActDidPropertyBit | 1(0x01) | 1(0x01) | (同左) | 0(0x00) |
| ActDsidPropertyBit | 1(0x01) | 1(0x01) | (同左) | 0(0x00) |
| ActHostAddress | 1.1.1.1 | 接続局側ユニットのホスト名またはIPアドレス | (同左) | 接続局CPUのIPアドレス |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00) | (同左) | 1(0x01) |
| ActIONumber | 1023(0x3FF) | 1023(0x3FF) | (同左) | 接続局ユニット番号 |
| ActMultiDropChannelNumber | 0(0x00) | 0(0x00) | (同左) | (同左) |
| ActNetworkNumber | 0(0x00) | 0(0x00) | 対象局側ユニットネットワークNo. | 0(0x00) |
| ActPacketType | 0x01(PACKET_PLC1) | PACKET_PLC1(0x01) | (同左) | (同左) |
| ActParity | 1(ODD_PARITY) | 0(0x00) | (同左) | (同左) |
| ActPassword | Null | Null | (同左) | (同左) |
| ActPortNumber | 1(PORT_1) | 1(0x01) | (同左) | (同左) |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USBGOT(0x13) | (同左) | (同左) |
| ActStopBits | 0(STOPBIT_ONE) | 0(0x00) | (同左) | (同左) |
| ActSumCheck | 0(NO_SUM_CHECK) | 0(0x00) | (同左) | (同左) |
| ActSourceNetworkNumber | 0(0x00) | 0(0x00) | (同左) | (同左) |
| ActSourceStationNumber | 0(0x00) | 0(0x00) | (同左) | (同左) |
| ActStationNumber | 255(0xFF) | 255(0xFF) | 対象局側ユニット局番 | 255(0xFF) |
| ActTargetSimulator | 0(0x00) | 0(0x00) | (同左) | (同左) |
| ActThroughNetworkType | 0(0x00) | 0(0x00) | (同左) | (同左) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | (同左) | (同左) |
| ActUnitNumber | 0(0x00) | 0(0x00) | (同左) | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_GOT_FXVETHER(0x2007) | (同左) | (同左) |

※「(同左)」は原本の共有セル(○(1)〜○(3)の3列，または○(1)〜○(2)の2列)。本節の値は「固定」の語が付かない(原本どおり)。

---

## パソコン側ポート: USB，GOT2000/3000側ポート: USB，CPU側ポート: Ethernetポート(3) (10.16 / 380-383 / 原本 p.382-385)

接続局がQCPU(モード)またはQCCPUの場合

※原本表記のまま「QCPU(モード)」(「QCPU(Qモード)」の「Q」抜けと思われる。要確認)。

### 構成 (10.16 / 380 / 原本 p.382)

【図】構成 (原本 p.382)
- パソコン ―USB― GOT ―Ethernet― 接続局CPU(Ethernetポート)
- 接続局CPU ＋ 経由ユニット ―経由ネットワーク― 経由局CPU ＋ 経由ユニット

### アクセス可否およびプロパティのパターン (10.16 / 380-381 / 原本 p.382-383)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU*1: QnUDE(H)CPU/QnUD(P)VCPU | 経由ネットワーク | 経由局CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × |
| ○(1) | CC IE Control<br>CC IE Field | × | × | × | × | × |
| ○(1) | MELSECNET/H | × | × | × | × | × |
| ○(1) | Ethernet | × | × | × | × | × |
| ○(1) | シリアルコミュニケーション | × | × | × | × | × |
| ○(1) | CC-Link | × | × | × | × | × |

| 接続局CPU*1: QnUDE(H)CPU/QnUD(P)VCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード)*2 | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
| ○(1) | CC IE Control<br>CC IE Field | ○(2) | ○(2)*3 | ○(2)*4 | × | × | × |
| ○(1) | MELSECNET/H | ○(2) | ○(2) | × | × | × | × |
| ○(1) | Ethernet | ○(2) | × | × | × | × | × |
| ○(1) | シリアルコミュニケーション | ○(3) | × | ○(3) | × | × | × |
| ○(1) | CC-Link | ○(4) | ○(4) | ○(4) | × | × | × |

| 接続局CPU*1: QCCPU | 経由ネットワーク | 経由局CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × |
| ○(1) | CC IE Control<br>CC IE Field | × | × | × | × | × |
| ○(1) | MELSECNET/H | × | × | × | × | × |
| ○(1) | Ethernet | × | × | × | × | × |
| ○(1) | シリアルコミュニケーション | × | × | × | × | × |
| ○(1) | CC-Link | × | × | × | × | × |

| 接続局CPU*1: QCCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード)*2 | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
| ○(1) | CC IE Control<br>CC IE Field | ○(2) | ○(2)*3 | ○(2)*4 | × | × | × |
| ○(1) | MELSECNET/H | ○(2) | ○(2) | × | × | × | × |
| ○(1) | Ethernet | × | × | × | × | × | × |
| ○(1) | シリアルコミュニケーション | × | × | × | × | × | × |
| ○(1) | CC-Link | ○(4) | ○(4) | ○(4) | × | × | × |

※4つ目の表は原本 p.383。接続局CPU列は原本では全行で共有セル。

> *1 接続局CPUにリモートパスワードが設定されている場合は通信できません。
> *2 二重化CPUの場合はアクセスできません。
> *3 Q12DCCPU-V(基本機能モード)は，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。
> *4 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。

### プロパティ一覧 (10.16 / 382-383 / 原本 p.384-385)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2)*1 | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | (同左) | (同左) | (同左) |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActHostAddress | 1.1.1.1 | 接続局側ユニットのホスト名またはIPアドレス | (同左) | (同左) | (同左) |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局<br>QCPU(Qモード)，LCPU: 1(0x01)<br>上記以外: 0(0x00) | 対象局<br>QCPU(Qモード)，QCCPU，LCPU : 1(0x01)<br>上記以外: 0(0x00) |
| ActIONumber*2 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 接続局側経由ユニットI/Oアドレス | 接続局側経由ユニットI/Oアドレス |
| ActMultiDropChannelNumber*3 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber*4 | 0(0x00) | 0(0x00)固定 | 対象局側ユニットネットワークNo. | 0(0x00)固定 | 0(0x00)固定 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USBGOT(0x13) | (同左) | (同左) | (同左) |
| ActStationNumber*4 | 255(0xFF) | 255(0xFF)固定 | 対象局側ユニット局番 | 255(0xFF)固定 | 255(0xFF)固定 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | (同左) | (同左) | (同左) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | (同左) | (同左) | (同左) |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_GOT_QNETHER(0x41) | (同左) | (同左) | (同左) |

※「(同左)」は原本で4列共有セル。

> *1 Ethernetユニット(Qシリーズ対応E71)経由のアクセスは，下記の事項に注意してください。
> ・ActNetworkNumber，ActStationNumberは，対象局側のQシリーズ対応E71のパラメータ設定で設定した値を指定してください。
> ・Qシリーズ対応E71のパラメータ設定の「局番↔IP関連情報」を設定してください。また，設定を行う際，「局番↔IP関連情報設定方式」は自動応答方式以外(IPアドレス算出方式，テーブル変換方式，併用方式のいずれか)を指定してください。
> *2 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *3 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2
> *4 プロパティのパターンが(2)の場合，ActNetworkNumberおよびActStationNumberは対象局側のパラメータで設定した値を指定してください。

※*1 の「↔」はテキスト抽出で落ちる記号(9章の ActPortNumber と同じ「局番↔IP関連情報設定方式」)。

---

## パソコン側ポート: USB，GOT2000/3000側ポート: USB，CPU側ポート: Ethernetポート(4) (10.16 / 384-386 / 原本 p.386-388)

接続局がLCPUの場合

### 構成 (10.16 / 384 / 原本 p.386)

【図】構成 (原本 p.386)
- パソコン ―USB― GOT ―Ethernet― 接続局CPU(Ethernetポート)
- 接続局CPU ＋ 経由ユニット ―経由ネットワーク― 経由局CPU ＋ 経由ユニット

### アクセス可否およびプロパティのパターン (10.16 / 384 / 原本 p.386)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU*1: LCPU | 経由ネットワーク | 経由局CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × |
| ○(1) | CC IE Field*3 | × | × | × | × | × |
| ○(1) | MELSECNET/H | × | × | × | × | × |
| ○(1) | Ethernet | × | × | × | × | × |
| ○(1) | シリアルコミュニケーション | × | × | × | × | × |
| ○(1) | CC-Link | × | × | × | × | × |

| 接続局CPU*1: LCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード)*2 | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
| ○(1) | CC IE Field*3 | ○(4) | ○(4)*4 | ○(4) | × | × | × |
| ○(1) | MELSECNET/H | × | × | × | × | × | × |
| ○(1) | Ethernet | ○(4) | × | ○(4) | × | × | × |
| ○(1) | シリアルコミュニケーション | ○(2) | × | ○(2) | × | × | × |
| ○(1) | CC-Link | ○(3) | ○(3) | ○(3) | × | × | × |

※接続局CPU列は原本では全行で共有セル。本節はシリアルコミュニケーションが(2)，CC-Linkが(3)，CC IE Field/Ethernetが(4)(他の節とパターン番号の割当てが異なる。原本どおり)。

> *1 接続局CPUにリモートパスワードが設定されている場合は通信できません。
> *2 二重化CPUの場合はアクセスできません。
> *3 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
> *4 Q12DCCPU-V(基本機能モード)は，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。

### プロパティ一覧 (10.16 / 385-386 / 原本 p.387-388)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | (同左) | (同左) | (同左) |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 0(0x00)固定 |
| ActDestinationPortNumber | 0(0x00) | 5006 | (同左) | (同左) | (同左) |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 | 1(0x01)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 | 1(0x01)固定 |
| ActHostAddress | 1.1.1.1 | 接続局側ユニットのホスト名またはIPアドレス | (同左) | (同左) | (同左) |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 対象局<br>QCPU(Qモード)，LCPU: 1(0x01)<br>上記以外: 0(0x00) | 対象局<br>QCPU(Qモード)，QCCPU，LCPU: 1(0x01)<br>上記以外: 0(0x00) | 0(0x00)固定 |
| ActIONumber*1 | 1023(0x3FF) | 1023(0x3FF)固定 | 接続局側経由ユニットI/Oアドレス | 接続局側経由ユニットI/Oアドレス | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 | 0(0x00)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニットネットワークNo. |
| ActParity | 1(ODD_PARITY) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActPortNumber | 1(PORT_1) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USBGOT(0x13) | (同左) | (同左) | (同左) |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 255(0xFF)固定 | 255(0xFF)固定 | 対象局側ユニット局番 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | (同左) | (同左) | (同左) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | (同左) | (同左) | (同左) |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 | 0(0x00)固定 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_GOT_LNETHER(0x55) | (同左) | (同左) | (同左) |

※「(同左)」は原本で4列共有セル。

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2

---

## パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: Ethernetアダプタユニット (10.16 / 387-390 / 原本 p.389-392)

### 構成 (10.16 / 387 / 原本 p.389)

【図】構成 (原本 p.389)
- パソコン ―USB― GOT ―Ethernet― Ethernetアダプタユニット ― CC-Link IEフィールドネットワークユニット(接続局CPU側)
- 接続局CPU ＋ CC-Link IEフィールドネットワークユニット ＋ 経由ユニット ―経由ネットワーク― 経由局CPU ＋ 経由ユニット

### アクセス可否およびプロパティのパターン (10.16 / 387-388 / 原本 p.389-390)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: QnUDE(H)CPU/QnUD(P)VCPU | 経由ネットワーク | 経由局CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × |
| ○(1) | CC IE Control<br>CC IE Field | × | × | × | × | × |
| ○(1) | MELSECNET/H | × | × | × | × | × |
| ○(1) | Ethernet | × | × | × | × | × |
| ○(1) | シリアルコミュニケーション | × | × | × | × | × |
| ○(1) | CC-Link | × | × | × | × | × |

| 接続局CPU: QnUDE(H)CPU/QnUD(P)VCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード)*1 | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
| ○(1) | CC IE Control<br>CC IE Field | ○(2) | ○(2)*2 | ○(2)*3 | × | × | × |
| ○(1) | MELSECNET/H | ○(2) | ○(2) | × | × | × | × |
| ○(1) | Ethernet | ○(2) | × | × | × | × | × |
| ○(1) | シリアルコミュニケーション | ○(3) | × | ○(3) | × | × | × |
| ○(1) | CC-Link | ○(4) | ○(4) | ○(4) | × | × | × |

| 接続局CPU: LCPU | 経由ネットワーク | 経由局CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × |
| ○(1) | CC IE Field*3 | × | × | × | × | × |
| ○(1) | MELSECNET/H | × | × | × | × | × |
| ○(1) | Ethernet | × | × | × | × | × |
| ○(1) | シリアルコミュニケーション | × | × | × | × | × |
| ○(1) | CC-Link | × | × | × | × | × |

| 接続局CPU: LCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード)*1 | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
| ○(1) | CC IE Field*3 | ○(2) | × | ○(2) | × | × | × |
| ○(1) | MELSECNET/H | × | × | × | × | × | × |
| ○(1) | Ethernet | × | × | × | × | × | × |
| ○(1) | シリアルコミュニケーション | ○(3) | × | ○(3) | × | × | × |
| ○(1) | CC-Link | ○(4) | ○(4) | ○(4) | × | × | × |

※4つ目の表は原本 p.390。接続局CPU列は原本では全行で共有セル。

> *1 二重化CPUの場合はアクセスできません。
> *2 Q12DCCPU-V(基本機能モード)は，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。
> *3 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。

### プロパティ一覧 (10.16 / 389-390 / 原本 p.391-392)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | (同左) | (同左) | (同左) |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActHostAddress | 1.1.1.1 | Ethernetアダプタユニットのホスト名またはIPアドレス | (同左) | (同左) | (同左) |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | (同左) | (同左) | (同左) |
| ActIONumber*1 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 接続局側経由ユニットI/Oアドレス | 接続局側経由ユニットI/Oアドレス |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber*3 | 0(0x00) | 接続局側CC-Link IEフィールドネットワークユニットネットワークNo. | 対象局側ユニットネットワークNo. | 接続局側CC-Link IEフィールドネットワークユニットネットワークNo. | 接続局側CC-Link IEフィールドネットワークユニットネットワークNo. |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USBGOT(0x13) | (同左) | (同左) | (同左) |
| ActStationNumber*3 | 255(0xFF) | 接続局側CC-Link IEフィールドネットワークユニット局番 | 対象局側ユニット局番 | 接続局側CC-Link IEフィールドネットワークユニット局番 | 接続局側CC-Link IEフィールドネットワークユニット局番 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | (同左) | (同左) | (同左) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | (同左) | (同左) | (同左) |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_GOT_NZ2GF_ETB(0x5B) | (同左) | (同左) | (同左) |

※「(同左)」は原本で4列共有セル。

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2
> *3 プロパティのパターンが(1)(3)(4)の場合，ActNetworkNumberおよびActStationNumberは対象局側のCC-Link IEフィールドネットワークユニットのパラメータで設定した値を指定してください。
> プロパティのパターンが(2)の場合，ActNetworkNumberおよびActStationNumberは対象局側のパラメータで設定した値を指定してください。

---

## パソコン側ポート: USB，GOT2000/3000側ポート: USB，CPU側ポート: Ethernetアダプタ/Ethernetユニット (10.16 / 391-392 / 原本 p.393-394)

接続局がFXCPUの場合

### 構成 (10.16 / 391 / 原本 p.393)

Ethernetアダプタ: FX3U-ENET-ADPの場合

【図】構成 (原本 p.393)
- パソコン ―USB― GOT ―Ethernet― Ethernetアダプタ(接続局CPUに装着)
- Ethernetアダプタ ＋ 接続局CPU ＋ 経由ユニット ―経由ネットワーク― 経由局CPU ＋ 経由ユニット

Ethernetユニット: FX3U-ENET-Lの場合

【図】構成 (原本 p.393)
- パソコン ―USB― GOT ―Ethernet― Ethernetユニット(接続局CPU側)
- 接続局CPU ＋ Ethernetユニット ＋ 経由ユニット ―経由ネットワーク― 経由局CPU ＋ 経由ユニット

### アクセス可否およびプロパティのパターン (10.16 / 391 / 原本 p.393)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: FXCPU | 経由ネットワーク | 経由局CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × |
| ○(1)*1 | CC IE Control<br>CC IE Field | × | × | × | × | × |
| ○(1)*1 | MELSECNET/H | × | × | × | × | × |
| ○(1)*1 | Ethernet | × | × | × | × | × |
| ○(1)*1 | シリアルコミュニケーション | × | × | × | × | × |
| ○(1)*1 | CC-Link | × | × | × | × | × |

| 接続局CPU: FXCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × | × |
| ○(1)*1 | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
| ○(1)*1 | MELSECNET/H | × | × | × | × | × | × |
| ○(1)*1 | Ethernet | × | × | × | × | × | × |
| ○(1)*1 | シリアルコミュニケーション | × | × | × | × | × | × |
| ○(1)*1 | CC-Link | × | × | × | × | × | × |

※接続局CPU列は原本では全行で共有セル。

> *1 FX3SCPU(FX3U-ENET-ADP)，FX3G(C)CPU，FX3U(C)CPUのみアクセス可能です。

### プロパティ一覧 (10.16 / 392 / 原本 p.394)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) |
|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ |
| ActHostAddress | 1.1.1.1 | FX3U-ENET-ADPユニットのホスト名またはIPアドレス<br>FX3U-ENET-Lユニットのホスト名またはIPアドレス |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USBGOT |
| ActTimeOut | 10000 | ms単位でユーザ任意 |
| ActUnitType | 0x13(UNIT_QNCPU) | FX3U-ENET-ADP: UNIT_GOT_FXETHER<br>FX3U-ENET-L: UNIT_GOT_FXENET |

※ActHostAddress と ActUnitType の○(1)欄は，原本ではユニットごとに2段に分かれている。

---

## パソコン側ポート: USB，GOT2000/3000側ポート: USB，CPU側ポート: Ethernetユニット (10.16 / 393-394 / 原本 p.395-396)

接続先CPUがFX5CPUの場合

### 構成 (10.16 / 393 / 原本 p.395)

【図】構成 (原本 p.395)
- パソコン ―USB― GOT ―Ethernet― Ethernetユニット(接続局CPU側)
- 接続局CPU ＋ Ethernetユニット ＋ 経由ユニット ―経由ネットワーク― 経由局CPU ＋ 経由ユニット

### アクセス可否およびプロパティのパターン (10.16 / 393 / 原本 p.395)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: FX5CPU | 経由ネットワーク | 経由局CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × |
| ○(1)*1 | CC IE Control<br>CC IE Field | × | × | × | × | × |
| ○(1)*1 | MELSECNET/H | × | × | × | × | × |
| ○(1)*1 | Ethernet | × | × | × | × | × |
| ○(1)*1 | シリアルコミュニケーション | × | × | × | × | × |
| ○(1)*1 | CC-Link | × | × | × | × | × |

| 接続局CPU: FX5CPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × | × |
| ○(1)*1 | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
| ○(1)*1 | MELSECNET/H | × | × | × | × | × | × |
| ○(1)*1 | Ethernet | × | × | × | × | × | × |
| ○(1)*1 | シリアルコミュニケーション | × | × | × | × | × | × |
| ○(1)*1 | CC-Link | × | × | × | × | × | × |

※接続局CPU列は原本では全行で共有セル。

> *1 FX5UCPU，FX5UJCPUのみアクセス可能です。

### プロパティ一覧 (10.16 / 393-394 / 原本 p.395-396)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) |
|---|---|---|
| ActConnectUnitNumber | 0(0x00) | 0(0x00)固定 |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 |
| ActDestinationPortNumber | 0(0x00) | 5554固定 |
| ActDidPropertyBit | 1(0x01) | 1(0x01)(無効) |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)(無効) |
| ActHostAddress | 1.1.1.1 | 接続先CPUのホスト名またはIPアドレス |
| ActIONumber | 1023(0x3FF) | 1023(0x3FF)固定 |
| ActMultiDropChannelNumber | 0(0x00) | 0(0x00)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_USBGOT |
| ActPacketType | 0x01(PACKET_PLC1) | PACKET_PLC1固定 |
| ActPortNumber | 1(PORT_1) | PORT_1 |
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 |
| ActCpuTimeOut | 0(0x00) | 0(0x00)固定 |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 |
| ActParity | 1(ODD_PARITY) | 0(0x00)固定 |
| ActStopBits | 0(STOPBIT_ONE) | 0(0x00)固定 |
| ActSumCheck | 0(NO_SUM_CHECK) | 0(0x00)固定 |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 |
| ActSourceNetworkNumber | 0(0x00) | 0(0x00)固定 |
| ActSourceStationNumber | 0(0x00) | 0(0x00)固定 |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 |
| ActThroughNetworkType | 0(0x00) | 0(0x00)固定 |
| ActTimeOut | 10000 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_GOT_FXVENET |

※原本では p.395 末尾(ActHostAddress まで)と p.396 に分かれた1つの表。
