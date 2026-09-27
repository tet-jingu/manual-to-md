# 6 EXPANSION CONTROL (拡張制御) (Chapter 6 / original p.188-219)

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

## Conversion range (変換範囲表 / original p.188-219)

| Original page | Section | Handling |
|---|---|---|
| p.188-218 | 6.1 Speed-torque Control | Full text |
| p.219 | 6.2 Advanced Synchronous Control | Full text |

## Table of Contents (目次)

- 6 EXPANSION CONTROL (拡張制御)
- 6.1 Speed-torque Control (速度・トルク制御)
- 6.2 Advanced Synchronous Control (アドバンスト同期制御)

---

## 6 EXPANSION CONTROL (拡張制御) (Chapter 6 / original p.188)

The details and usage of expansion control are explained in this chapter.
Expansion control includes the speed-torque control to execute the speed control and torque control not including position loop and the advanced synchronous control to synchronize with input axis using software with "advanced synchronous control parameter" instead of controlling mechanically with gear, shaft, speed change gear or cam, etc.
Execute the required settings to match each control.

## 6.1 Speed-torque Control (速度・トルク制御) (6.1 / original p.188-218)

### Outline of speed-torque control (速度・トルク制御の概要) (6.1 / original p.188)

This function is used to execute the speed control or torque control that does not include the position loop for the command to servo amplifier.
"Continuous operation to torque control mode" that switches the control mode to torque control mode without stopping the servo motor during positioning operation is also available for tightening a bottle cap or a screw.
Switch the control mode from "position control mode" to "speed control mode", "torque control mode" or "continuous operation to torque control mode" to execute the "Speed-torque control".

| Control mode | Control | Remark |
|---|---|---|
| Position control mode | Positioning control, home position return control, JOG operation, Inching operation and Manual pulse generator operation | Control that include the position loop for the command to servo amplifier |
| Speed control mode | Speed-torque control | Control that does not include the position loop for the command to servo amplifier |
| Torque control mode | Speed-torque control | Control that does not include the position loop for the command to servo amplifier |
| Continuous operation to torque control mode | Speed-torque control | Control that does not include the position loop for the command to servo amplifier<br>Control mode can be switched during positioning control or speed control. |

*In the original, "Speed-torque control" in the Control column is merged over the 3 rows Speed control mode / Torque control mode / Continuous operation to torque control mode, and the first Remark cell ("Control that does not include the position loop for the command to servo amplifier") is merged over the 2 rows Speed control mode / Torque control mode. Expanded to each row.

Use the servo amplifiers whose software versions are compatible with each control mode to execute the "Speed-torque control".
[FX5-SSC-G]
If the servo amplifier is not compatible with each control mode, the error "Driver control mode unsupported" (error code: 1AE7) will occur.

### Compatible software version (対応ソフトウェアバージョン) (6.1 / original p.189)

Servo amplifier software versions that are compatible with each control mode are shown below. For the support information not listed in the table below, refer to the manuals of each servo amplifier to be used.
—: There is no restriction by the version.

| Servo amplifier model | Module | Software version: Speed control | Software version: Torque control | Software version: Continuous operation to torque control*1 |
|---|---|---|---|---|
| MR-J5-_B_ | FX5-SSC-S | — | — | — |
| MR-J5W_-_B | FX5-SSC-S | — | — | — |
| MR-J5-_B_-RJ | FX5-SSC-S | — | — | — |
| MR-J4-_B_/MR-JE-B(F) | FX5-SSC-S | — | — | — |
| MR-J4W_-_B | FX5-SSC-S | — | — | — |
| MR-J4-_B_-RJ | FX5-SSC-S | — | — | — |
| MR-J3-_B_ | FX5-SSC-S | — | B3 or later | C7 or later |
| MR-J3W-_B | FX5-SSC-S | — | — | Not compatible |
| MR-J3-_BS_ | FX5-SSC-S | — | — | C7 or later |
| MR-J5-_G_/MR-JET | FX5-SSC-G | — | — | B2 or later |
| MR-J5-_G_-RJ | FX5-SSC-G | — | — | B2 or later |
| MR-J5W_-_G | FX5-SSC-G | — | — | B2 or later |
| MR-J5D_-_G_ | FX5-SSC-G | — | — | — |

*In the original, "Servo amplifier model" is one header spanning the model and module columns, and "Software version" spans the 3 control columns. Merged cells: FX5-SSC-S over the 9 rows MR-J5-_B_ to MR-J3-_BS_, FX5-SSC-G over the 4 rows MR-J5-_G_/MR-JET to MR-J5D_-_G_; Speed control "—" over all 13 rows; Torque control "—" over the 6 rows MR-J5-_B_ to MR-J4-_B_-RJ and over the 6 rows MR-J3W-_B to MR-J5D_-_G_; Continuous operation to torque control "—" over the 6 rows MR-J5-_B_ to MR-J4-_B_-RJ, and "B2 or later" over the 3 rows MR-J5-_G_/MR-JET to MR-J5W_-_G. Expanded to each row.

*1 [FX5-SSC-S]
The torque generation direction of servo motor can be changed by setting the following servo parameters for the servo amplifier that is compatible with the continuous operation to torque control. (→Page 192 Operation of speed-torque control)
For the servo amplifier that is not compatible with the continuous operation to torque control, the operation is the same as that of when the following servo parameters are set to "0: Enabled".
- For MR-J4(W)-B: Function selection C-B POL reflection selection at torque control (PC29)
- For MR-J5(W)-B: Function selection C-B Torque POL reflection selection (PC29.3)

Note that virtual servo amplifiers are not compatible with the continuous operation to torque control mode.
[FX5-SSC-G]
The torque generation direction of servo motor can be changed by setting the servo parameter "Function selection C-B Torque POL reflection selection (PC29.3)" for the servo amplifier that is compatible with the continuous operation to torque control. (→Page 192 Operation of speed-torque control)
For the servo amplifier that is not compatible with the continuous operation to torque control, the operation is the same as that of when "0: Enabled" is set in servo parameter "Function selection C-B Torque POL reflection selection (PC29.3)".

> **CAUTION**
> - If operation that generates torque more than 100% of the rating is performed with an abnormally high frequency in a servo motor stop status (servo lock status) or in a 30 r/min or less low-speed operation status, the servo amplifier may malfunction regardless of the electronic thermal relay protection.

> **Point** (original p.190)
> [FX5-SSC-G]
> When controlling motor HK-KT (67108864 pulses/rev), set the servo parameters of MR-J5(W)-G as follows.
> PA06 (Electronic gear numerator): 16
> PA07 (Electronic gear denominator): 1
> PT01.1 (Speed/acceleration/deceleration unit selection): 0 (r/min, mm/s)
> In speed control, torque control, and continuous operation to torque control mode, the Motion module multiplies the electronic gear ratio of the servo amplifier at the command speed set in the control data and sends the result to the servo amplifier.
>
> [Figure] Command speed and electronic gear ratio (original p.190)
> - Inside "Motion module": Command speed (speed unit) →(Speed unit)→ AP / (AL × AM) →(pulse)→ Encoder resolution → "× 16", "r/min" → Servo amplifier (Electronic gear numerator (PA06): 16, Electronic gear denominator (PA07): 1) →(pulse)→ M (motor) → Reduction ratio → Machine
> - ENC (encoder) returns "pulse" as "Feedback pulse" to the servo amplifier; the servo amplifier returns to "Motor rotation speed (feedback speed)" in the Motion module.
>
> Operation example for speed control mode
> - Condition
>   - [Pr.1] Unit setting: 0 [mm]
>   - [Pr.2] Number of pulses per rotation: 67108864 [pulse] × 1/16 = 4194304 [pulse]
>   - [Pr.3] Movement amount per rotation: 20000.0 [mm]
>   - [Pr.4] Unit magnification: 1 (x 1)
>   - [Cd.140] Command speed at speed control mode: 4000000 [× 10^-2 mm/min]
> - Control details
>   - [Md.103] Motor rotation speed: 200000 [0.01 r/min]
>   - Servo motor speed: 2000 [r/min]

### Setting the required parameters for speed-torque control (速度・トルク制御に必要なパラメータ設定) (6.1 / original p.191)

The "Positioning parameters" must be set to carry out speed-torque control.
The following table shows the setting items of the required parameters for carrying out speed-torque control. Parameters not shown below are not required to be set for carrying out only speed-torque control. (Set the initial values or a value within the setting range.)
◎: Setting always required.
○: Set according to requirements (Set the initial value or a value within the setting range when not used.)

| Setting item | No. | Name | Setting requirement |
|---|---|---|---|
| Positioning parameters | [Pr.1] | Unit setting | ◎ |
| Positioning parameters | [Pr.2] | Number of pulses per rotation (AP) | ◎ |
| Positioning parameters | [Pr.3] | Movement amount per rotation (AL) | ◎ |
| Positioning parameters | [Pr.4] | Unit magnification (AM) | ◎ |
| Positioning parameters | [Pr.8] | Speed limit value | ◎ |
| Positioning parameters | [Pr.12] | Software stroke limit upper limit value | ○ |
| Positioning parameters | [Pr.13] | Software stroke limit lower limit value | ○ |
| Positioning parameters | [Pr.14] | Software stroke limit selection | ○ |
| Positioning parameters | [Pr.22] | Input signal logic selection | ◎ |
| Positioning parameters | [Pr.83] | Speed control 10 × multiplier setting for degree axis | ○ |
| Positioning parameters | [Pr.90] | Operation setting for speed-torque control mode | ○ |
| Positioning parameters | [Pr.127] | Speed limit value input selection at control mode switching | ○ |
| Common parameters | [Pr.82] | Forced stop valid/invalid selection | ○ |

*In the original, the "Setting item" header spans 3 columns, and "Positioning parameters" is merged over 12 rows. Expanded to each row.

Refer to the following for the setting details.
→Page 444 Basic Setting

> **Point**
> - Positioning parameter settings and common parameters settings work in common for all controls using the Simple Motion module/Motion module. When carrying out other controls ("major positioning control", "high-level positioning control", "home position return control"), set the respective setting items as well.
> - "Positioning parameters" are set for each axis.

### Setting the required data for speed-torque control (速度・トルク制御に必要なデータ設定) (6.1 / original p.192-193)

#### Required control data setting for the control mode switching (制御モードの切換えに必要な制御データ) (6.1 / original p.192)

The control data shown below must be set to execute the control mode switching.
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.138] | Control mode switching request | 1 | Set "1: Switching request" after setting "[Cd.139] Control mode setting". | 4374+100n |
| [Cd.139] | Control mode setting | → | Set the control mode to switch.<br>0: Position control mode<br>10: Speed control mode<br>20: Torque control mode<br>30: Continuous operation to torque control mode | 4375+100n |

Refer to the following for the setting details.
→Page 561 Control Data
When "30: Continuous operation to torque control mode" is set, set the switching condition of the control mode to switch to the continuous operation to torque control mode.
The control data shown below must be set to set the switching condition of control mode.
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.153] | Control mode auto-shift selection | → | Set the switching condition when switching to continuous operation to torque control mode.<br>0: No switching condition<br>1: Command position value pass<br>2: Actual position value pass | 4393+100n |
| [Cd.154] | Control mode auto-shift parameter | → | Set the condition value when setting the control mode switching condition. | 4394+100n<br>4395+100n |

Refer to the following for the setting details.
→Page 561 Control Data

#### Required control data setting for the speed control mode (速度制御モードで必要な制御データ) (6.1 / original p.192)

The control data shown below must be set to execute the speed control.
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.140] | Command speed at speed control mode | → | Set the command speed at speed control mode. | 4376+100n<br>4377+100n |
| [Cd.141] | Acceleration time at speed control mode | → | Set the acceleration time at speed control mode. | 4378+100n |
| [Cd.142] | Deceleration time at speed control mode | → | Set the deceleration time at speed control mode. | 4379+100n |

Refer to the following for the setting details.
→Page 561 Control Data

#### Required control data setting for the torque control mode (トルク制御モードで必要な制御データ) (6.1 / original p.193)

The control data shown below must be set to execute the torque control.
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.143] | Command torque at torque control mode | → | Set the command torque at torque control mode. | 4380+100n |
| [Cd.144] | Torque time constant at torque control mode (Forward direction) | → | Set the time constant at driving during torque control mode. | 4381+100n |
| [Cd.145] | Torque time constant at torque control mode (Negative direction) | → | Set the time constant at regeneration during torque control mode. | 4382+100n |
| [Cd.146] | Speed limit value at torque control mode | → | Set the speed limit value at torque control mode. | 4384+100n<br>4385+100n |

Refer to the following for the setting details.
→Page 561 Control Data

#### Required control data setting for the continuous operation to torque control mode (押当て制御モードで必要な制御データ) (6.1 / original p.193)

