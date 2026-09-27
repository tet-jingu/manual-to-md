# 10 PARAMETER SETTINGS (パラメータ設定) (Chapter 10 / original p.391-399)

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

## Conversion range (変換範囲表 / original p.391-399)

| Original page | Section | Handling |
|---|---|---|
| p.391 | 10 PARAMETER SETTINGS (chapter intro), 10.1 Parameter Setting Procedure | Full text |
| p.392-398 | 10.2 Module Parameters (refresh setting: module label, device, setting item [FX5-SSC-S]/[FX5-SSC-G], refresh group) | Full text |
| p.399 | 10.3 Simple Motion Module Setting | Full text |

## Table of Contents (目次)

- 10 PARAMETER SETTINGS (パラメータ設定)
- 10.1 Parameter Setting Procedure (パラメータ設定手順)
- 10.2 Module Parameters (ユニットパラメータ)
- 10.3 Simple Motion Module Setting (シンプルモーションユニット設定)

---

## 10 PARAMETER SETTINGS (パラメータ設定) (Chapter 10 / original p.391)

This chapter describes the parameter setting of the Simple Motion module/Motion module. By setting parameters, the parameter setting by program is not needed.
The module parameter and Simple Motion module setting are included in the parameter settings.

## 10.1 Parameter Setting Procedure (パラメータ設定手順) (10.1 / original p.391)

1. Add the Simple Motion module/Motion module in the engineering tool.
   - Operation: Navigation window ⇨ "Parameter" ⇨ "Module Information" ⇨ Right-click ⇨ [Add New Module]
2. The module parameter and Simple Motion module setting are included in the parameter settings. Select one of the settings from the tree on the following window.
   - Operation: Navigation window ⇨ "Parameter" ⇨ "Module Information" ⇨ Target module
3. Write the settings to the CPU module using the engineering tool.
   - Operation: [Online] ⇨ [Write to PLC]
4. The settings are reflected by resetting the CPU module or powering off and on the system.

("Operation:" is the operation-procedure line marked with the mouse icon in the original.)

## 10.2 Module Parameters (ユニットパラメータ) (10.2 / original p.392-398)

Set the module parameter. The module parameter has the following settings.

[FX5-SSC-S]
- Refresh settings

[FX5-SSC-G]

Module parameter (Motion)
- Refresh settings

Module Parameter (Network)*1
- Required settings
- Basic settings
- Application settings

*1 For details, refer to the following.
[Other manual] MELSEC iQ-F FX5 Motion Module User's Manual (CC-Link IE TSN)

Select the module parameter from the tree on the following window.
- Operation: Navigation window ⇨ "Parameter" ⇨ "Module Information" ⇨ Target module ⇨ "Module Parameter"

### Refresh setting (リフレッシュ設定) (10.2 / original p.392)

Set the setting to transfer the values of the Simple Motion module/Motion module to devices or module labels of the CPU module. By configuring these refresh settings, reading the data by program is not needed.
Select the transfer destination from the following at "Target".
- Module Label (→Page 390 Module Label)
- Specify Device (→Page 390 Device)

#### Module Label (ユニットラベル) (10.2 / original p.392)

Transfer the setting of the buffer memory to the corresponding module label of each buffer memory area. Items of all axes are automatically set to "Enable" by setting "Command position value" of the axis 1 to "Enable".

#### Device (指定デバイス) (10.2 / original p.392)

Transfer the setting of the buffer memory to the specified device of the CPU module. The device X, Y, M, L, B, D, W, R, ZR, and RD can be specified. To use the bit device X, Y, M, L, or B, set a No. which is divisible by 16 points (example: X10, Y120, M16). The data in the buffer memory is stored in devices for 16 points from the set No.

Ex.
When X10 is set, data is stored in X10 to X1F.

#### Setting item (設定項目) (10.2 / original p.393-398)

The refresh setting has the following items.

##### Setting item [FX5-SSC-S] (設定項目[FX5-SSC-S]) (10.2 / original p.393-395)

