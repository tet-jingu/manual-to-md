# 三菱 MELSEC iQ-R シンプルモーションユニット ユーザーズマニュアル(応用編) 13 プログラミング 13.1 注意事項・13.2 ラベル一覧・13.3 プログラムの作成・13.4 プログラム例(前半)

| 項目 | 内容 |
|---|---|
| 原本 | 三菱電機 MELSEC iQ-R シンプルモーションユニット ユーザーズマニュアル(応用編)(対象形名: RD77MS2 / RD77MS4 / RD77MS8 / RD77MS16 / RD77GF4 / RD77GF8 / RD77GF16 / RD77GF32) |
| 発行元 | 三菱電機株式会社 |
| 資料番号・版数 | IB(名)-0300246-P (2509)MEE / P版 (2025年9月作成)。形名 RD77-U-APP |
| 原本PDF | `PDF/MELSEC iQ_Rシンプルモーションユニットユーザーズマニュアル(応用編).pdf` |
| 本ファイルの範囲 | 第13章 プログラミング の章冒頭、13.1 プログラム作成上の注意事項、13.2 使用するラベル一覧、13.3 プログラムの作成、13.4 位置決めプログラム例 のうち「パラメータ設定プログラム」「位置決めデータ設定プログラム」まで(印刷 p.668-677 / PDF p.670-679)。前ファイル(12章)は第12章まで、次ファイル(13b)は13.4の「ブロック始動データ設定プログラム」(印刷 p.678 / PDF p.680)から |
| ページ対応 | 印刷ページ = PDFページ − 2。本文中の「〇〇ページ参照」は印刷ページのまま |
| 変換日 | 2026-10-23 |
| 変換方法 | pypdfium2(本文) + PyMuPDF 200dpi 画像の目視(全ページ) |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。

転記上の扱い: 本文・注意事項は原文のまま全文転記した。ユニットラベル一覧表(13.2)は全行を転記し、結合セル(分類、および2つのラベルが1つの内容を共有する行)は各行に展開した。グローバルラベル一覧(原本ではGX Works3のラベル設定画面の画面図)は、PDFに埋め込まれた原寸画像を拡大して目視で読み取り、No.1～146の全行を表に起こした(画面図中の「...」ボタン列とクラス欄のプルダウン記号は画面部品のため転記していない)。13.3のプログラム全体構成表は全行転記し、結合された備考セルは各行に展開した。13.4のラダー図はすべて「図から書き起こし」のニモニックで示した(原本にニモニック記載は無い)。ステップ番号は原本のラダー図に表示されている回路先頭のステップ番号((0)、(38))のみを記し、表示されていない途中のステップ番号は推測で付けていない。ラベル名・デバイス名・バッファメモリ表記(`U0¥G0` 等)は原本の画面図どおりとした。ユニットFBの呼出し回路は、起動条件をニモニック、FB引数を表で示した。システム構成図は【図】プレースホルダと読み取れる事実の箇条書きで文章化した。

## 主要用語 対訳表 (Glossary) (13.1〜13.4 / 印刷 p.668-677 / 原本 p.670-679)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| プログラミング | Programming | 13章 | 参考訳 |
| プログラム作成上の注意事項 | Precautions for creating programs | 13.1 | 参考訳 |
| 使用するラベル一覧 | List of labels used | 13.2 | 参考訳 |
| ユニットラベル | Module label | — | 参考訳 |
| グローバルラベル | Global label | VAR_GLOBAL | 参考訳 |
| 割付けデバイス / 割付け(デバイス/ラベル) | Assigned device / Assignment (Device/Label) | — | 参考訳 |
| ユニットFB | Module FB | — | 参考訳 |
| 位置決めデータ設定FB | Positioning data setting FB | M+RD77_SetPositioningData_00E | 原本併記 |
| エンジニアリングツール | Engineering tool | — | 参考訳 |
| ユニットパラメータ | Module parameter | — | 参考訳 |
| スキャンタイム | Scan time | — | 参考訳 |
| 連続軌跡制御 / 連続位置決め制御 | Continuous path control / Continuous positioning control | — | 参考訳 |
| 速度変更機能 / オーバーライド機能 | Speed change function / Override function | — | 参考訳 |
| ストロークリミット上限値 / 下限値 | Stroke limit upper / lower limit value | [Pr.12] / [Pr.13] | 参考訳 |
| 限界リミットスイッチ | Limit switch (for overrun protection) | — | 参考訳 |
| 主回路電源 | Main circuit power supply | — | 参考訳 |
| 先頭I/O No. | Start I/O No. | RD77_1.uIO | 参考訳 |
| RD77準備完了 | RD77 READY | RD77_1.bReady | 参考訳 |
| RD77同期用フラグ | RD77 synchronization flag | RD77_1.bSynchronizationFlag / X1 | 参考訳 |
| BUSY信号 | BUSY signal | RD77_1.bnBusy[0] | 参考訳 |
| 全軸サーボON | All axis servo ON | RD77_1.bAllAxisServoOn / Y1 | 参考訳 |
| シーケンサレディ信号 | PLC READY signal | RD77_1.bPLC_Ready / Y0 | 参考訳 |
| 位置決め始動信号 | Positioning start signal | RD77_1.bnPositioningStart[0] | 参考訳 |
| 単位設定 | Unit setting | [Pr.1] / U0¥G0 | 参考訳 |
| 1回転あたりのパルス数(AP) | Number of pulses per rotation (AP) | [Pr.2] / U0¥G2 | 参考訳 |
| 1回転あたりの移動量(AL) | Movement amount per rotation (AL) | [Pr.3] / U0¥G4 | 参考訳 |
| 単位倍率(AM) | Unit magnification (AM) | [Pr.4] / U0¥G1 | 参考訳 |
| ソフトウェアストロークリミット上限値 / 下限値 | Software stroke limit upper / lower limit value | [Pr.12] U0¥G18 / [Pr.13] U0¥G20 | 参考訳 |
| 速度制御時の送り現在値 | Current feed value during speed control | [Pr.21] / U0¥G30 | 参考訳 |
| 速度･位置機能選択 | Speed-position function selection | [Pr.81] / U0¥G34 | 参考訳 |
| 外部指令機能選択 | External command function selection | [Pr.42] | 参考訳 |
| 原点復帰方式 | OPR method | [Pr.43] / U0¥G70 | 参考訳 |
| 原点復帰方向 | OPR direction | [Pr.44] / U0¥G71 | 参考訳 |
| 原点アドレス | OP address | [Pr.45] / U0¥G72 | 参考訳 |
| 原点復帰速度 | OPR speed | [Pr.46] / U0¥G74 | 参考訳 |
| クリープ速度 | Creep speed | [Pr.47] / U0¥G76 | 参考訳 |
| 原点復帰リトライ | OPR retry | [Pr.48] / U0¥G78 | 参考訳 |
| 送り現在値 | Current feed value | [Md.20] | 参考訳 |
| 有効Mコード | Valid M code | [Md.25] | 参考訳 |
| 原点復帰要求フラグ / 軸ワーニング検出 / MコードON / エラー検出 / 始動完了 / 位置決め完了 | OPR request flag / Axis warning detection / M code ON / Error detection / Start complete / Positioning complete | [Md.31] ステータス b3 / b9 / bC / bD / bE / bF | 参考訳 |
| SSCNET制御ステータス / SSCNET制御指令 | SSCNET control status / SSCNET control command | — | 参考訳 |
| 位置決め始動番号 | Positioning start No. | [Cd.3] | 参考訳 |
| MコードOFF要求 | M code OFF request | [Cd.7] | 参考訳 |
| 外部指令有効 | External command valid | [Cd.8] | 参考訳 |
| 原点復帰要求フラグOFF要求 | OPR request flag OFF request | [Cd.19] | 参考訳 |
| 実行命令 / 実行状態 / 正常終了 / エラー終了 / エラーコード | Execution command / Execution status / Normal completion / Error completion / Error code | i_bEN / o_bENO / o_bOK / o_bErr / o_uErrId | 参考訳 |
| 機械原点復帰制御 | Machine OPR control | — | 参考訳 |
| 位置決めデータ / ブロック始動データ / サーボパラメータ | Positioning data / Block start data / Servo parameter | — | 参考訳 |

