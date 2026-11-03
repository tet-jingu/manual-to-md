# MX Component Version 5 リファレンスマニュアル 10章 各通信経路で設定するプロパティ (9/9) p.397-417

| 項目 | 内容 |
|---|---|
| 原本 | 【三菱】MX Component Version 5 リファレンスマニュアル (SH-082394J) |
| メーカー | 三菱電機 |
| 原本ファイル | `PDF/【三菱】MX Component Version 5 リファレンスマニュアル_sh082394j.pdf` (全696ページ) |
| 本ファイルの範囲 | 10.16 GOTトランスペアレント通信のうち，パソコン側ポート: Ethernetボード経由の各節 (印刷ページ 395-415 / PDF p.397-417)。10章の最後まで |
| 出典表記 | `(節 / 印刷ページ / 原本 p.PDFページ)` |
| 作成日 | 2026-11-03 |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。
> 本文中の「○ページ」はすべて原本の**印刷ページ番号**です(PDFページ = 印刷ページ + 2)。
> 表の結合セル(複数パターン共通の値、接続局CPU列の縦結合)は各セルに展開しています。展開した値は原本では1つのセルです。

## 主要用語 対訳表 (Glossary)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| GOTトランスペアレント通信 | GOT transparent communication | UNIT_GOTETHER_* | 参考訳 |
| パソコン側ポート / GOT側ポート / CPU側ポート | PC side port / GOT side port / CPU side port | — | 参考訳 |
| Ethernetボード | Ethernet board | — | 参考訳 |
| 接続局CPU | Connected station CPU | — | 参考訳 |
| 経由ネットワーク | Relay network | CC IE TSN / CC IE Control / CC IE Field / MELSECNET/H / Ethernet / シリアルコミュニケーション / CC-Link | 参考訳 |
| 経由局CPU | Relay station CPU | — | 参考訳 |
| 経由ユニット | Relay module | — | 参考訳 |
| 対象局 | Target station | — | 参考訳 |
| アクセス可否 | Accessibility | ○(n) / × | 参考訳 |
| プロパティのパターン | Property pattern | (1)〜(4) | 参考訳 |
| デフォルト値 | Default value | — | 参考訳 |
| 固定 | Fixed | — | 参考訳 |
| シングルCPU / マルチCPU / 二重化CPU | Single CPU / Multiple CPU / Redundant CPU | — | 参考訳 |
| 接続号機 / 1号機〜4号機 | Connected CPU No. / CPU No.1 to No.4 | 1023(0x3FF) / 992(0x3E0)〜995(0x3E3) | 参考訳 |
| 制御系 | Control system | 976(0x3D0) | 参考訳 |
| I/Oアドレス / I/O先頭No. | I/O address / Start I/O No. | ActIONumber / ActDestinationIONumber | 参考訳 |
| マルチドロップチャネルNo. | Multidrop channel No. | ActMultiDropChannelNumber | 参考訳 |
| ユニットのデフォルトチャネル | Default channel of the module | 0 | 参考訳 |
| ネットワークNo. / 局番 | Network No. / Station No. | ActNetworkNumber / ActStationNumber | 参考訳 |
| GOTのポート番号 | GOT port number | ActDestinationPortNumber | 参考訳 |
| GOTのホスト名 / IPアドレス | GOT host name / IP address | ActHostAddress | 参考訳 |
| 拡張設定(ネットワークNo.局番設定) | Extended setting (network No./station No. setting) | — | 参考訳 |
| 自局宛て設定 | Setting addressed to own station | 1NetworkNumber: 0x00, 1StationNumber: 0xFF | 原本併記 |
| シリアルコミュニケーションユニット | Serial communication module | C24 (RJ71C24 / QJ71C24 / LJ71C24) | 参考訳 |
| Qシリーズ対応E71 | Q series compatible E71 | QJ71E71 | 参考訳 |
| バス | Bus | UNIT_GOTETHER_QBUS | 参考訳 |
| 基本機能モード | Basic function mode | Q12DCCPU-V | 参考訳 |
| 未サポート | Not supported | — | 参考訳 |

## 変換範囲表

| 原本ページ(PDF) | 印刷ページ | 節 | 扱い |
|---|---|---|---|
| p.397-398 | 395-396 | パソコン側ポート: Ethernetボード，GOT2000ポート: Ethernetポート，CPU側ポート: シリアル(1) 接続局がFX5CPU | 全文(構成図は文章化) |
| p.399-400 | 397-398 | 同 シリアル(2) 接続局がQCPU(Qモード)またはQCCPU | 全文 |
| p.401-402 | 399-400 | 同 シリアル(3) 接続局がLCPU | 全文 |
| p.403 | 401 | 同 シリアル(4) 接続局がFXCPU | 全文 |
| p.404-406 | 402-404 | パソコン側ポート: Ethernetボード，GOT2000側ポート: Ethernetポート，CPU側ポート: シリアルコミュニケーションユニット(1) MELSEC iQ-Rシリーズ対応C24 | 全文 |
| p.407-408 | 405-406 | 同 シリアルコミュニケーションユニット(2) Qシリーズ対応C24 | 全文 |
| p.409-410 | 407-408 | 同 シリアルコミュニケーションユニット(3) Lシリーズ対応C24 | 全文 |
| p.411-413 | 409-411 | パソコン側ポート: Ethernetボード，GOT2000側ポート: Ethernetポート，CPU側ポート: バス | 全文 |
| p.414-415 | 412-413 | パソコン側ポート: Ethernetボード，GOT2000/3000ポート: Ethernetポート，CPU側ポート: Ethernetポート | 全文 |
| p.416-417 | 414-415 | パソコン側ポート: Ethernetボード，GOT2000/3000ポート: Ethernet ポート，CPU側ポート: Qシリーズ対応E71 | 全文 |
| p.192-396 | 190-394 | 10章の他の範囲(10.1〜10.15，10.16のUSB/シリアル経由の各節) | 別ファイル(10-1〜10-8) |
| p.1-191, p.418-696 | — | 前付け・1〜9章・11章以降 | 別ファイルまたは**未変換** |

