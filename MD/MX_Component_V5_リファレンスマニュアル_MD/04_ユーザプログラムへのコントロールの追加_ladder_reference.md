# MX Component Version 5 リファレンスマニュアル 4章 ユーザプログラムへのコントロールの追加 (4 / 原本 p.46-57)

| 項目 | 内容 |
|---|---|
| 原本 | 【三菱】MX Component Version 5 リファレンスマニュアル (SH-082394J) |
| メーカー | 三菱電機 |
| 原本ファイル | `PDF/【三菱】MX Component Version 5 リファレンスマニュアル_sh082394j.pdf` (全696ページ) |
| 本ファイルの範囲 | 4章 ユーザプログラムへのコントロールの追加 (印刷ページ 44-55 / PDF p.46-57) |
| 出典表記 | `(節 / 印刷ページ / 原本 p.PDFページ)` |
| 作成日 | 2026-11-02 |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。
> 本文中の「○ページ」はすべて原本の**印刷ページ番号**です(PDFページ = 印刷ページ + 2)。

## 主要用語 対訳表 (Glossary)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| オブジェクトを生成して使用する | Use by creating an object | — | 参考訳 |
| コントロールをフォームに貼り付けて使用する | Use by pasting the control on a form | — | 参考訳 |
| 参照設定 | References | VBA [ツール] | 参考訳 |
| 参照可能なライブラリファイル | Available References | VBA | 参考訳 |
| 参照の追加 | Add Reference | Visual Studio [プロジェクト] | 参考訳 |
| 参照マネージャー | Reference Manager | COM / アセンブリ>拡張 | 参考訳 |
| 既存項目の追加 | Add Existing Item | Visual Studio [プロジェクト] | 参考訳 |
| インクルードファイル | Include file | ActDefine.vb / ActDefine.cs / ActDefine.h / *_i.c / *_i.h | 参考訳 |
| インクルードディレクトリ | Include Directories | [構成プロパティ]⇒[VC++ディレクトリ] | 参考訳 |
| インスタンス | Instance | — | 参考訳 |
| クラス | Class | ActUtlTypeLib.ActUtlTypeClass 等 | 参考訳 |
| ツールボックス | Toolbox | Visual Studio | 参考訳 |
| ツールボックス アイテムの選択 | Choose Toolbox Items | [COMコンポーネント]タブ | 参考訳 |
| ActiveXコントロールの挿入 | Insert ActiveX Control | Visual C++ | 参考訳 |
| 変数の追加 / コントロール変数の追加 | Add Variable / Add Control Variable | Visual C++ | 参考訳 |
| 変数の種類 | Variable type | CActUtlType 等 | 参考訳 |
| ソリューションエクスプローラー | Solution Explorer | — | 参考訳 |
| ナビゲーションペイン | Navigation pane | — | 参考訳 |
| ヘッダファイル | Header file | .h | 参考訳 |
| Windowsフォーム | Windows Forms | WPF / UWP は非対応 | 参考訳 |
| MFC | Microsoft Foundation Class | — | 参考訳 |
| キャッシュファイル(一時ファイル) | Cache file (temporary file) | *.exd | 参考訳 |
| 改ページプレビュー | Page Break Preview | Excel | 参考訳 |
| メモリリーク | Memory leak | — | 参考訳 |
| カスタムコントロール | Custom control | Access | 参考訳 |
| Heightプロパティ / Widthプロパティ | Height property / Width property | "24" | 原本併記 |
| ユーザ指定フォルダ | User-specified folder | (ユーザ指定フォルダ)\Act\Include | 参考訳 |
| 開発タイプ | Development type | ユーティリティ設定タイプ / プログラム設定タイプ | 参考訳 |

## 変換範囲表

| 原本ページ(PDF) | 印刷ページ | 節 | 扱い |
|---|---|---|---|
| p.46 | 44 | 4章冒頭(追加方法一覧) | 全文 |
| p.46-49 | 44-47 | 4.1 VBAを使用する場合 | 全文(操作画面図は文章化) |
| p.50-52 | 48-50 | 4.2 Visual Basic .NET，Visual C#を使用する場合 | 全文(操作画面図は文章化) |
| p.53-57 | 51-55 | 4.3 Visual C++を使用する場合 | 全文(操作画面図は文章化) |
| p.1-17 | — | 前付け | **未変換** |
| p.18-45 | 16-43 | 1章〜3章 | 別ファイル(01_〜03_) |
| p.58-696 | 56- | 5章〜13章・付録ほか | **未変換** |

