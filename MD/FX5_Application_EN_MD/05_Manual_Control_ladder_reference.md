# 5 MANUAL CONTROL (手動制御) (Chapter 5 / original p.159-187)

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

## Conversion range (変換範囲表 / original p.159-187)

| Original page | Section | Handling |
|---|---|---|
| p.159-160 | 5 MANUAL CONTROL (chapter intro) / 5.1 Outline of Manual Control | Full text |
| p.161-169 | 5.2 JOG Operation | Full text (program example is only a reference to Chapter 12/13; no body in this chapter) |
| p.170-177 | 5.3 Inching Operation | Full text (program example is only a reference to Chapter 12/13; no body in this chapter) |
| p.178-187 | 5.4 Manual Pulse Generator Operation | Full text (program example is only a reference to Chapter 12/13; no body in this chapter) |

## Table of Contents (目次)

- 5 MANUAL CONTROL (手動制御)
- 5.1 Outline of Manual Control (手動制御の概要)
- 5.2 JOG Operation (JOG運転)
- 5.3 Inching Operation (インチング運転)
- 5.4 Manual Pulse Generator Operation (手動パルサ運転)

---

## 5 MANUAL CONTROL (手動制御) (Chapter 5 / original p.159)

The details and usage of manual control are explained in this chapter.
In manual control, commands are issued during a JOG operation and an inching operation executed by the turning ON of the JOG start signal, or from a manual pulse generator connected to the Simple Motion module/Motion module.
Manual control using a program from the CPU module is explained in this chapter.

## 5.1 Outline of Manual Control (手動制御の概要) (5.1 / original p.159-160)

### Three manual control methods (3つの手動制御) (5.1 / original p.159-160)

"Manual control" refers to control in which positioning data is not used, and a positioning operation is carried out in response to signal input from an external device.
The three types of this "manual control" are explained below.

#### [JOG operation] ([JOG運転]) (5.1 / original p.159)

"JOG operation" is a control method in which the machine is moved by only a movement amount (commands are continuously output while the JOG start signal is ON). This operation is used to move the workpiece in the direction in which the limit signal is ON, when the operation is stopped by turning the limit signal OFF to confirm the positioning system connection and obtain the positioning data address (→Page 297 Teaching function).

[Figure] Concept of JOG operation (original p.159)
- A motor (M) drives a ball screw; the workpiece (table) moves to the right.
- JOG start signal: OFF→ON, held ON for a while, then ON→OFF.
- Label in figure: "Movement continues while the JOG start signal is ON."

#### [Inching operation] ([インチング運転]) (5.1 / original p.159)

"Inching operation" is a control method in which a minute movement amount of command is output manually in operation cycle. When the "inching movement amount" of the axis control data is set by JOG operation, the workpiece is moved by a set movement amount. (When the "inching movement amount" is set to "0", the machine operates as JOG operation.)

[Figure] Concept of inching operation (original p.159)
- A motor (M) drives a ball screw; the workpiece (table) moves to the right.
- JOG start signal: OFF→ON→OFF (short ON).
- Label in figure: "JOG start signal is turned ON to move the workpiece by the movement amount of pulses which is output in operation cycle."

#### [Manual pulse generator operation] ([手動パルサ運転]) (5.1 / original p.160)

"Manual pulse generator operation" is a control method in which positioning is carried out in response to the number of pulses input from a manual pulse generator (the number of input command is output). This operation is used for manual fine adjustment, etc., when carrying out accurate positioning to obtain the positioning address.

[FX5-SSC-S]

[Figure] Configuration of manual pulse generator operation [FX5-SSC-S] (original p.160)
- Manual pulse generator →(Pulse input)→ Simple Motion module →(Command output, pulse train)→ motor (M) driving a ball screw.
- Label in figure: "Movement in response to the command pulses" (workpiece moves to the right).

[FX5-SSC-G]

[Figure] Configuration of manual pulse generator operation [FX5-SSC-G] (original p.160)
- Manual pulse generator →(Pulse input)→ CPU module → Motion module →(Command output, pulse train)→ motor (M) driving a ball screw.
- Label in figure: "Movement in response to the command pulses" (workpiece moves to the right).

##### Manual control sub functions (手動制御の補助機能) (5.1 / original p.160)

Refer to the "Combination of Main Functions and Sub Functions" in the following manual for details on "sub functions" that can be combined with manual control.
[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Startup)
Also refer to the following for details on each sub function.
→Page 218 CONTROL SUB FUNCTIONS

##### Monitoring manual control (手動制御のモニタ) (5.1 / original p.160)

Refer to the following for directly monitoring the buffer memory using an engineering tool.
→Page 518 Monitor Data
Also refer to "Help" in the "Simple Motion Module Setting Function" when monitoring with the monitor functions of an engineering tool.

## 5.2 JOG Operation (JOG運転) (5.2 / original p.161-169)

### Outline of JOG operation (JOG運転の動作概要) (5.2 / original p.161-163)

#### Operation (動作) (5.2 / original p.161)

In JOG operation, the forward run JOG start signal [Cd.181] or reverse run JOG start signal [Cd.182] turns ON, causing pulses to be output to the servo amplifier from the Simple Motion module/Motion module while the signal is ON. The workpiece is then moved in the designated direction.
The following shows examples of JOG operation.

##### Operation example (動作例) (5.2 / original p.161)

1. When the start signal turns ON, acceleration begins in the direction designated by the start signal, and continues for the acceleration time designated in "[Pr.32] JOG operation acceleration time selection". At this time, the BUSY signal changes from OFF to ON.
2. When the workpiece being accelerated reaches the speed set in "[Cd.17] JOG speed", the movement continues at this speed. The constant speed movement takes place at 2. and 3.
3. When the start signal is turned OFF, deceleration begins from the speed set in "[Cd.17] JOG speed", and continues for the deceleration time designated in "[Pr.33] JOG operation deceleration time selection".
4. The operation stops when the speed becomes "0". At this time, the BUSY signal changes from ON to OFF.

[Figure] JOG operation example (original p.161)
- Speed waveform: at 1. forward acceleration starts ("Acceleration for the acceleration time selected in [Pr.32]") → at 2. reaches "[Cd.17] JOG speed" and runs at constant speed (Forward JOG run) → at 3. deceleration starts ("Deceleration for the deceleration time selected in [Pr.33]") → at 4. stops. After that, "Reverse JOG run" (negative direction: acceleration → constant speed → deceleration → stop).
- [Cd.190] PLC READY: OFF→ON first, then stays ON.
- [Cd.191] All axis servo ON: OFF→ON, then stays ON.
- READY signal ([Md.140] Module status: b0): OFF→ON, then stays ON.
- [Cd.181] Forward run JOG start: OFF→ON at 1., ON→OFF at 3.
- [Cd.182] Reverse run JOG start: OFF→ON after 4., ON→OFF at the start of the reverse run deceleration.
- [Md.141] BUSY: OFF→ON at 1., ON→OFF at 4.; OFF→ON again when [Cd.182] turns ON, ON→OFF when the reverse JOG run stops.

> **Restriction**
> Use the hardware stroke limit function when carrying out JOG operation near the upper or lower limits. (→Page 250 Hardware stroke limit function)
> If the hardware stroke limit function is not used, the workpiece may exceed the moving range, causing an accident.

#### Precautions during operation (動作上の注意) (5.2 / original p.162)

The following details must be understood before carrying out JOG operation.
- For safety, set a small value to "[Cd.17] JOG speed" at first and check the movement. Then gradually increase the value.
- The error "Outside JOG speed range" (error code: 1980H [FX5-SSC-S], or error code 1A80H [FX5-SSC-G]) will occur and the operation will not start if the "JOG speed" is outside the setting range at the JOG start.
- The error "JOG speed limit value error" (error code: 1AB7H [FX5-SSC-S], or error codes 1BB7H and 1BB8H [FX5-SSC-G]) will occur and the operation will not start if "[Pr.31] JOG speed limit value" is set to a value larger than "[Pr.8] Speed limit value".
- If "[Cd.17] JOG speed" exceeds the speed set in "[Pr.31] JOG speed limit value", the workpiece will move at the "[Pr.31] JOG speed limit value" and the warning "JOG speed limit value" (warning code: 0981H [FX5-SSC-S], or warning codes 0D41H and 0D42H [FX5-SSC-G]) will occur in the Simple Motion module/Motion module.
- The JOG operation can be continued even if an "Axis warning" has occurred.
- Set a "0" in "[Cd.16] Inching movement amount". If a value other than "0" is set, the operation will become an inching operation. (→Page 168 Inching Operation)

