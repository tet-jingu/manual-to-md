# 三菱 MELSEC iQ-R シンプルモーションユニット ユーザーズマニュアル(応用編) 13 プログラミング 13.4 位置決めプログラム例(後半)

| 項目 | 内容 |
|---|---|
| 原本 | 三菱電機 MELSEC iQ-R シンプルモーションユニット ユーザーズマニュアル(応用編)(対象形名: RD77MS2 / RD77MS4 / RD77MS8 / RD77MS16 / RD77GF4 / RD77GF8 / RD77GF16 / RD77GF32) |
| 発行元 | 三菱電機株式会社 |
| 資料番号・版数 | IB(名)-0300246-P (2509)MEE / P版 (2025年9月作成)。形名 RD77-U-APP |
| 原本PDF | `PDF/MELSEC iQ_Rシンプルモーションユニットユーザーズマニュアル(応用編).pdf` |
| 本ファイルの範囲 | 第13章 プログラミング 13.4 位置決めプログラム例 のうち「ブロック始動データ設定プログラム」から第13章の終わり(「軸停止プログラム」)まで(印刷 p.678-688 / PDF p.680-690)。前ファイル(13a)は13.4の「位置決めデータ設定プログラム」(印刷 p.677 / PDF p.679)まで、次ファイル(14a)は第14章 トラブルシューティング(印刷 p.689 / PDF p.691)から |
| ページ対応 | 印刷ページ = PDFページ − 2。本文中の「〇〇ページ参照」は印刷ページのまま |
| 変換日 | 2026-10-23 |
| 変換方法 | pypdfium2(本文) + PyMuPDF 200dpi 画像の目視(全ページ) |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。

転記上の扱い: 本範囲の原本はほぼすべてGX Works3のラダー図画面(ラベル表示)で、原本にニモニック記載は無いため、すべて「図から書き起こし」のニモニックで示した。プログラム名(原本の青帯見出し)を `####`、原本の■小見出しを `#####` とし、プログラム名で検索できるようにした。ステップ番号は原本のラダー図に表示されている回路先頭のステップ番号((0)、(20)、(311) 等)のみを記し、表示されていない途中のステップ番号は推測で付けていない。ラベル名・デバイス名・バッファメモリ表記(`U0¥G4321` 等)は原本の画面図どおりとし、ラベルに割付けデバイスが併記されている接点・出力は、ニモニック行の右側にそのデバイス(X1、Y10、DX10、U0¥G2417.F 等)を記した。接点記号は、a接点 = LD/AND/OR、b接点 = LDI/ANI/ORI、立上りパルス(↑)= LDP/ANDP、立下りパルス(↓)= LDF とした。1つの回路内で分岐して複数の出力を持つ回路は MPS/MRD/MPP で表した。ユニットFBの呼出し回路は、起動条件(i_bEN 等の入力接点)をニモニック、FB引数を表で示した。プログラム例の上下にある説明文はすべて原文のまま転記した。

## 主要用語 対訳表 (Glossary)(本ファイル範囲 / 原本 p.680-690)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| 位置決めプログラム例 | Positioning program examples | 13.4 | 参考訳 |
| エンジニアリングツール | Engineering tool | — | 参考訳 |
| ブロック始動データ | Block start data | uBlockData / uBlockInstData | 参考訳 |
| サーボパラメータ | Servo parameter | — | 参考訳 |
| 原点復帰要求 / 原点復帰要求フラグ | OPR request / OPR request flag | [Md.31] b3 | 参考訳 |
| 原点復帰要求フラグOFF要求 | OPR request flag OFF request | [Cd.19] / uClearHomingRequestFlag_D / U0¥G4321 | 参考訳 |
| 原点復帰未完時操作設定 | Operation setting for incompletion of OPR | [Pr.55] | 参考訳 |
| 外部指令機能 / 外部指令有効 | External command function / External command valid | [Cd.8] / uExternalCommandValid_D / U0¥G4305 | 参考訳 |
| シーケンサレディ信号 | PLC READY signal | Y0 / RD77_1.bPLC_Ready | 参考訳 |
| 全軸サーボON | All axis servo ON | Y1 / RD77_1.bAllAxisServoOn | 参考訳 |
| 同期用フラグ | Synchronization flag | X1 / RD77_1.bSynchronizationFlag | 参考訳 |
| 位置決め始動番号 | Positioning start No. | [Cd.3] / uPositioningStartNo | 参考訳 |
| 機械原点復帰 | Machine OPR | K9001 | 参考訳 |
| 高速原点復帰 | Fast OPR | K9002 | 参考訳 |
| 高度な位置決め制御 | Advanced positioning control | K7000 | 参考訳 |
| 速度・位置切換え制御 | Speed-position switching control | uEnableVP_Switching_D / U0¥G4328 | 参考訳 |
| 速度・位置切換え制御移動量変更レジスタ | Speed-position switching control movement amount change register | uVP_NewMovementAmount_D / U0¥G4326 | 参考訳 |
| 位置・速度切換え制御 | Position-speed switching control | uEnablePV_Switching_D / U0¥G4332 | 参考訳 |
| 位置・速度切換え制御速度変更レジスタ | Position-speed switching control speed change register | uPV_NewSpeed_D / U0¥G4330 | 参考訳 |
| 位置決め始動 / 位置決め始動信号 | Positioning start / Positioning start signal | Y10 / RD77_1.bnPositioningStart[0] | 参考訳 |
| 位置決め始動FB | Positioning start FB | M+RD77_StartPositioning_00C | 原本併記 |
| BUSY信号 | BUSY signal | X10 / RD77_1.bnBusy[0] | 参考訳 |
| RD77準備完了 | RD77 READY | X0 / RD77_1.bReady | 参考訳 |
| MコードOFF要求 | M code OFF request | [Cd.7] / uClear_M_Code_D / U0¥G4304 | 参考訳 |
| JOG運転 / インチング運転 | JOG operation / Inching operation | — | 参考訳 |
| JOG速度 / インチング移動量 | JOG speed / Inching movement amount | udJogOperationSpeed / uInchingMovementAmount | 参考訳 |
| JOG/インチング運転FB | JOG/inching operation FB | M+RD77_JOG_00C | 原本併記 |
| 手動パルサ運転 | Manual pulse generator operation | — | 参考訳 |
| 手動パルサ運転FB | Manual pulse generator OP FB | M+RD77_MPG_00C | 原本併記 |
| 速度変更 / 速度変更FB | Speed change / Speed change FB | M+RD77_ChangeSpeed_00C | 原本併記 |
| オーバーライド | Override | uOverride_D / U0¥G4313 | 参考訳 |
| 加減速時間変更 / 加減速時間変更FB | Acceleration/deceleration time change / Acc./dec. time SV change FB | M+RD77_ChangeAccDecTime_00E | 原本併記 |
| トルク変更 / 正転トルク制限値 | Torque change / New forward torque | uForwardNewTorque_D / U0¥G4325 | 参考訳 |
| ステップ運転 | Step operation | uStepMode_D U0¥G4344 / uStepValid_D U0¥G4345 / uStepStartInformation_D U0¥G4346 | 参考訳 |
| スキップ | Skip | uSkip_D / U0¥G4347 | 参考訳 |
| ティーチング | Teaching | uTeachingDataSelection_D U0¥G4348 / uTeachingPositioningDataNo_D U0¥G4349 | 参考訳 |
| 連続運転中断 | Continuous operation interrupt | uInterruptOperation_D / U0¥G4320 | 参考訳 |
| 目標位置変更 / 目標位置変更FB | Target position change / Target position change FB | M+RD77_ChangePosition_00C | 原本併記 |
| 再始動 / 再始動FB | Restart / Restart FB | M+RD77_Restart_00C | 原本併記 |
| パラメータ初期化 / パラメータ初期化FB | Parameter initialization / Parameter Initialization FB | M+RD77_InitializeParameter_00C | 原本併記 |
| フラッシュROM書込み / フラッシュROM書込みFB | Flash ROM writing / Flash ROM writing FB | M+RD77_WriteFlash_00C | 原本併記 |
| エラーリセット / エラー操作FB | Error reset / Error operation FB | M+RD77_OperateError_00C | 原本併記 |
| エラー検出 / 軸ワーニング検出 | Error detection / Axis warning detection | [Md.31] bD / b9(uStatus.D / uStatus.9) | 参考訳 |
| 軸停止 | Axis stop | uStopAxis_D / U0¥G30100 | 参考訳 |

