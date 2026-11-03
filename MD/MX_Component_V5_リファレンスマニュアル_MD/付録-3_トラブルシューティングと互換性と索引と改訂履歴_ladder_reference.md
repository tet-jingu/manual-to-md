# MX Component Version 5 リファレンスマニュアル 付録 (3/3) 付11・付12・関数索引・改訂履歴・保証 p.676-696

| 項目 | 内容 |
|---|---|
| 原本 | 【三菱】MX Component Version 5 リファレンスマニュアル (SH-082394J) |
| メーカー | 三菱電機 |
| 原本ファイル | `PDF/【三菱】MX Component Version 5 リファレンスマニュアル_sh082394j.pdf` (全696ページ) |
| 本ファイルの範囲 | 付11 トラブルシューティング，付12 従来品との相違点および互換性，関数索引，改訂履歴，保証について，サービスのお問い合わせ，商標，著作権，裏表紙 (印刷ページ 674-692 / PDF p.676-696) |
| 出典表記 | `(節 / 印刷ページ / 原本 p.PDFページ)`。印刷ページ番号のない裏表紙は PDFページのみ |
| 作成日 | 2026-11-03 |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。
> 本文中の「○ページ」はすべて原本の**印刷ページ番号**です(PDFページ = 印刷ページ + 2)。
> 原本で縦に結合されたセル(同じ内容を複数行で共有)は，先頭行に内容を書き，2行目以降を「(同上)」と表記しています。
> 「¥」は原本表記のまま(パス区切り。プログラム・エクスプローラ上は \ に相当)。

## 主要用語 対訳表 (Glossary)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| トラブルシューティング | Troubleshooting | 付11 | 参考訳 |
| 自己登録 / 自己登録エラー | Self-registration / Self-registration error | — | 参考訳 |
| ローカルセキュリティポリシー | Local Security Policy | Windows | 参考訳 |
| ユーザーアカウント制御 | User Account Control | UAC | 原本併記 |
| 昇格 / 資格情報 | Elevation / Credentials | — | 参考訳 |
| 時計設定用デバイス | Clock setting device | SM1028 | 参考訳 |
| 対象先生存確認(開始間隔) | Existence check of target (start interval) | デフォルト10分 | 参考訳 |
| MACアドレス / Ethernetアドレス | MAC address / Ethernet address | — | 原本併記 |
| オープン方式 / MELSOFT接続 | Open method / MELSOFT connection | Ethernetパラメータ | 参考訳 |
| リモートパスワード / パスワードロック解除 | Remote password / Password lock release | QJ71E71 | 参考訳 |
| TCP/IP用局番 / UDP/IP用局番 | Station number for TCP/IP / UDP/IP | — | 参考訳 |
| ソケット生成エラー | Socket creation error | 0x01808007 | 参考訳 |
| オクテット / 8進数 | Octet / Octal | IPアドレス | 参考訳 |
| アプリケーション構成ファイル | Application configuration file | app.config | 原本併記 |
| 相互運用型の埋め込み | Embed Interop Types | "False" | 参考訳 |
| 参照アセンブリの出力 | Reference Assembly Output | "False" | 参考訳 |
| ビルド後のイベント | Post-build event | copy app.config | 参考訳 |
| GX Simulator3未起動エラー | GX Simulator3 not started error | 0xF1000020 | 参考訳 |
| ポート番号=5500+システムNo.×10+号機No. | Port number = 5500 + system No.×10 + PLC No. | 例 5511 | 参考訳 |
| 従来品との相違点および互換性 | Differences and compatibility with conventional products | 付12 | 参考訳 |
| 開発環境 / 通信経路 / 接続可能機種 | Development environment / Communication route / Connectable models | — | 参考訳 |
| 置き換え / 流用 | Replacement / Reuse | — | 参考訳 |
| 設定ファイル(.ACTファイル) | Setting file (.ACT file) | Version 4 | 参考訳 |
| エクスポート / インポート | Export / Import | 通信設定・システムラベル | 参考訳 |
| 関数索引 | Function index | — | 参考訳 |
| 改訂履歴 / 取扱説明書番号 | Revision history / Manual number | SH(名)-082394-A〜J | 参考訳 |
| 無償保証期間 / 無償保証範囲 | Gratis warranty period / Gratis warranty range | 36ヵ月(上限42ヵ月) | 参考訳 |
| 生産中止後の有償修理期間 | Onerous repair period after discontinuation | 7年間 | 参考訳 |
| 機会損失 / 二次損失 | Opportunity loss / Secondary loss | — | 参考訳 |
| 電話技術相談窓口 | Technical support by phone | 052-712-2444 | 参考訳 |

## 変換範囲表

| 原本ページ(PDF) | 印刷ページ | 節 | 扱い |
|---|---|---|---|
| p.676-681 | 674-679 | 付11 トラブルシューティング | 全文(図は文章化) |
| p.682-689 | 680-687 | 付12 従来品との相違点および互換性 | 全文 |
| p.690 | 688 | 関数索引 | 全文 |
| p.691 | 689 | (MEMO) | 除外: MEMO欄のみで内容なし |
| p.692 | 690 | 改訂履歴 | 全文 |
| p.693 | 691 | 保証について | 全文 |
| p.694 | 692 | サービスのお問い合わせ，商標，著作権 | 全文 |
| p.695 | — | (白紙) | 除外: 白紙ページ |
| p.696 | — | 裏表紙(お問い合わせ先，電話技術相談窓口，発行情報) | 全文(QRコード・ロゴ画像は除く) |
| p.648-664 | 646-662 | 付1〜付5 | 別ファイル(付録-1) |
| p.665-675 | 663-673 | 付6〜付10 | 別ファイル(付録-2) |
| p.1-647 | — | 前付け，1〜13章 | 前付け**未変換**，1〜13章は別ファイル(01_〜13-3_) |

## 目次

- 付11 トラブルシューティング
  - インストーラ実行時に自己登録されない場合 / CPUユニット関連 / Ethernetユニット使用時 / 通信時 / 通信設定ユーティリティの設定保存時
  - Visual C++でフォームに貼り付けて使用する際に，ヘッダファイルが正しく作成されない場合
  - Visual Studio .NET を使用して，コントロールを使用するための設定でエラーが発生した場合
  - Visual C++を使用して，ユーザプログラムを作成するときにリンクエラーが発生した場合
  - GX Simulator3との通信時に未起動エラーが発生した場合
- 付12 従来品との相違点および互換性
  - MX Component Version 4との比較(開発環境 / 通信経路 / 接続可能機種)
  - コントロールの比較(Actコントロール / .Netコントロール)
  - 置き換えについて
- 関数索引
- 改訂履歴
- 保証について
- サービスのお問い合わせ / 商標 / 著作権
- 裏表紙

---
## 付11 トラブルシューティング (付11 / 674-679 / 原本 p.676-681)

MX Componentを使用する上で発生するエラーの内容，およびトラブルシューティングについて説明します。

### インストーラ実行時に自己登録されない場合 (付11 / 674 / 原本 p.676)

ローカルセキュリティポリシーの「ユーザーアカウント制御」の一部ポリシーについては，正しくインストールができなくなる設定があります。
下記のポリシーの設定を確認してください。

#### アプリケーションのインストールを検出し，昇格をプロンプトする (付11 / 674 / 原本 p.676)

