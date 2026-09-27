# 7 CONTROL SUB FUNCTIONS (制御の補助機能) (Chapter 7 / original p.220-317)

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

## Conversion range (変換範囲表 / original p.220-317)

| Original page | Section | Handling |
|---|---|---|
| p.220-221 | 7 CONTROL SUB FUNCTIONS (chapter intro), 7.1 Outline of Sub Functions | Full text |
| p.222-228 | 7.2 Sub Functions Specifically for Machine Home Position Return (home position return retry, home position shift) | Full text |
| p.229-240 | 7.3 Functions for Compensating the Control (backlash compensation, electronic gear, near pass) | Full text |
| p.241-258 | 7.4 Functions to Limit the Control (speed limit, torque limit, software stroke limit, hardware stroke limit, forced stop) | Full text |
| p.259-277 | 7.5 Functions to Change the Control Details (speed change, override, acceleration/deceleration time change, torque change, target position change) | Full text |
| p.278-279 | 7.6 Functions Related to Start (pre-reading start function, including program example) | Full text |
| p.280-282 | 7.7 Absolute Position System | Full text |
| p.283-291 | 7.8 Functions Related to Stop (stop command processing for deceleration stop, continuous operation interrupt, step function) | Full text |
| p.292-314 | 7.9 Other Functions (skip, M code output, teaching, command in-position, acceleration/deceleration processing, deceleration start flag, speed control 10 × multiplier for degree axis, operation setting for incompletion of home position return) | Full text (program examples on p.294/p.298 transcribed; skip/teaching program bodies are references to p.636/p.714) |
| p.315-317 | 7.10 Servo ON/OFF (servo ON/OFF, PDS state transition, follow up function) | Full text |

## Table of Contents (目次)

- 7 CONTROL SUB FUNCTIONS (制御の補助機能)
- 7.1 Outline of Sub Functions (補助機能の概要)
- 7.2 Sub Functions Specifically for Machine Home Position Return (機械原点復帰固有の補助機能)
- 7.3 Functions for Compensating the Control (制御を補正する機能)
- 7.4 Functions to Limit the Control (制御を制限する機能)
- 7.5 Functions to Change the Control Details (制御内容を変更する機能)
- 7.6 Functions Related to Start (始動に関連する機能)
- 7.7 Absolute Position System (絶対位置システム)
- 7.8 Functions Related to Stop (停止に関連する機能)
- 7.9 Other Functions (その他の機能)
- 7.10 Servo ON/OFF (サーボON/OFF)

---

## 7 CONTROL SUB FUNCTIONS (制御の補助機能) (Chapter 7 / original p.220)

The details and usage of the "sub functions" added and used in combination with the main functions are explained in this chapter.
A variety of sub functions are available, including functions specifically for machine home position return and generally related functions such as control compensation, etc. More appropriate, finer control can be carried out by using these sub functions.
Each sub function is used together with a main function by creating matching parameter settings and programs. Read the execution procedures and settings for each sub function, and set as required.

## 7.1 Outline of Sub Functions (補助機能の概要) (7.1 / original p.220-221)

"Sub functions" are functions that compensate, limit, add functions, etc., to the control when the main functions are executed.
These sub functions are executed by parameter settings, operation from the engineering tool, sub function programs, etc.

### Outline of sub functions (補助機能の概要) (7.1 / original p.220-221)

The following table shows the types of sub functions available.

| Sub function | | Details |
|---|---|---|
| Functions characteristic to machine home position return | Home position return retry function | This function retries the home position return with the upper/lower limit switches during machine home position return. This allows machine home position return to be carried out even if the axis is not returned to before the proximity dog with JOG operation, etc. |
| Functions characteristic to machine home position return | Home position shift function | After returning to the machine home position, this function compensates the position by the designated distance from the machine home position and sets that position as the home position address. |
| Functions that compensate control | Backlash compensation function | This function compensates the mechanical backlash. Feed command equivalent to the set backlash amount are output each time the movement direction changes. |
| Functions that compensate control | Electronic gear function | By setting the movement amount per pulse, this function can freely change the machine movement amount per commanded pulse.<br>When the movement amount per pulse is set, a flexible positioning system that matches the machine system can be structured. |
| Functions that compensate control | Near pass function *1 | This function suppresses the machine vibration when the speed is changed during continuous path control in the interpolation control. |
| Functions that limit control | Speed limit function | If the command speed exceeds "[Pr.8] Speed limit value" during control, this function limits the commanded speed to within the "[Pr.8] Speed limit value" setting range. |
| Functions that limit control | Torque limit function | If the torque generated by the servo motor exceeds "[Pr.17] Torque limit setting value" during control, this function limits the generated torque to within the "[Pr.17] Torque limit setting value" setting range. |
| Functions that limit control | Software stroke limit function | If a command outside of the upper/lower limit stroke limit setting range, set in the parameters, is issued, this function will not execute positioning for that command. |
| Functions that limit control | Hardware stroke limit function | This function carries out deceleration stop with the hardware stroke limit switch. |
| Functions that limit control | Forced stop function | This function stops all axes of the servo amplifier with the forced stop signal. |
| Functions that change control details | Speed change function | This function changes the speed during positioning.<br>Set the changed speed in the speed change buffer memory ([Cd.14] New speed value), and change the speed with the speed change request ([Cd.15] Speed change request). |
| Functions that change control details | Override function | This function changes the speed by a designated percentage during positioning. This is executed using "[Cd.13] Positioning operation speed override". |
| Functions that change control details | Acceleration/deceleration time change function | This function changes the acceleration/deceleration time during speed change. |
| Functions that change control details | Torque change function | This function changes the "torque limit value" during control. |
| Functions that change control details | Target position change function | This function changes the target position during the execution of positioning. At the same time, this also can change the speed. |
| Functions related to positioning start | Pre-reading start function | This function shortens the virtual start time. |
| Absolute position system function | (merged) | This function restores the absolute position of designated axis. |
| Functions related to positioning stop | Stop command processing for deceleration stop function | This function selects a deceleration curve when a stop cause occurs during deceleration stop processing to speed 0. |
| Functions related to positioning stop | Continuous operation interrupt function | This function interrupts continuous operation. When this request is accepted, the operation stops when the execution of the current positioning data is completed. |
| Functions related to positioning stop | Step function | This function temporarily stops the operation to confirm the positioning operation during debugging, etc.<br>The operation can be stopped at each "automatic deceleration" or "positioning data". |
| Other functions | Skip function | This function stops the positioning being executed (decelerates to a stop) when the skip signal is input, and carries out the next positioning. |
| Other functions | M code output function | This function issues a command for a sub work (clamp or drill stop, tool change, etc.) according to the code No. (0 to 65535) that can be set for each positioning data.<br>The M code output timing can be set for each positioning data. |
| Other functions | Teaching function | This function stores the address positioned with manual control into the positioning address ([Da.6] Positioning address/movement amount) having the designated positioning data No. |
| Other functions | Command in-position function | This function calculates the remaining distance for the Simple Motion module/Motion module to reach the positioning stop position, and when the value is less than the set value, sets the "command in-position flag".<br>When using another sub work before ending the control, use this function as a trigger for the sub work. |
| Other functions | Acceleration/deceleration processing function | This function adjusts the control acceleration/deceleration. |
| Other functions | Deceleration start flag function | This function turns ON the flag when the constant speed status or acceleration status switches to the deceleration status during position control, whose operation pattern is "Positioning complete", to make the stop timing known. |
| Other functions | Speed control 10 × multiplier setting for degree axis function | This function executes the positioning control by the 10 × speed of the command speed and the speed limit value when the setting unit is "degree". |
| Other functions | Operation setting for incompletion of home position return function | This function is provided to select whether positioning control is operated or not when the home position return request flag is ON. |
| Servo ON/OFF | Servo ON/OFF | This function executes servo ON/OFF of the servo amplifiers connected to the Simple Motion module/Motion module. |
| Servo ON/OFF | Follow up function | This function monitors the motor rotation amount with the servo turned OFF, and reflects it on the command position value. |

*In the original, the category cells in the first column are merged vertically over their rows (e.g. "Functions that limit control" over 5 rows, "Other functions" over 8 rows). "Absolute position system function" is one cell merged over the first two columns. The table continues from p.220 to p.221 (the rows from "Functions related to positioning stop" are on p.221). Expanded to each row.

*1 The near pass function is featured as standard and is valid only for setting continuous path control for position control. It cannot be set to be invalid with parameters.

## 7.2 Sub Functions Specifically for Machine Home Position Return (機械原点復帰固有の補助機能) (7.2 / original p.222-228)

The sub functions specifically for machine home position return include the "home position return retry function" and "home position shift function". Each function is executed by parameter setting.

### Home position return retry function [FX5-SSC-S] (原点復帰リトライ機能[FX5-SSC-S]) (7.2 / original p.222-225)

When the workpiece goes past the home position without stopping during positioning control, it may not move back in the direction of the home position although a machine home position return is commanded, depending on the workpiece position. This normally means the workpiece has to be moved to a position before the proximity dog by a JOG operation, etc., to start the machine home position return again. However, by using the home position return retry function, a machine home position return can be carried out regardless of the workpiece position.

#### Control details (制御内容) (7.2 / original p.222-224)

The following drawing shows the operation of the home position return retry function.

##### Home position return retry point return retry operation when the workpiece is within the range between the upper and lower limits. (ワークが上下限リミットの範囲内にある場合の原点復帰リトライ動作) (7.2 / original p.222)

[Figure] Home position return retry operation within the upper/lower limit range (original p.222)
- Point 1: movement starts (from a position between the proximity dog and the hardware limit switch) toward the hardware limit switch.
- Point 2: at "Limit signal OFF" (Hardware limit switch) the operation decelerates.
- Point 3: after stopping, the axis moves in the opposite direction at a constant speed, passing through the proximity dog area.
- Point 4: when the proximity dog (ON area) ends (proximity dog OFF), the operation decelerates and stops.
- Point 5: from the stop, the axis moves again in the home position return direction; at proximity dog ON it decelerates to creep speed; after the proximity dog OFF and the zero signal, it stops.
- Point 6: machine home position return completion (at a zero signal pulse after the proximity dog OFF).
- Signals drawn: Proximity dog (ON area), Zero signal (pulses), Hardware limit switch (Limit signal OFF area).

1. The movement starts in the "[Pr.44] Home position return direction" by a machine home position return start.
2. The operation decelerates when the limit signal OFF is detected.
3. After stopping due to the limit signal OFF detection, the operation moves at the "[Pr.46] Home position return speed" in the opposite direction of the "[Pr.44] Home position return direction".
4. The operation decelerates when the proximity dog turns OFF.
5. After stopping due to the proximity dog OFF, a machine home position return is carried out in the "[Pr.44] Home position return direction". (The zero point of the encoder must be passed at least once depending on the home position return method.)
6. Machine home position return completion.

##### Home position return retry operation when the workpiece is outside the range between the upper and lower limits. (ワークが上下限リミットの範囲外にある場合の原点復帰リトライ動作) (7.2 / original p.223)

- When the direction from the workpiece to the home position is the same as the "[Pr.44] Home position return direction", a normal machine home position return is carried out. The example shown below is for when "0: Positive direction" is set in "[Pr.44] Home position return direction".

[Figure] Normal machine home position return (workpiece on the lower limit side) (original p.223)
- Machine home position return start near the hardware lower limit switch; movement in the [Pr.44] Home position return direction (positive, arrow to the right).
- Accelerates to the home position return speed, decelerates at proximity dog ON to the creep speed, and stops at the home position (zero signal after proximity dog OFF).
- Hardware lower limit switch (left), Proximity dog, Hardware upper limit switch (right); Movement range is between the lower and upper limit switches.

- When the direction from the workpiece to the home position is the opposite direction from the "[Pr.44] Home position return direction", the operation carries out a deceleration stop when the proximity dog turns OFF, and then carries out a machine home position return in the direction set in "[Pr.44] Home position return direction". The example shown below is for when "0: Positive direction" is set in "[Pr.44] Home position return direction".

[Figure] Retry when the workpiece is beyond the home position (original p.223)
- Machine home position return start at a position near the hardware upper limit switch (beyond the home position in the [Pr.44] direction).
- The axis moves in the negative direction (opposite to [Pr.44]), passes the proximity dog, and decelerates to a stop after the proximity dog turns OFF.
- It then moves in the [Pr.44] Home position return direction (positive), decelerates at proximity dog ON, and stops at the home position (zero signal).
- Hardware lower limit switch, Proximity dog, Zero signal, Hardware upper limit switch; Movement range between the lower and upper limit switches.

> **Point**
> - When the "0: Positive direction" is selected in "[Pr.44] Home position return direction", the upper limit switch is set to the limit switch in the home position return direction.
> - When the "1: Negative direction" is selected in "[Pr.44] Home position return direction", the lower limit switch is set to the limit switch in the home position return direction.
> - If inverting the install positions of upper/lower limit switches, hardware stroke limit function cannot be operated properly. If any problem is found for home position return operation, review "Rotation direction selection/travel direction selection (PA14)"*1 and the wiring for the upper/lower limit switch.

*1 For MR-J4(W)-B. "Travel direction selection (PA14)" for MR-J5(W)-B.

##### Setting the dwell time during a home position return retry (原点復帰リトライ時のドウェルタイム設定) (7.2 / original p.224)

The home position return retry function can perform such function as the dwell time using "[Pr.57] Dwell time during home position return retry" when the reverse run operation is carried out due to detection by the limit signal for upper and lower limits and when the machine home position return is executed after the proximity dog is turned OFF to stop the operation.
"[Pr.57] Dwell time during home position return retry" is validated when the operation stops at the "A" and "B" positions in the following drawing. (The dwell time is the same value at both positions "A" and "B".)

[Figure] Dwell time positions A and B during home position return retry (original p.224)
- Machine home position return start → movement in the [Pr.44] Home position return direction → "Stop by limit signal detection" at the Hardware limit switch (Limit signal OFF) = position A.
- From A: "Reverse run operation after limit signal detection" (opposite direction) through the proximity dog → "Stop by proximity dog OFF" = position B.
- From B: "Machine home position return executed again" in the [Pr.44] direction; decelerates at the proximity dog to creep speed and stops at the Home position (zero signal).
- [Pr.57] dwell time applies at A and at B.

#### Precaution during control (制御上の注意事項) (7.2 / original p.224)

- The following table shows whether the home position return retry function may be executed by the "[Pr.43] Home position return method".

| [Pr.43] Home position return method | Execution status of home position return retry function |
|---|---|
| Proximity dog method | ○: Execution possible |
| Count method 1 | ○: Execution possible |
| Count method 2 | ○: Execution possible |
| Data set method | — |
| Scale origin signal detection method | ×: Execution not possible |
| Driver home position return method | — |

- Always establish upper/lower limit switches at the upper/lower limit positions of the machine. If the home position return retry function is used without hardware stroke limit switches, the motor will continue rotation until a hardware stroke limit signal is detected.
- Do not configure a system so that the servo amplifier power turns OFF by the upper/lower limit switches connected to the Simple Motion module. If the servo amplifier power is turned OFF, the home position return retry cannot be carried out.
- The operation decelerates upon detection of the hardware limit signal, and the movement starts in the opposite direction. In this case, however, the error "Hardware stroke limit (+)" (error code: 1904H) or "Hardware stroke limit (-)" (error code: 1906H) does not occur.

> **Point**
> The settings of the upper/lower stroke limit signal are shown below. The home position return retry function can be used with either setting. (→Page 250 Hardware stroke limit function)
> - External input signal of servo amplifier
> - External input signal via CPU (buffer memory of Simple Motion module)

#### Setting method (設定方法) (7.2 / original p.225)

To use the "home position return retry function", set the required details in the parameters shown in the following table, and write them to the Simple Motion module.
When the parameters are set, the home position return retry function will be added to the machine home position return control. The set details are validated at the rising edge (OFF → ON) of the "[Cd.190] PLC READY". Set "[Pr.57] Dwell time during home position return retry" according to the user's requirements.

| Setting item | | Setting value | Setting details | Factory-set initial value |
|---|---|---|---|---|
| [Pr.48] | Home position return retry | 1 | Set "1: Carry out home position return retry by limit switch". | 0 |
| [Pr.57] | Dwell time during home position return retry | → | Set the deceleration stop time during home position return retry.<br>(Random value between 0 and 65535 (ms)) | 0 |

Refer to the following for the setting details.
→Page 444 Basic Setting

> **Point**
> - Parameters are set for each axis.
> - It is recommended that the parameters be set whenever possible with the engineering tool. Execution by a program uses many programs and devices. The execution becomes complicated, and the scan times will increase.

### Home position shift function [FX5-SSC-S] (原点シフト機能[FX5-SSC-S]) (7.2 / original p.226-228)

When a machine home position return is carried out, the home position is normally established using the proximity dog and zero signal. However, by using the home position shift function, the machine can be moved a designated movement amount from the position where the zero signal was detected. A mechanically established home position can then be interpreted at that point.

#### Control details (制御内容) (7.2 / original p.226)

The following drawing shows the operation of the home position shift function.

[Figure] Operation of the home position shift function (original p.226)
- Machine home position return start → accelerates to "[Pr.46] Home position return speed" in the [Pr.44] Home position return direction.
- At proximity dog ON, decelerates to "[Pr.47] Creep speed"; after the proximity dog OFF, stops at the zero signal.
- From the zero signal position, the axis moves "[Pr.53] Home position shift amount" at the "Speed selected by the '[Pr.56] Speed designation during home position shift'" (drawn at the [Pr.46] level) and stops.

#### Setting range for the home position shift amount (原点シフト量の設定範囲) (7.2 / original p.226)

Set the home position shift amount within the range from the detected zero signal to the upper/lower limit switches.

[Figure] Setting range for the home position shift amount (original p.226)
- [Pr.44] Home position return direction: toward the lower limit switch side (arrow to the left) in this example.
- "Setting range of the negative home position shift amount": from the detected zero signal to the lower limit switch (address decrease direction).
- "Setting range of the positive home position shift amount": from the detected zero signal to the upper limit switch (address increase direction), passing the proximity dog.

#### Movement speed during home position shift (原点シフト時の移動速度) (7.2 / original p.227)

When using the home position shift function, the movement speed during the home position shift is set in "[Pr.56] Speed designation during home position shift". The movement speed during the home position shift is selected from either the "[Pr.46] Home position return speed" or the "[Pr.47] Creep speed". For the acceleration/deceleration time, the value specified in "[Pr.51] Home position return acceleration time selection" or "[Pr.52] Home position return deceleration time selection" is used.
The following drawings show the movement speed during the home position shift when a mechanical home position return is carried out by the proximity dog method.

##### Home position shift operation at the "[Pr.46] Home position return speed" (When "[Pr.56] Speed designation during home position shift" is 0) ("[Pr.46]原点復帰速度"での原点シフト動作) (7.2 / original p.227)

[Figure] Home position shift at [Pr.46] Home position return speed (original p.227)
- Machine home position return start → [Pr.46] Home position return speed in the [Pr.44] direction → deceleration at proximity dog ON to creep speed → stop at the zero signal.
- When the "[Pr.53] Home position shift amount" is positive: the axis accelerates to [Pr.46] Home position return speed in the positive direction and stops at the Home position.
- When the "[Pr.53] Home position shift amount" is negative (dashed line): the axis moves in the reverse direction at [Pr.46] Home position return speed and stops at the Home position.

##### Home position shift operation at the "[Pr.47] Creep speed" (When "[Pr.56] Speed designation during home position shift" is 1) ("[Pr.47]クリープ速度"での原点シフト動作) (7.2 / original p.227)

[Figure] Home position shift at [Pr.47] Creep speed (original p.227)
- Same home position return as above; the shift movement after the zero signal is carried out at [Pr.47] Creep speed.
- Positive shift amount: moves forward at creep speed to the Home position. Negative shift amount (dashed line): moves in reverse at creep speed to the Home position.

#### Precautions during control (制御上の注意事項) (7.2 / original p.227)

- The following data are set after the home position shift amount is complete.
  - Home position return complete flag ([Md.31] Status: b4)
  - [Md.20] Command position value
  - [Md.21] Machine feed value
  - [Md.26] Axis operation status

  Home position return request flag ([Md.31] Status: b3) is reset after completion of the home position shift.
- "[Pr.53] Home position shift amount" is not added to "[Md.34] Movement amount after proximity dog ON". The movement amount immediately before the home position shift operation, considering proximity dog ON as "0", is stored.

#### Setting method (設定方法) (7.2 / original p.228)

To use the "home position shift function", set the required details in the parameters shown in the following table, and write them to the Simple Motion module.
When the parameters are set, the home position shift function will be added to the machine home position return control. The set details are validated at the rising edge (OFF → ON) of the "[Cd.190] PLC READY".

| Setting item | | Setting value | Setting details | Factory-set initial value |
|---|---|---|---|---|
| [Pr.53] | Home position shift amount | → | Set the shift amount during the home position shift. | 0 |
| [Pr.56] | Speed designation during home position shift | → | Select the speed during the home position shift<br>0: [Pr.46] Home position return speed<br>1: [Pr.47] Creep speed | 0 |

Refer to the following for the setting details.
→Page 444 Basic Setting

> **Point**
> - Parameters are set for each axis.
> - It is recommended that the parameters be set whenever possible with the engineering tool. Execution by a program uses many programs and devices. The execution becomes complicated, and the scan times will increase.

## 7.3 Functions for Compensating the Control (制御を補正する機能) (7.3 / original p.229-240)

The sub functions for compensating the control include the "backlash compensation function", "electronic gear function", and "near pass function". Each function is executed by parameter setting or program creation and writing.

### Backlash compensation function (バックラッシュ補正機能) (7.3 / original p.229-230)

The "backlash compensation function" compensates the backlash amount in the mechanical system.

#### Control details (制御内容) (7.3 / original p.229)

When the backlash compensation amount is set, an extra amount of command equivalent to the set backlash amount is output every time the movement direction changes.
The following drawing shows the operation of the backlash compensation function.

[Figure] Backlash compensation (original p.229)
- Worm gear engaging with the Workpiece; the gap between the gear tooth and the workpiece groove is "[Pr.11] Backlash compensation amount".

#### Precautions during control (制御上の注意事項) (7.3 / original p.229)

- The feed command of the backlash compensation amount are not added to the "[Md.20] Command position value" or "[Md.21] Machine feed value".
- Always carry out a machine home position return before starting the control when using the backlash compensation function (when "[Pr.11] Backlash compensation amount" is set). The backlash in the mechanical system cannot be correctly compensated if a machine home position return is not carried out.
- Backlash compensation, which includes the movement amount and "[Pr.11] Backlash compensation amount", is output the moment at the moving direction changes.
  For details on the setting, refer to the following.
  →Page 462 [Pr.11] Backlash compensation amount
- Backlash compensation cannot be made when the speed control mode, torque control mode or continuous operation to torque control mode.
- In an axis operation such as positioning after home position return, whether the backlash compensation is necessary or not is judged from "[Pr.44] Home position return direction" of the Simple Motion module/Motion module. When the positioning is executed in the same direction as "[Pr.44] Home position return direction", the backlash compensation is not executed. However, when the positioning is executed in the reverse direction against "[Pr.44] Home position return direction", the backlash compensation is executed.

#### Setting method (設定方法) (7.3 / original p.230)

To use the "backlash compensation function", set the "backlash compensation amount" in the parameter shown in the following table, and write it to the Simple Motion module/Motion module.
The set details are validated at the rising edge (OFF → ON) of the "[Cd.190] PLC READY".

| Setting item | | Setting value | Setting details | Factory-set initial value |
|---|---|---|---|---|
| [Pr.11] | Backlash compensation amount | → | Set the backlash compensation amount. | 0 |
| [Pr.44] | Home position return direction | → | Set the same direction as the last home position return direction of the servo amplifier when using the driver home position return method. | 0 |

Refer to the following for the setting details.
→Page 444 Basic Setting

> **Point**
> - Parameters are set for each axis.
> - It is recommended that the parameters be set whenever possible with the engineering tool. Execution by a program uses many programs and devices. The execution becomes complicated, and the scan times will increase.

### Electronic gear function (電子ギア機能) (7.3 / original p.231-238)

The "electronic gear function" adjusts the actual machine movement amount and number of pulse output to servo amplifier according to the parameters set in the Simple Motion module/Motion module.
The "electronic gear function" has the following three functions ([A] to [C]).
- [A] During machine movement, the function increments in the Simple Motion module/Motion module values less than one pulse that could not be output, and outputs the incremented amount when the total incremented value reached one pulse or more.
- [B] When machine home position return is completed, current value changing is completed, speed control is started (except when command position value is updated), or fixed-feed control is started, the function clears to "0" the cumulative values of less than one pulse which could not be output. (If the cumulative value is cleared, an error will occur by a cleared amount in the feed machine value. Control can be constantly carried out at the same machine movement amount, even when the fixed-feed control is continued.)
- [C] The function compensates the mechanical system error of the command movement amount and actual movement amount by adjusting the "electronic gear". (The "movement amount per pulse" value is defined by "[Pr.2] Number of pulses per rotation (AP)", "[Pr.3] Movement amount per rotation (AL)" and "[Pr.4] Unit magnification (AM)".)

The Simple Motion module/Motion module automatically carries out the processing for [A] and [B].
The "Electronic gear function" section in this chapter is different from the "Electronic gear function" of the servo amplifier. For the "Electronic gear function" of the servo amplifier, refer to the following manual.
[Other manual] MR-J5 User's Manual (Function)

#### Precautions (注意事項) (7.3 / original p.231)

[FX5-SSC-S]
When MR-J5(W)-B series is used, there are restrictions on the electronic gear setting of the servo amplifier depending on the operation mode and encoder resolution. For details, refer to the following.
→Page 845 Connection with MR-J5(W)-B

[FX5-SSC-G]
The setting for the electronic gear of the servo amplifier is limited depending on the resolution of the encoder. For details, refer to the following.
→Page 850 Devices Compatible with CC-Link IE TSN [FX5-SSC-G]

#### Basic concept of the electronic gear (電子ギアの基本的な考え方) (7.3 / original p.232-237)

The electronic gear is an item which determines how many rotations (rotations by how many pulses) the motor must make in order to move the machine according to the programmed movement amount.

[Figure] Basic concept of the electronic gear (original p.232)
- Simple Motion module/Motion module: Command value (Control unit) → AP / (AL × AM) → pulse → Servo amplifier → pulse → Motor (M) → Reduction ratio → Machine (ball screw).
- Encoder (ENC) → pulse → Feedback pulse → Servo amplifier → pulse back to the module → Control unit back to Command value.

The basic concept of the electronic gear is represented by the following expression.
[Pr.2] (Number of pulses per rotation) = AP
[Pr.3] (Movement amount per rotation) = AL
[Pr.4] (Unit magnification) = AM
Movement amount per rotation that considered unit magnification = ΔS

```
Electronic gear = AP / ΔS = AP / (AL × AM)   ... (1)
```

Set values for AP, AL and AM so that this related equation is established.
However, because values to be set for AP, AL and AM have the settable range, values calculated (reduced) from the above related equation must be contained in the setting range for AP, AL and AM.

##### For "Ball screw" + "Reduction gear" (ボールネジ＋減速機の場合) (7.3 / original p.232-233)

Ex.
[FX5-SSC-S]
When the ball screw pitch is 10 mm, the motor is the HG-KR (4194304 pulses/rev) and the reduction ratio is 9/44.

[Figure] Motor (M) → Reduction ratio 9/44 → ball screw → machine (original p.232)

First, find how many millimeters the load (machine) will travel (ΔS) when the motor turns one revolution (AP).
AP (Number of pulses per rotation) = 4194304 [pulse]
ΔS (Movement amount per rotation) = Ball screw pitch × Reduction ratio = 10 [mm] × 9/44 = 110000.0 [μm] × 9/44*1

*1 When the control unit is "mm", the minimum command unit is 0.1 μm.

*Note: the original prints "110000.0 [μm]" here (and on p.233); the calculation on p.233 uses "10000.0 [μm] × 9/44". Transcribed as printed (要確認).