## 変換範囲表(原本 p.680-690)

| 原本ページ | 節 | 扱い |
|---|---|---|
| PDF p.1-679 (印刷 p.-1～677) | 第1部～13.4「位置決めデータ設定プログラム」 | 本ファイル対象外(他ファイル 00～13a で変換) |
| PDF p.680 (印刷 p.678) | 13.4 ブロック始動データ設定プログラム、サーボパラメータ設定プログラム | 全文(プログラム例を含む) |
| PDF p.681 (印刷 p.679) | 13.4 原点復帰要求OFFプログラム、外部指令機能有効設定プログラム、シーケンサレディ信号[Y0]ONプログラム、全軸サーボON[Y1]プログラム | 全文(プログラム例を含む) |
| PDF p.682-683 (印刷 p.680-681) | 13.4 位置決め始動番号設定プログラム、位置決め始動プログラム | 全文(プログラム例を含む) |
| PDF p.684 (印刷 p.682) | 13.4 MコードOFFプログラム、JOG運転設定プログラム、インチング運転設定プログラム | 全文(プログラム例を含む) |
| PDF p.685 (印刷 p.683) | 13.4 JOG運転／インチング運転実行プログラム、手動パルサ運転プログラム | 全文(プログラム例を含む) |
| PDF p.686 (印刷 p.684) | 13.4 速度変更プログラム、オーバーライドプログラム、加減速時間変更プログラム | 全文(プログラム例を含む) |
| PDF p.687 (印刷 p.685) | 13.4 トルク変更プログラム、ステップ運転プログラム、スキッププログラム、ティーチングプログラム | 全文(プログラム例を含む) |
| PDF p.688 (印刷 p.686) | 13.4 連続運転中断プログラム、目標位置変更プログラム、再始動プログラム | 全文(プログラム例を含む) |
| PDF p.689 (印刷 p.687) | 13.4 パラメータ初期化プログラム、フラッシュROM書込みプログラム | 全文(プログラム例を含む) |
| PDF p.690 (印刷 p.688) | 13.4 エラーリセットプログラム、軸停止プログラム(第13章の終わり) | 全文(プログラム例を含む) |
| PDF p.691- (印刷 p.689-) | 第14章以降 | 本ファイル対象外(他ファイル 14a～ で変換) |

## 目次

- 13.4 位置決めプログラム例(後半)
  - ブロック始動データ設定プログラム(印刷 p.678)
  - サーボパラメータ設定プログラム(印刷 p.678)
  - 原点復帰要求OFFプログラム(印刷 p.679)
  - 外部指令機能有効設定プログラム(印刷 p.679)
  - シーケンサレディ信号[Y0]ONプログラム(印刷 p.679)
  - 全軸サーボON[Y1]プログラム(印刷 p.679)
  - 位置決め始動番号設定プログラム(印刷 p.680-681): 機械原点復帰 / 高速原点復帰 / 位置決めデータNo.1による位置決め / 速度・位置切換え制御(位置決めデータNo.2) / 位置・速度切換え制御(位置決めデータNo.3) / 高度な位置決め制御 / 高速原点復帰指令，高速原点復帰指令記憶のOFF
  - 位置決め始動プログラム(印刷 p.681)
  - MコードOFFプログラム(印刷 p.682)
  - JOG運転設定プログラム(印刷 p.682)
  - インチング運転設定プログラム(印刷 p.682)
  - JOG運転／インチング運転実行プログラム(印刷 p.683)
  - 手動パルサ運転プログラム(印刷 p.683)
  - 速度変更プログラム(印刷 p.684)
  - オーバーライドプログラム(印刷 p.684)
  - 加減速時間変更プログラム(印刷 p.684)
  - トルク変更プログラム(印刷 p.685)
  - ステップ運転プログラム(印刷 p.685)
  - スキッププログラム(印刷 p.685)
  - ティーチングプログラム(印刷 p.685)
  - 連続運転中断プログラム(印刷 p.686)
  - 目標位置変更プログラム(印刷 p.686)
  - 再始動プログラム(印刷 p.686)
  - パラメータ初期化プログラム(印刷 p.687)
  - フラッシュROM書込みプログラム(印刷 p.687)
  - エラーリセットプログラム(印刷 p.688)
  - 軸停止プログラム(印刷 p.688)
- 転記時の要確認一覧

## 13 プログラミング (13 / 印刷 p.678-688 / 原本 p.680-690)

### 13.4 位置決めプログラム例(続き) (13.4 / 印刷 p.678-688 / 原本 p.680-690)

(本ファイルは13.4の途中「ブロック始動データ設定プログラム」から始まる。13.4冒頭の説明、パラメータ設定プログラム、位置決めデータ設定プログラムは前ファイル 13a。)

