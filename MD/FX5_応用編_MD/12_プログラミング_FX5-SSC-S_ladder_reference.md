# 12 プログラミング[FX5-SSC-S] (12章 / 原本 p.601-652)

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
| p.601 | 12.1 プログラム作成上の注意事項 | 全文 |
| p.602 | 12.2 プログラムの作成 | 全文 |
| p.603-619 | 12.3 位置決めプログラム例(ラベル使用時) | 全文(ラダーはニモニック書き起こし) |
| p.620-652 | 12.4 位置決めプログラム例(バッファメモリ使用時) | 全文(ラダーはニモニック書き起こし) |

## 目次

- 12 プログラミング[FX5-SSC-S]
- 12.1 プログラム作成上の注意事項
  - データの読出し／書込み
  - 速度変更実行間隔の制約
  - オーバーラン時の処理
  - システム構成
- 12.2 プログラムの作成
  - プログラムの全体構成
- 12.3 位置決めプログラム例(ラベル使用時)
  - 使用するラベル一覧
  - プログラム例
- 12.4 位置決めプログラム例(バッファメモリ使用時)
  - 使用するデバイス一覧
  - プログラム例

---

## 12 プログラミング[FX5-SSC-S] (12章 / 原本 p.601)

シンプルモーションユニットを使った位置決め制御を行うために必要なプログラムについて説明しています。制御に必要なプログラムは，「始動条件」，「始動タイムチャート」，「デバイス設定」，制御全体の構成などを考慮して作成します。(実行したい制御に合わせて，パラメータや位置決めデータ，ブロック始動データ，条件データなどをシンプルモーションユニットに設定し，制御データの設定プログラムや各制御の始動プログラムを作成する必要があります。)

## 12.1 プログラム作成上の注意事項 (12.1 / 原本 p.601)

CPUユニットからシンプルモーションユニットのバッファメモリへデータを書き込むときの，共通の注意事項を示します。

### データの読出し／書込み (12.1 / 原本 p.601)

本章に示すデータの設定(各種パラメータ，位置決めデータ，ブロック始動データ)は，できるだけエンジニアリングツールで行われることをおすすめします。プログラムで設定する場合，かなりのプログラムとデバイスを使用するため，複雑になると共に，スキャンタイムの増大につながります｡また，連続軌跡制御または連続位置決め制御中に位置決めデータを書き換える場合は，4つ前の位置決めデータを実行するまでに書き換えてください。4つ前の位置決めデータを実行する前に位置決めデータの書換えが行われていない場合，データは書き換えられていないものとして処理されます。

### 速度変更実行間隔の制約 (12.1 / 原本 p.601)

シンプルモーションユニットで速度変更機能またはオーバーライド機能により連続して速度変更を行う場合は，速度変更の間隔が10 ms以上となるようにしてください。

### オーバーラン時の処理 (12.1 / 原本 p.601)

詳細パラメータ1でストロークリミット上限値および下限値の設定にて，オーバーランの防止にはなります。ただし，これはシンプルモーションユニットが正常に動作している場合のみ有効です。システムの安全性からみて限界リミットスイッチを設け，リミットスイッチ作動によって，サーボアンプの主回路電源をOFFするような外部の回路を設けることをおすすめします。

### システム構成 (12.1 / 原本 p.601)

プログラム例で使用するシステム構成を示します。

【図】プログラム例のシステム構成(原本 p.601)
- 左から (1)(2)(3)(4) のユニットを連結。
  - (1)FX5U-32MR/ES
  - (2)FX5-40SSC-S
  - (3)FX5-16EX/ES
  - (4)FX5-16EX/ES
- 外部機器から X00~X17 が (1) へ，X20~X37 が (3) へ，X40~X57 が (4) へ入力される(矢印)。
- (2) の下にサーボアンプ(MR-J4-_B_)が接続され，その先にサーボモータが接続されている。

## 12.2 プログラムの作成 (12.2 / 原本 p.602)

本節では，実際に使用する「位置決め制御の運転プログラム」について説明します。

### プログラムの全体構成 (12.2 / 原本 p.602)

位置決め制御の運転プログラムの全体構成を示します。

| No. | プログラム名 | 備考 |
|---|---|---|
| 1 | パラメータ設定プログラム | • エンジニアリングツールにてパラメータ，位置決めデータ，ブロック始動データ，サーボパラメータを設定する場合，プログラムは不要です。<br>• 機械原点復帰制御を行わない場合は，原点復帰用パラメータの設定は不要です。 |
| 2 | 位置決めデータ設定プログラム | • エンジニアリングツールにてパラメータ，位置決めデータ，ブロック始動データ，サーボパラメータを設定する場合，プログラムは不要です。<br>• 機械原点復帰制御を行わない場合は，原点復帰用パラメータの設定は不要です。 |
| 3 | ブロック始動データ設定プログラム | • エンジニアリングツールにてパラメータ，位置決めデータ，ブロック始動データ，サーボパラメータを設定する場合，プログラムは不要です。<br>• 機械原点復帰制御を行わない場合は，原点復帰用パラメータの設定は不要です。 |
| 4 | サーボパラメータ設定プログラム | • エンジニアリングツールにてパラメータ，位置決めデータ，ブロック始動データ，サーボパラメータを設定する場合，プログラムは不要です。<br>• 機械原点復帰制御を行わない場合は，原点復帰用パラメータの設定は不要です。 |
| 5 | 原点復帰要求OFFプログラム | 機械原点復帰制御を行う場合は不要です。 |
| 6 | 外部指令機能有効設定プログラム | — |
| 7 | シーケンサレディ信号ONプログラム | — |
| 8 | 全軸サーボONプログラム | — |
| 9 | 位置決め始動番号設定プログラム | — |
| 10 | 位置決め始動プログラム | — |
| 11 | MコードOFFプログラム | Ｍコード出力機能を使用しない場合は不要です。 |
| 12 | JOG運転設定プログラム | JOG運転を使用しない場合は不要です。 |
| 13 | インチング運転設定プログラム | インチング運転を使用しない場合は不要です。 |
| 14 | JOG運転／インチング運転実行プログラム | JOG運転およびインチング運転を使用しない場合は不要です。 |
| 15 | 手動パルサ運転プログラム | 手動パルサ運転を使用しない場合は不要です。 |
| 16 | 速度変更プログラム | 必要に応じて追加するプログラムです。 |
| 17 | オーバーライドプログラム | 必要に応じて追加するプログラムです。 |
| 18 | 加減速時間変更プログラム | 必要に応じて追加するプログラムです。 |
| 19 | トルク変更プログラム | 必要に応じて追加するプログラムです。 |
| 20 | ステップ運転プログラム | 必要に応じて追加するプログラムです。 |
| 21 | スキッププログラム | 必要に応じて追加するプログラムです。 |
| 22 | ティーチングプログラム | 必要に応じて追加するプログラムです。 |
| 23 | 連続運転中断プログラム | 必要に応じて追加するプログラムです。 |
| 24 | 目標位置変更プログラム | 必要に応じて追加するプログラムです。 |
| 25 | 再始動プログラム | 必要に応じて追加するプログラムです。 |
| 26 | パラメータ初期化プログラム | 必要に応じて追加するプログラムです。 |
| 27 | フラッシュ ROM書込みプログラム | 必要に応じて追加するプログラムです。 |
| 28 | エラーリセットプログラム | 必要に応じて追加するプログラムです。 |
| 29 | 軸停止プログラム | — |

※原本では「備考」列の No.1～4(箇条書き2項目)，No.6～9(「—」)，No.16～28(「必要に応じて追加するプログラムです。」)がそれぞれ結合セル。各行に展開。No.10 と No.29 の「—」は単独セル。

## 12.3 位置決めプログラム例(ラベル使用時) (12.3 / 原本 p.603-619)

### 使用するラベル一覧 (12.3 / 原本 p.603-606)

プログラム例では，使用するラベルを下記のように割り付けています。

#### ユニットラベル (12.3 / 原本 p.603-604)

| 分類 | ラベル名 | 内容 |
|---|---|---|
| 先頭I/O No. | FX5SSC_1.uIO | 先頭I/O No. |
| 入力信号 | FX5SSC_1.stSysCtrl_D.bAllAxisServoOn_D | 全軸サーボON |
| 入力信号 | FX5SSC_1.stSysMntr2_D.bReady_D | 準備完了 |
| 入力信号 | FX5SSC_1.bSynchronizationFlag | 同期用フラグ |
| 入力信号 | FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D | 同期用フラグ |
| 入力信号 | FX5SSC_1.stSysMntr2_D.bnBusy_D[0] | 軸1 BUSY信号 |
| 出力信号 | FX5SSC_1.stSysCtrl_D.bPLC_Ready_D | シーケンサレディ信号 |
| 出力信号 | FX5SSC_1.stnAxCtrl2_D[0].uPositioningStart_D.0 | 軸1 位置決め始動信号 |
| パラメータ | FX5SSC_1.stnAxPrm_D[0].dHomePosition_D | 軸1 原点アドレス |
| パラメータ | FX5SSC_1.stnAxPrm_D[0].dSoftwareStrokeLowerLimit_D | 軸1 ソフトウェアストロークリミット下限値 |
| パラメータ | FX5SSC_1.stnAxPrm_D[0].dSoftwareStrokeUpperLimit_D | 軸1 ソフトウェアストロークリミット上限値 |
| パラメータ | FX5SSC_1.stnAxPrm_D[0].uExternalCommandFunctionMode_D | 軸1 外部指令機能選択 |
| パラメータ | FX5SSC_1.stnAxPrm_D[0].uHomingDirection_D | 軸1 原点復帰方向 |
| パラメータ | FX5SSC_1.stnAxPrm_D[0].uHomingMethod_D | 軸1 原点復帰方式 |
| パラメータ | FX5SSC_1.stnAxPrm_D[0].uHomingRetry_D | 軸1 原点復帰リトライ |
| パラメータ | FX5SSC_1.stnAxPrm_D[0].uUnitMagnification_D | 軸1 単位倍率(AM) |
| パラメータ | FX5SSC_1.stnAxPrm_D[0].uUnit_D | 軸1 単位設定 |
| パラメータ | FX5SSC_1.stnAxPrm_D[0].uVP_Mode_D | 軸1 速度･位置機能選択 |
| パラメータ | FX5SSC_1.stnAxPrm_D[0].uV_CommandPosition_D | 軸1 速度制御時の送り現在値 |
| パラメータ | FX5SSC_1.stnAxPrm_D[0].udCreepSpeed_D | 軸1 クリープ速度 |
| パラメータ | FX5SSC_1.stnAxPrm_D[0].udHomingSpeed_D | 軸1 原点復帰速度 |
| パラメータ | FX5SSC_1.stnAxPrm_D[0].udMovementAmountPerRotation_D | 軸1 1回転あたりの移動量(AL) |
| パラメータ | FX5SSC_1.stnAxPrm_D[0].udPulsesPerRotation_D | 軸1 1回転あたりのパルス数(AP) |
| 軸モニタデータ | FX5SSC_1.stnAxMntr_D[0].uM_Code_D | 軸1 有効Mコード |
| 軸モニタデータ | FX5SSC_1.stnAxMntr_D[0].uStatus_D.3 | 軸1 原点復帰要求フラグ |
| 軸モニタデータ | FX5SSC_1.stnAxMntr_D[0].uStatus_D.9 | 軸1 軸ワーニング検出 |
| 軸モニタデータ | FX5SSC_1.stnAxMntr_D[0].uStatus_D.C | 軸1 MコードON |
| 軸モニタデータ | FX5SSC_1.stnAxMntr[0].uStatus.D | 軸1 エラー検出 |
| 軸モニタデータ | FX5SSC_1.stnAxMntr_D[0].uStatus_D.D | 軸1 エラー検出 |
| 軸モニタデータ | FX5SSC_1.stnAxMntr[0].uStatus.E | 軸1 始動完了 |
| 軸モニタデータ | FX5SSC_1.stnAxMntr_D[0].uStatus_D.E | 軸1 始動完了 |
| 軸モニタデータ | FX5SSC_1.stnAxMntr_D[0].uStatus_D.F | 軸1 位置決め完了 |
| 軸モニタデータ | FX5SSC_1.stnAxMntr_D[0].dCommandPosition_D | 軸1 送り現在値 |
| システムモニタデータ | FX5SSC_1.stSysMntr1_D.wSSCNET_ControlStatus_D | SSCNET制御ステータス |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].dNewPosition_D | 軸1 現在値変更値 |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uClearHomingRequestFlag_D | 軸1 原点復帰要求フラグOFF要求 |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uClear_M_Code_D | 軸1 MコードOFF要求 |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uEnablePV_Switching_D | 軸1 位置・速度切換え許可フラグ |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uEnableVP_Switching_D | 軸1 速度・位置切換え許可フラグ |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uExternalCommandValid_D | 軸1 外部指令有効 |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uForwardNewTorque_D | 軸1トルク変更値/正転トルク変更値 |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uInterruptOperation_D | 軸1 連続運転中断要求 |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uOverride_D | 軸1 位置決め運転速度オーバーライド |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uPositioningStartNo_D | 軸1 位置決め始動番号 |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uPositioningStartingPointNo_D | 軸1 位置決め始動ポイント番号 |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uSkip_D | 軸1 スキップ指令 |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uStepMode_D | 軸1 ステップモード |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uStepStartInformation_D | 軸1 ステップ始動情報 |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uStepValid_D | 軸1 ステップ有効フラグ |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uTeachingDataSelection_D | 軸1 ティーチングデータ選択 |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].uTeachingPositioningDataNo_D | 軸1 ティーチング位置決めデータNo. |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].udNewSpeed_D | 軸1 速度変更値 |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].udPV_NewSpeed_D | 軸1 位置・速度切換え制御速度変更レジスタ |
| 軸制御データ1 | FX5SSC_1.stnAxCtrl1_D[0].udVP_NewMovementAmount_D | 軸1 速度・位置切換え制御移動量変更レジスタ |
| システム制御データ | FX5SSC_1.stSysCtrl_D.wSSCNET_ControlCommand_D | SSCNET制御指令 |
| 軸制御データ2 | FX5SSC_1.stnAxCtrl2_D[0].uProhibitPositioning_D | 軸1 実行禁止フラグ |
| 軸制御データ2 | FX5SSC_1.stnAxCtrl2_D[0].uProhibitPositioning_D.0 | 軸1 実行禁止フラグ |
| 軸制御データ2 | FX5SSC_1.stnAxCtrl2_D[0].uStopAxis_D | 軸1 軸停止 |
| 軸制御データ2 | FX5SSC_1.stnAxCtrl2_D[0].uStopAxis_D.0 | 軸1 軸停止 |

※原本では「分類」列(入力信号，出力信号，パラメータ，軸モニタデータ，軸制御データ1，軸制御データ2)が結合セル。「内容」列の「同期用フラグ」「軸1 エラー検出」「軸1 始動完了」「軸1 実行禁止フラグ」「軸1 軸停止」がそれぞれ2行の結合セル。各行に展開。表は p.603 と p.604 にまたがり，p.604 で見出し行(分類／ラベル名／内容)が再掲されている。原本 p.604 では「軸制御データ1」の分類セルが dNewPosition_D～uSkip_D の12行と uStepMode_D～udVP_NewMovementAmount_D の8行の2つに分かれて記載されている(原文のまま2つとも「軸制御データ1」)。
※「FX5SSC_1.stnAxMntr[0].uStatus.D」「FX5SSC_1.stnAxMntr[0].uStatus.E」は，他の行と異なり「_D」なしの表記(原文のまま)。

#### グローバルラベル (12.3 / 原本 p.605-606)

プログラム例で使用しているグローバルラベルを示します。下記のようにグローバルラベルを設定してください。

- 割付けデバイスを設定しないグローバルラベル(割付けデバイスを設定していない場合，使用していない内部リレーやデータデバイスが自動で割り付けられます。)

【図】グローバルラベル設定画面(割付けデバイスを設定しないもの)(原本 p.605-606)。以下は画面キャプチャから書き起こした内容。

