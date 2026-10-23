# 三菱 MELSEC iQ-R シンプルモーションユニット ユーザーズマニュアル(応用編) 付録 付4 リモートヘッドユニット装着時の運転例[RD77MS] 前半(システム構成例〜プログラム例 特殊始動命令を通常始動に設定)

| 項目 | 内容 |
|---|---|
| 原本 | 三菱電機 MELSEC iQ-R シンプルモーションユニット ユーザーズマニュアル(応用編)(形名 RD77-U-APP) |
| 発行元 | 三菱電機株式会社 |
| 資料番号・版数 | IB(名)-0300246-P (2509)MEE / P版 (2025年9月作成) |
| 対象形名 | RD77MS2 / RD77MS4 / RD77MS8 / RD77MS16 / RD77GF4 / RD77GF8 / RD77GF16 / RD77GF32 |
| 原本PDF | `PDF/MELSEC iQ_Rシンプルモーションユニットユーザーズマニュアル(応用編).pdf` |
| 本ファイルの範囲 | 付4 リモートヘッドユニット装着時の運転例[RD77MS] の冒頭から「システム構成例」「マスタ局の設定」「インテリジェントデバイス局の設定」「ネットワーク状態の確認」「プログラム例」(ユニットラベル、グローバルラベル、マスタ局動作状態確認、パラメータ設定プログラム、位置決めデータ設定プログラム、ブロック始動データ設定プログラム、特殊始動命令を通常始動に設定)まで。印刷 p.791-806 / PDF p.793-808。前ファイルは「付3 SSCNETIII(/H)対応機器[RD77MS]」(印刷 p.790 / PDF p.792 まで)、次ファイルは同じ付4のプログラム例「原点復帰要求OFFプログラム」(印刷 p.807 / PDF p.809)から |
| ページ対応 | 印刷ページ = PDFページ − 2。本文中の「〇〇ページ参照」は印刷ページのまま |
| 変換日 | 2026-10-23 |
| 変換方法 | pypdfium2(本文) + PyMuPDF 200dpi 画像の目視(全ページ) |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。

**転記上の扱い**: 本文・Pointは原文のまま全文転記した。GX Works3 の設定画面(新規作成、新規ユニット追加、ユニットラベル追加ダイアログ、必須設定、ネットワーク構成設定、リフレッシュ設定、ネットワーク必須設定)は画面上の設定値を全項目表に起こした。グローバルラベル一覧(175行、原本では画面キャプチャ)は画像から全行を読み取り、ラベル名の綴り(「Memmory」「Parametar」等)を含め原本どおりとした。配列化したラベルの内容(100行)は「内容」列の結合セルを各行に展開した。ラダー図(プログラム例)は原本にニモニック記載が無いため、すべて**図から書き起こし**たニモニックで示した。ステップ番号は原本のラダー図に表示されている回路先頭の番号((0)(3)(12)…)をそのまま付けた。1回路から複数の分岐(接点付き)を出している箇所は MPS/MRD/MPP で表したが、これは図の接続から起こしたもので原本の表記ではない。デバイス欄にはラダー図上のラベル名の下に表示されたデバイスを右側に併記した(モジュールラベル GF11_1.～ はラダー図上にデバイス表示が無いため、ユニットラベル表のデバイスを参照)。命令のオペランド中のラベルは `ラベル名(デバイス)` で表記した。原本のページ参照記号は「☞」で表記し参照先は印刷ページのまま、マニュアル参照のアイコン(本の絵)は省略してマニュアル名のみを原文どおり記載した。操作手順のマウスアイコンは「操作:」と表記した。矢印「⇨」「→」はテキスト抽出で欠落していたため画像を正とした。

## 主要用語 対訳表 (Glossary) (付4 / 原本 p.793-808)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| リモートヘッドユニット | Remote head module | RJ72GF15-T2 | 参考訳 |
| マスタ・ローカルユニット | Master/local module | RJ71GF11-T2 | 参考訳 |
| マスタ局 | Master station | 局番0 | 参考訳 |
| インテリジェントデバイス局 | Intelligent device station | 局番1 | 参考訳 |
| ネットワークNo. / 局番 | Network No. / Station No. | — | 参考訳 |
| CC-Link IEフィールドネットワーク | CC-Link IE Field Network | CC IE Field | 参考訳 |
| CC-Link IEフィールドネットワーク診断 | CC-Link IE Field Network diagnostics | — | 参考訳 |
| エンジニアリングツール | Engineering tool | GX Works3 | 参考訳 |
| ユニットラベル | Module label | — | 参考訳 |
| グローバルラベル | Global label | VAR_GLOBAL | 参考訳 |
| 配列化したラベル | Array label | — | 参考訳 |
| ユニットパラメータ / ユニット拡張パラメータ | Module parameter / Module extended parameter | — | 参考訳 |
| 必須設定 / 基本設定 | Required settings / Basic settings | — | 参考訳 |
| ネットワーク構成設定 | Network configuration settings | — | 参考訳 |
| リフレッシュ設定 | Refresh settings | — | 参考訳 |
| ネットワーク必須設定 | Network required settings | CPUパラメータ | 参考訳 |
| リンクスキャンタイム | Link scan time | — | 参考訳 |
| リンク特殊リレー/レジスタ | Link special relay / register | SB / SW | 参考訳 |
| 自局データリンク異常状態 | Data link error status of own station | SB0049 | 参考訳 |
| 各局データリンク状態 | Data link status of each station | SW00B0 | 参考訳 |
| RUN後1スキャンON / RUN後1スキャンOFF | ON for one scan after RUN / OFF for one scan after RUN | SM402 / SM403 | 参考訳 |
| マスタ局動作状態確認 | Master station operation status check | — | 参考訳 |
| 交信条件の成立フラグ | Communication condition satisfaction flag | M120 | 参考訳 |
| マスタコントロール | Master control | MC / N0 | 参考訳 |
| 完了デバイス | Completion device | — | 参考訳 |
| 基本パラメータ1 | Basic parameter 1 | — | 参考訳 |
| 原点復帰基本パラメータ | Home position return basic parameter | — | 参考訳 |
| 速度・位置切換え制御(ABSモード) | Speed-position switching control (ABS mode) | — | 参考訳 |
| 位置決めデータ | Positioning data | — | 参考訳 |
| ブロック始動データ / 始動ブロック | Block start data / Start block | — | 参考訳 |
| 特殊始動命令 / 通常始動 | Special start instruction / Normal start | — | 参考訳 |
| シーケンサレディ信号 | PLC READY signal | Y100 (bPLCReady) | 参考訳 |
| 全軸サーボON信号 | All axis servo ON signal | Y101 | 参考訳 |
| 同期用フラグ | Synchronization flag | X101 | 参考訳 |
| BUSY信号 | BUSY signal | X110〜X11F | 参考訳 |
| 位置決め始動信号 | Positioning start signal | Y110〜Y11F | 参考訳 |
| ソフトウェアストロークリミット上限値 / 下限値 | Software stroke limit upper / lower limit value | — | 参考訳 |
| 速度制御時の送り現在値 | Feed current value during speed control | — | 参考訳 |
| 速度・位置機能選択 | Speed-position function selection | — | 参考訳 |
| 原点復帰方式 / 原点復帰方向 / 原点アドレス | OPR method / OPR direction / Home position address | — | 参考訳 |
| 原点復帰速度 / クリープ速度 / 原点復帰リトライ | OPR speed / Creep speed / OPR retry | — | 参考訳 |

## 変換範囲表 (付4 / 原本 p.793-808)

| 原本ページ | 節 | 扱い |
|---|---|---|
| p.793 (印刷 p.791) | 付4 冒頭、システム構成例 | 全文 |
| p.794-796 (印刷 p.792-794) | マスタ局の設定 | 全文(設定画面の設定値を表に起こした) |
| p.797-798 (印刷 p.795-796) | インテリジェントデバイス局の設定 | 全文(設定画面の設定値を表に起こした) |
| p.799 (印刷 p.797) | ネットワーク状態の確認、プログラム例(冒頭)、ユニットラベル | 全文 |
| p.799-803 (印刷 p.797-801) | グローバルラベル(グローバルラベル一覧、配列化したラベルの内容) | 全文(175行 / 100行) |
| p.804-808 (印刷 p.802-806) | マスタ局動作状態確認、パラメータ設定プログラム、位置決めデータ設定プログラム、ブロック始動データ設定プログラム、特殊始動命令を通常始動に設定 | 全文(ラダーは図から書き起こしたニモニック) |
| p.809 以降 (印刷 p.807-) | 付4 プログラム例「原点復帰要求OFFプログラム」以降 | **未変換**(次ファイル 付04b の範囲) |
| p.1-792 / 付3 以前 | 本文各章・付1〜付3 | **未変換**(別ファイルの範囲) |

## 目次

- 付録
  - 付4 リモートヘッドユニット装着時の運転例[RD77MS]
    - システム構成例
    - マスタ局の設定
    - インテリジェントデバイス局の設定
    - ネットワーク状態の確認
    - プログラム例
      - ユニットラベル
      - グローバルラベル(■グローバルラベル一覧 / ■配列化したラベルの内容)
      - マスタ局動作状態確認
      - パラメータ設定プログラム(■基本パラメータ1(軸1)の設定 / ■原点復帰基本パラメータ(軸1)の設定 / ■速度・位置切換え制御(ABSモード)用パラメータ設定プログラム(軸1の場合))
      - 位置決めデータ設定プログラム(■位置決めデータNo.1(軸1)の場合)
      - ブロック始動データ設定プログラム(■始動ブロック0のブロック始動データ(軸1)1～5ポイント目までの設定の場合)
      - 特殊始動命令を通常始動に設定
- 転記時の要確認一覧

## 付録 (付録 / 印刷 p.791-806 / 原本 p.793-808)

### 付4 リモートヘッドユニット装着時の運転例[RD77MS] (付4 / 印刷 p.791 / 原本 p.793)

