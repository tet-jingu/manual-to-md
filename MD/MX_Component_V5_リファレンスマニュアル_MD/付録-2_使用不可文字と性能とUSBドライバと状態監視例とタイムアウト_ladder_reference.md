# MX Component Version 5 リファレンスマニュアル 付録 (2/3) 付6〜付10 p.665-675

| 項目 | 内容 |
|---|---|
| 原本 | 【三菱】MX Component Version 5 リファレンスマニュアル (SH-082394J) |
| メーカー | 三菱電機 |
| 原本ファイル | `PDF/【三菱】MX Component Version 5 リファレンスマニュアル_sh082394j.pdf` (全696ページ) |
| 本ファイルの範囲 | 付録 付6 ラベル名で使用できない文字列 〜 付10 タイムアウト時間について (印刷ページ 663-673 / PDF p.665-675) |
| 出典表記 | `(節 / 印刷ページ / 原本 p.PDFページ)` |
| 作成日 | 2026-11-03 |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。
> 本文中の「○ページ」はすべて原本の**印刷ページ番号**です(PDFページ = 印刷ページ + 2)。
> 付9のプログラム例の変数名先頭(l/I)は原本フォントで判別しにくいため、変数宣言(lInputData 等)に合わせて小文字 l で転記しています。
> 「¥」は原本表記のまま(日本語フォントでのバックスラッシュ表示)。

## 主要用語 対訳表 (Glossary)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| 予約語 | Reserved word | — | 参考訳 |
| ラベル名 | Label name | — | 参考訳 |
| クラス識別子 | Class identifier | VAR 等 | 参考訳 |
| データタイプ階層 | Data type hierarchy | ANY 等 | 参考訳 |
| ST演算子 / IL演算子 | ST operator / IL operator | — | 参考訳 |
| SFC命令 | SFC instruction | — | 参考訳 |
| STコードボディ | ST code body | — | 参考訳 |
| 応用関数 | Application function | — | 参考訳 |
| 日付時刻リテラル | Date and time literal | — | 参考訳 |
| Windows予約語 | Windows reserved word | COM1, LPT1, AUX, CON, PRN, NUL | 参考訳 |
| サロゲートペア | Surrogate pair | 0xD800〜0xDFFF | 参考訳 |
| 制御コード | Control code | U+0000〜U+001F 等 | 参考訳 |
| 環境依存文字 | Platform-dependent character | — | 参考訳 |
| 桁付 / インデックス修飾 | Digit specification / Index modification | — | 参考訳 |
| 性能 / 時間性能 / メモリ性能 | Performance / Time performance / Memory performance | — | 参考訳 |
| 処理時間 | Processing time | ms / 秒 | 参考訳 |
| キャッシュメモリ使用量 | Cache memory usage | KB | 参考訳 |
| ワーキングセット | Working set | KB | 参考訳 |
| ラベル管理サービス | Label management service | — | 参考訳 |
| ラベル管理ユーティリティ | Label Utility | — | 参考訳 |
| システムラベル Ver.1 / Ver.2 | System label Ver.1 / Ver.2 | — | 原本併記 |
| システムラベルデータの最新化 | Update of system label data | — | 参考訳 |
| ラベルスペース | Label space | — | 参考訳 |
| DISK占有サイズ | Disk occupancy size | KB | 参考訳 |
| 一括読出し / 一括書込み | Batch read / Batch write | — | 参考訳 |
| ランダム読出し / ランダム書込み | Random read / Random write | — | 参考訳 |
| USBドライバ | USB driver | Easysocket\USBDrivers | 参考訳 |
| デバイスマネージャー | Device Manager | — | 参考訳 |
| 不明なデバイス | Unknown device | — | 参考訳 |
| 状態監視 | Status monitoring | EntryDeviceStatus / OnDeviceStatus | 参考訳 |
| マスク / 論理和 | Mask / Logical OR | And 65535 / Or &HFFFF0000 | 参考訳 |
| タイムアウト時間 | Timeout time | ActTimeOut | 参考訳 |
| リトライ | Retry | 最大3回 | 参考訳 |
| 受信データエラー | Receive data error | — | 参考訳 |
| 固定タイムアウト時間 | Fixed timeout time | 1000ms〜4500ms | 参考訳 |

