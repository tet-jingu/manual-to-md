# 4 HIGH-LEVEL POSITIONING CONTROL (高度な位置決め制御) (Chapter 4 / original p.139-158)

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

## Conversion range (変換範囲表 / original p.139-158)

| Original page | Section | Handling |
|---|---|---|
| p.139 | 4 HIGH-LEVEL POSITIONING CONTROL (chapter introduction) | Full text |
| p.139-141 | 4.1 Outline of High-level Positioning Control | Full text (buffer memory configuration figure written out) |
| p.142 | 4.2 High-level Positioning Control Execution Procedure | Full text (flow figure written out as table) |
| p.143-151 | 4.3 Setting the Block Start Data | Full text |
| p.152-154 | 4.4 Setting the Condition Data | Full text |
| p.155-158 | 4.5 Start Program for High-level Positioning Control | Full text (including program example) |

## Table of Contents (目次)

- 4 HIGH-LEVEL POSITIONING CONTROL (高度な位置決め制御)
- 4.1 Outline of High-level Positioning Control (高度な位置決め制御の概要)
- 4.2 High-level Positioning Control Execution Procedure (高度な位置決め制御の実行手順)
- 4.3 Setting the Block Start Data (ブロック始動データの設定)
- 4.4 Setting the Condition Data (条件データの設定)
- 4.5 Start Program for High-level Positioning Control (高度な位置決め制御の始動プログラム)

---

## 4 HIGH-LEVEL POSITIONING CONTROL (高度な位置決め制御) (Chapter 4 / original p.139)

The details and usage of high-level positioning control (control functions using the "block start data") are explained in this chapter.
High-level positioning control is used to carry out applied control using the "positioning data". Examples of applied control are using conditional judgment to control "positioning data" set with the major positioning control, or simultaneously starting "positioning data" for several different axes.
Read the execution procedures and settings for each control, and set as required.

## 4.1 Outline of High-level Positioning Control (高度な位置決め制御の概要) (4.1 / original p.139-141)

In "high-level positioning control" the execution order and execution conditions of the "positioning data" are set to carry out more applied positioning. (The execution order and execution conditions are set in the "block start data" and "condition data".)
The following applied positioning controls can be carried out with "high-level positioning control".

| High-level positioning control | Details |
|---|---|
| Block*1 start (Normal start) | With one start, executes the positioning data in a random block with the set order. |
| Condition start | Carries out condition judgment set in the "condition data" for the designated positioning data, and then executes the "block start data".<br>• When the condition is established, the "block start data" is executed.<br>• When not established, that "block start data" is ignored, and the next point's "block start data" is executed. |
| Wait start | Carries out condition judgment set in the "condition data" for the designated positioning data, and then executes the "block start data".<br>• When the condition is established, the "block start data" is executed.<br>• When not established, stops the control until the condition is established. (Waits.) |
| Simultaneous start*2 | Simultaneously executes the designated positioning data of the axis designated with the "condition data". (Outputs command at the same timing.) |
| Repeated start (FOR loop) | Repeats the program from the "block start data" set with the "FOR loop" to the "block start data" set in "NEXT" for the designated number of times. |
| Repeated start (FOR condition) | Repeats the program from the "block start data" set with the "FOR condition" to the "block start data" set in "NEXT" until the conditions set in the "condition data" are established. |

*1 "1 block" is defined as all the data continuing from the positioning data in which "continuous positioning control" or "continuous path control" is set in the "[Da.1] Operation pattern" to the positioning data in which "independent positioning control (Positioning complete)" is set.

*2 Besides the simultaneous start of "block start data" system, the "simultaneous starts" include the "multiple axes simultaneous start control" of control method. Refer to the following for details.
→Page 28 Multiple axes simultaneous start

### High-level positioning control sub functions (高度な位置決め制御の補助機能) (4.1 / original p.139)

"High-level positioning control" uses the "positioning data" set with the "major positioning control". Refer to "Combination of Main Functions and Sub Functions" in the following manual for details on sub functions that can be combined with the major positioning control.
[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Startup)
Note that the pre-reading start function cannot be used together with "high-level positioning control".

### Data required for high-level positioning control (高度な位置決め制御に必要なデータ) (4.1 / original p.140)

"High-level positioning control" is executed by setting the required items in the "block start data" and "condition data", then starting that "block start data". Judgment about whether execution is possible, etc., is carried out at execution using the "condition data" designated in the "block start data".
"Block start data" can be set for each No. from 7000 to 7004 (called "block Nos."), and up to 50 points can be set for each axis. (This data is controlled with Nos. called "points" to distinguish it from the positioning data. For example, the 1st block start data item is called the "1st point block start data" or "point No.1 block start data".)
"Condition data" can be set for each No. from 7000 to 7004 (called "block Nos."), and up to 10 data items can be set for each axis.
The "block start data" and "condition data" are set as 1 set for each block No.
The following table shows an outline of the "block start data" and "condition data" stored in the Simple Motion module/Motion module.

| Setting item | | | Setting details |
|---|---|---|---|
| Block start data | [Da.11] | Shape | Set whether to end the control after executing only the "block start data" of the shape itself, or continue executing the "block start data" set in the next point. |
| Block start data | [Da.12] | Start data No. | Set the "positioning data No." to be executed. |
| Block start data | [Da.13] | Special start instruction | Set the method by which the positioning data set in [Da.12] will be started. |
| Block start data | [Da.14] | Parameter | Set the conditions by which the start will be executed according to the commands set in [Da.13]. (Designate the "condition data No." and "Number of repetitions".) |

*In the original, "Block start data" (classification column) is merged over the 4 rows. Expanded to each row.

| Setting item | | | Setting details |
|---|---|---|---|
| Condition data | [Da.15] | Condition target | Designate the "device", "buffer memory storage details", and "positioning data No." elements for which the conditions are set. |
| Condition data | [Da.16] | Condition operator | Set the judgment method carried out for the target set in [Da.15]. |
| Condition data | [Da.17] | Address | Set the buffer memory address in which condition judgment is carried out (only when the details set in [Da.15] are "buffer memory storage details"). |
| Condition data | [Da.18] | Parameter 1 | Set the required conditions according to the details set in [Da.15], [Da.16] and [Da.23]. |
| Condition data | [Da.19] | Parameter 2 | Set the required conditions according to the details set in [Da.15], [Da.16] and [Da.23]. |
| Condition data | [Da.23] | Number of simultaneously starting axes | Set the number of axes to be started simultaneously in the simultaneously start. |
| Condition data | [Da.24] | Simultaneously starting axis No.1 | Set the simultaneously starting axis in the simultaneously start. |
| Condition data | [Da.25] | Simultaneously starting axis No.2 | Set the simultaneously starting axis in the simultaneously start. |
| Condition data | [Da.26] | Simultaneously starting axis No.3 | Set the simultaneously starting axis in the simultaneously start. |