#### Operations when stroke limit error occurs (ストロークリミットエラー発生時の動作について) (5.2 / original p.162)

When the operation is stopped by hardware stroke limit error or software stroke limit error, the JOG operation can execute in an opposite way (direction within normal limits) after an error reset. (An error will occur again if JOG start signal is turned ON in a direction to outside the stroke limit.)

[Figure] JOG operation at stroke limit error (original p.162)
- Vertical axis V: "JOG operation" at constant speed; when the upper/lower limit signal turns ON→OFF, the speed decelerates to 0 and stops.
- Upper/lower limit signal: ON→OFF.
- Side before the limit signal OFF point (within range): "JOG operation possible"; side beyond the stop position (outside range): "JOG operation not possible".

#### Operation timing and processing time (動作タイミングと処理時間) (5.2 / original p.163)

The following drawing shows details of the JOG operation timing and processing time.

##### Operation example (動作例) (5.2 / original p.163)

[Figure] JOG operation timing (original p.163)
- [Cd.181] Forward run JOG start: OFF→ON→OFF.
- [Cd.182] Reverse run JOG start: stays OFF.
- [Md.141] BUSY: OFF→ON t1 after [Cd.181] turns ON; ON→OFF t4 after the positioning operation ends.
- [Md.26] Axis operation status: Standby (0) → JOG operation (3) (at BUSY ON) → Standby (0) (at BUSY OFF).
- Positioning operation: acceleration starts t3 after BUSY ON → constant speed → deceleration starts t2 after [Cd.181] turns OFF → stop.
- Positioning complete signal ([Md.31] Status: b15): shown dashed (if ON) before BUSY ON, OFF from BUSY ON, then stays OFF.

- Normal timing time (Unit: [ms])

| Model | Operation cycle | t1*1 | t2 | t3*2 | t4 |
|---|---|---|---|---|---|
| FX5-SSC-S | 0.888 | 0.1 to 1.1 | 0 to 0.9 | 3.78 to 4.45 | 0 to 0.9 |
| FX5-SSC-S | 1.777 | 0.1 to 2.1 | 0 to 1.8 | 5.58 to 7.13 | 0 to 1.8 |
| FX5-SSC-G | 0.500 | 0.4 to 1.0 | 0 to 0.5 | 1.8 to 2.0 | 0 to 0.5 |
| FX5-SSC-G | 1.000 | 0.4 to 1.5 | 0 to 1.0 | 3.4 to 3.8 | 0 to 1.0 |
| FX5-SSC-G | 2.000 | 0.4 to 2.8 | 0 to 2.0 | 6.4 to 6.6 | 0 to 2.0 |
| FX5-SSC-G | 4.000 | 0.4 to 4.5 | 0 to 4.0 | 12.0 to 12.5 | 0 to 4.0 |

*In the original, "Operation cycle" is one header spanning the model and cycle columns; the model cell is merged (FX5-SSC-S over 2 rows, FX5-SSC-G over 4 rows). Expanded to each row.

*1 Delays may occur in the t1 timing time due to the operation status of other axes.
*2 The t3 timing time depends on the setting of the acceleration time, servo parameter, etc.

### JOG operation execution procedure (JOG運転の実行手順) (5.2 / original p.164)

The JOG operation is carried out by the following procedure.

[Figure] JOG operation execution procedure flow (original p.164)
- Preparation
  - STEP 1: Set the parameters. ([Pr.1] to [Pr.39])
    - Note in figure: One of the following two methods can be used. <Method 1> Directly set (write) the parameters in the Simple Motion module/Motion module using the engineering tool. <Method 2> Set (write) the parameters from the CPU module to the Simple Motion module/Motion module using the program.
  - STEP 2: Create a program for the following setting. Set a "0" in "[Cd.16] Inching movement amount". Set the "[Cd.17] JOG speed". (Control data setting) / Create a program in which the "JOG start signal" is turned ON by a JOG operation start command.
  - STEP 3: Write the program created in STEP1 and STEP2 to the CPU module.
- JOG operation start
  - STEP 4: Turn ON the JOG start signal of the axis to be started.
    - Note in figure: Turn ON the JOG start signal. [Cd.181] Forward run JOG start / [Cd.182] Reverse run JOG start
- Monitoring of the JOG operation
  - STEP 5: Monitor the JOG operation status.
    - Note in figure: Monitor using the engineering tool.
- JOG operation stop
  - STEP 6: Turn OFF the JOG start signal that is ON.
    - Note in figure: Stop the JOG operation when the JOG start signal is turned OFF using the program in STEP 2.
- End of control

> **Point**
> - Mechanical elements such as limit switches are considered as already installed.
> - Parameter settings work in common for all control using the Simple Motion module/Motion module.

### Setting the required parameters for JOG operation (JOG運転に必要なパラメータの設定) (5.2 / original p.165)

The "Positioning parameters" must be set to carry out JOG operation.
The following table shows the setting items of the required parameters for carrying out JOG operation. Parameters not shown below are not required to be set for carrying out only JOG operation. (Set the initial values or a value within the setting range.)
◎: Setting always required.
○: Set according to requirements (Set the initial value or a value within the setting range when not used.)

| Setting item (category) | No. | Setting item | Setting requirement |
|---|---|---|---|
| Positioning parameters | [Pr.1] | Unit setting | ◎ |
| Positioning parameters | [Pr.2] | Number of pulses per rotation (AP) (Unit: pulse) | ◎ |
| Positioning parameters | [Pr.3] | Movement amount per rotation (AL) (Unit: pulse) | ◎ |
| Positioning parameters | [Pr.4] | Unit magnification (AM) | ◎ |
| Positioning parameters | [Pr.7] | Bias speed at start (Unit: pulse/s) | ○ |
| Positioning parameters | [Pr.8] | Speed limit value (Unit: pulse/s) | ◎ |
| Positioning parameters | [Pr.9] | Acceleration time 0 (Unit: ms) | ◎ |
| Positioning parameters | [Pr.10] | Deceleration time 0 (Unit: ms) | ◎ |
| Positioning parameters | [Pr.11] | Backlash compensation amount (Unit: pulse) | ○ |
| Positioning parameters | [Pr.12] | Software stroke limit upper limit value (Unit: pulse) | ○ |
| Positioning parameters | [Pr.13] | Software stroke limit lower limit value (Unit: pulse) | ○ |
| Positioning parameters | [Pr.14] | Software stroke limit selection | ○ |
| Positioning parameters | [Pr.15] | Software stroke limit valid/invalid setting | ○ |
| Positioning parameters | [Pr.17] | Torque limit setting value (Unit: 0.1%) | ○ |
| Positioning parameters | [Pr.25] | Acceleration time 1 (Unit: ms) | ○ |
| Positioning parameters | [Pr.26] | Acceleration time 2 (Unit: ms) | ○ |
| Positioning parameters | [Pr.27] | Acceleration time 3 (Unit: ms) | ○ |
| Positioning parameters | [Pr.28] | Deceleration time 1 (Unit: ms) | ○ |
| Positioning parameters | [Pr.29] | Deceleration time 2 (Unit: ms) | ○ |
| Positioning parameters | [Pr.30] | Deceleration time 3 (Unit: ms) | ○ |
| Positioning parameters | [Pr.31] | JOG speed limit value (Unit: pulse/s) | ◎ |
| Positioning parameters | [Pr.32] | JOG operation acceleration time selection | ◎ |
| Positioning parameters | [Pr.33] | JOG operation deceleration time selection | ◎ |
| Positioning parameters | [Pr.34] | Acceleration/deceleration process selection | ○ |
| Positioning parameters | [Pr.35] | S-curve ratio (Unit: %) | ○ |
| Positioning parameters | [Pr.36] | Sudden stop deceleration time (Unit: ms) | ○ |
| Positioning parameters | [Pr.37] | Stop group 1 sudden stop selection | ○ |
| Positioning parameters | [Pr.38] | Stop group 2 sudden stop selection | ○ |
| Positioning parameters | [Pr.39] | Stop group 3 sudden stop selection | ○ |