> **Point**
> When controlling an HK-KT motor (67108864 pulses/rev), set the servo parameters of MR-J5(W)-B as follows.
> Electronic gear numerator (PA06): 16
> Electronic gear denominator (PA07): 1
> Therefore, AP (Number of pulses per rotation) becomes the following value.
> AP (Number of pulses per rotation) = 67108864 [pulse] × 1/16 = 4194304 [pulse]
>
> [Figure] Simple Motion module (Command value / Control unit / AP ÷ (AL × AM)) → pulse → Servo amplifier (Electronic gear numerator (PA06): 16, Electronic gear denominator (PA07): 1) → pulse × 16 → M → Reduction ratio 9/44 → Machine; ENC → pulse → Feedback pulse → Servo amplifier → Control unit pulse/16 back to the module. (original p.232)

[FX5-SSC-G]
When the ball screw pitch is 10 mm, the motor is the HK-KT (67108864 pulses/rev) and the reduction ratio is 9/44.

[Figure] Motion module (Command value / Control unit / AP ÷ (AL × AM)) → pulse → Servo amplifier (Electronic gear numerator (PA06): 16, Electronic gear denominator (PA07): 1) → pulse × 16 → M → Reduction ratio 9/44 → Machine; ENC → pulse → Feedback pulse; Control unit pulse/16 back to the module. (original p.233)

First, find how many millimeters the load (machine) will travel (ΔS) when the motor turns one revolution (AP).
AP (Number of pulses per rotation) = 67108864 [pulse] × 1/16 = 4194304 [pulse]
ΔS (Movement amount per rotation) = Ball screw pitch × Reduction ratio = 10 [mm] × 9/44 = 110000.0 [μm] × 9/44*1

*1 When the control unit is "mm", the minimum command unit is 0.1 μm.

> **Point**
> Set the servo parameters of MR-J5(W)-G as follows.
> Electronic gear numerator (PA06): 16
> Electronic gear denominator (PA07): 1

Substitute this for the above expression (1).
At this time, make calculation with the reduction ratio 9/44 remaining as a fraction.

```
AP / ΔS = 4194304 [pulse] / (10000.0 [μm] × 9/44)
        = (4194304 × 44) / (10000.0 × 9)
        = 184549376 / 90000.0
        = 23068672 / 11250.0 = 23068672(AP) / (11250.0(AL) × 1(AM))
        = 23068672(AP) / (1125.0(AL) × 10(AM))
```

Thus, AP, AL and AM to be set are as follows. These two examples of settings are only examples. There are settings other than these examples.

| Setting value | Setting item |
|---|---|
| AP = 23068672 | [Pr.2] |
| AL = 11250.0 | [Pr.3] |
| AM = 1 | [Pr.4] |

or

| Setting value | Setting item |
|---|---|
| AP = 23068672 | [Pr.2] |
| AL = 1125.0 | [Pr.3] |
| AM = 10 | [Pr.4] |

##### When "pulse" is set as the control unit (制御単位をpulse(パルス)に設定した場合) (7.3 / original p.234)

When using pulse as the control unit, set the electronic gear as follows.
AP = "Number of pulses per rotation"
AL = "Movement amount per rotation"
AM = 1

Ex.
When the motor is HG-KR (4194304 pulses/rev) [FX5-SSC-S]/HK-KT (67108864 pulses/rev) [FX5-SSC-G]

> **Point**
> [FX5-SSC-S]
> When controlling an HK-KT motor (67108864 pulses/rev), set the servo parameters of MR-J5(W)-B as follows.
> Electronic gear numerator (PA06): 16
> Electronic gear denominator (PA07): 1
> [FX5-SSC-G]
> Set the servo parameters of MR-J5(W)-G as follows.
> Electronic gear numerator (PA06): 16
> Electronic gear denominator (PA07): 1

| Setting value | Setting item |
|---|---|
| AP = 4194304 | [Pr.2] |
| AL = 4194304 | [Pr.3] |
| AM = 1 | [Pr.4] |

##### When "degree" is set as the control unit for a rotary axis (回転軸で制御単位をdegreeに設定した場合) (7.3 / original p.234-235)

Ex.
When the rotary axis is used, the motor is HG-KR (4194304 pulses/rev) [FX5-SSC-S]/HK-KT (67108864 pulses/rev) [FX5-SSC-G] and the reduction ratio is 3/11.

[Figure] Rotary table driven by the motor (M) through Reduction ratio 3/11 (original p.234)

First, find how many degrees the load (machine) will travel (ΔS) when the motor turns one revolution (AP).
[FX5-SSC-S]
AP (Number of pulses per rotation) = 4194304 [pulse]
ΔS (Movement amount per rotation) = 360.00000 [degree] × Reduction ratio 360.00000 × 3/11

> **Point**
> When controlling an HK-KT motor (67108864 pulses/rev), set the servo parameters of MR-J5(W)-B as follows.
> Electronic gear numerator (PA06): 16
> Electronic gear denominator (PA07): 1
> Therefore, AP (Number of pulses per rotation) becomes the following value.
> AP (Number of pulses per rotation) = 67108864 [pulse] × 1/16 = 4194304 [pulse]

[FX5-SSC-G] (original p.235)
AP (Number of pulses per rotation) = 67108864 [pulse] x1/16 = 4194304 [pulse]
ΔS (Movement amount per rotation) = 360.00000 [degree] × Reduction ratio = 360.00000 × 3/11

> **Point**
> Set the servo parameters of MR-J5(W)-G as follows.
> Electronic gear numerator (PA06): 16
> Electronic gear denominator (PA07): 1

Substitute this for the above expression (1).
At this time, make calculation with the reduction ratio 3/11 remaining as a fraction.

```
AP / ΔS = 4194304 [pulse] / (360.00000 [degree] × 3/11)
        = (4194304 [pulse] × 11) / (360.00000 [degree] × 3)
        = 46137344 / 1080.00000
        = 2883584 / 67.50000 = 2883584(AP) / (67.50000(AL) × 1(AM))
        = 2883584(AP) / (0.06750(AL) × 1000(AM))
```

Thus, AP, AL and AM to be set are as follows. These two examples of settings are only examples. There are settings other than these examples.

| Setting value | Setting item |
|---|---|
| AP = 2883584 | [Pr.2] |
| AL = 67.50000 | [Pr.3] |
| AM = 1 | [Pr.4] |

or

| Setting value | Setting item |
|---|---|
| AP = 2883584 | [Pr.2] |
| AL = 0.06750 | [Pr.3] |
| AM = 1000 | [Pr.4] |

##### When "mm" is set as the control unit for conveyor drive (calculation including π) (コンベア駆動で制御単位をmmに設定した場合(πを含む計算)) (7.3 / original p.236-237)

Ex.
When the belt conveyor drive is used, the conveyor diameter is 135 mm, the pulley ratio is 1/3, the motor is HG-KR (4194304 pulses/rev) [FX5-SSC-S]/HK-KT (67108864 pulses/rev) [FX5-SSC-G] and the reduction ratio is 7/53.

[Figure] Motor (M) → Reduction ratio 7/53 → Pulley ratio 1/3 → Belt conveyor (φ135 mm) (original p.236)

As the travel value of the conveyor is used to exercise control, set "mm" as the control unit.
First, find how many millimeters the load (machine) will travel (ΔS) when the motor turns one revolution (AP).
[FX5-SSC-S]
AP (Number of pulses per rotation) = 4194304 [pulse]
ΔS (Movement amount per rotation) = 135000.0 [μm] × π × Reduction ratio = 135000.0 [μm] × π × 7/53 × 1/3

> **Point**
> When controlling an HK-KT motor (67108864 pulses/rev), set the servo parameters of MR-J5(W)-B as follows.
> Electronic gear numerator (PA06): 16
> Electronic gear denominator (PA07): 1
> Therefore, AP (Number of pulses per rotation) becomes the following value.
> AP (Number of pulses per rotation) = 67108864 [pulse] × 1/16 = 4194304 [pulse]

[FX5-SSC-G]
AP (Number of pulses per rotation) = 67108864 [pulse] x1/16 = 4194304 [pulse]
ΔS (Movement amount per rotation) = 135000.0 [μm] × π × Reduction ratio = 135000.0 [μm] × π × 7/53 × 1/3

> **Point**
> Set the servo parameters of MR-J5(W)-G as follows.
> Electronic gear numerator (PA06): 16
> Electronic gear denominator (PA07): 1

ΔS (Movement amount per rotation)
= 135000.0 [μm] × π × Reduction ratio
= 135000.0 [μm] × π × 7/53 × 1/3
Substitute this for the above expression (1).
At this time, make calculation with the reduction ratio 7/53 × 1/3 remaining as a fraction.

```
AP / ΔS = AP / (AL × AM) = 4194304 [pulse] / (135000.0 [μm] × π × 7/53 × 1/3)
                         = (4194304 × 53 × 3) / (135000.0 × π × 7)
                         = 166723584 / (236250 × π)
```

Here, make calculation on the assumption that π is equal to 3.141592654.

```
AP / ΔS = AP / (AL × AM) = 166723584 / 742201.2645075
```

AL has a significant number to first decimal place, round down numbers to two decimal places.

```
AP / ΔS = AP / (AL × AM) = 166723584 / 742201.2 = 166723584(AP) / (742201.2(AL) × 1(AM))
```

Thus, AP, AL and AM to be set are as follows.

| Setting value | Setting item |
|---|---|
| AP = 166723584 | [Pr.2] |
| AL = 742201.2 | [Pr.3] |
| AM = 1 | [Pr.4] |

This setting will produce an error for the true machine value, but it cannot be helped. (original p.237)
This error is as follows.

```
[ (7422012/166723584) / (2362500π/166723584) - 1 ] × 100 = -8.69 × 10^-6 [%]
```

AP (Number of pulses per rotation) = 4194304 [pulse]
ΔS (Movement amount per rotation)
= 135000.0 [μm] × π × Reduction ratio
= 135000.0 [μm] × π × 7/53 × 1/3
It is equivalent to an about 86.9 [μm] error in continuous 1 km feed.

##### Number of pulses/movement amount at linear servo motor use (リニアサーボモータ使用時のパルス数･移動量) (7.3 / original p.237)

[Figure] Linear servo motor configuration (original p.237)
- Simple Motion module/Motion module (Command value / Control unit / AP ÷ (AL × AM)) → pulse → Servo amplifier → pulse → Linear servo motor.
- Linear encoder → pulse → Feedback pulse → Servo amplifier → pulse back to the module.

Calculate the number of pulses (AP) and movement amount (AL × AM) for the linear encoder in the following conditions.

```
Linear encoder resolution = Number of pulses (AP) / Movement amount (AL × AM)
```

Ex.
Linear encoder resolution: 0.05 [μm] per pulse

```
1 [pulse] / 0.05 [μm] = Number of pulses (AP) [pulse] / Movement amount (AL × AM) [μm] = 20 / 1.0
```

Set the number of pulses in "[Pr.2] Number of pulses per rotation (AP)", the movement amount in "[Pr.3] Movement amount per rotation (AL)", and the unit magnification in "[Pr.4] Unit magnification (AM)" in the actual setting.
Set AP, AL, AM as shown below.

| Servo amplifier | Setting |
|---|---|
| When using MR-J4(W)-B [FX5-SSC-S] | Set the same value in AP, AL, and AM as the value set in the servo parameter "Linear encoder resolution - Numerator (PL02)" and "Linear encoder resolution - Denominator (PL03)". Refer to each servo amplifier instruction manual for details. |
| When using MR-J5(W)-B [FX5-SSC-S] | Set the same value in AP, AL, and AM as the value set in the servo parameter "Electronic gear numerator (PA06)", "Electronic gear denominator (PA07)", "Linear encoder resolution - Numerator (PL02)" and "Linear encoder resolution - Denominator (PL03)". Refer to each servo amplifier manual for details. |
| When using MR-J4(W)-G [FX5-SSC-G] | Set the same value in AP, AL, and AM as the value set in the servo parameter "Electronic gear numerator (PA06)", "Electronic gear denominator (PA07)", "Linear encoder resolution - Numerator (PL02)" and "Linear encoder resolution - Denominator (PL03)". Refer to each servo amplifier manual for details. |

*In the original, this table has no header row (the header "Servo amplifier / Setting" is added here). The right cell is merged over the 2 rows "MR-J5(W)-B [FX5-SSC-S]" and "MR-J4(W)-G [FX5-SSC-G]". Expanded to each row.

When set to the following,

| Setting values |
|---|
| Linear encoder resolution - Numerator (PL02): 1 [μm]<br>Linear encoder resolution - Denominator (PL03): 20 [μm] |
| Electronic gear numerator (PA06): 1<br>Electronic gear denominator (PA07): 1 |

The values of AP, AL and AM are shown below.

| Setting value | Setting item |
|---|---|
| AP = 20 | [Pr.2] |
| AL = 1.0 | [Pr.3] |
| AM = 1 | [Pr.4] |

#### The method for compensating the error (誤差補正方法) (7.3 / original p.238)

When the position control is carried out using the "Electronic gear" set in a parameter, this may produce an error between the command movement amount (L) and the actual movement amount (L'). With Simple Motion module/Motion module, this error is compensated by adjusting the electronic gear.
The "Error compensation amount", which is used for error compensation, is defined as follows:

```
Error compensation amount = Command movement amount (L) / Actual movement amount (L')
```

The electronic gear including an error compensation amount is shown below.

```
AP / (AL × AM) × L / L' = AP' / (AL' × AM')
```

[Figure] Electronic gear with error compensation (original p.238)
- Upper: Simple Motion module/Motion module: Command value ⇄ Control unit ⇄ AP/(AL × AM) ⇄ L/L' ⇄ pulse ⇄ Servo amplifier. L/L' is "1 if there is no error (in regular case)".
- Arrow "Electronic gear taking an error into consideration" → Lower: Command value ⇄ Control unit ⇄ AP'/(AL' × AM') ⇄ pulse ⇄ Servo amplifier.

##### Calculation example (計算例) (7.3 / original p.238)

(Conditions)
- Number of pulses per rotation (AP) : 4194304 [pulse]
- Movement amount per rotation (AL) : 5000.0 [μm]
- Unit magnification (AM) : 1

(Positioning results)
- Command movement amount (L) : 100 [mm]
- Actual movement amount (L') : 101 [mm]

(Compensation value)

```
AP / (AL × AM) × L / L' = 4194304 / (5000.0 × 1) × 100 / 101 = 4194304(AP') / (5050(AL') × 1(AM'))
```

- Number of pulses per rotation (AP') : 4194304 ... [Pr.2]
- Movement amount per rotation (AL') : 5050.0 ... [Pr.3]
- Unit magnification (AM') : 1 ... [Pr.4]

Set the post-compensation "[Pr.2] Number of pulses per rotation (AP')", "[Pr.3] Movement amount per rotation (AL')", and "[Pr.4] Unit magnification (AM')" in the parameters, and write them to the Simple Motion module/Motion module. The set details are validated at the rising edge (OFF → ON) of the "[Cd.190] PLC READY".

### Near pass function (近傍通過機能) (7.3 / original p.239-240)

When continuous pass control is carried out using interpolation control, the near pass function is carried out.
The "near pass function" is a function to suppress the mechanical vibration occurring at the time of switching the positioning data when continuous pass control is carried out using interpolation control.
[Near pass function]
The extra movement amount occurring at the end of each positioning data unit being continuously executed is carried over to the next positioning data unit. Alignment is not carried out, and thus the output speed drops are eliminated, and the mechanical vibration occurring during speed changes can be suppressed.
Because alignment is not carried out, the operation is controlled on a path that passes near the position set in "[Da.6] Positioning address/movement amount".

#### Control details (制御内容) (7.3 / original p.239)

The following drawing shows the path of the continuous path control by the 2-axis linear interpolation control.

##### The path of the near pass (近傍通過の軌跡) (7.3 / original p.239)

[Figure] Path of the near pass (original p.239)
- Path of positioning data No.3 heads toward "[Da.6] Positioning address"; before reaching it, the path switches to the path of positioning data No.4 (passes near the [Da.6] address, not through it; the direct path via the address is shown dashed).
- V-t chart: one trapezoid over positioning data No.3 and No.4; at the switching point between No.3 and No.4 "Speed dropping does not occur."

#### Precautions during control (制御上の注意事項) (7.3 / original p.240)

- If the movement amount designated by the positioning data is small when the continuous path control is executed, the output speed may not reach the designated speed.
- The movement direction is not checked during interpolation operation. Therefore, a deceleration stops are not carried out even if the movement direction changes. (See below) For this reason, the output will rapidly reverse when the reference axis movement direction changes. To prevent the rapid output reversal, assign not the continuous path control "11", but the continuous positioning control "01" to the positioning data of the passing point.

##### Positioning by interpolation (補間による位置決め) (7.3 / original p.240)

[Figure] Positioning by interpolation (original p.240)
- Reference axis (horizontal) / Partner axis (vertical). Positioning data No.1 moves up-right, positioning data No.2 moves down-right (partner axis direction reverses at the passing point).
- "Positioning data No.1 ..... Continuous path control"

##### Operation of reference axis (基準軸の動作) (7.3 / original p.240)

[Figure] Operation of reference axis (original p.240)
- V-t: accelerates during positioning data No.1, constant speed continues across the boundary into positioning data No.2, then decelerates to 0 at the end of No.2. No speed change at the boundary.

##### Operation of partner axis for interpolation (補間の相手軸の動作) (7.3 / original p.240)

[Figure] Operation of partner axis for interpolation (original p.240)
- V-t: accelerates in the positive direction and runs at constant speed during positioning data No.1; at the boundary to No.2 the speed jumps directly from positive to negative ("Rapidly reverse direction"); runs at constant negative speed and decelerates to 0 at the end of No.2.

## 7.4 Functions to Limit the Control (制御を制限する機能) (7.4 / original p.241-258)

Functions to limit the control include the "speed limit function", "torque limit function", "software stroke limit function", "hardware stroke limit function", and "forced stop function". Each function is executed by parameter setting or program creation and writing.

### Speed limit function (速度制限機能) (7.4 / original p.241-242)

The speed limit function limits the command speed to a value within the "speed limit value" setting range when the command speed during control exceeds the "speed limit value".

#### Relation between the speed limit function and various controls (速度制限機能と各制御の関係) (7.4 / original p.241)

The following table shows the relation of the "speed limit function" and various controls.
◎: Always set
—: Setting not required (Use the initial value or a value within the setting range.)

| Control type | | | Speed limit function | Speed limit value |
|---|---|---|---|---|
| Home position return control | Machine home position return control | — | ◎ | [Pr.8] Speed limit value<br>The speed limit value follows the specifications of the servo amplifier when using the driver home position return method. |
| Home position return control | Fast home position return control | — | ◎ | [Pr.8] Speed limit value |
| Major positioning control | Position control | 1-axis linear control | ◎ | [Pr.8] Speed limit value |
| Major positioning control | Position control | 2 to 4-axis linear interpolation control | ◎ | [Pr.8] Speed limit value |
| Major positioning control | Position control | 1-axis fixed-feed control | ◎ | [Pr.8] Speed limit value |
| Major positioning control | Position control | 2 to 4-axis fixed-feed control (interpolation) | ◎ | [Pr.8] Speed limit value |
| Major positioning control | Position control | 2-axis circular interpolation control | ◎ | [Pr.8] Speed limit value |
| Major positioning control | 1 to 4-axis speed control | — | ◎ | [Pr.8] Speed limit value |
| Major positioning control | Speed-position switching control, Position-speed switching control | — | ◎ | [Pr.8] Speed limit value |
| Major positioning control | Other control | Current value changing | — | Setting value invalid |
| Major positioning control | Other control | JUMP instruction, NOP instruction, LOOP to LEND | — | Setting value invalid |
| Manual control | JOG operation, Inching operation | — | ◎ | [Pr.31] JOG speed limit value |
| Manual control | Manual pulse generator operation | — | — | Setting is invalid |
| Expansion control | Speed-torque control | — | ◎ | [Pr.8] Speed limit value |

*In the original, "Control type" spans 3 columns; where the 2nd-level cell has no 3rd level it is merged over columns 2-3 (shown as "—" in the 3rd column here). "Home position return control" is merged over 2 rows, "Major positioning control" over 9 rows, "Position control" over 5 rows, "Other control" over 2 rows, "Manual control" over 2 rows. In the "Speed limit value" column, "[Pr.8] Speed limit value" is one cell merged from Fast home position return control through Speed-position switching control (8 rows), and "Setting value invalid" is merged over the 2 "Other control" rows. Expanded to each row.

#### Precautions during control (制御上の注意事項) (7.4 / original p.241)

- If any axis exceeds "[Pr.8] Speed limit value" during 2- to 4-axis speed control, the axis exceeding the speed limit value is controlled with the speed limit value. The speeds of the other axes being interpolated are suppressed by the command speed ratio.
- If the reference axis exceeds "[Pr.8] Speed limit value" during 2-axis circular interpolation control, the reference axis is controlled with the speed limit value (The speed limit does not function on the interpolation axis side.)
- If any axis exceeds "[Pr.8] Speed limit value" during 2- to 4-axis linear interpolation control or 2- to 4-axis fixed-feed control, the axis exceeding the speed limit value is controlled with the speed limit value. The speeds of the other axes being interpolated are suppressed by the movement amount ratio.

> **Point**
> When the "reference axis speed" is set during interpolation control, set so the major axis side becomes the reference axis. If the minor axis side is set as the reference axis, the major axis side speed may exceed the "[Pr.8] Speed limit value".

#### Setting method (設定方法) (7.4 / original p.242)

To use the "speed limit function", set the "speed limit value" in the parameters shown in the following table, and write them to the Simple Motion module/Motion module.
The set details are validated at the next start after they are written to the Simple Motion module/Motion module.

| Setting item | | Setting value | Setting details | Factory-set initial value |
|---|---|---|---|---|
| [Pr.8] | Speed limit value | → | Set the speed limit value (max. speed during control). | 200000 |
| [Pr.31] | JOG speed limit value | → | Set the speed limit value during JOG operation (max. speed during control).<br>(Note that "[Pr.31] JOG speed limit value" shall be less than or equal to "[Pr.8] Speed limit value".) | 20000 |

Refer to the following for the setting details.
→Page 444 Basic Setting

> **Point**
> - Parameters are set for each axis.
> - It is recommended that the parameters be set whenever possible with the engineering tool. Execution by a program uses many programs and devices. The execution becomes complicated, and the scan times will increase.

### Torque limit function (トルク制限機能) (7.4 / original p.243-246)

The "torque limit function" limits the generated torque to a value within the "torque limit value" setting range when the torque generated in the servo motor exceeds the "torque limit value".
The "torque limit function" protects the deceleration function, limits the power of the operation pressing against the stopper, etc. It controls the operation so that unnecessary force is not applied to the load and machine.

#### Relation between the torque limit function and various controls (トルク制限機能と各制御の関係) (7.4 / original p.243)

The following table shows the relation of the "torque limit function" and various controls.
○: Set when required (Set to " — " when not used.)
—: Setting not required (Use the initial value or a value within the setting range.)

| Control type | | | Torque limit function | Torque limit value *1 |
|---|---|---|---|---|
| Home position return control | Machine home position return control | — | ○ | [FX5-SSC-S]<br>"[Pr.17] Torque limit setting value" or "[Cd.101] Torque output setting value".<br>After the "[Pr.47] Creep speed" is reached, this value becomes the "[Pr.54] Home position return torque limit value".<br>[FX5-SSC-G]<br>"[Pr.17] Torque limit setting value" or "[Cd.101] Torque output setting value".*2<br>After the "[Pr.47] Creep speed" is reached, this value becomes the "[Pr.54] Home position return torque limit value".*3 |
| Home position return control | Fast home position return control | — | ○ | "[Pr.17] Torque limit setting value" or "[Cd.101] Torque output setting value". |
| Major positioning control | Position control | 1-axis linear control | ○ | "[Pr.17] Torque limit setting value" or "[Cd.101] Torque output setting value". |
| Major positioning control | Position control | 2 to 4-axis linear interpolation control | ○ | "[Pr.17] Torque limit setting value" or "[Cd.101] Torque output setting value". |
| Major positioning control | Position control | 1-axis fixed-feed control | ○ | "[Pr.17] Torque limit setting value" or "[Cd.101] Torque output setting value". |
| Major positioning control | Position control | 2 to 4-axis fixed-feed control (interpolation) | ○ | "[Pr.17] Torque limit setting value" or "[Cd.101] Torque output setting value". |
| Major positioning control | Position control | 2-axis circular interpolation control | ○ | "[Pr.17] Torque limit setting value" or "[Cd.101] Torque output setting value". |
| Major positioning control | 1 to 4-axis speed control | — | ○ | "[Pr.17] Torque limit setting value" or "[Cd.101] Torque output setting value". |
| Major positioning control | Speed-position switching control, Position-speed switching control | — | ○ | "[Pr.17] Torque limit setting value" or "[Cd.101] Torque output setting value". |
| Major positioning control | Other control | Current value changing | — | Setting value is invalid. |
| Major positioning control | Other control | JUMP instruction, NOP instruction, LOOP to LEND | — | Setting value is invalid. |
| Manual control | JOG operation, Inching operation | — | ○ | "[Pr.17] Torque limit setting value" or "[Cd.101] Torque output setting value". |
| Manual control | Manual pulse generator operation | — | ○ | "[Pr.17] Torque limit setting value" or "[Cd.101] Torque output setting value". |
| Expansion control | Speed-torque control | — | ○ | Torque limit value is continued after control mode switching. |

*In the original, "Control type" spans 3 columns (2nd-level cells without a 3rd level are merged over columns 2-3; "—" here). The first-level and "Position control"/"Other control" cells are merged vertically as in the speed limit table. The Machine home position return control "Torque limit value" is split into an [FX5-SSC-S] cell and an [FX5-SSC-G] cell (combined into one cell here). The "Torque limit value" cell "'[Pr.17] ...' or '[Cd.101] ...'" is merged from Fast home position return control through Speed-position switching control (8 rows), "Setting value is invalid." over the 2 Other control rows, and "'[Pr.17] ...' or '[Cd.101] ...'" over the 2 Manual control rows. Expanded to each row.

*1 Shows the torque limit value when "[Cd.22] New torque value/forward new torque value" or "[Cd.113] New reverse torque value" is set to "0".
*2 Only the value specified at start is enabled. The value cannot be changed during homing.
*3 For the setting method, refer to the servo amplifier manuals.
For MR-J5(W)-G: [Other manual] MR-J5-G/MR-J5W-G User's Manual (Parameters)

#### Control details (制御内容) (7.4 / original p.244)

The following drawing shows the operation of the torque limit function.

##### Operation example (動作例) (7.4 / original p.244)

[Figure] Torque limit function operation example (original p.244)
- Signals: Each operation, [Cd.190] PLC READY, [Cd.191] All axis servo ON, [Cd.184] Positioning start, [Pr.17] Torque limit setting value, [Cd.101] Torque output setting value, [Cd.112] Torque change function switching request, [Cd.22] New torque value/forward new torque value, [Md.35] Torque limit stored value/forward torque limit stored value.
- [Cd.112] = 0 (Forward/reverse torque limit value same setting) throughout. [Cd.22] = 0 throughout.
- Initial: [Pr.17] = 300, [Cd.101] = 0, [Md.35] = 0.
- [Cd.190] PLC READY ON (*1; then [Cd.191] All axis servo ON turns ON): [Md.35] becomes 300 ([Pr.17], since [Cd.101] = 0).
- 1st [Cd.184] Positioning start ON (*2, *3): [Md.35] = 300 ([Cd.101] = 0 → torque limit setting value used). Each operation runs.
- During the 1st operation [Cd.101] is changed to 100, then after it [Pr.17] is changed to 250.
- 2nd [Cd.184] ON (*2, *3): [Md.35] = 100 ([Cd.101]).
- [Cd.101] is changed to 150 during the 2nd operation.
- [Cd.190] PLC READY and [Cd.191] turn OFF, then PLC READY ON again (*1): [Md.35] = 150.
- 3rd [Cd.184] ON (*2, *3): [Md.35] = 150.

*1 The torque limit setting value or torque output setting value becomes effective at the "[Cd.190] PLC READY" rising edge (however, after the servo turned ON.)
If the torque output setting value is "0" or larger than the torque limit setting value, the torque limit setting value will be its value.
*2 The torque limit setting value or torque output setting value becomes effective at the "[Cd.184] Positioning start" rising edge.
If the torque output setting value is "0" or larger than the torque limit setting value, the torque limit setting value will be its value.
*3 The torque change value is cleared to "0" at the "[Cd.184] Positioning start" rising edge.

#### Precautions during control (制御上の注意事項) (7.4 / original p.244)

- When limiting the torque at the "[Pr.17] Torque limit setting value", confirm that "[Cd.22] New torque value/forward new torque value" or "[Cd.113] New reverse torque value" is set to "0". If this parameter is set to a value besides "0", the setting value will be validated, and the torque will be limited at that value. (Refer to →Page 268 Torque change function for details about the "new torque value".)
- When the operation is stopped by torque limiting, the droop pulse will remain in the deviation counter. If the load torque is eliminated, operation for the amount of droop pulses will be carried out. Note that the movement might start rapidly as soon as the load torque is eliminated.

[FX5-SSC-S]
- When the "[Pr.54] Home position return torque limit value" exceeds the "[Pr.17] Torque limit setting value", the error "Home position return torque limit value error" (error code: 1B0DH) occurs.

#### Setting method (設定方法) (7.4 / original p.245-246)

- To use the "torque limit function", set the "torque limit value" in the parameters shown in the following table, and write them to the Simple Motion module/Motion module.

The set details are validated at the rising edge (OFF → ON) of the "[Cd.190] PLC READY".

| Setting item | | Setting value | Setting details | Factory-set initial value |
|---|---|---|---|---|
| [Pr.17] | Torque limit setting value | → | Set the torque limit value*1 in 0.1% unit. | 3000 |
| [Pr.54] | Home position return torque limit value [FX5-SSC-S] | → | Set the torque limit value after the speed reaches "[Pr.47] Creep speed" in 0.1% unit. | 3000 |

The set details are validated at the rising edge (OFF → ON) of the "[Cd.184] Positioning start".

| Setting item | | Setting value | Setting details | Factory-set initial value |
|---|---|---|---|---|
| [Cd.101] | Torque output setting value*2 | → | Set the torque output value in 0.1% unit. | 0 |

*1 Torque limit value: Will be an upper limit value of the torque change value. If a larger value has been mistakenly input for the torque change value, it is restricted within the torque limit setting values to prevent an erroneous entry. (Even if a value larger than the torque limit setting value has been input to the torque change value, the torque value is not changed.)
*2 Torque output setting value: Taken at the positioning start and used as a torque limit value. If the value is "0" or the torque limit setting value or larger, the parameter "torque limit setting value" is taken at the start.

Refer to the following for the setting details.
→Page 444 Basic Setting, →Page 561 Control Data

- The "torque limit value" set in the Simple Motion module/Motion module is set in the "[Md.35] Torque limit stored value/forward torque limit stored value" or "[Md.120] Reverse torque limit stored value".

[Figure] Torque limit value data flow (original p.245)
- CPU module ⇄ Simple Motion module/Motion module Buffer memory: [Pr.17] Torque limit setting value, [Pr.54] Home position return torque limit value, [Cd.22] New torque value/forward new torque value, [Cd.113] New reverse torque value, [Cd.101] Torque output setting value.
- These are selected ("Positioning control") into the "Torque limit value" sent to the Servo amplifier; the valid value is stored back into [Md.35] Torque limit stored value/forward torque limit stored value and [Md.120] Reverse torque limit stored value.

- The following table shows the storage details of "[Md.35] Torque limit stored value/forward torque limit stored value" and "[Md.120] Reverse torque limit stored value".

n: Axis No. - 1

| Monitor item | | Monitor value | Storage details | Buffer memory address |
|---|---|---|---|---|
| [Md.35] | Torque limit stored value/forward torque limit stored value | → | The "torque limit value/forward torque limit stored value" valid at that time is stored. ([Pr.17], [Pr.54], [Cd.22] or [Cd.101]) | 2426+100n |
| [Md.120] | Reverse torque limit stored value | → | The "reverse torque limit stored value" is stored depending on the control status. ([Pr.17], [Pr.54], [Cd.22], [Cd.101] or [Cd.113]) | 2491+100n |

Refer to the following for information on the storage details.
→Page 518 Monitor Data

> **Point** (original p.246)
> - Parameters are set for each axis.
> - It is recommended that the parameters be set whenever possible with the engineering tool. Execution by a program uses many programs and devices. The execution becomes complicated, and the scan times will increase.
> - Use "[Md.120] Reverse torque limit stored value" and "[Cd.113] New reverse torque value" only when "1: Forward/reverse torque limit value individual setting" is set in "[Cd.112] Torque change function switching request". (→Page 268 Torque change function)

### Software stroke limit function (ソフトウェアストロークリミット機能) (7.4 / original p.246-251)

In the "software stroke limit function" the address established by a machine home position return is used to set the upper and lower limits of the moveable range of the workpiece. Movement commands issued to addresses outside that setting range will not be executed.
In the Simple Motion module/Motion module, the "command position value" and "machine feed value" are used as the addresses indicating the current position. However, in the "software stroke limit function", the address used to carry out the limit check is designated in the "[Pr.14] Software stroke limit selection". Refer to the following for details on the "command position value" and "machine feed value".
→Page 69 Confirming the current value
The upper and lower limits of the moveable range of the workpiece are set in "[Pr.12] Software stroke limit upper limit value"/"[Pr.13] Software stroke limit lower limit value".

#### Differences in the moveable range (可動領域の違い) (7.4 / original p.246-247)

The following drawing shows the moveable range of the workpiece when the software stroke limit function is used.

[Figure] Workpiece moveable range (original p.246)
- Ball screw with workpiece between RLS (left) and FLS (right) limit switches.
- "Workpiece moveable range" is from "Software stroke limit (lower limit)" to "Software stroke limit (upper limit)", both inside the RLS/FLS positions.

The following drawing shows the differences in the operation when "[Md.20] Command position value" and "[Md.21] Machine feed value" are used in the moveable range limit check.

##### Conditions (条件) (7.4 / original p.246)

Assume the current stop position is 2000, and the upper stroke limit is set to 5000.

[Figure] Conditions (original p.246)
- Stop position: [Md.20] Command position value 2000, [Md.21] Machine feed value 2000.
- Upper stroke limit: [Md.20] 5000, [Md.21] 5000. Moveable range up to 5000.

##### Current value changing (現在値変更) (7.4 / original p.247)

When the current value is changed by a new current value command from 2000 to 1000, the command position value will change to 1000, but the machine feed value will stay the same at 2000.
- When the machine feed value is set at the limit

The machine feed value of 5000 (command position value: 4000) becomes the upper stroke limit.

[Figure] Machine feed value at the limit (original p.247)
- Points: [Md.20] 1000 / [Md.21] 2000 (current); [Md.20] 4000 / [Md.21] 5000 = Upper stroke limit (end of moveable range); [Md.20] 5000 / [Md.21] 6000 (outside).

- When the command position value is set at the limit

The command position value of 5000 (machine feed value: 6000) becomes the upper stroke limit.

[Figure] Command position value at the limit (original p.247)
- Points: [Md.20] 1000 / [Md.21] 2000 (current); [Md.20] 4000 / [Md.21] 5000; [Md.20] 5000 / [Md.21] 6000 = Upper stroke limit (end of moveable range).

> **Point**
> When "machine feed value" is set in "[Pr.14] Software stroke limit selection", the moveable range becomes an absolute range referenced on the home position. When "command position value" is set, the moveable range is the relative range from the "command position value".

#### Software stroke limit check details (ソフトウェアストロークリミットチェックの内容) (7.4 / original p.247)

| Check details | | Processing when an error occurs |
|---|---|---|
| 1) | An error shall occur if the current value*1 is outside the software stroke limit range*2. (Check "[Md.20] Command position value" or "[Md.21] Machine feed value".) | The following errors will occur.<br>[FX5-SSC-S]<br>Error "Software stroke limit +" (error code: 1993H, 1A18H) and "Software stroke limit -" (error code: 1995H, 1A1AH)<br>[FX5-SSC-G]<br>Error "Software stroke limit +" (error code: 1A93H, 1B18H) and "Software stroke limit -" (error code: 1A95H, 1B1AH) |
| 2) | An error shall occur if the command address is outside the software stroke limit range. (Check "[Da.6] Positioning address/movement amount".) | The following errors will occur.<br>[FX5-SSC-S]<br>Error "Software stroke limit +" (error code: 1993H, 1A18H) and "Software stroke limit -" (error code: 1995H, 1A1AH)<br>[FX5-SSC-G]<br>Error "Software stroke limit +" (error code: 1A93H, 1B18H) and "Software stroke limit -" (error code: 1A95H, 1B1AH) |

*In the original, the "Processing when an error occurs" cell is merged over the 2 rows. Expanded to each row.

*1 Check whether the "[Md.20] Command position value" or "[Md.21] Machine feed value" is set in "[Pr.14] Software stroke limit selection".
*2 Moveable range from the "[Pr.12] Software stroke limit upper limit value" to the "[Pr.13] Software stroke limit lower limit value".

#### Relation between the software stroke limit function and various controls (ソフトウェアストロークリミット機能と各制御の関係) (7.4 / original p.248)

◎: Check valid
○: Check is not made when the command position value is not updated (→Page 467 [Pr.21] Command position value during speed control) at the setting of "command position value" in "[Pr.14] Software stroke limit selection" during speed control.
—: Check not carried out (check invalid).
△: Valid only when "0: valid" is set in the "[Pr.15] Software stroke limit valid/invalid setting".

| Control type | | | Limit check | Processing at check |
|---|---|---|---|---|
| Home position return control | Machine home position return control | Data set method | ◎ | The home position return control will not be carried out if the home position address is outside the software stroke limit range. |
| Home position return control | Machine home position return control | Other than "Data set method" | — | Check not carried out. |
| Home position return control | Fast home position return control | — | — | Check not carried out. |
| Major positioning control | Position control | 1-axis linear control | ◎ | Checks 1) and 2) in →Page 245 Software stroke limit check details are carried out.<br>For speed control: The axis decelerates to a stop when it exceeds the software stroke limit range.<br>For position control: The axis comes to an immediate stop when it exceeds the software stroke limit range. |
| Major positioning control | Position control | 2 to 4-axis axis linear interpolation control | ◎ | (same as above: Checks 1) and 2) ... immediate stop when it exceeds the software stroke limit range.) |
| Major positioning control | Position control | 1-axis fixed-feed control | ◎ | (same as above) |
| Major positioning control | Position control | 2 to 4-axis fixed-feed control (interpolation) | ◎ | (same as above) |
| Major positioning control | Position control | 2-axis circular interpolation control | ◎ | (same as above) |
| Major positioning control | 1 to 4-axis speed control | — | ○*1*2 | (same as above) |
| Major positioning control | Speed-position switching control, Position-speed switching control | — | ○*1*2 | (same as above) |
| Major positioning control | Other control | Current value changing | ◎ | The current value will not be changed if the new position value is outside the software stroke limit range. |
| Major positioning control | Other control | JUMP instruction, NOP instruction, LOOP to LEND | — | Check not carried out. |
| Manual control | JOG operation, Inching operation | — | △*3 | Check 1) in →Page 245 Software stroke limit check details is carried out.<br>The machine will carry out a deceleration stop when the software stroke limit range is exceeded. If the address is outside the software stroke limit range, the operation can only be started toward the moveable range. |
| Manual control | Manual pulse generator operation | — | △*3 | Check 1) in →Page 245 Software stroke limit check details is carried out.<br>The machine will carry out a deceleration stop when the software stroke limit range is exceeded. If the address is outside the software stroke limit range, the operation can only be started toward the moveable range. |
| Expansion control | Speed-torque control | — | ◎ | Check 1) in →Page 245 Software stroke limit check details is carried out.<br>The mode switches to the position control mode when the software stroke limit range is exceeded, and the operation immediately stops. |