*In the original, "Condition data" (classification column) is merged over the 9 rows; the "Setting details" of [Da.18] and [Da.19] is one merged cell (2 rows), and the "Setting details" of [Da.24] to [Da.26] is one merged cell (3 rows). Expanded to each row.

### "Block start data" and "condition data" configuration (「ブロック始動データ」と「条件データ」の構成) (4.1 / original p.141)

The "block start data" and "condition data" corresponding to "block No.7000" can be stored in the buffer memory.

[Figure] Buffer memory configuration of "block start data" and "condition data" (original p.141)
- Block start data: stacked sheets "1st point", "2nd point" ... "50th point", each with columns "Setting item" / "Buffer memory address". Each point consists of 2 words:
  - 1st word (1st point: 22000+400n): 16-bit word b15 ... b8 b7 ... b0. "[Da.11] Shape" is bracketed at the b15 end (a short bracket) and "[Da.12] Start data No." is bracketed over the remaining bits down to b0. (The exact bit boundary between [Da.11] and [Da.12] is not labeled in the figure; see original p.141.)
  - 2nd word (1st point: 22050+400n): b15 to b8 = "[Da.13] Special start instruction", b7 to b0 = "[Da.14] Parameter" (brackets split at the b8/b7 boundary).
- Addresses shown for each point:

| Point | 1st word ([Da.11] Shape / [Da.12] Start data No.) | 2nd word ([Da.13] Special start instruction / [Da.14] Parameter) |
|---|---|---|
| 1st point | 22000+400n | 22050+400n |
| 2nd point | 22001+400n | 22051+400n |
| 50th point | 22049+400n | 22099+400n |

  (The 3rd to 49th points are drawn as stacked sheets behind, without individual addresses.)
- Condition data: stacked sheets "No.1", "No.2" ... "No.10", each with columns "Setting item" / "Buffer memory address". Composition of No.1:
  - 22100+400n: 16-bit word with bit marks b15 b12 b8 b4 b0; "[Da.16] Condition operator" bracketed over b15 to b8, "[Da.15] Condition target" over b7 to b0.
  - [Da.17] Address: 22102+400n, 22103+400n
  - [Da.18] Parameter 1: 22104+400n, 22105+400n
  - [Da.19] Parameter 2: 22106+400n, 22107+400n
  - 22108+400n (bit marks b15 b12 b8 b4 b0): "[Da.25] Simultaneously starting axis No.2" over b15 to b8, "[Da.24] Simultaneously starting axis No.1" over b7 to b0.
  - 22109+400n (bit marks b31 b28 b24 b20 b16): "[Da.23] Number of simultaneously starting axes" over b31 to b24, "[Da.26] Simultaneously starting axis No.3" over b23 to b16.
- Addresses shown for each condition data No.:

| Setting item | No.1 | No.2 | No.10 |
|---|---|---|---|
| [Da.16] Condition operator / [Da.15] Condition target | 22100+400n | 22110+400n | 22190+400n |
| [Da.17] Address | 22102+400n<br>22103+400n | 22112+400n<br>22113+400n | 22192+400n<br>22193+400n |
| [Da.18] Parameter 1 | 22104+400n<br>22105+400n | 22114+400n<br>22115+400n | 22194+400n<br>22195+400n |
| [Da.19] Parameter 2 | 22106+400n<br>22107+400n | 22116+400n<br>22117+400n | 22196+400n<br>22197+400n |
| [Da.23] to [Da.26] | 22108+400n<br>22109+400n | 22118+400n<br>22119+400n | 22198+400n<br>22199+400n |

  - Labels in the figure: 22192+400n ← "Low-order buffer memory", 22193+400n ← "High-order buffer memory".
  - (No.3 to No.9 are drawn as stacked sheets behind, without individual addresses.)
- Below the figure (arrow down): Block No. → "7000". "Set the block No. with the program or the engineering tool."

Set the "block start data" and "condition data" corresponding to the following "block No.7001" using the program or the engineering tool to Simple Motion module/Motion module.
The "block start data" and "condition data" corresponding to "block No.7002 to 7004" are not allocated. Set the data with the engineering tool.

## 4.2 High-level Positioning Control Execution Procedure (高度な位置決め制御の実行手順) (4.2 / original p.142)

High-level positioning control is carried out using the following procedure.

[Figure] High-level positioning control execution procedure flow (original p.142)

| Stage | STEP | Box in the flow | Note on the right |
|---|---|---|---|
| Preparation | STEP 1 | Carry out the "major positioning control" setting. | "High-level positioning control" executes each control ("major positioning control") set in the positioning data with the designated conditions, so first carry out preparations so that "major positioning control" can be executed. |
| Preparation | STEP 2 | Set the "block start data" corresponding to each control. ([Da.11] to [Da.14]) × required data amount | The "block start data" from 1 to 50 points can be set. |
| Preparation | STEP 3 | Set the "condition data". ([Da.15] to [Da.19] and [Da.23] to [Da.26]) × required data amount | Set the "condition data" for designation with the "block start data". Up to 10 condition data items can be set. |
| Preparation | STEP 4 | Create a program in which block No. is set in the"[Cd.3] Positioning start No." (Control data setting) | The Simple Motion module/Motion module recognizes that the control is high-level positioning control using "block start data" by the "7000" designation. |
| Preparation | STEP 4 | Create a program in which the "block start data point No. to be started" (1 to 50) is set in the "[Cd. 4] Positioning starting point No." | Use the engineering tool to create a program to execute the "high-level positioning control". |
| Preparation | STEP 4 | Create a program in which the "positioning start signal" is turned ON by a positioning start command. | (STEP 4 common: note above) |
| Preparation | STEP 5 | Write the programs created in STEP4 to the CPU module. | Write the program created in STEP 4 to the CPU module using the engineering tool. |
| Starting the control | STEP 6 | Turn ON the "positioning start command" of the axis to be started. | Same procedure as for the "major positioning control" start. |
| Monitoring the control | STEP 7 | Monitor the high-level positioning control. | Monitor using the engineering tool. |
| Stopping the control | STEP 8 | Stop when control is completed | Same procedure as for the "major positioning control" stop. |

- The flow ends with "Control termination".
- *In the original, "Preparation" is a bracket over STEP 1 to STEP 5, and the 3 boxes of STEP 4 are enclosed by one bracket (the note "Use the engineering tool to create a program to execute the "high-level positioning control"." is placed beside that bracket). Expanded to each row.

