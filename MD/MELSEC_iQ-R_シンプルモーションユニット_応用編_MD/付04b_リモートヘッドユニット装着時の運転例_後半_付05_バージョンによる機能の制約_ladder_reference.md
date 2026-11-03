# 三菱 MELSEC iQ-R シンプルモーションユニット ユーザーズマニュアル(応用編) 付録 付4 リモートヘッドユニット装着時の運転例[RD77MS](後半: プログラム例の続き・動作・制約事項・GX Works3対応バージョン)／付5 バージョンによる機能の制約

| 項目 | 内容 |
|---|---|
| 原本 | 三菱電機 MELSEC iQ-R シンプルモーションユニット ユーザーズマニュアル(応用編)(形名 RD77-U-APP) |
| 発行元 | 三菱電機株式会社 |
| 資料番号・版数 | IB(名)-0300246-P (2509)MEE / P版 (2025年9月作成) |
| 対象形名 | RD77MS2 / RD77MS4 / RD77MS8 / RD77MS16 / RD77GF4 / RD77GF8 / RD77GF16 / RD77GF32 |
| 原本PDF | `PDF/MELSEC iQ_Rシンプルモーションユニットユーザーズマニュアル(応用編).pdf` |
| 本ファイルの範囲 | 付4 リモートヘッドユニット装着時の運転例[RD77MS] のうち「プログラム例」の続き(「原点復帰要求OFFプログラム」ステップ(328)から「停止プログラム」ステップ(1416) ENDまで)、「リモートヘッドユニット装着時のRD77MSの動作」「リモートヘッドユニット装着時の制約事項」「GX Works3の対応バージョン」、および付5 バージョンによる機能の制約 全部。印刷 p.807-824 / PDF p.809-826。前ファイル(付04a)は付4の冒頭〜プログラム例の途中(印刷 p.806 / PDF p.808 以前。システム構成例、各局の設定、グローバルラベル一覧、ステップ(328)より前の回路)。索引(PDF p.827〜)は本ファイルの範囲外 |
| ページ対応 | 印刷ページ = PDFページ − 2。本文中の「〇〇ページ参照」は印刷ページのまま |
| 変換日 | 2026-10-23 |
| 変換方法 | pypdfium2(本文) + PyMuPDF 200dpi 画像の目視(全ページ) |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。

**転記上の扱い**: 原本のプログラム例はすべてラダー図(画像)のみでニモニックの記載が無いため、全回路を図から書き起こした(ステップ番号は原本の回路左端の番号)。ラベル名・デバイス名は原本の表記どおり(「Memmory」等の綴りも原本どおり)とし、ニモニックでは「ラベル名 + 割付けデバイス」を並べ、多オペランド命令(JP.REMFR／JP.REMTO)は `ラベル名(デバイス)` の形で1行に書いた。分岐は MPS／MRD／MPP、並列ブロックは ORB／ANB で表した(GX Works3 が出力するニモニックと完全一致するとは限らない)。JP.REMFR／JP.REMTO のオペランドは原本の並び(J1, 要求番号K, 局番K1, H0, バッファメモリアドレス, 読出し先/書込み元, ワード数, 完了ステータス)のまま。比較命令は原本の表示(`<>_U`、`=_U`、`=`、`<>`)のまま区別した。付5の表の縦結合セルは各行に展開し、セル内改行は `<br>` とした。原本の参照記号は「☞」で表記し、参照先は印刷ページのまま。「SSCNETⅢ/H」の「Ⅲ」、「αSTEP」の「α」、「ON→OFF」の「→」はテキスト抽出で欠落していたため画像を正とした。

## 主要用語 対訳表 (Glossary) (付4〜付5 / 原本 p.809-826)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| リモートヘッドユニット | Remote head module | RJ72GF15-T2 | 参考訳 |
| 解列 / 復列 | Disconnection / Reconnection (return) | — | 参考訳 |
| リモートヘッドユニット二重化システム | Redundant system with remote head modules | — | 参考訳 |
| CPUエラー時出力モード設定 | Output mode setting at CPU error | 0: クリア | 参考訳 |
| シーケンサレディ信号 | PLC READY signal | [Y0] / bPLCReady | 参考訳 |
| 全軸サーボオン信号 | All axis servo ON signal | [Y1] / bAllAxisServoOn | 参考訳 |
| 運転中シーケンサレディ OFF | PLC READY OFF during operation | エラーコード 1900H | 参考訳 |
| エラーリセット | Error reset | — | 参考訳 |
| エラー検出信号 / ワーニング検出信号 | Error detection signal / Warning detection signal | W0.D / W0.9(軸1) | 参考訳 |
| 位置決め始動信号 | Positioning start signal | [Y10] / bnPositioningStart[ ] | 参考訳 |
| Mコード | M code | bMcodeOn_Axis1 | 参考訳 |
| 原点復帰要求OFF | Home position return request flag OFF | — | 参考訳 |
| 原点復帰未完時動作設定 | Operation setting for incompletion of home position return | — | 参考訳 |
| 機械原点復帰 / 高速原点復帰 | Machine home position return / Fast home position return | 9001 / 9002 | 参考訳 |
| 外部指令機能 | External command function | — | 参考訳 |
| 位置決め始動番号 | Positioning start No. | uPositioningStartNo | 参考訳 |
| 速度・位置切換え制御 / 位置・速度切換え制御 | Speed-position switching control / Position-speed switching control | — | 参考訳 |
| 高度な位置決め制御 | Advanced positioning control | 7000 | 参考訳 |
| JOG運転 / インチング運転 | JOG operation / Inching operation | — | 参考訳 |
| 手動パルサ運転 | Manual pulse generator operation | MPG | 参考訳 |
| 速度変更 / オーバーライド | Speed change / Override | — | 参考訳 |
| 加減速時間変更 | Acceleration/deceleration time change | — | 参考訳 |
| ステップ運転 / スキップ | Step operation / Skip | — | 参考訳 |
| 連続運転中断 | Continuous operation interrupt | — | 参考訳 |
| 目標位置変更 / 再始動 | Target position change / Restart | — | 参考訳 |
| パラメータ初期化 / フラッシュ ROM書込み | Parameter initialization / Flash ROM write | — | 参考訳 |
| ユニットラベル / ユニットFB | Module label / Module FB | — | 参考訳 |
| 自動リフレッシュ | Auto refresh | — | 参考訳 |
| 専用命令 / 割込み機能 | Dedicated instruction / Interrupt function | — | 参考訳 |
| ユニット間同期 | Inter-module synchronization | — | 参考訳 |
| ソフトウェアバージョン | Software version | Ver.xx | 参考訳 |
| エンジニアリングツール | Engineering tool | GX Works3 | 参考訳 |
| 光分岐ユニット | Optical hub unit | — | 参考訳 |
| オフラインデジタルオシロ | Offline digital oscilloscope | — | 参考訳 |
| 制御モード切換え時速度制限値取込み選択 | Speed limit value input selection at control mode switching | [Pr.127] | 参考訳 |
| トルク制限選択(ステッピングドライバ) | Torque limit selection (stepping driver) | [Pr128] | 参考訳 |
| 局単位ブロック保証 | Block data assurance per station | — | 参考訳 |
| 安全通信機能 | Safety communication function | — | 参考訳 |

## 変換範囲表 (付4〜付5 / 原本 p.809-826)

| 原本ページ | 節 | 扱い |
|---|---|---|
| p.793-808 | 付4 冒頭〜プログラム例(ステップ(328)より前) | 前ファイル(付04a)で変換 |
| p.809-823 | 付4 プログラム例(原点復帰要求OFFプログラム〜停止プログラム、ステップ(328)〜(1416)) | 全文(全回路をニモニックで図から書き起こし) |
| p.824 | 付4 リモートヘッドユニット装着時のRD77MSの動作／制約事項／GX Works3の対応バージョン | 全文 |
| p.825-826 | 付5 バージョンによる機能の制約([RD77MS] 23行、[RD77GF] 10行、機種別対応バージョン 2行) | 全文 |
| p.827〜 | 索引ほか | 未変換(本ファイルの範囲外。改訂履歴等は別ファイル) |

## 目次

- 付録
  - 付4 リモートヘッドユニット装着時の運転例[RD77MS](後半)
    - プログラム例(続き): 原点復帰要求OFF／外部指令機能有効設定／シーケンサレディ信号[Y0]+全軸サーボオン信号[Y1] ON／位置決め始動番号設定／位置決め始動／MコードOFF／JOG運転設定／インチング運転設定／JOG運転・インチング運転実行／手動パルサ運転／速度変更／オーバーライド／加減速時間変更／ステップ運転／スキップ／連続運転中断／目標位置変更／再始動／パラメータ初期化／フラッシュ ROM書込み／エラーリセット／停止
    - リモートヘッドユニット装着時のRD77MSの動作
    - リモートヘッドユニット装着時の制約事項
    - GX Works3の対応バージョン
  - 付5 バージョンによる機能の制約([RD77MS]／[RD77GF])

## 付録 (付録 / 印刷 p.807-824 / 原本 p.809-826)

### 付4 リモートヘッドユニット装着時の運転例[RD77MS](続き) (付4 / 印刷 p.807-822 / 原本 p.809-824)

#### プログラム例(続き) (付4 / 印刷 p.807-821 / 原本 p.809-823)

前ファイル(付04a)から続く。プログラムはマスタ局のCPUユニットに書き込む(前ファイル記載)。使用ラベルの定義(グローバルラベル一覧・配列化したラベルの内容)は前ファイルを参照。

##### 原点復帰要求OFFプログラム (付4 / 印刷 p.807 / 原本 p.809)

エンジニアリングツールの"ユニットパラメータ"にて，"原点復帰未完時動作設定"を"1: 位置決め制御"を実行するに設定した場合，本プログラムは不要です。

