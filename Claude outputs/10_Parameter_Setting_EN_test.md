# 10 PARAMETER SETTING (Chapter 10 / original p.376-383)

FX5 Motion Module/Simple Motion Module User's Manual (Application) IB(NA)-0300252-M — reference

> This file is a reference of the original PDF. In addition to tables, addresses and bit definitions,
> function descriptions, device ON/OFF timing, precautions and program examples are transcribed **in full as in the original**.
> For ranges not converted, see the "Conversion range table" (in this file and `00_索引_ladder_reference.md`). **When making design decisions based on instruction behavior,
> do the final check on the corresponding page of the original.**
>
> Notation:
> - "original p.N" is the **PDF page number**. Printed page number = PDF page − 2. Cross-references in the text (e.g. "Page 139 Block start") keep the original (printed page).
> - Merged cells of the original are expanded to each row (noted right after the table).
> - Figures are shown as a [Figure] placeholder + bullet list of facts that could be read.
> - The original "☞" (page reference mark) is written as "→", "📖" (other manual mark) as "[Other manual]", and `U1¥G` as `U1\G`.

## Conversion range table (management info of this file)

| Original page | Section | Handling |
|---|---|---|
| p.376 | 10.1 Parameter Setting Procedure | Full text |
| p.376-382 | 10.2 Module Parameters | Full text |
| p.383 | 10.3 Simple Motion Module Setting | Full text |

## Contents

- 10 PARAMETER SETTING
- 10.1 Parameter Setting Procedure
- 10.2 Module Parameters
  - Refresh settings
- 10.3 Simple Motion Module Setting

---

## 10 PARAMETER SETTING (Chapter 10 / original p.376)

This chapter describes the parameter setting of the Simple Motion module/Motion module. Setting parameters eliminates the need for parameter setting by programs.
There are two types of parameter setting: module parameters and Simple Motion module setting.

## 10.1 Parameter Setting Procedure (10.1 / original p.376)

1. Add the Simple Motion module/Motion module to the engineering tool.
   - Operation: Navigation window ⇨ "Parameter" ⇨ "Module Information" ⇨ right-click ⇨ [Add New Module]
2. There are two types of parameter setting, module parameters and Simple Motion module setting, which are selected from the tree on the following window.
   - Operation: Navigation window ⇨ "Parameter" ⇨ "Module Information" ⇨ target module
3. Write the settings to the CPU module with the engineering tool.
   - Operation: [Online] ⇨ [Write to PLC]
4. The settings are reflected by resetting the CPU module or turning the power OFF→ON.

("Operation:" is the operation line with the mouse icon in the original.)

## 10.2 Module Parameters (10.2 / original p.376-382)

Set the module parameters. The module parameters have the following settings.

[FX5-SSC-S]
- Refresh settings

[FX5-SSC-G]

Module parameter (Motion)
- Refresh settings

Module parameter (Network)*1
- Required settings
- Basic settings
- Application settings

*1 For details, refer to "PARAMETER SETTINGS" in the following manual.
[Other manual] MELSEC iQ-F FX5 Motion Module User's Manual (CC-Link IE TSN)

Module parameters are selected from the tree on the following window.
- Operation: Navigation window ⇨ "Parameter" ⇨ "Module Information" ⇨ target module ⇨ "Module Parameter"

### Refresh settings (10.2 / original p.377)

Set this to transfer the buffer memory contents of the Simple Motion module/Motion module to devices or module labels of the CPU module. This refresh setting eliminates the need for reading by programs.
Select the transfer destination in "Target" from the following.
- Module label (→Page 375 Module label)
- Specified device (→Page 375 Specified device)

#### Module label (10.2 / original p.377)

Transfers the buffer memory contents to the module label corresponding to each buffer memory. Setting "Feed current value" of axis 1 to "Enable" automatically sets the items of all axes to "Enable".

#### Specified device (10.2 / original p.377)

Transfers the buffer memory contents to the specified device of the CPU module. X, Y, M, L, B, D, W, R, ZR and RD can be specified. When using the bit devices X, Y, M, L and B, set a number divisible by 16 points (e.g. X10, Y120, M16). The buffer memory data is stored in 16 points starting from the set device No.