#### ブロック始動データ設定プログラム (13.4 / 印刷 p.678 / 原本 p.680)

エンジニアリングツールの"ブロック始動データ"にて設定する場合，本プログラムは不要です。

【図】ラダー図(図から書き起こし)。2つの回路とも、起動接点は RD77_1.bSynchronizationFlag(X1)の立上り(↑)パルス接点。ステップ(0)は uBlockData[0]～[4] に値を転送後、TOP命令でバッファメモリ K22000 から5ワードへ書き込む。ステップ(161)は uBlockInstData[0]～[4] に H0 を転送後、TOP命令でバッファメモリ K22050 から5ワードへ書き込む。

```
(0)   LDP    RD77_1.bSynchronizationFlag                                   X1
      MOVP   H8001     uBlockData[0]
      MOVP   H8002     uBlockData[1]
      MOVP   H8005     uBlockData[2]
      MOVP   H800A     uBlockData[3]
      MOVP   H0F       uBlockData[4]
      TOP    H0        K22000    uBlockData[0]       K5

(161) LDP    RD77_1.bSynchronizationFlag                                   X1
      MOVP   H0        uBlockInstData[0]
      MOVP   H0        uBlockInstData[1]
      MOVP   H0        uBlockInstData[2]
      MOVP   H0        uBlockInstData[3]
      MOVP   H0        uBlockInstData[4]
      TOP    H0        K22050    uBlockInstData[0]   K5
```

#### サーボパラメータ設定プログラム (13.4 / 印刷 p.678 / 原本 p.680)

エンジニアリングツールの"サーボパラメータ"にて設定する場合，本プログラムは不要です。

[RD77MSの例]

【図】ラダー図(図から書き起こし)。起動接点は RD77_1.bSynchronizationFlag(X1)の立上り(↑)パルス接点。TOP命令の第1オペランドは RD77_1.uIO(表示上の割付けは H0)。

```
(0)   LDP    RD77_1.bSynchronizationFlag                                   X1
      TOP    RD77_1.uIO(H0)  K28403  H1  K1
      DMOVP  H1000     RD77_1.stnSvNetPrm_D[0].udConnectedDevice_D         U0¥G58020
```

#### 原点復帰要求OFFプログラム (13.4 / 印刷 p.679 / 原本 p.681)

エンジニアリングツールの"原点復帰詳細パラメータ"にて"[Pr.55]原点復帰未完時操作設定"を「1: 位置決め制御を実行する」に設定した場合，本プログラムは不要です。

【図】ラダー図(図から書き起こし)。
- ステップ(0): bInputOPRReqFlagOffReq(X20)のa接点で bOPRReqFlagOffReq_P をPLS。
- ステップ(20): bOPRReqFlagOffReq_P のa接点、RD77_1.bnPositioningStart[0](Y10)のb接点、RD77_1.stnAxMntr[0].uStatus.E のb接点の直列で bOPRReqFlagOffReq_H をSET。
- ステップ(42): bOPRReqFlagOffReq_H のa接点の後で分岐。上段は RD77_1.stnAxMntr[0].uStatus.3 のa接点を経て bOPRReqFlagOffReq をSET、下段は直接 bOPRReqFlagOffReq_H をRST。
- ステップ(86): bOPRReqFlagOffReq のa接点の後で分岐。上段は MOVP K1 → RD77_1.stnAxCtrl1_D[0].uClearHomingRequestFlag_D(U0¥G4321)、下段は比較 =_U K0 RD77_1.stnAxCtrl1_D[0].uClearHomingRequestFlag_D(U0¥G4321)が成立で bOPRReqFlagOffReq をRST。

```
(0)   LD     bInputOPRReqFlagOffReq                                        X20
      PLS    bOPRReqFlagOffReq_P

(20)  LD     bOPRReqFlagOffReq_P
      ANI    RD77_1.bnPositioningStart[0]                                  Y10
      ANI    RD77_1.stnAxMntr[0].uStatus.E
      SET    bOPRReqFlagOffReq_H

(42)  LD     bOPRReqFlagOffReq_H
      MPS
      AND    RD77_1.stnAxMntr[0].uStatus.3
      SET    bOPRReqFlagOffReq
      MPP
      RST    bOPRReqFlagOffReq_H

(86)  LD     bOPRReqFlagOffReq
      MOVP   K1        RD77_1.stnAxCtrl1_D[0].uClearHomingRequestFlag_D    U0¥G4321
      AND=_U K0        RD77_1.stnAxCtrl1_D[0].uClearHomingRequestFlag_D    U0¥G4321
      RST    bOPRReqFlagOffReq
```

#### 外部指令機能有効設定プログラム (13.4 / 印刷 p.679 / 原本 p.681)

【図】ラダー図(図から書き起こし)。

```
(0)   LD     bInputExternalCommandValidReq                                 X21
      MOVP   K1        RD77_1.stnAxCtrl1_D[0].uExternalCommandValid_D      U0¥G4305

(19)  LD     bInputExternalCommandInvalidReq                               X22
      MOVP   K0        RD77_1.stnAxCtrl1_D[0].uExternalCommandValid_D      U0¥G4305
```

#### シーケンサレディ信号[Y0]ONプログラム (13.4 / 印刷 p.679 / 原本 p.681)

【図】ラダー図(図から書き起こし)。RD77_1.bSynchronizationFlag(X1)、bBasicParamSetComp、bOPRParamSetComp のa接点と、bInitializeParameterReq、bWriteFlashReq のb接点の直列で RD77_1.bPLC_Ready(Y0)を出力。

```
(0)   LD     RD77_1.bSynchronizationFlag                                   X1
      AND    bBasicParamSetComp
      AND    bOPRParamSetComp
      ANI    bInitializeParameterReq
      ANI    bWriteFlashReq
      OUT    RD77_1.bPLC_Ready                                             Y0
```

#### 全軸サーボON[Y1]プログラム (13.4 / 印刷 p.679 / 原本 p.681)

【図】ラダー図(図から書き起こし)。

```
(0)   LD     bAllAxisServoOnReq                                            X4F
      AND    RD77_1.bPLC_Ready                                             Y0
      AND    RD77_1.bSynchronizationFlag_D                                 DX1
      OUT    RD77_1.bAllAxisServoOn                                        Y1
```

#### 位置決め始動番号設定プログラム (13.4 / 印刷 p.680-681 / 原本 p.682-683)

##### 機械原点復帰 (13.4 / 印刷 p.680 / 原本 p.682)

