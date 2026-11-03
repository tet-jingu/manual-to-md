# MX Component Version 5 リファレンスマニュアル 12章 サンプルプログラム (12 / 原本 p.605-618)

| 項目 | 内容 |
|---|---|
| 原本 | 【三菱】MX Component Version 5 リファレンスマニュアル (SH-082394J) |
| メーカー | 三菱電機 |
| 原本ファイル | `PDF/【三菱】MX Component Version 5 リファレンスマニュアル_sh082394j.pdf` (全696ページ) |
| 本ファイルの範囲 | 12章 サンプルプログラム (印刷ページ 603-616 / PDF p.605-618) |
| 出典表記 | `(節 / 印刷ページ / 原本 p.PDFページ)` |
| 作成日 | 2026-11-03 |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。
> 本文中の「○ページ」はすべて原本の**印刷ページ番号**です(PDFページ = 印刷ページ + 2)。
> 原本で縦に結合されたセル(同じ参照先・同じ内容を複数行で共有)は，各行に展開して「(同上)」と表記しています。
> この章の原本にはプログラムのソースコードは掲載されていません(サンプルの画面と表示項目の説明のみ)。

## 主要用語 対訳表 (Glossary)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| サンプルプログラム | Sample program | (インストールフォルダ)\Samples | 参考訳 |
| インストールフォルダ | Installation folder | — | 参考訳 |
| ソリューションファイル | Solution file | *.sln | 参考訳 |
| 対象コントロール | Target control | — | 参考訳 |
| ターゲットCPU | Target CPU (platform target) | "x86"(32ビット) | 参考訳 |
| 64ビット用コントロール | 64-bit control | ActUtlType64 等 | 参考訳 |
| フォームに貼り付けて使用する場合 | When pasting on a form | EarlyBind | 原本併記 |
| オブジェクトを生成して使用する場合 | When creating an object | LateBind | 原本併記 |
| 画面表示 / 表示内容 | Screen display / Display contents | — | 参考訳 |
| フレーム | Frame | Control / Get/Set / Output 等 | 参考訳 |
| 論理局番 | Logical station number | LogicalStationNumber | 原本併記 |
| デバイス名 / ラベル名 | Device name / Label name | DeviceName / LabelName | 原本併記 |
| デバイス点数 | Number of device points | DeviceSize / Device Points / Points | 原本併記 |
| 状態監視間隔時間 | Status monitoring interval | MonitorCycle / Interval | 原本併記 |
| 実行結果 | Execution result | ReturnCode / Result / RESULT | 原本併記 |
| メッセージコード | Message code | Code / Error code / ErrorCode(Hex) | 原本併記 |
| リモートコントロール | Remote control | Status / Operation | 原本併記 |
| 時計データ | Clock data | Year/Month/Day/Week/Hour/Minute/Second | 原本併記 |
| バッファメモリ | Buffer memory | I/OAdress / BufferAddress / BufferSize | 原本併記 |
| ロギングファイル | Logging file | ActDatalogging_2019.sln | 参考訳 |
| ファイルリスト | File list | — | 参考訳 |
| メニュー画面 / Method画面 | Menu screen / Method screen | Access用 | 原本併記 |
| バイナリファイル | Binary file | Data file name | 参考訳 |
| ダンプ表示 | Dump | Dump | 原本併記 |
| モニタ開始 / 終了 | Monitor start / end | [Monitor Start] / [Monitor End] / Start monitor | 原本併記 |
| CPU形名 / CPU固有コード | CPU model name / CPU type code | PLC CPU type / PLC CPU type code | 原本併記 |
| バインディングの選択 | Select the binding | [アドイン]タブ⇒[Select the binding] | 原本併記 |

## 変換範囲表

| 原本ページ(PDF) | 印刷ページ | 節 | 扱い |
|---|---|---|---|
| p.605-606 | 603-604 | 12章冒頭(注意事項，ビルド時のエラー，サンプルプログラム一覧) | 全文 |
| p.607-610 | 605-608 | 12.1 Visual Basic.NET，Visual C#，Visual C++ (Act_2019.sln，Dot_2019.sln / ActDatalogging_2019.sln) | 全文(画面は表示項目を文章化) |
| p.611-617 | 609-615 | 12.2 VBA (Access用 / Excel用) | 全文(画面は表示項目を文章化) |
| p.618 | 616 | (MEMOページ) | 除外: 白紙のMEMOページで内容なし |
| p.1-17 | — | 前付け | **未変換** |
| p.18-604 | 16-602 | 1章〜11章 | 別ファイル(01_〜11-8_) |
| p.619-696 | 617- | 13章〜付録・関数索引・改訂履歴ほか | **未変換** |

## 目次