The control data shown below must be set to execute the continuous operation to torque control.
n: Axis No. - 1

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.147] | Speed limit value at continuous operation to torque control mode | → | Set the speed limit value at continuous operation to torque control mode. | 4386+100n<br>4387+100n |
| [Cd.148] | Acceleration time at continuous operation to torque control mode | → | Set the acceleration time at continuous operation to torque control mode. | 4388+100n |
| [Cd.149] | Deceleration time at continuous operation to torque control mode | → | Set the deceleration time at continuous operation to torque control mode. | 4389+100n |
| [Cd.150] | Target torque at continuous operation to torque control mode | → | Set the target torque at continuous operation to torque control mode. | 4390+100n |
| [Cd.151] | Torque time constant at continuous operation to torque control mode (Forward direction) | → | Set the time constant at driving during continuous operation to torque control mode. | 4391+100n |
| [Cd.152] | Torque time constant at continuous operation to torque control mode (Negative direction) | → | Set the time constant at regeneration during continuous operation to torque control mode. | 4392+100n |

Refer to the following for the setting details.
→Page 561 Control Data

### Operation of speed-torque control (速度・トルク制御の動作) (6.1 / original p.194-213)

#### Switching of control mode (Speed control/Torque control) (制御モードの切換え(速度制御／トルク制御)) (6.1 / original p.194-197)

##### Switching method of control mode (制御モードの切換え方法) (6.1 / original p.194)

To switch the control mode to the speed control or the torque control, set "1" in "[Cd.138] Control mode switching request" after setting the control mode in "[Cd.139] Control mode setting".
When the mode is switched to the speed control mode or the torque control mode, the control data used in each control mode must be set before setting "1" in "[Cd.138] Control mode switching request".
When the switching condition is satisfied at control mode switching request, "30: Control mode switch" is set in "[Md.26] Axis operation status", and the BUSY signal turns ON. "0" is automatically stored in "[Cd.138] Control mode switching request" by Simple Motion module/Motion module after completion of switching.
The warning "Control mode switching during BUSY" (warning code: 09E6H [FX5-SSC-S], or warning code 0DA6H [FX5-SSC-G]) or "Control mode switching during zero speed OFF" (warning code: 09E7H [FX5-SSC-S], or warning code 0DA7H [FX5-SSC-G]) occurs if the switching condition is not satisfied, and the control mode is not switched.
The following shows the switching condition of each control mode.

[Figure] Control mode switching paths (Speed control/Torque control) (original p.194)
- 1) Position control mode → Speed control mode, 2) Speed control mode → Position control mode
- 3) Position control mode → Torque control mode, 4) Torque control mode → Position control mode
- 5) Speed control mode → Torque control mode, 6) Torque control mode → Speed control mode

| No. | Switching operation | Switching condition |
|---|---|---|
| 1) | Position control mode → Speed control mode | Not during positioning*1 and during motor stop*2*3 |
| 2) | Speed control mode → Position control mode | During motor stop*2*3 |
| 3) | Position control mode → Torque control mode | Not during positioning*1 and during motor stop*2*3 |
| 4) | Torque control mode → Position control mode | During motor stop*2*3 |
| 5) | Speed control mode → Torque control mode | None |
| 6) | Torque control mode → Speed control mode | None |

*In the original, the "Switching operation" header spans 2 columns, and "None" is merged over rows 5) and 6). Expanded to each row.

*1 BUSY signal is OFF.
*2 ZERO speed ([Md.119] Servo status2: b3) is ON.
n: Axis No. - 1

| Monitor item | Buffer memory address |
|---|---|
| [Md.119] Servo status2: b3 | 2476+100n |

*3 Change the setting of "Condition selection at mode switching (b12 to b15)" in "[Pr.90] Operation setting for speed-torque control mode" when switching the control mode without waiting for the servo motor to stop. Note that it may cause vibration or impact at control switching. (→Page 480 [Pr.90] Operation setting for speed-torque control mode)

The history of control mode switching is stored to the starting history at request of control mode switching. (→Page 518 System monitor data)
Confirm the control mode with "control mode ([Md.108] Servo status1: b2, b3)" of "[Md.108] Servo status". (→Page 527 Axis monitor data)
n: Axis No. - 1

| Monitor item | Buffer memory address |
|---|---|
| [Md.108] Servo status1: b2, b3 | 2477+100n |

##### Precautions at control mode switching (制御モードの切換え時の注意事項) (6.1 / original p.195)

- The start complete signal and the positioning complete signal do not turn ON at control mode switching.
- When "30: Control mode switch", "31: Speed control", or "32: Torque control" is set in "[Md.26] Axis operation status", the BUSY signal turns ON.
- The motor rotation speed might change momentarily at switching from the speed control mode to the torque control mode. Therefore, it is recommended that the control mode is switched from the speed control to the torque control after the servo motors stop.
- Use the continuous operation to torque control mode for a usage such as pressing a workpiece. When using the continuous operation during speed control mode for a usage such as pressing a workpiece, set as follows.
  - For MR-J5(W)-B or MR-J5(W)-G: Set the servo parameter "Function selection B-1 Model adaptive control selection (PB25.0)" to "2: Disabled (PID control)".
  - For MR-J4(W)-B: Set the servo parameter "Function selection B-1 (PB25)" to "2: Disabled (PID control)".
- "In speed control flag" ([Md.31] Status: b0) does not turn ON during the speed control mode in the speed-torque control.

##### Operation for "Position control mode ⇔ Speed control mode switching" (位置制御モード ⇔ 速度制御モード切換え時の動作) (6.1 / original p.195)

When the position control mode is switched to the speed control mode, the command speed immediately after the switching is the speed set in "speed initial value selection (b8 to b11)" of "[Pr.90] Operation setting for speed-torque control mode".

| Speed initial value selection ([Pr.90]: b8 to b11) | Command speed to servo amplifier immediately after switching from position control mode to speed control mode |
|---|---|
| 0: Command speed | The speed to servo amplifier immediately after switching is "0". |
| 1: Feedback speed | Motor rotation speed received from servo amplifier at switching. |
| 2: Automatic selection | The command speed is invalid due to the setting of continuous operation to torque control mode.<br>At control mode switching, operation is the same as "0: Command speed". |

When the speed control mode is switched to the position control mode, the command position immediately after the switching is the command position value at switching.
The following chart shows the operation timing for axis 1.

[Figure] Operation timing of Position control mode ⇔ Speed control mode switching (axis 1) (original p.195)
- Speed (V-t): Position control mode → Speed control mode → Position control mode. In the speed control mode the axis accelerates to 20000, runs constant, accelerates to 30000, runs constant, then decelerates to 0.
- [Cd.138] Control mode switching request: 0 → 1 → 0 (stored automatically at switching completion) → 1 → 0
- [Cd.139] Control mode setting: 0 → 10 → 0
- [Cd.140] Command speed at speed control mode: 0 → 20000 → 30000 → 0
- [Md.141] BUSY: OFF → ON (at the switching request) → OFF (at completion of switching to position control mode)
- [Md.26] Axis operation status: 0 → 30 → 31 → 30 → 0
- Control mode ([Md.108] Servo status1: b2, b3): [0, 0] → [1, 0] → [0, 0]
- Zero speed ([Md.119] Servo status2: b3): ON → OFF (while the motor rotates) → ON
- The time from the switching request until the control mode changes is marked "*1" (both switchings).

*1 [FX5-SSC-S]
6 to 11 ms
[FX5-SSC-G]
The switching time varies depending on the specifications of the servo amplifier. When using MR-J5(W)-G and setting "ZSP disabled selection at control switching" of servo parameter "(Function selection C-E (PC76)" to "0: Enabled", the control mode switches after reaching Zero speed.
When the control mode of the servo amplifier does not change within 1 second, the error "Control mode switching error" (error code: 1F04H) occurs.

##### Operation for "Position control mode ⇔ Torque control mode switching" (位置制御モード ⇔ トルク制御モード切換え時の動作) (6.1 / original p.196)

When the position control mode is switched to the torque control mode, the command torque immediately after the switching is the torque set in "Torque initial value selection (b4 to b7)" of "[Pr.90] Operation setting for speed-torque control mode".

| Torque initial value selection ([Pr.90]: b4 to b7) | Command torque to servo amplifier immediately after switching from position control mode to torque control mode |
|---|---|
| 0: Command torque | The value of "[Cd.143] Command torque at torque control mode" at switching. |
| 1: Feedback torque | Motor torque value at switching. |

> **Point**
> [FX5-SSC-S]
> When the servo parameter "Function selection C-B POL reflection selection at torque control (PC29)"*1 is set to "0: Enabled" and "Torque initial value selection" is set to "1: Feedback torque", the warning "Torque initial value selection invalid" (warning code: 09E5H) will occur at control mode switching, and the command value immediately after switching is the same as the case of selecting "0: Command torque". If the feedback torque is selected, set "1: Disabled" in the servo parameter "Function selection C-B POL reflection selection at torque control (PC29)"*1.

*1 For MR-J4(W)-B. "Function selection C-B Torque POL reflection selection (PC29.3)" for MR-J5(W)-B.

When the torque control mode is switched to the position control mode, the command position immediately after the switching is the command position value at switching.
The following chart shows the operation timing for axis 1.

[Figure] Operation timing of Position control mode ⇔ Torque control mode switching (axis 1) (original p.196)
- Torque: Position control mode → Torque control mode → Position control mode. In the torque control mode the torque rises to 20.0%, stays constant, rises to 30.0%, stays constant, then decreases to 0.
- [Cd.138] Control mode switching request: 0 → 1 → 0 → 1 → 0
- [Cd.139] Control mode setting: 0 → 20 → 0
- [Cd.143] Command torque at torque control mode: 0 → 200 → 300 → 0
- [Cd.146] Speed limit value at torque control mode: 0 → 50000 (stays 50000 afterwards)
- [Md.141] BUSY: OFF → ON → OFF (at completion of switching to position control mode)
- [Md.26] Axis operation status: 0 → 30 → 32 → 30 → 0
- Control mode ([Md.108] Servo status1: b2, b3): [0, 0] → [0, 1] → [0, 0]
- Zero speed ([Md.119] Servo status2: b3): ON → OFF → ON
- The time from the switching request until the control mode changes is marked "*1" (both switchings).

*1 [FX5-SSC-S]
6 to 11 ms
[FX5-SSC-G]
The switching time varies depending on the specifications of the servo amplifier. When using MR-J5(W)-G and setting "ZSP disabled selection at control switching" of servo parameter "(Function selection C-E (PC76)" to "0: Enabled", the control mode switches after reaching Zero speed.
When the control mode of the servo amplifier does not change within 1 second, the error "Control mode switching error" (error code: 1F04H) occurs.

##### Operation for "Speed control mode ⇔ Torque control mode switching" (速度制御モード ⇔ トルク制御モード切換え時の動作) (6.1 / original p.197)

When the speed control mode is switched to the torque control mode, the command torque immediately after the switching is the torque set in "Torque initial value selection (b4 to b7)" of "[Pr.90] Operation setting for speed-torque control mode".

| Torque initial value selection ([Pr.90]: b4 to b7) | Command torque to servo amplifier immediately after switching from speed control mode to torque control mode |
|---|---|
| 0: Command torque | The value of "[Cd.143] Command torque at torque control mode" at switching. |
| 1: Feedback torque | Motor torque value at switching. |

> **Point**
> [FX5-SSC-S]
> When the servo parameter "Function selection C-B POL reflection selection at torque control (PC29)"*1 is set to "0: Enabled" and "Torque initial value selection" is set to "1: Feedback torque", the warning "Torque initial value selection invalid" (warning code: 09E5H) will occur at control mode switching, and the command value immediately after switching is the same as the case of selecting "0: Command torque". If the feedback torque is selected, set "1: Disabled" in the servo parameter "Function selection C-B POL reflection selection at torque control (PC29)"*1.

*1 For MR-J4(W)-B. "Function selection C-B Torque POL reflection selection (PC29.3)" for MR-J5(W)-B.

When the torque control mode is switched to the speed control mode, the command speed immediately after the switching is the motor rotation speed at switching.
The following chart shows the operation timing for axis 1.

[Figure] Operation timing of Speed control mode ⇔ Torque control mode switching (axis 1) (original p.197)
- Speed (V-t): Speed control mode at 20000 → decelerates to 0 (after [Cd.140] = 0) → stays 0 in the torque control mode → after returning to the speed control mode, accelerates to 30000.
- Torque: in the torque control mode the torque rises to 20.0%, stays constant, then decreases to 0.
- [Cd.138] Control mode switching request: 0 → 1 → 0 → 1 → 0
- [Cd.139] Control mode setting: 10 → 20 → 10
- [Cd.140] Command speed at speed control mode: 20000 → 0 → 30000
- [Cd.143] Command torque at torque control mode: 0 → 200 → 0
- [Cd.146] Speed limit value at torque control mode: 0 → 50000
- [Md.141] BUSY: ON throughout
- [Md.26] Axis operation status: 31 → 30 → 32 → 30 → 31
- Control mode ([Md.108] Servo status1: b2, b3): [1, 0] → [0, 1] → [1, 0]
- The time from the switching request until the control mode changes is marked "*1" (both switchings).