【図】ラダー図(図から書き起こし)。

```
(0)   LD     bInputOPRStartReq                                             X23
      MOVP   K9001     uPositioningStartNo
```

##### 高速原点復帰 (13.4 / 印刷 p.680 / 原本 p.682)

【図】ラダー図(図から書き起こし)。bInputFastOPRStartReq(X24)のa接点の後で3分岐。1段目は RD77_1.stnAxMntr[0].uStatus.3 のb接点を経て bFastOPRStartReq をSET、2段目は MOVP K9002 → uPositioningStartNo、3段目は bFastOPRStartReq_H をSET。

```
(34)  LD     bInputFastOPRStartReq                                         X24
      MPS
      ANI    RD77_1.stnAxMntr[0].uStatus.3
      SET    bFastOPRStartReq
      MRD
      MOVP   K9002     uPositioningStartNo
      MPP
      SET    bFastOPRStartReq_H
```

##### 位置決めデータNo.1による位置決め (13.4 / 印刷 p.680 / 原本 p.682)

【図】ラダー図(図から書き起こし)。

```
(91)  LD     bInputSetStartPositioningNoReq                                X25
      MOVP   K1        uPositioningStartNo
```

##### 速度・位置切換え制御(位置決めデータNo.2) (13.4 / 印刷 p.680 / 原本 p.682)

ABSモードの場合，変更後の移動量書込みは不要です。

【図】ラダー図(図から書き起こし)。

```
(112) LD     bInputSpeedPositionSwitchingReq                               X26
      MOVP   K2        uPositioningStartNo

(133) LD     bInputSpeedPositionSwitchingEnableReq                         X27
      MOVP   K1        RD77_1.stnAxCtrl1_D[0].uEnableVP_Switching_D        U0¥G4328

(157) LD     bInputSpeedPositionSwitchingDisableReq                        X28
      MOVP   K0        RD77_1.stnAxCtrl1_D[0].uEnableVP_Switching_D        U0¥G4328

(181) LD     bInputChangeSpeedPositionSwitchingMovementAmount              X29
      DMOVP  udMovementAmount  RD77_1.stnAxCtrl1_D[0].udVP_NewMovementAmount_D  U0¥G4326
```

##### 位置・速度切換え制御(位置決めデータNo.3) (13.4 / 印刷 p.680 / 原本 p.682)

【図】ラダー図(図から書き起こし)。

```
(200) LD     bInputPositionSpeedSwitchingReq                               X40
      MOVP   K3        uPositioningStartNo

(221) LD     bInputPositionSpeedSwitchingEnableReq                         X41
      MOVP   K1        RD77_1.stnAxCtrl1_D[0].uEnablePV_Switching_D        U0¥G4332

(245) LD     bInputPositionSpeedSwitchingDisableReq                        X42
      MOVP   K0        RD77_1.stnAxCtrl1_D[0].uEnablePV_Switching_D        U0¥G4332

(269) LD     bInputChangePositionSpeedSwitchingSpeedReq                    X43
      DMOV   udSpeed   RD77_1.stnAxCtrl1_D[0].udPV_NewSpeed_D              U0¥G4330
```

##### 高度な位置決め制御 (13.4 / 印刷 p.680 / 原本 p.682)

【図】ラダー図(図から書き起こし)。

```
(286) LD     bInputStartAdvancedPositioningReq                             X2A
      MOVP   K7000     uPositioningStartNo
```

##### 高速原点復帰指令，高速原点復帰指令記憶のOFF (13.4 / 印刷 p.681 / 原本 p.683)

高速原点復帰を使用しない場合は不要です。

【図】ラダー図(図から書き起こし)。6つのa接点(X23、X25、X26、X40、X2A、bPositioningStartReq)の並列(OR)で、bFastOPRStartReq と bFastOPRStartReq_H をRST。

```
(311) LD     bInputOPRStartReq                                             X23
      OR     bInputSetStartPositioningNoReq                                X25
      OR     bInputSpeedPositionSwitchingReq                               X26
      OR     bInputPositionSpeedSwitchingReq                               X40
      OR     bInputStartAdvancedPositioningReq                             X2A
      OR     bPositioningStartReq
      RST    bFastOPRStartReq
      RST    bFastOPRStartReq_H
```

#### 位置決め始動プログラム (13.4 / 印刷 p.681 / 原本 p.683)

[RD77MSの例]

【図】ラダー図(図から書き起こし)。
- ステップ(0): bInputStartPositioningReq(X2B)の立上り(↑)パルス接点、bDuringJogInchingOperation のb接点、bDuringMPGOperation のb接点に続き、「bFastOPRStartReq のb接点」と「bFastOPRStartReq のa接点と bFastOPRStartReq_H のa接点の直列」の並列ブロックを直列に接続して、bPositioningStartReq をSET。
- ステップ(10): bPositioningStartReq のa接点に、「RD77_1.stnAxMntr_D[0].uStatus_D.F(U0¥G2417.F)のa接点」と「RD77_1.stnAxMntr_D[0].uStatus_D.D(U0¥G2417.D)のa接点」の並列ブロック、RD77_1.bnBusy_D[0](DX10)のb接点を直列に接続して、bPositioningStartReq をRST。
- ステップ(21): bPositioningStartReq のa接点を位置決め始動FB(M_RD77_StartPositioning_1)の i_bEN に接続。

```
(0)   LDP    bInputStartPositioningReq                                     X2B
      ANI    bDuringJogInchingOperation
      ANI    bDuringMPGOperation
      LDI    bFastOPRStartReq
      LD     bFastOPRStartReq
      AND    bFastOPRStartReq_H
      ORB
      ANB
      SET    bPositioningStartReq

(10)  LD     bPositioningStartReq
      LD     RD77_1.stnAxMntr_D[0].uStatus_D.F                             U0¥G2417.F
      OR     RD77_1.stnAxMntr_D[0].uStatus_D.D                             U0¥G2417.D
      ANB
      ANI    RD77_1.bnBusy_D[0]                                            DX10
      RST    bPositioningStartReq

(21)  LD     bPositioningStartReq
      M_RD77_StartPositioning_1  (M+RD77_StartPositioning_00C)  Positioning start FB  ※引数は下表
```

ステップ(21) FB: インスタンス名 M_RD77_StartPositioning_1 / FB名 (M+RD77_StartPositioning_00C) / Positioning start FB

