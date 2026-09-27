# 13 PROGRAMMING [FX5-SSC-G] (プログラミング[FX5-SSC-G]) (Chapter 13 / original p.676-720)

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

## Conversion range (変換範囲表 / original p.676-720)

| Original page | Section | Handling |
|---|---|---|
| p.676 | 13 PROGRAMMING [FX5-SSC-G] (chapter introduction) | Full text |
| p.676 | 13.1 Precautions for Creating Program (reading/writing the data, speed change interval, overrun, system configuration) | Full text |
| p.677 | 13.2 Creating a Program (general configuration of program) | Full text |
| p.678-679 | 13.3 List of labels used (module label, global label) | Full text |
| p.680-682 | 13.3 Program examples: Parameter setting program | Full text (ladder transcribed as mnemonic) |
| p.683-699 | 13.3 Program examples: Positioning data setting program (local labels, No.1 to No.11 positioning data setting programs) | Full text (ladder transcribed as mnemonic) |
| p.700-701 | 13.3 No.15 positioning data setting program (end of Positioning data setting program) | Full text (ladder transcribed as mnemonic) |
| p.702 | 13.3 Block start data setting program | Full text (local labels, ladder transcribed as mnemonic) |
| p.703 | 13.3 Home position return request OFF program / External command function valid setting program | Full text (local labels, ladder transcribed as mnemonic) |
| p.704 | 13.3 PLC READY signal ON program / All axis servo ON program | Full text (local labels, ladder transcribed as mnemonic) |
| p.705-706 | 13.3 Positioning start No. setting program (machine/fast home position return, positioning data No.1, speed-position switching, position-speed switching, high-level positioning control, fast home position return command OFF) | Full text (local labels, ladder transcribed as mnemonic) |
| p.707 | 13.3 Positioning start program / M code OFF program | Full text (local labels, ladder transcribed as mnemonic) |
| p.708-710 | 13.3 JOG operation setting / Inching operation setting / JOG operation/inching operation execution / Manual pulse generator operation programs | Full text (ladder transcribed as mnemonic) |
| p.711-713 | 13.3 Speed change / Override / Acceleration/deceleration time change / Torque change / Target position change programs | Full text (local labels, ladder transcribed as mnemonic) |
| p.714-715 | 13.3 Servo parameter reading/writing program / Step operation program | Full text (local labels, ladder transcribed as mnemonic) |
| p.716-718 | 13.3 Skip / Teaching / Continuous operation interrupt / Restart / Parameter initialization / Flash ROM write programs | Full text (local labels, ladder transcribed as mnemonic) |
| p.719-720 | 13.3 Error reset program / Axis stop program | Full text (local labels, ladder transcribed as mnemonic) |

## Table of Contents (目次)

- 13 PROGRAMMING [FX5-SSC-G] (プログラミング[FX5-SSC-G])
- 13.1 Precautions for Creating Program (プログラム作成上の注意事項)
- 13.2 Creating a Program (プログラムの作成)
- 13.3 Positioning Program Examples (For Using Labels) (位置決めプログラム例(ラベル使用時))

---

## 13 PROGRAMMING [FX5-SSC-G] (プログラミング[FX5-SSC-G]) (Chapter 13 / original p.676)

This chapter describes the programs required to carry out positioning control with the Motion module.
The program required for control is created allowing for the "start conditions", "start time chart", "device settings" and general control configuration. (The parameters, positioning data, block start data and condition data, etc., must be set in the Motion module according to the control to be executed, and a setting program for the control data or a start program for the various controls must be created.)

## 13.1 Precautions for Creating Program (プログラム作成上の注意事項) (13.1 / original p.676)

The common precautions to be taken when writing data from the CPU module to the buffer memory of the Motion module are described below.

#### Reading/writing the data (データの読出し／書込み) (13.1 / original p.676)

Setting the data explained in this chapter (various parameters, positioning data, block start data) should be set using an engineering tool. When set with the program, many programs and devices must be used. This will not only complicate the program, but will also increase the scan time. When rewriting the positioning data during continuous path control or continuous positioning control, rewrite the data four positioning data items before the actual execution. If the positioning data is not rewritten before the positioning data four items earlier is executed, the process will be carried out as if the data was not rewritten.

#### Restrictions to speed change execution interval (速度変更実行間隔の制約) (13.1 / original p.676)

Be sure there is an interval between the speed changes of 10 ms or more when carrying out consecutive speed changes by the speed change function or override function with the Motion module.

#### Process during overrun (オーバーラン時の処理) (13.1 / original p.676)

Overrun is prevented by the setting of the upper and lower stroke limits with the detailed parameter 1. However, this applies only when the Motion module is operating correctly. From a system safety perspective, creating an external circuit that includes a boundary limit switch that turns OFF the main circuit power of the servo amplifier when activated is recommended.

#### System configuration (システム構成) (13.1 / original p.676)

The following figure shows the system configuration used for the program examples.

[Figure] System configuration used for the program examples (original p.676)
- Modules connected from left to right: (1) FX5U-32MR/ES, (2) FX5-80SSC-G, (3) FX5-16EX/ES, (4) FX5-16EX/ES.
- From the External device: X00 to X17 go to (1), X20 to X37 go to (3), X40 to X54 go to (4) (arrows).
- A Servo amplifier (MR-J5-_G_) is connected below (2), and a Servo motor is connected to the servo amplifier.

## 13.2 Creating a Program (プログラムの作成) (13.2 / original p.677)

The "positioning control operation program" actually used is explained in this section.

### General configuration of program (プログラムの全体構成) (13.2 / original p.677)

The general configuration of the positioning control operation program is shown below.

| No. | Program name | Remark |
|---|---|---|
| 1 | Parameter setting program | • The program is not required when the parameter, positioning data, block start data, and servo parameter are set using an engineering tool.<br>• The setting of the home position return parameters is not required when the machine home position return control is not executed. |
| 2 | Positioning data setting program | • The program is not required when the parameter, positioning data, block start data, and servo parameter are set using an engineering tool.<br>• The setting of the home position return parameters is not required when the machine home position return control is not executed. |
| 3 | Block start data setting program | • The program is not required when the parameter, positioning data, block start data, and servo parameter are set using an engineering tool.<br>• The setting of the home position return parameters is not required when the machine home position return control is not executed. |
| 4 | Home position return request OFF program | Not required when the fast home position return is executed. |
| 5 | External command function valid setting program | — |
| 6 | PLC READY signal ON program | — |
| 7 | All axis servo ON program | — |
| 8 | Positioning start No. setting program | — |
| 9 | Positioning start program | — |
| 10 | M code OFF program | Not required when the M code output function is not used. |
| 11 | JOG operation setting program | Not required when the JOG operation is not used. |
| 12 | Inching operation setting program | Not required when the inching operation is not used. |
| 13 | JOG operation/inching operation execution program | Not required when the JOG operation or the inching operation is not used. |
| 14 | Manual pulse generator operation program | Not required when the manual pulse generator operation is not used. |
| 15 | Speed change program | Add the program as necessary. |
| 16 | Override program | Add the program as necessary. |
| 17 | Acceleration/deceleration time change program | Add the program as necessary. |
| 18 | Torque change program | Add the program as necessary. |
| 19 | Target position change program | Add the program as necessary. |
| 20 | Servo parameter reading/writing program | Add the program as necessary. |
| 21 | Step operation program | Add the program as necessary. |
| 22 | Skip program | Add the program as necessary. |
| 23 | Teaching program | Add the program as necessary. |
| 24 | Continuous operation interrupt program | Add the program as necessary. |
| 25 | Restart program | Add the program as necessary. |
| 26 | Parameter initialization program | Add the program as necessary. |
| 27 | Flash ROM write program | Add the program as necessary. |
| 28 | Error reset program | Add the program as necessary. |
| 29 | Axis stop program | — |

*In the original, the "Remark" cell is merged over No.1 to 3 (the two bullet items), over No.5 to 8 ("—"), and over No.15 to 28 ("Add the program as necessary."). Expanded to each row. The "—" of No.9 and No.29 are individual cells.
*No.4 remark reads "Not required when the fast home position return is executed." in the English original (as printed).

## 13.3 Positioning Program Examples (For Using Labels) (位置決めプログラム例(ラベル使用時)) (13.3 / original p.678-699)

### List of labels used (使用するラベル一覧) (13.3 / original p.678-679)

In the program examples, the labels to be used are assigned as follows.

#### Module label (ユニットラベル) (13.3 / original p.678-679)

| Classification | Label name | Description |
|---|---|---|
| Input signal | FX5SSC_1.stSysCtrl_D.bAllAxisServoOn_D | All axis servo ON |
| Input signal | FX5SSC_1.stSysMntr2_D.bReady_D | READY |
| Input signal | FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D | Synchronization flag |
| Input signal | FX5SSC_1.stSysMntr2_D.bnBusy_D[0] | Axis 1 BUSY signal |
| Output signal | FX5SSC_1.stSysCtrl_D.bPLC_Ready_D | PLC READY signal |
| Output signal | FX5SSC_1.stnAxCtrl2_D[0].uPositioningStart_D.0 | Axis 1 Positioning start signal |
| Parameter | FX5SSC_1.stnAxPrm_D[0].dHomePosition_D | Axis 1 Home position address |
| Parameter | FX5SSC_1.stnAxPrm_D[0].dSoftwareStrokeLowerLimit_D | Axis 1 Software stroke limit lower limit value |
| Parameter | FX5SSC_1.stnAxPrm_D[0].dSoftwareStrokeUpperLimit_D | Axis 1 Software stroke limit upper limit value |
| Parameter | FX5SSC_1.stnAxPrm_D[0].uExternalCommandFunctionMode_D | Axis 1 External command function selection |
| Parameter | FX5SSC_1.stnAxPrm_D[0].uExternalCommandSignalMode_D | Axis 1 External command signal selection |
| Parameter | FX5SSC_1.stnAxPrm_D[0].uUnitMagnification_D | Axis 1 Unit magnification (AM) |
| Parameter | FX5SSC_1.stnAxPrm_D[0].uUnit_D | Axis 1 Unit setting |
| Parameter | FX5SSC_1.stnAxPrm_D[0].uVP_Mode_D | Axis 1 Speed-position function selection |
| Parameter | FX5SSC_1.stnAxPrm_D[0].uV_CommandPosition_D | Axis 1 Command position value during speed control |
| Parameter | FX5SSC_1.stnAxPrm_D[0].udHomingSpeed_D | Axis 1 Home position return speed |
| Parameter | FX5SSC_1.stnAXPrm_D[0].udJogSpeedLimit_D | Axis 1 JOG speed limit value |
| Parameter | FX5SSC_1.stnAxPrm_D[0].udMovementAmountPerRotation_D | Axis 1 Movement amount per rotation (AL) |
| Parameter | FX5SSC_1.stnAxPrm_D[0].udPulsesPerRotation_D | Axis 1 Number of pulses per rotation (AP) |
| Parameter | FX5SSC_1.stnAXPrm_D[0].udSpeedLimitValue_D | Axis 1 Speed limit value |
| Axis monitor data | FX5SSC_1.stnAxMntr_D[0].uStatus_D.3 | Axis 1 Home position return request flag |
| Axis monitor data | FX5SSC_1.stnAxMntr_D[0].uStatus_D.9 | Axis 1 Axis warning detection |
| Axis monitor data | FX5SSC_1.stnAxMntr_D[0].uStatus_D.C | Axis 1 M code ON |
| Axis monitor data | FX5SSC_1.stnAxMntr_D[0].uStatus_D.D | Axis 1 Error detection |
| Axis monitor data | FX5SSC_1.stnAxMntr_D[0].uStatus_D.E | Axis 1 Start complete |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uClearHomingRequestFlag_D | Axis 1 Home position return request flag OFF request |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uClear_M_Code_D | Axis 1 M code OFF request |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uEnablePV_Switching_D | Axis 1 Position-speed switching enable flag |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uEnableVP_Switching_D | Axis 1 Speed-position switching enable flag |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uExternalCommandValid_D | Axis 1 External command valid |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uForwardNewTorque_D | Axis 1 New torque value/forward new torque value |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uInchingMovementAmount_D | Axis 1 Inching movement amount |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uInterruptOperation_D | Axis 1 Interrupt request during continuous operation |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uOverride_D | Axis 1 Positioning operation speed override |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uSkip_D | Axis 1 Skip command |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uStepMode_D | Axis 1 Step mode |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uStepStartInformation_D | Axis 1 Step start information |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uStepValid_D | Axis 1 Step valid flag |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uTeachingDataSelection_D | Axis 1 Teaching data selection |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uTeachingPositioningDataNo_D | Axis 1 Teaching positioning data No. |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].udJOG_Speed_D | Axis 1 JOG speed |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].udPV_NewSpeed_D | Axis 1 Position-speed switching control speed change register |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].udVP_NewMovementAmount_D | Axis 1 Speed-position switching control movement amount change register |
| System control data | FX5SSC_1.stSysCtrl_D.dInputValueForManualPulseGeneratorViaCPU_D | Axis 1 Input value for manual pulse generator via CPU |
| Axis control data 2 | FX5SSC_1.stnAxCtrl2_D[0].uStopAxis_D.0 | Axis 1 Axis stop |

*In the original, the "Classification" cells (Input signal, Output signal, Parameter, Axis monitor data, Axis control data 1) are merged cells. Expanded to each row. The table spans p.678 and p.679 (43 rows on p.678, 2 rows on p.679); the header row (Classification / Label name / Description) is repeated on p.679. The label name of the "System control data" row is printed on two lines ("...ManualPulseGeneratorVia" / "CPU_D").
*"stnAXPrm_D" (capital X) in the udJogSpeedLimit_D and udSpeedLimitValue_D rows is as printed.

#### Global label (グローバルラベル) (13.3 / original p.679)

The following describes the global labels used in the program examples. Set the global labels as follows.

- Global label that the assignment device is not to be set (The unused internal relay and data device are automatically assigned when the assignment device is not set.)

[Figure] Global label setting screen (labels without assignment device) (original p.679). Transcribed from the screen capture below.

| No. | Label Name | Data Type | Class | Assign |
|---|---|---|---|---|
| 1 | G_bInitializeParameterReq | Bit | VAR_GLOBAL | (blank) |
| 2 | G_bWriteFlashReq | Bit | VAR_GLOBAL | (blank) |
| 3 | G_bDuringJogInchingOperation | Bit | VAR_GLOBAL | (blank) |
| 4 | G_bDuringMPGOperation | Bit | VAR_GLOBAL | (blank) |

- Global label that the assignment device is to be set

[Figure] Global label setting screen (labels with assignment device) (original p.679). Transcribed from the screen capture below.

