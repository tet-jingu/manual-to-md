# 8 COMMON FUNCTIONS (共通機能) (Chapter 8 / original p.318-388)

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

## Conversion range (変換範囲表 / original p.318-388)

| Original page | Section | Handling |
|---|---|---|
| p.318 | 8 COMMON FUNCTIONS (chapter intro), 8.1 Outline of Common Functions | Full text |
| p.319-320 | 8.2 Parameter Initialization Function | Full text |
| p.321-322 | 8.3 Execution Data Backup Function | Full text |
| p.323-330 | 8.4 External Input Signal Select Function | Full text (including program example) |
| p.331-337 | 8.5 Link Device External Signal Assignment Function [FX5-SSC-G] | Full text |
| p.338-341 | 8.6 History Monitor Function | Full text |
| p.342-345 | 8.7 Amplifier-less Operation Function [FX5-SSC-S] | Full text |
| p.346-351 | 8.8 Virtual Servo Amplifier Function | Full text |
| p.352-356 | 8.9 Driver Communication Function [FX5-SSC-S] | Full text |
| p.357-372 | 8.10 Mark Detection Function | Full text |
| p.373-377 | 8.11 Optional Data Monitor Function | Full text |
| p.378 | 8.12 Event History Function [FX5-SSC-G] | Full text |
| p.379-382 | 8.13 Connect/Disconnect Function of SSCNET Communication [FX5-SSC-S] | Full text (program example transcribed as mnemonic) |
| p.383-385 | 8.14 Servo Transient Transmission Function [FX5-SSC-G] | Full text |
| p.386 | 8.15 Firmware update function | Full text |
| p.387-388 | 8.16 Hot line forced stop function (new in this edition; not in the Japanese version) | Full text |

## Table of Contents (目次)

- 8 COMMON FUNCTIONS (共通機能)
- 8.1 Outline of Common Functions (共通機能の概要)
- 8.2 Parameter Initialization Function (パラメータの初期化機能)
- 8.3 Execution Data Backup Function (実行データのバックアップ機能)
- 8.4 External Input Signal Select Function (外部入力信号設定機能)
- 8.5 Link Device External Signal Assignment Function [FX5-SSC-G] (リンクデバイス外部信号割付け機能[FX5-SSC-G])
- 8.6 History Monitor Function (履歴モニタ機能)
- 8.7 Amplifier-less Operation Function [FX5-SSC-S] (アンプなし運転機能[FX5-SSC-S])
- 8.8 Virtual Servo Amplifier Function (仮想サーボアンプ機能)
- 8.9 Driver Communication Function [FX5-SSC-S] (ドライバ間通信機能[FX5-SSC-S])
- 8.10 Mark Detection Function (マーク検出機能)
- 8.11 Optional Data Monitor Function (任意データモニタ機能)
- 8.12 Event History Function [FX5-SSC-G] (イベント履歴機能[FX5-SSC-G])
- 8.13 Connect/Disconnect Function of SSCNET Communication [FX5-SSC-S] (SSCNET通信の切断／再接続機能[FX5-SSC-S])
- 8.14 Servo Transient Transmission Function [FX5-SSC-G] (サーボトランジェント伝送機能[FX5-SSC-G])
- 8.15 Firmware update function (ファームウェアアップデート機能)
- 8.16 Hot line forced stop function (ホットライン強制停止機能)

---

## 8 COMMON FUNCTIONS (共通機能) (Chapter 8 / original p.318)

The details and usage of the "common functions" executed according to the user's requirements are explained in this chapter.
Common functions include functions required when using the Simple Motion module/Motion module, such as parameter initialization and execution data backup.
Read the setting and execution procedures for each common function indicated in this chapter thoroughly, and execute the appropriate function where required.

## 8.1 Outline of Common Functions (共通機能の概要) (8.1 / original p.318)

"Common functions" are executed according to the user's requirements, regardless of the control method, etc.
These common functions are executed by an engineering tool or programs.
The following table shows the functions included in the "common functions".

| Common function | Details | Means: Program | Means: Engineering tool |
|---|---|---|---|
| Parameter initialization function | This function returns the setting data stored in the buffer memory/internal memory and flash ROM/internal memory (nonvolatile) of Simple Motion module/Motion module to the default values. | ○ | ○ |
| Execution data backup function | This function writes the "execution data", currently being used for control, to the flash ROM/internal memory (nonvolatile). | ○ | ○ |
| External input signal select function | This function is used to select from the following signals when using each external input signal of each axis (upper/lower stroke limit signal (FLS/RLS), proximity dog signal (DOG), and stop signal (STOP)).<br>• External input signal of servo amplifier<br>• External input signal via CPU (buffer memory)<br>• Link device input signal [FX5-SSC-G] | ○ | ○ |
| Link device external signal assignment function [FX5-SSC-G] | This function assigns link devices to the external signals of the Motion module. | ○ | ○ |
| History monitor function | This function monitors start history and current value history of all axes. | — | ○ |
| Amplifier-less operation function [FX5-SSC-S] | This function executes the positioning control of Simple Motion module without connecting to the servo amplifiers. It is used to debug the program at the start-up of the device or simulate the positioning operation. | ○ | — |
| Virtual servo amplifier function | This function executes the operation as the axis (virtual servo amplifier axis) that operates only command (instruction) virtually without servo amplifiers. | ○ | ○ |
| Driver communication function [FX5-SSC-S] | This function uses the "Master-slave operation function" of servo amplifier. The Simple Motion module controls the master axis and the slave axis is controlled by data communication between servo amplifiers (driver communication) without Simple Motion module. | ○ | ○ |
| Mark detection function | This function is used to latch any data at the input timing of the mark detection signal (DI). | ○ | ○ |
| Optional data monitor function | This function is used to store the data selected by user up to 4 data per axis to buffer memory and monitor them. | ○ | ○ |
| Event history function [FX5-SSC-G] | This function takes errors that occur on the Motion module and event information and collects them in the CPU module or saves them to the SD memory card.<br>Storing the errors in the CPU allows the error history to be checked even after turning OFF the power or resetting. | — | ○ |
| Connect/disconnect function of SSCNET communication [FX5-SSC-S] | Temporarily connect/disconnect of SSCNET communication is executed during system's power supply ON. This function is used to exchange the servo amplifiers or SSCNETⅢ cables. | ○ | — |
| Servo transient transmission function [FX5-SSC-G] | This function reads and writes objects of the device via transient transmission. | ○ | — |
| Hot line forced stop function | This function is used to execute deceleration stop safety for other axes when the servo alarm occurs in the servo amplifier MR-JE-B(F). | ○ | ○ |
| F/W update function | This function is used to update F/W of Simple Motion module/Motion module. | — | ○ |

*In the original, "Means" is a two-level header (Program / Engineering tool). ○: available, —: not available.

## 8.2 Parameter Initialization Function (パラメータの初期化機能) (8.2 / original p.319-320)

The "parameter initialization function" is used to return the setting data set in the buffer memory/internal memory and flash ROM/internal memory (nonvolatile) of Simple Motion module/Motion module to the default values.

#### Parameter initialization means (パラメータの初期化手段) (8.2 / original p.319)

- Initialization is executed with a program.
- Initialization is executed by an engineering tool.

Refer to "Help" in the "Simple Motion Module Setting Function" for the execution method by an engineering tool.

#### Control details (制御内容) (8.2 / original p.319)

The following table shows the setting data initialized by the "parameter initialization function".
(The data initialized are "buffer memory/internal memory" and "flash ROM/internal memory (nonvolatile)" setting data.)

| Target area | |
|---|---|
| Parameters | Servo network configuration parameters [FX5-SSC-G] |
| Parameters | Common parameters |
| Parameters | Basic parameters |
| Parameters | Detailed parameters |
| Parameters | Home position return basic parameters |
| Parameters | Home position return detailed parameters |
| Parameters | Extended parameters |
| Parameters | Link device external signal assignment parameters [FX5-SSC-G] |
| Servo parameters | Servo amplifier parameters [FX5-SSC-S] |
| Mark detection | Mark detection setting parameters |
| Synchronous control parameters | Servo input axis parameters |
| Synchronous control parameters | Synchronous encoder axis parameters |
| Synchronous control parameters | Synchronous encoder axis parameters via link device [FX5-SSC-G] |
| Synchronous control parameters | Command generation axis parameters |
| Synchronous control parameters | Command generation axis positioning data |
| Synchronous control parameters | Synchronous parameters |
| Positioning data | Positioning data (No.1 to 100) |
| Positioning data | Positioning data (No.101 to 600) |
| Block start data | Block start data (block No.7000 to 7001) |
| Block start data | Condition data (block No.7000 to 7001) |
| Block start data | Block start data (block No.7002 to 7004) |
| Block start data | Condition data (block No.7002 to 7004) |
| Cam data | (merged over both columns) |

*In the original, "Target area" is a single header over both columns; "Parameters" is merged over 8 rows, "Synchronous control parameters" over 6 rows, "Positioning data" over 2 rows and "Block start data" over 4 rows. "Cam data" is one cell merged over both columns. Expanded to each row.

#### Precautions during control (制御上の注意事項) (8.2 / original p.320)

- Parameter initialization is only executed when the positioning control is not carried out (when the "[Cd.190] PLC READY" is OFF). The warning "In PLC READY" (warning code: 0905H [FX5-SSC-S], or warning code: 0D05H [FX5-SSC-G]) will occur if executed when the "[Cd.190] PLC READY" is ON.
- Writing to the flash ROM is up to 100,000 times. If writing to the flash ROM exceeds 100,000 times, the writing may become impossible, and the error "Flash ROM write error" (error code: 1931H [FX5-SSC-S], or error code: 1A31H [FX5-SSC-G]) will occur.
- A "CPU module reset" or "CPU module power restart" must be carried out after the parameters are initialized.
- If an error occurs on the parameter set in the Simple Motion module/Motion module when the "[Cd.190] PLC READY" is turned ON, the READY signal ([Md.140] Module status: b0) will not be turned ON and the control cannot be carried out.

> **Restriction**
> Parameter initialization takes approximately 30 seconds. When a short time is assigned to the main cycle*1, initialization may take more than 30 seconds.
> Do not turn the power ON/OFF or reset the CPU module during parameter initialization.
> If the power is turned OFF or the CPU module is reset to forcibly end the process, the data backed up in the flash ROM/internal memory (nonvolatile) will be lost.

*1 Cycle of processing executed at free time except for the positioning control. It changes by status of axis start.

#### Parameter initialization method (パラメータの初期化方法) (8.2 / original p.320)

- Parameter initialization can be carried out by writing the data shown in the table below to the buffer memory of Simple Motion module/Motion module. The initialization of the parameter is executed at the time point the data is written to the buffer memory of Simple Motion module/Motion module.

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.2] | Parameter initialization request | 1 | Set "1" (parameter initialization request). | 5901 |

Refer to the following for the setting details.
→Page 561 Control Data
When the initialization is complete, "0" will be set in "[Cd.2] Parameter initialization request" by the Simple Motion module/Motion module automatically.

## 8.3 Execution Data Backup Function (実行データのバックアップ機能) (8.3 / original p.321-322)

When the buffer memory data of Simple Motion module/Motion module is rewritten from the CPU module, "the data backed up in the flash ROM/internal memory (nonvolatile)" of Simple Motion module/Motion module may differ from "the execution data being used for control (buffer memory data)". In this case, the execution data will be lost when the power supply of CPU module is turned OFF.
The "execution data backup function" is used to back up the execution data by writing to the flash ROM/internal memory (nonvolatile). The data backed up will be written to the buffer memory when the power is turned ON next time.

> **Point**
> When the Simple Motion module/Motion module is replaced, all the data in the Simple Motion module/Motion module including absolute position data can be backed up (read to) in the personal computer and restored to (written to) the Simple Motion module/Motion module again by using the backup/restore function of an engineering tool. Refer to "Help" in the "Simple Motion Module Setting Function" of the engineering tool for details.

#### Execution data backup means (実行データのバックアップ手段) (8.3 / original p.321)

- The backup is executed with a program.
- The data is written to the flash ROM by an engineering tool.

Refer to "Help" in the "Simple Motion Module Setting Function" for the flash ROM write method by an engineering tool.

#### Control details (制御内容) (8.3 / original p.321)

- The following shows the data that can be written to the flash ROM/internal memory (nonvolatile) using the "execution data backup function".

| Target area | |
|---|---|
| Parameters | Servo network configuration parameters [FX5-SSC-G] |
| Parameters | Common parameters |
| Parameters | Basic parameters |
| Parameters | Detailed parameters |
| Parameters | Home position return basic parameters |
| Parameters | Home position return detailed parameters |
| Parameters | Extended parameters |
| Parameters | Link device external signal assignment parameters [FX5-SSC-G] |
| Servo parameters | Servo amplifier parameters [FX5-SSC-S] |
| Mark detection | Mark detection setting parameters |
| Synchronous control parameters | Servo input axis parameters |
| Synchronous control parameters | Synchronous encoder axis parameters |
| Synchronous control parameters | Synchronous encoder axis parameters via link device [FX5-SSC-G] |
| Synchronous control parameters | Command generation axis parameters |
| Synchronous control parameters | Command generation axis positioning data |
| Synchronous control parameters | Synchronous parameters |
| Positioning data | Positioning data (No.1 to 100) |
| Positioning data | Positioning data (No.101 to 600) |
| Block start data | Block start data (block No.7000 to 7001) |
| Block start data | Condition data (block No.7000 to 7001) |
| Block start data | Block start data (block No.7002 to 7004) |
| Block start data | Condition data (block No.7002 to 7004) |

*In the original, "Target area" is a single header over both columns; "Parameters" is merged over 8 rows, "Synchronous control parameters" over 6 rows, "Positioning data" over 2 rows and "Block start data" over 4 rows. Expanded to each row. (Unlike the table in 8.2, there is no "Cam data" row.)

- The module parameters are stored in the CPU module. Therefore, these parameters cannot be backed up in the flash ROM in the Simple Motion module/Motion module.
- The cam data (cam storage area) is separately saved in the flash ROM/internal memory (nonvolatile). Therefore, it is not a target of the backup function.

#### Precautions during control (制御上の注意事項) (8.3 / original p.322)

- Data can only be written to the flash ROM when the positioning control is not carried out (when the "[Cd.190] PLC READY" is OFF). The warning "In PLC READY" (warning code: 0905H [FX5-SSC-S], or warning code: 0D05H [FX5-SSC-G]) will occur if executed when the "[Cd.190] PLC READY" is ON.
- After the power supply is turned ON or the CPU module is reset once, writing to the flash ROM using a program is limited to up to 25 times. If the 26th writing is executed, the error "Flash ROM write number error" (error code: 1080H) will occur. If this error occurs, carry out the error reset or power OFF → ON/CPU module reset operation again.

[FX5-SSC-S]
- Writing to the flash ROM can be executed up to 100,000 times. If writing to the flash ROM exceeds 100,000 times, the writing may become impossible, and the error "Flash ROM write error" (error code: 1931H) will occur.

[FX5-SSC-G]
- Writing to the flash ROM can be executed up to 100,000 times. If writing to the flash ROM exceeds 100,000 times, the error "Flash ROM write number error" (error code: 1080H) will occur. In addition, sometimes writing to the flash ROM may become impossible, in which case the error "Flash ROM write error" (error code: 1A31H) will occur.

> **Restriction**
> The writing time to the flash ROM is approximately 10 seconds. When a short time is assigned to the main cycle*1, writing may take more than 10 seconds.
> Do not turn the power ON/OFF or reset the CPU module during executing the flash ROM writing.
> If the power is turned OFF or the CPU module is reset to forcibly end the process, the data backed up in the flash ROM/internal memory (nonvolatile) will be lost.

*1 Cycle of processing executed at free time except for the positioning control. It changes by status of axis start.

#### Execution data backup method (実行データのバックアップ方法) (8.3 / original p.322)

- Refer to the following for the data transmission processing at the backup of the execution data.
  →Page 607 Data transmission process
- Execution data backup can be carried out by writing the data shown in the table below to the buffer memory of Simple Motion module/Motion module. The writing to the flash ROM/internal memory (nonvolatile) is executed at the time point the data is written to the buffer memory of Simple Motion module/Motion module.

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.1] | Flash ROM write request | 1 | Set "1: Requests write access to flash ROM.". | 5900 |

Refer to the following for the setting details.
→Page 561 Control Data
When the writing to the flash ROM/internal memory (nonvolatile) is complete, "0" will be set in "[Cd.1] Flash ROM write request" by the Simple Motion module/Motion module automatically.

## 8.4 External Input Signal Select Function (外部入力信号設定機能) (8.4 / original p.323-330)

The "external input signal select function" is used to select from the following signals when using each external input signal of each axis (upper/lower stroke limit signal (FLS/RLS), proximity dog signal (DOG), and stop signal (STOP)).
- External input signal of servo amplifier
- External input signal via CPU (buffer memory)
- Link device input signal [FX5-SSC-G]

#### Setting details (設定内容) (8.4 / original p.323)

The setting details of the "external input signal select function" are shown below.

| Setting item | | Initial value | Setting details |
|---|---|---|---|
| [Pr.116] | FLS signal selection | 0001H | ■Set with a hexadecimal.<br>H _ _ _ _ → Input type<br>Set the input type used as the external input signal.<br>1(0001H): Servo amplifier*1<br>2(0002H): Buffer memory<br>3(0003H): Link device [FX5-SSC-G]*2 |
| [Pr.117] | RLS signal selection | 0001H | ■Set with a hexadecimal.<br>H _ _ _ _ → Input type<br>Set the input type used as the external input signal.<br>1(0001H): Servo amplifier*1<br>2(0002H): Buffer memory<br>3(0003H): Link device [FX5-SSC-G]*2 |
| [Pr.118] | DOG signal selection | 0001H | ■Set with a hexadecimal.<br>H _ _ _ _ → Input type<br>Set the input type used as the external input signal.<br>1(0001H): Servo amplifier*1<br>2(0002H): Buffer memory<br>3(0003H): Link device [FX5-SSC-G]*2 |
| [Pr.119] | STOP signal selection | 0002H | ■Set with a hexadecimal.<br>H _ _ _ _ → Input type<br>Set the input type used as the external input signal.<br>1(0001H): Servo amplifier*1<br>2(0002H): Buffer memory<br>3(0003H): Link device [FX5-SSC-G]*2 |

*In the original, the "Setting details" cell is merged over the 4 rows [Pr.116] to [Pr.119]. Expanded to each row. The "H _ _ _ _" figure shows that the whole 4-digit hexadecimal value is the input type.

*1 The setting is not available in "[Pr.119] STOP signal selection". If it is set, the error "STOP signal selection error" (error code: 1AD3H [FX5-SSC-S], or error code: 1BD3H [FX5-SSC-G]) occurs and the "[Cd.190] PLC READY" is not turned ON.
*2 For details, refer to the following.
→Page 329 Link Device External Signal Assignment Function [FX5-SSC-G]

> **Point**
> [FX5-SSC-G]
> - When using MR-J5(W)-G, set the servo parameters as follows.
>   - Set "Function selection C-G DI status read selection (PC79.0)" to "Eh".
>   - Set "Function selection D-4 Sensor input method selection (PD41.3)" to "1: Input from controller".
>   - Set "Function selection D-4 Limit switch enabled status selection (PD41.2)" to "1: Enabled only for homing mode"
>   - Set "DI pin polarity selection (PD60)" to "00000000h".
>   - Set "Function selection T-3 Device input polarity 1 (PT29.0)" to "1: Dog detection with ON"
>
>   If the above servo parameters are set to different values, the error "Servo parameter invalid" (error code: 1DC8H) occurs, and the Motion module rewrites the value of said servo parameters to the above values. The servo parameters are enabled after the Motion module or servo amplifier is reset.
> - When parameter automatic setting is enabled, the saved parameters are automatically updated. Check the execution result of automatically updating the saved parameters in the event history.
> - When "[Pr.95] External command signal selection" is set to use the DOG signal of the axis, the DOG signal of the servo amplifier is used regardless of the setting value of "[Pr.118] DOG signal selection". For details of the logic selection for the signal, refer to the following.
>   →Page 850 Devices Compatible with CC-Link IE TSN [FX5-SSC-G]
> - A virtual servo amplifier cannot be used in an external command. When the axis selected in "[Pr.95] External command signal selection" is a virtual servo amplifier, the setting is invalid.

##### When "1: Servo amplifier" is set (「1: サーボアンプ」を設定した場合) (8.4 / original p.324)

The following table shows the pin No. of the external input signal of the servo amplifier to be used.
At MR-JE-B(F) use, refer to the following.
→Page 823 Connection with MR-JE-B(F)

[FX5-SSC-S]

| Pin No. of servo amplifier*1 | Signal name |
|---|---|
| CN3-19(DI3) | DOG |
| CN3-12(DI2) | RLS |
| CN3-2(DI1) | FLS |
| Buffer memory*2 | STOP |

*1 For MR-J4_B_(-RJ) or MR-J5-_B_(-RJ). For details, refer to the manuals of each servo amplifier to be used.
*2 The stop signal cannot be input from the external input signal of the servo amplifier. When inputting a stop signal, set "[Cd.44] External input signal operation device". Refer to the following for the setting details.
→Page 564 [Cd.44] External input signal operation device (Axis 1 to 8)
For MR-J5(W)-G: [Other manual] MR-J5 User's Manual (Hardware)

(Note: "MR-J4_B_(-RJ)" is written as printed in the original, without the hyphen used in "MR-J5-_B_(-RJ)".)

[FX5-SSC-G]

| Pin No. of servo amplifier*1 | Signal name |
|---|---|
| CN3-2 | LSP |
| CN3-12 | LSN |
| CN3-19 | DOG |
| CN3-20 | EM2 |

*1 For MR-J5_G_(-RJ). For details, refer to the manual of the servo amplifier to be used.

##### When "2: Buffer memory" is set (「2: バッファメモリ」を設定した場合) (8.4 / original p.324)

Uses the control data shown below to operate the external input signals (upper/lower stroke limit signal, proximity dog signal, and stop signal).

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.44] | External input signal operation device (Axis 1 to 8) | → | Set the status of the upper/lower limit signal, the proximity dog signal and the stop signal. | 5928<br>5929 |

Refer to the following for the setting details.
→Page 564 [Cd.44] External input signal operation device (Axis 1 to 8)

##### When "3: Link device" is set [FX5-SSC-G] (「3: リンクデバイス」を設定した場合[FX5-SSC-G]) (8.4 / original p.324)

Refer to the following for the setting details.
→Page 329 Link Device External Signal Assignment Function [FX5-SSC-G]

#### Input logic setting method for external input signals (外部入力信号に対する入力論理の設定方法) (8.4 / original p.325-328)

The signal logic can be switched according to the external input signals (upper/lower stroke limit signal (FLS/RLS), proximity dog signal (DOG), stop signal (STOP), and external command signal/switching signal (DI)) of the servo amplifier or external device connected with the Motion module.
For the system that does not use the upper/lower limit signal with b-contact, this function enables the control without wiring by changing to "Positive logic" in parameter logic setting.
When using the upper/lower limit signal, be sure to use in the negative logic (b-contact).
For the interface of the logic selection, the setting area varies depending on the input type and signal type of the external signal.
The logic setting method for external input signals (upper/lower limit signal, proximity dog signal and stop signal) is shown below.

| Input type of "[Pr.116] FLS signal selection" to "[Pr.119] STOP signal selection" | Signal type | Setting area |
|---|---|---|
| 1: Servo amplifier | FLS/RLS/DOG | [Pr.22] Input signal logic selection |
| 2: Buffer memory | FLS/RLS/DOG/STOP | [Pr.22] Input signal logic selection |
| 3: Link device | FLS | [Pr.913] Upper limit signal (FLS): Link device logic setting |
| 3: Link device | RLS | [Pr.923] Lower limit signal (RLS): Link device logic setting |
| 3: Link device | DOG | [Pr.933] Proximity dog signal (DOG): Link device logic setting |
| 3: Link device | STOP | [Pr.943] Stop signal (STOP): Link device logic setting |

*In the original, "[Pr.22] Input signal logic selection" is merged over the rows "1: Servo amplifier" and "2: Buffer memory", and "3: Link device" is merged over 4 rows. Expanded to each row.

##### Upper/lower stroke limit signal, stop signal, and proximity dog signal [FX5-SSC-S] (上／下限リミット信号，停止信号，近点ドグ信号[FX5-SSC-S]) (8.4 / original p.325)

Use the following parameter to switch the logic of the external input signals from the servo amplifier and buffer memory (upper/lower stroke limit signal (FLS/RLS), proximity dog signal (DOG), and stop signal (STOP)).

| Setting item | | Initial value | Setting details |
|---|---|---|---|
| [Pr.22] | Input signal logic selection | 0 | Select the logic of the signal which is input to the Simple Motion module from the external device.<br>0: Negative logic<br>1: Positive logic<br>(Always "0" is set to the part not used.) |