Example
When X10 is set, the data is stored in X10 to X1F.

#### Setting items (10.2 / original p.377-382)

The refresh settings have the following items.

##### Setting items [FX5-SSC-S] (10.2 / original p.377-379)

[Figure] FX5-40SSC-S module parameter window (refresh settings) (original p.377)
- Window title: "2[U2]:FX5-40SSC-S Module Parameter"
- Left pane "Setting Item List": search box "Input the Setting Item to Search", tree "Refresh settings". Bottom tabs "Item List" "Find Result"
- Right pane "Setting Item": Target "Specified Device" (grayed-out pull-down), top right "Number of transfers to intelligent function module" "Number of transfers to CPU" (values unreadable from figure; see original p.377)
- Table columns: Item / Axis 1 / Axis 2 / Axis 3 / Axis 4
- Tree: Refresh at the set timing ⊟ Transfer to CPU (row description "Transfer the buffer memory data to the specified device.") → Feed current value, Feed machine value, Feedrate, Axis error No., Axis warning No., Valid M code, Axis operation status, Current speed, Axis feedrate, Speed-position switching control positioning movement amount, External input signal, Status, Target value, Target speed, Movement amount after near-point dog ON, Torque limit stored value/forward torque limit stored value, Special start data instruction code setting value, Special start data instruction parameter setting value, Start positioning data No. setting value (rest out of scroll)
- Bottom "Explanation" field (blank), buttons "Check(K)" "Restore the Default Settings(U)"