*In the original, "Control type" spans 3 columns (2nd-level cells without a 3rd level are merged over columns 2-3; "—" here). First-level cells and "Machine home position return control"/"Position control"/"Other control" are merged vertically. In "Processing at check": "Check not carried out." is merged over the 2 rows "Other than 'Data set method'" and "Fast home position return control"; the "Checks 1) and 2) ..." cell is merged over the 7 rows from 1-axis linear control to Speed-position switching control (written in full in the first row, "(same as above)" in the others); the Manual control cell is merged over its 2 rows. Expanded to each row.

*1 The value in "[Md.20] Command position value" will differ according to the "[Pr.21] Command position value during speed control" setting.
*2 When the unit is "degree", check is not made during speed control.
*3 When the unit is "degree", check is not carried out.

#### Precautions during software stroke limit check (ソフトウェアストロークリミットチェック上の注意事項) (7.4 / original p.249)

- A machine home position return must be executed beforehand for the "software stroke limit function" to function properly.
- During interpolation control, a stroke limit check is carried out for the every current value of both the reference axis and the interpolation axis. Every axis will not start if an error occurs, even if it only occurs in one axis.
- During 2-axis circular interpolation control, the "[Pr.12] Software stroke limit upper limit value"/"[Pr.13] Software stroke limit lower limit value" may be exceeded. In this case, a deceleration stop will not be carried out even if the stroke limit is exceeded. Always install an external limit switch if there is a possibility the stroke limit will be exceeded.

Ex.

[Figure] 2-axis circular interpolation exceeding the stroke limit (original p.249)
- Axis 2 (horizontal) / Axis 1 (vertical). The arc goes from the Starting address (origin) through the Arc address ([Da.7]) to the End point address ([Da.6]).
- The arc top exceeds the "Axis 1 stroke limit" (dashed line): "Deceleration stop is not carried out."

> **Point**
> The software stroke limit check is carried out for the following addresses during 2-axis circular interpolation control.
> (Note that "[Da.7] Arc address" is carried out only for 2-axis circular interpolation control with sub point designation.)
> Current value/end point address ([Da.6])/arc address ([Da.7])

- If an error is detected during continuous path control, the axis stops immediately on completion of execution of the positioning data located right before the positioning data in error.

Ex.
If the positioning address of positioning data No.13 is outside the software stroke limit range, the operation immediately stops after positioning data No.12 has been executed.

[Figure] Immediate stop at error detection during continuous path control (original p.249)
- Positioning data: No.10 P11, No.11 P11, No.12 P11, No.13 P11, No.14 P01.
- Speed pattern: No.10 → No.11 → No.12 run continuously; at the end of No.12 the speed drops vertically to 0 ("Immediate stop at error detection"); No.13 is not executed.
- [Md.26] Axis operation status: "Position control" during No.10 to No.12 → "Error" at the stop.

- During simultaneous start, a stroke limit check is carried out for the current values of every axis to be started. Every axis will not start if an error occurs, even if it only occurs in one axis.

#### Setting method (設定方法) (7.4 / original p.250)

To use the "software stroke limit function", set the required values in the parameters shown in the following table, and write them to the Simple Motion module/Motion module.
The set details are validated at the rising edge (OFF → ON) of the "[Cd.190] PLC READY".

| Setting item | | Setting value | Setting details | Factory-set initial value |
|---|---|---|---|---|
| [Pr.12] | Software stroke limit upper limit value | → | Set the upper limit value of the moveable range. | 2147483647 |
| [Pr.13] | Software stroke limit lower limit value | → | Set the lower limit value of the moveable range. | -2147483648 |
| [Pr.14] | Software stroke limit selection | → | Set whether to use the "[Md.20] Command position value" or "[Md.21] Machine feed value" as the "current value". | 0: Command position value |
| [Pr.15] | Software stroke limit valid/invalid setting | 0: Valid | Set whether the software stroke limit is validated or invalidated during manual control (JOG operation, Inching operation, manual pulse generator operation). | 0: Valid |

Refer to the following for the setting details.
→Page 444 Basic Setting

#### Invalidating the software stroke limit (ソフトウェアストロークリミットを無効にするには) (7.4 / original p.250)

To invalidate the software stroke limit, set the following parameters as shown, and write them to the Simple Motion module/Motion module. (Set the value within the setting range.)
(To invalidate only the manual operation, set "1: software stroke limit invalid" in the "[Pr.15] Software stroke limit valid/invalid setting".)
The set details are validated at the rising edge (OFF → ON) of the "[Cd.190] PLC READY".
When the unit is "degree", the software stroke limit check is not performed during speed control (including speed control in speed-position switching control or position-speed switching control) or during manual control, independently of the values set in [Pr.12], [Pr.13] and [Pr.15].

*Note: the original does not show a parameter table under "Invalidating the software stroke limit" in this English edition (only the text above). Transcribed as printed.

> **Point**
> - Parameters are set for each axis.
> - It is recommended that the parameters be set whenever possible with the engineering tool. Execution by a program uses many programs and devices. The execution becomes complicated, and the scan times will increase.

#### Setting when the control unit is "degree" (制御単位が「degree」の場合の設定) (7.4 / original p.251)

##### Current value address (現在値のアドレス) (7.4 / original p.251)

The "[Md.20] Command position value" address is a ring address between 0 and 359.99999°.

[Figure] Ring address (original p.251)
- Sawtooth: the value rises from 0° to 359.99999°, then returns to 0° and rises again (repeated).

##### Setting the software stroke limit (ソフトウェアストロークリミットの設定) (7.4 / original p.251)

The upper limit value/lower limit value of the software stroke limit is a value between 0 and 359.99999°.
- Setting when the software stroke limit is to be validated.

When the software stroke limit is to be validated, set the upper limit value in a clockwise direction from the lower limit value.

[Figure] Section A / Section B on a circle (original p.251)
- Lower limit at 315°, "Set in a clockwise direction" to the Upper limit at 90°: the arc from 315° clockwise to 90° (through 0°) is Section A.
- The remaining arc from 90° to 315° is Section B.

Set as follows to set the movement range of section A or B in the above figure.

| Section set as movement range | Software stroke limit lower limit value | Software stroke limit upper limit value |
|---|---|---|
| Section A | 315.00000° | 90.00000° |
| Section B | 90.00000° | 315.00000° |

### Hardware stroke limit function (ハードウェアストロークリミット機能) (7.4 / original p.252-255)

> **WARNING**
> - When the hardware stroke limit is required to be wired, ensure to wire it in the negative logic using b-contact. If it is set in positive logic using a-contact, a serious accident may occur.

In the "hardware stroke limit function", limit switches are set at the upper/lower limit of the physical moveable range, and the control is stopped (by deceleration stop) by the input of a signal from the limit switch.
Damage to the machine can be prevented by stopping the control before the upper/lower limit of the physical moveable range is reached.
The hardware stroke limit is able to use the following signals. (→Page 469 [Pr.116] to [Pr.119] FLS/RLS/DOG/STOP signal selection)
- External input signal of servo amplifier
- External input signal via CPU (buffer memory of Simple Motion module/Motion module)
- Input signal on the CC-Link IE TSN network (link device) [FX5-SSC-G]

#### Control details (制御内容) (7.4 / original p.252-254)

The following drawing shows the operation of the hardware stroke limit function.

##### External input signal of servo amplifier (サーボアンプの外部入力信号の場合) (7.4 / original p.252-253)

[FX5-SSC-S]

[Figure] Hardware stroke limit with external input signal of servo amplifier [FX5-SSC-S] (original p.252)
- Mechanical stoppers at both ends; Lower limit switch and Upper limit switch inside them; "Control range of Simple Motion module" is from the Lower limit to the Upper limit.
- Start → movement toward the lower limit → "Deceleration stop at lower limit switch detection" (stops beyond the lower limit, before the mechanical stopper). Same for the upper side: "Deceleration stop at upper limit switch detection".
- Both limit switches are wired to the Servo amplifier, which is connected to the Simple Motion module via SSCNETⅢ(/H).

[FX5-SSC-G] (original p.253)
For the operation of the servo amplifier at stroke limit detection, check the specifications of the servo amplifier to use.
The example below uses MR-J5(W)-G.

[Figure] Hardware stroke limit with external input signal of servo amplifier [FX5-SSC-G] (original p.253)
- Same layout as the [FX5-SSC-S] figure; "Control range of Motion module" from Lower limit to Upper limit.
- "Deceleration stop at lower limit switch detection*3" / "Deceleration stop at upper limit switch detection*3"; "Lower limit switch*2" / "Upper limit switch*2" wired to the "Servo amplifier*1", which is connected to the Motion module via CC-Link IE TSN Network.

*1 Be sure to set the following servo parameters correctly.
- Set servo parameter "Function selection D-4 Sensor input method selection (PD41.3)" to "1: Input from controller". When set to a different value, the error "Servo parameter invalid" (error code: 1DC8H) occurs and the controller rewrites the value of "Function selection D-4 Sensor input method selection (PD41.3)" to "1: Input from controller". The servo parameter is enabled after the servo amplifier is reset.
- Assign the LSP/LSN signal in servo parameters "Input device selection 1 to 3 (PD03 to PD05)"

*2 The signal to be wired changes depending on the setting of servo parameter "Travel direction selection (PA14)".

| "Travel direction selection (PA14)" | Name of servo amplifier signal: Lower limit | Name of servo amplifier signal: Upper limit |
|---|---|---|
| 0: Forward rotation (CCW) with the increase of the positioning address | LSN | LSP |
| 1: Reverse rotation (CW) with the increase of the positioning address | LSP | LSN |

*In the original, "Name of servo amplifier signal" is a 2-level header over "Lower limit" and "Upper limit". Flattened into the column names.

*3 Stop processing is carried out in the Motion module.

##### External input signal via CPU (buffer memory of Simple Motion module/Motion module) (CPU経由外部入力信号(シンプルモーションユニット／モーションユニットのバッファメモリ)の場合) (7.4 / original p.253)

[Figure] Hardware stroke limit with external input signal via CPU (original p.253)
- Same layout; "Control range of Simple Motion module/Motion module" from Lower limit to Upper limit; Deceleration stop at lower/upper limit switch detection.
- Lower limit switch and Upper limit switch are wired to the CPU module side (the input module of the CPU module to which the Simple Motion module/Motion module is attached).

[FX5-SSC-G]
Be sure to set the servo parameters correctly. For details, refer to the following.
→Page 850 Devices Compatible with CC-Link IE TSN [FX5-SSC-G]

##### Link device [FX5-SSC-G] (リンクデバイスの場合[FX5-SSC-G]) (7.4 / original p.254)

[Figure] Hardware stroke limit with link device (original p.254)
- Same layout; "Control range of Motion module"; Lower limit switch and Upper limit switch are wired to a Remote I/O station, connected to the Motion module via CC-Link IE TSN Network.

Set the servo parameters and the link device external signal assignment parameters appropriately. For details, refer to the following.
→Page 850 Devices Compatible with CC-Link IE TSN [FX5-SSC-G]
→Page 329 Link Device External Signal Assignment Function [FX5-SSC-G]

#### Wiring the hardware stroke limit (ハードウェアストロークリミットの配線) (7.4 / original p.254-255)

When using the hardware stroke limit function, wire the terminals corresponding to the upper/lower stroke limit of the device to be used as shown in the following drawing.
[FX5-SSC-G]
For the setting method of the input logic for the upper/lower stroke limit, refer to the following.
→Page 323 Input logic setting method for external input signals

##### External input signal of the servo amplifier (サーボアンプの外部入力信号の場合) (7.4 / original p.254)

Refer to the manuals of each servo amplifier to be used for details on input and wiring of the signal.
[FX5-SSC-S]
Wire MR-J3(W)-B, MR-J4(W)-B, and MR-J5(W)-B as shown in the following drawing. As for the 24 V DC power supply, the polarity of current can be switched.

Ex.
When "[Pr.22] Input signal logic selection" is set to the initial value

[Figure] Wiring of FLS/RLS to the servo amplifier (original p.254)
- Servo amplifier terminals: DI1 (FLS), DI2 (RLS), DICOM.
- DI1 (FLS) and DI2 (RLS) are each connected through a limit switch contact (b-contact) to a common line; the common line connects through a 24 V DC power supply to DICOM.

[FX5-SSC-G]
Check the specifications of the servo amplifier to be connected before performing wiring and setting.

##### External input signal via CPU (buffer memory of the Simple Motion module/Motion module) (CPU経由外部入力信号(シンプルモーションユニット／モーションユニットのバッファメモリ)の場合) (7.4 / original p.254)

For the wiring, refer to the manual of the module into which the external input signal is to be input.
At MR-JE-B(F) use, refer to the following.
→Page 823 Connection with MR-JE-B(F)

##### Link device [FX5-SSC-G] (リンクデバイスの場合[FX5-SSC-G]) (7.4 / original p.254)

For the wiring, refer to the manual of the device station to be used.

> **Point** (original p.255)
> Wire the limit switch installed in the direction to which "Command position value" increases as upper limit switch and the limit switch installed in the limit switch installed in the direction to which "Command position value" decreases as lower limit switch.
> If inverting the install positions of upper/lower limit switches, hardware stroke limit function cannot be operated properly. In addition, the servo motor does not stop.
> The increase/decrease of "Command position value" and the motor rotation direction/movement direction can be changed by the parameters depending on the servo amplifier. Refer to the manuals of each servo amplifier for details.

#### When the hardware stroke limit function is not used (ハードウェアストロークリミット機能を使用しない場合) (7.4 / original p.255)

Set the logic of FLS and RLS to the "negative logic" (initial value) with "[Pr.22] Input signal logic selection" and input the signal which always turns ON. Otherwise, set the logic of FLS and RLS to the "positive logic" with "[Pr.22] Input signal logic selection" and always turn OFF the input.

#### Precautions during control (制御上の注意事項) (7.4 / original p.255)

- If the machine is stopped outside the Simple Motion module/Motion module control range (outside the upper/lower limit switches), or if stopped by hardware stroke limit detection, the starting for the "home position return control", "major positioning control", and "high-level positioning control" and the control mode switching cannot be executed. To carry out these types of control again, return the workpiece to the Simple Motion module/Motion module control range by a "JOG operation", "inching operation" or "manual pulse generator operation".

[FX5-SSC-S]
- When "[Pr.22] Input signal logic selection" or "[Pr.150] Input terminal logic selection" is set to the initial value, the Simple Motion module cannot carry out the positioning control if FLS (limit switch for upper limit) is separated from DICOM or RLS (limit switch for lower limit) is separated from DICOM (including when wiring is not carried out).

[FX5-SSC-G]
- When "[Pr.22] Input signal logic selection" is set to the initial value, the Motion module cannot carry out the positioning control if FLS (limit switch for upper limit) is separated from DICOM or RLS (limit switch for lower limit) is separated from DICOM (including when wiring is not carried out).

### Forced stop function (強制停止機能) (7.4 / original p.256-258)

> **WARNING**
> - When the forced stop is required to be wired, ensure to wire it in the negative logic using b-contact. [FX5-SSC-S]
> - When the forced stop is required to be wired, take the following measures. [FX5-SSC-G]
>   When using other than the link device for the forced stop input:
>   Ensure to wire in the negative logic using b-contact.
>   When using the link device for the forced stop input:
>   Wire according to "[Pr.903] Forced stop signal (EMI): Link device logic setting". It is recommended to set "0: Negative logic" in "[Pr.903] Forced stop signal (EMI): Link device logic setting" and wire in the negative logic using b-contact.
> - Provided safety circuit outside the Simple Motion module/Motion module so that the entire system will operate safety even when the "[Pr.82] Forced stop valid/invalid selection" is set "1: Invalid". Be sure to use the forced stop signal (EMI) of the servo amplifier.

"Forced stop function" stops all axes of the servo amplifier with the forced stop signal. (The initial value is "0: Valid (External input signal)" [FX5-SSC-S], or "1: Invalid" [FX5-SSC-G].)
The forced stop input valid/invalid is selected by "[Pr.82] Forced stop valid/invalid selection".

#### Control details (制御内容) (7.4 / original p.256-257)