- 12章冒頭
  - 注意事項 / サンプルプログラムをビルドしたときのエラーについて
  - サンプルプログラム一覧(Visual Basic.NET / Visual C# / Visual C++ / VBA(Access) / VBA(Excel))
- 12.1 Visual Basic.NET，Visual C#，Visual C++
  - Act_2019.sln，Dot_2019.sln
  - ActDatalogging_2019.sln
- 12.2 VBA
  - Access用(ActTest_EarlyBind.accdb，ActTest_LateBind.accdb，ActTest64.accdb): メニュー画面 / Method画面 / GetErrorMessage画面
  - Excel用(ActUtlType.xlsm，ActUtlType64.xlsm，ActProgType.xlsm，ActProgType64.xlsm)

---

## 12 サンプルプログラム (12 / 603-604 / 原本 p.605-606)

MX Componentインストール時に登録されるサンプルプログラムについて説明します。

### 注意事項 (12 / 603 / 原本 p.605)

- サンプルプログラムは，インストール時に(インストールフォルダ)\Samplesに格納されます。サンプルプログラムを実行する際は，任意のフォルダにコピーしてから使用してください。VC++のサンプルを使用する場合は，include ファイルもコピーしてください。
- サンプルプログラムはユーザプログラムを作成する際に，参考にしていただくために添付しています。これらは，お客様の責任においてご使用ください。

#### サンプルプログラムをビルドしたときのエラーについて (12 / 603 / 原本 p.605)

- 「System.Runtime.InteropServices.COMExceptionはハンドルされませんでした。」というエラーが発生した場合，MX Componentを使用したプログラムを作成するときのターゲットCPUに"x86"(32ビット)を指定してください。
- 64ビットプログラムからMX Componentを使用する場合，64ビット用コントロールを使用してください。

### サンプルプログラム一覧 (12 / 603-604 / 原本 p.605-606)

MX Componentインストール時に(インストールフォルダ)\Samples内に登録されるサンプルプログラム一覧を下記に示します。

#### 対応言語: Visual Basic.NET (12 / 603 / 原本 p.605)

| フォルダ名 | サンプルプログラム名 | 対象コントロール | 参照 |
|---|---|---|---|
| Vb.Net\Act | Visual Studio 2019: Act_2019.sln<br>Visual Studio 2022: Act_2022.sln<br>Visual Studio 2026: Act_2026.sln | ActUtlType<br>ActProgType<br>ActSupportMsg<br>ActUtlType64<br>ActProgType64<br>ActSupportMsg64 | ☞605ページ Act_2019.sln，Dot_2019.sln |
| Vb.Net\ActDatalogging | Visual Studio 2019: ActDatalogging_2019.sln<br>Visual Studio 2022: ActDatalogging_2022.sln<br>Visual Studio 2026: ActDatalogging_2026.sln | ActUtlDataLogging<br>ActProgDataLoging<br>ActUtlDataLogging64<br>ActProgDataLoging64 | ☞608ページ ActDatalogging_2019.sln |
| Vb.Net\Dot | Visual Studio 2019: Dot_2019.sln<br>Visual Studio 2022: Dot_2022.sln<br>Visual Studio 2026: Dot_2026.sln | DotUtlType<br>DotUtlType64 | ☞605ページ Act_2019.sln，Dot_2019.sln |

※「ActProgDataLoging」(gが1つ)は原本表記のまま(要確認: 正式名は ActProgDataLogging)。Visual C# / Visual C++ の表も同じ。

#### 対応言語: Visual C# (12 / 603 / 原本 p.605)

| フォルダ名 | サンプルプログラム名 | 対象コントロール | 参照 |
|---|---|---|---|
| Vcs.NET\Act | Visual Studio 2019: Act_2019.sln<br>Visual Studio 2022: Act_2022.sln<br>Visual Studio 2026: Act_2026.sln | ActUtlType<br>ActProgType<br>ActSupportMsg<br>ActUtlType64<br>ActProgType64<br>ActSupportMsg64 | ☞605ページ Act_2019.sln，Dot_2019.sln |
| Vcs.NET\ActDatalogging | Visual Studio 2019: ActDatalogging_2019.sln<br>Visual Studio 2022: ActDatalogging_2022.sln<br>Visual Studio 2026: ActDatalogging_2026.sln | ActUtlDataLogging<br>ActProgDataLoging<br>ActUtlDataLogging64<br>ActProgDataLoging64 | ☞608ページ ActDatalogging_2019.sln |
| Vcs.NET\Dot | Visual Studio 2019: Dot_2019.sln<br>Visual Studio 2022: Dot_2022.sln<br>Visual Studio 2026: Dot_2026.sln | DotUtlType<br>DotUtlType64 | ☞605ページ Act_2019.sln，Dot_2019.sln |

#### 対応言語: Visual C++ (12 / 604 / 原本 p.606)

| フォルダ名 | サンプルプログラム名 | 対象コントロール | 参照 |
|---|---|---|---|
| Vc\Act | Visual Studio 2019: Act_2019.sln<br>Visual Studio 2022: Act_2022.sln<br>Visual Studio 2026: Act_2026.sln | ActUtlType<br>ActProgType<br>ActSupportMsg<br>ActUtlType64<br>ActProgType64<br>ActSupportMsg64 | ☞605ページ Act_2019.sln，Dot_2019.sln |
| Vc\ActDatalogging | Visual Studio 2019: ActDatalogging_2019.sln<br>Visual Studio 2022: ActDatalogging_2022.sln<br>Visual Studio 2026: ActDatalogging_2026.sln | ActUtlDataLogging<br>ActProgDataLoging<br>ActUtlDataLogging64<br>ActProgDataLoging64 | ☞608ページ ActDatalogging_2019.sln |

#### 対応言語: VBA(Access) (12 / 604 / 原本 p.606)

| フォルダ名 | サンプルプログラム名 | 対象コントロール | 参照 |
|---|---|---|---|
| VBA\Access | EarlyBind用: ActTest_EarlyBind.accdb*1<br>LateBind用: ActTest_LateBind.accdb*2 | ActUtlType<br>ActProgType<br>ActSupportMsg | ☞609ページ Access用(ActTest_EarlyBind.accdb，ActTest_LateBind.accdb，ActTest64.accdb) |
| VBA\Access(同上) | LateBind用: ActTest64.accdb*2 | ActUtlType64<br>ActProgType64<br>ActSupportMsg64 | ☞609ページ Access用(ActTest_EarlyBind.accdb，ActTest_LateBind.accdb，ActTest64.accdb) |

> *1 フォームに貼り付けて使用する場合のサンプルです。
> *2 オブジェクトを生成して使用する場合のサンプルです。

#### 対応言語: VBA(Excel) (12 / 604 / 原本 p.606)

| フォルダ名 | サンプルプログラム名 | 対象コントロール | 参照 |
|---|---|---|---|
| VBA\Excel | EarlyBind用およびLateBind用: ActUtlType.xlsm*1*2 | ActUtlType<br>ActSupportMsg | ☞613ページ Excel用(ActUtlType.xlsm，ActUtlType64.xlsm，ActProgType.xlsm，ActProgType64.xlsm) |
| VBA\Excel(同上) | EarlyBind用およびLateBind用: ActProgType.xlsm*1*2 | ActProgType | (同上) |
| VBA\Excel(同上) | LateBind用: ActUtlType64.xlsm*2 | ActutlType64<br>ActSupportMsg64 | ☞613ページ Excel用(ActUtlType.xlsm，ActUtlType64.xlsm，ActProgType.xlsm，ActProgType64.xlsm) |
| VBA\Excel(同上) | LateBind用: ActProgType64.xlsm*2 | ActProgType64 | (同上) |

※参照セルは原本では上2行・下2行でそれぞれ共有。「ActutlType64」(小文字u)は原本表記のまま。

> *1 フォームに貼り付けて使用する場合のサンプルです。
> *2 オブジェクトを生成して使用する場合のサンプルです。

---

## 12.1 Visual Basic.NET，Visual C#，Visual C++ (12.1 / 605-608 / 原本 p.607-610)

### Act_2019.sln，Dot_2019.sln (12.1 / 605-607 / 原本 p.607-609)

**画面表示**

【図】サンプル画面「ActControl_Sample2019」 (12.1 / 605 / 原本 p.607)
- 左上 Control: ラジオボタン ActUtlType(選択) / ActProgType，LogicalStationNumber欄，Password欄，[Open] [Close]
- Get/Set: DeviceName欄，DeviceData欄，[GetDevice2] [GetDevice] [SetDevice2] [SetDevice]
- Random Read/Write: DeviceName(複数行)，DeviceSize，DeviceData(複数行)，[ReadDeviceRandom2] [ReadDeviceRandom] [WriteDeviceRandom2] [WriteDeviceRandom]
- Block Read/Write: DeviceName，DeviceSize，DeviceData(複数行)，[ReadDeviceBlock2] [ReadDeviceBlock] [WriteDeviceBlock2] [WriteDeviceBlock]
- Status Entry/Free: DeviceName(複数行)，DeviceSize，MonitorCycle，DeviceData(複数行)，[EntryDeviceStatus] [FreeDeviceStatus](グレー表示)
- Output: Return Code欄，Data欄(複数行)
- 右上 Message: Code欄，[GetErrorMessage]
- CpuType: [GetCpuType] / Status: Status欄(注記「0 : RUN，1 : STOP，2 : Pause」)，[SetCpuStatus]
- Clock: Year / Month / Day / Week / Hour / Minute / Second欄，[GetClockData] [SetClockData]
- Buffer Read/Write: I/OAddress / BufferAddress / BufferSize欄，BufferData(複数行)，[ReadBuffer] [WriteBuffer]
- SampleUsingTimer: DeviceName欄，[Start] [Stop](グレー表示)

**表示内容**

| フレーム | 選択/入力項目 | 内容 |
|---|---|---|
| Control | ActUtlType，ActProgType*1 | 使用するコントロールを選択します。 |
| Control | LogicalStationNumber | 通信設定ユーティリティにて通信設定を行った論理局番を入力します。 |
| Control | Password | パスワードが必要なCPUを使用している場合，パスワードを入力します。 |
| Control | [Open]ボタン | 通信回線をオープンします。 |
| Control | [Close]ボタン | 通信回線をクローズします。 |
| Get/Set | DeviceName/LabelName*2 | デバイス取得/設定を行うデバイス名/ラベル名を入力します。 |
| Get/Set | DeviceData | デバイス設定を行うデバイス値を入力します。 |
| Get/Set | [GetDevice2]ボタン | 同フレーム内の"DeviceName"("LabelName")欄に入力されたデータでGetDevice2を実行し，デバイスデータをCPUユニットから取得します。*3 |
| Get/Set | [SetDevice2]ボタン | 同フレーム内の"DeviceName"("LabelName")欄および"DeviceData"欄に入力されたデータでSetDevice2を実行し，デバイスデータをCPUユニットに設定します。 |
| Get/Set | [GetDevice]ボタン | 同フレーム内の"DeviceName"("LabelName")欄に入力されたデータでGetDeviceを実行し，デバイスデータをCPUユニットから取得します。*3 |
| Get/Set | [SetDevice]ボタン | 同フレーム内の"DeviceName"("LabelName")欄および"DeviceData"欄に入力されたデータでSetDeviceを実行し，デバイスデータをCPUユニットに設定します。 |
| Random Read/Write | DeviceName/LabelName*2 | ランダム読出し/書込みを行うデバイス名/ラベル名を入力します。 |
| Random Read/Write | DeviceSize | ランダム読出し/書込みを行うデバイスの点数を入力します。 |
| Random Read/Write | DeviceData | ランダム書込みを行うデバイス値を入力します。 |
| Random Read/Write | [ReadDeviceRandom2]ボタン | 同フレーム内の"DeviceName"("LabelName")欄および"DeviceSize"欄に入力されたデータでReadDeviceRandom2を実行し，デバイスデータをCPUユニットから取得します。*3 |
| Random Read/Write | [WriteDeviceRandom2]ボタン | 同フレーム内の"DeviceName"("LabelName")欄，"DeviceSize"欄および"DeviceData"欄に入力されたデータでWriteDeviceRandom2を実行し，デバイスデータをCPUユニットに設定します。 |
| Random Read/Write | [ReadDeviceRandom]ボタン | 同フレーム内の"DeviceName"("LabelName")欄および"DeviceSize"欄に入力されたデータでReadDeviceRandomを実行し，デバイスデータをCPUユニットから取得します。*3 |
| Random Read/Write | [WriteDeviceRandom]ボタン | 同フレーム内の"DeviceName"("LabelName")欄，"DeviceSize"欄および"DeviceData"欄に入力されたデータでWriteDeviceRandomを実行し，デバイスデータをCPUユニットに設定します。 |
| Block Read/Write | DeviceName/LabelName*2 | 一括読出し/書込みを行うデバイス名/ラベル名を入力します。 |
| Block Read/Write | DeviceSize | 一括読出し/書込みを行うデバイスの点数を入力します。 |
| Block Read/Write | DeviceData | 一括書込みを行うデバイス値を入力します。 |
| Block Read/Write | [ReadDeviceBlock2]ボタン | 同フレーム内の"DeviceName"("LabelName")欄および"DeviceSize"欄に入力されたデータでReadDeviceBlock2を実行し，デバイスデータをCPUユニットから取得します。*3 |
| Block Read/Write | [WriteDeviceBlock2]ボタン | 同フレーム内の"DeviceName"("LabelName")欄，"DeviceSize"欄および"DeviceData"欄に入力されたデータでWriteDeviceBlock2を実行し，デバイスデータをCPUユニットに設定します。 |
| Block Read/Write | [ReadDeviceBlock]ボタン | 同フレーム内の"DeviceName"("LabelName")欄および"DeviceSize"欄に入力されたデータでReadDeviceBlockを実行し，デバイスデータをCPUユニットから取得します。*3 |
| Block Read/Write | [WriteDeviceBlock]ボタン | 同フレーム内の"DeviceName"("LabelName")欄，"DeviceSize"欄および"DeviceData"欄に入力されたデータでWriteDeviceBlockを実行し，デバイスデータをCPUユニットに設定します。 |
| Status Entry/Free*4 | DeviceName/LabelName*2 | デバイス状態監視を行うデバイス名/ラベル名を入力します。 |
| Status Entry/Free*4 | DeviceSize | デバイス状態監視のデバイス点数を入力します。 |
| Status Entry/Free*4 | MonitorCycle | デバイス状態監視の状態監視間隔時間を入力します。 |
| Status Entry/Free*4 | DeviceData | デバイス監視の登録デバイス値を入力します。 |
| Status Entry/Free*4 | [EntryDeviceStatus]ボタン | 同フレーム内の"DeviceName"("LabelName")欄，"DeviceSize"欄，"MonitorCycle"欄，および"DeviceData"欄に入力されたデータでEntryDeviceStatusを実行し，デバイス監視登録を行います。 |
| Status Entry/Free*4 | [FreeDeviceStatus]ボタン | EntryDeviceStatus にて登録した，状態監視を行うデバイスを解除します。 |
| Output | ReturnCode | 各メソッド(関数)の実行結果を表示します。 |
| Output | Data | 読み出したデバイス値を表示します。 |
| Message | Code | メッセージコードを入力します。 |
| Message | [GetErrorMessage]ボタン | 同フレーム内の"Code"欄に入力されたデータでGetErrorMessageを実行し，メッセージを取得します。*3 |
| CpuType | [GetCpuType]ボタン | GetCpuTypeを実行し，CPUユニットから形名文字列と形名コード(16進)を取得します。*3 |
| Status | Status | 設定するリモートコントロールを入力します。 |
| Status | [SetCpuStatus]ボタン | 同フレーム内の"Status"欄に入力されたデータでSetCpuStatusを実行し，リモートコントロールをCPUユニットに設定します。 |
| Clock | Year | CPUユニットに設定する年を入力します。 |
| Clock | Month | CPUユニットに設定する月を入力します。 |
| Clock | Day | CPUユニットに設定する日を入力します。 |
| Clock | Week | CPUユニットに設定する曜日を入力します。 |
| Clock | Hour | CPUユニットに設定する時を入力します。 |
| Clock | Minute | CPUユニットに設定する分を入力します。 |
| Clock | Second | CPUユニットに設定する秒を入力します。 |
| Clock | [GetClockData]ボタン | CPUユニットから時計データを取得します。*3 |
| Clock | [SetClockData]ボタン | 同フレーム内の"Year"欄，"Month"欄，"Day"欄，"Week"欄，"Hour"欄，"Minute"欄および"Second"欄に入力されたデータで，CPUユニットに時計データを設定します。 |
| Buffer Read/Write | I/OAdress | バッファメモリ読出し/書込みを行うI/Oアドレスを入力します。 |
| Buffer Read/Write | BufferAddress | バッファメモリ読出し/書込みを行うアドレスを入力します。 |
| Buffer Read/Write | BufferSize | バッファメモリ読出し/書込みを行うサイズを入力します。 |
| Buffer Read/Write | BufferData | バッファメモリ読出し/書込みを行うデータを入力します。 |
| Buffer Read/Write | [ReadBuffer]ボタン | 同フレーム内の"I/OAdress"欄，"BufferAddress"欄および"BufferSize"欄に入力されたデータでReadBufferを実行し，デバイスデータをCPUユニットから取得します。*3 |
| Buffer Read/Write | [WriteBuffer]ボタン | 同フレーム内の"I/OAdress"欄，"BufferAddress"欄，"BufferSize"欄および"BufferData"欄に入力されたデータでWriteBufferを実行し，デバイスデータをCPUユニットに設定します。 |
| Sample Using Timer | DeviceName/LabelName*2 | 読み出しを行うデバイス名/ラベル名を入力します。 |
| Sample Using Timer | [Start]ボタン | 同フレーム内の"DeviceName"("LabelName")欄に入力されたデータで，ReadDeviceRandomを実行し，デバイスデータをCPUユニットから取得します。*3ReadDeviceRandomは，[Stop]ボタンをクリックするまで5秒に1度実行されます。 |
| Sample Using Timer | [Stop]ボタン | 同フレーム内の[Start]ボタンで開始された処理を終了します。 |

※表は原本 p.607〜p.609 の3ページにまたがる1つの表。「I/OAdress」は原本表記のまま(画面上の表記は「I/OAddress」)。

> *1 Act_2019.slnのみ表示されます。Dot_2019.slnでは表示されません。
> *2 Act_2019.slnの場合はDeviceName，Dot_2019.slnの場合はLabelNameが表示されます。
> *3 取得結果は"Output"フレームの"Data"欄に表示されます。
> *4 Visual C++のサンプルプログラムでは表示されません。

**操作手順** (12.1 / 607 / 原本 p.609)

1. "Control"項目で使用するコントロール(ActUtlTypeまたはActProgType)を選択します。
2. "LogicalStationNumber"欄に論理局番を入力します。
3. [Open]ボタンをクリックし，通信回線をオープンします。
4. 各項目でメソッド(関数)の引数となるデータを入力後，メソッド(関数)のボタンをクリックし，関数を実行します。
   "Output"項目の"Data"欄に読み出したデバイス値を，"ReturnCode"欄に各メソッド(関数)の実行結果を表示します。
5. "Control"項目で[Close]ボタンをクリックし，通信回線をクローズします。

### ActDatalogging_2019.sln (12.1 / 608 / 原本 p.610)

**画面表示**

【図】サンプル画面「ActControlDatalogging_Sample2019」 (12.1 / 608 / 原本 p.610)
- ラジオボタン ActUtlDataLogging(選択) / ActProgDataLogging，ReturnCode欄
- FolderName欄(初期表示例「/LOGGING」)，[Display] [Select] [Save] [Close]，左下にファイルリスト欄

**表示内容**

| 項目 | 内容 |
|---|---|
| ActUtlDataLogging /ActProgDataLogging | 使用するコントロールを選択します。 |
| ReturnCode | 各メソッドの実行結果を表示します。 |
| FolderName | アクセスするフォルダ名を入力します。 |
| [Display]ボタン | "ファイルリスト"欄に表示されている内容を更新します。 |
| [Select]ボタン | "ファイルリスト"欄で選択したフォルダ名を"FolderName"に反映します。ファイル名を選択している場合，ロギングファイルをパソコンに保存します。 |
| [Save]ボタン | "名前を付けて保存"画面を表示します。"ファイルの種類"は，テキストファイル(*.txt)のみ選択できます。 |
| [Close]ボタン | サンプルプログラムを終了します。 |
| ファイルリスト | "フォルダ名"欄に指定したパス内のファイル/フォルダを一覧で表示します。フォルダの場合，フォルダ名の先頭はスラッシュ「/」で始まります。 |

---

## 12.2 VBA (12.2 / 609-615 / 原本 p.611-617)

Access，Excel用のVBAサンプルプログラムについて説明します。

### Access用(ActTest_EarlyBind.accdb，ActTest_LateBind.accdb，ActTest64.accdb) (12.2 / 609-612 / 原本 p.611-614)

#### メニュー画面 (12.2 / 609 / 原本 p.611)

**画面表示**

【図】「Menu」画面 (12.2 / 609 / 原本 p.611)
- タイトル「MX ComponentVer5 Test Menu」，日付表示「21/01/27」
- Controls枠: [ActUtlType64] [ActProgType64] [ActSupportMsg64](画面例は ActTest64.accdb)
- 下部の注記(英文): 「A numeric input becomes a decimal. Please add "0x" to the head in case of the hexadecimal.」

**表示内容**

| 項目名 | 内容 |
|---|---|
| [ActUtlType]ボタン*1 | ActUtlTypeコントロール用(ActUtlType64コントロール用)のMethod画面を開きます。 |
| [ActUtlType64]ボタン*2 | (同上) |
| [ActProgType]ボタン*1 | ActProgTypeコントロール用(ActProgType64コントロール用)のMethod画面を開きます。 |
| [ActProgType64]ボタン*2 | (同上) |
| [ActSupportMsg]ボタン*1 | ActSupportMsgコントロール用(ActSupportMsg64コントロール用)のMethod画面を開きます。 |
| [ActSupportMsg64]ボタン*2 | (同上) |

> *1 ActTest_EarlyBind.accdb，ActTest_LateBind.accdb使用時
> *2 ActTest64.accdb使用時

#### Method画面 (12.2 / 610-611 / 原本 p.612-613)

**画面表示**

【図】「Method」画面(画面例は ActUtlType64) (12.2 / 610 / 原本 p.612)
- タブ(3段): ReadBuffer / WriteBuffer / GetCpuType / SetCpuStatus / GetClockData / SetClockData / GetDevice2，SetDevice2 / ReadDeviceBlock2 / WriteDeviceBlock2 / ReadDeviceRandom2 / WriteDeviceRandom2，Open / Close / GetDevice / SetDevice / ReadDeviceBlock / WriteDeviceBlock / ReadDeviceRandom / WriteDeviceRandom
- [Open]タブ選択時の表示: 「There is no parameter in this method.」
- 右側: [Property]，Result欄，[Execute]，Interval(S)欄(初期表示「1」)，[Monitor Start] [Monitor End](グレー表示)，[Close]

**表示内容**

| タブ名 | 項目 | 内容 |
|---|---|---|
| — | [Property]ボタン | プロパティを設定します。 |
| — | Result | 各メソッド(関数)の実行結果を表示します。 |
| — | [Execute]ボタン | 選択中のタブのメソッド(関数)を実行します。 |
| — | Interval(S) | モニタする時間間隔(秒)が表示されます。 |
| — | [Monitor Start]ボタン | ReadDeviceBlock/ReadDeviceBlock2のモニタを開始します。"Interval(S)"欄の時間が経過するごとにメソッド(関数)を実行し，データを取得します。 |
| — | [Monitor End]ボタン | ReadDeviceBlock/ReadDeviceBlock2のモニタを終了します。 |
| — | [Close]ボタン | メニュー画面に戻ります。 |
| Open | — | — |
| Close | — | — |
| GetDevice，GetDevice2 | Device Name | デバイス取得を行うデバイス名を入力します。 |
| GetDevice，GetDevice2 | Device Data | 取得したデバイス値を表示します。 |
| SetDevice，SetDevice2 | Device Name | デバイス設定を行うデバイス名を入力します。 |
| SetDevice，SetDevice2 | Device Data | デバイス設定を行うデバイス値を入力します。 |
| ReadDeviceRandom，ReadDeviceRandom2 | Device Name | ランダム読出しを行うデバイス名を入力します。 |
| ReadDeviceRandom，ReadDeviceRandom2 | Device Points | ランダム読出しを行うデバイスの点数を入力します。 |
| ReadDeviceRandom，ReadDeviceRandom2 | Data file name | 読み出したデータを保存する場合，保存先のバイナリファイル名を指定します。 |
| ReadDeviceRandom，ReadDeviceRandom2 | Dump | チェックボックスにチェックが入っている場合，読み出したデータを表示します。 |
| WriteDeviceRandom，WriteDeviceRandom2 | Device Name | ランダム書込みを行うデバイス名を入力します。 |
| WriteDeviceRandom，WriteDeviceRandom2 | Device Points | ランダム書込みを行うデバイスの点数を入力します。 |
| WriteDeviceRandom，WriteDeviceRandom2 | Written device value | ランダム書込みを行うデバイス値を入力します。指定データ以外を選択することで，データの自動入力が可能です。 |
| ReadDeviceBlock，ReadDeviceBlock2 | Device Name | 一括読出しを行うデバイス名を入力します。 |
| ReadDeviceBlock，ReadDeviceBlock2 | Device Points | 一括読出しを行うデバイスの点数を入力します。 |
| ReadDeviceBlock，ReadDeviceBlock2 | Data file name | 読み出したデータを保存する場合，保存先のバイナリファイル名を指定します。 |
| ReadDeviceBlock，ReadDeviceBlock2 | Dump | チェックボックスにチェックが入っている場合，読み出したデータを表示します。 |
| WriteDeviceBlock，WriteDeviceBlock2 | Device Name | 一括書込みを行うデバイス名を入力します。 |
| WriteDeviceBlock，WriteDeviceBlock2 | Device Points | 一括書込みを行うデバイスの点数を入力します。 |
| WriteDeviceBlock，WriteDeviceBlock2 | Written device value | ランダム書込みを行うデバイス値を入力します。指定データ以外を選択することで，データの自動入力が可能です。 |
| EntryDeviceStatus*1 | Device Name | デバイス状態監視を行うデバイス名を入力します。 |
| EntryDeviceStatus*1 | Points | デバイス状態監視のデバイス点数を入力します。 |
| EntryDeviceStatus*1 | Interval | デバイス状態監視の状態監視間隔時間を入力します。 |
| EntryDeviceStatus*1 | Device value | デバイス監視の登録デバイス値を入力します。 |
| FreeDeviceStatus*1 | — | — |
| GetCpuType | PLC CPU type | 取得したCPU形名を表示します。 |
| GetCpuType | PLC CPU type code | 取得したCPU固有コードを表示します。 |
| SetCpuStatus | Operation | 設定するリモートコントロールを入力します。 |
| GetClockData，SetClockData | Year | CPUユニットに設定する年を入力/表示します。 |
| GetClockData，SetClockData | Month | CPUユニットに設定する月を入力/表示します。 |
| GetClockData，SetClockData | Day | CPUユニットに設定する日を入力/表示します。 |
| GetClockData，SetClockData | WeekDay | CPUユニットに設定する曜日を入力/表示します。 |
| GetClockData，SetClockData | Hour | CPUユニットに設定する時を入力/表示します。 |
| GetClockData，SetClockData | Minute | CPUユニットに設定する分を入力/表示します。 |
| GetClockData，SetClockData | Second | CPUユニットに設定する秒を入力/表示します。 |
| ReadBuffer | First I/O address | バッファメモリ読出しを行うI/Oアドレスを入力します。 |
| ReadBuffer | Buffer memory address | バッファメモリ読出しを行うアドレスを入力します。 |
| ReadBuffer | Read size | バッファメモリ読出しを行うサイズを入力します。 |
| ReadBuffer | Data file name | 読み出したデータを保存する場合，保存先のバイナリファイル名を指定します。 |
| ReadBuffer | Dump | チェックボックスにチェックが入っている場合，読み出したデータを表示します。 |
| WriteBuffer | First I/O address | バッファメモリ書込みを行うI/Oアドレスを入力します。 |
| WriteBuffer | Buffer memory address | バッファメモリ書込みを行うアドレスを入力します。 |
| WriteBuffer | Write size | バッファメモリ書込みを行うサイズを入力します。 |
| WriteBuffer | Values written to buffer memory | バッファメモリ書込みを行うデバイス値を入力します。指定データ以外を選択することで，データの自動入力が可能です。 |

※表は原本 p.612〜p.613 の2ページにまたがる1つの表。WriteDeviceBlock の "Written device value" の内容が「ランダム書込みを行う…」となっているのは原本どおり(要確認: 一括書込みの誤記と思われる)。

> *1 ActTest_EarlyBind.accdb使用時にのみ表示されます。

**操作手順** (12.2 / 611 / 原本 p.613)

1. [Property]ボタンをクリックし，プロパティを設定します。
2. [Open]タブを選択し，[Execute]ボタンをクリックし，通信回線をオープンします。
3. 実行するメソッド(関数)のタブを選択し，引数となるデータを入力後，[Execute]ボタンをクリックします。
   "Dump"にチェックが入っている場合は画面下部に読み出したデバイス値を表示します。
   "Result"欄には各メソッド(関数)の実行結果を表示します。
4. [Close]タブを選択し，[Execute]ボタンをクリックし，通信回線をクローズします。

#### GetErrorMessage画面 (12.2 / 612 / 原本 p.614)

**画面表示**

【図】「GetErrorMessage」画面 (12.2 / 612 / 原本 p.614)
- Error code欄，Trouble shooting欄(複数行)，Result欄，[Execute] [Close]

**表示内容**

| 項目名 | 内容 |
|---|---|
| Error code | メッセージコードを入力します。 |
| Trouble shooting | 取得したメッセージを表示します。 |
| Result | GetErrorMessageの実行結果を表示します。 |
| [Execute]ボタン | "Error code"欄に入力されたデータでGetErrorMessageを実行します。 |
| [Close]]ボタン | メニュー画面に戻ります。 |

