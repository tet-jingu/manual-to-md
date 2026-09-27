# 11 DATA USED FOR POSITIONING CONTROL (位置決め制御に使用するデータ) (Chapter 11 / original p.400-623)

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

## Conversion range (変換範囲表 / original p.400-623)

| Original page | Section | Handling |
|---|---|---|
| p.400 | 11 DATA USED FOR POSITIONING CONTROL (chapter introduction) | Full text |
| p.400-402 | 11.1 Parameters and data required for control (setting data / monitor data / control data) | Full text |
| p.402 | 11.1 Setting items for servo network configuration parameters [FX5-SSC-G] | Full text |
| p.403-404 | 11.1 Setting items for common parameters | Full text |
| p.405-412 | 11.1 Setting items for positioning parameters (home position return / major positioning / manual / expansion control, checking) | Full text |
| p.413 | 11.1 Setting items for home position return parameters | Full text |
| p.414 | 11.1 Setting items for extended parameters / servo parameters [FX5-SSC-S] | Full text |
| p.415-416 | 11.1 Setting items for positioning data | Full text |
| p.417 | 11.1 Setting items for block start data / condition data | Full text |
| p.418-420 | 11.1 Types and roles of monitor data | Full text |
| p.421-423 | 11.1 Types and roles of control data | Full text |
| p.424-427 | 11.2 List of Buffer Memory Addresses: intro, [Basic setting] | Full text |
| p.427-430 | 11.2 [Monitor data] (System monitor data, Axis monitor data) | Full text |
| p.430-432 | 11.2 [Control data] (System control data, Axis control data, Axis control data (transient function) [FX5-SSC-G]) | Full text |
| p.433 | 11.2 [Positioning data] | Full text |
| p.434 | 11.2 [Block start data] | Full text |
| p.435-443 | 11.2 Servo parameters (Servo parameters [FX5-SSC-S]) | Full text |
| p.444 | 11.2 Mark detection function | Full text |
| p.445 | 11.2 Link device external signal assignment [FX5-SSC-G] | Full text |
| p.446-447 | 11.3 Basic Setting: intro, Servo network configuration parameters [FX5-SSC-G] | Full text |
| p.448-455 | 11.3 Common parameters | Full text |
| p.456-460 | 11.3 Basic parameters1 | Full text |
| p.461 | 11.3 Basic parameters2 | Full text |
| p.462-471 | 11.3 Detailed parameters1 | Full text |
| p.472-484 | 11.3 Detailed parameters2 (program example of [Pr.84] included) | Full text |
| p.485-488 | 11.3 Home position return basic parameters ([Pr.43] to [Pr.48]) | Full text |
| p.489-493 | 11.3 Home position return detailed parameters ([Pr.50] to [Pr.57]) | Full text |
| p.494-497 | 11.3 Extended parameters ([Pr.91] to [Pr.94], [Pr.512], [Pr.591] to [Pr.594]) | Full text |
| p.498 | 11.3 Servo parameters [FX5-SSC-S] (Servo series [Pr.100], Parameters of MR-J5(W)-B, Parameters of MR-J4(W)-B/MR-JE-B(F)/MR-J3(W)-B) | Full text |
| p.499-510 | 11.4 Positioning Data ([Da.1] to [Da.10], [Da.20] to [Da.22]) | Full text |
| p.511-513 | 11.5 Block Start Data ([Da.11] to [Da.14]) | Full text |
| p.514-519 | 11.6 Condition Data ([Da.15] to [Da.19], [Da.23] to [Da.26]) | Full text |
| p.520-528 | 11.7 Monitor Data: intro, System monitor data ([Md.3] to [Md.141]) | Full text |
| p.529-562 | 11.7 Axis monitor data ([Md.20] to [Md.514]) | Full text |
| p.563-570 | 11.8 Control Data: intro, System control data ([Cd.1] to [Cd.191]) | Full text |
| p.571-601 | 11.8 Axis control data ([Cd.3] to [Cd.184]) | Full text |
| p.602 | 11.8 Axis control data (transient function) [FX5-SSC-G] ([Cd.160], [Cd.164]) | Full text |
| p.603-605 | 11.9 Memory Configuration and Data Process: intro, Configuration and roles, Details of areas | Full text |
| p.606-607 | 11.9 Buffer memory area configuration | Full text |
| p.608 | 11.9 Timing for data transfers | Full text |
| p.609-614 | 11.9 Data transmission process: (1) to (10) Transmitting servo parameter [FX5-SSC-S] | Full text |
| p.615-616 | 11.9 (10) Transmitting servo parameter [FX5-SSC-G] | Full text |
| p.617-620 | 11.9 Data transmission patterns [FX5-SSC-S] (figures) | Full text (figures written out) |
| p.621-623 | 11.9 Data transmission patterns [FX5-SSC-G] (figures) | Full text (figures written out) |

## Table of Contents (目次)

- 11 DATA USED FOR POSITIONING CONTROL (位置決め制御に使用するデータ)
- 11.1 Types of Data (データの種類)
- 11.2 List of Buffer Memory Addresses (バッファメモリアドレス一覧)
- 11.3 Basic Setting (基本設定)
- 11.4 Positioning Data (位置決めデータ)
- 11.5 Block Start Data (ブロック始動データ)
- 11.6 Condition Data (条件データ)
- 11.7 Monitor Data (モニタデータ)
- 11.8 Control Data (制御データ)
- 11.9 Memory Configuration and Data Process (メモリ構成とデータ処理)

---

## 11 DATA USED FOR POSITIONING CONTROL (位置決め制御に使用するデータ) (Chapter 11 / original p.400)

The parameters and data used to carry out positioning control with the Simple Motion module/Motion module are explained in this chapter.
With the positioning system using the Simple Motion module/Motion module, the various parameters and data explained in this chapter are used for control. The parameters and data include parameters set according to the device configuration, such as the system configuration, and parameters and data set according to each control.
Read this section thoroughly and make settings according to each control or application.

## 11.1 Types of Data (データの種類) (11.1 / original p.400-423)

### Parameters and data required for control (制御に必要なパラメータとデータ) (11.1 / original p.400-402)

The parameters and data required to carry out control with the Simple Motion module/Motion module include the "setting data", "monitor data" and "control data" shown below.

#### Setting data (設定データ) (11.1 / original p.400-401)

The data is set beforehand according to the machine and application. Set the data with programs or engineering tools. The data set for the buffer memory can also be saved in the flash ROM or internal memory (nonvolatile) in the Simple Motion module/Motion module.

> **Restriction**
> The setting data can be backed up only in the flash ROM/internal memory (nonvolatile) of the Simple Motion module/Motion module. It cannot be backed up in the CPU module and the SD memory card mounted to the CPU module.

The setting data is classified as follows. (original p.400-401)

| Classification | Item | Item (sub-division) | Description |
|---|---|---|---|
| Parameters | Servo network configuration parameters [FX5-SSC-G] | — | Parameters for the network.<br>Perform settings for the devices used and the network according to the system configuration. |
| Parameters | Common parameters | — | Parameters that are independent of axes and related to the overall system.<br>Set according to the system configuration when the system is started up. |
| Parameters | Positioning parameters | Basic parameters 1*1 | Set according to the machine and applicable motor when the system is started up. |
| Parameters | Positioning parameters | Basic parameters 2 | Set according to the machine and applicable motor when the system is started up. |
| Parameters | Positioning parameters | Detailed parameters 1 | Set according to the system configuration when the system is started up. |
| Parameters | Positioning parameters | Detailed parameters 2*2 | Set according to the system configuration when the system is started up. |
| Parameters | Home position return parameters | Home position return basic parameters | Set the values required for carrying out home position return control. |
| Parameters | Home position return parameters | Home position return detailed parameters | Set the values required for carrying out home position return control. |
| Parameters | Extended parameters | — | Set according to the system configuration when the system is started up. |
| Parameters | Link device external signal assignment parameters [FX5-SSC-G] | — | Set according to the network configuration when the system is started up. |
| Servo parameters [FX5-SSC-S] | Servo amplifier parameters<br>([Pr.100], PA, PB, PC, PD, PE, PS, PF, Po, PL) | — | Set the data that is determined by the specification of the servo being used when the system is started up. |
| Mark detection | Mark detection setting parameters | — | Set the parameters for mark detection. |
| Positioning data | Positioning data | — | Set the data for "major positioning control". |
| Block start data | Block start data | — | Set the block start data for "high-level positioning control". |
| Block start data | Condition data | — | Set the condition data for "high-level positioning control". |
| Block start data | Memo data | — | Set the condition judgment values for the condition data used in "high-level positioning control". |
| Synchronous control parameters | Servo input axis parameters | — | Set the parameters for synchronous control. |
| Synchronous control parameters | Synchronous encoder axis parameters | — | Set the parameters for synchronous control. |
| Synchronous control parameters | Synchronous encoder axis parameters via link device [FX5-SSC-G] | — | Set the parameters for synchronous control. |
| Synchronous control parameters | Command generation axis parameters | — | Set the parameters for synchronous control. |
| Synchronous control parameters | Command generation axis positioning data | — | Set the parameters for synchronous control. |
| Synchronous control parameters | Synchronous parameters | — | Set the parameters for synchronous control. |
| Cam data | Cam data | — | Set the cam data to be used for synchronous control. |

*In the original, the table spans p.400 (Parameters to Memo data) and p.401 (Synchronous control parameters and Cam data). The "Classification" cells (Parameters / Block start data / Synchronous control parameters), the "Item" cells (Positioning parameters / Home position return parameters) and the "Description" cells (Basic parameters 1 and 2; Detailed parameters 1 and 2; Home position return basic and detailed parameters; the 6 Synchronous control parameters rows) are merged. Expanded to each row. The original "Item" column is split into two levels only for Positioning parameters and Home position return parameters; the lower level is shown here as "Item (sub-division)", and "—" is used where the original has no split. "Cam data" is one cell spanning the Classification and Item columns in the original (expanded to both columns here).

*1 If the setting of the basic parameters 1 is incorrect, the rotation direction may be reversed, or no operation may take place.
*2 Detailed parameters 2 are data items for using the functions of Simple Motion module/Motion module to the fullest. Set as required.

- The following methods are available for data setting. In this manual, the method using the engineering tool will be explained.
  - Set using the engineering tool.
  - Create the program for data setting and execute it.
- The basic parameters 1, detailed parameters 1, home position return parameters, "[Pr.83] Speed control 10 × multiplier setting for degree axis", "[Pr.90] Operation setting for speed-torque control mode", "[Pr.95] External command signal selection", "[Pr.122] Manual pulse generator speed limit mode", "[Pr.123] Manual pulse generator speed limit value", "[Pr.127] Speed limit value input selection at control mode switching" and common parameters (excluding "[Pr.97] SSCNET setting") become valid when the "[Cd.190] PLC READY" turns from OFF to ON.
- The basic parameters 2, detailed parameters 2 (excluding "[Pr.83] Speed control 10 × multiplier setting for degree axis", "[Pr.90] Operation setting for speed-torque control mode", "[Pr.95] External command signal selection", "[Pr.122] Manual pulse generator speed limit mode", "[Pr.123] Manual pulse generator speed limit value", and "[Pr.127] Speed limit value input selection at control mode switching") become valid immediately when they are written to the buffer memory, regardless of the state of the "[Cd.190] PLC READY".
- Even when the "[Cd.190] PLC READY" is ON, the values or contents of the following can be changed: basic parameters 2, detailed parameters 2, positioning data, and block start data.
- The servo parameter is transmitted from the Simple Motion module/Motion module to the servo amplifier when the initialized communication carried out after the power supply is turned ON or the CPU module is reset. The power supply is turned ON or the CPU module is reset after writing servo parameter in flash ROM of Simple Motion module/Motion module if the servo parameter is transmitted to the servo amplifier.
- The only valid data assigned to basic parameter 2, detailed parameter 2, positioning data or block start data are the data read at the moment when a positioning or JOG operation is started. Once the operation has started, any modification to the data is ignored. Exceptionally, however, modifications to the following are valid even when they are made during a positioning operation: acceleration time 0 to 3, deceleration time 0 to 3, and external command function.

| Setting data that can be changed during operation | Details |
|---|---|
| Acceleration time 0 to 3, deceleration time 0 to 3 | Positioning data are pre-read and pre-analyzed. Modifications to the data four or more steps after the current step are valid. |
| External command function selection | The value at the time of detection is valid. |

> **Point**
> - The "setting data" is created for each axis.
> - The "setting data" parameters have determined default values, and are set to the default values before shipment from the factory. (Parameters related to axes that are not used are left at the default value.)
> - The "setting data" can be initialized with the engineering tool or the program.
> - It is recommended to set the "setting data" with the engineering tool. The program for data setting is complicated and many devices must be used. This will increase the scan time.

#### Monitor data (モニタデータ) (11.1 / original p.402)

The data indicates the control status. The data is stored in the buffer memory. Monitor the data as necessary.
The monitor data is classified as follows.

| Item | Description |
|---|---|
| System monitor data | Monitors the specifications and the operation history of Simple Motion module/Motion module. |
| Axis monitor data | Monitors the data related to the operating axis, such as the current position and speed. |
| Synchronous control data | Monitors the data for synchronous control. |
| Mark detection monitor data | Monitors the data for mark detection. |

- The following methods are available for data monitoring:
  - Set using the engineering tool.
  - Create the program for monitoring and execute it.
- In this manual, the method using the engineering tool will be explained.

#### Control data (制御データ) (11.1 / original p.402)

The data is used by users to control the positioning system.
The control data is classified as follows.

| Item | Description |
|---|---|
| System control data | Writes/initializes the "positioning data" in the module.<br>Sets the setting for operation of all axes. |
| Axis control data | Makes settings related to the operation, and controls the speed change during operation, and stops/restarts the operation for each axis.<br>Output signals (axis stop signal, JOG start signal, execution prohibition flag, and axis start) from the CPU module to the Simple Motion module/Motion module. |
| Synchronous control data | Sets the data for synchronous control. |
| Mark detection control data | Sets the data for mark detection control. |

- Control using the control data is carried out with the program. "[Cd.41] Deceleration start flag valid" is valid for only the value at the time when the "[Cd.190] PLC READY" turns from OFF to ON.

### Setting items for servo network configuration parameters [FX5-SSC-G] (サーボネットワーク構成パラメータの設定項目[FX5-SSC-G]) (11.1 / original p.402)

The setting items for the "servo network configuration parameters" are shown below.

| No. | Servo network configuration parameter | Remark |
|---|---|---|
| [Pr.101] | Virtual servo amplifier setting | Set whether or not to use the axis as a virtual servo amplifier axis. The value is imported when the power is turned ON. |
| [Pr.140] | Driver command discard detection setting | When bit 12 in "[Md.117] Statusword" of the drive unit turns ON → OFF while operating an actual axis, the error "Driver command discard detection" (error code: 1BE6H) is outputted before the motor stops to stop the command. |
| [Pr.141] | IP address | Specify the IP address. |
| [Pr.142] | Multidrop number | When one station includes multiple logic axes, specify the No. in order to distinguish logic axes. |

*In the original, the "Servo network configuration parameter" header spans the No. column and the name column (split here as "No." / "Servo network configuration parameter").

### Setting items for common parameters (共通パラメータの設定項目) (11.1 / original p.403-404)

The setting items for the "common parameters" are shown below. The "common parameters" are independent of axes and related to the overall system.
◎: Always set
○: Set as required ("—" when not required)
—: Setting not required (When the value is the default value or within the setting range, there is no problem.)

(original p.403, upper table)

| No. | Common parameter | Home position return control | Major positioning control / Position control / 1-axis linear control, 2/3/4-axis linear interpolation control | Major positioning control / Position control / 1/2/3/4-axis fixed-feed control | Major positioning control / Position control / 2-axis circular interpolation control |
|---|---|---|---|---|---|
| [Pr.24] | Manual pulse generator/Incremental synchronous encoder input selection [FX5-SSC-S] | — | — | — | — |
| [Pr.82] | Forced stop valid/invalid selection | ○ | ○ | ○ | ○ |
| [Pr.89] | Manual pulse generator/Incremental synchronous encoder input type selection [FX5-SSC-S] | — | — | — | — |
| [Pr.96] | Operation cycle setting [FX5-SSC-S] | — | — | — | — |
| [Pr.97] | SSCNET setting [FX5-SSC-S] | — | — | — | — |
| [Pr.150] | Input terminal logic selection [FX5-SSC-S] | ○ | ○ | ○ | ○ |
| [Pr.151] | Manual pulse generator/Incremental synchronous encoder input logic selection [FX5-SSC-S] | — | — | — | — |
| [Pr.152] | Maximum number of control axes [FX5-SSC-G] | ○ | ○ | ○ | ○ |
| [Pr.156] | Manual pulse generator smoothing time constant [FX5-SSC-G] | — | — | — | — |

*In the original, the column header is 3 levels: "Major positioning control" > "Position control" > each control. Written in one header cell per column, levels separated by " / ". The "Common parameter" header spans the No. column and the name column.

(original p.403, lower table)

| No. | Common parameter | Major positioning control / 1 to 4 axis speed control | Major positioning control / Speed-position or position-speed control | Major positioning control / Other control / Current value changing | Major positioning control / Other control / JUMP instruction, NOP instruction, LOOP to LEND |
|---|---|---|---|---|---|
| [Pr.24] | Manual pulse generator/Incremental synchronous encoder input selection [FX5-SSC-S] | — | — | — | — |
| [Pr.82] | Forced stop valid/invalid selection | ○ | ○ | ○ | ○ |
| [Pr.89] | Manual pulse generator/Incremental synchronous encoder input type selection [FX5-SSC-S] | — | — | — | — |
| [Pr.96] | Operation cycle setting [FX5-SSC-S] | — | — | — | — |
| [Pr.97] | SSCNET setting [FX5-SSC-S] | — | — | — | — |
| [Pr.150] | Input terminal logic selection [FX5-SSC-S] | ○ | ○ | ○ | ○ |
| [Pr.151] | Manual pulse generator/Incremental synchronous encoder input logic selection [FX5-SSC-S] | — | — | — | — |
| [Pr.152] | Maximum number of control axes [FX5-SSC-G] | ○ | ○ | ○ | ○ |
| [Pr.156] | Manual pulse generator smoothing time constant [FX5-SSC-G] | — | — | — | — |

*In the original, the column header is multi-level ("Major positioning control" > "1 to 4 axis speed control" / "Speed-position or position-speed control" / "Other control" > each control). Written in one header cell per column, levels separated by " / ".

(original p.404)

| No. | Common parameter | Manual control / Manual pulse generator operation | Manual control / Inching operation | Manual control / JOG operation | Expansion control / Speed-torque control | Related sub function |
|---|---|---|---|---|---|---|
| [Pr.24] | Manual pulse generator/Incremental synchronous encoder input selection [FX5-SSC-S] | ◎ | — | — | — | — |
| [Pr.82] | Forced stop valid/invalid selection | ○ | ○ | ○ | ○ | →Page 254 Forced stop function |
| [Pr.89] | Manual pulse generator/Incremental synchronous encoder input type selection [FX5-SSC-S] | ◎ | — | — | — | — |
| [Pr.96] | Operation cycle setting [FX5-SSC-S] | — | — | — | — | — |
| [Pr.97] | SSCNET setting [FX5-SSC-S] | — | — | — | — | — |
| [Pr.150] | Input terminal logic selection [FX5-SSC-S] | ○ | ○ | ○ | ○ | — |
| [Pr.151] | Manual pulse generator/Incremental synchronous encoder input logic selection [FX5-SSC-S] | ◎ | — | — | — | — |
| [Pr.152] | Maximum number of control axes [FX5-SSC-G] | ○ | ○ | ○ | ○ | — |
| [Pr.156] | Manual pulse generator smoothing time constant [FX5-SSC-G] | ○ | — | — | — | — |

*In the original, the column header is 2 levels ("Manual control" > 3 operations; "Expansion control" > "Speed-torque control"). Written in one header cell per column, levels separated by " / ".

### Setting items for positioning parameters (位置決め用パラメータの設定項目) (11.1 / original p.405-412)

The setting items for the "positioning parameters" are shown below. The "positioning parameters" are set for each axis for all controls achieved by the Simple Motion module/Motion module.

#### Home position return control (原点復帰制御) (11.1 / original p.405-406)

◎: Always set, ○: Set as required ("—" when not required), △: Setting restricted,
—: Setting not required (When the value is the default value or within the setting range, there is no problem.)

(original p.405)

| Classification | Positioning parameter | Home position return control |
|---|---|---|
| Basic parameters 1 | [Pr.1] Unit setting | ◎ |
| Basic parameters 1 | [Pr.2] Number of pulses per rotation (AP) (Unit: pulse) | ◎ |
| Basic parameters 1 | [Pr.3] Movement amount per rotation (AL) | ◎ |
| Basic parameters 1 | [Pr.4] Unit magnification (AM) | ◎ |
| Basic parameters 1 | [Pr.7] Bias speed at start | ○ |
| Basic parameters 2 | [Pr.8] Speed limit value | ◎ |
| Basic parameters 2 | [Pr.9] Acceleration time 0 | ◎ |
| Basic parameters 2 | [Pr.10] Deceleration time 0 | ◎ |
| Detailed parameters 1 | [Pr.11] Backlash compensation amount | ○ |
| Detailed parameters 1 | [Pr.12] Software stroke limit upper limit value | — |
| Detailed parameters 1 | [Pr.13] Software stroke limit lower limit value | — |
| Detailed parameters 1 | [Pr.14] Software stroke limit selection | — |
| Detailed parameters 1 | [Pr.15] Software stroke limit valid/invalid setting | — |
| Detailed parameters 1 | [Pr.16] Command in-position width | — |
| Detailed parameters 1 | [Pr.17] Torque limit setting value | △ |
| Detailed parameters 1 | [Pr.18] M code ON signal output timing | — |
| Detailed parameters 1 | [Pr.19] Speed switching mode | — |
| Detailed parameters 1 | [Pr.20] Interpolation speed designation method | — |
| Detailed parameters 1 | [Pr.21] Command position value during speed control | — |
| Detailed parameters 1 | [Pr.22] Input signal logic selection | ◎ |
| Detailed parameters 1 | [Pr.81] Speed-position function selection | — |
| Detailed parameters 1 | [Pr.116] FLS signal selection | ○ |
| Detailed parameters 1 | [Pr.117] RLS signal selection | ○ |
| Detailed parameters 1 | [Pr.118] DOG signal selection | ○ |
| Detailed parameters 1 | [Pr.119] STOP signal selection | ○ |

*In the original, the "Classification" cells (Basic parameters 1 / Basic parameters 2 / Detailed parameters 1 / Detailed parameters 2) are merged. Expanded to each row. The original header "Positioning parameter" spans the Classification column and the parameter column.

(original p.406)

| Classification | Positioning parameter | Home position return control |
|---|---|---|
| Detailed parameters 2 | [Pr.25] Acceleration time 1 | ○ |
| Detailed parameters 2 | [Pr.26] Acceleration time 2 | ○ |
| Detailed parameters 2 | [Pr.27] Acceleration time 3 | ○ |
| Detailed parameters 2 | [Pr.28] Deceleration time 1 | ○ |
| Detailed parameters 2 | [Pr.29] Deceleration time 2 | ○ |
| Detailed parameters 2 | [Pr.30] Deceleration time 3 | ○ |
| Detailed parameters 2 | [Pr.31] JOG speed limit value | — |
| Detailed parameters 2 | [Pr.32] JOG operation acceleration time selection | — |
| Detailed parameters 2 | [Pr.33] JOG operation deceleration time selection | — |
| Detailed parameters 2 | [Pr.34] Acceleration/deceleration process selection | ○ |
| Detailed parameters 2 | [Pr.35] S-curve ratio | ○ |
| Detailed parameters 2 | [Pr.36] Sudden stop deceleration time | ○ |
| Detailed parameters 2 | [Pr.37] Stop group 1 sudden stop selection | ○ |
| Detailed parameters 2 | [Pr.38] Stop group 2 sudden stop selection | ○ |
| Detailed parameters 2 | [Pr.39] Stop group 3 sudden stop selection | ○ |
| Detailed parameters 2 | [Pr.40] Positioning complete signal output time | — |
| Detailed parameters 2 | [Pr.41] Allowable circular interpolation error width | — |
| Detailed parameters 2 | [Pr.42] External command function selection | ○ |
| Detailed parameters 2 | [Pr.83] Speed control 10 × multiplier setting for degree axis | ○ |
| Detailed parameters 2 | [Pr.84] Restart allowable range when servo OFF to ON | ○ |
| Detailed parameters 2 | [Pr.90] Operation setting for speed-torque control mode | — |
| Detailed parameters 2 | [Pr.95] External command signal selection | ○ |
| Detailed parameters 2 | [Pr.112] Servo OFF command valid/invalid setting [FX5-SSC-G] | — |
| Detailed parameters 2 | [Pr.122] Manual pulse generator speed limit mode [FX5-SSC-G] | — |
| Detailed parameters 2 | [Pr.123] Manual pulse generator speed limit value [FX5-SSC-G] | — |
| Detailed parameters 2 | [Pr.127] Speed limit value input selection at control mode switching | — |

*In the original, the "Classification" cells (Basic parameters 1 / Basic parameters 2 / Detailed parameters 1 / Detailed parameters 2) are merged. Expanded to each row. The original header "Positioning parameter" spans the Classification column and the parameter column.

#### Major positioning control (主要な位置決め制御) (11.1 / original p.407-408)

◎: Always set, ○: Set as required ("—" when not required), △: Setting restricted,
—: Setting not required (When the value is the default value or within the setting range, there is no problem.)

(original p.407)

| Classification | Positioning parameter | Major positioning control / Position control / 1-axis linear control, 2/3/4-axis linear interpolation control | Major positioning control / Position control / 1-axis fixed-feed control, 2/3/4-axis fixed-feed control | Major positioning control / Position control / 2-axis circular interpolation control | Major positioning control / 1 to 4 axis speed control | Major positioning control / Speed-position or position-speed control | Major positioning control / Other control / Current value changing | Major positioning control / Other control / JUMP instruction, NOP instruction, LOOP to LEND |
|---|---|---|---|---|---|---|---|---|
| Basic parameters 1 | [Pr.1] Unit setting | ◎ | ◎ | △ | ◎ | ◎ | ◎ | ◎ |
| Basic parameters 1 | [Pr.2] Number of pulses per rotation (AP) (Unit: pulse) | ◎ | ◎ | ◎ | ◎ | ◎ | ◎ | ◎ |
| Basic parameters 1 | [Pr.3] Movement amount per rotation (AL) | ◎ | ◎ | ◎ | ◎ | ◎ | ◎ | ◎ |
| Basic parameters 1 | [Pr.4] Unit magnification (AM) | ◎ | ◎ | ◎ | ◎ | ◎ | ◎ | ◎ |
| Basic parameters 1 | [Pr.7] Bias speed at start | ○ | ○ | ○ | ○ | ○ | — | — |
| Basic parameters 2 | [Pr.8] Speed limit value | ◎ | ◎ | ◎ | ◎ | ◎ | — | — |
| Basic parameters 2 | [Pr.9] Acceleration time 0 | ◎ | ◎ | ◎ | ◎ | ◎ | — | — |
| Basic parameters 2 | [Pr.10] Deceleration time 0 | ◎ | ◎ | ◎ | ◎ | ◎ | — | — |
| Detailed parameters 1 | [Pr.11] Backlash compensation amount | ○ | ○ | ○ | ○ | ○ | — | — |
| Detailed parameters 1 | [Pr.12] Software stroke limit upper limit value | ○ | ○ | ○ | ○ | ○ | ○ | — |
| Detailed parameters 1 | [Pr.13] Software stroke limit lower limit value | ○ | ○ | ○ | ○ | ○ | ○ | — |
| Detailed parameters 1 | [Pr.14] Software stroke limit selection | ○ | ○ | ○ | ○ | ○ | ○ | — |
| Detailed parameters 1 | [Pr.15] Software stroke limit valid/invalid setting | — | — | — | — | — | — | — |
| Detailed parameters 1 | [Pr.16] Command in-position width | ○ | ○ | ○ | — | ○ | — | — |
| Detailed parameters 1 | [Pr.17] Torque limit setting value | ○ | ○ | ○ | ○ | ○ | — | — |
| Detailed parameters 1 | [Pr.18] M code ON signal output timing | ○ | ○ | ○ | ○ | ○ | ○ | — |
| Detailed parameters 1 | [Pr.19] Speed switching mode | ○ | ○ | ○ | — | — | — | — |
| Detailed parameters 1 | [Pr.20] Interpolation speed designation method | △ | △ | △ | △ | — | — | — |
| Detailed parameters 1 | [Pr.21] Command position value during speed control | — | — | — | ○ | ○ | — | — |
| Detailed parameters 1 | [Pr.22] Input signal logic selection | ◎ | ◎ | ◎ | ◎ | ◎ | ◎ | ◎ |
| Detailed parameters 1 | [Pr.81] Speed-position function selection | — | — | — | — | ◎ | — | — |
| Detailed parameters 1 | [Pr.116] FLS signal selection | ○ | ○ | ○ | ○ | ○ | — | — |
| Detailed parameters 1 | [Pr.117] RLS signal selection | ○ | ○ | ○ | ○ | ○ | — | — |
| Detailed parameters 1 | [Pr.118] DOG signal selection | — | — | — | — | ○ | — | — |
| Detailed parameters 1 | [Pr.119] STOP signal selection | ○ | ○ | ○ | ○ | ○ | ○ | ○ |

*In the original, the "Classification" cells (Basic parameters 1 / Basic parameters 2 / Detailed parameters 1 / Detailed parameters 2) are merged. Expanded to each row. The original header "Positioning parameter" spans the Classification column and the parameter column. The column header is multi-level in the original ("Major positioning control" > "Position control" / "1 to 4 axis speed control" / "Speed-position or position-speed control" / "Other control" > each control); written in one header cell per column, levels separated by " / ". In the first and second columns the two control names are printed on separate lines in one cell (joined with ", " here).

(original p.408)

| Classification | Positioning parameter | Major positioning control / Position control / 1-axis linear control, 2/3/4-axis linear interpolation control | Major positioning control / Position control / 1-axis fixed-feed control, 2/3/4-axis fixed-feed control | Major positioning control / Position control / 2-axis circular interpolation control | Major positioning control / 1 to 4 axis speed control | Major positioning control / Speed-position or position-speed control | Major positioning control / Other control / Current value changing | Major positioning control / Other control / JUMP instruction, NOP instruction, LOOP to LEND |
|---|---|---|---|---|---|---|---|---|
| Detailed parameters 2 | [Pr.25] Acceleration time 1 | ○ | ○ | ○ | ○ | ○ | — | — |
| Detailed parameters 2 | [Pr.26] Acceleration time 2 | ○ | ○ | ○ | ○ | ○ | — | — |
| Detailed parameters 2 | [Pr.27] Acceleration time 3 | ○ | ○ | ○ | ○ | ○ | — | — |
| Detailed parameters 2 | [Pr.28] Deceleration time 1 | ○ | ○ | ○ | ○ | ○ | — | — |
| Detailed parameters 2 | [Pr.29] Deceleration time 2 | ○ | ○ | ○ | ○ | ○ | — | — |
| Detailed parameters 2 | [Pr.30] Deceleration time 3 | ○ | ○ | ○ | ○ | ○ | — | — |
| Detailed parameters 2 | [Pr.31] JOG speed limit value | — | — | — | — | — | — | — |
| Detailed parameters 2 | [Pr.32] JOG operation acceleration time selection | — | — | — | — | — | — | — |
| Detailed parameters 2 | [Pr.33] JOG operation deceleration time selection | — | — | — | — | — | — | — |
| Detailed parameters 2 | [Pr.34] Acceleration/deceleration process selection | ○ | ○ | ○ | ○ | ○ | — | — |
| Detailed parameters 2 | [Pr.35] S-curve ratio | ○ | ○ | ○ | ○ | ○ | — | — |
| Detailed parameters 2 | [Pr.36] Sudden stop deceleration time | ○ | ○ | ○ | ○ | ○ | — | — |
| Detailed parameters 2 | [Pr.37] Stop group 1 sudden stop selection | ○ | ○ | ○ | ○ | ○ | — | — |
| Detailed parameters 2 | [Pr.38] Stop group 2 sudden stop selection | ○ | ○ | ○ | ○ | ○ | — | — |
| Detailed parameters 2 | [Pr.39] Stop group 3 sudden stop selection | ○ | ○ | ○ | ○ | ○ | — | — |
| Detailed parameters 2 | [Pr.40] Positioning complete signal output time | ○ | ○ | ○ | ○ | ○ | ○ | — |
| Detailed parameters 2 | [Pr.41] Allowable circular interpolation error width | — | — | ○ | — | — | — | — |
| Detailed parameters 2 | [Pr.42] External command function selection | ○ | ○ | ○ | ○ | ◎ | ○ | — |
| Detailed parameters 2 | [Pr.83] Speed control 10 × multiplier setting for degree axis | ○ | ○ | ○ | ○ | ○ | — | — |
| Detailed parameters 2 | [Pr.84] Restart allowable range when servo OFF to ON | ○ | ○ | ○ | ○ | ○ | ○ | ○ |
| Detailed parameters 2 | [Pr.90] Operation setting for speed-torque control mode | — | — | — | — | — | — | — |
| Detailed parameters 2 | [Pr.95] External command signal selection | ○ | ○ | ○ | ○ | ◎ | ○ | — |
| Detailed parameters 2 | [Pr.112] Servo OFF command valid/invalid setting [FX5-SSC-G] | — | — | — | — | — | — | — |
| Detailed parameters 2 | [Pr.122] Manual pulse generator speed limit mode [FX5-SSC-G] | — | — | — | — | — | — | — |
| Detailed parameters 2 | [Pr.123] Manual pulse generator speed limit value [FX5-SSC-G] | — | — | — | — | — | — | — |
| Detailed parameters 2 | [Pr.127] Speed limit value input selection at control mode switching | — | — | — | — | — | — | — |

*In the original, the "Classification" cells (Basic parameters 1 / Basic parameters 2 / Detailed parameters 1 / Detailed parameters 2) are merged. Expanded to each row. The original header "Positioning parameter" spans the Classification column and the parameter column. The column header is multi-level in the original ("Major positioning control" > "Position control" / "1 to 4 axis speed control" / "Speed-position or position-speed control" / "Other control" > each control); written in one header cell per column, levels separated by " / ". In the first and second columns the two control names are printed on separate lines in one cell (joined with ", " here).

#### Manual control (手動制御) (11.1 / original p.409-410)

◎: Always set, ○: Set as required ("—" when not required), △: Setting restricted,
—: Setting not required (When the value is the default value or within the setting range, there is no problem.)

(original p.409)

| Classification | Positioning parameter | Manual control / Manual pulse generator operation | Manual control / Inching operation | Manual control / JOG operation |
|---|---|---|---|---|
| Basic parameters 1 | [Pr.1] Unit setting | ◎ | ◎ | ◎ |
| Basic parameters 1 | [Pr.2] Number of pulses per rotation (AP) (Unit: pulse) | ◎ | ◎ | ◎ |
| Basic parameters 1 | [Pr.3] Movement amount per rotation (AL) | ◎ | ◎ | ◎ |
| Basic parameters 1 | [Pr.4] Unit magnification (AM) | ◎ | ◎ | ◎ |
| Basic parameters 1 | [Pr.7] Bias speed at start | — | — | ○ |
| Basic parameters 2 | [Pr.8] Speed limit value | — | ◎ | ◎ |
| Basic parameters 2 | [Pr.9] Acceleration time 0 | — | — | ◎ |
| Basic parameters 2 | [Pr.10] Deceleration time 0 | — | — | ◎ |
| Detailed parameters 1 | [Pr.11] Backlash compensation amount | ○ | ○ | ○ |
| Detailed parameters 1 | [Pr.12] Software stroke limit upper limit value | ○ | ○ | ○ |
| Detailed parameters 1 | [Pr.13] Software stroke limit lower limit value | ○ | ○ | ○ |
| Detailed parameters 1 | [Pr.14] Software stroke limit selection | ○ | ○ | ○ |
| Detailed parameters 1 | [Pr.15] Software stroke limit valid/invalid setting | ○ | ○ | ○ |
| Detailed parameters 1 | [Pr.16] Command in-position width | — | — | — |
| Detailed parameters 1 | [Pr.17] Torque limit setting value | △ | △ | △ |
| Detailed parameters 1 | [Pr.18] M code ON signal output timing | — | — | — |
| Detailed parameters 1 | [Pr.19] Speed switching mode | — | — | — |
| Detailed parameters 1 | [Pr.20] Interpolation speed designation method | — | — | — |
| Detailed parameters 1 | [Pr.21] Command position value during speed control | — | — | — |
| Detailed parameters 1 | [Pr.22] Input signal logic selection | ◎ | ◎ | ◎ |
| Detailed parameters 1 | [Pr.81] Speed-position function selection | — | — | — |
| Detailed parameters 1 | [Pr.116] FLS signal selection | ○ | ○ | ○ |
| Detailed parameters 1 | [Pr.117] RLS signal selection | ○ | ○ | ○ |
| Detailed parameters 1 | [Pr.118] DOG signal selection | — | — | — |
| Detailed parameters 1 | [Pr.119] STOP signal selection | ○ | ○ | ○ |

*In the original, the "Classification" cells (Basic parameters 1 / Basic parameters 2 / Detailed parameters 1 / Detailed parameters 2) are merged. Expanded to each row. The original header "Positioning parameter" spans the Classification column and the parameter column. The column header is 2 levels in the original ("Manual control" > each operation); written with " / ".

(original p.410)

| Classification | Positioning parameter | Manual control / Manual pulse generator operation | Manual control / Inching operation | Manual control / JOG operation |
|---|---|---|---|---|
| Detailed parameters 2 | [Pr.25] Acceleration time 1 | — | — | ○ |
| Detailed parameters 2 | [Pr.26] Acceleration time 2 | — | — | ○ |
| Detailed parameters 2 | [Pr.27] Acceleration time 3 | — | — | ○ |
| Detailed parameters 2 | [Pr.28] Deceleration time 1 | — | — | ○ |
| Detailed parameters 2 | [Pr.29] Deceleration time 2 | — | — | ○ |
| Detailed parameters 2 | [Pr.30] Deceleration time 3 | — | — | ○ |
| Detailed parameters 2 | [Pr.31] JOG speed limit value | — | ◎ | ◎ |
| Detailed parameters 2 | [Pr.32] JOG operation acceleration time selection | — | — | ◎ |
| Detailed parameters 2 | [Pr.33] JOG operation deceleration time selection | — | — | ◎ |
| Detailed parameters 2 | [Pr.34] Acceleration/deceleration process selection | — | — | ○ |
| Detailed parameters 2 | [Pr.35] S-curve ratio | — | — | ○ |
| Detailed parameters 2 | [Pr.36] Sudden stop deceleration time | — | — | ○ |
| Detailed parameters 2 | [Pr.37] Stop group 1 sudden stop selection | — | — | ○ |
| Detailed parameters 2 | [Pr.38] Stop group 2 sudden stop selection | — | — | ○ |
| Detailed parameters 2 | [Pr.39] Stop group 3 sudden stop selection | — | — | ○ |
| Detailed parameters 2 | [Pr.40] Positioning complete signal output time | — | — | — |
| Detailed parameters 2 | [Pr.41] Allowable circular interpolation error width | — | — | — |
| Detailed parameters 2 | [Pr.42] External command function selection | — | — | ○ |
| Detailed parameters 2 | [Pr.83] Speed control 10 × multiplier setting for degree axis | ○ | ○ | ○ |
| Detailed parameters 2 | [Pr.84] Restart allowable range when servo OFF to ON | ○ | ○ | ○ |
| Detailed parameters 2 | [Pr.90] Operation setting for speed-torque control mode | — | — | — |
| Detailed parameters 2 | [Pr.95] External command signal selection | — | — | ○ |
| Detailed parameters 2 | [Pr.112] Servo OFF command valid/invalid setting [FX5-SSC-G] | — | — | — |
| Detailed parameters 2 | [Pr.122] Manual pulse generator speed limit mode [FX5-SSC-G] | ○ | — | — |
| Detailed parameters 2 | [Pr.123] Manual pulse generator speed limit value [FX5-SSC-G] | ○ | — | — |
| Detailed parameters 2 | [Pr.127] Speed limit value input selection at control mode switching | — | — | — |

*In the original, the "Classification" cells (Basic parameters 1 / Basic parameters 2 / Detailed parameters 1 / Detailed parameters 2) are merged. Expanded to each row. The original header "Positioning parameter" spans the Classification column and the parameter column. The column header is 2 levels in the original ("Manual control" > each operation); written with " / ".

#### Expansion control (拡張制御) (11.1 / original p.411-412)

◎: Always set, ○: Set as required ("—" when not required), ×: Setting not possible
—: Setting not required (When the value is the default value or within the setting range, there is no problem.)

(original p.411)

| Classification | Positioning parameter | Expansion control / Speed-torque control |
|---|---|---|
| Basic parameters 1 | [Pr.1] Unit setting | ◎ |
| Basic parameters 1 | [Pr.2] Number of pulses per rotation (AP) (Unit: pulse) | ◎ |
| Basic parameters 1 | [Pr.3] Movement amount per rotation (AL) | ◎ |
| Basic parameters 1 | [Pr.4] Unit magnification (AM) | ◎ |
| Basic parameters 1 | [Pr.7] Bias speed at start | × |
| Basic parameters 2 | [Pr.8] Speed limit value | ◎ |
| Basic parameters 2 | [Pr.9] Acceleration time 0 | — |
| Basic parameters 2 | [Pr.10] Deceleration time 0 | — |
| Detailed parameters 1 | [Pr.11] Backlash compensation amount | — |
| Detailed parameters 1 | [Pr.12] Software stroke limit upper limit value | ○ |
| Detailed parameters 1 | [Pr.13] Software stroke limit lower limit value | ○ |
| Detailed parameters 1 | [Pr.14] Software stroke limit selection | ○ |
| Detailed parameters 1 | [Pr.15] Software stroke limit valid/invalid setting | — |
| Detailed parameters 1 | [Pr.16] Command in-position width | — |
| Detailed parameters 1 | [Pr.17] Torque limit setting value | ○ |
| Detailed parameters 1 | [Pr.18] M code ON signal output timing | — |
| Detailed parameters 1 | [Pr.19] Speed switching mode | — |
| Detailed parameters 1 | [Pr.20] Interpolation speed designation method | — |
| Detailed parameters 1 | [Pr.21] Command position value during speed control | — |
| Detailed parameters 1 | [Pr.22] Input signal logic selection | ◎ |
| Detailed parameters 1 | [Pr.81] Speed-position function selection | — |
| Detailed parameters 1 | [Pr.116] FLS signal selection | ○ |
| Detailed parameters 1 | [Pr.117] RLS signal selection | ○ |
| Detailed parameters 1 | [Pr.118] DOG signal selection | — |
| Detailed parameters 1 | [Pr.119] STOP signal selection | ○ |

*In the original, the "Classification" cells (Basic parameters 1 / Basic parameters 2 / Detailed parameters 1 / Detailed parameters 2) are merged. Expanded to each row. The original header "Positioning parameter" spans the Classification column and the parameter column. The column header is 2 levels in the original ("Expansion control" > "Speed-torque control"); written with " / ".

(original p.412)

| Classification | Positioning parameter | Expansion control / Speed-torque control |
|---|---|---|
| Detailed parameters 2 | [Pr.25] Acceleration time 1 | — |
| Detailed parameters 2 | [Pr.26] Acceleration time 2 | — |
| Detailed parameters 2 | [Pr.27] Acceleration time 3 | — |
| Detailed parameters 2 | [Pr.28] Deceleration time 1 | — |
| Detailed parameters 2 | [Pr.29] Deceleration time 2 | — |
| Detailed parameters 2 | [Pr.30] Deceleration time 3 | — |
| Detailed parameters 2 | [Pr.31] JOG speed limit value | — |
| Detailed parameters 2 | [Pr.32] JOG operation acceleration time selection | — |
| Detailed parameters 2 | [Pr.33] JOG operation deceleration time selection | — |
| Detailed parameters 2 | [Pr.34] Acceleration/deceleration process selection | — |
| Detailed parameters 2 | [Pr.35] S-curve ratio | — |
| Detailed parameters 2 | [Pr.36] Sudden stop deceleration time | — |
| Detailed parameters 2 | [Pr.37] Stop group 1 sudden stop selection | — |
| Detailed parameters 2 | [Pr.38] Stop group 2 sudden stop selection | — |
| Detailed parameters 2 | [Pr.39] Stop group 3 sudden stop selection | — |
| Detailed parameters 2 | [Pr.40] Positioning complete signal output time | — |
| Detailed parameters 2 | [Pr.41] Allowable circular interpolation error width | — |
| Detailed parameters 2 | [Pr.42] External command function selection | — |
| Detailed parameters 2 | [Pr.83] Speed control 10 × multiplier setting for degree axis | ○ |
| Detailed parameters 2 | [Pr.84] Restart allowable range when servo OFF to ON | — |
| Detailed parameters 2 | [Pr.90] Operation setting for speed-torque control mode | ○ |
| Detailed parameters 2 | [Pr.95] External command signal selection | — |
| Detailed parameters 2 | [Pr.112] Servo OFF command valid/invalid setting [FX5-SSC-G] | ○ |
| Detailed parameters 2 | [Pr.122] Manual pulse generator speed limit mode [FX5-SSC-G] | — |
| Detailed parameters 2 | [Pr.123] Manual pulse generator speed limit value [FX5-SSC-G] | — |
| Detailed parameters 2 | [Pr.127] Speed limit value input selection at control mode switching | ○ |

*In the original, the "Classification" cells (Basic parameters 1 / Basic parameters 2 / Detailed parameters 1 / Detailed parameters 2) are merged. Expanded to each row. The original header "Positioning parameter" spans the Classification column and the parameter column. The column header is 2 levels in the original ("Expansion control" > "Speed-torque control"); written with " / ".

#### Checking the positioning parameters (位置決め用パラメータのチェックについて) (11.1 / original p.412)

[Pr.1] to [Pr.90], [Pr.95], [Pr.116] to [Pr.119], [Pr.122] to [Pr.123], and [Pr.127] are checked with the following timing.
- When the "[Cd.190] PLC READY" changes from OFF to ON

[Pr.112] is checked at the control mode switching.

> **Point**
> "High-level positioning control" is carried out in combination with the "major positioning control".
> Refer to the "major positioning control" parameter settings for details on the parameters required for "high-level positioning control".

### Setting items for home position return parameters (原点復帰用パラメータの設定項目) (11.1 / original p.413)

When carrying out "home position return control", the "home position return parameters" must be set. The setting items for the "home position return parameters" are shown below.
The "home position return parameters" are set for each axis.
◎: Always set
○: Set as required
—: Setting not required (When the value is the default value or within the setting range, there is no problem.)
R: Set when using the "Home position return retry function" ("—" when not set)
S: Set when using the "Home position shift function" ("—" when not set)

| Classification | No. | Home position return parameters | Machine home position return control: Proximity dog method [FX5-SSC-S] | Machine home position return control: Count method 1 [FX5-SSC-S] | Machine home position return control: Count method 2 [FX5-SSC-S] | Machine home position return control: Data set method [FX5-SSC-S] | Machine home position return control: Scale origin signal detection method [FX5-SSC-S] | Machine home position return control: Driver home position return method | Fast home position return control |
|---|---|---|---|---|---|---|---|---|---|
| Home position return basic parameters | [Pr.43] | Home position return method*1 | Proximity dog method [FX5-SSC-S] | Count method 1 [FX5-SSC-S] | Count method 2 [FX5-SSC-S] | Data set method [FX5-SSC-S] | Scale origin signal detection method [FX5-SSC-S] | Driver home position return method | — |
| Home position return basic parameters | [Pr.44] | Home position return direction | ◎ | ◎ | ◎ | ◎ | ◎ | ○*2 | — |
| Home position return basic parameters | [Pr.45] | Home position address | ◎ | ◎ | ◎ | ◎ | ◎ | ◎ | ◎ |
| Home position return basic parameters | [Pr.46] | Home position return speed | ◎ | ◎ | ◎ | — | ◎ | — | ◎ |
| Home position return basic parameters | [Pr.47] | Creep speed [FX5-SSC-S] | ◎ | ◎ | ◎ | — | ◎ | — | — |
| Home position return basic parameters | [Pr.48] | Home position return retry [FX5-SSC-S] | R | R | R | — | — | — | — |
| Home position return detailed parameters | [Pr.50] | Setting for the movement amount after proximity dog ON [FX5-SSC-S] | — | ◎ | ◎ | — | — | — | — |
| Home position return detailed parameters | [Pr.51] | Home position return acceleration time selection | ◎ | ◎ | ◎ | — | ◎ | — | ◎ |
| Home position return detailed parameters | [Pr.52] | Home position return deceleration time selection | ◎ | ◎ | ◎ | — | ◎ | — | ◎ |
| Home position return detailed parameters | [Pr.53] | Home position shift amount [FX5-SSC-S] | S | S | S | — | S | — | — |
| Home position return detailed parameters | [Pr.54] | Home position return torque limit value [FX5-SSC-S] | ○ | ○ | ○ | — | ○ | — | ◎ |
| Home position return detailed parameters | [Pr.55] | Operation setting for incompletion of home position return | ○ | ○ | ○ | ○ | ○ | ○ | — |
| Home position return detailed parameters | [Pr.56] | Speed designation during home position shift [FX5-SSC-S] | S | S | S | — | S | — | — |
| Home position return detailed parameters | [Pr.57] | Dwell time during home position return retry [FX5-SSC-S] | R | R | R | — | — | — | — |

*In the original, the "Classification" cells (Home position return basic parameters / Home position return detailed parameters) are merged. Expanded to each row. The header "Home position return parameters" spans the Classification, No. and name columns, and the header "Machine home position return control" spans 6 columns; in the original the 6 method names are not in the header but printed as the cells of the [Pr.43] row (kept as printed in the [Pr.43] row, and also added to the column headers here for readability).

*1 For details, refer to the following.
→Page 483 [Pr.43] Home position return method
*2 The home position return operation follows the home position return direction set in the driver (servo amplifier) and does not refer to "[Pr.44] Home position return direction". However, "[Pr.44] Home position return direction" must be set when using the backlash compensation function.
When the positioning is executed in the reverse direction against "[Pr.44] Home position return direction", the backlash compensation is executed in the axis operation such as positioning after the driver home position return. Set the same direction to "[Pr.44] Home position return direction" of the Simple Motion module/Motion module and the last home position return direction of the driver (servo amplifier).

#### Checking the home position return parameters (原点復帰用パラメータのチェックについて) (11.1 / original p.413)

[Pr.43] to [Pr.57] are checked with the following timing.
- When the "[Cd.190] PLC READY" changes from OFF to ON

### Setting items for extended parameters (拡張パラメータの設定項目) (11.1 / original p.414)

The setting items for the "extended parameters" are shown below. The "extended parameters" are set for each axis.

| No. | Extended parameter | Related sub function |
|---|---|---|
| [Pr.91] | Optional data monitor: Data type setting 1 | →Page 371 Optional Data Monitor Function |
| [Pr.92] | Optional data monitor: Data type setting 2 | →Page 371 Optional Data Monitor Function |
| [Pr.93] | Optional data monitor: Data type setting 3 | →Page 371 Optional Data Monitor Function |
| [Pr.94] | Optional data monitor: Data type setting 4 | →Page 371 Optional Data Monitor Function |
| [Pr.512] | Optional SDO 1 [FX5-SSC-G] | →Page 381 Virtual servo amplifier function [FX5-SSC-G] |
| [Pr.591] | Optional data monitor: Data type expansion setting 1 [FX5-SSC-G] | →Page 371 Optional Data Monitor Function |
| [Pr.592] | Optional data monitor: Data type expansion setting 2 [FX5-SSC-G] | →Page 371 Optional Data Monitor Function |
| [Pr.593] | Optional data monitor: Data type expansion setting 3 [FX5-SSC-G] | →Page 371 Optional Data Monitor Function |
| [Pr.594] | Optional data monitor: Data type expansion setting 4 [FX5-SSC-G] | →Page 371 Optional Data Monitor Function |

*In the original, the "Related sub function" cell is merged over [Pr.91] to [Pr.94] and over [Pr.591] to [Pr.594]. Expanded to each row. The header "Extended parameter" spans the No. column and the name column.

### Setting items for servo parameters [FX5-SSC-S] (サーボパラメータの設定項目[FX5-SSC-S]) (11.1 / original p.414)

The servo parameters are used to control the servo motor and the data that is determined by the specification of the servo amplifier being used. The setting item is different depending on the servo amplifier being used.

| No. | Servo parameter | Remark |
|---|---|---|
| [Pr.100] | Servo series | Set the servo amplifier series connected to the Simple Motion module. |
| From PA01 | PA group | Setting items are different according to the servo series. |
| From PB01 | PB group | Setting items are different according to the servo series. |
| From PC01 | PC group | Setting items are different according to the servo series. |
| From PD01 | PD group | Setting items are different according to the servo series. |
| From PE01 | PE group | Setting items are different according to the servo series. |
| From PS01 | PS group | Setting items are different according to the servo series. |
| From PF01 | PF group | Setting items are different according to the servo series. |
| From Po01 | Po group | Setting items are different according to the servo series. |
| From PL01 | PL group | Setting items are different according to the servo series. |

*In the original, the "Remark" cell is merged over the 9 rows From PA01 to From PL01. Expanded to each row. The header "Servo parameter" spans the No. column and the name column.

### Setting items for positioning data (位置決めデータの設定項目) (11.1 / original p.415-416)

Positioning data must be set for carrying out any "major positioning control". The table below lists the items to be set for producing the positioning data.
One to 600 positioning data items can be set for each axis.
◎: Always set
○: Set as required ("—" when not required)
×: Setting not possible (If set, the error "Continuous path control not possible" (error code: 1A1EH [FX5-SSC-S], or error codes: 1B1EH to 1B20H [FX5-SSC-G]) will occur at start.)
—: Setting not required (When the value is the default value or within the setting range, there is no problem.)

(original p.415)

| No. | Positioning data | Item (sub-division) | Position control / 1-axis linear control, 2/3/4-axis linear interpolation control | Position control / 1-axis fixed-feed control, 2/3/4-axis fixed-feed control | Position control / 2-axis circular interpolation control | 1 to 4 axis speed control |
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
| [Da.20] | Axis to be interpolated 1 | — | ◎: 2 axes, 3 axes, 4 axes, —: 1 axis | ◎: 2 axes, 3 axes, 4 axes, —: 1 axis | ◎: 2 axes, 3 axes, 4 axes, —: 1 axis | ◎: 2 axes, 3 axes, 4 axes, —: 1 axis |
| [Da.21] | Axis to be interpolated 2 | — | ◎: 3 axes, 4 axes, —: 1 axis, 2 axes | ◎: 3 axes, 4 axes, —: 1 axis, 2 axes | ◎: 3 axes, 4 axes, —: 1 axis, 2 axes | ◎: 3 axes, 4 axes, —: 1 axis, 2 axes |
| [Da.22] | Axis to be interpolated 3 | — | ◎: 4 axes, —: 1 axis, 2 axes, 3 axes | ◎: 4 axes, —: 1 axis, 2 axes, 3 axes | ◎: 4 axes, —: 1 axis, 2 axes, 3 axes | ◎: 4 axes, —: 1 axis, 2 axes, 3 axes |

*In the original, "[Da.1]" and "Operation pattern" are merged over the 3 operation pattern rows (expanded to each row). For [Da.2] to [Da.22], the name cell spans the "Positioning data" name and sub-division columns ("—" in the sub-division column here). For [Da.20] to [Da.22], the value is one cell spanning all 4 control columns (expanded to each column). The header "Positioning data" spans the No., name and sub-division columns; "Position control" spans the 3 position control columns (written with " / "). In the first and second position control columns the two control names are on separate lines in one header cell (joined with ", " here).

*1 Two control systems are available: the absolute (ABS) system and incremental (INC) system.

(original p.416)

◎: Always set
○: Set as required ("—" when not required)
×: Setting not possible (If set, the error "Continuous path control not possible" (error code: 1A1EH [FX5-SSC-S], or error codes: 1B1EH to 1B20H [FX5-SSC-G]) will occur at start.)
—: Setting not required (When the value is the default value or within the setting range, there is no problem.)

| No. | Positioning data | Item (sub-division) | Speed-position switching control | Position-speed switching control |
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
| [Da.20] | Axis to be interpolated 1 | — | — | — |
| [Da.21] | Axis to be interpolated 2 | — | — | — |
| [Da.22] | Axis to be interpolated 3 | — | — | — |

*In the original, "[Da.1]" and "Operation pattern" are merged over the 3 operation pattern rows (expanded to each row). For [Da.2] to [Da.22], the name cell spans the name and sub-division columns ("—" in the sub-division column here).

| No. | Positioning data | Item (sub-division) | Other control / NOP instruction | Other control / Current value changing | Other control / JUMP instruction | Other control / LOOP | Other control / LEND |
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
| [Da.20] | Axis to be interpolated 1 | — | — | — | — | — | — |
| [Da.21] | Axis to be interpolated 2 | — | — | — | — | — | — |
| [Da.22] | Axis to be interpolated 3 | — | — | — | — | — | — |

*In the original, "[Da.1]" and "Operation pattern" are merged over the 3 operation pattern rows (expanded to each row). For [Da.2] to [Da.22], the name cell spans the name and sub-division columns ("—" in the sub-division column here). The header "Other control" spans the 5 control columns (written with " / ").

*1 Two control systems are available: the absolute (ABS) system and incremental (INC) system.

#### Checking the positioning data (位置決めデータのチェックについて) (11.1 / original p.416)

[Da.1] to [Da.10], [Da.20] to [Da.22] are checked at the following timings:
- Startup of a positioning operation

### Setting items for block start data (ブロック始動データの設定項目) (11.1 / original p.417)

The "block start data" must be set when carrying out "high-level positioning control". The setting items for the "block start data" are shown below.
Up to 50 points of "block start data" can be set for each axis.
○: Set as required ("—" when not required)
—: Setting not required (When the value is the default value or within the setting range, there is no problem.)

| No. | Block start data | Block start (Normal start) | Condition start | Wait start | Simultaneous start | Repeated start (FOR loop) | Repeated start (FOR condition) |
|---|---|---|---|---|---|---|---|
| [Da.11] | Shape (end/continue) | ○ | ○ | ○ | ○ | ○ | ○ |
| [Da.12] | Start data No. | ○ | ○ | ○ | ○ | ○ | ○ |
| [Da.13] | Special start instruction | — | ○ | ○ | ○ | ○ | ○ |
| [Da.14] | Parameter | — | ○ | ○ | ○ | ○ | ○ |

*In the original, the header "Block start data" spans the No. column and the name column.

#### Checking the block start data (ブロック始動データのチェックについて) (11.1 / original p.417)

[Da.11] to [Da.14] are checked with the following timing.
- When "Block start data" starts

### Setting items for condition data (条件データの設定項目) (11.1 / original p.417)

When carrying out "high-level positioning control" or using the JUMP instruction in the "major positioning control", the "condition data" must be set as required. The setting items for the "condition data" are shown below.
Up to 10 "condition data" items can be set for each axis.
○: Set as required ("—" when not required)
△: Setting limited
—: Setting not required (When the value is the default value or within the setting range, there is no problem.)

| No. | Condition data | Major positioning control / Other than JUMP instruction | Major positioning control / JUMP instruction | High-level positioning control / Block start (Normal start) | High-level positioning control / Condition start | High-level positioning control / Wait start | High-level positioning control / Simultaneous start | High-level positioning control / Repeated start (FOR loop) | High-level positioning control / Repeated start (FOR condition) |
|---|---|---|---|---|---|---|---|---|---|
| [Da.15] | Condition target | — | ○ | — | ○ | ○ | ○ | — | ○ |
| [Da.16] | Condition operator | — | ○ | — | ○ | ○ | ○ | — | ○ |
| [Da.17] | Address | — | △ | — | △ | △ | — | — | △ |
| [Da.18] | Parameter 1 | — | ○ | — | ○ | ○ | △ | — | ○ |
| [Da.19] | Parameter 2 | — | △ | — | △ | △ | △ | — | △ |
| [Da.23] | Number of simultaneously starting axes | — | — | — | — | — | ○ | — | — |
| [Da.24] | Simultaneously starting axis No.1 | — | — | — | — | — | ○ | — | — |
| [Da.25] | Simultaneously starting axis No.2 | — | — | — | — | — | ○ | — | — |
| [Da.26] | Simultaneously starting axis No.3 | — | — | — | — | — | ○ | — | — |

*In the original, the column header is 2 levels ("Major positioning control" > 2 columns; "High-level positioning control" > 6 columns). Written in one header cell per column, levels separated by " / ". The header "Condition data" spans the No. column and the name column. Note: the legend here reads "△: Setting limited" (other tables in this section use "△: Setting restricted"); kept as printed.

#### Checking the condition data (条件データのチェックについて) (11.1 / original p.417)

[Da.15] to [Da.19], [Da.23] to [Da.26] are checked with the following timing.
- When "Block start data" starts
- When "JUMP instruction" starts

### Types and roles of monitor data (モニタデータの種類と役割) (11.1 / original p.418-420)

The monitor data area in the buffer memory stores data relating to the operating state of the positioning system, which are monitored as required while the positioning system is operating.
The following data are available for monitoring.

| Item | Description |
|---|---|
| System monitoring | Monitoring of the specification and operation history of Simple Motion module/Motion module (system monitor data [Md.3] to [Md.8], [Md.19], [Md.50] to [Md.54], [Md.59], [Md.60], [Md.130] to [Md.135], [Md.140], [Md.141]) |
| Axis operation monitoring | Monitoring of the current position and speed, and other data related to the movements of axes (axis monitor data [Md.20] to [Md.48], [Md.62], [Md.100] to [Md.117], [Md.119], [Md.120], [Md.122] to [Md.127], [Md.160], [Md.164], [Md.190], [Md.500], [Md.502], [Md.514]) |

#### Monitoring the system (システムをモニタする) (11.1 / original p.418)

##### ■Monitoring the positioning system operation history (位置決めシステムの運転履歴をモニタする) (11.1 / original p.418)

| Monitoring details | Monitoring details (detail) | Monitoring details (sub-detail) | Corresponding item |
|---|---|---|---|
| History of data that started an operation | Start information | — | [Md.3] Start information |
| History of data that started an operation | Start No. | — | [Md.4] Start No. |
| History of data that started an operation | Start*1 | Year: month | [Md.54] Start (Year: month) |
| History of data that started an operation | Start*1 | Day: hour | [Md.5] Start (Day: hour) |
| History of data that started an operation | Start*1 | Minute: second | [Md.6] Start (Minute: second) |
| History of data that started an operation | Start*1 | ms | [Md.60] Start (ms) |
| History of data that started an operation | Error upon starting | — | [Md.7] Error judgment |
| History of data that started an operation | Pointer No. next to the pointer No. where the latest history is stored | — | [Md.8] Start history pointer |
| Number of write accesses to the flash ROM after the power is switched ON | Number of write accesses to flash ROM | — | [Md.19] Number of write accesses to flash ROM |
| Forced stop input signal (EMI) turn ON/OFF | Forced stop input signal (EMI) information | — | [Md.50] Forced stop input |
| Monitor whether the system is in amplifier-less operation [FX5-SSC-S] | — | — | [Md.51] Amplifier-less operation mode status |
| Monitor the detection status of axis that set communication between amplifiers [FX5-SSC-S] | — | — | [Md.52] Communication between amplifiers axes searching flag |
| Monitor the connect/disconnect status of SSCNET communication [FX5-SSC-S] | — | — | [Md.53] SSCNET control status |
| Store the module information | — | — | [Md.59] Module information |
| Monitor the firmware version of the module | — | — | [Md.130] F/W version |
| Monitor the RUN status of digital oscilloscope | — | — | [Md.131] Digital oscilloscope running flag |
| Monitor the current operation cycle. | — | — | [Md.132] Operation cycle setting |
| Monitor whether the operation cycle time exceeds operation cycle. | — | — | [Md.133] Operation cycle over flag |
| Monitor the time that took for operation every operation cycle. | — | — | [Md.134] Operation time |
| Monitor the maximum value of operation time after each module's power supply ON. | — | — | [Md.135] Maximum operation time |
| Store the module status information. | — | — | [Md.140] Module status |
| Monitor the BUSY state. | — | — | [Md.141] BUSY |

*In the original, the "Monitoring details" header spans 3 levels of cells. "History of data that started an operation" is merged over 8 rows and "Start*1" over 4 rows (expanded to each row). Where a monitoring details cell is not subdivided, it spans the whole "Monitoring details" width ("—" in the unused columns here).

*1 Displays a value set by the clock function of the CPU module.

#### Monitoring the axis operation state (軸の運転状態をモニタする) (11.1 / original p.419-420)

##### ■Monitoring the position (位置をモニタする) (11.1 / original p.419)

| Monitor details | Corresponding item |
|---|---|
| Monitor the current machine feed value | [Md.21] Machine feed value |
| Monitor the command position value | [Md.20] Command position value |
| Monitor the current target value | [Md.32] Target value |

##### ■Monitoring the speed (速度をモニタする) (11.1 / original p.419)

| Monitor details | Monitor details (detail) | Monitor details (condition) | Monitor details (indication) | Corresponding item |
|---|---|---|---|---|
| Monitor the current speed | During independent axis control | — | Indicates the speed of each axis | [Md.22] Speed command |
| Monitor the current speed | During interpolation control | When "0: Composite speed" is set for "[Pr.20] Interpolation speed designation method" | Indicates the composite speed | [Md.22] Speed command |
| Monitor the current speed | During interpolation control | When "1: Reference axis speed" is set for "[Pr.20] Interpolation speed designation method" | Indicates the reference axis speed | [Md.22] Speed command |
| Monitor the current speed | Monitor "[Da.8] Command speed" currently being executed. | — | — | [Md.27] Current speed |
| Monitor the current speed | Constantly indicates the speed of each axis | — | — | [Md.28] Axis speed command |
| Monitor the current target speed | — | — | — | [Md.33] Target speed |
| Monitor the command speed at speed control mode or continuous operation to torque control mode in the speed-torque control | — | — | — | [Md.122] Speed during command |

*In the original, "Monitor the current speed" is merged over 5 rows, "During interpolation control" over 2 rows, and "[Md.22] Speed command" over 3 rows (expanded to each row). "During independent axis control" spans the detail and condition columns; "Monitor "[Da.8] Command speed" currently being executed." and "Constantly indicates the speed of each axis" span the detail, condition and indication columns; the last 2 rows span all 4 monitor details columns ("—" in the unused columns here).

##### ■Monitoring the status of servo amplifier (サーボアンプの状態をモニタする) (11.1 / original p.419-420)

| Monitor details | Corresponding item |
|---|---|
| Monitor the real current value "command position value - deviation counter value". [FX5-SSC-S] | [Md.101] Actual position value |
| Monitor the real current value "command position value - (command pulse - feedback pulse)". [FX5-SSC-G] | [Md.101] Actual position value |
| Monitor the pulse droop. | [Md.102] Deviation counter value |
| Monitor the motor speed of servo motor. | [Md.103] Motor rotation speed |
| Monitor the current value of servo motor. | [Md.104] Motor current value |
| Monitor the software No. of servo amplifier. [FX5-SSC-S] | [Md.106] Servo amplifier software No. |
| Monitor the parameter No. that an error occurred. [FX5-SSC-S] | [Md.107] Parameter error No. |
| Monitor the status (servo status) of servo amplifier. | [Md.108] Servo status1 |
| Monitor the status (servo status) of servo amplifier. | [Md.119] Servo status2 |
| Monitor the status (servo status) of servo amplifier. | [Md.125] Servo status3 |
| Monitor the status (servo status) of servo amplifier. [FX5-SSC-G] | [Md.126] Servo status4 |
| Monitor the status (servo status) of servo amplifier. [FX5-SSC-S] | [Md.127] Servo status5 |
| Monitor the status (servo status) of servo amplifier. [FX5-SSC-S] | [Md.500] Servo status7 |
| • Monitor the percentage of regenerative power to permissible regenerative value.<br>[FX5-SSC-S]<br>• Monitor the content of "[Pr.91] Optional data monitor: Data type setting 1" at optional data monitor data type setting.<br>[FX5-SSC-G]<br>• Monitor the content of "[Pr.91] Optional data monitor: Data type setting 1" and "[Pr.591] Optional data monitor: Data type expansion setting 1" at optional data monitor data type setting. | [Md.109] Regenerative load ratio/Optional data monitor output 1 |
| • Monitor the continuous effective load torque.<br>[FX5-SSC-S]<br>• Monitor the content of "[Pr.92] Optional data monitor: Data type setting 2" at optional data monitor data type setting.<br>[FX5-SSC-G]<br>• Monitor the content of "[Pr.92] Optional data monitor: Data type setting 2" and "[Pr.592] Optional data monitor: Data type expansion setting 2" at optional data monitor data type setting. | [Md.110] Effective load torque/Optional data monitor output 2 |
| • Monitor the maximum generated torque.<br>[FX5-SSC-S]<br>• Monitor the content of "[Pr.93] Optional data monitor: Data type setting 3" at optional data monitor data type setting.<br>[FX5-SSC-G]<br>• Monitor the content of "[Pr.93] Optional data monitor: Data type setting 3" and "[Pr.593] Optional data monitor: Data type expansion setting 3" at optional data monitor data type setting. | [Md.111] Peak torque ratio/Optional data monitor output 3 |
| [FX5-SSC-S]<br>• Monitor the content of "[Pr.94] Optional data monitor: Data type setting 4" at optional data monitor data type setting.<br>[FX5-SSC-G]<br>• Monitor the content of "[Pr.94] Optional data monitor: Data type setting 4" and "[Pr.594] Optional data monitor: Data type expansion setting 4" at optional data monitor data type setting. | [Md.112] Optional data monitor output 4 |
| Monitor the status of semi closed loop control/fully closed loop control. | [Md.113] Semi/Fully closed loop status |
| Monitor the alarm of servo amplifier. | [Md.114] Servo alarm |
| Monitor the alarm detail No. of the servo amplifier. [FX5-SSC-G] | [Md.115] Servo alarm detail number |
| Monitor the option information of encoder. | [Md.116] Encoder option information |
| Monitor the CiA402 Statusword of the servo amplifier. [FX5-SSC-G] | [Md.117] Statusword |
| Monitor the driver operation alarm No. [FX5-SSC-S] | [Md.502] Driver operation alarm No. |
| Monitor the status of the servo amplifier during home position return. [FX5-SSC-G] | [Md.514] HPR operating status |

*In the original, "[Md.101] Actual position value" is merged over 2 rows; "Monitor the status (servo status) of servo amplifier." is merged over the 3 rows [Md.108]/[Md.119]/[Md.125]; "Monitor the status (servo status) of servo amplifier. [FX5-SSC-S]" is merged over the 2 rows [Md.127]/[Md.500]. Expanded to each row. The table continues from p.419 ([Md.101] to [Md.111]) to p.420 ([Md.112] to [Md.514]). The cell line breaks and bullets in the [Md.109] to [Md.112] rows are as printed.

##### ■Monitoring the state (状態をモニタする) (11.1 / original p.420)

| Monitor details | Corresponding item |
|---|---|
| Monitor the latest error code that occurred with the axis | [Md.23] Axis error No. |
| Monitor the latest warning code that occurred with the axis | [Md.24] Axis warning No. |
| Monitor the valid M codes | [Md.25] Valid M code |
| Monitor the axis operation state | [Md.26] Axis operation status |
| Monitor the movement amount after the current position control switching when using "speed-position switching control". | [Md.29] Speed-position switching control positioning movement amount |
| Monitor the external input/output signal and flag | [Md.30] External input signal |
| Monitor the external input/output signal and flag | [Md.31] Status |
| Monitor the movement amount from proximity dog ON to machine home position return completion. [FX5-SSC-S] | [Md.34] Movement amount after proximity dog ON |
| Monitor the current torque limit value | [Md.35] Torque limit stored value/forward torque limit stored value |
| Monitor the current torque limit value | [Md.120] Reverse torque limit stored value |
| Monitor the "instruction code" of the special start data when using special start | [Md.36] Special start data instruction code setting value |
| Monitor the "instruction parameter" of the special start data when using special start | [Md.37] Special start data instruction parameter setting value |
| Monitor the "start data No." of the special start data when using special start | [Md.38] Start positioning data No. setting value |
| Monitor whether the speed is being limited | [Md.39] In speed limit flag |
| Monitor whether the speed is being changed | [Md.40] In speed change processing flag |
| Monitor the remaining number of repetitions (special start) | [Md.41] Special start repetition counter |
| Monitor the remaining number of repetitions (control system) | [Md.42] Control system repetition counter |
| Monitor the "start data" point currently being executed | [Md.43] Start data pointer being executed |
| Monitor the "positioning data No." currently being executed | [Md.44] Positioning data No. being executed |
| Monitor the block No. | [Md.45] Block No. being executed |
| Monitor the "positioning data No." executed last | [Md.46] Last executed positioning data No. |
| Monitor the positioning data currently being executed | [Md.47] Positioning data being executed |
| Monitor switching from the constant speed status or acceleration status to the deceleration status during position control whose operation pattern is "Positioning complete" | [Md.48] Deceleration start flag |
| Monitor the carrying over movement amount which exceeds "[Pr.123] Manual pulse generator speed limit value" [FX5-SSC-G] | [Md.62] Amount of the manual pulser driving carrying over movement |
| Monitor the distance that travels to zero point after stop once at home position return. [FX5-SSC-S] | [Md.100] Home position return re-travel value |
| Monitor the command torque at torque control mode or continuous operation to torque control mode in the speed-torque control. | [Md.123] Torque during command |
| Monitor the switching status of control mode. | [Md.124] Control mode switching status |
| Monitor the response code (SDO Abort code) received from the device in response to the transient request. [FX5-SSC-G] | [Md.160] Optional SDO transfer result 1 |
| Monitor the processing status of the transient request. [FX5-SSC-G] | [Md.164] Optional SDO transfer status 1 |
| Monitor the completion status of the controller current value restoration. [FX5-SSC-G] | [Md.190] Controller position value restoration complete status |

*In the original, "Monitor the external input/output signal and flag" is merged over 2 rows ([Md.30]/[Md.31]) and "Monitor the current torque limit value" over 2 rows ([Md.35]/[Md.120]). Expanded to each row.

### Types and roles of control data (制御データの種類と役割) (11.1 / original p.421-423)

Operation of the positioning system is achieved through the execution of necessary controls. (Data required for controls are given through the default values when the power is switched ON, which can be modified as required by the program.)
Items that can be controlled are described below.

| Item | Description |
|---|---|
| Controlling the system data | Setting and resetting "setting data" of Simple Motion module/Motion module.<br>(system control data [Cd.1], [Cd.2]) |
| Controlling the operation | Setting operation parameters, changing speed during operation, interrupting or restarting operation, etc.<br>(system control data [Cd.41], [Cd.42], [Cd.44], [Cd.55], [Cd.102], [Cd.137], [Cd.158], [Cd.190], [Cd.191], axis control data [Cd.3] to [Cd.40], [Cd.43], [Cd.45], [Cd.46], [Cd.100], [Cd.101], [Cd.108], [Cd.112], [Cd.113], [Cd.130] to [Cd.133], [Cd.136], [Cd.138] to [Cd.154], [Cd.180] to [Cd.184]) |

*The original table has no header row; "Item" / "Description" are added here.

#### Controlling the system data (システムデータを制御する) (11.1 / original p.421)

##### ■Setting and resetting the setting data (設定データの設定・リセット) (11.1 / original p.421)

| Control details | Controlled data item |
|---|---|
| Write setting data from buffer memory to flash ROM. | [Cd.1] Flash ROM write request |
| Reset (initialize) parameters. | [Cd.2] Parameter initialization request |

#### Controlling the operation (運転を制御する) (11.1 / original p.421-423)

##### ■Controlling the operation (運転を制御する) (11.1 / original p.421)

| Control details | Corresponding item |
|---|---|
| Set which positioning to execute (start No.). | [Cd.3] Positioning start No. |
| Set start point No. for executing block start. | [Cd.4] Positioning starting point No. |
| Clear (reset) the axis error ([Md.23]) and warning ([Md.24]). | [Cd.5] Axis error reset |
| Issue instruction to restart (When axis operation is stopped). | [Cd.6] Restart command |
| Stop continuous control. | [Cd.18] Interrupt request during continuous operation |
| Set start data No. of own axis at multiple axes simultaneous starting. | [Cd.30] Simultaneous starting own axis start data No. |
| Set start data No.1 for axes that start up simultaneously. | [Cd.31] Simultaneous starting axis start data No.1 |
| Set start data No.2 for axes that start up simultaneously. | [Cd.32] Simultaneous starting axis start data No.2 |
| Set start data No.3 for axes that start up simultaneously. | [Cd.33] Simultaneous starting axis start data No.3 |
| Stop (deceleration stop) the current positioning operation and execute the next positioning operation. | [Cd.37] Skip command |
| Specify write destination for teaching results. | [Cd.38] Teaching data selection |
| Specify data to be taught. | [Cd.39] Teaching positioning data No. |
| Set number of simultaneous starting axes and target axis. | [Cd.43] Simultaneous starting axis |
| Set the status of the external input signal (upper/lower limit switch signal, proximity dog signal, stop signal). | [Cd.44] External input signal operation device (Axis 1 to 8) |
| Set the forced stop information to the buffer memory. [FX5-SSC-G] | [Cd.158] Forced stop input |
| Stop axis in control. | [Cd.180] Axis stop |
| Execute start request of JOG operation or inching operation. | [Cd.181] Forward run JOG start |
| Execute start request of JOG operation or inching operation. | [Cd.182] Reverse run JOG start |
| Execute pre-reading at positioning start. | [Cd.183] Execution prohibition flag |
| Start the home position return or positioning operation. | [Cd.184] Positioning start |

*In the original, "Execute start request of JOG operation or inching operation." is merged over 2 rows ([Cd.181]/[Cd.182]). Expanded to each row.

##### ■Controlling operation per step (ステップ運転を制御する) (11.1 / original p.421)

| Control details | Corresponding item |
|---|---|
| Set unit to carry out step. | [Cd.34] Step mode |
| Stop positioning operation after each operation. | [Cd.35] Step valid flag |
| Continuous operation from stopped step. | [Cd.36] Step start information |

##### ■Controlling the speed (速度を制御する) (11.1 / original p.422)

| Control details | Corresponding item |
|---|---|
| When changing acceleration time during speed change, set new acceleration time. | [Cd.10] New acceleration time value |
| When changing deceleration time during speed change, set new deceleration time. | [Cd.11] New deceleration time value |
| Set acceleration/deceleration time validity during speed change. | [Cd.12] Acceleration/deceleration time change value during speed change, enable/disable |
| Change positioning operation speed within the set range (%). | [Cd.13] Positioning operation speed override |
| Set new speed when changing speed during operation. | [Cd.14] New speed value |
| Issue instruction to change speed in operation to [Cd.14] value. (Only during positioning operation and JOG operation). | [Cd.15] Speed change request |
| Set inching movement amount. | [Cd.16] Inching movement amount |
| Set JOG speed. | [Cd.17] JOG speed |

##### ■Change operation mode (運転モードを変更する) (11.1 / original p.422)

| Control details | Corresponding item |
|---|---|
| Change operation mode. [FX5-SSC-S] | [Cd.137] Amplifier-less operation mode switching request |

##### ■Making settings related to operation (運転に関する設定を行う) (11.1 / original p.422-423)

| Control details | Corresponding item |
|---|---|
| Turn M code ON signal OFF. | [Cd.7] M code OFF request |
| Validate external command signal. | [Cd.8] External command valid |
| Set new value when changing current value. | [Cd.9] New position value |
| Change home position return request flag from "ON to OFF". | [Cd.19] Home position return request flag OFF request |
| Set scale per pulse of number of input pulses from manual pulse generator. | [Cd.20] Manual pulse generator 1 pulse input magnification |
| Set manual pulse generator operation validity. | [Cd.21] Manual pulse generator enable flag |
| Change "[Md.35] Torque limit stored value/forward torque limit stored value". | [Cd.22] New torque value/forward new torque value |
| Change movement amount for position control during speed-position switching control (INC mode). | [Cd.23] Speed-position switching control movement amount change register |
| Validate switching signal set in "[Cd.45] Speed-position switching device selection". | [Cd.24] Speed-position switching enable flag |
| Change speed for speed control during position-speed switching control. | [Cd.25] Position-speed switching control speed change register |
| Validate switching signal set in "[Cd.45] Speed-position switching device selection". | [Cd.26] Position-speed switching enable flag |
| Set new positioning address when changing target position during positioning. | [Cd.27] Target position change value (New address) |
| Set new speed when changing target position during positioning. | [Cd.28] Target position change value (New speed) |
| Set up a flag when target position is changed during positioning. | [Cd.29] Target position change request flag |
| Set absolute (ABS) moving direction in degrees. | [Cd.40] ABS direction in degrees |
| Set whether "[Md.48] Deceleration start flag" is valid or invalid | [Cd.41] Deceleration start flag valid |
| Set the stop command processing for deceleration stop function (deceleration curve re-processing/deceleration curve continuation) | [Cd.42] Stop command processing for deceleration stop selection |
| Set the device used for speed-position switching. | [Cd.45] Speed-position switching device selection |
| Switch speed-position control. | [Cd.46] Speed-position switching command |
| Set the values to use as the input values of the manual pulse generator via CPU in order. | [Cd.55] Input value for manual pulse generator via CPU |
| Turn the servo OFF for each axis. | [Cd.100] Servo OFF command |
| Set torque limit value | [Cd.101] Torque output setting value |
| Set the connect/disconnect of SSCNET communication. [FX5-SSC-S] | [Cd.102] SSCNET control command |
| Set whether gain switching is execution or not. | [Cd.108] Gain switching command flag |
| Set "same setting/individual setting" of the forward torque limit value or reverse torque limit value in the torque change function. | [Cd.112] Torque change function switching request |
| Change "[Md.120] Reverse torque limit stored value". | [Cd.113] New reverse torque value |
| Set the semi closed loop control/fully closed loop control. | [Cd.133] Semi/Fully closed loop switching request |
| Set the PI-PID switching to servo amplifier. | [Cd.136] PI-PID switching request |
| Speed-torque control: Switch the control mode. | [Cd.138] Control mode switching request |
| Speed-torque control: Set the control mode to switch. | [Cd.139] Control mode setting |
| Speed-torque control: Set the command speed during speed control mode. | [Cd.140] Command speed at speed control mode |
| Speed-torque control: Set the acceleration time during speed control mode. | [Cd.141] Acceleration time at speed control mode |
| Speed-torque control: Set the deceleration time during speed control mode. | [Cd.142] Deceleration time at speed control mode |
| Speed-torque control: Set the command torque during torque control mode. | [Cd.143] Command torque at torque control mode |
| Speed-torque control: Set the time constant at driving of torque control mode. | [Cd.144] Torque time constant at torque control mode (Forward direction) |
| Speed-torque control: Set the time constant at regeneration of torque control mode. | [Cd.145] Torque time constant at torque control mode (Negative direction) |
| Speed-torque control: Set the speed limit value during torque control mode. | [Cd.146] Speed limit value at torque control mode |
| Speed-torque control: Set the command speed during continuous operation to torque control mode. | [Cd.147] Speed limit value at continuous operation to torque control mode |
| Speed-torque control: Set the acceleration time during continuous operation to torque control mode. | [Cd.148] Acceleration time at continuous operation to torque control mode |
| Speed-torque control: Set the deceleration time during continuous operation to torque control mode. | [Cd.149] Deceleration time at continuous operation to torque control mode |
| Speed-torque control: Set the target torque during continuous operation to torque control mode. | [Cd.150] Target torque at continuous operation to torque control mode |
| Speed-torque control: Set the time constant at driving of continuous operation to torque control mode. | [Cd.151] Torque time constant at continuous operation to torque control mode (Forward direction) |
| Speed-torque control: Set the time constant at regeneration of continuous operation to torque control mode. | [Cd.152] Torque time constant at continuous operation to torque control mode (Negative direction) |
| Speed-torque control: Set the switching conditions for switching to continuous operation to torque control mode. | [Cd.153] Control mode auto-shift selection |
| Speed-torque control: Set the condition value when "[Cd.153] Control mode auto-shift selection" is set. | [Cd.154] Control mode auto-shift parameter |
| Notify the Simple Motion module/Motion module that the CPU module is normal. | [Cd.190] PLC READY |
| Turn ON/OFF the servo for all the servo amplifiers connected to the Simple Motion module/Motion module. | [Cd.191] All axis servo ON |

*The table continues from p.422 ([Cd.7] to [Cd.113]) to p.423 ([Cd.133] to [Cd.191]). On p.423, "Speed-torque control" is a merged cell in a separate left sub-column over the 17 rows [Cd.138] to [Cd.154]; written here as the prefix "Speed-torque control:" in each of those rows. Note: the [Cd.26] Position-speed switching enable flag row reads "Validate switching signal set in "[Cd.45] Speed-position switching device selection"." (same text as the [Cd.24] row); kept as printed.

## 11.2 List of Buffer Memory Addresses (バッファメモリアドレス一覧) (11.2 / original p.424-445)

The following shows the relation between the buffer memory addresses and the various items.
Do not use the buffer memory address that not been described here for a "Maker setting".
*(Note: "that not been described" is as printed in the original.)*
References for the list of buffer memory addresses in this section are shown below.

| Buffer memory address | Reference |
|---|---|
| Buffer memory addresses for positioning data | "Help" in the "Simple Motion Module Setting Function" of the engineering tool.*1 |
| Buffer memory addresses used in synchronous control | Refer to "List of Buffer Memory Addresses (for Synchronous Control)" in the following manual.<br>[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Advanced Synchronous Control) |
| Buffer memory addresses used for the CC-Link IE TSN network [FX5-SSC-G] | Refer to "Buffer Memory" in the following manual.<br>[Other manual] MELSEC iQ-F FX5 Motion Module User's Manual (CC-Link IE TSN) |

*1 Simple Motion Module Setting Function ⇒ "Help" ⇒ "Buffer Memory Address List"

(Notation for the tables below: where the original lists several addresses stacked vertically in one cell (2-word data and the like), they are written in one row separated by `<br>`. The "Item" header of the original spans the item number column and the item name column.)

#### [Basic setting] (基本設定) (11.2 / original p.424-427)

##### Servo network configuration parameters [FX5-SSC-G] (サーボネットワーク構成パラメータ[FX5-SSC-G]) (11.2 / original p.424)

n: Axis No. -1

| Item | | Fetch cycle | Buffer memory address |
|---|---|---|---|
| [Pr.101] | Virtual servo amplifier setting | At power supply ON/the CPU module reset | 58022+32n |
| [Pr.140] | Driver command discard detection setting | At power supply ON/the CPU module reset | 58023+32n |
| [Pr.141] | IP address | At power supply ON/the CPU module reset | 58024+32n<br>58025+32n |
| [Pr.142] | Multidrop number | At power supply ON/the CPU module reset | 58028+32n |

*In the original, the "Fetch cycle" cell is merged over [Pr.101] to [Pr.142]. Expanded to each row.

##### Common parameters (共通パラメータ) (11.2 / original p.424)

| Item | | Fetch cycle | Buffer memory address |
|---|---|---|---|
| [Pr.24] | Manual pulse generator/Incremental synchronous encoder input selection [FX5-SSC-S] | "[Cd.190] PLC READY" OFF to ON | 33 |
| [Pr.82] | Forced stop valid/invalid selection | "[Cd.190] PLC READY" OFF to ON | 35 |
| [Pr.89] | Manual pulse generator/Incremental synchronous encoder input type selection [FX5-SSC-S] | "[Cd.190] PLC READY" OFF to ON | 67 |
| [Pr.96] | Operation cycle setting [FX5-SSC-S] | At power supply ON/the CPU module reset | 105 |
| [Pr.97] | SSCNET setting [FX5-SSC-S] | At power supply ON/the CPU module reset | 106 |
| [Pr.150] | Input terminal logic selection [FX5-SSC-S] | At power supply ON/the CPU module reset/"[Cd.190] PLC READY" OFF to ON | 58000<br>58001 |
| [Pr.151] | Manual pulse generator/Incremental synchronous encoder input logic selection [FX5-SSC-S] | At power supply ON/the CPU module reset/"[Cd.190] PLC READY" OFF to ON | 58002 |
| [Pr.152] | Maximum number of control axes [FX5-SSC-G] | At power supply ON/the CPU module reset | 58003 |
| [Pr.156] | Manual pulse generator smoothing time constant [FX5-SSC-G] | "[Cd.190] PLC READY" OFF to ON | 58011 |
| [Pr.900] | Forced stop signal (EMI): Link device type [FX5-SSC-G] | At power supply ON/the CPU module reset | 58014 |
| [Pr.901] | Forced stop signal (EMI): Link device start No. [FX5-SSC-G] | At power supply ON/the CPU module reset | 58015 |
| [Pr.902] | Forced stop signal (EMI): Link device bit specification [FX5-SSC-G] | At power supply ON/the CPU module reset | 58016 |
| [Pr.903] | Forced stop signal (EMI): Link device logic setting [FX5-SSC-G] | At power supply ON/the CPU module reset | 58017 |

*In the original, the "Fetch cycle" cell is merged over [Pr.24] to [Pr.89], [Pr.96] to [Pr.97], [Pr.150] to [Pr.151], and [Pr.900] to [Pr.903]. Expanded to each row.

##### Positioning parameters: Basic parameters 1 (位置決め用パラメータ: 基本パラメータ1) (11.2 / original p.425)

n: Axis No. - 1

| Item | | Fetch cycle | Buffer memory address |
|---|---|---|---|
| [Pr.1] | Unit setting | "[Cd.190] PLC READY" OFF to ON | 0+150n |
| [Pr.2] | Number of pulses per rotation (AP) | "[Cd.190] PLC READY" OFF to ON | 2+150n<br>3+150n |
| [Pr.3] | Movement amount per rotation (AL) | "[Cd.190] PLC READY" OFF to ON | 4+150n<br>5+150n |
| [Pr.4] | Unit magnification (AM) | "[Cd.190] PLC READY" OFF to ON | 1+150n |
| [Pr.7] | Bias speed at start | "[Cd.190] PLC READY" OFF to ON | 6+150n<br>7+150n |

*In the original, the "Fetch cycle" cell is merged over [Pr.1] to [Pr.7]. Expanded to each row.

##### Positioning parameters: Basic parameters 2 (位置決め用パラメータ: 基本パラメータ2) (11.2 / original p.425)

n: Axis No. - 1

| Item | | Fetch cycle | Buffer memory address |
|---|---|---|---|
| [Pr.8] | Speed limit value | When the next each control starts | 10+150n<br>11+150n |
| [Pr.9] | Acceleration time 0 | When the next each control starts | 12+150n<br>13+150n |
| [Pr.10] | Deceleration time 0 | When the next each control starts | 14+150n<br>15+150n |

*In the original, the "Fetch cycle" cell is merged over [Pr.8] to [Pr.10]. Expanded to each row.

##### Positioning parameters: Detailed parameters 1 (位置決め用パラメータ: 詳細パラメータ1) (11.2 / original p.425)

n: Axis No. - 1

| Item | | Fetch cycle | Buffer memory address |
|---|---|---|---|
| [Pr.11] | Backlash compensation amount | "[Cd.190] PLC READY" OFF to ON | 17+150n |
| [Pr.12] | Software stroke limit upper limit value | "[Cd.190] PLC READY" OFF to ON | 18+150n<br>19+150n |
| [Pr.13] | Software stroke limit lower limit value | "[Cd.190] PLC READY" OFF to ON | 20+150n<br>21+150n |
| [Pr.14] | Software stroke limit selection | "[Cd.190] PLC READY" OFF to ON | 22+150n |
| [Pr.15] | Software stroke limit valid/invalid setting | "[Cd.190] PLC READY" OFF to ON | 23+150n |
| [Pr.16] | Command in-position width | "[Cd.190] PLC READY" OFF to ON | 24+150n<br>25+150n |
| [Pr.17] | Torque limit setting value | "[Cd.190] PLC READY" OFF to ON | 26+150n |
| [Pr.18] | M code ON signal output timing | "[Cd.190] PLC READY" OFF to ON | 27+150n |
| [Pr.19] | Speed switching mode | "[Cd.190] PLC READY" OFF to ON | 28+150n |
| [Pr.20] | Interpolation speed designation method | "[Cd.190] PLC READY" OFF to ON | 29+150n |
| [Pr.21] | Command position value during speed control | "[Cd.190] PLC READY" OFF to ON | 30+150n |
| [Pr.22] | Input signal logic selection | "[Cd.190] PLC READY" OFF to ON | 31+150n |
| [Pr.81] | Speed-position function selection | "[Cd.190] PLC READY" OFF to ON | 34+150n |
| [Pr.116] | FLS signal selection | At power supply ON/the CPU module reset/"[Cd.190] PLC READY" OFF to ON | 116+150n |
| [Pr.117] | RLS signal selection | At power supply ON/the CPU module reset/"[Cd.190] PLC READY" OFF to ON | 117+150n |
| [Pr.118] | DOG signal selection | At power supply ON/the CPU module reset/"[Cd.190] PLC READY" OFF to ON | 118+150n |
| [Pr.119] | STOP signal selection | At power supply ON/the CPU module reset/"[Cd.190] PLC READY" OFF to ON | 119+150n |

*In the original, the "Fetch cycle" cell is merged over [Pr.11] to [Pr.81], and over [Pr.116] to [Pr.119]. Expanded to each row.

##### Positioning parameters: Detailed parameters 2 (位置決め用パラメータ: 詳細パラメータ2) (11.2 / original p.426)

n: Axis No. - 1

| Item | | Fetch cycle | Buffer memory address |
|---|---|---|---|
| [Pr.25] | Acceleration time 1 | When the next each control starts | 36+150n<br>37+150n |
| [Pr.26] | Acceleration time 2 | When the next each control starts | 38+150n<br>39+150n |
| [Pr.27] | Acceleration time 3 | When the next each control starts | 40+150n<br>41+150n |
| [Pr.28] | Deceleration time 1 | When the next each control starts | 42+150n<br>43+150n |
| [Pr.29] | Deceleration time 2 | When the next each control starts | 44+150n<br>45+150n |
| [Pr.30] | Deceleration time 3 | When the next each control starts | 46+150n<br>47+150n |
| [Pr.31] | JOG speed limit value | When the next each control starts | 48+150n<br>49+150n |
| [Pr.32] | JOG operation acceleration time selection | When the next each control starts | 50+150n |
| [Pr.33] | JOG operation deceleration time selection | When the next each control starts | 51+150n |
| [Pr.34] | Acceleration/deceleration process selection | When the next each control starts | 52+150n |
| [Pr.35] | S-curve ratio | When the next each control starts | 53+150n |
| [Pr.36] | Sudden stop deceleration time | When the next each control starts | 54+150n<br>55+150n |
| [Pr.37] | Stop group 1 sudden stop selection | When the next each control starts | 56+150n |
| [Pr.38] | Stop group 2 sudden stop selection | When the next each control starts | 57+150n |
| [Pr.39] | Stop group 3 sudden stop selection | When the next each control starts | 58+150n |
| [Pr.40] | Positioning complete signal output time | When the next each control starts | 59+150n |
| [Pr.41] | Allowable circular interpolation error width | When the next each control starts | 60+150n<br>61+150n |
| [Pr.42] | External command function selection | At conditions established (DI input) | 62+150n |
| [Pr.83] | Speed control 10 × multiplier setting for degree axis | "[Cd.190] PLC READY" OFF to ON | 63+150n |
| [Pr.84] | Restart allowable range when servo OFF to ON | At start | 64+150n<br>65+150n |
| [Pr.90] | Operation setting for speed-torque control mode | "[Cd.190] PLC READY" OFF to ON | 68+150n |
| [Pr.95] | External command signal selection | "[Cd.190] PLC READY" OFF to ON | 69+150n |
| [Pr.112] | Servo OFF command valid/invalid setting [FX5-SSC-G] | At conditions established (Control mode switching) | 112+150n |
| [Pr.122] | Manual pulse generator speed limit mode [FX5-SSC-G] | "[Cd.190] PLC READY" OFF to ON | 121+150n |
| [Pr.123] | Manual pulse generator speed limit value [FX5-SSC-G] | "[Cd.190] PLC READY" OFF to ON | 122+150n<br>123+150n |
| [Pr.127] | Speed limit value input selection at control mode switching | "[Cd.190] PLC READY" OFF to ON | 125+150n |

*In the original, the "Fetch cycle" cell is merged over [Pr.25] to [Pr.41], [Pr.90] to [Pr.95], and [Pr.122] to [Pr.127]. Expanded to each row.

##### Home position return parameters: Home position return basic parameters (原点復帰用パラメータ: 原点復帰基本パラメータ) (11.2 / original p.426)

n: Axis No. - 1

| Item | | Fetch cycle | Buffer memory address |
|---|---|---|---|
| [Pr.43] | Home position return method | "[Cd.190] PLC READY" OFF to ON | 70+150n |
| [Pr.44] | Home position return direction | "[Cd.190] PLC READY" OFF to ON | 71+150n |
| [Pr.45] | Home position address | "[Cd.190] PLC READY" OFF to ON | 72+150n<br>73+150n |
| [Pr.46] | Home position return speed | "[Cd.190] PLC READY" OFF to ON | 74+150n<br>75+150n |
| [Pr.47] | Creep speed [FX5-SSC-S] | "[Cd.190] PLC READY" OFF to ON | 76+150n<br>77+150n |
| [Pr.48] | Home position return retry [FX5-SSC-S] | "[Cd.190] PLC READY" OFF to ON | 78+150n |

*In the original, the "Fetch cycle" cell is merged over [Pr.43] to [Pr.48]. Expanded to each row.

##### Home position return parameters: Home position return detailed parameters (原点復帰用パラメータ: 原点復帰詳細パラメータ) (11.2 / original p.427)

n: Axis No. - 1

| Item | | Fetch cycle | Buffer memory address |
|---|---|---|---|
| [Pr.50] | Setting for the movement amount after proximity dog ON [FX5-SSC-S] | "[Cd.190] PLC READY" OFF to ON | 80+150n<br>81+150n |
| [Pr.51] | Home position return acceleration time selection | "[Cd.190] PLC READY" OFF to ON | 82+150n |
| [Pr.52] | Home position return deceleration time selection | "[Cd.190] PLC READY" OFF to ON | 83+150n |
| [Pr.53] | Home position shift amount [FX5-SSC-S] | "[Cd.190] PLC READY" OFF to ON | 84+150n<br>85+150n |
| [Pr.54] | Home position return torque limit value [FX5-SSC-S] | "[Cd.190] PLC READY" OFF to ON | 86+150n |
| [Pr.55] | Operation setting for incompletion of home position return | "[Cd.190] PLC READY" OFF to ON | 87+150n |
| [Pr.56] | Speed designation during home position shift [FX5-SSC-S] | "[Cd.190] PLC READY" OFF to ON | 88+150n |
| [Pr.57] | Dwell time during home position return retry [FX5-SSC-S] | "[Cd.190] PLC READY" OFF to ON | 89+150n |

*In the original, the "Fetch cycle" cell is merged over [Pr.50] to [Pr.57]. Expanded to each row.

##### Extended parameters (拡張パラメータ) (11.2 / original p.427)

n: Axis No. - 1

| Item | | Fetch cycle | Buffer memory address |
|---|---|---|---|
| [Pr.91] | Optional data monitor: Data type setting 1 | At power supply ON/the CPU module reset (The transmission to the servo amplifier is performed only at the initial communication) | 100+150n |
| [Pr.92] | Optional data monitor: Data type setting 2 | At power supply ON/the CPU module reset (The transmission to the servo amplifier is performed only at the initial communication) | 101+150n |
| [Pr.93] | Optional data monitor: Data type setting 3 | At power supply ON/the CPU module reset (The transmission to the servo amplifier is performed only at the initial communication) | 102+150n |
| [Pr.94] | Optional data monitor: Data type setting 4 | At power supply ON/the CPU module reset (The transmission to the servo amplifier is performed only at the initial communication) | 103+150n |
| [Pr.512] | Optional SDO 1 [FX5-SSC-G] | At request (Servo transient request) | 128+150n<br>129+150n |
| [Pr.591] | Optional data monitor: Data type expansion setting 1 [FX5-SSC-G] | Power supply ON | 92+150n |
| [Pr.592] | Optional data monitor: Data type expansion setting 2 [FX5-SSC-G] | Power supply ON | 93+150n |
| [Pr.593] | Optional data monitor: Data type expansion setting 3 [FX5-SSC-G] | Power supply ON | 94+150n |
| [Pr.594] | Optional data monitor: Data type expansion setting 4 [FX5-SSC-G] | Power supply ON | 95+150n |

*In the original, the "Fetch cycle" cell is merged over [Pr.91] to [Pr.94], and over [Pr.591] to [Pr.594]. Expanded to each row.

#### [Monitor data] (モニタデータ) (11.2 / original p.427-430)

##### System monitor data (システムモニタデータ) (11.2 / original p.427-428)

p: Pointer No. - 1

| Item | | Refresh cycle | Buffer memory address*1 |
|---|---|---|---|
| [Md.3] | Start history*2: Start information | At start | 87010+10p |
| [Md.4] | Start history*2: Start No. | At start | 87011+10p |
| [Md.54] | Start history*2: Start (Year: month) | At start | 87012+10p |
| [Md.5] | Start history*2: Start (Day: hour) | At start | 87013+10p |
| [Md.6] | Start history*2: Start (Minute: second) | At start | 87014+10p |
| [Md.60] | Start history*2: Start (ms) | At start | 87015+10p |
| [Md.7] | Start history*2: Error judgment | At start | 87016+10p |
| [Md.8] | Start history*2: Start history pointer | At start | 87000 |
| [Md.19] | Number of write accesses to flash ROM | Immediate | 4224<br>4225 |
| [Md.50] | Forced stop input | Operation cycle | 4231 |
| [Md.51] | Amplifier-less operation mode status [FX5-SSC-S] | Immediate | 4232 |
| [Md.52] | Communication between amplifiers axes searching flag [FX5-SSC-S] | Immediate | 4234 |
| [Md.53] | SSCNET control status [FX5-SSC-S] | Immediate | 4233 |
| [Md.59] | Module information | At power supply ON | 31332 |
| [Md.130] | F/W version | At power supply ON | 4006<br>4007 |
| [Md.131] | Digital oscilloscope running flag | Main cycle | 4011 |
| [Md.132] | Operation cycle setting | At power supply ON | 4238 |
| [Md.133] | Operation cycle over flag | Immediate | 4239 |
| [Md.134] | Operation time | Operation cycle | 4008 |
| [Md.135] | Maximum operation time | Immediate | 4009 |
| [Md.140] | Module status | b0: "[Cd.190] PLC READY" OFF to ON<br>b1: At power supply ON/the CPU module reset | 31500 |
| [Md.141] | BUSY | At start | 31501 |

*In the original, [Md.3] to [Md.8] have a third item column "Start history*2" merged over the 8 rows (written here as a prefix of the item name). The "Refresh cycle" cell is merged over [Md.3] to [Md.8] ("At start"), [Md.51] to [Md.53] ("Immediate"), and [Md.59] to [Md.130] ("At power supply ON"). Expanded to each row. The table continues from p.427 to p.428 (header repeated on p.428).

*1 Some buffer memory addresses differ from the addresses used on the command generation axis side in synchronous control. For specifications of the command generation axis, refer to "Command Generation Axis" in the following manual.
[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Advanced Synchronous Control)

*2 Displays a value set by the clock function of the CPU module.

##### Axis monitor data (軸モニタデータ) (11.2 / original p.428-430)

n: Axis No. - 1

| Item | | Refresh cycle | Buffer memory address*1 |
|---|---|---|---|
| [Md.20] | Command position value | Operation cycle | 2400+100n<br>2401+100n |
| [Md.21] | Machine feed value | Operation cycle | 2402+100n<br>2403+100n |
| [Md.22] | Speed command | Operation cycle | 2404+100n<br>2405+100n |
| [Md.23] | Axis error No. | Immediate | 2406+100n |
| [Md.24] | Axis warning No. | Immediate | 2407+100n |
| [Md.25] | Valid M code | Immediate | 2408+100n |
| [Md.26] | Axis operation status | Immediate | 2409+100n |
| [Md.27] | Current speed | Immediate | 2410+100n<br>2411+100n |
| [Md.28] | Axis speed command | Operation cycle | 2412+100n<br>2413+100n |
| [Md.29] | Speed-position switching control positioning movement amount | Immediate | 2414+100n<br>2415+100n |
| [Md.30] | External input signal | Operation cycle | 2416+100n |
| [Md.31] | Status | Immediate | 2417+100n |
| [Md.32] | Target value | Immediate | 2418+100n<br>2419+100n |
| [Md.33] | Target speed | Immediate | 2420+100n<br>2421+100n |
| [Md.34] | Movement amount after proximity dog ON [FX5-SSC-S] | Immediate | 2424+100n<br>2425+100n |
| [Md.35] | Torque limit stored value/forward torque limit stored value | Immediate | 2426+100n |
| [Md.36] | Special start data instruction code setting value | Immediate | 2427+100n |
| [Md.37] | Special start data instruction parameter setting value | Immediate | 2428+100n |
| [Md.38] | Start positioning data No. setting value | Immediate | 2429+100n |
| [Md.39] | In speed limit flag | Immediate | 2430+100n |
| [Md.40] | In speed change processing flag | Immediate | 2431+100n |
| [Md.41] | Special start repetition counter | Immediate | 2432+100n |
| [Md.42] | Control system repetition counter | Immediate | 2433+100n |
| [Md.43] | Start data pointer being executed | Immediate | 2434+100n |
| [Md.44] | Positioning data No. being executed | Immediate | 2435+100n |
| [Md.45] | Block No. being executed | At start | 2436+100n |
| [Md.46] | Last executed positioning data No. | Immediate | 2437+100n |
| [Md.47] | Positioning data being executed: Positioning identifier | Immediate | 2438+100n |
| [Md.47] | Positioning data being executed: M code | Immediate | 2439+100n |
| [Md.47] | Positioning data being executed: Dwell time | Immediate | 2440+100n |
| [Md.47] | Positioning data being executed: Command speed | Immediate | 2442+100n<br>2443+100n |
| [Md.47] | Positioning data being executed: Positioning address | Immediate | 2444+100n<br>2445+100n |
| [Md.47] | Positioning data being executed: Arc address | Immediate | 2446+100n<br>2447+100n |
| [Md.47] | Positioning data being executed: Axis to be interpolated | Immediate | 2496+100n<br>2497+100n |
| [Md.48] | Deceleration start flag | Immediate | 2499+100n |
| [Md.62] | Amount of the manual pulser driving carrying over movement [FX5-SSC-G] | Immediate | 2422+100n<br>2423+100n |
| [Md.100] | Home position return re-travel value [FX5-SSC-S] | At conditions established (At home position return re-travel) | 2448+100n<br>2449+100n |
| [Md.101] | Actual position value | Operation cycle | 2450+100n<br>2451+100n |
| [Md.102] | Deviation counter value | Operation cycle | 2452+100n<br>2453+100n |
| [Md.103] | Motor rotation speed | Operation cycle | 2454+100n<br>2455+100n |
| [Md.104] | Motor current value | Operation cycle | 2456+100n |
| [Md.106] | Servo amplifier software No. [FX5-SSC-S] | At servo amplifier's power supply ON | 2464+100n<br>2465+100n<br>2466+100n<br>2467+100n<br>2468+100n<br>2469+100n |
| [Md.107] | Parameter error No. [FX5-SSC-S] | Immediate | 2470+100n |
| [Md.108] | Servo status1 | Operation cycle | 2477+100n |
| [Md.109] | Regenerative load ratio/Optional data monitor output 1 | Operation cycle | 2478+100n |
| [Md.110] | Effective load torque/Optional data monitor output 2 | Operation cycle | 2479+100n |
| [Md.111] | Peak torque ratio/Optional data monitor output 3 | Operation cycle | 2480+100n |
| [Md.112] | Optional data monitor output 4 | Operation cycle | 2481+100n |
| [Md.113] | Semi/Fully closed loop status | Operation cycle | 2487+100n |
| [Md.114] | Servo alarm | Immediate | 2488+100n |
| [Md.115] | Servo alarm detail number [FX5-SSC-G] | Immediate | 2489+100n |
| [Md.116] | Encoder option information | At servo amplifier's power supply ON | 2490+100n |
| [Md.117] | Statusword [FX5-SSC-G] | Operation cycle | 2472+100n |
| [Md.119] | Servo status2 | Operation cycle | 2476+100n |
| [Md.120] | Reverse torque limit stored value | Immediate | 2491+100n |
| [Md.122] | Speed during command | Operation cycle (Only at the speed control mode/the continuous operation to torque control mode) | 2492+100n<br>2493+100n |
| [Md.123] | Torque during command | Operation cycle (Only at the torque control mode/the continuous operation to torque control mode) | 2494+100n |
| [Md.124] | Control mode switching status | Operation cycle (Only at the continuous operation to torque control mode) | 2495+100n |
| [Md.125] | Servo status3 | Operation cycle | 2458+100n |
| [Md.126] | Servo status4 [FX5-SSC-G] | Operation cycle | 2459+100n |
| [Md.127] | Servo status5 [FX5-SSC-S] | Operation cycle | 2460+100n |
| [Md.160] | Optional SDO transfer result 1 [FX5-SSC-G] | At request (Command request) | 59308+100n<br>59309+100n |
| [Md.164] | Optional SDO transfer status 1 [FX5-SSC-G] | At request (Command request) | 59312+100n |
| [Md.190] | Controller position value restoration complete status [FX5-SSC-G] | 16.0 ms | 59327+100n |
| [Md.500] | Servo status7 [FX5-SSC-S] | Operation cycle | 59300+100n |
| [Md.502] | Driver operation alarm No. [FX5-SSC-S] | Immediate | 59302+100n |
| [Md.514] | HPR operating status [FX5-SSC-G] | Operation cycle | 2457+100n |

*In the original, [Md.47] "Positioning data being executed" is merged over 7 rows with a sub-item column (Positioning identifier / M code / Dwell time / Command speed / Positioning address / Arc address / Axis to be interpolated); written here as "item: sub-item" in each row. The "Refresh cycle" cell is merged over [Md.20] to [Md.22] ("Operation cycle"), [Md.23] to [Md.27] ("Immediate"), [Md.31] to [Md.44] ("Immediate"), [Md.46] to [Md.62] ("Immediate", including all 7 rows of [Md.47]), [Md.101] to [Md.104] ("Operation cycle"), [Md.108] to [Md.113] ("Operation cycle"), [Md.114] to [Md.115] ("Immediate"), [Md.117] to [Md.119] ("Operation cycle"), [Md.125] to [Md.127] ("Operation cycle"), and [Md.160] to [Md.164] ("At request (Command request)"). Expanded to each row. The table continues over p.428-430 (header repeated on each page).

*1 Some buffer memory addresses differ from the addresses used on the command generation axis side in synchronous control. For specifications of the command generation axis, refer to "Command Generation Axis" in the following manual.
[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Advanced Synchronous Control)

#### [Control data] (制御データ) (11.2 / original p.430-432)

##### System control data (システム制御データ) (11.2 / original p.430)

| Item | | Fetch cycle | Buffer memory address |
|---|---|---|---|
| [Cd.1] | Flash ROM write request | 103 ms [FX5-SSC-S]<br>116 ms [FX5-SSC-G] | 5900 |
| [Cd.2] | Parameter initialization request | 103 ms [FX5-SSC-S]<br>116 ms [FX5-SSC-G] | 5901 |
| [Cd.41] | Deceleration start flag valid | "[Cd.190] PLC READY" OFF to ON | 5905 |
| [Cd.42] | Stop command processing for deceleration stop selection | At conditions established (At deceleration stop causes occurrence) | 5907 |
| [Cd.44] | External input signal operation device (Axis 1 to 8) | Operation cycle | 5928 (Axis 1 to 4)<br>5929 (Axis 5 to 8) |
| [Cd.55] | Input value for manual pulse generator via CPU [FX5-SSC-G] | 8.0 ms | 5946<br>5947 |
| [Cd.102] | SSCNET control command [FX5-SSC-S] | 3.5 ms | 5932 |
| [Cd.137] | Amplifier-less operation mode switching request [FX5-SSC-S] | 3.5 ms | 5926 |
| [Cd.158] | Forced stop input [FX5-SSC-G] | Operation cycle | 5945 |
| [Cd.190] | PLC READY | Operation cycle | 5950 |
| [Cd.191] | All axis servo ON | Operation cycle | 5951 |

*In the original, the "Fetch cycle" cell is merged over [Cd.1] to [Cd.2], [Cd.102] to [Cd.137], and [Cd.158] to [Cd.191]. Expanded to each row.

##### Axis control data (軸制御データ) (11.2 / original p.430-432)

n: Axis No. - 1

| Item | | Fetch cycle | Buffer memory address |
|---|---|---|---|
| [Cd.3] | Positioning start No. | At start | 4300+100n |
| [Cd.4] | Positioning starting point No. | At start | 4301+100n |
| [Cd.5] | Axis error reset | 14.2 ms [FX5-SSC-S]<br>16.0 ms [FX5-SSC-G] | 4302+100n |
| [Cd.6] | Restart command | 14.2 ms [FX5-SSC-S]<br>16.0 ms [FX5-SSC-G] | 4303+100n |
| [Cd.7] | M code OFF request | Operation cycle | 4304+100n |
| [Cd.8] | External command valid | At request | 4305+100n |
| [Cd.9] | New position value | At request | 4306+100n<br>4307+100n |
| [Cd.10] | New acceleration time value | At request | 4308+100n<br>4309+100n |
| [Cd.11] | New deceleration time value | At request | 4310+100n<br>4311+100n |
| [Cd.12] | Acceleration/deceleration time change value during speed change, enable/disable | At request | 4312+100n |
| [Cd.13] | Positioning operation speed override | Operation cycle | 4313+100n |
| [Cd.14] | New speed value | At request | 4314+100n<br>4315+100n |
| [Cd.15] | Speed change request | Operation cycle | 4316+100n |
| [Cd.16] | Inching movement amount | At start | 4317+100n |
| [Cd.17] | JOG speed | At start | 4318+100n<br>4319+100n |
| [Cd.18] | Interrupt request during continuous operation | Operation cycle | 4320+100n |
| [Cd.19] | Home position return request flag OFF request | 14.2 ms [FX5-SSC-S]<br>16.0 ms [FX5-SSC-G] | 4321+100n |
| [Cd.20] | Manual pulse generator 1 pulse input magnification | Operation cycle (At manual pulse generator enabled) | 4322+100n<br>4323+100n |
| [Cd.21] | Manual pulse generator enable flag | Operation cycle | 4324+100n |
| [Cd.22] | New torque value/forward new torque value | Operation cycle | 4325+100n |
| [Cd.23] | Speed-position switching control movement amount change register | At request | 4326+100n<br>4327+100n |
| [Cd.24] | Speed-position switching enable flag | At request | 4328+100n |
| [Cd.25] | Position-speed switching control speed change register | At request | 4330+100n<br>4331+100n |
| [Cd.26] | Position-speed switching enable flag | At request | 4332+100n |
| [Cd.27] | Target position change value (New address) | At request | 4334+100n<br>4335+100n |
| [Cd.28] | Target position change value (New speed) | At request | 4336+100n<br>4337+100n |
| [Cd.29] | Target position change request flag | Operation cycle | 4338+100n |
| [Cd.30] | Simultaneous starting own axis start data No. | At start | 4340+100n |
| [Cd.31] | Simultaneous starting axis start data No.1 | At start | 4341+100n |
| [Cd.32] | Simultaneous starting axis start data No.2 | At start | 4342+100n |
| [Cd.33] | Simultaneous starting axis start data No.3 | At start | 4343+100n |
| [Cd.34] | Step mode | At start | 4344+100n |
| [Cd.35] | Step valid flag | At start | 4345+100n |
| [Cd.36] | Step start information | 14.2 ms [FX5-SSC-S]<br>16.0 ms [FX5-SSC-G] | 4346+100n |
| [Cd.37] | Skip command | Operation cycle (During positioning operation) | 4347+100n |
| [Cd.38] | Teaching data selection | At request | 4348+100n |
| [Cd.39] | Teaching positioning data No. | 103 ms [FX5-SSC-S]<br>116 ms [FX5-SSC-G] | 4349+100n |
| [Cd.40] | ABS direction in degrees | At start | 4350+100n |
| [Cd.43] | Simultaneous starting axis | At start | 4368+100n<br>4369+100n |
| [Cd.45] | Speed-position switching device selection | At start | 4366+100n |
| [Cd.46] | Speed-position switching command | 0.888 ms [FX5-SSC-S]<br>Operation cycle [FX5-SSC-G] | 4367+100n |
| [Cd.100] | Servo OFF command | Operation cycle | 4351+100n |
| [Cd.101] | Torque output setting value | At start | 4352+100n |
| [Cd.108] | Gain switching command flag | Operation cycle | 4359+100n |
| [Cd.112] | Torque change function switching request | Operation cycle | 4363+100n |
| [Cd.113] | New reverse torque value | Operation cycle | 4364+100n |
| [Cd.130] | Servo parameter read/write request [FX5-SSC-S] | Main cycle | 4354+100n |
| [Cd.131] | Parameter No. (Setting for servo parameters to be changed) [FX5-SSC-S] | At request | 4355+100n |
| [Cd.132] | Change data [FX5-SSC-S] | At request | 4356+100n<br>4357+100n |
| [Cd.133] | Semi/Fully closed loop switching request | Operation cycle (The servo amplifiers for fully closed loop control only) | 4358+100n |
| [Cd.136] | PI-PID switching request | Operation cycle | 4365+100n |
| [Cd.138] | Control mode switching request | Operation cycle | 4374+100n |
| [Cd.139] | Control mode setting | At request (Mode switching) | 4375+100n |
| [Cd.140] | Command speed at speed control mode | Operation cycle (At speed control mode) | 4376+100n<br>4377+100n |
| [Cd.141] | Acceleration time at speed control mode | At request (Mode switching) | 4378+100n |
| [Cd.142] | Deceleration time at speed control mode | At request (Mode switching) | 4379+100n |
| [Cd.143] | Command torque at torque control mode | Operation cycle (At torque control mode) | 4380+100n |
| [Cd.144] | Torque time constant at torque control mode (Forward direction) | At request (Mode switching) | 4381+100n |
| [Cd.145] | Torque time constant at torque control mode (Negative direction) | At request (Mode switching) | 4382+100n |
| [Cd.146] | Speed limit value at torque control mode | Operation cycle (At torque control mode) | 4384+100n<br>4385+100n |
| [Cd.147] | Speed limit value at continuous operation to torque control mode | Operation cycle (At continuous operation to torque control mode) | 4386+100n<br>4387+100n |
| [Cd.148] | Acceleration time at continuous operation to torque control mode | At request (Mode switching) | 4388+100n |
| [Cd.149] | Deceleration time at continuous operation to torque control mode | At request (Mode switching) | 4389+100n |
| [Cd.150] | Target torque at continuous operation to torque control mode | Operation cycle (At continuous operation to torque control mode) | 4390+100n |
| [Cd.151] | Torque time constant at continuous operation to torque control mode (Forward direction) | At request (Mode switching) | 4391+100n |
| [Cd.152] | Torque time constant at continuous operation to torque control mode (Negative direction) | At request (Mode switching) | 4392+100n |
| [Cd.153] | Control mode auto-shift selection | At request (Mode switching) | 4393+100n |
| [Cd.154] | Control mode auto-shift parameter | At request (Mode switching) | 4394+100n<br>4395+100n |
| [Cd.180] | Axis stop | Operation cycle | 30100+10n |
| [Cd.181] | Forward run JOG start | Operation cycle | 30101+10n |
| [Cd.182] | Reverse run JOG start | Operation cycle | 30102+10n |
| [Cd.183] | Execution prohibition flag | At start | 30103+10n |
| [Cd.184] | Positioning start | Operation cycle | 30104+10n |

*In the original, the "Fetch cycle" cell is merged over [Cd.3] to [Cd.4] ("At start"), [Cd.5] to [Cd.6], [Cd.8] to [Cd.12] ("At request"), [Cd.16] to [Cd.17] ("At start"), [Cd.21] to [Cd.22] ("Operation cycle"), [Cd.23] to [Cd.28] ("At request"), [Cd.30] to [Cd.35] ("At start"), [Cd.40] to [Cd.45] ("At start"), [Cd.108] to [Cd.113] ("Operation cycle"), [Cd.131] to [Cd.132] ("At request"), [Cd.136] to [Cd.138] ("Operation cycle"), [Cd.141] to [Cd.142], [Cd.144] to [Cd.145], [Cd.148] to [Cd.149], [Cd.151] to [Cd.154] ("At request (Mode switching)"), and [Cd.180] to [Cd.182] ("Operation cycle"). Expanded to each row. The table continues over p.430-432 (header repeated on each page).

##### Axis control data (transient function) [FX5-SSC-G] (軸制御データ(トランジェント機能)[FX5-SSC-G]) (11.2 / original p.432)

n: Axis No. -1

| Item | | Fetch cycle | Buffer memory address |
|---|---|---|---|
| [Cd.160] | Optional SDO transfer request 1 | Main cycle | 57520+30n |
| [Cd.164] | Optional SDO transfer data 1 | At request (Command request) | 57522+30n<br>57523+30n<br>57524+30n<br>57525+30n |

#### [Positioning data] (位置決めデータ) (11.2 / original p.433)

##### Positioning data (位置決め用データ) (11.2 / original p.433)

n: Axis No. - 1

| Memory area | Item | | Sub-item | Buffer memory address |
|---|---|---|---|---|
| Positioning data No.1 | [Da.1] | Operation pattern | Positioning identifier | 6000+1000n |
| Positioning data No.1 | [Da.2] | Control method | Positioning identifier | 6000+1000n |
| Positioning data No.1 | [Da.3] | Acceleration time No. | Positioning identifier | 6000+1000n |
| Positioning data No.1 | [Da.4] | Deceleration time No. | Positioning identifier | 6000+1000n |
| Positioning data No.1 | [Da.6] | Positioning address/movement amount | | 6006+1000n<br>6007+1000n |
| Positioning data No.1 | [Da.7] | Arc address | | 6008+1000n<br>6009+1000n |
| Positioning data No.1 | [Da.8] | Command speed | | 6004+1000n<br>6005+1000n |
| Positioning data No.1 | [Da.9] | Dwell time/JUMP destination positioning data No. | | 6002+1000n |
| Positioning data No.1 | [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | | 6001+1000n |
| Positioning data No.1 | [Da.20] | Axis to be interpolated No.1 | Axis to be interpolated | 71000+1000n<br>71001+1000n |
| Positioning data No.1 | [Da.21] | Axis to be interpolated No.2 | Axis to be interpolated | 71000+1000n<br>71001+1000n |
| Positioning data No.1 | [Da.22] | Axis to be interpolated No.3 | Axis to be interpolated | 71000+1000n<br>71001+1000n |
| No.2 | [Da.1] to [Da.22] | [Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions<br>[Da.20] Axis to be interpolated No.1<br>[Da.21] Axis to be interpolated No.2<br>[Da.22] Axis to be interpolated No.3 | | 6010+1000n<br>⋮<br>6019+1000n<br>71010+1000n<br>71011+1000n |
| No.3 | [Da.1] to [Da.22] | (Same items as No.2: merged cell in the original) | | 6020+1000n<br>⋮<br>6029+1000n<br>71020+1000n<br>71021+1000n |
| ⋮ | [Da.1] to [Da.22] | (Same items as No.2: merged cell in the original) | | ⋮ |
| No.100 | [Da.1] to [Da.22] | (Same items as No.2: merged cell in the original) | | 6990+1000n<br>⋮<br>6999+1000n<br>71990+1000n<br>71991+1000n |
| No.101<br>⋮<br>No.600 | [Da.1] to [Da.22] | (Same items as No.2: merged cell in the original) | | Set with the engineering tool. |

*In the original, for Positioning data No.1, the sub-item "Positioning identifier" and the address "6000+1000n" are merged over [Da.1] to [Da.4] (4 items in 1 word), and the sub-item "Axis to be interpolated" and the address "71000+1000n / 71001+1000n" are merged over [Da.20] to [Da.22]. "Positioning data No.1" in the Memory area column is merged over all 12 rows. For No.2 to No.600, the item column is one merged cell listing [Da.1] to [Da.22] spanning all rows. Expanded to each row. "⋮" is as printed in the original (No.4 to No.99 etc. are omitted in the original itself). Rows with an empty Sub-item: the item name spans into the sub-item column in the original.

#### [Block start data] (ブロック始動データ) (11.2 / original p.434)

##### Positioning data (Block start data) (位置決め用データ(ブロック始動データ)) (11.2 / original p.434)

n: Axis No. - 1

| Memory area | Group | Item No. | Item | Sub-item | Buffer memory address (left column) | Buffer memory address (right column) |
|---|---|---|---|---|---|---|
| Starting block 0 | Block start data 1st point | [Da.11]<br>[Da.12] | Shape<br>Start data No. | | 22000+400n | — |
| Starting block 0 | Block start data 1st point | [Da.13]<br>[Da.14] | Special start instruction<br>Parameter | | — | 22050+400n |
| Starting block 0 | Block start data 2nd point | | | | 22001+400n | 22051+400n |
| Starting block 0 | Block start data 3rd point | | | | 22002+400n | 22052+400n |
| Starting block 0 | ⋮ | | | | ⋮ | |
| Starting block 0 | Block start data 50th point | | | | 22049+400n | 22099+400n |
| Starting block 0 | Condition data No.1 | [Da.15] | Condition target | | 22100+400n | |
| Starting block 0 | Condition data No.1 | [Da.16] | Condition operator | | 22100+400n | |
| Starting block 0 | Condition data No.1 | [Da.17] | Address | | 22102+400n<br>22103+400n | |
| Starting block 0 | Condition data No.1 | [Da.18] | Parameter 1 | | 22104+400n<br>22105+400n | |
| Starting block 0 | Condition data No.1 | [Da.19] | Parameter 2 | | 22106+400n<br>22107+400n | |
| Starting block 0 | Condition data No.1 | [Da.23] | Number of simultaneously starting axes | Simultaneously starting axis | 22108+400n<br>22109+400n | |
| Starting block 0 | Condition data No.1 | [Da.24] | Simultaneously starting axis No.1 | Simultaneously starting axis | 22108+400n<br>22109+400n | |
| Starting block 0 | Condition data No.1 | [Da.25] | Simultaneously starting axis No.2 | Simultaneously starting axis | 22108+400n<br>22109+400n | |
| Starting block 0 | Condition data No.1 | [Da.26] | Simultaneously starting axis No.3 | Simultaneously starting axis | 22108+400n<br>22109+400n | |
| Starting block 0 | Condition data No.2 | | | | 22110+400n<br>⋮<br>22119+400n | |
| Starting block 0 | Condition data No.3 | | | | 22120+400n<br>⋮<br>22129+400n | |
| Starting block 0 | ⋮ | | | | ⋮ | |
| Starting block 0 | Condition data No.10 | | | | 22190+400n<br>⋮<br>22199+400n | |
| Starting block 1 | Block start data | | | | 22200+400n<br>⋮<br>22299+400n | |
| Starting block 1 | Condition data | | | | 22300+400n<br>⋮<br>22399+400n | |
| Starting block 2 | Block start data | | | | Set with the engineering tool. | |
| Starting block 2 | Condition data | | | | Set with the engineering tool. | |
| Starting block 3 | Block start data | | | | Set with the engineering tool. | |
| Starting block 3 | Condition data | | | | Set with the engineering tool. | |
| Starting block 4 | Block start data | | | | Set with the engineering tool. | |
| Starting block 4 | Condition data | | | | Set with the engineering tool. | |

*In the original, the "Item" header spans the Group / Item No. / Item / Sub-item columns, and the "Buffer memory address" header spans two columns (left/right). Merged cells: the Memory area column (Starting block 0 to 4) is merged over all rows of each block. "Block start data 1st point" is merged over 2 rows; in the [Da.11]/[Da.12] row the left column is 22000+400n and the right column is "—", in the [Da.13]/[Da.14] row the left column is "—" and the right column is 22050+400n. For the 2nd point and later, the left column corresponds to [Da.11]/[Da.12] and the right column to [Da.13]/[Da.14] (as laid out in the original). "Condition data No.1" is merged over 9 rows; the address 22100+400n is merged over [Da.15] to [Da.16]; the sub-item "Simultaneously starting axis" and the address "22108+400n / 22109+400n" are merged over [Da.23] to [Da.26]. From Condition data No.1 onward and for blocks 1 to 4, the address spans both the left and right columns in the original (written in the left column; right column empty). "Set with the engineering tool." is merged over the 6 rows of Starting blocks 2 to 4. Expanded to each row. "⋮" is as printed in the original.

#### Servo parameters (サーボパラメータ) (11.2 / original p.435-443)

The following shows the relation between the buffer memory addresses of servo parameters and the various items.
Since the servo parameters of MR-J5(W)-B are not in the buffer memory, use GX Works3 or axis control data to set them. For details, refer to the following.
→Page 845 Connection with MR-J5(W)-B
The setting range is different depending on the servo amplifier model. Refer to the manuals of each servo amplifier for details.

##### Servo parameters [FX5-SSC-S] (サーボパラメータ[FX5-SSC-S]) (11.2 / original p.435-443)

n: Axis No. - 1

| Item | Servo amplifier parameter No. | Buffer memory address |
|---|---|---|
| [Pr.100] Servo series | — | 28400+100n |
| — | PA01 | 28401+100n |
| — | PA02 | 28402+100n |
| — | PA03 | 28403+100n |
| — | PA04 | 28404+100n |
| — | PA05 | 28405+100n |
| — | PA06 | 28406+100n |
| — | PA07 | 28407+100n |
| — | PA08 | 28408+100n |
| — | PA09 | 28409+100n |
| — | PA10 | 28410+100n |
| — | PA11 | 28411+100n |
| — | PA12 | 28412+100n |
| — | PA13 | 28413+100n |
| — | PA14 | 28414+100n |
| — | PA15 | 28415+100n |
| — | PA16 | 28416+100n |
| — | PA17 | 28417+100n |
| — | PA18 | 28418+100n |
| — | PA19 | 64464+70n |
| — | PA20 | 64400+70n |
| — | PA21 | 64401+70n |
| — | PA22 | 64402+70n |
| — | PA23 | 64403+70n |
| — | PA24 | 64404+70n |
| — | PA25 | 64405+70n |
| — | PA26 | 64406+70n |
| — | PA27 | 64407+70n |
| — | PA28 | 64408+70n |
| — | PA29 | 64409+70n |
| — | PA30 | 64410+70n |
| — | PA31 | 64411+70n |
| — | PA32 | 64412+70n |
| — | PB01 | 28419+100n |
| — | PB02 | 28420+100n |
| — | PB03 | 28421+100n |
| — | PB04 | 28422+100n |
| — | PB05 | 28423+100n |
| — | PB06 | 28424+100n |
| — | PB07 | 28425+100n |
| — | PB08 | 28426+100n |
| — | PB09 | 28427+100n |
| — | PB10 | 28428+100n |
| — | PB11 | 28429+100n |
| — | PB12 | 28430+100n |
| — | PB13 | 28431+100n |
| — | PB14 | 28432+100n |
| — | PB15 | 28433+100n |
| — | PB16 | 28434+100n |
| — | PB17 | 28435+100n |
| — | PB18 | 28436+100n |
| — | PB19 | 28437+100n |
| — | PB20 | 28438+100n |
| — | PB21 | 28439+100n |
| — | PB22 | 28440+100n |
| — | PB23 | 28441+100n |
| — | PB24 | 28442+100n |
| — | PB25 | 28443+100n |
| — | PB26 | 28444+100n |
| — | PB27 | 28445+100n |
| — | PB28 | 28446+100n |
| — | PB29 | 28447+100n |
| — | PB30 | 28448+100n |
| — | PB31 | 28449+100n |
| — | PB32 | 28450+100n |
| — | PB33 | 28451+100n |
| — | PB34 | 28452+100n |
| — | PB35 | 28453+100n |
| — | PB36 | 28454+100n |
| — | PB37 | 28455+100n |
| — | PB38 | 28456+100n |
| — | PB39 | 28457+100n |
| — | PB40 | 28458+100n |
| — | PB41 | 28459+100n |
| — | PB42 | 28460+100n |
| — | PB43 | 28461+100n |
| — | PB44 | 28462+100n |
| — | PB45 | 28463+100n |
| — | PB46 | 64413+70n |
| — | PB47 | 64414+70n |
| — | PB48 | 64415+70n |
| — | PB49 | 64416+70n |
| — | PB50 | 64417+70n |
| — | PB51 | 64418+70n |
| — | PB52 | 64419+70n |
| — | PB53 | 64420+70n |
| — | PB54 | 64421+70n |
| — | PB55 | 64422+70n |
| — | PB56 | 64423+70n |
| — | PB57 | 64424+70n |
| — | PB58 | 64425+70n |
| — | PB59 | 64426+70n |
| — | PB60 | 64427+70n |
| — | PB61 | 64428+70n |
| — | PB62 | 64429+70n |
| — | PB63 | 64430+70n |
| — | PB64 | 64431+70n |
| — | PC01 | 28464+100n |
| — | PC02 | 28465+100n |
| — | PC03 | 28466+100n |
| — | PC04 | 28467+100n |
| — | PC05 | 28468+100n |
| — | PC06 | 28469+100n |
| — | PC07 | 28470+100n |
| — | PC08 | 28471+100n |
| — | PC09 | 28472+100n |
| — | PC10 | 28473+100n |
| — | PC11 | 28474+100n |
| — | PC12 | 28475+100n |
| — | PC13 | 28476+100n |
| — | PC14 | 28477+100n |
| — | PC15 | 28478+100n |
| — | PC16 | 28479+100n |
| — | PC17 | 28480+100n |
| — | PC18 | 28481+100n |
| — | PC19 | 28482+100n |
| — | PC20 | 28483+100n |
| — | PC21 | 28484+100n |
| — | PC22 | 28485+100n |
| — | PC23 | 28486+100n |
| — | PC24 | 28487+100n |
| — | PC25 | 28488+100n |
| — | PC26 | 28489+100n |
| — | PC27 | 28490+100n |
| — | PC28 | 28491+100n |
| — | PC29 | 28492+100n |
| — | PC30 | 28493+100n |
| — | PC31 | 28494+100n |
| — | PC32 | 28495+100n |
| — | PC33 | 64432+70n |
| — | PC34 | 64433+70n |
| — | PC35 | 64434+70n |
| — | PC36 | 64435+70n |
| — | PC37 | 64436+70n |
| — | PC38 | 64437+70n |
| — | PC39 | 64438+70n |
| — | PC40 | 64439+70n |
| — | PC41 | 64440+70n |
| — | PC42 | 64441+70n |
| — | PC43 | 64442+70n |
| — | PC44 | 64443+70n |
| — | PC45 | 64444+70n |
| — | PC46 | 64445+70n |
| — | PC47 | 64446+70n |
| — | PC48 | 64447+70n |
| — | PC49 | 64448+70n |
| — | PC50 | 64449+70n |
| — | PC51 | 64450+70n |
| — | PC52 | 64451+70n |
| — | PC53 | 64452+70n |
| — | PC54 | 64453+70n |
| — | PC55 | 64454+70n |
| — | PC56 | 64455+70n |
| — | PC57 | 64456+70n |
| — | PC58 | 64457+70n |
| — | PC59 | 64458+70n |
| — | PC60 | 64459+70n |
| — | PC61 | 64460+70n |
| — | PC62 | 64461+70n |
| — | PC63 | 64462+70n |
| — | PC64 | 64463+70n |
| — | PD01 | 65520+340n |
| — | PD02 | 65521+340n |
| — | PD03 | 65522+340n |
| — | PD04 | 65523+340n |
| — | PD05 | 65524+340n |
| — | PD06 | 65525+340n |
| — | PD07 | 65526+340n |
| — | PD08 | 65527+340n |
| — | PD09 | 65528+340n |
| — | PD10 | 65529+340n |
| — | PD11 | 65530+340n |
| — | PD12 | 65531+340n |
| — | PD13 | 65532+340n |
| — | PD14 | 65533+340n |
| — | PD15 | 65534+340n |
| — | PD16 | 65535+340n |
| — | PD17 | 65536+340n |
| — | PD18 | 65537+340n |
| — | PD19 | 65538+340n |
| — | PD20 | 65539+340n |
| — | PD21 | 65540+340n |
| — | PD22 | 65541+340n |
| — | PD23 | 65542+340n |
| — | PD24 | 65543+340n |
| — | PD25 | 65544+340n |
| — | PD26 | 65545+340n |
| — | PD27 | 65546+340n |
| — | PD28 | 65547+340n |
| — | PD29 | 65548+340n |
| — | PD30 | 65549+340n |
| — | PD31 | 65550+340n |
| — | PD32 | 65551+340n |
| — | PD33 | 65552+340n |
| — | PD34 | 65553+340n |
| — | PD35 | 65554+340n |
| — | PD36 | 65555+340n |
| — | PD37 | 65556+340n |
| — | PD38 | 65557+340n |
| — | PD39 | 65558+340n |
| — | PD40 | 65559+340n |
| — | PD41 | 65560+340n |
| — | PD42 | 65561+340n |
| — | PD43 | 65562+340n |
| — | PD44 | 65563+340n |
| — | PD45 | 65564+340n |
| — | PD46 | 65565+340n |
| — | PD47 | 65566+340n |
| — | PD48 | 65567+340n |
| — | PE01 | 65568+340n |
| — | PE02 | 65569+340n |
| — | PE03 | 65570+340n |
| — | PE04 | 65571+340n |
| — | PE05 | 65572+340n |
| — | PE06 | 65573+340n |
| — | PE07 | 65574+340n |
| — | PE08 | 65575+340n |
| — | PE09 | 65576+340n |
| — | PE10 | 65577+340n |
| — | PE11 | 65578+340n |
| — | PE12 | 65579+340n |
| — | PE13 | 65580+340n |
| — | PE14 | 65581+340n |
| — | PE15 | 65582+340n |
| — | PE16 | 65583+340n |
| — | PE17 | 65584+340n |
| — | PE18 | 65585+340n |
| — | PE19 | 65586+340n |
| — | PE20 | 65587+340n |
| — | PE21 | 65588+340n |
| — | PE22 | 65589+340n |
| — | PE23 | 65590+340n |
| — | PE24 | 65591+340n |
| — | PE25 | 65592+340n |
| — | PE26 | 65593+340n |
| — | PE27 | 65594+340n |
| — | PE28 | 65595+340n |
| — | PE29 | 65596+340n |
| — | PE30 | 65597+340n |
| — | PE31 | 65598+340n |
| — | PE32 | 65599+340n |
| — | PE33 | 65600+340n |
| — | PE34 | 65601+340n |
| — | PE35 | 65602+340n |
| — | PE36 | 65603+340n |
| — | PE37 | 65604+340n |
| — | PE38 | 65605+340n |
| — | PE39 | 65606+340n |
| — | PE40 | 65607+340n |
| — | PE41 | 65608+340n |
| — | PE42 | 65609+340n |
| — | PE43 | 65610+340n |
| — | PE44 | 65611+340n |
| — | PE45 | 65612+340n |
| — | PE46 | 65613+340n |
| — | PE47 | 65614+340n |
| — | PE48 | 65615+340n |
| — | PE49 | 65616+340n |
| — | PE50 | 65617+340n |
| — | PE51 | 65618+340n |
| — | PE52 | 65619+340n |
| — | PE53 | 65620+340n |
| — | PE54 | 65621+340n |
| — | PE55 | 65622+340n |
| — | PE56 | 65623+340n |
| — | PE57 | 65624+340n |
| — | PE58 | 65625+340n |
| — | PE59 | 65626+340n |
| — | PE60 | 65627+340n |
| — | PE61 | 65628+340n |
| — | PE62 | 65629+340n |
| — | PE63 | 65630+340n |
| — | PE64 | 65631+340n |
| — | PS01 | 65712+340n |
| — | PS02 | 65713+340n |
| — | PS03 | 65714+340n |
| — | PS04 | 65715+340n |
| — | PS05 | 65716+340n |
| — | PS06 | 65717+340n |
| — | PS07 | 65718+340n |
| — | PS08 | 65719+340n |
| — | PS09 | 65720+340n |
| — | PS10 | 65721+340n |
| — | PS11 | 65722+340n |
| — | PS12 | 65723+340n |
| — | PS13 | 65724+340n |
| — | PS14 | 65725+340n |
| — | PS15 | 65726+340n |
| — | PS16 | 65727+340n |
| — | PS17 | 65728+340n |
| — | PS18 | 65729+340n |
| — | PS19 | 65730+340n |
| — | PS20 | 65731+340n |
| — | PS21 | 65732+340n |
| — | PS22 | 65733+340n |
| — | PS23 | 65734+340n |
| — | PS24 | 65735+340n |
| — | PS25 | 65736+340n |
| — | PS26 | 65737+340n |
| — | PS27 | 65738+340n |
| — | PS28 | 65739+340n |
| — | PS29 | 65740+340n |
| — | PS30 | 65741+340n |
| — | PS31 | 65742+340n |
| — | PS32 | 65743+340n |
| — | PF01 | 65632+340n |
| — | PF02 | 65633+340n |
| — | PF03 | 65634+340n |
| — | PF04 | 65635+340n |
| — | PF05 | 65636+340n |
| — | PF06 | 65637+340n |
| — | PF07 | 65638+340n |
| — | PF08 | 65639+340n |
| — | PF09 | 65640+340n |
| — | PF10 | 65641+340n |
| — | PF11 | 65642+340n |
| — | PF12 | 65643+340n |
| — | PF13 | 65644+340n |
| — | PF14 | 65645+340n |
| — | PF15 | 65646+340n |
| — | PF16 | 65647+340n |
| — | PF17 | 65648+340n |
| — | PF18 | 65649+340n |
| — | PF19 | 65650+340n |
| — | PF20 | 65651+340n |
| — | PF21 | 65652+340n |
| — | PF22 | 65653+340n |
| — | PF23 | 65654+340n |
| — | PF24 | 65655+340n |
| — | PF25 | 65656+340n |
| — | PF26 | 65657+340n |
| — | PF27 | 65658+340n |
| — | PF28 | 65659+340n |
| — | PF29 | 65660+340n |
| — | PF30 | 65661+340n |
| — | PF31 | 65662+340n |
| — | PF32 | 65663+340n |
| — | PF33 | 65664+340n |
| — | PF34 | 65665+340n |
| — | PF35 | 65666+340n |
| — | PF36 | 65667+340n |
| — | PF37 | 65668+340n |
| — | PF38 | 65669+340n |
| — | PF39 | 65670+340n |
| — | PF40 | 65671+340n |
| — | PF41 | 65672+340n |
| — | PF42 | 65673+340n |
| — | PF43 | 65674+340n |
| — | PF44 | 65675+340n |
| — | PF45 | 65676+340n |
| — | PF46 | 65677+340n |
| — | PF47 | 65678+340n |
| — | PF48 | 65679+340n |
| — | Po01 | 65680+340n |
| — | Po02 | 65681+340n |
| — | Po03 | 65682+340n |
| — | Po04 | 65683+340n |
| — | Po05 | 65684+340n |
| — | Po06 | 65685+340n |
| — | Po07 | 65686+340n |
| — | Po08 | 65687+340n |
| — | Po09 | 65688+340n |
| — | Po10 | 65689+340n |
| — | Po11 | 65690+340n |
| — | Po12 | 65691+340n |
| — | Po13 | 65692+340n |
| — | Po14 | 65693+340n |
| — | Po15 | 65694+340n |
| — | Po16 | 65695+340n |
| — | Po17 | 65696+340n |
| — | Po18 | 65697+340n |
| — | Po19 | 65698+340n |
| — | Po20 | 65699+340n |
| — | Po21 | 65700+340n |
| — | Po22 | 65701+340n |
| — | Po23 | 65702+340n |
| — | Po24 | 65703+340n |
| — | Po25 | 65704+340n |
| — | Po26 | 65705+340n |
| — | Po27 | 65706+340n |
| — | Po28 | 65707+340n |
| — | Po29 | 65708+340n |
| — | Po30 | 65709+340n |
| — | Po31 | 65710+340n |
| — | Po32 | 65711+340n |
| — | PL01 | 65744+340n |
| — | PL02 | 65745+340n |
| — | PL03 | 65746+340n |
| — | PL04 | 65747+340n |
| — | PL05 | 65748+340n |
| — | PL06 | 65749+340n |
| — | PL07 | 65750+340n |
| — | PL08 | 65751+340n |
| — | PL09 | 65752+340n |
| — | PL10 | 65753+340n |
| — | PL11 | 65754+340n |
| — | PL12 | 65755+340n |
| — | PL13 | 65756+340n |
| — | PL14 | 65757+340n |
| — | PL15 | 65758+340n |
| — | PL16 | 65759+340n |
| — | PL17 | 65760+340n |
| — | PL18 | 65761+340n |
| — | PL19 | 65762+340n |
| — | PL20 | 65763+340n |
| — | PL21 | 65764+340n |
| — | PL22 | 65765+340n |
| — | PL23 | 65766+340n |
| — | PL24 | 65767+340n |
| — | PL25 | 65768+340n |
| — | PL26 | 65769+340n |
| — | PL27 | 65770+340n |
| — | PL28 | 65771+340n |
| — | PL29 | 65772+340n |
| — | PL30 | 65773+340n |
| — | PL31 | 65774+340n |
| — | PL32 | 65775+340n |
| — | PL33 | 65776+340n |
| — | PL34 | 65777+340n |
| — | PL35 | 65778+340n |
| — | PL36 | 65779+340n |
| — | PL37 | 65780+340n |
| — | PL38 | 65781+340n |
| — | PL39 | 65782+340n |
| — | PL40 | 65783+340n |
| — | PL41 | 65784+340n |
| — | PL42 | 65785+340n |
| — | PL43 | 65786+340n |
| — | PL44 | 65787+340n |
| — | PL45 | 65788+340n |
| — | PL46 | 65789+340n |
| — | PL47 | 65790+340n |
| — | PL48 | 65791+340n |

*The table continues over p.435-443 (header repeated on each page). Rows per page: p.435: PA01 to PB10 (43 rows, including [Pr.100]); p.436: PB11 to PB63 (53 rows); p.437: PB64 to PC52 (53 rows); p.438: PC53 to PD41 (53 rows); p.439: PD42 to PE46 (53 rows); p.440: PE47 to PF03 (53 rows); p.441: PF04 to Po08 (53 rows); p.442: Po09 to PL29 (53 rows); p.443: PL30 to PL48 (19 rows). Total 433 rows ([Pr.100] + 432 servo amplifier parameters). "—" is as printed in the original. "Po01" to "Po32" are printed with a lowercase "o" in the original.

#### Mark detection function (マーク検出機能) (11.2 / original p.444)

The following shows the relation between the buffer memory addresses for mark detection function and the various items.

##### Mark detection setting parameters (マーク検出設定パラメータ) (11.2 / original p.444)

k: Mark detection setting No. - 1

| Item | | Fetch cycle | Buffer memory address |
|---|---|---|---|
| [Pr.800] | Mark detection signal setting | At power supply ON | 54000+20k |
| [Pr.801] | Mark detection signal compensation time | At power supply ON/"[Cd.190] PLC READY" OFF to ON | 54001+20k |
| [Pr.802] | Mark detection data type | At power supply ON | 54002+20k |
| [Pr.803] | Mark detection data axis No. | At power supply ON | 54003+20k |
| [Pr.804] | Mark detection data buffer memory No. | At power supply ON | 54004+20k<br>54005+20k |
| [Pr.805] | Latch data range upper limit value | At power supply ON/"[Cd.190] PLC READY" OFF to ON/at request (Latch data range change) | 54006+20k<br>54007+20k |
| [Pr.806] | Latch data range lower limit value | At power supply ON/"[Cd.190] PLC READY" OFF to ON/at request (Latch data range change) | 54008+20k<br>54009+20k |
| [Pr.807] | Mark detection mode setting | At power supply ON/"[Cd.190] PLC READY" OFF to ON | 54010+20k |
| [Pr.808] | Mark detection signal link device type [FX5-SSC-G] | At power supply ON | 54011+20k |
| [Pr.809] | Mark detection signal link device No. [FX5-SSC-G] | At power supply ON | 54012+20k |
| [Pr.810] | Mark detection signal link device bit specification [FX5-SSC-G] | At power supply ON | 54013+20k |
| [Pr.811] | Mark detection signal detection direction setting [FX5-SSC-G] | At power supply ON | 54014+20k |

*In the original, the "Fetch cycle" cell is merged over [Pr.802] to [Pr.804], and over [Pr.805] to [Pr.806]. Expanded to each row.

##### Mark detection control data (マーク検出制御データ) (11.2 / original p.444)

k: Mark detection setting No. - 1

| Item | | Fetch cycle | Buffer memory address |
|---|---|---|---|
| [Cd.800] | Number of mark detection clear request | Operation cycle | 54640+10k |
| [Cd.801] | Mark detection invalid flag | Operation cycle | 54641+10k |
| [Cd.802] | Latch data range change request | Operation cycle/At conditions established (DI input) | 54642+10k |

*In the original, the "Fetch cycle" cell is merged over [Cd.800] to [Cd.801]. Expanded to each row.

##### Mark detection monitor data (マーク検出モニタデータ) (11.2 / original p.444)

k: Mark detection setting No. - 1

| Item | | Refresh cycle | Buffer memory address |
|---|---|---|---|
| [Md.800] | Number of mark detection | At conditions established (Mark detection) | 54960+80k |
| [Md.801] | Mark detection data storage area (1 to 32): 1 | At conditions established (Mark detection) | 54962+80k<br>54963+80k |
| [Md.801] | Mark detection data storage area (1 to 32): 2 | At conditions established (Mark detection) | 54964+80k<br>54965+80k |
| [Md.801] | Mark detection data storage area (1 to 32): 3 | At conditions established (Mark detection) | 54966+80k<br>54967+80k |
| [Md.801] | Mark detection data storage area (1 to 32): ⋮ | At conditions established (Mark detection) | ⋮ |
| [Md.801] | Mark detection data storage area (1 to 32): 32 | At conditions established (Mark detection) | 55024+80k<br>55025+80k |

*In the original, [Md.801] "Mark detection data storage area (1 to 32)" is merged over 5 rows with a sub-item column (1 / 2 / 3 / ⋮ / 32); written here as "item: sub-item". The "Refresh cycle" cell is merged over [Md.800] to [Md.801] (all rows). Expanded to each row. "⋮" is as printed in the original (storage areas 4 to 31 are omitted in the original itself).

#### Link device external signal assignment [FX5-SSC-G] (リンクデバイス外部信号割付け[FX5-SSC-G]) (11.2 / original p.445)

The following shows the relation between the buffer memory addresses for link device external signal assignment and the various items.

##### Link device external signal assignment parameters (リンクデバイス外部信号割付けパラメータ) (11.2 / original p.445)

n: Axis No. - 1

| Item | | Fetch cycle | Buffer memory address |
|---|---|---|---|
| [Pr.910] | Upper limit signal (FLS): Link device type | At power supply ON/the CPU module reset | 36000+20n |
| [Pr.911] | Upper limit signal (FLS): Link device start No. | At power supply ON/the CPU module reset | 36001+20n |
| [Pr.912] | Upper limit signal (FLS): Link device bit specification | At power supply ON/the CPU module reset | 36002+20n |
| [Pr.913] | Upper limit signal (FLS): Link device logic setting | At power supply ON/the CPU module reset | 36003+20n |
| [Pr.920] | Lower limit signal (RLS): Link device type | At power supply ON/the CPU module reset | 36005+20n |
| [Pr.921] | Lower limit signal (RLS): Link device start No. | At power supply ON/the CPU module reset | 36006+20n |
| [Pr.922] | Lower limit signal (RLS): Link device bit specification | At power supply ON/the CPU module reset | 36007+20n |
| [Pr.923] | Lower limit signal (RLS): Link device logic setting | At power supply ON/the CPU module reset | 36008+20n |
| [Pr.930] | Proximity dog signal (DOG): Link device type | At power supply ON/the CPU module reset | 36010+20n |
| [Pr.931] | Proximity dog signal (DOG): Link device start No. | At power supply ON/the CPU module reset | 36011+20n |
| [Pr.932] | Proximity dog signal (DOG): Link device bit specification | At power supply ON/the CPU module reset | 36012+20n |
| [Pr.933] | Proximity dog signal (DOG): Link device logic setting | At power supply ON/the CPU module reset | 36013+20n |
| [Pr.940] | Stop signal (STOP): Link device type | At power supply ON/the CPU module reset | 36015+20n |
| [Pr.941] | Stop signal (STOP): Link device start No. | At power supply ON/the CPU module reset | 36016+20n |
| [Pr.942] | Stop signal (STOP): Link device bit specification | At power supply ON/the CPU module reset | 36017+20n |
| [Pr.943] | Stop signal (STOP): Link device logic setting | At power supply ON/the CPU module reset | 36018+20n |

*In the original, the "Fetch cycle" cell is merged over [Pr.910] to [Pr.943]. Expanded to each row.

## 11.3 Basic Setting (基本設定) (11.3 / original p.446-484)

The setting items of the setting data are explained in this section.

### Servo network configuration parameters [FX5-SSC-G] (サーボネットワーク構成パラメータ[FX5-SSC-G]) (11.3 / original p.446-447)

n: Axis No. -1

| Item | Setting value, setting range | Default value | Buffer memory address |
|---|---|---|---|
| [Pr.101] Virtual servo amplifier setting | 0: Use for the actual servo amplifier<br>1: Use for the virtual servo amplifier | 0 | 58022+32n |
| [Pr.140] Driver command discard detection setting | 0: Detection invalid<br>1: Detection valid | 0 | 58023+32n |
| [Pr.141] IP address | Set the IP address.<br>Assign 1 [byte] each to octets 1 to 4. | 0 | 58024+32n<br>58025+32n |
| [Pr.142] Multidrop number | 0 to 65535 | 0 | 58028+32n |

#### [Pr.101] Virtual servo amplifier setting ([Pr.101]仮想サーボアンプ設定) (11.3 / original p.446)

Set whether or not to use the axis as a virtual servo amplifier axis.
0: Use for the actual servo amplifier
1: Use for the virtual servo amplifier

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.446)

For the buffer memory addresses in this area, refer to the following.
→Page 422 Servo network configuration parameters [FX5-SSC-G]

#### [Pr.140] Driver command discard detection setting ([Pr.140]ドライバ指令破棄検出設定) (11.3 / original p.446)

By setting the driver command discard detection setting, when bit 12 in "[Md.117] Statusword" of the drive unit turns ON → OFF while operating an actual axis, the error "Driver command discard detection" (error code: 1BE6H) can be outputted before the motor stops to stop the command.
0: Detection invalid
1: Detection valid
The contents of bit 12 in "[Md.117] Statusword" changes depending on the control mode of the connected drive unit. Refer to the specifications for the drive unit being connected for the change conditions of "[Md.117] Statusword", etc.

| Driver control mode | Abbreviation for bit 12 of "[Md.117] Statusword" | Details |
|---|---|---|
| Cyclic synchronous position mode (csp) | Target position ignored | 0: Discarding Target position [Obj. 607Ah] |
| Cyclic synchronous velocity mode (csv) | Target velocity ignored | 0: Discarding Target velocity [Obj. 60FFh] |
| Cyclic synchronous torque mode (cst) | Target torque ignored | 0: Discarding Target torque [Obj. 6071h] |
| Continuous operation to torque control mode (ct) | Target torque ignored | 0: Discarding Target torque [Obj. 6071h] |
| Other than the above | — | Not checked |

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.446)

For the buffer memory addresses in this area, refer to the following.
→Page 422 Servo network configuration parameters [FX5-SSC-G]

#### [Pr.141] IP address ([Pr.141]IPアドレス) (11.3 / original p.447)

Set the IP address.
Assign 1 [byte] each to octets 1 to 4.

[Figure] Bit assignment of the IP address (original p.447)
- 32 bits (b31 to b0) divided into 8-bit groups; from the b31 side: "1st octet", "2nd octet", "3rd octet", "4th octet" (b0 side)
- Bit labels shown: b31, b16 b15, b0

Ex.
For 192.168.3.1
Setting value: HC0A80301

> **Point**
> - When using the amplifier as an actual servo amplifier, be sure to set an IP address. Axis control cannot be performed when set to the default value of "0".
> - For this parameter, the value set in the flash ROM of the Motion module becomes valid when the power is turned ON or the CPU module is reset. Inputting is not performed by turning "[Cd.190] PLC READY", so perform writing to the flash ROM after setting the value to the buffer memory when changing this parameter. (The value must be fixed when turning ON the power or resetting the CPU module.)
>
> *(Note: "by turning "[Cd.190] PLC READY"" without "OFF → ON" is as printed in the original.)*

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.447)

For the buffer memory addresses in this area, refer to the following.
→Page 422 Servo network configuration parameters [FX5-SSC-G]

#### [Pr.142] Multidrop number ([Pr.142]マルチドロップ番号) (11.3 / original p.447)

When one station includes multiple logic axes, such as for a multi-axis drive unit, specify the No. in order to distinguish logic axes. Specify 0 when using a single axis servo amplifier.

> **Point**
> For this parameter, the value set in the flash ROM of the Motion module becomes valid when the power is turned ON or the CPU module is reset. Inputting is not performed by turning "[Cd.190] PLC READY", so perform writing to the flash ROM after setting the value to the buffer memory when changing this parameter. (The value must be fixed when turning ON the power or resetting the CPU module.)

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.447)

For the buffer memory addresses in this area, refer to the following.
→Page 422 Servo network configuration parameters [FX5-SSC-G]

### Common parameters (共通パラメータ) (11.3 / original p.448-455)

| Item | Setting value, setting range: Value set with the engineering tool | Setting value, setting range: Value set with a program | Default value | Buffer memory address |
|---|---|---|---|---|
| [Pr.24] Manual pulse generator/Incremental synchronous encoder input selection [FX5-SSC-S] | 0: A-phase/B-phase multiplied by 4 | 0 | 0 | 33 |
| [Pr.24] Manual pulse generator/Incremental synchronous encoder input selection [FX5-SSC-S] | 1: A-phase/B-phase multiplied by 2 | 1 | 0 | 33 |
| [Pr.24] Manual pulse generator/Incremental synchronous encoder input selection [FX5-SSC-S] | 2: A-phase/B-phase multiplied by 1 | 2 | 0 | 33 |
| [Pr.24] Manual pulse generator/Incremental synchronous encoder input selection [FX5-SSC-S] | 3: pulse/SIGN | 3 | 0 | 33 |
| [Pr.82] Forced stop valid/invalid selection | 0: Valid (External input signal) [FX5-SSC-S] | 0 | 0 [FX5-SSC-S]<br>1 [FX5-SSC-G] | 35 |
| [Pr.82] Forced stop valid/invalid selection | 1: Invalid | 1 | 0 [FX5-SSC-S]<br>1 [FX5-SSC-G] | 35 |
| [Pr.82] Forced stop valid/invalid selection | 2: Valid (buffer memory) [FX5-SSC-G] | 2 | 0 [FX5-SSC-S]<br>1 [FX5-SSC-G] | 35 |
| [Pr.82] Forced stop valid/invalid selection | 3: Valid (Link device) [FX5-SSC-G] | 3 | 0 [FX5-SSC-S]<br>1 [FX5-SSC-G] | 35 |
| [Pr.89] Manual pulse generator/Incremental synchronous encoder input type selection [FX5-SSC-S] | 0: Differential output type | 0 | 1 | 67 |
| [Pr.89] Manual pulse generator/Incremental synchronous encoder input type selection [FX5-SSC-S] | 1: Voltage output/open collector type | 1 | 1 | 67 |
| [Pr.96] Operation cycle setting [FX5-SSC-S] | 0000H: 0.888 ms | 0000H | 1 | 105 |
| [Pr.96] Operation cycle setting [FX5-SSC-S] | 0001H: 1.777 ms | 0001H | 1 | 105 |
| [Pr.97] SSCNET setting [FX5-SSC-S] | 0: SSCNETⅢ | 0 | 1 | 106 |
| [Pr.97] SSCNET setting [FX5-SSC-S] | 1: SSCNETⅢ/H | 1 | 1 | 106 |
| [Pr.150] Input terminal logic selection [FX5-SSC-S] | b0: DI1 to b3: DI4 — 0: ON at leading edge | 0 | 0 | 58000, 58001 |
| [Pr.150] Input terminal logic selection [FX5-SSC-S] | b0: DI1 to b3: DI4 — 1: ON at trailing edge | 1 | 0 | 58000, 58001 |
| [Pr.151] Manual pulse generator/Incremental synchronous encoder input logic selection [FX5-SSC-S] | 0: Negative logic | 0 | 0 | 58002 |
| [Pr.151] Manual pulse generator/Incremental synchronous encoder input logic selection [FX5-SSC-S] | 1: Positive logic | 1 | 0 | 58002 |
| [Pr.152] Maximum number of control axes [FX5-SSC-G] | 0: No setting | 0 | 0 | 58003 |
| [Pr.152] Maximum number of control axes [FX5-SSC-G] | 1 to maximum No. of control axes | 1 to maximum No. of control axes | 0 | 58003 |
| [Pr.156] Manual pulse generator smoothing time constant [FX5-SSC-G] | 0 to 5000 (ms) | 0 to 5000 | 0 | 58011 |
| [Pr.900] Forced stop signal (EMI): Link device type [FX5-SSC-G] | Others: Invalid | — | 0 | 58014 |
| [Pr.900] Forced stop signal (EMI): Link device type [FX5-SSC-G] | 11H: RX | 11H | 0 | 58014 |
| [Pr.900] Forced stop signal (EMI): Link device type [FX5-SSC-G] | 12H: RY | 12H | 0 | 58014 |
| [Pr.900] Forced stop signal (EMI): Link device type [FX5-SSC-G] | 13H: RWr | 13H | 0 | 58014 |
| [Pr.900] Forced stop signal (EMI): Link device type [FX5-SSC-G] | 14H: RWw | 14H | 0 | 58014 |
| [Pr.901] Forced stop signal (EMI): Link device start No. | RX/RY: 0 to 1FFFH | 0 to 1FFFH | 0 | 58015 |
| [Pr.901] Forced stop signal (EMI): Link device start No. | RWr/RWw: 0 to 3FFH | 0 to 3FFH | 0 | 58015 |
| [Pr.902] Forced stop signal (EMI): Link device bit specification | 00H to 1FH | 00H to 1FH | 0 | 58016 |
| [Pr.903] Forced stop signal (EMI): Link device logic setting | 0: Negative logic | 0 | 0 | 58017 |
| [Pr.903] Forced stop signal (EMI): Link device logic setting | 1: Positive logic | 1 | 0 | 58017 |

*In the original, "Setting value, setting range" is a 2-level header ("Value set with the engineering tool" / "Value set with a program"). The Item, Default value and Buffer memory address cells are merged over the setting-value rows of each parameter. For [Pr.150], the bit column ("b0: DI1" / "to" / "b3: DI4") is shown as 3 stacked cells, and the setting-value cell "0: ON at leading edge / 1: ON at trailing edge" and the program-value cell "0 / 1" are each one cell spanning those bit rows (the same setting applies to each bit). Expanded to each row. "[FX5-SSC-G]" is not printed after [Pr.901] to [Pr.903] in this table (as printed).

#### [Pr.24] Manual pulse generator/Incremental synchronous encoder input selection [FX5-SSC-S] ([Pr.24]手動パルサ／INC同期エンコーダ入力選択[FX5-SSC-S]) (11.3 / original p.449-450)

Set the manual pulse generator/incremental synchronous encoder input pulse mode.

| Manual pulse generator/Incremental synchronous encoder input selection | Setting value |
|---|---|
| A-phase/B-phase multiplied by 4 | 0 |
| A-phase/B-phase multiplied by 2 | 1 |
| A-phase/B-phase multiplied by 1 | 2 |
| pulse/SIGN | 3 |

Set the positive logic or negative logic in "[Pr.151] Manual pulse generator/Incremental synchronous encoder input logic selection".

##### ■A-phase/B-phase mode (A相／B相モード) (11.3 / original p.449)

When the A-phase is 90° ahead of the B-phase, the motor will forward run.
When the B-phase is 90° ahead of the A-phase, the motor will reverse run.

- A-phase/B-phase multiplied by 4
  The positioning address increases or decreases at rising or falling edges of A-phase/B-phase.

[Figure] A-phase/B-phase multiplied by 4 — [Pr.151] Manual pulse generator/Incremental synchronous encoder input logic selection: Positive logic / Negative logic (original p.449)
- Signals: A-phase (Aφ), B-phase (Bφ), Positioning address; each logic shows "Forward run" and "Reverse run"
- Forward run: the positioning address changes by +1 at every rising and falling edge of A-phase and B-phase ("+1+1+1+1+1+1+1+1", 8 counts for 2 cycles)
- Reverse run: -1 at every edge ("-1 -1 -1 -1 -1 -1 -1 -1", 8 counts)
- Negative logic: waveforms are the inverse of positive logic (A-phase/B-phase normally HIGH); counts are the same (+1 ×8 forward, -1 ×8 reverse)

- A-phase/B-phase multiplied by 2
  The positioning address increases or decreases at twice rising or twice falling edges of A-phase/B-phase.

[Figure] A-phase/B-phase multiplied by 2 — Positive logic / Negative logic (original p.449)
- Signals: A-phase (Aφ), B-phase (Bφ), Positioning address
- Forward run: positioning address "+1 +1 +1 +1" (4 counts for 2 cycles)
- Reverse run: "-1 -1 -1 -1" (4 counts)
- Negative logic: waveforms inverted; counts the same

- A-phase/B-phase multiplied by 1
  The positioning address increases or decreases at twice rising or twice falling edges of A-phase/B-phase.

*(Note: the sentence for "multiplied by 1" is printed identically to the one for "multiplied by 2" in the original.)*

[Figure] A-phase/B-phase multiplied by 1 — Positive logic / Negative logic (original p.449)
- Signals: A-phase (Aφ), B-phase (Bφ), Positioning address
- Forward run: positioning address "+1 +1" (2 counts for 2 cycles, i.e. one count per cycle)
- Reverse run: "-1 -1" (2 counts)
- Negative logic: waveforms inverted; counts the same

##### ■pulse/SIGN (pulse/SIGN) (11.3 / original p.450)

| [Pr.151] Manual pulse generator/Incremental synchronous encoder input logic selection: Positive logic | [Pr.151] Manual pulse generator/Incremental synchronous encoder input logic selection: Negative logic |
|---|---|
| Forward run and reverse run are controlled with the ON/OFF of the direction sign (SIGN).<br>The motor will forward run when the direction sign is HIGH.<br>The motor will reverse run when the direction sign is LOW. | Forward run and reverse run are controlled with the ON/OFF of the direction sign (SIGN).<br>The motor will forward run when the direction sign is LOW.<br>The motor will reverse run when the direction sign is HIGH. |

[Figure] pulse/SIGN timing (original p.450)
- Positive logic: pulse is counted at rising edges. While SIGN is HIGH: "Forward run" (Move in + direction); while SIGN is LOW: "Reverse run" (Move in - direction)
- Negative logic: pulse is counted at falling edges. While SIGN is LOW: "Forward run" (Move in + direction); while SIGN is HIGH: "Reverse run" (Move in - direction)

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.450)

Refer to the following for the buffer memory address in this area.
→Page 422 Common parameters

#### [Pr.82] Forced stop valid/invalid selection ([Pr.82]緊急停止有効／無効設定) (11.3 / original p.450)

Set the forced stop valid/invalid.
All axes of the servo amplifier are made to batch forced stop after this is set to "0: Valid (External input signal)" or "2: Valid (Buffer memory)".
The error "Servo READY signal OFF during operation" (error code: 1902H [FX5-SSC-S], or error code 1A02H [FX5-SSC-G]) does not occur if the forced input signal is turned on during operation.

| Forced stop valid/invalid selection | Setting value |
|---|---|
| Valid (External input signal) (Forced stop is used.) [FX5-SSC-S] | 0 |
| Invalid (Forced stop is not used.) | 1 |
| Valid (Buffer memory) (Uses the forced stop from the buffer memory) [FX5-SSC-G] | 2 |
| Valid (Link device) (Uses the forced stop from the link device) [FX5-SSC-G] | 3 |

> **Point**
> - If the setting is other than 0 to 3, the error "Forced stop valid/invalid setting error" (error code: 1B71H [FX5-SSC-S], or error code 1DC1H [FX5-SSC-G]) occurs.
> - The "[Md.50] Forced stop input" is stored "1" by setting "Forced stop valid/invalid selection" to invalid.
>
> [FX5-SSC-G]
> - If "3: Valid (Link device)" is selected, specify the link device to be used for the forced stop signal by using the following parameters.
>   - [Pr.900] Forced stop signal (EMI): Link device type
>   - [Pr.901] Forced stop signal (EMI): Link device start No.
>   - [Pr.902] Forced stop signal (EMI): Link device bit specification
>   - [Pr.903] Forced stop signal (EMI): Link device logic setting

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.450)

Refer to the following for the buffer memory address in this area.
→Page 422 Common parameters

#### [Pr.89] Manual pulse generator/Incremental synchronous encoder input type selection [FX5-SSC-S] ([Pr.89]手動パルサ／INC同期エンコーダ入力タイプ選択[FX5-SSC-S]) (11.3 / original p.451)

Set the input type from the manual pulse generator/incremental synchronous encoder.

| Manual pulse generator/Incremental synchronous encoder input type selection | Setting value |
|---|---|
| Differential output type | 0 |
| Voltage output/open collector type | 1 |

Refer to "External Input Connection Connector [FX5-SSC-S]" in the following manual for details.
[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Startup)

> **Point**
> The "Manual pulse generator/Incremental synchronous encoder input type selection" is included in common parameters. However, it will be valid at the leading edge (OFF to ON) of the "[Cd.190] PLC READY".

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.451)

Refer to the following for the buffer memory address in this area.
→Page 422 Common parameters

#### [Pr.96] Operation cycle setting [FX5-SSC-S] ([Pr.96]演算周期設定[FX5-SSC-S]) (11.3 / original p.451)

Set the operation cycle.

| Operation cycle setting | Setting value |
|---|---|
| 0.888 ms | 0000H |
| 1.777 ms | 0001H |

> **Point**
> - In this parameter, the value set in flash ROM of Simple Motion module is valid at power supply ON or CPU module reset. Fetch by "[Cd.190] PLC READY" OFF to ON is not executed. Execute flash ROM writing to change after setting a value to buffer memory. Confirm the current operation cycle in "[Md.132] Operation cycle setting".
> - Confirm that "[Md.133] Operation cycle over flag" does not turn ON. If the flag is ON, the operation cycle over has been generated. Correct the positioning content or increase the operation cycle.

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.451)

Refer to the following for the buffer memory address in this area.
→Page 422 Common parameters

#### [Pr.97] SSCNET setting [FX5-SSC-S] ([Pr.97]SSCNET設定[FX5-SSC-S]) (11.3 / original p.452)

Set the servo network.

| SSCNET setting | Setting value |
|---|---|
| SSCNETⅢ | 0 |
| SSCNETⅢ/H | 1 |

The connectable servo amplifier differs by this parameter. When an unconnectable servo amplifier is set in "[Pr.100] Servo series", the error "SSCNET setting error" (error code: 1B74H) occurs and the communication with the servo amplifier is not executed.

> **Point**
> In this parameter, the value set in flash ROM of Simple Motion module is valid at power supply ON or CPU module reset. Fetch by "[Cd.190] PLC READY" OFF to ON is not executed. Execute flash ROM writing to change after setting a value to buffer memory.

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.452)

Refer to the following for the buffer memory address in this area.
→Page 422 Common parameters

#### [Pr.150] Input terminal logic selection [FX5-SSC-S] ([Pr.150]入力端子論理選択[FX5-SSC-S]) (11.3 / original p.452)

Set the external input signal logic (external command/switching signal) from the external device of the Simple Motion module.

| Input terminal logic selection | Setting value |
|---|---|
| ON at leading edge (When the current is flowed through the input signal terminal: ON, When the current is not flowed through the input signal terminal: OFF) | 0 |
| ON at trailing edge (When the current is flowed through the input signal terminal: OFF, When the current is not flowed through the input signal terminal: ON) | 1 |

| Bit | Input terminal |
|---|---|
| b0 | DI1 |
| b1 | DI2 |
| b2 | DI3 |
| b3 | DI4 |

> **Point**
> A mismatch in the setting may disable normal operation. Be careful when changing the default value.

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.452)

Refer to the following for the buffer memory address in this area.
→Page 422 Common parameters

#### [Pr.151] Manual pulse generator/INC synchronous encoder input logic selection [FX5-SSC-S] ([Pr.151]手動パルサ／INC同期エンコーダ入力論理選択[FX5-SSC-S]) (11.3 / original p.453)

Set the input signal logic from the manual pulse generator/incremental synchronous encoder.

| Manual pulse generator/Incremental synchronous encoder input logic selection | Setting value |
|---|---|
| Negative logic | 0 |
| Positive logic | 1 |

Refer to the following for the negative logic/positive logic.
→Page 447 [Pr.24] Manual pulse generator/Incremental synchronous encoder input selection [FX5-SSC-S]

> **Point**
> A mismatch in the signal logic will disable normal operation. Be careful of this when you change from the default value.

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.453)

Refer to the following for the buffer memory address in this area.
→Page 422 Common parameters

#### [Pr.152] Maximum number of control axes [FX5-SSC-G] ([Pr.152]制御軸数上限[FX5-SSC-G]) (11.3 / original p.453)

Set the upper limit for the number of control axes.
This is used to reduce the operation cycle when the actual number of axes used is lower than the maximum number of control axes of the relevant model.

| Maximum number of control axes | Setting value |
|---|---|
| No setting (Control is performed using the maximum number of control axes for the relevant model.) | 0 |
| Maximum number of control axes (Axes up to the set axis No. are used as the target for control.)*1 | 1 to maximum No. of control axes*2 |

*1 Example) When "4" is set, the control axes are Axis 1 to 4. Control cannot be performed for Axis 5 and later.
*2 The maximum No. of control axes for each model is shown below.
FX5-40SSC-G: 4
FX5-80SSC-G: 8

- When the maximum number of control axes exceeds the maximum No. of control axes for the Motion module (for example, "5" is set for a model with a maximum of 4 axes), the warning "Outside Maximum number of control axes" (warning code: 0D3AH) occurs, and control is performed as though the set value is "0: No setting". (The warning occurs on Axis 1.)
- When subsequent axes are set to a value other than "0: No setting" in "[Pr.141] IP address" or a value other than "0: Use for the actual servo amplifier" in "[Pr.101] Virtual servo amplifier setting" via the setting of the maximum number of control axes the warning "Outside control axis setting" (warning code: 0D3BH) occurs on the axes and the servo amplifier does not start the RUN time. (The LED display of the servo amplifier continues displaying "b_".)

> **Point**
> - For this parameter, the value set in the flash ROM of the Motion module becomes valid when the power is turned ON or the CPU module is reset. Inputting is not performed by turning "[Cd.190] PLC READY" OFF→ON, so perform writing to the flash ROM after setting the value to the buffer memory when changing this parameter. (The value must be fixed when turning ON the power or resetting the CPU module.)
> - Subsequent axes set as a servo input axis (synchronous control) or a virtual servo amplifier via the setting of the maximum number of control axes are also not eligible to be targets of control.

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.453)

For the buffer memory addresses in this area, refer to the following.
→Page 422 Common parameters

#### [Pr.156] Manual pulse generator smoothing time constant [FX5-SSC-G] ([Pr.156]手動パルサスムージング時定数[FX5-SSC-G]) (11.3 / original p.454)

- Smoothing processing smooths the speed change in manual pulse generator operation. Note that the input response is delayed by the time set for the smoothing processing.
- When a value outside the range is set, the error "Outside manual pulse generator smoothing time constant range error" (error code: 1DC6H) occurs when "[Cd.190] PLC READY" turns ON, preventing the READY signal ([Md.140] Module status: b0) from turning ON.
- The input cycle of "[Cd.55] Input value for manual pulse generator via CPU" has an interval of 8.0 ms, so the smoothing time constant is truncated in multiples of 8. (Example: a setting value of 8 to 15 ms is operated at a time constant of 8 ms.
- The smoothing time constant is not reflected at a stop cause occurrence or at a deceleration stop via the "0" setting of "[Cd.21] Manual pulse generator enable flag".

*(Note: the closing parenthesis of "(Example: ... 8 ms." is missing in the original.)*

##### ■Basic concept of speed change (速度変動の考え方) (11.3 / original p.454)

Speed change occurs because of a discrepancy between the scan time of the CPU module and the input cycle in "[Cd.55] Input value for manual pulse generator via CPU". As shown in the diagram below, the speed change can be suppressed by setting "[Pr.156] Manual pulse generator smoothing time constant" to a value larger than the maximum scan time.

- When speed change occurs
  As shown in the diagram below, speed change occurs when the scan time is larger than the input cycle of "[Cd.55] Input value for manual pulse generator via CPU".

[Figure] When speed change occurs (original p.454)
- Axes: Velocity (vertical) / Time (horizontal). Legend: solid line = [Cd.55] Input value for manual pulse generator via CPU; dashed line = [Md.20] Command position value
- [Cd.55] rises in equal steps once per scan (6 steps); [Md.20] follows each step immediately (slightly delayed dashed step)
- [Md.22] Speed command: a short triangular spike at each step and 0 between steps (speed change / pulsating speed)

- When speed change is suppressed
  Example: When "[Pr.156] Manual pulse generator smoothing time constant" is set to a value equal to double the scan time

[Figure] When speed change is suppressed (original p.454)
- Same legend: solid = [Cd.55] Input value for manual pulse generator via CPU; dashed = [Md.20] Command position value
- [Cd.55] rises in the same 6 steps; [Md.20] rises as a smooth continuous curve, reaching the final value after the last step
- [Md.22] Speed command: rises in 2 steps to a constant level, stays flat while input continues, then decreases in 2 steps to 0 after the input stops (no pulsation)

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.454)

For the buffer memory addresses in this area, refer to the following.
→Page 422 Common parameters

#### [Pr.900] Forced stop signal (EMI): Link device type [FX5-SSC-G] ([Pr.900]緊急停止信号(EMI): リンクデバイス種別[FX5-SSC-G]) (11.3 / original p.455)

Set the link device type for use. For details, refer to the following.
→Page 329 Link Device External Signal Assignment Function [FX5-SSC-G]

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.455)

Refer to the following for the buffer memory address in this area.
→Page 422 Common parameters

#### [Pr.901] Forced stop signal (EMI): Link device start No. [FX5-SSC-G] ([Pr.901]緊急停止信号(EMI): リンクデバイス先頭番号[FX5-SSC-G]) (11.3 / original p.455)

Set the link device No. for use. For details, refer to the following.
→Page 329 Link Device External Signal Assignment Function [FX5-SSC-G]

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.455)

Refer to the following for the buffer memory address in this area.
→Page 422 Common parameters

#### [Pr.902] Forced stop signal (EMI): Link device bit specification [FX5-SSC-G] ([Pr.902]緊急停止信号(EMI): リンクデバイスビット指定[FX5-SSC-G]) (11.3 / original p.455)

Set the bit No. that is used when "13H: RWr" and "14H: RWw" are set to "[Pr.900] Forced stop signal (EMI): Link device type". For details, refer to the following.
→Page 329 Link Device External Signal Assignment Function [FX5-SSC-G]

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.455)

Refer to the following for the buffer memory address in this area.
→Page 422 Common parameters

#### [Pr.903] Forced stop signal (EMI): Link device logic setting [FX5-SSC-G] ([Pr.903]緊急停止信号(EMI): リンクデバイス論理設定[FX5-SSC-G]) (11.3 / original p.455)

Set the logic for assignment signal. For details, refer to the following.
→Page 329 Link Device External Signal Assignment Function [FX5-SSC-G]

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.455)

Refer to the following for the buffer memory address in this area.
→Page 422 Common parameters

### Basic parameters1 (基本パラメータ1) (11.3 / original p.456-460)

This section describes the details on the basic parameter 1.
n: Axis No. - 1

| Item | | Setting value, setting range: Value set with the engineering tool | Setting value, setting range: Value set with a program | Default value | Buffer memory address |
|---|---|---|---|---|---|
| [Pr.1] Unit setting | — | 0: mm | 0 | 3 | 0+150n |
| [Pr.1] Unit setting | — | 1: inch | 1 | 3 | 0+150n |
| [Pr.1] Unit setting | — | 2: degree | 2 | 3 | 0+150n |
| [Pr.1] Unit setting | — | 3: pulse | 3 | 3 | 0+150n |
| Movement amount per pulse | [Pr.2] Number of pulses per rotation (AP) (Unit: pulse) | 1 to 200000000 | 1 to 200000000 | 20000 | 2+150n<br>3+150n |
| Movement amount per pulse | [Pr.3] Movement amount per rotation (AL) | The setting value range differs according to the "[Pr.1] Unit setting". | The setting value range differs according to the "[Pr.1] Unit setting". | 20000 | 4+150n<br>5+150n |
| Movement amount per pulse | [Pr.4] Unit magnification (AM) | 1: 1 times | 1 | 1 | 1+150n |
| Movement amount per pulse | [Pr.4] Unit magnification (AM) | 10: 10 times | 10 | 1 | 1+150n |
| Movement amount per pulse | [Pr.4] Unit magnification (AM) | 100: 100 times | 100 | 1 | 1+150n |
| Movement amount per pulse | [Pr.4] Unit magnification (AM) | 1000: 1000 times | 1000 | 1 | 1+150n |
| [Pr.7] Bias speed at start | — | The setting value range differs according to the "[Pr.1] Unit setting". | The setting value range differs according to the "[Pr.1] Unit setting". | 0 | 6+150n<br>7+150n |

*In the original, "Setting value, setting range" is a 2-level header ("Value set with the engineering tool" / "Value set with a program"). "[Pr.1] Unit setting" and "[Pr.7] Bias speed at start" span both Item columns (shown here with "—" in the second Item column). "Movement amount per pulse" is merged over [Pr.2] to [Pr.4]. The Item, Default value and Buffer memory address cells of [Pr.1] and [Pr.4] are merged over their setting-value rows. For [Pr.3] and [Pr.7], the text "The setting value range differs according to the "[Pr.1] Unit setting"." is one cell spanning both setting-value columns. Expanded to each row/column.

#### [Pr.1] Unit setting ([Pr.1]単位設定) (11.3 / original p.456)

Set the unit used for defining positioning operations. Choose from the following units depending on the type of the control target: mm, inch, degree, or pulse. Different units can be defined for different axes.

Ex.
Different units (mm, inch, degree, and pulse) are applicable to different systems:
- mm or inch: X-Y table, conveyor (Select mm or inch depending on the machine specifications.)
- degree: Rotating body (360 degrees/rotation)
- pulse: X-Y table, conveyor

> **Point**
> - When you change the unit, note that the values of other parameters and data will not be changed automatically. After changing the unit, check if the parameter and data values are within the allowable range.
> - Set "2: degree" to exercise speed-position switching control (ABS mode).
> - Set "2: degree" when executing unlimited length feed in the absolute position system.

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.456)

Refer to the following for the buffer memory address in this area.
→Page 423 Positioning parameters: Basic parameters 1

#### [Pr.2] to [Pr.4] Electronic gear (Movement amount per pulse) ([Pr.2]～[Pr.4]電子ギア(1パルスあたりの移動量)) (11.3 / original p.457)

Mechanical system value used when the Simple Motion module/Motion module performs positioning control.
The settings are made using [Pr.2] to [Pr.4].
The electronic gear is expressed by the following equation.

```
Electronic gear = [Pr.2] Number of pulses per rotation (AP) / ([Pr.3] Movement amount per rotation (AL) × [Pr.4] Unit magnification (AM))
```

When positioning has been performed, an error (mechanical system error) may be produced between the specified movement amount and the actual movement amount.
The error can be compensated by adjusting the value set in electronic gear.
→Page 229 Electronic gear function

> **Point**
> - Set the electronic gear within the following range. If the value outside the setting range is set, the error "Outside electronic gear setting range" (error code: 1A68H [FX5-SSC-S], or error code: 1B68H [FX5-SSC-G]) will occur.
>   [FX5-SSC-S]/[FX5-SSC-G] Ver.1.001 or earlier
>   `0.001 ≤ Electronic gear (AP / (AL × AM)) ≤ 320000`
>   [FX5-SSC-G] Ver.1.002 or later
>   The range is not checked.
> - The result of below calculation (round up after decimal point) is a minimum pulse when the command position value is updated at follow up processing. (The movement amount for droop pulse is reflected as the command position value when the droop pulse becomes more than above calculated value in pulse unit of motor end.)
>   [Pr.2] Number of pulses per rotation (AP) / [Pr.3] (Movement amount per rotation (AL) × [Pr.4] Unit magnification (AM)) [pulse]
>   Refer to the following for the follow up processing.
>   →Page 315 Follow up function

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.457)

Refer to the following for the buffer memory address in this area.
→Page 423 Positioning parameters: Basic parameters 1

#### [Pr.2] Number of pulses per rotation (AP) ([Pr.2]1回転あたりのパルス数(AP)) (11.3 / original p.458)

Set the number of pulses required for a complete rotation of the motor shaft.
[FX5-SSC-S]
If you are using the Mitsubishi servo amplifier MR-J4(W)-B/MR-JE-B(F)/MR-J3(W)-B, set the value given as the "resolution per servo motor rotation" in the speed/position detector specifications.
Number of pulses per rotation (AP) = Resolution per servo motor rotation
When using MR-J5(W)-B, refer to the following.
→Page 229 Electronic gear function
[FX5-SSC-G]
When using MR-J5(W)-G/MR-JET-G, add the electronic gear of the servo amplifier when setting.
Number of pulses per rotation (AP) = Servo motor resolution per rotation × Electronic gear denominator (PA07) / Electronic gear numerator (PA06)

> **Point**
> [FX5-SSC-G]
> When using the MR-J5(W)-G rotary servo motor, the servo motor resolution per rotation is 26 bits (67108864).
> However, set the number of pulses per rotation (AP) to 22 bits (4194304) to account for Electronic gear numerator (PA06)/Electronic gear denominator (PA07) of the servo amplifier being overwritten from the controller to 1/16 of their values.

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.458)

Refer to the following for the buffer memory address in this area.
→Page 423 Positioning parameters: Basic parameters 1

#### [Pr.3] Movement amount per rotation (AL), [Pr.4] Unit magnification (AM) ([Pr.3]1回転あたりの移動量(AL)，[Pr.4]単位倍率(AM)) (11.3 / original p.458)

The amount how the workpiece moves with one motor rotation is determined by the mechanical structure.
If the worm gear lead (μm/rev) is PB and the deceleration rate is 1/n, then
Movement amount per rotation (AL) = PB × 1/n
However, the maximum value that can be set for this "movement amount per rotation (AL)" parameter is 20000000.0 μm (20 m). Set the "movement amount per rotation (AL)" as shown below so that the "movement amount per rotation (AL)" does not exceed this maximum value.
Movement amount per rotation (AL)
= PB × 1/n
= Movement amount per rotation (AL) × Unit magnification (AM)*1

*1 The unit magnification (AM) is a value of 1, 10, 100 or 1000. If the "PB × 1/n" value exceeds 20000000.0 μm (20 m), adjust with the unit magnification so that the "movement amount per rotation (AL)" does not exceed 20000000.0 μm (20 m).

| [Pr.1] setting value | Value set with the engineering tool (unit) | Value set with a program (unit) |
|---|---|---|
| 0: mm | 0.1 to 20000000.0 (μm) | 1 to 200000000 (× 10^-1 μm) |
| 1: inch | 0.00001 to 2000.00000 (inch) | 1 to 200000000 (× 10^-5 inch) |
| 2: degree | 0.00001 to 2000.00000 (degree) | 1 to 200000000 (× 10^-5 degree) |
| 3: pulse | 1 to 200000000 (pulse) | 1 to 200000000 (pulse) |

Refer to the following for information about electric gear.
→Page 229 Electronic gear function

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.458)

Refer to the following for the buffer memory address in this area.
→Page 423 Positioning parameters: Basic parameters 1

#### [Pr.7] Bias speed at start ([Pr.7]始動時バイアス速度) (11.3 / original p.459-460)

Set the bias speed (minimum speed) upon starting. When using a stepping motor, etc., set it to start the motor smoothly. (If the motor speed at start is low, the stepping motor does not start smoothly.)
The specified "bias speed at start" will be valid during the following operations:
- Positioning operation
- Home position return operation
- JOG operation

Set the value that the bias speed should not exceed "[Pr.8] Speed limit value".

| [Pr.1] setting value | Value set with the engineering tool (unit) | Value set with a program (unit) |
|---|---|---|
| 0: mm | 0.00 to 20000000.00 (mm/min) | 0 to 2000000000 (× 10^-2 mm/min) |
| 1: inch | 0.000 to 2000000.000 (inch/min) | 0 to 2000000000 (× 10^-3 inch/min) |
| 2: degree | 0.000 to 2000000.000 (degree/min)*1 | 0 to 2000000000 (× 10^-3 degree/min)*2 |
| 3: pulse | 0 to 1000000000 (pulse/s) | 0 to 1000000000 (pulse/s) |

*1 Range of speed limit value when "[Pr.83] Speed control 10 × multiplier setting for degree axis" is set to valid: 0.00 to 20000000.00 (degree/min)
*2 Range of speed limit value when "[Pr.83] Speed control 10 × multiplier setting for degree axis" is set to valid: 0 to 2000000000 (× 10^-2 degree/min)

*(Note: the footnotes of the [Pr.7] Bias speed at start table say "Range of speed limit value" as printed in the original.)*

[Figure] Trapezoidal acceleration/deceleration (S-curve ratio is 0%) (original p.459)
- Vertical axis V, horizontal axis t. Levels marked: [Pr.8] Speed limit value (top), [Da.8] Command speed, [Pr.7] Bias speed at start
- The speed jumps from 0 to [Pr.7] Bias speed at start at start, rises linearly to [Da.8] Command speed, runs constant, decreases linearly to the bias speed, then drops to 0
- The acceleration slope is defined by the dashed line from 0 to [Pr.8] Speed limit value over "Acceleration time" ([Pr.9] Acceleration time 0 / [Pr.25] Acceleration time 1 / [Pr.26] Acceleration time 2 / [Pr.27] Acceleration time 3); deceleration likewise from [Pr.8] to 0 over "Deceleration time" ([Pr.10] Deceleration time 0 / [Pr.28] Deceleration time 1 / [Pr.29] Deceleration time 2 / [Pr.30] Deceleration time 3)
- "Actual acceleration time" = the time from bias speed to command speed (shorter than the acceleration time); "Actual deceleration time" = the time from command speed to bias speed

[Figure] S-curve acceleration/deceleration (S-curve ratio is other than 0%) (original p.459)
- Same levels and time labels as the trapezoidal figure; the section between [Pr.7] Bias speed at start and [Da.8] Command speed is an S-curve instead of a straight line
- Actual acceleration time / Actual deceleration time are measured between bias speed and command speed; Acceleration time / Deceleration time ([Pr.9], [Pr.25] to [Pr.27] / [Pr.10], [Pr.28] to [Pr.30]) refer to 0 ↔ [Pr.8] Speed limit value

> **Point**
> For the 2-axis or more interpolation control, the bias speed at start is applied by the setting of "[Pr.20] Interpolation speed designation method".
> - "0: Composite speed": Bias speed at start set to the reference axis is applied to the composite command speed.
> - "1: Reference axis speed": Bias speed at start is applied to the reference axis.

##### ■Precautions (注意事項) (11.3 / original p.460)

- Set "0" because "[Pr.7] Bias speed at start" is valid regardless of motor type. Otherwise, it may cause vibration or impact even though an error does not occur.
- Set "[Pr.7] Bias speed at start" according to the specification of stepping motor driver. If the setting is outside the range, it may cause the following troubles by rapid speed change or overload.
  - Stepping motor steps out.
  - An error occurs in the stepping motor driver.
- In synchronous control, when "[Pr.7] Bias speed at start" is set to the servo input axis, the bias speed at start is applied to the servo input axis. Note that the unexpected operation might be generated to the output axis.
- Set "[Pr.7] Bias speed at start" within the following range.
"[Pr.8] Speed limit value" ≥ "[Pr.46] Home position return speed" ≥ "[Pr.47] Creep speed" ≥ "[Pr.7] Bias speed at start"
- If the data ("[Da.8] Command speed" of positioning data, "[Da.8] Command speed" of next point for continuous path control, or "[Cd.14] New speed value" for speed change function) is less than "[Pr.7] Bias speed at start", the warning "Below bias speed" (warning code: 0908H [FX5-SSC-S], or warning code: 0D08H [FX5-SSC-G]) will occur and it will operate at "[Pr.7] Bias speed at start".
- When using S-curve acceleration/deceleration processing and bias speed at start together, S-curve acceleration/deceleration processing is carried out based on the acceleration/deceleration time set by user, "[Pr.8] Speed limit value" and "[Pr.35] S-curve ratio" (1 to 100%) in the section of acceleration/deceleration from bias speed at start to command speed.

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.460)

Refer to the following for the buffer memory address in this area.
→Page 423 Positioning parameters: Basic parameters 1

### Basic parameters2 (基本パラメータ2) (11.3 / original p.461)

This section describes the details on the basic parameter 2.
n: Axis No. - 1

| Item | Setting value, setting range: Value set with the engineering tool | Setting value, setting range: Value set with a program | Default value | Buffer memory address |
|---|---|---|---|---|
| [Pr.8] Speed limit value | The setting range differs depending on the "[Pr.1] Unit setting". | The setting range differs depending on the "[Pr.1] Unit setting". | 200000 | 10+150n<br>11+150n |
| [Pr.9] Acceleration time 0 | 1 to 8388608 (ms) | 1 to 8388608 (ms) | 1000 | 12+150n<br>13+150n |
| [Pr.10] Deceleration time 0 | 1 to 8388608 (ms) | 1 to 8388608 (ms) | 1000 | 14+150n<br>15+150n |

*In the original, "Setting value, setting range" is a 2-level header. For [Pr.8], one cell spans both setting-value columns. Expanded to each column.

#### [Pr.8] Speed limit value ([Pr.8]速度制限値) (11.3 / original p.461)

Set the maximum speed during positioning, home position return and speed-torque operations.

| [Pr.1] setting value | Value set with the engineering tool (unit) | Value set with a program (unit) |
|---|---|---|
| 0: mm | 0.01 to 20000000.00 (mm/min) | 1 to 2000000000 (× 10^-2 mm/min) |
| 1: inch | 0.001 to 2000000.000 (inch/min) | 1 to 2000000000 (× 10^-3 inch/min) |
| 2: degree | 0.001 to 2000000.000 (degree/min)*1 | 1 to 2000000000 (× 10^-3 degree/min)*2 |
| 3: pulse | 1 to 1000000000 (pulse/s) | 1 to 1000000000 (pulse/s) |

*1 Range of speed limit value when "[Pr.83] Speed control 10 × multiplier setting for degree axis" is set to valid: 0.01 to 20000000.00 (degree/min).
*2 Range of speed limit value when "[Pr.83] Speed control 10 × multiplier setting for degree axis" is set to valid: 1 to 2000000000 (× 10^-2 degree/min)

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.461)

Refer to the following for the buffer memory address in this area.
→Page 423 Positioning parameters: Basic parameters 2

#### [Pr.9] Acceleration time 0, [Pr.10] Deceleration time 0 ([Pr.9]加速時間0，[Pr.10]減速時間0) (11.3 / original p.461)

"[Pr.9] Acceleration time 0" specifies the time for the speed to increase from zero to the "[Pr.8] Speed limit value" ("[Pr.31] JOG speed limit value" at JOG operation control). "[Pr.10] Deceleration time 0" specifies the time for the speed to decrease from the "[Pr.8] Speed limit value" ("[Pr.31] JOG speed limit value" at JOG operation control) to zero.

[Figure] Acceleration time 0 / Deceleration time 0 (original p.461)
- Axes: Velocity / Time. Levels: [Pr.8] Speed limit value (upper), Positioning speed (lower)
- Dashed slopes from 0 to [Pr.8] Speed limit value over "[Pr.9] Acceleration time 0" and from [Pr.8] to 0 over "[Pr.10] Deceleration time 0"
- The actual operation at the lower positioning speed follows the same slope, so "Actual acceleration time" and "Actual deceleration time" are shorter than [Pr.9]/[Pr.10]

- If the positioning speed is set lower than the parameter-defined speed limit value, the actual acceleration/deceleration time will be relatively short. Thus, set the maximum positioning speed equal to or only a little lower than the parameter-defined speed limit value.
- These settings are valid for home position return, positioning and JOG operations.
- When the positioning involves interpolation, the acceleration/deceleration time defined for the reference axis is valid.

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.461)

Refer to the following for the buffer memory address in this area.
→Page 423 Positioning parameters: Basic parameters 2

### Detailed parameters1 (詳細パラメータ1) (11.3 / original p.462-471)

n: Axis No. - 1

| Item | Setting value, setting range: Value set with the engineering tool | Setting value, setting range: Value set with a program | Default value | Buffer memory address |
|---|---|---|---|---|
| [Pr.11] Backlash compensation amount | The setting value range differs according to the "[Pr.1] Unit setting". | The setting value range differs according to the "[Pr.1] Unit setting". | 0 | 17+150n |
| [Pr.12] Software stroke limit upper limit value | The setting value range differs according to the "[Pr.1] Unit setting". | The setting value range differs according to the "[Pr.1] Unit setting". | 2147483647 | 18+150n<br>19+150n |
| [Pr.13] Software stroke limit lower limit value | The setting value range differs according to the "[Pr.1] Unit setting". | The setting value range differs according to the "[Pr.1] Unit setting". | -2147483648 | 20+150n<br>21+150n |
| [Pr.14] Software stroke limit selection | 0: Apply software stroke limit on command position value | 0 | 0 | 22+150n |
| [Pr.14] Software stroke limit selection | 1: Apply software stroke limit on machine feed value | 1 | 0 | 22+150n |
| [Pr.15] Software stroke limit valid/invalid setting | 0: Software stroke limit valid during JOG operation, inching operation and manual pulse generator operation | 0 | 0 | 23+150n |
| [Pr.15] Software stroke limit valid/invalid setting | 1: Software stroke limit invalid during JOG operation, inching operation and manual pulse generator operation | 1 | 0 | 23+150n |
| [Pr.16] Command in-position width | The setting value range differs depending on the "[Pr.1] Unit setting". | The setting value range differs depending on the "[Pr.1] Unit setting". | 100 | 24+150n<br>25+150n |
| [Pr.17] Torque limit setting value | 0.1 to 1000.0 (%) | 1 to 10000 (× 0.1%) | 3000 | 26+150n |
| [Pr.18] M code ON signal output timing | 0: WITH mode | 0 | 0 | 27+150n |
| [Pr.18] M code ON signal output timing | 1: AFTER mode | 1 | 0 | 27+150n |
| [Pr.19] Speed switching mode | 0: Standard speed switching mode | 0 | 0 | 28+150n |
| [Pr.19] Speed switching mode | 1: Front-loading speed switching mode | 1 | 0 | 28+150n |
| [Pr.20] Interpolation speed designation method | 0: Composite speed | 0 | 0 | 29+150n |
| [Pr.20] Interpolation speed designation method | 1: Reference axis speed | 1 | 0 | 29+150n |
| [Pr.21] Command position value during speed control | 0: Do not update command position value | 0 | 0 | 30+150n |
| [Pr.21] Command position value during speed control | 1: Update command position value | 1 | 0 | 30+150n |
| [Pr.21] Command position value during speed control | 2: Clear command position value to zero | 2 | 0 | 30+150n |
| [Pr.22] Input signal logic selection | b0: Lower limit — 0: Negative logic / 1: Positive logic | (bit image, see figure below) | 0 | 31+150n |
| [Pr.22] Input signal logic selection | b1: Upper limit — 0: Negative logic / 1: Positive logic | (bit image, see figure below) | 0 | 31+150n |
| [Pr.22] Input signal logic selection | b2: Not used | (bit image, see figure below) | 0 | 31+150n |
| [Pr.22] Input signal logic selection | b3: Stop signal — 0: Negative logic / 1: Positive logic | (bit image, see figure below) | 0 | 31+150n |
| [Pr.22] Input signal logic selection | b4: Not used [FX5-SSC-S] / External command/switching signal [FX5-SSC-G] — 0: Negative logic / 1: Positive logic | (bit image, see figure below) | 0 | 31+150n |
| [Pr.22] Input signal logic selection | b5: Not used | (bit image, see figure below) | 0 | 31+150n |
| [Pr.22] Input signal logic selection | b6: Proximity dog signal — 0: Negative logic / 1: Positive logic | (bit image, see figure below) | 0 | 31+150n |
| [Pr.22] Input signal logic selection | b7 to b15: Not used | (bit image, see figure below) | 0 | 31+150n |
| [Pr.81] Speed-position function selection | 0: Speed-position switching control (INC mode) | 0 | 0 | 34+150n |
| [Pr.81] Speed-position function selection | 2: Speed-position switching control (ABS mode) | 2 | 0 | 34+150n |
| [Pr.116] FLS signal selection | 1 (0001H): Servo amplifier*1<br>2 (0002H): Buffer memory<br>3 (0003H): Link device [FX5-SSC-G] | 1*1<br>2<br>3 | 0001H | 116+150n |
| [Pr.117] RLS signal selection | 1 (0001H): Servo amplifier*1<br>2 (0002H): Buffer memory<br>3 (0003H): Link device [FX5-SSC-G] | 1*1<br>2<br>3 | 0001H | 117+150n |
| [Pr.118] DOG signal selection | 1 (0001H): Servo amplifier*1<br>2 (0002H): Buffer memory<br>3 (0003H): Link device [FX5-SSC-G] | 1*1<br>2<br>3 | 0001H | 118+150n |
| [Pr.119] STOP signal selection | 1 (0001H): Servo amplifier*1<br>2 (0002H): Buffer memory<br>3 (0003H): Link device [FX5-SSC-G] | 1*1<br>2<br>3 | 0002H | 119+150n |

*1 The setting is not available in "[Pr.119] STOP signal selection".

*In the original, "Setting value, setting range" is a 2-level header. The table continues from p.462 to p.463 ([Pr.116] to [Pr.119] on p.463). One cell spans both setting-value columns over [Pr.11] to [Pr.13] ("The setting value range differs according to the "[Pr.1] Unit setting"."), and for [Pr.16]. Item, Default value and Buffer memory address cells are merged over the setting-value rows of each parameter. For [Pr.22], the bit column (b0 to b7 to b15) and signal-name column are separate cells, the setting cell "0: Negative logic / 1: Positive logic" is one cell spanning all bits, and the "Value set with a program" column shows a bit image instead of values. For [Pr.116] to [Pr.119], the two setting-value cells are merged over the 4 parameters. Expanded to each row.

[Figure] [Pr.22] Input signal logic selection — bit image in the "Value set with a program" column (original p.462)
- A 16-bit word b15 (left) to b0 (right)
- An arrow bracket spanning the upper bits (b15 to b7) and leader lines to individual unused bits in the lower byte point to the note "Always "0" is set to the part not used."

#### [Pr.11] Backlash compensation amount ([Pr.11]バックラッシュ補正量) (11.3 / original p.464)

The error that occurs due to backlash when moving the machine via gears can be compensated.
(When the backlash compensation amount is set, commands equivalent to the compensation amount will be output each time the direction changes during positioning.)

[Figure] Backlash (original p.464)
- A workpiece (moving body) engages a worm gear; the arrow "[Pr.44] Home position return direction" points to the left
- The gap between the workpiece tooth and the worm gear tooth is labeled "Backlash (compensation amount)"

- The backlash compensation is valid after machine home position return. Thus, if the backlash compensation amount is set or changed, always carry out machine home position return once.
- "[Pr.2] Number of pulses per rotation (AP)", "[Pr.3] Movement amount per rotation (AL)", "[Pr.4] Unit magnification (AM)" and "[Pr.11] Backlash compensation amount" which satisfies the following (1) can be set up.

```
0 ≤ ([Pr.11] Backlash compensation amount) × ([Pr.2] Number of pulses per rotation (AP))
    / (([Pr.3] Movement amount per rotation (AL)) × ([Pr.4] Unit magnification (AM)))  (= A) ≤ 4194303 (pulse): (1)
    (round down after decimal point)
```

The error "Backlash compensation amount error" (error code: 1AA0H [FX5-SSC-S], or error code 1BA0H [FX5-SSC-G]) occurs when the setting is outside the range of the calculation result of (1).
A servo alarm (error code: 2031, 2035, etc.) may occur by kinds of servo amplifier (servo motor), load inertia moment and the amount of command of a cycle time (Simple Motion module/Motion module) even if the setting is within the calculation result of (1).
Reduce the setting value of "[Pr.11] Backlash compensation amount" if a servo alarm occurs. Use the value of the following (2) as a measure that a servo alarm does not occur.

```
A ≤ (Maximum motor speed (r/min)) × 1.2 × (Encoder resolution (pulse/rev)) × (Operation cycle (ms))
    / (60 (s) × 1000 (ms))  (pulse): (2)
```

The backlash compensation amount is output all at one operation cycle.

| [Pr.1] setting value | Value set with the engineering tool (unit) | Value set with a program (unit)*1 |
|---|---|---|
| 0: mm | 0 to 6553.5 (μm) | 0 to 65535 (× 10^-1 μm) |
| 1: inch | 0 to 0.65535 (inch) | 0 to 65535 (× 10^-5 inch) |
| 2: degree | 0 to 0.65535 (degree) | 0 to 65535 (× 10^-5 degree) |
| 3: pulse | 0 to 65535 (pulse) | 0 to 65535 (pulse) |

*1 0 to 32767: Set as a decimal
32768 to 65535: Convert into hexadecimal and set

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.464)

Refer to the following for the buffer memory address in this area.
→Page 423 Positioning parameters: Detailed parameters 1

#### [Pr.12] Software stroke limit upper limit value ([Pr.12]ソフトウェアストロークリミット上限値) (11.3 / original p.465)

Set the upper limit for the machine's movement range during positioning control.

| [Pr.1] setting value | Value set with the engineering tool (unit) | Value set with a program (unit) |
|---|---|---|
| 0: mm | -214748364.8 to 214748364.7 (μm) | -2147483648 to 2147483647 (× 10^-1 μm) |
| 1: inch | -21474.83648 to 21474.83647 (inch) | -2147483648 to 2147483647 (× 10^-5 inch) |
| 2: degree | 0 to 359.99999 (degree) | 0 to 35999999 (× 10^-5 degree) |
| 3: pulse | -2147483648 to 2147483647 (pulse) | -2147483648 to 2147483647 (pulse) |

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.465)

Refer to the following for the buffer memory address in this area.
→Page 423 Positioning parameters: Detailed parameters 1

#### [Pr.13] Software stroke limit lower limit value ([Pr.13]ソフトウェアストロークリミット下限値) (11.3 / original p.465)

Set the lower limit for the machine's movement range during positioning control.

[Figure] Software stroke limit (original p.465)
- A ball screw with a table; from left: Emergency stop limit switch, Software stroke limit lower limit, ..., Software stroke limit upper limit, Emergency stop limit switch
- "(Machine movement range)" is between the software stroke limit lower limit and upper limit
- "Home position" is shown at the software stroke limit lower limit position
- The emergency stop limit switches are outside the software stroke limit range at both ends

- Generally, the home position is set at the lower limit or upper limit of the stroke limit.
- By setting the upper limit value or lower limit value of the software stroke limit, overrun can be prevented in the software. However, an emergency stop limit switch must be installed nearby outside the range. To invalidate the software stroke limit, set the setting value to "upper limit value = lower limit value". (If it is within the setting range, the setting value can be anything.) When the unit is "degree", the software stroke limit check is invalid during speed control (including the speed control in speed-position and position-speed switching control) or during manual control.

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.465)

Refer to the following for the buffer memory address in this area.
→Page 423 Positioning parameters: Detailed parameters 1

#### [Pr.14] Software stroke limit selection ([Pr.14]ソフトウェアストロークリミット選択) (11.3 / original p.465)

Set whether to apply the software stroke limit on the "command position value" or the "machine feed value". The software stroke limit will be validated according to the set value. To invalidate the software stroke limit, set the setting value to "command position value".
When "2: degree" is set in "[Pr.1] Unit setting", set the setting value of software stroke limit to "command position value". The error "Software stroke limit selection" (error code: 1AA5H [FX5-SSC-S], or error code: 1BA5H [FX5-SSC-G]) will occur if "machine feed value" is set.

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.465)

Refer to the following for the buffer memory address in this area.
→Page 423 Positioning parameters: Detailed parameters 1

#### [Pr.15] Software stroke limit valid/invalid setting ([Pr.15]ソフトウェアストロークリミット有効／無効設定) (11.3 / original p.465)

Set whether to validate the software stroke limit during JOG/Inching operation and manual pulse generator operation.

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.465)

Refer to the following for the buffer memory address in this area.
→Page 423 Positioning parameters: Detailed parameters 1

#### [Pr.16] Command in-position width ([Pr.16]指令インポジション範囲) (11.3 / original p.466)

Set the remaining distance that turns the command in-position flag ON. The command in-position signal is used as a front-loading signal of the positioning complete signal. When the remaining distance to the stop position during the automatic deceleration of positioning control becomes equal to or less than the value set in command in-position width, the command in-position flag turns ON.

[Figure] Command in-position width (original p.466)
- Velocity profile: trapezoid starting at "Positioning control start"
- Command in-position flag: ON before the start, turns OFF at positioning control start, and turns ON again when the remaining distance becomes equal to or less than "[Pr.16] Command in-position width" (during deceleration, before the stop)

| [Pr.1] setting value | Value set with the engineering tool (unit) | Value set with a program (unit) |
|---|---|---|
| 0: mm | 0.1 to 214748364.7 (μm) | 1 to 2147483647 (× 10^-1 μm) |
| 1: inch | 0.00001 to 21474.83647 (inch) | 1 to 2147483647 (× 10^-5 inch) |
| 2: degree | 0.00001 to 21474.83647 (degree) | 1 to 2147483647 (× 10^-5 degree) |
| 3: pulse | 1 to 2147483647 (pulse) | 1 to 2147483647 (pulse) |

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.466)

Refer to the following for the buffer memory address in this area.
→Page 423 Positioning parameters: Detailed parameters 1

#### [Pr.17] Torque limit setting value ([Pr.17]トルク制限設定値) (11.3 / original p.466)

Set the maximum value of the torque generated by the servo motor as a percentage between 0.1 and 1000.0%.
The torque limit function limits the torque generated by the servo motor within the set range.
If the torque required for control exceeds the torque limit value, it is controlled with the set torque limit value.
→Page 241 Torque limit function

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.466)

Refer to the following for the buffer memory address in this area.
→Page 423 Positioning parameters: Detailed parameters 1

#### [Pr.18] M code ON signal output timing ([Pr.18]MコードON信号出力タイミング) (11.3 / original p.467)

This parameter sets the M code ON signal output timing.
Choose either WITH mode or AFTER mode as the M code ON signal output timing.

##### ■Operation example (動作例) (11.3 / original p.467)

WITH mode: An M code is output and the M code ON signal is turned ON when a positioning operation starts.
AFTER mode*2: An M code is output and the M code ON signal is turned ON when a positioning operation completes.

[Figure] WITH mode (original p.467)
- Signals: [Cd.184] Positioning start, [Md.141] BUSY, M code ON signal ([Md.31] Status: b12), [Cd.7] M code OFF request, [Md.25] Valid M code, Positioning, [Da.1] Operation pattern (01 (continuous) then 00 (end))
- [Cd.184] Positioning start ON → [Md.141] BUSY ON → at the start of the first positioning, [Md.25] Valid M code becomes m1*1 and the M code ON signal turns ON
- [Cd.7] M code OFF request ON → M code ON signal OFF → [Cd.7] OFF
- At the start of the second positioning (00 (end)), [Md.25] becomes m2*1 and the M code ON signal turns ON again; it is turned OFF by [Cd.7] M code OFF request in the same way
- After the second positioning ends, [Md.141] BUSY turns OFF; [Cd.184] Positioning start turns OFF at the end

[Figure] AFTER mode*2 (original p.467)
- Signals: Positioning complete signal ([Md.31] Status: b15), [Md.141] BUSY, M code ON signal ([Md.31] Status: b12), [Cd.7] M code OFF request, [Md.25] Valid M code, Positioning, [Da.1] Operation pattern (01 (continuous) then 00 (end))
- When the first positioning (01 (continuous)) completes, the positioning complete signal (b15) pulses ON, [Md.25] Valid M code becomes m1*1 and the M code ON signal turns ON
- [Cd.7] M code OFF request ON → M code ON signal OFF → [Cd.7] OFF; the second positioning is executed
- When the second positioning (00 (end)) completes, b15 pulses ON, [Md.141] BUSY turns OFF, [Md.25] becomes m2*1 and the M code ON signal turns ON

*1 m1 and m2 indicate set M codes.
*2 If AFTER mode is used with speed control, an M code will not be output and the M code ON signal will not be turned ON.

An M code is a number between 0 and 65535 that can be assigned to each positioning data ([Da.10] M code/Condition data No./Number of LOOP to LEND repetitions).
The program can be coded to read an M code from the buffer memory address specified by "[Md.25] Valid M code" whenever the M code ON signal turns ON so that a command for the sub work (e.g. clamping, drilling, or tool change) associated with the M code can be issued.

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.467)

Refer to the following for the buffer memory address in this area.
→Page 423 Positioning parameters: Detailed parameters 1

#### [Pr.19] Speed switching mode ([Pr.19]速度切換えモード) (11.3 / original p.468)

Set whether to switch the speed switching mode with the standard switching or front-loading switching mode.
- Speed of positioning data No.n > Speed of positioning data No.n + 1
  Decelerates at deceleration time No. of Positioning data No.n + 1
- Speed of positioning data No.n < Speed of positioning data No.n + 1
  Accelerates at acceleration time No. of Positioning data No.n + 1

| Setting value | Details |
|---|---|
| 0: Standard switching | Switch the speed when executing the next positioning data. |
| 1: Front-loading switching | The speed switches at the end of the positioning data currently being executed. |

[Figure] Speed switching (original p.468)
- n: Positioning data No.
- <For standard switching>: the speed stays at the speed of data n until the end of n; the speed change (acceleration) starts at the boundary n / n + 1 — "Switch the speed when executing the next positioning data"
- <For front-loading switching>: the speed change is completed by the end of data n — "The next positioning data starts positioning at the designated speed"

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.468)

Refer to the following for the buffer memory address in this area.
→Page 423 Positioning parameters: Detailed parameters 1

#### [Pr.20] Interpolation speed designation method ([Pr.20]補間速度指定方法) (11.3 / original p.469)

When carrying out linear interpolation/circular interpolation, set whether to designate the composite speed or reference axis speed.

| Setting value | Details |
|---|---|
| 0: Composite speed | The movement speed for the control target is designated, and the speed for each axis is calculated by the Simple Motion module/Motion module. |
| 1: Reference axis speed | The axis speed set for the reference axis is designated, and the speed for the other axis carrying out interpolation is calculated by the Simple Motion module/Motion module. |

[Figure] Interpolation speed designation (original p.469)
- <When composite speed is designated>: X axis / Y axis; the diagonal (composite) vector is "Designate composite speed"; the X and Y axis components are "Calculated by Simple Motion module"
- <When reference axis speed is designated>: the X axis component is "Designate speed for reference axis"; the Y axis component is "Calculated by Simple Motion module"

> **Point**
> Always specify the "reference axis speed" if 4-axis linear interpolation or 2 to 4 axis speed control has to be performed.
> If you specify the "composite speed" for 4-axis linear interpolation or 2 to 4 axis speed control, the error "Interpolation mode error" (error code: 199AH [FX5-SSC-S], or error code: 1A9AH [FX5-SSC-G]) occurs when the positioning operation is started.
> For the 2-axis circular interpolation control, specify the "composite speed" always. If you specify the "reference axis speed" for the 2-axis circular interpolation control when the positioning operation is started, the error "Interpolation mode error" (error code: 199AH [FX5-SSC-S], or error code: 1A9BH*1 [FX5-SSC-G]) occurs.

*1 1A9AH for the software version 1.000.

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.469)

Refer to the following for the buffer memory address in this area.
→Page 423 Positioning parameters: Detailed parameters 1

#### [Pr.21] Command position value during speed control ([Pr.21]速度制御時の送り現在値) (11.3 / original p.469)

Specify whether you wish to enable or disable the update of "[Md.20] Command position value" while operations are performed under the speed control (including the speed control in speed-position and position-speed switching control).

| Setting value | Details |
|---|---|
| 0: The update of the command position value is disabled | The command position value will not change. (The value at the beginning of the speed control will be kept.) |
| 1: The update of the command position value is enabled | The command position value will be updated. (The command position value will change from the initial.) |
| 2: The command position value is cleared to zero | The command position value will be set initially to zero and change from zero while the speed control is in effect. |

> **Point**
> - When the speed control is performed over two to four axes, the choice between enabling and disabling the update of "[Md.20] Command position value" depends on how the reference axis is set.
> - Set "1" to exercise speed-position switching control (ABS mode).

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.469)

Refer to the following for the buffer memory address in this area.
→Page 423 Positioning parameters: Detailed parameters 1

#### [Pr.22] Input signal logic selection ([Pr.22]入力信号論理選択) (11.3 / original p.470)

Set the input signal logic that matches the signaling specification of the external input signal (upper/lower limit switch, proximity dog) of servo amplifier connected to the Simple Motion module/Motion module or "[Cd.44] External input signal operation device (Axis 1 to 8)".

##### ■Negative logic (負論理) (11.3 / original p.470)

- The current is not flowed through the input signal contact.
  - FLS, RLS: Limit signal ON
  - DOG, DI, STOP: Invalid
- The current is flowed through the input signal contact.
  - FLS, RLS: Limit signal OFF
  - DOG, DI, STOP: Valid

##### ■Positive logic (正論理) (11.3 / original p.470)

Opposite the concept of negative logic.

> **Point**
> A mismatch in the signal logic will disable normal operation. Be careful of this when you change from the default value.

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.470)

Refer to the following for the buffer memory address in this area.
→Page 423 Positioning parameters: Detailed parameters 1

#### [Pr.81] Speed-position function selection ([Pr.81]速度・位置機能選択) (11.3 / original p.470)

Select the mode of speed-position switching control.
0: INC mode
2: ABS mode

> **Point**
> If the setting is other than 0 and 2, operation is performed in the INC mode with the setting regarded as 0.

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.470)

Refer to the following for the buffer memory address in this area.
→Page 423 Positioning parameters: Detailed parameters 1

#### [Pr.116] to [Pr.119] FLS/RLS/DOG/STOP signal selection ([Pr.116]～[Pr.119]FLS/RLS/DOG/STOP信号選択) (11.3 / original p.471)

##### ■Input type (入力種別) (11.3 / original p.471)

Set the input type whose external input signal (upper/lower limit signal (FLS/RLS), proximity dog signal (DOG) or stop signal (STOP)) is used.
1 (0001H): Servo amplifier*1*2 (Uses the external input signal of the servo amplifier.)
2 (0002H): Buffer memory (Uses the buffer memory of the Simple Motion module/Motion module.)
3 (0003H): Link device (Uses the link device.) [FX5-SSC-G]

*1 The setting is not available in "[Pr.119] STOP signal selection". If it is set, the error "STOP signal selection error" (error code: 1AD3H [FX5-SSC-S], or error code: 1BD3H [FX5-SSC-G]) occurs and the "[Cd.190] PLC READY" is not turned ON.
*2 At MR-JE-B(F) use, refer to the following.
→Page 823 Connection with MR-JE-B(F)

> **Point**
> [FX5-SSC-G]
> If "3: Link device" is selected, specify the link device to be used for the external input signals (upper/lower limit signal (FLS/RLS), proximity dog signal (DOG), stop signal (STOP)) by using the following parameters.
> - [Pr.910], [Pr.920], [Pr.930], [Pr.940] Link device type
> - [Pr.911], [Pr.921], [Pr.931], [Pr.941] Link device start No.
> - [Pr.912], [Pr.922], [Pr.932], [Pr.942] Link device bit specification
> - [Pr.913], [Pr.923], [Pr.933], [Pr.943] Link device logic setting

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.471)

Refer to the following for the buffer memory address in this area.
→Page 423 Positioning parameters: Detailed parameters 1

### Detailed parameters2 (詳細パラメータ2) (11.3 / original p.472-484)

n: Axis No. - 1

| Item | Setting value, setting range: Value set with the engineering tool | Setting value, setting range: Value set with a program | Default value | Buffer memory address |
|---|---|---|---|---|
| [Pr.25] Acceleration time 1 | 1 to 8388608 (ms) | 1 to 8388608 (ms) | 1000 | 36+150n<br>37+150n |
| [Pr.26] Acceleration time 2 | 1 to 8388608 (ms) | 1 to 8388608 (ms) | 1000 | 38+150n<br>39+150n |
| [Pr.27] Acceleration time 3 | 1 to 8388608 (ms) | 1 to 8388608 (ms) | 1000 | 40+150n<br>41+150n |
| [Pr.28] Deceleration time 1 | 1 to 8388608 (ms) | 1 to 8388608 (ms) | 1000 | 42+150n<br>43+150n |
| [Pr.29] Deceleration time 2 | 1 to 8388608 (ms) | 1 to 8388608 (ms) | 1000 | 44+150n<br>45+150n |
| [Pr.30] Deceleration time 3 | 1 to 8388608 (ms) | 1 to 8388608 (ms) | 1000 | 46+150n<br>47+150n |
| [Pr.31] JOG speed limit value | The setting range differs depending on the "[Pr.1] Unit setting". | The setting range differs depending on the "[Pr.1] Unit setting". | 20000 | 48+150n<br>49+150n |
| [Pr.32] JOG operation acceleration time selection | 0: [Pr.9] Acceleration time 0 | 0 | 0 | 50+150n |
| [Pr.32] JOG operation acceleration time selection | 1: [Pr.25] Acceleration time 1 | 1 | 0 | 50+150n |
| [Pr.32] JOG operation acceleration time selection | 2: [Pr.26] Acceleration time 2 | 2 | 0 | 50+150n |
| [Pr.32] JOG operation acceleration time selection | 3: [Pr.27] Acceleration time 3 | 3 | 0 | 50+150n |
| [Pr.33] JOG operation deceleration time selection | 0: [Pr.10] Deceleration time 0 | 0 | 0 | 51+150n |
| [Pr.33] JOG operation deceleration time selection | 1: [Pr.28] Deceleration time 1 | 1 | 0 | 51+150n |
| [Pr.33] JOG operation deceleration time selection | 2: [Pr.29] Deceleration time 2 | 2 | 0 | 51+150n |
| [Pr.33] JOG operation deceleration time selection | 3: [Pr.30] Deceleration time 3 | 3 | 0 | 51+150n |
| [Pr.34] Acceleration/deceleration process selection | 0: Trapezoid acceleration/deceleration process | 0 | 0 | 52+150n |
| [Pr.34] Acceleration/deceleration process selection | 1: S-curve acceleration/deceleration process | 1 | 0 | 52+150n |
| [Pr.35] S-curve ratio | 1 to 100 (%) | 1 to 100 (%) | 100 | 53+150n |
| [Pr.36] Sudden stop deceleration time | 1 to 8388608 (ms) | 1 to 8388608 (ms) | 1000 | 54+150n<br>55+150n |
| [Pr.37] Stop group 1 sudden stop selection | 0: Normal deceleration stop | 0 | 0 | 56+150n |
| [Pr.37] Stop group 1 sudden stop selection | 1: Rapid stop | 1 | 0 | 56+150n |
| [Pr.38] Stop group 2 sudden stop selection | 0: Normal deceleration stop | 0 | 0 | 57+150n |
| [Pr.38] Stop group 2 sudden stop selection | 1: Rapid stop | 1 | 0 | 57+150n |
| [Pr.39] Stop group 3 sudden stop selection | 0: Normal deceleration stop | 0 | 0 | 58+150n |
| [Pr.39] Stop group 3 sudden stop selection | 1: Rapid stop | 1 | 0 | 58+150n |
| [Pr.40] Positioning complete signal output time | 0 to 65535 (ms) | 0 to 65535 (ms)<br>0 to 32767: Set as a decimal<br>32768 to 65535: Convert into hexadecimal and set | 300 | 59+150n |
| [Pr.41] Allowable circular interpolation error width | The setting value range differs depending on the "[Pr.1] Unit setting". | The setting value range differs depending on the "[Pr.1] Unit setting". | 100 | 60+150n<br>61+150n |
| [Pr.42] External command function selection | 0: External positioning start | 0 | 0 | 62+150n |
| [Pr.42] External command function selection | 1: External speed change request | 1 | 0 | 62+150n |
| [Pr.42] External command function selection | 2: Speed-position, position-speed switching request | 2 | 0 | 62+150n |
| [Pr.42] External command function selection | 3: Skip request | 3 | 0 | 62+150n |
| [Pr.42] External command function selection | 4: High speed input request | 4 | 0 | 62+150n |
| [Pr.83] Speed control 10 times multiplier setting for degree axis | 0: Invalid | 0 | 0 | 63+150n |
| [Pr.83] Speed control 10 times multiplier setting for degree axis | 1: Valid | 1 | 0 | 63+150n |
| [Pr.84] Restart allowable range when servo OFF to ON | 0, 1 to 327680 [pulse]<br>0: restart not allowed | 0, 1 to 327680 [pulse]<br>0: restart not allowed | 0 | 64+150n<br>65+150n |
| [Pr.90] Operation setting for speed-torque control mode | b0 to b3: Not used | (bit image, see figure below) | 0000H | 68+150n |
| [Pr.90] Operation setting for speed-torque control mode | b4 to b7: Torque initial value selection<br>0: Command torque<br>1: Feedback torque | (bit image, see figure below) | 0000H | 68+150n |
| [Pr.90] Operation setting for speed-torque control mode | b8 to b11: Speed initial value selection<br>0: Command speed<br>1: Feedback speed<br>2: Automatic selection | (bit image, see figure below) | 0000H | 68+150n |
| [Pr.90] Operation setting for speed-torque control mode | b12 to b15: Condition selection at mode switching<br>[FX5-SSC-S]<br>0: Switching conditions valid at mode switching<br>1: ON conditions invalid during zero speed at mode switching<br>[FX5-SSC-G]<br>0: Check the switching condition on the Motion module<br>1: Follow the specifications of the servo amplifier | (bit image, see figure below) | 0000H | 68+150n |
| [Pr.95] External command signal selection | 0: Not used | 0 | 0 | 69+150n |
| [Pr.95] External command signal selection | 1 to 4: DI1 to DI4 [FX5-SSC-S] | 1 to 4 | 0 | 69+150n |
| [Pr.95] External command signal selection | 101 to 108: DOG signal of Axis 1 to Axis 8 [FX5-SSC-G] | 101 to 108 | 0 | 69+150n |
| [Pr.112] Servo OFF command valid/invalid setting [FX5-SSC-G] | b0: 0: Servo OFF Command Invalid<br>1: Servo OFF Command in Speed/Torque Control Valid | (bit image, see figure below) | 0000H | 112+150n |
| [Pr.112] Servo OFF command valid/invalid setting [FX5-SSC-G] | b1 to b15: Not used | (bit image, see figure below) | 0000H | 112+150n |
| [Pr.122] Manual pulse generator speed limit mode [FX5-SSC-G] | 0: Do not execute speed limit | 0 | 0 | 121+150n |
| [Pr.122] Manual pulse generator speed limit mode [FX5-SSC-G] | 1: Do not output the exceeding speed limit value | 1 | 0 | 121+150n |
| [Pr.122] Manual pulse generator speed limit mode [FX5-SSC-G] | 2: Output the exceeding speed limit value delay | 2 | 0 | 121+150n |
| [Pr.123] Manual pulse generator speed limit value [FX5-SSC-G] | The setting range differs depending on the "[Pr.1] Unit setting". | The setting range differs depending on the "[Pr.1] Unit setting". | 20000 | 122+150n<br>123+150n |
| [Pr.127] Speed limit value input selection at control mode switching | 1: Input disable | 1 | 0 | 125+150n |
| [Pr.127] Speed limit value input selection at control mode switching | Other than 1: Input enable | Other than 1 | 0 | 125+150n |

*In the original, "Setting value, setting range" is a 2-level header; the table continues from p.472 to p.473 ([Pr.83] to [Pr.127] on p.473). The setting-value cells and the Default value "1000" are merged over [Pr.25] to [Pr.30]. The Default value "0" is merged over [Pr.37] to [Pr.39]. For [Pr.31], [Pr.41], [Pr.84] and [Pr.123], one cell spans both setting-value columns. Item, Default value and Buffer memory address cells are merged over the setting-value rows of each parameter. For [Pr.90] and [Pr.112], the engineering-tool column is split into a bit column and a description column, and the "Value set with a program" column shows a bit image. Expanded to each row/column.

[Figure] [Pr.90] bit image (original p.473)
- A 16-bit word divided into 4-bit groups: b15 to b12 / b11 to b8 / b7 to b4 / b3 to b0
- A leader from the b3 to b0 group points to "Always "0" is set to the part not used."

[Figure] [Pr.112] bit image (original p.473)
- A 16-bit word b15 to b0; an arrow bracket spanning b15 to b1 points to "Always "0" is set to the part not used."

#### [Pr.25] Acceleration time 1 to [Pr.27] Acceleration time 3 ([Pr.25]加速時間1～[Pr.27]加速時間3) (11.3 / original p.473)

These parameters set the time for the speed to increase from zero to the "[Pr.8] Speed limit value" ("[Pr.31] JOG speed limit value" at JOG operation control) during a positioning operation.

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.473)

Refer to the following for the buffer memory address in this area.
→Page 424 Positioning parameters: Detailed parameters 2

#### [Pr.28] Deceleration time 1 to [Pr.30] Deceleration time 3 ([Pr.28]減速時間1～[Pr.30]減速時間3) (11.3 / original p.474)

These parameters set the time for the speed to decrease from the "[Pr.8] Speed limit value" ("[Pr.31] JOG speed limit value" at JOG operation control) to zero during a positioning operation.

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.474)

Refer to the following for the buffer memory address in this area.
→Page 424 Positioning parameters: Detailed parameters 2

#### [Pr.31] JOG speed limit value ([Pr.31]JOG速度制限値) (11.3 / original p.474)

Set the maximum speed for JOG operation.

| [Pr.1] setting value | Value set with the engineering tool (unit) | Value set with a program (unit) |
|---|---|---|
| 0: mm | 0.01 to 20000000.00 (mm/min) | 1 to 2000000000 (× 10^-2 mm/min) |
| 1: inch | 0.001 to 2000000.000 (inch/min) | 1 to 2000000000 (× 10^-3 inch/min) |
| 2: degree | 0.001 to 2000000.000 (degree/min)*1 | 1 to 2000000000 (× 10^-3 degree/min)*2 |
| 3: pulse | 1 to 1000000000 (pulse/s) | 1 to 1000000000 (pulse/s) |

*1 The range of JOG speed limit value when "[Pr.83] Speed control 10 × multiplier setting for degree axis" is valid: 0.01 to 20000000.00 (degree/min)
*2 The range of JOG speed limit value when "[Pr.83] Speed control 10 × multiplier setting for degree axis" is valid: 1 to 2000000000 (× 10^-2 degree/min)

> **Point**
> Set the "JOG speed limit value" to a value less than "[Pr.8] Speed limit value". If the "speed limit value" is exceeded, the error "JOG speed limit value error" (error code: 1AB7H [FX5-SSC-S], or error codes: 1BB7H and 1BB8H [FX5-SSC-G]) will occur.

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.474)

Refer to the following for the buffer memory address in this area.
→Page 424 Positioning parameters: Detailed parameters 2

#### [Pr.32] JOG operation acceleration time selection ([Pr.32]JOG運転加速時間選択) (11.3 / original p.474)

Set which of "acceleration time 0 to 3" to use for the acceleration time during JOG operation.
0: Use value set in "[Pr.9] Acceleration time 0".
1: Use value set in "[Pr.25] Acceleration time 1".
2: Use value set in "[Pr.26] Acceleration time 2".
3: Use value set in "[Pr.27] Acceleration time 3".

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.474)

Refer to the following for the buffer memory address in this area.
→Page 424 Positioning parameters: Detailed parameters 2

#### [Pr.33] JOG operation deceleration time selection ([Pr.33]JOG運転減速時間選択) (11.3 / original p.474)

Set which of "deceleration time 0 to 3" to use for the deceleration time during JOG operation.
0: Use value set in "[Pr.10] Deceleration time 0".
1: Use value set in "[Pr.28] Deceleration time 1".
2: Use value set in "[Pr.29] Deceleration time 2".
3: Use value set in "[Pr.30] Deceleration time 3".

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.474)

Refer to the following for the buffer memory address in this area.
→Page 424 Positioning parameters: Detailed parameters 2

#### [Pr.34] Acceleration/deceleration process selection ([Pr.34]加減速処理選択) (11.3 / original p.475)

Set whether to use trapezoid acceleration/deceleration or S-curve acceleration/deceleration for the acceleration/deceleration process.
Refer to the following for details.
→Page 304 Acceleration/deceleration processing function

[Figure] Acceleration/deceleration process (original p.475)
- <Trapezoid acceleration/deceleration>: Velocity/Time — "The acceleration and deceleration are linear."
- <S-curve acceleration/deceleration>: Velocity/Time — "The acceleration and deceleration follow a Sin curve."

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.475)

Refer to the following for the buffer memory address in this area.
→Page 424 Positioning parameters: Detailed parameters 2

#### [Pr.35] S-curve ratio ([Pr.35]S字比率) (11.3 / original p.475)

Set the S-curve ratio (1 to 100%) for carrying out the S-curve acceleration/deceleration process.
The S-curve ratio indicates where to draw the acceleration/deceleration curve using the Sin curve as shown below.

[Figure] S-curve ratio (original p.475)
- A Sin curve section of width A; the portion actually used has width B, centered (B/2 on each side of the center)
- "S-curve ratio = B/A × 100%"
- (Example) When S-curve ratio is 100%: the speed rises to the positioning speed along the whole Sin curve (half period)
- (Example) When S-curve ratio is 70%: b/a = 0.7 — only the central 70% of the Sin curve is used (the curve portion b within the full range a), the remainder is linear

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.475)

Refer to the following for the buffer memory address in this area.
→Page 424 Positioning parameters: Detailed parameters 2

#### [Pr.36] Sudden stop deceleration time ([Pr.36]急停止減速時間) (11.3 / original p.476)

Set the time to reach speed 0 from "[Pr.8] Speed limit value" ("[Pr.31] JOG speed limit value" at JOG operation control) during the rapid stop. The illustration below shows the relationships with other parameters.

[Figure] Relationship between sudden stop deceleration time and other parameters (original p.476)
- Levels: [Pr.8] Speed limit value, [Da.8] Command speed
- 1) Positioning start: When positioning is started, the acceleration starts following the "acceleration time". (Acceleration time = [Pr.9] Acceleration time 0 / [Pr.25] Acceleration time 1 / [Pr.26] Acceleration time 2 / [Pr.27] Acceleration time 3, defined from 0 to [Pr.8]; "Actual acceleration time" = 0 to [Da.8])
- 2) Rapid stop cause occurrence: When a "rapid stop cause" occurs, the deceleration starts following the "rapid stop deceleration time". ([Pr.36] Sudden stop deceleration time is defined from [Pr.8] to 0; "Actual rapid stop deceleration time" is from [Da.8] to 0 and is shorter)
- 3) Positioning stop: When a "rapid stop cause" does not occur, the deceleration starts toward the stop position following the "deceleration time". (Deceleration time = [Pr.10] Deceleration time 0 / [Pr.28] Deceleration time 1 / [Pr.29] Deceleration time 2 / [Pr.30] Deceleration time 3, defined from [Pr.8] to 0; "Actual deceleration time" = [Da.8] to 0)

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.476)

Refer to the following for the buffer memory address in this area.
→Page 424 Positioning parameters: Detailed parameters 2

#### [Pr.37] to [Pr.39] Stop group 1/2/3 sudden stop selection ([Pr.37]～[Pr.39]停止グループ1～3急停止選択) (11.3 / original p.476)

Set the method to stop when the stop causes in the following stop groups occur.

| Stop group | Details |
|---|---|
| Stop group 1 | Stop with hardware stroke limit |
| Stop group 2 | Error occurrence of the CPU module, "[Cd.190] PLC READY" OFF |
| Stop group 3 | Axis stop signal from the CPU module, Error occurrence (excludes errors in stop groups 1 and 2: includes only the software stroke limit errors during JOG operation, speed control, speed-position switching control, and position-speed switching control) |

The methods of stopping include "0: Normal deceleration stop" and "1: Rapid stop".
If "1: Rapid stop" is selected, the axis will rapidly decelerate to a stop when the stop cause occurs.

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.476)

Refer to the following for the buffer memory address in this area.
→Page 424 Positioning parameters: Detailed parameters 2

#### [Pr.40] Positioning complete signal output time ([Pr.40]位置決め完了信号出力時間) (11.3 / original p.477)

Set the output time of the positioning complete signal output from the Simple Motion module/Motion module.
A positioning completes when the specified dwell time has passed after the Simple Motion module/Motion module had terminated the command output.
For the interpolation control, the positioning completed signal of interpolation axis is output only during the time set to the reference axis.

##### ■Operation example (動作例) (11.3 / original p.477)

[Figure] Positioning complete signal output time (original p.477)
- Block diagram: CPU module → "Positioning start ([Cd.184])" → Simple Motion module/Motion module → motor (M) → ball screw "Positioning"; Simple Motion module/Motion module → "Positioning complete signal ([Md.31] Status: b15)" → CPU module
- Timing: [Cd.184] Positioning start ON → Start complete signal ([Md.31] Status: b14) ON and [Md.141] BUSY ON → [Cd.184] OFF → b14 OFF
- When positioning ends, [Md.141] BUSY turns OFF and the positioning complete signal ([Md.31] Status: b15) turns ON ("Positioning complete signal (after dwell time has passed)") for the "Output time", then OFF

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.477)

Refer to the following for the buffer memory address in this area.
→Page 424 Positioning parameters: Detailed parameters 2

#### [Pr.41] Allowable circular interpolation error width ([Pr.41]円弧補間誤差許容範囲) (11.3 / original p.478)

The allowable error range of the calculated arc path and end point address is set.*1
If the error of the calculated arc path and end point address is within the set range, circular interpolation will be carried out to the set end point address while compensating the error with spiral interpolation.
The allowable circular interpolation error width is set in the following axis buffer memory addresses.

Ex.
· If axis 1 is the reference axis, set in the axis 1 buffer memory addresses [60, 61].
· If axis 4 is the reference axis, set in the axis 4 buffer memory addresses [510, 511].

[Figure] Allowable circular interpolation error width (original p.478)
- Labels: Start point address, Center point address, End point address with calculation, End point address, Error, Path with spiral interpolation
- The calculated arc (from the start point around the center point) ends at the "End point address with calculation"; the difference to the set "End point address" is the "Error"; the actual path is a "Path with spiral interpolation" (dashed) that gradually shifts to reach the set end point address

*1 In 2-axis circular interpolation control with the center point designation, the arc path calculated with the start point address and center point address and the end point address may deviate.

| [Pr.1] setting value | Value set with the engineering tool (unit) | Value set with a program (unit) |
|---|---|---|
| 0: mm | 0 to 10000.0 (μm) | 0 to 100000 (× 10^-1 μm) |
| 1: inch | 0 to 1.00000 (inch) | 0 to 100000 (× 10^-5 inch) |
| 2: degree | 0 to 1.00000 (degree) | 0 to 100000 (× 10^-5 degree) |
| 3: pulse | 0 to 100000 (pulse) | 0 to 100000 (pulse) |

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.478)

Refer to the following for the buffer memory address in this area.
→Page 424 Positioning parameters: Detailed parameters 2

#### [Pr.42] External command function selection ([Pr.42]外部指令機能選択) (11.3 / original p.478)

Select a command with which the external command signal should be associated.

| Setting value | Details |
|---|---|
| 0: External positioning start | The external command signal input is used to start a positioning operation. |
| 1: External speed change request | The external command signal input is used to change the speed in the current positioning operation.<br>The new speed should be set in the "[Cd.14] New speed value". |
| 2: Speed-position, position-speed switching request | The external command signal input is used to switch from the speed control to the position control while in the speed-position switching control mode, or from the position control to the speed control while in the position-speed switching control mode.<br>To enable the speed-position switching control, set the "[Cd.24] Speed-position switching enable flag" to "1". To enable the position-speed switching control, set the "[Cd.26] Position-speed switching enable flag" to "1". |
| 3: Skip request | The external command signal input is used skip the current positioning operation. |
| 4: High speed input request | The external command signal input is used to execute the mark detection. And, also set to use the external command signal in the synchronous control. |

*(Note: "is used skip" (missing "to") is as printed in the original.)*

> **Point**
> To enable the external command signal, set the "[Cd.8] External command valid" to "1".

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.478)

Refer to the following for the buffer memory address in this area.
→Page 424 Positioning parameters: Detailed parameters 2

#### [Pr.83] Speed control 10 times multiplier setting for degree axis ([Pr.83]degree軸速度10倍指定) (11.3 / original p.479)

Set the speed control 10 × multiplier setting for degree axis when you use command speed and speed limit value set by the positioning data and the parameter at "[Pr.1] Unit setting" setup degree by ten times at the speed.
0: Invalid
1: Valid
Normally, the speed specification range is 0.001 to 2000000.000 [degree/min], but it will be decupled and become 0.01 to 20000000.00 [degree/min] by setting "[Pr.83] Speed control 10 × multiplier setting for degree axis" to valid.
Refer to the following for details on the speed control 10 × multiplier setting for degree axis.
→Page 309 Speed control 10 times multiplier setting for degree axis function

| [Pr.83] setting value | Value set with the engineering tool (unit) | Value set with a program (unit) |
|---|---|---|
| 0: Invalid | 0.001 to 2000000.000 (degree/min) | 1 to 2000000000 (× 10^-3 degree/min) |
| 1: Valid | 0.01 to 20000000.00 (degree/min) | 1 to 2000000000 (× 10^-2 degree/min) |

> **Point**
> The "Speed control 10 × multiplier setting for degree axis" is included in detailed parameters 2. However, it will be valid at the leading edge (OFF to ON) of the "[Cd.190] PLC READY".

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.479)

Refer to the following for the buffer memory address in this area.
→Page 424 Positioning parameters: Detailed parameters 2

#### [Pr.84] Restart allowable range when servo OFF to ON ([Pr.84]サーボOFF→ON時の再始動許容値範囲設定) (11.3 / original p.480-481)

##### ■Restart function at switching servo OFF to ON (サーボOFF→ON時の再始動機能とは) (11.3 / original p.480)

The restart function at switching servo OFF to ON performs continuous positioning operation (positioning start, restart) when switching servo OFF to ON while the Simple Motion module/Motion module is stopped (including forced stop, servo forced stop).
Restart at switching servo OFF to ON can be performed when the difference between the last command position of Simple Motion module/Motion module at stop and the current value at switching servo OFF to ON is equal to or less than the value set in the buffer memory for the restart allowable range setting.

- Servo emergency stop processing
  - When the difference between the last command position of Simple Motion module/Motion module at the forced stop input or the servo forced stop input and the current value at the forced stop release or the servo forced stop release is equal to or less than the value set in the buffer memory for the restart allowable range setting, the positioning operation is judged as stopped and can be restarted.
  - When the difference between the last command position of Simple Motion module/Motion module at the forced stop input or the servo forced stop input and the current value at the forced stop release or the servo forced stop release is greater than the value set in the buffer memory for the restart allowable range setting, the positioning operation is judged as on-standby and cannot be restarted.

[Figure] Servo emergency stop processing (original p.480)
- Forced stop: Release → Input → Release
- Axis operation status: Operation → Servo OFF (at forced stop input; "Last command position" is taken here) → Stop/Wait (at forced stop release; "Servo ON")
- From Stop/Wait: "Restart valid" (stop) or "Restart invalid" (wait), depending on the difference

- Processing at switching the servo ON signal from OFF to ON
  - When the difference between the last command position of Simple Motion module/Motion module at switching the servo ON signal from ON to OFF and the current value at switching the servo ON signal from OFF to ON is equal to or less than the value set in the buffer memory for the restart allowable range setting, the positioning operation is judged as stopped and can be restarted.
  - When the difference between the last command position of Simple Motion module/Motion module at switching the servo ON signal from ON to OFF and the current value at switching the servo ON signal from OFF to ON is greater than the value set in the buffer memory for the restart allowable range setting, the positioning operation is judged as on-standby and cannot be restarted.

[Figure] Processing at switching the servo ON signal from OFF to ON (original p.480)
- Servo ON signal ([Md.108] Servo status1: b1): ON → OFF → ON
- Axis operation status: Positioning → Stop ("Stop command") → Servo OFF (servo ON signal OFF) → Stop/Wait ("Servo ON")
- From Stop/Wait: "Restart valid" or "Restart invalid"

##### ■Setting method (設定方法) (11.3 / original p.481)

For performing restart at switching servo OFF to ON, set the restart allowable range in the following buffer memory.
n: Axis No. - 1

| Item | Setting range | Default value | Buffer memory address |
|---|---|---|---|
| [Pr.84] Restart allowable range when servo OFF to ON | 0, 1 to 327680 [pulse]<br>0: restart not allowed | 0 | 64+150n<br>65+150n |

- Setting example
A program to set the restart allowable range for axis 1 to 10000 pulses is shown below.

```
LD    (unreadable)       ; execution condition (a-contact; no device name is printed in the original figure, see original p.481)
DMOVP K10000 D0          ; Restart allowable range (10000 pulses) is stored in D0, D1.
DTOP  H0 K64 D0 K1       ; Data for D0, D1 is stored in buffer memory 64, 65 of the Simple Motion module/Motion module.
```

> **Point**
> - The difference between the last command position at servo OFF and the current value at servo ON is output at once at the first restart. If the restart allowable range is large at this time, an overload may occur on the servo side. Set a value which does not affect the mechanical system by output once to the restart allowable range when switching servo OFF to ON.
> - The restart at switching servo OFF to ON is valid only at switching servo OFF to ON at the first time. At the second time or later, the setting for restart allowable range when switching servo OFF to ON is disregarded.
> - Execute servo OFF when the mechanical system is in complete stop state. The restart at switching servo OFF to ON cannot be applied to a system in which the mechanical system is operated by external pressure or other force during servo OFF.
> - Restart can be executed only while the axis operation status is "stop". Restart cannot be executed when the axis operation status is other than "stop".
> - When the "[Cd.190] PLC READY" is switched from OFF to ON during servo OFF, restart cannot be executed. If restart is requested, the warning "Restart not possible" (warning code: 0902H [FX5-SSC-S], or warning code: 0D02H [FX5-SSC-G]) occurs.
> - Do not restart while a stop command is ON. When restart is executed during a stop, the error "Stop signal ON at start" (error code: 1908H [FX5-SSC-S], or error code: 1A08H [FX5-SSC-G]) occurs and the axis operation status becomes "ERR". Therefore, restart cannot be performed even if the error is reset.
> - Restart can also be executed while the positioning start signal is ON. However, do not set the positioning start signal from OFF to ON during a stop. If the positioning start signal is switched from OFF to ON, positioning is performed from the positioning data No. set in "[Cd.3] Positioning start No." or from the positioning data No. of the specified point.
> - When positioning is terminated by a continuous-operation interrupt request, restart cannot be performed. If a restart request is executed, the warning "Restart not possible" (warning code: 0902H [FX5-SSC-S], or warning code: 0D02H [FX5-SSC-G]) occurs.
>
> [Figure] [Operation at emergency stop input] / [Operation at restart] (original p.481)
> - At emergency stop input: "Emergency stop input (Last command position)"; the axis coasts ("Movement during servo OFF") to the "Stop position at servo OFF"
> - At restart: "Output at once at restart" of the difference between the "Last command position" and the "(Current value at servo ON) Stop position at servo OFF", then "Restart operation" continues

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.481)

Refer to the following for the buffer memory address in this area.
→Page 424 Positioning parameters: Detailed parameters 2

#### [Pr.90] Operation setting for speed-torque control mode ([Pr.90]速度・トルク制御モード動作設定) (11.3 / original p.482)

Operation setting of the speed control mode, torque control mode or continuous operation to torque control mode at the speed-torque control is executed.

##### ■Torque initial value selection (トルク初期値選択) (11.3 / original p.482)

Set the torque initial value at switching to torque control mode or to continuous operation to torque control mode.

| Setting value | Details |
|---|---|
| 0: Command torque | Command torque value at switching. (following axis control data)<br>Switching to torque control mode: "[Cd.143] Command torque at torque control mode"<br>Switching to continuous operation to torque control mode: "[Cd.150] Target torque at continuous operation to torque control mode" |
| 1: Feedback torque | Motor torque value at switching. |

##### ■Speed initial value selection (速度初期値選択) (11.3 / original p.482)

Set the initial speed at switching from position control mode to speed control mode or the initial speed at switching from position control mode or from speed control mode to continuous operation to torque control mode.

| Setting value | Details |
|---|---|
| 0: Command speed | Speed that position command at switching is converted into the motor rotation speed. |
| 1: Feedback speed | Motor rotation speed received from servo amplifier at switching |
| 2: Automatic selection | The lower speed between speed that position command at switching is converted into the motor rotation speed and motor rotation speed received from servo amplifier at switching. (This setting is valid only when continuous operation to torque control mode is used. At switching from position control mode to speed control mode, operation is the same as "0: Command speed".) |

##### ■Condition selection at mode switching (モード切換え時条件選択) (11.3 / original p.482)

Set the valid/invalid of switching conditions for switching control mode.
[FX5-SSC-S]
0: Switching conditions valid at mode switching
1: ON conditions invalid during zero speed at mode switching
[FX5-SSC-G]
0: Check the switching conditions on the Motion module
1: Follow the specifications of the servo amplifier

> **Point**
> - The "Operation setting for speed-torque control mode" is included in detailed parameters 2. However, it will be valid at the leading edge (OFF to ON) of the "[Cd.190] PLC READY".
> - Set the following settings to switch the control mode without waiting for the servo motor to stop. Note that it may cause vibration or impact at control switching.
>   [FX5-SSC-S]
>   Set "Condition selection at mode switching (b12 to b15)" to "1: ON conditions invalid during zero speed at mode switching".
>   [FX5-SSC-G]
>   Set "Condition selection at mode switching (b12 to b15)" to "1: Follow the specifications of the servo amplifier". When using MR-J5(W)-G, set "ZSP disabled selection at control switching" in servo parameter "Function selection C-E(PC76)" to "1: Disabled".

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.482)

Refer to the following for the buffer memory address in this area.
→Page 424 Positioning parameters: Detailed parameters 2

#### [Pr.95] External command signal selection ([Pr.95]外部指令信号選択) (11.3 / original p.483)

Set the external command signal.
DOG signal of the servo amplifier is used regardless of the values of "[Pr.118] DOG signal selection". [FX5-SSC-G]

##### ■FX5-SSC-S (FX5-SSC-S) (11.3 / original p.483)

| Setting value | Details |
|---|---|
| 0: Not used | External command signal is not used. |
| 1: DI1 | DI1 is used as external command signal. |
| ⋮ | ⋮ |
| 4: DI4 | DI4 is used as external command signal. |

*"⋮" is as printed in the original (2: DI2 and 3: DI3 are not listed individually in the original itself).

##### ■FX5-SSC-G (FX5-SSC-G) (11.3 / original p.483)

| Setting value | Details |
|---|---|
| 0: Not used | External command signal is not used. |
| 101: DOG signal of Axis 1 | DOG signal of Axis 1 is used as external command signal. |
| ⋮ | ⋮ |
| 108: DOG signal of Axis 8 | DOG signal of Axis 8 is used as external command signal. |

*"⋮" is as printed in the original (102 to 107 are not listed individually in the original itself).

The logic selection of the DOG signal assigned as the external command signal follows the setting of "[Pr.22] Input signal logic selection" "b4: External command/switching signal".

> **Point**
> - The "External command signal selection" is included in detailed parameters 2. However, it will be valid at the leading edge (OFF to ON) of the "[Cd.190] PLC READY".
> - Same external command signal can be used in the multiple axes.

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.483)

Refer to the following for the buffer memory address in this area.
→Page 424 Positioning parameters: Detailed parameters 2

#### [Pr.112] Servo OFF command valid/invalid setting [FX5-SSC-G] ([Pr.112]サーボOFF指令有効／無効設定[FX5-SSC-G]) (11.3 / original p.483)

Set whether accept "[Cd.100] Servo OFF command" and "[Cd.191] All axis servo ON" or not during the speed control mode, torque control mode, or continuous operation to torque control mode of each axis. The setting value is reflected at the control mode switching. Only the setting of bit0 is enabled.
0: Servo OFF Command Invalid
1: Servo OFF Command in Speed/Torque Control Valid

> **Point**
> When the value is "1" other than bit0, the setting is ignored and as the same behavior occurs as when the bit0 is set to "0: Servo OFF Command Invalid".

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.483)

Refer to the following for the buffer memory address in this area.
→Page 424 Positioning parameters: Detailed parameters 2

#### [Pr.122] Manual pulse generator speed limit mode [FX5-SSC-G] ([Pr.122]手動パルサ速度制限モード[FX5-SSC-G]) (11.3 / original p.484)

Set how to output when the output by manual pulse generator operation exceeds "[Pr.123] Manual pulse generator speed limit value".
0: Do not execute speed limit
1: Do not output the exceeding speed limit value
2: Output the exceeding speed limit value delay

> **Point**
> The "Manual pulse generator speed limit mode" is included in detailed parameters 2. However, it will be valid at the leading edge (OFF→ON) of "[Cd.190] PLC READY".

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.484)

Refer to the following for the buffer memory address in this area.
→Page 424 Positioning parameters: Detailed parameters 2

#### [Pr.123] Manual pulse generator speed limit value [FX5-SSC-G] ([Pr.123]手動パルサ速度制限値[FX5-SSC-G]) (11.3 / original p.484)

Set the maximum speed during manual pulse generator operation.

> **Point**
> - The "Manual pulse generator speed limit value" is included in detailed parameters 2. However, it will be valid at the leading edge (OFF→ON) of "[Cd.190] PLC READY".
> - Set the "Manual pulse generator speed limit value" to a value less than "[Pr.8] Speed limit value". If the "speed limit value" is exceeded, the error "Manual pulse generator speed limit value error" (error codes: 1BB7H and 1BB8H) will occur.

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.484)

Refer to the following for the buffer memory address in this area.
→Page 424 Positioning parameters: Detailed parameters 2

#### [Pr.127] Speed limit value input selection at control mode switching ([Pr.127]制御モード切換え時速度制限値取込み選択) (11.3 / original p.484)

Set whether to input the value of the "[Pr.8] Speed limit value" at speed-torque control mode switching.

> **Point**
> The "Speed limit value input selection at control mode switching" is included in detailed parameters 2. However, it will be valid at the leading edge (OFF to ON) of the "[Cd.190] PLC READY".

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.484)

Refer to the following for the buffer memory address in this area.
→Page 424 Positioning parameters: Detailed parameters 2

### Home position return basic parameters (原点復帰基本パラメータ) (11.3 / original p.485-488)

n: Axis No. - 1

| Item | | Value set with the engineering tool | Value set with a program | Default value | Buffer memory address |
|---|---|---|---|---|---|
| [Pr.43] | Home position return method | 0: Proximity dog method [FX5-SSC-S] | 0 | 0 [FX5-SSC-S]<br>8 [FX5-SSC-G] | 70+150n |
| [Pr.43] | Home position return method | 4: Count method 1 [FX5-SSC-S] | 4 | 0 [FX5-SSC-S]<br>8 [FX5-SSC-G] | 70+150n |
| [Pr.43] | Home position return method | 5: Count method 2 [FX5-SSC-S] | 5 | 0 [FX5-SSC-S]<br>8 [FX5-SSC-G] | 70+150n |
| [Pr.43] | Home position return method | 6: Data set method [FX5-SSC-S] | 6 | 0 [FX5-SSC-S]<br>8 [FX5-SSC-G] | 70+150n |
| [Pr.43] | Home position return method | 7: Scale origin signal detection method [FX5-SSC-S] | 7 | 0 [FX5-SSC-S]<br>8 [FX5-SSC-G] | 70+150n |
| [Pr.43] | Home position return method | 8: Driver home position return method | 8 | 0 [FX5-SSC-S]<br>8 [FX5-SSC-G] | 70+150n |
| [Pr.44] | Home position return direction | 0: Positive direction (address increment direction) | 0 | 0 | 71+150n |
| [Pr.44] | Home position return direction | 1: Negative direction (address decrement direction) | 1 | 0 | 71+150n |
| [Pr.45] | Home position address | The setting value range differs depending on the "[Pr.1] Unit setting". | The setting value range differs depending on the "[Pr.1] Unit setting". | 0 | 72+150n<br>73+150n |
| [Pr.46] | Home position return speed | The setting value range differs depending on the "[Pr.1] Unit setting". | The setting value range differs depending on the "[Pr.1] Unit setting". | 1 | 74+150n<br>75+150n |
| [Pr.47] | Creep speed [FX5-SSC-S] | The setting value range differs depending on the "[Pr.1] Unit setting". | The setting value range differs depending on the "[Pr.1] Unit setting". | 1 | 76+150n<br>77+150n |
| [Pr.48] | Home position return retry [FX5-SSC-S] | 0: Do not retry home position return with limit switch | 0 | 0 | 78+150n |
| [Pr.48] | Home position return retry [FX5-SSC-S] | 1: Retry home position return with limit switch | 1 | 0 | 78+150n |

*In the original, the header "Setting value, setting range" spans the two columns "Value set with the engineering tool" / "Value set with a program". The Item, Default value and Buffer memory address cells are merged over the rows of each parameter ([Pr.43] 6 rows, [Pr.44] 2 rows, [Pr.48] 2 rows). The text "The setting value range differs depending on the "[Pr.1] Unit setting"." is one cell merged over both setting columns and over the 3 rows [Pr.45] to [Pr.47]. Expanded to each row.

#### [Pr.43] Home position return method (原点復帰方式) (11.3 / original p.485)

Set the "home position return method" for carrying out machine home position return.

| Setting value | Details | Reference |
|---|---|---|
| 0: Proximity dog method [FX5-SSC-S] | After decelerating at the proximity dog ON, stop at the zero signal and complete the machine home position return. | →Page 42 Proximity dog method [FX5-SSC-S] |
| 4: Count method 1 [FX5-SSC-S] | After decelerating at the proximity dog ON, move the designated distance, and complete the machine home position return with the zero signal. | →Page 44 Count method1 [FX5-SSC-S] |
| 5: Count method 2 [FX5-SSC-S] | After decelerating at the proximity dog ON, move the designated distance, and complete the machine home position return. | →Page 46 Count method2 [FX5-SSC-S] |
| 6: Data set method [FX5-SSC-S] | The position where the machine home position return has been made will be the home position. | →Page 48 Data set method [FX5-SSC-S] |
| 7: Scale origin signal detection method [FX5-SSC-S] | After deceleration stop at the proximity dog ON, move to the opposite direction against the home position return direction, and move to the home position return direction after deceleration stop once at the detection of the first zero signal. Then, it stops at the detected nearest zero signal, and completes the machine home position return. | →Page 49 Scale origin signal detection method [FX5-SSC-S] |
| 8: Driver home position return method | Carry out the home position return operation on the driver side. The home position return operation and parameters depend on the specifications of the driver. | [FX5-SSC-S]<br>→Page 829 AlphaStep/5-phase stepping motor driver manufactured by ORIENTAL MOTOR Co., Ltd.<br>→Page 840 IAI electric actuator controller manufactured by IAI Corporation<br>[FX5-SSC-G]<br>→Page 52 Driver home position return method |

When setting the home position return method that cannot be executed, the error "Home position return method invalid" (error code: 1979H [FX5-SSC-S], or error code: 1A79H [FX5-SSC-G]) occurs and the home position return is not executed.

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.485)

Refer to the following for the buffer memory address in this area.
→Page 424 Home position return parameters: Home position return basic parameters

#### [Pr.44] Home position return direction (原点復帰方向) (11.3 / original p.486)

Set the direction to start movement when starting machine home position return.

| Setting value | Details |
|---|---|
| 0: Positive direction (address increment direction) | Moves in the direction that the address increments. (Arrow 2)) |
| 1: Negative direction (address decrement direction) | Moves in the direction that the address decrements. (Arrow 1)) |

Normally, the home position is set near the lower limit or the upper limit, so "[Pr.44] Home position return direction" is set as shown below.

[Figure] Setting of [Pr.44] according to the home position location (original p.486)
- Axis drawn from "Address decrement direction" (left) to "Address increment direction" (right), with Lower limit on the left and Upper limit on the right.
- Upper drawing: Home position near the Lower limit; arrow 1) points toward the lower limit (address decrement direction). Callout: "When the zero point is set at the lower limit side, the home position return direction is in the direction of arrow 1). Set "1" for [Pr.44]."
- Lower drawing: Home position near the Upper limit; arrow 2) points toward the upper limit (address increment direction). Callout: "When the home position is set at the upper limit side, the home position return direction is in the direction of arrow 2). Set "0" for [Pr.44]."

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.486)

Refer to the following for the buffer memory address in this area.
→Page 424 Home position return parameters: Home position return basic parameters

#### [Pr.45] Home position address (原点アドレス) (11.3 / original p.486)

Set the address used as the reference point for positioning control (ABS system).
(When the machine home position return is completed, the stop position address is changed to the address set in "[Pr.45] Home position address". At the same time, the "[Pr.45] Home position address" is stored in "[Md.20] Command position value" and "[Md.21] Machine feed value".)

| [Pr.1] setting value | Value set with the engineering tool (unit) | Value set with a program (unit) |
|---|---|---|
| 0: mm | -214748364.8 to 214748364.7 (μm) | -2147483648 to 2147483647 (×10^-1 μm) |
| 1: inch | -21474.83648 to 21474.83647 (inch) | -2147483648 to 2147483647 (×10^-5 inch) |
| 2: degree | 0 to 359.99999 (degree) | 0 to 35999999 (×10^-5 degree) |
| 3: pulse | -2147483648 to 2147483647 (pulse) | -2147483648 to 2147483647 (pulse) |

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.486)

Refer to the following for the buffer memory address in this area.
→Page 424 Home position return parameters: Home position return basic parameters

#### [Pr.46] Home position return speed (原点復帰速度) (11.3 / original p.487)

Set the speed for home position return.
Performs high-speed home position return with the home position return speed. [FX5-SSC-G]

| [Pr.1] setting value | Value set with the engineering tool (unit) | Value set with a program (unit) |
|---|---|---|
| 0: mm | 0.01 to 20000000.00 (mm/min) | 1 to 2000000000 (×10^-2 mm/min) |
| 1: inch | 0.001 to 2000000.000 (inch/min) | 1 to 2000000000 (×10^-3 inch/min) |
| 2: degree | 0.001 to 2000000.000 (degree/min)*1 | 1 to 2000000000 (×10^-3 degree/min)*2 |
| 3: pulse | 1 to 1000000000 (pulse/s) | 1 to 1000000000 (pulse/s) |

*1 The range of home position return speed when "[Pr.83] Speed control 10 × multiplier setting for degree axis" is valid: 0.01 to 20000000.00 (degree/min)
*2 The range of home position return speed when "[Pr.83] Speed control 10 × multiplier setting for degree axis" is valid: 1 to 2000000000 (×10^-2 degree/min)

> **Point**
> [FX5-SSC-S]
> Set the "home position return speed" to less than "[Pr.8] Speed limit value". If the "speed limit value" is exceeded, the error "Outside speed limit value range" (error code: 1A69H) will occur, and home position return will not be executed. The "home position return speed" should be equal to or faster than the "[Pr.7] Bias speed at start" and "[Pr.47] Creep speed".
> [FX5-SSC-G]
> Set the "home position return speed" to less than "[Pr.8] Speed limit value". If the "speed limit value" is exceeded, the error "Outside speed limit value range" (error code: 1B69H) will occur, and home position return will not be executed.

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.487)

Refer to the following for the buffer memory address in this area.
→Page 424 Home position return parameters: Home position return basic parameters

#### [Pr.47] Creep speed [FX5-SSC-S] (クリープ速度[FX5-SSC-S]) (11.3 / original p.488)

Set the creep speed after proximity dog ON (the low speed just before stopping after decelerating from the home position return speed). The creep speed is set within the following range.
([Pr.46] Home position return speed) ≥ ([Pr.47] Creep speed) ≥ ([Pr.7] Bias speed at start)

[Figure] Creep speed (original p.488)
- Speed (V) waveform: from "Machine home position return start" the axis accelerates to "[Pr.46] Home position return speed" and runs at constant speed.
- Proximity dog signal: OFF → ON. At proximity dog ON, the axis decelerates from the home position return speed to "[Pr.47] Creep speed" and runs at the creep speed.
- Proximity dog signal turns OFF while at creep speed; the axis stops at the first zero signal after the proximity dog OFF (zero signal pulses are drawn during creep; the stop coincides with a zero signal pulse after dog OFF).

| [Pr.1] setting value | Value set with the engineering tool (unit) | Value set with a program (unit) |
|---|---|---|
| 0: mm | 0.01 to 20000000.00 (mm/min) | 1 to 2000000000 (×10^-2 mm/min) |
| 1: inch | 0.001 to 2000000.000 (inch/min) | 1 to 2000000000 (×10^-3 inch/min) |
| 2: degree | 0.001 to 2000000.000 (degree/min)*1 | 1 to 2000000000 (×10^-3 degree/min)*2 |
| 3: pulse | 1 to 1000000000 (pulse/s) | 1 to 1000000000 (pulse/s) |

*1 The range of home position return speed when "[Pr.83] Speed control 10 × multiplier setting for degree axis" is valid: 0.01 to 20000000.00 (degree/min)
*2 The range of home position return speed when "[Pr.83] Speed control 10 × multiplier setting for degree axis" is valid: 1 to 2000000000 (×10^-2 degree/min)

*(Note: the footnotes under the creep speed table say "home position return speed" as printed in the original.)*

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.488)

Refer to the following for the buffer memory address in this area.
→Page 424 Home position return parameters: Home position return basic parameters

#### [Pr.48] Home position return retry [FX5-SSC-S] (原点復帰リトライ[FX5-SSC-S]) (11.3 / original p.488)

Set whether to carry out home position return retry.
Refer to the following for the operation of home position return retry.
→Page 220 Home position return retry function [FX5-SSC-S]

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.488)

Refer to the following for the buffer memory address in this area.
→Page 424 Home position return parameters: Home position return basic parameters

### Home position return detailed parameters (原点復帰詳細パラメータ) (11.3 / original p.489-493)

n: Axis No. - 1

| Item | | Value set with the engineering tool | Value set with a program | Default value | Buffer memory address |
|---|---|---|---|---|---|
| [Pr.50] | Setting for the movement amount after proximity dog ON [FX5-SSC-S] | The setting value range differs depending on the "[Pr.1] Unit setting". | The setting value range differs depending on the "[Pr.1] Unit setting". | 0 | 80+150n<br>81+150n |
| [Pr.51] | Home position return acceleration time selection | 0: [Pr.9] Acceleration time 0 | 0 | 0 | 82+150n |
| [Pr.51] | Home position return acceleration time selection | 1: [Pr.25] Acceleration time 1 | 1 | 0 | 82+150n |
| [Pr.51] | Home position return acceleration time selection | 2: [Pr.26] Acceleration time 2 | 2 | 0 | 82+150n |
| [Pr.51] | Home position return acceleration time selection | 3: [Pr.27] Acceleration time 3 | 3 | 0 | 82+150n |
| [Pr.52] | Home position return deceleration time selection | 0: [Pr.10] Deceleration time 0 | 0 | 0 | 83+150n |
| [Pr.52] | Home position return deceleration time selection | 1: [Pr.28] Deceleration time 1 | 1 | 0 | 83+150n |
| [Pr.52] | Home position return deceleration time selection | 2: [Pr.29] Deceleration time 2 | 2 | 0 | 83+150n |
| [Pr.52] | Home position return deceleration time selection | 3: [Pr.30] Deceleration time 3 | 3 | 0 | 83+150n |
| [Pr.53] | Home position shift amount [FX5-SSC-S] | The setting value range differs depending on the "[Pr.1] Unit setting". | The setting value range differs depending on the "[Pr.1] Unit setting". | 0 | 84+150n<br>85+150n |
| [Pr.54] | Home position return torque limit value [FX5-SSC-S] | 0.1 to 1000.0 (%) | 1 to 10000 (×0.1%) | 3000 | 86+150n |
| [Pr.55] | Operation setting for incompletion of home position return | 0: Positioning control is not executed. | 0 | 0 | 87+150n |
| [Pr.55] | Operation setting for incompletion of home position return | 1: Positioning control is executed. | 1 | 0 | 87+150n |
| [Pr.56] | Speed designation during home position shift [FX5-SSC-S] | 0: Home position return speed | 0 | 0 | 88+150n |
| [Pr.56] | Speed designation during home position shift [FX5-SSC-S] | 1: Creep speed | 1 | 0 | 88+150n |
| [Pr.57] | Dwell time during home position return retry [FX5-SSC-S] | 0 to 65535 (ms) | 0 to 65535 (ms)<br>0 to 32767: Set as a decimal<br>32768 to 65535: Convert into hexadecimal and set | 0 | 89+150n |

*In the original, the header "Setting value, setting range" spans the two columns "Value set with the engineering tool" / "Value set with a program". The Item, Default value and Buffer memory address cells are merged over the rows of each parameter ([Pr.51] 4 rows, [Pr.52] 4 rows, [Pr.55] 2 rows, [Pr.56] 2 rows). For [Pr.50] and [Pr.53], "The setting value range differs depending on the "[Pr.1] Unit setting"." is one cell merged over both setting columns. Expanded to each row.

#### [Pr.50] Setting for the movement amount after proximity dog ON [FX5-SSC-S] (近点ドグON後の移動量設定[FX5-SSC-S]) (11.3 / original p.490)

When using the count method 1 or 2, set the movement amount to the home position after the proximity dog signal turns ON.
(The movement amount after proximity dog ON should be equal to or greater than the sum of the "distance covered by the deceleration from the home position return speed to the creep speed" and "distance of movement in 10 ms at the home position return speed".)

##### ■Setting example (設定例) (11.3 / original p.490)

Assuming that the "[Pr.8] Speed limit value" is set to 200 kpulses/s, "[Pr.46] Home position return speed" to 10 kpulses/s, "[Pr.47] Creep speed" to 1 kpulses/s, and deceleration time to 300 ms, the minimum value of "[Pr.50] Setting for the movement amount after proximity dog ON" is calculated as follows:

[Figure] [Home position return operation] (original p.490)
- [Pr.8] Speed limit value: Vp = 200 kpulses/s (dotted line)
- [Pr.46] Home position return speed: Vz = 10 kpulses/s
- [Pr.47] Creep speed: Vc = 1 kpulses/s
- Deceleration time: Tb = 300 ms (time to decelerate from Vp to 0, drawn as the dotted slope)
- Actual deceleration time: t = Tb × Vz / Vp

Calculation (as shown in the figure):
```
[Deceleration distance] = 1/2 × Vz/1000 × t + 0.01 × Vz
                                              (0.01 × Vz: Movement amount for 10 ms at home position return speed.)
                        = Vz/2000 × (Tb × Vz)/Vp + 0.01 × Vz
                        = (10 × 10^3)/2000 × (300 × 10 × 10^3)/(200 × 10^3) + 0.01 × 10 × 10^3
                        = 75 + 100
                        = 175
→ "[Pr.50] Setting for the movement amount after proximity dog ON" should be equal to or larger than 175.
```

| [Pr.1] setting value | Value set with the engineering tool (unit) | Value set with a program (unit) |
|---|---|---|
| 0: mm | 0 to 214748364.7 (μm) | 0 to 2147483647 (×10^-1 μm) |
| 1: inch | 0 to 21474.83647 (inch) | 0 to 2147483647 (×10^-5 inch) |
| 2: degree | 0 to 21474.83647 (degree) | 0 to 2147483647 (×10^-5 degree) |
| 3: pulse | 0 to 2147483647 (pulse) | 0 to 2147483647 (pulse) |

> **Point**
> Regardless of the unit setting, calculate the movement amount in the same procedure as for the setting example.
> To calculate the movement amount, the deviation counter value is used to compensate the movement amount after the proximity dog is turned ON. If the deviation counter value is large, the corrected movement amount becomes small, and the error "Count method movement amount fault" (error code: 1944H) may occur. Adjust the gain to reduce the deviation counter value or to increase the movement amount.

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.490)

Refer to the following for the buffer memory address in this area.
→Page 425 Home position return parameters: Home position return detailed parameters

#### [Pr.51] Home position return acceleration time selection (原点復帰加速時間選択) (11.3 / original p.490)

Set which of "acceleration time 0 to 3" to use for the acceleration time during home position return.
0: Use the value set in "[Pr.9] Acceleration time 0".
1: Use the value set in "[Pr.25] Acceleration time 1".
2: Use the value set in "[Pr.26] Acceleration time 2".
3: Use the value set in "[Pr.27] Acceleration time 3".
Only valid at high-speed home position return. [FX5-SSC-G]

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.490)

Refer to the following for the buffer memory address in this area.
→Page 425 Home position return parameters: Home position return detailed parameters

#### [Pr.52] Home position return deceleration time selection (原点復帰減速時間選択) (11.3 / original p.491)

Set which of "deceleration time 0 to 3" to use for the deceleration time during home position return.
0: Use the value set in "[Pr.10] Deceleration time 0".
1: Use the value set in "[Pr.28] Deceleration time 1".
2: Use the value set in "[Pr.29] Deceleration time 2".
3: Use the value set in "[Pr.30] Deceleration time 3".
Only valid at high-speed home position return. [FX5-SSC-G]

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.491)

Refer to the following for the buffer memory address in this area.
→Page 425 Home position return parameters: Home position return detailed parameters

#### [Pr.53] Home position shift amount [FX5-SSC-S] (原点シフト量[FX5-SSC-S]) (11.3 / original p.491)

Set the amount to shift (move) from the position stopped at with machine home position return.
The home position shift function is used to compensate the home position stopped at with machine home position return.
If there is a physical limit to the home position, due to the relation of the proximity dog installation position, use this function to compensate the home position to an optimum position.

[Figure] Home position shift (original p.491)
- Arrow at top: "[Pr.44] Home position return direction" (left to right).
- From the Start point the axis accelerates in the home position return direction, decelerates to creep speed at proximity dog ON, and stops at the first zero signal after the proximity dog signal turns OFF.
- "When "[Pr.53] Home position shift amount" is positive": from the stop position the axis moves further in the home position return direction and stops at the Shift point (right).
- "When "[Pr.53] Home position shift amount" is negative": from the stop position the axis moves in the opposite direction (drawn as a dashed waveform below the axis) and stops at the Shift point (left, near the proximity dog ON position).
- Signals drawn: Proximity dog signal (ON section), Zero signal (pulses).

| [Pr.1] setting value | Value set with the engineering tool (unit) | Value set with a program (unit) |
|---|---|---|
| 0: mm | -214748364.8 to 214748364.7 (μm) | -2147483648 to 2147483647 (×10^-1 μm) |
| 1: inch | -21474.83648 to 21474.83647 (inch) | -2147483648 to 2147483647 (×10^-5 inch) |
| 2: degree | -21474.83648 to 21474.83647 (degree) | -2147483648 to 2147483647 (×10^-5 degree) |
| 3: pulse | -2147483648 to 2147483647 (pulse) | -2147483648 to 2147483647 (pulse) |

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.491)

Refer to the following for the buffer memory address in this area.
→Page 425 Home position return parameters: Home position return detailed parameters

#### [Pr.54] Home position return torque limit value [FX5-SSC-S] (原点復帰トルク制限値[FX5-SSC-S]) (11.3 / original p.492)

Set the value to limit the servo motor torque after reaching the creep speed during machine home position return.
Refer to the following for details on the torque limits.
→Page 241 Torque limit function

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.492)

Refer to the following for the buffer memory address in this area.
→Page 425 Home position return parameters: Home position return detailed parameters

#### [Pr.55] Operation setting for incompletion of home position return (原点復帰未完時動作設定) (11.3 / original p.492)

Set whether the positioning control is executed or not (When the home position return request flag is ON.).
0: Positioning control is not executed.
1: Positioning control is executed.
- When the home position return request flag is ON, selecting "0: Positioning control is not executed" will result in the error "Start at home position return incomplete" (error code: 19A6H [FX5-SSC-S], or error code: 1AA6H [FX5-SSC-G]), and positioning control will not be performed. At this time, operation with the manual control (JOG operation, inching operation, manual pulse generator operation) is available. The positioning control can be executed even if the home position return request flag is ON when selecting "1: Positioning control is executed".
- The following shows whether the positioning control is possible to start/restart or not when selecting "0: Positioning control is not executed".

| | |
|---|---|
| Start possible | Machine home position return, JOG operation, inching operation, manual pulse generator operation, and current value changing using current value changing start No. (9003) |
| Start/restart impossible control | When the following cases at block start, condition start, wait start, repeated start, multiple axes simultaneous start and pre-reading start<br>1-axis linear control, 2/3/4-axis linear interpolation control, 1/2/3/4-axis fixed-feed control, 2-axis circular interpolation control with sub point designation, 2-axis circular interpolation control with center point designation, 1/2/3/4-axis speed control, speed-position switching control (INC mode/ ABS mode), position-speed switching control, and current value changing using current value changing (No.1 to 600) |

*(The original table has no header row.)*

- When the home position return request flag is ON, starting the fast home position return will result in the error "Home position return request ON" (error code: 1945H [FX5-SSC-S], or error code: 1A45H [FX5-SSC-G]) despite the setting value of "Operation setting for incompletion of home position return", and the fast home position return will not be executed.

> **CAUTION**
> - Do not execute the positioning control in home position return request signal ON for the axis which uses in the positioning control. Failure to observe this could lead to an accident such as a collision.

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.492)

Refer to the following for the buffer memory address in this area.
→Page 425 Home position return parameters: Home position return detailed parameters

#### [Pr.56] Speed designation during home position shift [FX5-SSC-S] (原点シフト時速度指定[FX5-SSC-S]) (11.3 / original p.492)

Set the operation speed for when a value other than "0" is set for "[Pr.53] Home position shift amount". Select the setting from "[Pr.46] Home position return speed" or "[Pr.47] Creep speed".
0: Designate "[Pr.46] Home position return speed" as the setting value.
1: Designate "[Pr.47] Creep speed" as the setting value.

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.492)

Refer to the following for the buffer memory address in this area.
→Page 425 Home position return parameters: Home position return detailed parameters

#### [Pr.57] Dwell time during home position return retry [FX5-SSC-S] (原点復帰リトライ時ドウェルタイム[FX5-SSC-S]) (11.3 / original p.493)

When home position return retry is validated (when "1" is set for [Pr.48]), set the stop time after decelerating in 2) and 4) in the following drawing.

[Figure] Home position return retry operation (original p.493)
- 1): From the Start position the axis accelerates (to the right in the drawing).
- 2): The axis decelerates and stops. "Temporarily stop for the time set in [Pr.57]."
- 3): The axis moves in the reverse direction (to the left, drawn below the axis line).
- 4): The axis decelerates and stops. "Temporarily stop for the time set in [Pr.57]."
- 5): The axis accelerates again in the original direction (to the right).
- 6): The axis decelerates to creep speed and stops (home position return completes).

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.493)

Refer to the following for the buffer memory address in this area.
→Page 425 Home position return parameters: Home position return detailed parameters

### Extended parameters (拡張パラメータ) (11.3 / original p.494-497)

n: Axis No. - 1

| Item | | Value set with the engineering tool | Value set with a program | Default value | Buffer memory address |
|---|---|---|---|---|---|
| [Pr.91] | Optional data monitor: Data type setting 1 | (Setting value list below, common to [Pr.91] to [Pr.94]) | (Setting value list below, common to [Pr.91] to [Pr.94]) | 0 | 100+150n |
| [Pr.92] | Optional data monitor: Data type setting 2 | (Setting value list below, common to [Pr.91] to [Pr.94]) | (Setting value list below, common to [Pr.91] to [Pr.94]) | 0 | 101+150n |
| [Pr.93] | Optional data monitor: Data type setting 3 | (Setting value list below, common to [Pr.91] to [Pr.94]) | (Setting value list below, common to [Pr.91] to [Pr.94]) | 0 | 102+150n |
| [Pr.94] | Optional data monitor: Data type setting 4 | (Setting value list below, common to [Pr.91] to [Pr.94]) | (Setting value list below, common to [Pr.91] to [Pr.94]) | 0 | 103+150n |
| [Pr.512] | Optional SDO 1 [FX5-SSC-G] | Specify the object that will perform servo transient transmission.<br>[Figure: b31-b16: Index / b15-b0: Subindex (upper byte), Object size (lower byte)] | Example) When specifying an UNSIGNED32 object with the object index "6099H" and the sub-index "02H", specify as shown below.<br>Reading: "60990200H" (default size)<br>Writing: "6099204H" (size: 4 bytes) | 0 | 128+150n<br>129+150n |
| [Pr.591] | Optional data monitor: Data type expansion setting 1 [FX5-SSC-G] | Set the sub-index and size of the CiA402 object of the device.<br>Specify the size in bit lengths.<br>[Figure: b15-b8: Sub index / b7-b0: Size] | Example) When monitoring the effective load ratio (sub-index: 00h, size 1 [Word]), set "0010H". | 0 | 92+150n |
| [Pr.592] | Optional data monitor: Data type expansion setting 2 [FX5-SSC-G] | Set the sub-index and size of the CiA402 object of the device.<br>Specify the size in bit lengths.<br>[Figure: b15-b8: Sub index / b7-b0: Size] | Example) When monitoring the effective load ratio (sub-index: 00h, size 1 [Word]), set "0010H". | 0 | 93+150n |
| [Pr.593] | Optional data monitor: Data type expansion setting 3 [FX5-SSC-G] | Set the sub-index and size of the CiA402 object of the device.<br>Specify the size in bit lengths.<br>[Figure: b15-b8: Sub index / b7-b0: Size] | Example) When monitoring the effective load ratio (sub-index: 00h, size 1 [Word]), set "0010H". | 0 | 94+150n |
| [Pr.594] | Optional data monitor: Data type expansion setting 4 [FX5-SSC-G] | Set the sub-index and size of the CiA402 object of the device.<br>Specify the size in bit lengths.<br>[Figure: b15-b8: Sub index / b7-b0: Size] | Example) When monitoring the effective load ratio (sub-index: 00h, size 1 [Word]), set "0010H". | 0 | 95+150n |

Setting value list of [Pr.91] to [Pr.94] (one cell merged over [Pr.91] to [Pr.94] in the original):

| Value set with the engineering tool | Value set with a program |
|---|---|
| [FX5-SSC-S] | [FX5-SSC-S] |
| 0: No setting | 0 |
| 1: Effective load ratio*1 | 1 |
| 2: Regenerative load ratio | 2 |
| 3: Peak load ratio | 3 |
| 4: Load inertia moment ratio*1 | 4 |
| 5: Model loop gain*1 | 5 |
| 6: Bus voltage*1 | 6 |
| 7: Servo motor speed*1 | 7 |
| 8: Encoder multiple revolution counter | 8 |
| 9: Unit power consumption | 9 |
| 10: Instantaneous torque*1 | 10 |
| 12: Servo motor thermistor temperature | 12 |
| 13: Torque equivalent to disturbance*1 | 13 |
| 14: Overload alarm margin | 14 |
| 15: Excessive error alarm margin | 15 |
| 16: Settling time | 16 |
| 17: Overshoot amount | 17 |
| 18: Internal temperature of encoder | 18 |
| 20: Position feedback*2 | 20 |
| 21: Encoder position within one revolution*2 | 21 |
| 22: Selected droop pulse*2 | 22 |
| 23: Unit total power consumption*2 | 23 |
| 24: Load-side encoder information 1*2 | 24 |
| 25: Load-side encoder information 2*2 | 25 |
| 26: Z-phase counter*2 | 26 |
| 27: Servo motor side/load-side position deviation*2 | 27 |
| 28: Servo motor side/load-side speed deviation*2 | 28 |
| 29: External encoder counter value*2 | 29 |
| 30: Unit power consumption (2 words)*2 | 30 |
| Most significant bit1 + address value: Optional address of registered monitor | Most significant bit1 + address value |
| [FX5-SSC-G] | [FX5-SSC-G] |
| Set the index of the CiA402 object of the device. | Example) When monitoring the effective load ratio, set "2B09H". |

*1 The name differs depending on the connected device.
*2 Used point: 2 words

*In the original, the header "Setting value, setting range" spans the two columns "Value set with the engineering tool" / "Value set with a program". The setting value list of [Pr.91] to [Pr.94] is one cell merged over the 4 rows [Pr.91] to [Pr.94]; it is written once as a separate list above instead of repeating it in each row. For [Pr.591] to [Pr.594], the setting cells (engineering tool and program) are merged over the 4 rows; expanded to each row. The bit layout figures in the [Pr.512] and [Pr.591] cells are written as text in brackets.*
*(Note: "Writing: "6099204H"" is as printed in the original (7 hex digits).)*

#### [Pr.91] to [Pr.94] Optional data monitor: Data type setting (任意データモニタデータ種別設定) (11.3 / original p.495-496)

Set the data type monitored by the optional data monitor function.

##### ■Setting values [FX5-SSC-S] (設定値[FX5-SSC-S]) (11.3 / original p.495-496)

| Setting value | Data type | Used point |
|---|---|---|
| 0 | No setting*1 | 1 word |
| 1 | Effective load ratio*2 | 1 word |
| 2 | Regenerative load ratio | 1 word |
| 3 | Peak load ratio | 1 word |
| 4 | Load inertia moment ratio*2 | 1 word |
| 5 | Model loop gain*2 | 1 word |
| 6 | Bus voltage*2 | 1 word |
| 7 | Servo motor speed*2 | 1 word |
| 8 | Encoder multiple revolution counter | 1 word |
| 9 | Unit power consumption | 1 word |
| 10 | Instantaneous torque*2 | 1 word |
| 12 | Servo motor thermistor temperature | 1 word |
| 13 | Torque equivalent to disturbance*2 | 1 word |
| 14 | Overload alarm margin | 1 word |
| 15 | Excessive error alarm margin | 1 word |
| 16 | Settling time | 1 word |
| 17 | Overshoot amount | 1 word |
| 18 | Internal temperature of encoder | 1 word |
| 20 | Position feedback | 2 words |
| 21 | Encoder position within one revolution | 2 words |
| 22 | Selected droop pulse | 2 words |
| 23 | Unit total power consumption | 2 words |
| 24 | Load-side encoder information 1 | 2 words |
| 25 | Load-side encoder information 2 | 2 words |
| 26 | Z-phase counter | 2 words |
| 27 | Servo motor side/load-side position deviation | 2 words |
| 28 | Servo motor side/load-side speed deviation | 2 words |
| 29 | External encoder counter value | 2 words |
| 30 | Unit power consumption (2 words) | 2 words |
| Most significant bit1 + address value | Optional address of registered monitor | — |

*1 The stored value of "[Md.109] Regenerative load ratio/Optional data monitor output 1" to "[Md.112] Optional data monitor output 4" is different every data type setting 1 to 4. (→Page 527 Axis monitor data)
*2 The name differs depending on the connected device.

*In the original, "1 word" is merged over the 18 rows 0 to 18, and "2 words" over the 11 rows 20 to 30. Expanded to each row.

> **Point**
> - The monitor address of optional data monitor is registered to servo amplifier with initialized communication after power supply ON or CPU module reset.
> - Set the data type of "used point: 2 words" in "[Pr.91] Optional data monitor: Data type setting 1" or "[Pr.93] Optional data monitor: Data type setting 3". If it is set in "[Pr.92] Optional data monitor: Data type setting 2" or "[Pr.94] Optional data monitor: Data type setting 4", the warning "Optional data monitor data type setting error" (warning code: 0933H) will occur with initialized communication to servo amplifier and "0" will be set in "[Md.109] Regenerative load ratio/Optional data monitor output 1" to "[Md.112] Optional data monitor output 4".
> - Set "0" in "[Pr.92] Optional data monitor: Data type setting 2" when the data type of "used point: 2 words" is set in "[Pr.91] Optional data monitor: Data type setting 1", and set "0" in "[Pr.94] Optional data monitor: Data type setting 4" when the data type of "used point: 2 words" is set in "[Pr.93] Optional data monitor: Data type setting 3". When setting other than "0", the warning "Optional data monitor data type setting error" (warning code: 0933H) will occur with initialized communication to servo amplifier and "0" will be set in "[Md.109] Regenerative load ratio/Optional data monitor output 1" to "[Md.112] Optional data monitor output 4".
> - When the data type of "used point: 2 words" is set, the monitor data of low-order is "[Md.109] Regenerative load ratio/Optional data monitor output 1" or "[Md.111] Peak torque ratio/Optional data monitor output 3".
> - Refer to →Page 371 Optional Data Monitor Function for the data type that can be monitored on each servo amplifier. When the data type that cannot be monitored is set, "0" is stored to the monitor output.
> - When directly specifying addresses for each optional data monitor type, specify the addresses in bit0 to bit14 of "[Pr.91] Optional data monitor: Data type setting 1" to "[Pr.94] Optional data monitor: Data type setting 4" and set "1" in bit15.
> - When monitoring 2-word data, set the lower data to "[Pr.91] Optional data monitor: Data type setting 1" and the upper data to "[Pr.92] Optional data monitor: Data type setting 2", or the lower data to "[Pr.93] Optional data monitor: Data type setting 3" and the upper data to "[Pr.94] Optional data monitor: Data type setting 4".

##### ■Setting values [FX5-SSC-G] (設定値[FX5-SSC-G]) (11.3 / original p.496)

Set the index for the CiA402 object of the device.

> **Point**
> - Registered monitor addresses for the optional data monitor are imported after the power is turned ON or the CPU module is reset.
> - Set data types that use 2 points in either "[Pr.91] Optional data monitor: Data type setting 1" and "[Pr.591] Optional data monitor: Data type expansion setting 1" or "[Pr.93] Optional data monitor: Data type setting 3" and "[Pr.593] Optional data monitor: Data type expansion setting 3". The setting values of both "[Pr.92] Optional data monitor: Data type setting 2" and "[Pr.592] Optional data monitor: Data type expansion setting 2" and [Pr.94] Optional data monitor: Data type setting 4" and "[Pr.594] Optional data monitor: Data type expansion setting 4"are ignored.
> - When a value other than 08H, 10H, 20H, or 40H is set as the size in "[Pr.591] Optional data monitor: Data type expansion setting 1" to "[Pr.594] Optional data monitor: Data type expansion setting 4", the value is treated as being 20H.
> - When a CiA402 object that cannot be monitored is set, the error "PDO mapping setting error" (error code: 1C48H) occurs and communication with that axis is not performed.

*(Note: the missing opening quotation mark before "[Pr.94]" and the missing space in "4"are ignored" are as printed in the original.)*

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.496)

For the buffer memory addresses in this area, refer to the following.
→Page 425 Extended parameters

#### [Pr.512] Optional SDO 1 [FX5-SSC-G] (任意SDO 1[FX5-SSC-G]) (11.3 / original p.497)

Specify the object that will perform servo transient transmission. For details, refer to the following.
→Page 381 Servo Transient Transmission Function [FX5-SSC-G]

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.497)

For the buffer memory addresses in this area, refer to the following.
→Page 425 Extended parameters

#### [Pr.591] to [Pr.594] Optional data monitor: Data type expansion setting [FX5-SSC-G] (任意データモニタデータ種別拡張設定[FX5-SSC-G]) (11.3 / original p.497)

Set the data type to monitor with the optional data monitor function. For details of the data, refer to the manual of the servo amplifier.
For MR-J5(W)-G: [Other manual] MR-J5-G/MR-J5W-G User’s Manual (Object Dictionary)
Set the sub-index and size of the CiA402 object of the device.
Specify the size in bit lengths.

##### ■Buffer memory address (バッファメモリアドレス) (11.3 / original p.497)

For the buffer memory addresses in this area, refer to the following.
→Page 425 Extended parameters

### Servo parameters [FX5-SSC-S] (サーボパラメータ[FX5-SSC-S]) (11.3 / original p.498)

#### Servo series (サーボシリーズ) (11.3 / original p.498)

n: Axis No. -1

| Item | | Setting details | Set range | Default value | Buffer memory address |
|---|---|---|---|---|---|
| [Pr.100] | Servo series | Used to select the servo amplifier series to connect to the Simple Motion module. | 0: Not set<br>1: MR-J3-_B_, MR-J3W-_B (2-axis type)<br>3: MR-J3-_BS (For safety servo)<br>32: MR-J4-_B_(-RJ), MR-J4W_-_B (2-axis type, 3-axis type)<br>48: MR-JE-_B(F)<br>68: FR-A800-1<br>69: FR-A800-2<br>96: VCII series (manufactured by CKD NIKKI DENSO CO., LTD.)<br>97: AlphaStep/5-phase (manufactured by ORIENTAL MOTOR Co., Ltd.)<br>98: IAI electric actuator controller (manufactured by IAI Corporation)<br>99: VPH series (manufactured by CKD NIKKI DENSO CO., LTD.)<br>128: MR-J5-_B_(-RJ), MR-J5W_-_B (2-axis type, 3-axis type)<br>4097: Virtual servo amplifier (MR-J3)<br>4128: Virtual servo amplifier (MR-J4)<br>4224: Virtual servo amplifier (MR-J5) | 0 | 28400+100n |

*(Note: "VCII" is printed with the Roman numeral Ⅱ in the original ("VCⅡ series"); text extraction drops it.)*

> **Point**
> - Be sure to set up servo series. Communication with servo amplifier is not started by the initial value "0" in default value. (The LED indication of servo amplifier indicates "Ab".)
> - The connectable servo amplifier differs by the setting of "[Pr.97] SSCNET setting".

#### Parameters of MR-J5(W)-B (MR-J5(W)-Bのパラメータ) (11.3 / original p.498)

Refer to the manuals of each servo amplifier for details of the parameter list and setting items for MR-J5(W)-B.
Since the servo parameters of MR-J5(W)-B are not in the buffer memory, use GX Works3 or axis control data to set them.
Refer to the following for details.
→Page 845 Connection with MR-J5(W)-B
The default value of each parameter indicates the value to be stored in the internal memory area.
Never change the setting values of buffer memory other than the parameters described in each servo amplifier manual.

> **Point**
> Change the parameter value (or transfer the parameter to servo amplifier from Simple Motion module) and switch OFF the power once, and then switch it on again to make the changed parameter value valid.

#### Parameters of MR-J4(W)-B/MR-JE-B(F)/MR-J3(W)-B (MR-J4(W)-B/MR-JE-B(F)/MR-J3(W)-Bのパラメータ) (11.3 / original p.498)

Refer to each servo amplifier instruction manual for details of the parameter list and setting items for MR-J4(W)-B/MR-JE-B(F)/MR-J3(W)-B. Never change the setting values of buffer memory other than the parameters described in each servo amplifier instruction manual.

## 11.4 Positioning Data (位置決めデータ) (11.4 / original p.499-510)

Before explaining the positioning data setting items [Da.1] to [Da.10], [Da.20] to [Da.22], the configuration of the positioning data is shown below.
The positioning data stored in the buffer memory of the Simple Motion module/Motion module is the following configuration.

[Figure] Configuration of the positioning data in the buffer memory (original p.499)
- n: Axis No. - 1. Buffer memory address of each item (Positioning data No.1 / No.2 / ... / No.99 / No.100):

| Item | Positioning data No.1 | Positioning data No.2 | Positioning data No.99 | Positioning data No.100 |
|---|---|---|---|---|
| Positioning identifier [Da.1] to [Da.4] | 6000+1000n | 6010+1000n | 6980+1000n | 6990+1000n |
| [Da.10] M code/Condition data No./Number of LOOP to LEND repetitions | 6001+1000n | 6011+1000n | 6981+1000n | 6991+1000n |
| [Da.9] Dwell time/JUMP destination positioning data No. | 6002+1000n | 6012+1000n | 6982+1000n | 6992+1000n |
| [Da.8] Command speed | 6004+1000n<br>6005+1000n | 6014+1000n<br>6015+1000n | 6984+1000n<br>6985+1000n | 6994+1000n<br>6995+1000n |
| [Da.6] Positioning address/movement amount | 6006+1000n<br>6007+1000n | 6016+1000n<br>6017+1000n | 6986+1000n<br>6987+1000n | 6996+1000n<br>6997+1000n |
| [Da.7] Arc address | 6008+1000n<br>6009+1000n | 6018+1000n<br>6019+1000n | 6988+1000n<br>6989+1000n | 6998+1000n<br>6999+1000n |
| Axis to be interpolated No. [Da.20] to [Da.22] | 71000+1000n<br>71001+1000n | 71010+1000n<br>71011+1000n | 71980+1000n<br>71981+1000n | 71990+1000n<br>71991+1000n |

- ● Up to 100 positioning data items can be set (stored) for each axis in the buffer memory address shown on the left. No.101 to No.600 are not allocated to buffer memory. Set with the engineering tool. Data is controlled as positioning data No.1 to 600 for each axis.
- ● One positioning data item is configured of the items shown in the bold box.
- Configuration of positioning identifier (one word, b15 to b0): b15-b8: [Da.2] Control method / b7-b6: [Da.4] Deceleration time No. / b5-b4: [Da.3] Acceleration time No. / b1-b0: [Da.1] Operation pattern.
- Configuration of axis to be interpolated No. (buffer memory, 2 words): b7-b0: [Da.20] Axis to be interpolated No.1 / b15-b8: [Da.21] Axis to be interpolated No.2 / b23-b16: [Da.22] Axis to be interpolated No.3 / b31-b24: Not used*1
- *1: Always "0" is set to the part not used.

The following explains the positioning data setting items [Da.1] to [Da.10] and [Da.20] to [Da.22]. (The buffer memory addresses shown are those of the "positioning data No.1".)
n: Axis No. - 1

| Item | | | Value set with the engineering tool | Value set with a program | Default value | Buffer memory address |
|---|---|---|---|---|---|---|
| Positioning identifier | [Da.1] | Operation pattern | 00: Positioning complete | 00 | 0000H | 6000+1000n |
| Positioning identifier | [Da.1] | Operation pattern | 01: Continuous positioning control | 01 | 0000H | 6000+1000n |
| Positioning identifier | [Da.1] | Operation pattern | 11: Continuous path control | 11 | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 01H: ABS Linear 1 | 01H | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 02H: INC Linear 1 | 02H | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 03H: Feed 1 | 03H | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 04H: FWD V1 | 04H | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 05H: RVS V1 | 05H | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 06H: FWD V/P | 06H | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 07H: RVS V/P | 07H | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 08H: FWD P/V | 08H | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 09H: RVS P/V | 09H | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 0AH: ABS Linear 2 | 0AH | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 0BH: INC Linear 2 | 0BH | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 0CH: Feed 2 | 0CH | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 0DH: ABS ArcMP | 0DH | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 0EH: INC ArcMP | 0EH | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 0FH: ABS ArcRGT | 0FH | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 10H: ABS ArcLFT | 10H | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 11H: INC ArcRGT | 11H | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 12H: INC ArcLFT | 12H | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 13H: FWD V2 | 13H | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 14H: RVS V2 | 14H | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 15H: ABS Linear 3 | 15H | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 16H: INC Linear 3 | 16H | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 17H: Feed 3 | 17H | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 18H: FWD V3 | 18H | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 19H: RVS V3 | 19H | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 1AH: ABS Linear 4 | 1AH | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 1BH: INC Linear 4 | 1BH | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 1CH: Feed 4 | 1CH | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 1DH: FWD V4 | 1DH | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 1EH: RVS V4 | 1EH | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 80H: NOP | 80H | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 81H: Address CHG | 81H | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 82H: JUMP | 82H | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 83H: LOOP | 83H | 0000H | 6000+1000n |
| Positioning identifier | [Da.2] | Control method | 84H: LEND | 84H | 0000H | 6000+1000n |
| Positioning identifier | [Da.3] | Acceleration time No. | 0: [Pr.9] Acceleration time 0 | 00 | 0000H | 6000+1000n |
| Positioning identifier | [Da.3] | Acceleration time No. | 1: [Pr.25] Acceleration time 1 | 01 | 0000H | 6000+1000n |
| Positioning identifier | [Da.3] | Acceleration time No. | 2: [Pr.26] Acceleration time 2 | 10 | 0000H | 6000+1000n |
| Positioning identifier | [Da.3] | Acceleration time No. | 3: [Pr.27] Acceleration time 3 | 11 | 0000H | 6000+1000n |
| Positioning identifier | [Da.4] | Deceleration time No. | 0: [Pr.10] Deceleration time 0 | 00 | 0000H | 6000+1000n |
| Positioning identifier | [Da.4] | Deceleration time No. | 1: [Pr.28] Deceleration time 1 | 01 | 0000H | 6000+1000n |
| Positioning identifier | [Da.4] | Deceleration time No. | 2: [Pr.29] Deceleration time 2 | 10 | 0000H | 6000+1000n |
| Positioning identifier | [Da.4] | Deceleration time No. | 3: [Pr.30] Deceleration time 3 | 11 | 0000H | 6000+1000n |
| [Da.6] | Positioning address/movement amount | — | The setting value range differs according to the "[Da.2] Control method". | The setting value range differs according to the "[Da.2] Control method". | 0 | 6006+1000n<br>6007+1000n |
| [Da.7] | Arc address | — | The setting value range differs according to the "[Da.2] Control method". | The setting value range differs according to the "[Da.2] Control method". | 0 | 6008+1000n<br>6009+1000n |
| [Da.8] | Command speed | — | The setting value range differs depending on the "[Pr.1] Unit setting". | The setting value range differs depending on the "[Pr.1] Unit setting". | 0 | 6004+1000n<br>6005+1000n |
| [Da.8] | Command speed | — | -1: Current speed (Speed set for previous positioning data No.) | -1 | 0 | 6004+1000n<br>6005+1000n |
| [Da.9] | Dwell time/JUMP destination positioning data No. | Dwell time | The setting value range differs according to the "[Da.2] Control method". | The setting value range differs according to the "[Da.2] Control method". | 0 | 6002+1000n |
| [Da.9] | Dwell time/JUMP destination positioning data No. | JUMP destination positioning data No. | The setting value range differs according to the "[Da.2] Control method". | The setting value range differs according to the "[Da.2] Control method". | 0 | 6002+1000n |
| [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | M code | The setting value range differs according to the "[Da.2] Control method". | The setting value range differs according to the "[Da.2] Control method". | 0 | 6001+1000n |
| [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | Condition data No. | The setting value range differs according to the "[Da.2] Control method". | The setting value range differs according to the "[Da.2] Control method". | 0 | 6001+1000n |
| [Da.10] | M code/Condition data No./Number of LOOP to LEND repetitions | Number of LOOP to LEND repetitions | The setting value range differs according to the "[Da.2] Control method". | The setting value range differs according to the "[Da.2] Control method". | 0 | 6001+1000n |
| Axis to be interpolated | [Da.20] Axis to be interpolated No.1 | — | 0: Axis 1 selected | 0H | 0000H | 71000+1000n<br>71001+1000n |
| Axis to be interpolated | [Da.20] Axis to be interpolated No.1 | — | 1: Axis 2 selected | 1H | 0000H | 71000+1000n<br>71001+1000n |
| Axis to be interpolated | [Da.20] Axis to be interpolated No.1 | — | 2: Axis 3 selected | 2H | 0000H | 71000+1000n<br>71001+1000n |
| Axis to be interpolated | [Da.20] Axis to be interpolated No.1 | — | 3: Axis 4 selected | 3H | 0000H | 71000+1000n<br>71001+1000n |
| Axis to be interpolated | [Da.20] Axis to be interpolated No.1 | — | 4: Axis 5 selected | 4H | 0000H | 71000+1000n<br>71001+1000n |
| Axis to be interpolated | [Da.20] Axis to be interpolated No.1 | — | 5: Axis 6 selected | 5H | 0000H | 71000+1000n<br>71001+1000n |
| Axis to be interpolated | [Da.20] Axis to be interpolated No.1 | — | 6: Axis 7 selected | 6H | 0000H | 71000+1000n<br>71001+1000n |
| Axis to be interpolated | [Da.20] Axis to be interpolated No.1 | — | 7: Axis 8 selected | 7H | 0000H | 71000+1000n<br>71001+1000n |
| Axis to be interpolated | [Da.21] Axis to be interpolated No.2 | — | 0: Axis 1 selected | 0H | 0000H | 71000+1000n<br>71001+1000n |
| Axis to be interpolated | [Da.21] Axis to be interpolated No.2 | — | 1: Axis 2 selected | 1H | 0000H | 71000+1000n<br>71001+1000n |
| Axis to be interpolated | [Da.21] Axis to be interpolated No.2 | — | 2: Axis 3 selected | 2H | 0000H | 71000+1000n<br>71001+1000n |
| Axis to be interpolated | [Da.21] Axis to be interpolated No.2 | — | 3: Axis 4 selected | 3H | 0000H | 71000+1000n<br>71001+1000n |
| Axis to be interpolated | [Da.21] Axis to be interpolated No.2 | — | 4: Axis 5 selected | 4H | 0000H | 71000+1000n<br>71001+1000n |
| Axis to be interpolated | [Da.21] Axis to be interpolated No.2 | — | 5: Axis 6 selected | 5H | 0000H | 71000+1000n<br>71001+1000n |
| Axis to be interpolated | [Da.21] Axis to be interpolated No.2 | — | 6: Axis 7 selected | 6H | 0000H | 71000+1000n<br>71001+1000n |
| Axis to be interpolated | [Da.21] Axis to be interpolated No.2 | — | 7: Axis 8 selected | 7H | 0000H | 71000+1000n<br>71001+1000n |
| Axis to be interpolated | [Da.22] Axis to be interpolated No.3 | — | 0: Axis 1 selected | 0H | 0000H | 71000+1000n<br>71001+1000n |
| Axis to be interpolated | [Da.22] Axis to be interpolated No.3 | — | 1: Axis 2 selected | 1H | 0000H | 71000+1000n<br>71001+1000n |
| Axis to be interpolated | [Da.22] Axis to be interpolated No.3 | — | 2: Axis 3 selected | 2H | 0000H | 71000+1000n<br>71001+1000n |
| Axis to be interpolated | [Da.22] Axis to be interpolated No.3 | — | 3: Axis 4 selected | 3H | 0000H | 71000+1000n<br>71001+1000n |
| Axis to be interpolated | [Da.22] Axis to be interpolated No.3 | — | 4: Axis 5 selected | 4H | 0000H | 71000+1000n<br>71001+1000n |
| Axis to be interpolated | [Da.22] Axis to be interpolated No.3 | — | 5: Axis 6 selected | 5H | 0000H | 71000+1000n<br>71001+1000n |
| Axis to be interpolated | [Da.22] Axis to be interpolated No.3 | — | 6: Axis 7 selected | 6H | 0000H | 71000+1000n<br>71001+1000n |
| Axis to be interpolated | [Da.22] Axis to be interpolated No.3 | — | 7: Axis 8 selected | 7H | 0000H | 71000+1000n<br>71001+1000n |

*In the original, the header "Setting value" spans the two columns "Value set with the engineering tool" / "Value set with a program". The table continues from p.500 to p.501 (header repeated). "Positioning identifier" is merged over [Da.1] to [Da.4] (46 rows) and "Axis to be interpolated" over [Da.20] to [Da.22]; each [Da.] item name is merged over its own rows. The Default value "0000H" and Buffer memory address "6000+1000n" cells are merged over all rows of [Da.1] to [Da.4], and "0000H" / "71000+1000n, 71001+1000n" over [Da.20] to [Da.22]. The setting value list "0: Axis 1 selected" to "7: Axis 8 selected" / "0H" to "7H" is one cell merged over [Da.20] to [Da.22]. "The setting value range differs according to the "[Da.2] Control method"." is one cell merged over both setting columns and over [Da.6] and [Da.7], and another over [Da.9] and [Da.10] (all sub-items); for [Da.8] the "[Pr.1] Unit setting" sentence spans both setting columns. Expanded to each row. The "—" in the third column means the original has no sub-item cell (the item name spans it).*

Figures inside the "Value set with a program" column of the original:
- [Da.1] to [Da.4]: The value is written as "H□□□□". The upper two hexadecimal digits are the "[Da.2]" setting value; the lower two digits are the "Setting value" obtained by "Convert into hexadecimal" of bits b7 to b0, where b7-b6 = [Da.4], b5-b4 = [Da.3], and b1-b0 = [Da.1] (b15 to b8 = [Da.2]).
- [Da.20] to [Da.22]: b7-b0 (low-order bits) = [Da.20], b15-b8 = [Da.21]; b23-b16 = [Da.22], b31-b24 = Not used*1. "*1: Always "0" is set to the part not used."

### [Da.1] Operation pattern (運転パターン) (11.4 / original p.501)

The operation pattern designates whether positioning of a certain data No. is to be ended with just that data, or whether the positioning for the next data No. is to be carried out in succession.

| Operation pattern | Setting value | Details |
|---|---|---|
| Positioning complete | 00 | Set to execute positioning to the designated address, and then complete positioning. |
| Continuous positioning control | 01 | Positioning is carried out successively in order of data Nos. with one start signal. The operation halts at each position indicated by a positioning data. |
| Continuous path control | 11 | Positioning is carried out successively in order of data Nos. with one start signal. The operation does not stop at each positioning data. |

#### ■Buffer memory address (バッファメモリアドレス) (11.4 / original p.501)

Refer to the following for the buffer memory address in this area.
→Page 431 Positioning data

### [Da.2] Control method (制御方式) (11.4 / original p.502)

Set the "control method" for carrying out positioning control.

> **Point**
> - When "JUMP instruction" is set for the control method, the "[Da.9] Dwell time/JUMP destination positioning data No." and "[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions" setting details will differ.
> - In case you selected "LOOP" as the control method, the "[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions" should be set differently from other cases.
> - Refer to the following for details on the control methods.
> →Page 58 MAJOR POSITIONING CONTROL
> - If "degree" is set for "[Pr.1] Unit setting", 2-axis circular interpolation control cannot be carried out. (The error "Circular interpolation not possible" (error code: 199FH [FX5-SSC-S], or error code: 1A9FH [FX5-SSC-G]) will occur when executed.)

#### ■Buffer memory address (バッファメモリアドレス) (11.4 / original p.502)

Refer to the following for the buffer memory address in this area.
→Page 431 Positioning data

### [Da.3] Acceleration time No. (加速時間No.) (11.4 / original p.502)

Set which of "acceleration time 0 to 3" to use for the acceleration time during positioning.
0: Use the value set in "[Pr.9] Acceleration time 0".
1: Use the value set in "[Pr.25] Acceleration time 1".
2: Use the value set in "[Pr.26] Acceleration time 2".
3: Use the value set in "[Pr.27] Acceleration time 3".

#### ■Buffer memory address (バッファメモリアドレス) (11.4 / original p.502)

Refer to the following for the buffer memory address in this area.
→Page 431 Positioning data

### [Da.4] Deceleration time No. (減速時間No.) (11.4 / original p.502)

Set which of "deceleration time 0 to 3" to use for the deceleration time during positioning.
0: Use the value set in "[Pr.10] Deceleration time 0".
1: Use the value set in "[Pr.28] Deceleration time 1".
2: Use the value set in "[Pr.29] Deceleration time 2".
3: Use the value set in "[Pr.30] Deceleration time 3".

#### ■Buffer memory address (バッファメモリアドレス) (11.4 / original p.502)

Refer to the following for the buffer memory address in this area.
→Page 431 Positioning data

### [Da.6] Positioning address/movement amount (位置決めアドレス／移動量) (11.4 / original p.503-506)

Set the address to be used as the target value for positioning control.
The setting value range differs according to the "[Da.2] Control method".

#### ■Absolute (ABS) system, current value changing (アブソリュート(ABS)方式，現在値変更) (11.4 / original p.503)

- The setting value (positioning address) for the ABS system and current value changing is set with an absolute address (address from home position).

[Figure] ABS system (original p.503)
- Stop position (positioning start address) is 1000. Positioning to -1000 is a movement amount of 2000 (negative direction); positioning to 3000 is a movement amount of 2000 (positive direction).

#### ■Incremental (INC) system, fixed-feed 1, fixed-feed 2, fixed-feed 3, fixed-feed 4 (インクリメント(INC)方式，定寸送り1～4) (11.4 / original p.503)

- The setting value (movement amount) for the INC system is set as a movement amount with sign.
When movement amount is positive: Moves in the positive direction (address increment direction)
When movement amount is negative: Moves in the negative direction (address decrement direction)

[Figure] INC system (original p.503)
- From the Stop position (positioning start position): (Movement amount) -30000 → Moves in negative direction; (Movement amount) 30000 → Moves in positive direction.

#### ■Speed-position switching control (速度・位置切換え制御時) (11.4 / original p.503)

- INC mode: Set the amount of movement after the switching from speed control to position control.
- ABS mode: Set the absolute address which will be the target value after speed control is switched to position control. (The unit is "degree" only)

[Figure] Speed-position switching control (original p.503)
- Speed/Time chart: Speed control → at "Speed-position switching" → Position control (hatched area) → stop.
- The hatched area after switching is the "Movement amount setting (INC mode)"; the stop point is the "Target address setting (ABS mode)".

#### ■Position-speed switching control (位置・速度切換え制御時) (11.4 / original p.504-506)

- Set the amount of movement before the switching from position control to speed control.

##### ● When "[Pr.1] Unit setting" is "mm" (「mm」の場合) (11.4 / original p.504)

The table below lists the control methods that require the setting of the positioning address or movement amount and the associated setting ranges.
(With any control method excluded from the table below, neither the positioning address nor the movement amount needs to be set.)

| [Da.2] setting value | Value set with the engineering tool (μm) | Value set with a program*1 (×10^-1 μm) |
|---|---|---|
| ABS Linear 1: 01H<br>ABS Linear 2: 0AH<br>ABS Linear 3: 15H<br>ABS Linear 4: 1AH<br>Current value changing: 81H | • Set the address<br>-214748364.8 to 214748364.7 | • Set the address<br>-2147483648 to 2147483647 |
| INC Linear 1: 02H<br>INC Linear 2: 0BH<br>INC Linear 3: 16H<br>INC Linear 4: 1BH<br>Fixed-feed 1: 03H<br>Fixed-feed 2: 0CH<br>Fixed-feed 3: 17H<br>Fixed-feed 4: 1CH | • Set the movement amount<br>-214748364.8 to 214748364.7 | • Set the movement amount<br>-2147483648 to 2147483647 |
| Forward run speed/position: 06H<br>Reverse run speed/position: 07H<br>Forward run position/speed: 08H<br>Reverse run position/speed: 09H | • Set the movement amount<br>0 to 214748364.7 | • Set the movement amount<br>0 to 2147483647 |
| ABS circular sub: 0DH<br>ABS circular right: 0FH<br>ABS circular left: 10H | • Set the address<br>-214748364.8 to 214748364.7 | • Set the address<br>-2147483648 to 2147483647 |
| INC circular sub: 0EH<br>INC circular right: 11H<br>INC circular left: 12H | • Set the movement amount<br>-214748364.8 to 214748364.7 | • Set the movement amount<br>-2147483648 to 2147483647 |

*1 Set an integer because the program cannot handle fractions.
(The value will be converted properly within the system.)

##### ● When "[Pr.1] Unit setting" is "degree" (「degree」の場合) (11.4 / original p.505)

The table below lists the control methods that require the setting of the positioning address or movement amount and the associated setting ranges.
(With any control method excluded from the table below, neither the positioning address nor the movement amount needs to be set.)

| [Da.2] setting value | Value set with the engineering tool (degree) | Value set with a program*1 (×10^-5 degree) |
|---|---|---|
| ABS Linear 1: 01H<br>ABS Linear 2: 0AH<br>ABS Linear 3: 15H<br>ABS Linear 4: 1AH<br>Current value changing: 81H | • Set the address<br>0 to 359.99999 | • Set the address<br>0 to 35999999 |
| INC Linear 1: 02H<br>INC Linear 2: 0BH<br>INC Linear 3: 16H<br>INC Linear 4: 1BH<br>Fixed-feed 1: 03H<br>Fixed-feed 2: 0CH<br>Fixed-feed 3: 17H<br>Fixed-feed 4: 1CH | • Set the movement amount<br>-21474.83648 to 21474.83647 | • Set the movement amount<br>-2147483648 to 2147483647*2 |
| Forward run speed/position: 06H<br>Reverse run speed/position: 07H | In INC mode<br>• Set the movement amount<br>0 to 21474.83647<br>In ABS mode<br>• Set the address<br>0 to 359.99999 | In INC mode<br>• Set the movement amount<br>0 to 2147483647<br>In ABS mode<br>• Set the address<br>0 to 35999999 |
| Forward run position/speed: 08H<br>Reverse run position/speed: 09H | • Set the movement amount<br>0 to 21474.83647 | • Set the movement amount<br>0 to 2147483647 |

*1 Set an integer because the program cannot handle fractions.
(The value will be converted properly within the system.)
*2 When the software stroke limit is valid, -35999999 to 35999999 is set.

##### ● When "[Pr.1] Unit setting" is "pulse" (「pulse」の場合) (11.4 / original p.505)

The table below lists the control methods that require the setting of the positioning address or movement amount and the associated setting ranges.
(With any control method excluded from the table below, neither the positioning address nor the movement amount needs to be set.)

| [Da.2] setting value | Value set with the engineering tool (pulse) | Value set with a program (pulse) |
|---|---|---|
| ABS Linear 1: 01H<br>ABS Linear 2: 0AH<br>ABS Linear 3: 15H<br>ABS Linear 4: 1AH<br>Current value changing: 81H | • Set the address<br>-2147483648 to 2147483647 | • Set the address<br>-2147483648 to 2147483647 |
| INC Linear 1: 02H<br>INC Linear 2: 0BH<br>INC Linear 3: 16H<br>INC Linear 4: 1BH<br>Fixed-feed 1: 03H<br>Fixed-feed 2: 0CH<br>Fixed-feed 3: 17H<br>Fixed-feed 4: 1CH | • Set the movement amount<br>-2147483648 to 2147483647 | • Set the movement amount<br>-2147483648 to 2147483647 |
| Forward run speed/position: 06H<br>Reverse run speed/position: 07H<br>Forward run position/speed: 08H<br>Reverse run position/speed: 09H | • Set the movement amount<br>0 to 2147483647 | • Set the movement amount<br>0 to 2147483647 |
| ABS circular sub: 0DH<br>ABS circular right: 0FH<br>ABS circular left: 10H | • Set the address<br>-2147483648 to 2147483647 | • Set the address<br>-2147483648 to 2147483647 |
| INC circular sub: 0EH<br>INC circular right: 11H<br>INC circular left: 12H | • Set the movement amount<br>-2147483648 to 2147483647 | • Set the movement amount<br>-2147483648 to 2147483647 |

##### ● When "[Pr.1] Unit setting" is "inch" (「inch」の場合) (11.4 / original p.506)

The table below lists the control methods that require the setting of the positioning address or movement amount and the associated setting ranges.
(With any control method excluded from the table below, neither the positioning address nor the movement amount needs to be set.)

| [Da.2] setting value | Value set with the engineering tool (inch) | Value set with a program*1 (×10^-5 inch) |
|---|---|---|
| ABS Linear 1: 01H<br>ABS Linear 2: 0AH<br>ABS Linear 3: 15H<br>ABS Linear 4: 1AH<br>Current value changing: 81H | • Set the address<br>-21474.83648 to 21474.83647 | • Set the address<br>-2147483648 to 2147483647 |
| INC Linear 1: 02H<br>INC Linear 2: 0BH<br>INC Linear 3: 16H<br>INC Linear 4: 1BH<br>Fixed-feed 1: 03H<br>Fixed-feed 2: 0CH<br>Fixed-feed 3: 17H<br>Fixed-feed 4: 1CH | • Set the movement amount<br>-21474.83648 to 21474.83647 | • Set the movement amount<br>-2147483648 to 2147483647 |
| Forward run speed/position: 06H<br>Reverse run speed/position: 07H<br>Forward run position/speed: 08H<br>Reverse run position/speed: 09H | • Set the movement amount<br>0 to 21474.83647 | • Set the movement amount<br>0 to 2147483647 |
| ABS circular sub: 0DH<br>ABS circular right: 0FH<br>ABS circular left: 10H | • Set the address<br>-21474.83648 to 21474.83647 | • Set the address<br>-2147483648 to 2147483647 |
| INC circular sub: 0EH<br>INC circular right: 11H<br>INC circular left: 12H | • Set the movement amount<br>-21474.83648 to 21474.83647 | • Set the movement amount<br>-2147483648 to 2147483647 |

*1 Set an integer because the program cannot handle fractions.
(The value will be converted properly within the system.)

#### ■Buffer memory address (バッファメモリアドレス) (11.4 / original p.506)

Refer to the following for the buffer memory address in this area.
→Page 431 Positioning data

### [Da.7] Arc address (円弧アドレス) (11.4 / original p.506-507)

The arc address is data required only when carrying out 2-axis circular interpolation control.
- When carrying out circular interpolation with sub point designation, set the sub point (passing point) address as the arc address.
- When carrying out circular interpolation with center point designation, set the center point address of the arc as the arc address.

[Figure] Arc address (original p.506)
- <(1) Circular interpolation with sub point designation>: arc from the Start point address (Address before starting positioning) through the Sub point (Address set with [Da.7]) to the End point address (Address set with [Da.6]).
- <(2) Circular interpolation with center point designation>: arc from the Start point address (Address before starting positioning) to the End point address (Address set with [Da.6]) around the Center point address (Address set with [Da.7]).

When not carrying out 2-axis circular interpolation control, the value set in "[Da.7] Arc address" will be invalid.

#### ■When "[Pr.1] Unit setting" is "mm" ("[Pr.1]単位設定"が「mm」の場合) (11.4 / original p.507)

The table below lists the control methods that require the setting of the arc address and shows the setting range.
(With any control method excluded from the table below, the arc address does not need to be set.)

| [Da.2] setting value | Value set with the engineering tool (μm) | Value set with a program*1 (×10^-1 μm) |
|---|---|---|
| ABS circular sub: 0DH<br>ABS circular right: 0FH<br>ABS circular left: 10H | • Set the address<br>-214748364.8 to 214748364.7*2 | • Set the address<br>-2147483648 to 2147483647 |
| INC circular sub: 0EH<br>INC circular right: 11H<br>INC circular left: 12H | • Set the movement amount<br>-214748364.8 to 214748364.7*2 | • Set the movement amount<br>-2147483648 to 2147483647*2 |

*1 Set an integer because the program cannot handle fractions.
(The value will be converted properly within the system.)
*2 Note that the maximum radius that 2-axis circular interpolation control is possible is 536870912 (×10^-1 μm), although the setting value can be input within the range shown in the above table, as an arc address.

#### ■When "[Pr.1] Unit setting" is "degree" ("[Pr.1]単位設定"が「degree」の場合) (11.4 / original p.507)

No control method requires the setting of the arc address by "degree".

#### ■When "[Pr.1] Unit setting" is "pulse" ("[Pr.1]単位設定"が「pulse」の場合) (11.4 / original p.507)

The table below lists the control methods that require the setting of the arc address and shows the setting range.
(With any control method excluded from the table below, the arc address does not need to be set.)

| [Da.2] setting value | Value set with the engineering tool (pulse) | Value set with a program (pulse) |
|---|---|---|
| ABS circular sub: 0DH<br>ABS circular right: 0FH<br>ABS circular left: 10H | • Set the address<br>-2147483648 to 2147483647*1 | • Set the address<br>-2147483648 to 2147483647 |
| INC circular sub: 0EH<br>INC circular right: 11H<br>INC circular left: 12H | • Set the movement amount<br>-2147483648 to 2147483647*1 | • Set the movement amount<br>-2147483648 to 2147483647*1 |

*1 Note that the maximum radius that 2-axis circular interpolation control is possible is 536870912 (pulse), although the setting value can be input within the range shown in the above table, as an arc address.

#### ■When "[Pr.1] Unit setting" is "inch" ("[Pr.1]単位設定"が「inch」の場合) (11.4 / original p.507)

The table below lists the control methods that require the setting of the arc address and shows the setting range.
(With any control method excluded from the table below, the arc address does not need to be set.)

| [Da.2] setting value | Value set with the engineering tool (inch) | Value set with a program*1 (×10^-5 inch) |
|---|---|---|
| ABS circular sub: 0DH<br>ABS circular right: 0FH<br>ABS circular left: 10H | • Set the address<br>-21474.83648 to 21474.83647*2 | • Set the address<br>-2147483648 to 2147483647 |
| INC circular sub: 0EH<br>INC circular right: 11H<br>INC circular left: 12H | • Set the movement amount<br>-21474.83648 to 21474.83647*2 | • Set the movement amount<br>-2147483648 to 2147483647*2 |

*1 Set an integer because the program cannot handle fractions.
(The value will be converted properly within the system.)
*2 Note that the maximum radius that 2-axis circular interpolation control is possible is 536870912 (×10^-5 inch), although the setting value can be input within the range shown in the above table, as an arc address.

#### ■Buffer memory address (バッファメモリアドレス) (11.4 / original p.507)

Refer to the following for the buffer memory address in this area.
→Page 431 Positioning data
### [Da.8] Command speed (指令速度) (11.4 / original p.508)

Set the command speed for positioning.
- If the set command speed exceeds "[Pr.8] Speed limit value", positioning will be carried out at the speed limit value.
- If "-1" is set for the command speed, the current speed (speed set for previous positioning data No.) will be used for positioning control. Use the current speed for uniform speed control, etc. If "-1" is set for continuing positioning data, and the speed is changed, the following speed will also change.

Note that when starting positioning, if the "-1" speed is set for the positioning data that carries out positioning control first, the error "No command speed" (error code: 1A12H [FX5-SSC-S], or error code: 1B12H [FX5-SSC-G]) will occur, and the positioning will not start.
Refer to the following for details on the errors.
→Page 753 List of Error Codes

| [Pr.1] setting value | Value set with the engineering tool (unit) | Value set with a program (unit) |
|---|---|---|
| 0: mm | 0.01 to 20000000.00 (mm/min) | 1 to 2000000000 (×10^-2 mm/min) |
| 1: inch | 0.001 to 2000000.000 (inch/min) | 1 to 2000000000 (×10^-3 inch/min) |
| 2: degree | 0.001 to 2000000.000 (degree/min)*1 | 1 to 2000000000 (×10^-3 degree/min)*2 |
| 3: pulse | 1 to 1000000000 (pulse/s) | 1 to 1000000000 (pulse/s) |

*1 The range of command speed when "[Pr.83] Speed control 10 × multiplier setting for degree axis" is valid: 0.01 to 20000000.00 (degree/min)
*2 The range of command speed when "[Pr.83] Speed control 10 × multiplier setting for degree axis" is valid: 1 to 2000000000 (×10^-2 degree/min)

#### ■Buffer memory address (バッファメモリアドレス) (11.4 / original p.508)

Refer to the following for the buffer memory address in this area.
→Page 431 Positioning data

### [Da.9] Dwell time/JUMP destination positioning data No. (ドウェルタイム／JUMP先位置決めデータNo.) (11.4 / original p.508-509)

Set the "dwell time" or "positioning data No." corresponding to the "[Da.2] Control method".
- When a method other than "JUMP instruction" is set for "[Da.2] Control method": Set the "dwell time".
- When "JUMP instruction" is set for "[Da.2] Control method": Set the "positioning data No." for the JUMP destination.

When the "dwell time" is set, the setting details of the "dwell time" will be as follows according to "[Da.1] Operation pattern".

#### ■When "[Da.1] Operation pattern" in "00: Positioning complete" ("[Da.1]運転パターン"が「00: 位置決め終了」の場合) (11.4 / original p.508)

*(Note: "in" instead of "is" in this heading is as printed in the original.)*

- Set the time from when the positioning ends to when the "positioning complete signal" turns ON as the "dwell time".

[Figure] Dwell time with "00: Positioning complete" (original p.508)
- V/t chart: Positioning control (trapezoid) ends; after the time "[Da.9] Dwell time/JUMP destination positioning data No." elapses, the Positioning complete signal turns OFF → ON (it is drawn ON for a short time, then OFF again).

#### ■When "[Da.1] Operation pattern" is "01: Continuous positioning control" ("[Da.1]運転パターン"が「01: 連続位置決め制御」の場合) (11.4 / original p.508)

- Set the time from when positioning control ends to when the next positioning control starts as the "dwell time".

[Figure] Dwell time with "01: Continuous positioning control" (original p.508)
- V/t chart: Positioning control ends (speed 0); after the time "[Da.9] Dwell time/JUMP destination positioning data No." elapses, the Next positioning control starts.

#### ■When "[Da.1] Operation pattern" is "11: Continuous path control" ("[Da.1]運転パターン"が「11: 連続軌跡制御」の場合) (11.4 / original p.509)

- The setting value is irrelevant to the control. (The "dwell time" is 0 ms.)

[Figure] "11: Continuous path control" (original p.509)
- V/t chart: Positioning control changes directly to the Next positioning control without stopping. No dwell time (0 ms).

| [Da.2] setting value | Setting item | Value set with the engineering tool | Value set with a program*1 |
|---|---|---|---|
| JUMP instruction: 82H | Positioning data No. | 1 to 600 | 1 to 600 |
| Other than JUMP instruction | Dwell time | 0 to 65535 (ms) | 0 to 65535 (ms) |

*1 0 to 32767: Set as a decimal
32768 to 65535: Convert into hexadecimal and set

#### ■Buffer memory address (バッファメモリアドレス) (11.4 / original p.509)

Refer to the following for the buffer memory address in this area.
→Page 431 Positioning data

### [Da.10] M code/Condition data No./Number of LOOP to LEND repetitions (Mコード／条件データNo.／LOOP～LEND繰り返し回数) (11.4 / original p.509)

Set an "M code", a "condition data No.", or the "Number of LOOP to LEND repetitions" depending on how the "[Da.2] Control method" is set.*1
*1 The condition data specifies the condition for the JUMP instruction to be executed. (A JUMP will take place when the condition is satisfied.)

#### ■If a method other than "JUMP instruction" and "LOOP" is selected as the "[Da.2] Control method" ("[Da.2]制御方式"に「JUMP命令」「LOOP」以外を設定したとき) (11.4 / original p.509)

Set an "M code".
If no "M code" needs to be output, set "0" (default value).

#### ■If "JUMP instruction" or "LOOP" is selected as the "[Da.2] Control method" ("[Da.2]制御方式"に「JUMP命令」「LOOP」を設定したとき) (11.4 / original p.509)

Set the "condition data No." for JUMP.
- 0: Unconditional JUMP to the positioning data specified by "[Da.9] Dwell time/JUMP destination positioning data No.".
- 1 to 10: JUMP performed according to the condition data No. specified (a number between 1 and 10). Make sure that you specify the number of LOOP to LEND repetitions by a number other than "0". The error "Control method LOOP setting error" (error code: 1A33H [FX5-SSC-S], or error code: 1B33H [FX5-SSC-G]) will occur if you specify "0".

| [Da.2] setting value | Setting item | Value set with the engineering tool | Value set with a program*1 |
|---|---|---|---|
| JUMP instruction: 82H | Condition data No. | 0 to 10 | 0 to 10 |
| LOOP: 83H | Repetition count | 1 to 65535 | 1 to 65535 |
| Other than the above | M code | 0 to 65535 | 0 to 65535 |

*1 0 to 32767: Set as a decimal
32768 to 65535: Convert into hexadecimal and set

#### ■Buffer memory address (バッファメモリアドレス) (11.4 / original p.509)

Refer to the following for the buffer memory address in this area.
→Page 431 Positioning data

### [Da.20] Axis to be interpolated No.1 to [Da.22] Axis to be interpolated No.3 (補間対象軸番号1～補間対象軸番号3) (11.4 / original p.510)

Set the axis to be interpolated to execute the 2 to 4-axis interpolation operation.

| | |
|---|---|
| 2-axis interpolation | Set the target axis No. in "[Da.20] Axis to be interpolated No.1". |
| 3-axis interpolation | Set the target axis No. in "[Da.20] Axis to be interpolated No.1" and "[Da.21] Axis to be interpolated No.2". |
| 4-axis interpolation | Set the target axis No. in "[Da.20] Axis to be interpolated No.1" to "[Da.22] Axis to be interpolated No.3". |

*(The original table has no header row.)*

Set the axis set as axis to be interpolated.

| Setting value | Axis to be interpolated | Setting value | Axis to be interpolated |
|---|---|---|---|
| 0 | Axis 1 | 4 | Axis 5 |
| 1 | Axis 2 | 5 | Axis 6 |
| 2 | Axis 3 | 6 | Axis 7 |
| 3 | Axis 4 | 7 | Axis 8 |

> **Point**
> - Do not specify the own axis No. or the value outside the range. Otherwise, the error "Illegal interpolation description command" (error code: 1A22H [FX5-SSC-S], or error code: 1B22H [FX5-SSC-G]) will occur during the program execution.
> - When the same axis No. or axis No. of own axis is set to multiple axis to be interpolated No., the error "Illegal interpolation description command" (error code: 1A22H [FX5-SSC-S], or error code: 1B22H [FX5-SSC-G]) will occur during the program execution.)
> - Do not specify the axis to be interpolated No.2 and axis to be interpolated No.3 for 2-axis interpolation, and do not specify the axis to be interpolated No.3 for 3-axis interpolation. The setting value is ignored.

*(Note: the unmatched ")" at the end of the second item is as printed in the original.)*

#### ■Buffer memory address (バッファメモリアドレス) (11.4 / original p.510)

Refer to the following for the buffer memory address in this area.
→Page 431 Positioning data

## 11.5 Block Start Data (ブロック始動データ) (11.5 / original p.511-513)

Before explaining the block start data setting items [Da.11] to [Da.14], the configuration of the block start data is shown below.
The block start data stored in the buffer memory of the Simple Motion module/Motion module is the following configuration.

[Figure] Configuration of the block start data in the buffer memory (original p.511)
- n: Axis No. - 1. Start block 0 of each axis, points 1st to 50th:

| Point | Setting item | Buffer memory address |
|---|---|---|
| 1st point | [Da.11] Shape / [Da.12] Start data No. (bit layout drawn: b15 to b8 / b7 to b0; see the bit layout under the setting table below) | 22000+400n |
| 1st point | [Da.13] Special start instruction / [Da.14] Parameter (b15 to b8 / b7 to b0) | 22050+400n |
| 2nd point | [Da.11], [Da.12] | 22001+400n |
| 2nd point | [Da.13], [Da.14] | 22051+400n |
| 50th point | [Da.11], [Da.12] | 22049+400n |
| 50th point | [Da.13], [Da.14] | 22099+400n |

- ● Up to 50 block start data points can be set (stored) for each axis in the buffer memory addresses shown on the left.
- ● Items in a single unit of block start data are shown included in a bold frame.
- ● Each axis has five start blocks (block Nos. 0 to 4). Start block 2 to 4 are not allocated to buffer memory. Set with the engineering tool.

The following explains the block start data setting items [Da.11] to [Da.14]. (The buffer memory addresses shown are those of the "1st point block start data (block No.7000)".)

> **Point**
> - To perform a high-level positioning control using block start data, set a number between 7000 and 7004 to the "[Cd.3] Positioning start No." and use the "[Cd.4] Positioning starting point No." to specify a point number between 1 and 50, a position counted from the beginning of the block.
> - The number between 7000 and 7004 specified here is called the "block No.".
> - With the Simple Motion module/Motion module, up to 50 "block start data" points and up to 10 "condition data" items can be assigned to each "block No.".

| Block No.*1 | Axis | Block start data | Condition | Buffer memory | Engineering tool |
|---|---|---|---|---|---|
| 7000 | Axis 1 | Start block 0 | Condition data (1 to 10) | Supports the settings | Supports the settings |
| 7000 | ⋮ | Start block 0 | ⋮ | Supports the settings | Supports the settings |
| 7000 | Maximum control axis No. | Start block 0 | Condition data (1 to 10) | Supports the settings | Supports the settings |
| 7001 | Axis 1 | Start block 1 | Condition data (1 to 10) | Supports the settings | Supports the settings |
| 7001 | ⋮ | Start block 1 | ⋮ | Supports the settings | Supports the settings |
| 7001 | Maximum control axis No. | Start block 1 | Condition data (1 to 10) | Supports the settings | Supports the settings |
| 7002 | Axis 1 | Start block 2 | Condition data (1 to 10) | — | Supports the settings |
| 7002 | ⋮ | Start block 2 | ⋮ | — | Supports the settings |
| 7002 | Maximum control axis No. | Start block 2 | Condition data (1 to 10) | — | Supports the settings |
| 7003 | Axis 1 | Start block 3 | Condition data (1 to 10) | — | Supports the settings |
| 7003 | ⋮ | Start block 3 | ⋮ | — | Supports the settings |
| 7003 | Maximum control axis No. | Start block 3 | Condition data (1 to 10) | — | Supports the settings |
| 7004 | Axis 1 | Start block 4 | Condition data (1 to 10) | — | Supports the settings |
| 7004 | ⋮ | Start block 4 | ⋮ | — | Supports the settings |
| 7004 | Maximum control axis No. | Start block 4 | Condition data (1 to 10) | — | Supports the settings |

*In the original, each Block No. and "Start block" cell is merged over its 3 rows (Axis 1 / ⋮ / Maximum control axis No.). "Supports the settings" in the Buffer memory column is merged over block Nos. 7000 and 7001, and "—" over 7002 to 7004. "Supports the settings" in the Engineering tool column is merged over all rows. Expanded to each row.*

*1 Setting cannot be made when the "Pre-reading start function" is used. If you set any of Nos. 7000 to 7004 and perform the Pre-reading start function, the error "Outside start No. range" (error code: 19A3H [FX5-SSC-S], or error code: 1AA3H [FX5-SSC-G])" will occur.
Refer to the following for details.
→Page 276 Pre-reading start function

*(Note: the unmatched quotation mark after "1AA3H [FX5-SSC-G])" is as printed in the original.)*

n: Axis No. - 1

| Item | | Value set with the engineering tool | Value set with a program | Default value | Buffer memory address |
|---|---|---|---|---|---|
| [Da.11] | Shape | 0: End | 0 | 0000H | 22000+400n |
| [Da.11] | Shape | 1: Continue | 1 | 0000H | 22000+400n |
| [Da.12] | Start data No. | Positioning data No: 1 to 600<br>(01H to 258H) | 01H<br>to<br>258H | 0000H | 22000+400n |
| [Da.13] | Special start instruction | 0: Block start (normal start) | 00H | 0000H | 22050+400n |
| [Da.13] | Special start instruction | 1: Condition start | 01H | 0000H | 22050+400n |
| [Da.13] | Special start instruction | 2: Wait start | 02H | 0000H | 22050+400n |
| [Da.13] | Special start instruction | 3: Simultaneous start | 03H | 0000H | 22050+400n |
| [Da.13] | Special start instruction | 4: FOR loop | 04H | 0000H | 22050+400n |
| [Da.13] | Special start instruction | 5: FOR condition | 05H | 0000H | 22050+400n |
| [Da.13] | Special start instruction | 6: NEXT start | 06H | 0000H | 22050+400n |
| [Da.14] | Parameter | Condition data No.: 1 to 10 (01H to 0AH)<br>Number of repetitions: 0 to 255 (00H to FFH) | 00H<br>to<br>FFH | 0000H | 22050+400n |

*In the original, the header "Setting value" spans the two columns "Value set with the engineering tool" / "Value set with a program". The Item cells of [Da.11] and [Da.13] are merged over their rows. Default value "0000H" and Buffer memory address "22000+400n" are merged over [Da.11] and [Da.12]; "0000H" and "22050+400n" over [Da.13] and [Da.14]. Expanded to each row.*

Figures inside the "Value set with a program" column of the original:
- [Da.11]/[Da.12] (22000+400n): b15 = [Da.11]; b14 to b12 = 0, 0, 0; b11 to b0 = [Da.12].
- [Da.13]/[Da.14] (22050+400n): b15 to b8 = [Da.13]; b7 to b0 = [Da.14].

### [Da.11] Shape (形態) (11.5 / original p.512)

Set whether to carry out only the local "block start data" and then end control, or to execute the "block start data" set in the next point.

| Setting value | Setting details |
|---|---|
| 0: End | Execute the designated point's "block start data", and then complete the control. |
| 1: Continue | Execute the designated point's "block start data", and after completing control, execute the next point's "block start data". |

#### ■Buffer memory address (バッファメモリアドレス) (11.5 / original p.512)

Refer to the following for the buffer memory address in this area.
→Page 432 Positioning data (Block start data)

### [Da.12] Start data No. (始動データNo.) (11.5 / original p.512)

Set the "positioning data No." designated with the "block start data".

#### ■Buffer memory address (バッファメモリアドレス) (11.5 / original p.512)

Refer to the following for the buffer memory address in this area.
→Page 432 Positioning data (Block start data)

### [Da.13] Special start instruction (特殊始動命令) (11.5 / original p.513)

Set the "special start instruction" for using "high-level positioning control". (Set how to start the positioning data set in "[Da.12] Start data No.".)

| Setting value | Setting details |
|---|---|
| 00H: Block start (Normal start) | Execute the random block positioning data in the set order with one start. |
| 01H: Condition start | Carry out the condition judgment set in "condition data" for the designated positioning data, and when the conditions are established, execute the "block start data". If not established, ignore that "block start data", and then execute the next point's "block start data". |
| 02H: Wait start | Carry out the condition judgment set in "condition data" for the designated positioning data, and when the conditions are established, execute the "block start data". If not established, stop the control (wait) until the conditions are established. |
| 03H: Simultaneous start | Simultaneous execute (output command at same timing) the positioning data with the No. designated for the axis designated in the "condition data". Up to four axes can start simultaneously. |
| 04H: Repeated start (FOR loop) | Repeat the program from the block start data with the "FOR loop" to the block start data with "NEXT" for the designated number of times. |
| 05H: Repeated start (FOR condition) | Repeat the program from the block start data with the "FOR condition" to the block start data with "NEXT" until the conditions set in the "condition data" are established. |
| 06H: NEXT start | Set the end of the repetition when "04H: Repetition start (FOR loop)" or "05H: Repetition start (FOR condition)" is set. |

Refer to the following for details on the control.
→Page 137 HIGH-LEVEL POSITIONING CONTROL

#### ■Buffer memory address (バッファメモリアドレス) (11.5 / original p.513)

Refer to the following for the buffer memory address in this area.
→Page 432 Positioning data (Block start data)

### [Da.14] Parameter (パラメータ) (11.5 / original p.513)

Set the value as required for "[Da.13] Special start instruction".

| [Da.13] Special start instruction | Setting value | Setting details |
|---|---|---|
| Block start (Normal start) | — | Not used. (There is no need to set.) |
| Condition start | 1 to 10 | Set the condition data No. (Data No. of "condition data" is set up for the condition judgment.) (Refer to →Page 512 Condition Data for details on the condition data.) |
| Wait start | 1 to 10 | Set the condition data No. (Data No. of "condition data" is set up for the condition judgment.) (Refer to →Page 512 Condition Data for details on the condition data.) |
| Simultaneous start | 1 to 10 | Set the condition data No. (Data No. of "condition data" is set up for the condition judgment.) (Refer to →Page 512 Condition Data for details on the condition data.) |
| Repeated start (FOR loop) | 0 to 255 | Set the number of repetitions. |
| Repeated start (FOR condition) | 1 to 10 | Set the condition data No. (Data No. of "condition data" is set up for the condition judgment.) |

*In the original, "1 to 10" and the Setting details cell are merged over the 3 rows Condition start / Wait start / Simultaneous start. Expanded to each row.*

#### ■Buffer memory address (バッファメモリアドレス) (11.5 / original p.513)

Refer to the following for the buffer memory address in this area.
→Page 432 Positioning data (Block start data)
## 11.6 Condition Data (条件データ) (11.6 / original p.514-519)

Before explaining the condition data setting items [Da.15] to [Da.19] and [Da.23] to [Da.26], the configuration of the condition data is shown below.
The condition data stored in the buffer memory of the Simple Motion module/Motion module is the following configuration.

[Figure] Configuration of the condition data in the buffer memory (original p.514)
- n: Axis No. - 1. Start block 0 of each axis, Condition data No.1 to No.10:

| Setting item | No.1 | No.2 | No.10 |
|---|---|---|---|
| b15-b8: [Da.16] Condition operator / b7-b0: [Da.15] Condition target | 22100+400n | 22110+400n | 22190+400n |
| [Da.17] Address | 22102+400n<br>22103+400n | 22112+400n<br>22113+400n | 22192+400n<br>22193+400n |
| [Da.18] Parameter 1 | 22104+400n<br>22105+400n | 22114+400n<br>22115+400n | 22194+400n<br>22195+400n |
| [Da.19] Parameter 2 | 22106+400n<br>22107+400n | 22116+400n<br>22117+400n | 22196+400n<br>22197+400n |
| b15-b8: [Da.25] Simultaneously starting axis No.2 / b7-b0: [Da.24] Simultaneously starting axis No.1<br>b31-b24: [Da.23] Number of simultaneously starting axes / b23-b16: [Da.26] Simultaneously starting axis No.3 | 22108+400n<br>22109+400n | 22118+400n<br>22119+400n | 22198+400n<br>22199+400n |

- ● Up to 10 condition data points can be set (stored) for each block No. in the buffer memory addresses shown on the left.
- ● Items in a single unit of condition data are shown included in a bold frame.
- ● Each axis has five start blocks (block Nos. 0 to 4). Start block 2 to 4 are not allocated to buffer memory. Set with the engineering tool.

The following explains the condition data setting items [Da.15] to [Da.19] and [Da.23] to [Da.26]. (The buffer memory addresses shown are those of the "condition data No.1 (block No.7000)".)

> **Point**
> - To perform a high-level positioning control using block start data, set a number between 7000 and 7004 to the "[Cd.3] Positioning start No." and use the "[Cd.4] Positioning starting point No." to specify a point No. between 1 and 50, a position counted from the beginning of the block.
> - The number between 7000 and 7004 specified here is called the "block No.".
> - With the Simple Motion module/Motion module, up to 50 "block start data" points and up to 10 "condition data" items can be assigned to each "block No.".

| Block No.*1 | Axis | Block start data | Condition | Buffer memory | Engineering tool |
|---|---|---|---|---|---|
| 7000 | Axis 1 | Start block 0 | Condition data (1 to 10) | Supports the settings | Supports the settings |
| 7000 | ⋮ | Start block 0 | ⋮ | Supports the settings | Supports the settings |
| 7000 | Maximum control axis No. | Start block 0 | Condition data (1 to 10) | Supports the settings | Supports the settings |
| 7001 | Axis 1 | Start block 1 | Condition data (1 to 10) | Supports the settings | Supports the settings |
| 7001 | ⋮ | Start block 1 | ⋮ | Supports the settings | Supports the settings |
| 7001 | Maximum control axis No. | Start block 1 | Condition data (1 to 10) | Supports the settings | Supports the settings |
| 7002 | Axis 1 | Start block 2 | Condition data (1 to 10) | — | Supports the settings |
| 7002 | ⋮ | Start block 2 | ⋮ | — | Supports the settings |
| 7002 | Maximum control axis No. | Start block 2 | Condition data (1 to 10) | — | Supports the settings |
| 7003 | Axis 1 | Start block 3 | Condition data (1 to 10) | — | Supports the settings |
| 7003 | ⋮ | Start block 3 | ⋮ | — | Supports the settings |
| 7003 | Maximum control axis No. | Start block 3 | Condition data (1 to 10) | — | Supports the settings |
| 7004 | Axis 1 | Start block 4 | Condition data (1 to 10) | — | Supports the settings |
| 7004 | ⋮ | Start block 4 | ⋮ | — | Supports the settings |
| 7004 | Maximum control axis No. | Start block 4 | Condition data (1 to 10) | — | Supports the settings |

*In the original, each Block No. and "Start block" cell is merged over its 3 rows (Axis 1 / ⋮ / Maximum control axis No.). "Supports the settings" in the Buffer memory column is merged over block Nos. 7000 and 7001, and "—" over 7002 to 7004. "Supports the settings" in the Engineering tool column is merged over all rows. Expanded to each row.*

*1 Setting cannot be made when the "Pre-reading start function" is used. If you set any of Nos. 7000 to 7004 and perform the Pre-reading start function, the error "Outside start No. range" (error code: 19A3H [FX5-SSC-S], or error code: 1AA3H [FX5-SSC-G]) will occur.
Refer to the following for details.
→Page 276 Pre-reading start function

n: Axis No. - 1

| Item | | Value set with the engineering tool | Value set with a program | Default value | Buffer memory address |
|---|---|---|---|---|---|
| Condition identifier | [Da.15] Condition target | 01: Monitor data ([Md.140], [Md.141]) | 01H | 0000H | 22100+400n |
| Condition identifier | [Da.15] Condition target | 02: Control data ([Cd.184], [Cd.190], [Cd.191]) | 02H | 0000H | 22100+400n |
| Condition identifier | [Da.15] Condition target | 03: Buffer memory (1-word) | 03H | 0000H | 22100+400n |
| Condition identifier | [Da.15] Condition target | 04: Buffer memory (2-word) | 04H | 0000H | 22100+400n |
| Condition identifier | [Da.15] Condition target | 05: Positioning data No. | 05H | 0000H | 22100+400n |
| Condition identifier | [Da.16] Condition operator | 01: ** = P1 | 01H | 0000H | 22100+400n |
| Condition identifier | [Da.16] Condition operator | 02: ** ≠ P1 | 02H | 0000H | 22100+400n |
| Condition identifier | [Da.16] Condition operator | 03: ** ≤ P1 | 03H | 0000H | 22100+400n |
| Condition identifier | [Da.16] Condition operator | 04: ** ≥ P1 | 04H | 0000H | 22100+400n |
| Condition identifier | [Da.16] Condition operator | 05: P1 ≤ ** ≤ P2 | 05H | 0000H | 22100+400n |
| Condition identifier | [Da.16] Condition operator | 06: ** ≤ P1, P2 ≤ ** | 06H | 0000H | 22100+400n |
| Condition identifier | [Da.16] Condition operator | 07: SIG = ON | 07H | 0000H | 22100+400n |
| Condition identifier | [Da.16] Condition operator | 08: SIG = OFF | 08H | 0000H | 22100+400n |
| [Da.17] | Address | Buffer memory address | (see figure below) | 0000H | 22102+400n<br>22103+400n |
| [Da.18] | Parameter 1 | Value | (see figure below) | 0000H | 22104+400n<br>22105+400n |
| [Da.19] | Parameter 2 | Value | (see figure below) | 0000H | 22106+400n<br>22107+400n |
| Simultaneously starting axis | [Da.23] Number of simultaneously starting axes | 2: 2 axes | 2H | 0000H | 22108+400n<br>22109+400n |
| Simultaneously starting axis | [Da.23] Number of simultaneously starting axes | 3: 3 axes | 3H | 0000H | 22108+400n<br>22109+400n |
| Simultaneously starting axis | [Da.23] Number of simultaneously starting axes | 4: 4 axes | 4H | 0000H | 22108+400n<br>22109+400n |
| Simultaneously starting axis | [Da.24] Simultaneously starting axis No.1 | 0: Axis 1 selected | 0H | 0000H | 22108+400n<br>22109+400n |
| Simultaneously starting axis | [Da.24] Simultaneously starting axis No.1 | 1: Axis 2 selected | 1H | 0000H | 22108+400n<br>22109+400n |
| Simultaneously starting axis | [Da.24] Simultaneously starting axis No.1 | 2: Axis 3 selected | 2H | 0000H | 22108+400n<br>22109+400n |
| Simultaneously starting axis | [Da.24] Simultaneously starting axis No.1 | 3: Axis 4 selected | 3H | 0000H | 22108+400n<br>22109+400n |
| Simultaneously starting axis | [Da.24] Simultaneously starting axis No.1 | 4: Axis 5 selected | 4H | 0000H | 22108+400n<br>22109+400n |
| Simultaneously starting axis | [Da.24] Simultaneously starting axis No.1 | 5: Axis 6 selected | 5H | 0000H | 22108+400n<br>22109+400n |
| Simultaneously starting axis | [Da.24] Simultaneously starting axis No.1 | 6: Axis 7 selected | 6H | 0000H | 22108+400n<br>22109+400n |
| Simultaneously starting axis | [Da.24] Simultaneously starting axis No.1 | 7: Axis 8 selected | 7H | 0000H | 22108+400n<br>22109+400n |
| Simultaneously starting axis | [Da.25] Simultaneously starting axis No.2 | 0: Axis 1 selected | 0H | 0000H | 22108+400n<br>22109+400n |
| Simultaneously starting axis | [Da.25] Simultaneously starting axis No.2 | 1: Axis 2 selected | 1H | 0000H | 22108+400n<br>22109+400n |
| Simultaneously starting axis | [Da.25] Simultaneously starting axis No.2 | 2: Axis 3 selected | 2H | 0000H | 22108+400n<br>22109+400n |
| Simultaneously starting axis | [Da.25] Simultaneously starting axis No.2 | 3: Axis 4 selected | 3H | 0000H | 22108+400n<br>22109+400n |
| Simultaneously starting axis | [Da.25] Simultaneously starting axis No.2 | 4: Axis 5 selected | 4H | 0000H | 22108+400n<br>22109+400n |
| Simultaneously starting axis | [Da.25] Simultaneously starting axis No.2 | 5: Axis 6 selected | 5H | 0000H | 22108+400n<br>22109+400n |
| Simultaneously starting axis | [Da.25] Simultaneously starting axis No.2 | 6: Axis 7 selected | 6H | 0000H | 22108+400n<br>22109+400n |
| Simultaneously starting axis | [Da.25] Simultaneously starting axis No.2 | 7: Axis 8 selected | 7H | 0000H | 22108+400n<br>22109+400n |
| Simultaneously starting axis | [Da.26] Simultaneously starting axis No.3 | 0: Axis 1 selected | 0H | 0000H | 22108+400n<br>22109+400n |
| Simultaneously starting axis | [Da.26] Simultaneously starting axis No.3 | 1: Axis 2 selected | 1H | 0000H | 22108+400n<br>22109+400n |
| Simultaneously starting axis | [Da.26] Simultaneously starting axis No.3 | 2: Axis 3 selected | 2H | 0000H | 22108+400n<br>22109+400n |
| Simultaneously starting axis | [Da.26] Simultaneously starting axis No.3 | 3: Axis 4 selected | 3H | 0000H | 22108+400n<br>22109+400n |
| Simultaneously starting axis | [Da.26] Simultaneously starting axis No.3 | 4: Axis 5 selected | 4H | 0000H | 22108+400n<br>22109+400n |
| Simultaneously starting axis | [Da.26] Simultaneously starting axis No.3 | 5: Axis 6 selected | 5H | 0000H | 22108+400n<br>22109+400n |
| Simultaneously starting axis | [Da.26] Simultaneously starting axis No.3 | 6: Axis 7 selected | 6H | 0000H | 22108+400n<br>22109+400n |
| Simultaneously starting axis | [Da.26] Simultaneously starting axis No.3 | 7: Axis 8 selected | 7H | 0000H | 22108+400n<br>22109+400n |

*In the original, the header "Setting value" spans the two columns "Value set with the engineering tool" / "Value set with a program". "Condition identifier" is merged over [Da.15] and [Da.16] (13 rows), and "Simultaneously starting axis" over [Da.23] to [Da.26]. Default value "0000H" and Buffer memory address "22100+400n" are merged over [Da.15] and [Da.16]; "0000H" and "22108+400n, 22109+400n" over [Da.23] to [Da.26]. The setting value list "0: Axis 1 selected" to "7: Axis 8 selected" / "0H" to "7H" is one cell merged over [Da.24] to [Da.26]. Expanded to each row.*

Figures inside the "Value set with a program" column of the original:
- [Da.15]/[Da.16] (22100+400n): b15 to b8 = [Da.16] Condition operator; b7 to b0 = [Da.15] Condition target.
- [Da.17]: Example) 22103 (High-order) b31 to b16 / 22102 (Low-order) b15 to b0 = Buffer memory address.
- [Da.18]: Example) 22105 (High-order) b31 to b16 / 22104 (Low-order) b15 to b0 = Value.
- [Da.19]: Example) 22107 (High-order) b31 to b16 / 22106 (Low-order) b15 to b0 = Value.
- [Da.23] to [Da.26] (22108+400n, 22109+400n): b7 to b0 = [Da.24], b15 to b8 = [Da.25]; b23 to b16 = [Da.26], b31 to b24 = [Da.23].

### [Da.15] Condition target (条件対象) (11.6 / original p.517)

Set the condition target as required for each control.

| Setting value | Setting details |
|---|---|
| 01H: Monitor data ([Md.140], [Md.141]) | Set the state (ON/OFF) of each signal as a condition. |
| 02H: Control data ([Cd.184], [Cd.190], [Cd.191]) | Set the state (ON/OFF) of each signal as a condition. |
| 03H: Buffer memory (1-word) | Set the value stored in the buffer memory as a condition.<br>03H: The target buffer memory is "1-word (16 bits)"<br>04H: The target buffer memory is "2-word (32 bits)" |
| 04H: Buffer memory (2-word) | Set the value stored in the buffer memory as a condition.<br>03H: The target buffer memory is "1-word (16 bits)"<br>04H: The target buffer memory is "2-word (32 bits)" |
| 05H: Positioning data No. | Select only for "simultaneous start". |

*In the original, the Setting details cells are merged over 01H/02H and over 03H/04H. Expanded to each row.*

#### ■Buffer memory address (バッファメモリアドレス) (11.6 / original p.517)

Refer to the following for the buffer memory address in this area.
→Page 432 Positioning data (Block start data)

### [Da.16] Condition operator (条件演算子) (11.6 / original p.517)

Set the condition operator as required for the "[Da.15] Condition target".

| [Da.15] Condition target | Setting value | Setting details |
|---|---|---|
| 01H: Monitor data ([Md.140], [Md.141])<br>02H: Control data ([Cd.184], [Cd.190], [Cd.191]) | 07H: SIG= ON | When the state (ON/OFF) of each signal is set as a condition, select ON or OFF as the trigger. |
| 01H: Monitor data ([Md.140], [Md.141])<br>02H: Control data ([Cd.184], [Cd.190], [Cd.191]) | 08H: SIG = OFF | When the state (ON/OFF) of each signal is set as a condition, select ON or OFF as the trigger. |
| 03H: Buffer memory (1-word)<br>04H: Buffer memory (2-word) | 01H: ** = P1 | Select how to use the value (**) in the buffer memory as a part of the condition. |
| 03H: Buffer memory (1-word)<br>04H: Buffer memory (2-word) | 02H: ** ≠ P1 | Select how to use the value (**) in the buffer memory as a part of the condition. |
| 03H: Buffer memory (1-word)<br>04H: Buffer memory (2-word) | 03H: ** ≤ P1 | Select how to use the value (**) in the buffer memory as a part of the condition. |
| 03H: Buffer memory (1-word)<br>04H: Buffer memory (2-word) | 04H: ** ≥ P1 | Select how to use the value (**) in the buffer memory as a part of the condition. |
| 03H: Buffer memory (1-word)<br>04H: Buffer memory (2-word) | 05H: P1 ≤ ** ≤ P2 | Select how to use the value (**) in the buffer memory as a part of the condition. |
| 03H: Buffer memory (1-word)<br>04H: Buffer memory (2-word) | 06H: ** ≤ P1, P2 ≤ ** | Select how to use the value (**) in the buffer memory as a part of the condition. |

*In the original, the [Da.15] Condition target cells and the Setting details cells are merged over their rows (07H/08H, and 01H to 06H). Expanded to each row.*

#### ■Buffer memory address (バッファメモリアドレス) (11.6 / original p.517)

Refer to the following for the buffer memory address in this area.
→Page 432 Positioning data (Block start data)

### [Da.17] Address (アドレス) (11.6 / original p.517)

Set the address as required for the "[Da.15] Condition target".

| [Da.15] Condition target | Setting value | Setting details |
|---|---|---|
| 01H: Monitor data ([Md.140], [Md.141]) | — | Not used. (There is no need to set.) |
| 02H: Control data ([Cd.184], [Cd.190], [Cd.191]) | — | Not used. (There is no need to set.) |
| 03H: Buffer memory (1-word) | Value (Buffer memory address)*1 | Set the target "buffer memory address". (For 2 words, set the low-order buffer memory address.) |
| 04H: Buffer memory (2-word) | Value (Buffer memory address)*1 | Set the target "buffer memory address". (For 2 words, set the low-order buffer memory address.) |
| 05H: Positioning data No. | — | Not used. (There is no need to set.) |

*In the original, the Setting value and Setting details cells are merged over 01H/02H and over 03H/04H. Expanded to each row.*

*1 The setting range of the buffer memory address at specifying buffer memory is as follows.

| [Da.15] Condition target | Buffer memory address range |
|---|---|
| 03H: Buffer memory (1-word) | 0 to 98303 |
| 04H: Buffer memory (2-word) | 0 to 98302 |

#### ■Buffer memory address (バッファメモリアドレス) (11.6 / original p.517)

Refer to the following for the buffer memory address in this area.
→Page 432 Positioning data (Block start data)

### [Da.18] Parameter 1 (パラメータ1) (11.6 / original p.518)

Set the parameters as required for the "[Da.16] Condition operator" and "[Da.23] Number of simultaneously starting axes".

| [Da.16] Condition operator | [Da.23] Number of simultaneously starting axes | Setting value | Setting details |
|---|---|---|---|
| 01H: ** = P1 | — | Value | The value of P1 should be equal to or smaller than the value of P2. (P1 ≤ P2)<br>If P1 is greater than P2 (P1 > P2), the error "Condition data error" (error code: 1A00H [FX5-SSC-S], or error codes: 1B00H to 1B0FH [FX5-SSC-G]) will occur. |
| 02H: ** ≠ P1 | — | Value | The value of P1 should be equal to or smaller than the value of P2. (P1 ≤ P2)<br>If P1 is greater than P2 (P1 > P2), the error "Condition data error" (error code: 1A00H [FX5-SSC-S], or error codes: 1B00H to 1B0FH [FX5-SSC-G]) will occur. |
| 03H: ** ≤ P1 | — | Value | The value of P1 should be equal to or smaller than the value of P2. (P1 ≤ P2)<br>If P1 is greater than P2 (P1 > P2), the error "Condition data error" (error code: 1A00H [FX5-SSC-S], or error codes: 1B00H to 1B0FH [FX5-SSC-G]) will occur. |
| 04H: ** ≥ P1 | — | Value | The value of P1 should be equal to or smaller than the value of P2. (P1 ≤ P2)<br>If P1 is greater than P2 (P1 > P2), the error "Condition data error" (error code: 1A00H [FX5-SSC-S], or error codes: 1B00H to 1B0FH [FX5-SSC-G]) will occur. |
| 05H: P1 ≤ ** ≤ P2 | — | Value | The value of P1 should be equal to or smaller than the value of P2. (P1 ≤ P2)<br>If P1 is greater than P2 (P1 > P2), the error "Condition data error" (error code: 1A00H [FX5-SSC-S], or error codes: 1B00H to 1B0FH [FX5-SSC-G]) will occur. |
| 06H: ** ≤ P1, P2 ≤ ** | — | Value | The value of P1 should be equal to or smaller than the value of P2. (P1 ≤ P2)<br>If P1 is greater than P2 (P1 > P2), the error "Condition data error" (error code: 1A00H [FX5-SSC-S], or error codes: 1B00H to 1B0FH [FX5-SSC-G]) will occur. |
| 07H: SIG = ON | — | Value<br>(bit No.) | Set the bit No. of each signal.<br>Monitor data: 0H (READY ([Md.140] Module status: b0)), 1H (Synchronization flag ([Md.140] Module status: b1)), 10H to 17H (BUSY axis-1 to axis-8 ([Md.141] BUSY))<br>Control data: 0H (PLC READY ([Cd.190] PLC READY)), 1H (All axis servo ON ([Cd.191] All axis servo ON)), 10H to 17H (Positioning start axis axis-1 to axis-8 ([Cd.184] Positioning start)) |
| 08H: SIG = OFF | — | Value<br>(bit No.) | Set the bit No. of each signal.<br>Monitor data: 0H (READY ([Md.140] Module status: b0)), 1H (Synchronization flag ([Md.140] Module status: b1)), 10H to 17H (BUSY axis-1 to axis-8 ([Md.141] BUSY))<br>Control data: 0H (PLC READY ([Cd.190] PLC READY)), 1H (All axis servo ON ([Cd.191] All axis servo ON)), 10H to 17H (Positioning start axis axis-1 to axis-8 ([Cd.184] Positioning start)) |
| — | 2 to 4 | Value<br>(positioning data No.) | Set the positioning data No. for starting axis set in "[Da.24] Simultaneously starting axis No.1" and/or "[Da.25] Simultaneously starting axis No.2".<br>Low-order 16-bit: Simultaneously starting axis No.1 positioning data No.1 to 600 (01H to 258H)<br>High-order 16-bit: Simultaneously starting axis No.2 positioning data No.1 to 600 (01H to 258H) |

*In the original, "—" in the [Da.23] column is merged over 01H to 08H; "Value" and its Setting details over 01H to 06H; "Value (bit No.)" and its Setting details over 07H/08H. Expanded to each row.*

#### ■Buffer memory address (バッファメモリアドレス) (11.6 / original p.518)

Refer to the following for the buffer memory address in this area.
→Page 432 Positioning data (Block start data)

### [Da.19] Parameter 2 (パラメータ2) (11.6 / original p.518)

Set the parameters as required for the "[Da.16] Condition operator" and "[Da.23] Number of simultaneously starting axes".

| [Da.16] Condition operator | [Da.23] Number of simultaneously starting axes | Setting value | Setting details |
|---|---|---|---|
| 01H: ** = P1 | — | — | Not used. (No need to be set.) |
| 02H: ** ≠ P1 | — | — | Not used. (No need to be set.) |
| 03H: ** ≤ P1 | — | — | Not used. (No need to be set.) |
| 04H: ** ≥ P1 | — | — | Not used. (No need to be set.) |
| 05H: P1 ≤ ** ≤ P2 | — | Value | The value of P2 should be equal to or greater than the value of P1. (P1 ≤ P2)<br>If P1 is greater than P2 (P1 > P2), the error "Condition data error" (error code: 1A00H [FX5-SSC-S], or error codes: 1B00H to 1B0FH [FX5-SSC-G]) will occur. |
| 06H: ** ≤ P1, P2 ≤ ** | — | Value | The value of P2 should be equal to or greater than the value of P1. (P1 ≤ P2)<br>If P1 is greater than P2 (P1 > P2), the error "Condition data error" (error code: 1A00H [FX5-SSC-S], or error codes: 1B00H to 1B0FH [FX5-SSC-G]) will occur. |
| 07H: SIG = ON | — | — | Not used. (No need to be set.) |
| 08H: SIG = OFF | — | — | Not used. (No need to be set.) |
| — | 2 to 3 | — | Not used. (No need to be set.) |
| — | 4 | Value<br>(positioning data No.) | Set the positioning data No. for starting axis set in "[Da.26] Simultaneously starting axis No.3"<br>Low-order 16-bit: Simultaneously starting axis No.3 positioning data No.1 to 600 (01H to 258H)<br>High-order 16-bit: Not used (Set "0") |

*In the original, "—" in the [Da.23] column is merged over 01H to 08H; "—" / "Not used. (No need to be set.)" over 01H to 04H; "Value" and its Setting details over 05H/06H; "—" / "Not used. (No need to be set.)" over 07H, 08H and "— / 2 to 3"; "—" in the [Da.16] column over the rows "2 to 3" and "4". Expanded to each row.*

#### ■Buffer memory address (バッファメモリアドレス) (11.6 / original p.518)

Refer to the following for the buffer memory address in this area.
→Page 432 Positioning data (Block start data)

### [Da.23] Number of simultaneously starting axes (同時始動軸数) (11.6 / original p.519)

Set the number of simultaneously starting axes to execute the simultaneous start.

| Number of axes | Details |
|---|---|
| 2 | Simultaneous start by 2 axes of the starting axis and axis set in "[Da.24] Simultaneously starting axis No.1". |
| 3 | Simultaneous start by 3 axes of the starting axis and axis set in "[Da.24] Simultaneously starting axis No.1" and "[Da.25] Simultaneously starting axis No.2". |
| 4 | Simultaneous start by 4 axes of the starting axis and axis set in "[Da.24] Simultaneously starting axis No.1" to "[Da.26] Simultaneously starting axis No.3". |

#### ■Buffer memory address (バッファメモリアドレス) (11.6 / original p.519)

Refer to the following for the buffer memory address in this area.
→Page 432 Positioning data (Block start data)

### [Da.24] Simultaneously starting axis No.1 to [Da.26] Simultaneously starting axis No.3 (同時始動対象軸番号1～同時始動対象軸番号3) (11.6 / original p.519)

Set the simultaneously starting axis to execute the 2 to 4-axis simultaneous start.

| Simultaneously starting axis | Details |
|---|---|
| 2-axis interpolation | Set the target axis No. in "[Da.24] Simultaneously starting axis No.1". |
| 3-axis interpolation | Set the target axis No. in "[Da.24] Simultaneously starting axis No.1" and "[Da.25] Simultaneously starting axis No.2". |
| 4-axis interpolation | Set the target axis No. in "[Da.24] Simultaneously starting axis No.1" to "[Da.26] Simultaneously starting axis No.3". |

*(Note: "interpolation" in this table is as printed in the original.)*

Set the axis set as simultaneously starting axis.

| Setting value | Simultaneously starting axis | Setting value | Simultaneously starting axis |
|---|---|---|---|
| 0 | Axis 1 | 4 | Axis 5 |
| 1 | Axis 2 | 5 | Axis 6 |
| 2 | Axis 3 | 6 | Axis 7 |
| 3 | Axis 4 | 7 | Axis 8 |

> **Point**
> - Do not specify the own axis No. or the value outside the range. Otherwise, the error "Condition data error" (error code: 1A00H [FX5-SSC-S], or error codes: 1B00H to 1B0FH [FX5-SSC-G]) will occur during the program execution.
> - When the same axis No. is set to multiple simultaneously starting axis Nos. or the value outside the range is set to the number of simultaneously starting axes, the error "Condition data error" (error code: 1A00H [FX5-SSC-S], or error codes: 1B00H to 1B0FH [FX5-SSC-G]) will occur during the program execution.
> - Do not specify the simultaneously starting axis No.2 and simultaneously starting axis No.3 for 2-axis simultaneously start, and not specify the simultaneously starting axis No.3 for 3-axis simultaneously start. The setting value is ignored.

#### ■Buffer memory address (バッファメモリアドレス) (11.6 / original p.519)

Refer to the following for the buffer memory address in this area.
→Page 432 Positioning data (Block start data)

## 11.7 Monitor Data (モニタデータ) (11.7 / original p.520-562)

The setting items of the monitor data are explained in this section.

### System monitor data (システムモニタデータ) (11.7 / original p.520-528)

Unless noted in particular, the monitor value is saved as binary data.

#### [Md.3] Start information (始動情報) (11.7 / original p.520)

This area stores the start information (restart flag, start origin, and start axis):
- Restart flag: Indicates whether the operation has or has not been halted and restarted.
- Start origin: Indicates the source of the start signal.
- Start axis: Indicates the started axis.

The information shown in the diagram below is stored.

[Figure] [Md.3] Start information bit configuration (original p.520)
- The buffer memory (b15 to b0) value is shown as the monitor value (4 hexadecimal digits). Brackets from the bit frame point to the monitor value digits: b15 to the 1st digit, b9 to b8 to the 2nd digit, b7 to b0 to the 3rd and 4th digits.
- Bit assignment:

| Bit | Contents |
|---|---|
| b15 | Restart flag |
| b14 | Not used (0) |
| b13 | Not used (0) |
| b12 | Not used (0) |
| b11 | Not used (0) |
| b10 | Not used (0) |
| b9 | Start origin (b9 to b8, 2 bits) |
| b8 | Start origin (b9 to b8, 2 bits) |
| b7 | Start axis (b7 to b0) |
| b6 | Start axis (b7 to b0) |
| b5 | Start axis (b7 to b0) |
| b4 | Start axis (b7 to b0) |
| b3 | Start axis (b7 to b0) |
| b2 | Start axis (b7 to b0) |
| b1 | Start axis (b7 to b0) |
| b0 | Start axis (b7 to b0) |

*In the original, this is a bit frame in the figure: b14 to b10 are filled with "0" and labeled "Not used"; the start origin (b9 to b8) and start axis (b7 to b0) are shown with brackets. Expanded to each bit.

●Restart flag

| Stored contents | Stored value |
|---|---|
| Restart flag OFF | 0 |
| Restart flag ON | 1 |

●Start origin

| Stored contents | Stored value |
|---|---|
| CPU module | 00 |
| External signal | 01 |
| Engineering tool | 10 |

●Start axis

| Stored contents | Stored value |
|---|---|
| Axis 1 | 1 |
| Axis 2 | 2 |
| Axis 3 | 3 |
| Axis 4 | 4 |
| Axis 5 | 5 |
| ︙ | ︙ |
| Axis 8 | 8 |

*In the original table, the rows between Axis 5 and Axis 8 are shown as a vertical dotted line (︙); rows for Axis 6 and Axis 7 are not printed.

- The range from axis 1 to 4 is valid in the 4-axis module and from axis 1 to 8 is valid in the 8-axis module.

Refresh cycle: At start

> **Point**
> If a start signal is issued against an operating axis, a record relating to this event may be output before a record relating to an earlier start signal is output.

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.520)

Refer to the following for the buffer memory address in this area.
→Page 425 System monitor data

#### [Md.4] Start No. (始動番号) (11.7 / original p.521)

The start No. is stored.

| Stored value | Start No. |
|---|---|
| 001 to 600(0001H to 0258H) | Positioning operation |
| 7000(1B58H) | Positioning operation |
| 7001(1B59H) | Positioning operation |
| 7002(1B5AH) | Positioning operation |
| 7003(1B5BH) | Positioning operation |
| 7004(1B5CH) | Positioning operation |
| 9010(2332H) | JOG operation |
| 9011(2333H) | Manual pulse generator |
| 9001(2329H) | Machine home position return |
| 9002(232AH) | Fast home position return |
| 9003(232BH) | Current value changing |
| 9004(232CH) | Simultaneous start |
| 9020(233CH) | Synchronous control operation |
| 9030(2346H) | Position control mode → speed control mode switching |
| 9031(2347H) | Position control mode → torque control mode switching |
| 9032(2348H) | Speed control mode → torque control mode switching |
| 9033(2349H) | Torque control mode → speed control mode switching |
| 9034(234AH) | Speed control mode → position control mode switching |
| 9035(234BH) | Torque control mode → position control mode switching |
| 9036(234CH) | Outside the range of control mode setting |
| 9037(234DH) | Position control mode → continuous operation to torque control mode switching |
| 9038(234EH) | Continuous operation to torque control mode → position control mode switching |
| 9039(234FH) | Speed control mode → continuous operation to torque control mode switching |
| 9040(2350H) | Continuous operation to torque control mode → speed control mode switching |
| 9041(2351H) | Torque control mode → continuous operation to torque control mode switching |
| 9042(2352H) | Continuous operation to torque control mode → torque control mode switching |

*In the original, "001 to 600(0001H to 0258H)" to "7004(1B5CH)" share one merged cell "Positioning operation". Expanded to each row.

Refresh cycle: At start

> **Point**
> If a start signal is issued against an operating axis, a record relating to this event may be output before a record relating to an earlier start signal is output.

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.521)

Refer to the following for the buffer memory address in this area.
→Page 425 System monitor data

#### [Md.54] Start (Year: month) (始動(年・月)) (11.7 / original p.522)

The starting time (Year: month) is stored.

| Buffer memory configuration | Stored contents | Storage value |
|---|---|---|
| (1) b15 to b12 | Year (tens place) | 0 to 9 |
| (2) b11 to b8 | Year (ones place) | 0 to 9 |
| (3) b7 to b4 | Month (tens place) | 0, 1 |
| (4) b3 to b0 | Month (ones place) | 0 to 9 |

*In the original, the "Buffer memory configuration" column is a figure of the 16-bit frame (b15 to b0) divided into (1) to (4) by 4 bits. Written out as bit ranges.

Refresh cycle: At start

> **Point**
> If a start signal is issued against an operating axis, a record relating to this event may be output before a record relating to an earlier start signal is output.

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.522)

Refer to the following for the buffer memory address in this area.
→Page 425 System monitor data

#### [Md.5] Start (Day: hour) (始動(日・時)) (11.7 / original p.522)

The starting time (Day: hour) is stored.

| Buffer memory configuration | Stored contents | Storage value |
|---|---|---|
| (1) b15 to b12 | Day (tens place) | 0 to 3 |
| (2) b11 to b8 | Day (ones place) | 0 to 9 |
| (3) b7 to b4 | Hour (tens place) | 0 to 2 |
| (4) b3 to b0 | Hour (ones place) | 0 to 9 |

*In the original, the "Buffer memory configuration" column is a figure of the 16-bit frame (b15 to b0) divided into (1) to (4) by 4 bits. Written out as bit ranges.

Refresh cycle: At start

> **Point**
> If a start signal is issued against an operating axis, a record relating to this event may be output before a record relating to an earlier start signal is output.

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.522)

Refer to the following for the buffer memory address in this area.
→Page 425 System monitor data

#### [Md.6] Start (Minute: second) (始動(分・秒)) (11.7 / original p.522)

The starting time (Minute: second) is stored.

| Buffer memory configuration | Stored contents | Storage value |
|---|---|---|
| (1) b15 to b12 | Minute (tens place) | 0 to 5 |
| (2) b11 to b8 | Minute (ones place) | 0 to 9 |
| (3) b7 to b4 | Second (tens place) | 0 to 5 |
| (4) b3 to b0 | Second (ones place) | 0 to 9 |

*In the original, the "Buffer memory configuration" column is a figure of the 16-bit frame (b15 to b0) divided into (1) to (4) by 4 bits. Written out as bit ranges.

Refresh cycle: At start

> **Point**
> If a start signal is issued against an operating axis, a record relating to this event may be output before a record relating to an earlier start signal is output.

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.522)

Refer to the following for the buffer memory address in this area.
→Page 425 System monitor data

#### [Md.60] Start (ms) (始動(ms)) (11.7 / original p.523)

The starting time (ms) is stored.
000 (ms) to 999 (ms)

| Buffer memory configuration | Stored contents | Storage value |
|---|---|---|
| (1) b15 to b12 | 0 | 0 |
| (2) b11 to b8 | ms (hundreds place) | 0 to 9 |
| (3) b7 to b4 | ms (tens place) | 0 to 9 |
| (4) b3 to b0 | ms (ones place) | 0 to 9 |

*In the original, the "Buffer memory configuration" column is a figure of the 16-bit frame (b15 to b0) divided into (1) to (4) by 4 bits. Written out as bit ranges.

Refresh cycle: At start

> **Point**
> If a start signal is issued against an operating axis, a record relating to this event may be output before a record relating to an earlier start signal is output.

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.523)

Refer to the following for the buffer memory address in this area.
→Page 425 System monitor data

#### [Md.7] Error judgment (エラー判定) (11.7 / original p.523)

This area stores the following results of the error judgment performed upon starting:
- Warning flag
  - BUSY start
  - Control mode switching during BUSY
  - Control mode switching during zero speed OFF
  - Outside control mode range
  - Control mode switching
- Error flag
- Error code

*In the original, "BUSY start" to "Control mode switching" are listed in a ruled box under "Warning flag".

The results of the error judgment shown in the diagram below are stored.

[Figure] [Md.7] Error judgment bit configuration (original p.523)
- The buffer memory (b15 to b0) value is shown as the monitor value "A B C D" (4 hexadecimal digits): A = b15 to b12, B = b11 to b8, C = b7 to b4, D = b3 to b0.
- Bit assignment:

| Bit | Contents |
|---|---|
| b15 | Warning flag |
| b14 | Error flag |
| b13 | Error code (a) |
| b12 | Error code (a) |
| b11 | Error code (B) |
| b10 | Error code (B) |
| b9 | Error code (B) |
| b8 | Error code (B) |
| b7 | Error code (C) |
| b6 | Error code (C) |
| b5 | Error code (C) |
| b4 | Error code (C) |
| b3 | Error code (D) |
| b2 | Error code (D) |
| b1 | Error code (D) |
| b0 | Error code (D) |

*In the original, this is a bit frame in the figure: b13 to b12 are bracketed as "a", b11 to b8 as "B", b7 to b4 as "C", b3 to b0 as "D", and a to D together as "Error code". Expanded to each bit.

●Error flag

| Stored contents | Stored value |
|---|---|
| Error flag OFF | 0 |
| Error flag ON | 1 |

●Warning flag

| Stored contents | Stored value |
|---|---|
| Error flag OFF | 0 |
| Error flag ON | 1 |

*As printed in the original: the Warning flag table's "Stored contents" reads "Error flag OFF" / "Error flag ON" (presumably a typo for "Warning flag OFF/ON"; kept as printed).

●Error code
- Convert the hexadecimal value "a, B, C, D" into a decimal value and match it with Section 14.5 List of Error Codes.

Refresh cycle: At start

> **Point**
> If a start signal is issued against an operating axis, a record relating to this event may be output before a record relating to an earlier start signal is output.

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.523)

Refer to the following for the buffer memory address in this area.
→Page 425 System monitor data

#### [Md.8] Start history pointer (始動履歴ポインタ) (11.7 / original p.524)

Indicates a pointer No. that is next to the pointer No. assigned to the latest of the existing starting history records.
The storage value (Pointer No.) is 0 to 63.

Refresh cycle: At start

> **Point**
> If a start signal is issued against an operating axis, a record relating to this event may be output before a record relating to an earlier start signal is output.

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.524)

Refer to the following for the buffer memory address in this area.
→Page 425 System monitor data

#### [Md.19] Number of write accesses to flash ROM (フラッシュ ROM書込み回数) (11.7 / original p.524)

Stores the number of write accesses to the flash ROM after the power is switched ON.
The storage value is 0 to 25. The count is cleared to "0" when the number of write accesses reaches 26 and an error reset operation is performed.

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.524)

Refer to the following for the buffer memory address in this area.
→Page 425 System monitor data

#### [Md.50] Forced stop input (緊急停止入力) (11.7 / original p.524)

This area stores the forced stop input ON/OFF status.

| Storage value | Forced stop input |
|---|---|
| 0 | Forced stop input ON (Forced stop) |
| 1 | Forced stop input OFF (Forced stop release) |

Refresh cycle: Operation cycle

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.524)

Refer to the following for the buffer memory address in this area.
→Page 425 System monitor data

#### [Md.51] Amplifier-less operation mode status [FX5-SSC-S] (アンプなし運転モード状態[FX5-SSC-S]) (11.7 / original p.524)

Indicates a current operation mode.

| Storage value | Operation mode |
|---|---|
| 0 | Normal operation mode |
| 1 | Amplifier-less operation mode |

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.524)

Refer to the following for the buffer memory address in this area.
→Page 425 System monitor data

#### [Md.52] Communication between amplifiers axes searching flag [FX5-SSC-S] (ドライバ間通信軸検索中フラグ[FX5-SSC-S]) (11.7 / original p.525)

Stores the detection status of the axis that sets communication between amplifiers.

| Storage value | Detection status |
|---|---|
| 0 | Search end |
| 1 | Searching |

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.525)

Refer to the following for the buffer memory address in this area.
→Page 425 System monitor data

#### [Md.53] SSCNET control status [FX5-SSC-S] (SSCNET制御ステータス[FX5-SSC-S]) (11.7 / original p.525)

Stores the connect/disconnect status of SSCNET communication.

| Storage value | SSCNET control status |
|---|---|
| 1 | Disconnected axis existing |
| 0 | Command accept waiting |
| -1 | Execute waiting |
| -2 | Executing |

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.525)

Refer to the following for the buffer memory address in this area.
→Page 425 System monitor data

#### [Md.59] Module information (ユニット情報) (11.7 / original p.525)

Stores the model code of the module.

| Storage value | Module information |
|---|---|
| 63C0H | FX5-40SSC-S |
| 63C1H | FX5-80SSC-S |
| 6959H | FX5-40SSC-G |
| 695AH | FX5-80SSC-G |

Refresh cycle: At power supply ON

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.525)

Refer to the following for the buffer memory address in this area.
→Page 425 System monitor data

#### [Md.130] F/W version (ファームウェアバージョン) (11.7 / original p.525)

Stores the F/W version of the module.
- Monitoring is carried out with a decimal display.

Ex.
When the F/W version is "1.000", "1000" is stored.

Refresh cycle: At power supply ON

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.525)

Refer to the following for the buffer memory address in this area.
→Page 425 System monitor data

#### [Md.131] Digital oscilloscope running flag (デジタルオシロRUN中フラグ) (11.7 / original p.526)

Stores the RUN status of the digital oscilloscope.

| Storage value | Digital oscilloscope RUN status |
|---|---|
| 0 | Stop |
| 1 | Run |
| -1 | Stop by error |

Refresh cycle: Main cycle

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.526)

Refer to the following for the buffer memory address in this area.
→Page 425 System monitor data

#### [Md.132] Operation cycle setting (設定演算周期) (11.7 / original p.526)

Stores the current operation cycle.

| Storage value (module) | Storage value | Operation cycle |
|---|---|---|
| FX5-SSC-S | 0000H | 0.888 ms |
| FX5-SSC-S | 0001H | 1.777 ms |
| FX5-SSC-G | 1005H | 0.500 ms |
| FX5-SSC-G | 1006H | 1.000 ms |
| FX5-SSC-G | 1007H | 2.000 ms |
| FX5-SSC-G | 1008H | 4.000 ms |

*In the original, the "Storage value" header spans two columns; "FX5-SSC-S" is a merged cell over 2 rows and "FX5-SSC-G" over 4 rows. Expanded to each row.

Refresh cycle: At power supply ON

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.526)

Refer to the following for the buffer memory address in this area.
→Page 425 System monitor data

#### [Md.133] Operation cycle over flag (演算周期オーバーフラグ) (11.7 / original p.526)

This flag turns ON when the operation cycle time exceeds operation cycle.

| Storage value | Operation cycle over flag |
|---|---|
| 0 | OFF |
| 1 | ON (Operation cycle over occurred.) |

Refresh cycle: Immediate

> **Point**
> - Latch status of operation cycle over is indicated. When this flag turns ON, correct the positioning detail or change the operation cycle longer than current setting.
>
> [FX5-SSC-G]
> - The operation cycle time only includes the time spent on the positioning processing cycle and does not include the time spent on communication with the servo amplifier, etc. As such, errors such as "Operation cycle time over error" (error code: 1A3FH), "Driver error" (error code: 1ED0H), and "WDT error" (error code: 1ED2H) may occur even if the operation cycle time does not reach the set operation cycle.

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.526)

Refer to the following for the buffer memory address in this area.
→Page 425 System monitor data

#### [Md.134] Operation time (演算時間) (11.7 / original p.527)

Stores the time (Unit: μs) that took for operation every operation cycle.

Refresh cycle: Operation cycle

> **Point**
> [FX5-SSC-G]
> - The stored time only includes the time spent on the positioning processing cycle and does not include the time spent on communication with the servo amplifier, etc. As such, errors such as "Operation cycle time over error" (error code: 1A3FH), "Driver error" (error code: 1ED0H), and "WDT error" (error code: 1ED2H) may occur even if the operation cycle time does not reach the set operation cycle.

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.527)

Refer to the following for the buffer memory address in this area.
→Page 425 System monitor data

#### [Md.135] Maximum operation time (最大演算時間) (11.7 / original p.527)

Stores the maximum value (Unit: μs) of operation time after each module's power supply ON.

Refresh cycle: Immediate

> **Point**
> [FX5-SSC-G]
> - The stored time only includes the time spent on the positioning processing cycle and does not include the time spent on communication with the servo amplifier, etc. As such, errors such as "Operation cycle time over error" (error code: 1A3FH), "Driver error" (error code: 1ED0H), and "WDT error" (error code: 1ED2H) may occur even if the operation cycle time does not reach the set operation cycle.

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.527)

Refer to the following for the buffer memory address in this area.
→Page 425 System monitor data

#### [Md.140] Module status (ユニットステータス) (11.7 / original p.527)

Stores the status (ON/OFF) of various flags.
Storage details are shown below.

| Flag | Details |
|---|---|
| READY | • When the "[Cd.190] PLC READY" turns from OFF→ON, the parameter setting range is checked. If no error is found, this signal turns ON.<br>• When the "[Cd.190] PLC READY" turns OFF, this signal turns OFF.<br>• When watch dog timer error occurs, this signal turns OFF.<br>• This signal is used for interlock in a program, etc. |
| Synchronization flag | • After the CPC module is turned ON/reset, this signal turns ON if the access from the CPU module to the Simple Motion module/Motion module is possible.<br>• It is used for interlock when accessing the Simple Motion module/Motion module from the program. |

*As printed in the original: "CPC module" (presumably a typo for "CPU module"; kept as printed).

| Bit | Buffer memory configuration | Stored items | Storage value |
|---|---|---|---|
| b15 to b2 | Not used (0) | — | — |
| b1 | (2) | Synchronization flag | 0: OFF (Not READY/Watch dog timer error)<br>1: ON (READY) |
| b0 | (1) | READY | 0: OFF (Not READY/Watch dog timer error)<br>1: ON (READY) |

*In the original, the "Buffer memory configuration" column is a figure of the 16-bit frame: b15 to b2 are filled with "0" and labeled "Not used", b1 = (2), b0 = (1). The "Storage value" cell is merged over (1) and (2). Expanded to each row.

Refresh cycle of READY(b0): At "[Cd.190] PLC READY" OFF → ON
Refresh cycle of Synchronization flag (b1): At power supply ON/the CPU module reset

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.527)

Refer to the following for the buffer memory address in this area.
→Page 425 System monitor data

#### [Md.141] BUSY (BUSY) (11.7 / original p.528)

- This signal turns ON at the start of positioning, home position return or JOG operation. It turns OFF during the stop by the step operation that turns OFF (This signal remains ON during positioning) after the "[Da.9] Dwell time/JUMP destination positioning data No." has passed after positioning stops.
- During manual pulse generator operation, this signal turns ON while the "[Cd.21] Manual pulse generator enable flag" is ON.
- This signal turns OFF at error completion or positioning stop.

| Bit | Buffer memory configuration | Stored items | Storage value |
|---|---|---|---|
| b15 to b8 | Not used (0) | — | — |
| b7 | (8) | Axis 8 BUSY | 0: OFF (Not BUSY)<br>1: ON (BUSY) |
| b6 | (7) | Axis 7 BUSY | 0: OFF (Not BUSY)<br>1: ON (BUSY) |
| b5 | (6) | Axis 6 BUSY | 0: OFF (Not BUSY)<br>1: ON (BUSY) |
| b4 | (5) | Axis 5 BUSY | 0: OFF (Not BUSY)<br>1: ON (BUSY) |
| b3 | (4) | Axis 4 BUSY | 0: OFF (Not BUSY)<br>1: ON (BUSY) |
| b2 | (3) | Axis 3 BUSY | 0: OFF (Not BUSY)<br>1: ON (BUSY) |
| b1 | (2) | Axis 2 BUSY | 0: OFF (Not BUSY)<br>1: ON (BUSY) |
| b0 | (1) | Axis 1 BUSY | 0: OFF (Not BUSY)<br>1: ON (BUSY) |

*In the original, the "Buffer memory configuration" column is a figure of the 16-bit frame: b15 to b8 are filled with "0" and labeled "Not used", b7 to b0 = (8) to (1). The "Storage value" cell is merged over (1) to (8). Expanded to each row.

Refresh cycle: At start

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.528)

Refer to the following for the buffer memory address in this area.
→Page 425 System monitor data

### Axis monitor data (軸モニタデータ) (11.7 / original p.529-562)

#### [Md.20] Command position value (送り現在値) (11.7 / original p.529)

The currently commanded address is stored. (Different from the actual motor position during operation)
The current position address is stored.
If "degree" is selected as the unit, the addresses have a ring structure for values between 0 and 359.99999°.
As shown in the diagram below, the hexadecimal monitor value is changed to a decimal integer value. The decimal integer value can be converted into other units by multiplying said value by the following conversion values.

[Figure] Reading the 32-bit monitor value (original p.529)
- The low-order buffer memory (b15 to b0) is split every 4 bits into E (b15 to b12), F (b11 to b8), G (b7 to b4), H (b3 to b0), shown as the upper row "E F G H" of the monitor value.
- The high-order buffer memory (b31 to b16) is split every 4 bits into A (b31 to b28), B (b27 to b24), C (b23 to b20), D (b19 to b16), shown as the lower row "A B C D" of the monitor value.
- ◇Sorting → "(High-order buffer memory) A B C D" "(Low-order buffer memory) E F G H" in this order.
- ◇Converted from hexadecimal to decimal → "Decimal integer value".

| Unit | Conversion value |
|---|---|
| μm | × 10^-1 |
| inch | × 10^-5 |
| degree | × 10^-5 |
| pulse | × 10^0 |

- The home position address is stored when the machine home position return is completed.
- When the current value is changed with the current value changing function, the changed value is stored.

Refresh cycle: Operation cycle

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.529)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.21] Machine feed value (送り機械値) (11.7 / original p.530)

The address of the current position according to the machine coordinates will be stored. (Different from the actual motor position during operation)
Note that the current value changing function will not change the machine feed value.
Under the speed control mode, the machine feed value is constantly updated always, irrespective of the parameter setting.
The value will not be cleared to "0" at the beginning of fixed-feed control.
Even if "degree" is selected as the unit, the addresses become a cumulative value. (They do not have a ring structure for values between 0 and 359.99999°). However, the movement amount during the power supply OFF is added to the machine feed value before the power supply OFF (the rounded value within the range of 0 to 359.99999°) for restoration at the communication start with servo amplifier after the power supply ON or CPU module reset.
As shown in the diagram below, the hexadecimal monitor value is changed to a decimal integer value. The decimal integer value can be converted into other units by multiplying said value by the following conversion values.

[Figure] Reading the 32-bit monitor value (original p.530)
- The low-order buffer memory (b15 to b0) is split every 4 bits into E (b15 to b12), F (b11 to b8), G (b7 to b4), H (b3 to b0), shown as the upper row "E F G H" of the monitor value.
- The high-order buffer memory (b31 to b16) is split every 4 bits into A (b31 to b28), B (b27 to b24), C (b23 to b20), D (b19 to b16), shown as the lower row "A B C D" of the monitor value.
- ◇Sorting → "(High-order buffer memory) A B C D" "(Low-order buffer memory) E F G H" in this order.
- ◇Converted from hexadecimal to decimal → "Decimal integer value".

| Unit | Conversion value |
|---|---|
| μm | × 10^-1 |
| inch | × 10^-5 |
| degree | × 10^-5 |
| pulse | × 10^0 |

- Machine coordinates: Characteristic coordinates determined with machine

Refresh cycle: Operation cycle

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.530)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.22] Speed command (送り速度) (11.7 / original p.531)

The speed of the operating workpiece is stored. (May be different from the actual motor speed during operation)
As shown in the diagram below, the hexadecimal monitor value is changed to a decimal integer value. The decimal integer value can be converted into other units by multiplying said value by the following conversion values.

[Figure] Reading the 32-bit monitor value (original p.531)
- The low-order buffer memory (b15 to b0) is split every 4 bits into E (b15 to b12), F (b11 to b8), G (b7 to b4), H (b3 to b0), shown as the upper row "E F G H" of the monitor value.
- The high-order buffer memory (b31 to b16) is split every 4 bits into A (b31 to b28), B (b27 to b24), C (b23 to b20), D (b19 to b16), shown as the lower row "A B C D" of the monitor value.
- ◇Sorting → "(High-order buffer memory) A B C D" "(Low-order buffer memory) E F G H" in this order.
- ◇Converted from hexadecimal to decimal → "Decimal integer value".

| Unit | Conversion value |
|---|---|
| mm/min | × 10^-2 |
| inch/min | × 10^-3 |
| degree/min | × 10^-3*1 |
| pulse/s | × 10^0 |

*1 When "[Pr.83] Speed control 10 × multiplier setting for degree axis" is valid, becomes "× 10^-2".

- During interpolation operation, the speed is stored in the following manner.

| Axis | Stored speed |
|---|---|
| Reference axis | Composite speed or reference axis speed (Set with [Pr.20]) |
| Interpolation axis | 0 |

*In the original, this table has no header row. The header here was added for Markdown.

Refresh cycle: Operation cycle

> **Point**
> In case of the single axis operation, "[Md.22] Speed command" and "[Md.28] Axis speed command" are identical.
> In the composite mode of the interpolation operation, "[Md.22] Speed command" is a speed in a composite direction and "[Md.28] Axis speed command" is that in each axial direction.
> The absolute value is displayed in "[Md.22] Speed command". The operation direction can be checked in "[Md.20] Command position value".

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.531)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.23] Axis error No. (軸エラー番号) (11.7 / original p.531)

When an axis error is detected, the error code corresponding to the error details is stored.
- The latest error code is always stored. (When a new axis error occurs, the error code is overwritten.)
- When "[Cd.5] Axis error reset" is set to "1", the axis error No. is cleared (set to 0).
- Monitoring is carried out with a hexadecimal.

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.531)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.24] Axis warning No. (軸ワーニング番号) (11.7 / original p.532)

Whenever an axis warning is reported, a related warning code is stored.
- This area stores the latest warning code always. (Whenever an axis warning is reported, a new warning code replaces the stored warning code.)
- When "[Cd.5] Axis error reset" is set to "1", the axis warning No. is cleared to "0".
- Monitoring is carried out with a hexadecimal.

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.532)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.25] Valid M code (有効Mコード) (11.7 / original p.532)

This area stores an M code that is currently active (i.e. set to the positioning data relating to the current operation).
When the "[Cd.190] PLC READY" goes OFF, the value is set to "0".
The value stored is 0 to 65535.

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.532)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.26] Axis operation status (軸動作状態) (11.7 / original p.532)

This area stores the axis operation status.

| Storage value | Axis operation status |
|---|---|
| -2 | Step standby |
| -1 | Error |
| 0 | Standby |
| 1 | Stopped |
| 2 | Interpolation |
| 3 | JOG operation |
| 4 | Manual pulse generator operation |
| 5 | Analyzing |
| 6 | Special start standby |
| 7 | Home position return |
| 8 | Position control |
| 9 | Speed control |
| 10 | Speed control in speed-position switching control |
| 11 | Position control in speed-position switching control |
| 12 | Position control in position-speed switching control |
| 13 | Speed control in position-speed switching control |
| 15 | Synchronous control |
| 20 | Servo amplifier has not been connected/servo amplifier power OFF |
| 21 | Servo OFF |
| 30 | Control mode switch |
| 31 | Speed control |
| 32 | Torque control |
| 33 | Continuous operation to torque control |

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.532)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.27] Current speed (カレント速度) (11.7 / original p.533)

The "[Da.8] Command speed" used by the positioning data currently being executed is stored.
- If "[Da.8] Command speed" is set to "-1", this area stores the command speed set by the positioning data used one step earlier.
- If "[Da.8] Command speed" is set to a value other than "-1", this area stores the command speed set by the current positioning data.
- When speed change function is executed, this area stores "[Cd.14] New speed value". (For details of change speed function, refer to →Page 257 Speed change function)

The storage value converted into other units can be checked by multiplying said value by the following conversion values.

| Unit | Conversion value |
|---|---|
| mm/min | × 10^-2 |
| inch/min | × 10^-3 |
| degree/min | × 10^-3*1 |
| pulse/s | × 10^0 |

*1 When "[Pr.83] Speed control 10 × multiplier setting for degree axis" is valid, becomes "× 10^-2".

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.533)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.28] Axis speed command (軸送り速度) (11.7 / original p.534)

The speed which is actually output as a command at that time in each axis is stored. (May be different from the actual motor speed) "0" is stored when the axis is at a stop. (→Page 529 [Md.22] Speed command)
As shown in the diagram below, the hexadecimal monitor value is changed to a decimal integer value. The decimal integer value can be converted into other units by multiplying said value by the following conversion values.

[Figure] Reading the 32-bit monitor value (original p.534)
- The low-order buffer memory (b15 to b0) is split every 4 bits into E (b15 to b12), F (b11 to b8), G (b7 to b4), H (b3 to b0), shown as the upper row "E F G H" of the monitor value.
- The high-order buffer memory (b31 to b16) is split every 4 bits into A (b31 to b28), B (b27 to b24), C (b23 to b20), D (b19 to b16), shown as the lower row "A B C D" of the monitor value.
- ◇Sorting → "(High-order buffer memory) A B C D" "(Low-order buffer memory) E F G H" in this order.
- ◇Converted from hexadecimal to decimal → "Decimal integer value".

| Unit | Conversion value |
|---|---|
| mm/min | × 10^-2 |
| inch/min | × 10^-3 |
| degree/min | × 10^-3*1 |
| pulse/s | × 10^0 |

*1 When "[Pr.83] Speed control 10 × multiplier setting for degree axis" is valid, becomes "× 10^-2".

Refresh cycle: Operation cycle

> **Point**
> The absolute value is displayed in "[Md.28] Axis speed command". The operation direction can be checked in "[Md.20] Command position value".

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.534)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.29] Speed-position switching control positioning movement amount (速度・位置切換え制御の位置決め移動量) (11.7 / original p.535)

The movement amount for the position control to end after changing to position control with the speed-position switching control is stored. When the control method is "Reverse run: position/speed", the negative value is stored.
As shown in the diagram below, the hexadecimal monitor value is changed to a decimal integer value. The decimal integer value can be converted into other units by multiplying said value by the following conversion values.

[Figure] Reading the 32-bit monitor value (original p.535)
- The low-order buffer memory (b15 to b0) is split every 4 bits into E (b15 to b12), F (b11 to b8), G (b7 to b4), H (b3 to b0), shown as the upper row "E F G H" of the monitor value.
- The high-order buffer memory (b31 to b16) is split every 4 bits into A (b31 to b28), B (b27 to b24), C (b23 to b20), D (b19 to b16), shown as the lower row "A B C D" of the monitor value.
- ◇Sorting → "(High-order buffer memory) A B C D" "(Low-order buffer memory) E F G H" in this order.
- ◇Converted from hexadecimal to decimal → "Decimal integer value".

| Unit | Conversion value |
|---|---|
| μm | × 10^-1 |
| inch | × 10^-5 |
| degree | × 10^-5 |
| pulse | × 10^0 |

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.535)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.30] External input signal (外部入力信号) (11.7 / original p.536)

[FX5-SSC-S]
The ON/OFF state of the external input signal is stored.

| Bit | Buffer memory configuration | Stored items | Storage value |
|---|---|---|---|
| b15 to b7 | Not used (0) | — | — |
| b6 | (5) | Proximity dog signal*1 | 0: OFF<br>1: ON |
| b5 | Not used (0) | — | — |
| b4 | (4) | External command signal/switching signal | 0: OFF<br>1: ON |
| b3 | (3) | Stop signal*1 | 0: OFF<br>1: ON |
| b2 | Not used (0) | — | — |
| b1 | (2) | Upper limit signal*1 | 0: OFF<br>1: ON |
| b0 | (1) | Lower limit signal*1 | 0: OFF<br>1: ON |

*In the original, the "Buffer memory configuration" column is a figure of the 16-bit frame: b15 to b7, b5 and b2 are filled with "0" and labeled "Not used"; b6 = (5), b4 = (4), b3 = (3), b1 = (2), b0 = (1). The "Storage value" cell is merged over (1) to (5). Expanded to each row.

*1 This area stores the states of the external input signal (servo amplifier) or buffer memory of Simple Motion module/Motion module set by "[Pr.116] FLS signal selection", "[Pr.117] RLS signal selection", "[Pr.118] DOG signal selection", and "[Pr.119] STOP signal selection".

[FX5-SSC-G]
The state of the external input signal is stored.

| Bit | Buffer memory configuration | Stored items | Storage value |
|---|---|---|---|
| b15 to b7 | Not used (0) | — | — |
| b6 | (5) | Proximity dog signal | 0: Proximity dog signal is OFF<br>1: Proximity dog signal is ON |
| b5 | Not used (0) | — | — |
| b4 | (4) | External command signal/switching signal | 0: External command signal/switching signal is OFF<br>1: External command signal/switching signal is ON |
| b3 | (3) | Stop signal | 0: Stop signal is OFF<br>1: Stop signal is ON |
| b2 | Not used (0) | — | — |
| b1 | (2) | Upper limit signal | 0: Limit signal ON<br>1: Limit signal OFF |
| b0 | (1) | Lower limit signal | 0: Limit signal ON<br>1: Limit signal OFF |

*In the original, the "Buffer memory configuration" column is a figure of the 16-bit frame: b15 to b7, b5 and b2 are filled with "0" and labeled "Not used"; b6 = (5), b4 = (4), b3 = (3), b1 = (2), b0 = (1). The "Storage value" cell "0: Limit signal ON / 1: Limit signal OFF" is merged over (1) and (2). Expanded to each row.

> The signal state is stored according to the logic set by the following parameters.
> - [Pr.22] Input signal logic selection
> - [Pr.913] Upper limit signal (FLS): Link device logic setting
> - [Pr.923] Lower limit signal (RLS): Link device logic setting
> - [Pr.933] Proximity dog signal (DOG): Link device logic setting
> - [Pr.943] Stop signal (STOP): Link device logic setting

Refresh cycle: Operation cycle

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.536)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.31] Status (ステータス) (11.7 / original p.537-538)

This area stores the states (ON/OFF) of various flags.
Information on the following flags is stored.

| Flag | Details |
|---|---|
| In speed control flag | This signal that comes ON under the speed control can be used to judge whether the operation is performed under the speed control or position control. The signal goes OFF when the power is switched ON, under the position control, and during JOG operation or manual pulse generator operation. During the speed-position or position-speed switching control, this signal comes ON only when the speed control is in effect. During the speed-position switching control, this signal goes OFF when the speed-position switching signal executes a switching over from speed control to position control. During the position-speed switching control, this signal comes ON when the position-speed switching signal executes a switching over from position control to speed control. |
| Speed-position switching latch flag | This signal is used during the speed-position switching control for interlocking the movement amount change function. During the speed-position switching control, this signal comes ON when position control takes over. This signal goes OFF when the next positioning data is processed, and during JOG operation or manual pulse generator operation. |
| Command in-position flag | This signal is ON when the remaining distance is equal to or less than the command in-position range (set by a detailed parameter). This signal remains OFF with data that specify the continuous path control (P11) as the operation pattern. The state of this signal is monitored every operation cycle except when the monitoring is canceled under the speed control or while the speed control is in effect during the speed-position or position-speed switching control. While operations are performed with interpolation, this signal comes ON only in respect of the starting axis. (This signal goes OFF in respect of all axes upon starting.) |
| Home position return request flag | This signal comes ON when a home position return is required and goes OFF at completion of a home position return.<br>For details of home position return request flag, refer to →Page 36 Outline of Home Position Return Control. |
| Home position return complete flag | This signal comes ON when a machine home position return operation completes normally. This signal goes OFF when the operation start. |
| Position-speed switching latch flag | This signal is used during the position-speed switching control for interlocking the command speed change function. During the position-speed switching control, this signal comes ON when speed control takes over. This signal goes OFF when the next positioning data is processed, and during JOG operation or manual pulse generator operation. |
| Axis warning detection flag | This signal comes On when an axis warning is reported and goes OFF when the axis error reset signal comes ON. |
| Speed change 0 flag | This signal comes ON when the speed is "0" by the speed change or override. Otherwise, it goes OFF. |
| M code ON | In the WITH mode, this signal turns ON when the positioning data operation is started. In the AFTER mode, this signal turns ON when the positioning data operation is completed.<br>This signal turns OFF with the "[Cd.7] M code OFF request".<br>When M code is not designated (when "[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions" is "0"), this signal will remain OFF.<br>With using continuous path control for the positioning operation, the positioning will continue even when this signal does not turn OFF.<br>However, the warning "M code ON signal ON" (warning code: 0992H [FX5-SSC-S], or warning code: 0D52H [FX5-SSC-G]) will occur.<br>When the "[Cd.190] PLC READY" turns OFF, the M code ON signal will also turn OFF.<br>If operation is started while the M code is ON, the error "M code ON signal start" (error code: 19A0H [FX5-SSC-S], or error code: 1AA0H [FX5-SSC-G]) will occur. |
| Error detection | This signal turns ON when an error (→Page 753 List of Error Codes) occurs, and turns OFF when the error is reset on "[Cd.5] Axis error reset". |
| Start complete | This signal turns ON when the positioning start signal turns ON and the Simple Motion module/Motion module starts the positioning process. (The start complete signal also turns ON during home position return control.) |
| Positioning complete | This signal turns ON for the time set in "[Pr.40] Positioning complete signal output time" from the instant when the positioning control for each positioning data No. is completed.<br>For the interpolation control, the positioning complete signal of interpolation axis turns ON during the time set to the reference axis.<br>(It does not turn ON when "[Pr.40] Positioning complete signal output time" is "0".)<br>If positioning (including home position return), JOG/Inching operation, or manual pulse generator operation is started while this signal is ON, the signal will turn OFF.<br>This signal will not turn ON when speed control or positioning is canceled midway. |

*As printed in the original: "comes On" (Axis warning detection flag) and "goes OFF when the operation start" (Home position return complete flag); kept as printed.

| Bit | Buffer memory configuration | Stored items | Storage value |
|---|---|---|---|
| b15 | (12) | Positioning complete | 0: OFF<br>1: ON |
| b14 | (11) | Start complete | 0: OFF<br>1: ON |
| b13 | (10) | Error detection | 0: OFF<br>1: ON |
| b12 | (9) | M code ON | 0: OFF<br>1: ON |
| b11 | Not used (0) | — | — |
| b10 | (8) | Speed change 0 flag | 0: OFF<br>1: ON |
| b9 | (7) | Axis warning detection | 0: OFF<br>1: ON |
| b8 to b6 | Not used (0) | — | — |
| b5 | (6) | Position-speed switching latch flag | 0: OFF<br>1: ON |
| b4 | (5) | Home position return complete flag | 0: OFF<br>1: ON |
| b3 | (4) | Home position return request flag | 0: OFF<br>1: ON |
| b2 | (3) | Command in-position flag | 0: OFF<br>1: ON |
| b1 | (2) | Speed-position switching latch flag | 0: OFF<br>1: ON |
| b0 | (1) | In speed control flag | 0: OFF<br>1: ON |

*In the original (p.538), the "Buffer memory configuration" column is a figure of the 16-bit frame: b11 and b8 to b6 are filled with "0" and labeled "Not used"; b15 to b12 = (12) to (9), b10 = (8), b9 = (7), b5 to b0 = (6) to (1). The "Storage value" cell is merged over (1) to (12). Expanded to each row.

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.538)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.32] Target value (目標値) (11.7 / original p.538)

This area stores the target value ([Da.6] Positioning address/movement amount) for a positioning operation.
- At the beginning of positioning control and current value changing: Stores the value of "[Da.6] Positioning address/movement amount".
- At the home position shift operation of home position return control: Stores the value of home position shift amount.
- At other times: Stores "0".

The storage value converted into other units can be checked by multiplying said value by the following conversion values.

| Unit | Conversion value |
|---|---|
| μm | × 10^-1 |
| inch | × 10^-5 |
| degree | × 10^-5 |
| pulse | × 10^0 |

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.538)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.33] Target speed (目標速度) (11.7 / original p.539)

- During operation with positioning data: The actual target speed, considering the override and speed limit value, etc., is stored. "0" is stored when positioning is completed.
- During interpolation of position control: The composite speed or reference axis speed is stored in the reference axis address, and "0" is stored in the interpolation axis address.
- During interpolation of speed control: The target speeds of each axis are stored in the monitor of the reference axis and interpolation axis.
- During JOG operation: The actual target speed, considering the JOG speed limit value for the JOG speed, is stored.
- During manual pulse generator operation: "0" is stored.

As shown in the diagram below, the hexadecimal monitor value is changed to a decimal integer value. The decimal integer value can be converted into other units by multiplying said value by the following conversion values.

[Figure] Reading the 32-bit monitor value (original p.539)
- The low-order buffer memory (b15 to b0) is split every 4 bits into E (b15 to b12), F (b11 to b8), G (b7 to b4), H (b3 to b0), shown as the upper row "E F G H" of the monitor value.
- The high-order buffer memory (b31 to b16) is split every 4 bits into A (b31 to b28), B (b27 to b24), C (b23 to b20), D (b19 to b16), shown as the lower row "A B C D" of the monitor value.
- ◇Sorting → "(High-order buffer memory) A B C D" "(Low-order buffer memory) E F G H" in this order.
- ◇Converted from hexadecimal to decimal → "Decimal integer value".

| Unit | Conversion value |
|---|---|
| mm/min | × 10^-2 |
| inch/min | × 10^-3 |
| degree/min | × 10^-3*1 |
| pulse/s | × 10^0 |

*1 When "[Pr.83] Speed control 10 × multiplier setting for degree axis" is valid, becomes "× 10^-2".

Refresh cycle: Immediate

> **Point**
> The target speed is when an override is made to the command speed.
> When the speed limit value is overridden, the target speed is restricted to the speed limit value. The target speed changes every time data is switched, but does not change in an acceleration/deceleration state inside each piece of data (changes with the speed change because the target speed changes.)

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.539)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.34] Movement amount after proximity dog ON [FX5-SSC-S] (近点ドグON後の移動量[FX5-SSC-S]) (11.7 / original p.540)

- "0" is stored when machine home position return starts.
- After machine home position return starts, the movement amount from the proximity dog ON to the machine home position return completion is stored. (Movement amount: Movement amount to machine home position return completion using proximity dog ON as "0".)

As shown in the diagram below, the hexadecimal monitor value is changed to a decimal integer value. The decimal integer value can be converted into other units by multiplying said value by the following conversion values.

[Figure] Reading the 32-bit monitor value (original p.540)
- The low-order buffer memory (b15 to b0) is split every 4 bits into E (b15 to b12), F (b11 to b8), G (b7 to b4), H (b3 to b0), shown as the upper row "E F G H" of the monitor value.
- The high-order buffer memory (b31 to b16) is split every 4 bits into A (b31 to b28), B (b27 to b24), C (b23 to b20), D (b19 to b16), shown as the lower row "A B C D" of the monitor value.
- ◇Sorting → "(High-order buffer memory) A B C D" "(Low-order buffer memory) E F G H" in this order.
- ◇Converted from hexadecimal to decimal → "Decimal integer value".

| Unit | Conversion value |
|---|---|
| μm | × 10^-1 |
| inch | × 10^-5 |
| degree | × 10^-5 |
| pulse | × 10^0 |

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.540)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.35] Torque limit stored value/forward torque limit stored value (トルク制限格納値／正転トルク制限格納値) (11.7 / original p.541)

[FX5-SSC-S]
"[Pr.17] Torque limit setting value", "[Cd.101] Torque output setting value", "[Cd.22] New torque value/forward new torque value", or "[Pr.54] Home position return torque limit value" is stored.
- The value stored is 1 to 10000 (× 0.1%).
- During positioning start, JOG operation start, manual pulse generator operation: "[Pr.17] Torque limit setting value" or "[Cd.101] Torque output setting value" is stored.
- When a value is set in "[Cd.22] New torque value/forward new torque value" during operation: "[Cd.22] New torque value/forward new torque value" is stored.
- When home position return: "[Pr.17] Torque limit setting value" or "[Cd.101] Torque output setting value" is stored. However, "[Pr.54] Home position return torque limit value" is stored after the speed reaches "[Pr.47] Creep speed".

[FX5-SSC-G]
"[Pr.17] Torque limit setting value", "[Cd.101] Torque output setting value", or "[Cd.22] New torque value/forward new torque value" is stored.
- The value stored is 1 to 10000 (× 0.1%).
- During positioning start, JOG operation start, manual pulse generator operation: "[Pr.17] Torque limit setting value" or "[Cd.101] Torque output setting value" is stored.
- When a value is set in "[Cd.22] New torque value/forward new torque value" during operation: "[Cd.22] New torque value/forward new torque value" is stored.

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.541)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.36] Special start data instruction code setting value (特殊始動データ命令コード設定値) (11.7 / original p.541)

The "instruction code" used with special start and indicated by the start data pointer currently being executed is stored.

| Storage value | Special start data instruction code setting value |
|---|---|
| 0 | Block start |
| 1 | Condition start |
| 2 | Wait start |
| 3 | Simultaneous start |
| 4 | FOR loop |
| 5 | FOR condition |
| 6 | NEXT |

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.541)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.37] Special start data instruction parameter setting value (特殊始動データ命令パラメータ設定値) (11.7 / original p.542)

The "instruction parameter" used with special start and indicated by the start data pointer currently being executed is stored.
The stored value differs according to the value set for "[Md.36] Special start data instruction code setting value".

| Setting value of "[Md.36] Special start data instruction code setting value" | Storage value | Stored contents |
|---|---|---|
| Block start, NEXT | None | None |
| Condition start, Wait start, Simultaneous start, FOR condition | 1 to 10 | Condition data No. |
| FOR loop | 0 to 255 | Number of repetitions |

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.542)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.38] Start positioning data No. setting value (始動位置決めデータNo.設定値) (11.7 / original p.542)

The "positioning data No." indicated by the start data pointer currently being executed is stored.
The value stored is 1 to 600, and 9001 to 9003.

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.542)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.39] In speed limit flag (速度制限中フラグ) (11.7 / original p.542)

Stores whether the in speed limit is in progress or not.

| Storage value | In speed limit flag |
|---|---|
| 0 | Not in speed limit (OFF) |
| 1 | In speed limit (ON) |

- If the speed exceeds the "[Pr.8] Speed limit value" ("[Pr.31] JOG speed limit value" at JOG operation control) due to a speed change or override, the speed limit functions, and the in speed limit flag turns ON.
- When the speed drops to less than "[Pr.8] Speed limit value" ("[Pr.31] JOG speed limit value" at JOG operation control), or when the axis stops, the in speed limit flag turns OFF.

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.542)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.40] In speed change processing flag (速度変更処理中フラグ) (11.7 / original p.542)

Stores whether the in speed change is in progress or not.

| Storage value | In speed change processing flag |
|---|---|
| 0 | Not in speed change (OFF) |
| 1 | In speed change (ON) |

- The speed change process flag turns ON when the speed is changed during positioning control.
- After the speed change process is completed or when deceleration starts with the stop signal during the speed change process, the in speed change process flag turns OFF.

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.542)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.41] Special start repetition counter (特殊始動繰返しカウンタ) (11.7 / original p.543)

- This area stores the remaining number of repetitions during "repetitions" specific to special starting.
- The value stored is 0 to 255.
- The count is decremented by one (-1) at the loop end.
- The control comes out of the loop when the count reaches "0".
- This area stores "0" within an infinite loop.

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.543)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.42] Control system repetition counter (制御方式繰返しカウンタ) (11.7 / original p.543)

- This area stores the remaining number of repetitions during "repetitions" specific to control system.
- The value stored is 0000H to FFFFH.
- The count is decremented by one (-1) at the loop start.
- The loop is terminated with the positioning data of the control method "LEND", after the counter becomes "0".

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.543)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.43] Start data pointer being executed (実行中始動データポインタ) (11.7 / original p.543)

- This area stores a point No. (1 to 50) attached to the start data currently being executed.
- This area stores "0" after completion of a positioning operation.

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.543)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.44] Positioning data No. being executed (実行中位置決めデータNo.) (11.7 / original p.543)

- This area stores a positioning data No. attached to the positioning data currently being executed.
- The value stored is 1 to 600, and 9001 to 9003.
- This area stores "0" when the JOG/inching operation is executed.

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.543)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.45] Block No. being executed (実行中ブロックNo.) (11.7 / original p.543)

- When the operation is controlled by "block start data", this area stores a block No. (7000 to 7004) attached to the block currently being executed.
- At other times, this area stores "0".

Refresh cycle: At start

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.543)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.46] Last executed positioning data No. (最終実行位置決めデータNo.) (11.7 / original p.544)

- This area stores the positioning data No. attached to the positioning data that was executed last time.
- The value stored is 1 to 600, and 9001 to 9003.
- The value is retained until a new positioning operation is executed.
- This area stores "0" when the JOG/inching operation is executed.

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.544)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.47] Positioning data being executed (実行中位置決めデータ) (11.7 / original p.544)

The details of the positioning data currently being executed (positioning data No. given by "[Md.44] Positioning data No. being executed") are stored in the buffer memory addresses.
n: Axis No. - 1

| Buffer memory address | Stored items | Reference |
|---|---|---|
| 6000+1000n | Positioning identifier | Page 499 [Da.1] Operation pattern to Page 500 [Da.4] Deceleration time No. |
| 6006+1000n<br>6007+1000n | Positioning address/movement amount | Page 501 [Da.6] Positioning address/movement amount |
| 6008+1000n<br>6009+1000n | Arc address | Page 504 [Da.7] Arc address |
| 6004+1000n<br>6005+1000n | Command speed | Page 506 [Da.8] Command speed |
| 6002+1000n | Dwell time/JUMP destination positioning data No. | Page 506 [Da.9] Dwell time/JUMP destination positioning data No. |
| 6001+1000n | M code/Condition data No./Number of LOOP to LEND repetitions | Page 507 [Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| 71000+1000n<br>71001+1000n | Axis to be interpolated | Page 508 [Da.20] Axis to be interpolated No.1 to [Da.22] Axis to be interpolated No.3 |

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.544)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.48] Deceleration start flag (減速開始フラグ) (11.7 / original p.544)

- "1" is stored when the constant speed status or acceleration status switches to the deceleration status during position control whose operation pattern is "Positioning complete".
- "0" is stored at the next operation start or manual pulse generator operation enable.

Refresh cycle: Immediate

> **Point**
> This parameter is possible to monitor when "[Cd.41] Deceleration start flag valid" is valid.

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.544)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.62] Amount of the manual pulser driving carrying over movement [FX5-SSC-G] (手動パルサ運転持ち越し移動量[FX5-SSC-G]) (11.7 / original p.545)

When "2: Output the exceeding speed limit value delay" is set in "[Pr.122] Manual pulse generator speed limit mode", this area stores the carrying over movement amount which exceeds "[Pr.123] Manual pulse generator speed limit value".
As shown in the diagram below, the hexadecimal monitor value is changed to a decimal integer value. The decimal integer value can be converted into other units by multiplying said value by the following conversion values.

[Figure] Reading the 32-bit monitor value (original p.545)
- The low-order buffer memory (b15 to b0) is split every 4 bits into E (b15 to b12), F (b11 to b8), G (b7 to b4), H (b3 to b0), shown as the upper row "E F G H" of the monitor value.
- The high-order buffer memory (b31 to b16) is split every 4 bits into A (b31 to b28), B (b27 to b24), C (b23 to b20), D (b19 to b16), shown as the lower row "A B C D" of the monitor value.
- ◇Sorting → "(High-order buffer memory) A B C D" "(Low-order buffer memory) E F G H" in this order.
- ◇Converted from hexadecimal to decimal → "Decimal integer value".

| Unit | Conversion value |
|---|---|
| μm | × 10^-1 |
| inch | × 10^-5 |
| degree | × 10^-5 |
| pulse | × 10^0 |

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.545)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.100] Home position return re-travel value [FX5-SSC-S] (原点復帰再移動量[FX5-SSC-S]) (11.7 / original p.546)

This area stores the travel distance during the home position return travel to the zero point that was executed last time. "0" is stored at machine home position return start. (Depends on the setting unit.)
As shown in the diagram below, the hexadecimal monitor value is changed to a decimal integer value. The decimal integer value can be converted into other units by multiplying said value by the following conversion values.

[Figure] Reading the 32-bit monitor value (original p.546)
- The low-order buffer memory (b15 to b0) is split every 4 bits into E (b15 to b12), F (b11 to b8), G (b7 to b4), H (b3 to b0), shown as the upper row "E F G H" of the monitor value.
- The high-order buffer memory (b31 to b16) is split every 4 bits into A (b31 to b28), B (b27 to b24), C (b23 to b20), D (b19 to b16), shown as the lower row "A B C D" of the monitor value.
- ◇Sorting → "(High-order buffer memory) A B C D" "(Low-order buffer memory) E F G H" in this order.
- ◇Converted from hexadecimal to decimal → "Decimal integer value".

| Unit | Conversion value |
|---|---|
| μm | × 10^-1 |
| inch | × 10^-5 |
| degree | × 10^-5 |
| pulse | × 10^0 |

Ex.
mm
(Buffer memory details × 0.1) μm

Refresh cycle: At conditions established (At home position return re-travel)

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.546)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.101] Actual position value (実現在値) (11.7 / original p.547)

[FX5-SSC-S]
- This area stores the current value (command position value - deviation counter value). (Depends on the setting unit.)

[FX5-SSC-G]
- This area stores the current value (command position value - deviation counter value). (Depends on the setting unit.)

As shown in the diagram below, the hexadecimal monitor value is changed to a decimal integer value. The decimal integer value can be converted into other units by multiplying said value by the following conversion values.

[Figure] Reading the 32-bit monitor value (original p.547)
- The low-order buffer memory (b15 to b0) is split every 4 bits into E (b15 to b12), F (b11 to b8), G (b7 to b4), H (b3 to b0), shown as the upper row "E F G H" of the monitor value.
- The high-order buffer memory (b31 to b16) is split every 4 bits into A (b31 to b28), B (b27 to b24), C (b23 to b20), D (b19 to b16), shown as the lower row "A B C D" of the monitor value.
- ◇Sorting → "(High-order buffer memory) A B C D" "(Low-order buffer memory) E F G H" in this order.
- ◇Converted from hexadecimal to decimal → "Decimal integer value".

| Unit | Conversion value |
|---|---|
| μm | × 10^-1 |
| inch | × 10^-5 |
| degree | × 10^-5 |
| pulse | × 10^0 |

Ex.
mm
(Buffer memory details × 0.1) μm

Refresh cycle: Operation cycle

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.547)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.102] Deviation counter value (偏差カウンタ値) (11.7 / original p.548)

This area stores the droop pulse.
As shown in the diagram below, the hexadecimal monitor value is changed to a decimal integer value. The decimal integer value can be converted into other units by multiplying said value by the following conversion values.

[Figure] Reading the 32-bit monitor value (original p.548)
- The low-order buffer memory (b15 to b0) is split every 4 bits into E (b15 to b12), F (b11 to b8), G (b7 to b4), H (b3 to b0), shown as the upper row "E F G H" of the monitor value.
- The high-order buffer memory (b31 to b16) is split every 4 bits into A (b31 to b28), B (b27 to b24), C (b23 to b20), D (b19 to b16), shown as the lower row "A B C D" of the monitor value.
- ◇Sorting → "(High-order buffer memory) A B C D" "(Low-order buffer memory) E F G H" in this order.
- ◇Converted from hexadecimal to decimal → "Decimal integer value".

| Unit | Conversion value |
|---|---|
| pulse | × 10^0 |

(Buffer memory details) × 1) pulse

*As printed in the original: "(Buffer memory details) × 1) pulse" (unbalanced parentheses; kept as printed).

Refresh cycle: Operation cycle

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.548)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.103] Motor rotation speed (モータ回転数) (11.7 / original p.549)

This area stores the motor speed updated in real time.
As shown in the diagram below, the hexadecimal monitor value is changed to a decimal integer value. The decimal integer value can be converted into other units by multiplying said value by the following conversion values.

[Figure] Reading the 32-bit monitor value (original p.549)
- The low-order buffer memory (b15 to b0) is split every 4 bits into E (b15 to b12), F (b11 to b8), G (b7 to b4), H (b3 to b0), shown as the upper row "E F G H" of the monitor value.
- The high-order buffer memory (b31 to b16) is split every 4 bits into A (b31 to b28), B (b27 to b24), C (b23 to b20), D (b19 to b16), shown as the lower row "A B C D" of the monitor value.
- ◇Sorting → "(High-order buffer memory) A B C D" "(Low-order buffer memory) E F G H" in this order.
- ◇Converted from hexadecimal to decimal → "Decimal integer value".

| Unit | Conversion value |
|---|---|
| r/min*1 | × 10^-2 |

*1 When using a linear servo motor, the unit is mm/s.

Ex.
(Buffer memory × 0.01) r/min

Refresh cycle: Operation cycle

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.549)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.104] Motor current value (モータ電流値) (11.7 / original p.549)

This area stores the current value of the motor.
The storage value converted into other units can be checked by multiplying said value by the following conversion values.

| Unit | Conversion value |
|---|---|
| % | × 10^-1 |

(Buffer memory × 0.1)%

Refresh cycle: Operation cycle

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.549)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.106] Servo amplifier software No. [FX5-SSC-S] (サーボアンプソフトウェア番号[FX5-SSC-S]) (11.7 / original p.550)

- This area stores the software No. of the servo amplifier used.
- This area is update when the control power of the servo amplifier is turned ON.

Ex.
For software No. "-B35W200_A0_"

| Buffer memory address | Monitor value*1 | Stored value |
|---|---|---|
| 2464 | 422D | -B |
| 2465 | 3533 | 35 |
| 2466 | 3257 | W2 |
| 2467 | 3030 | 00 |
| 2468 | 4120 | SPACE A |
| 2469 | 2030 | 0 SPACE |

*1 The monitor value is the character code (ASCII format).

*As printed in the original: "This area is update" (kept as printed).

Refresh cycle: At servo amplifier's power supply ON

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.550)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.107] Parameter error No. [FX5-SSC-S] (パラメータエラー番号[FX5-SSC-S]) (11.7 / original p.551)

- When a servo parameter error occurs, the area that corresponds to the parameter No. affected by the error comes ON.
- When the "[Cd.5] Axis error reset" is set to "1" after remove the error factor of servo amplifier side, the servo alarm is cleared (set to "0").

| SSCNET setting | Servo amplifier | Stored value | Parameter No. |
|---|---|---|---|
| When SSCNETⅢ/H | MR-J5(W)-B | 1 to 48 | PA01 to PA48 |
| When SSCNETⅢ/H | MR-J5(W)-B | 257 to 355 | PB01 to PB99 |
| When SSCNETⅢ/H | MR-J5(W)-B | 513 to 611 | PC01 to PC99 |
| When SSCNETⅢ/H | MR-J5(W)-B | 769 to 867 | PD01 to PD99 |
| When SSCNETⅢ/H | MR-J5(W)-B | 1025 to 1123 | PE01 to PE99 |
| When SSCNETⅢ/H | MR-J5(W)-B | 1281 to 1379 | PF01 to PF99 |
| When SSCNETⅢ/H | MR-J5(W)-B | 1793 to 1891 | Po01 to Po99 |
| When SSCNETⅢ/H | MR-J5(W)-B | 2561 to 2659 | PS01 to PS99 |
| When SSCNETⅢ/H | MR-J5(W)-B | 2817 to 2915 | PL01 to PL99 |
| When SSCNETⅢ/H | MR-J4(W)-B | 1 to 64 | PA01 to PA64 |
| When SSCNETⅢ/H | MR-J4(W)-B | 65 to 128 | PB01 to PB64 |
| When SSCNETⅢ/H | MR-J4(W)-B | 129 to 192 | PC01 to PC64 |
| When SSCNETⅢ/H | MR-J4(W)-B | 193 to 256 | PD01 to PD64 |
| When SSCNETⅢ/H | MR-J4(W)-B | 257 to 320 | PE01 to PE64 |
| When SSCNETⅢ/H | MR-J4(W)-B | 321 to 384 | PF01 to PF64 |
| When SSCNETⅢ/H | MR-J4(W)-B | 385 to 448 | Po01 to Po64 |
| When SSCNETⅢ/H | MR-J4(W)-B | 449 to 512 | PS01 to PS64 |
| When SSCNETⅢ/H | MR-J4(W)-B | 513 to 576 | PL01 to PL64 |
| When SSCNETⅢ | MR-J3(W)-B | 1 to 18 | PA01 to PA18 |
| When SSCNETⅢ | MR-J3(W)-B | 19 to 63 | PB01 to PB45 |
| When SSCNETⅢ | MR-J3(W)-B | 64 to 95 | PC01 to PC32 |
| When SSCNETⅢ | MR-J3(W)-B | 96 to 127 | PD01 to PD32 |
| When SSCNETⅢ | MR-J3(W)-B | 128 to 167 | PE01 to PE40 |
| When SSCNETⅢ | MR-J3(W)-B | 168 to 183 | PF01 to PF16 |
| When SSCNETⅢ | MR-J3(W)-B | 184 to 199 | Po01 to Po16 |
| When SSCNETⅢ | MR-J3(W)-B | 200 to 231 | PS01 to PS32 |
| When SSCNETⅢ | MR-J3(W)-B | 232 | PA19 |

*In the original, "When SSCNETⅢ/H" is a merged cell over 18 rows, "MR-J5(W)-B" over 9 rows, "MR-J4(W)-B" over 9 rows, and "When SSCNETⅢ" / "MR-J3(W)-B" over 9 rows. Expanded to each row.

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.551)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.108] Servo status1 (サーボステータス1) (11.7 / original p.552)

This area stores the servo status1.
- READY ON: Indicates the ready ON/OFF.
- Servo ON: Indicates the servo ON/OFF.
- Control mode: Indicates the control mode of the servo amplifier.
- Gain switching: Turns ON during the gain switching.
- Fully closed loop control switching: Turns ON during the fully closed loop control.
- Servo alarm: Turns ON during the servo alarm.
- In-position: The dwell pulse turns ON within the servo parameter "in-position".
- Torque limit: Turns ON when the servo amplifier is having the torque restricted.
- Absolute position lost: Turns ON when the servo amplifier is lost the absolute position.
- Servo warning: Turns ON during the servo warning.

| Bit | Buffer memory configuration | Stored items | Storage value |
|---|---|---|---|
| b15 | (11) | Servo warning | 0: OFF<br>1: ON |
| b14 | (10) | Absolute position lost | 0: OFF<br>1: ON |
| b13 | (9) | Torque limit | 0: OFF<br>1: ON |
| b12 | (8) | In-position | 0: OFF<br>1: ON |
| b11 to b8 | (no label) | — | — |
| b7 | (7) | Servo alarm | 0: OFF<br>1: ON |
| b6 | (no label) | — | — |
| b5 | (6) | Fully closed loop control switching | 0: OFF<br>1: ON |
| b4 | (5) | Gain switching | 0: OFF<br>1: ON |
| b3 | (4) | Control mode*1 | (see *1) |
| b2 | (3) | Control mode*1 | (see *1) |
| b1 | (2) | Servo ON | 0: OFF<br>1: ON |
| b0 | (1) | READY ON | 0: OFF<br>1: ON |

*In the original, the "Buffer memory configuration" column is a figure of the 16-bit frame with (11) to (8) under b15 to b12, (7) under b7, (6) to (1) under b5 to b0; b11 to b8 and b6 have no label (not marked "Not used" or "0"). "Control mode*1" is a merged cell over (3) and (4), and the "Storage value" cell "0: OFF / 1: ON" is merged over (1) to (11). Expanded to each row.

*1 The control modes are shown below.

| b2 | b3 | Control mode |
|---|---|---|
| 0 | 0 | Position control mode |
| 1 | 0 | Speed control mode |
| 0 | 1 | Torque control mode |

*As printed in the original: "is lost the absolute position" (kept as printed).

Refresh cycle: Operation cycle

> **Point**
> - When the forced stop of controller and servo amplifier occurs, the servo warning is turned ON. When the forced stop is reset, the servo warning is turned OFF.
> - Confirm the status during continuous operation to torque control mode with "[Md.125] Servo status3".

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.552)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.109] Regenerative load ratio/Optional data monitor output 1 (回生負荷率／任意データモニタ出力1) (11.7 / original p.553)

- The rate of regenerative power to the allowable regenerative power is indicated as a percentage.
- When the regenerative option is used, the rate to the allowable regenerative power of the option is indicated.

(Buffer memory) %

[FX5-SSC-S]
- This area stores the content set in "[Pr.91] Optional data monitor: Data type setting 1" at optional data monitor data type setting.

[FX5-SSC-G]
- This area stores the content set in "[Pr.91] Optional data monitor: Data type setting 1" and "[Pr.591] Optional data monitor: Data type expansion setting 1" at optional data monitor data type setting.

Refresh cycle: Operation cycle

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.553)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.110] Effective load torque/Optional data monitor output 2 (実効負荷率／任意データモニタ出力2) (11.7 / original p.553)

- The continuous effective load current is indicated.
- The effective value for the past 15 seconds is displayed, with the rated current being 100%.

(Buffer memory) %

[FX5-SSC-S]
- This area stores the content set in "[Pr.92] Optional data monitor: Data type setting 2" at optional data monitor data type setting.

[FX5-SSC-G]
- This area stores the content set in "[Pr.92] Optional data monitor: Data type setting 2" and "[Pr.592] Optional data monitor: Data type expansion setting 2" at optional data monitor data type setting.

Refresh cycle: Operation cycle

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.553)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.111] Peak torque ratio/Optional data monitor output 3 (ピーク負荷率／任意データモニタ出力3) (11.7 / original p.553)

- The maximum torque is indicated. (Holding value)
- The peak values for the past 15 seconds are indicated, rated torque being 100%.

(Buffer memory) %

[FX5-SSC-S]
- This area stores the content set in "[Pr.93] Optional data monitor: Data type setting 3" at optional data monitor data type setting.

[FX5-SSC-G]
- This area stores the content set in "[Pr.93] Optional data monitor: Data type setting 3" and "[Pr.593] Optional data monitor: Data type expansion setting 3" at optional data monitor data type setting.

Refresh cycle: Operation cycle

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.553)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.112] Optional data monitor output 4 (任意データモニタ出力4) (11.7 / original p.554)

- This area stores the content set in "[Pr.94] Optional data monitor: Data type setting 4" at optional data monitor data type setting. ("0" is stored when the optional data monitor data type is not set.)

[FX5-SSC-G]
- This area stores the content set in "[Pr.94] Optional data monitor: Data type setting 4" and "[Pr.594] Optional data monitor: Data type expansion setting 4" at optional data monitor data type setting.

*In the original, the first bullet has no "[FX5-SSC-S]" label (unlike [Md.109] to [Md.111]); kept as printed.

Refresh cycle: Operation cycle

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.554)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.113] Semi/Fully closed loop status (セミ・フル状態) (11.7 / original p.554)

The switching status of semi closed loop control/fully closed loop control is indicated.

| Storage value | Semi/Fully closed loop status |
|---|---|
| 0 | In semi closed loop control |
| 1 | In fully closed loop control |

Refresh cycle: Operation cycle

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.554)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.114] Servo alarm (サーボアラーム) (11.7 / original p.555)

[FX5-SSC-S]
- This area stores the servo alarm code and servo warning code displayed in LED of servo amplifier.
- When the "[Cd.5] Axis error reset" is set to "1" after removing the cause of an error on the servo amplifier side, the servo alarm is cleared (set to "0").

Ex.
●When SSCNET setting is SSCNETⅢ/H
- For MR-J5(W)-B
  When the servo alarm "AL035.1 Command frequency error" occurs on the servo amplifier, "0351H" is stored.
- For MR-J4(W)-B
  When the servo alarm "AL35.1 Command frequency error" occurs on the servo amplifier, "0351H" is stored.

[Figure] Servo alarm LED display and monitor value, SSCNETⅢ/H (original p.555)
- LED display of MR-J5(W)-B: "Alarm No. display" shows "0 3 5." and then (arrow) "Alarm details display" shows "_ _ . 1". The "3 5" of the alarm No. display and the "1" of the alarm details display go to the monitor value "0 3 5 1".
- LED display of MR-J4(W)-B: "3 5 . 1". The "3 5" and the "1" go to the monitor value "0 3 5 1".

●When SSCNET setting is SSCNETⅢ
For MR-J3(W)-B
When the servo alarm "AL35 Command frequency error" occurs on the servo amplifier, "0035H" is stored.

[Figure] Servo alarm LED display and monitor value, SSCNETⅢ (original p.555)
- LED display of MR-J3(W)-B: "_ 3 5". The "3 5" goes to the monitor value "0 0 3 5".

[FX5-SSC-G]
- When a servo amplifier alarm/warning occurs, the alarm/warning No. is stored.
- When the "[Cd.5] Axis error reset" is set to "1" after removing the cause of an alarm/warning on the servo amplifier side, the servo alarm is cleared (set to 0).

Ex.
For MR-J5(W)-G
When the servo alarm [AL35.1 Command frequency error] occurs on the drive unit, "0035H" is stored.

[Figure] Servo alarm LED display and monitor value, FX5-SSC-G (original p.555)
- LED display of MR-J5(W)-B: "Alarm No. display" shows "_ 3 5." → the "3 5" goes to the monitor value "0 0 3 5" labeled "Servo alarm".
- Shown grayed out: "Alarm details display" "_ _ . 1" → monitor value "0 0 0 1" labeled "Servo alarm detail information" (stored in [Md.115]).
- *As printed in the original: the figure label reads "LED display of MR-J5(W)-B" although the example text is "For MR-J5(W)-G" (kept as printed).

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.555)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.115] Servo alarm detail number [FX5-SSC-G] (サーボアラーム詳細番号[FX5-SSC-G]) (11.7 / original p.556)

- When a servo amplifier alarm/warning occurs, the alarm/warning No. is stored.
- When the "[Cd.5] Axis error reset" is set to "1" after removing the cause of an alarm/warning on the servo amplifier side, the servo alarm detail number is cleared (set to 0).

Ex.
For MR-J5(W)-G
When the servo alarm [AL35.1 Command frequency error] occurs on the drive unit, "0001H" is stored.

[Figure] Servo alarm detail number LED display and monitor value (original p.556)
- Shown grayed out: LED display of MR-J5(W)-B "Alarm No. display" "_ 3 5." → monitor value "0 0 3 5" labeled "Servo alarm".
- "Alarm details display" "_ _ . 1" → the "1" goes to the monitor value "0 0 0 1" labeled "Servo alarm detail information".
- *As printed in the original: the figure label reads "LED display of MR-J5(W)-B" although the example text is "For MR-J5(W)-G" (kept as printed).

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.556)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.116] Encoder option information (エンコーダオプション情報) (11.7 / original p.556)

The option information of encoder is indicated.

| Bit | Buffer memory configuration | Stored items | Storage value |
|---|---|---|---|
| b15 to b10 | (no label) | — | — |
| b9 | (5) | Compatible with scale measurement mode | 0: Incompatible<br>1: Compatible |
| b8 | (4) | Compatible with continuous operation to torque control | 0: Incompatible<br>1: Compatible |
| b7 | (3) | Connecting to magnetism type encoder [FX5-SSC-S] | 0: No connection<br>1: Magnetism type encoder |
| b6 | (2) | Connecting to single-revolution ABS encoder [FX5-SSC-S] | 0: Multi-revolution ABS/INC<br>1: Single-revolution ABS |
| b5 to b4 | (no label) | — | — |
| b3 | (1) | ABS/INC mode distinction for magnetism type encoder [FX5-SSC-S] | 0: INC mode<br>1: ABS mode |
| b2 to b0 | (no label) | — | — |

*In the original, the "Buffer memory configuration" column is a figure of the 16-bit frame with (5) to (2) under b9 to b6 and (1) under b3; other bits have no label. The "Storage value" cell "0: Incompatible / 1: Compatible" is merged over (4) and (5). Expanded to each row.

Refresh cycle: At servo amplifier's power supply ON

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.556)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.117] Statusword [FX5-SSC-G] (Statusword[FX5-SSC-G]) (11.7 / original p.557)

Statusword is stored.

| Bit | Buffer memory configuration | Stored items | Storage value |
|---|---|---|---|
| b15 to b14 | (no label) | — | — |
| b13 | (11) | Operation mode specific | 0: OFF<br>1: ON |
| b12 | (10) | Operation mode specific | 0: OFF<br>1: ON |
| b11 to b10 | (no label) | — | — |
| b9 | (9) | Remote | 0: OFF<br>1: ON |
| b8 | (no label) | — | — |
| b7 | (8) | Warning | 0: OFF<br>1: ON |
| b6 | (7) | Switch on disabled | 0: OFF<br>1: ON |
| b5 | (6) | Quick stop | 0: OFF<br>1: ON |
| b4 | (5) | Voltage enabled | 0: OFF<br>1: ON |
| b3 | (4) | Fault | 0: OFF<br>1: ON |
| b2 | (3) | Operation enabled | 0: OFF<br>1: ON |
| b1 | (2) | Switched on | 0: OFF<br>1: ON |
| b0 | (1) | Ready to switch on | 0: OFF<br>1: ON |

*In the original, the "Buffer memory configuration" column is a figure of the 16-bit frame with (11) and (10) under b13 and b12, (9) under b9, (8) to (1) under b7 to b0; other bits have no label. "Operation mode specific" is a merged cell over (10) and (11), and the "Storage value" cell is merged over (1) to (11). Expanded to each row.

Refresh cycle: Operation cycle

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.557)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.119] Servo status2 (サーボステータス2) (11.7 / original p.557)

This area stores the servo status2.
- Zero point pass: Turns ON if the zero point of the encoder has been passed even once.
- Zero speed: Turns ON when the motor speed is lower than the servo parameter "zero speed."
- Speed limit: Turns ON during the speed limit in torque control mode.
- PID control: Turns ON when the servo amplifier is PID control.

| Bit | Buffer memory configuration | Stored items | Storage value |
|---|---|---|---|
| b15 to b9 | (no label) | — | — |
| b8 | (4) | PID control | 0: OFF<br>1: ON |
| b7 to b5 | (no label) | — | — |
| b4 | (3) | Speed limit | 0: OFF<br>1: ON |
| b3 | (2) | Zero speed | 0: OFF<br>1: ON |
| b2 to b1 | (no label) | — | — |
| b0 | (1) | Zero point pass | 0: OFF<br>1: ON |

*In the original, the "Buffer memory configuration" column is a figure of the 16-bit frame with (4) under b8, (3) under b4, (2) under b3 and (1) under b0; other bits have no label. The "Storage value" cell is merged over (1) to (4). Expanded to each row.

Refresh cycle: Operation cycle

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.557)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.120] Reverse torque limit stored value (逆転トルク制限格納値) (11.7 / original p.558)

[FX5-SSC-S]
"[Pr.17] Torque limit setting value", "[Cd.101] Torque output setting value", "[Cd.113] New reverse torque value", or "[Pr.54] Home position return torque limit value" is stored.
- The stored value 1 to 10000 (× 0.1%).
- At the positioning start/JOG operation start/manual pulse generator operation: "[Pr.17] Torque limit setting value" or "[Cd.101] Torque output setting value" is stored.
- When a value is set in "[Cd.22] New torque value/forward new torque value" or "[Cd.113] New reverse torque value" during operation.: "[Cd.22] New torque value/forward new torque value" is stored when "0" is set in "[Cd.112] Torque change function switching request". "[Cd.113] New reverse torque value" is stored when "1" is set in "[Cd.112] Torque change function switching request".
- At the home position return: "[Pr.17] Torque limit setting value" or "[Cd.101] Torque output setting value" is stored. However, "[Pr.54] Home position return torque limit value" is stored after the speed reaches "[Pr.47] Creep speed".

[FX5-SSC-G]
"[Pr.17] Torque limit setting value", "[Cd.101] Torque output setting value", or "[Cd.113] New reverse torque value" is stored.
- The stored value 1 to 10000 (× 0.1%).
- At the positioning start/JOG operation start/manual pulse generator operation: "[Pr.17] Torque limit setting value" or "[Cd.101] Torque output setting value" is stored.
- When a value is set in "[Cd.22] New torque value/forward new torque value" or "[Cd.113] New reverse torque value" during operation.: "[Cd.22] New torque value/forward new torque value" is stored when "0" is set in "[Cd.112] Torque change function switching request". "[Cd.113] New reverse torque value" is stored when "1" is set in "[Cd.112] Torque change function switching request".

Refresh cycle: Immediate

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.558)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.122] Speed during command (指令中速度) (11.7 / original p.558)

- This area stores the command speed during speed control mode.
- This area stores the command speed during continuous operation to torque control mode.
- "0" is stored other than during speed control mode or continuous operation to torque control mode.

The storage value converted into other units can be checked by multiplying said value by the following conversion values.

| Unit | Conversion value |
|---|---|
| mm/min | × 10^-2 |
| inch/min | × 10^-3 |
| degree/min | × 10^-3*1 |
| pulse/s | × 10^0 |

*1 When "[Pr.83] Speed control 10 × multiplier setting for degree axis" is valid, becomes " × 10^-2.

*As printed in the original: the *1 note has no closing quotation mark after "× 10^-2" (kept as printed).

Refresh cycle: Operation cycle (Only at the speed control mode and the continuous operation to torque control mode)

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.558)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.123] Torque during command (指令中トルク) (11.7 / original p.559)

- This area stores the command torque during torque control mode. (Buffer memory × 0.1)%
- This area stores the command torque during continuous operation to torque control mode.
- "0" is stored other than during torque control mode or continuous operation to torque control mode.

The storage value converted into other units can be checked by multiplying said value by the following conversion values.

| Unit | Conversion value |
|---|---|
| % | × 10^-1 |

Refresh cycle: Operation cycle (Only at the torque control mode and the continuous operation to torque control mode)

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.559)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.124] Control mode switching status (制御モード切換え状態) (11.7 / original p.559)

This area stores the switching status of control mode.

| Unit | Control mode switching status |
|---|---|
| 0 | Not during control mode switching |
| 1 | Position control mode ⇔ continuous operation to torque control mode, speed control mode ⇔ continuous operation to torque control mode switching |
| 2 | Waiting for the completion of control mode switching condition |

*As printed in the original: the first column header reads "Unit" (the column holds storage values; kept as printed).

Refresh cycle: Operation cycle (Only at the continuous operation to torque control mode)

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.559)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.125] Servo status3 (サーボステータス3) (11.7 / original p.559)

- This area stores the servo status3.
- Touch probe1 valid: Turn ON when the touch probe function using TPR1 signal of the servo amplifier is enabled. [FX5-SSC-G]
- Continuous operation to torque control mode: Turn ON when the continuous operation to torque control mode.
- Unsupported control mode: Turn ON when the unsupported control mode. [FX5-SSC-G]

| Bit | Buffer memory configuration | Servo status3 | Storage value |
|---|---|---|---|
| b15 | (3) | Unsupported control mode [FX5-SSC-G] | 0: OFF<br>1: ON |
| b14 | (2) | Continuous operation to torque control mode | 0: OFF<br>1: ON |
| b13 to b12 | (no label) | — | — |
| b11 | (1) | Touch probe1 valid [FX5-SSC-G] | 0: OFF<br>1: ON |
| b10 to b0 | (no label) | — | — |

*In the original, the "Buffer memory configuration" column is a figure of the 16-bit frame with (3) under b15, (2) under b14 and (1) under b11; other bits have no label. The "Storage value" cell is merged over (1) to (3). Expanded to each row.

Refresh cycle: Operation cycle

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.559)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.126] Servo status4 [FX5-SSC-G] (サーボステータス4[FX5-SSC-G]) (11.7 / original p.560)

- Servo status4 is stored.
- Toggle status for latch completion at the rising edge of touch probe 1/Toggle status for latch completion at the falling edge of touch probe 1: When TPR1 of the servo amplifier side is enabled, the status will change every time stamp is stored by the signal detection.

| Bit | Buffer memory configuration | Servo status4 | Storage value |
|---|---|---|---|
| b15 | (no label) | — | — |
| b14 | (2) | Toggle status for latch completion at the falling edge of touch probe 1 | 0: OFF<br>1: ON |
| b13 | (1) | Toggle status for latch completion at the rising edge of touch probe 1 | 0: OFF<br>1: ON |
| b12 to b0 | (no label) | — | — |

*In the original, the "Buffer memory configuration" column is a figure of the 16-bit frame with (2) under b14 and (1) under b13; other bits have no label. The "Storage value" cell is merged over (1) and (2). Expanded to each row.

Refresh cycle: Operation cycle

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.560)

For buffer memory in this area, refer to the following.
→Page 426 Axis monitor data

#### [Md.127] Servo status5 [FX5-SSC-S] (サーボステータス5[FX5-SSC-S]) (11.7 / original p.560)

- This area stores the servo status5.
- Gain switching 2: Turns ON during gain switching 2

| Bit | Buffer memory configuration | Servo status5 | Storage value |
|---|---|---|---|
| b15 to b5 | (no label) | — | — |
| b4 | (1) | Gain switching 2 | 0: OFF<br>1: ON |
| b3 to b0 | (no label) | — | — |

*In the original, the "Buffer memory configuration" column is a figure of the 16-bit frame with (1) under b4; other bits have no label.

Refresh cycle: Operation cycle

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.560)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.160] Optional SDO transfer result 1 [FX5-SSC-G] (任意SDO転送結果1[FX5-SSC-G]) (11.7 / original p.560)

Used in the servo transient transmission function. For details, refer to the following.
→Page 381 Servo Transient Transmission Function [FX5-SSC-G]

Refresh cycle: At request (Command request)

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.560)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.164] Optional SDO transfer status 1 [FX5-SSC-G] (任意SDO転送ステータス1[FX5-SSC-G]) (11.7 / original p.560)

Used in the servo transient transmission function. For details, refer to the following.
→Page 381 Servo Transient Transmission Function [FX5-SSC-G]

Refresh cycle: At request (Command request)

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.560)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.190] Controller position value restoration complete status [FX5-SSC-G] (コントローラ現在値復元完了状態[FX5-SSC-G]) (11.7 / original p.561)

The completion status of the controller current value restoration is stored.
The status becomes "0: Incomplete restoration" when the device is disconnected.

| Storage value | Controller position value restoration complete status |
|---|---|
| 0 | Incomplete restoration |
| 1 | Complete INC restoration |
| 2 | Complete ABS restoration (64-bit Restoration_Based on Backup Location) |
| 3 | Complete ABS restoration (32-bit Restoration_Based on Backup Location) |

Refresh cycle: 16.0 [ms]

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.561)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.500] Servo status7 [FX5-SSC-S] (サーボステータス7[FX5-SSC-S]) (11.7 / original p.561)

This area stores the servo status7.

| Bit | Buffer memory configuration | Stored items | Storage value |
|---|---|---|---|
| b15 to b10 | (no label) | — | — |
| b9 | (1) | Driver operation alarm | 0: OFF<br>1: ON |
| b8 to b0 | (no label) | — | — |

*In the original, the "Buffer memory configuration" column is a figure of the 16-bit frame with (1) under b9; other bits have no label.

Refresh cycle: Operation cycle

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.561)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.502] Driver operation alarm No. [FX5-SSC-S] (ドライバ運転アラーム番号[FX5-SSC-S]) (11.7 / original p.561)

- This area stores the driver operation alarm No.
- Upper 2 digits: Driver operation alarm (b8 to b15)
- Lower 2 digits: Detailed No. (b0 to b7)

Refresh cycle: Immediate

Ex.
When the driver operation alarm is "10H" and the detailed No. is "23H", "1023H" is displayed.

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.561)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

#### [Md.514] HPR operating status [FX5-SSC-G] (原点復帰動作状態[FX5-SSC-G]) (11.7 / original p.562)

The HPR (home position return) operating status is stored

| Storage value | HPR operating status |
|---|---|
| FFFFH | The servo amplifier is not set to the home position return mode |
| 0000H | Home position return is in progress |
| 0001H | Home position return is interrupted or not started |
| 0002H | Home position return is completed, but the target has not been reached. |
| 0003H | Home position return is completed successfully |
| 0004H | Home position return error occurred, speed is not 0 |
| 0005H | Home position return error occurred, speed is 0 |

Refresh cycle: Operation cycle

##### ■Buffer memory address (バッファメモリアドレス) (11.7 / original p.562)

Refer to the following for the buffer memory address in this area.
→Page 426 Axis monitor data

## 11.8 Control Data (制御データ) (11.8 / original p.563-602)

The setting items of the control data are explained in this section.

(Notation for this section: "Fetch cycle: ..." lines are underlined in the original. Units printed as "(×10 with superscript)" are written as "× 10^-n". "Ex." marks an example box of the original.)

### System control data (システム制御データ) (11.8 / original p.563-570)

#### [Cd.1] Flash ROM write request ([Cd.1]フラッシュ ROM書込み要求) (11.8 / original p.563)

- Writes not only "positioning data (No.1 to 600)" and "block start data (No.7000 to 7004)" stored in the buffer memory/internal memory area, but also "parameters" and "servo parameters" to the flash ROM/internal memory (nonvolatile).
- The Simple Motion module/Motion module resets the value to "0" automatically when the write access completes. (This indicates the completion of write operation.)

Fetch cycle: 103 [ms] [FX5-SSC-S]
Fetch cycle: 116 [ms] [FX5-SSC-G]

> **Point**
> - Do not turn the power OFF or reset the CPU module while writing to the flash ROM. If the power is turned OFF or the CPU module is reset to forcibly end the process, the data backed up in the flash ROM will be lost.
> - Do not write the data to the buffer memory before writing to the flash ROM is completed.
> - The number of writes to the flash ROM with the program is 25 max. while the power is turned ON. Writing to the flash ROM beyond 25 times will cause the error "Flash ROM write number error" (error code: 1080H). Refer to →Page 753 List of Error Codes for details.
> - Monitoring is the number of writes to the flash ROM after the power is switched ON by the "[Md.19] Number of write accesses to flash ROM".

##### ■Setting value (設定値) (11.8 / original p.563)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 1 | Flash ROM write request |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.563)

Refer to the following for the buffer memory address in this area.
→Page 428 System control data

##### ■Default value (初期値) (11.8 / original p.563)

Set to "0".

#### [Cd.2] Parameter initialization request ([Cd.2]パラメータ初期化要求) (11.8 / original p.564)

- Requests initialization of setting data.
- The Simple Motion module/Motion module resets the value to "0" automatically when the initialization completes. (This indicates the completion of the initialization.)

Refer to the following for initialized setting data.
→Page 317 Parameter Initialization Function
Initialization: Resetting of setting data to default values

Fetch cycle: 103 [ms] [FX5-SSC-S]
Fetch cycle: 116 [ms] [FX5-SSC-G]

> **Point**
> After completing the initialization of setting data, switch the power ON or reset the CPU module.

##### ■Setting value (設定値) (11.8 / original p.564)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 1 | Parameter initialization request |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.564)

Refer to the following for the buffer memory address in this area.
→Page 428 System control data

##### ■Default value (初期値) (11.8 / original p.564)

Set to "0".

#### [Cd.41] Deceleration start flag valid ([Cd.41]減速開始フラグ有効) (11.8 / original p.564)

Sets whether "[Md.48] Deceleration start flag" is made valid or invalid.

Fetch cycle: At "[Cd.190] PLC READY" OFF to ON

> **Point**
> The "[Cd.41] Deceleration start flag valid" become valid when the "[Cd.190] PLC READY" turns from OFF to ON.
> *(Note: "become valid" is as printed in the original.)*

##### ■Setting value (設定値) (11.8 / original p.564)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 0 | Deceleration start flag invalid |
| 1 | Deceleration start flag valid |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.564)

Refer to the following for the buffer memory address in this area.
→Page 428 System control data

##### ■Default value (初期値) (11.8 / original p.564)

Set to "0".

#### [Cd.42] Stop command processing for deceleration stop selection ([Cd.42]減速停止時停止指令処理選択) (11.8 / original p.565)

Sets the stop command processing for deceleration stop function (deceleration curve re-processing/deceleration curve continuation).

Fetch cycle: At conditions established (At deceleration stop causes occurrence)

##### ■Setting value (設定値) (11.8 / original p.565)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 0 | Deceleration curve re-processing |
| 1 | Deceleration curve continuation |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.565)

Refer to the following for the buffer memory address in this area.
→Page 428 System control data

##### ■Default value (初期値) (11.8 / original p.565)

Set to "0".

#### [Cd.44] External input signal operation device (Axis 1 to 8) ([Cd.44]外部入力信号操作デバイス(1～8軸)) (11.8 / original p.566)

Operates the external input signal status (Upper/lower limit signal, proximity dog signal, stop signal) of the Simple Motion module/Motion module when "2" is set in "[Pr.116] FLS signal selection", "[Pr.117] RLS signal selection", "[Pr.118] DOG signal selection", and "[Pr.119] STOP signal selection".

Fetch cycle: Operation cycle

##### ■Setting value (設定値) (11.8 / original p.566)

- Set with a hexadecimal.

| Buffer memory | Bit | Details | Setting value |
|---|---|---|---|
| 5928 | b0 | Axis 1 Upper limit signal (FLS) | When "[Pr.22] Input signal logic selection" is negative logic<br>0: OFF<br>1: ON<br>When "[Pr.22] Input signal logic selection" is positive logic<br>0: ON<br>1: OFF |
| 5928 | b1 | Axis 1 Lower limit signal (RLS) | (same as above) |
| 5928 | b2 | Axis 1 Proximity dog signal (DOG) | (same as above) |
| 5928 | b3 | Axis 1 STOP signal (STOP) | (same as above) |
| 5928 | b4 | Axis 2 Upper limit signal (FLS) | (same as above) |
| 5928 | b5 | Axis 2 Lower limit signal (RLS) | (same as above) |
| 5928 | b6 | Axis 2 Proximity dog signal (DOG) | (same as above) |
| 5928 | b7 | Axis 2 STOP signal (STOP) | (same as above) |
| 5928 | b8 | Axis 3 Upper limit signal (FLS) | (same as above) |
| 5928 | b9 | Axis 3 Lower limit signal (RLS) | (same as above) |
| 5928 | b10 | Axis 3 Proximity dog signal (DOG) | (same as above) |
| 5928 | b11 | Axis 3 STOP signal (STOP) | (same as above) |
| 5928 | b12 | Axis 4 Upper limit signal (FLS) | (same as above) |
| 5928 | b13 | Axis 4 Lower limit signal (RLS) | (same as above) |
| 5928 | b14 | Axis 4 Proximity dog signal (DOG) | (same as above) |
| 5928 | b15 | Axis 4 STOP signal (STOP) | (same as above) |
| 5929 | b0 | Axis 5 Upper limit signal (FLS) | (same as above) |
| 5929 | b1 | Axis 5 Lower limit signal (RLS) | (same as above) |
| 5929 | b2 | Axis 5 Proximity dog signal (DOG) | (same as above) |
| 5929 | b3 | Axis 5 STOP signal (STOP) | (same as above) |
| 5929 | b4 | Axis 6 Upper limit signal (FLS) | (same as above) |
| 5929 | b5 | Axis 6 Lower limit signal (RLS) | (same as above) |
| 5929 | b6 | Axis 6 Proximity dog signal (DOG) | (same as above) |
| 5929 | b7 | Axis 6 STOP signal (STOP) | (same as above) |
| 5929 | b8 | Axis 7 Upper limit signal (FLS) | (same as above) |
| 5929 | b9 | Axis 7 Lower limit signal (RLS) | (same as above) |
| 5929 | b10 | Axis 7 Proximity dog signal (DOG) | (same as above) |
| 5929 | b11 | Axis 7 STOP signal (STOP) | (same as above) |
| 5929 | b12 | Axis 8 Upper limit signal (FLS) | (same as above) |
| 5929 | b13 | Axis 8 Lower limit signal (RLS) | (same as above) |
| 5929 | b14 | Axis 8 Proximity dog signal (DOG) | (same as above) |
| 5929 | b15 | Axis 8 STOP signal (STOP) | (same as above) |

*In the original, the "Buffer memory" header spans the address column and the bit column; the address cell 5928 is merged over b0 to b15 and 5929 over b0 to b15; the "Setting value" cell is one merged cell over all 32 rows. Expanded to each row ("(same as above)" = identical to the first row).

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.566)

Refer to the following for the buffer memory address in this area.
→Page 428 System control data

##### ■Default value (初期値) (11.8 / original p.566)

Set to "0000H".

#### [Cd.55] Input value for manual pulse generator via CPU [FX5-SSC-G] ([Cd.55]CPU経由手動パルサ入力値[FX5-SSC-G]) (11.8 / original p.567)

- Set the values used as the input values for the manual pulse generator via CPU in order.
- Set the input values with the high speed counter function of the CPU module.

Fetch cycle: 8.0 [ms]

- Although "[Cd.55] Input value for manual pulse generator via CPU" is imported every 8.0 ms, synchronization with the scan time of the CPU module is not performed, so the speed change of the axis may become large if the refresh cycle of "[Cd.55] Input value for manual pulse generator via CPU" is slow. Use the following methods to smooth the speed change.
  - Refresh "[Cd.55] Input value for manual pulse generator via CPU" in a cycle that is 8.0 ms or less.
  - Smooth the speed change by using the smoothing function of "[Pr.156] Manual pulse generator smoothing time constant".
- When executing manual pulser operation using "[Cd.55] Input value for manual pulse generator via CPU", set the following items as shown below in [Module Parameter] → [High Speed I/O] → [Input Function] → [High Speed Counter] → [Detail Setting] of the CPU module.

| Setting items | Setting items (detail) | Setting value |
|---|---|---|
| Use/do not use counter | — | Enable |
| Operation mode | — | Normal mode |
| Pulse input mode | — | Set according to the system. |
| Preset input | Preset input enable/disable | Disable |
| Preset value | — | 0 |
| Enable input | Enable input enable/disable | Disable |
| Ring length setting | Ring length enable/disable | Disable |

*In the original, "Setting items" is a 2-column header; the rows Use/do not use counter, Operation mode, Pulse input mode and Preset value span both columns. Written with "—" in the detail column.

> **Restriction**
> Set the movement amount per fetch cycle of "[Cd.55] Input value for manual pulse generator via CPU" within the range of -2147483648 to 2147483647 pulse. When set to a value outside the range, the movement amount of the manual pulse generator and the movement amount of the outputted value may not match.

##### ■Setting range (設定範囲) (11.8 / original p.567)

- Set with a decimal.

| Setting range of [Cd.55] (Unit) |
|---|
| -2147483648 to 2147483647 (pulse) |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.567)

Refer to the following for the buffer memory address in this area.
→Page 428 System control data

##### ■Default value (初期値) (11.8 / original p.567)

Set to "0".

#### [Cd.102] SSCNET control command [FX5-SSC-S] ([Cd.102]SSCNET制御指令[FX5-SSC-S]) (11.8 / original p.568)

Sets the connect/disconnect command of SSCNET communication.

Fetch cycle: 3.5 [ms]

##### ■Setting value (設定値) (11.8 / original p.568)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 0 | No command |
| Axis No.*1 | Disconnect command of SSCNET communication (Axis No. to be disconnected) |
| -2 | Execute command |
| -10 | Connect command of SSCNET communication |
| Except above setting | Invalid |

*1 1 to the maximum control axes.

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.568)

Refer to the following for the buffer memory address in this area.
→Page 428 System control data

##### ■Default value (初期値) (11.8 / original p.568)

Set to "0".

#### [Cd.137] Amplifier-less operation mode switching request [FX5-SSC-S] ([Cd.137]アンプなし運転モード切換え要求[FX5-SSC-S]) (11.8 / original p.568)

Sets the switching request of the normal operation mode and amplifier-less operation mode.

Fetch cycle: 3.5 [ms]

##### ■Setting value (設定値) (11.8 / original p.568)

- Set with a hexadecimal.

| Setting value | Details |
|---|---|
| ABCDH | Change from normal operation mode to amplifier-less operation mode |
| 0000H | Change from amplifier-less operation mode to normal operation mode |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.568)

Refer to the following for the buffer memory address in this area.
→Page 428 System control data

##### ■Default value (初期値) (11.8 / original p.568)

Set to "0000H".

#### [Cd.158] Forced stop input [FX5-SSC-G] ([Cd.158]緊急停止入力[FX5-SSC-G]) (11.8 / original p.569)

Set the forced stop input information.

Fetch cycle: Operation cycle

##### ■Setting value (設定値) (11.8 / original p.569)

- Set with a hexadecimal.

| Setting value | Details |
|---|---|
| 0000H | Forced stop ON (Forced stop) |
| 0001H | Forced stop OFF (Forced stop release) |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.569)

Refer to the following for the buffer memory address in this area.
→Page 428 System control data

##### ■Default value (初期値) (11.8 / original p.569)

Set to "0000H".

#### [Cd.190] PLC READY ([Cd.190]シーケンサレディ) (11.8 / original p.569)

- This signal notifies the Simple Motion module/Motion module that the CPU module is normal.
  - It is turned ON/OFF with the program.
- When the data (parameter) are changed, the "[Cd.190] PLC READY" is turned OFF depending on the parameter.
- The following processes are carried out when the "[Cd.190] PLC READY" turns from OFF → ON.
  - The parameter setting range is checked.
  - The READY signal ([Md.140] Module status: b0) turns ON.
- The following processes are carried out when the "[Cd.190] PLC READY" turns from ON → OFF. In these cases, the OFF time should be set to 100 ms or more.
  - The READY signal ([Md.140] Module status: b0) turns OFF.
  - The operating axis stops.
  - The M code ON signal ([Md.31] Status: b12) for each axis turns OFF, and "0" is stored in "[Md.25] Valid M code".
- When parameters or positioning data (No.1 to 600) are written from the engineering tool or CPU module to the flash ROM, the "[Cd.190] PLC READY" will turn OFF.

(The indented items are shown in ruled boxes under each bullet in the original.)

Fetch cycle: Operation cycle

##### ■Setting value (設定値) (11.8 / original p.569)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 1 | PLC READY ON |
| Other than 1 | PLC READY OFF |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.569)

Refer to the following for the buffer memory address in this area.
→Page 428 System control data

##### ■Default value (初期値) (11.8 / original p.569)

Set to "0".

#### [Cd.191] All axis servo ON ([Cd.191]全軸サーボON) (11.8 / original p.570)

Sets all the servo amplifiers connected to the Simple Motion module/Motion module.

Fetch cycle: Operation cycle

##### ■Setting value (設定値) (11.8 / original p.570)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 1 | Servo ON |
| Other than 1 | Servo OFF |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.570)

Refer to the following for the buffer memory address in this area.
→Page 428 System control data

##### ■Default value (初期値) (11.8 / original p.570)

Set to "0".

### Axis control data (軸制御データ) (11.8 / original p.571-601)

#### [Cd.3] Positioning start No. ([Cd.3]位置決め始動番号) (11.8 / original p.571)

Sets the positioning start No. (Only 1 to 600 for the Pre-reading start function. For details, refer to →Page 276 Pre-reading start function.)

Fetch cycle: At start

##### ■Setting value (設定値) (11.8 / original p.571)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 1 to 600 | Positioning data No. |
| 7000 to 7004 | Block start designation |
| 9001 | Machine home position return |
| 9002 | Fast-home position return |
| 9003 | Current value changing |
| 9004 | Simultaneous starting of multiple axes |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.571)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.571)

Set to "0".

#### [Cd.4] Positioning starting point No. ([Cd.4]位置決め始動ポイント番号) (11.8 / original p.571)

- Sets a "starting point No." (1 to 50) if block start data is used for positioning. (Handled as "1" if the value other than 1 to 50 is set.)
- The Simple Motion module/Motion module resets the value to "0" automatically when the continuous operation is interrupted.

Fetch cycle: At start

##### ■Setting range (設定範囲) (11.8 / original p.571)

- Set with a decimal.

| Setting range of [Cd.4] |
|---|
| 1 to 50 |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.571)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.571)

Set to "0".

#### [Cd.5] Axis error reset ([Cd.5]軸エラーリセット) (11.8 / original p.572)

- Clears the axis error detection, axis error No., axis warning detection and axis warning No.
- When the axis operation state of Simple Motion module/Motion module is "in error occurrence", the error is cleared and the Simple Motion module/Motion module is returned to the "waiting" state.
- The Simple Motion module/Motion module resets the value to "0" automatically after the axis error reset is completed. (Indicates that the axis error reset is completed.)

[FX5-SSC-S]
- Clears both Simple Motion module/Motion module errors and servo amplifier errors by axis error reset. (Some servo amplifier alarms cannot be reset even if error reset is requested. At the time, "0" is not stored in "[Cd.5] Axis error reset" by the Simple Motion module. It remains "1". Set "0" in "[Cd.5] Axis error reset" and then set "1" to execute the error reset again by user side. For details, refer to each servo amplifier instruction manual.)

[FX5-SSC-G]
- Clears both Motion module errors and servo amplifier errors by axis error reset. (Some servo amplifier alarms cannot be reset even if error reset is requested. At the time, "0" is not stored in "[Cd.5] Axis error reset" by the Simple Motion module. It remains "1". Set "0" in "[Cd.5] Axis error reset" and then set "1" to execute the error reset again by user side. For details, refer to each servo amplifier manual.)
- Errors cannot be reset during the forced stop. Execute the axis error reset while the forced stop is in released status.

*(Note: "by the Simple Motion module" in the [FX5-SSC-G] item is as printed in the original.)*

Fetch cycle: 14.2 [ms] [FX5-SSC-S]
Fetch cycle: 16.0 [ms] [FX5-SSC-G]

##### ■Setting value (設定値) (11.8 / original p.572)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 1 | Axis error is reset. |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.572)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.572)

Set to "0".

#### [Cd.6] Restart command ([Cd.6]再始動指令) (11.8 / original p.572)

- When "1" is set in [Cd.6] after the positioning is stopped for any reason (while the axis operation state is "stopped"), the positioning will be carried out again from the stop position to the end point of the stopped positioning data.
- The Simple Motion module/Motion module resets the value to "0" automatically after restart acceptance is completed. (Indicates that the restart acceptance is completed.)

Fetch cycle: 14.2 [ms] [FX5-SSC-S]
Fetch cycle: 16.0 [ms] [FX5-SSC-G]

##### ■Setting value (設定値) (11.8 / original p.572)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 1 | Restarts |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.572)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.572)

Set to "0".

#### [Cd.7] M code OFF request ([Cd.7]MコードOFF要求) (11.8 / original p.573)

- The M code ON signal turns OFF.
- The Simple Motion module/Motion module resets the value to "0" automatically after the M code signal turns OFF. (Indicates that the OFF request is completed.)

Fetch cycle: Operation cycle

##### ■Setting value (設定値) (11.8 / original p.573)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 1 | M code ON signal turns OFF |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.573)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.573)

Set to "0".

#### [Cd.8] External command valid ([Cd.8]外部指令有効) (11.8 / original p.573)

Validates or invalidates external command signals.

Fetch cycle: At request

##### ■Setting value (設定値) (11.8 / original p.573)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 0 | Invalidates an external command. |
| 1 | Validates an external command. |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.573)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.573)

Set to "0".

#### [Cd.9] New position value ([Cd.9]現在値変更値) (11.8 / original p.573)

When changing the command position value using the start No. "9003", use this data item to specify a new feed value.

Fetch cycle: At request

##### ■Setting range (設定範囲) (11.8 / original p.573)

- Set with a decimal.
- The setting value range differs according to the "[Pr.1] Unit setting".

| Setting of "[Pr.1] Unit setting" | Setting value depending on program (unit) |
|---|---|
| 0: mm | -2147483648 to 2147483647 (× 10^-1 mm) |
| 1: inch | -2147483648 to 2147483647 (× 10^-5 inch) |
| 2: degree | 0 to 35999999 (× 10^-5 degree) |
| 3: pulse | -2147483648 to 2147483647 (pulse) |

*(Note: the unit "× 10^-1 mm" in the 0: mm row is as printed in the original; the same row of the other items in this section reads "× 10^-1 μm".)*

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.573)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.573)

Set to "0".

#### [Cd.10] New acceleration time value ([Cd.10]加速時間変更値) (11.8 / original p.574)

When changing the acceleration time during a speed change, use this data item to specify a new acceleration time.

Fetch cycle: At request

##### ■Setting range (設定範囲) (11.8 / original p.574)

- Set with a decimal.

| Setting range of [Cd.10] (unit) |
|---|
| 0 to 8388608 (ms) |

Ex.
When the "[Cd.10] New acceleration time value" is set as "60000 ms", the buffer memory stores "60000".

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.574)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.574)

Set to "0".

#### [Cd.11] New deceleration time value ([Cd.11]減速時間変更値) (11.8 / original p.574)

When changing the deceleration time during a speed change, use this data item to specify a new deceleration time.

Fetch cycle: At request

##### ■Setting range (設定範囲) (11.8 / original p.574)

- Set with a decimal.

| Setting range of [Cd.11] (unit) |
|---|
| 0 to 8388608 (ms) |

Ex.
When the "[Cd.11] New deceleration time value" is set as "60000 ms", the buffer memory stores "60000".

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.574)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.574)

Set to "0".

#### [Cd.12] Accel/decel*1 time change value during speed change, enable/disable ([Cd.12]速度変更時の加減速時間変更値許可／不許可) (11.8 / original p.574)

*1 "Accel/decel" is an abbreviation for "Acceleration/deceleration".

Enables or disables modifications to the acceleration/deceleration time during a speed change.

Fetch cycle: At request

##### ■Setting value (設定値) (11.8 / original p.574)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 1 | Enables modifications to acceleration/deceleration time |
| Other than 1 | Disables modifications to acceleration/deceleration time |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.574)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.574)

Set to "0".

#### [Cd.13] Positioning operation speed override ([Cd.13]位置決め運転速度オーバーライド) (11.8 / original p.575)

To use the positioning operation speed override function, use this data item to specify an "override" value.
If the command speed is set to less than the minimum unit using the override function, the speed is raised to the minimum unit and the warning "Less than minimum speed" (warning code: 0904H [FX5-SSC-S], or warning code: 0D04H [FX5-SSC-G]) occurs.
For details of the override function, refer to the following.
→Page 262 Override function

Fetch cycle: Operation cycle

##### ■Setting range (設定範囲) (11.8 / original p.575)

- Set with a decimal

| Model | Setting range of [Cd.13] (unit) |
|---|---|
| FX5-SSC-S | 1 to 300% |
| FX5-SSC-G | Version 1.001 or earlier: 1 to 300%<br>Version 1.002 or later: 0 to 300% |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.575)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.575)

Set to "100".

#### [Cd.14] New speed value ([Cd.14]速度変更値) (11.8 / original p.575)

- When changing the speed, use this data item to specify a new speed.
- The operation halts if you specify "0".

Fetch cycle: At request

##### ■Setting range (設定範囲) (11.8 / original p.575)

- Set with a decimal.
- The setting value range differs according to the "[Pr.1] Unit setting".

| Setting of "[Pr.1] Unit setting" | Setting value depending on program (unit) |
|---|---|
| 0: mm | 0 to 2000000000 (× 10^-2 mm/min) |
| 1: inch | 0 to 2000000000 (× 10^-3 inch/min) |
| 2: degree*1 | 0 to 2000000000 (× 10^-3 degree/min) |
| 3: pulse | 0 to 1000000000 (pulse/s) |

*1 When "[Pr.83] Speed control 10 × multiplier setting for degree axis" is valid, the setting range is 0 to 2000000000 (× 10^-2 degree/min).

Ex.
When the "[Cd.14] New speed degree axis" is valid: "2" value" is set as "20000.00 mm/min", the buffer memory stores "2000000".

*(Note: the example sentence is garbled as printed in the original (it apparently intends: When the "[Cd.14] New speed value" is set as "20000.00 mm/min", ...). Kept as printed.)*

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.575)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.575)

Set to "0".

#### [Cd.15] Speed change request ([Cd.15]速度変更要求) (11.8 / original p.576)

- After setting the "[Cd.14] New speed value", set this data item to "1" to execute the speed change (through validating the new speed value).
- The Simple Motion module/Motion module resets the value to "0" automatically when the speed change request has been processed. (This indicates the completion of speed change request.)

Fetch cycle: Operation cycle

##### ■Setting value (設定値) (11.8 / original p.576)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 1 | Executes speed change. |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.576)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.576)

Set to "0".

#### [Cd.16] Inching movement amount ([Cd.16]インチング移動量) (11.8 / original p.576)

- Use this data item to set the amount of movement by inching.
- The machine performs a JOG operation if "0" is set.

Fetch cycle: At start

##### ■Setting range (設定範囲) (11.8 / original p.576)

- Set a value within the following range.

| Setting of "[Pr.1] Unit setting" | Setting value depending on program (unit)*1 |
|---|---|
| 0: mm | 0 to 65535 (× 10^-1 μm) |
| 1: inch | 0 to 65535 (× 10^-5 inch) |
| 2: degree*1 | 0 to 65535 (× 10^-5 degree) |
| 3: pulse | 0 to 65535 (pulse) |

*1 0 to 32767: Set as a decimal
32768 to 65535: Convert into hexadecimal and set

*(Note: the "*1" mark on "2: degree" is as printed in the original.)*

Ex.
When the "[Cd.16] Inching movement amount" is set as "1.0 μm", the buffer memory stores "10".

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.576)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.576)

Set to "0".

#### [Cd.17] JOG speed ([Cd.17]JOG速度) (11.8 / original p.577)

Use this data item to set the JOG speed.

Fetch cycle: At start

##### ■Setting range (設定範囲) (11.8 / original p.577)

- Set with a decimal.
- The setting value range differs according to the "[Pr.1] Unit setting".

| Setting of "[Pr.1] Unit setting" | Setting value depending on program (unit) |
|---|---|
| 0: mm | 1 to 2000000000 (× 10^-2 mm/min) |
| 1: inch | 1 to 2000000000 (× 10^-3 inch/min) |
| 2: degree*1 | 1 to 2000000000 (× 10^-3 degree/min) |
| 3: pulse | 1 to 1000000000 (pulse/s) |

*1 When "[Pr.83] Speed control 10 × multiplier setting for degree axis" is valid, the setting range is 1 to 2000000000 (× 10^-2 degree/min).

Ex.
When the "[Cd.17] JOG speed" is set as "20000.00 mm/min", the buffer memory stores "2000000".

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.577)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.577)

Set to "0".

#### [Cd.18] Interrupt request during continuous operation ([Cd.18]連続運転中断要求) (11.8 / original p.577)

- To interrupt a continuous operation, set "1" to this data item.
- After processing the interruption request ("1"), the Simple Motion module automatically resets the value to "0".

Fetch cycle: Operation cycle

##### ■Setting value (設定値) (11.8 / original p.577)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 1 | Interrupts continuous operation control or continuous path control. |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.577)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.577)

Set to "0".

#### [Cd.19] Home position return request flag OFF request ([Cd.19]原点復帰要求フラグOFF要求) (11.8 / original p.578)

- The program can use this data item to forcibly turn the home position return request flag from ON to OFF.
- The Simple Motion module/Motion module resets the value to "0" automatically when the home position return request flag is turned OFF. (This indicates the completion of home position return request flag OFF request.)

Fetch cycle: 14.2 [ms] [FX5-SSC-S]
Fetch cycle: 16.0 [ms] [FX5-SSC-G]

> **Point**
> This parameter is made valid when the increment system is valid.

##### ■Setting value (設定値) (11.8 / original p.578)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 1 | Turns the "home position return request flag" from ON to OFF. |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.578)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.578)

Set to "0".

#### [Cd.20] Manual pulse generator 1 pulse input magnification ([Cd.20]手動パルサ1パルス入力倍率) (11.8 / original p.578)

- This data item determines the factor by which the number of pulses from the manual pulse generator is magnified.
- Value "0": read as "1".
- Value "10001 or more" or negative value: read as "10000".

Fetch cycle: Operation cycle (At manual pulse generator enabled)

##### ■Setting range (設定範囲) (11.8 / original p.578)

- Set with a decimal.

| Setting range of [Cd.20] |
|---|
| 1 to 10000 |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.578)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.578)

Set to "1".

#### [Cd.21] Manual pulse generator enable flag ([Cd.21]手動パルサ許可フラグ) (11.8 / original p.578)

This data item enables or disables operations using a manual pulse generator.

Fetch cycle: Operation cycle

##### ■Setting value (設定値) (11.8 / original p.578)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 0 | Disable manual pulse generator operation. |
| 1 | Enable manual pulse generator operation. |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.578)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.578)

Set to "0".

#### [Cd.22] New torque value/forward new torque value ([Cd.22]トルク変更値／正転トルク変更値) (11.8 / original p.579)

- When "0" is set to "[Cd.112] Torque change function switching request", a new torque limit value is set. (This value is set to the forward torque limit value and reverse torque limit value.) When "1" is set to "[Cd.112] Torque change function switching request", a new forward torque limit value is set.
- Set a value within "0" to "[Pr.17] Torque limit setting value". Set a ratio against the rated torque in 0.1% unit. (The new torque value is invalid when "0" is set, and "[Pr.17] Torque limit setting value" or "[Cd.101] Torque output setting value" becomes valid. The range of torque change is 1 to "[Pr.17] Torque limit setting value".)

Fetch cycle: Operation cycle

##### ■Setting range (設定範囲) (11.8 / original p.579)

- Set with a decimal.

| Setting range (unit) of [Cd.22] |
|---|
| 0 to [Pr.17] Torque limit setting value (× 0.1%) |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.579)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.579)

Set to "0".

#### [Cd.23] Speed-position switching control movement amount change register ([Cd.23]速度・位置切換え制御移動量変更レジスタ) (11.8 / original p.579)

- During the speed control stage of the speed-position switching control (INC mode), it is possible to change the specification of the movement amount during the position control stage. For that, use this data item to specify a new movement amount.
- The new movement amount has to be set during the speed control stage of the speed-position switching control (INC mode).
- The value is reset to "0" when the next operation starts.

Fetch cycle: At request

##### ■Setting range (設定範囲) (11.8 / original p.579)

- Set with a decimal.
- Set a value within the following range.

| Setting of "[Pr.1] Unit setting" | Setting value depending on program (unit) |
|---|---|
| 0: mm | 0 to 2147483647 (× 10^-1 μm) |
| 1: inch | 0 to 2147483647 (× 10^-5 inch) |
| 2: degree | 0 to 2147483647 (× 10^-5 degree) |
| 3: pulse | 0 to 2147483647 (pulse) |

Ex.
If "[Cd.23] Speed-position switching control movement amount change register" is set as "20000.0 μm", the buffer memory stores "200000".

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.579)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.579)

Set to "0".

#### [Cd.24] Speed-position switching enable flag ([Cd.24]速度・位置切換え許可フラグ) (11.8 / original p.580)

Sets whether the switching signal set in "[Cd.45] Speed-position switching device selection" is enabled or not.

Fetch cycle: At request

##### ■Setting value (設定値) (11.8 / original p.580)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 0 | Speed control will not be taken over by position control even when the signal set in "[Cd.45] Speed-position switching device selection" comes ON. |
| 1 | Speed control will be taken over by position control even when the signal set in "[Cd.45] Speed-position switching device selection" comes ON. |

*(Note: "even when" in the row for setting value 1 is as printed in the original.)*

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.580)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.580)

Set to "0".

#### [Cd.25] Position-speed switching control speed change register ([Cd.25]位置・速度切換え制御速度変更レジスタ) (11.8 / original p.580)

- During the position control stage of the position-speed switching control, it is possible to change the specification of the speed during the speed control stage. For that, use this data item to specify a new speed.
- The new speed has to be set during the position control stage of the position-speed switching control.
- The value is reset to "0" when the next operation starts.

Fetch cycle: At request

##### ■Setting range (設定範囲) (11.8 / original p.580)

- Set with a decimal.
- The setting value range differs according to the "[Pr.1] Unit setting".

| Setting of "[Pr.1] Unit setting" | Setting value depending on program (unit) |
|---|---|
| 0: mm | 0 to 2000000000 (× 10^-2 mm/min) |
| 1: inch | 0 to 2000000000 (× 10^-3 inch/min) |
| 2: degree*1 | 0 to 2000000000 (× 10^-3 degree/min) |
| 3: pulse | 0 to 1000000000 (pulse/s) |

*1 When "[Pr.83] Speed control 10 × multiplier setting for degree axis" is valid, the setting range is 0 to 2000000000 (× 10^-2 degree/min).

Ex.
If "[Cd.25] Position-speed switching control speed change register" is set as "2000.00 mm/min", the buffer memory stores "200000".

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.580)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.580)

Set to "0".

#### [Cd.26] Position-speed switching enable flag ([Cd.26]位置・速度切換え許可フラグ) (11.8 / original p.581)

Sets whether the switching signal set in "[Cd.45] Speed-position switching device selection" is enabled or not.

Fetch cycle: At request

##### ■Setting value (設定値) (11.8 / original p.581)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 0 | Position control will not be taken over by speed control even when the signal set in "[Cd.45] Speed-position switching device selection" comes ON. |
| 1 | Position control will be taken over by speed control when the signal set in "[Cd.45] Speed-position switching device selection" comes ON. |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.581)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.581)

Set to "0".

#### [Cd.27] Target position change value (New address) ([Cd.27]目標位置変更値(アドレス)) (11.8 / original p.581)

When changing the target position during a positioning operation, use this data item to specify a new positioning address.

Fetch cycle: At request

##### ■Setting range (設定範囲) (11.8 / original p.581)

- Set with a decimal.
- The setting value range differs according to the "[Pr.1] Unit setting".

| Setting of "[Pr.1] Unit setting" | Setting value depending on program (ABS) (unit) | Setting value depending on program (INC) (unit) |
|---|---|---|
| 0: mm | -2147483648 to 2147483647 (× 10^-1 μm) | -2147483648 to 2147483647 (× 10^-1 μm) |
| 1: inch | -2147483648 to 2147483647 (× 10^-5 inch) | -2147483648 to 2147483647 (× 10^-5 inch) |
| 2: degree | 0 to 35999999 (× 10^-5 degree) | -2147483648 to 2147483647 (× 10^-5 degree) |
| 3: pulse | -2147483648 to 2147483647 (pulse) | -2147483648 to 2147483647 (pulse) |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.581)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.581)

Set to "0".

#### [Cd.28] Target position change value (New speed) ([Cd.28]目標位置変更値(速度)) (11.8 / original p.582)

- When changing the target position during a positioning operation, use this data item to specify a new speed.
- The speed will not change if "0" is set.

Fetch cycle: At request

##### ■Setting range (設定範囲) (11.8 / original p.582)

- Set with a decimal.
- The setting value range differs according to the "[Pr.1] Unit setting".

| Setting of "[Pr.1] Unit setting" | Setting value depending on program (unit) |
|---|---|
| 0: mm | 0 to 2000000000 (× 10^-2 mm/min) |
| 1: inch | 0 to 2000000000 (× 10^-3 inch/min) |
| 2: degree*1 | 0 to 2000000000 (× 10^-3 degree/min) |
| 3: pulse | 0 to 1000000000 (pulse/s) |

*1 When "[Pr.83] Speed control 10 × multiplier setting for degree axis" is valid, the setting range is 0 to 2000000000 (× 10^-2 degree/min).

Ex.
If "[Cd.28] Target position change value (New speed)" is set as "10000.00 mm/min", the buffer memory stores "1000000".

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.582)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.582)

Set to "0".

#### [Cd.29] Target position change request flag ([Cd.29]目標位置変更要求フラグ) (11.8 / original p.582)

- Requests a change in the target position during a positioning operation.
- The Simple Motion module/Motion module resets the value to "0" automatically when the new target position value has been written. (This indicates the completion of target position change request.)

Fetch cycle: Operation cycle

##### ■Setting value (設定値) (11.8 / original p.582)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 1 | Requests a change in the target position |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.582)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.582)

Set to "0".

#### [Cd.30] Simultaneous starting own axis start data No. ([Cd.30]同時始動自軸始動データNo.) (11.8 / original p.583)

Use this data item to specify a start data No. of own axis at multiple axes simultaneous starting.

Fetch cycle: At start

##### ■Setting range (設定範囲) (11.8 / original p.583)

- Set with a decimal.

| Setting range of [Cd.30] |
|---|
| 1 to 600 |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.583)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.583)

Set to "0".

#### [Cd.31] Simultaneous starting axis start data No.1 ([Cd.31]同時始動対象軸1始動データNo.) (11.8 / original p.583)

Use this data item to specify a start data No.1 for each axis that starts simultaneously.

Fetch cycle: At start

##### ■Setting range (設定範囲) (11.8 / original p.583)

- Set with a decimal.

| Setting range of [Cd.31] |
|---|
| 1 to 600 |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.583)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.583)

Set to "0".

#### [Cd.32] Simultaneous starting axis start data No.2 ([Cd.32]同時始動対象軸2始動データNo.) (11.8 / original p.583)

Use this data item to specify a start data No.2 for each axis that starts simultaneously.

> **Point**
> For 2 axis simultaneous starting, the axis setting is not required. (Setting value is ignored.)

Fetch cycle: At start

##### ■Setting range (設定範囲) (11.8 / original p.583)

- Set with a decimal.

| Setting range of [Cd.32] |
|---|
| 1 to 600 |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.583)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.583)

Set to "0".

#### [Cd.33] Simultaneous starting axis start data No.3 ([Cd.33]同時始動対象軸3始動データNo.) (11.8 / original p.584)

Use this data item to specify a start data No.3 for each axis that starts simultaneously.

> **Point**
> For 2 axis simultaneous starting and 3 axis simultaneous starting, the axis setting is not required. (Setting value is ignored.)

Fetch cycle: At start

##### ■Setting range (設定範囲) (11.8 / original p.584)

- Set with a decimal.

| Setting range of [Cd.33] |
|---|
| 1 to 600 |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.584)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.584)

Set to "0".

#### [Cd.34] Step mode ([Cd.34]ステップモード) (11.8 / original p.584)

To perform a step operation, use this data item to specify the units by which the stepping should be performed.

Fetch cycle: At start

##### ■Setting value (設定値) (11.8 / original p.584)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 0 | Stepping by deceleration units |
| 1 | Stepping by data No. units |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.584)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.584)

Set to "0".

#### [Cd.35] Step valid flag ([Cd.35]ステップ有効フラグ) (11.8 / original p.584)

This data item validates or invalidates step operations.

Fetch cycle: At start

##### ■Setting value (設定値) (11.8 / original p.584)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 0 | Invalidates step operations |
| 1 | Validates step operations |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.584)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.584)

Set to "0".

#### [Cd.36] Step start information ([Cd.36]ステップ始動情報) (11.8 / original p.585)

- To continue the step operation when the step function is used, set "1" in the data item.
- The Simple Motion module/Motion module resets the value to "0" automatically when processing of the step start request completes.

Fetch cycle: 14.2 [ms] [FX5-SSC-S]
Fetch cycle: 16.0 [ms] [FX5-SSC-G]

##### ■Setting value (設定値) (11.8 / original p.585)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 1 | Continues step operation |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.585)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.585)

Set to "0".

#### [Cd.37] Skip command ([Cd.37]スキップ指令) (11.8 / original p.585)

- To skip the current positioning operation, set "1" in this data item.
- The Simple Motion module/Motion module resets the value to "0" automatically when processing of the skip request completes.

Fetch cycle: Operation cycle (During positioning operation)

##### ■Setting value (設定値) (11.8 / original p.585)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 1 | Issues a skip request to have the machine decelerate, stop, and then start the next positioning operation. |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.585)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.585)

Set to "0".

#### [Cd.38] Teaching data selection ([Cd.38]ティーチングデータ選択) (11.8 / original p.585)

- This data item specifies the teaching result write destination.
- Data are cleared to zero when the teaching ends.

Fetch cycle: At request

##### ■Setting value (設定値) (11.8 / original p.585)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 0 | Takes the command position value as a positioning address. |
| 1 | Takes the command position value as an arc data. |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.585)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.585)

Set to "0".

#### [Cd.39] Teaching positioning data No. ([Cd.39]ティーチング位置決めデータNo.) (11.8 / original p.586)

- This data item specifies data to be produced by teaching.
- If a value between 1 and 600 is set, a teaching operation is done.
- The value is cleared to "0" when the Simple Motion module/Motion module is initialized, when a teaching operation completes, and when an illegal value (601 or higher) is entered.

Fetch cycle: 103 [ms] [FX5-SSC-S]
Fetch cycle: 116 [ms] [FX5-SSC-G]

##### ■Setting range (設定範囲) (11.8 / original p.586)

- Set with a decimal.

| Setting range of [Cd.39] |
|---|
| 1 to 600 |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.586)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.586)

Set to "0".

#### [Cd.40] ABS direction in degrees ([Cd.40]degree時ABS方向設定) (11.8 / original p.586)

This data item specifies the ABS moving direction carrying out the position control when "degree" is selected as the unit.

Fetch cycle: At start

##### ■Setting value (設定値) (11.8 / original p.586)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 0 | Takes a shortcut. (Specified direction ignored.) |
| 1 | ABS circular right |
| 2 | ABS circular left |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.586)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.586)

Set to "0".

#### [Cd.43] Simultaneous starting axis ([Cd.43]同時始動対象軸) (11.8 / original p.587)

- Set the number of simultaneous starting axes and target axis. When "2" is set to the number of simultaneous starting axes, set the target axis No. to the simultaneous starting axis No.1. When "3" is set to the number of simultaneous starting axes, set the target axis No. to the simultaneous starting axis No.1 and 2. When "4" is set to the number of simultaneous starting axes, set the target axis No. to the simultaneous starting axis No.1 to 3.
- When the same axis No. or axis No. of own axis is set to the multiple simultaneous starting axis No, or the value outside the range is set to the number of simultaneous starting axes, the error "Error before simultaneous start" (error code: 1990H [FX5-SSC-S], or error codes: 1A90H and 1A91H [FX5-SSC-G]) occurs and the operation is not executed.

> **Point**
> Do not set the simultaneous starting axis No.2 and 3 for 2-axis interpolation, and do not set the simultaneous starting axis No.3 for 3-axis interpolation. The setting value is ignored.

Fetch cycle: At start

##### ■Setting value (設定値) (11.8 / original p.587)

- Set with a hexadecimal.

| Buffer memory | Bits | Details | Setting value | Setting value (meaning) |
|---|---|---|---|---|
| Low-order | b0 to b7 | Simultaneous starting axis No.1 | 00H to 07H | Axis 1 to Axis 8 |
| Low-order | b8 to b15 | Simultaneous starting axis No.2 | 00H to 07H | Axis 1 to Axis 8 |
| High-order | b0 to b7 | Simultaneous starting axis No.3 | 00H to 07H | Axis 1 to Axis 8 |
| High-order | b8 to b15 | Number of simultaneous starting axes | 02H to 04H | Axis 2 to Axis 4 |

*In the original, the "Buffer memory" header spans the order column and the bit column, and the "Setting value" header spans the value column and the meaning column. "Low-order" is merged over 2 rows and "High-order" over 2 rows; the cells "00H to 07H" and "Axis 1 to Axis 8" are merged over the 3 rows Simultaneous starting axis No.1 to No.3. Expanded to each row.

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.587)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.587)

Set to "0000H".

#### [Cd.45] Speed-position switching device selection ([Cd.45]速度⇔位置切換えデバイス選択) (11.8 / original p.587)

Select the device used for speed-position switching.

> **Point**
> If the setting is outside the range at start, operation is performed with the setting regarded as "0".

Fetch cycle: At start

##### ■Setting value (設定値) (11.8 / original p.587)

- Set with a decimal.

| Setting value | Details: Speed-position switching control | Details: Position-speed switching control |
|---|---|---|
| 0 | Use the external command signal for switching from speed control to position control | Use the external command signal for switching from position control to speed control |
| 1 | Use the proximity dog signal for switching from speed control to position control | Use the proximity dog signal for switching from position control to speed control |
| 2 | Use "[Cd.46] Speed-position switching command" for switching from speed control to position control | Use "[Cd.46] Speed-position switching command" for switching from position control to speed control |

*In the original, the "Details" header spans the 2 sub-columns "Speed-position switching control" and "Position-speed switching control". Written as combined column headers.

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.587)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.587)

Set to "0".

#### [Cd.46] Speed-position switching command ([Cd.46]速度⇔位置切換え指令) (11.8 / original p.588)

Speed-position control switching is performed when "2" is set in "[Cd.45] Speed-position switching device selection". Other than setting value is ignored.

> **Point**
> This parameter is made valid only when "2" is set in "[Cd.45] Speed-position switching device selection" at start.

Fetch cycle: 0.888 ms [FX5-SSC-S]
Fetch cycle: Operation cycle [FX5-SSC-G]

##### ■Setting value (設定値) (11.8 / original p.588)

- Set with a decimal.

| Setting value | Details: Speed-position switching control | Details: Position-speed switching control |
|---|---|---|
| 0 | Not switch from speed control to position control | Not switch from position control to speed control |
| 1 | Switch from speed control to position control | Switch from position control to speed control |

*In the original, the "Details" header spans the 2 sub-columns "Speed-position switching control" and "Position-speed switching control". Written as combined column headers.

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.588)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.588)

Set to "0".

#### [Cd.100] Servo OFF command ([Cd.100]サーボOFF指令) (11.8 / original p.588)

Executes servo OFF for each axis.

Fetch cycle: Operation cycle

> **Point**
> To execute servo ON for axes other than axis 1 being servo OFF, write "1" to storage buffer memory address of axis 1 and then turn ON "[Cd.191] All axis servo ON".

##### ■Setting value (設定値) (11.8 / original p.588)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 0 | Servo ON |
| 1 | Servo OFF |

Valid only during servo ON for all axes.

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.588)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.588)

Set to "0".

#### [Cd.101] Torque output setting value ([Cd.101]トルク出力設定値) (11.8 / original p.589)

Sets the torque output value. Set a ratio against the rated torque in 0.1% unit.

Fetch cycle: At start

> **Point**
> - If the "[Cd.101] Torque output setting value" is "0", the "[Pr.17] Torque limit setting value" will be its value.
> - If a value beside "0" is set in the "[Cd.101] Torque output setting value", the torque generated by the servo motor will be limited by that value.
> - The "[Pr.17] Torque limit setting value" of the detailed parameter becomes effective at the "[Cd.190] PLC READY" OFF → ON.
> - The "[Cd.101] Torque output setting value" (refer to the start) axis control data can be changed at all times. Therefore in the "[Cd.101] Torque output setting value" is used when you must change.
>
> (→Page 268 Torque change function)
>
> *(Note: the last bullet is worded as printed in the original.)*

##### ■Setting range (設定範囲) (11.8 / original p.589)

- Set with a decimal.

| Setting range (unit) of [Cd.101] |
|---|
| 0 to 10000 (× 0.1%) |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.589)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.589)

Set to "0".

#### [Cd.108] Gain switching command flag ([Cd.108]ゲイン切換え指令フラグ) (11.8 / original p.589-590)

The command required to carry out "gain switching" of the servo amplifier from the Simple Motion module/Motion module.

Fetch cycle: Operation cycle

> **Point**
> - For other than MR-J5(W)-B
>   If the setting value is other than "0" and "1", the gain switching command is set to OFF in the "gain switching" with the setting value regarded as "0".
>   Refer to the manuals of each servo amplifier for details of the gain switching.
> - For MR-J5(W)-B
>   If the setting value is outside the range (other than "0" to "3"*1), the gain switching command and the gain switching 2 command are set to OFF with the setting value regarded as "0".
>   Refer to the following for details of the gain switching command and the gain switching 2 command.
>   →Page 845 Connection with MR-J5(W)-B

*1 "3" is for manufacturer setting.

##### ■Setting value (設定値) (11.8 / original p.589)

- Set with a decimal.

[For other than MR-J5(W)-B]

| Setting value | Details |
|---|---|
| 0 | Gain switching command OFF |
| 1 | Gain switching command ON |

[For MR-J5(W)-B]

| Setting value | Details |
|---|---|
| 0 | Gain switching command OFF |
| 1 | Gain switching command ON |
| 2 | Gain switching 2 command ON |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.590)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.590)

Set to "0".

#### [Cd.112] Torque change function switching request ([Cd.112]トルク変更機能切換え要求) (11.8 / original p.590)

Sets "same setting/individual setting" of the forward torque limit value or reverse torque limit value in the torque change function.

Fetch cycle: Operation cycle

> **Point**
> - Set "0" normally. (when the forward torque limit value and reverse torque limit value are not divided.)
> - When a value except "1" is set, it operates as "forward/reverse torque limit value same setting".

##### ■Setting value (設定値) (11.8 / original p.590)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 0 | Forward/reverse torque limit value same setting |
| 1 | Forward/reverse torque limit value individual setting |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.590)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.590)

Set to "0".

#### [Cd.113] New reverse torque value ([Cd.113]逆転トルク変更値) (11.8 / original p.590)

- "1" is set in "[Cd.112] Torque change function switching request", a new reverse torque limit value is set. (when "0" is set in "[Cd.112] Torque change function switching request", the setting value is invalid.)
- Set a value within "0" to "[Pr.17] Torque limit setting value". Set a ratio against the rated torque in 0.1% unit. (The new torque value is invalid when "0" is set, and "[Pr.17] Torque limit setting value" or "[Cd.101] Torque output setting value" becomes valid. The range of torque change is 1 to "[Pr.17] Torque limit setting value".

*(Note: the missing closing parenthesis in the second bullet is as printed in the original.)*

Fetch cycle: Operation cycle

##### ■Setting range (設定範囲) (11.8 / original p.590)

- Set with a decimal.

| Setting range (unit) of [Cd.113] |
|---|
| 0 to "[Pr.17] Torque limit setting value" (× 0.1%) |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.590)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.590)

Set to "0".

#### [Cd.130] Servo parameter read/write request [FX5-SSC-S] ([Cd.130]サーボパラメータ読み出し／書き込み要求[FX5-SSC-S]) (11.8 / original p.591)

- To change the servo parameter after it is transferred, set the write request of servo parameter. Set "0001H: 1 word write request" or "0002H: 2 words write request" after setting "[Cd.131] Parameter No. (Setting for servo parameters to be changed)" and "[Cd.132] Change data".
- To change the servo parameter stored in the internal memory of the Simple Motion module, set the read/write request of the servo parameter.
  For writing, set "0022H: 2 words write request to internal memory" after setting "[Cd.131] Parameter No." and "[Cd.132] Change data".
  For reading, set "0032H: 2 words read request from internal memory" after setting "[Cd.131] Parameter No.".
- Set "0001H: 1 word write request" to MR-J4(W)-B and MR-J3(W)-B, and "0002H: 2 words write request" to the VCII series/VPH series.
- The Simple Motion module/Motion module resets the value to "0000H" automatically when the parameter read/write access completes. (The Simple Motion module resets the value to "0003H: Read/write failure" at writing failure.)

Fetch cycle: Main cycle*1

*1 Cycle of processing executed at free time except for the positioning control. It changes by status of axis start.

> **Point**
> - If this control data is set to "0001H: 1 word write request" or "0002H: 2 words write request" in the following states, it becomes "0003H: Read/write failure".
>   - The connection with the servo amplifier is not established or there is an error in the communication.
>   - "[Cd.131] Parameter No." is outside the setting range.
>   - The servo amplifier does not support the writing of the specified number of words.
> - If this control data is set to "0022H: 2 words write request to internal memory" or "0032H: 2 words read request from internal memory" in the following states, it becomes "0003H".
>   - The servo amplifier used is other than MR-J5(W)-B.
>   - "[Cd.131] Parameter No." is outside the setting range.

##### ■Setting value (設定値) (11.8 / original p.591)

- Set with a hexadecimal.

| Setting value | Details |
|---|---|
| 0001H | 1 word write request |
| 0002H | 2 words write request |
| 0003H | Read/write failure |
| 0022H | 2 words write request to internal memory |
| 0032H | 2 words read request from internal memory |
| Other than the above | Not request |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.591)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.591)

Set to "0000H".

#### [Cd.131] Parameter No. (Setting for servo parameters to be changed) [FX5-SSC-S] ([Cd.131]パラメータNo. (変更するサーボパラメータの設定)[FX5-SSC-S]) (11.8 / original p.592)

Set the servo parameter to be changed.

Fetch cycle: At request

##### ■Setting value (設定値) (11.8 / original p.592)

- Set with a hexadecimal.

| Buffer memory address | Details | Setting value: MR-J5(W)-B | Setting value: MR-J4(W)-B | Setting value: VCII series/VPH series |
|---|---|---|---|---|
| b0 to b7 | Parameter No. setting | 01H to 80H | 01H to 40H | 01H to 99H |
| b8 to b11 | Parameter group | 0H: PA group<br>1H: PB group<br>2H: PC group<br>3H: PD group<br>4H: PE group<br>5H: PF group<br>9H: Po group<br>AH: PS group<br>BH: PL group | 0H: PA group<br>1H: PB group<br>2H: PC group<br>3H: PD group<br>4H: PE group<br>5H: PF group<br>9H: Po group<br>AH: PS group<br>BH: PL group | 0H: Group 0<br>1H: Group 1<br>2H: Group 2<br>3H: Group 3<br>4H: Group 4<br>5H: Group 5<br>6H: Group 6<br>7H: Group 7<br>8H: Group 8<br>9H: Group 9 |
| b12 to b15 | Writing mode | Fixed to 0 | Fixed to 0 | 0H: Write to RAM |

*In the original, the "Setting value" header spans the 3 sub-columns MR-J5(W)-B / MR-J4(W)-B / VCII series/VPH series. Written as combined column headers.

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.592)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.592)

Set to "0000H".

#### [Cd.132] Change data [FX5-SSC-S] ([Cd.132]変更データ[FX5-SSC-S]) (11.8 / original p.592)

Set the changed value of servo parameter set in "[Cd.131] Parameter No. (Setting for servo parameters to be changed)".

Fetch cycle: At request

##### ■Setting value (設定値) (11.8 / original p.592)

- Set with a decimal or hexadecimal.

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.592)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.592)

Set to "0".

#### [Cd.133] Semi/Fully closed loop switching request ([Cd.133]セミ・フル切換え要求) (11.8 / original p.592)

Set the switching of semi closed control and fully closed loop control.

Fetch cycle: Operation cycle (The servo amplifiers for fully closed loop control only)

##### ■Setting value (設定値) (11.8 / original p.592)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 0 | Semi closed loop control |
| 1 | Fully closed loop control |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.592)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.592)

Set to "0".

#### [Cd.136] PI-PID switching request ([Cd.136]PI-PID切換え要求) (11.8 / original p.593)

Set the PI-PID switching to servo amplifier.

Fetch cycle: Operation cycle

##### ■Setting value (設定値) (11.8 / original p.593)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 1 | PID control switching request |
| Other than 1 | Not request |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.593)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.593)

Set to "0".

#### [Cd.138] Control mode switching request ([Cd.138]制御モード切換え要求) (11.8 / original p.593)

- Request the control mode switching. Set "1" after setting "[Cd.139] Control mode setting".
- The Simple Motion module/Motion module sets "0" at completion of control mode switching.

Fetch cycle: Operation cycle

##### ■Setting value (設定値) (11.8 / original p.593)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 1 | Switching request |
| Other than 1 | Not request |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.593)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.593)

Set to "0".

#### [Cd.139] Control mode setting ([Cd.139]制御モード指定) (11.8 / original p.593)

Set the control mode to be changed in the speed-torque control.

Fetch cycle: At request (Mode switching)

##### ■Setting value (設定値) (11.8 / original p.593)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 0 | Position control mode |
| 10 | Speed control mode |
| 20 | Torque control mode |
| 30 | Continuous operation to torque control mode |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.593)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.593)

Set to "0".

#### [Cd.140] Command speed at speed control mode ([Cd.140]速度制御モード時指令速度) (11.8 / original p.594)

Set the command speed at speed control mode.

Fetch cycle: Operation cycle (At speed control mode)

##### ■Setting range (設定範囲) (11.8 / original p.594)

- Set with a decimal.
- The setting value range differs according to the "[Pr.1] Unit setting".

| Setting of "[Pr.1] Unit setting" | Setting value depending on program (unit) |
|---|---|
| 0: mm | -2000000000 to 2000000000 (× 10^-2 mm/min) |
| 1: inch | -2000000000 to 2000000000 (× 10^-3 inch/min) |
| 2: degree*1 | -2000000000 to 2000000000 (× 10^-3 degree//min) |
| 3: pulse | -1000000000 to 1000000000 (pulse/s) |

*(Note: "degree//min" in the 2: degree row is as printed in the original.)*

*1 When "[Pr.83] Speed control 10 × multiplier setting for degree axis" is valid, the setting range is -2000000000 to 2000000000 (× 10^-2 degree/min).

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.594)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.594)

Set to "0".

#### [Cd.141] Acceleration time at speed control mode ([Cd.141]速度制御モード時加速時間) (11.8 / original p.594)

Set the acceleration time at speed control mode. (Set the time for the speed to increase from "0" to "[Pr.8] Speed limit value".)

Fetch cycle: At request (Mode switching)

##### ■Setting range (設定範囲) (11.8 / original p.594)

| Setting range (unit) of [Cd.141]*1 |
|---|
| 0 to 65535 (ms) |

*1 0 to 32767: Set as a decimal
32768 to 65535: Convert into hexadecimal and set

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.594)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.594)

Set to "1000".

#### [Cd.142] Deceleration time at speed control mode ([Cd.142]速度制御モード時減速時間) (11.8 / original p.594)

Set the deceleration time at speed control mode. (Set the time for the speed to decrease from "[Pr.8] Speed limit value" to "0".)

Fetch cycle: At request (Mode switching)

##### ■Setting range (設定範囲) (11.8 / original p.594)

| Setting range (unit) of [Cd.142]*1 |
|---|
| 0 to 65535 (ms) |

*1 0 to 32767: Set as a decimal
32768 to 65535: Convert into hexadecimal and set

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.594)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.594)

Set to "1000".

#### [Cd.143] Command torque at torque control mode ([Cd.143]トルク制御モード時指令トルク) (11.8 / original p.595)

Set the command torque at torque control mode. Set a ratio against the rated torque in 0.1% unit.

Fetch cycle: Operation cycle (At torque control mode)

##### ■Setting range (設定範囲) (11.8 / original p.595)

- Set with a decimal.

| Setting range (unit) of [Cd.143] |
|---|
| -10000 to 10000 (× 0.1%) |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.595)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.595)

Set to "0".

#### [Cd.144] Torque time constant at torque control mode (Forward direction) ([Cd.144]トルク制御モード時トルク時定数(正方向)) (11.8 / original p.595)

Set the time constant at driving during torque control mode. (Set the time for the torque to increase from "0" to "[Pr.17] Torque limit setting value".)

Fetch cycle: At request (Mode switching)

##### ■Setting range (設定範囲) (11.8 / original p.595)

| Setting range (unit) of [Cd.144]*1 |
|---|
| 0 to 65535 (ms) |

*1 0 to 32767: Set as a decimal
32768 to 65535: Convert into hexadecimal and set

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.595)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.595)

Set to "1000".

#### [Cd.145] Torque time constant at torque control mode (Negative direction) ([Cd.145]トルク制御モード時トルク時定数(負方向)) (11.8 / original p.595)

Set the time constant at regeneration during torque control mode. (Set the time for the torque to decrease from "[Pr.17] Torque limit setting value" to "0".)

Fetch cycle: At request (Mode switching)

##### ■Setting range (設定範囲) (11.8 / original p.595)

| Setting range (unit) of [Cd.145]*1 |
|---|
| 0 to 65535 (ms) |

*1 0 to 32767: Set as a decimal
32768 to 65535: Convert into hexadecimal and set

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.595)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.595)

Set to "1000".

#### [Cd.146] Speed limit value at torque control mode ([Cd.146]トルク制御モード時速度制限値) (11.8 / original p.596)

Set the speed limit value at torque control mode.

Fetch cycle: Operation cycle (At torque control mode)

##### ■Setting range (設定範囲) (11.8 / original p.596)

- Set with a decimal.
- The setting value range differs according to the "[Pr.1] Unit setting".

| Setting of "[Pr.1] Unit setting" | Setting value depending on program (unit) |
|---|---|
| 0: mm | 0 to 2147483647 (× 10^-2 mm/min) |
| 1: inch | 0 to 2000000000 (× 10^-3 inch/min) |
| 2: degree*1 | 0 to 2000000000 (× 10^-3 degree/min) |
| 3: pulse | 0 to 1000000000 (pulse/s) |

*(Note: the upper limit "2147483647" in the 0: mm row is as printed in the original.)*

*1 When "[Pr.83] Speed control 10 × multiplier setting for degree axis" is valid, the setting range is 0 to 2000000000 (× 10^-2 degree/min).

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.596)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.596)

Set to "1".

#### [Cd.147] Speed limit value at continuous operation to torque control mode ([Cd.147]押当て制御モード時速度制限値) (11.8 / original p.596)

Set the speed limit value at continuous operation to torque control mode.

Fetch cycle: Operation cycle (At continuous operation to torque control mode)

##### ■Setting range (設定範囲) (11.8 / original p.596)

- Set with a decimal.
- The setting value range differs according to the "[Pr.1] Unit setting".

| Setting of "[Pr.1] Unit setting" | Setting value depending on program [FX5-SSC-S] (unit) | Setting value depending on program [FX5-SSC-G] (unit) |
|---|---|---|
| 0: mm | -2000000000 to 2000000000 (× 10^-2 mm/min) | 0 to 2000000000 (× 10^-2 mm/min) |
| 1: inch | -2000000000 to 2000000000 (× 10^-3 inch/min) | 0 to 2000000000 (× 10^-3 inch/min) |
| 2: degree*1 | -2000000000 to 2000000000 (× 10^-3 degree/min) | 0 to 2000000000 (× 10^-3 degree/min) |
| 3: pulse | -1000000000 to 1000000000 (pulse/s) | 0 to 1000000000 (pulse/s) |

*1 [FX5-SSC-S]
When "[Pr.83] Speed control 10 × multiplier setting for degree axis" is valid, the setting range is -2000000000 to 2000000000 (× 10^-2 degree/min).
[FX5-SSC-G]
When "[Pr.83] Speed control 10 × multiplier setting for degree axis" is valid, the setting range is 0 to 2000000000 (× 10^-2 degree/min).

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.596)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.596)

Set to "0".

#### [Cd.148] Acceleration time at continuous operation to torque control mode ([Cd.148]押当て制御モード時加速時間) (11.8 / original p.597)

Set the acceleration time at continuous operation to torque control mode. (Set the time for the speed to increase from "0" to "[Pr.8] Speed limit value".)

Fetch cycle: At request (Mode switching)

##### ■Setting range (設定範囲) (11.8 / original p.597)

| Setting range (unit) of [Cd.148]*1 |
|---|
| 0 to 65535 (ms) |

*1 0 to 32767: Set as a decimal
32768 to 65535: Convert into hexadecimal and set

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.597)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.597)

Set to "1000".

#### [Cd.149] Deceleration time at continuous operation to torque control mode ([Cd.149]押当て制御モード時減速時間) (11.8 / original p.597)

Set the deceleration time at continuous operation to torque control mode. (Set the time for the speed to decrease from "[Pr.8] Speed limit value" to "0".)

Fetch cycle: At request (Mode switching)

##### ■Setting range (設定範囲) (11.8 / original p.597)

| Setting range (unit) of [Cd.149]*1 |
|---|
| 0 to 65535 (ms) |

*1 0 to 32767: Set as a decimal
32768 to 65535: Convert into hexadecimal and set

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.597)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.597)

Set to "1000".

#### [Cd.150] Target torque at continuous operation to torque control mode ([Cd.150]押当て制御モード時目標トルク) (11.8 / original p.597)

Set the target torque at continuous operation to torque control mode. Set a ratio against the rated torque in 0.1% unit.

Fetch cycle: Operation cycle (At continuous operation to torque control mode)

##### ■Setting range (設定範囲) (11.8 / original p.597)

- Set with a decimal.

| Setting range (unit) of [Cd.150] |
|---|
| -10000 to 10000 (× 0.1%) |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.597)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.597)

Set to "0".

#### [Cd.151] Torque time constant at continuous operation to torque control mode (+*1) ([Cd.151]押当て制御モード時トルク時定数(正方向)) (11.8 / original p.598)

*1 "+" is an abbreviation for "Forward direction".

Set the time constant at driving during continuous operation to torque control mode. (Set the time for the torque to increase from "0" to "[Pr.17] Torque limit setting value".)

Fetch cycle: At request (Mode switching)

##### ■Setting range (設定範囲) (11.8 / original p.598)

| Setting range (unit) of [Cd.151]*1 |
|---|
| 0 to 65535 (ms) |

*1 0 to 32767: Set as a decimal
32768 to 65535: Convert into hexadecimal and set

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.598)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.598)

Set to "1000".

#### [Cd.152] Torque time constant at continuous operation to torque control mode (-*1) ([Cd.152]押当て制御モード時トルク時定数(負方向)) (11.8 / original p.598)

*1 "-" is an abbreviation for "Negative direction".

Set the time constant at regeneration during continuous operation to torque control mode. (Set the time for the torque to decrease from "[Pr.17] Torque limit setting value" to "0".)

Fetch cycle: At request (Mode switching)

##### ■Setting range (設定範囲) (11.8 / original p.598)

| Setting range (unit) of [Cd.152]*1 |
|---|
| 0 to 65535 (ms) |

*1 0 to 32767: Set as a decimal
32768 to 65535: Convert into hexadecimal and set

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.598)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.598)

Set to "1000".

#### [Cd.153] Control mode auto-shift selection ([Cd.153]制御モード自動切換え選択) (11.8 / original p.599)

Set the switching condition when switching to continuous operation to torque control mode.

Fetch cycle: At request (Mode switching)

##### ■Setting value (設定値) (11.8 / original p.599)

- Set with a decimal.

| Setting value | Details | Details (description) |
|---|---|---|
| 0 | No switching condition | Switching is executed at switching request to continuous operation to torque control mode. |
| 1 | Command position value pass | Switching is executed when "[Md.20] Command position value" passes the address set in "[Cd.154] Control mode auto-shift parameter" after switching request to continuous operation to torque control mode. |
| 2 | Actual position value pass | Switching is executed when "[Md.101] Actual position value" passes the address set in "[Cd.154] Control mode auto-shift parameter" after switching request to continuous operation to torque control mode. |

*In the original, the "Details" header spans the 2 columns (condition name and description).

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.599)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.599)

Set to "0".

#### [Cd.154] Control mode auto-shift parameter ([Cd.154]制御モード自動切換えパラメータ) (11.8 / original p.599)

- Set the condition value when setting the control mode switching condition.
- The setting value differs depending on the value set in "[Cd.153] Control mode auto-shift selection". When "1" or "2" is set in "[Cd.153] Control mode auto-shift selection": Set the switching address.

Fetch cycle: At request (Mode switching)

##### ■Setting range (設定範囲) (11.8 / original p.599)

- Set with a decimal.
- The setting value range differs according to the "[Pr.1] Unit setting".

| Setting of "[Pr.1] Unit setting" | Setting value depending on program (unit) |
|---|---|
| 0: mm | -2147483648 to 2147483647 (× 10^-1 μm) |
| 1: inch | -2147483648 to 2147483647 (× 10^-5 inch) |
| 2: degree | 0 to 35999999 (× 10^-5 degree) |
| 3: pulse | -2147483648 to 2147483647 (pulse) |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.599)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.599)

Set to "0".

#### [Cd.180] Axis stop ([Cd.180]軸停止) (11.8 / original p.600)

- When the axis stop signal turns ON, the home position return control, positioning control, JOG operation, inching operation, manual pulse generator operation, speed-torque control, etc. will stop.
- By turning the axis stop signal ON during positioning operation, the positioning operation will be "stopped".
- Whether to decelerate stop or rapidly stop can be selected with "[Pr.39] Stop group 3 sudden stop selection".
- During interpolation control of the positioning operation, if the axis stop signal of any axis turns ON, all axes in the interpolation control will decelerate and stop.

Fetch cycle: Operation cycle

##### ■Setting value (設定値) (11.8 / original p.600)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 1 | Axis stop requested |
| Other than 1 | Axis stop not requested |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.600)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.600)

Set to "0".

#### [Cd.181] Forward run JOG start, [Cd.182] Reverse run JOG start ([Cd.181]正転JOG始動，[Cd.182]逆転JOG始動) (11.8 / original p.600)

- When the JOG start signal is ON, JOG operation will be carried out at the "[Cd.17] JOG speed". When the JOG start signal turns OFF, the operation will decelerate and stop.
- When inching movement amount is set, the designated movement amount is output for one operation cycle and then the operation stops.

Fetch cycle: Operation cycle

##### ■Setting value (設定値) (11.8 / original p.600)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 1 | JOG started |
| Other than 1 | JOG not started |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.600)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.600)

Set to "0".

#### [Cd.183] Execution prohibition flag ([Cd.183]実行禁止フラグ) (11.8 / original p.601)

If the execution prohibition flag is ON when the positioning start signal turns ON, positioning control does not start until the execution prohibition flag turns OFF. Used with the "Pre-reading start function". (→Page 276 Pre-reading start function)

Fetch cycle: At start

##### ■Setting value (設定値) (11.8 / original p.601)

- Set with a decimal.

| Setting value | Details |
|---|---|
| 1 | During execution prohibition |
| Other than 1 | Not during execution prohibition |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.601)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.601)

Set to "0".

#### [Cd.184] Positioning start ([Cd.184]位置決め始動) (11.8 / original p.601)

- Home position return operation or positioning operation is started.
- The positioning start signal is valid at the leading edge, and the operation is started.
- When the positioning start signal turns ON during BUSY, the warning "Start during operation" (warning code: 0900H [FX5-SSC-S], or warning code: 0D00H [FX5-SSC-G]) will occur.

Fetch cycle: Operation cycle

##### ■Setting value (設定値) (11.8 / original p.601)

- Set with a decimal

| Setting value | Details |
|---|---|
| 1 | Positioning start signal requested |
| Other than 1 | Positioning start signal not requested |

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.601)

Refer to the following for the buffer memory address in this area.
→Page 428 Axis control data

##### ■Default value (初期値) (11.8 / original p.601)

Set to "0".

### Axis control data (transient function) [FX5-SSC-G] (軸制御データ(トランジェント機能)[FX5-SSC-G]) (11.8 / original p.602)

#### [Cd.160] Optional SDO transfer request 1 ([Cd.160]任意SDO転送要求1) (11.8 / original p.602)

Used in the servo transient transmission function. Refer to the following for details.
→Page 381 Servo Transient Transmission Function [FX5-SSC-G]

Fetch cycle: Main cycle

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.602)

Refer to the following for the buffer memory address in this area.
→Page 430 Axis control data (transient function) [FX5-SSC-G]

##### ■Default value (初期値) (11.8 / original p.602)

Set to "0".

#### [Cd.164] Optional SDO transfer data 1 ([Cd.164]任意SDO転送データ1) (11.8 / original p.602)

Used in the servo transient transmission function. Refer to the following for details.
→Page 381 Servo Transient Transmission Function [FX5-SSC-G]

Fetch cycle: At request (Command request)

##### ■Buffer memory address (バッファメモリアドレス) (11.8 / original p.602)

Refer to the following for the buffer memory address in this area.
→Page 430 Axis control data (transient function) [FX5-SSC-G]

##### ■Default value (初期値) (11.8 / original p.602)

Set to "0".

## 11.9 Memory Configuration and Data Process (メモリ構成とデータ処理) (11.9 / original p.603-623)

The memory configuration and data transmission of Simple Motion module/Motion module are explained in this section.
The Simple Motion module/Motion module is configured of four memories. By understanding the configuration and roles of two memories, the internal data transmission process of Simple Motion module/Motion module, such as "when the power is turned ON" or "when the "[Cd.190] PLC READY" changes from OFF to ON", can be easily understood. This also allows the transmission process to be carried out correctly when saving or changing the data.
*(Note: "roles of two memories" is as printed in the original, although the preceding sentence says four memories.)*

### Configuration and roles (メモリ構成と役割) (11.9 / original p.603)

The Simple Motion module/Motion module is configured of the following four memories.
○: Setting and storage area provided, —: Setting and storage area not provided.
Not possible: Data is lost when power is turned OFF, Possible: Data is held even when power is turned OFF.

| Memory configuration | Role | Parameter area | Monitor data area | Control data area | Positioning data area (No.1 to 100) | Positioning data area (No.101 to 600) | Block start data area (No.7000 to 7001) | Block start data area (No.7002 to 7004) |
|---|---|---|---|---|---|---|---|---|
| Buffer memory | Area that can be directly accessed with a program with a CPU module | ○ | ○ | ○ | ○ | — | ○ | — |
| Internal memory | Area that can be set only with the engineering tool | — | — | — | — | ○ | — | ○ |
| Internal memory | Area that can be set only using buffer memory | — | — | — | — | — | — | — |
| Flash ROM | Area for backing up data required for positioning | ○ | — | — | ○ | ○ | ○ | ○ |
| Internal memory (nonvolatile) | Area for backing up servo parameter or cam data | — | — | — | — | — | — | — |

*In the original, the header "Area configuration" spans all area columns, "Positioning data area" spans (No.1 to 100) / (No.101 to 600), and "Block start data area" spans (No.7000 to 7001) / (No.7002 to 7004); written here as combined column headers. "Internal memory" is merged over 2 rows. Expanded to each row.

| Memory configuration | Role | Servo parameter area: FX5-SSC-S (When MR-J3(W)-B/MR-J4(W)-B is used) | Servo parameter area: FX5-SSC-S (When MR-J5(W)-B is used) | Servo parameter area: FX5-SSC-G | Synchronous control area | Cam area | Backup |
|---|---|---|---|---|---|---|---|
| Buffer memory | Area that can be directly accessed with a program with a CPU module | ○ | — | — | ○ | — | Not possible |
| Internal memory | Area that can be set only with the engineering tool | — | ○*1 | — | — | — | Not possible |
| Internal memory | Area that can be set only using buffer memory | — | — | — | — | ○ | Not possible |
| Flash ROM | Area for backing up data required for positioning | — | — | — | ○*2 | — | Possible |
| Internal memory (nonvolatile) | Area for backing up servo parameter or cam data | ○ | ○ | — | — | ○ | Possible |

*In the original, the header "Area configuration" spans the servo parameter / synchronous control / cam area columns, "Servo parameter area" spans the 3 servo parameter columns, and "FX5-SSC-S" spans the 2 MR-J3/J4 and MR-J5 columns; written here as combined column headers. "Internal memory" is merged over 2 rows. Expanded to each row.

*1 Can be set by using the axis control data ([Cd.130] to [Cd.132]).
*2 Parameter only

#### Details of areas (エリア詳細) (11.9 / original p.604-605)

| Area name | Description |
|---|---|
| Parameter area | Area where parameters, such as positioning parameters and home position return parameters, required for positioning control are set and stored. |
| Monitor data area | Area where the operation status of positioning system is stored. |
| Control data area | Area where data for operating and controlling positioning system is set and stored. |
| Positioning data area (No.1 to 600) | Area where positioning data No.1 to 600 is set and stored. |
| Block start data area (No.7000 to 7004) | Area where information required only when carrying out block No.7000 to 7004 high-level positioning is set and stored. |
| Servo parameter area | Area where parameters, such as servo parameters, required for positioning control on servo amplifier are set and stored. |
| Synchronous control area*1 | Area where parameters and control data required for synchronous control are set and stored. Also, the operation status of synchronous control is stored. |
| Cam area*1 | Area where cam data, etc. are set and stored. There are cam storage area and cam open area. |

*1 Refer to the following manual for details of synchronous control area and cam area.
[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Advanced Synchronous Control)

##### Area of FX5-SSC-S (FX5-SSC-Sのエリア) (11.9 / original p.604)

[Figure] Memory areas of the Simple Motion module (original p.604)
- Outer frame: "Simple Motion module".
- Left (dashed frame, "Data is backed up here."): Flash ROM = Parameter area (a) / Parameter area (b) / Parameter area (c) / Positioning data area (No.1 to 600) / Block start data area (No.7000 to 7004); Internal memory (nonvolatile) = Servo parameter area.
- Right ("User accesses here."): Buffer memory/Internal memory = Parameter area (a) / Parameter area (b) / Parameter area (c) / Positioning data area (No.1 to 600) / Block start data area (No.7000 to 7004) / Servo parameter area / Monitor data area / Control data area.

| Area name | Description | Parameters |
|---|---|---|
| Parameter area (a) | Parameters validated when "[Cd.190] PLC READY" changes from OFF to ON | [Pr.1] to [Pr.7], [Pr.11] to [Pr.24], [Pr.43] to [Pr.57], [Pr.81] to [Pr.83], [Pr.89], [Pr.90], [Pr.95], [Pr.116] to [Pr.119], [Pr.127], [Pr.150], [Pr.151], [Pr.801], [Pr.805] to [Pr.807] |
| Parameter area (b) | Parameters validated when the TO command is executed from the CPU module (validated when the next control is started after the TO command is executed, at request, and at conditions established) | [Pr.8] to [Pr.10], [Pr.25] to [Pr.41], [Pr.84] |
| Parameter area (c) | Parameters validated with power supply ON/the CPU module reset | [Pr.91] to [Pr.94], [Pr.96], [Pr.97], [Pr.116] to [Pr.119], [Pr.150], [Pr.151], [Pr.800] to [Pr.807] |

*In the original, the "Description" header spans the 2 right columns (text and parameter list); the column name "Parameters" is added here.

##### Area of FX5-SSC-G (FX5-SSC-Gのエリア) (11.9 / original p.605)

[Figure] Memory areas of the Motion module (original p.605)
- Outer frame: "Motion module".
- Left (dashed frame, "Data is backed up here."): Flash ROM = Parameter area (a) / Parameter area (b) / Parameter area (c) / Positioning data area (No.1 to 600) / Block start data area (No.7000 to 7004). (No internal memory (nonvolatile) / servo parameter area is shown.)
- Right ("User accesses here."): Buffer memory/Internal memory = Parameter area (a) / Parameter area (b) / Parameter area (c) / Positioning data area (No.1 to 600) / Block start data area (No.7000 to 7004) / Monitor data area / Control data area. (No servo parameter area is shown.)

| Area name | Description | Parameters |
|---|---|---|
| Parameter area (a) | Parameters validated when "[Cd.190] PLC READY" changes from OFF to ON | [Pr.1] to [Pr.7], [Pr.11] to [Pr.22], [Pr.43] to [Pr.46], [Pr.51], [Pr.52], [Pr.55], [Pr.81] to [Pr.83], [Pr.90], [Pr.95], [Pr.116] to [Pr.119], [Pr.122], [Pr.123], [Pr.127], [Pr.156], [Pr.801], [Pr.805] to [Pr.807] |
| Parameter area (b) | Parameters validated when the TO command is executed from the CPU module (validated when the next control is started after the TO command is executed, at request, and at conditions established) | [Pr.8] to [Pr.10], [Pr.25] to [Pr.41], [Pr.84], [Pr.112] |
| Parameter area (c) | Parameters validated with power supply ON/the CPU module reset | [Pr.91] to [Pr.94], [Pr.101], [Pr.116] to [Pr.119], [Pr.140] to [Pr.142] [Pr.152], [Pr.591] to [Pr.594], [Pr.800] to [Pr.811], [Pr.900] to [Pr.903], [Pr.910] to [Pr.913], [Pr.920] to [Pr.923], [Pr.930] to [Pr.933], [Pr.940] to [Pr.943] |

*In the original, the "Description" header spans the 2 right columns (text and parameter list); the column name "Parameters" is added here. (The missing comma after "[Pr.140] to [Pr.142]" is as printed.)

### Buffer memory area configuration (バッファメモリのエリア構成) (11.9 / original p.606-607)

The buffer memory of Simple Motion module/Motion module is configured of the following types of areas.
n: Axis No. - 1
k: Mark detection setting No. - 1
j: Synchronous encoder axis No. - 1

| Buffer memory area configuration | | Buffer memory address*1 | Writing possibility |
|---|---|---|---|
| Parameter area | Servo network configuration parameter [FX5-SSC-G] | 58022+32n to 58028+32n | Possible |
| Parameter area | Common parameter | 33, 35, 67, 105, 106, 58000 to 58003, 58011, 58014 to 58017 | Possible |
| Parameter area | Basic parameter | 0+150n to 15+150n | Possible |
| Parameter area | Detailed parameter | 17+150n to 69+150n, 116+150n to 119+150n, 125+150n | Possible |
| Parameter area | Home position return basic parameter | 70+150n to 78+150n | Possible |
| Parameter area | Home position return detailed parameter | 80+150n to 91+150n | Possible |
| Parameter area | Extended parameter | 92+150n to 95+150n, 100+150n to 103+150n, 128+150n, 129+150n | Possible |
| Parameter area | Link device external signal assignment parameter [FX5-SSC-G] | 36000+20n to 36019+20n | Possible |
| Parameter area | Mark detection setting parameter | 54000+20k to 54019+20k | Possible |
| Monitor data area | System monitor data | 4000 to 4299, 31300 to 31549, 87000 to 87649 | Not possible |
| Monitor data area | Axis monitor data | 2400+100n to 2499+100n, 59300+100n to 60899+100n | Not possible |
| Monitor data area | Mark detection monitor data | 54960+80k to 55039+80k | Not possible |
| Control data area | System control data | 5900 to 5999 | Possible |
| Control data area | Axis control data | 4300+100n to 4399+100n<br>30100+10n to 30109+10n<br>57520+30n, 57522+30n | Possible |
| Control data area | Mark detection control data | 54640+10k to 54649+10k | Possible |
| Positioning data area (No.1 to 100) | Positioning data | 6000+1000n to 6999+1000n<br>71000+1000n, 71001+1000n | Possible |
| Positioning data area (No.101 to 600) | Positioning data | Set with the engineering tool. | Possible |
| Block start data area (No.7000) | Block start data | 22000+400n to 22049+400n | Possible |
| Block start data area (No.7000) | Block start data | 22050+400n to 22099+400n | Possible |
| Block start data area (No.7000) | Condition data | 22100+400n to 22199+400n | Possible |
| Block start data area (No.7001) | Block start data | 22200+400n to 22249+400n | Possible |
| Block start data area (No.7001) | Block start data | 22250+400n to 22299+400n | Possible |
| Block start data area (No.7001) | Condition data | 22300+400n to 22399+400n | Possible |
| Block start data area (No.7002) | Block start data | Set with the engineering tool. | Possible |
| Block start data area (No.7002) | Condition data | Set with the engineering tool. | Possible |
| Block start data area (No.7003) | Block start data | Set with the engineering tool. | Possible |
| Block start data area (No.7003) | Condition data | Set with the engineering tool. | Possible |
| Block start data area (No.7004) | Block start data | Set with the engineering tool. | Possible |
| Block start data area (No.7004) | Condition data | Set with the engineering tool. | Possible |
| Servo parameter area [FX5-SSC-S] | Servo series | 28400+100n | Possible |
| Servo parameter area [FX5-SSC-S] | Servo parameter group*2: PA: PA01 to PA18 | 28401+100n to 28418+100n | Possible |
| Servo parameter area [FX5-SSC-S] | Servo parameter group*2: PA: PA19 | 64464+70n | Possible |
| Servo parameter area [FX5-SSC-S] | Servo parameter group*2: PA: PA20 to PA32 | 64400+70n to 64412+70n | Possible |
| Servo parameter area [FX5-SSC-S] | Servo parameter group*2: PB | 28419+100n to 28463+100n | Possible |
| Servo parameter area [FX5-SSC-S] | Servo parameter group*2: PB | 64413+70n to 64431+70n | Possible |
| Servo parameter area [FX5-SSC-S] | Servo parameter group*2: PC | 28464+100n to 28495+100n | Possible |
| Servo parameter area [FX5-SSC-S] | Servo parameter group*2: PC | 64432+70n to 64463+70n | Possible |
| Servo parameter area [FX5-SSC-S] | Servo parameter group*2: PD | 65520+340n to 65567+340n | Possible |
| Servo parameter area [FX5-SSC-S] | Servo parameter group*2: PE | 65568+340n to 65631+340n | Possible |
| Servo parameter area [FX5-SSC-S] | Servo parameter group*2: PS | 65712+340n to 65743+340n | Possible |
| Servo parameter area [FX5-SSC-S] | Servo parameter group*2: PF | 65632+340n to 65679+340n | Possible |
| Servo parameter area [FX5-SSC-S] | Servo parameter group*2: Po | 65680+340n to 65711+340n | Possible |
| Servo parameter area [FX5-SSC-S] | Servo parameter group*2: PL | 65744+340n to 65791+340n | Possible |
| Synchronous control area*3 | Servo input axis parameter | 32800+10n to 32805+10n | Possible |
| Synchronous control area*3 | Servo input axis monitor data | 33120+10n to 33127+10n | Not possible |
| Synchronous control area*3 | Synchronous encoder axis parameter | 34720+20j to 34735+20j | Possible |
| Synchronous control area*3 | Synchronous encoder axis control data | 35040+10j to 35048+10j | Possible |
| Synchronous control area*3 | Synchronous encoder axis monitor data | 35200+20j to 35212+20j | Not possible |
| Synchronous control area*3 | Synchronous encoder axis parameters via link device | 35520+20j to 35534+20j | Possible |
| Synchronous control area*3 | Synchronous control system control data | 36320, 36322 | Possible |
| Synchronous control area*3 | Synchronous parameter | 36400+200n to 36513+200n | Possible |
| Synchronous control area*3 | Synchronous control monitor data | 42800+40n to 42835+40n | Not possible |
| Synchronous control area*3 | Control data for synchronous control | 44080+20n to 44090+20n | Possible |
| Synchronous control area*3 | Cam operation control data | 45000 to 53791 | Possible |
| Synchronous control area*3 | Cam operation monitor data | 53800 to 53801 | Not possible |
| Synchronous control area*3 | Command generation axis parameter | Set with the engineering tool. | Possible |
| Synchronous control area*3 | Command generation axis control data | 61860 to 62883 | Possible |
| Synchronous control area*3 | Command generation axis monitor data | 60900 to 61859 | Not possible |
| Synchronous control area*3 | Command generation axis positioning data | Set with the engineering tool. | Possible |
| CC-Link IE TSN network area [FX5-SSC-G]*4 | Link device (RX) area | 63140 to 64163 | Not possible |
| CC-Link IE TSN network area [FX5-SSC-G]*4 | Link device (RY) area | 64164 to 65187 | Possible |
| CC-Link IE TSN network area [FX5-SSC-G]*4 | Link device (RWw) area | 65188 to 66211 | Possible |
| CC-Link IE TSN network area [FX5-SSC-G]*4 | Link device (RWr) area | 66212 to 67235 | Not possible |
| CC-Link IE TSN network area [FX5-SSC-G]*4 | Device station offset/size data | 68900 to 70995 | Not possible |

*In the original (table continues from p.606 to p.607): the first column (area) is merged over each group of rows. "Writing possibility" is merged: "Possible" over all Parameter area rows; "Not possible" over all Monitor data area rows; "Possible" over all Control data area rows; "Possible" over the Positioning data area rows and all Block start data area rows (No.7000 to No.7004); "Possible" over all Servo parameter area [FX5-SSC-S] rows. "Positioning data" is merged over the Positioning data area (No.1 to 100) and (No.101 to 600) rows. For block start data area No.7000 and No.7001, "Block start data" is merged over 2 address rows. For block start data area No.7002 to No.7004, "Set with the engineering tool." is merged over all 6 rows. In the servo parameter area, "Servo parameter group*2" is merged over all group rows, "PA" over PA01 to PA18 / PA19 / PA20 to PA32, and "PB" / "PC" each over 2 address rows; the sub-items are written here as "group: sub-group: range". Expanded to each row.

*1 Use of skipped address Nos. is prohibited. If used, the system may not operate correctly.
*2 Since the servo parameters of MR-J5(W)-B are not in the buffer memory, use GX Works3 or axis control data to set them. For details, refer to the following.
→Page 845 Connection with MR-J5(W)-B
*3 For details, refer to "List of Buffer Memory Addresses (for Synchronous Control)" in the following manual.
[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Advanced Synchronous Control)
*4 For details, refer to "Buffer memory" in the following manual.
[Other manual] MELSEC iQ-F FX5 Motion Module User's Manual (CC-Link IE TSN)

> **Point**
> [FX5-SSC-S]
> When the parameter of the servo amplifier side is changed by the following method, the Simple Motion module reads parameters automatically, and the data is transmitted to the servo parameter area in the buffer memory and internal memory (nonvolatile).
> - When changing the servo parameters by the auto tuning.
> - When the servo parameter is changing after the MR Configurator2 is connected directly with the servo amplifier.

### Timing for data transfers (データ転送のタイミング) (11.9 / original p.608)

Parameters of the Simple Motion module/Motion module are categorized as being either module parameters or Simple Motion module settings. Each parameter is reflected to the buffer memory of the Simple Motion module/Motion module at the following timing.

| Parameter reflection timing | Operation | Parameter setting value reflected to buffer memory: Module parameter*1 | Parameter setting value reflected to buffer memory: Simple Motion module setting*2 |
|---|---|---|---|
| Power ON | Power ON | Parameters set from the engineering tool*3 | Parameters stored within the Simple Motion module |
| Module initialization | [Cd.2] Parameter initialization request | Default setting (Initial setting) | Default setting (Initial setting) |

*In the original, the header "Parameter setting value reflected to buffer memory" spans the 2 columns Module parameter / Simple Motion module setting (written here as combined headers), and "Default setting (Initial setting)" is merged over those 2 columns in the Module initialization row. Expanded to each column.

*1 Certain module parameters are reflected within the Simple Motion module/Motion module by turning "[Cd.190] PLC READY" OFF → ON.
*2 When the reflection source does not exist at the reflection timing, refer to the following.
→Page 607 (1) Transmitting data when power is turned ON or CPU module is reset
*3 When not set from the engineering tool, the default value is used.

### Data transmission process (データの転送処理) (11.9 / original p.609-623)

The data is transmitted between the memories of Simple Motion module/Motion module with steps (1) to (10) shown below.
The data transmission patterns correspond to the numbers (1) to (10) in the following referential drawings.

| No. | Data transmission pattern | Referential drawing: FX5-SSC-S | Referential drawing: FX5-SSC-G |
|---|---|---|---|
| (1) | Transmitting data when power is turned ON or CPU module is reset | Page 615 Pattern (1) to (5) | Page 619 Pattern (1) to (4) |
| (2) | Transmitting data with TO command from CPU module | Page 615 Pattern (1) to (5) | Page 619 Pattern (1) to (4) |
| (3) | Validate parameters when "[Cd.190] PLC READY" changes from OFF to ON | Page 615 Pattern (1) to (5) | Page 619 Pattern (1) to (4) |
| (4) | Accessing with FROM command from CPU module | Page 615 Pattern (1) to (5) | Page 619 Pattern (1) to (4) |
| (5) | Reading the servo parameter from the servo amplifier [FX5-SSC-S] | Page 615 Pattern (1) to (5) | — |
| (6) | Writing the flash ROM by a CPU module request | Page 616 Pattern (6) and (7) | Page 620 Pattern (6) and (7) |
| (7) | Writing the flash ROM by a request from the engineering tool | Page 616 Pattern (6) and (7) | Page 620 Pattern (6) and (7) |
| (8) | Reading data from buffer memory/internal memory to the engineering tool | Page 617 Pattern (8) and (9) | Page 621 Pattern (8) and (9) |
| (9) | Writing data from the engineering tool to buffer memory/internal memory | Page 617 Pattern (8) and (9) | Page 621 Pattern (8) and (9) |
| (10) | Transmitting servo parameter [FX5-SSC-S] | Page 618 Pattern (10) | — |
| (10) | Transmitting servo parameter [FX5-SSC-G] | — | — |

*In the original, the header "Data transmission pattern" spans the number column and the name column, and "Referential drawing" spans FX5-SSC-S / FX5-SSC-G (written here as combined headers). Merged cells: FX5-SSC-S "Page 615 Pattern (1) to (5)" over (1) to (5); FX5-SSC-G "Page 619 Pattern (1) to (4)" over (1) to (4); "Page 616/620 Pattern (6) and (7)" over (6) and (7); "Page 617/621 Pattern (8) and (9)" over (8) and (9); "(10)" over the 2 rows [FX5-SSC-S] / [FX5-SSC-G]. Expanded to each row. (Page numbers are printed page numbers.)

#### (1) Transmitting data when power is turned ON or CPU module is reset ((1)電源ON/CPUユニットリセット時のデータ転送) (11.9 / original p.609)

When the power is turned ON or the CPU module is reset, the "parameter area (c)*1", "positioning data", "block start data" and "servo parameter" stored (backed up) in the flash ROM/internal memory (nonvolatile) are transmitted to the buffer memory and internal memory.
*1 For details, refer to the following.
→Page 602 Details of areas

#### (2) Transmitting data with TO command from CPU module ((2)CPUユニットからのTO命令によるデータ転送) (11.9 / original p.609)

The parameters or data is written from the CPU module to the buffer memory using the TO command*1.
At this time, when the "parameter area (b)*2", "positioning data", "block start data", and "control data" are written into the buffer memory with the TO command, it is simultaneously valid.
*1 Positioning data No.101 to 600 and Block start data No.7002 to 7004 can be set with only the engineering tool.
[FX5-SSC-S]
When using MR-J5(W)-B, "servo parameter" can be set only from engineering tool or axis control data ([Cd.130] to [Cd.132]).
*2 For details, refer to the following.
→Page 602 Details of areas

> **Point**
> [FX5-SSC-S]
> When a value other than "0" has been set to the servo parameter "[Pr.100] Servo series" inside the internal memory (nonvolatile), the power is turned ON or CPU module is reset to transmit the servo parameter inside the internal memory (nonvolatile) to the servo amplifier (servo amplifier LED indicates "b_"). After that, the TO instruction writes the servo parameter from the CPU module to the buffer memory so that the servo parameter in the buffer memory is not transmitted to the servo amplifier even if the "[Cd.190] PLC READY" is turned OFF then ON. Change the servo parameter with the above method, after setting the servo parameter "[Pr.100] Servo series" inside the internal memory (nonvolatile), to "0".

#### (3) Validate parameters when "[Cd.190] PLC READY" changes from OFF to ON ((3)"[Cd.190]シーケンサレディ"OFF → ON時の有効パラメータ) (11.9 / original p.610)

When the "[Cd.190] PLC READY" changes from OFF to ON, the data stored in the buffer memory's "parameter area (a)*1" is validated.
*1 For details, refer to the following.
→Page 602 Details of areas

> **Point**
> The setting values of the parameters that correspond to parameter area (b) are valid when written into the buffer memory with the TO command. However, the setting values of the parameters that correspond to parameter area (a) are not validated until the "[Cd.190] PLC READY" changes from OFF to ON.

#### (4) Accessing with FROM command from CPU module ((4)CPUユニットからのFROM命令によるアクセス) (11.9 / original p.610)

The data is read from the buffer memory to the CPU module using the FROM command*1.
*1 Positioning data No.101 to 600 and Block start data No.7002 to 7004 can be read with only the engineering tool.
[FX5-SSC-S]
When using MR-J5(W)-B, "servo parameter" can be set only from engineering tool or axis control data ([Cd.130] to [Cd.132]).

#### (5) Reading the servo parameter from the servo amplifier [FX5-SSC-S] ((5)サーボアンプからサーボパラメータ読出し[FX5-SSC-S]) (11.9 / original p.610)

When the parameter of the servo amplifier is changed, the servo parameter is read automatically from the servo amplifier to the buffer memory/internal memory and internal memory (nonvolatile).

> **Point**
> Parameters of the servo amplifier can be changed individually from the Simple Motion module by using the axis control data.

#### (6) Writing the flash ROM by a CPU module request ((6)CPUユニット要求によるフラッシュROM書込み) (11.9 / original p.610)

The following transmission process is carried out by setting "1" in "[Cd.1] Flash ROM write request".
- The "parameters", "positioning data (No.1 to 600)", "block start data (No.7000 to 7004)" and "servo parameter [FX5-SSC-S]" in the buffer memory/internal memory area are transmitted to the flash ROM/internal memory (nonvolatile).

#### (7) Writing the flash ROM by a request from the engineering tool ((7)エンジニアリングツールの要求によるフラッシュROM書込み) (11.9 / original p.610)

The following transmission processes are carried out with the [flash ROM write request] from the engineering tool. This transmission process is the same as (6) above.
- The "parameters", "positioning data (No.1 to 600)", "block start data (No.7000 to 7004)" and "servo parameter*1" in the buffer memory/internal memory area are transmitted to the flash ROM/internal memory (nonvolatile).

*1 Transferring of a servo parameter is possible only when using FX5-SSC-S.

> **Point**
> - Do not turn the power OFF or reset the CPU module while writing to the flash ROM. If the power is turned OFF or the CPU module is reset to forcibly end the process, the data backed up in the flash ROM/internal memory (nonvolatile) will be lost.
> - Do not write the data to the buffer memory/internal memory before writing to the flash ROM is completed.
> - The number of writes to the flash ROM with the program is 25 max. while the power is turned ON. Writing to the flash ROM beyond 25 times will cause the error "Flash ROM write number error" (error code: 1080H). Refer to →Page 753 List of Error Codes for details.
> - Monitoring is the number of writes to the flash ROM after power supply ON by the "[Md.19] Number of write accesses to flash ROM".

#### (8) Reading data from buffer memory/internal memory to the engineering tool ((8)バッファメモリ／内部メモリからエンジニアリングツールへのデータの読出し) (11.9 / original p.611)

The following transmission processes are carried out with the [Read from module] from the engineering tool.
- The "parameters", "positioning data (No.1 to 600)", "block start data (No.7000 to 7004)" and "servo parameter*1" in the buffer memory/internal memory area are transmitted to the engineering tool via the CPU module.

The following transmission processes are carried out with the [Monitor] from the engineering tool.
- The "monitor data" in the buffer memory area is transmitted to the engineering tool via the CPU module.

*1 Transferring of a servo parameter is possible only when using FX5-SSC-S.

#### (9) Writing data from the engineering tool to buffer memory/internal memory ((9)エンジニアリングツールからバッファメモリ／内部メモリへのデータの書込み) (11.9 / original p.611)

The following transmission processes are carried out with the [Write to module] from the engineering tool.
- The "parameters", "positioning data (No.1 to 600)", "block start data (No.7000 to 7004)" and "servo parameter*1" in the engineering tool are transmitted to the buffer memory/internal memory via the CPU module.

At this time, when [Flash ROM automatic write] is set with the engineering tool, the transmission processes indicated with "(7) Writing the flash ROM by a request from the engineering tool" are carried out.
*1 Transferring of a servo parameter is possible only when using FX5-SSC-S.

#### (10) Transmitting servo parameter [FX5-SSC-S] ((10)サーボパラメータの転送[FX5-SSC-S]) (11.9 / original p.611-614)

The servo parameter in the buffer memory/internal memory area is transmitted to the servo amplifier by the following timing.
- The servo parameter is transmitted to the servo amplifier when communications with servo amplifier start. The "extended parameter" and "servo parameter" in the buffer memory/internal memory area are transmitted to the servo amplifier.
- The following servo parameters in the buffer memory area are transmitted to the internal memory (nonvolatile) and servo amplifier when the "[Cd.190] PLC READY" turns from OFF to ON.

(Servo parameters transmitted at "[Cd.190] PLC READY" OFF → ON — boxed list in the original:)
- Auto tuning mode (PA08)
- Auto tuning response (PA09)
- Feed forward gain (PB04)
- Load to motor inertia ratio/load to motor mass ratio (PB06)
- Model loop gain (PB07)
- Position loop gain (PB08)
- Speed loop gain (PB09)
- Speed integral compensation (PB10)
- Speed differential compensation (PB11)

> **Point**
> When the "[Cd.190] PLC READY" is turned ON, the warning "SSCNET communication error" (warning code: 093EH) occurs, "Rotation direction selection/travel direction selection (PA14)"*1 is changed by the program or the engineering tool after the servo parameter is transmitted to servo amplifier (LED of the servo amplifier is indicated b_, C_, or d_). When "Rotation direction selection/travel direction selection (PA14)"*1 is changed, transmit the servo parameter to servo amplifier.

*1 For MR-J4(W)-B. "Travel direction selection (PA14)" for MR-J5(W)-B.

##### About the communication start with servo amplifier (サーボアンプとの通信開始について) (11.9 / original p.611)

Communication with servo amplifier is valid when following conditions are realized together.
- The power of Simple Motion module and servo amplifier is turned ON.
- The servo parameter "[Pr.100] Servo series" in the buffer memory of the Simple Motion module is set with a value other than "0".

When the power is turned ON or the CPU module is reset, the data stored in the flash ROM/internal memory (nonvolatile) is transmitted to the buffer memory/internal memory.
Therefore, when the servo parameter "[Pr.100] Servo series" stored in the internal memory (nonvolatile) is set with a value other than "0" and the module is started up in order of the servo amplifier and the Simple Motion module (even before the RUN LED of the CPU module is turned ON), the communication with the servo amplifier is started and the servo parameter stored in the internal memory (nonvolatile) is transmitted to the servo amplifier.

##### How to transfer the servo parameter setup from the program/engineering tool to the servo amplifier (プログラム／エンジニアリングツールから設定したサーボパラメータをサーボアンプへ転送する方法) (11.9 / original p.612)

The servo series of servo parameter "[Pr.100] Servo series" inside the internal memory (nonvolatile) set to "0". (Initial value: "0")
The setting value of the parameters that correspond to the servo parameter "[Pr.100] Servo series" inside the internal memory (nonvolatile) becomes valid when the power is turned ON or the CPU module is reset, after the communication with servo amplifier is not started.
However, the "[Cd.190] PLC READY" is changed from OFF to ON after setting the servo parameters ("[Pr.100] Servo series": except for 0) with the program/engineering tool the communication with servo amplifier starts.

##### How to transfer the servo parameter which wrote it in the internal memory (nonvolatile) to servo amplifier (保存用内部メモリに書き込んだサーボパラメータをサーボアンプへ転送する方法) (11.9 / original p.612)

Flash ROM writing carried out after the servo parameter is set up in the buffer memory/internal memory.
After that, when the power is turned ON or the CPU module is reset, the servo parameters stored in the internal memory (nonvolatile) is transmitted to the buffer memory/internal memory.
When the servo parameter is written in the internal memory (nonvolatile), it is unnecessary to use a setup from the program/engineering tool.

##### Servo parameter of the buffer memory/internal memory (バッファメモリ／内部メモリのサーボパラメータ) (11.9 / original p.612-613)

The following shows details about the operation timing and details at transmitting the servo parameter of the buffer memory/internal memory.

> **Point**
> - When the servo parameter is written in the internal memory (nonvolatile), it is unnecessary to use a setup from the program/engineering tool.
> - Axis connection time varies depending on the number of axes and the servo amplifier's power supply ON timing. And, time when "20: Servo amplifier has not been connected/servo amplifier power OFF" is set in "[Md.26] Axis operation status" is also varies.
>
> *(Note: "is also varies" is as printed in the original.)*

- When the servo amplifier's power supply is turned ON before the system's power supply ON and the servo parameter "[Pr.100] Servo series" ≠ "0" is stored in the internal memory (nonvolatile)

| Item | Details |
|---|---|
| Communication start timing with the servo amplifier | Initialization completion ((A) in the following figure) |
| Servo parameter to be transferred | The data stored (backed up) in the internal memory (nonvolatile). |

[Figure] Timing chart: servo amplifier power ON before system power ON, [Pr.100] ≠ 0 in internal memory (nonvolatile) (original p.612)
- Time markers (left to right): Simple Motion module power ON → Buffer memory/internal memory data setting → Initialization completion of Simple Motion module (A) → Axis connection completion.
- Servo parameter of buffer memory/internal memory: "Indefinite value" from power ON until buffer memory/internal memory data setting; then "Value of internal memory (nonvolatile)".
- "Transfer the servo parameter at this point to the servo amplifier" is indicated at (A) Initialization completion.
- Communication operation status with servo amplifier: "Communication invalid" until (A); "Communication start (Axis connection)" from (A) until Axis connection completion; then "During communication".
- [Md.26] Axis operation status: "0 (Standby)" until buffer memory/internal memory data setting; then "20 (Servo amplifier has not been connected/servo amplifier power OFF)" until Axis connection completion; then "21 (Servo OFF)".

- When the servo amplifier's power supply is turned ON before the system's power supply ON and the servo parameter "[Pr.100] Servo series" = "0" is stored in the internal memory (nonvolatile) (original p.613)

| Item | Details |
|---|---|
| Communication start timing with the servo amplifier | The "[Cd.190] PLC READY" is turned ON from OFF. ((B) in the following figure) |
| Servo parameter to be transferred | The data written from the program/engineering tool before the "[Cd.190] PLC READY" ON. ((A) in the following figure) |

[Figure] Timing chart: servo amplifier power ON before system power ON, [Pr.100] = 0 in internal memory (nonvolatile) (original p.613)
- Time markers (left to right): Simple Motion module power ON → Buffer memory/internal memory data setting → Initialization completion of Simple Motion module → CPU module RUN → Servo parameter setting from the program/engineering tool (A) → "[Cd.190] PLC READY" OFF → ON (B) → Axis connection completion.
- [Cd.190] PLC READY: turns ON at (B). READY ([Md.140] Module status: b0) turns ON after [Cd.190] PLC READY ON (arrow from PLC READY to READY).
- Servo parameter of buffer memory/internal memory: "Indefinite value" → (at data setting) "Value of internal memory (nonvolatile)" → (at (A)) "Write value by the program/engineering tool".
- "Transfer the servo parameter at this point to the servo amplifier" is indicated at (B).
- Communication operation status with servo amplifier: "Communication invalid" until Initialization completion; "Communication start valid" until (B); "Communication start (Axis connection)" from (B) until Axis connection completion; then "During communication".
- [Md.26] Axis operation status: "0 (Standby)" until data setting; "20 (Servo amplifier has not been connected/servo amplifier power OFF)" until Axis connection completion; then "21 (Servo OFF)".

- When the servo amplifier's power supply is turned ON after the "[Cd.190] PLC READY" is turned OFF to ON ((C) in the following figure)

| Item | Details |
|---|---|
| Communication start timing with the servo amplifier | When the servo amplifier had started ((B) in the following figure) |
| Servo parameter to be transferred | The data written from the program/engineering tool before the "[Cd.190] PLC READY" ON. ((A) in the following figure) |

[Figure] Timing chart: servo amplifier power ON after [Cd.190] PLC READY OFF → ON (original p.613)
- Time markers (left to right): Simple Motion module power ON → Buffer memory/internal memory data setting → Initialization completion of Simple Motion module → CPU module RUN → Servo parameter setting from the program/engineering tool (A) → "[Cd.190] PLC READY" OFF → ON (C) → Servo amplifier power ON (B) → Axis connection completion.
- [Cd.190] PLC READY: turns ON at (C). READY ([Md.140] Module status: b0) turns ON after [Cd.190] PLC READY ON.
- Servo parameter of buffer memory/internal memory: "Indefinite value" → (at data setting) "Value of internal memory (nonvolatile)" → (at (A)) "Write value by the program/engineering tool".
- "Transfer the servo parameter at this point to the servo amplifier" is indicated at (B) Servo amplifier power ON.
- Communication operation status with servo amplifier: "Communication invalid" until Initialization completion; "Communication start valid" until (B); "Communication start (Axis connection)" from (B) until Axis connection completion; then "During communication".
- [Md.26] Axis operation status: "0 (Standby)" until data setting; "20 (Servo amplifier has not been connected/servo amplifier power OFF)" until Axis connection completion; then "21 (Servo OFF)".

##### How to change individually the servo parameter after transfer of servo parameter (サーボパラメータ転送後にサーボパラメータを個別に変更する方法) (11.9 / original p.614)

The servo parameters can be individually changed from Simple Motion module with the following axis control data.
n: Axis No. - 1

| Setting item | | Setting details | Buffer memory address |
|---|---|---|---|
| [Cd.130] | Servo parameter read/write request | Set the write request of servo parameter.<br>Set "0001H" or "0002H" after setting "[Cd.131] Parameter No. (Setting for servo parameters to be changed)" and "[Cd.132] Change data".<br>0001H: 1 word write request<br>0002H: 2 words write request | 4354+100n |
| [Cd.131] | Parameter No. (Setting for servo parameters to be changed) | Set the servo parameter to be changed. | 4355+100n |
| [Cd.132] | Change data | Set the changed value of servo parameter set in "[Cd.131] Parameter No. (Setting for servo parameters to be changed)". | 4356+100n<br>4357+100n |

> **Point**
> - Both of the servo parameter area (internal memory (nonvolatile) and buffer memory/internal memory) of Simple Motion module and the parameter of servo amplifier are changed.
> - When the servo parameters that become valid by turning ON the servo amplifier's power supply are changed, be sure to turn ON twice the servo amplifier's power supply after change. (The servo amplifier's RAM data are changed by parameter setting, but the servo amplifier's EEPROM data are not changed. The EEPROM data before the change are overwritten to RAM by the servo amplifier's power supply ON again, and then the servo amplifier starts. After that, the changed data are written to the servo amplifier's EEPROM in an initial communication with Simple Motion module. Therefore, the changed data are overwritten to the RAM data by turning the servo amplifier's power supply ON again.)
> - If "[Cd.130] Servo parameter read/write request" is set to "0001H: 1 word write request" or "0002H: 2 words write request" in the following states, it becomes "0003H: Read/write failure ".
>   - The communication with the servo amplifier is not established or there is an error in the communication.
>   - "[Cd.131] Parameter No." is outside the setting range.
>   - The servo amplifier does not support the writing of the specified number of words.

##### Transfer from the CPU module to the Simple Motion module (CPUユニットからシンプルモーションユニットへの転送) (11.9 / original p.614)

When MR-J5(W)-B is used, set "0022H: 2 words write request to internal memory" or "0032H: 2 words read request from internal memory" in "[Cd.130] Servo parameter read/write request" of the axis control data to read/write the servo parameters from/to "Servo parameter (When MR-J5(W)-B is used)" of the internal memory.
For details of how to read and write from/to "Servo parameter (When MR-J5(W)-B is used)" of the internal memory by using the axis control data, refer to the following.
→Page 845 Connection with MR-J5(W)-B

#### (10) Transmitting servo parameter [FX5-SSC-G] ((10)サーボパラメータの転送[FX5-SSC-G]) (11.9 / original p.615-616)

On the CC-Link IE TSN network, when the device station parameter automatic setting is set to "Enabled", servo parameters controlled by the CPU module are transmitted when communications with the servo amplifier start.
When the device station parameter automatic setting is set to "Enabled", servo parameters controlled by the servo amplifier are enabled.
For the device station parameter automatic setting, refer to "Others" in the following manual.
[Other manual] MELSEC iQ-F FX5 Motion Module User's Manual (CC-Link IE TSN)
The Motion module checks whether the servo parameters transmitted from the CPU module and the servo parameters controlled by the servo amplifier are in the recommended setting when communications with the servo amplifier start.
When the parameters are not in the recommended setting, the error "Servo parameter invalid" (error code: 1DC8H) occurs and the setting values of the servo parameters are overwritten from the Motion module.
For details of the recommended setting of servo parameters, refer to the following.
→Page 850 Devices Compatible with CC-Link IE TSN [FX5-SSC-G]

*(Note: the two "Enabled" sentences above are as printed; the second one would be expected to read "Disabled" judging from the Control details figures below.)*

> **Point**
> When the error "Servo parameter invalid" (error code: 1DC8H), "[Md.190] Controller position value restoration complete status" becomes "0: Incomplete restoration" and servo ON cannot be performed.
> After resetting the error, cycle the power of the servo amplifier.

##### Control details (制御内容) (11.9 / original p.615-616)

- When the device station parameter automatic setting is set to "Disabled"

[Figure] Servo parameter transfer, device station parameter automatic setting "Disabled" (original p.615)
- Motion module ← (1) Servo parameter reading and checking ← Servo amplifier.
- Motion module → (2) Servo parameter writing → Servo amplifier.

- When the device station parameter automatic setting is set to "Enabled"

[Figure] Servo parameter transfer, device station parameter automatic setting "Enabled" (original p.615)
- GX Works3 ↔ (Writing/Reading project) ↔ Motion module (CPU module side).
- (1) Device station parameter automatic setting: from the CPU module/Motion module side to the Servo amplifier.
- Motion module ← (2) Reading/Checking servo parameter ← Servo amplifier.
- Motion module → (3) Writing servo parameter → Servo amplifier.

> **Point**
> - Transient communication (SLMP) is used for the reading and writing of servo parameters. For writing, servo parameters are saved by using the Store parameters request. For details of the Store parameters request, refer to the manual of the servo amplifier.
> - The timing of reading and checking servo parameter of the Motion module depends on the device station parameter automatic setting as follows.
>   When the device station automatic setting is "Valid": After the servo parameter is transferred from the CPU module.
>   When the device station parameter automatic setting is "Invalid": At the start of communication with the servo amplifier.
> - When the device station is used with the parameter automatic setting, the servo parameter "Parameter automatic backup update interval (PN20)"*1 is required to be set to perform "Automatic update of saved parameters" (automatic update when parameters are updated on the device station side). After the power is turned on, backup is performed every set time when the parameters that have been distributed and the current parameters are different. To reflect changes made to parameters in a project, reopen the servo parameter setting window and apply the servo parameters to the project by directly reading said parameters from the servo amplifier via "Read".
>
> [FX5-SSC-G]
> - In case of executing "Automatic update of saved parameters" with the device station parameter automatic setting, CPU module and the Motion module are needed to be updated to the following version.
>   CPU module: Ver. 1.250 or later, Motion module: Ver. 1.001 or later.
>   When using the earlier version of the above of CPU module and the Motion module the error "Servo parameter invalid" (error code: 1DC8H) occurs when the device station parameter automatic setting is set to "Enabled", be aware that rewritten servo parameters are not reflected to the CPU module. When updating servo parameters that are saved to the CPU module without using "Automatic update of saved parameters", execute the changes after performing reading from the servo amplifier.*2

*1 The number of times for writing data from the CPU module to the data memory is limited. For detail, refer to the following manual.
For MR-J5(W)-G: [Other manual] MR-J5-G/MR-J5W-G User's Manual(Parameter)
*2 The operation of "automatic update of saved parameters" is as follows depending on the combination of each version of the CPU module and the Motion module.

| Version of CPU module | Version of Motion module | Operation of Automatic update of saved parameters |
|---|---|---|
| 1.245 or before | 1.000 | Even if other than "0" is set to the servo parameter "Parameter automatic backup update interval (PN20)", it will not be backed up to the CPU module. |
| 1.250 or later | 1.000 | Even if other than "0" is set to the servo parameter "Parameter automatic backup update interval (PN20)", it will not be backed up to the CPU module. |
| 1.245 or before | 1.001 or later | When other than "0" is set to the servo parameter "Parameter automatic backup update interval (PN20)", Servo alarm [AL. 19E.1_Parameter automatic backup setting warning] will occur on the servo amplifier. Also, the servo parameter will not be backed up to the CPU module. |
| 1.250 or later | 1.001 or later | The servo parameter will be backed up to the CPU module in accordance with the setting of "Parameter automatic backup update interval (PN20)". |

*In the original, "1.000" and its operation text are merged over the 2 rows 1.245 or before / 1.250 or later, and "1.001 or later" is merged over the next 2 rows. Expanded to each row.

##### Restrictions (制約事項) (11.9 / original p.616)

Turning OFF the power of the servo amplifier while servo parameters are being changed to the recommended setting may cause the servo parameters to become corrupt. Turn OFF the power of the servo amplifier after checking that the Motion module is in one of the two following statuses.
- The error "Servo parameter invalid" (error code: 1DC8H) has occurred.
- "[Md.190] Controller position value restoration complete status" is complete (other than "0: Incomplete restoration").

#### Data transmission patterns [FX5-SSC-S] (データ転送処理のパターン[FX5-SSC-S]) (11.9 / original p.617-620)

##### Pattern (1) to (5) (パターン(1)～(5)) (11.9 / original p.617)

[Figure] Data transmission pattern (1) to (5) [FX5-SSC-S] (original p.617)
- Blocks: CPU module (top), Simple Motion module (middle; contains Buffer memory/Internal memory, Flash ROM, Internal memory (nonvolatile)), Servo amplifier (bottom).
- Buffer memory/Internal memory: Parameter area (a) / (b) / (c), Positioning data area (No.1 to 600), Block start data area (No.7000 to 7004), Servo parameter area, Monitor data area, Control data area (monitor and control data areas drawn in gray).
- Flash ROM: Parameter area (a) / (b) / (c), Positioning data area (No.1 to 600), Block start data area (No.7000 to 7004). Internal memory (nonvolatile): Servo parameter area.
- (1) Power supply ON/the CPU module reset: arrow from Flash ROM + Internal memory (nonvolatile) (bracketed together) to the buffer memory/internal memory areas from Parameter area (a) to Servo parameter area (bracketed).
- (2) TO command: arrow from CPU module to Buffer memory/Internal memory. (4) FROM command: arrow from Buffer memory/Internal memory to CPU module.
- (5) Servo amplifier data read: arrow from Servo amplifier up to the Buffer memory/Internal memory, branching to the Servo parameter area of the Internal memory (nonvolatile).
- An arrow from Buffer memory/Internal memory down to the Servo amplifier is also drawn (unlabeled in this figure).
- Legend at right: (1) Valid at power supply ON/the CPU module reset = Parameter area (c); (2) Valid upon execution of the TO command = Parameter area (b); (3) Valid at "[Cd.190] PLC READY" OFF → ON = Parameter area (a).

##### Pattern (6) and (7) (パターン(6)，(7)) (11.9 / original p.618)

[Figure] Data transmission pattern (6) and (7) [FX5-SSC-S] (original p.618)
- Blocks: Engineering tool (top), CPU module, Simple Motion module, Servo amplifier (bottom).
- (7) Flash ROM write request: Engineering tool → CPU module → Buffer memory/Internal memory → Flash ROM/Internal memory (nonvolatile) (hatched arrows).
- (6) Flash ROM write request (Set "1" in [Cd.1] with TO command): CPU module → Buffer memory/Internal memory; then "(6) Flash ROM write request" from Buffer memory/Internal memory → Flash ROM/Internal memory (nonvolatile) (solid arrows).
- Areas transferred (bracketed): Buffer memory/Internal memory Parameter area (a) to Servo parameter area → Flash ROM (Parameter area (a)/(b)/(c), Positioning data area (No.1 to 600), Block start data area (No.7000 to 7004)) and Internal memory (nonvolatile) Servo parameter area. Monitor data area and Control data area are drawn in gray (not transferred).

##### Pattern (8) and (9) (パターン(8)，(9)) (11.9 / original p.619)

[Figure] Data transmission pattern (8) and (9) [FX5-SSC-S] (original p.619)
- Blocks: Engineering tool (top), CPU module, Simple Motion module, Servo amplifier (bottom).
- (8) Data read: Buffer memory/Internal memory → CPU module → Engineering tool; bracket covers Parameter area (a) to Monitor data area.
- (9) Data write: Engineering tool → CPU module → Buffer memory/Internal memory; bracket covers Parameter area (a) to Servo parameter area.
- Control data area, Flash ROM and Internal memory (nonvolatile) are drawn in gray (not involved).

##### Pattern (10) (パターン(10)) (11.9 / original p.620)

[Figure] Data transmission pattern (10) [FX5-SSC-S] (original p.620)
- (10) Servo parameter transfer: from the Servo parameter area of Buffer memory/Internal memory (Simple Motion module) to the Servo amplifier.
- All other areas (Parameter areas, Positioning data area, Block start data area, Monitor data area, Control data area, Flash ROM, Internal memory (nonvolatile)) are drawn in gray (not involved).

#### Data transmission patterns [FX5-SSC-G] (データ転送処理のパターン[FX5-SSC-G]) (11.9 / original p.621-623)

##### Pattern (1) to (4) (パターン(1)～(4)) (11.9 / original p.621)

[Figure] Data transmission pattern (1) to (4) [FX5-SSC-G] (original p.621)
- Blocks: CPU module (top), Motion module (contains Buffer memory/Internal memory and Flash ROM). No servo amplifier block and no internal memory (nonvolatile)/servo parameter area are shown.
- Buffer memory/Internal memory: Parameter area (a) / (b) / (c), Positioning data area (No.1 to 600), Block start data area (No.7000 to 7004), Monitor data area, Control data area (monitor and control data areas drawn in gray).
- (1) Power supply ON/the CPU module reset: arrow from Flash ROM (Parameter area (a) to Block start data area) to Buffer memory/Internal memory (Parameter area (a) to Block start data area).
- (2) TO command: CPU module → Buffer memory/Internal memory. (4) FROM command: Buffer memory/Internal memory → CPU module.
- Legend at right: (1) Valid at power supply ON/the CPU module reset = Parameter area (c); (2) Valid upon execution of the TO command = Parameter area (b); (3) Valid at "[Cd.190] PLC READY" OFF → ON = Parameter area (a).

##### Pattern (6) and (7) (パターン(6)，(7)) (11.9 / original p.622)

[Figure] Data transmission pattern (6) and (7) [FX5-SSC-G] (original p.622)
- Blocks: Engineering tool (top), CPU module, Motion module, Servo amplifier (bottom).
- (7) Flash ROM write request: Engineering tool → CPU module → Buffer memory/Internal memory → Flash ROM (hatched arrows).
- (6) Flash ROM write request (Set "1" in [Cd.1] with TO command): CPU module → Buffer memory/Internal memory; then "(6) Flash ROM write request" from Buffer memory/Internal memory → Flash ROM (solid arrows).
- Areas transferred (bracketed): Parameter area (a) to Block start data area (No.7000 to 7004) → Flash ROM (Parameter area (a)/(b)/(c), Positioning data area (No.1 to 600), Block start data area (No.7000 to 7004)). Monitor data area and Control data area are drawn in gray. No servo parameter area is shown.

##### Pattern (8) and (9) (パターン(8)，(9)) (11.9 / original p.623)

[Figure] Data transmission pattern (8) and (9) [FX5-SSC-G] (original p.623)
- Blocks: Engineering tool (top), CPU module, Motion module, Servo amplifier (bottom).
- (8) Data read: Buffer memory/Internal memory → CPU module → Engineering tool; bracket covers Parameter area (a) to Monitor data area.
- (9) Data write: Engineering tool → CPU module → Buffer memory/Internal memory; bracket covers Parameter area (a) to Block start data area (No.7000 to 7004).
- Control data area and Flash ROM are drawn in gray (not involved). No servo parameter area is shown.