When "[Pr.82] Forced stop valid/invalid selection" is set to other than "1: Invalid", the forced stop signal is sent to all axes after the forced stop input is turned on.
Refer to the manuals of each servo amplifier for the operation of the servo amplifier after the forced stop signal is sent.
[FX5-SSC-G]
When "[Pr.82] Forced stop valid/invalid selection" is set to other than "1: Invalid", the "Quick stop" defined in CiA 402 is issued to all servo amplifier axes after the forced stop input is turned on.
Refer to the servo amplifier manual for the operation of the servo amplifier when the "Quick stop" is issued.
For MR-J5(W)-G: [Other manual] MR-J5 User's Manual (Function)

##### Forced stop processing (強制停止処理) (7.4 / original p.256)

| Stop cause | | Stop axis | M code ON signal after stop | Axis operation status ([Md.26]) after stopping | Stop process: Machine home position return control / Fast home position return control / Major positioning control / High-level positioning control / JOG/Inching operation | Stop process: Manual pulse generator operation |
|---|---|---|---|---|---|---|
| Forced stop | "Forced stop input signal" OFF [FX5-SSC-S] | All axes | No change | Servo OFF | Immediate stop | — |
| Forced stop | "[Cd.158] Forced stop input" OFF [FX5-SSC-G] | All axes | No change | Servo OFF | Immediate stop | — |

*In the original, the "Stop process" header spans "Home position return control (Machine home position return control / Fast home position return control)", "Major positioning control", "High-level positioning control" and "Manual control (JOG/Inching operation / Manual pulse generator operation)". "Immediate stop" is one cell merged horizontally over the 5 columns from Machine home position return control to JOG/Inching operation (collapsed into one column here). "Forced stop", "All axes", "No change", "Servo OFF", "Immediate stop" and "—" are merged vertically over the 2 rows. Expanded to each row.

The following drawing shows the operation of the forced stop function. (original p.257)

##### Operation example (動作例) (7.4 / original p.257)

- [FX5-SSC-S]

[Figure] Forced stop operation example [FX5-SSC-S] (original p.257)
- Signals: Each operation, [Cd.190] PLC READY, [Cd.191] All axis servo ON, [Cd.184] Positioning start, Forced stop input (Input voltage of EMI), [Md.50] Forced stop input, [Md.108] Servo status1 (b1: Servo ON), [Pr.82] Forced stop valid/invalid selection.
- [Pr.82] = 0 throughout ("Forced stop valid").
- PLC READY ON → All axis servo ON ON → [Md.108] b1 Servo ON = ON; [Md.50] = 1. Positioning start ON → operation starts.
- "Forced stop causes occurrence": the forced stop input (EMI voltage) turns OFF → the operation stops, [Md.50] becomes 0, [Md.108] b1 becomes OFF. Afterwards [Cd.191] and [Cd.184] are turned OFF (and later PLC READY OFF).
- The forced stop input is restored (ON) → [Md.50] returns to 1; [Md.108] b1 stays OFF until [Cd.191] All axis servo ON is turned ON again (PLC READY ON again, then servo ON) → b1 ON.
- 2nd operation, 2nd "Forced stop causes occurrence": forced stop input OFF → [Md.50] 0, b1 OFF (PLC READY and All axis servo ON remain ON in this case); forced stop input restored → [Md.50] 1 and b1 returns to ON (servo ON follows [Cd.191], which is still ON). [Cd.184] turns OFF after the stop.

- [FX5-SSC-G]

[Figure] Forced stop operation example [FX5-SSC-G] (original p.257)
- Same as [FX5-SSC-S] except the forced stop input is "Forced stop input ([Cd.158] Forced stop input)". Timings and values ([Md.50] 1→0→1→0→1, [Md.108] b1 ON→OFF→ON→OFF→ON, [Pr.82] = 0 "Forced stop valid") are drawn identically.

*Note: [Pr.82] is drawn as "0" in the [FX5-SSC-G] chart as well, although "0: Valid (External input signal)" is an [FX5-SSC-S] setting. Transcribed as printed (要確認).

#### Wiring the forced stop [FX5-SSC-S] (緊急停止の配線[FX5-SSC-S]) (7.4 / original p.257)

When using the forced stop function, wire the terminals of the Simple Motion module forced stop input as shown in the following drawing. As for the 24 V DC power supply, the polarity of current can be switched.

[Figure] Forced stop input wiring (original p.257)
- Simple Motion module terminals EMI and EMI.COM (internal photocoupler input circuit).
- EMI → forced stop switch (b-contact) → 24 V DC power supply → EMI.COM.

#### Setting the forced stop (緊急停止の設定方法) (7.4 / original p.258)

To use the "Forced stop function", set the following data using a program.
The set details are validated at the rising edge (OFF → ON) of the "[Cd.190] PLC READY".
Refer to the following for the setting details.
→Page 444 Basic Setting

| Setting item | | Setting value | Setting details | | Buffer memory address |
|---|---|---|---|---|---|
| [Pr.82] | Forced stop valid/invalid selection | → | Set the forced stop function. | | 35 |
| [Pr.82] | Forced stop valid/invalid selection | → | 0: Valid (External input signal) [FX5-SSC-S] | Forced stop from the external input signal is used | 35 |
| [Pr.82] | Forced stop valid/invalid selection | → | 1: Invalid | Forced stop is not used | 35 |
| [Pr.82] | Forced stop valid/invalid selection | → | 2: Valid (Buffer memory) [FX5-SSC-G] | Forced stop from the buffer memory is used | 35 |
| [Pr.82] | Forced stop valid/invalid selection | → | 3: Valid (Link device) [FX5-SSC-G] | Forced stop from the link device is used | 35 |
| [Cd.158] | Forced stop input [FX5-SSC-G] | → | Set the forced stop information in the buffer memory. | | 5945 |
| [Cd.158] | Forced stop input [FX5-SSC-G] | → | 0: Forced stop ON (Forced stop)*1 | Forced stop | 5945 |
| [Cd.158] | Forced stop input [FX5-SSC-G] | → | 1: Forced stop OFF (Forced stop release) | Forced stop is released | 5945 |

*In the original, "Setting details" has one row spanning both sub-columns ("Set the forced stop function." / "Set the forced stop information in the buffer memory.") followed by value/meaning rows; "[Pr.82]", "Forced stop valid/invalid selection", "→" and "35" are merged vertically over 5 rows, and "[Cd.158]", "Forced stop input [FX5-SSC-G]", "→" and "5945" over 3 rows. Expanded to each row.

*1 When a value other than "1" is set, the value is considered as being "0".

[FX5-SSC-G]
- "[Cd.158] Forced stop input" is valid only when "[Pr.82] Forced stop valid/invalid selection" is set to "2: Valid (Buffer memory)".
- When "[Pr.82] Forced stop valid/invalid selection" is set to "3: Valid (Link device)," set the link device external signal assignment function.

#### How to check the forced stop (緊急停止の確認方法) (7.4 / original p.258)

To use the states (ON/OFF) of forced stop input, set the parameters shown in the following table.

| Monitor item | | Monitor value | Storage details | Buffer memory address |
|---|---|---|---|---|
| [Md.50] | Forced stop input | → | Stores the states (ON/OFF) of forced stop input.<br>0: Forced stop input ON (Forced stop)<br>1: Forced stop input OFF (Forced stop release) | 4231 |

Refer to the following for the setting details.
→Page 518 Monitor Data

#### Precautions during control (制御上の注意事項) (7.4 / original p.258)

- After the "Forced stop input" is released, the servo ON/OFF is valid for the status of "[Cd.191] All axis servo ON".
- If the setting value of "[Pr.82] Forced stop valid/invalid selection" is outside the range, the error "Forced stop valid/invalid setting error" (error code: IB71H [FX5-SSC-S], or error code: 1DC1H [FX5-SSC-G]) occurs.
- The "[Md.50] Forced stop input" is stored "1" by setting "[Pr.82] Forced stop valid/invalid selection" to "1: invalid".
- When the "Forced stop input" is turned ON during operation, the error "Servo READY signal OFF during operation" (error code: 1902H [FX5-SSC-S], or error code: 1A02H [FX5-SSC-G]) does not occur.
- The status of the signal that is not selected in "[Pr.82] Forced stop valid/invalid selection" is ignored.

*Note: the original prints "IB71H" (letter I); likely 1B71H. Transcribed as printed (要確認).

[FX5-SSC-G]
- Errors cannot be cleared with "[Cd.5] Axis error reset" during a forced stop. Clear the errors after the forced stop is released.
- The error "Driver command discard detection" (error code: 1BE6H) may occur before servo OFF when "[Cd.158] Forced stop input" is set to "0000H: Forced stop ON (Forced stop)" during operation with "[Pr.140] Driver command discard detection setting" set to "1: Detection enabled".

## 7.5 Functions to Change the Control Details (制御内容を変更する機能) (7.5 / original p.259-277)

Functions to change the control details include the "speed change function", "override function", "acceleration/deceleration time change function", "torque change function" and "target position change function". Each function is executed by parameter setting or program creation and writing.
Refer to "Combination of Main Functions and Sub Functions" in the following manual for combination with main function.
[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Startup)
Both the "speed change function" or "override function" change the speed, but the differences between the functions are shown below. Use the function that corresponds to the application.
"Speed change function"
- The speed is changed at any time, only in the control being executed.
- The new speed is directly set.

"Override function"
- The speed is changed for all control to be executed.
- The new speed is set as a percent (%) of the command speed.

> **Point**
> "Speed change function" and "Override function" cannot be used in the manual pulse generator operation and speed-torque control.

### Speed change function (速度変更機能) (7.5 / original p.259-263)

The speed control function is used to change the speed during control to a newly designated speed at any time.
The new speed is directly set in the buffer memory, and the speed is changed by a speed change command ([Cd.15] Speed change request) or external command signal.
During the machine home position return, a speed change to the creep speed cannot be carried out after deceleration start because the proximity dog ON is detected. When the speed change function is enabled and the speed is slower than the creep speed, the speed change is disabled and the speed accelerates to the creep speed after the proximity dog ON is detected.

*Note: the original says "The speed control function is used to change the speed ..." at the start of the "Speed change function" section (as printed).

#### Control details (制御内容) (7.5 / original p.259)

The following drawing shows the operation during a speed change.

[Figure] Operation during a speed change (original p.259)
- The axis accelerates and runs at V1.
- "Speed changes to V2.": the speed decelerates from V1 to V2 (the dashed line continuing at V1 is "Operation during positioning by V1.").
- "Speed changes to V3.": the speed decelerates from V2 to V3, then the axis stops.
- [Md.40] In speed change processing flag: 0 → 1 during the change V1→V2 → 0 → 1 during the change V2→V3 → 0.

#### Precautions during control (制御上の注意事項) (7.5 / original p.260-261)

- At the speed change during continuous path control, when no speed designation (current speed) is provided in the next positioning data, the next positioning data is controlled at the "[Cd.14] New speed value". Also, when a speed designation is provided in the next positioning data, the next positioning data is controlled at its "[Da.8] Command speed".

[Figure] Speed change during continuous path control (original p.260)
- Horizontal: "Positioning control P1" then "Next control P2".
- Levels (top to bottom): [Cd.14] New speed value, Designated speed in P2, Designated speed in P1.
- The axis runs at the designated speed in P1; at the "Speed change command" it accelerates to the [Cd.14] New speed value.
- At the change to P2: [a] When no speed designation (current speed) is provided — the speed stays at [Cd.14] New speed value. [b] When a speed designation is provided — the speed decelerates to the designated speed in P2.

- When changing the speed during continuous path control, the speed change will be ignored if there is not enough distance remaining to carry out the change.
- When the stop command is given to make a stop after a speed change that has been made during position control, the restarting speed depends on the "[Cd.14] New speed value".

[Figure] Restart after a speed change and stop (original p.260)
- The axis runs at [Da.8] Command speed; at the "Speed change command" it decelerates to [Cd.14] New speed value.
- At the "Stop command" the axis decelerates to stop.
- At the "Restarting command" the axis accelerates to the [Cd.14] New speed value (not to [Da.8] Command speed).

- When the speed is changed by setting "[Cd.14] New speed value" to "0", the operation is carried out as follows.
  - When "[Cd.15] Speed change request" is turned ON, the speed change 0 flag ([Md.31] Status: b10) turns ON. (During interpolation control, the speed change 0 flag on the reference axis side turns ON.)
  - The axis stops, but "[Md.26] Axis operation status" does not change, and the BUSY signal remains ON. (If a stop signal is input, the BUSY signal will turn OFF, and "[Md.26] Axis operation status" will change to "stopped".) In this case, setting the "[Cd.14] New speed value" to a value besides "0" will turn OFF the speed change 0 flag ([Md.31] Status: b10), and enable continued operation.
  - Operation example

[Figure] Speed change with [Cd.14] New speed value = 0 (original p.260)
- [Cd.184] Positioning start OFF → ON → [Md.141] BUSY OFF → ON; positioning operation accelerates and runs.
- [Cd.14] New speed value = 0; [Cd.15] Speed change request OFF → ON (short pulse) → the positioning operation decelerates to 0 and the speed change 0 flag ([Md.31] status: b10) turns OFF → ON. BUSY stays ON.
- [Cd.14] New speed value changes 0 → 1000; then [Cd.15] Speed change request ON (pulse) → the speed change 0 flag turns OFF and the positioning operation accelerates again.
- After the positioning ends, [Md.141] BUSY turns OFF, then [Cd.184] Positioning start turns OFF.

- The warning "Deceleration/stop speed change" (warning code: 0990H [FX5-SSC-S], or warning code: 0D50H [FX5-SSC-G]) occurs and the speed cannot be changed in the following cases.
  - During deceleration by a stop command
  - During automatic deceleration during positioning control
- The warning "Speed limit value over" (warning code: 0991H [FX5-SSC-S], or warning code: 0D51H [FX5-SSC-G]) occurs and the speed is controlled at the "[Pr.8] Speed limit value" when the value set in "[Cd.14] New speed value" is larger than the "[Pr.8] Speed limit value".
- When the speed is changed during interpolation control, the required speed is set in the reference axis.
- When carrying out consecutive speed changes, be sure there is an interval between the speed changes of 10 ms or more. (If the interval between speed changes is short, the Simple Motion module/Motion module will not be able to track, and it may become impossible to carry out commands correctly.)
- When a speed change is requested simultaneously for multiple axes, change the speed one by one. Therefore, the start timing of speed change is different for each axis.
- Speed change cannot be carried out during the machine home position return. A request for speed change is ignored.
- When deceleration is started by the speed change function, the deceleration start flag does not turn ON.
- The speed change function cannot be used during speed control mode, torque control mode or continuous operation to torque control mode. Refer to the following for the speed change during speed control mode or continuous operation to torque control mode.
  →Page 186 Speed-torque Control

#### Setting method from the CPU module (CPUユニットからの設定方法) (7.5 / original p.261)

The following shows the data settings and program example for changing the control speed of axis 1 by the command from the CPU module. (In this example, the control speed is changed to "20.00 mm/min".)
- Set the following data. (Set using the program referring to the speed change time chart.)

n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.14] | New speed value | 2000 | Set the new speed. | 4314+100n<br>4315+100n |
| [Cd.15] | Speed change request | 1 | Set "1: Change the speed". | 4316+100n |

Refer to the following for the setting details.
→Page 561 Control Data
- The following shows the speed change time chart.

##### Operation example (動作例) (7.5 / original p.261)

[Figure] Speed change time chart from the CPU module (original p.261)
- [Cd.190] PLC READY ON → [Cd.191] All axis servo ON ON → READY signal ([Md.140] Module status: b0) ON.
- [Cd.184] Positioning start ON → Start complete signal ([Md.31] Status: b14) and [Md.141] BUSY turn ON; the axis accelerates and runs.
- [Cd.14] New speed value changes 0 → 2000; then [Cd.15] Speed change request 0 → 1 → 0 (returns to 0).
- At the speed change, [Md.40] In speed change processing flag 0 → 1 → 0, and the speed decelerates to the new (lower) speed.
- After the positioning ends and the dwell time, [Md.141] BUSY turns OFF and the positioning complete signal ([Md.31] Status: b15) turns ON, then OFF.
- [Cd.184] Positioning start turns OFF, then the start complete signal (b14) turns OFF.
- Error detection signal ([Md.31] Status: b13) stays OFF.

##### Program example (プログラム例) (7.5 / original p.261)

Refer to the following for the program example of the speed change program.
→Page 635 Speed change program [FX5-SSC-S]
→Page 709 Speed change program [FX5-SSC-G]

#### Setting method using an external command signal (外部指令信号を使った設定方法) (7.5 / original p.262-263)

The speed can also be changed using an "external command signal".
The following shows the data settings and program example for changing the control speed of axis 1 using an "external command signal". (In this example, the control speed is changed to "10000.00 mm/min".)
- Set the following data to change the speed using an external command signal. (Set using the program referring to the speed change time chart.)

n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Pr.42] | External command function selection | 1 | Set "1: External speed change request". | 62+150n |
| [Cd.8] | External command valid | 1 | Set "1: Validates an external command". | 4305+100n |
| [Cd.14] | New speed value | 1000000 | Set the new speed. | 4314+100n<br>4315+100n |

Set the external command signal (D1) in "[Pr.95] External command signal selection".
Refer to the following for the setting details.
→Page 444 Basic Setting, →Page 561 Control Data
- The following shows the speed change time chart.

*Note: the original prints "(D1)"; this presumably means "(DI)". Transcribed as printed.

##### Operation example (動作例) (7.5 / original p.262)

[Figure] Speed change time chart using an external command signal (original p.262)
- [Cd.190] PLC READY ON → [Cd.191] All axis servo ON ON → READY signal ([Md.140] Module status: b0) ON.
- [Pr.42] External command function selection = 1 (set before the start).
- [Cd.184] Positioning start ON → Start complete signal ([Md.31] Status: b14) and [Md.141] BUSY turn ON; the axis accelerates and runs.
- After the start, [Cd.14] New speed value changes 0 → 1000000 and [Cd.8] External command valid is set to 1.
- External command signal ON (short pulse) → [Md.40] In speed change processing flag 0 → 1 → 0 and the speed changes (decelerates) to the new speed. Afterwards [Cd.8] External command valid changes from 1 (to 0).
- After the positioning ends and the dwell time, [Md.141] BUSY turns OFF and the positioning complete signal ([Md.31] Status: b15) turns ON, then OFF.
- [Cd.184] Positioning start turns OFF, then the start complete signal (b14) turns OFF.
- Error detection signal ([Md.31] Status: b13) stays OFF.

##### Program example (プログラム例) (7.5 / original p.263)

Add the following program to the control program, and write it to the CPU module.

[Figure] Program example of speed change using an external command signal (ladder with labels) (original p.263)
- Step numbers: (0)

Mnemonic transcription (label names as in the original; the device shown under each module label in the ladder is given after `;`):

```text
(0)
LD    bInputExtChangeSpeedReq
DMOVP dChangeSpeedValue FX5SSC_1.stnAxCtrl1_D[0].udNewSpeed_D                   ; U1\G4314
MOVP  K1 FX5SSC_1.stnAxPrm_D[0].uExternalCommandFunctionMode_D                  ; U1\G62
MOVP  K1 FX5SSC_1.stnAxCtrl1_D[0].uExternalCommandValid_D                       ; U1\G4305
```

- Contact types (read from the figure): bInputExtChangeSpeedReq is an NO (a) contact. DMOVP / MOVP / MOVP are parallel outputs of the same condition.

| Classification | Label name | Description |
|---|---|---|
| Module label | FX5SSC_1.stnAxPrm_D[0].uExternalCommandFunctionMode_D | Axis 1 External command function selection |
| Module label | FX5SSC_1.stnAxCtrl1_D[0].uExternalCommandValid_D | Axis 1 External command valid |
| Module label | FX5SSC_1.stnAxCtrl1_D[0].udNewSpeed_D | Axis 1 New speed value |
| Global label, local label | (below) | Defines the global label or the local label as follows. The settings of Assign (Device/Label) are not required for the label that the assignment device is not set because the unused internal relay and data device are automatically assigned.<br>The following are for local labels. |

*In the original, "Module label" is merged over 3 rows. Expanded to each row.

Local label definition (transcribed from the screen image in the original):

| No. | Label Name | Data Type | Class |
|---|---|---|---|
| 1 | dChangeSpeedValue | Double Word [Unsigned]/Bit String [32-bit] | VAR |
| 2 | bInputExtChangeSpeedReq | Bit | VAR |

### Override function (オーバーライド機能) (7.5 / original p.264-266)

The override function changes the command speed by a designated percentage for all control to be executed.
The speed can be changed by setting the percentage (%) by which the speed is changed in "[Cd.13] Positioning operation speed override".
The setting range of "[Cd.13] Positioning operation speed override" differs depending on the model.

| Model | The setting range of "[Cd.13] Positioning operation speed override" |
|---|---|
| FX5-SSC-S | 1 to 300% |
| FX5-SSC-G | Version 1.001 or earlier: 1 to 300%<br>Version 1.002 or later: 0 to 300% |

#### Control details (制御内容) (7.5 / original p.264)

The following shows that operation of the override function.
- A value changed by the override function is monitored by "[Md.22] Speed command".
- If "[Cd.13] Positioning operation speed override" is set to 100%, the speed will not change.
- If "[Cd.13] Positioning operation speed override" is set with a value less than "100 (%)" and "[Md.22] Speed command" is less than "1", the warning "Less than minimum speed" (warning code: 0904H [FX5-SSC-S], or warning code: 0D04H [FX5-SSC-G]) occurs and "[Md.22] Speed command" is set with "1" in any speed unit.
- If there is not enough remaining distance to change the speed due to the "override function", when the speed is changed during the position control of speed-position switching control or position-speed switching control, the operation will be carried out at the speed that could be changed.
- If the speed changed by the override function is greater than the "[Pr.8] Speed limit value", the warning "Speed limit value over" (warning code: 0991H [FX5-SSC-S], or warning code: 0D51H [FX5-SSC-G]) will occur and the speed will be controlled at the "[Pr.8] Speed limit value". The "[Md.39] In speed limit flag" will turn ON.

[FX5-SSC-G]
- If "[Cd.13] Positioning operation speed override" is set to "0 (%)", the speed is set to "0" and the speed change 0 flag ([Md.31] Status: b10) is set to "1". At the time, the warning "Less than minimum speed" (warning code: 0D04H) does not occur.

##### Override function operation [FX5-SSC-S] (オーバーライド機能の動作[FX5-SSC-S]) (7.5 / original p.264)

[Figure] Override function operation [FX5-SSC-S] (original p.264)
- [Da.8] Command speed: 50 (constant).
- [Cd.13] Positioning operation speed override changes 100 → 1 → 50 → 150 → 100 → 200.
- [Md.22] Speed command correspondingly: 50 → 1 → 25 → 75 → (not changed during deceleration) → 50 → 75.
- The speed follows: 50, down to 1 (near 0), up to 25, up to 75; then deceleration to stop — "Not affected by the override value during deceleration." (the change 150 → 100 during deceleration does not affect it).
- Next positioning runs at 50; with override 200 near the end: "Not enough remaining distance could be secured, so operation is carried out at an increased speed." (the speed rises only briefly before stopping).

##### Override function operation [FX5-SSC-G] (オーバーライド機能の動作[FX5-SSC-G]) (7.5 / original p.264)

[Figure] Override function operation [FX5-SSC-G] (original p.264)
- [Da.8] Command speed: 50 (constant).
- [Cd.13] Positioning operation speed override changes 100 → 0 → 50 → 150 → 100 → 200.
- [Md.22] Speed command: 50 → 0 → 25 → 75 → (not changed during deceleration) → 50 → 75.
- Speed change 0 flag ([Md.31] Status: b10): ON while the override is 0 (speed 0), OFF when the override changes to 50.
- "Not affected by the override value during deceleration." and "Not enough remaining distance could be secured, so operation is carried out at an increased speed." — same as FX5-SSC-S.

#### Precaution during control (制御上の注意事項) (7.5 / original p.265)

- When changing the speed by the override function during continuous path control, the speed change will be ignored if there is not enough distance remaining to carry out the change.
- The warning "Deceleration/stop speed change" (warning code: 0990H [FX5-SSC-S], or warning code: 0D50H [FX5-SSC-G]) occurs and the speed cannot be changed by the override function in the following cases. (The value set in "[Cd.13] Positioning operation speed override" is validated after a deceleration stop.)
  - During deceleration by a stop command
  - During automatic deceleration during positioning control
- When the speed is changed by the override function during interpolation control, the required speed is set in the reference axis.
- When carrying out consecutive speed changes by the override function, be sure there is an interval between the speed changes of 10 ms or more. (If the interval between speed changes is short, the Simple Motion module/Motion module will not be able to track, and it may become impossible to carry out commands correctly.)
- When deceleration is started by the override function, the deceleration start flag does not turn ON.
- The override function cannot be used during speed control mode, torque control mode or continuous operation to torque control mode.
- The override function cannot be used during driver home position return.

[FX5-SSC-S]
- When a machine home position return is performed, the speed change by the override function cannot be carried out after a deceleration start to the creep speed following the detection of proximity dog ON. When the override is enabled during home position return and the speed is changed, the override is disabled and the speed accelerates to the creep speed after the proximity dog ON is detected.

#### Setting method (設定方法) (7.5 / original p.266)

The following shows the data settings and program example for setting the override value of axis 1 to "200%".
- Set the following data. (Set using the program referring to the speed change time chart.)

n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.13] | Positioning operation speed override | 200 | Set the new speed as a percentage (%). | 4313+100n |

Refer to the following for the setting details.
→Page 561 Control Data
- The following shows a time chart for changing the speed using the override function.

##### Operation example (動作例) (7.5 / original p.266)

[Figure] Speed change time chart using the override function (original p.266)
- [Cd.190] PLC READY ON → [Cd.191] All axis servo ON ON → READY signal ([Md.140] Module status: b0) ON.
- [Cd.184] Positioning start ON → Start complete signal ([Md.31] Status: b14) and [Md.141] BUSY turn ON; the axis accelerates and runs at the command speed.
- [Cd.13] Positioning operation speed override changes to 200 → the speed accelerates to the higher speed (double).
- After the positioning ends and the dwell time, [Md.141] BUSY turns OFF and the positioning complete signal ([Md.31] Status: b15) turns ON, then OFF.
- [Cd.184] Positioning start turns OFF, then the start complete signal (b14) turns OFF.
- Error detection signal ([Md.31] Status: b13) stays OFF.

##### Program example (プログラム例) (7.5 / original p.266)

Add the following program to the control program, and write it to the CPU module.
→Page 635 Override program [FX5-SSC-S]
→Page 709 Override program [FX5-SSC-G]

### Acceleration/deceleration time change function (加減速時間変更機能) (7.5 / original p.267-269)

The "acceleration/deceleration time change function" is used to change the acceleration/deceleration time during a speed change to a random value when carrying out the speed change by the "speed change function" and "override function".
In a normal speed change (when the acceleration/deceleration time is not changed), the acceleration/deceleration time previously set in the parameters ([Pr.9], [Pr.10], and [Pr.25] to [Pr.30] values) is set in the positioning parameter data items [Da.3] and [Da.4], and control is carried out with that acceleration/deceleration time. However, by setting the new acceleration/deceleration time ([Cd.10], [Cd.11]) in the control data, and issuing an acceleration/deceleration time change enable command ([Cd.12] Acceleration/deceleration time change value during speed change, enable/disable) to change the speed when the acceleration/deceleration time change is enabled, the speed will be changed with the new acceleration/deceleration time ([Cd.10], [Cd.11]).

#### Control details (制御内容) (7.5 / original p.267)

After setting the following two items, carry out the speed change to change the acceleration/deceleration time during the speed change.
- Set change value of the acceleration/deceleration time ("[Cd.10] New acceleration time value", "[Cd.11] New deceleration time value")
- Setting acceleration/deceleration time change to enable ("[Cd.12] Acceleration/deceleration time change value during speed change, enable/disable")

The following drawing shows the operation during an acceleration/deceleration time change.

