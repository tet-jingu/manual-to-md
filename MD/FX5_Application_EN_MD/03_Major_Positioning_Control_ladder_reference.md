# 3 MAJOR POSITIONING CONTROL (主要な位置決め制御) (Chapter 3 / original p.60-138)

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

## Conversion range (変換範囲表 / original p.60-138)

| Original page | Section | Handling |
|---|---|---|
| p.60-78 | 3.1 Outline of Major Positioning Controls (incl. chapter 3 lead text) | Full text |
| p.79-95 | 3.2 Setting the Positioning Data: Relation between each control and positioning data, 1-axis linear control, 2-axis linear interpolation control, 3-axis linear interpolation control, 4-axis linear interpolation control, Fixed-feed control | Full text |
| p.96-99 | 3.2 2-axis circular interpolation control with sub point designation | Full text |
| p.100-104 | 3.2 2-axis circular interpolation control with center point designation | Full text |
| p.105-108 | 3.2 Speed control | Full text |
| p.109-115 | 3.2 Speed-position switching control (INC mode) | Full text |
| p.116-122 | 3.2 Speed-position switching control (ABS mode) | Full text |
| p.123-129 | 3.2 Position-speed switching control | Full text |
| p.130-133 | 3.2 Current value changing | Full text (including program example) |
| p.134 | 3.2 NOP instruction | Full text |
| p.135-136 | 3.2 JUMP instruction | Full text |
| p.137 | 3.2 LOOP | Full text |
| p.138 | 3.2 LEND | Full text |

## Table of Contents (目次)

- 3 MAJOR POSITIONING CONTROL (主要な位置決め制御)
- 3.1 Outline of Major Positioning Controls (主要な位置決め制御の概要)
- 3.2 Setting the Positioning Data (位置決めデータの設定)

---

## 3 MAJOR POSITIONING CONTROL (主要な位置決め制御) (Chapter 3 / original p.60)

The details and usage of the major positioning controls (control functions using the "positioning data") are explained in this chapter.
The major positioning controls include such controls as "positioning control" in which positioning is carried out to a designated position using the address information, "speed control" in which a rotating object is controlled at a constant speed, "speed-position switching control" in which the operation is shifted from "speed control" to "position control" and "position-speed switching control" in which the operation is shifted from "position control" to "speed control".
Execute the required settings to match each control.

## 3.1 Outline of Major Positioning Controls (主要な位置決め制御の概要) (3.1 / original p.60-78)

"Major positioning controls" are carried out using the "positioning data" stored in the Simple Motion module/Motion module.
The basic controls such as position control and speed control are executed by setting the required items in this "positioning data", and then starting that positioning data.
The control method for the "major positioning controls" is set in setting item "[Da.2] Control method" of the positioning data.
Control defined as a "major positioning control" carries out the following types of control according to the "[Da.2] Control method" setting. However, the position loop is included for commanding to servo amplifier in the speed control set in "[Da.2] Control method". Use the "speed-torque control" to execute the speed control not including position loop. (→Page 186 Speed-torque Control)

- List of major positioning controls (original p.60-61)

| Major positioning control (1) | Major positioning control (2) | Major positioning control (3) | [Da.2] Control method | Details |
|---|---|---|---|---|
| Position control | Linear control | 1-axis linear control | ABS Linear 1<br>INC Linear 1 | Positioning of the designated 1 axis is carried out from the start address (current stop position) to the designated position. |
| Position control | Linear control | 2-axis linear interpolation control*1 | ABS Linear 2<br>INC Linear 2 | Using the designated 2 axes, linear interpolation control is carried out from the start address (current stop position) to the designated position. |
| Position control | Linear control | 3-axis linear interpolation control*1 | ABS Linear 3<br>INC Linear 3 | Using the designated 3 axes, linear interpolation control is carried out from the start address (current stop position) to the designated position. |
| Position control | Linear control | 4-axis linear interpolation control*1 | ABS Linear 4<br>INC Linear 4 | Using the designated 4 axes, linear interpolation control is carried out from the start address (current stop position) to the designated position. |
| Position control | Fixed-feed control | 1-axis fixed-feed control | Fixed-feed 1 | Positioning of the designated 1 axis is carried out for a designated movement amount from the start address (current stop position).<br>(The "[Md.20] Command position value" is set to "0" at the start.) |
| Position control | Fixed-feed control | 2-axis fixed-feed control*1 | Fixed-feed 2 | Using the designated 2 axes, linear interpolation control is carried out for a designated movement amount from the start address (current stop position).<br>(The "[Md.20] Command position value" is set to "0" at the start.) |
| Position control | Fixed-feed control | 3-axis fixed-feed control*1 | Fixed-feed 3 | Using the designated 3 axes, linear interpolation control is carried out for a designated movement amount from the start address (current stop position).<br>(The "[Md.20] Command position value" is set to "0" at the start.) |
| Position control | Fixed-feed control | 4-axis fixed-feed control*1 | Fixed-feed 4 | Using the designated 4 axes, linear interpolation control is carried out for a designated movement amount from the start address (current stop position).<br>(The "[Md.20] Command position value" is set to "0" at the start.) |
| Position control | 2-axis circular interpolation control*1 | Sub point designation | ABS Circular sub<br>INC Circular sub | Using the designated 2 axes, positioning is carried out in an arc path to a position designated from the start point address (current stop position). |
| Position control | 2-axis circular interpolation control*1 | Center point designation | ABS Circular right<br>ABS Circular left<br>INC Circular right<br>INC Circular left | Using the designated 2 axes, positioning is carried out in an arc path to a position designated from the start point address (current stop position). |
| Speed control | Speed control | 1-axis speed control | Forward run speed 1<br>Reverse run speed 1 | The speed control of the designated 1 axis is carried out. |
| Speed control | Speed control | 2-axis speed control*1 | Forward run speed 2<br>Reverse run speed 2 | The speed control of the designated 2 axes is carried out. |
| Speed control | Speed control | 3-axis speed control*1 | Forward run speed 3<br>Reverse run speed 3 | The speed control of the designated 3 axes is carried out. |
| Speed control | Speed control | 4-axis speed control*1 | Forward run speed 4<br>Reverse run speed 4 | The speed control of the designated 4 axes is carried out. |
| Speed-position switching control | Speed-position switching control | Speed-position switching control | Forward run speed/position<br>Reverse run speed/position | The control is continued as position control (positioning for the designated address or movement amount) by turning ON the "speed-position switching signal" after first carrying out speed control. |
| Position-speed switching control | Position-speed switching control | Position-speed switching control | Forward run position/speed<br>Reverse run position/speed | The control is continued as speed control by turning ON the "position-speed switching signal" after first carrying out position control. |
| Other control | Other control | NOP instruction | NOP | A nonexecutable control method. When this instruction is set, the operation is transferred to the next data operation, and the instruction is not executed. |
| Other control | Other control | Current value changing | Current value changing | "[Md.20] Command position value" is changed to an address set in the positioning data.<br>This can be carried out by either of the following 2 methods.<br>("[Md.21] Machine feed value" cannot be changed.)<br>• Current value changing using the control method<br>• Current value changing using the current value changing start No. (No.9003). |
| Other control | Other control | JUMP instruction | JUMP instruction | An unconditional or conditional JUMP is carried out to a designated positioning data No. |
| Other control | Other control | LOOP | LOOP | A repeat control is carried out by repeat LOOP to LEND. |
| Other control | Other control | LEND | LEND | Control is returned to the top of the repeat control by repeat LOOP to LEND. After the repeat operation is completed specified times, the next positioning data is run. |

*In the original, the "Major positioning control" heading spans 3 columns. "Position control" is merged over the 10 rows from 1-axis linear control to center point designation; "Linear control" and "Fixed-feed control" are each merged over 4 rows; "2-axis circular interpolation control*1" over 2 rows; "Speed control" (spanning the first 2 columns) over 4 rows; "Speed-position switching control" and "Position-speed switching control" each span the 3 "Major positioning control" columns in one row; "Other control" (spanning the first 2 columns) over 5 rows. The "Details" cell of 2-axis circular interpolation control is merged over the Sub point designation / Center point designation rows. Expanded to each row (columns (1)/(2)/(3) are the 3 levels of the merged heading). The table continues from p.60 to p.61 (header repeated on p.61).

*1 Control is carried out so that linear and arc paths are drawn using a motor set in two or more axes directions. This kind of control is called "interpolation control". (→Page 74 Interpolation control)

### Data required for major positioning control (主要な位置決め制御に必要なデータ) (3.1 / original p.62)

The following table shows an outline of the "positioning data" configuration and setting details required to carry out the "major positioning controls".

| Setting item (group) | Setting item (No.) | Setting item (name) | Setting details |
|---|---|---|---|
| Positioning data | [Da.1] | Operation pattern | Set the method by which the continuous positioning data (Ex: positioning data No.1, No.2, No.3) will be controlled. (→Page 61 Operation patterns of major positioning controls) |
| Positioning data | [Da.2] | Control method | Set the control method defined as a "major positioning control". (→Page 58 Outline of Major Positioning Controls) |
| Positioning data | [Da.3] | Acceleration time No. | Select and set the acceleration time at control start. (Select one of the four values set in [Pr.9], [Pr.25], [Pr.26], and [Pr.27] for the acceleration time.) |
| Positioning data | [Da.4] | Deceleration time No. | Select and set the deceleration time at control stop. (Select one of the four values set in [Pr.10], [Pr.28], [Pr.29], and [Pr.30] for the deceleration time.) |
| Positioning data | [Da.6] | Positioning address/movement amount | Set the target value during position control. (→Page 68 Designating the positioning address) |
| Positioning data | [Da.7] | Arc address | Set the sub point or center point address during 2-axis circular interpolation control. |
| Positioning data | [Da.8] | Command speed | Set the speed during the control execution. |
| Positioning data | [Da.9] | Dwell time/JUMP destination positioning data No. | The time between the command pulse output is completed to the positioning completed signal is turned ON. Set it for absorbing the delay of the mechanical system to the instruction, such as the delay of the servo system (deviation). |
| Positioning data | [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | Set this item when carrying out sub work (clamp and drill stops, tool replacement, etc.) corresponding to the code No. related to the positioning data execution. |
| Positioning data | [Da.20] | Axis to be interpolated No.1 | Set an axis to be interpolated during the 2- to 4-axis interpolation operation. (→Page 74 Interpolation control) |
| Positioning data | [Da.21] | Axis to be interpolated No.2 | Set an axis to be interpolated during the 2- to 4-axis interpolation operation. (→Page 74 Interpolation control) |
| Positioning data | [Da.22] | Axis to be interpolated No.3 | Set an axis to be interpolated during the 2- to 4-axis interpolation operation. (→Page 74 Interpolation control) |

*In the original, "Positioning data" is merged over all 12 rows, and the "Setting details" of [Da.20] to [Da.22] is merged over 3 rows. Expanded to each row. The original table has no [Da.5] row.

The settings and setting requirement for the setting details of [Da.1] to [Da.10] and [Da.20] to [Da.22] differ according to the "[Da.2] Control method".
→Page 77 Setting the Positioning Data

#### Major positioning control sub functions (主要な位置決め制御の補助機能) (3.1 / original p.62)

Refer to "Combination of Main Functions and Sub Functions" in the following manual for details on "sub functions" that can be combined with the major positioning control.
[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Startup)
Also refer to the following for details on each sub function.
→Page 218 CONTROL SUB FUNCTIONS

> **Point**
> 600 positioning data (positioning data No.1 to 600) items can be set per axis.

### Operation patterns of major positioning controls (主要な位置決め制御の運転パターン) (3.1 / original p.63-69)

In "major positioning control" (high-level positioning control), "[Da.1] Operation pattern" can be set to designate whether to continue executing positioning data after the started positioning data. The "operation pattern" includes the following 3 types.

| Positioning control | Operation pattern |
|---|---|
| Positioning complete | Independent positioning control (operation pattern: 00) |
| Positioning continue | Continuous positioning control (operation pattern: 01) |
| Positioning continue | Continuous path control (operation pattern: 11) |

*In the original, "Positioning continue" is merged over 2 rows. Expanded to each row.

#### Independent positioning control (Positioning complete) (単独位置決め制御(位置決め終了)) (3.1 / original p.63)

This control is set when executing only one designated data item of positioning. If a dwell time is designated, the positioning completes after the designated time elapses.
This data (operation pattern [00] data) becomes the end of block data when carrying out block positioning. (The positioning stops after this data is executed.)

##### Operation example (動作例) (3.1 / original p.63)

[Figure] Operation example of independent positioning control (original p.63)
- Speed waveform (V-t): one trapezoid labeled "Positioning complete (00)"; after the deceleration stop, a "Dwell time" interval.
- [Cd.184] Positioning start OFF→ON; following it, the start complete signal ([Md.31] Status: b14) and [Md.141] BUSY turn ON, and acceleration starts at the same time.
- After the deceleration stop and the dwell time elapses, [Md.141] BUSY turns OFF and the positioning complete signal ([Md.31] Status: b15) turns ON.
- The positioning complete signal (b15) turns OFF after a fixed time.
- [Cd.184] Positioning start turns OFF (after BUSY OFF), and the start complete signal (b14) turns OFF following it.

#### Continuous positioning control (連続位置決め制御) (3.1 / original p.64)

- The machine always automatically decelerates each time the positioning is completed. Acceleration is then carried out after the Simple Motion module/Motion module command speed reaches 0 to carry out the next positioning data operation. If a dwell time is designated, the acceleration is carried out after the designated time elapses.
- In operation by continuous positioning control (operation pattern "01"), the next positioning No. is automatically executed. Always set operation pattern "00" in the last positioning data to complete the positioning. If the operation pattern is set to positioning continue ("01" or "11"), the operation will continue until operation pattern "00" is found. If the operation pattern "00" cannot be found, the operation may be carried out until the positioning data No.600. If the operation pattern of the positioning data No.600 is not completed, the operation will be started again from the positioning data No.1.

##### Operation example (動作例) (3.1 / original p.64)

[Figure] Operation example of continuous positioning control (original p.64)
- Speed waveform (V-t; upper side "Address (+) direction", lower side "Address (-) direction"):
  - 1st "Positioning continue (01)": trapezoid in the address (+) direction. It decelerates to speed 0 and, labeled "Dwell time not designated", immediately accelerates for the next data.
  - 2nd "Positioning continue (01)": trapezoid in the address (+) direction (higher speed than the 1st). After stopping at speed 0, "Dwell time".
  - 3rd "Positioning complete (00)": trapezoid in the address (-) direction. After stopping, "Dwell time".
- [Cd.184] Positioning start OFF→ON; the start complete signal ([Md.31] Status: b14) and [Md.141] BUSY turn ON.
- The positioning complete signal ([Md.31] Status: b15) turns ON for a short time at the completion of each positioning data (at the stop of the 1st; after the dwell time of the 2nd; after the dwell time of the 3rd).
- After the dwell time of the last data (00), [Md.141] BUSY turns OFF. When [Cd.184] Positioning start turns OFF, the start complete signal (b14) turns OFF.

#### Continuous path control (連続軌跡制御) (3.1 / original p.65-69)

##### Continuous path control (連続軌跡制御) (3.1 / original p.65)

- The speed is changed without deceleration stop between the command speed of the "positioning data No. currently being executed" and the speed of the "positioning data No. to carry out the next operation". The speed is not changed if the current speed and the next speed are equal.
- The speed used in the previous positioning operation is continued when the command speed is set to "-1".
- Dwell time is ignored, even if it is set.
- The next positioning No. is executed automatically in operations by continuous path control (operation pattern "11"). Always complete the positioning by setting operation pattern "00" in the last positioning data. If the operation pattern is set to positioning continue ("01" or "11"), the operation will continue until operation pattern "00" is found. If the operation pattern "00" cannot be found, the operation may be carried out until the positioning data No.600. If the operation pattern of the positioning data No.600 is not complete, the operation will be started again from the positioning data No.1.
- The speed switching includes the "front-loading speed switching mode" in which the speed is changed at the end of the current positioning side, and the "standard speed switching mode" in which the speed is at the start of the next positioning side. (→Page 466 [Pr.19] Speed switching mode)
- In the continuous path control, the positioning may be completed before the set address/movement amount and the current data may be switched to the "positioning data that will be run next". This is because a preference is given to the positioning at a command speed. In actuality, the positioning is completed before the set address/movement amount by an amount of remaining distance at speeds less than the command speed. The remaining distance (Δ1) at speeds less than the command speed is 0 ≤ Δ1 ≤ (distance moved in operation cycle at a speed at the time of completion of the positioning). The remaining distance (Δ1) is output at the next positioning data No.

##### Operation example (動作例) (3.1 / original p.65)

[Figure] Operation example of continuous path control (original p.65)
- Speed waveform (V-t; upper side "Address (+) direction", lower side "Address (-) direction"): 1st "Positioning continue (11)" accelerates to a constant speed; without deceleration stop, accelerates to the higher speed of the 2nd "Positioning continue (11)" and runs at constant speed; without deceleration stop, decelerates to the lower speed of the 3rd "Positioning complete (00)" and runs at constant speed; finally a deceleration stop followed by "Dwell time".
- [Cd.184] Positioning start OFF→ON; the start complete signal ([Md.31] Status: b14) and [Md.141] BUSY turn ON.
- The positioning complete signal ([Md.31] Status: b15) turns ON for a short time at each switching of positioning data (1→2, 2→3) and after the final stop + dwell time.
- After the last dwell time, [Md.141] BUSY turns OFF. When [Cd.184] Positioning start turns OFF, the start complete signal (b14) turns OFF.

> **Point**
> In the continuous path control, a speed variation will not occur using the near-pass function when the positioning data No. is switched.
> (→Page 237 Near pass function)

##### Deceleration stop conditions during continuous path control (連続軌跡制御時の減速停止条件) (3.1 / original p.66)

Deceleration stops are not carried out in continuous path control, but the machine will carry out a deceleration stop to speed "0" in the following 3 cases.
- When the operation pattern of the positioning data currently being executed is "continuous path control: 11", and the movement direction of the positioning data currently being executed differs from that of the next positioning data. (Only for 1-axis positioning control (Refer to the next point.))

[Figure] Deceleration stop when the movement direction differs (original p.66)
- "Positioning data No.1 Operation pattern: 11" is a trapezoid in the positive direction; it decelerates and passes speed 0 at the point labeled "Speed becomes 0", then "Positioning data No.2 Operation pattern: 00" runs as a trapezoid in the negative direction.

- During operation by step operation. (→Page 285 Step function)
- When there is an error in the positioning data to carry out the next operation.

> **Point**
> - The movement direction is not checked during interpolation operations. Thus, automatic deceleration to a stop will not be carried out even if the movement direction is changed (See the figures below). Because of this, the interpolation axis may rapidly reverse direction. To avoid this rapid direction reversal in the interpolation axis, set the pass point to continuous positioning control "01" instead of setting it to continuous path control "11".
>
> [Figure] Rapid direction reversal during interpolation (original p.66)
> - [Positioning by interpolation]: horizontal axis "Reference axis", vertical axis "Interpolation axis". Positioning data No.1 moves linearly in reference axis + / interpolation axis + direction; positioning data No.2 moves linearly in reference axis + / interpolation axis - direction (inverted-V path). Label "Positioning data No.1 • • • Continuous path control".
> - [Reference axis operation] (V-t): accelerates to a constant speed in positioning data No.1, continues at the same speed through positioning data No.2, and decelerates to a stop at the end of No.2.
> - [Interpolation axis operation] (V-t): accelerates in the positive direction to a constant speed in positioning data No.1; at the No.1→No.2 switching point the speed changes at once from positive to negative (label "Rapidly reverse direction"); decelerates to a stop at the end of No.2.
>
> - When a "0" is set in the "[Da.6] Positioning address/movement amount" of the continuous path control positioning data, the command speed is reduced to 0 in an operation cycle. When a "0" is set in the "[Da.6] Positioning address/movement amount" to increase the number of speed change points in the future, change the "[Da.2] Control method" to the "NOP" to make the control nonexecutable. (→Page 132 NOP instruction)
> - In the continuous path control positioning data, assure a movement distance so that the execution time with that data is 100 ms or longer, or lower the command speed.

##### Speed handling (速度の扱い) (3.1 / original p.67)

- Continuous path control command speeds are set with each positioning data. The Simple Motion module/Motion module carries out the positioning at the speed designated with each positioning data.
- The command speed can be set to "-1" in continuous path control. The control will be carried out at the speed used in the previous positioning data No. if the command speed is set to "-1". The "current speed" will be displayed in the command speed when the positioning data is set with an engineering tool. The current speed is the speed of the positioning control being executed currently.
- The speed does not need to be set in each positioning data when carrying out uniform speed control if "-1" is set beforehand in the command speed.
- If the speed is changed or the override function is executed, in the previous positioning data when "-1" is set in the command speed, the operation can be continued at the new speed.
- The error "No command speed" (error code: 1A12H [FX5-SSC-S], or error codes 1B12H to 1B14H [FX5-SSC-G]) occurs and positioning cannot be started if "-1" is set in the command speed of the first positioning data at start.

[Relation between the command speed and current speed]

[Figure] Relation between the command speed and current speed (original p.67)
- Two speed waveforms (vertical axis Speed 1000/2000/3000, sections P1 to P5). Both figures have the values in the table below.
- Left figure: accelerates to 1000 in P1 and runs at constant speed; accelerates to 3000 in P2 and reaches 3000 within P2; 3000 constant in P3 to P4; decelerates to a stop in P5.
- Right figure: accelerates to 1000 in P1 and runs at constant speed; starts accelerating in P2 but does not reach 3000 within P2, reaches 3000 in the middle of P3; 3000 constant in P4; decelerates to a stop in P5. Label (pointing at P2): "The current speed is changed even if the command speed is not reached in P2."

| Item | P1 | P2 | P3 | P4 | P5 |
|---|---|---|---|---|---|
| [Da.8] Command speed | 1000 | 3000 | -1 | -1 | -1 |
| [Md.27] Current speed | 1000 | 3000 | 3000 | 3000 | 3000 |

*The table above lists the values printed in the figure (identical in the left and right figures).

> **Point**
> - In the continuous path control, a speed variation will not occur using the near-pass function when the positioning data is switched. (→Page 237 Near pass function)
> - The Simple Motion module/Motion module holds the command speed set with the positioning data, and the latest value of the speed set with the speed change request as the "[Md.27] Current speed". It controls the operation at the "current speed" when "-1" is set in the command speed. (Depending on the relation between the movement amount and the speed, the speed command may not reach the command speed value, but even then the current speed will be updated.)
> - When the address for speed change is identified beforehand, generate and execute the positioning data for speed change by the continuous path control to carry out the speed change without requesting the speed change with a program.

##### Speed switching (Standard speed switching mode: Switch the speed when executing the next positioning data.) (→Page 466 [Pr.19] Speed switching mode) (速度の切換え(標準速度切換えモード)) (3.1 / original p.68)

- If the respective command speeds differ in the "positioning data currently being executed" and the "positioning data to carry out the next operation", the machine will accelerate or decelerate after reaching the positioning point set in the "positioning data currently being executed" and the speed will change over to the speed set in the "positioning data to carry out the next operation".
- The parameters used in acceleration/deceleration to the command speed set in the "positioning data to carry out the next operation" are those of the positioning data to carry out acceleration/deceleration. Speed switching will not be carried out if the command speeds are the same.

Ex.

[Figure] Operation example of standard speed switching mode (original p.68)
- [Da.1] Operation pattern: 5 sections 11 → 11 → 11 → 01 → 00.
- Positioning (speed waveform V-t): 1st section (11) accelerates and runs at constant speed. From the end point of the 1st section (label "Speed switching"), it accelerates at the start of the 2nd section (11) and runs at constant speed; accelerates further at the start of the 3rd section (11) and runs at constant speed; decelerates at the start of the 4th section (01), runs at constant speed, then decelerates to a stop followed by "Dwell time". The 5th section (00) runs a trapezoid, decelerates to a stop, followed by "Dwell time".
- [Cd.184] Positioning start OFF→ON; the start complete signal ([Md.31] Status: b14) and [Md.141] BUSY turn ON.
- The positioning complete signal ([Md.31] Status: b15) turns ON for a short time at each section boundary (1→2, 2→3, 3→4), after the dwell time of the 4th section, and after the dwell time of the 5th section.
- After the last dwell time, [Md.141] BUSY turns OFF. When [Cd.184] Positioning start turns OFF, the start complete signal (b14) turns OFF.

- If the movement amount is small in regard to the target speed, the current speed may not reach the target speed even if acceleration/deceleration is carried out. In this case, the machine is accelerated/decelerated so that it nears the target speed. If the movement amount will be exceeded when automatic deceleration is required (Ex. Operation patterns "00", "01", etc.), the machine will immediately stop at the designated positioning address, and the warning "Insufficient movement amount" (warning code: 0998H [FX5-SSC-S], or warning code 0D58H [FX5-SSC-G]) will occur.

| [When the speed cannot change over in P2] | [When the movement amount is small during automatic deceleration] |
|---|---|
| For the following relation of the speed P1 = P4, P2 = P3, P1 < P2<br>[Figure] (original p.68) Accelerates and runs at constant speed in P1; in P2 it accelerates but cannot finish accelerating within the P2 section, reaches the P3 speed (= P2) in the middle of P3 and runs at constant speed; decelerates in P4 to the same speed as P1, runs at constant speed, then decelerates to a stop. | The movement amount required to carry out the automatic deceleration cannot be secured, so the machine immediately stops in a speed ≠ 0 status.<br>[Figure] (original p.68) Constant speed in Pn; deceleration starts at Pn + 1, but before the speed reaches 0 the speed drops vertically to 0 at the "Positioning address" (immediate stop). |

##### Speed switching (Front-loading speed switching mode: The speed switches at the end of the positioning data currently being executed.) (→Page 466 [Pr.19] Speed switching mode) (速度の切換え(前倒し速度切換えモード)) (3.1 / original p.69)

- If the respective command speeds differ in the "positioning data currently being executed" and the "positioning data to carry out the next operation", the speed will change over to the speed set in the "positioning data to carry out the next operation" at the end of the "positioning data currently being executed".
- The parameters used in acceleration/deceleration to the command speed set in the "positioning data to carry out the next operation" are those of the positioning data to carry out acceleration/deceleration. Speed switching will not be carried out if the command speeds are the same.

Ex.

[Figure] Operation example of front-loading speed switching mode (original p.69)
- [Da.1] Operation pattern: 5 sections 11 → 11 → 11 → 01 → 00.
- Positioning (speed waveform V-t): at the end of each section (before the section end point), the machine accelerates/decelerates to the speed of the next section, so the speed is already the next speed at the section boundary. Accelerates at the end of the 1st section (11), accelerates at the end of the 2nd section (11), decelerates at the end of the 3rd section (11); the 4th section (01) runs at constant speed, then decelerates to a stop followed by "Dwell time". The 5th section (00) runs a trapezoid, decelerates to a stop, followed by "Dwell time".
- [Cd.184] Positioning start OFF→ON; the start complete signal ([Md.31] Status: b14) and [Md.141] BUSY turn ON.
- The positioning complete signal ([Md.31] Status: b15) turns ON for a short time at each section boundary (1→2, 2→3, 3→4), after the dwell time of the 4th section, and after the dwell time of the 5th section.
- After the last dwell time, [Md.141] BUSY turns OFF. When [Cd.184] Positioning start turns OFF, the start complete signal (b14) turns OFF.

- If the movement amount is small in regard to the target speed, the current speed may not reach the target speed even if acceleration/deceleration is carried out. In this case, the machine is accelerated/decelerated so that it nears the target speed. If the movement amount will be exceeded when automatic deceleration is required (Ex. Operation patterns "00", "01", etc.), the machine will immediately stop at the designated positioning address, and the warning "Insufficient movement amount" (warning code: 0998H [FX5-SSC-S], or warning code 0D58H [FX5-SSC-G]) will occur.

| [When the speed cannot change over to the P2 speed in P1] | [When the movement amount is small during automatic deceleration] |
|---|---|
| For the following relation of the speed P1 = P4, P2 = P3, P1 < P2<br>[Figure] (original p.69) In P1 the machine accelerates from 0 and only reaches the P2 speed at the end of P1 (P1 speed itself is never held); constant speed through P2 and P3; decelerates at the end of P3 to the P4 speed (= P1), runs at constant speed in P4, then decelerates to a stop. | The movement amount required to carry out the automatic deceleration cannot be secured, so the machine immediately stops in a speed ≠ 0 status.<br>[Figure] (original p.69) Constant speed in Pn; deceleration starts before the Pn / Pn + 1 boundary, and in the middle of Pn + 1 the speed drops vertically to 0 at the "Positioning address" before reaching 0 (immediate stop). |

### Designating the positioning address (位置決めアドレスの指定方法) (3.1 / original p.70)

The following shows the two methods for commanding the position in control using positioning data.

#### Absolute system (アブソリュート方式) (3.1 / original p.70)

Positioning is carried out to a designated position (absolute address) having the home position as a reference. This address is regarded as the positioning address. (The start point can be anywhere.)

[Figure] Absolute system (original p.70)
- Horizontal axis: Home position (Reference point), 100 (A point), 150 (B point), 300 (C point). The whole is "Within the stroke limit range". Legend: "• Start point", "→ End point".
- From the home position: "Address 100" → A point; "Address 150" → B point; "Address 300" → C point.
- From a point between B and C: "Address 100" → A point. From a point between the home position and A: "Address 150" → B point. From C point: "Address 100" → A point. From a point between B and C: "Address 150" → B point. (Regardless of the start point, the end point is the designated address.)

#### Incremental system (インクリメント方式) (3.1 / original p.70)

The position where the machine is currently stopped is regarded as the start point, and positioning is carried out for a designated movement amount in a designated movement direction.

[Figure] Incremental system (original p.70)
- Horizontal axis: Home position (Reference point), 100 (A point), 150 (B point), 250, 300 (C point). The whole is "Within the stroke limit range". Legend: "• Start point", "→ End point".
- From the home position: "Movement amount +100" → A point (100).
- From C point (300): "Movement amount -100" → 200.
- From B point (150): "Movement amount +100" → 250.
- From 250: "Movement amount -150" → A point (100).
- From B point (150): "Movement amount -100" → 50.

### Confirming the current value (現在値の確認) (3.1 / original p.71-72)

#### Values showing the current value (現在値を示す値) (3.1 / original p.71)

The following two types of addresses are used as values to show the position in the Simple Motion module/Motion module.
These addresses ("command position value" and "machine feed value") are stored in the monitor data area, and used in monitoring the current value display, etc.

| Command position value | Machine feed value |
|---|---|
| • This is the value stored in "[Md.20] Command position value".<br>• This value has an address established with a "machine home position return" as a reference, but the address can be changed by changing the current value to a new value. | • This is the value stored in "[Md.21] Machine feed value".<br>• This value always has an address established with a "machine home position return" as a reference. The address cannot be changed, even if the current value is changed to a new value. |

The "command position value" and "machine feed value" are used in monitoring the current value display, etc.

[Figure] Command position value and machine feed value at current value changing (original p.71)
- Speed waveform (V-t): a trapezoid starting at the "Home position"; at the stop point, label "Current value changed to 20000 with current value changing instruction".
- [Md.20] Command position value: 0 → 1 to → 10000 → 20000 (label "Address after the current value is changed is stored").
- [Md.21] Machine feed value: 0 → 1 to → 10000, stays 10000 (label "Address does not change even after the current value is changed").

#### Restriction (制約事項) (3.1 / original p.71)

Operation cycle error will occur in the current value refresh cycle when the stored "command position value" and "machine feed value" are used in the control.

#### Monitoring the current value (現在値のモニタ) (3.1 / original p.71-72)

The "command position value" and "machine feed value" are stored in the following buffer memory addresses, and can be read using a "DMOV(P) instruction" from the CPU module.
n: Axis No. - 1

| Monitor item (No.) | Monitor item (name) | Buffer memory addresses |
|---|---|---|
| [Md.20] | Command position value | 2400+100n<br>2401+100n |
| [Md.21] | Machine feed value | 2402+100n<br>2403+100n |

##### Program example (プログラム例) (3.1 / original p.72)

The following shows the program example that stores the command position value of the axis 1 in the specified device when X40 is turned ON.

[FX5-SSC-S]

```
(0)
LD    X40
DMOV  FX5SSC_1.stnAxMntr_D[0].dCommandPosition_D  dCommandPositionValue   ; source shown as U1\G2400
```

[FX5-SSC-G]

```
(0)
LD    bCommandPositionValueReadReq
DMOV  FX5SSC_1.stnAxMntr_D[0].dCommandPosition_D  dCommandPositionValue   ; source shown as U1\G2400
```

| Classification | Label name | Description |
|---|---|---|
| Module label | FX5SSC_1.stnAxMntr_D[0].dCommandPosition_D | Axis 1 Command position value |
| Global label, local label | Defines the global label or the local label as follows. The settings of Assign (Device/Label) are not required for the label that the assignment device is not set because the unused internal relay and data device are automatically assigned.<br>The following are for local labels. | (see the label table below) |

*In the original, the "Label name" and "Description" cells of the "Global label, local label" row are merged, and the label definition screen is embedded under the text. The screen is separated into the table below.

- Local label definition (from the screen image on original p.72)

| No. | Label Name | Data Type | Class |
|---|---|---|---|
| 1 | dCommandPositionValue | Double Word [Signed] | VAR |
| 2 | bCommandPositionValueReadReq | Bit | VAR |

### Control unit "degree" handling (制御単位「degree」の扱い) (3.1 / original p.73-75)

When the control unit is set to "degree", the following items differ from when other control units are set.

#### Command position value and machine feed value addresses (送り現在値，送り機械値のアドレス) (3.1 / original p.73)

The address of "[Md.20] Command position value" becomes a ring address from 0 to 359.99999°. The address of "[Md.21] Machine feed value" will become a cumulative value. (They will not have a ring structure for values between 0 and 359.99999°.)
However, "[Md.21] Machine feed value" is restored when the movement amount during the power supply OFF is added to the machine feed value before the power supply OFF (the rounded value within the range of 0 to 359.99999°) at the communication start with servo amplifier after the power supply ON or CPU module reset.

[Figure] Ring address (original p.73)
- Sawtooth: increases from 0° to 359.99999° and returns to 0°, repeatedly (0°, 359.99999°, 0°, 359.99999°, 0°).

#### Software stroke limit valid/invalid setting (ソフトウェアストロークリミットの有効／無効設定) (3.1 / original p.73)

With the control unit set to "degree", the software stroke limit upper and lower limit values are 0° to 359.99999°.

##### Setting to validate software stroke limit (ソフトウェアストロークリミットを有効とする場合の設定) (3.1 / original p.73)

To validate the software stroke limit, set the software stroke limit lower limit value and the upper limit value in a clockwise direction.

[Figure] Movement range in degree (original p.73)
- Circle with 0° at the top; radial lines at 315.00000° and 90.00000°. "Clockwise direction" arrow.
- Section A: the arc from 315.00000° clockwise through 0° to 90.00000°.
- Section B: the arc from 90.00000° clockwise (through 180°) to 315.00000°.

- To set the movement range A, set as follows.

| Setting item | Value |
|---|---|
| Software stroke limit lower limit value | 315.00000° |
| Software stroke limit upper limit value | 90.00000° |

- To set the movement range B, set as follows.

| Setting item | Value |
|---|---|
| Software stroke limit lower limit value | 90.00000° |
| Software stroke limit upper limit value | 315.00000° |

*In the original, these two tables have no header row.

##### Setting to invalidate software stroke limit (ソフトウェアストロークリミットを無効にする場合) (3.1 / original p.73)

To invalidate the software stroke limit, set the software stroke limit lower limit value equal to the software stroke limit upper limit value.
The control can be carried out irrespective of the setting of the software stroke limit.

> **Point**
> - When the upper/lower limit value of the axis which set the software stroke limit as valid are changed, perform the machine home position return after that.
> - When the software stroke limit is set as valid in the incremental data system, perform the machine home position return after power supply on.

#### Positioning control method when the control unit is set to "degree" (制御単位が「degree」の場合の位置決め制御方法) (3.1 / original p.74-75)

##### Absolute system (When the software stroke limit is invalid) (アブソリュート方式の場合(ソフトウェアストロークリミット無効時)) (3.1 / original p.74)

Positioning is carried out in the nearest direction to the designated address, using the current value as a reference. (This is called "shortcut control".)

Ex.
1) Positioning is carried out in a clockwise direction when the current value is moved from 315° to 45°.
2) Positioning is carried out in a counterclockwise direction when the current value is moved from 45° to 315°.