【図】ラダー図(図から書き起こし)。リモートヘッドユニット経由のため、RD77MSのバッファメモリは JP.REMFR(読出し)／JP.REMTO(書込み)で D デバイスとの間で受け渡す。
- ステップ(328): bInputOPR_RequestFlagOffRequest(X20)のa接点で bOPR_RequestFlagOffRequestPulse(M1)をPLS。
- ステップ(332): M1のa接点、bnPositioningStart[0](Y110)のb接点、bStartComplete_Axis1(W0.E)のb接点の直列で bOPR_RequestFlagOffRequestMemmory(M2)をSET。
- ステップ(336): M2のa接点の後で分岐。1段目は JP.REMFR J1 K1 K1 H0 K2417 で uStatus(D0)へ1ワード読出し(完了ステータス bStatusRet(M5100))。2段目は bStatusRet[0](M5100)のa接点、bStatusRet[1](M5101)のb接点を経てさらに分岐し、uStatus.3(D0.3)のa接点で bOPR_RequestFlagOffRequest(M0)をSET、もう一方で M2 をRST。
- ステップ(358): M0のa接点の後で分岐。1段目 MOVP K1 → uOPR_RequestFlagOffRequestSetting(D82)。2段目 JP.REMTO J1 K2 K1 H0 K4321 で D82 を1ワード書込み(完了ステータス bOPR_RequestFlagOffRet1(M5110))。3段目は bOPR_RequestFlagOffRet1[0](M5110)のa接点、bOPR_RequestFlagOffRet1[1](M5111)のb接点を経て分岐し、M0 をRST、bOPR_RequestFlagOffRequestConfirmationPulse(M60)をSET。
- ステップ(380): M60のa接点の後で分岐。JP.REMFR J1 K3 K1 H0 K4321 で D82 へ1ワード読出し(完了ステータス bOPR_RequestFlagOffRet2(M5120))、もう一方で M60 をRST。
- ステップ(396): bOPR_RequestFlagOffRet2[0](M5120)のa接点、bOPR_RequestFlagOffRet2[1](M5121)のb接点、比較 <>_U uOPR_RequestFlagOffRequestSetting(D82) K0 の成立で M60 をSET。

```
(328) LD       bInputOPR_RequestFlagOffRequest                    X20
      PLS      bOPR_RequestFlagOffRequestPulse                    M1

(332) LD       bOPR_RequestFlagOffRequestPulse                    M1
      ANI      bnPositioningStart[0]                              Y110
      ANI      bStartComplete_Axis1                               W0.E
      SET      bOPR_RequestFlagOffRequestMemmory                  M2

(336) LD       bOPR_RequestFlagOffRequestMemmory                  M2
      MPS
      JP.REMFR J1 K1 K1 H0 K2417 uStatus(D0) K1 bStatusRet(M5100)
      MPP
      AND      bStatusRet[0]                                      M5100
      ANI      bStatusRet[1]                                      M5101
      MPS
      AND      uStatus.3                                          D0.3
      SET      bOPR_RequestFlagOffRequest                         M0
      MPP
      RST      bOPR_RequestFlagOffRequestMemmory                  M2

(358) LD       bOPR_RequestFlagOffRequest                         M0
      MPS
      MOVP     K1  uOPR_RequestFlagOffRequestSetting              D82
      MRD
      JP.REMTO J1 K2 K1 H0 K4321 uOPR_RequestFlagOffRequestSetting(D82) K1 bOPR_RequestFlagOffRet1(M5110)
      MPP
      AND      bOPR_RequestFlagOffRet1[0]                         M5110
      ANI      bOPR_RequestFlagOffRet1[1]                         M5111
      RST      bOPR_RequestFlagOffRequest                         M0
      SET      bOPR_RequestFlagOffRequestConfirmationPulse        M60

(380) LD       bOPR_RequestFlagOffRequestConfirmationPulse        M60
      MPS
      JP.REMFR J1 K3 K1 H0 K4321 uOPR_RequestFlagOffRequestSetting(D82) K1 bOPR_RequestFlagOffRet2(M5120)
      MPP
      RST      bOPR_RequestFlagOffRequestConfirmationPulse        M60

(396) LD       bOPR_RequestFlagOffRet2[0]                         M5120
      ANI      bOPR_RequestFlagOffRet2[1]                         M5121
      AND<>_U  uOPR_RequestFlagOffRequestSetting(D82)  K0
      SET      bOPR_RequestFlagOffRequestConfirmationPulse        M60
```

##### 外部指令機能有効設定プログラム (付4 / 印刷 p.807 / 原本 p.809)

【図】ラダー図(図から書き起こし)。
- ステップ(402): bInputExternalCommandValidRequest(X21)のa接点で、MOVP K1 → uExternalCommandValidSetting(D85)、JP.REMTO J1 K1 K1 H0 K4305 で D85 を1ワード書込み(完了ステータス bExternalCommandValidRet(M5130))。
- ステップ(421): bInputExternalCommandInvalidRequest(X22)のa接点で、MOVP K0 → D85、JP.REMTO J1 K2 K1 H0 K4305 で D85 を1ワード書込み(完了ステータス M5130)。

```
(402) LD       bInputExternalCommandValidRequest                  X21
      MPS
      MOVP     K1  uExternalCommandValidSetting                   D85
      MPP
      JP.REMTO J1 K1 K1 H0 K4305 uExternalCommandValidSetting(D85) K1 bExternalCommandValidRet(M5130)

(421) LD       bInputExternalCommandInvalidRequest                X22
      MPS
      MOVP     K0  uExternalCommandValidSetting                   D85
      MPP
      JP.REMTO J1 K2 K1 H0 K4305 uExternalCommandValidSetting(D85) K1 bExternalCommandValidRet(M5130)
```

##### シーケンサレディ信号[Y0] + 全軸サーボオン信号[Y1] ONプログラム (付4 / 印刷 p.808 / 原本 p.810)

【図】ラダー図(図から書き起こし)。
- ステップ(439): RCPU.stSM.bAfter_RUN1_Scan_OFF(SM403)、bBasicParameterSettingCompleteFlag(M50)、bOPR_BasicParameterSettingCompleteFlag(M51)、bSpeedPositionSwitchingParameterSettingCompleteFlag(M52)のa接点と、bInitializeParameterRequestMemory(M25)、bWriteFlashRequestMemory(M27)のb接点の直列で bPLCReady(Y100)を出力。
- ステップ(447): bReady(X100)のa接点で bAllAxisServoOn(Y101)を出力。

```
(439) LD       RCPU.stSM.bAfter_RUN1_Scan_OFF                     SM403
      AND      bBasicParameterSettingCompleteFlag                 M50
      AND      bOPR_BasicParameterSettingCompleteFlag             M51
      AND      bSpeedPositionSwitchingParameterSettingCompleteFlag M52
      ANI      bInitializeParameterRequestMemory                  M25
      ANI      bWriteFlashRequestMemory                           M27
      OUT      bPLCReady                                          Y100

(447) LD       bReady                                             X100
      OUT      bAllAxisServoOn                                    Y101
```

##### 位置決め始動番号設定プログラム (付4 / 印刷 p.808 / 原本 p.810)

###### 機械原点復帰 (付4 / 印刷 p.808 / 原本 p.810)

【図】ラダー図(図から書き起こし)。

```
(449) LD       bInputFastStartRequest                             X23
      MOVP     K9001  uPositioningStartNo                         D32
```

###### 高速原点復帰 (付4 / 印刷 p.808 / 原本 p.810)

【図】ラダー図(図から書き起こし)。bInputFastOPR_StartRequest(X24)のa接点の後で4段に分岐。1段目 JP.REMFR J1 K1 K1 H0 K2417 で uStatus(D0)へ1ワード読出し(完了ステータス bStatusRet(M5100))。2段目 bStatusRet[0](M5100)のa接点、bStatusRet[1](M5101)のb接点、uStatus.3(D0.3)のa接点で bFastOPR_Request(M3)をSET。3段目 MOVP K9002 → uPositioningStartNo(D32)。4段目 bFastOPR_RequestMemmory(M4)をSET。

```
(454) LD       bInputFastOPR_StartRequest                         X24
      MPS
      JP.REMFR J1 K1 K1 H0 K2417 uStatus(D0) K1 bStatusRet(M5100)
      MRD
      AND      bStatusRet[0]                                      M5100
      ANI      bStatusRet[1]                                      M5101
      AND      uStatus.3                                          D0.3
      SET      bFastOPR_Request                                   M3
      MRD
      MOVP     K9002  uPositioningStartNo                         D32
      MPP
      SET      bFastOPR_RequestMemmory                            M4
```

###### 位置決めデータNo.1による位置決め (付4 / 印刷 p.808 / 原本 p.810)

【図】ラダー図(図から書き起こし)。

```
(480) LD       bInputSetStartPositioningNoRequest                 X25
      MOVP     K1  uPositioningStartNo                            D32
```

###### 速度・位置切換え制御(位置決めデータNo.2) (付4 / 印刷 p.809 / 原本 p.811)

ABSモードの場合，変更後の移動量書込みは不要です。

【図】ラダー図(図から書き起こし)。
- ステップ(485): bInputSpeedPositionSwitchingRequest(X26)のa接点で MOVP K2 → uPositioningStartNo(D32)。
- ステップ(490): bInputSpeedPositionSwitchingEnableRequest(X27)のa接点で、MOVP K1 → uSpeedPositionSwitchingEnableFlagSetting(D86)、JP.REMTO J1 K2 K1 H0 K4328 で D86 を1ワード書込み(完了ステータス bSpeedPositionSwitchingEnableRet(M5140))。
- ステップ(508): bInputSpeedPositionSwitchingDisableRequest(X28)のa接点で、MOVP K0 → D86、JP.REMTO J1 K3 K1 H0 K4328 で D86 を1ワード書込み(完了ステータス M5140)。
- ステップ(526): bInputChangeMovementAmountRequest(X29)のa接点で JP.REMTO J1 K4 K1 H0 K4326 で wMovementAmount[0](D3)から2ワード書込み(完了ステータス bChangeMovementAmountRet(M5150))。

