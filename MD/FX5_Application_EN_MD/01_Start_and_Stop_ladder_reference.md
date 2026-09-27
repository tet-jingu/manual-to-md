# 1 START AND STOP (始動と停止) (Chapter 1 / original p.24-37)

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
> - The original "☞" (page reference mark) is written as "→", and "📖" (other manual mark) as "[Other manual]".
> - Headings carry the Japanese term in parentheses for search. Body text is the original English only.

## Conversion range (変換範囲表 / original p.24-37)

| Original page | Section | Handling |
|---|---|---|
| p.24-31 | 1.1 Start | Full text |
| p.32-35 | 1.2 Stop | Full text |
| p.36-37 | 1.3 Restart | Full text (program example is only a reference to Chapter 12/13; no body in this chapter) |

## Table of Contents (目次)

- 1 START AND STOP (始動と停止)
  - 1.1 Start (始動)
  - 1.2 Stop (停止)
  - 1.3 Restart (再始動)

---

## 1 START AND STOP (始動と停止) (Chapter 1 / original p.24)

This chapter describes start and stop methods of the positioning control for the Simple Motion module/Motion module.

## 1.1 Start (始動) (1.1 / original p.24-31)

The Simple Motion module/Motion module operates the start trigger in each control, and starts the positioning control. The following table shows the start signals for each control. This section describes the start using the positioning start signal and the external command signal.

| Control details | | Start trigger |
|---|---|---|
| Major positioning control | — | • Turns ON the "[Cd.184] Positioning start".<br>• Turns ON the external command signal (DI). |
| High-level positioning control | — | • Turns ON the "[Cd.184] Positioning start".<br>• Turns ON the external command signal (DI). |
| Home position return control | — | • Turns ON the "[Cd.184] Positioning start".<br>• Turns ON the external command signal (DI). |
| Manual control | JOG operation | Turns ON the "[Cd.181] Forward run JOG start" or the "[Cd.182] Reverse run JOG start". |
| Manual control | Inching operation | Turns ON the "[Cd.181] Forward run JOG start" or the "[Cd.182] Reverse run JOG start". |
| Manual control | Manual pulse generator operation | Operates the manual pulse generator. |

*In the original, the "Start trigger" cell is merged over the 3 rows Major positioning control / High-level positioning control / Home position return control, and over the 2 rows JOG operation / Inching operation. "Manual control" is merged over 3 rows. Expanded to each row.

In the control other than the manual control, the following start methods can be selected.
- Normal start (→Page 142 Block start)
- Multiple axes simultaneous start (→Page 28 Multiple axes simultaneous start)

The positioning data, block start data, and condition data are used for the position specified at the control. The data that can be used varies by the start method.

### Servo ON conditions (サーボON条件) (1.1 / original p.24)

Setting of servo parameter
↓
"[Cd.190] PLC READY" ON
↓
"[Cd.191] All axis servo ON" ON

### Starting conditions (始動条件) (1.1 / original p.24-25)

To start the control, the following conditions must be satisfied.
The necessary start conditions must be incorporated in the program so that the control is not started when the conditions are not satisfied.

- Operation state

n: Axis No. - 1

| Monitor item | | Operation state | Buffer memory address |
|---|---|---|---|
| [Md.26] | Axis operation status | "0: Standby" or "1: Stopped" | 2409+100n |

- Signal state (original p.25)

| Signal name | | Signal state | | Device |
|---|---|---|---|---|
| I/O signal | PLC READY signal | ON | CPU module preparation completed | [Cd.190] PLC READY |
| I/O signal | READY signal | ON | Preparation completed | [Md.140] Module status: b0 |
| I/O signal | All axis servo ON | ON | All axis servo ON | [Cd.191] All axis servo ON |
| I/O signal | Synchronization flag | ON | The buffer memory can be accessed. | [Md.140] Module status: b1 |
| I/O signal | Axis stop signal | OFF | Axis stop signal is OFF | [Cd.180] Axis stop |
| I/O signal | M code ON signal | OFF | M code ON signal is OFF | [Md.31] Status: b12 |
| I/O signal | Error detection signal | OFF | There is no error | [Md.31] Status: b13 |
| I/O signal | BUSY signal | OFF | BUSY signal is OFF | [Md.141] BUSY |
| I/O signal | Start complete signal | OFF | Start complete signal is OFF | [Md.31] Status: b14 |
| External signal | Forced stop input signal | ON | There is no forced stop input | — |
| External signal | Stop signal | OFF | Stop signal is OFF | — |
| External signal | Upper limit (FLS) | ON | Within limit range | — |
| External signal | Lower limit (RLS) | ON | Within limit range | — |

*In the original, "I/O signal" is merged over 9 rows and "External signal" over 4 rows. Expanded to each row.

### Start by the positioning start [Cd.184] (位置決め始動[Cd.184]による始動) (1.1 / original p.26-27)