[Figure] Operation during an acceleration/deceleration time change (original p.267)
- [For an acceleration/deceleration time change disable setting]: [Cd.12] Acceleration/deceleration time change value during speed change, enable/disable = Disabled throughout. At the [Cd.15] Speed change request the axis accelerates to the higher speed; the acceleration after the speed change and the final deceleration are "Operation with the acceleration/deceleration time set in [Da.3] and [Da.4]." (steep slopes).
- [For an acceleration/deceleration time change enable setting]: [Cd.12] changes Disabled → Enabled before the speed change. At the [Cd.15] Speed change request the acceleration after the speed change and the final deceleration are "Operation with the acceleration/deceleration time ([Cd.10] and [Cd.11]) set in the buffer memory." (gentler slopes).

#### Precautions during control (制御上の注意事項) (7.5 / original p.268-269)

- When "0" is set in "[Cd.10] New acceleration time value" and "[Cd.11] New deceleration time value", the acceleration/deceleration time will not be changed even if the speed is changed. In this case, the operation will be controlled at the acceleration/deceleration time previously set in the parameters.
- The "new acceleration/deceleration time" is valid during execution of the positioning data for which the speed was changed. In continuous positioning control and continuous path control, the speed is changed and control is carried out with the previously set acceleration/deceleration time at the changeover to the next positioning data, even if the acceleration/deceleration time is changed to the "new acceleration/deceleration time ([Cd.10], [Cd.11])".
- Even if the acceleration/deceleration time change is set to disable after the "new acceleration/deceleration time" is validated, the positioning data for which the "new acceleration/deceleration time" was validated will continue to be controlled with that value. (The next positioning data will be controlled with the previously set acceleration/deceleration time.)

Ex.

[Figure] Example: disabling after the new acceleration/deceleration time was validated (original p.268)
- Positioning start: the axis accelerates and runs (with [Cd.12] Disabled).
- [Cd.12] changes Disabled → Enabled; then a "Speed change" is made → the acceleration uses the "New acceleration/deceleration time ([Cd.10], [Cd.11])" (bold slope).
- [Cd.12] changes Enabled → Disabled; a second "Speed change" is still made with the new acceleration/deceleration time, and the final deceleration also uses the new acceleration/deceleration time (bold slopes).

- If the "new acceleration/deceleration time" is set to "0" and the speed is changed after the "new acceleration/deceleration time" is validated, the operation will be controlled with the previous "new acceleration/deceleration time".

Ex.

[Figure] Example: new acceleration/deceleration time set to 0 after validation (original p.268)
- [Cd.12] changes Disabled → Enabled; [Cd.10] New acceleration time value / [Cd.11] New deceleration time value = 0.
- First "Speed change" (with [Cd.10]/[Cd.11] = 0): "Controlled with the acceleration/deceleration time in the parameter."
- [Cd.10]/[Cd.11] change 0 → 1000; the second "Speed change" uses the "New acceleration/deceleration time ([Cd.10], [Cd.11])" (bold slope).
- [Cd.10]/[Cd.11] change 1000 → 0; the third "Speed change" and the final deceleration are still controlled with the new acceleration/deceleration time (bold slopes).

- The acceleration/deceleration change function cannot be used during speed control mode, torque control mode or continuous operation to torque control mode. Refer to the following for the acceleration/deceleration processing during speed control mode or continuous operation to torque control mode.
  →Page 186 Speed-torque Control

> **Point**
> If the speed is changed when an acceleration/deceleration change is enabled, the "new acceleration/deceleration time" will become the acceleration/deceleration time of the positioning data being executed. The "new acceleration/deceleration time" remains valid until the changeover to the next positioning data. (The automatic deceleration processing at the completion of the positioning will also be controlled by the "new acceleration/deceleration time".)

#### Setting method (設定方法) (7.5 / original p.269)

To use the "acceleration/deceleration time change function", write the data shown in the following table to the Simple Motion module/Motion module using the program.
The set details are validated when a speed change is executed after the details are written to the Simple Motion module/Motion module.
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.10] | New acceleration time value | → | Set the new acceleration time. | 4308+100n<br>4309+100n |
| [Cd.11] | New deceleration time value | → | Set the new deceleration time. | 4310+100n<br>4311+100n |
| [Cd.12] | Acceleration/deceleration time change value during speed change, enable/disable | 1 | Set "1: Acceleration/deceleration time change enable". | 4312+100n |

*"→" in the Setting value column is as printed in the original (value set by the user).

Refer to the following for the setting details.
→Page 561 Control Data

##### Program example (プログラム例) (7.5 / original p.269)

Add the following program to the control program, and write it to the CPU module.
→Page 635 Acceleration/deceleration time change program [FX5-SSC-S]
→Page 710 Acceleration/deceleration time change program [FX5-SSC-G]

### Torque change function (トルク変更機能) (7.5 / original p.270-273)

The "torque change function" is used to change the torque limit value during torque limiting.
The torque limit value at the control start is the value set in the "[Pr.17] Torque limit setting value" or "[Cd.101] Torque output setting value".
The following two change methods in the torque change function.

| Torque change function | Details |
|---|---|
| Forward/reverse torque limit value same setting | The forward torque limit value*1 and reverse torque limit value*2 are changed to the same value by the new torque value. (Use this method when they need not be separately set.) |
| Forward/reverse torque limit value individual setting | The forward torque limit value*1 and reverse torque limit value*2 are individually changed respectively by the forward new torque value and reverse new torque value. |

*1 Forward torque limit value: The limit value to the generated torque during CW regeneration at the CCW driving of the servo motor.
*2 Reverse torque limit value: The limit value to the generated torque during CCW regeneration at the CW driving of the servo motor.

Set previously "same setting" or "individual setting" of the forward/reverse torque limit value in "[Cd.112] Torque change function switching request". Set the new torque value (forward new torque value/reverse new torque value) in the axis control data ([Cd.22] or [Cd.113]) shown below.

| Torque change function | Setting items: Torque change function switching request ([Cd.112]) | Setting items: New torque value ([Cd.22], [Cd.113]) | |
|---|---|---|---|
| Forward/reverse torque limit value same setting | 0: Forward/reverse torque limit value same setting | [Cd.22] | New torque value/forward new torque value |
| Forward/reverse torque limit value same setting | 0: Forward/reverse torque limit value same setting | [Cd.113] | Setting invalid |
| Forward/reverse torque limit value individual setting | 1: Forward/reverse torque limit value individual setting | [Cd.22] | New torque value/forward new torque value |
| Forward/reverse torque limit value individual setting | 1: Forward/reverse torque limit value individual setting | [Cd.113] | New reverse torque value |

*In the original, "Setting items" is a header over the two sub-columns; "Torque change function" and "[Cd.112]" cells are merged over 2 rows each. Expanded to each row.

#### Control details (制御内容) (7.5 / original p.271-272)

The torque value (forward new torque value/reverse new torque value) of the axis control data can be changed at all times. The torque can be limited with a new torque value from the time the new torque value has been written to the Simple Motion module.
Note that the delay time until a torque control is executed is max. operation cycle after torque change value is written.
The toque limiting is not carried out from the time the power supply is turned ON to the time the "[Cd.190] PLC READY" is turned ON.
The new torque value ([Cd.22], [Cd.113]) is cleared to zero at the leading edge (OFF to ON) of the "[Cd.184] Positioning start at the start of JOG operation or synchronous control.
The torque setting range is from 0 to "[Pr.17] Torque limit setting value". (When the setting value is 0, a torque change is considered not to be carried out, and it becomes to the value set in "[Pr.17] Torque limit setting value" or "[Cd.101] Torque output setting value". The torque change range is 1 to "[Pr.17] Torque limit setting value".)
The following drawing shows the operation at the same setting and the operation at the individual setting for the forward new torque value and reverse new torque value.

*Note: "toque" and the unclosed quotation mark after "[Cd.184] Positioning start" are as printed in the original.

##### Operation example 1 (動作例1) (7.5 / original p.271)

[Figure] Torque change at the same setting ([Cd.112] = 0) (original p.271)
- Signals: Each operation, [Cd.190] PLC READY, [Cd.191] All axis servo ON, [Cd.184] Positioning start, [Pr.17] Torque limit setting value, [Cd.101] Torque output setting value, [Cd.112] Torque change function switching request, [Cd.22] New torque value/forward new torque value, [Md.35] Torque limit stored value/forward torque limit stored value.
- [Cd.112] Torque change function switching request = 0 throughout.
- Initially [Pr.17] = 300, [Cd.101] = 0, [Cd.22] = 0, [Md.35] = 0.
- [Cd.190] PLC READY ON, then [Cd.191] All axis servo ON ON → *1: [Md.35] = 300.
- 1st [Cd.184] Positioning start ON (operation starts) → *2: [Md.35] = 300 (updated; [Cd.101] = 0); *3: [Cd.22] cleared to 0.
- [Cd.22] = 200 → *4: [Md.35] = 200.
- [Cd.101] changes 0 → 100 during the operation (no immediate effect); [Pr.17] changes 300 → 250.
- [Cd.22] = 0 → *4, *5: no torque change ([Md.35] stays 200).
- [Cd.22] = 350 → *4, *6: exceeds the torque limit value, no torque change ([Md.35] stays 200).
- 2nd [Cd.184] Positioning start ON → *2: [Md.35] = 100 ([Cd.101] = 100); *3: [Cd.22] cleared to 0.
- [Cd.22] = 75 → *4: [Md.35] = 75. [Cd.101] changes 100 → 150.
- [Cd.22] = 230 → *4: [Md.35] = 230.
- [Cd.190] PLC READY and [Cd.191] All axis servo ON turn OFF, then ON again → *1 (Md.35 stays 230 in the chart).
- 3rd [Cd.184] Positioning start ON → *2: [Md.35] = 150 ([Cd.101] = 150); *3: [Cd.22] cleared to 0.

*1 The torque limit setting value or torque output setting value becomes effective at the rising edge of the "[Cd.190] PLC READY" (however, after the servo turned ON.)
If the torque output setting value is "0" or larger than the torque limit setting value, the torque limit setting value will be its value.
*2 The torque limit setting value or torque output setting value becomes effective at the rising edge of the "[Cd.184] Positioning start", and the torque limit value is updated.
If the torque output setting value is "0" or larger than the torque limit setting value, the torque limit setting value will be its value.
*3 The torque change value is cleared to "0" at the rising edge of the "[Cd.184] Positioning start".
*4 The torque limit value is changed by the torque changed value.
*5 When the new torque value is 0, a torque change is considered not to be carried out.
*6 When the change value exceeds the torque limit value, a torque change is considered not to be carried out.

##### Operation example 2 (動作例2) (7.5 / original p.272)

[Figure] Torque change at the individual setting ([Cd.112] = 1) (original p.272)
- Signals: as in Operation example 1, plus [Cd.113] New reverse torque value and [Md.120] Reverse torque limit stored value.
- [Cd.112] Torque change function switching request: 0 → 1 (after [Cd.190] PLC READY ON), stays 1, and returns to 0 at the 3rd positioning start.
- [Pr.17]: 300 → 250 (during the 1st operation). [Cd.101]: 0 → 100 (during the 1st operation) → 150 (during the 2nd operation).
- *1 at [Cd.190] PLC READY ON / servo ON: [Md.35] = 300, [Md.120] = 300.
- 1st [Cd.184] Positioning start ON: *2: [Md.35] = 300, [Md.120] = 300; *3: [Cd.22] and [Cd.113] cleared to 0.
- [Cd.113] = 120 → *4: [Md.120] = 120. [Cd.22] = 200 → *4: [Md.35] = 200.
- [Cd.22] = 0 and [Cd.113] = 0 → *5: no change ([Md.35] = 200, [Md.120] = 120).
- [Cd.22] = 350 and [Cd.113] = 320 → *6: exceed the torque limit value, no change.
- 2nd [Cd.184] Positioning start ON: *2: [Md.35] = 100, [Md.120] = 100 ([Cd.101] = 100); *3: [Cd.22] and [Cd.113] cleared to 0.
- [Cd.22] = 75 → *4: [Md.35] = 75. [Cd.113] = 200 → *4: [Md.120] = 200.
- [Cd.22] = 230 → *4: [Md.35] = 230. [Cd.113] = 80 → *4: [Md.120] = 80.
- [Cd.190] PLC READY and [Cd.191] All axis servo ON turn OFF, then ON again (*1).
- 3rd [Cd.184] Positioning start ON: *2: [Md.35] = 150, [Md.120] = 150 ([Cd.101] = 150); *3: [Cd.22] and [Cd.113] cleared to 0.

*1 The torque limit setting value or torque output setting value becomes effective at the rising edge of the "[Cd.190] PLC READY" (however, after the servo turned ON.)
*2 The torque limit setting value or torque output setting value becomes effective at the rising edge of the "[Cd.184] Positioning start", and the torque limit value is updated.
*3 The torque change value is cleared to "0" at the rising edge of the "[Cd.184] Positioning start".
*4 The torque limit value is changed by the torque changed value.
*5 When the new torque value is 0, a torque change is considered not to be carried out.
*6 When the change value exceeds the torque limit value, a torque change is considered not to be carried out.

#### Precautions during control (制御上の注意事項) (7.5 / original p.272)

- If a value besides "0" is set in the new torque value, the torque generated by the servo motor will be limited by the setting value. To limit the torque with the value set in "[Pr.17] Torque limit setting value" or "[Cd.101] Torque output setting value", set "0" to the new torque value.

| Setting value of "[Cd.112] Torque change function switching request" | Setting item (New torque value) |
|---|---|
| 0: Forward/reverse torque limit value same setting | [Cd.22] New torque value/forward new torque value |
| 1: Forward/reverse torque limit value individual setting | [Cd.22] New torque value/forward new torque value |
| 1: Forward/reverse torque limit value individual setting | [Cd.113] New reverse torque value |

*In the original, "1: Forward/reverse torque limit value individual setting" is merged over 2 rows. Expanded to each row.

- The "[Cd.22] New torque value/forward new torque value" or "[Cd.113] New reverse torque value" is validated when written to the Simple Motion module/Motion module. (Note that it is not validated from the time the power supply is turned ON to the time the "[Cd.190] PLC READY" is turned ON.)
- If the setting value of "[Cd.22] New torque value/forward new torque value" is outside the setting range, the warning "Outside new torque value range/outside forward new torque value range" (warning code: 0907H [FX5-SSC-S], or warning code: 0D07H [FX5-SSC-G]) will occur and the torque will not be changed. If the setting value of "[Cd.113] New reverse torque value" is outside the setting range, the warning "Outside reverse new torque value range" (warning code: 0932H [FX5-SSC-S], or warning code: 0D32H [FX5-SSC-G]) will occur and the torque will not be changed.
- If the time to hold the new torque value is not more than 10 ms, a torque change may not be executed.
- When changing from "0: Forward/reverse torque limit value same setting" to "1: Forward/reverse torque limit value individual setting" by the torque change function, set "0" or same value set in "[Cd.22] New torque value/forward new torque value" in "[Cd.113] New reverse torque value" before change.

#### Setting method (設定方法) (7.5 / original p.273)

To use the "torque change function", write the data shown in the following table to the Simple Motion module/Motion module using the program.
The set details are validated when written to the Simple Motion module/Motion module.
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.112] | Torque change function switching request | 0: Forward/reverse torque limit value same setting<br>1: Forward/reverse torque limit value individual setting | Sets "same setting/individual setting" of the forward torque limit value and reverse torque limit value.<br>• Set "0" normally. (When the forward torque limit value and reverse torque limit value are not divided.)<br>• When a value except "1" is set, it operates as "forward/reverse torque limit value same setting". | 4363+100n |
| [Cd.22] | New torque value/forward new torque value | 0 to [Pr.17] Torque limit setting value | When "0" is set to "[Cd.112] Torque change function switching request", a new torque limit value is set. (This value is set to the forward torque limit value and reverse torque limit value.)<br>When "1" is set to "[Cd.112] Torque change function switching request", a new forward torque limit value is set. | 4325+100n |
| [Cd.113] | New reverse torque value | 0 to [Pr.17] Torque limit setting value | "1" is set in "[Cd.112] Torque change function switching request", a new reverse torque limit value is set.<br>• When "0" is set in "[Cd.112] Torque change function switching request", the setting value is invalid. | 4364+100n |

Refer to the following for the setting details.
→Page 561 Control Data

### Target position change function (目標位置変更機能) (7.5 / original p.274-277)

The "target position change function" is a function to change a target position to a newly designated target position at any timing during the position control (1-axis linear control). A command speed can also be changed simultaneously.
The target position and command speed changed are set directly in the buffer memory, and the target position change is executed by "[Cd.29] Target position change request flag".

#### Details of control (制御内容) (7.5 / original p.274)

The following charts show the details of control of the target position change function.

##### When the address after change is positioned farther away from the start point than the positioning address: (始点からの位置が位置決めアドレスより変更後アドレスの方が遠い場合) (7.5 / original p.274)

[Figure] Address after change farther than the positioning address (original p.274)
- The axis runs at constant speed; the "Target position change request" pulse is given during the constant-speed part.
- Without the change, the axis would decelerate and stop at the "Positioning address" (dashed line).
- With the change, the axis continues at the same speed and decelerates to stop at the "Address after change".

##### When the speed is changed simultaneously with changing the address: (アドレス変更と同時に速度が変更される場合) (7.5 / original p.274)

[Figure] Speed changed simultaneously with the address (original p.274)
- At the "Target position change request", the axis accelerates from the "Speed before change" to the "Speed after change" and stops at the "Address after change" (instead of the "Positioning address", dashed).

##### When the direction of the operation is changed: (運転の向きが変化する場合) (7.5 / original p.274)

[Figure] Direction of the operation changed (original p.274)
- The "Address after change" is behind the current position (the original "Positioning address" is ahead, dashed).
- At the "Target position change request", the axis decelerates to a stop at the "Reversal position", then moves in the reverse direction (negative speed) and stops at the "Address after change".

#### Precautions during operation (制御上の注意事項) (7.5 / original p.275-276)

- When the direction of an operation changes, the positioning movement stops temporarily at the position where the positioning movement direction reverses (reversal position), and then positioning to the address after change is performed (→Page 272 When the direction of the operation is changed:). This reversal position is the position obtained by adding the distance required for deceleration stop to the position at the target position change request.

[Figure] Reversal position (original p.275)
- From the "Position at target position change request" (at the "Target position change request" pulse), the axis decelerates to 0 at the "Reversal position" and then reverses.
- Shaded area: "Distance required for deceleration stop" (from the position at the request to the reversal position).

- Even if the address after change is in the movement direction at target position change request, if the movement amount to the address after change is smaller than the distance required for deceleration stop, the movement direction reverses. In such case, advance the target position change request to increase the movement amount to the address after change, or shorten the deceleration time to reduce the distance required for deceleration stop.

[Figure] When the movement amount to the address after change is less than the distance required for deceleration stop (original p.275)
- Legend: gray = "Distance required for deceleration stop (including hatched part)"; hatched = "Movement amount to the address after change".
- The "Address after change" lies before the end of the deceleration distance, so the axis passes it, stops at the "Reversal position", and reverses.

[Figure] When advancing the target position change request (original p.275)
- Legend: gray = "Distance required for deceleration stop"; hatched = "Movement amount to the address after change (including gray part)".
- The request is given earlier; the movement amount to the address after change becomes larger than the deceleration distance, so the axis stops at the "Address after change" without reversing (the dotted line shows the former path to the reversal position).

[Figure] When shortening the deceleration time (original p.275)
- Legend: same as "When advancing the target position change request".
- With a shorter (steeper) deceleration, the deceleration distance becomes smaller than the movement amount to the address after change, so the axis stops at the "Address after change" without reversing (dotted: former path to the reversal position).

- If a command speed exceeding the speed limit value is set to change the command speed, the warning "Speed limit value over" (warning code: 0991H [FX5-SSC-S], or warning code: 0D51H [FX5-SSC-G]) will occur and the new command speed will be the speed limit value. Also, if the command speed change disables the remaining distance to the target value from being assured, the warning "Insufficient remaining distance" will occur (warning code: 0994H [FX5-SSC-S], or warning codes: 0D54H and 0D55H [FX5-SSC-G]).
- In the following cases, a target position change request given is ignored and the warning "Target position change not possible" (warning code: 099BH [FX5-SSC-S], or warning codes: 0D5BH and 0D61H [FX5-SSC-G]) occurs.
  - During interpolation control
  - While a new target position value (address) is outside the software stroke limit range
  - While decelerating to a stop by a stop cause
  - While the positioning data whose operation pattern is continuous path control is executed
  - While the speed change 0 flag ([Md.31] Status: b10) is turned ON
- When a command speed is changed, the current speed is also changed. When the next positioning speed uses the current speed in the continuous positioning, the next positioning operation is carried out at the new speed value. When the speed is set with the next positioning data, the speed becomes the current speed and the operation is carried out at the current speed.
- When a target position change request is given during automatic deceleration in position control and the movement direction is reversed, the positioning control to an address after change is performed after the positioning has stopped once. If the movement direction is not reversed, the speed accelerates to the command speed again and the positioning to the address after change is performed.
- If the constant speed status is regained or the output is reversed by a target position change made while "[Md.48] Deceleration start flag" is ON, the deceleration start flag remains ON. (→Page 306 Deceleration start flag function)
- Carrying out the target position change to the ABS linear 1 in degrees may carry out the positioning to the address after change after the operation decelerates to stop once, even if the movement direction is not reversed.

> **Restriction**
> When carrying out the target position change continuously, take an interval of 10 ms or longer between the times of the target position changes. Also, take an interval of 10 ms or longer when the speed change and override is carried out after changing the target position or the target position change is carried out after the speed change and override.

#### Setting method from the CPU module (CPUユニットからの設定方法) (7.5 / original p.277)

The following shows the data settings and program example for changing the target position of axis 1 by the command from the CPU module. (In this example, the target position value is changed to "300.0 μm" and the command speed is changed to "10000.00 mm/min".)
- The following data is set. (Set using the program referring to the target position change time chart.)

n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.27] | Target position change value (New address) | 3000 | Set the new address. | 4334+100n<br>4335+100n |
| [Cd.28] | Target position change value (New speed) | 1000000 | Set the new speed. | 4336+100n<br>4337+100n |
| [Cd.29] | Target position change request flag | 1 | Set "1: Requests a change in the target position". | 4338+100n |

Refer to the following for details on the setting details.
→Page 561 Control Data
- The following shows the time chart for target position change.

##### Operation example (動作例) (7.5 / original p.277)

[Figure] Target position change time chart (original p.277)
- [Cd.190] PLC READY ON → [Cd.191] All axis servo ON ON → READY signal ([Md.140] Module status: b0) ON.
- [Cd.184] Positioning start ON → Start complete signal ([Md.31] Status: b14) and [Md.141] BUSY turn ON; the axis accelerates and runs.
- [Cd.28] Target position change value (New speed) is set to 1000000, then [Cd.27] Target position change value (New address) is set to 3000.
- [Cd.29] Target position change request flag 0 → 1 → 0 (returns to 0); at that time the speed changes (decelerates to the new speed) and positioning continues to the new address.
- After the positioning ends and the dwell time, [Md.141] BUSY turns OFF and the positioning complete signal ([Md.31] Status: b15) turns ON, then OFF.
- [Cd.184] Positioning start turns OFF, then the start complete signal (b14) turns OFF.
- Error detection signal ([Md.31] Status: b13) stays OFF.

##### Program example (プログラム例) (7.5 / original p.277)

Add the following program to the control program, and write it to the CPU module.
→Page 637 Target position change program [FX5-SSC-S]
→Page 711 Target position change program [FX5-SSC-G]

## 7.6 Functions Related to Start (始動に関連する機能) (7.6 / original p.278-279)

A function related to start includes the "pre-reading start function". This function is executed by parameter setting or program creation and writing.

### Pre-reading start function (先読み始動機能) (7.6 / original p.278-279)

The "pre-reading start function" does not start servo while the execution prohibition flag is ON if a positioning start request is given with the execution prohibition flag ON, and starts servo within operation cycle after OFF of the execution prohibition flag is detected. The positioning start request is given when the axis is in a standby status, and the execution prohibition flag is turned OFF at the axis operating timing.

#### Controls (制御内容) (7.6 / original p.278)

The pre-reading start function is performed by turning ON the positioning start signal with the execution prohibition flag ([Cd.183]) ON. However, if positioning is started with the execution prohibition flag ON, the positioning data is analyzed but servo start is not provided. While the execution prohibition flag is ON, "[Md.26] Axis operation status" remains unchanged from "5: Analyzing". The servo starts within operation cycle after the execution prohibition flag has turned OFF, and "[Md.26] Axis operation status" changes to the status (e.g. position control, speed control) that matches the control method. (Refer to the following figure.)

##### Operation example (動作例) (7.6 / original p.278)

[Figure] Pre-reading start operation (original p.278)
- Initial state: [Cd.184] Positioning start ON, [Cd.183] Execution prohibition flag OFF, [Md.141] BUSY ON, [Md.26] Axis operation status "Position control"; the axis decelerates and stops.
- At the stop: [Md.141] BUSY turns OFF, [Md.26] changes to "Standby"; then [Cd.184] Positioning start turns OFF.
- [Cd.183] Execution prohibition flag turns ON; then [Cd.184] Positioning start turns ON → [Md.26] changes to "Analyzing" ("Positioning data analysis", then "Execution prohibition flag OFF waiting"). BUSY stays OFF and the axis does not move.
- Ta: the time from [Cd.184] Positioning start ON to the "Positioning start timing" ([Cd.183] OFF).
- When [Cd.183] Execution prohibition flag turns OFF ("Positioning start timing"), within "Operation cycle or less" [Md.141] BUSY turns ON, [Md.26] changes to "Position control", and the axis starts (accelerates).

#### Precautions during control (制御上の注意事項) (7.6 / original p.278)

- The time required to analyze the positioning data is up to an operation cycle.
- After positioning data analysis, the system is put in an execution prohibition flag OFF waiting status. Any change made to the positioning data in the execution prohibition flag OFF waiting status is not reflected on the positioning data. Change the positioning data before turning ON the positioning start signal.
- The pre-reading start function is invalid if the execution prohibition flag is turned OFF between when the positioning start signal has turned ON and when positioning data analysis is completed (Ta < start time, Ta: Reference to the above figure).
- The data No. which can be executed positioning start using "[Cd.3] Positioning start No." with the pre-reading start function are No.1 to 600 only. Performing the pre-reading start function at the setting of No.7000 to 7004 or 9001 to 9004 will result in the error "Outside start No. range" (error code: 19A3H [FX5-SSC-S], or error code: 1AA3H [FX5-SSC-G]).
- Always turn ON the execution prohibition flag at the same time or before turning ON the positioning start signal. Pre-reading may not be started if the execution prohibition flag is turned ON during Ta after the positioning start signal is turned ON. The pre-reading start function is invalid if the execution prohibition flag is turned ON after positioning start with the execution prohibition flag OFF. (It is made valid at the next positioning start.)

#### Program example (プログラム例) (7.6 / original p.279)

Refer to the following for the program example.

[Figure] Program example of the pre-reading start function (ladder with labels) (original p.279)
- Step numbers: (0), (5), (25), (30)

Mnemonic transcription (label names as in the original; the device shown under each module label and the comment shown in the ladder are given after `;`):

