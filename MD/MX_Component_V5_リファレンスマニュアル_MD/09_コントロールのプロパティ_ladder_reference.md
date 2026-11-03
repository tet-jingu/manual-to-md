# MX Component Version 5 リファレンスマニュアル 9章 コントロールのプロパティ (9 / 原本 p.178-191)

| 項目 | 内容 |
|---|---|
| 原本 | 【三菱】MX Component Version 5 リファレンスマニュアル (SH-082394J) |
| メーカー | 三菱電機 |
| 原本ファイル | `PDF/【三菱】MX Component Version 5 リファレンスマニュアル_sh082394j.pdf` (全696ページ) |
| 本ファイルの範囲 | 9章 コントロールのプロパティ (印刷ページ 176-189 / PDF p.178-191) |
| 出典表記 | `(節 / 印刷ページ / 原本 p.PDFページ)` |
| 作成日 | 2026-11-03 |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。
> 本文中の「○ページ」はすべて原本の**印刷ページ番号**です(PDFページ = 印刷ページ + 2)。
> 原本で複数行が1セルを共有している表(ActCpuTypeの説明、ActUnitTypeの値など)は、引きやすいよう各行に値を展開し、その旨を表の下に注記しています。

## 主要用語 対訳表 (Glossary)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| プロパティ | Property | — | 参考訳 |
| デフォルト値 | Default value | — | 参考訳 |
| プロパティ値(プロパティウィンドウ入力値) | Property value (Properties window input value) | — | 参考訳 |
| 論理局番 | Logical station number | ActLogicalStationNumber | 参考訳 |
| パスワードロック | Password lock | ActPassword | 参考訳 |
| ユニットのシリーズ | Unit series | ActMxUnitSeries | 参考訳 |
| ネットワーク番号 | Network number | ActNetworkNumber | 参考訳 |
| 局番号 / 局番 | Station number | ActStationNumber | 参考訳 |
| ユニット番号 | Unit number | ActUnitNumber / ActConnectUnitNumber | 参考訳 |
| ユニットI/O番号 / 実入出力No. | Unit I/O number / Actual I/O number | ActIONumber / ActDestinationIONumber | 参考訳 |
| CPUタイプ | CPU type | ActCpuType (CPU_xxx) | 参考訳 |
| 接続ポート番号 | Connection port number | ActPortNumber (PORT_n) | 参考訳 |
| 伝送速度 | Baud rate | ActBaudRate (BAUDRATE_xxx) | 参考訳 |
| データビット / パリティ / ストップビット | Data bits / Parity / Stop bits | ActDataBits / ActParity / ActStopBits | 参考訳 |
| 信号線の制御設定 | Signal line control setting | ActControl (TRC_xxx) | 参考訳 |
| 接続ホスト名(IPアドレス) | Host name (IP address) | ActHostAddress | 参考訳 |
| CPU監視タイマ | CPU watchdog timer | ActCpuTimeOut | 参考訳 |
| タイムアウト値 | Timeout value | ActTimeOut | 参考訳 |
| サムチェック | Sum check | ActSumCheck | 参考訳 |
| 要求元ネットワーク番号 / 要求元局番 | Source network number / Source station number | ActSourceNetworkNumber / ActSourceStationNumber | 参考訳 |
| 対象先ポート番号 / 中継先ポート番号 | Destination port number / Relay port number | ActDestinationPortNumber | 参考訳 |
| マルチドロップ接続 / マルチドロップリンク | Multidrop connection / Multidrop link | — | 参考訳 |
| マルチドロップ接続チャネルNo. | Multidrop channel number | ActMultiDropChannelNumber | 参考訳 |
| 経由ネットワーク | Relay network | ActThroughNetworkType | 参考訳 |
| CR/LFの有無 | CR/LF setting | ActPacketType (CRLF_xxx) | 参考訳 |
| 接続先シミュレータ | Target simulator | ActTargetSimulator | 参考訳 |
| ユニットタイプ | Unit type | ActUnitType (UNIT_xxx) | 参考訳 |
| 通信プロトコルタイプ | Communication protocol type | ActProtocolType (PROTOCOL_xxx) | 参考訳 |
| システムID / スロットNo. | System ID / Slot No. | ActMirrorSystemID / ActMirrorSlotNumber | 参考訳 |
| ユーザ認証機能 | User authentication function | ActUserAuthenticationUserName / Password | 参考訳 |
| 局番↔IP関連情報設定方式 / 自動応答方式 | Station No.↔IP information setting / Automatic response system | — | 参考訳 |
| 文字コード変換エラー | Character code conversion error | 0xF1000001 | 参考訳 |
| モデム通信用プロパティ | Properties for modem communication | ActATCommand 等 | 参考訳 |
| 自ボードアクセス | Own board access | CPU_BOARD | 参考訳 |

## 変換範囲表

| 原本ページ(PDF) | 印刷ページ | 節 | 扱い |
|---|---|---|---|
| p.178-179 | 176-177 | 9章冒頭 / 9.1 プロパティ一覧 | 全文 |
| p.180-191 | 178-189 | 9.2 プロパティの詳細 | 全文(p.190は脚注*1のみのページ) |
| p.1-17 | — | 前付け | **未変換** |
| p.18-177 | 16-175 | 1章〜8章 | 別ファイル(01_〜08b_) |
| p.192-696 | 190- | 10章〜13章・付録ほか | **未変換** |

## 目次

- 9.1 プロパティ一覧
- 9.2 プロパティの詳細
  - ユーティリティ設定タイプのコントロールのプロパティ: ActLogicalStationNumber / ActPassword
  - プログラム設定タイプのコントロールのプロパティ: ActMxUnitSeries / ActNetworkNumber / ActStationNumber / ActUnitNumber / ActConnectUnitNumber / ActIONumber / ActCpuType / ActPortNumber / ActBaudRate / ActDataBits / ActParity / ActStopBits / ActControl / ActHostAddress / ActCpuTimeOut / ActTimeOut / ActSumCheck / ActSourceNetworkNumber / ActSourceStationNumber / ActDestinationPortNumber / ActDestinationIONumber / ActMultiDropChannelNumber / ActThroughNetworkType / ActIntelligentPreferenceBit / ActDidPropertyBit / ActDsidPropertyBit / ActPacketType / ActPassword / ActTargetSimulator / ActUnitType / ActProtocolType / ActMirrorURL / ActMirrorSystemID / ActMirrorSlotNumber / ActUserAuthenticationUserName / ActUserAuthenticationPassword / モデム通信用(互換)プロパティ17種
  - ActCpuType(LONG): ActMxUnitSeries=0(シーケンサ/モーションコントローラ) / =1(インバータ) / =2(ロボット)
  - ActPortNumber(LONG) / ActControl(LONG) / ActUnitType(LONG) / ActProtocolType(LONG)