## 目次

- シリアル(1) 接続局がFX5CPUの場合
- シリアル(2) 接続局がQCPU(Qモード)またはQCCPUの場合
- シリアル(3) 接続局がLCPUの場合
- シリアル(4) 接続局がFXCPUの場合
- シリアルコミュニケーションユニット(1) MELSEC iQ-Rシリーズ対応C24
- シリアルコミュニケーションユニット(2) Qシリーズ対応C24
- シリアルコミュニケーションユニット(3) Lシリーズ対応C24
- CPU側ポート: バス
- CPU側ポート: Ethernetポート(GOT2000/3000)
- CPU側ポート: Qシリーズ対応E71(GOT2000/3000)

---

## パソコン側ポート: Ethernetボード，GOT2000ポート: Ethernetポート，CPU側ポート: シリアル(1) (10.16 / 395-396 / 原本 p.397-398)

接続局がFX5CPUの場合

### 構成 (10.16 / 395 / 原本 p.397)

【図】構成図 (10.16 / 395 / 原本 p.397)
- パソコン ―Ethernet― GOT ―シリアル― 接続局CPU＋経由ユニット
- 接続局側の経由ユニット ―経由ネットワーク― 経由局CPU＋経由ユニット

### アクセス可否およびプロパティのパターン (10.16 / 395 / 原本 p.397)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: FX5CPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × |
| (同上) | CC IE Control<br>CC IE Field | × | × | × | × | ○(2)*1*2 |
| (同上) | MELSECNET/H | × | × | × | × | × |
| (同上) | Ethernet | × | × | × | × | × |
| (同上) | シリアルコミュニケーション | × | × | × | × | × |
| (同上) | CC-Link | × | × | × | × | ○(3)*2 |

| 接続局CPU: FX5CPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
| (同上) | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
| (同上) | MELSECNET/H | × | × | × | × | × | × |
| (同上) | Ethernet | × | × | × | × | × | × |
| (同上) | シリアルコミュニケーション | × | × | × | × | × | × |
| (同上) | CC-Link | × | × | × | × | × | × |

> *1 CC-Link IEフィールドネットワークのみアクセス可能です。
> *2 FX5SCPUにはアクセスできません。

### プロパティ一覧 (10.16 / 396 / 原本 p.398)

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
| ActDestinationPortNumber | 0(0x00) | GOTのポートNo. | GOTのポートNo. | GOTのポートNo. |
| ActDidPropertyBit | 1(0x01) | 1(0x01) | 1(0x01) | 0(0x00) |
| ActDsidPropertyBit | 1(0x01) | 1(0x01) | 1(0x01) | 0(0x00) |
| ActHostAddress | 1.1.1.1 | GOTのホスト名かIPアドレス | GOTのホスト名かIPアドレス | GOTのホスト名かIPアドレス |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00) | 0(0x00) | 1(0x01) |
| ActIONumber | 1023(0x3FF) | 1023(0x3FF) | 1023(0x3FF) | 接続局ユニット番号 |
| ActMultiDropChannelNumber | 0(0x00) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActNetworkNumber | 0(0x00) | 0(0x00) | 対象局側ユニット<br>ネットワークNo. | 0(0x00) |
| ActPacketType | 0x01(PACKET_PLC1) | PACKET_PLC1(0x01) | PACKET_PLC1(0x01) | PACKET_PLC1(0x01) |
| ActParity | 1(ODD_PARITY) | 1(0x01) | 1(0x01) | 1(0x01) |
| ActPassword | Null | Null | Null | Null |
| ActPortNumber | 1(PORT_1) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_TCPIP(0x05) | PROTOCOL_TCPIP(0x05) | PROTOCOL_TCPIP(0x05) |
| ActStopBits | 0(STOPBIT_ONE) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActSumCheck | 0(NO_SUM_CHECK) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActSourceNetworkNumber | 0(0x00) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActSourceStationNumber | 0(0x00) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActStationNumber | 255(0xFF) | 255(0xFF) | 対象局側ユニット局番 | 255(0xFF) |
| ActTargetSimulator | 0(0x00) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActThroughNetworkType | 0(0x00) | 0(0x00) | 0(0x00) | 0(0x00) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00) | 0(0x00) | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_GOTETHER_FXVCPU(0x2006) | UNIT_GOTETHER_FXVCPU(0x2006) | UNIT_GOTETHER_FXVCPU(0x2006) |

※この表は原本どおり値に「固定」が付かない(他の節の表は「0(0x00)固定」等)。

## パソコン側ポート: Ethernetボード，GOT2000ポート: Ethernetポート，CPU側ポート: シリアル(2) (10.16 / 397-398 / 原本 p.399-400)

接続局がQCPU(Qモード)またはQCCPUの場合