The operation at starting by the "[Cd.184] Positioning start" is shown below.
- When the "[Cd.184] Positioning start" turns ON, the start complete signal ([Md.31] Status: b14) and "[Md.141] BUSY" turn ON, and the positioning operation starts. It can be seen that the axis is operating when the "[Md.141] BUSY" is ON.
- When the "[Cd.184] Positioning start" turns OFF, the start complete signal ([Md.31] Status: b14) also turns OFF. If the "[Cd.184] Positioning start" is ON even after positioning is completed, the start complete signal ([Md.31] Status: b14) will remain ON.
- If the positioning start signal turns ON again while the "[Md.141] BUSY" is ON, the warning "Start during operation" (warning code: 0900H [FX5-SSC-S], or warning code: 0D00H [FX5-SSC-G])" will occur.
- The process executed when the positioning operation is completed will differ by whether the next positioning control is executed.

| Whether the next positioning control is executed | Processing details |
|---|---|
| Do not execute the positioning | • If a dwell time is set, the system will wait for the set time to pass, and then positioning will be completed.<br>• When positioning is completed, the "[Md.141] BUSY" will turn OFF and the positioning complete signal ([Md.31] Status: b15) will turn ON. However, when using speed control or when the positioning complete signal output time is "0", the signal will not turn ON.<br>• When the time set in "[Pr.40] Positioning complete signal output time" is passed, the positioning complete signal ([Md.31] Status: b15) will turn OFF. |
| Execute the positioning | • If a dwell time is set, the system will wait for the set time to pass.<br>• When the set dwell time is passed, the next positioning will start. |

#### Operation example (動作例) (1.1 / original p.26)

[Figure] Timing chart of start by [Cd.184] Positioning start (original p.26)
- Signals (top to bottom): Positioning (V-t), [Cd.191] All axis servo ON, [Cd.184] Positioning start, Start complete signal ([Md.31] Status: b14), [Md.141] BUSY, Positioning complete signal ([Md.31] Status: b15)
- [Cd.191] All axis servo ON turns OFF→ON first; then [Cd.184] Positioning start turns ON.
- On the rise of [Cd.184], the start complete signal (b14) and [Md.141] BUSY turn ON, and the positioning (several continuous speed steps) starts.
- The positioning complete signal (b15) turns ON for a short time at the end of each positioning data (several pulses during the operation); a "Dwell time" is shown between a positioning end and the next positioning start.
- At the end of the last positioning, [Md.141] BUSY turns OFF and the positioning complete signal (b15) turns ON; then b15 turns OFF.
- [Cd.184] turns OFF after BUSY OFF; the start complete signal (b14) turns OFF following [Cd.184] OFF.

> **Point**
> The "[Md.141] BUSY" turns ON even when position control of movement amount 0 is executed. However, since the ON time is short, the ON status may not be detected in the program. (The ON status of the start complete signal ([Md.31] Status: b14), positioning complete signal ([Md.31] Status: b15) and M code ON signal ([Md.31] Status: b12) can be detected in the program.)

#### Operation timing and processing time (動作タイミングと処理時間) (1.1 / original p.27)

The following shows details about the operation timing and time during position control.
- Operation example

[Figure] Operation timing during position control (original p.27)
- [Cd.184] Positioning start ON → after t1, [Md.141] BUSY turns ON; at the same time the start complete signal (b14) turns ON, [Md.26] Axis operation status changes "Standby" → "Position control", and the M code ON signal (b12) (WITH mode) turns ON.
- The positioning complete signal (b15) and the home position return complete flag (b4) (shown dashed = if already ON) turn OFF at the time BUSY turns ON.
- M code ON signal (WITH mode): turns OFF t2 after [Cd.7] M code OFF request turns ON.
- Positioning operation starts t4 after BUSY ON.
- t5 after the positioning operation ends, [Md.141] BUSY turns OFF, [Md.26] returns to "Standby", the positioning complete signal (b15) turns ON, and the M code ON signal (AFTER mode) turns ON.
- The positioning complete signal (b15) turns OFF t6 after it turns ON.
- M code ON signal (AFTER mode): turns OFF t2 after [Cd.7] M code OFF request turns ON.
- Start complete signal (b14): turns OFF t3 after [Cd.184] Positioning start turns OFF.

> **Point**
> When the positioning start signal turns ON, if the "positioning complete signal" or the "home position return complete flag" are already ON, the "positioning complete signal" or the "home position return complete flag" will turn OFF when the positioning start signal turns ON.

- Normal timing time (Unit: [ms])