> **Point**
> - Five sets of "block start data (50 points)" and "condition data (10 items)" corresponding to "No.7000 to 7004" are set with a program.
> - Five sets corresponding to "7000" to "7004" can be set with an engineering tool as well. When writing to the Simple Motion module/Motion module after setting the "block start data" and the "condition data" corresponding to "7000" to "7004" using an engineering tool, "7000" to "7004" can be set in "[Cd.3] Positioning start No." on STEP4.

## 4.3 Setting the Block Start Data (ブロック始動データの設定) (4.3 / original p.143-151)

### Relation between various controls and block start data (各制御とブロック始動データの関係) (4.3 / original p.143)

The "block start data" must be set to carry out "high-level positioning control".
The setting requirements and details of each "block start data" item to be set differ according to the "[Da.13] Special start instruction" setting.
The following shows the "block start data" setting items corresponding to various control methods.
Also refer to the following for details on "condition data" with which control execution is judged.
→Page 150 Setting the Condition Data
(The "block start data" settings in this chapter are assumed to be carried out using the engineering tool.)
◎: One of the two setting items must be set.
○: Set as required (Set to "—" when not used.)
×: Setting not possible
—: Setting not required (Set the initial value or a value within the setting range.)

| Block start data setting items | | | Block start (Normal start) | Condition start | Wait start | Simultaneous start | Repeated start (FOR loop) | Repeated start (FOR condition) | NEXT start*1 |
|---|---|---|---|---|---|---|---|---|---|
| [Da.11] | Shape | 0: End | ◎ | ◎ | ◎ | ◎ | × | × | ◎ |
| [Da.11] | Shape | 1: Continue | ◎ | ◎ | ◎ | ◎ | ◎ | ◎ | ◎ |
| [Da.12] | Start data No. | | 1 to 600 | 1 to 600 | 1 to 600 | 1 to 600 | 1 to 600 | 1 to 600 | 1 to 600 |
| [Da.13] | Special start instruction | | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| [Da.14] | Parameter | | — | Condition data No. | Condition data No. | Condition data No. | Number of repetitions | Condition data No. | — |

*In the original, "[Da.11]" and "Shape" are merged over 2 rows; "1 to 600" of [Da.12] is one cell merged over all 7 control columns; "Condition data No." of [Da.14] is one cell merged over the 3 columns Condition start / Wait start / Simultaneous start. Expanded to each row/column.

*1 The "NEXT start" instruction is used in combination with "repeated start (FOR loop)" and "repeated start (FOR condition)". Control using only the "NEXT start" will not be carried out.

> **Point**
> It is recommended that the "block start data" be set whenever possible with the engineering tool. Execution by a program uses many programs and devices. The execution becomes complicated, and the scan times will increase.

### Block start (ブロック始動) (4.3 / original p.144-145)

In a "block start (normal start)", the positioning data groups of a block are continuously executed in a set PLC starting from the positioning data set in "[Da.12] Start data No." by one start.
The control examples are shown when the "block start data" and "positioning data" are set as shown in the setting examples.

#### Setting examples (設定例) (4.3 / original p.144)

##### Block start data setting example (ブロック始動データの設定例) (4.3 / original p.144)

| Axis 1 block start data | [Da.11] Shape | [Da.12] Start data No. | [Da.13] Special start instruction | [Da.14] Parameter |
|---|---|---|---|---|
| 1st point | 1: Continue | 1 | 0: Block start | — |
| 2nd point | 1: Continue | 2 | 0: Block start | — |
| 3rd point | 1: Continue | 5 | 0: Block start | — |
| 4th point | 1: Continue | 10 | 0: Block start | — |
| 5th point | 0: End | 15 | 0: Block start | — |
| ⋮ | | | | |

##### Positioning data setting example (位置決めデータの設定例) (4.3 / original p.144)

| Axis 1 positioning data No. | [Da.1] Operation pattern | (block) |
|---|---|---|
| 1 | 00: Positioning complete | |
| 2 | 11: Continuous path control | 1 block*1 |
| 3 | 01: Continuous positioning control | 1 block*1 |
| 4 | 00: Positioning complete | 1 block*1 |
| 5 | 11: Continuous path control | 1 block |
| 6 | 00: Positioning complete | 1 block |
| ⋮ | | |
| 10 | 00: Positioning complete | |
| ⋮ | | |
| 15 | 00: Positioning complete | |
| ⋮ | | |

*In the original, there is no header for the third column (it is part of the "[Da.1] Operation pattern" header area); "1 block*1" is merged over Nos.2 to 4 and "1 block" over Nos.5 to 6. Expanded to each row.

*1 "1 block" is defined as all the data continuing from the positioning data in which "continuous positioning control" or "continuous path control" is set in the "[Da.1] Operation pattern" to the positioning data in which "independent positioning control (Positioning complete)" is set.

#### Control examples (制御例) (4.3 / original p.145)

The following shows the control being executed when the "block start data" of the 1st point of axis 1 is set as shown in the setting examples and started.
- The positioning data is executed in the following order before stopping. Axis 1 positioning data No.1 → 2 → 3 → 4 → 5 → 6 → 10 → 15.

##### Operation example (動作例) (4.3 / original p.145)

[Figure] Operation example of block start (original p.145)
- Notation in the figure: "Positioning data No.(Operation pattern)". Vertical axis: Address(+) upward, Address(-) downward; horizontal axis: t.
- Positioning according to the 1st point settings: 1(00) in the Address(+) direction, stops; then *1.
- Positioning according to the 2nd point settings: 2(11) → 3(01) → 4(00), all in the Address(+) direction. 2(11) passes into 3(01) without stopping (continuous path); after 3(01) the axis decelerates and stops, *1 follows, then 4(00); after 4(00), *1.
- Positioning according to the 3rd point settings: 5(11) → 6(00) in the Address(-) direction (5(11) passes into 6(00) without stopping); after 6(00), *1.
- Positioning according to the 4th point settings: 10(00) in the Address(+) direction; after it, *1.
- Positioning according to the 5th point settings: 15(00) in the Address(-) direction; after it, *1.
- [Cd.184] Positioning start: OFF → ON at the start; turns OFF at the end (after the dwell time of 15(00)).
- Start complete signal ([Md.31] Status: b14): turns ON following the ON of [Cd.184]; turns OFF following the OFF of [Cd.184].
- [Md.141] BUSY: turns ON following the ON of [Cd.184]; stays ON through all points; turns OFF at the end of the dwell time of 15(00).
- Positioning complete signal ([Md.31] Status: b15): turns ON for a short time at the dashed lines between positioning data (8 short pulses are drawn during the operation, the first one labeled "ON"), and once more after [Md.141] BUSY turns OFF (arrow from BUSY OFF to b15 ON).
- *1 Dwell time of corresponding positioning data

### Condition start (条件始動) (4.3 / original p.146)

