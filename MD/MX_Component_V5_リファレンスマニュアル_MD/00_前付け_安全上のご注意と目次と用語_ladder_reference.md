# MX Component Version 5 リファレンスマニュアル 前付け (原本 p.1-17)

| 項目 | 内容 |
|---|---|
| 原本 | 【三菱】MX Component Version 5 リファレンスマニュアル (SH-082394J) |
| メーカー | 三菱電機 |
| 原本ファイル | `PDF/【三菱】MX Component Version 5 リファレンスマニュアル_sh082394j.pdf` (全696ページ) |
| 本ファイルの範囲 | 表紙，安全上のご注意，製品の適用について，はじめに，目次，関連マニュアル，用語，総称/略称，第1部扉 (印刷ページ 1-15 / PDF p.1-17) |
| 出典表記 | `(節 / 印刷ページ / 原本 p.PDFページ)`。印刷ページ番号のない表紙は PDFページのみ |
| 作成日 | 2026-11-03 |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。
> 本文中の「○ページ」はすべて原本の**印刷ページ番号**です(PDFページ = 印刷ページ + 2)。
> 下の「目次」節は原本目次(p.7-14)の全項目に、PDFページと対応する md ファイル名を併記した**総合索引**です。

## 主要用語 対訳表 (Glossary)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| 安全上のご注意 | Safety precautions | 警告 / 注意 | 参考訳 |
| 警告 / 注意 | WARNING / CAUTION | — | 参考訳 |
| 設計上の注意事項 | Design precautions | — | 参考訳 |
| セキュリティ上の注意事項 | Security precautions | — | 参考訳 |
| インタロック回路 | Interlock circuit | — | 参考訳 |
| 製品の適用について | Conditions of use for the product | — | 参考訳 |
| 関連マニュアル | Related manuals | SH-082394 | 参考訳 |
| ガイドライン | Guideline | XFB3-20PS001 | 参考訳 |
| A系 / B系 | System A / System B | 二重化システム | 参考訳 |
| 制御系 / 待機系 | Control system / Standby system | 二重化システム | 参考訳 |
| 自系 / 他系 | Own system / Other system | 二重化システム | 参考訳 |
| 系切替え | System switching | — | 参考訳 |
| 二重化システム | Redundant system | — | 参考訳 |
| 二重化CPU | Redundant CPU | QnPRH, RnPCPU, RnPSFCPU | 参考訳 |
| 二重化増設ベースユニット | Redundant extension base unit | Q65WRB | 参考訳 |
| Ethernetポート直結接続 | Ethernet port direct connection | — | 参考訳 |
| インテリジェント機能ユニット | Intelligent function module | — | 参考訳 |
| エンジニアリングツール | Engineering tool | — | 参考訳 |
| シーケンスプログラム | Sequence program | — | 参考訳 |
| プロセスCPU | Process CPU | RnPCPU | 参考訳 |
| 安全CPU | Safety CPU | RnSFCPU | 参考訳 |
| マスタ局 / 管理局 | Master station / Control station | — | 参考訳 |
| マルチCPUシステム | Multiple CPU system | 2〜4台 | 参考訳 |
| 管理CPU | Control CPU | マルチCPU | 参考訳 |
| 他局 / 中継局 | Other station / Relay station | — | 参考訳 |
| Actコントロール | Act control (ActiveX control) | — | 参考訳 |
| C言語コントローラ | C Controller | R12CCPU-V, Q12DCCPU-V 等 | 参考訳 |
| Ethernetアダプタユニット | Ethernet adapter module | NZ2GF-ETB | 参考訳 |
| Ethernetユニット | Ethernet module | E71 | 参考訳 |
| Ethernet内蔵形CPU / Ethernetポート内蔵QCPU | Built-in Ethernet port CPU / Built-in Ethernet port QCPU | — | 参考訳 |
| シリアルコミュニケーションユニット | Serial communication module | C24, FX拡張ポート | 参考訳 |
| MXコントローラ | MX Controller | MX-Rモデル(MXR300/MXR500), MX-Fモデル(MXF100) | 参考訳 |
| ハイパフォーマンスモデルQCPU / ベーシックモデルQCPU | High Performance model QCPU / Basic model QCPU | — | 参考訳 |
| ロボットコントローラ | Robot controller | CR750-D, CRnD-700 | 参考訳 |

## 変換範囲表

| 原本ページ(PDF) | 印刷ページ | 節 | 扱い |
|---|---|---|---|
| p.1 | — | 表紙 | 全文(ロゴ・表紙イラストは除外: 文字情報なし) |
| p.2 | — | 表紙裏 | 除外: 白紙 |
| p.3-4 | 1-2 | 安全上のご注意 | 全文 |
| p.5 | 3 | 製品の適用について | 全文 |
| p.6 | 4 | はじめに | 全文 |
| p.7-14 | 5-12 | 目次 | 全項目(下の「目次」節。PDFページ・対応mdファイルを併記) |
| p.15 | 13 | 関連マニュアル / ガイドライン / 用語 | 全文 |
| p.16 | 14 | 総称/略称 | 全文 |
| p.17 | 15 | 第1部 扉 | 全文 |
| p.18-696 | 16-692 | 第1章〜巻末 | 変換済み: 01_〜13-3_，付録-1_〜付録-3_ の別ファイル(下の目次の「対応mdファイル」列を参照) |

## 目次

- 表紙
- 安全上のご注意
- 製品の適用について
- はじめに
- 目次(原本目次の全項目＋対応mdファイル)
- 関連マニュアル / ガイドライン
- 用語
- 総称/略称
- 第1部 扉

---

## 表紙 (表紙 / 原本 p.1)

- MITSUBISHI ELECTRIC(ロゴ) / MELSOFT
- エンジニアリングソフトウェア
- MX Component Version 5
- リファレンスマニュアル
- -SW5DND-ACT-J

【図】表紙右下にソフトウェア画面のコラージュ(文字情報なし)

---

## 安全上のご注意 (安全上のご注意 / 1-2 / 原本 p.3-4)

(ご使用前に必ずお読みください)

本製品のご使用に際しては，本マニュアルをよくお読みいただくと共に，安全に対して十分に注意を払って，正しい取扱いをしていただくようお願いいたします。製造業者が指定していない方法で機器を用いると，機器が備えている保護が損なわれることがあります。
本マニュアルで示す注意事項は，本製品に関するもののみについて記載したものです。シーケンサシステムとしての安全上のご注意に関しては，使用するユニットのユーザーズマニュアルおよびMELSEC iQ-R ユニット構成マニュアルを参照してください。
この「安全上のご注意」では，安全注意事項のランクを「⚠警告」，「⚠注意」として区分してあります。

| ランク | 内容 |
|---|---|
| ⚠警告 | 取扱いを誤った場合に，危険な状況が起こりえて，死亡または重傷を受ける可能性が想定される場合。 |
| ⚠注意 | 取扱いを誤った場合に，危険な状況が起こりえて，中程度の傷害や軽傷を受ける可能性が想定される場合および物的損害だけの発生が想定される場合。 |

なお，⚠注意に記載した事項でも，状況によっては重大な結果に結びつく可能性があります。
いずれも重要な内容を記載していますので必ず守ってください。
本マニュアルは必要なときに読めるよう大切に保管すると共に，必ず最終ユーザまでお届けいただくようお願いいたします。

### [設計上の注意事項] ⚠警告 (安全上のご注意 / 1 / 原本 p.3)

- パソコンから運転中のシーケンサに対するデータ変更，状態制御は常にシステム全体が安全側に働くようにシーケンサシステムの外部でインタロック回路を構成してください。
  また，周辺機器からCPUユニットへのオンライン操作において，ケーブルの接続不良などによる交信異常発生時のシステムとしての処置方法を取り決めておいてください。

### [設計上の注意事項] ⚠注意 (安全上のご注意 / 1 / 原本 p.3)

- パソコンを運転中のCPUユニットに接続して行うオンライン操作(特に強制出力，運転状態の変更)については，マニュアルを熟読し十分に安全を確認の上実施してください。
  操作ミスにより機械の破損や事故の原因になります。
- 災害やシステムトラブルに備えるため，データは安全な場所に適切に保存してください。
- 大量のデバイスデータを扱う場合，システムが不安定になる可能性があるため，適切なデータ量で運用を実施してください。

### [セキュリティ上の注意事項] ⚠警告 (安全上のご注意 / 2 / 原本 p.4)

- ネットワーク経由による外部機器からの不正アクセス，DoS攻撃，コンピュータウイルスその他のサイバー攻撃に対して，シーケンサ，およびシステムのセキュリティ (可用性，完全性，機密性)を保つため，ファイアウォールやVPNの設置，コンピュータへのアンチウイルスソフト導入などの対策を盛り込んでください。
- パソコンおよびシーケンサへの不正アクセスを防止するため，Windowsセキュリティ機能で適切なユーザ権限を設定し，認証されたユーザのみ使用可能としてください。
- 情報漏洩やデータの改ざん防止のため，MX Componentを使用して作成および取得したデータは適切にアクセス管理を行い，またデータの暗号化を行うなど適切にデータを管理してください。
  MX Componentを使用した端末を破棄する場合，MX Componentの設定情報の削除のため，アンインストールを行ってください。
- システムの脆弱性をついた攻撃を防止するため，使用しているシステムの脆弱性についての最新の情報を確認し，必要な対策を実施してください。当社製品の脆弱性については三菱電機FAサイトにて確認してください。
- 暗号化通信を使用しない場合，データの改ざんや情報漏洩の危険があるため，ネットワークの安全が担保された環境で使用してください。

---

## 製品の適用について (製品の適用について / 3 / 原本 p.5)

（1）当社シーケンサをご使用いただくにあたりましては，万一シーケンサに故障・不具合などが発生した場合でも重大な事故にいたらない用途であること，および故障・不具合発生時にはバックアップやフェールセーフ機能が機器外部でシステム的に実施されていることをご使用の条件とさせていただきます。