```
(485) LD       bInputSpeedPositionSwitchingRequest                X26
      MOVP     K2  uPositioningStartNo                            D32

(490) LD       bInputSpeedPositionSwitchingEnableRequest          X27
      MPS
      MOVP     K1  uSpeedPositionSwitchingEnableFlagSetting       D86
      MPP
      JP.REMTO J1 K2 K1 H0 K4328 uSpeedPositionSwitchingEnableFlagSetting(D86) K1 bSpeedPositionSwitchingEnableRet(M5140)

(508) LD       bInputSpeedPositionSwitchingDisableRequest         X28
      MPS
      MOVP     K0  uSpeedPositionSwitchingEnableFlagSetting       D86
      MPP
      JP.REMTO J1 K3 K1 H0 K4328 uSpeedPositionSwitchingEnableFlagSetting(D86) K1 bSpeedPositionSwitchingEnableRet(M5140)

(526) LD       bInputChangeMovementAmountRequest                  X29
      JP.REMTO J1 K4 K1 H0 K4326 wMovementAmount[0](D3) K2 bChangeMovementAmountRet(M5150)
```

###### 位置・速度切換え制御(位置決めデータNo.3) (付4 / 印刷 p.809 / 原本 p.811)

【図】ラダー図(図から書き起こし)。
- ステップ(541): bInputPositionSpeedSwitchingRequest(X40)のa接点で MOVP K3 → uPositioningStartNo(D32)。
- ステップ(546): bInputPositionSpeedSwitchingEnableRequest(X41)のa接点で、MOVP K1 → uPositionSpeedSwitchingEnableFlagSetting(D87)、JP.REMTO J1 K5 K1 H0 K4332 で D87 を1ワード書込み(完了ステータス bPositionSpeedSwitchingEnableRet(M5160))。
- ステップ(564): bInputPositionSpeedSwitchingDisableRequest(X42)のa接点で、MOVP K0 → D87、JP.REMTO J1 K6 K1 H0 K4332 で D87 を1ワード書込み(完了ステータス M5160)。
- ステップ(582): bInputChangePositionSpeedSwitchingSpeedRequest(X43)のa接点で JP.REMTO J1 K7 K1 H0 K4330 で wSpeed[0](D1)から2ワード書込み(完了ステータス bPVSpeedChangeRet(M5170))。

```
(541) LD       bInputPositionSpeedSwitchingRequest                X40
      MOVP     K3  uPositioningStartNo                            D32

(546) LD       bInputPositionSpeedSwitchingEnableRequest          X41
      MPS
      MOVP     K1  uPositionSpeedSwitchingEnableFlagSetting       D87
      MPP
      JP.REMTO J1 K5 K1 H0 K4332 uPositionSpeedSwitchingEnableFlagSetting(D87) K1 bPositionSpeedSwitchingEnableRet(M5160)

(564) LD       bInputPositionSpeedSwitchingDisableRequest         X42
      MPS
      MOVP     K0  uPositionSpeedSwitchingEnableFlagSetting       D87
      MPP
      JP.REMTO J1 K6 K1 H0 K4332 uPositionSpeedSwitchingEnableFlagSetting(D87) K1 bPositionSpeedSwitchingEnableRet(M5160)

(582) LD       bInputChangePositionSpeedSwitchingSpeedRequest     X43
      JP.REMTO J1 K7 K1 H0 K4330 wSpeed[0](D1) K2 bPVSpeedChangeRet(M5170)
```

###### 高度な位置決め制御 (付4 / 印刷 p.809 / 原本 p.811)

【図】ラダー図(図から書き起こし)。

```
(597) LD       bInputStartAdvancedPositioningRequest              X2A
      MOVP     K7000  uPositioningStartNo                         D32
```

###### 高速原点復帰指令，高速原点復帰指令記憶のOFF (付4 / 印刷 p.810 / 原本 p.812)

高速原点復帰を使用しない場合は不要です。

【図】ラダー図(図から書き起こし)。bInputFastStartRequest(X23)、bInputSetStartPositioningNoRequest(X25)、bInputSpeedPositionSwitchingRequest(X26)、bInputPositionSpeedSwitchingRequest(X40)、bInputStartAdvancedPositioningRequest(X2A)、bPositioningStartRequestMemmory(M6)のa接点の並列(OR)で、bFastOPR_Request(M3)と bFastOPR_RequestMemmory(M4)をRST。

```
(602) LD       bInputFastStartRequest                             X23
      OR       bInputSetStartPositioningNoRequest                 X25
      OR       bInputSpeedPositionSwitchingRequest                X26
      OR       bInputPositionSpeedSwitchingRequest                X40
      OR       bInputStartAdvancedPositioningRequest              X2A
      OR       bPositioningStartRequestMemmory                    M6
      RST      bFastOPR_Request                                   M3
      RST      bFastOPR_RequestMemmory                            M4
```

##### 位置決め始動プログラム (付4 / 印刷 p.810 / 原本 p.812)

###### 位置決め始動信号[Y10]を使用する場合 (付4 / 印刷 p.810 / 原本 p.812)

- 高速原点復帰を使用しない場合，bFastOPR_Request，bFastOPR_RequestMemoryの接点は不要です。
- Mコードを使用しない場合，bInputUnitError4の接点は不要です。
- JOG運転／インチング運転を使用しない場合，bJogInchingOperationFlagの接点は不要です。
- 手動パルサ運転を使用しない場合，bMPG_OperationFlagの接点は不要です。

【図】ラダー図(図から書き起こし)。
- ステップ(611): bInputStartPositioningRequest(X4E)のa接点で bPositioningStartRequestPulse(M5)をPLS。
- ステップ(615): bPositioningStartRequestPulse(M5)のa接点、bnPositioningStart[0](Y110)・bStartComplete_Axis1(W0.E)・bMcodeOn_Axis1(W0.C)・bJogInchingOperationFlag(M7)・bMPG_OperationFlag(M9)のb接点の直列に、「bFastOPR_Request(M3)のb接点」と「bFastOPR_Request(M3)のa接点＋bFastOPR_RequestMemmory(M4)のa接点の直列」の並列ブロックを直列に接続し、さらに bReady(X100)のa接点、bnBusy[0](X110)のb接点を経て bPositioningStartRequestMemmory(M6)をSET。
- ステップ(629): M6のa接点の後で分岐。1段目 JP.REMTO J1 K1 K1 H0 K4300 で uPositioningStartNo(D32)を1ワード書込み(完了ステータス bPositioningStartRet(M5180))。2段目 bPositioningStartRet[0](M5180)のa接点、bPositioningStartRet[1](M5181)のb接点を経て、bnPositioningStart[0](Y110)をSET、M6をRST。
- ステップ(648): bnPositioningStart[0](Y110)のa接点に、bStartComplete_Axis1(W0.E)と bErrorDetection_Axis1(W0.D)のa接点の並列を直列に接続し、bnBusy[0](X110)のb接点を経て Y110 をRST。

```
(611) LD       bInputStartPositioningRequest                      X4E
      PLS      bPositioningStartRequestPulse                      M5

(615) LD       bPositioningStartRequestPulse                      M5
      ANI      bnPositioningStart[0]                              Y110
      ANI      bStartComplete_Axis1                               W0.E
      ANI      bMcodeOn_Axis1                                     W0.C
      ANI      bJogInchingOperationFlag                           M7
      ANI      bMPG_OperationFlag                                 M9
      LDI      bFastOPR_Request                                   M3
      LD       bFastOPR_Request                                   M3
      AND      bFastOPR_RequestMemmory                            M4
      ORB
      ANB
      AND      bReady                                             X100
      ANI      bnBusy[0]                                          X110
      SET      bPositioningStartRequestMemmory                    M6

(629) LD       bPositioningStartRequestMemmory                    M6
      MPS
      JP.REMTO J1 K1 K1 H0 K4300 uPositioningStartNo(D32) K1 bPositioningStartRet(M5180)
      MPP
      AND      bPositioningStartRet[0]                            M5180
      ANI      bPositioningStartRet[1]                            M5181
      SET      bnPositioningStart[0]                              Y110
      RST      bPositioningStartRequestMemmory                    M6

(648) LD       bnPositioningStart[0]                              Y110
      LD       bStartComplete_Axis1                               W0.E
      OR       bErrorDetection_Axis1                              W0.D
      ANB
      ANI      bnBusy[0]                                          X110
      RST      bnPositioningStart[0]                              Y110
```

##### MコードOFFプログラム (付4 / 印刷 p.811 / 原本 p.813)

Mコードを使用しない場合は不要です。

【図】ラダー図(図から書き起こし)。bInputMcodeOffRequest(X2C)と bMcodeOn_Axis1(W0.C)のa接点の直列の後で分岐。1段目 MOVP K1 → uMcodeOnSignalTurnsOffRequestSetting(D90)。2段目 JP.REMTO J1 K1 K1 H0 K4304 で D90 を1ワード書込み(完了ステータス bMcodeOffRet(M5200))。

```
(654) LD       bInputMcodeOffRequest                              X2C
      AND      bMcodeOn_Axis1                                     W0.C
      MPS
      MOVP     K1  uMcodeOnSignalTurnsOffRequestSetting           D90
      MPP
      JP.REMTO J1 K1 K1 H0 K4304 uMcodeOnSignalTurnsOffRequestSetting(D90) K1 bMcodeOffRet(M5200)
```

##### JOG運転設定プログラム (付4 / 印刷 p.811 / 原本 p.813)

【図】ラダー図(図から書き起こし)。bInputSetJogSpeedRequest(X2D)のa接点の後で3段に分岐。1段目 DMOVP K10000 → wSetJogSpeed[1](D6)。2段目 MOVP K0 → wSetJogSpeed[0](D5)。3段目 JP.REMTO J1 K1 K1 H0 K4317 で wSetJogSpeed[0](D5)から3ワード書込み(完了ステータス bJogSettingRet(M5210))。