*In the original, the "Setting item" header spans 3 columns, and "Positioning parameters" is merged over all 29 rows. Expanded to each row.

Refer to the following for the setting details.
→Page 444 Basic Setting

> **Point**
> - Parameter settings work in common for all controls using the Simple Motion module/Motion module. When carrying out other controls ("major positioning control", "high-level positioning control", "home position return positioning control"), set the respective setting items as well.
> - Parameters are set for each axis.

### Creating start programs for JOG operation (JOG運転の始動プログラムの作成) (5.2 / original p.166-167)

A program must be created to execute a JOG operation. Consider the "required control data setting", "start conditions" and "start time chart" when creating the program.
The following shows an example when a JOG operation is started for axis 1. ("[Cd.17] JOG speed" is set to "100.00 mm/min" in the example shown.)

#### Required control data setting (設定の必要な制御データ) (5.2 / original p.166)

The control data shown below must be set to execute a JOG operation. The setting is carried out with the program.
n: Axis No. - 1

| No. | Setting item | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.16] | Inching movement amount | 0 | Set "0". | 4317+100n |
| [Cd.17] | JOG speed | 10000 | Set a value equal to or below the "[Pr.31] JOG speed limit value". | 4318+100n<br>4319+100n |

*In the original, the "Setting item" header spans 2 columns (No. and name).

Refer to the following for the setting details.
→Page 561 Control Data

#### Start conditions (始動条件) (5.2 / original p.166)

The following conditions must be fulfilled when starting. The required conditions must also be assembled in the program, and the program must be configured so the operation will not start if the conditions are not fulfilled.

| Signal name (category) | Signal name | Signal state | Signal state (details) | Device |
|---|---|---|---|---|
| Interface signal | PLC READY signal | ON | CPU module preparation completed | [Cd.190] PLC READY |
| Interface signal | READY signal | ON | Preparation completed | [Md.140] Module status: b0 |
| Interface signal | All axis servo ON | ON | All axis servo ON | [Cd.191] All axis servo ON |
| Interface signal | Synchronization flag*1 | ON | The buffer memory can be accessed. | [Md.140] Module status: b1 |
| Interface signal | Axis stop signal | OFF | Axis stop signal is OFF | [Cd.180] Axis stop |
| Interface signal | Start complete signal | OFF | Start complete signal is OFF | [Md.31] Status: b14 |
| Interface signal | BUSY signal | OFF | Not in operation | [Md.141] BUSY |
| Interface signal | Error detection signal | OFF | There is no error | [Md.31] Status: b13 |
| Interface signal | M code ON signal | OFF | M code ON signal is OFF | [Md.31] Status: b12 |
| External signal | Forced stop input signal | ON | There is no forced stop input | — |
| External signal | Stop signal | OFF | Stop signal is OFF | — |
| External signal | Upper limit (FLS) | ON | Within limit range | — |
| External signal | Lower limit (RLS) | ON | Within limit range | — |

*In the original, the "Signal name" and "Signal state" headers each span 2 columns; "Interface signal" is merged over 9 rows and "External signal" over 4 rows. Expanded to each row.

*1 When the CPU module is set to the asynchronous mode in the synchronization setting, the synchronization flag must be inserted in the program as an interlock condition. When it is set to the synchronous mode, the synchronization flag is turned ON when the CPU module executes calculation. Therefore, the interlock condition is not required to be inserted in the program.

#### Start time chart (始動用タイムチャート) (5.2 / original p.167)

##### Operation example (動作例) (5.2 / original p.167)

[Figure] JOG operation start time chart (original p.167)
- Speed waveform (horizontal axis t): "Forward JOG run" (positive trapezoid) → stop → "Reverse JOG run" (negative trapezoid).
- [Cd.190] PLC READY: OFF→ON first.
- [Cd.191] All axis servo ON: OFF→ON after PLC READY ON.
- READY signal ([Md.140] Module status: b0): OFF→ON in response to PLC READY ON (arrow from [Cd.190]).
- [Cd.181] Forward run JOG start: OFF→ON (arrow → BUSY ON, forward JOG run starts); ON→OFF at the deceleration start point.
- [Md.141] BUSY: OFF→ON in response to [Cd.181] ON; ON→OFF when the forward JOG run stops. OFF→ON again in response to [Cd.182] ON; ON→OFF when the reverse JOG run stops.
- [Cd.182] Reverse run JOG start: OFF→ON after the forward run stops (arrow → BUSY ON, reverse JOG run starts); ON→OFF at the deceleration start point.
- Error detection signal ([Md.31] Status: b13): stays OFF.

#### Program example (プログラム例) (5.2 / original p.167)

Refer to the following for the program example of the JOG operation.
→Page 633 JOG operation setting program [FX5-SSC-S]
→Page 706 JOG operation setting program [FX5-SSC-G]
→Page 634 JOG operation/inching operation execution program [FX5-SSC-S]
→Page 707 JOG operation/inching operation execution program [FX5-SSC-G]

(There is no program example (ladder) body in this chapter; it is in the Chapter 12/13 conversion.)

### JOG operation example (JOG運転の動作例) (5.2 / original p.168-169)

#### Example 1 (例1) (5.2 / original p.168)

When the stop signal is turned ON during JOG operation, the JOG operation will stop by the deceleration stop method.
If the JOG start signal is turned ON while the stop signal is ON, the error "Stop signal ON at start" (error code: 1908H [FX5-SSC-S], or error code 1A08H [FX5-SSC-G]) will occur.
The inching operation can be re-started when the stop signal is turned OFF and the JOG start signal is turned ON from OFF.

##### Operation example (動作例) (5.2 / original p.168)

[Figure] Example 1: stop signal ON during JOG operation (original p.168)
- [Cd.190] PLC READY → [Cd.191] All axis servo ON → READY signal ([Md.140] Module status: b0) turn OFF→ON in this order (arrow from PLC READY to READY signal).
- [Cd.181] Forward run JOG start OFF→ON → [Md.141] BUSY OFF→ON; acceleration → constant speed.
- [Cd.180] Axis stop OFF→ON → deceleration starts → after stop, BUSY ON→OFF ([Cd.181] still ON).
- [Cd.181] then turns ON→OFF and OFF→ON again while [Cd.180] is still ON → label in figure: "Ignores that the JOG start signal is turned ON from OFF while the stop signal is ON." (BUSY stays OFF, speed stays 0).
- [Cd.180] Axis stop ON→OFF, then [Cd.181] ON→OFF.
- [Cd.181] OFF→ON again → BUSY OFF→ON, acceleration → constant speed → [Cd.181] ON→OFF → deceleration → stop → BUSY ON→OFF.

#### Example 2 (例2) (5.2 / original p.169)

When both the forward run JOG start signal and the reverse run JOG start signal are turned ON simultaneously for one axis, the forward run JOG start signal is given priority. In this case, the reverse run JOG start signal is validated when the BUSY signal of Simple Motion module/Motion module is turned OFF. If the forward run JOG operation is stopped due to stop by a stop signal or axis error, the reverse run JOG operation will not be executed even if the reverse run JOG start signal turns ON.

##### Operation example (動作例) (5.2 / original p.169)

[Figure] Example 2: forward and reverse JOG start ON simultaneously (original p.169)
- [Cd.181] Forward run JOG start and [Cd.182] Reverse run JOG start turn OFF→ON at the same time.
- "Forward run JOG operation" (positive trapezoid) is executed; [Md.141] BUSY OFF→ON.
- [Cd.181] ON→OFF → deceleration stop → BUSY ON→OFF (briefly).
- Label in figure: "The reverse run JOG start signal is ignored." (period from the simultaneous ON until BUSY OFF).
- After BUSY OFF, BUSY turns OFF→ON again and "Reverse run JOG operation" (negative trapezoid) is executed.
- [Cd.182] ON→OFF → deceleration stop → BUSY ON→OFF.

#### Example 3 (例3) (5.2 / original p.169)

When the JOG start signal is turned ON again during deceleration caused by the ON → OFF of the JOG start signal, the JOG operation will be carried out from the time the JOG start signal is turned ON.

##### Operation example (動作例) (5.2 / original p.169)