### 構成 (10.16 / 397 / 原本 p.399)

【図】構成図 (10.16 / 397 / 原本 p.399)
- パソコン ―Ethernet― GOT ―シリアル― 接続局CPU＋経由ユニット
- 接続局側の経由ユニット ―経由ネットワーク― 経由局CPU＋経由ユニット

### アクセス可否およびプロパティのパターン (10.16 / 397 / 原本 p.399)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: QCPU(Qモード) | 接続局CPU: QCCPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|---|
| ○(1)*1 | ○(1)*4 | CC IE TSN | × | × | × | × | × |
| (同上) | (同上) | CC IE Control<br>CC IE Field | × | × | × | × | × |
| (同上) | (同上) | MELSECNET/H | × | × | × | × | × |
| (同上) | (同上) | Ethernet | × | × | × | × | × |
| (同上) | (同上) | シリアルコミュニケーション | × | × | × | × | × |
| (同上) | (同上) | CC-Link | × | × | × | × | × |

| 接続局CPU: QCPU(Qモード) | 接続局CPU: QCCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード)*1 | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|---|
| ○(1)*1 | ○(1)*4 | CC IE TSN | × | × | × | × | × | × |
| (同上) | (同上) | CC IE Control<br>CC IE Field | ○(2) | ○(2)*2 | ○(2)*3 | × | × | × |
| (同上) | (同上) | MELSECNET/H | ○(2) | ○(2) | × | × | × | × |
| (同上) | (同上) | Ethernet | × | × | × | × | × | × |
| (同上) | (同上) | シリアルコミュニケーション | ○(3) | × | ○(3) | × | × | × |
| (同上) | (同上) | CC-Link | ○(4) | ○(4) | ○(4) | × | × | × |

> *1 二重化CPUの場合はアクセスできません。
> *2 Q12DCCPU-V(基本機能モード)は，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。
> *3 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
> *4 Q24DHCCPU-V，Q24DHCCPU-LS，Q24DHCCPU-VG，Q26DHCCPU-LSは，マルチCPU構成時の2号機以降の場合のみアクセス可能です。

### プロパティ一覧 (10.16 / 398 / 原本 p.400)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) |
| ActDestinationPortNumber | 0(0x00) | GOTのポート番号 | GOTのポート番号 | GOTのポート番号 | GOTのポート番号 |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActHostAddress | 1.1.1.1 | GOTのホスト名またはIPアドレス | GOTのホスト名またはIPアドレス | GOTのホスト名またはIPアドレス | GOTのホスト名またはIPアドレス |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局<br>QCPU(Qモード)，<br>LCPU: 1(0x01)<br>上記以外: 0(0x00) | 対象局<br>QCPU(Qモード)，<br>QCCPU，LCPU: 1(0x01)<br>上記以外: 0(0x00) |
| ActIONumber*1 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 接続局側ユニットI/Oアドレス | 接続局側ユニットI/Oアドレス |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニットネットワークNo. | 0(0x00)固定 | 0(0x00)固定 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_TCPIP(0x05) | PROTOCOL_TCPIP(0x05) | PROTOCOL_TCPIP(0x05) | PROTOCOL_TCPIP(0x05) |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 対象局側ユニット局番 | 255(0xFF)固定 | 255(0xFF)固定 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_GOTETHER_QNCPU(0x56) | UNIT_GOTETHER_QNCPU(0x56) | UNIT_GOTETHER_QNCPU(0x56) | UNIT_GOTETHER_QNCPU(0x56) |

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2

## パソコン側ポート: Ethernetボード，GOT2000ポート: Ethernetポート，CPU側ポート: シリアル(3) (10.16 / 399-400 / 原本 p.401-402)

接続局がLCPUの場合

### 構成 (10.16 / 399 / 原本 p.401)

【図】構成図 (10.16 / 399 / 原本 p.401)
- パソコン ―Ethernet― GOT ―シリアル― 接続局CPU＋経由ユニット
- 接続局側の経由ユニット ―経由ネットワーク― 経由局CPU＋経由ユニット

### アクセス可否およびプロパティのパターン (10.16 / 399 / 原本 p.401)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: LCPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × |
| (同上) | CC IE Field*2 | × | × | × | × | × |
| (同上) | MELSECNET/H | × | × | × | × | × |
| (同上) | Ethernet | × | × | × | × | × |
| (同上) | シリアルコミュニケーション | × | × | × | × | × |
| (同上) | CC-Link | × | × | × | × | × |

| 接続局CPU: LCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード)*1 | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
| (同上) | CC IE Field*2 | ○(4) | ○(4)*3 | ○(4) | × | × | × |
| (同上) | MELSECNET/H | × | × | × | × | × | × |
| (同上) | Ethernet | × | × | × | × | × | × |
| (同上) | シリアルコミュニケーション | ○(2) | × | ○(2) | × | × | × |
| (同上) | CC-Link | ○(3) | ○(3) | ○(3) | × | × | × |

> *1 二重化CPUの場合はアクセスできません。
> *2 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
> *3 Q12DCCPU-V(基本機能モード)は，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。

※この節の表には CC IE Control の行が無い(経由ネットワークは CC IE Field*2 のみ)。*2 の注記内容は CC-Link IEコントローラネットワークについての説明(原本どおり)。