## 目次

- 4章冒頭 追加方法一覧
- 4.1 VBAを使用する場合
- 4.2 Visual Basic .NET，Visual C#を使用する場合
- 4.3 Visual C++を使用する場合

---

## 4 ユーザプログラムへのコントロールの追加 (4 / 44 / 原本 p.46)

ユーザプログラムの中でMX Componentの関数，プロパティを使用するにはユーザプログラムにコントロールを追加する必要があります。
コントロールの追加方法は開発言語，コントロールの種類により異なります。

| 開発言語 | コントロールの種類 | コントロールの使用方法 | 詳細 |
|---|---|---|---|
| VBA | Actコントロール(32ビット用，64ビット用) | オブジェクトを生成して使用する | ☞44ページ オブジェクトを生成して使用する場合 |
| VBA | Actコントロール(32ビット用) | コントロールをフォームに貼り付けて使用する | ☞45ページ コントロールをフォームに貼り付けて使用する場合 |
| Visual Basic .NET<br>Visual C# | Actコントロール(32ビット用，64ビット用) | オブジェクトを生成して使用する | ☞48ページ オブジェクトを生成して使用する場合 |
| Visual Basic .NET<br>Visual C# | Actコントロール(32ビット用)*1 | コントロールをフォームに貼り付けて使用する | ☞50ページ コントロールをフォームに貼り付けて使用する場合 |
| Visual Basic .NET<br>Visual C# | .Netコントロール(32ビット用，64ビット用) | オブジェクトを生成して使用する | ☞48ページ オブジェクトを生成して使用する場合 |
| Visual C++ | Actコントロール(32ビット用，64ビット用) | オブジェクトを生成して使用する | ☞51ページ オブジェクトを生成して使用する場合 |
| Visual C++ | Actコントロール(32ビット用)*1 | コントロールをフォームに貼り付けて使用する | ☞53ページ コントロールをフォームに貼り付けて使用する場合 |

> *1 Visual Studio 2019のみサポートしています。

---

## 4.1 VBAを使用する場合 (4.1 / 44-47 / 原本 p.46-49)

VBAを使用する場合の設定操作を下記に示します。

### オブジェクトを生成して使用する場合 (4.1 / 44-45 / 原本 p.46-47)

**操作手順**

1. Visual Basic Editorを起動します。
   - Microsoft® Excel for Microsoft 365を使用する場合: [開発]タブの[Visual Basic]を選択します。
   - Microsoft Access for Microsoft 365を使用する場合: [データベースツール]タブの[Visual Basic]を選択します。
2. Visual Basic Editorの[ツール]タブの"参照設定"を選択します。
3. "参照可能なライブラリファイル"画面から，使用する"開発タイプ"のコントロール(☞45ページ 使用可能なコントロール(オブジェクトを生成して使用する場合))を選択し，[OK]ボタンをクリックします。

【図】"参照設定 - VBAProject"画面 (4.1 / 44 / 原本 p.46)
- 参照可能なライブラリファイル一覧で MITSUBISHI ActProgDataLogging Controls Ver1.0，MITSUBISHI ActProgType Controls Ver1.0，MITSUBISHI ActSupport Controls Ver3.0，MITSUBISHI ActSupportMsg Controls Ver1.0 にチェックが入った例
- 下部に選択中ライブラリの場所「C:\Program Files (x86)\MELSOFT\ACT\Control\ActSupportMsg.dll」(画面上は¥表記)

#### 使用可能なコントロール(オブジェクトを生成して使用する場合) (4.1 / 45 / 原本 p.47)

使用可能なコントロールを開発タイプ別に示します。