[Figure] FX5-40SSC-S Module Parameter window (refresh setting) (original p.393)
- Window title: "2[U2]:FX5-40SSC-S Module Parameter"
- Left pane "Setting Item List": search box "Input the Setting Item", tree item "Refresh setting". Bottom tabs "Item List" / "Find Result"
- Right pane "Setting Item": Target "Device" (grayed-out pull-down); top right "Number of transfers to intelligent function module 0", "Number of transfers to CPU 0"
- Table columns: Item / AXIS1 / AXIS2 / AXIS3 / AXIS4
- Tree: "Refresh at the set timing" ⊟ "Transfer to the CPU." (row text: "Transfer the buffer memory data to the specified device.") → Current feed value, Machine feed value, Feedrate, Axis error No., Axis warning No., Valid M code, Axis operation status, Current speed, Axis feedrate, Speed-position switching control positioning amount, External input signal, Status, Target value, Target speed, Movement amount after proximity dog ON, Torque limit stored value/forward torque limit stored value, Special start data instruction code setting value, Special start data instruction parameter setting value, Start positioning data No. setting value, In speed limit flag (list continues beyond the visible area)
- Note: some item names in the screenshot (e.g. "Current feed value", "Feedrate", "Axis feedrate") differ from the names in the table below (the table names are as printed in the manual text).
- Bottom: "Explanation" field (empty), buttons "Check" and "Restore the Default Settings"