リモートヘッドユニット装着時の運転例を示します。

#### システム構成例 (付4 / 印刷 p.791 / 原本 p.793)

下記のシステム構成を使用して説明します。

【図】システム構成図(付4 / 印刷 p.791 / 原本 p.793)
- (1) マスタ局のベース(左): 電源ユニット、CPUユニット、マスタ・ローカルユニット、入力ユニット×2 が装着されている。
- (2) インテリジェントデバイス局のベース(右): 電源ユニット、リモートヘッドユニット、シンプルモーションユニット(RD77MS16)が装着されている。
- (1)のマスタ・ローカルユニットと(2)のリモートヘッドユニットが Ethernet ケーブル1本で接続されている。

(1)マスタ局(ネットワークNo.1，局番0)
- 電源ユニット: R61P
- CPUユニット: R04CPU
- マスタ・ローカルユニット: RJ71GF11-T2(先頭入出力番号: 0000H~001FH)
- 入力ユニット: RX41C4(先頭入出力番号: 0020H~003FH)
- 入力ユニット: RX41C4(先頭入出力番号: 0040H~005FH)

(2)インテリジェントデバイス局(ネットワークNo.1，局番1)
- 電源ユニット: R61P
- リモートヘッドユニット: RJ72GF15-T2
- シンプルモーションユニット: RD77MS16(先頭入出力番号: 0100H~011FH)

#### マスタ局の設定 (付4 / 印刷 p.792-794 / 原本 p.794-796)

エンジニアリングツールをマスタ局のCPUユニットに接続し，パラメータを設定します。

1. 下記の内容にてプロジェクトを作成します。

   操作: [プロジェクト]⇨[新規作成]

   【図】「新規作成」ダイアログ(付4 / 印刷 p.792 / 原本 p.794)

   | 項目 | 設定 |
   |---|---|
   | シリーズ(S) | RCPU |
   | 機種(T) | R04 |
   | 動作モード(M) | (空欄・選択不可) |
   | プログラム言語(G) | ラダー |

2. ユニットラベルを使用するように設定し，CPUユニットのユニットラベルを追加します。

   【図】「MELSOFT GX Works3」ダイアログ(付4 / 印刷 p.792 / 原本 p.794)
   - 表示メッセージ: ユニットを追加します。[ユニット形名] R04CPU [先頭I/O No.] 3E00
   - ユニットの設定: ユニットラベル:使用する
   - 「以降、このダイアログを表示しない(D)」: チェックなし → [OK]

3. マスタ・ローカルユニットを下記の内容で追加します。

   操作: [ナビゲーションウィンドウ]⇨[パラメータ]⇨[ユニット情報]⇨右クリック⇨[新規ユニット追加]

   【図】「新規ユニット追加」ダイアログ(付4 / 印刷 p.792 / 原本 p.794)

   | 区分 | 項目 | 設定 |
   |---|---|---|
   | ユニット選択 | ユニット種別 | ネットワークユニット |
   | ユニット選択 | ユニット形名 | RJ71GF11-T2 |
   | ユニット選択 | 局種別 | マスタ局 |
   | 詳細設定 / 装着位置 | 装着ベース | 基本ベース(表示のみ) |
   | 詳細設定 / 装着位置 | 装着スロットNo. | 0 |
   | 詳細設定 / 装着位置 | 先頭I/ONo.指定 | 指定しない |
   | 詳細設定 / 装着位置 | 先頭I/ONo. | 0000 H(表示のみ) |
   | 詳細設定 / 装着位置 | 1スロット占有点数 | 32点(表示のみ) |

   (ダイアログ下部の説明欄: 「局種別 / 局種別を選択します。」)

4. ユニットラベルを使用するように設定し，マスタ・ローカルユニットのユニットラベルを追加します。

   【図】「MELSOFT GX Works3」ダイアログ(付4 / 印刷 p.793 / 原本 p.795)
   - 表示メッセージ: ユニットを追加します。[ユニット形名] RJ71GF11-T2 [先頭I/O No.] 0000
   - ユニットの設定: ユニットラベル:使用する
   - 「以降、このダイアログを表示しない(D)」: チェックなし → [OK]

5. マスタ・ローカルユニットの"ユニットパラメータ"の"必須設定"を，下記の内容で設定します。

   操作: [ナビゲーションウィンドウ]⇨[パラメータ]⇨[ユニット情報]⇨[RJ71GF11-T2]⇨[必須設定]

   【図】必須設定画面(付4 / 印刷 p.793 / 原本 p.795)

   | 項目(グループ) | 項目 | 設定 |
   |---|---|---|
   | 局種別設定 | 局種別 | マスタ局 |
   | ネットワークNo設定 | ネットワークNo. | 1 |
   | 局番設定 | 局番設定方法 | パラメータで設定 |
   | 局番設定 | 局番 | 0 |
   | パラメータ設定方法 | 基本設定/応用設定の設定方法 | パラメータで設定 |

6. マスタ・ローカルユニットの"ユニットパラメータ"の"ネットワーク構成設定"を，下記の内容で設定します。

   操作: [ナビゲーションウィンドウ]⇨[パラメータ]⇨[ユニット情報]⇨[RJ71GF11-T2]⇨[基本設定]⇨[ネットワーク構成設定]

   【図】「CC IE Field構成(先頭I/O : 0000)」画面(付4 / 印刷 p.793 / 原本 p.795)
   - モード設定(M): オンライン(標準モード)(表示のみ)
   - 割付方法(A): 先頭/最終
   - リンクスキャンタイム(概算値): 0.76 ms
   - 下部の構成図: 自局(局番0 マスタ局、総局数:1、ライン/スター)と局番1 の RJ72GF15-T2 が接続されている。

   | 台数 | 形名 | 局番 | 局種別 | RX/RY設定 点数 | RX/RY設定 先頭 | RX/RY設定 最終 | RWw/RWr設定 点数 | RWw/RWr設定 先頭 | RWw/RWr設定 最終 | 予約/エラー無効局/系切替え監視対象局 | ペアリング | ネットワーク同期通信設定 |
   |---|---|---|---|---|---|---|---|---|---|---|---|---|
   | 0 | 自局 | 0 | マスタ局 | | | | | | | | | |
   | 1 | RJ72GF15-T2 | 1 | インテリジェントデバイス局 | 32 | 0100 | 011F | 256 | 0000 | 00FF | 設定なし | | 同期しない |

7. マスタ・ローカルユニットの"ユニットパラメータ"の"リフレッシュ設定"を，下記の内容で設定します。

   操作: [ナビゲーションウィンドウ]⇨[パラメータ]⇨[ユニット情報]⇨[RJ71GF11-T2]⇨[基本設定]⇨[リフレッシュ設定]

   【図】「0000:RJ71GF11-T2 ユニットパラメータ」のリフレッシュ設定画面(付4 / 印刷 p.794 / 原本 p.796)。画面下の説明欄: 「CC-Link IE フィールドネットワークユニットのリンク特殊リレー/レジスタ，リンクデバイスとCPUユニットのデバイス間の転送範囲を設定します。」

   | No. | リンク側 デバイス名 | リンク側 点数 | リンク側 先頭 | リンク側 最終 | CPU側 リフレッシュ先 | CPU側 デバイス名 | CPU側 点数 | CPU側 先頭 | CPU側 最終 |
   |---|---|---|---|---|---|---|---|---|---|
   | - | SB | 512 | 00000 | 001FF | ユニットラベル | | | | |
   | - | SW | 512 | 00000 | 001FF | ユニットラベル | | | | |
   | 1 | RX | 32 | 00100 | 0011F | 指定デバイス | X | 32 | 00100 | 0011F |
   | 2 | RY | 32 | 00100 | 0011F | 指定デバイス | Y | 32 | 00100 | 0011F |
   | 3 | RWr | 256 | 00000 | 000FF | 指定デバイス | W | 256 | 00000 | 000FF |
   | 4 | RWw | 256 | 00000 | 000FF | 指定デバイス | W | 256 | 00100 | 001FF |

   (No.5 以降は空欄)

8. 設定したパラメータをマスタ局のCPUユニットに書き込み，CPUユニットをリセット，または電源をOFF→ONします。

   操作: [オンライン]⇨[シーケンサへの書込み]

> **Point**
> 手順にて示していないマスタ・ローカルユニットのパラメータは，デフォルトの設定を使用します。マスタ・ローカルユニットのパラメータについては，下記を参照してください。
> MELSEC iQ-R CC-Link IEフィールドネットワークユーザーズマニュアル(応用編)

#### インテリジェントデバイス局の設定 (付4 / 印刷 p.795-796 / 原本 p.797-798)

エンジニアリングツールをインテリジェントデバイス局のリモートヘッドユニットに接続し，パラメータを設定します。

1. 下記の内容にてプロジェクトを作成します。

   操作: [プロジェクト]⇨[新規作成]

   【図】「新規作成」ダイアログ(付4 / 印刷 p.795 / 原本 p.797)

   | 項目 | 設定 |
   |---|---|
   | シリーズ(S) | RCPU |
   | 機種(T) | RJ72GF15-T2 |
   | 動作モード(M) | (空欄・選択不可) |
   | プログラム言語(G) | 指定しない |

2. リモートヘッドユニットの"CPUパラメータ"の"ネットワーク必須設定"を，下記の内容で設定します。

   操作: [ナビゲーションウィンドウ]⇨[パラメータ]⇨[RJ72GF15-T2]⇨[CPUパラメータ]⇨[ネットワーク必須設定]

   【図】ネットワーク必須設定画面(付4 / 印刷 p.795 / 原本 p.797)

   | 項目(グループ) | 項目 | 設定 |
   |---|---|---|
   | ネットワークNo.設定 | ネットワークNo. | 1 |
   | 局番設定 | 局番 | 1 |

