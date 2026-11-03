# MX Component Version 5 リファレンスマニュアル 10章 各通信経路で設定するプロパティ (6/9) p.317-339

| 項目 | 内容 |
|---|---|
| 原本 | 【三菱】MX Component Version 5 リファレンスマニュアル (SH-082394J) |
| メーカー | 三菱電機 |
| 原本ファイル | `PDF/【三菱】MX Component Version 5 リファレンスマニュアル_sh082394j.pdf` (全696ページ) |
| 本ファイルの範囲 | 10.6 CC-Link IEコントローラネットワーク通信 〜 10.15 GOTゲートウェイデバイス通信 (印刷ページ 315-337 / PDF p.317-339) |
| 出典表記 | `(節 / 印刷ページ / 原本 p.PDFページ)` |
| 作成日 | 2026-11-03 |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。
> 本文中の「○ページ」はすべて原本の**印刷ページ番号**です(PDFページ = 印刷ページ + 2)。
> アクセス可否表の記号: ○(n) = アクセス可能(nはプロパティのパターン)，× = アクセス不可(原本凡例どおり)。原本で縦に結合されたセル(自ボード・接続局CPU)は，表の1行目にだけ値を書き，2行目以降は「〃」とした。

## 主要用語 対訳表 (Glossary)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| 自ボード | Own board | — | 参考訳 |
| 接続局CPU | Connected station CPU | — | 参考訳 |
| 経由ネットワーク | Relayed network | — | 参考訳 |
| 経由局CPU | Relayed station CPU | — | 参考訳 |
| 経由ユニット | Relayed module | — | 参考訳 |
| アクセス可否およびプロパティのパターン | Accessibility and property pattern | ○(n) / × | 参考訳 |
| プロパティのパターン | Property pattern | (1)〜(n) | 参考訳 |
| 対象局 / 接続局 | Target station / Connected station | — | 参考訳 |
| シングルCPU / マルチCPU / 二重化CPU | Single CPU / Multiple CPU / Redundant CPU | — | 参考訳 |
| 接続号機 / 1号機〜4号機 | Connected CPU / CPU No.1〜No.4 | 1023(0x3FF) / 992〜995(0x3E0〜0x3E3) | 参考訳 |
| 制御系 | Control system | 976(0x3D0) | 参考訳 |
| I/Oアドレス(I/O先頭No.を16で割った値) | I/O address (start I/O number ÷16) | ActIONumber | 参考訳 |
| マルチドロップチャネルNo. | Multidrop channel number | ActMultiDropChannelNumber | 参考訳 |
| ユニットネットワークNo. | Module network number | ActNetworkNumber | 参考訳 |
| ユニット局番 | Module station number | ActStationNumber / ActUnitNumber | 参考訳 |
| ボードのポート番号 | Board port number | ActPortNumber (PORT1〜PORT4) | 参考訳 |
| CC-Link IEコントローラネットワーク | CC-Link IE Controller Network | CC IE Control / PROTOCOL_MNETG(0x14) / UNIT_MNETGBOARD(0x2B) | 原本併記 |
| CC-Link IEフィールドネットワーク | CC-Link IE Field Network | CC IE Field / PROTOCOL_CCIEF(0x15) / UNIT_CCIEFBOARD(0x2F) | 原本併記 |
| CC-Link IE TSN | CC-Link IE TSN | CC IE TSN | 原本併記 |
| MELSECNET/H | MELSECNET/H | — | 原本併記 |
| MELSECNET/10を含む | Including MELSECNET/10 | ActThroughNetworkType | 参考訳 |
| マスタ局 / ローカル局 | Master station / Local station | CC-Link | 参考訳 |
| シミュレータ | Simulator | GX Simulator2 / GX Simulator3 / MT Simulator2 | 参考訳 |
| ゲートウェイデバイス | Gateway device | GOT | 参考訳 |

## 変換範囲表

| 原本ページ(PDF) | 印刷ページ | 節 | 扱い |
|---|---|---|---|
| p.317-321 | 315-319 | 10.6 CC-Link IEコントローラネットワーク通信 | 全文 |
| p.322-325 | 320-323 | 10.7 CC-Link IEフィールドネットワーク通信 | 全文 |
| p.326-327 | 324-325 | 10.8 CC-Link IE TSN通信 | 全文 |
| p.328-333 | 326-331 | 10.9 CC-Link通信 | 全文 |
| p.334-336 | 332-334 | 10.10 CC-Linkシステム RS-232インタフェース通信 | 全文 |
| p.337-338 | 335-336 | 10.11 GX Simulator2通信 / 10.12 GX Simulator3通信 / 10.13 MT Simulator2通信 / 10.14 MELSOFT Mirror通信 | 全文 |
| p.339 | 337 | 10.15 GOTゲートウェイデバイス通信 | 全文 |
| p.192-316 | 190-314 | 10.1〜10.5 | 別ファイル(10-1〜10-5) |
| p.340-417 | 338-415 | 10.16 GOTトランスペアレント通信 | 別ファイル(10-7〜10-9) |
| 上記以外 | — | 1〜9章，11章以降 | 別ファイル(01_〜09_)または**未変換** |

## 目次

- 10.6 CC-Link IEコントローラネットワーク通信
  - 接続局がRCPUのCC-Link IEコントローラネットワーク通信
  - 接続局がQシリーズのCC-Link IEコントローラネットワーク通信
- 10.7 CC-Link IEフィールドネットワーク通信
  - 接続局がRCPUのCC-Link IEフィールドネットワーク通信
  - 接続局がQCPU(Qモード)またはLCPUのCC-Link IEフィールドネットワーク通信
- 10.8 CC-Link IE TSN通信
  - 接続局がRCPUのCC-Link IE TSN通信
- 10.9 CC-Link通信
  - 接続局がRCPUのCC-Link通信 / 接続局がLCPUのCC-Link通信 / 接続局がQシリーズのCC-Link通信
- 10.10 CC-Linkシステム RS-232インタフェース通信
- 10.11 GX Simulator2通信 / 10.12 GX Simulator3通信 / 10.13 MT Simulator2通信 / 10.14 MELSOFT Mirror通信
- 10.15 GOTゲートウェイデバイス通信

---

## 10.6 CC-Link IEコントローラネットワーク通信 (10.6 / 315-319 / 原本 p.317-321)