| Item (level 1) | Item (level 2) | Item | Reference |
|---|---|---|---|
| Refresh at the set timing | Transfer to the CPU | Command position value | Page 527 [Md.20] Command position value |
| Refresh at the set timing | Transfer to the CPU | Machine feed value | Page 528 [Md.21] Machine feed value |
| Refresh at the set timing | Transfer to the CPU | Speed command | Page 529 [Md.22] Speed command |
| Refresh at the set timing | Transfer to the CPU | Axis error No. | Page 529 [Md.23] Axis error No. |
| Refresh at the set timing | Transfer to the CPU | Axis warning No. | Page 530 [Md.24] Axis warning No. |
| Refresh at the set timing | Transfer to the CPU | Valid M code | Page 530 [Md.25] Valid M code |
| Refresh at the set timing | Transfer to the CPU | Axis operation status | Page 530 [Md.26] Axis operation status |
| Refresh at the set timing | Transfer to the CPU | Current speed | Page 531 [Md.27] Current speed |
| Refresh at the set timing | Transfer to the CPU | Axis peed command | Page 532 [Md.28] Axis speed command |
| Refresh at the set timing | Transfer to the CPU | Speed-position switching control positioning movement amount | Page 533 [Md.29] Speed-position switching control positioning movement amount |
| Refresh at the set timing | Transfer to the CPU | External input signal | Page 534 [Md.30] External input signal |
| Refresh at the set timing | Transfer to the CPU | Status | Page 535 [Md.31] Status |
| Refresh at the set timing | Transfer to the CPU | Target value | Page 536 [Md.32] Target value |
| Refresh at the set timing | Transfer to the CPU | Target speed | Page 537 [Md.33] Target speed |
| Refresh at the set timing | Transfer to the CPU | Movement amount after proximity dog ON | Page 538 [Md.34] Movement amount after proximity dog ON [FX5-SSC-S] |
| Refresh at the set timing | Transfer to the CPU | Torque limit stored value/forward torque limit stored value | Page 539 [Md.35] Torque limit stored value/forward torque limit stored value |
| Refresh at the set timing | Transfer to the CPU | Special start data instruction code setting value | Page 539 [Md.36] Special start data instruction code setting value |
| Refresh at the set timing | Transfer to the CPU | Special start data instruction parameter setting value | Page 540 [Md.37] Special start data instruction parameter setting value |
| Refresh at the set timing | Transfer to the CPU | Start positioning data No. setting value | Page 540 [Md.38] Start positioning data No. setting value |
| Refresh at the set timing | Transfer to the CPU | In speed limit flag | Page 540 [Md.39] In speed limit flag |
| Refresh at the set timing | Transfer to the CPU | In speed change processing flag | Page 540 [Md.40] In speed change processing flag |
| Refresh at the set timing | Transfer to the CPU | Special start repetition counter | Page 541 [Md.41] Special start repetition counter |
| Refresh at the set timing | Transfer to the CPU | Control system repetition counter | Page 541 [Md.42] Control system repetition counter |
| Refresh at the set timing | Transfer to the CPU | Start data pointer being executed | Page 541 [Md.43] Start data pointer being executed |
| Refresh at the set timing | Transfer to the CPU | Positioning data No. being executed | Page 541 [Md.44] Positioning data No. being executed |
| Refresh at the set timing | Transfer to the CPU | Block No. being executed | Page 541 [Md.45] Block No. being executed |
| Refresh at the set timing | Transfer to the CPU | Last executed positioning data No. | Page 542 [Md.46] Last executed positioning data No. |
| Refresh at the set timing | Transfer to the CPU | Positioning data being executed (Positioning identifier) | Page 542 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to the CPU | Positioning data being executed (M code) | Page 542 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to the CPU | Positioning data being executed (Dwell time) | Page 542 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to the CPU | Positioning data being executed (Command speed) | Page 542 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to the CPU | Positioning data being executed (Positioning address) | Page 542 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to the CPU | Positioning data being executed (Arc address) | Page 542 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to the CPU | Home position return re-travel value | Page 544 [Md.100] Home position return re-travel value [FX5-SSC-S] |
| Refresh at the set timing | Transfer to the CPU | Actual position value | Page 545 [Md.101] Actual position value |
| Refresh at the set timing | Transfer to the CPU | Deviation counter value | Page 546 [Md.102] Deviation counter value |
| Refresh at the set timing | Transfer to the CPU | Motor rotation speed | Page 547 [Md.103] Motor rotation speed |
| Refresh at the set timing | Transfer to the CPU | Motor current value | Page 547 [Md.104] Motor current value |
| Refresh at the set timing | Transfer to the CPU | Servo status3 | Page 557 [Md.125] Servo status3 |
| Refresh at the set timing | Transfer to the CPU | Servo status5 | Page 558 [Md.127] Servo status5 [FX5-SSC-S] |
| Refresh at the set timing | Transfer to the CPU | Servo amplifier software No.1 | Page 548 [Md.106] Servo amplifier software No. [FX5-SSC-S] |
| Refresh at the set timing | Transfer to the CPU (axis monitor) | Servo amplifier software No.2 | Page 548 [Md.106] Servo amplifier software No. [FX5-SSC-S] |
| Refresh at the set timing | Transfer to the CPU (axis monitor) | Servo amplifier software No.3 | Page 548 [Md.106] Servo amplifier software No. [FX5-SSC-S] |
| Refresh at the set timing | Transfer to the CPU (axis monitor) | Servo amplifier software No.4 | Page 548 [Md.106] Servo amplifier software No. [FX5-SSC-S] |
| Refresh at the set timing | Transfer to the CPU (axis monitor) | Servo amplifier software No.5 | Page 548 [Md.106] Servo amplifier software No. [FX5-SSC-S] |
| Refresh at the set timing | Transfer to the CPU (axis monitor) | Servo amplifier software No.6 | Page 548 [Md.106] Servo amplifier software No. [FX5-SSC-S] |
| Refresh at the set timing | Transfer to the CPU (axis monitor) | Parameter error No. | Page 549 [Md.107] Parameter error No. [FX5-SSC-S] |
| Refresh at the set timing | Transfer to the CPU (axis monitor) | Servo status2 | Page 555 [Md.119] Servo status2 |
| Refresh at the set timing | Transfer to the CPU (axis monitor) | Servo status1 | Page 550 [Md.108] Servo status1 |
| Refresh at the set timing | Transfer to the CPU (axis monitor) | Regenerative load ratio/Optional data monitor output 1 | Page 551 [Md.109] Regenerative load ratio/Optional data monitor output 1 |
| Refresh at the set timing | Transfer to the CPU (axis monitor) | Effective load torque/Optional data monitor output 2 | Page 551 [Md.110] Effective load torque/Optional data monitor output 2 |
| Refresh at the set timing | Transfer to the CPU (axis monitor) | Peak torque ratio/Optional data monitor output 3 | Page 551 [Md.111] Peak torque ratio/Optional data monitor output 3 |
| Refresh at the set timing | Transfer to the CPU (axis monitor) | Optional data monitor output 4 | Page 552 [Md.112] Optional data monitor output 4 |
| Refresh at the set timing | Transfer to the CPU (axis monitor) | Semi/Fully closed loop status | Page 552 [Md.113] Semi/Fully closed loop status |
| Refresh at the set timing | Transfer to the CPU (axis monitor) | Servo alarm | Page 553 [Md.114] Servo alarm |
| Refresh at the set timing | Transfer to the CPU (axis monitor) | Encoder option information | Page 554 [Md.116] Encoder option information |
| Refresh at the set timing | Transfer to the CPU (axis monitor) | Reverse torque limit stored value | Page 556 [Md.120] Reverse torque limit stored value |
| Refresh at the set timing | Transfer to the CPU (axis monitor) | Speed during command | Page 556 [Md.122] Speed during command |
| Refresh at the set timing | Transfer to the CPU (axis monitor) | Torque during command | Page 557 [Md.123] Torque during command |
| Refresh at the set timing | Transfer to the CPU (axis monitor) | Control mode switching status | Page 557 [Md.124] Control mode switching status |
| Refresh at the set timing | Transfer to the CPU (axis monitor) | Positioning data being executed (Axis to be interpolated) | Page 542 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to the CPU (axis monitor) | Deceleration start flag | Page 542 [Md.48] Deceleration start flag |
| Refresh at the set timing | Transfer to the CPU | Command Generation Axis_Command position value | Page 527 [Md.20] Command position value |
| Refresh at the set timing | Transfer to the CPU | Command Generation Axis_speed command | Page 529 [Md.22] Speed command |
| Refresh at the set timing | Transfer to the CPU | Command Generation Axis_Axis error No. | Page 529 [Md.23] Axis error No. |
| Refresh at the set timing | Transfer to the CPU | Command Generation Axis_Axis warning No | Page 530 [Md.24] Axis warning No. |
| Refresh at the set timing | Transfer to the CPU | Command Generation Axis_Valid M code | Page 530 [Md.25] Valid M code |
| Refresh at the set timing | Transfer to the CPU | Command Generation Axis_Axis operation status | Page 530 [Md.26] Axis operation status |
| Refresh at the set timing | Transfer to the CPU | Command Generation Axis_Current speed | Page 531 [Md.27] Current speed |
| Refresh at the set timing | Transfer to the CPU | Command Generation Axis_Axis speed command | Page 532 [Md.28] Axis speed command |
| Refresh at the set timing | Transfer to the CPU | Command Generation Axis_Speed-position switching control positioning movement amount | Page 533 [Md.29] Speed-position switching control positioning movement amount |
| Refresh at the set timing | Transfer to the CPU | Command Generation Axis_Status | Page 535 [Md.31] Status |
| Refresh at the set timing | Transfer to the CPU | Command Generation Axis_Target value | Page 536 [Md.32] Target value |
| Refresh at the set timing | Transfer to the CPU | Command Generation Axis_Target speed | Page 537 [Md.33] Target speed |
| Refresh at the set timing | Transfer to the CPU | Command Generation Axis_Start positioning data No. setting value | Page 540 [Md.38] Start positioning data No. setting value |
| Refresh at the set timing | Transfer to the CPU | Command Generation Axis_In speed limit flag | Page 540 [Md.39] In speed limit flag |
| Refresh at the set timing | Transfer to the CPU | Command Generation Axis_In speed change processing flag | Page 540 [Md.40] In speed change processing flag |
| Refresh at the set timing | Transfer to the CPU | Command Generation Axis_Control system repetition counter | Page 541 [Md.42] Control system repetition counter |
| Refresh at the set timing | Transfer to the CPU | Command Generation Axis_Positioning data No. being executed | Page 541 [Md.44] Positioning data No. being executed |
| Refresh at the set timing | Transfer to the CPU | Command Generation Axis_Last executed positioning data No. | Page 542 [Md.46] Last executed positioning data No. |
| Refresh at the set timing | Transfer to the CPU | Command Generation Axis_Positioning data being executed : Positioning identifier | Page 542 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to the CPU | Command Generation Axis_Positioning data being executed : M code | Page 542 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to the CPU | Command Generation Axis_Positioning data being executed : Dwell time | Page 542 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to the CPU | Command Generation Axis_Positioning data being executed : Command speed | Page 542 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to the CPU | Command Generation Axis_Positioning data being executed : Positioning address | Page 542 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to the CPU | Command Generation Axis_Speed during command | Page 556 [Md.122] Speed during command |
| Refresh at the set timing | Transfer to the CPU | Command Generation Axis_Deceleration start flag | Page 542 [Md.48] Deceleration start flag |
| Refresh at the set timing | Transfer to the CPU | Command Generation Axis Accumulative Position Value | For details, refer to the following manual, command generation axis.<br>[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Advanced Synchronous Control) |
| Refresh at the set timing | Transfer to the CPU | Command Generation Axis Position Value per Cycle | For details, refer to the following manual, command generation axis.<br>[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Advanced Synchronous Control) |
| Refresh at the set timing | Transfer to the CPU | Command Generation Axis Busy | For details, refer to the following manual, command generation axis.<br>[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Advanced Synchronous Control) |
| Refresh Timing | Refresh Timing | Refresh Timing | Page 396 Refresh group |
| Refresh Timing | Refresh Timing | Refresh Group [n] (n: 1-64) | Page 396 Refresh group |
| Refresh Timing (I/O)*1 | Refresh Timing (I/O)*1 | Refresh Timing | — |