## 変換範囲表

| 原本ページ(PDF) | 印刷ページ | 節 | 扱い |
|---|---|---|---|
| p.665-666 | 663-664 | 付6 ラベル名で使用できない文字列 | 全文 |
| p.667-670 | 665-668 | 付7 性能 | 全文(構成イメージ図は文章化) |
| p.671 | 669 | 付8 USBドライバのインストール | 全文 |
| p.672-674 | 670-672 | 付9 ワードデバイスを状態監視する場合のプログラミング例 | 全文(コード全文) |
| p.675 | 673 | 付10 タイムアウト時間について | 全文 |
| p.648-664 | 646-662 | 付1〜付5 | 別ファイル(付録-1) |
| p.676-696 | 674- | 付11以降・関数索引・改訂履歴ほか | 別ファイル(付録-3) |
| p.1-647 | — | 前付け・1〜13章 | 前付け**未変換**、1〜13章は別ファイル(01_〜13-3_) |

## 目次

- 付6 ラベル名で使用できない文字列(予約語 / その他，ラベル使用時の注意事項)
- 付7 性能(システム構成 / MX Component(コントロール)の性能 / ラベル管理サービスの性能 / ラベル管理ユーティリティの性能 / DISK占有サイズ)
- 付8 USBドライバのインストール
- 付9 ワードデバイスを状態監視する場合のプログラミング例(VB.NET / VC++ / C#)
- 付10 タイムアウト時間について

---

## 付6 ラベル名で使用できない文字列 (付6 / 663-664 / 原本 p.665-666)

### 予約語 (付6 / 663 / 原本 p.665)

予約語は，ラベル名として使用できません。
予約語の一覧を下記に示します。

| カテゴリ | 文字列 |
|---|---|
| クラス識別子 | VAR，VAR_RETAIN，VAR_ACCESS，VAR_CONSTANT，VAR_CONSTANT_RETAIN，VAR_INPUT，VAR_INPUT_RETAIN，VAR_OUTPUT，VAR_OUTPUT_RETAIN，VAR_IN_OUT，VAR_IN_EXT，VAR_EXTERNAL，VAR_EXTERNAL_CONSTANT，VAR_EXTERNAL_CONSTANT_RETAIN，VAR_EXTERNAL_RETAIN，VAR_GLOBAL，VAR_GLOBAL_CONSTANT，VAR_GLOBAL_CONSTANT_RETAIN，VAR_GLOBAL_RETAIN |
| データ型 | BOOL，BYTE，INT，SINT，DINT，LINT，UINT，USINT，UDINT，ULINT，WORD，DWORD，LWORD，ARRAY，REAL，LREAL，TIME，STRING，TIMER，COUNTER，RETENTIVETIMER，POINTER，ビット，ワード[符号なし]/ビット列[16ビット]，ダブルワード[符号なし]/ビット列[32ビット]，ワード[符号付き]，ダブルワード[符号付き]，単精度実数，倍精度実数，文字列，時間，タイマ，カウンタ，積算タイマ，ポインタ |
| データタイプ階層 | ANY，ANY_NUM，ANY_BIT，ANY_REAL，ANY_INT，ANY_DATE |
| データタイプ階層 | ANY_SIMPLE，ANY16，ANY32 |
| デバイス名 | X，Y，D，M，T，B，C，F，L，P，V，Z，W，I，N，U，J，K，H，E，A，SD，SM，SW，SB，FX，FY，DX，DY，FD，TR，BL，SG，VD，ZR，ZZ |
| デバイスとして認識される文字列(デバイス名+数字) | X0など |
| ST演算子 | NOT，MOD |
| ST演算子 | (，)，- |
| IL演算子 | LD，LDN，ST，STN，S，S1，R，R1，AND，ANDN，OR，ORN，XOR，XORN，ADD，SUB，MUL，DIV，GT，GE，EQ，NE，LE，LT，JMP，JMPC，JMPCN，CAL，CALC，CALCN，RET，RETC，RETCN |
| IL演算子 | LDI，LDP，LDF，ANI，ANDP，ANDF，ANB，ORI，ORP，ORF，ORB，MPS，MRD，MPP，INV，MEP，MEF，EGP，EGF，OUT(H)，SET，RST，PLS，PLF，FF，DELTA(P)，SFT(P)，MC，MCR，STOP，PAGE，NOP，NOPLF |
| SFC命令 | SFCP，SFCPEND，BLOCK，BEND，TRANL，TRANO，TRANA，TRANC，TRANCA，TRANOA，SEND，TRANOC，TRANOCA，TRANCO，TRANCOC，STEPN，STEPD，STEPSC，STEPSE，STEPST，STEPR，STEPC，STEPG，STEPI，STEPID，STEPISC，STEPISE，STEPIST，STEPIR，TRANJ，TRANOJ，TRANOCJ，TRANCJ，TRANCOJ，TRANCOCJ |
| STコードボディ | RETURN，IF，THEN，ELSE，ELSIF，END_IF，CASE，OF，END_CASE，FOR，TO，BY，DO，END_FOR，WHILE，END_WHILE，REPEAT，UNTIL，END_REPEAT，EXIT，TYPE，END_TYPE，STRUCT，END_STRUCT，RETAIN，VAR_ACCESS，END_VAR，FUNCTION，END_FUNCTION，FUNCTION_BLOCK，END_FUNCTION_BLOCK，STEP，INITIAL_STEP，END_STEP，TRANSITION，END_TRANSITION，FROM，UNTILWHILE |
| 応用関数のファンクション名 | AND_E，NOT_Eなどの応用関数のファンクション名 |
| 応用関数のファンクションブロック名 | CTD，CTUなどの応用関数のファンクションブロック名 |
| 記号 | /，¥，*，?，<，>，｜，"，:，[，]，,，=，+，%，'，～，@，{，}，&，^，.，タブ文字 |
| 記号 | ; |
| 記号 | !，#，$，` |
| 日付時刻リテラル | DATE，DATE_AND_TIME，DT，TIME，TIME_OF_DAY，TOD |
| その他 | ACTION，END_ACTION，CONFIGURATION，END_CONFIGURATION，CONSTANT，F_EDGE，R_EDGE，AT，PROGRAM，WITH，END_PROGRAM，TRUE，FALSE，READ_ONLY，READ_WRITE，RESOURCE，END_RESOURCE，ON，TASK，EN，ENO，BODY_CCE，BODY_FBD，BODY_IL，BODY_LD，BODY_SFC，BODY_ST，END_BODY，END_PARAMETER_SECTION，PARAM_FILE_PATH，PARAMETER_SECTION，SINGLE，RETAIN，INTERVAL |
| K1～K8で始まる文字列 | K1AAAなど |
| ラダー言語でのステートメント | ;FB BLK START，;FB START，;FB END，;FB BLK END，;FB IN，;FB OUT，;FB_NAME，;INSTANCE_NAME，;FB，;INSTANCE |
| 共通命令 | MOVなど |
| Windows予約語 | COM1，COM2，COM3，COM4，COM5，COM6，COM7，COM8，COM9，LPT1，LPT2，LPT3，LPT4，LPT5，LPT6，LPT7，LPT8，LPT9，AUX，CON，PRN，NUL |
| サロゲートペア | 0xD800～0xDBFF，0xDC00～0xDFFF |
| 制御コード | U+0000～U+001F，U+0080～U+009F，U+00A0～U+00BF，U+FFFE，U+FFFF |
| 環境依存文字 | (原本も空欄) |

※原本ではデータタイプ階層・ST演算子・IL演算子・記号のカテゴリ欄が複数行で結合されている(各行に展開)。記号行の縦線は原本の全角「｜」のまま。「STコードボディ」の「UNTILWHILE」は原本表記のまま(要確認: UNTIL，WHILE の区切り抜けと思われる)。

### その他，ラベル使用時の注意事項 (付6 / 664 / 原本 p.666)

- システムラベルVer.1のラベルでは，33文字以上の文字列は使用できません。
- システムラベルVer.2のラベルでは，257文字以上の文字列は使用できません。
  (システムラベルリスト名では33文字以上，構造体名では247文字以上の文字列は使用できません。)
- 半角カナ文字は使用できません。
- スペースは使用できません。
- 先頭文字に半角の数字は使用できません。
- ラベル名の大文字，小文字は区別されません。
- _(アンダーバー )は，ラベル名の先頭および最後には使用できません。
  また，連続する_(アンダーバー )は，データ名およびラベル名には使用できません。
- ビットデバイスの桁付は使用できません。
- インデックス修飾は使用できません。
- バッファメモリは指定できません。
- ラベル登録時に，デバイスチェックを行いません。

---

## 付7 性能 (付7 / 665-668 / 原本 p.667-670)

下記のシステム構成における各性能を示します。

| イメージ図 | 項目 | 項目(詳細) | 内容 |
|---|---|---|---|
| 【図】パソコン ―Ethernet― R08CPU | パソコン | OS | Windows 11 Enterprise |
| (同上) | パソコン | CPU | Intel Core i5-13500(2.50GHz) |
| (同上) | パソコン | メモリ | 16GB |
| (同上) | 対象CPU | — | R08CPU(パソコンと対象CPUは1対1で接続) |
| (同上) | 通信経路 | — | TCP/IP |
| (同上) | システムラベル登録数 | — | 1000件 |

### MX Component(コントロール)の性能 (付7 / 665 / 原本 p.667)

#### 時間性能 (付7 / 665 / 原本 p.667)

デバイスおよびラベルの読込み/書込み性能を示します。

| 処理 | ラベル登録数 | デバイス(ms) | システムラベルVer.1 1回目(ms) | システムラベルVer.1 2回目(ms) | システムラベルVer.2 1回目(ms) | システムラベルVer.2 2回目(ms) |
|---|---|---|---|---|---|---|
| 一括読出し | 1ワード(1ラベル) | 5.9 | 230.5 | 10.7 | 174.4 | 12.5 |
| 一括読出し | 960ワード(1ラベル) | 12.3 | 227.3 | 17.3 | 182.0 | 19.8 |
| 一括読出し | 12288ワード(1ラベル) | 157.9 | 353.5 | 164.5 | 330.3 | 166.9 |
| 一括書込み | 1ワード(1ラベル) | 5.6 | 218.1 | 11.0 | 177.5 | 12.0 |
| 一括書込み | 960ワード(1ラベル) | 17.6 | 232.0 | 22.6 | 189.9 | 24.6 |
| 一括書込み | 12288ワード(1ラベル) | 161.4 | 367.7 | 170.1 | 327.3 | 171.6 |
| ランダム読出し | 1ワード(1ラベル) | 5.6 | 31.0 | 4.5 | 40.8 | 5.0 |
| ランダム読出し | 128ワード(128ラベル) | 24.1 | 1802.7 | 38.2 | 2381.9 | 45.3 |
| ランダム読出し | 256ワード(256ラベル) | 42.3 | 3550.2 | 136.3 | 4866.6 | 169.8 |
| ランダム書込み | 1ワード(1ラベル) | 5.0 | 26.2 | 4.3 | 38.5 | 5.0 |
| ランダム書込み | 128ワード(128ラベル) | 30.5 | 1817.0 | 41.8 | 2334.5 | 47.0 |
| ランダム書込み | 256ワード(256ラベル) | 52.6 | 3550.1 | 140.2 | 4799.8 | 166.1 |

> **Point**
> ユーザ認証機能が有効である場合，上記の表と比べて処理時間が遅くなることがあります。
> 詳細は各CPUユニットのマニュアルを参照してください。

#### メモリ性能 (付7 / 665 / 原本 p.667)

DotUtlTypeコントロールのキャッシュメモリ使用量を示します。

| 処理 | 条件 | メモリ使用量(KB) システムラベルVer.1 | メモリ使用量(KB) システムラベルVer.2 |
|---|---|---|---|
| 一括読出し<br>一括書込み<br>ランダム読出し<br>ランダム書込み | 1000ラベル | (160)*1 | (160)*1 |

> *1 ()内は理論値です。
> キャッシュサイズ(バイト)=160×使用したシステムラベル数
> 160(バイト)=システムラベルあたりのキャッシュデータのサイズ
> システムラベル数=累計1000件の異なるシステムラベルを指定

### ラベル管理サービスの性能 (付7 / 666 / 原本 p.668)

#### 時間性能 (付7 / 666 / 原本 p.668)

ラベル管理サービスの時間性能を示します。

| 処理 | システムラベル定義 | 処理時間(ms) |
|---|---|---|
| パソコン起動時のサービスによるメモリ展開処理 | 構造体型のシステムラベル | 4101 |
| パソコン起動時のサービスによるメモリ展開処理 | 構造体型以外のシステムラベル | 6161 |
| システムラベルデータの最新化 | 構造体型のシステムラベル | 5064 |
| システムラベルデータの最新化 | 構造体型以外のシステムラベル | 7081 |

#### メモリ性能 (付7 / 666 / 原本 p.668)

ラベル管理サービスのメモリ使用量(ワーキングセット)を示します。

- 測定条件: システムラベル登録数: 1000件

| システムラベル定義 | メモリ使用量(KB) システムラベルVer.1 | メモリ使用量(KB) システムラベルVer.2 |
|---|---|---|
| 構造体型のシステムラベル | 30256 | 30268 |
| 構造体型以外のシステムラベル | 31604 | 32156 |

> **Point**
> 測定条件のシステムラベル登録数は，構造体型以外の場合と，構造体型の場合で計算式が異なります。
> - 構造体型以外の場合: システムラベル登録数=ラベル管理ユーティリティで登録したシステムラベル数
> - 構造体型の場合: システムラベル登録数=(1+構造体要素数)×ラベル管理ユーティリティで登録したシステムラベル数
>
> 構造体型のシステムラベル登録数: 1000件については，構造体要素が9つの構造体型のシステムラベルを100件定義して，(1+9)×100=1000件としています。

### ラベル管理ユーティリティの性能 (付7 / 667 / 原本 p.669)

#### 時間性能 (付7 / 667 / 原本 p.669)

ラベル管理ユーティリティの時間性能を示します。

| 処理 | システムラベル定義 | 処理時間(秒) システムラベルVer.1 | 処理時間(秒) システムラベルVer.2 |
|---|---|---|---|
| ラベルスペースの変更(読出し) | 構造体型のシステムラベル | 7.2 | 6.2 |
| ラベルスペースの変更(読出し) | 構造体型以外のシステムラベル | 7.7 | 8.0 |
| ラベルスペースの保存 | 構造体型のシステムラベル | 8.7 | 6.8 |
| ラベルスペースの保存 | 構造体型でないシステムラベル | 9.2 | 9.1 |
| インポート | 構造体型のシステムラベル | 0.9 | 0.6 |
| インポート | 構造体型でないシステムラベル | 0.8 | 0.9 |
| エクスポート | 構造体型のシステムラベル | 0.8 | 0.9 |
| エクスポート | 構造体型でないシステムラベル | 0.8 | 0.9 |

※「構造体型以外」と「構造体型でない」の表記ゆれは原本どおり。

「ラベルスペースの保存」の処理時間は，システムラベルの登録数が増えるほど保存前のチェック処理に時間がかかるようになるため，登録数の増加率以上に処理時間が増加します。

#### メモリ性能 (付7 / 667 / 原本 p.669)

ラベル管理ユーティリティのメモリ使用量(ワーキングセット)を示します。

- 測定条件: システムラベル登録数: 1000件

| システムラベル定義 | メモリ使用量(KB) システムラベルVer.1 | メモリ使用量(KB) システムラベルVer.2 |
|---|---|---|
| システムラベル未定義 | 4108 | 4316 |
| 構造体型のシステムラベル | 8608 | 7500 |
| 構造体型以外のシステムラベル | 12872 | 12256 |

### DISK占有サイズ (付7 / 668 / 原本 p.670)

ラベル管理ユーティリティが生成するシステムラベルデータベースのDISK占有サイズを下記に示します。

| システムラベル定義 | DISK占有サイズ(KB) システムラベルVer.1 | DISK占有サイズ(KB) システムラベルVer.2 |
|---|---|---|
| ラベル未定義(システムラベル登録数: 0件) | 1756 | 24 |
| 構造体型のシステムラベル(システムラベル登録数: 1000件) | 2310 | 89 |
| 構造体型以外のシステムラベル(システムラベル登録数: 1000件) | 2370 | 246 |

> **Point**
> 測定条件のシステムラベル登録数は，構造体型以外の場合と，構造体型の場合で計算式が異なります。
> - 構造体型以外の場合: システムラベル登録数=ラベル管理ユーティリティで登録したシステムラベル数
> - 構造体型の場合: システムラベル登録数=(1+構造体要素数)×ラベル管理ユーティリティで登録したシステムラベル数
>
> 構造体型のシステムラベル登録数: 1000件については，構造体要素が9つの構造体型のシステムラベルを100件定義して，(1+9)×100=1000件としています。

---

## 付8 USBドライバのインストール (付8 / 669 / 原本 p.671)

CPUユニットとUSB通信を行うには，USBドライバのインストールが必要です。

**操作手順**

1. パソコンとCPUユニットをUSBケーブルで接続し，CPUユニットの電源を入れてください。
2. Windowsのデバイスマネージャーで"不明なデバイス"を右クリックして"ドライバーの更新"をクリックします。
3. "ドライバーの更新"画面で，"コンピューターを参照してドライバーを検索"を選択し，次の画面でMX Component Version 5をインストールしたフォルダーの"Easysocket\USBDrivers"を指定します。

インストール時にインストールフォルダーを変更していない場合は下記となります。

- C:\Program Files (x86)\MELSOFT\Easysocket\USBDrivers

なお，複数のMELSOFT製品をインストールしている場合，最初にインストールした製品のフォルダー内の"Easysocket\USBDrivers"を指定してください。
"Easysocket\USBDrivers"が存在しない場合，エクスプローラーで"USBDrivers"を検索してください。
"ユニバーサル シリアル バス コントローラー "に"MITSUBISHI Easysocket Driver"が表示されたらインストール成功です。

---

## 付9 ワードデバイスを状態監視する場合のプログラミング例 (付9 / 670-672 / 原本 p.672-674)

EntryDeviceStatusにて，ワードデバイスが負の値になるのを監視させる場合のプログラミング例について説明します。

### Visual Basic .NETを使用する場合 (付9 / 670 / 原本 p.672)

Visual Basic .NETを使用し，D0が-10，D1が0，D2が10になるのを監視する場合のプログラミング例を以下に示します。

```vb
Dim szDevice As String          '監視するデバイスリスト
Dim lInputData(2) As Long       '設定する値
Dim lEntryData(2) As Long       'EntryDeviceStatus の引数に設定する値
Dim lReturnCode As Long         'EntryDeviceStatus 返り値
Dim lCount As Long              'ループ用カウンタ
'監視するデバイスリストにD0，D1，D2 を設定する。
szDevice = "D0" + vbLf + "D1" + vbLf + "D2"
'D0に対する監視するデバイス値「-10」を設定する。
lInputData(0) = -10
'D1に対する監視するデバイス値「0」を設定する。
lInputData(1) = 0
'D2に対する監視するデバイス値「10」を設定する。
lInputData(2) = 10
'設定する値が負の値である場合は，EntryDeviceStatus に
'設定する値に変換するため，上位2 バイトに「0」を格納する。
'デバイス点数分ループする。
For lCount = 0 To 2
    '設定する値が負の値の場合
    If lInputData(lCount) < 0 Then
        '上位2バイトに「0」を格納するため，65535(0000FFFF[hex])でマスクする。
        lEntryData(lCount) = lInputData(lCount) And 65535
    Else
        '設定する値が正の値である場合，そのままの値をlEntryDataに代入する。
        lEntryData(lCount) = lInputData(lCount)
    End If
Next
'EntryDeviceStatusを実行する。
lReturnCode = AxActUtlType1.EntryDeviceStatus(szDevice, 3, 5, lEntryData(0))
```

#### lData=-1の場合 (付9 / 670 / 原本 p.672)

```vb
Private Sub AxActUtlType1_OnDeviceStatus(ByVal szDevice As String, ByVal lData As Long, ByVal lReturnCode As Long)
Dim lCheckData As Long          'EntryDeviceStatusで，設定した値(上位2バイトに0を格納する前の値)
    '条件成立したデバイス値がWORD型の負の値(32767(7FFF[Hex])より大きい)である場合
    If lData > 32767 Then
        '上位2バイトに「0」が格納されているため，FFFF0000[Hex]との
        '論理和をとることにより，LONG型の負の値に変換する。
        lCheckData = lData Or &HFFFF0000
    Else
        '条件成立したデバイス値が正の値である場合，そのままの値をlCheckDataに代入する。
        lCheckData = lData
    End If
End Sub
```

### Visual C++を使用する場合 (付9 / 671 / 原本 p.673)

Visual C++を使用し，D0が-10，D1が0，D2が10になるのを監視する場合のプログラミング例を以下に示します。

```cpp
CString szDevice;               // 監視するデバイスリスト
LONG lInputData[3];             // 設定する値
LONG lEntryData[3];             // EntryDeviceStatusの引数に設定する値
LONG lReturnCode;               // EntryDeviceStatus用返り値
LONG lCount;                    // ループ用カウンタ
// 監視するデバイスリストにD0，D1，D2を設定する。
szDevice = "D0\nD1\nD2";
// D0に対する監視するデバイス値「-10」を設定する。
lInputData[0] = -10;
// D1に対する監視するデバイス値「0」を設定する。
lInputData[1] = 0;
// D2に対する監視するデバイス値「10」を設定する。
lInputData[2] = 10;

// 設定する値が負の値である場合は，EntryDeviceStatusに
// 設定する値に変換するため，上位2バイトに「0」を格納する。
// デバイス点数分ループする。
for(lCount = 0;lCount<=2; lCount++) {
    // 設定する値が負の値の場合
    if (lInputData[lCount] < 0 ){
        // 上位2バイトに「0」を格納するため，0x0000FFFFでマスクする。
        lEntryData[lCount] = lInputData[lCount] & 0x0000FFFF;
    // 設定する値が正の値の場合
    }else{
        // そのままの値をlEntryDataに代入する。
        lEntryData[lCount] = lInputData[lCount];
    }
}

//EntryDeviceStatusを実行する。
lReturnCode = m_Actutltype.EntryDeviceStatus(szDevice,3,5,lEntryData);
```

#### lData=-1の場合 (付9 / 671 / 原本 p.673)

```cpp
void CSampleDlg::OnDeviceStatusActutltype1(LPCTSTR szDevice, long lData, long lReturnCode)
{
LONG lCheckData;                //EntryDeviceStatusで，設定した値(上位2バイトに0を格納する前の値)
    // 条件成立したデバイス値がWORD型の
    // 負の値(7FFF[Hex]より大きい)である場合
    if(lData > 0x7FFF){
        // 上位2バイトに「0」が格納されているため，FFFF0000[Hex]との
        // 論理和をとることにより，LONG型の負の値に変換する。
        lCheckData = lData | 0xFFFF0000;
    }else{
        // 条件成立したデバイス値が正の値である場合
        // そのままの値をlCheckDataに代入する。
        lCheckData = lData;
    }
}
```

### Visual C#を使用する場合 (付9 / 672 / 原本 p.674)

Visual C#を使用し，D0が-10，D1が0，D2が10になるのを監視する場合のプログラミング例を以下に示します。

```csharp
String szDevice;                    // 監視するデバイスリスト
int[] iInputData = new int[3];      // 設定する値
int[] iEntryData = new int[3];      // EntryDeviceStatusの引数に設定する値
int iReturnCode;                    // EntryDeviceStatus用返り値
int iCount;                         // ループ用カウンタ
// 監視するデバイスリストにD0，D1，D2を設定する。
szDevice = "D0\nD1\nD2";
// D0に対する監視するデバイス値「-10」を設定する。
iInputData[0] = -10;
// D1に対する監視するデバイス値「0」を設定する。
iInputData[1] = 0;
// D2に対する監視するデバイス値「10」を設定する。
iInputData[2] = 10;

// 設定する値が負の値である場合は，EntryDeviceStatusに
// 設定する値に変換するため，上位2バイトに「0」を格納する。
// デバイス点数分ループする。
for(iCount = 0;iCount<=2; iCount++) {
    // 設定する値が負の値の場合
    if (iInputData[iCount] < 0 ){
        // 上位2バイトに「0」を格納するため，0x0000FFFFでマスクする。
        iEntryData[iCount] = iInputData[iCount] & 0x0000FFFF;
    // 設定する値が正の値の場合
    }else{
        // そのままの値をlEntryDataに代入する。
        iEntryData[iCount] = iInputData[iCount];
    }
}
axActUtlType1.ActLogicalStationNumber = 0;
iReturnCode = axActUtlType1.Open();
    // EntryDeviceStatusを実行する。
    iReturnCode = axActUtlType1.EntryDeviceStatus(szDevice, 3, 5, ref iEntryData[0]);
```

※C#版には「lData=-1の場合」(OnDeviceStatus側の変換例)は原本に記載がない。C#版のコメント「lEntryDataに代入する」は変数名 iEntryData と食い違うが原本どおり。

---

## 付10 タイムアウト時間について (付10 / 673 / 原本 p.675)

MX ComponentではActコントロール内のActTimeOutプロパティに設定した値とは別の時間でタイムアウトが発生する場合があります。
各状態でのタイムアウト時間について説明します。

### タイムアウトエラーでリトライする場合 (付10 / 673 / 原本 p.675)

通信を行いタイムアウトエラーが発生した場合，Actコントロール内部でタイムアウトの処理を最大3回繰り返すことがあります。
その際はタイムアウトが発生するまでに設定したタイムアウト値の最大3倍の時間がかかります。

### 受信データエラーでリトライする場合 (付10 / 673 / 原本 p.675)

通信を行い受信データエラーが発生した場合，Actコントロール内部で送受信のリトライ処理を最大3回繰り返すことがあります。
その際は関数が正常終了または異常終了するまでに設定したタイムアウト値の最大3倍の時間がかかります。

### Actコントロール内部の固定時間でタイムアウトが発生する場合 (付10 / 673 / 原本 p.675)

MX Componentでは，Open関数を実行する際にパソコンとシーケンサシステムとの間で正常に接続されているかを確認するための通信を行います。
上記通信を行う場合，Actコントロール内部の固定タイムアウト時間(1000ms～4500ms)を使用します。
ただし，上記通信を行っている間にエラーが発生した場合，タイムアウトエラー以外のエラーが発生することがあります。