### 接続局がRCPUのCC-Link IEコントローラネットワーク通信 (10.6 / 315-316 / 原本 p.317-318)

#### 構成 (10.6 / 315 / 原本 p.317)

【図】構成 (10.6 / 315 / 原本 p.317)
- パソコン ―(CC-Link IE コントローラネットワーク)― 接続局CPU の CC-Link IE コントローラネットワークユニット
- 接続局CPU の経由ユニット ―(経由ネットワーク)― 経由局CPU の経由ユニット

#### アクセス可否およびプロパティのパターン (10.6 / 315 / 原本 p.317)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 自ボード | 接続局CPU: RCPU | 経由ネットワーク | 経由局CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|---|
| × | ○(2) | CC IE TSN | ○(2) | × | × | × | × |
| 〃 | 〃 | CC IE Control<br>CC IE Field | ○(2) | × | × | × | × |
| 〃 | 〃 | MELSECNET/H | × | × | × | × | × |
| 〃 | 〃 | Ethernet | ○(2) | × | × | × | × |
| 〃 | 〃 | シリアルコミュニケーション | ○(3)*1 | × | × | × | × |
| 〃 | 〃 | CC-Link | ○(4) | × | × | × | × |

| 自ボード | 接続局CPU: RCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU*2 | FXCPU |
|---|---|---|---|---|---|---|---|---|
| × | ○(2) | CC IE TSN | × | × | × | × | × | × |
| 〃 | 〃 | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
| 〃 | 〃 | MELSECNET/H | × | × | × | × | × | × |
| 〃 | 〃 | Ethernet | × | × | × | × | × | × |
| 〃 | 〃 | シリアルコミュニケーション | ○(3)*1 | × | ○(3)*1 | × | × | × |
| 〃 | 〃 | CC-Link | ○(4) | × | ○(4) | × | × | × |

> *1 二重化CPUの場合，マルチドロップ接続ができないため，基本ベースユニット上にあるシリアルコミュニケーションユニットにはアクセスできません。
> *2 マルチCPU構成時の，2号機以降の場合のみアクセス可能です。

#### プロパティ一覧 (10.6 / 316 / 原本 p.318)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | (同左) | (同左) | (同左) |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 指定なし: 1023(0x3FF) |
| ActDidPropertyBit | 1(0x01) | 0(0x00)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 0(0x00)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActIONumber*1 | 1023(0x3FF) | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 接続局側経由ユニットI/Oアドレス | 接続局側経由ユニットI/Oアドレス |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニットネットワークNo. | 接続局側ユニットネットワークNo. | 接続局側ユニットネットワークNo. |
| ActPortNumber | 1(PORT_1) | パソコン側CC-Link IEコントローラネットワークボードのポート番号，PORT1～PORT4(1枚目～4枚目) | (同左) | (同左) | (同左) |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_MNETG(0x14) | (同左) | (同左) | (同左) |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 対象局側ユニット局番 | 接続局側ユニット局番 | 接続局側ユニット局番 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | (同左) | (同左) | (同左) |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_MNETGBOARD(0x2B) | (同左) | (同左) | (同左) |

※「(同左)」は原本で(1)〜(4)の4列が結合された1セルであることを示す。原本の表記はプロパティ名「ActMultiDropChannelNumb er」(セル内改行)。

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2

### 接続局がQシリーズのCC-Link IEコントローラネットワーク通信 (10.6 / 317-319 / 原本 p.319-321)

#### 構成 (10.6 / 317 / 原本 p.319)

【図】構成 (10.6 / 317 / 原本 p.319)
- パソコン ―(CC-Link IE コントローラネットワーク)― 接続局CPU の CC-Link IE コントローラネットワークユニット
- 接続局CPU の経由ユニット ―(経由ネットワーク)― 経由局CPU の経由ユニット

#### アクセス可否およびプロパティのパターン (10.6 / 317-318 / 原本 p.319-320)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 自ボード | 接続局CPU: QCPU(Qモード) | QSCPU | QモーションCPU | 経由ネットワーク | 経由局CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|---|---|---|
| ○(1) | ○(2) | ○(2)*1*5 | ○(2)*1*5 | CC IE TSN | × | × | × | × | × |
| 〃 | 〃 | 〃 | 〃 | CC IE Control<br>CC IE Field | × | × | × | × | × |
| 〃 | 〃 | 〃 | 〃 | MELSECNET/H | × | × | × | × | × |
| 〃 | 〃 | 〃 | 〃 | Ethernet | × | × | × | × | × |
| 〃 | 〃 | 〃 | 〃 | シリアルコミュニケーション | × | × | × | × | × |
| 〃 | 〃 | 〃 | 〃 | CC-Link | × | × | × | × | × |

| 自ボード | 接続局CPU: QCPU(Qモード) | QSCPU | QモーションCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU*5 | FXCPU |
|---|---|---|---|---|---|---|---|---|---|---|
| ○(1) | ○(2) | ○(2)*1*5 | ○(2)*1*5 | CC IE TSN | × | × | × | × | × | × |
| 〃 | 〃 | 〃 | 〃 | CC IE Control<br>CC IE Field | ○(2) | ○(2)*2 | ○(2)*3 | ○(2)*1*2 | × | × |
| 〃 | 〃 | 〃 | 〃 | MELSECNET/H | ○(2) | ○(2) | × | ○(2)*1 | × | × |
| 〃 | 〃 | 〃 | 〃 | Ethernet | ○(2) | × | × | ○(2)*1 | × | × |
| 〃 | 〃 | 〃 | 〃 | シリアルコミュニケーション | ○(3)*4 | × | ○(3) | × | ○(3) | × |
| 〃 | 〃 | 〃 | 〃 | CC-Link | ○(4) | ○(4) | ○(4) | × | ○(4) | × |

| 自ボード | 接続局CPU: QCCPU | 経由ネットワーク | 経由局CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|---|
| ○(1) | ○(2)*6 | CC IE TSN | × | × | × | × | × |
| 〃 | 〃 | CC IE Control<br>CC IE Field | × | × | × | × | × |
| 〃 | 〃 | MELSECNET/H | × | × | × | × | × |
| 〃 | 〃 | Ethernet | × | × | × | × | × |
| 〃 | 〃 | シリアルコミュニケーション | × | × | × | × | × |
| 〃 | 〃 | CC-Link | × | × | × | × | × |