3. RD77MSを下記の内容で追加します。

   操作: [ナビゲーションウィンドウ]⇨[パラメータ]⇨[ユニット情報]⇨右クリック⇨[新規ユニット追加]

   【図】「新規ユニット追加」ダイアログ(付4 / 印刷 p.795 / 原本 p.797)

   | 区分 | 項目 | 設定 |
   |---|---|---|
   | ユニット選択 | ユニット種別 | シンプルモーション |
   | ユニット選択 | ユニット形名 | RD77MS16 |
   | ユニット選択 | 局種別 | (空欄・選択不可) |
   | 詳細設定 / 装着位置 | 装着ベース | 基本ベース(表示のみ) |
   | 詳細設定 / 装着位置 | 装着スロットNo. | 0 |
   | 詳細設定 / 装着位置 | 先頭I/ONo.指定 | 指定しない |
   | 詳細設定 / 装着位置 | 先頭I/ONo. | 0000 H(表示のみ) |
   | 詳細設定 / 装着位置 | 1スロット占有点数 | 32点(表示のみ) |

   (ダイアログ下部の説明欄: 「ユニット種別 / ユニット種別を選択します。」)

4. ユニットラベルを使用しないように設定します。

   【図】「MELSOFT GX Works3」ダイアログ(付4 / 印刷 p.796 / 原本 p.798)
   - 表示メッセージ: ユニットを追加します。[ユニット形名] RD77MS16 [先頭I/O No.] 0000
   - ユニットの設定: ユニットラベル:使用しない
   - 「以降、このダイアログを表示しない(D)」: チェックなし → [OK]

5. RD77MSの"ユニットパラメータ"の"リフレッシュ設定"を，下記の内容で設定します。

   操作: [ナビゲーションウィンドウ]⇨[パラメータ]⇨[ユニット情報]⇨[RD77MS16]⇨[ユニットパラメータ]⇨[リフレッシュ設定]

   【図】RD77MS16 のリフレッシュ設定画面(付4 / 印刷 p.796 / 原本 p.798)。項目グループ「設定したタイミングでリフレッシュ」→「CPUへ転送」(説明: バッファメモリのデータを指定したデバイスに転送します。)。画面に表示されている列は軸1〜軸5。

   | 項目 | 軸1 | 軸2 | 軸3 | 軸4 | 軸5 |
   |---|---|---|---|---|---|
   | 送り現在値 | | | | | |
   | 送り機械値 | | | | | |
   | 送り速度 | | | | | |
   | 軸エラー番号 | | | | | |
   | 軸ワーニング番号 | | | | | |
   | 有効Mコード | | | | | |
   | 軸動作状態 | | | | | |
   | カレント速度 | | | | | |
   | 軸送り速度 | | | | | |
   | 速度・位置切換え制御の位置決め移動量 | | | | | |
   | 外部入力信号 | | | | | |
   | ステータス | W1000 | | | | |
   | 目標値 | | | | | |

   (空欄は設定なし。設定されているのは軸1の「ステータス」= W1000 のみ)

6. 本プログラムでは，プログラムにてパラメータを設定しているため，エンジニアリングツールのユニットパラメータの設定は，デフォルト値にしてください。エンジニアリングツールでユニットパラメータを設定する場合は，下記を参照してください。
   ☞ 419ページ ユニットパラメータ

7. 設定したパラメータをインテリジェントデバイス局のリモートヘッドユニットに書き込み，リモートヘッドユニットをリセット，または電源をOFF→ONします。

   操作: [オンライン]⇨[シーケンサへの書込み]

> **Point**
> 手順にて示していないリモートヘッドユニットのパラメータは，デフォルトの設定を使用します。リモートヘッドユニットのパラメータについては，下記を参照してください。
> MELSEC iQ-R CC-Link IEフィールドネットワークリモートヘッドユニットユーザーズマニュアル(応用編)

#### ネットワーク状態の確認 (付4 / 印刷 p.797 / 原本 p.799)

マスタ局およびインテリジェントデバイス局にパラメータを設定後，マスタ局とインテリジェントデバイス局が正常にデータリンクできる状態かを確認します。確認は，エンジニアリングツールのCC-Link IEフィールドネットワーク診断を使用します。
マスタ局からのCC-Link IEフィールドネットワーク診断については，下記を参照してください。
MELSEC iQ-R CC-Link IEフィールドネットワークユーザーズマニュアル(応用編)

#### プログラム例 (付4 / 印刷 p.797-806 / 原本 p.799-808)

プログラムはマスタ局のCPUユニットに書き込んでください。

##### ユニットラベル (付4 / 印刷 p.797 / 原本 p.799)

プログラムでは，CPUユニットおよびマスタ・ローカルユニットのユニットラベルを使用しています。

| ラベル名 | 内容 | デバイス |
|---|---|---|
| RCPU.stSM.bAfter_RUN1_Scan_ON | RUN後1スキャンON | SM402 |
| RCPU.stSM.bAfter_RUN1_Scan_OFF | RUN後1スキャンOFF | SM403 |
| GF11_1.bSts_DataLinkError | 自局データリンク異常状態 | SB0049 |
| GF11_1.bnSts_DataLinkError_Station[1] | 各局データリンク状態(局番1) | SW00B0.0 |

##### グローバルラベル (付4 / 印刷 p.797-801 / 原本 p.799-803)

###### ■グローバルラベル一覧 (付4 / 印刷 p.797-799 / 原本 p.799-801)

下記のように，グローバルラベルを定義します。

【図】GX Works3 のグローバルラベル設定画面のキャプチャ(No.1〜175)。画像から全行を表に起こした(No.1〜50: 印刷 p.797、No.51〜150: 印刷 p.798、No.151〜175: 印刷 p.799)。