[有効]を設定してください。
[無効]にすると，インストールの途中で自己登録エラーが発生する場合があります。

#### 署名され検証された実行ファイルのみを昇格する (付11 / 674 / 原本 p.676)

[無効]を設定してください。
[有効]にすると，署名のない実行ファイルが実行できなくなるため，インストーラが正しく起動できなくなります。

#### 標準ユーザーに対する昇格時のプロンプトの動作 (付11 / 674 / 原本 p.676)

[セキュリティで保護されたデスクトップで資格情報を要求する]，または[資格情報を要求する]を設定してください。
[昇格の要求を自動的に拒否する]を設定すると昇格ができなくなり，インストーラが正しく起動できなくなります。

### CPUユニット関連 (付11 / 674 / 原本 p.676)

#### USB通信時 (付11 / 674 / 原本 p.676)

CPUユニットと交信中にUSBケーブルの脱着，CPUユニットのリセットおよび電源のOFF/ONを頻繁に行うと，交信エラーが発生し復旧しない場合があります。
その場合は，USBケーブルを一度完全に抜いて5秒以上経過後に再度装着してください。
なお，本操作後も初回交信時にエラーとなる場合がありますが，2回目以降は正常に機能します。

#### CPUユニットの時計データについて (付11 / 674 / 原本 p.676)

- QCPU(Qモード)，LCPU，およびFXCPUでは，CPUユニットがRUN状態でも時計データの設定が可能です。
- QCPU(Qモード)およびLCPUは，時計設定用デバイス"SM1028"のON/OFF状態に関係なく設定を行えます。
- FXCPUは，時計機能内蔵の機種で時計データが設定できます。
- 時計設定は，転送時間分の誤差が生じますのでご注意ください。

### Ethernetユニット使用時 (付11 / 674-675 / 原本 p.676-677)

#### TCP/IPコネクション確立中のCPUユニットリセット (付11 / 674 / 原本 p.676)

MX Componentを使用してTCP/IPコネクション確立中(Open中)にCPUユニットをリセットすると，それ以降の通信時に通信エラーや受信エラーが発生します。
その場合は，MX Componentを使用するアプリケーション内でクローズ処理をしたあと，再度オープン処理を行ってください。

#### Ethernetユニットの対象先生存確認開始間隔について (付11 / 674 / 原本 p.676)

パソコンからクローズ処理(Close)を実行しても，Ethernetユニットがクローズ処理(Close)を実行しない場合があります。このような原因の1つに，ケーブルの断線があげられます。
Ethernetユニットがクローズ処理(Close)を実行しない状態でパソコンからオープン処理(Open)を実行しても，Ethernetユニットが対象先生存確認を行い，Ethernetユニットのクローズ処理(Close)を実行するまでは，パソコンからのオープン処理(Open)は正常終了しません。
パソコンからオープン処理(Open)を早期に終了させたい場合は，Ethernetユニットの対象先生存確認間隔を短く設定してください。
(Ethernetユニットの対象先生存確認開始間隔は，デフォルトでは10分となっています。)

#### Ethernetユニットの交換 (付11 / 675 / 原本 p.677)

Ethernet通信を行っている際，デバッグや故障などによりEthernetユニットを交換した場合は，他ノード(パソコン)側の再起動が必要となります。
(Ethernetアドレス(MACアドレス)が機器ごとに異なっているためです。)

#### Qシリーズ対応Ethernetユニット使用時の同時アクセスについて (付11 / 675 / 原本 p.677)

複数のパソコンから同一ユニットにTCP/IPプロトコルを用いて同時に通信を行う場合は，下記の条件を満たしてください。

- シリアルNo.の上5桁が"02122"以降で機能バージョンB以降のQシリーズ対応E71ユニット(QJ71E71-100を除く)を使用する。
- GX Works2を使用して，Ethernetパラメータの[オープン方式]を"MELSOFT接続"に設定する。

#### QJ71E71使用時のパスワードロック解除について (付11 / 675 / 原本 p.677)

遠隔操作によりパスワードロックを解除できる範囲は，接続対象局までです。
下位階層側にもパスワードが設定されていると，下位の階層のCPUユニットと交信することはできません。

【図】パスワードロック解除の範囲 (付11 / 675 / 原本 p.677)
- 起動元(パソコン)の画面「パスワードを入力して解除してください。」に「AAAA」を入力
- 上位Ethernetに局❶(QCPU(Qモード)+QJ71E71)と局❷(QJ71E71)。局❷(❶と同じベースの2枚目)から下位Ethernetに局❸❹❺(各QCPU(Qモード)+QJ71E71)
- 破線で囲まれた範囲に注記「❶QJ71E71のパスワードロック解除で，この範囲のCPUユニットへアクセス可能」
- 図中の判定: 局❶のCPU = ○(アクセス可能)，局❸ = ×，局❹ = ×，局❺ = ○
- ○: アクセス可能，×: アクセス不可能

| 番号 | リモートパスワード |
|---|---|
| ❶ | 設定あり(AAAA) |
| ❷ | 設定なし |
| ❸ | 設定あり(AAAA) |
| ❹ | 設定あり(BBBB) |
| ❺ | 設定なし |

#### Ethernet通信について (付11 / 675 / 原本 p.677)

- Ethernet通信(プロトコルがTCP/IPの場合)にCPUダウンまたはEthernetユニットのリセットが発生すると，通信回線が切断されます。
  その場合は回線クローズ処理(Close)を実行後，再オープン処理(Open)を行ってください。
- 1台のパソコンから2種類の通信方式(プロトコル)を使用して1台のQシリーズ対応E71にアクセスを行う場合，TCP/IP用局番とUDP/IP用局番の2通りを設定する必要があります。
  ただし，MX Component Version 3以降とシリアル番号"05051"以降のQシリーズ対応E71を使用する場合は，TCP/IP用局番およびUDP/IP用局番を別々に設定する必要はありません。

**例**
MX ComponentがTCP/IP，GX Works2がUDP/IPを使用する場合

【図】TCP/IPとUDP/IPの局番設定例 (付11 / 675 / 原本 p.677)
- パソコン: MX Component用(TCP/IP)局番 : 2，GX Works2用(UDP/IP)局番 : 3
- Qシリーズ対応E71(局番: 1)へ，GX Works2(UDP/IP)とMX Component(TCP/IP)の2本で接続
- 図中注記: MX Component用(TCP/IP)局番とGX Works2用(UDP/IP)局番は，異なる局番に設定してください。同一局番に設定すると，Ethernetユニット側でエラーが発生します。

### 通信時 (付11 / 676 / 原本 p.678)

#### 通信時にソケット生成エラー (0x01808007)が発生する場合 (付11 / 676 / 原本 p.678)

| No. | 条件 | 対処方法 |
|---|---|---|
| 1 | GT SoftGOTを使用している場合 | アプリケーション起動時に，右クリックで[管理者として実行]を選択してください。 |
| 2 | 上記No.1で解決しない場合 | • 他のアプリケーションによって使用されているポート番号と異なる番号を，パソコン側で使用するポート番号に設定してください。<br>• 指定したIPアドレスの各オクテットの先頭が，0から始まっていないか確認してください。各オクテットの先頭を0に設定すると，対象のオクテットの値は8進数として処理されます。 |
| 3 | 上記No.1，2で解決しない場合 | 下記項目を確認し，弊社，電話技術相談窓口へお問い合わせください。<br>• システム構成(接続先のシーケンサ形名，ユニットの形名，使用ネットワーク)<br>• パソコンの名称(メーカ名)，CPU，メモリサイズ<br>• OS，エディション，32ビット/64ビット<br>• MX Componentのバージョン<br>• 現象が発生するMX Componentの関数と引数<br>• 通信設定ユーティリティの設定内容<br>• 現象の発生頻度と発生手順 |