| 自ボード | 接続局CPU: QCCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU*5 | FXCPU |
|---|---|---|---|---|---|---|---|---|
| ○(1) | ○(2)*6 | CC IE TSN | × | × | × | × | × | × |
| 〃 | 〃 | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
| 〃 | 〃 | MELSECNET/H | × | × | × | × | × | × |
| 〃 | 〃 | Ethernet | × | × | × | × | × | × |
| 〃 | 〃 | シリアルコミュニケーション | × | × | × | × | × | × |
| 〃 | 〃 | CC-Link | ○(4) | ○(4) | ○(4) | × | ○(4) | × |

> *1 QSCPUおよびQモーションCPUを経由して経由局CPUにアクセスできません。
> *2 Q12DCCPU-V(基本機能モード)，QSCPUは，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。
> *3 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
> *4 二重化CPUの場合，基本ベースユニット上にあるシリアルコミュニケーションユニットにはアクセスできません。
> *5 マルチCPU構成時の，2号機以降の場合のみアクセス可能です。
> *6 Q24DHCCPU-V，Q24DHCCPU-LS，Q24DHCCPU-VG，Q26DHCCPU-LSは，通信経路が未サポートのためアクセスできません。

#### プロパティ一覧 (10.6 / 319 / 原本 p.321)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | (同左) | (同左) | (同左) |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) |
| ActDidPropertyBit | 1(0x01) | 0(0x00)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 0(0x00)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActIONumber*1 | 1023(0x3FF) | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 接続局側経由ユニットI/Oアドレス | 接続局側経由ユニットI/Oアドレス |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニットネットワークNo. | 接続局側ユニットネットワークNo. | 接続局側ユニットネットワークNo. |
| ActPortNumber | 1(PORT_1) | パソコン側CC-Link IEコントローラネットワークボードのポート番号，PORT1～PORT4(1枚目～4枚目) | (同左) | (同左) | (同左) |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_MNETG(0x14) | (同左) | (同左) | (同左) |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 対象局側ユニット局番 | 接続局側ユニット局番 | 接続局側ユニット局番 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | (同左) | (同左) | (同左) |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_MNETGBOARD(0x2B) | (同左) | (同左) | (同左) |

※「(同左)」は原本で(1)〜(4)の4列が結合された1セル。p.316(接続局RCPU)の表との違いは ActDestinationIONumber のパターン(3)にも「■二重化CPU時」がある点と，(4)の二重化CPU時に「制御系: 976(0x3D0)」がある点(原本どおり)。

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2

---

## 10.7 CC-Link IEフィールドネットワーク通信 (10.7 / 320-323 / 原本 p.322-325)

### 接続局がRCPUのCC-Link IEフィールドネットワーク通信 (10.7 / 320-321 / 原本 p.322-323)

#### 構成 (10.7 / 320 / 原本 p.322)

【図】構成 (10.7 / 320 / 原本 p.322)
- パソコン ―(CC-Link IEフィールドネットワーク)― 接続局CPU の CC-Link IEフィールドネットワークユニット
- 接続局CPU の経由ユニット ―(経由ネットワーク)― 経由局CPU の経由ユニット

#### アクセス可否およびプロパティのパターン (10.7 / 320 / 原本 p.322)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 自ボード | 接続局CPU: RCPU | 経由ネットワーク | 経由局CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|---|
| × | ○(1) | CC IE TSN | ○(1) | × | × | × | × |
| 〃 | 〃 | CC IE Field | ○(1) | × | × | × | × |
| 〃 | 〃 | MELSECNET/H | × | × | × | × | × |
| 〃 | 〃 | Ethernet | ○(1) | × | × | × | × |
| 〃 | 〃 | シリアルコミュニケーション | ○(2)*1 | × | × | × | × |
| 〃 | 〃 | CC-Link | ○(3) | × | × | × | × |

| 自ボード | 接続局CPU: RCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|---|
| × | ○(1) | CC IE TSN | × | × | × | × | × | × |
| 〃 | 〃 | CC IE Field | × | × | × | × | × | × |
| 〃 | 〃 | MELSECNET/H | × | × | × | × | × | × |
| 〃 | 〃 | Ethernet | × | × | × | × | × | × |
| 〃 | 〃 | シリアルコミュニケーション | ○(2)*1 | × | ○(2)*1 | × | × | × |
| 〃 | 〃 | CC-Link | ○(3) | × | ○(3) | × | × | × |

> *1 二重化CPUの場合，マルチドロップ接続ができないため，基本ベースユニット上にあるシリアルコミュニケーションユニットにはアクセスできません。

#### プロパティ一覧 (10.7 / 321 / 原本 p.323)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) |
|---|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | (同左) | (同左) |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 指定なし: 1023(0x3FF) |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActIONumber*1 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 指定なし: 1023(0x3FF) | 接続局側経由ユニットI/Oアドレス | 接続局側経由ユニットI/Oアドレス |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber | 0(0x00) | 対象局側ユニットネットワークNo. | 接続局側ユニットネットワークNo. | 接続局側ユニットネットワークNo. |
| ActPortNumber | 1(PORT_1) | パソコン側CC-Link IEフィールドネットワークボードのポート番号，PORT1～PORT4(1枚目～4枚目) | (同左) | (同左) |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_CCIEF(0x15) | (同左) | (同左) |
| ActStationNumber | 255(0xFF) | 対象局側ユニット局番 | 接続局側ユニット局番 | 接続局側ユニット局番 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | (同左) | (同左) |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_CCIEFBOARD(0x2F) | (同左) | (同左) |

※「(同左)」は原本で(1)〜(3)の3列が結合された1セル。

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2

### 接続局がQCPU(Qモード)またはLCPUのCC-Link IEフィールドネットワーク通信 (10.7 / 322-323 / 原本 p.324-325)

#### 構成 (10.7 / 322 / 原本 p.324)

【図】構成 (10.7 / 322 / 原本 p.324)
- パソコン ―(CC-Link IEフィールドネットワーク)― 接続局CPU の CC-Link IEフィールドネットワークユニット
- 接続局CPU の経由ユニット ―(経由ネットワーク)― 経由局CPU の経由ユニット