## 変換範囲表 (13.1〜13.4 / 印刷 p.668-677 / 原本 p.670-679)

| 原本ページ | 節 | 扱い |
|---|---|---|
| PDF p.1-669 (印刷 p.-1～667) | 第1部～第12章 | 本ファイル対象外(他ファイル 00～12m で変換) |
| PDF p.670 (印刷 p.668) | 13章 冒頭、13.1 プログラム作成上の注意事項(データの読出し／書込み、速度変更実行間隔の制約、オーバーラン時の処理、システム構成) | 全文 |
| PDF p.671-675 (印刷 p.669-673) | 13.2 使用するラベル一覧(ユニットラベル、グローバルラベル) | 全文(全行) |
| PDF p.675 (印刷 p.673) | 13.3 プログラムの作成(プログラムの全体構成) | 全文 |
| PDF p.676-679 (印刷 p.674-677) | 13.4 位置決めプログラム例: 冒頭、パラメータ設定プログラム(基本パラメータ1、原点復帰基本パラメータ、単位degree用設定)、位置決めデータ設定プログラム | 全文(プログラム例を含む) |
| PDF p.680- (印刷 p.678-) | 13.4 ブロック始動データ設定プログラム 以降 | 本ファイル対象外(次ファイル 13b) |

## 目次

- 13 プログラミング
  - 13.1 プログラム作成上の注意事項
    - データの読出し／書込み
    - 速度変更実行間隔の制約
    - オーバーラン時の処理
    - システム構成
  - 13.2 使用するラベル一覧
    - ユニットラベル
    - グローバルラベル(割付けデバイスを設定する／設定しない)
  - 13.3 プログラムの作成
    - プログラムの全体構成
  - 13.4 位置決めプログラム例
    - パラメータ設定プログラム(基本パラメータ1(軸1)の設定 / 原点復帰基本パラメータ(軸1)の設定 / 単位degree用設定(軸1)プログラム)
    - 位置決めデータ設定プログラム
- 転記時の要確認一覧

## 13 プログラミング (13 / 印刷 p.668 / 原本 p.670)

シンプルモーションユニットを使った位置決め制御を行うために必要なプログラムについて説明しています。制御に必要なプログラムは，「始動条件」，「始動タイムチャート」，「デバイス設定」，制御全体の構成などを考慮して作成します。(実行したい制御に合わせて，パラメータや位置決めデータ，ブロック始動データ，条件データなどをシンプルモーションユニットに設定し，制御データの設定プログラムや各制御の始動プログラムを作成する必要があります。)

### 13.1 プログラム作成上の注意事項 (13.1 / 印刷 p.668 / 原本 p.670)

CPUユニットからシンプルモーションユニットのバッファメモリへデータを書き込むときの，共通の注意事項を示します。

##### データの読出し／書込み (13.1 / 印刷 p.668 / 原本 p.670)

本章に示すデータの設定(各種パラメータ，位置決めデータ，ブロック始動データ)は，できるだけエンジニアリングツールで行われることをおすすめします。プログラムで設定する場合，かなりのプログラムとデバイスを使用しますので，複雑になると共に，スキャンタイムの増大につながります｡また，連続軌跡制御または連続位置決め制御中に位置決めデータを書き換える場合は，4つ前の位置決めデータを実行するまでに書き換えてください。4つ前の位置決めデータを実行する前に位置決めデータの書換えが行われていない場合，データは書き換えられていないものとして処理されます。

##### 速度変更実行間隔の制約 (13.1 / 印刷 p.668 / 原本 p.670)

シンプルモーションユニットで速度変更機能またはオーバーライド機能により連続して速度変更を行う場合は，速度変更の間隔が10 ms以上となるようにしてください。

##### オーバーラン時の処理 (13.1 / 印刷 p.668 / 原本 p.670)

詳細パラメータ1でストロークリミット上限値および下限値の設定にて，オーバーランの防止にはなります。ただし，これはシンプルモーションユニットが正常に動作している場合のみ有効です。システムの安全性からみて限界リミットスイッチを設け，リミットスイッチ作動によって，サーボアンプの主回路電源をOFFするような外部の回路を設けることをおすすめします。

##### システム構成 (13.1 / 印刷 p.668 / 原本 p.670)

プログラム例で使用するシステム構成を示します。

【図】プログラム例で使用するシステム構成(13.1 / 印刷 p.668 / 原本 p.670)
- ベースユニット上に左から (1)～(5) のユニットを装着。
  - (1)R61P
  - (2)R16CPU
  - (3)RD77MS16(X0～X1F/Y0～Y1F)
  - (4)RX40C7(X20～X3F)
  - (5)RX40C7(X40～X5F)
- (3)RD77MS16 から サーボアンプ(MR-J4-_B_) に接続し、サーボアンプにサーボモータ(軸1)が接続される。
- 外部機器から (4)RX40C7 へ X20~X3F、(5)RX40C7 へ X40~X5F の信号が入力される(図中の矢印は外部機器から入力ユニットへの向き)。

### 13.2 使用するラベル一覧 (13.2 / 印刷 p.669 / 原本 p.671)

プログラム例では，使用するラベルを下記のように割り付けています。

#### ユニットラベル (13.2 / 印刷 p.669-670 / 原本 p.671-672)

