# 三菱 FR-E800 取扱説明書（通信編） 第3章 3.6 BACnet MS/TP

| 項目 | 内容 |
|---|---|
| 原本 | 三菱電機 FR-E800 取扱説明書（通信編） |
| 発行元 | 三菱電機株式会社 |
| 資料番号 / 版数 | IB-0600870 / S版（PDFメタデータ subject: IB-0600870-S） |
| 原本PDF | `PDF/【三菱】インバータ FR-E800 取扱説明書(通信編)_ib0600870s.pdf` (全330ページ) |
| 本ファイルの範囲 | 3.6 (印刷 p.258-272 / PDF p.259-273) |
| ページ対応 | 「原本 p.」はPDFのページ番号、「印刷 p.」は原本フッタのページ番号。印刷ページ = PDFページ − 1。本文中の「〇〇ページ参照」は印刷ページ |
| 変換日 | 2026-10-02 |
| 変換方法 | pypdfium2(本文) + PyMuPDF 200dpi 画像の目視(全ページ) |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。

**転記上の扱い**: 原本の結合セルは各行に値を展開。セル内改行は `<br>`。左右並置の表は方向ごとに別表に分割した場合あり（各所に注記）。機種アイコンは `[E800]` `[E800-(SC)E]` 等。図は【図】プレースホルダ＋読み取れる事実の箇条書き。ラダー図のニモニックは原本に記載がなく、図から書き起こしたもの（各所に注記）。見出しレベル: 章 `##` / 節 `###` / 項 `####` / ◆ `#####` / ■ `######`。

---

## 主要用語 対訳表 (Glossary) (3.6 / 原本 p.259-273)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| プロトコル選択 | Protocol selection | Pr.549 (N000) | 参考訳 |
| PU 通信局番 | PU communication station number | Pr.117 (N020) | 参考訳 |
| PU 通信速度 | PU communication speed | Pr.118 (N021) | 参考訳 |
| PU 通信チェック時間間隔 | PU communication check time interval | Pr.122 (N026) | 参考訳 |
| %設定基準周波数 | Frequency reference for % setting | Pr.390 (N054) | 参考訳 |
| 自動ボーレート / 最大マスタ | Auto baudrate / Max Master | Pr.726 (N050) | 参考訳 |
| 最大情報フレーム | Max Info Frames | Pr.727 (N051) | 原本併記 |
| デバイスインスタンス番号 | Device instance number | Pr.728、Pr.729 (N052、N053) | 参考訳 |
| 操作パネルメインモニタ選択 | Operation panel main monitor selection | Pr.52 (M100) | 参考訳 |
| BACnet 受信ステータス | BACnet reception status | Pr.52＝81 | 参考訳 |
| トークンパッシング方式 | Token passing | MS/TP | 参考訳 |
| 断線検出 | Signal loss detection | Pr.122 / E.PUE | 参考訳 |
| ボーレート自動認識 | Automatic baud rate detection | Pr.726＝128～255 | 参考訳 |
| ネットワークバイアス抵抗 | Network bias resistor | — | 参考訳 |
| オブジェクト識別子 | Object Identifier | — | 原本併記 |
| オブジェクト名 | Object Name | — | 原本併記 |
| 現在値 | Present Value | — | 原本併記 |
| 優先順位配列 | Priority Array | — | 原本併記 |
| レリンキッシュデフォルト | Relinquish Default | — | 原本併記 |
| 現在のコマンド優先度 | Current Command Priority | — | 原本併記 |
| サービス外 | Out Of Service | — | 原本併記 |
| 状態フラグ | Status Flags | — | 原本併記 |
| 変更の反映待ち | Changes Pending | — | 原本併記 |
| アナログ入力 / アナログ出力 / アナログ値 | Analog Input / Analog Output / Analog Value | ANALOG_INPUT(0)/ANALOG_OUTPUT(1)/ANALOG_VALUE(2) | 原本併記 |
| バイナリ入力 / バイナリ出力 / バイナリ値 | Binary Input / Binary Output / Binary Value | BINARY_INPUT(3)/BINARY_OUTPUT(4)/BINARY_VALUE(5) | 原本併記 |
| ネットワークポート | Network Port | NETWORK_PORT(56) | 原本併記 |
| 単位 | Unit | — | 原本併記 |
| 速度指令の比率 | Speed scale | AV 300 | 原本併記 |
| メールボックス | Mailbox parameter / Mailbox value | AV 398 / 399 | 原本併記 |
| バイナリ入力 | BINARY INPUT | BINARY_INPUT(3) | 原本併記 |
| バイナリ出力 | BINARY OUTPUT | BINARY_OUTPUT(4) | 原本併記 |
| バイナリ値 | BINARY VALUE | BINARY_VALUE(5) | 原本併記 |
| デバイス | DEVICE | DEVICE(8) | 原本併記 |
| 書込み拒否 | Write Access Denied |  | 原本併記 |
| 端子機能選択 | terminal function selection | Pr.180〜Pr.184、Pr.190〜Pr.192 | 参考訳 |
| 始動 / 停止 | Run/Stop | BV 400 | 原本併記 |
| 正転 / 逆転 | Forward/Reverse | BV 401 | 原本併記 |
| 異常リセット | Fault reset | BV 402 | 原本併記 |
| 軽故障出力 | Alarm output | LF 信号 | 原本併記 |
| 異常出力 | Fault output | ALM 信号 | 原本併記 |
| 運転準備完了 | Inverter operation ready | RY 信号 | 原本併記 |
| システム環境変数 | system environment variables | 40010 | 参考訳 |
| 運転モード／インバータ設定 | operation mode / inverter setting | 40010 | 参考訳 |
| モニタコード | monitor code | Pr.52 | 参考訳 |
| アラーム履歴 | alarm history | 40501〜40510 | 参考訳 |
| 機種情報モニタ | model information monitor | 44001〜44013 | 参考訳 |
| 計算機リンク | computer link |  | 参考訳 |
| 通信運転指令権 | command source for communication operation |  | 参考訳 |
| 相互運用性ビルディングブロック | BACnet Interoperability Building Blocks (BIBB) | DS-RP-B 等 | 参考訳 |
| プロトコル実装適合性宣言 | Protocol Implementation Conformance Statement (PICS) | ANNEX A | 参考訳 |

## 変換範囲表 (3.6 / 原本 p.259-273)

| 原本ページ | 節 | 扱い |
|---|---|---|
| p.259-273 | 3.6 BACnet MS/TP（PICS含む） | 全文 |
| p.274 | 第4章 章扉（章内目次のみ） | 未変換（目次のため） |
| 上記以外 | 他章 | 同フォルダの他ファイル参照（前付け p.1-6 表紙・目次は未変換） |

## 目次 (3.6)