[Figure] Example 3: JOG start turned ON again during deceleration (original p.169)
- [Cd.181] Forward run JOG start: OFF→ON → (short) OFF → ON → OFF.
- Speed waveform ("Forward run JOG operation"): acceleration → constant speed → deceleration starts at [Cd.181] OFF → during the deceleration (dash-dot line shows the deceleration that would continue without re-ON) [Cd.181] turns ON again and the speed re-accelerates from that point → constant speed → [Cd.181] OFF → deceleration stop.
- [Md.141] BUSY: OFF→ON at the first [Cd.181] ON, stays ON until the final stop, then ON→OFF.

## 5.3 Inching Operation (インチング運転) (5.3 / original p.170-177)

### Outline of inching operation (インチング運転の動作概要) (5.3 / original p.170-172)

#### Operation (動作) (5.3 / original p.170)

In inching operation, pulses are output to the servo amplifier at operation cycle to move the workpiece by a designated movement amount after the forward run JOG start signal [Cd.181] or reverse JOG start signal [Cd.182] is turned ON.
The following shows the example of inching operation.

1. When the start signal is turned ON, inching operation is carried out in the direction designated by the start signal. In this case, BUSY signal is turned from OFF to ON.
2. The workpiece is moved by a movement amount set in "[Cd.16] Inching movement amount".
3. The workpiece movement stops when the speed becomes "0". In this case, BUSY signal is turned from ON to OFF. The positioning complete signal is turned from OFF to ON.
4. The positioning complete signal is turned from ON to OFF after a time set in "[Pr.40] Positioning complete signal output time" has been elapsed.

##### Operation example (動作例) (5.3 / original p.170)

[Figure] Inching operation example (original p.170)
- Speed waveform: a rectangular pulse between 1. and 3. ("Forward run inching operation"); 2. is during the movement.
- [Cd.190] PLC READY / [Cd.191] All axis servo ON / READY signal ([Md.140] Module status: b0): OFF→ON first, then stay ON.
- [Cd.181] Forward run JOG start: OFF→ON at 1., ON→OFF between 3. and 4.
- [Md.141] BUSY: OFF→ON at 1., ON→OFF at 3.
- Positioning complete signal ([Md.31] Status: b15): OFF→ON at 3., ON→OFF at 4. (3. to 4. = "[Pr.40] Positioning complete signal output time").

> **Restriction**
> When the inching operation is carried out near the upper or lower limit, use the hardware stroke limit function. (→Page 250 Hardware stroke limit function)
> If the hardware stroke limit function is not used, the workpiece may exceed the movement range, and an accident may result.

#### Precautions during operation (動作上の注意) (5.3 / original p.171)

The following details must be understood before inching operation is carried out.
- Acceleration/deceleration processing is not carried out during inching operation.

(Commands corresponding to the designated inching movement amount are output at operation cycle. When the movement direction of inching operation is reversed and backlash compensation is carried out, the backlash compensation amount and inching movement amount are output at the same operation cycle.)
The "[Cd.17] JOG speed" is ignored even if it is set. The error "Inching movement amount error" (error code: 1981H [FX5-SSC-S], or error code 1A81H [FX5-SSC-G]) will occur in the following case.
([Cd.16] Inching movement amount) × (A) > ([Pr.31] JOG speed limit value)
However, (A) is as follows.

[FX5-SSC-S]

| Unit setting | Operation cycle 0.888 ms | Operation cycle 1.777 ms |
|---|---|---|
| When the unit setting is pulse | 1125 | 562.5 |
| When the unit setting is degree and the "[Pr.83] Speed control 10 × multiplier setting for degree axis" is valid | 67.5 | 33.75 |
| When the unit setting is other than the above | 675 | 337.5 |

*In the original, the "Operation cycle" header spans 2 columns (0.888 ms / 1.777 ms in the lower header row) and "Unit setting" spans 2 header rows. Expanded into column headers.

[FX5-SSC-G]

| Unit setting | Operation cycle 0.50 ms | Operation cycle 1.00 ms | Operation cycle 2.00 ms | Operation cycle 4.00 ms |
|---|---|---|---|---|
| When the unit setting is pulse | 2000 | 1000 | 500 | 250 |
| When the unit setting is degree and the "[Pr.83] Speed control 10 × multiplier setting for degree axis" is valid | 120 | 60 | 30 | 15 |
| When the unit setting is other than the above | 1200 | 600 | 300 | 150 |

*In the original, the "Operation cycle" header spans 4 columns (0.50 ms to 4.00 ms in the lower header row) and "Unit setting" spans 2 header rows. Expanded into column headers.

- Set a value other than a "0" in "[Cd.16] Inching movement amount".

If a "0" is set, the operation will become JOG operation. (→Page 159 JOG Operation)

#### Operations when stroke limit error occurs (ストロークリミットエラー発生時の動作について) (5.3 / original p.171)

When the operation is stopped by hardware stroke limit error or software stroke limit error, the inching operation can be performed in an opposite way (direction within normal limits) after an error reset. (An error will occur again if JOG start signal is turned ON in a direction to outside the stroke limit.)

[Figure] Inching operation at stroke limit error (original p.171)
- Vertical axis V: "Inching operation" speed drops to 0 (vertical edge, no deceleration slope) shortly after the upper/lower limit signal turns ON→OFF, and stops.
- Upper/lower limit signal: ON→OFF.
- Within-range side: "Inching operation possible"; outside-range side: "Inching operation not possible".

#### Operation timing and processing times (動作タイミングと処理時間) (5.3 / original p.172)

The following drawing shows the details of the inching operation timing and processing time.

##### Operation example (動作例) (5.3 / original p.172)

[Figure] Inching operation timing (original p.172)
- [Cd.181] Forward run JOG start: OFF→ON → (some time after the positioning complete signal turns ON) ON→OFF.
- [Cd.182] Reverse run JOG start: stays OFF.
- [Md.141] BUSY: OFF→ON t1 after [Cd.181] ON; ON→OFF t3 after the positioning operation ends.
- [Md.26] Axis operation status: Standby (0) → JOG operation (3)*1 (at BUSY ON) → Standby (0) (at BUSY OFF).
- [Cd.16] Inching movement amount: Arbitrary value.
- Positioning operation: rectangular output starts t2 after BUSY ON → ends.
- Positioning complete signal ([Md.31] Status: b15): OFF→ON at the same time as BUSY OFF; ON→OFF t4 later.

*1 "JOG operation" is set in "[Md.26] Axis operation status" even during inching operation.

- Normal timing time (Unit: [ms])

| Model | Operation cycle | t1*1 | t2*2 | t3 | t4 |
|---|---|---|---|---|---|
| FX5-SSC-S | 0.888 | 0.1 to 1.4 | 3.57 to 4.45 | 0 to 0.9 | Follows parameters |
| FX5-SSC-S | 1.777 | 0.1 to 2.1 | 5.96 to 7.11 | 0 to 1.8 | Follows parameters |
| FX5-SSC-G | 0.500 | 0.4 to 1.0 | 1.8 to 2.2 | 0 to 0.5 | Follows parameters |
| FX5-SSC-G | 1.000 | 0.4 to 1.5 | 3.3 to 3.5 | 0 to 1.0 | Follows parameters |
| FX5-SSC-G | 2.000 | 0.4 to 2.8 | 6.2 to 6.4 | 0 to 2.0 | Follows parameters |
| FX5-SSC-G | 4.000 | 0.4 to 4.5 | 12.5 to 13.0 | 0 to 4.0 | Follows parameters |

*In the original, "Operation cycle" is one header spanning the model and cycle columns; the model cell is merged (FX5-SSC-S over 2 rows, FX5-SSC-G over 4 rows). Expanded to each row.

*1 Depending on the operating statuses of the other axes, delay may occur in the t1 timing time.
*2 The t2 timing time depends on the setting of the acceleration time, servo parameter, etc.

### Inching operation execution procedure (インチング運転の実行手順) (5.3 / original p.173)

The inching operation is carried out by the following procedure.