[RD77MSの例]

| 分類 | ラベル名 | 内容 |
|---|---|---|
| 先頭I/O No. | RD77_1.uIO | 先頭I/O No. |
| 入力信号 | RD77_1.bReady | RD77準備完了 |
| 入力信号 | RD77_1.bSynchronizationFlag | RD77同期用フラグ |
| 入力信号 | RD77_1.bSynchronizationFlag_D | RD77同期用フラグ |
| 入力信号 | RD77_1.bnBusy[0] | 軸1 BUSY信号 |
| 入力信号 | RD77_1.bnBusy_D[0] | 軸1 BUSY信号 |
| 出力信号 | RD77_1.bAllAxisServoOn | RD77全軸サーボON |
| 出力信号 | RD77_1.bPLC_Ready | シーケンサレディ信号 |
| 出力信号 | RD77_1.bnPositioningStart[0] | 軸1 位置決め始動信号 |
| パラメータ | RD77_1.stnAxPrm_D[0].dHomePosition_D | 軸1 原点アドレス |
| パラメータ | RD77_1.stnAxPrm_D[0].dSoftwareStrokeLowerLimit_D | 軸1 ソフトウェアストロークリミット下限値 |
| パラメータ | RD77_1.stnAxPrm_D[0].dSoftwareStrokeUpperLimit_D | 軸1 ソフトウェアストロークリミット上限値 |
| パラメータ | RD77_1.stnAxPrm_D[0].uExternalCommandFunctionMode_D | 軸1 外部指令機能選択 |
| パラメータ | RD77_1.stnAxPrm_D[0].uHomingDirection_D | 軸1 原点復帰方向 |
| パラメータ | RD77_1.stnAxPrm_D[0].uHomingMethod_D | 軸1 原点復帰方式 |
| パラメータ | RD77_1.stnAxPrm_D[0].uHomingRetry_D | 軸1 原点復帰リトライ |
| パラメータ | RD77_1.stnAxPrm_D[0].uUnitMagnification_D | 軸1 単位倍率(AM) |
| パラメータ | RD77_1.stnAxPrm_D[0].uUnit_D | 軸1 単位設定 |
| パラメータ | RD77_1.stnAxPrm_D[0].uVP_Mode_D | 軸1 速度･位置機能選択 |
| パラメータ | RD77_1.stnAxPrm_D[0].uV_CommandPosition_D | 軸1 速度制御時の送り現在値 |
| パラメータ | RD77_1.stnAxPrm_D[0].udCreepSpeed_D | 軸1 クリープ速度 |
| パラメータ | RD77_1.stnAxPrm_D[0].udHomingSpeed_D | 軸1 原点復帰速度 |
| パラメータ | RD77_1.stnAxPrm_D[0].udMovementAmountPerRotation_D | 軸1 1回転あたりの移動量(AL) |
| パラメータ | RD77_1.stnAxPrm_D[0].udPulsesPerRotation_D | 軸1 1回転あたりのパルス数(AP) |
| 軸モニタデータ | RD77_1.stnAxMntr[0].uM_Code | 軸1 有効Mコード |
| 軸モニタデータ | RD77_1.stnAxMntr[0].uStatus.3 | 軸1 原点復帰要求フラグ |
| 軸モニタデータ | RD77_1.stnAxMntr[0].uStatus.9 | 軸1 軸ワーニング検出 |
| 軸モニタデータ | RD77_1.stnAxMntr[0].uStatus.C | 軸1 MコードON |
| 軸モニタデータ | RD77_1.stnAxMntr[0].uStatus.D | 軸1 エラー検出 |
| 軸モニタデータ | RD77_1.stnAxMntr_D[0].uStatus_D.D | 軸1 エラー検出 |
| 軸モニタデータ | RD77_1.stnAxMntr[0].uStatus.E | 軸1 始動完了 |
| 軸モニタデータ | RD77_1.stnAxMntr_D[0].uStatus_D.E | 軸1 始動完了 |
| 軸モニタデータ | RD77_1.stnAxMntr_D[0].uStatus_D.F | 軸1 位置決め完了 |
| 軸モニタデータ | RD77_1.stnAxMntr_D[0].dCommandPosition_D | 軸1 送り現在値 |
| システムモニタデータ | RD77_1.stSysMntr1_D.wSSCNET_ControlStatus_D | SSCNET制御ステータス |
| 軸制御データ1 | RD77_1.stnAxCtrl1_D[0].dNewPosition_D | 軸1 現在値変更値 |
| 軸制御データ1 | RD77_1.stnAxCtrl1_D[0].uClearHomingRequestFlag_D | 軸1 原点復帰要求フラグOFF要求 |
| 軸制御データ1 | RD77_1.stnAxCtrl1_D[0].uClear_M_Code_D | 軸1 MコードOFF要求 |
| 軸制御データ1 | RD77_1.stnAxCtrl1_D[0].uEnablePV_Switching_D | 軸1 位置・速度切換え許可フラグ |
| 軸制御データ1 | RD77_1.stnAxCtrl1_D[0].uExternalCommandValid_D | 軸1 外部指令有効 |
| 軸制御データ1 | RD77_1.stnAxCtrl1_D[0].uForwardNewTorque_D | 軸1トルク変更値/正転トルク変更値 |
| 軸制御データ1 | RD77_1.stnAxCtrl1_D[0].uInterruptOperation_D | 軸1 連続運転中断要求 |
| 軸制御データ1 | RD77_1.stnAxCtrl1_D[0].uOverride_D | 軸1 位置決め運転速度オーバーライド |
| 軸制御データ1 | RD77_1.stnAxCtrl1_D[0].uPositioningStartNo_D | 軸1 位置決め始動番号 |
| 軸制御データ1 | RD77_1.stnAxCtrl1_D[0].uPositioningStartingPointNo_D | 軸1 位置決め始動ポイント番号 |
| 軸制御データ1 | RD77_1.stnAxCtrl1_D[0].uSkip_D | 軸1 スキップ指令 |
| 軸制御データ1 | RD77_1.stnAxCtrl1_D[0].uStepMode_D | 軸1 ステップモード |
| 軸制御データ1 | RD77_1.stnAxCtrl1_D[0].uStepStartInformation_D | 軸1 ステップ始動情報 |
| 軸制御データ1 | RD77_1.stnAxCtrl1_D[0].uStepValid_D | 軸1 ステップ有効フラグ |
| 軸制御データ1 | RD77_1.stnAxCtrl1_D[0].uTeachingDataSelection_D | 軸1 ティーチングデータ選択 |
| 軸制御データ1 | RD77_1.stnAxCtrl1_D[0].uTeachingPositioningDataNo_D | 軸1 ティーチング位置決めデータNo. |
| 軸制御データ1 | RD77_1.stnAxCtrl1_D[0].udNewSpeed_D | 軸1 速度変更値 |
| 軸制御データ1 | RD77_1.stnAxCtrl1_D[0].udPV_NewSpeed_D | 軸1 位置・速度切換え制御速度変更レジスタ |
| 軸制御データ1 | RD77_1.stnAxCtrl1_D[0].udVP_NewMovementAmount_D | 軸1 速度・位置切換え制御移動量変更レジスタ |
| システム制御データ | RD77_1.stSysCtrl_D.wSSCNET_ControlCommand_D | SSCNET制御指令 |
| 軸制御データ2 | RD77_1.stnAxCtrl2_D[0].uProhibitPositioning_D | 軸1 実行禁止フラグ |
| 軸制御データ2 | RD77_1.stnAxCtrl2_D[0].uProhibitPositioning_D.0 | 軸1 実行禁止フラグ |
| 軸制御データ2 | RD77_1.stnAxCtrl2_D[0].uStopAxis_D | 軸1 軸停止 |
| 軸制御データ2 | RD77_1.stnAxCtrl2_D[0].uStopAxis_D.0 | 軸1 軸停止 |
| サーボネットワーク構成パラメータ | RD77_1.stnSvNetPrm_D[0].udConnectedDevice_D | 軸1 接続機器 |

