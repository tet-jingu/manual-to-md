# 13 プログラミング[FX5-SSC-G] (13章 / 原本 p.653-697)

FX5 モーションユニット／シンプルモーションユニット ユーザーズマニュアル(応用編) IB(名)-0300252-M 参照用リファレンス

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」(本ファイルおよび `00_索引_ladder_reference.md`)を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
>
> 表記注:
> - 「原本 p.N」は **PDFのページ番号**。原本の印刷ページ番号 = PDFページ − 2。本文中の相互参照(「139ページ ブロック始動」等)は原文(印刷ページ)のまま。
> - 原本の結合セルは各行に展開しています(該当表の直後に注記)。
> - 図は【図】プレースホルダ＋読み取れた事実の箇条書きです。
> - 原本の「☞」(参照ページ記号)は「→」、「📖」(別マニュアル参照記号)は「[別マニュアル]」、`U1¥G` は `U1\G` で表記しています。

## 変換範囲表 (本ファイルの管理情報)

| 原本ページ | 節 | 扱い |
|---|---|---|
| p.653 | 13.1 プログラム作成上の注意事項 | 全文 |
| p.654 | 13.2 プログラムの作成 | 全文 |
| p.655-697 | 13.3 位置決めプログラム例(ラベル使用時) | 全文(ラダーはニモニック書き起こし) |

## 目次

- 13 プログラミング[FX5-SSC-G]
- 13.1 プログラム作成上の注意事項
  - データの読出し／書込み
  - 速度変更実行間隔の制約
  - オーバーラン時の処理
  - システム構成
- 13.2 プログラムの作成
  - プログラムの全体構成
- 13.3 位置決めプログラム例(ラベル使用時)
  - 使用するラベル一覧
  - プログラム例
  - パラメータ設定プログラム
  - 位置決めデータ設定プログラム
  - ブロック始動データ設定プログラム
  - 原点復帰要求OFFプログラム
  - 外部指令機能有効設定プログラム
  - シーケンサレディ信号ONプログラム
  - 全軸サーボONプログラム

---

## 13 プログラミング[FX5-SSC-G] (13章 / 原本 p.653)

モーションユニットを使った位置決め制御を行うために必要なプログラムについて説明しています。制御に必要なプログラムは，「始動条件」，「始動タイムチャート」，「デバイス設定」，制御全体の構成などを考慮して作成します。(実行したい制御に合わせて，パラメータや位置決めデータ，ブロック始動データ，条件データなどをモーションユニットに設定し，制御データの設定プログラムや各制御の始動プログラムを作成する必要があります。)

## 13.1 プログラム作成上の注意事項 (13.1 / 原本 p.653)

CPUユニットからモーションユニットのバッファメモリへデータを書き込むときの，共通の注意事項を示します。

### データの読出し／書込み (13.1 / 原本 p.653)

本章に示すデータの設定(各種パラメータ，位置決めデータ，ブロック始動データ)は，できるだけエンジニアリングツールで行われることをおすすめします。プログラムで設定する場合，かなりのプログラムとデバイスを使用するため，複雑になると共に，スキャンタイムの増大につながります｡また，連続軌跡制御または連続位置決め制御中に位置決めデータを書き換える場合は，4つ前の位置決めデータを実行するまでに書き換えてください。4つ前の位置決めデータを実行する前に位置決めデータの書換えが行われていない場合，データは書き換えられていないものとして処理されます。

### 速度変更実行間隔の制約 (13.1 / 原本 p.653)

モーションユニットで速度変更機能またはオーバーライド機能により連続して速度変更を行う場合は，速度変更の間隔が10 ms以上となるようにしてください。

### オーバーラン時の処理 (13.1 / 原本 p.653)

詳細パラメータ1でストロークリミット上限値および下限値の設定にて，オーバーランの防止にはなります。ただし，これはモーションユニットが正常に動作している場合のみ有効です。システムの安全性からみて限界リミットスイッチを設け，リミットスイッチ作動によって，サーボアンプの主回路電源をOFFするような外部の回路を設けることをおすすめします。

### システム構成 (13.1 / 原本 p.653)

プログラム例で使用するシステム構成を示します。

【図】プログラム例のシステム構成(原本 p.653)
- (1)FX5U-32MR/ES
- (2)FX5-80SSC-G
- (3)FX5-16EX/ES
- (4)FX5-16EX/ES
- 外部機器 → (1) へ「X00~X17」，(3) へ「X20~X37」，(4) へ「X40~X54」の入力を接続
- (2)FX5-80SSC-G に「サーボアンプ(MR-J5-_G_)」を接続し，サーボアンプに「サーボモータ」を接続

## 13.2 プログラムの作成 (13.2 / 原本 p.654)

本節では，実際に使用する「位置決め制御の運転プログラム」について説明します。

### プログラムの全体構成 (13.2 / 原本 p.654)

位置決め制御の運転プログラムの全体構成を示します。

| No. | プログラム名 | 備考 |
|---|---|---|
| 1 | パラメータ設定プログラム | • エンジニアリングツールにてパラメータ，位置決めデータ，ブロック始動データ，サーボパラメータを設定する場合，プログラムは不要です。<br>• 機械原点復帰制御を行わない場合は，原点復帰用パラメータの設定は不要です。 |
| 2 | 位置決めデータ設定プログラム | • エンジニアリングツールにてパラメータ，位置決めデータ，ブロック始動データ，サーボパラメータを設定する場合，プログラムは不要です。<br>• 機械原点復帰制御を行わない場合は，原点復帰用パラメータの設定は不要です。 |
| 3 | ブロック始動データ設定プログラム | • エンジニアリングツールにてパラメータ，位置決めデータ，ブロック始動データ，サーボパラメータを設定する場合，プログラムは不要です。<br>• 機械原点復帰制御を行わない場合は，原点復帰用パラメータの設定は不要です。 |
| 4 | 原点復帰要求OFFプログラム | 機械原点復帰制御を行う場合は不要です。 |
| 5 | 外部指令機能有効設定プログラム | — |
| 6 | シーケンサレディ信号ONプログラム | — |
| 7 | 全軸サーボONプログラム | — |
| 8 | 位置決め始動番号設定プログラム | — |
| 9 | 位置決め始動プログラム | — |
| 10 | MコードOFFプログラム | Ｍコード出力機能を使用しない場合は不要です。 |
| 11 | JOG運転設定プログラム | JOG運転を使用しない場合は不要です。 |
| 12 | インチング運転設定プログラム | インチング運転を使用しない場合は不要です。 |
| 13 | JOG運転／インチング運転実行プログラム | JOG運転およびインチング運転を使用しない場合は不要です。 |
| 14 | 手動パルサ運転プログラム | 手動パルサ運転を使用しない場合は不要です。 |
| 15 | 速度変更プログラム | 必要に応じて追加するプログラムです。 |
| 16 | オーバーライドプログラム | 必要に応じて追加するプログラムです。 |
| 17 | 加減速時間変更プログラム | 必要に応じて追加するプログラムです。 |
| 18 | トルク変更プログラム | 必要に応じて追加するプログラムです。 |
| 19 | 目標位置変更プログラム | 必要に応じて追加するプログラムです。 |
| 20 | サーボパラメータ読出し／書込みプログラム | 必要に応じて追加するプログラムです。 |
| 21 | ステップ運転プログラム | 必要に応じて追加するプログラムです。 |
| 22 | スキッププログラム | 必要に応じて追加するプログラムです。 |
| 23 | ティーチングプログラム | 必要に応じて追加するプログラムです。 |
| 24 | 連続運転中断プログラム | 必要に応じて追加するプログラムです。 |
| 25 | 再始動プログラム | 必要に応じて追加するプログラムです。 |
| 26 | パラメータ初期化プログラム | 必要に応じて追加するプログラムです。 |
| 27 | フラッシュ ROM書込みプログラム | 必要に応じて追加するプログラムです。 |
| 28 | エラーリセットプログラム | 必要に応じて追加するプログラムです。 |
| 29 | 軸停止プログラム | — |

※原本では備考列の No.1〜3，No.5〜8，No.15〜28 がそれぞれ結合セル。各行に展開。

## 13.3 位置決めプログラム例(ラベル使用時) (13.3 / 原本 p.655-697)

### 使用するラベル一覧 (13.3 / 原本 p.655-656)

プログラム例では，使用するラベルを下記のように割り付けています。

#### ユニットラベル (13.3 / 原本 p.655-656)

| 分類 | ラベル名 | 内容 |
|---|---|---|
| 入力信号 | FX5SSC_1.stSysCtrl_D.bAllAxisServoOn_D | 全軸サーボON |
| 入力信号 | FX5SSC_1.stSysMntr2_D.bReady_D | 準備完了 |
| 入力信号 | FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D | 同期用フラグ |
| 入力信号 | FX5SSC_1.stSysMntr2_D.bnBusy_D[0] | 軸1 BUSY信号 |
| 出力信号 | FX5SSC_1.stSysCtrl_D.bPLC_Ready_D | シーケンサレディ信号 |
| 出力信号 | FX5SSC_1.stnAxCtrl2_D[0].uPositioningStart_D.0 | 軸1 位置決め始動信号 |
| パラメータ | FX5SSC_1.stnAxPrm_D[0].dHomePosition_D | 軸1 原点アドレス |
| パラメータ | FX5SSC_1.stnAxPrm_D[0].dSoftwareStrokeLowerLimit_D | 軸1 ソフトウェアストロークリミット下限値 |
| パラメータ | FX5SSC_1.stnAxPrm_D[0].dSoftwareStrokeUpperLimit_D | 軸1 ソフトウェアストロークリミット上限値 |
| パラメータ | FX5SSC_1.stnAxPrm_D[0].uExternalCommandFunctionMode_D | 軸1 外部指令機能選択 |
| パラメータ | FX5SSC_1.stnAxPrm_D[0].uExternalCommandSignalMode_D | 軸1 外部指令信号選択 |
| パラメータ | FX5SSC_1.stnAxPrm_D[0].uUnitMagnification_D | 軸1 単位倍率(AM) |
| パラメータ | FX5SSC_1.stnAxPrm_D[0].uUnit_D | 軸1 単位設定 |
| パラメータ | FX5SSC_1.stnAxPrm_D[0].uVP_Mode_D | 軸1 速度･位置機能選択 |
| パラメータ | FX5SSC_1.stnAxPrm_D[0].uV_CommandPosition_D | 軸1 速度制御時の送り現在値 |
| パラメータ | FX5SSC_1.stnAxPrm_D[0].udHomingSpeed_D | 軸1 原点復帰速度 |
| パラメータ | FX5SSC_1.stnAXPrm_D[0].udJogSpeedLimit_D | 軸1 JOG速度制限値 |
| パラメータ | FX5SSC_1.stnAxPrm_D[0].udMovementAmountPerRotation_D | 軸1 1回転あたりの移動量(AL) |
| パラメータ | FX5SSC_1.stnAxPrm_D[0].udPulsesPerRotation_D | 軸1 1回転あたりのパルス数(AP) |
| パラメータ | FX5SSC_1.stnAXPrm_D[0].udSpeedLimitValue_D | 軸1 速度制限値 |
| 軸モニタデータ | FX5SSC_1.stnAxMntr_D[0].uStatus_D.3 | 軸1 原点復帰要求フラグ |
| 軸モニタデータ | FX5SSC_1.stnAxMntr_D[0].uStatus_D.9 | 軸1 軸ワーニング検出 |
| 軸モニタデータ | FX5SSC_1.stnAxMntr_D[0].uStatus_D.C | 軸1 MコードON |
| 軸モニタデータ | FX5SSC_1.stnAxMntr_D[0].uStatus_D.D | 軸1 エラー検出 |
| 軸モニタデータ | FX5SSC_1.stnAxMntr_D[0].uStatus_D.E | 軸1 始動完了 |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uClearHomingRequestFlag_D | 軸1 原点復帰要求フラグOFF要求 |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uClear_M_Code_D | 軸1 MコードOFF要求 |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uEnablePV_Switching_D | 軸1 位置・速度切換え許可フラグ |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uEnableVP_Switching_D | 軸1 速度・位置切換え許可フラグ |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uExternalCommandValid_D | 軸1 外部指令有効 |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uForwardNewTorque_D | 軸1トルク変更値/正転トルク変更値 |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uInchingMovementAmount_D | 軸1 インチング移動量 |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uInterruptOperation_D | 軸1 連続運転中断要求 |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uOverride_D | 軸1 位置決め運転速度オーバーライド |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uSkip_D | 軸1 スキップ指令 |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uStepMode_D | 軸1 ステップモード |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uStepStartInformation_D | 軸1 ステップ始動情報 |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uStepValid_D | 軸1 ステップ有効フラグ |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uTeachingDataSelection_D | 軸1 ティーチングデータ選択 |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uTeachingPositioningDataNo_D | 軸1 ティーチング位置決めデータNo. |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].udJOG_Speed_D | 軸1 JOG速度 |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].udPV_NewSpeed_D | 軸1 位置・速度切換え制御速度変更レジスタ |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].udVP_NewMovementAmount_D | 軸1 速度・位置切換え制御移動量変更レジスタ |
| システム制御データ | FX5SSC_1.stSysCtrl_D.dInputValueForManualPulseGeneratorViaCPU_D | 軸1 CPU経由手動パルサ入力値 |
| 軸制御データ2 | FX5SSC_1.stnAxCtrl2_D[0].uStopAxis_D.0 | 軸1 軸停止 |

※原本では分類列が分類ごとに結合セル。各行に展開。最終行(軸制御データ2)は原本 p.656 に続く。ラベル名中の「stnAXPrm_D」(大文字X)は原本の表記のまま。

#### グローバルラベル (13.3 / 原本 p.656)

プログラム例で使用しているグローバルラベルを示します。下記のようにグローバルラベルを設定してください。

- 割付けデバイスを設定しないグローバルラベル(割付けデバイスを設定していない場合，使用していない内部リレーやデータデバイスが自動で割り付けられます。)

| No. | ラベル名 | データ型 | クラス | 割付け(デバイス/ラベル) | Japanese/日本語(表示対象) |
|---|---|---|---|---|---|
| 1 | G_bInitializeParameterReq | ビット | VAR_GLOBAL | (空欄) | パラメータ初期化指令 |
| 2 | G_bWriteFlashReq | ビット | VAR_GLOBAL | (空欄) | フラッシュROM書込み指令 |
| 3 | G_bDuringJogInchingOperation | ビット | VAR_GLOBAL | (空欄) | JOG/インチング運転中フラグ |
| 4 | G_bDuringMPGOperation | ビット | VAR_GLOBAL | (空欄) | 手動パルサ運転中フラグ |

- 割付けデバイスを設定するグローバルラベル