[Figure] Inching operation execution procedure flow (original p.173)
- Preparation
  - STEP 1: Set the parameters. ([Pr.1] to [Pr.31])
    - Note in figure: One of the following two methods can be used. <Method 1> Directly set (write) the parameters in the Simple Motion module/Motion module using the engineering tool. <Method 2> Set (write) the parameters from the CPU module to the Simple Motion module/Motion module using the program.
  - STEP 2: Create a program in which the "[Cd.16] Inching movement amount" is set. (Control data setting) / Create a program in which the "JOG start signal" is turned ON by an inching operation start command.
  - STEP 3: Write the program created in STEP1 and STEP2 to the CPU module.
- Inching operation start
  - STEP 4: Turn ON the JOG start signal of the axis to be started.
    - Note in figure: Turn ON the JOG start signal. [Cd.181] Forward run JOG start / [Cd.182] Reverse run JOG start
- Monitoring of the inching operation
  - STEP 5: Monitor the inching operation status.
    - Note in figure: Monitor using the engineering tool.
- Inching operation stop
  - STEP 6: Turn OFF the JOG start signal that is ON.
    - Note in figure: End the inching operation after moving a workpiece by an inching movement amount with the program created in STEP 2.
- End of control

> **Point**
> - Mechanical elements such as limit switches are considered as already installed.
> - Parameter settings work in common for all control using the Simple Motion module/Motion module.

### Setting the required parameters for inching operation (インチング運転に必要なパラメータの設定) (5.3 / original p.174)

The "Positioning parameters" must be set to carry out inching operation.
The following table shows the setting items of the required parameters for carrying out inching operation. Parameters not shown below are not required to be set for carrying out only inching operation. (Set the initial values or a value within the setting range.)
◎: Setting always required.
○: Set according to requirements (Set the initial value or a value within the setting range when not used.)

| Setting item (category) | No. | Setting item | Setting requirement |
|---|---|---|---|
| Positioning parameters | [Pr.1] | Unit setting | ◎ |
| Positioning parameters | [Pr.2] | Number of pulses per rotation (AP) (Unit: pulse) | ◎ |
| Positioning parameters | [Pr.3] | Movement amount per rotation (AL) (Unit: pulse) | ◎ |
| Positioning parameters | [Pr.4] | Unit magnification (AM) | ◎ |
| Positioning parameters | [Pr.11] | Backlash compensation amount (Unit: pulse) | ○ |
| Positioning parameters | [Pr.12] | Software stroke limit upper limit value (Unit: pulse) | ○ |
| Positioning parameters | [Pr.13] | Software stroke limit lower limit value (Unit: pulse) | ○ |
| Positioning parameters | [Pr.14] | Software stroke limit selection | ○ |
| Positioning parameters | [Pr.15] | Software stroke limit valid/invalid setting | ○ |
| Positioning parameters | [Pr.17] | Torque limit setting value (Unit: 0.1%) | ○ |
| Positioning parameters | [Pr.31] | JOG speed limit value (Unit: pulse/s) | ◎ |

*In the original, the "Setting item" header spans 3 columns, and "Positioning parameters" is merged over all 11 rows. Expanded to each row.

Refer to the following for the setting details.
→Page 444 Basic Setting

> **Point**
> - Positioning parameter settings work in common for all controls using the Simple Motion module/Motion module. When carrying out other controls ("major positioning control", "high-level positioning control", and "home position return control"), set the respective setting items as well.
> - Parameters are set for each axis.

### Creating a program to start the inching operation (インチング運転の始動プログラムの作成) (5.3 / original p.175-176)

A program must be created to execute an inching operation. Consider the "required control data setting", "start conditions", and "start time chart" when creating the program.
The following shows an example when an inching operation is started for axis 1. (The example shows the inching operation when a "10.0 μm" is set in "[Cd.16] Inching movement amount".)

#### Required control data setting (設定の必要な制御データ) (5.3 / original p.175)

The control data shown below must be set to execute an inching operation. The setting is carried out with the program.
n: Axis No. - 1

| No. | Setting item | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.16] | Inching movement amount | 100 | Set the setting value so that the JOG speed limit value is not increased larger than the maximum output pulse | 4317+100n |

*In the original, the "Setting item" header spans 2 columns (No. and name).

Refer to the following for the setting details.
→Page 561 Control Data

#### Start conditions (始動条件) (5.3 / original p.175)

The following conditions must be fulfilled when starting. The required conditions must also be assembled in the program, and the program must be configured so the operation will not start if the conditions are not fulfilled.

| Signal name (category) | Signal name | Signal state | Signal state (details) | Device |
|---|---|---|---|---|
| Interface signal | PLC READY signal | ON | CPU module preparation completed | [Cd.190] PLC READY |
| Interface signal | READY signal | ON | Preparation completed | [Md.140] Module status: b0 |
| Interface signal | All axis servo ON | ON | All axis servo ON | [Cd.191] All axis servo ON |
| Interface signal | Synchronization flag*1 | ON | The buffer memory can be accessed. | [Md.140] Module status: b1 |
| Interface signal | Axis stop signal | OFF | Axis stop signal is OFF | [Cd.180] Axis stop |
| Interface signal | Start complete signal | OFF | Start complete signal is OFF | [Md.31] Status: b14 |
| Interface signal | BUSY signal | OFF | Not in operation | [Md.141] BUSY |
| Interface signal | Positioning complete signal | OFF | Positioning complete signal is OFF | [Md.31] Status: b15 |
| Interface signal | Error detection signal | OFF | There is no error | [Md.31] Status: b13 |
| Interface signal | M code ON signal | OFF | M code ON signal is OFF | [Md.31] Status: b12 |
| External signal | Forced stop input signal | ON | There is no forced stop input | — |
| External signal | Stop signal | OFF | Stop signal is OFF | — |
| External signal | Upper limit (FLS) | ON | Within limit range | — |
| External signal | Lower limit (RLS) | ON | Within limit range | — |

*In the original, the "Signal name" and "Signal state" headers each span 2 columns; "Interface signal" is merged over 10 rows and "External signal" over 4 rows. Expanded to each row.

*1 When the CPU module is set to the asynchronous mode in the synchronization setting, the synchronization flag must be inserted in the program as an interlock condition. When it is set to the synchronous mode, the synchronization flag is turned ON when the CPU module executes calculation. Therefore, the interlock condition is not required to be inserted in the program.

#### Start time chart (始動用タイムチャート) (5.3 / original p.176)

##### Operation example (動作例) (5.3 / original p.176)

[Figure] Inching operation start time chart (original p.176)
- Speed waveform (vertical axis V, horizontal axis t): "Forward run inching operation" (positive rectangle) → "Reverse run inching operation" (negative rectangle).
- [Cd.190] PLC READY → [Cd.191] All axis servo ON → READY signal ([Md.140] Module status: b0) turn OFF→ON in this order (arrow from PLC READY to READY signal).
- [Cd.181] Forward run JOG start: OFF→ON (arrow → BUSY ON, forward run inching operation); later ON→OFF.
- [Md.141] BUSY: OFF→ON in response to [Cd.181] ON; ON→OFF after the forward inching movement ends. OFF→ON again in response to [Cd.182] ON; ON→OFF after the reverse inching movement ends.
- Positioning complete signal ([Md.31] Status: b15): OFF→ON at the end of each inching movement (arrow linked with BUSY OFF), ON→OFF after a fixed time.
- [Cd.182] Reverse run JOG start: OFF→ON after the forward run (arrow → BUSY ON, reverse run inching operation); later ON→OFF.
- Error detection signal ([Md.31] Status: b13): stays OFF.

#### Program example (プログラム例) (5.3 / original p.176)

Refer to the following for the program example of the inching operation.
→Page 634 Inching operation setting program [FX5-SSC-S]
→Page 706 JOG operation setting program [FX5-SSC-G]
→Page 634 JOG operation/inching operation execution program [FX5-SSC-S]
→Page 707 JOG operation/inching operation execution program [FX5-SSC-G]

(There is no program example (ladder) body in this chapter; it is in the Chapter 12/13 conversion.)

### Inching operation example (インチング運転の動作例) (5.3 / original p.177)

#### Example 1 (例1) (5.3 / original p.177)

If the JOG start signal is turned ON while the stop signal is ON, the error "Stop signal ON at start" (error code: 1908H [FX5-SSC-S], or error code 1A08H [FX5-SSC-G]) will occur.
The inching operation can be re-started when the stop signal is turned OFF and the JOG start signal is turned ON from OFF.

##### Operation example (動作例) (5.3 / original p.177)