In a "condition start", the "condition data" conditional judgment designated in "[Da.14] Parameter" is carried out for the positioning data set in "[Da.12] Start data No.". If the conditions have been established, the "block start data" set in "1: condition start" is executed. If the conditions have not been established, that "block start data" will be ignored, and the "block start data" of the next point will be executed.
The control examples are shown when the "block start data" and "positioning data" are set as shown in the setting examples.

#### Setting examples (設定例) (4.3 / original p.146)

##### Block start data setting example (ブロック始動データの設定例) (4.3 / original p.146)

| Axis 1 block start data | [Da.11] Shape | [Da.12] Start data No. | [Da.13] Special start instruction | [Da.14] Parameter |
|---|---|---|---|---|
| 1st point | 1: Continue | 1 | 1: Condition start | 1 |
| 2nd point | 1: Continue | 10 | 1: Condition start | 2 |
| 3rd point | 0: End | 50 | 0: Block start | — |
| ⋮ | | | | |

The "condition data Nos." have been set in "[Da.14] Parameter".

##### Positioning data setting example (位置決めデータの設定例) (4.3 / original p.146)

| Axis 1 positioning data No. | [Da.1] Operation pattern |
|---|---|
| 1 | 01: Continuous positioning control |
| 2 | 01: Continuous positioning control |
| 3 | 00: Positioning complete |
| ⋮ | |
| 10 | 11: Continuous path control |
| 11 | 11: Continuous path control |
| 12 | 00: Positioning complete |
| ⋮ | |
| 50 | 00: Positioning complete |
| ⋮ | |

#### Control examples (制御例) (4.3 / original p.146)

The following shows the control executed when the "block start data" of the 1st point of axis 1 is set as shown in the setting examples and started.
1. The conditional judgment set in "condition data No.1" is carried out before execution of the axis 1 "positioning data No.1".
   → Conditions established → Execute positioning data No.1, 2, and 3 → Go to the next 2.
   → Conditions not established → Go to the next 2.
2. The conditional judgment set in "condition data No.2" is carried out before execution of the axis 1 "positioning data No.10".
   → Conditions established → Execute positioning data No.10, 11, and 12 → Go to the next 3.
   → Conditions not established → Go to the next 3.
3. Execute axis 1 "positioning data No.50" and stop the control.

### Wait start (ウェイト始動) (4.3 / original p.147)

In a "wait start", the "condition data" conditional judgment designated in "[Da.14] Parameter" is carried out for the positioning data set in "[Da.12] Start data No.". If the conditions have been established, the "block start data" is executed. If the conditions have not been established, the control stops (waits) until the conditions are established.
The control examples are shown when the "block start data" and "positioning data" are set as shown in the setting examples.

#### Setting examples (設定例) (4.3 / original p.147)

##### Block start data setting example (ブロック始動データの設定例) (4.3 / original p.147)

| Axis 1 block start data | [Da.11] Shape | [Da.12] Start data No. | [Da.13] Special start instruction | [Da.14] Parameter |
|---|---|---|---|---|
| 1st point | 1: Continue | 1 | 2: Wait start | 3 |
| 2nd point | 1: Continue | 10 | 0: Block start | — |
| 3rd point | 0: End | 50 | 0: Block start | — |
| ⋮ | | | | |

The "condition data Nos." have been set in "[Da.14] Parameter".

##### Positioning data setting example (位置決めデータの設定例) (4.3 / original p.147)

| Axis 1 positioning data No. | [Da.1] Operation pattern |
|---|---|
| 1 | 01: Continuous positioning control |
| 2 | 01: Continuous positioning control |
| 3 | 00: Positioning complete |
| ⋮ | |
| 10 | 11: Continuous path control |
| 11 | 11: Continuous path control |
| 12 | 00: Positioning complete |
| ⋮ | |
| 50 | 00: Positioning complete |
| ⋮ | |

#### Control examples (制御例) (4.3 / original p.147)

The following shows the control executed when the "block start data" of the 1st point of axis 1 is set as shown in the setting examples and started.
1. The conditional judgment set in "condition data No.3" is carried out before execution of the axis 1 "positioning data No.1".
   → Conditions established → Execute positioning data No.1, 2, and 3 → Go to the next 2.
   → Conditions not established → Control stops (waits) until conditions are established → Go to the above 1.
2. Execute the axis 1 "positioning data No.10, 11, 12, and 50" and stop the control.

### Simultaneous start (同時始動) (4.3 / original p.148)

In a "simultaneous start", the positioning data set in the "[Da.12] Start data No." and positioning data of other axes set in the "condition data" are simultaneously executed (commands are output with the same timing). (The "condition data" is designated with "[Da.14] Parameter".)
The control examples are shown when the "block start data" and "positioning data" are set as shown in the setting examples.

#### Setting examples (設定例) (4.3 / original p.148)

##### Block start data setting example (ブロック始動データの設定例) (4.3 / original p.148)

| Axis 1 block start data | [Da.11] Shape | [Da.12] Start data No. | [Da.13] Special start instruction | [Da.14] Parameter |
|---|---|---|---|---|
| 1st point | 0: End | 1 | 3: Simultaneous start | 4 |
| ⋮ | | | | |

It is assumed that the "axis 2 positioning data" for simultaneous starting is set in the "condition data" designated with "[Da.14] Parameter".

##### Positioning data setting example (位置決めデータの設定例) (4.3 / original p.148)

| Axis 1 positioning data No. | [Da.1] Operation pattern |
|---|---|
| 1 | 01: Continuous positioning control |
| 2 | 01: Continuous positioning control |
| 3 | 00: Positioning complete |
| ⋮ | |

#### Control examples (制御例) (4.3 / original p.148)

The following shows the control executed when the "block start data" of the 1st point of axis 1 is set as shown in the setting examples and started.
1. Check the axis operation status of axis 2 which is regarded as the simultaneously started axis.
   → Axis 2 is standing by → Go to the next 2.
   → Axis 2 is carrying out positioning. → An error occurs and simultaneous start will not be carried out.
2. Simultaneously start the axis 1 "positioning data No.1" and axis 2 positioning data set in "condition data No.4.

#### Precautions (注意事項) (4.3 / original p.148)

Positioning data No. executed by simultaneously started axes is set to condition data ("[Da.18] Parameter 1", "[Da.19] Parameter 2"), but the setting value of start axis (the axis which carries out positioning start) should be "0". If the setting value is set to other than "0", the positioning data set in "[Da.18] Parameter 1", "[Da.19] Parameter 2" is given priority to be executed rather than "[Da.12] Start data No.".
For details, refer to the following.
→Page 512 Condition Data

### Repeated start (FOR loop) (繰り返し始動(FORループ)) (4.3 / original p.149)

