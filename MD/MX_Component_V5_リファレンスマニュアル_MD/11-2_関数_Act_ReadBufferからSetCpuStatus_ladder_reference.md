# MX Component Version 5 リファレンスマニュアル 11章 関数 (2/8) p.446-467

| 項目 | 内容 |
|---|---|
| 原本 | 【三菱】MX Component Version 5 リファレンスマニュアル (SH-082394J) |
| メーカー | 三菱電機 |
| 原本ファイル | `PDF/【三菱】MX Component Version 5 リファレンスマニュアル_sh082394j.pdf` (全696ページ) |
| 本ファイルの範囲 | 11.3 関数の詳細(Actコントロール用) ReadBuffer / WriteBuffer / GetClockData / SetClockData / GetCpuType / SetCpuStatus (印刷ページ 444-465 / PDF p.446-467) |
| 出典表記 | `(節 / 印刷ページ / 原本 p.PDFページ)` |
| 作成日 | 2026-11-03 |

> このファイルは原本PDFの参照用リファレンスです。表・アドレス・ビット定義に加え、
> 機能説明・デバイスのON/OFFタイミング・注意事項・プログラム例は**原文のまま全文**転記しています。
> 未変換の範囲は「変換範囲表」を見てください。**命令の挙動で設計判断をするときは、
> 最終確認を原本の該当ページで行ってください。**
> 冒頭の対訳表の「参考訳」はメーカー公式訳ではありません。
> 本文中の「○ページ」はすべて原本の**印刷ページ番号**です(PDFページ = 印刷ページ + 2)。
> 書式の変数名(lRet / IRet / iRet 等)は原本表記のまま。VB.NETの「IRet」「ICpuType」「IOperation」は原本テキストでは大文字Iで抽出される(フォント上は小文字lと判別困難)。
> この範囲の関数ページにプログラム例は掲載されていない(サンプルプログラムは12章)。

## 主要用語 対訳表 (Glossary)

| 日本語 | English | 略号・項目番号 | 訳の出典 |
|---|---|---|---|
| バッファメモリ読出し / 書込み | Buffer memory read / write | ReadBuffer / WriteBuffer | 参考訳 |
| 時計データ読出し / 書込み | Clock data read / write | GetClockData / SetClockData | 参考訳 |
| CPUユニット形名読出し | CPU module model name read | GetCpuType | 参考訳 |
| リモートコントロール | Remote control | SetCpuStatus | 参考訳 |
| リモートRUN / STOP / PAUSE / RESET | Remote RUN / STOP / PAUSE / RESET | lOperation 0〜3 | 参考訳 |
| 使用可能コントロール | Available controls | ActProgType / ActUtlType (64) | 参考訳 |
| 書式 / 書式(オブジェクトを生成して使用する場合) | Format / Format (when creating an object) | — | 参考訳 |
| 戻り値 / COMの戻り値 / 通信関数の戻り値 | Return value / COM return value / Communication function return value | lRet / hResult / lplRetCode | 参考訳 |
| 先頭I/O番号 | Start I/O number | lStartIO (実I/O番号÷16) | 参考訳 |
| バッファメモリのアドレス | Buffer memory address | lAddress | 参考訳 |
| 読み出すサイズ / 書き込むサイズ | Read size / Write size | lReadSize / lWriteSize | 参考訳 |
| インテリジェント機能ユニット | Intelligent function module | — | 参考訳 |
| 特殊増設機器のブロックNo. | Special extension unit block No. | 0〜7 (FXCPU) | 参考訳 |
| 共有メモリ | Shared memory | QCPU(Qモード) | 参考訳 |
| Qシリーズ専用ユニット | Q series dedicated module | — | 参考訳 |
| 西暦4桁 / 西暦下2桁 | 4-digit year / Last 2 digits of year | 1980〜2079 (RCPU, QCPU) | 参考訳 |
| 曜日 | Day of week | iDayOfWeek 0(日)〜6(土) | 参考訳 |
| 時計機能内蔵の機種 | Model with built-in clock function | FXCPU | 参考訳 |
| 転送時間分の誤差 | Error by transfer time | — | 参考訳 |
| 形名文字列 / 形名コード | Model name string / Model code | szCpuName / lCpuType (16進) | 参考訳 |
| 通信経路の使用可否 | Availability by communication route | — | 参考訳 |
| 自ボードアクセス | Own board access | — | 参考訳 |
| アクセスパスワードが不一致 | Access password mismatch | 0x010A42A0 | 参考訳 |
| ユーザ認証機能 | User authentication function | MXコントローラ | 参考訳 |
| インバータ通信 / ロボットコントローラ通信 | Inverter communication / Robot controller communication | — | 参考訳 |
| GOTトランスペアレント機能通信 | GOT transparent function communication | — | 参考訳 |

## 変換範囲表

| 原本ページ(PDF) | 印刷ページ | 節 | 扱い |
|---|---|---|---|
| p.446-449 | 444-447 | ReadBuffer(バッファメモリ読出し) | 全文 |
| p.450-453 | 448-451 | WriteBuffer(バッファメモリ書込み) | 全文 |
| p.454-458 | 452-456 | GetClockData(時計データ読出し) | 全文 |
| p.459-462 | 457-460 | SetClockData(時計データ書込み) | 全文 |
| p.463-464 | 461-462 | GetCpuType(CPUユニット形名読出し) | 全文 |
| p.465-467 | 463-465 | SetCpuStatus(リモートコントロール) | 全文 |
| p.418-445，p.468-604 | 416-443，466-602 | 11章の他の範囲 | 別ファイル(11-1，11-3〜11-8) |
| p.1-417，p.605-696 | — | 他の章 | 別ファイル(01_〜10-9_)または**未変換** |

## 目次

- ReadBuffer(バッファメモリ読出し)
- WriteBuffer(バッファメモリ書込み)
- GetClockData(時計データ読出し)
- SetClockData(時計データ書込み)
- GetCpuType(CPUユニット形名読出し)
- SetCpuStatus(リモートコントロール)

---

## ReadBuffer(バッファメモリ読出し) (11.3 / 444-447 / 原本 p.446-449)

### 使用可能コントロール (11.3 / 444 / 原本 p.446)

下記のコントロールで使用可能です。
- 32ビット用: ActProgType，ActUtlType
- 64ビット用: ActProgType64，ActUtlType64

### 機能 (11.3 / 444 / 原本 p.446)

インテリジェント機能ユニットのバッファメモリの値を読み出します。

### 書式 (11.3 / 444 / 原本 p.446)

**■VBA**