```
(674) LD       bInputSetJogSpeedRequest                           X2D
      MPS
      DMOVP    K10000  wSetJogSpeed[1]                            D6
      MRD
      MOVP     K0  wSetJogSpeed[0]                                D5
      MPP
      JP.REMTO J1 K1 K1 H0 K4317 wSetJogSpeed[0](D5) K3 bJogSettingRet(M5210)
```

##### インチング運転設定プログラム (付4 / 印刷 p.811 / 原本 p.813)

【図】ラダー図(図から書き起こし)。bInputInchingMovementAmountSettingRequest(X44)のa接点の後で分岐。1段目 MOVP K10 → wSetJogSpeed[0](D5)。2段目 JP.REMTO J1 K1 K1 H0 K4317 で wSetJogSpeed[0](D5)を1ワード書込み(完了ステータス bInchingSettingRet(M5220))。

```
(697) LD       bInputInchingMovementAmountSettingRequest          X44
      MPS
      MOVP     K10  wSetJogSpeed[0]                               D5
      MPP
      JP.REMTO J1 K1 K1 H0 K4317 wSetJogSpeed[0](D5) K1 bInchingSettingRet(M5220)
```

##### JOG運転／インチング運転実行プログラム (付4 / 印刷 p.812 / 原本 p.814)

【図】ラダー図(図から書き起こし)。正転JOG始動・逆転JOG始動はバッファメモリ K30101 / K30102 へ D211 / D212 を JP.REMTO で書き込む(完了ステータスはいずれも bStnAxCtrl2_Axis1(D214.0))。
- ステップ(716): bInputForwardJogStartRequest(X2E)と bInputReverseJogStartRequest(X2F)のa接点の並列に、bReady(X100)のa接点、bnBusy[0](X110)のb接点を直列に接続して bJogInchingOperationFlag(M7)をSET。
- ステップ(722): X2E と X2F のb接点の直列で M7 をRST。
- ステップ(725): bInputForwardJogStartRequest(X2E)のa接点、bJogInchingOperationFlag(M7)のa接点、bReverseRunJogStart_Axis1(D212.0)のb接点の直列で bForwardRunJogStart_Axis1(D211.0)を出力。
- ステップ(729): bForwardRunJogStart_Axis1(D211.0)のa接点で JP.REMTO J1 K1 K1 H0 K30101 D211 K1 bStnAxCtrl2_Axis1(D214.0)。
- ステップ(744): bForwardRunJogStart_Axis1(D211.0)のb接点で JP.REMTO J1 K1 K1 H0 K30101 D211 K1 bStnAxCtrl2_Axis1(D214.0)。
- ステップ(759): bInputReverseJogStartRequest(X2F)のa接点、M7のa接点、bForwardRunJogStart_Axis1(D211.0)のb接点の直列で bReverseRunJogStart_Axis1(D212.0)を出力。
- ステップ(763): D212.0 のa接点で JP.REMTO J1 K1 K1 H0 K30102 D212 K1 bStnAxCtrl2_Axis1(D214.0)。
- ステップ(778): D212.0 のb接点で JP.REMTO J1 K1 K1 H0 K30102 D212 K1 bStnAxCtrl2_Axis1(D214.0)。

```
(716) LD       bInputForwardJogStartRequest                       X2E
      OR       bInputReverseJogStartRequest                       X2F
      AND      bReady                                             X100
      ANI      bnBusy[0]                                          X110
      SET      bJogInchingOperationFlag                           M7

(722) LDI      bInputForwardJogStartRequest                       X2E
      ANI      bInputReverseJogStartRequest                       X2F
      RST      bJogInchingOperationFlag                           M7

(725) LD       bInputForwardJogStartRequest                       X2E
      AND      bJogInchingOperationFlag                           M7
      ANI      bReverseRunJogStart_Axis1                          D212.0
      OUT      bForwardRunJogStart_Axis1                          D211.0

(729) LD       bForwardRunJogStart_Axis1                          D211.0
      JP.REMTO J1 K1 K1 H0 K30101 D211 K1 bStnAxCtrl2_Axis1(D214.0)

(744) LDI      bForwardRunJogStart_Axis1                          D211.0
      JP.REMTO J1 K1 K1 H0 K30101 D211 K1 bStnAxCtrl2_Axis1(D214.0)

(759) LD       bInputReverseJogStartRequest                       X2F
      AND      bJogInchingOperationFlag                           M7
      ANI      bForwardRunJogStart_Axis1                          D211.0
      OUT      bReverseRunJogStart_Axis1                          D212.0

(763) LD       bReverseRunJogStart_Axis1                          D212.0
      JP.REMTO J1 K1 K1 H0 K30102 D212 K1 bStnAxCtrl2_Axis1(D214.0)

(778) LDI      bReverseRunJogStart_Axis1                          D212.0
      JP.REMTO J1 K1 K1 H0 K30102 D212 K1 bStnAxCtrl2_Axis1(D214.0)
```

##### 手動パルサ運転プログラム (付4 / 印刷 p.813 / 原本 p.815)

【図】ラダー図(図から書き起こし)。
- ステップ(793): bInputMPG_EnableRequest(X30)のa接点で bMPG_EnableFlagRequest(M8)をPLS。
- ステップ(797): M8・bReady(X100)のa接点、bnBusy[0](X110)のb接点の直列の後で4段に分岐。1段目 DMOVP K1 → wMPG[0](D8)。2段目 MOVP K1 → wMPG[2](D10)。3段目 JP.REMTO J1 K1 K1 H0 K4322 で wMPG[0](D8)から3ワード書込み(完了ステータス bMPG_SettingRet(M5230))。4段目 bMPG_OperationFlag(M9)をSET。
- ステップ(822): bInputMPG_DisableRequest(X31)のa接点で bMPG_DisableRequest(M10)をPLS。
- ステップ(825): bMPG_DisableRequest(M10)・bMPG_OperationFlag(M9)・bnBusy[0](X110)のa接点の直列の後で3段に分岐。1段目 MOVP K0 → wMPG[2](D10)。2段目 JP.REMTO J1 K2 K1 H0 K4324 で wMPG[2](D10)を1ワード書込み(完了ステータス bMPG_EnableRet(M5240))。3段目 M9 をRST。

```
(793) LD       bInputMPG_EnableRequest                            X30
      PLS      bMPG_EnableFlagRequest                             M8

(797) LD       bMPG_EnableFlagRequest                             M8
      AND      bReady                                             X100
      ANI      bnBusy[0]                                          X110
      MPS
      DMOVP    K1  wMPG[0]                                        D8
      MRD
      MOVP     K1  wMPG[2]                                        D10
      MRD
      JP.REMTO J1 K1 K1 H0 K4322 wMPG[0](D8) K3 bMPG_SettingRet(M5230)
      MPP
      SET      bMPG_OperationFlag                                 M9

(822) LD       bInputMPG_DisableRequest                           X31
      PLS      bMPG_DisableRequest                                M10

(825) LD       bMPG_DisableRequest                                M10
      AND      bMPG_OperationFlag                                 M9
      AND      bnBusy[0]                                          X110
      MPS
      MOVP     K0  wMPG[2]                                        D10
      MRD
      JP.REMTO J1 K2 K1 H0 K4324 wMPG[2](D10) K1 bMPG_EnableRet(M5240)
      MPP
      RST      bMPG_OperationFlag                                 M9
```

##### 速度変更プログラム (付4 / 印刷 p.814 / 原本 p.816)

【図】ラダー図(図から書き起こし)。
- ステップ(846): bInputSpeedChangeRequest(X32)のa接点で bSpeedChangeRequestPulse(M11)をPLS。
- ステップ(850): M11 と bnBusy[0](X110)のa接点の直列で bSpeedChangeRequestMemory(M12)をSET。
- ステップ(853): M12のa接点の後で4段に分岐。1段目 DMOVP K2000 → wSpeedChangeSetting[0](D11)。2段目 MOVP K1 → wSpeedChangeSetting[2](D13)。3段目 JP.REMTO J1 K1 K1 H0 K4314 で wSpeedChangeSetting[0](D11)から3ワード書込み(完了ステータス bSpeedChangeSettingRet(M5250))。4段目 bSpeedChangeSettingRet[0](M5250)のa接点、bSpeedChangeSettingRet[1](M5251)のb接点を経て分岐し、M12 をRST、bSpeedChangeRequestConfirmation(M62)をSET。
- ステップ(879): M62のa接点の後で分岐。JP.REMFR J1 K2 K1 H0 K4316 で wSpeedChangeSetting[0](D11)へ1ワード読出し(完了ステータス bSpeedChangeSettingRet(M5250))、もう一方で M62 をRST。
- ステップ(895): bSpeedChangeSettingRet[0](M5250)のa接点、bSpeedChangeSettingRet[1](M5251)のb接点、比較 <>_U wSpeedChangeSetting[0](D11) K0 の成立で M62 をSET。

```
(846) LD       bInputSpeedChangeRequest                           X32
      PLS      bSpeedChangeRequestPulse                           M11

(850) LD       bSpeedChangeRequestPulse                           M11
      AND      bnBusy[0]                                          X110
      SET      bSpeedChangeRequestMemory                          M12

(853) LD       bSpeedChangeRequestMemory                          M12
      MPS
      DMOVP    K2000  wSpeedChangeSetting[0]                      D11
      MRD
      MOVP     K1  wSpeedChangeSetting[2]                         D13
      MRD
      JP.REMTO J1 K1 K1 H0 K4314 wSpeedChangeSetting[0](D11) K3 bSpeedChangeSettingRet(M5250)
      MPP
      AND      bSpeedChangeSettingRet[0]                          M5250
      ANI      bSpeedChangeSettingRet[1]                          M5251
      RST      bSpeedChangeRequestMemory                          M12
      SET      bSpeedChangeRequestConfirmation                    M62

(879) LD       bSpeedChangeRequestConfirmation                    M62
      MPS
      JP.REMFR J1 K2 K1 H0 K4316 wSpeedChangeSetting[0](D11) K1 bSpeedChangeSettingRet(M5250)
      MPP
      RST      bSpeedChangeRequestConfirmation                    M62

(895) LD       bSpeedChangeSettingRet[0]                          M5250
      ANI      bSpeedChangeSettingRet[1]                          M5251
      AND<>_U  wSpeedChangeSetting[0](D11)  K0
      SET      bSpeedChangeRequestConfirmation                    M62
```