### プロパティ一覧 (10.16 / 400 / 原本 p.402)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 0(0x00)固定 |
| ActDestinationPortNumber | 0(0x00) | GOTのポート番号 | GOTのポート番号 | GOTのポート番号 | GOTのポート番号 |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 | 1(0x01)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 | 1(0x01)固定 |
| ActHostAddress | 1.1.1.1 | GOTのホスト名またはIPアドレス | GOTのホスト名またはIPアドレス | GOTのホスト名またはIPアドレス | GOTのホスト名またはIPアドレス |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 対象局<br>QCPU(Qモード)，<br>LCPU: 1(0x01)<br>上記以外: 0(0x00) | 対象局<br>QCPU(Qモード)，<br>QCCPU，LCPU: 1(0x01)<br>上記以外: 0(0x00) | 0(0x00)固定 |
| ActIONumber*1 | 1023(0x3FF) | 1023(0x3FF)固定 | 接続局側経由ユニットI/Oアドレス | 接続局側経由ユニットI/Oアドレス | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 | 0(0x00)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニットネットワークNo. |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_TCPIP(0x05) | PROTOCOL_TCPIP(0x05) | PROTOCOL_TCPIP(0x05) | PROTOCOL_TCPIP(0x05) |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 255(0xFF)固定 | 255(0xFF)固定 | 対象局側ユニット局番 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 | 0(0x00)固定 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_GOTETHER_LNCPU(0x57) | UNIT_GOTETHER_LNCPU(0x57) | UNIT_GOTETHER_LNCPU(0x57) | UNIT_GOTETHER_LNCPU(0x57) |

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2

## パソコン側ポート: Ethernetボード，GOT2000ポート: Ethernetポート，CPU側ポート: シリアル(4) (10.16 / 401 / 原本 p.403)

接続局がFXCPUの場合

### 構成 (10.16 / 401 / 原本 p.403)

【図】構成図 (10.16 / 401 / 原本 p.403)
- パソコン ―Ethernet― GOT ―シリアル― 接続局CPU＋経由ユニット
- 接続局側の経由ユニット ―経由ネットワーク― 経由局CPU＋経由ユニット

### アクセス可否およびプロパティのパターン (10.16 / 401 / 原本 p.403)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: FXCPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × |
| (同上) | CC IE Control<br>CC IE Field | × | × | × | × | × |
| (同上) | MELSECNET/H | × | × | × | × | × |
| (同上) | Ethernet | × | × | × | × | × |
| (同上) | シリアルコミュニケーション | × | × | × | × | × |
| (同上) | CC-Link | × | × | × | × | × |

| 接続局CPU: FXCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
| (同上) | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
| (同上) | MELSECNET/H | × | × | × | × | × | × |
| (同上) | Ethernet | × | × | × | × | × | × |
| (同上) | シリアルコミュニケーション | × | × | × | × | × | × |
| (同上) | CC-Link | × | × | × | × | × | × |

### プロパティ一覧 (10.16 / 401 / 原本 p.403)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) |
|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ |
| ActDestinationPortNumber*1 | 0(0x00) | GOTのポート番号 |
| ActHostAddress | 1.1.1.1 | GOTのホスト名かIPアドレス |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_TCPIP |
| ActTimeOut | 10000 | ms単位でユーザ任意 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_GOTETHER_FXCPU |

> *1 ActPortNumberはGOT側で設定した値を指定してください。

※要確認: 脚注*1は表中の ActDestinationPortNumber に付いているが，本文は「ActPortNumber」と記載(原本どおり。p.406の同種脚注は「ActDestinationPortNumber」)。

## パソコン側ポート: Ethernetボード，GOT2000側ポート: Ethernetポート，CPU側ポート: シリアルコミュニケーションユニット(1) (10.16 / 402-404 / 原本 p.404-406)

接続局側がMELSEC iQ-Rシリーズ対応C24の場合

### 構成 (10.16 / 402 / 原本 p.404)

【図】構成図 (10.16 / 402 / 原本 p.404)
- パソコン ―Ethernet― GOT ―シリアル― 接続局CPU＋MELSEC iQ-Rシリーズ対応C24＋経由ユニット
- 接続局側の経由ユニット ―経由ネットワーク― 経由局CPU＋経由ユニット

### アクセス可否およびプロパティのパターン (10.16 / 402 / 原本 p.404)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: RCPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × |
| (同上) | CC IE Control<br>CC IE Field | ○(4)*1 | ○(4) | × | × | × |
| (同上) | MELSECNET/H | × | × | × | × | × |
| (同上) | Ethernet | × | × | × | × | × |
| (同上) | シリアルコミュニケーション | ○(2) | × | × | × | × |
| (同上) | CC-Link | ○(3) | ○(3) | × | × | × |

| 接続局CPU: RCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
| (同上) | CC IE Control<br>CC IE Field | ○(4) | × | ○(4)*1 | × | × | × |
| (同上) | MELSECNET/H | ○(4) | × | × | × | × | × |
| (同上) | Ethernet | × | × | × | × | × | × |
| (同上) | シリアルコミュニケーション | ○(2) | × | ○(2) | × | × | × |
| (同上) | CC-Link | ○(3) | × | ○(3) | × | × | × |

> *1 RCPU，LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。