In a "repeated start (FOR loop)", the data between the "block start data" in which "4: FOR loop" is set in "[Da.13] Special start instruction" and the "block start data" in which "6: NEXT start" is set in "[Da.13] Special start instruction " is repeatedly executed for the number of times set in "[Da.14] Parameter". An endless loop will result if the number of repetitions is set to "0".
(The number of repetitions is set in "[Da.14] Parameter" of the "block start data" in which "4: FOR loop" is set in "[Da.13] Special start instruction".)
The control examples are shown when the "block start data" and "positioning data" are set as shown in the setting examples.

#### Setting examples (設定例) (4.3 / original p.149)

##### Block start data setting example (ブロック始動データの設定例) (4.3 / original p.149)

| Axis 1 block start data | [Da.11] Shape | [Da.12] Start data No. | [Da.13] Special start instruction | [Da.14] Parameter |
|---|---|---|---|---|
| 1st point | 1: Continue | 1 | 4: FOR loop | 2 |
| 2nd point | 1: Continue | 10 | 0: Block start | — |
| 3rd point | 0: End | 50 | 6: NEXT start | — |
| ⋮ | | | | |

The "condition data Nos." have been set in "[Da.14] Parameter".

(As printed in the original. In this example "[Da.14] Parameter" of the FOR loop point is the number of repetitions.)

##### Positioning data setting example (位置決めデータの設定例) (4.3 / original p.149)

| Axis 1 positioning data No. | [Da.1] Operation pattern |
|---|---|
| 1 | 01: Continuous positioning control |
| 2 | 01: Continuous positioning control |
| 3 | 00: Positioning complete |
| ⋮ | |
| 10 | 11: Continuous path control |
| 11 | 00: Positioning complete |
| ⋮ | |
| 50 | 01: Continuous positioning control |
| 51 | 00: Positioning complete |
| ⋮ | |

#### Control examples (制御例) (4.3 / original p.149)

The following shows the control executed when the "block start data" of the 1st point of axis 1 is set as shown in the setting examples and started.
1. Execute the axis 1 "positioning data No.1, 2, 3, 10, 11, 50, and 51".
2. Return to the axis 1 "1st point block start data". Again execute the axis 1 "positioning data No.1, 2, 3, 10, 11, 50 and 51", and then stop the control. (Repeat for the number of times (2 times) set in [Da.14].)

### Repeated start (FOR condition) (繰り返し始動(FOR条件)) (4.3 / original p.150)

In a "repeated start (FOR condition)", the data between the "block start data" in which "5: FOR condition" is set in "[Da.13] Special start instruction" and the "block start data" in which "6: NEXT start" is set in "[Da.13] Special start instruction" is repeatedly executed until the establishment of the conditions set in the "condition data".
Conditional judgment is carried out as soon as switching to the point of "6: NEXT start" (before positioning of NEXT start point).
(The "condition data" designation is set in "[Da.14] Parameter" of the "block start data" in which "5: FOR condition" is set in "[Da.13] Special start instruction".)
The control examples are shown when the "block start data" and "positioning data" are set as shown in the setting examples.

#### Setting examples (設定例) (4.3 / original p.150)

##### Block start data setting example (ブロック始動データの設定例) (4.3 / original p.150)

| Axis 1 block start data | [Da.11] Shape | [Da.12] Start data No. | [Da.13] Special start instruction | [Da.14] Parameter |
|---|---|---|---|---|
| 1st point | 1: Continue | 1 | 5: FOR condition | 5 |
| 2nd point | 1: Continue | 10 | 0: Block start | — |
| 3rd point | 0: End | 50 | 6: NEXT start | — |
| ⋮ | | | | |

The "condition data Nos." have been set in "[Da.14] Parameter".

##### Positioning data setting example (位置決めデータの設定例) (4.3 / original p.150)

| Axis 1 positioning data No. | [Da.1] Operation pattern |
|---|---|
| 1 | 01: Continuous positioning control |
| 2 | 01: Continuous positioning control |
| 3 | 00: Positioning complete |
| ⋮ | |
| 10 | 11: Continuous path control |
| 11 | 00: Positioning complete |
| ⋮ | |
| 50 | 01: Continuous positioning control |
| 51 | 00: Positioning complete |
| ⋮ | |

#### Control examples (制御例) (4.3 / original p.150)

The following shows the control executed when the "block start data" of the 1st point of axis 1 is set as shown in the setting examples and started.
1. Execute the axis 1 "positioning data No.1, 2, 3, 10, and 11".
2. Carry out the conditional judgment set in axis 1 "condition data No.5".*1
   → Conditions not established → Execute "Positioning data No.50, 51". Go to the above 1.
   → Conditions established → Execute "Positioning data No.50, 51" and complete the positioning.

*1 Conditional judgment is carried out as soon as switching to NEXT start point (before positioning of NEXT start point).

### Restrictions when using the NEXT start (NEXT始動使用上の制約事項) (4.3 / original p.151)

The "NEXT start" is an instruction indicating the end of the repetitions when executing the repeated start (FOR loop) and the repeated start (FOR condition).
(→Page 147 Repeated start (FOR loop), →Page 148 Repeated start (FOR condition))
The following shows the restrictions when setting "6: NEXT start" in the "block start data".
- The processing when "6: NEXT start" is set before execution of "4: FOR loop" or "5: FOR condition" is the same as that for a "0: block start".
- Repeated processing will not be carried out if there is no "6: NEXT start" instruction after the "4: FOR loop" or "5: FOR condition" instruction. (Note that an "error" will not occur.)
- Nesting is not possible between "4: FOR loop" and "6: NEXT start", or between "5: FOR condition" and "6: NEXT start". The warning "FOR to NEXT nest construction" (warning code: 09F1H [FX5-SSSC-S], or warning code 0DB1H [FX5-SSC-G]) will occur if nesting is attempted.

(The model name "FX5-SSSC-S" is as printed in the original; it refers to FX5-SSC-S.)

[Operating examples without nesting structure]

| Start block data | [Da.13] Special start instruction |
|---|---|
| 1st point | Normal start |
| 2nd point | FOR |
| 3rd point | Normal start |
| 4th point | NEXT → FOR of the 2nd point |
| 5th point | Normal start |
| 6th point | Normal start |
| 7th point | FOR |
| 8th point | Normal start |
| 9th point | NEXT → FOR of the 7th point |
| ⋮ | |

[Operating examples with nesting structure]

| Start block data | [Da.13] Special start instruction |
|---|---|
| 1st point | Normal start |
| 2nd point | FOR |
| 3rd point | Normal start |
| 4th point | FOR |
| 5th point | Normal start |
| 6th point | Normal start |
| 7th point | NEXT → FOR of the 4th point |
| 8th point | Normal start |
| 9th point | NEXT |
| ⋮ | |

A warning will occur when starting the 4th point "FOR". The JUMP destination of the 7th point "NEXT" is the 4th point. The 9th point "NEXT" is processed as normal start.