| Model | Operation cycle | t1*1 | t2 | t3 | t4*2 | t5 | t6 |
|---|---|---|---|
| FX5-SSC-S | 0.888 | 0.3 to 1.4 | 0 to 0.9 | 0 to 0.9 | 3.71 to 4.59 | 0 to 0.9 | Follows parameters |
| FX5-SSC-S | 1.777 | 0.3 to 1.4 | 0 to 1.8 | 0 to 1.8 | 4.57 to 6.28 | 0 to 1.8 | Follows parameters |
| FX5-SSC-G | 0.500 | 0.4 to 1.0 | 0 to 0.5 | 0 to 0.5 | 1.8 to 2.0 | 0 to 0.5 | Follows parameters |
| FX5-SSC-G | 1.000 | 0.4 to 1.5 | 0 to 1.0 | 0 to 1.0 | 3.3 to 3.5 | 0 to 1.0 | Follows parameters |
| FX5-SSC-G | 2.000 | 0.4 to 2.8 | 0 to 2.0 | 0 to 2.0 | 6.0 to 6.4 | 0 to 2.0 | Follows parameters |
| FX5-SSC-G | 4.000 | 0.4 to 4.5 | 0 to 4.0 | 0 to 4.0 | 12.0 to 12.2 | 0 to 4.0 | Follows parameters |

*In the original, "Operation cycle" is one header spanning the model and cycle columns; the model cell is merged (FX5-SSC-S over 2 rows, FX5-SSC-G over 4 rows). Expanded to each row.

*1 The t1 timing time could be delayed by the operation state of other axes.
*2 The t4 timing time depends on the setting of the acceleration time, servo parameter, etc.

### Start by the external command signal (DI) (外部指令信号(DI)による始動) (1.1 / original p.28-29)

[FX5-SSC-S]
When starting positioning control by inputting the external command signal (DI), the start command can be directly input into the Simple Motion module. This allows the variation time equivalent to one scan time of the CPU module to be eliminated. This is an effective procedure when operation is to be started as quickly as possible with the start command or when the starting variation time is to be suppressed.

[FX5-SSC-G]
When starting positioning control by inputting the external command signal (DI), the start command from the drive unit can be directly input into the Motion module.

#### Advance setting (事前設定) (1.1 / original p.28)

Set the following data in advance.
N: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Pr.42] | External command function selection | 0 | Set to "0: External positioning start". | 62+150n |
| [Pr.95] | External command signal selection | 0 | Set the external command signal (DI) to be used. | 69+150n |

Set the external command signal (DI) to be used in "[Pr.95] External command signal selection".
Refer to the following for the setting details.
→Page 444 Basic Setting

#### Start method (始動方法) (1.1 / original p.28)

Set "[Cd.3] Positioning start No." and enable "[Cd.8] External command valid" with a program. Then, turn ON the external command signal (DI).
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.3] | Positioning start No. | 1 to 600 | Set the positioning data No. to be started. | 4300+100n |
| [Cd.8] | External command valid | 1 | Set to "1: Validates an external command.". | 4305+100n |

Refer to the following for the setting details.
→Page 561 Control Data

#### Restriction (制限事項) (1.1 / original p.28)

When starting by inputting the external command signal (DI), the start complete signal ([Md.31] Status: b14) will not turn ON.

#### Starting time chart (始動タイムチャート) (1.1 / original p.29)

- Operation example

[Figure] Starting time chart by external command signal (DI) (original p.29)
- Operation pattern / Positioning data No.: 1(00); a dwell time follows the end of the positioning.
- [Cd.190] PLC READY ON → READY signal ([Md.140] Module status: b0) ON.
- [Cd.191] All axis servo ON ON → [Md.26] Axis operation status changes "Servo OFF" → "Standby".
- [Cd.184] Positioning start stays OFF throughout.
- Settings before the start: [Pr.42] External command function selection = 0, [Cd.3] Positioning start No. = 1, [Cd.8] External command valid = 1.
- External command signal ON → [Md.141] BUSY turns ON and the positioning starts; [Md.26] leaves "Standby". After the external command signal turns ON, [Cd.8] External command valid changes 1 → 0.
- Start complete signal ([Md.31] Status: b14) stays OFF (see Restriction).
- After the dwell time, [Md.141] BUSY turns OFF and the positioning complete signal ([Md.31] Status: b15) turns ON, then OFF.
- Error detection signal ([Md.31] Status: b13) stays OFF.

### Multiple axes simultaneous start (複数軸同時始動) (1.1 / original p.30-31)

The "multiple axes simultaneous start" starts outputting the command to the specified simultaneous starting axis at the same timing as the started axis. A maximum of four axes can be started simultaneously.

#### Control details (制御内容) (1.1 / original p.30)

The multiple axes simultaneous start control is carried out by setting the simultaneous start setting data to the multiple axes simultaneous start control buffer memory of the axis control data, "9004" to "[Cd.3] Positioning start No." of the start axis, and then turning ON the positioning start signal.
Set the number of axes to be started simultaneously and axis No. in "[Cd.43] Simultaneous starting axis", and the start data No. of simultaneous starting axis (positioning data No. to be started simultaneously for each axis) in "[Cd.30] Simultaneous starting own axis start data No." and "[Cd.31] Simultaneous starting axis start data No.1" to "[Cd.33] Simultaneous starting axis start data No.3".