Refer to the following for the setting details.
→Page 454 Basic parameters1

##### Upper/lower stroke limit signal, stop signal, proximity dog signal, and external command/switching signal [FX5-SSC-G] (上／下限リミット信号，停止信号，近点ドグ信号，外部指令／切換え信号[FX5-SSC-G]) (8.4 / original p.325)

Use the following parameter to switch the logic of the external input signals from the servo amplifier and buffer memory (upper/lower stroke limit signal (FLS/RLS), proximity dog signal (DOG), stop signal (STOP), and external command/switching signal (DI)).

| Setting item | | Initial value | Setting details |
|---|---|---|---|
| [Pr.22] | Input signal logic selection | 0 | Select the logic of the signal which is input to the Motion module from the external device.<br>0: Negative logic<br>1: Positive logic<br>(Always "0" is set to the part not used.) |

Refer to the following for the setting details.
→Page 460 Detailed parameters1
When using the signals on the servo amplifier side, match the setting with the input logic setting on the servo amplifier. If the input logic settings do not match, the limit signal may be erroneously detected during home position return. For the input logic specifications of the servo amplifier, refer to the manual of the servo amplifier used.

##### External command signal/switching signal [FX5-SSC-S] (外部指令信号／切換え信号[FX5-SSC-S]) (8.4 / original p.326)

Use the following parameter to switch the logic of the external input signals for the external command signal/switching signal (DI).

| Setting item | | Initial value | Setting details |
|---|---|---|---|
| [Pr.150] | Input terminal logic selection | 0 | Select the logic for the input signal from the external device connected with the Simple Motion module.<br>0: ON at leading edge<br>(When the current is flowed through the input signal terminal: ON,<br>When the current is not flowed through the input signal terminal: OFF)<br>1: ON at trailing edge<br>(When the current is flowed through the input signal terminal: OFF,<br>When the current is not flowed through the input signal terminal: ON)<br>[Input terminal range]<br>b0 to b3 |

Refer to the following for the setting details.
→Page 446 Common parameters

##### External input signal when connecting to MR-J5(W)-G [FX5-SSC-G] (MR-J5(W)-Gを接続する場合の外部入力信号[FX5-SSC-G]) (8.4 / original p.326-327)

The data sent and received with the external input signal when connecting the Motion module to MR-J5(W)-G is shown below.
[Flow of upper/lower stroke limit signal (FLS/RLS) and proximity dog signal (DOG)]
- When using the external input signal of the servo amplifier

The inputted command signal is sent from the servo amplifier to the Motion module, following which the stop command or DOG signal is sent to the servo amplifier after the input signal logic selection processing completes in the Motion module.

[Figure] Signal flow when using the external input signal of the servo amplifier (original p.326)
- DOG signal, Lower limit and Upper limit switches are wired to the MR-J5(W)-G.
- MR-J5(W)-G → Motion module: "CC-Link IE TSN Network cyclic transmission" (arrow toward the Motion module).
- In the Motion module: [Pr.22] Input signal logic selection → Hardware stroke limit processing / DOG signal processing.
- Motion module → MR-J5(W)-G: "CC-Link IE TSN Network cyclic transmission" (arrow back toward the servo amplifier) → "Hardware stroke limit processing / DOG signal processing" block in the MR-J5(W)-G.

- When not using the external input signal of the servo amplifier

The stop command or DOG signal is sent to the servo amplifier after the input signal logic selection processing completes in the Motion module.

[Figure] Signal flow when not using the external input signal of the servo amplifier (original p.326)
- DOG signal, Lower limit and Upper limit switches are wired to the "CPU module or I/O module".
- CPU module or I/O module → Motion module: [Pr.22] Input signal logic selection → "Hardware stroke limit processing / DOG signal processing" and "Signal switching (ON: Limit normal, OFF: Limit abnormal, ON: DOG ON)".
- Motion module → MR-J5(W)-G: "CC-Link IE TSN Network cyclic transmission" → "Hardware stroke limit processing / DOG signal processing" in the MR-J5(W)-G.

- When using the link device (original p.327)

The upper/lower limit switch signal or the DOG signal is sent to the servo amplifier after the input signal logic selection processing completes in the Motion module.

[Figure] Signal flow when using the link device (original p.327)
- DOG signal, Lower limit and Upper limit switches are wired to the "Remote I/O Module".
- Remote I/O Module → Motion module: "[Pr.913] [Pr.923] [Pr.933] Link device logical setting" → "Hardware stroke limit processing / DOG signal processing" and "Signal switching (ON: limit normal, OFF: limit error, ON: DOG ON)".
- Motion module → MR-J5(W)-G: "CC-Link IE TSN Network cyclic transmission" → "Hardware stroke limit processing / DOG signal processing" in the MR-J5(W)-G.

Upper/lower limit signal (Remote I/O → Motion module → MR-J5(W)-G):

| Remote I/O: Upper/lower limit signal bit | Motion module: [Pr.913]Upper limit signal (FLS): Link device logic setting / [Pr.923]Lower limit signal (RLS): Link device logic setting | Motion module: Hardware stroke limit error detection | Motion module: "Lower limit signal (RLS)(b0)" and "Upper limit signal(FLS)(b1)" of "[Md.30] External input signal" | MR-J5(W)-G: Hardware stroke limit error detection |
|---|---|---|---|---|
| 0 | 0: Negative logic | Detect | OFF | Detect |
| 0 | 1: Positive logic | Not detect | ON | Not detect |
| 1 | 0: Negative logic | Not detect | ON | Not detect |
| 1 | 1: Positive logic | Detect | OFF | Detect |

*In the original, the header has group columns "Remote I/O → Motion module → MR-J5(W)-G" with "→" arrow columns between the groups and between "Hardware stroke limit error detection" and "[Md.30]"; the arrow columns are omitted here. The bit values "0" and "1" are each merged over 2 rows. Expanded to each row.

DOG signal (Remote I/O → Motion module → MR-J5(W)-G):

| Remote I/O: DOG signal bit | Motion module: [Pr.933] Proximity dog signal (DOG): Link device logic setting | Motion module: Processing with proximity dog signal detection | Motion module: "Proximity dog signal (DOG)(b6)" of "[Md.30] External input signal" | MR-J5(W)-G: External input signal logic (Function selection T-3 Device input polarity 1 (PT29.0)) | MR-J5(W)-G: Processing with proximity dog signal detection |
|---|---|---|---|---|---|
| 0 | 0: Detection at ON | Not proceed | OFF | 1: Dog detection with on | Not proceed |
| 0 | 1: Detection at OFF | Proceed | ON | 1: Dog detection with on | Proceed |
| 1 | 0: Detection at ON | Proceed | ON | 1: Dog detection with on | Proceed |
| 1 | 1: Detection at OFF | Not proceed | OFF | 1: Dog detection with on | Not proceed |

*In the original, the header has group columns "Remote I/O → Motion module → MR-J5(W)-G" with "→" arrow columns between groups and between "Processing with proximity dog signal detection" and "[Md.30]"; the arrow columns are omitted here. The bit values "0" and "1" are each merged over 2 rows. Expanded to each row.

> **Point**
> The signal status of the servo amplifier is read by the object Digital inputs (Obj. 60FDh), following which the hardware stroke limit processing or DOG signal processing is executed by sending Control DI 5 (Obj. 2D05h) on the controller side.

##### External input signal via link device, external command signal [FX5-SSC-G] (リンクデバイス経由の外部入力信号，外部指令信号[FX5-SSC-G]) (8.4 / original p.328)

The following parameters are used for logic switching when various external input signals and external command signals are input from the link device of the CC-Link IE TSN network.

| Signal type | | Setting item | | Initial value | Setting details*1 |
|---|---|---|---|---|---|
| External input signals*2 | Forced stop signal (EMI) | [Pr.903] | Forced stop signal (EMI): Link device logic setting | 0 | 0: Negative logic<br>1: Positive logic |
| External input signals*2 | Upper limit signal (FLS) | [Pr.913] | Upper limit signal (FLS): Link device logic setting | 0 | 0: Negative logic<br>1: Positive logic |
| External input signals*2 | Lower limit signal (RLS) | [Pr.923] | Lower limit signal (RLS): Link device logic setting | 0 | 0: Negative logic<br>1: Positive logic |
| External input signals*2 | Proximity dog signal (DOG) | [Pr.933] | Proximity dog signal (DOG): Link device logic setting | 0 | 0: Detection at ON<br>1: Detection at OFF |
| External input signals*2 | Stop signal (STOP) | [Pr.943] | Stop signal (STOP): Link device logic setting | 0 | 0: Detection at ON<br>1: Detection at OFF |
| External command signals | Synchronous encoder axis start request | [Pr.1013] | Synchronous encoder axis start request: Link device logic setting | 0 | 0: Negative logic<br>1: Positive logic<br>2: Falling detection<br>3: Rising detection |
| External command signals | Mark detection input signal | [Pr.811] | Mark detection signal detection direction setting | 0 | 0: Rising detection<br>1: Falling detection |

*In the original, "External input signals*2" is merged over 5 rows and "External command signals" over 2 rows; the setting details "0: Negative logic / 1: Positive logic" are merged over the 3 rows EMI/FLS/RLS, and "0: Detection at ON / 1: Detection at OFF" over the 2 rows DOG/STOP. Expanded to each row.

| Setting item | | Initial value | Setting details*3 |
|---|---|---|---|
| [Pr.22] | Input signal logic selection | 0 | Select the logic of the signal to be input to the Motion module from the outside.<br>0: Negative logic<br>1: Positive logic<br>• b0: Lower limit<br>• b1: Upper limit<br>• b3: Stop signal<br>• b6: Proximity dog signal |

*1 For the setting details, refer to the following.
→Page 329 Link Device External Signal Assignment Function [FX5-SSC-G]
*2 For the logic setting of the external input signals, refer to the following.
→Page 850 Devices Compatible with CC-Link IE TSN [FX5-SSC-G]
*3 For the setting details, refer to the following.
→Page 460 Detailed parameters1

##### Manual pulse generator/Incremental synchronous encoder input [FX5-SSC-S] (手動パルサ／INC同期エンコーダ入力[FX5-SSC-S]) (8.4 / original p.328)

Use the following parameter to switch the external input signal logic for the manual pulse generator/incremental synchronous encoder.

| Setting item | | Initial value | Setting details |
|---|---|---|---|
| [Pr.151] | Manual pulse generator/Incremental synchronous encoder input logic selection | 0 | Select the input signal logic to the Simple Motion module from the manual pulse generator/incremental synchronous encoder.<br>0: Negative logic<br>1: Positive logic |

Refer to the following for the setting details.
→Page 444 Basic Setting

##### Precautions on parameter setting (パラメータ設定上の注意事項) (8.4 / original p.328)

- The external I/O signal logic switching parameters are validated when the "[Cd.190] PLC READY" is turned OFF to ON. (The logic is negative right after power-on.)
- If the logic of each signal is set erroneously, the operation may not be carried out correctly. Before setting, check the specifications of the equipment to be used.

#### Input filter setting method for external input signals (外部入力信号に対する入力フィルタの設定方法) (8.4 / original p.329)

The input filter is used to suppress chattering when the external input signal is chattering by noise, etc.
The setting area of the input filter varies by the input type of "[Pr.116] FLS signal selection" to "[Pr.119] STOP signal selection".

| Input type of "[Pr.116] FLS signal selection" to "[Pr.119] STOP signal selection" | Setting area |
|---|---|
| 1: Servo amplifier | Servo parameter "Input filter setting (PD11)"*1 |
| 2: Buffer memory | No setting (No input filter when the buffer memory is set.) |
| 3: Link device [FX5-SSC-G] | Set at the device station. |

*1 Refer to the manuals of each servo amplifier to be used.
For MR-J5(W)-G, Set with the servo parameter "Input filter setting (PD11)".
[Other manual] MR-J5-G/MR-J5W-G User's Manual (Parameters)

#### Program (プログラム) (8.4 / original p.329-330)

The following shows the program example to operate "[Cd.44] External input signal operation device (Axis 1 to 8)" of axis 1 using the limit switch connected to the CPU module when "2: Buffer memory" is set in "[Pr.116] FLS signal selection" to "[Pr.119] STOP signal selection".

[Figure] Wiring (original p.329)
- Limit switches FLS, RLS, DOG and STOP are connected to the CPU module inputs X0 to X3.
- The Simple Motion module/Motion module is mounted to the right of the CPU module.

##### Program example (プログラム例) (8.4 / original p.330)

```
; Axis 1 FLS operation
(0)
LD    G_bInputAxsi1FLSReq                                    ; Axis 1 FLS ON command
OUT   FX5SSC_1.stSysCtrl_D.uExternalInputOperationDevice1_D.0 ; RW:External input signal operation device (Axis 1 to 4) (Direct)
; Axis 1 RLS operation
(31)
LD    G_bInputAxsi1RLSReq                                    ; Axis 1 RLS ON command
OUT   FX5SSC_1.stSysCtrl_D.uExternalInputOperationDevice1_D.1 ; RW:External input signal operation device (Axis 1 to 4) (Direct)
; Axis 1 DOG operation
(62)
LD    G_bInputAxsi1DOGReq                                    ; Axis 1 DOG ON command
OUT   FX5SSC_1.stSysCtrl_D.uExternalInputOperationDevice1_D.2 ; RW:External input signal operation device (Axis 1 to 4) (Direct)
; Axis 1 STOP operation
(93)
LD    G_bInputAxsi1STOPReq                                   ; Axis 1 STOP ON command
OUT   FX5SSC_1.stSysCtrl_D.uExternalInputOperationDevice1_D.3 ; RW:External input signal operation device (Axis 1 to 4) (Direct)
```

- All contacts are NO (a) contacts; each rung has one contact and one coil. Step numbers (0), (31), (62), (93) are as shown in the ladder.
- The label names "G_bInputAxsi1..." ("Axsi" instead of "Axis") are written as printed in the original. The coil label in the ladder is "uExternalInputOperationDevice1_D.n", while the label table below prints "uExternalInputOperationDevice_D[0].n"; both are kept as printed.

In the program examples, the labels to be used are assigned as follows.

| Classification | Label name | Description |
|---|---|---|
| Module label | FX5SSC_1.stSysCtrl_D.uExternalInputOperationDevice_D[0].0 | Axis 1 FLS |
| Module label | FX5SSC_1.stSysCtrl_D.uExternalInputOperationDevice_D[0].1 | Axis 1 RLS |
| Module label | FX5SSC_1.stSysCtrl_D.uExternalInputOperationDevice_D[0].2 | Axis 1 DOG |
| Module label | FX5SSC_1.stSysCtrl_D.uExternalInputOperationDevice_D[0].3 | Axis 1 STOP |
| Global label | Defines the global labels to set the assignment device as follows. | (see the label table below) |

*In the original, "Module label" is merged over 4 rows. Expanded to each row. For "Global label", the "Label name" and "Description" cells are merged and the label definition screen is embedded under the text; the screen is separated into the table below.

Global label definition (transcribed from the screen image in the original):

| No. | Label Name | Data Type | Class | Assign (Device/Label) |
|---|---|---|---|---|
| 1 | G_bInputAxsi1FLSReq | Bit | VAR_GLOBAL | X0 |
| 2 | G_bInputAxsi1RLSReq | Bit | VAR_GLOBAL | X1 |
| 3 | G_bInputAxsi1DOGReq | Bit | VAR_GLOBAL | X2 |
| 4 | G_bInputAxsi1STOPReq | Bit | VAR_GLOBAL | X3 |

## 8.5 Link Device External Signal Assignment Function [FX5-SSC-G] (リンクデバイス外部信号割付け機能[FX5-SSC-G]) (8.5 / original p.331-337)

This function assigns link devices to the external signals of the Motion module.
Signals such as the upper/lower limit signal and proximity dog signal can be assigned to link devices.

> **Point**
> - The following are available in the software version 1.004 or later.
>   - Synchronous encoder via link device
>   - Mark detection (link device input)
> - The following are available in the software version 1.005 or later.
>   - Forced stop signal (EMI)
>   - Upper limit signal (FLS)
>   - Lower limit signal (RLS)
>   - Proximity dog signal (DOG)
>   - Stop signal (STOP)

#### Signals that can be assigned (割付け可能な信号) (8.5 / original p.331-332)

The following signals used in the Motion module can be assigned to the link devices of the CC-Link IE TSN Network. The same link device can be assigned to multiple external signals.

##### Bit device (ビットデバイス) (8.5 / original p.331)

- External input signal

○: Setting possible, ×: Setting not possible

| External signal | RX 1 bit | RX 1 word | RX 2 words | RY 1 bit | RY 1 word | RY 2 words | RWr 1 bit | RWr 1 word | RWr 2 words | RWw 1 bit | RWw 1 word | RWw 2 words | Settable points |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Forced stop signal (EMI) | ○ | × | × | ○ | × | × | ○ | × | × | ○ | × | × | 1 point/1 module*1 |
| Upper limit signal (FLS) | ○ | × | × | ○ | × | × | ○ | × | × | ○ | × | × | 1 point/1 axis |
| Lower limit signal (RLS) | ○ | × | × | ○ | × | × | ○ | × | × | ○ | × | × | 1 point/1 axis |
| Proximity dog signal (DOG) | ○ | × | × | ○ | × | × | ○ | × | × | ○ | × | × | 1 point/1 axis |
| Stop signal (STOP) | ○ | × | × | ○ | × | × | ○ | × | × | ○ | × | × | 1 point/1 axis |

*In the original, RX/RY/RWr/RWw are two-level headers (1 bit / 1 word / 2 words); flattened into single column names.

*1 Only the setting value for the axis 1 is valid.

- External command signal

○: Setting possible, ×: Setting not possible

| External signal | RX 1 bit | RX 1 word | RX 2 words | RY 1 bit | RY 1 word | RY 2 words | RWr 1 bit | RWr 1 word | RWr 2 words | RWw 1 bit | RWw 1 word | RWw 2 words | Settable points |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Synchronous encoder axis start request*1*2 | ○ | × | × | ○ | × | × | ○ | × | × | ○ | × | × | 1 point/1 axis |
| Input signal for mark detection*1*3 | ○ | × | × | ○ | × | × | ○ | × | × | ○ | × | × | 1 point/1 mark detection setting |

*In the original, RX/RY/RWr/RWw are two-level headers (1 bit / 1 word / 2 words); flattened into single column names.

*1 This is the accuracy of the operation cycle.
*2 Set by synchronous encoder axis parameters via link device. For details, refer to "Synchronous Encoder Axis" in the following manual.
[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Advanced Synchronous Control)
*3 Set by mark detection setting parameters. Refer to the following for details.
→Page 355 Mark Detection Function

##### Word device (ワードデバイス) (8.5 / original p.332)

- External input signal

○: Setting possible, ×: Setting not possible

| External signal | RX 1 bit | RX 1 word | RX 2 words | RY 1 bit | RY 1 word | RY 2 words | RWr 1 bit | RWr 1 word | RWr 2 words | RWw 1 bit | RWw 1 word | RWw 2 words | Settable points |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Synchronous encoder input*1*2 | × | ○ | ○ | × | ○ | ○ | × | ○ | ○ | × | ○ | ○ | 1 point/1 axis |

*In the original, RX/RY/RWr/RWw are two-level headers (1 bit / 1 word / 2 words); flattened into single column names.

*1 When assigning RX/RY, the setting is made in units of 16 points.
*2 Set by synchronous encoder axis parameters via link device. For details, refer to "Synchronous Encoder Axis" in the following manual.
[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Advanced Synchronous Control)

#### Operation in case of data link error during communication (通信中にデータリンク異常になった場合の動作) (8.5 / original p.332)

##### Bit device (ビットデバイス) (8.5 / original p.332)

Signals are as follows regardless of the logical setting.

| External signal | Operation details |
|---|---|
| Forced stop signal | Forced stop of all axes of the servo amplifier. |
| Upper/lower limit signal | Outside the upper/lower limit range. |
| Proximity dog signal | The proximity dog signal becomes invalid. |
| Stop signal | The control of the axis is stopped. |
| Other signals | No request is made. |

##### Word device (ワードデバイス) (8.5 / original p.332)

Synchronous encoder axis: When the connection is in progress, the connection is disabled.

#### Setting method (設定方法) (8.5 / original p.332-334)

Set this function with link device external signal assignment parameters. Refer to the following for details on each setting.
→Page 333 Related buffer memory
→Page 422 List of Buffer Memory Addresses
For the setting method of the mark detection input signal, refer to the following.
→Page 355 Mark Detection Function
For the setting method of the synchronous encoder axis start request and the synchronous encoder input, refer to "Synchronous Encoder Axis" in the following manual.
[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Advanced Synchronous Control)

##### Forced stop signal (緊急停止信号) (8.5 / original p.332-333)

Set the following for the forced stop signal.
- Set to use the link device for the forced stop signal.

| Item | | Details | Buffer memory address |
|---|---|---|---|
| [Pr.82] | Forced stop valid/invalid selection | Set "3: Valid (Link device)".*1 | 35 |

*1 If "3: Valid (Link device)" is set in "[Pr.82] Forced stop valid/invalid selection", and the link device external signal assignment parameter is not set, the error "Forced stop signal link device incorrect configuration" (error code: 1F13H) occurs and the READY signal ([Md.140] Module status: b0) does not turn ON.

- Set the link device external signal assignment parameter to be used as the forced stop signal. (original p.333)

| Item | | Details | Buffer memory address |
|---|---|---|---|
| [Pr.900] | Forced stop signal (EMI): Link device type | Set the link device type for use. | 58014 |
| [Pr.901] | Forced stop signal (EMI): Link device start No. | Set the link device No. for use. | 58015 |
| [Pr.902] | Forced stop signal (EMI): Link device bit specification | Set the bit No. that is used when "13H: RWr" and "14H: RWw" are set to the link device type. | 58016 |
| [Pr.903] | Forced stop signal (EMI): Link device logic setting | Set the logic for assignment signal.<br>• 0: Negative logic<br>• 1: Positive logic | 58017 |

##### FLS signal, RLS signal (FLS信号，RLS信号) (8.5 / original p.333)

Set the FLS signal and the RLS signal of the corresponding axis as follows.
- Set the corresponding signal to use the link device and set the corresponding signal logic.

n: Axis No. - 1

| Item | | Details | Buffer memory address |
|---|---|---|---|
| [Pr.116] | FLS signal selection | Set "3: Link device".*1 | 116+150n |
| [Pr.117] | RLS signal selection | Set "3: Link device".*1 | 117+150n |

*In the original, the "Details" cell is merged over the 2 rows. Expanded to each row.

*1 If "3: Link device" is set in "[Pr. 116] FLS signal selection" and "[Pr. 117] RLS signal selection", and the link device external signal assignment parameter is not set, the error "FLS signal link device incorrect configuration" (error code: 1F14H) or the error "RLS signal link device incorrect configuration" (error code: 1F15H) occurs, and the READY signal ([Md.140] Module status: b0) does not turn ON.

- Set the link device external signal assignment parameter to be used as the corresponding signal.

n: Axis No. - 1

| Item | | Details | Buffer memory address |
|---|---|---|---|
| [Pr.910] | Upper limit signal (FLS): Link device type | Set the link device type for use. | 36000+20n |
| [Pr.920] | Lower limit signal (RLS): Link device type | Set the link device type for use. | 36005+20n |
| [Pr.911] | Upper limit signal (FLS): Link device start No. | Set the link device No. for use. | 36001+20n |
| [Pr.921] | Lower limit signal (RLS): Link device start No. | Set the link device No. for use. | 36006+20n |
| [Pr.912] | Upper limit signal (FLS): Link device bit specification | Set the bit No. that is used when "13H: RWr" and "14H: RWw" are set to the link device type. | 36002+20n |
| [Pr.922] | Lower limit signal (RLS): Link device bit specification | Set the bit No. that is used when "13H: RWr" and "14H: RWw" are set to the link device type. | 36007+20n |
| [Pr.913] | Upper limit signal (FLS): Link device logic setting | Set the logic for assignment signal.<br>• 0: Negative logic<br>• 1: Positive logic | 36003+20n |
| [Pr.923] | Lower limit signal (RLS): Link device logic setting | Set the logic for assignment signal.<br>• 0: Negative logic<br>• 1: Positive logic | 36008+20n |

*In the original, each "Details" cell is merged over the FLS/RLS pair of rows. Expanded to each row.

##### DOG signal, STOP signal (DOG信号，STOP信号) (8.5 / original p.334)

Set the DOG signal and the STOP signal of the corresponding axis as follows.
- Set the corresponding signal to use the link device and set the corresponding signal logic.

n: Axis No. - 1

| Item | | Details | Buffer memory address |
|---|---|---|---|
| [Pr.118] | DOG signal selection | Set "3: Link device".*1 | 118+150n |
| [Pr.119] | STOP signal selection | Set "3: Link device".*1 | 119+150n |

*In the original, the "Details" cell is merged over the 2 rows. Expanded to each row.

