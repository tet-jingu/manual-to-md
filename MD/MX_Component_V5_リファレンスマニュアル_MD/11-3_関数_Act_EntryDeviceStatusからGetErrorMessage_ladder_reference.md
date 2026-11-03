# MX Component Version 5 リファレンスマニュアル 11章 関数 (3/8) p.468-495

| 項目 | 内容 |
|---|---|
| 原本 | 【三菱】MX Component Version 5 リファレンスマニュアル (SH-082394J) |
| メーカー | 三菱電機 |
| 原本ファイル | `PDF/【三菱】MX Component Version 5 リファレンスマニュアル_sh082394j.pdf` (全696ページ) |
| 本ファイルの範囲 | 11.3 関数の詳細(Actコントロール用) EntryDeviceStatus〜GetErrorMessage (印刷ページ 466-493 / PDF p.468-495) |
| 出典表記 | `(節 / 印刷ページ / 原本 p.PDFページ)` |
| 作成日 | 2026-11-03 |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。
> 本文中の「○ページ」はすべて原本の**印刷ページ番号**です(PDFページ = 印刷ページ + 2)。
> デバイスリスト例の「¥n」は原本表記のまま(日本語フォントでのバックスラッシュ表示。プログラム上は `\n`)。
> 引数名の先頭文字(VBA/C++の `lRet` = 小文字エル、VB.NETの `IRet` = 大文字アイ)はテキスト抽出結果のまま。原本フォントでは判別しにくいので要確認。

## 主要用語 対訳表 (Glossary)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| 状態監視登録 | Device status monitoring registration | EntryDeviceStatus | 参考訳 |
| 状態監視登録解除 | Deregistration of device status monitoring | FreeDeviceStatus | 参考訳 |
| イベント告知 | Event announcement | OnDeviceStatus | 参考訳 |
| 一括読出し / 一括書込み | Batch read / Batch write | ReadDeviceBlock2 / WriteDeviceBlock2 | 参考訳 |
| ランダム読出し / ランダム書込み | Random read / Random write | ReadDeviceRandom2 / WriteDeviceRandom2 | 参考訳 |
| デバイスデータの設定 / 取得 | Set device data / Get device data | SetDevice2 / GetDevice2 | 参考訳 |
| エラー内容と処置方法の取得 | Get error description and corrective action | GetErrorMessage | 参考訳 |
| 登録デバイス名リスト | Registered device name list | szDeviceList | 参考訳 |
| 登録デバイス点数 | Number of registered devices | lSize / iSize | 参考訳 |
| 状態監視間隔時間 | Status monitoring interval | lMonitorCycle / iMonitorCycle (1〜3600秒) | 参考訳 |
| 登録デバイス値リスト | Registered device value list | lData / lplData / iData | 参考訳 |
| 条件成立したデバイス名 / 値 | Device name / value that met the condition | szDevice / lData | 参考訳 |
| 条件チェック処理の戻り値 | Return value of condition check | lReturnCode | 参考訳 |
| 戻り値 | Return value | lRet / iRet | 参考訳 |
| COMの戻り値 | COM return value | hResult (HRESULT) | 参考訳 |
| 通信関数の戻り値 | Communication function return value | lplRetCode | 参考訳 |
| 読出し点数 / 書込み点数 | Number of read points / write points | lSize | 参考訳 |
| 改行記号 | Line feed character | vbLf / ¥n | 参考訳 |
| イベントハンドラ | Event handler | — | 参考訳 |
| 管理イベント | Control events | Visual C++ プロパティ | 参考訳 |
| ワードデバイス / ダブルワードデバイス | Word device / Double word device | D / LTN | 参考訳 |
| 桁指定 | Digit specification | K8M0 | 参考訳 |
| ゲートウェイデバイス | Gateway device | EG | 参考訳 |
| 4ワードデバイス | 4-word device | FD | 参考訳 |
| 上位2バイト / 下位2バイト | Upper 2 bytes / Lower 2 bytes | H / L | 参考訳 |
| セーフティモード / 安全デバイス | Safety mode / Safety device | RnSFCPU, 0x010A42A5 | 参考訳 |
| グローバルラベル | Global label | — | 参考訳 |
| メモリエリア | Memory area | — | 参考訳 |
| 待機関数 | Wait function | Sleep / WaitForSingleObject | 参考訳 |
| 参照設定 | References | — | 参考訳 |

## 変換範囲表

| 原本ページ(PDF) | 印刷ページ | 節 | 扱い |
|---|---|---|---|
| p.468-471 | 466-469 | EntryDeviceStatus | 全文(タイミング図は文章化) |
| p.472 | 470 | FreeDeviceStatus | 全文 |
| p.473-475 | 471-473 | OnDeviceStatus | 全文 |
| p.476-478 | 474-476 | ReadDeviceBlock2 | 全文 |
| p.479-481 | 477-479 | WriteDeviceBlock2 | 全文 |
| p.482-484 | 480-482 | ReadDeviceRandom2 | 全文 |
| p.485-487 | 483-485 | WriteDeviceRandom2 | 全文 |
| p.488-490 | 486-488 | SetDevice2 | 全文 |
| p.491-493 | 489-491 | GetDevice2 | 全文 |
| p.494-495 | 492-493 | GetErrorMessage | 全文 |
| p.418-467 | 416-465 | 11.1〜11.3 Open〜SetCpuStatus | 別ファイル(11-1, 11-2) |
| p.496-604 | 494-602 | 11.4 ロギングファイル転送用、11.5 .Netコントロール用 | 別ファイル(11-4〜11-8) |
| p.1-417, p.605-696 | — | 11章以外 | 別ファイル(01_〜10-9_)または**未変換** |

※本範囲の関数ページにはプログラム例(コード)は掲載されていない(書式・引数表・説明・デバイス指定方法のみ)。

## 目次

- EntryDeviceStatus(デバイスの状態監視登録)
- FreeDeviceStatus(デバイスの状態監視登録解除)
- OnDeviceStatus(イベント告知)
- ReadDeviceBlock2(デバイスの一括読出し)
- WriteDeviceBlock2(デバイスの一括書込み)
- ReadDeviceRandom2(デバイスのランダム読出し)
- WriteDeviceRandom2(デバイスのランダム書込み)
- SetDevice2(デバイスデータの設定)
- GetDevice2(デバイスデータの取得)
- GetErrorMessage(エラー内容と処置方法の取得)

---
## EntryDeviceStatus(デバイスの状態監視登録) (11.3 / 466 / 原本 p.468)

### 使用可能コントロール (11.3 / 466 / 原本 p.468)

下記のコントロールで使用可能です。
- 32ビット用: ActProgType，ActUtlType

### 機能 (11.3 / 466 / 原本 p.468)

状態監視を行うデバイスを登録します。

### 書式 (11.3 / 466 / 原本 p.468)

**■VBA**