```text
(0)
LD    bInputPreReadingStartReq                            ; Pre-reading start command
PLS   bPreReadingStartReq_P                               ; Pre-reading start command pulse
(5)
LD    bPreReadingStartReq_P                               ; Pre-reading start command pulse
ANI   FX5SSC_1.stnAxCtrl2_D[0].uPositioningStart_D.0      ; U1\G30104.0  RW:Positioning start (Direct)
ANI   FX5SSC_1.stnAxMntr_D[0].uStatus_D.E                 ; U1\G2417.E   R:Status(Direct)
MOVP  K1 FX5SSC_1.stnAxCtrl1_D[0].uPositioningStartNo_D   ; U1\G4300     RW:Positioning start No. (Direct)
SET   FX5SSC_1.stnAxCtrl2_D[0].uProhibitPositioning_D.0   ; U1\G30103.0  RW:Execution prohibition flag(Direct)
SET   FX5SSC_1.stnAxCtrl2_D[0].uPositioningStart_D.0      ; U1\G30104.0  RW:Positioning start(Direct)
(25)
LD    bInputExecutionProhibitionFlagReleaseReq            ; Execution prohibition flag release command
RST   FX5SSC_1.stnAxCtrl2_D[0].uProhibitPositioning_D.0   ; U1\G30103.0  RW:Execution prohibition flag(Direct)
(30)
LD    FX5SSC_1.stnAxCtrl2_D[0].uPositioningStart_D.0      ; U1\G30104.0  RW:Positioning start (Direct)
LD    FX5SSC_1.stnAxMntr_D[0].uStatus_D.E                 ; U1\G2417.E   R:Status(Direct)
OR    FX5SSC_1.stnAxMntr_D[0].uStatus_D.D                 ; U1\G2417.D   R:Status(Direct)
ANB
ANI   FX5SSC_1.stSysMntr2_D.bnBusy_D[0]                   ; U1\G31501.0  R:BUSY(Axis 1 to 8)(Direct)
RST   FX5SSC_1.stnAxCtrl2_D[0].uPositioningStart_D.0      ; U1\G30104.0  RW:Positioning start(Direct)
```

- Contact types (read from the figure): in (5), uPositioningStart_D.0 and uStatus_D.E are NC (b) contacts; in (30), bnBusy_D[0] is an NC (b) contact; the others are NO (a) contacts. In (30), uStatus_D.E and uStatus_D.D are in parallel. In (5), MOVP / SET / SET are parallel outputs of the same condition.

| Classification | Label name | Description |
|---|---|---|
| Module label | FX5SSC_1.stSysMntr2_D.bnBusy_D[0] | Axis 1 BUSY signal |
| Module label | FX5SSC_1.stnAxCtrl2_D[0].uPositioningStart_D.0 | Axis 1 Positioning start signal |
| Module label | FX5SSC_1.stnAxMntr_D[0].uStatus_D.D | Axis 1 Error detection |
| Module label | FX5SSC_1.stnAxMntr_D[0].uStatus_D.E | Axis 1 Start complete |
| Module label | FX5SSC_1.stnAxCtrl1_D[0].uPositioningStartNo_D | Axis 1 Positioning start No. |
| Module label | FX5SSC_1.stnAxCtrl2_D[0].uProhibitPositioning_D.0 | Axis 1 Execution prohibition flag |
| Global label, local label | (below) | Defines the global label or the local label as follows. The settings of Assign (Device/Label) are not required for the label that the assignment device is not set because the unused internal relay and data device are automatically assigned.<br>The following are for local labels. |

*In the original, "Module label" is merged over 6 rows. Expanded to each row.

Local label definition (transcribed from the screen image in the original):

| No. | Label Name | Data Type | Class |
|---|---|---|---|
| 1 | bPreReadingStartReq_P | Bit | VAR |
| 2 | bInputPreReadingStartReq | Bit | VAR |
| 3 | bInputExecutionProhibitionFlagReleaseReq | Bit | VAR |

## 7.7 Absolute Position System (絶対位置システム) (7.7 / original p.280-282)

The Simple Motion module/Motion module can construct an absolute position system by installing the absolute position system and connecting it through SSCNETⅢ/H.
The following describes precautions when constructing the absolute position system.
The configuration of the absolute position system is shown below.

[Figure] Configuration of the absolute position system (original p.280)
- CPU module → Simple Motion module/Motion module: • Position command • Control command • Servo parameter. Simple Motion module/Motion module → CPU module: • Monitor data.
- Simple Motion module/Motion module (holds the "Home position address") → Servo amplifier: • Position command • Control command • Servo parameter. Servo amplifier → Simple Motion module/Motion module: • Monitor data.
- Servo amplifier with "Battery"; Servo motor (Motor M + Encoder); "Back-up" line between the servo amplifier (battery) and the encoder.
- "Restoration of the current value": from the encoder/servo amplifier to the home position address in the Simple Motion module/Motion module.

### Setting for absolute positions (絶対位置対応の設定) (7.7 / original p.280)

For constructing an absolute position system, use a servo amplifier and a servo motor which enable absolute position detection.

#### Settings for MR-J4(W)-B [FX5-SSC-S] (MR-J4(W)-Bの設定[FX5-SSC-S]) (7.7 / original p.280)

It is also necessary to install a battery for retaining the location of the home position return in the servo amplifier.
To use the absolute position system, select "1: Enabled (used in absolute position detection system)" in "Absolute position detection system (PA03)" in the amplifier setting for the servo parameters. Refer to the manuals of each servo amplifier for details of the absolute position system.
n: Axis No. - 1

| Item | Buffer memory address |
|---|---|
| Absolute position detection system (PA03) | 28403+100n |

#### Settings for MR-J5(W)-B [FX5-SSC-S] (MR-J5(W)-Bの設定[FX5-SSC-S]) (7.7 / original p.280)

Select "1: Enabled (absolute position detection system)" for the servo parameter "Absolute position detection system selection (PA03.0)". To connect MR-J5(W)-B, set the servo parameters "Electronic gear numerator (PA06)" and "Electronic gear denominator (PA07)" so that their ratio becomes 16:1.

#### Settings for MR-J5(W)-G [FX5-SSC-G] (MR-J5(W)-Gの設定[FX5-SSC-G]) (7.7 / original p.280)

Select "1: Enabled (absolute position detection system)" in the servo parameter "Absolute position detection system selection (PA03.0)". In addition, select "0: Disabled" in the servo parameter "[AL.0E3 Absolute position counter warning] selection (29.5)".
When connecting to the encoder with 67108864 pulse resolution, set the servo parameters so that the value of "Electronic gear numerator (PA06)" is 16:1 the value of "Electronic gear denominator (PA07)".

### Precautions (注意事項) (7.7 / original p.280-281)

- When "degree" is used for the setting unit, the absolute position system can be used in infinite feed.
- When a unit other than "degree" is used for the setting unit, infinite feed is not possible when using the absolute position system.

[FX5-SSC-S]
- The following parameters are used to connect the absolute position system to the servo amplifier. Perform all changes to the following parameters before connecting the servo amplifier. When the following parameters are changed after the servo amplifier is connected, the command position value and the motor position may not match.
  - [Pr.1] Unit setting
  - [Pr.2] Number of pulses per rotation (AP)
  - [Pr.3] Movement amount per rotation (AL)
  - [Pr.4] Unit magnification (AM)
  - [Pr.11] Backlash compensation amount
- For MR-J4/MR-J5 series rotary servo motors, in the absolute position system, if the communication between the Simple Motion module and the servo amplifier is disconnected*1 and then reconnected after the servo motor makes 512 rotations or more in one direction, the command position value may not match the motor position. Reconnect the communication therebetween once before 512 rotations or more. If it makes 512 rotations or more without reconnection, perform the machine home position return.

*1 The SSCNET communication is disconnected (disconnect/reconnect function of SSCNET communication is used, the SSCNETⅢ cable is disconnected), the Simple Motion module or the servo amplifier is turned off, etc.

[FX5-SSC-G]
- When connecting the absolute position system to the servo amplifier for the first time, the warning "Home position return data incorrect" (warning code: 0D3CH) occurs based on one of the following conditions and the home position return request turns ON.
  - The backup data for absolute position restoration is corrupted.
  - The rotation direction setting of the servo amplifier is different from that in the backup data.
  - The backup was performed while the home position return request was ON.
  - Absolute position loss occurred on the servo amplifier side.
  - HomeOffset is different from that in the backup data.
  - The encoder resolution is different from that in the backup data.
  - The servo amplifier model is different from that in the backup data.
- The movement amount removed with the electronic gear of the servo amplifier cannot be restored.
- If the absolute position of the servo amplifier cannot be restored, the error "Encoder initial communication error at servo amplifier power supply on" (error code: 1A7EH) occurs and the absolute position cannot be restored. The absolute position may be restored by checking the status of the servo amplifier and reconnecting it. If the home position return request is ON when reconnecting, execute the home position return again.

### Restoration by absolute position system [FX5-SSC-G] (絶対位置システムによる復元[FX5-SSC-G]) (7.7 / original p.281-282)

#### Related buffer memory (関連バッファメモリ) (7.7 / original p.281)

- Axis monitor data

n: Axis No. - 1

| Monitor item | | Monitor value | Storage details | Buffer memory address |
|---|---|---|---|---|
| [Md.190] | Controller position value restoration complete status | → | This area stores the completion status of controller current value restoration.<br>The status becomes "0: Incomplete restoration" when the device is disconnected.<br>• 0: Incomplete restoration<br>• 1: Complete INC restoration<br>• 2: Complete ABS restoration (64-bit Restoration_Based on Backup Location)<br>• 3: Complete ABS restoration (32-bit Restoration_Based on Backup Location) | 59327+100n |

#### Restoration method (復元方法) (7.7 / original p.282)

The following current values are restored.

| Current value | Details |
|---|---|
| Command position value | The restored address is stored.<br>If "degree" is selected as the unit, the addresses have a ring structure for values between 0 and 359.99999°. |
| Feed machine value | The restored address is stored.<br>If "degree" is selected as the unit, the movement amount during the power supply OFF is added to the machine feed value before the power supply OFF (the rounded value within the range of 0 to 359.99999°) for restoration. |

There are following types of current value restoration by the absolute position system.

| Current value restoration method | Reference position | Details | Condition |
|---|---|---|---|
| 64-bit restoration | Backup position | The current value is accurately restored from the backup position within a maximum signed 64-bit integer range [command unit].*1<br>Restoration is performed based on the motion system backup data, and the encoder multiple revolution counter, encoder position within one revolution and encoder resolution of the driver. | 32-bit restoration is performed under either of the following conditions.<br>• The encoder resolution is 0.<br>• The maximum value of the encoder multiple revolution counter is other than 2 to the power of n.<br>&lt;Example&gt; Using HK-KT motor<br>64-bit restoration is performed for the following conditions.<br>Encoder resolution: 67108864 pulses<br>Maximum value of encoder multiple revolution counter: 65536 |
| 32-bit restoration*2 | Backup position | The current value is accurately restored from the backup position within a signed 32-bit integer range [command unit].<br>Restoration is performed based on the motion system backup data and the driver current position (Position Actual Value). | 32-bit restoration is performed under either of the following conditions.<br>• The encoder resolution is 0.<br>• The maximum value of the encoder multiple revolution counter is other than 2 to the power of n.<br>&lt;Example&gt; Using HK-KT motor<br>64-bit restoration is performed for the following conditions.<br>Encoder resolution: 67108864 pulses<br>Maximum value of encoder multiple revolution counter: 65536 |

*In the original, the "Condition" cell is merged over the 2 rows. Expanded to each row.

*1 The actual restoration possible range is - ((Multiple revolution counter maximum value) / 2 × (Encoder resolution)) to ((Multiple revolution counter maximum value) / 2 × (Encoder resolution -1)).
*2 32-bit restoration is available with software version 1.005 or later. Do not use the 32-bit restoration encoder with software version 1.004 or earlier.

> **Point**
> Which restoration method has been used, 64-bit restoration (based on backup location) or 32-bit restoration (based on backup location), can be checked in "[Md.190] Controller position value restoration complete status".

#### Precautions (注意事項) (7.7 / original p.282)

When restoring the current value using 32-bit restoration, if the driver current position (Position Actual Value) has changed by an amount exceeding the signed 32-bit integer range since the last backup, the current value after reconnecting the driver will become an abnormal value.

### Home position return (原点復帰) (7.7 / original p.282)

In the absolute position system, a home position can be determined through home position return.
In the "Data set method" home position return method, the location to which the location of the home position is moved by manual operation (JOG operation/manual pulse generator operation) is treated as the home position.

#### Operation example (動作例) (7.7 / original p.282)

[Figure] Home position return with the data set method (original p.282)
- Within the "Movement range for the machine", the axis is "Moved to this position by manual operation."
- [Cd.3] Positioning start No. is set to "9001 (Home position return destination)"; then [Cd.184] Positioning start turns ON (pulse).
- "The stop position during home position return execution is stored as the home position return position."

## 7.8 Functions Related to Stop (停止に関連する機能) (7.8 / original p.283-291)

Functions related to stop include the "stop command processing for deceleration stop function", "Continuous operation interrupt function" and "step function". Each function is executed by parameter setting or program creation and writing.

### Stop command processing for deceleration stop function (減速停止時停止指令処理機能) (7.8 / original p.283-284)

The "stop command processing for deceleration stop function" is provided to set the deceleration curve if a stop cause occurs during deceleration stop processing (including automatic deceleration).
This function is valid for both trapezoidal and S-curve acceleration/deceleration processing methods.
Refer to the following for details of the stop cause.
→Page 30 Stop process
The "stop command processing for deceleration stop function" performs the following two operations.

#### Control (制御内容) (7.8 / original p.283)

The operation of "stop command processing for deceleration stop function" is explained below.

##### Deceleration curve re-processing (減速カーブ再作成) (7.8 / original p.283)

A deceleration curve is re-processed starting from the speed at stop cause occurrence until a stop, according to the preset deceleration time.
If a stop cause occurs during automatic deceleration of position control, the deceleration stop processing stops as soon as the target has reached the positioning address specified in the positioning data that is currently executed.

[Figure] Deceleration curve re-processing (original p.283)
- "Deceleration stop processing (automatic deceleration) start" → the speed starts to decrease (S-curve).
- At "Stop cause occurrence", a new "Deceleration curve according to preset deceleration time" (bold, gentler) starts from the speed at that moment.
- "Immediate stop at the specified positioning address": when the target reaches the positioning address, the speed drops vertically to 0.
- "Deceleration curve when stop cause does not occur" is shown as a thin (dotted) line for comparison; the dashed line shows the rest of the re-processed curve beyond the positioning address.

##### Deceleration curve continuation (減速カーブ継続) (7.8 / original p.283)

The current deceleration curve is continued after a stop cause has occurred.
If a stop cause occurs during automatic deceleration of position control, the deceleration stop processing may be complete before the target has reached the positioning address specified in the positioning data that is currently executed.

[Figure] Deceleration curve continuation (original p.283)
- After "Deceleration stop processing (automatic deceleration) start", the "Stop cause occurrence" does not change the curve; the same deceleration curve continues to 0.

#### Precautions for control (制御上の注意事項) (7.8 / original p.284)

- In manual control (JOG operation, inching operation, manual pulse generator operation) and speed-torque control, the stop command processing for deceleration stop function is invalid.
- The stop command processing for deceleration stop function is valid when "0: Normal deceleration stop" is set in "[Pr.37] Stop group 1 sudden stop selection" to "[Pr.39] Stop group 3 sudden stop selection" as the stopping method for stop cause occurrence.
- The stop command processing for deceleration stop function is invalid when "1: Rapid stop" is set in "[Pr.37] Stop group 1 sudden stop selection" to "[Pr.39] Stop group 3 sudden stop selection". (A deceleration curve is re-processed starting from the speed at stop cause occurrence until a stop, according to the "[Pr.36] Sudden stop deceleration time".) In the position control (including position control of speed/position changeover control or position/speed changeover control) mode, positioning may stop immediately depending on the stop cause occurrence timing and "[Pr.36] Sudden stop deceleration time" setting.

[Figure] Rapid stop cause during deceleration stop processing (original p.284)
- Left, "(Rapid stop in front of the specified positioning address)": after "Deceleration stop processing (automatic deceleration) start", a "Stop cause occurrence (Rapid stop cause)" starts a "Deceleration curve according to rapid stop deceleration time" (bold, steeper), and the axis stops before the specified positioning address; "Deceleration curve when stop cause does not occur" (dotted) would stop later.
- Right, "(Immediate stop at the specified positioning address)": after the rapid stop cause, the "Deceleration curve according to rapid stop deceleration time" is followed, but the speed drops vertically to 0 when the target reaches the specified positioning address (the dashed line shows the rest of the rapid stop curve); "Deceleration curve when stop cause does not occur" is dotted.

#### Setting method (設定方法) (7.8 / original p.284)

To use the "stop command processing for deceleration stop function", set the following control data in a program.
The set data are made valid as soon as they are written to the buffer memory. The "[Cd.190] PLC READY" is irrelevant.

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.42] | Stop command processing for deceleration stop selection | → | Set the stop command processing for deceleration stop function.<br>0: Deceleration curve re-processing<br>1: Deceleration curve continuation | 5907 |

Refer to the following for the setting details.
→Page 561 Control Data

### Continuous operation interrupt function (連続運転中断機能) (7.8 / original p.285-286)

During positioning control, the control can be interrupted during continuous positioning control and continuous path control (continuous operation interrupt function). When "continuous operation interruption" is execution, the control will stop when the operation of the positioning data being executed ends. To execute continuous operation interruption, set "1: Interrupts continuous operation control or continuous path control." for "[Cd.18] Interrupt request during continuous operation".

#### Operation during continuous operation interruption (連続運転中断時の動作) (7.8 / original p.285)

When the stop command is ON

[Figure] When the stop command is ON (original p.285)
- Start → Positioning data No.10 → Positioning data No.11 → Positioning data No.12 (continuous).
- The stop command turns ON during Positioning data No.11 → "Stop process when stop command turns ON": the axis decelerates to stop immediately (in the middle of No.11). The rest of No.11 and No.12 (dashed) are not executed.

When "1" is set in [Cd.18]

[Figure] When "1" is set in [Cd.18] (original p.285)
- [Cd.18] is set to "1" (ON) during Positioning data No.11 → "Stop process at continuous operation interrupt request": the axis completes No.11 and decelerates to stop at the end of No.11. No.12 (dashed) is not executed.

#### Restrictions (制約事項) (7.8 / original p.286)

- When the "continuous operation interrupt request" is executed, the positioning will end. Thus, after stopping, the operation cannot be "restarted". When "[Cd.6] Restart command" is issued, the warning "Restart not possible" (warning code: 0902H [FX5-SSC-S], or warning code: 0D02H [FX5-SSC-G]) will occur.
- Even if the stop command is turned ON after executing the "continuous operation interrupt request", the "continuous operation interrupt request" cannot be canceled. Thus, if "restart" is executed after stopping by turning the stop command ON, the operation will stop when the positioning data No. where "continuous operation interrupt request" was executed is completed.

[Figure] Continuous operation interrupt with 2-axis interpolation (original p.286)
- Axis 1 (vertical) / Axis 2 (horizontal) path: "Positioning with positioning data No.10" (diagonal), then "Positioning with positioning data No.11" (horizontal).
- "Continuous operation interrupt request" is given during No.11 → "Positioning ends with continuous operation interrupt request." at the end of No.11.
- "Positioning for positioning data No.12 is not executed." (dashed).

- If the operation cannot be decelerated to a stop because the remaining distance is insufficient when "continuous operation interrupt request" is executed with continuous path control, the interruption of the continuous operation will be postponed until the positioning data shown below.
  - Positioning data No. have sufficient remaining distance
  - Positioning data No. for positioning complete (pattern: 00)
  - Positioning data No. for continuous positioning control (pattern: 01)

[Figure] Interrupt postponed because of insufficient remaining distance (original p.286)
- Start → Positioning data No.10 → No.11 → No.12.
- "Continuous operation interrupt request" is given near the end of No.10: "Even when the continuous operation interrupt is requested, the remaining distance is insufficient, and thus, the operation cannot stop at the positioning No. being executed." (the dashed deceleration within No.10 is not possible).
- "Stop process when operation cannot stop at positioning data No.10": No.11 is executed and the axis stops at the end of No.11; No.12 (dashed) is not executed.

- When operation is not performed (BUSY signal is OFF), the interrupt request during continuous operation is not accepted. It is cleared to 0 at a start or restart.

#### Control data requiring settings (設定の必要な制御データ) (7.8 / original p.286)

Set the following data to interrupt continuous operation.
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.18] | Interrupt request during continuous operation | 1 | Set "1: Interrupts continuous operation control or continuous path control.". | 4320+100n |

Refer to the following for the setting details.
→Page 561 Control Data

### Step function (ステップ機能) (7.8 / original p.287-291)

The "step function" is used to confirm each operation of the positioning control one by one.
It is used in debugging work for major positioning control, etc.
A positioning operation in which a "step function" is used is called a "step operation".
In step operations, the timing for stopping the control can be set. (This is called the "step mode".) Control stopped by a step operation can be continued by setting "step continues (to continue the control)" in the "step start information".

#### Relation between the step function and various controls (ステップ機能と各制御の関係) (7.8 / original p.287)

The following table shows the relation between the "step function" and various controls.
○: Set when required, ×: Setting not possible

| Control type | | | Step function | Step applicability |
|---|---|---|---|---|
| Home position return control | Machine home position return control | — | × | Step operation not possible |
| Home position return control | Fast home position return control | — | × | Step operation not possible |
| Major positioning control | Position control | 1-axis linear control | ○ | Step operation possible |
| Major positioning control | Position control | 2 to 4-axis linear interpolation control | ○ | Step operation possible |
| Major positioning control | Position control | 1-axis fixed-feed control | ○ | Step operation possible |
| Major positioning control | Position control | 2 to 4-axis fixed-feed control (interpolation) | ○ | Step operation possible |
| Major positioning control | Position control | 2-axis circular interpolation control | ○ | Step operation possible |
| Major positioning control | 1 to 4-axis speed control | — | × | Step operation not possible |
| Major positioning control | Speed-position switching control, Position-speed switching control | — | ○ | Step operation possible |
| Major positioning control | Other control | Current value changing | ○ | Step operation possible |
| Major positioning control | Other control | JUMP instruction, NOP instruction, LOOP to LEND | × | Step operation not possible |
| Manual control | JOG operation, Inching operation | — | × | Step operation not possible |
| Manual control | Manual pulse generator operation | — | × | Step operation not possible |
| Expansion control | Speed-torque control | — | × | Step operation not possible |

*In the original, the 2nd and 3rd "Control type" columns are merged horizontally where there is no 3rd-level item ("—" here). "Home position return control" is merged over 2 rows, "Major positioning control" over 9 rows, "Position control" over 5 rows, "Other control" over 2 rows, "Manual control" over 2 rows. "Step applicability" is merged: "Step operation not possible" over the 2 home position return rows; "Step operation possible" over the 5 position control rows; "Step operation possible" over Speed-position switching control and Current value changing; "Step operation not possible" over the 3 rows JOG/Inching, Manual pulse generator, Speed-torque control. Expanded to each row.

#### Step mode (ステップモード) (7.8 / original p.287)

In step operations, the timing for stopping the control can be set. This is called the "step mode". (The "step mode" is set in the control data "[Cd.34] Step mode".)
The following shows the two types of "step mode" functions.

##### Deceleration unit step (減速単位ステップ) (7.8 / original p.287)

The operation stops at positioning data requiring automatic deceleration. (A normal operation will be carried out until the positioning data requiring automatic deceleration is found. Once found, that positioning data will be executed, and the operation will then automatically decelerate and stop.)

##### Data No. unit step (データNo.単位ステップ) (7.8 / original p.287)

The operation automatically decelerates and stops for each positioning data. (Even in continuous path control, an automatic deceleration and stop will be forcibly carried out.)

#### Step start request (ステップ始動要求) (7.8 / original p.288)

Control stopped by a step operation can be continued by setting "step continues" (to continue the control) in the "step start information". (The "step start information" is set in the control data "[Cd.36] Step start information".)
The following table shows the results of starts using the "step start information" during step operation.

| Stop status in the step operation | [Md.26] Axis operation status | [Cd.36] Step start information | Step start results |
|---|---|---|---|
| 1 step of positioning stopped normally | Step standby | 1: Continues step operation | The next positioning data is executed. |

The warning "Step not possible" (warning code: 0996H [FX5-SSC-S], or warning code: 0D56H [FX5-SSC-G]) will occur if the "[Md.26] Axis operation status" is as shown below or the step valid flag is OFF when step start information is set.

| [Md.26] Axis operation status | Step start results |
|---|---|
| Standby | Step not continued by warning |
| Stopped | Step not continued by warning |
| Interpolation | Step not continued by warning |
| JOG operation | Step not continued by warning |
| Manual pulse generator operation | Step not continued by warning |
| Analyzing | Step not continued by warning |
| Special start standby | Step not continued by warning |
| Home position return | Step not continued by warning |
| Position control | Step not continued by warning |
| Speed control | Step not continued by warning |
| Speed control in speed-position switching control | Step not continued by warning |
| Position control in speed-position switching control | Step not continued by warning |
| Speed control in position-speed switching control | Step not continued by warning |
| Position control in position-speed switching control | Step not continued by warning |
| Synchronous control | Step not continued by warning |
| Control mode switch | Step not continued by warning |
| Speed control | Step not continued by warning |
| Torque control | Step not continued by warning |
| Continuous operation to torque control | Step not continued by warning |

*In the original, "Step not continued by warning" is merged over all 19 rows. Expanded to each row. ("Speed control" appears twice in the original.)

#### Using the step operation (ステップ運転の使い方) (7.8 / original p.289)

The following shows the procedure for checking positioning data using the step operation.

[Figure] Procedure for checking positioning data using the step operation (flowchart) (original p.289)
1. Start
2. Turn ON the step valid flag. — Write "1" (carry out step operation) in "[Cd.35] Step valid flag".
3. Set the step mode. — Set in "[Cd.34] Step mode".
4. Start positioning.
5. Decision "Positioning stopped by an error." — YES: return to 4 (Start positioning.). NO: go to 6.
6. Decision "One step of positioning is completed." — YES: go to 8. NO: go to 7.
7. Restart positioning. — Write "1" (restart) to "[Cd.6] Restart command" and check whether the positioning data operates normally. Then go to 8.
8. Decision "All positioning is completed." — YES: go to 10. NO: go to 9.
9. Continue the step operation. — Write "1" (step continue) in "[Cd.36] Step start information", and check whether the next positioning data operates normally. Then return to 5.
10. Turn OFF the step valid flag. — Write "0" (carry out no step operation) in "[Cd.35] Step valid flag".
11. End

#### Control details (制御内容) (7.8 / original p.290)

- The following drawing shows a step operation example during a "deceleration unit step".

[Figure] Step operation example during a "deceleration unit step" (original p.290)
- [Cd.35] Step valid flag: ON from the beginning; turns OFF at the end.
- [Cd.184] Positioning start OFF → ON → [Md.141] BUSY OFF → ON.
- Positioning data No.10 ([Da.1] Operation pattern 11) and No.11 ([Da.1] Operation pattern 01) are executed continuously without stopping: at the change No.10 → No.11 the positioning complete signal ([Md.31] Status: b15) turns ON briefly, but the axis does not stop.
- After No.11 decelerates and stops, [Md.141] BUSY turns OFF and the positioning complete signal (b15) turns ON, then OFF; [Cd.184] Positioning start turns OFF.
- "No positioning data No. unit, so operation pattern becomes one step of unit for carrying out automatic deceleration."

- The following drawing shows a step operation example during a "data No. unit step".

[Figure] Step operation example during a "data No. unit step" (original p.290)
- [Cd.35] Step valid flag: ON from the beginning; turns OFF at the end.
- [Cd.184] Positioning start OFF → ON → [Md.141] BUSY OFF → ON; No.10 ([Da.1] Operation pattern 11) is executed and the axis decelerates and stops at its end.
- At the stop of No.10: [Md.141] BUSY turns OFF and the positioning complete signal ([Md.31] Status: b15) turns ON, then OFF.
- [Cd.36] Step start information changes 00H → 01H → 00H: [Md.141] BUSY turns ON again and No.11 ([Da.1] Operation pattern 01) is executed.
- At the end of No.11: BUSY turns OFF, b15 turns ON, then OFF; [Cd.184] Positioning start turns OFF.
- "Operation pattern becomes one step of positioning data No. unit, regardless of continuous path control (11)."

#### Precautions during control (制御上の注意事項) (7.8 / original p.290)