---

## 9 コントロールのプロパティ (9 / 176 / 原本 p.178)

コントロールが保有するプロパティ一覧，およびそれぞれのプロパティの詳細について説明します。

## 9.1 プロパティ一覧 (9.1 / 176-177 / 原本 p.178-179)

各コントロールが保有するプロパティを下記に示します。

| コントロール名 | 対象コントロール | プロパティ名 | 原本ページ |
|---|---|---|---|
| ACT Control | ActUtlType<br>ActUtlType64<br>ActUtlDataLogging*1*2<br>ActUtlDataLogging64*1*2 | ActLogicalStationNumber | p.178 |
| ACT Control | ActUtlType<br>ActUtlType64<br>ActUtlDataLogging*1*2<br>ActUtlDataLogging64*1*2 | ActPassword | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActBaudRate | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActConnectUnitNumber | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActControl | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActCpuTimeOut | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActCpuType | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActDataBits | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActDestinationIONumber | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActDestinationPortNumber | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActDidPropertyBit | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActDsidPropertyBit | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActHostAddress | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActIntelligentPreferenceBit | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActIONumber | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActMirrorSlotNumber | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActMirrorSystemID | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActMirrorURL | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActMultiDropChannelNumber | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActMxUnitSeries*3 | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActNetworkNumber | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActPacketType | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActParity | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActPassword | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActPortNumber | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActProtocolType | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActSourceNetworkNumber | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActSourceStationNumber | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActStationNumber | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActStopBits | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActSumCheck | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActTargetSimulator | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActThroughNetworkType | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActTimeOut | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActUnitNumber | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActUnitType | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActUserAuthenticationUserName | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActUserAuthenticationPassword | p.178 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActATCommand*4 | p.179 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActATCommandPasswordCancelRetryTimes*4 | p.179 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActATCommandResponseWaitTime*4 | p.179 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActCallbackCancelWaitTime*4 | p.179 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActCallbackDelayTime*4 | p.179 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActCallbackNumber*4 | p.179 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActCallbackReceptionWaitingTimeOut*4 | p.179 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActConnectionCDWaitTime*4 | p.179 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActConnectionModemReportWaitTime*4 | p.179 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActConnectWay*4 | p.179 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActDialNumber*4 | p.179 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActDisconnectionCDWaitTime*4 | p.179 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActDisconnectionDelayTime*4 | p.179 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActLineType*4 | p.179 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActOutsideLineNumber*4 | p.179 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActPasswordCancelResponseWaitTime*4 | p.179 |
| ACT Control | ActProgType<br>ActProgType64<br>ActProgDataLogging*1*2<br>ActProgDataLogging64*1*2 | ActTransmissionDelayTime*4 | p.179 |
| ACT Control | ActSupportMsg<br>ActSupportMsg64 | — | p.179 |
| .NET Control | DotUtlType<br>DotUtlType64 | ActLogicalStationNumber | p.179 |
| .NET Control | DotUtlType<br>DotUtlType64 | ActPassword | p.179 |
| .NET Control | DotSupportMsg<br>DotSupportMsg64 | — | p.179 |

> *1 RCPUのみ対応しています。
> *2 GX Simulator3には対応していません。
> *3 プロパティ値は自動で設定され，変更できません。
> *4 モデム通信用プロパティです。MX Component Version 4からの互換性のためのプロパティになります。MX Component Version 5以降で使用することはできません。

※原本の表は「ACT Control」の大枠の中に3つのコントロール群(ActUtlType群 / ActProgType群 / ActSupportMsg群)、「.NET Control」の大枠の中に2群(DotUtlType群 / DotSupportMsg群)があり、各群が保有するプロパティを右列に並べている。ActProgType群はp.178に35個、p.179に*4付きの17個が続く(同一群)。本mdでは1行1プロパティに展開した。ActPassword はActProgType群の中にも1行ある(原本どおり)。

---

## 9.2 プロパティの詳細 (9.2 / 178-189 / 原本 p.180-191)

ユーザプログラムを作成する際に設定するプロパティの詳細を下記に示します。

### ユーティリティ設定タイプのコントロールのプロパティ (9.2 / 178 / 原本 p.180)

ActUtlTypeコントロールおよびDotUtlTypeコントロールのプロパティを下記に示します。

| プロパティ名(型) | 内容 | デフォルト値 |
|---|---|---|
| ActLogicalStationNumber(LONG) | 通信設定ユーティリティにて設定した論理局番です。(設定可能範囲: 0～1023) | 0(0x00) |
| ActPassword(BSTR) | パスワードロック可能なユニットに設定されたパスワードロックを解除するために，パスワードを指定します。*1<br>パスワードロック可能なユニットを使用しない場合は無視されます。 | あき |

> *1 パスワードの最大文字数を超えて入力した文字は無視されます。
> 英数字以外の文字を指定した場合は，Open時に文字コード変換エラー (0xF1000001)となります。

### プログラム設定タイプのコントロールのプロパティ (9.2 / 178-182 / 原本 p.180-184)

ActProgTypeコントロールのプロパティを下記に示します。