| No. | ラベル名 | データ型 | クラス | 割付け(デバイス/ラベル) | コメント |
|---|---|---|---|---|---|
| 1 | bInputUnitError | ビット | VAR_GLOBAL | X0 | ユニット異常 |
| 2 | bUnitReady | ビット | VAR_GLOBAL | X0F | ユニットREADY |
| 3 | bInputOPR_RequestFlagOffRequest | ビット | VAR_GLOBAL | X20 | 原点復帰要求OFF指令 |
| 4 | bInputExternalCommandValidRequest | ビット | VAR_GLOBAL | X21 | 外部指令有効指令 |
| 5 | bInputExternalCommandInvalidRequest | ビット | VAR_GLOBAL | X22 | 外部指令無効指令 |
| 6 | bInputFastStartRequest | ビット | VAR_GLOBAL | X23 | 機械原点復帰指令 |
| 7 | bInputFastOPR_StartRequest | ビット | VAR_GLOBAL | X24 | 高速原点復帰指令 |
| 8 | bInputSetStartPositioningNoRequest | ビット | VAR_GLOBAL | X25 | 位置決め始動指令 |
| 9 | bInputSpeedPositionSwitchingRequest | ビット | VAR_GLOBAL | X26 | 速度・位置切換え運転指令 |
| 10 | bInputSpeedPositionSwitchingEnableRequest | ビット | VAR_GLOBAL | X27 | 速度・位置切換え許可指令 |
| 11 | bInputSpeedPositionSwitchingDisableRequest | ビット | VAR_GLOBAL | X28 | 速度・位置切換え禁止指令 |
| 12 | bInputChangeMovementAmountRequest | ビット | VAR_GLOBAL | X29 | 移動量変更指令 |
| 13 | bInputStartAdvancedPositioningRequest | ビット | VAR_GLOBAL | X2A | 高度な位置決め制御始動指令 |
| 14 | bInputMcodeOffRequest | ビット | VAR_GLOBAL | X2C | MコードOFF指令 |
| 15 | bInputSetJogSpeedRequest | ビット | VAR_GLOBAL | X2D | JOG運転速度設定指令 |
| 16 | bInputForwardJogStartRequest | ビット | VAR_GLOBAL | X2E | 正転JOG/インチング指令 |
| 17 | bInputReverseJogStartRequest | ビット | VAR_GLOBAL | X2F | 逆転JOG/インチング指令 |
| 18 | bInputMPG_EnableRequest | ビット | VAR_GLOBAL | X30 | 手動パルサ運転許可指令 |
| 19 | bInputMPG_DisableRequest | ビット | VAR_GLOBAL | X31 | 手動パルサ運転不許可指令 |
| 20 | bInputSpeedChangeRequest | ビット | VAR_GLOBAL | X32 | 速度変更指令 |
| 21 | bInputOverrideRequest | ビット | VAR_GLOBAL | X33 | オーバライド指令 |
| 22 | bInputChangeAccDecTimeRequest | ビット | VAR_GLOBAL | X34 | 加減速時間変更指令 |
| 23 | bInputChangeAccDecTimeDisable | ビット | VAR_GLOBAL | X35 | 加減速時間変更不許可指令 |
| 24 | bInputStepOperationRequest | ビット | VAR_GLOBAL | X37 | ステップ運転指令 |
| 25 | bInputSkipCommandRequest | ビット | VAR_GLOBAL | X38 | スキップ指令 |
| 26 | bInputStopContinuousOperationRequest | ビット | VAR_GLOBAL | X3A | 連続運転中断指令 |
| 27 | bInputRestartRequest | ビット | VAR_GLOBAL | X3B | 再始動指令 |
| 28 | bInputModuleInitializeParameterRequest | ビット | VAR_GLOBAL | X3C | パラメータ初期化指令 |
| 29 | bInputWriteFlashRequest | ビット | VAR_GLOBAL | X3D | フラッシュROM書込み指令 |
| 30 | bInputErrResetRequest | ビット | VAR_GLOBAL | X3E | エラーリセット指令 |
| 31 | bInputStopRequest | ビット | VAR_GLOBAL | X3F | 停止指令 |
| 32 | bInputPositionSpeedSwitchingRequest | ビット | VAR_GLOBAL | X40 | 位置・速度切換え運転指令 |
| 33 | bInputPositionSpeedSwitchingEnableRequest | ビット | VAR_GLOBAL | X41 | 位置・速度切換え許可指令 |
| 34 | bInputPositionSpeedSwitchingDisableRequest | ビット | VAR_GLOBAL | X42 | 位置・速度切換え禁止指令 |
| 35 | bInputChangePositionSpeedSwitchingSpeedRequest | ビット | VAR_GLOBAL | X43 | 速度変更指令 |
| 36 | bInputInchingMovementAmountSettingRequest | ビット | VAR_GLOBAL | X44 | インチング移動量設定指令 |
| 37 | bInputTargetPositionChangeRequest | ビット | VAR_GLOBAL | X45 | 目標位置変更指令 |
| 38 | bInputSpeedPositionSwitchingSettingRequest | ビット | VAR_GLOBAL | X4D | 速・位切換用設定指令 |
| 39 | bInputStartPositioningRequest | ビット | VAR_GLOBAL | X4E | 位置決め始動指令(Y始動) |
| 40 | bReady | ビット | VAR_GLOBAL | X100 | RD77MS準備完了 |
| 41 | bSynchronizationFlag | ビット | VAR_GLOBAL | X101 | 同期用フラグ |
| 42 | bnBusy | ビット(0..15) | VAR_GLOBAL | X110 | BUSY信号 |
| 43 | bPLCReady | ビット | VAR_GLOBAL | Y100 | シーケンサレディ信号 |
| 44 | bAllAxisServoOn | ビット | VAR_GLOBAL | Y101 | 全軸サーボON信号 |
| 45 | bnPositioningStart | ビット(0..15) | VAR_GLOBAL | Y110 | 位置決め始動信号 |
| 46 | uStatus | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D0 | ステータス |
| 47 | wSpeed | ワード[符号付き](0..1) | VAR_GLOBAL | D1 | 速度 |
| 48 | wMovementAmount | ワード[符号付き](0..1) | VAR_GLOBAL | D3 | 移動量 |
| 49 | wSetJogSpeed | ワード[符号付き](0..2) | VAR_GLOBAL | D5 | インチング移動量，JOG運転速度 |
| 50 | wMPG | ワード[符号付き](0..2) | VAR_GLOBAL | D8 | 手動パルサ |
| 51 | wSpeedChangeSetting | ワード[符号付き](0..2) | VAR_GLOBAL | D11 | 移動変更値，速度変更要求 |
| 52 | uOverrideValue | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D14 | オーバライド値 |
| 53 | wACCDecTimeChange | ワード[符号付き](0..4) | VAR_GLOBAL | D15 | 速度変更時の加減速時間 |
| 54 | wStep | ワード[符号付き](0..1) | VAR_GLOBAL | D20 | ステップモード，ステップ有効フラグ |
| 55 | wTarget | ワード[符号付き](0..4) | VAR_GLOBAL | D23 | 目標 |
| 56 | uPositioningStartNo | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D32 | 始動番号 |
| 57 | wBasicParam | ワード[符号付き](0..7) | VAR_GLOBAL | D50 | 基本パラメータ |
| 58 | wPositioningData | ワード[符号付き](0..11) | VAR_GLOBAL | D58 | 位置決めパラメータ |
| 59 | wBlockData | ワード[符号付き](0..4) | VAR_GLOBAL | D70 | ブロック始動データ(形態，始動データNo.) |
| 60 | wBlockInstData | ワード[符号付き](0..4) | VAR_GLOBAL | D75 | ブロック始動データ(特殊始動命令) |
| 61 | uErrorCode | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D80 | エラーコード |
| 62 | wAxisOperationStatus | ワード[符号付き] | VAR_GLOBAL | D81 | 軸動作状態 |
| 63 | uOPR_RequestFlagOffRequestSetting | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D82 | 原点復帰要求フラグOFF設定値 |
| 64 | uExternalCommandValidSetting | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D85 | 外部指令有効設定値 |
| 65 | uSpeedPositionSwitchingEnableFlagSetting | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D86 | 速度・位置切換え許可設定値 |
| 66 | uPositionSpeedSwitchingEnableFlagSetting | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D87 | 位置・速度切換え許可設定値 |
| 67 | uMcodeOnSignalTurnsOffRequestSetting | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D90 | MコードOFF要求設定値 |
| 68 | uSkipCommandSetting | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D91 | スキップ指令設定値 |
| 69 | uRestartSetting | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D92 | 再始動指令設定値 |
| 70 | uInitializeParameterSetting | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D93 | パラメータ初期化設定値 |
| 71 | uWriteFlashSetting | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D94 | フラッシュROM書込み設定値 |
| 72 | uStopContinuousOperationRequestSetting | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D95 | 連続運転中断要求設定値 |
| 73 | uErrorResetRequestSetting | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D96 | エラーリセット要求設定値 |
| 74 | uUnit_D | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D150 | 詳細パラメータ1:単位設定 |
| 75 | wSoftwareStrokeLimitValue | ワード[符号付き](0..3) | VAR_GLOBAL | D151 | 詳細パラメータ1:ソフトウェアリミット上下限値 |
| 76 | uCommandPositionValue_SpeedControl | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D155 | 詳細パラメータ1:速度制御時の送り現在値 |
| 77 | uSpeedPositionFunctionSelection | ワード[符号なし]/ビット列[16ビット] | VAR_GLOBAL | D156 | 詳細パラメータ1:速度・位置機能選択 |
| 78 | wOPRBasicParam | ワード[符号付き](0..8) | VAR_GLOBAL | D200 | 軸1:原点復帰 |
| 79 | bAxisStop_Axis1 | ビット | VAR_GLOBAL | D210.0 | 軸1:軸停止 |
| 80 | bForwardRunJogStart_Axis1 | ビット | VAR_GLOBAL | D211.0 | 軸1:正転JOG始動 |
| 81 | bReverseRunJogStart_Axis1 | ビット | VAR_GLOBAL | D212.0 | 軸1:逆転JOG始動 |
| 82 | bExecutionProhibitionFlag_Axis1 | ビット | VAR_GLOBAL | D213.0 | 軸1:実行禁止フラグ |
| 83 | bStnAxCtrl2_Axis1 | ビット(0..1) | VAR_GLOBAL | D214.0 | 軸1:軸制御データ2変更完了デバイス |
| 84 | bOPR_RequestFlagOffRequest | ビット | VAR_GLOBAL | M0 | 原点復帰要求OFF指令 |
| 85 | bOPR_RequestFlagOffRequestPulse | ビット | VAR_GLOBAL | M1 | 原点復帰要求OFF指令パルス |
| 86 | bOPR_RequestFlagOffRequestMemmory | ビット | VAR_GLOBAL | M2 | 原点復帰要求OFF指令記憶 |
| 87 | bFastOPR_Request | ビット | VAR_GLOBAL | M3 | 高速原点復帰指令 |
| 88 | bFastOPR_RequestMemmory | ビット | VAR_GLOBAL | M4 | 高速原点復帰指令記憶 |
| 89 | bPositioningStartRequestPulse | ビット | VAR_GLOBAL | M5 | 位置決め始動指令パルス |
| 90 | bPositioningStartRequestMemmory | ビット | VAR_GLOBAL | M6 | 位置決め始動指令記憶 |
| 91 | bJogInchingOperationFlag | ビット | VAR_GLOBAL | M7 | JOG/インチング運転中フラグ |
| 92 | bMPG_EnableFlagRequest | ビット | VAR_GLOBAL | M8 | 手動パルサ運転許可指令 |
| 93 | bMPG_OperationFlag | ビット | VAR_GLOBAL | M9 | 手動パルサ運転中フラグ |
| 94 | bMPG_DisableRequest | ビット | VAR_GLOBAL | M10 | 手動パルサ運転不許可指令 |
| 95 | bSpeedChangeRequestPulse | ビット | VAR_GLOBAL | M11 | 速度変更指令パルス |
| 96 | bSpeedChangeRequestMemory | ビット | VAR_GLOBAL | M12 | 速度変更指令記憶 |
| 97 | bOverrideRequest | ビット | VAR_GLOBAL | M13 | オーバライド指令 |
| 98 | bChangeAccDecTimeSettingRequest | ビット | VAR_GLOBAL | M14 | 加減速時間変更指令 |
| 99 | bStepOperationRequestPulse | ビット | VAR_GLOBAL | M16 | ステップ運転指令パルス |
| 100 | bSkipCommandRequestPulse | ビット | VAR_GLOBAL | M17 | ステップ指令パルス |
| 101 | bSkipCommandRequestMemory | ビット | VAR_GLOBAL | M18 | ステップ指令記憶 |
| 102 | bStopContinuousOperationRequest | ビット | VAR_GLOBAL | M21 | 連続運転中断指令 |
| 103 | bRestartRequest | ビット | VAR_GLOBAL | M22 | 再始動指令 |
| 104 | bRestartRequestMemory | ビット | VAR_GLOBAL | M23 | 再始動指令記憶 |
| 105 | bInitializeParameterRequestPulse | ビット | VAR_GLOBAL | M24 | パラメータ初期化指令パルス |
| 106 | bInitializeParameterRequestMemory | ビット | VAR_GLOBAL | M25 | パラメータ初期化指令記憶 |
| 107 | bWriteFlashRequestPulse | ビット | VAR_GLOBAL | M26 | フラッシュROM書込み指令パルス |
| 108 | bWriteFlashRequestMemory | ビット | VAR_GLOBAL | M27 | フラッシュROM書込み指令記憶 |
| 109 | bErrorReset | ビット | VAR_GLOBAL | M28 | エラーリセット |
| 110 | bStopRequestPulse | ビット | VAR_GLOBAL | M29 | 停止指令パルス |
| 111 | bTargetPositionChangeRequestPulse | ビット | VAR_GLOBAL | M30 | 目標位置変更指令パルス |
| 112 | bTargetPositionChangeRequestMemory | ビット | VAR_GLOBAL | M31 | 目標位置変更指令記憶 |
| 113 | bBasicParameterSettingCompleteFlag | ビット | VAR_GLOBAL | M50 | 基本パラメータ1設定完了デバイス |
| 114 | bOPR_BasicParameterSettingCompleteFlag | ビット | VAR_GLOBAL | M51 | 原点復帰基本パラメータ設定完了デバイス |
| 115 | bSpeedPositionSwitchingParameterSettingCompleteFlag | ビット | VAR_GLOBAL | M52 | 速・位切換えパラメータ設定完了デバイス |
| 116 | bOPR_RequestFlagOffRequestConfirmationPulse | ビット | VAR_GLOBAL | M60 | 原点復帰OFF指令確認パルス |
| 117 | bRestartRequestConfirmation | ビット | VAR_GLOBAL | M61 | 再始動指令確認パルス |
| 118 | bSpeedChangeRequestConfirmation | ビット | VAR_GLOBAL | M62 | 速度変更指令確認 |
| 119 | bTargetPositionChangeRequestConfirmation | ビット | VAR_GLOBAL | M63 | 目標位置変更指令確認 |
| 120 | bSkipCommandRequestConfirmation | ビット | VAR_GLOBAL | M64 | スキップ指令確認 |
| 121 | bAxisOperationStatusAcquisitionRequest | ビット | VAR_GLOBAL | M65 | 軸動作状態取得指令 |
| 122 | bInitializeParameterRequestConfirmation | ビット | VAR_GLOBAL | M66 | パラメータ初期化指令確認パルス |
| 123 | bWriteFlashRequestConfirmation | ビット | VAR_GLOBAL | M67 | フラッシュROM書込み指令確認パルス |
| 124 | bAfter_RUN1_Scan_ON_Memory | ビット | VAR_GLOBAL | M99 | RUN後1スキャンON記憶 |
| 125 | bBasicParametarSettingRequest | ビット | VAR_GLOBAL | M100 | 基本パラメータ1設定指令 |
| 126 | bOPR_BasicParameterSettingRequest | ビット | VAR_GLOBAL | M101 | 原点復帰基本パラメータ設定指令 |
| 127 | bSpeedPositionSwitchingSettingRequest | ビット | VAR_GLOBAL | M102 | 速・位切換用設定指令 |
| 128 | bPositioningDataSettingRequest | ビット | VAR_GLOBAL | M103 | 位置決めデータ設定指令 |
| 129 | bBlockStartDataSettingRequest | ビット | VAR_GLOBAL | M104 | ブロック始動データ設定指令 |
| 130 | bBlockStartData_SpecialStartCommandSettingRequest | ビット | VAR_GLOBAL | M105 | ブロック始動(特殊始動)設定指令 |
| 131 | bCommunicatingConditionSatisfactionFlag | ビット | VAR_GLOBAL | M120 | 交信条件の成立フラグ(局番1) |
| 132 | bBasicParameterSettingRet | ビット(0..1) | VAR_GLOBAL | M5000 | 基本パラメータ1完了デバイス |
| 133 | bOPR_BasicParameterSettingRet | ビット(0..1) | VAR_GLOBAL | M5010 | 原点復帰基本パラメータ完了デバイス |
| 134 | bSpeedPositionSwitchingSettingRet1 | ビット(0..1) | VAR_GLOBAL | M5020 | 単位設定完了デバイス |
| 135 | bSpeedPositionSwitchingSettingRet2 | ビット(0..1) | VAR_GLOBAL | M5022 | S/Wストロークリミット完了デバイス |
| 136 | bSpeedPositionSwitchingSettingRet3 | ビット(0..1) | VAR_GLOBAL | M5024 | 速度制御時の送り現在値完了デバイス |
| 137 | bSpeedPositionSwitchingSettingRet4 | ビット(0..1) | VAR_GLOBAL | M5026 | 速度・位置機能設定完了デバイス |
| 138 | bPositioningDataSettingRet | ビット(0..3) | VAR_GLOBAL | M5030 | 位置決めデータ完了デバイス |
| 139 | bBlockStartDataSettingRet1 | ビット(0..1) | VAR_GLOBAL | M5040 | ブロック始動データ完了デバイス |
| 140 | bBlockStartDataSettingRet2 | ビット(0..1) | VAR_GLOBAL | M5050 | ブロック始動(特殊始動)完了デバイス |
| 141 | bStatusRet | ビット(0..1) | VAR_GLOBAL | M5100 | ステータス読出し完了デバイス |
| 142 | bOPR_RequestFlagOffRet1 | ビット(0..1) | VAR_GLOBAL | M5110 | 原点復帰要求OFF完了デバイス |
| 143 | bOPR_RequestFlagOffRet2 | ビット(0..1) | VAR_GLOBAL | M5120 | ステータス読出し完了デバイス |
| 144 | bExternalCommandValidRet | ビット(0..1) | VAR_GLOBAL | M5130 | 外部指令有効完了デバイス |
| 145 | bSpeedPositionSwitchingEnableRet | ビット(0..1) | VAR_GLOBAL | M5140 | 速度・位置切換え許可完了デバイス |
| 146 | bChangeMovementAmountRet | ビット(0..1) | VAR_GLOBAL | M5150 | 移動量変更許可完了デバイス |
| 147 | bPositionSpeedSwitchingEnableRet | ビット(0..1) | VAR_GLOBAL | M5160 | 位置・速度切換え許可完了デバイス |
| 148 | bPVSpeedChangeRet | ビット(0..1) | VAR_GLOBAL | M5170 | 速度変更完了デバイス |
| 149 | bPositioningStartRet | ビット(0..1) | VAR_GLOBAL | M5180 | 位置決め始動完了デバイス |
| 150 | bMcodeOffRet | ビット(0..1) | VAR_GLOBAL | M5200 | Mコード要求完了デバイス |
| 151 | bJogSettingRet | ビット(0..1) | VAR_GLOBAL | M5210 | JOG運転速度設定完了デバイス |
| 152 | bInchingSettingRet | ビット(0..1) | VAR_GLOBAL | M5220 | インチング移動量設定完了デバイス |
| 153 | bMPG_SettingRet | ビット(0..1) | VAR_GLOBAL | M5230 | 手動パルサ入力倍率設定完了デバイス |
| 154 | bMPG_EnableRet | ビット(0..1) | VAR_GLOBAL | M5240 | 手動パルサ設定完了デバイス |
| 155 | bSpeedChangeSettingRet | ビット(0..1) | VAR_GLOBAL | M5250 | 速度変更完了デバイス |
| 156 | bOverrideSettingRet | ビット(0..1) | VAR_GLOBAL | M5260 | オーバライド完了デバイス |
| 157 | bChangeAccDecTimeSettingRet | ビット(0..1) | VAR_GLOBAL | M5270 | 加減速時間設定完了デバイス |
| 158 | bChangeAccDecTimeEnableRet | ビット(0..1) | VAR_GLOBAL | M5280 | 加減速時間変更完了デバイス |
| 159 | bStepOperationSettingRet | ビット(0..1) | VAR_GLOBAL | M5290 | ステップ運転設定完了デバイス |
| 160 | bSkipCommandSettingRet | ビット(0..1) | VAR_GLOBAL | M5300 | スキップ指令完了デバイス |
| 161 | bTargetPositionChangeRet | ビット(0..1) | VAR_GLOBAL | M5310 | 目標位置変更完了デバイス |
| 162 | bAxisOperationStatusRet | ビット(0..1) | VAR_GLOBAL | M5320 | 軸動作状態取得完了デバイス |
| 163 | bRestartRet | ビット(0..1) | VAR_GLOBAL | M5330 | 再始動指令完了デバイス |
| 164 | bInitializeParameterRet | ビット(0..1) | VAR_GLOBAL | M5340 | パラメータ初期化指令完了デバイス |
| 165 | bWriteFlashRet | ビット(0..1) | VAR_GLOBAL | M5350 | フラッシュROM書込み完了デバイス |
| 166 | bStopContinuousOperationRet | ビット(0..1) | VAR_GLOBAL | M5360 | 連続運転中断完了デバイス |
| 167 | bErrorCodeRet1 | ビット(0..1) | VAR_GLOBAL | M5370 | エラーコード取得完了デバイス |
| 168 | bErrorCodeRet2 | ビット(0..1) | VAR_GLOBAL | M5380 | エラーリセット完了デバイス |
| 169 | bErrorResetCompleteAbnormalFlag | ビット | VAR_GLOBAL | M5381 | エラーリセット異常完了デバイス |
| 170 | tdPLCReadyOff1 | タイマ | VAR_GLOBAL | T104 | シーケンサレディOFF確認 |
| 171 | tdPLCReadyOff2 | タイマ | VAR_GLOBAL | T105 | シーケンサレディOFF確認 |
| 172 | bMcodeOn_Axis1 | ビット | VAR_GLOBAL | W0.C | 軸1:MコードON信号 |
| 173 | bErrorDetection_Axis1 | ビット | VAR_GLOBAL | W0.D | 軸1:エラー検出信号 |
| 174 | bStartComplete_Axis1 | ビット | VAR_GLOBAL | W0.E | 軸1:始動完了信号 |
| 175 | bPositioningComplete_Axis1 | ビット | VAR_GLOBAL | W0.F | 軸1:位置決め完了信号 |

