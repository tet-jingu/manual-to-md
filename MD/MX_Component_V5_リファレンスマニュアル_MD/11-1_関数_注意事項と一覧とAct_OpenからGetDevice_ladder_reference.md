# MX Component Version 5 リファレンスマニュアル 11章 関数 (1/8) p.418-445

| 項目 | 内容 |
|---|---|
| 原本 | 【三菱】MX Component Version 5 リファレンスマニュアル (SH-082394J) |
| メーカー | 三菱電機 |
| 原本ファイル | `PDF/【三菱】MX Component Version 5 リファレンスマニュアル_sh082394j.pdf` (全696ページ) |
| 本ファイルの範囲 | 11章冒頭，11.1 プログラミング時の注意事項，11.2 関数一覧，11.3 関数の詳細(Actコントロール用) Open〜GetDevice (印刷ページ 416-443 / PDF p.418-445) |
| 出典表記 | `(節 / 印刷ページ / 原本 p.PDFページ)` |
| 作成日 | 2026-11-03 |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。
> 本文中の「○ページ」はすべて原本の**印刷ページ番号**です(PDFページ = 印刷ページ + 2)。
> デバイスリスト例の「¥n」は原本表記のまま(日本語フォントのバックスラッシュ表示。プログラム上は `\n`)。
> 戻り値の変数名は原本どおり VBA/Visual C++ が `lRet`(小文字エル)，Visual Basic .NET が `IRet`(大文字アイ)，Visual C# が `iRet`。

## 主要用語 対訳表 (Glossary)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| 通信回線のオープン / クローズ | Open / Close communication line | Open / Close | 参考訳 |
| デバイスの一括読出し / 一括書込み | Batch read / write of devices | ReadDeviceBlock / WriteDeviceBlock | 参考訳 |
| デバイスのランダム読出し / ランダム書込み | Random read / write of devices | ReadDeviceRandom / WriteDeviceRandom | 参考訳 |
| デバイスデータの設定 / 取得 | Set / Get device data | SetDevice / GetDevice | 参考訳 |
| バッファメモリ読出し / 書込み | Read / Write buffer memory | ReadBuffer / WriteBuffer | 参考訳 |
| 時計データ読出し / 書込み | Read / Write clock data | GetClockData / SetClockData | 参考訳 |
| CPUユニット形名読出し | Read CPU module model | GetCpuType | 参考訳 |
| リモートコントロール | Remote control | SetCpuStatus | 参考訳 |
| デバイスの状態監視登録 / 解除 | Register / Deregister device status monitoring | EntryDeviceStatus / FreeDeviceStatus | 参考訳 |
| イベント告知 | Event notification | OnDeviceStatus | 参考訳 |
| エラー内容と処置方法の取得 | Get error description and corrective action | GetErrorMessage | 参考訳 |
| メモリの解放 | Release memory | Dispose | 参考訳 |
| LONG型の関数 / SHORT型/INT型の関数 | LONG-type / SHORT-type/INT-type functions | 4バイト / 2バイトデータ | 参考訳 |
| 戻り値 | Return value | lRet / IRet / iRet | 参考訳 |
| COMの戻り値 | COM return value | hResult (HRESULT) | 参考訳 |
| 通信関数の戻り値 | Communication function return value | *lplRetCode | 参考訳 |
| 読出し点数 / 書込み点数 | Number of read / write points | lSize / iSize | 参考訳 |
| デバイス名 / モニタタイプ | Device name / Monitor type | szDevice / szDeviceList | 参考訳 |
| 上位2バイト / 下位2バイト | Upper 2 bytes / Lower 2 bytes | — | 参考訳 |
| ビットデバイス / ワードデバイス / ダブルワードデバイス | Bit / Word / Double-word device | M / D / LTN | 参考訳 |
| 桁指定 | Digit specification | K8M0 | 参考訳 |
| ゲートウェイデバイス | Gateway device | EG | 参考訳 |
| 改行記号 | Line feed | vbLf / ¥n | 参考訳 |
| マルチスレッドプログラミング | Multi-thread programming | STAモデル | 参考訳 |
| アパートメント / マーシャリング | Apartment / Marshaling | CoMarshalInterThreadInterfaceInStream | 参考訳 |
| セーフティモード / 安全デバイス | Safety mode / Safety device | RnSFCPU | 参考訳 |
| 機能未サポートエラー | Function not supported error | 0xF0000007 | 参考訳 |
| シーケンススキャンタイム | Sequence scan time | — | 参考訳 |

## 変換範囲表

| 原本ページ(PDF) | 印刷ページ | 節 | 扱い |
|---|---|---|---|
| p.418 | 416 | 11章冒頭 | 全文 |
| p.418-421 | 416-419 | 11.1 プログラミング時の注意事項 | 全文(フロー図・変換図は文章化) |
| p.422-423 | 420-421 | 11.2 関数一覧 | 全文 |
| p.424-445 | 422-443 | 11.3 関数の詳細(Actコントロール用): Open，Close，ReadDeviceBlock，WriteDeviceBlock，ReadDeviceRandom，WriteDeviceRandom，SetDevice，GetDevice | 全文 |
| p.446-604 | 444-602 | 11.3 ReadBuffer以降〜11.5 Dispose | 別ファイル(11-2〜11-8) |
| p.1-417 | — | 前付け，1〜10章 | 前付け**未変換**，1〜10章は別ファイル(01_〜10-9_) |
| p.605-696 | 603- | 12章〜付録ほか | **未変換** |

## 目次

- 11 関数 / 11.1 プログラミング時の注意事項
- 11.2 関数一覧
- 11.3 関数の詳細(Actコントロール用)
  - Open(通信回線のオープン)
  - Close(通信回線のクローズ)
  - ReadDeviceBlock(デバイスの一括読出し)
  - WriteDeviceBlock(デバイスの一括書込み)
  - ReadDeviceRandom(デバイスのランダム読出し)
  - WriteDeviceRandom(デバイスのランダム書込み)
  - SetDevice(デバイスデータの設定)
  - GetDevice(デバイスデータの取得)

---

## 11 関数 (11 / 416 / 原本 p.418)

プログラミング時の注意事項，関数一覧，および関数の詳細について説明します。

## 11.1 プログラミング時の注意事項 (11.1 / 416-419 / 原本 p.418-421)

関数を使用してプログラム作成を行う場合の注意事項について説明します。  
プログラム作成を開始する前に必ずお読みください。

### Open(通信回線のオープン)について (11.1 / 416 / 原本 p.418)

Open関数は通信経路の確立，シーケンサ内部情報の取得などの処理を行うため，処理時間が長くなる場合があります。  
ユーザプログラムの速度性能をあげるため，効率的なプログラムを作成する必要があります。  
下記に効率的なユーザプログラムと非効率的なユーザプログラムの作成フローを示します。

【図】効率的/非効率的なユーザプログラムの作成フロー (11.1 / 416 / 原本 p.418)
- ＜効率的なユーザプログラム＞: 開始 → 通信回線をオープンする。(Open) → 関数(GetDeviceなど)を使用しCPUユニット，ユニットとアクセスする。 → ユーザプログラムを終了する？ — No: 「関数(GetDeviceなど)を使用し…アクセスする。」に戻る / Yes: 通信回線をクローズする。(Close) → 終了
- ＜非効率的なユーザプログラム＞: 開始 → 通信回線をオープンする。(Open) → 関数(GetDeviceなど)を使用しCPUユニット，ユニットとアクセスする。 → 通信回線をクローズする。(Close) → ユーザプログラムを終了する？ — No: 「通信回線をオープンする。(Open)」に戻る / Yes: 終了

### LONG型の関数とSHORT型/INT型の関数の違い (11.1 / 416-417 / 原本 p.418-419)

MX Componentでは"デバイスの一括読出し"，"デバイスの一括書込み"，"デバイスのランダム読出し"，"デバイスのランダム書込み"，"デバイスデータの設定"および"デバイスデータの取得"を行うための関数としてLONG型の関数とSHORT型/INT型の関数の2種類を用意しています。  
下記にLONG型の関数とSHORT型/INT型の関数との違いを示します。