## 4.4 Setting the Condition Data (条件データの設定) (4.4 / original p.152-154)

### Relation between various controls and the condition data (各制御と条件データの関係) (4.4 / original p.152)

"Condition data" is set in the following cases.
- When setting conditions during execution of JUMP instruction (major positioning control)
- When setting conditions during execution of "high-level positioning control"

The "condition data" to be set includes the setting items from [Da.15] to [Da.19] and [Da.23] to [Da.26], but the setting requirements and details differ according to the control method and setting conditions.
The following shows the "condition data" "[Da.15] Condition target" corresponding to the different types of control.
(The "condition data" settings in this chapter are assumed to be carried out using the engineering tool.)
◎: One of the setting items must be set.
×: Setting not possible

| Setting item for "[Da.15] Condition target" | High-level positioning control: Block start | High-level positioning control: Wait start | High-level positioning control: Simultaneous start | High-level positioning control: Repeated start (For condition) | Major positioning control: JUMP instruction |
|---|---|---|---|---|---|
| 01H: Monitor data ([Md.140], [Md.141]) | ◎ | ◎ | × | ◎ | ◎ |
| 02H: Control data ([Cd.184], [Cd.190], [Cd.191]) | ◎ | ◎ | × | ◎ | ◎ |
| 03H: Buffer memory (1 word) | ◎ | ◎ | × | ◎ | ◎ |
| 04H: Buffer memory (2 words) | ◎ | ◎ | × | ◎ | ◎ |
| 05H: Positioning data No. | × | × | ◎ | × | × |

*In the original, the header "High-level positioning control" is merged over the 4 columns Block start / Wait start / Simultaneous start / Repeated start (For condition), and "Major positioning control" is over the JUMP instruction column. Expanded into each column header. (The first column of the original reads "Block start", as printed.)

> **Restriction**
> It is recommended that the "condition data" be set whenever possible with the engineering tool. Execution by a program uses many programs and devices. The execution becomes complicated, and the scan times will increase.

### Setting items according to [Da.15] Condition target ("[Da.15]条件対象"に応じた設定項目) (4.4 / original p.153)

(This heading is added for navigation; in the original this text continues without a heading at the top of p.153.)

The setting requirements and details of the following "condition data" [Da.16] to [Da.19] and [Da.23] setting items differ according to the "[Da.15] Condition target" setting.
The following shows the [Da.16] to [Da.19] and [Da.23] setting items corresponding to the "[Da.15] Condition target".
—: Setting not required (Set the initial value or a value within the setting range.)
**: Value stored in buffer memory designated in [Da.17]

| [Da.15] Condition target | [Da.16] Condition operator | [Da.23] Number of simultaneously starting axes | [Da.17] Address | [Da.18] Parameter 1 | [Da.19] Parameter 2 |
|---|---|---|---|---|---|
| 01H: Monitor data ([Md.140], [Md.141]) | 07H: SIG = ON<br>08H: SIG = OFF | — | — | Monitor data: 0H (READY ([Md.140] Module status: b0)), 1H (Synchronization flag ([Md.140] Module status: b1)), 10H to 17H (BUSY axis-1 to axis-8 ([Md.141] BUSY))<br>Control data: 0H (PLC READY ([Cd.190] PLC READY)), 1H (All axis servo ON ([Cd.191] All axis servo ON)), 10H to 17H (Positioning start axis axis-1 to axis-8 ([Cd.184] Positioning start)) | — |
| 02H: Control data ([Cd.184], [Cd.190], [Cd.191]) | 07H: SIG = ON<br>08H: SIG = OFF | — | — | Monitor data: 0H (READY ([Md.140] Module status: b0)), 1H (Synchronization flag ([Md.140] Module status: b1)), 10H to 17H (BUSY axis-1 to axis-8 ([Md.141] BUSY))<br>Control data: 0H (PLC READY ([Cd.190] PLC READY)), 1H (All axis servo ON ([Cd.191] All axis servo ON)), 10H to 17H (Positioning start axis axis-1 to axis-8 ([Cd.184] Positioning start)) | — |
| 03H: Buffer memory (1 word)*1 | 01H: ** = P1<br>02H: ** ≠ P1<br>03H: ** ≤ P1<br>04H: ** ≥ P1<br>05H: P1 ≤ ** ≤ P2<br>06H: ** ≤ P1, P2 ≤ ** | — | Buffer memory address | P1 (numeric value) | P2 (numeric value)<br>(Set only when "[Da.16] Condition operator" is [05H] or [06H].) |
| 04H: Buffer memory (2 words)*1 | 01H: ** = P1<br>02H: ** ≠ P1<br>03H: ** ≤ P1<br>04H: ** ≥ P1<br>05H: P1 ≤ ** ≤ P2<br>06H: ** ≤ P1, P2 ≤ ** | — | Buffer memory address | P1 (numeric value) | P2 (numeric value)<br>(Set only when "[Da.16] Condition operator" is [05H] or [06H].) |
| 05H: Positioning data No. | Setting not possible | 2 | — | Low-order 16 bits: "[Da.24] Simultaneously starting axis No.1" positioning data No.<br>High-order 16 bits: "[Da.25] Simultaneously starting axis No.2" positioning data No. | — |
| 05H: Positioning data No. | Setting not possible | 3 | — | Low-order 16 bits: "[Da.24] Simultaneously starting axis No.1" positioning data No.<br>High-order 16 bits: "[Da.25] Simultaneously starting axis No.2" positioning data No. | — |
| 05H: Positioning data No. | Setting not possible | 4 | — | Low-order 16 bits: "[Da.24] Simultaneously starting axis No.1" positioning data No.<br>High-order 16 bits: "[Da.25] Simultaneously starting axis No.2" positioning data No. | Low-order 16 bits: "[Da.26] Simultaneously starting axis No.3" positioning data No.<br>High-order 16 bits: Unusable (Set "0".) |

*In the original: for 01H/02H, [Da.16], [Da.17] "—", [Da.18] and [Da.19] "—" are merged over the 2 rows; for 03H/04H, [Da.16], [Da.17], [Da.18] and [Da.19] are merged over the 2 rows; [Da.23] "—" is one cell merged over 01H to 04H (4 rows); for 05H (3 rows by [Da.23] = 2 / 3 / 4), [Da.15], [Da.16], [Da.17] "—" and [Da.18] are merged over the 3 rows, and [Da.19] "—" is merged over the rows [Da.23] = 2 and 3. Expanded to each row.

*1 Comparison of ≤ and ≥ is judged as signed values. (→Page 515 [Da.16] Condition operator)

### Judgment whether the condition operator is "=" or "≠" at the start of wait. (ウェイト始動時，条件演算子「＝」と「≠」の判定) (4.4 / original p.153)

