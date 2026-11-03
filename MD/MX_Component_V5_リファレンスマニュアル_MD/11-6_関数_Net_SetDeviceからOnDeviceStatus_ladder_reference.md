# MX Component Version 5 リファレンスマニュアル 11章 関数 (6/8) p.542-567

| 項目 | 内容 |
|---|---|
| 原本 | 【三菱】MX Component Version 5 リファレンスマニュアル (SH-082394J) |
| メーカー | 三菱電機 |
| 原本ファイル | `PDF/【三菱】MX Component Version 5 リファレンスマニュアル_sh082394j.pdf` (全696ページ) |
| 本ファイルの範囲 | 11.5 関数の詳細(.Netコントロール用) のうち SetDevice〜OnDeviceStatus (印刷ページ 540-565 / PDF p.542-567) |
| 出典表記 | `(節 / 印刷ページ / 原本 p.PDFページ)` |
| 作成日 | 2026-11-03 |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。
> 本文中の「○ページ」はすべて原本の**印刷ページ番号**です(PDFページ = 印刷ページ + 2)。
> 書式中の引数名の大文字/小文字(例: VBの `IRet` / `lData` / `ICpuType` / `IOperation`)は原本表記のまま。原本には本範囲の関数のプログラム例(コード)の掲載はなく，書式行とラベル/デバイス設定例のみ。

## 主要用語 対訳表 (Glossary)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| デバイスデータの設定 | Set device data | SetDevice | 参考訳 |
| デバイスデータの取得 | Get device data | GetDevice | 参考訳 |
| バッファメモリ読出し / 書込み | Read / Write buffer memory | ReadBuffer / WriteBuffer | 参考訳 |
| 時計データ読出し / 書込み | Read / Write clock data | GetClockData / SetClockData | 参考訳 |
| CPUユニット形名読出し | Read CPU module model name | GetCpuType | 参考訳 |
| リモートコントロール | Remote control | SetCpuStatus | 参考訳 |
| デバイスの状態監視登録 / 登録解除 | Register / Deregister device status monitor | EntryDeviceStatus / FreeDeviceStatus | 参考訳 |
| イベント告知 | Event notification | OnDeviceStatus | 参考訳 |
| 戻り値 | Return value | IRet / iRet | 参考訳 |
| ラベル名 | Label name | szLabel | 参考訳 |
| 登録ラベル名リスト | Registered label name list | szLabelList | 参考訳 |
| 書き込むデバイス値 / 読み出したデバイス値 | Device value to write / Read device value | iData | 参考訳 |
| システムラベル | System label | Ver.1 / Ver.2 | 参考訳 |
| ラベルメモリ | Label memory | — | 参考訳 |
| 型分類 / 配列要素 / 構造体メンバ | Type class / Array element / Structure member | — | 参考訳 |
| 桁指定 / インデックス修飾 | Digit specification / Index modification | — | 参考訳 |
| セーフティモード / 安全デバイス | Safety mode / Safety device | RnSFCPU | 参考訳 |
| インテリジェント機能ユニット | Intelligent function module | — | 参考訳 |
| ユニットのI/O番号(先頭I/O番号) | Module I/O number (start I/O number) | iStartIO | 参考訳 |
| バッファメモリのアドレス | Buffer memory address | iAddress | 参考訳 |
| 読み出すサイズ / 書き込むサイズ | Read size / Write size | iReadSize / iWriteSize | 参考訳 |
| 特殊増設機器のブロックNo. | Special extension unit block No. | 0～7 | 参考訳 |
| 共有メモリ | Shared memory | QCPU(Qモード) | 参考訳 |
| 時計データ | Clock data | sYear〜sSecond | 参考訳 |
| 曜日 | Day of week | sDayOfWeek (0〜6) | 参考訳 |
| 形名文字列 / 形名コード | Model name string / Model code | szCpuName / iCpuType | 参考訳 |
| リモートRUN/STOP/PAUSE/RESET | Remote RUN/STOP/PAUSE/RESET | iOperation 0〜3 | 参考訳 |
| 自ボードアクセス | Own board access | — | 参考訳 |
| ユーザ認証機能 | User authentication function | MXコントローラ | 参考訳 |
| 登録デバイス点数 | Number of registered devices | iSize (最大20点) | 参考訳 |
| 状態監視間隔時間 | Status monitor interval time | iMonitorCycle (1～3600秒) | 参考訳 |
| 登録デバイス値リスト | Registered device value list | iData | 参考訳 |
| イベントハンドラ | Event handler | AddHandler / RemoveHandler / += / -= | 参考訳 |
| イベントの発生元 / イベントのデータ | Event source / Event data | sender / e | 参考訳 |
| 条件チェック処理の戻り値 | Return value of condition check | e.lReturnCode | 参考訳 |

## 変換範囲表

| 原本ページ(PDF) | 印刷ページ | 節 | 扱い |
|---|---|---|---|
| p.542-545 | 540-543 | 11.5 SetDevice(デバイスデータの設定) | 全文 |
| p.546-549 | 544-547 | 11.5 GetDevice(デバイスデータの取得) | 全文 |
| p.550-551 | 548-549 | 11.5 ReadBuffer(バッファメモリ読出し) | 全文 |
| p.552-553 | 550-551 | 11.5 WriteBuffer(バッファメモリ書込み) | 全文 |
| p.554-555 | 552-553 | 11.5 GetClockData(時計データ読出し) | 全文 |
| p.556-557 | 554-555 | 11.5 SetClockData(時計データ書込み) | 全文 |
| p.558 | 556 | 11.5 GetCpuType(CPUユニット形名読出し) | 全文 |
| p.559-560 | 557-558 | 11.5 SetCpuStatus(リモートコントロール) | 全文 |
| p.561-564 | 559-562 | 11.5 EntryDeviceStatus(デバイスの状態監視登録) | 全文(シーケンス図は文章化) |
| p.565 | 563 | 11.5 FreeDeviceStatus(デバイスの状態監視登録解除) | 全文 |
| p.566-567 | 564-565 | 11.5 OnDeviceStatus(イベント告知) | 全文 |
| p.418-541，p.568-604 | 416-539，566-602 | 11章の他の範囲 | 別ファイル(11-1〜11-5，11-7，11-8) |
| p.1-417，p.605-696 | — | 11章以外 | 別ファイル(01_〜10-9_)または**未変換** |

## 目次