[Figure] Shortcut control (original p.74)
- "1) Moved from 315° to 45°": arrow from 315° clockwise over 0° to 45°.
- "2) Moved from 45° to 315°": arrow from 45° counterclockwise over 0° to 315°.

To designate the positioning direction (not carrying out the shortcut control), the shortcut control is invalidated and positioning in a designated direction is carried out by the "[Cd.40] ABS direction in degrees".
This function can perform only when the software stroke limit is invalid. When the software stroke limit is valid, the error "Illegal setting of ABS direction in unit of degree" (error code: 19A4H [FX5-SSC-S], or error code 1AA5H*1 [FX5-SSC-G]) occurs and positioning is not started.
*1 1AA4H for the software version 1.000.

To designate the movement direction in the ABS control, a "1" or "2" is written to the "[Cd.40] ABS direction in degrees" of the buffer memory (initial value: 0).
The value written to the "[Cd.40] ABS direction in degrees" becomes valid only when the positioning control is started.
In the continuous positioning control and continuous path control, the operation is continued with the setting set at the time of start even if the setting is changed during the operation.
n: Axis No. - 1

| Name | Function | Buffer memory address | Initial value |
|---|---|---|---|
| [Cd.40] ABS direction in degrees | The ABS movement direction in the unit of degree is designated.<br>0: Shortcut (direction setting invalid)<br>1: ABS clockwise<br>2: ABS counterclockwise | 4350+100n | 0 |

##### Absolute system (When the software stroke limit is valid) (アブソリュート方式の場合(ソフトウェアストロークリミット有効時)) (3.1 / original p.74)

The positioning is carried out in a clockwise/counterclockwise direction depending on the software stroke limit range setting method.
Because of this, positioning with "shortcut control" may not be possible.

Ex.
When the current value is moved from 0° to 315°, positioning is carried out in the clockwise direction if the software stroke limit lower limit value is 0° and the upper limit value is 345°.

[Figure] Positioning when the software stroke limit is valid (original p.74)
- Circle with marks at 0°, 345.00000° and 315.00000°. A thick arrow runs from 0° clockwise all the way around to 315.00000°. Label: "Positioning carried out in the clockwise direction."

> **Point**
> Positioning addresses are within a range of 0° to 359.99999°.
> Use the incremental system to carry out positioning of one rotation or more.

##### Incremental system (インクリメント方式の場合) (3.1 / original p.75)

Positioning is carried out for a designated movement amount in a designated movement direction when in the incremental system of positioning.
The movement direction is determined by the sign (+, -) of the movement amount.

| Movement direction | Rotation direction |
|---|---|
| For a positive (+) movement direction | Clockwise |
| For a negative (-) movement direction | Counterclockwise |

*In the original, this table has no header row (header added here).

> **Point**
> Positioning of 360° or more can be carried out with the incremental system.
> At this time, set as shown below to invalidate the software stroke limit.
> [Software stroke limit upper limit value = Software stroke limit lower limit value]
> Set the value within the setting range (0° to 359.99999°).

### Interpolation control (補間制御) (3.1 / original p.76-78)

#### Meaning of interpolation control (補間制御とは) (3.1 / original p.76)

In "2-axis linear interpolation control", "3-axis linear interpolation control", "4-axis linear interpolation control", "2-axis fixed-feed control", "3-axis fixed-feed control", "4-axis fixed-feed control", "2-axis speed control", "3-axis speed control", "4-axis speed control", and "2-axis circular interpolation control", control is carried out so that linear and arc paths are drawn using a motor set in two to four axis directions. This kind of control is called "interpolation control".
In interpolation control, the axis in which the control method is set is defined as the "reference axis", and the other axis is defined as the "interpolation axis".
The Simple Motion module/Motion module controls the "reference axis" following the positioning data set in the "reference axis", and controls the "interpolation axis" corresponding to the reference axis control so that a linear or arc path is drawn.
The following table shows the reference axis and interpolation axis combinations.

| Interpolation of "[Da.2] Control method" | Axis definition: Reference axis | Axis definition: Interpolation axis |
|---|---|---|
| 2-axis linear interpolation control<br>2-axis fixed-feed control<br>2-axis circular interpolation control<br>2-axis speed control | 4-axis module: Any of axes 1 to 4<br>8-axis module: Any of axes 1 to 8 | "Axis to be interpolated No.1" set in reference axis |
| 3-axis linear interpolation control<br>3-axis fixed-feed control<br>3-axis speed control | 4-axis module: Any of axes 1 to 4<br>8-axis module: Any of axes 1 to 8 | "Axis to be interpolated No.1" and "Axis to be interpolated No.2" set in reference axis |
| 4-axis linear interpolation control<br>4-axis fixed-feed control<br>4-axis speed control | 4-axis module: Any of axes 1 to 4<br>8-axis module: Any of axes 1 to 8 | "Axis to be interpolated No.1", "Axis to be interpolated No.2" and "Axis to be interpolated No.3" set in reference axis |

*In the original, "Axis definition" is a 2-level header over "Reference axis" / "Interpolation axis", and the "Reference axis" cell is merged over the 3 rows. Expanded to each row.

#### Setting positioning data (設定する位置決めデータ) (3.1 / original p.76-77)

When carrying out interpolation control, the same positioning data Nos. are set for the "reference axis" and the "interpolation axis". The following table shows the "positioning data" setting items for the reference axis and interpolation axis.
◎: Setting always required, ○: Set according to requirements (Set to "—" when not used.), △: Setting restrictions exist
—: Setting not required (Use the initial value or a value within the setting range.)