### プロパティ一覧 (10.16 / 403 / 原本 p.405)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDestinationIONumber*1 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) |
| ActDestinationPortNumber*2 | 0(0x00) | GOTのポート番号 | GOTのポート番号 | GOTのポート番号 | GOTのポート番号 |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActHostAddress | 1.1.1.1 | GOTのホスト名かIPアドレス | GOTのホスト名かIPアドレス | GOTのホスト名かIPアドレス | GOTのホスト名かIPアドレス |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局<br>RCPU，QCPU(Qモード)，LCPU: 1(0x01)<br>上記以外 : 0(0x00) | 対象局<br>RCPU，QCPU(Qモード)，QCCPU，LCPU: 1(0x01)<br>上記以外 : 0(0x00) |
| ActIONumber*1 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 接続局側ユニットI/Oアドレス | 接続局側ユニットI/Oアドレス |
| ActMultiDropChannelNumber*3 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber*4 | 0(0x00) | 0(0x00)固定 | 対象局側ユニットのネットワークNo. | 0(0x00)固定 | 0(0x00)固定 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_TCPIP | PROTOCOL_TCPIP | PROTOCOL_TCPIP | PROTOCOL_TCPIP |
| ActPacketType | 0x01(PACKET_PLC1) | PACKET_PLC1 | PACKET_PLC1 | PACKET_PLC1 | PACKET_PLC1 |
| ActConnectUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActPortNumber | 1(PORT_1) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActCpuTimeOut | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActParity | 1(ODD_PARITY) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActStopBits | 0(STOPBIT_ONE) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActSumCheck | 0(NO_SUM_CHECK) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActSourceNetworkNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActSourceStationNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActStationNumber*4 | 255(0xFF) | 255(0xFF)固定 | 対象局側ユニット局番 | 255(0xFF)固定 | 255(0xFF)固定 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_GOTETHER_RJ71C24 | UNIT_GOTETHER_RJ71C24 | UNIT_GOTETHER_RJ71C24 | UNIT_GOTETHER_RJ71C24 |

※原本では表がp.405〜p.406の2ページにまたがる(ActUnitType行のみp.406)。

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 ActDestinationPortNumberはGOT側で設定した値を指定してください。
> *3 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2
> *4 プロパティのパターンが○(2)の場合，ActNetworkNumberおよびActStationNumberは対象局側のパラメータで設定した値を指定してください。

## パソコン側ポート: Ethernetボード，GOT2000側ポート: Ethernetポート，CPU側ポート: シリアルコミュニケーションユニット(2) (10.16 / 405-406 / 原本 p.407-408)

接続局側がQシリーズ対応C24の場合

### 構成 (10.16 / 405 / 原本 p.407)

【図】構成図 (10.16 / 405 / 原本 p.407)
- パソコン ―Ethernet― GOT ―シリアル― 接続局CPU＋Qシリーズ対応C24＋経由ユニット
- 接続局側の経由ユニット ―経由ネットワーク― 経由局CPU＋経由ユニット

### アクセス可否およびプロパティのパターン (10.16 / 405 / 原本 p.407)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: QCPU(Qモード) | 接続局CPU: QCCPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|---|
| ○(1)*1 | ○(1) | CC IE TSN | × | × | × | × | × |
| (同上) | (同上) | CC IE Control<br>CC IE Field | × | × | × | × | × |
| (同上) | (同上) | MELSECNET/H | × | × | × | × | × |
| (同上) | (同上) | Ethernet | × | × | × | × | × |
| (同上) | (同上) | シリアルコミュニケーション | × | × | × | × | × |
| (同上) | (同上) | CC-Link | × | × | × | × | × |

| 接続局CPU: QCPU(Qモード) | 接続局CPU: QCCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード)*1 | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|---|
| ○(1)*1 | ○(1) | CC IE TSN | × | × | × | × | × | × |
| (同上) | (同上) | CC IE Control<br>CC IE Field | ○(2) | ○(2)*2 | ○(2)*3 | × | × | × |
| (同上) | (同上) | MELSECNET/H | ○(2) | ○(2) | × | × | × | × |
| (同上) | (同上) | Ethernet | × | × | × | × | × | × |
| (同上) | (同上) | シリアルコミュニケーション | ○(3) | × | ○(3) | × | × | × |
| (同上) | (同上) | CC-Link | ○(4) | ○(4) | ○(4) | × | × | × |

> *1 二重化CPUの場合はアクセスできません。
> *2 Q12DCCPU-V(基本機能モード)は，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。
> *3 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。

### プロパティ一覧 (10.16 / 406 / 原本 p.408)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) |
| ActDestinationPortNumber | 0(0x00) | GOTのポート番号 | GOTのポート番号 | GOTのポート番号 | GOTのポート番号 |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActHostAddress | 1.1.1.1 | GOTのホスト名またはIPアドレス | GOTのホスト名またはIPアドレス | GOTのホスト名またはIPアドレス | GOTのホスト名またはIPアドレス |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局<br>QCPU(Qモード)，<br>LCPU: 1(0x01)<br>上記以外: 0(0x00) | 対象局<br>QCPU(Qモード)，<br>QCCPU，LCPU: 1(0x01)<br>上記以外: 0(0x00) |
| ActIONumber*1 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 接続局側ユニットI/Oアドレス | 接続局側ユニットI/Oアドレス |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニットネットワークNo. | 0(0x00)固定 | 0(0x00)固定 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_TCPIP(0x05) | PROTOCOL_TCPIP(0x05) | PROTOCOL_TCPIP(0x05) | PROTOCOL_TCPIP(0x05) |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 対象局側ユニット局番 | 255(0xFF)固定 | 255(0xFF)固定 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_GOTETHER_QNCPU(0x56) | UNIT_GOTETHER_QNCPU(0x56) | UNIT_GOTETHER_QNCPU(0x56) | UNIT_GOTETHER_QNCPU(0x56) |

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2

