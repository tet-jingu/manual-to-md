# MELSEC iQ-R Ethernetユーザーズマニュアル(応用編) — 1.5 固定バッファによる交信 (c: 固定バッファによる交信例)

| 項目 | 内容 |
|---|---|
| 変換範囲 (本ファイル) | 固定バッファによる交信例(システム構成・パラメータ設定・送信側/受信側プログラム例) (原本 p.83-92 / PDFページ85-94) |
| 変換日 | 2026-09-20 |
| 変換方法 | pypdfium2(本文) + PyMuPDF目視(PDF p.89-91, 93-94をrenderで確認。ユニットFB呼出しのラダー図を直接読み取り) |
| ページ対応 | PDFページ = 原本印刷ページ + 2 |
| 関連ファイル | `07_1-5a_...`、`08_1-5b_...` |

> このファイルは原本PDFの参照用リファレンスです。プログラム例は使用ラベル・ラダー(ユニットFB呼出し含む)・
> 説明文を**原文のまま全文**転記しています。
> 未変換の範囲は `00_索引_ladder_reference.md` の変換範囲表を見てください。**設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**

## 目次

- [固定バッファによる交信例](#固定バッファによる交信例-原本-p83)
  - [システム構成](#システム構成-原本-p83)
  - [パラメータ設定(送信側/受信側)](#パラメータ設定-原本-p83-86)
  - [送信側プログラム例](#送信側プログラム例-原本-p87-90)
  - [受信側プログラム例](#受信側プログラム例-原本-p91-92)

---

## 固定バッファによる交信例 (原本 p.83)

TCP/IP通信のActiveオープンを使用した，固定バッファによる交信例を示します。

### システム構成 (原本 p.83)

【図】システム構成(原本 p.83)。GX Works3(エンジニアリングツール)を送信側に接続。送信側(IPアドレス 192.0.1.100)と受信側(IPアドレス 192.0.1.101)がEthernetで接続されている。

### パラメータ設定 (原本 p.83)

エンジニアリングツールをCPUユニットに接続し，パラメータを設定します。

#### 送信側の設定 (原本 p.83-85)

1. CPUユニットを下記で設定します。操作: [プロジェクト][新規作成]
2. 下記で[設定変更]ボタンをクリックし，ユニットラベルを使用する設定にします。
3. [OK]ボタンをクリックし，CPUユニットのユニットラベルを追加します。
4. RJ71EN71を下記で設定します。操作: [ナビゲーションウィンドウ][パラメータ][ユニット情報]→右クリック→[新規ユニット追加]
5. 下記で[OK]ボタンをクリックし，RJ71EN71のユニットラベルを追加します。
6. "基本設定"の内容を，下記で設定します。操作: [ナビゲーションウィンドウ][パラメータ][ユニット情報][RJ71EN71][ポート1 ユニットパラメータ(Ethernet)][基本設定]
7. ネットワーク構成を，下記で設定します。操作: [ナビゲーションウィンドウ][パラメータ][ユニット情報][RJ71EN71][ポート1 ユニットパラメータ(Ethernet)][基本設定][相手機器接続構成設定]
8. 設定したパラメータをCPUユニットに書き込み，CPUユニットをリセット，または電源をOFF→ONします。操作: [オンライン][シーケンサへの書込み]

プログラム例では，上記で示したパラメータ以外はデフォルトの設定を使用します。パラメータについては，本マニュアルのパラメータの章を参照してください。(308ページ パラメータ設定)

#### 受信側の設定 (原本 p.85-86)

1. CPUユニットを設定し，CPUユニットのユニットラベルを追加します。CPUユニットの設定方法とユニットラベルの追加方法は，送信側の場合と同様です。(83ページ 送信側の設定)
2. RJ71EN71を設定し，RJ71EN71のユニットラベルを追加します。RJ71EN71の設定方法とユニットラベルの追加方法は，送信側の場合と同様です。(83ページ 送信側の設定)
3. "基本設定"の内容を，下記で設定します。操作: [ナビゲーションウィンドウ][パラメータ][ユニット情報][RJ71EN71][ポート1 ユニットパラメータ(Ethernet)][基本設定]
4. ネットワーク構成を，下記で設定します。操作: [ナビゲーションウィンドウ][パラメータ][ユニット情報][RJ71EN71][ポート1 ユニットパラメータ(Ethernet)][基本設定][相手機器接続構成設定]
5. 設定したパラメータをCPUユニットに書き込み，CPUユニットをリセット，または電源をOFF→ONします。操作: [オンライン][シーケンサへの書込み]

プログラム例では，上記で示したパラメータ以外はデフォルトの設定を使用します。パラメータについては，本マニュアルのパラメータの章を参照してください。(308ページ パラメータ設定)

### 送信側プログラム例 (原本 p.87-90)

#### 使用ラベル

| 分類 | ラベル名 | 内容 | デバイス |
|---|---|---|---|
| ユニットラベル | RCPU.stSM.bAlways_ON | 常時ON | SM400 |
| ユニットラベル | EN71_EE_1.stPort1.uStatus_HUB_Connection_D.0 | 接続状態 | U0\G5192.0 |
| ユニットラベル | EN71_EE_1.bnCompletion_ConnectionOpen[1] | オープン完了信号(コネクションNo.1) | U0\G1900000.0 |
| ユニットラベル | EN71_EE_1.bnStatus_ConnectionOpenExecution[1] | オープン要求信号(コネクションNo.1) | U0\G1900008.0 |
| ユニットラベル | EN71_EE_1.uCompletion_EthernetInitialized.0 | イニシャル状態 | U0\G1900024.0 |

定義するラベル: 下記のように，グローバルラベルを定義します。

| ラベル名 | データ型 | クラス | 割付け(デバイス/ラベル) | コメント |
|---|---|---|---|---|
| bRunRefresh | ビット | VAR_GLOBAL | M0 | リフレッシュ実行状態 |
| bStartOpen | ビット | VAR_GLOBAL | M1 | オープン指示 |
| bRunOpen | ビット | VAR_GLOBAL | M2 | オープン実行状態 |
| bOpen_OK | ビット | VAR_GLOBAL | M3 | オープン正常完了 |
| bOpen_NG | ビット | VAR_GLOBAL | M4 | オープン異常完了 |
| bStartSend | ビット | VAR_GLOBAL | M5 | データ送信指示 |
| bRunSend | ビット | VAR_GLOBAL | M6 | 送信実行状態 |
| bSend_OK | ビット | VAR_GLOBAL | M7 | 送信正常完了 |
| bSend_NG | ビット | VAR_GLOBAL | M8 | 送信異常完了 |
| bStartClose | ビット | VAR_GLOBAL | M13 | クローズ指示 |
| bRunClose | ビット | VAR_GLOBAL | M14 | クローズ実行中 |
| bClose_OK | ビット | VAR_GLOBAL | M15 | 正常完了 |
| bClose_NG | ビット | VAR_GLOBAL | M16 | 異常完了 |
| bStartOpenFB | ビット | VAR_GLOBAL | M20 | オープン指示(FB起動用) |
| bStartCloseFB | ビット | VAR_GLOBAL | M21 | クローズ指示(FB起動用) |
| uOpenErrID | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D0 | オープンエラーコード |
| uSendErrID | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D10 | 送信エラーコード |
| uCloseErrID | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D30 | クローズエラーコード |
| uSendData | ワード[符号なし]/ビット列[16ビット](0..3) | VAR_GLOBAL | D1000 | 送信データ |

#### 使用ファンクションブロック

本プログラム例で使用するファンクションブロックを示します。

 - M_RJ71EN71_EE_Refresh_Data
 - M_RJ71EN71_EE_ConnectionOpen
 - M_RJ71EN71_EE_Send_Socket
 - M_RJ71EN71_EE_ConnectionClose

#### ラダー(ニモニック)

```
(0)
LD    SM400                                        RCPU.stSM.bAlways_ON
< M_RJ71EN71_EE_Refresh_Data_00B_1 (Data Refresh FB) 呼出し >
    B:i_bEN        = 上記条件
    DUT:i_stModule = EN71_EE_1
    o_bENO:B       → bRunRefresh (M0)

(56)
LD    M1                                            bStartOpen
ANI   U0\G1900000.0                                 EN71_EE_1.bnCompletion_ConnectionOpen[1]
ANI   U0\G1900008.0                                 EN71_EE_1.bnStatus_ConnectionOpenExecution[1]
SET   M20                                           bStartOpenFB

(62)
LD    M20                                           bStartOpenFB
AND   U0\G1900024.0                                 EN71_EE_1.uCompletion_EthernetInitialized.0
AND   U0\G5192.0                                    EN71_EE_1.stPort1.uStatus_HUB_Connection_D.0
< M_RJ71EN71_EE_ConnectionOpen_00B_1 (Connection Open FB) 呼出し >
    B:i_bEN            = 上記条件
    DUT:i_stModule     = EN71_EE_1
    UW:i_uConnectionNo = K1
    pbi_bUseParameters       = 0
    pbi_uProtocol            = 0
    pbi_uOpen_System         = 0
    pbi_uConnUsage           = 0
    pbi_bProcedure           = 0
    pbi_uExist_Confirm       = 0
    pbi_uLocal_Port_No       = 4096
    pbi_uTarget_Port_No      = 4096
    pbi_u2IP_Address         = 0
    pbi_bEnable_Online_Change = 0
    pbi_bData_Code           = 0
    o_bENO:B   → bRunOpen (M2)
    o_bOK:B    → SET bOpen_OK (M3)
    o_bErr:B   → SET bOpen_NG (M4)
    o_uErrId:UW → D0 (uOpenErrID)

(248)
LD    M3                                            bOpen_OK
RST   M1                                            bStartOpen

LD    M4                                            bOpen_NG
RST   M20                                           bStartOpenFB

(252)
LD    M5                                            bStartSend
AND   U0\G1900000.0                                 EN71_EE_1.bnCompletion_ConnectionOpen[1]
MOVP  K6      D1000                                 uSendData[0]
MOVP  K1234   D1001                                 uSendData[1]
MOVP  K5678   D1002                                 uSendData[2]
MOVP  K8901   D1003                                 uSendData[3]

(267)
LD    M5                                            bStartSend
AND   U0\G1900000.0                                 EN71_EE_1.bnCompletion_ConnectionOpen[1]
< M_RJ71EN71_EE_Send_Socket_00B_1 (Send Socket FB) 呼出し >
    B:i_bEN            = 上記条件
    DUT:i_stModule     = EN71_EE_1
    UW:i_uConnectionNo = K1
    UW:i_uSendData     = D1000 (uSendData)
    o_bENO:B   → bRunSend (M6)
    o_bOK:B    → SET bSend_OK (M7)
    o_bErr:B   → SET bSend_NG (M8)
    o_uErrId:UW → D10 (uSendErrID)

(338)
LD    M7                                            bSend_OK
OR    M8                                            bSend_NG
RST   M5                                            bStartSend

(341)
LD    M13                                           bStartClose
AND   U0\G1900000.0                                 EN71_EE_1.bnCompletion_ConnectionOpen[1]
SET   M21                                           bStartCloseFB

(345)
LD    M21                                           bStartCloseFB
< M_RJ71EN71_EE_ConnectionClose_00B_1 (Connection Close FB) 呼出し >
    B:i_bEN            = 上記条件
    DUT:i_stModule     = EN71_EE_1
    UW:i_uConnectionNo = K1
    pbo_uErrConn_No = 0
    o_bENO:B   → bRunClose (M14)
    o_bOK:B    → SET bClose_OK (M15)
    o_bErr:B   → SET bClose_NG (M16)
    o_uErrId:UW → D30 (uCloseErrID)
```

#### 動作説明 (原本 p.90)

(0) ユニットラベルのリフレッシュ処理を行います。(ユニットFBを使用する場合に必要となる処理です)

リフレッシュ処理が完了すると，'リフレッシュ実行状態'(M0)がONされます。

(56) 'オープン指示'(M1)をONすると，コネクションNo.1のオープン処理を行います。

オープン処理が正常に完了すると，'オープン正常完了'(M3)がONされます。

(252) 'データ送信指示'(M5)をONすると，送信データを格納し，受信側に対してデータを送信します。

データの送信が正常に完了すると，'送信正常完了'(M7)がONされます。

(341) 'クローズ指示'(M13)のONにより，コネクションNo.1のクローズ処理を行います。

クローズ処理が正常に完了すると，'正常完了'(M15)がONされます。

### 受信側プログラム例 (原本 p.91-92)

#### 使用ラベル

| 分類 | ラベル名 | 内容 | デバイス |
|---|---|---|---|
| ユニットラベル | RCPU.stSM.bAlways_ON | 常時ON | SM400 |
| ユニットラベル | EN71_EE_1.bnCompletion_ConnectionOpen[1] | オープン完了信号(コネクションNo.1) | U0\G1900000.0 |
| ユニットラベル | EN71_EE_1.bnCompletion_ReceiveSocket_FixedBuffer[1] | ソケット/固定バッファ受信状態信号(コネクションNo.1) | U0\G1900016.0 |
| ユニットラベル | EN71_EE_1.uCompletion_EthernetInitialized.0 | イニシャル状態 | U0\G1900024.0 |

定義するラベル: 下記のように，グローバルラベルを定義します。

| ラベル名 | データ型 | クラス | 割付け(デバイス/ラベル) | コメント |
|---|---|---|---|---|
| bRunRefresh | ビット | VAR_GLOBAL | M0 | リフレッシュ実行状態 |
| bStartRecv | ビット | VAR_GLOBAL | M9 | 受信指示 |
| bRunRecv | ビット | VAR_GLOBAL | M10 | 受信実行状態 |
| bRecv_OK | ビット | VAR_GLOBAL | M11 | 受信正常完了 |
| bRecv_NG | ビット | VAR_GLOBAL | M12 | 受信異常完了 |
| bStartRecvFB | ビット | VAR_GLOBAL | M17 | 受信指示(FB起動用) |
| uRecvErrID | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D20 | 受信エラーコード |
| uRecvData | ワード[符号なし]/ビット列[16ビット](0..5119) | VAR_GLOBAL | D2000 | 受信データ |

#### 使用ファンクションブロック

本プログラム例で使用するファンクションブロックを示します。

 - M_RJ71EN71_EE_Refresh_Data
 - M_RJ71EN71_EE_Recv_Socket

#### ラダー(ニモニック)

```
(0)
LD    SM400                                         RCPU.stSM.bAlways_ON
< M_RJ71EN71_EE_Refresh_Data_00B_1 (Data Refresh FB) 呼出し >
    B:i_bEN        = 上記条件
    DUT:i_stModule = EN71_EE_1
    o_bENO:B       → bRunRefresh (M0)

(68)
LD    SM400                                         RCPU.stSM.bAlways_ON
SET   M_RJ71EN71_EE_Recv_Socket_01A_1.pbi_bReadTiming    受信用FBインスタンスの読出しタイミングをON

(98)
LD    M9                                            bStartRecv
AND   U0\G1900024.0                                 EN71_EE_1.uCompletion_EthernetInitialized.0
AND   U0\G1900000.0                                 EN71_EE_1.bnCompletion_ConnectionOpen[1]
AND   U0\G1900016.0                                 EN71_EE_1.bnCompletion_ReceiveSocket_FixedBuffer[1]
ANI   M11                                           bRecv_OK
ANI   M12                                           bRecv_NG
SET   M17                                           bStartRecvFB

(108)
LD    M17                                           bStartRecvFB
< M_RJ71EN71_EE_Recv_Socket_01A_1 (Receive Socket FB) 呼出し >
    B:i_bEN            = 上記条件
    DUT:i_stModule     = EN71_EE_1
    UW:i_uConnectionNo = K1
    pbi_bReadTiming = 0
    o_bENO:B      → bRunRecv (M10)
    o_bOK:B       → bRecv_OK (M11)
    o_bErr:B      → bRecv_NG (M12)
    o_uErrId:UW   → D20 (uRecvErrID)
    o_uRecvData:UW → D2000 (uRecvData)

(206)
END
```

> 補足(本プロジェクト): (108)のFB出力 o_bOK:B / o_bErr:B は、送信側プログラム例のオープン/送信/クローズFB(SETコイル出力)と異なり、
> 原本の回路図では通常のOUTコイル(丸印)として bRecv_OK(M11) / bRecv_NG(M12) に出力されている。(108)は毎回のFB実行でM11/M12が
> 更新される設計であり、(98)でその2点をB接点(ANI)として実行条件に含めることで多重起動を防いでいる。

#### 動作説明 (原本 p.92)

(0) ユニットラベルのリフレッシュ処理を行います。(ユニットFBを使用する場合に必要となる処理です)

リフレッシュ処理が完了すると，'リフレッシュ実行状態'(M0)がONされます。

(98) '受信指示'(M9)をONすると，送信側から送信されたデータを受信し，'受信データ'(D2000)に格納します。(受信したデータのデータ長により，データが格納されるデバイス範囲は異なります。)

受信が正常に完了すると，'受信正常完了'(M11)がONされます。

> Point
> - 他の用途で使用しているデバイスエリアが受信データによって上書きされないよう，送信元からの最大送信データ長に合わせてデバイスエリアを確保してください。
> - データ受信を連続で実行する場合は，上記のプログラムのように，pbi_bReadTiming(読出しタイミング)をONしてください。
> - CPUユニットのスキャンタイムよりも短い間隔でデータを受信する場合は，上記のプログラムのように'受信正常完了'(M11)および'受信異常完了'(M12)のB接点を受信用のFBの実行条件に追加してください。'受信正常完了'(M11)および'受信異常完了'(M12)のB接点がない場合，'受信指示(FB起動用)'(M17)がOFF→ONせず，受信用のFBが実行されない可能性があります。

---

## 図・原本参照が必要な項目の一覧 (原本 p.83-92)

| 項目 | 原本ページ | 扱い |
|---|---|---|
| システム構成図 | p.83 | 文章化済み(上記参照) |
| パラメータ設定のGX Works3画面スクリーンショット | p.83-86 | UI画面のため操作パスのみ本文に記載済み |
| 送信側/受信側ラダー(ユニットFB呼出し含む) | p.87-92 | ニモニックとして全文転記済み(上記参照) |

## 抜けチェック結果 (本md管理用 / 原本外)

原文(PDF p.85-94)とmdを突き合わせ、手順・表の欠落なし。ラダー(ユニットFB呼出し)はテキスト抽出では崩れるため、p.89-91, 93-94をrenderして目視で書き起こした。