| Setting item (group) | Setting item (No.) | Setting item (name) | Reference axis setting item | Interpolation axis setting item |
|---|---|---|---|---|
| Same positioning data Nos. | [Da.1] | Operation pattern | ◎ | — |
| Same positioning data Nos. | [Da.2] | Control method | Linear 2, 3, 4<br>Fixed-feed 2, 3, 4<br>Circular sub, Circular right, Circular left<br>Forward run speed 2, 3, 4<br>Reverse run speed 2, 3, 4 | — |
| Same positioning data Nos. | [Da.3] | Acceleration time No. | ◎ | — |
| Same positioning data Nos. | [Da.4] | Deceleration time No. | ◎ | — |
| Same positioning data Nos. | [Da.6] | Positioning address/movement amount | △<br>(Forward run speed 2, 3, and 4. Reverse run speed 2, 3, and 4 not required.) | △<br>(Forward run speed 2, 3, and 4. Reverse run speed 2, 3, and 4 not required.) |
| Same positioning data Nos. | [Da.7] | Arc address | △<br>(Only during circular sub, circular right, and circular left). | △<br>(Only during circular sub, circular right, and circular left). |
| Same positioning data Nos. | [Da.8] | Command speed | ◎ | △<br>(Only during forward run speed 2, 3, 4 and reverse run speed 2, 3, 4). |
| Same positioning data Nos. | [Da.9] | Dwell time/JUMP destination positioning data No. | ○ | — |
| Same positioning data Nos. | [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | ○ | — |
| Same positioning data Nos. | [Da.20] | Axis to be interpolated No.1 | ○*1 | — |
| Same positioning data Nos. | [Da.21] | Axis to be interpolated No.2 | ○*1 | — |
| Same positioning data Nos. | [Da.22] | Axis to be interpolated No.3 | ○*1 | — |

*In the original, "Same positioning data Nos." is merged over all 11 rows. Expanded to each row.

*1 The axis No. is set to axis to be interpolated No.1 for 2-axis linear interpolation, to axis to be interpolated No.1 and No.2 for 3-axis linear interpolation, and to axis to be interpolated No.1 to No.3 for 4-axis linear interpolation.
If the self-axis is set, the error "Illegal interpolation description command" (error code: 1A22H [FX5-SSC-S], or error code 1B22H [FX5-SSC-G]) will occur. The axes that are not used are not required.

Refer to the following for information on the setting details.
→Page 497 Positioning Data

#### Starting the interpolation control (補間制御の始動) (3.1 / original p.77)

The positioning data Nos. of the reference axis (axis in which interpolation control was set in "[Da.2] Control method") are started when starting the interpolation control. (Starting of the interpolation axis is not required.)
The following errors or warnings will occur and the positioning will not start if both reference axis and the interpolation axis are started.
- Reference axis: Interpolation while interpolation axis BUSY (error code: 1998H [FX5-SSC-S], or error code 1A98H [FX5-SSC-G])
- Interpolation axis: Control method setting error (error code: 1A24H [FX5-SSC-S], or error code 1B24H [FX5-SSC-G]), start during operation (warning code: 0900H [FX5-SSC-S], or warning code 0D00H [FX5-SSC-G]).

#### Interpolation control continuous positioning (補間制御の連続位置決め) (3.1 / original p.77)

When carrying out interpolation control in which "continuous positioning control" and "continuous path control" are designated in the operation pattern, the positioning method for all positioning data from the started positioning data to the positioning data in which "positioning complete" is set must be set to interpolation control.
The number of the interpolation axes and axes to be interpolated cannot be changed from the intermediate positioning data. When the number of the interpolation axes and axes to be interpolated are changed, the error "Control method setting error" (error code: 1A24H [FX5-SSC-S], or error code 1B25H*1 [FX5-SSC-G]) will occur and the positioning will stop.
*1 1B24H for the software version 1.000.

#### Speed during interpolation control (補間制御時の速度) (3.1 / original p.77)

Either the "composite speed" or "reference axis speed" can be designated as the speed during interpolation control.
([Pr.20] Interpolation speed designation method)
Only the "reference axis speed" can be designated in the following interpolation control.
When a "composite speed" is set and positioning is started, the error "Interpolation mode error" (error code: 199AH [FX5-SSC-S], or error code 1A9AH [FX5-SSC-G]) occurs, and the system will not start.
- 4-axis linear interpolation
- 2-axis speed control
- 3-axis speed control
- 4-axis speed control

#### Cautions (注意事項) (3.1 / original p.77)

- If any axis exceeds "[Pr.8] Speed limit value" during 2- to 4-axis speed control, the axis exceeding the speed limit value is controlled with the speed limit value. The speeds of the other axes being interpolated are suppressed by the command speed ratio.
- If the reference axis exceeds "[Pr.8] Speed limit value" during 2-axis circular interpolation control, the reference axis is controlled with the speed limit value. (The speed limit does not function on the interpolation axis side.)
- If any axis exceeds "[Pr.8] Speed limit value" during 2- to 4-axis linear interpolation control or 2- to 4-axis fixed-feed control, the axis exceeding the speed limit value is controlled with the speed limit value. The speeds of the other axes being interpolated are suppressed by the movement amount ratio.
- In 2- to 4-axis interpolation, you cannot change the combination of interpolated axes midway through operation.

> **Point**
> When the "reference axis speed" is set during interpolation control, set so the major axis side becomes the reference axis. If the minor axis side is set as the reference axis, the major axis side speed may exceed the "[Pr.8] Speed limit value".

#### Limits to interpolation control (補間制御の制限) (3.1 / original p.78)

There are limits to the interpolation control that can be executed and speed ([Pr.20] Interpolation speed designation method) that can be set, depending on the "[Pr.1] Unit setting" of the reference axis and interpolation axis. (For example, 2-axis circular interpolation control cannot be executed if the reference axis and interpolation axis units differ.)
The following table shows the interpolation control and speed designation limits.
○: Setting possible, ×: Setting not possible.

| "[Da.2] Control method" interpolation control | [Pr.20] Interpolation speed designation method | [Pr.1] Unit setting*1: Reference axis and interpolation axis units are the same, or a combination of "mm" and "inch".*2 | [Pr.1] Unit setting*1: Reference axis and interpolation axis units differ*3 |
|---|---|---|---|
| Linear 2 (ABS, INC)<br>Fixed-feed 2 | Composite speed | ○ | × |
| Linear 2 (ABS, INC)<br>Fixed-feed 2 | Reference axis speed | ○ | ○ |
| Circular sub (ABS, INC)<br>Circular right (ABS, INC)<br>Circular left (ABS, INC) | Composite speed | ○*3 | × |
| Circular sub (ABS, INC)<br>Circular right (ABS, INC)<br>Circular left (ABS, INC) | Reference axis speed | × | × |
| Linear 3 (ABS, INC)<br>Fixed-feed 3 | Composite speed | ○ | × |
| Linear 3 (ABS, INC)<br>Fixed-feed 3 | Reference axis speed | ○ | ○ |
| Linear 4 (ABS, INC)<br>Fixed-feed 4 | Composite speed | × | × |
| Linear 4 (ABS, INC)<br>Fixed-feed 4 | Reference axis speed | ○ | ○ |
| 2- to 4-axis speed control | Composite speed | × | × |
| 2- to 4-axis speed control | Reference axis speed | ○ | ○ |

*In the original, "[Pr.1] Unit setting*1" is a 2-level header over the last 2 columns, and each "[Da.2] Control method" cell is merged over its 2 rows (Composite speed / Reference axis speed). Expanded to each row.

*1 "mm" and "inch" unit mix possible.
When "mm" and "inch" are mixed, convert as follows for the positioning.
If interpolation control units are "mm", positioning is controlled by calculating position commands from the address, travel value, positioning speed and electronic gear, which have been converted to "mm" using the formula: inch setting value × 25.4 = mm setting value.
If interpolation control units are "inch", positioning is controlled by calculating position commands from the address, travel value, positioning speed and electronic gear, which have been converted to "inch" using the formula: mm setting value/25.4 = inch setting value.
*2 The unit set in the reference axis will be used for the speed unit during control if the units differ or if "mm" and "inch" are combined.
*3 "degree" setting not possible.
The error "Circular interpolation not possible" (error code: 199FH [FX5-SSC-S], or error code 1A9FH [FX5-SSC-G]) will occur and the positioning control does not start if 2-axis circular interpolation control is set when the unit is "degree".
The machine will immediately stop if "degree" is set during positioning control.

#### Axis operation status during interpolation control (補間制御中の軸動作状態) (3.1 / original p.78)

"Interpolation" will be stored in the "[Md.26] Axis operation status" during interpolation control. "Standby" will be stored when the interpolation operation is terminated. Both the reference axis and interpolation axis will carry out a deceleration stop if an error occurs during control, and "Error" will be stored in the operation status.

## 3.2 Setting the Positioning Data (位置決めデータの設定) (3.2 / original p.79-95, this part up to Fixed-feed control)

### Relation between each control and positioning data (各制御と位置決めデータの関係) (3.2 / original p.79-81)

The setting requirements and details for the setting items of the positioning data to be set differ according to the "[Da.2] Control method".
The following table shows the positioning data setting items corresponding to the different types of control.
(In this section, it is assumed that the positioning data setting is carried out using an engineering tool.)
◎: Always set
○: Set as required ("—" when not required)
×: Setting not possible (If set, the error "Continuous path control not possible" (error code: 1A1EH [FX5-SSC-S], or error codes 1B1EH to 1B20H [FX5-SSC-G]) will occur at start.)
—: Setting not required (When the value is the default value or within the setting range, there is no problem.)

- Position control / 1 to 4 axis speed control (original p.79)

| Positioning data (No.) | Positioning data (item) | Positioning data (sub item) | Position control: 1-axis linear control / 2/3/4-axis linear interpolation control | Position control: 1/2/3/4-axis fixed-feed control | Position control: 2-axis circular interpolation control | 1 to 4 axis speed control |
|---|---|---|---|---|---|---|
| [Da.1] | Operation pattern | Independent positioning control (Positioning complete) | ◎ | ◎ | ◎ | ◎ |
| [Da.1] | Operation pattern | Continuous positioning control | ◎ | ◎ | ◎ | × |
| [Da.1] | Operation pattern | Continuous path control | ◎ | × | ◎ | × |
| [Da.2] | Control method | — | Linear 1<br>Linear 2<br>Linear 3<br>Linear 4<br>*1 | Fixed-feed 1<br>Fixed-feed 2<br>Fixed-feed 3<br>Fixed-feed 4 | Circular sub<br>Circular right<br>Circular left<br>*1 | Forward run speed 1<br>Reverse run speed 1<br>Forward run speed 2<br>Reverse run speed 2<br>Forward run speed 3<br>Reverse run speed 3<br>Forward run speed 4<br>Reverse run speed 4 |
| [Da.3] | Acceleration time No. | — | ◎ | ◎ | ◎ | ◎ |
| [Da.4] | Deceleration time No. | — | ◎ | ◎ | ◎ | ◎ |
| [Da.6] | Positioning address/movement amount | — | ◎ | ◎ | ◎ | — |
| [Da.7] | Arc address | — | — | — | ◎ | — |
| [Da.8] | Command speed | — | ◎ | ◎ | ◎ | ◎ |
| [Da.9] | Dwell time/JUMP destination positioning data No. | — | ○ | ○ | ○ | — |
| [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | — | ○ | ○ | ○ | ○ |
| [Da.20] | Axis to be interpolated No.1 | — | ◎: 2 axes, 3 axes, 4 axes, —: 1 axis | ◎: 2 axes, 3 axes, 4 axes, —: 1 axis | ◎: 2 axes, 3 axes, 4 axes, —: 1 axis | ◎: 2 axes, 3 axes, 4 axes, —: 1 axis |
| [Da.21] | Axis to be interpolated No.2 | — | ◎: 3 axes, 4 axes, —: 1 axis, 2 axes | ◎: 3 axes, 4 axes, —: 1 axis, 2 axes | ◎: 3 axes, 4 axes, —: 1 axis, 2 axes | ◎: 3 axes, 4 axes, —: 1 axis, 2 axes |
| [Da.22] | Axis to be interpolated No.3 | — | ◎: 4 axes, —: 1 axis, 2 axes, 3 axes | ◎: 4 axes, —: 1 axis, 2 axes, 3 axes | ◎: 4 axes, —: 1 axis, 2 axes, 3 axes | ◎: 4 axes, —: 1 axis, 2 axes, 3 axes |

*In the original, "Positioning data" is a header spanning 3 columns (the "sub item" column is used only by [Da.1]; "—" in that column here means the cell does not exist in the original). "[Da.1]" and "Operation pattern" are merged over 3 rows. "Position control" is a 2-level header over 3 columns. The cells of [Da.20], [Da.21] and [Da.22] are each merged across all 4 control columns. Expanded to each row/column.

*1 Two control systems are available: the absolute (ABS) system and incremental (INC) system.

- Speed-position switching control / Position-speed switching control (original p.80)

| Positioning data (No.) | Positioning data (item) | Positioning data (sub item) | Speed-position switching control | Position-speed switching control |
|---|---|---|---|---|
| [Da.1] | Operation pattern | Independent positioning control (Positioning complete) | ◎ | ◎ |
| [Da.1] | Operation pattern | Continuous positioning control | ◎ | × |
| [Da.1] | Operation pattern | Continuous path control | × | × |
| [Da.2] | Control method | — | Forward run speed/position<br>Reverse run speed/position<br>*1 | Forward run position/speed<br>Reverse run position/speed |
| [Da.3] | Acceleration time No. | — | ◎ | ◎ |
| [Da.4] | Deceleration time No. | — | ◎ | ◎ |
| [Da.6] | Positioning address/movement amount | — | ◎ | ◎ |
| [Da.7] | Arc address | — | — | — |
| [Da.8] | Command speed | — | ◎ | ◎ |
| [Da.9] | Dwell time/JUMP destination positioning data No. | — | ○ | ○ |
| [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | — | ○ | ○ |
| [Da.20] | Axis to be interpolated No.1 | — | — | — |
| [Da.21] | Axis to be interpolated No.2 | — | — | — |
| [Da.22] | Axis to be interpolated No.3 | — | — | — |

*In the original, "[Da.1]" and "Operation pattern" are merged over 3 rows. Expanded to each row. ("—" in the "sub item" column means the cell does not exist in the original.)

- Other control (original p.80)

| Positioning data (No.) | Positioning data (item) | Positioning data (sub item) | NOP instruction | Current value changing | JUMP instruction | LOOP | LEND |
|---|---|---|---|---|---|---|---|
| [Da.1] | Operation pattern | Independent positioning control (Positioning complete) | — | ◎ | — | — | — |
| [Da.1] | Operation pattern | Continuous positioning control | — | ◎ | — | — | — |
| [Da.1] | Operation pattern | Continuous path control | — | × | — | — | — |
| [Da.2] | Control method | — | NOP | Current value changing | JUMP instruction | LOOP | LEND |
| [Da.3] | Acceleration time No. | — | — | — | — | — | — |
| [Da.4] | Deceleration time No. | — | — | — | — | — | — |
| [Da.6] | Positioning address/movement amount | — | — | New address | — | — | — |
| [Da.7] | Arc address | — | — | — | — | — | — |
| [Da.8] | Command speed | — | — | — | — | — | — |
| [Da.9] | Dwell time/JUMP destination positioning data No. | — | — | — | JUMP destination positioning data No. | — | — |
| [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | — | — | ○ | JUMP condition data No. | Number of LOOP to LEND repetitions | — |
| [Da.20] | Axis to be interpolated No.1 | — | — | — | — | — | — |
| [Da.21] | Axis to be interpolated No.2 | — | — | — | — | — | — |
| [Da.22] | Axis to be interpolated No.3 | — | — | — | — | — | — |

*In the original, "Other control" is a 2-level header over the 5 control columns, and "[Da.1]" and "Operation pattern" are merged over 3 rows. Expanded to each row. ("—" in the "sub item" column means the cell does not exist in the original.)

*1 Two control systems are available: the absolute (ABS) system and incremental (INC) system.

> **Point**
> It is recommended that the "positioning data" be set whenever possible with an engineering tool. Execution by a program uses many programs and devices. The execution becomes complicated, and the scan times will increase.

### 1-axis linear control (1軸直線制御) (3.2 / original p.81-82)

In "1-axis linear control" ("[Da.2] Control method" = ABS linear 1, INC linear 1), one motor is used to carry out position control in a set axis direction.

#### 1-axis linear control (ABS linear 1) (1軸直線制御(ABS直線1)) (3.2 / original p.81)

##### Operation chart (動作図) (3.2 / original p.81)

In absolute system 1-axis linear control, positioning is carried out from the current stop position (start point address) to the address (end point address) set in "[Da.6] Positioning address/movement amount".

Ex.
When the start point address (current stop position) is 1000, and the end point address (positioning address) is 8000, positioning is carried out in the positive direction for a movement amount of 7000 (8000 - 1000)

[Figure] ABS linear 1 example (original p.81)
- Number line: 0, 1000 ("Start point address (current stop position)"), 8000 ("End point address (positioning address)").
- Arrow from 1000 to 8000: "Positioning control (movement amount 7000)".

##### Setting positioning data (設定する位置決めデータ) (3.2 / original p.81)

When using 1-axis linear control (ABS linear 1), set the following positioning data.
◎: Always set, ○: Set as required, —: Setting not required

| Setting item (No.) | Setting item (name) | Setting required/not required |
|---|---|---|
| [Da.1] | Operation pattern | ◎ |
| [Da.2] | Control method | ◎<br>(Set ABS linear 1.) |
| [Da.3] | Acceleration time No. | ◎ |
| [Da.4] | Deceleration time No. | ◎ |
| [Da.6] | Positioning address/movement amount | ◎ |
| [Da.7] | Arc address | — |
| [Da.8] | Command speed | ◎ |
| [Da.9] | Dwell time/JUMP destination positioning data No. | ○ |
| [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | ○ |
| [Da.20] | Axis to be interpolated No.1 | — |
| [Da.21] | Axis to be interpolated No.2 | — |
| [Da.22] | Axis to be interpolated No.3 | — |

Refer to the following for information on the setting details.
→Page 497 Positioning Data

#### 1-axis linear control (INC linear 1) (1軸直線制御(INC直線1)) (3.2 / original p.82)

##### Operation chart (動作図) (3.2 / original p.82)

In incremental system 1-axis linear control, positioning is carried out from the current stop position (start point address) to a position at the end of the movement amount set in "[Da.6] Positioning address/movement amount". The movement direction is determined by the sign of the movement amount.

[Figure] Movement direction (original p.82)
- Horizontal line with "Reverse direction" on the left and "Forward direction" on the right; "Start point address (current stop position)" in the middle.
- "Movement direction for a negative movement amount" = toward the left (reverse); "Movement direction for a positive movement amount" = toward the right (forward).

Ex.
When the start point address is 5000, and the movement amount is -7000, positioning is carried out to the -2000 position.

[Figure] INC linear 1 example (original p.82)
- Number line: -3000, -2000, -1000, 0, 1000, 2000, 3000, 4000, 5000, 6000.
- Start point address (current stop position) = 5000; Stop address after the positioning control = -2000.
- Arrow from 5000 to -2000: "Positioning control in the reverse direction (movement amount -7000)".

##### Setting positioning data (設定する位置決めデータ) (3.2 / original p.82)

When using 1-axis linear control (INC linear 1), set the following positioning data.
◎: Always set, ○: Set as required, —: Setting not required

| Setting item (No.) | Setting item (name) | Setting required/not required |
|---|---|---|
| [Da.1] | Operation pattern | ◎ |
| [Da.2] | Control method | ◎<br>(Set INC linear 1.) |
| [Da.3] | Acceleration time No. | ◎ |
| [Da.4] | Deceleration time No. | ◎ |
| [Da.6] | Positioning address/movement amount | ◎ |
| [Da.7] | Arc address | — |
| [Da.8] | Command speed | ◎ |
| [Da.9] | Dwell time/JUMP destination positioning data No. | ○ |
| [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | ○ |
| [Da.20] | Axis to be interpolated No.1 | — |
| [Da.21] | Axis to be interpolated No.2 | — |
| [Da.22] | Axis to be interpolated No.3 | — |

Refer to the following for information on the setting details.
→Page 497 Positioning Data

### 2-axis linear interpolation control (2軸直線補間制御) (3.2 / original p.83-86)

In "2-axis linear interpolation control" ("[Da.2] Control method" = ABS linear 2, INC linear 2), two motors are used to carry out position control in a linear path while carrying out interpolation for the axis directions set in each axis. (Refer to →Page 74 Interpolation control for details on interpolation control.)

#### 2-axis linear interpolation control (ABS linear 2) (2軸直線補間制御(ABS直線2)) (3.2 / original p.83-84)

##### Operation chart (動作図) (3.2 / original p.83)

In absolute system 2-axis linear interpolation control, the designated 2 axes are used. Linear interpolation positioning is carried out from the current stop position (start point address) to the address (end point address) set in "[Da.6] Positioning address/movement amount".

[Figure] ABS linear 2 operation chart (original p.83)
- X axis: "Reverse direction" (left) / "Forward direction (X axis)" (right); Y axis: "Forward direction (Y axis)" (up) / "Reverse direction" (down).
- "Start point address (X1, Y1) (current stop position)" → "End point address (X2, Y2) (positioning address)" along a straight line labeled "Movement by linear interpolation of the X axis and Y axis".
- "X axis movement amount" = X1 to X2; "Y axis movement amount" = Y1 to Y2.

Ex.
When the start point address (current stop position) is (1000, 1000) and the end point address (positioning address) is (10000, 4000), positioning is carried out as follows.

[Figure] ABS linear 2 example (original p.83)
- Axis 1 (horizontal): 0, 1000, 5000, 10000. Axis 2 (vertical): 1000, 4000.
- Start point address (current stop position) = (1000, 1000); End point address (positioning address) = (10000, 4000); straight-line movement.
- "Axis 1 movement amount (10000 - 1000 = 9000)", "Axis 2 movement amount (4000 - 1000 = 3000)".

##### Restrictions (制約事項) (3.2 / original p.83)

An error will occur and the positioning will not start in the following cases. The machine will immediately stop if the error is detected during a positioning control.
- If the movement amount of each axis exceeds "1073741824 (= 2^30)" when "0: Composite speed" is set in "[Pr.20] Interpolation speed designation method", the error "Outside linear movement amount range" (error code: 1A15H [FX5-SSC-S], or error code 1B15H [FX5-SSC-G]) occurs at a positioning start. (The maximum movement amount that can be set in "[Da.6] Positioning address/movement amount" is "1073741824 (= 2^30)".)

##### Setting positioning data (設定する位置決めデータ) (3.2 / original p.84)

When using 2-axis linear interpolation control (ABS linear 2), set the following positioning data.
◎: Always set, ○: Set as required, —: Setting not required

| Setting item (No.) | Setting item (name) | Setting required/not required for the reference axis | Setting required/not required for the interpolation axis |
|---|---|---|---|
| [Da.1] | Operation pattern | ◎ | — |
| [Da.2] | Control method | ◎<br>(Set ABS linear 2.) | — |
| [Da.3] | Acceleration time No. | ◎ | — |
| [Da.4] | Deceleration time No. | ◎ | — |
| [Da.6] | Positioning address/movement amount | ◎ | ◎ |
| [Da.7] | Arc address | — | — |
| [Da.8] | Command speed | ◎ | — |
| [Da.9] | Dwell time/JUMP destination positioning data No. | ○ | — |
| [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | ○ | — |
| [Da.20] | Axis to be interpolated No.1 | ◎ | — |
| [Da.21] | Axis to be interpolated No.2 | — | — |
| [Da.22] | Axis to be interpolated No.3 | — | — |

Refer to the following for information on the setting details.
→Page 497 Positioning Data

> **Restriction**
> When the "reference axis speed" is set during 2-axis linear interpolation control, set so the major axis side becomes the reference axis. If the minor axis side is set as the reference axis, the major axis side speed may exceed the "[Pr.8] Speed limit value".

#### 2-axis linear interpolation control (INC linear 2) (2軸直線補間制御(INC直線2)) (3.2 / original p.85-86)

##### Operation chart (動作図) (3.2 / original p.85)

In incremental system 2-axis linear interpolation control, the designated 2 axes are used. Linear interpolation positioning is carried out from the current stop position (start point address) to a position at the end of the movement amount set in "[Da.6] Positioning address/movement amount". The movement direction is determined by the sign of the movement amount.
- Positive movement amount: Positioning control to forward direction (Address increase direction)
- Negative movement amount: Positioning control to reverse direction (Address decrease direction)

[Figure] INC linear 2 operation chart (original p.85)
- X axis: "Reverse direction" / "Forward direction (X axis)"; Y axis: "Forward direction (Y axis)" / "Reverse direction".
- "Start point address (X1, Y1) (current stop position)" → "Stop address after the positioning control (X2, Y2)" along a straight line labeled "Movement by linear interpolation positioning of the X axis and Y axis".
- "X axis movement amount" = X1 to X2; "Y axis movement amount" = Y1 to Y2.

Ex.
When the axis 1 movement amount is 9000 and the axis 2 movement amount is -3000, positioning address (10000, 4000) is carried out as follows.

[Figure] INC linear 2 example (original p.85)
- Axis 1 (horizontal): 0, 5000, 10000. Axis 2 (vertical): 1000, 4000.
- Start point address (current stop position) is at axis 2 = 4000 (axis 1 near 1000); Stop address after the positioning control is at axis 1 = 10000, axis 2 = 1000 (line goes down to the right).
- "Axis 1 movement amount (9000)", "Axis 2 movement amount (-3000)".

*(Converter note, not in the original: the figure shows movement from (1000, 4000) to (10000, 1000), consistent with the movement amounts 9000 / -3000; the example sentence reads "positioning address (10000, 4000)" as printed.)

##### Restrictions (制約事項) (3.2 / original p.85)

An error will occur and the positioning will not start in the following cases. The machine will immediately stop if the error is detected during a positioning operation.
- If the movement amount of each axis exceeds "1073741824 (= 2^30)" when "0: Composite speed" is set in "[Pr.20] Interpolation speed designation method", the error "Outside linear movement amount range" (error code: 1A15H [FX5-SSC-S], or error code 1B15H [FX5-SSC-G]) occurs at a positioning start. (The maximum movement amount that can be set in "[Da.6] Positioning address/movement amount" is "1073741824 (= 2^30)".)

##### Setting positioning data (設定する位置決めデータ) (3.2 / original p.86)

When using 2-axis linear interpolation control (INC linear 2), set the following positioning data.
◎: Always set, ○: Set as required, —: Setting not required

| Setting item (No.) | Setting item (name) | Setting required/not required for the reference axis | Setting required/not required for the interpolation axis |
|---|---|---|---|
| [Da.1] | Operation pattern | ◎ | — |
| [Da.2] | Control method | ◎<br>(Set INC linear 2.) | — |
| [Da.3] | Acceleration time No. | ◎ | — |
| [Da.4] | Deceleration time No. | ◎ | — |
| [Da.6] | Positioning address/movement amount | ◎ | ◎ |
| [Da.7] | Arc address | — | — |
| [Da.8] | Command speed | ◎ | — |
| [Da.9] | Dwell time/JUMP destination positioning data No. | ○ | — |
| [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | ○ | — |
| [Da.20] | Axis to be interpolated No.1 | ◎ | — |
| [Da.21] | Axis to be interpolated No.2 | — | — |
| [Da.22] | Axis to be interpolated No.3 | — | — |

Refer to the following for information on the setting details.
→Page 497 Positioning Data

> **Restriction**
> When the "reference axis speed" is set during 2-axis linear interpolation control, set so the major axis side becomes the reference axis. If the minor axis side is set as the reference axis, the major axis side speed may exceed the "[Pr.8] Speed limit value".

### 3-axis linear interpolation control (3軸直線補間制御) (3.2 / original p.87-90)

In "3-axis linear interpolation control" ("[Da.2] Control method" = ABS linear 3, INC linear 3), three motors are used to carry out position control in a linear path while carrying out interpolation for the axis directions set in each axis.
(Refer to →Page 74 Interpolation control for details on interpolation control.)

#### 3-axis linear interpolation control (ABS linear 3) (3軸直線補間制御(ABS直線3)) (3.2 / original p.87-88)

##### Operation chart (動作図) (3.2 / original p.87)

In the absolute system 3-axis linear interpolation control, the designated 3 axes are used. Linear interpolation positioning is carried out from the current stop position (start point address) to the address (end point address) set in the "[Da.6] Positioning address/movement amount".

[Figure] ABS linear 3 operation chart (original p.87)
- 3D axes: "Forward direction (X axis)" / "Reverse direction"; "Forward direction (Y axis)" / "Reverse direction"; "Forward direction (Z axis)" / "Reverse direction".
- "Start point address (X1, Y1, Z1) (current stop position)" → "End point address (X2, Y2, Z2) (positioning address)" along a straight line labeled "Movement by linear interpolation of the X axis, Y axis and Z axis".
- "X axis movement amount", "Y axis movement amount", "Z axis movement amount" shown as the box edges.

Ex.
When the start point address (current stop position) is (1000, 2000, 1000) and the end point address (positioning address) is (4000, 8000, 4000), positioning is carried out as follows.

[Figure] ABS linear 3 example (original p.87)
- Axis 1: 0, 1000, 4000; Axis 2: 2000, 8000; Axis 3: 1000, 4000.
- Start point address (current stop position) → End point address (positioning address).
- "Axis 1 movement amount (4000 - 1000 = 3000)", "Axis 2 movement amount (8000 - 2000 = 6000)", "Axis 3 movement amount (4000 - 1000 = 3000)".

##### Restrictions (制約事項) (3.2 / original p.87)

An error will occur and the positioning will not start in the following cases. The machine will immediately stop if the error is detected during a positioning control.
- If the movement amount of each axis exceeds "1073741824 (= 2^30)" when "0: Composite speed" is set in "[Pr.20] Interpolation speed designation method", the error "Outside linear movement amount range" (error code: 1A15H [FX5-SSC-S], or error code 1B15H [FX5-SSC-G]) occurs at a positioning start. (The maximum movement amount that can be set in "[Da.6] Positioning address/movement amount" is "1073741824 (= 2^30)".)

##### Setting positioning data (設定する位置決めデータ) (3.2 / original p.88)

When using 3-axis linear interpolation control (ABS linear 3), set the following positioning data.
◎: Always set, ○: Set as required, —: Setting not required

| Setting item (No.) | Setting item (name) | Setting required/not required for the reference axis | Setting required/not required for the interpolation axis |
|---|---|---|---|
| [Da.1] | Operation pattern | ◎ | — |
| [Da.2] | Control method | ◎<br>(Set ABS linear 3.) | — |
| [Da.3] | Acceleration time No. | ◎ | — |
| [Da.4] | Deceleration time No. | ◎ | — |
| [Da.6] | Positioning address/movement amount | ◎ | ◎ |
| [Da.7] | Arc address | — | — |
| [Da.8] | Command speed | ◎ | — |
| [Da.9] | Dwell time/JUMP destination positioning data No. | ○ | — |
| [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | ○ | — |
| [Da.20] | Axis to be interpolated No.1 | ◎ | — |
| [Da.21] | Axis to be interpolated No.2 | ◎ | — |
| [Da.22] | Axis to be interpolated No.3 | — | — |

Refer to the following for information on the setting details.
→Page 497 Positioning Data

> **Restriction**
> - When the "reference axis speed" is set during 3-axis linear interpolation control, set so the major axis side becomes the reference axis. If the minor axis side is set as the reference axis, the major axis side speed may exceed the "[Pr.8] Speed limit value".
> - Refer to →Page 74 Interpolation control for the reference axis and interpolation axis combinations.

#### 3-axis linear interpolation control (INC linear 3) (3軸直線補間制御(INC直線3)) (3.2 / original p.89-90)

##### Operation chart (動作図) (3.2 / original p.89)

In the incremental system 3-axis linear interpolation control, the designated 3 axes are used. Linear interpolation positioning is carried out from the current stop position (start point address) to a position at the end of the movement amount set in the "[Da.6] Positioning address/movement amount". The movement direction is determined the sign of the movement amount.
- Positive movement amount: Positioning control to forward direction (Address increase direction)
- Negative movement amount: Positioning control to reverse direction (Address decrease direction)

[Figure] INC linear 3 operation chart (original p.89)
- 3D axes with "Forward direction" / "Reverse direction" on each axis.
- "Start point address (X1, Y1, Z1) (current stop position)" → point (X2, Y2, Z2) along a straight line labeled "Movement by linear interpolation positioning of the X axis, Y axis and Z axis".
- "X axis movement amount", "Y axis movement amount", "Z axis movement amount" shown as the box edges.

Ex.
When the axis 1 movement amount is 10000, the axis 2 movement amount is 5000 and the axis 3 movement amount is 6000, positioning is carried out as follows.

[Figure] INC linear 3 example (original p.89)
- Axis 1: 5000, 10000; Axis 2: 5000; Axis 3: 6000.
- Start point address (current stop position) → "Stop address after the positioning control".
- "Axis 1 movement amount (10000)", "Axis 2 movement amount (5000)", "Axis 3 movement amount (6000)".

##### Restrictions (制約事項) (3.2 / original p.89)

An error will occur and the positioning will not start in the following cases. The machine will immediately stop if the error is detected during a positioning operation.
- If the movement amount of each axis exceeds "1073741824 (= 2^30)" when "0: Composite speed" is set in "[Pr.20] Interpolation speed designation method", the error "Outside linear movement amount range" (error code: 1A15H [FX5-SSC-S], or error code 1B15H [FX5-SSC-G]) occurs at a positioning start. (The maximum movement amount that can be set in "[Da.6] Positioning address/movement amount" is "1073741824 (= 2^30)".)

##### Setting positioning data (設定する位置決めデータ) (3.2 / original p.90)

When using 3-axis linear interpolation control (INC linear 3), set the following positioning data.
◎: Always set, ○: Set as required, —: Setting not required

| Setting item (No.) | Setting item (name) | Setting required/not required for the reference axis | Setting required/not required for the interpolation axis |
|---|---|---|---|
| [Da.1] | Operation pattern | ◎ | — |
| [Da.2] | Control method | ◎<br>(Set INC linear 3.) | — |
| [Da.3] | Acceleration time No. | ◎ | — |
| [Da.4] | Deceleration time No. | ◎ | — |
| [Da.6] | Positioning address/movement amount | ◎ | ◎ |
| [Da.7] | Arc address | — | — |
| [Da.8] | Command speed | ◎ | — |
| [Da.9] | Dwell time/JUMP destination positioning data No. | ○ | — |
| [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | ○ | — |
| [Da.20] | Axis to be interpolated No.1 | ◎ | — |
| [Da.21] | Axis to be interpolated No.2 | ◎ | — |
| [Da.22] | Axis to be interpolated No.3 | — | — |

Refer to the following for information on the setting details.
→Page 497 Positioning Data

> **Restriction**
> - When the "reference axis speed" is set during 3-axis linear interpolation control, set so the major axis side becomes the reference axis. If the minor axis side is set as the reference axis, the major axis side speed may exceed the "[Pr.8] Speed limit value".
> - Refer to →Page 74 Interpolation control for the reference axis and interpolation axis combinations.

### 4-axis linear interpolation control (4軸直線補間制御) (3.2 / original p.91-92)

In "4-axis linear interpolation control" ("[Da.2] Control method" = ABS linear 4, INC linear 4), four motors are used to carry out position control in a linear path while carrying out interpolation for the axis directions set in each axis. (Refer to →Page 74 Interpolation control for details on interpolation control.)

#### 4-axis linear interpolation control (ABS linear 4) (4軸直線補間制御(ABS直線4)) (3.2 / original p.91)

In the absolute system 4-axis linear interpolation control, the designated 4 axes are used. Linear interpolation positioning is carried out from the current stop position (start point address) to the address (end point address) set in the "[Da.6] Positioning address/movement amount".

##### Setting positioning data (設定する位置決めデータ) (3.2 / original p.91)

When using 4-axis linear interpolation control (ABS linear 4), set the following positioning data.
◎: Always set, ○: Set as required, —: Setting not required

| Setting item (No.) | Setting item (name) | Setting required/not required for the reference axis | Setting required/not required for the interpolation axis |
|---|---|---|---|
| [Da.1] | Operation pattern | ◎ | — |
| [Da.2] | Control method | ◎<br>(Set ABS linear 4.) | — |
| [Da.3] | Acceleration time No. | ◎ | — |
| [Da.4] | Deceleration time No. | ◎ | — |
| [Da.6] | Positioning address/movement amount | ◎ | ◎ |
| [Da.7] | Arc address | — | — |
| [Da.8] | Command speed | ◎ | — |
| [Da.9] | Dwell time/JUMP destination positioning data No. | ○ | — |
| [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | ○ | — |
| [Da.20] | Axis to be interpolated No.1 | ◎ | — |
| [Da.21] | Axis to be interpolated No.2 | ◎ | — |
| [Da.22] | Axis to be interpolated No.3 | ◎ | — |

Refer to the following for information on the setting details.
→Page 497 Positioning Data

> **Restriction**
> - When the "reference axis speed" is set during 4-axis linear interpolation control, set so the major axis side becomes the reference axis. If the minor axis side is set as the reference axis, the major axis side speed may exceed the "[Pr.8] Speed limit value".
> - Refer to →Page 74 Interpolation control for the reference axis and interpolation axis combinations.

#### 4-axis linear interpolation control (INC linear 4) (4軸直線補間制御(INC直線4)) (3.2 / original p.92)

In the incremental system 4-axis linear interpolation control, the designated 4 axes are used. Linear interpolation positioning is carried out from the current stop position (start point address) to a position at the end of the movement amount set in the "[Da.6] Positioning address/movement amount". The movement direction is determined by the sign of the movement amount.

##### Restrictions (制約事項) (3.2 / original p.92)

An error will occur and the positioning will not start in the following cases. The machine will immediately stop if the error is detected during a positioning operation.
- When the movement amount for each axis exceeds "1073741824 (= 2^30)", the error "Outside linear movement amount range" (error code: 1A15H [FX5-SSC-S], or error code 1B15H [FX5-SSC-G]) will occur at the positioning start. (The maximum movement amount that can be set in "[Da.6] Positioning address/movement amount" is "1073741824 (= 2^30)".)

##### Setting positioning data (設定する位置決めデータ) (3.2 / original p.92)

When using 4-axis linear interpolation control (INC linear 4), set the following positioning data.
◎: Always set, ○: Set as required, —: Setting not required

| Setting item (No.) | Setting item (name) | Setting required/not required for the reference axis | Setting required/not required for the interpolation axis |
|---|---|---|---|
| [Da.1] | Operation pattern | ◎ | — |
| [Da.2] | Control method | ◎<br>(Set INC linear 4.) | — |
| [Da.3] | Acceleration time No. | ◎ | — |
| [Da.4] | Deceleration time No. | ◎ | — |
| [Da.6] | Positioning address/movement amount | ◎ | ◎ |
| [Da.7] | Arc address | — | — |
| [Da.8] | Command speed | ◎ | — |
| [Da.9] | Dwell time/JUMP destination positioning data No. | ○ | — |
| [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | ○ | — |
| [Da.20] | Axis to be interpolated No.1 | ◎ | — |
| [Da.21] | Axis to be interpolated No.2 | ◎ | — |
| [Da.22] | Axis to be interpolated No.3 | ◎ | — |

Refer to the following for information on the setting details.
→Page 497 Positioning Data

> **Restriction**
> - When the "reference axis speed" is set during 4-axis linear interpolation control, set so the major axis side becomes the reference axis. If the minor axis side is set as the reference axis, the major axis side speed may exceed the "[Pr.8] Speed limit value".
> - Refer to →Page 74 Interpolation control for the reference axis and interpolation axis combinations.

### Fixed-feed control (定寸送り制御) (3.2 / original p.93-95)

In "fixed-feed control" ("[Da.2] Control method" = fixed-feed 1, fixed-feed 2, fixed-feed 3, fixed-feed 4), the motor of the specified axis is used to carry out fixed-feed control in a set axis direction.
In fixed-feed control, any remainder of below control accuracy is rounded down to convert the movement amount designated in the positioning data into the command value to servo amplifier.

#### Operation chart (動作図) (3.2 / original p.93-94)

In fixed-feed control, the address ([Md.20] Command position value) of the current stop position (start point address) is set to "0". Positioning is then carried out to a position at the end of the movement amount set in "[Da.6] Positioning address/movement amount". The movement direction is determined by the movement amount sign.
- Positive movement amount: Positioning control to forward direction (Address increase direction)
- Negative movement amount: Positioning control to reverse direction (Address decrease direction)

Ex.
1-axis fixed-feed control

[Figure] 1-axis fixed-feed control (original p.93)
- Repeated positioning on a line: at each "Positioning start" the position is "0", and the axis moves by the "Designated movement amount" (5 consecutive segments, each starting from 0).
- Label: ""[Md.20] Command position value" is set to "0" at the positioning start".
- Direction figure: "Reverse direction" (left) / "Forward direction" (right) with "Stop position" in the middle; "Movement direction for a negative movement amount" = left, "Movement direction for a positive movement amount" = right.

Ex.
2-axis fixed-feed control

[Figure] 2-axis fixed-feed control (original p.93)
- X axis / Y axis plane. Consecutive straight-line movements up to the right; at each start point the coordinates are (0,0).
- Label: ""[Md.20] Command position value" of each axis is set to "0" at the positioning start".
- "Designated movement amount" shown for the X axis and the Y axis of one segment.

##### Restrictions (制約事項) (3.2 / original p.94)

- The error "Continuous path control not possible" (error code: 1A1EH [FX5-SSC-S], or error codes 1B1EH to 1B20H [FX5-SSC-G]) will occur and the operation cannot start if "continuous path control" is set in "[Da.1] Operation pattern". ("Continuous path control" cannot be set in fixed-feed control.)
- "Fixed-feed" cannot be set in "[Da.2] Control method" in the positioning data when "continuous path control" has been set in "[Da.1] Operation pattern" of the immediately prior positioning data. (For example, if the operation pattern of positioning data No.1 is "continuous path control", fixed-feed control cannot be set in positioning data No.2.) The error "Continuous path control not possible" (error code: 1A1EH [FX5-SSC-S], or error codes 1B1EH to 1B20H [FX5-SSC-G]) will occur and the machine will carry out a deceleration stop if this type of setting is carried out.
- In 2- or 3-axis fixed-feed control, if the movement amount of each axis exceeds "1073741824 (=2^30)" when "0: Composite speed" is set in "[Pr.20] Interpolation speed designation method", the error "Outside linear movement amount range" (error code: 1A15H [FX5-SSC-S], or error code 1B15H [FX5-SSC-G]) occurs at a positioning start and the positioning cannot be started. (The maximum movement amount that can be set in "[Da.6] Positioning address/movement amount" is "1073741824 (= 2^30)".
- In 4-axis fixed-feed control, set "1: Reference axis speed" in "[Pr.20] Interpolation speed designation method". If "0: Composite speed" is set, the error "Interpolation mode error" (error code: 199AH [FX5-SSC-S], or error code 1A9AH [FX5-SSC-G]) occurs and the positioning cannot be started.

#### Setting positioning data (設定する位置決めデータ) (3.2 / original p.94-95)

When using fixed-feed control (fixed-feed 1), set the following positioning data.
◎: Always set, ○: Set as required, —: Setting not required

| Setting item (No.) | Setting item (name) | Setting required/not required for the reference axis | Setting required/not required for the interpolation axis |
|---|---|---|---|
| [Da.1] | Operation pattern | ◎ | — |
| [Da.2] | Control method | ◎ | — |
| [Da.3] | Acceleration time No. | ◎ | — |
| [Da.4] | Deceleration time No. | ◎ | — |
| [Da.6] | Positioning address/movement amount | ◎ | ◎ |
| [Da.7] | Arc address | — | — |
| [Da.8] | Command speed | ◎ | — |
| [Da.9] | Dwell time/JUMP destination positioning data No. | ○ | — |
| [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | ○ | — |
| [Da.20] | Axis to be interpolated No.1 | —*1 | — |
| [Da.21] | Axis to be interpolated No.2 | —*1 | — |
| [Da.22] | Axis to be interpolated No.3 | —*1 | — |

*1 To use the 2- to 4-axis fixed-feed control (interpolation), it is required to set the axis used as the interpolation axis.
Refer to the following for information on the setting details.
→Page 497 Positioning Data

> **Point**
> When the movement amount is converted to the actual number of command pulses, a fraction appears after the decimal point, according to the movement amount per pulse. This fraction is normally retained in the Simple Motion module/Motion module and reflected at the next positioning. For the fixed-feed control, since the movement distance is maintained constant (= the command number of pulses is maintained constant), the control is carried out after the fraction pulse is cleared to zero at start.
> [Accumulation/cutoff for fractional pulses]
> When movement amount per pulse is 1.0 [μm] and movement for 2.5 [μm] is executed two times.
> → Conversion to command pulses: 2.5 [μm]/1.0 = 2.5 [pulse]
>
> [Figure] Accumulation/cutoff for fractional pulses (original p.95)
> - Movement amount: 2.5 μm, then 2.5 μm.
> - INC Linear 1: 1st positioning = 2 pulses; 2nd positioning = 3 pulses ( = 2.5 + 0.5 ). Label: "0.5 pulses hold by the Simple Motion module/Motion module is carried to next positioning."
> - Fixed-feed 1: 1st positioning = 2 pulses; 2nd positioning = 2 pulses. Label: "0.5 pulses hold by the Simple Motion module/Motion module is cleared to 0 at start and not carried to next positioning."
>
> When the "reference axis speed" is set in 2- to 4-axis fixed-feed control, set so the major axis side becomes the reference axis. If the minor axis side is set as the reference axis, the major axis side speed may exceed the "[Pr.8] Speed limit value".
> Refer to the following for the combination of the reference axis and the interpolation axis.
> →Page 74 Interpolation control

### 2-axis circular interpolation control with sub point designation (補助点指定の2軸円弧補間制御) (3.2 / original p.96-99)

In "2-axis circular interpolation control" ("[Da.2] Control method" = ABS circular sub, INC circular sub), two motors are used to carry out position control in an arc path passing through designated sub points, while carrying out interpolation for the axis directions set in each axis. (Refer to →Page 74 Interpolation control for details on interpolation control.)

#### 2-axis circular interpolation control with sub point designation (ABS circular sub) (補助点指定の2軸円弧補間制御(ABS円弧補)) (3.2 / original p.96-97)

##### Operation chart (動作図) (3.2 / original p.96)

In the absolute system, 2-axis circular interpolation control with sub point designation, positioning is carried out from the current stop position (start point address) to the address (end point address) set in "[Da.6] Positioning address/movement amount", in an arc path that passes through the sub point address set in "[Da.7] Arc address".
The resulting control path is an arc having as its center the intersection point of perpendicular bisectors of a straight line between the start point address (current stop position) and sub point address (arc address), and a straight line between the sub point address (arc address) and end point address (positioning address).

[Figure] 2-axis circular interpolation control with sub point designation (ABS circular sub) (original p.96)
- Two axes crossing at the "Home position"; each axis has "Forward direction" / "Reverse direction".
- The arc "Movement by circular interpolation" runs from "Start point address (current stop position)" through "Sub point address (arc address)" to "End point address (positioning address)".
- Dashed straight lines connect start point–sub point and sub point–end point; their perpendicular bisectors intersect at the "Arc center point".

##### Restrictions (制約事項) (3.2 / original p.96)

2-axis circular interpolation control cannot be set in the following cases.
- When "degree" is set in "[Pr.1] Unit setting"
- When the units set in "[Pr.1] Unit setting" are different for the reference axis and interpolation axis. ("mm" and "inch" combinations are possible.)
- When "reference axis speed" is set in "[Pr.20] Interpolation speed designation method"

An error will occur and the positioning start will not be possible in the following cases. The machine will immediately stop if the error is detected during positioning control.

| Error factor | Error | Error code FX5-SSC-S | Error code FX5-SSC-G |
|---|---|---|---|
| When the radius exceeds "536870912 (= 2^29)" (The maximum radius for which 2-axis circular interpolation control is possible is "536870912 (= 2^29)".) | "Outside radius range" at positioning start | 1A32H | 1B32H |
| The center point address is outside the range of "-2147483648 (-2^31) to 2147483647 (2^31 - 1)". | "Sub point setting error" at positioning start | 1A27H | 1B37H |
| Start point address = End point address | "End point setting error" | 1A2BH | 1B2BH |
| Start point address = Sub point address | "Sub point setting error" | 1A27H | 1B27H |
| End point address = Sub point address | "Sub point setting error" | 1A27H | 1B28H*1 |
| Start point address, sub point address, and end point address are in a straight line. | "Sub point setting error" | 1A27H | 1B29H*1 |

*In the original, "Error code" is one header spanning the 2 columns FX5-SSC-S / FX5-SSC-G. Expanded to columns.

*1 1B27H for the software version 1.000.

##### Setting positioning data (設定する位置決めデータ) (3.2 / original p.97)

When using 2-axis circular interpolation control with sub point designation (ABS circular sub), set the following positioning data.
◎: Always set, ○: Set as required, —: Setting not required

| Setting item | | Setting required/not required for the reference axis | Setting required/not required for the interpolation axis |
|---|---|---|---|
| [Da.1] | Operation pattern | ◎ | — |
| [Da.2] | Control method | ◎<br>(Set ABS circular sub.) | — |
| [Da.3] | Acceleration time No. | ◎ | — |
| [Da.4] | Deceleration time No. | ◎ | — |
| [Da.6] | Positioning address/movement amount | ◎ | ◎ |
| [Da.7] | Arc address | ◎ | ◎ |
| [Da.8] | Command speed | ◎ | — |
| [Da.9] | Dwell time/JUMP destination positioning data No. | ○ | — |
| [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | ○ | — |
| [Da.20] | Axis to be interpolated No.1 | ◎ | — |
| [Da.21] | Axis to be interpolated No.2 | — | — |
| [Da.22] | Axis to be interpolated No.3 | — | — |

Refer to the following for information on the setting details.
→Page 497 Positioning Data

> **Restriction**
> Set a value in "[Da.8] Command speed" so that the speed of each axis does not exceed the "[Pr.8] Speed limit value". (The speed limit does not function for the speed calculated by the Simple Motion module/Motion module during interpolation control.)

#### 2-axis circular interpolation control with sub point designation (INC circular sub) (補助点指定の2軸円弧補間制御(INC円弧補)) (3.2 / original p.98-99)

##### Operation chart (動作図) (3.2 / original p.98)

In the incremental system, 2-axis circular interpolation control with sub point designation, positioning is carried out from the current stop position (start point address) to a position at the end of the movement amount set in "[Da.6] Positioning address/movement amount" in an arc path that passes through the sub point address set in "[Da.7] Arc address". The movement direction depends on the sign (+ or -) of the movement amount.
The resulting control path is an arc having as its center the intersection point of perpendicular bisectors of the straight line between the start point address (current stop position) and sub point address (arc address) calculated from the movement amount to the sub point, and a straight line between the sub point address (arc address) and end point address (positioning address) calculated from the movement amount to the end point.

[Figure] 2-axis circular interpolation control with sub point designation (INC circular sub) (original p.98)
- Two axes with "Forward direction" / "Reverse direction".
- The arc "Movement by circular interpolation" runs from "Start point address" through "Sub point address (arc address)" to the end point.
- "Movement amount to sub point" is dimensioned from the start point to the sub point on both the horizontal and the vertical axis.
- "Movement amount to the end point" is dimensioned from the start point to the end point on both the horizontal and the vertical axis.
- The intersection of the perpendicular bisectors is the "Arc center".

##### Restrictions (制約事項) (3.2 / original p.98)

2-axis circular interpolation control cannot be set in the following cases.
- When "degree" is set in "[Pr.1] Unit setting"
- When the units set in "[Pr.1] Unit setting" are different for the reference axis and interpolation axis. ("mm" and "inch" combinations are possible.)
- When "reference axis speed" is set in "[Pr.20] Interpolation speed designation method"

An error will occur and the positioning start will not be possible in the following cases. The machine will immediately stop if the error is detected during positioning control.

| Error factor | Error | Error code FX5-SSC-S | Error code FX5-SSC-G |
|---|---|---|---|
| When the radius exceeds "536870912 (= 2^29)" (The maximum radius for which 2-axis circular interpolation control is possible is "536870912 (= 2^29)".) | "Outside radius range" at positioning start | 1A32H | 1B32H |
| The sub point address is outside the range of "-2147483648 (-2^31) to 2147483647 (2^31 - 1)". | "Sub point setting error" | 1A27H | 1B2AH*1 |
| The end point address is outside the range of "-2147483648 (-2^31) to 2147483647 (2^31 - 1)". | "End point setting error" | 1A2BH | 1B2CH*2 |
| The center point address is outside the range of "-2147483648 (-2^31) to 2147483647 (2^31 - 1)". | "Sub point setting error" at positioning start | 1A27H | 1B37H |
| Start point address = End point address | "End point setting error" | 1A2BH | 1B2BH |
| Start point address = Sub point address | "Sub point setting error" | 1A27H | 1B27H |
| End point address = Sub point address | "Sub point setting error" | 1A27H | 1B28H*1 |
| Start point address, sub point address, and end point address are in a straight line. | "Sub point setting error" | 1A27H | 1B29H*1 |

*In the original, "Error code" is one header spanning the 2 columns FX5-SSC-S / FX5-SSC-G. Expanded to columns.

*1 1B27H for the software version 1.000.
*2 1B2BH for the software version 1.000.

##### Setting positioning data (設定する位置決めデータ) (3.2 / original p.99)

When using 2-axis circular interpolation control with sub point designation (INC circular sub), set the following positioning data.
◎: Always set, ○: Set as required, —: Setting not required

| Setting item | | Setting required/not required for the reference axis | Setting required/not required for the interpolation axis |
|---|---|---|---|
| [Da.1] | Operation pattern | ◎ | — |
| [Da.2] | Control method | ◎<br>(Set INC circular sub.) | — |
| [Da.3] | Acceleration time No. | ◎ | — |
| [Da.4] | Deceleration time No. | ◎ | — |
| [Da.6] | Positioning address/movement amount | ◎ | ◎ |
| [Da.7] | Arc address | ◎ | ◎ |
| [Da.8] | Command speed | ◎ | — |
| [Da.9] | Dwell time/JUMP destination positioning data No. | ○ | — |
| [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | ○ | — |
| [Da.20] | Axis to be interpolated No.1 | ◎ | — |
| [Da.21] | Axis to be interpolated No.2 | — | — |
| [Da.22] | Axis to be interpolated No.3 | — | — |

Refer to the following for information on the setting details.
→Page 497 Positioning Data

> **Restriction**
> Set a value in "[Da.8] Command speed" so that the speed of each axis does not exceed the "[Pr.8] Speed limit value". (The speed limit does not function for the speed calculated by the Simple Motion module/Motion module during interpolation control.)

### 2-axis circular interpolation control with center point designation (中心点指定の2軸円弧補間制御) (3.2 / original p.100-104)

In "2-axis circular interpolation control" ("[Da.2] Control method" = ABS circular right, INC circular right, ABS circular left, INC circular left), two motors are used to carry out position control in an arc path having an arc address as a center point, while carrying out interpolation for the axis directions set in each axis. (Refer to →Page 74 Interpolation control for details on interpolation control.)
The following table shows the rotation directions, arc center angles that can be controlled, and positioning paths for the different control methods.

| Control method | Rotation direction | Arc center angle that can be controlled | Positioning path |
|---|---|---|---|
| ABS circular right | Clockwise | 0° < θ ≤ 360° | [Figure] Arc from "Start point (current stop position)" to "End point (positioning address)" passing above the "Center point", moving clockwise; center angle 0° < θ ≤ 360° |
| INC circular right | Clockwise | 0° < θ ≤ 360° | [Figure] Arc from "Start point (current stop position)" to "End point (positioning address)" passing above the "Center point", moving clockwise; center angle 0° < θ ≤ 360° |
| ABS circular left | Counterclockwise | 0° < θ ≤ 360° | [Figure] Arc from "Start point (current stop position)" to "End point (positioning address)" passing below the "Center point", moving counterclockwise; center angle 0° < θ ≤ 360° |
| INC circular left | Counterclockwise | 0° < θ ≤ 360° | [Figure] Arc from "Start point (current stop position)" to "End point (positioning address)" passing below the "Center point", moving counterclockwise; center angle 0° < θ ≤ 360° |

*In the original, "Clockwise" is merged over the 2 rows ABS/INC circular right, "Counterclockwise" over the 2 rows ABS/INC circular left, "0° < θ ≤ 360°" over all 4 rows, and each "Positioning path" figure over 2 rows (circular right / circular left). Expanded to each row.

#### Circular interpolation error compensation (円弧補間の誤差補正) (3.2 / original p.100-101)

In 2-axis circular interpolation control with center point designation, the arc path calculated from the start point address and center point address may deviate from the position of the end point address set in "[Da.6] Positioning address/movement amount". (Refer to →Page 476 [Pr.41] Allowable circular interpolation error width.)

##### Calculated error ≤ "[Pr.41] Allowable circular interpolation error width" (算出した誤差 ≦ "[Pr.41]円弧補間誤差許容範囲") (3.2 / original p.100)

2-axis circular interpolation control to the set end point address is carried out while the error compensation is carried out. (This is called "spiral interpolation".)

[Figure] Spiral interpolation (original p.100)
- A half circle drawn from "Start point address" around "Center point address".
- The deviation between "Calculated end point address" and "End point address" is labeled "Error".
- "Path using spiral interpolation" gradually compensates the radius so that the path reaches the set end point address.

In 2-axis circular interpolation control with center point designation, an angular velocity is calculated on the assumption that operation is carried out at a command speed on the arc using the radius calculated from the start point address and center point address, and the radius is compensated in proportion to the angular velocity deviated from that at the start point.
Thus, when there is a difference (error) between a radius calculated from the start point address and center point address (start point radius) and a radius calculated from the end point address and center point address (end point radius), the composite speed differs from the command speed as follows.

| Condition | Composite speed |
|---|---|
| Start point radius > End point radius | As compared with the speed without error, the speed becomes slower as end point address is reached. |
| Start point radius < End point radius | As compared with the speed without error, the speed becomes faster as end point address is reached. |

*The original table has no header row. The headers "Condition" / "Composite speed" were added in conversion.

##### Calculated error > "[Pr.41] Allowable circular interpolation error width" (算出した誤差 > "[Pr.41]円弧補間誤差許容範囲") (3.2 / original p.101)

At the positioning start, the error "Large arc error deviation" (error code: 1A17H [FX5-SSC-S], or error code 1B17H [FX5-SSC-G]) will occur and the control will not start. The machine will immediately stop if the error is detected during positioning control.

#### 2-axis circular interpolation control with center point designation (ABS circular right, ABS circular left) (中心点指定の2軸円弧補間制御(ABS円弧右，ABS円弧左)) (3.2 / original p.101-102)

##### Operation chart (動作図) (3.2 / original p.101)

In the absolute system, 2-axis circular interpolation control with center point designation positioning is carried out from the current stop position (start point address) to the address (end point address) set in "[Da.6] Positioning address/movement amount", in an arc path having as its center the address (arc address) of the center point set in "[Da.7] Arc address".

[Figure] 2-axis circular interpolation control with center point designation (ABS) (original p.101)
- Two axes with "Forward direction" / "Reverse direction".
- The arc "Movement by circular interpolation" runs clockwise from "Start point address (current stop position)" to "End point address (positioning address)".
- The distance between the "Arc center point (Arc address)" and the start point address is the "Radius".

Positioning of a complete round with a radius from the start point address to the arc center point can be carried out by setting the end point address (positioning address) to the same address as the start point address.

[Figure] Complete round (ABS) (original p.101)
- A full circle around the "Arc center point (Arc address)".
- "Start point address (current stop position)" = "End point address (positioning address)".

In 2-axis circular interpolation control with center point designation, an angular velocity is calculated on the assumption that operation is carried out at a command speed on the arc using the radius calculated from the start point address and center point address, and the radius is compensated in proportion to the angular velocity deviated from that at the start point.
Thus, when there is a difference (error) between a radius calculated from the start point address and center point address (start point radius) and a radius calculated from the end point address and center point address (end point radius), the composite speed differs from the command speed as follows.

| Condition | Composite speed |
|---|---|
| Start point radius > End point radius | As compared with the speed without error, the speed becomes slower as end point address is reached. |
| Start point radius < End point radius | As compared with the speed without error, the speed becomes faster as end point address is reached. |

*The original table has no header row. The headers "Condition" / "Composite speed" were added in conversion.

##### Restrictions (制約事項) (3.2 / original p.102)

2-axis circular interpolation control cannot be set in the following cases.
- When "degree" is set in "[Pr.1] Unit setting"
- When the units set in "[Pr.1] Unit setting" are different for the reference axis and interpolation axis. ("mm" and "inch" combinations are possible.)
- When "reference axis speed" is set in "[Pr.20] Interpolation speed designation method"

An error will occur and the positioning start will not be possible in the following cases. The machine will immediately stop if the error is detected during positioning control.

| Error factor | Error | Error code FX5-SSC-S | Error code FX5-SSC-G |
|---|---|---|---|
| When the radius exceeds "536870912 (= 2^29)" (The maximum radius for which 2-axis circular interpolation control is possible is "536870912 (= 2^29)".) | "Outside radius range" at positioning start | 1A32H | 1B32H |
| Start point address = Center point address | "Center point setting error" | 1A2DH | 1B2DH |
| End point address = Center point address | "Center point setting error" | 1A2DH | 1B2EH*1 |
| The center point address is outside the range of "-2147483648 (-2^31) to 2147483647 (2^31 - 1)". | "Center point setting error" | 1A2DH | 1B2FH*1 |

*In the original, "Error code" is one header spanning the 2 columns FX5-SSC-S / FX5-SSC-G. Expanded to columns.

*1 1B2DH for the software version 1.000.

##### Setting positioning data (設定する位置決めデータ) (3.2 / original p.102)

When using 2-axis circular interpolation control with center point designation (ABS circular right, ABS circular left), set the following positioning data.
◎: Always set, ○: Set as required, —: Setting not required

| Setting item | | Setting required/not required for the reference axis | Setting required/not required for the interpolation axis |
|---|---|---|---|
| [Da.1] | Operation pattern | ◎ | — |
| [Da.2] | Control method | ◎<br>(Set ABS circular right or ABS circular left.) | — |
| [Da.3] | Acceleration time No. | ◎ | — |
| [Da.4] | Deceleration time No. | ◎ | — |
| [Da.6] | Positioning address/movement amount | ◎ | ◎ |
| [Da.7] | Arc address | ◎ | ◎ |
| [Da.8] | Command speed | ◎ | — |
| [Da.9] | Dwell time/JUMP destination positioning data No. | ○ | — |
| [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | ○ | — |
| [Da.20] | Axis to be interpolated No.1 | ◎ | — |
| [Da.21] | Axis to be interpolated No.2 | — | — |
| [Da.22] | Axis to be interpolated No.3 | — | — |

Refer to the following for information on the setting details.
→Page 497 Positioning Data

> **Restriction**
> Set a value in "[Da.8] Command speed" so that the speed of each axis does not exceed the "[Pr.8] Speed limit value". (The speed limit does not function for the speed calculated by the Simple Motion module/Motion module during interpolation control.)

#### 2-axis circular interpolation control with center point designation (INC circular right, INC circular left) (中心点指定の2軸円弧補間制御(INC円弧右，INC円弧左)) (3.2 / original p.103-104)

##### Operation chart (動作図) (3.2 / original p.103)

In the incremental system, 2-axis circular interpolation control with center point designation, positioning is carried out from the current stop position (start point address) to a position at the end of the movement amount set in "[Da.6] Positioning address/movement amount", in an arc path having as its center the address (arc address) of the center point set in "[Da.7] Arc address".

[Figure] 2-axis circular interpolation control with center point designation (INC) (original p.103)
- Two axes with "Forward direction" / "Reverse direction".
- The arc "Movement by circular interpolation" runs clockwise from "Start point address (current stop position)" to the end point.
- The distance between the "Arc center point (Arc address)" and the start point address is the "Radius".
- "Movement amount to the end point" is dimensioned from the start point to the end point on both the horizontal and the vertical axis.

Positioning of a complete round with a radius of the distance from the start point address to the arc center point can be carried out by setting the movement amount to "0".

[Figure] Complete round (INC) (original p.103)
- A full circle around the "Arc center point (Arc address)".
- "Movement amount" = 0.

In 2-axis circular interpolation control with center point designation, an angular velocity is calculated on the assumption that operation is carried out at a command speed on the arc using the radius calculated from the start point address and center point address, and the radius is compensated in proportion to the angular velocity deviated from that at the start point.
Thus, when there is a difference (error) between a radius calculated from the start point address and center point address (start point radius) and a radius calculated from the end point address and center point address (end point radius), the composite speed differs from the command speed as follows.

| Condition | Composite speed |
|---|---|
| Start point radius > End point radius | As compared with the speed without error, the speed becomes slower as end point address is reached. |
| Start point radius < End point radius | As compared with the speed without error, the speed becomes faster as end point address is reached. |

*The original table has no header row. The headers "Condition" / "Composite speed" were added in conversion.

##### Restrictions (制約事項) (3.2 / original p.104)

2-axis circular interpolation control cannot be set in the following cases.
- When "degree" is set in "[Pr.1] Unit setting"
- When the units set in "[Pr.1] Unit setting" are different for the reference axis and interpolation axis. ("mm" and "inch" combinations are possible.)
- When "reference axis speed" is set in "[Pr.20] Interpolation speed designation method"

An error will occur and the positioning start will not be possible in the following cases. The machine will immediately stop if the error is detected during positioning control.

| Error factor | Error | Error code FX5-SSC-S | Error code FX5-SSC-G |
|---|---|---|---|
| When the radius exceeds "536870912 (= 2^29)" (The maximum radius for which 2-axis circular interpolation control is possible is "536870912 (= 2^29)".) | "Outside radius range" at positioning start | 1A32H | 1B32H |
| The end point address is outside the range of "-2147483648 (-2^31) to 2147483647 (2^31 - 1)". | "End point setting error" | 1A2BH | 1B2CH*1 |
| Start point address = Center point address | "Center point setting error" | 1A2DH | 1B2DH |
| End point address = Center point address | "Center point setting error" | 1A2DH | 1B2EH*2 |
| The center point address is outside the range of "-2147483648 (-2^31) to 2147483647 (2^31 - 1)". | "Center point setting error" | 1A2DH | 1B2FH*2 |

*In the original, "Error code" is one header spanning the 2 columns FX5-SSC-S / FX5-SSC-G. Expanded to columns.

*1 1B2BH for the software version 1.000.
*2 1B2DH for the software version 1.000.

##### Setting positioning data (設定する位置決めデータ) (3.2 / original p.104)

When using 2-axis circular interpolation control with center point designation (INC circular right, INC circular left), set the following positioning data.
◎: Always set, ○: Set as required, —: Setting not required

| Setting item | | Setting required/not required for the reference axis | Setting required/not required for the interpolation axis |
|---|---|---|---|
| [Da.1] | Operation pattern | ◎ | — |
| [Da.2] | Control method | ◎<br>(Set INC circular right or INC circular left.) | — |
| [Da.3] | Acceleration time No. | ◎ | — |
| [Da.4] | Deceleration time No. | ◎ | — |
| [Da.6] | Positioning address/movement amount | ◎ | ◎ |
| [Da.7] | Arc address | ◎ | ◎ |
| [Da.8] | Command speed | ◎ | — |
| [Da.9] | Dwell time/JUMP destination positioning data No. | ○ | — |
| [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | ○ | — |
| [Da.20] | Axis to be interpolated No.1 | ◎ | — |
| [Da.21] | Axis to be interpolated No.2 | — | — |
| [Da.22] | Axis to be interpolated No.3 | — | — |

Refer to the following for information on the setting details.
→Page 497 Positioning Data

> **Restriction**
> Set a value in "[Da.8] Command speed" so that the speed of each axis does not exceed the "[Pr.8] Speed limit value". (The speed limit does not function for the speed calculated by the Simple Motion module/Motion module during interpolation control.)

### Speed control (速度制御) (3.2 / original p.105-108)

In "speed control" ("[Da.2] Control method" = Forward run: speed 1 to 4, Reverse run: speed 1 to 4), control is carried out in the axis direction in which the positioning data has been set by continuously outputting pulses for the speed set in "[Da.8] Command speed" until the input of a stop command.
The eight types of speed control includes "Forward run: speed 1 to 4" in which the control starts in the forward run direction, and "Reverse run: speed 1 to 4" in which the control starts in the reverse run direction.
Refer to the following for the combination of the reference axis and the interpolation axis.
→Page 74 Interpolation control

#### Operation chart (動作図) (3.2 / original p.105-106)

The following charts show the operation timing for 1-axis speed control with axis 1 and 2-axis speed control with axis 2 when the axis 1 is set as the reference axis.
The "in speed control" flag ([Md.31] Status: b0) is turned ON during speed control.
The "Positioning complete signal" is not turned ON.

##### 1-axis speed control (1軸速度制御) (3.2 / original p.105)

Ex.

[Figure] 1-axis speed control timing chart (original p.105)
- V-t: the axis accelerates to "[Da.8] Command speed", runs at constant speed, and decelerates to a stop after [Cd.180] Axis stop.
- [Cd.184] Positioning start OFF→ON → [Md.141] BUSY turns ON and the "In speed control flag ([Md.31] Status: b0)" turns ON; acceleration starts.
- [Cd.180] Axis stop turns ON (short pulse) → deceleration starts.
- At the end of the deceleration (stop), [Md.141] BUSY and the In speed control flag turn OFF; [Cd.184] Positioning start then turns OFF (arrow from BUSY OFF to Positioning start OFF).
- Positioning complete signal ([Md.31] Status: b15) stays OFF: "Does not turn ON even when control is stopped by stop command."

##### 2-axis speed control (2軸速度制御) (3.2 / original p.106)

Ex.

[Figure] 2-axis speed control timing chart (original p.106)
- Two V-t charts: "Interpolation axis (axis 2)" and "Reference axis (axis 1)", each accelerating to its own "[Da.8] Command speed", running at constant speed and decelerating to a stop; both start and stop at the same timing.
- [Cd.184] Positioning start OFF→ON → [Md.141] BUSY ON and In speed control flag ([Md.31] Status: b0) ON.
- [Cd.180] Axis stop ON (short pulse) → both axes decelerate; at the stop, [Md.141] BUSY and the In speed control flag turn OFF, then [Cd.184] Positioning start turns OFF.
- Positioning complete signal ([Md.31] Status: b15) stays OFF: "Does not turn ON even when control is stopped by stop command."

#### Command position value (送り現在値) (3.2 / original p.107)

The following table shows the "[Md.20] Command position value" during speed control corresponding to the "[Pr.21] Command position value during speed control" settings. (However, the parameters use the set value of the reference axis.)

| "[Pr.21] Command position value during speed control" setting | [Md.20] Command position value |
|---|---|
| 0: Do not update command position value | The command position value at speed control start is maintained. |
| 1: Update command position value | The command position value is updated. |
| 2: Zero clear command position value | The command position value is fixed at 0. |

[Figure] Command position value during speed control (original p.107)
- (a) Command position value not updated: V-t "In speed control"; the command position value shows "Command position value during speed control start is maintained".
- (b) Command position value updated: "Command position value is updated".
- (c) Command position value zero cleared: the command position value is "0".

#### Restrictions (制約事項) (3.2 / original p.107)

- Set "Positioning complete" in "[Da.1] Operation pattern". The error "Continuous path control not possible" (error code: 1A1EH [FX5-SSC-S], or error codes 1B1EH to 1B20H [FX5-SSC-G]) will occur and the operation cannot start if "continuous positioning control" or "continuous path control" is set in "[Da.1] Operation pattern". ("Continuous positioning control" and "continuous path control" cannot be set in speed control.)
- Set the WITH mode in the output timing when using an M code. The M code will not be output, and the M code ON signal will not turn ON if the AFTER mode is set.
- The error "No command speed" (error code: 1A12H [FX5-SSC-S], or error codes 1B12H to 1B14H [FX5-SSC-G]) will occur if the current speed (-1) is set in "[Da.8] Command speed".
- Set "1: Reference axis speed" in "[Pr.20] Interpolation speed designation method". If "0: Composite speed" is set, the error "Interpolation mode error" (error code: 199AH [FX5-SSC-S], or error code 1A9AH [FX5-SSC-G]) occurs and the positioning cannot be started.
- The software stroke limit check is not carried out if the control unit is set to "degree".

##### Restriction for the speed limit value (速度制限値の制約) (3.2 / original p.107)

When any of control axes (1 to 4 axes) exceeds the speed limit, that axis is controlled with the speed limit value. The speeds of the other axes are limited at the ratios of "[Da.8] Command speed".

Ex.
When the axis 1 and the axis 2 are used

| Setting item | | Axis 1 setting | Axis 2 setting |
|---|---|---|---|
| [Pr.8] | Speed limit value | 4000.00 mm/min | 5000.00 mm/min |
| [Da.8] | Command speed | 8000.00 mm/min | 6000.00 mm/min |

With the settings shown above, the operation speed in speed control is as follows.
- Axis 1: 4000.00 mm/min (Speed is limited by [Pr.8].)
- Axis 2: 3000.00 mm/min (Speed is limited at a ratio of an axis 1 command speed to an axis 2 command speed.)

Operation runs at speed 1 when a reference axis speed is less than 1 as a result of speed limit. In addition, when the bias speed is set, the set value will be the minimum speed.

#### Setting positioning data (設定する位置決めデータ) (3.2 / original p.108)

When using speed control (forward run: speed 1 to 4, reverse run: speed 1 to 4), set the following positioning data.
◎: Always set, ○: Set as required, —: Setting not required

| Setting item | | Setting required/not required for the reference axis | Setting required/not required for the interpolation axis |
|---|---|---|---|
| [Da.1] | Operation pattern | ◎ | — |
| [Da.2] | Control method | ◎ | — |
| [Da.3] | Acceleration time No. | ◎ | — |
| [Da.4] | Deceleration time No. | ◎ | — |
| [Da.6] | Positioning address/movement amount | — | — |
| [Da.7] | Arc address | — | — |
| [Da.8] | Command speed | ◎ | ◎ |
| [Da.9] | Dwell time/JUMP destination positioning data No. | — | — |
| [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | ○ | — |
| [Da.20] | Axis to be interpolated No.1 | —*1 | — |
| [Da.21] | Axis to be interpolated No.2 | —*1 | — |
| [Da.22] | Axis to be interpolated No.3 | —*1 | — |

*1 When using 2- to 4-axis speed control, it is necessary to set the axis to be used as the interpolation axis.

Refer to the following for information on the setting details.
→Page 497 Positioning Data

### Speed-position switching control (INC mode) (速度・位置切換え制御(INCモード)) (3.2 / original p.109-115)

In "speed-position switching control (INC mode)" ("[Da.2] Control method" = Forward run: speed/position, Reverse run: speed/position), the pulses of the speed set in "[Da.8] Command speed" are kept output on the axial direction set to the positioning data. When the "speed-position switching signal" is input, position control of the movement amount set in "[Da.6] Positioning address/movement amount" is exercised.
"Speed-position switching control (INC mode)" is available in two different types: "forward run: speed/position" which starts the axis in the forward run direction and "reverse run: speed/position" which starts the axis in the reverse run direction.
Use the detailed parameter 1 "[Pr.81] Speed-position function selection" with regard to the choice for "speed-position switching control (INC mode)".
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Pr.81] | Speed-position function selection | 0 | Speed-position switching control (INC mode) | 34+150n |

If the set value is other than 0 and 2, it is regarded as 0 and operation is performed in the INC mode.
For details of the setting, refer to the following.
→Page 444 Basic Setting

#### Switching over from speed control to position control (速度制御→位置制御への切換え) (3.2 / original p.109)

- The control is selected the switching method from speed control to position control by the setting value of "[Cd.45] Speed-position switching device selection".

n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.45] | Speed-position switching device selection | → | The device used for speed-position switching is selected.<br>0: Use the external command signal for switching from speed control to position control<br>1: Use the proximity dog signal for switching from speed control to position control<br>2: Use the "[Cd.46] Speed-position switching command" for switching from speed control to position control | 4366+100n |

*In the original, the Setting value cell of [Cd.45] shows "→" (see Setting details).

The switching is performed by using the following device when "2" is set.
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.46] | Speed-position switching command | 1 | Speed control will be taken over by position control | 4367+100n |

- "[Cd.24] Speed-position switching enable flag" must be turned ON to switch over from speed control to position control. (If the "[Cd.24] Speed-position switching enable flag" turns ON after the speed-position switching signal turns ON, the control will continue as speed control without switching over to position control. The control will be switched over from position control to speed control when the speed-position switching signal turns from OFF to ON again. Only position control will be carried out when the "[Cd.24] Speed-position switching enable flag" and speed-position switching signal are ON at the operation start.)

n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.24] | Speed-position switching enable flag | 1 | Speed control will be taken over by position control when switching signal set in "[Cd.45] Speed-position switching device selection" turns ON. | 4328+100n |

#### Operation chart (動作図) (3.2 / original p.110)

The following chart shows the operation timing for speed-position switching control (INC mode).
The "in speed control flag" ([Md.31] Status: b0) is turned ON during speed control of speed-position switching control (INC mode).

##### Operation example (動作例) (3.2 / original p.110)

- When using the external command signal (DI) as speed-position switching signal

[Figure] Speed-position switching control (INC mode) operation example (original p.110)
- V-t: acceleration to "[Da.8] Command speed" → constant speed ("Speed control") → at the speed-position switching signal ON, "Position control" starts; the hatched area after the switching is the "Movement amount set in "[Da.6] Positioning address/movement amount""; deceleration to stop, then "Dwell time".
- [Cd.24] Speed-position switching enable flag turns ON before [Cd.184] Positioning start turns ON, and turns OFF at the end (when BUSY turns OFF).
- [Cd.45] Speed-position switching device selection = 0; "Setting details are taken in at positioning start."
- [Cd.184] Positioning start ON → [Md.141] BUSY ON and In speed control flag ([Md.31] Status: b0) ON.
- Speed-position switching signal (External command signal (DI)) ON (short pulse) → In speed control flag turns OFF; position control starts.
- After the dwell time, [Md.141] BUSY turns OFF and the Positioning complete signal ([Md.31] Status: b15) turns ON (short); [Cd.184] Positioning start turns OFF.

The following operation assumes that the speed-position switching signal is input at the position of the command position value of 90.00000 [degree] during execution of "[Da.2] Control method" "Forward run: speed/position" at "[Pr.1] Unit setting" of "2: degree" and "[Pr.21] Command position value during speed control" setting of "1: Update command position value".
(The value set in "[Da.6] Positioning address/movement amount" is 270.00000 [degree])

[Figure] Degree example (INC mode) (original p.110)
- Left circle: rotation from 0.00000° to 90.00000°, where the "Speed-position switching signal ON" occurs.
- Right circle: from 90.00000° a further 270.00000° is moved: "90.00000 + 270.00000 = 360.00000 = Stop at 0.00000 [degree]".

#### Operation timing and processing time (動作タイミングと処理時間) (3.2 / original p.111-112)

##### Operation example (動作例) (3.2 / original p.111)

[Figure] Operation timing of speed-position switching control (INC mode) (original p.111)
- [Cd.184] Positioning start ON → after t1, [Md.141] BUSY ON; at the same time the M code ON signal ([Md.31] Status: b12) (WITH mode) and the Start complete signal ([Md.31] Status: b14) turn ON, and [Md.26] Axis operation status changes "Standby" → "Speed control".
- M code ON signal (WITH mode) turns OFF t2 after [Cd.7] M code OFF request turns ON.
- Positioning operation starts t4 after BUSY ON ("Speed control").
- Speed-position switching command ON → after t6, the control changes to "Position control" ([Md.26] "Speed control" → "Position control"); [Cd.23] Speed-position switching control movement amount change register value is taken at this point. Notes in the chart: "Speed control is carried out until speed-position switching signal turns ON." / "Position control movement amount is from the input position of the external speed-position switching signal."
- t5 after the positioning operation ends, [Md.141] BUSY turns OFF, [Md.26] returns to "Standby", the Positioning complete signal ([Md.31] Status: b15) turns ON, and the M code ON signal (AFTER mode) ([Md.31] Status: b12) turns ON.
- The Positioning complete signal turns OFF t7 after it turns ON.
- M code ON signal (AFTER mode) turns OFF t2 after [Cd.7] M code OFF request turns ON.
- Start complete signal (b14) turns OFF t3 after [Cd.184] Positioning start turns OFF.
- Positioning complete signal and Home position return complete flag ([Md.31] Status: b4) (shown dashed = if already ON) turn OFF at BUSY ON.

- Normal timing time (Unit: [ms]) (original p.112)

| Model | Operation cycle | t1*1 | t2 | t3 | t4*2 | t5 | t6*3 | t7 |
|---|---|---|---|---|---|---|---|---|
| FX5-SSC-S | 0.888 | 0.3 to 1.4 | 0 to 0.9 | 0 to 0.9 | 3.96 to 4.45 | 0 to 0.9 | 0 to 0.9 | Follows parameters |
| FX5-SSC-S | 1.777 | 0.3 to 1.4 | 0 to 1.8 | 0 to 1.8 | 4.85 to 6.49 | 0 to 1.8 | 0 to 0.9 | Follows parameters |
| FX5-SSC-G | 0.500 | 0.4 to 1.0 | 0 to 0.5 | 0 to 0.5 | 1.9 to 2.3 | 0 to 0.5 | 5.9 to 6.1*4 | Follows parameters |
| FX5-SSC-G | 1.000 | 0.4 to 1.5 | 0 to 1.0 | 0 to 1.0 | 3.2 to 3.7 | 0 to 1.0 | 7.5 to 7.7*4 | Follows parameters |
| FX5-SSC-G | 2.000 | 0.4 to 2.8 | 0 to 2.0 | 0 to 2.0 | 6.0 to 6.4 | 0 to 2.0 | 10.5 to 10.7*4 | Follows parameters |
| FX5-SSC-G | 4.000 | 0.4 to 4.5 | 0 to 4.0 | 0 to 4.0 | 12.0 to 13.5 | 0 to 4.0 | 16.5 to 17.0*4 | Follows parameters |

*In the original, "Operation cycle" is one header spanning the model and cycle columns; the model cell is merged (FX5-SSC-S over 2 rows, FX5-SSC-G over 4 rows). Expanded to each row.

*1 The t1 timing time could be delayed by the operation state of other axes.
*2 The t4 timing time depends on the setting of the acceleration time, servo parameter, etc.
*3 When using the proximity dog signal or "[Cd.46] Speed-position switching command", the t6 timing time could be delayed or vary influenced by the PLC scan time or communication with servo amplifier.
*4 When the servo parameter of the servo amplifier "Input filter setting (PD11)" is set to "0: No filter", the time fluctuates depending on the setting value of the servo parameter "Input filter setting (PD11)".

#### Command position value (送り現在値) (3.2 / original p.112)

The following table shows the "[Md.20] Command position value" during speed-position switching control (INC mode) corresponding to the "[Pr.21] Command position value during speed control" settings.

| "[Pr.21] Command position value during speed control" setting | [Md.20] Command position value |
|---|---|
| 0: Do not update command position value | The command position value at control start is maintained during speed control, and updated from the switching to position control. |
| 1: Update command position value | The command position value is updated during speed control and position control. |
| 2: Zero clear command position value | The command position value is cleared (set to "0") at control start, and updated from the switching to position control. |

[Figure] Command position value during speed-position switching control (INC mode) (original p.112)
- (a) Command position value not updated: Speed control → "Maintained"; Position control → "Updated".
- (b) Command position value updated: "Updated" throughout speed control and position control.
- (c) Command position value zero cleared: Speed control → "0"; Position control → "Updated from 0".

#### Switching time from speed control to position control (速度制御→位置制御への切換え時間) (3.2 / original p.112)

It takes 1 ms from the time the speed-position switching signal is turned ON to the time the speed-position switching latch flag ([Md.31] Status: b1) turns ON.

[Figure] Switching time (original p.112)
- Speed-position switching signal OFF→ON (short pulse) → 1 ms later the Speed-position switching latch flag turns OFF→ON.

#### Speed-position switching signal setting (速度・位置切換え信号の設定) (3.2 / original p.113)

##### External command signals (DI) (外部指令信号(DI)の場合) (3.2 / original p.113)

The following table shows the items that must be set to use the external command signals (DI) as speed-position switching signals.
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Pr.42] | External command function selection | 2 | Speed-position, position-speed switching request | 62+150n |
| [Cd.8] | External command valid | 1 | Validates an external command | 4305+100n |
| [Cd.45] | Speed-position switching device selection | 0 | Use the external command signal for switching from speed control to position control | 4366+100n |

Set the external command signal (DI) in "[Pr.95] External command signal selection". Refer to the following for information on the setting details.
→Page 444 Basic Setting, →Page 561 Control Data

##### Proximity dog signal (DOG) (近点ドグ信号(DOG)の場合) (3.2 / original p.113)

The following table shows the items that must be set to use the proximity dog signal (DOG) as speed-position switching signals.
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.45] | Speed-position switching device selection | 1 | Use the proximity dog signal for switching from speed control to position control | 4366+100n |

This setting is not required for "[Pr.42] External command function selection" and "[Cd.8] External command valid". Refer to the following for information on the setting details.
→Page 561 Control Data

[FX5-SSC-G]
If "3: Link device" is selected in "[Pr.118] DOG signal selection", specify the link device to be used by the link device external signal assignment function. The detection accuracy is the operation cycle considering the communication delay.

##### [Cd.46] Speed-position switching command ("[Cd.46]速度⇔位置切換え指令"の場合) (3.2 / original p.113)

The following table shows the items that must be set to use "[Cd.46] Speed-position switching command" as speed-position switching signals.
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.45] | Speed-position switching device selection | 2 | Use the "[Cd.46] Speed-position switching command" for switching from speed control to position control | 4366+100n |

This setting is not required for "[Pr.42] External command function selection" and "[Cd.8] External command valid". Refer to the following for information on the setting details.
→Page 561 Control Data

#### Changing the position control movement amount (位置制御の移動量の変更) (3.2 / original p.114)

In "speed-position switching control (INC mode)", the position control movement amount can be changed during the speed control section.
- The position control movement amount can be changed during the speed control section of speed-position switching control (INC mode). A movement amount change request will be ignored unless issued during the speed control section of the speed-position switching control (INC mode).
- The "new movement amount" is stored in "[Cd.23] Speed-position switching control movement amount change register" by the program during speed control. When the speed-position switching signal is turned ON, the movement amount for position control is stored in "[Cd.23] Speed-position switching control movement amount change register".
- The movement amount is stored in the "[Md.29] Speed-position switching control positioning movement amount" of the axis monitor area from the point where the control changes to position control by the input of a speed-position switching signal from an external device.

[Figure] Changing the position control movement amount (original p.114)
- "Speed-position switching control (INC mode) start" → "Speed control" section ("Movement amount change possible") → speed-position switching signal ON → "Position control" (hatched) → stop. A second operation is shown later as "Position control start".
- [Cd.23] Speed-position switching control movement amount change register: 0 → P2 (written during speed control) → P3 (written after the switching signal ON).
- "P2 becomes the position control movement amount" (the value at the moment the speed-position switching signal turns ON).
- "Setting after the speed-position switching signal ON is ignored." (P3)
- Speed-position switching latch flag ([Md.31] Status: b1): ON → OFF at the start of speed-position switching control, OFF → ON at the speed-position switching signal ON, and OFF at the next "Position control start".

> **Point**
> - The machine recognizes the presence of a movement amount change request when the data is written to "[Cd.23] Speed-position switching control movement amount change register" with the program.
> - The new movement amount is validated after execution of the speed-position switching control (INC mode), before the input of the speed-position switching signal.
> - The movement amount change can be enable/disable with the interlock function in position control using the "speed-position switching latch flag" ([Md.31] Status: b1) of the axis monitor area.

#### Restrictions (制約事項) (3.2 / original p.115)

- The error "Continuous path control not possible" (error code: 1A1EH [FX5-SSC-S], or error codes 1B1EH to 1B20H [FX5-SSC-G]) will occur and the operation cannot start if "continuous positioning control" or "continuous path control" is set in "[Da.1] Operation pattern".
- "Speed-position switching control" cannot be set in "[Da.2] Control method" of the positioning data when "continuous path control" has been set in "[Da.1] Operation pattern" of the immediately prior positioning data. (For example, if the operation pattern of positioning data No.1 is "continuous path control", "speed-position switching control" cannot be set in positioning data No.2.) The error "Continuous path control not possible" (error code: 1A1EH [FX5-SSC-S], or error codes 1B1EH to 1B20H [FX5-SSC-G]) will occur and the machine will carry out a deceleration stop if this type of setting is carried out.
- The error "No command speed" (error code: 1A12H [FX5-SSC-S], or error codes 1B12H to 1B14H [FX5-SSC-G]) will occur if "current speed (-1)" is set in "[Da.8] Command speed".
- The software stroke limit range check during speed control is made only when the following are satisfied:

| Condition | Description |
|---|---|
| "[Pr.21] Command position value during speed control" is "1: Update command position value". | If the movement amount exceeds the software stroke limit range during speed control in case of the setting of other than "1: Update command position value", the error "Software stroke limit +" (error code: 1993H [FX5-SSC-S], or error code 1A93H [FX5-SSC-G]) or "Software stroke limit -" (error code: 1995H [FX5-SSC-S], or error code 1A95H [FX5-SSC-G]) will occur as soon as speed control is changed to position control and the axis will decelerate to a stop. |
| When "[Pr.1] Unit setting" is other than "2: degree" | If the unit is "degree", the software stroke limit range check is not performed. |

*The original table has no header row. The headers "Condition" / "Description" were added in conversion.

- If the value set in "[Da.6] Positioning address/movement amount" is negative, the error "Outside address range" (error code: 1A30H [FX5-SSC-S], or error codes 1B30H and 1B31H [FX5-SSC-G]) will occur.
- Deceleration processing is carried out from the point where the speed-position switching signal is input if the position control movement amount set in "[Da.6] Positioning address/movement amount" is smaller than the deceleration distance from the "[Da.8] Command speed".
- Turn ON the speed-position switching signal in the speed stabilization region (constant speed status). When the switching signal is turned ON while the speed does not reach the command speed, deviation in the stop position may occur because of large deviation in the droop pulse amount. During use of the servo motor, the movement amount is "[Da.6] Positioning address/movement amount" from the assumed motor position based on "[Md.101] Actual position value" at switching of speed control to position control. Therefore, if the signal is turned ON during acceleration/deceleration, the stop position will vary due to large variation of the droop pulse amount. Even though "[Md.29] Speed-position switching control positioning movement amount" is the same, the stop position will change due to a change in droop pulse amount when "[Da.8] Command speed" is different.

#### Setting positioning data (設定する位置決めデータ) (3.2 / original p.115)

When using speed-position switching control (INC mode), set the following positioning data.
◎: Always set, ○: Set as required, —: Setting not required

| Setting item | | Setting required/not required |
|---|---|---|
| [Da.1] | Operation pattern | ◎ |
| [Da.2] | Control method | ◎<br>(Set "Forward run: speed/position" or "Reverse run: speed/position".) |
| [Da.3] | Acceleration time No. | ◎ |
| [Da.4] | Deceleration time No. | ◎ |
| [Da.6] | Positioning address/movement amount | ◎ |
| [Da.7] | Arc address | — |
| [Da.8] | Command speed | ◎ |
| [Da.9] | Dwell time/JUMP destination positioning data No. | ○ |
| [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | ○ |
| [Da.20] | Axis to be interpolated No.1 | — |
| [Da.21] | Axis to be interpolated No.2 | — |
| [Da.22] | Axis to be interpolated No.3 | — |

Refer to the following for information on the setting details.
→Page 497 Positioning Data

### Speed-position switching control (ABS mode) (速度・位置切換え制御(ABSモード)) (3.2 / original p.116-122)

In case of "speed-position switching control (ABS mode)" ("[Da.2] Control method" = Forward run: speed/position, Reverse run: speed/position), the pulses of the speed set in "[Da.8] Command speed" are kept output in the axial direction set to the positioning data. When the "speed-position switching signal" is input, position control to the address set in "[Da.6] Positioning address/movement amount" is exercised.
"Speed-position switching control (ABS mode)" is available in two different types: "forward run: speed/position" which starts the axis in the forward run direction and "reverse run: speed/position" which starts the axis in the reverse run direction.
"Speed-position switching control (ABS mode)" is valid only when "[Pr.1] Unit setting" is "2: degree".
○: Setting allowed, ×: Setting disallowed (If setting is made, the error "Speed-position function selection error" (error code: 1AAEH [FX5-SSC-S], or error code 1BAEH [FX5-SSC-G]) will occur when the "[Cd.190] PLC READY" turns ON.)

| Speed-position function selection | [Pr.1] Unit setting: mm | [Pr.1] Unit setting: inch | [Pr.1] Unit setting: degree | [Pr.1] Unit setting: pulse |
|---|---|---|---|---|
| INC mode | ○ | ○ | ○ | ○ |
| ABS mode | × | × | ○ | × |

*In the original, "[Pr.1] Unit setting" is one header spanning the 4 columns mm / inch / degree / pulse. Expanded to columns.

Use the detailed parameter 1 "[Pr.81] Speed-position function selection" to choose "speed-position switching control (ABS mode)".
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Pr.81] | Speed-position function selection | 2 | Speed-position switching control (ABS mode) | 34+150n |

If the set value is other than 0 and 2, it is regarded as 0 and operation is performed in the INC mode. For details of the setting, refer to the following.
→Page 444 Basic Setting

#### Switching over from speed control to position control (速度制御→位置制御への切換え) (3.2 / original p.116-117)

- The control is selected the switching method from speed control to position control by the setting value of "[Cd.45] Speed-position switching device selection".

n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.45] | Speed-position switching device selection | → | The device used for speed-position switching is selected.<br>0: Use the external command signal for switching from position control to speed control<br>1: Use the proximity dog signal for switching from position control to speed control<br>2: Use the "[Cd.46] Speed-position switching command" for switching from position control to speed control | 4366+100n |

*In the original, the Setting value cell of [Cd.45] shows "→" (see Setting details). The option texts read "from position control to speed control" in the original on this page (as is).

The switching is performed by using the following device when "2" is set.
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.46] | Speed-position switching command | 1 | Speed control will be taken over by position control. | 4367+100n |

- "[Cd.24] Speed-position switching enable flag" must be turned ON to switch over from speed control to position control. (If the "[Cd.24] Speed-position switching enable flag" turns ON after the speed-position switching signal turns ON, the control will continue as speed control without switching over to position control. The control will be switched over from speed control to position control when the speed-position switching signal turns from OFF to ON again. Only position control will be carried out when the "[Cd.24] Speed-position switching enable flag" and speed-position switching signal are ON at the operation start.)

n: Axis No. - 1 (original p.117)

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.24] | Speed-position switching enable flag | 1 | Speed control will be taken over by position control when the switching signal set in "[Cd.45] Speed-position switching device selection" turns ON. | 4328+100n |

#### Operation chart (動作図) (3.2 / original p.117)

The following chart shows the operation timing for speed-position switching control (ABS mode).
The "in speed control flag" ([Md.31] Status: b0) is turned ON during speed control of speed-position switching control (ABS mode).

##### Operation example (動作例) (3.2 / original p.117)

- When using the external command signal (DI) as speed-position switching signal

[Figure] Speed-position switching control (ABS mode) operation example (original p.117)
- V-t: acceleration to "[Da.8] Command speed" → "Speed control" → at the speed-position switching signal ON, "Position control" (hatched) to the "Address set in "[Da.6] Positioning address/movement amount"" → stop → "Dwell time".
- [Cd.24] Speed-position switching enable flag turns ON before [Cd.184] Positioning start turns ON, and OFF at the end (when BUSY turns OFF).
- [Cd.45] Speed-position switching device selection = 0; "Setting details are taken in at positioning start."
- [Cd.184] Positioning start ON → [Md.141] BUSY ON and In speed control flag ([Md.31] Status: b0) ON.
- Speed-position switching signal (External command signal (DI)) ON (short pulse) → In speed control flag OFF; position control starts.
- After the dwell time, [Md.141] BUSY OFF and Positioning complete signal ([Md.31] Status: b15) ON (short); [Cd.184] Positioning start OFF.

The following operation assumes that the speed-position switching signal is input at the position of the command position value of 90.00000 [degree] during execution of "[Da.2] Control method" "Forward run: speed/position" at "[Pr.1] Unit setting" of "2: degree" and "[Pr.21] Command position value during speed control" setting of "1: Update command position value".
(The value set in "[Da.6] Positioning address/movement amount" is 270.00000 [degree])

[Figure] Degree example (ABS mode) (original p.117)
- Left circle: rotation from 0.00000° to 90.00000°, where the "Speed-position switching signal ON" occurs.
- Right circle: from 90.00000° the axis moves on to the address 270.00000°: "Stop at 270.00000 [degree]".

#### Operation timing and processing time (動作タイミングと処理時間) (3.2 / original p.118)

##### Operation example (動作例) (3.2 / original p.118)

[Figure] Operation timing of speed-position switching control (ABS mode) (original p.118)
- [Cd.184] Positioning start ON → after t1, [Md.141] BUSY ON; at the same time the M code ON signal ([Md.31] Status: b12) (WITH mode) and the Start complete signal ([Md.31] Status: b14) turn ON; [Md.26] Axis operation status "Standby" → "Speed control".
- M code ON signal (WITH mode) turns OFF t2 after [Cd.7] M code OFF request turns ON.
- Positioning operation starts t4 after BUSY ON ("Speed control").
- Speed-position switching command ON → after t6, "Position control" ([Md.26] "Speed control" → "Position control"). Note in the chart: "Speed control is carried out until speed-position switching signal turns ON."
- t5 after the positioning operation ends, [Md.141] BUSY OFF, [Md.26] "Standby", Positioning complete signal ([Md.31] Status: b15) ON, M code ON signal ([Md.31] Status: b12) (AFTER mode) ON.
- Positioning complete signal turns OFF t7 after it turns ON; M code ON signal (AFTER mode) turns OFF t2 after [Cd.7] M code OFF request turns ON.
- Start complete signal (b14) turns OFF t3 after [Cd.184] Positioning start turns OFF.
- Positioning complete signal and Home position return complete flag ([Md.31] Status: b4) (shown dashed = if already ON) turn OFF at BUSY ON.

- Normal timing time (Unit: [ms])

| Model | Operation cycle | t1*1 | t2 | t3 | t4*2 | t5 | t6*3 | t7 |
|---|---|---|---|---|---|---|---|---|
| FX5-SSC-S | 0.888 | 0.3 to 1.4 | 0 to 0.9 | 0 to 0.9 | 3.62 to 4.62 | 0 to 0.9 | 0 to 0.9 | Follows parameters |
| FX5-SSC-S | 1.777 | 0.3 to 1.4 | 0 to 1.8 | 0 to 1.8 | 4.54 to 6.38 | 0 to 1.8 | 0 to 0.9 | Follows parameters |
| FX5-SSC-G | 0.500 | 0.4 to 1.0 | 0 to 0.5 | 0 to 0.5 | 1.8 to 2.0 | 0 to 0.5 | 5.9 to 6.1*4 | Follows parameters |
| FX5-SSC-G | 1.000 | 0.4 to 1.5 | 0 to 1.0 | 0 to 1.0 | 3.0 to 3.5 | 0 to 1.0 | 7.5 to 7.7*4 | Follows parameters |
| FX5-SSC-G | 2.000 | 0.4 to 2.8 | 0 to 2.0 | 0 to 2.0 | 6.0 to 6.6 | 0 to 2.0 | 10.5 to 10.7*4 | Follows parameters |
| FX5-SSC-G | 4.000 | 0.4 to 4.5 | 0 to 4.0 | 0 to 4.0 | 12.0 to 12.5 | 0 to 4.0 | 16.5 to 17.0*4 | Follows parameters |

*In the original, "Operation cycle" is one header spanning the model and cycle columns; the model cell is merged (FX5-SSC-S over 2 rows, FX5-SSC-G over 4 rows). Expanded to each row.

*1 The t1 timing time could be delayed by the operation state of other axes.
*2 The t4 timing time depends on the setting of the acceleration time, servo parameter, etc.
*3 When using the proximity dog signal and "[Cd.46] Speed-position switching command", the t6 timing time could be delayed or vary influenced by the PLC scan time or communication with servo amplifier.
*4 When the servo parameter of the servo amplifier "Input filter setting (PD11)" is set to "0: No filter", the time fluctuates depending on the setting value of the servo parameter "Input filter setting (PD11)".

#### Command position value (送り現在値) (3.2 / original p.119)

The following table shows the "[Md.20] Command position value" during speed-position switching control (ABS mode) corresponding to the "[Pr.21] Command position value during speed control" settings.

| "[Pr.21] Command position value during speed control" setting | [Md.20] Command position value |
|---|---|
| 1: Update command position value | The command position value is updated during speed control and position control. |

Only "1: Update command position value" is valid for the setting of "[Pr.21] Command position value during speed control" in speed-position switching control (ABS mode).
The error "Speed-position function selection error" (error code: 1AAEH [FX5-SSC-S], or error code 1BAEH [FX5-SSC-G]) will occur if the "[Pr.21] Command position value during speed control" setting is other than 1.

[Figure] Command position value updated (original p.119)
- V-t: "Speed control" then "Position control" (hatched); the command position value is "Updated" throughout ("Command position value updated").

#### Switching time from speed control to position control (速度制御→位置制御への切換え時間) (3.2 / original p.119)

It takes 1 ms from the time the speed-position switching signal is turned ON to the time the speed-position switching latch flag ([Md.31] Status: b1) turns ON.

[Figure] Switching time (original p.119)
- Speed-position switching signal OFF→ON (short pulse) → 1 ms later the Speed-position switching latch flag turns OFF→ON.

#### Speed-position switching signal setting (速度・位置切換え信号の設定) (3.2 / original p.120)

##### External command signals (DI) (外部指令信号(DI)の場合) (3.2 / original p.120)

The following table shows the items that must be set to use the external command signals (DI) as speed-position switching signals.
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Pr.42] | External command function selection | 2 | Speed-position, position-speed switching request | 62+150n |
| [Cd.8] | External command valid | 1 | Validates an external command | 4305+100n |
| [Cd.45] | Speed-position switching device selection | 0 | Use the external command signal for switching from speed control to position control | 4366+100n |

Set the external command signal (DI) in "[Pr.95] External command signal selection". Refer to the following for information on the setting details.
→Page 444 Basic Setting, →Page 561 Control Data

##### Proximity dog signal (DOG) (近点ドグ信号(DOG)の場合) (3.2 / original p.120)

The following table shows the items that must be set to use the proximity dog signal (DOG) as speed-position switching signals.
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.45] | Speed-position switching device selection | 1 | Use the proximity dog signal for switching from speed control to position control | 4366+100n |

The setting is not required for "[Pr.42] External command function selection" and "[Cd.8] External command valid". Refer to the following for information on the setting details.
→Page 561 Control Data

[FX5-SSC-G]
If "3: Link device" is selected in "[Pr.118] DOG signal selection", specify the link device to be used by the link device external signal assignment function. The detection accuracy is the operation cycle.

##### [Cd.46] Speed-position switching command ("[Cd.46]速度⇔位置切換え指令"の場合) (3.2 / original p.120)

The following table shows the items that must be set to use "[Cd.46] Speed-position switching command" as speed-position switching signals.
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.45] | Speed-position switching device selection | 2 | Use the "[Cd.46] Speed-position switching command" for switching from speed control to position control | 4366+100n |

The setting is not required for "[Pr.42] External command function selection" and "[Cd.8] External command valid". Refer to the following for information on the setting details.
→Page 561 Control Data

#### Restrictions (制約事項) (3.2 / original p.121)

- The error "Continuous path control not possible" (error code: 1A1EH [FX5-SSC-S], or error codes 1B1EH to 1B20H [FX5-SSC-G]) will occur and the operation cannot start if "continuous positioning control" or "continuous path control" is set in "[Da.1] Operation pattern".
- "Speed-position switching control" cannot be set in "[Da.2] Control method" of the positioning data when "continuous path control" has been set in "[Da.1] Operation pattern" of the immediately prior positioning data. (For example, if the operation pattern of positioning data No.1 is "continuous path control", "speed-position switching control" cannot be set in positioning data No.2.) The error "Continuous path control not possible" (error code: 1A1EH [FX5-SSC-S], or error codes 1B1EH to 1B20H [FX5-SSC-G]) will occur and the machine will carry out a deceleration stop if this type of setting is carried out.
- The error "No command speed" (error code: 1A12H [FX5-SSC-S], or error codes 1B12H to 1B14H [FX5-SSC-G]) will occur if "current speed (-1)" is set in "[Da.8] Command speed".
- If the value set in "[Da.6] Positioning address/movement amount" is negative, the error "Outside address range" (error code: 1A30H [FX5-SSC-S], or error codes 1B30H and 1B31H [FX5-SSC-G]) will occur.
- Even though the axis control data "[Cd.23] Speed-position switching control movement amount change register" was set in speed-position switching control (ABS mode), it would not function. The set value is ignored.
- To exercise speed-position switching control (ABS mode), the following conditions must be satisfied:
  1) "[Pr.1] Unit setting" is "2: degree"
  2) The software stroke limit function is invalid (upper limit value = lower limit value)
  3) "[Pr.21] Command position value during speed control" is "1: Update command position value"
  4) The "[Da.6] Positioning address/movement amount" setting range is 0 to 359.99999 (degree). If the value is outside of the range, the error "Outside address range" (error code: 1A30H [FX5-SSC-S], or error codes 1B30H and 1B31H [FX5-SSC-G]) will occur at a start.
  5) The "[Pr.81] Speed-position function selection" setting is "2: Speed-position switching control (ABS mode)".
- If any of the conditions in 1) to 3) is not satisfied in the case of 5), the error "Speed-position function selection error" (error code: 1AAEH [FX5-SSC-S], or error code 1BAEH [FX5-SSC-G]) will occur when the "[Cd.190] PLC READY" turns from OFF to ON.
- If the axis reaches the positioning address midway through deceleration after automatic deceleration started at the input of the speed-position switching signal, the axis will not stop immediately at the positioning address. The axis will stop at the positioning address after N revolutions so that automatic deceleration can always be made. (N: Natural number) In the following example, since making deceleration in the path of dotted line will cause the axis to exceed the positioning addresses twice, the axis will decelerate to a stop at the third positioning address.