| 開発タイプ | 使用可能なコントロール |
|---|---|
| ユーティリティ設定タイプ(32ビット用) | MITSUBISHI ActUtlType Controls Ver1.0<br>MITSUBISHI ActSupportMsg Controls Ver1.0 |
| ユーティリティ設定タイプ(64ビット用) | ActUtlType64 Control<br>ActSupportMsg64 Control |
| プログラム設定タイプ(32ビット用) | MITSUBISHI ActProgType Controls Ver1.0<br>MITSUBISHI ActSupportMsg Controls Ver1.0 |
| プログラム設定タイプ(64ビット用) | ActProgType64 Control<br>ActSupportMsg64 Control |

### コントロールをフォームに貼り付けて使用する場合 (4.1 / 45-46 / 原本 p.47-48)

**操作手順**

1. 画面にActiveXコントロールを追加します。
   - Microsoft Excel for Microsoft 365を使用する場合: [開発]タブの[挿入]から【アイコン: その他のコントロール(工具アイコン)】を選択します。
   - Microsoft Access for Microsoft 365を使用する場合: [デザイン]タブの[コントロール]⇒[ActiveXコントロール]を選択します。

【図】Excelの[開発]タブ⇒[挿入]のフォームコントロール/ActiveXコントロール一覧，およびAccessの[デザイン]タブ⇒コントロール一覧下部の「ActiveX コントロール(O)」メニュー (4.1 / 45 / 原本 p.47)

2. "コントロールの選択"画面で，使用する"開発タイプ"のコントロール(☞46ページ 使用可能なコントロール(フォームに貼り付けて使用する場合))を選択し，[OK]ボタンをクリックします。
3. 選択したActコントロールをシートに貼り付けます。
4. Visual Basic Editorを起動します。
   - Microsoft Excel for Microsoft 365を使用する場合: [開発]タブの[Visual Basic]を選択します。
   - Microsoft Access for Microsoft 365を使用する場合: [デザイン]タブの[コードの表示]を選択します。

【図】手順2〜3の操作画面 (4.1 / 46 / 原本 p.48)
- 手順2: "コントロールの選択"画面の一覧で MITSUBISHI ActUtlType Control を選択した例(一覧には ActQNUDECPUTCP / ActQNUDECPUUDP / ActQSS / ActSIM / ActSupport / ActSupportMsg / ActSupportMsg64 / ActUtlDataLogging / ActUtlType / ActWizard の各 Control が表示)
- 手順3: Excelシート上(B3付近)にActコントロールのアイコンが貼り付き，数式バーに `=埋め込み("ActUtlType.ActUtlType.1","")` と表示された例

#### 使用可能なコントロール(フォームに貼り付けて使用する場合) (4.1 / 46 / 原本 p.48)

使用可能なコントロールを開発タイプ別に示します。

| 開発タイプ | 使用可能なコントロール |
|---|---|
| ユーティリティ設定タイプ(32ビット用) | MITSUBISHI ActUtlType Control<br>MITSUBISHI ActSupportMsg Control |
| プログラム設定タイプ(32ビット用) | MITSUBISHI ActProgType Control<br>MITSUBISHI ActSupportMsg Control |

### Microsoft Excel使用時の注意事項 (4.1 / 47 / 原本 p.49)

#### Excelにコントロールの貼付けを行っても，貼り付かない場合 (4.1 / 47 / 原本 p.49)

この現象は，Excelのキャッシュファイル(一時ファイル)が残っている場合に発生します。
その場合は，下記の手順にて操作してください。

**操作手順**

1. Excelを終了します。
2. tempフォルダのExcel8.0フォルダにある"*.exd"を削除します。
   - tempフォルダは，OSによって場所が異なります。
   - 該当フォルダ，ファイルが表示されていない場合は，フォルダオプションの設定ですべてのファイルとフォルダを表示するように設定してください。
3. Excelを再起動します。

#### Actコントロールのサイズ変更について(Excel) (4.1 / 47 / 原本 p.49)

ExcelではActコントロールのサイズ変更ができますが，MX Componentの動作には影響ありません。
サイズを元に戻す場合は，ActコントロールのHeightプロパティとWidthプロパティを"24"に設定し直してください。

※原本の見出しは「Actコントロールのサイズ変更について」(Access側と同名のため，本mdでは(Excel)を付記)。