- SetDevice(デバイスデータの設定)
- GetDevice(デバイスデータの取得)
- ReadBuffer(バッファメモリ読出し)
- WriteBuffer(バッファメモリ書込み)
- GetClockData(時計データ読出し)
- SetClockData(時計データ書込み)
- GetCpuType(CPUユニット形名読出し)
- SetCpuStatus(リモートコントロール)
- EntryDeviceStatus(デバイスの状態監視登録)
- FreeDeviceStatus(デバイスの状態監視登録解除)
- OnDeviceStatus(イベント告知)

---

## SetDevice(デバイスデータの設定) (11.5 / 540-543 / 原本 p.542-545)

**使用可能コントロール**

下記のコントロールで使用可能です。

- 32ビット用: DotUtlType
- 64ビット用: DotUtlType64

**機能**

デバイス1点の設定を行います。

**書式**

■Visual Basic .NET

```vb
IRet = object.SetDevice(szLabel, iData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| String | szLabel | ラベル名 | Input |
| Integer | iData | 書き込むデバイス値 | Input |

■Visual C#

```csharp
iRet = object.SetDevice(ref szLabel, iData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |
| String | szLabel | ラベル名 | Input |
| int | iData | 書き込むデバイス値 | Input |

**戻り値**

正常終了: 0を返します。
異常終了: 0以外を返します。(☞617ページ エラーコード)

**説明**

- ラベル名szLabelで指定したデバイス1点に対して，書き込むデバイス値iDataの値を書き込みます。
- ビットデバイス設定時は，書き込むデバイス値iDataの最下位のビットが有効となります。

> **Point**
> - ラベル名に対応するデバイスが存在しない場合はエラーとなり，書き込めません。
> - ダブルワードデバイスを指定した場合，ダブルワード型で2ワード書き込みます。
>   2ワード以上になるデータ型にダブルワードデバイス以外を指定した場合，本関数では下位1ワード(2バイト)分のデータに書込みを行います。(上位2バイトの値は保証できません。)
>   2ワード分以上のデバイスを書き込む場合は，WriteDeviceRandom関数を使用してください。
> - システムラベルVer.2でデバイスを指定せずラベルメモリを使用する場合はワード2点の扱いになります。
> - ビットデバイスの桁指定およびインデックス修飾は，使用できません。
> - RnSFCPUのセーフティモードで安全デバイスに対して実行した場合は，エラーコード"0x010A42A5"(セーフティモードでは実施できない操作を行った)が返されます。

#### ラベル指定方法 (11.5 / 541 / 原本 p.543)

ラベルの指定方法を，下記に示します。
システムラベル名には下記の型分類，配列要素，ラベルのデータ型を指定できます。
プログラム内でシステムラベル名を指定する場合，下記の書式を使用してください。
○: 指定可，×: 指定不可，—: 該当なし

| ラベル管理ユーティリティ上でのラベル定義: 型分類 | 配列要素 | プログラム内でのラベル指定方法: ラベル名の書式 | 指定可否 | データ型 |
|---|---|---|---|---|
| 基本データ | なし | システムラベル名 | ○ | Integer/int (32ビット値) |
| 基本データ | 要素数(1次元) | システムラベル名 | × | — |
| 基本データ | 要素数(1次元) | システムラベル名[n1] | ○ | Integer/int (32ビット値) |
| 基本データ | 要素数(2次元) | システムラベル名 | × | — |
| 基本データ | 要素数(2次元) | システムラベル名[n1][n2] | ○ | Integer/int (32ビット値) |
| 基本データ | 要素数(3次元) | システムラベル名 | × | — |
| 基本データ | 要素数(3次元) | システムラベル名[n1][n2][n3] | ○ | Integer/int (32ビット値) |
| 構造体 | なし | システムラベル名 | × | — |
| 構造体 | なし | システムラベル名.構造体メンバ名 | ○ | Integer/int (32ビット値) |
| 構造体 | 要素数(1次元) | システムラベル名 | × | — |
| 構造体 | 要素数(1次元) | システムラベル名[n1] | × | — |
| 構造体 | 要素数(1次元) | システムラベル名[n1].構造体メンバ名 | ○ | Integer/int (32ビット値) |
| 構造体 | 要素数(2次元) | システムラベル名 | × | — |
| 構造体 | 要素数(2次元) | システムラベル名[n1][n2] | × | — |
| 構造体 | 要素数(2次元) | システムラベル名[n1][n2].構造体メンバ名 | ○ | Integer/int (32ビット値) |
| 構造体 | 要素数(3次元) | システムラベル名 | × | — |
| 構造体 | 要素数(3次元) | システムラベル名[n1][n2][n3] | × | — |
| 構造体 | 要素数(3次元) | システムラベル名[n1][n2][n3].構造体メンバ名 | ○ | Integer/int (32ビット値) |

#### データ型 (11.5 / 541 / 原本 p.543)

ラベルには，下記のデータ型が指定できます。

ビット，ワード(符号付き)，ダブルワード(符号付き)*1，ワード(符号なし)，ダブルワード(符号なし)*1，単精度実数*1，倍精度実数*1，文字列*1，文字列[Unicode]*1*2，時間*1，タイマ，タイマ(符号なし)，ロングタイマ*2，カウンタ，カウンタ(符号なし)，ロングカウンタ*2，積算タイマ，積算タイマ(符号なし)，ロング積算タイマ*2

> *1 先頭デバイスの下位2バイトのみ書き込めます。2ワード分以上のデバイスを書き込む場合はWriteDeviceRandom関数を使用してください。
> *2 システムラベルVer.1の場合は使用できません。

#### デバイス指定方法 (11.5 / 542-543 / 原本 p.544-545)

書き込むデバイス値は，下記のように設定してください。

##### ビットデバイス指定時 (11.5 / 542 / 原本 p.544)

(例) M0を書き込む。

- ラベル設定

| szLabel | ラベル名 | データ型 | デバイス |
|---|---|---|---|
| [0] | LABEL | ビット | M0 |

- 書込み点数: 1
- 書き込むデバイス値

| 上位2バイト | 下位2バイト | 対応ラベル |
|---|---|---|
| 使用しません。(0が格納されます。) | M0 | LABEL |

##### ワードデバイス指定時 (11.5 / 542 / 原本 p.544)

(例) D0を書き込む。

- ラベル設定

| szLabel | ラベル名 | データ型 | デバイス |
|---|---|---|---|
| [0] | LABEL | ワード | D0 |

- 書込み点数: 1
- 書き込むデバイス値

| 上位2バイト | 下位2バイト | 対応ラベル |
|---|---|---|
| 使用しません。(0が格納されます。) | D0 | LABEL |

##### ダブルワード指定時(1点で2ワード書き込みできるダブルワードデバイスの場合) (11.5 / 542 / 原本 p.544)

(例) CN200を書き込む。
FXCPUのCN200以降は，4バイト書き込みます。

- ラベル設定

| szLabel | ラベル名 | データ型 | デバイス |
|---|---|---|---|
| [0] | LABEL | ダブルワード | CN200 |

- 書込み点数: 1
- 書き込むデバイス値

| 上位2バイト | 下位2バイト | 対応ラベル |
|---|---|---|
| CN200のH | CN200のL | LABEL |

##### ダブルワード指定時(1点で2ワード書き込みできないデバイスの場合) (11.5 / 543 / 原本 p.545)

(例) D0を指定して書き込む。

- ラベル設定

| szLabel | ラベル名 | データ型 | デバイス |
|---|---|---|---|
| [0] | LABELW | ダブルワード | D0 |

- 書込み点数: 1
- 書き込むデバイス値

| 上位2バイト | 下位2バイト | 対応ラベル |
|---|---|---|
| 使用しません。 | D0*1 | LABELW |

> *1 下位から順に2バイト書き込みます。システムラベルVer.2の場合は上位2バイトは不定値となります。

##### ラベルで2ワード以上に相当するデータ型指定時 (11.5 / 543 / 原本 p.545)

(例) 文字列型ラベルを指定して書き込む。

- ラベル設定

| szLabel | ラベル名 | データ型 | デバイス |
|---|---|---|---|
| [0] | LABEL | 文字列 | D0 |

- 書込み点数: 1
- 書き込むデバイス値

| 上位2バイト | 下位2バイト | 対応ラベル |
|---|---|---|
| 使用しません。 | D0*1 | LABEL |

> *1 下位から順に2バイト書き込みます。システムラベルVer.2の場合は上位2バイトは不定値となります。

---

## GetDevice(デバイスデータの取得) (11.5 / 544-547 / 原本 p.546-549)

**使用可能コントロール**

下記のコントロールで使用可能です。

- 32ビット用: DotUtlType
- 64ビット用: DotUtlType64

**機能**

デバイス1点のデータを取得します。

**書式**

■Visual Basic .NET

```vb
IRet = object.GetDevice(szLabel, lData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| String | szLabel | ラベル名 | Input |
| Integer | iData | 読み出したデバイス値 | Output |

※VB書式行の第2引数は原本表記「lData」，引数表は「iData」(原本どおり)。

■Visual C#

```csharp
iRet = object.GetDevice(ref szLabel, ref iData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |
| String | szLabel | ラベル名 | Input |
| int | iData | 読み出したデバイス値 | Output |

**戻り値**

正常終了: 0を返します。
異常終了: 0以外を返します。(☞617ページ エラーコード)

**説明**

- ラベル名szLabelで指定したデバイス1点のデータを，読み出したデバイス値iDataに格納します。

> **Point**
> - ラベル名に対応するデバイスが存在しない場合はエラーとなり，読み出せません。
> - 読み出したデバイス値には，4バイトのメモリエリアを用意してください。メモリエリアがない場合は，アプリケーションエラーなどの重大な現象が発生するおそれがあります。
> - ビットデバイスの桁指定およびインデックス修飾は，使用できません。

#### ラベル指定方法 (11.5 / 545 / 原本 p.547)

ラベルの指定方法を，下記に示します。
システムラベル名には下記の型分類，配列要素，ラベルのデータ型を指定できます。
プログラム内でシステムラベル名を指定する場合，下記の書式を使用してください。
○: 指定可，×: 指定不可，—: 該当なし

| ラベル管理ユーティリティ上でのラベル定義: 型分類 | 配列要素 | プログラム内でのラベル指定方法: ラベル名の書式 | 指定可否 | データ型 |
|---|---|---|---|---|
| 基本データ | なし | システムラベル名 | ○ | Integer/int (32ビット値) |
| 基本データ | 要素数(1次元) | システムラベル名 | × | — |
| 基本データ | 要素数(1次元) | システムラベル名[n1] | ○ | Integer/int (32ビット値) |
| 基本データ | 要素数(2次元) | システムラベル名 | × | — |
| 基本データ | 要素数(2次元) | システムラベル名[n1][n2] | ○ | Integer/int (32ビット値) |
| 基本データ | 要素数(3次元) | システムラベル名 | × | — |
| 基本データ | 要素数(3次元) | システムラベル名[n1][n2][n3] | ○ | Integer/int (32ビット値) |
| 構造体 | なし | システムラベル名 | × | — |
| 構造体 | なし | システムラベル名.構造体メンバ名 | ○ | Integer/int (32ビット値) |
| 構造体 | 要素数(1次元) | システムラベル名 | × | — |
| 構造体 | 要素数(1次元) | システムラベル名[n1] | × | — |
| 構造体 | 要素数(1次元) | システムラベル名[n1].構造体メンバ名 | ○ | Integer/int (32ビット値) |
| 構造体 | 要素数(2次元) | システムラベル名 | × | — |
| 構造体 | 要素数(2次元) | システムラベル名[n1][n2] | × | — |
| 構造体 | 要素数(2次元) | システムラベル名[n1][n2].構造体メンバ名 | ○ | Integer/int (32ビット値) |
| 構造体 | 要素数(3次元) | システムラベル名 | × | — |
| 構造体 | 要素数(3次元) | システムラベル名[n1][n2][n3] | × | — |
| 構造体 | 要素数(3次元) | システムラベル名[n1][n2][n3].構造体メンバ名 | ○ | Integer/int (32ビット値) |

#### データ型 (11.5 / 545 / 原本 p.547)

ラベルには，下記のデータ型が指定できます。

ビット，ワード(符号付き)，ダブルワード(符号付き)*1，ワード(符号なし)，ダブルワード(符号なし)*1，単精度実数*1，倍精度実数*1，文字列*1，文字列[Unicode]*1*2，時間*1，タイマ，タイマ(符号なし)，ロングタイマ*2，カウンタ，カウンタ(符号なし)，ロングカウンタ*2，積算タイマ，積算タイマ(符号なし)，ロング積算タイマ*2

> *1 先頭デバイスの下位2バイトのみ読み出せます。
> 2ワード分以上のデバイスを読み出す場合はReadDeviceRandom関数を使用してください。
> ただし1点で取得可能なダブルワードデバイスを指定した場合は，ダブルワード型で上位2バイトも読み出されます。
> *2 システムラベルVer.1の場合は使用できません。

#### デバイス指定方法 (11.5 / 546-547 / 原本 p.548-549)

読み出したデバイス値は，下記のように格納されます。

##### ビットデバイス指定時 (11.5 / 546 / 原本 p.548)

(例) M0を読み出す。

- ラベル設定

| szLabel | ラベル名 | データ型 | デバイス |
|---|---|---|---|
| [0] | LABEL | ビット | M0 |

- 読出し点数: 1
- 読み出したデバイス値

| 上位2バイト | 下位2バイト | 対応ラベル |
|---|---|---|
| 使用しません。(0が格納されます。) | M0*1 | LABEL |

> *1 読み出すデバイスは「M0」1点のみを対象とし，デバイス値は「0」または「1」が格納されます。

##### ワードデバイス指定時 (11.5 / 546 / 原本 p.548)

(例) D0を読み出す。

- ラベル設定

| szLabel | ラベル名 | データ型 | デバイス |
|---|---|---|---|
| [0] | LABEL | ワード | D0 |

- 読出し点数: 1
- 読み出したデバイス値

| 上位2バイト | 下位2バイト | 対応ラベル |
|---|---|---|
| 使用しません。(0が格納されます。) | D0 | LABEL |

##### ダブルワード指定時(1点で2ワード読み出せるダブルワードデバイスの場合) (11.5 / 546 / 原本 p.548)

(例) CN200を読み出す。

- ラベル設定

| szLabel | ラベル名 | データ型 | デバイス |
|---|---|---|---|
| [0] | LABEL | ダブルワード | CN200 |

- 読出し点数: 1
- 読み出したデバイス値

| 上位2バイト | 下位2バイト | 対応ラベル |
|---|---|---|
| CN200のH | CN200のL*1 | LABEL |

> *1 FXCPUのCN200以降は，4バイト読み出します。

##### ダブルワード指定時(1点で2ワード読み出せないデバイスの場合) (11.5 / 546 / 原本 p.548)

(例) D0を指定して読み出す。

- ラベル設定

| szLabel | ラベル名 | データ型 | デバイス |
|---|---|---|---|
| [0] | LABELW | ダブルワード | D0 |

- 読出し点数: 1
- 読み出したデバイス値

| 上位2バイト | 下位2バイト | 対応ラベル |
|---|---|---|
| 使用しません。(0が格納されます。) | D0*1 | LABELW |

> *1 下位から順に2バイト読み出します。

##### ラベルで2ワード以上に相当するデータ型指定時 (11.5 / 547 / 原本 p.549)

(例) 文字列型ラベルを指定して読み出す。

- ラベル設定

| szLabel | ラベル名 | データ型 | デバイス |
|---|---|---|---|
| [0] | LABEL | 文字列 | D0 |

- 読出し点数: 1
- 読み出したデバイス値

| 上位2バイト | 下位2バイト | 対応ラベル |
|---|---|---|
| 使用しません。(0が格納されます。) | D0*1 | LABEL |

> *1 下位から順に2バイト読み出します。

---

## ReadBuffer(バッファメモリ読出し) (11.5 / 548-549 / 原本 p.550-551)

**使用可能コントロール**

下記のコントロールで使用可能です。

- 32ビット用: DotUtlType
- 64ビット用: DotUtlType64

**機能**

インテリジェント機能ユニットのバッファメモリの値を読み出します。

**書式**

■Visual Basic .NET

```vb
IRet = object.ReadBuffer(iStartIO, iAddress, iReadSize, sData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| Integer | iStartIO | 値を読み出すユニットのI/O番号 | Input |
| Integer | iAddress | バッファメモリのアドレス | Input |
| Integer | iReadSize | 読み出すサイズ | Input |
| Short | sData(n) | バッファメモリから読み出した値 | Output |

■Visual C#

```csharp
iRet = object.ReadBuffer(iStartIO, iAddress, iReadSize, sData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |
| int | iStartIO | 値を読み出すユニットのI/O番号 | Input |
| int | iAddress | バッファメモリのアドレス | Input |
| int | iReadSize | 読み出すサイズ | Input |
| short[n] | sData | バッファメモリから読み出した値 | Output |

**戻り値**

正常終了: 0を返します。
異常終了: 0以外を返します。(☞617ページ エラーコード)

**説明** (11.5 / 549 / 原本 p.551)

- iStartIOに指定するユニットのI/O番号は，実際のI/O番号を16で割った値を指定してください。
  FX5CPUの場合は，対象局側のユニット番号を指定してください。
- iStartIOに指定した先頭I/O番号に位置するインテリジェント機能ユニットの，iAddressに指定されたバッファメモリアドレスのバッファ値をiReadSize分読み出します。
- 接続局がFXCPUのCPU COM通信およびGX Simulator2通信を行う場合，ユニット先頭I/O番号には，特殊増設機器のブロックNo.(0～7)を，バッファメモリアドレスには0～32767を指定してください。
- sDataは，iReadSize以上の配列を確保してください。

> **Point**
> - RモーションCPUおよびQモーションCPUへアクセスを行うと，エラーが返ります。
> - iDataは，iReadSizeに指定した点数分のメモリエリアを用意してください。 メモリエリアがない場合は，アプリケーションエラーなど重大な現象が発生するおそれがあります。
> - QCPU(Qモード)に対してバッファメモリ読出し(ReadBuffer)を行う場合，Qシリーズ専用ユニットにしか読出し操作を行うことができません。また，QCPU(Qモード)の共有メモリからの読出し操作も行うことができません。

※Point 2項目めの「iData」は原本表記のまま(書式上の引数名はsData)。要確認。

**通信経路の使用可否**

下記を参照ください。
☞446ページ 通信経路の使用可否

---

## WriteBuffer(バッファメモリ書込み) (11.5 / 550-551 / 原本 p.552-553)

**使用可能コントロール**

下記のコントロールで使用可能です。

- 32ビット用: DotUtlType
- 64ビット用: DotUtlType64

**機能**

インテリジェント機能ユニットのバッファメモリの値を書き込みます。

**書式**

■Visual Basic .NET

```vb
IRet = object.WriteBuffer(iStartIO, iAddress, iWriteSize, sData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| Integer | iStartIO | 値を書き込むユニットのI/O番号 | Input |
| Integer | iAddress | バッファメモリのアドレス | Input |
| Integer | iWriteSize | 書き込むサイズ | Input |
| Short | sData(n) | バッファメモリに書き込む値 | Input |

■Visual C#

```csharp
iRet = object. WriteBuffer (iStartIO, iAddress, iWriteSize, sData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |
| int | iStartIO | 値を書き込むユニットのI/O番号 | Input |
| int | iAddress | バッファメモリのアドレス | Input |
| int | iWriteSize | 書き込むサイズ | Input |
| short[n] | sData | バッファメモリに書き込む値 | Input |

**戻り値**

正常終了: 0を返します。
異常終了: 0以外を返します。(☞617ページ エラーコード)

**説明** (11.5 / 551 / 原本 p.553)

- iStartIOに指定するユニットのI/O番号は，実際のI/O番号を16で割った値を指定してください。
  FX5CPUの場合は，対象局側のユニット番号を指定してください。
- iStartIOに指定した先頭I/O番号に位置するインテリジェント機能ユニットの，iAddressに指定されたバッファメモリアドレスのバッファ値をiWriteSize分書き込みます。
- 接続局がFXCPUのCPU COM通信およびGX Simulator2通信を行う場合，ユニット先頭I/O番号には，特殊増設機器のブロックNo.(0～7)を，バッファメモリアドレスには0～32767を指定してください。
- sDataは，iWriteSize以上の配列を確保してください。

> **Point**
> - RモーションCPUおよびQモーションCPUへアクセスを行うと，エラーが返ります。
> - sDataは，iReadSizeに指定した点数分のメモリエリアを用意してください。 メモリエリアがない場合は，アプリケーションエラーなど重大な現象が発生するおそれがあります。
> - QCPU(Qモード)に対してバッファメモリ読出し(ReadBuffer)を行う場合，Qシリーズ専用ユニットにしか読出し操作を行うことができません。また，QCPU(Qモード)の共有メモリからの読出し操作も行うことができません。

※Point 2項目めの「iReadSize」，3項目めの「バッファメモリ読出し(ReadBuffer)」「読出し操作」はWriteBufferのページでも原本表記のまま(ReadBufferからの流用と思われる)。要確認。

**通信経路の使用可否**

下記を参照ください。
☞450ページ 通信経路の使用可否

---

## GetClockData(時計データ読出し) (11.5 / 552-553 / 原本 p.554-555)

**使用可能コントロール**

下記のコントロールで使用可能です。

- 32ビット用: DotUtlType
- 64ビット用: DotUtlType64

**機能**

CPUユニットの時計データから時間を読み出します。

**書式**

■Visual Basic .NET

```vb
IRet = object.GetClockData(sYear, sMonth, sDay, sDayOfWeek, sHour, sMinute, sSecond)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| Short | sYear | 読み出した年の値 | Output |
| Short | sMonth | 読み出した月の値 | Output |
| Short | sDay | 読み出した日の値 | Output |
| Short | sDayOfWeek | 読み出した曜日の値 | Output |
| Short | sHour | 読み出した時間の値 | Output |
| Short | sMinute | 読み出した分の値 | Output |
| Short | sSecond | 読み出した秒の値 | Output |

■Visual C#

```csharp
hResult = object.GetClockData
(ref sYear, ref sMonth, ref sDay, ref sDayOfWeek,ref sHour, ref sMinute, ref sSecond)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |
| short | sYear | 読み出した年の値 | Output |
| short | sMonth | 読み出した月の値 | Output |
| short | sDay | 読み出した日の値 | Output |
| short | sDayOfWeek | 読み出した曜日の値 | Output |
| short | sHour | 読み出した時間の値 | Output |
| short | sMinute | 読み出した分の値 | Output |
| short | sSecond | 読み出した秒の値 | Output |

※C#書式行の戻り値の変数名は原本表記「hResult」，引数表は「iRet」(原本どおり)。

**戻り値**

正常終了: 0を返します。
異常終了: 0以外を返します。(☞617ページ エラーコード)

**説明** (11.5 / 553 / 原本 p.555)

- CPUユニットに正しい時計データが設定されていない場合，エラーが返ります。
- sYearに格納される値は，RCPUおよびQCPU(Qモード)は西暦4桁，それ以外のCPUは西暦下2桁が返ります。
  ただし，RCPUおよびQCPU(Qモード)は1980年から2079年までとなります。
- sDayOfWeekに格納される値は，下記のとおりです。

| 値 | 曜日 |
|---|---|
| 0 | 日曜日 |
| 1 | 月曜日 |
| 2 | 火曜日 |
| 3 | 水曜日 |
| 4 | 木曜日 |
| 5 | 金曜日 |
| 6 | 土曜日 |

> **Point**
> - RモーションCPUおよびQモーションCPUへアクセスを行うと，エラーが返ります。
> - FXCPUは，時計機能内蔵の機種で，時計データが読み出せます。
>   上記以外のFXCPUはエラーが返ります。
> - 時計設定は転送時間分の誤差が生じますのでご注意ください。
> - 通信経路の使用可否については，☞452ページ GetClockData(時計データ読出し)に記載の一覧表を参照してください。

**通信経路の使用可否**

下記を参照ください。
☞455ページ 通信経路の使用可否

---

## SetClockData(時計データ書込み) (11.5 / 554-555 / 原本 p.556-557)

**使用可能コントロール**

下記のコントロールで使用可能です。

- 32ビット用: DotUtlType
- 64ビット用: DotUtlType64

**機能**

CPUユニットの時計データへ時間を書き込みます。

**書式**

■Visual Basic .NET

```vb
IRet = object.SetClockData(sYear, sMonth, sDay, sDayOfWeek, sHour, sMinute, sSecond)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| Short | sYear | 書き込む年の値 | Input |
| Short | sMonth | 書き込む月の値 | Input |
| Short | sDay | 書き込む日の値 | Input |
| Short | sDayOfWeek | 書き込む曜日の値 | Input |
| Short | sHour | 書き込む時間の値 | Input |
| Short | sMinute | 書き込む分の値 | Input |
| Short | sSecond | 書き込む秒の値 | Input |

■Visual C#

```csharp
lRet = object.SetClockData(sYear, sMonth, sDay, sDayOfWeek, sHour, sMinute, sSecond)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |
| short | sYear | 書き込む年の値 | Input |
| short | sMonth | 書き込む月の値 | Input |
| short | sDay | 書き込む日の値 | Input |
| short | sDayOfWeek | 書き込む曜日の値 | Input |
| short | sHour | 書き込む時間の値 | Input |
| short | sMinute | 書き込む分の値 | Input |
| short | sSecond | 書き込む秒の値 | Input |

※C#書式行の戻り値の変数名は原本表記「lRet」，引数表は「iRet」(原本どおり)。

**戻り値**

正常終了: 0を返します。
異常終了: 0以外を返します。(☞617ページ エラーコード)

**説明** (11.5 / 555 / 原本 p.557)

- 設定する時計データが正しい値でない場合，エラーが返ります。
- sYearに指定した値は，RCPUおよびQCPU(Qモード)は西暦4桁，それ以外のCPUは西暦下2桁が有効となります。
  ただし，RCPUおよびQCPU(Qモード)は1980年から2079までとなります。
  RCPUおよびQCPU(Qモード)以外のCPUで4桁を設定した場合はエラーとなります。
- sDayOfWeekに指定する値は，下記のとおりです。

| 値 | 曜日 |
|---|---|
| 0 | 日曜日 |
| 1 | 月曜日 |
| 2 | 火曜日 |
| 3 | 水曜日 |
| 4 | 木曜日 |
| 5 | 金曜日 |
| 6 | 土曜日 |

> **Point**
> - RモーションCPUおよびQモーションCPUへアクセスを行うと，エラーが返ります。
> - FXCPUは，時計機能内蔵の機種で，時計データが書き込めます。
>   上記以外のFXCPUはエラーが返ります。
> - 時計設定は転送時間分の誤差が生じますのでご注意ください。
> - 通信経路の使用可否については，☞457ページ SetClockData(時計データ書込み)に記載の一覧表を参照してください。
> - 自ボードアクセス時はエラーが返ります。
> - ユーザ認証機能が有効なMXコントローラでは使用できません。

**通信経路の使用可否**

下記を参照ください。
☞459ページ 通信経路の使用可否

---

## GetCpuType(CPUユニット形名読出し) (11.5 / 556 / 原本 p.558)

**使用可能コントロール**

下記のコントロールで使用可能です。

- 32ビット用: DotUtlType
- 64ビット用: DotUtlType64

**機能**

CPUユニット，ネットワークボード，GOTの形名文字列および形名コード(16進)を読み出します。

**書式**

■Visual Basic .NET

```vb
IRet = object.GetCpuType(szCpuName, ICpuType)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| String | szCpuName | 形名文字列 | Output |
| Integer | ICpuType | 形名コード | Output |

■Visual C#

```csharp
iRet = object.GetCpuType (ref szCpuName, ref iCpuType)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |
| String | szCpuName | 形名文字列 | Output |
| int | iCpuType | 形名コード | Output |

**戻り値**

正常終了: 0を返します。
異常終了: 0以外を返します。(☞617ページ エラーコード)

**説明**

- 通信を行っているCPUユニットの形名文字列をszCpuNameに，形名コード(16進)をiCpuTypeに格納します。
- 形名文字列はUNICODEで返されます。
- 形名コードはユニット固有の値(16進)です。

---

## SetCpuStatus(リモートコントロール) (11.5 / 557-558 / 原本 p.559-560)

**使用可能コントロール**

下記のコントロールで使用可能です。

- 32ビット用: DotUtlType
- 64ビット用: DotUtlType64

**機能**

CPUユニットのリモート操作を行います。

**書式**

■Visual Basic .NET

```vb
IRet = object.SetCpuStatus(IOperation)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| Integer | IOperation | リモートRUN/STOP/PAUSE/RESET | Input |

■Visual C#

```csharp
iRet = object.SetCpuStatus (iOperation)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |
| int | iOperation | リモートRUN/STOP/PAUSE/RESET | Input |

**戻り値**

正常終了: 0を返します。
異常終了: 0以外を返します。(☞617ページ エラーコード)

**説明**

iOperationにて指定された操作を行います。
下記以外の値を指定するとエラーとなります。

| 値 | 操作 |
|---|---|
| 0 | リモートRUN |
| 1 | リモートSTOP |
| 2 | リモートPAUSE |
| 3 | リモートRESET |

> **Point**
> - FXCPUはCPUユニットとしてPAUSEスイッチを持たないため，SetCpuStatusでリモートPAUSEを指定するとエラーを返します。
> - QモーションCPUへアクセスし，PAUSEを指定するとエラーが返ります。
> - RモーションCPUへアクセスを行うと，エラーが返ります。
> - 通信経路の使用可否については，☞463ページ SetCpuStatus(リモートコントロール)に記載の一覧表を参照してください。
> - リモートRESETは，QCPU，LCPU，RCPU，LHCPU，およびFX5CPUでリモートRESETに対応している機種のみサポートしています。
> - ユーザ認証機能が有効なMXコントローラでは使用できません。

**通信経路の使用可否** (11.5 / 557-558 / 原本 p.559-560)

下記を参照ください。
☞464ページ 通信経路の使用可否

※参照先の行はページをまたいで原本 p.560 に1行だけ掲載。

---

## EntryDeviceStatus(デバイスの状態監視登録) (11.5 / 559-562 / 原本 p.561-564)

**使用可能コントロール**

下記のコントロールで使用可能です。

- 32ビット用: DotUtlType

**機能**

状態監視を行うデバイスを登録します。

**書式**

■Visual Basic .NET

```vb
IRet = object.EntryDeviceStatus(szLabelList, iSize, iMonitorCycle, iData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| String | szLabelList(n) | 登録ラベル名リスト | Input |
| Integer | iSize | 登録デバイス点数 | Input |
| Integer | iMonitorCycle | 状態監視間隔時間 | Input |
| Integer | iData(n) | 登録デバイス値リスト | Input |

■Visual C#

```csharp
iRet = object. EntryDeviceStatus(szLabelList, iSize, iMonitorCycle, iData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |
| System.String[n] | szLabelList | 登録ラベル名リスト | Input |
| int | iSize | 登録デバイス点数 | Input |
| int | iMonitorCycle | 状態監視間隔時間 | Input |
| int[n] | iData | 登録デバイス値リスト | Input |

**戻り値**

正常終了: 0を返します。
異常終了: 0以外を返します。(☞617ページ エラーコード)

**説明**

- szLabelListにて指定したiSize分のデバイス群が，iDataにて指定した状態であるかを確認します。確認時間はiMonitorCycleにて指定します。
  状態成立によりユーザプログラムのOnDeviceStatus関数を実行します。
- iSizeに指定できる最大デバイス点数は，20点です。
- iMonitorCycleは1秒～1時間の範囲(1～3600の秒単位で設定)で指定してください。
  これ以外の値を指定するとエラーとなります。
- 登録デバイス値リストを，iDataに格納します。

> **Point** (11.5 / 560 / 原本 p.562)
> - パソコン性能，実行中のアプリケーション負荷，シーケンサとの通信に要する時間などの条件により，指定の状態監視間隔時間に，デバイスの状態監視が行えない場合があります。
>   また，コントロールの他の関数を同時に使用する場合も，指定の状態監視間隔時間でデバイスの状態監視ができない原因になります。
> - iDataは，iSizeに指定した点数分のメモリエリアを用意してください。
>   メモリエリアがない場合は，アプリケーションエラーなど重大な現象が発生するおそれがあります。
> - 状態監視中にEntryDeviceStatusを実行した場合は，エラーとなります。
>   状態監視の条件を変更する場合は，FreeDeviceStatusを実行後，再度EntryDeviceStatusを実行してください。
> - 複数デバイスが同時に状態変化した場合は，状態変化したごとに，OnDeviceStatusイベントが実行されます。
>   (例: M0を監視している場合)
> - コントロールが定期的にデバイスランダム読出しを実行し，状態成立を確認する機能です。
>   したがって，CPUユニットがデバイスの状態成立をMX Componentに通知する機能ではありません。
>   そのため，指定の状態監視間隔時間によっては，コントロールがCPUユニットのデバイスの状態成立を確認できない場合があります。
> - ビットデバイスの桁指定およびインデックス修飾は，使用できません。

【図】状態監視のシーケンス(例: M0を監視している場合) (11.5 / 560 / 原本 p.562)
- 登場者: アプリケーション / MX Component / シーケンサ
- MX Component → シーケンサ: 「M0, M1読出し要求」，シーケンサ → MX Component: 「M0, M1の内容」を定期的に繰り返す(図中は「:」で繰り返しを表現)
- シーケンサで「M0 ON !」となった後の読出しで成立 → MX Component → アプリケーション: イベント通知（M0）→ アプリケーション側で「OnDeviceStatus イベント実行」
- その後シーケンサで「M0 OFF」→ さらに「M0, M1 ON !」となった後の読出しで，イベント通知（M0）とイベント通知（M1）が順に通知され，アプリケーション側で「OnDeviceStatus イベント実行」が2回行われる(状態変化したデバイスごとに1回)

#### ワードデバイスを状態監視する場合の注意事項 (11.5 / 560 / 原本 p.562)

ワードデバイスが負の値-1～-32768(FFFFH～8000H)になるのを状態監視する場合，EntryDeviceStatusの監視デバイス値は上位2バイトに「0」を格納した65535～32768(0000FFFFH～00008000H)を設定してください。
(例) D0が「-10」となるのを状態監視させる場合
「-10(FFFFFFF6H)」の上位2バイトに「0」を格納した値「65526(0000FFF6H)」を監視デバイス値に設定してください。
CPUユニットのワードデバイスがWORD型であるのに対し，EntryDeviceStatusの監視デバイス値の型はLONG型であるため，CPUユニットの現在値とEntryDeviceStatusの監視デバイス値を比較した場合，同じ値にはならず上記の設定が必要になります。(ビットデバイスおよびダブルワードデバイス使用時は，本注意事項は該当しません。)
本注意事項についてのプログラミング例は下記を参照してください。
☞670ページ ワードデバイスを状態監視する場合のプログラミング例

#### ラベル指定方法 (11.5 / 561 / 原本 p.563)

ラベルの指定方法を，下記に示します。
システムラベル名には下記の型分類，配列要素，ラベルのデータ型を指定できます。
プログラム内でシステムラベル名を指定する場合，下記の書式を使用してください。
○: 指定可，×: 指定不可，—: 該当なし

| ラベル管理ユーティリティ上でのラベル定義: 型分類 | 配列要素 | プログラム内でのラベル指定方法: ラベル名の書式 | 指定可否 | データ型 |
|---|---|---|---|---|
| 基本データ | なし | システムラベル名 | ○ | Integer/int (32ビット値) |
| 基本データ | 要素数(1次元) | システムラベル名 | × | — |
| 基本データ | 要素数(1次元) | システムラベル名[n1] | ○ | Integer/int (32ビット値) |
| 基本データ | 要素数(2次元) | システムラベル名 | × | — |
| 基本データ | 要素数(2次元) | システムラベル名[n1][n2] | ○ | Integer/int (32ビット値) |
| 基本データ | 要素数(3次元) | システムラベル名 | × | — |
| 基本データ | 要素数(3次元) | システムラベル名[n1][n2][n3] | ○ | Integer/int (32ビット値) |
| 構造体 | なし | システムラベル名 | × | — |
| 構造体 | なし | システムラベル名.構造体メンバ名 | ○ | Integer/int (32ビット値) |
| 構造体 | 要素数(1次元) | システムラベル名 | × | — |
| 構造体 | 要素数(1次元) | システムラベル名[n1] | × | — |
| 構造体 | 要素数(1次元) | システムラベル名[n1].構造体メンバ名 | ○ | Integer/int (32ビット値) |
| 構造体 | 要素数(2次元) | システムラベル名 | × | — |
| 構造体 | 要素数(2次元) | システムラベル名[n1][n2] | × | — |
| 構造体 | 要素数(2次元) | システムラベル名[n1][n2].構造体メンバ名 | ○ | Integer/int (32ビット値) |
| 構造体 | 要素数(3次元) | システムラベル名 | × | — |
| 構造体 | 要素数(3次元) | システムラベル名[n1][n2][n3] | × | — |
| 構造体 | 要素数(3次元) | システムラベル名[n1][n2][n3].構造体メンバ名 | ○ | Integer/int (32ビット値) |

#### データ型 (11.5 / 561 / 原本 p.563)

ラベルには，下記のデータ型が指定できます。

ビット，ワード(符号付き)，ワード(符号なし)

#### デバイス指定方法 (11.5 / 561-562 / 原本 p.563-564)

登録するデバイス値は，下記のように設定してください。

##### ビットデバイスおよびワードデバイス指定時 (11.5 / 561 / 原本 p.563)

(例) M0とD0を1点ずつ登録する。

- ラベル設定

| szLabelList | ラベル名 | データ型 | デバイス |
|---|---|---|---|
| [0] | LABEL1 | ビット | M0 |
| [1] | LABEL2 | ワード | D0 |

- 登録デバイス点数: 2
- 登録デバイス値

| 上位2バイト | 下位2バイト | 対応ラベル |
|---|---|---|
| 使用しません。(0が格納されます。) | M0 | LABEL1 |
| (同上) | D0 | LABEL2 |

※上位2バイト欄は原本では2行で結合。

##### FXCPUのCN200以降指定時 (11.5 / 562 / 原本 p.564)

(例) CN200を含めて3点登録する。

- ラベル設定

| szLabelList | ラベル名 | データ型 | デバイス |
|---|---|---|---|
| [0] | LABEL1 | ワード | D0 |
| [1] | LABEL2 | ワード | CN200 |
| [2] | LABEL3 | ワード | D1 |

- 登録デバイス点数: 3
- 登録デバイス値

| 上位2バイト | 下位2バイト | 対応ラベル |
|---|---|---|
| 使用しません。(0が格納されます。) | D0 | LABEL1 |
| CN200のH | CN200のL*1 | LABEL2 |
| 使用しません。(0が格納されます。) | D1 | LABEL3 |

> *1 FXCPUのCN200以降は，4バイト登録できます。

##### FDデバイス指定時(4ワードデバイス) (11.5 / 562 / 原本 p.564)

(例) FD0を含めて3点登録する。

- ラベル設定

| szLabelList | ラベル名 | データ型 | デバイス |
|---|---|---|---|
| [0] | LABEL1 | ワード | D0 |
| [1] | LABEL2 | ワード | FD0 |
| [2] | LABEL3 | ワード | D1 |

- 登録デバイス点数: 3
- 登録デバイス値

| 上位2バイト | 下位2バイト | 対応ラベル |
|---|---|---|
| 使用しません。(0が格納されます。) | D0 | LABEL1 |
| (同上) | FD0のLL*1 | LABEL2 |
| (同上) | D1 | LABEL3 |

※上位2バイト欄は原本では3行で結合。

> *1 下位2バイトのみ登録できます。指定デバイスのHH，HL，LH(上位6バイト)は登録できません。

---

## FreeDeviceStatus(デバイスの状態監視登録解除) (11.5 / 563 / 原本 p.565)

**使用可能コントロール**

下記のコントロールで使用可能です。

- 32ビット用: DotUtlType

**機能**

EntryDeviceStatusにて登録した，状態監視を行うデバイスを解除します。

**書式**

■Visual Basic .NET

```vb
IRet = object.FreeDeviceStatus()
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |

■Visual C#

```csharp
iRet = object. FreeDeviceStatus()
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |

**戻り値**

正常終了: 0を返します。
異常終了: 0以外を返します。(☞617ページ エラーコード)

**説明**

EntryDeviceStatus関数にて設定した状態監視を行うデバイスを解除します。

---

## OnDeviceStatus(イベント告知) (11.5 / 564-565 / 原本 p.566-567)

**使用可能コントロール**

下記のコントロールで使用可能です。

- 32ビット用: DotUtlType

**機能**

EntryDeviceStatus関数にて登録したデバイス条件が成立時に実行します。

**書式**

■Visual Basic .NET

- イベントハンドラの生成

```vb
AddHandler object.OnDeviceStatus, AddressOf object_OnDeviceStatus
```

- イベントハンドラ

```vb
Private Sub object_OnDeviceStatus(ByVal sender As System.Object,
ByVal e As MITSUBISHI.Component.DeviceStatusEventArgs)
```

| 引数 | 内容 | Input/Output |
|---|---|---|
| sender | イベントの発生元 | Output |
| e | イベントのデータ | Output |

eのメンバは下記のとおりです。

| メンバ | 内容 |
|---|---|
| e.szDevice | 条件成立したラベル名 |
| e.lData | 条件成立したデバイス値 |
| e.lReturnCode | 条件チェック処理の戻り値 |

- イベントハンドラの削除

```vb
RemoveHandler object.OnDeviceStatus, AddressOf object_OnDeviceStatus
```

■Visual C#

- イベントハンドラの生成

```csharp
object.OnDeviceStatus += new MITSUBISHI.Component.DotUtlType.DeviceStatusEventHandler (object_OnDeviceStatus);
```

- イベントハンドラ

```csharp
private void object_OnDeviceStatus(object sender, MITSUBISHI.Component.DeviceStatusEventArgs e)
```

| 引数 | 内容 | Input/Output |
|---|---|---|
| sender | イベントの発生元 | Output |
| e | イベントのデータ | Output |

eのメンバは下記のとおりです。

| メンバ | 内容 |
|---|---|
| e.szDevice | 条件成立したラベル名 |
| e.lData | 条件成立したデバイス値 |
| e.lReturnCode | 条件チェック処理の戻り値 |

- イベントハンドラの削除

```csharp
object.OnDeviceStatus -= new MITSUBISHI.Component.DotUtlType.DeviceStatusEventHandler(object_OnDeviceStatus);
```

**戻り値** (11.5 / 565 / 原本 p.567)

なし

**説明**

- EntryDeviceStatus関数にて登録したデバイス条件が，成立時にアプリケーションに対してイベントを通知します。
  ユーザプログラム側にて本関数を実装することにより，登録されたデバイス条件成立時に，イベントを受けることができます。
- lDataには，EntryDeviceStatusにて登録したデバイス値が入ります。
  (例) ワードデバイスで「-1」の値を監視している場合
  EntryDeviceStatusで65535(0000FFFFH)を登録デバイス値として設定します。
  CPUユニットの対象ワードデバイスが「-1」(FFFFH)の状態になると，OnDeviceStatusが実行され，lDataには(0000FFFFH)が入ります。

> **Point**
> ユーザプログラム内で下記の設定を行っている場合，EntryDeviceStatus関数で登録したデバイスの条件が成立してもOnDeviceStatusのイベントが発生しません。
> イベント発生待ちになった場合，下記の設定が終了するまで.Netコントロールに制御が戻らず，デバイス管理処理が停止しますので注意してください。
> - Visual Basic .NETで作成しているユーザプログラム
>   ユーザプログラム内でメッセージボックスを表示している場合
>   ユーザプログラム内でInputBox/OutputBoxを表示している場合
> - Visual Basic .NETおよびVisual C#で作成しているユーザプログラム
>   ユーザプログラム内でSleep処理，WaitForSingleObject関数などの待機関数を使用している場合