#### Restrictions (制限事項) (1.1 / original p.30)

- The error "Error before simultaneous start" (error code: 1990H [FX5-SSC-S], or error codes 1A90H and 1A91H [FX5-SSC-G]) will occur and all simultaneously started axes will not start if the simultaneously started axis start data No. is not set to the axis control data on the start axis or set outside the setting range.
- The error "Error before simultaneous start" (error code: 1990H [FX5-SSC-S], or error codes 1A90H and 1A91H [FX5-SSC-G]) will occur and all simultaneously started axes will not start if either of the simultaneously started axes is BUSY.
- The error "Error before simultaneous start" (error code: 1990H [FX5-SSC-S], or error codes 1A90H and 1A91H [FX5-SSC-G]) will occur and all simultaneously started axes will not start if an error occurs during the analysis of the positioning data on the simultaneously started axes.
- No error or warning will occur if only the start axis is the simultaneously started axis.
- This function cannot be used with the sub function (→Page 276 Pre-reading start function).

#### Procedure (手順) (1.1 / original p.30)

The procedure for multiple axes simultaneous start control is shown below.
1. Set the following axis control data.
   - [Cd.43] Simultaneous starting axis
   - [Cd.30] Simultaneous starting own axis start data No.
   - [Cd.31] Simultaneous starting axis start data No.1
   - [Cd.32] Simultaneous starting axis start data No.2
   - [Cd.33] Simultaneous starting axis start data No.3
2. Write [9004] in "[Cd.3] Positioning start No.".
3. Turn ON the positioning start signal to be started.

#### Setting method (設定方法) (1.1 / original p.31)

The following shows the setting of the data used to execute the multiple axes simultaneous start control with positioning start signals (The axis control data on the start axis is set).
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.3] | Positioning start No. | 9004 | Set the multiple axes simultaneous start control start No. "9004". | 4300+100n |
| [Cd.43] | Simultaneous starting axis | (merged →) | Set the number of simultaneous starting axes and target axis. | 4368+100n<br>4369+100n |
| [Cd.30] | Simultaneous starting own axis start data No. | (merged →) | Set the simultaneously started axis start data No. Set a "0" for the axis other than the simultaneously started axes. | 4340+100n |
| [Cd.31] | Simultaneous starting axis start data No.1 | (merged →) | Set the simultaneously started axis start data No. Set a "0" for the axis other than the simultaneously started axes. | 4341+100n |
| [Cd.32] | Simultaneous starting axis start data No.2 | (merged →) | Set the simultaneously started axis start data No. Set a "0" for the axis other than the simultaneously started axes. | 4342+100n |
| [Cd.33] | Simultaneous starting axis start data No.3 | (merged →) | Set the simultaneously started axis start data No. Set a "0" for the axis other than the simultaneously started axes. | 4343+100n |

*In the original, for [Cd.43] the "Setting value" and "Setting details" cells are merged horizontally; for [Cd.30] to [Cd.33] they are merged horizontally and vertically over the 4 rows. Expanded to each row; "(merged →)" in the Setting value column means the cell is merged with Setting details.

Refer to the following for the setting details.
→Page 561 Control Data

#### Setting examples (設定例) (1.1 / original p.31)

The following shows the setting examples in which the axis 1 is used as the start axis and the axis 2 and axis 4 are used as the simultaneously started axes.

| Setting item | | Setting value | Setting details | Buffer memory address (Axis 1) |
|---|---|---|---|---|
| [Cd.3] | Positioning start No. | 9004 | Set the multiple axes simultaneous start control start No. "9004". | 4300 |
| [Cd.43] | Simultaneous starting axis | 03000301H | Set the axis 2 (01H) to the simultaneously starting axis No.1, and the axis 4 (03H) to the simultaneously starting axis No.2. | 4368, 4369 |
| [Cd.30] | Simultaneous starting own axis start data No. | 100 | The axis 1 starts the positioning data No.100. | 4340 |
| [Cd.31] | Simultaneous starting axis start data No.1 | 200 | Immediately after the start of the axis 1, the axis 2 starts the axis 2 positioning data No.200. | 4341 |
| [Cd.32] | Simultaneous starting axis start data No.2 | 300 | Immediately after the start of the axis 1, the axis 4 starts the axis 4 positioning data No.300. | 4342 |
| [Cd.33] | Simultaneous starting axis start data No.3 | 0 | Will not start simultaneously. | 4343 |

> **Point**
> The "multiple axes simultaneous start control" carries out an operation equivalent to the "simultaneous start" using the "block start data".
> The setting of the "multiple axes simultaneous start control" is easier than that of the "simultaneous start" using the "block start data".
> - Setting items for "simultaneous start" using "block start data": Positioning start data, block start data, condition data, and positioning data
> - Setting items for "multiple axes simultaneous start control": Positioning data and axis control data