###### ■配列化したラベルの内容 (付4 / 印刷 p.799-801 / 原本 p.801-803)

グローバルラベル一覧に記載されたラベルで，配列化されたラベルの内容を示します。

注: 原本では「内容」列が2要素以上にまたがる結合セルになっている箇所(wSpeed[0]〜[1]、wSetJogSpeed[1]〜[2]、wMPG[0]〜[1] 等)を各行に展開した。

| ラベル名 | 割付けデバイス | 内容 |
|---|---|---|
| bnBusy[0] | X110 | 軸1: BUSY信号 |
| bnBusy[1] | X111 | 軸2: BUSY信号 |
| bnBusy[2] | X112 | 軸3: BUSY信号 |
| bnBusy[3] | X113 | 軸4: BUSY信号 |
| bnBusy[4] | X114 | 軸5: BUSY信号 |
| bnBusy[5] | X115 | 軸6: BUSY信号 |
| bnBusy[6] | X116 | 軸7: BUSY信号 |
| bnBusy[7] | X117 | 軸8: BUSY信号 |
| bnBusy[8] | X118 | 軸9: BUSY信号 |
| bnBusy[9] | X119 | 軸10: BUSY信号 |
| bnBusy[10] | X11A | 軸11: BUSY信号 |
| bnBusy[11] | X11B | 軸12: BUSY信号 |
| bnBusy[12] | X11C | 軸13: BUSY信号 |
| bnBusy[13] | X11D | 軸14: BUSY信号 |
| bnBusy[14] | X11E | 軸15: BUSY信号 |
| bnBusy[15] | X11F | 軸16: BUSY信号 |
| bnPositioningStart[0] | Y110 | 軸1: 位置決め始動信号 |
| bnPositioningStart[1] | Y111 | 軸2: 位置決め始動信号 |
| bnPositioningStart[2] | Y112 | 軸3: 位置決め始動信号 |
| bnPositioningStart[3] | Y113 | 軸4: 位置決め始動信号 |
| bnPositioningStart[4] | Y114 | 軸5: 位置決め始動信号 |
| bnPositioningStart[5] | Y115 | 軸6: 位置決め始動信号 |
| bnPositioningStart[6] | Y116 | 軸7: 位置決め始動信号 |
| bnPositioningStart[7] | Y117 | 軸8: 位置決め始動信号 |
| bnPositioningStart[8] | Y118 | 軸9: 位置決め始動信号 |
| bnPositioningStart[9] | Y119 | 軸10: 位置決め始動信号 |
| bnPositioningStart[10] | Y11A | 軸11: 位置決め始動信号 |
| bnPositioningStart[11] | Y11B | 軸12: 位置決め始動信号 |
| bnPositioningStart[12] | Y11C | 軸13: 位置決め始動信号 |
| bnPositioningStart[13] | Y11D | 軸14: 位置決め始動信号 |
| bnPositioningStart[14] | Y11E | 軸15: 位置決め始動信号 |
| bnPositioningStart[15] | Y11F | 軸16: 位置決め始動信号 |
| wSpeed[0] | D1 | 速度 |
| wSpeed[1] | D2 | 速度 |
| wMovementAmount[0] | D3 | 移動量 |
| wMovementAmount[1] | D4 | 移動量 |
| wSetJogSpeed[0] | D5 | インチング移動量 |
| wSetJogSpeed[1] | D6 | JOG運転速度 |
| wSetJogSpeed[2] | D7 | JOG運転速度 |
| wMPG[0] | D8 | 手動パルサ1パルス入力倍率 |
| wMPG[1] | D9 | 手動パルサ1パルス入力倍率 |
| wMPG[2] | D10 | 手動パルサ運転許可 |
| wSpeedChangeSetting[0] | D11 | 速度変更値 |
| wSpeedChangeSetting[1] | D12 | 速度変更値 |
| wSpeedChangeSetting[2] | D13 | 速度変更要求 |
| wACCDecTimeChange[0] | D15 | 加速時間変更値 |
| wACCDecTimeChange[1] | D16 | 加速時間変更値 |
| wACCDecTimeChange[2] | D17 | 減速時間変更値 |
| wACCDecTimeChange[3] | D18 | 減速時間変更値 |
| wACCDecTimeChange[4] | D19 | 速度変更時の加減速時間変更許可／不許可選択 |
| wStep[0] | D20 | ステップモード |
| wStep[1] | D21 | ステップ有効フラグ |
| wTarget[0] | D23 | 目標位置変更(アドレス) |
| wTarget[1] | D24 | 目標位置変更(アドレス) |
| wTarget[2] | D25 | 目標位置変更(速度) |
| wTarget[3] | D26 | 目標位置変更(速度) |
| wTarget[4] | D27 | 目標位置変更要求フラグ |
| wBasicParam[0] | D50 | 基本パラメータ: 単位設定 |
| wBasicParam[1] | D51 | 基本パラメータ: 単位倍率 |
| wBasicParam[2] | D52 | 基本パラメータ: 1回転あたりのパルス数 |
| wBasicParam[3] | D53 | 基本パラメータ: 1回転あたりのパルス数 |
| wBasicParam[4] | D54 | 基本パラメータ: 1回転あたりの移動量 |
| wBasicParam[5] | D55 | 基本パラメータ: 1回転あたりの移動量 |
| wBasicParam[6] | D56 | 基本パラメータ: 始動時バイアス速度 |
| wBasicParam[7] | D57 | 基本パラメータ: 始動時バイアス速度 |
| wPositioningData[0] | D58 | 運転パターン/制御方式/加速時間№/減速時間№ |
| wPositioningData[1] | D59 | Mコード/条件データ/LOOP～LEND繰り返し回数 |
| wPositioningData[2] | D60 | ドウェルタイム/JUMP先位置決めデータNo. |
| wPositioningData[3] | D61 | 位置決めオプション |
| wPositioningData[4] | D62 | 指令速度 |
| wPositioningData[5] | D63 | 指令速度 |
| wPositioningData[6] | D64 | 位置決めアドレス/移動量 |
| wPositioningData[7] | D65 | 位置決めアドレス/移動量 |
| wPositioningData[8] | D66 | 円弧アドレス |
| wPositioningData[9] | D67 | 円弧アドレス |
| wPositioningData[10] | D68 | 補間対称軸 |
| wPositioningData[11] | D69 | 補間対称軸 |
| wBlockData[0] | D70 | ブロック始動データ(形態，始動データNo.)　1 |
| wBlockData[1] | D71 | ブロック始動データ(形態，始動データNo.)　2 |
| wBlockData[2] | D72 | ブロック始動データ(形態，始動データNo.)　3 |
| wBlockData[3] | D73 | ブロック始動データ(形態，始動データNo.)　4 |
| wBlockData[4] | D74 | ブロック始動データ(形態，始動データNo.)　5 |
| wBlockInstData[0] | D75 | ブロック始動データ(特殊始動命令)　1 |
| wBlockInstData[1] | D76 | ブロック始動データ(特殊始動命令)　2 |
| wBlockInstData[2] | D77 | ブロック始動データ(特殊始動命令)　3 |
| wBlockInstData[3] | D78 | ブロック始動データ(特殊始動命令)　4 |
| wBlockInstData[4] | D79 | ブロック始動データ(特殊始動命令)　5 |
| wSoftwareStrokeLimitValue[0] | D151 | ソフトウェアストロークリミット上限値 |
| wSoftwareStrokeLimitValue[1] | D152 | ソフトウェアストロークリミット上限値 |
| wSoftwareStrokeLimitValue[2] | D153 | ソフトウェアストロークリミット下限値 |
| wSoftwareStrokeLimitValue[3] | D154 | ソフトウェアストロークリミット下限値 |
| wOPRBasicParam[0] | D200 | 軸1: 原点復帰方式 |
| wOPRBasicParam[1] | D201 | 軸1: 原点復帰方向 |
| wOPRBasicParam[2] | D202 | 軸1: 原点アドレス |
| wOPRBasicParam[3] | D203 | 軸1: 原点アドレス |
| wOPRBasicParam[4] | D204 | 軸1: 原点復帰速度 |
| wOPRBasicParam[5] | D205 | 軸1: 原点復帰速度 |
| wOPRBasicParam[6] | D206 | 軸1: クリープ速度 |
| wOPRBasicParam[7] | D207 | 軸1: クリープ速度 |
| wOPRBasicParam[8] | D208 | 軸1: 原点復帰リトライ |