*1 If "3: Link device" is set in "[Pr. 118] DOG signal selection" and "[Pr. 119] STOP signal selection", and the link device external signal assignment parameter is not set, the error "DOG signal link device incorrect configuration" (error code: 1F16H) or the error "STOP signal link device incorrect configuration" (error code: 1F17H) occurs, and the READY signal ([Md.140] Module status: b0) does not turn ON.

- Set the link device external signal assignment parameter to be used as the corresponding signal.

n: Axis No. - 1

| Item | | Details | Buffer memory address |
|---|---|---|---|
| [Pr.930] | Proximity dog signal (DOG): Link device type | Set the link device type for use. | 36010+20n |
| [Pr.940] | Stop signal (STOP): Link device type | Set the link device type for use. | 36015+20n |
| [Pr.931] | Proximity dog signal (DOG): Link device start No. | Set the link device No. for use. | 36011+20n |
| [Pr.941] | Stop signal (STOP): Link device start No. | Set the link device No. for use. | 36016+20n |
| [Pr.932] | Proximity dog signal (DOG): Link device bit specification | Set the bit No. that is used when "13H: RWr" and "14H: RWw" are set to the link device type. | 36012+20n |
| [Pr.942] | Stop signal (STOP): Link device bit specification | Set the bit No. that is used when "13H: RWr" and "14H: RWw" are set to the link device type. | 36017+20n |
| [Pr.933] | Proximity dog signal (DOG): Link device logic setting | Set the logic for assignment signal.<br>• 0: Detection at ON<br>• 1: Detection at OFF | 36013+20n |
| [Pr.943] | Stop signal (STOP): Link device logic setting | Set the logic for assignment signal.<br>• 0: Detection at ON<br>• 1: Detection at OFF | 36018+20n |

*In the original, each "Details" cell is merged over the DOG/STOP pair of rows. Expanded to each row.

> **Point**
> Using a link device No. that is not assigned in the network configuration settings does not result in an error/warning. The signal is detected when the link device or the corresponding buffer memory is operated.
> If the link device No. exceeds the setting range of the start No., an error/warning occurs.

#### Monitoring method (モニタ方法) (8.5 / original p.334)

The input status of each bit device signal can be monitored by the following signal.
- External command signal

n: Axis No. - 1

| Monitor item | | Storage details | Buffer memory address |
|---|---|---|---|
| [Md.50] | Forced stop input | Forced stop signal (EMI) | 4231 |
| [Md.30] | External input signal | • b0: Lower limit signal (RLS)<br>• b1: Upper limit signal (FLS)<br>• b3: Stop signal (STOP)<br>• b6: Proximity dog signal (DOG) | 2416+100n |

(Note: The original prints "External command signal" as the bullet title above this table as well as above the next one, although this table lists external input signals; kept as printed.)

- External command signal

j: Synchronous encoder axis No. - 1

| Monitor item | | Storage details | Buffer memory address |
|---|---|---|---|
| [Md.325] | Synchronous encoder axis status | b6: Start command flag | 35210+20j |

#### Related buffer memory (関連バッファメモリ) (8.5 / original p.335)

Each external signal can be assigned by setting the following buffer memories.

> **Point**
> - Refer to the following for mark detection setting parameters.
>   →Page 355 Mark Detection Function
> - For the synchronous encoder axis parameters via link device, refer to "Synchronous Encoder Axes" in the following manual.
>   [Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Advanced Synchronous Control)

##### For bit device setting (ビットデバイス設定用) (8.5 / original p.335)

n: Axis No. - 1

| Setting item | | Setting details, setting value | Buffer memory address |
|---|---|---|---|
| [Pr.900] | Forced stop signal (EMI): Link device type | Set the link device type for use.<br>• Others: Invalid<br>• 11H: RX<br>• 12H: RY<br>• 13H: RWr<br>• 14H: RWw<br>Fetch cycle: At power supply ON/the CPU module reset | 58014 |
| [Pr.910] | Upper limit signal (FLS): Link device type | (same as [Pr.900]) | 36000+20n |
| [Pr.920] | Lower limit signal (RLS): Link device type | (same as [Pr.900]) | 36005+20n |
| [Pr.930] | Proximity dog signal (DOG): Link device type | (same as [Pr.900]) | 36010+20n |
| [Pr.940] | Stop signal (STOP): Link device type | (same as [Pr.900]) | 36015+20n |
| [Pr.901] | Forced stop signal (EMI): Link device start No. | Set the link device type for use.*1<br>• RX/RY: 0 to 1FFFH<br>• RWr/RWw: 0 to 3FFH<br>Fetch cycle: At power supply ON/the CPU module reset | 58015 |
| [Pr.911] | Upper limit signal (FLS): Link device start No. | (same as [Pr.901]) | 36001+20n |
| [Pr.921] | Lower limit signal (RLS): Link device start No. | (same as [Pr.901]) | 36006+20n |
| [Pr.931] | Proximity dog signal (DOG): Link device start No. | (same as [Pr.901]) | 36011+20n |
| [Pr.941] | Stop signal (STOP): Link device start No. | (same as [Pr.901]) | 36016+20n |
| [Pr.902] | Forced stop signal (EMI): Link device bit specification | Set the bit No. that is used when "13H: RWr" and "14H: RWw" are set to the link device type.*2<br>• 00H to 0FH<br>Fetch cycle: At power supply ON/the CPU module reset | 58016 |
| [Pr.912] | Upper limit signal (FLS): Link device bit specification | (same as [Pr.902]) | 36002+20n |
| [Pr.922] | Lower limit signal (RLS): Link device bit specification | (same as [Pr.902]) | 36007+20n |
| [Pr.932] | Proximity dog signal (DOG): Link device bit specification | (same as [Pr.902]) | 36012+20n |
| [Pr.942] | Stop signal (STOP): Link device bit specification | (same as [Pr.902]) | 36017+20n |
| [Pr.903] | Forced stop signal (EMI): Link device logic setting | Set the logic for assignment signal. (Only the 0th bit is valid.)<br>• 0: Negative logic<br>When link device relevant bit = 0<br>EMI: Forced stop input ON (Forced stop)<br>FLS, RLS: Limit signal is OFF (Limit over)<br>• 1: Positive logic<br>Opposite of the negative logic<br>Fetch cycle: At power supply ON/the CPU module reset | 58017 |
| [Pr.913] | Upper limit signal (FLS): Link device logic setting | (same as [Pr.903]) | 36003+20n |
| [Pr.923] | Lower limit signal (RLS): Link device logic setting | (same as [Pr.903]) | 36008+20n |
| [Pr.933] | Proximity dog signal (DOG): Link device logic setting | Set the logic for assignment signal. (Only the 0th bit is valid.)<br>• 0: Detection at ON<br>The link device status and the signal status are not inverted.<br>When the link device is set to 0, the corresponding signal is set to OFF.<br>When the link device is set to 1, the corresponding signal is set to ON.<br>• 1: Detection at OFF<br>The link device status and the signal status are inverted.<br>When the link device is set to 0, the corresponding signal is set to ON.<br>When the link device is set to 0, the corresponding signal is set to OFF.<br>Fetch cycle: At power supply ON/the CPU module reset | 36013+20n |
| [Pr.943] | Stop signal (STOP): Link device logic setting | (same as [Pr.933]) | 36018+20n |

*In the original, the "Setting details, setting value" cell is merged over each group of rows: [Pr.900]/[Pr.910]/[Pr.920]/[Pr.930]/[Pr.940] (5 rows), [Pr.901] to [Pr.941] (5 rows), [Pr.902] to [Pr.942] (5 rows), [Pr.903]/[Pr.913]/[Pr.923] (3 rows), [Pr.933]/[Pr.943] (2 rows). Because the merged text is long, it is written once on the first row of each group and the other rows say "(same as ...)".
(Note: For [Pr.901] to [Pr.941] the original prints "Set the link device type for use.*1" although the item is the start No.; and in "1: Detection at OFF" the last line is printed as "When the link device is set to 0, the corresponding signal is set to OFF." (probably "set to 1" is intended). Both kept as printed.)

*1 If the setting value is outside the setting range, the error "Outside the link device start No. range" (error code: 1F10H) occurs and the corresponding external signal becomes invalid.
*2 If the setting value is outside the setting range, the error "Outside the link device bit specification range" (error code: 1F11H) occurs and the corresponding external signal becomes invalid.

#### Setting example of link device external signal assignment (外部入力信号のリンクデバイス割付けの設定例) (8.5 / original p.336-337)

Ex.
When using link device as upper/lower limit signal (FLS/RLS)

[Figure] System configuration (original p.336)
- Motion module (mounted on the CPU module) — CC-Link IE TSN cable — MR-J5-G servo amplifier (with servo motor "Axis 1") — NZ2GN2S1-32D (IP address: 192.168.3.2) — "Sensor" wired to the NZ2GN2S1-32D.

In this example, the signal used as the upper limit signal (FLS) is assigned to RX0 and the signal used as the lower limit signal (RLS) is assigned to RX1.

##### Network configuration setting (ネットワーク構成設定) (8.5 / original p.336)

[Figure] CC-Link IE TSN Configuration screen (Mounting Position No.: 1[U1]) (original p.336)
- Mode Setting: Online (Unicast Mode); Assignment Method: Point/Start; Cyclic Transmission Time (Min.): 50.00 us; Communication Period Interval (Min.): 244.00 us.
- No.0: Host Station, STA#0, Master Station.
- No.1: MR-J5-G, STA#1, Remote Station, "Motion Control Station" checked.
- No.2: NZ2GN2S1-32D, STA#2, Remote Station, "Motion Control Station" unchecked; RX Setting Points 32, Start 0000, End 001F; RY Setting Points 32, Start 0000, End 001F; RWr Setting Points 4, Start 0018, End 001B; RWw Setting Points 4, Start 0018, End 001B.
- Callout: Uncheck "Motion Control Station". (for the NZ2GN2S1-32D row)

In this example, the following link devices are used.
- Remote input (RX)

| Device No. | Application |
|---|---|
| RX0 | Used as the upper limit signal (FLS). |
| RX1 | Used as the lower limit signal (RLS). |

##### Link device external input signal assignment parameter (リンクデバイス外部入力信号割付けパラメータ) (8.5 / original p.337)

Set the link device to be used as the upper/lower limit signal (FLS/RLS).

| Parameter | Setting value |
|---|---|
| [Pr.910] Upper limit signal (FLS): Link device type | 11h: RX |
| [Pr.911] Upper limit signal (FLS): Link device start No. | H0000 |
| [Pr.912] Upper limit signal (FLS): Link device bit specification | Not necessary when "11h: RX" or "12h: RY" is selected for link device type. |
| [Pr.913] Upper limit signal (FLS): Link device logic setting | 0: Negative logic |
| [Pr.920] Lower limit signal (RLS): Link device type | 11h: RX |
| [Pr.921] Lower limit signal (RLS): Link device start No. | H0001 |
| [Pr.922] Lower limit signal (RLS): Link device bit specification | Not necessary when "11h: RX" or "12h: RY" is selected for link device type. |
| [Pr.923] Lower limit signal (RLS): Link device logic setting | 0: Negative logic |

[Figure] MELSOFT Simple Motion Module Setting Function screen, 01:FX5-40SSC-G(S) Parameter, Axis #1 (original p.337)
- Upper limit signal (Set the link device to assign upper limit signal.): Pr.910:Type = 11h:RX; Pr.911:Start No. = H0000; Pr.912:Bit specification = H0 (grayed); Pr.913:Logic setting = 0:Negative Logic.
- Lower limit signal (Set the link device to assign lower limit signal.): Pr.920:Type = 11h:RX; Pr.921:Start No. = H0000; Pr.922:Bit specification = H0 (grayed); Pr.923:Logic setting = 0:Negative Logic.
- Proximity dog signal (Set the link device to assign proximity dog signal.): Pr.930:Type = 00h:Invalid; Pr.931:Start No. = H0000; Pr.932:Bit specification = H0; Pr.933:Logic setting = 0:Detection at ON.
- (Note: the screen image shows Pr.921:Start No. = H0000, while the table above gives H0001; both as printed.)

#### Restrictions (制約事項) (8.5 / original p.337)

- Use the communication cycle setting of the network configuration settings in the basic cycle. If not used in the basic cycle, the signal detection accuracy will be poor.
- The fetch timing of the link device fluctuates by 1 operation cycle.

## 8.6 History Monitor Function (履歴モニタ機能) (8.6 / original p.338-341)

This function monitors starting history and current value history stored in the buffer memory of the Simple Motion module/Motion module on the operation monitor of an engineering tool.

#### Starting history (始動履歴) (8.6 / original p.338)

The starting history logs of operations such as positioning operation, JOG operation, and manual pulse generator operation can be monitored. The latest 64 logs are stored all the time. This function allows users to check the operation sequence (whether the operations have been started in a predetermined sequence) at system start-up.
For the starting history check method, refer to "Help" in the "Simple Motion Module Setting Function" of an engineering tool.

> **Point**
> Set the clock of CPU module.
> Refer to the following for setting method.
> [Other manual] GX Works3 Operating Manual
> There may be an error in tens of ms between the clock data of the CPU and the time data of the Simple Motion module/Motion module.

#### Current value history (現在値履歴) (8.6 / original p.339-341)

The current value history data of each axis can be monitored. The following shows about the current value history data of each axis.

| Monitor details | Monitor item |
|---|---|
| Latest backup data<br>The number of backup: Once | Command position value |
| Latest backup data<br>The number of backup: Once | Servo command value |
| Latest backup data<br>The number of backup: Once | Encoder position within one revolution*1 |
| Latest backup data<br>The number of backup: Once | Encoder multiple revolution counter |
| Latest backup data<br>The number of backup: Once | Time 1 (Year: month)*2 |
| Latest backup data<br>The number of backup: Once | Time 2 (Day: hour)*2 |
| Latest backup data<br>The number of backup: Once | Time 3 (Minute: second)*2 |
| Latest backup data<br>The number of backup: Once | Latest backup data pointer |
| Backup data at the power disconnection<br>The number of backup: 4 times | Command position value |
| Backup data at the power disconnection<br>The number of backup: 4 times | Servo command value |
| Backup data at the power disconnection<br>The number of backup: 4 times | Encoder position within one revolution*1 |
| Backup data at the power disconnection<br>The number of backup: 4 times | Encoder multiple revolution counter |
| Backup data at the power disconnection<br>The number of backup: 4 times | Time 1 (Year: month)*2 |
| Backup data at the power disconnection<br>The number of backup: 4 times | Time 2 (Day: hour)*2 |
| Backup data at the power disconnection<br>The number of backup: 4 times | Time 3 (Minute: second)*2 |
| Backup data at the power disconnection<br>The number of backup: 4 times | Backup data pointer |
| Backup data at the power on<br>The number of backup: 4 times | Command position value |
| Backup data at the power on<br>The number of backup: 4 times | Servo command value |
| Backup data at the power on<br>The number of backup: 4 times | Encoder position within one revolution*1 |
| Backup data at the power on<br>The number of backup: 4 times | Encoder multiple revolution counter |
| Backup data at the power on<br>The number of backup: 4 times | Time 1 (Year: month)*2 |
| Backup data at the power on<br>The number of backup: 4 times | Time 2 (Day: hour)*2 |
| Backup data at the power on<br>The number of backup: 4 times | Time 3 (Minute: second)*2 |
| Home position return data<br>The number of backup: Once | Command position value |
| Home position return data<br>The number of backup: Once | Servo command value |
| Home position return data<br>The number of backup: Once | Encoder position within one revolution*1 |
| Home position return data<br>The number of backup: Once | Encoder multiple revolution counter |
| Home position return data<br>The number of backup: Once | Time 1 (Year: month)*2 |
| Home position return data<br>The number of backup: Once | Time 2 (Day: hour)*2 |
| Home position return data<br>The number of backup: Once | Time 3 (Minute: second)*2 |

*In the original, each "Monitor details" cell is merged over its rows (8 rows for Latest backup data, 8 rows for Backup data at the power disconnection, 7 rows for Backup data at the power on, 7 rows for Home position return data). Expanded to each row.

*1 [FX5-SSC-S]
When MR-J5(W)-B is connected, the value is multiplied by the multiplicative inverse of the electronic gear ratio of the servo amplifier (command unit). The same data as MR-J4(W)-B can be stored by configuring the electronic gear setting of the servo amplifier.
[FX5-SSC-G]
The value multiplied by the multiplicative inverse of the electronic gear ratio of the servo amplifier (command unit) is displayed.
*2 Displays a value set by the clock function of the CPU module.

##### Latest backup data (最新バックアップデータ) (8.6 / original p.340)

The latest backup data outputs the following data saved in the fixed cycle to the buffer memory.

- Command position value
- Servo command value
- Encoder position within one revolution*1
- Encoder multiple revolution counter
- Time 1 (Year: month) data
- Time 2 (Day: hour) data
- Time 3 (Minute: second) data
- Latest backup data pointer

*1 [FX5-SSC-S]
When MR-J5(W)-B is connected, the value is multiplied by the multiplicative inverse of the electronic gear ratio of the servo amplifier (command unit). The same data as MR-J4(W)-B can be stored by configuring the electronic gear setting of the servo amplifier.
[FX5-SSC-G]
The value multiplied by the multiplicative inverse of the electronic gear ratio of the servo amplifier (command unit) is displayed.

The latest backup data starts outputting the data after the power on.
After the home position is established in the absolute system, the data becomes valid and outputs the current value.
[FX5-SSC-S]
The following servo amplifier and servo motor are connected artificially during amplifier-less operation. Therefore, the encoder position within one revolution and encoder multiple revolution counter made virtually by the command value are output.

| [Pr.97] SSCNET setting | [Pr.100] Servo series | Servo amplifier type | Motor type |
|---|---|---|---|
| 1: SSCNETⅢ/H | 128: MR-J5-_B_(-RJ), MR-J5W_-_B (2-axis type, 3-axis type) | MR-J5-10B | Rotary servo motor (Resolution per servo motor rotation: 4194304 pulses/rev) |
| 1: SSCNETⅢ/H | Other than "128: MR-J5-_B_(-RJ), MR-J5W_-_B (2-axis type, 3-axis type)" | MR-J4-10B | HG-KR053 (Resolution per servo motor rotation: 4194304 pulses/rev) |
| 0: SSCNETⅢ | — | MR-J3-10B | HF-KP053 (Resolution per servo motor rotation: 262144 pulses/rev) |

*In the original, "1: SSCNETⅢ/H" is merged over 2 rows. Expanded to each row.

##### Backup data at the power disconnection (電源断時バックアップデータ) (8.6 / original p.340)

- The detail of the latest backup data right before the power disconnection is output to the buffer memory.
- The backup data at the power disconnection starts being output after the power on.
- The detail of the latest backup data right before the power disconnection used in the absolute system setting is output, regardless of the setting of the absolute system or incremental system.
- If the data has never been used in the absolute system in the incremental system setting, "0" is output in all storage items.

##### Backup data at the power on (電源投入時バックアップデータ) (8.6 / original p.340)

- After the power on, the detail of the data which restored the current value is output to the buffer memory.
- The backup data at the power on starts being output after the power on.
- The warning "Home position return data incorrect" (warning code: 093CH [FX5-SSC-S], or warning code: 0D3CH [FX5-SSC-G]) is set in the error/warning code at current value restoration.
- When the incremental system is set, the detail of the backup data at power supply on used in the absolute system setting is output. If the data has never been used in the absolute system, "0" is output in all storage items.

[FX5-SSC-S]
- If the current value cannot be restored in the absolute system, "0" is set to the command position value and servo command value.

[FX5-SSC-G]
- When current value restoration could not be performed in the absolute position system, "0" is set to the command position value, the encoder position within one revolution, the encoder multiple revolution counter and the feedback value from the servo amplifier is set to the servo command value.
- When 32-bit restoration is performed in the absolute position system, "0" is set to the encoder position within one revolution and the encoder multiple revolution counter at power supply on.

##### Home position return data (原点復帰時データ) (8.6 / original p.341)

The following data saved at home position return completion to the buffer memory.

- Command position value at home position return completion
- Servo command value at home position return completion
- Encoder position within one revolution of absolute position reference point data*1
- Encoder multiple revolution counter of absolute position reference point data
- Time 1 (Year: month) data
- Time 2 (Day: hour) data
- Time 3 (Minute: second) data

*1 [FX5-SSC-S]
When MR-J5(W)-B is connected, the value is multiplied by the multiplicative inverse of the electronic gear ratio of the servo amplifier (command unit). The same data as MR-J4(W)-B can be stored by configuring the electronic gear setting of the servo amplifier.
[FX5-SSC-G]
The value multiplied by the multiplicative inverse of the electronic gear ratio of the servo amplifier (command unit) is displayed.

The data becomes valid only when the absolute system is set.
If the data has never been used in the absolute system in the incremental system setting, "0" is output in all storage items.

## 8.7 Amplifier-less Operation Function [FX5-SSC-S] (アンプなし運転機能[FX5-SSC-S]) (8.7 / original p.342-345)

The positioning control of Simple Motion module without servo amplifiers connection can be executed in the amplifier-less function. This function is used to debug of user program or simulate of positioning operation at the start.

#### Control details (制御内容) (8.7 / original p.342)

Switch the mode from the normal operation mode (with servo amplifier connection) to the amplifier-less operation mode (without servo amplifier connection) to use the amplifier-less operation function.
Operation for each axis without servo amplifier connection as the normal operation mode can be executed during amplifier-less operation mode. The start method of positioning control is also the same procedure of normal operation mode.
The normal operation (with servo amplifier connection) is possible by switching from the amplifier-less operation mode to the normal operation mode after amplifier-less operation.
The current value management (command position value, machine feed value) at the switching the normal operation mode and amplifier-less operation mode is shown below.

| Setting of "Absolute position detection system (PA03)"*1 | Current value management at the operation mode switching: Normal operation mode → Amplifier-less operation mode | Current value management at the operation mode switching: Amplifier-less operation mode → Normal operation mode |
|---|---|---|
| "0: Disabled (used in incremental system)" | The command position value and machine feed value are "0". | The command position value and machine feed value are "0". (At the communication start to the servo amplifiers) |
| "1: Enabled (used in absolute position detection system)" | The amplifier-less operation mode starts with the address that the servo amplifier's power supply was finally turned OFF.<br>However, the home position is not established in the normal operation mode, the command position value and machine feed value are "0". | The command position value and machine feed value are restored according to the actual position of servo motor. (At the communication start to the servo amplifiers)<br>However, when the home position is not established in the normal operation mode before switching to the amplifier-less operation mode, the command position value and machine feed value are not restored. Execute the home position return.<br>When the mode is switched to the normal operation mode after moving that exceeds the range "-2147483648(-2^31) to 2147483647(2^31-1) [pulse]" from the actual position of servo motor during amplifier-less operation mode, the command position value and machine feed value might be not restored correctly. |

*In the original, "Current value management at the operation mode switching" is a two-level header over the last two columns.

*1 For MR-J4(W)-B. "Absolute position detection system selection (PA03.0)" for MR-J5(W)-B.

##### Point for control details (制御内容のPoint) (8.7 / original p.342)

- Switch of the normal operation mode and amplifier-less operation mode is executed by the batch of all axes. Switch of the operation mode for each axis cannot be executed.
- Only axis that operated either of the following before switching to the amplifier-less operation mode becomes the connection status during amplifier-less operation.
  - "[Pr.100] Servo series" is set, and then the written to flash ROM is executed. (Turn the power supply ON or reset the CPU module after written to flash ROM.)
  - "[Pr.100] Servo series" is set, and then the "[Cd.190] PLC READY" is turned ON. (Servo amplifier connection is unnecessary.)
- Suppose the following servo amplifier and servo motor are connected during amplifier-less operation mode.

| [Pr.97] SSCNET setting | [Pr.100] Servo series | Servo amplifier type | Motor type |
|---|---|---|---|
| 1: SSCNETⅢ/H | 128: MR-J5-_B_(-RJ), MR-J5W_-_B (2-axis type, 3-axis type) | MR-J5-10B | Rotary servo motor (Resolution per servo motor rotation: 4194304 pulses/rev) |
| 1: SSCNETⅢ/H | Other than "128: MR-J5-_B_(-RJ), MR-J5W_-_B (2-axis type, 3-axis type)" | MR-J4-10B | HG-KR053 (Resolution per servo motor rotation: 4194304 pulses/rev) |
| 0: SSCNETⅢ | — | MR-J3-10B | HF-KP053 (Resolution per servo motor rotation: 262144 pulses/rev) |

*In the original, "1: SSCNETⅢ/H" is merged over 2 rows. Expanded to each row.

#### Restrictions (制約事項) (8.7 / original p.343-344)

- Some monitor data differ from the actual servo amplifier during amplifier-less operation mode.

n: Axis No. - 1