#### コントロールやシーケンサモニタユーティリティの応答がなくなった場合 (付11 / 676 / 原本 p.678)

一時的な断線などが原因でMX Componentにて設定したタイムアウト時間の間，コントロールやシーケンサモニタユーティリティが応答待ちになる場合があります。
タイムアウトエラーが発生するように，適切なタイムアウト時間を設定してください。

### 通信設定ユーティリティの設定保存時 (付11 / 676 / 原本 p.678)

#### 通信設定ユーティリティで設定を保存するときに発生するエラーとその対処方法について (付11 / 676 / 原本 p.678)

| エラーメッセージ | 対処方法 | 注意事項 |
|---|---|---|
| システム情報の更新に失敗しました。<br>• 操作権限がない可能性があります。管理者権限のあるユーザで実行してください。<br>• アプリケーションが動作する環境が壊れている可能性があります。再度インストールを行ってください。 | Windowsのスタートで"MELSOFT"から"通信設定ユーティリティ "を選択し，右クリックで[管理者として実行]を選択し，アプリケーションを起動してください。 | ラベル管理ユーティリティ実行時は，管理者権限で動作します。<br>ユーザーアカウント制御(UAC)の設定により動作が異なります。 |

### Visual C++でフォームに貼り付けて使用する際に，ヘッダファイルが正しく作成されない場合 (付11 / 676 / 原本 p.678)

Visual Studio2019のバージョンにより，Visual C++でフォームに貼り付けて使用する際に，ヘッダファイルが正しく作成されない場合があります。
正しく作成されない場合は，"[ユーザ指定フォルダ]\Act\Include"に格納されている下記のヘッダファイルで，作成されたファイルを上書きしてください。

| 使用するコントロール | ヘッダファイル |
|---|---|
| ActUtlType | actutltype.h |
| ActUtlDataLogging | actutldatalogging.h |
| ActSupportMsg | actsupportmsg.h |
| ActProgType | actprogtype.h |
| ActProgDataLogging | actprogdatalogging.h |

### Visual Studio .NET を使用して，コントロールを使用するための設定でエラーが発生した場合 (付11 / 677 / 原本 p.679)

コントロールを使用するための設定で，エラーが発生することがあります。
対処方法は，下記のPointを参照してください。

> **Point**
> .NET Framework 4/.NET Framework 4.5/.NET Framework 4.6を使用したアプリケーションを作成する場合(下記は.NET Framework 4の例です。)アプリケーションの.exeファイルを含むフォルダに，下記の内容を記述したアプリケーション構成ファイル(app.config)を追加してください。
> 詳細についてはVisual Studioのヘルプを参照してください。

```xml
<configuration>
<startup useLegacyV2RuntimeActivationPolicy="true">
<supportedRuntime version="v4.0"/>
</startup>
</configuration>
```

#### コントロールをフォームに貼り付けて使用する場合 (付11 / 677 / 原本 p.679)

> **Point**
> - Visual C++ .NET/Visual Basic .NET/Visual C#のプロジェクトを使用する場合
>   "参照設定"に下記のライブラリが追加されます。
>   ActProgTypeの場合: ActProgTypeLib
>   ActUtlTypeの場合: ActUtlTypeLib
>   ActSupportMsgの場合: ActSupportMsgLib
>   DotUtlTypeの場合: MITSUBISHI.Component.DotUtlType
>   DotSupportMsgの場合: MITSUBISHI.Component.DotSupportMsg
>   各ライブラリのプロパティで"相互運用型の埋め込み"を"False"にしてください。

### Visual C++を使用して，ユーザプログラムを作成するときにリンクエラーが発生した場合 (付11 / 678 / 原本 p.680)

1つのプログラムに.Netコントロール(DotUtlType)とActコントロール(ActUtlType)を同時に貼り付けて使用すると，リンクエラーが発生します。
対処方法は下記のとおりです。

#### アプリケーション構成ファイルの追加手順 (付11 / 678 / 原本 p.680)

1. [プロジェクト]⇒[新しい項目の追加]を選択します。
2. [インストール済み]⇒[Visual C++]⇒[ユーティリティ ]を選択します。
3. "構成ファイル(app.config)"を選択し，[追加]をクリックします。
4. アプリケーション構成ファイル(app.config)に下記の内容を記述します。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <startup useLegacyV2RuntimeActivationPolicy="true">
        <supportedRuntime version="v4.0"/>
    </startup>