*In the original, the Item column has 3 levels (level 1 / level 2 / item) with merged cells. "Refresh at the set timing" (level 1) and each "Transfer to the CPU..." (level 2) are merged vertically over all their rows; "Refresh Timing" (level 1-2) is merged over 2 rows; "Refresh Timing (I/O)*1" is one cell. Here level 1 and level 2 are both filled with the same word for "Refresh Timing" and "Refresh Timing (I/O)*1". The Reference cells "Page 542 [Md.47] Positioning data being executed" (for the Positioning data being executed rows), "Page 548 [Md.106] Servo amplifier software No. [FX5-SSC-S]" (Servo amplifier software No.1 to No.6, spanning the level-2 boundary), "For details, refer to the following manual, command generation axis. ..." (Accumulative Position Value / Position Value per Cycle / Busy) and "Page 396 Refresh group" (2 rows) are also merged cells. Expanded to each row. Page numbers in the Reference column are the original (printed) pages. The table spans original p.393-395; the level-2 group "Transfer to the CPU" that starts at "Command Generation Axis_Command position value" is a separate cell from the first "Transfer to the CPU" group. "Servo amplifier software No.1" belongs to the "Transfer to the CPU" group and No.2 to No.6 to the "Transfer to the CPU (axis monitor)" group, as printed.
*"Axis peed command" (row on original p.393) is printed as-is in the original (typo for "Axis speed command"; the Reference column reads "[Md.28] Axis speed command"). "Command Generation Axis_speed command" (lower-case "s") and "Command Generation Axis_Axis warning No" (no period) are also as printed.