| プロパティ名(型) | 内容 | デフォルト値 |
|---|---|---|
| ActMxUnitSeries(LONG) | 接続対象となるユニットのシリーズを指定します。<br>プロパティ値は自動で設定され，変更できません。<br>■プロパティ値<br>0(0x00): シーケンサ/モーションコントローラ/GOT指定<br>1(0x01): インバータ指定<br>2(0x02): ロボットコントローラ指定 | 0(0x00) |
| ActNetworkNumber(LONG) | MELSECNET/Hでのネットワーク番号を指定します。(自局指定時は"0"(0x00)を指定)<br>マルチドロップ接続(Qシリーズ対応C24経由)時に指定した場合は下記のとおりです。<br>■ActIntelligentPreferenceBitのプロパティ値<br>0(0x00): 自ネットワーク指定<br>1(0x01): マルチドロップ先の他ネットワーク指定 | 0(0x00) |
| ActStationNumber(LONG) | MELSECNET/H，CC-Linkでの局番号を指定します。(自局指定時は"255"(0xFF)を指定)<br>GX Simulator3におけるシステム番号を指定します。<br>マルチドロップ接続(Qシリーズ対応C24経由)時に指定した場合は下記のとおりです。<br>■ActIntelligentPreferenceBitのプロパティ値<br>0(0x00): 自ネットワーク指定<br>1(0x01): マルチドロップ先の他ネットワーク指定<br>インバータ通信時は，接続するインバータの局番(0～31)を指定します。 | 255(0xFF) |
| ActUnitNumber(LONG) | シリアルコミュニケーションユニットのユニット番号およびQシリーズ対応のインテリジェント機能ユニット対象時の局番を指定します。<br>シリアルコミュニケーション通信およびQシリーズ対応のインテリジェント機能ユニットを対象としていない場合は無効です。<br>マルチドロップリンク時は対象先のシリアルコミュニケーションユニットのユニット番号を指定します。 | 0(0x00) |
| ActConnectUnitNumber(LONG) | シリアルコミュニケーションユニット，Qシリーズ対応E71のユニット番号を指定します。<br>マルチドロップリンク時は，要求元のシリアルコミュニケーションユニットのユニット番号を指定します。<br>ただし，CPU COM通信経由のマルチドロップリンクの場合，要求元局のユニット番号は不要です。("0"(0x00)を指定)<br>マルチドロップリンク以外の場合は，"0"(0x00)を指定します。<br>Qシリーズ対応E71の場合は，中継先局番を指定します。(自ネットワーク内アクセスの場合は"0"(0x00)固定)<br>MELSECNET/10経由で他のネットワークへアクセスする場合は，接続Ethernetユニットのパラメータで設定した局番を指定します。 | 0(0x00) |
| ActIONumber(LONG) | ユニットI/O番号を指定します。<br>マルチドロップリンクおよびインテリジェント機能ユニットアクセス時は，対象となるシリアルコミュニケーションユニットおよびインテリジェント機能ユニットの実入出力No.(先頭入出力番号÷16)を指定します。(マルチドロップリンク時は，経由する局，要求元局のI/O番号を指定)<br>自局CPUやネットワーク経由で他局へアクセスする場合は，"992"(0x3E0)～"1023"(0x3FF)を指定します。 | 1023(0x3FF) |
| ActCpuType(LONG) | **ActMxUnitSeriesプロパティが0(シーケンサ/モーションコントローラ)の場合**<br>通信を行う対象CPUを指定します。<br>パラメータには，下記のCPUタイプを指定します。<br>☞183ページ ActCpuType(LONG): ActMxUnitSeriesプロパティが0(シーケンサ/モーションコントローラ)の場合 | 34(CPU_Q02CPU) |
| ActCpuType(LONG) | **ActMxUnitSeriesプロパティが1(インバータ)の場合**<br>通信を行う対象インバータを指定します。<br>パラメータには，下記のCPUタイプを指定します。<br>☞184ページ ActCpuType(LONG): ActMxUnitSeriesプロパティが1(インバータ)の場合 | 34(CPU_Q02CPU) |
| ActCpuType(LONG) | **ActMxUnitSeriesプロパティが2(ロボット)の場合**<br>通信を行う対象ロボットを指定します。<br>パラメータには，下記のCPUタイプを指定します。<br>☞185ページ ActCpuType(LONG): ActMxUnitSeriesプロパティが2(ロボット)の場合 | 34(CPU_Q02CPU) |
| ActPortNumber(LONG) | パソコンの接続ポート番号を指定します。<br>Ethernetユニット接続時は，要求元(パソコン)のポート番号として任意値を設定します。<br>ポート番号として"=0"を指定した場合，局番↔IP関連情報設定方式は自動応答方式となります。(自動応答方式以外を選択時は，固定値"5001"を設定)<br>Ethernet通信のTCP/IP経由で通信時，ポート番号に"0"以外を指定すると，Close関数実行直後にOpen関数の実行に失敗します。Close関数実行後にOpen関数が正常終了しない場合は，時間をおいてから再度Open関数を実行する，またはポート番号に"0"(ポート番号の自動割り当て)を設定してください。<br>また，ネットワークボード使用時は，ボード1枚目をPORT_1，2枚目以降はPORT_2，PORT_3･･･の順に指定します。<br>☞186ページ ActPortNumber(LONG) | 1(PORT_1) |
| ActBaudRate(LONG) | シリアルコミュニケーション通信時の伝送速度を指定します。<br>■プロパティ値(プロパティウィンドウ入力値)<br>BAUDRATE_300 (300): 300bps<br>BAUDRATE_600 (600): 600bps<br>BAUDRATE_1200 (1200): 1200bps<br>BAUDRATE_2400 (2400): 2400bps<br>BAUDRATE_4800 (4800): 4800bps<br>BAUDRATE_9600 (9600): 9600bps<br>BAUDRATE_19200 (19200): 19200bps<br>BAUDRATE_38400 (38400): 38400bps<br>BAUDRATE_57600 (57600): 57600bps<br>BAUDRATE_115200 (115200): 115200bps<br>インバータ通信時は，BAUDRATE_4800 (4800)以上を指定します。 | 19200(BAUDRATE_19200) |
| ActDataBits(LONG) | シリアルコミュニケーション通信時の送信および受信されるバイトデータのビット数を指定します。<br>■プロパティ値(プロパティウィンドウ入力値)<br>DATABIT_7 (7): 7ビット<br>DATABIT_8 (8): 8ビット<br>ロボットコントローラの場合，文字サイズを指定します。 | 8(DATABIT_8) |
| ActParity(LONG) | シリアルコミュニケーション通信時に使われるパリティ方式を指定します。<br>■プロパティ値(プロパティウィンドウ入力値)<br>NO_PARITY (0): パリティなし<br>ODD_PARITY (1): 奇数<br>EVEN_PARITY (2): 偶数 | 1(ODD_PARITY) |
| ActStopBits(LONG) | シリアルコミュニケーション通信時に使われるストップビットの数を指定します。<br>■プロパティ値(プロパティウィンドウ入力値)<br>STOPBIT_ONE (0): 1ストップビット<br>STOPBITS_TWO (2): 2ストップビット<br>ロボットコントローラの場合，下記のストップビットの数を指定します。<br>■プロパティ値(プロパティウィンドウ入力値)<br>ONESTOPBIT(0): 1ストップビット<br>ONE5STOPBITS(1): 1.5ストップビット<br>TWOSTOPBITS(2): 2ストップビット | 0(STOPBIT_ONE) |
| ActControl(LONG) | 信号線の制御設定を指定します。<br>☞186ページ ActControl(LONG) | 8(TRC_DTR_OR_RTS) |
| ActHostAddress(BSTR) | Ethernet通信時の接続ホスト名(IPアドレス)文字列を示すポインタです。<br>各オクテットの先頭を0に設定すると，その値は8進数として処理されます。 | 1.1.1.1 |
| ActCpuTimeOut(LONG) | Ethernet通信時のCPU監視タイマを指定します。(単位は"×250ms")<br>FXCPU/インバータの場合，シリアルコミュニケーション通信時の送信待ち時間を指定します。(単位は"×10ms")<br>ロボットコントローラの場合，送信時のタイムアウト時間を指定します。(1000～30000ms) | 0(0x00) |
| ActTimeOut(LONG) | パソコンとシーケンサ/インバータ間の，通信のタイムアウト値を設定します。(単位は"ms")<br>ロボットコントローラの場合，受信時のタイムアウト時間を指定します。(5000～120000ms)<br>MX Componentでは，通信経路によりタイムアウト処理を内部処理で行う場合があります。<br>詳細については下記を参照してください。<br>☞673ページ タイムアウト時間について<br>■注意事項<br>一時的な断線などが原因でMX Componentにて設定したタイムアウト時間の間，コントロールやシーケンサモニタユーティリティが応答待ちになる場合があります。<br>タイムアウトエラーが発生するように，適切なタイムアウト時間を設定してください。 | 10000 |
| ActSumCheck(LONG) | サムチェックの有無を指定します。<br>シリアルコミュニケーションユニットのみ有効です。<br>■プロパティ値(プロパティウィンドウ入力値)<br>NO_SUM_CHECK (0): サムチェックなし<br>SUM_CHECK (1): サムチェックあり | 0(NO_SUM_CHECK) |
| ActSourceNetworkNumber(LONG) | Ethernetユニット指定時の要求元ネットワーク番号を指定します。<br>接続しているEthernetと同じネットワークNo.(ネットワークパラメータで指定するネットワークNo.)を指定します。 | 0(0x00) |
| ActSourceStationNumber(LONG) | Ethernetユニット指定時の要求元局番(パソコン側局番)を指定します。<br>Ethernet同一ループ内で設定したEthernetユニットの局番と重複しないように設定します。 | 0(0x00) |
| ActDestinationPortNumber(LONG) | Ethernet通信指定時に対象先のポート番号を指定します。<br>ほかのネットワークへのアクセス時は，中継先ポート番号を指定します。<br>自動応答方式以外は下表の設定とします。<br>■設定<br>MELSEC iQ-Rシリーズ対応E71(TCP/IP) - MELSOFT接続: "5002"固定<br>MELSEC iQ-Rシリーズ対応E71(TCP/IP) - OPS接続: ネットワークパラメータによる<br>MELSEC iQ-Rシリーズ対応E71(UDP/IP): "5001"固定<br>Qシリーズ対応E71(TCP/IP) - 二重化CPU以外: "5002"固定<br>Qシリーズ対応E71(TCP/IP) - MELSOFT接続*1: "5002"固定<br>Qシリーズ対応E71(TCP/IP) - OPS接続*1: ネットワークパラメータによる<br>Qシリーズ対応E71(UDP/IP): "5001"固定 | 0(0x00) |
| ActDestinationIONumber(LONG) | マルチドロップ接続(MELSEC iQ-Rシリーズ対応C24・Qシリーズ対応C24・Lシリーズ対応C24・CC-Link経由)時，最終アクセス対象局の実入出力No.(先頭入出力÷16)を指定します。(対象がインテリジェント機能ユニットの場合)<br>自局CPUやネットワーク経由で他局へアクセスする場合は，"992"(0x3E0)～"1023"(0x3FF)を指定します。 | 0(0x00) |
| ActMultiDropChannelNumber(LONG) | マルチドロップ接続(MELSEC iQ-Rシリーズ対応C24・Qシリーズ対応C24・Lシリーズ対応C24・CC-Link経由)時，マルチドロップ接続チャネルNo.(CH1/CH2)を指定します。<br>ロボットコントローラの場合，通信エラー時のリトライ回数を指定します。(0～10回)<br>他の接続時は無効です。 | 0(0x00) |
| ActThroughNetworkType(LONG) | ネットワークを経由して他局にアクセスする場合，経由ネットワークにMELSECNET/10が含まれているかどうかを指定します。<br>■プロパティ値<br>0(0x00): MELSECNET/10を含んでいません。<br>1(0x01): MELSECNET/10を含んでいます。<br>ロボットコントローラの場合，使用プロトコル(通信方法)を指定します。(有手順(0)/無手順(1)) | 0(0x00) |
| ActIntelligentPreferenceBit(LONG) | マルチドロップ接続(MELSEC iQ-Rシリーズ対応C24・Qシリーズ対応C24・Lシリーズ対応C24・CC-Link経由)時，マルチドロップリンク先のネットワークを経由するかどうかを指定します。(自ネットワークユニットを区別するため)<br>■プロパティ値<br>0(0x00): マルチドロップ先の他のネットワークにアクセスしません。<br>1(0x01): マルチドロップ先の他のネットワークにアクセスします。 | 0(0x00) |
| ActDidPropertyBit(LONG) | Qシリーズ対応の自局インテリジェント機能ユニット(自局CPUに装着されているインテリジェント機能ユニット)にアクセス時，下記設定を無効にすることで"ActUnitNumber"を指定する必要がなくなります。(ユニットI/O番号"ActIONumber"のみで指定)<br>■プロパティ値<br>0(0x00): ユニット番号を有効にします。<br>1(0x01): ユニット番号を無効にします。 | 1(0x01) |
| ActDsidPropertyBit(LONG) | マルチドロップ接続(MELSEC iQ-Rシリーズ対応C24・Qシリーズ対応C24・Lシリーズ対応C24・CC-Link経由)時，下記設定を無効にすることで"ActDestinationIONumber"を指定する必要がなくなります。<br>ただし，下記設定を無効とする場合は"ActDidPropertyBit"は必ず有効にします。("ActUnitNumber"で指定)<br>■プロパティ値<br>0(0x00): 最終アクセス対象局のI/O番号を有効にします。<br>1(0x01): 最終アクセス対象局のI/O番号を無効にします。 | 1(0x01) |
| ActPacketType(LONG) | CR/LFの有無を設定します。<br>■プロパティ値(プロパティウィンドウ入力値)<br>CRLF_NONE (0): CR/LFなし<br>CRLF_CR (1): CRのみあり<br>CRLF_CRLF (2): CR/LFあり | 1(CRLF_CR) |
| ActPassword(BSTR)*2 | パスワードロック可能なユニットに設定されたパスワードロックを解除するために，パスワードを指定します。*3*4*5<br>パスワードロック可能なユニットを使用しない場合は無視されます。 | あき |
| ActTargetSimulator(LONG) | 起動中の接続先GX Simulator2を指定します。<br>FXCPUを接続する場合は，"0"(0x00)を指定します。<br>■プロパティ値<br>0(0x00): 指定なし<br>(起動中のシミュレータが1台の場合は，起動中のシミュレータに接続。複数の場合は，A，B，C，Dの順で起動中のシミュレータを探し，接続。)<br>1(0x01): シミュレータA<br>2(0x02): シミュレータB<br>3(0x03): シミュレータC<br>4(0x04): シミュレータD | 0(0x00) |
| ActTargetSimulator(LONG) | 起動中の接続先GX Simulator3の号機番号を指定します。 | 0(0x00) |
| ActTargetSimulator(LONG) | 起動中の接続先MT Simulator2を指定します。<br>■プロパティ値<br>2(0x02): シミュレータ2号機<br>3(0x03): シミュレータ3号機<br>4(0x04): シミュレータ4号機 | 0(0x00) |
| ActUnitType(LONG) | 物理ポートと接続しているユニットタイプを指定します。<br>☞186ページ ActUnitType(LONG) | 0x13(UNIT_QNCPU) |
| ActProtocolType(LONG) | 接続するユニット(ボード)の通信プロトコルタイプを指定します。<br>☞189ページ ActProtocolType(LONG) | 0x04(PROTOCOL_SERIAL) |
| ActMirrorURL(BSTR) | 接続するMELSOFT MirrorのURLを指定します。 | あき |
| ActMirrorSystemID(LONG) | 接続するMELSOFT MirrorのシステムID.を指定します。 | 1(0x01) |
| ActMirrorSlotNumber(LONG) | 接続するMELSOFT MirrorのスロットNo.を指定します。<br>■プロパティ値<br>0(0x00): CPU<br>1(0x01): I/O 0<br>2(0x02): I/O 1<br>3(0x03): I/O 2<br>4(0x04): I/O 3<br>5(0x05): I/O 4<br>6(0x06): I/O 5<br>7(0x07): I/O 6 | 0(0x00) |
| ActUserAuthenticationUserName (BSTR)*6 | MXコントローラのユーザ認証機能で作成したユーザ名を指定します。*4*7<br>ユーザ認証機能を使用しない場合は無視されます。 | あき |
| ActUserAuthenticationPassword (BSTR)*6 | MXコントローラのユーザ認証機能で作成したユーザ名に対するパスワードを指定します。*4*7<br>ユーザ認証機能を使用しない場合は無視されます。 | あき |
| ActATCommand | MX Component Version 4からの互換性のためのプロパティになります。MX Component Version 5以降で使用することはできません。 | — |
| ActATCommandPasswordCancelRetryTimes | (同上) | — |
| ActATCommandResponseWaitTime | (同上) | — |
| ActCallbackCancelWaitTime | (同上) | — |
| ActCallbackDelayTime | (同上) | — |
| ActCallbackNumber | (同上) | — |
| ActCallbackReceptionWaitingTimeOut | (同上) | — |
| ActConnectionCDWaitTime | (同上) | — |
| ActConnectionModemReportWaitTime | (同上) | — |
| ActConnectWay | (同上) | — |
| ActDialNumber | (同上) | — |
| ActDisconnectionCDWaitTime | (同上) | — |
| ActDisconnectionDelayTime | (同上) | — |
| ActLineType | (同上) | — |
| ActOutsideLineNumber | (同上) | — |
| ActPasswordCancelResponseWaitTime | (同上) | — |
| ActTransmissionDelayTime | (同上) | — |