| No. | ラベル名 | データ型 | クラス | 割付け(デバイス/ラベル) | Japanese/日本語(表示対象) |
|---|---|---|---|---|---|
| 8 | G_bInputOPRReqFlagOffReq | ビット | VAR_GLOBAL | X2 | 原点復帰要求OFF指令 |
| 9 | G_bInputExternalCommandValidReq | ビット | VAR_GLOBAL | X3 | 外部指令有効指令 |
| 10 | G_bInputExternalCommandInvalidReq | ビット | VAR_GLOBAL | X4 | 外部指令無効指令 |
| 11 | G_bInputOPRStartReq | ビット | VAR_GLOBAL | X5 | 機械原点復帰指令 |
| 12 | G_bInputFastOPRStartReq | ビット | VAR_GLOBAL | X6 | 高速原点復帰指令 |
| 13 | G_bInputSetStartPositioningNoReq | ビット | VAR_GLOBAL | X7 | 位置決め始動指令 |
| 14 | G_bInputSpeedPositionSwitchingReq | ビット | VAR_GLOBAL | X10 | 速度･位置切換え運転指令 |
| 15 | G_bInputSpeedPositionSwitchingEnableReq | ビット | VAR_GLOBAL | X11 | 速度･位置切換え許可指令 |
| 16 | G_bInputSpeedPositionSwitchingDisableReq | ビット | VAR_GLOBAL | X12 | 速度･位置切換え禁止指令 |
| 17 | G_bInputChangeSpeedPositionSwitchingMovementAmount | ビット | VAR_GLOBAL | X13 | 移動量変更指令 |
| 18 | G_bInputStartAdvancedPositioningReq | ビット | VAR_GLOBAL | X14 | 高度な位置決め制御始動指令 |
| 19 | G_bInputStartPositioningReq | ビット | VAR_GLOBAL | X15 | 位置決め始動指令 |
| 20 | G_bInputMcodeOffReq | ビット | VAR_GLOBAL | X16 | MコードOFF要求 |
| 21 | G_bInputSetJogSpeedReq | ビット | VAR_GLOBAL | X17 | JOG運転速度設定指令 |
| 22 | G_bInputForwardJogStartReq | ビット | VAR_GLOBAL | X20 | 正転JOG/インチング指令 |
| 23 | G_bInputReverseJogStartReq | ビット | VAR_GLOBAL | X22 | 逆転JOG/インチング指令 |
| 24 | G_bInputStartMPGReq | ビット | VAR_GLOBAL | X23 | 手動パルサ運転指令 |
| 25 | G_bInputChangeSpeedReq | ビット | VAR_GLOBAL | X24 | 速度変更指令 |
| 26 | G_bInputOverrideReq | ビット | VAR_GLOBAL | X25 | オーバーライド指令 |
| 27 | G_bInputChangeAccDecTimeReq | ビット | VAR_GLOBAL | X26 | 加減速時間変更指令 |
| 28 | G_bInputChangeAccDecTimeDisable | ビット | VAR_GLOBAL | X27 | 加減速時間変更不許可指令 |
| 29 | G_bInputChangeTorqueReq | ビット | VAR_GLOBAL | X30 | トルク変更指令 |
| 30 | G_bInputStepOperationReq | ビット | VAR_GLOBAL | X31 | ステップ運転指令 |
| 31 | G_bInputSkipReq | ビット | VAR_GLOBAL | X32 | スキップ指令 |
| 32 | G_bInputTeachingReq | ビット | VAR_GLOBAL | X33 | ティーチング指令 |
| 33 | G_bInputStopContinuousOperationReq | ビット | VAR_GLOBAL | X34 | 連続運転中断指令 |
| 34 | G_bInputRestartReq | ビット | VAR_GLOBAL | X35 | 再始動指令 |
| 35 | G_bInputInitializeParameterReq | ビット | VAR_GLOBAL | X36 | パラメータ初期化指令 |
| 36 | G_bInputWriteFlashReq | ビット | VAR_GLOBAL | X37 | フラッシュROM書込み指令 |
| 37 | G_bInputErrResetReq | ビット | VAR_GLOBAL | X40 | エラーリセット指令 |
| 38 | G_bInputStopReq | ビット | VAR_GLOBAL | X41 | 停止指令 |
| 39 | G_bInputPositionSpeedSwitchingReq | ビット | VAR_GLOBAL | X42 | 位置･速度切換え運転指令 |
| 40 | G_bInputPositionSpeedSwitchingEnableReq | ビット | VAR_GLOBAL | X43 | 位置･速度切換え許可指令 |
| 41 | G_bInputPositionSpeedSwitchingDisableReq | ビット | VAR_GLOBAL | X44 | 位置･速度切換え禁止指令 |
| 42 | G_bInputChangePositionSpeedSwitchingSpeedReq | ビット | VAR_GLOBAL | X45 | 速度変更指令 |
| 43 | G_bInputSetInchingMovementAmountReq | ビット | VAR_GLOBAL | X46 | インチング移動量設定指令 |
| 44 | G_bInputTargetPositionChangeReq | ビット | VAR_GLOBAL | X47 | 目標位置変更指令 |
| 45 | G_bInputStepStartInformationReq | ビット | VAR_GLOBAL | X50 | ステップ始動情報指令 |
| 46 | G_bInputG_bInputSpeedPositionSwitchingAbsSetReq | ビット | VAR_GLOBAL | X51 | 速度･位置切換え(ABS)設定指令 |
| 47 | G_bAllAxisServoOnReq | ビット | VAR_GLOBAL | X52 | 全軸サーボON指令 |
| 48 | G_bInputServoParamChange | ビット | VAR_GLOBAL | X53 | サーボパラメータ変更指令 |
| 49 | G_bInputServoParamRead | ビット | VAR_GLOBAL | X54 | サーボパラメータ読出し指令 |

※原本はGX Works3のラベル設定画面のキャプチャ。行番号は画面の行番号のまま(2つ目の表は8から始まる。5〜7行目は原本に記載なし)。No.46のラベル名「G_bInputG_bInputSpeedPositionSwitchingAbsSetReq」は原本表記のまま。

### プログラム例(ラベル使用時) (13.3 / 原本 p.657-697)

ユニットFBの詳細は下記マニュアルの"シンプルモーションユニット／モーションユニットFB"を参照してください。
[別マニュアル]MELSEC iQ-F FX5モーションユニット／シンプルモーションユニットFBリファレンス

表記注(本節のニモニック): 各命令のオペランドは原本のラベル名で記載し，原本に併記されたバッファメモリ(U1\G…)・割付けデバイス(X51等)と原本のデバイスコメントを `//` の後に記載。FB(ファンクションブロック)は原本にニモニックが示されていないため，`FBCALL <インスタンス名>` の後に各ピンの接続を `ピン名 := 入力` / `ピン名 => 出力先` で記載。原本の「¥」は「\」で表記。ステートメント(水色の帯)は `// ` で該当命令の直前に記載。

### パラメータ設定プログラム (13.3 / 原本 p.657-658)

エンジニアリングツールの"ユニットパラメータ"にてパラメータを設定する場合，本プログラムは不要です。
下記のようにローカルラベルを設定してください。

| No. | ラベル名 | データ型 | クラス | Japanese/日本語(表示対象) |
|---|---|---|---|---|
| 1 | bServoNetworkCompositionParamSetComp | ビット | VAR | サーボネットワーク構成パラメータ設定完了 |
| 2 | bBasicParamSetComp | ビット | VAR | 基本パラメータ1設定完了 |
| 3 | bDetailedParamSetComp | ビット | VAR | 詳細パラメータ2設定完了 |
| 4 | bOPRParamSetComp | ビット | VAR | 原点復帰基本パラメータ設定完了 |
| 5 | (空欄) | (空欄) | (空欄) | (空欄) |

#### サーボネットワーク構成パラメータ(軸1)の設定 (13.3 / 原本 p.657)

```
// [Title]サーボネットワーク構成パラメータ(軸1)の設定
// 変更する場合はバッファメモリに値を設定後，フラッシュROM書込みを行ってください
(0)  LDP  FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D   // U1\G31500.1  R:同期用フラグ(ダイレクト)
     // IPアドレス:192.168.3.1の設定
     MOV  H301 U1\G58024   // 軸1 IPアドレス(L)
     // IPアドレス:192.168.3.1の設定
     MOV  H0C0A8 U1\G58025   // 軸1 IPアドレス(H)
     // マルチドロップ番号:0の設定
     MOV  H0 U1\G58028
```

- 原本図では本回路の出力は上記3命令のみ(bServoNetworkCompositionParamSetComp をSETする命令は図中に記載なし。要確認)。次回路のステップ番号は(185)。

#### 基本パラメータ1(軸1)の設定 (13.3 / 原本 p.657)

```
// [Title]基本パラメータ1(軸1)の設定
(185) LDP  FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D   // U1\G31500.1  R:同期用フラグ(ダイレクト)
     // 単位設定(0:mm)
     MOV  K0 FX5SSC_1.stnAxPrm_D[0].uUnit_D   // U1\G0  RW:単位設定(ダイレクト)
     // 単位倍率設定(×1倍)
     MOV  K1 FX5SSC_1.stnAxPrm_D[0].uUnitMagnification_D   // U1\G1  RW:単位倍率(AM)(ダイレクト)
     // 1回転あたりのパルス数(4194304pls)
     DMOVP K4194304 FX5SSC_1.stnAxPrm_D[0].udPulsesPerRotation_D   // U1\G2  RW:1回転あたりのパルス数(AP)(ダイレクト)
     // 1回転あたりの移動量(25000.0μm)
     DMOVP K250000 FX5SSC_1.stnAxPrm_D[0].udMovementAmountPerRotation_D   // U1\G4  RW:1回転あたりの移動量(AL)(ダイレクト)
     SET  bBasicParamSetComp   // 基本パラメータ1設定完了
```

#### 詳細パラメータ2(軸1)の設定 (13.3 / 原本 p.658)

```
// [Title]詳細パラメータ2(軸1)の設定
(336) LDP  FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D   // U1\G31500.1  R:同期用フラグ(ダイレクト)
     // 外部指令機能選択(2:速度⇔位置 制御切換要求)
     MOVP K2 FX5SSC_1.stnAxPrm_D[0].uExternalCommandFunctionMode_D   // U1\G62  RW:外部指令機能選択(ダイレクト)
     // 外部指令信号選択(101:軸1のDOG信号)
     MOVP K101 FX5SSC_1.stnAxPrm_D[0].uExternalCommandSignalMode_D   // U1\G69  RW:外部指令信号選択(ダイレクト)
     SET  bDetailedParamSetComp   // 詳細パラメータ2設定完了
```

#### 原点復帰基本パラメータ(軸1)の設定 (13.3 / 原本 p.658)

原点復帰方式や原点復帰のデータは，使用するドライバのパラメータで設定してください。

```
// [Title]原点復帰基本パラメータ(軸1)の設定
(442) LDP  FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D   // U1\G31500.1  R:同期用フラグ(ダイレクト)
     // 原点アドレス(0.0um)
     DMOVP K0 FX5SSC_1.stnAxPrm_D[0].dHomePosition_D   // U1\G72  RW:原点アドレス(ダイレクト)
     // 原点復帰速度(1000.00mm/min)
     DMOVP K100000 FX5SSC_1.stnAxPrm_D[0].udHomingSpeed_D   // U1\G74  RW:原点復帰速度(ダイレクト)
     SET  bOPRParamSetComp   // 原点復帰基本パラメータ設定完了
```

#### 単位degree用設定(軸1)プログラム (13.3 / 原本 p.659)

```
// [Title]単位degree用設定(軸1)プログラム
(541) LDP  FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D   // U1\G31500.1  R:同期用フラグ(ダイレクト)
     AND  G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   // X51  速度・位置切換え(ABS)設定指令
     // 単位設定(2:degree)
     MOVP K2 FX5SSC_1.stnAxPrm_D[0].uUnit_D   // U1\G0  RW:単位設定(ダイレクト)
     // 1回転あたりの移動量(90.00000degree)
     DMOVP K9000000 FX5SSC_1.stnAxPrm_D[0].udMovementAmountPerRotation_D   // U1\G4  RW:1回転あたりの移動量(AL)(ダイレクト)
     // 速度制限値(20000.000degree/min)
     DMOVP K20000000 FX5SSC_1.stnAxPrm_D[0].udSpeedLimitValue_D   // U1\G10  RW:速度制限値(ダイレクト)
     // ソフトウェアストロークリミット上限値(0.00000degree/min)
     DMOVP K0 FX5SSC_1.stnAxPrm_D[0].dSoftwareStrokeUpperLimit_D   // U1\G18  RW:ソフトウェアストロークリミット上限値(ダイレクト)
     // ソフトウェアストロークリミット下限値(0.00000degree/min)
     DMOVP K0 FX5SSC_1.stnAxPrm_D[0].dSoftwareStrokeLowerLimit_D   // U1\G20  RW:ソフトウェアストロークリミット下限値(ダイレクト)
     // 速度制御時の送り現在値(1:送り現在値の更新を行う)
     MOVP K1 FX5SSC_1.stnAxPrm_D[0].uV_CommandPosition_D   // U1\G30  RW:速度制御時の送り現在値(ダイレクト)
     // 速度・位置機能選択(2:速度・位置切換え制御(ABSモード))
     MOVP K2 FX5SSC_1.stnAxPrm_D[0].uVP_Mode_D   // U1\G34  RW:速度・位置機能選択(ダイレクト)
     // JOG速度制限値(20000.000degree/min)
     DMOVP K20000000 FX5SSC_1.stnAxPrm_D[0].udJogSpeedLimit_D   // U1\G48  RW:JOG速度制限値(ダイレクト)
     // 原点復帰速度(1000.000degree/min)
     DMOVP K1000000 FX5SSC_1.stnAxPrm_D[0].udHomingSpeed_D   // U1\G74  RW:原点復帰速度(ダイレクト)
```

- ステートメント中の単位表記(ソフトウェアストロークリミット「degree/min」等)は原本の表記のまま。

### 位置決めデータ設定プログラム (13.3 / 原本 p.660-678)

エンジニアリングツールの"位置決めデータ"にて設定する場合，本プログラムは不要です。
下記のようにローカルラベルを設定してください。

| No. | ラベル名 | データ型 | クラス | Japanese/日本語(表示対象) |
|---|---|---|---|---|
| 1 | bSetPositioningData_bEN | ビット | VAR | No1実行命令 |
| 2 | bSetPositioningData2_bEN | ビット | VAR | No2実行命令 |
| 3 | bSetPositioningData3_bEN | ビット | VAR | No3実行命令 |
| 4 | bSetPositioningData4_bEN | ビット | VAR | No4実行命令 |
| 5 | bSetPositioningData5_bEN | ビット | VAR | No5実行命令 |
| 6 | bSetPositioningData6_bEN | ビット | VAR | No6実行命令 |
| 7 | bSetPositioningData10_bEN | ビット | VAR | No10実行命令 |
| 8 | bSetPositioningData11_bEN | ビット | VAR | No11実行命令 |
| 9 | bSetPositioningData15_bEN | ビット | VAR | No15実行命令 |
| 10 | (空欄) | (空欄) | (空欄) | (空欄) |

#### No.1位置決めデータ設定プログラム (13.3 / 原本 p.661-662)

```
// [Title]No.1位置決めデータ設定プログラム
// <位置決め識別子>
//   運転パターン:位置決め終了
//   制御方式:1軸の直線制御(ABS)
//   加速時間No.:1，減速時間No.:2
//   Mコード:9843
(959) LDP  FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D   // (U1\G31500.1) R:同期用フラグ(ダイレクト)
     MOV  K0 M_FX5SSC_SetPositioningData_01A_1.pb_uOpePattern          // Da.1:運転パターン
     MOV  H1 M_FX5SSC_SetPositioningData_01A_1.pb_uCtrlSys             // Da.2:制御方式
     MOV  K1 M_FX5SSC_SetPositioningData_01A_1.pb_uAccTimeNo           // Da.3:加速時間No.
     MOV  K2 M_FX5SSC_SetPositioningData_01A_1.pb_uDecTimeNo           // Da.4:減速時間No.
     MOV  K9843 M_FX5SSC_SetPositioningData_01A_1.pb_uMcode    // Da.10:Mコード
     MOV  K300 M_FX5SSC_SetPositioningData_01A_1.pb_uDwellTime       // Da.9:ドウェルタイム
     DMOV K18000 M_FX5SSC_SetPositioningData_01A_1.pb_udCmdSpd     // Da.8:指令速度
     MPS
     AND  G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   // (X51) 速度・位置切換え(ABS)設定指令
     DMOV K1200000 M_FX5SSC_SetPositioningData_01A_1.pb_udCmdSpd    // Da.8:指令速度
     MRD
     DMOV K-500000 M_FX5SSC_SetPositioningData_01A_1.pb_dPositAdr    // Da.6:位置決めアドレス
     MRD
     AND  G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   // (X51) 速度・位置切換え(ABS)設定指令
     DMOV K27000000 M_FX5SSC_SetPositioningData_01A_1.pb_dPositAdr   // Da.6:位置決めアドレス
     MPP
     DMOV K0 M_FX5SSC_SetPositioningData_01A_1.pb_dArcAdr              // Da.7:円弧アドレス
     MOV  K0 M_FX5SSC_SetPositioningData_01A_1.pb_uInterpolationAxisNo1   // Da.20:補間対象軸番号1
     MOV  K0 M_FX5SSC_SetPositioningData_01A_1.pb_uInterpolationAxisNo2   // Da.21:補間対象軸番号2
     MOV  K0 M_FX5SSC_SetPositioningData_01A_1.pb_uInterpolationAxisNo3   // Da.22:補間対象軸番号3
     SET  bSetPositioningData_bEN                      // No1実行命令
(1189) LD   bSetPositioningData_bEN                       // No1実行命令
     FBCALL M_FX5SSC_SetPositioningData_01A_1                          // (M+FX5SSC_SetPositioningData_01A) Positioning data setting FB
          i_bEN      (B)   := 上記接点(bSetPositioningData_bEN)   // 実行指令
          i_stModule (DUT) := FX5SSC_1                 // ユニットラベル / ユニットラベル
          i_uAxis    (UW)  := K1                       // 対象軸
          i_uDataNo  (UW)  := K1                       // 位置決めデータNo.
          o_bENO     (B)   => (接続先の記載なし)       // 実行状態
          o_bOK      (B)   => (接続先の記載なし)       // 正常完了
          o_bErr     (B)   => (接続先の記載なし)       // 異常完了
          o_uErrId   (UW)  => (接続先の記載なし)       // エラーコード
          // FBブロック内の表示(パブリック変数): pb_uOpePattern, pb_uCtrlSys, pb_uAccTimeNo, pb_uDecTimeNo, pb_uMcode, pb_uDwellTime, pb_udCmdSpd, pb_dPositAdr, pb_dArcAdr, pb_uInterpolationAxisNo1, pb_uInterpolationAxisNo2, pb_uInterpolationAxisNo3
```