*1 The setting cannot be changed from the default in the Motion module.

##### Setting item [FX5-SSC-G] (設定項目[FX5-SSC-G]) (10.2 / original p.396-398)

[Figure] FX5-40SSC-G(S) Module Parameter window (refresh setting) (original p.396)
- Window title: "1[U1]:FX5-40SSC-G(S) Module Parameter"
- Left pane "Setting Item List": search box "Input the Setting Item", tree item "Refresh setting". Bottom tabs "Item List" / "Find Result"
- Right pane "Setting Item": Target "Device" (grayed-out pull-down); top right "Number of transfers to intelligent function module 0", "Number of transfers to CPU 0"
- Table columns: Item / AXIS1 / AXIS2 / AXIS3 / AXIS4
- Tree: "Refresh at the set timing" ⊟ "Transfer to the CPU (Axis monitor 1)" → Command position value, Machine feed value, Speed command, Axis error No., Axis warning No., Valid M code, Axis operation status, Current speed, Axis speed command, Speed-position switching control positioning movement amount, External input signal, Status, Target value, Target speed, Amount of the manual pulser driving carrying over movement, Torque limit stored value/forward torque limit stored value, Special start data instruction code setting value, Special start data instruction parameter setting value, Start positioning data No. setting value, In speed limit flag (list continues beyond the visible area)
- Bottom: "Explanation" field (empty), buttons "Check" and "Restore the Default Settings"