（2）当社シーケンサは，一般工業などへの用途を対象とした汎用品として設計・製作されています。
したがいまして，以下のような機器・システムなどの特殊用途へのご使用については，当社シーケンサの適用を除外させていただきます。万一使用された場合は当社として当社シーケンサの品質，性能，安全に関る一切の責任（債務不履行責任，瑕疵担保責任，品質保証責任，不法行為責任，製造物責任を含むがそれらに限定されない）を負わないものとさせていただきます。

・各電力会社殿の原子力発電所およびその他発電所向けなどの公共への影響が大きい用途  
・鉄道各社殿および官公庁殿など，特別な品質保証体制の構築を当社にご要求になる用途  
・航空宇宙，医療，鉄道，燃焼・燃料装置，乗用移動体，有人搬送装置，娯楽機械，安全機械など生命，身体，財産に大きな影響が予測される用途

ただし，上記の用途であっても，具体的に使途を限定すること，特別な品質（一般仕様を超えた品質等）をご要求されないこと等を条件に，当社の判断にて当社シーケンサの適用可とする場合もございますので，詳細につきましては当社窓口へご相談ください。

（3）DoS攻撃，不正アクセス，コンピュータウイルスその他のサイバー攻撃により発生するシーケンサ，およびシステムトラブル上の諸問題に対して，当社はその責任を負わないものとさせていただきます。

---

## はじめに (はじめに / 4 / 原本 p.6)

このたびは，エンジニアリングソフトウェア MELSOFTシリーズをお買い上げいただきまことにありがとうございました。
本マニュアルは，MX Componentについてご理解いただくためのマニュアルです。
ご使用前に本マニュアルや関連マニュアルをよくお読みいただき，MX Componentの機能・性能を十分ご理解のうえ，正しくご使用くださるようお願いいたします。
なお，ご使用のOSとOSバージョンによってはメニュー名や操作手順が異なる場合があります。本マニュアルをお読みいただく際は，必要に応じてご使用のOSとOSバージョンに読み替えてください。

---

## 目次 (目次 / 5-12 / 原本 p.7-14)

原本目次の全項目(375項目)。「印刷ページ」は原本目次の記載値、「PDFページ」= 印刷ページ + 2、「対応mdファイル」は本シリーズで当該ページを収録しているファイル。階層: 前付け / 部 / 章 / 節(n.n・付n) / 項 / 巻末。