※ActATCommand〜ActTransmissionDelayTimeの17行(原本 p.184)は，原本では内容欄・デフォルト値欄を全行で共有している(「(同上)」と表記)。原本ではプロパティ名に"(型)"の記載が無い。
※原本では ActCpuType の3つの説明セルと ActTargetSimulator の3つの説明セルはそれぞれデフォルト値セルを共有している(各行に同じ値を展開)。ActUserAuthenticationUserName / Password のデフォルト値「あき」も2行で共有。表は原本ではp.180〜p.182の3ページにまたがる1つの表。

> *1 詳細については下記のマニュアルを参照してください。
> 📖Q対応Ethernetインタフェースユニットユーザーズマニュアル(基本編)
> *2 Ethernet通信を行う場合に使用できます。
> *3 パスワードが設定されていない場合，当該プロパティは設定不要です。
> *4 最大文字数を超えて入力した文字は無視されます。
> *5 英数字以外の文字を指定した場合は，Open時に文字コード変換エラー (0xF1000001)となります。
> *6 データの登録のみ実行できます。データの取得は実行できません。
> *7 ユーザ認証機能を使用しない場合，当該プロパティは設定不要です。

### ActCpuType(LONG): ActMxUnitSeriesプロパティが0(シーケンサ/モーションコントローラ)の場合 (9.2 / 183-184 / 原本 p.185-186)