| 区分 | FB引数(型) | 接続先 |
|---|---|---|
| 入力 | B:i_bEN | bPositioningStartReq(a接点) |
| 入力 | DUT:i_stModule | RD77_1 |
| 入力 | UW:i_uAxis | K1 |
| 入力 | UW:i_uStartNo | uPositioningStartNo |
| 出力 | o_bENO:B | bStartPositioning_bENO(コイル) |
| 出力 | o_bOK:B | bStartPositioning_bOK(コイル) |
| 出力 | o_bErr:B | bStartPositioning_bErr(コイル) |
| 出力 | o_uErrId:UW | uStartPositioning_uErrId |

#### MコードOFFプログラム (13.4 / 印刷 p.682 / 原本 p.684)

【図】ラダー図(図から書き起こし)。

```
(0)   LD     bInputMcodeOffReq                                             X2C
      AND    RD77_1.stnAxMntr[0].uStatus.C
      MOVP   K1        RD77_1.stnAxCtrl1_D[0].uClear_M_Code_D              U0¥G4304
```

#### JOG運転設定プログラム (13.4 / 印刷 p.682 / 原本 p.684)

【図】ラダー図(図から書き起こし)。

```
(0)   LD     bInputSetJogSpeedReq                                          X2D
      DMOVP  K10000    udJogOperationSpeed
      MOVP   K0        uInchingMovementAmount
```

#### インチング運転設定プログラム (13.4 / 印刷 p.682 / 原本 p.684)

【図】ラダー図(図から書き起こし)。

```
(0)   LD     bInputSetInchingMovementAmountReq                             X44
      MOVP   K10       uInchingMovementAmount
```

#### JOG運転／インチング運転実行プログラム (13.4 / 印刷 p.683 / 原本 p.685)

[RD77MSの例]

【図】ラダー図(図から書き起こし)。
- ステップ(0): bInputForwardJogStartReq(X2E)と bInputReverseJogStartReq(X2F)のa接点の並列に、RD77_1.bReady(X0)のa接点、RD77_1.bnBusy[0](X10)のb接点を直列に接続して、bDuringJogInchingOperation をSET。
- ステップ(26): X2E のb接点と X2F のb接点の直列で bDuringJogInchingOperation をRST。
- ステップ(45): JOG/インチング運転FB(M_RD77_JOG_1)。i_bEN、i_bFJog、i_bRJog はそれぞれ別の接点から入力。

```
(0)   LD     bInputForwardJogStartReq                                      X2E
      OR     bInputReverseJogStartReq                                      X2F
      AND    RD77_1.bReady                                                 X0
      ANI    RD77_1.bnBusy[0]                                              X10
      SET    bDuringJogInchingOperation

(26)  LDI    bInputForwardJogStartReq                                      X2E
      ANI    bInputReverseJogStartReq                                      X2F
      RST    bDuringJogInchingOperation

(45)  LD     bDuringJogInchingOperation                ※i_bEN
      LD     bInputForwardJogStartReq          X2E     ※i_bFJog
      LD     bInputReverseJogStartReq          X2F     ※i_bRJog
      M_RD77_JOG_1  (M+RD77_JOG_00C)  JOG/inching operation FB  ※引数は下表
```

ステップ(45) FB: インスタンス名 M_RD77_JOG_1 / FB名 (M+RD77_JOG_00C) / JOG/inching operation FB

| 区分 | FB引数(型) | 接続先 |
|---|---|---|
| 入力 | B:i_bEN | bDuringJogInchingOperation(a接点) |
| 入力 | DUT:i_stModule | RD77_1 |
| 入力 | UW:i_uAxis | K1 |
| 入力 | B:i_bFJog | bInputForwardJogStartReq X2E(a接点) |
| 入力 | B:i_bRJog | bInputReverseJogStartReq X2F(a接点) |
| 入力 | UD:i_udJogSpeed | udJogOperationSpeed |
| 入力 | UW:i_uInching | K0 |
| 出力 | o_bENO:B | bJOG_bENO(コイル) |
| 出力 | o_bOK:B | bJOG_bOK(コイル) |
| 出力 | o_bErr:B | bJOG_bErr(コイル) |
| 出力 | o_uErrId:UW | uJOG_uErrId |

#### 手動パルサ運転プログラム (13.4 / 印刷 p.683 / 原本 p.685)

[RD77MSの例]

【図】ラダー図(図から書き起こし)。ステップ(0)の X30 は立上り(↑)パルス接点、ステップ(22)の X30 は立下り(↓)パルス接点。

```
(0)   LDP    bInputStartMPGReq                                             X30
      AND    RD77_1.bReady                                                 X0
      ANI    RD77_1.bnBusy[0]                                              X10
      SET    bDuringMPGOperation

(22)  LDF    bInputStartMPGReq                                             X30
      RST    bDuringMPGOperation

(43)  LD     bDuringMPGOperation
      M_RD77_MPG_1  (M+RD77_MPG_00C)  Manual pulse generator OP FB  ※引数は下表
```

ステップ(43) FB: インスタンス名 M_RD77_MPG_1 / FB名 (M+RD77_MPG_00C) / Manual pulse generator OP FB

| 区分 | FB引数(型) | 接続先 |
|---|---|---|
| 入力 | B:i_bEN | bDuringMPGOperation(a接点) |
| 入力 | DUT:i_stModule | RD77_1 |
| 入力 | UW:i_uAxis | K1 |
| 入力 | UD:i_udMPGInputMagnification | K1 |
| 出力 | o_bENO:B | bMPG_bENO(コイル) |
| 出力 | o_bOK:B | bMPG_bOK(コイル) |
| 出力 | o_bErr:B | bMPG_bErr(コイル) |
| 出力 | o_uErrId:UW | uMPG_uErrId |

#### 速度変更プログラム (13.4 / 印刷 p.684 / 原本 p.686)

[RD77MSの例]

【図】ラダー図(図から書き起こし)。ステップ(0)は X32 の立上り(↑)パルス接点と RD77_1.bnBusy[0](X10)のa接点の直列。

```
(0)   LDP    bInputChangeSpeedReq                                          X32
      AND    RD77_1.bnBusy[0]                                              X10
      SET    bChangeSpeedReq

(18)  LD     bChangeSpeed_bOK
      RST    bChangeSpeedReq

(35)  LD     bChangeSpeedReq
      M_RD77_ChangeSpeed_1  (M+RD77_ChangeSpeed_00C)  Speed change FB  ※引数は下表
```

ステップ(35) FB: インスタンス名 M_RD77_ChangeSpeed_1 / FB名 (M+RD77_ChangeSpeed_00C) / Speed change FB