[Figure] Stop after N revolutions (original p.121)
- At "Speed-position switching signal" input, the dotted deceleration line would pass the first and second "positioning address" before stopping.
- The actual deceleration (solid line) continues at speed and then decelerates to stop at the third "positioning address"; the positioning addresses are spaced "360° added" apart.

#### Setting positioning data (設定する位置決めデータ) (3.2 / original p.122)

When using speed-position switching control (ABS mode), set the following positioning data.
◎: Always set, ○: Set as required, —: Setting not required

| Setting item | | Setting required/not required |
|---|---|---|
| [Da.1] | Operation pattern | ◎ |
| [Da.2] | Control method | ◎<br>(Set "Forward run: speed/position" or "Reverse run: speed/position".) |
| [Da.3] | Acceleration time No. | ◎ |
| [Da.4] | Deceleration time No. | ◎ |
| [Da.6] | Positioning address/movement amount | ◎ |
| [Da.7] | Arc address | — |
| [Da.8] | Command speed | ◎ |
| [Da.9] | Dwell time/JUMP destination positioning data No. | ○ |
| [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | ○ |
| [Da.20] | Axis to be interpolated No.1 | — |
| [Da.21] | Axis to be interpolated No.2 | — |
| [Da.22] | Axis to be interpolated No.3 | — |

Refer to the following for information on the setting details.
→Page 497 Positioning Data

### Position-speed switching control (位置・速度切換え制御) (3.2 / original p.123-129)

In "position-speed switching control" ("[Da.2] Control method" = Forward run: position/speed, Reverse run: position/speed), before the position-speed switching signal is input, position control is carried out for the movement amount set in "[Da.6] Positioning address/movement amount" in the axis direction in which the positioning data has been set. When the position-speed switching signal is input, the position control is carried out by continuously outputting the pulses for the speed set in "[Da.8] Command speed" until the input of a stop command.
The two types of position-speed switching control are "Forward run: position/speed" in which the control starts in the forward run direction, and "Reverse run: position/speed" in which control starts in the reverse run direction.

#### Switching over from position control to speed control (位置制御→速度制御への切換え) (3.2 / original p.123)

- The control is selected the switching method from position control to speed control by the setting value of "[Cd.45] Speed-position switching device selection".

n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.45] | Speed-position switching device selection | → | The device used for speed-position switching is selected.<br>0: Use the external command signal for switching from position control to speed control<br>1: Use the proximity dog signal for switching from position control to speed control<br>2: Use the "[Cd.46] Speed-position switching command" for switching from position control to speed control | 4366+100n |