| No. | Label Name | Data Type | Class | Assign |
|---|---|---|---|---|
| 5 | G_bInputOPRReqFlagOffReq | Bit | VAR_GLOBAL | X2 |
| 6 | G_bInputExternalCommandValidReq | Bit | VAR_GLOBAL | X3 |
| 7 | G_bInputExternalCommandInvalidReq | Bit | VAR_GLOBAL | X4 |
| 8 | G_bInputOPRStartReq | Bit | VAR_GLOBAL | X5 |
| 9 | G_bInputFastOPRStartReq | Bit | VAR_GLOBAL | X6 |
| 10 | G_bInputSetStartPositioningNoReq | Bit | VAR_GLOBAL | X7 |
| 11 | G_bInputSpeedPositionSwitchingReq | Bit | VAR_GLOBAL | X10 |
| 12 | G_bInputSpeedPositionSwitchingEnableReq | Bit | VAR_GLOBAL | X11 |
| 13 | G_bInputSpeedPositionSwitchingDisableReq | Bit | VAR_GLOBAL | X12 |
| 14 | G_bInputChangeSpeedPositionSwitchingMovementAmount | Bit | VAR_GLOBAL | X13 |
| 15 | G_bInputStartAdvancedPositioningReq | Bit | VAR_GLOBAL | X14 |
| 16 | G_bInputStartPositioningReq | Bit | VAR_GLOBAL | X15 |
| 17 | G_bInputMcodeOffReq | Bit | VAR_GLOBAL | X16 |
| 18 | G_bInputSetJogSpeedReq | Bit | VAR_GLOBAL | X17 |
| 19 | G_bInputForwardJogStartReq | Bit | VAR_GLOBAL | X20 |
| 20 | G_bInputReverseJogStartReq | Bit | VAR_GLOBAL | X22 |
| 21 | G_bInputStartMPGReq | Bit | VAR_GLOBAL | X23 |
| 22 | G_bInputChangeSpeedReq | Bit | VAR_GLOBAL | X24 |
| 23 | G_bInputOverrideReq | Bit | VAR_GLOBAL | X25 |
| 24 | G_bInputChangeAccDecTimeReq | Bit | VAR_GLOBAL | X26 |
| 25 | G_bInputChangeAccDecTimeDisable | Bit | VAR_GLOBAL | X27 |
| 26 | G_bInputChangeTorqueReq | Bit | VAR_GLOBAL | X30 |
| 27 | G_bInputStepOperationReq | Bit | VAR_GLOBAL | X31 |
| 28 | G_bInputSkipReq | Bit | VAR_GLOBAL | X32 |
| 29 | G_bInputTeachingReq | Bit | VAR_GLOBAL | X33 |
| 30 | G_bInputStopContinuousOperationReq | Bit | VAR_GLOBAL | X34 |
| 31 | G_bInputRestartReq | Bit | VAR_GLOBAL | X35 |
| 32 | G_bInputInitializeParameterReq | Bit | VAR_GLOBAL | X36 |
| 33 | G_bInputWriteFlashReq | Bit | VAR_GLOBAL | X37 |
| 34 | G_bInputErrResetReq | Bit | VAR_GLOBAL | X40 |
| 35 | G_bInputStopReq | Bit | VAR_GLOBAL | X41 |
| 36 | G_bInputPositionSpeedSwitchingReq | Bit | VAR_GLOBAL | X42 |
| 37 | G_bInputPositionSpeedSwitchingEnableReq | Bit | VAR_GLOBAL | X43 |
| 38 | G_bInputPositionSpeedSwitchingDisableReq | Bit | VAR_GLOBAL | X44 |
| 39 | G_bInputChangePositionSpeedSwitchingSpeedReq | Bit | VAR_GLOBAL | X45 |
| 40 | G_bInputSetInchingMovementAmountReq | Bit | VAR_GLOBAL | X46 |
| 41 | G_bInputTargetPositionChangeReq | Bit | VAR_GLOBAL | X47 |
| 42 | G_bInputStepStartInformationReq | Bit | VAR_GLOBAL | X50 |
| 43 | G_bInputG_bInputSpeedPositionSwitchingAbsSetReq | Bit | VAR_GLOBAL | X51 |
| 44 | G_bAllAxisServoOnReq | Bit | VAR_GLOBAL | X52 |
| 45 | G_bInputServoParamChange | Bit | VAR_GLOBAL | X53 |
| 46 | G_bInputServoParamRead | Bit | VAR_GLOBAL | X54 |

*The originals are screen captures of the GX Works3 global label setting screen. The "..." button column and the drop-down marks of the "Class" column are not transcribed. The English screens have no comment column. The row numbers are as shown on the screens (the second table continues from No.5).
*No.19 is assigned X20 and No.20 is assigned X22 (X21 is not used), as printed. No.43 "G_bInputG_bInputSpeedPositionSwitchingAbsSetReq" is as printed.

### Program examples (for using labels) (プログラム例(ラベル使用時)) (13.3 / original p.680-699)