*1 [FX5-SSC-S]
6 to 11 ms
[FX5-SSC-G]
The switching time varies depending on the specifications of the servo amplifier. When using MR-J5(W)-G and setting "ZSP disabled selection at control switching" of servo parameter "(Function selection C-E (PC76)" to "0: Enabled", the control mode switches after reaching Zero speed.
When the control mode of the servo amplifier does not change within 1 second, the error "Control mode switching error" (error code: 1F04H) occurs.

#### Switching of control mode (Continuous operation to torque control) (制御モードの切換え(押当て制御)) (6.1 / original p.198-205)

##### Switching method of control mode (制御モードの切換え方法) (6.1 / original p.198-199)

To switch the control mode to the continuous operation to torque control mode, set "1" in "[Cd.138] Control mode switching request" after setting the control mode to switch to "[Cd.139] Control mode setting" (30: Continuous operation to torque control mode) from position control mode or speed control mode.
The selected control mode can be checked in "[Md.26] Axis operation status".
When the switching condition is satisfied at control mode switching request, "1: Position control mode - continuous operation to torque control mode, speed control mode - continuous operation to torque control mode switching" is set in "[Md.124] Control mode switching status", and the BUSY signal turns ON.
The following shows the switching condition of the continuous operation to torque control mode.

[Figure] Control mode switching paths (Continuous operation to torque control) (original p.198)
- 1) Position control mode → Continuous operation to torque control mode, 2) Continuous operation to torque control mode → Position control mode
- 3) Speed control mode → Continuous operation to torque control mode, 4) Continuous operation to torque control mode → Speed control mode
- 5) Torque control mode → Continuous operation to torque control mode and 6) Continuous operation to torque control mode → Torque control mode are crossed out with a large "×" (switching impossible).

| No. | Switching operation | Switching condition |
|---|---|---|
| 1) | Position control mode → Continuous operation to torque control mode | Not during positioning*1 or during following positioning/synchronous mode<br>• ABS1: 1-axis linear control (ABS)<br>• INC1: 1-axis linear control (INC)<br>• FEED1: 1-axis fixed-feed control<br>• VF1: 1-axis speed control (Forward)<br>• VR1: 1-axis speed control (Reverse)<br>• VPF: Speed-position switching control (Forward)<br>• VPR: Speed-position switching control (Reverse)<br>• PVF: Position-speed switching control (Forward)<br>• PVR: Position-speed switching control (Reverse)<br>• Synchronous control |
| 2) | Continuous operation to torque control mode → Position control mode | During motor stop*2*3 |
| 3) | Speed control mode → Continuous operation to torque control mode | None |
| 4) | Continuous operation to torque control mode → Speed control mode | None |
| 5) | Torque control mode → Continuous operation to torque control mode | Switching is impossible. |
| 6) | Continuous operation to torque control mode → Torque control mode | Switching is impossible. |

*In the original, the "Switching operation" header spans 2 columns; "None" is merged over rows 3) and 4), and "Switching is impossible." over rows 5) and 6). Expanded to each row.

*1 BUSY signal is OFF.
*2 ZERO speed ([Md.119] Servo status2: b3) is ON.
n: Axis No. - 1

| Monitor item | Buffer memory address |
|---|---|
| [Md.119] Servo status2: b3 | 2476+100n |

*3 Change the setting of "Condition selection at mode switching (b12 to b15)" in "[Pr.90] Operation setting for speed-torque control mode" when switching the control mode without waiting for the servo motor to stop. Note that it may cause vibration or impact at control switching. (→Page 480 [Pr.90] Operation setting for speed-torque control mode)

The history of control mode switching is stored to the starting history at request of control mode switching. (→Page 518 System monitor data)
Confirm the status of the continuous operation to torque control mode with "b14: Continuous operation to torque control mode" of "[Md.125] Servo status3". When the mode is switched to the continuous operation to torque control mode, the value in "control mode (b2, b3)" of "[Md.108] Servo status1" remains the same as before switching the control mode. (→Page 527 Axis monitor data)
n: Axis No. - 1

| Monitor item | Buffer memory address |
|---|---|
| [Md.108] Servo status1: b2, b3 | 2477+100n |

> **Point**
> - When the mode is switched from position control mode to continuous operation to torque control mode, only the switching from continuous operation to torque control mode to position control mode is possible. If the mode is switched to other control modes, the warning "Control mode switching not possible" (warning code: 09EBH [FX5-SSC-S], or warning code 0DABH [FX5-SSC-G]) will occur, and the control mode is not switched.
> - When the mode is switched from speed control mode to continuous operation to torque control mode, only the switching from continuous operation to torque control mode to speed control mode is possible. If the mode is switched to other control modes, the warning "Control mode switching not possible" (warning code: 09EBH [FX5-SSC-S], or warning code 0DABH [FX5-SSC-G]) will occur, and the control mode is not switched.

##### Precautions at control mode switching (制御モードの切換え時の注意事項) (6.1 / original p.199)

- The start complete signal and positioning complete signal do not turn ON at control mode switching.
- When "33: Continuous operation to torque control" is set in "[Md.26] Axis operation status" and "1: Position control mode - continuous operation to torque control mode, speed control mode - continuous operation to torque control mode switching" is set in "[Md.124] Control mode switching status", the BUSY signal turns ON.
- When using the continuous operation to torque control mode, use the servo amplifiers that are compatible with the continuous operation to torque control. If the servo amplifiers that are not compatible with the continuous operation to torque control are used, the error "Continuous operation to torque control not supported" (error code: 19E7H) [FX5-SSC-S], or "Driver control mode unsupported" (error code: 1AE7H) [FX5-SSC-G]) occurs at request of switching to continuous operation to torque control mode, and the operation stops. (In the positioning control, the operation stops according to the setting of "[Pr.39] Stop group 3 sudden stop selection". In the speed control, the mode switches to the position control, and the operation immediately stops.)

##### Operation for "Position control mode ⇔ Continuous operation to torque control mode switching" (位置制御モード ⇔ 押当て制御モード切換え時の動作) (6.1 / original p.200-201)

To switch to the continuous operation to torque control mode, set the control data used in the control mode before setting "1" in "[Cd.138] Control mode switching request".
When the switching condition is satisfied at control mode switching request, "1: Position control mode - continuous operation to torque control mode, speed control mode - continuous operation to torque control mode switching" is set in "[Md.124] Control mode switching status" and the BUSY signal turns ON. (When the control mode switching request is executed while the BUSY signal is ON, the BUSY signal does not turn OFF but stays ON at control mode switching.)
"0" is automatically stored in "[Cd.138] Control mode switching request" and "[Md.124] Control mode switching status" after completion of switching.
When the position control mode is switched to the continuous operation to torque control mode, the command torque and command speed immediately after the switching are the values set according to the following setting in "Torque initial value selection (b4 to b7)" and "Speed initial value selection (b8 to b11)" of "[Pr.90] Operation setting for speed-torque control mode".

| Torque initial value selection ([Pr.90]: b4 to b7) | Command torque to servo amplifier immediately after switching from position control mode to continuous operation to torque control mode |
|---|---|
| 0: Command torque | The value of "[Cd.150] Target torque at continuous operation to torque control mode" at switching. |
| 1: Feedback torque | Motor torque value at switching. |

| Speed initial value selection ([Pr.90]: b8 to b11) | Command speed to servo amplifier immediately after switching from position control mode to continuous operation to torque control mode |
|---|---|
| 0: Command speed | Speed that the position command at switching is converted into the motor rotation speed.<br>(When the positioning does not start at switching, the speed to servo amplifier immediately after switching is "0".) |
| 1: Feedback speed | Motor rotation speed received from servo amplifier at switching. |
| 2: Automatic selection | The lower speed between speed that position command at switching is converted into the motor rotation speed and motor rotation speed received from servo amplifier at switching. |

> **Point**
> When the mode is switched to continuous operation to torque control mode in cases where command speed and actual speed are different such as during acceleration/deceleration or when the speed does not reach command speed due to torque limit, set "1: Feedback speed" in "Speed initial value selection (b8 to b11)".

The following chart shows the operation timing for axis 1. (original p.201)

[Figure] Operation timing of Position control mode ⇔ Continuous operation to torque control mode switching (axis 1) (original p.201)
- Sections: Position control mode → Continuous operation to torque control mode → Position control mode.
- Speed (V-t): constant speed in position control mode → after switching, decelerates to 1000 and runs constant → drops to 0 at "Contact with target" → after returning to position control mode, accelerates in the negative direction and runs constant.
- Torque: constant torque in position control mode → right after switching it goes negative momentarily, then a small positive value → after contact with the target it rises (curve) to 30.0% and stays constant → at the switch back to position control mode it drops to 0 → then goes negative (momentarily larger) and settles at a smaller negative value.
- [Cd.138] Control mode switching request: 0 → 1 → 0 → 1 → 0
- [Cd.139] Control mode setting: 0 → 30 → 0
- [Md.141] BUSY: ON → turns OFF briefly at completion of switching back to position control mode → ON again
- [Md.26] Axis operation status: ** → 33 → 30 → 0 → **
- [Md.124] Control mode switching status: 0 → 1 → 0 → 1 → 0
- Continuous operation to torque control ([Md.125] Servo status3: b14): OFF → ON (at completion of switching to continuous operation to torque control mode) → OFF (at completion of switching to position control mode)
- [Cd.147] Speed limit value at continuous operation to torque control mode: 0 → 1000 → 0
- [Cd.150] Target torque at continuous operation to torque control mode: 0 → 300 → 0
- Control mode ([Md.108] Servo status1: b2, b3): [0, 0] throughout (no change)
- Figure note (verbatim): "**: Depending on the positioning method."
- The time from the switching request until the control mode changes is marked "*1" (both switchings).

*1 [FX5-SSC-S]
6 to 11 ms
[FX5-SSC-G]
The switching time varies depending on the specifications of the servo amplifier. When setting "ZSP disabled selection at control switching" of servo parameter "(Function selection C-E (PC76)" to "0: Enabled", the control mode switches after reaching Zero speed.
When the control mode of the servo amplifier does not change within 1 second, the error "Control mode switching error" (error code: 1F04H) occurs.

##### Operation for "Speed control mode ⇔ Continuous operation to torque control mode switching" (速度制御モード ⇔ 押当て制御モード切換え時の動作) (6.1 / original p.202-203)

To switch to the continuous operation to torque control mode, set the control data used in the control mode before setting "1" in "[Cd.138] Control mode switching request".
When the switching condition is satisfied at control mode switching request, "1: Position control mode - continuous operation to torque control mode, speed control mode - continuous operation to torque control mode switching" is set in "[Md.124] Control mode switching status" and the BUSY signal turns ON. (When the control mode switching request is executed while the BUSY signal is ON, the BUSY signal does not turn OFF but stays ON at control mode switching.)
"0" is automatically stored in "[Cd.138] Control mode switching request" and "[Md.124] Control mode switching status" after completion of switching.
When the speed control mode is switched to the continuous operation to torque control mode, the command torque and command speed immediately after the switching is the value set in "Torque initial value selection (b4 to b7)" and "Speed initial value selection (b8 to b11)" of "[Pr.90] Operation setting for speed-torque control mode".

| Torque initial value selection ([Pr.90]: b4 to b7) | Command torque to servo amplifier immediately after switching from speed control mode to continuous operation to torque control mode |
|---|---|
| 0: Command torque | The value of "[Cd.150] Target torque at continuous operation to torque control mode" at switching. |
| 1: Feedback torque | Motor torque value at switching. |

| "Speed initial value selection" ([Pr.90]: b8 to b11) | Command speed to servo amplifier immediately after switching from speed control mode to continuous operation to torque control mode |
|---|---|
| 0: Command speed | The speed commanded to the servo amplifier immediately after switching is the currently commanded speed. |
| 1: Feedback speed | Motor rotation speed received from servo amplifier at switching. |
| 2: Automatic selection | The speed at switching is the lower speed between the currently commanded speed converted into the motor rotation speed and the motor rotation speed received from servo amplifier. |

The following chart shows the operation timing for axis 1. (original p.203)