| CPUタイプ | 10進 | 16進 | 対象CPU |
|---|---|---|---|
| CPU_R00CPU | 4609 | 0x1201 | R00CPU |
| CPU_R01CPU | 4610 | 0x1202 | R01CPU |
| CPU_R02CPU | 4611 | 0x1203 | R02CPU |
| CPU_R04CPU | 4097 | 0x1001 | R04CPU |
| CPU_R04ENCPU | 4104 | 0x1008 | R04ENCPU |
| CPU_R08CPU | 4098 | 0x1002 | R08CPU |
| CPU_R08ENCPU | 4105 | 0x1009 | R08ENCPU |
| CPU_R08PCPU | 4354 | 0x1102 | R08PCPU |
| CPU_R08PSFCPU | 4369 | 0x1111 | R08PSFCPU |
| CPU_R08SFCPU | 4386 | 0x1122 | R08SFCPU |
| CPU_R16CPU | 4099 | 0x1003 | R16CPU |
| CPU_R16ENCPU | 4106 | 0x100A | R16ENCPU |
| CPU_R16PCPU | 4355 | 0x1103 | R16PCPU |
| CPU_R16PSFCPU | 4370 | 0x1112 | R16PSFCPU |
| CPU_R16SFCPU | 4387 | 0x1123 | R16SFCPU |
| CPU_R32CPU | 4100 | 0x1004 | R32CPU |
| CPU_R32ENCPU | 4107 | 0x100B | R32ENCPU |
| CPU_R32PCPU | 4356 | 0x1104 | R32PCPU |
| CPU_R32PSFCPU | 4371 | 0x1113 | R32PSFCPU |
| CPU_R32SFCPU | 4388 | 0x1124 | R32SFCPU |
| CPU_R120CPU | 4101 | 0x1005 | R120CPU |
| CPU_R120ENCPU | 4108 | 0x100C | R120ENCPU |
| CPU_R120PCPU | 4357 | 0x1105 | R120PCPU |
| CPU_R120PSFCPU | 4372 | 0x1114 | R120PSFCPU |
| CPU_R120SFCPU | 4389 | 0x1125 | R120SFCPU |
| CPU_R16MTCPU | 4113 | 0x1011 | R16MTCPU |
| CPU_R32MTCPU | 4114 | 0x1012 | R32MTCPU |
| CPU_R64MTCPU | 4115 | 0x1013 | R64MTCPU |
| CPU_R12CCPU_V | 4129 | 0x1021 | R12CCPU-V |
| CPU_R102WCPU_W | 4136 | 0x1028 | R102WCPU_W |
| CPU_MXR300_16 | 7690 | 0x1E0A | MXR300-16 |
| CPU_MXR300_32 | 7691 | 0x1E0B | MXR300-32 |
| CPU_MXR300_64 | 7692 | 0x1E0C | MXR300-64 |
| CPU_MXR500_128 | 7695 | 0x1E0F | MXR500-128 |
| CPU_MXR500_256 | 7696 | 0x1E10 | MXR500-256 |
| CPU_MXF100_8 | 7731 | 0x1E33 | MXF100-8-N32，MXF100-8-P32 |
| CPU_MXF100_16 | 7732 | 0x1E34 | MXF100-16-N32，MXF100-16-P32 |
| CPU_MXF100_8_EC | 7761 | 0x1E51 | MXF100-8-N32-EC |
| CPU_MXF100_16_EC | 7762 | 0x1E52 | MXF100-16-N32-EC |
| CPU_L04HCPU | 4625 | 0x1211 | L04HCPU |
| CPU_L08HCPU | 4626 | 0x1212 | L08HCPU |
| CPU_L16HCPU | 4627 | 0x1213 | L16HCPU |
| CPU_L32HCPU | 4628 | 0x1214 | L32HCPU |
| CPU_Q00UJCPU | 128 | 0x80 | Q00UJCPU |
| CPU_Q00UCPU | 129 | 0x81 | Q00UCPU |
| CPU_Q01UCPU | 130 | 0x82 | Q01UCPU |
| CPU_Q02UCPU | 131 | 0x83 | Q02UCPU |
| CPU_Q03UDCPU | 112 | 0x70 | Q03UDCPU |
| CPU_Q03UDECPU | 144 | 0x90 | Q03UDECPU |
| CPU_Q03UDVCPU | 209 | 0xD1 | Q03UDVCPU |
| CPU_Q04UDHCPU | 113 | 0x71 | Q04UDHCPU |
| CPU_Q04UDEHCPU | 145 | 0x91 | Q04UDEHCPU |
| CPU_Q04UDVCPU | 210 | 0xD2 | Q04UDVCPU |
| CPU_Q04UDPVCPU | 71 | 0x47 | Q04UDPVCPU |
| CPU_Q06UDHCPU | 114 | 0x72 | Q06UDHCPU |
| CPU_Q06UDEHCPU | 146 | 0x92 | Q06UDEHCPU |
| CPU_Q06UDVCPU | 211 | 0xD3 | Q06UDVCPU |
| CPU_Q06UDPVCPU | 72 | 0x48 | Q06UDPVCPU |
| CPU_Q10UDHCPU | 117 | 0x75 | Q10UDHCPU |
| CPU_Q10UDEHCPU | 149 | 0x95 | Q10UDEHCPU |
| CPU_Q12PRHCPU | 67 | 0x43 | Q12PRHCPU |
| CPU_Q13UDHCPU | 115 | 0x73 | Q13UDHCPU |
| CPU_Q13UDEHCPU | 147 | 0x93 | Q13UDEHCPU |
| CPU_Q13UDVCPU | 212 | 0xD4 | Q13UDVCPU |
| CPU_Q13UDPVCPU | 73 | 0x49 | Q13UDPVCPU |
| CPU_Q20UDHCPU | 118 | 0x76 | Q20UDHCPU |
| CPU_Q20UDEHCPU | 150 | 0x96 | Q20UDEHCPU |
| CPU_Q25PRHCPU | 68 | 0x44 | Q25PRHCPU |
| CPU_Q26UDHCPU | 116 | 0x74 | Q26UDHCPU |
| CPU_Q26UDEHCPU | 148 | 0x94 | Q26UDEHCPU |
| CPU_Q26UDVCPU | 213 | 0xD5 | Q26UDVCPU |
| CPU_Q26UDPVCPU | 74 | 0x4A | Q26UDPVCPU |
| CPU_Q50UDEHCPU | 152 | 0x98 | Q50UDEHCPU |
| CPU_Q100UDEHCPU | 154 | 0x9A | Q100UDEHCPU |
| CPU_L02SCPU | 163 | 0xA3 | L02SCPU |
| CPU_L02CPU | 161 | 0xA1 | L02CPU |
| CPU_L06CPU | 165 | 0xA5 | L06CPU |
| CPU_L26CPU | 164 | 0xA4 | L26CPU |
| CPU_L26CPUBT | 162 | 0xA2 | L26CPU-BT |
| CPU_Q12DC_V | 88 | 0x58 | Q12DCCPU-V |
| CPU_Q24DHC_V | 89 | 0x59 | Q24DHCCPU-V |
| CPU_Q24DHC_LS | 91 | 0x5B | Q24DHCCPU-LS |
| CPU_Q24DHC_VG | 92 | 0x5C | Q24DHCCPU-VG |
| CPU_Q26DHC_LS | 93 | 0x5D | Q26DHCCPU-LS |
| CPU_QS001CPU | 96 | 0x60 | QS001CPU |
| CPU_Q172DCPU | 1573 | 0x625 | Q172DCPU |
| CPU_Q173DCPU | 1574 | 0x626 | Q173DCPU |
| CPU_Q172DSCPU | 1578 | 0x62A | Q172DSCPU |
| CPU_Q173DSCPU | 1579 | 0x62B | Q173DSCPU |
| CPU_FX3SCPU | 522 | 0x20A | FX3SCPU |
| CPU_FX3GCPU | 521 | 0x209 | FX3G(C)CPU |
| CPU_FX3UCCPU | 520 | 0x208 | FX3U(C)CPU |
| CPU_FX5UCPU | 528 | 0x0210 | FX5UCPU |
| CPU_FX5UJCPU | 529 | 0x0211 | FX5UJCPU |
| CPU_FX5SCPU | 530 | 0x0212 | FX5SCPU |
| CPU_BOARD | 1025 | 0x401 | 自ボードアクセス時*1 |