#### グローバルラベル (13.2 / 印刷 p.671-673 / 原本 p.673-675)

プログラム例で使用しているグローバルラベルを示します。下記のようにグローバルラベルを設定してください。

[RD77MSの例]

##### 割付けデバイスを設定するグローバルラベル (13.2 / 印刷 p.671 / 原本 p.673)

【図】GX Works3 のグローバルラベル設定画面(No.1～47)。画面図から全行を転記(13.2 / 印刷 p.671 / 原本 p.673)。全行ともクラスは VAR_GLOBAL。

| No. | ラベル名 | データ型 | クラス | 割付け(デバイス/ラベル) | Japanese/日本語(表示対象) |
|---|---|---|---|---|---|
| 1 | bOutpuAbsReq | ビット | VAR_GLOBAL | Y62 | ABSデータ要求 |
| 2 | bOutpuAbsTrMode | ビット | VAR_GLOBAL | Y61 | ABS転送モード |
| 3 | bOutpuServoON | ビット | VAR_GLOBAL | Y60 | サーボON信号 |
| 4 | bInputFastStartReq | ビット | VAR_GLOBAL | X52 | 高速始動指令 |
| 5 | bAllAxisServoOnReq | ビット | VAR_GLOBAL | X4F | 全軸サーボON指令 |
| 6 | bInputbInputSpeedPositionSwitchingAbsSetReq | ビット | VAR_GLOBAL | X4D | 速度・位置切換え(ABS)設定指令 |
| 7 | bInputTrDataComp | ビット | VAR_GLOBAL | X49 | 送信データ準備完了フラグ |
| 8 | bInputAbsBit1 | ビット | VAR_GLOBAL | X48 | ABSデータbit1 |
| 9 | bInputAbsBit0 | ビット | VAR_GLOBAL | X47 | ABSデータbit0 |
| 10 | bInputStepStartInformationReq | ビット | VAR_GLOBAL | X46 | ステップ始動情報指令 |
| 11 | bInputTargetPositionChangeReq | ビット | VAR_GLOBAL | X45 | 目標位置変更指令 |
| 12 | bInputSetInchingMovementAmountReq | ビット | VAR_GLOBAL | X44 | インチング移動量設定指令 |
| 13 | bInputChangePositionSpeedSwitchingSpeedReq | ビット | VAR_GLOBAL | X43 | 速度変更指令 |
| 14 | bInputPositionSpeedSwitchingDisableReq | ビット | VAR_GLOBAL | X42 | 位置・速度切換え禁止指令 |
| 15 | bInputPositionSpeedSwitchingEnableReq | ビット | VAR_GLOBAL | X41 | 位置・速度切換え許可指令 |
| 16 | bInputPositionSpeedSwitchingReq | ビット | VAR_GLOBAL | X40 | 位置・速度切換え運転指令 |
| 17 | bInputStopReq | ビット | VAR_GLOBAL | X3F | 停止指令 |
| 18 | bInputErrResetReq | ビット | VAR_GLOBAL | X3E | エラーリセット指令 |
| 19 | bInputWriteFlashReq | ビット | VAR_GLOBAL | X3D | フラッシュROM書込み指令 |
| 20 | bInputInitializeParameterReq | ビット | VAR_GLOBAL | X3C | パラメータ初期化指令 |
| 21 | bInputRestartReq | ビット | VAR_GLOBAL | X3B | 再始動指令 |
| 22 | bInputStopContinuousOperationReq | ビット | VAR_GLOBAL | X3A | 連続運転中断指令 |
| 23 | bInputTeachingReq | ビット | VAR_GLOBAL | X39 | ティーチング指令 |
| 24 | bInputSkipReq | ビット | VAR_GLOBAL | X38 | スキップ指令 |
| 25 | bInputStepOperationReq | ビット | VAR_GLOBAL | X37 | ステップ運転指令 |
| 26 | bInputChangeTorqueReq | ビット | VAR_GLOBAL | X36 | トルク変更指令 |
| 27 | bInputChangeAccDecTimeDisable | ビット | VAR_GLOBAL | X35 | 加減速時間変更不許可指令 |
| 28 | bInputChangeAccDecTimeReq | ビット | VAR_GLOBAL | X34 | 加減速時間変更指令 |
| 29 | bInputOverrideReq | ビット | VAR_GLOBAL | X33 | オーバーライド指令 |
| 30 | bInputChangeSpeedReq | ビット | VAR_GLOBAL | X32 | 速度変更指令 |
| 31 | bInputStartMPGReq | ビット | VAR_GLOBAL | X30 | 手動パルサ運転指令 |
| 32 | bInputReverseJogStartReq | ビット | VAR_GLOBAL | X2F | 逆転JOG/インチング指令 |
| 33 | bInputForwardJogStartReq | ビット | VAR_GLOBAL | X2E | 正転JOG/インチング指令 |
| 34 | bInputSetJogSpeedReq | ビット | VAR_GLOBAL | X2D | JOG運転速度設定指令 |
| 35 | bInputMcodeOffReq | ビット | VAR_GLOBAL | X2C | MコードOFF要求 |
| 36 | bInputStartPositioningReq | ビット | VAR_GLOBAL | X2B | 位置決め始動指令 |
| 37 | bInputStartAdvancedPositioningReq | ビット | VAR_GLOBAL | X2A | 高度な位置決め制御始動指令 |
| 38 | bInputChangeSpeedPositionSwitchingMovementAmount | ビット | VAR_GLOBAL | X29 | 移動量変更指令 |
| 39 | bInputSpeedPositionSwitchingDisableReq | ビット | VAR_GLOBAL | X28 | 速度・位置切換え禁止指令 |
| 40 | bInputSpeedPositionSwitchingEnableReq | ビット | VAR_GLOBAL | X27 | 速度・位置切換え許可指令 |
| 41 | bInputSpeedPositionSwitchingReq | ビット | VAR_GLOBAL | X26 | 速度・位置切換え運転指令 |
| 42 | bInputSetStartPositioningNoReq | ビット | VAR_GLOBAL | X25 | 位置決め始動指令 |
| 43 | bInputFastOPRStartReq | ビット | VAR_GLOBAL | X24 | 高速原点復帰指令 |
| 44 | bInputOPRStartReq | ビット | VAR_GLOBAL | X23 | 機械原点復帰指令 |
| 45 | bInputExternalCommandInvalidReq | ビット | VAR_GLOBAL | X22 | 外部指令無効指令 |
| 46 | bInputExternalCommandValidReq | ビット | VAR_GLOBAL | X21 | 外部指令有効指令 |
| 47 | bInputOPRReqFlagOffReq | ビット | VAR_GLOBAL | X20 | 原点復帰要求OFF指令 |