## 1.2 Stop (停止) (1.2 / original p.32-35)

The axis stop signal or stop signal from external input signal is used to stop the control.
Create a program to turn ON the axis stop signal [Cd.180] as the stop program.
Each control is stopped in the following cases.
- When each control is completed normally
- When the Servo READY signal is turned OFF
- When a CPU module error occurs
- When the "[Cd.190] PLC READY" is turned OFF
- When an error occurs in Simple Motion module/Motion module
- When control is intentionally stopped (Stop signal from CPU module turned ON.)

The stop process for the above cases is shown below.
(Excluding when each control is completed normally.)
Refer to the following for the stop process during speed control mode and torque control mode.
→Page 186 Speed-torque Control

### Stop process (停止処理) (1.2 / original p.32-33)

| Stop cause | | Stop axis | M code ON signal after stop | Axis operation status after stopping ([Md.26]) |
|---|---|---|---|---|
| Forced stop | Forced stop input to Simple Motion module/Motion module | All axes | No change | Servo OFF |
| Forced stop | Servo READY OFF<br>• Servo amplifier power supply OFF | Each axis | No change | Servo amplifier has not been connected |
| Forced stop | Servo READY OFF<br>• Servo alarm | Each axis | No change | Error |
| Forced stop | Servo READY OFF<br>• Forced stop input to servo amplifier | Each axis | No change | Servo OFF |
| Fatal stop (Stop group 1) | Hardware stroke limit upper/lower limit error occurrence | Each axis | No change | Error |
| Emergency stop (Stop group 2) | Error occurs in a CPU module | All axes | No change | Error |
| Emergency stop (Stop group 2) | "[Cd.190] PLC READY" OFF | All axes | Turns OFF | Error |
| Relatively safe stop (Stop group 3) | Axis error detection (Error other than stop group 1 or 2)*1 | Each axis | No change | Error |
| Intentional stop (Stop group 3) | "Axis stop signal" ON from a CPU module*2 | Each axis | No change | Stopped (Standby) |

*In the original, "Forced stop" is merged over 4 rows; the 3 "Servo READY OFF" rows are written as one cell "Servo READY OFF" with the bullets "Servo amplifier power supply OFF" / "Servo alarm" / "Forced stop input to servo amplifier" in separate rows (the "Servo READY OFF" heading is repeated in each row here); "Each axis" and "No change" are merged over those 3 rows. "Emergency stop (Stop group 2)" is merged over 2 rows, with "All axes" and "Error" also merged over the 2 rows. Expanded to each row.

*1 If an error occurs in a positioning data due to an invalid setting value, when the continuous positioning control uses multiple positioning data successively, it automatically decelerates at the previous positioning data. It does not stop rapidly even when the setting value is rapid stop in stop group 3. If any of the following error occurs, the operation is performed up to the positioning data immediately before the positioning data where an error occurred, and then stops immediately.
- No command speed (error code: 1A12H [FX5-SSC-S], or error codes: 1B12H to 1B14H [FX5-SSC-G])
- Outside linear movement amount range (error code: 1A15H [FX5-SSC-S], or error codes: 1B15H and 1B16H [FX5-SSC-G])
- Large arc error deviation (error code: 1A17H [FX5-SSC-S], or error code: 1B17H [FX5-SSC-G])
- Software stroke limit + (error code: 1A18H [FX5-SSC-S], or error codes: 1B18H and 1B19H [FX5-SSC-G])
- Software stroke limit - (error code: 1A1AH [FX5-SSC-S], or error codes: 1B1AH and 1B1BH [FX5-SSC-G])
- Sub point setting error (error code: 1A27H [FX5-SSC-S], or error codes: 1B27H to 1B2AH, and 1B37H [FX5-SSC-G])
- End point setting error (error code: 1A2BH [FX5-SSC-S], or error codes: 1B2BH and 1B2CH [FX5-SSC-G])
- Center point setting error (error code: 1A2DH [FX5-SSC-S], or error codes: 1B2DH to 1B2FH [FX5-SSC-G])
- Outside radius range (error code: 1A32H [FX5-SSC-S], or error code: 1B32H [FX5-SSC-G])
- Illegal setting of ABS direction in unit of degree (error code: 19A4H [FX5-SSC-S], or error codes: 1AA4H and 1AA5H [FX5-SSC-G])

*2 For the stop signal, it is recommended to perform control while checking the axis is BUSY condition, such as by using the BUSY signal being ON as an interlock. Depending on the timing, the occurrence of "Stop signal ON at start" (error code: 1908H [FX5-SSC-S], or error codes: 1A08H and 1A09H [FX5-SSC-G]) can be prevented.

Stop process by control (original p.33):

