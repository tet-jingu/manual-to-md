# MX Component Version 5 リファレンスマニュアル 2章 システム構成 (2 / 原本 p.31-42)

| 項目 | 内容 |
|---|---|
| 原本 | 【三菱】MX Component Version 5 リファレンスマニュアル (SH-082394J) |
| メーカー | 三菱電機 |
| 原本ファイル | `PDF/【三菱】MX Component Version 5 リファレンスマニュアル_sh082394j.pdf` (全696ページ) |
| 本ファイルの範囲 | 2章 システム構成 (印刷ページ 29-40 / PDF p.31-42) |
| 出典表記 | `(節 / 印刷ページ / 原本 p.PDFページ)` |
| 作成日 | 2026-11-02 |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。
> 本文中の「○ページ」はすべて原本の**印刷ページ番号**です(PDFページ = 印刷ページ + 2)。

## 主要用語 対訳表 (Glossary)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| 動作環境 | Operating environment | — | 参考訳 |
| 通信経路 | Communication route | — | 参考訳 |
| シリアルコミュニケーション通信 | Serial communication | C24 | 参考訳 |
| シリアルコミュニケーションユニット | Serial communication module | C24 | 参考訳 |
| シリアルコミュニケーション機能対応CPU | CPU supporting serial communication function | Q00UJ/Q00U/Q01U/Q02UCPU | 参考訳 |
| Ethernet通信 | Ethernet communication | E71 | 参考訳 |
| Ethernet内蔵形CPU | Built-in Ethernet port CPU | — | 参考訳 |
| Ethernetアダプタユニット | Ethernet adapter module | NZ2GF-ETB | 参考訳 |
| Ethernet直結接続 | Ethernet direct connection | — | 参考訳 |
| CPU COM通信 / CPU USB通信 | CPU COM communication / CPU USB communication | — | 参考訳 |
| FX拡張ポート | FX extended port | FX***-485-BD | 参考訳 |
| 機能拡張ボード | Expansion board | FX3U-***-BD | 参考訳 |
| 特殊アダプタ / 拡張アダプタ | Special adapter / Expansion adapter | ADP | 参考訳 |
| 変換器 | Converter | — | 参考訳 |
| マルチドロップ接続 | Multidrop connection | — | 参考訳 |
| 1:1接続 | 1:1 connection | — | 参考訳 |
| 通信ドライバ | Communication driver | SW0DNC-MNETH-B 等 | 参考訳 |
| ネットワークボード | Network board | — | 参考訳 |
| CC-Link IEコントローラネットワーク | CC-Link IE Controller Network | — | 参考訳 |
| CC-Link IEフィールドネットワーク | CC-Link IE Field Network | — | 参考訳 |
| CC-Linkマスタ局 | CC-Link master station | — | 参考訳 |
| ソフトウェアバージョン | Software version | — | 参考訳 |
| 機能バージョン | Function version | — | 参考訳 |
| GOTゲートウェイデバイス通信 | GOT gateway device communication | — | 参考訳 |
| GOTトランスペアレント通信 | GOT transparent communication | — | 参考訳 |
| インバータ | Inverter | — | 参考訳 |
| ロボットコントローラ | Robot controller | CR750 / CRnD-700 | 参考訳 |
| 安全シーケンサシステム | Safety programmable controller system | — | 参考訳 |
| セーフティモード | Safety mode | — | 参考訳 |
| 安全デバイス | Safety device | — | 参考訳 |
| リモート操作 / リモートPAUSE | Remote operation / Remote PAUSE | — | 参考訳 |
| 伝送速度 / 通信速度 | Transmission speed / Communication speed | — | 参考訳 |
| インデックスレジスタ | Index register | Z, V | 参考訳 |
| タイマ現在値 / カウンタ現在値 | Timer current value / Counter current value | TN / CN | 参考訳 |
| 先頭I/O番号 | Start I/O number | — | 参考訳 |
| 多重通信 | Multiple communication | — | 参考訳 |
| PCパラメータ | PC parameter | GX Works2 | 参考訳 |
| シミュレーション機能 | Simulation function | GX Simulator2 / GX Simulator3 / MT Simulator2 / MELSOFT Mirror | 参考訳 |

## 変換範囲表

| 原本ページ(PDF) | 印刷ページ | 節 | 扱い |
|---|---|---|---|
| p.31 | 29 | 2.1 動作環境 / 2.2 サポートする通信経路 | 全文 |
| p.32-33 | 30-31 | 2.3 システム構成一覧 | 全文(構成図は文章化) |
| p.34-36 | 32-34 | 2.4 使用可能な機種一覧 | 全文 |
| p.37-42 | 35-40 | 2.5 各通信経路の詳細内容 | 全文 |
| p.1-17 | — | 前付け | **未変換** |
| p.18-30 | 16-28 | 1章 | 別ファイル `01_MX_Componentの基本_ladder_reference.md` |
| p.43-696 | 41- | 3章〜13章・付録ほか | **未変換** |

## 目次

- 2.1 動作環境
- 2.2 サポートする通信経路
- 2.3 システム構成一覧
- 2.4 使用可能な機種一覧
- 2.5 各通信経路の詳細内容

---

MX Componentの動作環境，通信経路，使用可能な機器などのシステム構成について説明します。

## 2.1 動作環境 (2.1 / 29 / 原本 p.31)

MX Componentの動作環境は，下記を参照してください。
📖MX Component Version 5インストール手順書(BCN-P5999-1383)

## 2.2 サポートする通信経路 (2.2 / 29 / 原本 p.31)