##### 割付けデバイスを設定しないグローバルラベル (13.2 / 印刷 p.672-673 / 原本 p.674-675)

割付けデバイスを設定しないグローバルラベル(割付けデバイスを設定していない場合，使用していない内部リレーやデータデバイスが自動で割り付けられます。)

【図】GX Works3 のグローバルラベル設定画面(No.48～146)。画面図から全行を転記(13.2 / 印刷 p.672-673 / 原本 p.674-675)。全行ともクラスは VAR_GLOBAL、割付け(デバイス/ラベル)欄は空欄。

| No. | ラベル名 | データ型 | クラス | 割付け(デバイス/ラベル) | Japanese/日本語(表示対象) |
|---|---|---|---|---|---|
| 48 | bSetPositioningData_bEN | ビット | VAR_GLOBAL | (空欄) | 実行命令 |
| 49 | bSetPositioningData_bENO | ビット | VAR_GLOBAL | (空欄) | 実行状態 |
| 50 | bSetPositioningData_bOK | ビット | VAR_GLOBAL | (空欄) | 正常終了 |
| 51 | bSetPositioningData_bErr | ビット | VAR_GLOBAL | (空欄) | エラー終了 |
| 52 | uSetPositioningData_bErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | エラーコード |
| 53 | bJOG_bENO | ビット | VAR_GLOBAL | (空欄) | 実行状態 |
| 54 | bJOG_bOK | ビット | VAR_GLOBAL | (空欄) | 正常終了 |
| 55 | bJOG_bErr | ビット | VAR_GLOBAL | (空欄) | エラー終了 |
| 56 | uJOG_uErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | エラーコード |
| 57 | bMPG_bENO | ビット | VAR_GLOBAL | (空欄) | 実行状態 |
| 58 | bMPG_bOK | ビット | VAR_GLOBAL | (空欄) | 正常終了 |
| 59 | bMPG_bErr | ビット | VAR_GLOBAL | (空欄) | エラー終了 |
| 60 | uMPG_uErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | エラーコード |
| 61 | bChangeSpeed_bENO | ビット | VAR_GLOBAL | (空欄) | 実行状態 |
| 62 | bChangeSpeed_bOK | ビット | VAR_GLOBAL | (空欄) | 正常終了 |
| 63 | bChangeSpeed_bErr | ビット | VAR_GLOBAL | (空欄) | エラー終了 |
| 64 | uChangeSpeed_uErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | エラーコード |
| 65 | bChangeAccDecTime_bENO | ビット | VAR_GLOBAL | (空欄) | 実行状態 |
| 66 | bChangeAccDecTime_bOK | ビット | VAR_GLOBAL | (空欄) | 正常終了 |
| 67 | bChangeAccDecTime_bErr | ビット | VAR_GLOBAL | (空欄) | エラー終了 |
| 68 | uChangeAccDecTime_uErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | エラーコード |
| 69 | bChangePosition_bENO | ビット | VAR_GLOBAL | (空欄) | 実行状態 |
| 70 | bChangePosition_bOK | ビット | VAR_GLOBAL | (空欄) | 正常終了 |
| 71 | bChangePosition_bErr | ビット | VAR_GLOBAL | (空欄) | エラー終了 |
| 72 | uChangePosition_uErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | エラーコード |
| 73 | bRestart_bENO | ビット | VAR_GLOBAL | (空欄) | 実行状態 |
| 74 | bRestart_bOK | ビット | VAR_GLOBAL | (空欄) | 正常終了 |
| 75 | bRestart_bErr | ビット | VAR_GLOBAL | (空欄) | エラー終了 |
| 76 | uRestart_uErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | エラーコード |
| 77 | bInitializeParameter_bENO | ビット | VAR_GLOBAL | (空欄) | 実行状態 |
| 78 | bInitializeParameter_bOK | ビット | VAR_GLOBAL | (空欄) | 正常終了 |
| 79 | bInitializeParameter_bErr | ビット | VAR_GLOBAL | (空欄) | エラー終了 |
| 80 | uInitializeParameter_uErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | エラーコード |
| 81 | bOperateError_bENO | ビット | VAR_GLOBAL | (空欄) | 実行状態 |
| 82 | bOperateError_bOK | ビット | VAR_GLOBAL | (空欄) | 正常終了 |
| 83 | bOperateError_bModuleErr | ビット | VAR_GLOBAL | (空欄) | 軸エラー検出 |
| 84 | uOperateError_uModuleErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | 軸エラーコード |
| 85 | bOperateError_bModuleWarn | ビット | VAR_GLOBAL | (空欄) | 軸ワーニング検出 |
| 86 | uOperateError_bModuleWarnId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | 軸ワーニングコード |
| 87 | bOperateError_bErr | ビット | VAR_GLOBAL | (空欄) | エラー終了 |
| 88 | uOperateError_uErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | エラーコード |
| 89 | bWriteFlash_bENO | ビット | VAR_GLOBAL | (空欄) | 実行状態 |
| 90 | bWriteFlash_bOK | ビット | VAR_GLOBAL | (空欄) | 正常終了 |
| 91 | bWriteFlash_bErr | ビット | VAR_GLOBAL | (空欄) | エラー終了 |
| 92 | uWriteFlash_uErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | エラーコード |
| 93 | bBasicParamSetComp | ビット | VAR_GLOBAL | (空欄) | 基本パラメータ1設定完了 |
| 94 | bSetElectronicGear16bit | ビット | VAR_GLOBAL | (空欄) | 電子ギア(16bit)設定 |
| 95 | bOPRParamSetComp | ビット | VAR_GLOBAL | (空欄) | 原点復帰基本パラメータ設定完了 |
| 96 | uBlockData | ワード[符号なし]/ビット列[16ビット](0..4) | VAR_GLOBAL | (空欄) | ブロック始動データ(形態、始動データNo) |
| 97 | uBlockInstData | ワード[符号なし]/ビット列[16ビット](0..4) | VAR_GLOBAL | (空欄) | ブロック始動データ(特殊始動命令) |
| 98 | bOPRReqFlagOffReq_P | ビット | VAR_GLOBAL | (空欄) | 原点復帰要求OFF指令パルス |
| 99 | bOPRReqFlagOffReq_H | ビット | VAR_GLOBAL | (空欄) | 原点復帰要求OFF指令記憶 |
| 100 | bOPRReqFlagOffReq | ビット | VAR_GLOBAL | (空欄) | 原点復帰要求OFF指令 |
| 101 | udMovementAmount | ダブルワード[符号なし]/ビット列[32ビット] | VAR_GLOBAL | (空欄) | 速度・位置切換え制御移動量 |
| 102 | udSpeed | ダブルワード[符号付き] | VAR_GLOBAL | (空欄) | 位置・速度切換え制御速度 |
| 103 | bStartPositioning_bENO | ビット | VAR_GLOBAL | (空欄) | 実行状態 |
| 104 | bStartPositioning_bOK | ビット | VAR_GLOBAL | (空欄) | 正常終了 |
| 105 | bStartPositioning_bErr | ビット | VAR_GLOBAL | (空欄) | エラー終了 |
| 106 | uStartPositioning_uErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | エラーコード |
| 107 | bDuringMPGOperation | ビット | VAR_GLOBAL | (空欄) | 手動パルサ運転中フラグ |
| 108 | bFastStartPreparationComp | ビット | VAR_GLOBAL | (空欄) | 高速始動準備完了 |
| 109 | bFastOPRStartReq | ビット | VAR_GLOBAL | (空欄) | 高速原点復帰指令 |
| 110 | bFastOPRStartReq_H | ビット | VAR_GLOBAL | (空欄) | 高速原点復帰指令記憶 |
| 111 | bDuringJogInchingOperation | ビット | VAR_GLOBAL | (空欄) | JOG/インチング運転中フラグ |
| 112 | udJogOperationSpeed | ダブルワード[符号なし]/ビット列[32ビット] | VAR_GLOBAL | (空欄) | JOG運転速度 |
| 113 | uInchingMovementAmount | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | インチング移動量 |
| 114 | bChangeSpeedReq | ビット | VAR_GLOBAL | (空欄) | 速度変更指令 |
| 115 | bOverrideReq_P | ビット | VAR_GLOBAL | (空欄) | オーバライド指令パルス |
| 116 | bAccDecTimeChangeReq | ビット | VAR_GLOBAL | (空欄) | 加減速変更指令 |
| 117 | bChangeAccDecTime_iEnable | ビット | VAR_GLOBAL | (空欄) | 加減速時間変更許可フラグ |
| 118 | bStepOperationReq_P | ビット | VAR_GLOBAL | (空欄) | ステップ運転指令パルス |
| 119 | bChangeTorqueReq | ビット | VAR_GLOBAL | (空欄) | トルク変更指令 |
| 120 | bSkipReq_P | ビット | VAR_GLOBAL | (空欄) | スキップ指令パルス |
| 121 | bSkipReq | ビット | VAR_GLOBAL | (空欄) | スキップ指令 |
| 122 | bTeachingReq_P | ビット | VAR_GLOBAL | (空欄) | ティーチング指令パルス |
| 123 | bTeachingReq | ビット | VAR_GLOBAL | (空欄) | ティーチング指令 |
| 124 | uTeachingData | ワード[符号なし]/ビット列[16ビット](0..3) | VAR_GLOBAL | (空欄) | GP.TEACH1命令用コントロールデータ |
| 125 | uTeachingDevice | ビット(0..1) | VAR_GLOBAL | (空欄) | GP.TEACH1命令完了デバイス |
| 126 | uIO | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | IO番号(上位12bit) |
| 127 | bStopContinuousOperationReq_P | ビット | VAR_GLOBAL | (空欄) | 連続運転中断指令パルス |
| 128 | bTargetPositionChangeReq | ビット | VAR_GLOBAL | (空欄) | 目標位置変更指令 |
| 129 | bRestartReq | ビット | VAR_GLOBAL | (空欄) | 再始動指令 |
| 130 | bInitializeParameterReq | ビット | VAR_GLOBAL | (空欄) | パラメータ初期化指令 |
| 131 | bWriteFlashReq | ビット | VAR_GLOBAL | (空欄) | フラッシュROM書込み指令 |
| 132 | bErrResetReq | ビット | VAR_GLOBAL | (空欄) | エラーリセット指令 |
| 133 | bStopReq_P | ビット | VAR_GLOBAL | (空欄) | 停止指令 |
| 134 | bABRSTReq | ビット | VAR_GLOBAL | (空欄) | 絶対位置復元指令 |
| 135 | uOperateError_bModuleErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | 軸エラーコード |
| 136 | bErrReadReq | ビット | VAR_GLOBAL | (空欄) | エラー読出し指令 |
| 137 | bPositioningStartReq | ビット | VAR_GLOBAL | (空欄) | 位置決め始動指令 |
| 138 | bABRSTReq_P | ビット | VAR_GLOBAL | (空欄) | 絶対位置復元指令パルス |
| 139 | bABRST_bENO | ビット | VAR_GLOBAL | (空欄) | 実行状態 |
| 140 | bABRST_bOK | ビット | VAR_GLOBAL | (空欄) | 正常終了 |
| 141 | bABRST_bAbsNG | ビット | VAR_GLOBAL | (空欄) | ABSエラー |
| 142 | uABRST_uAbsErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | ABSエラーコード |
| 143 | bABRST_bErr | ビット | VAR_GLOBAL | (空欄) | エラー終了 |
| 144 | uABRST_uErrId | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | エラーコード |
| 145 | bPosiStart10 | ビット | VAR_GLOBAL | (空欄) | デバッグ用位置決め始動 |
| 146 | uPositioningStartNo | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | (空欄) | 位置決め始動番号 |