#### LONG型の関数 (11.1 / 416-417 / 原本 p.418-419)

LONG型の関数は負のデバイス値を書込み/読出しする場合，ユーザプログラム内にてSHORT型/INT型への変換作業を行う必要があります。  
負のデバイス値を書込み/読出しする場合は，SHORT型/INT型の関数を使用してください。  
☞417ページ SHORT型/INT型の関数

| 対象関数 | 参照 |
|---|---|
| ReadDeviceBlock | ☞425ページ ReadDeviceBlock(デバイスの一括読出し) |
| WriteDeviceBlock | ☞428ページ WriteDeviceBlock(デバイスの一括書込み) |
| ReadDeviceRandom | ☞432ページ ReadDeviceRandom(デバイスのランダム読出し) |
| WriteDeviceRandom | ☞432ページ ReadDeviceRandom(デバイスのランダム読出し) |
| SetDevice | ☞439ページ SetDevice(デバイスデータの設定) |
| GetDevice | ☞441ページ GetDevice(デバイスデータの取得) |

※要確認: WriteDeviceRandom の参照先が「432ページ ReadDeviceRandom」になっている(原本表記のまま。本来は436ページ WriteDeviceRandom と思われる)。

**例** ReadDeviceBlockで負の値が入ったデバイスデータを読み出す場合

【図】LONG型関数で負の値を読み出す流れ (11.1 / 417 / 原本 p.419)
- シーケンサ: D0 = -1 (0xFFFF)
- 「ReadDeviceBlockでD0のデータを読み出す。」→ パソコン: lplData = 65535 (0x0000FFFF)。ユーザアプリケーション内ではLONG型(4バイト)のデータとして格納されます。
- 「SHORT/INT型への変換」→ 変換作業: `lpsData = (SHORT)lplData;` lpsData = -1 (0xFFFF)。ユーザアプリケーション内でSHORT/INT型(2バイト)のデータへの変換が必要となります。

#### SHORT型/INT型の関数 (11.1 / 417 / 原本 p.419)

SHORT型/INT型の関数は負のデバイス値を書込み/読出しする場合，書込み/読出しを行うデバイス値をそのまま使用することが可能です。(変換作業を行う必要はありません。)  
ダブルワードデバイスなどを扱う場合は，LONG型の関数を使用してください。  
☞416ページ LONG型の関数

| 対象関数 | 参照 |
|---|---|
| ReadDeviceBlock2 | ☞474ページ ReadDeviceBlock2(デバイスの一括読出し) |
| WriteDeviceBlock2 | ☞477ページ WriteDeviceBlock2(デバイスの一括書込み) |
| ReadDeviceRandom2 | ☞480ページ ReadDeviceRandom2(デバイスのランダム読出し) |
| WriteDeviceRandom2 | ☞483ページ WriteDeviceRandom2(デバイスのランダム書込み) |
| SetDevice2 | ☞486ページ SetDevice2(デバイスデータの設定) |
| GetDevice2 | ☞489ページ GetDevice2(デバイスデータの取得) |

**例** ReadDeviceBlock2で負の値が入ったデバイスデータを読み出す場合

【図】SHORT型/INT型関数で負の値を読み出す流れ (11.1 / 417 / 原本 p.419)
- シーケンサ: D0 = -1 (0xFFFF) → 「ReadDeviceBlock2でD0のデータを読み出す。」→ パソコン: lpsData = -1 (0xFFFF)。ユーザアプリケーション内でSHORT/INT型(2バイト)のデータとして格納されます。

### マルチスレッドプログラミング時の注意事項 (11.1 / 417 / 原本 p.419)

マルチスレッドプログラミングを行う際には，COMおよびActiveXコントロールの規約に従ってください。  
詳細については，COMおよびActiveXコントロールの規約，参考書を参照してください。

> **Point**
> - MX Componentで使用するActiveXコントロールはSTAモデルです。
> - インタフェースポインタを他のアパートメントに渡す場合，インタフェースポインタをマーシャリングする必要があります。
>   COM関数のCoMarshalInterThreadInterfaceInStream，CoGetInterfaceAndReleaseStreamを使用して同期をとってください。

### RnSFCPU使用時の注意 (11.1 / 418 / 原本 p.420)

セーフティモードの場合，下記の関数はRnSFCPUの安全デバイスに対して使用できません。

| 関数名 | 機能 |
|---|---|
| WriteDeviceBlock | デバイスの一括書込み |
| WriteDeviceRandom | デバイスのランダム書込み |
| SetDevice | デバイスデータの設定 |
| WriteDeviceBlock2 | デバイスの一括書込み |
| WriteDeviceRandom2 | デバイスのランダム書込み |
| SetDevice2 | デバイスデータの設定 |
| WriteBuffer | バッファメモリ書込み |

> **Point**
> 使用できない関数を使用した場合は，エラーコード"0x010A42A5"(セーフティモードでは実施できない操作を行った)が返されます。

### QSCPU使用時の注意 (11.1 / 418 / 原本 p.420)

下記の関数はQSCPUに対して使用できません。

| 関数名 | 機能 |
|---|---|
| WriteDeviceBlock | デバイスの一括書込み |
| WriteDeviceRandom | デバイスのランダム書込み |
| SetDevice | デバイスデータの設定 |
| WriteBuffer | バッファメモリ書込み |
| SetClockData | 時計データ書込み |
| SetCpuStatus | リモートコントロール |
| WriteDeviceBlock2 | デバイスの一括書込み |
| WriteDeviceRandom2 | デバイスのランダム書込み |
| SetDevice2 | デバイスデータの設定 |

> **Point**
> 使用できない関数を使用した場合は，エラーコード"0x010A42A0"(CPUアクセスパスワードが不一致)が返されます。

### インバータ/ロボットコントローラ使用時の注意 (11.1 / 418 / 原本 p.420)

.Netコントロールの関数およびプログラムで設定するコントロール(☞42ページ 使用するコントロールの把握)は，インバータ通信/ロボットコントローラ通信時は使用できません。

> **Point**
> 使用できない関数を使用した場合は，エラーコード"0xF0000007"(機能未サポートエラー )が返されます。

### 通信中のプロセスの強制終了について (11.1 / 418 / 原本 p.420)

複数のプロセスで同種のコントロールをオープンして通信を行っている場合，タスクマネージャなどによりプロセスを強制終了すると，他プロセスが通信関数実行部分で停止することがあります。

### 通信開始時のエラーについて (11.1 / 418 / 原本 p.420)

通信診断ボタンの押下時，モニタ開始時，各関数実行時などの通信開始時に，設定されたタイムアウト値以内に通信エラーが発生する場合があります。  
これらは，タイムアウトエラー以前にエラーが検出された場合です。  
(例: 通信ケーブルが接続されていない，シーケンサ電源OFF時など)

### Ethernetユニット使用時の注意事項 (11.1 / 419 / 原本 p.421)

- Openメソッド実行後，Closeメソッドを実行するまでに，Ethernetユニット装着局のシーケンススキャンタイム以上の間隔をおいてください。
- Closeメソッド実行後，再度Openメソッドを実行するまでに最低500ms以上間隔をおいてください。

### コントロールについて (11.1 / 419 / 原本 p.421)

#### CheckDeviceString (11.1 / 419 / 原本 p.421)

各ActコントロールにはCheckDeviceStringメソッドがありますが，使用しないでください。

#### ActUMsgコントロール，ActUWzdコントロール (11.1 / 419 / 原本 p.421)

MX Componentをインストールすると，ActUMsgコントロールおよびActUWzdコントロールが登録されますが，使用しないでください。

---

## 11.2 関数一覧 (11.2 / 420-421 / 原本 p.422-423)

各関数の機能と各コントロールで使用可能な関数の一覧を下記に示します。