- ステップ(959): 同期用フラグは立上り検出接点(LDP)。X51(G_bInputG_bInputSpeedPositionSwitchingAbsSetReq)はa接点で，Da.8指令速度の2つ目のDMOV(K1200000)と，Da.6位置決めアドレスの2つ目のDMOV(K27000000)の直前にそれぞれ直列に入る。他の出力はすべて同期用フラグの条件のみ。原本はラダー図のため MPS/MRD/MPP は本書き起こしで補ったもの。
- ステップ(1189): FBの出力ピンは原本では線が右へ延びているのみで，接続先の記載なし。原本 p.662 はこのFB回路で終わる。

#### No.2位置決めデータ設定プログラム (13.3 / 原本 p.663-664)

```
// [Title]No.2位置決めデータ設定プログラム
// <位置決め識別子>
//   運転パターン:位置決め終了
//   制御方式:速度・位置切換え制御(正転)
//   加速時間No.:1，減速時間No.:2
(1500) LDP  FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D   // (U1\G31500.1) R:同期用フラグ(ダイレクト)
     MOV  K0 M_FX5SSC_SetPositioningData_01A_2.pb_uOpePattern          // Da.1:運転パターン
     MOV  H6 M_FX5SSC_SetPositioningData_01A_2.pb_uCtrlSys             // Da.2:制御方式
     MOV  K1 M_FX5SSC_SetPositioningData_01A_2.pb_uAccTimeNo           // Da.3:加速時間No.
     MOV  K2 M_FX5SSC_SetPositioningData_01A_2.pb_uDecTimeNo           // Da.4:減速時間No.
     MOV  K0 M_FX5SSC_SetPositioningData_01A_2.pb_uMcode    // Da.10:Mコード
     MOV  K300 M_FX5SSC_SetPositioningData_01A_2.pb_uDwellTime       // Da.9:ドウェルタイム
     DMOV K18000 M_FX5SSC_SetPositioningData_01A_2.pb_udCmdSpd     // Da.8:指令速度
     MPS
     AND  G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   // (X51) 速度・位置切換え(ABS)設定指令
     DMOV K3600000 M_FX5SSC_SetPositioningData_01A_2.pb_udCmdSpd    // Da.8:指令速度
     MRD
     DMOV K25000 M_FX5SSC_SetPositioningData_01A_2.pb_dPositAdr    // Da.6:位置決めアドレス
     MRD
     AND  G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   // (X51) 速度・位置切換え(ABS)設定指令
     DMOV K9000000 M_FX5SSC_SetPositioningData_01A_2.pb_dPositAdr   // Da.6:位置決めアドレス
     MPP
     DMOV K0 M_FX5SSC_SetPositioningData_01A_2.pb_dArcAdr              // Da.7:円弧アドレス
     MOV  K0 M_FX5SSC_SetPositioningData_01A_2.pb_uInterpolationAxisNo1   // Da.20:補間対象軸番号1
     MOV  K0 M_FX5SSC_SetPositioningData_01A_2.pb_uInterpolationAxisNo2   // Da.21:補間対象軸番号2
     MOV  K0 M_FX5SSC_SetPositioningData_01A_2.pb_uInterpolationAxisNo3   // Da.22:補間対象軸番号3
     SET  bSetPositioningData2_bEN                      // No2実行命令
(1695) LD   bSetPositioningData2_bEN                       // No2実行命令
     FBCALL M_FX5SSC_SetPositioningData_01A_2                          // (M+FX5SSC_SetPositioningData_01A) Positioning data setting FB
          i_bEN      (B)   := 上記接点(bSetPositioningData2_bEN)   // 実行指令
          i_stModule (DUT) := FX5SSC_1                 // ユニットラベル / ユニットラベル
          i_uAxis    (UW)  := K1                       // 対象軸
          i_uDataNo  (UW)  := K2                       // 位置決めデータNo.
          o_bENO     (B)   => (接続先の記載なし)       // 実行状態
          o_bOK      (B)   => (接続先の記載なし)       // 正常完了
          o_bErr     (B)   => (接続先の記載なし)       // 異常完了
          o_uErrId   (UW)  => (接続先の記載なし)       // エラーコード
          // FBブロック内の表示(パブリック変数): pb_uOpePattern, pb_uCtrlSys, pb_uAccTimeNo, pb_uDecTimeNo, pb_uMcode, pb_uDwellTime, pb_udCmdSpd, pb_dPositAdr, pb_dArcAdr, pb_uInterpolationAxisNo1, pb_uInterpolationAxisNo2, pb_uInterpolationAxisNo3
```

- ステップ(1500): 同期用フラグは立上り検出接点(LDP)。X51(G_bInputG_bInputSpeedPositionSwitchingAbsSetReq)はa接点で，Da.8指令速度の2つ目のDMOV(K3600000)と，Da.6位置決めアドレスの2つ目のDMOV(K9000000)の直前にそれぞれ直列に入る。他の出力はすべて同期用フラグの条件のみ。原本はラダー図のため MPS/MRD/MPP は本書き起こしで補ったもの。
- ステップ(1695): FBの出力ピンは原本では線が右へ延びているのみで，接続先の記載なし。原本 p.664 はこのFB回路で終わる。

#### No.3位置決めデータ設定プログラム (13.3 / 原本 p.665-666)

```
// [Title]No.3位置決めデータ設定プログラム
// <位置決め識別子>
//   運転パターン:位置決め終了
//   制御方式:位置・速度切換え制御(正転)
//   加速時間No.:1，減速時間No.:2
(2006) LDP  FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D   // (U1\G31500.1) R:同期用フラグ(ダイレクト)
     MOV  K0 M_FX5SSC_SetPositioningData_01A_3.pb_uOpePattern          // Da.1:運転パターン
     MOV  H8 M_FX5SSC_SetPositioningData_01A_3.pb_uCtrlSys             // Da.2:制御方式
     MOV  K1 M_FX5SSC_SetPositioningData_01A_3.pb_uAccTimeNo           // Da.3:加速時間No.
     MOV  K2 M_FX5SSC_SetPositioningData_01A_3.pb_uDecTimeNo           // Da.4:減速時間No.
     MOV  K0 M_FX5SSC_SetPositioningData_01A_3.pb_uMcode    // Da.10:Mコード
     MOV  K300 M_FX5SSC_SetPositioningData_01A_3.pb_uDwellTime       // Da.9:ドウェルタイム
     DMOV K18000 M_FX5SSC_SetPositioningData_01A_3.pb_udCmdSpd     // Da.8:指令速度
     MPS
     AND  G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   // (X51) 速度・位置切換え(ABS)設定指令
     DMOV K3600000 M_FX5SSC_SetPositioningData_01A_3.pb_udCmdSpd    // Da.8:指令速度
     MRD
     DMOV K200000 M_FX5SSC_SetPositioningData_01A_3.pb_dPositAdr    // Da.6:位置決めアドレス
     MRD
     AND  G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   // (X51) 速度・位置切換え(ABS)設定指令
     DMOV K72000000 M_FX5SSC_SetPositioningData_01A_3.pb_dPositAdr   // Da.6:位置決めアドレス
     MPP
     DMOV K0 M_FX5SSC_SetPositioningData_01A_3.pb_dArcAdr              // Da.7:円弧アドレス
     MOV  K0 M_FX5SSC_SetPositioningData_01A_3.pb_uInterpolationAxisNo1   // Da.20:補間対象軸番号1
     MOV  K0 M_FX5SSC_SetPositioningData_01A_3.pb_uInterpolationAxisNo2   // Da.21:補間対象軸番号2
     MOV  K0 M_FX5SSC_SetPositioningData_01A_3.pb_uInterpolationAxisNo3   // Da.22:補間対象軸番号3
     SET  bSetPositioningData3_bEN                      // No3実行命令
(2201) LD   bSetPositioningData3_bEN                       // No3実行命令
     FBCALL M_FX5SSC_SetPositioningData_01A_3                          // (M+FX5SSC_SetPositioningData_01A) Positioning data setting FB
          i_bEN      (B)   := 上記接点(bSetPositioningData3_bEN)   // 実行指令
          i_stModule (DUT) := FX5SSC_1                 // ユニットラベル / ユニットラベル
          i_uAxis    (UW)  := K1                       // 対象軸
          i_uDataNo  (UW)  := K3                       // 位置決めデータNo.
          o_bENO     (B)   => (接続先の記載なし)       // 実行状態
          o_bOK      (B)   => (接続先の記載なし)       // 正常完了
          o_bErr     (B)   => (接続先の記載なし)       // 異常完了
          o_uErrId   (UW)  => (接続先の記載なし)       // エラーコード
          // FBブロック内の表示(パブリック変数): pb_uOpePattern, pb_uCtrlSys, pb_uAccTimeNo, pb_uDecTimeNo, pb_uMcode, pb_uDwellTime, pb_udCmdSpd, pb_dPositAdr, pb_dArcAdr, pb_uInterpolationAxisNo1, pb_uInterpolationAxisNo2, pb_uInterpolationAxisNo3
```

- ステップ(2006): 同期用フラグは立上り検出接点(LDP)。X51(G_bInputG_bInputSpeedPositionSwitchingAbsSetReq)はa接点で，Da.8指令速度の2つ目のDMOV(K3600000)と，Da.6位置決めアドレスの2つ目のDMOV(K72000000)の直前にそれぞれ直列に入る。他の出力はすべて同期用フラグの条件のみ。原本はラダー図のため MPS/MRD/MPP は本書き起こしで補ったもの。
- ステップ(2201): FBの出力ピンは原本では線が右へ延びているのみで，接続先の記載なし。原本 p.666 はこのFB回路で終わる。

#### No.4位置決めデータ設定プログラム (13.3 / 原本 p.667-668)

```
// [Title]No.4位置決めデータ設定プログラム
// <位置決め識別子>
//   運転パターン：位置決め終了
//   制御方式：1軸の直線制御(INC)
//   加速時間No.：1，減速時間No.：2
(2512) LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      // U1\G31500.1 R:同期用フラグ(ダイレクト)
       MOV   K0  M_FX5SSC_SetPositioningData_01A_4.pb_uOpePattern            // Da.1：運転パターン
       MOV   H2  M_FX5SSC_SetPositioningData_01A_4.pb_uCtrlSys                 // Da.2：制御方式
       MOV   K1  M_FX5SSC_SetPositioningData_01A_4.pb_uAccTimeNo               // Da.3：加速時間No.
       MOV   K2  M_FX5SSC_SetPositioningData_01A_4.pb_uDecTimeNo               // Da.4：減速時間No.
       MOV   K0  M_FX5SSC_SetPositioningData_01A_4.pb_uMcode                   // Da.10：Mコード
       MOV   K300  M_FX5SSC_SetPositioningData_01A_4.pb_uDwellTime            // Da.9：ドウェルタイム
       DMOV  K9000  M_FX5SSC_SetPositioningData_01A_4.pb_udCmdSpd             // Da.8：指令速度
       MPS
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   // X51 速度・位置切換え(ABS)設定指令
       DMOV  K1800000  M_FX5SSC_SetPositioningData_01A_4.pb_udCmdSpd             // Da.8：指令速度
       MPP
       DMOV  K50000  M_FX5SSC_SetPositioningData_01A_4.pb_dPositAdr            // Da.6：位置決めアドレス
       MPS
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   // X51 速度・位置切換え(ABS)設定指令
       DMOV  K18000000  M_FX5SSC_SetPositioningData_01A_4.pb_dPositAdr            // Da.6：位置決めアドレス
       MPP
       DMOV  K0  M_FX5SSC_SetPositioningData_01A_4.pb_dArcAdr                  // Da.7：円弧アドレス
       MOV   K0  M_FX5SSC_SetPositioningData_01A_4.pb_uInterpolationAxisNo1    // Da.20：補間対象軸番号1
       MOV   K0  M_FX5SSC_SetPositioningData_01A_4.pb_uInterpolationAxisNo2    // Da.21：補間対象軸番号2     (原本 p.668)
       MOV   K0  M_FX5SSC_SetPositioningData_01A_4.pb_uInterpolationAxisNo3    // Da.22：補間対象軸番号3
       SET   bSetPositioningData4_bEN              // No4実行命令

(2705) LD    bSetPositioningData4_bEN              // No4実行命令
       // FB呼出し: M_FX5SSC_SetPositioningData_01A_4 (M+FX5SSC_SetPositioningData_01A) Positioning data setting FB
       //   入力  B: i_bEN         ← (上記接点)      実行指令
       //   入力  DUT: i_stModule  ← FX5SSC_1        ユニットラベル
       //   入力  UW: i_uAxis      ← K1              対象軸
       //   入力  UW: i_uDataNo    ← K4              位置決めデータNo.
       //   出力  o_bENO :B   実行状態    (接続先ラベルなし)
       //   出力  o_bOK :B    正常完了    (接続先ラベルなし)
       //   出力  o_bErr :B   異常完了    (接続先ラベルなし)
       //   出力  o_uErrId :UW エラーコード (接続先ラベルなし)
       //   FB内部の公開変数(FBボックス下部の表示): pb_uOpePattern, pb_uCtrlSys, pb_uAccTimeNo, pb_uDecTimeNo, pb_uMcode, pb_uDwellTime, pb_udCmdSpd, pb_dPositAdr, pb_dArcAdr, pb_uInterpolationAxisNo1, pb_uInterpolationAxisNo2, pb_uInterpolationAxisNo3
       CALL  M_FX5SSC_SetPositioningData_01A_4  (i_bEN, FX5SSC_1, K1, K4)
```
- ステップ(2512)の回路は原本 p.667 から p.668 へ続く(補間対象軸番号2以降が p.668)。ステップ(2705)の FB 回路は原本 p.668。
- 図中コメント: FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D = U1\G31500.1「R:同期用フラグ(ダイレクト)」(立上り接点)，G_bInputG_bInputSpeedPositionSwitchingAbsSetReq = X51「速度・位置切換え(ABS)設定指令」，bSetPositioningData4_bEN「No4実行命令」
- X51(速度・位置切換え(ABS)設定指令)の a接点は，Da.8 指令速度の2つ目の DMOV(K1800000)と，Da.6 位置決めアドレスの2つ目の DMOV(K18000000)の直前にのみ直列に入る(母線側の分岐点は同期用フラグ接点の直後)。
- 出力側 o_bENO / o_bOK / o_bErr / o_uErrId は原本では右母線まで線が延びているのみで，ラベルは接続されていない。
- ニモニックの MPS/MPP および CALL 行は原本ラダー図からの書き起こし表記(原本はラダー図のみでニモニック表示なし)。

#### No.5位置決めデータ設定プログラム (13.3 / 原本 p.669-670)