| Item (level 1) | Item (level 2) | Item | Reference |
|---|---|---|---|
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Command position value | Page 527 [Md.20] Command position value |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Machine feed value | Page 528 [Md.21] Machine feed value |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Speed command | Page 529 [Md.22] Speed command |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Axis error No. | Page 529 [Md.23] Axis error No. |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Axis warning No. | Page 530 [Md.24] Axis warning No. |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Valid M code | Page 530 [Md.25] Valid M code |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Axis operation status | Page 530 [Md.26] Axis operation status |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Current speed | Page 531 [Md.27] Current speed |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Axis speed command | Page 532 [Md.28] Axis speed command |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Speed-position switching control positioning movement amount | Page 533 [Md.29] Speed-position switching control positioning movement amount |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | External input signal | Page 534 [Md.30] External input signal |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Status | Page 535 [Md.31] Status |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Target value | Page 536 [Md.32] Target value |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Target speed | Page 537 [Md.33] Target speed |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Amount of the manual pulser driving carrying over movement | Page 543 [Md.62] Amount of the manual pulser driving carrying over movement [FX5-SSC-G] |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Torque limit stored value/forward torque limit stored value | Page 539 [Md.35] Torque limit stored value/forward torque limit stored value |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Special start data instruction code setting value | Page 539 [Md.36] Special start data instruction code setting value |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Special start data instruction parameter setting value | Page 540 [Md.37] Special start data instruction parameter setting value |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Start positioning data No. setting value | Page 540 [Md.38] Start positioning data No. setting value |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | In speed limit flag | Page 540 [Md.39] In speed limit flag |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | In speed change processing flag | Page 540 [Md.40] In speed change processing flag |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Special start repetition counter | Page 541 [Md.41] Special start repetition counter |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Control system repetition counter | Page 541 [Md.42] Control system repetition counter |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Start data pointer being executed | Page 541 [Md.43] Start data pointer being executed |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Positioning data No. being executed | Page 541 [Md.44] Positioning data No. being executed |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Block No. being executed | Page 541 [Md.45] Block No. being executed |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Last executed positioning data No. | Page 542 [Md.46] Last executed positioning data No. |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Positioning data being executed (Positioning identifier) | Page 542 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Positioning data being executed (M code) | Page 542 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Positioning data being executed (Dwell time) | Page 542 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Positioning data being executed (Command speed) | Page 542 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Positioning data being executed (Positioning address) | Page 542 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Positioning data being executed (Arc address) | Page 542 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Actual position value | Page 545 [Md.101] Actual position value |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Deviation counter value | Page 546 [Md.102] Deviation counter value |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Motor rotation speed | Page 547 [Md.103] Motor rotation speed |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Motor current value | Page 547 [Md.104] Motor current value |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Home position return operating status | Page 560 [Md.514] HPR operating status [FX5-SSC-G] |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Servo status3 | Page 557 [Md.125] Servo status3 |
| Refresh at the set timing | Transfer to the CPU (axis monitor 1) | Servo status4 | Page 558 [Md.126] Servo status4 [FX5-SSC-G] |
| Refresh at the set timing | Transfer to the CPU (axis monitor 2) | Statusword | Page 555 [Md.117] Statusword [FX5-SSC-G] |
| Refresh at the set timing | Transfer to the CPU (axis monitor 2) | Servo status2 | Page 555 [Md.119] Servo status2 |
| Refresh at the set timing | Transfer to the CPU (axis monitor 2) | Servo status1 | Page 550 [Md.108] Servo status1 |
| Refresh at the set timing | Transfer to the CPU (axis monitor 2) | Regenerative load ratio/Optional data monitor output 1 | Page 551 [Md.109] Regenerative load ratio/Optional data monitor output 1 |
| Refresh at the set timing | Transfer to the CPU (axis monitor 2) | Effective load torque/Optional data monitor output 2 | Page 551 [Md.110] Effective load torque/Optional data monitor output 2 |
| Refresh at the set timing | Transfer to the CPU (axis monitor 2) | Peak torque ratio/Optional data monitor output 3 | Page 551 [Md.111] Peak torque ratio/Optional data monitor output 3 |
| Refresh at the set timing | Transfer to the CPU (axis monitor 2) | Optional data monitor output 4 | Page 552 [Md.112] Optional data monitor output 4 |
| Refresh at the set timing | Transfer to the CPU (axis monitor 2) | Semi/Fully closed loop status | Page 552 [Md.113] Semi/Fully closed loop status |
| Refresh at the set timing | Transfer to the CPU (axis monitor 2) | Servo alarm | Page 553 [Md.114] Servo alarm |
| Refresh at the set timing | Transfer to the CPU (axis monitor 2) | Encoder option information | Page 554 [Md.116] Encoder option information |
| Refresh at the set timing | Transfer to the CPU (axis monitor 2) | Reverse torque limit stored value | Page 556 [Md.120] Reverse torque limit stored value |
| Refresh at the set timing | Transfer to the CPU (axis monitor 2) | Speed during command | Page 556 [Md.122] Speed during command |
| Refresh at the set timing | Transfer to the CPU (axis monitor 2) | Torque during command | Page 557 [Md.123] Torque during command |
| Refresh at the set timing | Transfer to the CPU (axis monitor 2) | Control mode switching status | Page 557 [Md.124] Control mode switching status |
| Refresh at the set timing | Transfer to the CPU (axis monitor 2) | Positioning data being executed (Axis to be interpolated) | Page 542 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to the CPU (axis monitor 2) | Deceleration start flag | Page 542 [Md.48] Deceleration start flag |
| Refresh at the set timing | Transfer to the CPU (axis monitor 2) | Optional SDO transfer result 1 | Page 558 [Md.160] Optional SDO transfer result 1 [FX5-SSC-G] |
| Refresh at the set timing | Transfer to the CPU (axis monitor 2) | Optional SDO transfer status 1 | Page 558 [Md.164] Optional SDO transfer status 1 [FX5-SSC-G] |
| Refresh at the set timing | Transfer to the CPU (axis monitor 2) | Controller position value restoration complete status | Page 559 [Md.190] Controller position value restoration complete status [FX5-SSC-G] |
| Refresh at the set timing | Transfer to the CPU (command generation axis monitor) | Command Generation Axis_Command position value | Page 527 [Md.20] Command position value |
| Refresh at the set timing | Transfer to the CPU (command generation axis monitor) | Command Generation Axis_Speed command | Page 529 [Md.22] Speed command |
| Refresh at the set timing | Transfer to the CPU (command generation axis monitor) | Command Generation Axis_Axis error No. | Page 529 [Md.23] Axis error No. |
| Refresh at the set timing | Transfer to the CPU (command generation axis monitor) | Command Generation Axis_Axis warning No | Page 530 [Md.24] Axis warning No. |
| Refresh at the set timing | Transfer to the CPU (command generation axis monitor) | Command Generation Axis_Valid M code | Page 530 [Md.25] Valid M code |
| Refresh at the set timing | Transfer to the CPU (command generation axis monitor) | Command Generation Axis_Axis operation status | Page 530 [Md.26] Axis operation status |
| Refresh at the set timing | Transfer to the CPU (command generation axis monitor) | Command Generation Axis_Current speed | Page 531 [Md.27] Current speed |
| Refresh at the set timing | Transfer to the CPU (command generation axis monitor) | Command Generation Axis_Axis speed command | Page 532 [Md.28] Axis speed command |
| Refresh at the set timing | Transfer to the CPU (command generation axis monitor) | Command Generation Axis_Speed-position switching control positioning movement amount | Page 533 [Md.29] Speed-position switching control positioning movement amount |
| Refresh at the set timing | Transfer to the CPU (command generation axis monitor) | Command Generation Axis_Status | Page 535 [Md.31] Status |
| Refresh at the set timing | Transfer to the CPU (command generation axis monitor) | Command Generation Axis_Target value | Page 536 [Md.32] Target value |
| Refresh at the set timing | Transfer to the CPU (command generation axis monitor) | Command Generation Axis_Target speed | Page 537 [Md.33] Target speed |
| Refresh at the set timing | Transfer to the CPU (command generation axis monitor) | Command Generation Axis_Start positioning data No. setting value | Page 540 [Md.38] Start positioning data No. setting value |
| Refresh at the set timing | Transfer to the CPU (command generation axis monitor) | Command Generation Axis_In speed limit flag | Page 540 [Md.39] In speed limit flag |
| Refresh at the set timing | Transfer to the CPU (command generation axis monitor) | Command Generation Axis_In speed change processing flag | Page 540 [Md.40] In speed change processing flag |
| Refresh at the set timing | Transfer to the CPU (command generation axis monitor) | Command Generation Axis_Control system repetition counter | Page 541 [Md.42] Control system repetition counter |
| Refresh at the set timing | Transfer to the CPU (command generation axis monitor) | Command Generation Axis_Positioning data No. being executed | Page 541 [Md.44] Positioning data No. being executed |
| Refresh at the set timing | Transfer to the CPU (command generation axis monitor) | Command Generation Axis_Last executed positioning data No. | Page 542 [Md.46] Last executed positioning data No. |
| Refresh at the set timing | Transfer to the CPU (command generation axis monitor) | Command Generation Axis_Positioning data being executed : Positioning identifier | Page 542 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to the CPU (command generation axis monitor) | Command Generation Axis_Positioning data being executed : M code | Page 542 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to the CPU (command generation axis monitor) | Command Generation Axis_Positioning data being executed : Dwell time | Page 542 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to the CPU (command generation axis monitor) | Command Generation Axis_Positioning data being executed : Command speed | Page 542 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to the CPU (command generation axis monitor) | Command Generation Axis_Positioning data being executed : Positioning address | Page 542 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to the CPU (command generation axis monitor) | Command Generation Axis_Speed during command | Page 556 [Md.122] Speed during command |
| Refresh at the set timing | Transfer to the CPU (command generation axis monitor) | Command Generation Axis_Deceleration start flag | Page 542 [Md.48] Deceleration start flag |
| Refresh at the set timing | Transfer to the CPU (command generation axis monitor) | Command Generation Axis Accumulative Position Value | For details, refer to the following manual, command generation axis.<br>[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Advanced Synchronous Control) |
| Refresh at the set timing | Transfer to the CPU (command generation axis monitor) | Command Generation Axis Position Value per Cycle | For details, refer to the following manual, command generation axis.<br>[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Advanced Synchronous Control) |
| Refresh at the set timing | Transfer to the CPU (command generation axis monitor) | Command Generation Axis Busy signal | For details, refer to the following manual, command generation axis.<br>[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Advanced Synchronous Control) |
| Refresh Timing | Refresh Timing | Refresh Timing | Page 396 Refresh group |
| Refresh Timing | Refresh Timing | Refresh Group [n] (n: 1-64) | Page 396 Refresh group |
| Refresh Timing (I/O)*1 | Refresh Timing (I/O)*1 | Refresh Timing | — |