##### オーバーライドプログラム (付4 / 印刷 p.814 / 原本 p.816)

【図】ラダー図(図から書き起こし)。
- ステップ(901): bInputOverrideRequest(X33)のa接点で bOverrideRequest(M13)をPLS。
- ステップ(905): M13 と bnBusy[0](X110)のa接点の直列の後で分岐。1段目 MOV K200 → uOverrideValue(D14)(原本は MOV。MOVP ではない)。2段目 JP.REMTO J1 K1 K1 H0 K4313 で uOverrideValue(D14)を1ワード書込み(完了ステータス bOverrideSettingRet(M5260))。

```
(901) LD       bInputOverrideRequest                              X33
      PLS      bOverrideRequest                                   M13

(905) LD       bOverrideRequest                                   M13
      AND      bnBusy[0]                                          X110
      MPS
      MOV      K200  uOverrideValue                               D14
      MPP
      JP.REMTO J1 K1 K1 H0 K4313 uOverrideValue(D14) K1 bOverrideSettingRet(M5260)
```

##### 加減速時間変更プログラム (付4 / 印刷 p.815 / 原本 p.817)

【図】ラダー図(図から書き起こし)。
- ステップ(923): bInputChangeAccDecTimeRequest(X34)のa接点で bChangeAccDecTimeSettingRequest(M14)をPLS。
- ステップ(927): M14 と bnBusy[0](X110)のa接点の直列の後で5段に分岐。1段目 DMOV K2000 → wACCDecTimeChange[0](D15)。2段目 DMOV K0 → wACCDecTimeChange[2](D17)。3段目 MOVP K1 → wACCDecTimeChange[4](D19)。4段目 JP.REMTO J1 K1 K1 H0 K4308 で wACCDecTimeChange[0](D15)から5ワード書込み(完了ステータス bChangeAccDecTimeSettingRet(M5270))。5段目 bChangeAccDecTimeSettingRet[0](M5270)のa接点、bChangeAccDecTimeSettingRet[1](M5271)のb接点を経て M14 をRST。
- ステップ(955): bInputChangeAccDecTimeDisable(X35)のa接点の後で分岐。1段目 MOVP K0 → wACCDecTimeChange[4](D19)。2段目 JP.REMTO J1 K2 K1 H0 K4312 で wACCDecTimeChange[4](D19)を1ワード書込み(完了ステータス bChangeAccDecTimeEnableRet(M5280))。

```
(923) LD       bInputChangeAccDecTimeRequest                      X34
      PLS      bChangeAccDecTimeSettingRequest                    M14

(927) LD       bChangeAccDecTimeSettingRequest                    M14
      AND      bnBusy[0]                                          X110
      MPS
      DMOV     K2000  wACCDecTimeChange[0]                        D15
      MRD
      DMOV     K0  wACCDecTimeChange[2]                           D17
      MRD
      MOVP     K1  wACCDecTimeChange[4]                           D19
      MRD
      JP.REMTO J1 K1 K1 H0 K4308 wACCDecTimeChange[0](D15) K5 bChangeAccDecTimeSettingRet(M5270)
      MPP
      AND      bChangeAccDecTimeSettingRet[0]                     M5270
      ANI      bChangeAccDecTimeSettingRet[1]                     M5271
      RST      bChangeAccDecTimeSettingRequest                    M14

(955) LD       bInputChangeAccDecTimeDisable                      X35
      MPS
      MOVP     K0  wACCDecTimeChange[4]                           D19
      MPP
      JP.REMTO J1 K2 K1 H0 K4312 wACCDecTimeChange[4](D19) K1 bChangeAccDecTimeEnableRet(M5280)
```

##### ステップ運転プログラム (付4 / 印刷 p.815 / 原本 p.817)

【図】ラダー図(図から書き起こし)。
- ステップ(973): bInputStepOperationRequest(X37)のa接点で bStepOperationRequestPulse(M16)をPLS。
- ステップ(977): M16のa接点、bnPositioningStart[0](Y110)のb接点、bStartComplete_Axis1(W0.E)のb接点の直列の後で3段に分岐。1段目 MOVP K1 → wStep[0](D20)。2段目 MOVP K1 → wStep[1](D21)。3段目 JP.REMTO J1 K1 K1 H0 K4344 で wStep[0](D20)から2ワード書込み(完了ステータス bStepOperationSettingRet(M5290))。

```
(973) LD       bInputStepOperationRequest                         X37
      PLS      bStepOperationRequestPulse                         M16

(977) LD       bStepOperationRequestPulse                         M16
      ANI      bnPositioningStart[0]                              Y110
      ANI      bStartComplete_Axis1                               W0.E
      MPS
      MOVP     K1  wStep[0]                                       D20
      MRD
      MOVP     K1  wStep[1]                                       D21
      MPP
      JP.REMTO J1 K1 K1 H0 K4344 wStep[0](D20) K2 bStepOperationSettingRet(M5290)
```

##### スキッププログラム (付4 / 印刷 p.816 / 原本 p.818)

【図】ラダー図(図から書き起こし)。
- ステップ(1000): bInputSkipCommandRequest(X38)のa接点で bSkipCommandRequestPulse(M17)をPLS。
- ステップ(1004): M17 と bnBusy[0](X110)のa接点の直列で bSkipCommandRequestMemory(M18)をSET。
- ステップ(1007): M18のa接点の後で3段に分岐。1段目 MOVP K1 → uSkipCommandSetting(D91)。2段目 JP.REMTO J1 K1 K1 H0 K4347 で uSkipCommandSetting(D91)から2ワード書込み(完了ステータス bSkipCommandSettingRet(M5300))。3段目 bSkipCommandSettingRet[0](M5300)のa接点、bSkipCommandSettingRet[1](M5301)のb接点を経て分岐し、M18 をRST、bSkipCommandRequestConfirmation(M64)をSET。
- ステップ(1029): M64のa接点の後で分岐。JP.REMFR J1 K2 K1 H0 K4347 で uSkipCommandSetting(D91)へ1ワード読出し(完了ステータス bSkipCommandSettingRet(M5300))、もう一方で M64 をRST。
- ステップ(1045): bSkipCommandSettingRet[0](M5300)のa接点、bSkipCommandSettingRet[1](M5301)のb接点、比較 <>_U uSkipCommandSetting(D91) K0 の成立で M64 をSET。

```
(1000) LD       bInputSkipCommandRequest                          X38
       PLS      bSkipCommandRequestPulse                          M17

(1004) LD       bSkipCommandRequestPulse                          M17
       AND      bnBusy[0]                                         X110
       SET      bSkipCommandRequestMemory                         M18

(1007) LD       bSkipCommandRequestMemory                         M18
       MPS
       MOVP     K1  uSkipCommandSetting                           D91
       MRD
       JP.REMTO J1 K1 K1 H0 K4347 uSkipCommandSetting(D91) K2 bSkipCommandSettingRet(M5300)
       MPP
       AND      bSkipCommandSettingRet[0]                         M5300
       ANI      bSkipCommandSettingRet[1]                         M5301
       RST      bSkipCommandRequestMemory                         M18
       SET      bSkipCommandRequestConfirmation                   M64

(1029) LD       bSkipCommandRequestConfirmation                   M64
       MPS
       JP.REMFR J1 K2 K1 H0 K4347 uSkipCommandSetting(D91) K1 bSkipCommandSettingRet(M5300)
       MPP
       RST      bSkipCommandRequestConfirmation                   M64

(1045) LD       bSkipCommandSettingRet[0]                         M5300
       ANI      bSkipCommandSettingRet[1]                         M5301
       AND<>_U  uSkipCommandSetting(D91)  K0
       SET      bSkipCommandRequestConfirmation                   M64
```

##### 連続運転中断プログラム (付4 / 印刷 p.816 / 原本 p.818)

【図】ラダー図(図から書き起こし)。
- ステップ(1051): bInputStopContinuousOperationRequest(X3A)のa接点で bStopContinuousOperationRequest(M21)をPLS。
- ステップ(1055): M21 と bnBusy[0](X110)のa接点の直列の後で分岐。1段目 MOVP K1 → uStopContinuousOperationRequestSetting(D95)。2段目 JP.REMTO J1 K1 K1 H0 K4320 で D95 を1ワード書込み(完了ステータス bStopContinuousOperationRet(M5360))。

```
(1051) LD       bInputStopContinuousOperationRequest              X3A
       PLS      bStopContinuousOperationRequest                   M21

(1055) LD       bStopContinuousOperationRequest                   M21
       AND      bnBusy[0]                                         X110
       MPS
       MOVP     K1  uStopContinuousOperationRequestSetting        D95
       MPP
       JP.REMTO J1 K1 K1 H0 K4320 uStopContinuousOperationRequestSetting(D95) K1 bStopContinuousOperationRet(M5360)
```

##### 目標位置変更プログラム (付4 / 印刷 p.817 / 原本 p.819)