| 階層 | 項目 | 印刷ページ | PDFページ | 対応mdファイル |
|---|---|---|---|---|
| 前付け | 安全上のご注意 | 1 | 3 | 00_前付け(本ファイル) |
| 前付け | 製品の適用について | 3 | 5 | 00_前付け(本ファイル) |
| 前付け | はじめに | 4 | 6 | 00_前付け(本ファイル) |
| 前付け | 関連マニュアル | 13 | 15 | 00_前付け(本ファイル) |
| 前付け | 用語 | 13 | 15 | 00_前付け(本ファイル) |
| 前付け | 総称/略称 | 14 | 16 | 00_前付け(本ファイル) |
| 部 | 第1部 基本と開発の流れ | — | — | — |
| 章 | 第1章 MX Componentの基本 | 16 | 18 | 01_MX_Componentの基本_ladder_reference.md |
| 節 | 1.1 ご使用の前に | 16 | 18 | 01_MX_Componentの基本_ladder_reference.md |
| 項 | MX Componentの活用 | 16 | 18 | 01_MX_Componentの基本_ladder_reference.md |
| 節 | 1.2 コントロールの種類 | 21 | 23 | 01_MX_Componentの基本_ladder_reference.md |
| 項 | コントロール一覧 | 21 | 23 | 01_MX_Componentの基本_ladder_reference.md |
| 節 | 1.3 ラベルの種類 | 22 | 24 | 01_MX_Componentの基本_ladder_reference.md |
| 項 | グローバルラベル名を指定したデータ取得 | 22 | 24 | 01_MX_Componentの基本_ladder_reference.md |
| 節 | 1.4 ユーティリティの種類 | 27 | 29 | 01_MX_Componentの基本_ladder_reference.md |
| 章 | 第2章 システム構成 | 29 | 31 | 02_システム構成_ladder_reference.md |
| 節 | 2.1 動作環境 | 29 | 31 | 02_システム構成_ladder_reference.md |
| 節 | 2.2 サポートする通信経路 | 29 | 31 | 02_システム構成_ladder_reference.md |
| 節 | 2.3 システム構成一覧 | 30 | 32 | 02_システム構成_ladder_reference.md |
| 項 | 各通信経路のシステム構成例 | 30 | 32 | 02_システム構成_ladder_reference.md |
| 節 | 2.4 使用可能な機種一覧 | 32 | 34 | 02_システム構成_ladder_reference.md |
| 項 | CPUユニット | 32 | 34 | 02_システム構成_ladder_reference.md |
| 項 | ユニット | 34 | 36 | 02_システム構成_ladder_reference.md |
| 節 | 2.5 各通信経路の詳細内容 | 35 | 37 | 02_システム構成_ladder_reference.md |
| 章 | 第3章 ユーザプログラムの開発手順 | 41 | 43 | 03_ユーザプログラムの開発手順_ladder_reference.md |
| 節 | 3.1 MX Componentのインストール | 41 | 43 | 03_ユーザプログラムの開発手順_ladder_reference.md |
| 項 | バージョンの確認 | 41 | 43 | 03_ユーザプログラムの開発手順_ladder_reference.md |
| 項 | マニュアルを開く | 41 | 43 | 03_ユーザプログラムの開発手順_ladder_reference.md |
| 節 | 3.2 使用するコントロールの把握 | 42 | 44 | 03_ユーザプログラムの開発手順_ladder_reference.md |
| 節 | 3.3 通信設定方法の選択 | 42 | 44 | 03_ユーザプログラムの開発手順_ladder_reference.md |
| 節 | 3.4 ユーザプログラムへのコントロールの追加 | 43 | 45 | 03_ユーザプログラムの開発手順_ladder_reference.md |
| 節 | 3.5 ユーザプログラムの新規作成 | 43 | 45 | 03_ユーザプログラムの開発手順_ladder_reference.md |
| 節 | 3.6 通信設定 | 43 | 45 | 03_ユーザプログラムの開発手順_ladder_reference.md |
| 節 | 3.7 プログラミング | 43 | 45 | 03_ユーザプログラムの開発手順_ladder_reference.md |
| 章 | 第4章 ユーザプログラムへのコントロールの追加 | 44 | 46 | 04_ユーザプログラムへのコントロールの追加_ladder_reference.md |
| 節 | 4.1 VBAを使用する場合 | 44 | 46 | 04_ユーザプログラムへのコントロールの追加_ladder_reference.md |
| 節 | 4.2 Visual Basic .NET，Visual C#を使用する場合 | 48 | 50 | 04_ユーザプログラムへのコントロールの追加_ladder_reference.md |
| 節 | 4.3 Visual C++を使用する場合 | 51 | 53 | 04_ユーザプログラムへのコントロールの追加_ladder_reference.md |
| 章 | 第5章 通信設定 | 56 | 58 | 05_通信設定_ladder_reference.md |
| 節 | 5.1 ユーティリティを使った設定 | 56 | 58 | 05_通信設定_ladder_reference.md |
| 項 | 通信設定ユーティリティの起動 | 56 | 58 | 05_通信設定_ladder_reference.md |
| 項 | [通信設定]タブ | 57 | 59 | 05_通信設定_ladder_reference.md |
| 項 | [一覧表示]タブ | 62 | 64 | 05_通信設定_ladder_reference.md |
| 項 | [通信テスト]タブ | 63 | 65 | 05_通信設定_ladder_reference.md |
| 項 | ユーザ認証情報管理 | 64 | 66 | 05_通信設定_ladder_reference.md |
| 項 | 通信の暗号化(証明書管理) | 66 | 68 | 05_通信設定_ladder_reference.md |
| 項 | 通信設定のエクスポートとインポート | 68 | 70 | 05_通信設定_ladder_reference.md |
| 項 | 作成した論理局番をプログラムの中で指定する | 70 | 72 | 05_通信設定_ladder_reference.md |
| 節 | 5.2 プログラムで設定する | 71 | 73 | 05_通信設定_ladder_reference.md |
| 項 | 通信設定ユーティリティでプロパティを確認する | 71 | 73 | 05_通信設定_ladder_reference.md |
| 項 | ユーザプログラムの中で必要なプロパティを設定する | 73 | 75 | 05_通信設定_ladder_reference.md |
| 章 | 第6章 通信設定例(ユーティリティ使用時) | 74 | 76 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 節 | 6.1 シリアルコミュニケーション通信 | 74 | 76 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 項 | アクセスまでの手順 | 74 | 76 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 項 | 論理局番の設定例 | 75 | 77 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 項 | シリアルコミュニケーションユニットの設定 | 76 | 78 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 節 | 6.2 Ethernet通信(Ethernetユニット使用時) | 81 | 83 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 項 | アクセスまでの手順 | 81 | 83 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 項 | 論理局番の設定例 | 82 | 84 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 項 | ユニットの設定 | 83 | 85 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 節 | 6.3 Ethernet通信(Ethernet内蔵形CPU使用時) | 85 | 87 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 項 | アクセスまでの手順 | 85 | 87 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 項 | 論理局番の設定例 | 86 | 88 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 項 | ユニットの設定 | 87 | 89 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 節 | 6.4 Ethernet通信(Ethernetアダプタユニット使用時) | 88 | 90 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 項 | アクセスまでの手順 | 88 | 90 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 項 | 論理局番の設定例 | 88 | 90 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 節 | 6.5 Ethernet通信(Ethernetアダプタ使用時) | 89 | 91 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 項 | アクセスまでの手順 | 89 | 91 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 項 | 論理局番の設定例 | 90 | 92 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 節 | 6.6 CPU COM通信 | 91 | 93 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 項 | アクセスまでの手順 | 91 | 93 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 項 | 論理局番の設定例 | 91 | 93 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 節 | 6.7 CPU USB通信 | 92 | 94 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 項 | アクセスまでの手順 | 92 | 94 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 項 | 論理局番の設定例 | 92 | 94 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 節 | 6.8 CC-Link通信 | 93 | 95 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 項 | アクセスまでの手順 | 93 | 95 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 項 | 論理局番の設定例 | 94 | 96 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 項 | ユニットの設定 | 95 | 97 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 節 | 6.9 CC-Linkシステム RS-232インタフェース通信 | 96 | 98 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 項 | アクセスまでの手順 | 96 | 98 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 項 | 論理局番の設定例 | 96 | 98 | 06a_通信設定例_シリアルからCC-LinkRS232_ladder_reference.md |
| 節 | 6.10 GX Simulator2通信 | 97 | 99 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | アクセスまでの手順 | 97 | 99 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | 論理局番の設定例 | 97 | 99 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 節 | 6.11 GX Simulator3通信 | 98 | 100 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | アクセスまでの手順 | 98 | 100 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | 論理局番の設定例 | 99 | 101 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 節 | 6.12 MT Simulator2通信 | 100 | 102 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | アクセスまでの手順 | 100 | 102 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | 論理局番の設定例 | 100 | 102 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 節 | 6.13 MELSOFT Mirror通信 | 101 | 103 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | アクセスまでの手順 | 101 | 103 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | 論理局番の設定例 | 102 | 104 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 節 | 6.14 MELSECNET/H通信 | 103 | 105 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | アクセスまでの手順 | 103 | 105 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | 論理局番の設定例 | 103 | 105 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 節 | 6.15 CC-Link IEコントローラネットワーク通信 | 105 | 107 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | アクセスまでの手順 | 105 | 107 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | 論理局番の設定例 | 105 | 107 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 節 | 6.16 CC-Link IEフィールドネットワーク通信 | 108 | 110 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | アクセスまでの手順 | 108 | 110 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | 論理局番の設定例 | 108 | 110 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 節 | 6.17 CC-Link IE TSN通信 | 110 | 112 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | アクセスまでの手順 | 110 | 112 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | 論理局番の設定例 | 110 | 112 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 節 | 6.18 GOTゲートウェイデバイス通信 | 112 | 114 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | アクセスまでの手順 | 112 | 114 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | 論理局番の設定例 | 113 | 115 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 節 | 6.19 GOTトランスペアレント通信 | 114 | 116 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | アクセスまでの手順 | 114 | 116 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | 論理局番の設定例 | 115 | 117 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 節 | 6.20 インバータCOM通信 | 116 | 118 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | アクセスまでの手順 | 116 | 118 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | 論理局番の設定例 | 116 | 118 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 節 | 6.21 インバータUSB通信 | 117 | 119 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | アクセスまでの手順 | 117 | 119 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | 論理局番の設定例 | 117 | 119 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 節 | 6.22 ロボットコントローラCOM通信 | 118 | 120 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | アクセスまでの手順 | 118 | 120 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | 論理局番の設定例 | 118 | 120 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 節 | 6.23 ロボットコントローラUSB通信 | 119 | 121 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | アクセスまでの手順 | 119 | 121 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | 論理局番の設定例 | 119 | 121 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 節 | 6.24 ロボットコントローラEthernet通信 | 120 | 122 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | アクセスまでの手順 | 120 | 122 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 項 | 論理局番の設定例 | 120 | 122 | 06b_通信設定例_シミュレータからロボットコントローラ_ladder_reference.md |
| 章 | 第7章 プログラミング | 121 | 123 | 07a_プログラミング_ラベル管理ユーティリティ_ladder_reference.md |
| 節 | 7.1 ラベル管理ユーティリティを使ったラベルの作成 | 121 | 123 | 07a_プログラミング_ラベル管理ユーティリティ_ladder_reference.md |
| 項 | ラベル管理ユーティリティの起動 | 121 | 123 | 07a_プログラミング_ラベル管理ユーティリティ_ladder_reference.md |
| 項 | ラベル管理画面 | 121 | 123 | 07a_プログラミング_ラベル管理ユーティリティ_ladder_reference.md |
| 項 | 論理局番の登録/削除 | 123 | 125 | 07a_プログラミング_ラベル管理ユーティリティ_ladder_reference.md |
| 項 | システムラベルリスト | 124 | 126 | 07a_プログラミング_ラベル管理ユーティリティ_ladder_reference.md |
| 項 | 構造体設定 | 129 | 131 | 07a_プログラミング_ラベル管理ユーティリティ_ladder_reference.md |
| 項 | ワークスペースの参照登録/解除 | 130 | 132 | 07a_プログラミング_ラベル管理ユーティリティ_ladder_reference.md |
| 項 | 変更通知 | 131 | 133 | 07a_プログラミング_ラベル管理ユーティリティ_ladder_reference.md |
| 項 | システムラベルデータの最新化 | 132 | 134 | 07a_プログラミング_ラベル管理ユーティリティ_ladder_reference.md |
| 項 | ラベルスペースのエクスポートとインポート | 133 | 135 | 07a_プログラミング_ラベル管理ユーティリティ_ladder_reference.md |
| 項 | システムラベルについて | 134 | 136 | 07b_プログラミング_システムラベルとコーディングとデバッグ_ladder_reference.md |
| 節 | 7.2 コーディング | 148 | 150 | 07b_プログラミング_システムラベルとコーディングとデバッグ_ladder_reference.md |
| 節 | 7.3 デバッグ | 149 | 151 | 07b_プログラミング_システムラベルとコーディングとデバッグ_ladder_reference.md |
| 項 | シーケンサモニタユーティリティを使って値の確認をする | 149 | 151 | 07b_プログラミング_システムラベルとコーディングとデバッグ_ladder_reference.md |
| 部 | 第2部 プログラムの詳細仕様 | — | — | — |
| 章 | 第8章 アクセス可能デバイスおよびデバイスタイプ | 160 | 162 | 08a_アクセス可能デバイス_ladder_reference.md |
| 節 | 8.1 アクセス可能デバイス | 160 | 162 | 08a_アクセス可能デバイス_ladder_reference.md |
| 項 | アクセス先がCPUユニット(モーションCPUおよびWinCPU以外) | 161 | 163 | 08a_アクセス可能デバイス_ladder_reference.md |
| 項 | アクセス先がモーションCPU | 163 | 165 | 08a_アクセス可能デバイス_ladder_reference.md |
| 項 | アクセス先がWinCPU | 164 | 166 | 08a_アクセス可能デバイス_ladder_reference.md |
| 項 | アクセス先がRnSFCPUおよびRnPSFCPU(安全デバイス) | 164 | 166 | 08a_アクセス可能デバイス_ladder_reference.md |
| 項 | アクセス先がCC-Link通信時の自ボード | 165 | 167 | 08a_アクセス可能デバイス_ladder_reference.md |
| 項 | アクセス先がMELSECNET/H通信時の自ボード | 165 | 167 | 08a_アクセス可能デバイス_ladder_reference.md |
| 項 | アクセス先がCC-Link IEコントローラネットワーク通信時の自ボード | 165 | 167 | 08a_アクセス可能デバイス_ladder_reference.md |
| 項 | アクセス先がCC-Link IEフィールドネットワーク通信時の自ボード | 165 | 167 | 08a_アクセス可能デバイス_ladder_reference.md |
| 項 | アクセス先がCC-Link IE TSN通信時の自ボード | 166 | 168 | 08a_アクセス可能デバイス_ladder_reference.md |
| 項 | アクセス先がインバータ | 167 | 169 | 08a_アクセス可能デバイス_ladder_reference.md |
| 項 | アクセス先がロボットコントローラ | 168 | 170 | 08a_アクセス可能デバイス_ladder_reference.md |
| 節 | 8.2 デバイスタイプ | 169 | 171 | 08b_デバイスタイプ_ladder_reference.md |
| 章 | 第9章 コントロールのプロパティ | 176 | 178 | 09_コントロールのプロパティ_ladder_reference.md |
| 節 | 9.1 プロパティ一覧 | 176 | 178 | 09_コントロールのプロパティ_ladder_reference.md |
| 節 | 9.2 プロパティの詳細 | 178 | 180 | 09_コントロールのプロパティ_ladder_reference.md |
| 章 | 第10章 各通信経路で設定するプロパティ | 190 | 192 | 10-1_各通信経路のプロパティ_シリアルとE71iQR_ladder_reference.md |
| 節 | 10.1 シリアルコミュニケーション通信 | 190 | 192 | 10-1_各通信経路のプロパティ_シリアルとE71iQR_ladder_reference.md |
| 項 | 接続局がMELSEC iQ-Rシリーズ対応C24のシリアルコミュニケーション通信(1) | 190 | 192 | 10-1_各通信経路のプロパティ_シリアルとE71iQR_ladder_reference.md |
| 項 | 接続局がMELSEC iQ-Rシリーズ対応C24のシリアルコミュニケーション通信(2) | 193 | 195 | 10-1_各通信経路のプロパティ_シリアルとE71iQR_ladder_reference.md |
| 項 | 接続局がQシリーズ対応C24のシリアルコミュニケーション通信(1) | 195 | 197 | 10-1_各通信経路のプロパティ_シリアルとE71iQR_ladder_reference.md |
| 項 | 接続局がQシリーズ対応C24のシリアルコミュニケーション通信(2) | 198 | 200 | 10-1_各通信経路のプロパティ_シリアルとE71iQR_ladder_reference.md |
| 項 | 接続局がLシリーズ対応C24のシリアルコミュニケーション通信(1) | 200 | 202 | 10-1_各通信経路のプロパティ_シリアルとE71iQR_ladder_reference.md |
| 項 | 接続局がLシリーズ対応C24のシリアルコミュニケーション通信(2) | 203 | 205 | 10-1_各通信経路のプロパティ_シリアルとE71iQR_ladder_reference.md |
| 項 | 接続局がFX拡張ポートのシリアルコミュニケーション通信 | 205 | 207 | 10-1_各通信経路のプロパティ_シリアルとE71iQR_ladder_reference.md |
| 節 | 10.2 Ethernet通信 | 207 | 209 | 10-1_各通信経路のプロパティ_シリアルとE71iQR_ladder_reference.md |
| 項 | 接続局がMELSEC iQ-Rシリーズ対応E71のEthernet通信(TCP) | 207 | 209 | 10-1_各通信経路のプロパティ_シリアルとE71iQR_ladder_reference.md |
| 項 | 接続局がMELSEC iQ-Rシリーズ対応E71のEthernet通信(UDP) | 210 | 212 | 10-1_各通信経路のプロパティ_シリアルとE71iQR_ladder_reference.md |
| 項 | 接続局がQシリーズ対応E71のEthernet通信(TCP) | 213 | 215 | 10-2_各通信経路のプロパティ_E71QLとCPU内蔵Ethernet_ladder_reference.md |
| 項 | 接続局がQシリーズ対応E71のEthernet通信(UDP) | 216 | 218 | 10-2_各通信経路のプロパティ_E71QLとCPU内蔵Ethernet_ladder_reference.md |
| 項 | 接続局がLシリーズ対応E71のEthernet通信(TCP) | 219 | 221 | 10-2_各通信経路のプロパティ_E71QLとCPU内蔵Ethernet_ladder_reference.md |
| 項 | 接続局がLシリーズ対応E71のEthernet通信(UDP) | 222 | 224 | 10-2_各通信経路のプロパティ_E71QLとCPU内蔵Ethernet_ladder_reference.md |
| 項 | 接続局がMELSEC iQ-RシリーズCPUユニットのEthernet通信(TCP) | 225 | 227 | 10-2_各通信経路のプロパティ_E71QLとCPU内蔵Ethernet_ladder_reference.md |
| 項 | 接続局がMELSEC iQ-RシリーズCPUユニットのEthernet通信(UDP) | 229 | 231 | 10-2_各通信経路のプロパティ_E71QLとCPU内蔵Ethernet_ladder_reference.md |
| 項 | 接続局がLHCPUのEthernet通信(TCP) | 233 | 235 | 10-2_各通信経路のプロパティ_E71QLとCPU内蔵Ethernet_ladder_reference.md |
| 項 | 接続局がLHCPUのEthernet通信(UDP) | 235 | 237 | 10-2_各通信経路のプロパティ_E71QLとCPU内蔵Ethernet_ladder_reference.md |
| 項 | 接続局がFX5CPUのEthernet通信(TCP) | 237 | 239 | 10-2_各通信経路のプロパティ_E71QLとCPU内蔵Ethernet_ladder_reference.md |
| 項 | 接続局がFX5CPUのEthernet通信(UDP) | 239 | 241 | 10-2_各通信経路のプロパティ_E71QLとCPU内蔵Ethernet_ladder_reference.md |
| 項 | 接続局がEthernetポート内蔵QCPUのEthernet通信(TCP) | 241 | 243 | 10-3_各通信経路のプロパティ_内蔵QCPU_LCPUとEthernetアダプタユニット_ladder_reference.md |
| 項 | 接続局がEthernetポート内蔵QCPUのEthernet通信(UDP) | 245 | 247 | 10-3_各通信経路のプロパティ_内蔵QCPU_LCPUとEthernetアダプタユニット_ladder_reference.md |
| 項 | 接続局がEthernetポート内蔵LCPUのEthernet通信(TCP) | 249 | 251 | 10-3_各通信経路のプロパティ_内蔵QCPU_LCPUとEthernetアダプタユニット_ladder_reference.md |
| 項 | 接続局がEthernetポート内蔵LCPUのEthernet通信(UDP) | 252 | 254 | 10-3_各通信経路のプロパティ_内蔵QCPU_LCPUとEthernetアダプタユニット_ladder_reference.md |
| 項 | 接続局がEthernetアダプタユニットのEthernet通信(TCP) | 255 | 257 | 10-3_各通信経路のプロパティ_内蔵QCPU_LCPUとEthernetアダプタユニット_ladder_reference.md |
| 項 | 接続局がEthernetアダプタユニットのEthernet通信(UDP) | 259 | 261 | 10-3_各通信経路のプロパティ_内蔵QCPU_LCPUとEthernetアダプタユニット_ladder_reference.md |
| 項 | 接続局がEthernetアダプタのEthernet通信(TCP)(1) | 263 | 265 | 10-4_各通信経路のプロパティ_EthernetアダプタからTSNとCPUCOM_ladder_reference.md |
| 項 | 接続局がEthernetアダプタのEthernet通信(TCP)(2) | 264 | 266 | 10-4_各通信経路のプロパティ_EthernetアダプタからTSNとCPUCOM_ladder_reference.md |
| 項 | 接続局がEthernetアダプタのEthernet通信(UDP)(1) | 266 | 268 | 10-4_各通信経路のプロパティ_EthernetアダプタからTSNとCPUCOM_ladder_reference.md |
| 項 | 接続局がEthernetアダプタのEthernet通信(UDP)(2) | 267 | 269 | 10-4_各通信経路のプロパティ_EthernetアダプタからTSNとCPUCOM_ladder_reference.md |
| 項 | 接続局がEthernetアダプタのEthernet通信(UDP)(3) | 269 | 271 | 10-4_各通信経路のプロパティ_EthernetアダプタからTSNとCPUCOM_ladder_reference.md |
| 項 | 接続局がロボットコントローラのEthernet通信 | 271 | 273 | 10-4_各通信経路のプロパティ_EthernetアダプタからTSNとCPUCOM_ladder_reference.md |
| 項 | 接続局がCC-Link IE TSNユニットのEthernet通信(TCP) | 272 | 274 | 10-4_各通信経路のプロパティ_EthernetアダプタからTSNとCPUCOM_ladder_reference.md |
| 項 | 接続局がCC-Link IE TSNユニットのEthernet通信(UDP) | 275 | 277 | 10-4_各通信経路のプロパティ_EthernetアダプタからTSNとCPUCOM_ladder_reference.md |
| 節 | 10.3 CPU COM通信 | 278 | 280 | 10-4_各通信経路のプロパティ_EthernetアダプタからTSNとCPUCOM_ladder_reference.md |
| 項 | 接続局がFX5CPUのCPU COM通信 | 278 | 280 | 10-4_各通信経路のプロパティ_EthernetアダプタからTSNとCPUCOM_ladder_reference.md |
| 項 | 接続局がQCPU(Qモード)のCPU COM通信 | 280 | 282 | 10-4_各通信経路のプロパティ_EthernetアダプタからTSNとCPUCOM_ladder_reference.md |
| 項 | 接続局がLCPUのCPU COM通信 | 283 | 285 | 10-4_各通信経路のプロパティ_EthernetアダプタからTSNとCPUCOM_ladder_reference.md |
| 項 | 接続局がQモーションCPUのCPU COM通信 | 286 | 288 | 10-4_各通信経路のプロパティ_EthernetアダプタからTSNとCPUCOM_ladder_reference.md |
| 項 | 接続局がFXCPUのCPU COM通信 | 288 | 290 | 10-4_各通信経路のプロパティ_EthernetアダプタからTSNとCPUCOM_ladder_reference.md |
| 項 | 接続局がインバータのCPU COM通信 | 290 | 292 | 10-4_各通信経路のプロパティ_EthernetアダプタからTSNとCPUCOM_ladder_reference.md |
| 項 | 接続局がロボットコントローラのCPU COM通信 | 291 | 293 | 10-4_各通信経路のプロパティ_EthernetアダプタからTSNとCPUCOM_ladder_reference.md |
| 節 | 10.4 CPU USB通信 | 292 | 294 | 10-5_各通信経路のプロパティ_CPUUSBとMELSECNETH_ladder_reference.md |
| 項 | 接続局がRCPUのCPU USB通信 | 292 | 294 | 10-5_各通信経路のプロパティ_CPUUSBとMELSECNETH_ladder_reference.md |
| 項 | 接続局がRモーションCPUのCPU USB通信 | 295 | 297 | 10-5_各通信経路のプロパティ_CPUUSBとMELSECNETH_ladder_reference.md |
| 項 | 接続局がLHCPUのCPU USB通信 | 297 | 299 | 10-5_各通信経路のプロパティ_CPUUSBとMELSECNETH_ladder_reference.md |
| 項 | 接続局がFX5CPUのCPU USB通信 | 299 | 301 | 10-5_各通信経路のプロパティ_CPUUSBとMELSECNETH_ladder_reference.md |
| 項 | 接続局がQCPU(Qモード)のCPU USB通信 | 301 | 303 | 10-5_各通信経路のプロパティ_CPUUSBとMELSECNETH_ladder_reference.md |
| 項 | 接続局がLCPUのCPU USB通信 | 304 | 306 | 10-5_各通信経路のプロパティ_CPUUSBとMELSECNETH_ladder_reference.md |
| 項 | 接続局がQSCPUのCPU USB通信 | 307 | 309 | 10-5_各通信経路のプロパティ_CPUUSBとMELSECNETH_ladder_reference.md |
| 項 | 接続局がQモーションCPUのCPU USB通信 | 308 | 310 | 10-5_各通信経路のプロパティ_CPUUSBとMELSECNETH_ladder_reference.md |
| 項 | 接続局がFXCPUのCPU USB通信 | 309 | 311 | 10-5_各通信経路のプロパティ_CPUUSBとMELSECNETH_ladder_reference.md |
| 項 | 接続局がインバータのCPU USB通信 | 310 | 312 | 10-5_各通信経路のプロパティ_CPUUSBとMELSECNETH_ladder_reference.md |
| 項 | 接続局がロボットコントローラのCPU USB通信 | 311 | 313 | 10-5_各通信経路のプロパティ_CPUUSBとMELSECNETH_ladder_reference.md |
| 節 | 10.5 MELSECNET/H通信 | 312 | 314 | 10-5_各通信経路のプロパティ_CPUUSBとMELSECNETH_ladder_reference.md |
| 節 | 10.6 CC-Link IEコントローラネットワーク通信 | 315 | 317 | 10-6_各通信経路のプロパティ_CCLinkIE系からGOTゲートウェイ_ladder_reference.md |
| 項 | 接続局がRCPUのCC-Link IEコントローラネットワーク通信 | 315 | 317 | 10-6_各通信経路のプロパティ_CCLinkIE系からGOTゲートウェイ_ladder_reference.md |
| 項 | 接続局がQシリーズのCC-Link IEコントローラネットワーク通信 | 317 | 319 | 10-6_各通信経路のプロパティ_CCLinkIE系からGOTゲートウェイ_ladder_reference.md |
| 節 | 10.7 CC-Link IEフィールドネットワーク通信 | 320 | 322 | 10-6_各通信経路のプロパティ_CCLinkIE系からGOTゲートウェイ_ladder_reference.md |
| 項 | 接続局がRCPUのCC-Link IEフィールドネットワーク通信 | 320 | 322 | 10-6_各通信経路のプロパティ_CCLinkIE系からGOTゲートウェイ_ladder_reference.md |
| 項 | 接続局がQCPU(Qモード)またはLCPUのCC-Link IEフィールドネットワーク通信 | 322 | 324 | 10-6_各通信経路のプロパティ_CCLinkIE系からGOTゲートウェイ_ladder_reference.md |
| 節 | 10.8 CC-Link IE TSN通信 | 324 | 326 | 10-6_各通信経路のプロパティ_CCLinkIE系からGOTゲートウェイ_ladder_reference.md |
| 項 | 接続局がRCPUのCC-Link IE TSN通信 | 324 | 326 | 10-6_各通信経路のプロパティ_CCLinkIE系からGOTゲートウェイ_ladder_reference.md |
| 節 | 10.9 CC-Link通信 | 326 | 328 | 10-6_各通信経路のプロパティ_CCLinkIE系からGOTゲートウェイ_ladder_reference.md |
| 項 | 接続局がRCPUのCC-Link通信 | 326 | 328 | 10-6_各通信経路のプロパティ_CCLinkIE系からGOTゲートウェイ_ladder_reference.md |
| 項 | 接続局がLCPUのCC-Link通信 | 328 | 330 | 10-6_各通信経路のプロパティ_CCLinkIE系からGOTゲートウェイ_ladder_reference.md |
| 項 | 接続局がQシリーズのCC-Link通信 | 329 | 331 | 10-6_各通信経路のプロパティ_CCLinkIE系からGOTゲートウェイ_ladder_reference.md |
| 節 | 10.10 CC-Linkシステム RS-232インタフェース通信 | 332 | 334 | 10-6_各通信経路のプロパティ_CCLinkIE系からGOTゲートウェイ_ladder_reference.md |
| 節 | 10.11 GX Simulator2通信 | 335 | 337 | 10-6_各通信経路のプロパティ_CCLinkIE系からGOTゲートウェイ_ladder_reference.md |
| 節 | 10.12 GX Simulator3通信 | 335 | 337 | 10-6_各通信経路のプロパティ_CCLinkIE系からGOTゲートウェイ_ladder_reference.md |
| 節 | 10.13 MT Simulator2通信 | 336 | 338 | 10-6_各通信経路のプロパティ_CCLinkIE系からGOTゲートウェイ_ladder_reference.md |
| 節 | 10.14 MELSOFT Mirror通信 | 336 | 338 | 10-6_各通信経路のプロパティ_CCLinkIE系からGOTゲートウェイ_ladder_reference.md |
| 節 | 10.15 GOTゲートウェイデバイス通信 | 337 | 339 | 10-6_各通信経路のプロパティ_CCLinkIE系からGOTゲートウェイ_ladder_reference.md |
| 節 | 10.16 GOTトランスペアレント通信 | 338 | 340 | 10-7_各通信経路のプロパティ_GOTトランスペアレントUSB直結バスC24_ladder_reference.md |
| 項 | パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: 直結(1) | 338 | 340 | 10-7_各通信経路のプロパティ_GOTトランスペアレントUSB直結バスC24_ladder_reference.md |
| 項 | パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: 直結(2) | 340 | 342 | 10-7_各通信経路のプロパティ_GOTトランスペアレントUSB直結バスC24_ladder_reference.md |
| 項 | パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: 直結(3) | 342 | 344 | 10-7_各通信経路のプロパティ_GOTトランスペアレントUSB直結バスC24_ladder_reference.md |
| 項 | パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: 直結(4) | 345 | 347 | 10-7_各通信経路のプロパティ_GOTトランスペアレントUSB直結バスC24_ladder_reference.md |
| 項 | パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: バス | 347 | 349 | 10-7_各通信経路のプロパティ_GOTトランスペアレントUSB直結バスC24_ladder_reference.md |
| 項 | パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: シリアルコミュニケーションユニット(1) | 350 | 352 | 10-7_各通信経路のプロパティ_GOTトランスペアレントUSB直結バスC24_ladder_reference.md |
| 項 | パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: シリアルコミュニケーションユニット(2) | 353 | 355 | 10-7_各通信経路のプロパティ_GOTトランスペアレントUSB直結バスC24_ladder_reference.md |
| 項 | パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: シリアルコミュニケーションユニット(3) | 355 | 357 | 10-7_各通信経路のプロパティ_GOTトランスペアレントUSB直結バスC24_ladder_reference.md |
| 項 | パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: シリアルコミュニケーションユニット(4) | 357 | 359 | 10-7_各通信経路のプロパティ_GOTトランスペアレントUSB直結バスC24_ladder_reference.md |
| 項 | パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: シリアルコミュニケーションユニット(5) | 359 | 361 | 10-7_各通信経路のプロパティ_GOTトランスペアレントUSB直結バスC24_ladder_reference.md |
| 項 | パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: シリアルコミュニケーションユニット(6) | 361 | 363 | 10-7_各通信経路のプロパティ_GOTトランスペアレントUSB直結バスC24_ladder_reference.md |
| 項 | パソコン側ポート: シリアル，GOT2000側ポート: シリアル，CPU側ポート: MELSEC iQ-Rシリーズ対応E71 | 363 | 365 | 10-8_各通信経路のプロパティ_GOTトランスペアレントE71とEthernetポート_ladder_reference.md |
| 項 | パソコン側ポート: USB，GOT2000/3000側ポート: USB，CPU側ポート: MELSEC iQ-Rシリーズ対応E71 | 366 | 368 | 10-8_各通信経路のプロパティ_GOTトランスペアレントE71とEthernetポート_ladder_reference.md |
| 項 | パソコン側ポート: USB，GOT2000/3000側ポート: USB，CPU側ポート: Qシリーズ対応E71 | 369 | 371 | 10-8_各通信経路のプロパティ_GOTトランスペアレントE71とEthernetポート_ladder_reference.md |
| 項 | パソコン側ポート: USB，GOT2000/3000側ポート: USB，CPU側ポート: Lシリーズ対応E71 | 372 | 374 | 10-8_各通信経路のプロパティ_GOTトランスペアレントE71とEthernetポート_ladder_reference.md |
| 項 | パソコン側ポート: USB，GOT2000/3000側ポート: USB，CPU側ポート: Ethernetポート(1) | 375 | 377 | 10-8_各通信経路のプロパティ_GOTトランスペアレントE71とEthernetポート_ladder_reference.md |
| 項 | パソコン側ポート: USB，GOT2000/3000側ポート: USB，CPU側ポート: Ethernetポート(2) | 378 | 380 | 10-8_各通信経路のプロパティ_GOTトランスペアレントE71とEthernetポート_ladder_reference.md |
| 項 | パソコン側ポート: USB，GOT2000/3000側ポート: USB，CPU側ポート: Ethernetポート(3) | 380 | 382 | 10-8_各通信経路のプロパティ_GOTトランスペアレントE71とEthernetポート_ladder_reference.md |
| 項 | パソコン側ポート: USB，GOT2000/3000側ポート: USB，CPU側ポート: Ethernetポート(4) | 384 | 386 | 10-8_各通信経路のプロパティ_GOTトランスペアレントE71とEthernetポート_ladder_reference.md |
| 項 | パソコン側ポート: USB，GOT2000側ポート: USB，CPU側ポート: Ethernetアダプタユニット | 387 | 389 | 10-8_各通信経路のプロパティ_GOTトランスペアレントE71とEthernetポート_ladder_reference.md |
| 項 | パソコン側ポート: USB，GOT2000/3000側ポート: USB，CPU側ポート: Ethernetアダプタ/Ethernetユニット | 391 | 393 | 10-8_各通信経路のプロパティ_GOTトランスペアレントE71とEthernetポート_ladder_reference.md |
| 項 | パソコン側ポート: USB，GOT2000/3000側ポート: USB，CPU側ポート: Ethernetユニット | 393 | 395 | 10-8_各通信経路のプロパティ_GOTトランスペアレントE71とEthernetポート_ladder_reference.md |
| 項 | パソコン側ポート: Ethernetボード，GOT2000ポート: Ethernetポート，CPU側ポート: シリアル(1) | 395 | 397 | 10-9_各通信経路のプロパティ_GOTトランスペアレントEthernetボード経由_ladder_reference.md |
| 項 | パソコン側ポート: Ethernetボード，GOT2000ポート: Ethernetポート，CPU側ポート: シリアル(2) | 397 | 399 | 10-9_各通信経路のプロパティ_GOTトランスペアレントEthernetボード経由_ladder_reference.md |
| 項 | パソコン側ポート: Ethernetボード，GOT2000ポート: Ethernetポート，CPU側ポート: シリアル(3) | 399 | 401 | 10-9_各通信経路のプロパティ_GOTトランスペアレントEthernetボード経由_ladder_reference.md |
| 項 | パソコン側ポート: Ethernetボード，GOT2000ポート: Ethernetポート，CPU側ポート: シリアル(4) | 401 | 403 | 10-9_各通信経路のプロパティ_GOTトランスペアレントEthernetボード経由_ladder_reference.md |
| 項 | パソコン側ポート: Ethernetボード，GOT2000側ポート: Ethernetポート，CPU側ポート: シリアルコミュニケーションユニット(1) | 402 | 404 | 10-9_各通信経路のプロパティ_GOTトランスペアレントEthernetボード経由_ladder_reference.md |
| 項 | パソコン側ポート: Ethernetボード，GOT2000側ポート: Ethernetポート，CPU側ポート: シリアルコミュニケーションユニット(2) | 405 | 407 | 10-9_各通信経路のプロパティ_GOTトランスペアレントEthernetボード経由_ladder_reference.md |
| 項 | パソコン側ポート: Ethernetボード，GOT2000側ポート: Ethernetポート，CPU側ポート: シリアルコミュニケーションユニット(3) | 407 | 409 | 10-9_各通信経路のプロパティ_GOTトランスペアレントEthernetボード経由_ladder_reference.md |
| 項 | パソコン側ポート: Ethernetボード，GOT2000側ポート: Ethernetポート，CPU側ポート: バス | 409 | 411 | 10-9_各通信経路のプロパティ_GOTトランスペアレントEthernetボード経由_ladder_reference.md |
| 項 | パソコン側ポート: Ethernetボード，GOT2000/3000ポート: Ethernetポート，CPU側ポート: Ethernetポート | 412 | 414 | 10-9_各通信経路のプロパティ_GOTトランスペアレントEthernetボード経由_ladder_reference.md |
| 項 | パソコン側ポート: Ethernetボード，GOT2000/3000ポート: Ethernetポート，CPU側ポート: Qシリーズ対応E71 | 414 | 416 | 10-9_各通信経路のプロパティ_GOTトランスペアレントEthernetボード経由_ladder_reference.md |
| 章 | 第11章 関数 | 416 | 418 | 11-1_関数_注意事項と一覧とAct_OpenからGetDevice_ladder_reference.md |
| 節 | 11.1 プログラミング時の注意事項 | 416 | 418 | 11-1_関数_注意事項と一覧とAct_OpenからGetDevice_ladder_reference.md |
| 節 | 11.2 関数一覧 | 420 | 422 | 11-1_関数_注意事項と一覧とAct_OpenからGetDevice_ladder_reference.md |
| 節 | 11.3 関数の詳細(Actコントロール用) | 422 | 424 | 11-1_関数_注意事項と一覧とAct_OpenからGetDevice_ladder_reference.md |
| 項 | Open(通信回線のオープン) | 422 | 424 | 11-1_関数_注意事項と一覧とAct_OpenからGetDevice_ladder_reference.md |
| 項 | Close(通信回線のクローズ) | 424 | 426 | 11-1_関数_注意事項と一覧とAct_OpenからGetDevice_ladder_reference.md |
| 項 | ReadDeviceBlock(デバイスの一括読出し) | 425 | 427 | 11-1_関数_注意事項と一覧とAct_OpenからGetDevice_ladder_reference.md |
| 項 | WriteDeviceBlock(デバイスの一括書込み) | 428 | 430 | 11-1_関数_注意事項と一覧とAct_OpenからGetDevice_ladder_reference.md |
| 項 | ReadDeviceRandom(デバイスのランダム読出し) | 432 | 434 | 11-1_関数_注意事項と一覧とAct_OpenからGetDevice_ladder_reference.md |
| 項 | WriteDeviceRandom(デバイスのランダム書込み) | 436 | 438 | 11-1_関数_注意事項と一覧とAct_OpenからGetDevice_ladder_reference.md |
| 項 | SetDevice(デバイスデータの設定) | 439 | 441 | 11-1_関数_注意事項と一覧とAct_OpenからGetDevice_ladder_reference.md |
| 項 | GetDevice(デバイスデータの取得) | 441 | 443 | 11-1_関数_注意事項と一覧とAct_OpenからGetDevice_ladder_reference.md |
| 項 | ReadBuffer(バッファメモリ読出し) | 444 | 446 | 11-2_関数_Act_ReadBufferからSetCpuStatus_ladder_reference.md |
| 項 | WriteBuffer(バッファメモリ書込み) | 448 | 450 | 11-2_関数_Act_ReadBufferからSetCpuStatus_ladder_reference.md |
| 項 | GetClockData(時計データ読出し) | 452 | 454 | 11-2_関数_Act_ReadBufferからSetCpuStatus_ladder_reference.md |
| 項 | SetClockData(時計データ書込み) | 457 | 459 | 11-2_関数_Act_ReadBufferからSetCpuStatus_ladder_reference.md |
| 項 | GetCpuType(CPUユニット形名読出し) | 461 | 463 | 11-2_関数_Act_ReadBufferからSetCpuStatus_ladder_reference.md |
| 項 | SetCpuStatus(リモートコントロール) | 463 | 465 | 11-2_関数_Act_ReadBufferからSetCpuStatus_ladder_reference.md |
| 項 | EntryDeviceStatus(デバイスの状態監視登録) | 466 | 468 | 11-3_関数_Act_EntryDeviceStatusからGetErrorMessage_ladder_reference.md |
| 項 | FreeDeviceStatus(デバイスの状態監視登録解除) | 470 | 472 | 11-3_関数_Act_EntryDeviceStatusからGetErrorMessage_ladder_reference.md |
| 項 | OnDeviceStatus(イベント告知) | 471 | 473 | 11-3_関数_Act_EntryDeviceStatusからGetErrorMessage_ladder_reference.md |
| 項 | ReadDeviceBlock2(デバイスの一括読出し) | 474 | 476 | 11-3_関数_Act_EntryDeviceStatusからGetErrorMessage_ladder_reference.md |
| 項 | WriteDeviceBlock2(デバイスの一括書込み) | 477 | 479 | 11-3_関数_Act_EntryDeviceStatusからGetErrorMessage_ladder_reference.md |
| 項 | ReadDeviceRandom2(デバイスのランダム読出し) | 480 | 482 | 11-3_関数_Act_EntryDeviceStatusからGetErrorMessage_ladder_reference.md |
| 項 | WriteDeviceRandom2(デバイスのランダム書込み) | 483 | 485 | 11-3_関数_Act_EntryDeviceStatusからGetErrorMessage_ladder_reference.md |
| 項 | SetDevice2(デバイスデータの設定) | 486 | 488 | 11-3_関数_Act_EntryDeviceStatusからGetErrorMessage_ladder_reference.md |
| 項 | GetDevice2(デバイスデータの取得) | 489 | 491 | 11-3_関数_Act_EntryDeviceStatusからGetErrorMessage_ladder_reference.md |
| 項 | GetErrorMessage(エラー内容と処置方法の取得) | 492 | 494 | 11-3_関数_Act_EntryDeviceStatusからGetErrorMessage_ladder_reference.md |
| 節 | 11.4 関数の詳細(Actコントロール用(ロギングファイル転送)) | 494 | 496 | 11-4_関数_ロギング転送とNet_OpenからReadDeviceBlock_ladder_reference.md |
| 項 | Open(通信回線のオープン) | 494 | 496 | 11-4_関数_ロギング転送とNet_OpenからReadDeviceBlock_ladder_reference.md |
| 項 | Close(通信回線のクローズ) | 496 | 498 | 11-4_関数_ロギング転送とNet_OpenからReadDeviceBlock_ladder_reference.md |
| 項 | ReadFirstFile(ファイル名/ディレクトリ名の検索) | 497 | 499 | 11-4_関数_ロギング転送とNet_OpenからReadDeviceBlock_ladder_reference.md |
| 項 | ReadNextFile(ファイル名/ディレクトリ名の検索) | 499 | 501 | 11-4_関数_ロギング転送とNet_OpenからReadDeviceBlock_ladder_reference.md |
| 項 | ReadClose(検索の終了) | 501 | 503 | 11-4_関数_ロギング転送とNet_OpenからReadDeviceBlock_ladder_reference.md |
| 項 | GetFile(ロギングファイルの転送) | 502 | 504 | 11-4_関数_ロギング転送とNet_OpenからReadDeviceBlock_ladder_reference.md |
| 節 | 11.5 関数の詳細(.Netコントロール用) | 504 | 506 | 11-4_関数_ロギング転送とNet_OpenからReadDeviceBlock_ladder_reference.md |
| 項 | Open(通信回線のオープン) | 504 | 506 | 11-4_関数_ロギング転送とNet_OpenからReadDeviceBlock_ladder_reference.md |
| 項 | Close(通信回線のクローズ) | 505 | 507 | 11-4_関数_ロギング転送とNet_OpenからReadDeviceBlock_ladder_reference.md |
| 項 | ReadDeviceBlock(デバイスの一括読出し) | 506 | 508 | 11-4_関数_ロギング転送とNet_OpenからReadDeviceBlock_ladder_reference.md |
| 項 | WriteDeviceBlock(デバイスの一括書込み) | 512 | 514 | 11-5_関数_Net_WriteDeviceBlockからWriteDeviceRandom_ladder_reference.md |
| 項 | ReadDeviceRandom(デバイスのランダム読出し) | 518 | 520 | 11-5_関数_Net_WriteDeviceBlockからWriteDeviceRandom_ladder_reference.md |
| 項 | WriteDeviceRandom(デバイスのランダム書込み) | 529 | 531 | 11-5_関数_Net_WriteDeviceBlockからWriteDeviceRandom_ladder_reference.md |
| 項 | SetDevice(デバイスデータの設定) | 540 | 542 | 11-6_関数_Net_SetDeviceからOnDeviceStatus_ladder_reference.md |
| 項 | GetDevice(デバイスデータの取得) | 544 | 546 | 11-6_関数_Net_SetDeviceからOnDeviceStatus_ladder_reference.md |
| 項 | ReadBuffer(バッファメモリ読出し) | 548 | 550 | 11-6_関数_Net_SetDeviceからOnDeviceStatus_ladder_reference.md |
| 項 | WriteBuffer(バッファメモリ書込み) | 550 | 552 | 11-6_関数_Net_SetDeviceからOnDeviceStatus_ladder_reference.md |
| 項 | GetClockData(時計データ読出し) | 552 | 554 | 11-6_関数_Net_SetDeviceからOnDeviceStatus_ladder_reference.md |
| 項 | SetClockData(時計データ書込み) | 554 | 556 | 11-6_関数_Net_SetDeviceからOnDeviceStatus_ladder_reference.md |
| 項 | GetCpuType(CPUユニット形名読出し) | 556 | 558 | 11-6_関数_Net_SetDeviceからOnDeviceStatus_ladder_reference.md |
| 項 | SetCpuStatus(リモートコントロール) | 557 | 559 | 11-6_関数_Net_SetDeviceからOnDeviceStatus_ladder_reference.md |
| 項 | EntryDeviceStatus(デバイスの状態監視登録) | 559 | 561 | 11-6_関数_Net_SetDeviceからOnDeviceStatus_ladder_reference.md |
| 項 | FreeDeviceStatus(デバイスの状態監視登録解除) | 563 | 565 | 11-6_関数_Net_SetDeviceからOnDeviceStatus_ladder_reference.md |
| 項 | OnDeviceStatus(イベント告知) | 564 | 566 | 11-6_関数_Net_SetDeviceからOnDeviceStatus_ladder_reference.md |
| 項 | ReadDeviceBlock2(デバイスの一括読出し) | 566 | 568 | 11-7_関数_Net_ReadDeviceBlock2からReadDeviceRandom2_ladder_reference.md |
| 項 | WriteDeviceBlock2(デバイスの一括書込み) | 570 | 572 | 11-7_関数_Net_ReadDeviceBlock2からReadDeviceRandom2_ladder_reference.md |
| 項 | ReadDeviceRandom2(デバイスのランダム読出し) | 575 | 577 | 11-7_関数_Net_ReadDeviceBlock2からReadDeviceRandom2_ladder_reference.md |
| 項 | WriteDeviceRandom2(デバイスのランダム書込み) | 584 | 586 | 11-8_関数_Net_WriteDeviceRandom2からDispose_ladder_reference.md |
| 項 | SetDevice2(デバイスデータの設定) | 595 | 597 | 11-8_関数_Net_WriteDeviceRandom2からDispose_ladder_reference.md |
| 項 | GetDevice2(デバイスデータの取得) | 599 | 601 | 11-8_関数_Net_WriteDeviceRandom2からDispose_ladder_reference.md |
| 項 | Dispose(メモリの解放) | 602 | 604 | 11-8_関数_Net_WriteDeviceRandom2からDispose_ladder_reference.md |
| 章 | 第12章 サンプルプログラム | 603 | 605 | 12_サンプルプログラム_ladder_reference.md |
| 節 | 12.1 Visual Basic.NET，Visual C#，Visual C++ | 605 | 607 | 12_サンプルプログラム_ladder_reference.md |
| 項 | Act_2019.sln，Dot_2019.sln | 605 | 607 | 12_サンプルプログラム_ladder_reference.md |
| 項 | ActDatalogging_2019.sln | 608 | 610 | 12_サンプルプログラム_ladder_reference.md |
| 節 | 12.2 VBA | 609 | 611 | 12_サンプルプログラム_ladder_reference.md |
| 項 | Access用(ActTest_EarlyBind.accdb，ActTest_LateBind.accdb，ActTest64.accdb) | 609 | 611 | 12_サンプルプログラム_ladder_reference.md |
| 項 | Excel用(ActUtlType.xlsm，ActUtlType64.xlsm，ActProgType.xlsm，ActProgType64.xlsm) | 613 | 615 | 12_サンプルプログラム_ladder_reference.md |
| 章 | 第13章 エラーコード | 617 | 619 | 13-1_エラーコード一覧_前半_ladder_reference.md |
| 節 | 13.1 エラーコード一覧 | 617 | 619 | 13-1_エラーコード一覧_前半_ladder_reference.md |
| 節 | 13.2 CPU，ユニット，ネットワークボードが返すエラーコード | 644 | 646 | 13-3_エラーコード一覧_後半とCPUエラーとHRESULT_ladder_reference.md |
| 節 | 13.3 HRESULT型のエラーコード | 645 | 647 | 13-3_エラーコード一覧_後半とCPUエラーとHRESULT_ladder_reference.md |
| 節 | 13.4 イベントビューアに表示されるエラーコード | 645 | 647 | 13-3_エラーコード一覧_後半とCPUエラーとHRESULT_ladder_reference.md |
| 章 | 付録 | 646 | 648 | 付録-1_変更点とルーチングとマルチCPUと二重化CPU_ladder_reference.md |
| 節 | 付1 以前のバージョンからの変更点 | 646 | 648 | 付録-1_変更点とルーチングとマルチCPUと二重化CPU_ladder_reference.md |
| 節 | 付2 ルーチングパラメータの考え方 | 648 | 650 | 付録-1_変更点とルーチングとマルチCPUと二重化CPU_ladder_reference.md |
| 節 | 付3 マルチCPUシステムについて | 650 | 652 | 付録-1_変更点とルーチングとマルチCPUと二重化CPU_ladder_reference.md |
| 節 | 付4 Q00UJCPU，Q00UCPU，Q01UCPU使用時のネットワークユニットの装着可能台数について | 651 | 653 | 付録-1_変更点とルーチングとマルチCPUと二重化CPU_ladder_reference.md |
| 節 | 付5 二重化CPUへの対応について | 652 | 654 | 付録-1_変更点とルーチングとマルチCPUと二重化CPU_ladder_reference.md |
| 項 | RnPCPU(二重化モード)またはRnPSFCPUの場合 | 652 | 654 | 付録-1_変更点とルーチングとマルチCPUと二重化CPU_ladder_reference.md |
| 項 | QnPRHの場合 | 655 | 657 | 付録-1_変更点とルーチングとマルチCPUと二重化CPU_ladder_reference.md |
| 節 | 付6 ラベル名で使用できない文字列 | 663 | 665 | 付録-2_使用不可文字と性能とUSBドライバと状態監視例とタイムアウト_ladder_reference.md |
| 節 | 付7 性能 | 665 | 667 | 付録-2_使用不可文字と性能とUSBドライバと状態監視例とタイムアウト_ladder_reference.md |
| 項 | MX Component(コントロール)の性能 | 665 | 667 | 付録-2_使用不可文字と性能とUSBドライバと状態監視例とタイムアウト_ladder_reference.md |
| 項 | ラベル管理サービスの性能 | 666 | 668 | 付録-2_使用不可文字と性能とUSBドライバと状態監視例とタイムアウト_ladder_reference.md |
| 項 | ラベル管理ユーティリティの性能 | 667 | 669 | 付録-2_使用不可文字と性能とUSBドライバと状態監視例とタイムアウト_ladder_reference.md |
| 節 | 付8 USBドライバのインストール | 669 | 671 | 付録-2_使用不可文字と性能とUSBドライバと状態監視例とタイムアウト_ladder_reference.md |
| 節 | 付9 ワードデバイスを状態監視する場合のプログラミング例 | 670 | 672 | 付録-2_使用不可文字と性能とUSBドライバと状態監視例とタイムアウト_ladder_reference.md |
| 節 | 付10 タイムアウト時間について | 673 | 675 | 付録-2_使用不可文字と性能とUSBドライバと状態監視例とタイムアウト_ladder_reference.md |
| 項 | タイムアウトエラーでリトライする場合 | 673 | 675 | 付録-2_使用不可文字と性能とUSBドライバと状態監視例とタイムアウト_ladder_reference.md |
| 項 | 受信データエラーでリトライする場合 | 673 | 675 | 付録-2_使用不可文字と性能とUSBドライバと状態監視例とタイムアウト_ladder_reference.md |
| 項 | Actコントロール内部の固定時間でタイムアウトが発生する場合 | 673 | 675 | 付録-2_使用不可文字と性能とUSBドライバと状態監視例とタイムアウト_ladder_reference.md |
| 節 | 付11 トラブルシューティング | 674 | 676 | 付録-3_トラブルシューティングと互換性と索引と改訂履歴_ladder_reference.md |
| 項 | Visual C++でフォームに貼り付けて使用する際に，ヘッダファイルが正しく作成されない場合 | 676 | 678 | 付録-3_トラブルシューティングと互換性と索引と改訂履歴_ladder_reference.md |
| 項 | Visual Studio .NET を使用して，コントロールを使用するための設定でエラーが発生した場合 | 677 | 679 | 付録-3_トラブルシューティングと互換性と索引と改訂履歴_ladder_reference.md |
| 項 | Visual C++を使用して，ユーザプログラムを作成するときにリンクエラーが発生した場合 | 678 | 680 | 付録-3_トラブルシューティングと互換性と索引と改訂履歴_ladder_reference.md |
| 項 | GX Simulator3との通信時に未起動エラーが発生した場合 | 679 | 681 | 付録-3_トラブルシューティングと互換性と索引と改訂履歴_ladder_reference.md |
| 節 | 付12 従来品との相違点および互換性 | 680 | 682 | 付録-3_トラブルシューティングと互換性と索引と改訂履歴_ladder_reference.md |
| 項 | MX Component Version 4との比較 | 681 | 683 | 付録-3_トラブルシューティングと互換性と索引と改訂履歴_ladder_reference.md |
| 項 | コントロールの比較 | 684 | 686 | 付録-3_トラブルシューティングと互換性と索引と改訂履歴_ladder_reference.md |
| 項 | 置き換えについて | 687 | 689 | 付録-3_トラブルシューティングと互換性と索引と改訂履歴_ladder_reference.md |
| 章 | 関数索引 | 688 | 690 | 付録-3_トラブルシューティングと互換性と索引と改訂履歴_ladder_reference.md |
| 巻末 | 改訂履歴 | 690 | 692 | 付録-3_トラブルシューティングと互換性と索引と改訂履歴_ladder_reference.md |
| 巻末 | 保証について | 691 | 693 | 付録-3_トラブルシューティングと互換性と索引と改訂履歴_ladder_reference.md |
| 巻末 | サービスのお問い合わせ | 692 | 694 | 付録-3_トラブルシューティングと互換性と索引と改訂履歴_ladder_reference.md |
| 巻末 | 商標 | 692 | 694 | 付録-3_トラブルシューティングと互換性と索引と改訂履歴_ladder_reference.md |
| 巻末 | 著作権 | 692 | 694 | 付録-3_トラブルシューティングと互換性と索引と改訂履歴_ladder_reference.md |