## パソコン側ポート: Ethernetボード，GOT2000側ポート: Ethernetポート，CPU側ポート: シリアルコミュニケーションユニット(3) (10.16 / 407-408 / 原本 p.409-410)

接続局側がLシリーズ対応C24の場合

### 構成 (10.16 / 407 / 原本 p.409)

【図】構成図 (10.16 / 407 / 原本 p.409)
- パソコン ―Ethernet― GOT ―シリアル― 接続局CPU＋Lシリーズ対応C24＋経由ユニット
- 接続局側の経由ユニット ―経由ネットワーク― 経由局CPU＋経由ユニット

### アクセス可否およびプロパティのパターン (10.16 / 407 / 原本 p.409)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: LCPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × |
| (同上) | CC IE Field*2 | × | × | × | × | × |
| (同上) | MELSECNET/H | × | × | × | × | × |
| (同上) | Ethernet | × | × | × | × | × |
| (同上) | シリアルコミュニケーション | × | × | × | × | × |
| (同上) | CC-Link | × | × | × | × | × |

| 接続局CPU: LCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード)*1 | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
| (同上) | CC IE Field*2 | ○(4) | ○(4)*3 | ○(4) | × | × | × |
| (同上) | MELSECNET/H | × | × | × | × | × | × |
| (同上) | Ethernet | × | × | × | × | × | × |
| (同上) | シリアルコミュニケーション | ○(2) | × | ○(2) | × | × | × |
| (同上) | CC-Link | ○(3) | ○(3) | ○(3) | × | × | × |

> *1 二重化CPUの場合はアクセスできません。
> *2 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
> *3 Q12DCCPU-V(基本機能モード)は，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。

※この節の表にも CC IE Control の行は無い(原本どおり)。

### プロパティ一覧 (10.16 / 408 / 原本 p.410)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 0(0x00)固定 |
| ActDestinationPortNumber | 0(0x00) | GOTのポート番号 | GOTのポート番号 | GOTのポート番号 | GOTのポート番号 |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 | 1(0x01)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 | 1(0x01)固定 |
| ActHostAddress | 1.1.1.1 | GOTのホスト名またはIPアドレス | GOTのホスト名またはIPアドレス | GOTのホスト名またはIPアドレス | GOTのホスト名またはIPアドレス |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 対象局<br>QCPU(Qモード)，<br>LCPU: 1(0x01)<br>上記以外: 0(0x00) | 対象局<br>QCPU(Qモード)，<br>QCCPU，LCPU : 1(0x01)<br>上記以外: 0(0x00) | 0(0x00)固定 |
| ActIONumber*1 | 1023(0x3FF) | 1023(0x3FF)固定 | 接続局側経由ユニットI/Oアドレス | 接続局側経由ユニットI/Oアドレス | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 | 0(0x00)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニットネットワークNo. |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_TCPIP(0x05) | PROTOCOL_TCPIP(0x05) | PROTOCOL_TCPIP(0x05) | PROTOCOL_TCPIP(0x05) |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 255(0xFF)固定 | 255(0xFF)固定 | 対象局側ユニット局番 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 | 0(0x00)固定 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_GOTETHER_LNCPU(0x57) | UNIT_GOTETHER_LNCPU(0x57) | UNIT_GOTETHER_LNCPU(0x57) | UNIT_GOTETHER_LNCPU(0x57) |

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2

## パソコン側ポート: Ethernetボード，GOT2000側ポート: Ethernetポート，CPU側ポート: バス (10.16 / 409-411 / 原本 p.411-413)

### 構成 (10.16 / 409 / 原本 p.411)

【図】構成図 (10.16 / 409 / 原本 p.411)
- パソコン ―Ethernet― GOT ―バス― 接続局CPU＋経由ユニット
- 接続局側の経由ユニット ―経由ネットワーク― 経由局CPU＋経由ユニット

### アクセス可否およびプロパティのパターン (10.16 / 409 / 原本 p.411)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: QCPU(Qモード) | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × |
| (同上) | CC IE Control<br>CC IE Field | × | × | × | × | × |
| (同上) | MELSECNET/H | × | × | × | × | × |
| (同上) | Ethernet | × | × | × | × | × |
| (同上) | シリアルコミュニケーション | × | × | × | × | × |
| (同上) | CC-Link | × | × | × | × | × |

| 接続局CPU: QCPU(Qモード) | 経由ネットワーク | 経由局CPU: QCPU(Qモード)*1 | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × | × |
| (同上) | CC IE Control<br>CC IE Field | ○(2) | ○(2)*2 | ○(2)*3 | × | × | × |
| (同上) | MELSECNET/H | ○(2) | ○(2) | × | × | × | × |
| (同上) | Ethernet | × | × | × | × | × | × |
| (同上) | シリアルコミュニケーション | ○(3) | × | ○(3) | × | × | × |
| (同上) | CC-Link | ○(4) | ○(4) | ○(4) | × | × | × |

| 接続局CPU: QCCPU | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × |
| (同上) | CC IE Control<br>CC IE Field | × | × | × | × | × |
| (同上) | MELSECNET/H | × | × | × | × | × |
| (同上) | Ethernet | × | × | × | × | × |
| (同上) | シリアルコミュニケーション | × | × | × | × | × |
| (同上) | CC-Link | × | × | × | × | × |