【図】ラダー図(図から書き起こし)。
- ステップ(1074): bInputTargetPositionChangeRequest(X45)のa接点で bTargetPositionChangeRequestPulse(M30)をPLS。
- ステップ(1078): M30 と bnBusy[0](X110)のa接点の直列で bTargetPositionChangeRequestMemory(M31)をSET。
- ステップ(1081): M31のa接点の後で5段に分岐。1段目 DMOVP K3000 → wTarget[0](D23)。2段目 DMOVP K100000 → wTarget[2](D25)。3段目 MOVP K1 → wTarget[4](D27)。4段目 JP.REMTO J1 K1 K1 H0 K4334 で wTarget[0](D23)から5ワード書込み(完了ステータス bTargetPositionChangeRet(M5310))。5段目 bTargetPositionChangeRet[0](M5310)のa接点、bTargetPositionChangeRet[1](M5311)のb接点を経て分岐し、M31 をRST、bTargetPositionChangeRequestConfirmation(M63)をSET。
- ステップ(1111): M63のa接点の後で分岐。JP.REMFR J1 K2 K1 H0 K4338 で wTarget[4](D27)へ1ワード読出し(完了ステータス bTargetPositionChangeRet(M5310))、もう一方で M63 をRST。
- ステップ(1127): bTargetPositionChangeRet[0](M5310)のa接点、bTargetPositionChangeRet[1](M5311)のb接点、比較 <> D27 K0(原本は「<>」。他の回路の「<>_U」とは異なる)の成立で M63 をSET。

```
(1074) LD       bInputTargetPositionChangeRequest                 X45
       PLS      bTargetPositionChangeRequestPulse                 M30

(1078) LD       bTargetPositionChangeRequestPulse                 M30
       AND      bnBusy[0]                                         X110
       SET      bTargetPositionChangeRequestMemory                M31

(1081) LD       bTargetPositionChangeRequestMemory                M31
       MPS
       DMOVP    K3000  wTarget[0]                                 D23
       MRD
       DMOVP    K100000  wTarget[2]                               D25
       MRD
       MOVP     K1  wTarget[4]                                    D27
       MRD
       JP.REMTO J1 K1 K1 H0 K4334 wTarget[0](D23) K5 bTargetPositionChangeRet(M5310)
       MPP
       AND      bTargetPositionChangeRet[0]                       M5310
       ANI      bTargetPositionChangeRet[1]                       M5311
       RST      bTargetPositionChangeRequestMemory                M31
       SET      bTargetPositionChangeRequestConfirmation          M63

(1111) LD       bTargetPositionChangeRequestConfirmation          M63
       MPS
       JP.REMFR J1 K2 K1 H0 K4338 wTarget[4](D27) K1 bTargetPositionChangeRet(M5310)
       MPP
       RST      bTargetPositionChangeRequestConfirmation          M63

(1127) LD       bTargetPositionChangeRet[0]                       M5310
       ANI      bTargetPositionChangeRet[1]                       M5311
       AND<>    D27  K0
       SET      bTargetPositionChangeRequestConfirmation          M63
```

##### 再始動プログラム (付4 / 印刷 p.818 / 原本 p.820)

【図】ラダー図(図から書き起こし)。
- ステップ(1133): bInputRestartRequest(X3B)のa接点で bRestartRequest(M22)をPLS。
- ステップ(1137): M22のa接点で bAxisOperationStatusAcquisitionRequest(M65)をSET。
- ステップ(1139): M65のa接点の後で分岐。1段目 JP.REMFR J1 K1 K1 H0 K2409 で wAxisOperationStatus(D81)へ1ワード読出し(完了ステータス bAxisOperationStatusRet(M5320))。2段目 bAxisOperationStatusRet[0](M5320)のa接点、bAxisOperationStatusRet[1](M5321)のb接点、比較 = wAxisOperationStatus(D81) K1 の成立の後で分岐し、bRestartRequestMemory(M23)をSET、M65 をRST。
- ステップ(1161): M23のa接点、bPositioningComplete_Axis1(W0.F)のb接点、bStartComplete_Axis1(W0.E)のb接点の直列の後で3段に分岐。1段目 MOVP K1 → uRestartSetting(D92)。2段目 JP.REMTO J1 K2 K1 H0 K4303 で D92 を1ワード書込み(完了ステータス bRestartRet(M5330))。3段目 bRestartRet[0](M5330)のa接点、bRestartRet[1](M5331)のb接点を経て分岐し、M23 をRST、bRestartRequestConfirmation(M61)をSET。
- ステップ(1185): M61のa接点の後で分岐。JP.REMFR J1 K3 K1 H0 K4303 で uRestartSetting(D92)へ1ワード読出し(完了ステータス bRestartRet(M5330))、もう一方で M61 をRST。
- ステップ(1201): bRestartRet[0](M5330)のa接点、bRestartRet[1](M5331)のb接点、比較 <>_U uRestartSetting(D92) K0 の成立で M61 をSET。

```
(1133) LD       bInputRestartRequest                              X3B
       PLS      bRestartRequest                                   M22

(1137) LD       bRestartRequest                                   M22
       SET      bAxisOperationStatusAcquisitionRequest            M65

(1139) LD       bAxisOperationStatusAcquisitionRequest            M65
       MPS
       JP.REMFR J1 K1 K1 H0 K2409 wAxisOperationStatus(D81) K1 bAxisOperationStatusRet(M5320)
       MPP
       AND      bAxisOperationStatusRet[0]                        M5320
       ANI      bAxisOperationStatusRet[1]                        M5321
       AND=     wAxisOperationStatus(D81)  K1
       SET      bRestartRequestMemory                             M23
       RST      bAxisOperationStatusAcquisitionRequest            M65

(1161) LD       bRestartRequestMemory                             M23
       ANI      bPositioningComplete_Axis1                        W0.F
       ANI      bStartComplete_Axis1                              W0.E
       MPS
       MOVP     K1  uRestartSetting                               D92
       MRD
       JP.REMTO J1 K2 K1 H0 K4303 uRestartSetting(D92) K1 bRestartRet(M5330)
       MPP
       AND      bRestartRet[0]                                    M5330
       ANI      bRestartRet[1]                                    M5331
       RST      bRestartRequestMemory                             M23
       SET      bRestartRequestConfirmation                       M61

(1185) LD       bRestartRequestConfirmation                       M61
       MPS
       JP.REMFR J1 K3 K1 H0 K4303 uRestartSetting(D92) K1 bRestartRet(M5330)
       MPP
       RST      bRestartRequestConfirmation                       M61

(1201) LD       bRestartRet[0]                                    M5330
       ANI      bRestartRet[1]                                    M5331
       AND<>_U  uRestartSetting(D92)  K0
       SET      bRestartRequestConfirmation                       M61
```

##### パラメータ初期化プログラム (付4 / 印刷 p.819 / 原本 p.821)

【図】ラダー図(図から書き起こし)。
- ステップ(1207): bInputModuleInitializeParameterRequest(X3C)のa接点で bInitializeParameterRequestPulse(M24)をPLS。
- ステップ(1211): M24のa接点、bnBusy[0](X110)・bnBusy[1](X111)・bnBusy[2](X112)・bnBusy[3](X113)のb接点の直列で bInitializeParameterRequestMemory(M25)をSET。
- ステップ(1217): M25のa接点、bPLCReady(Y100)のb接点の直列でタイマ tdPLCReadyOff1(T104)を設定値 K2 で OUT。
- ステップ(1223): tdPLCReadyOff1(T104)のa接点の後で3段に分岐。1段目 MOVP K1 → uInitializeParameterSetting(D93)。2段目 JP.REMTO J1 K1 K1 H0 K5901 で D93 を1ワード書込み(完了ステータス bInitializeParameterRet(M5340))。3段目 bInitializeParameterRet[0](M5340)のa接点、bInitializeParameterRet[1](M5341)のb接点を経て bInitializeParameterRequestConfirmation(M66)をSET。
- ステップ(1244): M66のa接点の後で分岐。JP.REMFR J1 K2 K1 H0 K5901 で uInitializeParameterSetting(D93)へ1ワード読出し(完了ステータス bInitializeParameterRet(M5340))、もう一方で M66 をRST。
- ステップ(1260): bInitializeParameterRet[0](M5340)のa接点、bInitializeParameterRet[1](M5341)のb接点の後で分岐。上段は比較 =_U uInitializeParameterSetting(D93) K0 の成立で M25 をRST。下段は比較 <>_U uInitializeParameterSetting(D93) K0 の成立で M66 をSET。

```
(1207) LD       bInputModuleInitializeParameterRequest            X3C
       PLS      bInitializeParameterRequestPulse                  M24

(1211) LD       bInitializeParameterRequestPulse                  M24
       ANI      bnBusy[0]                                         X110
       ANI      bnBusy[1]                                         X111
       ANI      bnBusy[2]                                         X112
       ANI      bnBusy[3]                                         X113
       SET      bInitializeParameterRequestMemory                 M25

(1217) LD       bInitializeParameterRequestMemory                 M25
       ANI      bPLCReady                                         Y100
       OUT      tdPLCReadyOff1(T104)  K2

(1223) LD       tdPLCReadyOff1                                    T104
       MPS
       MOVP     K1  uInitializeParameterSetting                   D93
       MRD
       JP.REMTO J1 K1 K1 H0 K5901 uInitializeParameterSetting(D93) K1 bInitializeParameterRet(M5340)
       MPP
       AND      bInitializeParameterRet[0]                        M5340
       ANI      bInitializeParameterRet[1]                        M5341
       SET      bInitializeParameterRequestConfirmation           M66

(1244) LD       bInitializeParameterRequestConfirmation           M66
       MPS
       JP.REMFR J1 K2 K1 H0 K5901 uInitializeParameterSetting(D93) K1 bInitializeParameterRet(M5340)
       MPP
       RST      bInitializeParameterRequestConfirmation           M66

(1260) LD       bInitializeParameterRet[0]                        M5340
       ANI      bInitializeParameterRet[1]                        M5341
       MPS
       AND=_U   uInitializeParameterSetting(D93)  K0
       RST      bInitializeParameterRequestMemory                 M25
       MPP
       AND<>_U  uInitializeParameterSetting(D93)  K0
       SET      bInitializeParameterRequestConfirmation           M66
```