※列見出しは原本では「プロパティ値(プロパティウィンドウ入力値)」の下に CPUタイプ / 10進 / 16進、右に「対象CPU」。全96行(p.185に49行、p.186に47行)。

> *1 CPUボード，AFボードを除きます。

### ActCpuType(LONG): ActMxUnitSeriesプロパティが1(インバータ)の場合 (9.2 / 184 / 原本 p.186)

| CPUタイプ | 10進 | 16進 | 対象インバータ |
|---|---|---|---|
| INV_A800 | 7776 | 0x1E60 | A800 |

### ActCpuType(LONG): ActMxUnitSeriesプロパティが2(ロボット)の場合 (9.2 / 185 / 原本 p.187)

| CPUタイプ | 10進 | 16進 | 対象ロボット |
|---|---|---|---|
| UCPU_CRD700 | 77825 | 0x13001 | CRnD-7xx/CR75x-D |

### ActPortNumber(LONG) (9.2 / 186 / 原本 p.188)

| ポート番号 | 10進 | 16進 | 内容 |
|---|---|---|---|
| PORT_1 | 1 | 0x01 | 通信ポート1 |
| PORT_2 | 2 | 0x02 | 通信ポート2 |
| PORT_3 | 3 | 0x03 | 通信ポート3 |
| PORT_4 | 4 | 0x04 | 通信ポート4 |
| PORT_5 | 5 | 0x05 | 通信ポート5 |
| PORT_6 | 6 | 0x06 | 通信ポート6 |
| PORT_7 | 7 | 0x07 | 通信ポート7 |
| PORT_8 | 8 | 0x08 | 通信ポート8 |
| PORT_9 | 9 | 0x09 | 通信ポート9 |
| PORT_10 | 10 | 0x0A | 通信ポート10 |