- When step operation is carried out using interpolation control positioning data, the step function settings are carried out for the reference axis.
- When the step valid flag is ON, the step operation will start from the beginning if the positioning start signal is turned ON while "[Md.26] Axis operation status" is "step standby". (The step operation will be carried out from the positioning data set in "[Cd.3] Positioning start No.".)

#### Step function settings (ステップ機能の設定) (7.8 / original p.291)

To use the "step function", write the data shown in the following table to the Simple Motion module/Motion module using the program. Refer to the following for the timing of the settings.
→Page 287 Using the step operation
The set details are validated after they are written to the Simple Motion module/Motion module.
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.34] | Step mode | → | Set "0: Stepping by deceleration units" or "1: Stepping by data No. units". | 4344+100n |
| [Cd.35] | Step valid flag | 1 | Set "1: Validates step operations". | 4345+100n |
| [Cd.36] | Step start information | → | Set "1: Continues step operation", depending on the stop status. | 4346+100n |

Refer to the following for the setting details.
→Page 561 Control Data

## 7.9 Other Functions (その他の機能) (7.9 / original p.292-314)

Other functions include the "skip function", "M code output function", "teaching function", "command in-position function", "acceleration/deceleration processing function", "deceleration start flag function", "speed control 10 × multiplier setting for degree axis function" and "operation setting for incompletion of home position return function".
Each function is executed by parameter setting or program creation and writing.

### Skip function (スキップ機能) (7.9 / original p.292-294)

The "skip function" is used to stop (deceleration stop) the control of the positioning data being executed at the time of the skip signal input, and execute the next positioning data.
A skip is executed by a skip command ([Cd.37] Skip command) or external command signal.
The "skip function" can be used during control in which positioning data is used.

#### Relation between the skip function and various controls (スキップ機能と各制御の関係) (7.9 / original p.292)

The following table shows the relation between the "skip function" and various controls.
○: Set when required, ×: Setting not possible

| Control type | | | Skip function | Skip applicability |
|---|---|---|---|---|
| Home position return control | Machine home position return control | — | × | Skip operation not possible |
| Home position return control | Fast home position return control | — | × | Skip operation not possible |
| Major positioning control | Position control | 1-axis linear control | ○ | Skip operation possible |
| Major positioning control | Position control | 2 to 4-axis linear interpolation control | ○ | Skip operation possible |
| Major positioning control | Position control | 1-axis fixed-feed control | ○ | Skip operation possible |
| Major positioning control | Position control | 2 to 4-axis fixed-feed control (interpolation) | ○ | Skip operation possible |
| Major positioning control | Position control | 2-axis circular interpolation control | ○ | Skip operation possible |
| Major positioning control | 1 to 4-axis speed control | — | × | Skip operation not possible |
| Major positioning control | Speed-position switching control | — | ○ | Skip operation possible |
| Major positioning control | Position-speed switching control | — | × | Skip operation not possible |
| Major positioning control | Other control | Current value changing | ○ | Skip operation possible |
| Major positioning control | Other control | JUMP instruction, NOP instruction, LOOP to LEND | × | Skip operation not possible |
| Manual control | JOG operation, Inching operation | — | × | Skip operation not possible |
| Manual control | Manual pulse generator operation | — | × | Skip operation not possible |
| Expansion control | Speed-torque control | — | × | Skip operation not possible |

*In the original, "Control type" spans three sub-columns; where a row has only two levels, the second-level cell spans the second and third sub-columns (shown here as "—" in the third). "Home position return control" is merged over 2 rows, "Major positioning control" over 10 rows, "Position control" over 5 rows, "Other control" over 2 rows, "Manual control" over 2 rows. In "Skip applicability", "Skip operation not possible" is merged over the 2 home position return rows, "Skip operation possible" over the 5 position control rows, and "Skip operation not possible" over the 3 rows Manual control (2 rows) / Expansion control. Expanded to each row.

#### Control details (制御内容) (7.9 / original p.292)

The following drawing shows the skip function operation.

##### Operation example (動作例) (7.9 / original p.292)

[Figure] Skip function operation (original p.292)
- Signals (top to bottom): [Cd.184] Positioning start, [Md.141] BUSY, Positioning complete signal ([Md.31] Status: b15), Positioning (V-t), Skip signal.
- [Cd.184] Positioning start turns OFF→ON; [Md.141] BUSY turns ON following it, and the positioning starts.
- While the positioning is running at constant speed, the skip signal turns ON (a short pulse): "Deceleration by skip signal" occurs, and after the deceleration, "Start of the next positioning" follows immediately.
- The positioning complete signal (b15) does not turn ON at the skip point.
- When the next positioning is completed, [Md.141] BUSY turns OFF and the positioning complete signal (b15) turns ON; after [Cd.184] turns OFF, b15 turns OFF.

#### Precautions during control (制御上の注意事項) (7.9 / original p.293)

- If the skip signal is turned ON at the last of an operation, a deceleration stop will occur and the operation will be terminated.
- When a control is skipped (when the skip signal is turned ON during a control), the positioning complete signals will not turn ON.
- When the skip signal is turned ON during the dwell time, the remaining dwell time will be ignored, and the next positioning data will be executed.
- When a control is skipped during interpolation control, the reference axis skip signal is turned ON. When the reference axis skip signal is turned ON, a deceleration stop will be carried out for every axis, and the next reference axis positioning data will be executed.
- The M code ON signals will not turn ON when the M code output is set to the AFTER mode. (In this case, the M code will not be stored in "[Md.25] Valid M code".)
- The skip cannot be carried out by the speed control and position-speed switching control.
- If the skip signal is turned ON with the M code signal turned ON, the transition to the next data is not carried out until the M code signal is turned OFF.

#### Setting method from the CPU module (CPUユニットからの設定方法) (7.9 / original p.293)

The following shows the settings and program example for skipping the control being executed in axis 1 with a command from the CPU module.

##### Setting data (設定データ) (7.9 / original p.293)

Set the following data.
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.37] | Skip command | 1 | Set "1: Skip request". | 4347+100n |

Refer to the following for the setting details.
→Page 561 Control Data

- Add the following program to the control program, and write it to the CPU module.

When the "skip command" is input, the value "1" (skip request) set in "[Cd.37] Skip command" is written to the buffer memory of the Simple Motion module/Motion module.

##### Program example (プログラム例) (7.9 / original p.293)

Refer to the following for the program example.
→Page 636 Skip program [FX5-SSC-S]
→Page 714 Skip program [FX5-SSC-G]

#### Setting method using an external command signal (外部指令信号を使った設定方法) (7.9 / original p.294)

The skip function can also be executed using an "external command signal".
The following shows the settings and program example for skipping the control being executed in axis 1 using an "external command signal".

- Set the following data to execute the skip function using an external command signal. (The setting is carried out using the program.)

n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Pr.42] | External command function selection | 3 | Set "3: Skip request". | 62+150n |
| [Cd.8] | External command valid | 1 | Set "1: Validate external command". | 4305+100n |

Set the external command signal (DI) to be used in "[Pr.95] External command signal selection".
Refer to the following for the setting details.
→Page 444 Basic Setting, →Page 561 Control Data

- Add the following program to the control program, and write it to the CPU module.

##### Program example (プログラム例) (7.9 / original p.294)

Refer to the following for the program example.

```
(0)
LD    bSkipFunctionSelectionReq                                        ; Skip function selection command
MOVP  K3  FX5SSC_1.stnAxPrm_D[0].uExternalCommandFunctionMode_D        ; U1\G62  RW:External command function selection(Direct)
MOVP  K1  FX5SSC_1.stnAxCtrl1_D[0].uExternalCommandValid_D             ; U1\G4305  RW:External command valid(Direct)
```

| Classification | Label name | Description |
|---|---|---|
| Module label | FX5SSC_1.stnAxPrm_D[0].uExternalCommandFunctionMode_D | Axis 1 External command function selection |
| Module label | FX5SSC_1.stnAxCtrl1_D[0].uExternalCommandValid_D | Axis 1 External command valid |
| Global label, local label | Defines the global label or the local label as follows. The settings of Assign (Device/Label) are not required for the label that the assignment device is not set because the unused internal relay and data device are automatically assigned.<br>The following are for local labels. | (see the label table below) |

*In the original, "Module label" is merged over 2 rows, and the "Label name" and "Description" cells of the "Global label, local label" row are merged, with the label definition screen embedded under the text. The screen is separated into the table below.

- Local label definition (from the screen image on original p.294)

| No. | Label Name | Data Type | Class |
|---|---|---|---|
| 1 | bSkipFunctionSelectionReq | Bit | VAR |

### M code output function (Mコード出力機能) (7.9 / original p.295-298)

The "M code output function" is used to command sub work (clamping, drill rotation, tool replacement, etc.) related to the positioning data being executed.
When the M code ON signal ([Md.31] Status: b12) is turned ON during positioning execution, a No. called the M code is stored in "[Md.25] Valid M code".
These "[Md.25] Valid M code" are read from the CPU module, and used to command auxiliary work. M codes can be set for each positioning data. (Set in setting item "[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions" of the positioning data.)
The timing for outputting (storing) the M codes can also be set in the "M code output function".

#### M code ON signal output timing (MコードON信号の出力タイミング) (7.9 / original p.295)

The timing for outputting (storing) the M codes can be set in the "M code output function". (The M code is stored in "[Md.25] Valid M code" when the M code ON signal is turned ON.)
The following shows the two types of timing for outputting M codes: the "WITH mode" and the "AFTER mode".

##### WITH mode (WITHモード) (7.9 / original p.295)

The M code ON signal is turned ON at the positioning start, and the M code is stored in "[Md.25] Valid M code".

Ex.

[Figure] M code ON signal output timing - WITH mode (original p.295)
- Signals (top to bottom): [Cd.184] Positioning start, [Md.141] BUSY, M code ON signal ([Md.31] Status: b12), [Cd.7] M code OFF request, [Md.25] Valid M code, Positioning (V-t), [Da.1] Operation pattern.
- [Da.1] Operation pattern: first positioning "01", second positioning "00". A "Dwell time" is shown after the end of each positioning.
- At the positioning start ([Cd.184] ON → BUSY ON), the M code ON signal turns ON and [Md.25] changes to m1 (*1) at the same time.
- [Cd.7] M code OFF request 0→1 turns the M code ON signal OFF, then [Cd.7] returns 1→0.
- At the start of the second positioning (after the dwell time), the M code ON signal turns ON again and [Md.25] changes to m2 (*1); again [Cd.7] 0→1→0 turns it OFF.
- After the second positioning (pattern 00) and its dwell time, [Md.141] BUSY turns OFF; [Cd.184] turns OFF.

*1 m1 and m2 indicate set M codes.

##### AFTER mode (AFTERモード) (7.9 / original p.295)

The M code ON signal is turned ON at the positioning completion, and the M code is stored in "[Md.25] Valid M code".

Ex.

[Figure] M code ON signal output timing - AFTER mode (original p.295)
- Signals: same as the WITH mode figure. [Da.1] Operation pattern: first positioning "01", second positioning "00".
- At the completion of the first positioning, the M code ON signal turns ON and [Md.25] changes to m1 (*1).
- [Cd.7] M code OFF request 0→1 turns the M code ON signal OFF, then [Cd.7] returns 1→0; the second positioning starts after this.
- At the completion of the second positioning, [Md.141] BUSY turns OFF, the M code ON signal turns ON and [Md.25] changes to m2 (*1). [Cd.184] turns OFF around the same time.

*1 m1 and m2 indicate set M codes.

#### M code ON signal OFF request (MコードON信号OFF要求) (7.9 / original p.296)

When the M code ON signal is ON, it must be turned OFF by the program.
To turn OFF the M code ON signal, set "1" (turn OFF the M code signal) in "[Cd.7] M code OFF request".
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.7] | M code OFF request | 1 | Set "1: Turn OFF the M code ON signal". | 4304+100n |

Refer to the following for the setting details.
→Page 561 Control Data

The next positioning data will be processed as follows if the M code ON signal is not turned OFF. (The processing differs according to the "[Da.1] Operation pattern".)

| [Da.1] Operation pattern | | Processing |
|---|---|---|
| 00 | Independent positioning control (Positioning control) | The next positioning data will not be executed until the M code ON signal is turned OFF. |
| 01 | Continuous positioning control | The next positioning data will not be executed until the M code ON signal is turned OFF. |
| 11 | Continuous path control | The next positioning data will be executed. If the M code is set to the next positioning data, the warning "M code ON signal ON" (warning code: 0992H [FX5-SSC-S], or warning code: 0D52H [FX5-SSC-G]) will occur. |

*In the original, the "Processing" cell is merged over the 2 rows 00 / 01. Expanded to each row.

##### Operation example (動作例) (7.9 / original p.296)

[Figure] Operation when the M code ON signal is not turned OFF in continuous path control (original p.296)
- Signals (top to bottom): [Cd.184] Positioning start, [Md.141] BUSY, M code ON signal ([Md.31] Status: b12), [Cd.7] M code OFF request, [Md.25] Valid M code, Positioning (V-t), [Da.1] Operation pattern.
- [Da.1] Operation pattern: "11", "11", "00" (three continuous speed steps, then deceleration to stop).
- At the start, BUSY and the M code ON signal turn ON; [Md.25] = m1 (*1). [Cd.7] 0→1→0 turns the M code ON signal OFF during the first positioning.
- At the switch to the second positioning data, the M code ON signal turns ON; [Md.25] = m2 (*1). It is not turned OFF before the switch to the third positioning data.
- At the switch to the third positioning data, [Md.25] changes to m3 (*1): "Warning occurs at this timing." Then [Cd.7] 1→0 turns the M code ON signal OFF.
- After the third positioning (00) is completed, [Md.141] BUSY turns OFF and [Cd.184] turns OFF.

*1 m1 and m3 indicate set M codes.

*Note: the footnote is printed as "m1 and m3" in the original (the figure shows m1, m2 and m3); transcribed as printed.

> **Point**
> If the M code output function is not required, set "0" in the setting item of the positioning data "[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions".

#### Precautions during control (制御上の注意事項) (7.9 / original p.297)

- During interpolation control, the reference axis M code ON signal is turned ON.
- The M code ON signal will not turn ON if "0" is set in "[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions". (The M code will not be output, and the previously output value will be held in "[Md.25] Valid M code".)
- If the M code ON signal is ON at the positioning start, the error "M code ON signal start" (error code: 19A0H [FX5-SSC-S], or error code: 1AA0H [FX5-SSC-G]) will occur, and the positioning will not start.
- If the "[Cd.190] PLC READY" is turned OFF, the M code ON signal will turn OFF and "0" will be stored in "[Md.25] Valid M code".
- If the positioning operation time is short during continuous path control, there will not be enough time to turn OFF the M code ON signal and the warning "M code ON signal ON" (warning code: 0992H [FX5-SSC-S], or warning code: 0D52H [FX5-SSC-G]) may occur. In this case, set a "0" in the "[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions" of that section's positioning data to prevent the M code from being output for avoiding the warning occurrence.
- In the AFTER mode during speed control, the M code is not output and the M code ON signal does not turn ON.
- If current value changing where "9003" has been set to "[Cd.3] Positioning start No." is performed, the M code output function is made invalid.

#### Setting method (設定方法) (7.9 / original p.297)

The following shows the settings to use the "M code output function".
- Set the M code No. in the positioning data "[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions".
- Set the timing to output the M code ON signal. The "WITH mode/AFTER mode" also can be set for each positioning data.

Set the required value in the following parameter, and write it to the Simple Motion module/Motion module. The set details are validated at the rising edge (OFF → ON) of the "[Cd.190] PLC READY".
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Pr.18] | M code ON signal output timing | → | Set the timing to output the M code ON signal.<br>0: WITH mode<br>1: AFTER mode | 27+150n |

Refer to the following for the setting details.
→Page 444 Basic Setting

#### Reading M codes (Mコードの読出し) (7.9 / original p.297-298)

"M codes" are stored in the following buffer memory when the M code ON signal turns ON.
n: Axis No. - 1

| Monitor item | | Monitor value | Storage details | Buffer memory address |
|---|---|---|---|---|
| [Md.25] | Valid M code | → | The M code No. ([Da.10] M code/Condition data No./Number of LOOP to LEND repetitions) set in the positioning data is stored. | 2408+100n |

Refer to the following for information on the storage details.
→Page 518 Monitor Data

The following shows a program example for reading the "[Md.25] Valid M code" to the data register (D110) of the CPU module. (The read value is used to command the sub work.)
Read M codes not as "rising edge commands", but as "ON execution commands".

##### Program example (プログラム例) (7.9 / original p.298)

Refer to the following for the program example.

```
(0)
LD    FX5SSC_1.stnAxMntr_D[0].uStatus_D.C                      ; U1\G2417.C  R:Status(Direct)
MOV   FX5SSC_1.stnAxMntr_D[0].uM_Code_D  G_uValidMode          ; source U1\G2408 R:Valid M code(Direct) / destination D110 Valid M code
```

| Classification | Label name | Description |
|---|---|---|
| Module label | FX5SSC_1.stnAxMntr_D[0].uStatus_D.C | Axis 1 M code ON |
| Module label | FX5SSC_1.stnAxMntr_D[0].uM_Code_D | Axis 1 Valid M code |
| Global label, local label | Defines the global label or the local label as follows. The settings of Assign (Device/Label) are not required for the label that the assignment device is not set because the unused internal relay and data device are automatically assigned.<br>The following are for global labels. | (see the label table below) |

*In the original, "Module label" is merged over 2 rows, and the "Label name" and "Description" cells of the "Global label, local label" row are merged, with the label definition screen embedded under the text. The screen is separated into the table below.

- Global label definition (from the screen image on original p.298)

| No. | Label Name | Data Type | Class | Assign (Device/Label) |
|---|---|---|---|---|
| 1 | G_uValidMode | Word [Unsigned]/Bit String [16-bit] | VAR_GLOBAL | D110 |

### Teaching function (ティーチング機能) (7.9 / original p.299-303)

The "teaching function" is used to set addresses aligned using the manual control (JOG operation, inching operation manual pulse generator operation) in the positioning data addresses ([Da.6] Positioning address/movement amount, [Da.7] Arc address).

#### Control details (制御内容) (7.9 / original p.299)

##### Teaching timing (ティーチングのタイミング) (7.9 / original p.299)

Teaching is executed using the program when the "[Md.141] BUSY" is OFF. (During manual control, teaching can be carried out as long as the axis is not BUSY, even when an error or warning has occurred.)

##### Addresses for which teaching is possible (ティーチング可能なアドレス) (7.9 / original p.299)

The addresses for which teaching is possible are "command position values" ([Md.20] Command position value) having the home position as a reference. The settings of the "movement amount" used in incremental system positioning cannot be used. In the teaching function, these "command position values" are set in the "[Da.6] Positioning address/movement amount" or "[Da.7] Arc address".

[Figure] Teaching destination (original p.299)
- Positions aligned by manual control: "Command position value" A → Positioning data "[Da.6] Positioning address/movement amount"
- Positions aligned by manual control: "Command position value" B → Positioning data "[Da.7] Arc address"

#### Precautions during control (制御上の注意事項) (7.9 / original p.299)

- Before teaching, a "machine home position return" must be carried out to establish the home position. (When a current value changing, etc., is carried out, "[Md.20] Command position value" may not show absolute addresses having the home position as a reference.)
- Teaching cannot be carried out for positions to which movement cannot be executed by manual control (positions to which the workpiece cannot physically move). (During 2-axis circular interpolation control with center point designation, etc., teaching of "[Da.7] Arc address" cannot be carried out if the center point of the arc is not within the moveable range of the workpiece.)
- Writing to the flash ROM can be executed up to 100,000 times. If writing to the flash ROM exceeds 100,000 times, the writing may become impossible (assured value is up to 100,000 times). If the error "Flash ROM write number error" (error code: 1080H) occurs when writing to the flash ROM has been completed, check whether or not the program is created so as to write continuously to the flash ROM.

#### Data used in teaching (ティーチングに使用するデータ) (7.9 / original p.299)

The following control data is used in teaching.
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.1] | Flash ROM write request | 1 | Writes the set details to the flash ROM (backup the changed data). | 5900 |
| [Cd.38] | Teaching data selection | → | Sets to which of the following "command position value" is written.<br>0: Written to "[Da.6] Positioning address/movement amount".<br>1: Written to "[Da.7] Arc address". | 4348+100n |
| [Cd.39] | Teaching positioning data No. | → | Designates the data to be taught. (Teaching is carried out when the setting value is 1 to 600.)<br>When teaching has been completed, this data is zero cleared. | 4349+100n |

Refer to the following for the setting details.
→Page 561 Control Data

#### Teaching procedure (ティーチング手順) (7.9 / original p.300-302)

The following shows the procedure for a teaching operation.

- When teaching to the "[Da.6] Positioning address/movement amount" (Teaching example on axis 1)

[Figure] Teaching procedure flowchart - [Da.6] (original p.300)
1. Start
2. Perform machine home position return on axis 1.
3. Move the workpiece to the target position using a manual operation. ··· Using a JOG operation, inching operation, or manual pulse generator operation.
4. Set "Writes the command position value to "[Da.6] Positioning address/movement amount"" in teaching data selection. ··· Set 0 in "[Cd.38] Teaching data selection".
5. Set the positioning data No. for which the teaching will be carried out. ··· Set the positioning data No. in "[Cd.39] Teaching positioning data No.".
6. Confirm completion of the teaching. ··· Confirm that "[Cd.39] Teaching positioning data No." has become 0.
7. End teaching? NO → return to step 3. YES → next.
8. Turn OFF the "[Cd.190] PLC READY".
9. Carry out a writing request to the flash ROM. ··· Set 1 in "[Cd.1] Flash ROM write request".
10. Confirm the completion of the writing. ··· Confirm that "[Cd.1] Flash ROM write request" has become 0.
11. End

- When teaching to the "[Da.7] Arc address", then teaching to the "[Da.6] Positioning address/movement amount" (Teaching example for 2-axis circular interpolation control with sub point designation on axis 1 and axis 2)

[Figure] Teaching procedure flowchart - [Da.7] then [Da.6] (original p.301-302)
1. Start
2. Perform a machine home position return on axis 1 and axis 2.
3. Move the workpiece to the circular interpolation sub point using a manual operation.*1 ··· Using a JOG operation, inching operation, or manual pulse generator operation.
4. (Teaching arc sub point address on axis 1)
   - Set "Writes the command position value to "[Da.7] Arc address"" in teaching data selection. ··· Set 1 in "[Cd.38] Teaching data selection".
   - Set the positioning data No. for which the teaching will be carried out. ··· Set the positioning data No. in "[Cd.39] Teaching positioning data No.".
   - Confirm completion of the teaching. ··· Confirm that "[Cd.39] Teaching positioning data No." has become 0.
5. Teach arc sub point address of axis 2. ··· Entering teaching data using "[Cd.38] Teaching data selection" and "[Cd.39] Teaching positioning data No." for axis 2 in the same fashion as for axis 1.
6. Move the workpiece to the circular interpolation end point position using a manual operation*2. ··· Using a JOG operation, inching operation, or manual pulse generator operation.
7. (Teaching arc end point address on axis 1)
   - Set "Writes the command position value to "[Da.6] Positioning address/movement amount"" in teaching data selection. ··· Set 0 in "[Cd.38] Teaching data selection".
   - Set the positioning data No. for which the teaching will be carried out. ··· Set the positioning data No. in "[Cd.39] Teaching positioning data No.".
   - Confirm completion of the teaching. ··· Confirm that "[Cd.39] Teaching positioning data No." has become 0.
8. (connector 1, continues on p.302) Teaching arc end point address on axis 2. ··· Entering teaching data using "[Cd.38] Teaching data selection" and "[Cd.39] Teaching positioning data No." for axis 2 in the same fashion as for axis 1.
9. End teaching? NO → (connector 2) return to step 3. YES → next.
10. Turn OFF the "[Cd.190] PLC READY".
11. Carry out a writing request to the flash ROM. ··· Set 1 in "[Cd.1] Flash ROM write request".
12. Confirm the completion of the writing. ··· Confirm that "[Cd.1] Flash ROM write request" has become 0.
13. End

##### Motion path (動作図) (7.9 / original p.302)

[Figure] Motion path of 2-axis circular interpolation with sub point designation (original p.302)
- Horizontal axis: Forward direction (Axis 1) / Reverse direction; vertical axis: (Axis 2) Forward direction / Reverse direction; the origin is the Home position.
- Start point address (current stop position) → arc through *1 Sub point address (arc address) → *2 End point address (positioning address): "Movement by circular interpolation".
- The Arc center point is shown on the Axis 1 line, at the intersection of the perpendicular bisectors of the start–sub point and sub point–end point chords.

*1 The sub point address is stored in the arc address.
*2 The end point address is stored in the positioning address.

#### Teaching program example (ティーチングのプログラム例) (7.9 / original p.303)

The following shows a program example for setting (writing) the positioning data obtained with the teaching function to the Simple Motion module/Motion module.

##### Setting conditions (設定条件) (7.9 / original p.303)

When setting the command position value as the positioning address, write it when the BUSY signal is OFF.

##### Operation example (動作例) (7.9 / original p.303)

The following example shows a program carrying out the teaching of axis 1.
- Move the workpiece to the target position using a JOG operation (or an inching operation, a manual pulse generator operation).

[Figure] Teaching timing (original p.303)
- Signals (top to bottom): Positioning (V-t), [Cd.181] Forward run JOG start, [Cd.190] PLC READY, [Cd.191] All axis servo ON, READY signal ([Md.140] Module status: b0), [Md.141] BUSY, Error detection signal ([Md.31] Status: b13), [Md.20] Command position value.
- [Cd.190] PLC READY turns ON → READY signal (b0) turns ON; [Cd.191] All axis servo ON turns ON.
- [Cd.181] Forward run JOG start turns ON → [Md.141] BUSY turns ON and the JOG movement starts; [Cd.181] turns OFF → the axis decelerates and stops at the "Target position"; BUSY turns OFF at the stop.
- Error detection signal (b13) stays OFF throughout.
- [Md.20] Command position value: n1 before the movement, nx during the movement, n2 after the stop.
- "Teaching is possible" while BUSY is OFF (before the JOG start and after the stop); "Teaching is impossible" while BUSY is ON.

> **Point**
> - Confirm the teaching function and teaching procedure before setting the positioning data.
> - The positioning addresses that are written are absolute address (ABS) values.
> - The positioning data written by the teaching function overwrites the data of buffer memory only. Therefore, read from the buffer memory and write to the flash ROM before turning the power OFF as necessary.

##### Program example (プログラム例) (7.9 / original p.303)

Refer to the following for the program example.
→Page 636 Teaching program [FX5-SSC-S]
→Page 714 Teaching program [FX5-SSC-G]

### Command in-position function (指令インポジション機能) (7.9 / original p.304-305)

The "command in-position function" checks the remaining distance to the stop position during the automatic deceleration of positioning control, and sets "1". This flag is called the "command in-position flag". The command in-position flag is used as a front-loading signal indicating beforehand the completion of the position control.

#### Control details (制御内容) (7.9 / original p.304)

The following shows control details of the command in-position function.
- When the remaining distance to the stop position during the automatic deceleration of positioning control becomes equal to or less than the value set in "[Pr.16] Command in-position width", "1" is stored in the command in-position flag ([Md.31] Status: b2).

##### Command in-position width check (指令インポジションの範囲チェック) (7.9 / original p.304)

Remaining distance ≤ "[Pr.16] Command in-position width" setting value

[Figure] Command in-position width check (original p.304)
- Positioning (V-t) with several continuous speed steps, then automatic deceleration to stop.
- Command in-position flag ([Md.31] Status: b2): ON → OFF at the positioning start; turns OFF→ON when the remaining distance enters the "Command in-position width setting value" area (the shaded tail of the deceleration).

- A command in-position width check is carried out every operation cycle.

#### Precautions during control (制御上の注意事項) (7.9 / original p.304)

- A command in-position width check will not be carried out in the following cases.
  - During speed control
  - During speed control in speed-position switching control
  - During speed control in position-speed switching control
  - During speed control mode
  - During torque control mode
  - During continuous operation to torque control mode

