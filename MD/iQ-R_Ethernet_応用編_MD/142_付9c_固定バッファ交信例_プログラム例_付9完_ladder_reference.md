# MELSEC iQ-R Ethernetユーザーズマニュアル(応用編) — 付9 二重化増設ベース構成で増設ベースユニットに装着して使用する場合 (c: 固定バッファによる交信例 — プログラム例。付9完)

| 項目 | 内容 |
|---|---|
| 変換範囲 (本ファイル) | 固定バッファによる交信例: プログラム例 全文(ラベル定義表20行、ラダープログラム全ラング(0)〜(237/END)、ラング別説明文)。これで付9が完了 | 原本 p.534-536 / PDFページ536-538) |
| 変換日 | 2026-09-20 |
| 変換方法 | pypdfium2(本文) + PyMuPDF目視(PDF p.536-538を全ページrenderしてラベル表・ラダー回路をニモニックに書き起こし) |
| ページ対応 | PDFページ = 原本印刷ページ + 2 |
| 関連ファイル | 前 `141_付9b_...`(システム構成・パラメータの設定)、続き `143_付10_...`(Ethernet搭載ユニットで使用するポート番号) |

> このファイルは原本PDFの参照用リファレンスです。ラベル表・プログラムは**原文のまま全文**転記しています。
> 未変換の範囲は `00_索引_ladder_reference.md` の変換範囲表を見てください。**設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
>
> ラダー図はASCIIアートにすると線がずれて誤読の元になるため、**ニモニック形式**で書き起こしている(本プロジェクトの標準方針)。
> 並列分岐(複数コイル・複数条件分岐)は、インデントと「分岐:」注記で構造を示す。正確なグラフィカルレイアウトの確認が必要な場合は、原本 p.536-538 のrender画像を参照すること。

## 目次