[Figure] Operation timing of Speed control mode ⇔ Continuous operation to torque control mode switching (axis 1) (original p.203)
- Sections: Speed control mode → Continuous operation to torque control mode → Speed control mode.
- Speed (V-t): 10000 in speed control mode → after switching, decelerates to 1000 and runs constant → drops to 0 at "Contact with target" → after returning to speed control mode, accelerates to -10000 and runs constant.
- Torque: constant torque in speed control mode → right after switching it goes negative momentarily, then a small positive value → after contact with the target it rises (curve) to 30.0% and stays constant → at the switch back to speed control mode it drops to 0 → then goes negative (momentarily larger) and settles at a smaller negative value.
- [Cd.138] Control mode switching request: 0 → 1 → 0 → 1 → 0
- [Cd.139] Control mode setting: 10 → 30 → 10
- [Md.141] BUSY: ON throughout
- [Md.26] Axis operation status: 31 → 33 → 30 → 31
- [Md.124] Control mode switching status: 0 → 1 → 0 → 1 → 0
- Continuous operation to torque control ([Md.125] Servo status3: b14): OFF → ON → OFF
- [Cd.147] Speed limit value at continuous operation to torque control mode: 0 → 1000 → 0
- [Cd.150] Target torque at continuous operation to torque control mode: 0 → 300 → 0
- Control mode ([Md.108] Servo status1: b2, b3): [1, 0] throughout (no change)
- [Cd.140] Command speed at speed control mode: 10000 → 0 (at the first switching) → -10000
- The time from the switching request until the control mode changes is marked "*1" (both switchings).

*1 [FX5-SSC-S]
6 to 11 ms
[FX5-SSC-G]
The switching time varies depending on the specifications of the servo amplifier. When setting "ZSP disabled selection at control switching" of servo parameter "(Function selection C-E (PC76)" to "0: Enabled", the control mode switches after reaching Zero speed.
When the control mode of the servo amplifier does not change within 1 second, the error "Control mode switching error" (error code: 1F04H) occurs.

##### Operation for switching from "Position control mode" to "Continuous operation to torque control mode" automatically (自動切換えによる位置制御モードから押当て制御モード切換え時の動作) (6.1 / original p.204-205)

To switch to the continuous operation to torque control mode automatically when the conditions set in "[Cd.153] Control mode auto-shift selection" and "[Cd.154] Control mode auto-shift parameter" are satisfied, set the control data necessary in the continuous operation to torque control mode, "[Cd.153] Control mode auto-shift selection" and "[Cd.154] Control mode auto-shift parameter", and then set "30: Continuous operation to torque control mode" in "[Cd.139] Control mode setting" and "1: Switching request" in "[Cd.138] Control mode switching request".
In this case, the current control is continued until the setting condition is satisfied after control mode switching request, and "2: Waiting for the completion of control mode switching condition" is set in "[Md.124] Control mode switching status". When the set condition is satisfied, "1: Position control mode - continuous operation to torque control mode, speed control mode - continuous operation to torque control mode switching" is set in "[Md.124] Control mode switching status".
"0" is stored in "[Cd.138] Control mode switching request" and "[Md.124] Control mode switching status" after completion of switching.
If "[Cd.154] Control mode auto-shift parameter" is outside the setting range, the error "Outside control mode auto-shift switching parameter range" (error code: 19E4H [FX5-SSC-S], or error code 1AE4H [FX5-SSC-G]) occurs at control mode switching request, and the current processing stops. (In the positioning control, the operation stops according to the setting of "[Pr.39] Stop group 3 sudden stop selection". In the speed control, the mode switches to the position control, and the operation immediately stops.)

> **Point**
> - Automatic switching is valid only when the control mode is switched from the position control mode to the continuous operation to torque control mode. When the mode is switched from speed control mode to continuous operation to torque control mode or from continuous operation to torque control mode to other control modes, even if the automatic switching is set, the state is not waiting for the completion of condition, and control mode switching is executed immediately.
> - When the mode switching request is executed after setting the switching condition, the state of waiting for the completion of control mode switching condition continues until the setting condition is satisfied. Therefore, if the positioning by automatic switching is interrupted, unexpected control mode switching may be executed in other positioning operations. Waiting for the completion of control mode switching condition can be cancelled by setting "Other than 1: Not request" in "[Cd.138] Control mode switching request" or by turning the axis stop signal ON. When an error occurs, waiting for the completion of control mode switching condition is also cancelled. (In both cases, "0" is stored in "[Cd.138] Control mode switching request".)
> - In the state of waiting for the completion of control mode switching condition, if the current values are updated by the current value changing, the fixed-feed control or the speed control (when "2: Clear command position to zero" is set in "[Pr.21] Command position value during speed control"), an auto-shift judgment is executed based on the updated current value. Therefore, depending on the setting condition, the mode may be switched to the continuous operation to torque control mode immediately after the positioning starts. To avoid this switching, set "1: Switching request" in "[Cd.138] Control mode switching request".

The following chart shows the operation when "1: Command position value pass" is set in "[Cd.153] Control mode auto-shift selection". (original p.205)

[Figure] Automatic switching (1: Command position value pass) from position control mode to continuous operation to torque control mode (original p.205)
- Sections: Position control mode → Continuous operation to torque control mode.
- Speed (V-t): constant speed in position control mode → figure note (verbatim): "Command position value passes the address "adr" set in "[Cd.154] Control mode auto-shift parameter"." → after the time *1, the mode switches; the axis decelerates to 1000 and runs constant → drops to 0 at "Contact with target".
- Torque: constant torque in position control mode → right after switching it goes negative momentarily, then a small positive value → after contact with the target it rises (curve) to 30.0% and stays constant.
- [Cd.138] Control mode switching request: 0 → 1 → 0 (at switching completion)
- [Cd.139] Control mode setting: ** → 30 → **
- [Cd.153] Control mode auto-shift selection: 0 → 1
- [Cd.154] Control mode auto-shift parameter: 0 → adr
- [Md.26] Axis operation status: ** → 33
- [Md.124] Control mode switching status: 0 → 2 (after the switching request, waiting for the condition) → 1 (when adr is passed) → 0
- Continuous operation to torque control ([Md.125] Servo status3: b14): OFF → ON (at switching completion)
- [Cd.147] Speed limit value at continuous operation to torque control mode: 0 → 1000
- [Cd.150] Target torque at continuous operation to torque control mode: 0 → 300
- Figure note (verbatim): "**: Depending on the control mode."
- The time from passing adr until the control mode changes is marked "*1".

*1 [FX5-SSC-S]
6 to 11 ms
[FX5-SSC-G]
The switching time varies depending on the specifications of the servo amplifier. When setting "ZSP disabled selection at control switching" of servo parameter "(Function selection C-E (PC76)" to "0: Enabled", the control mode switches after reaching Zero speed.
When the control mode of the servo amplifier does not change within 1 second, the error "Control mode switching error" (error code: 1F04H) occurs.

#### Speed control mode (速度制御モード) (6.1 / original p.206-207)

##### Operation for speed control mode (速度制御モードの動作) (6.1 / original p.206)

The speed control is executed at the speed set in "[Cd.140] Command speed at speed control mode" in the speed control mode.
Set a positive value for forward rotation and a negative value for reverse rotation. "[Cd.140]" can be changed any time during the speed control mode.
Acceleration/deceleration is performed based on a trapezoidal acceleration/deceleration processing. Set acceleration/deceleration time toward "[Pr.8] Speed limit value" in "[Cd.141] Acceleration time at speed control mode" and "[Cd.142] Deceleration time at speed control mode". The value at speed control mode switching request is valid for "[Cd.141]" and "[Cd.142]".
The command speed during the speed control mode is limited with "[Pr.8] Speed limit value". If the speed exceeding the speed limit value is set, the warning "Speed limit value over" (warning code: 0991H [FX5-SSC-S], or warning code 0D51H [FX5-SSC-G]) occurs, and the operation is controlled with the speed limit value.
Confirm the command speed to servo amplifier with "[Md.122] Speed during command".

[Figure] Operation for speed control mode (original p.206)
- Speed (V-t): 0 → accelerates to 20000, constant → accelerates to 30000, constant → decelerates to 0 → accelerates to -10000, constant → accelerates to -20000, constant → decelerates to 0.
- The acceleration slope is shown by a dashed line reaching "[Pr.8] Speed limit value" (positive and negative sides) in the time "[Cd.141] Acceleration time at speed control mode"; the deceleration slope by a dashed line from [Pr.8] to 0 in the time "[Cd.142] Deceleration time at speed control mode".
- Figure note (verbatim): "The command speed to servo amplifier is stored in "[Md.122] Speed during command"."
- [Cd.140] Command speed at speed control mode: 0 → 20000 → 30000 → 0 → -10000 → -20000 → 0

##### Command position value during speed control mode (速度制御モード中の送り現在値) (6.1 / original p.206)

"[Md.20] Command position value", "[Md.21] Machine feed value" and "[Md.101] Actual position value" are updated even in the speed control mode.
If the command position value exceeds the software stroke limit, the error "Software stroke limit +" (error code: 1993H [FX5-SSC-S], or error code 1A93H [FX5-SSC-G]) or "Software stroke limit -" (error code: 1995H [FX5-SSC-S], or error code 1A95H [FX5-SSC-G]) occurs and the operation switches to the position control mode. Invalidate the software stroke limit to execute one-way feed.

##### Stop cause during speed control mode (速度制御モード中の停止要因) (6.1 / original p.207)

The operation for stop cause during speed control mode is shown below.

| Item | Operation during speed control mode |
|---|---|
| "[Cd.180] Axis stop" turned ON. | The motor decelerates to speed "0" according to the setting value of "[Cd.142] Deceleration time at speed control mode". The mode switches to the position control mode when "Zero speed" of "[Md.119] Servo status2" turns ON, and the operation stops. |
| Stop signal of "[Cd.44] External input signal operation device (Axis 1 to 8)" turned ON. | The motor decelerates to speed "0" according to the setting value of "[Cd.142] Deceleration time at speed control mode". The mode switches to the position control mode when "Zero speed" of "[Md.119] Servo status2" turns ON, and the operation stops. |
| "[Cd.191] All axis servo ON" turned OFF. | The servo OFF is not executed during the speed control mode. The command status when the mode is switched to the position control mode becomes valid. |
| "[Cd.100] Servo OFF command" turned ON. | The servo OFF is not executed during the speed control mode. The command status when the mode is switched to the position control mode becomes valid. |
| The current value reached the software stroke limit. | One of the following errors occurs. The mode switches to the position control mode at the current position, and the operation immediately stops. (Deceleration processing is not executed.)<br>[FX5-SSC-S] Error code: 1900H, 1904H, 1906H, 1993H, 1995H<br>[FX5-SSC-G] Error code: 1A00H, 1A04H to 1A07H, 1A93H, 1A95H |
| The position of the motor reached the hardware stroke limit. | One of the following errors occurs. The mode switches to the position control mode at the current position, and the operation immediately stops. (Deceleration processing is not executed.)<br>[FX5-SSC-S] Error code: 1900H, 1904H, 1906H, 1993H, 1995H<br>[FX5-SSC-G] Error code: 1A00H, 1A04H to 1A07H, 1A93H, 1A95H |
| "[Cd.190] PLC READY" turned OFF. | One of the following errors occurs. The mode switches to the position control mode at the current position, and the operation immediately stops. (Deceleration processing is not executed.)<br>[FX5-SSC-S] Error code: 1900H, 1904H, 1906H, 1993H, 1995H<br>[FX5-SSC-G] Error code: 1A00H, 1A04H to 1A07H, 1A93H, 1A95H |
| Command discard was detected on the servo amplifier. [FX5-SSC-G] | An error (error code: 1BE6H) occurs. The mode switches to the position control mode at the current position, and the operation immediately stops. (Deceleration processing is not executed.) |
| The forced stop input to Simple Motion module/Motion module. | The mode switches to the position control mode when the servo OFF (Servo ON of "[Md.108] Servo status1" turns OFF) is executed. (While the servo amplifier is servo OFF, even if the mode is switched to position control mode, the servo motor immediately stops.) |
| The emergency stop input to servo amplifier. | The mode switches to the position control mode when the servo OFF (Servo ON of "[Md.108] Servo status1" turns OFF) is executed. (While the servo amplifier is servo OFF, even if the mode is switched to position control mode, the servo motor immediately stops.) |
| The servo alarm occurred. | The mode switches to the position control mode when the servo OFF (Servo ON of "[Md.108] Servo status1" turns OFF) is executed. (While the servo amplifier is servo OFF, even if the mode is switched to position control mode, the servo motor immediately stops.) |
| The servo amplifier's power supply turned OFF. | Stop processing of the controller is immediate stop. (The mode is set to the position control mode at the servo amplifier's power supply ON again.) |

*In the original, the "Operation during speed control mode" cell is merged over the 2 rows Axis stop / External input stop signal, the 2 rows All axis servo ON OFF / Servo OFF command ON, the 3 rows software stroke limit / hardware stroke limit / PLC READY OFF, and the 3 rows forced stop / emergency stop / servo alarm. Expanded to each row.

#### Torque control mode (トルク制御モード) (6.1 / original p.207-209)

##### Operation for torque control mode (トルク制御モードの動作) (6.1 / original p.207-208)