| 区分 | FB引数(型) | 接続先 |
|---|---|---|
| 入力 | B:i_bEN | bChangeSpeedReq(a接点) |
| 入力 | DUT:i_stModule | RD77_1 |
| 入力 | UW:i_uAxis | K1 |
| 入力 | UD:i_udSpeedChangeValue | K20000 |
| 出力 | o_bENO:B | bChangeSpeed_bENO(コイル) |
| 出力 | o_bOK:B | bChangeSpeed_bOK(コイル) |
| 出力 | o_bErr:B | bChangeSpeed_bErr(コイル) |
| 出力 | o_uErrId:UW | uChangeSpeed_uErrId |

#### オーバーライドプログラム (13.4 / 印刷 p.684 / 原本 p.686)

【図】ラダー図(図から書き起こし)。

```
(0)   LD     bInputOverrideReq                                             X33
      PLS    bOverrideReq_P

(19)  LD     bOverrideReq_P
      AND    RD77_1.bnBusy[0]                                              X10
      MOVP   K200      RD77_1.stnAxCtrl1_D[0].uOverride_D                  U0¥G4313
```

#### 加減速時間変更プログラム (13.4 / 印刷 p.684 / 原本 p.686)

[RD77MSの例]

【図】ラダー図(図から書き起こし)。ステップ(0)は bInputChangeAccDecTimeDisable(X35)のb接点で bChangeAccDecTime_iEnable を出力。ステップ(2)は加減速時間変更FB(M_RD77_ChangeAccDecTime_00E_1)で、i_bEN と i_bEnable はそれぞれ別の接点から入力。

```
(0)   LDI    bInputChangeAccDecTimeDisable                                 X35
      OUT    bChangeAccDecTime_iEnable

(2)   LD     bInputChangeAccDecTimeReq                 X34     ※i_bEN
      LD     bChangeAccDecTime_iEnable                         ※i_bEnable
      M_RD77_ChangeAccDecTime_00E_1  (M+RD77_ChangeAccDecTime_00E)  Acc./dec. time SV change FB  ※引数は下表
```

ステップ(2) FB: インスタンス名 M_RD77_ChangeAccDecTime_00E_1 / FB名 (M+RD77_ChangeAccDecTime_00E) / Acc./dec. time SV change FB

| 区分 | FB引数(型) | 接続先 |
|---|---|---|
| 入力 | B: i_bEN | bInputChangeAccDecTimeReq X34(a接点) |
| 入力 | DUT: i_stModule | RD77_1 |
| 入力 | UW: i_uAxis | K1 |
| 入力 | B: i_bEnable | bChangeAccDecTime_iEnable(a接点) |
| 入力 | UD: i_udNewAccelerationTime | K2000 |
| 入力 | UD: i_udNewDecelerationTime | K0 |
| 出力 | o_bENO :B | bChangeAccDecTime_bENO(コイル) |
| 出力 | o_bOK :B | bChangeAccDecTime_bOK(コイル) |
| 出力 | o_bErr :B | bChangeAccDecTime_bErr(コイル) |
| 出力 | o_uErrId :UW | uChangeAccDecTime_uErrId |

#### トルク変更プログラム (13.4 / 印刷 p.685 / 原本 p.687)

【図】ラダー図(図から書き起こし)。

```
(0)   LD     bInputChangeTorqueReq                                         X36
      PLS    bChangeTorqueReq

(18)  LD     bChangeTorqueReq
      AND    RD77_1.bnBusy[0]                                              X10
      MOV    K1000     RD77_1.stnAxCtrl1_D[0].uForwardNewTorque_D          U0¥G4325
```

#### ステップ運転プログラム (13.4 / 印刷 p.685 / 原本 p.687)

【図】ラダー図(図から書き起こし)。ステップ(19)は3接点の直列の後で分岐し、MOV 2つを並列に駆動。

```
(0)   LD     bInputStepOperationReq                                        X37
      PLS    bStepOperationReq_P

(19)  LD     bStepOperationReq_P
      ANI    RD77_1.bnPositioningStart[0]                                  Y10
      ANI    RD77_1.stnAxMntr[0].uStatus.E
      MOV    K1        RD77_1.stnAxCtrl1_D[0].uStepMode_D                  U0¥G4344
      MOV    K1        RD77_1.stnAxCtrl1_D[0].uStepValid_D                 U0¥G4345

(65)  LD     bInputStepStartInformationReq                                 X46
      MOVP   K1        RD77_1.stnAxCtrl1_D[0].uStepStartInformation_D      U0¥G4346
```

#### スキッププログラム (13.4 / 印刷 p.685 / 原本 p.687)

【図】ラダー図(図から書き起こし)。ステップ(34)は bSkipReq のa接点の後で分岐し、上段は MOVP K1 → uSkip_D、下段は比較 =_U RD77_1.stnAxCtrl1_D[0].uSkip_D(U0¥G4347) K0 が成立で bSkipReq をRST。

```
(0)   LD     bInputSkipReq                                                 X38
      PLS    bSkipReq_P

(17)  LD     bSkipReq_P
      AND    RD77_1.bnBusy[0]                                              X10
      SET    bSkipReq

(34)  LD     bSkipReq
      MOVP   K1        RD77_1.stnAxCtrl1_D[0].uSkip_D                      U0¥G4347
      AND=_U RD77_1.stnAxCtrl1_D[0].uSkip_D  K0                            U0¥G4347
      RST    bSkipReq
```

#### ティーチングプログラム (13.4 / 印刷 p.685 / 原本 p.687)

【図】ラダー図(図から書き起こし)。ステップ(19)の RD77_1.bnBusy[0](X10)はb接点。ステップ(36)は bTeachingReq のa接点の後で3分岐し、1段目 MOVP K0 → uTeachingDataSelection_D、2段目 MOVP K1 → uTeachingPositioningDataNo_D、3段目は比較 =_U RD77_1.stnAxCtrl1_D[0].uTeachingPositioningDataNo_D(U0¥G4349) K0 が成立で bTeachingReq をRST。

```
(0)   LD     bInputTeachingReq                                             X39
      PLS    bTeachingReq_P

(19)  LD     bTeachingReq_P
      ANI    RD77_1.bnBusy[0]                                              X10
      SET    bTeachingReq

(36)  LD     bTeachingReq
      MOVP   K0        RD77_1.stnAxCtrl1_D[0].uTeachingDataSelection_D     U0¥G4348
      MOVP   K1        RD77_1.stnAxCtrl1_D[0].uTeachingPositioningDataNo_D U0¥G4349
      AND=_U RD77_1.stnAxCtrl1_D[0].uTeachingPositioningDataNo_D  K0       U0¥G4349
      RST    bTeachingReq
```