*In the original, the Item column has 3 levels (level 1 / level 2 / item) with merged cells. "Refresh at the set timing" (level 1) and each "Transfer to the CPU (...)" (level 2) are merged vertically over all their rows; "Refresh Timing" (level 1) is merged over 2 rows; "Refresh Timing (I/O)*1" is one cell. Here level 1 and level 2 are both filled with the same word for "Refresh Timing" and "Refresh Timing (I/O)*1". The Reference cells "Page 542 [Md.47] Positioning data being executed" (for the Positioning data being executed rows), "For details, refer to the following manual, command generation axis. ..." (Accumulative Position Value / Position Value per Cycle / Busy signal) and "Page 396 Refresh group" (2 rows) are also merged cells. Expanded to each row. Page numbers in the Reference column are the original (printed) pages. The table spans original p.396-398; level-2 "Transfer to the CPU (command generation axis monitor)" is printed on several lines in the original.
*Compared with the Japanese edition, this English edition has no "Servo alarm detail No." ([Md.115]) row in "Transfer to the CPU (axis monitor 2)" (90 rows here vs 91 in the Japanese edition). Transcribed as printed in this English edition.

*1 The setting cannot be changed from the default in the Motion module.

##### Refresh group (リフレッシュグループ) (10.2 / original p.398)

Set the refresh timing of the specified refresh destination.

| Setting value | Description |
|---|---|
| At the Execution Time of END Instruction | Performs refresh at END processing of the CPU module. |

## 10.3 Simple Motion Module Setting (シンプルモーションユニット設定) (10.3 / original p.399)

Set the required setting for the Simple Motion module/Motion module. Refer to "Help" in the "Simple Motion Module Setting Function" of the engineering tool for details.
Select the Simple Motion module setting from the tree on the following window.
- Operation: Navigation window ⇨ "Parameter" ⇨ "Module Information" ⇨ Target module ⇨ "Simple Motion module setting"