```
// [Title]No.5位置決めデータ設定プログラム
// <位置決め識別子>
//   運転パターン：連続位置決め制御
//   制御方式：1軸の直線制御(INC)
//   加速時間No.：1，減速時間No.：2
(3016) LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      // U1\G31500.1 R:同期用フラグ(ダイレクト)
       MOV   K1  M_FX5SSC_SetPositioningData_01A_5.pb_uOpePattern            // Da.1：運転パターン
       MOV   H2  M_FX5SSC_SetPositioningData_01A_5.pb_uCtrlSys                 // Da.2：制御方式
       MOV   K1  M_FX5SSC_SetPositioningData_01A_5.pb_uAccTimeNo               // Da.3：加速時間No.
       MOV   K2  M_FX5SSC_SetPositioningData_01A_5.pb_uDecTimeNo               // Da.4：減速時間No.
       MOV   K0  M_FX5SSC_SetPositioningData_01A_5.pb_uMcode                   // Da.10：Mコード
       MOV   K300  M_FX5SSC_SetPositioningData_01A_5.pb_uDwellTime            // Da.9：ドウェルタイム
       DMOV  K36000  M_FX5SSC_SetPositioningData_01A_5.pb_udCmdSpd             // Da.8：指令速度
       MPS
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   // X51 速度・位置切換え(ABS)設定指令
       DMOV  K6000000  M_FX5SSC_SetPositioningData_01A_5.pb_udCmdSpd             // Da.8：指令速度
       MPP
       DMOV  K100000  M_FX5SSC_SetPositioningData_01A_5.pb_dPositAdr            // Da.6：位置決めアドレス
       MPS
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   // X51 速度・位置切換え(ABS)設定指令
       DMOV  K36000000  M_FX5SSC_SetPositioningData_01A_5.pb_dPositAdr            // Da.6：位置決めアドレス
       MPP
       DMOV  K0  M_FX5SSC_SetPositioningData_01A_5.pb_dArcAdr                  // Da.7：円弧アドレス
       MOV   K0  M_FX5SSC_SetPositioningData_01A_5.pb_uInterpolationAxisNo1    // Da.20：補間対象軸番号1
       MOV   K0  M_FX5SSC_SetPositioningData_01A_5.pb_uInterpolationAxisNo2    // Da.21：補間対象軸番号2     (原本 p.670)
       MOV   K0  M_FX5SSC_SetPositioningData_01A_5.pb_uInterpolationAxisNo3    // Da.22：補間対象軸番号3
       SET   bSetPositioningData5_bEN              // No5実行命令

(3211) LD    bSetPositioningData5_bEN              // No5実行命令
       // FB呼出し: M_FX5SSC_SetPositioningData_01A_5 (M+FX5SSC_SetPositioningData_01A) Positioning data setting FB
       //   入力  B: i_bEN         ← (上記接点)      実行指令
       //   入力  DUT: i_stModule  ← FX5SSC_1        ユニットラベル
       //   入力  UW: i_uAxis      ← K1              対象軸
       //   入力  UW: i_uDataNo    ← K5              位置決めデータNo.
       //   出力  o_bENO :B   実行状態    (接続先ラベルなし)
       //   出力  o_bOK :B    正常完了    (接続先ラベルなし)
       //   出力  o_bErr :B   異常完了    (接続先ラベルなし)
       //   出力  o_uErrId :UW エラーコード (接続先ラベルなし)
       //   FB内部の公開変数(FBボックス下部の表示): pb_uOpePattern, pb_uCtrlSys, pb_uAccTimeNo, pb_uDecTimeNo, pb_uMcode, pb_uDwellTime, pb_udCmdSpd, pb_dPositAdr, pb_dArcAdr, pb_uInterpolationAxisNo1, pb_uInterpolationAxisNo2, pb_uInterpolationAxisNo3
       CALL  M_FX5SSC_SetPositioningData_01A_5  (i_bEN, FX5SSC_1, K1, K5)
```
- ステップ(3016)の回路は原本 p.669 から p.670 へ続く(補間対象軸番号2以降が p.670)。ステップ(3211)の FB 回路は原本 p.670。
- 図中コメント: FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D = U1\G31500.1「R:同期用フラグ(ダイレクト)」(立上り接点)，G_bInputG_bInputSpeedPositionSwitchingAbsSetReq = X51「速度・位置切換え(ABS)設定指令」，bSetPositioningData5_bEN「No5実行命令」
- X51(速度・位置切換え(ABS)設定指令)の a接点は，Da.8 指令速度の2つ目の DMOV(K6000000)と，Da.6 位置決めアドレスの2つ目の DMOV(K36000000)の直前にのみ直列に入る(母線側の分岐点は同期用フラグ接点の直後)。
- 出力側 o_bENO / o_bOK / o_bErr / o_uErrId は原本では右母線まで線が延びているのみで，ラベルは接続されていない。
- ニモニックの MPS/MPP および CALL 行は原本ラダー図からの書き起こし表記(原本はラダー図のみでニモニック表示なし)。

#### No.6位置決めデータ設定プログラム (13.3 / 原本 p.671-672)

```
// [Title]No.6位置決めデータ設定プログラム
// <位置決め識別子>
//   運転パターン：位置決め終了
//   制御方式：1軸の直線制御(INC)
//   加速時間No.：1，減速時間No.：2
(3522) LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      // U1\G31500.1 R:同期用フラグ(ダイレクト)
       MOV   K0  M_FX5SSC_SetPositioningData_01A_6.pb_uOpePattern            // Da.1：運転パターン
       MOV   H2  M_FX5SSC_SetPositioningData_01A_6.pb_uCtrlSys                 // Da.2：制御方式
       MOV   K1  M_FX5SSC_SetPositioningData_01A_6.pb_uAccTimeNo               // Da.3：加速時間No.
       MOV   K2  M_FX5SSC_SetPositioningData_01A_6.pb_uDecTimeNo               // Da.4：減速時間No.
       MOV   K0  M_FX5SSC_SetPositioningData_01A_6.pb_uMcode                   // Da.10：Mコード
       MOV   K300  M_FX5SSC_SetPositioningData_01A_6.pb_uDwellTime            // Da.9：ドウェルタイム
       DMOV  K9000  M_FX5SSC_SetPositioningData_01A_6.pb_udCmdSpd             // Da.8：指令速度
       MPS
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   // X51 速度・位置切換え(ABS)設定指令
       DMOV  K1800000  M_FX5SSC_SetPositioningData_01A_6.pb_udCmdSpd             // Da.8：指令速度
       MPP
       DMOV  K50000  M_FX5SSC_SetPositioningData_01A_6.pb_dPositAdr            // Da.6：位置決めアドレス
       MPS
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   // X51 速度・位置切換え(ABS)設定指令
       DMOV  K18000000  M_FX5SSC_SetPositioningData_01A_6.pb_dPositAdr            // Da.6：位置決めアドレス
       MPP
       DMOV  K0  M_FX5SSC_SetPositioningData_01A_6.pb_dArcAdr                  // Da.7：円弧アドレス
       MOV   K0  M_FX5SSC_SetPositioningData_01A_6.pb_uInterpolationAxisNo1    // Da.20：補間対象軸番号1
       MOV   K0  M_FX5SSC_SetPositioningData_01A_6.pb_uInterpolationAxisNo2    // Da.21：補間対象軸番号2     (原本 p.672)
       MOV   K0  M_FX5SSC_SetPositioningData_01A_6.pb_uInterpolationAxisNo3    // Da.22：補間対象軸番号3
       SET   bSetPositioningData6_bEN              // No6実行命令

(3715) LD    bSetPositioningData6_bEN              // No6実行命令
       // FB呼出し: M_FX5SSC_SetPositioningData_01A_6 (M+FX5SSC_SetPositioningData_01A) Positioning data setting FB
       //   入力  B: i_bEN         ← (上記接点)      実行指令
       //   入力  DUT: i_stModule  ← FX5SSC_1        ユニットラベル
       //   入力  UW: i_uAxis      ← K1              対象軸
       //   入力  UW: i_uDataNo    ← K6              位置決めデータNo.
       //   出力  o_bENO :B   実行状態    (接続先ラベルなし)
       //   出力  o_bOK :B    正常完了    (接続先ラベルなし)
       //   出力  o_bErr :B   異常完了    (接続先ラベルなし)
       //   出力  o_uErrId :UW エラーコード (接続先ラベルなし)
       //   FB内部の公開変数(FBボックス下部の表示): pb_uOpePattern, pb_uCtrlSys, pb_uAccTimeNo, pb_uDecTimeNo, pb_uMcode, pb_uDwellTime, pb_udCmdSpd, pb_dPositAdr, pb_dArcAdr, pb_uInterpolationAxisNo1, pb_uInterpolationAxisNo2, pb_uInterpolationAxisNo3
       CALL  M_FX5SSC_SetPositioningData_01A_6  (i_bEN, FX5SSC_1, K1, K6)
```
- ステップ(3522)の回路は原本 p.671 から p.672 へ続く(補間対象軸番号2以降が p.672)。ステップ(3715)の FB 回路は原本 p.672。
- 図中コメント: FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D = U1\G31500.1「R:同期用フラグ(ダイレクト)」(立上り接点)，G_bInputG_bInputSpeedPositionSwitchingAbsSetReq = X51「速度・位置切換え(ABS)設定指令」，bSetPositioningData6_bEN「No6実行命令」
- X51(速度・位置切換え(ABS)設定指令)の a接点は，Da.8 指令速度の2つ目の DMOV(K1800000)と，Da.6 位置決めアドレスの2つ目の DMOV(K18000000)の直前にのみ直列に入る(母線側の分岐点は同期用フラグ接点の直後)。
- 出力側 o_bENO / o_bOK / o_bErr / o_uErrId は原本では右母線まで線が延びているのみで，ラベルは接続されていない。
- ニモニックの MPS/MPP および CALL 行は原本ラダー図からの書き起こし表記(原本はラダー図のみでニモニック表示なし)。

#### No.10位置決めデータ設定プログラム (13.3 / 原本 p.673-674)

```
// [Title]No.10位置決めデータ設定プログラム
// <位置決め識別子>
//   運転パターン：連続位置決め制御
//   制御方式：軸1の直線制御(INC)
//   加速時間No：1，　減速時間No：2
(4026) LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      // U1\G31500.1 R:同期用フラグ(ダイレクト)
       MOV   K1  M_FX5SSC_SetPositioningData_01A_10.pb_uOpePattern            // Da.1：運転パターン
       MOV   H2  M_FX5SSC_SetPositioningData_01A_10.pb_uCtrlSys                 // Da.2：制御方式
       MOV   K1  M_FX5SSC_SetPositioningData_01A_10.pb_uAccTimeNo               // Da.3：加速時間No.
       MOV   K2  M_FX5SSC_SetPositioningData_01A_10.pb_uDecTimeNo               // Da.4：減速時間No.
       MOV   K0  M_FX5SSC_SetPositioningData_01A_10.pb_uMcode                   // Da.10：Mコード
       MOV   K300  M_FX5SSC_SetPositioningData_01A_10.pb_uDwellTime            // Da.9：ドウェルタイム
       DMOV  K9000  M_FX5SSC_SetPositioningData_01A_10.pb_udCmdSpd             // Da.8：指令速度
       MPS
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   // X51 速度・位置切換え(ABS)設定指令
       DMOV  K3600000  M_FX5SSC_SetPositioningData_01A_10.pb_udCmdSpd             // Da.8：指令速度
       MPP
       DMOV  K50000  M_FX5SSC_SetPositioningData_01A_10.pb_dPositAdr            // Da.6：位置決めアドレス
       MPS
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   // X51 速度・位置切換え(ABS)設定指令
       DMOV  K36000000  M_FX5SSC_SetPositioningData_01A_10.pb_dPositAdr            // Da.6：位置決めアドレス
       MPP
       DMOV  K0  M_FX5SSC_SetPositioningData_01A_10.pb_dArcAdr                  // Da.7：円弧アドレス
       MOV   K0  M_FX5SSC_SetPositioningData_01A_10.pb_uInterpolationAxisNo1    // Da.20：補間対象軸番号1
       MOV   K0  M_FX5SSC_SetPositioningData_01A_10.pb_uInterpolationAxisNo2    // Da.21：補間対象軸番号2     (原本 p.674)
       MOV   K0  M_FX5SSC_SetPositioningData_01A_10.pb_uInterpolationAxisNo3    // Da.22：補間対象軸番号3
       SET   bSetPositioningData10_bEN              // No10実行命令

(4221) LD    bSetPositioningData10_bEN              // No10実行命令
       // FB呼出し: M_FX5SSC_SetPositioningData_01A_10 (M+FX5SSC_SetPositioningData_01A) Positioning data setting FB
       //   入力  B: i_bEN         ← (上記接点)      実行指令
       //   入力  DUT: i_stModule  ← FX5SSC_1        ユニットラベル
       //   入力  UW: i_uAxis      ← K1              対象軸
       //   入力  UW: i_uDataNo    ← K10              位置決めデータNo.
       //   出力  o_bENO :B   実行状態    (接続先ラベルなし)
       //   出力  o_bOK :B    正常完了    (接続先ラベルなし)
       //   出力  o_bErr :B   異常完了    (接続先ラベルなし)
       //   出力  o_uErrId :UW エラーコード (接続先ラベルなし)
       //   FB内部の公開変数(FBボックス下部の表示): pb_uOpePattern, pb_uCtrlSys, pb_uAccTimeNo, pb_uDecTimeNo, pb_uMcode, pb_uDwellTime, pb_udCmdSpd, pb_dPositAdr, pb_dArcAdr, pb_uInterpolationAxisNo1, pb_uInterpolationAxisNo2, pb_uInterpolationAxisNo3
       CALL  M_FX5SSC_SetPositioningData_01A_10  (i_bEN, FX5SSC_1, K1, K10)
```
- ステップ(4026)の回路は原本 p.673 から p.674 へ続く(補間対象軸番号2以降が p.674)。ステップ(4221)の FB 回路は原本 p.674。
- 図中コメント: FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D = U1\G31500.1「R:同期用フラグ(ダイレクト)」(立上り接点)，G_bInputG_bInputSpeedPositionSwitchingAbsSetReq = X51「速度・位置切換え(ABS)設定指令」，bSetPositioningData10_bEN「No10実行命令」
- X51(速度・位置切換え(ABS)設定指令)の a接点は，Da.8 指令速度の2つ目の DMOV(K3600000)と，Da.6 位置決めアドレスの2つ目の DMOV(K36000000)の直前にのみ直列に入る(母線側の分岐点は同期用フラグ接点の直後)。
- 出力側 o_bENO / o_bOK / o_bErr / o_uErrId は原本では右母線まで線が延びているのみで，ラベルは接続されていない。
- ニモニックの MPS/MPP および CALL 行は原本ラダー図からの書き起こし表記(原本はラダー図のみでニモニック表示なし)。

#### No.11位置決めデータ設定プログラム (13.3 / 原本 p.675-676)