#### 連続運転中断プログラム (13.4 / 印刷 p.686 / 原本 p.688)

【図】ラダー図(図から書き起こし)。

```
(0)   LD     bInputStopContinuousOperationReq                              X3A
      PLS    bStopContinuousOperationReq_P

(19)  LD     bStopContinuousOperationReq_P
      AND    RD77_1.bnBusy[0]                                              X10
      MOV    K1        RD77_1.stnAxCtrl1_D[0].uInterruptOperation_D        U0¥G4320
```

#### 目標位置変更プログラム (13.4 / 印刷 p.686 / 原本 p.688)

[RD77MSの例]

【図】ラダー図(図から書き起こし)。ステップ(0)は X45 の立上り(↑)パルス接点と RD77_1.bnBusy[0](X10)のa接点の直列。

```
(0)   LDP    bInputTargetPositionChangeReq                                 X45
      AND    RD77_1.bnBusy[0]                                              X10
      SET    bTargetPositionChangeReq

(18)  LD     bChangePosition_bOK
      RST    bTargetPositionChangeReq

(35)  LD     bTargetPositionChangeReq
      M_RD77_ChangePosition_1  (M+RD77_ChangePosition_00C)  Target position change FB  ※引数は下表
```

ステップ(35) FB: インスタンス名 M_RD77_ChangePosition_1 / FB名 (M+RD77_ChangePosition_00C) / Target position change FB

| 区分 | FB引数(型) | 接続先 |
|---|---|---|
| 入力 | B:i_bEN | bTargetPositionChangeReq(a接点) |
| 入力 | DUT:i_stModule | RD77_1 |
| 入力 | UW:i_uAxis | K1 |
| 入力 | D:i_dTargetNewPosition | K3000 |
| 入力 | UD:i_udTargetNewSpeed | K1000000 |
| 出力 | o_bENO:B | bChangePosition_bENO(コイル) |
| 出力 | o_bOK:B | bChangePosition_bOK(コイル) |
| 出力 | o_bErr:B | bChangePosition_bErr(コイル) |
| 出力 | o_uErrId:UW | uChangePosition_uErrId |

#### 再始動プログラム (13.4 / 印刷 p.686 / 原本 p.688)

[RD77MSの例]

【図】ラダー図(図から書き起こし)。ステップ(0)の X3B は立上り(↑)パルス接点。

```
(0)   LDP    bInputRestartReq                                              X3B
      SET    bRestartReq

(14)  LD     bRestart_bOK
      RST    bRestartReq

(28)  LD     bRestartReq
      M_RD77_Restart_1  (M+RD77_Restart_00C)  Restart FB  ※引数は下表
```

ステップ(28) FB: インスタンス名 M_RD77_Restart_1 / FB名 (M+RD77_Restart_00C) / Restart FB

| 区分 | FB引数(型) | 接続先 |
|---|---|---|
| 入力 | B:i_bEN | bRestartReq(a接点) |
| 入力 | DUT:i_stModule | RD77_1 |
| 入力 | UW:i_uAxis | K1 |
| 出力 | o_bENO:B | bRestart_bENO(コイル) |
| 出力 | o_bOK:B | bRestart_bOK(コイル) |
| 出力 | o_bErr:B | bRestart_bErr(コイル) |
| 出力 | o_uErrId:UW | uRestart_uErrId |

#### パラメータ初期化プログラム (13.4 / 印刷 p.687 / 原本 p.689)

[RD77MSの例]

【図】ラダー図(図から書き起こし)。ステップ(0)の X3C は立上り(↑)パルス接点。

```
(0)   LDP    bInputInitializeParameterReq                                  X3C
      SET    bInitializeParameterReq

(19)  LD     bInitializeParameter_bOK
      RST    bInitializeParameterReq

(38)  LD     bInitializeParameterReq
      M_RD77_InitializeParameter_1  (M+RD77_InitializeParameter_00C)  Parameter Initialization FB  ※引数は下表
```

ステップ(38) FB: インスタンス名 M_RD77_InitializeParameter_1 / FB名 (M+RD77_InitializeParameter_00C) / Parameter Initialization FB

| 区分 | FB引数(型) | 接続先 |
|---|---|---|
| 入力 | B:i_bEN | bInitializeParameterReq(a接点) |
| 入力 | DUT:i_stModule | RD77_1 |
| 出力 | o_bENO:B | bInitializeParameter_bENO(コイル) |
| 出力 | o_bOK:B | bInitializeParameter_bOK(コイル) |
| 出力 | o_bErr:B | bInitializeParameter_bErr(コイル) |
| 出力 | o_uErrId:UW | uInitializeParameter_uErrId |

#### フラッシュ ROM書込みプログラム (13.4 / 印刷 p.687 / 原本 p.689)

[RD77MSの例]

【図】ラダー図(図から書き起こし)。ステップ(0)の X3D は立上り(↑)パルス接点。

```
(0)   LDP    bInputWriteFlashReq                                           X3D
      SET    bWriteFlashReq

(22)  LD     bWriteFlash_bOK
      RST    bWriteFlashReq

(44)  LD     bWriteFlashReq
      M_RD77_WriteFlash_1  (M+RD77_WriteFlash_00C)  Flash ROM writing FB  ※引数は下表
```

ステップ(44) FB: インスタンス名 M_RD77_WriteFlash_1 / FB名 (M+RD77_WriteFlash_00C) / Flash ROM writing FB

| 区分 | FB引数(型) | 接続先 |
|---|---|---|
| 入力 | B:i_bEN | bWriteFlashReq(a接点) |
| 入力 | DUT:i_stModule | RD77_1 |
| 出力 | o_bENO:B | bWriteFlash_bENO(コイル) |
| 出力 | o_bOK:B | bWriteFlash_bOK(コイル) |
| 出力 | o_bErr:B | bWriteFlash_bErr(コイル) |
| 出力 | o_uErrId:UW | uWriteFlash_uErrId |

#### エラーリセットプログラム (13.4 / 印刷 p.688 / 原本 p.690)

[RD77MSの例]

【図】ラダー図(図から書き起こし)。ステップ(0)は RD77_1.stnAxMntr[0].uStatus.D と RD77_1.stnAxMntr[0].uStatus.9 のa接点の並列で bErrReadReq を出力。ステップ(23)はエラー操作FB(M_RD77_OperateError_1)で、i_bEN と i_bErrReset はそれぞれ別の接点から入力。