| Item (category 1) | Item (category 2) | Item | Reference |
|---|---|---|---|
| Refresh at the set timing | Transfer to CPU | Feed current value | Page 507 [Md.20] Feed current value |
| Refresh at the set timing | Transfer to CPU | Feed machine value | Page 508 [Md.21] Feed machine value |
| Refresh at the set timing | Transfer to CPU | Feedrate | Page 509 [Md.22] Feedrate |
| Refresh at the set timing | Transfer to CPU | Axis error No. | Page 509 [Md.23] Axis error No. |
| Refresh at the set timing | Transfer to CPU | Axis warning No. | Page 510 [Md.24] Axis warning No. |
| Refresh at the set timing | Transfer to CPU | Valid M code | Page 510 [Md.25] Valid M code |
| Refresh at the set timing | Transfer to CPU | Axis operation status | Page 510 [Md.26] Axis operation status |
| Refresh at the set timing | Transfer to CPU | Current speed | Page 511 [Md.27] Current speed |
| Refresh at the set timing | Transfer to CPU | Axis feedrate | Page 511 [Md.28] Axis feedrate |
| Refresh at the set timing | Transfer to CPU | Speed-position switching control positioning movement amount | Page 512 [Md.29] Speed-position switching control positioning movement amount |
| Refresh at the set timing | Transfer to CPU | External input signal | Page 513 [Md.30] External input signal |
| Refresh at the set timing | Transfer to CPU | Status | Page 514 [Md.31] Status |
| Refresh at the set timing | Transfer to CPU | Target value | Page 515 [Md.32] Target value |
| Refresh at the set timing | Transfer to CPU | Target speed | Page 515 [Md.33] Target speed |
| Refresh at the set timing | Transfer to CPU | Movement amount after near-point dog ON | Page 516 [Md.34] Movement amount after near-point dog ON[FX5-SSC-S] |
| Refresh at the set timing | Transfer to CPU | Torque limit stored value/forward torque limit stored value | Page 517 [Md.35] Torque limit stored value/forward torque limit stored value |
| Refresh at the set timing | Transfer to CPU | Special start data instruction code setting value | Page 517 [Md.36] Special start data instruction code setting value |
| Refresh at the set timing | Transfer to CPU | Special start data instruction parameter setting value | Page 518 [Md.37] Special start data instruction parameter setting value |
| Refresh at the set timing | Transfer to CPU | Start positioning data No. setting value | Page 518 [Md.38] Start positioning data No. setting value |
| Refresh at the set timing | Transfer to CPU | In speed limit flag | Page 518 [Md.39] In speed limit flag |
| Refresh at the set timing | Transfer to CPU | In speed change processing flag | Page 518 [Md.40] In speed change processing flag |
| Refresh at the set timing | Transfer to CPU | Special start repetition counter | Page 519 [Md.41] Special start repetition counter |
| Refresh at the set timing | Transfer to CPU | Control system repetition counter | Page 519 [Md.42] Control system repetition counter |
| Refresh at the set timing | Transfer to CPU | Start data pointer being executed | Page 519 [Md.43] Start data pointer being executed |
| Refresh at the set timing | Transfer to CPU | Positioning data No. being executed | Page 519 [Md.44] Positioning data No. being executed |
| Refresh at the set timing | Transfer to CPU | Block No. being executed | Page 519 [Md.45] Block No. being executed |
| Refresh at the set timing | Transfer to CPU | Last executed positioning data No. | Page 520 [Md.46] Last executed positioning data No. |
| Refresh at the set timing | Transfer to CPU | Positioning data being executed (positioning identifier) | Page 520 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to CPU | Positioning data being executed (M code) | Page 520 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to CPU | Positioning data being executed (dwell time) | Page 520 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to CPU | Positioning data being executed (command speed) | Page 520 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to CPU | Positioning data being executed (positioning address) | Page 520 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to CPU | Positioning data being executed (arc address) | Page 520 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to CPU | Home position return re-travel value | Page 522 [Md.100] Home position return re-travel value[FX5-SSC-S] |
| Refresh at the set timing | Transfer to CPU | Real current value | Page 523 [Md.101] Real current value |
| Refresh at the set timing | Transfer to CPU | Deviation counter value | Page 524 [Md.102] Deviation counter value |
| Refresh at the set timing | Transfer to CPU | Motor speed | Page 525 [Md.103] Motor speed |
| Refresh at the set timing | Transfer to CPU | Motor current value | Page 525 [Md.104] Motor current value |
| Refresh at the set timing | Transfer to CPU | Servo status3 | Page 535 [Md.125] Servo status3 |
| Refresh at the set timing | Transfer to CPU | Servo status5 | Page 536 [Md.127] Servo status5[FX5-SSC-S] |
| Refresh at the set timing | Transfer to CPU | Servo amplifier software No.1 | Page 526 [Md.106] Servo amplifier software No.[FX5-SSC-S] |
| Refresh at the set timing | Transfer to CPU (axis monitor) | Servo amplifier software No.2 | Page 526 [Md.106] Servo amplifier software No.[FX5-SSC-S] |
| Refresh at the set timing | Transfer to CPU (axis monitor) | Servo amplifier software No.3 | Page 526 [Md.106] Servo amplifier software No.[FX5-SSC-S] |
| Refresh at the set timing | Transfer to CPU (axis monitor) | Servo amplifier software No.4 | Page 526 [Md.106] Servo amplifier software No.[FX5-SSC-S] |
| Refresh at the set timing | Transfer to CPU (axis monitor) | Servo amplifier software No.5 | Page 526 [Md.106] Servo amplifier software No.[FX5-SSC-S] |
| Refresh at the set timing | Transfer to CPU (axis monitor) | Servo amplifier software No.6 | Page 526 [Md.106] Servo amplifier software No.[FX5-SSC-S] |
| Refresh at the set timing | Transfer to CPU (axis monitor) | Parameter error No. | Page 527 [Md.107] Parameter error No.[FX5-SSC-S] |
| Refresh at the set timing | Transfer to CPU (axis monitor) | Servo status2 | Page 533 [Md.119] Servo status2 |
| Refresh at the set timing | Transfer to CPU (axis monitor) | Servo status1 | Page 528 [Md.108] Servo status1 |
| Refresh at the set timing | Transfer to CPU (axis monitor) | Regenerative load ratio/Optional data monitor output 1 | Page 529 [Md.109] Regenerative load ratio/Optional data monitor output 1 |
| Refresh at the set timing | Transfer to CPU (axis monitor) | Effective load ratio/Optional data monitor output 2 | Page 529 [Md.110] Effective load ratio/Optional data monitor output 2 |
| Refresh at the set timing | Transfer to CPU (axis monitor) | Peak load ratio/Optional data monitor output 3 | Page 529 [Md.111] Peak load ratio/Optional data monitor output 3 |
| Refresh at the set timing | Transfer to CPU (axis monitor) | Optional data monitor output 4 | Page 530 [Md.112] Optional data monitor output 4 |
| Refresh at the set timing | Transfer to CPU (axis monitor) | Semi/Fully closed loop status | Page 530 [Md.113] Semi/Fully closed loop status |
| Refresh at the set timing | Transfer to CPU (axis monitor) | Servo alarm | Page 531 [Md.114] Servo alarm |
| Refresh at the set timing | Transfer to CPU (axis monitor) | Encoder option information | Page 532 [Md.116] Encoder option information |
| Refresh at the set timing | Transfer to CPU (axis monitor) | Reverse torque limit stored value | Page 534 [Md.120] Reverse torque limit stored value |
| Refresh at the set timing | Transfer to CPU (axis monitor) | Speed during command | Page 534 [Md.122] Speed during command |
| Refresh at the set timing | Transfer to CPU (axis monitor) | Torque during command | Page 535 [Md.123] Torque during command |
| Refresh at the set timing | Transfer to CPU (axis monitor) | Control mode switching status | Page 535 [Md.124] Control mode switching status |
| Refresh at the set timing | Transfer to CPU (axis monitor) | Positioning data being executed (interpolation target axis) | Page 520 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to CPU (axis monitor) | Deceleration start flag | Page 520 [Md.48] Deceleration start flag |
| Refresh at the set timing | Transfer to CPU | Command generation axis_Feed current value | Page 507 [Md.20] Feed current value |
| Refresh at the set timing | Transfer to CPU | Command generation axis_Feedrate | Page 509 [Md.22] Feedrate |
| Refresh at the set timing | Transfer to CPU | Command generation axis_Axis error No. | Page 509 [Md.23] Axis error No. |
| Refresh at the set timing | Transfer to CPU | Command generation axis_Axis warning No. | Page 510 [Md.24] Axis warning No. |
| Refresh at the set timing | Transfer to CPU | Command generation axis_Valid M code | Page 510 [Md.25] Valid M code |
| Refresh at the set timing | Transfer to CPU | Command generation axis_Axis operation status | Page 510 [Md.26] Axis operation status |
| Refresh at the set timing | Transfer to CPU | Command generation axis_Current speed | Page 511 [Md.27] Current speed |
| Refresh at the set timing | Transfer to CPU | Command generation axis_Axis feedrate | Page 511 [Md.28] Axis feedrate |
| Refresh at the set timing | Transfer to CPU | Command generation axis_Speed-position switching control positioning movement amount | Page 512 [Md.29] Speed-position switching control positioning movement amount |
| Refresh at the set timing | Transfer to CPU | Command generation axis_Status | Page 514 [Md.31] Status |
| Refresh at the set timing | Transfer to CPU | Command generation axis_Target value | Page 515 [Md.32] Target value |
| Refresh at the set timing | Transfer to CPU | Command generation axis_Target speed | Page 515 [Md.33] Target speed |
| Refresh at the set timing | Transfer to CPU | Command generation axis_Start positioning data No. setting value | Page 518 [Md.38] Start positioning data No. setting value |
| Refresh at the set timing | Transfer to CPU | Command generation axis_In speed limit flag | Page 518 [Md.39] In speed limit flag |
| Refresh at the set timing | Transfer to CPU | Command generation axis_In speed change processing flag | Page 518 [Md.40] In speed change processing flag |
| Refresh at the set timing | Transfer to CPU | Command generation axis_Control system repetition counter | Page 519 [Md.42] Control system repetition counter |
| Refresh at the set timing | Transfer to CPU | Command generation axis_Positioning data No. being executed | Page 519 [Md.44] Positioning data No. being executed |
| Refresh at the set timing | Transfer to CPU | Command generation axis_Last executed positioning data No. | Page 520 [Md.46] Last executed positioning data No. |
| Refresh at the set timing | Transfer to CPU | Command generation axis_Positioning data being executed_positioning identifier | Page 520 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to CPU | Command generation axis_Positioning data being executed_M code | Page 520 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to CPU | Command generation axis_Positioning data being executed_dwell time | Page 520 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to CPU | Command generation axis_Positioning data being executed_command speed | Page 520 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to CPU | Command generation axis_Positioning data being executed_positioning address | Page 520 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to CPU | Command generation axis_Speed during command | Page 534 [Md.122] Speed during command |
| Refresh at the set timing | Transfer to CPU | Command generation axis_Deceleration start flag | Page 520 [Md.48] Deceleration start flag |
| Refresh at the set timing | Transfer to CPU | Command generation axis_Cumulative current value | Refer to "Command generation axis" in the following manual for details.<br>[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Advanced Synchronous Control) |
| Refresh at the set timing | Transfer to CPU | Command generation axis_Current value per cycle | Refer to "Command generation axis" in the following manual for details.<br>[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Advanced Synchronous Control) |
| Refresh at the set timing | Transfer to CPU | Command generation axis_BUSY | Refer to "Command generation axis" in the following manual for details.<br>[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Advanced Synchronous Control) |
| Refresh timing | Refresh timing | Refresh timing | Page 380 Refresh group |
| Refresh timing | Refresh timing | Refresh group [n] (n: 1-64) | Page 380 Refresh group |
| Refresh timing (I/O)*1 | Refresh timing (I/O)*1 | Refresh timing | — |