```
// [Title]No.11位置決めデータ設定プログラム
// <位置決め識別子>
//   運転パターン：位置決め終了
//   制御方式：軸1の直線制御(INC)
//   加速時間No：1，　減速時間No：2
(4532) LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      // U1\G31500.1 R:同期用フラグ(ダイレクト)
       MOV   K0  M_FX5SSC_SetPositioningData_01A_11.pb_uOpePattern            // Da.1：運転パターン
       MOV   H2  M_FX5SSC_SetPositioningData_01A_11.pb_uCtrlSys                 // Da.2：制御方式
       MOV   K1  M_FX5SSC_SetPositioningData_01A_11.pb_uAccTimeNo               // Da.3：加速時間No.
       MOV   K2  M_FX5SSC_SetPositioningData_01A_11.pb_uDecTimeNo               // Da.4：減速時間No.
       MOV   K0  M_FX5SSC_SetPositioningData_01A_11.pb_uMcode                   // Da.10：Mコード
       MOV   K300  M_FX5SSC_SetPositioningData_01A_11.pb_uDwellTime            // Da.9：ドウェルタイム
       DMOV  K18000  M_FX5SSC_SetPositioningData_01A_11.pb_udCmdSpd             // Da.8：指令速度
       MPS
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   // X51 速度・位置切換え(ABS)設定指令
       DMOV  K3600000  M_FX5SSC_SetPositioningData_01A_11.pb_udCmdSpd             // Da.8：指令速度
       MPP
       DMOV  K-100000  M_FX5SSC_SetPositioningData_01A_11.pb_dPositAdr            // Da.6：位置決めアドレス
       MPS
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   // X51 速度・位置切換え(ABS)設定指令
       DMOV  K-36000000  M_FX5SSC_SetPositioningData_01A_11.pb_dPositAdr            // Da.6：位置決めアドレス
       MPP
       DMOV  K0  M_FX5SSC_SetPositioningData_01A_11.pb_dArcAdr                  // Da.7：円弧アドレス
       MOV   K0  M_FX5SSC_SetPositioningData_01A_11.pb_uInterpolationAxisNo1    // Da.20：補間対象軸番号1
       MOV   K0  M_FX5SSC_SetPositioningData_01A_11.pb_uInterpolationAxisNo2    // Da.21：補間対象軸番号2     (原本 p.676)
       MOV   K0  M_FX5SSC_SetPositioningData_01A_11.pb_uInterpolationAxisNo3    // Da.22：補間対象軸番号3
       SET   bSetPositioningData11_bEN              // No11実行命令

(4727) LD    bSetPositioningData11_bEN              // No11実行命令
       // FB呼出し: M_FX5SSC_SetPositioningData_01A_11 (M+FX5SSC_SetPositioningData_01A) Positioning data setting FB
       //   入力  B: i_bEN         ← (上記接点)      実行指令
       //   入力  DUT: i_stModule  ← FX5SSC_1        ユニットラベル
       //   入力  UW: i_uAxis      ← K1              対象軸
       //   入力  UW: i_uDataNo    ← K11              位置決めデータNo.
       //   出力  o_bENO :B   実行状態    (接続先ラベルなし)
       //   出力  o_bOK :B    正常完了    (接続先ラベルなし)
       //   出力  o_bErr :B   異常完了    (接続先ラベルなし)
       //   出力  o_uErrId :UW エラーコード (接続先ラベルなし)
       //   FB内部の公開変数(FBボックス下部の表示): pb_uOpePattern, pb_uCtrlSys, pb_uAccTimeNo, pb_uDecTimeNo, pb_uMcode, pb_uDwellTime, pb_udCmdSpd, pb_dPositAdr, pb_dArcAdr, pb_uInterpolationAxisNo1, pb_uInterpolationAxisNo2, pb_uInterpolationAxisNo3
       CALL  M_FX5SSC_SetPositioningData_01A_11  (i_bEN, FX5SSC_1, K1, K11)
```
- ステップ(4532)の回路は原本 p.675 から p.676 へ続く(補間対象軸番号2以降が p.676)。ステップ(4727)の FB 回路は原本 p.676。
- 図中コメント: FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D = U1\G31500.1「R:同期用フラグ(ダイレクト)」(立上り接点)，G_bInputG_bInputSpeedPositionSwitchingAbsSetReq = X51「速度・位置切換え(ABS)設定指令」，bSetPositioningData11_bEN「No11実行命令」
- X51(速度・位置切換え(ABS)設定指令)の a接点は，Da.8 指令速度の2つ目の DMOV(K3600000)と，Da.6 位置決めアドレスの2つ目の DMOV(K-36000000)の直前にのみ直列に入る(母線側の分岐点は同期用フラグ接点の直後)。
- 出力側 o_bENO / o_bOK / o_bErr / o_uErrId は原本では右母線まで線が延びているのみで，ラベルは接続されていない。
- ニモニックの MPS/MPP および CALL 行は原本ラダー図からの書き起こし表記(原本はラダー図のみでニモニック表示なし)。

#### No.15位置決めデータ設定プログラム (13.3 / 原本 p.677-678)

```
// [Title]No.15位置決めデータ設定プログラム
// <位置決め識別子>
//   運転パターン：位置決め終了
//   制御方式：軸1の直線制御(INC)
//   加速時間No:1，　減速時間No:2
(5038) LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      // U1\G31500.1 R:同期用フラグ(ダイレクト)
       MOV   K0  M_FX5SSC_SetPositioningData_01A_15.pb_uOpePattern            // Da.1：運転パターン
       MOV   H2  M_FX5SSC_SetPositioningData_01A_15.pb_uCtrlSys                 // Da.2：制御方式
       MOV   K1  M_FX5SSC_SetPositioningData_01A_15.pb_uAccTimeNo               // Da.3：加速時間No.
       MOV   K2  M_FX5SSC_SetPositioningData_01A_15.pb_uDecTimeNo               // Da.4：減速時間No.
       MOV   K0  M_FX5SSC_SetPositioningData_01A_15.pb_uMcode                   // Da.10：Mコード
       MOV   K0  M_FX5SSC_SetPositioningData_01A_15.pb_uDwellTime            // Da.9：ドウェルタイム
       DMOV  K9000  M_FX5SSC_SetPositioningData_01A_15.pb_udCmdSpd             // Da.8：指令速度
       MPS
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   // X51 速度・位置切換え(ABS)設定指令
       DMOV  K1800000  M_FX5SSC_SetPositioningData_01A_15.pb_udCmdSpd             // Da.8：指令速度
       MPP
       DMOV  K50000  M_FX5SSC_SetPositioningData_01A_15.pb_dPositAdr            // Da.6：位置決めアドレス
       MPS
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   // X51 速度・位置切換え(ABS)設定指令
       DMOV  K18000000  M_FX5SSC_SetPositioningData_01A_15.pb_dPositAdr            // Da.6：位置決めアドレス
       MPP
       DMOV  K0  M_FX5SSC_SetPositioningData_01A_15.pb_dArcAdr                  // Da.7：円弧アドレス
       MOV   K0  M_FX5SSC_SetPositioningData_01A_15.pb_uInterpolationAxisNo1    // Da.20：補間対象軸番号1
       MOV   K0  M_FX5SSC_SetPositioningData_01A_15.pb_uInterpolationAxisNo2    // Da.21：補間対象軸番号2     (原本 p.678)
       MOV   K0  M_FX5SSC_SetPositioningData_01A_15.pb_uInterpolationAxisNo3    // Da.22：補間対象軸番号3
       SET   bSetPositioningData15_bEN              // No15実行命令

(5229) LD    bSetPositioningData15_bEN              // No15実行命令
       // FB呼出し: M_FX5SSC_SetPositioningData_01A_15 (M+FX5SSC_SetPositioningData_01A) Positioning data setting FB
       //   入力  B: i_bEN         ← (上記接点)      実行指令
       //   入力  DUT: i_stModule  ← FX5SSC_1        ユニットラベル
       //   入力  UW: i_uAxis      ← K1              対象軸
       //   入力  UW: i_uDataNo    ← K15              位置決めデータNo.
       //   出力  o_bENO :B   実行状態    (接続先ラベルなし)
       //   出力  o_bOK :B    正常完了    (接続先ラベルなし)
       //   出力  o_bErr :B   異常完了    (接続先ラベルなし)
       //   出力  o_uErrId :UW エラーコード (接続先ラベルなし)
       //   FB内部の公開変数(FBボックス下部の表示): pb_uOpePattern, pb_uCtrlSys, pb_uAccTimeNo, pb_uDecTimeNo, pb_uMcode, pb_uDwellTime, pb_udCmdSpd, pb_dPositAdr, pb_dArcAdr, pb_uInterpolationAxisNo1, pb_uInterpolationAxisNo2, pb_uInterpolationAxisNo3
       CALL  M_FX5SSC_SetPositioningData_01A_15  (i_bEN, FX5SSC_1, K1, K15)
```
- ステップ(5038)の回路は原本 p.677 から p.678 へ続く(補間対象軸番号2以降が p.678)。ステップ(5229)の FB 回路は原本 p.678。
- 図中コメント: FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D = U1\G31500.1「R:同期用フラグ(ダイレクト)」(立上り接点)，G_bInputG_bInputSpeedPositionSwitchingAbsSetReq = X51「速度・位置切換え(ABS)設定指令」，bSetPositioningData15_bEN「No15実行命令」
- X51(速度・位置切換え(ABS)設定指令)の a接点は，Da.8 指令速度の2つ目の DMOV(K1800000)と，Da.6 位置決めアドレスの2つ目の DMOV(K18000000)の直前にのみ直列に入る(母線側の分岐点は同期用フラグ接点の直後)。
- 出力側 o_bENO / o_bOK / o_bErr / o_uErrId は原本では右母線まで線が延びているのみで，ラベルは接続されていない。
- ニモニックの MPS/MPP および CALL 行は原本ラダー図からの書き起こし表記(原本はラダー図のみでニモニック表示なし)。

### ブロック始動データ設定プログラム (13.3 / 原本 p.679)

エンジニアリングツールの"ブロック始動データ"にて設定する場合，本プログラムは不要です。
下記のようにローカルラベルを設定してください。

- ローカルラベル定義(原本 p.679 の画面図より)

| No. | ラベル名 | データ型 | クラス | Japanese/日本語(表示対象) |
|---|---|---|---|---|
| 1 | uBlockData | ワード[符号なし]/ビット列[16ビット](0..4) | VAR | ブロック始動データ(形態、始動データNo) |
| 2 | uBlockInstData | ワード[符号なし]/ビット列[16ビット](0..4) | VAR | ブロック始動データ(特殊始動命令) |
| 3 | (空欄) | (空欄) | (空欄) | (空欄) |

```
// [Title]ブロック始動データ設定プログラム
//   ブロック始動順序： 位置決めNo1→No2→No5→No10→No15
(5540) LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      // U1\G31500.1 R:同期用フラグ(ダイレクト)
       MOVP  H8001  uBlockData[0]                 // ブロック始動データ(形態、始動データNo)
       MOVP  H8002  uBlockData[1]                 // ブロック始動データ(形態、始動データNo)
       MOVP  H8005  uBlockData[2]                 // ブロック始動データ(形態、始動データNo)
       MOVP  H800A  uBlockData[3]                 // ブロック始動データ(形態、始動データNo)
       MOVP  H0F    uBlockData[4]                 // ブロック始動データ(形態、始動データNo)
       TOP   H1  K22000  uBlockData[0]  K5        // ブロック始動データ(形態、始動データ…)

(5647) LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      // U1\G31500.1 R:同期用フラグ(ダイレクト)
       MOVP  H0  uBlockInstData[0]                // ブロック始動データ(特殊始動命令)
       MOVP  H0  uBlockInstData[1]                // ブロック始動データ(特殊始動命令)
       MOVP  H0  uBlockInstData[2]                // ブロック始動データ(特殊始動命令)
       MOVP  H0  uBlockInstData[3]                // ブロック始動データ(特殊始動命令)
       MOVP  H0  uBlockInstData[4]                // ブロック始動データ(特殊始動命令)
       TOP   H1  K22050  uBlockInstData[0]  K5    // ブロック始動データ(特殊始動命令)
```