#### アクセス可否およびプロパティのパターン (10.7 / 322-323 / 原本 p.324-325)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 自ボード | 接続局CPU: QCPU(Qモード) | 経由ネットワーク | 経由局CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|---|
| ○(1) | ○(2) | CC IE TSN | × | × | × | × | × |
| 〃 | 〃 | CC IE Control<br>CC IE Field | × | × | × | × | × |
| 〃 | 〃 | MELSECNET/H | × | × | × | × | × |
| 〃 | 〃 | Ethernet | × | × | × | × | × |
| 〃 | 〃 | シリアルコミュニケーション | × | × | × | × | × |
| 〃 | 〃 | CC-Link | × | × | × | × | × |

| 自ボード | 接続局CPU: QCPU(Qモード) | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|---|
| ○(1) | ○(2) | CC IE TSN | × | × | × | × | × | × |
| 〃 | 〃 | CC IE Control<br>CC IE Field | ○(2) | ○(2)*1 | ○(2)*2 | × | × | × |
| 〃 | 〃 | MELSECNET/H | ○(2) | ○(2) | × | × | × | × |
| 〃 | 〃 | Ethernet | ○(2) | × | × | × | × | × |
| 〃 | 〃 | シリアルコミュニケーション | ○(3) | × | ○(3) | × | × | × |
| 〃 | 〃 | CC-Link | ○(4) | ○(4) | ○(4) | × | × | × |

| 自ボード | 接続局CPU: LCPU | 経由ネットワーク | 経由局CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|---|
| ○(1) | ○(2) | CC IE TSN | × | × | × | × | × |
| 〃 | 〃 | CC IE Field*2 | × | × | × | × | × |
| 〃 | 〃 | MELSECNET/H | × | × | × | × | × |
| 〃 | 〃 | Ethernet | × | × | × | × | × |
| 〃 | 〃 | シリアルコミュニケーション | × | × | × | × | × |
| 〃 | 〃 | CC-Link | × | × | × | × | × |

| 自ボード | 接続局CPU: LCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|---|
| ○(1) | ○(2) | CC IE TSN | × | × | × | × | × | × |
| 〃 | 〃 | CC IE Field*2 | ○(2) | × | ○(2) | × | × | × |
| 〃 | 〃 | MELSECNET/H | × | × | × | × | × | × |
| 〃 | 〃 | Ethernet | × | × | × | × | × | × |
| 〃 | 〃 | シリアルコミュニケーション | ○(3) | × | ○(3) | × | × | × |
| 〃 | 〃 | CC-Link | ○(4) | ○(4) | ○(4) | × | × | × |

> *1 Q12DCCPU-V(基本機能モード)は，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。
> *2 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。

#### プロパティ一覧 (10.7 / 323 / 原本 p.325)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) | ○(4) |
|---|---|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | (同左) | (同左) | (同左) |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 | 0(0x00)固定 | 0(0x00)固定 |
| ActIONumber*1 | 1023(0x3FF) | 1023(0x3FF)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3) | 接続局側経由ユニットI/Oアドレス | 接続局側経由ユニットI/Oアドレス |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | マルチドロップチャネルNo. | 0(0x00)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニットネットワークNo. | 接続局側ユニットネットワークNo. | 接続局側ユニットネットワークNo. |
| ActPortNumber | 1(PORT_1) | パソコン側CC-Link IEフィールドネットワークボードのポート番号，PORT1～PORT4(1枚目～4枚目) | (同左) | (同左) | (同左) |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_CCIEF(0x15) | (同左) | (同左) | (同左) |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 対象局側ユニット局番 | 接続局側ユニット局番 | 接続局側ユニット局番 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | (同左) | (同左) | (同左) |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_CCIEFBOARD(0x2F) | (同左) | (同左) | (同左) |

※「(同左)」は原本で(1)〜(4)の4列が結合された1セル。

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2

---

## 10.8 CC-Link IE TSN通信 (10.8 / 324-325 / 原本 p.326-327)

### 接続局がRCPUのCC-Link IE TSN通信 (10.8 / 324-325 / 原本 p.326-327)

#### 構成 (10.8 / 324 / 原本 p.326)

【図】構成 (10.8 / 324 / 原本 p.326)
- パソコン ―(CC-Link IE TSN)― 接続局CPU の CC-Link IE TSNユニット
- 接続局CPU の経由ユニット ―(経由ネットワーク)― 経由局CPU の経由ユニット

#### アクセス可否およびプロパティのパターン (10.8 / 324 / 原本 p.326)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 自ボード | 接続局CPU: RCPU | 経由ネットワーク | 経由局CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|---|
| ○(1) | ○(2) | CC IE TSN | ○(2) | × | × | × | × |
| 〃 | 〃 | CC IE Control<br>CC IE Field | ○(2) | × | × | × | × |
| 〃 | 〃 | MELSECNET/H | × | × | × | × | × |
| 〃 | 〃 | Ethernet | ○(2) | × | × | × | × |
| 〃 | 〃 | シリアルコミュニケーション | × | × | × | × | × |
| 〃 | 〃 | CC-Link | × | × | × | × | × |

| 自ボード | 接続局CPU: RCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|---|
| ○(1) | ○(2) | CC IE TSN | × | × | × | × | × | × |
| 〃 | 〃 | CC IE Control<br>CC IE Field | ○(2) | × | ○(2)*1 | × | × | × |
| 〃 | 〃 | MELSECNET/H | × | × | × | × | × | × |
| 〃 | 〃 | Ethernet | × | × | × | × | × | × |
| 〃 | 〃 | シリアルコミュニケーション | × | × | × | × | × | × |
| 〃 | 〃 | CC-Link | × | × | × | × | × | × |

> *1 CC-Link IEフィールドネットワークのみアクセス可能です。

#### プロパティ一覧 (10.8 / 325 / 原本 p.327)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) |
|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | (同左) |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 |
| ActDidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 |
| ActDsidPropertyBit | 1(0x01) | 1(0x01)固定 | 1(0x01)固定 |
| ActIONumber*1 | 1023(0x3FF) | 1023(0x3FF)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 指定なし: 1023(0x3FF) |
| ActMultiDropChannelNumber*2 | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニットネットワークNo. |
| ActPortNumber | 1(PORT_1) | パソコン側CC-Link IE TSNボードのポート番号，PORT1～PORT4(1枚目～4枚目) | (同左) |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_CCIETSN | (同左) |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 対象局側ユニット局番 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | (同左) |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_CCIETSNBOARD | (同左) |