[Figure] Example 1: inching operation and stop signal (original p.177)
- [Cd.190] PLC READY → [Cd.191] All axis servo ON → READY signal ([Md.140] Module status: b0) turn OFF→ON in this order.
- [Cd.181] Forward run JOG start OFF→ON → [Md.141] BUSY OFF→ON; inching movement (rectangle).
- [Cd.180] Axis stop OFF→ON at the point where the movement ends; BUSY ON→OFF (arrow from [Cd.180] ON).
- [Cd.181] ON→OFF, then OFF→ON again while [Cd.180] is still ON → label in figure: "Ignores that the JOG start signal is turned ON from OFF while the stop signal is ON." (BUSY stays OFF, no movement).
- [Cd.180] Axis stop ON→OFF, then [Cd.181] ON→OFF.
- [Cd.181] OFF→ON again → BUSY OFF→ON, inching movement → movement ends and BUSY ON→OFF; after that [Cd.181] ON→OFF.

## 5.4 Manual Pulse Generator Operation (手動パルサ運転) (5.4 / original p.178-187)

### Outline of manual pulse generator operation (手動パルサ運転の動作概要) (5.4 / original p.178-182)

#### Operation (動作) (5.4 / original p.178)

In manual pulse generator operations, pulses are input to the Simple Motion module/Motion module from the manual pulse generator. This causes the same number of input command to be output from the Simple Motion module/Motion module to the servo amplifier, and the workpiece is moved in the designated direction.
The following shows an example of manual pulse generator operation.

1. When "[Cd.21] Manual pulse generator enable flag" is set to "1", the BUSY signal turns ON and the manual pulse generator operation is enabled.
2. The workpiece is moved corresponding to the number of pulses input from the manual pulse generator.
3. The workpiece movement stops when no more pulses are input from the manual pulse generator.
4. When "[Cd.21] Manual pulse generator enable flag" is set to "0", the BUSY signal turns OFF and the manual pulse generator operation is disabled.

##### Operation example (動作例) (5.4 / original p.178)

[Figure] Manual pulse generator operation example (original p.178)
- Speed waveform (horizontal axis t): at 2. acceleration → constant speed → at 3. deceleration to stop (label in figure: "Manual pulse generator operation stops*1").
- [Cd.21] Manual pulse generator enable flag: 0→1 at 1., 1→0 at 4.
- [Md.141] BUSY: OFF→ON at 1., ON→OFF at 4.
- Manual pulse generator input: starts at 2., ends at 3.
- Start complete signal*2 ([Md.31] Status: b14): stays OFF.
- Period 1. to 4.: "Manual pulse generator operation enabled".

*1 If the input from the manual pulse generator stops or "0" is set in "[Cd.21] Manual pulse generator enable flag" during manual pulse generator operation, the machine will decelerate to a stop.
*2 The start complete signal does not turn ON in manual pulse generator operation.

> **Restriction**
> - Create the program so that "[Cd.21] Manual pulse generator enable flag" is always set to "0" (disabled) when a manual pulse generator operation is not carried out. Mistakenly touching the manual pulse generator when the "manual pulse generator enable flag" is set to "1" (enable) can cause accidents or incorrect positioning.
> - A pulse generator such as a manual pulse generator is required to carry out manual pulse generator operation.

#### Precautions during operation (動作上の注意) (5.4 / original p.179)

The following details must be understood before carrying out manual pulse generator operation.
- If "[Cd.21] Manual pulse generator enable flag" is turned ON while the Simple Motion module/Motion module is BUSY (BUSY signal ON), the warning "Start during operation" (warning code: 0900H [FX5-SSC-S], or warning code 0D00H [FX5-SSC-G]) will occur.
- If a stop factor occurs during manual pulse generator operation, the operation will stop, and the BUSY signal will turn OFF. At this time, "[Cd.21] Manual pulse generator enable flag" will remain ON. However, manual pulse generator operation will not be possible. To carry out manual pulse generator operation again, measures must be carried out to eliminate the stop factor. Once eliminated, the operation can be carried out again by turning "[Cd.21] Manual pulse generator enable flag" ON → OFF → ON. (Note that this excludes hardware/software stroke limit error.)
- Command will not be output if an error occurs when the manual pulse generator operation starts.

> **Restriction**
> The speed command is issued according to the input from the manual pulse generator irrelevant of the speed limit setting. When the speed command is larger than 62914560 [pulse/s], the servo alarm "Command frequency error" (alarm No.: 35) will occur.
> The following calculation formula is used to judge whether or not a servo alarm will occur.
>
> Speed command = Number of input pulses for one second × Manual pulse generator 1 pulse input magnification × Manual pulse generator 1 pulse movement amount × (Number of pulses per rotation / Movement amount per rotation)
>
> If a large value is set to the manual pulse generator 1 pulse input magnification, there is a high possibility of the servo alarm "Command frequency error" (alarm No.: 35) occurrence. Note that the servo motor does not work rapidly by rapid pulse input even if the servo alarm will not occur.

> **Point**
> - The Simple Motion module/Motion module can simultaneously command to multiple servo amplifiers by one manual pulse generator. (Axis 1 to the number of maximum control axes)
>
> [FX5-SSC-S]
> - Only one manual pulse generator can be connected to one Simple Motion module.
>
> [FX5-SSC-G]
> - The manual pulse generator is connected to a CPU module, high-speed pulse input/output module, etc. One Motion module can be connected to one manual pulse generator.

#### Manual pulse generator speed limit mode [FX5-SSC-G] (手動パルサ速度制限モード[FX5-SSC-G]) (5.4 / original p.180)

In "[Pr.122] Manual pulse generator speed limit mode", the output operation which exceeds "[Pr.123] Manual pulse generator speed limit value" can be set during manual pulse generator operation.
The setting value and operation for "[Pr.122] Manual pulse generator speed limit mode" are shown below.

| Setting value | Operation |
|---|---|
| 0 | The speed limit by "[Pr.123] Manual pulse generator speed limit value" is not executed. |
| 1 | The pulses which exceed "[Pr.123] Manual pulse generator speed limit value" are not output.*1 |
| 2 | The pulses which exceed "[Pr.123] Manual pulse generator speed limit value" are output later. The overcarrying movement amount which exceeds "[Pr.123] Manual pulse generator speed limit value" can be checked in "[Md.62] Amount of the manual pulser driving carrying over movement" (-2147483648 to 2147483647). When the movement amount which exceeds "[Pr.123] Manual pulse generator speed limit value" is generated continuously and "[Md.62] Amount of the manual pulser driving carrying over movement" exceeds tolerance (-2147483648 to 2147483647), the error "Manual pulse generator carry-over movement amount overflow" (error code: 1A82H) occurs and a deceleration stop is executed.*2 |

[Figure] Output waveform for each setting value (original p.180, figures inside the table)
- Each figure: vertical axis V ("Output"), horizontal axis t, dashed horizontal line = "[Pr.123] Manual pulse generator speed limit value"; two trapezoids: one below the limit value and one whose peak exceeds it.
- Setting value 0: both trapezoids are output as they are (the second exceeds the limit value).
- Setting value 1: the part of the second trapezoid above the limit value (hatched, dashed outline) is cut off; the output is clipped flat at the limit value.
- Setting value 2: the part above the limit value (hatched) is clipped, and a curved arrow shows it being moved to later; the output stays at the limit value longer and the end of the output (deceleration) is delayed (hatched area appended after the dashed original deceleration line).

*1 When "[Pr.123] Manual pulse generator speed limit value" is exceeded, the input from the manual pulse generator is not the same as the output from the Motion module.
*2 When the pulses which exceed "[Pr.123] Manual pulse generator speed limit value" are large, it takes time between when the input from the manual pulse generator stops and when the output from the Motion module stops.

- When "1: Do not output the exceeding speed limit value" or "2: Output the exceeding speed limit value delay" is set in "[Pr.122] Manual pulse generator speed limit mode", the warning "Manual pulse generator speed limit value over" (warning code: 0D49H) is output at exceeding "[Pr.123] Manual pulse generator speed limit value".
- The warning "Manual pulse generator speed limit value over" (warning code: 0D49H) prevents continuous detection by chattering so that the warning is not detected until the speed less than the speed limit value is kept for 10 seconds or more.
- When "0: Do not execute speed limit" is set in "[Pr.122] Manual pulse generator speed limit mode", the warning "Manual pulse generator speed limit value over" (warning code: 0D49H) will not be output even if the speed limit value is exceeded.