※「[Close]]ボタン」(閉じ括弧が2つ)は原本表記のまま。

### Excel用(ActUtlType.xlsm，ActUtlType64.xlsm，ActProgType.xlsm，ActProgType64.xlsm) (12.2 / 613-615 / 原本 p.615-617)

**画面表示**

【図】Excelシート画面(画面例は ActProgType64.xlsm，シート名「ActProgType(Late)」) (12.2 / 613 / 原本 p.615)
- 上部: ActOpen method [Open]，ActClose method [Close]，RESULT欄(初期値0)，Other method(コンボボックス，表示例「GetDevice」)，Other methods are executed. [Execute]，[Property]，凡例 IN(水色)/OUT(黄色)
- 注記(英文): 「A numeric input becomes a decimal. Please add "0x" to the head in case of the hexadecimal.」
- 右上: [GetErrorMessage]，ErrorCode(Hex)欄，RESULT欄(初期値0)，メッセージ表示枠
- 本体: 「GetDevice method information」(Device name / Device value)，「SetDevice method information」(Device name / Device value) などメソッドごとの入力ブロック
- リボンに「MX Sheet」タブ

**表示内容**

| メソッド(関数) | 項目 | 内容 |
|---|---|---|
| Open | [Open]ボタン | 通信回線をオープンします。 |
| Close | [Close]ボタン | 通信回線をクローズします。 |
| — | RESULT | 各メソッド(関数)の実行結果を表示します。 |
| — | Other method | コンボボックスで選択したメソッド(関数)の位置までセルが移動します。 |
| — | [Execute]ボタン | コンボボックスで選択中のメソッド(関数)を，入力データをもとに実行します。 |
| — | [Property]ボタン | ActUtlType/ActProgTypeのプロパティ値を設定します。 |
| — | Result | 各メソッド(関数)の実行結果を表示します。 |
| GetDevice，GetDevice2 | Device name | デバイス取得を行うデバイス名を入力します。 |
| GetDevice，GetDevice2 | Device value | 取得したデバイス値を表示します。 |
| SetDevice，SetDevice2 | Device name | デバイス設定を行うデバイス名を入力します。 |
| SetDevice，SetDevice2 | Device value | デバイス設定を行うデバイス値を入力します。 |
| ReadDeviceRandom，ReadDeviceRandom2 | Device name | ランダム読出しを行うデバイス名を入力します。 |
| ReadDeviceRandom，ReadDeviceRandom2 | Points | ランダム読出しを行うデバイスの点数を入力します。 |
| ReadDeviceRandom，ReadDeviceRandom2 | Data file name | 読み出したデータを保存する場合，保存先のバイナリファイル名を指定します。 |
| ReadDeviceRandom，ReadDeviceRandom2 | Dump | チェックボックスにチェックが入っている場合，読み出したデータを表示します。 |
| WriteDeviceRandom，WriteDeviceRandom2 | Device name | ランダム書込みを行うデバイス名を入力します。 |
| WriteDeviceRandom，WriteDeviceRandom2 | Points | ランダム書込みを行うデバイスの点数を入力します。 |
| WriteDeviceRandom，WriteDeviceRandom2 | Device value | ランダム書込みを行うデバイス値を入力します。指定データ以外を選択することで，データの自動入力が可能です。 |
| ReadDeviceBlock，ReadDeviceBlock2 | Device name | 一括読出しを行うデバイス名を入力します。 |
| ReadDeviceBlock，ReadDeviceBlock2 | Points | 一括読出しを行うデバイスの点数を入力します。 |
| ReadDeviceBlock，ReadDeviceBlock2 | Data file name | 読み出したデータを保存する場合，保存先のバイナリファイル名を指定します。 |
| ReadDeviceBlock，ReadDeviceBlock2 | Dump | チェックボックスにチェックが入っている場合，読み出したデータを表示します。 |
| ReadDeviceBlock，ReadDeviceBlock2 | Interval(sec) | モニタする時間間隔(秒)を入力します。 |
| ReadDeviceBlock，ReadDeviceBlock2 | Start monitor | メソッド(関数)のモニタを開始します。"モニタ間隔(s)"欄の時間が経過するごとにメソッド(関数)を実行し，データを取得します。 |
| WriteDeviceBlock，WriteDeviceBlock2 | Device name | 一括書込みを行うデバイス名を入力します。 |
| WriteDeviceBlock，WriteDeviceBlock2 | Points | 一括書込みを行うデバイスの点数を入力します。 |
| WriteDeviceBlock，WriteDeviceBlock2 | Device value | ランダム書込みを行うデバイス値を入力します。指定データ以外を選択することで，データの自動入力が可能です。 |
| EntryDeviceStatus*1 | Device name | デバイス状態監視を行うデバイス名を入力します。 |
| EntryDeviceStatus*1 | Points | デバイス状態監視のデバイス点数を入力します。 |
| EntryDeviceStatus*1 | Interval(sec) | デバイス状態監視の状態監視間隔時間(秒)を入力します。 |
| EntryDeviceStatus*1 | Device value | デバイス監視の登録デバイス値を入力します。 |
| OnDeviceStatus*1 | Device and value to which condition consists. | OnDeviceStatusイベントの結果を表示します。 |
| FreeDeviceStatus*1 | — | — |
| GetCpuType | CPU type | 取得したCPU形名を表示します。 |
| GetCpuType | CPU type code | 取得したCPU固有コードを表示します。 |
| SetCpuStatus | Operation | 設定するリモートコントロールを入力します。 |
| GetClockData，SetClockData | Year | CPUユニットに設定する年を入力/表示します。 |
| GetClockData，SetClockData | Month | CPUユニットに設定する月を入力/表示します。 |
| GetClockData，SetClockData | Day | CPUユニットに設定する日を入力/表示します。 |
| GetClockData，SetClockData | Day-of-week | CPUユニットに設定する曜日を入力/表示します。 |
| GetClockData，SetClockData | Hour | CPUユニットに設定する時を入力/表示します。 |
| GetClockData，SetClockData | Minute | CPUユニットに設定する分を入力/表示します。 |
| GetClockData，SetClockData | Second | CPUユニットに設定する秒を入力/表示します。 |
| ReadBuffer | First I/O address | バッファメモリ読出しを行うI/Oアドレスを入力します。 |
| ReadBuffer | Buffer memory address | バッファメモリ読出しを行うアドレスを入力します。 |
| ReadBuffer | Read size | バッファメモリ読出しを行うサイズを入力します。 |
| ReadBuffer | Data file name | 読み出したデータを保存する場合，保存先のバイナリファイル名を指定します。 |
| ReadBuffer | Dump | チェックボックスにチェックが入っている場合，読み出したデータを表示します。 |
| WriteBuffer | First I/O address | バッファメモリ書込みを行うI/Oアドレスを入力します。 |
| WriteBuffer | Buffer memory address | バッファメモリ書込みを行うアドレスを入力します。 |
| WriteBuffer | Write size | バッファメモリ書込みを行うサイズを入力します。 |
| WriteBuffer | Device value | バッファメモリ書込みを行うデバイス値を入力します。指定データ以外を選択することで，データの自動入力が可能です。 |
| GetErrorMessage | [GetErrorMessage]ボタン | "ErrorCode(Hex)"に入力されたデータをもとに，GetErrorMessageを実行します。取得したメッセージをボタンの右のテキストに出力します。 |
| GetErrorMessage | ErrorCode(Hex) | メッセージコードを入力します。 |
| GetErrorMessage | RESULT | GetErrorMessageの実行結果を表示します。 |

※表は原本 p.615〜p.616 の2ページにまたがる1つの表。ReadDeviceBlock の "Start monitor" の説明中の「"モニタ間隔(s)"欄」は，項目名「Interval(sec)」と表記が異なる(原本どおり)。WriteDeviceBlock の "Device value" の「ランダム書込み」も原本どおり(要確認)。

> *1 フォームに貼り付けて使用する場合(EarlyBind)にのみ表示されます。

> **Point**
> フォームに貼り付けて使用する場合(EarlyBind)とオブジェクトを生成して使用する場合(LateBind)は，Excelの[アドイン]タブ⇒[Select the binding]⇒[Early binding]/[Late binding]で切り替えてください。

**操作手順** (12.2 / 615 / 原本 p.617)

1. [Property]ボタンをクリックし，プロパティを設定します。
2. [Open]ボタンをクリックし，通信回線をオープンします。
3. "Other method"項目で実行するメソッド(関数)を選択し，メソッド(関数)の引数となるデータを入力後，[Execute]ボタンをクリックします。
   "Dump"にチェックが入っている場合は読み出したデバイス値を表示します。
   "RESULT"欄には各メソッド(関数)の実行結果を表示します。