*In the original, the Setting value cell of [Cd.45] shows "→" (see Setting details).

The switching is performed by using the following device when "2" is set.
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.46] | Speed-position switching command | 1 | Position control will be taken over by speed control. | 4367+100n |

- "[Cd.26] Position-speed switching enable flag" must be turned ON to switch over from position control to speed control. (If the "[Cd.26] Position-speed switching enable flag" turns ON after the position-speed switching signal turns ON, the control will continue as position control without switching over to speed control. The control will be switched over from position control to speed control when the position-speed switching signal turns from OFF to ON again. Only speed control will be carried out when the "[Cd.26] Position-speed switching enable flag" and position-speed switching signal are ON at the operation start.)

n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.26] | Position-speed switching enable flag | 1 | Speed control will be taken over by position control when the switching signal set in "[Cd.45] Speed-position switching device selection" turns ON. | 4332+100n |

*The Setting details text of [Cd.26] is as printed in the original.

#### Operation chart (動作図) (3.2 / original p.124)

The following chart shows the operation timing for position-speed switching control.
The "in speed control" flag ([Md.31] Status: b0) is turned ON during speed control of position-speed switching control.

##### Operation example (動作例) (3.2 / original p.124)

- When using the external command signal (DI) as position-speed switching signal

[Figure] Position-speed switching control operation example (original p.124)
- V-t: acceleration to "[Da.8] Command speed"; the first section (hatched) is "Position control", after the position-speed switching signal ON the section is "Speed control"; deceleration to stop after [Cd.180] Axis stop.
- [Cd.26] Position-speed switching enable flag turns ON before [Cd.184] Positioning start turns ON, and OFF when BUSY turns OFF.
- [Cd.45] Speed-position switching device selection = 0; "Setting details are taken in at positioning start."
- [Cd.184] Positioning start ON → [Md.141] BUSY ON.
- Position-speed switching signal (External command signal (DI)) ON (short pulse) → In speed control flag ([Md.31] Status: b0) ON.
- [Cd.180] Axis stop ON (short pulse) → deceleration; at the stop [Md.141] BUSY and the In speed control flag turn OFF, then [Cd.184] Positioning start turns OFF.
- Positioning complete signal ([Md.31] Status: b15) stays OFF: "Does not turn ON even when control is stopped by stop command."