| No. | ラベル名 | データ型 | クラス | 割付け(デバイス/ラベル) | Japanese/日本語(表示対象) |
|---|---|---|---|---|---|
| 1 | bSetPositioningData_bEN | ビット | VAR_GLOBAL | (空欄) | 実行命令 |
| 2 | bSetPositioningData_bENO | ビット | VAR_GLOBAL | (空欄) | 実行状態 |
| 3 | bSetPositioningData_bOK | ビット | VAR_GLOBAL | (空欄) | 正常終了 |
| 4 | bSetPositioningData_bErr | ビット | VAR_GLOBAL | (空欄) | エラー終了 |
| 5 | uSetPositioningData_bErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | エラーコード |
| 6 | bJOG_bENO | ビット | VAR_GLOBAL | (空欄) | 実行状態 |
| 7 | bJOG_bOK | ビット | VAR_GLOBAL | (空欄) | 正常終了 |
| 8 | bJOG_bErr | ビット | VAR_GLOBAL | (空欄) | エラー終了 |
| 9 | uJOG_uErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | エラーコード |
| 10 | bMPG_bENO | ビット | VAR_GLOBAL | (空欄) | 実行状態 |
| 11 | bMPG_bOK | ビット | VAR_GLOBAL | (空欄) | 正常終了 |
| 12 | bMPG_bErr | ビット | VAR_GLOBAL | (空欄) | エラー終了 |
| 13 | uMPG_uErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | エラーコード |
| 14 | bChangeSpeed_bENO | ビット | VAR_GLOBAL | (空欄) | 実行状態 |
| 15 | bChangeSpeed_bOK | ビット | VAR_GLOBAL | (空欄) | 正常終了 |
| 16 | bChangeSpeed_bErr | ビット | VAR_GLOBAL | (空欄) | エラー終了 |
| 17 | uChangeSpeed_uErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | エラーコード |
| 18 | bChangeAccDecTime_bENO | ビット | VAR_GLOBAL | (空欄) | 実行状態 |
| 19 | bChangeAccDecTime_bOK | ビット | VAR_GLOBAL | (空欄) | 正常終了 |
| 20 | bChangeAccDecTime_bErr | ビット | VAR_GLOBAL | (空欄) | エラー終了 |
| 21 | uChangeAccDecTime_uErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | エラーコード |
| 22 | bChangePosition_bENO | ビット | VAR_GLOBAL | (空欄) | 実行状態 |
| 23 | bChangePosition_bOK | ビット | VAR_GLOBAL | (空欄) | 正常終了 |
| 24 | bChangePosition_bErr | ビット | VAR_GLOBAL | (空欄) | エラー終了 |
| 25 | uChangePosition_uErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | エラーコード |
| 26 | bRestart_bENO | ビット | VAR_GLOBAL | (空欄) | 実行状態 |
| 27 | bRestart_bOK | ビット | VAR_GLOBAL | (空欄) | 正常終了 |
| 28 | bRestart_bErr | ビット | VAR_GLOBAL | (空欄) | エラー終了 |
| 29 | uRestart_uErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | エラーコード |
| 30 | bInitializeParameter_bENO | ビット | VAR_GLOBAL | (空欄) | 実行状態 |
| 31 | bInitializeParameter_bOK | ビット | VAR_GLOBAL | (空欄) | 正常終了 |
| 32 | bInitializeParameter_bErr | ビット | VAR_GLOBAL | (空欄) | エラー終了 |
| 33 | uInitializeParameter_uErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | エラーコード |
| 34 | bOperateError_bENO | ビット | VAR_GLOBAL | (空欄) | 実行状態 |
| 35 | bOperateError_bOK | ビット | VAR_GLOBAL | (空欄) | 正常終了 |
| 36 | bOperateError_bModuleErr | ビット | VAR_GLOBAL | (空欄) | 軸エラー検出 |
| 37 | uOperateError_uModuleErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | 軸エラーコード |
| 38 | bOperateError_bModuleWarn | ビット | VAR_GLOBAL | (空欄) | 軸ワーニング検出 |
| 39 | uOperateError_bModuleWarnId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | 軸ワーニングコード |
| 40 | bOperateError_bErr | ビット | VAR_GLOBAL | (空欄) | エラー終了 |
| 41 | uOperateError_uErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | エラーコード |
| 42 | bWriteFlash_bENO | ビット | VAR_GLOBAL | (空欄) | 実行状態 |
| 43 | bWriteFlash_bOK | ビット | VAR_GLOBAL | (空欄) | 正常終了 |
| 44 | bWriteFlash_bErr | ビット | VAR_GLOBAL | (空欄) | エラー終了 |
| 45 | uWriteFlash_uErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | エラーコード |
| 46 | bBasicParamSetComp | ビット | VAR_GLOBAL | (空欄) | 基本パラメータ1設定完了 |
| 47 | bSetElectronicGear16bit | ビット | VAR_GLOBAL | (空欄) | 電子ギア(16bit)設定 |
| 48 | bOPRParamSetComp | ビット | VAR_GLOBAL | (空欄) | 原点復帰基本パラメータ設定完了 |
| 49 | uBlockData | ワード[符号なし]/ビット列[16ビット](0.4) | VAR_GLOBAL | (空欄) | ブロック始動データ(形態、始動データNo) |
| 50 | uBlockInstData | ワード[符号なし]/ビット列[16ビット](0.4) | VAR_GLOBAL | (空欄) | ブロック始動データ(特殊始動命令) |
| 51 | bOPRReqFlagOffReq_P | ビット | VAR_GLOBAL | (空欄) | 原点復帰要求OFF指令パルス |
| 52 | bOPRReqFlagOffReq_H | ビット | VAR_GLOBAL | (空欄) | 原点復帰要求OFF指令記憶 |
| 53 | bOPRReqFlagOffReq | ビット | VAR_GLOBAL | (空欄) | 原点復帰要求OFF指令 |
| 54 | udMovementAmount | ダブルワード[符号なし]/ビット列[32ビット] | VAR_GLOBAL | (空欄) | 速度・位置切換え制御移動量 |
| 55 | udSpeed | ダブルワード[符号付き] | VAR_GLOBAL | (空欄) | 位置・速度切換え制御速度 |
| 56 | bStartPositioning_bENO | ビット | VAR_GLOBAL | (空欄) | 実行状態 |
| 57 | bStartPositioning_bOK | ビット | VAR_GLOBAL | (空欄) | 正常終了 |
| 58 | bStartPositioning_bErr | ビット | VAR_GLOBAL | (空欄) | エラー終了 |
| 59 | uStartPositioning_uErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | エラーコード |
| 60 | bDuringMPGOperation | ビット | VAR_GLOBAL | (空欄) | 手動パルサ運転中フラグ |
| 61 | bFastStartPreparationComp | ビット | VAR_GLOBAL | (空欄) | 高速始動準備完了 |
| 62 | bFastOPRStartReq | ビット | VAR_GLOBAL | (空欄) | 高速原点復帰指令 |
| 63 | bFastOPRStartReq_H | ビット | VAR_GLOBAL | (空欄) | 高速原点復帰指令記憶 |
| 64 | bDuringJogInchingOperation | ビット | VAR_GLOBAL | (空欄) | JOG/インチング運転中フラグ |
| 65 | udJogOperationSpeed | ダブルワード[符号なし]/ビット列[32ビット] | VAR_GLOBAL | (空欄) | JOG運転速度 |
| 66 | uInchingMovementAmount | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | インチング移動量 |
| 67 | bChangeSpeedReq | ビット | VAR_GLOBAL | (空欄) | 速度変更指令 |
| 68 | bOverrideReq_P | ビット | VAR_GLOBAL | (空欄) | オーバライド指令パルス |
| 69 | bAccDecTimeChangeReq | ビット | VAR_GLOBAL | (空欄) | 加減速変更指令 |
| 70 | bChangeAccDecTime_jEnable | ビット | VAR_GLOBAL | (空欄) | 加減速時間変更許可フラグ |
| 71 | bStepOperationReq_P | ビット | VAR_GLOBAL | (空欄) | ステップ運転指令パルス |
| 72 | bChangeTorqueReq | ビット | VAR_GLOBAL | (空欄) | トルク変更指令 |
| 73 | bSkipReq_P | ビット | VAR_GLOBAL | (空欄) | スキップ指令パルス |
| 74 | bSkipReq | ビット | VAR_GLOBAL | (空欄) | スキップ指令 |
| 75 | bTeachingReq_P | ビット | VAR_GLOBAL | (空欄) | ティーチング指令パルス |
| 76 | bTeachingReq | ビット | VAR_GLOBAL | (空欄) | ティーチング指令 |
| 77 | uTeachingData | ワード[符号なし]/ビット列[16ビット](0.3) | VAR_GLOBAL | (空欄) | GP.TEACH1 命令用コントロールデータ |
| 78 | uTeachingDevice | ビット(0.1) | VAR_GLOBAL | (空欄) | GP.TEACH1 命令完了デバイス |
| 79 | uIO | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | IO番号(上位12bit) |
| 80 | bStopContinuousOperationReq_P | ビット | VAR_GLOBAL | (空欄) | 連続運転中断指令パルス |
| 81 | bTargetPositionChangeReq | ビット | VAR_GLOBAL | (空欄) | 目標位置変更指令 |
| 82 | bRestartReq | ビット | VAR_GLOBAL | (空欄) | 再始動指令 |
| 83 | bInitializeParameterReq | ビット | VAR_GLOBAL | (空欄) | パラメータ初期化指令 |
| 84 | bWriteFlashReq | ビット | VAR_GLOBAL | (空欄) | フラッシュROM書込み指令 |
| 85 | bErrResetReq | ビット | VAR_GLOBAL | (空欄) | エラーリセット指令 |
| 86 | bStopReq_P | ビット | VAR_GLOBAL | (空欄) | 停止指令 |
| 87 | bABRSTReq | ビット | VAR_GLOBAL | (空欄) | 絶対位置復元指令 |
| 88 | uOperateError_bModuleErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | 軸エラーコード |
| 89 | bErrReadReq | ビット | VAR_GLOBAL | (空欄) | エラー読出し指令 |
| 90 | bPositioningStartReq | ビット | VAR_GLOBAL | (空欄) | 位置決め始動指令 |
| 91 | bABRSTReq_P | ビット | VAR_GLOBAL | (空欄) | 絶対位置復元指令パルス |
| 92 | bABRST_bENO | ビット | VAR_GLOBAL | (空欄) | 実行状態 |
| 93 | bABRST_bOK | ビット | VAR_GLOBAL | (空欄) | 正常終了 |
| 94 | bABRST_bAbsNG | ビット | VAR_GLOBAL | (空欄) | ABSエラー |
| 95 | uABRST_uAbsErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | ABSエラーコード |
| 96 | bABRST_bErr | ビット | VAR_GLOBAL | (空欄) | エラー終了 |
| 97 | uABRST_uErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | エラーコード |
| 98 | bPosiStart10 | ビット | VAR_GLOBAL | (空欄) | デバッグ用位置決め始動 |
| 99 | uPositioningStartNo | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | 位置決め始動番号 |

※原本は GX Works3 のグローバルラベル設定画面のキャプチャ(No.1～85 が p.605，No.86～99 が p.606)。「データ型」列右の「...」ボタン列，「クラス」列のドロップダウン記号は省略。「割付け(デバイス/ラベル)」列はすべて空欄。データ型の「(0.4)」「(0.3)」「(0.1)」は画面上の表示のまま(配列範囲 0..4 等の意と思われるが画像の解像度上「.」が1つに見える。要確認)。
※No.5 は「uSetPositioningData_bErrId」，No.39 は「uOperateError_bModuleWarnId」，No.88 は「uOperateError_bModuleErrId」と画面上は表示(原文のまま)。No.70 は画面上「bChangeAccDecTime_jEnable」と読める(「_j」部分は解像度が低く要確認)。

- 割付けデバイスを設定するグローバルラベル

【図】グローバルラベル設定画面(割付けデバイスを設定するもの)(原本 p.606)。以下は画面キャプチャから書き起こした内容。

| No. | ラベル名 | データ型 | クラス | 割付け(デバイス/ラベル) | Japanese/日本語(表示対象) |
|---|---|---|---|---|---|
| 100 | bInputOPRReqFlagOffReq | ビット | VAR_GLOBAL | X0 | 原点復帰要求OFF指令 |
| 101 | bInputExternalCommandValidReq | ビット | VAR_GLOBAL | X1 | 外部指令有効指令 |
| 102 | bInputExternalCommandInvalidReq | ビット | VAR_GLOBAL | X2 | 外部指令無効指令 |
| 103 | bInputOPRStartReq | ビット | VAR_GLOBAL | X3 | 機械原点復帰指令 |
| 104 | bInputFastOPRStartReq | ビット | VAR_GLOBAL | X4 | 高速原点復帰指令 |
| 105 | bInputStartPositioningNoReq | ビット | VAR_GLOBAL | X5 | 位置決め始動指令 |
| 106 | bInputSpeedPositionSwitchingReq | ビット | VAR_GLOBAL | X6 | 速度・位置切換え運転指令 |
| 107 | bInputSpeedPositionSwitchingEnableReq | ビット | VAR_GLOBAL | X7 | 速度・位置切換え許可指令 |
| 108 | bInputSpeedPositionSwitchingDisableReq | ビット | VAR_GLOBAL | X10 | 速度・位置切換え禁止指令 |
| 109 | bInputChangeSpeedPositionSwitchingMovementAmount | ビット | VAR_GLOBAL | X11 | 移動量変更指令 |
| 110 | bInputStartAdvancedPositioningReq | ビット | VAR_GLOBAL | X12 | 高度な位置決め制御始動指令 |
| 111 | bInputMcodeOffReq | ビット | VAR_GLOBAL | X14 | MコードOFF要求 |
| 112 | bInputSetJogSpeedReq | ビット | VAR_GLOBAL | X15 | JOG運転速度設定指令 |
| 113 | bInputForwardJogStartReq | ビット | VAR_GLOBAL | X16 | 正転JOG/インチング指令 |
| 114 | bInputReverseJogStartReq | ビット | VAR_GLOBAL | X17 | 逆転JOG/インチング指令 |
| 115 | bInputStartMPGReq | ビット | VAR_GLOBAL | X20 | 手動パルサ運転指令 |
| 116 | bInputChangeSpeedReq | ビット | VAR_GLOBAL | X22 | 速度変更指令 |
| 117 | bInputOverrideReq | ビット | VAR_GLOBAL | X23 | オーバーライド指令 |
| 118 | bInputChangeAccDecTimeReq | ビット | VAR_GLOBAL | X24 | 加減速時間変更指令 |
| 119 | bInputChangeAccDecTimeDisable | ビット | VAR_GLOBAL | X25 | 加減速時間変更不許可指令 |
| 120 | bInputChangeTorqueReq | ビット | VAR_GLOBAL | X26 | トルク変更指令 |
| 121 | bInputStepOperationReq | ビット | VAR_GLOBAL | X27 | ステップ運転指令 |
| 122 | bInputSkipReq | ビット | VAR_GLOBAL | X30 | スキップ指令 |
| 123 | bInputTeachingReq | ビット | VAR_GLOBAL | X31 | ティーチング指令 |
| 124 | bInputStopContinuousOperationReq | ビット | VAR_GLOBAL | X32 | 連続運転中断指令 |
| 125 | bInputRestartReq | ビット | VAR_GLOBAL | X33 | 再始動指令 |
| 126 | bInputInitializeParameterReq | ビット | VAR_GLOBAL | X34 | パラメータ初期化指令 |
| 127 | bInputWriteFlashReq | ビット | VAR_GLOBAL | X35 | フラッシュROM書込み指令 |
| 128 | bInputErrResetReq | ビット | VAR_GLOBAL | X36 | エラーリセット指令 |
| 129 | bInputStopReq | ビット | VAR_GLOBAL | X37 | 停止指令 |
| 130 | bInputPositionSpeedSwitchingReq | ビット | VAR_GLOBAL | X40 | 位置・速度切換え運転指令 |
| 131 | bInputPositionSpeedSwitchingEnableReq | ビット | VAR_GLOBAL | X41 | 位置・速度切換え許可指令 |
| 132 | bInputPositionSpeedSwitchingDisableReq | ビット | VAR_GLOBAL | X42 | 位置・速度切換え禁止指令 |
| 133 | bInputChangePositionSpeedSwitchingSpeedReq | ビット | VAR_GLOBAL | X43 | 速度変更指令 |
| 134 | bInputSetInchingMovementAmountReq | ビット | VAR_GLOBAL | X44 | インチング移動量設定指令 |
| 135 | bInputTargetPositionChangeReq | ビット | VAR_GLOBAL | X45 | 目標位置変更指令 |
| 136 | bInputStepStartInformationReq | ビット | VAR_GLOBAL | X46 | ステップ始動情報指令 |
| 137 | bInputSpeedPositionSwitchingAbsSetReq | ビット | VAR_GLOBAL | X56 | 速度・位置切換え(ABS)設定指令 |
| 138 | bAllAxisServoOnReq | ビット | VAR_GLOBAL | X57 | 全軸サーボON指令 |

※原本は GX Works3 のグローバルラベル設定画面のキャプチャ。「...」ボタン列，ドロップダウン記号は省略。No.100～138 の「データ型」はすべて「ビット」，「クラス」はすべて「VAR_GLOBAL」。

### プログラム例(ラベル使用時) (12.3 / 原本 p.607-619)

ユニットFBの詳細は下記マニュアルの"シンプルモーションユニット／モーションユニットFB"を参照してください。
[別マニュアル]MELSEC iQ-F FX5モーションユニット／シンプルモーションユニットFBリファレンス

書き起こしの表記:
- ラダー図はニモニックで書き起こし，ステップ番号は原本のラダー図左端の番号。`;` 以降はラダー図中に表示されている割付けデバイス(U1¥G… は U1\G… と表記)。
- ユニットFB(ファンクションブロック)の呼出しはニモニックの1命令で表せないため，`FB` 行にFBインスタンス名を書き，入出力の接続を `//` 付きで列挙した(書き起こし用の表記)。
- 並列回路は MPS/MPP/ORB/ANB で表した(ラダー図の分岐構造を表すための書き起こし)。

#### パラメータ設定プログラム (12.3 / 原本 p.607)

エンジニアリングツールの"ユニットパラメータ"にてパラメータを設定する場合，本プログラムは不要です。

##### 基本パラメータ1(軸1)の設定 (12.3 / 原本 p.607)

```
(0)   LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1
      MOV   K0 FX5SSC_1.stnAxPrm_D[0].uUnit_D                   ; U1\G0
      MOV   K1 FX5SSC_1.stnAxPrm_D[0].uUnitMagnification_D      ; U1\G1
      DMOVP K4194304 FX5SSC_1.stnAxPrm_D[0].udPulsesPerRotation_D        ; U1\G2
      DMOVP K250000 FX5SSC_1.stnAxPrm_D[0].udMovementAmountPerRotation_D ; U1\G4
      SET   bBasicParamSetComp
```

##### 原点復帰基本パラメータ(軸1)の設定 (12.3 / 原本 p.607)

```
(75)  LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1
      MOVP  K0 FX5SSC_1.stnAxPrm_D[0].uHomingMethod_D           ; U1\G70
      MOVP  K0 FX5SSC_1.stnAxPrm_D[0].uHomingDirection_D        ; U1\G71
      DMOVP K0 FX5SSC_1.stnAxPrm_D[0].dHomePosition_D           ; U1\G72
      DMOVP K5000 FX5SSC_1.stnAxPrm_D[0].udHomingSpeed_D        ; U1\G74
      DMOVP K1500 FX5SSC_1.stnAxPrm_D[0].udCreepSpeed_D         ; U1\G76
      MOVP  K1 FX5SSC_1.stnAxPrm_D[0].uHomingRetry_D            ; U1\G78
      SET   bOPRParamSetComp
```

##### 単位degree用設定(軸1)プログラム (12.3 / 原本 p.607)

```
(146) LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1
      AND   bInputSpeedPositionSwitchingAbsSetReq               ; X56
      MOVP  K2 FX5SSC_1.stnAxPrm_D[0].uUnit_D                   ; U1\G0
      DMOVP K0 FX5SSC_1.stnAxPrm_D[0].dSoftwareStrokeUpperLimit_D ; U1\G18
      DMOVP K0 FX5SSC_1.stnAxPrm_D[0].dSoftwareStrokeLowerLimit_D ; U1\G20
      MOVP  K1 FX5SSC_1.stnAxPrm_D[0].uV_CommandPosition_D      ; U1\G30
      MOVP  K2 FX5SSC_1.stnAxPrm_D[0].uVP_Mode_D                ; U1\G34
```

- 接点種別(図から判読): p.607 の3回路の FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D 接点は，a接点(X56 等)と異なり接点記号の中央に縦線がある表示で，p.608 の同じラベルの立上り(↑)接点と同形のため LDP(立上りパルス)と判読。画像が小さく矢印の向きは直接判読できないため要確認(原本 p.607 参照)。X56 は a接点。
- 基本パラメータ1の設定の出力は，ラダー図上 MOV(非パルス)×2，DMOVP×2，SET(原文のまま)。

#### 位置決めデータ設定プログラム (12.3 / 原本 p.608)

エンジニアリングツールの"位置決めデータ"にて設定する場合，本プログラムは不要です。

```
(0)   LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1
      MOV   K0 M_FX5SSC_SetPositioningData_01A_1.pb_uOpePattern
      MOV   H1 M_FX5SSC_SetPositioningData_01A_1.pb_uCtrlSys
      MOV   K1 M_FX5SSC_SetPositioningData_01A_1.pb_uAccTimeNo
      MOV   K2 M_FX5SSC_SetPositioningData_01A_1.pb_uDecTimeNo
      MOV   K9843 M_FX5SSC_SetPositioningData_01A_1.pb_uMcode
      MOV   K300 M_FX5SSC_SetPositioningData_01A_1.pb_uDwellTime
      DMOV  K18000 M_FX5SSC_SetPositioningData_01A_1.pb_udCmdSpd
      DMOV  K4126 M_FX5SSC_SetPositioningData_01A_1.pb_dPositAdr
      DMOV  K0 M_FX5SSC_SetPositioningData_01A_1.pb_dArcAdr
      MOV   K0 M_FX5SSC_SetPositioningData_01A_1.pb_uInterpolationAxisNo1
      MOV   K0 M_FX5SSC_SetPositioningData_01A_1.pb_uInterpolationAxisNo2
      MOV   K0 M_FX5SSC_SetPositioningData_01A_1.pb_uInterpolationAxisNo3
      SET   bSetPositioningData_bEN
(58)  LD    bSetPositioningData_bEN
      FB    M_FX5SSC_SetPositioningData_01A_1
      // FBタイトル: M_FX5SSC_SetPositioningData_01A_1 (M+FX5SSC_SetPositioningData_01A) Positioning data setting FB
      // 入力 B: i_bEN        ← bSetPositioningData_bEN (上記a接点)
      // 入力 DUT: i_stModule ← FX5SSC_1
      // 入力 UW: i_uAxis     ← K1
      // 入力 UW: i_uDataNo   ← K1
      // 出力 o_bENO :B       → bSetPositioningData_bENO (コイル)
      // 出力 o_bOK :B        → bSetPositioningData_bOK (コイル)
      // 出力 o_bErr :B       → bSetPositioningData_bErr (コイル)
      // 出力 o_uErrId :UW    → uSetPositioningData_bErrId
      // FB内の公開変数表示: pb_uOpePattern, pb_uCtrlSys, pb_uAccTimeNo, pb_uDecTimeNo, pb_uMcode, pb_uDwellTime, pb_udCmdSpd, pb_dPositAdr, pb_dArcAdr, pb_uInterpolationAxisNo1, pb_uInterpolationAxisNo2, pb_uInterpolationAxisNo3
```

- 接点種別(図から判読): (0) の bSynchronizationFlag_D は立上り(↑)接点，(58) の bSetPositioningData_bEN は a接点。

#### ブロック始動データ設定プログラム (12.3 / 原本 p.609)

エンジニアリングツールの"ブロック始動データ"にて設定する場合，本プログラムは不要です。

```
(0)   LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1
      MOVP  H8001 uBlockData[0]
      MOVP  H8002 uBlockData[1]
      MOVP  H8005 uBlockData[2]
      MOVP  H800A uBlockData[3]
      MOVP  H0F uBlockData[4]
      TOP   FX5SSC_1.uIO K22000 uBlockData[0] K5            ; FX5SSC_1.uIO = H1
(50)  LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1
      MOVP  H0 uBlockInstData[0]
      MOVP  H0 uBlockInstData[1]
      MOVP  H0 uBlockInstData[2]
      MOVP  H0 uBlockInstData[3]
      MOVP  H0 uBlockInstData[4]
      TOP   FX5SSC_1.uIO K22050 uBlockInstData[0] K5        ; FX5SSC_1.uIO = H1
```