The torque control is executed at the command torque set in "[Cd.143] Command torque at torque control mode" in the torque control mode.
- [FX5-SSC-S]

"[Cd.143] Command torque at torque control mode" can be changed any time during torque control mode. The relation between the setting of command torque and the torque generation direction of servo motor varies depending on the setting of servo parameters "Rotation direction selection/travel direction selection (PA14)"*1 and "Function selection C-B POL reflection selection at torque control (PC29)"*2.

| Setting value of "Function selection C-B POL reflection selection at torque control (PC29)"*2 | Setting value of "Rotation direction selection/travel direction selection (PA14)"*1 | Setting value of "[Cd.143] Command torque at torque control mode" | Torque generation direction of servo motor*3 |
|---|---|---|---|
| 0: Enabled | 0: Forward rotation (CCW) with the increase of the positioning address | Positive value (Forward direction) | CCW direction |
| 0: Enabled | 0: Forward rotation (CCW) with the increase of the positioning address | Negative value (Reverse direction) | CW direction |
| 0: Enabled | 1: Reverse rotation (CW) with the increase of the positioning address | Positive value (Forward direction) | CW direction |
| 0: Enabled | 1: Reverse rotation (CW) with the increase of the positioning address | Negative value (Reverse direction) | CCW direction |
| 1: Disabled | 0: Forward rotation (CCW) with the increase of the positioning address | Positive value (Forward direction) | CCW direction |
| 1: Disabled | 0: Forward rotation (CCW) with the increase of the positioning address | Negative value (Reverse direction) | CW direction |
| 1: Disabled | 1: Reverse rotation (CW) with the increase of the positioning address | Positive value (Forward direction) | CCW direction |
| 1: Disabled | 1: Reverse rotation (CW) with the increase of the positioning address | Negative value (Reverse direction) | CW direction |

*In the original, the PC29 setting value cells are merged over 4 rows each and the PA14 setting value cells over 2 rows each. Expanded to each row.

*1 For MR-J4(W)-B. "Travel direction selection (PA14)" for MR-J5(W)-B.
*2 For MR-J4(W)-B. "Function selection C-B Torque POL reflection selection (PC29.3)" for MR-J5(W)-B.
*3 Refer to the following diagram.

[Figure] CCW direction / CW direction of the servo motor (FX5-SSC-S) (original p.207)
- Left pair: "CCW direction" — the arrow on the motor shaft and on the flange view (seen from the load (shaft) side) turns counterclockwise.
- Right pair: "CW direction" — the arrow on the motor shaft and on the flange view (seen from the load (shaft) side) turns clockwise.

- [FX5-SSC-G] (original p.208)

"[Cd.143] Command torque at torque control mode" can be changed any time during torque control mode. The relation between the setting of command torque and the torque generation direction of servo motor varies depending on the setting of servo parameters "Travel direction selection (PA14)" and "Function selection C-B Torque POL reflection selection (PC29.3)".

| Setting value of "Function selection C-B Torque POL reflection selection (PC29.3)" | Setting value of "Travel direction selection (PA14)" | Setting value of "[Cd.143] Command torque at torque control mode" | Torque generation direction of servo motor*1 |
|---|---|---|---|
| 0: Enabled | 0: Forward rotation (CCW) with the increase of the positioning address | Positive value (Forward direction) | CCW direction |
| 0: Enabled | 0: Forward rotation (CCW) with the increase of the positioning address | Negative value (Reverse direction) | CW direction |
| 0: Enabled | 1: Reverse rotation (CW) with the increase of the positioning address | Positive value (Forward direction) | CW direction |
| 0: Enabled | 1: Reverse rotation (CW) with the increase of the positioning address | Negative value (Reverse direction) | CCW direction |
| 1: Disabled | 0: Forward rotation (CCW) with the increase of the positioning address | Positive value (Forward direction) | CCW direction |
| 1: Disabled | 0: Forward rotation (CCW) with the increase of the positioning address | Negative value (Reverse direction) | CW direction |
| 1: Disabled | 1: Reverse rotation (CW) with the increase of the positioning address | Positive value (Forward direction) | CCW direction |
| 1: Disabled | 1: Reverse rotation (CW) with the increase of the positioning address | Negative value (Reverse direction) | CW direction |

*In the original, the PC29.3 setting value cells are merged over 4 rows each and the PA14 setting value cells over 2 rows each. Expanded to each row.

*1 Refer to the following diagram.

[Figure] CCW direction / CW direction of the servo motor (FX5-SSC-G) (original p.208)
- Left pair: "CCW direction" — the arrow on the motor shaft and on the flange view (seen from the load (shaft) side) turns counterclockwise.
- Right pair: "CW direction" — the arrow on the motor shaft and on the flange view (seen from the load (shaft) side) turns clockwise.

Set time for the command torque to increase from 0% to "[Pr.17] Torque limit setting value" in "[Cd.144] Torque time constant at torque control mode (Forward direction)" and for the command torque to decrease from "[Pr.17] Torque limit setting value" to 0% in "[Cd.145] Torque time constant at torque control mode (Negative direction)". The value at torque control mode switching request is valid for "[Cd.144]" and "[Cd.145]".
The command torque during the torque control mode is limited with "[Pr.17] Torque limit setting value". If the torque exceeding the torque limit setting value is set, the warning "Torque limit value over" (warning code: 09E4H [FX5-SSC-S], or warning code: 0DA4H [FX5-SSC-G]) occurs, and the operation is controlled with the torque limit setting value.
Confirm the command torque to servo amplifier with "[Md.123] Torque during command".

[Figure] Operation for torque control mode (original p.208)
- Torque [%]: 0 → rises to 20.0, constant → rises to 30.0, constant → decreases to 0 → changes to -10.0, constant → changes to -20.0, constant → returns to 0.
- The slopes are shown by dashed lines: from 0 to "[Pr.17] Torque limit setting value" (positive and negative sides) in the time "[Cd.144] Torque time constant at torque control mode (Forward direction)", and from [Pr.17] to 0 in the time "[Cd.145] Torque time constant at torque control mode (Negative direction)".
- Figure note (verbatim): "The command torque to servo amplifier is stored in "[Md.123] Torque during command"."
- [Cd.143] Command torque at torque control mode: 0 → 200 → 300 → 0 → -100 → -200 → 0

##### Speed during torque control mode (トルク制御モード中の速度) (6.1 / original p.209)

The speed during the torque control mode is controlled with "[Cd.146] Speed limit value at torque control mode". At this time, "Speed limit" ("[Md.119] Servo status2": b4) turns ON.
n: Axis No. - 1

| Monitor item | Buffer memory address |
|---|---|
| [Md.119] Servo status2: b4 | 2476+100n |

"[Cd.146] Speed limit value at torque control mode" is set to a positive value regardless of the rotation direction. (Controlled by the same value for forward and reverse directions.)
In addition, "[Cd.146] Speed limit value at torque control mode" is limited with "[Pr.8] Speed limit value". If the speed exceeding the speed limit value is set, the warning "Speed limit value over" (warning code: 0991H [FX5-SSC-S], or warning code: 0D51H [FX5-SSC-G]) occurs, and the operation is controlled with the speed limit value.
The acceleration/deceleration processing is invalid for "[Cd.146] Speed limit value at torque control mode".

> **Point**
> The actual motor speed may not reach the speed limit value depending on the machine load situation during the torque control.

##### Command position value during torque control mode (トルク制御モード中の送り現在値) (6.1 / original p.209)

"[Md.20] Command position value", "[Md.21] Machine feed value" and "[Md.101] Actual position value" are updated even in the torque control mode.
If the command position value exceeds the software stroke limit, the error "Software stroke limit +" (error code: 1993H [FX5-SSC-S], or error code: 1A93H [FX5-SSC-G]) or "Software stroke limit -" (error code: 1995H [FX5-SSC-S], or error code: 1A95H [FX5-SSC-G]) occurs and the operation switches to the position control mode. Invalidate the software stroke limit to execute one-way feed.

##### Stop cause during torque control mode (トルク制御モード中の停止要因) (6.1 / original p.209)

The operation for stop cause during torque control mode is shown below.

| Item | Operation during torque control mode |
|---|---|
| "[Cd.180] Axis stop" turned ON. | The speed limit value commanded to servo amplifier is "0" regardless of the setting value of "[Cd.146] Speed limit value at torque control mode". The mode switches to the position control mode when "Zero speed" of "[Md.119] Servo status2" turns ON, and the operation immediately stops. (Deceleration processing is not executed.)<br>The value of command torque is not changed. It might take time to reach the speed "0" depending on the current torque command value. |
| Stop signal of "[Cd.44] External input signal operation device (Axis 1 to 8)" turned ON. | The speed limit value commanded to servo amplifier is "0" regardless of the setting value of "[Cd.146] Speed limit value at torque control mode". The mode switches to the position control mode when "Zero speed" of "[Md.119] Servo status2" turns ON, and the operation immediately stops. (Deceleration processing is not executed.)<br>The value of command torque is not changed. It might take time to reach the speed "0" depending on the current torque command value. |
| "[Cd.191] All axis servo ON" turned OFF. | The servo OFF is not executed during the torque control mode. The command status when the mode is switched to the position control mode becomes valid. |
| "[Cd.100] Servo OFF command" turned ON. | The servo OFF is not executed during the torque control mode. The command status when the mode is switched to the position control mode becomes valid. |
| The current value reached the software stroke limit. | One of the following errors occurs. The mode switches to the position control mode at the current position, and the operation immediately stops. (Deceleration processing is not executed.)<br>[FX5-SSC-S] Error code: 1900H, 1904H, 1906H, 1993H, 1995H<br>[FX5-SSC-G] Error code: 1A00H, 1A04H to 1A07H, 1A93H, 1A95H |
| The position of the motor reached the hardware stroke limit. | One of the following errors occurs. The mode switches to the position control mode at the current position, and the operation immediately stops. (Deceleration processing is not executed.)<br>[FX5-SSC-S] Error code: 1900H, 1904H, 1906H, 1993H, 1995H<br>[FX5-SSC-G] Error code: 1A00H, 1A04H to 1A07H, 1A93H, 1A95H |
| "[Cd.190] PLC READY" turned OFF. | One of the following errors occurs. The mode switches to the position control mode at the current position, and the operation immediately stops. (Deceleration processing is not executed.)<br>[FX5-SSC-S] Error code: 1900H, 1904H, 1906H, 1993H, 1995H<br>[FX5-SSC-G] Error code: 1A00H, 1A04H to 1A07H, 1A93H, 1A95H |
| Command discard was detected on the servo amplifier. [FX5-SSC-G] | An error (error code: 1BE6H) occurs. The mode switches to the position control mode at the current position, and the operation immediately stops. (Deceleration processing is not executed.) |
| The forced stop input to Simple Motion module/Motion module. | The mode switches to the position control mode when the servo OFF (Servo ON of "[Md.108] Servo status1" turns OFF) is executed.<br>(While the servo amplifier is servo OFF, even if the mode is switched to position control mode, the servo motor immediately stops.) |
| The emergency stop input to servo amplifier. | The mode switches to the position control mode when the servo OFF (Servo ON of "[Md.108] Servo status1" turns OFF) is executed.<br>(While the servo amplifier is servo OFF, even if the mode is switched to position control mode, the servo motor immediately stops.) |
| The servo alarm occurred. | The mode switches to the position control mode when the servo OFF (Servo ON of "[Md.108] Servo status1" turns OFF) is executed.<br>(While the servo amplifier is servo OFF, even if the mode is switched to position control mode, the servo motor immediately stops.) |
| The servo amplifier's power supply turned OFF. | Stop processing of the controller is immediate stop. (The mode is set to the position control mode at the servo amplifier's power supply ON again.) |

*In the original, the "Operation during torque control mode" cell is merged over the 2 rows Axis stop / External input stop signal, the 2 rows All axis servo ON OFF / Servo OFF command ON, the 3 rows software stroke limit / hardware stroke limit / PLC READY OFF, and the 3 rows forced stop / emergency stop / servo alarm. Expanded to each row.

#### Continuous operation to torque control mode (押当て制御モード) (6.1 / original p.210-213)

##### Operation for continuous operation to torque control mode (押当て制御モードの動作) (6.1 / original p.210-211)

In continuous operation to torque control, the torque control can be executed without stopping the operation during the positioning in position control mode or speed command in speed control mode.
During the continuous operation to torque control mode, the torque control is executed at the command torque set in "[Cd.150] Target torque at continuous operation to torque control mode" while executing acceleration/deceleration to reach the speed set in "[Cd.147] Speed limit value at continuous operation to torque control mode".
- [FX5-SSC-S]