- 図中コメント: FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D = U1\G31500.1「R:同期用フラグ(ダイレクト)」(立上り接点，2回路とも)
- 1つ目の TOP の第3オペランド uBlockData[0] のコメントは原本の表示上「ブロック始動データ(形態、始動データ…」で途切れている。

### 原点復帰要求OFFプログラム (13.3 / 原本 p.680)

エンジニアリングツールの"原点復帰詳細パラメータ"にて"[Pr.55]原点復帰未完時操作設定"を「1: 位置決め制御を実行する」に設定した場合，本プログラムは不要です。
下記のようにローカルラベルを設定してください。

- ローカルラベル定義(原本 p.680 の画面図より)

| No. | ラベル名 | データ型 | クラス | Japanese/日本語(表示対象) |
|---|---|---|---|---|
| 1 | bOPRReqFlagOffReq_P | ビット | VAR | 原点復帰要求OFF指令パルス |
| 2 | bOPRReqFlagOffReq_H | ビット | VAR | 原点復帰要求OFF指令記憶 |
| 3 | bOPRReqFlagOffReq | ビット | VAR | 原点復帰要求OFF指令 |
| 4 | (空欄) | (空欄) | (空欄) | (空欄) |

```
// [Title]原点復帰要求OFFプログラム
// ■始動条件 X2(原点復帰要求OFF信号)
(5677) LD    G_bInputOPRReqFlagOffReq                          // X2 原点復帰要求OFF指令
       PLS   bOPRReqFlagOffReq_P                               // 原点復帰要求OFF指令パルス

(5737) LD    bOPRReqFlagOffReq_P                               // 原点復帰要求OFF指令パルス
       ANI   FX5SSC_1.stnAxCtrl2_D[0].uPositioningStart_D.0    // U1\G30104.0 RW:位置決め始動(ダイレクト)
       ANI   FX5SSC_1.stnAxMntr_D[0].uStatus_D.E               // U1\G2417.E R:ステータス(ダイレクト)
       SET   bOPRReqFlagOffReq_H                               // 原点復帰要求OFF指令記憶

(5747) LD    bOPRReqFlagOffReq_H                               // 原点復帰要求OFF指令記憶
       MPS
       AND   FX5SSC_1.stnAxMntr_D[0].uStatus_D.3               // U1\G2417.3 R:ステータス(ダイレクト)
       SET   bOPRReqFlagOffReq                                 // 原点復帰要求OFF指令
       MPP
       RST   bOPRReqFlagOffReq_H                               // 原点復帰要求OFF指令記憶

(5758) LD    bOPRReqFlagOffReq                                 // 原点復帰要求OFF指令
       MOVP  K1  FX5SSC_1.stnAxCtrl1_D[0].uClearHomingRequestFlag_D   // U1\G4321 RW:原点復帰要求フラグOFF要求(ダイレクト)
       AND=_U  K0  FX5SSC_1.stnAxCtrl1_D[0].uClearHomingRequestFlag_D // U1\G4321 RW:原点復帰要求フラグOFF要求(ダイレクト)
       RST   bOPRReqFlagOffReq                                 // 原点復帰要求OFF指令
```

- 図中コメント: G_bInputOPRReqFlagOffReq = X2「原点復帰要求OFF指令」，FX5SSC_1.stnAxCtrl2_D[0].uPositioningStart_D.0 = U1\G30104.0「RW:位置決め始動(ダイレクト)」(b接点)，FX5SSC_1.stnAxMntr_D[0].uStatus_D.E = U1\G2417.E「R:ステータス(ダイレクト)」(b接点)，FX5SSC_1.stnAxMntr_D[0].uStatus_D.3 = U1\G2417.3「R:ステータス(ダイレクト)」(a接点)，FX5SSC_1.stnAxCtrl1_D[0].uClearHomingRequestFlag_D = U1\G4321「RW:原点復帰要求フラグOFF要求(ダイレクト)」
- ステップ(5747): RST bOPRReqFlagOffReq_H の分岐は bOPRReqFlagOffReq_H 接点の直後(U1\G2417.3 接点の手前)から出ている。
- ステップ(5758): =_U 比較(K0 と U1\G4321)の分岐は bOPRReqFlagOffReq 接点の直後から出ている。

### 外部指令機能有効設定プログラム (13.3 / 原本 p.680)

```
// [Title]外部指令有効プログラム
// ■始動条件 X3(外部指令有効信号)
(5774) LD    G_bInputExternalCommandValidReq                   // X3 外部指令有効指令
       MOVP  K1  FX5SSC_1.stnAxCtrl1_D[0].uExternalCommandValid_D     // U1\G4305 RW:外部指令有効(ダイレクト)

(5831) LD    G_bInputExternalCommandInvalidReq                 // X4 外部指令無効指令
       MOVP  K0  FX5SSC_1.stnAxCtrl1_D[0].uExternalCommandValid_D     // U1\G4305 RW:外部指令有効(ダイレクト)
```

- 図中コメント: G_bInputExternalCommandValidReq = X3「外部指令有効指令」，G_bInputExternalCommandInvalidReq = X4「外部指令無効指令」，FX5SSC_1.stnAxCtrl1_D[0].uExternalCommandValid_D = U1\G4305「RW:外部指令有効(ダイレクト)」
- 原本の見出しは「外部指令機能有効設定プログラム」，ラダーの Title 行は「外部指令有効プログラム」。

### シーケンサレディ信号ONプログラム (13.3 / 原本 p.681)

下記のようにローカルラベルを設定してください。

- ローカルラベル定義(原本 p.681 の画面図より)

| No. | ラベル名 | データ型 | クラス | Japanese/日本語(表示対象) |
|---|---|---|---|---|
| 1 | bBasicParamSetComp | ビット | VAR | 基本パラメータ1設定完了 |
| 2 | bDetailedParamSetComp | ビット | VAR | 詳細パラメータ2設定完了 |
| 3 | bOPRParamSetComp | ビット | VAR | 原点復帰基本パラメータ設定完了 |
| 4 | (空欄) | (空欄) | (空欄) | (空欄) |

```
// [Title]シーケンサレディONプログラム
(5839) LD    FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      // U1\G31500.1 R:同期用フラグ(ダイレクト)
       AND   bBasicParamSetComp                                // 基本パラメータ1設定完了
       AND   bDetailedParamSetComp                             // 詳細パラメータ2設定完了
       AND   bOPRParamSetComp                                  // 原点復帰基本パラメータ設定完了
       ANI   G_bInitializeParameterReq                         // パラメータ初期化指令
       ANI   G_bWriteFlashReq                                  // フラッシュROM書込み指令
       OUT   FX5SSC_1.stSysCtrl_D.bPLC_Ready_D                 // U1\G5950.0 RW:シーケンサレディ(ダイレクト)
```

- 図中コメント: FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D = U1\G31500.1「R:同期用フラグ(ダイレクト)」，bBasicParamSetComp「基本パラメータ1設定完了」，bDetailedParamSetComp「詳細パラメータ2設定完了」，bOPRParamSetComp「原点復帰基本パラメータ設定完了」，G_bInitializeParameterReq「パラメータ初期化指令」(b接点)，G_bWriteFlashReq「フラッシュROM書込み指令」(b接点)，FX5SSC_1.stSysCtrl_D.bPLC_Ready_D = U1\G5950.0「RW:シーケンサレディ(ダイレクト)」

### 全軸サーボONプログラム (13.3 / 原本 p.681)

```
// [Title]全軸サーボONプログラム
//   ＊サーボネットワーク構成パラメータ(IPアドレス)をフラッシュROM書き込みにて有効
(5885) LD    G_bAllAxisServoOnReq                              // X52 全軸サーボON指令
       AND   FX5SSC_1.stSysCtrl_D.bPLC_Ready_D                 // U1\G5950.0 RW:シーケンサレディ(ダイレクト)
       AND   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      // U1\G31500.1 R:同期用フラグ(ダイレクト)
       OUT   FX5SSC_1.stSysCtrl_D.bAllAxisServoOn_D            // U1\G5951.0 RW:全軸サーボON(ダイレクト)
```

- 図中コメント: G_bAllAxisServoOnReq = X52「全軸サーボON指令」，FX5SSC_1.stSysCtrl_D.bPLC_Ready_D = U1\G5950.0「RW:シーケンサレディ(ダイレクト)」，FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D = U1\G31500.1「R:同期用フラグ(ダイレクト)」，FX5SSC_1.stSysCtrl_D.bAllAxisServoOn_D = U1\G5951.0「RW:全軸サーボON(ダイレクト)」

#### 位置決め始動番号設定プログラム (13.3 / 原本 p.682)

下記のようにローカルラベルを設定してください。

| No. | ラベル名 | データ型 | クラス | Japanese/日本語(表示対象) |
|---|---|---|---|---|
| 1 | uPositioningStartNo | ワード[符号付き] | VAR | 位置決め始動番号 |
| 2 | bFastOPRStartReq | ビット | VAR | 高速原点復帰指令 |
| 3 | bFastOPRStartReq_H | ビット | VAR | 高速原点復帰指令記憶 |
| 4 | bPositioningStartReq | ビット | VAR | 位置決め始動指令 |
| 5 | udMovementAmount | ダブルワード[符号なし]/ビット列[32ビット] | VAR | 速度・位置切換え制御移動量 |
| 6 | udSpeed | ダブルワード[符号付き] | VAR | 位置・速度切換え制御速度 |
| 7 | bInputSpeedPositionSwitching | ビット | VAR | 速度・位置切換え指令 |

(GX Works3 ラダー図からの書き起こし。左端の数字はステップNo.。接点のグローバルラベルに割り付けられたデバイス(X5等)と原本表記の「U1¥G」(= GX Works3 の `U1\G`)は括弧内に記載。`//` 以降はラダー上のコメント。ラベル一覧表の末尾の空行(原本 No.8 等)は省略。FB(ファンクションブロック)は原本にニモニックが示されていないため，`FBCALL <インスタンス名>` の後に各ピンの接続を `ピン名 := 入力` / `ピン名 => 出力先` で記載。)

##### ■機械原点復帰 (13.3 / 原本 p.682)

```
// [Title]機械原点復帰
// ■始動条件 X5(機械原点復帰指令:K9001)→位置決め始動プログラム
(0)
LD   G_bInputOPRStartReq (X5)                                   // 機械原点復帰指令
MOVP K9001 uPositioningStartNo                                  // 位置決め始動番号
```

##### ■高速原点復帰 (13.3 / 原本 p.682)

```
// [Title]高速原点復帰
// ■始動条件 X6(高速原点復帰指令:K9002)→位置決め始動プログラム
(68)
LD   G_bInputFastOPRStartReq (X6)                               // 高速原点復帰指令
MPS
ANI  FX5SSC_1.stnAxMntr_D[0].uStatus_D.3 (U1\G2417.3)           // R:ステータス(ダイレクト)
SET  bFastOPRStartReq                                           // 高速原点復帰指令
MPP
MOVP K9002 uPositioningStartNo                                  // 位置決め始動番号
SET  bFastOPRStartReq_H                                         // 高速原点復帰指令記憶
```

- ステップ(68): uStatus_D.3 はb接点。SET bFastOPRStartReq のみ uStatus_D.3 のb接点と直列。MOVP K9002 と SET bFastOPRStartReq_H は X6 の直後から分岐した並列出力(uStatus_D.3 を経由しない)。

##### ■位置決めデータNo.1による位置決め (13.3 / 原本 p.682)

```
// [Title]位置決めデータNo.1による位置決め
// ■始動条件 X7(位置決め始動指令:K1)→位置決め始動プログラム
(145)
LD   G_bInputSetStartPositioningNoReq (X7)                      // 位置決め始動指令
MOVP K1 uPositioningStartNo                                     // 位置決め始動番号
```

##### ■速度・位置切換え制御(位置決めデータNo.2) (13.3 / 原本 p.682)

ABSモードの場合，変更後の移動量書込みは不要です。

```
// [Title]速度・位置切換え制御(位置決めデータNo.2)
// ■始動条件 外部指令有効プログラム始動→X10(速度・位置切換え運転指令:K2)→位置決め始動プログラム ＊速度・位置切換えは軸1ドグ信号 ＊速度制御停止は軸停止始動
(223)
LD   G_bInputSpeedPositionSwitchingReq (X10)                    // 速度・位置切換え運転指令
MOVP K2 uPositioningStartNo                                     // 位置決め始動番号

(361)
LD   G_bInputSpeedPositionSwitchingEnableReq (X11)              // 速度・位置切換え許可指令
MOVP K1 FX5SSC_1.stnAxCtrl1_D[0].uEnableVP_Switching_D (U1\G4328)   // RW:速度・位置切換え許可フラグ(ダイレクト)

(369)
LD   G_bInputSpeedPositionSwitchingDisableReq (X12)             // 速度・位置切換え禁止指令
MOVP K0 FX5SSC_1.stnAxCtrl1_D[0].uEnableVP_Switching_D (U1\G4328)   // RW:速度・位置切換え許可フラグ(ダイレクト)

(377)
LD   G_bInputChangeSpeedPositionSwitchingMovementAmount (X13)   // 移動量変更指令
DMOVP udMovementAmount FX5SSC_1.stnAxCtrl1_D[0].udVP_NewMovementAmount_D (U1\G4326)   // 速度・位置切換え制御移動量 → RW:速度・位置切換え制御移動量変更レジスタ(ダイレクト)
```

##### ■位置・速度切換え制御(位置決めデータNo.3) (13.3 / 原本 p.683)

```
// [Title]位置・速度切換え制御(位置決めデータNo.3)
// ■始動条件 外部指令有効プログラム始動→X10(位置・速度切換え運転指令:K3)→位置決め始動プログラム ＊速度・位置切換えは軸1ドグ信号 ＊速度制御停止は軸停止始動
(385)
LD   G_bInputPositionSpeedSwitchingReq (X42)                    // 位置・速度切換え運転指令
MOVP K3 uPositioningStartNo                                     // 位置決め始動番号

(523)
LD   G_bInputPositionSpeedSwitchingEnableReq (X43)              // 位置・速度切換え許可指令
MOVP K1 FX5SSC_1.stnAxCtrl1_D[0].uEnablePV_Switching_D (U1\G4332)   // RW:位置・速度切換え許可フラグ(ダイレクト)

(531)
LD   G_bInputPositionSpeedSwitchingDisableReq (X44)             // 位置・速度切換え禁止指令
MOVP K0 FX5SSC_1.stnAxCtrl1_D[0].uEnablePV_Switching_D (U1\G4332)   // RW:位置・速度切換え許可フラグ(ダイレクト)

(539)
LD   G_bInputChangePositionSpeedSwitchingSpeedReq (X45)         // 速度変更指令
DMOVP udSpeed FX5SSC_1.stnAxCtrl1_D[0].udPV_NewSpeed_D (U1\G4330)   // 位置・速度切換え制御速度 → RW:位置・速度切換え制御速度変更レジスタ(ダイレクト)
```

- ステートメントの「X10(位置・速度切換え運転指令:K3)」「＊速度・位置切換えは軸1ドグ信号」は原本の記載のまま(ステップ(385)の接点は X42)。

##### ■高度な位置決め制御 (13.3 / 原本 p.683)

```
// [Title]高度な位置決め制御
// ブロック始動順序: 位置決めNo1→No2→No5→No10→No15
// ■起動条件 X14(高度な位置決め制御始動指令:K7000)→位置決め始動プログラム:
(547)
LD   G_bInputStartAdvancedPositioningReq (X14)                  // 高度な位置決め制御始動指令
MOVP K7000 uPositioningStartNo                                  // 位置決め始動番号
```

##### ■高速原点復帰指令，高速原点復帰指令記憶のOFF (13.3 / 原本 p.683)

高速原点復帰を使用しない場合は不要です。

```
// [Title]高速原点復帰指令、高速原点復帰指令記憶のOFF
// 高速原点復帰をしない場合は不要
// ■始動条件 X5(機械原点復帰指令)
(670)
LD   G_bInputOPRStartReq (X5)                                   // 機械原点復帰指令
OR   G_bInputSetStartPositioningNoReq (X7)                      // 位置決め始動指令
OR   G_bInputSpeedPositionSwitchingReq (X10)                    // 速度・位置切換え運転指令
OR   G_bInputPositionSpeedSwitchingReq (X42)                    // 位置・速度切換え運転指令
OR   G_bInputStartAdvancedPositioningReq (X14)                  // 高度な位置決め制御始動指令
OR   bPositioningStartReq                                       // 位置決め始動指令
RST  bFastOPRStartReq                                           // 高速原点復帰指令
RST  bFastOPRStartReq_H                                         // 高速原点復帰指令記憶
```

- ステップ(670): 6個のa接点の並列(OR)条件で，RST 2命令を並列出力。

#### 位置決め始動プログラム (13.3 / 原本 p.684)

下記のようにローカルラベルを設定してください。

| No. | ラベル名 | データ型 | クラス | Japanese/日本語(表示対象) |
|---|---|---|---|---|
| 1 | uPositioningStartNo | ワード[符号付き] | VAR | 位置決め始動番号 |
| 2 | bFastOPRStartReq | ビット | VAR | 高速原点復帰指令 |
| 3 | bFastOPRStartReq_H | ビット | VAR | 高速原点復帰指令記憶 |
| 4 | bPositioningStartReq | ビット | VAR | 位置決め始動指令 |

```
// [Title]位置決め始動プログラム
// ■始動条件 X15(位置決め始動指令)
(770)
LDP  G_bInputStartPositioningReq (X15)                          // 位置決め始動指令
ANI  G_bDuringJogInchingOperation                               // JOG/インチング運転中フラグ
ANI  G_bDuringMPGOperation                                      // 手動パルサ運転中フラグ
LDI  bFastOPRStartReq                                           // 高速原点復帰指令
LD   bFastOPRStartReq                                           // 高速原点復帰指令
AND  bFastOPRStartReq_H                                         // 高速原点復帰指令記憶
ORB
ANB
SET  bPositioningStartReq                                       // 位置決め始動指令

(840)
LD   bPositioningStartReq                                       // 位置決め始動指令
LD   M_FX5SSC_StartPositioning_01A_1.o_bOK                      // 正常完了
OR   M_FX5SSC_StartPositioning_01A_1.o_bErr                     // 異常完了
OR   G_bInputErrResetReq (X40)                                  // エラーリセット指令
ANB
ANI  FX5SSC_1.stSysMntr2_D.bnBusy_D[0] (U1\G31501.0)            // R:BUSY(1～8軸)(ダイレクト)
RST  bPositioningStartReq                                       // 位置決め始動指令

(854)
LD   bPositioningStartReq                                       // 位置決め始動指令
FBCALL M_FX5SSC_StartPositioning_01A_1                          // (M+FX5SSC_StartPositioning_01A) Positioning start FB
     i_bEN      (B)   := 上記接点(bPositioningStartReq)         // 実行指令
     i_stModule (DUT) := FX5SSC_1                               // ユニットラベル / ユニットラベル
     i_uAxis    (UW)  := K1                                     // 対象軸
     i_uStartNo (UW)  := uPositioningStartNo                    // 位置決め始動番号 / Cd.3:位置決め始動番号
     o_bENO     (B)   => (接続先の記載なし)                     // 実行状態
     o_bOK      (B)   => (接続先の記載なし)                     // 正常完了
     o_bErr     (B)   => (接続先の記載なし)                     // 異常完了
     o_uErrId   (UW)  => (接続先の記載なし)                     // エラーコード
```

- ステップ(770): X15 は立上り検出接点(LDP)。G_bDuringJogInchingOperation，G_bDuringMPGOperation，bFastOPRStartReq(上段)はb接点。bFastOPRStartReq のb接点と，「bFastOPRStartReq(a接点)と bFastOPRStartReq_H(a接点)の直列」とが並列。
- ステップ(840): o_bOK，o_bErr，X40 の3接点が並列(OR)。bnBusy_D[0] はb接点。
- ステップ(854): FBの出力ピンは原本では線が右へ延びているのみで，接続先の記載なし。

#### MコードOFFプログラム (13.3 / 原本 p.685)

```
// [Title]MコードOFF要求プログラム
// ■始動条件 X16(MコードOFF要求)
(1121)
LD   G_bInputMcodeOffReq (X16)                                  // MコードOFF要求
AND  FX5SSC_1.stnAxMntr_D[0].uStatus_D.C (U1\G2417.C)           // R:ステータス(ダイレクト)
MOVP K1 FX5SSC_1.stnAxCtrl1_D[0].uClear_M_Code_D (U1\G4304)     // RW:MコードOFF要求(ダイレクト)
```

#### JOG運転設定プログラム (13.3 / 原本 p.685)

```
// [Title]JOG運転設定プログラム
// ■起動条件 X17(JOG運転速度設定指令)
(0)
LDP  G_bInputSetJogSpeedReq (X17)                               // JOG運転速度設定指令
DMOVP K20000 FX5SSC_1.stnAxCtrl1_D[0].udJOG_Speed_D (U1\G4318)  // RW:JOG速度(ダイレクト)
MOVP K0 FX5SSC_1.stnAxCtrl1_D[0].uInchingMovementAmount_D (U1\G4317)   // RW:インチング移動量(ダイレクト)
```

- ステップ(0): X17 は立上り検出接点(LDP)。DMOVP と MOVP は同一条件の並列出力。

#### インチング運転設定プログラム (13.3 / 原本 p.685)

```
// [Title]インチング運転設定プログラム
// ■起動条件 X46(インチング移動量設定指令)
(71)
LDP  G_bInputSetInchingMovementAmountReq (X46)                  // インチング移動量設定指令
MOVP K10 FX5SSC_1.stnAxCtrl1_D[0].uInchingMovementAmount_D (U1\G4317)  // RW:インチング移動量(ダイレクト)
```

- ステップ(71): X46 は立上り検出接点(LDP)。ステップ番号は原本では「(7」「1)」と折り返し表示。

#### JOG運転／インチング運転実行プログラム (13.3 / 原本 p.686)

```
// [Title]JOG運転/インチング運転実行プログラム
// ■起動条件 X20(正転JOG/インチング指令)，X22(逆転JOG/インチング指令)
(138)
LD   G_bInputForwardJogStartReq (X20)                           // 正転JOG/インチング指令
OR   G_bInputReverseJogStartReq (X22)                           // 逆転JOG/インチング指令
AND  FX5SSC_1.stSysMntr2_D.bReady_D (U1\G31500.0)               // R:準備完了(ダイレクト)
ANI  FX5SSC_1.stSysMntr2_D.bnBusy_D[0] (U1\G31501.0)            // R:BUSY(1～8軸)(ダイレクト)
SET  G_bDuringJogInchingOperation                               // JOG/インチング運転中フラグ

(237)
LDI  G_bInputForwardJogStartReq (X20)                           // 正転JOG/インチング指令
ANI  G_bInputReverseJogStartReq (X22)                           // 逆転JOG/インチング指令
RST  G_bDuringJogInchingOperation                               // JOG/インチング運転中フラグ

(244)
LD   G_bDuringJogInchingOperation                               // JOG/インチング運転中フラグ
FBCALL M_FX5SSC_JOG_01A_1                                       // (M+FX5SSC_JOG_01A) JOG/inching operation FB
     i_bEN        (B)   := 上記接点(G_bDuringJogInchingOperation)   // 実行指令
     i_stModule   (DUT) := FX5SSC_1                             // ユニットラベル / ユニットラベル
     i_uAxis      (UW)  := K1                                   // 対象軸
     i_bFJog      (B)   := G_bInputForwardJogStartReq (X20) のa接点   // 正転JOG/インチング指令 / 正転JOG指令
     i_bRJog      (B)   := G_bInputReverseJogStartReq (X22) のa接点   // 逆転JOG/インチング指令 / 逆転JOG指令
     i_udJogSpeed (UD)  := FX5SSC_1.stnAxCtrl1_D[0].udJOG_Speed_D (U1\G4318)             // RW:JOG速度(ダイレクト) / Cd.17:JOG速度
     i_uInching   (UW)  := FX5SSC_1.stnAxCtrl1_D[0].uInchingMovementAmount_D (U1\G4317)  // RW:インチング移動量(ダイレクト) / Cd.16:インチング移動量
     o_bENO       (B)   => (接続先の記載なし)                   // 実行状態
     o_bOK        (B)   => (接続先の記載なし)                   // 正常完了
     o_bErr       (B)   => (接続先の記載なし)                   // 異常完了
     o_uErrId     (UW)  => (接続先の記載なし)                   // エラーコード
```

- ステップ(138): X20 と X22 が並列(OR)，その後 bReady_D(a接点)，bnBusy_D[0](b接点)と直列。ステップ番号は原本では「(1」「38」「)」と折り返し表示(237，244も同様)。
- ステップ(237): X20，X22 ともb接点の直列。
- ステップ(244): FBの出力ピンは原本では線が右へ延びているのみで，接続先の記載なし。

#### 手動パルサ運転プログラム (13.3 / 原本 p.687)

```
// [Title]手動パルサ運転プログラム
// ■始動条件 X23↑(手動パルサ運転指令) ■停止条件 X23↓(手動パルサ運転指令)
(490)
LD   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D (U1\G31500.1)   // R:同期用フラグ(ダイレクト)
// 高速カウンタ機能の開始
DHIOEN K0 H1 H0
// CPU経由手動パルサ入力値の設定
DHCMOV FX5CPU.stSD.stHighSpeedInOut.stnHighSpeedCounter[0].dCurrentValue (SD4500) FX5SSC_1.stSysCtrl_D.dInputValueForManualPulseGeneratorViaCPU_D (U1\G5946) K0
//   SD4500: RW:高速カウンタ現在値 / U1\G5946: RW:CPU経由手動パルサ入力値(ダイレクト)

(625)
LDP  G_bInputStartMPGReq (X23)                                  // 手動パルサ運転指令
AND  FX5SSC_1.stSysMntr2_D.bReady_D (U1\G31500.0)               // R:準備完了(ダイレクト)
ANI  FX5SSC_1.stSysMntr2_D.bnBusy_D[0] (U1\G31501.0)            // R:BUSY(1～8軸)(ダイレクト)
SET  G_bDuringMPGOperation                                      // 手動パルサ運転中フラグ

(638)
LDF  G_bInputStartMPGReq (X23)                                  // 手動パルサ運転指令
RST  G_bDuringMPGOperation                                      // 手動パルサ運転中フラグ

(645)
LD   G_bDuringMPGOperation                                      // 手動パルサ運転中フラグ
FBCALL M_FX5SSC_MPG_01A_1                                       // (M+FX5SSC_MPG_01A) Manual pulse generator OP FB
     i_bEN                   (B)   := 上記接点(G_bDuringMPGOperation)   // 実行指令
     i_stModule              (DUT) := FX5SSC_1                  // ユニットラベル / ユニットラベル
     i_uAxis                 (UW)  := K1                        // 対象軸
     i_udMPGInputMagnification (UD) := K100                     // Cd.20:手動パルサ1パルス入力倍率
     o_bENO                  (B)   => (接続先の記載なし)        // 実行状態
     o_bOK                   (B)   => (接続先の記載なし)        // 正常完了
     o_bErr                  (B)   => (接続先の記載なし)        // 異常完了
     o_uErrId                (UW)  => (接続先の記載なし)        // エラーコード
```

- ステップ(490): bSynchronizationFlag_D(a接点)を条件とする DHIOEN と DHCMOV の並列出力。各命令の上に「高速カウンタ機能の開始」「CPU経由手動パルサ入力値の設定」のステートメント。ステップ番号は原本では「(4」「90」「)」と折り返し表示(625，638，645も同様)。
- ステップ(625): X23 は立上り検出接点(LDP)。bnBusy_D[0] はb接点。
- ステップ(638): X23 は立下り検出接点(LDF)。
- ステップ(645): FBの出力ピンは原本では線が右へ延びているのみで，接続先の記載なし。

#### 速度変更プログラム (13.3 / 原本 p.688)

下記のようにローカルラベルを設定してください。

| No. | ラベル名 | データ型 | クラス | Japanese/日本語(表示対象) |
|---|---|---|---|---|
| 1 | bChangeSpeedReq | ビット | VAR | 速度変更指令 |

```
// [Title]速度変更プログラム
// ■始動条件 X24(速度変更指令)
(0)
LDP  G_bInputChangeSpeedReq (X24)                               // 速度変更指令
AND  FX5SSC_1.stSysMntr2_D.bnBusy_D[0] (U1\G31501.0)            // R:BUSY(1～8軸)(ダイレクト)
SET  bChangeSpeedReq                                            // 速度変更指令

(55)
LD   M_FX5SSC_ChangeSpeed_01A_1.o_bOK                           // 正常完了
RST  bChangeSpeedReq                                            // 速度変更指令

(59)
LD   bChangeSpeedReq                                            // 速度変更指令
FBCALL M_FX5SSC_ChangeSpeed_01A_1                               // (M+FX5SSC_ChangeSpeed_01A) Speed change FB
     i_bEN               (B)   := 上記接点(bChangeSpeedReq)     // 実行指令
     i_stModule          (DUT) := FX5SSC_1                      // ユニットラベル / ユニットラベル
     i_uAxis             (UW)  := K1                            // 対象軸
     i_udSpeedChangeValue (UD) := K20000                        // Cd.14:速度変更値
     o_bENO              (B)   => (接続先の記載なし)            // 実行状態
     o_bOK               (B)   => (接続先の記載なし)            // 正常完了
     o_bErr              (B)   => (接続先の記載なし)            // 異常完了
     o_uErrId            (UW)  => (接続先の記載なし)            // エラーコード
```

- ステップ(0): X24 は立上り検出接点(LDP)。bnBusy_D[0] はa接点。
- ステップ(59): FBの出力ピンは原本では線が右へ延びているのみで，接続先の記載なし。

#### オーバーライドプログラム (13.3 / 原本 p.688)

下記のようにローカルラベルを設定してください。

| No. | ラベル名 | データ型 | クラス | Japanese/日本語(表示対象) |
|---|---|---|---|---|
| 1 | bOverrideReq_P | ビット | VAR | オーバーライド指令パルス |

```
// [Title]オーバーライドプログラム
// ■始動条件 X25(オーバーライド指令)
(206)
LD   G_bInputOverrideReq (X25)                                  // オーバーライド指令
PLS  bOverrideReq_P                                             // オーバーライド指令パルス

(263)
LD   bOverrideReq_P                                             // オーバーライド指令パルス
AND  FX5SSC_1.stSysMntr2_D.bnBusy_D[0] (U1\G31501.0)            // R:BUSY(1～8軸)(ダイレクト)
MOVP K200 FX5SSC_1.stnAxCtrl1_D[0].uOverride_D (U1\G4313)       // RW:位置決め運転速度オーバーライド(ダイレクト)
```

- ステップ(263): bnBusy_D[0] はa接点。

#### 加減速時間変更プログラム (13.3 / 原本 p.689)

下記のようにローカルラベルを設定してください。

| No. | ラベル名 | データ型 | クラス | Japanese/日本語(表示対象) |
|---|---|---|---|---|
| 1 | bChangeAccDecTime_iEnable | ビット | VAR | 加減速時間変更許可フラグ |

```
// [Title]加減速時間変更プログラム
// ■始動条件 X27(加減速時間変更不許可指令)
(273)
LDI  G_bInputChangeAccDecTimeDisable (X27)                      // 加減速時間変更不許可指令
OUT  bChangeAccDecTime_iEnable                                  // 加減速時間変更許可フラグ

(332)
LD   G_bInputChangeAccDecTimeReq (X26)                          // 加減速時間変更指令
FBCALL M_FX5SSC_ChangeAccDecTime_01A_1                          // (M+FX5SSC_ChangeAccDecTime_01A) Acc./dec. time SV change FB
     i_bEN                    (B)   := 上記接点(G_bInputChangeAccDecTimeReq (X26))   // 実行指令
     i_stModule               (DUT) := FX5SSC_1                 // ユニットラベル / ユニットラベル
     i_uAxis                  (UW)  := K1                       // 対象軸
     i_bEnable                (B)   := bChangeAccDecTime_iEnable のa接点   // 加減速時間変更許可フラグ / 加減速時間変更許可フラグ
     i_udNewAccelerationTime  (UD)  := K2000                    // Cd.10:加速時間変更値
     i_udNewDecelerationTime  (UD)  := K0                       // Cd.11:減速時間変更値
     o_bENO                   (B)   => (接続先の記載なし)       // 実行状態
     o_bOK                    (B)   => (接続先の記載なし)       // 正常完了
     o_bErr                   (B)   => (接続先の記載なし)       // 異常完了
     o_uErrId                 (UW)  => (接続先の記載なし)       // エラーコード
```

- ステップ(273): X27 はb接点。
- ステップ(332): FBの出力ピンは原本では線が右へ延びているのみで，接続先の記載なし。

#### トルク変更プログラム (13.3 / 原本 p.689)

下記のようにローカルラベルを設定してください。

| No. | ラベル名 | データ型 | クラス | Japanese/日本語(表示対象) |
|---|---|---|---|---|
| 1 | bChangeTorqueReq | ビット | VAR | トルク変更指令 |

```
// [Title]トルク変更プログラム
// ■始動条件 X30(トルク変更指令)
(473)
LD   G_bInputChangeTorqueReq (X30)                              // トルク変更指令
PLS  bChangeTorqueReq                                           // トルク変更指令

(526)
LD   bChangeTorqueReq                                           // トルク変更指令
AND  FX5SSC_1.stSysMntr2_D.bnBusy_D[0] (U1\G31501.0)            // R:BUSY(1～8軸)(ダイレクト)
MOV  K1000 FX5SSC_1.stnAxCtrl1_D[0].uForwardNewTorque_D (U1\G4325)   // RW:トルク変更値/正転トルク変更値(ダイレクト)
```

- ステップ(526): bnBusy_D[0] はa接点。命令は MOV(パルス形ではない)。

#### 目標位置変更プログラム (13.3 / 原本 p.690)

下記のようにローカルラベルを設定してください。

| No. | ラベル名 | データ型 | クラス | Japanese/日本語(表示対象) |
|---|---|---|---|---|
| 1 | bTargetPositionChangeReq | ビット | VAR | 目標位置変更指令 |

```
// [Title]目標位置変更プログラム
// ■始動条件 X47(目標位置変更指令)
(537)
LDP  G_bInputTargetPositionChangeReq (X47)                      // 目標位置変更指令
AND  FX5SSC_1.stSysMntr2_D.bnBusy_D[0] (U1\G31501.0)            // R:BUSY(1～8軸)(ダイレクト)
SET  bTargetPositionChangeReq                                   // 目標位置変更指令

(596)
LD   M_FX5SSC_ChangePosition_01A_1.o_bOK                        // 正常完了
RST  bTargetPositionChangeReq                                   // 目標位置変更指令

(600)
LD   bTargetPositionChangeReq                                   // 目標位置変更指令
FBCALL M_FX5SSC_ChangePosition_01A_1                            // (M+FX5SSC_ChangePosition_01A) Target position change FB
     i_bEN                (B)   := 上記接点(bTargetPositionChangeReq)   // 実行指令
     i_stModule           (DUT) := FX5SSC_1                     // ユニットラベル / ユニットラベル
     i_uAxis              (UW)  := K1                           // 対象軸
     i_dTargetNewPosition (D)   := K-750000                     // Cd.27:目標位置変更値(アドレス)
     i_udTargetNewSpeed   (UD)  := K54000                       // Cd.28:目標位置変更値(速度)
     o_bENO               (B)   => (接続先の記載なし)           // 実行状態
     o_bOK                (B)   => (接続先の記載なし)           // 正常完了
     o_bErr               (B)   => (接続先の記載なし)           // 異常完了
     o_uErrId             (UW)  => (接続先の記載なし)           // エラーコード
```

- ステップ(537): X47 は立上り検出接点(LDP)。bnBusy_D[0] はa接点。
- ステップ(600): FBの出力ピンは原本では線が右へ延びているのみで，接続先の記載なし。

#### サーボパラメータ読出し／書込みプログラム (13.3 / 原本 p.691)

下記のようにローカルラベルを設定してください。

| No. | ラベル名 | データ型 | クラス | Japanese/日本語(表示対象) |
|---|---|---|---|---|
| 1 | bServoParamRWReq | ビット | VAR | サーボパラメータ読出し書込み要求 |
| 2 | uCmdData | ワード[符号なし]/ビット列[16ビット] | VAR | コマンド送信要求 |
| 3 | bServoParamChange | ビット | VAR | サーボパラメータ変更 |
| 4 | bServoParamRead | ビット | VAR | サーボパラメータ読出し |

```
// [Title]サーボパラメータ読出し/書込みプログラム
// ■ 対象パラメータ PA10 指令インポジション範囲(Obj2010h)
(769)
LD   G_bInputServoParamRead (X54)                               // サーボパラメータ読出し指令
PLS  bServoParamRead                                            // サーボパラメータ読出し

(850)
LD   bServoParamRead                                            // サーボパラメータ読出し
MOVP K1 uCmdData                                                // コマンド送信要求
SET  bServoParamRWReq                                           // サーボパラメータ読出し書込み要求

(858)
LD   G_bInputServoParamChange (X53)                             // サーボパラメータ変更指令
PLS  bServoParamChange                                          // サーボパラメータ変更

(863)
LD   bServoParamChange                                          // サーボパラメータ変更
BMOVP D20 M_FX5SSC_ReadWriteParameter_00A_1.pb_u4SDOData K4     // D20: サーボパラメータ変更値 → Cd.164:任意SDO転送データ1
MOVP K11 uCmdData                                               // コマンド送信要求
SET  bServoParamRWReq                                           // サーボパラメータ読出し書込み要求

(876)
LD   M_FX5SSC_ReadWriteParameter_00A_1.o_bOK                    // 正常完了
MPS
AND  G_bInputServoParamRead (X54)                               // サーボパラメータ読出し指令
BMOVP M_FX5SSC_ReadWriteParameter_00A_1.pb_u4SDOData D40 K4     // Cd.164:任意SDO転送データ1 → D40: サーボパラメータ読出し値
MPP
RST  bServoParamRWReq                                           // サーボパラメータ読出し書込み要求

// ↓ 原本 p.692
(889)
LD   bServoParamRWReq                                           // サーボパラメータ読出し書込み要求
FBCALL M_FX5SSC_ReadWriteParameter_00A_1                        // (M+FX5SSC_ReadWriteParameter_00A) read/write parameters FB
     i_bEN          (B)   := 上記接点(bServoParamRWReq)         // 実行指令
     i_stModule     (DUT) := FX5SSC_1                           // ユニットラベル / ユニットラベル
     i_uAxis        (UW)  := K1                                 // 対象軸
     i_udSDONumber  (UD)  := H200A0000                          // Pr.512:任意SDO1
     i_uSDORequest  (UW)  := uCmdData                           // コマンド送信要求 / Cd.160:任意SDO転送要求1
     o_bENO         (B)   => (接続先の記載なし)                 // 実行状態
     o_bOK          (B)   => (接続先の記載なし)                 // 正常完了
     o_udSDOErrorID (UD)  => (接続先の記載なし)                 // SDO転送結果
     o_uSDOStatus   (UW)  => (接続先の記載なし)                 // SDO転送ステータス
     o_bErr         (B)   => (接続先の記載なし)                 // 異常完了
     o_uErrId       (UW)  => (接続先の記載なし)                 // エラーコード
     // FBボックス下端に「pb_u4SDOData」の表示あり
```

- ステップ(850)，(863): 各命令は同一条件の並列出力。BMOVPは原本では「BMOV」「P」と2段表示。ステップ番号は原本では「(76」「9)」のように折り返し表示(850，858，863，876も同様)。
- ステップ(876): BMOVP のみ X54(a接点)と直列。RST bServoParamRWReq は o_bOK の直後から分岐(X54 を経由しない)。
- ステップ(889)(原本 p.692): FBの出力ピンは原本では線が右へ延びているのみで，接続先の記載なし。ステップ番号は原本では「(88」「9)」と折り返し表示。
#### ステップ運転プログラム (13.3 / 原本 p.692)

下記のようにローカルラベルを設定してください。

| No. | ラベル名 | データ型 | クラス | Japanese/日本語(表示対象) |
|---|---|---|---|---|
| 1 | bStepOperationReq_P | ビット | VAR | ステップ運転指令パルス |

```
// [Title]ステップモードプログラム
// ■始動条件 X31(ステップ運転指令)
(0)
LD   G_bInputStepOperationReq (X31)                             // ステップ運転指令
PLS  bStepOperationReq_P                                        // ステップ運転指令パルス

(56)
LD   bStepOperationReq_P                                        // ステップ運転指令パルス
ANI  FX5SSC_1.stnAxCtrl2_D[0].uPositioningStart_D.0 (U1\G30104.0)   // RW:位置決め始動(ダイレクト)
ANI  FX5SSC_1.stnAxMntr_D[0].uStatus_D.E (U1\G2417.E)           // R:ステータス(ダイレクト)
MOV  K1 FX5SSC_1.stnAxCtrl1_D[0].uStepMode_D (U1\G4344)         // RW:ステップモード(ダイレクト)
MOV  K1 FX5SSC_1.stnAxCtrl1_D[0].uStepValid_D (U1\G4345)        // RW:ステップ有効フラグ(ダイレクト)

(76)
LD   G_bInputStepStartInformationReq (X50)                      // ステップ始動情報指令
MOVP K1 FX5SSC_1.stnAxCtrl1_D[0].uStepStartInformation_D (U1\G4346)   // RW:ステップ始動情報(ダイレクト)
```

- ステップ(56): uPositioningStart_D.0 と uStatus_D.E はb接点。2つの MOV(パルス形ではない)は同一条件の並列出力。

#### スキッププログラム (13.3 / 原本 p.693)

下記のようにローカルラベルを設定してください。

| No. | ラベル名 | データ型 | クラス | Japanese/日本語(表示対象) |
|---|---|---|---|---|
| 1 | bSkipReq_P | ビット | VAR | スキップ指令パルス |
| 2 | bSkipReq | ビット | VAR | スキップ指令 |

```
// [Title]スキップ指令プログラム
// ■始動条件 X32(スキップ指令)
(0)
LD   G_bInputSkipReq (X32)                                      // スキップ指令
PLS  bSkipReq_P                                                 // スキップ指令パルス

(53)
LD   bSkipReq_P                                                 // スキップ指令パルス
AND  FX5SSC_1.stSysMntr2_D.bnBusy_D[0] (U1\G31501.0)            // R:BUSY(1～8軸)(ダイレクト)
SET  bSkipReq                                                   // スキップ指令

(60)
LD   bSkipReq                                                   // スキップ指令
MPS
MOVP K1 FX5SSC_1.stnAxCtrl1_D[0].uSkip_D (U1\G4347)             // RW:スキップ指令(ダイレクト)
MPP
AND=_U FX5SSC_1.stnAxCtrl1_D[0].uSkip_D (U1\G4347) K0           // RW:スキップ指令(ダイレクト)
RST  bSkipReq                                                   // スキップ指令
```

- ステップ(53): bnBusy_D[0] はa接点。
- ステップ(60): bSkipReq の直後で分岐し，上段が MOVP，下段が比較接点「=_U」(uSkip_D = K0)を経由して RST bSkipReq。

#### ティーチングプログラム (13.3 / 原本 p.693)

下記のようにローカルラベルを設定してください。

| No. | ラベル名 | データ型 | クラス | Japanese/日本語(表示対象) |
|---|---|---|---|---|
| 1 | bTeachingReq_P | ビット | VAR | ティーチング指令パルス |
| 2 | bTeachingReq | ビット | VAR | ティーチング指令 |

```
// [Title]ティーチングプログラム
// ■始動条件 X33(ティーチング指令) ＊[Da.6]位置決めアドレス/移動量、もしくは[Da.7]円弧アドレスに設定
(0)
LD   G_bInputTeachingReq (X33)                                  // ティーチング指令
PLS  bTeachingReq_P                                             // ティーチング指令パルス

(100)
LD   bTeachingReq_P                                             // ティーチング指令パルス
ANI  FX5SSC_1.stSysMntr2_D.bnBusy_D[0] (U1\G31501.0)            // R:BUSY(1～8軸)(ダイレクト)
SET  bTeachingReq                                               // ティーチング指令

(107)
LD   bTeachingReq                                               // ティーチング指令
MPS
MOVP K0 FX5SSC_1.stnAxCtrl1_D[0].uTeachingDataSelection_D (U1\G4348)        // RW:ティーチングデータ選択(ダイレクト)
MRD
MOVP K1 FX5SSC_1.stnAxCtrl1_D[0].uTeachingPositioningDataNo_D (U1\G4349)    // RW:ティーチング位置決めデータNo.(ダイレクト)
MPP
AND=_U FX5SSC_1.stnAxCtrl1_D[0].uTeachingPositioningDataNo_D (U1\G4349) K0  // RW:ティーチング位置決めデータNo.(ダイレクト)
RST  bTeachingReq                                               // ティーチング指令
```

- ステップ(100): bnBusy_D[0] はb接点。
- ステップ(107): bTeachingReq の直後で3分岐。上段・中段が MOVP，下段が比較接点「=_U」(uTeachingPositioningDataNo_D = K0)を経由して RST bTeachingReq。

#### 連続運転中断プログラム (13.3 / 原本 p.694)

下記のようにローカルラベルを設定してください。

| No. | ラベル名 | データ型 | クラス | Japanese/日本語(表示対象) |
|---|---|---|---|---|
| 1 | bStopContinuousOperationReq_P | ビット | VAR | 連続運転中断指令パルス |

```
// [Title]連続運転中断要求プログラム
// ■始動条件 X34(連続運転中断指令)
(0)
LD   G_bInputStopContinuousOperationReq (X34)                   // 連続運転中断指令
PLS  bStopContinuousOperationReq_P                              // 連続運転中断指令パルス

(57)
LD   bStopContinuousOperationReq_P                              // 連続運転中断指令パルス
AND  FX5SSC_1.stSysMntr2_D.bnBusy_D[0] (U1\G31501.0)            // R:BUSY(1～8軸)(ダイレクト)
MOV  K1 FX5SSC_1.stnAxCtrl1_D[0].uInterruptOperation_D (U1\G4320)   // RW:連続運転中断要求(ダイレクト)
```

- ステップ(57): bnBusy_D[0] はa接点。命令は MOV(パルス形ではない)。

#### 再始動プログラム (13.3 / 原本 p.694)

下記のようにローカルラベルを設定してください。

| No. | ラベル名 | データ型 | クラス | Japanese/日本語(表示対象) |
|---|---|---|---|---|
| 1 | bRestartReq | ビット | VAR | 再始動指令 |

```
// [Title]再始動プログラム
// ■始動条件 X35(再始動指令)
(0)
LDP  G_bInputRestartReq (X35)                                   // 再始動指令
SET  bRestartReq                                                // 再始動指令

(50)
LDP  M_FX5SSC_Restart_01A_1.o_bOK                               // 正常完了
RST  bRestartReq                                                // 再始動指令

(56)
LD   bRestartReq                                                // 再始動指令
FBCALL M_FX5SSC_Restart_01A_1                                   // (M+FX5SSC_Restart_01A) Restart FB
     i_bEN      (B)   := 上記接点(bRestartReq)                  // 実行指令
     i_stModule (DUT) := FX5SSC_1                               // ユニットラベル / ユニットラベル
     i_uAxis    (UW)  := K1                                     // 対象軸
     o_bENO     (B)   => (接続先の記載なし)                     // 実行状態
     o_bOK      (B)   => (接続先の記載なし)                     // 正常完了
     o_bErr     (B)   => (接続先の記載なし)                     // 異常完了
     o_uErrId   (UW)  => (接続先の記載なし)                     // エラーコード
```

- ステップ(0): X35 は立上り検出接点(LDP)。
- ステップ(50): o_bOK は立上り検出接点(LDP)。
- ステップ(56): FBの出力ピンは原本では線が右へ延びているのみで，接続先の記載なし。

#### パラメータ初期化プログラム (13.3 / 原本 p.695)

```
// [Title]パラメータ初期化プログラム
// ■始動条件 X36(パラメータ初期化指令)
(0)
LDP  G_bInputInitializeParameterReq (X36)                       // パラメータ初期化指令
SET  G_bInitializeParameterReq                                  // パラメータ初期化指令

(61)
LD   M_FX5SSC_InitializeParameter_00A_1.o_bOK                   // 正常完了
RST  G_bInitializeParameterReq                                  // パラメータ初期化指令

(66)
LD   G_bInitializeParameterReq                                  // パラメータ初期化指令
FBCALL M_FX5SSC_InitializeParameter_00A_1                       // (M+FX5SSC_InitializeParameter_00A) Parameter Initialization FB
     i_bEN      (B)   := 上記接点(G_bInitializeParameterReq)    // 実行指令
     i_stModule (DUT) := FX5SSC_1                               // ユニットラベル / ユニットラベル
     o_bENO     (B)   => (接続先の記載なし)                     // 実行状態
     o_bOK      (B)   => (接続先の記載なし)                     // 正常完了
     o_bErr     (B)   => (接続先の記載なし)                     // 異常完了
     o_uErrId   (UW)  => (接続先の記載なし)                     // エラーコード
```

- ステップ(0): X36 は立上り検出接点(LDP)。
- ステップ(66): FBの出力ピンは原本では線が右へ延びているのみで，接続先の記載なし。

#### フラッシュROM書込みプログラム (13.3 / 原本 p.695)

```
// [Title]フラッシュROM書込みプログラム
// ■始動条件 X37(フラッシュROM書込み指令)
(0)
LDP  G_bInputWriteFlashReq (X37)                                // フラッシュROM書込み指令
SET  G_bWriteFlashReq                                           // フラッシュROM書込み指令

(67)
LD   M_FX5SSC_WriteFlash_00A_1.o_bOK                            // 正常完了
RST  G_bWriteFlashReq                                           // フラッシュROM書込み指令

(72)
LD   G_bWriteFlashReq                                           // フラッシュROM書込み指令
FBCALL M_FX5SSC_WriteFlash_00A_1                                // (M+FX5SSC_WriteFlash_00A) Flash ROM writing FB
     i_bEN      (B)   := 上記接点(G_bWriteFlashReq)             // 実行指令
     i_stModule (DUT) := FX5SSC_1                               // ユニットラベル / ユニットラベル
     o_bENO     (B)   => (接続先の記載なし)                     // 実行状態
     o_bOK      (B)   => (接続先の記載なし)                     // 正常完了
     o_bErr     (B)   => (接続先の記載なし)                     // 異常完了
     o_uErrId   (UW)  => (接続先の記載なし)                     // エラーコード
```

- ステップ(0): X37 は立上り検出接点(LDP)。
- ステップ(72): FBの出力ピンは原本では線が右へ延びているのみで，接続先の記載なし。

#### エラーリセットプログラム (13.3 / 原本 p.696)

下記のようにローカルラベルを設定してください。

| No. | ラベル名 | データ型 | クラス | Japanese/日本語(表示対象) |
|---|---|---|---|---|
| 1 | bErrReadReq | ビット | VAR | エラー読出し指令 |
| 2 | bErrResetReq | ビット | VAR | エラーリセット指令 |

```
// [Title]エラーリセットプログラム
// ■始動条件 X40(エラーリセット指令)
(0)
LD   FX5SSC_1.stnAxMntr_D[0].uStatus_D.D (U1\G2417.D)           // R:ステータス(ダイレクト)
OR   FX5SSC_1.stnAxMntr_D[0].uStatus_D.9 (U1\G2417.9)           // R:ステータス(ダイレクト)
OUT  bErrReadReq                                                // エラー読出し指令

(60)
LD   G_bInputErrResetReq (X40)                                  // エラーリセット指令
PLS  bErrResetReq                                               // エラーリセット指令

(65)
LD   bErrReadReq                                                // エラー読出し指令
FBCALL M_FX5SSC_OperateError_01A_1                              // (M+FX5SSC_OperateError_01A) Error operation FB
     i_bEN            (B)   := 上記接点(bErrReadReq)            // 実行指令
     i_stModule       (DUT) := FX5SSC_1                         // ユニットラベル / ユニットラベル
     i_uAxis          (UW)  := K1                               // 対象軸
     i_bErrReset      (B)   := bErrResetReq のa接点             // エラーリセット指令 / エラーリセット指令
     o_bENO           (B)   => (接続先の記載なし)               // 実行状態
     o_bOK            (B)   => (接続先の記載なし)               // 正常完了
     o_bModuleErr     (B)   => (接続先の記載なし)               // 軸エラー検出
     o_uModuleErrId   (UW)  => (接続先の記載なし)               // 軸エラーコード
     o_bModuleWarn    (B)   => (接続先の記載なし)               // 軸ワーニング検出
     o_uModuleWarnId  (UW)  => (接続先の記載なし)               // 軸ワーニングコード
     o_bErr           (B)   => (接続先の記載なし)               // 異常完了
     o_uErrId         (UW)  => (接続先の記載なし)               // エラーコード
```

- ステップ(0): uStatus_D.D と uStatus_D.9(いずれもa接点)の並列(OR)で bErrReadReq をコイル出力(OUT)。
- ステップ(65): FBの出力ピンは原本では線が右へ延びているのみで，接続先の記載なし。

#### 軸停止プログラム (13.3 / 原本 p.697)

下記のようにローカルラベルを設定してください。

| No. | ラベル名 | データ型 | クラス | Japanese/日本語(表示対象) |
|---|---|---|---|---|
| 1 | bStopReq_P | ビット | VAR | 停止指令 |

```
// [Title]軸停止プログラム
// ■始動条件 X41(停止指令)
(0)
LD   G_bInputStopReq (X41)                                      // 停止指令
PLS  bStopReq_P                                                 // 停止指令

(48)
LD   bStopReq_P                                                 // 停止指令
SET  FX5SSC_1.stnAxCtrl2_D[0].uStopAxis_D.0 (U1\G30100.0)       // RW:軸停止(ダイレクト)

(53)
LDI  G_bInputStopReq (X41)                                      // 停止指令
RST  FX5SSC_1.stnAxCtrl2_D[0].uStopAxis_D.0 (U1\G30100.0)       // RW:軸停止(ダイレクト)
```

- ステップ(53): X41 はb接点。