※「(同左)」は原本で(1)(2)の2列が結合された1セル。PROTOCOL_CCIETSN / UNIT_CCIETSNBOARD には，他節と違って括弧書きの値が無い(原本どおり)。

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。
> *2 マルチドロップリンクするチャネルNo.は下記を指定してください。
> 0: ユニットのデフォルトチャネルを使用
> 1: チャネル1
> 2: チャネル2

---

## 10.9 CC-Link通信 (10.9 / 326-331 / 原本 p.328-333)

### 接続局がRCPUのCC-Link通信 (10.9 / 326-327 / 原本 p.328-329)

#### 構成 (10.9 / 326 / 原本 p.328)

【図】構成 (10.9 / 326 / 原本 p.328)
- パソコン ―(線で直接)― 接続局CPU の CC-Link ユニット(図ではネットワーク名の表示なし)
- 接続局CPU の経由ユニット ―(経由ネットワーク)― 経由局CPU の経由ユニット

#### アクセス可否およびプロパティのパターン (10.9 / 326 / 原本 p.328)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 自ボード | 接続局CPU: RCPU | 経由ネットワーク | 経由局CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|---|
| × | ○(1) | CC IE TSN | ○(2) | × | × | × | × |
| 〃 | 〃 | CC IE Control<br>CC IE Field | ○(2) | × | × | × | × |
| 〃 | 〃 | MELSECNET/H | × | × | × | × | × |
| 〃 | 〃 | Ethernet | ○(2) | × | × | × | × |
| 〃 | 〃 | シリアルコミュニケーション | × | × | × | × | × |
| 〃 | 〃 | CC-Link | × | × | × | × | × |

| 自ボード | 接続局CPU: RCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|---|
| × | ○(1) | CC IE TSN | × | × | × | × | × | × |
| 〃 | 〃 | CC IE Control<br>CC IE Field | ○(2) | × | ○(2)*1 | × | × | × |
| 〃 | 〃 | MELSECNET/H | × | × | × | × | × | × |
| 〃 | 〃 | Ethernet | ○(2) | × | ○(2) | × | × | × |
| 〃 | 〃 | シリアルコミュニケーション | × | × | × | × | × | × |
| 〃 | 〃 | CC-Link | × | × | × | × | × | × |

> *1 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。

#### プロパティ一覧 (10.9 / 327 / 原本 p.329)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) |
|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | (同左) |
| ActDestinationIONumber | 0(0x00) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 指定なし: 1023(0x3FF) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 指定なし: 1023(0x3FF) |
| ActIONumber | 1023(0x3FF) | 1023(0x3FF)固定 | 1023(0x3FF)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニットネットワークNo. |
| ActPortNumber | 1(PORT_1) | パソコン側CC-Link Ver.2ボードのポート番号，PORT1～PORT4(1枚目～4枚目) | (同左) |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_CCLINK(0x07) | (同左) |
| ActStationNumber | 255(0xFF) | 対象局側CC-Linkユニット局番 | 対象局側ユニット局番 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 接続局側CC-Linkユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_CCLINKBOARD(0x0C) | (同左) |

※「(同左)」は原本で2列が結合された1セル。(2)の「接続号機: 1023(0x3FF)」に行頭の「•」が無いのは原本どおり。

### 接続局がLCPUのCC-Link通信 (10.9 / 328 / 原本 p.330)

#### 構成 (10.9 / 328 / 原本 p.330)

【図】構成 (10.9 / 328 / 原本 p.330)
- パソコン ―(線で直接)― 接続局CPU の CC-Link ユニット
- 接続局CPU の経由ユニット ―(経由ネットワーク)― 経由局CPU の経由ユニット

#### アクセス可否およびプロパティのパターン (10.9 / 328 / 原本 p.330)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 自ボード | 接続局CPU: LCPU | 経由ネットワーク | 経由局CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|---|
| ○(1) | ○(2) | CC IE TSN | × | × | × | × | × |
| 〃 | 〃 | CC IE Control<br>CC IE Field | × | × | × | × | × |
| 〃 | 〃 | MELSECNET/H | × | × | × | × | × |
| 〃 | 〃 | Ethernet | × | × | × | × | × |
| 〃 | 〃 | シリアルコミュニケーション | × | × | × | × | × |
| 〃 | 〃 | CC-Link | × | × | × | × | × |

| 自ボード | 接続局CPU: LCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|---|
| ○(1) | ○(2) | CC IE TSN | × | × | × | × | × | × |
| 〃 | 〃 | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
| 〃 | 〃 | MELSECNET/H | × | × | × | × | × | × |
| 〃 | 〃 | Ethernet | × | × | × | × | × | × |
| 〃 | 〃 | シリアルコミュニケーション | × | × | × | × | × | × |
| 〃 | 〃 | CC-Link | × | × | × | × | × | × |

#### プロパティ一覧 (10.9 / 328 / 原本 p.330)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) |
|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | (同左) |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>1023(0x3FF)固定 |
| ActIONumber | 1023(0x3FF) | 0(0x00)固定 | 1023(0x3FF)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 |
| ActPortNumber | 1(PORT_1) | パソコン側CC-Link Ver.2ボードのポート番号，PORT1～PORT4(1枚目～4枚目) | (同左) |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_CCLINK(0x07) | (同左) |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 対象局側CC-Linkユニット局番 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_CCLINKBOARD(0x0C) | (同左) |

※「(同左)」は原本で2列が結合された1セル。

### 接続局がQシリーズのCC-Link通信 (10.9 / 329-331 / 原本 p.331-333)

#### 構成 (10.9 / 329 / 原本 p.331)

【図】構成 (10.9 / 329 / 原本 p.331)
- パソコン ―(線で直接)― 接続局CPU の CC-Link ユニット
- 接続局CPU の経由ユニット ―(経由ネットワーク)― 経由局CPU の経由ユニット

#### アクセス可否およびプロパティのパターン (10.9 / 329-330 / 原本 p.331-332)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可