Judgment on data is carried out for each operation cycle of the Simple Motion module/Motion module. Thus, in the judgment on the data such as command position value which varies continuously, the operator "=" may not be detected. If this occurs, use a range operator.

### Condition data setting examples (条件データの設定例) (4.4 / original p.154)

The following shows the setting examples for "condition data".

#### Setting the monitor data ON/OFF as a condition (モニタデータのON/OFFを条件として設定する場合) (4.4 / original p.154)

[Condition]
The monitor data "[Md.141] BUSY" (Axis 1) is OFF

| [Da.15] Condition target | [Da.16] Condition operator | [Da.17] Address | [Da.18] Parameter 1 | [Da.19] Parameter 2 | [Da.23] Number of simultaneously starting axes | [Da.24] Simultaneously starting axis No.1 | [Da.25] Simultaneously starting axis No.2 | [Da.26] Simultaneously starting axis No.3 |
|---|---|---|---|---|---|---|---|---|
| 01H: Monitor data ([Md.140], [Md.141]) | 08H: SIG = OFF | — | 10H | — | — | — | — | — |

#### Setting the numeric value stored in the "buffer memory" as a condition (「バッファメモリ」に格納された数値を条件として設定する場合) (4.4 / original p.154)

[Condition]
The value stored in buffer memory addresses "2400, 2401" ([Md.20] Command position value) is "1000" or larger.

| [Da.15] Condition target | [Da.16] Condition operator | [Da.17] Address | [Da.18] Parameter 1 | [Da.19] Parameter 2 | [Da.23] Number of simultaneously starting axes | [Da.24] Simultaneously starting axis No.1 | [Da.25] Simultaneously starting axis No.2 | [Da.26] Simultaneously starting axis No.3 |
|---|---|---|---|---|---|---|---|---|
| 04H: Buffer memory (2 words) | 04H: ** ≥ P1 | 2400 | 1000 | — | — | — | — | — |

#### Designating the axis and positioning data No.*1 (「同時始動」で同時に始動する軸と位置決めデータNo.を指定する場合) (4.4 / original p.154)

*1 The axis and positioning data No. are to be simultaneously started in "simultaneous start".

[Condition]
Simultaneously starting "axis 2 positioning data No.3"

| [Da.15] Condition target | [Da.16] Condition operator | [Da.17] Address | [Da.18] Parameter 1 | [Da.19] Parameter 2 | [Da.23] Number of simultaneously starting axes | [Da.24] Simultaneously starting axis No.1 | [Da.25] Simultaneously starting axis No.2 | [Da.26] Simultaneously starting axis No.3 |
|---|---|---|---|---|---|---|---|---|
| 05H: Positioning data No. | — | — | Low-order 16 bits "0003H" | — | 2H: 2 axes | 1H: Axis 2 | 0H | 0H |

## 4.5 Start Program for High-level Positioning Control (高度な位置決め制御の始動プログラム) (4.5 / original p.155-158)

### Starting high-level positioning control (高度な位置決め制御の始動) (4.5 / original p.155)

To execute high-level positioning control, a program must be created to start the control in the same method as for major positioning control.
The following shows the procedure for starting the "1st point block start data" (regarded as block No.7000) set in axis 1.

[Figure] Start procedure of high-level positioning control (original p.155)
- CPU module → Simple Motion module/Motion module (Buffer memory / Input/output signal) → Servo amplifier
- 1. 7000 → Buffer memory "[Cd.3] Positioning start No."
- 2. 1 → Buffer memory "[Cd.4] Positioning starting point No."
- 3. ON → Input/output signal "[Cd.184] Positioning start"
- 4. Control by designated positioning data (Simple Motion module/Motion module → Servo amplifier)

> **Point**
> When carrying out a positioning start with the next scan after a positioning operation is completed, turn the "[Cd.184] Positioning start" OFF and input the start complete signal ([Md.31] Status: b14) as an interlock condition to start after the start complete signal ([Md.31] Status: b14) is turned OFF.

1. Set "7000" in "[Cd.3] Positioning start No.".
   (This establishes that the control as "high-level positioning control" using block start data.)
2. Set the point No. of the "block start data" to be started. (In this case "1".)
3. Turn ON the start signal.
4. The positioning data set in the "1st point block start data" is started.

### Example of a start program for high-level positioning control (高度な位置決め制御の始動プログラム例) (4.5 / original p.156-158)

The following shows an example of a start program for high-level positioning control in which the 1st point "block start data" of axis 1 is started. (The block No. is regarded as "7000".)

#### Control data that require setting (設定の必要な制御データ) (4.5 / original p.156)

The following control data must be set to execute high-level positioning control. The setting is carried out using a program.
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.3] | Positioning start No. | 7000 | Set "7000" to indicate control using "block start data". | 4300+100n |
| [Cd.4] | Positioning starting point No. | 1 | Set the point No. of the "block start data" to be started. | 4301+100n |

Refer to the following for details on the setting details.
→Page 561 Control Data

#### Start conditions (始動条件) (4.5 / original p.156)

The following conditions must be fulfilled when starting the control. The required conditions must also be integrated into the program, and configured so the control does not start unless the conditions are fulfilled.

| Signal name | | Signal state | | Device |
|---|---|---|---|---|
| Interface signal | PLC READY signal | ON | CPU module preparation completed | [Cd.190] PLC READY |
| Interface signal | READY signal | ON | Preparation completed | [Md.140] Module status: b0 |
| Interface signal | All axis servo ON | ON | All axis servo ON | [Cd.191] All axis servo ON |
| Interface signal | Synchronization flag | ON | The buffer memory can be accessed. | [Md.140] Module status: b1 |
| Interface signal | Axis stop signal | OFF | Axis stop signal is OFF | [Cd.180] Axis stop |
| Interface signal | Start complete signal | OFF | Start complete signal is OFF | [Md.31] Status: b14 |
| Interface signal | BUSY signal | OFF | BUSY signal is OFF | [Md.141] BUSY |
| Interface signal | Error detection signal | OFF | There is no error | [Md.31] Status: b13 |
| Interface signal | M code ON signal | OFF | M code ON signal is OFF | [Md.31] Status: b12 |
| External signal | Forced stop input signal | ON | There is no forced stop input | — |
| External signal | Stop signal | OFF | Stop signal is OFF | — |
| External signal | Upper limit (FLS) | ON | Within limit range | — |
| External signal | Lower limit (RLS) | ON | Within limit range | — |

*In the original, "Interface signal" is merged over 9 rows and "External signal" over 4 rows. Expanded to each row.

#### Start time chart (始動用タイムチャート) (4.5 / original p.157)

The following chart shows a time chart in which the positioning data No.1, 2, 10, 11, and 12 of the axis 1 are continuously executed as an example.

