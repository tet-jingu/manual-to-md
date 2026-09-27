# 2 HOME POSITION RETURN CONTROL (原点復帰制御) (Chapter 2 / original p.38-59)

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

## Conversion range (変換範囲表 / original p.38-59)

| Original page | Section | Handling |
|---|---|---|
| p.38-40 | 2.1 Outline of Home Position Return Control | Full text |
| p.41-56 | 2.2 Machine Home Position Return | Full text |
| p.57-58 | 2.3 Fast Home Position Return | Full text |
| p.59 | 2.4 Selection of the Home Position Return Setting Condition | Full text |

## Table of Contents (目次)

- 2 HOME POSITION RETURN CONTROL (原点復帰制御)
- 2.1 Outline of Home Position Return Control (原点復帰制御の概要)
- 2.2 Machine Home Position Return (機械原点復帰)
- 2.3 Fast Home Position Return (高速原点復帰)
- 2.4 Selection of the Home Position Return Setting Condition (原点セット条件選択)

---

## 2 HOME POSITION RETURN CONTROL (原点復帰制御) (Chapter 2 / original p.38)

The details and usage of "home position return control" are explained in this chapter.

## 2.1 Outline of Home Position Return Control (原点復帰制御の概要) (2.1 / original p.38-40)

### Two types of home position return control (2つの原点復帰制御) (2.1 / original p.38)

In "home position return control", a position is established as the starting point (or "home position") when carrying out positioning control, and positioning is carried out toward that starting point.
It is used to return a machine system at any position other than the home position to the home position when the Simple Motion module/Motion module issues a "home position return request" with the power turned ON or others, or after a positioning stop.
In the Simple Motion module/Motion module, the following two control types are defined as "home position return control", following the flow of the home position return work. These two types of home position return control can be executed by setting the "home position return parameters", setting "Positioning start No.9001" and "positioning start No.9002" prepared beforehand in the Simple Motion module/Motion module to "[Cd.3] Positioning start No.", and turning ON the positioning start signal.

| Home position return method | Home position return method operation details |
|---|---|
| Machine home position return (positioning start No.9001) | Executes the home position return operation to establish a machine home position. The following positioning control is executed based on the home position established by the home position return completion. The machine home position return is required when the machine home position has not been established (the current value monitor of the Simple Motion module/Motion module and the actual machine position are not matched) due to the power supply ON of the system, etc. |
| Fast home position return (positioning start No.9002) | Executes the positioning to the home position established by a machine home position return. The fast home position return is operated by specifying the positioning start No.9002, so that the positioning which returns to the home position can be executed without setting the positioning data. |

The "machine home position return" above must be carried out in advance to execute the "fast home position return".

> **CAUTION**
> - When using an absolute position system, execute a home position return always at the following cases: on starting up and when the controller or absolute position motor has been replaced. Check the home position return request signal using the program, etc. before performing the positioning control. Failure to observe this could lead to an accident such as a collision.

The address information stored in the Simple Motion module/Motion module cannot be guaranteed while the "home position return request flag" is ON.
The "home position return request flag" turns OFF and the "home position return complete flag" ([Md.31] Status: b4) turns ON if the machine home position return is executed and is completed normally.
The "home position return request flag" ([Md.31] Status: b3) must be turned ON in the Simple Motion module/Motion module, and a machine home position return must be executed in the following cases.

### When not using an absolute position system (絶対位置システムでないとき) (2.1 / original p.38)

- This flag turns on in the following cases:
  - System's power supply on or reset
  - Servo amplifier power supply on
  - Machine home position return start (Unless a machine home position return is completed normally, the home position return request flag does not turn off.)
  - [FX5-SSC-G]
    - When "Electronic gear numerator (PA06)", "Electronic gear denominator (PA07)", "Linear encoder resolution setting - Numerator (PL02)", or "Linear encoder resolution setting - Denominator (PL03)" of the servo amplifier is changed
    - When the object "HomeOffset (607CH)" of drive unit is changed
- This flag turns off by the completion of machine home position return.

### When using an absolute position system (絶対位置システムのとき) (2.1 / original p.39)