#### Excel VBA使用時の注意事項 (4.1 / 47 / 原本 p.49)

Excel VBAを使用したアプリケーションに，改ページプレビュー機能を設定しないでください。
メモリリークの発生，OS基本操作(ファイル操作，印刷など)の異常といった現象が発生するおそれがあります。

### Microsoft Access使用時の注意事項 (4.1 / 47 / 原本 p.49)

#### ActコントロールをAccessフォームに貼り付けて，Actコントロールのダブルクリックまたはプロパティ中のカスタムコントロールを選択すると下記のエラーメッセージが表示される (4.1 / 47 / 原本 p.49)

下記のエラーメッセージが表示されますが，Actコントロールの動作には影響はありません。
(その他のエラーメッセージが表示される場合もあります。)

【図】エラーメッセージ (4.1 / 47 / 原本 p.49)。タイトル「Sample」，表示内容:

```
MITSUBISHI ActEasyIF Control オブジェクトを操作できません。
OLE サーバーが登録されていません。
OLE サーバーを再セットアップしてください。
```

#### Actコントロールを貼り付けてプロパティの表示を行った場合に，プロパティ名が途切れて表示される (4.1 / 47 / 原本 p.49)

この現象は，表示だけの問題であり，プロパティの機能には問題ありません。

#### Actコントロールのサイズ変更について(Access) (4.1 / 47 / 原本 p.49)

AccessではActコントロールのサイズ変更ができますが，MX Componentの動作には影響ありません。
サイズを元に戻す場合は，ActコントロールのHeightプロパティとWidthプロパティを"24"に設定し直してください。

※原本の見出しは「Actコントロールのサイズ変更について」。

---

## 4.2 Visual Basic .NET，Visual C#を使用する場合 (4.2 / 48-50 / 原本 p.50-52)

Visual Basic .NET，Visual C#を使用する場合の設定操作を下記に示します。

### オブジェクトを生成して使用する場合 (4.2 / 48-49 / 原本 p.50-51)

**操作手順**

1. Visual Studioを起動します。
2. [プロジェクト]⇒[参照の追加]を選択します。
3. 使用する"開発タイプ"のコントロール(☞49ページ 使用可能なコントロール(オブジェクトを生成して使用する場合))を追加します。
   - Actコントロールを使用する場合: "参照マネージャー "画面の"COM"からコントロールを選択します。
   - .Netコントロールを使用する場合: "参照マネージャー "画面の"アセンブリ"内の"拡張"からコントロールを選択します。