| 接続局CPU: QCCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード)*1 | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
| (同上) | CC IE Control<br>CC IE Field | ○(2) | ○(2)*2 | ○(2)*3 | × | × | × |
| (同上) | MELSECNET/H | ○(2) | ○(2) | × | × | × | × |
| (同上) | Ethernet | × | × | × | × | × | × |
| (同上) | シリアルコミュニケーション | × | × | × | × | × | × |
| (同上) | CC-Link | ○(4) | ○(4) | ○(4) | × | × | × |

※原本では4つ目の表(接続局QCCPU，経由局QCPU〜FXCPU)がp.412にある。

> *1 二重化CPUの場合はアクセスできません。
> *2 Q12DCCPU-V(基本機能モード)は，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。
> *3 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。

### プロパティ一覧 (10.16 / 411 / 原本 p.413)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ | 対象局に該当するCPUタイプ |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) |
| ActDestinationPortNumber | 0(0x00) | GOTのポート番号 | GOTのポート番号 | GOTのポート番号 | GOTのポート番号 |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActHostAddress | 1.1.1.1 | GOTのホスト名またはIPアドレス | GOTのホスト名またはIPアドレス | GOTのホスト名またはIPアドレス | GOTのホスト名またはIPアドレス |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局<br>QCPU(Qモード)，<br>LCPU: 1(0x01)<br>上記以外: 0(0x00) | 対象局<br>QCPU(Qモード)，<br>QCCPU，LCPU: 1(0x01)<br>上記以外: 0(0x00) |
| ActIONumber*1 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 接続局側ユニットI/Oアドレス | 接続局側ユニットI/Oアドレス |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニットネットワークNo. | 0(0x00)固定 | 0(0x00)固定 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_TCPIP(0x05) | PROTOCOL_TCPIP(0x05) | PROTOCOL_TCPIP(0x05) | PROTOCOL_TCPIP(0x05) |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 対象局側ユニット局番 | 255(0xFF)固定 | 255(0xFF)固定 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_GOTETHER_QBUS(0x58) | UNIT_GOTETHER_QBUS(0x58) | UNIT_GOTETHER_QBUS(0x58) | UNIT_GOTETHER_QBUS(0x58) |

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2

## パソコン側ポート: Ethernetボード，GOT2000/3000ポート: Ethernetポート，CPU側ポート: Ethernetポート (10.16 / 412-413 / 原本 p.414-415)

### 構成 (10.16 / 412 / 原本 p.414)

【図】構成図 (10.16 / 412 / 原本 p.414)
- パソコン ―Ethernet― GOT ―Ethernet― 接続局CPU＋経由ユニット
- 接続局側の経由ユニット ―経由ネットワーク― 経由局CPU＋経由ユニット

### アクセス可否およびプロパティのパターン (10.16 / 412 / 原本 p.414)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: QCPU(Qモード) | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × |
| (同上) | CC IE Control<br>CC IE Field | × | × | × | × | × |
| (同上) | MELSECNET/H | × | × | × | × | × |
| (同上) | Ethernet | × | × | × | × | × |
| (同上) | シリアルコミュニケーション | × | × | × | × | × |
| (同上) | CC-Link | × | × | × | × | × |

| 接続局CPU: QCPU(Qモード) | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × | × |
| (同上) | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
| (同上) | MELSECNET/H | × | × | × | × | × | × |
| (同上) | Ethernet | × | × | × | × | × | × |
| (同上) | シリアルコミュニケーション | × | × | × | × | × | × |
| (同上) | CC-Link | × | × | × | × | × | × |

> *1 Qn(U)(J)(P)(D)(E)(V)(H)の場合のみ動作します。QnPRHCPUは，未サポートのためアクセスできません。

### プロパティ一覧 (10.16 / 413 / 原本 p.415)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) |
|---|---|---|
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 |
| ActConnectUnitNumber | 0(0x00) | 0(0x00)固定 |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 |
| ActCpuTimeOut | 0(0x00) | 0(0x00)固定 |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 |
| ActDestinationPortNumber*1 | 0(0x00) | GOTのポート番号 |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 |
| ActHostAddress | 1.1.1.1 | GOTのホスト名またはIPアドレス |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 |
| ActIONumber*2 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) |
| ActMultiDropChannelNumber*3 | 0(0x00) | 0(0x00)固定 |
| ActNetworkNumber*4 | 0(0x00) | 0(0x00)固定 |
| ActPacketType | 0x01(PACKET_PLC1) | PACKET_PLC1 |
| ActParity | 1(ODD_PARITY) | 0(0x00)固定 |
| ActPortNumber | 1(PORT_1) | 0(0x00)固定 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_TCPIP(0x05)/PROTOCOL_UDPIP(0x08) |
| ActStopBits | 0(STOPBIT_ONE) | 0(0x00)固定 |
| ActSumCheck | 0(NO_SUM_CHECK) | 0(0x00)固定 |
| ActSourceNetworkNumber*5 | 0(0x00) | 0(0x00)固定 |
| ActSourceStationNumber*6 | 0(0x00) | 0(0x00)固定 |
| ActStationNumber*4 | 255(0xFF) | 255(0xFF)固定 |
| ActThroughNetworkType | 0(0x00) | 1(0x01)固定 |
| ActTimeOut | 10000 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_GOTETHER_QN_ETHER(0x6F) |