#### Operations when stroke limit error occurs (ストロークリミットエラー発生時の動作について) (5.4 / original p.181)

When the hardware stroke limit error or the software stroke limit error is detected*1 during operation, the operation will decelerate to a stop. However, in case of "[Md.26] Axis operation status", "Manual pulse generator operation" will continue*1. After stopping, input pulses from a manual pulse generator to the outside direction of the limit range are not accepted, but operation can be executed within the range.

*1 Only when the command position value or the machine feed value overflows or underflows during deceleration, the manual pulse generator operation will terminate as "error occurring". To carry out manual pulse generator operation again, "[Cd.21] Manual pulse generator enable flag" must be turned OFF once and turn ON.

[Figure] Manual pulse generator operation at stroke limit error (original p.181)
- Vertical axis V: "Manual pulse generator operation" at constant speed; when the upper/lower limit signal turns ON→OFF, the speed decelerates to 0 and stops.
- Upper/lower limit signal: ON→OFF.
- Within-range side: "Manual pulse generator operation possible"; outside-range side: "Manual pulse generator operation not possible".

#### Operation timing and processing time (動作タイミングと処理時間) (5.4 / original p.181)

The following drawing shows details of the manual pulse generator operation timing and processing time.

##### Operation example (動作例) (5.4 / original p.181)

[Figure] Manual pulse generator operation timing (original p.181)
- [Cd.21] Manual pulse generator enable flag: 0 → 1 → 0.
- [Md.141] BUSY: OFF→ON t1 after the enable flag changes 0→1; ON→OFF t4 after the enable flag changes 1→0.
- Manual pulse generator input pulses: input starts after BUSY ON → input ends.
- Start complete signal ([Md.31] Status: b14): label in figure: "The start complete signal does not turn ON in manual pulse generator operation."
- [Md.26] Axis operation status: Standby (0) → Manual pulse generator operation (4) (at BUSY ON) → Standby (0) (at BUSY OFF).
- Positioning operation: starts t2 after the input pulses start; ends t3 after the input pulses end.

- Normal timing time (Unit: [ms])

| Model | Operation cycle | t1*1 | t2*2*3 | t3*2*3 | t4 |
|---|---|---|---|---|---|
| FX5-SSC-S | 0.888 | 0.6 to 0.9 | 10 to 15 | 18 to 25 | 7.1 to 14.3 |
| FX5-SSC-S | 1.777 | 0.3 to 1.8 | 10 to 15 | 18 to 25 | 7.1 to 14.3 |
| FX5-SSC-G | 0.500 | 0.4 to 1.0 | 10 to 18 | 16 to 24 | 8 to 16 |
| FX5-SSC-G | 1.000 | 0.4 to 1.5 | 10 to 18 | 16 to 24 | 8 to 16 |
| FX5-SSC-G | 2.000 | 0.4 to 2.8 | 10 to 18 | 16 to 24 | 8 to 16 |
| FX5-SSC-G | 4.000 | 0.4 to 4.5 | 10 to 18 | 16 to 24 | 8 to 16 |

*In the original, "Operation cycle" is one header spanning the model and cycle columns; the model cell is merged (FX5-SSC-S over 2 rows, FX5-SSC-G over 4 rows). Expanded to each row.

*1 Delays may occur in the t1 timing time due to the operation status of other axes.
*2 The t2 and t3 timing time depend on the setting of the acceleration time, servo parameter, etc.
*3 For when "[Pr.156] Manual pulse generator smoothing time constant" is set to "0 ms". The time fluctuates depending on the setting value of "[Pr.156] Manual pulse generator smoothing time constant".

#### Position control by manual pulse generator operation (手動パルサ運転による位置の制御) (5.4 / original p.182)

In manual pulse generator operation, the position is moved by a "manual pulse generator 1 pulse movement amount" per pulse. The command position value in the positioning control by manual pulse generator operation can be calculated using the expression shown below.
Command position value = Number of input pulses × [Cd.20] Manual pulse generator 1 pulse input magnification × Manual pulse generator 1 pulse movement amount

| [Pr.1] Unit setting | mm | inch | degree | pulse |
|---|---|---|---|---|
| Manual pulse generator 1 pulse movement amount | 0.1 μm | 0.00001 inch | 0.00001 degree | 1 pulse |

For example, when "[Pr.1] Unit setting" is mm and "[Cd.20] Manual pulse generator 1 pulse input magnification" is 2, and 100 pulses are input from the manual pulse generator, the command position value is as follows.
100 × 2 × 0.1 = 20 [μm] ("[Md.20] Command position value" = 200)
The number of pulses output actually to the servo amplifier is "Manual pulse generator 1pulse movement amount/movement amount per pulse".
The movement amount per pulse can be calculated using the expression shown below.

Movement amount per pulse = ([Pr.3] Movement amount per rotation (AL) / [Pr.2] Number of pulses per rotation (AP)) × [Pr.4] Unit magnification (AM)

For example, when "[Pr.1] Unit setting" is mm and the movement amount per pulse is 1 μm, 0.1/1 = 1/10, i.e., the output to the servo amplifier per pulse from the manual pulse generator is 1/10 pulse. Thus, the Simple Motion module/Motion module outputs 1 pulse to the servo amplifier after receiving 10 pulses from the manual pulse generator.

#### Speed control by manual pulse generation operation (手動パルサ運転による速度の制御) (5.4 / original p.182)

The speed during positioning control by manual pulse generator operation is a speed corresponding to the number of input pulses per unit time, and can be obtained using the following equation.
Output command frequency = Input frequency × [Cd.20] Manual pulse generator 1 pulse input magnification

### Manual pulse generator operation execution procedure (手動パルサ運転の実行手順) (5.4 / original p.183)

The manual pulse generator operation is carried out by the following procedure.

[Figure] Manual pulse generator operation execution procedure flow (original p.183)
- Preparation
  - STEP 1: Set the parameters. [FX5-SSC-S] [Pr.1] to [Pr.24], [Pr.89], [Pr.151] / [FX5-SSC-G] [Pr.1] to [Pr.22], [Pr.156]
    - Note in figure: One of the following two methods can be used. <Method 1> Directly set (write) the parameters in the Simple Motion module/Motion module using the engineering tool. <Method 2> Set (write) the parameters from the CPU module to the Simple Motion module/Motion module using the program.
  - STEP 2: Create a program in which the "[Cd.20] Manual pulse generator 1 pulse input magnification" is set. (Control data setting) / Create a program in which the enable/disable is set for the manual pulse generator operation. ("[Cd.21] Manual pulse generator enable flag" setting.)
  - STEP 3: Write the program created in STEP1 and STEP2 to the CPU module.
- Manual pulse generator operation start
  - STEP 4: Issue a command to enable the manual pulse generator operation, and input the signals from the manual pulse generator.
    - Note in figure: Write "1" in "[Cd.21] Manual pulse generator enable flag", and operate the manual pulse generator.
- Monitoring of the manual pulse generator operation
  - STEP 5: Monitor the manual pulse generator operation.
    - Note in figure: Monitor using the engineering tool.
- Manual pulse generator operation stop
  - STEP 6: End the input from the manual pulse generator, and issue a command to disable the manual pulse generator operation.
    - Note in figure: Stop operating the manual pulse generator, and write "0" in "[Cd.21] Manual pulse generator enable flag".
- End of control

> **Point**
> - Mechanical elements such as limit switches are considered as already installed.
> - Parameter settings work in common for all control using the Simple Motion module/Motion module.

### Setting the required parameters for manual pulse generator operation (手動パルサ運転に必要なパラメータの設定) (5.4 / original p.184)

The "Positioning parameters" and "Common parameters" must be set to carry out manual pulse generator operation.
The following table shows the setting items of the required parameters for carrying out manual pulse generator operation. Parameters not shown below are not required to be set for carrying out only manual pulse generator operation. (Set the initial values or a value within the setting range.)
◎: Setting always required.
○: Set according to requirements (Set the initial value or a value within the setting range when not used.)