#### Operation timing and processing time (動作タイミングと処理時間) (3.2 / original p.125)

[Figure] Operation timing of position-speed switching control (original p.125)
- [Cd.184] Positioning start ON → after t1, [Md.141] BUSY ON; at the same time the M code ON signal ([Md.31] Status: b12) (WITH mode) and Start complete signal ([Md.31] Status: b14) turn ON; [Md.26] Axis operation status "Standby" → "Position control".
- M code ON signal (WITH mode) turns OFF t2 after [Cd.7] M code OFF request turns ON.
- Positioning operation starts t4 after BUSY ON ("Position control").
- Position-speed switching command ON → after t6, "Speed control" ([Md.26] "Position control" → "Speed control"); [Cd.25] Position-speed switching control speed change register value is taken at this point. Notes in the chart: "Position control carried out until position-speed switching signal turns ON." / "Speed control command speed is from the input position of the external position-speed switching signal."
- [Cd.180] Axis stop ON → deceleration stop; [Md.141] BUSY OFF and [Md.26] "Stopped".
- Start complete signal (b14) turns OFF t3 after [Cd.184] Positioning start turns OFF.
- Positioning complete signal ([Md.31] Status: b15) and Home position return complete flag ([Md.31] Status: b4) (shown dashed = if already ON) turn OFF at BUSY ON; the positioning complete signal does not turn ON afterwards.