*The item column of the original consists of merged cells in 3 levels (category 1 / category 2 / item). "Refresh at the set timing" (category 1) and each "Transfer to CPU..." (category 2) are merged vertically over all applicable rows; "Refresh timing" and "Refresh timing (I/O)*1" are merged horizontally across categories 1-2 (expanded by writing the same word in both columns); "Refresh timing" (categories 1-2) is also merged vertically over 2 rows. In the reference column, "Page 520 [Md.47] Positioning data being executed" (each row of positioning data being executed), "Page 526 [Md.106] Servo amplifier software No.[FX5-SSC-S]" (6 rows for software No.1-6; only No.1 has category 2 "Transfer to CPU", No.2-6 have "Transfer to CPU (axis monitor)"), "Refer to "Command generation axis"... (Advanced Synchronous Control)" (3 rows: cumulative current value / current value per cycle / BUSY) and "Page 380 Refresh group" (2 rows) are also merged cells. Expanded to each row. Page numbers in the reference column keep the original (printed page) notation. The table spans original p.378-379.

*1 For the Simple Motion module, this cannot be changed from the default setting.

##### Setting items [FX5-SSC-G] (10.2 / original p.380-382)

[Figure] FX5-40SSC-G(S) module parameter window (refresh settings) (original p.380)
- Window title: "1[U1]:FX5-40SSC-G(S) Module Parameter"
- Left pane "Setting Item List": search box "Input the Setting Item to Search", tree "Refresh settings". Bottom tabs "Item List" "Find Result"
- Right pane "Setting Item": Target "Specified Device" (grayed-out pull-down), "Number of transfers to intelligent function module" 0, "Number of transfers to CPU" 0
- Table columns: Item / Axis 1 / Axis 2 / Axis 3 / Axis 4
- Tree: Refresh at the set timing ⊟ Transfer to CPU (axis monitor 1) → Feed current value, Feed machine value, Feedrate, Axis error No., Axis warning No., Valid M code, Axis operation status, Current speed, Axis feedrate, Speed-position switching control positioning movement amount, External input signal, Status, Target value, Target speed, Manual pulse generator operation carry-over movement amount, Torque limit stored value/forward torque limit stored value, Special start data instruction code setting value, Special start data instruction parameter setting value, Start positioning data No. setting value, In speed limit flag (rest out of scroll)
- Bottom "Explanation" field (blank), buttons "Check(K)" "Restore the Default Settings(U)"