| 関数名 | 機能 | 参照*1 |
|---|---|---|
| Open | 通信回線のオープン | Act: ☞422ページ Open(通信回線のオープン)<br>DataLogging: ☞494ページ Open(通信回線のオープン)<br>Dot: ☞504ページ Open(通信回線のオープン) |
| Close | 通信回線のクローズ | Act: ☞424ページ Close(通信回線のクローズ)<br>DataLogging: ☞496ページ Close(通信回線のクローズ)<br>Dot: ☞505ページ Close(通信回線のクローズ) |
| ReadDeviceBlock | デバイスの一括読出し(4バイトデータ) | Act: ☞425ページ ReadDeviceBlock(デバイスの一括読出し)<br>Dot: ☞506ページ ReadDeviceBlock(デバイスの一括読出し) |
| WriteDeviceBlock | デバイスの一括書込み(4バイトデータ) | Act: ☞428ページ WriteDeviceBlock(デバイスの一括書込み)<br>Dot: ☞512ページ WriteDeviceBlock(デバイスの一括書込み) |
| ReadDeviceRandom | デバイスのランダム読出し(4バイトデータ) | Act: ☞432ページ ReadDeviceRandom(デバイスのランダム読出し)<br>Dot: ☞518ページ ReadDeviceRandom(デバイスのランダム読出し) |
| WriteDeviceRandom | デバイスのランダム書込み(4バイトデータ) | Act: ☞436ページ WriteDeviceRandom(デバイスのランダム書込み)<br>Dot: ☞529ページ WriteDeviceRandom(デバイスのランダム書込み) |
| SetDevice | デバイス1点の設定(4バイトデータ) | Act: ☞439ページ SetDevice(デバイスデータの設定)<br>Dot: ☞540ページ SetDevice(デバイスデータの設定) |
| GetDevice | デバイス1点のデータ取得(4バイトデータ) | Act: ☞441ページ GetDevice(デバイスデータの取得)<br>Dot: ☞544ページ GetDevice(デバイスデータの取得) |
| ReadBuffer | バッファメモリの読出し | Act: ☞444ページ ReadBuffer(バッファメモリ読出し)<br>Dot: ☞548ページ ReadBuffer(バッファメモリ読出し) |
| WriteBuffer | バッファメモリの書込み | Act: ☞448ページ WriteBuffer(バッファメモリ書込み)<br>Dot: ☞550ページ WriteBuffer(バッファメモリ書込み) |
| GetClockData | CPUユニットの時計データ読出し | Act: ☞452ページ GetClockData(時計データ読出し)<br>Dot: ☞552ページ GetClockData(時計データ読出し) |
| SetClockData | CPUユニットの時計データ書込み | Act: ☞457ページ SetClockData(時計データ書込み)<br>Dot: ☞554ページ SetClockData(時計データ書込み) |
| GetCpuType | CPUユニット形名読出し | Act: ☞461ページ GetCpuType(CPUユニット形名読出し)<br>Dot: ☞556ページ GetCpuType(CPUユニット形名読出し) |
| SetCpuStatus | CPUユニットのリモートRUN/STOP/PAUSE/RESET | Act: ☞463ページ SetCpuStatus(リモートコントロール)<br>Dot: ☞557ページ SetCpuStatus(リモートコントロール) |
| EntryDeviceStatus*2 | デバイスの状態監視登録 | Act: ☞466ページ EntryDeviceStatus(デバイスの状態監視登録)<br>Dot: ☞559ページ EntryDeviceStatus(デバイスの状態監視登録) |
| FreeDeviceStatus*2 | デバイスの状態監視登録の解除 | Act: ☞470ページ FreeDeviceStatus(デバイスの状態監視登録解除)<br>Dot: ☞563ページ FreeDeviceStatus(デバイスの状態監視登録解除) |
| OnDeviceStatus*2 | イベント告知 | Act: ☞471ページ OnDeviceStatus(イベント告知)<br>Dot: ☞564ページ OnDeviceStatus(イベント告知) |
| ReadDeviceBlock2 | デバイスの一括読出し(2バイトデータ) | Act: ☞474ページ ReadDeviceBlock2(デバイスの一括読出し)<br>Dot: ☞566ページ ReadDeviceBlock2(デバイスの一括読出し) |
| WriteDeviceBlock2 | デバイスの一括書込み(2バイトデータ) | Act: ☞477ページ WriteDeviceBlock2(デバイスの一括書込み)<br>Dot: ☞570ページ WriteDeviceBlock2(デバイスの一括書込み) |
| ReadDeviceRandom2 | デバイスのランダム読出し(2バイトデータ) | Act: ☞480ページ ReadDeviceRandom2(デバイスのランダム読出し)<br>Dot: ☞575ページ ReadDeviceRandom2(デバイスのランダム読出し) |
| WriteDeviceRandom2 | デバイスのランダム書込み(2バイトデータ) | Act: ☞483ページ WriteDeviceRandom2(デバイスのランダム書込み)<br>Dot: ☞584ページ WriteDeviceRandom2(デバイスのランダム書込み) |
| SetDevice2 | デバイス1点の設定(2バイトデータ) | Act: ☞486ページ SetDevice2(デバイスデータの設定)<br>Dot: ☞595ページ SetDevice2(デバイスデータの設定) |
| GetDevice2 | デバイス1点のデータ取得(2バイトデータ) | Act: ☞489ページ GetDevice2(デバイスデータの取得)<br>Dot: ☞599ページ GetDevice2(デバイスデータの取得) |
| GetErrorMessage | エラー内容と処置方法の取得 | Msg: ☞492ページ GetErrorMessage(エラー内容と処置方法の取得) |
| ReadFirstFile | ファイル名/ディレクトリ名の検索 | DataLogging: ☞497ページ ReadFirstFile(ファイル名/ディレクトリ名の検索) |
| ReadNextFile | ファイル名/ディレクトリ名の検索 | DataLogging: ☞499ページ ReadNextFile(ファイル名/ディレクトリ名の検索) |
| ReadClose | 検索の終了 | DataLogging: ☞501ページ ReadClose(検索の終了) |
| GetFile | ロギングファイルの転送 | DataLogging: ☞502ページ GetFile(ロギングファイルの転送) |
| Dispose | メモリの解放 | Dot: ☞602ページ Dispose(メモリの解放) |

> *1 Act: ActUtlType，ActUtlType64，ActProgType，ActProgType64，
> DataLogging: ActDataLogging，ActDataLogging64，ActProgDataLogging，ActProgDataLogging64，
> Dot: DotUtilType，DotUtilType64，
> Msg: ActSupportMsg，ActSupportMsg64
> *2 VC++およびVBAではコントロールをフォームに貼り付けて使用する場合のみ使用できます。オブジェクトを生成して使用する場合には対応していません。また，64ビット用コントロールについては，すべての開発言語で使用できません。
> 各コントロールの違いについては下記を参照ください。
> ☞44ページ ユーザプログラムへのコントロールの追加

※要確認: 脚注*1の「ActDataLogging」「DotUtilType」は原本表記のまま(4章では ActUtlDataLogging，DotUtlType)。

> **Point**
> - 通信対象のCPUユニットがRnSFCPUの場合
>   安全シーケンサシステムを保護するため，バッファメモリに対する書込み，セーフティモードでの安全デバイスに対する書込みを行う関数は，実行するとエラーコードが返ります。
> - 通信対象のCPUユニットがQSCPUの場合
>   安全シーケンサシステムを保護するため，バッファメモリに対する書込み，デバイスに対する書込み・設定，時計データの書込みを行う関数は，実行するとエラーコードが返ります。

---

## 11.3 関数の詳細(Actコントロール用) (11.3 / 422-443 / 原本 p.424-445)

### Open(通信回線のオープン) (11.3 / 422-423 / 原本 p.424-425)

#### 使用可能コントロール (11.3 / 422 / 原本 p.424)

下記のコントロールで使用可能です。

- 32ビット用: ActProgType，ActUtlType
- 64ビット用: ActProgType64，ActUtlType64

#### 機能 (11.3 / 422 / 原本 p.424)

通信回線をオープンします。

#### 書式 (11.3 / 422 / 原本 p.424)