</configuration>
```

5. [プロジェクト]⇒[プロパティ ]を選択します。
6. [構成プロパティ ]⇒[ビルド イベント]⇒[ビルド後のイベント]を選択します。
7. "コマンド ライン"に"copy app.config"$(TargetPath).config""を設定します。

#### コントロールの貼り付け手順 (付11 / 678 / 原本 p.680)

対処方法は，下記のPointを参照してください。

> **Point**
> 1つのプログラムに.Netコントロール(DotUtlType)とActコントロール(ActUtlType)を同時に貼り付けて使用する場合，ソリューションエクスプローラーの[プロジェクト]⇒[プロパティ ]メニューから下記の操作を実施してください。
> ❶[共通プロパティ ]⇒[Frameworkと参照]を選択する。
> ❷"参照"の"名前"から"ActUtlTypeLib"を選択し，"ビルドプロパティ "の"参照アセンブリの出力"の設定を"False"に変更する。
> ❸"参照"の"名前"から"Interop.ActUtlTypeLib.1.0"を選択し，"ビルドプロパティ "の"参照アセンブリの出力"の設定を"False"に変更する。
> ❹[OK]をクリックし，設定の変更を反映する。

### GX Simulator3との通信時に未起動エラーが発生した場合 (付11 / 679 / 原本 p.681)

MX Component Version 4.15R以前の設定をインポートしてGX Simulator3通信を行った場合，GX Simulator3未起動エラー(0xF1000020)が発生します。
対処方法は下記のとおりです。

#### ユーティリティ設定タイプのコントロールを使用している場合 (付11 / 679 / 原本 p.681)

シミュレータのポート番号を基準値5500で計算し，その値を通信設定ユーティリティで再設定してください。

- ポート番号=5500+システムNo.×10+号機No. (システムNo.=1，号機No.=1 の場合，5511=5500+1×10+1)

#### プログラム設定タイプのコントロールを使用している場合 (付11 / 679 / 原本 p.681)

シミュレータのポート番号を基準値5500で計算し，その値をコントロールのプロパティに渡すように変更してください。

- ポート番号=5500+システムNo.×10+号機No. (システムNo.=1，号機No.=1 の場合，5511=5500+1×10+1)

※「×」はテキスト抽出で欠落していたため画像から補った。

---

## 付12 従来品との相違点および互換性 (付12 / 680-687 / 原本 p.682-689)

MX ComponentのVersion 4とVersion 5の相違点，および互換性について示します。
Version 5.000A以降のバージョンで追加，変更になった機能については下記を参照してください。
☞646ページ 以前のバージョンからの変更点

> **Point**
> MX Component Version 5で対応しなくなった開発環境や通信経路などを使用したい場合は，MX Component Version 4を使用してください。
> ただし，MX Component Version 4は，MX Component Version 5と同じパソコンにインストールできません。
> MX Component Version 5をアンインストールしてから，インストールしてください。
> また，MX Component Version 4を使用する場合は，FAサイトにて当社製品の脆弱性についての最新の情報を確認し，必要な対策を実施してください。
> MX Component Version 4は，MX Component Version 5のDVDに格納されています。

### MX Component Version 4との比較 (付12 / 681-683 / 原本 p.683-685)

#### 開発環境 (付12 / 681 / 原本 p.683)

MX ComponentのVersion 4とVersion 5の開発環境の差異を示します。

| 項目 | 項目(詳細) | MX Component Version 4 | MX Component Version 5 |
|---|---|---|---|
| OS*1 | Windows | Microsoft Windows 10<br>Microsoft Windows 8.1<br>Microsoft Windows 8<br>Microsoft Windows 7<br>Microsoft Windows Vista<br>Microsoft Windows XP | Microsoft Windows 11 IoT Enterprise 2024<br>Microsoft Windows 11<br>Microsoft Windows Server 2025<br>Microsoft Windows Server 2022<br>Microsoft Windows Server 2019 |
| プログラミング言語*1 | Visual Basic .NET | Microsoft Visual Studio 2017 Visual Basic<br>Microsoft Visual Studio 2015 Visual Basic<br>Microsoft Visual Studio 2013 Visual Basic<br>Microsoft Visual Studio 2012 Visual Basic<br>Microsoft Visual Studio 2010 Visual Basic<br>Microsoft Visual Studio 2008 Visual Basic<br>Microsoft Visual Studio 2005 Visual Basic | Microsoft Visual Studio 2026 Visual Basic<br>Microsoft Visual Studio 2022 Visual Basic<br>Microsoft Visual Studio 2019 Visual Basic |
| プログラミング言語*1 | Visual C++ | Microsoft Visual Studio 2017 Visual C++<br>Microsoft Visual Studio 2015 Visual C++<br>Microsoft Visual Studio 2013 Visual C++<br>Microsoft Visual Studio 2012 Visual C++<br>Microsoft Visual Studio 2010 Visual C++<br>Microsoft Visual Studio 2008 Visual C++<br>Microsoft Visual Studio 2005 Visual C++ | Microsoft Visual Studio 2026 Visual C++<br>Microsoft Visual Studio 2022 Visual C++<br>Microsoft Visual Studio 2019 Visual C++ |
| プログラミング言語*1 | Visual C# | Microsoft Visual Studio 2017 Visual C#<br>Microsoft Visual Studio 2015 Visual C#<br>Microsoft Visual Studio 2013 Visual C#<br>Microsoft Visual Studio 2012 Visual C#<br>Microsoft Visual Studio 2010Visual C#<br>Microsoft Visual Studio 2008 Visual C#<br>Microsoft Visual Studio 2005 Visual C# | Microsoft Visual Studio 2026 Visual C#<br>Microsoft Visual Studio 2022 Visual C#<br>Microsoft Visual Studio 2019 Visual C# |
| プログラミング言語*1 | VBA(Excel) | Microsoft Excel 2019(32ビット版)<br>Microsoft Excel 2016(32ビット版)<br>Microsoft Excel 2013(32ビット版)<br>Microsoft Excel 2010(32ビット版)<br>Microsoft Excel 2007<br>Microsoft Excel 2003 | Microsoft Excel for Microsoft 365(64ビット版)<br>Microsoft Excel 2024(32ビット版/64ビット版)<br>Microsoft Excel 2021(32ビット版/64ビット版) |
| プログラミング言語*1 | VBA(Access) | Microsoft Access 2019(32ビット版)<br>Microsoft Access 2016(32ビット版)<br>Microsoft Access 2013(32ビット版)<br>Microsoft Access 2010(32ビット版)<br>Microsoft Access 2007<br>Microsoft Access 2003 | Microsoft Access for Microsoft 365(64ビット版)<br>Microsoft Access 2024(32ビット版/64ビット版)<br>Microsoft Access 2021(32ビット版/64ビット版) |
| プログラミング言語*1 | VBScript | テキストエディタおよび市販のHTMLツール | 非対応 |

※原本では「VBA」の詳細セルをExcel行とAccess行で共有(本mdでは(Excel)(Access)を付記)。「Microsoft Visual Studio 2010Visual C#」の空白欠落は原本表記のまま。

> *1 OSおよびプログラミング言語の詳細は下記を参照してください。
> ·MX Component Version 4: 📖MX Component Version 4 オペレーティングマニュアル
> ·MX Component Version 5: 📖MX Component Version 5 インストール手順書

#### 通信経路 (付12 / 682 / 原本 p.684)

MX ComponentのVersion 4とVersion 5の通信経路の差異を示します。

> **Point**
> 使用するOSにより通信の可否が異なります。また，使用可能なボードおよびドライバにもバージョンの制約がある場合があります。
> 詳細は，下記を参照してください。
> - ☞29ページ サポートする通信経路
> - ☞34ページ ユニット

○: 通信可，×: 通信不可

| 通信経路 | MX Component Version 4*1 | MX Component Version 5 |
|---|---|---|
| シリアルコミュニケーション通信 | ○ | ○ |
| Ethernet通信 | ○ | ○ |
| CPU COM通信 | ○ | ○ |
| CPU USB通信 | ○ | ○ |
| MELSECNET/H通信 | ○ | ○*2*3 |
| CC-Link IEコントローラネットワーク通信 | ○ | ○*2*3 |
| CC-Link IEフィールドネットワーク通信 | ○ | ○*2*3 |
| CC-Link IE TSN通信 | × | ○*2*3 |
| CC-Link通信 | ○ | ○*2*3 |
| CC-Linkシステム RS-232インタフェース通信 | ○ | ○ |
| Qシリーズバス通信(パソコンCPUユニット使用時のみ) | ○ | × |
| GX Simulator通信 | ○ | × |
| GX Simulator2通信 | ○ | ○ |
| GX Simulator3通信 | ○ | ○ |
| MT Simulator2通信 | ○ | ○ |
| MELSOFT Mirror通信 | × | ○ |
| モデム通信 | ○ | × |
| GOTゲートウェイデバイス通信 | ○ | ○ |
| GOTトランスペアレント通信 | ○ | ○ |
| インバータCOM通信 | ○ | ○ |
| インバータUSB通信 | ○ | ○ |
| ロボットコントローラCOM通信 | ○ | ○*3 |
| ロボットコントローラUSB通信 | ○ | ○*3 |
| ロボットコントローラEthernet通信 | ○ | ○*3 |

> *1 使用するOSにより通信の可否が異なります。(📖MX Component Version 4 オペレーティングマニュアル)
> *2 Windows 10 Education使用時は未サポートです。
> *3 Windows 10 IoT Enterprise 2016 LTSB使用時は64ビット版未サポートです。

#### 接続可能機種 (付12 / 683 / 原本 p.685)

MX ComponentのVersion 4とVersion 5の接続可能機種の差異を示します。
○: 対応，×: 非対応

| 分類 | シリーズ | MX Component Version 4 | MX Component Version 5 |
|---|---|---|---|
| CPU | MX-Rモデル | × | ○ |
| CPU | MX-Fモデル | × | ○ |
| CPU | RCPU | ○ | ○ |
| CPU | RCCPU | ○ | ○ |
| CPU | RモーションCPU | ○ | ○ |
| CPU | LHCPU | ○ | ○ |
| CPU | FX5CPU | ○ | ○ |
| CPU | QCPU(Qモード) | ○ | ○*1 |
| CPU | LCPU | ○ | ○ |
| CPU | QCCPU | ○ | ○ |
| CPU | QSCPU | ○ | ○ |
| CPU | QモーションCPU | ○ | ○*2 |
| CPU | FXCPU(FX3CPU)*3 | ○ | ○ |
| CPU | FXCPU(FX0CPU～FX2CPU)*4 | ○ | × |
| GOT | GOT1000 | ○ | × |
| GOT | GOT2000 | ○ | ○ |
| GOT | GOT3000 | × | ○ |
| インバータ | A800 | ○ | ○ |
| ロボットコントローラ | CR750 | ○ | ○ |
| ロボットコントローラ | CRnD-700 | ○ | ○ |
| シミュレータ | GX Simulator | ○ | × |
| シミュレータ | GX Simulator2 | ○ | ○ |
| シミュレータ | GX Simulator3 | ○ | ○ |
| シミュレータ | MT Simulator2 | ○ | ○ |

> *1 ベーシックモデルQCPU，ハイパフォーマンスモデルQCPU，プロセスCPUはサポートしていません。
> *2 Q172CPU，Q173CPU，Q172HCPU，Q173HCPUはサポートしていません。
> *3 FX3SCPU，FX3GCPU，FX3GCCPU，FX3UCPU，FX3UCCPU
> *4 FX0CPU，FX0SCPU，FX0NCPU，FX1CPU，FX1NCPU，FX1NCCPU，FX1SCPU，FX2CPU，FX2CCPU，FX2NCPU，FX2NCCPU

### コントロールの比較 (付12 / 684-686 / 原本 p.686-688)

MX ComponentのVersion 3，Version 4，およびVersion 5のコントロールの相違点を示します。

#### Actコントロール: プログラム設定タイプ (付12 / 684-686 / 原本 p.686-688)

※原本は p.686(ActCCBD〜ActSIM 34行)，p.687(ActMLCCBD〜ActMLAFBD 52行)，p.688(ActMLAJ71C24〜ActAJ71QC24TEL 10行＋ActProgDataLogging行)の3ページにまたがる1つの表(計97行)。
※縦結合セル: Ver.4 32ビットの「ActProgType」はActCCBD〜ActSIMの34行，「ActMLProgType」はActMLCCBD〜ActMLSIMの34行で共有。Ver.5 32ビット/64ビットの「ActProgType」「ActProgType64」はActCCBD〜ActSIMの34行で共有。2行目以降は「(同上)」と表記。
—: 該当なし

| Ver.3 32ビット | Ver.3 64ビット | Ver.4 32ビット | Ver.4 64ビット | Ver.5 32ビット | Ver.5 64ビット*1 |
|---|---|---|---|---|---|
| ActCCBD | — | ActProgType | — | ActProgType | ActProgType64 |
| ActCCG4A | — | (同上) | — | (同上) | (同上) |
| ActCCG4Q | — | (同上) | — | (同上) | (同上) |
| ActCCG4QnA | — | (同上) | — | (同上) | (同上) |
| ActCCIEFADPTCP | — | (同上) | — | (同上) | (同上) |
| ActCCIEFADPUDP | — | (同上) | — | (同上) | (同上) |
| ActCCIEFBD | — | (同上) | — | (同上) | (同上) |
| ActFX485BD | — | (同上) | — | (同上) | (同上) |
| ActFXCPU | — | (同上) | — | (同上) | (同上) |
| ActFXCPUUSB | — | (同上) | — | (同上) | (同上) |
| ActFXENETTCP | — | (同上) | — | (同上) | (同上) |
| ActGOT | — | (同上) | — | (同上) | (同上) |
| ActGOTTRSP | — | (同上) | — | (同上) | (同上) |
| ActLCPU | — | (同上) | — | (同上) | (同上) |
| ActLCPUTCP | — | (同上) | — | (同上) | (同上) |
| ActLCPUUDP | — | (同上) | — | (同上) | (同上) |
| ActLCPUUSB | — | (同上) | — | (同上) | (同上) |
| ActLJ71C24 | — | (同上) | — | (同上) | (同上) |
| ActLLT | — | (同上) | — | (同上) | (同上) |
| ActMnet10BD | — | (同上) | — | (同上) | (同上) |
| ActMnet2BD | — | (同上) | — | (同上) | (同上) |
| ActMnetGBD | — | (同上) | — | (同上) | (同上) |
| ActMnetHBD | — | (同上) | — | (同上) | (同上) |
| ActQCPUA | — | (同上) | — | (同上) | (同上) |
| ActQCPUQ | — | (同上) | — | (同上) | (同上) |
| ActQCPUQBus | — | (同上) | — | (同上) | (同上) |
| ActQCPUQUSB | — | (同上) | — | (同上) | (同上) |
| ActQJ71C24 | — | (同上) | — | (同上) | (同上) |
| ActQJ71E71TCP | — | (同上) | — | (同上) | (同上) |
| ActQJ71E71UDP | — | (同上) | — | (同上) | (同上) |
| ActQnACPU | — | (同上) | — | (同上) | (同上) |
| ActQNUDECPUTCP | — | (同上) | — | (同上) | (同上) |
| ActQNUDECPUUDP | — | (同上) | — | (同上) | (同上) |
| ActSIM | — | (同上) | — | (同上) | (同上) |
| ActMLCCBD | — | ActMLProgType | — | — | — |
| ActMLCCG4A | — | (同上) | — | — | — |
| ActMLCCG4Q | — | (同上) | — | — | — |
| ActMLCCG4QnA | — | (同上) | — | — | — |
| ActMLCCIEFADPTCP | — | (同上) | — | — | — |
| ActMLCCIEFADPUDP | — | (同上) | — | — | — |
| ActMLCCIEFBD | — | (同上) | — | — | — |
| ActMLFX485BD | — | (同上) | — | — | — |
| ActMLFXCPU | — | (同上) | — | — | — |
| ActMLFXCPUUSB | — | (同上) | — | — | — |
| ActMLFXENETTCP | — | (同上) | — | — | — |
| ActMLGOT | — | (同上) | — | — | — |
| ActMLGOTTRSP | — | (同上) | — | — | — |
| ActMLLCPU | — | (同上) | — | — | — |
| ActMLLCPUTCP | — | (同上) | — | — | — |
| ActMLLCPUUDP | — | (同上) | — | — | — |
| ActMLLCPUUSB | — | (同上) | — | — | — |
| ActMLLJ71C24 | — | (同上) | — | — | — |
| ActMLLLT | — | (同上) | — | — | — |
| ActMLMnet10BD | — | (同上) | — | — | — |
| ActMLMnet2BD | — | (同上) | — | — | — |
| ActMLMnetGBD | — | (同上) | — | — | — |
| ActMLMnetHBD | — | (同上) | — | — | — |
| ActMLQCPUA | — | (同上) | — | — | — |
| ActMLQCPUQ | — | (同上) | — | — | — |
| ActMLQCPUQBus | — | (同上) | — | — | — |
| ActMLQCPUQUSB | — | (同上) | — | — | — |
| ActMLQJ71C24 | — | (同上) | — | — | — |
| ActMLQJ71E71TCP | — | (同上) | — | — | — |
| ActMLQJ71E71UDP | — | (同上) | — | — | — |
| ActMLQnACPU | — | (同上) | — | — | — |
| ActMLQNUDECPUTCP | — | (同上) | — | — | — |
| ActMLQNUDECPUUDP | — | (同上) | — | — | — |
| ActMLSIM | — | (同上) | — | — | — |
| ActFXCPUTEL | — | — | — | — | — |
| ActLJ71C24TEL | — | — | — | — | — |
| ActQ6TEL | — | — | — | — | — |
| ActQJ71C24TEL | — | — | — | — | — |
| ActSupport | — | ActSupportMsg | — | ActSupportMsg | ActSupportMsg64 |
| ActMLSupport | — | ActMLSupportMsg | — | — | — |
| ActACPU | — | — | — | — | — |
| ActAFBD | — | — | — | — | — |
| ActAJ71C24 | — | — | — | — | — |
| ActAJ71E71TCP | — | — | — | — | — |
| ActAJ71E71UDP | — | — | — | — | — |
| ActAJ71QC24 | — | — | — | — | — |
| ActAJ71QE71TCP | — | — | — | — | — |
| ActAJ71QE71UDP | — | — | — | — | — |
| ActAJ71UC24 | — | — | — | — | — |
| ActAnUBD | — | — | — | — | — |
| ActMLACPU | — | — | — | — | — |
| ActMLAFBD | — | — | — | — | — |
| ActMLAJ71C24 | — | — | — | — | — |
| ActMLAJ71E71TCP | — | — | — | — | — |
| ActMLAJ71E71UDP | — | — | — | — | — |
| ActMLAJ71QC24 | — | — | — | — | — |
| ActMLAJ71QE71TCP | — | — | — | — | — |
| ActMLAJ71QE71UDP | — | — | — | — | — |
| ActMLAJ71UC24 | — | — | — | — | — |
| ActMLAnUBD | — | — | — | — | — |
| ActA6TEL | — | — | — | — | — |
| ActAJ71QC24TEL | — | — | — | — | — |
| — | — | ActProgDataLogging | — | ActProgDataLogging | ActProgDataLogging64 |

> *1 フォームに貼り付けて使用する方法は使用できません。

#### Actコントロール: ユーティリティ設定タイプ (付12 / 686 / 原本 p.688)

| Ver.3 32ビット | Ver.3 64ビット | Ver.4 32ビット | Ver.4 64ビット | Ver.5 32ビット | Ver.5 64ビット*1 |
|---|---|---|---|---|---|
| ActEasyIF | — | ActUtlType | — | ActUtlType | ActUtlType64 |
| ActMLEasyIF | — | ActMLUtlType | — | — | — |
| — | — | ActUtlDataLogging | — | ActUtlDataLogging | ActUtlDataLogging64 |

> *1 フォームに貼り付けて使用する方法は使用できません。

#### .Netコントロール: ユーティリティ設定タイプ (付12 / 686 / 原本 p.688)

| Ver.3 32ビット | Ver.3 64ビット | Ver.4 32ビット | Ver.4 64ビット | Ver.5 32ビット | Ver.5 64ビット*1 |
|---|---|---|---|---|---|
| — | — | DotUtlType | — | DotUtlType | DotUtlType64 |
| — | — | DotSupportMsg | — | ActSupportMsg*2 | ActSupportMsg64 |

> *1 フォームに貼り付けて使用する方法は使用できません。
> *2 DotSupportMsgのコントロールは，Version 5.000AでActSupportMsgに統合しました。

### 置き換えについて (付12 / 687 / 原本 p.689)

MX Component Version 4で作成したプログラムや通信設定は，MX Component Version 5に流用できます。

#### インストール (付12 / 687 / 原本 p.689)

MX Component Version 5は，MX Component Version 4，MX Component Version 3と同じパソコンにインストールできません。
MX Component Version 4，MX Component Version 3をアンインストールしてから，インストールしてください。

#### プログラムの流用 (付12 / 687 / 原本 p.689)

MX Component Version 5には，MX Component Version 4のコントロールが含まれています。
このため，MX Component Version 4のコントロールを使用して作成したプログラムは，MX Component Version 5で動作します。

#### 通信設定の流用 (付12 / 687 / 原本 p.689)

MX Component Version 4の設定ファイル(.ACTファイル)を，MX Component Version 5の通信設定ユーティリティでインポートしてください。(☞68ページ インポート)
MX Component Version 4およびMX Component Version 5のコントロールで使用できます。

##### エクスポート/インポート (付12 / 687 / 原本 p.689)

通信設定のエクスポート/インポートを使用してMX Component Version 4の通信設定およびシステムラベルをMX Component Version 5に流用できます。
通信設定およびシステムラベルの対応表は，下記のとおりです。

| エクスポート | インポート: MX Component Version 4 | インポート: MX Component Version 5 |
|---|---|---|
| MX Component Version 4 | ○ | ○ |
| MX Component Version 5 | × | ○ |

#### コントロールの使用方法 (付12 / 687 / 原本 p.689)

##### 32ビットで使用する場合 (付12 / 687 / 原本 p.689)

MX Component Version 4のDotSupportMsgコントロールをMX Component Version 5で使用する場合は，ActSupportMsgコントロールに置き換えてください。
上記以外のMX Component Version 4のコントロールは，MX Component Version 5で，そのまま使用可能です。

##### 64ビットで使用する場合 (付12 / 687 / 原本 p.689)

- MX Component Version 4のコントロールをオブジェクトを生成して使用していた場合
  64ビット用のコントロールに置き換えることで，MX Component Version 5で使用可能です。(☞684ページ コントロールの比較)

**例**
DotSupportMsg → ActSupportMsg64

- MX Component Version 4のコントロールをフォームに貼り付けて使用していた場合
  MX Component Version 5では，フォームに貼り付けて使用することはできません。
  オブジェクトを生成して使用する方法に変更してください。
  - Visual Basic .NET，Visual C#: ☞48ページ オブジェクトを生成して使用する場合
  - Visual C++: ☞51ページ オブジェクトを生成して使用する場合

---

## 関数索引 (関数索引 / 688 / 原本 p.690)

※ページ番号は原本の印刷ページ番号。複数ある場合は Actコントロール用 / Actコントロール(ロギングファイル転送)用 / .Netコントロール用 の順(該当するもののみ)。

| 頭文字 | 関数名 | 印刷ページ |
|---|---|---|
| C | Close(通信回線のクローズ) | 424，496，505 |
| D | Dispose(メモリの解放) | 602 |
| E | EntryDeviceStatus(デバイスの状態監視登録) | 466，559 |
| F | FreeDeviceStatus(デバイスの状態監視登録解除) | 470，563 |
| G | GetClockData(時計データ読出し) | 452，552 |
| G | GetCpuType(CPUユニット形名読出し) | 461，556 |
| G | GetDevice(デバイスデータの取得) | 441，544 |
| G | GetDevice2(デバイスデータの取得) | 489，599 |
| G | GetErrorMessage(エラー内容と処置方法の取得) | 492 |
| G | GetFile(ロギングファイルの転送) | 502 |
| O | OnDeviceStatus(イベント告知) | 471，564 |
| O | Open(通信回線のオープン) | 422，494，504 |
| R | ReadBuffer(バッファメモリ読出し) | 444，548 |
| R | ReadClose(検索の終了) | 501 |
| R | ReadDeviceBlock(デバイスの一括読出し) | 425，506 |
| R | ReadDeviceBlock2(デバイスの一括読出し) | 474，566 |
| R | ReadDeviceRandom(デバイスのランダム読出し) | 432，518 |
| R | ReadDeviceRandom2(デバイスのランダム読出し) | 480，575 |
| R | ReadFirstFile(ファイル名/ディレクトリ名の検索) | 497 |
| R | ReadNextFile(ファイル名/ディレクトリ名の検索) | 499 |
| S | SetClockData(時計データ書込み) | 457，554 |
| S | SetCpuStatus(リモートコントロール) | 463，557 |
| S | SetDevice(デバイスデータの設定) | 439，540 |
| S | SetDevice2(デバイスデータの設定) | 486，595 |
| W | WriteBuffer(バッファメモリ書込み) | 448，550 |
| W | WriteDeviceBlock(デバイスの一括書込み) | 428，512 |
| W | WriteDeviceBlock2(デバイスの一括書込み) | 477，570 |
| W | WriteDeviceRandom(デバイスのランダム書込み) | 436，529 |
| W | WriteDeviceRandom2(デバイスのランダム書込み) | 483，584 |

---

## 改訂履歴 (改訂履歴 / 690 / 原本 p.692)

*取扱説明書番号は，本説明書の裏表紙の左下に記載してあります。

| 改訂年月 | *取扱説明書番号 | 改訂内容 |
|---|---|---|
| 2021年4月 | SH(名)-082394-A | 初版 |
| 2021年11月 | SH(名)-082394-B | ■追加･修正箇所<br>総称/略称，2.1節，2.4節，5.1節，9.1節，9.2節，10.2節，10.14節，11.2節，12章，13.1節，付1，付12，付13，商標 |
| 2022年3月 | SH(名)-082394-C | ■追加･修正箇所<br>2.1節，付1，付13 |
| 2022年10月 | SH(名)-082394-D | ■追加･修正箇所<br>用語，総称/略称，2.1節，2.4節，9.1節，9.2節，10.2節，10.3節，10.4節，10.14節，11.2節，11.5節，12章，13章，付1，付13 |
| 2023年5月 | SH(名)-082394-E | ■追加･修正箇所<br>2.1節，2.4節，6.1節，8.1節，9.2節，付1，付13 |
| 2023年10月 | SH(名)-082394-F | ■追加･修正箇所<br>総称/略称，2.2節，2.3節，2.4節，2.5節，4章，5.1節，6.16節，8.1節，8.2節，9.2節，10.8節，11.2節，11.3節，11.5節，13.1節，付1，付12 |
| 2024年4月 | SH(名)-082394-G | ■追加･修正箇所<br>2.2節，2.3節，2.5節，5.1節，6.13節，8.1節，9.1節，9.2節，10.2節，10.6節，10.14節，11.3節，13.1節，付1，付5，付12 |
| 2024年12月 | SH(名)-082394-H | ■追加･修正箇所<br>1.2節，1.3節，2.1節，3.1節，4.2節，4.3節，7.1節，9.2節，10.2節，11.3節，付1，付12 |
| 2025年8月 | SH(名)-082394-I | ■追加･修正箇所<br>2.1節，付1，付12 |
| 2026年7月 | SH(名)-082394-J | ■追加･修正箇所<br>安全上のご注意，総称/略称，1.4節，2.4節，3.3節，5.1節，7.3節，8.1節，9.1節，9.2節，10.2節，10.12節，10.16節，11.3節，11.5節，12章，13.1節，付1，付7，付11，付12，著作権 |

> 本書によって，工業所有権その他の権利の実施に対する保証，または実施権を許諾するものではありません。また本書の掲載内容の使用により起因する工業所有権上の諸問題については，当社は一切その責任を負うことができません。

© 2021 MITSUBISHI ELECTRIC CORPORATION

※改訂内容に「付13」が出てくるが，現行版(J)の付録は付12まで(原本どおり)。

---

## 保証について (保証 / 691 / 原本 p.693)

ご使用に際しましては，以下の製品保証内容をご確認いただきますよう，よろしくお願いいたします。

### 1. 無償保証期間と無償保証範囲 (保証 / 691 / 原本 p.693)

無償保証期間中に，製品に当社側の責任による故障や瑕疵（以下併せて「故障」と呼びます）が発生した場合，当社はお買い上げいただきました販売店または当社サービス会社を通じて，無償で製品を修理させていただきます。
ただし，国内および海外における出張修理が必要な場合は，技術者派遣に要する実費を申し受けます。
また，故障ユニットの取替えに伴う現地再調整・試運転は当社責務外とさせていただきます。

**【無償保証期間】**
製品の無償保証期間は，お客様にてご購入後またはご指定場所に納入後 36 ヵ月とさせていただきます。
ただし，当社製品出荷後の流通期間を最長 6 ヵ月として，製造から 42 ヵ月を無償保証期間の上限とさせていただきます。
また，修理品の無償保証期間は，修理前の無償保証期間を超えて長くなることはありません。

**【無償保証範囲】**
(1) 一次故障診断は，原則として貴社にて実施をお願い致します。
ただし，貴社要請により当社，または当社サービス網がこの業務を有償にて代行することができます。この場合，故障原因が当社側にある場合は無償と致します。
(2) 使用状態・使用方法，および使用環境などが，取扱説明書，ユーザーズマニュアル，製品本体注意ラベルなどに記載された条件・注意事項などに従った正常な状態で使用されている場合に限定させていただきます。
(3) 無償保証期間内であっても，以下の場合には有償修理とさせていただきます。
① お客様における不適切な保管や取扱い，不注意，過失などにより生じた故障およびお客様のハードウェアまたはソフトウェア設計内容に起因した故障。
② お客様にて当社の了解なく製品に改造などの手を加えたことに起因する故障。
③ 当社製品がお客様の機器に組み込まれて使用された場合，お客様の機器が受けている法的規制による安全装置または業界の通念上備えられているべきと判断される機能・構造などを備えていれば回避できたと認められる故障。
④ 取扱説明書などに指定された消耗部品が正常に保守・交換されていれば防げたと認められる故障。
⑤ 消耗部品（バッテリ，リレー，ヒューズなど）の交換。
⑥ 火災，異常電圧などの不可抗力による外部要因および地震，雷，風水害などの天変地異による故障。
⑦ 当社出荷当時の科学技術の水準では予見できなかった事由による故障。
⑧ その他，当社の責任外の場合またはお客様が当社責任外と認めた故障。

### 2. 生産中止後の有償修理期間 (保証 / 691 / 原本 p.693)

(1) 当社が有償にて製品修理を受け付けることができる期間は，その製品の生産中止後 7 年間です。
生産中止に関しましては，当社テクニカルニュースなどにて報じさせていただきます。
(2) 生産中止後の製品供給（補用品も含む）はできません。

### 3. 海外でのサービス (保証 / 691 / 原本 p.693)

海外においては，当社の各地域 FA センターで修理受付をさせていただきます。ただし，各 FA センターでの修理条件などが異なる場合がありますのでご了承ください。

### 4. 機会損失，二次損失などへの保証責務の除外 (保証 / 691 / 原本 p.693)

無償保証期間の内外を問わず，以下については当社責務外とさせていただきます。
(1) 当社の責に帰すことができない事由から生じた障害。
(2) 当社製品の故障に起因するお客様での機会損失，逸失利益。
(3) 当社の予見の有無を問わず特別の事情から生じた損害，二次損害，事故補償，当社製品以外への損傷。
(4) お客様による交換作業，現地機械設備の再調整，立上げ試運転その他の業務に対する補償。

### 5. 製品仕様の変更 (保証 / 691 / 原本 p.693)

カタログ，マニュアルもしくは技術資料などに記載の仕様は，お断りなしに変更させていただく場合がありますので，あらかじめご承知おきください。

以　　上

---

## サービスのお問い合わせ (サービス / 692 / 原本 p.694)

修理・サービスに関するお問い合わせはこちらにお問い合わせください。

**三菱電機システムサービス株式会社**

| 拠点 | 電話番号 |
|---|---|
| 北日本支社 | (022) 353-7814 |
| 北海道支店 | (011) 890-7515 |
| 首都圏第２支社 | (03) 3454-5521 |
| 神奈川機器サービスステーション | (045) 938-5420 |
| 関越機器サービスステーション | (048) 708-5910 |
| 新潟機器サービスステーション | (025) 241-7261 |
| 中部支社 | (052) 722-7601 |
| 静岡機器サービスステーション | (054) 287-8866 |
| 北陸支店 | (076) 252-9519 |
| 関西支社 | (06) 6458-9728 |
| 京滋機器サービスステーション | (075) 874-3614 |
| 姫路機器サービスステーション | (079) 269-8845 |
| 中四国支社 | (082) 285-2111 |
| 岡山機器サービスステーション | (086) 242-1900 |
| 四国支店 | (087) 831-3186 |
| 九州支社 | (092) 483-8208 |

## 商標 (商標 / 692 / 原本 p.694)

Intelは，Intel Corporation またはその子会社の商標です。
Javaは，オラクルおよびその関連会社の登録商標です。
Microsoft，Microsoft Access，Excel，Visual Basic .NET，Visual C++，Visual C#，Visual Studio，Windows，Windows Vista，およびWindows XPは，マイクロソフトグループの企業の商標です。
本文中における会社名，システム名，製品名などは，一般に各社の登録商標または商標です。
本文中で，商標記号(™,®)は明記していない場合があります。

## 著作権 (著作権 / 692 / 原本 p.694)

Microsoft Corporationのガイドラインに従って画面写真を使用しています。
SPREAD
Copyright © 2004 FarPoint Technologies, Inc.
VSFlexGrid8 Pro
Copyright © 2008 ComponentOne LLC.
OpenSSL
Copyright © 1995-2025 The OpenSSL Project Authors.
詳細は本製品をインストールしたフォルダ内の"MELSOFT¥ACT¥Licenses¥OpenSsl-License.txt"を参照してください。

---

## 裏表紙 (裏表紙 / 原本 p.696)

**三菱電機株式会社** 〒100-8310 東京都千代田区丸の内2-7-3 (東京ビル)

お問い合わせは下記へどうぞ

| 拠点 | 郵便番号 | 住所 | 電話番号 |
|---|---|---|---|
| 本社機器営業部 | 〒100-8310 | 東京都千代田区丸の内2-7-3 (東京ビル) | (03) 3218-2606 |
| 関越機器営業部 | 〒330-6034 | さいたま市中央区新都心11-2 (明治安田生命さいたま新都心ビル) | (048) 600-5835 |
| 新潟支店 | 〒950-8504 | 新潟市中央区東大通2-4-10 (日本生命新潟ビル) | (025) 241-7227 |
| 神奈川機器営業部 | 〒220-8118 | 横浜市西区みなとみらい2-2-1 (横浜ランドマークタワー) | (045) 224-2624 |
| 北海道支社 | 〒060-8693 | 札幌市中央区大通西3-11 (北洋ビル) | (011) 212-3792 |
| 東北支社 | 〒980-0013 | 仙台市青葉区花京院1-1-20 (花京院スクエア) | (022) 216-4546 |
| 北陸支社 | 〒920-0031 | 金沢市広岡3-1-1 (金沢パークビル) | (076) 233-5502 |
| 中部支社 | 〒450-6423 | 名古屋市中村区名駅3-28-12 (大名古屋ビルヂング) | (052) 565-3314 |
| 豊田支店 | 〒471-0034 | 豊田市小坂本町1-5-10 (矢作豊田ビル) | (0565) 34-4112 |
| 関西支社 | 〒530-8206 | 大阪市北区大深町4-20 (グランフロント大阪タワーA) | (06) 6486-4122 |
| 中国支社 | 〒730-8657 | 広島市中区中町7-32 (ニッセイ広島ビル) | (082) 248-5348 |
| 四国支社 | 〒760-8654 | 高松市寿町1-1-8 (日本生命高松駅前ビル) | (087) 825-0055 |
| 九州支社 | 〒810-8686 | 福岡市中央区天神2-12-1 (天神ビル) | (092) 721-2247 |

**インターネットによる情報サービス「三菱電機FAサイト」**
三菱電機FAサイトでは、製品や事例などの技術情報に加え、トレーニングスクール情報や各種お問い合わせ窓口をご提供しています。また、メンバー登録いただくとマニュアルやCADデータ等のダウンロード、eラーニングなどの各種サービスをご利用いただけます。
(バナー: 三菱電機 FA [検索] www.MitsubishiElectric.co.jp/fa ／ メンバー登録無料!)

**仕様・機能に関するお問い合わせ**
製品ごとにお問い合わせを受け付けております。
三菱電機FAサイト － 仕様・機能に関するお問い合わせ
www.MitsubishiElectric.co.jp/fa/contact-us/spec/
(QRコード画像あり。原本 p.696 参照)

**本マニュアル対象機種の電話技術相談窓口**
共通電話番号にお電話いただき、お客様相談内容に関する代理店、商社への「情報展開可否」を「ご承諾いただける場合は(1)」、「ご承諾いただけない場合は(2)」のいずれかを入力後、「製品番号」を入力してください。
製品番号は、ガイダンスの途中でも入力いただけます。

| 対象機種 | 共通電話番号 | 製品番号 | 受付時間※1 |
|---|---|---|---|
| MELSOFT通信支援ソフトウェアツール | 052-712-2444 | 2→4 | 月曜～木曜 9:00～19:00<br>金曜 9:00～17:00<br>(祝日を除く) |

お問い合わせの際には、今一度電話番号をお確かめの上、お掛け間違いのないようお願いいたします。
※1: 春季・夏季・年末年始の休日を除く

ORIGINAL INSTRUCTIONS
SH(名)-082394-J(2607)
形名: MXCV5-R-J
2026年7月作成

本マニュアルは，お断りなしに仕様を変更することがありますのでご了承ください。
本マニュアルは，輸出する場合，経済産業省への役務取引許可申請は不要です。