[Figure] Command in-position width check with speed-position switching control (original p.304)
- Positioning control start → accel/constant/decel; the command in-position flag (b2) turns OFF→ON when the remaining distance ≤ the command in-position width setting value; "Execution of the command in-position width check" covers this positioning control (from its start).
- At the speed-position switching control start, b2 turns OFF. During the speed control part no check is carried out; after "Speed to position switching", the check is executed ("Execution of the command in-position width check"), and b2 turns ON when the remaining distance ≤ the command in-position width setting value.

- The command in-position flag will be turned OFF in the following cases. ("0" will be stored in "[Md.31] Status: b2".)
  - At the positioning control start
  - At the speed control start
  - At the speed-position switching control, position-speed switching control start
  - At the home position return control start
  - At the JOG operation start
  - At the inching operation start
  - When the manual pulse generator operation is enabled
- The "[Pr.16] Command in-position width" and command in-position flag ([Md.31] Status: b2) of the reference axis are used during interpolation control. When the "[Pr.20] Interpolation speed designation method" is "Composite speed", the command in-position width check is carried out in the remaining distance on the composite axis (line/arc connecting the start point address and end point address).

#### Setting method (設定方法) (7.9 / original p.305)

To use the "command in-position function", set the required value in the parameter shown in the following table, and write it to the Simple Motion module/Motion module.
The set details are validated at the rising edge (OFF → ON) of the "[Cd.190] PLC READY".

| Setting item | | Setting value | Setting details | Factory-set initial value |
|---|---|---|---|---|
| [Pr.16] | Command in-position width | → | Turn ON the command in-position flag, and set the remaining distance to the stop position of the position control. | 100 |

Refer to the following for the setting details.
→Page 444 Basic Setting

#### Confirming the command in-position flag (指令インポジションフラグの確認) (7.9 / original p.305)

The "command in-position flag" is stored in the following buffer memory.
n: Axis No. - 1

| Monitor item | | Monitor value | Storage details | Buffer memory address |
|---|---|---|---|---|
| [Md.31] | Status | → | The command in-position flag is stored in the "b2" position. | 2417+100n |

Refer to the following for information on the storage details.
→Page 518 Monitor Data

> **Point**
> - Parameters are set for each axis.
> - It is recommended that the parameters be set whenever possible with the engineering tool. Execution by a program uses many programs and devices. The execution becomes complicated, and the scan times will increase.

### Acceleration/deceleration processing function (加減速処理機能) (7.9 / original p.306-307)

The "acceleration/deceleration processing function" adjusts the acceleration/deceleration of each control to the acceleration/deceleration curve suitable for device.
Setting the acceleration/deceleration time changes the slope of the acceleration/deceleration curve.
The following two methods can be selected for the acceleration/deceleration curve:
- Trapezoidal acceleration/deceleration
- S-curve acceleration/deceleration

Refer to the following for acceleration/deceleration processing of speed-torque control.
→Page 186 Speed-torque Control

#### "Acceleration/deceleration time 0 to 3" control details and setting (「加減速時間0～3」の制御内容と設定) (7.9 / original p.306)

In the Simple Motion module/Motion module, four types each of acceleration time and deceleration time can be set. By using separate acceleration/deceleration times, control can be carried out with different acceleration/deceleration times for positioning control, JOG operation, home position return, etc.
Set the required values for the acceleration/deceleration time in the parameters shown in the following table, and write them to the Simple Motion module/Motion module.
The set details are validated when written to the Simple Motion module/Motion module.

| Setting item | | Setting value | Setting details | Factory-set initial value |
|---|---|---|---|---|
| [Pr.9] | Acceleration time 0 | → | Set the acceleration time at a value within the range of 1 to 8388608 ms. | 1000 |
| [Pr.25] | Acceleration time 1 | → | Set the acceleration time at a value within the range of 1 to 8388608 ms. | 1000 |
| [Pr.26] | Acceleration time 2 | → | Set the acceleration time at a value within the range of 1 to 8388608 ms. | 1000 |
| [Pr.27] | Acceleration time 3 | → | Set the acceleration time at a value within the range of 1 to 8388608 ms. | 1000 |
| [Pr.10] | Deceleration time 0 | → | Set the deceleration time at a value within the range of 1 to 8388608 ms. | 1000 |
| [Pr.28] | Deceleration time 1 | → | Set the deceleration time at a value within the range of 1 to 8388608 ms. | 1000 |
| [Pr.29] | Deceleration time 2 | → | Set the deceleration time at a value within the range of 1 to 8388608 ms. | 1000 |
| [Pr.30] | Deceleration time 3 | → | Set the deceleration time at a value within the range of 1 to 8388608 ms. | 1000 |

*In the original, the "Setting details" cell is merged over the 4 acceleration time rows and over the 4 deceleration time rows. Expanded to each row.

Refer to the following for the setting details.
→Page 444 Basic Setting

#### "Acceleration/deceleration method setting" control details and setting (「加減速方式の設定」の制御内容と設定) (7.9 / original p.306-307)

In the "acceleration/deceleration method setting", the acceleration/deceleration processing method is selected and set. The set acceleration/deceleration processing is applied to all acceleration/deceleration. (except for inching operation, manual pulse generator operation and speed-torque control.)
The two types of "acceleration/deceleration processing method" are shown below.

##### Trapezoidal acceleration/deceleration processing method (台形加減速処理方式) (7.9 / original p.306)

This is a method in which linear acceleration/deceleration is carried out based on the acceleration time, deceleration time, and speed limit value set by the user.

[Figure] Trapezoidal acceleration/deceleration (original p.306)
- V-t: linear acceleration, constant speed, linear deceleration (trapezoid).

##### S-curve acceleration/deceleration processing method (S字加減速処理方式) (7.9 / original p.307)

In this method, the motor burden is reduced during starting and stopping.
This is a method in which acceleration/deceleration is carried out gradually, based on the acceleration time, deceleration time, speed limit value, and "[Pr.35] S-curve ratio" (1 to 100%) set by the user.

[Figure] S-curve acceleration/deceleration (original p.307)
- V-t: acceleration and deceleration with rounded (S-shaped) start and end.

When a speed change request or override request is given during S-curve acceleration/deceleration processing, S-curve acceleration/deceleration processing begins at a speed change request or override request start.

[Figure] Speed change during S-curve acceleration/deceleration (original p.307)
- A speed change request is given during S-curve acceleration toward the "Command speed before speed change".
- "When speed change request is not given" (dashed): the S-curve continues to the command speed before speed change.
- "Speed change (acceleration)": a new S-curve begins at the speed change request point and reaches the new, higher speed.
- "Speed change (deceleration)": a new S-curve begins at the speed change request point and settles at the new, lower speed.

Set the required values for the "acceleration/deceleration method setting" in the parameters shown in the following table, and write them to the Simple Motion module/Motion module.
The set details are validated when written to the Simple Motion module/Motion module.

| Setting item | | Setting value | Setting details | Factory-set initial value |
|---|---|---|---|---|
| [Pr.34] | Acceleration/deceleration process selection | → | Set the acceleration/deceleration method.<br>0: Trapezoidal acceleration/deceleration processing<br>1: S-curve acceleration/deceleration processing | 0 |
| [Pr.35] | S-curve ratio | → | Set the acceleration/deceleration curve when "1" is set in "[Pr.34] Acceleration/deceleration process selection". | 100 |

Refer to the following for the setting details.
→Page 444 Basic Setting

> **Point**
> - Parameters are set for each axis.
> - It is recommended that the parameters be set whenever possible with the engineering tool. Execution by a program uses many programs and devices. The execution becomes complicated, and the scan times will increase.

### Deceleration start flag function (減速開始フラグ機能) (7.9 / original p.308-310)

The "deceleration start flag function" turns ON the flag when the constant speed status or acceleration status switches to the deceleration status during position control whose operation pattern is "Positioning complete". This function can be used as a signal to start the operation to be performed by other equipment at each end of position control or to perform preparatory operation, etc. for the next position control.

#### Control details (制御内容) (7.9 / original p.308)

When deceleration for a stop is started in the position control whose operation pattern is "Positioning complete", "1" is stored into "[Md.48] Deceleration start flag". When the next operation start is made or the manual pulse generator operation enable status is gained, "0" is stored. (Reference to the figure below)

##### Start made with positioning data No. specified (位置決めデータNo.指定による始動時) (7.9 / original p.308)

[Figure] Deceleration start flag at start with positioning data No. specified (original p.308)
- Operation pattern: Positioning complete (00).
- [Md.48] Deceleration start flag: 0 → 1 at the point where deceleration starts; 1 → 0 at the next operation start.

##### Block start (ブロック始動時) (7.9 / original p.308)

At a block start, this function is valid for only the position control whose operation pattern is "Positioning complete" at the point whose shape has been set to "End". (Reference to the figure below)
The following table indicates the operation of the deceleration start flag in the case of the following block start data and positioning data.

| Block start data | [Da.11] Shape | [Da.12] Start data No. | [Da.13] Special start instruction |
|---|---|---|---|
| 1st point | 1: Continue | 1 | 0: Block start |
| 2nd point | 1: Continue | 3 | 0: Block start |
| 3rd point | 0: End | 4 | 0: Block start |
| ⋮ | | | |

| Positioning Data No. | [Da.1] Operation pattern |
|---|---|
| 1 | 01: Continuous positioning control |
| 2 | 00: Positioning complete |
| 3 | 00: Positioning complete |
| 4 | 11: Continuous path control |
| 5 | 00: Positioning complete |
| ⋮ | |

[Figure] Deceleration start flag at block start (original p.308)
- 1st point: Continue (1): Positioning data No.1 (Continuous positioning control (01)) → Positioning data No.2 (Positioning complete (00)).
- 2nd point: Continue (1): Positioning data No.3 (Positioning complete (00)).
- 3rd point: End (0): Positioning data No.4 (Continuous path control (11)) → Positioning data No.5 (Positioning complete (00)).
- [Md.48] Deceleration start flag stays 0 through No.1 to No.4 (including the decelerations of No.2 and No.3), and changes 0 → 1 only when No.5 (at the "End" point) starts decelerating.

#### Precautions during control (制御上の注意事項) (7.9 / original p.309)

- The deceleration start flag function is valid for the control method of "1-axis linear control", "2-axis linear interpolation control", "3-axis linear interpolation control", "4-axis linear interpolation control", "speed-position switching control" or "position-speed switching control". In the case of linear interpolation control, the function is valid for only the reference axis.
  For details, refer to "Combination of Main Functions and Sub Functions" in the following manual.
  [Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Startup)
- The deceleration start flag does not turn ON when the operation pattern is "continuous positioning control" or "continuous path control".
- The deceleration start flag function is invalid for a home position return, JOG operation, inching operation, manual pulse generator operation, speed-torque control and deceleration made with a stop signal.
- The deceleration start flag does not turn ON when a speed change or override is used to make deceleration.
- If a target position change is made while the deceleration start flag is ON, the deceleration start flag remains ON.

[Figure] Target position change while the deceleration start flag is ON (original p.309)
- Operation pattern: Positioning complete (00). At the "Deceleration start point", [Md.48] changes 0 → 1.
- During the deceleration, "Execution of target position change request" occurs: the axis re-accelerates, runs at constant speed and decelerates to a stop; [Md.48] remains 1.

- When the movement direction is reversed by a target position change, the deceleration start flag turns ON.

[Figure] Movement direction reversed by a target position change (original p.309)
- Operation pattern: Positioning complete (00). At the "Execution of target position change request" during constant speed, the axis decelerates and moves in the reverse direction (dashed line = original profile); [Md.48] changes 0 → 1 at that point.

- During position control of position-speed switching control, the deceleration start flag is turned ON by automatic deceleration. The deceleration start flag remains ON if position control is switched to speed control by the position-speed switching signal after the deceleration start flag has turned ON.
- If the condition start of a block start is not made since the condition is not satisfied, the deceleration start flag turns ON when the shape is "End".
- When an interrupt request during continuous operation is issued, the deceleration start flag turns ON at a start of deceleration in the positioning data being executed.

#### Setting method (設定方法) (7.9 / original p.309)

To use the "deceleration start flag function", set "1" to the following control data using a program.
The set data is made valid on the rising edge (OFF to ON) of the "[Cd.190] PLC READY".

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.41] | Deceleration start flag valid | → | Set whether the deceleration start flag function is made valid or invalid.<br>0: Deceleration start flag invalid<br>1: Deceleration start flag valid | 5905 |

Refer to the following for the setting details.
→Page 561 Control Data

#### Checking of deceleration start flag (減速開始フラグの確認) (7.9 / original p.310)

The "deceleration start flag" is stored into the following buffer memory addresses.
n: Axis No. - 1

| Monitor item | | Monitor value | Storage details | Buffer memory address |
|---|---|---|---|---|
| [Md.48] | Deceleration start flag | → | 0: Status other than below<br>1: Status from deceleration start to next operation start or manual pulse generator operation enable | 2499+100n |

Refer to the following for information on the storage details.
→Page 518 Monitor Data

### Speed control 10 times multiplier setting for degree axis function (degree軸速度10倍指定機能) (7.9 / original p.311-312)

The "Speed control 10 × multiplier setting for degree axis function" is provided to execute the positioning control by 10 × speed of the setting value in the command speed and the speed limit value when the setting unit is "degree".

#### Control details (制御内容) (7.9 / original p.311)

When "Speed control 10 multiplier specifying function for degree axis" is valid, this function related to the command speed, monitor data, speed limit value, is shown below.

##### Command speed (指令速度) (7.9 / original p.311)

- Parameters
  - "[Pr.7] Bias speed at start"
  - "[Pr.46] Home position return speed"
  - "[Pr.47] Creep speed" [FX5-SSC-S]
  - "[Cd.14] New speed value"
  - "[Cd.17] JOG speed"
  - "[Cd.25] Position-speed switching control speed change register"
  - "[Cd.28] Target position change value (New speed)"
  - "[Cd.140] Command speed at speed control mode"
  - "[Da.8] Command speed"
- Major positioning control
  - For "2 to 4 axis linear interpolation control" and "2 to 4 axis fixed-feed control", the positioning control is performed at decuple speed of command speed, when "[Pr.83] Speed control 10 × multiplier setting for degree axis" of reference axis is valid.
  - For "2 to 4 axis speed control", "[Pr.83] Speed control 10 × multiplier setting for degree axis" is evaluated whether it is valid for each axis. If valid, the positioning control will be performed at decuple speed of command speed.

##### Monitor data (モニタデータ) (7.9 / original p.311)

- "[Md.22] Speed command"
- "[Md.27] Current speed"
- "[Md.28] Axis speed command"
- "[Md.33] Target speed"
- "[Md.122] Speed during command"

For the above monitoring data, "[Pr.83] Speed control 10 × multiplier setting for degree axis" is evaluated whether it is valid for each axis. If valid, unit conversion value is changed (×10^-3 → ×10^-2). The unit conversion table of monitor value is shown below.

[Figure] Unit conversion of monitor value (original p.311)
- Monitor value R (converted from hexadecimal to decimal) → Unit conversion: R × 10^m → Actual value ([Md.22] Speed command/[Md.27] Current speed/[Md.28] Axis speed command/[Md.33] Target speed/[Md.122] Speed during command)

- Unit conversion table ([Md.22], [Md.27], [Md.28], [Md.33], [Md.122])

| [Pr.83] setting value | m | Unit |
|---|---|---|
| 0: Invalid | -3 | degree/min |
| 1: Valid | -2 | degree/min |

*In the original, the "Unit" cell is merged over the 2 rows. Expanded to each row.

##### Speed limit value (速度制限値) (7.9 / original p.311)

- "[Pr.8] Speed limit value"
- "[Pr.31] JOG speed limit value"
- "[Cd.146] Speed limit value at torque control mode"
- "[Cd.147] Speed limit value at continuous operation to torque control mode"

For the speed limit value, "[Pr.83] Speed control 10 × multiplier setting for degree axis" is evaluated whether it is valid for each axis. If valid, the positioning control will be performed at decouple speed of setting value (max. speed).

*Note: "decouple speed" is printed as-is in the original (the other sentences use "decuple speed" = 10 × speed).

#### Setting method (設定方法) (7.9 / original p.312)

Set "Valid/Invalid" by "[Pr.83] Speed control 10 × multiplier setting for degree axis".
Normally, the speed specification range is 0.001 to 2000000.000 [degree/min], but it will be decupled and become 0.01 to 20000000.00 [degree/min] by setting "[Pr.83] Speed control 10 × multiplier setting for degree axis" to valid.
To use the "Speed control 10 × multiplier setting for degree axis function", set the parameters shown in the following table.
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Pr.83] | Speed control 10 × multiplier setting for degree axis | → | Set the speed control 10 × multiplier setting for degree axis.<br>0: Invalid<br>1: Valid | 63+150n |

Refer to the following for the setting details.
→Page 444 Basic Setting

### Operation setting for incompletion of home position return function (原点復帰未完時動作指定機能) (7.9 / original p.313-314)

The "Operation setting for incompletion of home position return function" is provided to select whether positioning control is operated or not when the home position return request flag is ON.

#### Control details (制御内容) (7.9 / original p.313)

When "[Pr.55] Operation setting for incompletion of home position return" is valid, this function related to the command speed, monitor data, speed limit value, is shown below.
○: Positioning start possible (Execution possible), ×: Positioning start impossible (Execution not possible)

| Positioning control | [Pr.55] "0: Positioning control is not executed." and "home position return request flag ON" | [Pr.55] "1: Positioning control is executed." and "home position return request flag ON" |
|---|---|---|
| • Machine home position return<br>• JOG operation<br>• Inching operation<br>• Manual pulse generator operation<br>• Current value changing using current value changing start No. (No.9003). | ○*1 | ○*1 |
| When the following cases at block start, condition start, wait start, repeated start, multiple axes simultaneous start and pre-reading start<br>• 1-axis linear control<br>• 2/3/4-axis linear interpolation control<br>• 1/2/3/4-axis fixed-feed control<br>• 2-axis circular interpolation control (with sub point designation/center point designation)<br>• 1/2/3/4-axis speed control<br>• Speed-position switching control (INC mode/ ABS mode)<br>• Position-speed switching control<br>• Current value changing using positioning data No. (No.1 to 600). | × | ○*1 |
| Control mode switching | × | ○*1 |

*In the original, the header "[Pr.55] Operation setting for incompletion of home position return" spans the two value columns. Combined into each column header.

*1 There may be restrictions in the operation for incompletion of home position return depending on the setting or specifications of the servo amplifier. Refer to the manuals of each servo amplifier for details.

#### Precautions during control (制御上の注意事項) (7.9 / original p.313)

- The error "Start at home position return incomplete" (error code: 19A6H [FX5-SSC-S], or error code: 1AA6H [FX5-SSC-G]) occurs if the home position return request flag ([Md.31] Status: b3) is executed the positioning control by turning on, when "0: Positioning control is not executed" is selected the operation setting for incompletion of home position return setting, and positioning control will not be performed. At this time, operation with the manual control (JOG operation, inching operation, manual pulse generator operation) is available.
- When the home position return request flag ([Md.31] Status: b3) is ON, starting Fast home position return will result in the error "Home position return request ON" (error code: 1945H [FX5-SSC-S], or error code: 1A45H [FX5-SSC-G]) despite the setting value of "[Pr.55] Operation setting for incompletion of home position return", and Fast home position return will not be performed.

#### Setting method (設定方法) (7.9 / original p.314)

To use the "Operation setting for incompletion of home position return", set the following parameters using a program.
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Pr.55] | Operation setting for incompletion of home position return | → | Set the operation setting for incompletion of home position return.<br>0: Positioning control is not executed.<br>1: Positioning control is executed. | 87+150n |

Refer to the following for the setting details.
→Page 444 Basic Setting

## 7.10 Servo ON/OFF (サーボON/OFF) (7.10 / original p.315-317)

### Servo ON/OFF (サーボON/OFF) (7.10 / original p.315-316)

This function executes servo ON/OFF of the servo amplifiers connected to the Simple Motion module/Motion module.
By establishing the servo ON status with the servo ON command, servo motor operation is enabled.
The following two signals can be used to execute servo ON/OFF.
- [Cd.191] All axis servo ON
- [Cd.100] Servo OFF command

n: Axis No. - 1

| Setting item | Buffer memory address |
|---|---|
| [Cd.191] All axis servo ON | 5951 |
| [Cd.100] Servo OFF command | 4351+100n |

A list of the "[Cd.191] All axis servo ON" and "[Cd.100] Servo OFF command" is given below.
○: Servo ON (Servo operation enabled)
×: Servo OFF (Servo operation disabled)

| Setting item | | [Cd.100] Servo OFF command: Setting value "0" | Command to servo amplifier | [Cd.100] Servo OFF command: Setting value "1" | Command to servo amplifier |
|---|---|---|---|---|---|
| [Cd.191] All axis servo ON | Other than 1 | × | Servo ON command: OFF<br>Ready ON command: OFF | × | Servo ON command: OFF<br>Ready ON command: OFF |
| [Cd.191] All axis servo ON | 1 | ○ | Servo ON command: ON<br>Ready ON command: ON | × | Servo ON command: OFF<br>Ready ON command: ON |

*In the original, "[Cd.100] Servo OFF command" is a header spanning the four right columns, and "[Cd.191] All axis servo ON" is merged over 2 rows. Expanded.

> **Point**
> When the delay time of "Electromagnetic brake sequence output (PC02)" is used, execute the servo ON to OFF by "[Cd.100] Servo OFF command". (When "[Cd.191] All axis servo ON" is turned ON to OFF, set "1" in "[Cd.100] Servo OFF command" and execute the servo OFF. Then, turn off the "[Cd.191] All axis servo ON" after delay time passes.)
> Refer to the manuals of each servo amplifier for details of servo ON command OFF and ready ON command OFF from Simple Motion module/Motion module.

[FX5-SSC-G]
After the initial communication with the servo amplifier completes, the status will not change to servo ON in the following cases.
- When the error "Servo parameter invalid" (error code: 1DC8H) is occurring.*1
- When the current value restoration is not complete.*2

*1 For details, refer to the following.
→Page 850 Setting methods
*2 After the initial communication with the servo amplifier completes, restoration of the current value is performed on the Motion module. The status of the current value restoration can be checked using the following monitor data.

n: Axis No. -1

| Monitor item | | Monitor value | Stored contents | Buffer memory address |
|---|---|---|---|---|
| [Md.190] | Controller position value restoration complete status | → | This area stores the completion status of controller current value restoration.<br>The status becomes "0: Incomplete restoration" when the device is disconnected.<br>• 0: Incomplete restoration<br>• 1: Complete INC restoration<br>• 2: Complete ABS restoration (64-bit Restoration_Based on Backup Location)<br>• 3: Complete ABS restoration (32-bit Restoration_Based on Backup Location) | 59327+100n |

#### Servo ON (Servo operation enabled) (サーボON(サーボ動作可)) (7.10 / original p.316)

The following shows the procedure for servo ON.
1. Make sure that the servo amplifier LED indicates as follows. (The initial value for "[Cd.191] All axis servo ON" is "OFF".)
   For MR-J4(W)-B and MR-J5(W)-B [FX5-SSC-S]: "b_"
   For MR-J5(W)-G [FX5-SSC-G]: "r_"
2. Set "0" for "[Cd.100] Servo OFF command".
3. Turn ON "[Cd.191] All axis servo ON".

Now the servo amplifier turns ON the servo (servo operation enabled state). (The servo amplifier LED indicates "d_" (for MR-J4(W)-B and MRJ5(W)-B), or "r._" (for MR-J5(W)-G).)

*Note: "MRJ5(W)-B" (without hyphen) is printed as-is in the original.

#### Servo OFF (Servo operation disabled) (サーボOFF(サーボ動作不可)) (7.10 / original p.316)

The following shows the procedure for servo OFF.
1. Set "1" for "[Cd.100] Servo OFF command". (The servo amplifier LED indicates "c_" (for MR-J4(W)-B and MR-J5(W)-B), or "r_" (for MR-J5(W)-G).)

(If the "[Cd.100] Servo OFF command" set "0" again, after the servo operation enabled.)

2. Turn OFF "[Cd.191] All axis servo ON". (The servo amplifier LED indicates "b_" (for MR-J4(W)-B and MR-J5(W)-B), or "r_" (for MR-J5(W)-G).)

> **Point**
> - If the servo motor is rotated by external force during the servo OFF status, follow up processing is performed.
> - Change between servo ON or OFF status while operation is stopped (position control mode). The servo OFF command of during positioning in position control mode, manual pulse control, home position return, speed control mode, torque control mode and continuous operation to torque control mode will be ignored.
> - When the servo OFF is given to all axes, "[Cd.191] All axis servo ON" is applied even if all axis servo ON command is turned ON to OFF with "[Cd.100] Servo OFF command" set "0".

#### PDS state transition [FX5-SSC-G] (PDS状態遷移[FX5-SSC-G]) (7.10 / original p.316)

The drive unit connected as an axis performs operation according to the state transition defined by the CiA402 drive profile as shown below. The Motion module determines whether the drive unit is in servo ON or OFF status based on the current drive unit status.
For details on operation in each status, refer to the specifications of the connected drive unit.

[Figure] PDS state transition (CiA402) (original p.316)
- Start → NotReadyToSwitchOn (area "Not connected") → SwitchOnDisabled (dashed arrow).
- Area "Servo OFF / Driver READY OFF / Each axis is Servo OFF": SwitchOnDisabled, ReadyToSwitchOn. SwitchOnDisabled ⇄ ReadyToSwitchOn.
- Area "Servo OFF / Driver READY ON / Each axis is Servo OFF": SwitchedOn. ReadyToSwitchOn ⇄ SwitchedOn; SwitchedOn → SwitchOnDisabled.
- Area "Servo ON / Driver READY ON / Each axis is Servo ON": OperationEnable, QuickStopActive. SwitchedOn ⇄ OperationEnable; OperationEnable → ReadyToSwitchOn; OperationEnable ⇄ QuickStopActive (solid arrows), plus a dashed arrow OperationEnable → QuickStopActive; QuickStopActive → SwitchOnDisabled (dashed).
- Area "Driver error occurring (Servo OFF)": (dashed arrow, entry from below) → FaultReactionActive → (dashed) Fault → SwitchOnDisabled.
- (The direction of each of the two solid arrows between QuickStopActive and OperationEnable is hard to read from the figure; see original p.316.)

### Follow up function (フォローアップ機能) (7.10 / original p.317)

#### Follow up function (フォローアップ機能) (7.10 / original p.317)

The follow up function monitors the number of motor rotations (actual position value) with the servo OFF and reflects the value in the command position value.
If the servo motor rotates during the servo OFF, the servo motor will not just rotate for the amount of droop pulses at switching the servo ON next time, so that the positioning can be performed from the stop position.

#### Execution of follow up (フォローアップの実行) (7.10 / original p.317)

Follow up function is executed continually during the servo OFF status.

[Figure] Execution of follow up (original p.317)
- Signals: [Cd.191] All axis servo ON, Each axis servo OFF command, Servo ON or OFF status.
- [Cd.191] OFF→ON with servo OFF command = 0 → servo status turns ON.
- Servo OFF command 0→1 → servo status turns OFF (while [Cd.191] is still ON); servo OFF command 1→0 → servo status turns ON again.
- [Cd.191] ON→OFF → servo status turns OFF.
- [Cd.191] OFF→ON again → servo status turns ON, then "Servo alarm detected" → servo status turns OFF (while [Cd.191] stays ON); later [Cd.191] turns OFF.
- "Follow up function executed" in every period where the servo ON or OFF status is OFF.

> **Point**
> The follow up function performs the process if the "Simple Motion module/Motion module and the servo amplifier is turned ON" and "servo OFF" regardless of the presence of the absolute position system.
> [FX5-SSC-G]
> However, in the following case, follow up function is executed even during the servo ON.
> - When the control mode of the servo amplifier is other than the control mode that the Motion module supports*1

*1 The control mode that the Motion module supports
- Position control mode
- Speed control mode
- Torque control mode
- Continuous operation to torque control mode
- Home position return mode