| Storage item | | Storage details | Buffer memory address |
|---|---|---|---|
| [Md.102] | Deviation counter value | Always "0". | 2452+100n<br>2453+100n |
| [Md.106] | Servo amplifier software No. | Always "0". | 2464+100n<br>⋮<br>2469+100n |
| [Md.107] | Parameter error No. | Always "0". | 2470+100n |
| [Md.108] | Servo status1 | • READY ON(b0), Servo ON(b1): Changed depending on the "[Cd.191] All axis servo ON" and "[Cd.100] Servo OFF command".<br>• Control mode (b2, b3): Indicates control mode.<br>• Gain switching (b4): Always OFF<br>• Fully closed control switching (b5): Always OFF<br>• Servo alarm (b7): Always OFF<br>• In-position (b12): Always ON<br>• Torque limit (b13): Changed depending on "[Md.104] Motor current value". (Refer to the 2nd and 3rd bullets of restrictions for details.)<br>• Absolute position lost (b14): Always OFF<br>• Servo warning (b15): Always OFF | 2477+100n |
| [Md.109] | Regenerative load ratio/Optional data monitor output 1 | Always "0". | 2478+100n |
| [Md.110] | Effective load torque/Optional data monitor output 2 | Always "0". | 2479+100n |
| [Md.111] | Peak torque ratio/Optional data monitor output 3 | Always "0". | 2480+100n |
| [Md.112] | Optional data monitor output 4 | Always "0". | 2481+100n |
| [Md.119] | Servo status2 | • Zero point pass (b0): Always ON<br>• Zero speed (b3): Changed depending on the command speed<br>• Speed limit (b4): Always ON when the value other than "0" is set to the command torque at torque control mode. Otherwise, always OFF.<br>• PID control (b8): Always OFF | 2476+100n |

- The operation of following function differs from the normal operation mode during amplifier-less operation mode.

| Function | Operation |
|---|---|
| External signal selection function | When "1: Servo amplifier" is set in "[Pr.116] FLS signal selection", "[Pr.117] RLS signal selection", and "[Pr.118] DOG signal selection", the status of external signal at the amplifier-less operation mode start is shown below.<br>• Upper/lower limit signal (FLS, RLS): ON<br>• Proximity dog signal (DOG): OFF<br>Change "[Md.30] External input signal" to change the signal status. (Refer to the 3rd bullet of restrictions for details.)<br>When "2: Buffer memory" is set in "[Pr.116] FLS signal selection", "[Pr.117] RLS signal selection", and "[Pr.118] DOG signal selection", the upper/lower limit signal (FLS, RLS) and proximity dog signal (DOG) follow the buffer memory status of Simple Motion module during amplifier-less operation mode. |
| Torque limit function | Turns ON/OFF torque limit ([Md.108] Servo status1: b13) depending on "[Md.104] Motor current value". (Refer to the 3rd bullet of restrictions for details.) |

- The operation of following monitor data differs from the normal operation mode during amplifier-less operation mode.

n: Axis No. - 1

| Storage item | | Storage details | Buffer memory address |
|---|---|---|---|
| [Md.30] | External input signal | When "1: Servo amplifier" is set in "[Pr.116] FLS signal selection", "[Pr.117] RLS signal selection", and "[Pr.118] DOG signal selection", the external input signal status can be operated by turning ON/OFF the "b0: Lower limit signal", "b1: Upper limit signal" or "b6: Proximity dog signal" during amplifier-less operation mode. | 2416+100n |
| [Md.104] | Motor current value | "0" is set at the amplifier-less operation mode start.<br>The motor current value can be emulated by changing this monitor data in user side during amplifier-less operation mode. | 2456+100n |

(original p.344)
- When the power supply is turned OFF → ON or CPU module is reset during amplifier-less operation mode, the mode is switched to the normal operation mode.
- The operation of servo motor or the timing of operation cycle, etc. at the amplifier-less operation is different from the case where the servo amplifiers are connected at the normal operation mode. Confirm the operation finally with a real machine.
- The amplifier-less operation cannot be used in the fully closed loop system, linear servo motor or direct drive motor.
- Even if the "[Cd.190] PLC READY" is turned ON by changing "[Pr.100] Servo series" from "0: Servo series is not set" to other than "0", the setting does not become valid. (The axis connecting status remains disconnection.)
- The operation cannot be changed to amplifier-less operation when connected and not connected servo amplifier axes are mixed. Change to amplifier-less operation when all axes are connected, or disconnect all axes of the servo amplifier.
- The synchronous encoder via servo amplifier cannot be used during amplifier-less operation mode.

#### Data list (データ一覧) (8.7 / original p.344)

The data used in the amplifier-less operation function is shown below.
- System control data

| Setting item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.137] | Amplifier-less operation mode switching request | → | Switch operation mode.<br>ABCDH: Switch from the normal operation mode to the amplifier-less operation mode.<br>0000H: Switch from the amplifier-less operation mode to the normal operation mode | 5926 |

- System monitor data

| Monitor item | | Monitor value | Storage details | Buffer memory address |
|---|---|---|---|---|
| [Md.51] | Amplifier-less operation mode status | → | Indicate the current operation mode.<br>0: Normal operation mode<br>1: Amplifier-less operation mode | 4232 |

#### Operation mode switching procedure (運転モード切換え手順) (8.7 / original p.344-345)

- Switch from the normal operation mode to the amplifier-less operation mode
  1. Stop all operating axes, and then confirm that the "[Md.141] BUSY" for all axes turned OFF.
  2. Turn OFF the "[Cd.190] PLC READY".
  3. Confirm that the READY signal ([Md.140] Module status: b0) turned OFF.
  4. Set "ABCDH" in "[Cd.137] Amplifier-less operation mode switching request".
  5. Confirm that "1: Amplifier-less operation mode" was set in "[Md.51] Amplifier-less operation mode status".
- Switch from the amplifier-less operation mode to the normal operation mode
  1. Stop all operating axes, and then confirm that the "[Md.141] BUSY" for all axes turned OFF.
  2. Turn OFF the "[Cd.190] PLC READY".
  3. Confirm that the READY signal ([Md.140] Module status: b0) turned OFF.
  4. Set "0000H" in "[Cd.137] Amplifier-less operation mode switching request".
  5. Confirm that "0: Normal operation mode" was set in "[Md.51] Amplifier-less operation mode status".

##### Operation example (動作例) (8.7 / original p.345)

The following drawing shows the operation for the switching of the normal operation mode and amplifier-less operation mode

[Figure] Switching between normal operation mode and amplifier-less operation mode (original p.345)
- Signals (top to bottom): Each operation (V-t), [Md.141] BUSY, [Cd.190] PLC READY, READY signal ([Md.140] Module status: b0), [Cd.137] Amplifier-less operation mode switching request, [Md.51] Amplifier-less operation mode status.
- Period 1 "Normal operation mode": the operation decelerates to stop → [Md.141] BUSY turns OFF → [Cd.190] PLC READY turns OFF → following it, the READY signal (b0) turns OFF.
- [Cd.137] changes 0000H → ABCDH; following it, [Md.51] changes 0 → 1 and the "Amplifier-less operation mode" period starts.
- In the amplifier-less operation mode: [Cd.190] PLC READY turns ON → following it, the READY signal (b0) turns ON; the operation (acceleration, constant speed, deceleration) is executed with [Md.141] BUSY ON during it; then BUSY turns OFF.
- [Cd.190] PLC READY turns OFF → the READY signal (b0) turns OFF → [Cd.137] changes ABCDH → 0000H; following it, [Md.51] changes 1 → 0 and the "Normal operation mode" period starts.
- In the normal operation mode: [Cd.190] PLC READY turns ON → the READY signal (b0) turns ON; then an operation starts with [Md.141] BUSY ON.

##### Point for operation mode switching procedure (運転モード切換え手順のPoint) (8.7 / original p.345)

- Switch the "normal operation mode" and "amplifier-less operation mode" after confirming the all input signals except synchronization flag OFF. When switching the normal operation mode and amplifier-less operation mode in the status that any one of input signals except the synchronization flag is ON, the error "Error when switching from normal operation mode to amplifier-less operation mode" (error code: 18B0H) or "Error when switching from amplifier-less operation mode to normal operation mode" (error code: 18B1H) will occur, and the switching of operation mode will not execute.
- When the operation mode is switched with the servo amplifiers connected, the communication to the servo amplifiers is shown below.
  - At switching from normal operation mode to amplifier-less operation mode: The communication for all axes during connection is disconnected. (The servo amplifier LED indicates "AA".)
  - At switching from amplifier-less operation mode to normal operation mode: The communication to the servo amplifiers during connection is started.
- Even if the servo amplifiers are not connected, the switching of operation mode is possible.
- The forced stop is invalid regardless of the setting in "[Pr.82] Forced stop valid/invalid selection" during the amplifier-less operation mode.
- Only "0000H" and "ABCDH" are valid for the "[Cd.137] Amplifier-less operation mode switching request". The switching to amplifier-less operation mode can be accepted only when "[Cd.137] Amplifier-less operation mode switching request" is switched from "0000H" to "ABCDH". The switching to normal operation mode can be accepted only when "[Cd.137] Amplifier-less operation mode switching request" is switched from "ABCDH" to "0000H".

## 8.8 Virtual Servo Amplifier Function (仮想サーボアンプ機能) (8.8 / original p.346-351)

This function executes the operation virtually without connecting servo amplifiers (regarded as connected). The synchronous control with virtually input command is possible by using the virtual servo amplifier axis as servo input axis of synchronous control. Also, it can be used as simulation operation for axes without servo amplifiers.

### Virtual servo amplifier function [FX5-SSC-S] (仮想サーボアンプ機能[FX5-SSC-S]) (8.8 / original p.346-348)

#### Control details (制御内容) (8.8 / original p.346)

- When "4097, 4128, 4224" is set in "[Pr.100] Servo series" set in the flash ROM, it operates as virtual servo amplifier immediately after power supply ON.
- When "0" is set in "[Pr.100] Servo series" set in the flash ROM, it operates as virtual servo amplifier by setting "4097, 4128, 4224" in "[Pr.100] Servo series" of buffer memory and by turning the "[Cd.190] PLC READY" OFF to ON after power supply ON.
- Do not connect the actual servo amplifier to axis set as virtual servo amplifier. If MR-J4(W)-B is connected, the LED display status remains "Ab" and the servo amplifier is not recognized. When MR-J5(W)-B is connected, the servo alarm "Connection mode error 1" (alarm No.: 3E.9) occurs and the servo amplifier is not recognized. If the power of MR-J5(W)-B is reset after the servo alarm occurs, the LED display status remains "Ab" and the servo amplifier is not recognized. The following servo amplifiers cannot be connected up to the end station.
  (Note: In the original, no list follows this sentence; kept as printed.)
- The command position value and machine feed value of virtual servo amplifier are as follows.
  - When the absolute position detection system is invalid, both the command position value and machine feed value are set to "0".
  - When the absolute position detection system is valid, the address at the latest power supply OFF is set if the home position has been established. If the home position has not been established, the both of command position value and machine feed value are set to "0".
- When the virtual servo amplifier is set in the system setting of the engineering tool, "0: Disabled (used in incremental system)" is set in "Absolute position detection system (PA03)"*1. Set "1: Enabled (used in absolute position detection system)" to the buffer memory to use as absolute position system.

*1 For MR-J4(W)-B. "Absolute position detection system selection (PA03.0)" for MR-J5(W)-B.

> **Point**
> Do not make to operate by switching between the actual servo amplifier and virtual servo amplifier. When a value except "0" is set in "[Pr.100] Servo series" set in the flash ROM, the connected device is not changed even if the "[Pr.100] Servo series" of buffer memory is changed after power supply ON and then the "[Cd.190] PLC READY" is turned OFF to ON. To change the connected device, write to the flash ROM and turn the power ON again or reset the CPU module.

#### Restrictions (制約事項) (8.8 / original p.347)

- The following monitor data of virtual servo amplifier differ from the actual servo amplifier.

n: Axis No. - 1

| Storage item | | Storage details | Buffer memory address |
|---|---|---|---|
| [Md.102] | Deviation counter value | Always "0". | 2452+100n<br>2453+100n |
| [Md.106] | Servo amplifier software No. | Always "0". | 2464+100n<br>⋮<br>2469+100n |
| [Md.107] | Parameter error No. | Always "0". | 2470+100n |
| [Md.108] | Servo status1 | • READY ON (b0), Servo ON (b1): Changed depending on the "[Cd.191] All axis servo ON" and "[Cd.100] Servo OFF command"<br>• Control mode (b2, b3): Indicates control mode.<br>• Gain switching (b4): Always OFF<br>• Fully closed control switching (b5): Always OFF<br>• Servo alarm (b7): Always OFF<br>• In-position (b12): Always ON<br>• Torque limit (b13): Changed depending on "[Md.104] Motor current value". (Refer to the 2nd and 3rd bullets of restrictions for details.)<br>• Absolute position lost (b14): Always OFF<br>• Servo warning (b15): Always OFF | 2477+100n |
| [Md.109] | Regenerative load ratio/Optional data monitor output 1 | Always "0". | 2478+100n |
| [Md.110] | Effective load torque/Optional data monitor output 2 | Always "0". | 2479+100n |
| [Md.111] | Peak torque ratio/Optional data monitor output 3 | Always "0". | 2480+100n |
| [Md.112] | Optional data monitor output 4 | Always "0". | 2481+100n |
| [Md.119] | Servo status2 | • Zero point pass (b0): Always ON<br>• Zero speed (b3): Changed depending on the command speed<br>• Speed limit (b4): Always ON when the value other than "0" is set to the command torque at torque control mode. Otherwise, always OFF.<br>• PID control (b8): Always OFF | 2476+100n |

- The operation of the following function of virtual servo amplifier differs from the actual servo amplifier.

| Function | Operation |
|---|---|
| External signal selection function | When "1: Servo amplifier" is set in "[Pr.116] FLS signal selection", "[Pr.117] RLS signal selection", and "[Pr.118] DOG signal selection", the external signal status immediately after the power supply ON is shown below.<br>• Upper/lower limit signal (FLS, RLS): ON<br>• Proximity dog signal (DOG): OFF<br>Change the signal status in "[Md.30] External input signal". (Refer to the 3rd bullet of restrictions for details.)<br>When "2: Buffer memory" is set in "[Pr.116] FLS signal selection", "[Pr.117] RLS signal selection", and "[Pr.118] DOG signal selection", the upper/lower limit signal (FLS, RLS) and proximity dog signal (DOG) follow the buffer memory status of the Simple Motion module even with a virtual servo amplifier. |
| Torque limit function | Turns ON/OFF torque limit ([Md.108] Servo status1: b13) depending on "[Md.104] Motor current value". (Refer to the 3rd bullet of restrictions for details.) |

- The following monitor data of virtual servo amplifier differ from the actual servo amplifiers. The writing operation is possible in the virtual servo amplifier.

n: Axis No. - 1

| Storage item | | Storage details | Buffer memory address |
|---|---|---|---|
| [Md.30] | External input signal | When "1: Servo amplifier" is set in "[Pr.116] FLS signal selection", "[Pr.117] RLS signal selection", and "[Pr.118] DOG signal selection", the external input signal status can be operated by turning ON/OFF the following signals.<br>• b0: Lower limit signal<br>• b1: Upper limit signal<br>• b6: Proximity dog signal | 2416+100n |
| [Md.104] | Motor current value | "0" is set after immediately power supply ON.<br>The motor current value can be emulated by changing this monitor data in user side. | 2456+100n |

#### Setting method (設定方法) (8.8 / original p.348)

Set "[Pr.100] Connected device" as follows based on the value in "[Pr.97] SSCNET setting".

| Setting value of "[Pr.97] SSCNET setting" | Setting value of "[Pr.100] Servo series" |
|---|---|
| 0: SSCNETⅢ | 4097: Virtual servo amplifier (MR-J3) |
| 1: SSCNETⅢ/H | 4128: Virtual servo amplifier (MR-J4)<br>4224: Virtual servo amplifier (MR-J5) |

(Note: The sentence says "[Pr.100] Connected device" while the table header says "[Pr.100] Servo series"; both as printed.)

### Virtual servo amplifier function [FX5-SSC-G] (仮想サーボアンプ機能[FX5-SSC-G]) (8.8 / original p.349-351)

#### Control details (制御内容) (8.8 / original p.349)

- The servo amplifier is operated as a virtual servo amplifier when the value of "[Pr.101] Virtual servo amplifier setting" is "1: Use for the virtual servo amplifier" immediately after power cycling.
- When the value of "[Pr.101] Virtual servo amplifier setting" is other than "1: Use for the virtual servo amplifier" immediately after power cycling, the servo amplifier is not operated as a virtual servo amplifier even if "[Pr.101] Virtual servo amplifier setting" in the buffer memory is set to "1: Use for the virtual servo amplifier" and "[Cd.190] PLC READY" is turned OFF → ON after power cycling.
- Virtual servo amplifiers are connected with the absolute position detection system enabled. The command position value and machine feed value are as follows.
  - When the servo amplifier is turned on for the first time as a virtual servo amplifier, the warning "Homing data incorrect" (warning code: 0D3CH) occurs, the home position return request turns ON, and the command position value and feed machine value both become "0". Following this, establishing the home position and then turning the power OFF → ON causes the address to become the address from the last time that the module power was disconnected.

#### Restrictions (制約事項) (8.8 / original p.349-351)

- The following monitor data of virtual servo amplifier differ from the actual servo amplifier.

n: Axis No. - 1

| Storage item | | Storage details | Buffer memory address |
|---|---|---|---|
| [Md.30] | External input signal | When "1: Servo amplifier" is set in "[Pr.116] FLS signal selection", "[Pr.117] RLS signal selection", and "[Pr.118] DOG signal selection":<br>• Lower limit signal (b0): Always ON<br>• Upper limit signal (b1): Always ON<br>• Proximity dog signal (b6): Always OFF | 2416+100n |
| [Md.102] | Deviation counter value | Always "0". | 2452+100n<br>2453+100n |
| [Md.104] | Motor current value | Outputs the command torque during torque control and continuous operation to torque control mode. | 2456+100n |
| [Md.108] | Servo status1 | • READY ON (b0), Servo ON (b1): Changed depending on the "[Cd.191] All axis servo ON" and "[Cd.100] Servo OFF command"<br>• Control mode (b2, b3): Indicates control mode.<br>• Gain switching (b4): Always OFF<br>• Fully closed control switching (b5): Always OFF<br>• Servo alarm (b7): Always OFF<br>• In-position (b12): Always ON during Servo ON, always OFF during Servo OFF<br>• Torque limit (b13): Changed depending on the command torque value<br>• Absolute position lost (b14): Turns ON when the connected device is not MR-J5-G at establishment of the home position when connected to a virtual servo amplifier axis, and turns OFF when home position return is performed.<br>• Servo warning (b15): Always OFF | 2477+100n |
| [Md.109] | Regenerative load ratio/Optional data monitor output 1 | Always "0". | 2478+100n |
| [Md.110] | Effective load torque/Optional data monitor output 2 | Always "0". | 2479+100n |
| [Md.111] | Peak torque ratio/Optional data monitor output 3 | Always "0". | 2480+100n |
| [Md.112] | Optional data monitor output 4 | Always "0". | 2481+100n |
| [Md.119] | Servo status2 | • Zero point pass (b0): Always ON<br>• Zero speed (b3): Changed depending on the command speed<br>• Speed limit (b4): Turns ON when the speed exceeds the limit value at torque control mode.<br>• PID control (b8): Always OFF | 2476+100n |
| [Md.514] | HPR operating status | Changed depending on the HPR (home position return) status | 2457+100n |

- The operation of the following function of virtual servo amplifier differs from the actual servo amplifier. (original p.350)

| Function | Operation |
|---|---|
| External signal selection function | When "1: Servo amplifier" is set in "[Pr.116] FLS signal selection", "[Pr.117] RLS signal selection", and "[Pr.118] DOG signal selection", this function cannot be used to emulate the upper/lower limit signal (FLS, RLS) and proximity dog signal (DOG).<br>When "2: Buffer memory" is set in "[Pr.116] FLS signal selection", "[Pr.117] RLS signal selection", and "[Pr.118] DOG signal selection", the upper/lower limit signal (FLS, RLS) and proximity dog signal (DOG) follow the buffer memory status of the Motion module even with a virtual servo amplifier. |
| External command function selection | This function cannot be used to emulate "[Pr.95] External command signal selection". |
| Torque limit function | Turns ON/OFF torque limit ("[Md.108] Servo status1": b13) depending on the command torque value. |

- When a device is connected to an axis or station that is operating as a virtual servo amplifier, the relevant device is connected to the CC-Link IE TSN network, but does not enter the in synchronous communication status.
- An axis being operated as a virtual servo amplifier emulate the following servo amplifier types.
  - Servo amplifier type: MR-J5-G

The specification of the emulated MR-J5(W)-G is as follows.

| Function | | Support | Description |
|---|---|---|---|
| Reception check | WDC check | × | Check of reception WDC (the master station → the device station) is not carried out. |
| PDO-related | Emulation of feedback | ○ | Simulates feedback of MR-J5(W)-G. |
| PDO-related | Variable mapping | × | When the emulate function is valid, the default mapping of MR-J5(W)-G is used.<br>For the default mapping, refer to MR-J5(W)-G manuals.<br>The following functions cannot be used with the virtual servo amplifier function.<br>• External input signal<br>• Synchronous encoder via servo amplifier<br>• Optional data monitor |
| SLMP-related | Response data simulation | × | SLMP communication simulation is not supported. |
| Servo alarm-related | (merged) | × | Servo alarms cannot be detected. |
| Motor type | Standard rotary type | ○ | Operates as a rotary servo motor (resolution: 4194304).<br>A speed unit of the servo amplifier is fixed to 0.01 r/min. |
| Operation mode | csp | ○ | Position control operation by csp is available. |
| Operation mode | csv | ○ | Velocity control operation by csv is available. |
| Operation mode | cst | ○ | Torque control operation by cst is available. |
| Operation mode | hm | ○ | Homing by hm is available. The homing method supports the driver homing method (data set method) only. |
| Operation mode | ct | ○ | Continuous operation to torque control by ct is available. (The operation is the same as cst.) |
| External signal-related | FLS | ○ | • Only input via the controller is available.<br>Stop operation of the device station when the FLS is OFF is not simulated. The command from the master station stops by FLS detection, following which the servo motor stops as well.<br>• In the case of input via the servo amplifier, the input value is always OFF. |
| External signal-related | RLS | ○ | • Only input via the controller is available.<br>Stop operation of the device station when the RLS is OFF is not simulated. The command from the master station stops by RLS detection, following which the servo motor stops as well.<br>• In the case of input via the servo amplifier, the input value is always OFF. |

*In the original, "PDO-related" is merged over 2 rows, "Operation mode" over 5 rows and "External signal-related" over 2 rows. "Servo alarm-related" is one cell merged over the two "Function" columns. Expanded to each row. ○: supported, ×: not supported.

[Servo parameter specification] (original p.351)

| No. | Servo parameter | Description |
|---|---|---|
| PA03.0 | Absolute position detection system selection | Fixed to "1: Enabled (absolute position detection system)" |
| PA14 | Travel direction selection | Fixed to "0". |
| PC07 | Zero speed | 50 r/min |
| PC29 | Function selection C-B | 1000H<br>X_ _ _: Torque POL reflection selection<br>1: Disabled |
| PC76 | Function selection C-E | 0011H<br>_ _ X _: ZSP disabled selection at control switching<br>1: Disabled (control switching is performed regardless of the range of ZSP) |
| PT07 | Home position shift distance | 0 |
| PT45 | Homing method | 37 (data set type) |

#### Setting method (設定方法) (8.8 / original p.351)

Set "[Pr.101] Virtual servo amplifier setting" as follows.

n: Axis No. - 1

| Storage item | | Storage details | Buffer memory address |
|---|---|---|---|
| [Pr.101] | Virtual servo amplifier setting | Sets whether or not to use the axis as a virtual servo amplifier axis. The value is imported when the power is turned ON.<br>0: Use for the actual servo amplifier<br>1: Use for the virtual servo amplifier*1 | 58022+32n |

*1 When set to a value other than "1: Use for the virtual servo amplifier", the axis is used as an actual axis.

## 8.9 Driver Communication Function [FX5-SSC-S] (ドライバ間通信機能[FX5-SSC-S]) (8.9 / original p.352-356)

This function uses the "Master-slave operation function" of servo amplifier. The Simple Motion module controls master axis and the slave axis is controlled by data communication between servo amplifiers (driver communication) without Simple Motion module.
There are restrictions in the function that can be used by the version of servo amplifier. Refer to the manuals of each servo amplifier for details.
The following shows the number of settable axes for the master axis and slave axis.