- 接点種別(図から判読): (0)，(50) の bSynchronizationFlag_D 接点は p.607 と同じく中央に縦線のある表示で LDP と判読(矢印の向きは画像から直接判読できず要確認)。
- TOP 命令の第1オペランド欄には「FX5SSC_1.uIO」とその下に「H1」が表示されている。

#### サーボパラメータ設定プログラム (12.3 / 原本 p.609)

エンジニアリングツールの"サーボパラメータ"にて設定する場合，本プログラムは不要です。

```
(746) LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1
      TOP   FX5SSC_1.uIO K28403 H1 K1                       ; FX5SSC_1.uIO = H1
      TOP   FX5SSC_1.uIO K28400 K32 K1                      ; FX5SSC_1.uIO = H1
```

- ステップ番号は原本では「(74」「6)」と2行に折り返して表示。
- 接点種別(図から判読): bSynchronizationFlag_D 接点は中央に縦線のある表示で LDP と判読(要確認)。

#### 原点復帰要求OFFプログラム (12.3 / 原本 p.610)

エンジニアリングツールの"原点復帰詳細パラメータ"にて"[Pr.55]原点復帰未完時操作設定"を「1: 位置決め制御を実行する」に設定した場合，本プログラムは不要です。

```
(785) LD    bInputOPRReqFlagOffReq                             ; X0
      PLS   bInputForwardJogStartReq                           ; X16
(812) LD    bInputForwardJogStartReq                           ; X16
      ANI   FX5SSC_1.stnAxCtrl2_D[0].uPositioningStart_D.0     ; U1\G30104.0
      ANI   FX5SSC_1.stnAxMntr_D[0].uStatus_D.E                ; U1\G2417.E
      SET   bOPRReqFlagOffReq_H
(823) LD    bOPRReqFlagOffReq_H
      MPS
      AND   FX5SSC_1.stnAxMntr_D[0].uStatus_D.3                ; U1\G2417.3
      SET   bOPRReqFlagOffReq
      MPP
      RST   bOPRReqFlagOffReq_H
(837) LD    bOPRReqFlagOffReq
      MOVP  K1 FX5SSC_1.stnAxCtrl1_D[0].uClearHomingRequestFlag_D   ; U1\G4321
      AND=_U K0 FX5SSC_1.stnAxCtrl1_D[0].uClearHomingRequestFlag_D  ; U1\G4321
      RST   bOPRReqFlagOffReq
```

- (785) の PLS 出力先，(812) の先頭接点はラダー図上「bInputForwardJogStartReq」「X16」と表示(原文のまま。グローバルラベル一覧では bOPRReqFlagOffReq_P が「原点復帰要求OFF指令パルス」として定義されている。要確認)。
- (823) は bOPRReqFlagOffReq_H の直後で2分岐: 上段 uStatus_D.3(a接点) → SET bOPRReqFlagOffReq，下段 → RST bOPRReqFlagOffReq_H。
- (837) は bOPRReqFlagOffReq の直後で2分岐: 上段 → MOVP K1，下段 比較命令「=_U K0 …uClearHomingRequestFlag_D」 → RST bOPRReqFlagOffReq。
- 接点種別(図から判読): (812) の uPositioningStart_D.0 と uStatus_D.E は b接点，他は a接点。

#### 外部指令機能有効設定プログラム (12.3 / 原本 p.610)

```
(855) LD    bInputExternalCommandValidReq                      ; X1
      MOVP  K1 FX5SSC_1.stnAxCtrl1_D[0].uExternalCommandValid_D ; U1\G4305
(881) LD    bInputExternalCommandInvalidReq                    ; X2
      MOVP  K0 FX5SSC_1.stnAxCtrl1_D[0].uExternalCommandValid_D ; U1\G4305
```

#### シーケンサレディ信号ONプログラム (12.3 / 原本 p.610)

```
(889) LD    FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1
      AND   bBasicParamSetComp
      AND   bOPRParamSetComp
      ANI   bInitializeParameterReq
      ANI   bWriteFlashReq
      OUT   FX5SSC_1.stSysCtrl_D.bPLC_Ready_D                  ; U1\G5950.0
```

- 接点種別(図から判読): bSynchronizationFlag_D，bBasicParamSetComp，bOPRParamSetComp は a接点，bInitializeParameterReq，bWriteFlashReq は b接点。

#### 全軸サーボONプログラム (12.3 / 原本 p.610)

```
(930) LD    bAllAxisServoOnReq                                 ; X57
      AND   FX5SSC_1.stSysCtrl_D.bPLC_Ready_D                  ; U1\G5950.0
      AND   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1
      OUT   FX5SSC_1.stSysCtrl_D.bAllAxisServoOn_D             ; U1\G5951.0
```

#### 位置決め始動番号設定プログラム (12.3 / 原本 p.611-612)

##### 機械原点復帰 (12.3 / 原本 p.611)

```
(961) LD    bInputOPRStartReq                                  ; X3
      MOVP  K9001 uPositioningStartNo
```

##### 高速原点復帰 (12.3 / 原本 p.611)

```
(1005) LD   bInputFastOPRStartReq                              ; X4
      MPS
      ANI   FX5SSC_1.stnAxMntr_D[0].uStatus_D.3                ; U1\G2417.3
      SET   bFastOPRStartReq
      MPP
      MOVP  K9002 uPositioningStartNo
      SET   bFastOPRStartReq_H
```

- X4 の直後で3分岐: 上段 uStatus_D.3(b接点) → SET bFastOPRStartReq，中段 → MOVP K9002 uPositioningStartNo，下段 → SET bFastOPRStartReq_H。

##### 位置決めデータNo.1による位置決め (12.3 / 原本 p.611)

```
(1037) LD   bInputStartPositioningNoReq                        ; X5
      MOVP  K1 uPositioningStartNo
```

##### 速度・位置切換え制御(位置決めデータNo.2) (12.3 / 原本 p.611)

ABSモードの場合，変更後の移動量書込みは不要です。

```
(1071) LD   bInputSpeedPositionSwitchingReq                    ; X6
      MOVP  K2 uPositioningStartNo
(1110) LD   bInputSpeedPositionSwitchingEnableReq              ; X7
      MOVP  K1 FX5SSC_1.stnAxCtrl1_D[0].uEnableVP_Switching_D  ; U1\G4328
(1118) LD   bInputSpeedPositionSwitchingDisableReq             ; X10
      MOVP  K0 FX5SSC_1.stnAxCtrl1_D[0].uEnableVP_Switching_D  ; U1\G4328
(1126) LD   bInputChangeSpeedPositionSwitchingMovementAmount   ; X11
      DMOVP udMovementAmount FX5SSC_1.stnAxCtrl1_D[0].udVP_NewMovementAmount_D ; U1\G4326
```

##### 位置・速度切換え制御(位置決めデータNo.3) (12.3 / 原本 p.611)

```
(1136) LD   bInputPositionSpeedSwitchingReq                    ; X40
      MOVP  K3 uPositioningStartNo
(1175) LD   bInputPositionSpeedSwitchingEnableReq              ; X41
      MOVP  K1 FX5SSC_1.stnAxCtrl1_D[0].uEnablePV_Switching_D  ; U1\G4332
(1183) LD   bInputPositionSpeedSwitchingDisableReq             ; X42
      MOVP  K0 FX5SSC_1.stnAxCtrl1_D[0].uEnablePV_Switching_D  ; U1\G4332
(1191) LD   bInputChangePositionSpeedSwitchingSpeedReq         ; X43
      DMOVP udSpeed FX5SSC_1.stnAxCtrl1_D[0].udPV_NewSpeed_D   ; U1\G4330
```

##### 高度な位置決め制御 (12.3 / 原本 p.611)

```
(1201) LD   bInputStartAdvancedPositioningReq                  ; X12
      MOVP  K7000 uPositioningStartNo
```

##### 高速原点復帰指令，高速原点復帰指令記憶のOFF (12.3 / 原本 p.612)

高速原点復帰を使用しない場合は不要です。

```
(1225) LD   bInputOPRStartReq                                  ; X3
      OR    bInputStartPositioningNoReq                        ; X5
      OR    bInputSpeedPositionSwitchingReq                    ; X6
      OR    bInputPositionSpeedSwitchingReq                    ; X40
      OR    bInputStartAdvancedPositioningReq                  ; X12
      OR    bPositioningStartReq
      RST   bFastOPRStartReq
      RST   bFastOPRStartReq_H
```

#### 位置決め始動プログラム (12.3 / 原本 p.612)

```
(0)   LDP   bInputStartPositioningNoReq                        ; X5
      ANI   bDuringJogInchingOperation
      ANI   bDuringMPGOperation
      LDI   bFastOPRStartReq
      LD    bFastOPRStartReq
      AND   bFastOPRStartReq_H
      ORB
      ANB
      SET   bPositioningStartReq
(24)  LD    bPositioningStartReq
      LD    FX5SSC_1.stnAxMntr_D[0].uStatus_D.F                ; U1\G2417.F
      OR    FX5SSC_1.stnAxMntr_D[0].uStatus_D.D                ; U1\G2417.D
      ANB
      ANI   FX5SSC_1.stSysMntr2_D.bnBusy_D[0]                  ; U1\G31501.0
      RST   bPositioningStartReq
(40)  LD    bPositioningStartReq
      FB    M_FX5SSC_StartPositioning_01A_1
      // FBタイトル: M_FX5SSC_StartPositioning_01A_1 (M+FX5SSC_StartPositioning_01A) Positioning start FB
      // 入力 B: i_bEN        ← bPositioningStartReq (上記a接点)
      // 入力 DUT: i_stModule ← FX5SSC_1
      // 入力 UW: i_uAxis     ← K1
      // 入力 UW: i_uStartNo  ← uPositioningStartNo
      // 出力 o_bENO :B       → bStartPositioning_bENO (コイル)
      // 出力 o_bOK :B        → bStartPositioning_bOK (コイル)
      // 出力 o_bErr :B       → bStartPositioning_bErr (コイル)
      // 出力 o_uErrId :UW    → uStartPositioning_uErrId
```

- 接点種別(図から判読): (0) の bInputStartPositioningNoReq(X5) は立上り(↑)接点，bDuringJogInchingOperation，bDuringMPGOperation，上段の bFastOPRStartReq は b接点，下段の bFastOPRStartReq と bFastOPRStartReq_H は a接点。(24) の bnBusy_D[0] は b接点，他は a接点。
- (0) は bDuringMPGOperation の後で「bFastOPRStartReq(b接点)」と「bFastOPRStartReq(a接点)－bFastOPRStartReq_H(a接点)の直列」の並列ブロックとなり SET bPositioningStartReq へ。
- (24) は bPositioningStartReq の後で「uStatus_D.F(位置決め完了)」と「uStatus_D.D(エラー検出)」の並列，続いて bnBusy_D[0] の b接点で RST bPositioningStartReq。
- 位置決め始動プログラムのステップ番号は (0) から始まる(原文のまま)。

#### MコードOFFプログラム (12.3 / 原本 p.612)

```
(1870) LD   bInputMcodeOffReq                                  ; X14
      AND   FX5SSC_1.stnAxMntr_D[0].uStatus_D.C                ; U1\G2417.C
      MOVP  K1 FX5SSC_1.stnAxCtrl1_D[0].uClear_M_Code_D        ; U1\G4304
```

#### JOG運転設定プログラム (12.3 / 原本 p.613)

```
(1904) LD   bInputSetJogSpeedReq(X15)
       DMOVP K10000 udJogOperationSpeed
       MOVP K0 uInchingMovementAmount
```

#### インチング運転設定プログラム (12.3 / 原本 p.613)

```
(1942) LD   bInputSetInchingMovementAmountReq(X44)
       MOVP K10 uInchingMovementAmount
```

#### JOG運転／インチング運転実行プログラム (12.3 / 原本 p.613)

```
(0)   LD   bInputForwardJogStartReq(X16)
      OR   bInputReverseJogStartReq(X17)
      AND  FX5SSC_1.stSysMntr2_D.bReady_D(U1\G31500.0)
      ANI  FX5SSC_1.stSysMntr2_D.bnBusy_D[0](U1\G31501.0)
      SET  bDuringJogInchingOperation
(13)  // FBインスタンス M_FX5SSC_JOG_01A_1 (M+FX5SSC_JOG_01A)  JOG/inching operation FB
      LD   bDuringJogInchingOperation            -> B: i_bEN
      [FX5SSC_1]                                  -> DUT: i_stModule
      [K1]                                        -> UW: i_uAxis
      LD   bInputForwardJogStartReq(X16)          -> B: i_bFJog
      LD   bInputReverseJogStartReq(X17)          -> B: i_bRJog
      [udJogOperationSpeed]                       -> UD: i_udJogSpeed
      [K0]                                        -> UW: i_uInching
      o_bENO :B   -> OUT bJOG_bENO
      o_bOK :B    -> OUT bJOG_bOK
      o_bErr :B   -> OUT bJOG_bErr
      o_uErrId :UW -> [uJOG_uErrId]
(280) LDI  bInputForwardJogStartReq(X16)
      ANI  bInputReverseJogStartReq(X17)
      RST  bDuringJogInchingOperation
```

> 表記注(本断片のラダー): 接点・コイルは「ラベル名(割付デバイス)」で表記。FB呼出し(FBインスタンス)はニモニック1命令で表せないため、`// FBインスタンス` 行の下に各入力ピンへの接続(`LD 接点 -> ピン` または `[定数/ラベル] -> ピン`)と各出力ピンの接続先(`ピン -> OUT コイル` / `ピン -> [ラベル]`)を並べて書く。

#### 手動パルサ運転プログラム (12.3 / 原本 p.614)

```
(0)   LDP  bInputStartMPGReq(X20)
      AND  FX5SSC_1.stSysMntr2_D.bReady_D(U1\G31500.0)
      ANI  FX5SSC_1.stSysMntr2_D.bnBusy_D[0](U1\G31501.0)
      SET  bDuringMPGOperation
(13)  LDF  bInputStartMPGReq(X20)
      RST  bDuringMPGOperation
(20)  // FBインスタンス M_FX5SSC_MPG_01A_1 (M+FX5SSC_MPG_01A)  Manual pulse generator OP FB
      LD   bDuringMPGOperation                    -> B: i_bEN
      [FX5SSC_1]                                  -> DUT: i_stModule
      [K1]                                        -> UW: i_uAxis
      [K1]                                        -> UD: i_udMPGInputMagnification
      o_bENO :B   -> OUT bMPG_bENO
      o_bOK :B    -> OUT bMPG_bOK
      o_bErr :B   -> OUT bMPG_bErr
      o_uErrId :UW -> [uMPG_uErrId]
```

#### 速度変更プログラム (12.3 / 原本 p.614)

```
(0)   LDP  bInputChangeSpeedReq(X22)
      ANI  FX5SSC_1.stSysMntr2_D.bnBusy_D[0](U1\G31501.0)
      SET  bChangeSpeedReq
(10)  LD   bChangeSpeed_bOK
      RST  bChangeSpeedReq
(16)  // FBインスタンス M_FX5SSC_ChangeSpeed_01A_1 (M+FX5SSC_ChangeSpeed_01A)  Speed change FB
      LD   bChangeSpeedReq                        -> B: i_bEN
      [FX5SSC_1]                                  -> DUT: i_stModule
      [K1]                                        -> UW: i_uAxis
      [K20000]                                    -> UD: i_udSpeedChangeValue
      o_bENO :B   -> OUT bChangeSpeed_bENO
      o_bOK :B    -> OUT bChangeSpeed_bOK
      o_bErr :B   -> OUT bChangeSpeed_bErr
      o_uErrId :UW -> [uChangeSpeed_uErrId]
```

#### オーバーライドプログラム (12.3 / 原本 p.614)

```
(0)   LD   bInputOverrideReq(X23)
      PLS  bOverrideReq_P
(5)   LD   bOverrideReq_P
      AND  FX5SSC_1.stSysMntr2_D.bnBusy_D[0](U1\G31501.0)
      MOVP K200 FX5SSC_1.stnAxCtrl1_D[0].uOverride_D(U1\G4313)
```

#### 加減速時間変更プログラム (12.3 / 原本 p.615)

```
(0)   LDI  bInputChangeAccDecTimeDisable(X25)
      OUT  bChangeAccDecTime_iEnable
(5)   // FBインスタンス M_FX5SSC_ChangeAccDecTime_01A_1 (M+FX5SSC_ChangeAccDecTime_01A)  Acc./dec. time SV change FB
      LD   bInputChangeAccDecTimeReq(X24)         -> B: i_bEN
      [FX5SSC_1]                                  -> DUT: i_stModule
      [K1]                                        -> UW: i_uAxis
      LD   bChangeAccDecTime_iEnable              -> B: i_bEnable
      [K2000]                                     -> UD: i_udNewAccelerationTime
      [K0]                                        -> UD: i_udNewDecelerationTime
      o_bENO :B   -> OUT bChangeAccDecTime_bENO
      o_bOK :B    -> OUT bChangeAccDecTime_bOK
      o_bErr :B   -> OUT bChangeAccDecTime_bErr
      o_uErrId :UW -> [uChangeAccDecTime_uErrId]
```

#### トルク変更プログラム (12.3 / 原本 p.615)

```
(3493) LD   bInputChangeTorqueReq(X26)
       PLS  bChangeTorqueReq
(3516) LD   bChangeTorqueReq
       AND  FX5SSC_1.stSysMntr2_D.bnBusy_D[0](U1\G31501.0)
       MOV  K1000 FX5SSC_1.stnAxCtrl1_D[0].uForwardNewTorque_D(U1\G4325)
```

#### ステップ運転プログラム (12.3 / 原本 p.615)

```
(3528) LD   bInputStepOperationReq(X27)
       PLS  bStepOperationReq_P
(3554) LD   bStepOperationReq_P
       ANI  FX5SSC_1.stnAxCtrl2_D[0].uPositioningStart_D.0(U1\G30104.0)
       ANI  FX5SSC_1.stnAxMntr_D[0].uStatus_D.E(U1\G2417.E)
       MOV  K1 FX5SSC_1.stnAxCtrl1_D[0].uStepMode_D(U1\G4344)
       MOV  K1 FX5SSC_1.stnAxCtrl1_D[0].uStepValid_D(U1\G4345)
(3575) LD   bInputStepStartInformationReq(X46)
       MOVP K1 FX5SSC_1.stnAxCtrl1_D[0].uStepStartInformation_D(U1\G4346)
```

#### スキッププログラム (12.3 / 原本 p.616)

```
(3583) LD   bInputSkipReq(X30)
       PLS  bSkipReq_P
(3608) LD   bSkipReq_P
       AND  FX5SSC_1.stSysMntr2_D.bnBusy_D[0](U1\G31501.0)
       SET  bSkipReq
(3617) LD   bSkipReq
       MPS
       MOVP K1 FX5SSC_1.stnAxCtrl1_D[0].uSkip_D(U1\G4347)
       MPP
       AND=_U FX5SSC_1.stnAxCtrl1_D[0].uSkip_D(U1\G4347) K0
       RST  bSkipReq
```

#### ティーチングプログラム (12.3 / 原本 p.616)

```
(3635) LD   bInputTeachingReq(X31)
       PLS  bTeachingReq_P
(3660) LD   bTeachingReq_P
       ANI  FX5SSC_1.stSysMntr2_D.bnBusy_D[0](U1\G31501.0)
       SET  bTeachingReq
(3669) LD   bTeachingReq
       MPS
       MOVP K0 FX5SSC_1.stnAxCtrl1_D[0].uTeachingDataSelection_D(U1\G4348)
       MRD
       MOVP K1 FX5SSC_1.stnAxCtrl1_D[0].uTeachingPositioningDataNo_D(U1\G4349)
       MPP
       AND=_U FX5SSC_1.stnAxCtrl1_D[0].uTeachingPositioningDataNo_D(U1\G4349) K0
       RST  bTeachingReq
```

#### 連続運転中断プログラム (12.3 / 原本 p.616)