| 自ボード | 接続局CPU: QCPU(Qモード) | QモーションCPU | 経由ネットワーク | 経由局CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|---|---|
| ○(1) | ○(2) | ○(2)*1*4 | CC IE TSN | × | × | × | × | × |
| 〃 | 〃 | 〃 | CC IE Control<br>CC IE Field | × | × | × | × | × |
| 〃 | 〃 | 〃 | MELSECNET/H | × | × | × | × | × |
| 〃 | 〃 | 〃 | Ethernet | × | × | × | × | × |
| 〃 | 〃 | 〃 | シリアルコミュニケーション | × | × | × | × | × |
| 〃 | 〃 | 〃 | CC-Link | × | × | × | × | × |

| 自ボード | 接続局CPU: QCPU(Qモード) | QモーションCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|---|---|
| ○(1) | ○(2) | ○(2)*1*4 | CC IE TSN | × | × | × | × | × | × |
| 〃 | 〃 | 〃 | CC IE Control<br>CC IE Field | ○(3) | ○(3)*2 | ○(3)*3 | ○(3)*2 | ○(3)*2 | × |
| 〃 | 〃 | 〃 | MELSECNET/H | ○(3) | ○(3) | × | ○(3) | ○(3) | × |
| 〃 | 〃 | 〃 | Ethernet | ○(3) | × | × | ○(3) | ○(3) | × |
| 〃 | 〃 | 〃 | シリアルコミュニケーション | × | × | × | × | × | × |
| 〃 | 〃 | 〃 | CC-Link | × | × | × | × | × | × |

| 自ボード | 接続局CPU: QCCPU | 経由ネットワーク | 経由局CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|---|
| ○(1) | ○(2)*5 | CC IE TSN | × | × | × | × | × |
| 〃 | 〃 | CC IE Control<br>CC IE Field | × | × | × | × | × |
| 〃 | 〃 | MELSECNET/H | × | × | × | × | × |
| 〃 | 〃 | Ethernet | × | × | × | × | × |
| 〃 | 〃 | シリアルコミュニケーション | × | × | × | × | × |
| 〃 | 〃 | CC-Link | × | × | × | × | × |

| 自ボード | 接続局CPU: QCCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|---|
| ○(1) | ○(2)*5 | CC IE TSN | × | × | × | × | × | × |
| 〃 | 〃 | CC IE Control<br>CC IE Field | ○(3) | ○(3)*2 | × | ○(3)*2 | ○(3)*2 | × |
| 〃 | 〃 | MELSECNET/H | ○(3) | ○(3) | × | ○(3) | ○(3) | × |
| 〃 | 〃 | Ethernet | × | × | × | × | × | × |
| 〃 | 〃 | シリアルコミュニケーション | × | × | × | × | × | × |
| 〃 | 〃 | CC-Link | × | × | × | × | × | × |

> *1 QモーションCPUを経由して経由局CPUにアクセスできません。
> *2 Q12DCCPU-V(基本機能モード)，QSCPU，QモーションCPUは，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。
> *3 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
> *4 マルチCPU構成時の，2号機以降の場合のみアクセス可能です。
> *5 Q24DHCCPU-V，Q24DHCCPU-LS，Q24DHCCPU-VG，Q26DHCCPU-LSは，通信経路が未サポートのためアクセスできません。

#### プロパティ一覧 (10.9 / 331 / 原本 p.333)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) |
|---|---|---|---|---|
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | (同左) | (同左) |
| ActDestinationIONumber | 0(0x00) | 0(0x00)固定 | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) |
| ActIONumber | 1023(0x3FF) | 0(0x00)固定 | 1023(0x3FF)固定 | 1023(0x3FF)固定 |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニットネットワークNo. |
| ActPortNumber | 1(PORT_1) | パソコン側CC-Link Ver.2ボードのポート番号，PORT1～PORT4(1枚目～4枚目) | (同左) | (同左) |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_CCLINK(0x07) | (同左) | (同左) |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 対象局側CC-Linkユニット局番 | 対象局側ユニット局番 |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 接続局側CC-Linkユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_CCLINKBOARD(0x0C) | (同左) | (同左) |

※「(同左)」は原本で(1)〜(3)の3列が結合された1セル。

---

## 10.10 CC-Linkシステム RS-232インタフェース通信 (10.10 / 332-334 / 原本 p.334-336)

### 構成 (10.10 / 332 / 原本 p.334)

【図】構成 (10.10 / 332 / 原本 p.334)
- パソコン ― AJ65BT-R2Nユニット(Qモード) ―(CC-Link)― 接続局CPU の CC-Link ユニット
- 接続局CPU の経由ユニット ―(経由ネットワーク)― 経由局CPU の経由ユニット

### アクセス可否およびプロパティのパターン (10.10 / 332-333 / 原本 p.334-335)

○(n): アクセス可能(nはプロパティのパターン)，×: アクセス不可
※この節の表には「自ボード」列が無い(原本どおり)。

| 接続局CPU: QCPU(Qモード) | QモーションCPU | 経由ネットワーク | 経由局CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|---|
| ○(1) | ○(2)*1*5 | CC IE TSN | × | × | × | × | × |
| 〃 | 〃 | CC IE Control<br>CC IE Field | × | × | × | × | × |
| 〃 | 〃 | MELSECNET/H | × | × | × | × | × |
| 〃 | 〃 | Ethernet | × | × | × | × | × |
| 〃 | 〃 | シリアルコミュニケーション | × | × | × | × | × |
| 〃 | 〃 | CC-Link | × | × | × | × | × |

| 接続局CPU: QCPU(Qモード) | QモーションCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|---|
| ○(1) | ○(2)*1*5 | CC IE TSN | × | × | × | × | × | × |
| 〃 | 〃 | CC IE Control<br>CC IE Field | ○(2) | ○(2)*2 | ○(2)*3 | ○(2)*2 | ○(2)*2 | × |
| 〃 | 〃 | MELSECNET/H | ○(2) | ○(2) | × | ○(2) | ○(2) | × |
| 〃 | 〃 | Ethernet | ○(2) | × | × | ○(2) | ○(2) | × |
| 〃 | 〃 | シリアルコミュニケーション | × | × | × | × | × | × |
| 〃 | 〃 | CC-Link | × | × | × | × | × | × |