### 13.3 プログラムの作成 (13.3 / 印刷 p.673 / 原本 p.675)

本節では，実際に使用する「位置決め制御の運転プログラム」について説明します。

#### プログラムの全体構成 (13.3 / 印刷 p.673 / 原本 p.675)

位置決め制御の運転プログラムの全体構成を示します。

| No. | プログラム名 | 備考 |
|---|---|---|
| 1a | 基本パラメータ設定 | • エンジニアリングツールにてパラメータ，位置決めデータ，ブロック始動データ，サーボパラメータを設定する場合，プログラムは不要です。<br>• 機械原点復帰制御を行わない場合は，原点復帰用パラメータの設定は不要です。 |
| 1b | 原点復帰パラメータ設定プログラム | • エンジニアリングツールにてパラメータ，位置決めデータ，ブロック始動データ，サーボパラメータを設定する場合，プログラムは不要です。<br>• 機械原点復帰制御を行わない場合は，原点復帰用パラメータの設定は不要です。 |
| 1c | 単位degree用設定プログラム | • エンジニアリングツールにてパラメータ，位置決めデータ，ブロック始動データ，サーボパラメータを設定する場合，プログラムは不要です。<br>• 機械原点復帰制御を行わない場合は，原点復帰用パラメータの設定は不要です。 |
| 2 | 位置決めデータ設定プログラム | • エンジニアリングツールにてパラメータ，位置決めデータ，ブロック始動データ，サーボパラメータを設定する場合，プログラムは不要です。<br>• 機械原点復帰制御を行わない場合は，原点復帰用パラメータの設定は不要です。 |
| 3 | ブロック始動データ設定プログラム | • エンジニアリングツールにてパラメータ，位置決めデータ，ブロック始動データ，サーボパラメータを設定する場合，プログラムは不要です。<br>• 機械原点復帰制御を行わない場合は，原点復帰用パラメータの設定は不要です。 |
| 4 | サーボパラメータ設定プログラム | • エンジニアリングツールにてパラメータ，位置決めデータ，ブロック始動データ，サーボパラメータを設定する場合，プログラムは不要です。<br>• 機械原点復帰制御を行わない場合は，原点復帰用パラメータの設定は不要です。 |
| 5 | 原点復帰要求OFFプログラム | 機械原点復帰制御を行う場合は不要です。 |
| 6 | 外部指令機能有効設定プログラム | — |
| 7 | シーケンサレディ信号[Y0]ONプログラム | — |
| 8 | 全軸サーボON[Y1]プログラム | — |
| 9 | 位置決め始動番号設定プログラム | — |
| 10 | 位置決め始動プログラム | — |
| 11 | MコードOFFプログラム | Ｍコード出力機能を使用しない場合は不要です。 |
| 12 | JOG運転設定プログラム | JOG運転を使用しない場合は不要です。 |
| 13 | インチング運転設定プログラム | インチング運転を使用しない場合は不要です。 |
| 14 | JOG運転/インチング運転実行プログラム | JOG運転およびインチング運転を使用しない場合は不要です。 |
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