| Item (category 1) | Item (category 2) | Item | Reference |
|---|---|---|---|
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Feed current value | Page 507 [Md.20] Feed current value |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Feed machine value | Page 508 [Md.21] Feed machine value |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Feedrate | Page 509 [Md.22] Feedrate |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Axis error No. | Page 509 [Md.23] Axis error No. |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Axis warning No. | Page 510 [Md.24] Axis warning No. |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Valid M code | Page 510 [Md.25] Valid M code |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Axis operation status | Page 510 [Md.26] Axis operation status |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Current speed | Page 511 [Md.27] Current speed |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Axis feedrate | Page 511 [Md.28] Axis feedrate |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Speed-position switching control positioning movement amount | Page 512 [Md.29] Speed-position switching control positioning movement amount |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | External input signal | Page 513 [Md.30] External input signal |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Status | Page 514 [Md.31] Status |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Target value | Page 515 [Md.32] Target value |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Target speed | Page 515 [Md.33] Target speed |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Manual pulse generator operation carry-over movement amount | Page 521 [Md.62] Manual pulse generator operation carry-over movement amount[FX5-SSC-G] |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Torque limit stored value/forward torque limit stored value | Page 517 [Md.35] Torque limit stored value/forward torque limit stored value |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Special start data instruction code setting value | Page 517 [Md.36] Special start data instruction code setting value |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Special start data instruction parameter setting value | Page 518 [Md.37] Special start data instruction parameter setting value |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Start positioning data No. setting value | Page 518 [Md.38] Start positioning data No. setting value |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | In speed limit flag | Page 518 [Md.39] In speed limit flag |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | In speed change processing flag | Page 518 [Md.40] In speed change processing flag |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Special start repetition counter | Page 519 [Md.41] Special start repetition counter |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Control system repetition counter | Page 519 [Md.42] Control system repetition counter |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Start data pointer being executed | Page 519 [Md.43] Start data pointer being executed |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Positioning data No. being executed | Page 519 [Md.44] Positioning data No. being executed |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Block No. being executed | Page 519 [Md.45] Block No. being executed |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Last executed positioning data No. | Page 520 [Md.46] Last executed positioning data No. |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Positioning data being executed (positioning identifier) | Page 520 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Positioning data being executed (M code) | Page 520 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Positioning data being executed (dwell time) | Page 520 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Positioning data being executed (command speed) | Page 520 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Positioning data being executed (positioning address) | Page 520 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Positioning data being executed (arc address) | Page 520 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Real current value | Page 523 [Md.101] Real current value |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Deviation counter value | Page 524 [Md.102] Deviation counter value |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Motor speed | Page 525 [Md.103] Motor speed |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Motor current value | Page 525 [Md.104] Motor current value |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Home position return operation status | Page 538 [Md.514] Home position return operation status[FX5-SSC-G] |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Servo status3 | Page 535 [Md.125] Servo status3 |
| Refresh at the set timing | Transfer to CPU (axis monitor 1) | Servo status4 | Page 536 [Md.126] Servo status4[FX5-SSC-G] |
| Refresh at the set timing | Transfer to CPU (axis monitor 2) | Statusword | Page 533 [Md.117] Statusword[FX5-SSC-G] |
| Refresh at the set timing | Transfer to CPU (axis monitor 2) | Servo status2 | Page 533 [Md.119] Servo status2 |
| Refresh at the set timing | Transfer to CPU (axis monitor 2) | Servo status1 | Page 528 [Md.108] Servo status1 |
| Refresh at the set timing | Transfer to CPU (axis monitor 2) | Regenerative load ratio/Optional data monitor output 1 | Page 529 [Md.109] Regenerative load ratio/Optional data monitor output 1 |
| Refresh at the set timing | Transfer to CPU (axis monitor 2) | Effective load ratio/Optional data monitor output 2 | Page 529 [Md.110] Effective load ratio/Optional data monitor output 2 |
| Refresh at the set timing | Transfer to CPU (axis monitor 2) | Peak load ratio/Optional data monitor output 3 | Page 529 [Md.111] Peak load ratio/Optional data monitor output 3 |
| Refresh at the set timing | Transfer to CPU (axis monitor 2) | Optional data monitor output 4 | Page 530 [Md.112] Optional data monitor output 4 |
| Refresh at the set timing | Transfer to CPU (axis monitor 2) | Semi/Fully closed loop status | Page 530 [Md.113] Semi/Fully closed loop status |
| Refresh at the set timing | Transfer to CPU (axis monitor 2) | Servo alarm | Page 531 [Md.114] Servo alarm |
| Refresh at the set timing | Transfer to CPU (axis monitor 2) | Servo alarm detail No. | Page 532 [Md.115] Servo alarm detail No.[FX5-SSC-G] |
| Refresh at the set timing | Transfer to CPU (axis monitor 2) | Encoder option information | Page 532 [Md.116] Encoder option information |
| Refresh at the set timing | Transfer to CPU (axis monitor 2) | Reverse torque limit stored value | Page 534 [Md.120] Reverse torque limit stored value |
| Refresh at the set timing | Transfer to CPU (axis monitor 2) | Speed during command | Page 534 [Md.122] Speed during command |
| Refresh at the set timing | Transfer to CPU (axis monitor 2) | Torque during command | Page 535 [Md.123] Torque during command |
| Refresh at the set timing | Transfer to CPU (axis monitor 2) | Control mode switching status | Page 535 [Md.124] Control mode switching status |
| Refresh at the set timing | Transfer to CPU (axis monitor 2) | Positioning data being executed (interpolation target axis) | Page 520 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to CPU (axis monitor 2) | Deceleration start flag | Page 520 [Md.48] Deceleration start flag |
| Refresh at the set timing | Transfer to CPU (axis monitor 2) | Optional SDO transfer result 1 | Page 536 [Md.160] Optional SDO transfer result 1[FX5-SSC-G] |
| Refresh at the set timing | Transfer to CPU (axis monitor 2) | Optional SDO transfer status 1 | Page 536 [Md.164] Optional SDO transfer status 1[FX5-SSC-G] |
| Refresh at the set timing | Transfer to CPU (axis monitor 2) | Controller current value restoration complete status | Page 537 [Md.190] Controller current value restoration complete status[FX5-SSC-G] |
| Refresh at the set timing | Transfer to CPU (command generation axis monitor) | Command generation axis_Feed current value | Page 507 [Md.20] Feed current value |
| Refresh at the set timing | Transfer to CPU (command generation axis monitor) | Command generation axis_Feedrate | Page 509 [Md.22] Feedrate |
| Refresh at the set timing | Transfer to CPU (command generation axis monitor) | Command generation axis_Axis error No. | Page 509 [Md.23] Axis error No. |
| Refresh at the set timing | Transfer to CPU (command generation axis monitor) | Command generation axis_Axis warning No. | Page 510 [Md.24] Axis warning No. |
| Refresh at the set timing | Transfer to CPU (command generation axis monitor) | Command generation axis_Valid M code | Page 510 [Md.25] Valid M code |
| Refresh at the set timing | Transfer to CPU (command generation axis monitor) | Command generation axis_Axis operation status | Page 510 [Md.26] Axis operation status |
| Refresh at the set timing | Transfer to CPU (command generation axis monitor) | Command generation axis_Current speed | Page 511 [Md.27] Current speed |
| Refresh at the set timing | Transfer to CPU (command generation axis monitor) | Command generation axis_Axis feedrate | Page 511 [Md.28] Axis feedrate |
| Refresh at the set timing | Transfer to CPU (command generation axis monitor) | Command generation axis_Speed-position switching control positioning movement amount | Page 512 [Md.29] Speed-position switching control positioning movement amount |
| Refresh at the set timing | Transfer to CPU (command generation axis monitor) | Command generation axis_Status | Page 514 [Md.31] Status |
| Refresh at the set timing | Transfer to CPU (command generation axis monitor) | Command generation axis_Target value | Page 515 [Md.32] Target value |
| Refresh at the set timing | Transfer to CPU (command generation axis monitor) | Command generation axis_Target speed | Page 515 [Md.33] Target speed |
| Refresh at the set timing | Transfer to CPU (command generation axis monitor) | Command generation axis_Start positioning data No. setting value | Page 518 [Md.38] Start positioning data No. setting value |
| Refresh at the set timing | Transfer to CPU (command generation axis monitor) | Command generation axis_In speed limit flag | Page 518 [Md.39] In speed limit flag |
| Refresh at the set timing | Transfer to CPU (command generation axis monitor) | Command generation axis_In speed change processing flag | Page 518 [Md.40] In speed change processing flag |
| Refresh at the set timing | Transfer to CPU (command generation axis monitor) | Command generation axis_Control system repetition counter | Page 519 [Md.42] Control system repetition counter |
| Refresh at the set timing | Transfer to CPU (command generation axis monitor) | Command generation axis_Positioning data No. being executed | Page 519 [Md.44] Positioning data No. being executed |
| Refresh at the set timing | Transfer to CPU (command generation axis monitor) | Command generation axis_Last executed positioning data No. | Page 520 [Md.46] Last executed positioning data No. |
| Refresh at the set timing | Transfer to CPU (command generation axis monitor) | Command generation axis_Positioning data being executed_positioning identifier | Page 520 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to CPU (command generation axis monitor) | Command generation axis_Positioning data being executed_M code | Page 520 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to CPU (command generation axis monitor) | Command generation axis_Positioning data being executed_dwell time | Page 520 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to CPU (command generation axis monitor) | Command generation axis_Positioning data being executed_command speed | Page 520 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to CPU (command generation axis monitor) | Command generation axis_Positioning data being executed_positioning address | Page 520 [Md.47] Positioning data being executed |
| Refresh at the set timing | Transfer to CPU (command generation axis monitor) | Command generation axis_Speed during command | Page 534 [Md.122] Speed during command |
| Refresh at the set timing | Transfer to CPU (command generation axis monitor) | Command generation axis_Deceleration start flag | Page 520 [Md.48] Deceleration start flag |
| Refresh at the set timing | Transfer to CPU (command generation axis monitor) | Command generation axis_Cumulative current value | Refer to "Command generation axis" in the following manual for details.<br>[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Advanced Synchronous Control) |
| Refresh at the set timing | Transfer to CPU (command generation axis monitor) | Command generation axis_Current value per cycle | Refer to "Command generation axis" in the following manual for details.<br>[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Advanced Synchronous Control) |
| Refresh at the set timing | Transfer to CPU (command generation axis monitor) | Command generation axis_BUSY | Refer to "Command generation axis" in the following manual for details.<br>[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Advanced Synchronous Control) |
| Refresh timing | Refresh timing | Refresh timing | Page 380 Refresh group |
| Refresh timing | Refresh timing | Refresh group [n] (n: 1-64) | Page 380 Refresh group |
| Refresh timing (I/O)*1 | Refresh timing (I/O)*1 | Refresh timing | — |