※原本目次で2行に折り返している項目(Ethernetボード経由の「シリアルコミュニケーションユニット(1)〜(3)」，「Qシリーズ対応E71」)は1行に連結した。

---

## 関連マニュアル (関連マニュアル / 13 / 原本 p.15)

本製品に関連するマニュアルには，下記のものがあります。
最新のマニュアルは，三菱電機FAサイトからダウンロードできます。
https://www.MitsubishiElectric.co.jp/fa

| マニュアル名称[マニュアル番号] | 内容 |
|---|---|
| MX Component Version 5 リファレンスマニュアル<br>[SH-082394](本マニュアル) | MX Component Version 5の操作方法，プログラミング手順，およびエラーコードなどについて記載しています。 |

### ガイドライン (関連マニュアル / 13 / 原本 p.15)

| ガイドライン名称[ガイドライン番号] | 内容 |
|---|---|
| FAシステム セキュリティガイドライン<br>～三菱電機FA製品を安全・安心にご利用いただくために～<br>[XFB3-20PS001] | 当社のFA製品のセキュリティに対する取組みと，当社FA製品をお使いいただく上でお客様に取り組んでいただきたい推奨事項を記載しています。 |

---

## 用語 (用語 / 13 / 原本 p.15)

本マニュアルでは，特に明記する場合を除き，下記の用語を使用して説明します。