| 接続局CPU: QCCPU | 経由ネットワーク | 経由局CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|
| ○(1)*4 | CC IE TSN | × | × | × | × | × |
| 〃 | CC IE Control<br>CC IE Field | × | × | × | × | × |
| 〃 | MELSECNET/H | × | × | × | × | × |
| 〃 | Ethernet | × | × | × | × | × |
| 〃 | シリアルコミュニケーション | × | × | × | × | × |
| 〃 | CC-Link | × | × | × | × | × |

| 接続局CPU: QCCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1)*4 | CC IE TSN | × | × | × | × | × | × |
| 〃 | CC IE Control<br>CC IE Field | ○(2) | ○(2)*2 | ○(2)*3 | ○(2)*2 | ○(2)*2 | × |
| 〃 | MELSECNET/H | ○(2) | ○(2) | × | ○(2) | ○(2) | × |
| 〃 | Ethernet | × | × | × | × | × | × |
| 〃 | シリアルコミュニケーション | × | × | × | × | × | × |
| 〃 | CC-Link | × | × | × | × | × | × |

| 接続局CPU: LCPU | 経由ネットワーク | 経由局CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU |
|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × |
| 〃 | CC IE Control<br>CC IE Field | × | × | × | × | × |
| 〃 | MELSECNET/H | × | × | × | × | × |
| 〃 | Ethernet | × | × | × | × | × |
| 〃 | シリアルコミュニケーション | × | × | × | × | × |
| 〃 | CC-Link | × | × | × | × | × |

| 接続局CPU: LCPU | 経由ネットワーク | 経由局CPU: QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|
| ○(1) | CC IE TSN | × | × | × | × | × | × |
| 〃 | CC IE Control<br>CC IE Field | × | × | × | × | × | × |
| 〃 | MELSECNET/H | × | × | × | × | × | × |
| 〃 | Ethernet | × | × | × | × | × | × |
| 〃 | シリアルコミュニケーション | × | × | × | × | × | × |
| 〃 | CC-Link | × | × | × | × | × | × |

> *1 QモーションCPUを経由して経由局CPUにアクセスできません。
> *2 RモーションCPU，Q12DCCPU-V(基本機能モード)，QSCPU，QモーションCPUは，CC-Link IEフィールドネットワーク未サポートのため，CC-Link IEフィールドネットワークにはアクセスできません。
> *3 LCPUは，CC-Link IEコントローラネットワーク未サポートのため，CC-Link IEコントローラネットワークにはアクセスできません。
> *4 Q24DHCCPU-V，Q24DHCCPU-LS，Q24DHCCPU-VG，Q26DHCCPU-LSは，通信経路が未サポートのためアクセスできません。
> *5 マルチCPU構成時の，2号機以降の場合のみアクセス可能です。

※要確認: アクセス可否表には○(1)と○(2)しか現れないが，下のプロパティ一覧にはパターン○(3)の列がある(原本どおり)。

### プロパティ一覧 (10.10 / 334 / 原本 p.336)

各通信経路で設定するプロパティを下記に示します。
記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | ○(1) | ○(2) | ○(3) |
|---|---|---|---|---|
| ActBaudRate | 19200(BAUDRATE_19200) | BAUDRATE_9600，BAUDRATE_19200，BAUDRATE_38400，BAUDRATE_57600，BAUDRATE_115200 | (同左) | (同左) |
| ActConnectUnitNumber | 0(0x00) | 接続局側ユニット局番 | (同左) | (同左) |
| ActControl | 8(TRC_DTR_OR_RTS) | 使用ケーブルによる | (同左) | (同左) |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ | (同左) | (同左) |
| ActIONumber*1 | 1023(0x3FF) | ■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 対象局側<br>■シングルCPU時<br>• 1023(0x3FF)固定<br>■マルチCPU時<br>• 接続号機: 1023(0x3FF)<br>• 1号機: 992(0x3E0)<br>• 2号機: 993(0x3E1)<br>• 3号機: 994(0x3E2)<br>• 4号機: 995(0x3E3)<br>■二重化CPU時<br>• 制御系: 976(0x3D0)<br>• 指定なし: 1023(0x3FF) | 接続局側経由ユニットI/Oアドレス |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 | 対象局側ユニットネットワークNo. | 0(0x00)固定 |
| ActPortNumber | 1(PORT_1) | パソコン側COMポートNo. | (同左) | (同左) |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_SERIAL(0x04) | (同左) | (同左) |
| ActStationNumber | 255(0xFF) | 255(0xFF)固定 | 対象局側ユニット局番 | 255(0xFF)固定 |
| ActThroughNetworkType | 0(0x00) | • MELSECNET/10を含まない: 0(0x00)<br>• MELSECNET/10を含む: 1(0x01) | (同左) | (同左) |
| ActTimeOut | 10000 | ms単位でユーザ任意 | (同左) | (同左) |
| ActUnitNumber | 0(0x00) | 0(0x00)固定 | 0(0x00)固定 | 対象局側ユニット局番 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_G4QNCPU(0x1B) | (同左) | (同左) |

※「(同左)」は原本で(1)〜(3)の3列が結合された1セル。

> *1 I/Oアドレスは，実際のI/O先頭No.を16で割った値を指定してください。

---

## 10.11 GX Simulator2通信 (10.11 / 335 / 原本 p.337)

### アクセス可否 (10.11 / 335 / 原本 p.337)

○: アクセス可能，×: アクセス不可

| 対象局 | 接続先CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU | QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 他局 | × | × | × | × | × | ○ | × | ○ | × | × | ○ |

### プロパティ一覧 (10.11 / 335 / 原本 p.337)

記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | プロパティのパターン |
|---|---|---|
| ActTargetSimulator | 0(0x00) | プロパティ [ActTargetSimulator]を参照<br>☞178ページ プロパティの詳細 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_SIMULATOR2(0x30) |

## 10.12 GX Simulator3通信 (10.12 / 335-336 / 原本 p.337-338)

### アクセス可否 (10.12 / 335 / 原本 p.337)

○: アクセス可能，×: アクセス不可

| 対象局 | 接続先CPU: MX-Rモデル | MX-Fモデル | RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU | QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 他局 | ○*1 | ○*1 | ○*1 | × | × | × | ○*1 | × | × | × | × | × | × |