##### マスタ局動作状態確認 (付4 / 印刷 p.802 / 原本 p.804)

【図】ラダー図(図から書き起こし)。
- ステップ(0): RUN後1スキャンON(SM402)で bAfter_RUN1_Scan_ON_Memory(M99)をセットする。
- ステップ(3): 自局データリンク異常状態(GF11_1.bSts_DataLinkError)のb接点と各局データリンク状態(局番1)(GF11_1.bnSts_DataLinkError_Station[1])のb接点の直列で、マスタコントロール MC N0 bCommunicatingConditionSatisfactionFlag(M120)を実行する。同じ接続点から分岐した bAfter_RUN1_Scan_ON_Memory(M99)のa接点で、bBasicParametarSettingRequest(M100)をセットし、bAfter_RUN1_Scan_ON_Memory(M99)をリセットする。
- 回路の下に母線の表示「N0 ⊥ bCommunicatingConditionSatisfactionFlag M120」があり、以降の回路がマスタコントロール N0 の範囲であることを示す。本ファイル範囲内(印刷 p.806 まで)に MCR は表示されていない。

```
(0)  LD     RCPU.stSM.bAfter_RUN1_Scan_ON                                  SM402
     SET    bAfter_RUN1_Scan_ON_Memory                                     M99

(3)  LDI    GF11_1.bSts_DataLinkError
     ANI    GF11_1.bnSts_DataLinkError_Station[1]
     MPS
     MC     N0        bCommunicatingConditionSatisfactionFlag              M120
     MPP
     AND    bAfter_RUN1_Scan_ON_Memory                                     M99
     SET    bBasicParametarSettingRequest                                  M100
     RST    bAfter_RUN1_Scan_ON_Memory                                     M99

     (母線表示: N0 ⊥ bCommunicatingConditionSatisfactionFlag M120 ← 以降の回路はマスタコントロール N0 の範囲)
```

##### パラメータ設定プログラム (付4 / 印刷 p.802-804 / 原本 p.804-806)