- This flag turns on in the following cases:
  - When not executing a machine home position return even once after the system starts
  - Machine home position return start (Unless a machine home position return is completed normally, the home position return request flag does not turn off.)
  - When an absolute position data in the Simple Motion module/Motion module is erased due to a memory error, etc. (Occurrence of the warning "Home position return data incorrect" (warning code: 093CH (for MR-J4(W)-B), or warning code: 0D3CH (for MR-J5(W)-B or MR-J5(W)-G).)
  - When the servo parameter "Rotation direction selection/travel direction selection (PA14)" [FX5-SSC-S], or "Travel direction selection (PA14)" [FX5-SSC-G] is changed.
  - The servo alarm "Absolute position erased" (alarm No.: 25) occurs. ([Md.108] Servo status1: b14 ON) (→Page 426 Axis monitor data)
  - The servo warning "Absolute position counter warning" (warning No.: E3) occurs. ([Md.108] Servo status1: b14 ON) (→Page 426 Axis monitor data)
  - [FX5-SSC-G]
    - When the servo parameter "Electronic gear numerator (PA06)", "Electronic gear denominator (PA07)", "Linear encoder resolution setting - Numerator (PL02)", or "Linear encoder resolution setting - Denominator (PL03)" is changed
    - When the object "HomeOffset (607CH)" of drive unit is changed
    - When a change of the servo amplifier or motor encoder is detected
    - When connecting a virtual servo amplifier, MR-J5(W)-G is not the servo amplifier connected at the previous home position establishment
- This flag turns off by the completion of the machine home position return.

### When a home position return is not required (原点復帰を必要としない場合) (2.1 / original p.39)

Control can be carried out ignoring the "home position return request flag" ([Md.31] Status: b3) in systems that do not require a home position return.
In this case, the "home position return parameters ([Pr.43] to [Pr.57])" must all be set to their initial values or a value at which an error does not occur.

### Wiring the proximity dog (近点ドグの配線) (2.1 / original p.39)

When using the proximity dog signal, wire the signal terminals corresponding to the proximity dog of the device to be used as follows.
[FX5-SSC-S]
Refer to the following for how to set the input logic of the proximity dog signal.
→Page 323 Input logic setting method for external input signals

#### External input signal of the servo amplifier (サーボアンプの外部入力信号の場合) (2.1 / original p.39)

Refer to the manuals of each servo amplifier to be used for details on signal input availability and wiring.
[FX5-SSC-S]
Wire MR-J3(W)-B, MR-J4(W)-B, and MR-J5(W)-B as shown in the following drawing. As for the 24 V DC power supply, the polarity of current can be switched.

Ex.
When "[Pr.22] Input signal logic selection" is set to the initial value

[Figure] Proximity dog wiring to the servo amplifier (original p.39)
- Servo amplifier terminal DI3 (DOG) is connected through the proximity dog contact (normally open switch symbol) and a 24 V DC power supply to terminal DICOM.
- Circuit: DI3 (DOG) — proximity dog switch — 24 V DC — DICOM (the polarity of the 24 V DC supply is not specified in the figure; see the text above: it can be switched).

[FX5-SSC-G]
Refer to the following for settings of servo parameters when using the external input signal.
→Page 321 External Input Signal Select Function

#### External input signal via CPU (buffer memory of the Simple Motion module/Motion module) (CPU経由外部入力信号(シンプルモーションユニット／モーションユニットのバッファメモリ)の場合) (2.1 / original p.39)

Refer to the manual of the input module to be used for wiring.

#### Link device [FX5-SSC-G] (リンクデバイスの場合[FX5-SSC-G]) (2.1 / original p.39)

Refer to the manual of the device station to be used for wiring.

### Home position return sub functions (原点復帰の補助機能) (2.1 / original p.40)

Refer to "Combination of Main Functions and Sub Functions" in the following manual for details on "sub functions" that can be combined with home position return control.
[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Startup)
Also refer to the following for details on each sub function.
→Page 218 CONTROL SUB FUNCTIONS
[Remarks]
The following two sub functions are only related to machine home position return.
○: Combination possible, △: Restricted, ×: Combination not possible

| Sub function name | Machine home position return | Fast home position return | Reference |
|---|---|---|---|
| Home position return retry function | △*1*2 | × | →Page 220 Home position return retry function [FX5-SSC-S] |
| Home position shift function | ○*1 | × | →Page 224 Home position shift function [FX5-SSC-S] |

*1 [FX5-SSC-G]
If stop is input during deceleration for home position return, the operation will stop at that deceleration speed.
When using the driver homing method, the stop processing follows the specifications of the servo amplifier. For details, refer to the manual of the servo amplifier to use.
When using MR-J5(W)-G: [Other manual] MR-J5 User's Manual (Function)

*2 [FX5-SSC-G]
The Motion module performs the home position return request for the servo amplifier regardless of the proximity dog signal and position of the work. For home position return specifications executed on the servo amplifier side, the relationship between the proximity dog and the work requires the work to be returned to its position prior to the proximity dog.

## 2.2 Machine Home Position Return (機械原点復帰) (2.2 / original p.41-56)

### Outline of the machine home position return operation (機械原点復帰の動作概要) (2.2 / original p.41-42)

#### Machine home position return operation (機械原点復帰の動作) (2.2 / original p.41)

In a machine home position return, a home position is established.
None of the address information stored in the Simple Motion module/Motion module, CPU module, or servo amplifier is used at this time.
The position mechanically established after the machine home position return is regarded as the "home position" to be the starting point for positioning control.

[Figure] Machine home position return (original p.41)
- Motor (M) drives a ball screw with a table. The home position (▲) is on the motor side; the proximity dog is located near the home position.
- Arrow "Machine home position return": the table moves from its current position toward the home position (toward the motor side), passing the proximity dog.

The method for establishing a home position by a machine home position return differs according to the method set in "[Pr.43] Home position return method".
The following shows the operation when starting a machine home position return.

##### When "[Pr.43] Home position return method" is set to other than "Driver home position return method" ("[Pr.43]原点復帰方式"が「ドライバ原点復帰式」以外のとき) (2.2 / original p.41)

1. The "machine home position return" is started.
2. The operation starts according to the speed and direction set in the home position return parameters ([Pr.43] to [Pr.57]).
3. The "home position" is established by the method set in "[Pr.43] Home position return method", and the machine stops.
   →Page 41 Machine home position return method to Page 49 Scale origin signal detection method [FX5-SSC-S]
4. If "a" is set as "[Pr.45] Home position address", "a" will be stored as the current position in the "[Md.20] Command position value" and "[Md.21] Machine feed value" which are monitoring the position.
5. The machine home position return is completed.

> **Point**
> Use the home position return retry function when the home position is not always in the same direction from the workpiece operation area (when the home position is not set near the upper or lower limit of the machine).
> The machine home position return may not complete unless the home position return retry function is used.

##### When "[Pr.43] Home position return method" is set to "Driver home position return method" ("[Pr.43]原点復帰方式"が「ドライバ原点復帰式」のとき) (2.2 / original p.42)

1. Set the home position return parameters of the servo amplifier.*1
2. The "machine home position return" is started.
3. The operation starts according to the speed and direction set in the servo amplifier.
4. The "home position" is established and the machine stops.
5. If "a" is set as "[Pr.45] Home position address", "a" will be stored as the current position in the "[Md.20] Command position value" and "[Md.21] Machine feed value" which are monitoring the position.
6. The machine home position return is completed.

*1 [FX5-SSC-G]
Change the setting as necessary by using the servo transient transmission function. For the setting change method, refer to the servo amplifier manual.
[Other manual] MR-J5-G/MR-J5W-G User's Manual (Parameters)

> **Point**
> The method for establishing a "home position" by a driver home position return method differs according to the setting of the servo amplifier. For details, refer to the manuals of each servo amplifier.

### Machine home position return method (機械原点復帰の原点復帰方式) (2.2 / original p.43-44)

The method by which the machine home position is established (method for judging the home position and machine home position return completion) is designated in the machine home position return according to the configuration and application of the positioning method.
The following table shows the methods that can be used for this home position return method. (The home position return method is one of the items set in the home position return parameters. It is set in "[Pr.43] Home position return method" of the basic parameters for home position return.)
○: Supported, ×: Not supported

| [Pr.43] Home position return method | Operation details | FX5-SSC-S | FX5-SSC-G |
|---|---|---|---|
| Proximity dog method | Deceleration starts by the OFF → ON of the proximity dog. (Speed is reduced to "[Pr.47] Creep speed".)<br>The operation stops once after the proximity dog turns ON and then OFF. Later the operation restarts and then stops at the first zero signal to complete the home position return.<br>That position is assumed as a home position. | ○ | × |
| Count method 1 | The deceleration starts by the OFF → ON of the proximity dog, and the machine moves at the "[Pr.47] Creep speed".<br>The machine stops once after moving the distance set in the "[Pr.50] Setting for the movement amount after proximity dog ON" from the OFF → ON position. Later the operation restarts and then stops at the first zero point to complete the machine home position return. | ○ | × |
| Count method 2 | The deceleration starts by the OFF → ON of the proximity dog, and the machine moves at the "[Pr.47] Creep speed.<br>The machine moves the distance set in the "[Pr.50] Setting for the movement amount after proximity dog ON" from the proximity dog OFF → ON position, and stops at that position. The machine home position return is then regarded as completed. | ○ | × |
| Data set method | The position where the machine home position return has been performed becomes a home position.<br>The command position value and feed machine value are overwritten to the home position address. | ○ | × |
| Scale origin signal detection method | The machine moves in the opposite direction against of "[Pr.44] Home position return direction" at the "[Pr.46] Home position return speed" by the OFF → ON of the proximity dog, and a deceleration stop is carried out once at the first zero signal. Later the operation moves in direction of "[Pr.44] Home position return direction" at the "[Pr.47] Creep speed", and then stops at the detected nearest zero point to complete the machine home position return. | ○ | × |
| Driver home position return method | [FX5-SSC-S]<br>Refer to the following for details on the driver home position return method.<br>→Page 829 AlphaStep/5-phase stepping motor driver manufactured by ORIENTAL MOTOR Co., Ltd.<br>→Page 840 IAI electric actuator controller manufactured by IAI Corporation<br>[FX5-SSC-G]<br>Switches the servo amplifier to the home position return mode and starts the home position return set to the servo amplifier. | ○ | ○ |

(The original reads "the "[Pr.47] Creep speed." in the Count method 2 row as is.)

The following shows the signals used for machine home position return.
◎: Necessary, ○: Necessary as required, —: Unnecessary

| [Pr.43] Home position return method | Signals required for control: Proximity dog | Signals required for control: Zero signal | Signals required for control: Upper/lower limit |
|---|---|---|---|
| Proximity dog method [FX5-SSC-S] | ◎ | ◎ | ○ |
| Count method 1 [FX5-SSC-S] | ◎ | ◎ | ○ |
| Count method 2 [FX5-SSC-S] | ◎ | — | ○ |
| Data set method [FX5-SSC-S] | — | — | — |
| Scale origin signal detection method [FX5-SSC-S] | ◎ | ◎ | — |
| Driver home position return method | ○*1 | ○*1 | ○*1 |

*In the original, "Signals required for control" is one header spanning the 3 columns Proximity dog / Zero signal / Upper/lower limit. Written here as one header per column.

*1 Confirm to the home position return specification of the servo amplifier for the signals required for control.

> **Point**
> Creep speed
> The stopping accuracy is poor when the machine rapidly stops from fast speeds. To improve the machine's stopping accuracy, it is required to slow down the speed before it stops. This speed is set in the "[Pr.47] Creep speed".

### Proximity dog method [FX5-SSC-S] (近点ドグ式[FX5-SSC-S]) (2.2 / original p.44-45)

The following shows an operation outline of the home position return method "proximity dog method".

#### Operation chart (動作図) (2.2 / original p.44)

[Figure] Operation chart of proximity dog method (original p.44)
- V-t: at 1. the machine accelerates to "[Pr.46] Home position return speed"; at 2. "Deceleration at the proximity dog ON" starts; at 3. the speed reaches "[Pr.47] Creep speed" and the machine moves at creep speed; at the proximity dog OFF the machine stops (point A); it then restarts at creep speed and stops at the first zero signal (4. 5.).
- [Md.34] Movement amount after proximity dog ON*1: measured from the proximity dog OFF→ON (2.) to the stop position (4. 5.).
- Proximity dog: OFF → ON at 2.; ON → OFF while moving at creep speed, after which the machine stops (point A).
- Zero signal: pulses once per servo motor rotation ("One servo motor rotation" shown between two zero signal pulses); the stop (4. 5.) is at the first zero signal after the proximity dog OFF.
- Note in figure: "Adjust so the proximity dog OFF position is as close as possible to the center of the zero signal HIGH level. If the proximity dog OFF position overlaps with the zero signal, the machine home position return stop position may deviate by one servo motor rotation."
- [POINT] in figure: "After the home position return has been started, the zero point of the encoder must be passed at least once before point A is reached."
- Machine home position return start (Positioning start signal): OFF → ON at 1.; turns OFF after the home position return complete flag turns ON.
- Home position return request flag ([Md.31] Status: b3): OFF → ON at the start (1.); ON → OFF at completion (4. 5.).
- Home position return complete flag ([Md.31] Status: b4): OFF; turns ON at completion (4. 5.).
- [Md.26] Axis operation status: Standby → Home position return (from 1.) → Standby (at completion).
- [Md.34] Movement amount after proximity dog ON: Inconsistent → 0 (at start) → Value of *1 (at completion).
- [Md.20] Command position value / [Md.21] Machine feed value: Inconsistent → Value of the machine moved is stored → Home position address (at completion).

1. The machine home position return is started.
(The machine begins the acceleration designated in "[Pr.51] Home position return acceleration time selection", in the direction designated in "[Pr.44] Home position return direction". It then moves at the "[Pr.46] Home position return speed" when the acceleration is completed.)
2. The machine begins decelerating when the proximity dog ON is detected.
3. The machine decelerates to the "[Pr.47] Creep speed", and subsequently moves at that speed.
(At this time, the proximity dog must be ON. The workpiece will continue decelerating and stop if the proximity dog is OFF.)
4. After the proximity dog turns OFF, the machine stops. It then restarts and stops at the first zero point.
5. The home position return complete flag ([Md.31] Status: b4) turns from OFF to ON and the home position return request flag ([Md.31] Status: b3) turns from ON to OFF.

#### Precautions during operation (動作上の注意) (2.2 / original p.45)

- When the home position return retry function is not set ("0" is set in "[Pr.48] Home position return retry"), the error "Start at home position" (error code: 1940H) will occur if the machine home position return is attempted again after the machine home position return completion.
- Machine home position return carried out from the proximity dog ON position will start at the "[Pr.47] Creep speed".
- The proximity dog must be ON during deceleration from the home position return speed "[Pr.47] Creep speed".
- When the stop signal stops the machine home position return, carry out the machine home position return again. When restart command is turned ON after the stop signal stops the home position return, the error "Home position return restart not possible" (error code: 1946H) will occur.
- After the home position return has been started, the zero point of the encoder must be passed at least once before point A is reached. However, if selecting "1: Not need to pass servo motor Z-phase after power on" with "Function selection C-4 (PC17)"*1, it is possible to carry out the home position return without passing the zero point. The workpiece will continue decelerating and stop if the proximity dog is turned OFF before it has decelerated to the creep speed, thus causing the error "Dog detection timing fault" (error code: 1941H).

*1 For MR-J4(W)-B. For MR-J5(W)-B, "1: Z-phase of the servo motor does not need to be passed after the power supply is switched on" is selected for "Function selection C-4 Homing condition selection (PC17.0)".

[Figure] Proximity dog turned OFF before deceleration to creep speed (Dog detection timing fault) (original p.45)
- V-t: acceleration to "[Pr.46] Home position return speed", deceleration starts at proximity dog ON; the proximity dog turns OFF before the speed reaches "[Pr.47] Creep speed" (creep speed shown dashed), so the machine continues decelerating and stops.
- Proximity dog: OFF → ON → OFF (short ON pulse during deceleration).
- Machine home position return start (Positioning start signal): OFF → ON at start; turns OFF after the stop.
- Home position return request flag ([Md.31] Status: b3): OFF → ON at start; stays ON.
- Home position return complete flag ([Md.31] Status: b4): stays OFF.
- [Md.26] Axis operation status: Standby → Home position return → Error (at the stop).
- [Md.34] Movement amount after proximity dog ON: Inconsistent → 0 (stays 0).
- [Md.20] Command position value / [Md.21] Machine feed value: Inconsistent → Value of the machine moved is stored → Address at stop.

### Count method1 [FX5-SSC-S] (カウント式1[FX5-SSC-S]) (2.2 / original p.46-47)

The following shows an operation outline of the home position return method "count method 1".
In the home position return for "count method 1", the following are possible:
- Machine home position return with the proximity dog
- Repeating machine home position return after the machine home position return is completed

#### Operation chart (動作図) (2.2 / original p.46)

[Figure] Operation chart of count method 1 (original p.46)
- V-t: acceleration to "[Pr.46] Home position return speed"; deceleration starts at proximity dog ON; moves at "[Pr.47] Creep speed"; stops once after the movement amount "[Pr.50] Setting for the movement amount after proximity dog ON" (shaded area, from proximity dog ON) — point A; then restarts and stops at the first zero signal.
- [Md.34] Movement amount after proximity dog ON*1: from proximity dog ON to the final stop position.
- Proximity dog: OFF → ON at deceleration start; stays ON past the home position ("Leave sufficient distance from the home position to the proximity dog OFF.").
- Zero signal: "First zero signal after moving a set to "[Pr.50] Setting for the movement amount after proximity dog ON"." is the stop point; "One servo motor rotation" between zero signal pulses.
- Note in figure: "Adjust the setting for the movement amount after proximity dog ON to be as near as possible to the center of the zero signal HIGH. If the setting for the movement amount after proximity dog ON falls within the zero signal, there may be produced an error of one servo motor rotation in the home position return stop position."
- [POINT] in figure: "After the home position return has been started, the zero point of the encoder must be passed at least once before point A is reached."
- Machine home position return start (Positioning start signal): OFF → ON at start; OFF after completion.
- Home position return request flag ([Md.31] Status: b3): OFF → ON at start; ON → OFF at completion.
- Home position return complete flag ([Md.31] Status: b4): OFF → ON at completion.
- [Md.26] Axis operation status: Standby → Home position return → Standby.
- [Md.34] Movement amount after proximity dog ON: Inconsistent → 0 → Value of *1.
- [Md.20] Command position value / [Md.21] Machine feed value: Inconsistent → Value of the machine moved is stored → Home position address.

1. The machine home position return is started.
(The machine begins the acceleration designated in "[Pr.51] Home position return acceleration time selection", in the direction designated in "[Pr.44] Home position return direction". It then moves at the "[Pr.46] Home position return speed" when the acceleration is completed.)
2. The machine begins decelerating when the proximity dog ON is detected.
3. The machine decelerates to the "[Pr.47] Creep speed", and subsequently moves at that speed.
4. The machine stops after the workpiece has been moved the amount set in the "[Pr.50] Setting for the movement amount after proximity dog ON" after the proximity dog turned ON. It then restarts and stops at the first zero point.
5. The home position return complete flag ([Md.31] Status: b4) turns from OFF to ON, and the home position return request flag ([Md.31] Status: b3) turns from ON to OFF.

#### Precautions during operation (動作上の注意) (2.2 / original p.47)

- The error "Count method movement amount fault" (error code: 1944H) will occur if the "[Pr.50] Setting for the movement amount after proximity dog ON" is smaller than the deceleration distance from the "[Pr.46] Home position return speed" to "[Pr.47] Creep speed".
- If the speed is changed to a speed faster than "[Pr.46] Home position return speed" by the speed change function (→Page 257 Speed change function) during a machine home position return, the distance to decelerate to "[Pr.47] Creep speed" may not be ensured, depending on the setting value of "[Pr.50] Setting for the movement amount after proximity dog ON". In this case, the error "Count method movement amount fault" (error code: 1944H) occurs and the machine home position return is stopped.
- The following shows the operation when a machine home position return is started while the proximity dog is ON.

##### Operation when a machine home position return is started at the proximity dog ON position (近点ドグON上での機械原点復帰始動時の動作) (2.2 / original p.47)

[Figure] Count method 1 started at the proximity dog ON position (original p.47)
- Proximity dog: ON at the start position (1.); it turns OFF as the machine moves in the opposite direction (the ON→OFF edge is at the reversal point).
- 1. start → 2. the machine accelerates at home position return speed in the opposite direction of home position return (below the axis) → 3. deceleration at proximity dog OFF, stop → 4. machine home position return in the home position return direction (accelerates, decelerates at proximity dog ON) → moves "[Pr.50] Setting for the movement amount after proximity dog ON" (shaded, from the proximity dog OFF→ON point) at creep speed, stops, restarts and stops at the first zero signal (5.).
- Zero signal: pulses shown; the completion (5.) coincides with a zero signal pulse after the [Pr.50] movement.

1. A machine home position return is started.
2. The machine moves at the home position return speed in the opposite direction of a home position return.
3. Deceleration processing is carried out when the proximity dog OFF is detected.
4. After the machine stops, a machine home position return is carried out in the home position return direction.
5. The machine home position return is completed on detection of the first zero signal after the travel of the movement amount set to "[Pr.50] Setting for the movement amount after proximity dog ON" on detection of the proximity dog signal ON.

- Turn OFF the proximity dog at a sufficient distance from the Home position. Although there is no harm in operation if the proximity dog is turned OFF during a machine home position return, it is recommended to leave a sufficient distance from the home position when the proximity dog is turned OFF for the following reason.

> If the machine home position return is performed consecutively after the proximity dog is turned OFF at the time of machine home position return completion, operation will be performed at the home position return speed until the hardware stroke limit (upper/lower limit) is reached. If a sufficient distance cannot be kept, consider the use of the home position return retry function.

- When the stop signal stops the machine home position return, carry out the machine home position return again. When restart command is turned ON after the stop signal stops the home position return, the error "Home position return restart not possible" (error code: 1946H) will occur.
- After the home position return has been started, the zero point of the encoder must be passed at least once before point A is reached. However, if selecting "1: Not need to pass servo motor Z-phase after power on" with "Function selection C-4 (PC17)"*1, it is possible to carry out the home position return without passing the zero point.

*1 For MR-J4(W)-B. For MR-J5(W)-B, "1: Z-phase of the servo motor does not need to be passed after the power supply is switched on" is selected for "Function selection C-4 Homing condition selection (PC17.0)".

### Count method2 [FX5-SSC-S] (カウント式2[FX5-SSC-S]) (2.2 / original p.48-49)

The following shows an operation outline of the home position return method "count method 2".
The "count method 2" method is effective when a "zero signal" cannot be received. (Note that compared to the "count method 1" method, using this method will result in more deviation in the stop position during machine home position return.)

#### Operation chart (動作図) (2.2 / original p.48)

[Figure] Operation chart of count method 2 (original p.48)
- V-t: acceleration to "[Pr.46] Home position return speed"; deceleration starts at proximity dog ON; moves at "[Pr.47] Creep speed"; decelerates and stops when the movement amount "[Pr.50] Setting for the movement amount after proximity dog ON" (shaded, from proximity dog ON) is reached. No zero signal is used.
- [Md.34] Movement amount after proximity dog ON*1: from proximity dog ON to the stop position.
- Proximity dog: OFF → ON at deceleration start; turns OFF after the stop position ("Leave sufficient distance from the home position to the proximity dog OFF.").
- Machine home position return start (Positioning start signal): OFF → ON at start; OFF after completion.
- Home position return request flag ([Md.31] Status: b3): OFF → ON at start; ON → OFF at completion.
- Home position return complete flag ([Md.31] Status: b4): OFF → ON at completion.
- [Md.26] Axis operation status: Standby → Home position return → Standby.
- [Md.34] Movement amount after proximity dog ON: Inconsistent → 0 → Value of *1.
- [Md.20] Command position value / [Md.21] Machine feed value: Inconsistent → Value of the machine moved is stored → Home position address.

1. The machine home position return is started.
(The machine begins the acceleration designated in "[Pr.51] Home position return acceleration time selection", in the direction designated in "[Pr.44] Home position return direction". It then moves at the "[Pr.46] Home position return speed" when the acceleration is completed.)
2. The machine begins decelerating when the proximity dog ON is detected.
3. The machine decelerates to the "[Pr.47] Creep speed", and subsequently moves at that speed.
4. The command from the Simple Motion module will stop and the machine home position return will be completed when the machine moves the movement amount set in "[Pr.50] Setting for the movement amount after proximity dog ON" from the proximity dog ON position.

#### Restrictions (制約事項) (2.2 / original p.48)

When this method is used, a deviation will occur in the stop position (home position) compared to other home position return methods because an error of about 1 ms occurs in taking in the proximity dog ON.

#### Precautions during operation (動作上の注意) (2.2 / original p.49)

- The error "Count method movement amount fault" (error code: 1944H) will occur and the operation will not start if the "[Pr.50] Setting for the movement amount after proximity dog ON" is smaller than the deceleration distance from the "[Pr.46] Home position return speed" to "[Pr.47] Creep speed".
- If the speed is changed to a speed faster than "[Pr.46] Home position return speed" by the speed change function (→Page 257 Speed change function) during a machine home position return, the distance to decelerate to "[Pr.47] Creep speed" may not be ensured, depending on the setting value of "[Pr.50] Setting for the movement amount after proximity dog ON". In this case, the error "Count method movement amount fault" (error code: 1944H) occurs and the machine home position return is stopped.
- The following shows the operation when a machine home position return is started while the proximity dog is ON.

##### Operation when a home position return is started at the proximity dog ON position (近点ドグON上での原点復帰始動時の動作) (2.2 / original p.49)

[Figure] Count method 2 started at the proximity dog ON position (original p.49)
- Proximity dog: ON at the start position (1.); turns OFF as the machine moves in the opposite direction.
- 1. start → 2. moves at home position return speed in the opposite direction of home position return → 3. deceleration at proximity dog OFF, stop → 4. machine home position return in the home position return direction; at proximity dog OFF→ON, decelerates to creep speed → stops after the "[Pr.50] Setting for the movement amount after proximity dog ON" (shaded, from the proximity dog ON point) (5.). No zero signal is shown.

1. A machine home position return is started.
2. The machine moves at the home position return speed in the opposite direction of a home position return.
3. Deceleration processing is carried out when the proximity dog OFF is detected.
4. After the machine stops, a machine home position return is carried out in the home position return direction.
5. The machine home position return is completed after moving the movement amount set in the "[Pr.50] Setting for the movement amount after proximity dog ON".

- Turn OFF the proximity dog at a sufficient distance from the home position. Although there is no harm in operation if the proximity dog is turned OFF during a machine home position return, it is recommended to leave a sufficient distance from the home position when the proximity dog is turned OFF for the following reason.

> If the machine home position return is performed consecutively after the proximity dog is turned OFF at the time of machine home position return completion, operation will be performed at the home position return speed until the hardware stroke limit (upper/lower limit) is reached. If a sufficient distance cannot be kept, consider the use of the home position return retry function.

- When the stop signal stops the machine home position return, carry out the machine home position return again. When restart command is turned ON after the stop signal stops the home position return, the error "Home position return restart not possible" (error code: 1946H) will occur.

### Data set method [FX5-SSC-S] (データセット式[FX5-SSC-S]) (2.2 / original p.50)

The following shows an operation outline of the home position return method "data set method".
The "Data set method" method is a method in which a "Proximity dog" is not used.
With the data set method home position return, the position where the machine home position return has been carried out, is registered into the Simple Motion module as the home position, and the command position value and feed machine value is overwritten to a home position address.
Use the JOG or manual pulse generator operation to move the home position.

#### Operation chart (動作図) (2.2 / original p.50)

[Figure] Operation chart of data set method (original p.50)
- Home position return start ([Cd.184] Positioning start): a short ON pulse.
- No axis movement (V stays 0). At the start: "The address upon execution of the home position return is registered as a home position address."

#### Precautions during operation (動作上の注意) (2.2 / original p.50)

- The zero point must be passed before the home position return is carried out after the power supply is turned ON. If the home position return is carried out without passing the zero point even once, the error "Home position return zero point not passed" (error code: 197AH) will occur. When the error "Home position return zero point not passed" (error code: 197AH) occurs, perform the JOG or similar operation so that the servo motor makes more than one revolution after an error reset, before carrying out the machine home position return again. However, if selecting "1: Not need to pass servo motor Z-phase after power on" with "Function selection C-4 (PC17)"*1, it is possible to carry out the home position return without passing the zero point.
- The home position return data used for the data set method is the "home position return direction" and "home position address". The home position return data other than that for the home position return direction and home position address is not used for the data set method home position return method, but if a value is set the outside the setting range, an error will occur when the "[Cd.190] PLC READY" is turned ON so that the READY signal ([Md.140] Module status: b0) is not turned ON. With the home position return data other than that for the home position return direction and home position address, set an arbitrary value (default value can be allowed) within each data setting range so that an error will not occur upon receiving the "[Cd.190] PLC READY" ON.
- When using the backlash compensation function, set the same movement direction of the JOG or manual pulse generator operation to the home position before the home position return is executed as "home position return direction".

*1 For MR-J4(W)-B. For MR-J5(W)-B, "1: Z-phase of the servo motor does not need to be passed after the power supply is switched on" is selected for "Function selection C-4 Homing condition selection (PC17.0)".

### Scale origin signal detection method [FX5-SSC-S] (スケール原点信号検出式[FX5-SSC-S]) (2.2 / original p.51-53)

The following shows an operation outline of the home position return method "scale origin signal detection method".

> **Point**
> - For MR-J4(W)-B
>   Set "0: Need to pass servo motor Z-phase after power on" for "Function selection C-4 (PC17)". If set to "1: Not need to pass servo motor Z-phase after power on", the error "Z-phase passing parameter invalid" (error code: 1978H) will occur at the start of scale origin signal detection method home position return.
> - For MR-J5(W)-B
>   Set "0: Z-phase of the servo motor must be passed after the power supply is switched on" for "Function selection C-4 Homing condition selection (PC17.0)". If set to "1: Z-phase of the servo motor does not need to be passed after the power supply is switched on", the error "Z-phase passing parameter invalid" (error code: 1978H) will occur at the start of scale origin signal detection method home position return.

#### Operation chart (動作図) (2.2 / original p.51)

[Figure] Operation chart of scale origin signal detection method (original p.51)
- "[Pr.44] Home position return direction" arrow points to the right (positive side of the V axis = home position return direction).
- 1. start, acceleration to "[Pr.46] Home position return speed" in the home position return direction → 2. deceleration starts at proximity dog OFF→ON → 3. deceleration stop, then moves in the opposite direction at "[Pr.46] Home position return speed" → 4. deceleration starts at the first zero signal (zero signal pulse located before the proximity dog ON edge in the return path) → 5. after deceleration stop, moves in the home position return direction at "[Pr.47] Creep speed" → 6. stops at the detected nearest zero signal.
- Proximity dog: OFF → ON at 2.; ON region ends before the hardware limit switch; a "Hardware limit switch" is located beyond the proximity dog in the home position return direction.
- Zero signal: pulse at the position of 4./6.

1. The machine home position return is started.
(The machine begins the acceleration designated in "[Pr.51] Home position return acceleration time selection", in the direction designated in "[Pr.44] Home position return direction". It then moves at the "[Pr.46] Home position return speed" when the acceleration is completed.)
2. The machine begins decelerating when the proximity dog ON is detected.
3. After deceleration stop, the machine moves in the opposite direction against of home position return at the "[Pr.46] Home position return speed".
4. During movement, the machine begins decelerating when the first zero signal is detected.
5. After deceleration stop, the operation moves in direction of home position return at the "[Pr.47] Creep speed", and then stops at the detected nearest zero signal.
6. The home position return complete flag ([Md.31] Status: b4) turns from OFF to ON, and the home position return request flag ([Md.31] Status: b3) turns from ON to OFF.

> **Point**
> After 3., when the zero signal is in the proximity dog position, deceleration stop (4.) is started at the zero signal without waiting for the proximity dog OFF.

#### Precautions during operation (動作上の注意) (2.2 / original p.52-53)

- The error "Start at home position" (error code: 1940H) will occur if another machine home position return is attempted immediately after a machine home position return completion when the home position is in the proximity dog ON position.
- The following shows the operation when a machine home position return is started from the proximity dog ON position.

##### Operation when a machine home position return is started from the proximity dog ON position (近点ドグ上での原点復帰始動時の動作) (2.2 / original p.52)

[Figure] Scale origin signal detection method started from the proximity dog ON position (original p.52)
- "[Pr.44] Home position return direction" arrow points to the right.
- 1. start at the proximity dog ON position; the machine moves in the opposite direction at "[Pr.46] Home position return speed" → 2. deceleration at the first zero signal → 3. after the stop, moves in the home position return direction at "[Pr.47] Creep speed" and stops at the zero signal.
- Proximity dog: ON region; the "Hardware limit switch" is beyond the proximity dog in the home position return direction.

1. The machine moves in the opposite direction against of home position return at the home position return speed.
2. The machine begins decelerating when the first zero signal is detected.
3. After deceleration stop, the operation moves in direction of home position return at the creep speed, and then stops at the zero signal to complete the machine home position return.

> **Point**
> After 1., when the zero signal is in the proximity dog ON position, deceleration stop (2.) is started at the zero signal without waiting for the proximity dog OFF.

- When the stop signal stops the machine home position return, carry out the machine home position return again. When restart command is turned ON after the stop signal stops the home position return, the error "Home position return restart not possible" (error code: 1946H) will occur.
- The home position return retry will not be performed regardless of setting set in "[Pr.48] Home position return retry" in the scale origin signal detection method. When a hardware limit switch is detected during machine home position return, the error "Hardware stroke limit (+)" (error code: 1904H) or "Hardware stroke limit (-)" (error code: 1906H) will occur.
- Position the proximity dog forward to overlaps with the hardware limit switch in direction of home position return. When the proximity dog is in the opposite direction against of home position return from the machine home position return start position, the error "Hardware stroke limit (+)" (error code: 1904H) or "Hardware stroke limit (-)" (error code: 1906H) will occur.

[Figure] Arrangement of proximity dog and hardware limit switch (original p.52)
- Motor (M) on the right drives a ball screw; the table is on the left; "Machine home position return" arrow points to the right (toward the motor side).
- Home position (▲) is between the table and the proximity dog; the proximity dog is ahead in the home position return direction, and the hardware limit switch is further ahead, overlapping the end of the proximity dog.

- When the zero signal is detected again during deceleration (4.) in the following figure) with detection of zero signal, the operation stops at the zero signal detected lastly to complete the home position return.

[Figure] Zero signal detected again during deceleration (original p.53)
- "[Pr.44] Home position return direction" arrow points to the right.
- 1. start, acceleration to "[Pr.46] Home position return speed" → 2. deceleration at proximity dog OFF→ON → 3. stop, then moves in the opposite direction at home position return speed → 4. deceleration at the zero signal; during this deceleration further zero signal pulses are passed → 5. after the stop, moves in the home position return direction at "[Pr.47] Creep speed" → 6. stops at the zero signal detected lastly.
- Zero signal: three pulses shown (at 6., at 4., and one further right).

- Do not use the scale origin signal detection method home position return with the backlash compensation function.
- When using the direct drive motor, make it passed the Z-phase once before reaching 3. in the previous operation chart. (→Page 49 Scale origin signal detection method [FX5-SSC-S])

### Driver home position return method (ドライバ原点復帰式) (2.2 / original p.54-56)

The home position return is executed based on the positioning pattern set on the driver (servo amplifier) side (hereafter called the "driver side"). Set the setting values of home position return in the parameters of the driver side. Refer to the manual of the driver because the home position return operation and parameters depend on the specification of the driver.

#### Operation chart (動作図) (2.2 / original p.54-55)

1. The machine home position return is started. (The machine executes the home position return based on the positioning pattern set on the driver side.)
2. The command position value is continuously updated by follow up processing during the home position return.
3. The home position return complete flag ([Md.31] Status: b4) turns from OFF to ON and the home position return request flag ([Md.31] Status: b3) turns from ON to OFF.

##### Operation chart [FX5-SSC-S] (動作図[FX5-SSC-S]) (2.2 / original p.54)

Refer to the following for the operation chart.
→Page 829 AlphaStep/5-phase stepping motor driver manufactured by ORIENTAL MOTOR Co., Ltd.
→Page 840 IAI electric actuator controller manufactured by IAI Corporation

##### Operation chart [FX5-SSC-G] (動作図[FX5-SSC-G]) (2.2 / original p.54)

[Figure] Driver home position return operation chart [FX5-SSC-G] (original p.54)
- [Cd.3] Positioning start No.: 9001 (set before the start).
- [Cd.184] Positioning start: OFF → ON at start; turns OFF later (after [Md.141] Busy turns ON).
- [Md.26] Axis operation status: 0: Standby → 5: Analyzing (at [Cd.184] ON) → 7: Home position return → 0: Standby (at completion).
- [Md.141] Busy: OFF → ON at the change to "7: Home position return"; ON → OFF at completion.
- Home position return request flag ([Md.31] Status: b3): OFF → ON at the same time as Busy ON; ON → OFF at completion.
- Home position return complete flag ([Md.31] Status: b4): OFF → ON at completion.
- [Md.514] Home position return operating status: FFFFH → 1H → 0H: Homing procedure is in progress (motor running) → 3H: Homing procedure is completed successfully → FFFFH (after completion; "FFFFH: The servo amplifier is not set to the home position return mode").
- Label for 1H: "1H: Homing procedure is interrupted or not started" — Other than MR-J5(W)-G: "3H" is stored if the home position has been established. MR-J5(W)-G: "1H" is stored if the home position has been established.
- Motor speed: starts after [Md.514] = 0H; high-speed movement, deceleration at proximity dog ON, creep, then a further move and stop at the zero signal (pattern set on the driver side).
- Proximity dog: ON pulse during the movement. Zero signal: pulses during the movement; the stop coincides with a zero signal pulse.
- Note in figure: "When the driver is set to the home position return method such as Method 35 or 37 (Data set method), the home position return is completed immediately after the execution. Thus, the operating status may not be able to be checked."

##### When the machine home position return is stopped (機械原点復帰を停止した場合) (2.2 / original p.55)

[Figure] Driver home position return stopped by [Cd.180] Axis stop [FX5-SSC-G] (original p.55)
- [Cd.3] Positioning start No.: 9001.
- [Cd.184] Positioning start: OFF → ON at start; OFF later.
- [Md.141] Busy: OFF → ON; ON → OFF after the motor stops.
- [Cd.180] Axis stop: OFF → ON during the home position return (motor decelerates to stop); turns OFF after Busy OFF.
- Home position return request flag ([Md.31] Status: b3): OFF → ON at Busy ON; stays ON.
- Home position return complete flag ([Md.31] Status: b4): stays OFF.
- [Md.26] Axis operation status: 0: Standby → 5: Analyzing → 7: Home position return → 1: Stopped.
- [Md.514] Home position return operating status: FFFFH → 1H → 0H: Homing procedure is in progress → 1H (after the stop; "1H: Homing procedure is interrupted or not started") → FFFFH ("FFFFH: The servo amplifier is not set to the home position return mode").
- Label for the first 1H: "1H: Homing procedure is interrupted or not started" — Other than MR-J5(W)-G: "3H" is stored if the home position has been established. MR-J5(W)-G: "1H" is stored if the home position has been established.
- Motor speed: accelerates after 0H, decelerates to stop after [Cd.180] ON.

#### Parameter setting required after the driver home position return method (ドライバ原点復帰式後に必要なパラメータ設定) (2.2 / original p.55)

Refer to the following.
→Page 411 Setting items for home position return parameters

#### Start of the driver home position return method (ドライバ原点復帰式の始動) (2.2 / original p.55)

Set "9001" in "[Cd.3] Positioning start No.", and start the axis.
[FX5-SSC-G]
The control mode of the servo amplifier is set to "Homing mode".
If Zero speed is not ON ([Md.119] Servo status 2: b3 is not ON) at start for MR-J5(W)-G, the home position return operation does not start until Zero speed turns ON. Even in this case, "7: Home position return" is set in "[Md.26] Axis operation status".
When home position return starts/completes and the control mode of the servo amplifier does not change within 1 second, the error "Control mode switching error" (error code: 1F04H) occurs.

#### Axis stop of the driver home position return method [FX5-SSC-G] (ドライバ原点復帰式の軸停止[FX5-SSC-G]) (2.2 / original p.55)

When "[Cd.180] Axis stop" is turned ON during the home position return, the "HALT" signal is sent to the servo amplifier. If the servo amplifier which does not support the "HALT" signal is used, the axis is not stopped by this signal. Use the forced stop signal instead. Refer to the servo amplifier manual for support information on the HALT signal and forced stop signal.
MR-J5(W)-G supports the HALT signal.
For MR-J5(W)-G: [Other manual] MR-J5 User's Manual (Function)

#### Backlash compensation after the driver home position return method (ドライバ原点復帰式後のバックラッシュ補正) (2.2 / original p.56)

When "[Pr.11] Backlash compensation amount" is set in the Simple Motion module/Motion module, whether the backlash compensation is necessary or not is judged from "[Pr.44] Home position return direction" of the Simple Motion module/Motion module in the axis operation such as positioning after the driver home position return.
When the positioning is executed in the same direction as "[Pr.44] Home position return direction", the backlash compensation is not executed. However, when the positioning is executed in the reverse direction against "[Pr.44] Home position return direction", the backlash compensation is executed.
Note that the home position return is executed based on the home position return direction of the driver side parameter during the driver home position return. Therefore, set the same direction to "[Pr.44] Home position return direction" of the Simple Motion module/Motion module and the last home position return direction of the drive side.

#### Restrictions (制約事項) (2.2 / original p.56)

- The home position return cannot be started with the Simple Motion module/Motion module during servo-off. Thus, the servo amplifier home position return method, Method 35 and 37 (Data set method), cannot be executed during servo-off.

[FX5-SSC-G]
- When home position return is used during synchronous control, the output axis performs the following operations based on the setting of "[Pr.300] Servo input axis type".

| [Pr.300] Servo input axis type | Output axis operation during synchronous control |
|---|---|
| 1: Command position value | Continues synchronous control after home position return completion. |
| 3: Servo command value | Continues synchronous control after home position return completion. |
| 2: Actual position value | Synchronizes with the input axis until home position return completion, following which servo alarm "AL.031.1_Servo motor speed error" or "AL.035.1_Command frequency error" may occur and synchronous control may not be performed. |
| 4: Feedback value | Synchronizes with the input axis until home position return completion, following which servo alarm "AL.031.1_Servo motor speed error" or "AL.035.1_Command frequency error" may occur and synchronous control may not be performed. |

*In the original, "1: Command position value" and "3: Servo command value" are written in one cell (one row), and "2: Actual position value" and "4: Feedback value" in one cell (one row). Expanded to one row per setting value.

When "2: Actual position value" or "4: Feedback value" is set in "[Pr.300] Servo input axis type" and the value other than "0" is set in "[Pr.301] Servo input axis smoothing time constant" or "[Pr.303] Servo input axis phase compensation time constant", the warning "Input axis speed display over (warning code: 0E42H)" will occur.

## 2.3 Fast Home Position Return (高速原点復帰) (2.3 / original p.57-58)

### Outline of the fast home position return operation (高速原点復帰の動作概要) (2.3 / original p.57)

#### Fast home position return operation (高速原点復帰の動作) (2.3 / original p.57)

After establishing home position by a machine home position return, positioning control to the home position is executed without using a proximity dog or a zero signal.
The following shows the operation during a basic fast home position return start.

[Figure] Fast home position return operation (original p.57)
- V-t: trapezoidal movement at "[Pr.46] Home position return speed", stopping at "Machine home position (Home position)".
- Fast home position return start (Positioning start signal): OFF → ON at the start; ON → OFF at the stop.
- [Md.26] Axis operation status: Standby → Position control → Standby.
- Mechanism: table moves along the ball screw toward the home position (▲) near the motor (M): "Positioning to the home position".

1. The fast home position return is started.
2. Positioning control to the home position established by a machine home position return begins at speed set in "[Pr.46] Home position return speed".
3. The fast home position return is completed.

### Operation timing and processing time (動作タイミングと処理時間) (2.3 / original p.57-58)

The following shows details about the operation timing and time during fast home position return.

#### Operation example (動作例) (2.3 / original p.57)

[Figure] Operation timing during fast home position return (original p.57)
- [Cd.184] Positioning start ON → after t1, [Md.141] BUSY turns ON; at the same time the start complete signal ([Md.31] Status: b14) turns ON and [Md.26] Axis operation status changes "Standby" → "Position control".
- The positioning operation starts t2 after BUSY ON.
- At the end of the positioning operation, [Md.141] BUSY turns OFF and [Md.26] returns to "Standby".
- [Cd.184] Positioning start turns OFF (after BUSY OFF); the start complete signal (b14) turns OFF t3 after [Cd.184] turns OFF.

- Normal timing time (Unit: [ms])

| Model | Operation cycle | t1*1 | t2*2 | t3 |
|---|---|---|---|---|
| FX5-SSC-S | 0.888 | 0.3 to 1.4 | 3.83 to 4.59 | 0 to 0.9 |
| FX5-SSC-S | 1.777 | 0.3 to 1.4 | 4.76 to 6.43 | 0 to 1.8 |
| FX5-SSC-G | 0.500 | 0.4 to 1.0 | 1.75 to 2.50 | 0 to 1.0 |
| FX5-SSC-G | 1.000 | 0.4 to 1.5 | 3.2 to 3.5 | 0 to 2.0 |
| FX5-SSC-G | 2.000 | 0.4 to 2.8 | 6.0 to 6.4 | 0 to 4.0 |
| FX5-SSC-G | 4.000 | 0.4 to 4.5 | 12.2 to 13.0 | 0 to 8.0 |

*In the original, "Operation cycle" is one header spanning the model and cycle columns; the model cell is merged (FX5-SSC-S over 2 rows, FX5-SSC-G over 4 rows). Expanded to each row.

*1 The t1 timing time could be delayed by the operation state of other axes.
*2 The t2 timing time depends on the setting of the acceleration time, servo parameter, etc.

### Operating restrictions (動作上の注意) (2.3 / original p.58)

- The fast home position return can only be executed after the home position is established by executing the machine home position return. If not, the error "Home position return request ON" (error code: 1945H [FX5-SSC-S], or error code 1A45H [FX5-SSC-G]) will occur. (Home position return request flag ([Md.31] Status: b3) must be turned OFF).
- If the fraction pulse is cleared to zero using current value changing or fixed-feed control, execute the fast home position return and an error will occur by a cleared amount.
- When unlimited length feed is executed by speed control and the machine feed value overflows or underflows once, the fast home position return cannot be executed normally.
- The home position return complete flag ([Md.31] Status: b4) is not turned ON.
- The axis operation status during fast home position return is "in position control".

## 2.4 Selection of the Home Position Return Setting Condition (原点セット条件選択) (2.4 / original p.59)

This function can be set when the servo amplifier to be connected supports the servo parameter "Selection of the home position return setting condition". Refer to the manuals of each servo amplifier to be connected for confirming if the function is supported or not.

### Outline of the home position return setting condition (原点セット条件選択の動作概要) (2.4 / original p.59)

To execute the home position return when selecting "0: Need to pass servo motor Z-phase after power on" with the servo parameter of the servo amplifier "Function selection C-4 (PC17)"*1, it is necessary that the servo motor has been rotated more than one revolution and passed the Z-phase (Motor reference position signal) and that the zero point pass signal ([Md.119] Servo status2: b0) has turned ON.
When selecting "1: Not need to pass servo motor Z-phase after power on" with "Function selection C-4 (PC17)"*2, it is possible to turn the zero point pass signal ([Md.119] Servo status2: b0) ON without passing the zero point.
n: Axis No. - 1

| Monitor item | Buffer memory address |
|---|---|
| [Md.119] Servo status2: b0 | 2476+100n |

*1 For MR-J4(W)-B. For MR-J5(W)-B, "0: Z-phase of the servo motor must be passed after the power supply is switched on" is selected for "Function selection C-4 Homing condition selection (PC17.0)".
*2 For MR-J4(W)-B. For MR-J5(W)-B, "1: Z-phase of the servo motor does not need to be passed after the power supply is switched on" is selected for "Function selection C-4 Homing condition selection (PC17.0)".

### Data setting (データの設定) (2.4 / original p.59)

To select the "home position return setting condition", set the servo amplifier shown in the following table.
Servo parameters are set for each axis.
The "home position return setting condition" is stored into the following buffer memory addresses.
n: Axis No. - 1

| Setting item | Setting value | Setting details | Buffer memory address |
|---|---|---|---|
| Function selection C-4 (PC17)*1 | → | 0: Need to pass servo motor Z-phase after power on<br>1: Not need to pass servo motor Z-phase after power on | 28480+100n |

*1 For MR-J4(W)-B. "Function selection C-4 Homing condition selection (PC17.0)" for MR-J5(W)-B.

Refer to the following for information on the setting details.
→Page 496 Servo parameters [FX5-SSC-S]
The servo parameters for MR-J5(W)-B do not exist in the buffer memory. Therefore, use GX Works3 or the axis control data to set them. For details, refer to the following.
→Page 845 Connection with MR-J5(W)-B

### Precautions during operation (動作上の注意) (2.4 / original p.59)

Set "Function selection C-4 (PC17)"*1, and then turn off the power supply of the servo amplifier once and switch it on again to make that parameter setting valid.

*1 For MR-J4(W)-B. "Function selection C-4 Homing condition selection (PC17.0)" for MR-J5(W)-B.