| Stop cause | | Machine home position return control*1 / Fast home position return control / Major positioning control / High-level positioning control / JOG/Inching operation | Manual pulse generator operation |
|---|---|---|---|
| Forced stop | Forced stop input to Simple Motion module/Motion module | Immediate stop. For the stop method of the servo amplifier, the manuals of each servo amplifier. | — |
| Forced stop | Servo READY OFF<br>• Servo amplifier power supply OFF | Immediate stop. For the stop method of the servo amplifier, the manuals of each servo amplifier. | — |
| Forced stop | Servo READY OFF<br>• Servo alarm | Immediate stop. For the stop method of the servo amplifier, the manuals of each servo amplifier. | — |
| Forced stop | Servo READY OFF<br>• Forced stop input to servo amplifier | Immediate stop. For the stop method of the servo amplifier, the manuals of each servo amplifier. | — |
| Fatal stop (Stop group 1) | Hardware stroke limit upper/lower limit error occurrence | Deceleration stop/rapid stop (Select with "[Pr.37] Stop group 1 sudden stop selection".) | Deceleration stop |
| Emergency stop (Stop group 2) | Error occurs in a CPU module | Deceleration stop/rapid stop (Select with "[Pr.38] Stop group 2 sudden stop selection".) | Deceleration stop |
| Emergency stop (Stop group 2) | "[Cd.190] PLC READY" OFF | Deceleration stop/rapid stop (Select with "[Pr.38] Stop group 2 sudden stop selection".) | Deceleration stop |
| Relatively safe stop (Stop group 3) | Axis error detection (Error other than stop group 1 or 2)*2 | Deceleration stop/rapid stop (Select with "[Pr.39] Stop group 3 sudden stop selection".) | Deceleration stop |
| Intentional stop (Stop group 3) | "Axis stop signal" ON from a CPU module*3 | Deceleration stop/rapid stop (Select with "[Pr.39] Stop group 3 sudden stop selection".) | Deceleration stop |

*In the original, the header is "Stop process" over "Home position return control (Machine home position return control*1 / Fast home position return control)", "Major positioning control", "High-level positioning control" and "Manual control (JOG/Inching operation / Manual pulse generator operation)". Each "Stop process" cell is merged horizontally over the 5 columns from Machine home position return control to JOG/Inching operation (written here as one column). Forced stop (4 rows): "Immediate stop ..." and "—" merged vertically. Stop group 2 (2 rows) and Stop group 3 (2 rows): merged vertically. Expanded to each row. The original reads "For the stop method of the servo amplifier, the manuals of each servo amplifier." as is.

*1 [FX5-SSC-G]
When using the driver homing method, the stop processing follows the specifications of the servo amplifier.
For details, refer to the manual of the servo amplifier to use.
When using MR-J5(W)-G: [Other manual] MR-J5 User's Manual (Function)

*2 If an error occurs in a positioning data due to an invalid setting value, when the continuous positioning control uses multiple positioning data successively, it automatically decelerates at the previous positioning data. It does not stop rapidly even when the setting value is rapid stop in stop group 3. If any of the following error occurs, the operation is performed up to the positioning data immediately before the positioning data where an error occurred, and then stops immediately.
- No command speed (error code: 1A12H [FX5-SSC-S], or error codes: 1B12H to 1B14H [FX5-SSC-G])
- Outside linear movement amount range (error code: 1A15H [FX5-SSC-S], or error codes: 1B15H and 1B16H [FX5-SSC-G])
- Large arc error deviation (error code: 1A17H [FX5-SSC-S], or error code: 1B17H [FX5-SSC-G])
- Software stroke limit + (error code: 1A18H [FX5-SSC-S], or error codes: 1B18H and 1B19H [FX5-SSC-G])
- Software stroke limit - (error code: 1A1AH [FX5-SSC-S], or error codes: 1B1AH and 1B1BH [FX5-SSC-G])
- Sub point setting error (error code: 1A27H [FX5-SSC-S], or error codes: 1B27H to 1B2AH, and 1B37H [FX5-SSC-G])
- End point setting error (error code: 1A2BH [FX5-SSC-S], or error codes: 1B2BH and 1B2CH [FX5-SSC-G])
- Center point setting error (error code: 1A2DH [FX5-SSC-S], or error codes: 1B2DH to 1B2FH [FX5-SSC-G])
- Outside radius range (error code: 1A32H [FX5-SSC-S], or error code: 1B32H [FX5-SSC-G])
- Illegal setting of ABS direction in unit of degree (error code: 19A4H [FX5-SSC-S], or error codes: 1AA4H and 1AA5H [FX5-SSC-G])

*3 For the stop signal, it is recommended to perform control while checking the axis is BUSY condition, such as by using the BUSY signal being ON as an interlock. Depending on the timing, the occurrence of "Stop signal ON at start" (error code: 1908H [FX5-SSC-S], or error codes: 1A08H and 1A09H [FX5-SSC-G]) can be prevented.

> **Point**
> Provide the emergency stop circuits outside the servo system to prevent cases where danger may result from abnormal operation of the overall system in the event of an external power supply fault or servo system failure.