> *1 GOT側で設定した値を指定してください。
> *2 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *3 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2
> *4 対象局側のパラメータ設定で設定した値を指定してください。
> *5 接続局がEthernetポート，拡張設定(ネットワークNo.局番設定)ありの場合は，Ethernetポートに設定したネットワークNo.と同一のネットワークNo.を指定してください。
> 接続局がEthernetポート，拡張設定(ネットワークNo.局番設定)なしの場合は，GOTのEthernet設定で設定している接続局のネットワークNo.と同一のネットワークNo.を指定してください。ただし自局宛て設定(1NetworkNumber: 0x00,1StationNumber:0xFF)の場合は，1NetworkNumberと同じ0x00を設定してください。
> *6 Ethernetの同一ネットワーク内でQJ71E71に設定した局番と重複しないようパソコン側の局番を指定してください。

※要確認: この節(接続局はCPU内蔵Ethernetポート)の脚注*6も「QJ71E71に設定した局番」と記載(原本どおり)。また値が「0(0x00)固定」の ActNetworkNumber / ActStationNumber / ActSourceNetworkNumber / ActSourceStationNumber に「設定した値を指定」とする脚注*4〜*6が付いている(原本どおり)。

## パソコン側ポート: Ethernetボード，GOT2000/3000ポート: Ethernet ポート，CPU側ポート: Qシリーズ対応E71 (10.16 / 414-415 / 原本 p.416-417)

### 構成 (10.16 / 414 / 原本 p.416)

【図】構成図 (10.16 / 414 / 原本 p.416)
- パソコン ―Ethernet― GOT ―Ethernet― 接続局CPU＋Qシリーズ対応E71＋経由ユニット
- 接続局側の経由ユニット ―経由ネットワーク― 経由局CPU＋経由ユニット

### アクセス可否およびプロパティのパターン (10.16 / 414 / 原本 p.416)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 接続局CPU: QCPU(Qモード) | 経由ネットワーク | 経由局CPU: RCPU | 経由局CPU: RCCPU | 経由局CPU: RモーションCPU | 経由局CPU: LHCPU | 経由局CPU: FX5CPU |
|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × |
| (同上) | CC IE Control<br>CC IE Field | × | × | × | × | × |
| (同上) | MELSECNET/H | × | × | × | × | × |
| (同上) | Ethernet | × | × | × | × | × |
| (同上) | シリアルコミュニケーション | × | × | × | × | × |
| (同上) | CC-Link | × | × | × | × | × |

| 接続局CPU: QCPU(Qモード) | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | 経由局CPU: QCCPU | 経由局CPU: LCPU | 経由局CPU: QSCPU | 経由局CPU: QモーションCPU | 経由局CPU: FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1)*1 | CC IE TSN | × | × | × | × | × | × |
| (同上) | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
| (同上) | MELSECNET/H | × | × | × | × | × | × |
| (同上) | Ethernet | × | × | × | × | × | × |
| (同上) | シリアルコミュニケーション | × | × | × | × | × | × |
| (同上) | CC-Link | × | × | × | × | × | × |

> *1 Qn(U)(J)(P)(D)(E)(V)(H)の場合のみ動作します。QnPRHCPUは，未サポートのためアクセスできません。

### プロパティ一覧 (10.16 / 415 / 原本 p.417)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) |
|---|---|---|
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00)固定 |
| ActConnectUnitNumber | 0(0x00) | 0(0x00)固定 |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00)固定 |
| ActCpuTimeOut | 0(0x00) | 0(0x00)固定 |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ |
| ActDataBits | 8(DATABIT_8) | 0(0x00)固定 |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 |
| ActDestinationPortNumber*1 | 0(0x00) | GOTのポート番号 |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 |
| ActHostAddress | 1.1.1.1 | GOTのホスト名またはIPアドレス |
| ActIntelligentPreferenceBit | 0(0x00) | 0(0x00)固定 |
| ActIONumber*2 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) |
| ActMultiDropChannelNumber*3 | 0(0x00) | 0(0x00)固定 |
| ActNetworkNumber*4 | 0(0x00) | 対象局側ユニットネットワークNo. |
| ActPacketType | 0x01(PACKET_PLC1) | PACKET_PLC1 |
| ActParity | 1(ODD_PARITY) | 0(0x00)固定 |
| ActPortNumber | 1(PORT_1) | 0(0x00)固定 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_TCPIP(0x05)/PROTOCOL_UDPIP(0x08) |
| ActStopBits | 0(STOPBIT_ONE) | 0(0x00)固定 |
| ActSumCheck | 0(NO_SUM_CHECK) | 0(0x00)固定 |
| ActSourceNetworkNumber*5 | 0(0x00) | GOT側ネットワークNo. |
| ActSourceStationNumber*6 | 0(0x00) | GOT側局番 |
| ActStationNumber*4 | 255(0xFF) | 対象局側ユニット局番 |
| ActThroughNetworkType | 0(0x00) | 1(0x01)固定 |
| ActTimeOut | 10000 | ms単位でユーザ任意 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_GOTETHER_QN_ETHER(0x6F) |

> *1 GOT側で設定した値を指定してください。
> *2 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *3 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2
> *4 対象局側のパラメータ設定で設定した値を指定してください。
> *5 QJ71E71のパラメータ設定でQJ71E71に設定したネットワークNo.と同一のネットワークNo.を指定してください。
> *6 Ethernetの同一ネットワーク内でQJ71E71に設定した局番と重複しないようパソコン側の局番を指定してください。