```
(3693) LD   bInputStopContinuousOperationReq(X32)
       PLS  bStopContinuousOperationReq_P
(3720) LD   bStopContinuousOperationReq_P
       AND  FX5SSC_1.stSysMntr2_D.bnBusy_D[0](U1\G31501.0)
       MOV  K1 FX5SSC_1.stnAxCtrl1_D[0].uInterruptOperation_D(U1\G4320)
```

#### 目標位置変更プログラム (12.3 / 原本 p.617)

```
(0)   LDP  bInputTargetPositionChangeReq(X45)
      AND  FX5SSC_1.stSysMntr2_D.bnBusy_D[0](U1\G31501.0)
      SET  bTargetPositionChangeReq
(10)  // FBインスタンス M_FX5SSC_ChangePosition_01A_1 (M+FX5SSC_ChangePosition_01A)  Target position change FB
      LD   bTargetPositionChangeReq               -> B: i_bEN
      [FX5SSC_1]                                  -> DUT: i_stModule
      [K1]                                        -> UW: i_uAxis
      [K3000]                                     -> D: i_dTargetNewPosition
      [K1000000]                                  -> UD: i_udTargetNewSpeed
      o_bENO :B   -> OUT bChangeAccDecTime_bENO
      o_bOK :B    -> OUT bChangeAccDecTime_bOK
      o_bErr :B   -> OUT bChangeAccDecTime_bErr
      o_uErrId :UW -> [uChangeAccDecTime_uErrId]
(199) LD   bChangePosition_bOK
      RST  bTargetPositionChangeReq
```

> 転記注: 原本の図では、このFBの出力ラベルが bChangeAccDecTime_bENO／bChangeAccDecTime_bOK／bChangeAccDecTime_bErr／uChangeAccDecTime_uErrId と記載され、ステップ(199)の接点は bChangePosition_bOK と記載されている(原本 p.617 のとおり転記。要確認)。

#### 再始動プログラム (12.3 / 原本 p.617)

```
(0)   LDP  bInputRestartReq(X33)
      SET  bRestartReq
(7)   LD   bRestart_bOK
      RST  bRestartReq
(13)  // FBインスタンス M_FX5SSC_Restart_01A_1 (M+FX5SSC_Restart_01A)  Restart FB
      LD   bRestartReq                            -> B: i_bEN
      [FX5SSC_1]                                  -> DUT: i_stModule
      [K1]                                        -> UW: i_uAxis
      o_bENO :B   -> OUT bRestart_bENO
      o_bOK :B    -> OUT bRestart_bOK
      o_bErr :B   -> OUT bRestart_bErr
      o_uErrId :UW -> [uRestart_uErrId]
```

#### パラメータ初期化プログラム (12.3 / 原本 p.618)

```
(0)   LDP  bInputInitializeParameterReq(X34)
      SET  bInitializeParameterReq
(7)   LD   bInitializeParameter_bOK
      RST  bInitializeParameterReq
(13)  // FBインスタンス M_FX5SSC_InitializeParameter_00A_1 (M+FX5SSC_InitializeParameter_00A)  Parameter Initialization FB
      LD   bInitializeParameterReq                -> B: i_bEN
      [FX5SSC_1]                                  -> DUT: i_stModule
      o_bENO :B   -> OUT bInitializeParameter_bENO
      o_bOK :B    -> OUT bInitializeParameter_bOK
      o_bErr :B   -> OUT bInitializeParameter_bErr
      o_uErrId :UW -> [uInitializeParameter_uErrId]
```

#### フラッシュ ROM書込みプログラム (12.3 / 原本 p.618)

```
(0)   LDP  bInputWriteFlashReq(X35)
      SET  bWriteFlashReq
(7)   LD   bInitializeParameter_bOK
      RST  bWriteFlashReq
(13)  // FBインスタンス M_FX5SSC_WriteFlash_00A_1 (M+FX5SSC_WriteFlash_00A)  Flash ROM writing FB
      LD   bWriteFlashReq                         -> B: i_bEN
      [FX5SSC_1]                                  -> DUT: i_stModule
      o_bENO :B   -> OUT bWriteFlash_bENO
      o_bOK :B    -> OUT bWriteFlash_bOK
      o_bErr :B   -> OUT bWriteFlash_bErr
      o_uErrId :UW -> [uWriteFlash_uErrId]
```

> 転記注: ステップ(7)の接点は原本 p.618 の図で bInitializeParameter_bOK と記載されている(bWriteFlash_bOK ではない。原本のとおり転記。要確認)。

#### エラーリセットプログラム (12.3 / 原本 p.619)

```
(0)   LD   FX5SSC_1.stnAxMntr_D[0].uStatus_D.D(U1\G2417.D)
      OR   FX5SSC_1.stnAxMntr_D[0].uStatus_D.9(U1\G2417.9)
      OUT  bErrReadReq
(9)   LD   bInputErrResetReq(X36)
      RST  bErrResetReq
(14)  // FBインスタンス M_FX5SSC_OperateError_01A_1 (M+FX5SSC_OperateError_01A)  Error operation FB
      LD   bErrReadReq                            -> B: i_bEN
      [FX5SSC_1]                                  -> DUT: i_stModule
      [K1]                                        -> UW: i_uAxis
      LD   bErrResetReq                           -> B: i_bErrReset
      o_bENO :B          -> OUT bOperateError_bENO
      o_bOK :B           -> OUT bOperateError_bOK
      o_bModuleErr :B    -> OUT bOperateError_bModuleErr
      o_uModuleErrId :UW -> [uOperateError_bModuleErrId]
      o_bModuleWarn :B   -> OUT bOperateError_bModuleWarn
      o_uModuleWarnId :UW -> [uOperateError_bModuleWarnId]
      o_bErr :B          -> OUT bOperateError_bErr
      o_uErrId :UW       -> [uOperateError_uErrId]
```

> 転記注: ステップ(9)は原本 p.619 の図で X36(a接点)→ RST bErrResetReq と記載されている(原本のとおり転記)。

#### 軸停止プログラム (12.3 / 原本 p.619)

```
(4783) LD   bInputStopReq(X37)
       PLS  bStopReq_P
(4804) LD   bStopReq_P
       SET  FX5SSC_1.stnAxCtrl2_D[0].uStopAxis_D.0(U1\G30100.0)
(4810) LDI  bInputStopReq(X37)
       RST  FX5SSC_1.stnAxCtrl2_D[0].uStopAxis_D.0(U1\G30100.0)
```

## 12.4 位置決めプログラム例(バッファメモリ使用時) (12.4 / 原本 p.620-652)

### 使用するデバイス一覧 (12.4 / 原本 p.620-626)

バッファメモリ使用時のプログラム例では，使用するデバイスを以下のように割り付けています。
ユニットアクセスデバイス，外部入力，内部リレー，データレジスタ，タイマは，使用するシステムに合わせ変更してください。

#### シンプルモーションユニットのバッファメモリアドレス，外部入力，内部リレー (12.4 / 原本 p.620-622)

| デバイス名称 | 軸1 | 軸2 | 軸3 | 軸4 | 用途 | デバイスON時の内容 |
|---|---|---|---|---|---|---|
| シンプルモーションユニットのバッファメモリアドレス | U1\G31500.0 | U1\G31500.0 | U1\G31500.0 | U1\G31500.0 | 準備完了信号 | 準備完了 |
| シンプルモーションユニットのバッファメモリアドレス | U1\G31500.1 | U1\G31500.1 | U1\G31500.1 | U1\G31500.1 | 同期用フラグ | バッファメモリアクセス可 |
| シンプルモーションユニットのバッファメモリアドレス | U1\G2417.C | — | — | — | MコードON信号 | Mコード出力中 |
| シンプルモーションユニットのバッファメモリアドレス | U1\G2417.D | — | — | — | エラー検出信号 | エラー検出 |
| シンプルモーションユニットのバッファメモリアドレス | U1\G31501.0 | — | — | — | BUSY信号 | BUSY(運転中) |
| シンプルモーションユニットのバッファメモリアドレス | U1\G2417.E | — | — | — | 始動完了信号 | 始動完了 |
| シンプルモーションユニットのバッファメモリアドレス | U1\G2417.F | — | — | — | 位置決め完了信号 | 位置決め完了 |
| シンプルモーションユニットのバッファメモリアドレス | U1\G5950 | U1\G5950 | U1\G5950 | U1\G5950 | シーケンサレディ信号 | CPUユニット準備完了 |
| シンプルモーションユニットのバッファメモリアドレス | U1\G5951 | U1\G5951 | U1\G5951 | U1\G5951 | 全軸サーボON信号 | 全軸サーボON |
| シンプルモーションユニットのバッファメモリアドレス | U1\G30100 | — | — | — | 軸停止信号 | 停止要求中 |
| シンプルモーションユニットのバッファメモリアドレス | U1\G30101 | — | — | — | 正転JOG始動信号 | 正転JOG始動中 |
| シンプルモーションユニットのバッファメモリアドレス | U1\G30102 | — | — | — | 逆転JOG始動信号 | 逆転JOG始動中 |
| シンプルモーションユニットのバッファメモリアドレス | U1\G30103 | — | — | — | 実行禁止要求 | 実行禁止 |
| シンプルモーションユニットのバッファメモリアドレス | U1\G30104 | — | — | — | 位置決め始動信号 | 始動要求中 |
| 外部入力(指令) | X0 | — | — | — | 原点復帰要求OFF指令 | 原点復帰要求OFF指令中 |
| 外部入力(指令) | X1 | — | — | — | 外部指令有効指令 | 外部指令有効設定指令中 |
| 外部入力(指令) | X2 | — | — | — | 外部指令無効指令 | 外部指令無効指令中 |
| 外部入力(指令) | X3 | — | — | — | 機械原点復帰指令 | 機械原点復帰指令中 |
| 外部入力(指令) | X4 | — | — | — | 高速原点復帰指令 | 高速原点復帰指令中 |
| 外部入力(指令) | X5 | — | — | — | 位置決め始動指令 | 位置決め始動指令中 |
| 外部入力(指令) | X6 | — | — | — | 速度・位置切換え運転指令 | 速度・位置切換え運転指令中 |
| 外部入力(指令) | X7 | — | — | — | 速度・位置切換え許可指令 | 速度・位置切換え許可指令中 |
| 外部入力(指令) | X10 | — | — | — | 速度・位置切換え禁止指令 | 速度・位置切換え禁止指令中 |
| 外部入力(指令) | X11 | — | — | — | 移動量変更指令 | 移動量変更指令中 |
| 外部入力(指令) | X12 | — | — | — | 高度な位置決め制御始動指令 | 高度な位置決め制御始動指令中 |
| 外部入力(指令) | X14 | — | — | — | MコードOFF指令 | MコードOFF指令中 |
| 外部入力(指令) | X15 | — | — | — | JOG運転速度設定指令 | JOG運転速度設定指令中 |
| 外部入力(指令) | X16 | — | — | — | 正転JOG／インチング指令 | 正転JOG／インチング運転指令中 |
| 外部入力(指令) | X17 | — | — | — | 逆転JOG／インチング指令 | 逆転JOG／インチング運転指令中 |
| 外部入力(指令) | X20 | — | — | — | 手動パルサ運転許可指令 | 手動パルサ運転許可指令中 |
| 外部入力(指令) | X21 | — | — | — | 手動パルサ運転不許可指令 | 手動パルサ運転不許可指令中 |
| 外部入力(指令) | X22 | — | — | — | 速度変更指令 | 速度変更指令中 |
| 外部入力(指令) | X23 | — | — | — | オーバーライド指令 | オーバーライド指令中 |
| 外部入力(指令) | X24 | — | — | — | 加減速時間変更指令 | 加減速時間変更指令中 |
| 外部入力(指令) | X25 | — | — | — | 加減速時間変更不許可指令 | 加減速時間変更不許可指令中 |
| 外部入力(指令) | X26 | — | — | — | トルク変更指令 | トルク変更指令中 |
| 外部入力(指令) | X27 | — | — | — | ステップ運転指令 | ステップ運転指令中 |
| 外部入力(指令) | X30 | — | — | — | スキップ指令 | スキップ指令中 |
| 外部入力(指令) | X31 | — | — | — | ティーチング指令 | ティーチング指令中 |
| 外部入力(指令) | X32 | — | — | — | 連続運転中断指令 | 連続運転中断指令中 |
| 外部入力(指令) | X33 | — | — | — | 再始動指令 | 再始動指令 |
| 外部入力(指令) | X34 | X34 | X34 | X34 | パラメータ初期化指令 | パラメータ初期化指令中 |
| 外部入力(指令) | X35 | X35 | X35 | X35 | フラッシュ ROM書込み指令 | フラッシュ ROM書込み指令中 |
| 外部入力(指令) | X36 | — | — | — | エラーリセット指令 | エラーリセット指令中 |
| 外部入力(指令) | X37 | — | — | — | 停止指令 | 停止指令中 |
| 外部入力(指令) | X40 | — | — | — | 位置・速度切換え運転指令 | 位置・速度切換え運転指令 |
| 外部入力(指令) | X41 | — | — | — | 位置・速度切換え許可指令 | 位置・速度切換え許可指令 |
| 外部入力(指令) | X42 | — | — | — | 位置・速度切換え禁止指令 | 位置・速度切換え禁止指令 |
| 外部入力(指令) | X43 | — | — | — | 速度変更指令 | 速度変更指令 |
| 外部入力(指令) | X44 | — | — | — | インチング移動量設定指令 | インチング移動量設定指令 |
| 外部入力(指令) | X45 | — | — | — | 目標位置変更指令 | 目標位置変更指令 |
| 外部入力(指令) | X46 | — | — | — | ステップ始動情報指令 | ステップ始動情報指令 |
| 外部入力(指令) | X47 | — | — | — | 位置決め始動指令K10 | 位置決め始動指令K10 |
| 外部入力(指令) | X50 | — | — | — | オーバーライド初期値指令 | オーバーライド初期値指令 |
| 外部入力(指令) | X53 | — | — | — | シーケンサレディ信号ON | シーケンサレディ信号ON |
| 外部入力(指令) | X54 | — | — | — | エラーリセットクリア指令 | エラーリセットクリア指令 |
| 外部入力(指令) | X55 | — | — | — | 単位(degree)の場合 | 単位(degree)の場合 |
| 外部入力(指令) | X56 | — | — | — | 位置決め始動信号指令 | 位置決め始動指令中 |
| 外部入力(指令) | X57 | — | — | — | 全軸サーボON指令 | 全軸サーボON指令 |
| 内部リレー | M0 | — | — | — | 原点復帰要求OFF指令 | 原点復帰要求OFF要求中 |
| 内部リレー | M1 | — | — | — | 原点復帰要求OFF指令パルス | 原点復帰要求OFF指令あり |
| 内部リレー | M2 | — | — | — | 原点復帰要求OFF指令記憶 | 原点復帰要求OFF指令保持 |
| 内部リレー | M3 | — | — | — | 高速原点復帰指令 | 高速原点復帰要求中 |
| 内部リレー | M4 | — | — | — | 高速原点復帰指令記憶 | 高速原点復帰指令保持 |
| 内部リレー | M5 | — | — | — | 位置決め始動指令パルス | 位置決め始動指令あり |
| 内部リレー | M6 | — | — | — | 位置決め始動指令記憶 | 位置決め始動指令保持 |
| 内部リレー | M7 | — | — | — | JOG／インチング運転中フラグ | JOG／インチング運転中フラグ |
| 内部リレー | M8 | — | — | — | 手動パルサ運転許可指令 | 手動パルサ運転許可要求中 |
| 内部リレー | M9 | — | — | — | 手動パルサ運転中フラグ | 手動パルサ運転中フラグ |
| 内部リレー | M10 | — | — | — | 手動パルサ運転不許可指令 | 手動パルサ運転不許可要求中 |
| 内部リレー | M11 | — | — | — | 速度変更指令パルス | 速度変更指令あり |
| 内部リレー | M12 | — | — | — | 速度変更指令記憶 | 速度変更指令保持 |
| 内部リレー | M13 | — | — | — | オーバーライド指令 | オーバーライド要求中 |
| 内部リレー | M14 | — | — | — | 加減速時間変更指令 | 加減速時間変更要求中 |
| 内部リレー | M15 | — | — | — | トルク変更指令 | トルク変更要求中 |
| 内部リレー | M16 | — | — | — | ステップ運転指令パルス | ステップ運転指令あり |
| 内部リレー | M17 | — | — | — | スキップ指令パルス | スキップ指令あり |
| 内部リレー | M18 | — | — | — | スキップ指令記憶 | スキップ指令保持 |
| 内部リレー | M19 | — | — | — | ティーチング指令パルス | ティーチング指令あり |
| 内部リレー | M20 | — | — | — | ティーチング指令記憶 | ティーチング指令保持 |
| 内部リレー | M21 | — | — | — | 連続運転中断指令 | 連続運転中断要求中 |
| 内部リレー | M22 | — | — | — | 再始動指令 | 再始動要求中 |
| 内部リレー | M23 | — | — | — | 再始動指令記憶 | 再始動指令保持 |
| 内部リレー | M24 | — | — | — | パラメータ初期化指令パルス | パラメータ初期化指令あり |
| 内部リレー | M25 | M25 | M25 | M25 | パラメータ初期化指令記憶 | パラメータ初期化指令保持 |
| 内部リレー | M26 | M26 | M26 | M26 | フラッシュ ROM書込み指令パルス | フラッシュ ROM書込み指令あり |
| 内部リレー | M27 | M27 | M27 | M27 | フラッシュ ROM書込み指令記憶 | フラッシュ ROM書込み指令保持 |
| 内部リレー | M28 | — | — | — | エラーリセット | エラーリセット完了 |
| 内部リレー | M29 | — | — | — | 停止指令パルス | 停止指令あり |
| 内部リレー | M30 | — | — | — | 目標位置変更指令パルス | 目標位置変更指令あり |
| 内部リレー | M31 | — | — | — | 目標位置変更指令記憶 | 目標位置変更指令保持 |
| 内部リレー | M40 | — | — | — | オーバーライド初期値指令 | オーバーライド初期値 |
| 内部リレー | M50 | — | — | — | パラメータ設定完了デバイス | パラメータ設定完了 |

※原本では「デバイス名称」列(シンプルモーションユニットのバッファメモリアドレス／外部入力(指令)／内部リレー)が区分ごとに縦の結合セル。各行に展開。
※原本では「デバイス」の軸2～軸4列が縦横の結合セルで「—」(U1\G2417.C～U1\G2417.F，U1\G30100～U1\G30104，X0～X33，X36～X57，M0～M24，M28～M50の各範囲)。各行・各列に展開。
※原本では U1\G31500.0，U1\G31500.1，U1\G5950，U1\G5951，X34，X35，M25，M26，M27 の行はデバイスが軸1～軸4の結合セル(1つのセルに1デバイス)。軸1～軸4の各列に同じ値を展開。
※原本では p.620-622 の3ページにまたがる表(p.621，p.622で見出し行を再掲)。

#### データレジスタ，タイマ (12.4 / 原本 p.623-626)