注: 原本では No.1a～4 の備考が1つの結合セル、No.6～9 の備考「—」が1つの結合セル、No.16～28 の備考「必要に応じて追加するプログラムです。」が1つの結合セルである(上表では各行に展開)。

### 13.4 位置決めプログラム例 (13.4 / 印刷 p.674 / 原本 p.676)

ユニットFBの詳細は下記マニュアルの"シンプルモーションユニットFB"を参照してください。
MELSEC iQ-R シンプルモーションユニットFBリファレンス

#### パラメータ設定プログラム (13.4 / 印刷 p.674-675 / 原本 p.676-677)

エンジニアリングツールの"ユニットパラメータ"にてパラメータを設定する場合，本プログラムは不要です。

##### 基本パラメータ1(軸1)の設定 (13.4 / 印刷 p.674 / 原本 p.676)

【図】ラダー図(図から書き起こし)。起動接点は RD77_1.bSynchronizationFlag(X1)の立上り(↑)パルス接点。1つの起動条件で5つの出力を並列に駆動する。

```
(0)  LDP    RD77_1.bSynchronizationFlag                                    X1
     MOV    K0        RD77_1.stnAxPrm_D[0].uUnit_D                         U0¥G0
     MOV    K1        RD77_1.stnAxPrm_D[0].uUnitMagnification_D            U0¥G1
     DMOVP  K4194304  RD77_1.stnAxPrm_D[0].udPulsesPerRotation_D           U0¥G2
     DMOVP  K250000   RD77_1.stnAxPrm_D[0].udMovementAmountPerRotation_D   U0¥G4
     SET    bBasicParamSetComp
```

##### 原点復帰基本パラメータ(軸1)の設定 (13.4 / 印刷 p.674 / 原本 p.676)

[RD77MSの例]

【図】ラダー図(図から書き起こし)。起動接点は RD77_1.bSynchronizationFlag(X1)の立上り(↑)パルス接点。1つの起動条件で7つの出力を並列に駆動する。

```
(0)  LDP    RD77_1.bSynchronizationFlag                                    X1
     MOVP   K0        RD77_1.stnAxPrm_D[0].uHomingMethod_D                 U0¥G70
     MOVP   K0        RD77_1.stnAxPrm_D[0].uHomingDirection_D              U0¥G71
     DMOVP  K0        RD77_1.stnAxPrm_D[0].dHomePosition_D                 U0¥G72
     DMOVP  K5000     RD77_1.stnAxPrm_D[0].udHomingSpeed_D                 U0¥G74
     DMOVP  K1500     RD77_1.stnAxPrm_D[0].udCreepSpeed_D                  U0¥G76
     MOVP   K1        RD77_1.stnAxPrm_D[0].uHomingRetry_D                  U0¥G78
     SET    bOPRParamSetComp
```

##### 単位degree用設定(軸1)プログラム (13.4 / 印刷 p.675 / 原本 p.677)

【図】ラダー図(図から書き起こし)。起動条件は RD77_1.bSynchronizationFlag(X1)の立上り(↑)パルス接点と bInputbInputSpeedPositionSwitchingAbsSetReq(X4D)のa接点の直列。1つの起動条件で5つの出力を並列に駆動する。

```
(0)  LDP    RD77_1.bSynchronizationFlag                                    X1
     AND    bInputbInputSpeedPositionSwitchingAbsSetReq                    X4D
     MOVP   K2        RD77_1.stnAxPrm_D[0].uUnit_D                         U0¥G0
     DMOVP  K0        RD77_1.stnAxPrm_D[0].dSoftwareStrokeUpperLimit_D     U0¥G18
     DMOVP  K0        RD77_1.stnAxPrm_D[0].dSoftwareStrokeLowerLimit_D     U0¥G20
     MOVP   K1        RD77_1.stnAxPrm_D[0].uV_CommandPosition_D            U0¥G30
     MOVP   K2        RD77_1.stnAxPrm_D[0].uVP_Mode_D                      U0¥G34
```

#### 位置決めデータ設定プログラム (13.4 / 印刷 p.676-677 / 原本 p.678-679)

エンジニアリングツールの"位置決めデータ"にて設定する場合，本プログラムは不要です。