**VBA**

```
lRet = object.Open()
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |

**Visual C++**

```
lRet = object.Open()
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |

**Visual Basic .NET**

```
IRet = object.Open()
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |

**Visual C#**

```
iRet = object.Open()
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |

#### 書式(オブジェクトを生成して使用する場合) (11.3 / 422 / 原本 p.424)

**Visual C++**

```
hResult = object.Open(*lplRetCode)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| HRESULT | hResult | COMの戻り値 | Output |
| LONG | *lplRetCode | 通信関数の戻り値 | Output |

#### 戻り値 (11.3 / 422 / 原本 p.424)

正常終了: 0を返します。  
異常終了: 0以外を返します。(☞617ページ エラーコード)

#### 説明 (11.3 / 423 / 原本 p.425)

通信回線をオープンします。  
Open関数用プロパティの設定値をもとに回線の接続を行います。

> **Point**
> - Open完了後にOpen関数用プロパティを変更しても，通信相手先の変更は行われません。通信設定の変更を行う場合は，1度通信回線をクローズした後，通信相手先の設定を行い再度通信回線をオープンしてください。
> - Openする際に，ActCpuTypeプロパティに通信を行うCPUと異なるCPUタイプを入力した場合でも，Openが正常に終了することがあります。
>   このような場合，接続範囲，使用可能メソッドおよびデバイス範囲が狭まるなどの現象が発生します。
>   Openを行う際には，ActCpuTypeプロパティに正しいCPUタイプを設定してください。

### Close(通信回線のクローズ) (11.3 / 424 / 原本 p.426)

#### 使用可能コントロール (11.3 / 424 / 原本 p.426)

下記のコントロールで使用可能です。

- 32ビット用: ActProgType，ActUtlType
- 64ビット用: ActProgType64，ActUtlType64

#### 機能 (11.3 / 424 / 原本 p.426)

通信回線をクローズします。

#### 書式 (11.3 / 424 / 原本 p.426)

**VBA**

```
lRet = object.Close()
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |

**Visual C++**

```
lRet = object.Close()
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |

**Visual Basic .NET**

```
IRet = object.Close()
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |

**Visual C#**

```
iRet = object.Close()
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |

#### 書式(オブジェクトを生成して使用する場合) (11.3 / 424 / 原本 p.426)

**Visual C++**

```
hResult = object.Close(*lplRetCode)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| HRESULT | hResult | COMの戻り値 | Output |
| LONG | *lplRetCode | 通信関数の戻り値 | Output |

#### 戻り値 (11.3 / 424 / 原本 p.426)

正常終了: 0を返します。  
異常終了: 0以外を返します。(☞617ページ エラーコード)

#### 説明 (11.3 / 424 / 原本 p.426)

Open関数にて接続した回線をクローズします。

### ReadDeviceBlock(デバイスの一括読出し) (11.3 / 425-427 / 原本 p.427-429)

#### 使用可能コントロール (11.3 / 425 / 原本 p.427)

下記のコントロールで使用可能です。

- 32ビット用: ActProgType，ActUtlType
- 64ビット用: ActProgType64，ActUtlType64

#### 機能 (11.3 / 425 / 原本 p.427)

デバイスの一括読出しを行います。

#### 書式 (11.3 / 425 / 原本 p.427)

**VBA**