> *1 対応しているCPUタイプを下記に示します。

| 接続先CPU | CPUタイプ |
|---|---|
| MX-Rモデル | MXR300-16，MXR300-32，MXR300-64，MXR500-128，MXR500-256 |
| MX-Fモデル | MXF100-8-N32，MXF100-8-P32，MXF100-16-N32，MXF100-16-P32 |
| RCPU | R00，R01，R02，R04，R04EN，R08，R08EN，R08P，R08PSF，R08SF，R16，R16EN，R16P，R16PSF，R16SF，R32，R32EN，R32P，R32PSF，R32SF，R120，R120EN，R120P，R120PSF，R120SF |
| FX5CPU | FX5U，FX5UJ |

### プロパティ一覧 (10.12 / 335-336 / 原本 p.337-338)

記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | プロパティのパターン |
|---|---|---|
| ActBaudRate | 19200(BAUDRATE_19200) | 0(0x00) |
| ActControl | 8(TRC_DTR_OR_RTS) | 0(0x00) |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ |
| ActDataBits | 8(DATABIT_8) | 0(0x00) |
| ActDestinationPortNumber | 0(0x00) | 0(0x00)固定 |
| ActDidPropertyBit | 1(0x01) | 0(0x00) |
| ActDsidPropertyBit | 1(0x01) | 0(0x00) |
| ActHostAddress | 1.1.1.1 | ループバックアドレス(127.0.0.1) |
| ActIONumber | 1023(0x3FF) | 0(0x00) |
| ActNetworkNumber | 0(0x00) | 0(0x00)固定 |
| ActPacketType | 0x01(PACKET_PLC1) | PACKET_PLC1 |
| ActParity | 1(ODD_PARITY) | 0(0x00) |
| ActPassword | あき | 0(0x00) |
| ActPortNumber | 1(PORT_1) | 0(0x00) |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_TCPIP(0x05) |
| ActStationNumber | 255(0xFF) | 対象局に該当するシステム番号 |
| ActStopBits | 0(STOPBIT_ONE) | 0(0x00)固定 |
| ActSumCheck | 0(NO_SUM_CHECK) | 0(0x00)固定 |
| ActThroughNetworkType | 0(0x00) | 0(0x00)固定 |
| ActTimeOut | 10000 | ms単位でユーザ任意 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_SIMULATOR3(0x31) |
| ActTargetSimulator | 0(0x00) | 対象局に該当する号機番号 |

※表は原本で p.337(ActBaudRate〜ActParity)と p.338(ActPassword〜ActTargetSimulator)にまたがる。

## 10.13 MT Simulator2通信 (10.13 / 336 / 原本 p.338)

### アクセス可否 (10.13 / 336 / 原本 p.338)

○: アクセス可能，×: アクセス不可

| 対象局 | 接続先CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU | QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 他局 | × | × | × | × | × | × | × | × | × | ○ | × |

### プロパティ一覧 (10.13 / 336 / 原本 p.338)

記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | プロパティのパターン |
|---|---|---|
| ActTargetSimulator | 0(0x00) | プロパティ [ActTargetSimulator]を参照<br>☞178ページ プロパティの詳細 |
| ActCpuType | CPU_Q02CPU | 対象局に該当するCPUタイプ(QモーションCPU) |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_SIMULATOR2(0x30) |

※ActCpuType のデフォルト値は他節の「34(CPU_Q02CPU)」と違い「CPU_Q02CPU」のみ(原本どおり)。ActUnitType が MT Simulator2 でも UNIT_SIMULATOR2(0x30) なのも原本どおり。

## 10.14 MELSOFT Mirror通信 (10.14 / 336-337 / 原本 p.338-339)

### アクセス可否 (10.14 / 336 / 原本 p.338)

○: アクセス可能，×: アクセス不可

| 対象局 | 接続先CPU: RCPU | RCCPU | RモーションCPU | LHCPU | FX5CPU | QCPU(Qモード) | QCCPU | LCPU | QSCPU | QモーションCPU | FXCPU |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 他局 | ○*1 | × | × | × | × | × | × | × | × | × | × |

> *1 対応しているCPUタイプを下記に示します。

| 接続先CPU | CPUタイプ |
|---|---|
| RCPU | R04，R08，R08P，R16，R16P，R32，R32P，R120，R120P |

### プロパティ一覧 (10.14 / 336-337 / 原本 p.338-339)

記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | プロパティのパターン |
|---|---|---|
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_RETHER_LCS(0x1008) |
| ActCpuType | 34(CPU_Q02CPU) | 対象局に該当するCPUタイプ |
| ActMirrorURL | あき | 接続するMELSOFT MirrorのURL |
| ActMirrorSystemID | 1(0x01) | 接続するMELSOFT MirrorのシステムID. |
| ActMirrorSlotNumber | 0(0x00) | 接続するMELSOFT MirrorのスロットNo. |
| ActTimeOut | 10000 | ms単位でユーザ任意 |

※表は原本で p.338(ActUnitType〜ActMirrorSystemID)と p.339(ActMirrorSlotNumber，ActTimeOut)にまたがる。

## 10.15 GOTゲートウェイデバイス通信 (10.15 / 337 / 原本 p.339)

### 構成 (10.15 / 337 / 原本 p.339)

【図】構成 (10.15 / 337 / 原本 p.339)
- パソコン ― GOT の1対1接続(接続媒体の表記なし)

### プロパティ一覧 (10.15 / 337 / 原本 p.339)

記載のないプロパティについては設定不要です。

| プロパティ | デフォルト値 | プロパティのパターン |
|---|---|---|
| ActHostAddress | 1.1.1.1 | 接続するGOTのホスト名またはIPアドレス |
| ActPortNumber | 1(PORT_1) | パソコン側COMポート番号 |
| ActProtocolType | 0x04(PROTOCOL_SERIAL) | PROTOCOL_UDPIP(0x08) |
| ActTimeOut | 10000 | ms単位でユーザ任意 |
| ActUnitType | 0x13(UNIT_QNCPU) | UNIT_A900GOT(0x21) |

※要確認: プロトコルが PROTOCOL_UDPIP(0x08) なのに ActPortNumber のパターンが「パソコン側COMポート番号」となっている(原本どおり)。