| Network | Servo amplifier | Module | Combination of number of settable axes*1: Master axis | Combination of number of settable axes*1: Slave axis | Remark |
|---|---|---|---|---|---|
| SSCNETⅢ | MR-J3-_B_<br>MR-J3-_BS_ | FX5-40SSC-S | 1 axis to 2 axes | 1 axis or more per master axis | The axes other than the master axis and slave axis can be used as normal axis. |
| SSCNETⅢ | MR-J3-_B_<br>MR-J3-_BS_ | FX5-80SSC-S | 1 axis to 4 axes | 1 axis or more per master axis | The axes other than the master axis and slave axis can be used as normal axis. |
| SSCNETⅢ/H | MR-J4(W)-B<br>MR-J5(W)-B*2*3 | FX5-40SSC-S | 1 axis to 2 axes | 1 axis or more per master axis | The axes other than the master axis and slave axis can be used as normal axis. |
| SSCNETⅢ/H | MR-J4(W)-B<br>MR-J5(W)-B*2*3 | FX5-80SSC-S | 1 axis to 4 axes | 1 axis or more per master axis | The axes other than the master axis and slave axis can be used as normal axis. |

*In the original, "Network" and "Servo amplifier" are each merged over 2 rows per network; "Slave axis" and "Remark" are merged over all 4 rows. Expanded to each row.

*1 When the slave axis is not allocated for the master axis, only the master axis operates independently.
*2 In the fully closed loop system, the servo amplifier can be set for the master axis only. It cannot be set for the slave axis. Also, it cannot be used with the linear servo motors and direct drive motors. Refer to the manuals of each servo amplifier for details.
*3 When using MR-J5-_B_/MR-J5-_B_-RJ, set all the master and slave axes to be used in combination to MR-J5-_B_/MR-J5-_B_-RJ. If MR-J4-_B_/MR-J4-_B_-RJ is included, the error "Master axis amplifier type error" (error code: 1C96H) will occur.

#### Control details (制御内容) (8.9 / original p.352-353)

Set the master axis and slave axis in the servo parameter.
Execute each control of Simple Motion module for the master axis. (However, be sure to execute the servo ON/OFF of slave axis and error reset at servo alarm occurrence in the slave axis.)
The servo amplifier set as master axis receives command (positioning command, speed command, torque command) from the Simple Motion module, and send the control data to the servo amplifier set as slave axis by driver communication between servo amplifiers.
The servo amplifier set as the slave axis is controlled with the control data transmitted from master axis by driver communication between servo amplifiers.

[Figure] Driver communication configuration (original p.352)
- Simple Motion module — SSCNETⅢ(/H) — Master axis (d1, Axis 1 ABS/INC) — Slave axis 1 (d2, Axis 2 INC) — Slave axis 2 (d3, Axis 3 INC) — Slave axis 3 (d4, Axis 4 INC).
- Master axis: Position command, speed command or torque command is received from Simple Motion module. ("Positioning command/speed command/torque command" arrow into the master axis.)
- Slave axis: Control data is received from Master axis by driver communication.
- [Driver communication] from Master axis: Control data 1, Control data 2, Control data 3 → Slave axis 1; from Slave axis 1: Control data 2, Control data 3 → Slave axis 2; from Slave axis 2: Control data 3 → Slave axis 3.

> **Point** (original p.353)
> - When the communication is disconnected due to a fault in the servo amplifier, it is not possible to communicate with the axis after the faulty axis. Therefore, when connecting the SSCNETⅢ cable, connect the master axis in the closest position to the Simple Motion module.
> - This function is used for the case to operate by multiple motors in one system. Connect the master axis and slave axis without slip.

#### Precautions during control (制御上の注意事項) (8.9 / original p.353-354)

> **CAUTION**
> - In the operation by driver communication, the positioning control or JOG operation of the master axis is not interrupted even if the servo alarm occurs in the slave axis. Be sure to stop by user program.

##### Servo amplifier (サーボアンプ) (8.9 / original p.353)

- Use the servo amplifiers compatible with the driver communication for the axis to execute the driver communication.
- The combination of the master axis and slave axis is set in the servo parameters. The setting is valid by turning ON or resetting the system's power supply after writing the servo parameters to the Simple Motion module.
- Check the operation enabled status of driver communication in "[Md.52] Communication between amplifiers axes searching flag". The operation cannot be changed to amplifier-less operation when connected and not connected servo amplifier axes are mixed. Change to amplifier-less operation when all axes are connected, or disconnect all axes of the servo amplifier.
- When connecting/disconnecting at driver communication function use, it can be executed only for the head axis (servo amplifier connected directly to the Simple Motion module). The servo amplifier other than the head axis can be disconnected, however it cannot be connected again.
- Differences between SSCNETⅢ connection and SSCNETⅢ/H connection in driver communication function are shown below.