MX Componentは，下記の通信経路をサポートしています。

| 通信経路 | 内容 | 参照先 |
|---|---|---|
| シリアルコミュニケーション通信 | シリアルコミュニケーションユニットを使用して，CPUユニットと通信します。 | ☞35ページ シリアルコミュニケーション通信 |
| Ethernet通信 | パソコンとEthernetユニットまたはEthernet内蔵形CPUを接続して通信します。 | ☞36ページ Ethernet通信 |
| CPU COM通信 | パソコンをCPUユニットのRS-232コネクタまたはRS-422コネクタに接続して通信します。 | ☞36ページ CPU COM通信 |
| CPU USB通信 | パソコンをCPUユニットのUSBコネクタに接続して通信します。 | ☞39ページ CPU USB通信 |
| MELSECNET/H通信 | MELSECNET/Hボードを使用して，CPUユニットと通信します。 | ☞39ページ MELSECNET/H通信 |
| CC-Link IEコントローラネットワーク通信 | CC-Link IEコントローラネットワークボードを使用して，CPUユニットと通信します。 | ☞39ページ CC-Link IEコントローラネットワーク通信 |
| CC-Link IEフィールドネットワーク通信 | CC-Link IEフィールドネットワークボードを使用して，CPUユニットと通信します。 | ☞39ページ CC-Link IEフィールドネットワーク通信 |
| CC-Link IE TSN通信 | CC-Link IE TSNボードを使用して，CPUユニットと通信します。 | ☞39ページ CC-Link IE TSN通信 |
| CC-Link通信 | CC-Link Ver.2ボードを使用して，CPUユニットと通信します。 | ☞39ページ CC-Link通信 |
| CC-Linkシステム RS-232インタフェース通信 | AJ65BT-R2Nユニットを使用して，CPUユニットと通信します。 | ☞40ページ CC-Linkシステム RS-232インタフェース通信 |
| GX Simulator2通信 | GX Works2のシミュレーション機能を使用して通信します。 | ☞40ページ GX Simulator2通信 |
| GX Simulator3通信 | GX Works3のシミュレーション機能を使用して通信します。 | ☞40ページ GX Simulator3通信 |
| MT Simulator2通信 | MT Developer2のシミュレーション機能を使用して通信します。 | ☞40ページ MT Simulator2通信 |
| MELSOFT Mirror通信 | MELSOFT Mirrorのシミュレーション機能を使用して通信します。 | ☞40ページ MELSOFT Mirror 通信 |
| GOTゲートウェイデバイス通信 | GOTのゲートウェイ機能を使用して，CPUユニットおよび各社シーケンサと通信します。 | ☞40ページ GOTゲートウェイデバイス通信 |
| GOTトランスペアレント通信 | GOTのトランスペアレント機能を使用して，CPUユニットと通信します。 | ☞40ページ GOTトランスペアレント通信 |
| インバータCOM通信 | インバータをパソコンのCOMポートに接続して通信します。 | ☞40ページ インバータ(COM/USB)通信 |
| インバータUSB通信 | インバータをパソコンのUSBポートに接続して通信します。 | ☞40ページ インバータ(COM/USB)通信 |
| ロボットコントローラCOM通信 | ロボットコントローラをパソコンのCOMポートに接続して通信します。 | ☞40ページ ロボットコントローラ(COM/USB/Ethernet)通信 |
| ロボットコントローラUSB通信 | ロボットコントローラをパソコンのUSBポートに接続して通信します。 | ☞40ページ ロボットコントローラ(COM/USB/Ethernet)通信 |
| ロボットコントローラEthernet通信 | ロボットコントローラとパソコンをEthernetに接続して通信します。 | ☞40ページ ロボットコントローラ(COM/USB/Ethernet)通信 |

※インバータ2行・ロボットコントローラ3行は，原本では参照先セルを共有。

---

## 2.3 システム構成一覧 (2.3 / 30-31 / 原本 p.32-33)

> **Point**
> 使用可能なケーブルおよび通信時の注意事項などの詳細は，各ユニットのマニュアルを参照してください。

### 各通信経路のシステム構成例 (2.3 / 30-31 / 原本 p.32-33)

【図】各通信経路のシステム構成例(その1) (2.3 / 30 / 原本 p.32)。パソコンからの接続を通信経路ごとに文章化:

| 通信経路 | パソコン側 | 経路(媒体・中継) | 接続先 |
|---|---|---|---|
| シリアルコミュニケーション通信 | — | RS-232 | MELSEC iQ-Rシリーズ対応C24，Qシリーズ対応C24，Lシリーズ対応C24 |
| シリアルコミュニケーション通信 | — | RS-232/RS-485変換 | FX拡張ポート(FX***-485-BD) |
| Ethernet通信 | Ethernetボード | Ethernet | Ethernetユニット |
| Ethernet通信 | Ethernetボード | Ethernet | Ethernet内蔵形CPU |
| Ethernet通信 | Ethernetボード | Ethernet → Ethernetアダプタユニット → CC-Link IEフィールドネットワーク | CC-Link IEフィールドネットワークユニット |
| Ethernet通信 | Ethernetボード | Ethernet | Ethernetアダプタ/Ethernetユニット |
| Ethernet通信 | Ethernetボード | Ethernet | CC-Link IE TSNユニット |
| CPU COM通信 | — | RS-232 | FX5CPU(FX5-232-BD，FX5-232ADP) |
| CPU COM通信 | — | RS-232，RS-232/RS-422変換 | QCPU(Qモード)，LCPU，QモーションCPU，FXCPU |
| CPU COM通信 | — | 変換器／ケーブル | FXCPU(FX3S/FX3G/FX3GC/FX3U/FX3UC) |
| CPU USB通信 | — | USB | MXコントローラ，RCPU，RモーションCPU，LHCPU，FX5CPU(FX5UJ)，QCPU(Qモード），LCPU，C言語コントローラ，QSCPU，QモーションCPU，FXCPU(FX3S/FX3G/FX3GC) |
| MELSECNET/H通信 | MELSECNET/Hボード | MELSECNET/H | MELSECNET/Hユニット |
| CC-Link IEコントローラネットワーク通信 | CC-Link IEコントローラネットワークボード | CC-Link IEコントローラネットワーク | CC-Link IEコントローラネットワークユニット |
| CC-Link IEフィールドネットワーク通信 | CC-Link IEフィールドネットワークボード | CC-Link IEフィールドネットワーク | CC-Link IEフィールドネットワークユニット |
| CC-Link IE TSN通信 | CC-Link IE TSNボード | CC-Link IE TSN | CC-Link IE TSNユニット |
| CC-Link通信 | CC-Link Ver.2ボード | CC-Link | CC-Linkユニット |
| CC-Linkシステム RS-232インタフェース通信 | — | RS-232 → AJ65BT-R2ユニット → CC-Link | CC-Linkユニット |

※図中のAJ65BT-R2ユニットの表記は原本図のまま(本文・2.4の表ではAJ65BT-R2N)。

【図】各通信経路のシステム構成例(その2) (2.3 / 31 / 原本 p.33):

| 通信経路 | パソコン側 | 経路(媒体・中継) | 接続先 |
|---|---|---|---|
| GX Simulator2通信 | — | (パソコン内) | GX Works2 シミュレーション機能（GX Simulator2） |
| GX Simulator3通信 | — | (パソコン内) | GX Works3 シミュレーション機能（GX Simulator3） |
| MT Simulator2通信 | — | (パソコン内) | MT Developer2 シミュレーション機能（MT Simulator2） |
| MELSOFT Mirror通信 | — | (パソコン内) | MELSOFT Mirror シミュレーション機能 |
| GOTゲートウェイデバイス通信 | Ethernetボード | Ethernet | GOT |
| GOTトランスペアレント通信 | — | USB, RS-232 / Ethernet → GOT → RS-232 | RCPU，QCPU（Qモード），LCPU，C言語コントローラ，QモーションCPU |
| GOTトランスペアレント通信 | — | USB, RS-232 / Ethernet → GOT → RS-232/RS-422 | FX5CPU，FXCPU |
| GOTトランスペアレント通信 | — | USB, RS-232 / Ethernet → GOT → RS-232 | MELSEC iQ-Rシリーズ対応C24，Qシリーズ対応C24，Lシリーズ対応C24 |
| GOTトランスペアレント通信 | — | USB, RS-232 / Ethernet → GOT → Ethernet | Ethernetユニット |
| GOTトランスペアレント通信 | — | USB, RS-232 / Ethernet → GOT → Ethernet | Ethernet内蔵形CPU |
| GOTトランスペアレント通信 | — | USB, RS-232 / Ethernet → GOT → Ethernet → Ethernetアダプタユニット → CC-Link IEフィールドネットワーク | CC-Link IEフィールドネットワークユニット |
| GOTトランスペアレント通信 | — | USB, RS-232 / Ethernet → GOT → Ethernet | Ethernetアダプタ/Ethernetユニット |
| インバータCOM通信 | — | RS-232/RS-485変換 | インバータ |
| インバータUSB通信 | — | USB | インバータ |
| ロボットコントローラCOM通信 | — | RS-232 | ロボットコントローラ |
| ロボットコントローラUSB通信 | — | USB | ロボットコントローラ |
| ロボットコントローラEthernet通信 | Ethernetボード | Ethernet | ロボットコントローラ |

---

## 2.4 使用可能な機種一覧 (2.4 / 32-34 / 原本 p.34-36)

MX Componentで使用可能な機種を示します。

### CPUユニット (2.4 / 32 / 原本 p.34)

使用可能なCPUユニットを一覧で示します。

| 分類 | 分類(詳細) | 形名 |
|---|---|---|
| MXコントローラ | MXR300 | MXR300-16，MXR300-32，MXR300-64 |
| MXコントローラ | MXR500 | MXR500-128，MXR500-256 |
| MXコントローラ | MXF100 | MXF100-8-N32，MXF100-8-N32-EC，MXF100-8-P32，MXF100-16-N32，MXF100-16-N32-EC，MXF100-16-P32 |
| RCPU | RnCPU | R00CPU，R01CPU，R02CPU，R04CPU，R04ENCPU，R08CPU，R08ENCPU，R16CPU，R16ENCPU，R32CPU，R32ENCPU，R120CPU，R120ENCPU |
| RCPU | RnPCPU | R08PCPU，R16PCPU，R32PCPU，R120PCPU |
| RCPU | RnSFCPU | R08SFCPU，R16SFCPU，R32SFCPU，R120SFCPU |
| RCPU | RnPSFCPU | R08PSFCPU，R16PSFCPU，R32PSFCPU，R120PSFCPU |
| RCCPU | — | R12CCPU-V |
| RモーションCPU | — | R16MTCPU，R32MTCPU，R64MTCPU |
| WinCPU | — | R102WCPU-W |
| LHCPU | — | L04HCPU，L08HCPU，L16HCPU，L32HCPU |
| FX5CPU | — | FX5UCPU，FX5UCCPU，FX5UJCPU，FX5SCPU |
| QCPU(Qモード) | — | Q00UJCPU，Q00UCPU，Q01UCPU，Q02UCPU，Q03UDCPU，Q03UDECPU，Q03UDVCPU，Q04UDHCPU，Q04UDEHCPU，Q04UDVCPU，Q04UDPVCPU，Q06UDHCPU，Q06UDEHCPU，Q06UDVCPU，Q06UDPVCPU，Q10UDHCPU，Q10UDEHCPU，Q12PRHCPU，Q13UDHCPU，Q13UDEHCPU，Q13UDVCPU，Q13UDPVCPU，Q20UDHCPU，Q20UDEHCPU，Q25PRHCPU，Q26UDHCPU，Q26UDEHCPU，Q26UDVCPU，Q26UDPVCPU，Q50UDEHCPU，Q100UDEHCPU |
| LCPU | — | L02SCPU，L02CPU，L06CPU，L26CPU，L26CPU-BT |
| QCCPU | — | Q12DCCPU-V(基本機能モード)*1，Q12DCCPU-V(機能拡張モード)，Q24DHCCPU-V，Q24DHCCPU-LS，Q24DHCCPU-VG，Q26DHCCPU-LS |
| QSCPU | — | QS001CPU |
| QモーションCPU | — | Q172DCPU，Q173DCPU，Q172DSCPU，Q173DSCPU |
| FXCPU | — | FX3SCPU，FX3GCPU，FX3GCCPU，FX3UCPU，FX3UCCPU |

> *1 シリアルNo.の上5桁が"12042"以降品のみ対応しています。

### 注意事項 (2.4 / 33 / 原本 p.35)

#### RnSFCPU (2.4 / 33 / 原本 p.35)

安全シーケンサシステムを保護するため，セーフティモードでの，バッファメモリに対する書込み，安全デバイスに対する書込みを行う関数は実行できません。

#### FX5CPU (2.4 / 33 / 原本 p.35)

- Ethernet直結接続で使用するアダプタを指定し通信する場合は，異なるアダプタを指定した経路で複数同時に通信することはできません。
- 通信設定のパソコン側アダプタの情報は，パソコン環境の変化や他のMELSOFTアプリケーションの設定により，再設定が必要になる場合があります。

#### Q00UJ/Q00U/Q01U/Q02UCPU (2.4 / 33 / 原本 p.35)

Q00UJ/Q00U/Q01U/Q02UCPUをシリアルコミュニケーション機能対応CPUと記載します。
下記の条件をすべて満たすときは，パソコン-シリアルコミュニケーション機能対応CPU間の通信速度は9600bpsです。

- 接続CPUのシリアルコミュニケーション機能が有効になっている。
- パソコン側伝送速度設定とシリアルコミュニケーション機能対応CPU側伝送速度設定が異なっている。

なお，通信速度を向上させたい場合は，パソコン側伝送速度とシリアルコミュニケーション機能対応CPU側伝送速度を一致させてください。

#### QSCPU (2.4 / 33 / 原本 p.35)

安全シーケンサシステムを保護するため，セーフティモードでの，バッファメモリに対する書込み，安全デバイスに対する書込みを行う関数は実行できません。

#### Ethernet内蔵形CPU (2.4 / 33 / 原本 p.35)

- MX Componentを使用してTCP/IPコネクション確立中(Open中)にCPUユニットをリセットすると，それ以降の通信時に通信エラーや受信エラーが発生します。
  その場合は，MX Componentを使用するアプリケーション内でクローズ処理をしたあと，再度オープン処理を行ってください。
- 別のパソコンでEthernet直結接続で通信していたCPUに対して，Ethernet直結接続を行う場合に通信エラーとなる場合があります。この場合は，CPUをリセットし再度通信を実行してください。

#### FXCPU (2.4 / 33 / 原本 p.35)

- FXCPU使用時のTNデバイス(タイマ現在値)およびCNデバイス(カウンタ現在値)へのアクセスは，デバイス番号199以前からデバイス番号200を越えてアクセスすることはできません。
- FXCPUは，CPUユニットとしてPAUSEスイッチを持たないため，SetCpuStatusでリモートPAUSEを指定するとエラーを返します。
- ユニットが存在しない先頭I/O番号を指定してWriteBuffer()メソッドを実行しても，エラーは返りませんので注意してください。
- FXCPUのインデックスレジスタ(Z，V)に対して，WriteDeviceBlock()で2点以上を連続して書き込むことはできません。(1点のみ書込み可能です。)

### ユニット (2.4 / 34 / 原本 p.36)

各通信形態でCPUユニットと通信する場合に使用可能なユニットおよびボードを一覧で示します。

| 通信形態 | 分類 | 形名 |
|---|---|---|
| シリアルコミュニケーション通信 | MELSEC iQ-Rシリーズ対応C24 | RJ71C24，RJ71C24-R2，RJ71C24-R4 |
| シリアルコミュニケーション通信 | Qシリーズ対応C24 | QJ71C24，QJ71C24N，QJ71C24N-R2，QJ71C24N-R4 |
| シリアルコミュニケーション通信 | Lシリーズ対応C24 | LJ71C24，LJ71C24-R2 |
| シリアルコミュニケーション通信 | FX拡張ポート | FX3G-485-BD，FX3U-485-BD |
| Ethernet通信 | MELSEC iQ-Rシリーズ対応E71 | RJ71EN71 |
| Ethernet通信 | Qシリーズ対応E71 | QJ71E71，QJ71E71-B2，QJ71E71-B5，QJ71E71-100 |
| Ethernet通信 | Lシリーズ対応E71 | LJ71E71-100 |
| Ethernet通信 | Ethernetアダプタユニット | NZ2GF-ETB |
| Ethernet通信 | Ethernetアダプタ/Ethernetユニット | FX3U-ENET-ADP，FX3U-ENET-L，FX5-CCLGN-MS，FX5-ENET，FX5-ENET/IP |
| MELSECNET/H通信 | MELSECNET/Hユニット | QJ71LP21-25，QJ71BR11 |
| MELSECNET/H通信 | MELSECNET/Hボード*1 | Q80BD-J71LP21-25，Q80BD-J71LP21S-25，Q81BD-J71LP21-25，Q80BD-J71LP21G，Q80BD-J71BR11 |
| CC-Link通信 | CC-Linkユニット | RJ61BT11 |
| CC-Link通信 | CC-Linkユニット | QJ61BT11N |
| CC-Link通信 | CC-Linkユニット | LJ61BT11 |
| CC-Link通信 | CC-Linkユニット | FX3U-64CCL |
| CC-Link通信 | CC-Link Ver.2ボード*2 | Q80BD-J61BT11N，Q81BD-J61BT11 |
| CC-Linkシステム RS-232インタフェース通信 | AJ65BT-R2Nユニット | AJ65BT-R2N |
| CC-Link IEコントローラネットワーク通信 | CC-Link IEコントローラネットワークユニット | RJ71GP21-SX |
| CC-Link IEコントローラネットワーク通信 | CC-Link IEコントローラネットワークユニット | QJ71GP21S-SX，QJ71GP21-SX |
| CC-Link IEコントローラネットワーク通信 | CC-Link IEコントローラネットワークボード*3 | Q80BD-J71GP21-SX，Q80BD-J71GP21S-SX，NZ81GP21-SX |
| CC-Link IEフィールドネットワーク通信 | CC-Link IEフィールドネットワークユニット | RJ71GF11-T2 |
| CC-Link IEフィールドネットワーク通信 | CC-Link IEフィールドネットワークユニット | QJ71GF11-T2 |
| CC-Link IEフィールドネットワーク通信 | CC-Link IEフィールドネットワークユニット | LJ71GF11-T2 |
| CC-Link IEフィールドネットワーク通信 | CC-Link IEフィールドネットワークボード*4 | Q81BD-J71GF11-T2 |
| CC-Link IE TSN通信 | CC-Link IE TSNユニット | RJ71GN11-T2，RJ71GN11-SX |
| CC-Link IE TSN通信 | CC-Link IE TSNボード*5 | NZ81GN11-T2，NZ81GN11-SX |
| GOTトランスペアレント通信 | GOT2000 | GT27，GT25 |
| GOTトランスペアレント通信 | GOT3000 | GT37 |
| インバータ通信 | A800 | — |
| ロボットコントローラ通信 | CR750 | CR750-DCR751-D |
| ロボットコントローラ通信 | CRnD-700 | CR1DA-7xx，CR2DA-7xx，CR3DA-7xx |

※CR750の形名は原本表記のまま「CR750-DCR751-D」(区切り記号が無い。CR750-D，CR751-D の意と思われるが要確認)。

> *1 使用可能ドライバ: SW0DNC-MNETH-B(バージョン30G)以降
> *2 使用可能ドライバ: SW1DNC-CCBD2-B(バージョン1.19V)
> *3 使用可能ドライバ: SW1DNC-MNETG-B(バージョン1.22Y)以降
> *4 使用可能ドライバ: SW1DNC-CCIEF-B(バージョン1.10L)
> *5 使用可能ドライバ: SW1DNN-CCIETBDM-B(バージョン1.000A)以降

---

## 2.5 各通信経路の詳細内容 (2.5 / 35-40 / 原本 p.37-42)

各通信経路の詳細および注意事項などを説明します。

### シリアルコミュニケーション通信 (2.5 / 35 / 原本 p.37)

シリアルコミュニケーションユニットへの接続方法は，ご使用のシリアルコミュニケーションユニットのマニュアルを参照してください。

#### シリアルコミュニケーション通信について (2.5 / 35 / 原本 p.37)

- シリアルコミュニケーションユニットでは，すべての接続でリモート操作"PAUSE"がエラーとなります。
- FX3S，FX3G(C)，FX3U(C)CPUでシリアルコミュニケーション通信をする場合は，FX拡張ポートが必要です。

#### 使用可能ユニットの接続について (2.5 / 35 / 原本 p.37)

パソコンからシリアルコミュニケーションユニット経由でCPUユニットにアクセスする場合，パソコンと直接接続できるユニットが限定されますので注意してください。
また，パソコンと直接接続できない場合でも，マルチドロップ接続のn台目として使用できることがあります。
○: 接続可能，×: 接続不可

| 形名 | インタフェース | 1:1接続 | マルチドロップ接続 1台目 | マルチドロップ接続 n台目 |
|---|---|---|---|---|
| RJ71C24 | RS-232(CH1) | ○ | ○ | × |
| RJ71C24 | RS-422/485(CH2) | × | × | ○ |
| RJ71C24-R2 | RS-232(CH1) | ○ | × | × |
| RJ71C24-R2 | RS-232(CH2) | ○ | × | × |
| RJ71C24-R4 | RS-422/485(CH1) | × | × | ○ |
| RJ71C24-R4 | RS-422/485(CH2) | × | × | ○ |
| QJ71C24<br>QJ71C24N | RS-232(CH1) | ○ | ○ | × |
| QJ71C24<br>QJ71C24N | RS-422/485(CH2) | × | × | ○ |
| QJ71C24N-R2 | RS-232(CH1) | ○ | × | × |
| QJ71C24N-R2 | RS-232(CH2) | ○<br>(機能バージョンB以降品) | × | × |
| QJ71C24N-R4 | RS-422/485(CH1) | × | × | ○ |
| QJ71C24N-R4 | RS-422/485(CH2) | × | × | ○ |
| LJ71C24 | RS-232(CH1) | ○ | ○ | × |
| LJ71C24 | RS-422/485(CH2) | × | × | ○ |
| LJ71C24-R2 | RS-232(CH1) | ○ | × | × |
| LJ71C24-R2 | RS-232(CH2) | ○ | × | × |
| FX3G-485-BD<br>FX3U-485-BD | RS-422/485 | ○ | ○ | ○ |

### Ethernet通信 (2.5 / 36 / 原本 p.38)

- Ethernetユニットへの接続方法は，ご使用のEthernetユニットのマニュアルを参照してください。
- FXシリーズ用のEthernetユニットについては，FXシリーズのユーザーズマニュアルを参照してください。
- Ethernet内蔵形CPUへの接続方法は，ご使用のEthernet内蔵形CPUのマニュアルを参照してください。
- Ethernetアダプタユニットへの接続方法は，ご使用のEthernetアダプタユニットのマニュアルを参照してください。
- Ethernetアダプタへの接続方法は，ご使用のEthernetアダプタのマニュアルを参照してください。
- CC-Link IE TSNユニットへの接続方法は，ご使用のCC-Link IE TSNユニットのマニュアルを参照してください。

### CPU COM通信 (2.5 / 36-38 / 原本 p.38-40)

#### QCPU(Qモード)，LCPU接続時のケーブル (2.5 / 36 / 原本 p.38)

パソコンとQCPU(Qモード)間で交信を行うためには，下記のケーブルが必要です。

| RS-232ケーブル |
|---|
| QC30R2(パソコンのコネクタがDサブ9ピン) |

LCPUと接続する場合は，RS-232アダプタ(L6ADP-R2)が必要です。

#### FX5CPU接続時のケーブル (2.5 / 36 / 原本 p.38)

パソコンとFX5CPU間で交信を行うためには，下記のケーブルが必要です。

| 必要になる機能拡張ボードおよび拡張アダプタ | RS-232ケーブル |
|---|---|
| • FX5-232ADP<br>• FX5-232-BD | FX-232CAB-1 |

詳細は下記を参照してください。
📖MELSEC iQ-F FX5Uユーザーズマニュアル(ハードウェア編)

#### FXCPU接続時のケーブル (2.5 / 36 / 原本 p.38)

パソコンとFXCPU間で交信を行うためには，下記のケーブルが必要です。

| パソコン側(RS-232ケーブル) | RS-232/RS-422変換器 | CPUユニット側(RS-422ケーブル) |
|---|---|---|
| • F2-232CAB(Dサブ25ピン↔Dサブ25ピン)<br>• F2-232CAB-1(Dサブ9ピン↔Dサブ25ピン)<br>• F2-232CAB-2(ハーフピッチ↔Dサブ25ピン)<br>• AC30N2A(25ピン↔25ピン) | • FX-232AW<br>• FX-232AWC<br>• FX-232AWC-H | FX-422CAB0 (1.5m) |

#### QモーションCPU接続時のケーブル (2.5 / 36 / 原本 p.38)

パソコンとQモーションCPU間で交信を行う場合，下記と同様のケーブルを使用してください。
☞36ページ QCPU(Qモード)，LCPU接続時のケーブル

#### パソコン側USB接続時の変換器/ケーブル(FXCPU対応) (2.5 / 36 / 原本 p.38)

システム構成

- FX-USB-AW
- USBケーブル(同梱)

> **Point**
> - USBケーブルを初めて使用する場合
>   FX-USB-AWまたは，FX3U-USB-BDに同梱しているCDのドライバをインストールしてください。
> - 注意事項，制約事項について
>   FX-USB-AW使用時の注意事項，制約事項は，同梱しているマニュアルを参照してください。

#### USBケーブルと機能拡張ボード(FX3U/FX3UCCPU対応) (2.5 / 37 / 原本 p.39)

システム構成

- FX3U-USB-BD
- USBケーブル(同梱)

> **Point**
> - USBケーブルを初めて使用する場合
>   FX-USB-AWまたは，FX3U-USB-BDに同梱しているCDのドライバをインストールしてください。
> - 注意事項，制約事項について
>   FX3U-USB-BD使用時の注意事項，制約事項は，同梱しているマニュアルを参照してください。
> - PCパラメータについて
>   GX Works2で，PCパラメータの[PCシステム設定(2)]タブの"通信設定をする"にチェックを入れると，このポートによるCPUユニットとの通信ができなくなります。この場合は，CPUユニット内蔵のプログラミングポートよりこの設定をはずした設定を書き込んでください。
>   PCパラメータの設定方法については，下記のマニュアルを参照してください。
>   📖GX Works2 Version 1 オペレーティングマニュアル (共通編)

#### USBケーブル(FX3S/FX3G/FX3GCCPU対応) (2.5 / 37 / 原本 p.39)

ケーブルの詳細は下記を参照してください。
📖FX3Sシリーズ ユーザーズマニュアル[ハードウェア編]
📖FX3Gシリーズ ユーザーズマニュアル[ハードウェア編]
📖FX3GCシリーズ ユーザーズマニュアル[ハードウェア編

※最後の書名は原本表記のまま(閉じ括弧「]」が無い)。

> **Point**
> - USBケーブルを初めて使用する場合
>   USBドライバをインストールしてください。(☞669ページ USBドライバのインストール)

#### FXCPUのRS-422機能拡張ボード (2.5 / 37 / 原本 p.39)

| シリーズ | 機能拡張ボード |
|---|---|
| FX3U，FX3UC(FX3UC-32MT-LT，FX3UC-32MT-LT-2のみ) | FX3U-422-BD |
| FX3S，FX3G | FX3G-422-BD |

> **Point**
> - PCパラメータについて
>   GX Works2で，PCパラメータの[PCシステム設定(2)]タブの"通信設定をする"にチェックを入れると，このポートによるCPUユニットとの通信ができなくなります。
>   この場合は，CPUユニット内蔵のプログラミングポートよりこの設定をはずした設定を書き込んでください。
>   PCパラメータの設定方法については，下記を参照してください。
>   📖GX Works2 Version 1 オペレーティングマニュアル (共通編)

#### FXCPUのRS-232ケーブルと機能拡張ボード(特殊アダプタ) (2.5 / 38 / 原本 p.40)

| パソコンのシリアルポートの形状 | シリーズ | 必要になる機能拡張ボードおよび特殊アダプタ | RS-232ケーブル |
|---|---|---|---|
| Dサブ9ピン | FX3U，FX3UC | FX3U-232-BD*1 | FX-232CAB-1 |
| Dサブ9ピン | FX3U，FX3UC | 機能拡張ボード(FX3U-***-BD)*2 + FX3U-232ADP | FX-232CAB-1 |
| Dサブ9ピン | FX3G，FX3GC | FX3G-232-BD*3 | FX-232CAB-1 |
| Dサブ9ピン | FX3G，FX3GC | FX3G-CNV-ADP*4 + FX3U-232ADP | FX-232CAB-1 |
| Dサブ9ピン | FX3S | FX3G-232-BD | FX-232CAB-1 |
| Dサブ9ピン | FX3S | FX3S-CNV-ADP + FX3U-232ADP | FX-232CAB-1 |
| ハーフピッチ14ピン | FX3U，FX3UC | FX3U-232-BD | FX-232CAB-2 |
| ハーフピッチ14ピン | FX3U，FX3UC | 機能拡張ボード(FX3U-***-BD)*2 + FX3U-232ADP | FX-232CAB-2 |
| ハーフピッチ14ピン | FX3G，FX3GC | FX3G-232-BD*3 | FX-232CAB-2 |
| ハーフピッチ14ピン | FX3G，FX3GC | FX3G-CNV-ADP*4 + FX3U-232ADP | FX-232CAB-2 |
| ハーフピッチ14ピン | FX3S | FX3G-232-BD | FX-232CAB-2 |
| ハーフピッチ14ピン | FX3S | FX3S-CNV-ADP + FX3U-232ADP | FX-232CAB-2 |
| Dサブ25ピン | FX3U，FX3UC | FX3U-232-BD | F2-232CAB-1 |
| Dサブ25ピン | FX3U，FX3UC | 機能拡張ボード(FX3U-***-BD)*2 + FX3U-232ADP | F2-232CAB-1 |
| Dサブ25ピン | FX3G，FX3GC | FX3G-232-BD*3 | F2-232CAB-1 |
| Dサブ25ピン | FX3G，FX3GC | FX3G-CNV-ADP*4 + FX3U-232ADP | F2-232CAB-1 |
| Dサブ25ピン | FX3S | FX3G-232-BD | F2-232CAB-1 |
| Dサブ25ピン | FX3S | FX3S-CNV-ADP + FX3U-232ADP | F2-232CAB-1 |

※RS-232ケーブル列は，原本ではシリーズごとに2行でセルを共有。*1 はDサブ9ピンのFX3U-232-BD行にのみ付く(原本どおり)。

> *1 FX3UCシリーズは，FX3UC-32MT-LT，FX3UC-32MT-LT-2のみ使用可能です。
> *2 機能拡張ボード(FX3U-***-BD)の***には，232，485，422，USB，CNV，8AVが入ります。
> 機能拡張ボード(FX3U-***-BD)は，FX3UC(D，DS，DSS)シリーズには不要です。
> なお，FX3U-485-BDについては，シリアルコミュニケーション通信も行えます。シリアルコミュニケーション通信時の設定については，下記を参照してください。
> ☞78ページ FX拡張ポート
> *3 FX3GCシリーズは，使用できません。
> *4 FX3Uアダプタ接続用ADP(FX3G-CNV-ADP)は，FX3GCシリーズには不要です。

> **Point**
> - PCパラメータについて
>   GX Works2で，PCパラメータの[PCシステム設定(2)]タブの"通信設定をする"にチェックを入れると，このポートによるCPUユニットとの通信ができなくなります。この場合は，CPUユニット内蔵のプログラミングポートよりこの設定をはずした設定を書き込んでください。
>   PCパラメータの設定方法については，下記を参照してください。
>   📖GX Works2 Version 1 オペレーティングマニュアル (共通編)

### CPU USB通信 (2.5 / 39 / 原本 p.41)

使用可能なUSBケーブルを示します。

| 製品名 | 形名 |
|---|---|
| USBケーブル(USB Aタイプ―USB Bタイプ) | AU230 |
| USBケーブル(USB Aタイプ―USB miniBタイプ) | KU-AMB530 |
| USBケーブル(USB Aタイプ―USB miniBタイプ) | U2C-M30BK |
| USBケーブル(USB Aタイプ―USB miniBタイプ) | MR-J3USBCBL3M |
| USBケーブル(USB Aタイプ―USB miniBタイプ) | GT09-C30USB-5P |

> **Point**
> - USBケーブルを初めて使用する場合
>   USBドライバをインストールしてください。インストール方法は，下記を参照してください。
>   ☞669ページ USBドライバのインストール
> - 注意事項・制約事項について
>   CPUユニットにアクセスする場合の注意事項・制約事項については，下記を参照してください。
>   ☞674ページ CPUユニット関連

### MELSECNET/H通信 (2.5 / 39 / 原本 p.41)

- MELSECNET/H ボードが使用できます。
- 通信ドライバは，SW0DNC-MNETH-B以降を使用してください。
  その他の通信ドライバは使用できません。
- 通信に使用するネットワークボードの対応OSの詳細は，各ネットワークボードのマニュアルを参照してください。

### CC-Link IEコントローラネットワーク通信 (2.5 / 39 / 原本 p.41)

- CC-Link IEコントローラネットワークボードが使用できます。
- 通信ドライバは，SW1DNC-MNETG-B以降を使用してください。
  その他の通信ドライバは使用できません。
- 通信に使用するネットワークボードの対応OSの詳細は，各ネットワークボードのマニュアルを参照してください。

### CC-Link IEフィールドネットワーク通信 (2.5 / 39 / 原本 p.41)

- CC-Link IEフィールドネットワークボードが使用できます。
- 通信ドライバは，SW1DNC-CCIEF-B以降を使用してください。
  その他の通信ドライバは使用できません。
- 通信に使用するネットワークボードの対応OSの詳細は，各ネットワークボードのマニュアルを参照してください。

### CC-Link IE TSN通信 (2.5 / 39 / 原本 p.41)

- CC-Link IE TSNボードが使用できます。
- 通信ドライバは，SW1DNN-CCIETBDM-B以降を使用してください。
  その他の通信ドライバは使用できません。
- 通信に使用するネットワークボードの対応OSの詳細は，各ネットワークボードのマニュアルを参照してください。

### CC-Link通信 (2.5 / 39 / 原本 p.41)

- CC-Link Ver.2 ボードが使用できます。
- 通信ドライバは，SW1DNC-CCBD2-B以降を使用してください。
  その他の通信ドライバは使用できません。
- 通信に使用するネットワークボードの対応OSの詳細は，各ネットワークボードのマニュアルを参照してください。
- CC-Linkマスタ局のユニットは，ソフトウェアバージョン"N"以降を使用してください。
  "M"以前のソフトウェアバージョンのユニットでは，正常に動作しません。

### CC-Linkシステム RS-232インタフェース通信 (2.5 / 40 / 原本 p.42)

- CC-Linkマスタ局のユニットは，ソフトウェアバージョン"N"以降を使用してください。
  "M"以前のソフトウェアバージョンのユニットでは，正常に動作しません。
- AJ65BT-R2Nユニットとの接続の詳細は，CC-LinkシステムRS-232インタフェースユニットのユーザーズマニュアルを参照してください。

### GX Simulator2通信 (2.5 / 40 / 原本 p.42)

GX Simulator2通信を行う場合は，GX Works2が必要です。

### GX Simulator3通信 (2.5 / 40 / 原本 p.42)

GX Simulator3通信を行う場合は，GX Works3が必要です。

### MT Simulator2通信 (2.5 / 40 / 原本 p.42)

MT Simulator2通信を行う場合は，MT Developer2が必要です。
QモーションCPUの場合のみ本機能に対応しています。

#### MT Simulator2通信時の注意事項 (2.5 / 40 / 原本 p.42)

MX Componentをインストール後に，MT Developer2をインストールしてください。

### MELSOFT Mirror 通信 (2.5 / 40 / 原本 p.42)

MELSOFT Mirror通信を行う場合は，バージョン1.001B以降のMELSOFT Mirrorが必要です。

### GOTゲートウェイデバイス通信 (2.5 / 40 / 原本 p.42)

ゲートウェイ機能に対応しているGOTおよび設定の詳細は，ご使用になるGOTのマニュアルを参照してください。

### GOTトランスペアレント通信 (2.5 / 40 / 原本 p.42)

接続および設定の詳細は，下記を参照してください。
📖使用するGOTの各接続マニュアル

### インバータ(COM/USB)通信 (2.5 / 40 / 原本 p.42)

使用可能なケーブルは，ご使用になるインバータのマニュアルを参照してください。

### ロボットコントローラ(COM/USB/Ethernet)通信 (2.5 / 40 / 原本 p.42)

使用可能なケーブルは，下記を参照してください。
📖CR750/700/500シリーズRT ToolBox2/RT ToolBox2 mini取扱説明書

#### ロボットコントローラをUSBで接続する場合の注意事項 (2.5 / 40 / 原本 p.42)

ロボットコントローラをUSBで接続する場合の注意事項は下記を参照してください。
📖CR750/700/500シリーズRT ToolBox2/RT ToolBox2 mini取扱説明書

ロボットコントローラをUSBで接続した場合，ロボットコントローラが使用できない状態でもコントロールのOpenメソッドではエラーが発生しません。
Openを実行後に使用するメソッドでエラーコード106(接続が切断された)が発生した場合は，Closeを実行後，再度Openを実行してください。

#### 多重通信について (2.5 / 40 / 原本 p.42)

1台のロボットコントローラに対して多重通信は行わないでください。