- Normal timing time (Unit: [ms])

| Model | Operation cycle | t1*1 | t2 | t3 | t4*2 | t5 | t6*3 |
|---|---|---|---|---|---|---|---|
| FX5-SSC-S | 0.888 | 0.3 to 1.4 | 0 to 0.9 | 0 to 0.9 | 3.75 to 4.40 | — | 0 to 0.9 |
| FX5-SSC-S | 1.777 | 0.3 to 1.4 | 0 to 1.8 | 0 to 1.8 | 4.80 to 6.24 | — | 0 to 0.9 |
| FX5-SSC-G | 0.500 | 0.4 to 1.0 | 0 to 0.5 | 0 to 0.5 | 1.80 to 2.0 | — | 5.9 to 6.1*4 |
| FX5-SSC-G | 1.000 | 0.4 to 1.5 | 0 to 1.0 | 0 to 1.0 | 3.2 to 3.5 | — | 7.5 to 7.7*4 |
| FX5-SSC-G | 2.000 | 0.4 to 2.8 | 0 to 2.0 | 0 to 2.0 | 6.4 to 6.9 | — | 10.5 to 10.7*4 |
| FX5-SSC-G | 4.000 | 0.4 to 4.5 | 0 to 4.0 | 0 to 4.0 | 12.0 to 12.5 | — | 16.5 to 17.0*4 |

*In the original, "Operation cycle" is one header spanning the model and cycle columns; the model cell is merged (FX5-SSC-S over 2 rows, FX5-SSC-G over 4 rows). Expanded to each row.

*1 The t1 timing time could be delayed by the operation state of other axes.
*2 The t4 timing time depends on the setting of the acceleration time, servo parameter, etc.
*3 When using the proximity dog signal and "[Cd.46] Speed-position switching command", the t6 timing time could be delayed or vary influenced by the PLC scan time or communication with servo amplifier.
*4 When the servo parameter of the servo amplifier "Input filter setting (PD11)" is set to "0: No filter", the time fluctuates depending on the setting value of the servo parameter "Input filter setting (PD11)".

#### Command position value (送り現在値) (3.2 / original p.126)

The following table shows the "[Md.20] Command position value" during position-speed switching control corresponding to the "[Pr.21] Command position value during speed control" settings.

| "[Pr.21] Command position value during speed control" setting | [Md.20] Command position value |
|---|---|
| 0: Do not update command position value | The command position value is updated during position control, and the command position value at the time of switching is maintained as soon as position control is switched to speed control. |
| 1: Update command position value | The command position value is updated during position control and speed control. |
| 2: Zero clear command position value | The command position value is updated during position control, and the command position value is cleared (to "0") as soon as position control is switched to speed control. |

[Figure] Command position value during position-speed switching control (original p.126)
- (a) Command position value not updated: Position control → "Updated"; Speed control → "Maintained".
- (b) Command position value updated: "Updated" throughout.
- (c) Command position value zero cleared: Position control → "Updated"; Speed control → "0".

#### Switching time from position control to speed control (位置制御→速度制御への切換え時間) (3.2 / original p.126)

It takes 1 ms from the time the position-speed switching signal is turned ON to the time the position-speed switching latch flag ([Md.31] Status: b5) turns ON.

[Figure] Switching time (original p.126)
- Position-speed switching signal OFF→ON (short pulse) → 1 ms later the Position-speed switching latch flag turns OFF→ON.

#### Position-speed switching signal setting (位置・速度切換え信号の設定) (3.2 / original p.127)

##### External command signals (DI) (外部指令信号(DI)の場合) (3.2 / original p.127)

The following table shows the items that must be set to use the external command signals (DI) as position-speed switching signals.
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Pr.42] | External command function selection | 2 | Speed-position, position-speed switching request. | 62+150n |
| [Cd.8] | External command valid | 1 | Validates an external command. | 4305+100n |
| [Cd.45] | Speed-position switching device selection | 0 | Use the external command signal for switching from position control to speed control. | 4366+100n |

Set the external command signal (DI) in "[Pr.95] External command signal selection". Refer to the following for information on the setting details.
→Page 444 Basic Setting, →Page 561 Control Data

##### Proximity dog signal (DOG) (近点ドグ信号(DOG)の場合) (3.2 / original p.127)

The following table shows the items that must be set to use the proximity dog signal (DOG) as position-speed switching signals.
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.45] | Speed-position switching device selection | 1 | Use the proximity dog signal for switching from position control to speed control. | 4366+100n |

The setting is not required for "[Pr.42] External command function selection" and "[Cd.8] External command valid". Refer to the following for information on the setting details.
→Page 561 Control Data

[FX5-SSC-G]
If "3: Link device" is selected in "[Pr.118] DOG signal selection", specify the link device to be used by the link device external signal assignment function. The detection accuracy is the operation cycle.

##### [Cd.46] Speed-position switching command ("[Cd.46]速度⇔位置切換え指令"の場合) (3.2 / original p.127)

The following table shows the items that must be set to use "[Cd.46] Speed-position switching command" as position-speed switching signals.
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.45] | Speed-position switching device selection | 2 | Use the "[Cd.46] Speed-position switching command" for switching from position control to speed control. | 4366+100n |

The setting is not required for "[Pr.42] External command function selection" and "[Cd.8] External command valid". Refer to the following for information on the setting details.
→Page 561 Control Data

#### Changing the speed control command speed (速度制御の指令速度の変更) (3.2 / original p.128)

In "position-speed switching control", the speed control command speed can be changed during the position control.
- The speed control command speed can be changed during the position control of position-speed switching control. A command speed change request will be ignored unless issued during the position control of the position-speed switching control.
- The "new command speed" is stored in "[Cd.25] Position-speed switching control speed change register" by the program during position control. This value then becomes the speed control command speed when the position-speed switching signal turns ON.

[Figure] Changing the speed control command speed (original p.128)
- "Position-speed switching control start" → "Position control" (hatched; "Speed change enable") → position-speed switching signal ON → "Speed control" at the new speed (lower in the figure) → Stop signal ON → stop. A later operation is shown as "Position control start".
- [Cd.25] Position-speed switching control speed change register: 0 → V2 (written during position control) → V3 (written after the switching signal ON).
- "V2 becomes the speed control command speed." (the value at the moment the position-speed switching signal turns ON)
- "Setting after the position-speed switching signal ON is ignored." (V3)
- Position-speed switching latch flag ([Md.31] Status: b5): ON → OFF at the start of position-speed switching control, OFF → ON at the position-speed switching signal ON, OFF at the next "Position control start".
- Stop signal: ON (short pulse) during speed control → deceleration stop.

> **Point**
> - The machine recognizes the presence of a command speed change request when the data is written to "[Cd.25] Position-speed switching control speed change register" with the program.
> - The new command speed is validated after execution of the position-speed switching control before the input of the position-speed switching signal.
> - The command speed change can be enabled/disabled with the interlock function in speed control using the "position-speed switching latch flag" ([Md.31] Status: b5) of the axis monitor area.

#### Restrictions (制約事項) (3.2 / original p.129)

- The error "Continuous path control not possible" (error code: 1A1EH [FX5-SSC-S], or error codes 1B1EH to 1B20H [FX5-SSC-G]) will occur and the operation cannot start if "continuous positioning control" or "continuous path control" is set in "[Da.1] Operation pattern".
- "Position-speed switching control" cannot be set in "[Da.2] Control method" of the positioning data when "continuous path control" has been set in "[Da.1] Operation pattern" of the immediately prior positioning data. (For example, if the operation pattern of positioning data No.1 is "continuous path control", "position-speed switching control" cannot be set in positioning data No.2.) The error "Continuous path control not possible" (error code: 1A1EH [FX5-SSC-S], or error codes 1B1EH to 1B20H [FX5-SSC-G]) will occur and the machine will carry out a deceleration stop if this type of setting is carried out.
- The software stroke limit range is only checked during speed control if the "1: Update command position value" is set in "[Pr.21] Command position value during speed control". The software stroke limit range is not checked when the control unit is set to "degree".
- The error "Software stroke limit +" (error code: 1993H [FX5-SSC-S], or error code 1A93H [FX5-SSC-G]) or "Software stroke limit -" (error code: 1995H [FX5-SSC-S], or error code 1A95H [FX5-SSC-G]) will occur and the operation cannot start if the start point address or end point address for position control exceeds the software stroke limit range.
- Deceleration stop will be carried out if the position-speed switching signal is not input before the machine is moved by a specified movement amount. When the position-speed switching signal is input during automatic deceleration by positioning control, acceleration is carried out again to the command speed to continue speed control. When the position-speed switching signal is input during deceleration to a stop with the stop signal, the control is switched to the speed control to stop the machine. Restart is carried out by speed control using the restart command.
- The warning "Speed limit value over" (warning code: 0991H [FX5-SSC-S], or warning code 0D51H [FX5-SSC-G]) will occur and control is continued by "[Pr.8] Speed limit value" if a new speed exceeds "[Pr.8] Speed limit value" at the time of change of the command speed.
- If the value set in "[Da.6] Positioning address/movement amount" is negative, the error "Outside address range" (error code: 1A30H [FX5-SSC-S], or error codes 1B30H and 1B31H [FX5-SSC-G]) will occur.
- Set WITH mode in the output timing at M code use. The M code will not be output, and the M code ON signal will not turn ON if the AFTER mode is set.

#### Setting positioning data (設定する位置決めデータ) (3.2 / original p.129)

When using position-speed switching control, set the following positioning data.
◎: Always set, ○: Set as required, —: Setting not required