| Item | SSCNETⅢ | SSCNETⅢ/H |
|---|---|---|
| Communication with the servo amplifiers after controller's power supply ON | The servo amplifiers cannot be operated until the connection with all system setting axes is confirmed. | The servo amplifiers cannot be operated until the connection with all driver communication setting axes is confirmed. The normal operation axis (driver communication unset up axis) can be connected after the network is established. |
| Connect/disconnect with servo amplifier | Only the first axis (servo amplifier connected directly to the Simple Motion module) can connect/disconnect.<br>Servo amplifiers other than the first axis can be disconnected but cannot be connected. | Only the first axis (servo amplifier connected directly to the Simple Motion module) can connect/disconnect.<br>Only normal axes (axes not set to driver communication) other than the first axis can be connected when they are disconnected. However, when axes set to driver communication are disconnected, they cannot communicate with servo amplifiers that were connected after disconnecting. (The servo amplifier's LED display remains "AA".) |

- If all axes set to driver communication are not detected at the start of communication with the servo amplifier, all axes including independent axes cannot be operated. (The servo amplifier's LED display remains "Ab".) Check the operation enabled status with "[Md.52] Communication between amplifiers axes searching flag". When all independent axes and axes set to driver communication are connected, "0: Search end" is set in "[Md.52] Communication between amplifiers axes searching flag".

| Monitor item | | Monitor value | Storage details | Buffer memory address |
|---|---|---|---|---|
| [Md.52] | Communication between amplifiers axes searching flag | → | The detection status of axis that set communication between amplifiers is stored.<br>0: Search end<br>1: Searching | 4234 |

(Note: The 3rd bullet above, "The operation cannot be changed to amplifier-less operation ...", is printed as in the original.)

##### Home position return control, positioning control, manual control, expansion control, and synchronous control (原点復帰制御，位置決め制御，手動制御，拡張制御，同期制御) (8.9 / original p.354)

- Do not start the slave axis. The command to servo amplifier is invalid even if the slave axis is started.
- The home position return request flag ([Md.31] Status: b3) of slave axis is always ON. There is no influence for control of slave axis.
- There are some restrictions for data used as the positioning control of slave axis. The external input signals such as FLS or RLS, and the parameters such as software stroke limit are invalid. Refer to →Page 352 I/O signals of slave axis and →Page 352 Data used for positioning control of slave axis for details.
- For setting the slave axis as a servo input axis, set "2: Actual position value" or "4: Feedback value" in "[Pr.300] Servo input axis type". Otherwise, the slave axis does not operate as an input axis.
- At the driver communication operation, only the switching to positioning control mode, speed control mode, and torque control mode are possible. When the mode is switched to continuous operation to torque control mode for the master axis, the warning "Control mode switching not possible" (warning code: 09EBH) will occur, and the control mode is not switched.

##### Absolute position system (絶対位置システム) (8.9 / original p.354)

Set "0: Disabled (used in incremental system)" in "Absolute position detection system (PA03)"*1 of servo parameter for slave axis. If "1: Enabled (used in absolute position detection system)" is set, the warning "Home position return data incorrect" (warning code: 093CH) will occur and the home position return of slave axis cannot be executed.

*1 For MR-J4(W)-B. "Absolute position detection system selection (PA03.0)" for MR-J5(W)-B.

##### I/O signals of slave axis (スレーブ軸の入出力信号) (8.9 / original p.354)

- Input signal: All signals cannot be used. The error detection signal turns ON "Error detection" ([Md.31] Status: b13).
- Output signal: All signals cannot be used.

##### Data used for positioning control of slave axis (スレーブ軸の位置決め制御に使用するデータ) (8.9 / original p.354)

- Only the following axis monitor data are valid in slave axis.

| Item | | Remark |
|---|---|---|
| [Md.23] | Axis error No. | Valid for only servo alarm detection. |
| [Md.35] | Torque limit stored value/forward torque limit stored value | — |
| [Md.103] | Motor rotation speed | — |
| [Md.104] | Motor current value | — |
| [Md.107] | Parameter error No. | — |
| [Md.108] | Servo status1 | The following bits are valid.<br>• b0: READY ON<br>• b1: Servo ON<br>• b7: Servo alarm<br>The slave axis is always controlled in torque control mode, "control mode (b2, b3)" is set to torque control mode (0, 1). |
| [Md.109] | Regenerative load ratio/Optional data monitor output 1 | — |
| [Md.110] | Effective load torque/Optional data monitor output 2 | — |
| [Md.111] | Peak torque ratio/Optional data monitor output 3 | — |
| [Md.112] | Optional data monitor output 4 | — |
| [Md.114] | Servo alarm | — |
| [Md.119] | Servo status2 | The following bit is valid.<br>• b0: Zero point pass<br>(Execute home position return to the master axis.) |
| [Md.120] | Reverse torque limit stored value | — |

- Only the following axis control data are valid in slave axis.

| Item | | Remark |
|---|---|---|
| [Cd.5] | Axis error reset | Only servo alarm detection |
| [Cd.22] | New torque value/forward new torque value | — |
| [Cd.100] | Servo OFF command | — |
| [Cd.101] | Torque output setting value | — |
| [Cd.112] | Torque change function switching request | — |
| [Cd.113] | New reverse torque value | — |

#### Servo parameter (サーボパラメータ) (8.9 / original p.355-356)

Set the following parameters for the axis to execute the driver communication. (Refer to the manuals of each servo amplifier for details.)

##### MR-J3-_B_/MR-J3-_BS_ used (MR-J3-_B_/MR-J3-_BS_使用時) (8.9 / original p.355)

n: Axis No. - 1

| Setting item | | | Setting details | Buffer memory address |
|---|---|---|---|---|
| Input/output setting | PA04 | Forced stop deceleration function selection | Disable deceleration stop function at the master axis and slave axis.*1 | 28404+100n |
| Input/output setting | PD15 | Driver communication setting | Set the master axis and slave axis. | 65534+340n |
| Input/output setting | PD16 | Driver communication setting<br>Master transmit data selection 1 | Set the transmitted data at master axis setting. | 65535+340n |
| Input/output setting | PD17 | Driver communication setting<br>Master transmit data selection 2 | Set the transmitted data at master axis setting. | 65536+340n |
| Input/output setting | PD20 | Driver communication setting<br>Master axis No. selection 1 for slave | Set the axis No. of master axis at slave axis setting. | 65539+340n |
| Input/output setting | PD30 | Master-slave operation<br>Torque command coefficient on slave | Set the parameter at slave axis setting. | 65549+340n |
| Input/output setting | PD31 | Master-slave operation<br>Speed limit coefficient on slave | Set the parameter at slave axis setting. | 65550+340n |
| Input/output setting | PD32 | Master-slave operation<br>Speed limit adjusted value on slave | Set the parameter at slave axis setting. | 65551+340n |

*In the original, "Input/output setting" is merged over 8 rows; "Set the transmitted data at master axis setting." is merged over PD16/PD17, and "Set the parameter at slave axis setting." over PD30/PD31/PD32. Expanded to each row.

*1 At MR-J3-_B_ use, it is not necessary to change the setting since the initial value is disabled. However, it is required to set disabled since the initial value is enabled at MR-J3-_BS_ use.

When the slave axis is not allocated for the master axis, only the master axis operates independently.

> **Point**
> - The servo parameters are transmitted from Simple Motion module to servo amplifier after power supply ON or reset of the CPU module. Execute flash ROM writing of Simple Motion module after writing the servo parameter to buffer memory, and then turn the power supply ON or reset the CPU module.
> - The servo parameters for driver communication setting (PD15 to PD17, PD20) become valid by turning the servo amplifier's power supply OFF to ON. Turn the servo amplifier's power supply OFF to ON after executing the above shown in the 1st bullet. Then, turn the system's power supply ON again or reset the CPU module.
> - In the driver communication function, the torque generation direction for slave axis can be set in "Rotation direction selection/travel direction selection (PA14)".

##### MR-J4-_B_/MR-J4-_B_-RJ/MR-J5-_B_/MR-J5-_B_-RJ used (MR-J4-_B_/MR-J4-_B_-RJ/MR-J5-_B_/MR-J5-_B_-RJ使用時) (8.9 / original p.356)

n: Axis No. - 1

| Setting item | | | Setting details | Buffer memory address |
|---|---|---|---|---|
| Input/output setting | PA04 | Forced stop deceleration function selection*1 | Disable deceleration stop function at the master axis and slave axis. | 28404+100n |
| Input/output setting | PD15 | Driver communication setting | Set the master axis and slave axis. | 65534+340n |
| Input/output setting | PD16 | Driver communication setting<br>Master transmit data selection 1 | Set the transmitted data at master axis setting. | 65535+340n |
| Input/output setting | PD17 | Driver communication setting<br>Master transmit data selection 2 | Set the transmitted data at master axis setting. | 65536+340n |
| Input/output setting | PD20 | Driver communication setting<br>Master axis No. selection 1 for slave | Set the axis No. of master axis at slave axis setting. | 65539+340n |
| Input/output setting | PD30 | Master-slave operation<br>Torque command coefficient on slave | Set the parameter at slave axis setting. | 65549+340n |
| Input/output setting | PD31 | Master-slave operation<br>Speed limit coefficient on slave | Set the parameter at slave axis setting. | 65550+340n |
| Input/output setting | PD32 | Master-slave operation<br>Speed limit adjusted value on slave | Set the parameter at slave axis setting. | 65551+340n |

*In the original, "Input/output setting" is merged over 8 rows; "Set the transmitted data at master axis setting." is merged over PD16/PD17, and "Set the parameter at slave axis setting." over PD30/PD31/PD32. Expanded to each row.

*1 For MR-J4(W)-B. "Function selection A-1 Forced stop deceleration function selection (PA04.3)" for MR-J5(W)-B.

When the slave axis is not allocated for the master axis, only the master axis operates independently.
At slave setting, set only "Driver communication setting Master axis No. selection 1 for slave (PD20)" in the master axis No. selection normally.
Since the servo parameters of MR-J5(W)-B are not in the buffer memory, use GX Works3 or axis control data to set them. Refer to the following for details.
→Page 845 Connection with MR-J5(W)-B

> **Point**
> - The servo parameters are transmitted from Simple Motion module to servo amplifier after power supply ON or reset of the CPU module. Execute flash ROM writing of Simple Motion module after writing the servo parameter to buffer memory, and then turn the power supply ON or reset the CPU module.
> - The servo parameters for driver communication setting (PA04, PD15 to PD17, PD20) become valid by turning the servo amplifier's power supply OFF to ON. Turn the servo amplifier's power supply OFF to ON after executing the above shown in the 1st bullet. Then, turn the system's power supply ON again or reset the CPU module.
> - In the driver communication function, the torque generation direction for slave axis can be set in "Rotation direction selection/travel direction selection (PA14)"*1.

*1 For MR-J4(W)-B. "Travel direction selection (PA14)" for MR-J5(W)-B.

## 8.10 Mark Detection Function (マーク検出機能) (8.10 / original p.357-372)

Any data can be latched at the input timing of the mark detection signal (DI).
Also, only data within a specific range can be latched by specifying the data detection range.
The following three modes are available for execution of mark detection.

### Continuous detection mode (常時検出モード) (8.10 / original p.357)

The latched data is always stored to the first of mark detection data storage area at mark detection.

[Figure] Continuous detection mode (original p.357)
- Mark detection signal: 5 pulses; at each leading edge (arrow) the latched data is stored.
- Mark detection data storage area: all 5 detections are stored to "Storage area 1" (overwritten each time).

### Specified number of detections mode (指定回数モード) (8.10 / original p.357)

The latched data from a specified number of detections is stored.
The detected position for a specified number of detections can be collected when the mark detection signal is continuously input at high speed.

Ex.
Number of detections: 3

[Figure] Specified number of detections mode (Number of detections: 3) (original p.357)
- Mark detection signal: 5 pulses.
- 1st detection → Storage area 1, 2nd detection → Storage area 2, "The 3rd detection" → Storage area 3 (storage order is downward, shown by an arrow from Storage area 1 toward Storage area 3/4).
- "The 4th detection and later are ignored." (Storage area 4 is not used.)

### Ring buffer mode (リングバッファモード) (8.10 / original p.357)

The latched data is stored in a ring buffer for a specified number of detections.
The latched data is always stored at mark detection.

Ex.
Number of detections: 4

[Figure] Ring buffer mode (Number of detections: 4) (original p.357)
- Mark detection signal: 5 pulses.
- 1st detection → Storage area 1, 2nd → Storage area 2, 3rd → Storage area 3, "The 4th detection" → Storage area 4 (a circular arrow returns from Storage area 4 to Storage area 1).
- "The 5th detection replaces the previous first detection." (the 5th detection is stored to Storage area 1).

> **Point**
> [FX5-SSC-G]
> For the software version 1.004 or later, a link device can be used for the mark detection signal.

### Performance specifications (性能仕様) (8.10 / original p.358-362)

#### Performance specifications [FX5-SSC-S] (性能仕様[FX5-SSC-S]) (8.10 / original p.358)

| Item | FX5-40SSC-S | FX5-80SSC-S |
|---|---|---|
| Number of mark detection settings | Up to 16 | Up to 16 |
| Input signal | Axis 1 to Axis 4 External input signal (DI1 to DI4) | Axis 1 to Axis 8 External input signal (DI1 to DI4) |
| Input signal detection direction | Selectable for leading edge or trailing edge in logic setting of external input signal | Selectable for leading edge or trailing edge in logic setting of external input signal |
| Input signal compensation time | Correctable within the range of -32768 to 32767 μs | Correctable within the range of -32768 to 32767 μs |
| Detection accuracy | 10 μs | 10 μs |
| Latch data | 13 types + Optional buffer memory data (2 words)<br>(Command position value, Machine feed value, Actual position value, Servo input axis position value, Synchronous encoder axis position value, Synchronous encoder axis position value per cycle, Position value after composite main shaft gear, Position value per cycle after main shaft gear, Position value per cycle after auxiliary shaft gear, Cam axis position value per cycle, Cam axis position value per cycle (real position), Command position value of command generation axis, Position value per cycle of command generation axis) | (same as left) |
| Number of continuous latch data storage | Up to 32 | Up to 32 |
| Latched data range | Settable in the range of -2147483648 to 2147483647 | Settable in the range of -2147483648 to 2147483647 |

*In the original, the FX5-40SSC-S / FX5-80SSC-S cells are merged horizontally for every row except "Input signal". Expanded to each column ("(same as left)" is used for the long Latch data cell).

#### Performance specifications [FX5-SSC-G] (性能仕様[FX5-SSC-G]) (8.10 / original p.358)

| Item | FX5-40SSC-G / FX5-80SSC-G |
|---|---|
| Number of mark detection settings | Up to 16 |
| Input signal | External input signal DOG of the servo amplifier, TPR1 (Touch probe1), Link device |
| Input signal detection direction | When using the DOG signal of the servo amplifier: Detection at leading edge/detection at trailing edge are selectable in "b4: External command/switching signal" of "[Pr.22] Input signal logic selection"<br>When using the TPR1 signal of the servo amplifier and link device: Detection at leading edge/detection at trailing edge are selectable in "[Pr.811] Mark detection signal detection direction setting" |
| Input signal compensation time | Correctable within the range of -32768 to 32767 μs |
| Detection accuracy | When using the DOG signal: operation cycle<br>When using the TPR1 signal: high-accuracy<br>When using the link device: operation cycle |
| Latch data | 13 types + Optional buffer memory data (2 words)<br>(Command position value, Machine feed value, Actual position value, Servo input axis position value, Synchronous encoder axis position value, Synchronous encoder axis position value per cycle, Position value after composite main shaft gear, Position value per cycle after main shaft gear, Position value per cycle after auxiliary shaft gear, Cam axis position value per cycle, Cam axis position value per cycle (real position), Command position value of command generation axis, Position value per cycle of command generation axis) |
| Number of continuous latch data storage | Up to 32 |
| Latched data range | Settable in the range of -2147483648 to 2147483647 |

*In the original, the header has separate "FX5-40SSC-G" and "FX5-80SSC-G" columns, and every row's value cell is merged over both columns. Collapsed into one column.

#### Calculation by estimation [FX5-SSC-G] (推定計算[FX5-SSC-G]) (8.10 / original p.359-362)

The mark detection value during operation cycle interval is calculated by estimation. The value calculated by estimation when the mark detection input signal is inputted is stored in the buffer memory as the mark detection data. The value is calculated as shown in the figure below.

- When using the DOG signal of the servo amplifier

The detection timing is the operation cycle.

[Figure] Calculation by estimation when using the DOG signal (original p.359)
- Vertical axis: Mark detection data, with "Data upper limit value" and "Data lower limit value" (dashed); horizontal axis: t.
- Mark detection data is updated stepwise every "Operation cycle"; an "Estimated straight line" is drawn through the steps. At the upper limit value the data wraps to the lower limit value (ring).
- At the leading edge of the "Mark detection input signal", the value on the estimated straight line at that time is the "Mark detection data storage value".

- When using the TPR1 signal of the servo amplifier

High-accurately estimated calculation using signal detection time is performed by using the following signals for touch probe function of MR-J5(W)-G series.
For the signal details and the accuracy of signal detection time, refer to the manual of the servo amplifier.
For MR-J5(W)-G: [Other manual] MR-J5 User's Manual (Function)
[Touch probe status (Obj. 60B9h)]
Bit6: Toggle status for latch completion at the rising edge of touch probe 1
Bit7: Toggle status for latch completion at the falling edge of touch probe 1

[Figure] Calculation by estimation when using the TPR1 signal (original p.359)
- Vertical axis: "Probe data" between "Word data upper limit" and "Word data lower limit"; horizontal axis: t. The data is updated stepwise every "Operation cycle"; "Estimate straight line" drawn through the steps; wraps from the upper limit to the lower limit.
- "Touch probe 1 valid ([Md.125] Servo status3: b11)" turns ON first (before the detection).
- Signal on servo amplifier: "CN3-TPR1" pulses (a first pulse, then a second pulse); at the rising edge of the second pulse, "Toggle status for latch completion at the rising edge of touch probe 1" (on the servo amplifier) changes (toggles).
- The Motion module receives the change later: "Toggle status for latch completion at the rising edge of touch probe 1 ([Md.126] Servo status4: b13)" changes some operation cycles after the TPR1 input.
- "Detection time correction": the time from the TPR1 input to the change of [Md.126] b13 is corrected, and the value on the estimate straight line at the TPR1 input time is stored as "Mark detection data storage value(estimate)".

> **Point** (original p.360)
> - Confirm that TPR1 is assigned to CN3 on the servo parameter of the MR-J5(W)-G series before it is connected.*1
>   And also, in case of using multi-axis servo amplifier, confirm that the axis using TPR1 is selected. If TPR1 is not assigned to CN3, the status is to be touch probe 1 enabled but the signal cannot be detected.
>   For the details of the servo parameter setting, refer to "4.4 Touch probe [G]" in the following manual.
>   For MR-J5(W)-G: [Other manual] MR-J5 User's Manual (Function)
> - There are restrictions to use the touch probe function of the MR-J5(W)-G series on the model and its version. One example of supported version is shown below. For details and the other servo amplifier models not shown below, refer to the manual of the servo amplifier to be used.
>   MR-J5-_G*2: C0 or later and the servo amplifier manufactured in June, 2021 or later*3
>   MR-J5-_G_-RJ*2: B6 or later
>   MR-J5W2-_G/MR-J5W3-_G*4: B6 or later
>   When using TPR1 as the signal, if the servo amplifier that the function is unsupported is connected, the error "PDO mapping setting error" (error code: 1C48H) will occur and the servo amplifier cannot be connected.
> - To detect TPR1 on the Motion module, the touch probe function on the servo amplifier side is needed to be enabled after the connection. Even if operating the cycle for enabling function and the TPR1 input before enabling function, as the signal for mark detection input signal is ignored. Therefore, the Motion module automatically executes enabling by using SLMP after the servo amplifier using TPR1 is connected. If the function cannot be enabled, the warning "Mark detection - Driver touch probe function invalid" (warning: 0D3FH) will occur and the mark detection setting specifying TPR1 of the axis which has error is disabled. Whether the servo amplifier is in touch probe enabled function or not can be checked with the following monitor.
>   "[Md.125] Servo status 3", "b11: Touch probe 1 enabled"
> - About two communication cycles of delay will occur until "[Md.800] Number of mark detection" or "[Md.801] Mark detection data storage area (1 to 32)" is updated from the servo amplifier TPR1 input.
> - The status of TPR1 for the servo amplifier can be checked by one of these methods below.
>   - Specify "Touch probe status" by optional data monitor*5
>   - Check Toggle status for latch completion at the rising/falling edge of touch probe 1 received from the servo amplifier*6
> - If TPR1 is used for the axis that is not set in the axis setting or the axis set as virtual servo amplifier, the warning "Outside mark detection signal setting range" (warning code: 0D36H) will occur and the mark detection will be invalid.

*1 Set the related servo parameter in TPR1. Even if the related parameter is set in TPR2 or later, the Motion module does not detect the signal.
*2 When the single axis is connected to the Motion module, the following CiA402 object will be automatically set to the PDO mapping to use the touch probe function. For the details of the each object, refer to the manual of the servo amplifier.
For MR-J5(W)-G: [Other manual] MR-J5-G/MR-J5W-G User's Manual (Object Dictionary)
- Touch probe status (Obj. 60B9h)
- Touch probe time stamp 1 positive value (Obj. 60D1h)
- Touch probe time stamp 1 negative value (Obj. 60D2h)

*3 For the manufactured date of MR-J5-_G, refer to the following manual.
[Other manual] MR-J5-G/MR-J5W-G User's Manual (Introduction)
*4 When connecting the multi-axis servo amplifier such as MR-J5W_-_G/MR-J5W3-_G, the CiA402 object of the touch probe function is not automatically set in the PDO mapping. When using TPR1 of the multi-axis servo amplifier as the input signal for mark detection, it is necessary to assign TPR1 in CN3 before it is connected and to select if TPR1 is used in axis A, B or C. After that, it can be used by specifying CiA402 object for the touch probe optional data monitor function of the axis selecting TPR1 in the Motion module. However, if Touch probe time stamp 1 positive value (Obj. 60D1h) or Touch probe time stamp 1 negative value (Obj. 60D2h) is not set in the optional data monitor, the detection accuracy is operation cycle.

| Parameter name | Setting value |
|---|---|
| [Pr.91] Optional data monitor: Data type setting 1 | Touch probe status (Obj. 60B9h) |
| [Pr.93] Optional data monitor: Data type setting 3 | When "0: Rising detection" is set in "[Pr.811] Mark detection signal detection direction setting": Touch probe time stamp 1 positive value (Obj. 60D1h)<br>When "1: Falling detection" is set in "[Pr.811] Mark detection signal detection direction setting": Touch probe time stamp 1 negative value (Obj. 60D2h) |
| [Pr.591] Optional data monitor: Data type expansion setting 1 | 0010H |
| [Pr.593] Optional data monitor: Data type expansion setting 3 | 0020H |

*5 When specifying optional data monitor1

| Parameter name | Setting value |
|---|---|
| [Pr.91] Optional data monitor: Data type setting 1 | Touch probe status (Obj. 60B9h) |
| [Pr.591] Optional data monitor: Data type expansion setting 1 | 0010H |

*6 Can be checked by referring to the corresponding bit of "[Md.126] Servo status4".
- b13: Toggle status for latch completion at the rising edge of touch probe 1
- b14: Toggle status for latch completion at the falling edge of touch probe 1

- When using a link device (original p.362)

> **Point**
> The signal response time varies depending on the input response time setting value of the remote I/O.
> Therefore, the signal delay caused by the input response time setting value should be corrected by "[Pr.801] Mark detection signal compensation time".

The detection timing is the operation cycle.

[Figure] Calculation by estimation when using a link device (original p.362)
- Vertical axis: "Probe data" between "Word data upper limit" and "Word data lower limit"; horizontal axis: t. The data is updated stepwise every "Operation cycle"; "Estimate straight line" through the steps; wraps from the upper limit to the lower limit.
- Remote I/O side: "External input X0 (X0 terminal status)" pulses ON briefly; then "Remote input signal RX0" turns ON (at an operation cycle boundary) and stays ON.
- Motion module side: "Link device RX0*1" turns ON later than the remote input signal RX0.
- "Detection time correction": the time between the remote input signal RX0 ON and the link device RX0 ON on the Motion module side is corrected; the value on the estimate straight line at the time the remote input signal RX0 turned ON is stored as "Mark detection data storage value (estimate)".

*1 When using RX0 as the link device.

### Operation for mark detection function (マーク検出機能の動作) (8.10 / original p.363)

Operations done at mark detection are shown below.
- Calculations for the mark detection data are estimated at leading edge/trailing edge of the mark detection signal. However, when the specified number of detections mode is set, the current number of mark detection is checked, and then it is judged whether to execute the mark detection.
- When a mark detection data range is set, it is first confirmed whether the mark detection data is within the range or not. Data outside the range are not detected.
- The mark detection data is stored in the mark detection data storage area according to the mark detection mode, and then the number of mark detection is updated.

#### Continuous detection mode (常時検出モード時) (8.10 / original p.363)

[Figure] Operation in continuous detection mode (original p.363)
- Signals (top to bottom): Mark detection signal (Leading edge detection setting), Mark detection data value, [Md.801] Mark detection data storage area (1 to 32), [Md.800] Number of mark detection, [Pr.42] External command function selection, [Cd.8] External command valid.
- [Pr.42] External command function selection = "4: High speed input request" throughout.
- [Cd.8] External command valid: 0 → 1. "Set "1" before mark detection start."
- [Md.800] Number of mark detection: "**" (previous value) → 0: ""0" clear by setting "1" in "[Cd.800] Number of mark detection clear request"."
- Mark detection data value = "Actual position value (Continuous update)".
- At each leading edge of the mark detection signal, "Confirmation of mark detection data range (Upper/lower limit value setting: Valid)" is performed.
- 1st leading edge (within range): [Md.801] (storage area 1) is updated to "Detected actual position value"; [Md.800] 0 → 1.
- 2nd leading edge (within range): [Md.801] (storage area 1) is updated to the new "Detected actual position value"; [Md.800] 1 → 2.
- 3rd leading edge: "Data outside range are not latched." — [Md.801] and [Md.800] (2) do not change.

#### Specified number of detection mode (Number of detections: 2) (指定回数モード時(指定回数「2」)) (8.10 / original p.363)

[Figure] Operation in specified number of detection mode (Number of detections: 2) (original p.363)
- Signals (top to bottom): Mark detection signal (Leading edge detection setting), Mark detection data value, [Md.801] Mark detection data storage area (1 to 32) (1st area), [Md.801] Mark detection data storage area (1 to 32) (2nd area), [Md.800] Number of mark detection, [Pr.42] External command function selection, [Cd.8] External command valid.
- [Pr.42] = "4: High speed input request"; [Cd.8] 0 → 1 ("Set "1" before mark detection start.").
- [Md.800]: "**" → 0 (""0" clear by setting "1" in "[Cd.800] Number of mark detection clear request".").
- Mark detection data value = "Actual position value (Continuous update)"; "Confirmation of mark detection data range (Upper/lower limit value setting: Valid)" at each leading edge.
- 1st leading edge: 1st area = "Detected actual position value (1st)"; [Md.800] 0 → 1.
- 2nd leading edge: 2nd area = "Detected actual position value (2nd)"; [Md.800] 1 → 2.
- 3rd leading edge: "Mark detection is not executed because the number of mark detections is already 2 (More than the specified number of detections)." — [Md.800] stays 2.

### How to use mark detection function (マーク検出機能の使用方法) (8.10 / original p.364)

The following shows an example for mark detection using the signals shown below.
- External command signal (DI2) of axis 2 [FX5-SSC-S]
- DOG signal of MR-J5(W)-G [FX5-SSC-G]

The mark detection target is axis 1 actual position value, and the all range is detected in continuous detection mode.

1. [FX5-SSC-S]
   Allocate the input signal (DI2) to the external command signal of axis 2, and set the "high speed input request" for mark detection.
   [FX5-SSC-G]
   Allocate the input signal to the external command signal of axis 2, and set the "high speed input request" for mark detection.

n: Axis No. - 1

| Setting item | | Setting value | Setting details/setting value | Buffer memory address |
|---|---|---|---|---|
| [Pr.42] | External command function selection | 4 | Set "4: High speed input request" as the function used in the external command signal of axis 2. | 212 (62+150n) |
| [Pr.95] | External command signal selection | → | Set the following to the external command signal of axis 2.<br>• 2: D12 [FX5-SSC-S]<br>• 102: DOG signal of axis 2 [FX5-SSC-G] | 219 (69+150n) |

*"2: D12" is as printed in the original (presumably "DI2").

2. Set the following mark detection setting parameters. The optional mark detection setting No. can be set.

k: Mark detection setting No. - 1

| Setting item | | Setting value | Setting details/setting value | Buffer memory address |
|---|---|---|---|---|
| [Pr.800] | Mark detection signal setting | 2 | Set "2: Axis 2" to the external input signal for mark detection. | 54000+20k |
| [Pr.801] | Mark detection signal compensation time | 0 | Set "0: (No compensation)" to the compensation time such as delay of sensor. | 54001+20k |
| [Pr.802] | Mark detection data type | 2 | Set "2: Actual position value" to the target data for mark detection. | 54002+20k |
| [Pr.803] | Mark detection data axis No. | 1 | Set "1: Axis 1" to the axis No. of target data for mark detection. | 54003+20k |
| [Pr.805] | Latch data range upper limit value | 0 | Set "0" to the valid upper limit value for latch data at mark detection. (Mark detection for all range is executed by setting the same value as lower limit value.) | 54006+20k<br>54007+20k |
| [Pr.806] | Latch data range lower limit value | 0 | Set "0" to the valid lower limit value for latch data at mark detection. (Mark detection for all range is executed by setting the same value as upper limit value.) | 54008+20k<br>54009+20k |
| [Pr.807] | Mark detection mode setting | 0 | Set "0: Continuous detection mode" to the mark detection mode. | 54010+20k |

3. Turn the power supply OFF or reset of the CPU module to validate the setting parameters.
4. The mark detection starts by setting "1: Validates an external command." in "[Cd.8] External command valid" of axis 2 with the program. Refer to "[Md.800] Number of mark detection" or "[Md.801] Mark detection data storage area (1 to 32)" of the set detection setting No. for the number of mark detections and mark detection data.

### List of parameters and data (パラメータ・データ一覧) (8.10 / original p.365)

The following shows the configuration of parameters and data for mark detection function.

| Buffer memory address | Item | Mark detection setting No. |
|---|---|---|
| 54000 to 54019 | Mark detection setting parameter [Pr.800] to [Pr.811] | Mark detection setting 1 |
| 54020 to 54039 | Mark detection setting parameter [Pr.800] to [Pr.811] | Mark detection setting 2 |
| 54040 to 54059 | Mark detection setting parameter [Pr.800] to [Pr.811] | Mark detection setting 3 |
| ⋮ | Mark detection setting parameter [Pr.800] to [Pr.811] | ⋮ |
| 54300 to 54319 | Mark detection setting parameter [Pr.800] to [Pr.811] | Mark detection setting 16 |
| 54640 to 54649 | Mark detection control data [Cd.800], [Cd.801], [Cd.802] | Mark detection setting 1 |
| 54650 to 54659 | Mark detection control data [Cd.800], [Cd.801], [Cd.802] | Mark detection setting 2 |
| 54660 to 54669 | Mark detection control data [Cd.800], [Cd.801], [Cd.802] | Mark detection setting 3 |
| ⋮ | Mark detection control data [Cd.800], [Cd.801], [Cd.802] | ⋮ |
| 54790 to 54799 | Mark detection control data [Cd.800], [Cd.801], [Cd.802] | Mark detection setting 16 |
| 54960 to 55039 | Mark detection monitor data [Md.800], [Md.801] | Mark detection setting 1 |
| 55040 to 55119 | Mark detection monitor data [Md.800], [Md.801] | Mark detection setting 2 |
| 55120 to 55199 | Mark detection monitor data [Md.800], [Md.801] | Mark detection setting 3 |
| ⋮ | Mark detection monitor data [Md.800], [Md.801] | ⋮ |
| 56160 to 56239 | Mark detection monitor data [Md.800], [Md.801] | Mark detection setting 16 |

*In the original, each "Item" cell is merged over its 5 rows. Expanded to each row. The "⋮" rows are as printed in the original (settings 4 to 15 are not listed; they follow the same increments: 20 words for parameters, 10 words for control data, 80 words for monitor data).

The following shows the parameters and data used in the mark detection function.

### Mark detection setting parameters (マーク検出設定パラメータ) (8.10 / original p.366-367)

k: Mark detection setting No. - 1

| Setting item | | Setting details/setting value | Default value | Buffer memory address |
|---|---|---|---|---|
| [Pr.800] | Mark detection signal setting | Set the external input signal (high speed input request) for mark detection.<br>0: Invalid<br>1 to 4: External command signal on axis 1 to axis 4 (4-axis module)<br>1 to 8: External command signal on axis 1 to axis 8 (8-axis module)<br>301 to 304: TPR1 of servo amplifiers on axis 1 to axis 4 (4-axis module) [FX5-SSC-G]<br>301 to 308: TPR1 of servo amplifiers on axis 1 to axis 8 (8-axis module) [FX5-SSC-G]<br>901: Link device [FX5-SSC-G]<br>Fetch cycle: At power supply ON | 0 | 54000+20k |
| [Pr.801] | Mark detection signal compensation time | Set the compensation time such as delay of sensor.<br>Set a positive value to compensate for a delay.<br>-32768 to 32767 [μs]<br>Fetch cycle: At power supply ON or "[Cd.190] PLC READY" OFF to ON | 0 | 54001+20k |
| [Pr.802] | Mark detection data type | Set the target data for mark detection.<br>0 to 14: Data type<br>-1: Optional 2 word buffer memory<br>Fetch cycle: At power supply ON | 0 | 54002+20k |
| [Pr.803] | Mark detection data axis No. | Set the axis No. of target data for mark detection.<br>1 to 4: Axis 1 to axis 4 (4-axis module)<br>1 to 8: Axis 1 to axis 8 (8-axis module)<br>201 to 204: Command generation axis 1 to axis 4 (4-axis module)<br>201 to 208: Command generation axis 1 to axis 8 (8-axis module)<br>801 to 804: Synchronous encoder axis 1 to axis 4<br>Fetch cycle: At power supply ON | 0 | 54003+20k |
| [Pr.804] | Mark detection data buffer memory No. | Set the optional buffer memory No.<br>Set this parameter as an even number.<br>0 to 98302: Optional buffer memory<br>Fetch cycle: At power supply ON | 0 | 54004+20k<br>54005+20k |
| [Pr.805] | Latch data range upper limit value | Set the valid upper limit value for latch data at mark detection.<br>-2147483648 to 2147483647<br>Fetch cycle: At power supply ON, "[Cd.190] PLC READY" OFF to ON, or request (Latch data range change) | 0 | 54006+20k<br>54007+20k |
| [Pr.806] | Latch data range lower limit value | Set the valid lower limit value for latch data at mark detection<br>-2147483648 to 2147483647<br>Fetch cycle: At power supply ON, "[Cd.190] PLC READY" OFF to ON, or request (Latch data range change) | 0 | 54008+20k<br>54009+20k |
| [Pr.807] | Mark detection mode setting | Set the continuous detection mode or specified number of detection mode.<br>0: Continuous detection mode<br>1 to 32: Specified number of detection mode (Set the number of detections.)<br>-1 to -32: Ring buffer mode (Set the value that made the number of buffers into negative value.)<br>Fetch cycle: At power supply ON or "[Cd.190] PLC READY" OFF to ON | 0 | 54010+20k |
| [Pr.808] | Mark detection signal link device type [FX5-SSC-G] | Set the link device for use.<br>Others: Invalid<br>11H: RX<br>12H: RY<br>13H: RWr<br>14H: RWw<br>Fetch cycle: At power supply ON | 0 | 54011+20k |
| [Pr.809] | Mark detection signal link device start No. [FX5-SSC-G] | Set the link device No. for use.<br>Fetch cycle: At power supply ON | 0 | 54012+20k |
| [Pr.810] | Mark detection signal link device bit specification [FX5-SSC-G] | Set the bit No. to be used when setting "13H: RWr", "14H: RWw" to "[Pr.808] Mark detection signal link device type".<br>Fetch cycle: At power supply ON | 0 | 54013+20k |
| [Pr.811] | Mark detection signal detection direction setting [FX5-SSC-G] | Set signal detection direction in case of specifying TPR1 of the servo amplifier and the link device in "[Pr.800] Mark detection signal setting". Only bit0 setting is enabled.<br>0: Rising detection<br>1: Falling detection<br>Fetch cycle: At power supply ON | 0 | 54014+20k |

> **Point** (original p.367)
> The above parameters are valid with the value set in the flash ROM of the Simple Motion module/Motion module when the power ON or the CPU module reset. Except for a part, the value is not fetched by turning the "[Cd.190] PLC READY" ON from OFF. Therefore, write to the flash ROM after setting the value in the buffer memory to change.

### [Pr.800] Mark detection signal setting ([Pr.800]マーク検出信号設定) (8.10 / original p.367)

Set the input signal for mark detection.

| Setting value | Setting details |
|---|---|
| 0 | Invalid |
| 1 to 4 | External command signal (DI) on axis 1 to axis 4 (4-axis module) |
| 1 to 8 | External command signal (DI) on axis 1 to axis 8 (8-axis module) |
| 301 to 304 [FX5-SSC-G] | TPR1 of servo amplifiers on axis 1 to axis 4 (4-axis module) |
| 301 to 308 [FX5-SSC-G] | TPR1 of servo amplifiers on axis 1 to axis 8 (8-axis module) |
| 901 [FX5-SSC-G] | Link device |

If a value other than the above is set, the warning "Outside mark detection signal setting range" (warning code: 0936H [FX5-SSC-S], or warning code: 0D36H [FX5-SSC-G]) occurs and the target mark detection is not available.

[FX5-SSC-S]
Set "4: High speed input request" in "[Pr.42] External command function selection" and set "1: Validates an external command." in "[Cd.8] External command valid".

[FX5-SSC-G]
- When executing mark detection by the external signal command, Set "[Pr.42] External command function selection" to "4: High speed input request", "[Cd.8] External command valid" to "1: Validates an external command".
- When executing mark detection by TPR1 of the servo amplifier, assign TPR1 to CN3 of the corresponding servo amplifier.
- When using a link device, specify the target link device in [Pr.808] to [Pr.811].

> **Point**
> [FX5-SSC-G]
> When setting this parameter and executing mark detection by the external command, also set "[Pr.95] External command signal selection".
> - Setting example
>   When "101: DOG signal of axis 1" is set in "[Pr.95] External command signal selection" and "8: External command signal of axis 8 (DI)" is set in "[Pr.800] Mark detection signal setting" of axis 8, mark detection is performed with the DOG signal of the servo amplifier connected to axis 1.
>
> When the DOG signal is selected for use as the external command signal in "[Pr.95] External command signal selection", the accuracy of the mark detection changes to the accuracy of the operation cycle.
> When setting this parameter and executing mark detection by TPR1 of the servo amplifier, also set "[Pr.811] Mark detection signal detection direction setting". For the accuracy when using TPR1 of the servo amplifier, refer to the manual for servo amplifier.
> For MR-J5(W)-G: [Other manual] MR-J5 User's Manual (Function)

### [Pr.801] Mark detection signal compensation time ([Pr.801]マーク検出信号補正時間) (8.10 / original p.367)

Compensate the input timing of the mark detection signal.
Set this parameter to compensate such as delay of sensor input. (Set a positive value to compensate for a delay.)

### [Pr.802] Mark detection data type ([Pr.802]マーク検出データ種別) (8.10 / original p.368)

Set the data that latched at mark detection.
The target data is latched by setting "0 to 14". Set the axis No. in "[Pr.803] Mark detection data axis No.".
Optional 2 word buffer memory is latched by setting "-1". Set the buffer memory No. in "[Pr.804] Mark detection data buffer memory No.".

| Setting value | Data name |
|---|---|
| 0 | Command position value |
| 1 | Machine feed value |
| 2 | Actual position value |
| 3 | Servo input axis position value |
| 6 | Synchronous encoder axis position value |
| 7 | Synchronous encoder axis position value per cycle |
| 8 | Position value after composite main shaft gear |
| 9 | Position value per cycle after main shaft gear |
| 10 | Position value per cycle after auxiliary shaft gear |
| 11 | Cam axis position value per cycle |
| 12 | Cam axis position value per cycle (Real position) |
| 13 | Command position value of command generation axis |
| 14 | Position value per cycle of command generation axis |
| -1 | Optional 2 words buffer memory |

If a value other than the above is set, the warning "Outside mark detection data type setting range" (warning code: 0937H [FX5-SSC-S], or warning code: 0D37H [FX5-SSC-G]) occurs and the target mark detection is not available.

### [Pr.803] Mark detection data axis No. ([Pr.803]マーク検出データ軸番号) (8.10 / original p.368)

Set the axis No. of data that latched at mark detection.

| [Pr.802] Setting value | [Pr.802] Data name | Unit | [Pr.803] 4-axis module | [Pr.803] 8-axis module |
|---|---|---|---|---|
| 0 | Command position value | 10^-1 [μm], 10^-5 [inch], 10^-5 [degree], [pulse] | 1 to 4 | 1 to 8 |
| 1 | Machine feed value | 10^-1 [μm], 10^-5 [inch], 10^-5 [degree], [pulse] | 1 to 4 | 1 to 8 |
| 2 | Actual position value | 10^-1 [μm], 10^-5 [inch], 10^-5 [degree], [pulse] | 1 to 4 | 1 to 8 |
| 3 | Servo input axis position value | 10^-1 [μm], 10^-5 [inch], 10^-5 [degree], [pulse] | 1 to 4 | 1 to 8 |
| 6 | Synchronous encoder axis position value | Synchronous encoder axis position unit | 801 to 804 | 801 to 804 |
| 7 | Synchronous encoder axis position value per cycle | Synchronous encoder axis position unit | 801 to 804 | 801 to 804 |
| 8 | Position value after composite main shaft gear | Main input axis position unit | 1 to 4 | 1 to 8 |
| 9 | Position value per cycle after main shaft gear | Cam axis cycle unit | 1 to 4 | 1 to 8 |
| 10 | Position value per cycle after auxiliary shaft gear | Cam axis cycle unit | 1 to 4 | 1 to 8 |
| 11 | Cam axis position value per cycle | Cam axis cycle unit | 1 to 4 | 1 to 8 |
| 12 | Cam axis position value per cycle (Real position)*1 | Cam axis cycle unit | 1 to 4 | 1 to 8 |
| 13 | Command position value of command generation axis | Command generation axis position unit | 201 to 204 | 201 to 208 |
| 14 | Position value per cycle of command generation axis | Command generation axis position unit | 201 to 204 | 201 to 208 |

*In the original, the header row is split into "[Pr.802] Mark detection data type" (Setting value / Data name / Unit) and "[Pr.803] Mark detection data axis No." (4-axis module / 8-axis module). The Unit cells are merged vertically (rows 0-3, 6-7, 9-12, 13-14), and the axis No. cells are merged vertically (rows 0-3, 6-7, 8-12, 13-14). Expanded to each row.

*1 The same value as "11: Cam axis position value per cycle".

If a value other than the above is set, the warning "Outside mark detection data axis No. setting range" (warning code: 0938H [FX5-SSC-S], or warning code: 0D38H [FX5-SSC-G]) occurs and the target mark detection is not available.

### [Pr.804] Mark detection data buffer memory No. ([Pr.804]マーク検出データバッファメモリ番号) (8.10 / original p.368)

Set the No. of optional 2 words buffer memory that latched at mark detection.
Set this No. as an even No.
If a value other than the above is set, the warning "Outside mark detection data buffer memory No. setting range" (warning code: 0939H [FX5-SSC-S], or warning code: 0D39H [FX5-SSC-G]) occurs and the target mark detection is not available.

### [Pr.805] Latch data range upper limit value, [Pr.806] Latch data range lower limit value ([Pr.805]ラッチデータ範囲上限値，[Pr.806]ラッチデータ範囲下限値) (8.10 / original p.369)

Set the upper limit value and lower limit value of the latch data at mark detection.
When the data at mark detection is within the range, they are stored in "[Md.801] Mark detection data storage area (1 to 32)" and the "[Md.800] Number of mark detection" is incremented by 1. The mark detection processing is not executed.
(*As printed in the original. The last sentence presumably refers to data outside the range.)

- Upper limit value > Lower limit value

The mark detection is executed when the mark detection data is "greater or equal to the lower limit value and less than the upper limit value".

[Figure] Upper limit value > Lower limit value (original p.369)
- Sawtooth data over t. The range from "Lower limit value" (filled circle = included) to "Upper limit value" (open circle = not included) is drawn as a thick line = mark detection executed; the rest is a thin line.

- Upper limit value < Lower limit value

The mark detection is executed when the mark detection data is "greater or equal to the lower limit value or less than the upper limit value".

[Figure] Upper limit value < Lower limit value (original p.369)
- Sawtooth data over t. The part from "Lower limit value" (filled circle = included) up to the wrap, and from the wrap up to "Upper limit value" (open circle = not included), is drawn thick = mark detection executed; the part between the upper limit value and the lower limit value is thin (not executed).

- Upper limit value = Lower limit value

The mark detection range is not checked. The mark detection is executed for all range.

### [Pr.807] Mark detection mode setting ([Pr.807]マーク検出モード設定) (8.10 / original p.369)

Set the data storage method of mark detection.

| Mode | Setting value | Operation for mark detection | Mark detection data storage method |
|---|---|---|---|
| Continuous detection mode | 0 | Always | The data is updated in the mark detection data storage area 1. |
| Specified number of detection mode | 1 to 32 | Number of detections<br>(If the number of mark detection is the number of detections or more, the mark detection is not executed.) | The data is stored to the mark detection data storage area "n".<br>n = (1 + Number of mark detection) |
| Ring buffer mode | -1 to -32 | Always<br>(The mark detection data storage area 1 to 32 is used as a ring buffer for the number of detections.) | The data is stored to the mark detection data storage area "n".<br>n = (1 + Number of mark detection) |

*In the original, the "Mark detection data storage method" cell is merged over the 2 rows Specified number of detection mode / Ring buffer mode. Expanded to each row.

### [Pr.808] Mark detection signal link device type [FX5-SSC-G] ([Pr.808]マーク検出信号リンクデバイス種別[FX5-SSC-G]) (8.10 / original p.369)

Set the link device type for use.

| Setting value | Setting details |
|---|---|
| 11H | RX |
| 12H | RY |
| 13H | RWr |
| 14H | RWw |

Values other than the above are invalid.

### [Pr.809] Mark detection signal link device start No. [FX5-SSC-G] ([Pr.809]マーク検出信号リンクデバイス先頭番号[FX5-SSC-G]) (8.10 / original p.370)

Set the link device No. for use.
RX/RY: 0 to 1FFFH
RWr/RWw: 0 to 3FFH
When a link device No. outside the range is set, the warning "Mark detection link device start No. specification" (warning code: 0D2EH) occurs and the target mark detection cannot be used.

### [Pr.810] Mark detection signal link device bit specification [FX5-SSC-G] ([Pr.810]マーク検出信号リンクデバイスビット指定[FX5-SSC-G]) (8.10 / original p.370)

Set the link device No. to be used when setting "13H: RWr" and "14H: RWw" for "[Pr.808] Mark detection signal link device type".
When a value outside the range is set, the warning "Mark detection link device bit specification" (warning code: 0D2FH) occurs and the target mark detection cannot be used.

### [Pr.811] Mark detection signal detection direction setting [FX5-SSC-G] ([Pr.811]マーク検出信号検出方向設定[FX5-SSC-G]) (8.10 / original p.370)

Set signal detection direction in case of specifying TPR1 of the servo amplifier and the link device in "[Pr.811] Mark detection signal detection direction setting". Only bit0 setting is enabled.
0: Rising detection
1: Falling detection

(*As printed in the original. In the parameter table on p.366 the same sentence reads "... in "[Pr.800] Mark detection signal setting".")

### Mark detection control data (マーク検出制御データ) (8.10 / original p.371)

k: Mark detection setting No. - 1

| Setting item | | Setting details/setting value | Default value | Buffer memory address |
|---|---|---|---|---|
| [Cd.800] | Number of mark detection clear request | Set "1" to execute "0" clear of number of mark detections.<br>"0" is automatically set after completion by "0" clear of number of mark detections.<br>1: 0 clear of number of mark detections<br>Fetch cycle: Operation cycle | 0 | 54640+10k |
| [Cd.801] | Mark detection invalid flag | Set this flag to invalidate mark detection temporarily.<br>1: Mark detection: Invalid<br>Others: Mark detection: Valid<br>Fetch cycle: Operation cycle | 0 | 54641+10k |
| [Cd.802] | Latch data range change request | Request the processing of latch data range change.<br>Set the following value depending on the timing of updating the change value.<br>1: Change in the next Operation cycle of the requested<br>2: Change in the next DI input of the requested<br>"0" is automatically set after the change is completed.<br>Fetch cycle: Operation cycle or at conditions established (DI input) | 0 | 54642+10k |

### [Cd.800] Number of mark detection clear request ([Cd.800]マーク検出回数クリア要求) (8.10 / original p.371)

Set "1" to execute "0" clear of "[Md.800] Number of mark detection". "0" is automatically set after completion by "0" clear of "[Md.800] Number of mark detection".

### [Cd.801] Mark detection invalid flag ([Cd.801]マーク検出無効フラグ) (8.10 / original p.371)

Set "1" to invalidate mark detection temporarily. The mark detection signal during invalidity is ignored.

### [Cd.802] Latch data range change request ([Cd.802]ラッチデータ範囲変更要求) (8.10 / original p.371)

Request the processing of latch data range change. Set the following value depending on the timing of updating the change value.
1: Change in the next Operation cycle of the requested
2: Change in the next DI input of the requested
- "0" is automatically set after receiving the latch data range change request. (It indicates that the latch data range change is completed.)
- "[Pr.805] Latch data range upper limit value" and "[Pr.806] Latch data range lower limit value" at latch data range change request are used as the change value.
- Restrictions according to the type of latch data range change request are shown below.

○: Possible, ×: Not possible

| Types of change request | [Cd.801] Mark detection invalid flag | Changing possibility |
|---|---|---|
| 1: Change in the next Operation cycle of the requested | 1: Mark detection: Invalid | ○ |
| 1: Change in the next Operation cycle of the requested | Other than 1: Mark detection: Valid | ○ |
| 2: Change in the next DI input of the requested | 1: Mark detection: Invalid | × |
| 2: Change in the next DI input of the requested | Other than 1: Mark detection: Valid | ○ |

*In the original, each "Types of change request" cell is merged over 2 rows, and the "○" for type 1 is merged over its 2 rows. Expanded to each row.

### Mark detection monitor data (マーク検出モニタデータ) (8.10 / original p.372)

k: Mark detection setting No. - 1

| Storage item | | Storage details/storage value | Buffer memory address |
|---|---|---|---|
| [Md.800] | Number of mark detection | The number of mark detections is stored.<br>"0" clear is executed at power supply ON.<br>Continuous detection mode: 0 to 65535 (Ring counter)<br>Specified number of detection mode: 0 to 32<br>Ring buffer mode: 0 to (number of buffers - 1)<br>Refresh cycle: At conditions established (Mark detection) | 54960+80k |
| [Md.801] | Mark detection data storage area 1<br>⋮<br>Mark detection data storage area 32 | The latch data at mark detection is stored.<br>Data for up to 32 times are stored in the specified number of detection mode.<br>Data are stored as a ring buffer for number of detections in the ring buffer mode.<br>-2147483648 to 2147483647<br>Refresh cycle: At conditions established (Mark detection) | 54962+80k<br>54963+80k<br>⋮<br>55024+80k<br>55025+80k |

### [Md.800] Number of mark detection ([Md.800]マーク検出回数) (8.10 / original p.372)

The counter value is incremented by 1 at mark detection. Preset "0" clear in "[Cd.800] Number of mark detection clear request" to execute the mark detection in specified number of detections mode or ring buffer mode.

### [Md.801] Mark detection data storage area (1 to 32) ([Md.801]マーク検出データ格納エリア(1～32)) (8.10 / original p.372)

The latch data at mark detection is stored. Data for up to 32 times can be stored in the specified number of detection mode or ring buffer mode.

### Precautions (注意事項) (8.10 / original p.372)

- When the data of "[Pr.802] Mark detection data type" or "[Pr.803] Mark detection data axis No." is selected incorrectly, the incorrect latch data is stored. For the data of "[Pr.802] Mark detection data type", set the item No. instead of specifying the buffer memory No. directly.
- When mark detection is performed when not in synchronous control and "8: Position value after composite main shaft gear" to "12: Cam axis position value per cycle (Real position)" is selected in "[Pr.802] Mark detection data type", the latched value may be different from the actual outputted monitor data.
- If the mark detection signal is input at the timing when the latch target data is changed significantly such as by the current position change or the home position return, the correct data cannot be latched.
  During the current position change or the home position return, use the data such as "[Cd.801] Mark detection invalid flag" to temporarily disable the mark detection.

[FX5-SSC-G]
- If the operation cycle over occurs before or after signal input at the mark detection, the accuracy of estimate calculation may be lowered.
- When using TPR1 of the servo amplifier as mark detection input, do not turn ON and Off multiple times in one communication cycle to the signal input in the servo amplifier. By doing so, the signal cannot be detected correctly.

## 8.11 Optional Data Monitor Function (任意データモニタ機能) (8.11 / original p.373-377)

### Registered monitor (登録モニタ) (8.11 / original p.373-377)

The data of the registered monitor is refreshed every operation cycle.
This function is used to store the data (refer to following table) up to four points per axis to the buffer memory and monitor them.

#### Data that can be set [FX5-SSC-S] (指定可能なデータ[FX5-SSC-S]) (8.11 / original p.373)

○: Possible, —: Not possible ("0" is stored.)

| Data type | | Unit | Used point | MR-J3(W)-B | MR-J4(W)-B | MR-J5(W)-B | MR-JE-B(F) |
|---|---|---|---|---|---|---|---|
| 1 | Effective load ratio | [%] | 1 word | ○ | ○ | ○ | ○ |
| 2 | Regenerative load ratio | [%] | 1 word | ○ | ○ | ○ | ○ |
| 3 | Peak load ratio | [%] | 1 word | ○ | ○ | ○ | ○ |
| 4 | Load inertia moment ratio | [× 0.1] | 1 word | ○ | ○ | ○ | ○ |
| 5 | Model loop gain | [rad/s] | 1 word | ○ | ○ | ○ | ○ |
| 6 | Bus voltage | [V] | 1 word | ○ | ○ | ○ | ○ |
| 7 | Servo motor speed*1 | [r/min] | 1 word | ○ | ○ | ○ | ○ |
| 8 | Encoder multiple revolution counter | [rev] | 1 word | ○ | ○ | ○ | ○ |
| 9 | Unit power consumption | [W] | 1 word | — | ○ | ○ | ○ |
| 10 | Instantaneous torque | [× 0.1%] | 1 word | — | ○ | ○ | ○ |
| 12 | Servo motor thermistor temperature | [℃] | 1 word | ○ | ○ | ○ | ○ |
| 13 | Torque equivalent to disturbance | [× 0.1%] | 1 word | — | ○ | ○ | ○ |
| 14 | Overload alarm margin | [× 0.1%] | 1 word | — | ○ | ○ | ○ |
| 15 | Excessive error alarm margin | [× 16 pulses] | 1 word | — | ○ | ○*2 | ○ |
| 16 | Settling time | [ms] | 1 word | — | ○ | ○ | ○ |
| 17 | Overshoot amount | [pulse] | 1 word | — | ○ | ○*2 | ○ |
| 18 | Internal temperature of encoder | [℃] | 1 word | — | ○ | ○ | ○ |
| 20 | Position feedback | [pulse] | 2 words | ○ | ○ | ○*2 | ○ |
| 21 | Encoder position within one revolution | [pulse] | 2 words | ○ | ○ | ○*2 | ○ |
| 22 | Selected droop pulse | [pulse] | 2 words | ○ | ○ | ○*2 | ○ |
| 23 | Unit total power consumption | [Wh] | 2 words | — | ○ | ○ | ○ |
| 24 | Load-side encoder information 1 | [pulse] | 2 words | — | ○*4 | ○*3*4 | ○*4 |
| 25 | Load-side encoder information 2 | — | 2 words | — | ○*4 | ○*3*4 | ○*4 |
| 26 | Z-phase counter | [pulse] | 2 words | — | ○*5 | ○*2*5 | ○*5 |
| 27 | Servo motor side/load-side position deviation | [pulse] | 2 words | — | ○*3 | ○*2*3 | ○*3 |
| 28 | Servo motor side/load-side speed deviation | [× 0.01 r/min] | 2 words | — | ○*3 | ○*3 | ○*3 |
| 30 | Unit power consumption (2 words) | [Wh] | 2 words | — | ○ | ○ | ○ |
| Most significant bit1 + address value | Optional address of registered monitor | (blank) | — | ○ | ○ | ○ | ○ |

*In the original, the 4 servo amplifier columns are under the common header "Monitoring possibility". "Used point" is merged: "1 word" over data types 1 to 18, "2 words" over 20 to 30. Expanded to each row.

*1 The motor rotation speed that took the average every 227 [ms].
Use the servo amplifiers of version compatible with the monitor of motor speed.
Always "0" if the monitor is executed for the servo amplifier which does not support this function.
*2 The value is multiplied by the multiplicative inverse of the electronic gear ratio of the servo amplifier (command unit). The same data as MR-J4(W)-B can be stored by configuring the electronic gear setting of the servo amplifier.
*3 It can be monitored when using the fully closed loop control.
*4 It can be monitored when using the synchronous encoder via servo amplifier.
*5 It can be monitored when using the linear servo motors.

Refer to the manuals of each servo amplifier for details of the data monitored.

#### Specifiable data [FX5-SSC-G] (指定可能なデータ[FX5-SSC-G]) (8.11 / original p.374)

Set the index of the CiA402 object of the device.

Ex.
When monitoring the effective load ratio, set "2B09H".

#### List of parameters and data (パラメータ・データ一覧) (8.11 / original p.374-377)

The parameters and data used in the optional data monitor function is shown below.

- Extended parameter

n: Axis No. - 1

| Setting item | | Setting details/setting value | Buffer memory address |
|---|---|---|---|
| [Pr.91] | Optional data monitor: Data type setting 1 | • Set the data type monitored in optional data monitor function every data type setting. (→Page 371 Data that can be set [FX5-SSC-S])<br>• When "0: No setting" is set, the stored value of "[Md.109] Regenerative load ratio/Optional data monitor output 1" to "[Md.112] Optional data monitor output 4" is different every data type setting 1 to 4. | 100+150n |
| [Pr.92] | Optional data monitor: Data type setting 2 | (same as [Pr.91]) | 101+150n |
| [Pr.93] | Optional data monitor: Data type setting 3 | (same as [Pr.91]) | 102+150n |
| [Pr.94] | Optional data monitor: Data type setting 4 | (same as [Pr.91]) | 103+150n |
| [Pr.591] | Optional data monitor: Data type expansion setting 1 [FX5-SSC-G] | Set the data type monitored in optional data monitor function. | 92+150n |
| [Pr.592] | Optional data monitor: Data type expansion setting 2 [FX5-SSC-G] | Set the data type monitored in optional data monitor function. | 93+150n |
| [Pr.593] | Optional data monitor: Data type expansion setting 3 [FX5-SSC-G] | Set the data type monitored in optional data monitor function. | 94+150n |
| [Pr.594] | Optional data monitor: Data type expansion setting 4 [FX5-SSC-G] | Set the data type monitored in optional data monitor function. | 95+150n |

*In the original, the "Setting details/setting value" cell is merged over [Pr.91] to [Pr.94] (4 rows) and over [Pr.591] to [Pr.594] (4 rows). Expanded to each row ("(same as [Pr.91])" for the long cell).

[When specifying the optional address of registered monitor] [FX5-SSC-S]
Switches to direct specification of the registered monitor address for each optional data monitor data type.

[Figure] Bit layout of [Pr.91] to [Pr.94] when specifying the optional address (original p.374)
- b0 to b14: Address direct specification area
- b15: Optional address of registered monitor — Setting value: 0: Address not specified / 1: Address specification

Optional address of registered monitor is used to retrieve data not selectable with each connected device. For details, contact the manufacturer of the connected device.

> **Point** (original p.375)
> [FX5-SSC-S]
> - The monitor address of optional data monitor is registered to servo amplifier with initialized communication after the power supply is turned ON or the CPU module is reset.
> - Set the data type of "used point: 2 words" in "[Pr.91] Optional data monitor: Data type setting 1" or "[Pr.93] Optional data monitor: Data type setting 3". If it is set in "[Pr.92] Optional data monitor: Data type setting 2" or "[Pr.94] Optional data monitor: Data type setting 4", the warning "Optional data monitor data type setting error" (warning code: 0933H) will occur with initialized communication to servo amplifier, and "0" is set in "[Md.109] Regenerative load ratio/Optional data monitor output 1" to "[Md.112] Optional data monitor output 4".
> - Set "0" in "[Pr.92] Optional data monitor: Data type setting 2" when the data type of "used point: 2 words" is set in "[Pr.91] Optional data monitor: Data type setting 1", and set "0" in "[Pr.94] Optional data monitor: Data type setting 4" when the data type of "used point: 2 words" is set in "[Pr.93] Optional data monitor: Data type setting 3". When other than "0" is set, the warning "Optional data monitor data type setting error" (warning code: 0933H) will occur with initialized communication to servo amplifier, and "0" is set in "[Md.109] Regenerative load ratio/Optional data monitor output 1" to "[Md.112] Optional data monitor output 4".
> - When the data type of "used point: 2 words" is set, the monitor data of low-order is "[Md.109] Regenerative load ratio/Optional data monitor output 1" or "[Md.111] Peak torque ratio/Optional data monitor output 3".
> - Refer to →Page 371 Data that can be set [FX5-SSC-S] for the data type that can be monitored on each servo amplifier. When the data type that cannot be monitored is set, "0" is stored to the monitor output.
> - When directly specifying addresses for each optional data monitor type, specify the addresses in bit0 to bit14 of "[Pr.91] Optional data monitor: Data type setting 1" to "[Pr.94] Optional data monitor: Data type setting 4" and set "1" in bit15.
> - When monitoring 2-word data, set the lower data to "[Pr.91] Optional data monitor: Data type setting 1" and the upper data to "[Pr.92] Optional data monitor: Data type setting 2", or the lower data to "[Pr.93] Optional data monitor: Data type setting 3" and the upper data to "[Pr.94] Optional data monitor: Data type setting 4".

> **Point** (original p.376)
> [FX5-SSC-G]
> - Registered monitor addresses for the optional data monitor are imported after the power is turned ON or the CPU module is reset.
> - Set data types that use 2 points in either "[Pr.91] Optional data monitor: Data type setting 1" and "[Pr.591] Optional data monitor: Data type expansion setting 1" or "[Pr.93] Optional data monitor: Data type setting 3" and "[Pr.593] Optional data monitor: Data type expansion setting 3". The setting values of both "[Pr.92] Optional data monitor: Data type setting 2" and "[Pr.592] Optional data monitor: Data type expansion setting 2" and [Pr.94] Optional data monitor: Data type setting 4" and "[Pr.594] Optional data monitor: Data type expansion setting 4"are ignored.
> - Confirming the correctness of the object size cannot be performed on the Motion module. As such, the monitor output value will not be stored correctly when the set object size and the actual object size are different. Exercise caution when directly specifying from the engineering tool or setting the optional data monitor from the buffer memory.
>
> [Figure] Example of incorrect object size setting (original p.376)
> - Correct objects: (1) Effective load ratio (2B09H, size 16 bit), (2) Servo motor speed (2B02H, size 32 bit), (3) Regenerative load ratio (2B08H, size 16 bit).
> - "When the items above are incorrectly set to the following:" (1) Effective load ratio (2B09H, size 32 bit), (2) Servo motor speed (2B02H, size 16 bit), (3) Regenerative load ratio (2B08H, size 16 bit).
> - Settings: Pr.91 = 2B09H, Pr.92 = 2B09H, Pr.93 = 2B02H, Pr.94 = 2B08H; Pr.591 = 0020H, Pr.592 = 0020H, Pr.593 = 0010H, Pr.594 = 0010H.
> - Result: Md.109 "The actual load ratio (2B09H) is output to the monitor"; Md.110 "The servo motor speed (2B02H) is output to the monitor"; Md.111 "The servo motor speed (2B02H) is output to the monitor"; Md.112 "The regenerative load ratio (2B08H) is output to the monitor".
> - Note for Pr.91/Pr.591: "The actual object size is 16 bit, so the monitor is only output to "[Md.109] Regenerative load ratio/Optional data monitor output 1"."
> - Note for Pr.93/Pr.593: "The actual object size is 32 bit, so the monitor is only output to "[Md.110] Effective load torque/Optional data monitor output 2" and "[Md.111] Peak torque ratio/Optional data monitor output 3"."
> - (Arrows in the figure: Pr.591 → Md.109, Pr.593 → Md.111, Pr.594 → Md.112. "actual load ratio" is as printed.)
>
> - When a value other than 08H, 10H, 20H, or 40H is set in "[Pr.591] Optional data monitor: Data type expansion setting 1" to "[Pr.594] Optional data monitor: Data type expansion setting 4", the value is treated as being 20H.
> - When a CiA402 object that cannot be monitored is set, the error "PDO mapping setting error" (error code: 1C48H) occurs and communication with that axis is not performed.

- Axis monitor data (original p.377)

n: Axis No. - 1

| Storage item | | Storage details/storage value (FX5-SSC-S) | Storage details/storage value (FX5-SSC-G) | Buffer memory address |
|---|---|---|---|---|
| [Md.109] | Regenerative load ratio/Optional data monitor output 1 | • The content set in "[Pr.91] Optional data monitor: Data type setting 1" is stored at optional data monitor data type setting.<br>• The regenerative load ratio is stored when nothing is set. | • The content set in "[Pr.91] Optional data monitor: Data type setting 1" and "[Pr.591] Optional data monitor: Data type expansion setting 1" is stored at optional data monitor data type setting.<br>• The regenerative load ratio is stored when nothing is set. | 2478+100n |
| [Md.110] | Effective load torque/Optional data monitor output 2 | • The content set in "[Pr.92] Optional data monitor: Data type setting 2" is stored at optional data monitor data type setting.<br>• The effective load ratio is stored when nothing is set. | • The content set in "[Pr.92] Optional data monitor: Data type setting 2" and "[Pr.592] Optional data monitor: Data type expansion setting 2" is stored at optional data monitor data type setting.<br>• The effective load ratio is stored when nothing is set. | 2479+100n |
| [Md.111] | Peak torque ratio/Optional data monitor output 3 | • The content set in "[Pr.93] Optional data monitor: Data type setting 3" is stored at optional data monitor data type setting.<br>• The peak torque ratio is stored when nothing is set. | • The content set in "[Pr.93] Optional data monitor: Data type setting 3" and "[Pr.593] Optional data monitor: Data type expansion setting 3" is stored at optional data monitor data type setting.<br>• The peak torque ratio is stored when nothing is set. | 2480+100n |
| [Md.112] | Optional data monitor output 4 | • The content set in "[Pr.94] Optional data monitor: Data type setting 4" is stored at optional data monitor data type setting.<br>• "0" is stored when nothing is set. | • The content set in "[Pr.94] Optional data monitor: Data type setting 4" and "[Pr.594] Optional data monitor: Data type expansion setting 4" is stored at optional data monitor data type setting.<br>• "0" is stored when nothing is set. | 2481+100n |

*In the original, "Storage details/storage value" is one header spanning the FX5-SSC-S and FX5-SSC-G columns.

> **Point**
> When the communication interrupted by the servo amplifier's power supply OFF or disconnection of communication cable with servo amplifiers during optional data monitor, "0" is stored in [Md.109] to [Md.112].

## 8.12 Event History Function [FX5-SSC-G] (イベント履歴機能[FX5-SSC-G]) (8.12 / original p.378)

The "Event History Function" is a function that saves error information and operations performed to the module as events on the CPU module or SD memory card. The saved event information can be displayed in the engineering tool, allowing the occurrence history to be checked in chronological order.
In addition, error detail information can be checked by referencing "Added Information" in the event history.

[Figure] Outline of the event history function (original p.378)
- Engineering tool shows "Event history" (Date and time*1 / Module / Details):
  - 2020/4/7 16:55 / Analog / Executed the parameter operation.
  - 2020/4/7 19:27 / Power supply / An error occurred in the power supply module.
  - 2020/4/7 19:28 / Positioning / A home position return method error occurred.
  - 2020/4/7 19:29 / CPU / The BATTERY ERR occurred.
  - 2020/4/7 19:45 / CPU / Executed the PC reading by a user.
  - 2020/4/8 00:00 / CPU / Executed the time adjustment.
- "Event occurrence history which is stored in the connected CPU module can be checked using the engineering tool."
- "The CPU module can collect and save the event information occurred in the self CPU and the module controlled by the self CPU in a batch." — saved to CPU data memory or SD memory card.
- The Motion module is connected to servo amplifiers/motors via the CC-Link IE TSN Network.

*1 Displays a value set by the clock function of the CPU module.

> **Restriction**
> Detail information of some events are not displayed in the event history.

### Events that occur on the Motion module (モーションユニットで発生するイベント) (8.12 / original p.378)

The items saved in the event history are shown below.
For events related to the CC-Link IE TSN network, refer to "Event List" in the following manual.
[Other manual] MELSEC iQ-F FX5 Motion Module User's Manual (CC-Link IE TSN)

| Event type | Event category | Details | Event item | Event code |
|---|---|---|---|---|
| System | Error | An error was detected on the Motion module. | Major error | 03C00 to 03FFF |
| System | Error | An error was detected on the Motion module. | Moderate error | 02000 to 03BFF |
| System | Error | An error was detected on the Motion module. | Minor error | 01000 to 01FFF |
| System | Warning | A warning was detected on the Motion module. | Warning | 00800 to 00FFF |

*In the original, "System" is merged over 4 rows; "Error" and "An error was detected on the Motion module." are merged over 3 rows. Expanded to each row.

## 8.13 Connect/Disconnect Function of SSCNET Communication [FX5-SSC-S] (SSCNET通信の切断／再接続機能[FX5-SSC-S]) (8.13 / original p.379-382)

Temporarily connect/disconnect of SSCNET communication is executed during system's power supply ON. This function is used to exchange the servo amplifiers or SSCNETⅢ cables.

### Control details (制御内容) (8.13 / original p.379)

Set the connect/disconnect request of SSCNET communication in "[Cd.102] SSCNET control command", and the status for the command accept waiting or execute waiting is stored in "[Md.53] SSCNET control status". Use this buffer memory to connect the servo amplifiers disconnected by this function.
When the power supply module of head axis of SSCNET system (servo amplifier connected directly to the Simple Motion module) turns OFF/ON, this function is not necessary.

### Precautions during control (制御上の注意事項) (8.13 / original p.379)

- Confirm the LED display of the servo amplifier for "AA" after completion of SSCNET communication disconnect processing. And then, turn OFF the servo amplifier's power supply.
- The "[Md.53] SSCNET control status" only changes into the "-1: Execute waiting" even if the "Axis No.: Disconnect command of SSCNET communication" or "-10: Connect command of SSCNET communication" is set in "[Cd.102] SSCNET control command". The actual processing is not executed. Set "-2: Execute command" in "[Cd.102] SSCNET control command" to execute.
- When the "Axis No.: Disconnect command of SSCNET communication" is set to axis not connect or virtual servo amplifier, the status will not change without "[Md.53] SSCNET control status" becoming "-1: Execute waiting".
- Operation failure may occur in some axes if the servo amplifier's power supply is turned OFF without using the disconnect function. Be sure to turn OFF the servo amplifier's power supply by the disconnect function.
- Execute the connect/disconnect command to the A-axis for multiple-axis servo amplifier.
- When using the driver communication function, it can be disconnected by executing the connect/disconnect command, however it cannot be connected again.
- The connect/disconnect/execute command cannot be accepted during amplifier-less operation mode. "[Md.53] SSCNET control status" will be "0: Command accept waiting" (The disconnection is released.). If being switched to the amplifier-less operation mode when "[Md.53] SSCNET control status" is "1: Disconnected axis existing", the disconnected axis is automatically connected when switching to the normal operation mode again. If being switched to the amplifier-less operation mode when "[Md.53] SSCNET control status" is "-1: Execute waiting", the connect/disconnect command becomes invalid.

### Data list (データ一覧) (8.13 / original p.379-380)

The data for the connect/disconnect function of SSCNET communication is shown below.

#### System control data (システム制御データ) (8.13 / original p.379)

| Monitor item | | Setting value | Setting details | Buffer memory address |
|---|---|---|---|---|
| [Cd.102] | SSCNET control command | → | The connect/disconnect command of SSCNET communication is executed.<br>0: No command<br>Axis No.*1: Disconnect command of SSCNET communication (Axis No. to be disconnected)<br>-2: Execute command<br>-10: Connect command of SSCNET communication<br>Except above setting: Invalid | 5932 |

*The header "Monitor item" is as printed in the original (for control data).

*1 1 to the maximum control axes

#### System monitor data (システムモニタデータ) (8.13 / original p.380)

| Monitor item | | Monitor value | Storage details | Buffer memory address |
|---|---|---|---|---|
| [Md.53] | SSCNET control status | → | The connect/disconnect status of SSCNET communication is stored.<br>1: Disconnected axis existing<br>0: Command accept waiting<br>-1: Execute waiting<br>-2: Executing | 4233 |

### Procedure to connect/disconnect (切断／再接続手順) (8.13 / original p.380)

Procedure to connect/disconnect at the exchange of servo amplifiers or SSCNETⅢ cables is shown below.

#### Procedure to disconnect (切断手順) (8.13 / original p.380)

1. Set the axis No. to disconnect in "[Cd.102] SSCNET control command". (Setting value: 1 to the maximum control axes)
2. Check that "-1: Execute waiting" is stored in "[Md.53] SSCNET control status". (Disconnect execute waiting)
3. Set "-2: Execute command" in "[Cd.102] SSCNET control command".
4. Check that "1: Disconnected axis existing" is stored in "[Md.53] SSCNET control status". (Completion of disconnection. "20: Servo amplifier has not been connected" is stored in "[Md.26] Axis operation status".)
5. Turn OFF the servo amplifier's power supply after checking the LED display "AA" of servo amplifier to be disconnected.

[Figure] Disconnect timing (original p.380)
- [Cd.102] SSCNET control command: 0 → "1 to the maximum control axes" (Disconnect command (Axis No. of servo amplifier to be disconnected)) → -2 (Disconnect execute command) → 0 (Disconnect command clear).
- [Md.53] SSCNET control status: 0 (Command accept waiting) → -1 (Disconnect execute waiting), following the disconnect command → -2 (Disconnect executing), following the execute command → 1 (Disconnected axis existing) = "Completion of disconnection".
- The disconnect command clear (0) is written after the completion of disconnection.

#### Procedure to connect (再接続手順) (8.13 / original p.380)

1. Turn ON the servo amplifier's power supply.
2. Set "-10: Connect command of SSCNET communication" in "[Cd.102] SSCNET control command".
3. Check that "-1: Execute waiting" is set in "[Md.53] SSCNET control status". (Connect execute waiting)
4. Set "-2: Execute command" in "[Cd.102] SSCNET control command".
5. Check that "0: Command accept waiting" is set in "[Md.53] SSCNET control status". (Completion of connection)
6. Resume operation of servo amplifier after checking "0: Standby" in "[Md.26] Axis operation status" of the connected axis.

[Figure] Connect timing (original p.380)
- [Cd.102] SSCNET control command: 0 → -10 (Connect command) → -2 (Connect execute command) → 0 (Connect command clear).
- [Md.53] SSCNET control status: 1 (Disconnected axis existing) → -1 (Connect execute waiting), following the connect command → -2 (Connect executing), following the execute command → 0 (Command accept waiting) = "Completion of connection".
- The connect command clear (0) is written after the completion of connection.

> **Point**
> When "-1: Execute waiting" is set in "[Md.53] SSCNET control status", the command of execute waiting can be canceled if "0: No command" is set in "[Cd.102] SSCNET control command".

### Program (プログラム) (8.13 / original p.381-382)

The following shows the program example to connect/disconnect the servo amplifiers connected after Axis 3.

| Disconnect procedure | Connect procedure |
|---|---|
| Turn OFF the servo amplifier's power supply after checking the LED display "AA" of servo amplifier by turning bDisconnectCommand OFF to ON. | Resume operation of servo amplifier after checking the "[Md.26] Axis operation status" of the connected servo amplifier by turning bConnectCommand from OFF to ON. |

#### System configuration (システム構成) (8.13 / original p.381)

[Figure] System configuration (original p.381)
- Simple Motion module → Servo amplifier MR-J3(W)-B/MR-J4(W)-B/MR-J5(W)-B, daisy-chained Axis 1 → Axis 2 → Axis 3 → Axis 4.
- Axis 3 and Axis 4 are enclosed with a dashed line: "Disconnection (After Axis 3)".

#### Program example (プログラム例) (8.13 / original p.381-382)

- Disconnect operation (original p.381)

[Figure] Ladder of disconnect operation (labels used). Step numbers: (0), (16), (41), (59).

Mnemonic transcription (label names as in the original; the ladder shows no comments, the comments after ";" give the assigned device shown under the label):

```text
(0)
LDP   bDisconnectCommand
ANI   bDisconnectReq
ANI   bDisconnectExecutionReq
ANI   bDisconnectCompletionCheck
MOV   K3 uSSCNETControlCommand
SET   bDisconnectReq
(16)
LD    bDisconnectReq
MPS
AND=  K0 FX5SSC_1.stSysMntr1_D.wSSCNET_ControlStatus_D     ; U1\G4233
MOV   uSSCNETControlCommand FX5SSC_1.stSysCtrl_D.wSSCNET_ControlCommand_D   ; U1\G5932
MPP
AND=  K1 FX5SSC_1.stSysMntr1_D.wSSCNET_ControlStatus_D     ; U1\G4233
RST   bDisconnectReq
SET   bDisconnectExecutionReq
(41)
LD    bDisconnectExecutionReq
AND=  K-1 FX5SSC_1.stSysMntr1_D.wSSCNET_ControlStatus_D    ; U1\G4233
MOV   K-2 FX5SSC_1.stSysCtrl_D.wSSCNET_ControlCommand_D    ; U1\G5932
RST   bDisconnectExecutionReq
SET   bDisconnectCompletionCheck
(59)
LD    bDisconnectCompletionCheck
AND=  K1 FX5SSC_1.stSysMntr1_D.wSSCNET_ControlStatus_D     ; U1\G4233
RST   bDisconnectCompletionCheck
```

- Contact types read from the figure: at (0), bDisconnectCommand is a rising-edge (↑) contact; bDisconnectReq, bDisconnectExecutionReq and bDisconnectCompletionCheck are b contacts; the others are a contacts.
- At (16), after bDisconnectReq the circuit branches in two: upper "= K0 ...ControlStatus_D" → MOV; lower "= K1 ...ControlStatus_D" → RST bDisconnectReq and SET bDisconnectExecutionReq (parallel outputs). MPS/MPP are used here to express this branch.

- Connect operation (original p.382)

[Figure] Ladder of connect operation (labels used). Step numbers: (0), (17), (35), (53).

```text
(0)
LDP   bConnectCommand
ANI   bConnectReq
ANI   bConnectExecutionReq
ANI   bConnectCompletionCheck
MOV   K-10 uSSCNETControlCommand
SET   bConnectReq
(17)
LD    bConnectReq
AND=  K1 FX5SSC_1.stSysMntr1_D.wSSCNET_ControlStatus_D     ; U1\G4233
MOV   uSSCNETControlCommand FX5SSC_1.stSysCtrl_D.wSSCNET_ControlCommand_D   ; U1\G5932
RST   bConnectReq
SET   bConnectExecutionReq
(35)
LD    bConnectExecutionReq
AND=  K-1 FX5SSC_1.stSysMntr1_D.wSSCNET_ControlStatus_D    ; U1\G4233
MOV   K-2 FX5SSC_1.stSysCtrl_D.wSSCNET_ControlCommand_D    ; U1\G5932
RST   bConnectExecutionReq
SET   bDisconnectCompletionCheck                           ; as printed in the original (要確認)
(53)
LD    bConnectCompletionCheck
AND=  K0 FX5SSC_1.stSysMntr1_D.wSSCNET_ControlStatus_D     ; U1\G4233
RST   bConnectCompletionCheck
```

- Contact types read from the figure: at (0), bConnectCommand is a rising-edge contact; bConnectReq, bConnectExecutionReq and bConnectCompletionCheck are b contacts; the others are a contacts.
- At (35), the SET target is printed as "bDisconnectCompletionCheck" in the original, while (53) resets "bConnectCompletionCheck". This is presumably a misprint in the original (bConnectCompletionCheck intended) (要確認). Transcribed as printed.
- (17) has no branch (one condition "= K1" drives MOV / RST / SET in parallel).

| Classification | Label name | Description |
|---|---|---|
| Module label | FX5SSC_1.stSysMntr1_D.wSSCNET_ControlStatus_D | Axis 1 SSCNET control status |
| Module label | FX5SSC_1.stSysCtrl_D.wSSCNET_ControlCommand_D | Axis 1 SSCNET control command |
| Global label, local label | (below) | Defines the global label or the local label as follows. The settings of Assign (Device/Label) are not required for the label that the assignment device is not set because the unused internal relay and data device are automatically assigned.<br>The following are for local labels. |

*In the original, "Module label" is merged over 2 rows. Expanded to each row.

Local label definition (from the screen image in the original):

| No. | Label Name | Data Type | Class |
|---|---|---|---|
| 1 | bDisconnectCommand | Bit | VAR |
| 2 | bDisconnectReq | Bit | VAR |
| 3 | bDisconnectExecutionReq | Bit | VAR |
| 4 | bDisconnectCompletionCheck | Bit | VAR |
| 5 | bConnectCommand | Bit | VAR |
| 6 | bConnectReq | Bit | VAR |
| 7 | bConnectExecutionReq | Bit | VAR |
| 8 | bConnectCompletionCheck | Bit | VAR |
| 9 | uSSCNETControlCommand | Word [Signed] | VAR |

## 8.14 Servo Transient Transmission Function [FX5-SSC-G] (サーボトランジェント伝送機能[FX5-SSC-G]) (8.14 / original p.383-385)

The "Servo Transient Transmission Function" is a function that reads and writes objects of the device using transient transmission. Transient transmission is suitable for data that does not require reading and writing in a fixed cycle and data with a large size.
For objects that can be read and written using transient transmission, refer to the manual of the device.
In the servo transient transmission function, one point can be set per axis, and changes can be made at any time.

### Control details (制御内容) (8.14 / original p.383-385)

The following parameters and data are used in the "Servo Transient Transmission Function".

#### Extension parameters (拡張パラメータ) (8.14 / original p.383)

n: Axis No. -1

| Setting item | | Setting details/setting value | Default value | Buffer memory address |
|---|---|---|---|---|
| [Pr.512] | Optional SDO 1 | Specifies the object that will perform servo transient transmission.<br>(Bit layout: b31 to b16: Index; b15 to b8: Subindex; b7 to b0: Object size)<br>At reading:<br>Reads the object using SDO Upload of the SLMP. The writing object size [byte] is ignored.<br>And the size of the object that is read will be stored to the request object of optional SDO transfer status.<br>At writing:<br>Writes the object using Download command of the SLMP. The writing object size [byte] can be set to "0x01, 0x02, 0x04, or 0x08" along with the object being written. When the object size is outside the range, the size is considered to be "0x04".<br>Example)<br>When specifying an UNSIGNED32 object with the object index "6099H" and the sub-index "02H", specify as shown below.<br>Reading: "60990200H" (default size)<br>Writing: "6099204H" (size: 4 bytes)<br>Fetch cycle: At request (Servo transient request) | 0 | 128+150n<br>129+150n |

*"6099204H" is as printed in the original (7 digits; presumably "60990204H").
*The bit layout is a figure in the original: upper word b31 to b16 = Index; lower word b15 to b0 split into Subindex (upper byte) and Object size (lower byte).

> **Point**
> - Servo transient processing operates in the series of request sent → response received which is performed in order of the setting numbers.
> - For the specifiable indexes, sub-indexes, and object sizes, refer to the manual of the device. When an object not supported by the device is specified, error completion occurs.

#### Axis control data (transient function) (軸制御データ(トランジェント機能)) (8.14 / original p.384)

n: Axis No. -1

| Setting item | | Setting details/setting value | Default value | Buffer memory address |
|---|---|---|---|---|
| [Cd.160] | Optional SDO transfer request 1 | Requests the servo transient transmission.<br>• Changes to values are not accepted during processing.<br>• Automatically 0 cleared when processing completes.<br>1: Individual read request<br>11: Individual write request<br>Other than above: No request<br>Fetch cycle: Main cycle | 0 | 57520+30n |
| [Cd.164] | Optional SDO transfer data 1 | Stores data up to 8 bytes (4 words) from the top of the buffer memory as follows in accordance with the specified object.<br>(Figure: from the high side "H": 4th word / 3rd word / 2nd word / 1st word (Top of the buffer memory) Storage/setting destination)<br>Example)<br>To write "1234H" and "5678H" from the top of the buffer memory to "Optional SDO transfer result 1", set "H56781234" in G57522.<br>• When reading the object, the read value is stored at normal completion of communication. Values are not updated when an error occurs.<br>• When writing the object, specify the data being written. Do not change the written contents until the processing completes.<br>Fetch cycle: At request (Command request) | 0 | 57522+30n<br>57523+30n<br>57524+30n<br>57525+30n |