### Types of stop processes (停止処理の種類) (1.2 / original p.34)

The operation can be stopped with deceleration stop, rapid stop or immediate stop.

#### Deceleration stop (減速停止) (1.2 / original p.34)

The operation stops with "deceleration time 0 to 3" ([Pr.10], [Pr.28], [Pr.29], [Pr.30]). Which time from "deceleration time 0 to 3" to use for control is set in positioning data ([Da.4]).

#### Rapid stop (急停止) (1.2 / original p.34)

The operation stops with "[Pr.36] Sudden stop deceleration time".

#### Immediate stop (即停止) (1.2 / original p.34)

The operation does not decelerate.
The Simple Motion module/Motion module immediately stops the command. For the stop method of the servo amplifier, refer to the manuals of each servo amplifier.

[Figure] Deceleration stop / Rapid stop / Immediate stop (original p.34)
- Deceleration stop: from the positioning speed, deceleration starts at the stop cause and reaches stop. "Set deceleration time" is the time to decelerate from "[Pr.8] Speed limit value" to 0; "Actual deceleration time" is from the stop cause to the stop (shorter, because the positioning speed is lower than [Pr.8]).
- Rapid stop: same shape with "Rapid stop cause"; "[Pr.36] Sudden stop deceleration time" is the time from [Pr.8] Speed limit value to 0; "Actual rapid stop deceleration time" is from the rapid stop cause to the stop.
- Immediate stop: the speed drops vertically from the positioning speed to 0 at the stop cause.

> **Point**
> "Deceleration stop" and "rapid stop" are selected with the detailed parameter 2 "stop group 1 to 3 rapid stop selection". (The default setting is "deceleration stop".)

### Order of priority for stop process (停止処理の優先順位) (1.2 / original p.35)

The order of priority for the Simple Motion module/Motion module stop process is as follows.
(Deceleration stop) < (Rapid stop) < (Immediate stop)
- If the deceleration stop command ON (stop signal ON) or deceleration stop cause occurs during deceleration to speed 0 (including automatic deceleration), operation changes depending on the setting of "[Cd.42] Stop command processing for deceleration stop selection". (→Page 281 Stop command processing for deceleration stop function)

| Positioning control during deceleration | Setting value of [Cd.42] | Processing details |
|---|---|---|
| Manual control | — | Independently of the [Cd.42] setting, a deceleration curve is re-processed from the speed at stop cause occurrence. |
| Home position return control*1, positioning control | 0: Deceleration curve re-processing | A deceleration curve is re-processed from the speed at stop cause occurrence. (→Page 281 Deceleration curve re-processing) |
| Home position return control*1, positioning control | 1: Deceleration curve continuation | The current deceleration curve is continued after stop cause occurrence. (→Page 281 Deceleration curve continuation) |

*In the original, "Home position return control*1, positioning control" is merged over 2 rows. Expanded to each row.

*1 [FX5-SSC-G]
When using the driver homing method, the stop processing follows the specifications of the servo amplifier.
For details, refer to the manual of the servo amplifier to use.
When using MR-J5(W)-G: [Other manual] MR-J5 User's Manual (Function)

- If the stop signal designated for rapid stop turns ON or a stop cause occurs during deceleration, the rapid stop process will start from that point. However, if the rapid stop deceleration time is longer than the deceleration time, the deceleration stop process will be continued even if a rapid stop cause occurs during the deceleration stop process.

Example
The process when a rapid stop cause occurs during deceleration stop is shown below.

[Figure] Rapid stop cause during deceleration stop (original p.35)
- (a) When deceleration stop time > rapid stop deceleration time: after the rapid stop cause, the slope becomes steeper ("Rapid stop deceleration process") and the axis stops earlier than the original deceleration line (dashed).
- (b) When deceleration stop time < rapid stop deceleration time: after the rapid stop cause, the original deceleration line is kept ("Deceleration stop process continues"); the "Process for rapid stop" (dashed, less steep) would stop later, so it is not used.

### Inputting the stop signal during deceleration (減速中の停止信号入力) (1.2 / original p.35)

- Even if stop is input during deceleration (including automatic deceleration), the operation will stop at that deceleration speed.
- If a stop cause, designated for rapid stop, occurs during deceleration, the rapid stop process will start from that point. The rapid stop process during deceleration is carried out only when the rapid stop time is shorter than the deceleration stop time.

[FX5-SSC-S]
- If stop is input during deceleration for home position return, the operation will stop at that deceleration speed. If input at the creep speed, the operation will stop immediately.

[FX5-SSC-G]
- If stop is input during deceleration for home position return, the operation will stop at that deceleration speed. When using the driver homing method, the stop processing follows the specifications of the servo amplifier. For details, refer to the manual of the servo amplifier to use.
  When using MR-J5(W)-G: [Other manual] MR-J5 User's Manual (Function)