```
lRet = object.ReadBuffer(lStartIO,lAddress,lReadSize, iData(0))
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| Long | lStartIO | 値を読み出すユニットの先頭I/O番号 | Input |
| Long | lAddress | バッファメモリのアドレス | Input |
| Long | lReadSize | 読み出すサイズ | Input |
| Integer | iData(n) | バッファメモリから読み出した値 | Output |

**■Visual C++**

```
lRet = object.ReadBuffer(lStartIO, lAddress, lReadSize, *lpsData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| Long | lStartIO | 値を読み出すユニットの先頭I/O番号 | Input |
| Long | lAddress | バッファメモリのアドレス | Input |
| Long | lReadSize | 読み出すサイズ | Input |
| Short | *lpsData | バッファメモリから読み出した値 | Output |

**■Visual Basic .NET**

```
IRet = object.ReadBuffer(iStartIO, iAddress, iReadSize, iData(0))
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| Integer | iStartIO | 値を読み出すユニットのI/O番号 | Input |
| Integer | iAddress | バッファメモリのアドレス | Input |
| Integer | iReadSize | 読み出すサイズ | Input |
| short | iData(n) | バッファメモリから読み出した値 | Output |

**■Visual C#**

```
iRet = object.ReadBuffer(iStartIO, iAddress, iReadSize, out sData[0])
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |
| int | iStartIO | 値を読み出すユニットのI/O番号 | Input |
| int | iAddress | バッファメモリのアドレス | Input |
| int | iReadSize | 読み出すサイズ | Input |
| short[n] | sData | バッファメモリから読み出した値 | Output |

### 書式(オブジェクトを生成して使用する場合) (11.3 / 445 / 原本 p.447)

**■Visual C++**

```
hResult = object.ReadBuffer(lStartIO, lAddress, lReadSize, *lpsData, *lplRetCode)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| HRESULT | hResult | COMの戻り値 | Output |
| LONG | lStartIO | 値を読み出すユニットの先頭I/O番号 | Input |
| LONG | lAddress | バッファメモリのアドレス | Input |
| LONG | lReadSize | 読み出すサイズ | Input |
| SHORT | *lpsData | バッファメモリから読み出した値 | Output |
| LONG | *lplRetCode | 通信関数の戻り値 | Output |

### 戻り値 (11.3 / 445 / 原本 p.447)

正常終了: 0を返します。  
異常終了: 0以外を返します。(☞617ページ エラーコード)  

### 説明 (11.3 / 445 / 原本 p.447)

- lStartIO(iStartIO)に指定するユニットのI/O番号は，実際のI/O番号を16で割った値を指定してください。
  FX5CPUの場合は，対象局側のユニット番号を指定してください。
- lStartIO(iStartIO)に指定した先頭I/O番号に位置するインテリジェント機能ユニットの，lAddress(iAddress)に指定されたバッファメモリアドレスのバッファ値をlReadSize(iReadSize)分読み出します。
- 接続局がFXCPUのCPU COM通信およびGX Simulator2通信を行う場合，ユニット先頭I/O番号には，特殊増設機器のブロックNo.(0～7)を，バッファメモリアドレスには0～32767を指定してください。
- iData(lpsDataまたはsData)は，lReadSize(iReadSize)以上の配列を確保してください。

> **Point**
> - RモーションCPUおよびQモーションCPUへアクセスを行うと，エラーが返ります。
> - iData(lpsDataまたはsData)は，lReadSize(iReadSize)に指定した点数分のメモリエリアを用意してください。
>   メモリエリアがない場合は，アプリケーションエラーなど重大な現象が発生するおそれがあります。
> - QCPU(Qモード)に対してバッファメモリ読出し(ReadBuffer)を行う場合，Qシリーズ専用ユニットにしか読出し操作を行うことができません。また，QCPU(Qモード)の共有メモリからの読出し操作も行うことができません。
> - インバータ通信/ロボットコントローラ通信時は使用できません。

#### 通信経路の使用可否 (11.3 / 446-447 / 原本 p.448-449)

通信経路の使用可否を下表に示します。
○: 使用可能，×: 使用不可

| 通信経路 | 通信経路(詳細) | ActUnitType | ActProtocolType | 使用可否 |
|---|---|---|---|---|
| シリアルコミュニケーション通信 | 接続ユニットがMELSEC iQ-Rシリーズ対応C24 | UNIT_RJ71C24 | PROTOCOL_SERIAL | ○ |
| シリアルコミュニケーション通信 | 接続ユニットがQシリーズ対応C24 | UNIT_QJ71C24 | PROTOCOL_SERIAL | ○ |
| シリアルコミュニケーション通信 | 接続ユニットがLシリーズ対応C24 | UNIT_LJ71C24 | PROTOCOL_SERIAL | ○ |
| シリアルコミュニケーション通信 | 接続ユニットがFX拡張ポート | UNIT_FX485BD | PROTOCOL_SERIAL | × |
| Ethernet通信 | — | UNIT_RJ71EN71 | PROTOCOL_TCPIP, PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_RJ71EN71_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_QJ71E71 | PROTOCOL_TCPIP, PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_LJ71E71 | PROTOCOL_TCPIP, PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_RETHER | PROTOCOL_TCPIP, PROTOCOL_UDPIP, PROTOCOL_TLS, PROTOCOL_DTLS | ○ |
| Ethernet通信 | — | UNIT_RETHER_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_FXVETHER | PROTOCOL_TCPIP | ○ |
| Ethernet通信 | — | UNIT_FXVETHER_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_MXF_ETHER | PROTOCOL_TCPIP, PROTOCOL_UDPIP, PROTOCOL_TLS, PROTOCOL_DTLS | ○ |
| Ethernet通信 | — | UNIT_MXF_ETHER_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_LNETHER | PROTOCOL_TCPIP | ○ |
| Ethernet通信 | — | UNIT_LNETHER, UNIT_LNETHER_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_QNETHER | PROTOCOL_TCPIP | ○ |
| Ethernet通信 | — | UNIT_QNETHER, UNIT_QNETHER_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_RJ71GN11 | PROTOCOL_TCPIP, PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_NZ2GF_ETB | PROTOCOL_TCPIP | ○ |
| Ethernet通信 | — | UNIT_NZ2GF_ETB, UNIT_NZ2GF_ETB_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_FXETHER | PROTOCOL_TCPIP | ○ |
| Ethernet通信 | — | UNIT_FXETHER_DIRECT | PROTOCOL_UDPIP | ○ |
| CPU COM通信 | 接続先CPUがFX5CPU | UNIT_FXVCPU | PROTOCOL_SERIAL | ○ |
| CPU COM通信 | 接続先CPUがQCPU(Qモード) | UNIT_QNCPU | PROTOCOL_SERIAL | ○ |
| CPU COM通信 | 接続先CPUがLCPU | UNIT_LNCPU | PROTOCOL_SERIAL | ○ |
| CPU COM通信 | 接続先CPUがQモーションCPU | UNIT_QNMOTION | PROTOCOL_SERIAL | × |
| CPU COM通信 | 接続先CPUがFXCPU | UNIT_FXCPU | PROTOCOL_SERIAL | ○*1 |
| USB通信 | 接続先CPUがRCPU | UNIT_RUSB | PROTOCOL_USB | ○ |
| USB通信 | 接続先CPUがLHCPU | UNIT_LHUSB | PROTOCOL_USB | ○ |
| USB通信 | 接続先CPUがFX5CPU | UNIT_FXVUSB | PROTOCOL_USB | ○ |
| USB通信 | 接続先CPUがQCPU(Qモード) | UNIT_QNUSB | PROTOCOL_USB | ○ |
| USB通信 | 接続先CPUがLCPU | UNIT_LNUSB | PROTOCOL_USB | ○ |
| USB通信 | 接続先CPUがQSCPU | UNIT_QSUSB | PROTOCOL_USB | ○ |
| USB通信 | 接続先CPUがQモーションCPU | UNIT_QNMOTIONUSB | PROTOCOL_USB | × |
| USB通信 | 接続先CPUがFXCPU | UNIT_FXCPU | PROTOCOL_USB | ○ |
| MELSECNET/H通信 | — | UNIT_MNETHBOARD | PROTOCOL_MNETH | ○*2 |
| CC-Link IEコントローラネットワーク通信 | — | UNIT_MNETGBOARD | PROTOCOL_MNETG | ○*2 |
| CC-Link IEフィールドネットワーク通信 | — | UNIT_CCIEFBOARD | PROTOCOL_CCIEF | ○*2 |
| CC-Link IE TSN通信 | — | UNIT_CCIETSNBOARD | PROTOCOL_CCIETSN | ○*2 |
| CC-Link通信 | — | UNIT_CCLINKBOARD | PROTOCOL_CCLINK | ○*2 |
| CC-Linkシステム RS-232インタフェース通信 | — | UNIT_G4QCPU | PROTOCOL_SERIAL | ○ |
| GX Simulator2通信 | — | UNIT_SIMULATOR2 | — | ○ |
| GX Simulator3通信(RCPU) | — | UNIT_SIMULATOR3 | — | × |
| GX Simulator3通信(FX5CPU) | — | UNIT_SIMULATOR3 | — | × |
| GX Simulator3通信(MX-Rモデル) | — | UNIT_SIMULATOR3 | — | × |
| GX Simulator3通信(MX-Fモデル) | — | UNIT_SIMULATOR3 | — | × |
| MT Simulator2通信 | — | UNIT_SIMULATOR2 | — | × |
| MELSOFT Mirror通信 | — | UNIT_RETHER_LCS | — | ○ |
| GOTゲートウェイデバイス通信 | — | UNIT_A900GOT | PROTOCOL_UDPIP | × |
| GOTトランスペアレント機能通信 | — | UNIT_RJ71C24, UNIT_FXVCPU, UNIT_QNCPU, UNIT_LNCPU | PROTOCOL_SERIAL, PROTOCOL_USBGOT | ○ |
| GOTトランスペアレント機能通信 | — | UNIT_FXCPU | PROTOCOL_SERIAL, PROTOCOL_USBGOT | ○*1 |
| GOTトランスペアレント機能通信 | — | UNIT_QJ71C24, UNIT_LJ71C24, UNIT_GOT_RJ71EN71, UNIT_GOT_QJ71E71, UNIT_GOT_LJ71E71, UNIT_GOT_RETHER, UNIT_GOT_QNETHER, UNIT_GOT_LNETHER, UNIT_A900GOT, UNIT_GOT_NZ2GF_ETB, UNIT_GOT_FXETHER, UNIT_GOT_FXENET | PROTOCOL_SERIAL, PROTOCOL_USBGOT | ○ |
| GOTトランスペアレント機能通信 | — | UNIT_GOTETHER_RJ71C24, UNIT_GOTETHER_FXVCPU, UNIT_GOTETHER_QNCPU, UNIT_GOTETHER_LNCPU | PROTOCOL_TCPIP | ○ |
| GOTトランスペアレント機能通信 | — | UNIT_GOTETHER_FXCPU | PROTOCOL_TCPIP | ○*1 |
| GOTトランスペアレント機能通信 | — | UNIT_GOTETHER_QBUS | PROTOCOL_TCPIP | ○ |
| GOTトランスペアレント機能通信 | — | UNIT_GOTETHER_QN_ETHER | PROTOCOL_TCPIP | ○ |
| インバータ通信 | — | — | COMM_RS232C, COMM_USB | × |

※原本では使用可否欄・ActProtocolType欄が複数行で結合されている箇所がある。本表では各行に同じ値を展開した。

> *1 FX3U，FX3UC，FX3G，FX3GC以外のCPUはエラーが返ります。
> *2 自ボードアクセス時はエラーが返ります。

---

## WriteBuffer(バッファメモリ書込み) (11.3 / 448-451 / 原本 p.450-453)

### 使用可能コントロール (11.3 / 448 / 原本 p.450)

下記のコントロールで使用可能です。
- 32ビット用: ActProgType，ActUtlType
- 64ビット用: ActProgType64，ActUtlType64

### 機能 (11.3 / 448 / 原本 p.450)

インテリジェント機能ユニットのバッファメモリの値を書き込みます。

### 書式 (11.3 / 448 / 原本 p.450)

**■VBA**

```
lRet = object.WriteBuffer(lStartIO, lAddress, lWriteSize, iData(0))
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| Long | lStartIO | 値を書き込むユニットの先頭I/O番号 | Input |
| Long | lAddress | バッファメモリのアドレス | Input |
| Long | lWriteSize | 書き込むサイズ | Input |
| Integer | iData(n) | バッファメモリに書き込む値 | Input |

**■Visual C++**

```
lRet = object.WriteBuffer(lStartIO, lAddress, lWriteSize, *lpsData)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| Long | lStartIO | 値を書き込むユニットの先頭I/O番号 | Input |
| Long | lAddress | バッファメモリのアドレス | Input |
| Long | lWriteSize | 書き込むサイズ | Input |
| Short | *lpsData | バッファメモリに書き込む値 | Input |

**■Visual Basic .NET**

```
IRet = object.WriteBuffer(iStartIO, iAddress, iWriteSize, iData(0))
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| Integer | iStartIO | 値を書き込むユニットのI/O番号 | Input |
| Integer | iAddress | バッファメモリのアドレス | Input |
| Integer | iWriteSize | 書き込むサイズ | Input |
| short | iData(n) | バッファメモリに書き込む値 | Input |

**■Visual C#**

```
iRet = object. WriteBuffer (iStartIO, iAddress, iWriteSize, ref sData[0])
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |
| int | iStartIO | 値を書き込むユニットのI/O番号 | Input |
| int | iAddress | バッファメモリのアドレス | Input |
| int | iWriteSize | 書き込むサイズ | Input |
| short[n] | sData | バッファメモリに書き込む値 | Input |

※Visual C#の書式の空白(`object. WriteBuffer (`)は原本表記のまま。

### 書式(オブジェクトを生成して使用する場合) (11.3 / 449 / 原本 p.451)

**■Visual C++**

```
hResult = object.WriteBuffer(lStartIO, lAddress, lWriteSize, *lpsData, *lplRetCode)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| HRESULT | hResult | COMの戻り値 | Output |
| LONG | lStartIO | 値を書き込むユニットの先頭I/O番号 | Input |
| LONG | lAddress | バッファメモリのアドレス | Input |
| LONG | lWriteSize | 書き込むサイズ | Input |
| SHORT | *lpsData | バッファメモリに書き込む値 | Input |
| LONG | *lplRetCode | 通信関数の戻り値 | Output |

### 戻り値 (11.3 / 449 / 原本 p.451)

正常終了: 0を返します。  
異常終了: 0以外を返します。(☞617ページ エラーコード)  

### 説明 (11.3 / 449 / 原本 p.451)

- lStartIO(iStartIO)に指定するユニットのI/O番号は，実際のI/O番号を16で割った値を指定してください。
  FX5CPUの場合は，対象局側のユニット番号を指定してください。
- lStartIO(iStartIO)に指定した先頭I/O番号に位置するインテリジェント機能ユニットの，lAddress(iAddress)に指定されたバッファメモリアドレスのバッファ値をlWriteSize(iWriteSize)分書き込みます。
- 接続局がFXCPUのCPU COM通信およびGX Simulator2通信を行う場合，ユニット先頭I/O番号には，特殊増設機器のブロックNo.(0～7)を，バッファメモリアドレスには0～32767を指定してください。
- iData(lpsDataまたはsData)は，lWriteSize(iWriteSize)以上の配列を確保してください。

> **Point**
> - RモーションCPUおよびQモーションCPUへアクセスを行うと，エラーが返ります。
> - iData(lpsData，varData，またはsData)は，lWriteSize(varWriteSizeまたはiWriteSize)に指定した点数分のメモリエリアを用意してください。
>   メモリエリアがない場合は，アプリケーションエラーなど重大な現象が発生するおそれがあります。
> - QCPU(Qモード)に対してバッファメモリ書込み(WriteBuffer)を行う場合，Qシリーズ専用ユニットにしか書込み操作を行うことができません。また，QCPU(Qモード)の共有メモリへの書込み操作も行うことができません。
> - インバータ通信/ロボットコントローラ通信時は使用できません。

※Pointの「varData」「varWriteSize」は原本表記のまま(この関数の書式には出てこない引数名。要確認)。

#### 通信経路の使用可否 (11.3 / 450-451 / 原本 p.452-453)

通信経路の使用可否を下表に示します。
○: 使用可能，×: 使用不可

| 通信経路 | 通信経路(詳細) | ActUnitType | ActProtocolType | 使用可否 |
|---|---|---|---|---|
| シリアルコミュニケーション通信 | 接続ユニットがMELSEC iQ-Rシリーズ対応C24 | UNIT_RJ71C24 | PROTOCOL_SERIAL | ○ |
| シリアルコミュニケーション通信 | 接続ユニットがQシリーズ対応C24 | UNIT_QJ71C24 | PROTOCOL_SERIAL | ○ |
| シリアルコミュニケーション通信 | 接続ユニットがLシリーズ対応C24 | UNIT_LJ71C24 | PROTOCOL_SERIAL | ○ |
| シリアルコミュニケーション通信 | 接続ユニットがFX拡張ポート | UNIT_FX485BD | PROTOCOL_SERIAL | × |
| Ethernet通信 | — | UNIT_RJ71EN71 | PROTOCOL_TCPIP, PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_RJ71EN71_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_QJ71E71 | PROTOCOL_TCPIP, PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_LJ71E71 | PROTOCOL_TCPIP, PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_RETHER | PROTOCOL_TCPIP, PROTOCOL_UDPIP, PROTOCOL_TLS, PROTOCOL_DTLS | ○ |
| Ethernet通信 | — | UNIT_RETHER_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_FXVETHER | PROTOCOL_TCPIP | ○ |
| Ethernet通信 | — | UNIT_FXVETHER_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_MXF_ETHER | PROTOCOL_TCPIP, PROTOCOL_UDPIP, PROTOCOL_TLS, PROTOCOL_DTLS | ○ |
| Ethernet通信 | — | UNIT_MXF_ETHER_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_LNETHER | PROTOCOL_TCPIP | ○ |
| Ethernet通信 | — | UNIT_LNETHER, UNIT_LNETHER_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_QNETHER | PROTOCOL_TCPIP | ○ |
| Ethernet通信 | — | UNIT_QNETHER, UNIT_QNETHER_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_RJ71GN11 | PROTOCOL_TCPIP, PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_NZ2GF_ETB | PROTOCOL_TCPIP | ○ |
| Ethernet通信 | — | UNIT_NZ2GF_ETB, UNIT_NZ2GF_ETB_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_FXETHER | PROTOCOL_TCPIP | ○ |
| Ethernet通信 | — | UNIT_FXETHER_DIRECT | PROTOCOL_UDPIP | ○ |
| CPU COM通信 | 接続先CPUがFX5CPU | UNIT_FXVCPU | PROTOCOL_SERIAL | ○ |
| CPU COM通信 | 接続先CPUがQCPU(Qモード) | UNIT_QNCPU | PROTOCOL_SERIAL | ○ |
| CPU COM通信 | 接続先CPUがLCPU | UNIT_LNCPU | PROTOCOL_SERIAL | ○ |
| CPU COM通信 | 接続先CPUがQモーションCPU | UNIT_QNMOTION | PROTOCOL_SERIAL | × |
| CPU COM通信 | 接続先CPUがFXCPU | UNIT_FXCPU | PROTOCOL_SERIAL | ○*1 |
| USB通信 | 接続先CPUがRCPU | UNIT_RUSB | PROTOCOL_USB | ○ |
| USB通信 | 接続先CPUがLHCPU | UNIT_LHUSB | PROTOCOL_USB | ○ |
| USB通信 | 接続先CPUがFX5CPU | UNIT_FXVUSB | PROTOCOL_USB | ○ |
| USB通信 | 接続先CPUがQCPU(Qモード) | UNIT_QNUSB | PROTOCOL_USB | ○ |
| USB通信 | 接続先CPUがLCPU | UNIT_LNUSB | PROTOCOL_USB | ○ |
| USB通信 | 接続先CPUがQSCPU | UNIT_QSUSB | PROTOCOL_USB | ×*2 |
| USB通信 | 接続先CPUがQモーションCPU | UNIT_QNMOTIONUSB | PROTOCOL_USB | × |
| USB通信 | 接続先CPUがFXCPU | UNIT_FXCPU | PROTOCOL_USB | ○ |
| MELSECNET/H通信 | — | UNIT_MNETHBOARD | PROTOCOL_MNETH | ○*3 |
| CC-Link IEコントローラネットワーク通信 | — | UNIT_MNETGBOARD | PROTOCOL_MNETG | ○*3 |
| CC-Link IEフィールドネットワーク通信 | — | UNIT_CCIEFBOARD | PROTOCOL_CCIEF | ○*3 |
| CC-Link IE TSN通信 | — | UNIT_CCIETSNBOARD | PROTOCOL_CCIETSN | ○*3 |
| CC-Link通信 | — | UNIT_CCLINKBOARD | PROTOCOL_CCLINK | ○*3 |
| CC-Linkシステム RS-232インタフェース通信 | — | UNIT_G4QCPU | PROTOCOL_SERIAL | ○ |
| GX Simulator2通信 | — | UNIT_SIMULATOR2 | — | ○ |
| GX Simulator3通信(RCPU) | — | UNIT_SIMULATOR3 | — | × |
| GX Simulator3通信(FX5CPU) | — | UNIT_SIMULATOR3 | — | × |
| GX Simulator3通信(MX-Rモデル) | — | UNIT_SIMULATOR3 | — | × |
| GX Simulator3通信(MX-Fモデル) | — | UNIT_SIMULATOR3 | — | × |
| MT Simulator2通信 | — | UNIT_SIMULATOR2 | — | × |
| MELSOFT Mirror通信 | — | UNIT_RETHER_LCS | — | ○ |
| GOTゲートウェイデバイス通信 | — | UNIT_A900GOT | PROTOCOL_UDPIP | × |
| GOTトランスペアレント機能通信 | — | UNIT_RJ71C24, UNIT_FXVCPU, UNIT_QNCPU, UNIT_LNCPU | PROTOCOL_SERIAL, PROTOCOL_USBGOT | ○ |
| GOTトランスペアレント機能通信 | — | UNIT_FXCPU | PROTOCOL_SERIAL, PROTOCOL_USBGOT | ○*1 |
| GOTトランスペアレント機能通信 | — | UNIT_QJ71C24, UNIT_LJ71C24, UNIT_GOT_RJ71EN71, UNIT_GOT_QJ71E71, UNIT_GOT_LJ71E71, UNIT_GOT_RETHER, UNIT_GOT_QNETHER, UNIT_GOT_LNETHER, UNIT_A900GOT, UNIT_GOT_NZ2GF_ETB, UNIT_GOT_FXETHER, UNIT_GOT_FXENET | PROTOCOL_SERIAL, PROTOCOL_USBGOT | ○ |
| GOTトランスペアレント機能通信 | — | UNIT_GOTETHER_RJ71C24, UNIT_GOTETHER_FXVCPU, UNIT_GOTETHER_QNCPU, UNIT_GOTETHER_LNCPU | PROTOCOL_TCPIP | ○ |
| GOTトランスペアレント機能通信 | — | UNIT_GOTETHER_FXCPU | PROTOCOL_TCPIP | ○*1 |
| GOTトランスペアレント機能通信 | — | UNIT_GOTETHER_QBUS | PROTOCOL_TCPIP | ○ |
| GOTトランスペアレント機能通信 | — | UNIT_GOTETHER_QN_ETHER | PROTOCOL_TCPIP | ○ |
| インバータ通信 | — | — | COMM_RS232C, COMM_USB | × |

※原本では使用可否欄・ActProtocolType欄が複数行で結合されている箇所がある。本表では各行に同じ値を展開した。

> *1 FX3U，FX3UC，FX3G，FX3GC以外のCPUはエラーが返ります。
> *2 QSCPUにアクセス時は，エラー 0x010A42A0(アクセスパスワードが不一致)となります。
> *3 自ボードアクセス時はエラーが返ります。

---

## GetClockData(時計データ読出し) (11.3 / 452-456 / 原本 p.454-458)

### 使用可能コントロール (11.3 / 452 / 原本 p.454)

下記のコントロールで使用可能です。
- 32ビット用: ActProgType，ActUtlType
- 64ビット用: ActProgType64，ActUtlType64

### 機能 (11.3 / 452 / 原本 p.454)

CPUユニットの時計データから時間を読み出します。

### 書式 (11.3 / 452-453 / 原本 p.454-455)

**■VBA**

```
lRet = object.GetClockData(iYear, iMonth, iDay, iDayOfWeek, iHour, iMinute, iSecond)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| Integer | iYear | 読み出した年の値 | Output |
| Integer | iMonth | 読み出した月の値 | Output |
| Integer | iDay | 読み出した日の値 | Output |
| Integer | iDayOfWeek | 読み出した曜日の値 | Output |
| Integer | iHour | 読み出した時間の値 | Output |
| Integer | iMinute | 読み出した分の値 | Output |
| Integer | iSecond | 読み出した秒の値 | Output |

**■Visual C++**

```
lRet = object.GetClockData(*lpsYear, *lpsMonth, *lpsDay, *lpsDayOfWeek, *lpsHour, *lpsMinute,
 *lpsSecond)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| Short | *lpsYear | 読み出した年の値 | Output |
| Short | *lpsMonth | 読み出した月の値 | Output |
| Short | *lpsDay | 読み出した日の値 | Output |
| Short | *lpsDayOfWeek | 読み出した曜日の値 | Output |
| Short | *lpsHour | 読み出した時間の値 | Output |
| Short | *lpsMinute | 読み出した分の値 | Output |
| Short | *lpsSecond | 読み出した秒の値 | Output |

**■Visual Basic .NET**

```
IRet = object.GetClockData(iYear, iMonth, iDay, iDayOfWeek,iHour, iMinute,iSecond)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| short | iYear | 読み出した年の値 | Output |
| short | iMonth | 読み出した月の値 | Output |
| short | iDay | 読み出した日の値 | Output |
| short | iDayOfWeek | 読み出した曜日の値 | Output |
| short | iHour | 読み出した時間の値 | Output |
| short | iMinute | 読み出した分の値 | Output |
| short | iSecond | 読み出した秒の値 | Output |

**■Visual C#**

```
hResult = object.GetClockData(out sYear, out sMonth, out sDay, out sDayOfWeek,out sHour, out sMinute, out sSecond)
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

※Visual C#の書式の左辺が「hResult」なのに引数表の戻り値は「iRet」(原本表記のまま。要確認)。

### 書式(オブジェクトを生成して使用する場合) (11.3 / 453 / 原本 p.455)

**■Visual C++**

```
hResult = object.GetClockData(*lpsYear, *lpsMonth, *lpsDay, *lpsDayOfWeek, *lpsHour,
 *lpsMinute, *lpsSecond, *lplRetCode)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| HRESULT | hResult | COMの戻り値 | Output |
| SHORT | *lpsYear | 読み出した年の値 | Output |
| SHORT | *lpsMonth | 読み出した月の値 | Output |
| SHORT | *lpsDay | 読み出した日の値 | Output |
| SHORT | *lpsDayOfWeek | 読み出した曜日の値 | Output |
| SHORT | *lpsHour | 読み出した時間の値 | Output |
| SHORT | *lpsMinute | 読み出した分の値 | Output |
| SHORT | *lpsSecond | 読み出した秒の値 | Output |
| LONG | *lplRetCode | 通信関数の戻り値 | Output |

### 戻り値 (11.3 / 453 / 原本 p.455)

正常終了: 0を返します。  
異常終了: 0以外を返します。(☞617ページ エラーコード)  

### 説明 (11.3 / 453-454 / 原本 p.455-456)

- CPUユニットに正しい時計データが設定されていない場合，エラーが返ります。
- iYear(lpsYearまたはsYear)に格納される値は，RCPUおよびQCPU(Qモード)は西暦4桁，それ以外のCPUは西暦下2桁が返ります。
  ただし，RCPUおよびQCPU(Qモード)は1980年から2079年までとなります。
- iDayOfWeek(lpsDayOfWeekまたはsDayOfWeek)に格納される値は，下記のとおりです。

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
> - インバータ通信/ロボットコントローラ通信時は使用できません。

#### 通信経路の使用可否 (11.3 / 455-456 / 原本 p.457-458)

通信経路の使用可否を下表に示します。
○: 使用可能，×: 使用不可

| 通信経路 | 通信経路(詳細) | ActUnitType | ActProtocolType | 使用可否 |
|---|---|---|---|---|
| シリアルコミュニケーション通信 | 接続ユニットがMELSEC iQ-Rシリーズ対応C24 | UNIT_RJ71C24 | PROTOCOL_SERIAL | ○ |
| シリアルコミュニケーション通信 | 接続ユニットがQシリーズ対応C24 | UNIT_QJ71C24 | PROTOCOL_SERIAL | ○ |
| シリアルコミュニケーション通信 | 接続ユニットがLシリーズ対応C24 | UNIT_LJ71C24 | PROTOCOL_SERIAL | ○ |
| シリアルコミュニケーション通信 | 接続ユニットがFX拡張ポート | UNIT_FX485BD | PROTOCOL_SERIAL | ○ |
| Ethernet通信 | — | UNIT_RJ71EN71 | PROTOCOL_TCPIP, PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_RJ71EN71_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_QJ71E71 | PROTOCOL_TCPIP, PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_LJ71E71 | PROTOCOL_TCPIP, PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_RETHER | PROTOCOL_TCPIP, PROTOCOL_UDPIP, PROTOCOL_TLS, PROTOCOL_DTLS | ○ |
| Ethernet通信 | — | UNIT_RETHER_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_FXVETHER | PROTOCOL_TCPIP | ○ |
| Ethernet通信 | — | UNIT_FXVETHER_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_MXF_ETHER | PROTOCOL_TCPIP, PROTOCOL_UDPIP, PROTOCOL_TLS, PROTOCOL_DTLS | ○ |
| Ethernet通信 | — | UNIT_MXF_ETHER_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_LNETHER | PROTOCOL_TCPIP | ○ |
| Ethernet通信 | — | UNIT_LNETHER, UNIT_LNETHER_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_QNETHER | PROTOCOL_TCPIP | ○ |
| Ethernet通信 | — | UNIT_QNETHER, UNIT_QNETHER_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_RJ71GN11 | PROTOCOL_TCPIP, PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_NZ2GF_ETB | PROTOCOL_TCPIP | ○ |
| Ethernet通信 | — | UNIT_NZ2GF_ETB, UNIT_NZ2GF_ETB_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_FXETHER | PROTOCOL_TCPIP | ○ |
| Ethernet通信 | — | UNIT_FXETHER_DIRECT | PROTOCOL_UDPIP | ○ |
| CPU COM通信 | 接続先CPUがFX5CPU | UNIT_FXVCPU | PROTOCOL_SERIAL | ○ |
| CPU COM通信 | 接続先CPUがQCPU(Qモード) | UNIT_QNCPU | PROTOCOL_SERIAL | ○ |
| CPU COM通信 | 接続先CPUがLCPU | UNIT_LNCPU | PROTOCOL_SERIAL | ○ |
| CPU COM通信 | 接続先CPUがQモーションCPU | UNIT_QNMOTION | PROTOCOL_SERIAL | × |
| CPU COM通信 | 接続先CPUがFXCPU | UNIT_FXCPU | PROTOCOL_SERIAL | ○ |
| USB通信 | 接続先CPUがRCPU | UNIT_RUSB | PROTOCOL_USB | ○ |
| USB通信 | 接続先CPUがLHCPU | UNIT_LHUSB | PROTOCOL_USB | ○ |
| USB通信 | 接続先CPUがFX5CPU | UNIT_FXVUSB | PROTOCOL_USB | ○ |
| USB通信 | 接続先CPUがQCPU(Qモード) | UNIT_QNUSB | PROTOCOL_USB | ○ |
| USB通信 | 接続先CPUがLCPU | UNIT_LNUSB | PROTOCOL_USB | ○ |
| USB通信 | 接続先CPUがQSCPU | UNIT_QSUSB | PROTOCOL_USB | ○ |
| USB通信 | 接続先CPUがQモーションCPU | UNIT_QNMOTIONUSB | PROTOCOL_USB | × |
| USB通信 | 接続先CPUがFXCPU | UNIT_FXCPU | PROTOCOL_USB | ○ |
| MELSECNET/H通信 | — | UNIT_MNETHBOARD | PROTOCOL_MNETH | ○*1 |
| CC-Link IEコントローラネットワーク通信 | — | UNIT_MNETGBOARD | PROTOCOL_MNETG | ○*1 |
| CC-Link IEフィールドネットワーク通信 | — | UNIT_CCIEFBOARD | PROTOCOL_CCIEF | ○*1 |
| CC-Link IE TSN通信 | — | UNIT_CCIETSNBOARD | PROTOCOL_CCIETSN | ○*1 |
| CC-Link通信 | — | UNIT_CCLINKBOARD | PROTOCOL_CCLINK | ○*1 |
| CC-Linkシステム RS-232インタフェース通信 | — | UNIT_G4QCPU | PROTOCOL_SERIAL | ○ |
| GX Simulator2通信 | — | UNIT_SIMULATOR2 | — | ○ |
| GX Simulator3通信(RCPU) | — | UNIT_SIMULATOR3 | — | ○ |
| GX Simulator3通信(FX5CPU) | — | UNIT_SIMULATOR3 | — | ○ |
| GX Simulator3通信(MX-Rモデル) | — | UNIT_SIMULATOR3 | — | ○ |
| GX Simulator3通信(MX-Fモデル) | — | UNIT_SIMULATOR3 | — | ○ |
| MT Simulator2通信 | — | UNIT_SIMULATOR2 | — | × |
| MELSOFT Mirror通信 | — | UNIT_RETHER_LCS | — | ○ |
| GOTゲートウェイデバイス通信 | — | UNIT_A900GOT | PROTOCOL_UDPIP | × |
| GOTトランスペアレント機能通信 | — | UNIT_RJ71C24, UNIT_FXVCPU, UNIT_QNCPU, UNIT_LNCPU, UNIT_FXCPU, UNIT_QJ71C24, UNIT_LJ71C24, UNIT_GOT_RJ71EN71, UNIT_GOT_QJ71E71, UNIT_GOT_LJ71E71, UNIT_GOT_RETHER, UNIT_GOT_QNETHER, UNIT_GOT_LNETHER, UNIT_A900GOT, UNIT_GOT_NZ2GF_ETB, UNIT_GOT_FXETHER, UNIT_GOT_FXENET | PROTOCOL_SERIAL, PROTOCOL_USBGOT | ○ |
| GOTトランスペアレント機能通信 | — | UNIT_GOTETHER_RJ71C24, UNIT_GOTETHER_FXVCPU, UNIT_GOTETHER_QNCPU, UNIT_GOTETHER_LNCPU, UNIT_GOTETHER_FXCPU, UNIT_GOTETHER_QBUS, UNIT_GOTETHER_QN_ETHER | PROTOCOL_TCPIP | ○ |
| インバータ通信 | — | — | COMM_RS232C, COMM_USB | × |

※原本では使用可否欄・ActProtocolType欄が複数行で結合されている箇所がある。本表では各行に同じ値を展開した。
※GX Simulator2通信とGX Simulator3通信(4行)の使用可否は原本では1セル(○)で結合。

> *1 自ボードアクセス時はエラーが返ります。

---

## SetClockData(時計データ書込み) (11.3 / 457-460 / 原本 p.459-462)

### 使用可能コントロール (11.3 / 457 / 原本 p.459)

下記のコントロールで使用可能です。
- 32ビット用: ActProgType，ActUtlType
- 64ビット用: ActProgType64，ActUtlType64

### 機能 (11.3 / 457 / 原本 p.459)

CPUユニットの時計データへ時間を書き込みます。

### 書式 (11.3 / 457-458 / 原本 p.459-460)

**■VBA**

```
object.SetClockData(iYear, iMonth, iDay, iDayOfWeek, iHour, iMinute, iSecond)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| Integer | iYear | 書き込む年の値 | Input |
| Integer | iMonth | 書き込む月の値 | Input |
| Integer | iDay | 書き込む日の値 | Input |
| Integer | iDayOfWeek | 書き込む曜日の値 | Input |
| Integer | iHour | 書き込む時間の値 | Input |
| Integer | iMinute | 書き込む分の値 | Input |
| Integer | iSecond | 書き込む秒の値 | Input |

※VBAの書式に「lRet =」が無いが引数表には lRet がある(原本表記のまま)。

**■Visual C++**

```
lRet = object.SetClockData(sYear, sMonth, sDay, sDayOfWeek, sHour, sMinute, sSecond)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| Short | sYear | 書き込む年の値 | Input |
| Short | sMonth | 書き込む月の値 | Input |
| Short | sDay | 書き込む日の値 | Input |
| Short | sDayOfWeek | 書き込む曜日の値 | Input |
| Short | sHour | 書き込む時間の値 | Input |
| Short | sMinute | 書き込む分の値 | Input |
| Short | sSecond | 書き込む秒の値 | Input |

**■Visual Basic .NET**

```
IRet = object.SetClockData(iYear, iMonth, iDay, iDayOfWeek, iHour, iMinute,iSecond)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| short | iYear | 書き込む年の値 | Input |
| short | iMonth | 書き込む月の値 | Input |
| short | iDay | 書き込む日の値 | Input |
| short | iDayOfWeek | 書き込む曜日の値 | Input |
| short | iHour | 書き込む時間の値 | Input |
| short | iMinute | 書き込む分の値 | Input |
| short | iSecond | 書き込む秒の値 | Input |

**■Visual C#**

```
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

※Visual C#の書式の左辺が「lRet」なのに引数表の戻り値は「iRet」(原本表記のまま。要確認)。原本では引数表がp.459とp.460にまたがる。

### 書式(オブジェクトを生成して使用する場合) (11.3 / 458 / 原本 p.460)

**■Visual C++**

```
hResult = object.SetClockData(sYear,sMonth, sDay, sDayOfWeek, sHour, sMinute, sSecond,
 *lplRetCode)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| HRESULT | hResult | COMの戻り値 | Output |
| SHORT | sYear | 書き込む年の値 | Input |
| SHORT | sMonth | 書き込む月の値 | Input |
| SHORT | sDay | 書き込む日の値 | Input |
| SHORT | sDayOfWeek | 書き込む曜日の値 | Input |
| SHORT | sHour | 書き込む時間の値 | Input |
| SHORT | sMinute | 書き込む分の値 | Input |
| SHORT | sSecond | 書き込む秒の値 | Input |
| LONG | *lplRetCode | 通信関数の戻り値 | Output |

### 戻り値 (11.3 / 458 / 原本 p.460)

正常終了: 0を返します。  
異常終了: 0以外を返します。(☞617ページ エラーコード)  

### 説明 (11.3 / 458 / 原本 p.460)

- 設定する時計データが正しい値でない場合，エラーが返ります。
- iYear(sYear)に指定した値は，RCPUおよびQCPU(Qモード)は西暦4桁，それ以外のCPUは西暦下2桁が有効となります。
  ただし，RCPUおよびQCPU(Qモード)は1980年から2079までとなります。
  RCPUおよびQCPU(Qモード)以外のCPUで4桁を設定した場合はエラーとなります。
- iDayOfWeek(sDayOfWeek)に指定する値は，下記のとおりです。

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
>   上記以外のFXCPU はエラーが返ります。
> - 時計設定は転送時間分の誤差が生じますのでご注意ください。
> - インバータ通信/ロボットコントローラ通信時は使用できません。
> - ユーザ認証機能が有効なMXコントローラでは使用できません。

#### 通信経路の使用可否 (11.3 / 459-460 / 原本 p.461-462)

通信経路の使用可否を下表に示します。
○: 使用可能，×: 使用不可

| 通信経路 | 通信経路(詳細) | ActUnitType | ActProtocolType | 使用可否 |
|---|---|---|---|---|
| シリアルコミュニケーション通信 | 接続ユニットがMELSEC iQ-Rシリーズ対応C24 | UNIT_RJ71C24 | PROTOCOL_SERIAL | ○ |
| シリアルコミュニケーション通信 | 接続ユニットがQシリーズ対応C24 | UNIT_QJ71C24 | PROTOCOL_SERIAL | ○ |
| シリアルコミュニケーション通信 | 接続ユニットがLシリーズ対応C24 | UNIT_LJ71C24 | PROTOCOL_SERIAL | ○ |
| シリアルコミュニケーション通信 | 接続ユニットがFX拡張ポート | UNIT_FX485BD | PROTOCOL_SERIAL | ○ |
| Ethernet通信 | — | UNIT_RJ71EN71 | PROTOCOL_TCPIP, PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_RJ71EN71_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_QJ71E71 | PROTOCOL_TCPIP, PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_LJ71E71 | PROTOCOL_TCPIP, PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_RETHER | PROTOCOL_TCPIP, PROTOCOL_UDPIP, PROTOCOL_TLS, PROTOCOL_DTLS | ○ |
| Ethernet通信 | — | UNIT_RETHER_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_FXVETHER | PROTOCOL_TCPIP | ○ |
| Ethernet通信 | — | UNIT_FXVETHER_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_MXF_ETHER | PROTOCOL_TCPIP, PROTOCOL_UDPIP, PROTOCOL_TLS, PROTOCOL_DTLS | ○ |
| Ethernet通信 | — | UNIT_MXF_ETHER_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_LNETHER | PROTOCOL_TCPIP | ○ |
| Ethernet通信 | — | UNIT_LNETHER, UNIT_LNETHER_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_QNETHER | PROTOCOL_TCPIP | ○ |
| Ethernet通信 | — | UNIT_QNETHER, UNIT_QNETHER_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_RJ71GN11 | PROTOCOL_TCPIP, PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_NZ2GF_ETB | PROTOCOL_TCPIP | ○ |
| Ethernet通信 | — | UNIT_NZ2GF_ETB, UNIT_NZ2GF_ETB_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_FXETHER | PROTOCOL_TCPIP | ○ |
| Ethernet通信 | — | UNIT_FXETHER_DIRECT | PROTOCOL_UDPIP | ○ |
| CPU COM通信 | 接続先CPUがFX5CPU | UNIT_FXVCPU | PROTOCOL_SERIAL | ○ |
| CPU COM通信 | 接続先CPUがQCPU(Qモード) | UNIT_QNCPU | PROTOCOL_SERIAL | ○ |
| CPU COM通信 | 接続先CPUがLCPU | UNIT_LNCPU | PROTOCOL_SERIAL | ○ |
| CPU COM通信 | 接続先CPUがQモーションCPU | UNIT_QNMOTION | PROTOCOL_SERIAL | × |
| CPU COM通信 | 接続先CPUがFXCPU | UNIT_FXCPU | PROTOCOL_SERIAL | ○ |
| USB通信 | 接続先CPUがRCPU | UNIT_RUSB | PROTOCOL_USB | ○ |
| USB通信 | 接続先CPUがLHCPU | UNIT_LHUSB | PROTOCOL_USB | ○ |
| USB通信 | 接続先CPUがFX5CPU | UNIT_FXVUSB | PROTOCOL_USB | ○ |
| USB通信 | 接続先CPUがQCPU(Qモード) | UNIT_QNUSB | PROTOCOL_USB | ○ |
| USB通信 | 接続先CPUがLCPU | UNIT_LNUSB | PROTOCOL_USB | ○ |
| USB通信 | 接続先CPUがQSCPU | UNIT_QSUSB | PROTOCOL_USB | ×*1 |
| USB通信 | 接続先CPUがQモーションCPU | UNIT_QNMOTIONUSB | PROTOCOL_USB | × |
| USB通信 | 接続先CPUがFXCPU | UNIT_FXCPU | PROTOCOL_USB | ○ |
| MELSECNET/H通信 | — | UNIT_MNETHBOARD | PROTOCOL_MNETH | ○*2 |
| CC-Link IEコントローラネットワーク通信 | — | UNIT_MNETGBOARD | PROTOCOL_MNETG | ○*2 |
| CC-Link IEフィールドネットワーク通信 | — | UNIT_CCIEFBOARD | PROTOCOL_CCIEF | ○*2 |
| CC-Link IE TSN通信 | — | UNIT_CCIETSNBOARD | PROTOCOL_CCIETSN | ○*2 |
| CC-Link通信 | — | UNIT_CCLINKBOARD | PROTOCOL_CCLINK | ○*2 |
| CC-Linkシステム RS-232インタフェース通信 | — | UNIT_G4QCPU | PROTOCOL_SERIAL | ○ |
| GX Simulator2通信 | — | UNIT_SIMULATOR2 | — | × |
| GX Simulator3通信(RCPU) | — | UNIT_SIMULATOR3 | — | × |
| GX Simulator3通信(FX5CPU) | — | UNIT_SIMULATOR3 | — | × |
| GX Simulator3通信(MX-Rモデル) | — | UNIT_SIMULATOR3 | — | × |
| GX Simulator3通信(MX-Fモデル) | — | UNIT_SIMULATOR3 | — | × |
| MT Simulator2通信 | — | UNIT_SIMULATOR2 | — | × |
| MELSOFT Mirror通信 | — | UNIT_RETHER_LCS | — | ○ |
| GOTゲートウェイデバイス通信 | — | UNIT_A900GOT | PROTOCOL_UDPIP | × |
| GOTトランスペアレント機能通信 | — | UNIT_RJ71C24, UNIT_FXVCPU, UNIT_QNCPU, UNIT_LNCPU, UNIT_FXCPU, UNIT_QJ71C24, UNIT_LJ71C24, UNIT_GOT_RJ71EN71, UNIT_GOT_QJ71E71, UNIT_GOT_LJ71E71, UNIT_GOT_RETHER, UNIT_GOT_QNETHER, UNIT_GOT_LNETHER, UNIT_A900GOT, UNIT_GOT_NZ2GF_ETB, UNIT_GOT_FXETHER, UNIT_GOT_FXENET | PROTOCOL_SERIAL, PROTOCOL_USBGOT | ○ |
| GOTトランスペアレント機能通信 | — | UNIT_GOTETHER_RJ71C24, UNIT_GOTETHER_FXVCPU, UNIT_GOTETHER_QNCPU, UNIT_GOTETHER_LNCPU, UNIT_GOTETHER_FXCPU, UNIT_GOTETHER_QBUS, UNIT_GOTETHER_QN_ETHER | PROTOCOL_TCPIP | ○ |
| インバータ通信 | — | — | COMM_RS232C, COMM_USB | × |

※原本では使用可否欄・ActProtocolType欄が複数行で結合されている箇所がある。本表では各行に同じ値を展開した。
※GX Simulator2通信とGX Simulator3通信(4行)の使用可否は原本では1セル(×)で結合。

> *1 QSCPUにアクセス時は，エラー 0x010A42A0(アクセスパスワードが不一致)となります。
> *2 自ボードアクセス時はエラーが返ります。

---

## GetCpuType(CPUユニット形名読出し) (11.3 / 461-462 / 原本 p.463-464)

### 使用可能コントロール (11.3 / 461 / 原本 p.463)

下記のコントロールで使用可能です。
- 32ビット用: ActProgType，ActUtlType
- 64ビット用: ActProgType64，ActUtlType64

### 機能 (11.3 / 461 / 原本 p.463)

CPUユニット，ネットワークボード，GOTの形名文字列および形名コード(16進)を読み出します。

### 書式 (11.3 / 461 / 原本 p.463)

**■VBA**

```
lRet = object.GetCpuType(szCpuName, lCpuType)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| String | szCpuName | 形名文字列 | Output |
| Long | lCpuType | 形名コード | Output |

**■Visual C++**

```
lRet = object.GetCpuType(*szCpuName, *lplCpuType)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| BSTR | *szCpuName | 形名文字列 | Output |
| Long | *lplCpuType | 形名コード | Output |

**■Visual Basic .NET**

```
IRet = object.GetCpuType(szCpuName, ICpuType)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| String | szCpuName | 形名文字列 | Output |
| Integer | ICpuType | 形名コード | Output |

**■Visual C#**

```
iRet = object.GetCpuType (out szCpuName, out iCpuType)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |
| String | szCpuName | 形名文字列 | Output |
| int | iCpuType | 形名コード | Output |

### 書式(オブジェクトを生成して使用する場合) (11.3 / 461 / 原本 p.463)

**■Visual C++**

```
hResult = object.GetCpuType(*szCpuName *lplCpuType, *lplRetCode)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| HRESULT | hResult | COMの戻り値 | Output |
| BSTR | *szCpuName | 形名文字列 | Output |
| LONG | *lplCpuType | 形名コード | Output |
| LONG | *lplRetCode | 通信関数の戻り値 | Output |

※書式の「*szCpuName *lplCpuType」の間にカンマが無いのは原本表記のまま(要確認)。

### 戻り値 (11.3 / 462 / 原本 p.464)

正常終了: 0を返します。  
異常終了: 0以外を返します。(☞617ページ エラーコード)  

### 説明 (11.3 / 462 / 原本 p.464)

- 通信を行っているCPUユニットの形名文字列をszCpuNameに，形名コード(16進)をlCpuType(lplCpuTypeまたはiCpuType)に格納します。
- 形名文字列はUNICODEで返されます。
- 形名コードはユニット固有の値(16進)です。

※GetCpuTypeには「通信経路の使用可否」表は掲載されていない(原本どおり)。

---

## SetCpuStatus(リモートコントロール) (11.3 / 463-465 / 原本 p.465-467)

### 使用可能コントロール (11.3 / 463 / 原本 p.465)

下記のコントロールで使用可能です。
- 32ビット用: ActProgType，ActUtlType
- 64ビット用: ActProgType64，ActUtlType64

### 機能 (11.3 / 463 / 原本 p.465)

CPUユニットのリモート操作を行います。

### 書式 (11.3 / 463 / 原本 p.465)

**■VBA**

```
lRet = object.SetCpuStatus(lOperation)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| Long | lOperation | リモートRUN/STOP/PAUSE/RESET | Input |

**■Visual C++**

```
lRet = object.SetCpuStatus(lOperation)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Long | lRet | 戻り値 | Output |
| Long | lOperation | リモートRUN/STOP/PAUSE/RESET | Input |

**■Visual Basic .NET**

```
IRet = object.SetCpuStatus(IOperation)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| Integer | IRet | 戻り値 | Output |
| Integer | IOperation | リモートRUN/STOP/PAUSE/RESET | Input |

**■Visual C#**

```
iRet = object.SetCpuStatus (iOperation)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| int | iRet | 戻り値 | Output |
| int | iOperation | リモートRUN/STOP/PAUSE/RESET | Input |

### 書式(オブジェクトを生成して使用する場合) (11.3 / 463 / 原本 p.465)

**■Visual C++**

```
hResult = object.SetCpuStatus(lOperation, *lplRetCode)
```

| データ型 | 引数 | 内容 | Input/Output |
|---|---|---|---|
| HRESULT | hResult | COMの戻り値 | Output |
| LONG | lOperation | リモートRUN/STOP/PAUSE/RESET | Input |
| LONG | *lplRetCode | 通信関数の戻り値 | Output |

### 戻り値 (11.3 / 463 / 原本 p.465)

正常終了: 0を返します。  
異常終了: 0以外を返します。(☞617ページ エラーコード)  

### 説明 (11.3 / 464 / 原本 p.466)

lOperation(iOperation)にて指定された操作を行います。
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
> - インバータ通信/ロボットコントローラ通信時は使用できません。
> - リモートRESETは，QCPU，LCPU，RCPU，LHCPU，およびFX5CPUでリモートRESETに対応している機種のみサポートしています。
> - ユーザ認証機能が有効なMXコントローラでは使用できません。

#### 通信経路の使用可否 (11.3 / 464-465 / 原本 p.466-467)

通信経路の使用可否を下表に示します。
○: 使用可能，×: 使用不可

| 通信経路 | 通信経路(詳細) | ActUnitType | ActProtocolType | 使用可否 |
|---|---|---|---|---|
| シリアルコミュニケーション通信 | 接続ユニットがMELSEC iQ-Rシリーズ対応C24 | UNIT_RJ71C24 | PROTOCOL_SERIAL | ○ |
| シリアルコミュニケーション通信 | 接続ユニットがQシリーズ対応C24 | UNIT_QJ71C24 | PROTOCOL_SERIAL | ○ |
| シリアルコミュニケーション通信 | 接続ユニットがLシリーズ対応C24 | UNIT_LJ71C24 | PROTOCOL_SERIAL | ○ |
| シリアルコミュニケーション通信 | 接続ユニットがFX拡張ポート | UNIT_FX485BD | PROTOCOL_SERIAL | ○*1*2 |
| Ethernet通信 | — | UNIT_RJ71EN71 | PROTOCOL_TCPIP, PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_RJ71EN71_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_QJ71E71 | PROTOCOL_TCPIP, PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_LJ71E71 | PROTOCOL_TCPIP, PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_RETHER | PROTOCOL_TCPIP, PROTOCOL_UDPIP, PROTOCOL_TLS, PROTOCOL_DTLS | ○ |
| Ethernet通信 | — | UNIT_RETHER_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_FXVETHER | PROTOCOL_TCPIP | ○*1 |
| Ethernet通信 | — | UNIT_FXVETHER_DIRECT | PROTOCOL_UDPIP | ○*1 |
| Ethernet通信 | — | UNIT_MXF_ETHER | PROTOCOL_TCPIP, PROTOCOL_UDPIP, PROTOCOL_TLS, PROTOCOL_DTLS | ○ |
| Ethernet通信 | — | UNIT_MXF_ETHER_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_LNETHER | PROTOCOL_TCPIP | ○ |
| Ethernet通信 | — | UNIT_LNETHER, UNIT_LNETHER_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_QNETHER | PROTOCOL_TCPIP | ○ |
| Ethernet通信 | — | UNIT_QNETHER, UNIT_QNETHER_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_RJ71GN11 | PROTOCOL_TCPIP, PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_NZ2GF_ETB | PROTOCOL_TCPIP | ○ |
| Ethernet通信 | — | UNIT_NZ2GF_ETB, UNIT_NZ2GF_ETB_DIRECT | PROTOCOL_UDPIP | ○ |
| Ethernet通信 | — | UNIT_FXETHER | PROTOCOL_TCPIP | ○*1 |
| Ethernet通信 | — | UNIT_FXETHER_DIRECT | PROTOCOL_UDPIP | ○*1 |
| CPU COM通信 | 接続先CPUがFX5CPU | UNIT_FXVCPU | PROTOCOL_SERIAL | ○*1 |
| CPU COM通信 | 接続先CPUがQCPU(Qモード) | UNIT_QNCPU | PROTOCOL_SERIAL | ○ |
| CPU COM通信 | 接続先CPUがLCPU | UNIT_LNCPU | PROTOCOL_SERIAL | ○ |
| CPU COM通信 | 接続先CPUがQモーションCPU | UNIT_QNMOTION | PROTOCOL_SERIAL | ○ |
| CPU COM通信 | 接続先CPUがFXCPU | UNIT_FXCPU | PROTOCOL_SERIAL | ○*1 |
| USB通信 | 接続先CPUがRCPU | UNIT_RUSB | PROTOCOL_USB | ○ |
| USB通信 | 接続先CPUがLHCPU | UNIT_LHUSB | PROTOCOL_USB | ○ |
| USB通信 | 接続先CPUがFX5CPU | UNIT_FXVUSB | PROTOCOL_USB | ○ |
| USB通信 | 接続先CPUがQCPU(Qモード) | UNIT_QNUSB | PROTOCOL_USB | ○ |
| USB通信 | 接続先CPUがLCPU | UNIT_LNUSB | PROTOCOL_USB | ○ |
| USB通信 | 接続先CPUがQSCPU | UNIT_QSUSB | PROTOCOL_USB | ×*3 |
| USB通信 | 接続先CPUがQモーションCPU | UNIT_QNMOTIONUSB | PROTOCOL_USB | ○ |
| USB通信 | 接続先CPUがFXCPU | UNIT_FXCPU | PROTOCOL_USB | ○*1 |
| MELSECNET/H通信 | — | UNIT_MNETHBOARD | PROTOCOL_MNETH | ○*4 |
| CC-Link IEコントローラネットワーク通信 | — | UNIT_MNETGBOARD | PROTOCOL_MNETG | ○*4 |
| CC-Link IEフィールドネットワーク通信 | — | UNIT_CCIEFBOARD | PROTOCOL_CCIEF | ○*4 |
| CC-Link IE TSN通信 | — | UNIT_CCIETSNBOARD | PROTOCOL_CCIETSN | ○*4 |
| CC-Link通信 | — | UNIT_CCLINKBOARD | PROTOCOL_CCLINK | ○*4 |
| CC-Linkシステム RS-232インタフェース通信 | — | UNIT_G4QCPU | PROTOCOL_SERIAL | ○ |
| GX Simulator2通信 | — | UNIT_SIMULATOR2 | — | ○ |
| GX Simulator3通信(RCPU) | — | UNIT_SIMULATOR3 | — | ○ |
| GX Simulator3通信(FX5CPU) | — | UNIT_SIMULATOR3 | — | ○*1 |
| GX Simulator3通信(MX-Rモデル) | — | UNIT_SIMULATOR3 | — | ○*1 |
| GX Simulator3通信(MX-Fモデル) | — | UNIT_SIMULATOR3 | — | ○*1 |
| MT Simulator2通信 | — | UNIT_SIMULATOR2 | — | ○ |
| MELSOFT Mirror通信 | — | UNIT_RETHER_LCS | — | ○ |
| GOTゲートウェイデバイス通信 | — | UNIT_A900GOT | PROTOCOL_UDPIP | × |
| GOTトランスペアレント機能通信 | — | UNIT_RJ71C24, UNIT_QNCPU, UNIT_LNCPU | PROTOCOL_SERIAL, PROTOCOL_USBGOT | ○ |
| GOTトランスペアレント機能通信 | — | UNIT_FXVCPU, UNIT_FXCPU | PROTOCOL_SERIAL, PROTOCOL_USBGOT | ○*1 |
| GOTトランスペアレント機能通信 | — | UNIT_QJ71C24, UNIT_LJ71C24, UNIT_GOT_RJ71EN71, UNIT_GOT_QJ71E71, UNIT_GOT_LJ71E71, UNIT_GOT_RETHER, UNIT_GOT_QNETHER, UNIT_GOT_LNETHER, UNIT_A900GOT, UNIT_GOT_NZ2GF_ETB | PROTOCOL_SERIAL, PROTOCOL_USBGOT | ○ |
| GOTトランスペアレント機能通信 | — | UNIT_GOT_FXETHER, UNIT_GOT_FXENET | PROTOCOL_SERIAL, PROTOCOL_USBGOT | ○*1 |
| GOTトランスペアレント機能通信 | — | UNIT_GOTETHER_RJ71C24, UNIT_GOTETHER_QNCPU, UNIT_GOTETHER_LNCPU | PROTOCOL_TCPIP | ○ |
| GOTトランスペアレント機能通信 | — | UNIT_GOTETHER_FXVCPU, UNIT_GOTETHER_FXCPU | PROTOCOL_TCPIP | ○*1 |
| GOTトランスペアレント機能通信 | — | UNIT_GOTETHER_QBUS | PROTOCOL_TCPIP | ○ |
| GOTトランスペアレント機能通信 | — | UNIT_GOTETHER_QN_ETHER | PROTOCOL_TCPIP | ○ |
| インバータ通信 | — | — | COMM_RS232C, COMM_USB | × |

※原本では使用可否欄・ActProtocolType欄が複数行で結合されている箇所がある。本表では各行に同じ値を展開した。
※GX Simulator2通信とGX Simulator3通信(RCPU)の使用可否は原本では1セル(○)，GX Simulator3通信(FX5CPU)/(MX-Rモデル)/(MX-Fモデル)の3行は1セル(○*1)で結合。MX-R/MX-Fモデルに*1(PAUSE指定でエラー)が掛かるのは原本の結合範囲どおり(要確認)。Ethernet通信の UNIT_FXVETHER と UNIT_FXVETHER_DIRECT，UNIT_FXETHER と UNIT_FXETHER_DIRECT の○*1 はそれぞれ結合セル。

> *1 PAUSE指定を行うとエラーが返ります。
> *2 FX3S，FX3U，FX3UC，FX3G，FX3GC以外のCPUはエラーが返ります。
> *3 QSCPUにアクセス時は，エラー 0x010A42A0(アクセスパスワードが不一致)となります。
> *4 自ボードアクセス時はエラーが返ります。