```
(0)   LD     RD77_1.stnAxMntr[0].uStatus.D
      OR     RD77_1.stnAxMntr[0].uStatus.9
      OUT    bErrReadReq

(5)   LD     bInputErrResetReq                                             X3E
      PLS    bErrResetReq

(23)  LD     bErrReadReq                                       ※i_bEN
      LD     bErrResetReq                                      ※i_bErrReset
      M_RD77_OperateError_1  (M+RD77_OperateError_00C)  Error operation FB  ※引数は下表
```

ステップ(23) FB: インスタンス名 M_RD77_OperateError_1 / FB名 (M+RD77_OperateError_00C) / Error operation FB

| 区分 | FB引数(型) | 接続先 |
|---|---|---|
| 入力 | B:i_bEN | bErrReadReq(a接点) |
| 入力 | DUT:i_stModule | RD77_1 |
| 入力 | UW:i_uAxis | K1 |
| 入力 | B:i_bErrReset | bErrResetReq(a接点) |
| 出力 | o_bENO:B | bOperateError_bENO(コイル) |
| 出力 | o_bOK:B | bOperateError_bOK(コイル) |
| 出力 | o_bModuleErr:B | bOperateError_bModuleErr(コイル) |
| 出力 | o_uModuleErrId:UW | uOperateError_bModuleErrId |
| 出力 | o_bModuleWarn:B | bOperateError_bModuleWarn(コイル) |
| 出力 | o_uModuleWarnId:UW | uOperateError_bModuleWarnId |
| 出力 | o_bErr:B | bOperateError_bModuleErr(コイル) |
| 出力 | o_uErrId:UW | uOperateError_uErrId |

#### 軸停止プログラム (13.4 / 印刷 p.688 / 原本 p.690)

【図】ラダー図(図から書き起こし)。ステップ(27)の X3F はb接点。

```
(0)   LD     bInputStopReq                                                 X3F
      PLS    bStopReq_P

(15)  LD     bStopReq_P
      SET    RD77_1.stnAxCtrl2_D[0].uStopAxis_D.0                          U0¥G30100.0

(27)  LDI    bInputStopReq                                                 X3F
      RST    RD77_1.stnAxCtrl2_D[0].uStopAxis_D                            U0¥G30100
```

(第13章はここまで。次ページ(印刷 p.689 / 原本 p.691)から第14章 トラブルシューティング。)

## 転記時の要確認一覧

- (印刷 p.678-688 / 原本 p.680-690) ラダー図の中間ステップ番号は原本に表示が無いため記載していない(回路先頭のステップ番号のみ記載)。MPS/MRD/MPP・ORB/ANB による表現は図の接続から書き起こしたもので、原本に記載は無い。
- (印刷 p.678 / 原本 p.680) サーボパラメータ設定プログラムの TOP 命令の第1オペランドは「RD77_1.uIO」の下に「H0」と表示されている(ラベルと割付け値の併記と判断し `RD77_1.uIO(H0)` と表記)。
- (印刷 p.679 / 原本 p.681) 原点復帰要求OFFプログラム ステップ(86)の比較は「=_U K0 RD77_1.stnAxCtrl1_D[0].uClearHomingRequestFlag_D」(K0 が先)、スキッププログラム・ティーチングプログラムの比較は「=_U <バッファメモリ> K0」(K0 が後)で、オペランドの順序が異なる。原文どおり転記。
- (印刷 p.679 / 原本 p.681) 全軸サーボON[Y1]プログラムの3つ目の接点は「RD77_1.bSynchronizationFlag_D」(割付け DX1)。シーケンサレディ信号[Y0]ONプログラムの「RD77_1.bSynchronizationFlag」(X1)とは別表記。原文どおり。
- (印刷 p.680 / 原本 p.682) 位置・速度切換え制御 ステップ(269)は DMOV(非パルス)、速度・位置切換え制御 ステップ(181)は DMOVP(パルス)。原文どおり。ステップ(181)の接点ラベル「bInputChangeSpeedPositionSwitchingMovementAmount」は末尾に Req が付いていない。原文どおり。
- (印刷 p.681 / 原本 p.683) 位置決め始動プログラム ステップ(10)の接点は「RD77_1.stnAxMntr_D[0].uStatus_D.F / .D」(U0¥G2417.F / .D)と「RD77_1.bnBusy_D[0]」(DX10)で、他プログラムの「RD77_1.stnAxMntr[0].uStatus.x」「RD77_1.bnBusy[0]」(X10)とは別表記。原文どおり。
- (印刷 p.681 / 原本 p.683) 位置決め始動プログラム ステップ(0)の並列ブロックは「bFastOPRStartReq のb接点」と「bFastOPRStartReq のa接点 + bFastOPRStartReq_H のa接点」。上段の接点名は bFastOPRStartReq、下段の2つ目は「bFastOPRStartReq_H」(図上の改行は「bFastOPRS / tartReq_H」)と判読。
- (印刷 p.684 / 原本 p.686) 速度変更プログラム・目標位置変更プログラムのステップ(0)、オーバーライドプログラムのステップ(19)、トルク変更・スキップ・連続運転中断プログラムの BUSY 接点(X10)はa接点、ティーチングプログラムのステップ(19)の X10 はb接点。原文どおり。
- (印刷 p.684 / 原本 p.686) 加減速時間変更プログラムの画面図は他のラダー図より文字色が薄い(灰色)表示。内容は判読可能。
- (印刷 p.685 / 原本 p.687) トルク変更プログラム ステップ(18)とステップ運転プログラム ステップ(19)、連続運転中断プログラム ステップ(19)は MOV(非パルス)。起動接点は PLS 出力のパルス信号。原文どおり。
- (印刷 p.688 / 原本 p.690) エラーリセットプログラムで、FB出力 o_bModuleErr と o_bErr の接続先コイルがどちらも「bOperateError_bModuleErr」と表示されている(o_bErr 側の誤植の可能性)。また o_uModuleErrId / o_uModuleWarnId の接続先ラベルは「uOperateError_bModuleErrId」「uOperateError_bModuleWarnId」(u接頭辞だが b を含む)。原文どおり転記。
- (印刷 p.688 / 原本 p.690) 軸停止プログラムで、SET の対象は「RD77_1.stnAxCtrl2_D[0].uStopAxis_D.0 / U0¥G30100.0」(ビット指定)、RST の対象は「RD77_1.stnAxCtrl2_D[0].uStopAxis_D / U0¥G30100」(ビット指定なし)と表示されている。原文どおり転記。
- (印刷 p.681, 683-688 / 原本 p.683, 685-690) 一部のラダー図の左下に水色の帯(画面の選択枠と思われる)が写っているが、回路の内容には関係しないため転記していない。