| Setting item (category) | No. | Setting item | Setting requirement |
|---|---|---|---|
| Positioning parameters | [Pr.1] | Unit setting | ◎ |
| Positioning parameters | [Pr.2] | Number of pulses per rotation (AP) (Unit: pulse) | ◎ |
| Positioning parameters | [Pr.3] | Movement amount per rotation (AL) (Unit: pulse) | ◎ |
| Positioning parameters | [Pr.4] | Unit magnification (AM) | ◎ |
| Positioning parameters | [Pr.8] | Speed limit value (Unit: pulse/s) | ◎ |
| Positioning parameters | [Pr.11] | Backlash compensation amount (Unit: pulse) | ○ |
| Positioning parameters | [Pr.12] | Software stroke limit upper limit value (Unit: pulse) | ○ |
| Positioning parameters | [Pr.13] | Software stroke limit lower limit value (Unit: pulse) | ○ |
| Positioning parameters | [Pr.14] | Software stroke limit selection | ○ |
| Positioning parameters | [Pr.15] | Software stroke limit valid/invalid setting | ○ |
| Positioning parameters | [Pr.17] | Torque limit setting value (Unit: 0.1%) | ○ |
| Common parameters | [Pr.24] | Manual pulse generator/Incremental synchronous encoder input selection [FX5-SSC-S] | ○ |
| Common parameters | [Pr.89] | Manual pulse generator/Incremental synchronous encoder input type selection [FX5-SSC-S] | ◎ |
| Common parameters | [Pr.151] | Manual pulse generator/Incremental synchronous encoder input logic selection [FX5-SSC-S] | ○ |
| Common parameters | [Pr.156] | Manual pulse generator smoothing time constant [FX5-SSC-G] | ○ |

*In the original, the "Setting item" header spans 3 columns; "Positioning parameters" is merged over 11 rows and "Common parameters" over 4 rows. Expanded to each row.

Refer to the following for the setting details.
→Page 444 Basic Setting

> **Point**
> - Positioning parameter settings and common parameters settings work in common for all controls using the Simple Motion module/Motion module. When carrying out other controls ("major positioning control", "high-level positioning control", "home position return control"), set the respective setting items as well.
> - "Positioning parameters" are set for each axis.

### Block diagram of the manual pulse generator operation [FX5-SSC-G] (手動パルサ運転のブロック図[FX5-SSC-G]) (5.4 / original p.185)

The flow of the manual pulse generator operation is shown below.

[Figure] Block diagram of the manual pulse generator operation [FX5-SSC-G] (original p.185)
- Manual pulse generator → CPU module → [Cd.55] Input value for manual pulse generator via CPU
- [Cd.55] Input value for manual pulse generator via CPU →(By 8 [ms])→ Manual pulse generator input value importing
- Manual pulse generator input value importing → Manual pulse generator smoothing
- [Pr.156] Manual pulse generator smoothing time constant →("[Cd.190] PLC READY" ON)→ Manual pulse generator smoothing
- Manual pulse generator smoothing → Magnification added
- [Cd.20] Manual pulse generator 1 pulse input magnification → Magnification added
- Magnification added → Output value

### Creating a program to enable/disable the manual pulse generator operation (手動パルサ運転の許可／不許可プログラムの作成) (5.4 / original p.186-187)

A program must be created to execute a manual pulse generator operation. Consider the "required control data setting", "start conditions" and "start time chart" when creating the program.
The following shows an example when a manual pulse generator operation is started for axis 1.

#### Required control data setting (設定の必要な制御データ) (5.4 / original p.186)

The control data shown below must be set to execute a manual pulse generator operation. The setting is carried out with the program.
n: Axis No. - 1

| No. | Setting item | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.20] | Manual pulse generator 1 pulse input magnification | 1 | Set the manual pulse generator 1 pulse input magnification. (1 to 10000 times) | 4322+100n<br>4323+100n |
| [Cd.21] | Manual pulse generator enable flag | 1 (0) | Set "1: Enable manual pulse generator operation".<br>(Set "0: Disable manual pulse generator operation" when finished with the manual pulse generator operation.) | 4324+100n |
| [Cd.55] | Input value for manual pulse generator via CPU [FX5-SSC-G] | → | Set the values used for the input values of the manual pulse generator via CPU in order.<br>Setting range: -2147483648 to 2147483647 [pulse] | 5946<br>5947 |

*In the original, the "Setting item" header spans 2 columns (No. and name). The "Setting value" cell of [Cd.55] is printed as "→" in the original.

Refer to the following for the setting details.
→Page 561 Control Data

> **Restriction**
> [FX5-SSC-G]
> Set the movement amount per capture cycle in "[Cd.55] Input value for manual pulse generator via CPU" within the range of -2147483648 to 2147483647. When set to a value outside of the range, the movement amount of the manual pulse generator and the movement amount of the output value may not match.

#### Start conditions (始動条件) (5.4 / original p.186)

The following conditions must be fulfilled when starting. The required conditions must also be assembled in the program, and the program must be configured so the operation will not start if the conditions are not fulfilled.

| Signal name (category) | Signal name | Signal state | Signal state (details) | Device |
|---|---|---|---|---|
| Interface signal | PLC READY signal | ON | CPU module preparation completed | [Cd.190] PLC READY |
| Interface signal | READY signal | ON | Preparation completed | [Md.140] Module status: b0 |
| Interface signal | All axis servo ON | ON | All axis servo ON | [Cd.191] All axis servo ON |
| Interface signal | Synchronization flag*1 | ON | The buffer memory can be accessed. | [Md.140] Module status: b1 |
| Interface signal | Axis stop signal | OFF | Axis stop signal is OFF | [Cd.180] Axis stop |
| Interface signal | Start complete signal | OFF | Start complete signal is OFF | [Md.31] Status: b14 |
| Interface signal | BUSY signal | OFF | Not in operation | [Md.141] BUSY |
| Interface signal | Error detection signal | OFF | There is no error | [Md.31] Status: b13 |
| Interface signal | M code ON signal | OFF | M code ON signal is OFF | [Md.31] Status: b12 |
| External signal | Forced stop input signal | ON | There is no forced stop input | — |
| External signal | Stop signal | OFF | Stop signal is OFF | — |
| External signal | Upper limit (FLS) | ON | Within limit range | — |
| External signal | Lower limit (RLS) | ON | Within limit range | — |

*In the original, the "Signal name" and "Signal state" headers each span 2 columns; "Interface signal" is merged over 9 rows and "External signal" over 4 rows. Expanded to each row.

*1 When the CPU module is set to the asynchronous mode in the synchronization setting, the synchronization flag must be inserted in the program as an interlock condition. When it is set to the synchronous mode, the synchronization flag is turned ON when the CPU module executes calculation. Therefore, the interlock condition is not required to be inserted in the program.

#### Start time chart (始動用タイムチャート) (5.4 / original p.187)

##### Operation example (動作例) (5.4 / original p.187)

[Figure] Manual pulse generator operation start time chart (original p.187)
- Speed waveform (horizontal axis t): "Forward run" (positive trapezoid) → "Reverse run" (negative trapezoid).
- Pulse input A-phase / Pulse input B-phase: 3 phase-shifted pulses in each section; in the forward run section the A-phase leads the B-phase, in the reverse run section the B-phase leads the A-phase.
- [Cd.190] PLC READY → [Cd.191] All axis servo ON → READY signal ([Md.140] Module status: b0) turn OFF→ON in this order (arrow from PLC READY to READY signal).
- Start complete signal ([Md.31] Status: b14): stays OFF.
- [Md.141] BUSY: OFF→ON in response to [Cd.21] 0→1 (arrow), ON→OFF in response to [Cd.21] 1→0 (arrow).
- Error detection signal ([Md.31] Status: b13): stays OFF.
- [Cd.21] Manual pulse generator enable flag: 0 → 1 (before the forward run) → 0 (after the reverse run ends).
- [Cd.20] Manual pulse generator 1 pulse input magnification: set to 1 (before the enable flag is set).

#### Program example (プログラム例) (5.4 / original p.187)

Refer to the following for the program example of the manual pulse generator operation.
→Page 634 Manual pulse generator operation program [FX5-SSC-S]
→Page 708 Manual pulse generator operation program [FX5-SSC-G]

(There is no program example (ladder) body in this chapter; it is in the Chapter 12/13 conversion.)