```
lRet = object.ReadDeviceBlock(szDevice, lSize, lData(0))
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| String | szDevice | デバイス名 | Input |
| Long | lSize | 読出し点数 | Input |
| Long | lData(n) | 読み出したデバイス値 | Output |

**Visual C++**

```
lRet = object.ReadDeviceBlock(szDevice, lSize, *lplData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| CString | szDevice | デバイス名 | Input |
| Long | lSize | 読出し点数 | Input |
| Long | *lplData | 読み出したデバイス値 | Output |

**Visual Basic .NET**

```
IRet = object.ReadDeviceBlock(szDevice, iSize, iData(0))
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| String | szDevice | デバイス名 | Input |
| Integer | iSize | 読出し点数 | Input |
| Integer | iData(n) | 読み出したデバイス値 | Output |

**Visual C#**

```
iRet = object.ReadDeviceBlock(szDevice, iSize, out iData[0])
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |
| String | szDevice | デバイス名 | Input |
| int | iSize | 読出し点数 | Input |
| int[n] | iData | 読み出したデバイス値 | Output |

#### 書式(オブジェクトを生成して使用する場合) (11.3 / 425 / 原本 p.427)

**Visual C++**

```
hResult = object.ReadDeviceBlock(szDevice, lSize, *lplData, *lplRetCode)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| HRESULT | hResult | COMの戻り値 | Output |
| BSTR | szDevice | デバイス名 | Input |
| LONG | lSize | 読出し点数 | Input |
| LONG | *lplData | 読み出したデバイス値 | Output |
| LONG | *lplRetCode | 通信関数の戻り値 | Output |

#### 戻り値 (11.3 / 426 / 原本 p.428)

正常終了: 0を返します。  
異常終了: 0以外を返します。(☞617ページ エラーコード)

#### 説明 (11.3 / 426 / 原本 p.428)

- szDeviceにて指定したデバイスから，lSize(iSize)分のデバイス値を一括して読み出します。
- 読み出したデバイス値は，lData(lplDataまたはiData)に格納されます。
- lData(lplDataまたはiData)は，lSize(iSize)以上の配列を確保してください。

> **Point**
> - lSize(iSize)に指定できる最大読出し点数は，下記の満たす範囲です。
>   読出し開始デバイス番号 + 読出し点数 ≤ 最終デバイス番号
> - ビットデバイス指定時は，デバイス番号は16の倍数が指定可能です。
> - インバータ通信/ロボットコントローラ通信時は使用できません。
> - lData(lplDataまたはiData)は，lSize(iSize)に指定した点数分のメモリエリアを用意してください。
>   メモリエリアがない場合は，アプリケーションエラーなど重大な現象が発生するおそれがあります。
> - ロングタイマの接点(LTS)，ロングタイマのコイル(LTC)，ロング積算タイマの接点(LSTS)，ロング積算タイマのコイル(LSTC)のデバイスの読出しはできません。ReadDeviceRandom関数，またはGetDevice関数を使用してください。

#### デバイス指定方法 (11.3 / 426-427 / 原本 p.428-429)

デバイスの指定方法を下記に示します。

##### ビットデバイス指定時 (11.3 / 426 / 原本 p.428)

(例) M0から16点単位で3点(3ワード分)読み出す。

| 上位2バイト | 下位2バイト |
|---|---|
| 使用しません。(0が格納されます。) | M0～M15*1 |
| (同上) | M16～M31*1 |
| (同上) | M32～M47*1 |

> *1 デバイスの番号順に，下位ビットから格納されます。

##### ワードデバイス指定時 (11.3 / 426 / 原本 p.428)

(例) D0から3点読み出す。

| 上位2バイト | 下位2バイト |
|---|---|
| 使用しません。(0が格納されます。) | D0 |
| (同上) | D1 |
| (同上) | D2 |

##### FXCPUのCN200以降指定時 (11.3 / 427 / 原本 p.429)

(例) CN200から6点読み出す。  
FXCPUのCN200以降は，2点で2ワード読み出します。1点ではエラーとなります。

| 上位2バイト | 下位2バイト |
|---|---|
| 使用しません。(0が格納されます。) | CN200のL |
| (同上) | CN200のH |
| (同上) | CN201のL |
| (同上) | CN201のH |
| (同上) | CN202のL |
| (同上) | CN202のH |

##### FDデバイス指定時(4ワードデバイス) (11.3 / 427 / 原本 p.429)

(例) FD0から6点読み出す。

| 上位2バイト | 下位2バイト |
|---|---|
| 使用しません。(0が格納されます。) | FD0のLL |
| (同上) | FD0のLH |
| (同上) | FD0のHL |
| (同上) | FD0のHH |
| (同上) | FD1のLL |
| (同上) | FD1のLH |

##### ゲートウェイデバイスに割り付けられた8ビットデバイス (11.3 / 427 / 原本 p.429)

(例) EG0から4点読み出す。  
(EG0～EG3に8ビットデバイス(シャープ社製シーケンサのE0000～E0007)が割り付けられている場合)

| 上位2バイト | 下位2バイト |
|---|---|
| 使用しません。(0が格納されます。) | EG0: (E0001)(上位8ビット) / (E0000)(下位8ビット) |
| (同上) | EG1: (E0003) / (E0002) |
| (同上) | EG2: (E0005) / (E0004) |
| (同上) | EG3: (E0007) / (E0006) |

※下位2バイトは原本では「EGn」行の下に上位8ビット/下位8ビットの2セルに分かれている。

##### ダブルワードデバイス指定時 (11.3 / 427 / 原本 p.429)

(例) LTN0から3点読み出す。

| 上位2バイト | 下位2バイト |
|---|---|
| LTN0のH | LTN0のL |
| LTN1のH | LTN1のL |
| LTN2のH | LTN2のL |

### WriteDeviceBlock(デバイスの一括書込み) (11.3 / 428-431 / 原本 p.430-433)

#### 使用可能コントロール (11.3 / 428 / 原本 p.430)

下記のコントロールで使用可能です。

- 32ビット用: ActProgType，ActUtlType
- 64ビット用: ActProgType64，ActUtlType64

#### 機能 (11.3 / 428 / 原本 p.430)

デバイスの一括書込みを行います。

#### 書式 (11.3 / 428 / 原本 p.430)

**VBA**

```
lRet = object.WriteDeviceBlock(szDevice, lSize, lData(0))
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| String | szDevice | デバイス名 | Input |
| Long | lSize | 書込み点数 | Input |
| Long | lData(n) | 書き込むデバイス値 | Input |

**Visual C++**

```
lRet = object.WriteDeviceBlock(szDevice, lSize, *lplData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| CString | szDevice | デバイス名 | Input |
| Long | lSize | 書込み点数 | Input |
| Long | *lplData | 書き込むデバイス値 | Input |

**Visual Basic .NET**

```
IRet = object.WriteDeviceBlock(szDevice, iSize, iData(0))
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| String | szDevice | デバイス名 | Input |
| Integer | iSize | 書込み点数 | Input |
| Integer | iData(n) | 書き込むデバイス値 | Input |

**Visual C#**

```
iRet = object.WriteDeviceBlock(szDevice, iSize, ref iData[0])
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |
| String | szDevice | デバイス名 | Input |
| int | iSize | 書込み点数 | Input |
| int[n] | iData | 書き込むデバイス値 | Input |

#### 書式(オブジェクトを生成して使用する場合) (11.3 / 428 / 原本 p.430)

**Visual C++**

```
hResult = object.WriteDeviceBlock(szDevice, lSize, *lplData, *lplRetCode)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| HRESULT | hResult | COMの戻り値 | Output |
| BSTR | szDevice | デバイス名 | Input |
| LONG | lSize | 書込み点数 | Input |
| LONG | *lplData | 書き込むデバイス値 | Input |
| LONG | *lplRetCode | 通信関数の戻り値 | Output |

#### 戻り値 (11.3 / 429 / 原本 p.431)

正常終了: 0を返します。  
異常終了: 0以外を返します。(☞617ページ エラーコード)

#### 説明 (11.3 / 429 / 原本 p.431)

- szDeviceにて指定したデバイスから，lSize(iSize)分のデバイス値を一括して書き込みます。
- 書き込むデバイス値を，lData(lplDataまたはiData)に格納します。
- lData(lplDataまたはiData)は，lSize(iSize)以上の配列を確保してください。

> **Point**
> - lSize(iSize)に指定できる最大書込み点数は，下記の満たす範囲です。
>   書込み開始デバイス番号 + 書込み点数 ≤ 最終デバイス番号
> - ビットデバイス指定時は，デバイス番号は16の倍数が指定可能です。
> - lData(lplDataまたはiData)は，lSize(iSize)に指定した点数分のメモリエリアを用意してください。
>   メモリエリアがない場合は，アプリケーションエラーなど重大な現象が発生するおそれがあります。
> - ロングタイマの接点(LTS)，ロングタイマのコイル(LTC)，ロング積算タイマの接点(LSTS)，ロング積算タイマのコイル(LSTC)のデバイスの書込みはできません。WriteDeviceRandom関数，またはSetDevice関数を使用してください。
> - RnSFCPUのセーフティモードで安全デバイスに対して実行した場合は，エラーコード"0x010A42A5"(セーフティモードでは実施できない操作を行った)が返されます。
> - インバータ通信/ロボットコントローラ通信時は使用できません。

#### デバイス指定方法 (11.3 / 430-431 / 原本 p.432-433)

デバイスの指定方法を下記に示します。

##### ビットデバイス指定時 (11.3 / 430 / 原本 p.432)

(例) M0から16点単位で3点(3ワード分)書き込む。

| 上位2バイト | 下位2バイト |
|---|---|
| 使用しません。(0が格納されます。) | M0～M15*1 |
| (同上) | M16～M31*1 |
| (同上) | M32～M47*1 |

> *1 デバイスの番号順に，下位ビットから格納されます。

##### ワードデバイス指定時 (11.3 / 430 / 原本 p.432)

(例) D0から3点書き込む。

| 上位2バイト | 下位2バイト |
|---|---|
| 使用しません。(0が格納されます。) | D0 |
| (同上) | D1 |
| (同上) | D2 |

##### FXCPUのCN200以降指定時 (11.3 / 430 / 原本 p.432)

(例) CN200から6点書き込む。  
FXCPUのCN200以降は，2点で2ワード書き込みます。1点ではエラーとなります。

| 上位2バイト | 下位2バイト |
|---|---|
| 使用しません。(0が格納されます。) | CN200のL |
| (同上) | CN200のH |
| (同上) | CN201のL |
| (同上) | CN201のH |
| (同上) | CN202のL |
| (同上) | CN202のH |

##### FDデバイス指定時(4ワードデバイス) (11.3 / 431 / 原本 p.433)

(例) FD0から6点書き込む。

| 上位2バイト | 下位2バイト |
|---|---|
| 使用しません。(0が格納されます。) | FD0のLL |
| (同上) | FD0のLH |
| (同上) | FD0のHL |
| (同上) | FD0のHH |
| (同上) | FD1のLL |
| (同上) | FD1のLH |

##### ゲートウェイデバイスに割り付けられた8ビットデバイス (11.3 / 431 / 原本 p.433)

(例) EG0から4点書き込む。  
(EG0～EG3に8ビットデバイス(シャープ社製シーケンサのE0000～E0007)が割り付けられている場合)

| 上位2バイト | 下位2バイト |
|---|---|
| 使用しません。(0が格納されます。) | EG0: (E0001)(上位8ビット) / (E0000)(下位8ビット) |
| (同上) | EG1: (E0003) / (E0002) |
| (同上) | EG2: (E0005) / (E0004) |
| (同上) | EG3: (E0007) / (E0006) |

※下位2バイトは原本では「EGn」行の下に上位8ビット/下位8ビットの2セルに分かれている。

##### ダブルワードデバイス指定時 (11.3 / 431 / 原本 p.433)

(例) LTN0から3点書き込む。

| 上位2バイト | 下位2バイト |
|---|---|
| LTN0のH | LTN0のL |
| LTN1のH | LTN1のL |
| LTN2のH | LTN2のL |

### ReadDeviceRandom(デバイスのランダム読出し) (11.3 / 432-435 / 原本 p.434-437)

#### 使用可能コントロール (11.3 / 432 / 原本 p.434)

下記のコントロールで使用可能です。

- 32ビット用: ActProgType，ActUtlType
- 64ビット用: ActProgType64，ActUtlType64

#### 機能 (11.3 / 432 / 原本 p.434)

デバイスのランダム読出しを行います。  
インバータ/ロボットコントローラのモニタタイプのランダム読出しを行います。

#### 書式 (11.3 / 432 / 原本 p.434)

**VBA**

```
lRet = object.ReadDeviceRandom(szDeviceList, lSize, lData(0))
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| String | szDeviceList | デバイス名/モニタタイプ | Input |
| Long | lSize | 読出し点数 | Input |
| Long | lData(n) | 読み出したデバイス値 | Output |

**Visual C++**

```
lRet = object.ReadDeviceRandom(szDeviceList, lSize,*lplData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| CString | szDeviceList | デバイス名/モニタタイプ | Input |
| Long | lSize | 読出し点数 | Input |
| Long | *lplData | 読み出したデバイス値 | Output |

**Visual Basic .NET**

```
IRet = object.ReadDeviceRandom(szDeviceList, iSize, iData(0))
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| String | szDeviceList | デバイス名/モニタタイプ | Input |
| Integer | iSize | 読出し点数 | Input |
| Integer | iData(n) | 読み出したデバイス値 | Output |

**Visual C#**

```
iRet = object.ReadDeviceRandom(szDeviceList, iSize, out iData[0])
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |
| String | szDeviceList | デバイス名/モニタタイプ | Input |
| int | iSize | 読出し点数 | Input |
| int[n] | iData | 読み出したデバイス値 | Output |

#### 書式(オブジェクトを生成して使用する場合) (11.3 / 432 / 原本 p.434)

**Visual C++**

```
hResult = object.ReadDeviceRandom(szDeviceList, lSize, *lplData, *lplRetCode)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| HRESULT | hResult | COMの戻り値 | Output |
| BSTR | szDeviceList | デバイス名/モニタタイプ | Input |
| LONG | lSize | 読出し点数 | Input |
| LONG | *lplData | 読み出したデバイス値 | Output |
| LONG | *lplRetCode | 通信関数の戻り値 | Output |

#### 戻り値 (11.3 / 433 / 原本 p.435)

正常終了: 0を返します。  
異常終了: 0以外を返します。(☞617ページ エラーコード)

#### 説明 (11.3 / 433 / 原本 p.435)

- szDeviceListにて指定したデバイス群/モニタタイプ群を，lSize(iSize)分のデバイス値/モニタタイプ分だけ読み出します。
- 読み出したデバイス値は，lData(lplDataまたはiData)に格納されます。
- デバイスリストに指定する文字列は改行記号で区切ってください。最終デバイスの後ろには改行記号は必要ありません。
  (例)

| 開発言語 | デバイスリストの指定 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"D0" & vbLf & "D1" & vbLf & "D2"` |
| Visual C++使用時 | `D0¥nD1¥nD2` |
| Visual C#使用時 | `D0¥nD1¥nD2` |

- lData(lplDataまたはiData)は，lSize(iSize)以上の配列を確保してください。
- モニタ可能な項目(モニタタイプ)は，下記を参照してください。
  ☞160ページ アクセス可能デバイスおよびデバイスタイプ
- グローバルラベルにアクセスする場合は，szDeviceListにグローバルラベルを指定してください。また，使用可能なグローバルラベルのデータ型および指定点数については下記を参照してください。
  ☞22ページ グローバルラベル名を指定したデータ取得

> **Point**
> - lSize(iSize)に指定できる最大読出し点数は，0x7FFFFFFF点までです。
> - lData(lplDataまたはiData)は，lSize(iSize)に指定した点数分のメモリエリアを用意してください。
>   メモリエリアがない場合は，アプリケーションエラーなど重大な現象が発生するおそれがあります。

#### デバイス指定方法 (11.3 / 434-435 / 原本 p.436-437)

デバイスの指定方法を下記に示します。

##### 下記のように指定した場合(点数は3点) (11.3 / 434 / 原本 p.436)

| 開発言語 | デバイスリストの指定 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"M0" & vbLf & "D0" & vbLf & "K8M0"` |
| Visual C++使用時 | `M0¥nD0¥nK8M0` |
| Visual C#使用時 | `M0¥nD0¥nK8M0` |

| 上位2バイト | 下位2バイト |
|---|---|
| 使用しません。(0が格納されます。) | M0 |
| (同上) | D0 |
| M16～M31*1 | M0～M15*1 |

> *1 デバイスの番号順に，下位ビットから格納されます。

##### FXCPUのCN200以降を含むデバイスを指定した場合(点数は合計3点) (11.3 / 434 / 原本 p.436)

FXCPUのCN200以降は，ランダム読出しでは1点で2ワード分読み出します。

| 開発言語 | デバイスリストの指定 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"D0" & vbLf & "CN200" & vbLf & "D1"` |
| Visual C++使用時 | `D0¥nCN200¥nD1` |
| Visual C#使用時 | `D0¥nCN200¥nD1` |

| 上位2バイト | 下位2バイト |
|---|---|
| 使用しません。(0が格納されます。) | D0 |
| CN200のH | CN200のL |
| 使用しません。(0が格納されます。) | D1 |

##### FDを含むデバイスを指定した場合(点数は合計3点) (11.3 / 434 / 原本 p.436)

| 開発言語 | デバイスリストの指定 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"D0" & vbLf & "FD0" & vbLf & "D1"` |
| Visual C++使用時 | `D0¥nFD0¥nD1` |
| Visual C#使用時 | `D0¥nFD0¥nD1` |

| 上位2バイト | 下位2バイト |
|---|---|
| 使用しません。(0が格納されます。) | D0 |
| (同上) | FD0のLL |
| (同上) | D1 |

##### EGを含むデバイスを指定した場合(点数は合計3点) (11.3 / 435 / 原本 p.437)

EG0に8ビットデバイス(シャープ社製シーケンサのE0000，E0001)が割り付けられている例を下記に示します。

| 開発言語 | デバイスリストの指定 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"D0" & vbLf & "EG0" & vbLf & "D1"` |
| Visual C++使用時 | `D0¥nEG0¥nD1` |
| Visual C#使用時 | `D0¥nEG0¥nD1` |

| 上位2バイト | 下位2バイト |
|---|---|
| 使用しません。(0が格納されます。) | D0 |
| (同上) | EG0 |
| (同上) | (E0001) |
| (同上) | D1 |

※ReadDeviceRandomのEG例は原本では「(E0001)」のセルのみで「(E0000)」が無い(WriteDeviceRandom・SetDevice等では「(E0001) / (E0000)」の2セル)。原本どおり。

##### ダブルワードデバイスを指定した場合 (11.3 / 435 / 原本 p.437)

| 開発言語 | デバイスリストの指定 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"LTN0" & vbLf & "LTN1" & vbLf & "LTN2"` |
| Visual C++使用時 | `LTN0¥nLTN1¥nLTN2` |
| Visual C#使用時 | `LTN0¥nLTN1¥nLTN2` |

| 上位2バイト | 下位2バイト |
|---|---|
| LTN0のH | LTN0のL |
| LTN1のH | LTN1のL |
| LTN2のH | LTN2のL |

##### インバータのモニタタイプ(1，2，5)を指定した場合(点数は合計3点) (11.3 / 435 / 原本 p.437)

| 開発言語 | デバイスリストの指定 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"1" & vbLf &"2" & vbLf &"5"` |
| Visual C++使用時 | `1¥n2¥n5` |
| Visual C#使用時 | `1¥n2¥n5` |

| 上位2バイト | 下位2バイト |
|---|---|
| 1のH | 1のL |
| 2のH | 2のL |
| 5のH | 5のL |

##### ロボットコントローラのモニタタイプ(223.102.A，223.103.B)を指定した場合(点数は合計2点) (11.3 / 435 / 原本 p.437)

形式: (要求ID).(データタイプ).(引数)

| 開発言語 | デバイスリストの指定 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"223.102.A" & vbLf &"223.103.B"` |
| Visual C++使用時 | `223.102.A¥n223.103.B` |
| Visual C#使用時 | `223.102.A¥n223.103.B` |

| 上位2バイト | 下位2バイト |
|---|---|
| 223.102.AのH | 223.102.AのL |
| 223.103.BのH | 223.103.BのL |

### WriteDeviceRandom(デバイスのランダム書込み) (11.3 / 436-438 / 原本 p.438-440)

#### 使用可能コントロール (11.3 / 436 / 原本 p.438)

下記のコントロールで使用可能です。

- 32ビット用: ActProgType，ActUtlType
- 64ビット用: ActProgType64，ActUtlType64

#### 機能 (11.3 / 436 / 原本 p.438)

デバイスのランダム書込みを行います。

#### 書式 (11.3 / 436 / 原本 p.438)

**VBA**

```
lRet = object.WriteDeviceRandom(szDeviceList, lSize,lData(0))
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| String | szDeviceList | デバイス名 | Input |
| Long | lSize | 書込み点数 | Input |
| Long | lData(n) | 書き込むデバイス値 | Input |

**Visual C++**

```
lRet = object.WriteDeviceRandom(szDeviceList, lSize,*lplData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| CString | szDeviceList | デバイス名 | Input |
| Long | lSize | 書込み点数 | Input |
| Long | *lplData | 書き込むデバイス値 | Input |

**Visual Basic .NET**

```
IRet = object.WriteDeviceRandom(szDeviceList, iSize, iData(0))
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| String | szDeviceList | デバイス名 | Input |
| Integer | iSize | 書込み点数 | Input |
| Integer | iData(n) | 書き込むデバイス値 | Input |

**Visual C#**

```
iRet = object.WriteDeviceRandom(szDeviceList, iSize, ref iData[0])
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |
| String | szDeviceList | デバイス名 | Input |
| int | iSize | 書込み点数 | Input |
| int[n] | iData | 書き込むデバイス値 | Input |

#### 書式(オブジェクトを生成して使用する場合) (11.3 / 436 / 原本 p.438)

**Visual C++**

```
hResult = object.WriteDeviceRandom(szDeviceList, lSize, *lplData,*lplRetCode)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| HRESULT | hResult | COMの戻り値 | Output |
| BSTR | szDeviceList | デバイス名 | Input |
| LONG | lSize | 書込み点数 | Input |
| LONG | *lplData | 書き込むデバイス値 | Input |
| LONG | *lplRetCode | 通信関数の戻り値 | Output |

#### 戻り値 (11.3 / 437 / 原本 p.439)

正常終了: 0を返します。  
異常終了: 0以外を返します。(☞617ページ エラーコード)

#### 説明 (11.3 / 437 / 原本 p.439)

- szDeviceListにて指定したデバイス群を，lSize(iSize)分のデバイス値だけ書き込みます。
- 書き込むデバイス値を，lData(lplDataまたはiData)に格納します。
- デバイスリストに指定する文字列は改行記号で区切ってください。
  最終デバイスの後ろには改行記号は必要ありません。
  (例)

| 開発言語 | デバイスリストの指定 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"D0" & vbLf & "D1" & vbLf & "D2"` |
| Visual C++使用時 | `D0¥nD1¥nD2` |
| Visual C#使用時 | `D0¥nD1¥nD2` |

- lData(lplDataまたはiData)は，lSize(iSize)以上の配列を確保してください。
- グローバルラベルにアクセスする場合は，szDeviceListにグローバルラベルを指定してください。また，使用可能なグローバルラベルのデータ型および指定点数については下記を参照してください。
  ☞22ページ グローバルラベル名を指定したデータ取得

> **Point**
> - lSize(iSize)に指定できる最大書込み点数は，0x7FFFFFFF点までです。
> - lData(lplDataまたはiData)は，lSize(iSize)に指定した点数分のメモリエリアを用意してください。
>   メモリエリアがない場合は，アプリケーションエラーなど重大な現象が発生するおそれがあります。
> - QモーションCPUへアクセスを行うと，エラーが返ります。
> - RnSFCPUのセーフティモードで安全デバイスに対して実行した場合は，エラーコード"0x010A42A5"(セーフティモードでは実施できない操作を行った)が返されます。
> - インバータ通信/ロボットコントローラ通信時は使用できません。

#### デバイス指定方法 (11.3 / 437-438 / 原本 p.439-440)

デバイスの指定方法を下記に示します。

##### 下記のように指定した場合(点数は3点) (11.3 / 437 / 原本 p.439)

| 開発言語 | デバイスリストの指定 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"M0" & vbLf & "D0" & vbLf & "K8M0"` |
| Visual C++使用時 | `M0¥nD0¥nK8M0` |
| Visual C#使用時 | `M0¥nD0¥nK8M0` |

| 上位2バイト | 下位2バイト |
|---|---|
| 使用しません。(0が格納されます。) | M0 |
| (同上) | D0 |
| M16～M31*1 | M0～M15*1 |

> *1 デバイスの番号順に，下位ビットから格納されます。

##### FXCPUのCN200以降を含むデバイスを指定した場合(点数は合計3点) (11.3 / 438 / 原本 p.440)

FXCPUのCN200以降は，ランダム読出しでは1点で2ワード分読み出します。

※WriteDeviceRandomの節でも原本は「ランダム読出しでは…読み出します」の表記(原本どおり)。

| 開発言語 | デバイスリストの指定 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"D0" & vbLf & "CN200" & vbLf & "D1"` |
| Visual C++使用時 | `D0¥nCN200¥nD1` |
| Visual C#使用時 | `D0¥nCN200¥nD1` |

| 上位2バイト | 下位2バイト |
|---|---|
| 使用しません。(0が格納されます。) | D0 |
| CN200のH | CN200のL |
| 使用しません。(0が格納されます。) | D1 |

##### FDを含むデバイスを指定した場合(点数は合計3点) (11.3 / 438 / 原本 p.440)

※WriteDeviceRandomの節では原本にデバイスリスト例の記載が無い(表のみ)。

| 上位2バイト | 下位2バイト |
|---|---|
| 使用しません。(0が格納されます。) | D0 |
| (同上) | FD0のLL |
| (同上) | D1 |

##### EGを含むデバイスを指定した場合(点数は合計3点) (11.3 / 438 / 原本 p.440)

EG0に8ビットデバイス(シャープ社製シーケンサのE0000，E0001)が割り付けられている例を下記に示します。

| 開発言語 | デバイスリストの指定 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"D0" & vbLf & "EG0" & vbLf & "D1"` |
| Visual C++使用時 | `D0¥nEG0¥nD1` |
| Visual C#使用時 | `D0¥nEG0¥nD1` |

| 上位2バイト | 下位2バイト |
|---|---|
| 使用しません。(0が格納されます。) | D0 |
| (同上) | EG0 |
| (同上) | (E0001)(上位8ビット) / (E0000)(下位8ビット) |
| (同上) | D1 |

##### ダブルワードデバイスを指定した場合 (11.3 / 438 / 原本 p.440)

| 開発言語 | デバイスリストの指定 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"LTN0" & vbLf & "LTN1" & vbLf & "LTN2"` |
| Visual C++使用時 | `LTN0¥nLTN1¥nLTN2` |
| Visual C#使用時 | `LTN0¥nLTN1¥nLTN2` |

| 上位2バイト | 下位2バイト |
|---|---|
| LTN0のH | LTN0のL |
| LTN1のH | LTN1のL |
| LTN2のH | LTN2のL |

### SetDevice(デバイスデータの設定) (11.3 / 439-440 / 原本 p.441-442)

#### 使用可能コントロール (11.3 / 439 / 原本 p.441)

下記のコントロールで使用可能です。

- 32ビット用: ActProgType，ActUtlType
- 64ビット用: ActProgType64，ActUtlType64

#### 機能 (11.3 / 439 / 原本 p.441)

デバイス1点の設定を行います。

#### 書式 (11.3 / 439 / 原本 p.441)

**VBA**

```
lRet = object.SetDevice(szDevice, lData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| String | szDevice | デバイス名 | Input |
| Long | lData | 設定データ | Input |

**Visual C++**

```
lRet = object.SetDevice(szDevice, lData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| CString | szDevice | デバイス名 | Input |
| Long | lData | 設定データ | Input |

**Visual Basic .NET**

```
IRet = object.SetDevice(szDevice, iData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| String | szDevice | デバイス名 | Input |
| Integer | iData | 設定データ | Input |

**Visual C#**

```
iRet = object.SetDevice(szDevice, iData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |
| String | szDevice | デバイス名 | Input |
| int | iData | 設定データ | Input |

#### 書式(オブジェクトを生成して使用する場合) (11.3 / 439 / 原本 p.441)

**Visual C++**

```
hResult = object.SetDevice(szDevice, lData, *lplRetCode)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| HRESULT | hResult | COMの戻り値 | Output |
| BSTR | szDevice | デバイス名 | Input |
| LONG | lData | 設定データ | Input |
| LONG | *lplRetCode | 通信関数の戻り値 | Output |

#### 戻り値 (11.3 / 440 / 原本 p.442)

正常終了: 0を返します。  
異常終了: 0以外を返します。(☞617ページ エラーコード)

#### 説明 (11.3 / 440 / 原本 p.442)

- szDeviceにて指定したデバイス1点に対してlData(iData)で指定する操作を行います。
- ビットデバイス設定時は，lData値(varData値またはiData値)の最下位のビットが有効となります。
- グローバルラベルにアクセスする場合は，szDeviceにグローバルラベルを指定してください。また，使用可能なグローバルラベルのデータ型および指定点数については下記を参照してください。
  ☞22ページ グローバルラベル名を指定したデータ取得

> **Point**
> - RnSFCPUのセーフティモードで安全デバイスに対して実行した場合は，エラーコード"0x010A42A5"(セーフティモードでは実施できない操作を行った)が返されます。
> - インバータ通信/ロボットコントローラ通信時は使用できません。

#### デバイス指定方法 (11.3 / 440 / 原本 p.442)

デバイスの指定方法を下記に示します。

##### ビットデバイス指定時 (11.3 / 440 / 原本 p.442)

(例) M0

| 上位2バイト | 下位2バイト |
|---|---|
| 使用しません。(0が格納されます。) | M0 |

##### ワードデバイス指定時 (11.3 / 440 / 原本 p.442)

(例) D0

| 上位2バイト | 下位2バイト |
|---|---|
| 使用しません。(0が格納されます。) | D0 |

##### ダブルワードデバイス指定時 (11.3 / 440 / 原本 p.442)

(例) LTN0

| 上位2バイト | 下位2バイト |
|---|---|
| LTN0のH | LTN0のL |

##### ダブルワードデバイス指定時(桁指定) (11.3 / 440 / 原本 p.442)

(例) K8M0

| 上位2バイト | 下位2バイト |
|---|---|
| M16～M31*1 | M0～M15*1 |

> *1 デバイスの番号順に，下位ビットから格納されます。

##### FXCPUのCN200以降指定時 (11.3 / 440 / 原本 p.442)

(例) CN200

| 上位2バイト | 下位2バイト |
|---|---|
| CN200のH | CN200のL |

##### ゲートウェイデバイス指定時 (11.3 / 440 / 原本 p.442)

(例) EG0に8ビットデバイス(シャープ社製シーケンサのE0000，E0001)が割り付けられている場合

| 上位2バイト | 下位2バイト |
|---|---|
| 使用しません。(0が格納されます。) | EG0 |
| (同上) | (E0001)(上位8ビット) / (E0000)(下位8ビット) |

### GetDevice(デバイスデータの取得) (11.3 / 441-443 / 原本 p.443-445)

#### 使用可能コントロール (11.3 / 441 / 原本 p.443)

下記のコントロールで使用可能です。

- 32ビット用: ActProgType，ActUtlType
- 64ビット用: ActProgType64，ActUtlType64

#### 機能 (11.3 / 441 / 原本 p.443)

デバイス1点のデータを取得します。  
インバータ/ロボットコントローラのモニタタイプ1点のデータを取得します。

#### 書式 (11.3 / 441 / 原本 p.443)

**VBA**

```
lRet = object.GetDevice(szDevice, lData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| String | szDevice | デバイス名/モニタタイプ | Input |
| Long | lData | 取得データ | Output |

**Visual C++**

```
lRet = object.GetDevice(szDevice, *lplData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| CString | szDevice | デバイス名/モニタタイプ | Input |
| Long | *lplData | 取得データ | Output |

**Visual Basic .NET**

```
IRet = object.GetDevice(szDevice, iData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| String | szDevice | デバイス名/モニタタイプ | Input |
| Integer | iData | 取得データ | Output |

**Visual C#**

```
iRet = object.GetDevice(szDevice, out iData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |
| String | szDevice | デバイス名/モニタタイプ | Input |
| int | iData | 取得データ | Output |

#### 書式(オブジェクトを生成して使用する場合) (11.3 / 441 / 原本 p.443)

**Visual C++**

```
hResult = object.GetDevice(szDevice, *lplData, *lplRetCode)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| HRESULT | hResult | COMの戻り値 | Output |
| BSTR | szDevice | デバイス名/モニタタイプ | Input |
| LONG | *lplData | 取得データ | Output |
| LONG | *lplRetCode | 通信関数の戻り値 | Output |

#### 戻り値 (11.3 / 442 / 原本 p.444)

正常終了: 0を返します。  
異常終了: 0以外を返します。(☞617ページ エラーコード)

#### 説明 (11.3 / 442 / 原本 p.444)

- szDeviceにて指定した1点のデバイスのデータを，lData(lplDataまたはiData)に格納します。
- モニタ可能な項目(モニタタイプ)は，下記を参照してください。
  ☞160ページ アクセス可能デバイスおよびデバイスタイプ
- グローバルラベルにアクセスする場合は，szDeviceにグローバルラベルを指定してください。また，使用可能なグローバルラベルのデータ型および指定点数については下記を参照してください。
  ☞22ページ グローバルラベル名を指定したデータ取得

#### デバイス指定方法 (11.3 / 442-443 / 原本 p.444-445)

デバイス/モニタタイプの指定方法を下記に示します。

##### ビットデバイス指定時 (11.3 / 442 / 原本 p.444)

(例) M0

| 上位2バイト | 下位2バイト |
|---|---|
| 使用しません。(0が格納されます。) | M0 |

##### ワードデバイス指定時 (11.3 / 442 / 原本 p.444)

(例) D0

| 上位2バイト | 下位2バイト |
|---|---|
| 使用しません。(0が格納されます。) | D0 |

##### ダブルワードデバイス指定時 (11.3 / 442 / 原本 p.444)

(例) LTN0

| 上位2バイト | 下位2バイト |
|---|---|
| LTN0のH | LTN0のL |

##### ダブルワードデバイス指定時(桁指定) (11.3 / 442 / 原本 p.444)

(例) K8M0

| 上位2バイト | 下位2バイト |
|---|---|
| M16～M31*1 | M0～M15*1 |

> *1 デバイスの番号順に，下位ビットから格納されます。

##### FXCPUのCN200以降指定時 (11.3 / 443 / 原本 p.445)

(例) CN200

| 上位2バイト | 下位2バイト |
|---|---|
| CN200のH | CN200のL |

##### ゲートウェイデバイス指定時 (11.3 / 443 / 原本 p.445)

(例) EG0に8ビットデバイス(シャープ社製シーケンサのE0000，E0001)が割り付けられている場合

| 上位2バイト | 下位2バイト |
|---|---|
| 使用しません。(0が格納されます。) | EG0 |
| (同上) | (E0001)(上位8ビット) / (E0000)(下位8ビット) |

##### インバータのモニタタイプ指定時 (11.3 / 443 / 原本 p.445)

(例) 2

| 上位2バイト | 下位2バイト |
|---|---|
| 1のH | 1のL |

※要確認: 例は「2」だが表は「1のH / 1のL」(原本表記のまま)。

##### ロボットコントローラのモニタタイプ指定時 (11.3 / 443 / 原本 p.445)

形式: (要求ID).(データタイプ).(引数)  
(例) 223.102.A

| 上位2バイト | 下位2バイト |
|---|---|
| 223.102.AのH | 223.102.AのL |