"[Cd.147] Speed limit value at continuous operation to torque control mode" and "[Cd.150] Target torque at continuous operation to torque control mode" can be changed any time during the continuous operation to torque control mode. The relation between the setting value of command torque and the torque generation direction of servo motor is fixed regardless of the setting of servo parameters "Rotation direction selection/travel direction selection (PA14)"*1 and "Function selection C-B POL reflection selection at torque control (PC29)"*2.

| Setting value of "Rotation direction selection/travel direction selection (PA14)"*1 | Setting value of "[Cd.150] Target torque at continuous operation to torque control mode" | Torque generation direction of servo motor*3 |
|---|---|---|
| 0: Forward rotation (CCW) with the increase of the positioning address | Positive value (Forward direction) | CCW direction |
| 0: Forward rotation (CCW) with the increase of the positioning address | Negative value (Reverse direction) | CW direction |
| 1: Reverse rotation (CW) with the increase of the positioning address | Positive value (Forward direction) | CCW direction |
| 1: Reverse rotation (CW) with the increase of the positioning address | Negative value (Reverse direction) | CW direction |

*In the original, the PA14 setting value cells are merged over 2 rows each. Expanded to each row.

*1 For MR-J4(W)-B. "Travel direction selection (PA14)" for MR-J5(W)-B.
*2 For MR-J4(W)-B. "Function selection C-B Torque POL reflection selection (PC29.3)" for MR-J5(W)-B.
*3 Refer to the following diagram.

[Figure] CCW direction / CW direction of the servo motor (continuous operation to torque control, FX5-SSC-S) (original p.210)
- Left pair: "CCW direction" — the arrow on the motor shaft and on the flange view (seen from the load (shaft) side) turns counterclockwise.
- Right pair: "CW direction" — the arrow on the motor shaft and on the flange view (seen from the load (shaft) side) turns clockwise.

> **Restriction**
> Regardless of the setting in "Rotation direction selection/travel direction selection (PA14)"*1, set a positive value when torque command is in CCW direction of servo motor and a negative value when torque command is in CW direction of servo motor in "[Cd.150] Target torque at continuous operation to torque control mode".
> If the setting is incorrect, the motor may rotate in an opposite direction.

*1 For MR-J4(W)-B. "Travel direction selection (PA14)" for MR-J5(W)-B.

> **Point**
> - Speed is not limited for reverse torque generation direction.
> - The motor rotates in a direction according to the setting in "[Cd.150] Target torque at continuous operation to torque control mode". Set the value corresponding to the motor rotation direction in "[Cd.147] Speed limit value at continuous operation to torque control mode".

- [FX5-SSC-G] (original p.211)

The relation between the setting of command torque and the torque generation direction of servo motor varies depending on the setting of servo parameters "Travel direction selection (PA14)" and "Function selection C-B Torque POL reflection selection (PC29.3)".

| Setting value of "Function selection C-B Torque POL reflection selection (PC29.3)" | Setting value of "Travel direction selection (PA14)" | Setting value of "[Cd.150] Target torque at continuous operation to torque control mode" | Torque generation direction of servo motor*1 |
|---|---|---|---|
| 0: Enabled | 0: Forward rotation (CCW) with the increase of the positioning address | Positive value (Forward direction) | CCW direction |
| 0: Enabled | 0: Forward rotation (CCW) with the increase of the positioning address | Negative value (Reverse direction) | CW direction |
| 0: Enabled | 1: Reverse rotation (CW) with the increase of the positioning address | Positive value (Forward direction) | CW direction |
| 0: Enabled | 1: Reverse rotation (CW) with the increase of the positioning address | Negative value (Reverse direction) | CCW direction |
| 1: Disabled | 0: Forward rotation (CCW) with the increase of the positioning address | Positive value (Forward direction) | CCW direction |
| 1: Disabled | 0: Forward rotation (CCW) with the increase of the positioning address | Negative value (Reverse direction) | CW direction |
| 1: Disabled | 1: Reverse rotation (CW) with the increase of the positioning address | Positive value (Forward direction) | CCW direction |
| 1: Disabled | 1: Reverse rotation (CW) with the increase of the positioning address | Negative value (Reverse direction) | CW direction |

*In the original, the PC29.3 setting value cells are merged over 4 rows each and the PA14 setting value cells over 2 rows each. Expanded to each row.

*1 Refer to the following diagram.

[Figure] CCW direction / CW direction of the servo motor (continuous operation to torque control, FX5-SSC-G) (original p.211)
- Left pair: "CCW direction" — the arrow on the motor shaft and on the flange view (seen from the load (shaft) side) turns counterclockwise.
- Right pair: "CW direction" — the arrow on the motor shaft and on the flange view (seen from the load (shaft) side) turns clockwise.

> **Point**
> Speed is not limited for reverse torque generation direction.

##### Torque command setting method (トルク指令の設定方法) (6.1 / original p.211)

During the continuous operation to torque control mode, set time for the command torque to increase from 0% to "[Pr.17] Torque limit setting value" in "[Cd.151] Torque time constant at continuous operation to torque control mode (Forward direction)" and for the command torque to decrease from "[Pr.17] Torque limit setting value" to 0% in "[Cd.152] Torque time constant at continuous operation to torque control mode (Negative direction)". The value at continuous operation to torque control mode switching request is valid for "[Cd.151]" and "[Cd.152]".
The command torque during the continuous operation to torque control mode is limited with "[Pr.17] Torque limit setting value".
If torque exceeding the torque limit setting value is commanded, the warning "Torque limit value over" (warning code: 09E4H [FX5-SSC-S], or warning code: 0DA4H [FX5-SSC-G]) occurs, and the operation is controlled with the torque limit setting value.
Confirm the command torque to servo amplifier with "[Md.123] Torque during command".
During the continuous operation to torque control mode, "Torque limit" ([Md.108] Servo status1: b13) does not turn ON. Confirm the current torque value in "[Md.104] Motor current value".
n: Axis No. - 1

| Monitor item | Buffer memory address |
|---|---|
| [Md.108] Servo status1: b13 | 2477+100n |

##### Speed limit value setting method (速度制限値の設定方法) (6.1 / original p.212)

Acceleration/deceleration is performed based on a trapezoidal acceleration/deceleration processing.
Set acceleration/deceleration time toward "[Pr.8] Speed limit value" in "[Cd.148] Acceleration time at continuous operation to torque control mode" and "[Cd.149] Deceleration time at continuous operation to torque control mode". The value at continuous operation to torque control mode switching is valid for "[Cd.148]" and "[Cd.149]".
"[Cd.147] Speed limit value at continuous operation to torque control mode" is limited with "[Pr.8] Speed limit value". If the speed exceeding the speed limit value is commanded, the warning "Speed limit value over" (warning code: 0991H [FX5-SSC-S], or warning code: 0D51H [FX5-SSC-G]) occurs, and the operation is controlled with the speed limit value.
Confirm the command speed to servo amplifier with "[Md.122] Speed during command".

[Figure] Speed limit value and torque in continuous operation to torque control mode (original p.212)
- Sections: Position control mode or Speed control mode → Continuous operation to torque control mode → Position control mode or Speed control mode.
- Speed (V-t): constant speed before switching → after switching, decelerates to 1000 with the slope defined by "[Cd.149] Deceleration time at continuous operation to torque control mode" (time from "[Pr.8] Speed limit value" to 0) and runs constant → drops to 0 at "Contact with target". "[Pr.8] Speed limit value" is shown on the positive and negative sides.
- Torque: constant torque before switching → right after switching it goes negative momentarily, then a small positive value → after contact with the target it rises (curve) to 30.0% and stays constant (below "[Pr.17] Torque limit setting value", shown on the positive and negative sides) → drops to 0 at the end of the continuous operation to torque control mode.
- [Cd.147] Speed limit value at continuous operation to torque control mode: 0 → 1000 → 0
- [Cd.150] Target torque at continuous operation to torque control mode: 0 → 300 → 0

##### Precautions at continuous operation to torque control mode (押当て制御モード時の注意事項) (6.1 / original p.212)

For functions of the servo amplifier that are not available during the continuous operation to torque control mode, refer to the manuals of each servo amplifier to be connected.

> **Point**
> If vibration occurs during the continuous operation to torque control, lower the value of the servo parameter "Torque feedback loop gain (PB03)" and check if the issue has been solved.

> **Restriction**
> Set the system configuration with an unlimited operation range during the continuous operation to torque control mode as a stroke limit signal of the servo amplifier cannot be used during the continuous operation to torque control mode.
> Use the software stroke limit function on the Simple Motion module/Motion module side to restrict the set position.

##### Speed during continuous operation to torque control mode (押当て制御モード中の速度) (6.1 / original p.213)

The speed during the continuous operation to torque control mode is controlled with an absolute value of the value set in "[Cd.147] Speed limit value at continuous operation to torque control mode" as command speed. When the speed reaches the absolute value of "[Cd.147] Speed limit value at continuous operation to torque control mode", "Speed limit" ([Md.119] Servo status2: b4) turns ON.
n: Axis No. - 1

| Monitor item | Buffer memory address |
|---|---|
| [Md.119] Servo status2: b4 | 2476+100n |

In addition, "[Cd.147] Speed limit value at continuous operation to torque control mode" is limited with "[Pr.8] Speed limit value". If the command speed exceeding the speed limit value is set, the warning "Speed limit value over" (warning code: 0991H [FX5-SSC-S], or warning code: 0D51H [FX5-SSC-G]) occurs, and the operation is controlled with the speed limit value.

> **Point**
> The actual motor speed may not reach the command speed depending on the machine load situation during the continuous operation to torque control mode.

##### Command position value during continuous operation to torque control mode (押当て制御モード中の送り現在値) (6.1 / original p.213)

"[Md.20] Command position value", "[Md.21] Machine feed value" and "[Md.101] Actual position value" are updated even in the continuous operation to torque control mode.
If the command position value exceeds the software stroke limit, the error "Software stroke limit +" (error code: 1993H [FX5-SSC-S], or error code: 1A93H [FX5-SSC-G]) or "Software stroke limit -" (error code: 1995H [FX5-SSC-S], or error code: 1A95H [FX5-SSC-G]) occurs and the operation switches to the position control mode. Invalidate the software stroke limit to execute one-way feed.

##### Stop cause during continuous operation to torque control mode (押当て制御モード中の停止要因) (6.1 / original p.213)

The operation for stop cause during continuous operation to torque control mode is shown below.

| Item | Operation during continuous operation to torque control mode |
|---|---|
| "[Cd.180] Axis stop" turned ON. | The speed limit value commanded to servo amplifier is "0" regardless of the setting value of "[Cd.147] Speed limit value at continuous operation to torque control mode". The mode switches to the position control mode when "Zero speed" of "[Md.119] Servo status2" turns ON, and the operation immediately stops. (Deceleration processing is not executed.)<br>The value of command torque is not changed. It might take time to reach the speed "0" depending on the current torque command value. |
| Stop signal of "[Cd.44] External input signal operation device (Axis 1 to 8)" turned ON. | The speed limit value commanded to servo amplifier is "0" regardless of the setting value of "[Cd.147] Speed limit value at continuous operation to torque control mode". The mode switches to the position control mode when "Zero speed" of "[Md.119] Servo status2" turns ON, and the operation immediately stops. (Deceleration processing is not executed.)<br>The value of command torque is not changed. It might take time to reach the speed "0" depending on the current torque command value. |
| "[Cd.191] All axis servo ON" turned OFF. | The servo OFF is not executed during the continuous operation to torque control mode. The command status when the mode is switched to the position control mode becomes valid. |
| "[Cd.100] Servo OFF command" turned ON. | The servo OFF is not executed during the continuous operation to torque control mode. The command status when the mode is switched to the position control mode becomes valid. |
| The current value reached the software stroke limit. | One of the following errors occurs. The mode switches to the position control mode at the current position, and the operation immediately stops. (Deceleration processing is not executed.)*1<br>[FX5-SSC-S] Error code: 1900H, 1904H, 1906H, 1993H, 1995H<br>[FX5-SSC-G] Error code: 1A00H, 1A04H to 1A07H, 1A93H, 1A95H<br>When the operation immediately stops, the motor may start hunting depending on the motor speed. Therefore, be sure not to reach the limit in high speed and not to turn OFF the "[Cd.190] PLC READY". |
| The position of the motor reached the hardware stroke limit. | One of the following errors occurs. The mode switches to the position control mode at the current position, and the operation immediately stops. (Deceleration processing is not executed.)*1<br>[FX5-SSC-S] Error code: 1900H, 1904H, 1906H, 1993H, 1995H<br>[FX5-SSC-G] Error code: 1A00H, 1A04H to 1A07H, 1A93H, 1A95H<br>When the operation immediately stops, the motor may start hunting depending on the motor speed. Therefore, be sure not to reach the limit in high speed and not to turn OFF the "[Cd.190] PLC READY". |
| "[Cd.190] PLC READY" turned OFF. | One of the following errors occurs. The mode switches to the position control mode at the current position, and the operation immediately stops. (Deceleration processing is not executed.)*1<br>[FX5-SSC-S] Error code: 1900H, 1904H, 1906H, 1993H, 1995H<br>[FX5-SSC-G] Error code: 1A00H, 1A04H to 1A07H, 1A93H, 1A95H<br>When the operation immediately stops, the motor may start hunting depending on the motor speed. Therefore, be sure not to reach the limit in high speed and not to turn OFF the "[Cd.190] PLC READY". |
| Command discard was detected on the servo amplifier. [FX5-SSC-G] | An error (error code: 1BE6H) occurs. The mode switches to the position control mode at the current position, and the operation immediately stops. (Deceleration processing is not executed.)<br>When the operation immediately stops, the motor may start hunting depending on the motor speed. Therefore, be sure not to reach the limit in high speed and not to turn OFF the "[Cd.190] PLC READY". |
| The forced stop input to Simple Motion module/Motion module. | The mode switches to the position control mode when the servo OFF (Servo ON of "[Md.108] Servo status1" turns OFF) is executed.*1<br>(While the servo amplifier is servo OFF, even if the mode is switched to position control mode, the servo motor immediately stops.) |
| The emergency stop input to servo amplifier. | The mode switches to the position control mode when the servo OFF (Servo ON of "[Md.108] Servo status1" turns OFF) is executed.*1<br>(While the servo amplifier is servo OFF, even if the mode is switched to position control mode, the servo motor immediately stops.) |
| The servo alarm occurred. | The mode switches to the position control mode when the servo OFF (Servo ON of "[Md.108] Servo status1" turns OFF) is executed.*1<br>(While the servo amplifier is servo OFF, even if the mode is switched to position control mode, the servo motor immediately stops.) |
| The servo amplifier's power supply turned OFF. | Stop processing of the controller is immediate stop. (The mode is set to the position control mode at the servo amplifier's power supply ON again.) |