| 用語 | 内容 |
|---|---|
| A系 | 二重化システムにおいて，2つのシステムを判別するため，A系に設定したシステムです。<br>A系およびB系があり，接続した2つのシステムを判別するために使用します。 |
| B系 | 二重化システムにおいて，2つのシステムを判別するため，B系に設定したシステムです。<br>A系およびB系があり，接続した2つのシステムを判別するために使用します。 |
| Ethernetポート直結接続 | シーケンサとパソコンを，ハブを使用せずに直接接続することです。 |
| MELSOFT Navigator | MELSOFT iQ Worksの中の統合開発環境を示します。 |
| インテリジェント機能ユニット | A/D，D/A変換ユニットなど入出力以外の機能を持つユニットです。 |
| エンジニアリングツール | シーケンサの設定，プログラミング，デバッグ，保守までを行うためのツールです。 |
| シーケンスプログラム | 有接点シーケンスを，そのままシーケンサの言語に対応できるように考案されたプログラム方式です。縦2本の制御母線を描き，母線と母線の間に接点などを記述してプログラミングします。 |
| プロセスCPU | プロセス制御とシーケンス制御を行うCPUユニットです。プロセス制御FBやオンラインユニット交換などができます。<br>二重化機能ユニットと組み合わせて使用し，二重化システムを構成できます。 |
| マスタ局 | ネットワーク全体を制御する局です。すべての局とサイクリック伝送およびトランジェント伝送ができます。1ネットワークに1台のみ存在します。 |
| マルチCPUシステム | 複数台(2～4台)のCPUユニットで，それぞれが管理する入出力ユニットやインテリジェント機能ユニットを制御するシステムです。 |
| 安全CPU | 安全機能ユニットと組み合わせて使用し，一般制御と安全制御を行うCPUユニットです。 |
| 管理CPU | 各入出力ユニット，インテリジェント機能ユニットを制御するCPUユニットです。マルチCPUシステムでは，ユニットごとに管理CPUを設定します。 |
| 管理局 | ネットワークを管理する局で，1ネットワークに1台のみ存在します。管理局に，サイクリック伝送の各局送信範囲を割り付けます。 |
| 系切替え | 二重化システム構成時，制御系の故障または異常時にシステムの運転を継続させるために，制御系と待機系を切り替えます。 |
| 自系 | 二重化システム構成時に制御の対象となっているCPUユニットの系です。 |
| 制御系 | 二重化システム構成時に制御やネットワークの通信を行っているシステムです。 |
| 待機系 | 二重化システム構成時のバックアップ用のシステムです。 |
| 他局 | 接続局(自局)と接続しているネットワーク上の局を示します。 |
| 他系 | トラッキングケーブルで自系に接続されているもう一方のシステムです。A系が自系の場合はB系が，B系が自系の場合はA系が他系になります。 |
| 中継局 | 1台のシーケンサに複数のネットワークユニットを装着し，他ネットワークへのデータリンクを中継する局です。 |
| 二重化システム | CPUユニット，電源ユニット，ネットワークユニットなどの基本システムを二重化し，一方のシステムで異常が発生しても，もう一方のシステムで制御を継続できるシステムです。 |