For details of the module function blocks (FBs), refer to "Simple Motion Module FB/Motion Module FB" in the following manual.
[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module Function Block Reference

Transcription notation:
- The ladder diagrams are transcribed as mnemonic. The number in parentheses is the step number shown at the left of the ladder rung in the original. After `;` is the device assigned to the label, as shown under the label in the ladder (`U1¥G` is written as `U1\G`), followed by the device comment shown in the ladder (green text).
- `// [Title]...` and `// ...` lines are the statements (light-blue bars) of the ladder, placed right before the instruction they belong to.
- A module FB (function block) call cannot be expressed as one mnemonic instruction; it is written as an `FB <instance>` line, followed by the input/output connections as `//` lines (transcription notation).
- Parallel branches are expressed with MPS/MRD/MPP/ORB/ANB (transcription of the ladder branch structure).
- Contact type: `LD`/`AND` = normally open, `LDI`/`ANI` = normally closed, `LDP`/`ANDP` = rising edge (↑), `LDF` = falling edge (↓).

#### Parameter setting program (パラメータ設定プログラム) (13.3 / original p.680-682)

The program is not required when the parameter is set by "Module Parameter" using an engineering tool.
Set the local labels as follows.

[Figure] Local label setting screen (original p.680). Transcribed from the screen capture below.

| No. | Label Name | Data Type | Class |
|---|---|---|---|
| 1 | bServoNetworkCompositionParam (truncated in the cell) | Bit | VAR |
| 2 | bBasicParamSetComp | Bit | VAR |
| 3 | bDetailedParamSetComp | Bit | VAR |
| 4 | bOPRParamSetComp | Bit | VAR |

*The label name of No.1 is cut off at the right edge of the "Label Name" cell on the screen ("bServoNetworkCompositionParam"; the Japanese edition shows "bServoNetworkCompositionParamSetComp"). The "..." button column and the drop-down marks are not transcribed.

##### Setting for servo network configuration parameter (axis 1) (サーボネットワーク構成パラメータ(軸1)の設定) (13.3 / original p.680)

```
// [Title]Setting for servo network configuration parameter (axis 1)
// When changing, write to the flash ROM after setting values to the buffer memory
(0)   LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1  R:Synchronization flag(Direct)
      // IP address: set to 192.168.3.1
      MOV   H301 U1\G58024                                    ; Axis 1 IP address (L)
      // IP address: set to 192.168.3.1
      MOV   H0C0A8 U1\G58025                                  ; Axis 1 IP address (H)
      // Multidrop No.: set to 0
      MOV   H0 U1\G58028
```

- Contact type (read from figure): bSynchronizationFlag_D is a rising edge (↑) contact.
- In the original, the outputs of this rung are only the three MOV instructions above (no SET of bServoNetworkCompositionParam... is drawn). The next rung starts at step (293).

##### Setting for basic parameter 1 (axis 1) (基本パラメータ1(軸1)の設定) (13.3 / original p.680)

```
// [Title]Setting for basic parameter 1 (axis 1)
(293) LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1  R:Synchronization flag(Direct)
      // Unit setting (0: mm)
      MOV   K0 FX5SSC_1.stnAxPrm_D[0].uUnit_D                 ; U1\G0  RW:Unit setting(Direct)
      // Unit magnification setting (×1)
      MOV   K1 FX5SSC_1.stnAxPrm_D[0].uUnitMagnification_D    ; U1\G1  RW:Unit magnification (AM)(Direct)
      // Number of pulses per rotation (4194304pls)
      DMOVP K4194304 FX5SSC_1.stnAxPrm_D[0].udPulsesPerRotation_D   ; U1\G2  RW:Number of pulses per rotation (AP)(Direct)
      // Movement amount per rotation (25000.0μm)
      DMOVP K250000 FX5SSC_1.stnAxPrm_D[0].udMovementAmountPerRotation_D   ; U1\G4  RW:Movement amount per rotation (AL)(Direct)
      SET   bBasicParamSetComp                                ; Basic parameter 1 setting complete
```

- Contact type (read from figure): bSynchronizationFlag_D is a rising edge (↑) contact.
- The outputs are MOV (non-pulse) ×2, DMOVP ×2 and SET in the ladder (as printed).

##### Setting for detailed parameter 2 (axis 1) (詳細パラメータ2(軸1)の設定) (13.3 / original p.681)

```
// [Title]Setting for detailed parameter 2 (axis 1)
(541) LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1  R:Synchronization flag(Direct)
      // External command function selection (2:Speed⇔position switching)
      MOVP  K2 FX5SSC_1.stnAxPrm_D[0].uExternalCommandFunctionMode_D   ; U1\G62  RW:External command function selection(Direct)
      // External command signal selection (101: Axis 1 DOG signal)
      MOVP  K101 FX5SSC_1.stnAxPrm_D[0].uExternalCommandSignalMode_D   ; U1\G69  RW:External command signal selection(Direct)
      SET   bDetailedParamSetComp                             ; Detailed parameter 2 setting complete
```

- Contact type (read from figure): bSynchronizationFlag_D is a rising edge (↑) contact.

##### Setting for home position return basic parameter (axis 1) (原点復帰基本パラメータ(軸1)の設定) (13.3 / original p.681)

For the home position return method and home position return data, set the parameters of the driver to be used.

```
// [Title]Setting for home position return basic parameter (axis 1)
(757) LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1  R:Synchronization flag(Direct)
      // Home position address (0.0um)
      DMOVP K0 FX5SSC_1.stnAxPrm_D[0].dHomePosition_D         ; U1\G72  RW:Home position address(Direct)
      // Home position return speed (1000.00mm/min)
      DMOVP K100000 FX5SSC_1.stnAxPrm_D[0].udHomingSpeed_D    ; U1\G74  RW:Home position return speed(Direct)
      SET   bOPRParamSetComp                                  ; Home position return basic parameter setting complete
```

- Contact type (read from figure): bSynchronizationFlag_D is a rising edge (↑) contact.

##### Unit "degree" setting (axis 1) program (単位degree用設定(軸1)プログラム) (13.3 / original p.682)

```
// [Title]Unit "degree" setting (axis 1) program
(937) LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1  R:Synchronization flag(Direct)
      AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   ; X51  Speed-position switching (ABS) setting command
      // Unit setting (2: degree)
      MOVP  K2 FX5SSC_1.stnAxPrm_D[0].uUnit_D                 ; U1\G0  RW:Unit setting(Direct)
      // Movement amount per rotation (90.00000degree)
      DMOVP K9000000 FX5SSC_1.stnAxPrm_D[0].udMovementAmountPerRotation_D   ; U1\G4  RW:Movement amount per rotation (AL)(Direct)
      // Speed limit value (20000.000degree/min)
      DMOVP K20000000 FX5SSC_1.stnAxPrm_D[0].udSpeedLimitValue_D   ; U1\G10  RW:Speed limit value(Direct)
      // Software stroke limit upper limit value (0.00000degree/min)
      DMOVP K0 FX5SSC_1.stnAxPrm_D[0].dSoftwareStrokeUpperLimit_D   ; U1\G18  RW:Software stroke limit upper limit value(Direct)
      // Software stroke limit lower limit value (0.00000degree/min)
      DMOVP K0 FX5SSC_1.stnAxPrm_D[0].dSoftwareStrokeLowerLimit_D   ; U1\G20  RW:Software stroke limit lower limit value(Direct)
      // Feed current value during speed control (1: Update value)
      MOVP  K1 FX5SSC_1.stnAxPrm_D[0].uV_CommandPosition_D    ; U1\G30  RW:Current feed value during speed control(Direct)
      // Speed-position function selection (2: speed-position switching)
      MOVP  K2 FX5SSC_1.stnAxPrm_D[0].uVP_Mode_D              ; U1\G34  RW:Speed-position function selection(Direct)
      // JOG speed limit value (20000.000degree/min)
      DMOVP K20000000 FX5SSC_1.stnAxPrm_D[0].udJogSpeedLimit_D   ; U1\G48  RW:JOG speed limit value(Direct)
      // Home position return speed (1000.000degree/min)
      DMOVP K1000000 FX5SSC_1.stnAxPrm_D[0].udHomingSpeed_D   ; U1\G74  RW:Home position return speed(Direct)
```

- Contact type (read from figure): bSynchronizationFlag_D is a rising edge (↑) contact; G_bInputG_bInputSpeedPositionSwitchingAbsSetReq (X51) is a normally open contact in series.
- The unit in the software stroke limit statements ("degree/min") is as printed.
- In the ladder, the labels udSpeedLimitValue_D and udJogSpeedLimit_D are written as "FX5SSC_1.stnAxPrm_D[0]..." (lowercase x), while the module label table writes "stnAXPrm_D" (as printed).

#### Positioning data setting program (位置決めデータ設定プログラム) (13.3 / original p.683-699)

This program is not required when the data is set by "Positioning Data" using an engineering tool.
Set the local labels as follows.

[Figure] Local label setting screen (original p.683). Transcribed from the screen capture below.

| No. | Label Name | Data Type | Class |
|---|---|---|---|
| 1 | bSetPositioningData_bEN | Bit | VAR |
| 2 | bSetPositioningData2_bEN | Bit | VAR |
| 3 | bSetPositioningData3_bEN | Bit | VAR |
| 4 | bSetPositioningData4_bEN | Bit | VAR |
| 5 | bSetPositioningData5_bEN | Bit | VAR |
| 6 | bSetPositioningData6_bEN | Bit | VAR |
| 7 | bSetPositioningData10_bEN | Bit | VAR |
| 8 | bSetPositioningData11_bEN | Bit | VAR |
| 9 | bSetPositioningData15_bEN | Bit | VAR |

*The "..." button column and the drop-down marks are not transcribed. The English screen has no comment column.

Common notes for the positioning data setting programs below (read from figure):
- The step number at the left of each rung is printed wrapped over two lines (e.g. "(1572" / ")").
- The destination labels of the MOV/DMOV instructions are printed wrapped in the ladder cells (e.g. "M_FX5SSC_SetPositioningData_01A_1.pb_uOpeP" / "attern"); they are written joined here.
- The comments after `;` (for example "Da.1: Operation pattern") are the device comments shown under the destination labels.
- The No.15 positioning data setting program (p.700 and later) is not part of this file.

##### No.1 positioning data setting program (No.1位置決めデータ設定プログラム) (13.3 / original p.684-685)

```
// [Title]No.1 positioning data setting program
// <Positioning identifier>
//   Operation pattern: positioning complete
//   Control method: 1 axis linear control (ABS)
//   Acceleration time No.: 1, deceleration time No.: 2
//   M code: 9843
(1572) LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1  R:Synchronization flag(Direct)
       MOV   K0 M_FX5SSC_SetPositioningData_01A_1.pb_uOpePattern          ; Da.1: Operation pattern
       MOV   H1 M_FX5SSC_SetPositioningData_01A_1.pb_uCtrlSys             ; Da.2: Control system
       MOV   K1 M_FX5SSC_SetPositioningData_01A_1.pb_uAccTimeNo             ; Da.3: Acceleration time No.
       MOV   K2 M_FX5SSC_SetPositioningData_01A_1.pb_uDecTimeNo             ; Da.4: Deceleration time No.
       MOV   K9843 M_FX5SSC_SetPositioningData_01A_1.pb_uMcode            ; Da.10: M code
       MOV   K300 M_FX5SSC_SetPositioningData_01A_1.pb_uDwellTime           ; Da.9: Dwell time
       DMOV  K18000 M_FX5SSC_SetPositioningData_01A_1.pb_udCmdSpd             ; Da.8: Command speed
       MPS
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   ; X51  Speed-position switching (ABS) setting command
       DMOV  K1200000 M_FX5SSC_SetPositioningData_01A_1.pb_udCmdSpd             ; Da.8: Command speed
       MRD
       DMOV  K-500000 M_FX5SSC_SetPositioningData_01A_1.pb_dPositAdr            ; Da.6: Positioning address
       MRD
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   ; X51  Speed-position switching (ABS) setting command
       DMOV  K27000000 M_FX5SSC_SetPositioningData_01A_1.pb_dPositAdr            ; Da.6: Positioning address
       MPP
       DMOV  K0 M_FX5SSC_SetPositioningData_01A_1.pb_dArcAdr                ; Da.7: Arc address
       MOV   K0 M_FX5SSC_SetPositioningData_01A_1.pb_uInterpolationAxisNo1  ; Da.20: Axis to be interpolated No.1
       MOV   K0 M_FX5SSC_SetPositioningData_01A_1.pb_uInterpolationAxisNo2  ; Da.21: Axis to be interpolated No.2
       MOV   K0 M_FX5SSC_SetPositioningData_01A_1.pb_uInterpolationAxisNo3  ; Da.22: Axis to be interpolated No.3
       SET   bSetPositioningData_bEN                   ; No.1 Execution command
(1950) LD    bSetPositioningData_bEN                   ; No.1 Execution command
       FB    M_FX5SSC_SetPositioningData_01A_1
       // FB title: M_FX5SSC_SetPositioningData_01A_1 (M+FX5SSC_SetPos...) Positioning data setting FB
       // in  B: i_bEN         <- bSetPositioningData_bEN (normally open contact above)   ; Execution command
       // in  DUT: i_stModule  <- FX5SSC_1   ; Module label / Module label
       // in  UW: i_uAxis      <- K1         ; Target axis
       // in  UW: i_uDataNo    <- K1        ; Data No.
       // out o_bENO :B        -> (no connection shown)   ; Execution status
       // out o_bOK :B         -> (no connection shown)   ; Normal completion
       // out o_bErr :B        -> (no connection shown)   ; Error completion
       // out o_uErrId :UW     -> (no connection shown)   ; Error code
       // public variables shown in the FB: pb_uOpePatt..., pb_uCtrlSys, pb_uAccTim..., pb_uDecTim..., pb_uMcode, pb_uDwellTi..., pb_udCmdS..., pb_dPositAdr, pb_dArcAdr, pb_uInterpol..., pb_uInterpol..., pb_uInterpol...
```

- Step (1572) (p.684-685): bSynchronizationFlag_D is a rising edge (↑) contact. G_bInputG_bInputSpeedPositionSwitchingAbsSetReq (X51) is a normally open contact placed in series only before the second DMOV to pb_udCmdSpd (K1200000) and the second DMOV to pb_dPositAdr (K27000000); all other outputs are driven by the synchronization flag condition only. The original is a ladder diagram; MPS/MRD/MPP are added by this transcription.
- Step (1950) (p.685): the FB output pins (o_bENO, o_bOK, o_bErr, o_uErrId) only have lines extending to the right; no connection destination is shown. The FB instance name is shown as "M_FX5SSC_SetPos" / "itioningData_01A_1" and the type name as "(M+FX5SS" / "C_SetPos..." (truncated display).

##### No.2 positioning data setting program (No.2位置決めデータ設定プログラム) (13.3 / original p.686-687)

```
// [Title]No.2 positioning data setting program
// <Positioning identifier>
//   Operation pattern: positioning complete
//   Control method: Speed-position switching control (forward run)
//   Acceleration time No.: 1, deceleration time No.: 2
(2261) LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1  R:Synchronization flag(Direct)
       MOV   K0 M_FX5SSC_SetPositioningData_01A_2.pb_uOpePattern          ; Da.1: Operation pattern
       MOV   H6 M_FX5SSC_SetPositioningData_01A_2.pb_uCtrlSys             ; Da.2: Control system
       MOV   K1 M_FX5SSC_SetPositioningData_01A_2.pb_uAccTimeNo             ; Da.3: Acceleration time No.
       MOV   K2 M_FX5SSC_SetPositioningData_01A_2.pb_uDecTimeNo             ; Da.4: Deceleration time No.
       MOV   K0 M_FX5SSC_SetPositioningData_01A_2.pb_uMcode            ; Da.10: M code
       MOV   K300 M_FX5SSC_SetPositioningData_01A_2.pb_uDwellTime           ; Da.9: Dwell time
       DMOV  K18000 M_FX5SSC_SetPositioningData_01A_2.pb_udCmdSpd             ; Da.8: Command speed
       MPS
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   ; X51  Speed-position switching (ABS) setting command
       DMOV  K3600000 M_FX5SSC_SetPositioningData_01A_2.pb_udCmdSpd             ; Da.8: Command speed
       MRD
       DMOV  K25000 M_FX5SSC_SetPositioningData_01A_2.pb_dPositAdr            ; Da.6: Positioning address
       MRD
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   ; X51  Speed-position switching (ABS) setting command
       DMOV  K9000000 M_FX5SSC_SetPositioningData_01A_2.pb_dPositAdr            ; Da.6: Positioning address
       MPP
       DMOV  K0 M_FX5SSC_SetPositioningData_01A_2.pb_dArcAdr                ; Da.7: Arc address
       MOV   K0 M_FX5SSC_SetPositioningData_01A_2.pb_uInterpolationAxisNo1  ; Da.20: Axis to be interpolated No.1
       MOV   K0 M_FX5SSC_SetPositioningData_01A_2.pb_uInterpolationAxisNo2  ; Da.21: Axis to be interpolated No.2
       MOV   K0 M_FX5SSC_SetPositioningData_01A_2.pb_uInterpolationAxisNo3  ; Da.22: Axis to be interpolated No.3
       SET   bSetPositioningData2_bEN                   ; No.2 Execution command
(2599) LD    bSetPositioningData2_bEN                   ; No.2 Execution command
       FB    M_FX5SSC_SetPositioningData_01A_2
       // FB title: M_FX5SSC_SetPositioningData_01A_2 (M+FX5SSC_SetPos...) Positioning data setting FB
       // in  B: i_bEN         <- bSetPositioningData2_bEN (normally open contact above)   ; Execution command
       // in  DUT: i_stModule  <- FX5SSC_1   ; Module label / Module label
       // in  UW: i_uAxis      <- K1         ; Target axis
       // in  UW: i_uDataNo    <- K2        ; Data No.
       // out o_bENO :B        -> (no connection shown)   ; Execution status
       // out o_bOK :B         -> (no connection shown)   ; Normal completion
       // out o_bErr :B        -> (no connection shown)   ; Error completion
       // out o_uErrId :UW     -> (no connection shown)   ; Error code
       // public variables shown in the FB: pb_uOpePatt..., pb_uCtrlSys, pb_uAccTim..., pb_uDecTim..., pb_uMcode, pb_uDwellTi..., pb_udCmdS..., pb_dPositAdr, pb_dArcAdr, pb_uInterpol..., pb_uInterpol..., pb_uInterpol...
```

- Step (2261) (p.686-687): bSynchronizationFlag_D is a rising edge (↑) contact. G_bInputG_bInputSpeedPositionSwitchingAbsSetReq (X51) is a normally open contact placed in series only before the second DMOV to pb_udCmdSpd (K3600000) and the second DMOV to pb_dPositAdr (K9000000); all other outputs are driven by the synchronization flag condition only. The original is a ladder diagram; MPS/MRD/MPP are added by this transcription.
- Step (2599) (p.687): the FB output pins (o_bENO, o_bOK, o_bErr, o_uErrId) only have lines extending to the right; no connection destination is shown. The FB instance name is shown as "M_FX5SSC_SetPos" / "itioningData_01A_2" and the type name as "(M+FX5SS" / "C_SetPos..." (truncated display).

##### No.3 positioning data setting program (No.3位置決めデータ設定プログラム) (13.3 / original p.688-689)

```
// [Title]No.3 positioning data setting program
// <Positioning identifier>
//   Operation pattern: positioning complete
//   Control method: Position-speed switching control (forward run)
//   Acceleration time No.: 1, deceleration time No.: 2
(2910) LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1  R:Synchronization flag(Direct)
       MOV   K0 M_FX5SSC_SetPositioningData_01A_3.pb_uOpePattern          ; Da.1: Operation pattern
       MOV   H8 M_FX5SSC_SetPositioningData_01A_3.pb_uCtrlSys             ; Da.2: Control system
       MOV   K1 M_FX5SSC_SetPositioningData_01A_3.pb_uAccTimeNo             ; Da.3: Acceleration time No.
       MOV   K2 M_FX5SSC_SetPositioningData_01A_3.pb_uDecTimeNo             ; Da.4: Deceleration time No.
       MOV   K0 M_FX5SSC_SetPositioningData_01A_3.pb_uMcode            ; Da.10: M code
       MOV   K300 M_FX5SSC_SetPositioningData_01A_3.pb_uDwellTime           ; Da.9: Dwell time
       DMOV  K18000 M_FX5SSC_SetPositioningData_01A_3.pb_udCmdSpd             ; Da.8: Command speed
       MPS
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   ; X51  Speed-position switching (ABS) setting command
       DMOV  K3600000 M_FX5SSC_SetPositioningData_01A_3.pb_udCmdSpd             ; Da.8: Command speed
       MRD
       DMOV  K200000 M_FX5SSC_SetPositioningData_01A_3.pb_dPositAdr            ; Da.6: Positioning address
       MRD
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   ; X51  Speed-position switching (ABS) setting command
       DMOV  K72000000 M_FX5SSC_SetPositioningData_01A_3.pb_dPositAdr            ; Da.6: Positioning address
       MPP
       DMOV  K0 M_FX5SSC_SetPositioningData_01A_3.pb_dArcAdr                ; Da.7: Arc address
       MOV   K0 M_FX5SSC_SetPositioningData_01A_3.pb_uInterpolationAxisNo1  ; Da.20: Axis to be interpolated No.1
       MOV   K0 M_FX5SSC_SetPositioningData_01A_3.pb_uInterpolationAxisNo2  ; Da.21: Axis to be interpolated No.2
       MOV   K0 M_FX5SSC_SetPositioningData_01A_3.pb_uInterpolationAxisNo3  ; Da.22: Axis to be interpolated No.3
       SET   bSetPositioningData3_bEN                   ; No.3 Execution command
(3248) LD    bSetPositioningData3_bEN                   ; No.3 Execution command
       FB    M_FX5SSC_SetPositioningData_01A_3
       // FB title: M_FX5SSC_SetPositioningData_01A_3 (M+FX5SSC_SetPos...) Positioning data setting FB
       // in  B: i_bEN         <- bSetPositioningData3_bEN (normally open contact above)   ; Execution command
       // in  DUT: i_stModule  <- FX5SSC_1   ; Module label / Module label
       // in  UW: i_uAxis      <- K1         ; Target axis
       // in  UW: i_uDataNo    <- K3        ; Data No.
       // out o_bENO :B        -> (no connection shown)   ; Execution status
       // out o_bOK :B         -> (no connection shown)   ; Normal completion
       // out o_bErr :B        -> (no connection shown)   ; Error completion
       // out o_uErrId :UW     -> (no connection shown)   ; Error code
       // public variables shown in the FB: pb_uOpePatt..., pb_uCtrlSys, pb_uAccTim..., pb_uDecTim..., pb_uMcode, pb_uDwellTi..., pb_udCmdS..., pb_dPositAdr, pb_dArcAdr, pb_uInterpol..., pb_uInterpol..., pb_uInterpol...
```

- Step (2910) (p.688-689): bSynchronizationFlag_D is a rising edge (↑) contact. G_bInputG_bInputSpeedPositionSwitchingAbsSetReq (X51) is a normally open contact placed in series only before the second DMOV to pb_udCmdSpd (K3600000) and the second DMOV to pb_dPositAdr (K72000000); all other outputs are driven by the synchronization flag condition only. The original is a ladder diagram; MPS/MRD/MPP are added by this transcription.
- Step (3248) (p.689): the FB output pins (o_bENO, o_bOK, o_bErr, o_uErrId) only have lines extending to the right; no connection destination is shown. The FB instance name is shown as "M_FX5SSC_SetPos" / "itioningData_01A_3" and the type name as "(M+FX5SS" / "C_SetPos..." (truncated display).

##### No.4 positioning data setting program (No.4位置決めデータ設定プログラム) (13.3 / original p.690-691)

```
// [Title]No.4 positioning data setting program
// <Positioning identifier>
//   Operation pattern: positioning complete
//   Control method: 1 axis linear control (INC)
//   Acceleration time No.: 1, deceleration time No.: 2
(3559) LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1  R:Synchronization flag(Direct)
       MOV   K0 M_FX5SSC_SetPositioningData_01A_4.pb_uOpePattern          ; Da.1: Operation pattern
       MOV   H2 M_FX5SSC_SetPositioningData_01A_4.pb_uCtrlSys             ; Da.2: Control system
       MOV   K1 M_FX5SSC_SetPositioningData_01A_4.pb_uAccTimeNo             ; Da.3: Acceleration time No.
       MOV   K2 M_FX5SSC_SetPositioningData_01A_4.pb_uDecTimeNo             ; Da.4: Deceleration time No.
       MOV   K0 M_FX5SSC_SetPositioningData_01A_4.pb_uMcode            ; Da.10: M code
       MOV   K300 M_FX5SSC_SetPositioningData_01A_4.pb_uDwellTime           ; Da.9: Dwell time
       DMOV  K9000 M_FX5SSC_SetPositioningData_01A_4.pb_udCmdSpd             ; Da.8: Command speed
       MPS
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   ; X51  Speed-position switching (ABS) setting command
       DMOV  K1800000 M_FX5SSC_SetPositioningData_01A_4.pb_udCmdSpd             ; Da.8: Command speed
       MRD
       DMOV  K50000 M_FX5SSC_SetPositioningData_01A_4.pb_dPositAdr            ; Da.6: Positioning address
       MRD
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   ; X51  Speed-position switching (ABS) setting command
       DMOV  K18000000 M_FX5SSC_SetPositioningData_01A_4.pb_dPositAdr            ; Da.6: Positioning address
       MPP
       DMOV  K0 M_FX5SSC_SetPositioningData_01A_4.pb_dArcAdr                ; Da.7: Arc address
       MOV   K0 M_FX5SSC_SetPositioningData_01A_4.pb_uInterpolationAxisNo1  ; Da.20: Axis to be interpolated No.1
       MOV   K0 M_FX5SSC_SetPositioningData_01A_4.pb_uInterpolationAxisNo2  ; Da.21: Axis to be interpolated No.2
       MOV   K0 M_FX5SSC_SetPositioningData_01A_4.pb_uInterpolationAxisNo3  ; Da.22: Axis to be interpolated No.3
       SET   bSetPositioningData4_bEN                   ; No.4 Execution command
(3877) LD    bSetPositioningData4_bEN                   ; No.4 Execution command
       FB    M_FX5SSC_SetPositioningData_01A_4
       // FB title: M_FX5SSC_SetPositioningData_01A_4 (M+FX5SSC_SetPos...) Positioning data setting FB
       // in  B: i_bEN         <- bSetPositioningData4_bEN (normally open contact above)   ; Execution command
       // in  DUT: i_stModule  <- FX5SSC_1   ; Module label / Module label
       // in  UW: i_uAxis      <- K1         ; Target axis
       // in  UW: i_uDataNo    <- K4        ; Data No.
       // out o_bENO :B        -> (no connection shown)   ; Execution status
       // out o_bOK :B         -> (no connection shown)   ; Normal completion
       // out o_bErr :B        -> (no connection shown)   ; Error completion
       // out o_uErrId :UW     -> (no connection shown)   ; Error code
       // public variables shown in the FB: pb_uOpePatt..., pb_uCtrlSys, pb_uAccTim..., pb_uDecTim..., pb_uMcode, pb_uDwellTi..., pb_udCmdS..., pb_dPositAdr, pb_dArcAdr, pb_uInterpol..., pb_uInterpol..., pb_uInterpol...
```

- Step (3559) (p.690-691): bSynchronizationFlag_D is a rising edge (↑) contact. G_bInputG_bInputSpeedPositionSwitchingAbsSetReq (X51) is a normally open contact placed in series only before the second DMOV to pb_udCmdSpd (K1800000) and the second DMOV to pb_dPositAdr (K18000000); all other outputs are driven by the synchronization flag condition only. The original is a ladder diagram; MPS/MRD/MPP are added by this transcription.
- Step (3877) (p.691): the FB output pins (o_bENO, o_bOK, o_bErr, o_uErrId) only have lines extending to the right; no connection destination is shown. The FB instance name is shown as "M_FX5SSC_SetPos" / "itioningData_01A_4" and the type name as "(M+FX5SS" / "C_SetPos..." (truncated display).

##### No.5 positioning data setting program (No.5位置決めデータ設定プログラム) (13.3 / original p.692-693)

```
// [Title]No.5 positioning data setting program
// <Positioning identifier>
//   Operation pattern: continuous positioning control
//   Control method: 1 axis linear control (INC)
//   Acceleration time No.: 1, deceleration time No.: 2
(4188) LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1  R:Synchronization flag(Direct)
       MOV   K1 M_FX5SSC_SetPositioningData_01A_5.pb_uOpePattern          ; Da.1: Operation pattern
       MOV   H2 M_FX5SSC_SetPositioningData_01A_5.pb_uCtrlSys             ; Da.2: Control system
       MOV   K1 M_FX5SSC_SetPositioningData_01A_5.pb_uAccTimeNo             ; Da.3: Acceleration time No.
       MOV   K2 M_FX5SSC_SetPositioningData_01A_5.pb_uDecTimeNo             ; Da.4: Deceleration time No.
       MOV   K0 M_FX5SSC_SetPositioningData_01A_5.pb_uMcode            ; Da.10: M code
       MOV   K300 M_FX5SSC_SetPositioningData_01A_5.pb_uDwellTime           ; Da.9: Dwell time
       DMOV  K36000 M_FX5SSC_SetPositioningData_01A_5.pb_udCmdSpd             ; Da.8: Command speed
       MPS
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   ; X51  Speed-position switching (ABS) setting command
       DMOV  K6000000 M_FX5SSC_SetPositioningData_01A_5.pb_udCmdSpd             ; Da.8: Command speed
       MRD
       DMOV  K100000 M_FX5SSC_SetPositioningData_01A_5.pb_dPositAdr            ; Da.6: Positioning address
       MRD
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   ; X51  Speed-position switching (ABS) setting command
       DMOV  K36000000 M_FX5SSC_SetPositioningData_01A_5.pb_dPositAdr            ; Da.6: Positioning address
       MPP
       DMOV  K0 M_FX5SSC_SetPositioningData_01A_5.pb_dArcAdr                ; Da.7: Arc address
       MOV   K0 M_FX5SSC_SetPositioningData_01A_5.pb_uInterpolationAxisNo1  ; Da.20: Axis to be interpolated No.1
       MOV   K0 M_FX5SSC_SetPositioningData_01A_5.pb_uInterpolationAxisNo2  ; Da.21: Axis to be interpolated No.2
       MOV   K0 M_FX5SSC_SetPositioningData_01A_5.pb_uInterpolationAxisNo3  ; Da.22: Axis to be interpolated No.3
       SET   bSetPositioningData5_bEN                   ; No.5 Execution command
(4517) LD    bSetPositioningData5_bEN                   ; No.5 Execution command
       FB    M_FX5SSC_SetPositioningData_01A_5
       // FB title: M_FX5SSC_SetPositioningData_01A_5 (M+FX5SSC_SetPos...) Positioning data setting FB
       // in  B: i_bEN         <- bSetPositioningData5_bEN (normally open contact above)   ; Execution command
       // in  DUT: i_stModule  <- FX5SSC_1   ; Module label / Module label
       // in  UW: i_uAxis      <- K1         ; Target axis
       // in  UW: i_uDataNo    <- K5        ; Data No.
       // out o_bENO :B        -> (no connection shown)   ; Execution status
       // out o_bOK :B         -> (no connection shown)   ; Normal completion
       // out o_bErr :B        -> (no connection shown)   ; Error completion
       // out o_uErrId :UW     -> (no connection shown)   ; Error code
       // public variables shown in the FB: pb_uOpePatt..., pb_uCtrlSys, pb_uAccTim..., pb_uDecTim..., pb_uMcode, pb_uDwellTi..., pb_udCmdS..., pb_dPositAdr, pb_dArcAdr, pb_uInterpol..., pb_uInterpol..., pb_uInterpol...
```

- Step (4188) (p.692-693): bSynchronizationFlag_D is a rising edge (↑) contact. G_bInputG_bInputSpeedPositionSwitchingAbsSetReq (X51) is a normally open contact placed in series only before the second DMOV to pb_udCmdSpd (K6000000) and the second DMOV to pb_dPositAdr (K36000000); all other outputs are driven by the synchronization flag condition only. The original is a ladder diagram; MPS/MRD/MPP are added by this transcription.
- Step (4517) (p.693): the FB output pins (o_bENO, o_bOK, o_bErr, o_uErrId) only have lines extending to the right; no connection destination is shown. The FB instance name is shown as "M_FX5SSC_SetPos" / "itioningData_01A_5" and the type name as "(M+FX5SS" / "C_SetPos..." (truncated display).

##### No.6 positioning data setting program (No.6位置決めデータ設定プログラム) (13.3 / original p.694-695)

```
// [Title]No.6 positioning data setting program
// <Positioning identifier>
//   Operation pattern: positioning complete
//   Control method: 1 axis linear control (INC)
//   Acceleration time No.: 1, deceleration time No.: 2
(4828) LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1  R:Synchronization flag(Direct)
       MOV   K0 M_FX5SSC_SetPositioningData_01A_6.pb_uOpePattern          ; Da.1: Operation pattern
       MOV   H2 M_FX5SSC_SetPositioningData_01A_6.pb_uCtrlSys             ; Da.2: Control system
       MOV   K1 M_FX5SSC_SetPositioningData_01A_6.pb_uAccTimeNo             ; Da.3: Acceleration time No.
       MOV   K2 M_FX5SSC_SetPositioningData_01A_6.pb_uDecTimeNo             ; Da.4: Deceleration time No.
       MOV   K0 M_FX5SSC_SetPositioningData_01A_6.pb_uMcode            ; Da.10: M code
       MOV   K300 M_FX5SSC_SetPositioningData_01A_6.pb_uDwellTime           ; Da.9: Dwell time
       DMOV  K9000 M_FX5SSC_SetPositioningData_01A_6.pb_udCmdSpd             ; Da.8: Command speed
       MPS
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   ; X51  Speed-position switching (ABS) setting command
       DMOV  K1800000 M_FX5SSC_SetPositioningData_01A_6.pb_udCmdSpd             ; Da.8: Command speed
       MRD
       DMOV  K50000 M_FX5SSC_SetPositioningData_01A_6.pb_dPositAdr            ; Da.6: Positioning address
       MRD
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   ; X51  Speed-position switching (ABS) setting command
       DMOV  K18000000 M_FX5SSC_SetPositioningData_01A_6.pb_dPositAdr            ; Da.6: Positioning address
       MPP
       DMOV  K0 M_FX5SSC_SetPositioningData_01A_6.pb_dArcAdr                ; Da.7: Arc address
       MOV   K0 M_FX5SSC_SetPositioningData_01A_6.pb_uInterpolationAxisNo1  ; Da.20: Axis to be interpolated No.1
       MOV   K0 M_FX5SSC_SetPositioningData_01A_6.pb_uInterpolationAxisNo2  ; Da.21: Axis to be interpolated No.2
       MOV   K0 M_FX5SSC_SetPositioningData_01A_6.pb_uInterpolationAxisNo3  ; Da.22: Axis to be interpolated No.3
       SET   bSetPositioningData6_bEN                   ; No.6 Execution command
(5146) LD    bSetPositioningData6_bEN                   ; No.6 Execution command
       FB    M_FX5SSC_SetPositioningData_01A_6
       // FB title: M_FX5SSC_SetPositioningData_01A_6 (M+FX5SSC_SetPos...) Positioning data setting FB
       // in  B: i_bEN         <- bSetPositioningData6_bEN (normally open contact above)   ; Execution command
       // in  DUT: i_stModule  <- FX5SSC_1   ; Module label / Module label
       // in  UW: i_uAxis      <- K1         ; Target axis
       // in  UW: i_uDataNo    <- K6        ; Data No.
       // out o_bENO :B        -> (no connection shown)   ; Execution status
       // out o_bOK :B         -> (no connection shown)   ; Normal completion
       // out o_bErr :B        -> (no connection shown)   ; Error completion
       // out o_uErrId :UW     -> (no connection shown)   ; Error code
       // public variables shown in the FB: pb_uOpePatt..., pb_uCtrlSys, pb_uAccTim..., pb_uDecTim..., pb_uMcode, pb_uDwellTi..., pb_udCmdS..., pb_dPositAdr, pb_dArcAdr, pb_uInterpol..., pb_uInterpol..., pb_uInterpol...
```

- Step (4828) (p.694-695): bSynchronizationFlag_D is a rising edge (↑) contact. G_bInputG_bInputSpeedPositionSwitchingAbsSetReq (X51) is a normally open contact placed in series only before the second DMOV to pb_udCmdSpd (K1800000) and the second DMOV to pb_dPositAdr (K18000000); all other outputs are driven by the synchronization flag condition only. The original is a ladder diagram; MPS/MRD/MPP are added by this transcription.
- Step (5146) (p.695): the FB output pins (o_bENO, o_bOK, o_bErr, o_uErrId) only have lines extending to the right; no connection destination is shown. The FB instance name is shown as "M_FX5SSC_SetPos" / "itioningData_01A_6" and the type name as "(M+FX5SS" / "C_SetPos..." (truncated display).

##### No.10 positioning data setting program (No.10位置決めデータ設定プログラム) (13.3 / original p.696-697)

```
// [Title]No.10 positioning data setting program
// <Positioning identifier>
//   Operation pattern: continuous positioning control
//   Control method: 1 axis linear control (INC)
//   Acceleration time No.: 1, deceleration time No.: 2
(5457) LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1  R:Synchronization flag(Direct)
       MOV   K1 M_FX5SSC_SetPositioningData_01A_10.pb_uOpePattern          ; Da.1: Operation pattern
       MOV   H2 M_FX5SSC_SetPositioningData_01A_10.pb_uCtrlSys             ; Da.2: Control system
       MOV   K1 M_FX5SSC_SetPositioningData_01A_10.pb_uAccTimeNo             ; Da.3: Acceleration time No.
       MOV   K2 M_FX5SSC_SetPositioningData_01A_10.pb_uDecTimeNo             ; Da.4: Deceleration time No.
       MOV   K0 M_FX5SSC_SetPositioningData_01A_10.pb_uMcode            ; Da.10: M code
       MOV   K300 M_FX5SSC_SetPositioningData_01A_10.pb_uDwellTime           ; Da.9: Dwell time
       DMOV  K9000 M_FX5SSC_SetPositioningData_01A_10.pb_udCmdSpd             ; Da.8: Command speed
       MPS
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   ; X51  Speed-position switching (ABS) setting command
       DMOV  K3600000 M_FX5SSC_SetPositioningData_01A_10.pb_udCmdSpd             ; Da.8: Command speed
       MRD
       DMOV  K50000 M_FX5SSC_SetPositioningData_01A_10.pb_dPositAdr            ; Da.6: Positioning address
       MRD
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   ; X51  Speed-position switching (ABS) setting command
       DMOV  K36000000 M_FX5SSC_SetPositioningData_01A_10.pb_dPositAdr            ; Da.6: Positioning address
       MPP
       DMOV  K0 M_FX5SSC_SetPositioningData_01A_10.pb_dArcAdr                ; Da.7: Arc address
       MOV   K0 M_FX5SSC_SetPositioningData_01A_10.pb_uInterpolationAxisNo1  ; Da.20: Axis to be interpolated No.1
       MOV   K0 M_FX5SSC_SetPositioningData_01A_10.pb_uInterpolationAxisNo2  ; Da.21: Axis to be interpolated No.2
       MOV   K0 M_FX5SSC_SetPositioningData_01A_10.pb_uInterpolationAxisNo3  ; Da.22: Axis to be interpolated No.3
       SET   bSetPositioningData10_bEN                   ; No.10 Execution command
(5787) LD    bSetPositioningData10_bEN                   ; No.10 Execution command
       FB    M_FX5SSC_SetPositioningData_01A_10
       // FB title: M_FX5SSC_SetPositioningData_01A_10 (M+FX5SSC_SetPos...) Positioning data setting FB
       // in  B: i_bEN         <- bSetPositioningData10_bEN (normally open contact above)   ; Execution command
       // in  DUT: i_stModule  <- FX5SSC_1   ; Module label / Module label
       // in  UW: i_uAxis      <- K1         ; Target axis
       // in  UW: i_uDataNo    <- K10        ; Data No.
       // out o_bENO :B        -> (no connection shown)   ; Execution status
       // out o_bOK :B         -> (no connection shown)   ; Normal completion
       // out o_bErr :B        -> (no connection shown)   ; Error completion
       // out o_uErrId :UW     -> (no connection shown)   ; Error code
       // public variables shown in the FB: pb_uOpePatt..., pb_uCtrlSys, pb_uAccTim..., pb_uDecTim..., pb_uMcode, pb_uDwellTi..., pb_udCmdS..., pb_dPositAdr, pb_dArcAdr, pb_uInterpol..., pb_uInterpol..., pb_uInterpol...
```

- Step (5457) (p.696-697): bSynchronizationFlag_D is a rising edge (↑) contact. G_bInputG_bInputSpeedPositionSwitchingAbsSetReq (X51) is a normally open contact placed in series only before the second DMOV to pb_udCmdSpd (K3600000) and the second DMOV to pb_dPositAdr (K36000000); all other outputs are driven by the synchronization flag condition only. The original is a ladder diagram; MPS/MRD/MPP are added by this transcription.
- Step (5787) (p.697): the FB output pins (o_bENO, o_bOK, o_bErr, o_uErrId) only have lines extending to the right; no connection destination is shown. The FB instance name is shown as "M_FX5SSC_SetPos" / "itioningData_01A_..." and the type name as "(M+FX5SS" / "C_SetPos..." (truncated display).
- The FB instance name in the FB header is truncated to "...itioningData_01A_..." in the display; the instance is M_FX5SSC_SetPositioningData_01A_10, as used in the MOV destinations of step (5457). The contact label is printed on two lines ("bSetPositioningData10_b" / "EN").

##### No.11 positioning data setting program (No.11位置決めデータ設定プログラム) (13.3 / original p.698-699)

```
// [Title]No.11 positioning data setting program
// <Positioning identifier>
//   Operation pattern: positioning complete
//   Control method: 1 axis linear control (INC)
//   Acceleration time No.: 1, deceleration time No.: 2
(6098) LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1  R:Synchronization flag(Direct)
       MOV   K0 M_FX5SSC_SetPositioningData_01A_11.pb_uOpePattern          ; Da.1: Operation pattern
       MOV   H2 M_FX5SSC_SetPositioningData_01A_11.pb_uCtrlSys             ; Da.2: Control system
       MOV   K1 M_FX5SSC_SetPositioningData_01A_11.pb_uAccTimeNo             ; Da.3: Acceleration time No.
       MOV   K2 M_FX5SSC_SetPositioningData_01A_11.pb_uDecTimeNo             ; Da.4: Deceleration time No.
       MOV   K0 M_FX5SSC_SetPositioningData_01A_11.pb_uMcode            ; Da.10: M code
       MOV   K300 M_FX5SSC_SetPositioningData_01A_11.pb_uDwellTime           ; Da.9: Dwell time
       DMOV  K18000 M_FX5SSC_SetPositioningData_01A_11.pb_udCmdSpd             ; Da.8: Command speed
       MPS
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   ; X51  Speed-position switching (ABS) setting command
       DMOV  K3600000 M_FX5SSC_SetPositioningData_01A_11.pb_udCmdSpd             ; Da.8: Command speed
       MRD
       DMOV  K-100000 M_FX5SSC_SetPositioningData_01A_11.pb_dPositAdr            ; Da.6: Positioning address
       MRD
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq   ; X51  Speed-position switching (ABS) setting command
       DMOV  K-36000000 M_FX5SSC_SetPositioningData_01A_11.pb_dPositAdr            ; Da.6: Positioning address
       MPP
       DMOV  K0 M_FX5SSC_SetPositioningData_01A_11.pb_dArcAdr                ; Da.7: Arc address
       MOV   K0 M_FX5SSC_SetPositioningData_01A_11.pb_uInterpolationAxisNo1  ; Da.20: Axis to be interpolated No.1
       MOV   K0 M_FX5SSC_SetPositioningData_01A_11.pb_uInterpolationAxisNo2  ; Da.21: Axis to be interpolated No.2
       MOV   K0 M_FX5SSC_SetPositioningData_01A_11.pb_uInterpolationAxisNo3  ; Da.22: Axis to be interpolated No.3
       SET   bSetPositioningData11_bEN                   ; No.11 Execution command
(6419) LD    bSetPositioningData11_bEN                   ; No.11 Execution command
       FB    M_FX5SSC_SetPositioningData_01A_11
       // FB title: M_FX5SSC_SetPositioningData_01A_11 (M+FX5SSC_SetPos...) Positioning data setting FB
       // in  B: i_bEN         <- bSetPositioningData11_bEN (normally open contact above)   ; Execution command
       // in  DUT: i_stModule  <- FX5SSC_1   ; Module label / Module label
       // in  UW: i_uAxis      <- K1         ; Target axis
       // in  UW: i_uDataNo    <- K11        ; Data No.
       // out o_bENO :B        -> (no connection shown)   ; Execution status
       // out o_bOK :B         -> (no connection shown)   ; Normal completion
       // out o_bErr :B        -> (no connection shown)   ; Error completion
       // out o_uErrId :UW     -> (no connection shown)   ; Error code
       // public variables shown in the FB: pb_uOpePatt..., pb_uCtrlSys, pb_uAccTim..., pb_uDecTim..., pb_uMcode, pb_uDwellTi..., pb_udCmdS..., pb_dPositAdr, pb_dArcAdr, pb_uInterpol..., pb_uInterpol..., pb_uInterpol...
```

- Step (6098) (p.698-699): bSynchronizationFlag_D is a rising edge (↑) contact. G_bInputG_bInputSpeedPositionSwitchingAbsSetReq (X51) is a normally open contact placed in series only before the second DMOV to pb_udCmdSpd (K3600000) and the second DMOV to pb_dPositAdr (K-36000000); all other outputs are driven by the synchronization flag condition only. The original is a ladder diagram; MPS/MRD/MPP are added by this transcription.
- Step (6419) (p.699): the FB output pins (o_bENO, o_bOK, o_bErr, o_uErrId) only have lines extending to the right; no connection destination is shown. The FB instance name is shown as "M_FX5SSC_SetPos" / "itioningData_01A_..." and the type name as "(M+FX5SS" / "C_SetPos..." (truncated display).
- The FB instance name in the FB header is truncated to "...itioningData_01A_..." in the display; the instance is M_FX5SSC_SetPositioningData_01A_11, as used in the MOV destinations of step (6098). The contact label is printed on two lines ("bSetPositioningData11_b" / "EN").

##### No.15 positioning data setting program (No.15位置決めデータ設定プログラム) (13.3 / original p.700-701)

```
// [Title]No.15 positioning data setting program
// <Positioning identifier>
//   Operation pattern: positioning complete
//   Control method: 1 axis linear control (INC)
// Acceleration time No.: 1, deceleration time No.: 2
(6730) LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D                       ; U1\G31500.1  R:Synchronization flag (Direct)
       MOV   K0 M_FX5SSC_SetPositioningData_01A_15.pb_uOpePattern               ; Da.1: Operation pattern
       MOV   H2 M_FX5SSC_SetPositioningData_01A_15.pb_uCtrlSys                  ; Da.2: Control system
       MOV   K1 M_FX5SSC_SetPositioningData_01A_15.pb_uAccTimeNo                ; Da.3: Acceleration time No.
       MOV   K2 M_FX5SSC_SetPositioningData_01A_15.pb_uDecTimeNo                ; Da.4: Deceleration time No.
       MOV   K0 M_FX5SSC_SetPositioningData_01A_15.pb_uMcode                    ; Da.10: M code
       MOV   K0 M_FX5SSC_SetPositioningData_01A_15.pb_uDwellTime                ; Da.9: Dwell time
       DMOV  K9000 M_FX5SSC_SetPositioningData_01A_15.pb_udCmdSpd               ; Da.8: Command speed
       MPS
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq                    ; X51  Speed-position switching (ABS) setting command
       DMOV  K1800000 M_FX5SSC_SetPositioningData_01A_15.pb_udCmdSpd            ; Da.8: Command speed
       MPP
       DMOV  K50000 M_FX5SSC_SetPositioningData_01A_15.pb_dPositAdr             ; Da.6: Positioning address
       MPS
       AND   G_bInputG_bInputSpeedPositionSwitchingAbsSetReq                    ; X51  Speed-position switching (ABS) setting command
       DMOV  K18000000 M_FX5SSC_SetPositioningData_01A_15.pb_dPositAdr          ; Da.6: Positioning address
       MPP
       DMOV  K0 M_FX5SSC_SetPositioningData_01A_15.pb_dArcAdr                   ; Da.7: Arc address
       MOV   K0 M_FX5SSC_SetPositioningData_01A_15.pb_uInterpolationAxisNo1     ; Da.20: Axis to be interpolated No.1
       MOV   K0 M_FX5SSC_SetPositioningData_01A_15.pb_uInterpolationAxisNo2     ; Da.21: Axis to be interpolated No.2
       MOV   K0 M_FX5SSC_SetPositioningData_01A_15.pb_uInterpolationAxisNo3     ; Da.22: Axis to be interpolated No.3   (original p.701)
       SET   bSetPositioningData15_bEN                                          ; No.15 Execution command
(7047) LD    bSetPositioningData15_bEN                                          ; No.15 Execution command
       FB    M_FX5SSC_SetPositioningData_01A_15
       // FB title: M_FX5SSC_SetPositioningData_01A_15 (M+FX5SSC_SetPos...) Positioning data setting FB
       // in  B: i_bEN         <- bSetPositioningData15_bEN (normally open contact above)   ; Execution command
       // in  DUT: i_stModule  <- FX5SSC_1        ; Module label / Module label
       // in  UW: i_uAxis      <- K1              ; Target axis
       // in  UW: i_uDataNo    <- K15             ; Data No.
       // out o_bENO :B        -> (line only, no label connected)   ; Execution status
       // out o_bOK :B         -> (line only, no label connected)   ; Normal completion
       // out o_bErr :B        -> (line only, no label connected)   ; Error completion
       // out o_uErrId :UW     -> (line only, no label connected)   ; Error code
       // public variables shown in the FB: pb_uOpePatt..., pb_uCtrlSys, pb_uAccTim..., pb_uDecTim..., pb_uMcode, pb_uDwellTi..., pb_udCmdS..., pb_dPositAdr, pb_dArcAdr, pb_uInterpol..., pb_uInterpol..., pb_uInterpol...
```

- Contact type (read from figure): FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D at (6730) is a rising edge (↑) contact. G_bInputG_bInputSpeedPositionSwitchingAbsSetReq (X51) is a normally open contact, in series only before the second DMOV of Da.8 Command speed (K1800000) and the second DMOV of Da.6 Positioning address (K18000000); the branch point is right after the synchronization flag contact. All other outputs are conditioned only by the synchronization flag. MPS/MPP are added by this transcription (the original is a ladder diagram only).
- The rung at (6730) continues from p.700 to p.701 (Da.22 and SET are on p.701). The FB rung (7047) is on p.701.
- The step numbers are shown folded in the ladder as "(6730" / ")" and "(7047" / ")".
- The FB instance name and type name are truncated in the ladder display ("M_FX5SSC_SetPos itioningData_01A_..." / "(M+FX5SSC_SetPos..."), as printed. The i_stModule and i_uDataNo pin names are shown folded ("i_stModu le", "i_uDataN o").

#### Block start data setting program (ブロック始動データ設定プログラム) (13.3 / original p.702)

This program is not required when the data is set by "Block Start Data" using an engineering tool.
Set the local labels as follows.

| No. | Label Name | Data Type | Class |
|---|---|---|---|
| 1 | uBlockData | Word [Unsigned]/Bit String [16-bit](0..4) | VAR |
| 2 | uBlockInstData | Word [Unsigned]/Bit String [16-bit](0..4) | VAR |
*The original is a screen capture of the GX Works3 local label setting screen. The "..." button column and the drop-down marks of the "Class" column are not transcribed.

```
// [Title]Block start data setting program
//   Block start order: Positioning No1→No2→No5→No10→No15
(7358) LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1  R:Synchronization flag (Direct)
       MOVP  H8001 uBlockData[0]                               ; Block start data (shape, start data No.)
       MOVP  H8002 uBlockData[1]                               ; Block start data (shape, start data No.)
       MOVP  H8005 uBlockData[2]                               ; Block start data (shape, start data No.)
       MOVP  H800A uBlockData[3]                               ; Block start data (shape, start data No.)
       MOVP  H0F uBlockData[4]                                 ; Block start data (shape, start data No.)
       TOP   H1 K22000 uBlockData[0] K5                        ; uBlockData[0]: Block start data (shape, start data No.)
(7500) LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1  R:Synchronization flag (Direct)
       MOVP  H0 uBlockInstData[0]                              ; Block start data (special start instruction)
       MOVP  H0 uBlockInstData[1]                              ; Block start data (special start instruction)
       MOVP  H0 uBlockInstData[2]                              ; Block start data (special start instruction)
       MOVP  H0 uBlockInstData[3]                              ; Block start data (special start instruction)
       MOVP  H0 uBlockInstData[4]                              ; Block start data (special start instruction)
       TOP   H1 K22050 uBlockInstData[0] K5                    ; uBlockInstData[0]: Block start data (special start instruction)
```

- Contact type (read from figure): bSynchronizationFlag_D at (7358) and (7500) are rising edge (↑) contacts.
- The first operand of both TOP instructions is shown as "H1" in the ladder.

#### Home position return request OFF program (原点復帰要求OFFプログラム) (13.3 / original p.703)

This program is not required when "1: Positioning control is executed." is set in "[Pr.55] Operation setting for incompletion of home position return" by "Home Position Return Detailed Parameters" using an engineering tool.
Set the local labels as follows.

| No. | Label Name | Data Type | Class |
|---|---|---|---|
| 1 | bOPRReqFlagOffReq_P | Bit | VAR |
| 2 | bOPRReqFlagOffReq_H | Bit | VAR |
| 3 | bOPRReqFlagOffReq | Bit | VAR |
*The original is a screen capture of the GX Works3 local label setting screen. The "..." button column and the drop-down marks of the "Class" column are not transcribed.

```
// [Title]Home position return request OFF program
//   ■Start condition X2 (home position return request OFF signal)
(7530) LD    G_bInputOPRReqFlagOffReq                                   ; X2  Home position return request OFF command
       PLS   bOPRReqFlagOffReq_P                                        ; Home position return request OFF command pulse
(7661) LD    bOPRReqFlagOffReq_P                                        ; Home position return request OFF command pulse
       ANI   FX5SSC_1.stnAxCtrl2_D[0].uPositioningStart_D.0             ; U1\G30104.0  RW:Positioning start(Direct)
       ANI   FX5SSC_1.stnAxMntr_D[0].uStatus_D.E                        ; U1\G2417.E  R:Status (Direct)
       SET   bOPRReqFlagOffReq_H                                        ; Home position return request OFF command storage
(7671) LD    bOPRReqFlagOffReq_H                                        ; Home position return request OFF command storage
       MPS
       AND   FX5SSC_1.stnAxMntr_D[0].uStatus_D.3                        ; U1\G2417.3  R:Status(Direct)
       SET   bOPRReqFlagOffReq                                          ; Home position return request OFF command
       MPP
       RST   bOPRReqFlagOffReq_H                                        ; Home position return request OFF command storage
(7682) LD    bOPRReqFlagOffReq                                          ; Home position return request OFF command
       MOVP  K1 FX5SSC_1.stnAxCtrl1_D[0].uClearHomingRequestFlag_D      ; U1\G4321  RW:Home position return request flag OFF request (Direct)
       AND=_U K0 FX5SSC_1.stnAxCtrl1_D[0].uClearHomingRequestFlag_D     ; U1\G4321  RW:Home position return request flag...
       RST   bOPRReqFlagOffReq                                          ; Home position return request OFF command
```

- Contact type (read from figure): X2 at (7530) is a normally open contact. FX5SSC_1.stnAxCtrl2_D[0].uPositioningStart_D.0 (U1\G30104.0) and FX5SSC_1.stnAxMntr_D[0].uStatus_D.E (U1\G2417.E) at (7661) are normally closed contacts. FX5SSC_1.stnAxMntr_D[0].uStatus_D.3 (U1\G2417.3) at (7671) is a normally open contact.
- (7671): the RST bOPRReqFlagOffReq_H branch comes out right after the bOPRReqFlagOffReq_H contact (before the U1\G2417.3 contact).
- (7682): the =_U comparison (K0 and U1\G4321) branch comes out right after the bOPRReqFlagOffReq contact; RST bOPRReqFlagOffReq is in series with it.
- Labels in the comparison cell and in the (7661) U1\G2417.E cell are truncated in the ladder display ("FX5SSC_1.s tnAxCtrl1_D...", "FX5SSC_1.s tnAxMntr_D...", "RW:Home position return request flag..."), as printed.

#### External command function valid setting program (外部指令機能有効設定プログラム) (13.3 / original p.703)

```
// [Title]External command valid program
//   ■Start condition X3 (external command valid signal)
(7698) LD    G_bInputExternalCommandValidReq                            ; X3  External command valid command
       MOVP  K1 FX5SSC_1.stnAxCtrl1_D[0].uExternalCommandValid_D        ; U1\G4305  RW:External command valid(Direct)
(7810) LD    G_bInputExternalCommandInvalidReq                          ; X4  External command invalid command
       MOVP  K0 FX5SSC_1.stnAxCtrl1_D[0].uExternalCommandValid_D        ; U1\G4305  RW:External command valid(Direct)
```

- Contact type (read from figure): X3 and X4 are normally open contacts.
- The heading is "External command function valid setting program"; the Title line of the ladder is "External command valid program" (as printed).

#### PLC READY signal ON program (シーケンサレディ信号ONプログラム) (13.3 / original p.704)

Set the local labels as follows.

| No. | Label Name | Data Type | Class |
|---|---|---|---|
| 1 | bBasicParamSetComp | Bit | VAR |
| 2 | bDetailedParamSetComp | Bit | VAR |
| 3 | bOPRParamSetComp | Bit | VAR |
*The original is a screen capture of the GX Works3 local label setting screen. The "..." button column and the drop-down marks of the "Class" column are not transcribed.

```
// [Title]PLC READY ON program
(7818) LD    FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D               ; U1\G31500.1  R:Synchronization flag (Direct)
       AND   bBasicParamSetComp                                         ; Basic parameter 1 setting complete
       AND   bDetailedParamSetComp                                      ; Detailed parameter 2 setting complete
       AND   bOPRParamSetComp                                           ; Home position return basic parameter s...
       ANI   G_bInitializeParameterReq                                  ; Parameter initialization command
       ANI   G_bWriteFlashReq                                           ; Flash ROM write command
       OUT   FX5SSC_1.stSysCtrl_D.bPLC_Ready_D                          ; U1\G5950.0  RW:SSCNET cntrol command(Direct)
```

- Contact type (read from figure): bSynchronizationFlag_D, bBasicParamSetComp, bDetailedParamSetComp and bOPRParamSetComp are normally open contacts; G_bInitializeParameterReq and G_bWriteFlashReq are normally closed contacts.
- The comment of bOPRParamSetComp is truncated in the ladder ("Home position return basic parameter s..."). The comment of FX5SSC_1.stSysCtrl_D.bPLC_Ready_D (U1\G5950.0) is shown as "RW:SSCNET cntrol command(Direct)" in the ladder (as printed).

#### All axis servo ON program (全軸サーボONプログラム) (13.3 / original p.704)

```
// [Title]All axis servo ON program
//   * Servo network configuration parameter (IP address) is made valid by writing it to the flash ROM
(7869) LD    G_bAllAxisServoOnReq                                       ; X52  All axis servo ON command
       AND   FX5SSC_1.stSysCtrl_D.bPLC_Ready_D                          ; U1\G5950.0  RW:SSCNET cntrol command(Direct)
       AND   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D               ; U1\G31500.1  R:Synchronization flag (Direct)
       OUT   FX5SSC_1.stSysCtrl_D.bAllAxisServoOn_D                     ; U1\G5951.0  RW:Forced stop input(Direct)
```

- Contact type (read from figure): all three contacts are normally open contacts.
- The comments "RW:SSCNET cntrol command(Direct)" (U1\G5950.0) and "RW:Forced stop input(Direct)" (U1\G5951.0) are as shown in the ladder (as printed).

#### Positioning start No. setting program (位置決め始動番号設定プログラム) (13.3 / original p.705-706)

Set the local labels as follows.

| No. | Label Name | Data Type | Class |
|---|---|---|---|
| 1 | uPositioningStartNo | Word [Signed] | VAR |
| 2 | bFastOPRStartReq | Bit | VAR |
| 3 | bFastOPRStartReq_H | Bit | VAR |
| 4 | bPositioningStartReq | Bit | VAR |
| 5 | udMovementAmount | Double Word [Unsigned]/Bit String [32-bit] | VAR |
| 6 | udSpeed | Double Word [Signed] | VAR |
| 7 | bInputSpeedPositionSwitching | Bit | VAR |
*The original is a screen capture of the GX Works3 local label setting screen. The "..." button column and the drop-down marks of the "Class" column are not transcribed.

##### Machine home position return (機械原点復帰) (13.3 / original p.705)

```
// [Title]Machine home position return
//   ■Start condition X5 (machine home position return command: K9001)→Positioning start program
(0)    LD    G_bInputOPRStartReq                                        ; X5  Machine home position return command
       MOVP  K9001 uPositioningStartNo                                  ; Positioning start No.
```

- Contact type (read from figure): X5 is a normally open contact.

##### Fast home position return (高速原点復帰) (13.3 / original p.705)

```
// [Title]Fast home position return
//   ■Start condition X6 (fast home position return command: K9002)→Positioning start program
(151)  LD    G_bInputFastOPRStartReq                                    ; X6  Fast home position return command
       MPS
       ANI   FX5SSC_1.stnAxMntr_D[0].uStatus_D.3                        ; U1\G2417.3  R:Status(Direct)
       SET   bFastOPRStartReq                                           ; Fast home position return command
       MPP
       MOVP  K9002 uPositioningStartNo                                  ; Positioning start No.
       SET   bFastOPRStartReq_H                                         ; Fast home position return command storage
```

- Contact type (read from figure): X6 is a normally open contact; FX5SSC_1.stnAxMntr_D[0].uStatus_D.3 (U1\G2417.3) is a normally closed contact.
- Only SET bFastOPRStartReq is in series with the U1\G2417.3 normally closed contact. MOVP K9002 and SET bFastOPRStartReq_H branch from right after X6 (they do not pass through U1\G2417.3).

##### Positioning with positioning data No.1 (位置決めデータNo.1による位置決め) (13.3 / original p.705)

```
// [Title]Positioning with positioning data No.1
//   ■Start condition X7 (positioning start command: K1)→Positioning start program
(305)  LD    G_bInputSetStartPositioningNoReq                           ; X7  Positioning start command
       MOVP  K1 uPositioningStartNo                                     ; Positioning start No.
```

- Contact type (read from figure): X7 is a normally open contact.

##### Speed-position switching operation (Positioning data No.2) (速度・位置切換え制御(位置決めデータNo.2)) (13.3 / original p.705)

In the ABS mode, new movement amount is not needed to be written.

```
// [Title]Speed-position switching control (Positioning data No.2)
//   ■Start condition  External command valid program start→X10 (Speed-position switching operation command: K2)→Positioning start program *Speed-position switching with axis 1 dog signal ※Speed control stop with axis stop start
(452)  LD    G_bInputSpeedPositionSwitchingReq                          ; X10  Speed-position switching operation command
       MOVP  K2 uPositioningStartNo                                     ; Positioning start No.
(772)  LD    G_bInputSpeedPositionSwitchingEnableReq                    ; X11  Speed-position switching enable command
       MOVP  K1 FX5SSC_1.stnAxCtrl1_D[0].uEnableVP_Switching_D          ; U1\G4328  RW:Speed-position switching enable flag(Direct)
(780)  LD    G_bInputSpeedPositionSwitchingDisableReq                   ; X12  Speed-position switching prohibit command
       MOVP  K0 FX5SSC_1.stnAxCtrl1_D[0].uEnableVP_Switching_D          ; U1\G4328  RW:Speed-position switching enable flag(Direct)
(788)  LD    G_bInputChangeSpeedPositionSwitchingMo...                  ; X13  Movement amount change command
       DMOVP udMovementAmount FX5SSC_1.stnAxCtrl1_D[0].udVP_NewMovementAmount_D   ; udMovementAmount: Speed-position switching control move... / U1\G4326  RW:Speed-position switching control movement amount change register(Direct)
```

- Contact type (read from figure): X10, X11, X12 and X13 are normally open contacts.
- The label name of X13 is truncated in the ladder display ("G_bInputChangeSpeedPositionSwitchingMo..."), and the comment of udMovementAmount is truncated ("Speed-position switching control move..."), as printed.
- The heading is "Speed-position switching operation (Positioning data No.2)"; the Title line of the ladder is "Speed-position switching control (Positioning data No.2)" (as printed).

##### Position-speed switching operation (Positioning data No.3) (位置・速度切換え制御(位置決めデータNo.3)) (13.3 / original p.706)

```
// [Title]Position-speed switching operation (Positioning data No.3)
//   ■Start condition External command valid program start→X10 (Position-speed switching operation command: K3)→Positioning start command ※Speed-position switching with axis 1 dog signal ※Speed control stop with axis stop start
(796)  LD    G_bInputPositionSpeedSwitchingReq                          ; X42  Position-speed switching operation command
       MOVP  K3 uPositioningStartNo                                     ; Positioning start No.
(1118) LD    G_bInputPositionSpeedSwitchingEnableReq                    ; X43  Position-speed switching enable command
       MOVP  K1 FX5SSC_1.stnAxCtrl1_D[0].uEnablePV_Switching_D          ; U1\G4332  RW:Position-speed switching enable flag(Direct)
(1126) LD    G_bInputPositionSpeedSwitchingDisableReq                   ; X44  Position-speed switching prohibit command
       MOVP  K0 FX5SSC_1.stnAxCtrl1_D[0].uEnablePV_Switching_D          ; U1\G4332  RW:Position-speed switching enable flag(Direct)
(1134) LD    G_bInputChangePositionSpeedSwitchingSp...                  ; X45  Speed change command
       DMOVP udSpeed FX5SSC_1.stnAxCtrl1_D[0].udPV_NewSpeed_D           ; udSpeed: Position-speed switching control speed / U1\G4330  RW:Position-speed switching control speed change register (Direct)
```

- Contact type (read from figure): X42, X43, X44 and X45 are normally open contacts.
- The statement "X10 (Position-speed switching operation command: K3)" and "Speed-position switching with axis 1 dog signal" are as printed (the contact of (796) is X42). The label name of X45 is truncated in the ladder display ("G_bInputChangePositionSpeedSwitchingSp..."), as printed.

##### High-level positioning control (高度な位置決め制御) (13.3 / original p.706)

```
// [Title]High-level positioning control
//   Block start order: Positioning No1→No2→No5→No10→No15
//   ■Start condition X14 (high-level positioning control start command: K7000)→Positioning start program:
(1142) LD    G_bInputStartAdvancedPositioningReq                        ; X14  High-level positioning control start command
       MOVP  K7000 uPositioningStartNo                                  ; Positioning start No.
```

- Contact type (read from figure): X14 is a normally open contact.

##### Fast home position return command and fast home position return command storage OFF (高速原点復帰指令，高速原点復帰指令記憶のOFF) (13.3 / original p.706)

Not required when fast home position return is not used.

```
// [Title]Fast home position return command and fast home position return command storage OFF
//   Not required when fast home position return is not used
//   ■Start condition X5 (machine home position return command)
(1366) LD    G_bInputOPRStartReq                                        ; X5  Machine home position return command
       OR    G_bInputSetStartPositioningNoReq                           ; X7  Positioning start command
       OR    G_bInputSpeedPositionSwitchingReq                          ; X10  Speed-position switching operation command
       OR    G_bInputPositionSpeedSwitchingReq                          ; X42  Position-speed switching operation command
       OR    G_bInputStartAdvancedPositioningReq                        ; X14  High-level positioning control start command
       OR    bPositioningStartReq                                       ; Positioning start command
       RST   bFastOPRStartReq                                           ; Fast home position return command
       RST   bFastOPRStartReq_H                                         ; Fast home position return command storage
```

- Contact type (read from figure): the six contacts are normally open contacts connected in parallel (OR); the two RST instructions are parallel outputs.

#### Positioning start program (位置決め始動プログラム) (13.3 / original p.707)

Set the local labels as follows.

| No. | Label Name | Data Type | Class |
|---|---|---|---|
| 1 | uPositioningStartNo | Word [Signed] | VAR |
| 2 | bFastOPRStartReq | Bit | VAR |
| 3 | bFastOPRStartReq_H | Bit | VAR |
| 4 | bPositioningStartReq | Bit | VAR |
*The original is a screen capture of the GX Works3 local label setting screen. The "..." button column and the drop-down marks of the "Class" column are not transcribed.

```
// [Title]Positioning start program
//   ■Start condition X15 (positioning start command)
(1615) LDP   G_bInputStartPositioningReq                                ; X15  Positioning start command
       ANI   G_bDuringJogInchingOperation                               ; JOG/inching operation termination
       ANI   G_bDuringMPGOperation                                      ; Manual pulse generator operating flag
       LDI   bFastOPRStartReq                                           ; Fast home position return command
       LD    bFastOPRStartReq                                           ; Fast home position return command
       AND   bFastOPRStartReq_H                                         ; Fast home position return command storage
       ORB
       ANB
       SET   bPositioningStartReq                                       ; Positioning start command
(1731) LD    bPositioningStartReq                                       ; Positioning start command
       LD    M_FX5SSC_StartPositioning_01A_1.o_bOK                      ; Normal completion
       OR    M_FX5SSC_StartPositioning_01A_1.o_bErr                     ; Error completion
       OR    G_bInputErrResetReq                                        ; X40  Error reset command
       ANB
       ANI   FX5SSC_1.stSysMntr2_D.bnBusy_D[0]                          ; U1\G31501.0  R:BUSY(Axis 1 to 8)(Direct)
       RST   bPositioningStartReq                                       ; Positioning start command
(1745) LD    bPositioningStartReq                                       ; Positioning start command
       FB    M_FX5SSC_StartPositioning_01A_1
       // FB title: M_FX5SSC_StartPositioning_01A_1 (M+FX5SSC_StartPo...) Positioning start FB
       // in  B: i_bEN         <- bPositioningStartReq (normally open contact above)   ; Execution command
       // in  DUT: i_stModule  <- FX5SSC_1              ; Module label / Module label
       // in  UW: i_uAxis      <- K1                    ; Target axis
       // in  UW: i_uStartNo   <- uPositioningStartNo   ; Positioning start No. / Cd.3: Positioning start No.
       // out o_bENO :B        -> (line only, no label connected)   ; Execution status
       // out o_bOK :B         -> (line only, no label connected)   ; Normal completion
       // out o_bErr :B        -> (line only, no label connected)   ; Error completion
       // out o_uErrId :UW     -> (line only, no label connected)   ; Error code
```

- Contact type (read from figure): X15 at (1615) is a rising edge (↑) contact. G_bDuringJogInchingOperation, G_bDuringMPGOperation and the upper bFastOPRStartReq are normally closed contacts. The normally closed bFastOPRStartReq contact is in parallel with "bFastOPRStartReq (normally open) in series with bFastOPRStartReq_H (normally open)".
- (1731): o_bOK, o_bErr and X40 are normally open contacts in parallel (OR); FX5SSC_1.stSysMntr2_D.bnBusy_D[0] (U1\G31501.0) is a normally closed contact.
- The comment of G_bDuringJogInchingOperation is shown as "JOG/inching operation termination" in the ladder (as printed). The FB type name is truncated in the ladder display ("(M+FX5SSC_StartPo..."), as printed.

#### M code OFF program (MコードOFFプログラム) (13.3 / original p.707)

```
// [Title]M code OFF request program
//   ■Start condition X16 (M code OFF request)
(2012) LD    G_bInputMcodeOffReq                                        ; X16  M code OFF request
       AND   FX5SSC_1.stnAxMntr_D[0].uStatus_D.C                        ; U1\G2417.C  R:Status(Direct)
       MOVP  K1 FX5SSC_1.stnAxCtrl1_D[0].uClear_M_Code_D                ; U1\G4304  RW:M code OFF request(Direct)
```

- Contact type (read from figure): X16 and U1\G2417.C are normally open contacts.

#### JOG operation setting program (JOG運転設定プログラム) (13.3 / original p.708)

```
// [Title]JOG operation setting program
//   ■Start condition X17 (JOG operation speed setting command)
(0)    LDP   G_bInputSetJogSpeedReq                                     ; X17  JOG operation speed setting command
       DMOVP K20000 FX5SSC_1.stnAxCtrl1_D[0].udJOG_Speed_D              ; U1\G4318  RW:JOG speed(Direct)
       MOVP  K0 FX5SSC_1.stnAxCtrl1_D[0].uInchingMovementAmount_D       ; U1\G4317  RW:Inching movement amount (Direct)
```

- Contact type (read from figure): X17 is a rising edge (↑) contact. DMOVP and MOVP are parallel outputs under the same condition.

#### Inching operation setting program (インチング運転設定プログラム) (13.3 / original p.708)

```
// [Title]Inching operation setting program
//   ■Start condition X46 (inching movement amount setting command)
(128)  LDP   G_bInputSetInchingMovementAmo...                           ; X46  Inching movement amount setting command
       MOVP  K10 FX5SSC_1.stnAxCtrl1_D[0].uInchingMovementAmount_D      ; U1\G4317  RW:Inching movement amount (Direct)
```

- Contact type (read from figure): X46 is a rising edge (↑) contact.
- The label name of X46 is truncated in the ladder display ("G_bInputSetInchingMovementAmo..."), as printed.

#### JOG operation/inching operation execution program (JOG運転／インチング運転実行プログラム) (13.3 / original p.709)

```
// [Title]JOG operation/inching operation execution program
//   ■Start condition X20 (forward run JOG/inching command), X22 (reverse run JOG/inching command)
(257)  LD    G_bInputForwardJogStartReq                                 ; X20  Forward run JOG/inching command
       OR    G_bInputReverseJogStartReq                                 ; X22  Reverse run JOG/inching command
       AND   FX5SSC_1.stSysMntr2_D.bReady_D                             ; U1\G31500.0  R:READY(Direct)
       ANI   FX5SSC_1.stSysMntr2_D.bnBusy_D[0]                          ; U1\G31501.0  R:BUSY(Axis 1 to 8)(Direct)
       SET   G_bDuringJogInchingOperation                               ; JOG/inching operation termination
(439)  LDI   G_bInputForwardJogStartReq                                 ; X20  Forward run JOG/inching command
       ANI   G_bInputReverseJogStartReq                                 ; X22  Reverse run JOG/inching command
       RST   G_bDuringJogInchingOperation                               ; JOG/inching operation termination
(446)  LD    G_bDuringJogInchingOperation                               ; JOG/inching operation termination
       FB    M_FX5SSC_JOG_01A_1
       // FB title: M_FX5SSC_JOG_01A_1 (M+FX5SSC_JOG_0...) JOG/inching operation FB
       // in  B: i_bEN         <- G_bDuringJogInchingOperation (normally open contact above)   ; Execution command
       // in  DUT: i_stModule  <- FX5SSC_1                                          ; Module label / Module label
       // in  UW: i_uAxis      <- K1                                                ; Target axis
       // in  B: i_bFJog       <- G_bInputForwardJogStartReq (X20, normally open contact)   ; Forward run JOG/inching command / Forward run JOG command
       // in  B: i_bRJog       <- G_bInputReverseJogStartReq (X22, normally open contact)   ; Reverse run JOG/inching command / Reverse run JOG command
       // in  UD: i_udJogSpeed <- FX5SSC_1.stnAxCtrl1_D[0].udJOG_Speed_D (U1\G4318)          ; RW:JOG speed(Direct) / Cd.17: JOG speed
       // in  UW: i_uInching   <- FX5SSC_1.stnAxCtrl1_D[0].uInchingMovementAmount_D (U1\G4317)   ; RW:Inching movement amount (Direct) / Cd.16: Inching movement amount
       // out o_bENO :B        -> (line only, no label connected)   ; Execution status
       // out o_bOK :B         -> (line only, no label connected)   ; Normal completion
       // out o_bErr :B        -> (line only, no label connected)   ; Error completion
       // out o_uErrId :UW     -> (line only, no label connected)   ; Error code
```

- Contact type (read from figure): (257): X20 and X22 are normally open contacts in parallel (OR), U1\G31500.0 is a normally open contact and U1\G31501.0 is a normally closed contact. (439): X20 and X22 are normally closed contacts in series. (446): G_bDuringJogInchingOperation, X20 (to i_bFJog) and X22 (to i_bRJog) are normally open contacts, each connected from the left bus to its FB input.
- The comment of G_bDuringJogInchingOperation is shown as "JOG/inching operation termination" in the ladder (as printed). The FB type name is truncated in the ladder display ("(M+FX5SSC_JOG_0..."), and the pin name i_udJogSpeed is shown folded ("i_udJogSpee d"), as printed.

#### Manual pulse generator operation program (手動パルサ運転プログラム) (13.3 / original p.710)

```
// [Title]Manual pulse generator operation program
//   ■Start condition X23↑ (manual pulse generator operation command) ■Start condition X23↓ (manual pulse generator operation command)
(692)  LD    FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D               ; U1\G31500.1  R:Synchronization flag (Direct)
       // [statement] Start of high-speed counter function
       DHIOEN K0 H1 H0
       // [statement] Setting of input value for manual pulse generator via CPU
       DHCMOV FX5CPU.stSD.stHighSpeedInOut.stnHighSpeedCounter[0].dCurrentValue FX5SSC_1.stSysCtrl_D.dInputValueForManualPulseGeneratorViaCPU_D K0
                                                                        ; SD4500  RW :High-speed counter current value / U1\G5946  RW:Input value for Manual pulse generator via CPU(Direct)
(1020) LDP   G_bInputStartMPGReq                                        ; X23  Manual pulse generator operation command
       AND   FX5SSC_1.stSysMntr2_D.bReady_D                             ; U1\G31500.0  R:READY(Direct)
       ANI   FX5SSC_1.stSysMntr2_D.bnBusy_D[0]                          ; U1\G31501.0  R:BUSY(Axis 1 to 8)(Direct)
       SET   G_bDuringMPGOperation                                      ; Manual pulse generator operating flag
(1033) LDF   G_bInputStartMPGReq                                        ; X23  Manual pulse generator operation command
       RST   G_bDuringMPGOperation                                      ; Manual pulse generator operating flag
(1040) LD    G_bDuringMPGOperation                                      ; Manual pulse generator operating flag
       FB    M_FX5SSC_MPG_01A_1
       // FB title: M_FX5SSC_MPG_01A_1 (M+FX5SSC_MPG_0...) Manual pulse generator OP FB
       // in  B: i_bEN                  <- G_bDuringMPGOperation (normally open contact above)   ; Execution command
       // in  DUT: i_stModule           <- FX5SSC_1     ; Module label / Module label
       // in  UW: i_uAxis               <- K1           ; Target axis
       // in  UD: i_udMPGInputMagnification <- K100     ; Cd.20: Manual pulse generator 1 pulse input magnification
       // out o_bENO :B                 -> (line only, no label connected)   ; Execution status
       // out o_bOK :B                  -> (line only, no label connected)   ; Normal completion
       // out o_bErr :B                 -> (line only, no label connected)   ; Error completion
       // out o_uErrId :UW              -> (line only, no label connected)   ; Error code
```

- Contact type (read from figure): bSynchronizationFlag_D (U1\G31500.1) at (692) is a normally open contact; DHIOEN and DHCMOV are parallel outputs under that condition. X23 at (1020) is a rising edge (↑) contact, U1\G31500.0 is a normally open contact and U1\G31501.0 is a normally closed contact. X23 at (1033) is a falling edge (↓) contact. G_bDuringMPGOperation at (1040) is a normally open contact.
- "Start of high-speed counter function" and "Setting of input value for manual pulse generator via CPU" are statement bars (comments) shown above the DHIOEN and DHCMOV instructions.
- The label names are shown folded in the ladder ("FX5CPU.stSD.stHighSpeedInOut.stn / HighSpeedCounter[0].dCurrentValue", "FX5SSC_1.stSysCtrl_D.dInputValueF / orManualPulseGeneratorViaCPU_D", "G_bDuringM / PGOperation", "i_udMPGInpu / tMagnification"). The FB type name is truncated ("(M+FX5SSC_MPG_0..."), as printed.

#### Speed change program (速度変更プログラム) (13.3 / original p.711)

Set the local labels as follows.

| No. | Label Name | Data Type | Class |
|---|---|---|---|
| 1 | bChangeSpeedReq | Bit | VAR |
*The original is a screen capture of the GX Works3 local label setting screen. The "..." button column and the drop-down marks of the "Class" column are not transcribed.

```
// [Title]Speed change program
//   ■Start condition X24 (speed change command)
(0)    LDP   G_bInputChangeSpeedReq                                     ; X24  Speed change command
       AND   FX5SSC_1.stSysMntr2_D.bnBusy_D[0]                          ; U1\G31501.0  R:BUSY(Axis 1 to 8)(Direct)
       SET   bChangeSpeedReq                                            ; Speed change command
(94)   LD    M_FX5SSC_ChangeSpeed_01A_1.o_bOK                           ; Normal completion
       RST   bChangeSpeedReq                                            ; Speed change command
(98)   LD    bChangeSpeedReq                                            ; Speed change command
       FB    M_FX5SSC_ChangeSpeed_01A_1
       // FB title: M_FX5SSC_ChangeSpeed_01A_1 (M+FX5SSC_Chang...) Speed change FB
       // in  B: i_bEN               <- bChangeSpeedReq (normally open contact above)   ; Execution command
       // in  DUT: i_stModule        <- FX5SSC_1     ; Module label / Module label
       // in  UW: i_uAxis            <- K1           ; Target axis
       // in  UD: i_udSpeedChangeValue <- K20000     ; Cd.14: New speed value
       // out o_bENO :B              -> (line only, no label connected)   ; Execution status
       // out o_bOK :B               -> (line only, no label connected)   ; Normal completion
       // out o_bErr :B              -> (line only, no label connected)   ; Error completion
       // out o_uErrId :UW           -> (line only, no label connected)   ; Error code
```

- Contact type (read from figure): X24 at (0) is a rising edge (↑) contact; FX5SSC_1.stSysMntr2_D.bnBusy_D[0] (U1\G31501.0) at (0) is a normally open contact. M_FX5SSC_ChangeSpeed_01A_1.o_bOK at (94) and bChangeSpeedReq at (98) are normally open contacts.
- The FB type name is truncated in the ladder display ("(M+FX5SSC_Chang..."), and the pin name is shown folded ("i_udSpeedC / hangeValue"), as printed.

#### Override program (オーバーライドプログラム) (13.3 / original p.711)

Set the local labels as follows.

| No. | Label Name | Data Type | Class |
|---|---|---|---|
| 1 | bOverrideReq_P | Bit | VAR |
*The original is a screen capture of the GX Works3 local label setting screen. The "..." button column and the drop-down marks of the "Class" column are not transcribed.

```
// [Title]Override program
//   ■Start condition X25 (override command)
(245)  LD    G_bInputOverrideReq                                        ; X25  Override command
       PLS   bOverrideReq_P                                             ; Override command pulse
(326)  LD    bOverrideReq_P                                             ; Override command pulse
       AND   FX5SSC_1.stSysMntr2_D.bnBusy_D[0]                          ; U1\G31501.0  R:BUSY(Axis 1 to 8)(Direct)
       MOVP  K200 FX5SSC_1.stnAxCtrl1_D[0].uOverride_D                  ; U1\G4313  RW:Positioning operation speed override(Direct)
```

- Contact type (read from figure): X25, bOverrideReq_P and U1\G31501.0 are normally open contacts.

#### Acceleration/deceleration time change program (加減速時間変更プログラム) (13.3 / original p.712)

Set the local labels as follows.

| No. | Label Name | Data Type | Class |
|---|---|---|---|
| 1 | bChangeAccDecTime_iEnable | Bit | VAR |
*The original is a screen capture of the GX Works3 local label setting screen. The "..." button column and the drop-down marks of the "Class" column are not transcribed.

```
// [Title]Acceleration/deceleration time change program
//   ■Start condition X27 (acceleration/deceleration time change disable command)
(337)  LDI   G_bInputChangeAccDecTimeDisable                            ; X27  Acceleration/deceleration time change disable command
       OUT   bChangeAccDecTime_iEnable                                  ; Acceleration/deceleration time change enabled flag
(488)  LD    G_bInputChangeAccDecTimeReq                                ; X26  Acceleration/deceleration time change command
       FB    M_FX5SSC_ChangeAccDecTime_01A_1
       // FB title: M_FX5SSC_ChangeAccDecTime_01A_1 (M+FX5SSC_Chang...) Acc./dec. time SV change FB
       // in  B: i_bEN               <- G_bInputChangeAccDecTimeReq (X26, normally open contact above)   ; Execution command
       // in  DUT: i_stModule        <- FX5SSC_1     ; Module label / Module label
       // in  UW: i_uAxis            <- K1           ; Target axis
       // in  B: i_bEnable           <- bChangeAccDecTime_iEnable (normally open contact)   ; Acceleration/deceleration time change enabled flag / Acceleration/deceleration time change enable flag
       // in  UD: i_udNewAccelerationTi...  <- K2000 ; Cd.10: New acceleration time value
       // in  UD: i_udNewDecelerationTi...  <- K0    ; Cd.11: New deceleration time value
       // out o_bENO :B              -> (line only, no label connected)   ; Execution status
       // out o_bOK :B               -> (line only, no label connected)   ; Normal completion
       // out o_bErr :B              -> (line only, no label connected)   ; Error completion
       // out o_uErrId :UW           -> (line only, no label connected)   ; Error code
```

- Contact type (read from figure): X27 at (337) is a normally closed contact. X26 (to i_bEN) and bChangeAccDecTime_iEnable (to i_bEnable) at (488) are normally open contacts, each connected from the left bus to its FB input.
- The pin names of Cd.10/Cd.11 are truncated in the ladder display ("i_udNewAcc / elerationTi...", "i_udNewDec / elerationTi..."), and the FB type name is truncated ("(M+FX5SSC_Chang..."), as printed.

#### Torque change program (トルク変更プログラム) (13.3 / original p.712)

Set the local labels as follows.

| No. | Label Name | Data Type | Class |
|---|---|---|---|
| 1 | bChangeTorqueReq | Bit | VAR |
*The original is a screen capture of the GX Works3 local label setting screen. The "..." button column and the drop-down marks of the "Class" column are not transcribed.

```
// [Title]Torque change program
//   ■Start condition X30 (torque change command)
(629)  LD    G_bInputChangeTorqueReq                                    ; X30  Torque change command
       PLS   bChangeTorqueReq                                           ; Torque change command
(721)  LD    bChangeTorqueReq                                           ; Torque change command
       AND   FX5SSC_1.stSysMntr2_D.bnBusy_D[0]                          ; U1\G31501.0  R:BUSY(Axis 1 to 8)(Direct)
       MOV   K1000 FX5SSC_1.stnAxCtrl1_D[0].uForwardNewTorque_D         ; U1\G4325  RW:New torque value/forward new torque value(Direct)
```

- Contact type (read from figure): X30, bChangeTorqueReq and U1\G31501.0 are normally open contacts. The output at (721) is MOV (non-pulse) in the ladder (as printed).

#### Target position change program (目標位置変更プログラム) (13.3 / original p.713)

Set the local labels as follows.

| No. | Label Name | Data Type | Class |
|---|---|---|---|
| 1 | bTargetPositionChangeReq | Bit | VAR |
*The original is a screen capture of the GX Works3 local label setting screen. The "..." button column and the drop-down marks of the "Class" column are not transcribed.

```
// [Title]Target position change program
//   ■Start condition X47 (target position change command)
(732)  LDP   G_bInputTargetPositionChangeReq                            ; X47  Target position change command
       AND   FX5SSC_1.stSysMntr2_D.bnBusy_D[0]                          ; U1\G31501.0  R:BUSY(Axis 1 to 8)(Direct)
       SET   bTargetPositionChangeReq                                   ; Target position change command
(847)  LD    M_FX5SSC_ChangePosition_01A_1.o_bOK                        ; Normal completion
       RST   bTargetPositionChangeReq                                   ; Target position change command
(851)  LD    bTargetPositionChangeReq                                   ; Target position change command
       FB    M_FX5SSC_ChangePosition_01A_1
       // FB title: M_FX5SSC_ChangePosition_01A_1 (M+FX5SSC_Chang...) Target position change FB
       // in  B: i_bEN               <- bTargetPositionChangeReq (normally open contact above)   ; Execution command
       // in  DUT: i_stModule        <- FX5SSC_1     ; Module label / Module label
       // in  UW: i_uAxis            <- K1           ; Target axis
       // in  D: i_dTargetNewPosition  <- K-750000   ; Cd.27: Target position change value (new address)
       // in  UD: i_udTargetNewSpeed   <- K54000     ; Cd.28: Target position change value (new speed)
       // out o_bENO :B              -> (line only, no label connected)   ; Execution status
       // out o_bOK :B               -> (line only, no label connected)   ; Normal completion
       // out o_bErr :B              -> (line only, no label connected)   ; Error completion
       // out o_uErrId :UW           -> (line only, no label connected)   ; Error code
```

- Contact type (read from figure): X47 at (732) is a rising edge (↑) contact; U1\G31501.0 at (732), o_bOK at (847) and bTargetPositionChangeReq at (851) are normally open contacts.
- The pin names are shown folded in the ladder ("i_dTargetNew / D:Position", "i_udTargetN / UD:ewSpeed"); the FB type name is truncated ("(M+FX5SSC_Chang..."), as printed.

#### Servo parameter reading/writing program (サーボパラメータ読出し／書込みプログラム) (13.3 / original p.714-715)

Set the local labels as follows.

| No. | Label Name | Data Type | Class |
|---|---|---|---|
| 1 | bServoParamRWReq | Bit | VAR |
| 2 | uCmdData | Word [Unsigned]/Bit String [16-bit] | VAR |
| 3 | bServoParamChange | Bit | VAR |
| 4 | bServoParamRead | Bit | VAR |
*The original is a screen capture of the GX Works3 local label setting screen. The "..." button column and the drop-down marks of the "Class" column are not transcribed.

```
// [Title]Servo parameter reading/writing program
//   ■Target parameter PA10 Command in-position width (Obj.2010h)
(1020) LD    G_bInputServoParamRead                                     ; X54  Servo parameter read command
       PLS   bServoParamRead                                            ; Servo parameter read
(1148) LD    bServoParamRead                                            ; Servo parameter read
       MOVP  K1 uCmdData                                                ; Command send request
       SET   bServoParamRWReq                                           ; Servo parameter read/write request
(1156) LD    G_bInputServoParamChange                                   ; X53  Servo parameter change command
       PLS   bServoParamChange                                          ; Servo parameter change
(1161) LD    bServoParamChange                                          ; Servo parameter change
       BMOVP D20 M_FX5SSC_ReadWriteParameter_00A_1.pb_u4SDOData K4      ; D20: Servo parameter change value / pb_u4SDOData: Cd.164: Optional SDO transfer data 1
       MOVP  K11 uCmdData                                               ; Command send request
       SET   bServoParamRWReq                                           ; Servo parameter read/write request
(1174) LD    M_FX5SSC_ReadWriteParameter_00A_1.o_bOK                    ; Normal completion
       MPS
       AND   G_bInputServoParamRead                                     ; X54  Servo parameter read command
       BMOVP M_FX5SSC_ReadWriteParameter_00A_1.pb_u4SDOData D40 K4      ; pb_u4SDOData: Cd.164: Optional SDO transfer data 1 / D40: Servo parameter read value
       MPP
       RST   bServoParamRWReq                                           ; Servo parameter read/write request
(1187) LD    bServoParamRWReq                                           ; Servo parameter read/write request   (original p.715)
       FB    M_FX5SSC_ReadWriteParameter_00A_1
       // FB title: M_FX5SSC_ReadWriteParameter_00A_1 (M+FX5SSC_ReadW...) read/write parameters FB
       // in  B: i_bEN               <- bServoParamRWReq (normally open contact above)   ; Execution command
       // in  DUT: i_stModule        <- FX5SSC_1     ; Module label / Module label
       // in  UW: i_uAxis            <- K1           ; Target axis
       // in  UD: i_udSDONumber      <- H200A00...   ; Pr.512: Optional SDO 1
       // in  UW: i_uSDORequest      <- uCmdData     ; Command send request / Cd.160: Command sending request1
       // out o_bENO :B              -> (line only, no label connected)   ; Execution status
       // out o_bOK :B               -> (line only, no label connected)   ; Normal completion
       // out o_udSDOErrorID :UD     -> (line only, no label connected)   ; ptional SDO transfer result
       // out o_uSDOStatus :UW       -> (line only, no label connected)   ; Optional SDO transfer status
       // out o_bErr :B              -> (line only, no label connected)   ; Error completion
       // out o_uErrId :UW           -> (line only, no label connected)   ; Error code
       // shown at the bottom of the FB box: pb_u4SDOData
```

- Contact type (read from figure): all contacts on p.714-715 (X54, bServoParamRead, X53, bServoParamChange, o_bOK, X54 at (1174), bServoParamRWReq) are normally open contacts.
- (1148) and (1161): the instructions are parallel outputs under the same condition.
- (1174): only BMOVP is in series with X54; RST bServoParamRWReq branches from right after the o_bOK contact (not through X54).
- The rungs (1020) to (1174) are on p.714; the FB rung (1187) is on p.715.
- The i_udSDONumber input constant is truncated in the ladder display ("H200A00..."), as printed (unreadable beyond "H200A00"; see original p.715). The comment of o_udSDOErrorID is shown as "ptional SDO transfer result" (first letter cut off in the display), as printed. The pin names are shown folded ("i_udSDONu / mber", "i_uSDOReq / uest", "o_udSDOErr / orID", "o_uSDOStat / us"), and the FB instance/type names are truncated ("M_FX5SSC_ReadWriteP / arameter_00A_1", "(M+FX5SSC_ReadW..."), as printed.
- The step number (1020) of this program is the same as that of the Manual pulse generator operation program (1020) (as printed).

#### Step operation program (ステップ運転プログラム) (13.3 / original p.715)

Set the local labels as follows.

| No. | Label Name | Data Type | Class |
|---|---|---|---|
| 1 | bStepOperationReq_P | Bit | VAR |
*The original is a screen capture of the GX Works3 local label setting screen. The "..." button column and the drop-down marks of the "Class" column are not transcribed.

```
// [Title]Step mode program
//   ■Start condition X31 (step operation command)
(0)    LD    G_bInputStepOperationReq                                   ; X31  Step operation command
       PLS   bStepOperationReq_P                                        ; Step operation command pulse
(89)   LD    bStepOperationReq_P                                        ; Step operation command pulse
       ANI   FX5SSC_1.stnAxCtrl2_D[0].uPositioningStart_D.0             ; U1\G30104.0  RW:Positioning start(Direct)
       ANI   FX5SSC_1.stnAxMntr_D[0].uStatus_D.E                        ; U1\G2417.E  R:Status(Direct)
       MOV   K1 FX5SSC_1.stnAxCtrl1_D[0].uStepMode_D                    ; U1\G4344  RW:Step mode(Direct)
       MOV   K1 FX5SSC_1.stnAxCtrl1_D[0].uStepValid_D                   ; U1\G4345  RW:Step valid flag(Direct)
(109)  LD    G_bInputStepStartInformationReq                            ; X50  Step start information command
       MOVP  K1 FX5SSC_1.stnAxCtrl1_D[0].uStepStartInformation_D        ; U1\G4346  RW:Step start information (Direct)
```

- Contact type (read from figure): X31, bStepOperationReq_P and X50 are normally open contacts; U1\G30104.0 and U1\G2417.E at (89) are normally closed contacts. The two MOV instructions at (89) are parallel outputs after the U1\G2417.E contact, and are MOV (non-pulse) in the ladder (as printed).
- The heading is "Step operation program"; the Title line of the ladder is "Step mode program" (as printed).

#### Skip program (スキッププログラム) (13.3 / original p.716)

Set the local labels as follows.

| No. | Label Name | Data Type | Class |
|---|---|---|---|
| 1 | bSkipReq_P | Bit | VAR |
| 2 | bSkipReq | Bit | VAR |
*The original is a screen capture of the GX Works3 local label setting screen. The "..." button column and the drop-down marks of the "Class" column are not transcribed.

```
// [Title]Skip command program
//   ■Start condition X32 (skip command)
(0)    LD    G_bInputSkipReq                                            ; X32  Skip command
       PLS   bSkipReq_P                                                 ; Skip command pulse
(81)   LD    bSkipReq_P                                                 ; Skip command pulse
       AND   FX5SSC_1.stSysMntr2_D.bnBusy_D[0]                          ; U1\G31501.0  R:BUSY(Axis 1 to 8)(Direct)
       SET   bSkipReq                                                   ; Skip command
(88)   LD    bSkipReq                                                   ; Skip command
       MOVP  K1 FX5SSC_1.stnAxCtrl1_D[0].uSkip_D                        ; U1\G4347  RW:Skip command (Direct)
       AND=_U FX5SSC_1.stnAxCtrl1_D[0].uSkip_D K0                       ; U1\G4347  RW:Skip command(Direct)
       RST   bSkipReq                                                   ; Skip command
```

- Contact type (read from figure): X32, bSkipReq_P, U1\G31501.0 and bSkipReq are normally open contacts.
- (88): the =_U comparison (U1\G4347 and K0) branch comes out right after the bSkipReq contact; RST bSkipReq is in series with it.
- The heading is "Skip program"; the Title line of the ladder is "Skip command program" (as printed).

#### Teaching program (ティーチングプログラム) (13.3 / original p.716)

Set the local labels as follows.

| No. | Label Name | Data Type | Class |
|---|---|---|---|
| 1 | bTeachingReq_P | Bit | VAR |
| 2 | bTeachingReq | Bit | VAR |
*The original is a screen capture of the GX Works3 local label setting screen. The "..." button column and the drop-down marks of the "Class" column are not transcribed.

```
// [Title]Teaching program
//   ■Start condition X33 (teaching command) *Set in [Da.6] Positioning address/movement amount, or [Da.7] Arc address
(0)    LD    G_bInputTeachingReq                                        ; X33  Teaching command
       PLS   bTeachingReq_P                                             ; Teaching command pulse
(160)  LD    bTeachingReq_P                                             ; Teaching command pulse
       ANI   FX5SSC_1.stSysMntr2_D.bnBusy_D[0]                          ; U1\G31501.0  R:BUSY(Axis 1 to 8)(Direct)
       SET   bTeachingReq                                               ; Teaching command
(167)  LD    bTeachingReq                                               ; Teaching command
       MOVP  K0 FX5SSC_1.stnAxCtrl1_D[0].uTeachingDataSelection_D       ; U1\G4348  RW:Teaching data selection(Direct)
       MOVP  K1 FX5SSC_1.stnAxCtrl1_D[0].uTeachingPositioningDataNo_D   ; U1\G4349  RW:Teaching positioning data No. (Direct)
       AND=_U FX5SSC_1.stnAxCtrl1_D[0].uTeachingPositioningDataNo_D K0  ; U1\G4349  RW:Teaching positioning data No. (Direct)
       RST   bTeachingReq                                               ; Teaching command
```

- Contact type (read from figure): X33, bTeachingReq_P and bTeachingReq are normally open contacts; U1\G31501.0 at (160) is a normally closed contact.
- (167): MOVP K0, MOVP K1 and the =_U comparison (U1\G4349 and K0) branch from right after the bTeachingReq contact; RST bTeachingReq is in series with the comparison.

#### Continuous operation interrupt program (連続運転中断プログラム) (13.3 / original p.717)

Set the local labels as follows.

| No. | Label Name | Data Type | Class |
|---|---|---|---|
| 1 | bStopContinuousOperationReq_P | Bit | VAR |
*The original is a screen capture of the GX Works3 local label setting screen. The "..." button column and the drop-down marks of the "Class" column are not transcribed.

```
// [Title]Continuous operation interrupt request program
//   ■Start condition X34 (continuous operation interrupt command)
(0)    LD    G_bInputStopContinuousOperationReq                         ; X34  Continuous operation interrupt command
       PLS   bStopContinuousOperationReq_P                              ; Continuous operation interrupt command pulse
(137)  LD    bStopContinuousOperationReq_P                              ; Continuous operation interrupt command pulse
       AND   FX5SSC_1.stSysMntr2_D.bnBusy_D[0]                          ; U1\G31501.0  R:BUSY(Axis 1 to 8)(Direct)
       MOV   K1 FX5SSC_1.stnAxCtrl1_D[0].uInterruptOperation_D          ; U1\G4320  RW:Interrupt request during continuous operation(Direct)
```

- Contact type (read from figure): X34, bStopContinuousOperationReq_P and U1\G31501.0 are normally open contacts. The output at (137) is MOV (non-pulse) in the ladder (as printed).

#### Restart program (再始動プログラム) (13.3 / original p.717)

Set the local labels as follows.

| No. | Label Name | Data Type | Class |
|---|---|---|---|
| 1 | bRestartReq | Bit | VAR |
*The original is a screen capture of the GX Works3 local label setting screen. The "..." button column and the drop-down marks of the "Class" column are not transcribed.

```
// [Title]Restart program
//   ■Start condition X35 (restart command)
(0)    LDP   G_bInputRestartReq                                         ; X35  Restart command
       SET   bRestartReq                                                ; Restart command
(80)   LDP   M_FX5SSC_Restart_01A_1.o_bOK                               ; Normal completion
       RST   bRestartReq                                                ; Restart command
(86)   LD    bRestartReq                                                ; Restart command
       FB    M_FX5SSC_Restart_01A_1
       // FB title: M_FX5SSC_Restart_01A_1 (M+FX5SSC_Restart...) Restart FB
       // in  B: i_bEN               <- bRestartReq (normally open contact above)   ; Execution command
       // in  DUT: i_stModule        <- FX5SSC_1     ; Module label / Module label
       // in  UW: i_uAxis            <- K1           ; Target axis
       // out o_bENO :B              -> (line only, no label connected)   ; Execution status
       // out o_bOK :B               -> (line only, no label connected)   ; Normal completion
       // out o_bErr :B              -> (line only, no label connected)   ; Error completion
       // out o_uErrId :UW           -> (line only, no label connected)   ; Error code
```

- Contact type (read from figure): X35 at (0) and M_FX5SSC_Restart_01A_1.o_bOK at (80) are rising edge (↑) contacts; bRestartReq at (86) is a normally open contact.
- The FB type name is truncated in the ladder display ("(M+FX5SSC_Restart..."), as printed.

#### Parameter initialization program (パラメータ初期化プログラム) (13.3 / original p.718)

```
// [Title]Parameter initialization program
//   ■Start condition X36 (parameter initialization command)
(0)    LDP   G_bInputInitializeParameterReq                             ; X36  Parameter initialization command
       SET   G_bInitializeParameterReq                                  ; Parameter initialization command
(117)  LD    M_FX5SSC_InitializeParameter_00A_1.o_bOK                   ; Normal completion
       RST   G_bInitializeParameterReq                                  ; Parameter initialization command
(122)  LD    G_bInitializeParameterReq                                  ; Parameter initialization command
       FB    M_FX5SSC_InitializeParameter_00A_1
       // FB title: M_FX5SSC_InitializeParameter_00A_1 (M+FX5SSC_Initializ...) Parameter Initialization FB
       // in  B: i_bEN               <- G_bInitializeParameterReq (normally open contact above)   ; Execution command
       // in  DUT: i_stModule        <- FX5SSC_1     ; Module label / Module label
       // out o_bENO :B              -> (line only, no label connected)   ; Execution status
       // out o_bOK :B               -> (line only, no label connected)   ; Normal completion
       // out o_bErr :B              -> (line only, no label connected)   ; Error completion
       // out o_uErrId :UW           -> (line only, no label connected)   ; Error code
```

- Contact type (read from figure): X36 at (0) is a rising edge (↑) contact; o_bOK at (117) and G_bInitializeParameterReq at (122) are normally open contacts.
- The FB instance/type names are truncated in the ladder display ("M_FX5SSC_InitializeParamet / er_00A_1", "(M+FX5SSC_Initializ..."), as printed. A small square mark is shown in an empty cell of the FB rung (left of the o_bErr row) in the original (no instruction; as printed).

#### Flash ROM write program (フラッシュROM書込みプログラム) (13.3 / original p.718)

```
// [Title]Flash ROM write program
//   ■Start condition X37 (flash ROM write command)
(0)    LDP   G_bInputWriteFlashReq                                      ; X37  Flash ROM write command
       SET   G_bWriteFlashReq                                           ; Flash ROM write command
(99)   LD    M_FX5SSC_WriteFlash_00A_1.o_bOK                            ; Normal completion
       RST   G_bWriteFlashReq                                           ; Flash ROM write command
(104)  LD    G_bWriteFlashReq                                           ; Flash ROM write command
       FB    M_FX5SSC_WriteFlash_00A_1
       // FB title: M_FX5SSC_WriteFlash_00A_1 (M+FX5SSC_WriteFl...) Flash ROM writing FB
       // in  B: i_bEN               <- G_bWriteFlashReq (normally open contact above)   ; Execution command
       // in  DUT: i_stModule        <- FX5SSC_1     ; Module label / Module label
       // out o_bENO :B              -> (line only, no label connected)   ; Execution status
       // out o_bOK :B               -> (line only, no label connected)   ; Normal completion
       // out o_bErr :B              -> (line only, no label connected)   ; Error completion
       // out o_uErrId :UW           -> (line only, no label connected)   ; Error code
```

- Contact type (read from figure): X37 at (0) is a rising edge (↑) contact; o_bOK at (99) and G_bWriteFlashReq at (104) are normally open contacts.
- The FB type name is truncated in the ladder display ("(M+FX5SSC_WriteFl..."), as printed. A small square mark is shown in an empty cell of the FB rung (left of the o_bErr row) in the original (no instruction; as printed).

#### Error reset program (エラーリセットプログラム) (13.3 / original p.719)

Set the local labels as follows.

| No. | Label Name | Data Type | Class |
|---|---|---|---|
| 1 | bErrReadReq | Bit | VAR |
| 2 | bErrResetReq | Bit | VAR |
*The original is a screen capture of the GX Works3 local label setting screen. The "..." button column and the drop-down marks of the "Class" column are not transcribed.

```
// [Title]Error reset program
//   ■Start condition X40 (error reset command)
(0)    LD    FX5SSC_1.stnAxMntr_D[0].uStatus_D.D                        ; U1\G2417.D  R:Status(Direct)
       OR    FX5SSC_1.stnAxMntr_D[0].uStatus_D.9                        ; U1\G2417.9  R:Status(Direct)
       OUT   bErrReadReq                                                ; Error read command
(90)   LD    G_bInputErrResetReq                                        ; X40  Error reset command
       PLS   bErrResetReq                                               ; Error reset command
(95)   LD    bErrReadReq                                                ; Error read command
       FB    M_FX5SSC_OperateError_01A_1
       // FB title: M_FX5SSC_OperateError_01A_1 (M+FX5SSC_Operat...) Error operation FB
       // in  B: i_bEN               <- bErrReadReq (normally open contact above)   ; Execution command
       // in  DUT: i_stModule        <- FX5SSC_1     ; Module label / Module label
       // in  UW: i_uAxis            <- K1           ; Target axis
       // in  B: i_bErrReset         <- bErrResetReq (normally open contact)   ; Error reset command / Error reset command
       // out o_bENO :B              -> (line only, no label connected)   ; Execution status
       // out o_bOK :B               -> (line only, no label connected)   ; Normal completion
       // out o_bModuleErr :B        -> (line only, no label connected)   ; Axis error detection
       // out o_uModuleErrId :UW     -> (line only, no label connected)   ; Axis error code
       // out o_bModuleWarn :B       -> (line only, no label connected)   ; Axis warning detection
       // out o_uModuleWarnId :UW    -> (line only, no label connected)   ; Axis warning code
       // out o_bErr :B              -> (line only, no label connected)   ; Error completion
       // out o_uErrId :UW           -> (line only, no label connected)   ; Error code
```

- Contact type (read from figure): U1\G2417.D and U1\G2417.9 at (0) are normally open contacts in parallel (OR); X40 at (90), bErrReadReq (to i_bEN) and bErrResetReq (to i_bErrReset) at (95) are normally open contacts. bErrResetReq is connected from the left bus to the i_bErrReset input.
- The FB type name is truncated in the ladder display ("(M+FX5SSC_Operat..."), and the pin name o_uModuleWarnId is shown folded ("o_uModuleWarnI / d :UW"), as printed.

#### Axis stop program (軸停止プログラム) (13.3 / original p.720)

Set the local labels as follows.

| No. | Label Name | Data Type | Class |
|---|---|---|---|
| 1 | bStopReq_P | Bit | VAR |
*The original is a screen capture of the GX Works3 local label setting screen. The "..." button column and the drop-down marks of the "Class" column are not transcribed.

```
// [Title]Axis stop program
//   ■Start condition X41 (stop command)
(0)    LD    G_bInputStopReq                                            ; X41  Stop command
       PLS   bStopReq_P                                                 ; Stop command
(78)   LD    bStopReq_P                                                 ; Stop command
       SET   FX5SSC_1.stnAxCtrl2_D[0].uStopAxis_D.0                     ; U1\G30100.0  RW:Axis stop(Direct)
(83)   LDI   G_bInputStopReq                                            ; X41  Stop command
       RST   FX5SSC_1.stnAxCtrl2_D[0].uStopAxis_D.0                     ; U1\G30100.0  RW:Axis stop(Direct)
```

- Contact type (read from figure): X41 at (0) and bStopReq_P at (78) are normally open contacts; X41 at (83) is a normally closed contact.