- [3.6 BACnet MS/TP (3.6 / 印刷 p.258 / 原本 p.259)](#36-bacnet-mstp-36--印刷-p258--原本-p259)

---

### 3.6 BACnet MS/TP (3.6 / 印刷 p.258 / 原本 p.259)

インバータの PU コネクタから BACnet MS/TP プロトコルを使用し、通信運転やパラメータ設定ができます。
BACnet MS/TP を使用する場合、**Pr.549 プロトコル選択**＝ “2” としてください。
インバータの製造時期によっては対応しません。仕様変更の内容については 318 ページを参照してください。

| Pr. | 名称 | 初期値*1 Gr.1 | 初期値*1 Gr.2 | 設定範囲 | 内容 |
|---|---|---|---|---|---|
| 52<br>M100 | 操作パネルメインモニタ選択 | 0 | 0 | 0、5 ～ 14、17 ～ 20、22 ～ 33、35、38、40 ～ 42、44、45、50 ～ 57、61、62、64、65、67、68、81 ～ 84、85*2、86*3、91、97、100 | 81：BACnet 受信ステータス<br>82：BACnet トークンパスカウンタ（トークンを受け取った回数を表示）<br>83：BACnet 有効 APDU カウンタ（有効な APDU を検出した回数を表示）<br>84：BACnet 通信エラー検出カウンタ（通信エラーを検出した回数を表示）<br>85：端子 FM 出力レベル（AnalogOutput0 と同じ表示内容）<br>86：端子 AM 出力レベル（AnalogOutput1 と同じ表示内容）<br>設定値 82、83 のカウンタは 9999 を超えると 0 に戻ります。設定値 84 のカウンタは 9999 が上限です。 |
| 774<br>M101 | 操作パネルモニタ選択 1 | 9999 | 9999 | 1 ～ 3、5 ～ 14、17 ～ 20、22 ～ 33、35、38、40 ～ 42、44、45、50 ～ 57、61、62、64、65、67、68、81 ～ 84、85*2、86*3、91、97、100、9999 | 81：BACnet 受信ステータス<br>82：BACnet トークンパスカウンタ（トークンを受け取った回数を表示）<br>83：BACnet 有効 APDU カウンタ（有効な APDU を検出した回数を表示）<br>84：BACnet 通信エラー検出カウンタ（通信エラーを検出した回数を表示）<br>85：端子 FM 出力レベル（AnalogOutput0 と同じ表示内容）<br>86：端子 AM 出力レベル（AnalogOutput1 と同じ表示内容）<br>設定値 82、83 のカウンタは 9999 を超えると 0 に戻ります。設定値 84 のカウンタは 9999 が上限です。 |
| 775<br>M102 | 操作パネルモニタ選択 2 | 9999 | 9999 | 1 ～ 3、5 ～ 14、17 ～ 20、22 ～ 33、35、38、40 ～ 42、44、45、50 ～ 57、61、62、64、65、67、68、81 ～ 84、85*2、86*3、91、97、100、9999 | 81：BACnet 受信ステータス<br>82：BACnet トークンパスカウンタ（トークンを受け取った回数を表示）<br>83：BACnet 有効 APDU カウンタ（有効な APDU を検出した回数を表示）<br>84：BACnet 通信エラー検出カウンタ（通信エラーを検出した回数を表示）<br>85：端子 FM 出力レベル（AnalogOutput0 と同じ表示内容）<br>86：端子 AM 出力レベル（AnalogOutput1 と同じ表示内容）<br>設定値 82、83 のカウンタは 9999 を超えると 0 に戻ります。設定値 84 のカウンタは 9999 が上限です。 |
| 776<br>M103 | 操作パネルモニタ選択 3 | 9999 | 9999 | 1 ～ 3、5 ～ 14、17 ～ 20、22 ～ 33、35、38、40 ～ 42、44、45、50 ～ 57、61、62、64、65、67、68、81 ～ 84、85*2、86*3、91、97、100、9999 | 81：BACnet 受信ステータス<br>82：BACnet トークンパスカウンタ（トークンを受け取った回数を表示）<br>83：BACnet 有効 APDU カウンタ（有効な APDU を検出した回数を表示）<br>84：BACnet 通信エラー検出カウンタ（通信エラーを検出した回数を表示）<br>85：端子 FM 出力レベル（AnalogOutput0 と同じ表示内容）<br>86：端子 AM 出力レベル（AnalogOutput1 と同じ表示内容）<br>設定値 82、83 のカウンタは 9999 を超えると 0 に戻ります。設定値 84 のカウンタは 9999 が上限です。 |
| 117<br>N020 | PU 通信局番 | 0 | 0 | 0 ～ 127*4 | インバータの局番（ノード）を設定します。 |
| 118<br>N021 | PU 通信速度 | 192 | 192 | 96 、192 、384、576、768、1152*4*5 | 通信速度を設定します。<br>設定値 ×100 が通信速度になります。<br>例えば、96 なら 9600bps となります。 |
| 122<br>N026 | PU 通信チェック時間間隔 | 0 | 0 | 0 | RS-485 通信可能ですが、指令権のある運転モードにすると、インバータは出力遮断します。 |
| 122<br>N026 | PU 通信チェック時間間隔 | 0 | 0 | 0.1 ～ 999.8s | 通信チェック（断線検出）時間の間隔を設定します。<br>無通信状態が許容時間以上継続すると、インバータは出力遮断します。 |
| 122<br>N026 | PU 通信チェック時間間隔 | 0 | 0 | 9999 | 通信チェック（断線検出）しません。 |
| 390<br>N054 | %設定基準周波数 | 60Hz | 50Hz | 1 ～ 590Hz | 設定周波数の基準周波数を設定することができます。 |
| 549<br>N000 | プロトコル選択 | 0 | 0 | 0 | 三菱インバータ（計算機リンク）プロトコル |
| 549<br>N000 | プロトコル選択 | 0 | 0 | 1 | MODBUS RTU プロトコル |
| 549<br>N000 | プロトコル選択 | 0 | 0 | 2*6 | BACnet MS/TP プロトコル |
| 726<br>N050 | 自動ボーレート / 最大マスタ | 255 | 255 | 0 ～ 255 | Auto baudrate (bit7)<br>0：無効、1：有効 |
| 726<br>N050 | 自動ボーレート / 最大マスタ | 255 | 255 | 0 ～ 255 | Max Master (bit0 ～ bit6) 設定範囲：0 ～ 127<br>マスタノードに指定するアドレスの上限値 |
| 727<br>N051 | 最大情報フレーム | 1 | 1 | 1 ～ 255 | トークン保持中に送信できるフレームの最大数 |
| 728<br>N052 | デバイスインスタンス番号（上位 3 桁） | 0 | 0 | 0 ～ 419<br>（0 ～ 418） | デバイスの識別番号<br>**Pr.728、Pr.729** の組合せが 0 ～ 4194302 以外の場合は設定範囲外になります。<br>**Pr.729** の設定範囲は **Pr.728** ＝ “419” のとき 0 ～ 4302 までとなります。<br>**Pr.728** の設定範囲は **Pr.729** ＝ “4303 以上 ” のとき 0 ～ 418 までとなります。 |
| 729<br>N053 | デバイスインスタンス番号（下位 4 桁） | 0 | 0 | 0 ～ 9999<br>（0 ～ 4302） | デバイスの識別番号<br>**Pr.728、Pr.729** の組合せが 0 ～ 4194302 以外の場合は設定範囲外になります。<br>**Pr.729** の設定範囲は **Pr.728** ＝ “419” のとき 0 ～ 4302 までとなります。<br>**Pr.728** の設定範囲は **Pr.729** ＝ “4303 以上 ” のとき 0 ～ 418 までとなります。 |

（注: 原本では初期値欄は Gr.1/Gr.2 共通の結合セル（Pr.390 のみ 60Hz/50Hz で分かれる）。Pr.52/774/775/776 の内容欄、Pr.774〜776 の設定範囲・初期値欄、Pr.728/729 の内容欄はそれぞれ結合セルで、各行に展開した。）

*1 Gr.1、Gr.2 はパラメータ初期値グループを表します。（FR-E800 取扱説明書（機能編）参照）
*2 FR-E800-1 のみ設定可能です。
*3 FR-E800-4/FR-E800-5 のみ設定可能です。
*4 設定範囲外の値が設定されている場合は、初期値で動作します。
*5 Auto baudrate 使用時は検出した通信速度に変更されます。
*6 **Pr.549** ＝ “2（BACnet MS/TP）” 設定時、パラメータユニットは使用できません。

> **NOTE**
> - 各パラメータの初期設定を行ったあと必ずインバータリセットを行ってください。通信関連のパラメータは変更後、リセットを行わないと通信不可となります。

##### ◆ 通信仕様 (3.6 / 原本 p.260)

- 物理メディア EIA-485 の BACnet 規格に準拠しています。

| 項目 | 項目（細目） | 内容 |
|---|---|---|
| 物理メディア | | EIA-485 (RS-485) |
| 物理メディア | 接続ポート | PU コネクタ |
| 物理メディア | データ伝送方式 | NRZ 符号化方式 |
| 物理メディア | ボーレート | 9600bps、19200bps、38400bps、57600bps、76800bps、115200bps |
| 物理メディア | スタートビット | 1Bit 固定 |
| 物理メディア | データ長 | 8Bit 固定 |
| 物理メディア | パリティビット | なし固定 |
| 物理メディア | ストップビット | 1Bit 固定 |
| ネットワークトポロジー | | バス型 |
| 通信方式 | | トークンパッシング方式（トークンバス） |
| 通信方式 | | マスタ・スレーブ方式 （本製品はマスタのみ対応します。） |
| 通信プロトコル | | MS/TP ( マスタスレーブ / トークンパッシング LAN) |
| 最大接続数 | | 255 台 (1 セグメント 32 台まで、リピータで追加可能 ) |
| ノード番号 | | 0 ～ 127 |
| ノード番号 | マスタ | 0 ～ 127（本製品はマスタのため、この範囲となります。） |
| サポートする BACnet 標準オブジェクトタイプとプロパティ | | 261 ページ参照 |
| サポートする BIBBs(AnnexK) | | 270 ページ参照 |
| BACnet 標準デバイスプロファイル (AnnexL) | | 270 ページ参照 |
| セグメンテーション能力 | | 非サポート |
| デバイスアドレスバインディング | | 非サポート |

> **NOTE**
> - 本製品は、BACnet Application Specific Controller(B-ASC) として定義されています。
> - 本製品は、複数マスタが存在する通信となるため２線式の通信となります。
> - 本製品はローカルバイアス抵抗付きノードであるため、システム構成にネットワークバイアス抵抗付きノードが少なくとも 1 台必要です。別途、ネットワークバイアス抵抗付きノードを用意してください。

##### ◆ BACnet 受信ステータスモニタ (Pr.52) (3.6 / 原本 p.260)

- **Pr. 52** に “81” を設定すると、操作パネルで BACnet 通信の状態をモニタすることができます。

| モニタ値 | 状態 | 内容 | LF 信号出力 |
|---|---|---|---|
| 0 | アイドル | 一度も BACnet 通信していない | OFF |
| 1 | ボーレート自動認識中 | ボーレート自動認識中<br>（ボーレート自動認識中に検出した通信エラーは、異常認識しない） | OFF |
| 2 | ネットワーク未加入 | 自ノード宛トークンを受信待ちしている状態 | OFF |
| 10 | 自ノード宛データ | 自ノード宛トークンを受信 | OFF |
| 11 | 自ノード宛データ | 自ノード宛（一斉同報含む）のサポートしている要求を受信 | OFF |
| 12 | 自ノード宛データ | 自ノード宛（一斉同報含む）のサポートしていない要求を受信 | OFF |
| 20 | 他ノード宛データ | 他ノード宛データを受信 | OFF |
| 30 | ネットワーク離脱 | 一度トークンに加入後、トークンから離脱している状態 | OFF |
| 90 | 異常データ | 通信エラー検出 | ON |
| 91 | 異常データ | プロトコル異常<br>（LPDU、NPDU、APDU が規定フォーマットに従っていない場合） | ON |

##### ◆ 断線検出（Pr.122） (3.6 / 原本 p.260)

- インバータ、計算機間の断線検出を行い、断線した（通信が途絶えた）場合、通信エラー（E.PUE）が発生してインバータは出力遮断します。
- 断線を検出した場合、LF 信号を出力します。
- 設定値を “9999” にした場合、通信チェック（断線検出）は行いません。
- 設定値が “0” の場合、RS-485 通信からのモニタやパラメータの読出しなどは可能ですが、指令権のある運転モード（初期設定では、ネットワーク運転モード）に変更した瞬間に通信エラー（E.PUE）となります。
- 設定値を “0.1s ～ 999.8s” に設定すると、断線検出を行います。断線検出を行う場合は、計算機から通信チェック時間間隔以内でデータを送信する必要があります。（マスタから送信するデータの局番設定に関係なく、インバータは通信チェック（通信チェックカウンタのクリア）を行います。）
- 通信チェックは、操作権のある運転モード（初期設定では、ネットワーク運転モード）で、1 回目の通信から開始します。

【図】例）Pr.122＝“0.1～999.8s”の場合 のタイミングチャート (原本 p.261)
- 図中の信号・軸: 運転モード（← 外部 → | ← NET →）、計算機→インバータ、インバータ→計算機、通信チェックカウンタ（Pr.122 のレベルを破線で表示）、ALM、時間（右向き矢印）。
- 運転モードが外部の間: 計算機→インバータ のデータ 1 回、インバータ→計算機 の応答 1 回がある。通信チェックカウンタは 0 のまま。
- 運転モードが NET に切り換わった後: 計算機→インバータ のデータ送信、続いてインバータ→計算機 の応答。応答の後の時点に「チェック開始」の矢印があり、そこから通信チェックカウンタが増加し始める。
- 次に計算機→インバータ のデータ（ENQ）を受信した時点でカウンタは 0 にクリアされる（Pr.122 に達する前）。
- その後インバータ→計算機 の応答の後、再びカウンタが増加し、計算機からのデータが無いまま Pr.122 のレベルに達した時点で「アラーム(E.PUE)」が発生する。
- ALM はそれまで OFF で、カウンタが Pr.122 に達した時点で ON となる。

> **NOTE**
> - **Pr.502 通信異常時停止モード選択**の設定によって通信異常時の動作が異なります。（310 ページ参照）

##### ◆ %設定基準周波数 (Pr.390) (3.6 / 原本 p.261)

- 設定周波数の基準周波数を設定することができます。**Pr. 390 %設定基準周波数**の設定値を 100% の基準とします。周波数指令の比率は、下記の計算式によって設定周波数に換算されます。
  設定周波数＝**%設定基準周波数** × Speed scale (264 ページ参照 )

【図】%設定基準周波数と設定周波数の関係 (原本 p.261)
- 横軸: 設定周波数（Speed scale）、0% ～ 100.00%。縦軸: 周波数、原点 0.00Hz。
- 原点（0%, 0.00Hz）から右上へ直線。100.00% のとき縦軸は「Pr.390 %設定周波数基準」の値となる（破線）。
- 任意の Speed scale の値から直線に当たった点を左へ読むと「インバータに書き込まれる設定周波数」となる。

> **NOTE**
> - インバータの最小周波数分解能以下の分解能で設定することはできません。
> - 設定周波数は RAM 書込みで反映します。
> - 設定周波数への反映は、Speed scale の書込み時に反映されます。（**Pr.390** の設定値を変更した時点では、設定周波数には反映されません。）

##### ◆ ボーレート自動認識機能（Pr.726 自動ボーレート / 最大マスタ） (3.6 / 原本 p.261)

- **Pr.726** の設定により通信速度を自動で切り換えることが可能です。**Pr.726** ＝ “128 ～ 255” の場合、電源 OFF → ON またはインバータリセット後、ボーレートの自動認識を開始します。

| Pr.726 設定値 | 動作 |
|---|---|
| 0 ～ 127 | ボーレート自動切換え機能無効<br>（ボーレートは **Pr.118** 設定値を使用） |
| 128 ～ 255 | 通信バス上のデータを監視し、ボーレートを自動的に切り換えます。<br>認識したボーレートは **Pr.118** に書き込まれます。 |

> **NOTE**
> - ボーレートを認識できたら、認識したボーレートは **Pr.342 通信 EEPROM 書込み選択**の設定によらず、**Pr.118** の設定値として EEPROM に書き込みます。
> - ボーレート自動認識中は、BACnet ステータスモニタで “1” を表示します。
> - ボーレート自動認識中は通信エラーモニタのカウントは行いません。
> - ボーレート自動認識中は、受信のみとし、送信は行いません。
> - 通信バスにインバータを接続していない状態では、ボーレート切換え動作は終了しません。（BACnet プロトコルは確立しません）
> - ボーレート自動切換え中に異常データを受信し続けている場合、ボーレート切換え動作も終了しません。（BACnet プロトコルは確立しません）

##### ◆ サポートする BACnet 標準オブジェクトタイプとプロパティ (3.6 / 原本 p.262)

R：読出しのみ可能　W：読出し / 書込み可能（Commandable values 非対応）　C：読出し / 書込み可能（Commandable values 対応）

各オブジェクトのサポート:

| プロパティ | (Analog Input)<br>アナログ入力 | (Analog Output)<br>アナログ出力 | (Analog Value)<br>アナログ値 | (Binary Input)<br>バイナリ入力 | (Binary Output)<br>バイナリ出力 | (Binary Value)<br>バイナリ値 | (Device)<br>デバイス | (Network Port)<br>ネットワークポート |
|---|---|---|---|---|---|---|---|---|
| APDU 長さ (APDU Length) | | | | | | | | R |
| APDU タイムアウト (APDU Timeout) | | | | | | | R | |
| アプリケーションソフトウェアバージョン (Application Software Version) | | | | | | | R | |
| 変更の反映待ち (Changes Pending) | | | | | | | | R |
| データベースリビジョン (Database Revision) | | | | | | | R | |
| デバイスアドレスバインディング (Device Address Binding) | | | | | | | R | |
| イベント状態 (Event State) | R | | R | R | R | R | | |
| ファームウェアリビジョン (Firmware Revision) | | | | | | | R | |
| 通信速度 (Link Speed) | | | | | | | | R |
| MAC アドレス (MAC Address) | | | | | | | | R |
| 受容する APDU の最大長 (Max APDU Length Accepted) | | | | | | | R | |
| 最大情報フレーム (Max Info Frames) | | | | | | | W | W |
| 最大マスタ (Max Master) | | | | | | | W | W |
| モデル名 (Model Name) | | | | | | | R | |
| ネットワーク番号 (Network Number) | | | | | | | | W |
| ネットワーク番号品質 (Network Number Quality) | | | | | | | | R |
| ネットワークタイプ (Network Type) | | | | | | | | R |
| APDU 再送回数 (Number of APDU Retries) | | | | | | | R | |
| オブジェクト識別子 (Object Identifier) | R | | R | R | R | R | R | R |
| オブジェクトリスト (Object List) | | | | | | | R | |
| オブジェクト名 (Object Name) | R | | R | R | R | R | R | R |
| オブジェクトタイプ (Object Type) | R | | R | R | R | R | R | R |
| サービス外 (Out Of Service) | R | | R | R | R | R | | R |
| 極性 (Polarity) | | | | R | R | | | |
| 現在値 (Present Value) | R | | C*1 | R | C | C*1 | | |
| 優先順位配列 (Priority Array) | | | R*2 | | R | R*2 | | |
| プロトコルレベル (Protocol Level) | | | | | | | | R |
| プロトコルオブジェクトタイプサポート (Protocol Object Types Supported) | | | | | | | R | |
| プロトコルリビジョン (Protocol Revision) | | | | | | | R | |
| プロトコルサービスサポート (Protocol Services Supported) | | | | | | | R | |
| プロトコルバージョン (Protocol Version) | | | | | | | R | |
| 信頼性 (Reliability) | | | | | | | | R |
| レリンキッシュデフォルト (Relinquish Default) | | | R*2 | | R | R*2 | | |
| セグメントサポート (Segmentation Supported) | | | | | | | R | |
| 状態フラグ (Status Flags) | R | | R | R | R | R | | R |
| システム状態 (System Status) | | | | | | | R | |
| 単位 (Unit) | R | | R | | | | | |
| ベンダ識別子 (Vendor Identifier) | | | | | | | R | |
| ベンダ名 (Vendor Name) | | | | | | | R | |
| プロパティリスト (Property List) | R | R | R | R | R | R | R | R |
| 現在のコマンド優先度 (Current Command Priority) | | R | | | R | | | |

（注: 原本 p.262〜p.263 にまたがる1つの表。セル位置は画像の列位置どおりに転記した。）

*1 このプロパティはオブジェクトの一部のインスタンスに対し Commandable です。それ以外には読出し / 書込み可能です。
*2 このプロパティは現在値プロパティが Commandable であるオブジェクトのインスタンスにのみサポートされています。

##### ◆ サポートするプロパティの詳細 (3.6 / 原本 p.263)

- 対応するプロパティの詳細を下記に示します。

| プロパティ | 詳細 |
|---|---|
| APDU 長さ (APDU Length) | オクテットの最大数を示します。<br>FR-E800 では 50 オクテット固定です。 |
| APDU タイムアウト (APDU Timeout) | APDU 要求に対する到達確認の返信がない場合の再送信時間間隔 (ms) を示します。 |
| アプリケーションソフトウェアバージョン (Application Software Version) | インバータのソフトフェアバージョンを示します。 |
| 変更の反映待ち (Changes Pending) | リセット時反映のプロパティ値が変更された場合、TRUE(1) となります。<br>リセット時に初期化されて FALSE(0) になります。 |
| データベースリビジョン (Database Revision) | 常に 0 |
| デバイスアドレスバインディング (Device Address Binding) | データなし |
| イベント状態 (Event State) | 関連するオブジェクトのイベント状態を示します。<br>FR-E800 では NORMAL(0) 固定です。 |
| ファームウェアリビジョン (Firmware Revision) | ファームウェアのレベルを示します。 |
| 通信速度 (Link Speed) | 通信速度をビット / 秒として表します。<br>**Pr.118** の設定値 ×100 が通信速度となります。 |
| MAC アドレス (MAC Address) | ネットワークポートの MAC アドレスを示します。<br>**Pr.117** の設定値が MAC アドレスとなります。<br>例えば、**Pr.117** が 127 の場合は 7F となります。 |
| 受容する APDU の最大長 (Max APDU Length Accepted) | APDU の最大長を示します。 |
| 最大情報フレーム (Max Info Frames) | トークン保持中に送信できるフレームの最大数を示します。書込み時は **Pr.727** に反映される。 |
| 最大マスタ (Max Master) | マスタノードに指定するアドレスの上限値を示します。書込み時は **Pr.726** に反映される。 |
| モデル名 (Model Name) | BACnet デバイスのモデルを示します。 |
| ネットワーク番号 (Network Number) | ネットワーク番号を示します。<br>FR-E800 では 0 固定です。書込み時に 0 以外の値を書き込んだ場合は VALUE_OUT_OF_RANGE (37) エラーとなります。 |
| ネットワーク番号品質 (Network Number Quality) | ネットワークポート番号の品質を示します。<br>FR-E800 では UNKNOWN(0) 固定です。 |
| ネットワークタイプ (Network Type) | ネットワークの通信方式を示します。<br>FR-E800 では MSTP(2) 固定です。 |
| APDU 再送回数 (Number of APDU Retries) | APDU 再送回数の最大数を示します。 |
| オブジェクト識別子 (Object Identifier) | オブジェクト識別のため固有の数値コードを示します。 |
| オブジェクトリスト (Object List) | オブジェクト識別子の一覧を示します。 |
| オブジェクト名 (Object Name) | オブジェクトの名前を示します。 |
| オブジェクトタイプ (Object Type) | アナログ入力：ANALOG_INPUT(0)<br>アナログ出力：ANALOG_OUTPUT(1)<br>アナログ値：ANALOG_VALUE(2)<br>バイナリ入力：BINARY_INPUT(3)<br>バイナリ出力：BINARY_OUTPUT(4)<br>バイナリ値：BINARY_VALUE(5)<br>デバイス：DEVICE(8)<br>ネットワークポート：NETWORK_PORT(56) |
| サービス外 (Out Of Service) | 現在値プロパティが変更されない、または変更が反映されない場合、TRUE(1) となります。それ以外は FALSE(0) となります。 |
| 極性 (Polarity) | バイナリ出力が負論理の場合は、REVERSE(1) となります。バイナリ入力は NORMAL(0) 固定です。 |
| 現在値 (Present Value) | 各オブジェクト識別子の現在値を示します。 |
| 優先順位配列 (Priority Array) | Commandable values に対応したオブジェクトへ書き込む値が格納されます。電源 ON またはインバータリセット時に初期化されます。 |
| プロトコルレベル (Protocol Level) | プロトコルのレベルを示します。<br>FR-E800 では BACNET_APPLICATION(2) 固定です。 |
| プロトコルオブジェクトタイプサポート (Protocol Object Types Supported) | サポートするオブジェクトは Bit ＝ 1、それ以外は Bit ＝ 0 となります。 |
| プロトコルリビジョン (Protocol Revision) | 対応する BACnet 規格のリビジョンを示します。 |
| プロトコルサービスサポート (Protocol Services Supported) | サポートするサービスは Bit ＝ 1、それ以外は Bit ＝ 0 となります。 |
| プロトコルバージョン (Protocol Version) | 対応する BACnet 規格のバージョンを示します。 |
| 信頼性 (Reliability) | ネットワークポートの信頼性を示します。<br>FR-E800 では no-fault-detected(0) 固定です。 |
| レリンキッシュデフォルト (Relinquish Default) | 優先順位配列プロパティにデータがない場合に適用されるデフォルト値を示します。 |
| セグメントサポート (Segmentation Supported) | 送受信のメッセージ分割をサポートするかを示します。<br>FR-E800 では NO_SEGMENTATION(3) 固定です。 |
| 状態フラグ (Status Flags) | 常に 0 |
| システム状態 (System Status) | デバイスの現在の物理的状態および論理的状態を示します。 |
| 単位 (Unit) | 計測単位を工学単位で示します。 |
| ベンダ識別子 (Vendor Identifier) | ASHRAE より割り当てられた 16 ビットのベンダ識別コードを示します。 |
| ベンダ名 (Vendor Name) | Mitsubishi Electric Corporation |
| プロパティリスト (Property List) | プロパティ識別子の一覧を示します。 |
| 現在のコマンド優先度 (Current Command Priority) | 現在アクティブな優先度を示します。 |

##### ◆ サポートする BACnet オブジェクト (3.6 / 原本 p.264)

- アナログ入力 (ANALOG INPUT)

| オブジェクト識別子<br>Object Identifier | オブジェクト名<br>Object Name | Present Value<br>Access Type*1 | 内容 | 単位<br>Unit |
|---|---|---|---|---|
| 1 | Terminal 2 | R | 端子 2 の物理的な入力電圧（または電流）レベルを示します。<br>(**Pr.73、Pr.267** の設定により範囲が異なります。<br>0 ～ 10V (0% ～ 100%)、<br>0 ～ 5V (0% ～ 100%) 、<br>0 ～ 20mA (0% ～ 100%) ) | percent<br>(98) |
| 2 | Terminal 4 | R | 端子 4 の物理的な入力電流（または電圧）レベルを示します。<br>(**Pr.73、Pr.267** の設定により範囲が異なります。<br>2 ～ 10V (0% ～ 100%)、<br>1 ～ 5V (0% ～ 100%) 、<br>4 ～ 20mA (0% ～ 100%) ) | percent<br>(98) |

*1 R：読出しのみ可能、W：読出し / 書込み可能（Commandable values 非対応）、C：読出し / 書込み可能（Commandable values 対応）

- アナログ出力 (ANALOG OUTPUT)

| オブジェクト識別子<br>Object Identifier | オブジェクト名<br>Object Name | Present Value<br>Access Type*1 | 内容 | 単位<br>Unit |
|---|---|---|---|---|
| 0*2 | Terminal FM | C | 端子 FM の物理的な出力電流レベルを制御します。<br>**Pr.54 FM 端子機能選択** =“85” の場合に制御可能 *4 になります。<br>( 設定範囲：0 ～ 200%) | percent<br>(98) |
| 1*3 | Terminal AM | C | 端子 AM の物理的な出力電圧レベルを制御します。<br>**Pr.158 AM 端子機能選択** =“86” の場合に制御可能 *4 になります。<br>( 設定範囲：-200 ～ 200%) | percent<br>(98) |

*1 R：読出しのみ可能、W：読出し / 書込み可能（Commandable values 非対応）、C：読出し / 書込み可能（Commandable values 対応）
　Commandable values に対応したオブジェクトへの書込みは、運転モードなどの書込み条件が合わずに "Write Access Denied" が返信されても、設定範囲内の書込みであれば優先順位配列に格納されます。
*2 FR-E800-1 のみ設定可能です。
*3 FR-E800-4/FR-E800-5 のみ設定可能です。
*4 運転モード、操作指令権、運転指令権に関係なく動作します。

- アナログ値 (ANALOG VALUE)

| オブジェクト識別子<br>Object Identifier | オブジェクト名<br>Object Name | Present Value<br>Access Type*1 | 内容 | 単位<br>Unit |
|---|---|---|---|---|
| 1 | Output frequency*2 | R | 出力周波数モニタを示します。 | hertz<br>(27) |
| 2 | Output current | R | 出力電流モニタを示します。 | amperes<br>(3) |
| 3 | Output voltage | R | 出力電圧モニタを示します。 | volts<br>(5) |
| 6 | Running speed*2 | R | 運転速度モニタを示します。 | revolution-per-minute<br>(104) |
| 8 | Converter output voltage | R | コンバータ出力電圧モニタを示します。 | volts<br>(5) |
| 14 | Output power | R | 出力電力モニタを示します。 | kilowatts<br>(48) |
| 17 | Load meter | R | ロードメータモニタを示します。 | percent<br>(98) |
| 20 | Cumulative energization time | R | 積算通電時間モニタを示します。 | hours<br>(71) |
| 23 | Actual operation time | R | 実稼動時間モニタを示します。 | hours<br>(71) |
| 25 | Cumulative power | R | 積算電力モニタを示します。 | kilowatt-hours<br>(19) |
| 52 | PID set point | R | PID 目標値モニタを示します。 | no-units<br>(95) |
| 54 | PID deviation | R | PID 偏差モニタを示します。<br>（0%基準でマイナスも表示、0.1%単位） | no-units<br>(95) |
| 67 | PID measured value2 | R | PID 測定値モニタ 2 を示します。 | no-units<br>(95) |
| 200 | Alarm history 1 | R | アラーム履歴 1（最新の異常）を示します。 | no-units<br>(95) |
| 201 | Alarm history 2 | R | アラーム履歴 2（1 回前の異常）を示します。 | no-units<br>(95) |
| 202 | Alarm history 3 | R | アラーム履歴 3（2 回前の異常）を示します。 | no-units<br>(95) |
| 203 | Alarm history 4 | R | アラーム履歴 4（3 回前の異常）を示します。 | no-units<br>(95) |
| 300 | Speed scale*3 | C | 周波数指令の比率を設定します。（設定範囲：0.00 ～ 100.00）<br>(260 ページ参照 ) | percent<br>(98) |
| 310 | PID set point CMD*3 | C | PID 動作目標値を設定します。<br>• **Pr.128** ＝ “40 ～ 43” かつ **Pr.609** ＝ “4” であればダンサ制御時に目標値となります。（設定範囲：0.00 ～ 100.00）*5<br>• **Pr.128** ＝ “60 または 61” であれば PID 動作時に目標値となります。（設定範囲：0.00 ～ 100.00）*4<br>• **Pr.128** ＝ “1000 または 1001” かつ **Pr.609** ＝ “4” であれば PID 動作時に目標値となります。（設定範囲：0.00 ～ 100.00）*4*5<br>• **Pr.128** ＝ “2000 または 2001”（周波数反映なし）かつ **Pr.609** ＝ “4” であれば PID 動作時に目標値となります。（設定範囲：0.00 ～ 100.00）*4*5 | no-units<br>(95) |
| 311 | PID measured value CMD*3 | C | PID 測定値を設定します。<br>• **Pr.128** ＝ “40 ～ 43” かつ **Pr.610** ＝ “4” であればダンサ制御時に測定値となります。（設定範囲：0.00 ～ 100.00）<br>• **Pr.128** ＝ “60 または 61” であれば PID 動作時に測定値となります。（設定範囲：0.00 ～ 100.00）*4<br>• **Pr.128** ＝ “1000 または 1001” かつ **Pr.610** ＝ “4” であれば PID 動作時に測定値となります。（設定範囲：0.00 ～ 100.00）*4<br>• **Pr.128** ＝ “2000 または 2001”（周波数反映なし）かつ **Pr.610** ＝ “4” であれば PID 動作時に測定値となります。（設定範囲：0.00 ～ 100.00）*4 | no-units<br>(95) |
| 312 | PID deviation CMD*3 | C | PID 偏差を設定します。(0.01 単位 )<br>• **Pr.128** ＝ “50 または 51” であれば PID 動作時に偏差となります。（設定範囲：-100.00 ～ 100.00）<br>• **Pr.128** ＝ “1010 または 1011” かつ **Pr.609** ＝ “4” であれば PID 動作時に偏差となります。（設定範囲：-100.00 ～ 100.00）<br>• **Pr.128** ＝ “2010 または 2011”（周波数反映なし）かつ **Pr.609** ＝ “4” であれば PID 動作時に偏差となります。（設定範囲：-100.00 ～ 100.00） | percent<br>(98) |
| 398 | Mailbox parameter | W | オブジェクトとして定義されていないプロパティへアクセスすることができます。(267 ページ参照 ) | no-units<br>(95) |
| 399 | Mailbox value | W | オブジェクトとして定義されていないプロパティへアクセスすることができます。(267 ページ参照 ) | no-units<br>(95) |
| 10007 | Acceleration time | W | **Pr.7 加速時間**を設定します。 | seconds<br>(73) |
| 10008 | Deceleration time | W | **Pr.8 減速時間**を設定します。 | seconds<br>(73) |

（注: 原本 p.265〜p.266 にまたがる1つの表。398/399 の内容欄は結合セルで、各行に展開した。）

*1 R：読出しのみ可能、W：読出し / 書込み可能（Commandable values 非対応）、C：読出し / 書込み可能（Commandable values 対応）
　Commandable values に対応したオブジェクトへの書込みは、運転モードなどの書込み条件が合わずに "Write Access Denied" が返信されても、設定範囲内の書込みであれば優先順位配列に格納されます。
*2 **Pr.37、Pr.53** の設定は無効となります。
*3 通信速度指令権が NET 以外の場合は、設定値は書き込まれますが動作には反映されません。
*4 **C42、C44** がともに≠ "9999" の場合、設定範囲は **C42、C44** の小さい係数～大きい係数までになります。また設定する値によっては書込み値と読出し値で最小桁の値が一致しない場合があります
*5 **Pr.133** ≠ “9999” の場合は **Pr.133** の設定が有効になります。

### （続き）3.6 BACnet MS/TP (3.6 / 印刷 p.266 / 原本 p.267)

##### ◆ （続き）サポートする BACnet オブジェクト (3.6 / 原本 p.267)

• バイナリ入力 (BINARY INPUT) (原本 p.267)

| オブジェクト識別子<br>Object Identifier | オブジェクト名<br>Object Name | Present Value<br>Access Type*1 | 内容<br>(0: Inactive、 1: Active) |
|---|---|---|---|
| 0 | Terminal STF*2 | R | 端子 STF の物理的な入力を示します。 |
| 1 | Terminal STR*2 | R | 端子 STR の物理的な入力を示します。 |
| 4 | Terminal RL*2 | R | 端子 RL の物理的な入力を示します。 |
| 5 | Terminal RM*2 | R | 端子 RM の物理的な入力を示します。 |
| 6 | Terminal RH*2 | R | 端子 RH の物理的な入力を示します。 |
| 8 | Terminal MRS*2 | R | 端子 MRS の物理的な入力を示します。 |
| 10 | Terminal RES*2 | R | 端子 RES の物理的な入力を示します。 |
| 100 | Terminal RUN | R | 端子 RUN の物理的な出力を示します。 |
| 104 | Terminal FU | R | 端子 FU の物理的な出力を示します。 |
| 105 | Terminal ABC | R | 端子 ABC の物理的な出力を示します。 |
| 107*3 | Terminal SO | R | 端子 SO の物理的な出力を示します。 |

*1 R：読出しのみ可能、W：読出し / 書込み可能（Commandable values 非対応）、C：読出し / 書込み可能（Commandable values 対応）
*2 FR-A8AC 装着時は端子 X1 ～ X7 の物理的な入力を示します。
*3 FR-E8TR、FR-E8TE7 装着時は機能なしとなります。

• バイナリ出力 (BINARY OUTPUT) (原本 p.267)

| オブジェクト識別子<br>Object Identifier | オブジェクト名<br>Object Name | Present Value<br>Access Type*1 | 内容<br>(0: Inactive、 1: Active) |
|---|---|---|---|
| 0 | Terminal RUN CMD | C | 端子 RUN の物理的な出力を制御します。<br>Pr.190 RUN 端子機能選択 ="82 または 182" の場合に制御可能 *2 になります。 |
| 4 | Terminal FU CMD | C | 端子 FU の物理的な出力を制御します。<br>Pr.191 FU 端子機能選択 ="82 または 182" の場合に制御可能 *2 になります。 |
| 5 | Terminal ABC CMD | C | 端子 ABC の物理的な出力を制御します。<br>Pr.192 ABC 端子機能選択 ="82 または 182" の場合に制御可能 *2 になります。 |

*1 R：読出しのみ可能、W：読出し / 書込み可能（Commandable values 非対応）、C：読出し / 書込み可能（Commandable values 対応）
Commandable values に対応したオブジェクトへの書込みは、運転モードなどの書込み条件が合わずに "Write Access Denied" が返信されても、設定範囲内の書込みであれば優先順位配列に格納されます。
*2 運転モード、操作指令権、運転指令権に関係なく動作します。

• バイナリ値 (BINARY VALUE) (原本 p.268)

| オブジェクト識別子<br>Object Identifier | オブジェクト名<br>Object Name | Present Value<br>Access Type*1 | 内容 |
|---|---|---|---|
| 0 | Inverter running | R | インバータ運転中 (RUN 信号 ) 状態を示します。 |
| 11 | Inverter operation ready | R | インバータ運転準備完了 (RY 信号 ) 状態を示します。 |
| 98 | Alarm output | R | 軽故障出力 (LF 信号 ) 状態を示します。 |
| 99 | Fault output | R | 異常出力 (ALM 信号 ) 状態を示します。 |
| 200 | Inverter running reverse | R | インバータ逆転中状態を示します。 |
| 302 | Control input instruction RL | C | 端子 RL に割り付けられている機能を制御します。<br>1 を設定した場合、Pr.180 RL 端子機能選択の信号が ON します。 |
| 303 | Control input instruction RM | C | 端子 RM に割り付けられている機能を制御します。<br>1 を設定した場合、Pr.181 RM 端子機能選択の信号が ON します。 |
| 304 | Control input instruction RH | C | 端子 RH に割り付けられている機能を制御します。<br>1 を設定した場合、Pr.182 RH 端子機能選択の信号が ON します。 |
| 306 | Control input instruction MRS | C | 端子 MRS に割り付けられている機能を制御します。<br>1 を設定した場合、Pr.183 MRS 端子機能選択の信号が ON します。 |
| 308 | Control input instruction RES*2 | C | 端子 RES に割り付けられている機能を制御します。<br>1 を設定した場合、Pr.184 RES 端子機能選択の信号が ON します。 |
| 400 | Run/Stop | C | 始動 / 停止指令を制御します。Speed scale 反映後に始動指令が書き込まれます。*3<br>1： 始動<br>0： 停止 |
| 401 | Forward/Reverse | C | 正転 / 逆転方向を制御します。*3<br>1： 逆転<br>0： 正転 |
| 402 | Fault reset | C | 異常出力状態をクリアします。<br>（リセットをせずに、インバータアラームを解除することが可能です。） |

*1 R：読出しのみ可能、W：読出し / 書込み可能（Commandable values 非対応）、C：読出し / 書込み可能（Commandable values 対応）
Commandable values に対応したオブジェクトへの書込みは、運転モードなどの書込み条件が合わずに "Write Access Denied" が返信されても、設定範囲内の書込みであれば優先順位配列に格納されます。
*2 リセット信号はネットワークで制御することはできないので、初期状態では Control input instruction RES は無効になります。Control input instruction RES を使用する場合は、Pr.184 RES 端子機能選択（FR-E800 取扱説明書（機能編）参照）で信号を変更してください。（リセットは ReinitializeDevice で実行可能です。）
*3 通信運転指令権が NET 以外の場合は、設定値は書き込まれるが動作には反映されません。

• デバイス (DEVICE) (原本 p.268)

| オブジェクト識別子<br>Object Identifier | オブジェクト名<br>Object Name | 内容 |
|---|---|---|
| 0 ～ 4194302 | 機種情報 # デバイスインスタンス番号 | デバイスの状態読出し、または設定変更を行います。<br>デバイスインスタンス番号：Pr.728×10000 ＋ Pr.729 |
| 4194303*1 | 機種情報 # デバイスインスタンス番号 | デバイスの状態読出し、または設定変更を行います。<br>デバイスインスタンス番号：Pr.728×10000 ＋ Pr.729 |

（注: オブジェクト名・内容は 0 ～ 4194302 と 4194303 の2行で結合セル。各行に展開した）

*1 Read Property Service のみ有効です。

• ネットワークポート (NETWORK PORT) (原本 p.268)

| オブジェクト識別子<br>Object Identifier | オブジェクト名<br>Object Name | 内容 |
|---|---|---|
| 0 | BACnetMSTP on EIA-485 | PU コネクタの状態読出し、または設定変更を行います。 |
| 4194303*1 | 要求を受信した PORT のオブジェクト識別子としてアクセスします。 | 要求を受信した PORT のオブジェクト識別子としてアクセスします。 |

（注: 4194303 の行はオブジェクト名・内容の列が結合セル。各列に展開した）

*1 Read Property Service のみ有効です。

##### ◆ Mailbox parameter と Mailbox value (BACnet registers) (3.6 / 原本 p.268)

• Mailbox parameter と Mailbox value を使用することで、オブジェクトとして定義されていないプロパティへアクセスすることができます。
• 読出しの場合は読み出したいプロパティのレジスタを「Mailbox parameter」に書き込み、「Mailbox value」を読み出してください。書込みの場合は書き込みたいプロパティのレジスタを「Mailbox parameter」に書き込み、「Mailbox value」にデータを書き込んでください。

• システム環境変数 (原本 p.269)

| レジスタ | 定義 | 読出 / 書込 | 備考 |
|---|---|---|---|
| 40010 | 運転モード／インバータ設定 | 読出 / 書込 | 書込み時は運転モード設定としてデータを設定します。<br>読出し時は運転モード状態としてデータが読み出されます。 |

＜運転モード／インバータ設定＞

| モード | 読出し値 | 書込み値 |
|---|---|---|
| EXT | H0000 | H0010 *1 |
| PU | H0001 | H0011 *1 |
| EXT<br>JOG | H0002 | ─ |
| PU<br>JOG | H0003 | ─ |
| NET | H0004 | H0014 |
| PU ＋<br>EXT | H0005 | ─ |

*1 書込み可否は Pr.79、Pr.340 の設定により異なります。詳細は FR-E800 取扱説明書（機能編）を参照してください。
運転モードによる制約は、計算機リンクの仕様に準じます。

• モニタコード
レジスタ番号およびモニタ項目については FR-E800 取扱説明書（機能編）の Pr.52 の内容を参照してください。

• パラメータ (原本 p.269〜270)

| Pr. | レジスタ | パラメータ名称 | 読出 / 書込 | 備考 |
|---|---|---|---|---|
| 0 ～ 999 | 41000 ～<br>41999 | パラメータ名称はパラメータ一覧（FR-E800 取扱説明書（機能編））参照 | 読出 / 書込 | パラメータ番号 +41000 がレジスタ番号になります。 |
| C2(902) | 41902 | 端子 2 周波数設定バイアス周波数 | 読出 / 書込 | |
| C3(902) | 42092 | 端子 2 周波数設定バイアス（アナログ値） | 読出 / 書込 | C3(902) に設定されているアナログ値 (%) |
| C3(902) | 43902 | 端子 2 周波数設定バイアス（端子アナログ値） | 読出 | 端子 2 に印加されている電圧（電流）のアナログ値 (%) |
| 125(903) | 41903 | 端子 2 周波数設定ゲイン周波数 | 読出 / 書込 | |
| C4(903) | 42093 | 端子 2 周波数設定ゲイン（アナログ値） | 読出 / 書込 | C4(903) に設定されているアナログ値 (%) |
| C4(903) | 43903 | 端子 2 周波数設定ゲイン（端子アナログ値） | 読出 | 端子 2 に印加されている電圧（電流）のアナログ値 (%) |
| C5(904) | 41904 | 端子 4 周波数設定バイアス周波数 | 読出 / 書込 | |
| C6(904) | 42094 | 端子 4 周波数設定バイアス（アナログ値） | 読出 / 書込 | C6(904) に設定されているアナログ値 (%) |
| C6(904) | 43904 | 端子 4 周波数設定バイアス（端子アナログ値） | 読出 | 端子 4 に印加されている電流（電圧）のアナログ値 (%) |
| 126(905) | 41905 | 端子 4 周波数設定ゲイン周波数 | 読出 / 書込 | |
| C7(905) | 42095 | 端子 4 周波数設定ゲイン（アナログ値） | 読出 / 書込 | C7(905) に設定されているアナログ値 (%) |
| C7(905) | 43905 | 端子 4 周波数設定ゲイン（端子アナログ値） | 読出 | 端子 4 に印加されている電流（電圧）のアナログ値 (%) |
| C12(917) | 41917 | 端子 1 バイアス周波数（速度） | 読出 / 書込 | FR-E8AXY 装着時のみ |
| C13(917) | 42107 | 端子 1 バイアス（速度）（アナログ値） | 読出 / 書込 | C13(917) に設定されているアナログ値 (%)（FR-E8AXY 装着時のみ） |
| C13(917) | 43917 | 端子 1 バイアス（速度）（端子アナログ値） | 読出 | 端子 1 に印加されている電圧のアナログ値 (%)（FR-E8AXY 装着時のみ） |
| C14(918) | 41918 | 端子 1 ゲイン周波数（速度） | 読出 / 書込 | FR-E8AXY 装着時のみ |
| C15(918) | 42108 | 端子 1 ゲイン（速度）（アナログ値） | 読出 / 書込 | C15(918) に設定されているアナログ値 (%)（FR-E8AXY 装着時のみ） |
| C15(918) | 43918 | 端子 1 ゲイン（速度）（端子アナログ値） | 読出 | 端子 1 に印加されている電圧のアナログ値 (%)（FR-E8AXY 装着時のみ） |
| C16(919) | 41919 | 端子 1 バイアス指令（トルク） | 読出 / 書込 | FR-E8AXY 装着時のみ |
| C17(919) | 42109 | 端子 1 バイアス（トルク）（アナログ値） | 読出 / 書込 | C17(919) に設定されているアナログ値 (%)（FR-E8AXY 装着時のみ） |
| C17(919) | 43919 | 端子 1 バイアス（トルク）（端子アナログ値） | 読出 | 端子 1 に印加されている電圧のアナログ値 (%)（FR-E8AXY 装着時のみ） |
| C18(920) | 41920 | 端子 1 ゲイン指令（トルク） | 読出 / 書込 | FR-E8AXY 装着時のみ |
| C19(920) | 42110 | 端子 1 ゲイン（トルク）（アナログ値） | 読出 / 書込 | C19(920) に設定されているアナログ値 (%)（FR-E8AXY 装着時のみ） |
| C19(920) | 43920 | 端子 1 ゲイン（トルク）（端子アナログ値） | 読出 | 端子 1 に印加されている電圧のアナログ値 (%)（FR-E8AXY 装着時のみ） |
| C38(932) | 41932 | 端子 4 バイアス指令（トルク） | 読出 / 書込 | |
| C39(932) | 42122 | 端子 4 バイアス（トルク）（アナログ値） | 読出 / 書込 | C39(932) に設定されているアナログ値 (%) |
| C39(932) | 43932 | 端子 4 バイアス（トルク）（端子アナログ値） | 読出 | 端子 4 に印加されている電流（電圧）のアナログ値 (%) |
| C40(933) | 41933 | 端子 4 ゲイン指令（トルク） | 読出 / 書込 | |
| C41(933) | 42123 | 端子 4 ゲイン（トルク）（アナログ値） | 読出 / 書込 | C41(933) に設定されているアナログ値 (%) |
| C41(933) | 43933 | 端子 4 ゲイン（トルク）（端子アナログ値） | 読出 | 端子 4 に印加されている電流（電圧）のアナログ値 (%) |
| C42(934) | 41934 | PID 表示バイアス係数 | 読出 / 書込 | |
| C43(934) | 42124 | PID 表示バイアスアナログ値 | 読出 / 書込 | C43(934) に設定されているアナログ値 (%) |
| C43(934) | 43934 | PID 表示バイアスアナログ値（端子アナログ値） | 読出 | 端子 4 に印加されている電流（電圧）のアナログ値 (%) |
| C44(935) | 41935 | PID 表示ゲイン係数 | 読出 / 書込 | |
| C45(935) | 42125 | PID 表示ゲインアナログ値 | 読出 / 書込 | C45(935) に設定されているアナログ値 (%) |
| C45(935) | 43935 | PID 表示ゲインアナログ値（端子アナログ値） | 読出 | 端子 4 に印加されている電流（電圧）のアナログ値 (%) |
| 1000 ～<br>1999 | 45000 ～<br>45999 | パラメータ名称はパラメータ一覧（FR-E800 取扱説明書（機能編））参照 | 読出 / 書込 | パラメータ番号 +44000 がレジスタ番号になります。 |

（注: C3/C4/C6/C7/C13/C15/C17/C19/C39/C41/C43/C45 の Pr. 欄は原本では2行結合セル。各行に展開した。C19(920) 以降は原本 p.270 に表の続きとして掲載）

• アラーム履歴 (原本 p.270)

| レジスタ | 定義 | 読出 / 書込 | 備考 |
|---|---|---|---|
| 40501 | アラーム履歴 1 | 読出 / 書込 | データは 2byte のため "H00 ○○ " で格納されます。<br>下位 1byte にエラーコードを参照できます。（エラーコードは FR-E800 取扱説明書（保守編）の異常表示一覧を参照）<br>レジスタ 40501 に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 |
| 40502 | アラーム履歴 2 | 読出 | データは 2byte のため "H00 ○○ " で格納されます。<br>下位 1byte にエラーコードを参照できます。（エラーコードは FR-E800 取扱説明書（保守編）の異常表示一覧を参照）<br>レジスタ 40501 に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 |
| 40503 | アラーム履歴 3 | 読出 | データは 2byte のため "H00 ○○ " で格納されます。<br>下位 1byte にエラーコードを参照できます。（エラーコードは FR-E800 取扱説明書（保守編）の異常表示一覧を参照）<br>レジスタ 40501 に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 |
| 40504 | アラーム履歴 4 | 読出 | データは 2byte のため "H00 ○○ " で格納されます。<br>下位 1byte にエラーコードを参照できます。（エラーコードは FR-E800 取扱説明書（保守編）の異常表示一覧を参照）<br>レジスタ 40501 に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 |
| 40505 | アラーム履歴 5 | 読出 | データは 2byte のため "H00 ○○ " で格納されます。<br>下位 1byte にエラーコードを参照できます。（エラーコードは FR-E800 取扱説明書（保守編）の異常表示一覧を参照）<br>レジスタ 40501 に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 |
| 40506 | アラーム履歴 6 | 読出 | データは 2byte のため "H00 ○○ " で格納されます。<br>下位 1byte にエラーコードを参照できます。（エラーコードは FR-E800 取扱説明書（保守編）の異常表示一覧を参照）<br>レジスタ 40501 に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 |
| 40507 | アラーム履歴 7 | 読出 | データは 2byte のため "H00 ○○ " で格納されます。<br>下位 1byte にエラーコードを参照できます。（エラーコードは FR-E800 取扱説明書（保守編）の異常表示一覧を参照）<br>レジスタ 40501 に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 |
| 40508 | アラーム履歴 8 | 読出 | データは 2byte のため "H00 ○○ " で格納されます。<br>下位 1byte にエラーコードを参照できます。（エラーコードは FR-E800 取扱説明書（保守編）の異常表示一覧を参照）<br>レジスタ 40501 に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 |
| 40509 | アラーム履歴 9 | 読出 | データは 2byte のため "H00 ○○ " で格納されます。<br>下位 1byte にエラーコードを参照できます。（エラーコードは FR-E800 取扱説明書（保守編）の異常表示一覧を参照）<br>レジスタ 40501 に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 |
| 40510 | アラーム履歴 10 | 読出 | データは 2byte のため "H00 ○○ " で格納されます。<br>下位 1byte にエラーコードを参照できます。（エラーコードは FR-E800 取扱説明書（保守編）の異常表示一覧を参照）<br>レジスタ 40501 に書込みを行うことでアラーム履歴一括クリアとなります。<br>データは任意の値を設定してください。 |

（注: 備考欄は原本では 40501〜40510 の全10行で1つの結合セル。各行に全文を展開した）

• 機種情報モニタ (原本 p.270)

| レジスタ | 定義 | 読出 / 書込 | 備考 |
|---|---|---|---|
| 44001 | 機種名（1 文字目、2 文字目） | 読出 | 機種名を ASCII コードで読出し可能<br>空白部分は、"H20"（空白コード）がセットされる<br>例）"FR-E840-1（FM タイプ）" の場合、<br>H46,H52,H2D,H45,H38,H34,H30,H2D,H31,H20・・・H20 |
| 44002 | 機種名（3 文字目、4 文字目） | 読出 | 機種名を ASCII コードで読出し可能<br>空白部分は、"H20"（空白コード）がセットされる<br>例）"FR-E840-1（FM タイプ）" の場合、<br>H46,H52,H2D,H45,H38,H34,H30,H2D,H31,H20・・・H20 |
| 44003 | 機種名（5 文字目、6 文字目） | 読出 | 機種名を ASCII コードで読出し可能<br>空白部分は、"H20"（空白コード）がセットされる<br>例）"FR-E840-1（FM タイプ）" の場合、<br>H46,H52,H2D,H45,H38,H34,H30,H2D,H31,H20・・・H20 |
| 44004 | 機種名（7 文字目、8 文字目） | 読出 | 機種名を ASCII コードで読出し可能<br>空白部分は、"H20"（空白コード）がセットされる<br>例）"FR-E840-1（FM タイプ）" の場合、<br>H46,H52,H2D,H45,H38,H34,H30,H2D,H31,H20・・・H20 |
| 44005 | 機種名（9 文字目、10 文字目） | 読出 | 機種名を ASCII コードで読出し可能<br>空白部分は、"H20"（空白コード）がセットされる<br>例）"FR-E840-1（FM タイプ）" の場合、<br>H46,H52,H2D,H45,H38,H34,H30,H2D,H31,H20・・・H20 |
| 44006 | 機種名（11 文字目、12 文字目） | 読出 | 機種名を ASCII コードで読出し可能<br>空白部分は、"H20"（空白コード）がセットされる<br>例）"FR-E840-1（FM タイプ）" の場合、<br>H46,H52,H2D,H45,H38,H34,H30,H2D,H31,H20・・・H20 |
| 44007 | 機種名（13 文字目、14 文字目） | 読出 | 機種名を ASCII コードで読出し可能<br>空白部分は、"H20"（空白コード）がセットされる<br>例）"FR-E840-1（FM タイプ）" の場合、<br>H46,H52,H2D,H45,H38,H34,H30,H2D,H31,H20・・・H20 |
| 44008 | 機種名（15 文字目、16 文字目） | 読出 | 機種名を ASCII コードで読出し可能<br>空白部分は、"H20"（空白コード）がセットされる<br>例）"FR-E840-1（FM タイプ）" の場合、<br>H46,H52,H2D,H45,H38,H34,H30,H2D,H31,H20・・・H20 |
| 44009 | 機種名（17 文字目、18 文字目） | 読出 | 機種名を ASCII コードで読出し可能<br>空白部分は、"H20"（空白コード）がセットされる<br>例）"FR-E840-1（FM タイプ）" の場合、<br>H46,H52,H2D,H45,H38,H34,H30,H2D,H31,H20・・・H20 |
| 44010 | 機種名（19 文字目、20 文字目） | 読出 | 機種名を ASCII コードで読出し可能<br>空白部分は、"H20"（空白コード）がセットされる<br>例）"FR-E840-1（FM タイプ）" の場合、<br>H46,H52,H2D,H45,H38,H34,H30,H2D,H31,H20・・・H20 |
| 44011 | 容量（1 文字目、2 文字目） | 読出 | インバータ容量を ASCII コードで読出し可能<br>読出しデータは、0.1kW 単位で、0.01kW 単位は切り捨てる<br>空白部分は、"H20"（空白コード）がセットされる<br>例）0.75K・・・"　7"（H20,H20,H20,H20,H20,H37） |
| 44012 | 容量（3 文字目、4 文字目） | 読出 | インバータ容量を ASCII コードで読出し可能<br>読出しデータは、0.1kW 単位で、0.01kW 単位は切り捨てる<br>空白部分は、"H20"（空白コード）がセットされる<br>例）0.75K・・・"　7"（H20,H20,H20,H20,H20,H37） |
| 44013 | 容量（5 文字目、6 文字目） | 読出 | インバータ容量を ASCII コードで読出し可能<br>読出しデータは、0.1kW 単位で、0.01kW 単位は切り捨てる<br>空白部分は、"H20"（空白コード）がセットされる<br>例）0.75K・・・"　7"（H20,H20,H20,H20,H20,H37） |

（注: 備考欄は原本では 44001〜44010 の10行、44011〜44013 の3行がそれぞれ1つの結合セル。各行に全文を展開した）

> **NOTE**
> • 32bit サイズのパラメータ設定値やモニタ内容を読み出した場合に、読出し値が HFFFF を超えていると、返信データは HFFFF となります。

##### ◆ ANNEX A - PROTOCOL IMPLEMENTATION CONFORMANCE STATEMENT (NORMATIVE) (3.6 / 原本 p.271)

(This annex is part of this Standard and is required for its use.)

**BACnet Protocol Implementation Conformance Statement**

- Date: 1st Sep 2021
- Vendor Name: Mitsubishi Electric Corporation
- Product Name: Inverter
- Product Model Number: (FR-E800 series)
- Application Software Version: 8650F
- Firmware Revision: 1.00
- BACnet Protocol Revision: 19

**Product Description:**
（注: 原本は記入欄（下線3本）のみで記載なし）

**BACnet Standardized Device Profile (Annex L):**
（注: [x] はチェックあり（☒）、[ ] はチェックなし（☐）。原本の画像で確認）

- [ ] BACnet Cross-Domain Advanced Operator Workstation (B-XAWS)
- [ ] BACnet Advanced Operator Workstation (B-AWS)
- [ ] BACnet Operator Workstation (B-OWS)
- [ ] BACnet Operator Display (B-OD)
- [ ] BACnet Advanced Life Safety Workstation (B-ALSWS)
- [ ] BACnet Life Safety Workstation (B-LSWS)
- [ ] BACnet Life Safety Annunciator Panel (B-LSAP)
- [ ] BACnet Advanced Access Control Workstation (B-AACWS)
- [ ] BACnet Access Control Workstation (B-ACWS)
- [ ] BACnet Access Control Security Display (B-ACSD)
- [ ] BACnet Building Controller (B-BC)
- [ ] BACnet Advanced Application Controller (B-AAC)
- [x] BACnet Application Specific Controller (B-ASC)
- [ ] BACnet Smart Sensor (B-SS)
- [ ] BACnet Smart Actuator (B-SA)
- [ ] BACnet Advanced Life Safety Controller (B-ALSC)
- [ ] BACnet Life Safety Controller (B-LSC)
- [ ] BACnet Advanced Access Control Controller (B-AACC)
- [ ] BACnet Access Control Controller (B-ACC)
- [ ] BACnet Router (B-RTR)
- [ ] BACnet Gateway (B-GW)
- [ ] BACnet Broadcast Management Device (B-BBMD)
- [ ] BACnet Access Control Door Controller (B-ACDC)
- [ ] BACnet Access Control Credential Reader (B-ACCR)
- [ ] BACnet General (B-GENERAL)

**List all BACnet Interoperability Building Blocks Supported (Annex K):** (原本 p.272)
DS-RP-B, DS-WP-B, DM-DDB-B, DM-DOB-B, DM-DCC-B , DM-RD-B

**Segmentation Capability:**

- [ ] Able to transmit segmented messages　Window Size ＿＿＿＿（注: 空欄）
- [ ] Able to receive segmented messages　Window Size ＿＿＿＿（注: 空欄）

**Standard Object Types Supported:**
An object type is supported if it may be present in the device. For each standard Object Type supported provide the following data:

1. Whether objects of this type are dynamically creatable using the CreateObject service
2. Whether objects of this type are dynamically deletable using the DeleteObject service
3. List of the optional properties supported
4. List of all properties that are writable where not otherwise required by this standard
5. List of all properties that are conditionally writable where not otherwise required by this standard
6. List of proprietary properties and for each its property identifier, datatype, and meaning
7. List of any property range restrictions

Dynamic object creation and deletion is not supported.
標準仕様品でサポートしているオブジェクトタイプは 263 ページを参照してください。

**Data Link Layer Options:**

- [ ] ARCNET (ATA 878.1), 2.5 Mb. (Clause 8)
- [ ] ARCNET (ATA 878.1), EIA-485 (Clause 8), baud rate(s) ＿＿＿＿（注: 空欄）
- [ ] BACnet IP, (Annex J)
- [ ] BACnet IP, (Annex J), BACnet Broadcast Management Device (BBMD)
- [ ] BACnet IP, (Annex J), Network Address Translation (NAT Traversal)
- [ ] BACnet IPv6, (Annex U)
- [ ] BACnet IPv6, (Annex U), BACnet Broadcast Management Device (BBMD)
- [ ] BACnet/ZigBee (Annex O) ＿＿＿＿（注: 空欄）
- [ ] ISO 8802-3, Ethernet (Clause 7)
- [x] MS/TP master (Clause 9), baud rate(s): 9600, 19200, 38400, 57600, 76800, 115200
- [ ] MS/TP slave (Clause 9), baud rate(s): ＿＿＿＿（注: 空欄）
- [ ] Point-To-Point, EIA 232 (Clause 10), baud rate(s): ＿＿＿＿（注: 空欄）
- [ ] Point-To-Point, modem, (Clause 10), baud rate(s):
- [ ] Other: ＿＿＿＿（注: 空欄）

**Device Address Binding:**
Is static device binding supported? (This is currently necessary for two-way communication with MS/TP slaves and certain other devices.)　☐ Yes　☒ No

**Networking Options:**

- [ ] Router, Clause 6 - List all routing configurations, e.g., ARCNET-Ethernet, Ethernet-MS/TP, etc.
- [ ] Annex H, BACnet Tunneling Router over IP

**Character Sets Supported:** (原本 p.273)
Indicating support for multiple character sets does not imply that they can all be supported simultaneously.

- [ ] ISO 10646 (UTF-8)
- [ ] IBM™/Microsoft™ DBCS
- [ ] ISO 8859-1
- [ ] ISO 10646 (UCS-2)
- [ ] ISO 10646 (UCS-4)
- [ ] JIS X 0208

（注: 原本は3列×2行の配置。左列 UTF-8 / UCS-2、中列 IBM™/Microsoft™ DBCS / UCS-4、右列 ISO 8859-1 / JIS X 0208）

**Gateway Options:**
If this product is a communication gateway, describe the types of non-BACnet equipment/networks(s) that the gateway supports:
（注: 原本は記入欄（下線3本）のみで記載なし）

If this product is a communication gateway which presents a network of virtual BACnet devices, a separate PICS shall be provided that describes the functionality of the virtual BACnet devices. That PICS shall describe a superset of the functionality of all types of virtual BACnet devices that can be presented by the gateway.

**Network Security Options:**

- [ ] Non-secure Device - is capable of operating without BACnet Network Security
- [ ] Secure Device - is capable of using BACnet Network Security (NS-SD BIBB)
- [ ] Multiple Application-Specific Keys
- [ ] Supports encryption (NS-ED BIBB)
- [ ] Key Server (NS-KS BIBB)


---

## 転記時の要確認一覧 (3.6 / 原本 p.259-273)

（注: 転記担当が記録した、原本の不整合・判読上の注意。原文はいずれも原本どおり転記済み）

1. 原本 p.262〜263「サポートする BACnet 標準オブジェクトタイプとプロパティ」表で、アナログ出力 (Analog Output) 列は Property List と Current Command Priority のみ R で、Object Identifier / Object Name / Object Type / Present Value / Unit 等が空欄になっている。一方 p.265 のアナログ出力オブジェクト（Terminal FM / AM）は Present Value Access Type＝C、単位 percent を持つ。また Current Command Priority は AO と BO に R だが、Present Value が C/C*1 の AV・BV には付いていない。列ずれ等の原本不整合の可能性あり（画像の列位置どおりに転記済み）。
2. 原本 p.263「アプリケーションソフトウェアバージョン」の詳細「インバータのソフトフェアバージョン」は原文のまま（「ソフトウェア」の誤記と思われる）。
3. アナログ値 (ANALOG VALUE) 表は原本 p.266 で 10008 Deceleration time の後に脚注 *1〜*5 があり終わっている。p.267 以降（バイナリ系オブジェクト等）は担当範囲外。

- 機種情報モニタ「容量」の例「0.75K・・・" 7"」：原本では " と 7 の間の空白数が画像から判別しにくい（H20 が5個なので5文字分の空白と推定されるが、原本表記は「" 7"」のまま全角空白1つで転記）。(原本 p.270)
- 原本 p.274 は第4章の章扉。`## 4 その他通信` 見出しと章内目次を本パートに含めたため、次パート（4.1〜）で章見出しを重複させないよう統合時に確認が必要。