---

## 総称/略称 (総称/略称 / 14 / 原本 p.16)

本マニュアルでは，特に明記する場合を除き，下記の総称/略称を使用して説明します。

| 総称/略称 | 内容 |
|---|---|
| Actコントロール | MX Componentが提供するActiveXコントロールを示します。 |
| CC-Link IE TSNボード | CC-Link IE TSNインタフェースボードを示します。 |
| CC-Link IEコントローラネットワークボード | CC-Link IEコントローラネットワークインタフェースボードを示します。 |
| CC-Link IEフィールドネットワークボード | CC-Link IEフィールドネットワークインタフェースボードを示します。 |
| CC-Link Ver.2ボード | CC-Linkシステムマスタ・ローカルインタフェースボードを示します。 |
| C言語コントローラ | R12CCPU-V，Q12DCCPU-V(基本機能モード)，Q12DCCPU-V(機能拡張モード)，Q24DHCCPU-V，Q24DHCCPU-LS，Q24DHCCPU-VG，Q26DHCCPU-LSを示します。 |
| Ethernetアダプタユニット | NZ2GF-ETB形CC-Link IEフィールドネットワークEthernetアダプタユニットを示します。 |
| Ethernetポート内蔵QCPU | Ethernetポートを有するQシリーズのCPUを示します。 |
| Ethernetユニット | MELSEC iQ-Rシリーズ対応E71，Qシリーズ対応E71，Lシリーズ対応E71を示します。 |
| Ethernet内蔵形CPU | Ethernetポートを有するCPUを示します。 |
| GOT | 三菱電機グラフィックオペレーションターミナルGOT2000シリーズ，GOT3000シリーズを示します。 |
| GT SoftGOT | GT SoftGOT3000 Version1，GT SoftGOT2000 Version1を示します。 |
| MELSECNET/Hボード | MELSECNET/Hインタフェースボードを示します。 |
| MX-Fモデル | MXF100を示します。 |
| MX-Rモデル | MXR300，MXR500を示します。 |
| MXF100 | MXF100-8-N32，MXF100-8-N32-EC，MXF100-8-P32，MXF100-16-N32，MXF100-16-N32-EC，MXF100-16-P32を示します。 |
| MXR300 | MXR300-16，MXR300-32，MXR300-64を示します。 |
| MXR500 | MXR500-128，MXR500-256を示します。 |
| MXコントローラ | MELSEC MXコントローラ MX-Rモデル，MX-Fモデルを示します。 |
| Q12DCCPU-V(機能拡張モード) | Q12DCCPU-Vを機能拡張モードで初期化した状態です。<br>Q12DCCPU-V(機能拡張モード)については，下記を参照してください。<br>📖MELSEC-Q C言語コントローラユニットユーザーズマニュアル |
| Q12DCCPU-V(基本機能モード) | Q12DCCPU-Vを基本機能モードで初期化した状態です。<br>Q12DCCPU-V(基本機能モード)については，下記を参照してください。<br>📖C言語コントローラユニットユーザーズマニュアル(ハードウェア設計・機能解説編) |
| QnPRH | Q12PRHCPU，Q25PRHCPUを示します。 |
| QnUDE(H)CPU/QnUD(P)VCPU | Q03UDECPU，Q03UDVCPU，Q04UDEHCPU，Q04UDVCPU，Q04UDPVCPU，Q06UDEHCPU，Q06UDVCPU，Q06UDPVCPU，Q10UDEHCPU，Q13UDEHCPU，Q13UDVCPU，Q13UDPVCPU，Q20UDEHCPU，Q26UDEHCPU，Q26UDVCPU，Q26UDPVCPU，Q50UDEHCPU，Q100UDEHCPUを示します。 |
| シリアルコミュニケーションユニット | MELSEC iQ-Rシリーズ対応C24，Qシリーズ対応C24，Lシリーズ対応C24，FX拡張ポートを示します。 |
| 二重化CPU | QnPRH，RnPCPU，RnPSFCPUを示します。 |
| 二重化増設ベースユニット | Q65WRB形CPU・電源二重化システム用増設ベースユニットを示します。 |
| ハイパフォーマンスモデルQCPU | Q02CPU，Q02HCPU，Q06HCPU，Q12HCPU，Q25HCPUを示します。 |
| ベーシックモデルQCPU | Q00JCPU，Q00CPU，Q01CPUを示します。 |
| ロボットコントローラ | CR750-Dシリーズ，CRnD-700シリーズを示します。 |

> 補足(本シリーズ): 「ハイパフォーマンスモデルQCPU」(Q02CPU 等)・「ベーシックモデルQCPU」は総称として定義されているが，2.4 の使用可能CPU一覧(02_)には含まれない。9章 ActCpuType のデフォルト値「34(CPU_Q02CPU)」が一覧に無い件(09_ 要確認)は，この旧機種名の名残と考えられる(推測。原本に記載なし)。

---

## 第1部 基本と開発の流れ (扉 / 15 / 原本 p.17)

基本と開発の流れを説明します。

1　MX Componentの基本
2　システム構成
3　ユーザプログラムの開発手順
4　ユーザプログラムへのコントロールの追加
5　通信設定
6　通信設定例(ユーティリティ使用時)
7　プログラミング