```
lRet = object.EntryDeviceStatus(szDeviceList, lSize, lMonitorCycle, lData(0))
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| String | szDeviceList | 登録デバイス名リスト | Input |
| Long | lSize | 登録デバイス点数 | Input |
| Long | lMonitorCycle | 状態監視間隔時間 | Input |
| Long | lData(n) | 登録デバイス値リスト | Input |

**■Visual C++**

```
lRet = object.EntryDeviceStatus (szDeviceList, lSize, lMonitorCycle, *lplData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| CString | szDeviceList | 登録デバイス名リスト | Input |
| Long | lSize | 登録デバイス点数 | Input |
| Long | lMonitorCycle | 状態監視間隔時間 | Input |
| Long | *lplData | 登録デバイス値リスト | Input |

**■Visual Basic .NET**

```
IRet = object.EntryDeviceStatus(szDeviceList, ISize,IMonitorCycle, IData(0))
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| String | szDeviceList | 登録デバイス名リスト | Input |
| Integer | ISize | 登録デバイス点数 | Input |
| Integer | IMonitorCycle | 状態監視間隔時間 | Input |
| Integer | IData(n) | 登録デバイス値リスト | Input |

**■Visual C#**

```
iRet = object. EntryDeviceStatus(szDeviceList, iSize, iMonitorCycle, ref iData[0])
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |
| String | szDeviceList | 登録デバイス名リスト | Input |
| int | iSize | 登録デバイス点数 | Input |
| int | iMonitorCycle | 状態監視間隔時間 | Input |
| int[n] | iData | 登録デバイス値リスト | Input |

### 戻り値 (11.3 / 466 / 原本 p.468)

正常終了: 0を返します。
異常終了: 0以外を返します。(☞617ページ エラーコード)

### 説明 (11.3 / 467 / 原本 p.469)

- szDeviceListにて指定したlSize(iSize)分のデバイス群が，lData(lplDataまたはiData)にて指定した状態であるかを確認します。
  確認時間はlMonitorCycle(iMonitorCycle)にて指定します。
  状態成立によりユーザプログラムのOnDeviceStatus関数を実行します。
- デバイスリストに指定する文字列は改行記号で区切ってください。
  最終デバイスの後ろには改行記号は必要ありません。
  (例)

| 言語 | 指定例 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"D0" & vbLf & "D1" & vbLf & "D2"` |
| Visual C++使用時 | `D0¥nD1¥nD2` |
| Visual C#使用時 | `D0¥nD1¥nD2` |

- lSize(iSize)に指定できる最大デバイス点数は，20点です。
- lMonitorCycle(iMonitorCycle)は1秒～1時間の範囲(1～3600の秒単位で設定)で指定してください。
  これ以外の値を指定するとエラーとなります。
- 登録デバイス値リストを，lData(lplDataまたはiData)に格納します。

> **Point**
> - パソコン性能，実行中のアプリケーション負荷，シーケンサとの通信に要する時間などの条件により，指定の状態監視間隔時間に，デバイスの状態監視が行えない場合があります。また，コントロールの他の関数を同時に使用する場合も，指定の状態監視間隔時間でデバイスの状態監視ができない原因になります。
> - lData(lplDataまたはiData)は，lSize(iSize)に指定した点数分のメモリエリアを用意してください。メモリエリアがない場合は，アプリケーションエラーなど重大な現象が発生するおそれがあります。
> - 状態監視中にEntryDeviceStatusを実行した場合は，エラーとなります。状態監視の条件を変更する場合は，FreeDeviceStatusを実行後，再度EntryDeviceStatusを実行してください。
> - 複数デバイスが同時に状態変化した場合は，状態変化したごとに，OnDeviceStatusイベントが実行されます。
>   (例: M0を監視している場合)
>
> 【図】状態監視の動作シーケンス(アプリケーション / MX Component / シーケンサ) (11.3 / 467 / 原本 p.469)
> - MX Component → シーケンサ: 「M0, M1読出し要求」，シーケンサ → MX Component: 「M0, M1の内容」を周期的に繰り返す
> - シーケンサで「M0 ON !」となった後の読出しで，MX Component → アプリケーションに「イベント通知(M0)」→ アプリケーションで「OnDeviceStatus イベント実行」
> - その後シーケンサで「M0 OFF」，続いて「M0, M1 ON !」となった後の読出しで，MX Component → アプリケーションに「イベント通知(M0)」と「イベント通知(M1)」が順に送られ，アプリケーションで「OnDeviceStatus イベント実行」が2回行われる
>
> - コントロールが定期的にデバイスランダム読出しを実行し，状態成立を確認する機能です。したがって，CPUユニットがデバイスの状態成立をMX Componentに通知する機能ではありません。そのため，指定の状態監視間隔時間によっては，コントロールがCPUユニットのデバイスの状態成立を確認できない場合があります。
> - インバータ通信/ロボットコントローラ通信時は使用できません。

### ワードデバイスを状態監視する場合の注意事項 (11.3 / 468 / 原本 p.470)

ワードデバイスが負の値-1～-32768(FFFFH～8000H)になるのを状態監視する場合，EntryDeviceStatusの監視デバイス値は上位2バイトに「0」を格納した65535～32768(0000FFFFH～00008000H)を設定してください。
(例) D0が「-10」となるのを状態監視させる場合
「-10(FFFFFFF6H)」の上位2バイトに「0」を格納した値「65526(0000FFF6H)」を監視デバイス値に設定してください。
CPUユニットのワードデバイスがWORD型であるのに対し，EntryDeviceStatusの監視デバイス値の型はLONG型であるため，CPUユニットの現在値とEntryDeviceStatusの監視デバイス値を比較した場合，同じ値にはならず上記の設定が必要になります。(ビットデバイスおよびダブルワードデバイス使用時は，本注意事項は該当しません。)
本注意事項についてのプログラミング例は下記を参照してください。
☞670ページ ワードデバイスを状態監視する場合のプログラミング例

### デバイス指定方法 (11.3 / 468 / 原本 p.470)

デバイスの指定方法を下記に示します。

#### 下記のように指定した場合(点数は3点) (11.3 / 468 / 原本 p.470)

| 言語 | 指定例 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"M0" & vbLf & "D0" & vbLf & "K8M0"` |
| Visual C++使用時 | `M0¥nD0¥nK8M0` |
| Visual C#使用時 | `M0¥nD0¥nK8M0` |

| 上位2バイト | 下位2バイト |
|---|---|
| 使用しません。(0が格納されます。) | M0 |
| (同上) | D0 |
| M16～M31*1 | M0～M15*1 |

※原本では上位2バイト「使用しません。(0が格納されます。)」のセルはM0・D0の2行で共有。

> *1 デバイスの番号順に，下位ビットから格納されます。

#### FXCPUのCN200以降を含むデバイスを指定した場合(点数は合計3点) (11.3 / 468 / 原本 p.470)

FXCPUのCN200以降は，ランダム読出しでは1点で2ワード分読み出します。

| 言語 | 指定例 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"D0" & vbLf & "CN200" & vbLf & "D1"` |
| Visual C++使用時 | `D0¥nCN200¥nD1` |
| Visual C#使用時 | `D0¥nCN200¥nD1` |

| 上位2バイト | 下位2バイト |
|---|---|
| 使用しません。(0が格納されます。) | D0 |
| CN200のH | CN200のL |
| 使用しません。(0が格納されます。) | D1 |

#### FDを含むデバイスを指定した場合(点数は合計3点) (11.3 / 468 / 原本 p.470)

| 言語 | 指定例 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"D0" & vbLf & "FD0" & vbLf & "D1"` |
| Visual C++使用時 | `D0¥nFD0¥nD1` |
| Visual C#使用時 | `D0¥nFD0¥nD1` |

| 上位2バイト | 下位2バイト |
|---|---|
| 使用しません。(0が格納されます。) | D0 |
| (同上) | FD0のLL |
| (同上) | D1 |

※原本では上位2バイト「使用しません。(0が格納されます。)」のセルは3行で共有。

#### EGを含むデバイスを指定した場合(点数は合計3点) (11.3 / 469 / 原本 p.471)

EG0に8ビットデバイス(シャープ社製シーケンサのE0000，E0001)が割り付けられている例を下記に示します。

| 言語 | 指定例 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"D0" & vbLf & "EG0" & vbLf & "D1"` |
| Visual C++使用時 | `D0¥nEG0¥nD1` |
| Visual C#使用時 | `D0¥nEG0¥nD1` |

| 上位2バイト | 下位2バイト |
|---|---|
| 使用しません。(0が格納されます。) | D0 |
| (同上) | EG0<br>(E0001) / (E0000) |
| (同上) | D1 |

※原本では上位2バイト「使用しません。(0が格納されます。)」のセルは3行で共有。
※原本では EG0 の下段が (E0001)(E0000) の2セルに分割(左=上位バイト側 E0001，右=下位バイト側 E0000)。本mdでは「(E0001) / (E0000)」と表記。

#### ダブルワードデバイスを指定した場合 (11.3 / 469 / 原本 p.471)

| 言語 | 指定例 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"LTN0" & vbLf & "LTN1" & vbLf & "LTN2"` |
| Visual C++使用時 | `LTN0¥nLTN1¥nLTN2` |
| Visual C#使用時 | `LTN0¥nLTN1¥nLTN2` |

| 上位2バイト | 下位2バイト |
|---|---|
| LTN0のH | LTN0のL |
| LTN1のH | LTN1のL |
| LTN2のH | LTN2のL |

---

## FreeDeviceStatus(デバイスの状態監視登録解除) (11.3 / 470 / 原本 p.472)

### 使用可能コントロール (11.3 / 470 / 原本 p.472)

下記のコントロールで使用可能です。
- 32ビット用: ActProgType，ActUtlType

### 機能 (11.3 / 470 / 原本 p.472)

EntryDeviceStatusにて登録した，状態監視を行うデバイスを解除します。

### 書式 (11.3 / 470 / 原本 p.472)

**■VBA**

```
lRet = object.FreeDeviceStatus()
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |

**■Visual C++**

```
iRet = object. FreeDeviceStatus()
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |

**■Visual Basic .NET**

```
IRet = object.FreeDeviceStatus()
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |

**■Visual C#**

```
iRet = object. FreeDeviceStatus()
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |

※Visual C++ の戻り値が他関数(Long lRet)と異なり int iRet となっているのは原本どおり(要確認)。

### 戻り値 (11.3 / 470 / 原本 p.472)

正常終了: 0を返します。
異常終了: 0以外を返します。(☞617ページ エラーコード)

### 説明 (11.3 / 470 / 原本 p.472)

EntryDeviceStatus関数にて設定した状態監視を行うデバイスを解除します。

> **Point**
> インバータ通信/ロボットコントローラ通信時は使用できません。

---

## OnDeviceStatus(イベント告知) (11.3 / 471 / 原本 p.473)

### 使用可能コントロール (11.3 / 471 / 原本 p.473)

下記のコントロールで使用可能です。
- 32ビット用: ActProgType，ActUtlType

### 機能 (11.3 / 471 / 原本 p.473)

EntryDeviceStatus関数にて登録したデバイス条件が成立時に実行します。

### 書式(オブジェクトを生成して使用する場合) (11.3 / 471 / 原本 p.473)

**■VBA**

- イベントハンドラの生成

```
Private WithEvents object As objectLib.object
```

- イベントハンドラ

```
Private Sub object_OnDeviceStatus(szDevice, lData, lReturnCode)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| String | szDevice | 条件成立したデバイス名 | Input |
| Long | lData | 条件成立したデバイス値 | Input |
| Long | lReturnCode | 条件チェック処理の戻り値 | Input |

**■Visual Basic .NET**

- イベントハンドラの生成

```
AddHandler object.OnDeviceStatus, AddressOf object_OnDeviceStatus
```

- イベントハンドラ

```
Private Sub object_OnDeviceStatus(szDevice, iData, iReturnCode)
```

- イベントハンドラの削除

```
RemoveHandler object.OnDeviceStatus, AddressOf object_OnDeviceStatus
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| String | szDevice | 条件成立したデバイス名 | Input |
| Integer | iData | 条件成立したデバイス値 | Input |
| Integer | iReturnCode | 条件チェック処理の戻り値 | Input |

**■Visual C#**

- イベントハンドラの生成

```
object.OnDeviceStatus += new objectLib._IobjectEvents_OnDeviceStatusEventHandler(object_OnDeviceStatus);
```

- イベントハンドラ

```
private void object_OnDeviceStatus(szDevice, iData, iReturnCode)
```

- イベントハンドラの削除

```
object.OnDeviceStatus -= new objectLib._IobjectEvents_OnDeviceStatusEventHandler(object_OnDeviceStatus);
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| String | szDevice | 条件成立したデバイス名 | Input |
| int | iData | 条件成立したデバイス値 | Input |
| int | iReturnCode | 条件チェック処理の戻り値 | Input |

### 書式(フォームに貼り付けて使用する場合) (11.3 / 472 / 原本 p.474)

**■VBA**

```
Private Sub object.OnDeviceStatus(szDevice, lData, lReturnCode)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| String | szDevice | 条件成立したデバイス名 | Input |
| Long | lData | 条件成立したデバイス値 | Input |
| Long | lReturnCode | 条件チェック処理の戻り値 | Input |

**■Visual C++**

- イベントハンドラの生成
  フォームに貼り付けたコントロールのプロパティ ⇒[管理イベント]タブからOnDeviceStatusイベントを追加する。
  OnDeviceStatusイベント名: object_OnDeviceStatus
- イベントハンドラ

```
void object.OnDeviceStatus(szDevice, lData, lReturnCode)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| LPCTSTR | szDevice | 条件成立したデバイス名 | Input |
| Long | lData | 条件成立したデバイス値 | Input |
| Long | lReturnCode | 条件チェック処理の戻り値 | Input |

**■Visual Basic .NET**

```
Private Sub object_OnDeviceStatus(ByVal sender As System.Object,
ByVal e As objectLib. _objectIEvents_OnDeviceStatusEvent)
```

| 引数 | 内容 | Input/Output |
|---|---|---|
| sender | イベントの発生元 | Output |
| e | イベントのデータ | Output |

eのメンバは下記のとおりです。

| メンバ | 内容 |
|---|---|
| e.szDevice | 条件成立したデバイス名 |
| e.lReturnCode | 条件成立したデバイス値 |
| e.lData | 条件チェック処理の戻り値 |

※要確認: Visual Basic .NET の表では e.lReturnCode = 「条件成立したデバイス値」，e.lData = 「条件チェック処理の戻り値」となっており，Visual C# の表および他の書式と内容が入れ替わっている(原本どおり転記)。

**■Visual C#**

```
private void object_OnDeviceStatus
(object sender,object._IActUtlTypeEvents_OnDeviceStatusEvent e)
```

| 引数 | 内容 | Input/Output |
|---|---|---|
| sender | イベントの発生元 | Output |
| e | イベントのデータ | Output |

eのメンバは下記のとおりです。

| メンバ | 内容 |
|---|---|
| e->szDevice | 条件成立したデバイス名 |
| e->lReturnCode | 条件チェック処理の戻り値 |
| e->lData | 条件成立したデバイス値 |

※Visual C# のメンバ表記が「e->」(C++の矢印演算子)になっているのは原本どおり。

### 戻り値 (11.3 / 472 / 原本 p.474)

なし

### 説明 (11.3 / 473 / 原本 p.475)

- EntryDeviceStatus関数にて登録したデバイス条件が，成立時にアプリケーションに対してイベントを通知します。
  ユーザプログラム側にて本関数を実装することにより，登録されたデバイス条件成立時に，イベントを受けることができます。
- lDataには，EntryDeviceStatusにて登録したデバイス値が入ります。
  (例) ワードデバイスで「-1」の値を監視している場合
  EntryDeviceStatusで65535(0000FFFFH)を登録デバイス値として設定します。
  CPUユニットの対象ワードデバイスが「-1」(FFFFH)の状態になると，OnDeviceStatusが実行され，lDataには(0000FFFFH)が入ります。

> **Point**
> - ユーザプログラム内で下記設定を行っている場合，EntryDeviceStatus関数で登録したデバイスの条件が成立してもOnDeviceStatusのイベントが発生しません。イベント発生待ちになった場合，下記設定が終了するまでコントロールに制御が戻らず，デバイス管理処理が停止しますので注意してください。
>   (1) Visual Basic .NET ，VBA(Excel)で作成しているユーザプログラム
>   ･ユーザプログラム内でメッセージボックスを表示している。
>   ･ユーザプログラム内でInputBox/OutputBoxを表示している。
>   (2) Visual Basic .NET，Visual C++，Visual C#，およびVBA(Excel，Access)で作成しているユーザプログラム
>   ･ユーザプログラム内でSleep処理，WaitForSingleObject関数などの待機関数を使用している。
> - "参照設定"の実装方法についてはサンプルプログラムを参考にしてください。
> - 64ビット用ではフォームに貼り付けて使用する方法は利用できません。
> - インバータ通信/ロボットコントローラ通信時は使用できません。

---

## ReadDeviceBlock2(デバイスの一括読出し) (11.3 / 474 / 原本 p.476)

### 使用可能コントロール (11.3 / 474 / 原本 p.476)

下記のコントロールで使用可能です。
- 32ビット用: ActProgType，ActUtlType
- 64ビット用: ActProgType64，ActUtlType64

### 機能 (11.3 / 474 / 原本 p.476)

2バイトデータでデバイスの一括読出しを行います。

### 書式 (11.3 / 474 / 原本 p.476)

**■VBA**

```
lRet = object.ReadDeviceBlock2(szDevice, lSize, iData(0))
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| String | szDevice | デバイス名 | Input |
| Long | lSize | 読出し点数 | Input |
| Integer | iData(n) | 読み出したデバイス値 | Output |

**■Visual C++**

```
lRet = object.ReadDeviceBlock2(szDevice, lSize, *lpsData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| CString | szDevice | デバイス名 | Input |
| Long | lSize | 読出し点数 | Input |
| Short | *lpsData | 読み出したデバイス値 | Output |

**■Visual Basic .NET**

```
IRet = object.ReadDeviceBlock2(szDevice, ISize, sData(0))
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| String | szDevice | デバイス名 | Input |
| Integer | ISize | 読出し点数 | Input |
| short | sData(n) | 読み出したデバイス値 | Output |

**■Visual C#**

```
iRet = object.ReadDeviceBlock2(szDevice, iSize, out sData[0])
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |
| String | szDevice | デバイス名 | Input |
| int | iSize | 読出し点数 | Input |
| short[n] | sData | 読み出したデバイス値 | Output |

### 書式(オブジェクトを生成して使用する場合) (11.3 / 475 / 原本 p.477)

**■Visual C++**

```
hResult = object.ReadDeviceBlock2(szDevice, lSize, *lpsData, *lplRetCode)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| HRESULT | hResult | COMの戻り値 | Output |
| BSTR | szDevice | デバイス名 | Input |
| LONG | lSize | 読出し点数 | Input |
| SHORT | *lpsData | 読み出したデバイス値 | Output |
| LONG | *lplRetCode | 通信関数の戻り値 | Output |

### 戻り値 (11.3 / 475 / 原本 p.477)

正常終了: 0を返します。
異常終了: 0以外を返します。(☞617ページ エラーコード)

### 説明 (11.3 / 475 / 原本 p.477)

- szDeviceにて指定したデバイスから，lSize(iSize)分のデバイス値をSHORT型のデータとして一括して読み出します。
- 読み出したデバイス値は，iData(lpsDataまたはsData)に格納されます。
- iData(lpsDataまたはsData)は，lSize(iSize)以上の配列を確保してください。

> **Point**
> - lSizeに指定できる最大読出し点数は，下記の満たす範囲です。
>   読出し開始デバイス番号 + 読出し点数 ≦ 最終デバイス番号
> - ビットデバイス指定時は，デバイス番号は16の倍数が指定可能です。
> - iData(lpsDataまたはsData)は，lSize(iSize)に指定した点数分のメモリエリアを用意してください。メモリエリアがない場合は，アプリケーションエラーなど重大な現象が発生するおそれがあります。
> - ロングタイマの接点(LTS)，ロングタイマのコイル(LTC)，ロング積算タイマの接点(LSTS)，ロング積算タイマのコイル(LSTC)のデバイスの読出しはできません。ReadDeviceRandom2関数，またはGetDevice2関数を使用してください。
> - インバータ通信/ロボットコントローラ通信時は使用できません。

※「≦」はテキスト抽出で欠落していたため原本画像から補った。

### デバイス指定方法 (11.3 / 475 / 原本 p.477)

デバイスの指定方法を下記に示します。

#### ビットデバイス指定時 (11.3 / 475 / 原本 p.477)

(例) M0から16点単位で3点(3ワード分)読み出す。

| 2バイト |
|---|
| M0～M15*1 |
| M16～M31*1 |
| M32～M47*1 |

> *1 デバイスの番号順に，下位ビットから格納されます。

#### ワードデバイス指定時 (11.3 / 475 / 原本 p.477)

(例) D0から3点読み出す。

| 2バイト |
|---|
| D0 |
| D1 |
| D2 |

#### FXCPUのCN200以降指定時 (11.3 / 476 / 原本 p.478)

(例) CN200から6点読み出す。
FXCPUのCN200以降は，2点で2ワード読み出します。1点ではエラーとなります。

| 2バイト |
|---|
| CN200のL |
| CN200のH |
| CN201のL |
| CN201のH |
| CN202のL |
| CN202のH |

#### FDデバイス指定時(4ワードデバイス) (11.3 / 476 / 原本 p.478)

(例) FD0から6点読み出す。

| 2バイト |
|---|
| FD0のLL |
| FD0のLH |
| FD0のHL |
| FD0のHH |
| FD1のLL |
| FD1のLH |

#### ゲートウェイデバイスに割り付けられた8ビットデバイス (11.3 / 476 / 原本 p.478)

(例) EG0から4点読み出す。
(EG0～EG3に8ビットデバイス(シャープ社製シーケンサのE0000～E0007)が割り付けられている場合)

| 2バイト |
|---|
| EG0<br>(E0001) / (E0000) |
| EG1<br>(E0003) / (E0002) |
| EG2<br>(E0005) / (E0004) |
| EG3<br>(E0007) / (E0006) |

※原本では EG0 の下段が (E0001)(E0000) の2セルに分割(左=上位バイト側 E0001，右=下位バイト側 E0000)。本mdでは「(E0001) / (E0000)」と表記。

#### ダブルワードデバイス指定時 (11.3 / 476 / 原本 p.478)

(例) LTN0から3点読み出す。

| 2バイト |
|---|
| LTN0のL |
| LTN1のL |
| LTN2のL |

---

## WriteDeviceBlock2(デバイスの一括書込み) (11.3 / 477 / 原本 p.479)

### 使用可能コントロール (11.3 / 477 / 原本 p.479)

下記のコントロールで使用可能です。
- 32ビット用: ActProgType，ActUtlType
- 64ビット用: ActProgType64，ActUtlType64

### 機能 (11.3 / 477 / 原本 p.479)

2バイトデータでデバイスの一括書込みを行います。

### 書式 (11.3 / 477 / 原本 p.479)

**■VBA**

```
lRet = object.WriteDeviceBlock2(szDevice, lSize, iData(0))
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| String | szDevice | デバイス名 | Input |
| Long | lSize | 書込み点数 | Input |
| Integer | iData(n) | 書き込むデバイス値 | Input |

**■Visual C++**

```
lRet = object.WriteDeviceBlock2(szDevice, lSize, *lpsData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| CString | szDevice | デバイス名 | Input |
| Long | lSize | 書込み点数 | Input |
| Short | *lpsData | 書き込むデバイス値 | Input |

**■Visual Basic .NET**

```
IRet = object.WriteDeviceBlock2(szDevice, ISize, sData(0))
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| String | szDevice | デバイス名 | Input |
| Integer | ISize | 書込み点数 | Input |
| short | sData(n) | 書き込むデバイス値 | Input |

**■Visual C#**

```
iRet = object.WriteDeviceBlock2(szDevice, iSize, ref sData[0])
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |
| String | szDevice | デバイス名 | Input |
| int | iSize | 書込み点数 | Input |
| short[n] | sData | 書き込むデバイス値 | Input |

### 書式(オブジェクトを生成して使用する場合) (11.3 / 478 / 原本 p.480)

**■Visual C++**

```
hResult = object.WriteDeviceBlock2(szDevice, lSize, *lpsData, *lplRetCode)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| HRESULT | hResult | COMの戻り値 | Output |
| BSTR | szDevice | デバイス名 | Input |
| LONG | lSize | 書込み点数 | Input |
| SHORT | *lpsData | 書き込むデバイス値 | Input |
| LONG | *lplRetCode | 通信関数の戻り値 | Output |

### 戻り値 (11.3 / 478 / 原本 p.480)

正常終了: 0を返します。
異常終了: 0以外を返します。(☞617ページ エラーコード)

### 説明 (11.3 / 478 / 原本 p.480)

- szDeviceにて指定したデバイスから，lSize(iSize)分のデバイス値を一括して書き込みます。
- 書き込むデバイス値を，iData(lpsDataまたはsData)に格納します。
- iData(lpsDataまたはsData)は，lSize(iSize)以上の配列を確保してください。

> **Point**
> - lSize(iSize)に指定できる最大書込み点数は，下記の満たす範囲です。
>   書込み開始デバイス番号 + 書込み点数 ≦ 最終デバイス番号
> - ビットデバイス指定時は，デバイス番号は16の倍数が指定可能です。
> - iData(lpsDataまたはsData)は，lSize(iSize)に指定した点数分のメモリエリアを用意してください。
>   メモリエリアがない場合は，アプリケーションエラーなど重大な現象が発生するおそれがあります。
> - ロングタイマの接点(LTS)，ロングタイマのコイル(LTC)，ロング積算タイマの接点(LSTS)，ロング積算タイマのコイル(LSTC)のデバイスの書込みはできません。WriteDeviceRandom2関数，またはSetDevice2関数を使用してください。
> - RnSFCPUのセーフティモードで安全デバイスに対して実行した場合は，エラーコード"0x010A42A5"(セーフティモードでは実施できない操作を行った)が返されます。
> - インバータ通信/ロボットコントローラ通信時は使用できません。

※「≦」はテキスト抽出で欠落していたため原本画像から補った。

### デバイス指定方法 (11.3 / 478 / 原本 p.480)

デバイスの指定方法を下記に示します。

#### ビットデバイス指定時 (11.3 / 478 / 原本 p.480)

(例) M0から16点単位で3点(3ワード分)書き込む。

| 2バイト |
|---|
| M0～M15*1 |
| M16～M31*1 |
| M32～M47*1 |

> *1 デバイスの番号順に，下位ビットから格納されます。

#### ワードデバイス指定時 (11.3 / 478 / 原本 p.480)

(例) D0から3点書き込む。

| 2バイト |
|---|
| D0 |
| D1 |
| D2 |

#### FXCPUのCN200以降指定時 (11.3 / 479 / 原本 p.481)

(例) CN200から6点書き込む。
FXCPUのCN200以降は，2点で2ワード書き込みます。1点ではエラーとなります。

| 2バイト |
|---|
| CN200のL |
| CN200のH |
| CN201のL |
| CN201のH |
| CN202のL |
| CN202のH |

#### FDデバイス指定時(4ワードデバイス) (11.3 / 479 / 原本 p.481)

(例) FD0から6点書き込む。

| 2バイト |
|---|
| FD0のLL |
| FD0のLH |
| FD0のHL |
| FD0のHH |
| FD1のLL |
| FD1のLH |

#### ゲートウェイデバイスに割り付けられた8ビットデバイス (11.3 / 479 / 原本 p.481)

(例) EG0から4点書き込む。
(EG0～EG3に8ビットデバイス(シャープ社製シーケンサのE0000～E0007)が割り付けられている場合)

| 2バイト |
|---|
| EG0<br>(E0001) / (E0000) |
| EG1<br>(E0003) / (E0002) |
| EG2<br>(E0005) / (E0004) |
| EG3<br>(E0007) / (E0006) |

※原本では EG0 の下段が (E0001)(E0000) の2セルに分割(左=上位バイト側 E0001，右=下位バイト側 E0000)。本mdでは「(E0001) / (E0000)」と表記。

#### ダブルワードデバイス指定時 (11.3 / 479 / 原本 p.481)

(例) LTN0から3点書き込む。

| 2バイト |
|---|
| LTN0のL |
| LTN1のL |
| LTN2のL |

---

## ReadDeviceRandom2(デバイスのランダム読出し) (11.3 / 480 / 原本 p.482)

### 使用可能コントロール (11.3 / 480 / 原本 p.482)

下記のコントロールで使用可能です。
- 32ビット用: ActProgType，ActUtlType
- 64ビット用: ActProgType64，ActUtlType64

### 機能 (11.3 / 480 / 原本 p.482)

2バイトデータでデバイスのランダム読出しを行います。

### 書式 (11.3 / 480 / 原本 p.482)

**■VBA**

```
lRet = object.ReadDeviceRandom2(szDeviceList, lSize, iData(0))
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| String | szDeviceList | デバイス名 | Input |
| Long | lSize | 読出し点数 | Input |
| Integer | iData(n) | 読み出したデバイス値 | Output |

**■Visual C++**

```
lRet = object.ReadDeviceRandom2(szDeviceList, lSize, *lpsData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| CString | szDeviceList | デバイス名 | Input |
| Long | lSize | 読出し点数 | Input |
| Short | *lpsData | 読み出したデバイス値 | Output |

**■Visual Basic .NET**

```
IRet = object.ReadDeviceRandom2(szDeviceList, ISize, sData(0))
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| String | szDeviceList | デバイス名 | Input |
| Integer | ISize | 読出し点数 | Input |
| short | sData(n) | 読み出したデバイス値 | Output |

**■Visual C#**

```
iRet = object.ReadDeviceRandom2(szDeviceList, iSize, out sData[0])
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |
| String | szDeviceList | デバイス名 | Input |
| int | iSize | 読出し点数 | Input |
| short[n] | sData | 読み出したデバイス値 | Output |

### 書式(オブジェクトを生成して使用する場合) (11.3 / 481 / 原本 p.483)

**■Visual C++**

```
hResult = object.ReadDeviceRandom2(szDeviceList, lSize, *lpsData, *lplRetCode)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| HRESULT | hResult | COMの戻り値 | Output |
| BSTR | szDeviceList | デバイス名 | Input |
| LONG | lSize | 読出し点数 | Input |
| SHORT | *lpsData | 読み出したデバイス値 | Output |
| LONG | *lplRetCode | 通信関数の戻り値 | Output |

### 戻り値 (11.3 / 481 / 原本 p.483)

正常終了: 0を返します。
異常終了: 0以外を返します。(☞617ページ エラーコード)

### 説明 (11.3 / 481 / 原本 p.483)

- szDeviceListにて指定したデバイス群を，lSize(iSize)分のデバイス値だけ読み出します。
- 読み出したデバイス値は，iData(lpsDataまたはsData)に格納されます。
- デバイスリストに指定する文字列は改行記号で区切ってください。
  最終デバイスの後ろには改行記号は必要ありません。
  (例)

| 言語 | 指定例 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"D0" & vbLf & "D1" & vbLf & "D2"` |
| Visual C++使用時 | `D0¥nD1¥nD2` |
| Visual C#使用時 | `D0¥nD1¥nD2` |

- iData(lpsDataまたはsData)は，lSize(iSize)以上の配列を確保してください。
- グローバルラベルにアクセスする場合は，szDeviceListにグローバルラベルを指定してください。また，使用可能なグローバルラベルのデータ型および指定点数については下記を参照してください。
  ☞22ページ グローバルラベル名を指定したデータ取得

> **Point**
> - lSize(iSize)に指定できる最大読出し点数は，0x7FFFFFFF点までです。
> - iData(lpsDataまたはsData)は，lSize(iSize)に指定した点数分のメモリエリアを用意してください。
>   メモリエリアがない場合は，アプリケーションエラーなど重大な現象が発生するおそれがあります。
> - ダブルワードデバイスを指定した場合，ReadDeviceRandom2関数では下位1ワード(2バイト)分のデータのみ格納されます。(エラーは発生しません。)
>   ダブルワードデバイスの読出しを行う場合は，ReadDeviceRandom関数またはGetDevice関数を使用してください。
> - インバータ通信/ロボットコントローラ通信時は使用できません。

### デバイス指定方法 (11.3 / 481 / 原本 p.483)

デバイスの指定方法を下記に示します。

#### 下記のように指定した場合(点数は3点) (11.3 / 481 / 原本 p.483)

| 言語 | 指定例 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"M0" & vbLf & "D0" & vbLf & "K8M0"` |
| Visual C++使用時 | `M0¥nD0¥nK8M0` |
| Visual C#使用時 | `M0¥nD0¥nK8M0` |

| 2バイト |
|---|
| M0*1 |
| D0 |
| M0～M15*2 |

> *1 読み出すデバイスは「M0」1点のみを対象とし，デバイス値は「0」または「1」が格納されます。
> *2 デバイスの番号順に，下位ビットから格納されます。
> 上位2バイトM16～M31は読み出されません。

#### FXCPUのCN200以降を含むデバイスを指定した場合(点数は合計3点) (11.3 / 482 / 原本 p.484)

| 言語 | 指定例 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"D0" & vbLf & "CN200" & vbLf & "D1"` |
| Visual C++使用時 | `D0¥nCN200¥nD1` |
| Visual C#使用時 | `D0¥nCN200¥nD1` |

| 2バイト |
|---|
| D0 |
| CN200のL*1 |
| D1 |

> *1 FXCPUのCN200以降は，ReadDeviceRandom2では1点で指定デバイスのL(下位2バイト)を読み出します。
> 指定デバイスのH(上位2バイト)は読み出されません。

#### FDを含むデバイスを指定した場合(点数は合計3点) (11.3 / 482 / 原本 p.484)

| 言語 | 指定例 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"D0" & vbLf & "FD0" & vbLf & "D1"` |
| Visual C++使用時 | `D0¥nFD0¥nD1` |
| Visual C#使用時 | `D0¥nFD0¥nD1` |

| 2バイト |
|---|
| D0 |
| FD0のLL |
| D1 |

#### EGを含むデバイスを指定した場合(点数は合計3点) (11.3 / 482 / 原本 p.484)

EG0に8ビットデバイス(シャープ社製シーケンサのE0000，E0001)が割り付けられている例を下記に示します。

| 言語 | 指定例 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"D0" & vbLf & "EG0" & vbLf & "D1"` |
| Visual C++使用時 | `D0¥nEG0¥nD1` |
| Visual C#使用時 | `D0¥nEG0¥nD1` |

| 2バイト |
|---|
| D0 |
| EG0<br>(E0001) / (E0000) |
| D1 |

※原本では EG0 の下段が (E0001)(E0000) の2セルに分割(左=上位バイト側 E0001，右=下位バイト側 E0000)。本mdでは「(E0001) / (E0000)」と表記。

#### ダブルワードデバイスを指定した場合 (11.3 / 482 / 原本 p.484)

| 言語 | 指定例 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"LTN0" & vbLf & "LTN1" & vbLf & "LTN2"` |
| Visual C++使用時 | `LTN0¥nLTN1¥nLTN2` |
| Visual C#使用時 | `LTN0¥nLTN1¥nLTN2` |

| 2バイト |
|---|
| LTN0のL |
| LTN1のL |
| LTN2のL |

---

## WriteDeviceRandom2(デバイスのランダム書込み) (11.3 / 483 / 原本 p.485)

### 使用可能コントロール (11.3 / 483 / 原本 p.485)

下記のコントロールで使用可能です。
- 32ビット用: ActProgType，ActUtlType
- 64ビット用: ActProgType64，ActUtlType64

### 機能 (11.3 / 483 / 原本 p.485)

2バイトデータでデバイスのランダム書込みを行います。

### 書式 (11.3 / 483 / 原本 p.485)

**■VBA**

```
lRet = object.WriteDeviceRandom2(szDeviceList, lSize,iData(0))
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| String | szDeviceList | デバイス名 | Input |
| Long | lSize | 書込み点数 | Input |
| Integer | iData(n) | 書き込むデバイス値 | Input |

**■Visual C++**

```
lRet = object.WriteDeviceRandom2(szDeviceList, lSize,*lpsData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| CString | szDeviceList | デバイス名 | Input |
| Long | lSize | 書込み点数 | Input |
| Short | *lpsData | 書き込むデバイス値 | Input |

**■Visual Basic .NET**

```
IRet = object.WriteDeviceRandom2(szDeviceList, ISize, sData(0))
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| String | szDeviceList | デバイス名 | Input |
| Integer | ISize | 書込み点数 | Input |
| short | sData(n) | 書き込むデバイス値 | Input |

**■Visual C#**

```
iRet = object.WriteDeviceRandom2(szDeviceList, iSize, ref sData[0])
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |
| String | szDeviceList | デバイス名 | Input |
| int | iSize | 書込み点数 | Input |
| short[n] | sData | 書き込むデバイス値 | Input |

### 書式(オブジェクトを生成して使用する場合) (11.3 / 484 / 原本 p.486)

**■Visual C++**

```
hResult = object.WriteDeviceRandom2(szDeviceList, lSize, *lpsData, *lplRetCode)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| HRESULT | hResult | COMの戻り値 | Output |
| BSTR | szDeviceList | デバイス名 | Input |
| LONG | lSize | 書込み点数 | Input |
| SHORT | *lpsData | 書き込むデバイス値 | Input |
| LONG | *lplRetCode | 通信関数の戻り値 | Output |

### 戻り値 (11.3 / 484 / 原本 p.486)

正常終了: 0を返します。
異常終了: 0以外を返します。(☞617ページ エラーコード)

### 説明 (11.3 / 484 / 原本 p.486)

- szDeviceListにて指定したデバイス群を，lSize(iSize)分のデバイス値だけ書き込みます。
- 書き込むデバイス値を，iData(lpsDataまたはsData)に格納します。
- デバイスリストに指定する文字列は改行記号で区切ってください。最終デバイスの後ろには改行記号は必要ありません。
  (例)

| 言語 | 指定例 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"D0" & vbLf & "D1" & vbLf & "D2"` |
| Visual C++使用時 | `D0¥nD1¥nD2` |
| Visual C#使用時 | `D0¥nD1¥nD2` |

- iData(lpsDataまたはsData)は，lSize(iSize)以上の配列を確保してください。
- グローバルラベルにアクセスする場合は，szDeviceListにグローバルラベルを指定してください。また，使用可能なグローバルラベルのデータ型および指定点数については下記を参照してください。
  ☞22ページ グローバルラベル名を指定したデータ取得

> **Point**
> - lSize(iSize)に指定できる最大書込み点数は，0x7FFFFFFF点までです。
> - iData(lpsDataまたはsData)は，lSize(iSize)に指定した点数分のメモリエリアを用意してください。
>   メモリエリアがない場合は，アプリケーションエラーなど重大な現象が発生するおそれがあります。
> - ダブルワードデバイスを指定した場合，WriteDeviceRandom2関数では下位1ワード(2バイト)分のデータに書込みを行い，上位1ワード(2バイト)分のデータには"0"を書込みます。
>   ダブルワードデバイスの書込みを行う場合は，WriteDeviceRandom関数またはSetDevice関数を使用してください。
> - QモーションCPUへアクセスを行うと，エラーが返ります。
> - RnSFCPUのセーフティモードで安全デバイスに対して実行した場合は，エラーコード"0x010A42A5"(セーフティモードでは実施できない操作を行った)が返されます。
> - インバータ通信/ロボットコントローラ通信時は使用できません。

### デバイス指定方法 (11.3 / 485 / 原本 p.487)

デバイスの指定方法を下記に示します。

#### 下記のように指定した場合(点数は3点) (11.3 / 485 / 原本 p.487)

| 言語 | 指定例 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"M0" & vbLf & "D0" & vbLf & "K8M0"` |
| Visual C++使用時 | `M0¥nD0¥nK8M0` |
| Visual C#使用時 | `M0¥nD0¥nK8M0` |

| 2バイト |
|---|
| M0*1 |
| D0 |
| M0～M15*2 |

> *1 書き込むデバイスは「M0」1点のみを対象とし，デバイス値は設定する2バイトデータの最下位ビットが書き込む値となります。
> *2 デバイスの番号順に，下位ビットから格納されます。
> 上位2バイトM16～M31には"0"が書き込まれます。

#### FXCPUのCN200以降を含むデバイスを指定した場合(点数は合計3点) (11.3 / 485 / 原本 p.487)

| 言語 | 指定例 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"D0" & vbLf & "CN200" & vbLf & "D1"` |
| Visual C++使用時 | `D0¥nCN200¥nD1` |
| Visual C#使用時 | `D0¥nCN200¥nD1` |

| 2バイト |
|---|
| D0 |
| CN200のL*1 |
| D1 |

> *1 FXCPUのCN200以降は，WriteDeviceRandom2では1点で指定デバイスのL(下位2バイト)に書込みを行います。
> 指定デバイスのH(上位2バイト)には"0"が書き込まれます。

#### FDを含むデバイスを指定した場合(点数は合計3点) (11.3 / 485 / 原本 p.487)

| 言語 | 指定例 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"D0" & vbLf & "FD0" & vbLf & "D1"` |
| Visual C++使用時 | `D0¥nFD0¥nD1` |
| Visual C#使用時 | `D0¥nFD0¥nD1` |

| 2バイト |
|---|
| D0 |
| FD0のLL |
| D1 |

#### EGを含むデバイスを指定した場合(点数は合計3点) (11.3 / 485 / 原本 p.487)

EG0に8ビットデバイス(シャープ社製シーケンサのE0000，E0001)が割り付けられている例を下記に示します。

| 言語 | 指定例 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"D0" & vbLf & "EG0" & vbLf & "D1"` |
| Visual C++使用時 | `D0¥nEG0¥nD1` |
| Visual C#使用時 | `D0¥nEG0¥nD1` |

| 2バイト |
|---|
| D0 |
| EG0<br>(E0001) / (E0000) |
| D1 |

※原本では EG0 の下段が (E0001)(E0000) の2セルに分割(左=上位バイト側 E0001，右=下位バイト側 E0000)。本mdでは「(E0001) / (E0000)」と表記。

#### ダブルワードデバイスを指定した場合 (11.3 / 485 / 原本 p.487)

| 言語 | 指定例 |
|---|---|
| Visual Basic .NET，VBA使用時 | `"LTN0" & vbLf & "LTN1" & vbLf & "LTN2"` |
| Visual C++使用時 | `LTN0¥nLTN1¥nLTN2` |
| Visual C#使用時 | `LTN0¥nLTN1¥nLTN2` |

| 2バイト |
|---|
| LTN0のL |
| LTN1のL |
| LTN2のL |

---

## SetDevice2(デバイスデータの設定) (11.3 / 486 / 原本 p.488)

### 使用可能コントロール (11.3 / 486 / 原本 p.488)

下記のコントロールで使用可能です。
- 32ビット用: ActProgType，ActUtlType
- 64ビット用: ActProgType64，ActUtlType64

### 機能 (11.3 / 486 / 原本 p.488)

2バイトデータでデバイス1点の設定を行います。

### 書式 (11.3 / 486 / 原本 p.488)

**■VBA**

```
lRet = object.SetDevice2(szDevice, iData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| String | szDevice | デバイス名 | Input |
| Integer | iData | 設定データ | Input |

**■Visual C++**

```
lRet = object.SetDevice2(szDevice, sData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| CString | szDevice | デバイス名 | Input |
| Short | sData | 設定データ | Input |

**■Visual Basic .NET**

```
IRet = object.SetDevice2(szDevice, sData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| String | szDevice | デバイス名 | Input |
| Short | sData | 設定データ | Input |

**■Visual C#**

```
iRet = object.SetDevice2(szDevice, sData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |
| String | szDevice | デバイス名 | Input |
| short | sData | 設定データ | Input |

### 書式(オブジェクトを生成して使用する場合) (11.3 / 486 / 原本 p.488)

**■Visual C++**

```
hResult = object.SetDevice2(szDevice, sData, *lplRetCode)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| HRESULT | hResult | COMの戻り値 | Output |
| BSTR | szDevice | デバイス名 | Input |
| LONG | lData | 設定データ | Input |
| LONG | *lplRetCode | 通信関数の戻り値 | Output |

※要確認: 書式は `sData` だが，引数表は「LONG lData 設定データ」となっている(原本どおり転記)。

### 戻り値 (11.3 / 487 / 原本 p.489)

正常終了: 0を返します。
異常終了: 0以外を返します。(☞617ページ エラーコード)

### 説明 (11.3 / 487 / 原本 p.489)

- szDeviceにて指定したデバイス1点に対してiData(sData)で指定する操作を行います。
- ビットデバイス設定時は，iData値(sData値)の最下位のビットが有効となります。
- グローバルラベルにアクセスする場合は，szDeviceにグローバルラベルを指定してください。また，使用可能なグローバルラベルのデータ型および指定点数については下記を参照してください。
  ☞22ページ グローバルラベル名を指定したデータ取得

> **Point**
> - ダブルワードデバイスを指定した場合，SetDevice2関数では下位1ワード(2バイト)分のデータに書込みを行い，上位1ワード(2バイト)分のデータには"0"を書き込みます。
>   ダブルワードデバイスの書込みを行う場合は，WriteDeviceRandom関数またはSetDevice関数を使用してください。
> - RnSFCPUのセーフティモードで安全デバイスに対して実行した場合は，エラーコード"0x010A42A5"(セーフティモードでは実施できない操作を行った)が返されます。
> - インバータ通信/ロボットコントローラ通信時は使用できません。

### デバイス指定方法 (11.3 / 487 / 原本 p.489)

デバイスの指定方法を下記に示します。

#### ビットデバイス指定時 (11.3 / 487 / 原本 p.489)

(例) M0

| 2バイト |
|---|
| M0*1 |

> *1 書き込むデバイスは「M0」1点のみを対象とし，デバイス値は設定する2バイトデータの最下位ビットが書き込む値となります。

#### ワードデバイス指定時 (11.3 / 487 / 原本 p.489)

(例) D0

| 2バイト |
|---|
| D0 |

#### ダブルワードデバイス指定時 (11.3 / 487 / 原本 p.489)

(例) LTN0

| 2バイト |
|---|
| LTN0のL |

#### ダブルワードデバイス指定時(桁指定) (11.3 / 487 / 原本 p.489)

(例) K8M0

| 2バイト |
|---|
| M0～M15*1 |

> *1 デバイスの番号順に，下位ビットから格納されます。
> 上位2バイトM16～M31には"0"が書き込まれます。

#### FXCPUのCN200以降指定時 (11.3 / 488 / 原本 p.490)

(例) CN200

| 2バイト |
|---|
| CN200のL*1 |

> *1 FXCPUのCN200以降は，SetDevice2では1点で指定デバイスのL(下位2バイト)に書込みを行います。
> 指定デバイスのH(上位2バイト)には"0"が書き込まれます。

#### ゲートウェイデバイス指定時 (11.3 / 488 / 原本 p.490)

(例) EG0に8ビットデバイス(シャープ社製シーケンサのE0000，E0001)が割り付けられている場合

| 2バイト |
|---|
| EG0<br>(E0001) / (E0000) |

※原本では EG0 の下段が (E0001)(E0000) の2セルに分割(左=上位バイト側 E0001，右=下位バイト側 E0000)。本mdでは「(E0001) / (E0000)」と表記。

---

## GetDevice2(デバイスデータの取得) (11.3 / 489 / 原本 p.491)

### 使用可能コントロール (11.3 / 489 / 原本 p.491)

下記のコントロールで使用可能です。
- 32ビット用: ActProgType，ActUtlType
- 64ビット用: ActProgType64，ActUtlType64

### 機能 (11.3 / 489 / 原本 p.491)

2バイトデータでデバイス1点のデータを取得します。

### 書式 (11.3 / 489 / 原本 p.491)

**■VBA**

```
lRet = object.GetDevice2(szDevice, iData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| String | szDevice | デバイス名 | Input |
| Integer | iData | 取得データ | Output |

**■Visual C++**

```
lRet = object.GetDevice2(szDevice, *lpsData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| CString | szDevice | デバイス名 | Input |
| Short | *lpsData | 取得データ | Output |

**■Visual Basic .NET**

```
IRet = object.GetDevice2(szDevice, sData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| String | szDevice | デバイス名 | Input |
| short | sData | 取得データ | Output |

**■Visual C#**

```
iRet = object.GetDevice2(szDevice, out sData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |
| String | szDevice | デバイス名 | Input |
| short | sData | 取得データ | Output |

### 書式(オブジェクトを生成して使用する場合) (11.3 / 489 / 原本 p.491)

**■Visual C++**

```
hResult = object.GetDevice2(szDevice, *lpsData, *lplRetCode)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| HRESULT | hResult | COMの戻り値 | Output |
| BSTR | szDevice | デバイス名 | Input |
| SHORT | *lpsData | 取得データ | Output |
| LONG | *lplRetCode | 通信関数の戻り値 | Output |

### 戻り値 (11.3 / 490 / 原本 p.492)

正常終了: 0を返します。
異常終了: 0以外を返します。(☞617ページ エラーコード)

### 説明 (11.3 / 490 / 原本 p.492)

- szDeviceにて指定した1点のデバイスのデータを，iData(lpsDataまたはsData)に格納します。
- グローバルラベルにアクセスする場合は，szDeviceにグローバルラベルを指定してください。また，使用可能なグローバルラベルのデータ型および指定点数については下記を参照してください。
  ☞22ページ グローバルラベル名を指定したデータ取得

> **Point**
> - ダブルワードデバイスを指定した場合，GetDevice2関数では下位1ワード(2バイト)分のデータのみ格納されます。(エラーは発生しません。)
> - ダブルワードデバイスの読出しを行う場合は，ReadDeviceRandom関数またはGetDevice関数を使用してください。
> - インバータ通信/ロボットコントローラ通信時は使用できません。

### デバイス指定方法 (11.3 / 490 / 原本 p.492)

デバイスの指定方法を下記に示します。

#### ビットデバイス指定時 (11.3 / 490 / 原本 p.492)

(例) M0

| 2バイト |
|---|
| M0*1 |

> *1 読み出すデバイスは「M0」1点のみを対象とし，デバイス値は「0」または「1」が格納されます。

#### ワードデバイス指定時 (11.3 / 490 / 原本 p.492)

(例) D0

| 2バイト |
|---|
| D0 |

#### ダブルワードデバイス指定時 (11.3 / 490 / 原本 p.492)

(例) LTN0

| 2バイト |
|---|
| LTN0のL |

#### ダブルワードデバイス指定時(桁指定) (11.3 / 490 / 原本 p.492)

(例) K8M0

| 2バイト |
|---|
| M0～M15*1 |

> *1 デバイスの番号順に，下位ビットから格納されます。
> 上位2バイトM16～M31のデータは読み出されません。

#### FXCPUのCN200以降指定時 (11.3 / 490 / 原本 p.492)

(例) CN200

| 2バイト |
|---|
| CN200のL*1 |

> *1 FXCPUのCN200以降は，GetDevice2では1点で指定デバイスのL(下位2バイト)を読み出します。
> 指定デバイスのH(上位2バイト)は読み出されません。

#### ゲートウェイデバイス指定時 (11.3 / 491 / 原本 p.493)

(例) EG0に8ビットデバイス(シャープ社製シーケンサのE0000，E0001)が割り付けられている場合

| 2バイト |
|---|
| EG0<br>(E0001) / (E0000) |

※原本では EG0 の下段が (E0001)(E0000) の2セルに分割(左=上位バイト側 E0001，右=下位バイト側 E0000)。本mdでは「(E0001) / (E0000)」と表記。

---

## GetErrorMessage(エラー内容と処置方法の取得) (11.3 / 492 / 原本 p.494)

### 使用可能コントロール (11.3 / 492 / 原本 p.494)

下記のコントロールで使用可能です。
- 32ビット用: ActSupportMsg
- 64ビット用: ActSupportMsg64

### 機能 (11.3 / 492 / 原本 p.494)

エラーコードに対するエラー内容および処置方法を取得します。

### 書式 (11.3 / 492 / 原本 p.494)

**■VBA**

```
lRet = object.GetErrorMessage(lErrorCode, szErrorMessage)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| Long | lErrorCode | エラーコード | Input |
| String | szErrorMessage | エラーメッセージ | Output |

**■Visual C++**

```
lRet = object.GetErrorMessage(lErrorCode, *lpszErrorMessage)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| Long | lErrorCode | エラーコード | Input |
| BSTR | *lpszErrorMessage | エラーメッセージ | Output |

**■Visual Basic .NET**

```
IRet = object.GetErrorMessage(IErrorCode, szErrorMessage)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| Integer | IErrorCode | エラーコード | Input |
| String | szErrorMessage | エラーメッセージ | Output |

**■Visual C#**

```
iRet = object.GetErrorMessage(iErrorCode, out szErrorMessage)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |
| int | iErrorCode | エラーコード | Input |
| String | szErrorMessage | エラーメッセージ | Output |

### 書式(オブジェクトを生成して使用する場合) (11.3 / 492 / 原本 p.494)

**■Visual C++**

```
hResult = object.GetErrorMessage(lErrorCode, *lpszErrorMessage, *lplRetCode)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| HRESULT | hResult | COMの戻り値 | Output |
| LONG | lErrorCode | エラーコード | Input |
| BSTR | *lpszErrorMessage | エラーメッセージ | Output |
| LONG | *lplRetCode | 通信関数の戻り値 | Output |

### 戻り値 (11.3 / 493 / 原本 p.495)

正常終了: 0を返します。
異常終了: 0以外を返します。(☞617ページ エラーコード)

### 説明 (11.3 / 493 / 原本 p.495)

- lErrorCode(iErrorCode)にて指定したエラーコードのエラー内容および処置方法を読み出します。
- 読み出したエラー内容および処置方法はszErrorMessage(lpszErrorMessage)に格納されます。

> **Point**
> インバータ通信時は使用できません。