[RD77MSの例]

【図】ラダー図(図から書き起こし)。ステップ(0)の回路は RD77_1.bSynchronizationFlag(X1)の立上り(↑)パルス接点で、位置決めデータ設定FB(M_RD77_SetPositioningData_00E_1)の入力ラベル(pb_～)へ値を転送し、bSetPositioningData_bEN をセットする。ステップ(38)の回路で bSetPositioningData_bEN をFBの実行命令(i_bEN)に接続する。

```
(0)  LDP    RD77_1.bSynchronizationFlag                                    X1
     MOV    K0        M_RD77_SetPositioningData_00E_1.pb_uOpePattern
     MOV    K1        M_RD77_SetPositioningData_00E_1.pb_uCtrlSys
     MOV    K1        M_RD77_SetPositioningData_00E_1.pb_uAccTimeNo
     MOV    K2        M_RD77_SetPositioningData_00E_1.pb_uDecTimeNo
     MOV    K0        M_RD77_SetPositioningData_00E_1.pb_uInterpolationAxisNo1
     MOV    K0        M_RD77_SetPositioningData_00E_1.pb_uInterpolationAxisNo2
     MOV    K0        M_RD77_SetPositioningData_00E_1.pb_uInterpolationAxisNo3
     MOV    K9843     M_RD77_SetPositioningData_00E_1.pb_uMcode
     MOV    K300      M_RD77_SetPositioningData_00E_1.pb_uDwellTime
     MOV    K0        M_RD77_SetPositioningData_00E_1.pb_uMcodeOnTiming
     MOV    K0        M_RD77_SetPositioningData_00E_1.pb_uABS
     MOV    K0        M_RD77_SetPositioningData_00E_1.pb_uInterpolateSpd
     MOV    K0        M_RD77_SetPositioningData_00E_1.pb_uInterpolateSpd
     DMOV   K18000    M_RD77_SetPositioningData_00E_1.pb_udCmdSpd
     DMOV   K4126     M_RD77_SetPositioningData_00E_1.pb_dPositAdr
     DMOV   K0        M_RD77_SetPositioningData_00E_1.pb_dArcAdr
     SET    bSetPositioningData_bEN

(38) LD     bSetPositioningData_bEN
     M_RD77_SetPositioningData_00E_1  (M+RD77_SetPositioningData_00E)  Positioning data setting FB  ※引数は下表
```

ステップ(38) FB: インスタンス名 M_RD77_SetPositioningData_00E_1 / FB名 (M+RD77_SetPositioningData_00E) / Positioning data setting FB

| 区分 | FB引数(型) | 接続先 |
|---|---|---|
| 入力 | B: i_bEN | bSetPositioningData_bEN(a接点) |
| 入力 | DUT: i_stModule | RD77_1 |
| 入力 | UW: i_uAxis | K1 |
| 入力 | UW: i_uDataNo | K1 |
| 出力 | o_bENO :B | bSetPositioningData_bENO(コイル) |
| 出力 | o_bOK :B | bSetPositioningData_bOK(コイル) |
| 出力 | o_bErr :B | bSetPositioningData_bErr(コイル) |
| 出力 | o_uErrId :UW | uSetPositioningData_bErrId |

FBボックス内に表示されている入力ラベル(パブリック変数)の一覧(原本の表示順):
pb_uOpePattern, pb_uCtrlSys, pb_uAccTimeNo, pb_uDecTimeNo, pb_uMcode, pb_uDwellTime, pb_uMcodeOnTiming, pb_uABS, pb_uInterpolateSpd, pb_udCmdSpd, pb_dPositAdr, pb_dArcAdr, pb_uInterpolationAxisNo1, pb_uInterpolationAxisNo2, pb_uInterpolationAxisNo3

(本ファイルの範囲はここまで。「ブロック始動データ設定プログラム」(印刷 p.678 / 原本 p.680)以降は次ファイル 13b。)

## 転記時の要確認一覧

- (印刷 p.671 / 原本 p.673) グローバルラベル No.6 のラベル名が「bInputbInputSpeedPositionSwitchingAbsSetReq」と "bInput" が二重になっている。原文どおり転記(単位degree用設定プログラム(印刷 p.675)の接点ラベルも同じ表記)。
- (印刷 p.671 / 原本 p.673) グローバルラベル No.1～3 のラベル名が「bOutpu～」(Output の t 欠落と思われる)。原文どおり転記。
- (印刷 p.671 / 原本 p.673) グローバルラベル No.13 bInputChangePositionSpeedSwitchingSpeedReq の日本語が「速度変更指令」(No.30 bInputChangeSpeedReq と同じ表記)。原文どおり転記。
- (印刷 p.671 / 原本 p.673) グローバルラベル No.31 が X30、No.30 が X32 で、X31 の割付けは一覧に無い。原文どおり転記。No.36(X2B)と No.42(X25)の日本語がどちらも「位置決め始動指令」。原文どおり。
- (印刷 p.671 / 原本 p.673) 画面図の最下端に No.48 の行が途中で切れて写っている(次ページ先頭の No.48 と同じ行と判断し、No.48 は次ページから転記)。また (印刷 p.673 / 原本 p.675) の画面図最下端に No.147 の行番号の一部が見えるが内容は読めない(空行と思われる)。
- (印刷 p.672 / 原本 p.674) グローバルラベル No.52 が「uSetPositioningData_bErrId」(u接頭辞のワード型だが末尾が bErrId)。No.86「uOperateError_bModuleWarnId」、No.135「uOperateError_bModuleErrId」(No.84 uOperateError_uModuleErrId と別に存在)も同様。原文どおり転記。
- (印刷 p.672 / 原本 p.674) グローバルラベル No.115 の日本語は「オーバライド指令パルス」(ー無し)、No.116 は「加減速変更指令」。原文どおり。No.133 bStopReq_P の日本語は「停止指令」(パルスの記載なし)。原文どおり。
- (印刷 p.674 / 原本 p.676) 基本パラメータ1(軸1)の設定は MOV/MOV(非パルス)と DMOVP/DMOVP(パルス)が混在している(起動接点は立上りパルス接点)。原文どおり。
- (印刷 p.676 / 原本 p.678) 位置決めデータ設定プログラムで MOV K0 → pb_uInterpolateSpd が2回続けて記載されている。原文どおり転記。
- (印刷 p.674-677 / 原本 p.676-679) ラダー図の中間ステップ番号は原本に表示が無いため記載していない(表示は (0) と (38) のみ)。
- (印刷 p.676-677 / 原本 p.678-679) 位置決めデータ設定プログラムの起動接点(X1)の記号は画像解像度が低いが、他のパラメータ設定プログラムと同じ立上り(↑)パルス接点と判読した。