| Setting item | | Setting required/not required |
|---|---|---|
| [Da.1] | Operation pattern | ◎ |
| [Da.2] | Control method | ◎<br>(Set "Forward run: position/speed" or "Reverse run: position/speed".) |
| [Da.3] | Acceleration time No. | ◎ |
| [Da.4] | Deceleration time No. | ◎ |
| [Da.6] | Positioning address/movement amount | ◎ |
| [Da.7] | Arc address | — |
| [Da.8] | Command speed | ◎ |
| [Da.9] | Dwell time/JUMP destination positioning data No. | ○ |
| [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | ○ |
| [Da.20] | Axis to be interpolated No.1 | — |
| [Da.21] | Axis to be interpolated No.2 | — |
| [Da.22] | Axis to be interpolated No.3 | — |

Refer to the following for information on the setting details.
→Page 497 Positioning Data

### Current value changing (現在値変更) (3.2 / original p.130-133)

When the current value is changed to a new value, control is carried out in which the "[Md.20] Command position value" of the stopped axis is changed to a random address set by the user. (The "[Md.21] Machine feed value" is not changed when the current value is changed.)
The two methods for changing the current value are shown below.
- Changing to a new current value using the positioning data
- Changing to a new current value using the start No. (No.9003) for a current value changing

The current value changing using method [1] is used during continuous positioning of multiple blocks, etc.

#### Changing to a new current value using the positioning data (位置決めデータを使った現在値変更の場合) (3.2 / original p.130-131)

In "current value changing" ("[Da.2] Control method" = current value changing), "[Md.20] Command position value" is changed to the address set in "[Da.6] Positioning address/movement amount".

##### Operation chart (動作図) (3.2 / original p.130)

The following chart shows the operation timing for a current value changing. The "[Md.20] Command position value" is changed to the value set in "[Da.6] Positioning address/movement amount" when the positioning start signal turns ON.

[Figure] Current value changing using the positioning data (original p.130)
- [Cd.184] Positioning start: OFF → ON (pulse).
- [Md.20] Command position value: 50000 → 0 at the moment [Cd.184] turns ON.
- Note in the chart: "Command position value changes to the positioning address designated by the positioning data of the current value changing."
- Note in the chart: "The above chart shows an example when the positioning address is "0"."

##### Restrictions (制約事項) (3.2 / original p.130)

- The error "New current value not possible" (error code: 1A1CH [FX5-SSC-S], or error codes 1B1CH and 1B1DH [FX5-SSC-G]) will occur and the operation cannot start if "continuous path control" is set in "[Da.1] Operation pattern". ("Continuous path control" cannot be set in current value changing.)
- "Current value changing" cannot be set in "[Da.2] Control method" of the positioning data when "continuous path control" has been set in "[Da.1] Operation pattern" of the immediately prior positioning data. (For example, if the operation pattern of positioning data No.1 is "continuous path control", "current value changing" cannot be set in positioning data No.2.) The error "New current value not possible" (error code: 1A1CH [FX5-SSC-S], or error codes 1B1CH and 1B1DH [FX5-SSC-G]) will occur and the machine will carry out a deceleration stop if this type of setting is carried out.
- The error "Outside new current value range" (error code: 1997H [FX5-SSC-S], or error code 1A97H [FX5-SSC-G]) will occur and the operation cannot start if "degree" is set in "[Pr.1] Unit setting" and the value set in "[Da.6] Positioning address/movement amount (0 to 359.99999 [degree])" is outside the setting range.
- If the value set in "[Da.6] Positioning address/movement amount" is outside the software stroke limit ([Pr.12], [Pr.13]) setting range, the error "Software stroke limit +" (error code: 1A18H [FX5-SSC-S], or error code 1B18H [FX5-SSC-G]) or "Software stroke limit -" (error code: 1A1AH [FX5-SSC-S], or error code 1B1AH [FX5-SSC-G]) will occur at the positioning start, and the operation will not start.
- The error "Software stroke limit +" (error code: 1993H [FX5-SSC-S], or error code 1A94H*1 [FX5-SSC-G]) or "Software stroke limit -" (error code: 1995H [FX5-SSC-S], or error code 1A96H*2 [FX5-SSC-G]) will occur if the new position value is outside the software stroke limit range.

*1 1A93H for the software version 1.000.
*2 1A95H for the software version 1.000.

- The new current value using the positioning data (No.1 to 600) cannot be changed, if "0: Positioning control is not executed" is set in "[Pr.55] Operation setting for incompletion of home position return" and "home position return request flag" ON. The error "Start at home position return incomplete" (error code: 19A6H [FX5-SSC-S], or error code 1AA6H [FX5-SSC-G]) will occur.
- When using an absolute position system, "[Md.20] Command position value" returns to the value of "[Md.21] Machine feed value" at the start of communication with the servo amplifier after cycling the power or resetting the CPU module.

##### Setting positioning data (設定する位置決めデータ) (3.2 / original p.131)

When using current value changing, set the following positioning data.
◎: Always set, ○: Set as required, —: Setting not required

| Setting item | | Setting required/not required |
|---|---|---|
| [Da.1] | Operation pattern | ◎ |
| [Da.2] | Control method | ◎<br>(Set the current value changing.) |
| [Da.3] | Acceleration time No. | — |
| [Da.4] | Deceleration time No. | — |
| [Da.6] | Positioning address/movement amount | ◎<br>(Set the address to be changed.) |
| [Da.7] | Arc address | — |
| [Da.8] | Command speed | — |
| [Da.9] | Dwell time/JUMP destination positioning data No. | — |
| [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | ○ |
| [Da.20] | Axis to be interpolated No.1 | — |
| [Da.21] | Axis to be interpolated No.2 | — |
| [Da.22] | Axis to be interpolated No.3 | — |

Refer to the following for information on the setting details.
→Page 497 Positioning Data

#### Changing to a new current value using the current value changing start No. (No.9003) (現在値変更用始動番号(No.9003)を使った現在値変更の場合) (3.2 / original p.131-133)

In "current value changing" ("[Cd.3] Positioning start No." = 9003), "[Md.20] Command position value" is changed to the address set in "[Cd.9] New position value".

##### Operation chart (動作図) (3.2 / original p.131)

The current value is changed by setting the new current value in the current value changing buffer memory "[Cd.9] New position value", setting "9003" in the "[Cd.3] Positioning start No.", and turning ON the positioning start signal.

[Figure] Current value changing using No.9003 (original p.131)
- [Cd.184] Positioning start: OFF → ON (pulse).
- [Md.20] Command position value: 50000 → 0 at the moment [Cd.184] turns ON.
- Note in the chart: "Current value changes to the positioning address designated by the current value changing buffer memory."
- Note in the chart: "The above chart shows an example when the positioning address is "0"."

##### Restrictions (制約事項) (3.2 / original p.131)

- The error "Outside new current value range" (error code: 1997H [FX5-SSC-S], or error code 1A97H [FX5-SSC-G]) will occur if the designated value is outside the setting range when "degree" is set in "Unit setting".
- The error "Software stroke limit +" (error code: 1993H [FX5-SSC-S], or error code 1A94H*1 [FX5-SSC-G]) or "Software stroke limit -" (error code: 1995H [FX5-SSC-S], or error code 1A96H*2 [FX5-SSC-G]) will occur if the designated value is outside the software stroke limit range.

*1 1A93H for the software version 1.000.
*2 1A95H for the software version 1.000.

- The current value cannot be changed during stop commands and while the M code ON signal is ON.
- The M code output function is made invalid.
- When an absolute position system is used, "[Md.20] Command position value" returns to the same value as "[Md.21] Machine feed value" at the start of communication with the servo amplifier after the power supply ON or the CPU module reset.

> **Point** (original p.132)
> The new current value can be changed using the current value changing start No. (No.9003) if "0: Positioning control is not executed" is set in "[Pr.55] Operation setting for incompletion of home position return" and home position return request flag is ON.

##### Current value changing procedure (現在値変更手順) (3.2 / original p.132)

The following shows the procedure for changing the current value to a new value.
1. Write the current value to "[Cd.9] New position value".
2. Write "9003" in "[Cd.3] Positioning start No.".
3. Turn ON the positioning start signal.

##### Setting method for the current value changing function (設定方法) (3.2 / original p.132)

The following shows an example of a program and data setting to change the current value to a new value with the positioning start signal. (The value "[Md.20] Command position value" is changed to "5000.0 μm" in the example shown.)
- Set the following data. (Set using the program referring to the start time chart.)

n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.3] | Positioning start No. | 9003 | Set the start No. "9003" for the new current value. | 4300+100n |
| [Cd.9] | New position value | 50000 | Set the new "[Md.20] Command position value". | 4306+100n<br>4307+100n |

Refer to the following for details on the setting details.
→Page 561 Control Data
- The following shows a start time chart.

##### Operation example (動作例) (3.2 / original p.132)

[Figure] Start time chart of current value changing (No.9003) (original p.132)
- V-t: a normal positioning (trapezoid) is executed first; later, while stopped, "Start of data No.9003" (no movement).
- [Cd.190] PLC READY OFF→ON first → READY signal ([Md.140] Module status: b0) OFF→ON.
- [Cd.184] Positioning start: 1st ON (normal positioning) → OFF after the positioning completes; 2nd ON (start of data No.9003) → OFF.
- Start complete signal ([Md.31] Status: b14): turns ON following each [Cd.184] ON, OFF following each [Cd.184] OFF.
- [Md.141] BUSY: ON at the 1st start, OFF at the stop; at the No.9003 start it turns ON for a short time and OFF.
- Positioning complete signal ([Md.31] Status: b15): ON when the 1st positioning stops, OFF at the next start; ON again after the No.9003 start, then OFF.
- Error detection signal ([Md.31] Status: b13): stays OFF.
- [Md.20] Command position value: "Address during positioning execution" → 50000 (at the start of data No.9003).
- [Cd.3] Positioning start No.: "Data No. during positioning execution" → 9003 (set after the 1st positioning completes).
- [Cd.9] New position value: 50000 (set after the 1st positioning completes).

##### Program example (プログラム例) (3.2 / original p.133)

Add the following program to the control program, and write it to the CPU module.

[Figure] Program example of current value changing (No.9003) (ladder with labels) (original p.133)
- Step numbers: (0), (5), (28)

Mnemonic transcription (label names as in the original, including the spelling "dNewPositonValue"; the device shown under each module label in the ladder is given after `;`):

```text
(0)
LD    bInputCommandPositionValChangeReq
PLS   bCommandPositionValueChangeReq_P
(5)
LD    bCommandPositionValueChangeReq_P
ANI   FX5SSC_1.stnAxCtrl2_D[0].uPositioningStart_D.0     ; U1\G30104.0
ANI   FX5SSC_1.stnAxMntr_D[0].uStatus_D.E                ; U1\G2417.E
DMOVP dNewPositonValue FX5SSC_1.stnAxCtrl1_D[0].dNewPosition_D      ; U1\G4306
MOVP  K9003 FX5SSC_1.stnAxCtrl1_D[0].uPositioningStartNo_D          ; U1\G4300
SET   FX5SSC_1.stnAxCtrl2_D[0].uPositioningStart_D.0     ; U1\G30104.0
(28)
LD    FX5SSC_1.stnAxCtrl2_D[0].uPositioningStart_D.0     ; U1\G30104.0
LD    FX5SSC_1.stnAxMntr_D[0].uStatus_D.E                ; U1\G2417.E
OR    FX5SSC_1.stnAxMntr_D[0].uStatus_D.D                ; U1\G2417.D
ANB
ANI   FX5SSC_1.stSysMntr2_D.bnBusy_D[0]                  ; U1\G31501.0
RST   FX5SSC_1.stnAxCtrl2_D[0].uPositioningStart_D.0     ; U1\G30104.0
```

- Contact types (read from the figure): in (5), uPositioningStart_D.0 and uStatus_D.E are NC (b) contacts; in (28), bnBusy_D[0] is an NC (b) contact; the others are NO (a) contacts. In (28), uStatus_D.E and uStatus_D.D are in parallel. In (5), DMOVP / MOVP / SET are parallel outputs of the same condition.

| Classification | Label name | Description |
|---|---|---|
| Module label | FX5SSC_1.stnAxCtrl2_D[0].uPositioningStart_D.0 | Axis 1 Positioning start signal |
| Module label | FX5SSC_1.stnAxMntr_D[0].uStatus_D.E | Axis 1 Start complete |
| Module label | FX5SSC_1.stnAxCtrl1_D[0].dNewPosition_D | Axis 1 New position value |
| Module label | FX5SSC_1.stnAxCtrl1_D[0].uPositioningStartNo_D | Axis 1 Positioning start No. |
| Module label | FX5SSC_1.stnAxMntr_D[0].uStatus_D.D | Axis 1 Error detection |
| Module label | FX5SSC_1.stSysMntr2_D.bnBusy_D[0] | Axis 1 BUSY signal |
| Global label, local label | (below) | Defines the global label or the local label as follows. The settings of Assign (Device/Label) are not required for the label that the assignment device is not set because the unused internal relay and data device are automatically assigned.<br>The following are for local labels. |

*In the original, "Module label" is merged over 6 rows. Expanded to each row.

Local label definition (transcribed from the screen image in the original):

| No. | Label Name | Data Type | Class |
|---|---|---|---|
| 1 | dNewPositonValue | Double Word [Signed] | VAR |
| 2 | bCommandPositionValueChangeReq_P | Bit | VAR |
| 3 | bInputCommandPositionValChangeReq | Bit | VAR |

### NOP instruction (NOP命令) (3.2 / original p.134)

The NOP instruction is used for the nonexecutable control method.

#### Operation (動作) (3.2 / original p.134)

The positioning data No. to which the NOP instruction is set transfers, without any processing, to the operation for the next positioning data No.

#### Setting positioning data (設定する位置決めデータ) (3.2 / original p.134)

When using the NOP instruction, set the following positioning data.
◎: Always set, ○: Set as required, —: Setting not required

| Setting item | | Setting required/not required |
|---|---|---|
| [Da.1] | Operation pattern | — |
| [Da.2] | Control method | ◎<br>(Set the NOP instruction.) |
| [Da.3] | Acceleration time No. | — |
| [Da.4] | Deceleration time No. | — |
| [Da.6] | Positioning address/movement amount | — |
| [Da.7] | Arc address | — |
| [Da.8] | Command speed | — |
| [Da.9] | Dwell time/JUMP destination positioning data No. | — |
| [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | — |
| [Da.20] | Axis to be interpolated No.1 | — |
| [Da.21] | Axis to be interpolated No.2 | — |
| [Da.22] | Axis to be interpolated No.3 | — |

Refer to the following for information on the setting details.
→Page 497 Positioning Data

#### Restrictions (制約事項) (3.2 / original p.134)

The error "Control method setting error" (error code: 1A24H [FX5-SSC-S], or error code 1B26H*1 [FX5-SSC-G]) will occur if the "NOP instruction" is set for the control method of the positioning data No.600.
*1 1B24H for the software version 1.000.

> **Point**
> Example of NOP instruction usage
> If there is a possibility of speed switching or temporary stop (automatic deceleration) at a point between two points during positioning, that data can be reserved with the NOP instruction to change the data merely by the replacement of the identifier.

### JUMP instruction (JUMP命令) (3.2 / original p.135-136)

The JUMP instruction is used to control the operation so it jumps to a positioning data No. set in the positioning data during "continuous positioning control" or "continuous path control".
JUMP instruction includes the following two types of JUMP.

| JUMP instruction | Description |
|---|---|
| Unconditional JUMP | When execution conditions are not set for the JUMP instruction (When "0" is set to the condition data No.) |
| Conditional JUMP | When execution conditions are set for the JUMP instruction (The conditions are set to the "condition data" used with "high-level positioning control".) |

Using the JUMP instruction enables repeating of the same positioning control, or selection of positioning data by the execution conditions during "continuous positioning control" or "continuous path control".

#### Operation (動作) (3.2 / original p.135)

##### Unconditional JUMP (無条件JUMPの場合) (3.2 / original p.135)

The JUMP instruction is unconditionally executed. The operation jumps to the positioning data No. set in "[Da.9] Dwell time/JUMP destination positioning data No.".

##### Conditional JUMP (条件付きJUMPの場合) (3.2 / original p.135)

The block start condition data is used as the JUMP instruction execution conditions.
- When block positioning data No.7000 to 7004 is started, each block condition data is used.
- When positioning data No.1 to 600 is started, start block 0 condition data is used.
- When the execution conditions set in "[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions" of the JUMP instruction have been established, the JUMP instruction is executed to jump the operation to the positioning data No. set in "[Da.9] Dwell time/JUMP destination positioning data No.".
- When the execution conditions set in "[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions" of the JUMP instruction have not been established, the JUMP instruction is ignored, and the next positioning data No. is executed.

#### Restrictions (制約事項) (3.2 / original p.135)

- When using a conditional JUMP instruction, establish the JUMP instruction execution conditions by the 4th positioning data No. before the JUMP instruction positioning data No. If the JUMP instruction execution conditions are not established by the time the 4th positioning control is carried out before the JUMP instruction positioning data No., the operation will be processed as an operation without established JUMP instruction execution conditions. (During execution of continuous path control/continuous positioning control, the Simple Motion module/Motion module calculates the positioning data of the positioning data No. four items ahead of the current positioning data.)
- Set JUMP instruction to positioning data No. that "continuous positioning control" or "continuous path control" is set in operation pattern. It cannot set to positioning data No. that "positioning complete" is set in operation pattern.
- Positioning control such as loops cannot be executed by conditional JUMP instructions alone until the conditions have been established. When loop control is executed using JUMP instruction, an axis operation status is "analyzing" during loop control, and the positioning data analysis (start) for other axes are not executed. As the target of the JUMP instruction, specify a positioning data that is controlled by other than JUMP and NOP instructions.

#### Setting positioning data (設定する位置決めデータ) (3.2 / original p.136)

When using the JUMP instruction, set the following positioning data.
◎: Always set, ○: Set as required, —: Setting not required

| Setting item | | Setting required/not required |
|---|---|---|
| [Da.1] | Operation pattern | — |
| [Da.2] | Control method | ◎<br>(Set the JUMP instruction.) |
| [Da.3] | Acceleration time No. | — |
| [Da.4] | Deceleration time No. | — |
| [Da.6] | Positioning address/movement amount | — |
| [Da.7] | Arc address | — |
| [Da.8] | Command speed | — |
| [Da.9] | Dwell time/JUMP destination positioning data No. | ◎<br>(Set the positioning data No.1 to 600 for the JUMP destination.) |
| [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | ◎<br>(Set the JUMP instruction execution conditions with the condition data No.<br>0: Unconditional JUMP<br>1 to 10: Condition data No. ("Simultaneous start" condition data cannot be set.)) |
| [Da.20] | Axis to be interpolated No.1 | — |
| [Da.21] | Axis to be interpolated No.2 | — |
| [Da.22] | Axis to be interpolated No.3 | — |

Refer to the following for information on the setting details.
→Page 497 Positioning Data

### LOOP (LOOP) (3.2 / original p.137)

The LOOP is used for loop control by the repetition of LOOP to LEND.

#### Operation (動作) (3.2 / original p.137)

The LOOP to LEND loop is repeated by set repeat cycles.

#### Setting positioning data (設定する位置決めデータ) (3.2 / original p.137)

When using the LOOP, set the following positioning data.
◎: Always set, ○: Set as required, —: Setting not required

| Setting item | | Setting required/not required |
|---|---|---|
| [Da.1] | Operation pattern | — |
| [Da.2] | Control method | ◎<br>(Set the LOOP.) |
| [Da.3] | Acceleration time No. | — |
| [Da.4] | Deceleration time No. | — |
| [Da.6] | Positioning address/movement amount | — |
| [Da.7] | Arc address | — |
| [Da.8] | Command speed | — |
| [Da.9] | Dwell time/JUMP destination positioning data No. | — |
| [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | ◎<br>(Set the repeat cycles.) |
| [Da.20] | Axis to be interpolated No.1 | — |
| [Da.21] | Axis to be interpolated No.2 | — |
| [Da.22] | Axis to be interpolated No.3 | — |

Refer to the following for information on the setting details.
→Page 497 Positioning Data

#### Restrictions (制約事項) (3.2 / original p.137)

- The error "Control method LOOP setting error" (error code: 1A33H [FX5-SSC-S], or error code 1B33H [FX5-SSC-G]) will occur if a "0" is set for the repeat cycles.
- Even if LEND is absent after LOOP, no error will occur, but repeat processing will not be carried out.
- Nesting is not allowed between LOOP-LEND's. If such setting is made, only the inner LOOP-LEND is processed repeatedly.

> **Point**
> The setting by this control method is easier than that by the special start "FOR loop". (→Page 147 Repeated start (FOR loop))
> - For special start: Positioning start data, special start data, condition data, and positioning data
> - For control method: Positioning data
>
> For the special start FOR to NEXT, the positioning data is required for each of FOR and NEXT points. For the control method, loop can be executed even only by one data.
> Also, nesting is enabled by using the control method LOOP to LEND in combination with the special start FOR to NEXT. However LOOP to LEND cannot be set across block. Always set LOOP to LEND so that the processing ends within one block.
> For details of the "block", refer to the following.
> →Page 137 HIGH-LEVEL POSITIONING CONTROL

### LEND (LEND) (3.2 / original p.138)

The LEND is used to return the operation to the top of the repeat (LOOP to LEND) loop.

#### Operation (動作) (3.2 / original p.138)

When the repeat cycle designated by the LOOP becomes 0, the loop is terminated, and the next positioning data No. processing is started. (The operation pattern, if set to "Positioning complete", will be ignored.)
When the operation is stopped after the repeat operation is executed by designated cycles, the dummy positioning data (for example, incremental positioning without movement amount) is set next to LEND.
The following table shows the operation when the positioning complete (00) is set to LOOP and LEND.

| Positioning data No. | Operation pattern | Control method | Conditions | Operation |
|---|---|---|---|---|
| 1 | Continuous control | ABS2 | | Executed in the order of the positioning data No.1 → 2 → 3 → 4 → 5 → 2 → 3 → 4 → 5 → 6.<br>(The operation patterns of the positioning data Nos. 2 and 5 are ignored.) |
| 2 | Positioning complete | LOOP | Number of loop cycles: 2 | Executed in the order of the positioning data No.1 → 2 → 3 → 4 → 5 → 2 → 3 → 4 → 5 → 6.<br>(The operation patterns of the positioning data Nos. 2 and 5 are ignored.) |
| 3 | Continuous path control | ABS2 | | Executed in the order of the positioning data No.1 → 2 → 3 → 4 → 5 → 2 → 3 → 4 → 5 → 6.<br>(The operation patterns of the positioning data Nos. 2 and 5 are ignored.) |
| 4 | Continuous control | ABS2 | | Executed in the order of the positioning data No.1 → 2 → 3 → 4 → 5 → 2 → 3 → 4 → 5 → 6.<br>(The operation patterns of the positioning data Nos. 2 and 5 are ignored.) |
| 5 | Positioning complete | LEND | | Executed in the order of the positioning data No.1 → 2 → 3 → 4 → 5 → 2 → 3 → 4 → 5 → 6.<br>(The operation patterns of the positioning data Nos. 2 and 5 are ignored.) |
| 6 | Positioning complete | ABS2 | | Executed in the order of the positioning data No.1 → 2 → 3 → 4 → 5 → 2 → 3 → 4 → 5 → 6.<br>(The operation patterns of the positioning data Nos. 2 and 5 are ignored.) |

*In the original, the "Operation" cell is merged over the 6 rows. Expanded to each row.

#### Setting positioning data (設定する位置決めデータ) (3.2 / original p.138)

When using the LEND, set the following positioning data.
◎: Always set, ○: Set as required, —: Setting not required

| Setting item | | Setting required/not required |
|---|---|---|
| [Da.1] | Operation pattern | — |
| [Da.2] | Control method | ◎<br>(Set the LEND.) |
| [Da.3] | Acceleration time No. | — |
| [Da.4] | Deceleration time No. | — |
| [Da.6] | Positioning address/movement amount | — |
| [Da.7] | Arc address | — |
| [Da.8] | Command speed | — |
| [Da.9] | Dwell time/JUMP destination positioning data No. | — |
| [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | — |
| [Da.20] | Axis to be interpolated No.1 | — |
| [Da.21] | Axis to be interpolated No.2 | — |
| [Da.22] | Axis to be interpolated No.3 | — |

Refer to the following for information on the setting details.
→Page 497 Positioning Data

#### Restrictions (制約事項) (3.2 / original p.138)

- Ignore the "LEND" before the "LOOP" is executed.
- When the operation pattern "Positioning complete" has been set between LOOP and LEND, the positioning control is completed after the positioning data is executed, and the LOOP control is not executed.
