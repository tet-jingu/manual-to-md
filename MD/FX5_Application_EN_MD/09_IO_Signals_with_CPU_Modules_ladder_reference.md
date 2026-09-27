# 9 SPECIFICATIONS OF I/O SIGNALS WITH CPU MODULES (CPUユニットとの入出力信号仕様) (Chapter 9 / original p.389-390)

FX5 Motion Module/Simple Motion Module User's Manual (Application) IB(NA)-0300253ENG-P (Japanese manual number: IB-0300252-M) — reference

> This file is a reference of the original PDF. In addition to tables, addresses and bit definitions,
> function descriptions, device ON/OFF timing, precautions and program examples are transcribed **verbatim in full**.
> For ranges not converted, see the "Conversion range" table (in this file and `00_Index_ladder_reference.md`). **When making design decisions based on module behavior,
> do the final check on the corresponding page of the original.**
>
> Notation:
> - "original p.N" is the **PDF page number**. Printed page number = PDF page − 2. Cross-references in the text (e.g. "Page 142 Block start") keep the original (printed page).
> - Merged cells of the original are expanded to each row (noted right after the table).
> - Figures are shown as a [Figure] placeholder + bullet list of facts that could be read.
> - The original "☞" (page reference mark) is written as "→", and "📖" (other manual mark) as "[Other manual]". `U1¥G` is written `U1\G`.
> - Ladder program examples are transcribed as mnemonic (step numbers and devices as printed).
> - Headings carry the Japanese term in parentheses for search. Body text is the original English only.
> - Obvious typos in the original are kept as printed and marked with a short note ("*Note" / 要確認).

## Conversion range (変換範囲表 / original p.389-390)

| Original page | Section | Handling |
|---|---|---|
| p.389-390 | 9 SPECIFICATIONS OF I/O SIGNALS WITH CPU MODULES, 9.1 List of Input/Output Signals with CPU Modules (p.390 is a blank MEMO page) | Full text |

## Table of Contents (目次)

- 9 SPECIFICATIONS OF I/O SIGNALS WITH CPU MODULES (CPUユニットとの入出力信号仕様)
- 9.1 List of Input/Output Signals with CPU Modules (CPUユニットとの入出力信号一覧)

---

## 9 SPECIFICATIONS OF I/O SIGNALS WITH CPU MODULES (CPUユニットとの入出力信号仕様) (Chapter 9 / original p.389-390)

## 9.1 List of Input/Output Signals with CPU Modules (CPUユニットとの入出力信号一覧) (9.1 / original p.389-390)

The Simple Motion module/Motion module uses 10 input points and 10 output points for exchanging data with the CPU module.
The input/output signals of the Simple Motion module/Motion module are shown below.
- 4-axis/8-axis module

#### Signal direction: Simple Motion module/Motion module → CPU module (信号方向: シンプルモーションユニット／モーションユニット→CPUユニット) (9.1 / original p.389)

| Buffer memory address | Signal name |
|---|---|
| 31500.b0 | READY |
| 31500.b1 | Synchronization flag |
| 31501.b0 | Axis 1 BUSY*1 |
| 31501.b1 | Axis 2 BUSY*1 |
| 31501.b2 | Axis 3 BUSY*1 |
| 31501.b3 | Axis 4 BUSY*1 |
| 31501.b4 | Axis 5 BUSY*1 |
| 31501.b5 | Axis 6 BUSY*1 |
| 31501.b6 | Axis 7 BUSY*1 |
| 31501.b7 | Axis 8 BUSY*1 |

*In the original, the "Signal name" column is split into an "Axis 1" to "Axis 8" column and a "BUSY*1" column, and "BUSY*1" is one cell merged over the 8 rows 31501.b0 to 31501.b7. Expanded to each row.

#### Signal direction: CPU module → Simple Motion module/Motion module (信号方向: CPUユニット→シンプルモーションユニット／モーションユニット) (9.1 / original p.389)

| Buffer memory address | Signal name |
|---|---|
| 5950 | PLC READY |
| 5951 | All axis servo ON |
| 30104 | Axis 1 Positioning start*1 |
| 30114 | Axis 2 Positioning start*1 |
| 30124 | Axis 3 Positioning start*1 |
| 30134 | Axis 4 Positioning start*1 |
| 30144 | Axis 5 Positioning start*1 |
| 30154 | Axis 6 Positioning start*1 |
| 30164 | Axis 7 Positioning start*1 |
| 30174 | Axis 8 Positioning start*1 |

*In the original, the "Signal name" column is split into an "Axis 1" to "Axis 8" column and a "Positioning start*1" column, and "Positioning start*1" is one cell merged over the 8 rows 30104 to 30174. Expanded to each row.

*1 The BUSY signal and positioning start signal, whose axis Nos. exceed the number of controlled axes, cannot be used.

> **Point**
> - The M code ON signal, error detection signal, start complete signal and positioning complete signal are assigned to the bit of "[Md.31] Status".
> - The axis stop signal, forward run JOG start signal, reverse run JOG start signal, execution prohibition flag are assigned to the buffer memory [Cd.180] to [Cd.183].

(original p.390 is a "MEMO" page (blank). No body text.)