*The item column of the original consists of merged cells in 3 levels (category 1 / category 2 / item). "Refresh at the set timing" (category 1) and each "Transfer to CPU..." (category 2) are merged vertically over all applicable rows; "Refresh timing" and "Refresh timing (I/O)*1" are merged horizontally across categories 1-2 (expanded by writing the same word in both columns); "Refresh timing" (categories 1-2) is also merged vertically over 2 rows. In the reference column, "Page 520 [Md.47] Positioning data being executed" (each row of positioning data being executed), "Refer to "Command generation axis"... (Advanced Synchronous Control)" (3 rows: cumulative current value / current value per cycle / BUSY) and "Page 380 Refresh group" (2 rows) are also merged cells. Expanded to each row. Page numbers in the reference column keep the original (printed page) notation. The table spans original p.380-382. Category 2 "Transfer to CPU (command generation axis monitor)" is written over 3 lines in the original.

*1 For the Motion module, this cannot be changed from the default setting.

##### Refresh group (10.2 / original p.382)

Set the refresh timing of the specified refresh target.

| Setting value | Description |
|---|---|
| At the execution time of END instruction | Refreshed at END processing of the CPU module. |

## 10.3 Simple Motion Module Setting (10.3 / original p.383)

Configure the settings required for the Simple Motion module/Motion module. For details, refer to the help of the "Simple Motion Module Setting Function" of the engineering tool.
Simple Motion module setting is selected from the tree on the following window.
- Operation: Navigation window ⇨ "Parameter" ⇨ "Module Information" ⇨ target module ⇨ "Simple Motion Module Setting"