### ActControl(LONG) (9.2 / 186 / 原本 p.188)

| 制御設定 | 10進 | 16進 | 内容 |
|---|---|---|---|
| TRC_DTR | 1 | 0x01 | DTR制御 |
| TRC_RTS | 2 | 0x02 | RTS制御 |
| TRC_DRT_AND_RTS | 7 | 0x07 | DTR制御かつRTS制御 |
| TRC_DTR_OR_RTS | 8 | 0x08 | DTR制御またはRTS制御 |

※「TRC_DRT_AND_RTS」は原本表記のまま(DTRのつづりが「DRT」。要確認)。

### ActUnitType(LONG) (9.2 / 186-187 / 原本 p.188-189)

| ユニットタイプ | 接続方法 | 値 |
|---|---|---|
| UNIT_RJ71C24 | MELSEC iQ-Rシリーズ対応C24ユニット直結 | 0x1000 |
| UNIT_RJ71C24 | GOT2000シリーズ経由MELSEC iQ-Rシリーズ対応C24接続 | 0x1000 |
| UNIT_QJ71C24 | Qシリーズ対応C24ユニット直結 | 0x19 |
| UNIT_QJ71C24 | GOT2000シリーズ経由Qシリーズ対応C24接続 | 0x19 |
| UNIT_LJ71C24 | Lシリーズ対応C24ユニット直結 | 0x54 |
| UNIT_LJ71C24 | GOT2000シリーズ経由Lシリーズ対応C24接続 | 0x54 |
| UNIT_FX485BD | FX拡張ポート(RS-485)接続 | 0x24 |
| UNIT_RJ71EN71 | MELSEC iQ-Rシリーズ対応E71経由接続(IP指定) | 0x1001 |
| UNIT_RJ71EN71_DIRECT | MELSEC iQ-Rシリーズ対応E71経由接続(直結) | 0x1005 |
| UNIT_QJ71E71 | Qシリーズ対応E71 Ethernetポート接続/直結 | 0x1A |
| UNIT_LJ71E71 | Lシリーズ対応E71ユニット接続 | 0x5C |
| UNIT_RETHER | RCPU Ethernetポート接続(IP指定) | 0x1002 |
| UNIT_RETHER | MX-Rモデル Ethernetポート接続(IP指定) | 0x1002 |
| UNIT_LHETHER | LHCPU Ethernetポート接続(IP指定) | 0x1002 |
| UNIT_RETHER_DIRECT | RCPU Ethernetポート直結 | 0x1003 |
| UNIT_RETHER_DIRECT | MX-Rモデル Ethernetポート直結 | 0x1003 |
| UNIT_LHETHER_DIRECT | LHCPU Ethernetポート直結 | 0x1003 |
| UNIT_MXF_ETHER | MX-Fモデル Ethernetポート接続 | 0x2201 |
| UNIT_MXF_ETHER_DIRECT | MX-Fモデル Ethernetポート直結 | 0x2202 |
| UNIT_FXVETHER | FX5CPU Ethernetポート接続 | 0x2001 |
| UNIT_FXVETHER_DIRECT | FX5CPU Ethernetポート直結 | 0x2002 |
| UNIT_LNETHER | LCPU Ethernetポート接続 | 0x52 |
| UNIT_LNETHER_DIRECT | LCPU Ethernetポート直結 | 0x53 |
| UNIT_QNETHER | QCPU Ethernetポート接続 | 0x2C |
| UNIT_QNETHER_DIRECT | QCPU Ethernetポート直結 | 0x2D |
| UNIT_RJ71GN11 | RCPU用RJ71GN11-T2ユニットIP指定接続 | 0x1006 |
| UNIT_RJ71GN11_DIRECT | RCPU用RJ71GN11-T2ユニット直結 | 0x1007 |
| UNIT_NZ2GF_ETB | Ethernetアダプタユニット(NZ2GF-ETB)接続 | 0x59 |
| UNIT_NZ2GF_ETB_DIRECT | Ethernetアダプタユニット(NZ2GF-ETB)直結 | 0x5A |
| UNIT_FXETHER | FXCPU Ethernetアダプタ(FX3U-ENET-ADP)ハブ経由接続 | 0x4A |
| UNIT_FXETHER_DIRECT | FXCPU Ethernetアダプタ(FX3U-ENET-ADP)直結 | 0x4B |
| UNIT_FXVENET | FX5CPU Ethernetユニット(FX5-ENET，FX5-ENET/IP)IP指定接続 | 0x2004 |
| UNIT_FXVENET_DIRECT | FX5CPU Ethernetユニット(FX5-ENET，FX5-ENET/IP)直結 | 0x200E |
| UNIT_FXVCCLGN | FX5-CCLGN-MSユニット経由接続 | 0x200D |
| UNIT_FXVCPU | FX5CPUシリアルポート接続 | 0x2000 |
| UNIT_QNCPU | QCPU(Qモード)-RS232Cポート直結 | 0x13 |
| UNIT_QNCPU | GOT2000シリーズ QCPU(Qモード)直結 | 0x13 |
| UNIT_LNCPU | LCPU-RS232Cポート直結 | 0x50 |
| UNIT_LNCPU | GOT2000シリーズ LCPU直結 | 0x50 |
| UNIT_QNMOTION | QモーションCPU-RS232Cポート直結 | 0x1C |
| UNIT_FXCPU | FXCPU-RS422ポート直結 | 0x0F |
| UNIT_FXCPU | FXCPU USB直結 | 0x0F |
| UNIT_FXCPU | GOT2000シリーズ FXCPU直結 | 0x0F |
| UNIT_RUSB | RCPU USBポート直結 | 0x1004 |
| UNIT_RUSB | MX-Rモデル USBポート直結 | 0x1004 |
| UNIT_LHUSB | LHCPU USBポート直結 | 0x1004 |
| UNIT_MXF_USB | MX-Fモデル USBポート直結 | 0x2200 |
| UNIT_FXVUSB | FX5CPU USBポート直結 | 0x200C |
| UNIT_QNUSB | QCPU(Qモード)USBポート直結 | 0x16 |
| UNIT_LNUSB | LCPU USBポート直結 | 0x51 |
| UNIT_QSUSB | QSCPU(安全PLC)USBポート直結 | 0x29 |
| UNIT_QNMOTIONUSB | QモーションCPU USBポート直結 | 0x1D |
| UNIT_MNETHBOARD | MELSECNET/Hボード接続 | 0x1E |
| UNIT_MNETGBOARD | CC-Link IEコントローラネットワークボード接続 | 0x2B |
| UNIT_CCIETSNBOARD | CC-Link IE TSNボード接続 | 0x73 |
| UNIT_CCIEFBOARD | CC-Link IEフィールドネットワークボード接続 | 0x2F |
| UNIT_CCLINKBOARD | CC-Link Ver.2ボード接続 | 0x0C |
| UNIT_G4QNCPU | Qシリーズ対応AJ65BT-G4-S3ユニット直結 | 0x1B |
| UNIT_SIMULATOR2*1 | シミュレータ(GX Simulator2)接続 | 0x30 |
| UNIT_SIMULATOR2*1 | シミュレータ(MT Simulator2)接続 | 0x30 |
| UNIT_SIMULATOR3 | シミュレータ(GX Simulator3)接続 | 0x31 |
| UNIT_RETHER_LCS | シミュレータ(MELSOFT Mirror)接続 | 0x1008 |
| UNIT_A900GOT | GOT2000シリーズ接続 | 0x21 |
| UNIT_GOT_RJ71EN71 | GOT2000/3000シリーズ経由MELSEC iQ-Rシリーズ対応E71接続 | 0x1051 |
| UNIT_GOT_QJ71E71 | GOT2000/3000シリーズ経由Qシリーズ対応E71接続 | 0x40 |
| UNIT_GOT_LJ71E71 | GOT2000/3000シリーズ経由Lシリーズ対応E71接続 | 0x5D |
| UNIT_GOT_RETHER | GOT2000/3000シリーズ経由RCPU Ethernetポート接続 | 0x1052 |
| UNIT_GOT_QNETHER | GOT2000/3000シリーズ経由QCPU Ethernetポート接続 | 0x41 |
| UNIT_GOT_LNETHER | GOT2000/3000シリーズ経由LCPU Ethernetポート接続 | 0x55 |
| UNIT_GOT_NZ2GF_ETB | GOT2000シリーズ経由Ethernetアダプタユニット(NZ2GF-ETB)接続 | 0x5B |
| UNIT_GOT_FXETHER | GOT2000/3000シリーズ経由FXCPU Ethernetアダプタ(FX3U-ENET-ADP)接続 | 0x61 |
| UNIT_GOT_FXENET | GOT2000/3000シリーズ経由FXCPU Ethernetユニット(FX3U-ENET-L)接続 | 0x62 |
| UNIT_GOT_FXVENET | GOT2000/3000シリーズ経由FX5CPU Ethernetユニット(FX5-ENET，FX5-ENET/IP)接続 | 0x2008 |
| UNIT_GOT_FXVCPU | FX5CPU GOT-CPUシリアル接続 | 0x2005 |
| UNIT_GOTETHER_FXVCPU | FX5CPU Ethernet-GOT接続 | 0x2006 |
| UNIT_GOT_FXVETHER | FX5CPU GOT-内蔵Ethernet接続 | 0x2007 |
| UNIT_GOTETHER_RJ71C24 | GOT2000シリーズ経由RCPU Ethernetポート(RS422)接続 | 0x1061 |
| UNIT_GOTETHER_QNCPU | GOT2000シリーズ経由QCPU(Qモード)Ethernetポート(RS422)接続 | 0x56 |
| UNIT_GOTETHER_LNCPU | GOT2000シリーズ経由LCPU Ethernetポート(RS232C)接続 | 0x57 |
| UNIT_GOTETHER_FXCPU | GOT2000シリーズ経由FXCPU Ethernetポート接続 | 0x60 |
| UNIT_GOTETHER_QN_ETHER | GOT Ethernetトランスペアレント(Ethernet-GOT-Ethernet-QnCPU)接続 | 0x6F |