##### フラッシュ ROM書込みプログラム (付4 / 印刷 p.820 / 原本 p.822)

【図】ラダー図(図から書き起こし)。
- ステップ(1272): bInputWriteFlashRequest(X3D)のa接点で bWriteFlashRequestPulse(M26)をPLS。
- ステップ(1276): M26のa接点、bnBusy[0](X110)・bnBusy[1](X111)・bnBusy[2](X112)・bnBusy[3](X113)のb接点の直列で bWriteFlashRequestMemory(M27)をSET。
- ステップ(1282): M27のa接点、bPLCReady(Y100)のb接点の直列でタイマ tdPLCReadyOff2(T105)を設定値 K2 で OUT。
- ステップ(1288): tdPLCReadyOff2(T105)のa接点の後で3段に分岐。1段目 MOVP K1 → uWriteFlashSetting(D94)。2段目 JP.REMTO J1 K1 K1 H0 K5900 で D94 を1ワード書込み(完了ステータス bWriteFlashRet(M5350))。3段目 bWriteFlashRet[0](M5350)のa接点、bWriteFlashRet[1](M5351)のb接点を経て bWriteFlashRequestConfirmation(M67)をSET。
- ステップ(1309): M67のa接点の後で分岐。JP.REMFR J1 K2 K1 H0 K5900 で uWriteFlashSetting(D94)へ1ワード読出し(完了ステータス bWriteFlashRet(M5350))、もう一方で M67 をRST。
- ステップ(1325): bWriteFlashRet[0](M5350)のa接点、bWriteFlashRet[1](M5351)のb接点の後で分岐。上段は比較 =_U uWriteFlashSetting(D94) K0 の成立で M27 をRST。下段は比較 <>_U uWriteFlashSetting(D94) K0 の成立で M67 をSET。

```
(1272) LD       bInputWriteFlashRequest                           X3D
       PLS      bWriteFlashRequestPulse                           M26

(1276) LD       bWriteFlashRequestPulse                           M26
       ANI      bnBusy[0]                                         X110
       ANI      bnBusy[1]                                         X111
       ANI      bnBusy[2]                                         X112
       ANI      bnBusy[3]                                         X113
       SET      bWriteFlashRequestMemory                          M27

(1282) LD       bWriteFlashRequestMemory                          M27
       ANI      bPLCReady                                         Y100
       OUT      tdPLCReadyOff2(T105)  K2

(1288) LD       tdPLCReadyOff2                                    T105
       MPS
       MOVP     K1  uWriteFlashSetting                            D94
       MRD
       JP.REMTO J1 K1 K1 H0 K5900 uWriteFlashSetting(D94) K1 bWriteFlashRet(M5350)
       MPP
       AND      bWriteFlashRet[0]                                 M5350
       ANI      bWriteFlashRet[1]                                 M5351
       SET      bWriteFlashRequestConfirmation                    M67

(1309) LD       bWriteFlashRequestConfirmation                    M67
       MPS
       JP.REMFR J1 K2 K1 H0 K5900 uWriteFlashSetting(D94) K1 bWriteFlashRet(M5350)
       MPP
       RST      bWriteFlashRequestConfirmation                    M67

(1325) LD       bWriteFlashRet[0]                                 M5350
       ANI      bWriteFlashRet[1]                                 M5351
       MPS
       AND=_U   uWriteFlashSetting(D94)  K0
       RST      bWriteFlashRequestMemory                          M27
       MPP
       AND<>_U  uWriteFlashSetting(D94)  K0
       SET      bWriteFlashRequestConfirmation                    M67
```

##### エラーリセットプログラム (付4 / 印刷 p.820 / 原本 p.822)

【図】ラダー図(図から書き起こし)。
- ステップ(1337): bErrorDetection_Axis1(W0.D)のa接点で JP.REMFR J1 K1 K1 H0 K2406 で uErrorCode(D80)へ1ワード読出し(完了ステータス bErrorCodeRet1(M5370))。
- ステップ(1353): bInputErrResetRequest(X3E)のa接点で bErrorReset(M28)をPLS。
- ステップ(1356): bErrorReset(M28)と bErrorDetection_Axis1(W0.D)のa接点の直列の後で分岐。1段目 MOVP K1 → uErrorResetRequestSetting(D96)。2段目 JP.REMTO J1 K2 K1 H0 K4302 で D96 を1ワード書込み(完了ステータス bErrorCodeRet2(M5380))。

```
(1337) LD       bErrorDetection_Axis1                             W0.D
       JP.REMFR J1 K1 K1 H0 K2406 uErrorCode(D80) K1 bErrorCodeRet1(M5370)

(1353) LD       bInputErrResetRequest                             X3E
       PLS      bErrorReset                                       M28

(1356) LD       bErrorReset                                       M28
       AND      bErrorDetection_Axis1                             W0.D
       MPS
       MOVP     K1  uErrorResetRequestSetting                     D96
       MPP
       JP.REMTO J1 K2 K1 H0 K4302 uErrorResetRequestSetting(D96) K1 bErrorCodeRet2(M5380)
```

本プログラムはエラーコードのみを格納，リセットするプログラムです。
ワーニングもリセットしたい場合は，ステップ1356でエラー検出信号(軸1)W0.Dとワーニング検出信号(軸1)W0.9に対してOR回路を作成してください。
また必要に応じて，ステップ1337を参考にワーニングコードを格納するプログラムを作成してください。

##### 停止プログラム (付4 / 印刷 p.821 / 原本 p.823)

【図】ラダー図(図から書き起こし)。停止信号は bAxisStop_Axis1(D210.0)を含む D210 を、JP.REMTO でバッファメモリ K30100 へ書き込む(完了ステータス bStnAxCtrl2_Axis1(D214.0))。
- ステップ(1375): bInputStopRequest(X3F)のa接点で bStopRequestPulse(M29)をPLS。
- ステップ(1379): M29 と bnBusy[0](X110)のa接点の直列で bAxisStop_Axis1(D210.0)をSET。
- ステップ(1382): bAxisStop_Axis1(D210.0)のa接点で JP.REMTO J1 K1 K1 H0 K30100 D210 K1 bStnAxCtrl2_Axis1(D214.0)。
- ステップ(1397): bInputStopRequest(X3F)のb接点、bnBusy[0](X110)のb接点の直列で D210.0 をRST。
- ステップ(1400): bAxisStop_Axis1(D210.0)のb接点で JP.REMTO J1 K1 K1 H0 K30100 D210 K1 bStnAxCtrl2_Axis1(D214.0)。
- ステップ(1415): MCR N0(接点なし)。
- ステップ(1416): END。

```
(1375) LD       bInputStopRequest                                 X3F
       PLS      bStopRequestPulse                                 M29

(1379) LD       bStopRequestPulse                                 M29
       AND      bnBusy[0]                                         X110
       SET      bAxisStop_Axis1                                   D210.0

(1382) LD       bAxisStop_Axis1                                   D210.0
       JP.REMTO J1 K1 K1 H0 K30100 D210 K1 bStnAxCtrl2_Axis1(D214.0)

(1397) LDI      bInputStopRequest                                 X3F
       ANI      bnBusy[0]                                         X110
       RST      bAxisStop_Axis1                                   D210.0

(1400) LDI      bAxisStop_Axis1                                   D210.0
       JP.REMTO J1 K1 K1 H0 K30100 D210 K1 bStnAxCtrl2_Axis1(D214.0)

(1415) MCR      N0

(1416) END
```

#### リモートヘッドユニット装着時のRD77MSの動作 (付4 / 印刷 p.822 / 原本 p.824)

リモートヘッドユニット装着時のRD77MSにおいて，リモートヘッドユニットが解列している場合のRD77MSの動作について示します。

##### 解列時のRD77MSの動作 (付4 / 印刷 p.822 / 原本 p.824)

> RD77MSの"CPUエラー時出力モード設定"は"0: クリア"固定のため，解列時は出力信号がOFFされます。そのため，位置決め運転中にリモートヘッドユニットが解列すると，シーケンサレディ信号[Y0]がON→OFFとなり，エラー「運転中シーケンサレディ OFF」(エラーコード: 1900H)が発生し，位置決め動作は減速停止します。
> リモートヘッドユニットの復列後に位置決めを行う場合は，エラーリセットによりエラー状態を解除した後，始動してください。

#### リモートヘッドユニット装着時の制約事項 (付4 / 印刷 p.822 / 原本 p.824)

リモートヘッドユニット装着時の制約事項を以下に示します。

| No. | 項目 | 内容 |
|---|---|---|
| 1 | ユニットラベル | ユニットラベルは使用できません。 |
| 2 | ユニットFB | ユニットFBは使用できません。 |
| 3 | 自動リフレッシュ | 指定デバイスのみ使用可能です。 |
| 4 | 専用命令 | 専用命令は使用できません。 |
| 5 | 割込み機能 | 割込み機能は使用できません。 |
| 6 | ユニット間同期 | リモートヘッドユニット二重化システムの場合は使用できません。 |

#### GX Works3の対応バージョン (付4 / 印刷 p.822 / 原本 p.824)

リモートヘッドユニットに対応したGX Works3の対応バージョンを以下に示します。

| No. | 品名 | ソフトウェアバージョン |
|---|---|---|
| 1 | GX Works3 | 1.025B |

### 付5 バージョンによる機能の制約 (付5 / 印刷 p.823-824 / 原本 p.825-826)

各シンプルモーションユニットに対応するソフトウェアのバージョンは，以下のとおりです。

| 機種 | バージョン(GX Works3) |
|---|---|
| RD77MS | 1.000A |
| RD77GF | 1.020W |

シンプルモーションユニットのソフトウェアおよびエンジニアリングツールのバージョンにより，使用できる機能に制約があります。各バージョンと機能の組合せを下記に示します。

#### [RD77MS] (付5 / 印刷 p.823 / 原本 p.825)

—: バージョンによる制約はありません。

結合セル(ソフトウェアバージョン・GX Works3・参照の縦結合)は各行に展開した。