*In the original, the "Operation during continuous operation to torque control mode" cell is merged over the 2 rows Axis stop / External input stop signal, the 2 rows All axis servo ON OFF / Servo OFF command ON, the 3 rows software stroke limit / hardware stroke limit / PLC READY OFF, and the 3 rows forced stop / emergency stop / servo alarm. Expanded to each row.

*1 When the mode has switched from the speed control mode to the continuous operation to torque control mode, the mode switches to the position control mode after switching the speed control mode once. Therefore, it takes the following time to switch to the position control mode.
Switching time for the speed control mode + Switching time for the position control mode

### Servo OFF command valid function during speed-torque control [FX5-SSC-G] (速度・トルク制御中のサーボOFF指令有効機能[FX5-SSC-G]) (6.1 / original p.214-218)

"Servo OFF command valid function" is the function that enables "[Cd.100] Servo OFF command" and "[Cd.191] All axis servo ON" to be accepted during the speed control mode, the torque control mode, and the continuous operation to torque control mode.
When using this function, servo amplifiers can be set to servo OFF without using dynamic brake.
It is possible to select valid or invalid on "[Cd.100] Servo OFF command" and "[Cd.191] All axis servo ON" during speed/torque/continuous operation to torque control by selecting "[Pr.112] Servo OFF command valid/invalid setting". When "1: Servo OFF command in speed/torque control valid" is set to "[Pr.112] Servo OFF command valid/invalid setting", the servo OFF command will be valid. When "0: Servo OFF Command Invalid" is set to "[Pr.112] Servo OFF command valid/invalid setting", the servo OFF command will be invalid.
The setting value of "[Pr.112] Servo OFF command valid/invalid setting" is to be valid at control mode switching.
At servo OFF command valid, the target axis is set to be servo OFF when "1: Servo OFF" is set to "[Cd.100] Servo OFF command" or "[Cd.191] All axis servo ON" is set to OFF. The control mode during servo OFF carries over the control mode at servo OFF command execution.

#### Precautions (注意事項) (6.1 / original p.214)

For a safe operation, execute "[Cd. 100] Servo OFF command" while not braking with the dynamic brake and turning servo OFF will not cause any problems.

#### Relevant buffer memory (関連するバッファメモリ) (6.1 / original p.214)

##### Detailed parameter 2 (詳細パラメータ2) (6.1 / original p.214)

n: Axis No. -1

| Setting item | Setting value (bit) | Setting value | Buffer memory address (Axis 1 to axis 8) |
|---|---|---|---|
| [Pr.112] Servo OFF command valid/invalid setting*1 | bit0 | 0: Servo OFF command invalid<br>1: Servo OFF command in speed/torque control valid | 112+150n |
| [Pr.112] Servo OFF command valid/invalid setting*1 | bit1 or later | Not used*2 | 112+150n |

*In the original, the "Setting value" header spans 2 columns, "Buffer memory address" has the sub-header "Axis 1 to axis 8", and the Setting item and Buffer memory address cells are merged over the 2 rows. Expanded to each row.

*1 Saved to the flash ROM by Flash ROM write by the "[Cd.1] Flash ROM write request" or the engineering tool.
*2 When other than bit0 is ON, it operates with the setting "0: Servo OFF Command Invalid".

##### Axis control data (軸制御データ) (6.1 / original p.214)

n: Axis No. -1

| Setting item | Setting detail | Buffer memory address (Axis 1 to axis 8) |
|---|---|---|
| [Cd.100] Servo OFF command | 0: Servo ON<br>1: Servo OFF | 4351+100n |
| [Cd.191] All axis servo ON | 0: Servo OFF<br>1: Servo ON | 5951 |

*In the original, "Buffer memory address" has the sub-header "Axis 1 to axis 8".

#### Stop cause (停止要因) (6.1 / original p.215-216)

When "1: Servo OFF command in speed/torque control valid" is set to "[Pr.112] Servo OFF command valid/invalid setting", the operation at stop cause occurrence is as follows.

##### Stop cause during speed control mode (速度制御モード中の停止要因) (6.1 / original p.215)

| Setting item | Operation during speed control mode |
|---|---|
| "[Cd.180] Axis stop" turned ON. | The motor decelerates to speed "0" according to the setting value of "[Cd.142] Deceleration time at speed control mode". The mode switches to the position control mode when "Zero speed" of "[Md.119] Servo status 2" turns ON, and the operation stops.<br>During Servo OFF, the stop signal is not accepted even if "[Cd.180] Axis stop" turned ON. |
| Stop signal of "[Cd.44] External input signal operation device" turned ON. | The motor decelerates to speed "0" according to the setting value of "[Cd.142] Deceleration time at speed control mode". The mode switches to the position control mode when "Zero speed" of "[Md.119] Servo status 2" turns ON, and the operation stops.<br>During Servo OFF, the stop signal is not accepted even if "[Cd.180] Axis stop" turned ON. |
| "[Cd.191] All axis servo ON" turned OFF. | The servo turned OFF and the speed control mode will continue. It will be braked by the dynamic brake at the stop by the servo OFF.<br>The speed control mode can be continued after servo ON. |
| "[Cd.100] Servo OFF command" turned OFF. | The servo turned OFF and the speed control mode will continue. It will not be braked by the dynamic brake at the stop by the servo OFF.<br>The speed control mode can be continued after servo ON. |
| The current value reached the software stroke limit. | An error (error code: 1A00H, 1A04H to 1A07H, 1A93H, 1A95H, 1BE6H) occurs. The mode switches to the position control mode at the current position, and the operation immediately stops. (Deceleration processing is not executed.)<br>While the servo amplifier is servo OFF, an error does not occur even if any operation on the left is performed. |
| The position of the motor reached the hardware stroke limit. | An error (error code: 1A00H, 1A04H to 1A07H, 1A93H, 1A95H, 1BE6H) occurs. The mode switches to the position control mode at the current position, and the operation immediately stops. (Deceleration processing is not executed.)<br>While the servo amplifier is servo OFF, an error does not occur even if any operation on the left is performed. |
| "[Cd.190] PLC READY" turned OFF. | An error (error code: 1A00H, 1A04H to 1A07H, 1A93H, 1A95H, 1BE6H) occurs. The mode switches to the position control mode at the current position, and the operation immediately stops. (Deceleration processing is not executed.)<br>While the servo amplifier is servo OFF, an error does not occur even if any operation on the left is performed. |
| Command discard was detected on the servo amplifier. | An error (error code: 1A00H, 1A04H to 1A07H, 1A93H, 1A95H, 1BE6H) occurs. The mode switches to the position control mode at the current position, and the operation immediately stops. (Deceleration processing is not executed.)<br>While the servo amplifier is servo OFF, an error does not occur even if any operation on the left is performed. |
| The forced stop input to Motion module. | Stop processing of the controller is immediate stop. (Speed control mode will continue. It can be possible to continue after the cause is removed.) |
| The emergency stop input to servo amplifier. | Stop processing of the controller is immediate stop. (Speed control mode will continue. It can be possible to continue after the cause is removed.) |
| The servo alarm occurred. | The mode switches to the position control mode when the servo OFF (Servo ON of "[Md.108] Servo status 1" turns OFF) is executed. (While the servo amplifier is servo OFF, even if the mode is switched to position control mode, the servo motor immediately stops.) |
| The servo amplifier's power supply turned OFF. | Stop processing of the controller is immediate stop. (The mode is set to the position control mode at the servo amplifier's power supply ON again.) |

*In the original, the "Operation during speed control mode" cell is merged over the 2 rows Axis stop / External input stop signal, the 4 rows software stroke limit / hardware stroke limit / PLC READY OFF / command discard, and the 2 rows forced stop / emergency stop. Expanded to each row. The row '"[Cd.100] Servo OFF command" turned OFF.' is as printed in the original (the torque control mode table has "turned ON").

##### Stop cause during torque control mode (トルク制御モード中の停止要因) (6.1 / original p.215)

| Setting item | Operation during torque mode |
|---|---|
| "[Cd.180] Axis stop" turned ON. | The speed limit value commanded to servo amplifier is "0" regardless of the setting value of "[Cd.146] Speed limit value at torque control mode". The mode switches to the position control mode when "Zero speed" of "[Md.119] Servo status 2" turns ON, and the operation immediately stops. (Deceleration processing is not executed.)<br>The value of command torque is not changed. It might take time to reach the speed "0" depending on the current torque command value. During Servo OFF, the stop signal is not accepted even if "[Cd.180] Axis stop" turned ON. |
| Stop signal of "[Cd.44] External input signal operation device" turned ON. | The speed limit value commanded to servo amplifier is "0" regardless of the setting value of "[Cd.146] Speed limit value at torque control mode". The mode switches to the position control mode when "Zero speed" of "[Md.119] Servo status 2" turns ON, and the operation immediately stops. (Deceleration processing is not executed.)<br>The value of command torque is not changed. It might take time to reach the speed "0" depending on the current torque command value. During Servo OFF, the stop signal is not accepted even if "[Cd.180] Axis stop" turned ON. |
| "[Cd.191] All axis servo ON" turned OFF. | The servo turned OFF and the torque control mode will continue. It will be braked by the dynamic brake at the stop by the servo OFF. The torque control mode can be continued after servo ON. |
| "[Cd.100] Servo OFF command" turned ON. | The servo turned OFF and the torque control mode will continue. It will not be braked by the dynamic brake at the stop by the servo OFF. The torque control mode can be continued after servo ON. |
| The current value reached the software stroke limit. | An error (error code: 1A00H, 1A04H to 1A07H, 1A93H, 1A95H, 1BE6H) occurs. The mode switches to the position control mode at the current position, and the operation immediately stops. (Deceleration processing is not executed.)<br>While the servo amplifier is servo OFF, an error does not occur even if any operation on the left is performed. |
| The position of the motor reached the hardware stroke limit. | An error (error code: 1A00H, 1A04H to 1A07H, 1A93H, 1A95H, 1BE6H) occurs. The mode switches to the position control mode at the current position, and the operation immediately stops. (Deceleration processing is not executed.)<br>While the servo amplifier is servo OFF, an error does not occur even if any operation on the left is performed. |
| "[Cd.190] PLC READY" turned OFF. | An error (error code: 1A00H, 1A04H to 1A07H, 1A93H, 1A95H, 1BE6H) occurs. The mode switches to the position control mode at the current position, and the operation immediately stops. (Deceleration processing is not executed.)<br>While the servo amplifier is servo OFF, an error does not occur even if any operation on the left is performed. |
| Command discard was detected on the servo amplifier. | An error (error code: 1A00H, 1A04H to 1A07H, 1A93H, 1A95H, 1BE6H) occurs. The mode switches to the position control mode at the current position, and the operation immediately stops. (Deceleration processing is not executed.)<br>While the servo amplifier is servo OFF, an error does not occur even if any operation on the left is performed. |
| The forced stop input to Motion module. | Stop processing of the controller is immediate stop. (Torque control mode will continue after the cause is removed.) |
| The emergency stop input to servo amplifier. | Stop processing of the controller is immediate stop. (Torque control mode will continue after the cause is removed.) |
| The servo alarm occurred. | The mode switches to the position control mode when the servo OFF (Servo ON of "[Md.108] Servo status 1" turns OFF) is executed. (While the servo amplifier is servo OFF, even if the mode is switched to position control mode, the servo motor immediately stops. |
| The servo amplifier's power supply turned OFF. | Stop processing of the controller is immediate stop. (The mode is set to the position control mode at the servo amplifier's power supply ON again.) |