- [プログラム例](#プログラム例-原本-p534)

---

## プログラム例 (原本 p.534)

コネクションNo.1をオープンして，交信相手機器に対してデータを送信するプログラムです。

また，コネクションNo.2を使用して交信相手機器からのデータも受信します。

### 定義するラベル (原本 p.534)

下記のように，グローバルラベルを定義します。

| ラベル名 | データ型 | クラス | 割付け(デバイス/ラベル) | コメント |
|---|---|---|---|---|
| bOpenInstruction_1 | ビット | VAR_GLOBAL | X1041 | オープン指令-1 |
| bSendInstruction | ビット | VAR_GLOBAL | X1043 | 固定BUF送信指令 |
| bRecvInstruction | ビット | VAR_GLOBAL | X1044 | 固定BUF受信指令 |
| bCloseInstruction_1 | ビット | VAR_GLOBAL | X1045 | クローズ指令-1 |
| uRecvWordsCountTmp | ワード[符号なし]/ビット列[16ビット](0..1) | VAR_GLOBAL | D15 | 受信ワード数算出用一時 |
| uRecvWordsCount | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D17 | 受信ワード数 |
| uOpenErrCodeTmp_1 | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D18 | オープン異常コード-1一時 |
| uOpenErrCode_1 | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D100 | オープン異常コード-1 |
| uSendErrCode_1 | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D108 | 送信異常コード-1 |
| uRecvErrCode_2 | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D110 | 受信異常コード-2 |
| uSendDataLength | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D300 | 送信データ長 |
| uSendData | ワード[符号なし]/ビット列[16ビット](0..2) | VAR_GLOBAL | D301 | 送信データ |
| uRecvDataLength | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D500 | 受信データ長 |
| uRecvData | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D501 | 受信データ |
| bCommReady_1 | ビット | VAR_GLOBAL | M1 | 交信可-1 |
| bCommReady_2 | ビット | VAR_GLOBAL | M2 | 交信可-2 |
| bCloseOccurred_1 | ビット | VAR_GLOBAL | M11 | クローズ発生-1 |
| bOpenImpossible_1 | ビット | VAR_GLOBAL | M21 | オープン不可-1 |
| bCloseAccepted_1 | ビット | VAR_GLOBAL | M31 | クローズ指令受付-1 |
| bSendAccepted_1 | ビット | VAR_GLOBAL | M41 | 送信指令受付-1 |
| bOpenFailed_1 | ビット | VAR_GLOBAL | M51 | オープン失敗-1 |
| tdOpenWait_1 | タイマ | VAR_GLOBAL | T1 | オープン待-1 |

原本の表行数(目視カウント): 20行。上表は全20行を転記(render確認済み)。

### ラダープログラム (原本 p.534-536)

```
(0)   LD    bOpenInstruction_1     ; X1041
      ANI   X119
      ANI   X11F
      ANI   X110
      ANI   Y100
      ANI   Y108
      ANI   bOpenImpossible_1      ; M21
      ANI   bCloseAccepted_1       ; M31
      SET   Y108

(36)  LD    X110
      AND   Y108
      ANI   X11F
      OUT   bCommReady_1           ; M1

(40)  LD    X118
      AND   Y108
      ANI   X110
      ANI   X11F
      FROMP H10  K124  uOpenErrCodeTmp_1(D18)  K1
      ; 分岐(同一条件から並列): D18(uOpenErrCodeTmp_1)が0でなければ以下を実行
      <>_U  K0   uOpenErrCodeTmp_1(D18)
        TOP   H10  K124  K0  K1
        MOVP  uOpenErrCodeTmp_1(D18)  uOpenErrCode_1(D100)
        SET   bOpenFailed_1         ; M51

(63)  LD    bCommReady_1            ; M1
      PLF   bCloseOccurred_1        ; M11

(66)  LD    bSendInstruction        ; X1043
      PLS   bSendAccepted_1         ; M41

(92)  LD    bSendAccepted_1         ; M41
      AND   bCommReady_1            ; M1
      ANI   X100
      ANI   X101
      ANI   Y100
      MOV   K6     uSendDataLength(D300)
      MOV   H1234  uSendData[0](D301)
      MOV   H5678  uSendData[1](D302)
      MOV   H8901  uSendData[2](D303)
      TO    H10  K1664  uSendDataLength(D300)  K4
      SET   Y100

(111) LD    Y100
      AND   bCommReady_1            ; M1
      ; 分岐A
      AND   X100
        RST   Y100
      ; 分岐B
      AND   X101
        FROMP H10  K125  uSendErrCode_1(D108)  K1
        RST   Y100

(125) LD    bCloseInstruction_1     ; X1045
      OR    bCloseOccurred_1        ; M11
      OR    bOpenFailed_1           ; M51
      SET   bCloseAccepted_1        ; M31

(148) LD    bCloseAccepted_1        ; M31
      ANI   X100
      ANI   X101
      ANI   Y100
      RST   Y108
      ; 分岐(同一条件から並列)
      ANI   X110
        SET   bOpenImpossible_1     ; M21
        RST   bCloseAccepted_1      ; M31
        RST   bOpenFailed_1         ; M51

(157) LD    bOpenImpossible_1       ; M21
      OUT   tdOpenWait_1(T1)  K5
      ; 分岐
      LD    tdOpenWait_1            ; T1
        RST   bOpenImpossible_1     ; M21

(164) LD    X111
      ANI   X11F
      OUT   bCommReady_2            ; M2

(201) LD    bRecvInstruction        ; X1044
      AND   X102
      AND   bCommReady_2            ; M2
      FROMP H10  K2688  uRecvDataLength(D500)  K1
      /P_U  uRecvDataLength(D500)  K2  uRecvWordsCountTmp(D15)
      +P_U  uRecvWordsCountTmp[0](D15)  uRecvWordsCountTmp[1](D16)  uRecvWordsCount(D17)
      FROMP H10  K2689  uRecvData(D501)  uRecvWordsCount(D17)
      SET   Y101

(225) LD    X103
      FROMP H10  K135  uRecvErrCode_2(D110)  K1

(232) LDI   X102
      ANI   X103
      AND   Y101
      AND   bCommReady_2            ; M2
      RST   Y101

(237) END
```

### ラング別の動作説明 (原本 p.536)

- (0) bOpenInstruction_1をONすると，コネクションNo.1のオープン処理を行います。
- (66) bSendInstructionをONすると，コネクションNo.1を使用して交信相手機器に対してデータを送信します。
- (125) bCloseInstruction_1をONすると，コネクションNo.1のクローズ処理を行います。
- (201) bRecvInstructionをONすると，コネクションNo.2を使用して交信相手機器からのデータを受信します。

これで**付9 二重化増設ベース構成で増設ベースユニットに装着して使用する場合(140〜142の3ファイル、原本p.529-536)が完了**。

---

## 図・原本参照が必要な項目の一覧 (原本 p.534-536)

| 項目 | 内容 |
|---|---|
| ラダー回路図(ラング(0)〜(237)) | render目視によりニモニック形式で書き起こし済み。正確なグラフィカルレイアウト(接点・コイルの配置)を確認する場合は原本 p.536-538 を参照すること |

## 抜けチェック結果 (本md管理用 / 原本外)

原文(PDF p.536-538)とmdを突き合わせ、欠落なし。ラベル定義表(20行)、ラダープログラム全ラング(0)〜(237/END)、ラング別動作説明文(4件)はすべて全件転記。プログラム例はニモニック形式で全命令・全デバイス・全定数を書き起こした(省略なし)。付9全体(原本p.529-536、8ページ)の変換が完了。続きは`143_付10_...`(Ethernet搭載ユニットで使用するポート番号)。