| 機能 | ソフトウェアバージョン | GX Works3 | 参照 |
|---|---|---|---|
| イベント履歴 フラッシュ ROM書込み対応 | Ver.03以降 | — | ☞ 385ページ イベント履歴機能 |
| ユニット間同期始動 | Ver.03以降 | — | ☞ 194ページ ユニット間同期機能 |
| アドバンスト同期制御<br>滑り量スムージング方式(直線: 入力量追従) | Ver.03以降 | 1.007H以降 | *1 |
| カム軸1 サイクル長変更 | Ver.03以降 | 1.007H以降 | *1 |
| オンラインユニット交換 | Ver.03以降 | — | ☞ 399ページ オンラインユニット交換[RD77MS] |
| 指令パルス制限機能 | Ver.03以降 | — | ☞ 241ページ 指令パルス制限機能[RD77MS] |
| 3 軸ヘリカル補間制御 | Ver.03以降 | 1.007H以降 | ☞ 101ページ 補助点指定の3軸ヘリカル補間制御<br>☞ 107ページ 中心点指定の3軸ヘリカル補間制御 |
| アドバンスト同期制御モニタでの回転方向モニタ対応 | Ver.03以降 | 1.007H以降 | *1 |
| 緊急停止(バッファメモリ入力) | Ver.05以降 | 1.010L以降 | ☞ 260ページ 緊急停止機能 |
| テストモード | Ver.05以降 | 1.010L以降 | ☞ 400ページ テストモード |
| 光分岐ユニット | Ver.05以降 | — | ☞ 746ページ 光分岐ユニット |
| オフラインデジタルオシロ | Ver.05以降 | 1.010L以降 | — |
| オリエンタルモーター株式会社製ステッピングモーターユニット(αSTEP/5相)対応(SSCNETⅢ/H) | Ver.06以降 | 1.010L以降 | ☞ 770ページ オリエンタルモーター株式会社製ステッピングモーターユニットαSTEP/5相 |
| CKD日機電装株式会社製サーボドライバ(VPHシリーズ) | Ver.07以降 | 1.020W以降 | ☞ 776ページ CKD日機電装株式会社製サーボドライバVCIIシリーズ／VPHシリーズ |
| 汎用インバータ(FR-A800シリーズ) | Ver.07以降 | 1.020W以降 | ☞ 757ページ 汎用インバータFR-A800シリーズ |
| [Pr.127]制御モード切換え時速度制限値取込み選択 | Ver.08以降 | 1.025B以降 | ☞ 512ページ 詳細パラメータ2 |
| 株式会社アイエイアイ製IAI電動アクチュエータ用コントローラ | Ver.08以降 | 1.025B以降 | ☞ 780ページ 株式会社アイエイアイ製IAI電動アクチュエータ用コントローラ |
| オリエンタルモーター株式会社製ステッピングモーターユニット(αSTEP)速度・トルク制御対応 | Ver.09以降 | 1.045X以降 | ☞ 770ページ オリエンタルモーター株式会社製ステッピングモーターユニットαSTEP/5相 |
| [Pr128]トルク制限選択(ステッピングドライバ) | Ver.09以降 | 1.045X以降 | ☞ 770ページ オリエンタルモーター株式会社製ステッピングモーターユニットαSTEP/5相 |
| シーケンサレディ信号[Y0]ON時のサーボパラメータ転送機能対応 | Ver.10以降 | 1.060N以降 | ☞ 656ページ (10)サーボパラメータの転送[RD77MS] |
| 位置決めデータ，始動ブロックデータの書込み読出し機能 | Ver.11以降 | — | ☞ 408ページ 位置決めデータ，始動ブロックデータ書込み読出し機能[RD77MS] |
| MR-J5(W)-B対応 | Ver.13以降 | 1.085P以降 | ☞ 786ページ MR-J5(W)-Bとの接続 |
| 任意トランジェントコマンド送信機能 | Ver.16以降 | — | ☞ 379ページ 任意トランジェントコマンド送信機能[RD77MS] |

- *1 詳細は下記マニュアルを参照してください。
  MELSEC iQ-R シンプルモーションユニットユーザーズマニュアル(アドバンスト同期制御編)

#### [RD77GF] (付5 / 印刷 p.824 / 原本 p.826)

—: バージョンによる制約はありません。

結合セル(各列の縦結合)は各行に展開した。原本の見出しは「4軸／8軸／16軸ユニット」「32軸ユニット」の下にそれぞれ「ソフトウェアバージョン」「GX Works3」の2段構成。

| 機能 | 4軸／8軸／16軸ユニット<br>ソフトウェアバージョン | 4軸／8軸／16軸ユニット<br>GX Works3 | 32軸ユニット<br>ソフトウェアバージョン | 32軸ユニット<br>GX Works3 | 参照 |
|---|---|---|---|---|---|
| サーボパラメータ「機能選択D-4(PD41)」の「ストロークリミット有効状態選択」が「0」に対応 | Ver.02以降 | — | Ver.05以降 | 1.030G以降 | — |
| 局単位ブロック保証対応(同期局のみ) | Ver.02以降 | 1.020W以降 | Ver.05以降 | 1.030G以降 | *1 |
| データリンク異常局設定対応 | Ver.02以降 | 1.020W以降 | Ver.05以降 | 1.030G以降 | *1 |
| サーボアンプ経由同期エンコーダ対応 | Ver.02以降 | 1.022Y以降 | Ver.05以降 | 1.030G以降 | *2 |
| リニアサーボモータ制御モード・ダイレクトドライブモータ制御モード・フルクローズド制御モード対応 | Ver.02以降 | 1.022Y以降 | Ver.05以降 | 1.030G以降 | — |
| 安全通信機能*3 | Ver.05以降 | 1.030G以降 | Ver.05以降 | 1.030G以降 | *4 |
| 通信モードの標準モード設定対応 | Ver.05以降 | 1.030G以降 | Ver.05以降 | 1.030G以降 | *4 |
| ユニット間同期機能を「使用しない」設定対応 | Ver.05以降 | 1.030G以降 | Ver.05以降 | 1.030G以降 | ☞ 194ページ ユニット間同期機能 |
| 始動履歴モニタ(256点)対応 | Ver.05以降 | 1.030G以降 | Ver.05以降 | 1.030G以降 | ☞ 343ページ 履歴モニタ機能 |
| iQ Sensor Solution対応バックアップ／リストア機能*3 | Ver.05以降 | — | Ver.05以降 | — | — |

- *1 詳細は下記マニュアルの"サイクリック伝送"を参照してください。
  MELSEC iQ-R シンプルモーションユニットユーザーズマニュアル(ネットワーク編)
- *2 詳細は下記マニュアルの"同期エンコーダ軸"を参照してください。
  MELSEC iQ-R シンプルモーションユニットユーザーズマニュアル(アドバンスト同期制御編)
- *3 使用するCPUユニットに制約があります。詳細は下記を参照してください。
  MELSEC iQ-R CPUユニットユーザーズマニュアル(応用編)
- *4 詳細は下記マニュアルの"安全通信機能"を参照してください。
  MELSEC iQ-R シンプルモーションユニットユーザーズマニュアル(ネットワーク編)

## 転記時の要確認一覧

- (印刷 p.810 / 原本 p.812) 「位置決め始動信号[Y10]を使用する場合」の注記は「Mコードを使用しない場合，bInputUnitError4の接点は不要です。」とあるが、直下のステップ(615)の回路にあるMコード関連の接点は bMcodeOn_Axis1(W0.C)で、bInputUnitError4 という接点は回路上に無い。原文どおり転記した。
- (印刷 p.810 / 原本 p.812) 同注記の「bFastOPR_RequestMemory」に対し、回路上のラベルは「bFastOPR_RequestMemmory」(M4)。原文どおり両方を転記した。他にも bOPR_RequestFlagOffRequestMemmory(M2)、bPositioningStartRequestMemmory(M6)等「Memmory」の綴りが回路に見られる(原本どおり)。
- (印刷 p.808 / 原本 p.810) 「機械原点復帰」のステップ(449)の起動接点ラベルは bInputFastStartRequest(X23)(「Fast」を含むが機械原点復帰 K9001 の設定)。原本どおり。
- (印刷 p.807 / 原本 p.809) 原点復帰要求OFFプログラムの前置き「"原点復帰未完時動作設定"を"1: 位置決め制御"を実行するに設定した場合」は文の構成が不自然だが原文どおり。
- (印刷 p.807 / 原本 p.809) 外部指令機能有効設定プログラムのステップ番号は原本画像で「402)」「421)」と左括弧が欠けて表示されている。(402)(421)として転記した。
- (印刷 p.817 / 原本 p.819) 目標位置変更プログラムのステップ(1127)の比較は「<> D27 K0」(ラベル表示なし・符号付き比較)で、他の同種回路の「<>_U ラベル(デバイス) K0」と表記が異なる。原本どおり。
- (印刷 p.814 / 原本 p.816) オーバーライドプログラムのステップ(905)は MOV(非パルス)、加減速時間変更のステップ(927)は DMOV(非パルス)。他の回路の MOVP／DMOVP と異なるが原本どおり。
- (印刷 p.823 / 原本 p.825) [RD77MS]表の「[Pr128]トルク制限選択(ステッピングドライバ)」は「Pr」の後のピリオドが無い。原文どおり。参照欄「CKD日機電装株式会社製サーボドライバVCIIシリーズ」の「VCII」も原本の表記どおり(本文見出しでは「VCⅡ」)。
- (印刷 p.821 / 原本 p.823) 停止プログラムのステップ(1415)の MCR N0 に対応する MC 命令は本範囲には無い(前ファイルの範囲と思われる)。
- ニモニックは図から書き起こしたもの(原本にニモニック記載なし)。分岐の MPS／MRD／MPP の置き方は等価な回路表現であり、GX Works3 のニモニック変換結果と一致するとは限らない。