エンジニアリングツールの"ユニットパラメータ"にてパラメータを設定する場合，本プログラムは不要です。

###### ■基本パラメータ1(軸1)の設定 (付4 / 印刷 p.802 / 原本 p.804)

【図】ラダー図(図から書き起こし)。起動接点は bBasicParametarSettingRequest(M100)のa接点。MOVP/DMOVP で wBasicParam[0]〜[7](D50〜D57)に値を格納し、JP.REMTO を実行する。同じ起動条件から分岐した完了デバイス bBasicParameterSettingRet[0](M5000)のa接点と bBasicParameterSettingRet[1](M5001)のb接点の直列で、bBasicParameterSettingCompleteFlag(M50)・bOPR_BasicParameterSettingRequest(M101)をセットし、bBasicParametarSettingRequest(M100)をリセットする。

```
(12) LD     bBasicParametarSettingRequest                                  M100
     MOVP   K0        wBasicParam[0]                                       D50
     MOVP   K1        wBasicParam[1]                                       D51
     DMOVP  K20000    wBasicParam[2]                                       D52
     DMOVP  K15000    wBasicParam[4]                                       D54
     DMOVP  K1000     wBasicParam[6]                                       D56
     JP.REMTO  J1  K1  K1  H0  K0  wBasicParam(D50)  K8  bBasicParameterSettingRet(M5000)
     AND    bBasicParameterSettingRet[0]                                   M5000
     ANI    bBasicParameterSettingRet[1]                                   M5001
     SET    bBasicParameterSettingCompleteFlag                             M50
     SET    bOPR_BasicParameterSettingRequest                              M101
     RST    bBasicParametarSettingRequest                                  M100
```

JP.REMTO のオペランド(図の表示順): J1 / K1 / K1 / H0 / K0 / wBasicParam(D50) / K8 / bBasicParameterSettingRet(M5000)

###### ■原点復帰基本パラメータ(軸1)の設定 (付4 / 印刷 p.803 / 原本 p.805)

【図】ラダー図(図から書き起こし)。起動接点は bOPR_BasicParameterSettingRequest(M101)のa接点。wOPRBasicParam[0]〜[8](D200〜D208)に値を格納し、JP.REMTO を実行する。完了デバイス bOPR_BasicParameterSettingRet[0](M5010)のa接点と bOPR_BasicParameterSettingRet[1](M5011)のb接点の直列で、bOPR_BasicParameterSettingCompleteFlag(M51)・bSpeedPositionSwitchingSettingRequest(M102)をセットし、bOPR_BasicParameterSettingRequest(M101)をリセットする。

```
(51) LD     bOPR_BasicParameterSettingRequest                              M101
     MOVP   K0        wOPRBasicParam[0]                                    D200
     MOVP   K0        wOPRBasicParam[1]                                    D201
     DMOVP  K0        wOPRBasicParam[2]                                    D202
     DMOVP  K5000     wOPRBasicParam[4]                                    D204
     DMOVP  K1500     wOPRBasicParam[6]                                    D206
     MOVP   K1        wOPRBasicParam[8]                                    D208
     JP.REMTO  J1  K1  K1  H0  K70  wOPRBasicParam(D200)  K9  bOPR_BasicParameterSettingRet(M5010)
     AND    bOPR_BasicParameterSettingRet[0]                               M5010
     ANI    bOPR_BasicParameterSettingRet[1]                               M5011
     SET    bOPR_BasicParameterSettingCompleteFlag                         M51
     SET    bSpeedPositionSwitchingSettingRequest                          M102
     RST    bOPR_BasicParameterSettingRequest                              M101
```

JP.REMTO のオペランド(図の表示順): J1 / K1 / K1 / H0 / K70 / wOPRBasicParam(D200) / K9 / bOPR_BasicParameterSettingRet(M5010)

###### ■速度・位置切換え制御(ABSモード)用パラメータ設定プログラム(軸1の場合) (付4 / 印刷 p.804 / 原本 p.806)

速度・位置切換え制御(ABSモード)を実行しない場合は不要です。

【図】ラダー図(図から書き起こし)。
- ステップ(93): bSpeedPositionSwitchingSettingRequest(M102)のa接点と bInputSpeedPositionSwitchingSettingRequest(X4D)のa接点の直列で、uUnit_D(D150)、wSoftwareStrokeLimitValue[0](D151)、wSoftwareStrokeLimitValue[2](D153)、uCommandPositionValue_SpeedControl(D155)、uSpeedPositionFunctionSelection(D156)に値を格納し、1つ目の JP.REMTO(K0, uUnit_D, K1)を実行する。同じ接続点から4本の分岐があり、それぞれ前段の完了デバイス[0]のa接点と[1]のb接点の直列を条件に、次の JP.REMTO を順に実行する(Ret1→K18、Ret2→K30、Ret3→K34)。最後の分岐(bSpeedPositionSwitchingSettingRet4[0] M5026 a接点・[1] M5027 b接点)で bSpeedPositionSwitchingParameterSettingCompleteFlag(M52)・bPositioningDataSettingRequest(M103)をセットし、bSpeedPositionSwitchingSettingRequest(M102)をリセットする。
- ステップ(184): bSpeedPositionSwitchingSettingRequest(M102)のa接点と bInputSpeedPositionSwitchingSettingRequest(X4D)のb接点の直列で、M52・M103をセットし、M102をリセットする(X4D がOFFのときは速度・位置切換え用の設定を行わずに次へ進む)。

```
(93) LD     bSpeedPositionSwitchingSettingRequest                          M102
     AND    bInputSpeedPositionSwitchingSettingRequest                     X4D
     MOVP   K2        uUnit_D                                              D150
     DMOVP  K0        wSoftwareStrokeLimitValue[0]                         D151
     DMOVP  K0        wSoftwareStrokeLimitValue[2]                         D153
     MOVP   K1        uCommandPositionValue_SpeedControl                   D155
     MOVP   K2        uSpeedPositionFunctionSelection                      D156
     JP.REMTO  J1  K1  K1  H0  K0   uUnit_D(D150)  K1  bSpeedPositionSwitchingSettingRet1(M5020)
     MPS
     AND    bSpeedPositionSwitchingSettingRet1[0]                          M5020
     ANI    bSpeedPositionSwitchingSettingRet1[1]                          M5021
     JP.REMTO  J1  K1  K1  H0  K18  wSoftwareStrokeLimitValue[0](D151)  K4  bSpeedPositionSwitchingSettingRet2(M5022)
     MRD
     AND    bSpeedPositionSwitchingSettingRet2[0]                          M5022
     ANI    bSpeedPositionSwitchingSettingRet2[1]                          M5023
     JP.REMTO  J1  K1  K1  H0  K30  uCommandPositionValue_SpeedControl(D155)  K1  bSpeedPositionSwitchingSettingRet3(M5024)
     MRD
     AND    bSpeedPositionSwitchingSettingRet3[0]                          M5024
     ANI    bSpeedPositionSwitchingSettingRet3[1]                          M5025
     JP.REMTO  J1  K1  K1  H0  K34  uSpeedPositionFunctionSelection(D156)  K1  bSpeedPositionSwitchingSettingRet4(M5026)
     MPP
     AND    bSpeedPositionSwitchingSettingRet4[0]                          M5026
     ANI    bSpeedPositionSwitchingSettingRet4[1]                          M5027
     SET    bSpeedPositionSwitchingParameterSettingCompleteFlag            M52
     SET    bPositioningDataSettingRequest                                 M103
     RST    bSpeedPositionSwitchingSettingRequest                          M102

(184) LD    bSpeedPositionSwitchingSettingRequest                          M102
     ANI    bInputSpeedPositionSwitchingSettingRequest                     X4D
     SET    bSpeedPositionSwitchingParameterSettingCompleteFlag            M52
     SET    bPositioningDataSettingRequest                                 M103
     RST    bSpeedPositionSwitchingSettingRequest                          M102
```

JP.REMTO のオペランド(図の表示順):

| 順 | 起動条件(/はb接点) | 第1オペランド | 第2オペランド | 第3オペランド | 第4オペランド | 第5オペランド | 第6オペランド | 第7オペランド | 第8オペランド |
|---|---|---|---|---|---|---|---|---|---|
| 1 | M102・X4D | J1 | K1 | K1 | H0 | K0 | uUnit_D(D150) | K1 | bSpeedPositionSwitchingSettingRet1(M5020) |
| 2 | M5020・/M5021 | J1 | K1 | K1 | H0 | K18 | wSoftwareStrokeLimitValue[0](D151) | K4 | bSpeedPositionSwitchingSettingRet2(M5022) |
| 3 | M5022・/M5023 | J1 | K1 | K1 | H0 | K30 | uCommandPositionValue_SpeedControl(D155) | K1 | bSpeedPositionSwitchingSettingRet3(M5024) |
| 4 | M5024・/M5025 | J1 | K1 | K1 | H0 | K34 | uSpeedPositionFunctionSelection(D156) | K1 | bSpeedPositionSwitchingSettingRet4(M5026) |

##### 位置決めデータ設定プログラム (付4 / 印刷 p.805 / 原本 p.807)

###### ■位置決めデータNo.1(軸1)の場合 (付4 / 印刷 p.805 / 原本 p.807)

エンジニアリングツールの"ユニット拡張パラメータ"にて位置決めデータを設定する場合，本プログラムは不要です。

【図】ラダー図(図から書き起こし)。起動条件は bPositioningDataSettingRequest(M103)のa接点と bSynchronizationFlag(X101)のa接点の直列。wPositioningData[0]〜[11](D58〜D69)に値を格納し、JP.REMTO(K6000, 10ワード)を実行する。同じ接続点からの分岐1: bPositioningDataSettingRet[0](M5030)のa接点と bPositioningDataSettingRet[1](M5031)のb接点の直列で JP.REMTOD(K71000, 2ワード)を実行する。分岐2: bPositioningDataSettingRet[2](M5032)のa接点と bPositioningDataSettingRet[3](M5033)のb接点の直列で bBlockStartDataSettingRequest(M104)をセットし、bPositioningDataSettingRequest(M103)をリセットする。