| デバイス名称 | 軸1 | 軸2 | 軸3 | 軸4 | 用途 | 格納内容 |
|---|---|---|---|---|---|---|
| データレジスタ | D0 | — | — | — | 原点復帰要求フラグ | [Md.31]ステータス: b3 |
| データレジスタ | D1 | — | — | — | 速度(下位16ビット) | [Cd.25]位置・速度切換え制御速度変更レジスタ |
| データレジスタ | D2 | — | — | — | 速度(上位16ビット) | [Cd.25]位置・速度切換え制御速度変更レジスタ |
| データレジスタ | D3 | — | — | — | 移動量(下位16ビット) | [Cd.23]速度・位置切換え制御移動量変更レジスタ |
| データレジスタ | D4 | — | — | — | 移動量(上位16ビット) | [Cd.23]速度・位置切換え制御移動量変更レジスタ |
| データレジスタ | D5 | — | — | — | インチング移動量 | [Cd.16]インチング移動量 |
| データレジスタ | D6 | — | — | — | JOG運転速度(下位16ビット) | [Cd.17]JOG速度 |
| データレジスタ | D7 | — | — | — | JOG運転速度(上位16ビット) | [Cd.17]JOG速度 |
| データレジスタ | D8 | — | — | — | 手動パルサ1パルス入力倍率(下位) | [Cd.20]手動パルサ1パルス入力倍率 |
| データレジスタ | D9 | — | — | — | 手動パルサ1パルス入力倍率(上位) | [Cd.20]手動パルサ1パルス入力倍率 |
| データレジスタ | D10 | — | — | — | 手動パルサ運転許可 | [Cd.21]手動パルサ許可フラグ |
| データレジスタ | D11 | — | — | — | 速度変更値(下位16ビット) | [Cd.14]速度変更値 |
| データレジスタ | D12 | — | — | — | 速度変更値(上位16ビット) | [Cd.14]速度変更値 |
| データレジスタ | D13 | — | — | — | 速度変更要求 | [Cd.15]速度変更要求 |
| データレジスタ | D14 | — | — | — | オーバーライド値 | [Cd.13]位置決め運転速度オーバーライド |
| データレジスタ | D15 | — | — | — | 加速時間設定(下位16ビット) | [Cd.10]加速時間変更値 |
| データレジスタ | D16 | — | — | — | 加速時間設定(上位16ビット) | [Cd.10]加速時間変更値 |
| データレジスタ | D17 | — | — | — | 減速時間設定(下位16ビット) | [Cd.11]減速時間変更値 |
| データレジスタ | D18 | — | — | — | 減速時間設定(上位16ビット) | [Cd.11]減速時間変更値 |
| データレジスタ | D19 | — | — | — | 加減速時間変更許可 | [Cd.12]速度変更時の加減速時間変更許可／不許可選択 |
| データレジスタ | D20 | — | — | — | ステップモード | [Cd.34]ステップモード |
| データレジスタ | D21 | — | — | — | ステップ有効フラグ | [Cd.35]ステップ有効フラグ |
| データレジスタ | D22 | — | — | — | ステップ始動情報 | — |
| データレジスタ | D23 | — | — | — | 目標位置(下位16ビット) | [Cd.27]目標位置変更値(アドレス) |
| データレジスタ | D24 | — | — | — | 目標位置(上位16ビット) | [Cd.27]目標位置変更値(アドレス) |
| データレジスタ | D25 | — | — | — | 目標速度(下位16ビット) | [Cd.28]目標位置変更値(速度) |
| データレジスタ | D26 | — | — | — | 目標速度(上位16ビット) | [Cd.28]目標位置変更値(速度) |
| データレジスタ | D27 | — | — | — | 目標位置変更要求 | [Cd.29]目標位置変更要求フラグ |
| データレジスタ | D31 | — | — | — | 完了ステータス | — |
| データレジスタ | D32 | — | — | — | 始動番号 | — |
| データレジスタ | D34 | — | — | — | 完了ステータス | — |
| データレジスタ | D35 | — | — | — | ティーチングデータ | — |
| データレジスタ | D36 | — | — | — | 位置決めデータNo. | — |
| データレジスタ | D38 | — | — | — | 完了ステータス | — |
| データレジスタ | D40 | — | — | — | 完了ステータス | — |
| データレジスタ | D50 | — | — | — | 単位設定 | [Pr.1]単位設定 |
| データレジスタ | D51 | — | — | — | 単位倍率 | [Pr.4]単位倍率(AM) |
| データレジスタ | D52 | — | — | — | 1回転あたりのパルス数(下位16ビット) | [Pr.2]1回転あたりのパルス数(AP) |
| データレジスタ | D53 | — | — | — | 1回転あたりのパルス数(上位16ビット) | [Pr.2]1回転あたりのパルス数(AP) |
| データレジスタ | D54 | — | — | — | 1回転あたりの移動量(下位16ビット) | [Pr.3]1回転あたりの移動量(AL) |
| データレジスタ | D55 | — | — | — | 1回転あたりの移動量(上位16ビット) | [Pr.3]1回転あたりの移動量(AL) |
| データレジスタ | D56 | — | — | — | 始動時バイアス速度(下位16ビット) | [Pr.7]始動時バイアス速度 |
| データレジスタ | D57 | — | — | — | 始動時バイアス速度(上位16ビット) | [Pr.7]始動時バイアス速度 |
| データレジスタ | D68 | — | — | — | ブロック始動データ(ブロック0)／1ポイント目(形態，始動No.) | [Da.11]形態<br>[Da.12]始動データNo.<br>[Da.13]特殊始動命令<br>[Da.14]パラメータ |
| データレジスタ | D69 | — | — | — | ブロック始動データ(ブロック0)／2ポイント目(形態，始動No.) | [Da.11]形態<br>[Da.12]始動データNo.<br>[Da.13]特殊始動命令<br>[Da.14]パラメータ |
| データレジスタ | D70 | — | — | — | ブロック始動データ(ブロック0)／3ポイント目(形態，始動No.) | [Da.11]形態<br>[Da.12]始動データNo.<br>[Da.13]特殊始動命令<br>[Da.14]パラメータ |
| データレジスタ | D71 | — | — | — | ブロック始動データ(ブロック0)／4ポイント目(形態，始動No.) | [Da.11]形態<br>[Da.12]始動データNo.<br>[Da.13]特殊始動命令<br>[Da.14]パラメータ |
| データレジスタ | D72 | — | — | — | ブロック始動データ(ブロック0)／5ポイント目(形態，始動No.) | [Da.11]形態<br>[Da.12]始動データNo.<br>[Da.13]特殊始動命令<br>[Da.14]パラメータ |
| データレジスタ | D73 | — | — | — | ブロック始動データ(ブロック0)／1ポイント目(特殊始動命令) | [Da.11]形態<br>[Da.12]始動データNo.<br>[Da.13]特殊始動命令<br>[Da.14]パラメータ |
| データレジスタ | D74 | — | — | — | ブロック始動データ(ブロック0)／2ポイント目(特殊始動命令) | [Da.11]形態<br>[Da.12]始動データNo.<br>[Da.13]特殊始動命令<br>[Da.14]パラメータ |
| データレジスタ | D75 | — | — | — | ブロック始動データ(ブロック0)／3ポイント目(特殊始動命令) | [Da.11]形態<br>[Da.12]始動データNo.<br>[Da.13]特殊始動命令<br>[Da.14]パラメータ |
| データレジスタ | D76 | — | — | — | ブロック始動データ(ブロック0)／4ポイント目(特殊始動命令) | [Da.11]形態<br>[Da.12]始動データNo.<br>[Da.13]特殊始動命令<br>[Da.14]パラメータ |
| データレジスタ | D77 | — | — | — | ブロック始動データ(ブロック0)／5ポイント目(特殊始動命令) | [Da.11]形態<br>[Da.12]始動データNo.<br>[Da.13]特殊始動命令<br>[Da.14]パラメータ |
| データレジスタ | D78 | — | — | — | トルク変更値 | — |
| データレジスタ | D79 | — | — | — | エラーコード | [Md.23]軸エラー番号 |
| データレジスタ | D80 | — | — | — | サーボシリーズ | [Pr.100]サーボシリーズ |
| データレジスタ | D81 | — | — | — | 絶対位置システム有無 | MR-J4(W)-Bの場合:<br>絶対位置検出システム(PA03)<br>MR-J5(W)-Bの場合:<br>絶対位置検出システム選択(PA03.0) |
| データレジスタ | D85 | — | — | — | 原点復帰方法 | [Pr.43]原点復帰方式 |
| データレジスタ | D100 | — | — | — | 位置決め識別子 | データNo.1<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D101 | — | — | — | Mコード | データNo.1<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D102 | — | — | — | ドウェルタイム | データNo.1<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D103 | — | — | — | ダミー | データNo.1<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D104 | — | — | — | 指令速度(下位16ビット) | データNo.1<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D105 | — | — | — | 指令速度(上位16ビット) | データNo.1<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D106 | — | — | — | 位置決めアドレス(下位16ビット) | データNo.1<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D107 | — | — | — | 位置決めアドレス(上位16ビット) | データNo.1<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D108 | — | — | — | 円弧アドレス(下位16ビット) | データNo.1<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D109 | — | — | — | 円弧アドレス(上位16ビット) | データNo.1<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D110 | — | — | — | 位置決め識別子 | データNo.2<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D111 | — | — | — | Mコード | データNo.2<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D112 | — | — | — | ドウェルタイム | データNo.2<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D113 | — | — | — | ダミー | データNo.2<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D114 | — | — | — | 指令速度(下位16ビット) | データNo.2<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D115 | — | — | — | 指令速度(上位16ビット) | データNo.2<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D116 | — | — | — | 位置決めアドレス(下位16ビット) | データNo.2<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D117 | — | — | — | 位置決めアドレス(上位16ビット) | データNo.2<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D118 | — | — | — | 円弧アドレス(下位16ビット) | データNo.2<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D119 | — | — | — | 円弧アドレス(上位16ビット) | データNo.2<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D120 | — | — | — | 位置決め識別子 | データNo.3<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D121 | — | — | — | Mコード | データNo.3<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D122 | — | — | — | ドウェルタイム | データNo.3<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D123 | — | — | — | ダミー | データNo.3<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D124 | — | — | — | 指令速度(下位16ビット) | データNo.3<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D125 | — | — | — | 指令速度(上位16ビット) | データNo.3<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D126 | — | — | — | 位置決めアドレス(下位16ビット) | データNo.3<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D127 | — | — | — | 位置決めアドレス(上位16ビット) | データNo.3<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D128 | — | — | — | 円弧アドレス(下位16ビット) | データNo.3<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D129 | — | — | — | 円弧アドレス(上位16ビット) | データNo.3<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D130 | — | — | — | 位置決め識別子 | データNo.4<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D131 | — | — | — | Mコード | データNo.4<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D132 | — | — | — | ドウェルタイム | データNo.4<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D133 | — | — | — | ダミー | データNo.4<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D134 | — | — | — | 指令速度(下位16ビット) | データNo.4<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D135 | — | — | — | 指令速度(上位16ビット) | データNo.4<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D136 | — | — | — | 位置決めアドレス(下位16ビット) | データNo.4<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D137 | — | — | — | 位置決めアドレス(上位16ビット) | データNo.4<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D138 | — | — | — | 円弧アドレス(下位16ビット) | データNo.4<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D139 | — | — | — | 円弧アドレス(上位16ビット) | データNo.4<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D140 | — | — | — | 位置決め識別子 | データNo.5<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D141 | — | — | — | Mコード | データNo.5<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D142 | — | — | — | ドウェルタイム | データNo.5<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D143 | — | — | — | ダミー | データNo.5<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D144 | — | — | — | 指令速度(下位16ビット) | データNo.5<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D145 | — | — | — | 指令速度(上位16ビット) | データNo.5<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D146 | — | — | — | 位置決めアドレス(下位16ビット) | データNo.5<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D147 | — | — | — | 位置決めアドレス(上位16ビット) | データNo.5<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D148 | — | — | — | 円弧アドレス(下位16ビット) | データNo.5<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D149 | — | — | — | 円弧アドレス(上位16ビット) | データNo.5<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D150 | — | — | — | 位置決め識別子 | データNo.6<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D151 | — | — | — | Mコード | データNo.6<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D152 | — | — | — | ドウェルタイム | データNo.6<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D153 | — | — | — | ダミー | データNo.6<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D154 | — | — | — | 指令速度(下位16ビット) | データNo.6<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D155 | — | — | — | 指令速度(上位16ビット) | データNo.6<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D156 | — | — | — | 位置決めアドレス(下位16ビット) | データNo.6<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D157 | — | — | — | 位置決めアドレス(上位16ビット) | データNo.6<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D158 | — | — | — | 円弧アドレス(下位16ビット) | データNo.6<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D159 | — | — | — | 円弧アドレス(上位16ビット) | データNo.6<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D190 | — | — | — | 位置決め識別子 | データNo.10<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D191 | — | — | — | Mコード | データNo.10<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D192 | — | — | — | ドウェルタイム | データNo.10<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D193 | — | — | — | ダミー | データNo.10<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D194 | — | — | — | 指令速度(下位16ビット) | データNo.10<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D195 | — | — | — | 指令速度(上位16ビット) | データNo.10<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D196 | — | — | — | 位置決めアドレス(下位16ビット) | データNo.10<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D197 | — | — | — | 位置決めアドレス(上位16ビット) | データNo.10<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D198 | — | — | — | 円弧アドレス(下位16ビット) | データNo.10<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D199 | — | — | — | 円弧アドレス(上位16ビット) | データNo.10<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D200 | — | — | — | 位置決め識別子 | データNo.11<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D201 | — | — | — | Mコード | データNo.11<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D202 | — | — | — | ドウェルタイム | データNo.11<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D203 | — | — | — | ダミー | データNo.11<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D204 | — | — | — | 指令速度(下位16ビット) | データNo.11<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D205 | — | — | — | 指令速度(上位16ビット) | データNo.11<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D206 | — | — | — | 位置決めアドレス(下位16ビット) | データNo.11<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D207 | — | — | — | 位置決めアドレス(上位16ビット) | データNo.11<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D208 | — | — | — | 円弧アドレス(下位16ビット) | データNo.11<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D209 | — | — | — | 円弧アドレス(上位16ビット) | データNo.11<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D240 | — | — | — | 位置決め識別子 | データNo.15<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D241 | — | — | — | Mコード | データNo.15<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D242 | — | — | — | ドウェルタイム | データNo.15<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D243 | — | — | — | ダミー | データNo.15<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D244 | — | — | — | 指令速度(下位16ビット) | データNo.15<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D245 | — | — | — | 指令速度(上位16ビット) | データNo.15<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D246 | — | — | — | 位置決めアドレス(下位16ビット) | データNo.15<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D247 | — | — | — | 位置決めアドレス(上位16ビット) | データNo.15<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D248 | — | — | — | 円弧アドレス(下位16ビット) | データNo.15<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| データレジスタ | D249 | — | — | — | 円弧アドレス(上位16ビット) | データNo.15<br>[Da.1]運転パターン<br>[Da.2]制御方式<br>[Da.3]加速時間No.<br>[Da.4]減速時間No.<br>[Da.20]～[Da.22]補間対象軸<br>[Da.6]位置決めアドレス／移動量<br>[Da.7]円弧アドレス<br>[Da.8]指令速度<br>[Da.9]ドウェルタイム／JUMP先位置決めデータNo.<br>[Da.10]Mコード／条件データNo.／LOOP～LEND繰り返し回数 |
| タイマ | T0 | — | — | — | シーケンサレディ信号OFF確認 | シーケンサレディ信号OFF |
| タイマ | T1 | — | — | — | シーケンサレディ信号OFF確認 | シーケンサレディ信号OFF |
| コード | U1\G2406 | U1\G2406 | U1\G2406 | U1\G2406 | エラーコード | [Md.23]軸エラー番号 |
| コード | U1\G2409 | U1\G2409 | U1\G2409 | U1\G2409 | 軸動作状態 | [Md.26]軸動作状態 |
| コード | U1\G2417 | U1\G2417 | U1\G2417 | U1\G2417 | ステータス | [Md.31]ステータス |
| コード | U1\G4300 | U1\G4300 | U1\G4300 | U1\G4300 | 位置決め始動番号 | [Cd.3]位置決め始動番号 |
| コード | U1\G4301 | U1\G4301 | U1\G4301 | U1\G4301 | 位置決め始動ポイント番号 | [Cd.4]位置決め始動ポイント番号 |
| コード | U1\G4302 | U1\G4302 | U1\G4302 | U1\G4302 | エラーリセット | [Cd.5]軸エラーリセット |
| コード | U1\G4303 | U1\G4303 | U1\G4303 | U1\G4303 | 再始動命令 | [Cd.6]再始動指令 |
| コード | U1\G4304 | U1\G4304 | U1\G4304 | U1\G4304 | MコードOFF要求(バッファメモリ) | [Cd.7]MコードOFF要求 |
| コード | U1\G4305 | U1\G4305 | U1\G4305 | U1\G4305 | 外部指令有効 | [Cd.8]外部指令有効 |
| コード | U1\G4313 | U1\G4313 | U1\G4313 | U1\G4313 | オーバーライド要求 | [Cd.13]位置決め運転速度オーバーライド |
| コード | U1\G4316 | U1\G4316 | U1\G4316 | U1\G4316 | 速度変更要求 | [Cd.15]速度変更要求 |
| コード | U1\G4317 | U1\G4317 | U1\G4317 | U1\G4317 | インチング移動量 | [Cd.16]インチング移動量 |
| コード | U1\G4320 | U1\G4320 | U1\G4320 | U1\G4320 | 連続運転中断要求 | [Cd.18]連続運転中断要求 |
| コード | U1\G4321 | U1\G4321 | U1\G4321 | U1\G4321 | 原点復帰要求フラグOFF要求 | [Cd.19]原点復帰要求フラグOFF要求 |
| コード | U1\G4324 | U1\G4324 | U1\G4324 | U1\G4324 | 手動パルサ許可フラグ | [Cd.21]手動パルサ許可フラグ |
| コード | U1\G4326 | U1\G4326 | U1\G4326 | U1\G4326 | 速度・位置切換え制御移動量 | [Cd.23]速度・位置切換え制御移動量変更レジスタ |
| コード | U1\G4328 | U1\G4328 | U1\G4328 | U1\G4328 | 速度・位置切換え許可フラグ | [Cd.24]速度・位置切換え許可フラグ |
| コード | U1\G4330 | U1\G4330 | U1\G4330 | U1\G4330 | 位置・速度切換え制御速度変更 | [Cd.25]位置・速度切換え制御速度変更レジスタ |
| コード | U1\G4332 | U1\G4332 | U1\G4332 | U1\G4332 | 位置・速度切換え許可フラグ | [Cd.26]位置・速度切換え許可フラグ |
| コード | U1\G4338 | U1\G4338 | U1\G4338 | U1\G4338 | 目標位置変更要求フラグ | [Cd.29]目標位置変更要求フラグ |
| コード | U1\G4344 | U1\G4344 | U1\G4344 | U1\G4344 | ステップモード | [Cd.34]ステップモード |
| コード | U1\G4347 | U1\G4347 | U1\G4347 | U1\G4347 | スキップ指令 | [Cd.37]スキップ指令 |