## 1.3 Restart (再始動) (1.3 / original p.36-37)

When a stop factor occurs during position control and the operation stops, the positioning can be restarted from the stopped position to the position control end point by using the "restart command" ([Cd.6] Restart command). ("Restarting" is not possible when "continuous operation is interrupted.")
This instruction is efficient when performing the remaining positioning from the stopped position in the positioning control of incremental method such as INC linear 1. (Calculation of remaining distance is not required.)

### Operation (動作) (1.3 / original p.36)

After a deceleration stop by the stop command is completed, write "1: Restarts" to the "[Cd.6] Restart command" with "[Md.26] Axis operation status" is "stopped" and the positioning restarts.

[Figure] Restart operation (original p.36)
- Start → Positioning data No.10 → Positioning data No.11 → Positioning data No.12 (continuous).
- During Positioning data No.11, "Stop process with stop command" decelerates the axis to stop.
- "Positioning data No.11 continues with restart command": the axis restarts and completes the rest of No.11, then continues to No.12.

### Restrictions (制限事項) (1.3 / original p.36)

- Restarting can be executed only when the "[Md.26] Axis operation status" is "stopped (the deceleration stop by stop command is completed)". If the axis operation is not "stopped", restarting is not possible. In this case, the warning "Restart not possible" (warning code: 0902H [FX5-SSC-S], or warning code: 0D02H [FX5-SSC-G]) will occur, and the process at that time will be continued.
- Do not execute restart while the stop command is ON. If restart is executed while stopped, the error "Stop signal ON at start" (error code: 1908H [FX5-SSC-S], or error code: 1A08H [FX5-SSC-G]) will occur, and the "[Md.26] Axis operation status" will change to "Error". Thus, even if the error is reset, the operation cannot be restarted.
- Restarting can be executed even while the positioning start signal is ON. However, make sure that the positioning start signal does not change from OFF to ON while stopped.
- If the positioning start signal is changed from OFF to ON while "[Md.26] Axis operation status" is "stopped", the normal positioning (the positioning data set in "[Cd.3] Positioning start No.") is started.
- If positioning is ended with the continuous operation interrupt request, the operation cannot be restarted. If restart is requested, the warning "Restart not possible" (warning code: 0902H [FX5-SSC-S], or warning code: 0D02H [FX5-SSC-G]) will occur.
- When stopped with interpolation operation, write "1: Restarts" into "[Cd.6] Restart command" for the reference axis, and then restart.
- If the "[Cd.190] PLC READY" is changed from OFF to ON while stopped, restarting is not possible. If restart is requested, the warning "Restart not possible" (warning code: 0902H [FX5-SSC-S], or warning code: 0D02H [FX5-SSC-G]) will occur.
- When the machine home position return and fast home position return is stopped, the error "Home position return restart not possible" (error code: 1946H [FX5-SSC-S], or error code: 1A46H [FX5-SSC-G]) will occur and the positioning cannot restart.
- If any of reference partner axes executes the positioning operation once after interpolation operation stop, the warning "Restart not possible" (warning code: 0902H [FX5-SSC-S], or warning code: 0D02H [FX5-SSC-G]) will occur, and the positioning cannot restart.

### Setting method (設定方法) (1.3 / original p.37)

Set the following data to execute restart.
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.6] | Restart command | 1 | Set "1: Restarts". | 4303+100n |

Refer to the following for the setting details.
→Page 561 Control Data

### Time chart for restarting (再始動のタイムチャート) (1.3 / original p.37)

#### Operation example (動作例) (1.3 / original p.37)

[Figure] Time chart for restarting (original p.37)
- [Cd.190] PLC READY ON → READY signal ([Md.140] Module status: b0) ON; then [Cd.191] All axis servo ON ON.
- [Cd.184] Positioning start ON → Start complete signal ([Md.31] Status: b14) and [Md.141] BUSY turn ON; [Md.26] Axis operation status 0 → 8; positioning starts.
- [Cd.180] Axis stop ON during the positioning → deceleration stop; after the stop, [Md.141] BUSY turns OFF and [Md.26] changes 8 → 1 (stopped).
- [Cd.180] Axis stop and [Cd.184] Positioning start turn OFF; the start complete signal (b14) turns OFF following [Cd.184] OFF.
- [Cd.6] Restart command 0 → 1 while [Md.26] = 1 → [Md.141] BUSY turns ON, [Md.26] 1 → 8, and the remaining positioning is executed; [Cd.6] returns to 0.
- After the positioning and the dwell time, [Md.141] BUSY turns OFF, [Md.26] 8 → 0, and the positioning complete signal ([Md.31] Status: b15) turns ON, then OFF.
- Error detection signal ([Md.31] Status: b13) stays OFF.

### Program example (プログラム例) (1.3 / original p.37)

Refer to the following for the program example of restart.
→Page 637 Restart program [FX5-SSC-S]
→Page 715 Restart program [FX5-SSC-G]