##### Block start data setting example (ブロック始動データの設定例) (4.5 / original p.157)

| Axis 1 block start data | [Da.11] Shape | [Da.12] Start data No. | [Da.13] Special start instruction | [Da.14] Parameter |
|---|---|---|---|---|
| 1st point | 1: Continue | 1 | 0: Block start | — |
| 2nd point | 0: End | 10 | 0: Block start | — |
| ⋮ | | | | |

##### Positioning data setting example (位置決めデータの設定例) (4.5 / original p.157)

| Axis 1 positioning data No. | [Da.1] Operation pattern |
|---|---|
| 1 | 11: Continuous path control |
| 2 | 00: Positioning complete |
| ⋮ | |
| 10 | 11: Continuous path control |
| 11 | 11: Continuous path control |
| 12 | 00: Positioning complete |
| ⋮ | |

##### Start time chart (始動タイムチャート) (4.5 / original p.157)

Ex.

[Figure] Start time chart (original p.157)
- Speed waveform (V-t), notation "Positioning data No.(Operation pattern)": 1(11) accelerates and runs, passes into 2(00) at a lower speed without stopping, 2(00) decelerates to stop → Dwell time → 10(11) → 11(11) (a break mark is drawn during 10(11)) → 12(00) decelerates to stop → Dwell time.
- [Cd.190] PLC READY turns ON first, then [Cd.191] All axis servo ON turns ON, then the READY signal turns ON (arrows show this order); all three stay ON afterwards. (The READY signal is labeled "READY signal ([Md.141] Module status: b0)" in the original figure, as printed; the start condition table gives the device as [Md.140] Module status: b0.)
- [Cd.3] Positioning start No. = 7000 and [Cd.4] Positioning starting point No. = 1 are set before [Cd.184] turns ON (value change marks before the start).
- 1st point [buffer memory address 22000] = -32767(8001H); 2nd point [buffer memory address 22001] = 10(000AH). Both are shown valid from before the start until after the end (value change marks after the end).
- [Cd.184] Positioning start OFF → ON; following it, the start complete signal ([Md.31] Status: b14) and [Md.141] BUSY turn ON and the positioning starts.
- Positioning complete signal ([Md.31] Status: b15): short ON pulses at the dashed lines at the 1(11) → 2(00) switching, at the end of the dwell time after 2(00) (start of 10(11)), at the 11(11) → 12(00) switching, and after the dwell time of 12(00) (following [Md.141] BUSY OFF).
- At the end of the dwell time of 12(00), [Md.141] BUSY turns OFF; then [Cd.184] Positioning start turns OFF, and following it the start complete signal (b14) turns OFF.
- Error detection signal ([Md.31] Status: b13): OFF throughout.

#### Program example (プログラム例) (4.5 / original p.158)

Note in the figure: "Set the block start data beforehand."

(Transcribed from the GX Works3 ladder. The number in parentheses is the step No. The comment after `//` is the comment shown in the ladder; the device in parentheses is the assigned device shown under the label.)

```
(0)
LD   bInputPositioningStartReq                                      // Positioning start command
PLS  bPositioningStartReq_P                                         // Positioning start command pulse

(5)
LD   bPositioningStartReq_P                                         // Positioning start command pulse
ANI  FX5SSC_1.stSysMntr2_D.bnBusy_D[0]                (U1\G31501.0) // R:BUSY(Axis 1 to 8)(Direct)
ANI  FX5SSC_1.stnAxMntr_D[0].uStatus_D.E              (U1\G2417.E)  // R:Status(Direct)
MOV  K7000 FX5SSC_1.stnAxCtrl1_D[0].uPositioningStartNo_D          (U1\G4300)    // RW:Positioning start No.(Direct)
MOV  K1    FX5SSC_1.stnAxCtrl1_D[0].uPositioningStartingPointNo_D  (U1\G4301)    // RW:Positioning starting point No.(Direct)
SET  FX5SSC_1.stnAxCtrl2_D[0].uPositioningStart_D.0                (U1\G30104.0) // RW:Positioning start(Direct)

(28)
LD   FX5SSC_1.stnAxCtrl2_D[0].uPositioningStart_D.0   (U1\G30104.0) // RW:Positioning start(Direct)
LD   FX5SSC_1.stnAxMntr_D[0].uStatus_D.E              (U1\G2417.E)  // R:Status(Direct)
OR   FX5SSC_1.stnAxMntr_D[0].uStatus_D.D              (U1\G2417.D)  // R:Status(Direct)
ANB
ANI  FX5SSC_1.stSysMntr2_D.bnBusy_D[0]                (U1\G31501.0) // R:BUSY(Axis 1 to 8)(Direct)
RST  FX5SSC_1.stnAxCtrl2_D[0].uPositioningStart_D.0   (U1\G30104.0) // RW:Positioning start(Direct)
```

- Step (5): the 3 instructions MOV, MOV, SET are parallel outputs under the same condition.
- Step (0): bInputPositioningStartReq is an a-contact. Step (5): bnBusy_D[0] and uStatus_D.E are b-contacts (NC). Step (28): uPositioningStart_D.0 (a-contact) in series with the parallel of uStatus_D.E (a-contact) and uStatus_D.D (a-contact), then bnBusy_D[0] (b-contact). Contact types read from the ladder image.
- No END instruction or final step No. is shown in the original.

| Classification | Label name | Description |
|---|---|---|
| Module label | FX5SSC_1.stSysMntr2_D.bnBusy_D[0] | Axis 1 BUSY signal |
| Module label | FX5SSC_1.stnAxMntr_D[0].uStatus_D.E | Axis 1 Start complete |
| Module label | FX5SSC_1.stnAxCtrl1_D[0].uPositioningStartNo_D | Axis 1 Positioning start No. |
| Module label | FX5SSC_1.stnAxCtrl1_D[0].uPositioningStartingPointNo_D | Axis 1 Positioning starting point No. |
| Module label | FX5SSC_1.stnAxCtrl2_D[0].uPositioningStart_D.0 | Axis 1 Positioning start signal |
| Global label, local label | (below) | Defines the global label or the local label as follows. The settings of Assign (Device/Label) are not required for the label that the assignment device is not set because the unused internal relay and data device are automatically assigned.<br>The following are for local labels. |

*In the original, "Module label" (classification column) is merged over 5 rows. Expanded to each row. FX5SSC_1.stnAxMntr_D[0].uStatus_D.D (U1\G2417.D), used in step (28), is not listed in the label table of the original (as printed).

Local label definition (from the GX Works3 label setting screen in the original):

| No. | Label Name | Data Type | Class |
|---|---|---|---|
| 1 | bInputPositioningStartReq | Bit | VAR |
| 2 | bPositioningStartReq_P | Bit | VAR |
| 3 | | | |