*In the original, the "Operation during torque mode" cell is merged over the 2 rows Axis stop / External input stop signal, the 4 rows software stroke limit / hardware stroke limit / PLC READY OFF / command discard, and the 2 rows forced stop / emergency stop. Expanded to each row. The missing closing parenthesis in the servo alarm row is as printed in the original.

##### Stop cause during continuous operation to torque control mode (押当て制御モード中の停止要因) (6.1 / original p.216)

| Item | Operation during continuous operation to torque control mode |
|---|---|
| "[Cd.180] Axis stop" turned ON. | The speed limit value commanded to servo amplifier is "0" regardless of the setting value of "[Cd.147] Speed limit value at continuous operation to torque control mode". The mode switches to the position control mode when "Zero speed" of "[Md.119] Servo status 2" turns ON, and the operation immediately stops. (Deceleration processing is not executed.)<br>The value of command torque is not changed. It might take time to reach the speed "0" depending on the current torque command value. |
| Stop signal of "[Cd.44] External input signal operation device" turned ON. | The speed limit value commanded to servo amplifier is "0" regardless of the setting value of "[Cd.147] Speed limit value at continuous operation to torque control mode". The mode switches to the position control mode when "Zero speed" of "[Md.119] Servo status 2" turns ON, and the operation immediately stops. (Deceleration processing is not executed.)<br>The value of command torque is not changed. It might take time to reach the speed "0" depending on the current torque command value. |
| "[Cd.191] All axis servo ON" turned OFF. | The servo turned OFF and the continuous control to torque control mode will continue. It will be braked by dynamic brake at the stop by the servo OFF. The continuous control to torque control can be continued after servo ON. |
| "[Cd.100] Servo OFF command" turned ON. | The servo turned OFF and the continuous control to torque control mode will continue. It will not be braked by dynamic brake at the stop by the servo OFF. The continuous operation to torque control can be continued after servo ON. |
| The current value reached the software stroke limit. | An error (error code: 1A00H, 1A04H to 1A07H, 1A93H, 1A95H, 1BE6H) occurs. The mode switches to the position control mode at the current position, and the operation immediately stops. (Deceleration processing is not executed.) When the operation immediately stops, the motor may start hunting depending on the motor speed. Therefore, be sure not to reach the limit in high speed and not to turn OFF "[Cd.190] PLC READY".<br>While the servo amplifier is servo OFF, an error does not occur even if any operation on the left is performed. |
| The position of the motor reached the hardware stroke limit. | An error (error code: 1A00H, 1A04H to 1A07H, 1A93H, 1A95H, 1BE6H) occurs. The mode switches to the position control mode at the current position, and the operation immediately stops. (Deceleration processing is not executed.) When the operation immediately stops, the motor may start hunting depending on the motor speed. Therefore, be sure not to reach the limit in high speed and not to turn OFF "[Cd.190] PLC READY".<br>While the servo amplifier is servo OFF, an error does not occur even if any operation on the left is performed. |
| "[Cd.190] PLC READY" turned OFF. | An error (error code: 1A00H, 1A04H to 1A07H, 1A93H, 1A95H, 1BE6H) occurs. The mode switches to the position control mode at the current position, and the operation immediately stops. (Deceleration processing is not executed.) When the operation immediately stops, the motor may start hunting depending on the motor speed. Therefore, be sure not to reach the limit in high speed and not to turn OFF "[Cd.190] PLC READY".<br>While the servo amplifier is servo OFF, an error does not occur even if any operation on the left is performed. |
| Command discard was detected on the servo amplifier. | An error (error code: 1A00H, 1A04H to 1A07H, 1A93H, 1A95H, 1BE6H) occurs. The mode switches to the position control mode at the current position, and the operation immediately stops. (Deceleration processing is not executed.) When the operation immediately stops, the motor may start hunting depending on the motor speed. Therefore, be sure not to reach the limit in high speed and not to turn OFF "[Cd.190] PLC READY".<br>While the servo amplifier is servo OFF, an error does not occur even if any operation on the left is performed. |
| The forced stop input to Motion module. | Stop processing of the controller is immediate stop. (Torque control mode will continue. It can be possible to continue after the cause is removed.) |
| The emergency stop input to servo amplifier. | Stop processing of the controller is immediate stop. (Torque control mode will continue. It can be possible to continue after the cause is removed.) |
| The servo alarm occurred. | The mode switches to the position control mode when the servo OFF (Servo ON of "[Md.108] Servo status 1" turns OFF) is executed. (While the servo amplifier is servo OFF, even if the mode is switched to position control mode, the servo motor immediately stops.) |
| The servo amplifier's power supply turned OFF. | Stop processing of the controller is immediate stop. (The mode is set to the position control mode at the servo amplifier's power supply ON again.) |

*In the original, the "Operation during continuous operation to torque control mode" cell is merged over the 2 rows Axis stop / External input stop signal, the 4 rows software stroke limit / hardware stroke limit / PLC READY OFF / command discard, and the 2 rows forced stop / emergency stop. Expanded to each row.

#### Operation timing (動作タイミング) (6.1 / original p.216-217)

The following shows the operation of the speed torque control mode in case of setting "1: Servo OFF Command in Speed/Torque Control Valid Function" in "[Pr.112] Servo OFF command valid/invalid setting". The operation at torque control mode or continuous operation to torque control mode is the same as that operation.

[Figure] Operation timing of speed control mode with servo OFF command valid (original p.216)
- Speed (v-t): after switching to speed control mode, accelerates to 200.00 r/min and runs constant → when [Cd.100] Servo OFF command = 1 (servo OFF), the speed falls to 0 → after [Cd.100] = 0 (servo ON), accelerates again toward 200.00 r/min → decelerates to 0 when [Cd.140] = 0.
- [Cd.138] Control mode switching request: 0 → 1 → 0 → 1 → 0 (from the switching request to switching completion: "6 to 8 ms*1", both switchings)
- [Cd.139] Control mode setting: 0 → 10 → 0
- [Cd.140] Command speed at speed control mode: 0 → 2000 → 0
- BUSY signal: OFF → ON → OFF
- [Md.26] Axis operation status: 0 → 30 → 31 → 30 → 0
- Control mode ([Md.108] Servo status 1: b2, b3): [0, 0] → [0, 1] → [0, 0] (as shown in the figure)
- [Pr.112] Servo OFF command valid/invalid setting: 0 → 1
- [Cd.100] Servo OFF command: 0 → 1 → 0
- Servo ON ([Md.108] Servo status 1: b1): ON → OFF (while [Cd.100] = 1) → ON

*1 Switching time differs depending on the specification of the servo amplifier.

- The following shows the operation in case of switching from the position control mode to speed control mode during servo OFF command. The operation when switching from the position control mode to torque control mode or continuous operation to torque control mode is the same as that operation.

[Figure] Switching from position control mode to speed control mode during servo OFF command (original p.217)
- [Cd.138] Control mode switching request: 0 → 1 → 0 (from the switching request to switching completion: "6 to 8 ms*1")
- [Cd.139] Control mode setting: 0 → 10
- BUSY signal: OFF → ON
- [Md.26] Axis operation status: 0 → 21 → 30 → 31
- Control mode ([Md.108] Servo status 1: b2, b3): [0, 0] → [0, 1] (as shown in the figure)
- [Pr.112] Servo OFF command valid/invalid setting: 0 → 1
- [Cd.100] Servo OFF command: 0 → 1 → 0
- Servo ON ([Md.108] Servo status 1: b1): ON → OFF (while [Cd.100] = 1) → ON

*1 Switching time differs depending on the specification of the servo amplifier.

#### Control mode switching during servo OFF (サーボOFF中の制御モード切換え) (6.1 / original p.217)

The position control mode can be switched to speed-torque-continuous operation to torque control mode, and the speed control mode ⇔ torque control mode switching*1 can be performed during servo OFF in case of setting "1: Servo OFF Command in Speed/Torque Control Valid Function" in "[Pr.112] Servo OFF command valid/invalid setting".
The control mode cannot be switched during continuous operation to torque control mode.

[Figure] Control mode switching during servo OFF (original p.217)
- Position control mode → (Speed control mode / Torque control mode / Continuous operation to torque control mode): ○ (possible)
- (Speed control mode / Torque control mode / Continuous operation to torque control mode) → Position control mode: × — figure note (verbatim): Warning "Control mode switching not possible" (warning: 0DABH) detection
- Speed control mode ⇔ Torque control mode: ○*1
- Speed control mode ⇔ Continuous operation to torque control mode and Torque control mode ⇔ Continuous operation to torque control mode: × — figure note (verbatim): Warning "Control mode switching not possible" (warning: 0DABH) detection
- (The box label reads "Continuous operation to" in the figure, as printed.)

*1 The operation differs depending on the software version.

| Software version | Operation |
|---|---|
| 1.003 or later | The speed control mode ⇔ torque control mode switching during servo OFF is possible. |
| 1.002 or earlier | For the speed control mode ⇔ torque control mode switching during servo OFF, the warning "Control mode switching not possible" (warning code: 0DABH) is detected. |

#### Precautions during operation (制御上の注意事項) (6.1 / original p.218)

- When the speed control or torque control, the control mode cannot be switched to during servo OFF. If "1: Switching request" is set in "[Cd.138] Control mode switching request", the warning "Control mode switching not possible" (warning code: 0DABH) will be detected. However, in case of satisfying the following conditions, switching from speed-torque control mode to continuous operation to torque control mode can be possible during servo OFF.
  - "[Md.26] Axis operation status" is standstill or stopping
  - "[Cd.180] Axis stop" is OFF
  - No error occurred
  - Driver communication function is not used [FX5-SSC-S]
- In the continuous operation to torque control mode, the control mode cannot be switched during servo OFF. If "1: Switching request" is set in "[Cd.138] Control mode switching request", the warning "Control mode switching not possible" (warning code: 0DABH) will be detected. However, in case of satisfying the following conditions, switching from continuous operation to torque control mode to speed control mode can be possible.
  - The current control mode is continuous operation to torque control mode and the previous control mode is positioning control mode
  - During zero speed ([Md.119] Servo status 2: b3) is OFF
  - Servo amplifier is connected
  - No immediately stop cause
  - "1: ON conditions invalid during zero speed at mode switching" is set in "Condition selection at mode switching (b12 to b15)" of "[Pr.90] Operation setting for speed-torque control mode". [FX5-SSC-S]
  - "1: According to the Servo Amplifier Specification" is set in "Condition selection at mode switching (b12 to b15)" of "[Pr.90] Operation setting for speed-torque control mode" and also "ZSP disabled selection at control switching" of MR-J5-G servo parameter "Function selection C-E (PC76)" is "1: Disabled". [FX5-SSC-G]
- When the setting is "[Md.26] Axis operation status" is "30: Control mode switch" or "[Md.124] Control mode switching status" is other than "0: Not during control mode switching", the servo OFF command will not be accepted. Request the servo OFF command after completing the control mode switching.
- If the value other than "0: Servo OFF Command Invalid" or "1: Servo OFF Command in Speed/Torque Control Valid" is set in "[Pr.112] Servo OFF command valid/invalid setting", it will be processed as "0: Servo OFF command invalid".
- The immediate stop cannot be accepted after the servo OFF. However, if the stop cause is the cause involved with switching to position control mode, the control mode will be switched to position control mode.
- When the axis is stopped with the servo OFF status during speed-torque-continuous operation to torque control mode, the operation of the each control mode will be restarted at the point of removing the stop causes.
- When "1: Servo OFF Command in Speed/Torque Control Valid" is set in "[Pr.112] Servo OFF command valid/invalid setting" and it becomes servo OFF by "[Cd.100] Servo OFF command", dynamic brake is not performed. Make sure that there is no problem even the servo motor is not braked by the dynamic brake and then execute "[Cd.100] Servo OFF command" because it is dangerous.

## 6.2 Advanced Synchronous Control (アドバンスト同期制御) (6.2 / original p.219)

"Advanced synchronous control" can be achieved using software instead of controlling mechanically with gear, shaft, speed change gear or cam, etc.
"Advanced synchronous control" synchronizes movement with the input axis (servo input axis, command generation axis, or synchronous encoder axis), by setting "the parameters for advanced synchronous control" and starting synchronous control on each output axis.
Refer to the following for details of advanced synchronous control.
[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Advanced Synchronous Control)

(No program example body in this chapter.)