※原本では「デバイス名称」列(データレジスタ／タイマ／コード)が区分ごとに縦の結合セル。各行に展開。
※原本では「デバイス」の軸2～軸4列が D0～T1 の範囲で縦横の結合セルで「—」。各行・各列に展開。
※原本では「コード」区分(U1\G2406～U1\G4347)の各行はデバイスが軸1～軸4の結合セル(1つのセルに1デバイス)。軸1～軸4の各列に同じ値を展開。
※原本では「格納内容」列が次の範囲で縦の結合セル。各行に展開: D1-D2，D3-D4，D6-D7，D8-D9，D11-D12，D15-D16，D17-D18，D23-D24，D25-D26，D52-D53，D54-D55，D56-D57，D68-D77，D100-D109，D110-D119，D120-D129，D130-D139，D140-D149，D150-D159，D190-D199，D200-D209，D240-D249，T0-T1。
※原本では D68～D77 の「用途」列が2段構成で、左段「ブロック始動データ(ブロック0)」が D68～D77 の縦の結合セル、右段が各ポイントの内容。「左段／右段」の形で各行に展開。
※原本 p.625 の D190～D199(データNo.10)の格納内容は「Da.8]指令速度」と先頭の「[」が欠けた表記(原本のとおり転記)。
※原本では p.623-626 の4ページにまたがる表(p.624～p.626で見出し行を再掲)。

### プログラム例(バッファメモリ使用時) (12.4 / 原本 p.627-652)

#### パラメータ設定プログラム (12.4 / 原本 p.627-628)

エンジニアリングツールの"ユニットパラメータ"にてパラメータを設定する場合，本プログラムは不要です。

【ラダー図】No.1 パラメータ設定プログラム(原本 p.627)

```
// No.1 パラメータ設定プログラム
//  (基本パラメータ1<軸1>の場合)
// 原点復帰パラメータ
(0)    LD    SM402              // SM402: RUN後1スキャンのみON
       // <変更速度設定(90.00 mm/min)>
       DMOVP K9000 D1    // D1: 速度(下位16ビット)
       // <変更後の移動量設定(5000.0 μm)>
       DMOVP K50000 D3    // D3: 移動量(下位16ビット)
       // <単位設定(0:mm)の設定>
       MOVP K0 D50    // D50: 単位設定
       // <単位倍率(1倍)の設定>
       MOVP K1 D51    // D51: 単位倍率:AM
       // <1回転あたりのパルス数(4194304 pulse)>
       DMOVP K4194304 D52    // D52: 1回転あたりのパルス数(下位16):AP
       // <1回転あたりの移動量(2500.0 μm)>
       DMOVP K25000 D54    // D54: 1回転あたりのパルス移動量(下位16):AL
       // <基本パラメータ1の設定>
       TOP H1 K0 D50 K8    // D50: 単位設定
       // <外部指令機能選択(2:速度/位置)>
       TOP H1 K62 K2 K1
       // <原点復帰方法(データセット式)>
       TOP H1 K70 K6 K1
       // <原点復帰速度(15.00 mm/min)>
       DTOP H1 K74 K1500 K1
       // <クリープ速度設定(12.00 mm/min)>
       DTOP H1 K76 K1200 K1
       // <基本パラメータ1設定完了>
       SET M50    // M50: パラメータ設定完了デバイス
```

```
// 単位degree設定用プログラム
// <軸1の場合>
//  (速度・位置切換え制御(ABSモード)を実行する場合など)
// <X55は立上げ前にON>
(428)  LD    SM402              // SM402: RUN後1スキャンのみON
       AND   X55                // X55: 単位(degree)の場合
       // <単位設定(2:degree)の設定>
       TOP H1 K0 K2 K1
       // <1回転あたりの移動量:AL>
       DTOP H1 K4 K9000000 K1
       // <速度制限値(20000.000 degree/min)>
       DTOP H1 K10 K20000000 K1
       // <(S/Wストロークリミット上限)=0>
       DTOP H1 K18 K0 K1
       // <(S/Wストロークリミット下限)=0>
       DTOP H1 K20 K0 K1
       // <(速度制御時の送り現在値)=0>
       TOP H1 K30 K2 K1
       // <速度・位置機能選択(ABSモード)>
       TOP H1 K34 K2 K1
       // <JOG速度制限値(20000.000 degree/min)>
       DTOP H1 K48 K20000000 K1
       // <原点復帰速度(1000.000 degree/min)>
       DTOP H1 K74 K1000000 K1
       // <クリープ速度(800.000 degree/min)>
       DTOP H1 K76 K800000 K1
```

- 原本 p.627 の回路はステップ(0)，原本 p.628 の回路はステップ(428)から始まる。いずれも SM402 の後の母線から各命令が並列に分岐する回路。

#### 位置決めデータ設定プログラム (12.4 / 原本 p.629-637)

エンジニアリングツールの"位置決めデータ"にて設定する場合，本プログラムは不要です。

##### No.2-1 位置決めデータ設定プログラム(位置決めデータNo.1<軸1>の場合) (12.4 / 原本 p.629)

```
// No.2-1  位置決めデータ設定プログラム
//  (位置決めデータNo.1<軸1>の場合)
// <位置決め識別子>
//   運転パターン:位置決め終了
//   制御方式:1軸の直線制御(ABS)
//   加速時間No.:1, 減速時間No.:2
(857)  LD    SM402              // SM402: RUN後1スキャンのみON
       // <位置決め識別子の設定>
       MOVP  H190 D100    // D100: 位置決め識別子
       // <Mコード(9843)の設定>
       MOVP  K9843 D101    // D101: Mコード
       // <ドウェルタイム(300 ms)の設定>
       MOVP  K300 D102    // D102: ドウェルタイム
       // <(ダミーデータ)>
       MOVP  K0 D103    // D103: (ダミー)
       // <指令速度(20.00 mm/min)の設定>
       DMOVP K2000 D104    // D104: 指令速度(下位16ビット)
       MPS
       AND   X55                // X55: 単位(degree)の場合
       // <指令速度(1200.000 degree/min)の設定>
       DMOVP K1200000 D104    // D104: 指令速度(下位16ビット)
       MPP
       // <位置決めアドレス(-10000.0 μm)の設定>
       DMOVP K-100000 D106    // D106: 位置決めアドレス(下位16ビット)
       MPS
       AND   X55                // X55: 単位(degree)の場合
       // <位置決めアドレス(270.00000 degree)の設定>
       DMOVP K27000000 D106    // D106: 位置決めアドレス(下位16ビット)
       MPP
       // <円弧アドレス(0.0 μm)の設定>
       DMOVP K0 D108    // D108: 円弧アドレス(下位16ビット)
       // <位置決めデータNo.1の設定>
       TOP   H1 K6000 D100 K10    // D100: 位置決め識別子
```

##### No.2-2 位置決めデータ設定プログラム(位置決めデータNo.2<軸1>の場合) (12.4 / 原本 p.630)

```
// No.2-2  位置決めデータ設定プログラム
//  (位置決めデータNo.2<軸1>の場合)
// <位置決め識別子>
//   運転パターン:位置決め終了
//   制御方式:速度・位置切り換え制御(正転)
//   加速時間No.:0, 減速時間No.:0
(1248) LD    SM402              // SM402: RUN後1スキャンのみON
       // <位置決め識別子の設定>
       MOVP  H600 D110    // D110: 位置決め識別子
       // <Mコード(0)の設定>
       MOVP  K0 D111    // D111: Mコード
       // <ドウェルタイム(300 ms)の設定>
       MOVP  K300 D112    // D112: ドウェルタイム
       // <(ダミーデータ)>
       MOVP  K0 D113    // D113: (ダミー)
       // <指令速度(180.00 mm/min)の設定>
       DMOVP K18000 D114    // D114: 指令速度(下位16ビット)
       MPS
       AND   X55                // X55: 単位(degree)の場合
       // <指令速度(3600.000 degree/min)の設定>
       DMOVP K3600000 D114    // D114: 指令速度(下位16ビット)
       MPP
       // <位置決めアドレス(2500.0 μm)の設定>
       DMOVP K25000 D116    // D116: 位置決めアドレス(下位16ビット)
       MPS
       AND   X55                // X55: 単位(degree)の場合
       // <位置決めアドレス(90.00000 degree)の設定>
       DMOVP K9000000 D116    // D116: 位置決めアドレス(下位16ビット)
       MPP
       // <円弧アドレス(0.0 μm)の設定>
       DMOVP K0 D118    // D118: 円弧アドレス(下位16ビット)
       // <位置決めデータNo.2の設定>
       TOP   H1 K6010 D110 K10    // D110: 位置決め識別子
```

##### No.2-3 位置決めデータ設定プログラム(位置決めデータNo.3<軸1>の場合) (12.4 / 原本 p.631)

```
// No.2-3  位置決めデータ設定プログラム
//  (位置決めデータNo.3<軸1>の場合)
// <位置決め識別子>
//   運転パターン:位置決め終了
//   制御方式:位置・速度切り換え制御(正転)
//   加速時間No.:0, 減速時間No.:0
(1632) LD    SM402              // SM402: RUN後1スキャンのみON
       // <位置決め識別子の設定>
       MOVP  H800 D120    // D120: 位置決め識別子
       // <Mコード(0)の設定>
       MOVP  K0 D121    // D121: Mコード
       // <ドウェルタイム(300 ms)の設定>
       MOVP  K300 D122    // D122: ドウェルタイム
       // <(ダミーデータ)>
       MOVP  K0 D123    // D123: (ダミー)
       // <指令速度(180.00 mm/min)の設定>
       DMOVP K18000 D124    // D124: 指令速度(下位16ビット)
       MPS
       AND   X55                // X55: 単位(degree)の場合
       // <指令速度(3600.000 degree/min)の設定>
       DMOVP K3600000 D124    // D124: 指令速度(下位16ビット)
       MPP
       // <位置決めアドレス(20000.0 μm)の設定>
       DMOVP K200000 D126    // D126: 位置決めアドレス(下位16ビット)
       MPS
       AND   X55                // X55: 単位(degree)の場合
       // <位置決めアドレス(720.00000 degree)の設定>
       DMOVP K72000000 D126    // D126: 位置決めアドレス(下位16ビット)
       MPP
       // <円弧アドレス(0.0 μm)の設定>
       DMOVP K0 D128    // D128: 円弧アドレス(下位16ビット)
       // <位置決めデータNo.3の設定>
       TOP   H1 K6020 D120 K10    // D120: 位置決め識別子
```

##### No.2-4 位置決めデータ設定プログラム(位置決めデータNo.4<軸1>の場合) (12.4 / 原本 p.632)

```
// No.2-4  位置決めデータ設定プログラム
//  (位置決めデータNo.4<軸1>の場合)
// <位置決め識別子>
//   運転パターン:位置決め終了
//   制御方式:1軸の直線制御(INC)
//   加速時間No.:0, 減速時間No.:0
(2018) LD    SM402              // SM402: RUN後1スキャンのみON
       // <位置決め識別子の設定>
       MOVP  H200 D130    // D130: 位置決め識別子
       // <Mコード(0)の設定>
       MOVP  K0 D131    // D131: Mコード
       // <ドウェルタイム(300 ms)の設定>
       MOVP  K300 D132    // D132: ドウェルタイム
       // <(ダミーデータ)>
       MOVP  K0 D133    // D133: (ダミー)
       // <指令速度(90.00 mm/min)の設定>
       DMOVP K9000 D134    // D134: 指令速度(下位16ビット)
       MPS
       AND   X55                // X55: 単位(degree)の場合
       // <指令速度(1800.000 degree/min)の設定>
       DMOVP K1800000 D134    // D134: 指令速度(下位16ビット)
       MPP
       // <位置決めアドレス(5000.0 μm)の設定>
       DMOVP K50000 D136    // D136: 位置決めアドレス(下位16ビット)
       MPS
       AND   X55                // X55: 単位(degree)の場合
       // <位置決めアドレス(180.00000 degree)の設定>
       DMOVP K18000000 D136    // D136: 位置決めアドレス(下位16ビット)
       MPP
       // <円弧アドレス(0.0 μm)の設定>
       DMOVP K0 D138    // D138: 円弧アドレス(下位16ビット)
       // <位置決めデータNo.4の設定>
       TOP   H1 K6030 D130 K10    // D130: 位置決め識別子
```

##### No.2-5 位置決めデータ設定プログラム(位置決めデータNo.5<軸1>の場合) (12.4 / 原本 p.633)

```
// No.2-5  位置決めデータ設定プログラム
//  (位置決めデータNo.5<軸1>の場合)
// <位置決め識別子>
//   運転パターン:連続位置決め制御
//   制御方式:1軸の直線制御(INC)
//   加速時間No.:0, 減速時間No.:0
(2402) LD    SM402              // SM402: RUN後1スキャンのみON
       // <位置決め識別子の設定>
       MOVP  H201 D140    // D140: 位置決め識別子
       // <Mコード(0)の設定>
       MOVP  K0 D141    // D141: Mコード
       // <ドウェルタイム(300 ms)の設定>
       MOVP  K300 D142    // D142: ドウェルタイム
       // <(ダミーデータ)>
       MOVP  K0 D143    // D143: (ダミー)
       // <指令速度(360.00 mm/min)の設定>
       DMOVP K36000 D144    // D144: 指令速度(下位16ビット)
       MPS
       AND   X55                // X55: 単位(degree)の場合
       // <指令速度(6000.000 degree/min)の設定>
       DMOVP K6000000 D144    // D144: 指令速度(下位16ビット)
       MPP
       // <位置決めアドレス(10000.0 μm)の設定>
       DMOVP K100000 D146    // D146: 位置決めアドレス(下位16ビット)
       MPS
       AND   X55                // X55: 単位(degree)の場合
       // <位置決めアドレス(360.00000 degree)の設定>
       DMOVP K36000000 D146    // D146: 位置決めアドレス(下位16ビット)
       MPP
       // <円弧アドレス(0.0 μm)の設定>
       DMOVP K0 D148    // D148: 円弧アドレス(下位16ビット)
       // <位置決めデータNo.5の設定>
       TOP   H1 K6040 D140 K10    // D140: 位置決め識別子
```

##### No.2-6 位置決めデータ設定プログラム(位置決めデータNo.6<軸1>の場合) (12.4 / 原本 p.634)

```
// No.2-6  位置決めデータ設定プログラム
//  (位置決めデータNo.6<軸1>の場合)
// <位置決め識別子>
//   運転パターン:位置決め終了
//   制御方式:1軸の直線制御(INC)
//   加速時間No.:0, 減速時間No.:0
(2788) LD    SM402              // SM402: RUN後1スキャンのみON
       // <位置決め識別子の設定>
       MOVP  H200 D150    // D150: 位置決め識別子
       // <Mコード(0)の設定>
       MOVP  K0 D151    // D151: Mコード
       // <ドウェルタイム(300 ms)の設定>
       MOVP  K300 D152    // D152: ドウェルタイム
       // <(ダミーデータ)>
       MOVP  K0 D153    // D153: (ダミー)
       // <指令速度(90.00 mm/min)の設定>
       DMOVP K9000 D154    // D154: 指令速度(下位16ビット)
       MPS
       AND   X55                // X55: 単位(degree)の場合
       // <指令速度(1800.000 degree/min)の設定>
       DMOVP K1800000 D154    // D154: 指令速度(下位16ビット)
       MPP
       // <位置決めアドレス(5000.0 μm)の設定>
       DMOVP K50000 D156    // D156: 位置決めアドレス(下位16ビット)
       MPS
       AND   X55                // X55: 単位(degree)の場合
       // <位置決めアドレス(180.00000 degree)の設定>
       DMOVP K18000000 D156    // D156: 位置決めアドレス(下位16ビット)
       MPP
       // <円弧アドレス(0.0 μm)の設定>
       DMOVP K0 D158    // D158: 円弧アドレス(下位16ビット)
       // <位置決めデータNo.6の設定>
       TOP   H1 K6050 D150 K10    // D150: 位置決め識別子
```

##### No.2-7 位置決めデータ設定プログラム(位置決めデータNo.10<軸1>の場合) (12.4 / 原本 p.635)

```
// No.2-7  位置決めデータ設定プログラム
//  (位置決めデータNo.10<軸1>の場合)
// <位置決め識別子>
//   運転パターン:連続位置決め制御
//   制御方式:1軸の直線制御(INC)
//   加速時間No.:0, 減速時間No.:0
(3172) LD    SM402              // SM402: RUN後1スキャンのみON
       // <位置決め識別子の設定>
       MOVP  H201 D190    // D190: 位置決め識別子
       // <Mコード(0)の設定>
       MOVP  K0 D191    // D191: Mコード
       // <ドウェルタイム(300 ms)の設定>
       MOVP  K300 D192    // D192: ドウェルタイム
       // <(ダミーデータ)>
       MOVP  K0 D193    // D193: (ダミー)
       // <指令速度(180.00 mm/min)の設定>
       DMOVP K18000 D194    // D194: 指令速度(下位16ビット)
       MPS
       AND   X55                // X55: 単位(degree)の場合
       // <指令速度(3600.000 degree/min)の設定>
       DMOVP K3600000 D194    // D194: 指令速度(下位16ビット)
       MPP
       // <位置決めアドレス(10000.0 μm)の設定>
       DMOVP K100000 D196    // D196: 位置決めアドレス(下位16ビット)
       MPS
       AND   X55                // X55: 単位(degree)の場合
       // <位置決めアドレス(360.00000 degree)の設定>
       DMOVP K36000000 D196    // D196: 位置決めアドレス(下位16ビット)
       MPP
       // <円弧アドレス(0.0 μm)の設定>
       DMOVP K0 D198    // D198: 円弧アドレス(下位16ビット)
       // <位置決めデータNo.10の設定>
       TOP   H1 K6090 D190 K10    // D190: 位置決め識別子
```

##### No.2-8 位置決めデータ設定プログラム(位置決めデータNo.11<軸1>の場合) (12.4 / 原本 p.636)

```
// No.2-8  位置決めデータ設定プログラム
//  (位置決めデータNo.11<軸1>の場合)
// <位置決め識別子>
//   運転パターン:位置決め終了
//   制御方式:1軸の直線制御(INC)
//   加速時間No.:0, 減速時間No.:0
(3559) LD    SM402              // SM402: RUN後1スキャンのみON
       // <位置決め識別子の設定>
       MOVP  H200 D200    // D200: 位置決め識別子
       // <Mコード(0)の設定>
       MOVP  K0 D201    // D201: Mコード
       // <ドウェルタイム(300 ms)の設定>
       MOVP  K300 D202    // D202: ドウェルタイム
       // <(ダミーデータ)>
       MOVP  K0 D203    // D203: (ダミー)
       // <指令速度(180.00 mm/min)の設定>
       DMOVP K18000 D204    // D204: 指令速度(下位16ビット)
       MPS
       AND   X55                // X55: 単位(degree)の場合
       // <指令速度(3600.000 degree/min)の設定>
       DMOVP K3600000 D204    // D204: 指令速度(下位16ビット)
       MPP
       // <位置決めアドレス(-10000.0 μm)の設定>
       DMOVP K-100000 D206    // D206: 位置決めアドレス(下位16ビット)
       MPS
       AND   X55                // X55: 単位(degree)の場合
       // <位置決めアドレス(-360.00000 degree)の設定>
       DMOVP K-36000000 D206    // D206: 位置決めアドレス(下位16ビット)
       MPP
       // <円弧アドレス(0.0 μm)の設定>
       DMOVP K0 D208    // D208: 円弧アドレス(下位16ビット)
       // <位置決めデータNo.11の設定>
       TOP   H1 K6100 D200 K10    // D200: 位置決め識別子
```

##### No.2-9 位置決めデータ設定プログラム(位置決めデータNo.15<軸1>の場合) (12.4 / 原本 p.637)

```
// No.2-9  位置決めデータ設定プログラム
//  (位置決めデータNo.15<軸1>の場合)
// <位置決め識別子>
//   運転パターン:位置決め終了
//   制御方式:1軸の直線制御(INC)
//   加速時間No.0, 減速時間No.:0
(3950) LD    SM402              // SM402: RUN後1スキャンのみON
       // <位置決め識別子の設定>
       MOVP  H200 D240    // D240: 位置決め識別子
       // <Mコード(0)の設定>
       MOVP  K0 D241    // D241: Mコード
       // <ドウェルタイム(0 ms)の設定>
       MOVP  K0 D242    // D242: ドウェルタイム
       // <(ダミーデータ)>
       MOVP  K0 D243    // D243: (ダミー)
       // <指令速度(90.00 mm/min)の設定>
       DMOVP K9000 D244    // D244: 指令速度(下位16ビット)
       MPS
       AND   X55                // X55: 単位(degree)の場合
       // <指令速度(1800.000 degree/min)の設定>
       DMOVP K1800000 D244    // D244: 指令速度(下位16ビット)
       MPP
       // <位置決めアドレス(5000.0 μm)の設定>
       DMOVP K50000 D246    // D246: 位置決めアドレス(下位16ビット)
       MPS
       AND   X55                // X55: 単位(degree)の場合
       // <位置決めアドレス(180.00000 degree)の設定>
       DMOVP K18000000 D246    // D246: 位置決めアドレス(下位16ビット)
       MPP
       // <円弧アドレス(0.0 μm)の設定>
       DMOVP K0 D248    // D248: 円弧アドレス(下位16ビット)
       // <位置決めデータNo.15の設定>
       TOP   H1 K6140 D240 K10    // D240: 位置決め識別子
```

- 各位置決めデータ設定プログラムの回路構成(原本 p.629-637 共通): SM402 の後の母線から各出力命令が並列に分岐する。X55 は「指令速度(degree)」と「位置決めアドレス(degree)」の DMOVP の分岐にのみ直列に入る(上記ニモニックでは MPS/AND/MPP で表現)。同じ転送先への mm 用の DMOVP の後に degree 用の DMOVP が実行されるため，X55 ON時は degree 用の値で上書きされる。
- 原本 p.637 のコメント「加速時間No.0，減速時間No.:0」は原本表記のまま(「No.」の後のコロンなし)。

#### ブロック始動データ設定プログラム (12.4 / 原本 p.638)

エンジニアリングツールの"ブロック始動データ"にて設定する場合，本プログラムは不要です。

```
// No.3 ブロック始動データ設定プログラム
//   始動ブロック0のブロック始動データ(軸1)
//   1～5ポイント目までの設定の場合
//     (条件)
//       形態:1～4ポイント目は続行，5ポイント目は終了
//       特殊始動命令:1～5ポイント目まですべて通常始動
//       <位置決めデータはあらかじめ設定済みとする>
//
//     【形態，始動No.の設定】
(4182) LD    SM402              // SM402: RUN後1スキャンのみON
       // <続行，始動データNo.1を設定>
       MOVP  H8001 D68    // D68: 1ポイント目(形態，始動No.)
       // <続行，始動データNo.4を設定>
       MOVP  H8004 D69    // D69: 2ポイント目(形態，始動No.)
       // <続行，始動データNo.5を設定>
       MOVP  H8005 D70    // D70: 3ポイント目(形態，始動No.)
       // <続行，始動データNo.10を設定>
       MOVP  H800A D71    // D71: 4ポイント目(形態，始動No.)
       // <終了，始動データNo.15を設定>
       MOVP  H0F D72    // D72: 5ポイント目(形態，始動No.)
       // <ブロック始動データの設定>
       TOP   H1 K22000 D68 K5    // D68: 1ポイント目(形態，始動No.)

//   【特殊始動命令を通常始動に設定】
(4443) LD    SM402              // SM402: RUN後1スキャンのみON
       // <通常始動を設定>
       MOVP  H0 D73    // D73: 1ポイント目(特殊始動命令)
       // <通常始動を設定>
       MOVP  H0 D74    // D74: 2ポイント目(特殊始動命令)
       // <通常始動を設定>
       MOVP  H0 D75    // D75: 3ポイント目(特殊始動命令)
       // <通常始動を設定>
       MOVP  H0 D76    // D76: 4ポイント目(特殊始動命令)
       // <通常始動を設定>
       MOVP  H0 D77    // D77: 5ポイント目(特殊始動命令)
       // <ブロック始動データの設定>
       TOP   H1 K22050 D73 K5    // D73: 1ポイント目(特殊始動命令)
```

#### サーボパラメータ設定プログラム (12.4 / 原本 p.639)

エンジニアリングツールの"サーボパラメータ"にて設定する場合，本プログラムは不要です。

```
// No.4 サーボパラメータ
(4576) LD    SM402              // SM402: RUN後1スキャンのみON
       // <絶対位置システム有り>
       TOP   H1 K28403 H1 K1
       // <サーボシリーズ(MR-J4-B)>
       TOP   H1 K28400 K32 K1
```

#### 原点復帰要求OFFプログラム (12.4 / 原本 p.639)

エンジニアリングツールの"原点復帰詳細パラメータ"にて"[Pr.55]原点復帰未完時操作設定"を「1: 位置決め制御を実行する」に設定した場合，本プログラムは不要です。

```
// No.5 原点復帰要求OFFプログラム
(4659) LD    X0                 // X0: 原点復帰要求OFF指令
       // <原点復帰要求OFF指令のパルス化>
       PLS   M1                 // M1: 原点復帰要求OFF指令パルス
(4723) LD    M1                 // M1: 原点復帰要求OFF指令パルス
       ANI   U1\G30104.0        // U1\G30104.0: 位置決め始動信号(軸1)
       ANI   U1\G2417.E         // U1\G2417.E: 始動完了信号(軸1)
       // <原点復帰要求OFF指令の保持>
       SET   M2                 // M2: 原点復帰要求OFF指令記憶
(4755) LD    M2                 // M2: 原点復帰要求OFF指令記憶
       WANDP U1\G2417 H8 D0     // U1\G2417: ステータス / D0: 原点復帰要求フラグ
       MPS
       AND<> D0 K0              // D0: 原点復帰要求フラグ
       // <原点復帰要求OFF指令のON>
       SET   M0                 // M0: 原点復帰要求OFF指令
       MPP
       // <原点復帰要求OFF指令記憶のOFF>
       RST   M2                 // M2: 原点復帰要求OFF指令記憶
(4822) LD    M0                 // M0: 原点復帰要求OFF指令
       // <原点復帰要求OFF書込み>
       MOVP  K1 U1\G4321        // U1\G4321: 原点復帰要求フラグOFF要求
       AND=  U1\G4321 K0        // U1\G4321: 原点復帰要求フラグOFF要求
       // <原点復帰要求フラグOFF指令のOFF>
       RST   M0                 // M0: 原点復帰要求OFF指令
```

- 原本のラダー図ではバッファメモリの表記は「U1¥G30104.0」「U1¥G2417.E」「U1¥G2417」「U1¥G4321」(¥はバックスラッシュ)。
- U1\G30104.0 と U1\G2417.E は b接点(原本図の接点記号から判読)。
- ステップ(4755)の回路: M2 の後で分岐し，WANDP，[<> D0 K0]→SET M0，RST M2 の3つが並列。ステップ(4822)の回路: M0 の後で分岐し，MOVP K1 U1\G4321 と [= U1\G4321 K0]→RST M0 が並列。

#### 外部指令機能有効設定プログラム (12.4 / 原本 p.639)

```
// No.6 外部指令機能有効設定プログラム
(4884) LD    X1                 // X1: 外部指令有効指令
       // <外部指令有効の書込み>
       MOVP  K1 U1\G4305        // U1\G4305: 外部指令有効
(4945) LD    X2                 // X2: 外部指令無効指令
       // <外部指令無効の書込み>
       MOVP  K0 U1\G4305        // U1\G4305: 外部指令有効
```

- 本プログラムは原本 p.639 で完結している(原本 p.640 は「シーケンサレディ信号ONプログラム」から始まる)。

#### シーケンサレディ信号ONプログラム (12.4 / 原本 p.640)

【図】No.7 [Cd.190]シーケンサレディ信号ONプログラム(ラダー図)(原本 p.640)

```text
// No.7 [Cd.190]シーケンサレディ信号ONプログラム
(4970)
// <シーケンサレディ信号のON/OFF>
      LD    SM403                    // RUN後1スキャンOFF
      AND   M50                      // パラメータ設定完了デバイス
      ANI   M25                      // パラメータ初期化指令記憶
      ANI   M27                      // フラッシュROM書込み指令記憶
      AND   X53                      // シーケンサレディ信号ON
      OUT   U1\G5950.0               // シーケンサレディ信号
```

- 接点種別(図から判読): M25，M27はb接点，SM403，M50，X53はa接点。
- 原本の図中のバッファメモリ表記は「U1¥G5950.0」(ニモニック中では U1\G と表記。以下同じ)。

#### 全軸サーボONプログラム (12.4 / 原本 p.640)

【図】No.8 [Cd.191]全軸サーボON信号ONプログラム(ラダー図)(原本 p.640)

```text
// No.8 [Cd.191]全軸サーボON信号ONプログラム
(5060)
// <全軸サーボON>
      LD    X57                      // 全軸サーボON指令
      AND   U1\G5950.0               // シーケンサレディ信号
      AND   U1\G31500.1              // 同期用フラグ
      OUT   U1\G5951.0               // 全軸サーボON信号
```

- 接点種別(図から判読): すべてa接点。

#### 位置決め始動番号設定プログラム (12.4 / 原本 p.641-642)

【図】No.9 位置決め始動番号設定プログラム(ラダー図)(原本 p.641-642)

```text
// No.9 位置決め始動番号設定プログラム
// (1)機械原点復帰
(5136)
// <機械原点復帰(9001)の書込み>
      LD    X3                       // 機械原点復帰指令
      MOVP  K9001 D32                // D32: 始動番号

// (2)高速原点復帰
(5212)
      LD    X4                       // 高速原点復帰指令
// <原点復帰要求フラグのON/OFFの抽出>
      WANDP U1\G2417 H8 D0           // U1\G2417: ステータス / D0: 原点復帰要求フラグ
      MPS
// <高速原点復帰の始動許可>
      AND=  D0 K0                    // D0: 原点復帰要求フラグ
      SET   M3                       // 高速原点復帰指令
      MRD
// <高速原点復帰(9002)の書込み>
      MOVP  K9002 D32                // D32: 始動番号
      MPP
// <高速原点復帰指令の保持>
      SET   M4                       // 高速原点復帰指令記憶

// (3)位置決めデータNo.1による位置決め
(5338)
// <位置決めデータNo.1の設定>
      LD    X5                       // 位置決め始動指令
      MOVP  K1 D32                   // D32: 始動番号

// (4)速度・位置切換え運転(位置決めデータNo.2)
//    (ABSモードの場合，変更後の移動量書込みは不要)
(5381)
// <位置決めデータNo.2の設定>
      LD    X6                       // 速度・位置切換え運転指令
      MOVP  K2 D32                   // D32: 始動番号
(5429)
// <速度・位置切換え信号の許可設定>
      LD    X7                       // 速度・位置切換え許可指令
      MOVP  K1 U1\G4328              // U1\G4328: 速度・位置切換え許可フラグ
(5460)
// <速度・位置切換え信号の禁止設定>
      LD    X10                      // 速度・位置切換え禁止指令
      MOVP  K0 U1\G4328              // U1\G4328: 速度・位置切換え許可フラグ
(5491)
// <変更後の移動量書込み>
      LD    X11                      // 移動量変更指令
      DMOVP D3 U1\G4326              // D3: 移動量(下位16ビット) / U1\G4326: 速度・位置切換え制御移動量

// (5)位置・速度切換え運転(位置決めデータNo.3)     ← 原本 p.642
(5516)
// <位置決めデータNo.3の設定>
      LD    X40                      // 位置・速度切換え運転指令
      MOVP  K3 D32                   // D32: 始動番号
(5559)
// <位置・速度切換え信号の許可設定>
      LD    X41                      // 位置・速度切換え許可指令
      ANI   X42                      // 位置・速度切換え禁止指令
      MOVP  K1 U1\G4332              // U1\G4332: 位置・速度切換え許可フラグ
(5592)
// <位置・速度切換え信号の禁止設定>
      LDI   X41                      // 位置・速度切換え許可指令
      AND   X42                      // 位置・速度切換え禁止指令
      MOVP  K0 U1\G4332              // U1\G4332: 位置・速度切換え許可フラグ
(5625)
// <変更後の速度書込み>
      LD    X43                      // 速度変更指令
      DMOVP D1 U1\G4330              // D1: 速度(下位16ビット) / U1\G4330: 位置・速度切換え制御速度変更

// (6)高度な位置決め制御
(5649)
      LD    X12                      // 高度な位置決め制御始動指令
// <ブロック位置決め(7000)の書込み>
      MOVP  K7000 D32                // D32: 始動番号
// <位置決め始動ポイント番号(1)の書込み>
      MOVP  K1 U1\G4301              // U1\G4301: 位置決め始動ポイント番号

// (7)高速原点復帰指令，高速原点復帰指令記憶のOFF
//    (高速原点復帰を使用しない場合は不要)
(5729)
      LD    X3                       // 機械原点復帰指令
      OR    X5                       // 位置決め始動指令
      OR    X6                       // 速度・位置切換え運転指令
      OR    X40                      // 位置・速度切換え運転指令
      OR    X12                      // 高度な位置決め制御始動指令
      OR    M6                       // 位置決め始動指令記憶
// <高速原点復帰指令のOFF>
      RST   M3                       // 高速原点復帰指令
// <高速原点復帰指令記憶のOFF>
      RST   M4                       // 高速原点復帰指令記憶
```

- 接点種別(図から判読): (5559)のX42，(5592)のX41はb接点。他はすべてa接点。
- (5212)は X4 の後，WANDP を直結し，その後の分岐で「= D0 K0」→ SET M3，(接点なし)→ MOVP K9002 D32，(接点なし)→ SET M4 の3分岐(図から判読)。MPS/MRD/MPP は分岐構造を表すための書き起こし。
- (5649)は X12 の後で MOVP K7000 D32 と MOVP K1 U1\G4301 の並列出力(同一条件)。
- (5729)は X3，X5，X6，X40，X12，M6 の6接点のOR(並列)で，RST M3 と RST M4 の並列出力(同一条件)。
- 原本では (5)〜(7) は p.642 に続く。

#### 位置決め始動プログラム (12.4 / 原本 p.643)

【図】No.10 位置決め始動プログラム(ラダー図)(原本 p.643)

```text
// No.10 位置決め始動プログラム
//   (高速原点復帰を行わない場合，M3，M4の接点は不要)
//   (Mコードを使用しない場合，U0¥G2417.Cの接点は不要)
//   (JOG運転/インチング運転を行わない場合，M7の接点は不要)
//   (手動パルサ運転を行わない場合，M9の接点は不要)
(5807)
// <位置決め始動指令のパルス化>
      LD    X56                      // 位置決め始動信号指令
      PLS   M5                       // 位置決め始動指令パルス
(5886)
// <位置決め始動指令の保持>
      LD    M5                       // 位置決め始動指令パルス
      ANI   U1\G30104.0              // 位置決め始動信号(軸1)
      ANI   U1\G2417.E               // 始動完了信号(軸1)
      ANI   U1\G2417.C               // MコードON信号(軸1)
      ANI   M7                       // JOG/インチング運転中フラグ
      ANI   M9                       // 手動パルサ運転中フラグ
      LDI   M3                       // 高速原点復帰指令
      LD    M3                       // 高速原点復帰指令
      AND   M4                       // 高速原点復帰指令記憶
      ORB
      ANB
      SET   M6                       // 位置決め始動指令記憶
(5929)
      LD    M6                       // 位置決め始動指令記憶
// <位置決め始動No.の設定>
      MOVP  D32 U1\G4300             // D32: 始動番号 / U1\G4300: 位置決め始動番号
// <位置決め始動の実行>
      SET   U1\G30104.0              // 位置決め始動信号(軸1)
// <位置決め始動指令記憶のOFF>
      RST   M6                       // 位置決め始動指令記憶
(6000)
// <位置決め始動信号のOFF>
      LD    U1\G30104.0              // 位置決め始動信号(軸1)
      LD    U1\G2417.E               // 始動完了信号(軸1)
      OR    U1\G2417.D               // エラー検出信号(軸1)
      ANB
      ANI   U1\G31501.0              // BUSY信号(軸1)
      RST   U1\G30104.0              // 位置決め始動信号(軸1)
```

- 接点種別(図から判読): (5886)の U1\G30104.0，U1\G2417.E，U1\G2417.C，M7，M9，上段のM3はb接点，下段のM3，M4とM5はa接点。(6000)の U1\G31501.0 はb接点，他はa接点。
- (5886)の末尾は「M3(b接点)」と「M3(a接点)・M4(a接点)の直列」の並列回路(図から判読)。
- (6000)は「U1\G2417.E」と「U1\G2417.D」の並列回路。
- 冒頭注記の「U0¥G2417.C」は原本の注記の表記のまま(ラダー上の接点は U1¥G2417.C。要確認)。

#### ＭコードOFFプログラム (12.4 / 原本 p.643)

【図】No.11 MコードOFFプログラム(ラダー図)(原本 p.643)

```text
// No.11 MコードOFFプログラム
//   (Mコードを使用しない場合は不要)
(6036)
// <MコードOFF要求書込み>
      LD    X14                      // MコードOFF指令
      AND   U1\G2417.C               // MコードON信号(軸1)
      MOVP  K1 U1\G4304              // U1\G4304: MコードOFF要求(バッファメモリ)
```

- 接点種別(図から判読): すべてa接点。

#### JOG運転設定プログラム (12.4 / 原本 p.644)

【図】No.12 JOG運転設定プログラム(ラダー図)(原本 p.644)

```text
// No.12 JOG運転設定プログラム
(6257)
      LD    X15                      // JOG運転速度設定指令
// <JOG運転速度(100.00 mm/min)の設定>
      DMOVP K10000 D6                // D6: JOG運転速度(下位16ビット)
      MPS
      AND   X55                      // 単位(degree)の場合
// <JOG運転速度(1200.000 degree/min)の設定>
      DMOVP K1200000 D6              // D6: JOG運転速度(下位16ビット)
      MPP
// <インチング移動量に(0)を設定>
      MOVP  K0 D5                    // D5: インチング移動量
// <JOG運転速度の書込み>
      TOP   H1 K4317 D5 K3           // D5: インチング移動量
```

- 接点種別(図から判読): すべてa接点。
- X15 の後の4分岐: (接点なし)→ DMOVP K10000 D6，X55 → DMOVP K1200000 D6，(接点なし)→ MOVP K0 D5，(接点なし)→ TOP H1 K4317 D5 K3。

#### インチング運転設定プログラム (12.4 / 原本 p.644)

【図】No.13 インチング運転設定プログラム(ラダー図)(原本 p.644)

```text
// No.13 インチング運転設定プログラム
(6431)
      LD    X44                      // インチング移動量設定指令
      ANI   X15                      // JOG運転速度設定指令
// <インチング移動量(10.0 μm)の設定>
      MOVP  K100 D5                  // D5: インチング移動量
// <インチング移動量の書込み>
      MOVP  D5 U1\G4317              // D5: インチング移動量 / U1\G4317: インチング移動量
```

- 接点種別(図から判読): X15はb接点，X44はa接点。

#### JOG運転／インチング運転実行プログラム (12.4 / 原本 p.644)

【図】No.14 JOG運転/インチング運転実行プログラム(ラダー図)(原本 p.644)

```text
// No.14 JOG運転/インチング運転実行プログラム
(6529)
// <JOG/インチング運転中フラグのON>
      LD    X16                      // 正転JOG/インチング指令
      OR    X17                      // 逆転JOG/インチング指令
      AND   U1\G31500.0              // 準備完了信号
      ANI   U1\G31501.0              // BUSY信号(軸1)
      SET   M7                       // JOG/インチング運転中フラグ
(6609)
// <JOG/インチング運転終了>
      LDI   X16                      // 正転JOG/インチング指令
      ANI   X17                      // 逆転JOG/インチング指令
      RST   M7                       // JOG/インチング運転中フラグ
(6636)
// <正転JOG/インチング運転の実行>
      LD    X16                      // 正転JOG/インチング指令
      AND   M7                       // JOG/インチング運転中フラグ
      ANI   U1\G30102.0              // 逆転JOG始動信号(軸1)
      OUT   U1\G30101.0              // 正転JOG始動信号(軸1)
(6670)
// <逆転JOG/インチング運転の実行>
      LD    X17                      // 逆転JOG/インチング指令
      AND   M7                       // JOG/インチング運転中フラグ
      ANI   U1\G30101.0              // 正転JOG始動信号(軸1)
      OUT   U1\G30102.0              // 逆転JOG始動信号(軸1)
```

- 接点種別(図から判読): (6529)の U1\G31501.0，(6609)の X16・X17，(6636)の U1\G30102.0，(6670)の U1\G30101.0 はb接点。他はa接点。
- (6529)は X16 と X17 の並列回路の後に U1\G31500.0，U1\G31501.0 が直列。

#### 手動パルサ運転プログラム (12.4 / 原本 p.645)

【図】No.15 手動パルサ運転プログラム(ラダー図)(原本 p.645)

```text
// No.15 手動パルサ運転プログラム
(6547)
// <手動パルサ運転指令のパルス化>
      LD    X20                      // 手動パルサ運転許可指令
      PLS   M8                       // 手動パルサ運転許可指令
(6608)
      LD    M8                       // 手動パルサ運転許可指令
      AND   U1\G31500.0              // 準備完了信号
      ANI   U1\G31501.0              // BUSY信号(軸1)
// <手動パルサ1パルス入力倍率を設定>
      DMOVP K1 D8                    // D8: 手動パルサ1パルス入力倍率(下位)
// <手動パルサ運転許可の書込み>
      MOVP  K1 D10                   // D10: 手動パルサ運転許可
// <手動パルサ用データ書込み>
      TOP   H1 K4322 D8 K3           // D8: 手動パルサ1パルス入力倍率(下位)
// <手動パルサ運転中フラグのON>
      SET   M9                       // 手動パルサ運転中フラグ
(6720)
// <手動パルサ運転不許可指令パルス化>
      LD    X21                      // 手動パルサ運転不許可指令
      PLS   M10                      // 手動パルサ運転不許可指令
(6749)
      LD    M10                      // 手動パルサ運転不許可指令
      AND   M9                       // 手動パルサ運転中フラグ
      AND   U1\G31501.0              // BUSY信号(軸1)
// <手動パルサ運転不許可の書込み>
      MOVP  K0 U1\G4324              // U1\G4324: 手動パルサ許可フラグ
// <手動パルサ運転中フラグのOFF>
      RST   M9                       // 手動パルサ運転中フラグ
```

- 接点種別(図から判読): (6608)の U1\G31501.0 はb接点。(6749)の U1\G31501.0 はa接点(拡大して確認。原本のまま)。他はa接点。
- (6608)は同一条件で DMOVP，MOVP，TOP，SET の並列出力。(6749)は同一条件で MOVP，RST の並列出力。
- ステップ番号は原本の図の表記のまま((6547)〜(6749))。

#### 速度変更プログラム (12.4 / 原本 p.646)

【図】No.16 速度変更プログラム(ラダー図)(原本 p.646)

```text
// No.16 速度変更プログラム
(6966)
// <速度変更指令のパルス化>
      LD    X22                      // 速度変更指令
      PLS   M11                      // 速度変更指令パルス
(7020)
// <速度変更指令の保持>
      LD    M11                      // 速度変更指令パルス
      AND   U1\G31501.0              // BUSY信号(軸1)
      SET   M12                      // 速度変更指令記憶
(7043)
      LD    M12                      // 速度変更指令記憶
// <速度変更値(90.00 mm/min)の設定>
      DMOVP K9000 D11                // D11: 速度変更値(下位16ビット)
      MPS
      AND   X55                      // 単位(degree)の場合
// <速度変更値(3600.000 degree/min)の設定>
      DMOVP K3600000 D11             // D11: 速度変更値(下位16ビット)
      MRD
// <速度変更要求の設定>
      MOVP  K1 D13                   // D13: 速度変更要求
      MRD
// <速度変更の書込み>
      TOP   H1 K4314 D11 K3          // D11: 速度変更値(下位16ビット)
      MPP
// <速度変更要求記憶のOFF>
      AND=  U1\G4316 K0              // U1\G4316: 速度変更要求
      RST   M12                      // 速度変更指令記憶
```

- 接点種別(図から判読): すべてa接点。
- (7043)は M12 の後の5分岐: (接点なし)→ DMOVP K9000 D11，X55 → DMOVP K3600000 D11，(接点なし)→ MOVP K1 D13，(接点なし)→ TOP H1 K4314 D11 K3，「= U1\G4316 K0」→ RST M12。

#### オーバーライドプログラム (12.4 / 原本 p.646)

【図】No.17 オーバーライドプログラム(ラダー図)(原本 p.646)

```text
// No.17 オーバーライドプログラム
(8354)
// <オーバーライド指令>
      LD    X23                      // オーバーライド指令
      PLS   M13                      // オーバーライド指令
(8405)
      LD    M13                      // オーバーライド指令
      AND   U1\G31501.0              // BUSY信号(軸1)
// <オーバーライド値を(200%)に設定>
      MOV   K200 D14                 // D14: オーバーライド値
// <オーバーライド値の書込み>
      MOV   D14 U1\G4313             // D14: オーバーライド値 / U1\G4313: オーバーライド
(8466)
// <オーバーライド指令>
      LD    X50                      // オーバーライド初期値指令
      PLS   M40                      // オーバーライド初期値指令
(8487)
      LD    M40                      // オーバーライド初期値指令
      ANI   U1\G31501.0              // BUSY信号(軸1)
// <オーバーライド値を初期値(100%)に設定>
      MOV   K100 D14                 // D14: オーバーライド値
// <オーバーライド値の書込み>
      MOV   D14 U1\G4313             // D14: オーバーライド値 / U1\G4313: オーバーライド
```

- 接点種別(図から判読): (8487)の U1\G31501.0 はb接点。(8405)の U1\G31501.0 を含め他はa接点。
- 原本の図の MOV 命令はパルス形(MOVP)ではなく「MOV」表記(原本のまま)。
- (8466)の見出しは原本の図のまま「<オーバーライド指令>」。
- ステップ番号は原本の図の表記のまま((8354)〜(8487))。

#### 加減速時間変更プログラム (12.4 / 原本 p.647)

【図】No.18 加減速時間変更プログラム(ラダー図)(原本 p.647)

```text
// No.18 加減速時間変更プログラム
(7225)
// <加減速時間変更指令のパルス化>
      LD    X24                      // 加減速時間変更指令
      ANI   X25                      // 加減速時間変更不許可指令
      PLS   M14                      // 加減速時間変更指令
(7288)
      LD    M14                      // 加減速時間変更指令
      AND   U1\G31501.0              // BUSY信号(軸1)
// <加速時間を(2000ms)に設定>
      DMOV  K2000 D15                // D15: 加速時間設定(下位16ビット)
// <減速時間を変更無(0)に設定>
      DMOV  K0 D17                   // D17: 減速時間設定(下位16ビット)
// <加減速時間の書込み>
      MOVP  K1 D19                   // D19: 加減速時間変更許可
// <加減速時間/変更許可の書込み>
      TOP   H1 K4308 D15 K5          // D15: 加速時間設定(下位16ビット)
(7397)
// <加減速時間の変更不許可の書込み>
      LD    X25                      // 加減速時間変更不許可指令
      ANI   X24                      // 加減速時間変更指令
      MOVP  K0 U1\G4312
```

- 接点種別(図から判読): (7225)の X25，(7397)の X24 はb接点。他はa接点。
- (7288)は同一条件で DMOV，DMOV，MOVP，TOP の並列出力。
- (7397)の出力先 U1\G4312 にはデバイスコメントの記載なし(原本のまま)。

#### トルク変更プログラム (12.4 / 原本 p.647)

【図】No.19 トルク変更プログラム(ラダー図)(原本 p.647)

```text
// No.19 トルク変更プログラム
(7430)
      LD    X26                      // トルク変更指令
// <トルク変更値を(100%)に設定>
      MOVP  K1000 D78                // D78: トルク変更値
// <トルク変更指令のパルス化>
      PLS   M15                      // トルク変更指令
(7515)
// <トルク制限値の変更>
      LD    M15                      // トルク変更指令
      AND   U1\G31501.0              // BUSY信号(軸1)
      MOVP  D78 U1\G4325             // D78: トルク変更値
```

- 接点種別(図から判読): すべてa接点。
- (7430)は同一条件で MOVP と PLS の並列出力。

#### ステップ運転プログラム (12.4 / 原本 p.648)

【図】No.20 ステップ運転プログラム(ラダー図)(原本 p.648)

```text
// No.20 ステップ運転プログラム
(7542)
      LD    X27                      // ステップ運転指令
// <ステップ運転指令のパルス化>
      PLS   M16                      // ステップ運転指令パルス
// <始動プログラム(K10)を設定>
      MOVP  K10 D32                  // D32: 始動番号
(7628)
      LD    M16                      // ステップ運転指令パルス
      ANI   U1\G30104.0              // 位置決め始動信号(軸1)
      ANI   U1\G2417.E               // 始動完了信号(軸1)
// <ステップ動作を行うを選択>
      MOVP  K1 D20                   // D20: ステップモード
// <データNo.単位ステップモード選択>
      MOVP  K1 D21                   // D21: ステップ有効フラグ
// <ステップ始動情報(1:ステップ続行)>
      MOVP  K1 D22                   // D22: ステップ始動情報
// <ステップ運転指令の書込み>
      DMOVP D20 U1\G4344             // D20: ステップモード / U1\G4344: ステップモード
(7745)
// <次の位置決めデータへ>
      LD    X46                      // ステップ始動情報指令
      MOVP  D22 U1\G4346             // D22: ステップ始動情報
```

- 接点種別(図から判読): (7628)の U1\G30104.0，U1\G2417.E はb接点。他はa接点。
- (7542)は同一条件で PLS と MOVP の並列出力。(7628)は同一条件で MOVP×3，DMOVP の並列出力。

#### スキッププログラム (12.4 / 原本 p.648)

【図】No.21 スキッププログラム(ラダー図)(原本 p.648)

```text
// No.21 スキッププログラム
(7933)
// <位置決め始動番号(No.10)を設定>
      LD    X47                      // 位置決め始動指令(K10)
      MOVP  K10 D32                  // D32: 始動番号
(7996)
// <スキップのパルス化>
      LD    X30                      // スキップ指令
      PLS   M17                      // スキップ指令パルス
(8017)
// <スキップ指令記憶のON>
      LD    M17                      // スキップ指令パルス
      AND   U1\G31501.0              // BUSY信号(軸1)
      SET   M18                      // スキップ指令記憶
(8042)
      LD    M18                      // スキップ指令記憶
      MPS
// <スキップ指令の書込み>
      MOVP  K1 U1\G4347              // U1\G4347: スキップ指令
      MPP
// <スキップ指令記憶のOFF>
      AND=  U1\G4347 K0              // U1\G4347: スキップ指令
      RST   M18                      // スキップ指令記憶
```

- 接点種別(図から判読): すべてa接点。
- (8042)は M18 の後の2分岐: (接点なし)→ MOVP K1 U1\G4347，「= U1\G4347 K0」→ RST M18。(MPS/MPP は分岐構造を表すための書き起こし。)
- (7933)の図中，D32 のデバイスコメント欄に「D32; 始動番号」というツールチップ(吹き出し)が重なって写り込んでいる(原本のまま)。

#### ティーチングプログラム (12.4 / 原本 p.649)

【図】No.22 ティーチングプログラム(ラダー図)(原本 p.649)

```text
// No.22 ティーチングプログラム
//   (手動操作で目的位置への位置決めを行う)
(8095)
// <ティーチング指令のパルス化>
      LD    X31                      // ティーチング指令
      PLS   M19                      // ティーチング指令パルス
(8159)
// <ティーチング指令の保持>
      LD    M19                      // ティーチング指令パルス
      ANI   U1\G31501.0              // BUSY信号(軸1)
      SET   M20                      // ティーチング指令記憶
(8184)
      LD    M20                      // ティーチング指令記憶
      MPS
// <位置決めアドレスをティーチング>
      MOVP  K0 U1\G4348              // U1\G4348: ティーチングデータ選択
// <ティーチング位置決めデータNo.7を(1)に設定>
      MOVP  K1 U1\G4349              // U1\G4349: ティーチング位置決めデータNo.
      MPP
// <ティーチング指令記憶のOFF>
      AND=  U1\G4349 K0              // U1\G4349: ティーチング位置決めデータNo.
      RST   M20                      // ティーチング指令記憶
```

- 接点種別(図から判読): (8159)の U1\G31501.0 はb接点。他はa接点。
- (8184)は M20 の後の3分岐: (接点なし)→ MOVP K0 U1\G4348，(接点なし)→ MOVP K1 U1\G4349，「= U1\G4349 K0」→ RST M20。
- 図中の見出しは原本のまま「<ティーチング位置決めデータNo.7を(1)に設定>」(命令は MOVP K1 U1\G4349)。

#### 連続運転中断プログラム (12.4 / 原本 p.649)

【図】No.23 連続運転中断プログラム(ラダー図)(原本 p.649)

```text
// No.23 連続運転中断プログラム
(8283)
// <連続運転中断指令のパルス化>
      LD    X32                      // 連続運転中断指令
      PLS   M21                      // 連続運転中断指令
(8342)
// <連続運転中断の書込み>
      LD    M21                      // 連続運転中断指令
      AND   U1\G31501.0              // BUSY信号(軸1)
      MOVP  K1 U1\G4320              // U1\G4320: 連続運転中断要求
```

- 接点種別(図から判読): すべてa接点。

#### 目標位置変更プログラム (12.4 / 原本 p.650)

【図】No.24 目標位置変更プログラム(ラダー図)(原本 p.650)

```text
// No.24 目標位置変更プログラム
(8370)
// <目標位置変更指令のパルス化>
      LD    X45                      // 目標位置変更指令
      PLS   M30                      // 目標位置変更指令パルス
(8429)
// <目標位置変更指令の保持>
      LD    M30                      // 目標位置変更指令パルス
      AND   U1\G31501.0              // BUSY信号(軸1)
      SET   M31                      // 目標位置変更指令記憶
(8454)
      LD    M31                      // 目標位置変更指令記憶
// <目標アドレス(-12000.0 μm)の設定>
      DMOVP K-120000 D23             // D23: 目標位置(下位16ビット)
      MPS
      AND   X55                      // 単位(degree)の場合
// <目標アドレス(300.00000 degree)の設定>
      DMOVP K30000000 D23            // D23: 目標位置(下位16ビット)
      MRD
// <速度変更(0:速度変更しない)>
      DMOVP K0 D25                   // D25: 目標速度(下位16ビット)
      MRD
// <目標位置変更要求の設定>
      MOVP  K1 D27                   // D27: 目標位置変更要求
      MRD
// <目標位置変更の書込み>
      TOP   H1 K4334 D23 K5          // D23: 目標位置(下位16ビット)
      MPP
// <目標位置変更指令記憶のOFF>
      AND=  U1\G4338 K0              // U1\G4338: 目標位置変更要求フラグ
      RST   M31                      // 目標位置変更指令記憶
```

- 接点種別(図から判読): すべてa接点。
- (8454)は M31 の後の6分岐: (接点なし)→ DMOVP K-120000 D23，X55 → DMOVP K30000000 D23，(接点なし)→ DMOVP K0 D25，(接点なし)→ MOVP K1 D27，(接点なし)→ TOP H1 K4334 D23 K5，「= U1\G4338 K0」→ RST M31。

#### 再始動プログラム (12.4 / 原本 p.650)

【図】No.25 再始動プログラム(ラダー図)(原本 p.650)

```text
// No.25 再始動プログラム
(8471)
// <再始動指令のパルス化>
      LD    X33                      // 再始動指令
      PLS   M22                      // 再始動指令
(8524)
// <停止中で再始動指令をON>
      LD    M22                      // 再始動指令
      AND=  U1\G2409 K1              // U1\G2409: 軸動作状態
      SET   M23                      // 再始動指令記憶
(8554)
      LD    M23                      // 再始動指令記憶
      ANI   U1\G2417.F               // 位置決め完了信号(軸1)
      ANI   U1\G2417.E               // 始動完了信号(軸1)
      MPS
// <再始動要求の書込み>
      MOVP  K1 U1\G4303              // U1\G4303: 再始動命令
      MPP
// <再始動指令記憶のOFF>
      AND=  U1\G… K0                 // 再始動命令 (デバイス番号は原本の図で「U1¥G…」と省略表示。判読不可。要確認)
      RST   M23                      // 再始動指令記憶
```

- 接点種別(図から判読): (8554)の U1\G2417.F，U1\G2417.E はb接点。他はa接点。
- (8554)は3接点の後の2分岐: (接点なし)→ MOVP K1 U1\G4303，「= U1¥G… K0」→ RST M23。
- 比較命令のデバイスは原本の図で「U1¥G…」と省略表示されている(コメントは「再始動命令」)。デバイス番号は図から判読不可(原本 p.650 参照)。

#### パラメータ初期化プログラム (12.4 / 原本 p.651)

【図】No.26 パラメータの初期化プログラム(ラダー図)(原本 p.651)

```text
// No.26 パラメータの初期化プログラム
(8610)
// <パラメータ初期化指令のパルス化>
      LD    X34                      // パラメータ初期化指令
      PLS   M24                      // パラメータ初期化指令パルス
(8674)
// <パラメータ初期化指令の保持>
      LD    M24                      // パラメータ初期化指令パルス
      ANI   U1\G31501.0              // BUSY信号(軸1)
      SET   M25                      // パラメータ初期化指令記憶
(8702)
// <シーケンサレディ出力待ち>
      LD    M25                      // パラメータ初期化指令記憶
      ANI   U1\G5950.0               // シーケンサレディ信号
      OUT   T0 K2                    // T0: シーケンサレディ信号OFF確認
(8732)
      LD    T0                       // シーケンサレディ信号OFF確認
      MPS
// <パラメータ初期化の実行>
      MOVP  K1 U1\G5901              // U1\G5901: パラメータの初期化要求
      MPP
// <パラメータ初期化指令記憶のOFF>
      AND=  U1\G5901 K0              // U1\G5901: パラメータの初期化要求
      RST   M25                      // パラメータ初期化指令記憶
```

- 接点種別(図から判読): (8674)の U1\G31501.0，(8702)の U1\G5950.0 はb接点。他はa接点。
- (8732)は T0 の後の2分岐: (接点なし)→ MOVP K1 U1\G5901，「= U1\G5901 K0」→ RST M25。

#### フラッシュROM書込みプログラム (12.4 / 原本 p.651)

【図】No.27 フラッシュROM書込みプログラム(ラダー図)(原本 p.651)

```text
// No.27 フラッシュROM書込みプログラム
(8790)
// <フラッシュROM書込み指令のパルス化>
      LD    X35                      // フラッシュROM書込み指令
      PLS   M26                      // フラッシュROM書込み指令パルス
(8859)
// <フラッシュROM書込み指令の保持>
      LD    M26                      // フラッシュROM書込み指令パルス
      ANI   U1\G31501.0              // BUSY信号(軸1)
      SET   M27                      // フラッシュROM書込み指令記憶
(8890)
// <シーケンサレディ出力待ち>
      LD    M27                      // フラッシュROM書込み指令記憶
      ANI   U1\G5950.0               // シーケンサレディ信号
      OUT   T1 K2                    // T1: シーケンサレディ信号OFF確認
(8920)
      LD    T1                       // シーケンサレディ信号OFF確認
      MPS
// <フラッシュROM書込みの実行>
      MOVP  K1 U1\G5900              // U1\G5900: フラッシュROM書込み要求
      MPP
// <フラッシュROM書込み指令記憶のOFF>
      AND=  U1\G5900 K0              // U1\G5900: フラッシュROM書込み要求
      RST   M27                      // フラッシュROM書込み指令記憶
```

- 接点種別(図から判読): (8859)の U1\G31501.0，(8890)の U1\G5950.0 はb接点。他はa接点。
- (8920)は T1 の後の2分岐: (接点なし)→ MOVP K1 U1\G5900，「= U1\G5900 K0」→ RST M27。

#### エラーリセットプログラム (12.4 / 原本 p.652)

【図】No.28 エラーリセットプログラム(ラダー図)(原本 p.652)

```text
// No.28 エラーリセットプログラム
(8985)
// <エラーコード読出し>
      LD    U1\G2417.D               // エラー検出信号(軸1)
      MOV   U1\G2406 D79             // U1\G2406: エラーコード / D79: エラーコード
(9044)
// <エラーリセット指令のパルス化>
      LD    X36                      // エラーリセット指令
      PLS   M28                      // エラーリセット
(9071)
// <エラーリセットの実行>
      LD    M28                      // エラーリセット
      AND   U1\G2417.D               // エラー検出信号(軸1)
      MOVP  K1 U1\G4302              // U1\G4302: エラーリセット
(9099)
// <エラーリセットクリアの実行>
      LD    X54                      // エラーリセットクリア指令
// 図中注記(X54 を指す吹き出し): エラーリセット要求時にサーボエラーのリセットが不可の場合，軸エラーリセットの値はシンプルモーションによって「0」が格納されず，「1」のままとなります。再度エラーリセットを行う場合は，いったん軸エラーリセットに「0」を設定した後，「1」を設定してください。
      MOVP  K0 U1\G4302              // U1\G4302: エラーリセット
```

- 接点種別(図から判読): すべてa接点。
- 図中の吹き出し注記は(9099)の X54(エラーリセットクリア指令)を指している(テキスト抽出では「軸停止プログラム」の後に出力されるが，図上の位置はエラーリセットプログラム内)。

本プログラムはエラーコードのみを格納，リセットするプログラムです。
ワーニングもリセットしたい場合は，ステップ9071でエラー検出信号(軸1)G2417.Dとワーニング検出信号(軸1)G2417.9に対してOR回路を作成してください。
また必要に応じて，ステップ8985を参考にワーニングコードを格納するプログラムを作成してください。

#### 軸停止プログラム (12.4 / 原本 p.652)

【図】No.29 停止プログラム(ラダー図)(原本 p.652)

```text
// No.29 停止プログラム
(9128)
// <停止指令のパルス化>
      LD    X37                      // 停止指令
      PLS   M29                      // 停止指令パルス
(9177)
// <停止の実行>
      LD    M29                      // 停止指令パルス
      AND   U1\G31501.0              // BUSY信号(軸1)
      SET   U1\G30100.0              // 軸停止信号(軸1)
(9197)
// <停止のクリア>
      LDI   X37                      // 停止指令
      ANI   U1\G31501.0              // BUSY信号(軸1)
      RST   U1\G30100.0              // 軸停止信号(軸1)
```

- 接点種別(図から判読): (9197)の X37，U1\G31501.0 はb接点。他はa接点。