※原本では1つのユニットタイプに複数の接続方法が並ぶ場合、ユニットタイプ欄と値欄が複数行で共有されている。また UNIT_RETHER と UNIT_LHETHER は値 0x1002、UNIT_RETHER_DIRECT と UNIT_LHETHER_DIRECT は値 0x1003、UNIT_RUSB と UNIT_LHUSB は値 0x1004 を共有している。本mdでは各行にユニットタイプと値を展開した(接続方法 81行 / ユニットタイプ 70種)。

> *1 CPUタイプがQモーションCPUの場合はMT Simulator2へ，他の場合はGX Simulator2へ接続されます。

### ActProtocolType(LONG) (9.2 / 189 / 原本 p.191)

| 通信プロトコルタイプ | 接続方法 | 値 |
|---|---|---|
| PROTOCOL_SERIAL | シリアルポート経由 | 0x04(4) |
| PROTOCOL_USB | USBポート経由 | 0x0D(13) |
| PROTOCOL_TCPIP | TCP/IP経由 | 0x05(5) |
| PROTOCOL_UDPIP | UDP/IP経由 | 0x08(8) |
| PROTOCOL_TLS | TLS経由 | 0x1D |
| PROTOCOL_DTLS | DTLS経由 | 0x1E |
| PROTOCOL_MNETH | MELSECNET/Hボード経由 | 0x0F(15) |
| PROTOCOL_MNETG | CC-Link IEコントローラネットワークボード経由 | 0x14(20) |
| PROTOCOL_CCIETSN | CC-Link IE TSNボード経由 | 0x1C(28) |
| PROTOCOL_CCIEF | CC-Link IEフィールドネットワークボード経由 | 0x15(21) |
| PROTOCOL_CCLINK | CC-Link経由 | 0x07(7) |
| PROTOCOL_USBGOT | USBポート+GOT経由 | 0x13(19) |
| PROTOCOL_SHAREDMEMORY | 共有メモリサーバ経由(シミュレータ) | 0x06(6) |
| COMM_RS232C*1 | インバータRS-232C通信 | 0x00(0) |
| COMM_USB*1 | インバータUSB通信 | 0x01(1) |
| RC_PROTOCOL_SERIAL | ロボットコントローラRS-232C通信 | 0x01(1) |
| RC_PROTOCOL_USB | ロボットコントローラUSB通信 | 0x04(4) |
| RC_PROTOCOL_TCPIP | ロボットコントローラEthernet(TCP/IP)通信 | 0x02(2) |

> *1 ActMxUnitSeriesが1(0x01)の場合に使用できます。

※ PROTOCOL_TLS(0x1D)・PROTOCOL_DTLS(0x1E)のみ、値に10進の括弧書きが無いのは原本どおり。