```
(189) LD    bPositioningDataSettingRequest                                 M103
     AND    bSynchronizationFlag                                           X101
     MOVP   H190      wPositioningData[0]                                  D58
     MOVP   K9843     wPositioningData[1]                                  D59
     MOVP   K300      wPositioningData[2]                                  D60
     MOVP   K0        wPositioningData[3]                                  D61
     DMOVP  K18000    wPositioningData[4]                                  D62
     DMOVP  K4126     wPositioningData[6]                                  D64
     DMOVP  K0        wPositioningData[8]                                  D66
     DMOVP  K0        wPositioningData[10]                                 D68
     JP.REMTO   J1  K1  K1  H0  K6000   wPositioningData[0](D58)   K10  bPositioningDataSettingRet[0](M5030)
     MPS
     AND    bPositioningDataSettingRet[0]                                  M5030
     ANI    bPositioningDataSettingRet[1]                                  M5031
     JP.REMTOD  J1  K1  K1  H0  K71000  wPositioningData[10](D68)  K2   bPositioningDataSettingRet[2](M5032)
     MPP
     AND    bPositioningDataSettingRet[2]                                  M5032
     ANI    bPositioningDataSettingRet[3]                                  M5033
     SET    bBlockStartDataSettingRequest                                  M104
     RST    bPositioningDataSettingRequest                                 M103
```

JP.REMTO / JP.REMTOD のオペランド(図の表示順):

| 命令 | 起動条件(/はb接点) | 第1オペランド | 第2オペランド | 第3オペランド | 第4オペランド | 第5オペランド | 第6オペランド | 第7オペランド | 第8オペランド |
|---|---|---|---|---|---|---|---|---|---|
| JP.REMTO | M103・X101 | J1 | K1 | K1 | H0 | K6000 | wPositioningData[0](D58) | K10 | bPositioningDataSettingRet[0](M5030) |
| JP.REMTOD | M5030・/M5031 | J1 | K1 | K1 | H0 | K71000 | wPositioningData[10](D68) | K2 | bPositioningDataSettingRet[2](M5032) |

##### ブロック始動データ設定プログラム (付4 / 印刷 p.806 / 原本 p.808)

###### ■始動ブロック0のブロック始動データ(軸1)1～5ポイント目までの設定の場合 (付4 / 印刷 p.806 / 原本 p.808)

エンジニアリングツールの"ユニット拡張パラメータ"にてブロック始動データを設定する場合，本プログラムは不要です。

【図】ラダー図(図から書き起こし)。起動条件は bBlockStartDataSettingRequest(M104)のa接点と bSynchronizationFlag(X101)のa接点の直列。wBlockData[0]〜[4](D70〜D74)に H8001 / H8002 / H8005 / H800A / H0F を格納し、JP.REMTO(K22000, 5ワード)を実行する。完了デバイス bBlockStartDataSettingRet1[0](M5040)のa接点と bBlockStartDataSettingRet1[1](M5041)のb接点の直列で bBlockStartData_SpecialStartCommandSettingRequest(M105)をセットし、bBlockStartDataSettingRequest(M104)をリセットする。

```
(257) LD    bBlockStartDataSettingRequest                                  M104
     AND    bSynchronizationFlag                                           X101
     MOVP   H8001     wBlockData[0]                                        D70
     MOVP   H8002     wBlockData[1]                                        D71
     MOVP   H8005     wBlockData[2]                                        D72
     MOVP   H800A     wBlockData[3]                                        D73
     MOVP   H0F       wBlockData[4]                                        D74
     JP.REMTO  J1  K1  K1  H0  K22000  wBlockData[0](D70)  K5  bBlockStartDataSettingRet1(M5040)
     AND    bBlockStartDataSettingRet1[0]                                  M5040
     ANI    bBlockStartDataSettingRet1[1]                                  M5041
     SET    bBlockStartData_SpecialStartCommandSettingRequest              M105
     RST    bBlockStartDataSettingRequest                                  M104
```

JP.REMTO のオペランド(図の表示順): J1 / K1 / K1 / H0 / K22000 / wBlockData[0](D70) / K5 / bBlockStartDataSettingRet1(M5040)

##### 特殊始動命令を通常始動に設定 (付4 / 印刷 p.806 / 原本 p.808)

エンジニアリングツールの"ユニット拡張パラメータ"にてブロック始動データを設定する場合，本プログラムは不要です。

【図】ラダー図(図から書き起こし)。起動条件は bBlockStartData_SpecialStartCommandSettingRequest(M105)のa接点と bSynchronizationFlag(X101)のa接点の直列。wBlockInstData[0]〜[4](D75〜D79)に H0 を格納し、JP.REMTO(K22050, 5ワード)を実行する。完了デバイス bBlockStartDataSettingRet2[0](M5050)のa接点と bBlockStartDataSettingRet2[1](M5051)のb接点の直列で bBlockStartData_SpecialStartCommandSettingRequest(M105)をリセットする。

```
(293) LD    bBlockStartData_SpecialStartCommandSettingRequest              M105
     AND    bSynchronizationFlag                                           X101
     MOVP   H0        wBlockInstData[0]                                    D75
     MOVP   H0        wBlockInstData[1]                                    D76
     MOVP   H0        wBlockInstData[2]                                    D77
     MOVP   H0        wBlockInstData[3]                                    D78
     MOVP   H0        wBlockInstData[4]                                    D79
     JP.REMTO  J1  K1  K1  H0  K22050  wBlockInstData[0](D75)  K5  bBlockStartDataSettingRet2(M5050)
     AND    bBlockStartDataSettingRet2[0]                                  M5050
     ANI    bBlockStartDataSettingRet2[1]                                  M5051
     RST    bBlockStartData_SpecialStartCommandSettingRequest              M105
```

JP.REMTO のオペランド(図の表示順): J1 / K1 / K1 / H0 / K22050 / wBlockInstData[0](D75) / K5 / bBlockStartDataSettingRet2(M5050)

(プログラム例の続き「原点復帰要求OFFプログラム」以降は印刷 p.807 / 原本 p.809 から。次ファイルの範囲)

## 転記時の要確認一覧 (付4 / 原本 p.793-808)

| No. | 箇所 (印刷p./原本p.) | 内容 |
|---|---|---|
| 1 | グローバルラベル一覧 No.51 wSpeedChangeSetting (印刷 p.798 / 原本 p.800) | コメントが「移動変更値，速度変更要求」。配列化したラベルの内容(印刷 p.800)では wSpeedChangeSetting[0]〜[1] は「速度変更値」。原文どおり転記した。 |
| 2 | グローバルラベル一覧 No.86/88/90 (印刷 p.798 / 原本 p.800) | ラベル名が「…RequestMemmory」(m が2つ)。No.96 等は「…RequestMemory」。原本のラベル名どおり転記した(プログラムで参照する場合は原本の綴りで定義すること)。 |
| 3 | グローバルラベル一覧 No.125 bBasicParametarSettingRequest (印刷 p.798 / 原本 p.800) | 「Parametar」の綴り。ラダー図(印刷 p.802)でも同じ綴りで使用。原文どおり。一方 No.113 等は「Parameter」。 |
| 4 | グローバルラベル一覧 No.100 / No.101 (印刷 p.798 / 原本 p.800) | bSkipCommandRequestPulse / bSkipCommandRequestMemory のコメントが「ステップ指令パルス」「ステップ指令記憶」(スキップではなくステップ)。原文どおり。 |
| 5 | グローバルラベル一覧 No.117 / No.143 (印刷 p.798 / 原本 p.800) | No.117 bRestartRequestConfirmation のコメント「再始動指令確認パルス」、No.143 bOPR_RequestFlagOffRet2 のコメント「ステータス読出し完了デバイス」(No.141 と同じ)。原文どおり。 |
| 6 | 配列化したラベルの内容 wPositioningData[10]〜[11] (印刷 p.800 / 原本 p.802) | 内容が「補間対称軸」(「補間対象軸」の誤植の可能性)。原文どおり。 |
| 7 | 配列化したラベルの内容 wPositioningData[0] (印刷 p.800 / 原本 p.802) | 「加速時間№/減速時間№」と「№」記号表記(他の行は「No.」)。原文どおり。 |
| 8 | 配列化したラベルの内容 wSetJogSpeed (印刷 p.799-800 / 原本 p.801-802) | グローバルラベル一覧では wSetJogSpeed はワード(0..2)・コメント「インチング移動量，JOG運転速度」。配列化表では [0] D5=インチング移動量、[1]〜[2] D6〜D7=JOG運転速度(結合セル)。原文どおり。 |
| 9 | マスタ局動作状態確認 ステップ(3) (印刷 p.802 / 原本 p.804) | MC と、同じ接続点から分岐する M99 の回路を MPS/MPP で書き起こした。原本はラダー図のみでニモニックは無い。GX Works3 での実際の変換結果は原本のプロジェクトで確認のこと。MC に対応する MCR は本ファイルの範囲(印刷 p.806 まで)には無い。 |
| 10 | 全ラダー図 (印刷 p.802-806 / 原本 p.804-808) | ステップ番号は回路先頭の表示((0)(3)(12)(51)(93)(184)(189)(257)(293))のみ原本どおり。各命令のステップ番号は原本に表示が無いため付けていない。 |
| 11 | JP.REMTO の完了デバイスの表記 (印刷 p.802-806 / 原本 p.804-808) | JP.REMTO の最終オペランドは、基本パラメータ1・原点復帰基本パラメータ・速度位置切換え・ブロック始動では配列名のみ(例: bBasicParameterSettingRet M5000)、位置決めデータでは要素付き(bPositioningDataSettingRet[0] M5030 / [2] M5032)で表示されている。表示どおり転記した。 |