#### Axis monitor data (軸モニタデータ) (8.14 / original p.384)

n: Axis No. -1

| Setting item | | Setting details/setting value | Default value | Buffer memory address |
|---|---|---|---|---|
| [Md.160] | Optional SDO transfer result 1 | Stores the response code (SDO Abort code) received from the device in response to the transient request. For details of the code, refer to "Response Code (SDO Abort Code)" in the following manual.<br>[Other manual] MELSEC iQ-F FX5 Motion Module User's Manual (CC-Link IE TSN)<br>"0" is stored when a response code cannot be retrieved because of a communication error, etc.<br>Refresh cycle: At request (Command request) | 0 | 59308+100n<br>59309+100n |
| [Md.164] | Optional SDO transfer status 1 | Stores the processing status of the transient request.<br>• b7 to 0: Response object size (byte)<br>The object size received from the device is stored when the processing completes.<br>• b8: Communicating<br>Turns ON during transient communication.<br>• b9: Communication error detection<br>Turns ON when an error is detected in transient transmission, and remains ON until the transient transmission completes normally.<br>Error causes are shown below.<br>- Standard errors<br>- Error response (SDO Abort code) received from device<br>(Example: When the index, sub-index, or size specified in "[Pr.512] Optional SDO 1" is incorrect.<br>• b10: Not used<br>• b15: Data enabled bit<br>Turns ON at normal completion of the read request. Turns OFF when a read error is detected.<br>Refresh cycle: At request (Command request) | 0 | 59312+100n |

*The header "Setting item / Setting details/setting value" of the monitor data table is as printed in the original.

#### Send/receive timing (送受信タイミング) (8.14 / original p.385)

The send/receive timing for the servo transient transmission is shown below.

- Send/receive timing for individual read/write (at normal operation)

[Figure] Send/receive timing at normal operation (original p.385)
- [Cd.160] Optional SDO transfer request 1: Not request → Write/Read request (single) → Not request (returns at the completion, dashed line).
- [Md.164] Optional SDO transfer status 1, Communicating (b8): turns ON following the request, and turns OFF at the completion.
- At the completion (dashed line): [Md.160] Optional SDO transfer result 1 becomes 0; [Cd.164] Optional SDO transfer data 1 (at reading) becomes "Read data"; Data valid bit (b15) turns ON ("At reading"); Response object size (b0 to b7) (at reading) becomes "Read size".
- [Cd.164] (at writing): "Write data" is held from before the request until after the completion.

- Send/receive timing for individual read/write (when an error occurs)

[Figure] Send/receive timing when an error occurs (original p.385)
- [Cd.160]: Not request → Write/Read request (single) → Not request.
- Communicating (b8): ON following the request, OFF at the completion.
- At the completion: [Md.160] becomes "Other than 0"; Communication error detection (b9) turns ON; [Cd.164] (at reading) "Not updated"; Response object size (b0 to b7) "Not updated"; Data valid bit (b15) stays OFF.
- [Cd.164] (at writing): "Write data" held.

### Precautions (注意事項) (8.14 / original p.385)

Obtains home position data of the driver by the transient transmission function in a driver homing method. Therefore, if reading/writing objects of the device is executed with transient transmission while driver homing is being carried out, the error "ABS Reference Point Read Error" (error code: 1A75H) may occur.

## 8.15 Firmware update function (ファームウェアアップデート機能) (8.15 / original p.386)

This function is used to update firmware of Simple Motion module/Motion module.

### Procedure to update firmware (ファームウェアアップデート手順) (8.15 / original p.386)

#### Firmware update when using GX Works3 (GX Works3を使用したファームウェアアップデート) (8.15 / original p.386)

For the method to update firmware of Simple Motion module/Motion module, refer to "update instruction using engineering tool" in the following manual.
[Other manual] MELSEC iQ-F FX5 User's Manual (Application)

#### LED display at firmware version update (ファームウェアバージョンアップ時のLED表示) (8.15 / original p.386)

□: OFF, ■: ON, ●: Fast flashing (200 ms interval), ▲: Slow flashing (1000 ms interval)

| LED | Description | Remedy |
|---|---|---|
| POWER ■<br>RUN ▲<br>ERROR ▲ | Firmware version updating | Turn ON→ OFF or reset the CPU module and then execute firmware version update. |
| POWER ■<br>RUN ▲<br>ERROR ▲ | Firmware version update executing | — |
| POWER ■<br>RUN □<br>ERROR □ | Firmware version update complete successfully | Reset the system and then check if the CPU module can be RUN/STOP correctly and BFM can be monitored on the intelligent function modules correctly. |
| POWER ■<br>RUN □<br>ERROR ● | Firmware version update error complete | Turn ON → OFF the power supply of the CPU module or reset the system and then execute firmware version update again. |

*In the original, the LED cell "POWER ■ / RUN ▲ / ERROR ▲" is merged over the 2 rows "Firmware version updating" / "Firmware version update executing". Expanded to each row.

## 8.16 Hot line forced stop function (ホットライン強制停止機能) (8.16 / original p.387-388)

This function is used to execute deceleration stop safety for other axes when the servo alarm occurs in the servo amplifier MR-JE-B(F).

### Control details (制御内容) (8.16 / original p.387)

The hot line forced stop function is set in the servo parameter. This function can execute deceleration stop for other axes without via Simple Motion module by notifying the servo alarm occurrence. For details, refer to the following.
[Other manual] MR-JE-_B(F) Servo Amplifier Instruction Manual
This function is enabled at the MR-JE-B(F) factory-set. To disable this function, set "1: Disabled" in the servo parameter "Hot line forced stop function Hot line forced stop function selection (PA27)".
Also, when the system is configured with MR-JE-B(F) and MR-J4(W)-B, this function can execute deceleration stop for MR-J4(W)-B at the servo alarm occurrence in MR-JE-B(F). To execute deceleration stop for MR-J4(W)-B, set "2: Enabled" in the servo parameter of MR-J4(W)-B "Hot line forced stop function Deceleration to stop selection (PA27)". ("0: Disabled" is set at factory-set.)
The following shows the setting value of the servo parameter (PA27) and the operation of servo amplifier.

[MR-JE-B(F)]

| Setting value of "Hot line forced stop function Hot line forced stop function selection (PA27)" | Output hot line | Deceleration stop when receiving the hot line signal |
|---|---|---|
| 0: Enabled (Initial value) | Enabled | Enabled |
| 1: Disabled | Disabled | Disabled |

[MR-J4(W)-B]

| Setting value of "Hot line forced stop function Deceleration to stop selection (PA27)" | Output hot line | Deceleration stop when receiving the hot line signal |
|---|---|---|
| 0: Disabled (Initial value) | Disabled | Disabled |
| 2: Enabled | Disabled | Enabled |

Use the software version that supports the hot line forced stop function for the servo amplifier to use the hot line forced stop function.
The following table shows the software version of servo amplifier that supports the hot line forced stop function.

| Servo amplifier type | Software version |
|---|---|
| MR-J4(W)-B | B7 or later |
| MR-JE-B(F) | B6 or later |

*1 The servo amplifier except above does not support the hot line forced stop function. Therefore, it does not output the hot line or execute deceleration stop by receiving the hot line signal.
(*As printed in the original, the reference mark "*1" does not appear in the table.)

### Precautions during control (制御上の注意事項) (8.16 / original p.387-388)

- The servo warning "Controller forced stop warning" (warning No.: E7) occurs in the axis where the hot line forced stop function executes deceleration stop.
- To clear the servo warning "Controller forced stop warning" (warning No.: E7) occurred by the hot line forced stop function, set "1" in "[Cd.5] Axis error reset" for each axis after the factor is removed in the axis where the servo alarm occurred. Even if "1" is set in "[Cd.5] Axis error reset" before the factor is not removed, the servo warning "Controller forced stop warning" (warning No.: E7) is not cleared.
- The following shows the timing chart at the servo alarm occurrence.

[Figure] Timing chart at the servo alarm occurrence (original p.388)
- Axis in which the servo alarm occurred (axis 2): Positioning control (trapezoid); at 1) "[Md.108] Servo status1 (b7: Servo alarm)" turns ON during constant speed and the speed drops to 0 (stop with dynamic brake); at 3) b7 turns OFF.
- Axis in which the servo alarm does not occur (axis 1): Positioning control (trapezoid); at 2) (notification from axis 2, dashed arrow) "[Md.108] Servo status1 (b15: Servo warning)" turns ON and the axis decelerates to stop.
- "[Cd.5] Axis error reset" of axis 1 pulses ON (after 3)); at 4) b15 of axis 1 turns OFF.

1) The servo alarm occurs in axis 2 and the servo motor stops with dynamic brake.
2) The notification from the alarm occurrence axis is received in axis 1. The servo warning ("[Md.108] servo status1": b15) is turned ON and the deceleration stop is executed.
3) The servo alarm ("[Md.108] Servo status1": b7) is turned OFF by removing the servo alarm factor of axis 2.
4) The warning ("[Md.108] Servo status1": b15) is turned OFF by "[Cd.5] Axis error reset" of axis 1.