4. プログラム設定タイプで開発を行う場合，[プロジェクト]⇒[既存項目の追加]を選択し，インクルードファイル(☞49ページ インクルードファイル(Visual Basic .NET，Visual C#の場合))を追加します。インクルードファイルはインストール時， 下記に格納されています。
   (ユーザ指定フォルダ)\Act\Include
5. 使用するコントロールごとにクラスのインスタンスを作成してください。(☞49ページ コントロールごとに生成するクラス)

【図】"参照マネージャー"画面 (4.2 / 48 / 原本 p.50)
- Actコントロールの例: [COM]⇒[タイプ ライブラリ]で MITSUBISHI ActProgType Controls Ver1.0，MITSUBISHI ActSupportMsg Controls Ver1.0，MITSUBISHI ActUtlType Controls Ver1.0 にチェック(いずれもバージョン1.0)
- .Netコントロールの例: [アセンブリ]⇒[拡張](ターゲット: .NET Framework 4.7.2)で ActSupportMsgLib，ActUtlTypeLib(バージョン1.0.0.0)にチェック

#### 使用可能なコントロール(オブジェクトを生成して使用する場合) (4.2 / 49 / 原本 p.51)

使用可能なコントロールを開発タイプ別に示します。

| 開発タイプ | コントロールの種類 | 使用可能なコントロール |
|---|---|---|
| ユーティリティ設定タイプ(32ビット用) | Actコントロール | MITSUBISHI ActUtlType Controls Ver1.0<br>MITSUBISHI ActUtlDataLogging Controls Ver1.0<br>MITSUBISHI ActSupportMsg Controls Ver1.0 |
| ユーティリティ設定タイプ(32ビット用) | .Netコントロール | MITSUBISHI DotUtlType Component |
| ユーティリティ設定タイプ(64ビット用) | Actコントロール | ActUtlType64 Control<br>ActUtlDataLogging64 Control<br>ActSupportMsg64 Control |
| ユーティリティ設定タイプ(64ビット用) | .Netコントロール | DotUtlType64 Control |
| プログラム設定タイプ(32ビット用) | Actコントロール | MITSUBISHI ActProgType Controls Ver1.0<br>MITSUBISHI ActProgDataLogging Controls Ver1.0<br>MITSUBISHI ActSupportMsg Controls Ver1.0 |
| プログラム設定タイプ(64ビット用) | Actコントロール | ActProgType64 Control<br>ActProgDataLogging64 Control<br>ActSupportMsg64 Control |

#### コントロールごとに生成するクラス (4.2 / 49 / 原本 p.51)

| コントロール | クラス |
|---|---|
| ActUtlType Control | ActUtlTypeLib.ActUtlTypeClass |
| ActUtlDataLogging Control | ActUtlDataLoggingLib.ActUtlDataLoggingClass |
| ActSupportMsg Control | ActSupportMsgLib.ActSupportMsgClass |
| MITSUBISHI DotUtlType Component | MITSUBISHI.Component.DotUtlType |
| ActUtlType64 Control | ActUtlType64Lib.ActUtlType64Class |
| ActUtlDataLogging64 Control | ActUtlDataLogging64Lib.ActUtlDataLogging64Class |
| ActSupportMsg64 Control | ActSupportMsg64Lib.ActSupportMsg64Class |
| DotUtlType64 Control | DotUtlType64.DotUtlType64 |
| ActProgType Control | ActProgTypeLib.ActProgTypeClass |
| ActProgDataLogging Control | ActProgDataLoggingLib.ActProgDataLoggingClass |
| ActSupportMsg Control | ActSupportMsgLib.ActSupportMsgClass |
| ActProgType64 | ActProgType64Lib.ActProgType64Class |
| ActProgDataLogging64 | ActProgDataLogging64Lib.ActProgDataLogging64Class |
| ActSupportMsg64 | ActSupportMsg64Lib.ActSupportMsg64Class |

※最後の3行のコントロール名に"Control"が付かないのは原本どおり。

#### インクルードファイル(Visual Basic .NET，Visual C#の場合) (4.2 / 49 / 原本 p.51)

| 開発言語 | インクルードファイル |
|---|---|
| Visual Basic .NET | ActDefine.vb |
| Visual C# | ActDefine.cs |

### コントロールをフォームに貼り付けて使用する場合 (4.2 / 50 / 原本 p.52)

本機能はWindows®フォームにのみ対応しています。WPF，UWPには対応していません。
また，Visual Studio 2022には対応していません。

**操作手順**

1. Visual Studioを起動します。
2. "ツールボックス"内で右クリックし，[アイテムの選択...]を選択します。
3. "ツールボックス アイテムの選択"画面の[COMコンポーネント]タブから，使用する"開発タイプ"のコントロール(☞50ページ 使用可能なコントロール(フォームに貼り付けて使用する場合))を選択し，[OK]ボタンをクリックします。
4. ツールボックスに追加されたコントロールをフォームに貼り付けます。
5. [プロジェクト]⇒[既存項目の追加]を選択し，インクルードファイル(☞49ページ インクルードファイル(Visual Basic .NET，Visual C#の場合))を追加します。インクルードファイルはインストール時，下記に格納されています。
   (ユーザ指定フォルダ)\Act\Include

【図】"ツールボックス アイテムの選択"画面 (4.2 / 50 / 原本 p.52)
- [COM コンポーネント]タブで MITSUBISHI ActSupportMsg Control，MITSUBISHI ActUtlDataLogging Control，MITSUBISHI ActUtlType Control にチェックが入った例
- パス列は C:\Program Files (x86)\MELSOFT\ACT\C…(画面上は¥表記，途中で切れて判読不可)

#### 使用可能なコントロール(フォームに貼り付けて使用する場合) (4.2 / 50 / 原本 p.52)

使用可能なコントロールを開発タイプ別に示します。

| 開発タイプ | 使用可能なコントロール |
|---|---|
| ユーティリティ設定タイプ(32ビット用) | MITSUBISHI ActUtlType Controls<br>MITSUBISHI ActUtlDataLogging Controls<br>MITSUBISHI ActSupportMsg Controls |
| プログラム設定タイプ(32ビット用) | MITSUBISHI ActProgType Controls<br>MITSUBISHI ActProgDataLogging Controls<br>MITSUBISHI ActSupportMsg Controls |

---

## 4.3 Visual C++を使用する場合 (4.3 / 51-55 / 原本 p.53-57)

Visual C++でコントロールを使用する場合，あらかじめMFCをインストールしておく必要があります。
Visual C++を使用する場合の設定操作を下記に示します。

### オブジェクトを生成して使用する場合 (4.3 / 51-52 / 原本 p.53-54)

**操作手順**

1. Visual Studioを起動します。
2. 下記を参照し，使用する"開発タイプ"で必要なインクルードファイルを設定します。(☞52ページ インクルードファイルの設定(Visual C++の場合))インクルードファイルはインストール時， 下記に格納されています。
   (ユーザ指定フォルダ)\Act\Include

| 開発タイプ | 必要なインクルードファイル |
|---|---|
| ユーティリティ設定タイプ(32ビット用) | ActUtlType_i.c<br>ActUtlType_i.h<br>ActUtlDataLogging_i.c<br>ActUtlDataLogging_i.h<br>ActSupportMsg_i.c<br>ActSupportMsg_i.h |
| ユーティリティ設定タイプ(64ビット用) | ActUtlType64_i.c<br>ActUtlType64_i.h<br>ActUtlDataLogging64_i.c<br>ActUtlDataLogging64_i.h<br>ActSupportMsg64_i.c<br>ActSupportMsg64_i.h |
| プログラム設定タイプ(32ビット用) | ActProgType_i.c<br>ActProgType_i.h<br>ActProgDataLogging_i.h<br>ActProgDataLogging_i.c<br>ActSupportMsg_i.c<br>ActSupportMsg_i.h<br>ActDefine.h |
| プログラム設定タイプ(64ビット用) | ActProgType64_i.c<br>ActProgType64_i.h<br>ActProgDataLogging64_i.h<br>ActProgDataLogging64_i.c<br>ActSupportMsg64_i.c<br>ActSupportMsg64_i.h<br>ActDefine.h |

3. 使用するコントロールごとにインスタンスを作成してください。インスタンスの作成方法はVisual C++用のサンプルプログラムを参照してください

※手順3の文末に句点が無いのは原本どおり。

#### インクルードファイルの設定(Visual C++の場合) (4.3 / 52 / 原本 p.54)

**操作手順**

1. Visual Studioを起動し，[プロジェクト]⇒[プロパティ ]を選択します。
2. 表示される画面左側のナビゲーションペインで，[構成プロパティ ]⇒[VC++ディレクトリ]を選択します。
3. 画面右側の"インクルードディレクトリ"を選択した状態で[▼]ボタンをクリックし，＜編集...＞を選択します。
4. [新しい行]ボタンを選択します。
5. 続いて，[...]ボタンを選択します。
6. "ディレクトリの選択"画面でインクルードファイルが格納されているフォルダ("Include")を選択します。
   インクルードファイルはインストール時，下記に格納されています。
   (ユーザ指定フォルダ)\Act\Include

【図】手順2〜5の操作画面 (4.3 / 52 / 原本 p.54)
- 手順2: プロパティページ左ペインで[構成プロパティ]⇒[VC++ディレクトリ]を選択。右ペイン「全般」に インクルード ディレクトリ = $(VC_IncludePath);$(WindowsSDK_IncludePath);
- 手順3: インクルード ディレクトリ行の[▼]から＜編集...＞
- 手順4: "インクルード ディレクトリ"画面の[新しい行 (Ctrl+Ins…)]ボタン(フォルダ+☆アイコン)
- 手順5: 追加された行の右端[...]ボタン

### コントロールをフォームに貼り付けて使用する場合 (4.3 / 53-54 / 原本 p.55-56)

Visual Studio 2022には対応していません。

**操作手順**

1. Visual Studioを起動します。
2. フォームを右クリックして，[ActiveXコントロールの挿入]を選択します。
3. 使用する"開発タイプ"のコントロール(☞55ページ 使用可能なコントロール(フォームに貼り付けて使用する場合))を選択し，[OK]ボタンをクリックします。
4. フォームを右クリックして，[変数の追加]を選択します。
5. "コントロール変数の追加"画面の"全般設定"で，"名前"と"変数の種類"(☞55ページ 変数の種類)を入力し，[次へ]ボタンをクリックします。
   "名前"にはプログラム内で使用するオブジェクト名を入力します。
6. "コントロール変数の追加"画面の"その他の設定"で，".hファイル"と".cppファイル"(☞55ページ .hファイルと.cppファイル)を入力し，[完了]ボタンをクリックします。
7. ソリューションエクスプローラーで，手順6にて設定した".hファイル"と".cppファイル"が作成されていることを確認します。
8. ActProgTypeまたはActProgDataLoggingを使用する場合，[プロジェクト]⇒[既存項目の追加]を選択し，インクルードファイル"ActDefine.h"を追加します。インクルードファイルはインストール時， 下記に格納されています。
   (ユーザ指定フォルダ)\Act\Include

【図】手順4〜7の操作画面 (4.3 / 53-54 / 原本 p.55-56)
- 手順4: フォーム(dialog1)右クリックメニューの「変数の追加(B)...」
- 手順5の画面例("全般設定"): コントロール ID = IDC_ACTUTLTYPE1，コントロールの種類 = OCX，カテゴリ = コントロール，アクセス = public，名前 = m_ActUtlType，変数の種類 = CActUtlType
- 手順6の画面例("その他の設定"): .h ファイル = actutltype.h，.cpp ファイル = actutltype.cpp
- 手順7: ソリューションエクスプローラーの「ソース ファイル」に actutltype.cpp が追加されている

> **Point**
> コントロールをフォームに貼り付けて使用する場合(☞53ページ コントロールをフォームに貼り付けて使用する場合)の手順6で作成される".hファイル"が，正しく作成されない場合があります。(☞676ページ Visual C++でフォームに貼り付けて使用する際に，ヘッダファイルが正しく作成されない場合)

#### 使用可能なコントロール(フォームに貼り付けて使用する場合) (4.3 / 55 / 原本 p.57)

使用可能なコントロールを開発タイプ別に示します。

| 開発タイプ | 使用可能なコントロール |
|---|---|
| ユーティリティ設定タイプ(32ビット用) | MITSUBISHI ActUtlType Controls<br>MITSUBISHI ActUtlDataLogging Controls<br>MITSUBISHI ActSupportMsg Controls |
| プログラム設定タイプ(32ビット用) | MITSUBISHI ActProgType Controls<br>MITSUBISHI ActProgDataLogging Controls<br>MITSUBISHI ActSupportMsg Controls |

#### 変数の種類 (4.3 / 55 / 原本 p.57)

"コントロール変数の追加"画面に入力する，コントロール別の"変数の種類"について下記に示します。

| コントロール | 変数の種類 |
|---|---|
| ActUtlType | CActUtlType |
| ActUtlDataLogging | CActUtlDataLogging |
| ActSupportMsg | CActSupportMsg |
| ActProgType | CActProgType |
| ActProgDataLogging | CActProgDataLogging |

#### .hファイルと.cppファイル (4.3 / 55 / 原本 p.57)

"コントロール変数の追加"画面に入力する，コントロール別の".hファイル"および".cppファイル"について下記に示します。

| コントロール | .hファイル | .cppファイル |
|---|---|---|
| ActUtlType | actutltype.h | actutltype.cpp |
| ActUtlDataLogging | actutldatalogging.h | actutldatalogging.cpp |
| ActSupportMsg | actsupportmsg.h | actsupportmsg.cpp |
| ActProgType | actprogtype.h | actprogtype.cpp |
| ActProgDataLogging | actprogdatalogging.h | actprogdatalogging.cpp |
