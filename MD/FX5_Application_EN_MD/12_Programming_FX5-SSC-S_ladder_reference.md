# 12 PROGRAMMING [FX5-SSC-S] (プログラミング[FX5-SSC-S]) (Chapter 12 / original p.624-675)

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

## Conversion range (変換範囲表 / original p.624-675)

| Original page | Section | Handling |
|---|---|---|
| p.624 | 12 PROGRAMMING [FX5-SSC-S] (chapter introduction) | Full text |
| p.624 | 12.1 Precautions for Creating Program (reading/writing the data, speed change interval, overrun, system configuration) | Full text |
| p.625 | 12.2 Creating a Program (general configuration of program) | Full text |
| p.626-629 | 12.3 List of labels used (module label, global label) | Full text |
| p.630-641 | 12.3 Program examples (for using labels) | Full text (ladder transcribed as mnemonic) |
| p.642-649 | 12.4 Positioning Program Examples (For Using Buffer Memory) — List of devices used | Full text |
| p.650-675 | 12.4 Program examples (for using buffer memory) (No.1 to No.29, ladder transcribed as mnemonic) | Full text |

## Table of Contents (目次)

- 12 PROGRAMMING [FX5-SSC-S] (プログラミング[FX5-SSC-S])
- 12.1 Precautions for Creating Program (プログラム作成上の注意事項)
- 12.2 Creating a Program (プログラムの作成)
- 12.3 Positioning Program Examples (For Using Labels) (位置決めプログラム例(ラベル使用時))
- 12.4 Positioning Program Examples (For Using Buffer Memory) (位置決めプログラム例(バッファメモリ使用時))

---

## 12 PROGRAMMING [FX5-SSC-S] (プログラミング[FX5-SSC-S]) (Chapter 12 / original p.624)

This chapter describes the programs required to carry out positioning control with the Simple Motion module.
The program required for control is created allowing for the "start conditions", "start time chart", "device settings" and general control configuration. (The parameters, positioning data, block start data and condition data, etc., must be set in the Simple Motion module according to the control to be executed, and a setting program for the control data or a start program for the various controls must be created.)

## 12.1 Precautions for Creating Program (プログラム作成上の注意事項) (12.1 / original p.624)

The common precautions to be taken when writing data from the CPU module to the buffer memory of the Simple Motion module are described below.

#### Reading/writing the data (データの読出し／書込み) (12.1 / original p.624)

Setting the data explained in this chapter (various parameters, positioning data, block start data) should be set using an engineering tool. When set with the program, many programs and devices must be used. This will not only complicate the program, but will also increase the scan time. When rewriting the positioning data during continuous path control or continuous positioning control, rewrite the data four positioning data items before the actual execution. If the positioning data is not rewritten before the positioning data four items earlier is executed, the process will be carried out as if the data was not rewritten.

#### Restrictions to speed change execution interval (速度変更実行間隔の制約) (12.1 / original p.624)

Be sure there is an interval between the speed changes of 10 ms or more when carrying out consecutive speed changes by the speed change function or override function with the Simple Motion module.

#### Process during overrun (オーバーラン時の処理) (12.1 / original p.624)

Overrun is prevented by the setting of the upper and lower stroke limits with the detailed parameter 1. However, this applies only when the Simple Motion module is operating correctly. From a system safety perspective, creating an external circuit that includes a boundary limit switch that turns OFF the main circuit power of the servo amplifier when activated is recommended.

#### System configuration (システム構成) (12.1 / original p.624)

The following figure shows the system configuration used for the program examples.

[Figure] System configuration used for the program examples (original p.624)
- Modules connected from left to right: (1) FX5U-32MR/ES, (2) FX5-40SSC-S, (3) FX5-16EX/ES, (4) FX5-16EX/ES.
- From the External device: X00 to X17 go to (1), X20 to X37 go to (3), X40 to X57 go to (4) (arrows).
- A Servo amplifier (MR-J4-_B_) is connected below (2), and a Servo motor is connected to the servo amplifier.

## 12.2 Creating a Program (プログラムの作成) (12.2 / original p.625)

The "positioning control operation program" actually used is explained in this section.

### General configuration of program (プログラムの全体構成) (12.2 / original p.625)

The general configuration of the positioning control operation program is shown below.

| No. | Program name | Remark |
|---|---|---|
| 1 | Parameter setting program | • The program is not required when the parameter, positioning data, block start data, and servo parameter are set using an engineering tool.<br>• The setting of the home position return parameters is not required when the machine home position return control is not executed. |
| 2 | Positioning data setting program | • The program is not required when the parameter, positioning data, block start data, and servo parameter are set using an engineering tool.<br>• The setting of the home position return parameters is not required when the machine home position return control is not executed. |
| 3 | Block start data setting program | • The program is not required when the parameter, positioning data, block start data, and servo parameter are set using an engineering tool.<br>• The setting of the home position return parameters is not required when the machine home position return control is not executed. |
| 4 | Servo parameter setting program | • The program is not required when the parameter, positioning data, block start data, and servo parameter are set using an engineering tool.<br>• The setting of the home position return parameters is not required when the machine home position return control is not executed. |
| 5 | Home position return request OFF program | Not required when the fast home position return is executed. |
| 6 | External command function valid setting program | — |
| 7 | PLC READY signal ON program | — |
| 8 | All axis servo ON program | — |
| 9 | Positioning start No. setting program | — |
| 10 | Positioning start program | — |
| 11 | M code OFF program | Not required when the M code output function is not used. |
| 12 | JOG operation setting program | Not required when the JOG operation is not used. |
| 13 | Inching operation setting program | Not required when the inching operation is not used. |
| 14 | JOG operation/inching operation execution program | Not required when the JOG operation or the inching operation is not used. |
| 15 | Manual pulse generator operation program | Not required when the manual pulse generator operation is not used. |
| 16 | Speed change program | Add the program as necessary. |
| 17 | Override program | Add the program as necessary. |
| 18 | Acceleration/deceleration time change program | Add the program as necessary. |
| 19 | Torque change program | Add the program as necessary. |
| 20 | Step operation program | Add the program as necessary. |
| 21 | Skip program | Add the program as necessary. |
| 22 | Teaching program | Add the program as necessary. |
| 23 | Continuous operation interrupt program | Add the program as necessary. |
| 24 | Target position change program | Add the program as necessary. |
| 25 | Restart program | Add the program as necessary. |
| 26 | Parameter initialization program | Add the program as necessary. |
| 27 | Flash ROM write program | Add the program as necessary. |
| 28 | Error reset program | Add the program as necessary. |
| 29 | Axis stop program | — |

*In the original, the "Remark" cell is merged over No.1 to 4 (the two bullet items), over No.6 to 9 ("—"), and over No.16 to 28 ("Add the program as necessary."). Expanded to each row. The "—" of No.10 and No.29 are individual cells.
*No.5 remark reads "Not required when the fast home position return is executed." in the English original (as printed).

## 12.3 Positioning Program Examples (For Using Labels) (位置決めプログラム例(ラベル使用時)) (12.3 / original p.626-641)

### List of labels used (使用するラベル一覧) (12.3 / original p.626-629)

In the program examples, the labels to be used are assigned as follows.

#### Module label (ユニットラベル) (12.3 / original p.626-627)

| Classification | Label name | Description |
|---|---|---|
| Start I/O No. | FX5SSC_1.uIO | Start I/O No. |
| Input signal | FX5SSC_1.stSysCtrl_D.bAllAxisServoOn_D | All axis servo ON |
| Input signal | FX5SSC_1.stSysMntr2_D.bReady_D | READY |
| Input signal | FX5SSC_1.bSynchronizationFlag | Synchronization flag |
| Input signal | FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D | Synchronization flag |
| Input signal | FX5SSC_1.stSysMntr2_D.bnBusy_D[0] | Axis 1 BUSY signal |
| Output signal | FX5SSC_1.stSysCtrl_D.bPLC_Ready_D | PLC READY signal |
| Output signal | FX5SSC_1.stnAxCtrl2_D[0].uPositioningStart_D.0 | Axis 1 Positioning start signal |
| Parameter | FX5SSC_1.stnAxPrm_D[0].dHomePosition_D | Axis 1 Home position address |
| Parameter | FX5SSC_1.stnAxPrm_D[0].dSoftwareStrokeLowerLimit_D | Axis 1 Software stroke limit lower limit value |
| Parameter | FX5SSC_1.stnAxPrm_D[0].dSoftwareStrokeUpperLimit_D | Axis 1 Software stroke limit upper limit value |
| Parameter | FX5SSC_1.stnAxPrm_D[0].uExternalCommandFunctionMode_D | Axis 1 External command function selection |
| Parameter | FX5SSC_1.stnAxPrm_D[0].uHomingDirection_D | Axis 1 Home position return direction |
| Parameter | FX5SSC_1.stnAxPrm_D[0].uHomingMethod_D | Axis 1 Home position return method |
| Parameter | FX5SSC_1.stnAxPrm_D[0].uHomingRetry_D | Axis 1 Home position return retry |
| Parameter | FX5SSC_1.stnAxPrm_D[0].uUnitMagnification_D | Axis 1 Unit magnification (AM) |
| Parameter | FX5SSC_1.stnAxPrm_D[0].uUnit_D | Axis 1 Unit setting |
| Parameter | FX5SSC_1.stnAxPrm_D[0].uVP_Mode_D | Axis 1 Speed-position function selection |
| Parameter | FX5SSC_1.stnAxPrm_D[0].uV_CommandPosition_D | Axis 1 Command position value during speed control |
| Parameter | FX5SSC_1.stnAxPrm_D[0].udCreepSpeed_D | Axis 1 Creep speed |
| Parameter | FX5SSC_1.stnAxPrm_D[0].udHomingSpeed_D | Axis 1 Home position return speed |
| Parameter | FX5SSC_1.stnAxPrm_D[0].udMovementAmountPerRotation_D | Axis 1 Movement amount per rotation (AL) |
| Parameter | FX5SSC_1.stnAxPrm_D[0].udPulsesPerRotation_D | Axis 1 Number of pulses per rotation (AP) |
| Axis monitor data | FX5SSC_1.stnAxMntr_D[0].uM_Code_D | Axis 1 Valid M code |
| Axis monitor data | FX5SSC_1.stnAxMntr_D[0].uStatus_D.3 | Axis 1 Home position return request flag |
| Axis monitor data | FX5SSC_1.stnAxMntr_D[0].uStatus_D.9 | Axis 1 Axis warning detection |
| Axis monitor data | FX5SSC_1.stnAxMntr_D[0].uStatus_D.C | Axis 1 M code ON |
| Axis monitor data | FX5SSC_1.stnAxMntr[0].uStatus.D | Axis 1 Error detection |
| Axis monitor data | FX5SSC_1.stnAxMntr_D[0].uStatus_D.D | Axis 1 Error detection |
| Axis monitor data | FX5SSC_1.stnAxMntr[0].uStatus.E | Axis 1 Start complete |
| Axis monitor data | FX5SSC_1.stnAxMntr_D[0].uStatus_D.E | Axis 1 Start complete |
| Axis monitor data | FX5SSC_1.stnAxMntr_D[0].uStatus_D.F | Axis 1 Positioning complete |
| Axis monitor data | FX5SSC_1.stnAxMntr_D[0].dCommandPosition_D | Axis 1 Command position value |
| System monitor data | FX5SSC_1.stSysMntr1_D.wSSCNET_ControlStatus_D | SSCNET control status |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].dNewPosition_D | Axis 1 New position value |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uClearHomingRequestFlag_D | Axis 1 Home position return request flag OFF request |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uClear_M_Code_D | Axis 1 M code OFF request |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uEnablePV_Switching_D | Axis 1 Position-speed switching enable flag |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uEnableVP_Switching_D | Axis 1 Speed-position switching enable flag |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uExternalCommandValid_D | Axis 1 External command valid |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uForwardNewTorque_D | Axis 1 New torque value/forward new torque value |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uInterruptOperation_D | Axis 1 Interrupt request during continuous operation |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uOverride_D | Axis 1 Positioning operation speed override |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uPositioningStartNo_D | Axis 1 Positioning start No. |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uPositioningStartingPointNo_D | Axis 1 Positioning starting point No. |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uSkip_D | Axis 1 Skip command |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uStepMode_D | Axis 1 Step mode |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uStepStartInformation_D | Axis 1 Step start information |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uStepValid_D | Axis 1 Step valid flag |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uTeachingDataSelection_D | Axis 1 Teaching data selection |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].uTeachingPositioningDataNo_D | Axis 1 Teaching positioning data No. |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].udNewSpeed_D | Axis 1 New speed value |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].udPV_NewSpeed_D | Axis 1 Position-speed switching control speed change register |
| Axis control data 1 | FX5SSC_1.stnAxCtrl1_D[0].udVP_NewMovementAmount_D | Axis 1 Speed-position switching control movement amount change register |
| System control data | FX5SSC_1.stSysCtrl_D.wSSCNET_ControlCommand_D | SSCNET control command |
| Axis control data 2 | FX5SSC_1.stnAxCtrl2_D[0].uProhibitPositioning_D | Axis 1 Execution prohibition flag |
| Axis control data 2 | FX5SSC_1.stnAxCtrl2_D[0].uProhibitPositioning_D.0 | Axis 1 Execution prohibition flag |
| Axis control data 2 | FX5SSC_1.stnAxCtrl2_D[0].uStopAxis_D | Axis 1 Axis stop |
| Axis control data 2 | FX5SSC_1.stnAxCtrl2_D[0].uStopAxis_D.0 | Axis 1 Axis stop |

*In the original, the "Classification" cells (Input signal, Output signal, Parameter, Axis monitor data, Axis control data 1, Axis control data 2) are merged cells. In the "Description" column, "Synchronization flag", "Axis 1 Error detection", "Axis 1 Start complete", "Axis 1 Execution prohibition flag" and "Axis 1 Axis stop" are each merged over 2 rows. Expanded to each row. The table spans p.626 and p.627; the header row (Classification / Label name / Description) is repeated on p.627. On p.627, the "Axis control data 1" classification cell is printed as two separate cells: 12 rows (dNewPosition_D to uSkip_D) and 8 rows (uStepMode_D to udVP_NewMovementAmount_D) (both "Axis control data 1", as printed).
*"FX5SSC_1.stnAxMntr[0].uStatus.D" and "FX5SSC_1.stnAxMntr[0].uStatus.E" are written without "_D", unlike the other rows (as printed).

#### Global label (グローバルラベル) (12.3 / original p.628-629)

The following describes the global labels used in the program examples. Set the global labels as follows.

- Global label that the assignment device is not to be set (The unused internal relay and data device are automatically assigned when the assignment device is not set.)

[Figure] Global label setting screen (labels without assignment device) (original p.628-629). Transcribed from the screen capture below.

| No. | Label Name | Data Type | Class | Assign (Device/Label) |
|---|---|---|---|---|
| 1 | bSetPositioningData_bEN | Bit | VAR_GLOBAL | (blank) |
| 2 | bSetPositioningData_bENO | Bit | VAR_GLOBAL | (blank) |
| 3 | bSetPositioningData_bOK | Bit | VAR_GLOBAL | (blank) |
| 4 | bSetPositioningData_bErr | Bit | VAR_GLOBAL | (blank) |
| 5 | uSetPositioningData_bErrId | Word [Unsigned]/Bit String [16-bit] | VAR_GLOBAL | (blank) |
| 6 | bJOG_bENO | Bit | VAR_GLOBAL | (blank) |
| 7 | bJOG_bOK | Bit | VAR_GLOBAL | (blank) |
| 8 | bJOG_bErr | Bit | VAR_GLOBAL | (blank) |
| 9 | uJOG_uErrId | Word [Unsigned]/Bit String [16-bit] | VAR_GLOBAL | (blank) |
| 10 | bMPG_bENO | Bit | VAR_GLOBAL | (blank) |
| 11 | bMPG_bOK | Bit | VAR_GLOBAL | (blank) |
| 12 | bMPG_bErr | Bit | VAR_GLOBAL | (blank) |
| 13 | uMPG_uErrId | Word [Unsigned]/Bit String [16-bit] | VAR_GLOBAL | (blank) |
| 14 | bChangeSpeed_bENO | Bit | VAR_GLOBAL | (blank) |
| 15 | bChangeSpeed_bOK | Bit | VAR_GLOBAL | (blank) |
| 16 | bChangeSpeed_bErr | Bit | VAR_GLOBAL | (blank) |
| 17 | uChangeSpeed_uErrId | Word [Unsigned]/Bit String [16-bit] | VAR_GLOBAL | (blank) |
| 18 | bChangeAccDecTime_bENO | Bit | VAR_GLOBAL | (blank) |
| 19 | bChangeAccDecTime_bOK | Bit | VAR_GLOBAL | (blank) |
| 20 | bChangeAccDecTime_bErr | Bit | VAR_GLOBAL | (blank) |
| 21 | uChangeAccDecTime_uErrId | Word [Unsigned]/Bit String [16-bit] | VAR_GLOBAL | (blank) |
| 22 | bChangePosition_bENO | Bit | VAR_GLOBAL | (blank) |
| 23 | bChangePosition_bOK | Bit | VAR_GLOBAL | (blank) |
| 24 | bChangePosition_bErr | Bit | VAR_GLOBAL | (blank) |
| 25 | uChangePosition_uErrId | Word [Unsigned]/Bit String [16-bit] | VAR_GLOBAL | (blank) |
| 26 | bRestart_bENO | Bit | VAR_GLOBAL | (blank) |
| 27 | bRestart_bOK | Bit | VAR_GLOBAL | (blank) |
| 28 | bRestart_bErr | Bit | VAR_GLOBAL | (blank) |
| 29 | uRestart_uErrId | Word [Unsigned]/Bit String [16-bit] | VAR_GLOBAL | (blank) |
| 30 | bInitializeParameter_bENO | Bit | VAR_GLOBAL | (blank) |
| 31 | bInitializeParameter_bOK | Bit | VAR_GLOBAL | (blank) |
| 32 | bInitializeParameter_bErr | Bit | VAR_GLOBAL | (blank) |
| 33 | uInitializeParameter_uErrId | Word [Unsigned]/Bit String [16-bit] | VAR_GLOBAL | (blank) |
| 34 | bOperateError_bENO | Bit | VAR_GLOBAL | (blank) |
| 35 | bOperateError_bOK | Bit | VAR_GLOBAL | (blank) |
| 36 | bOperateError_bModuleErr | Bit | VAR_GLOBAL | (blank) |
| 37 | uOperateError_uModuleErrId | Word [Unsigned]/Bit String [16-bit] | VAR_GLOBAL | (blank) |
| 38 | bOperateError_bModuleWarn | Bit | VAR_GLOBAL | (blank) |
| 39 | uOperateError_bModuleWarnId | Word [Unsigned]/Bit String [16-bit] | VAR_GLOBAL | (blank) |
| 40 | bOperateError_bErr | Bit | VAR_GLOBAL | (blank) |
| 41 | uOperateError_uErrId | Word [Unsigned]/Bit String [16-bit] | VAR_GLOBAL | (blank) |
| 42 | bWriteFlash_bENO | Bit | VAR_GLOBAL | (blank) |
| 43 | bWriteFlash_bOK | Bit | VAR_GLOBAL | (blank) |
| 44 | bWriteFlash_bErr | Bit | VAR_GLOBAL | (blank) |
| 45 | uWriteFlash_uErrId | Word [Unsigned]/Bit String [16-bit] | VAR_GLOBAL | (blank) |
| 46 | bBasicParamSetComp | Bit | VAR_GLOBAL | (blank) |
| 47 | bSetElectronicGear16bit | Bit | VAR_GLOBAL | (blank) |
| 48 | bOPRParamSetComp | Bit | VAR_GLOBAL | (blank) |
| 49 | uBlockData | Word [Unsigned]/Bit String [16-bit](0..4) | VAR_GLOBAL | (blank) |
| 50 | uBlockInstData | Word [Unsigned]/Bit String [16-bit](0..4) | VAR_GLOBAL | (blank) |
| 51 | bOPRReqFlagOffReq_P | Bit | VAR_GLOBAL | (blank) |
| 52 | bOPRReqFlagOffReq_H | Bit | VAR_GLOBAL | (blank) |
| 53 | bOPRReqFlagOffReq | Bit | VAR_GLOBAL | (blank) |
| 54 | udMovementAmount | Double Word [Unsigned]/Bit String [32-bit] | VAR_GLOBAL | (blank) |
| 55 | udSpeed | Double Word [Signed] | VAR_GLOBAL | (blank) |
| 56 | bStartPositioning_bENO | Bit | VAR_GLOBAL | (blank) |
| 57 | bStartPositioning_bOK | Bit | VAR_GLOBAL | (blank) |
| 58 | bStartPositioning_bErr | Bit | VAR_GLOBAL | (blank) |
| 59 | uStartPositioning_uErrId | Word [Unsigned]/Bit String [16-bit] | VAR_GLOBAL | (blank) |
| 60 | bDuringMPGOperation | Bit | VAR_GLOBAL | (blank) |
| 61 | bFastStartPreparationComp | Bit | VAR_GLOBAL | (blank) |
| 62 | bFastOPRStartReq | Bit | VAR_GLOBAL | (blank) |
| 63 | bFastOPRStartReq_H | Bit | VAR_GLOBAL | (blank) |
| 64 | bDuringJogInchingOperation | Bit | VAR_GLOBAL | (blank) |
| 65 | udJogOperationSpeed | Double Word [Unsigned]/Bit String [32-bit] | VAR_GLOBAL | (blank) |
| 66 | uInchingMovementAmount | Word [Unsigned]/Bit String [16-bit] | VAR_GLOBAL | (blank) |
| 67 | bChangeSpeedReq | Bit | VAR_GLOBAL | (blank) |
| 68 | bOverrideReq_P | Bit | VAR_GLOBAL | (blank) |
| 69 | bAccDecTimeChangeReq | Bit | VAR_GLOBAL | (blank) |
| 70 | bChangeAccDecTime_iEnable | Bit | VAR_GLOBAL | (blank) |
| 71 | bStepOperationReq_P | Bit | VAR_GLOBAL | (blank) |
| 72 | bChangeTorqueReq | Bit | VAR_GLOBAL | (blank) |
| 73 | bSkipReq_P | Bit | VAR_GLOBAL | (blank) |
| 74 | bSkipReq | Bit | VAR_GLOBAL | (blank) |
| 75 | bTeachingReq_P | Bit | VAR_GLOBAL | (blank) |
| 76 | bTeachingReq | Bit | VAR_GLOBAL | (blank) |
| 77 | uTeachingData | Word [Unsigned]/Bit String [16-bit](0..3) | VAR_GLOBAL | (blank) |
| 78 | uTeachingDevice | Bit(0..1) | VAR_GLOBAL | (blank) |
| 79 | uIO | Word [Unsigned]/Bit String [16-bit] | VAR_GLOBAL | (blank) |
| 80 | bStopContinuousOperationReq_P | Bit | VAR_GLOBAL | (blank) |
| 81 | bTargetPositionChangeReq | Bit | VAR_GLOBAL | (blank) |
| 82 | bRestartReq | Bit | VAR_GLOBAL | (blank) |
| 83 | bInitializeParameterReq | Bit | VAR_GLOBAL | (blank) |
| 84 | bWriteFlashReq | Bit | VAR_GLOBAL | (blank) |
| 85 | bErrResetReq | Bit | VAR_GLOBAL | (blank) |
| 86 | bStopReq_P | Bit | VAR_GLOBAL | (blank) |
| 87 | bABRSTReq | Bit | VAR_GLOBAL | (blank) |
| 88 | uOperateError_bModuleErrId | Word [Unsigned]/Bit String [16-bit] | VAR_GLOBAL | (blank) |
| 89 | bErrReadReq | Bit | VAR_GLOBAL | (blank) |
| 90 | bPositioningStartReq | Bit | VAR_GLOBAL | (blank) |
| 91 | bABRSTReq_P | Bit | VAR_GLOBAL | (blank) |
| 92 | bABRST_bENO | Bit | VAR_GLOBAL | (blank) |
| 93 | bABRST_bOK | Bit | VAR_GLOBAL | (blank) |
| 94 | bABRST_bAbsNG | Bit | VAR_GLOBAL | (blank) |
| 95 | uABRST_uAbsErrId | Word [Unsigned]/Bit String [16-bit] | VAR_GLOBAL | (blank) |
| 96 | bABRST_bErr | Bit | VAR_GLOBAL | (blank) |
| 97 | uABRST_uErrId | Word [Unsigned]/Bit String [16-bit] | VAR_GLOBAL | (blank) |
| 98 | bPosiStart10 | Bit | VAR_GLOBAL | (blank) |
| 99 | uPositioningStartNo | Word [Unsigned]/Bit String [16-bit] | VAR_GLOBAL | (blank) |
*The original is a screen capture of the GX Works3 global label setting screen (No.1 to 85 on p.628, No.86 to 99 on p.629). The "..." button column and the drop-down marks of the "Class" column are not transcribed. The "Assign (Device/Label)" column is blank for all rows. The English screen has no comment column.
*No.5 is shown as "uSetPositioningData_bErrId", No.39 as "uOperateError_bModuleWarnId", No.88 as "uOperateError_bModuleErrId" on the screen (as printed). No.70 reads "bChangeAccDecTime_iEnable".

- Global label that the assignment device is to be set

[Figure] Global label setting screen (labels with assignment device) (original p.629). Transcribed from the screen capture below.

| No. | Label Name | Data Type | Class | Assign (Device/Label) |
|---|---|---|---|---|
| 100 | bInputOPRReqFlagOffReq | Bit | VAR_GLOBAL | X0 |
| 101 | bInputExternalCommandValidReq | Bit | VAR_GLOBAL | X1 |
| 102 | bInputExternalCommandInvalidReq | Bit | VAR_GLOBAL | X2 |
| 103 | bInputOPRStartReq | Bit | VAR_GLOBAL | X3 |
| 104 | bInputFastOPRStartReq | Bit | VAR_GLOBAL | X4 |
| 105 | bInputStartPositioningNoReq | Bit | VAR_GLOBAL | X5 |
| 106 | bInputSpeedPositionSwitchingReq | Bit | VAR_GLOBAL | X6 |
| 107 | bInputSpeedPositionSwitchingEnableReq | Bit | VAR_GLOBAL | X7 |
| 108 | bInputSpeedPositionSwitchingDisableReq | Bit | VAR_GLOBAL | X10 |
| 109 | bInputChangeSpeedPositionSwitchingMovementAmount | Bit | VAR_GLOBAL | X11 |
| 110 | bInputStartAdvancedPositioningReq | Bit | VAR_GLOBAL | X12 |
| 111 | bInputMcodeOffReq | Bit | VAR_GLOBAL | X14 |
| 112 | bInputSetJogSpeedReq | Bit | VAR_GLOBAL | X15 |
| 113 | bInputForwardJogStartReq | Bit | VAR_GLOBAL | X16 |
| 114 | bInputReverseJogStartReq | Bit | VAR_GLOBAL | X17 |
| 115 | bInputStartMPGReq | Bit | VAR_GLOBAL | X20 |
| 116 | bInputChangeSpeedReq | Bit | VAR_GLOBAL | X22 |
| 117 | bInputOverrideReq | Bit | VAR_GLOBAL | X23 |
| 118 | bInputChangeAccDecTimeReq | Bit | VAR_GLOBAL | X24 |
| 119 | bInputChangeAccDecTimeDisable | Bit | VAR_GLOBAL | X25 |
| 120 | bInputChangeTorqueReq | Bit | VAR_GLOBAL | X26 |
| 121 | bInputStepOperationReq | Bit | VAR_GLOBAL | X27 |
| 122 | bInputSkipReq | Bit | VAR_GLOBAL | X30 |
| 123 | bInputTeachingReq | Bit | VAR_GLOBAL | X31 |
| 124 | bInputStopContinuousOperationReq | Bit | VAR_GLOBAL | X32 |
| 125 | bInputRestartReq | Bit | VAR_GLOBAL | X33 |
| 126 | bInputInitializeParameterReq | Bit | VAR_GLOBAL | X34 |
| 127 | bInputWriteFlashReq | Bit | VAR_GLOBAL | X35 |
| 128 | bInputErrResetReq | Bit | VAR_GLOBAL | X36 |
| 129 | bInputStopReq | Bit | VAR_GLOBAL | X37 |
| 130 | bInputPositionSpeedSwitchingReq | Bit | VAR_GLOBAL | X40 |
| 131 | bInputPositionSpeedSwitchingEnableReq | Bit | VAR_GLOBAL | X41 |
| 132 | bInputPositionSpeedSwitchingDisableReq | Bit | VAR_GLOBAL | X42 |
| 133 | bInputChangePositionSpeedSwitchingSpeedReq | Bit | VAR_GLOBAL | X43 |
| 134 | bInputSetInchingMovementAmountReq | Bit | VAR_GLOBAL | X44 |
| 135 | bInputTargetPositionChangeReq | Bit | VAR_GLOBAL | X45 |
| 136 | bInputStepStartInformationReq | Bit | VAR_GLOBAL | X46 |
| 137 | bInputSpeedPositionSwitchingAbsSetReq | Bit | VAR_GLOBAL | X56 |
| 138 | bAllAxisServoOnReq | Bit | VAR_GLOBAL | X57 |
*The original is a screen capture of the GX Works3 global label setting screen. The "..." button column and the drop-down marks are not transcribed. For No.100 to 138, "Data Type" is "Bit" and "Class" is "VAR_GLOBAL" for all rows.

### Program examples (for using labels) (プログラム例(ラベル使用時)) (12.3 / original p.630-641)

For details of the module function blocks (FBs), refer to "Simple Motion Module FB/Motion Module FB" in the following manual.
[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module Function Block Reference

Transcription notation:
- The ladder diagrams are transcribed as mnemonic. The number in parentheses is the step number shown at the left of the ladder rung in the original. After `;` is the device assigned to the label, as shown under the label in the ladder (`U1¥G` is written as `U1\G`).
- A module FB (function block) call cannot be expressed as one mnemonic instruction; it is written as an `FB <instance>` line, followed by the input/output connections as `//` lines (transcription notation). Label names that the ladder cell truncates with "..." are written as shown.
- Parallel branches are expressed with MPS/MRD/MPP/ORB/ANB (transcription of the ladder branch structure).
- Contact type: `LD`/`AND` = normally open, `LDI`/`ANI` = normally closed, `LDP`/`ANDP` = rising edge (↑), `LDF` = falling edge (↓).

#### Parameter setting program (パラメータ設定プログラム) (12.3 / original p.630)

This program is not required when the parameter is set by "Module Parameter" using an engineering tool.

##### Setting for basic parameter 1 (axis 1) (基本パラメータ1(軸1)の設定) (12.3 / original p.630)

```
(0)   LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D                  ; U1\G31500.1
      MOV   K0 FX5SSC_1.stnAxPrm_D[0].uUnit_D                             ; U1\G0
      MOV   K1 FX5SSC_1.stnAxPrm_D[0].uUnitMagnification_D                ; U1\G1
      DMOVP K4194304 FX5SSC_1.stnAxPrm_D[0].udPulsesPerRotation_D         ; U1\G2
      DMOVP K250000 FX5SSC_1.stnAxPrm_D[0].udMovementAmountPerRotation_D  ; U1\G4
      SET   bBasicParamSetComp
```

##### Setting for home position return basic parameter (axis 1) (原点復帰基本パラメータ(軸1)の設定) (12.3 / original p.630)

```
(75)  LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D                  ; U1\G31500.1
      MOVP  K0 FX5SSC_1.stnAxPrm_D[0].uHomingMethod_D                     ; U1\G70
      MOVP  K0 FX5SSC_1.stnAxPrm_D[0].uHomingDirection_D                  ; U1\G71
      DMOVP K0 FX5SSC_1.stnAxPrm_D[0].dHomePosition_D                     ; U1\G72
      DMOVP K5000 FX5SSC_1.stnAxPrm_D[0].udHomingSpeed_D                  ; U1\G74
      DMOVP K1500 FX5SSC_1.stnAxPrm_D[0].udCreepSpeed_D                   ; U1\G76
      MOVP  K1 FX5SSC_1.stnAxPrm_D[0].uHomingRetry_D                      ; U1\G78
      SET   bOPRParamSetComp
```

##### Unit "degree" setting (axis 1) program (単位degree用設定(軸1)プログラム) (12.3 / original p.630)

```
(146) LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D                  ; U1\G31500.1
      AND   bInputSpeedPositionSwitchingAbsSetReq                         ; X56
      MOVP  K2 FX5SSC_1.stnAxPrm_D[0].uUnit_D                             ; U1\G0
      DMOVP K0 FX5SSC_1.stnAxPrm_D[0].dSoftwareStrokeUpperLimit_D         ; U1\G18
      DMOVP K0 FX5SSC_1.stnAxPrm_D[0].dSoftwareStrokeLowerLimit_D         ; U1\G20
      MOVP  K1 FX5SSC_1.stnAxPrm_D[0].uV_CommandPosition_D                ; U1\G30
      MOVP  K2 FX5SSC_1.stnAxPrm_D[0].uVP_Mode_D                          ; U1\G34
```

- Contact type (read from figure): the FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D contacts of the three rungs on p.630 are drawn as a contact with a vertical mark in the center (unlike the normally open X56), the same shape as the rising edge (↑) contact of the same label on p.631, so they are transcribed as LDP. The arrow itself cannot be seen at the image resolution (要確認; see original p.630). X56 is a normally open contact.
- The outputs of "Setting for basic parameter 1" are MOV (non-pulse) ×2, DMOVP ×2 and SET in the ladder (as printed).
- The label is shown in the ladder as "FX5SSC_1.stSysMntr2_D.b" / "SynchronizationFlag_D" on two lines (line break of the display).

#### Positioning data setting program (位置決めデータ設定プログラム) (12.3 / original p.631)

This program is not required when the data is set by "Positioning Data" using an engineering tool.

```
(0)   LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1
      MOV   K0 M_FX5SSC_SetPositioningData_01A_1.pb_uOpePattern
      MOV   H1 M_FX5SSC_SetPositioningData_01A_1.pb_uCtrlSys
      MOV   K1 M_FX5SSC_SetPositioningData_01A_1.pb_uAccTimeNo
      MOV   K2 M_FX5SSC_SetPositioningData_01A_1.pb_uDecTimeNo
      MOV   K9843 M_FX5SSC_SetPositioningData_01A_1.pb_uMcode
      MOV   K300 M_FX5SSC_SetPositioningData_01A_1.pb_uDwellTime
      DMOV  K18000 M_FX5SSC_SetPositioningData_01A_1.pb_udCmdSpd
      DMOV  K4126 M_FX5SSC_SetPositioningData_01A_1.pb_dPositAdr
      DMOV  K0 M_FX5SSC_SetPositioningData_01A_1.pb_dArcAdr
      MOV   K0 M_FX5SSC_SetPositioningData_01A_1.pb_uInterpolationAxisNo1
      MOV   K0 M_FX5SSC_SetPositioningData_01A_1.pb_uInterpolationAxisNo2
      MOV   K0 M_FX5SSC_SetPositioningData_01A_1.pb_uInterpolationAxisNo3
      SET   bSetPositioningData_bEN
(58)  LD    bSetPositioningData_bEN
      FB    M_FX5SSC_SetPositioningData_01A_1
      // FB title: M_FX5SSC_SetPositioningData_01A_1 (M+FX5SSC_SetPos...) Positioning data setting FB
      // in  B: i_bEN         <- bSetPositioningData_bEN (normally open contact above)
      // in  DUT: i_stModule  <- FX5SSC_1
      // in  UW: i_uAxis      <- K1
      // in  UW: i_uDataNo    <- K1
      // out o_bENO :B        -> bSetPositioningData_bENO (coil)
      // out o_bOK :B         -> bSetPositioningData_bOK (coil)
      // out o_bErr :B        -> bSetPositioningData_bErr (coil)
      // out o_uErrId :UW     -> uSetPositioningData_bErrId
      // public variables shown in the FB: pb_uOpePattern, pb_uCtrlSys, pb_uAccTimeNo, pb_uDecTimeNo, pb_uMcode, pb_uDwellTime, pb_udCmdSpd, pb_dPositAdr, pb_dArcAdr, pb_uInterpolatio..., pb_uInterpolatio..., pb_uInterpolatio...
```

- Contact type (read from figure): bSynchronizationFlag_D at (0) is a rising edge (↑) contact; bSetPositioningData_bEN at (58) is a normally open contact.
- The FB type name in parentheses is truncated in the ladder display ("(M+FX5SSC_SetPos..."), as printed.

#### Block start data setting program (ブロック始動データ設定プログラム) (12.3 / original p.632)

This program is not required when the data is set by "Block Start Data" using an engineering tool.

```
(0)   LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1
      MOVP  H8001 uBlockData[0]
      MOVP  H8002 uBlockData[1]
      MOVP  H8005 uBlockData[2]
      MOVP  H800A uBlockData[3]
      MOVP  H0F uBlockData[4]
      TOP   FX5SSC_1.uIO K22000 uBlockData[0] K5            ; FX5SSC_1.uIO = H1
(50)  LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1
      MOVP  H0 uBlockInstData[0]
      MOVP  H0 uBlockInstData[1]
      MOVP  H0 uBlockInstData[2]
      MOVP  H0 uBlockInstData[3]
      MOVP  H0 uBlockInstData[4]
      TOP   FX5SSC_1.uIO K22050 uBlockInstData[0] K5        ; FX5SSC_1.uIO = H1
```

- Contact type (read from figure): bSynchronizationFlag_D at (0) and (50) are rising edge (↑) contacts.
- In the first operand cell of the TOP instructions, "FX5SSC_1.uIO" is shown with "H1" under it.

#### Servo parameter setting program (サーボパラメータ設定プログラム) (12.3 / original p.632)

This program is not required when the parameter is set by "Servo Parameter" using an engineering tool.

```
(0)   LDP   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1
      TOP   FX5SSC_1.uIO K28403 H1 K1                       ; FX5SSC_1.uIO = H1
      TOP   FX5SSC_1.uIO K28400 K32 K1                      ; FX5SSC_1.uIO = H1
```

- Contact type (read from figure): bSynchronizationFlag_D is a rising edge (↑) contact.

#### Home position return request OFF program (原点復帰要求OFFプログラム) (12.3 / original p.633)

This program is not required when "1: Positioning control is executed." is set in "[Pr.55] Operation setting for incompletion of home position return" by "Home Position Return Detailed Parameters" using an engineering tool.

```
(785) LD    bInputOPRReqFlagOffReq                             ; X0
      PLS   bInputForwardJogStartReq                           ; X16
(812) LD    bInputForwardJogStartReq                           ; X16
      ANI   FX5SSC_1.stnAxCtrl2_D[0].uPositioningStart_D.0     ; U1\G30104.0
      ANI   FX5SSC_1.stnAxMntr_D[0].uStatus_D.E                ; U1\G2417.E
      SET   bOPRReqFlagOffReq_H
(823) LD    bOPRReqFlagOffReq_H
      MPS
      AND   FX5SSC_1.stnAxMntr_D[0].uStatus_D.3                ; U1\G2417.3
      SET   bOPRReqFlagOffReq
      MPP
      RST   bOPRReqFlagOffReq_H
(837) LD    bOPRReqFlagOffReq
      MPS
      MOVP  K1 FX5SSC_1.stnAxCtrl1_D[0].uClearHomingRequestFlag_D   ; U1\G4321
      MPP
      AND=_U K0 FX5SSC_1.stnAxCtrl1_D[0].uClearHomingRequestFlag_D  ; U1\G4321
      RST   bOPRReqFlagOffReq
```

- The PLS output of (785) and the first contact of (812) are shown in the ladder as "bInputForwardJogStartReq" / "X16" (as printed; the global label list defines bOPRReqFlagOffReq_P as a separate label. 要確認).
- (823): after bOPRReqFlagOffReq_H, 2 branches: upper = uStatus_D.3 (normally open) → SET bOPRReqFlagOffReq; lower → RST bOPRReqFlagOffReq_H.
- (837): after bOPRReqFlagOffReq, 2 branches: upper → MOVP K1; lower = comparison "=_U K0 FX5SSC_1.stnAxCtrl1_D[0].uClearHomingRequestFlag_D" → RST bOPRReqFlagOffReq.
- Contact type (read from figure): uPositioningStart_D.0 and uStatus_D.E at (812) are normally closed contacts; the others are normally open.

#### External command function valid setting program (外部指令機能有効設定プログラム) (12.3 / original p.633)

```
(855) LD    bInputExternalCommandValidReq                      ; X1
      MOVP  K1 FX5SSC_1.stnAxCtrl1_D[0].uExternalCommandValid_D ; U1\G4305
(881) LD    bInputExternalCommandInvalidReq                    ; X2
      MOVP  K0 FX5SSC_1.stnAxCtrl1_D[0].uExternalCommandValid_D ; U1\G4305
```

#### PLC READY signal ON program (シーケンサレディ信号ONプログラム) (12.3 / original p.633)

```
(889) LD    FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1
      AND   bBasicParamSetComp
      AND   bOPRParamSetComp
      ANI   bInitializeParameterReq
      ANI   bWriteFlashReq
      OUT   FX5SSC_1.stSysCtrl_D.bPLC_Ready_D                  ; U1\G5950.0
```

- Contact type (read from figure): bSynchronizationFlag_D, bBasicParamSetComp and bOPRParamSetComp are normally open; bInitializeParameterReq and bWriteFlashReq are normally closed.

#### All axis servo ON program (全軸サーボONプログラム) (12.3 / original p.633)

```
(930) LD    bAllAxisServoOnReq                                 ; X57
      AND   FX5SSC_1.stSysCtrl_D.bPLC_Ready_D                  ; U1\G5950.0
      AND   FX5SSC_1.stSysMntr2_D.bSynchronizationFlag_D      ; U1\G31500.1
      OUT   FX5SSC_1.stSysCtrl_D.bAllAxisServoOn_D             ; U1\G5951.0
```

#### Positioning start No. setting program (位置決め始動番号設定プログラム) (12.3 / original p.634-635)

##### Machine home position return (機械原点復帰) (12.3 / original p.634)

```
(961) LD    bInputOPRStartReq                                  ; X3
      MOVP  K9001 uPositioningStartNo
```

##### Fast home position return (高速原点復帰) (12.3 / original p.634)

```
(1005) LD   bInputFastOPRStartReq                              ; X4
      MPS
      ANI   FX5SSC_1.stnAxMntr_D[0].uStatus_D.3                ; U1\G2417.3
      SET   bFastOPRStartReq
      MRD
      MOVP  K9002 uPositioningStartNo
      MPP
      SET   bFastOPRStartReq_H
```

- After X4, 3 branches: upper = uStatus_D.3 (normally closed) → SET bFastOPRStartReq; middle → MOVP K9002 uPositioningStartNo; lower → SET bFastOPRStartReq_H.

##### Positioning with positioning data No.1 (位置決めデータNo.1による位置決め) (12.3 / original p.634)

```
(1037) LD   bInputStartPositioningNoReq                        ; X5
      MOVP  K1 uPositioningStartNo
```

##### Speed-position switching operation (Positioning data No.2) (速度・位置切換え制御(位置決めデータNo.2)) (12.3 / original p.634)

In the ABS mode, new movement amount is not needed to be written.

```
(1071) LD   bInputSpeedPositionSwitchingReq                    ; X6
      MOVP  K2 uPositioningStartNo
(1110) LD   bInputSpeedPositionSwitchingEnableReq              ; X7
      MOVP  K1 FX5SSC_1.stnAxCtrl1_D[0].uEnableVP_Switching_D  ; U1\G4328
(1118) LD   bInputSpeedPositionSwitchingDisableReq             ; X10
      MOVP  K0 FX5SSC_1.stnAxCtrl1_D[0].uEnableVP_Switching_D  ; U1\G4328
(1126) LD   bInputChangeSpeedPositionSwitchingMovementAmount   ; X11
      DMOVP udMovementAmount FX5SSC_1.stnAxCtrl1_D[0].udVP_NewMovementAmount_D ; U1\G4326
```

##### Position-speed switching operation (Positioning data No.3) (位置・速度切換え制御(位置決めデータNo.3)) (12.3 / original p.634)

```
(1136) LD   bInputPositionSpeedSwitchingReq                    ; X40
      MOVP  K3 uPositioningStartNo
(1175) LD   bInputPositionSpeedSwitchingEnableReq              ; X41
      MOVP  K1 FX5SSC_1.stnAxCtrl1_D[0].uEnablePV_Switching_D  ; U1\G4332
(1183) LD   bInputPositionSpeedSwitchingDisableReq             ; X42
      MOVP  K0 FX5SSC_1.stnAxCtrl1_D[0].uEnablePV_Switching_D  ; U1\G4332
(1191) LD   bInputChangePositionSpeedSwitchingSpeedReq         ; X43
      DMOVP udSpeed FX5SSC_1.stnAxCtrl1_D[0].udPV_NewSpeed_D   ; U1\G4330
```

##### High-level positioning control (高度な位置決め制御) (12.3 / original p.634)

```
(1201) LD   bInputStartAdvancedPositioningReq                  ; X12
      MOVP  K7000 uPositioningStartNo
```

##### Fast home position return command and fast home position return command storage OFF (高速原点復帰指令，高速原点復帰指令記憶のOFF) (12.3 / original p.635)

Not required when fast home position return is not used.

```
(1225) LD   bInputOPRStartReq                                  ; X3
      OR    bInputStartPositioningNoReq                        ; X5
      OR    bInputSpeedPositionSwitchingReq                    ; X6
      OR    bInputPositionSpeedSwitchingReq                    ; X40
      OR    bInputStartAdvancedPositioningReq                  ; X12
      OR    bPositioningStartReq
      RST   bFastOPRStartReq
      RST   bFastOPRStartReq_H
```

#### Positioning start program (位置決め始動プログラム) (12.3 / original p.635)

```
(0)   LDP   bInputStartPositioningNoReq                        ; X5
      ANI   bDuringJogInchingOperation
      ANI   bDuringMPGOperation
      LDI   bFastOPRStartReq
      LD    bFastOPRStartReq
      AND   bFastOPRStartReq_H
      ORB
      ANB
      SET   bPositioningStartReq
(24)  LD    bPositioningStartReq
      LD    FX5SSC_1.stnAxMntr_D[0].uStatus_D.F                ; U1\G2417.F
      OR    FX5SSC_1.stnAxMntr_D[0].uStatus_D.D                ; U1\G2417.D
      ANB
      ANI   FX5SSC_1.stSysMntr2_D.bnBusy_D[0]                  ; U1\G31501.0
      RST   bPositioningStartReq
(40)  LD    bPositioningStartReq
      FB    M_FX5SSC_StartPositioning_01A_1
      // FB title: M_FX5SSC_StartPositioning_01A_1 (M+FX5SSC_StartPo...) Positioning start FB
      // in  B: i_bEN         <- bPositioningStartReq (normally open contact above)
      // in  DUT: i_stModule  <- FX5SSC_1
      // in  UW: i_uAxis      <- K1
      // in  UW: i_uStartNo   <- uPositioningStartNo
      // out o_bENO :B        -> bStartPositioning_bENO (coil)
      // out o_bOK :B         -> bStartPositioning_bOK (coil)
      // out o_bErr :B        -> bStartPositioning_bErr (coil)
      // out o_uErrId :UW     -> uStartPositioning_uErrId
```

- Contact type (read from figure): at (0), bInputStartPositioningNoReq (X5) is a rising edge (↑) contact; bDuringJogInchingOperation, bDuringMPGOperation and the upper bFastOPRStartReq are normally closed; the lower bFastOPRStartReq and bFastOPRStartReq_H are normally open. At (24), bnBusy_D[0] is normally closed; the others are normally open.
- (0): after bDuringMPGOperation, a parallel block of "bFastOPRStartReq (normally closed)" and "bFastOPRStartReq (normally open) – bFastOPRStartReq_H (normally open) in series" leads to SET bPositioningStartReq.
- (24): after bPositioningStartReq, "uStatus_D.F (positioning complete)" and "uStatus_D.D (error detection)" in parallel, then the normally closed bnBusy_D[0] → RST bPositioningStartReq.
- The step numbers of the positioning start program start from (0) (as printed).

#### M code OFF program (MコードOFFプログラム) (12.3 / original p.635)

```
(1870) LD   bInputMcodeOffReq                                  ; X14
      AND   FX5SSC_1.stnAxMntr_D[0].uStatus_D.C                ; U1\G2417.C
      MOVP  K1 FX5SSC_1.stnAxCtrl1_D[0].uClear_M_Code_D        ; U1\G4304
```

#### JOG operation setting program (JOG運転設定プログラム) (12.3 / original p.635)

```
(1904) LD   bInputSetJogSpeedReq                               ; X15
      MPS
      DMOVP K10000 udJogOperationSpeed
      MPP
      MOVP  K0 uInchingMovementAmount
```

#### Inching operation setting program (インチング運転設定プログラム) (12.3 / original p.636)

```
(1942) LD   bInputSetInchingMovementAmountReq                  ; X44
      MOVP  K10 uInchingMovementAmount
```

#### JOG operation/inching operation execution program (JOG運転／インチング運転実行プログラム) (12.3 / original p.636)

```
(0)   LD    bInputForwardJogStartReq                           ; X16
      OR    bInputReverseJogStartReq                           ; X17
      AND   FX5SSC_1.stSysMntr2_D.bReady_D                     ; U1\G31500.0
      ANI   FX5SSC_1.stSysMntr2_D.bnBusy_D[0]                  ; U1\G31501.0
      SET   bDuringJogInchingOperation
(13)  LD    bDuringJogInchingOperation
      FB    M_FX5SSC_JOG_01A_1
      // FB title: M_FX5SSC_JOG_01A_1 (M+FX5SSC_JOG_01A) JOG/inching operation FB
      // in  B: i_bEN         <- bDuringJogInchingOperation (normally open contact)
      // in  DUT: i_stModule  <- FX5SSC_1
      // in  UW: i_uAxis      <- K1
      // in  B: i_bFJog       <- LD bInputForwardJogStartReq ; X16 (normally open contact)
      // in  B: i_bRJog       <- LD bInputReverseJogStartReq ; X17 (normally open contact)
      // in  UD: i_udJogSpeed <- udJogOperationSpeed
      // in  UW: i_uInching   <- K0
      // out o_bENO :B        -> bJOG_bENO (coil)
      // out o_bOK :B         -> bJOG_bOK (coil)
      // out o_bErr :B        -> bJOG_bErr (coil)
      // out o_uErrId :UW     -> uJOG_uErrId
(280) LDI   bInputForwardJogStartReq                           ; X16
      ANI   bInputReverseJogStartReq                           ; X17
      RST   bDuringJogInchingOperation
```

#### Manual pulse generator operation program (手動パルサ運転プログラム) (12.3 / original p.636)

```
(0)   LDP   bInputStartMPGReq                                  ; X20
      AND   FX5SSC_1.stSysMntr2_D.bReady_D                     ; U1\G31500.0
      ANI   FX5SSC_1.stSysMntr2_D.bnBusy_D[0]                  ; U1\G31501.0
      SET   bDuringMPGOperation
(13)  LDF   bInputStartMPGReq                                  ; X20
      RST   bDuringMPGOperation
(20)  LD    bDuringMPGOperation
      FB    M_FX5SSC_MPG_01A_1
      // FB title: M_FX5SSC_MPG_01A_1 (M+FX5SSC_MPG_01A) Manual pulse generator OP FB
      // in  B: i_bEN         <- bDuringMPGOperation (normally open contact)
      // in  DUT: i_stModule  <- FX5SSC_1
      // in  UW: i_uAxis      <- K1
      // in  UD: i_udMPGInputMagnification <- K1
      // out o_bENO :B        -> bMPG_bENO (coil)
      // out o_bOK :B         -> bMPG_bOK (coil)
      // out o_bErr :B        -> bMPG_bErr (coil)
      // out o_uErrId :UW     -> uMPG_uErrId
```

- Contact type (read from figure): X20 at (0) is a rising edge (↑) contact, X20 at (13) is a falling edge (↓) contact.

#### Speed change program (速度変更プログラム) (12.3 / original p.637)

```
(0)   LDP   bInputChangeSpeedReq                               ; X22
      ANI   FX5SSC_1.stSysMntr2_D.bnBusy_D[0]                  ; U1\G31501.0
      SET   bChangeSpeedReq
(10)  LD    bChangeSpeed_bOK
      RST   bChangeSpeedReq
(16)  LD    bChangeSpeedReq
      FB    M_FX5SSC_ChangeSpeed_01A_1
      // FB title: M_FX5SSC_ChangeSpeed_01A_1 (M+FX5SSC_Chang...) Speed change FB
      // in  B: i_bEN         <- bChangeSpeedReq (normally open contact)
      // in  DUT: i_stModule  <- FX5SSC_1
      // in  UW: i_uAxis      <- K1
      // in  UD: i_udSpeedChangeValue <- K20000
      // out o_bENO :B        -> bChangeSpeed_bENO (coil)
      // out o_bOK :B         -> bChangeSpeed_bOK (coil)
      // out o_bErr :B        -> bChangeSpeed_bErr (coil)
      // out o_uErrId :UW     -> uChangeSpeed_uErrId
```

#### Override program (オーバーライドプログラム) (12.3 / original p.637)

```
(0)   LD    bInputOverrideReq                                  ; X23
      PLS   bOverrideReq_P
(5)   LD    bOverrideReq_P
      AND   FX5SSC_1.stSysMntr2_D.bnBusy_D[0]                  ; U1\G31501.0
      MOVP  K200 FX5SSC_1.stnAxCtrl1_D[0].uOverride_D          ; U1\G4313
```

- The assigned devices of this rung are printed as "U1¥G31501.0" and "U1¥G4313" (written as U1\G).

#### Acceleration/deceleration time change program (加減速時間変更プログラム) (12.3 / original p.637)

```
(0)   LDI   bInputChangeAccDecTimeDisable                      ; X25
      OUT   bChangeAccDecTime_iEnable
(5)   LD    bInputChangeAccDecTimeReq                          ; X24
      FB    M_FX5SSC_ChangeAccDecTime_01A_1
      // FB title: M_FX5SSC_ChangeAccDecTime_01A_1 (M+FX5SSC_Chang...) Acc./dec. time SV change FB
      // in  B: i_bEN         <- bInputChangeAccDecTimeReq ; X24 (normally open contact)
      // in  DUT: i_stModule  <- FX5SSC_1
      // in  UW: i_uAxis      <- K1
      // in  B: i_bEnable     <- LD bChangeAccDecTime_iEnable (normally open contact)
      // in  UD: i_udNewAccelerationTime <- K2000
      // in  UD: i_udNewDecelerationTime <- K0
      // out o_bENO :B        -> bChangeAccDecTime_bENO (coil)
      // out o_bOK :B         -> bChangeAccDecTime_bOK (coil)
      // out o_bErr :B        -> bChangeAccDecTime_bErr (coil)
      // out o_uErrId :UW     -> uChangeAccDecTime_uErrId
```

#### Torque change program (トルク変更プログラム) (12.3 / original p.638)

```
(3493) LD   bInputChangeTorqueReq                              ; X26
      PLS   bChangeTorqueReq
(3516) LD   bChangeTorqueReq
      AND   FX5SSC_1.stSysMntr2_D.bnBusy_D[0]                  ; U1\G31501.0
      MOV   K1000 FX5SSC_1.stnAxCtrl1_D[0].uForwardNewTorque_D ; U1\G4325
```

#### Step operation program (ステップ運転プログラム) (12.3 / original p.638)

```
(3528) LD   bInputStepOperationReq                             ; X27
      PLS   bStepOperationReq_P
(3554) LD   bStepOperationReq_P
      ANI   FX5SSC_1.stnAxCtrl2_D[0].uPositioningStart_D.0     ; U1\G30104.0
      ANI   FX5SSC_1.stnAxMntr_D[0].uStatus_D.E                ; U1\G2417.E
      MPS
      MOV   K1 FX5SSC_1.stnAxCtrl1_D[0].uStepMode_D            ; U1\G4344
      MPP
      MOV   K1 FX5SSC_1.stnAxCtrl1_D[0].uStepValid_D           ; U1\G4345
(3575) LD   bInputStepStartInformationReq                      ; X46
      MOVP  K1 FX5SSC_1.stnAxCtrl1_D[0].uStepStartInformation_D ; U1\G4346
```

- Contact type (read from figure): uPositioningStart_D.0 and uStatus_D.E at (3554) are normally closed contacts.

#### Skip program (スキッププログラム) (12.3 / original p.638)

```
(3583) LD   bInputSkipReq                                      ; X30
      PLS   bSkipReq_P
(3608) LD   bSkipReq_P
      AND   FX5SSC_1.stSysMntr2_D.bnBusy_D[0]                  ; U1\G31501.0
      SET   bSkipReq
(3617) LD   bSkipReq
      MPS
      MOVP  K1 FX5SSC_1.stnAxCtrl1_D[0].uSkip_D                ; U1\G4347
      MPP
      AND=_U FX5SSC_1.stnAxCtrl1_D[0].uSkip_D K0               ; U1\G4347
      RST   bSkipReq
```

- (3617): the comparison instruction is "=_U FX5SSC_1.stnAxCtrl1_D[0].uSkip_D K0" (label first, K0 second, as printed).

#### Teaching program (ティーチングプログラム) (12.3 / original p.638)

```
(3635) LD   bInputTeachingReq                                  ; X31
      PLS   bTeachingReq_P
(3660) LD   bTeachingReq_P
      ANI   FX5SSC_1.stSysMntr2_D.bnBusy_D[0]                  ; U1\G31501.0
      SET   bTeachingReq
(3669) LD   bTeachingReq
      MPS
      MOVP  K0 FX5SSC_1.stnAxCtrl1_D[0].uTeachingDataSelection_D     ; U1\G4348
      MRD
      MOVP  K1 FX5SSC_1.stnAxCtrl1_D[0].uTeachingPositioningDataNo_D ; U1\G4349
      MPP
      AND=_U FX5SSC_1.stnAxCtrl1_D[0].uTeachingPositioningDataNo_D K0 ; U1\G4349
      RST   bTeachingReq
```

- Contact type (read from figure): bnBusy_D[0] at (3660) is a normally closed contact.

#### Continuous operation interrupt program (連続運転中断プログラム) (12.3 / original p.639)

```
(3693) LD   bInputStopContinuousOperationReq                   ; X32
      PLS   bStopContinuousOperationReq_P
(3720) LD   bStopContinuousOperationReq_P
      AND   FX5SSC_1.stSysMntr2_D.bnBusy_D[0]                  ; U1\G31501.0
      MOV   K1 FX5SSC_1.stnAxCtrl1_D[0].uInterruptOperation_D  ; U1\G4320
```

#### Target position change program (目標位置変更プログラム) (12.3 / original p.639)

```
(0)   LDP   bInputTargetPositionChangeReq                      ; X45
      AND   FX5SSC_1.stSysMntr2_D.bnBusy_D[0]                  ; U1\G31501.0
      SET   bTargetPositionChangeReq
(10)  LD    bTargetPositionChangeReq
      FB    M_FX5SSC_ChangePosition_01A_1
      // FB title: M_FX5SSC_ChangePosition_01A_1 (M+FX5SSC_Chang...) Target position change FB
      // in  B: i_bEN         <- bTargetPositionChangeReq (normally open contact)
      // in  DUT: i_stModule  <- FX5SSC_1
      // in  UW: i_uAxis      <- K1
      // in  D: i_dTargetNewPosition <- K3000
      // in  UD: i_udTargetNewSpeed  <- K1000000
      // out o_bENO :B        -> bChangeAccDecTime_bENO (coil)
      // out o_bOK :B         -> bChangeAccDecTime_bOK (coil)
      // out o_bErr :B        -> bChangeAccDecTime_bErr (coil)
      // out o_uErrId :UW     -> uChangeAccDecTime_uErrId
(199) LD    bChangePosition_bOK
      RST   bTargetPositionChangeReq
```

- In the original figure, the output labels of this FB are printed as bChangeAccDecTime_bENO / bChangeAccDecTime_bOK / bChangeAccDecTime_bErr / uChangeAccDecTime_uErrId, while the contact at step (199) is printed as bChangePosition_bOK (transcribed as printed on p.639; 要確認).

#### Restart program (再始動プログラム) (12.3 / original p.639)

```
(0)   LDP   bInputRestartReq                                   ; X33
      SET   bRestartReq
(7)   LD    bRestart_bOK
      RST   bRestartReq
(13)  LD    bRestartReq
      FB    M_FX5SSC_Restart_01A_1
      // FB title: M_FX5SSC_Restart_01A_1 (M+FX5SSC_Restart...) Restart FB
      // in  B: i_bEN         <- bRestartReq (normally open contact)
      // in  DUT: i_stModule  <- FX5SSC_1
      // in  UW: i_uAxis      <- K1
      // out o_bENO :B        -> bRestart_bENO (coil)
      // out o_bOK :B         -> bRestart_bOK (coil)
      // out o_bErr :B        -> bRestart_bErr (coil)
      // out o_uErrId :UW     -> uRestart_uErrId
```

#### Parameter initialization program (パラメータ初期化プログラム) (12.3 / original p.640)

```
(4417) LDP  bInputInitializeParameterReq                       ; X34
      SET   bInitializeParameterReq
(4446) LD   bInitializeParameter_bOK
      RST   bInitializeParameterReq
(4452) LD   bInitializeParameterReq
      FB    M_FX5SSC_InitializeParameter_00A_1
      // FB title: M_FX5SSC_InitializeParameter_00A_1 (M+FX5SSC_InitializeParameter_00A) Parameter Initialization FB
      // in  B: i_bEN         <- bInitializeParameterReq (normally open contact)
      // in  DUT: i_stModule  <- FX5SSC_1
      // out o_bENO:B         -> bInitializeParameter_bENO (coil)
      // out o_bOK:B          -> bInitializeParameter_bOK (coil)
      // out o_bErr:B         -> bInitializeParameter_bErr (coil)
      // out o_uErrId:UW      -> uInitializeParameter_uErrId
```

- Contact type (read from figure): X34 at (4417) is drawn as a contact with a vertical mark in the center (same appearance as the bSynchronizationFlag_D contacts on p.630) and is transcribed as LDP; the arrow itself cannot be seen at the image resolution (要確認; see original p.640).
- The step numbers of this program in the English original are (4417), (4446), (4452) (as printed). The FB instance name in the title is displayed as "M FX5SSC InitializeParameter 00A 1" with the underscores not visible at the image resolution.

#### Flash ROM write program (フラッシュROM書込みプログラム) (12.3 / original p.640)

```
(0)   LDP   bInputWriteFlashReq                                ; X35
      SET   bWriteFlashReq
(7)   LD    bInitializeParameter_bOK
      RST   bWriteFlashReq
(13)  LD    bWriteFlashReq
      FB    M_FX5SSC_WriteFlash_00A_1
      // FB title: M_FX5SSC_WriteFlash_00A_1 (M+FX5SSC_WriteFlash_00A) Flash ROM writing FB
      // in  B: i_bEN         <- bWriteFlashReq (normally open contact)
      // in  DUT: i_stModule  <- FX5SSC_1
      // out o_bENO :B        -> bWriteFlash_bENO (coil)
      // out o_bOK :B         -> bWriteFlash_bOK (coil)
      // out o_bErr :B        -> bWriteFlash_bErr (coil)
      // out o_uErrId :UW     -> uWriteFlash_uErrId
```

- The contact at step (7) is printed as bInitializeParameter_bOK in the original figure on p.640 (not bWriteFlash_bOK; transcribed as printed. 要確認).

#### Error reset program (エラーリセットプログラム) (12.3 / original p.641)

```
(0)   LD    FX5SSC_1.stnAxMntr_D[0].uStatus_D.D                ; U1\G2417.D
      OR    FX5SSC_1.stnAxMntr_D[0].uStatus_D.9                ; U1\G2417.9
      OUT   bErrReadReq
(9)   LD    bInputErrResetReq                                  ; X36
      RST   bErrResetReq
(14)  LD    bErrReadReq
      FB    M_FX5SSC_OperateError_01A_1
      // FB title: M_FX5SSC_OperateError_01A_1 (M+FX5SSC_Operat...) Error operation FB
      // in  B: i_bEN         <- bErrReadReq (normally open contact)
      // in  DUT: i_stModule  <- FX5SSC_1
      // in  UW: i_uAxis      <- K1
      // in  B: i_bErrReset   <- LD bErrResetReq (normally open contact)
      // out o_bENO :B        -> bOperateError_bENO (coil)
      // out o_bOK :B         -> bOperateError_bOK (coil)
      // out o_bModuleErr :B  -> bOperateError_bModuleErr (coil)
      // out o_uModuleErrId :UW  -> uOperateError_bModuleErrId
      // out o_bModuleWarn :B -> bOperateError_bModuleWarn (coil)
      // out o_uModuleWarnId :UW -> uOperateError_bModuleWarnId
      // out o_bErr :B        -> bOperateError_bErr (coil)
      // out o_uErrId :UW     -> uOperateError_uErrId
```

- Step (9) is printed on p.641 as X36 (normally open contact) → RST bErrResetReq (transcribed as printed).

#### Axis stop program (軸停止プログラム) (12.3 / original p.641)

```
(5100) LD   bInputStopReq                                      ; X37
      PLS   bStopReq_P
(5121) LD   bStopReq_P
      SET   FX5SSC_1.stnAxCtrl2_D[0].uStopAxis_D.0             ; U1\G30100.0
(5127) LDI  bInputStopReq                                      ; X37
      RST   FX5SSC_1.stnAxCtrl2_D[0].uStopAxis_D.0             ; U1\G30100.0
```

## 12.4 Positioning Program Examples (For Using Buffer Memory) (位置決めプログラム例(バッファメモリ使用時)) (12.4 / original p.642-675)

### List of devices used (使用するデバイス一覧) (12.4 / original p.642-649)

In the program examples, the devices to be used are assigned as follows.
In addition, change the module access device, external inputs, internal relays, data resisters, and timers according to the system used.

#### Buffer memory address of Simple Motion module, external inputs, internal relay (シンプルモーションユニットのバッファメモリアドレス，外部入力，内部リレー) (12.4 / original p.642-644)

| Device name | Axis 1 | Axis 2 | Axis 3 | Axis 4 | Application | Description at device ON |
|---|---|---|---|---|---|---|
| Buffer memory address of Simple Motion module | U1\G31500.0 | U1\G31500.0 | U1\G31500.0 | U1\G31500.0 | READY signal | READY |
| Buffer memory address of Simple Motion module | U1\G31500.1 | U1\G31500.1 | U1\G31500.1 | U1\G31500.1 | Synchronization flag | Buffer memory accessible |
| Buffer memory address of Simple Motion module | U1\G2417.C | — | — | — | M code ON signal | M code outputting |
| Buffer memory address of Simple Motion module | U1\G2417.D | — | — | — | Error detection signal | Error detection |
| Buffer memory address of Simple Motion module | U1\G31501.0 | — | — | — | BUSY signal | BUSY (operating) |
| Buffer memory address of Simple Motion module | U1\G2417.E | — | — | — | Start complete signal | Start completed |
| Buffer memory address of Simple Motion module | U1\G2417.F | — | — | — | Positioning complete signal | Positioning completed |
| Buffer memory address of Simple Motion module | U1\G5950 | U1\G5950 | U1\G5950 | U1\G5950 | PLC READY signal | CPU module preparation completed |
| Buffer memory address of Simple Motion module | U1\G5951 | U1\G5951 | U1\G5951 | U1\G5951 | All axis servo ON signal | All axis servo ON |
| Buffer memory address of Simple Motion module | U1\G30100 | — | — | — | Axis stop signal | Requesting stop |
| Buffer memory address of Simple Motion module | U1\G30101 | — | — | — | Forward run JOG start signal | Starting forward run JOG |
| Buffer memory address of Simple Motion module | U1\G30102 | — | — | — | Reverse run JOG start signal | Starting reverse run JOG |
| Buffer memory address of Simple Motion module | U1\G30103 | — | — | — | Execution prohibition request | Execution prohibition |
| Buffer memory address of Simple Motion module | U1\G30104 | — | — | — | Positioning start signal | Requesting start |
| External input (command) | X0 | — | — | — | Home position return request OFF command | Commanding home position return request OFF |
| External input (command) | X1 | — | — | — | External command valid command | Commanding external command valid setting |
| External input (command) | X2 | — | — | — | External command invalid command | Commanding external command invalid |
| External input (command) | X3 | — | — | — | Machine home position return command | Commanding machine home position return |
| External input (command) | X4 | — | — | — | Fast home position return command | Commanding fast home position return |
| External input (command) | X5 | — | — | — | Positioning start command | Commanding positioning start |
| External input (command) | X6 | — | — | — | Speed-position switching operation command | Commanding speed-position switching operation |
| External input (command) | X7 | — | — | — | Speed-position switching enable command | Commanding speed-position switching enable |
| External input (command) | X10 | — | — | — | Speed-position switching prohibit command | Commanding speed-position switching prohibit |
| External input (command) | X11 | — | — | — | Movement amount change command | Commanding movement amount change |
| External input (command) | X12 | — | — | — | High-level positioning control start command | Commanding high-level positioning control start |
| External input (command) | X14 | — | — | — | M code OFF command | Commanding M code OFF |
| External input (command) | X15 | — | — | — | JOG operation speed setting command | Commanding JOG operation speed setting |
| External input (command) | X16 | — | — | — | Forward run JOG/inching command | Commanding forward run JOG/inching operation |
| External input (command) | X17 | — | — | — | Reverse run JOG/inching command | Commanding reverse run JOG/inching operation |
| External input (command) | X20 | — | — | — | Manual pulse generator operation enable command | Commanding manual pulse generator operation enable |
| External input (command) | X21 | — | — | — | Manual pulse generator operation disable command | Commanding manual pulse generator operation disable |
| External input (command) | X22 | — | — | — | Speed change command | Commanding speed change |
| External input (command) | X23 | — | — | — | Override command | Commanding override |
| External input (command) | X24 | — | — | — | Acceleration/deceleration time change command | Commanding acceleration/deceleration time change |
| External input (command) | X25 | — | — | — | Acceleration/deceleration time change disable command | Commanding acceleration/deceleration time change disable |
| External input (command) | X26 | — | — | — | Torque change command | Commanding torque change |
| External input (command) | X27 | — | — | — | Step operation command | Commanding step operation |
| External input (command) | X30 | — | — | — | Skip command | Commanding skip |
| External input (command) | X31 | — | — | — | Teaching command | Commanding teaching |
| External input (command) | X32 | — | — | — | Continuous operation interrupt command | Commanding continuous operation interrupt |
| External input (command) | X33 | — | — | — | Restart command | Commanding restart |
| External input (command) | X34 | X34 | X34 | X34 | Parameter initialization command | Commanding parameter initialization |
| External input (command) | X35 | X35 | X35 | X35 | Flash ROM write command | Commanding flash ROM write |
| External input (command) | X36 | — | — | — | Error reset command | Commanding error reset |
| External input (command) | X37 | — | — | — | Stop command | Commanding stop |
| External input (command) | X40 | — | — | — | Position-speed switching operation command | Position-speed switching operation command |
| External input (command) | X41 | — | — | — | Position-speed switching enable command | Position-speed switching enable command |
| External input (command) | X42 | — | — | — | Position-speed switching prohibit command | Position-speed switching prohibit command |
| External input (command) | X43 | — | — | — | Speed change command | Speed change command |
| External input (command) | X44 | — | — | — | Inching movement amount setting command | Inching movement amount setting command |
| External input (command) | X45 | — | — | — | Target position change command | Target position change command |
| External input (command) | X46 | — | — | — | Step start information command | Step start information command |
| External input (command) | X47 | — | — | — | Positioning start command K10 | Positioning start command K10 |
| External input (command) | X50 | — | — | — | Override initialization value command | Override initialization value command |
| External input (command) | X53 | — | — | — | PLC READY signal ON | PLC READY signal ON |
| External input (command) | X54 | — | — | — | Error reset clear command | Error reset clear command |
| External input (command) | X55 | — | — | — | For Unit (degree) | For Unit (degree) |
| External input (command) | X56 | — | — | — | Positioning start signal command | Commanding positioning start |
| External input (command) | X57 | — | — | — | All axis servo ON command | All axis servo ON command |
| Internal relay | M0 | — | — | — | Home position return request OFF command | Commanding home position return request OFF |
| Internal relay | M1 | — | — | — | Home position return request OFF command pulse | Home position return request OFF commanded |
| Internal relay | M2 | — | — | — | Home position return request OFF command storage | Home position return request OFF command held |
| Internal relay | M3 | — | — | — | Fast home position return command | Commanding fast home position return |
| Internal relay | M4 | — | — | — | Fast home position return command storage | Fast home position return command held |
| Internal relay | M5 | — | — | — | Positioning start command pulse | Positioning start commanded |
| Internal relay | M6 | — | — | — | Positioning start command storage | Positioning start command held |
| Internal relay | M7 | — | — | — | JOG/inching operation termination | JOG/inching operation termination |
| Internal relay | M8 | — | — | — | Manual pulse generator operation enable command | Commanding manual pulse generator operation enable |
| Internal relay | M9 | — | — | — | Manual pulse generator operating flag | Manual pulse generator operating flag |
| Internal relay | M10 | — | — | — | Manual pulse generator operation disable command | Commanding manual pulse generator operation disable |
| Internal relay | M11 | — | — | — | Speed change command pulse | Speed change commanded |
| Internal relay | M12 | — | — | — | Speed change command storage | Speed change command held |
| Internal relay | M13 | — | — | — | Override command | Requesting override |
| Internal relay | M14 | — | — | — | Acceleration/deceleration time change command | Requesting acceleration/deceleration time change |
| Internal relay | M15 | — | — | — | Torque change command | Requesting torque change |
| Internal relay | M16 | — | — | — | Step operation command pulse | Step operation commanded |
| Internal relay | M17 | — | — | — | Skip command pulse | Skip commanded |
| Internal relay | M18 | — | — | — | Skip command storage | Skip command held |
| Internal relay | M19 | — | — | — | Teaching command pulse | Teaching commanded |
| Internal relay | M20 | — | — | — | Teaching command storage | Teaching command held |
| Internal relay | M21 | — | — | — | Continuous operation interrupt command | Requesting continuous operation interrupt |
| Internal relay | M22 | — | — | — | Restart command | Requesting restart |
| Internal relay | M23 | — | — | — | Restart command storage | Restart command held |
| Internal relay | M24 | — | — | — | Parameter initialization command pulse | Parameter initialization commanded |
| Internal relay | M25 | M25 | M25 | M25 | Parameter initialization command storage | Parameter initialization command held |
| Internal relay | M26 | M26 | M26 | M26 | Flash ROM write command pulse | Flash ROM write commanded |
| Internal relay | M27 | M27 | M27 | M27 | Flash ROM write command storage | Flash ROM write command held |
| Internal relay | M28 | — | — | — | Error reset | Error reset completed |
| Internal relay | M29 | — | — | — | Stop command pulse | Stop commanded |
| Internal relay | M30 | — | — | — | Target position change command pulse | Target position change commanded |
| Internal relay | M31 | — | — | — | Target position change command storage | Target position change command held |
| Internal relay | M40 | — | — | — | Override initialization value command | Override initialization value |
| Internal relay | M50 | — | — | — | Parameter setting complete device | Parameter setting completed |

*In the original, the "Device name" column (Buffer memory address of Simple Motion module / External input (command) / Internal relay) is a vertically merged cell for each category. Expanded to each row.
*In the original, the Axis 2 to Axis 4 columns of "Device" are merged vertically and horizontally into one cell showing "—" for each of the ranges U1\G2417.C to U1\G2417.F, U1\G30100 to U1\G30104, X0 to X33, X36 to X57, M0 to M24, and M28 to M50. Expanded to each row and column.
*In the original, the rows U1\G31500.0, U1\G31500.1, U1\G5950, U1\G5951, X34, X35, M25, M26 and M27 have the device in one cell merged over Axis 1 to Axis 4 (one device in one cell). The same value is expanded to each of the Axis 1 to Axis 4 columns.
*In the original, the table spans the 3 pages p.642-644 (the header row is repeated on p.643 and p.644).

#### Data registers and timers (データレジスタ，タイマ) (12.4 / original p.645-649)

| Device name | Axis 1 | Axis 2 | Axis 3 | Axis 4 | Application | Storage details |
|---|---|---|---|---|---|---|
| Data register | D0 | — | — | — | Home position return request flag | [Md.31] Status: b3 |
| Data register | D1 | — | — | — | Speed (low-order 16 bits) | [Cd.25] Position-speed switching control speed change register |
| Data register | D2 | — | — | — | Speed (high-order 16 bits) | [Cd.25] Position-speed switching control speed change register |
| Data register | D3 | — | — | — | Movement amount (low-order 16 bits) | [Cd.23] Speed-position switching control movement amount change register |
| Data register | D4 | — | — | — | Movement amount (high-order 16 bits) | [Cd.23] Speed-position switching control movement amount change register |
| Data register | D5 | — | — | — | Inching movement amount | [Cd.16] Inching movement amount |
| Data register | D6 | — | — | — | JOG operation speed (low-order 16 bits) | [Cd.17] JOG speed |
| Data register | D7 | — | — | — | JOG operation speed (high-order 16 bits) | [Cd.17] JOG speed |
| Data register | D8 | — | — | — | Manual pulse generator 1 pulse input magnification (low-order) | [Cd.20] Manual pulse generator 1 pulse input magnification |
| Data register | D9 | — | — | — | Manual pulse generator 1 pulse input magnification (high-order) | [Cd.20] Manual pulse generator 1 pulse input magnification |
| Data register | D10 | — | — | — | Manual pulse generator operation enable | [Cd.21] Manual pulse generator enable flag |
| Data register | D11 | — | — | — | Speed change value (low-order 16 bits) | [Cd.14] New speed value |
| Data register | D12 | — | — | — | Speed change value (high-order 16 bits) | [Cd.14] New speed value |
| Data register | D13 | — | — | — | Speed change request | [Cd.15] Speed change request |
| Data register | D14 | — | — | — | Override value | [Cd.13] Positioning operation speed override |
| Data register | D15 | — | — | — | Acceleration time setting (low-order 16 bits) | [Cd.10] New acceleration time value |
| Data register | D16 | — | — | — | Acceleration time setting (high-order 16 bits) | [Cd.10] New acceleration time value |
| Data register | D17 | — | — | — | Deceleration time setting (low-order 16 bits) | [Cd.11] New deceleration time value |
| Data register | D18 | — | — | — | Deceleration time setting (high-order 16 bits) | [Cd.11] New deceleration time value |
| Data register | D19 | — | — | — | Acceleration/deceleration time change enable | [Cd.12] Acceleration/deceleration time change during speed change, enable/disable selection |
| Data register | D20 | — | — | — | Step mode | [Cd.34] Step mode |
| Data register | D21 | — | — | — | Step valid flag | [Cd.35] Step valid flag |
| Data register | D22 | — | — | — | Step start information | — |
| Data register | D23 | — | — | — | Target position (low-order 16 bits) | [Cd.27] Target position change value (New address) |
| Data register | D24 | — | — | — | Target position (high-order 16 bits) | [Cd.27] Target position change value (New address) |
| Data register | D25 | — | — | — | Target speed (low-order 16 bits) | [Cd.28] Target position change value (New speed) |
| Data register | D26 | — | — | — | Target speed (high-order 16 bits) | [Cd.28] Target position change value (New speed) |
| Data register | D27 | — | — | — | Target position change request | [Cd.29] Target position change request flag |
| Data register | D31 | — | — | — | Completion status | — |
| Data register | D32 | — | — | — | Start No. | — |
| Data register | D34 | — | — | — | Completion status | — |
| Data register | D35 | — | — | — | Teaching data | — |
| Data register | D36 | — | — | — | Positioning data No. | — |
| Data register | D38 | — | — | — | Completion status | — |
| Data register | D40 | — | — | — | Completion status | — |
| Data register | D50 | — | — | — | Unit setting | [Pr.1] Unit setting |
| Data register | D51 | — | — | — | Unit magnification | [Pr.4] Unit magnification (AM) |
| Data register | D52 | — | — | — | Number of pulses per rotation (low-order 16 bits) | [Pr.2] Number of pulses per rotation (AP) |
| Data register | D53 | — | — | — | Number of pulses per rotation (high-order 16 bits) | [Pr.2] Number of pulses per rotation (AP) |
| Data register | D54 | — | — | — | Movement amount per rotation (low-order 16 bits) | [Pr.3] Movement amount per rotation (AL) |
| Data register | D55 | — | — | — | Movement amount per rotation (high-order 16 bits) | [Pr.3] Movement amount per rotation (AL) |
| Data register | D56 | — | — | — | Bias speed at start (low-order 16 bits) | [Pr.7] Bias speed at start |
| Data register | D57 | — | — | — | Bias speed at start (high-order 16 bits) | [Pr.7] Bias speed at start |
| Data register | D68 | — | — | — | Block start data (Block 0) / Point 1 (shape, start No.) | [Da.11] Shape<br>[Da.12] Start data No.<br>[Da.13] Special start instruction<br>[Da.14] Parameter |
| Data register | D69 | — | — | — | Block start data (Block 0) / Point 2 (shape, start No.) | [Da.11] Shape<br>[Da.12] Start data No.<br>[Da.13] Special start instruction<br>[Da.14] Parameter |
| Data register | D70 | — | — | — | Block start data (Block 0) / Point 3 (shape, start No.) | [Da.11] Shape<br>[Da.12] Start data No.<br>[Da.13] Special start instruction<br>[Da.14] Parameter |
| Data register | D71 | — | — | — | Block start data (Block 0) / Point 4 (shape, start No.) | [Da.11] Shape<br>[Da.12] Start data No.<br>[Da.13] Special start instruction<br>[Da.14] Parameter |
| Data register | D72 | — | — | — | Block start data (Block 0) / Point 5 (shape, start No.) | [Da.11] Shape<br>[Da.12] Start data No.<br>[Da.13] Special start instruction<br>[Da.14] Parameter |
| Data register | D73 | — | — | — | Block start data (Block 0) / Point 1 (special start instruction) | [Da.11] Shape<br>[Da.12] Start data No.<br>[Da.13] Special start instruction<br>[Da.14] Parameter |
| Data register | D74 | — | — | — | Block start data (Block 0) / Point 2 (special start instruction) | [Da.11] Shape<br>[Da.12] Start data No.<br>[Da.13] Special start instruction<br>[Da.14] Parameter |
| Data register | D75 | — | — | — | Block start data (Block 0) / Point 3 (special start instruction) | [Da.11] Shape<br>[Da.12] Start data No.<br>[Da.13] Special start instruction<br>[Da.14] Parameter |
| Data register | D76 | — | — | — | Block start data (Block 0) / Point 4 (special start instruction) | [Da.11] Shape<br>[Da.12] Start data No.<br>[Da.13] Special start instruction<br>[Da.14] Parameter |
| Data register | D77 | — | — | — | Block start data (Block 0) / Point 5 (special start instruction) | [Da.11] Shape<br>[Da.12] Start data No.<br>[Da.13] Special start instruction<br>[Da.14] Parameter |
| Data register | D78 | — | — | — | Torque change value | — |
| Data register | D79 | — | — | — | Error | [Md.23] Axis error No. |
| Data register | D80 | — | — | — | Servo series | [Pr.100] Servo series |
| Data register | D81 | — | — | — | Absolute position system valid/invalid | For MR-J4(W)-B:<br>Absolute position detection system (PA03)<br>For MR-J5(W)-B:<br>Absolute position detection system selection (PA03.0) |
| Data register | D85 | — | — | — | Home position return method | [Pr.43] Home position return method |
| Data register | D100 | — | — | — | Positioning identifier | Data No.1<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D101 | — | — | — | M code | Data No.1<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D102 | — | — | — | Dwell time | Data No.1<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D103 | — | — | — | Dummy | Data No.1<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D104 | — | — | — | Command speed (low-order 16 bits) | Data No.1<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D105 | — | — | — | Command speed (high-order 16 bits) | Data No.1<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D106 | — | — | — | Positioning address (low-order 16 bits) | Data No.1<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D107 | — | — | — | Positioning address (high-order 16 bits) | Data No.1<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D108 | — | — | — | Arc address (low-order 16 bits) | Data No.1<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D109 | — | — | — | Arc address (high-order 16 bits) | Data No.1<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D110 | — | — | — | Positioning identifier | Data No.2<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D111 | — | — | — | M code | Data No.2<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D112 | — | — | — | Dwell time | Data No.2<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D113 | — | — | — | Dummy | Data No.2<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D114 | — | — | — | Command speed (low-order 16 bits) | Data No.2<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D115 | — | — | — | Command speed (high-order 16 bits) | Data No.2<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D116 | — | — | — | Positioning address (low-order 16 bits) | Data No.2<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D117 | — | — | — | Positioning address (high-order 16 bits) | Data No.2<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D118 | — | — | — | Arc address (low-order 16 bits) | Data No.2<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D119 | — | — | — | Arc address (high-order 16 bits) | Data No.2<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D120 | — | — | — | Positioning identifier | Data No.3<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D121 | — | — | — | M code | Data No.3<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D122 | — | — | — | Dwell time | Data No.3<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D123 | — | — | — | Dummy | Data No.3<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D124 | — | — | — | Command speed (low-order 16 bits) | Data No.3<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D125 | — | — | — | Command speed (high-order 16 bits) | Data No.3<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D126 | — | — | — | Positioning address (low-order 16 bits) | Data No.3<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D127 | — | — | — | Positioning address (high-order 16 bits) | Data No.3<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D128 | — | — | — | Arc address (low-order 16 bits) | Data No.3<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D129 | — | — | — | Arc address (high-order 16 bits) | Data No.3<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D130 | — | — | — | Positioning identifier | Data No.4<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D131 | — | — | — | M code | Data No.4<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D132 | — | — | — | Dwell time | Data No.4<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D133 | — | — | — | Dummy | Data No.4<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D134 | — | — | — | Command speed (low-order 16 bits) | Data No.4<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D135 | — | — | — | Command speed (high-order 16 bits) | Data No.4<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D136 | — | — | — | Positioning address (low-order 16 bits) | Data No.4<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D137 | — | — | — | Positioning address (high-order 16 bits) | Data No.4<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D138 | — | — | — | Arc address (low-order 16 bits) | Data No.4<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D139 | — | — | — | Arc address (high-order 16 bits) | Data No.4<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D140 | — | — | — | Positioning identifier | Data No.5<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D141 | — | — | — | M code | Data No.5<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D142 | — | — | — | Dwell time | Data No.5<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D143 | — | — | — | Dummy | Data No.5<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D144 | — | — | — | Command speed (low-order 16 bits) | Data No.5<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D145 | — | — | — | Command speed (high-order 16 bits) | Data No.5<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D146 | — | — | — | Positioning address (low-order 16 bits) | Data No.5<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D147 | — | — | — | Positioning address (high-order 16 bits) | Data No.5<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D148 | — | — | — | Arc address (low-order 16 bits) | Data No.5<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D149 | — | — | — | Arc address (high-order 16 bits) | Data No.5<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D150 | — | — | — | Positioning identifier | Data No.6<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D151 | — | — | — | M code | Data No.6<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D152 | — | — | — | Dwell time | Data No.6<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D153 | — | — | — | Dummy | Data No.6<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D154 | — | — | — | Command speed (low-order 16 bits) | Data No.6<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D155 | — | — | — | Command speed (high-order 16 bits) | Data No.6<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D156 | — | — | — | Positioning address (low-order 16 bits) | Data No.6<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D157 | — | — | — | Positioning address (high-order 16 bits) | Data No.6<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D158 | — | — | — | Arc address (low-order 16 bits) | Data No.6<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D159 | — | — | — | Arc address (high-order 16 bits) | Data No.6<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D190 | — | — | — | Positioning identifier | Data No.10<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D191 | — | — | — | M code | Data No.10<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D192 | — | — | — | Dwell time | Data No.10<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D193 | — | — | — | Dummy | Data No.10<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D194 | — | — | — | Command speed (low-order 16 bits) | Data No.10<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D195 | — | — | — | Command speed (high-order 16 bits) | Data No.10<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D196 | — | — | — | Positioning address (low-order 16 bits) | Data No.10<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D197 | — | — | — | Positioning address (high-order 16 bits) | Data No.10<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D198 | — | — | — | Arc address (low-order 16 bits) | Data No.10<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D199 | — | — | — | Arc address (high-order 16 bits) | Data No.10<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D200 | — | — | — | Positioning identifier | Data No.11<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D201 | — | — | — | M code | Data No.11<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D202 | — | — | — | Dwell time | Data No.11<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D203 | — | — | — | Dummy | Data No.11<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D204 | — | — | — | Command speed (low-order 16 bits) | Data No.11<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D205 | — | — | — | Command speed (high-order 16 bits) | Data No.11<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D206 | — | — | — | Positioning address (low-order 16 bits) | Data No.11<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D207 | — | — | — | Positioning address (high-order 16 bits) | Data No.11<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D208 | — | — | — | Arc address (low-order 16 bits) | Data No.11<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D209 | — | — | — | Arc address (high-order 16 bits) | Data No.11<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D240 | — | — | — | Positioning identifier | Data No.15<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D241 | — | — | — | M code | Data No.15<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D242 | — | — | — | Dwell time | Data No.15<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D243 | — | — | — | Dummy | Data No.15<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D244 | — | — | — | Command speed (low-order 16 bits) | Data No.15<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D245 | — | — | — | Command speed (high-order 16 bits) | Data No.15<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D246 | — | — | — | Positioning address (low-order 16 bits) | Data No.15<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D247 | — | — | — | Positioning address (high-order 16 bits) | Data No.15<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D248 | — | — | — | Arc address (low-order 16 bits) | Data No.15<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Data register | D249 | — | — | — | Arc address (high-order 16 bits) | Data No.15<br>[Da.1] Operation pattern<br>[Da.2] Control method<br>[Da.3] Acceleration time No.<br>[Da.4] Deceleration time No.<br>[Da.20] to [Da.22] Axis to be interpolated<br>[Da.6] Positioning address/movement amount<br>[Da.7] Arc address<br>[Da.8] Command speed<br>[Da.9] Dwell time/JUMP destination positioning data No.<br>[Da.10] M code/Condition data No./Number of LOOP to LEND repetitions |
| Timer | T0 | — | — | — | PLC READY signal OFF confirmation | PLC READY signal OFF |
| Timer | T1 | — | — | — | PLC READY signal OFF confirmation | PLC READY signal OFF |
| Code | U1\G2406 | U1\G2406 | U1\G2406 | U1\G2406 | Error code | [Md.23] Axis error No. |
| Code | U1\G2409 | U1\G2409 | U1\G2409 | U1\G2409 | Axis operation status | [Md.26] Axis operation status |
| Code | U1\G2417 | U1\G2417 | U1\G2417 | U1\G2417 | Status | [Md.31] Status |
| Code | U1\G4300 | U1\G4300 | U1\G4300 | U1\G4300 | Positioning start No. | [Cd.3] Positioning start No. |
| Code | U1\G4301 | U1\G4301 | U1\G4301 | U1\G4301 | Positioning starting point No. | [Cd.4] Positioning starting point No. |
| Code | U1\G4302 | U1\G4302 | U1\G4302 | U1\G4302 | Error reset | [Cd.5] Axis error reset |
| Code | U1\G4303 | U1\G4303 | U1\G4303 | U1\G4303 | Restart command | [Cd.6] Restart command |
| Code | U1\G4304 | U1\G4304 | U1\G4304 | U1\G4304 | M code OFF request (Buffer memory) | [Cd.7] M code OFF request |
| Code | U1\G4305 | U1\G4305 | U1\G4305 | U1\G4305 | External command valid | [Cd.8] External command valid |
| Code | U1\G4313 | U1\G4313 | U1\G4313 | U1\G4313 | Override request | [Cd.13] Positioning operation speed override |
| Code | U1\G4316 | U1\G4316 | U1\G4316 | U1\G4316 | Speed change request | [Cd.15] Speed change request |
| Code | U1\G4317 | U1\G4317 | U1\G4317 | U1\G4317 | Inching movement amount | [Cd.16] Inching movement amount |
| Code | U1\G4320 | U1\G4320 | U1\G4320 | U1\G4320 | Interrupt request during continuous operation | [Cd.18] Interrupt request during continuous operation |
| Code | U1\G4321 | U1\G4321 | U1\G4321 | U1\G4321 | Home position return request flag OFF request | [Cd.19] Home position return request flag OFF request |
| Code | U1\G4324 | U1\G4324 | U1\G4324 | U1\G4324 | Manual pulse generator enable flag | [Cd.21] Manual pulse generator enable flag |
| Code | U1\G4326 | U1\G4326 | U1\G4326 | U1\G4326 | Speed-position switching control movement amount | [Cd.23] Speed-position switching control movement amount change register |
| Code | U1\G4328 | U1\G4328 | U1\G4328 | U1\G4328 | Speed-position switching enable flag | [Cd.24] Speed-position switching enable flag |
| Code | U1\G4330 | U1\G4330 | U1\G4330 | U1\G4330 | Position-speed switching control speed change | [Cd.25] Position-speed switching control speed change register |
| Code | U1\G4332 | U1\G4332 | U1\G4332 | U1\G4332 | Position-speed switching enable flag | [Cd.26] Position-speed switching enable flag |
| Code | U1\G4338 | U1\G4338 | U1\G4338 | U1\G4338 | Target position change request flag | [Cd.29] Target position change request flag |
| Code | U1\G4344 | U1\G4344 | U1\G4344 | U1\G4344 | Step mode | [Cd.34] Step mode |
| Code | U1\G4347 | U1\G4347 | U1\G4347 | U1\G4347 | Skip command | [Cd.37] Skip command |

*In the original, the "Device name" column (Data register / Timer / Code) is a vertically merged cell for each category. Expanded to each row.
*In the original, the Axis 2 to Axis 4 columns of "Device" are merged vertically and horizontally into one cell showing "—" for the range D0 to T1. Expanded to each row and column.
*In the original, each row of the "Code" category (U1\G2406 to U1\G4347) has the device in one cell merged over Axis 1 to Axis 4 (one device in one cell). The same value is expanded to each of the Axis 1 to Axis 4 columns.
*In the original, the "Storage details" column is a vertically merged cell over the following ranges. Expanded to each row: D1-D2, D3-D4, D6-D7, D8-D9, D11-D12, D15-D16, D17-D18, D23-D24, D25-D26, D52-D53, D54-D55, D56-D57, D68-D77, D100-D109, D110-D119, D120-D129, D130-D139, D140-D149, D150-D159, D190-D199, D200-D209, D240-D249, T0-T1.
*In the original, the "Application" column of D68 to D77 has two parts: the left part "Block start data (Block 0)" is a vertically merged cell over D68 to D77, and the right part is the content of each point. Expanded to each row in the form "left part / right part".
*In the original, the table spans the 5 pages p.645-649 (the header row is repeated on p.646 to p.649).

### Program examples (for using buffer memory) (プログラム例(バッファメモリ使用時)) (12.4 / original p.650-675)

Transcription notation:
- The ladder diagrams are transcribed as mnemonic. The step number in parentheses is the number shown at the left end of the original ladder diagram. The text after `//` on an instruction line is the device comment shown in the ladder diagram (`U1¥G` written as `U1\G`).
- Statements (the light-blue comment bars in the ladder, e.g. `<Change speed setting (90.00 mm/min)>`) are written as `// <...>` lines immediately before the instruction they belong to. Rung-head comment blocks are written as `// ...` lines before the step number.
- Parallel circuits are represented with MPS/MRD/MPP/ORB/ANB (a transcription to represent the branch structure of the ladder diagram).

#### Parameter setting program (パラメータ設定プログラム) (12.4 / original p.650-651)

This program is not required when the parameter is set by "Module Parameter" using an engineering tool.

[Ladder] No.1 Parameter setting program (original p.650)

```
// No.1 Parameter setting program
// (For basic parameters <Axis 1>)
// HPR paramter
(0)    LD    SM402              // SM402: ON for 1 scan only after RUN
       // <Change speed setting (90.00 mm/min)>
       DMOVP K9000 D1           // D1: Speed (low-order 16 bits)
       // <Travel distance setting after change (5000.0 μm)>
       DMOVP K50000 D3          // D3: Movement amount (low-order 16 bits)
       // <Unit setting (0: mm) setting>
       MOVP  K0 D50             // D50: Unit setting
       // <Unit magnification (direct) setting>
       MOVP  K1 D51             // D51: Unit magnification: AM
       // <Number of pulses per rotation (4194304 pulses)>
       DMOVP K4194304 D52       // D52: No. of pulses per rotation (low-order 16 bits): AP
       // <Movement amount per rotation (2500.0 μm)>
       DMOVP K25000 D54         // D54: Movement amount per rotation (low-order 16 bits): AL
       // <Setting of basic parameter1>
       TOP   H1 K0 D50 K8       // D50: Unit setting
       // <External command function selection (2: Speed/Position)>
       TOP   H1 K62 K2 K1
       // <HPR method (data set type)>
       TOP   H1 K70 K6 K1
       // <HPR speed (15.00 mm/min)>
       DTOP  H1 K74 K1500 K1
       // <Creep speed setting (12.00 mm/min)>
       DTOP  H1 K76 K1200 K1
       // <Setting of basic parameter1 completed>
       SET   M50                // M50: Parameter setting complete device
```

- "HPR paramter" is spelled as in the original.
- In the original, the step (0) circuit has SM402 followed by instructions branching in parallel from the bus after SM402.

[Ladder] Unit degree setting program (original p.651)

```
// Unit degree setting program
// <For axis 1>
// (When executing speed/position switching control (ABS mode), etc.
// <X55 turns ON before startup.>
(720)  LD    SM402              // SM402: ON for 1 scan only after RUN
       AND   X55                // X55: For unit (degree)
       // <Unit setting (2: degree) setting>
       TOP   H1 K0 K2 K1
       // <Movement amount per rotation: AL>
       DTOP  H1 K4 K9000000 K1
       // <Speed limit value (20000.000 degrees/min)>
       DTOP  H1 K10 K20000000 K1
       // <(S/W stroke limit upper limit) = 0>
       DTOP  H1 K18 K0 K1
       // <(S/W stroke limit lower limit) = 0>
       DTOP  H1 K20 K0 K1
       // <(Feed current value in speed control mode) = 0>
       TOP   H1 K30 K2 K1
       // <Speed/position function selection (ABS mode)>
       TOP   H1 K34 K2 K1
       // <JOG speed limit value (20000.000 degrees/min)>
       DTOP  H1 K48 K20000000 K1
       // <HPR speed (1000.000 degrees/min)>
       DTOP  H1 K74 K1000000 K1
       // <Creep speed (800.000 degrees/min)>
       DTOP  H1 K76 K800000 K1
```

- The rung-head comment "(When executing speed/position switching control (ABS mode), etc." has no closing parenthesis in the original.
- The statement "<(Feed current value in speed control mode) = 0>" is followed by `TOP H1 K30 K2 K1` (value K2) as printed in the original.

#### Positioning data setting program (位置決めデータ設定プログラム) (12.4 / original p.652-660)

This program is not required when the data is set by "Positioning Data" using an engineering tool.

- In each of No.2-1 to No.2-9, the X55 contacts are placed in series only on the branch of the instruction that follows them (branch from the bus after SM402); this is written with MPS/AND/MPP.

##### No.2-1 Positioning data setting program (For positioning data No.1 <Axis 1>) (No.2-1 位置決めデータ設定プログラム(位置決めデータNo.1<軸1>の場合)) (12.4 / original p.652)

```
// No.2-1 Positioning data setting program
// (For positioning data No.1 <Axis 1>)
// <Positioning identifier>
//   Operation pattern: Positioning terminated
//   Control system: 1 axis linear control (ABS)
//   Acceleration time No.: 1, deceleration time No.: 2
(1428) LD    SM402              // SM402: ON for 1 scan only after RUN
       // <Positioning identifier setting>
       MOVP  H190 D100         // D100: Positioning identifier
       // <M code (9843) setting>
       MOVP  K9843 D101        // D101: M code
       // <Dwell time (300 ms) setting>
       MOVP  K300 D102         // D102: Dwell time
       // <(Dummy data)>
       MOVP  K0 D103           // D103: (Dummy)
       // <Command speed (20.00 mm/min) setting>
       DMOVP K2000 D104        // D104: Command speed (low-order 16 bits)
       MPS
       AND   X55               // X55: For unit (degree)
       // <Command speed (1200.000 degrees/min) setting>
       DMOVP K1200000 D104     // D104: Command speed (low-order 16 bits)
       MPP
       // <Positioning address (-10000.0 μm) setting>
       DMOVP K-100000 D106     // D106: Positioning address (low-order 16 bits)
       MPS
       AND   X55               // X55: For unit (degree)
       // <Positioning address (270.00000 degrees) setting>
       DMOVP K27000000 D106    // D106: Positioning address (low-order 16 bits)
       MPP
       // <Arc address (0.0 μm) setting>
       DMOVP K0 D108           // D108: Arc address (low-order 16 bits)
       // <Positioning data No.1 setting>
       TOP   H1 K6000 D100 K10 // D100: Positioning identifier
```

##### No.2-2 Positioning data setting program (For positioning data No.2 <Axis 1>) (No.2-2 位置決めデータ設定プログラム(位置決めデータNo.2<軸1>の場合)) (12.4 / original p.653)

```
// No.2-2 Positioning data setting program
// (For positioning data No.2 <Axis 1>)
// <Positioning identifier>
//   Operation pattern: Positioning terminated
//   Control method: Speed/position switching control (forward run)
//   Acceleration time No.: 0, deceleration time No.: 0
(2035) LD    SM402              // SM402: ON for 1 scan only after RUN
       // <Positioning identifier setting>
       MOVP  H600 D110         // D110: Positioning identifier
       // <M code (0) setting>
       MOVP  K0 D111           // D111: M code
       // <Dwell time (300 ms) setting>
       MOVP  K300 D112         // D112: Dwell time
       // <(Dummy data)>
       MOVP  K0 D113           // D113: (Dummy)
       // <Command speed (180.00 mm/min) setting>
       DMOVP K18000 D114       // D114: Command speed (low-order 16 bits)
       MPS
       AND   X55               // X55: For unit (degree)
       // <Command speed (3600.000 degrees/min) setting>
       DMOVP K3600000 D114     // D114: Command speed (low-order 16 bits)
       MPP
       // <Positioning address (2500.0 μm) setting>
       DMOVP K25000 D116       // D116: Positioning address (low-order 16 bits)
       MPS
       AND   X55               // X55: For unit (degree)
       // <Positioning address (90.00000 degrees) setting>
       DMOVP K9000000 D116     // D116: Positioning address (low-order 16 bits)
       MPP
       // <Arc address (0.0 μm) setting>
       DMOVP K0 D118           // D118: Arc address (low-order 16 bits)
       // <Positioning data No.2 setting>
       TOP   H1 K6010 D110 K10 // D110: Positioning identifier
```

##### No.2-3 Positioning data setting program (For positioning data No.3 <Axis 1>) (No.2-3 位置決めデータ設定プログラム(位置決めデータNo.3<軸1>の場合)) (12.4 / original p.654)

```
// No.2-3 Positioning data setting program
// (For positioning data No.3 <Axis 1>)
// <Positioning identifier>
//   Operation pattern: Positioning terminated
//   Control method: Position/speed switching control (forward run)
//   Acceleration time No.: 0, deceleration time No.: 0
(2636) LD    SM402              // SM402: ON for 1 scan only after RUN
       // <Positioning identifier setting>
       MOVP  H800 D120         // D120: Positioning identifier
       // <M code (0) setting>
       MOVP  K0 D121           // D121: M code
       // <Dwell time (300 ms) setting>
       MOVP  K300 D122         // D122: Dwell time
       // <(Dummy data)>
       MOVP  K0 D123           // D123: (Dummy)
       // <Command speed (180.00 mm/min) setting>
       DMOVP K18000 D124       // D124: Command speed (low-order 16 bits)
       MPS
       AND   X55               // X55: For unit (degree)
       // <Command speed (3600.000 degrees/min) setting>
       DMOVP K3600000 D124     // D124: Command speed (low-order 16 bits)
       MPP
       // <Positioning address (20000.0 μm) setting>
       DMOVP K200000 D126      // D126: Positioning address (low-order 16 bits)
       MPS
       AND   X55               // X55: For unit (degree)
       // <Positioning address (720.00000 degrees) setting>
       DMOVP K72000000 D126    // D126: Positioning address (low-order 16 bits)
       MPP
       // <Arc address (0.0 μm) setting>
       DMOVP K0 D128           // D128: Arc address (low-order 16 bits)
       // <Positioning data No.3 setting>
       TOP   H1 K6020 D120 K10 // D120: Positioning identifier
```

##### No.2-4 Positioning data setting program (For positioning data No.4 <Axis 1>) (No.2-4 位置決めデータ設定プログラム(位置決めデータNo.4<軸1>の場合)) (12.4 / original p.655)

```
// No.2-4 Positioning data setting program
// (For positioning data No.4 <Axis 1>)
// <Positioning identifier>
//   Operation pattern: Positioning terminated
//   Control system: 1-axis linear control (INC)
//   Acceleration time No.: 0, deceleration time No.: 0
(3239) LD    SM402              // SM402: ON for 1 scan only after RUN
       // <Positioning identifier setting>
       MOVP  H200 D130         // D130: Positioning identifier
       // <M code (0) setting>
       MOVP  K0 D131           // D131: M code
       // <Dwell time (300 ms) setting>
       MOVP  K300 D132         // D132: Dwell time
       // <(Dummy data)>
       MOVP  K0 D133           // D133: (Dmmy)
       // <Command speed (90.00 mm/min) setting>
       DMOVP K9000 D134        // D134: Command speed (low-order 16 bits)
       MPS
       AND   X55               // X55: For unit (degree)
       // <Command speed (1800.000 degrees/min)>
       DMOVP K1800000 D134     // D134: Command speed (low-order 16 bits)
       MPP
       // <Positioning address (5000.0 μm) setting>
       DMOVP K50000 D136       // D136: Positioning address (low-order 16 bits)
       MPS
       AND   X55               // X55: For unit (degree)
       // <Positioning address (180.00000 degrees) setting>
       DMOVP K18000000 D136    // D136: Positioning address (low-order 16 bits)
       MPP
       // <Arc address (0.0 μm) setting>
       DMOVP K0 D138           // D138: Arc address (low-order 16 bits)
       // <Positioning data No.4 setting>
       TOP   H1 K6030 D130 K10 // D130: Positioning identifier
```

- The device comment of D133 is shown as "(Dmmy)" in the original (transcribed as printed).
- The statement "<Command speed (1800.000 degrees/min)>" has no "setting" in the original (transcribed as printed).

##### No.2-5 Positioning data setting program (For positioning data No.5 <Axis 1>) (No.2-5 位置決めデータ設定プログラム(位置決めデータNo.5<軸1>の場合)) (12.4 / original p.656)

```
// No.2-5 Positioning data setting program
// (For positioning data No.5 <Axis 1>)
// <Positioning identifier>
//   Operation pattern: Continuous positioning control
//   Control system: 1-axis linear control (INC)
//   Acceleration time No.: 0, deceleration time No.: 0
(3831) LD    SM402              // SM402: ON for 1 scan only after RUN
       // <Positioning identifier setting>
       MOVP  H201 D140         // D140: Positioning identifier
       // <M code (0) setting>
       MOVP  K0 D141           // D141: M code
       // <Dwell time (300 ms) setting>
       MOVP  K300 D142         // D142: Dwell time
       // <(Dummy data)>
       MOVP  K0 D143           // D143: (Dummy)
       // <Command speed (360.00 mm/min) setting>
       DMOVP K36000 D144       // D144: Command speed (low-order 16 bits)
       MPS
       AND   X55               // X55: For unit (degree)
       // <Command speed (6000.000 degrees/min) setting>
       DMOVP K6000000 D144     // D144: Command speed (low-order 16 bits)
       MPP
       // <Positioning address (10000.0 μm) setting>
       DMOVP K100000 D146      // D146: Positioning address (low-order 16 bits)
       MPS
       AND   X55               // X55: For unit (degree)
       // <Positioning address (360.00000 degrees) setting>
       DMOVP K36000000 D146    // D146: Positioning address (low-order 16 bits)
       MPP
       // <Arc address (0.0 μm) setting>
       DMOVP K0 D148           // D148: Arc address (low-order 16 bits)
       // <Positioning data No.5 setting>
       TOP   H1 K6040 D140 K10 // D140: Positioning identifier
```

##### No.2-6 Positioning data setting program (For positioning data No.6 <Axis 1>) (No.2-6 位置決めデータ設定プログラム(位置決めデータNo.6<軸1>の場合)) (12.4 / original p.657)

```
// No.2-6 Positioning data setting program
// (For positioning data No.6 <Axis 1>)
// <Positioning identifier>
//   Operation pattern: Positioning terminated
//   Control system: 1-axis linear control (INC)
//   Acceleration time No.: 0, deceleration time No.: 0
(4434) LD    SM402              // SM402: ON for 1 scan only after RUN
       // <Positioning identifier setting>
       MOVP  H200 D150         // D150: Positioning identifier
       // <M code (0) setting>
       MOVP  K0 D151           // D151: M code
       // <Dwell time (300 ms) setting>
       MOVP  K300 D152         // D152: Dwell time
       // <(Dummy data)>
       MOVP  K0 D153           // D153: (Dummy)
       // <Command speed (90.00 mm/min) setting>
       DMOVP K9000 D154        // D154: Command speed (low-order 16 bits)
       MPS
       AND   X55               // X55: For unit (degree)
       // <Command speed (1800.000 degrees/min) setting>
       DMOVP K1800000 D154     // D154: Command speed (low-order 16 bits)
       MPP
       // <Positioning address (5000.0 μm) setting>
       DMOVP K50000 D156       // D156: Positioning address (low-order 16 bits)
       MPS
       AND   X55               // X55: For unit (degree)
       // <Positioning address (180.00000 degrees) setting>
       DMOVP K18000000 D156    // D156: Positioning address (low-order 16 bits)
       MPP
       // <Arc address (0.0 μm) setting>
       DMOVP K0 D158           // D158: Arc address (low-order 16 bits)
       // <Positioning data No.6 setting>
       TOP   H1 K6050 D150 K10 // D150: Positioning identifier
```

##### No.2-7 Positioning data setting program (For positioning data No.10 <Axis 1>) (No.2-7 位置決めデータ設定プログラム(位置決めデータNo.10<軸1>の場合)) (12.4 / original p.658)

```
// No.2-7 Positioning data setting program
// (For positioning data No.10 <Axis 1>)
// <Positioning identifier>
//   Operation pattern: Continuous positioning control
//   Control system: 1-axis linear control (INC)
//   Acceleration time No.: 0, deceleration time No.: 0
(5035) LD    SM402              // SM402: ON for 1 scan only after RUN
       // <Positioning identifier setting>
       MOVP  H201 D190         // D190: Positioning identifier
       // <M code (0) setting>
       MOVP  K0 D191           // D191: M code
       // <Dwell time (300 ms) setting>
       MOVP  K300 D192         // D192: Dwell time
       // <(Dummy data)>
       MOVP  K0 D193           // D193: (Dummy)
       // <Command speed (180.00 mm/min) setting>
       DMOVP K18000 D194       // D194: Command speed (low-order 16 bits)
       MPS
       AND   X55               // X55: For unit (degree)
       // <Command speed (3600.000 degrees/min) setting>
       DMOVP K3600000 D194     // D194: Command speed (low-order 16 bits)
       MPP
       // <Positioning address (10000.0 μm) setting>
       DMOVP K100000 D196      // D196: Positioning address (low-order 16 bits)
       MPS
       AND   X55               // X55: For unit (degree)
       // <Positioning address (360.00000 degrees) setting>
       DMOVP K36000000 D196    // D196: Positioning address (low-order 16 bits)
       MPP
       // <Arc address (0.0 μm) setting>
       DMOVP K0 D198           // D198: Arc address (low-order 16 bits)
       // <Positioning data No.10 setting>
       TOP   H1 K6090 D190 K10 // D190: Positioning identifier
```

##### No.2-8 Positioning data setting program (For positioning data No.11 <Axis 1>) (No.2-8 位置決めデータ設定プログラム(位置決めデータNo.11<軸1>の場合)) (12.4 / original p.659)

```
// No.2-8 Positioning data setting program
// (For positioning data No.11 <Axis 1>)
// <Positioning identifier>
//   Operation pattern: Positioning terminated
//   Control system: 1-axis linear control (INC)
//   Acceleration time No.: 0, deceleration time No.: 0
(5640) LD    SM402              // SM402: ON for 1 scan only after RUN
       // <Positioning identifier setting>
       MOVP  H200 D200         // D200: Positioning identifier
       // <M code (0) setting>
       MOVP  K0 D201           // D201: M code
       // <Dwell time (300 ms) setting>
       MOVP  K300 D202         // D202: Dwell time
       // <(Dummy data)>
       MOVP  K0 D203           // D203: (Dummy)
       // <Command speed (180.00 mm/min) setting>
       DMOVP K18000 D204       // D204: Command speed (low-order 16 bits)
       MPS
       AND   X55               // X55: For unit (degree)
       // <Command speed (3600.000 degrees/min) setting>
       DMOVP K3600000 D204     // D204: Command speed (low-order 16 bits)
       MPP
       // <Positioning address (-10000.0 μm) setting>
       DMOVP K-100000 D206     // D206: Positioning address (low-order 16 bits)
       MPS
       AND   X55               // X55: For unit (degree)
       // <Positioning address (-360.00000 degrees) setting>
       DMOVP K-36000000 D206   // D206: Positioning address (low-order 16 bits)
       MPP
       // <Arc address (0.0 μm) setting>
       DMOVP K0 D208           // D208: Arc address (low-order 16 bits)
       // <Positioning data No.11 setting>
       TOP   H1 K6100 D200 K10 // D200: Positioning identifier
```

##### No.2-9 Positioning data setting program (For positioning data No.15 <Axis 1>) (No.2-9 位置決めデータ設定プログラム(位置決めデータNo.15<軸1>の場合)) (12.4 / original p.660)

```
// No.2-9 Positioning data setting program
// (For positioning data No. 15 <Axis 1>)
// <Positioning identifier>
//   Operation pattern: Positioning terminated
//   Control system: 1-axis linear control (INC)
//   Acceleration time No.: 0, deceleration time No.: 0
(6249) LD    SM402              // SM402: ON for 1 scan only after RUN
       // <Positioning identifier setting>
       MOVP  H200 D240         // D240: Positioning identifier
       // <M code (0) setting>
       MOVP  K0 D241           // D241: M code
       // <Dwell time (0 ms) setting>
       MOVP  K0 D242           // D242: Dwell time
       // <(Dummy data)>
       MOVP  K0 D243           // D243: (Dummy)
       // <Command speed (90.00 mm/min) setting>
       DMOVP K9000 D244        // D244: Command speed (low-order 16 bits)
       MPS
       AND   X55               // X55: For unit (degree)
       // <Command speed (1800.000 degrees/min) setting>
       DMOVP K1800000 D244     // D244: Command speed (low-order 16 bits)
       MPP
       // <Positioning address (5000.0 μm) setting>
       DMOVP K50000 D246       // D246: Positioning address (low-order 16 bits)
       MPS
       AND   X55               // X55: For unit (degree)
       // <Positioning address (180.00000 degrees) setting>
       DMOVP K18000000 D246    // D246: Positioning address (low-order 16 bits)
       MPP
       // <Arc address (0.0 μm) setting>
       DMOVP K0 D248           // D248: Arc address (low-order 16 bits)
       // <Positioning data No.15 setting>
       TOP   H1 K6140 D240 K10 // D240: Positioning identifier
```

#### Block start data setting program (ブロック始動データ設定プログラム) (12.4 / original p.661)

This program is not required when the data is set by "Block Start Data" using an engineering tool.

```
// No.3 Block start data setting program
//   Block start data of start block 0 (Axis1)
//   For setting of points 1 to 5
//     (Conditions)
//       Shape: Continued at points 1 to 4, ended at points 5
//       Special start instruction: Normal start (Points 1 to 5)
//       <Positioning data are already preset>
//
//     [Setting of shape and start data No.]
(6850) LD    SM402              // SM402: ON for 1 scan only after RUN
       // <Continue, Set start data No.1.>
       MOVP  H8001 D68          // D68: Point 1 (shape, start No.)
       // <Continue, Set start data No.4.>
       MOVP  H8004 D69          // D69: Point 2 (shape, start No.)
       // <Continue, Set start data No.5>
       MOVP  H8005 D70          // D70: Point 3 (shape, start No.)
       // <Continue, Set start data No.10.>
       MOVP  H800A D71          // D71: Point 4 (shape, start No.)
       // <Continue, Set start data No.15.>
       MOVP  H0F D72            // D72: Point 5 (shape, start No.)
       // <Set block start data.>
       TOP   H1 K22000 D68 K5   // D68: Point 1 (shape, start No.)

//     [Setting of special start instruction to normal start]
(7216) LD    SM402              // SM402: ON for 1 scan only after RUN
       // <Set normal start.>
       MOVP  H0 D73             // D73: Point 1 (special start instruction)
       // <Set normal start.>
       MOVP  H0 D74             // D74: Point 2 (special start instruction)
       // <Set normal start.>
       MOVP  H0 D75             // D75: Point 3 (special start instruction)
       // <Set normal start.>
       MOVP  H0 D76             // D76: Point 4 (special start instruction)
       // <Set normal start.>
       MOVP  H0 D77             // D77: Point 5 (special start instruction)
       // <Block start data setting>
       TOP   H1 K22050 D73 K5   // D73: Point 1 (special start instruction)
```

- The statement for point 5 reads "<Continue, Set start data No.15.>" in the original although the value H0F (end, start data No.15) is set and the rung-head condition says "ended at points 5" (transcribed as printed).

#### Servo parameter setting program (サーボパラメータ設定プログラム) (12.4 / original p.662)

This program is not required when the parameter is set by "Servo Parameter" using an engineering tool.

```
// No.4 Servo parameter
(7318) LD    SM402              // SM402: ON for 1 scan only after RUN
       // <Absolute position system exists>
       TOP   H1 K28403 H1 K1
       // <Servo series (MR-J4-B)>
       TOP   H1 K28400 K32 K1
```

#### Home position return request OFF program (原点復帰要求OFFプログラム) (12.4 / original p.662)

This program is not required when "1: Positioning control is executed." is set in "[Pr.55] Operation setting for incompletion of home position return" by "Home Position Return Detailed Parameters" using an engineering tool.

```
// No.5 HPR request OFF program
(7438) LD    X0                 // X0: HPR request OFF command
       // <Pulse conversion of HPR request OFF command>
       PLS   M1                 // M1: HPR request OFF command pulse
(7540) LD    M1                 // M1: HPR request OFF command pulse
       ANI   U1\G30104.0        // U1\G30104.0: Positioning start signal (axis 1)
       ANI   U1\G2417.E         // U1\G2417.E: Start complete signal (axis 1)
       // <Holding the HPR request OFF command>
       SET   M2                 // M2: HPR request OFF command storage
(7594) LD    M2                 // M2: HPR request OFF command storage
       WANDP U1\G2417 H8 D0     // U1\G2417: Status / D0: HPR request flag
       MPS
       AND<> D0 K0              // D0: HPR request flag
       // <HPR request OFF command ON>
       SET   M0                 // M0: HPR request OFF command
       MPP
       // <HPR request OFF command storage OFF>
       RST   M2                 // M2: HPR request OFF command storage
(7692) LD    M0                 // M0: HPR request OFF command
       // <Writing HPR request OFF request>
       MOVP  K1 U1\G4321        // U1\G4321: HPR request flag OFF request
       AND=  U1\G4321 K0        // U1\G4321: HPR request flag OFF request
       // <HPR request flag OFF command OFF >
       RST   M0                 // M0: HPR request OFF command
```

- In the original ladder diagram, the buffer memory is written "U1¥G30104.0", "U1¥G2417.E", "U1¥G2417", "U1¥G4321" (¥ = backslash).
- U1\G30104.0 and U1\G2417.E are b contacts (read from the contact symbols in the original figure).
- Step (7594) circuit: branches after M2 into 3 parallel lines: WANDP, [<> D0 K0]→SET M0, and RST M2. Step (7692) circuit: branches after M0 into MOVP K1 U1\G4321 and [= U1\G4321 K0]→RST M0 in parallel.
- In the original, the step numbers (7438) and (7540) are also shown on the statement row above each rung.

#### External command function valid setting program (外部指令機能有効設定プログラム) (12.4 / original p.662)

```
// No.6 External command function valid setting program
(7790) LD    X1                 // X1: External command valid command
       // <Writing external commend valid>
       MOVP  K1 U1\G4305        // U1\G4305: External command valid
(7907) LD    X2                 // X2: External command invalid command
       // <Writing external commend invalid>
       MOVP  K0 U1\G4305        // U1\G4305: External command valid
```

- "commend" in the two statements is spelled as in the original.

#### PLC READY signal ON program (シーケンサレディ信号ONプログラム) (12.4 / original p.663)

```
// No.7 [Cd.190] PLC READY signal ON program
(7956) LD    SM403              // SM403: 1 scan OFF after RUN
       AND   M50                // M50: Parameter setting complete device
       ANI   M25                // M25: Parameter initialization command storage
       ANI   M27                // M27: Flash ROM write command storage
       AND   X53                // X53: PLC READY signal ON
       // <PLC ready signal ON/OFF>
       OUT   U1\G5950.0         // U1\G5950.0: PLC READY signal
```

- Contact types (read from figure): M25 and M27 are b contacts; SM403, M50 and X53 are a contacts.
- In the original figure the buffer memory is written "U1¥G5950.0" (written as U1\G in the mnemonic; the same applies below).

#### All axis servo ON program (全軸サーボONプログラム) (12.4 / original p.663)

```
// No.8 [Cd.191] All axis servo ON signal ON program
(8063) LD    X57                // X57: All axis servo ON command
       AND   U1\G5950.0         // U1\G5950.0: PLC READY signal
       AND   U1\G31500.1        // U1\G31500.1: Synchronization flag
       // <All axes servo ON>
       OUT   U1\G5951.0         // U1\G5951.0: All axis servo ON signal
```

- Contact types (read from figure): all a contacts.

#### Positioning start No. setting program (位置決め始動番号設定プログラム) (12.4 / original p.664-665)

```
// No.9 Positioning start number setting program
// (1) Machine HPR
(8159) LD    X3                 // X3: Machine HPR command
       // <Writing Machine HPR (9001)>
       MOVP  K9001 D32          // D32: Start number

// (2) Fast HPR
(8272) LD    X4                 // X4: Fast HPR command
       // <Extracting HPR request flag ON/OFF>
       WANDP U1\G2417 H8 D0     // U1\G2417: Status / D0: HPR request flag
       MPS
       AND=  D0 K0              // D0: HPR request flag
       // <Enabling fast HPR start>
       SET   M3                 // M3: Fast HPR command
       MPP
       // <Writing fast HPR (9002)>
       MOVP  K9002 D32          // D32: Start number
       // <Holding the fast HPR command>
       SET   M4                 // M4: Fast HPR command storage

// (3) Positioning with positioning data No. 1
(8453) LD    X5                 // X5: Positioning start command
       // <Positioning data No. 1 setting>
       MOVP  K1 D32             // D32: Start number

// (4) Speed-position switching operation (Positioning data No. 2)
//     (In the ABS mode, new movement amount write is not needed.)
(8513) LD    X6                 // X6: Speed/position switching operation command
       // <Positioning data No.2 setting>
       MOVP  K2 D32             // D32: Start number
(8577) LD    X7                 // X7: Speed/position switching enable command
       // <Setting speed/position switching signal enable>
       MOVP  K1 U1\G4328        // U1\G4328: Speed/position switching enable flag
(8641) LD    X10                // X10: Speed/position switching prohibit command
       // <Setting speed/position switching signal prohibit>
       MOVP  K0 U1\G4328        // U1\G4328: Speed/position switching enable flag
(8707) LD    X11                // X11: Movement amount change command
       // <Writing movement amount after change>
       DMOVP D3 U1\G4326        // D3: Movement amount (low-order 16 bits) / U1\G4326: Speed/position switching control movement amount

// (5) Position/speed switching operation (positioning data No. 3)          <- original p.665
(8772) LD    X40                // X40: Position/speed switching operation command
       // <Positioning data No.3 setting>
       MOVP  K3 D32             // D32: Start number
(8831) LD    X41                // X41: Position/speed switching enable command
       ANI   X42                // X42: Position/speed switching prohibit command
       // <Setting position/speed switching signal enable>
       MOVP  K1 U1\G4332        // U1\G4332: Position/speed switching enable flag
(8897) LDI   X41                // X41: Position/speed switching enable command
       AND   X42                // X42: Position/speed switching prohibit command
       // <Setting position/speed switching signal prohibit>
       MOVP  K0 U1\G4332        // U1\G4332: Position/speed switching enable flag
(8965) LD    X43                // X43: Speed change command
       // <Writing speed after change>
       DMOVP D1 U1\G4330        // D1: Speed (low-order 16 bits) / U1\G4330: Position/speed switching control speed change

// (6) High-level positioning control
(9007) LD    X12                // X12: High-level positioning control start command
       // <Writing block positioning (7000)>
       MOVP  K7000 D32          // D32: Start number
       // <Writing positioning start point number (1)>
       MOVP  K1 U1\G4301        // U1\G4301: Positioning starting point No.

// (7) Fast HPR command and fast HPR command storage OFF
//     (Not required when fast HPR is not used)
(9127) LD    X3                 // X3: Machine HPR command
       OR    X5                 // X5: Positioning start command
       OR    X6                 // X6: Speed/position switching operation command
       OR    X40                // X40: Position/speed switching operation command
       OR    X12                // X12: High-level positioning control start command
       OR    M6                 // M6: Positioning start command storage
       // <Fast HPR command OFF>
       RST   M3                 // M3: Fast HPR command
       // <Fast HPR command storage OFF>
       RST   M4                 // M4: Fast HPR command storage
```

- Contact types (read from figure): X42 in (8831) and X41 in (8897) are b contacts. All others are a contacts.
- (8272): after X4, the circuit branches into 4 lines: WANDP U1\G2417 H8 D0; [= D0 K0]→SET M3; (no contact)→MOVP K9002 D32; (no contact)→SET M4 (read from figure). MPS/MPP are a transcription to represent the branch structure.
- (9007): after X12, MOVP K7000 D32 and MOVP K1 U1\G4301 are parallel outputs (same condition).
- (9127): the 6 contacts X3, X5, X6, X40, X12 and M6 are in OR (parallel), with RST M3 and RST M4 as parallel outputs (same condition).
- In the original, (1) to (4) are on p.664 and (5) to (7) continue on p.665. Step numbers are also shown on the statement row above each rung.

#### Positioning start program (位置決め始動プログラム) (12.4 / original p.666)

```
// No.10 Positioning start program
//   (When fast HPR is not perfomed, contacts of M3 and M4 are not needed.)
//   (When M code is not used, contacts of U0\G2417.C are not needed.)
//   (When JOG/inching operation is not performed, contacts of M7 are not needed.)
//   (When manual pulse generator operation is not perfomed, contacts of M9 is not needed.)
(9228) LD    X56                // X56: Positioning start signal command
       // <Pulse conversion of positioning start command>
       PLS   M5                 // M5: Positioning start command pulse
(9356) LD    M5                 // M5: Positioning start command pulse
       ANI   U1\G30104.0        // U1\G30104.0: Positioning start signal (axis 1)
       ANI   U1\G2417.E         // U1\G2417.E: Start complete signal (axis 1)
       ANI   U1\G2417.C         // U1\G2417.C: M code ON signal (axis 1)
       ANI   M7                 // M7: JOG/inching operation flag
       ANI   M9                 // M9: Manual pulse generator operating flag
       LDI   M3                 // M3: Fast HPR command
       LD    M3                 // M3: Fast HPR command
       AND   M4                 // M4: Fast HPR command storage
       ORB
       ANB
       // <Holding the positioning start command>
       SET   M6                 // M6: Positioning start command storage
(9427) LD    M6                 // M6: Positioning start command storage
       // <Positioning start No. setting>
       MOVP  D32 U1\G4300       // D32: Start number / U1\G4300: Positioning start No.
       // <Executing positioning start>
       SET   U1\G30104.0        // U1\G30104.0: Positioning start signal (axis 1)
       // <Positioning start command storage OFF>
       RST   M6                 // M6: Positioning start command storage
(9560) LD    U1\G30104.0        // U1\G30104.0: Positioning start signal (axis 1)
       LD    U1\G2417.E         // U1\G2417.E: Start complete signal (axis 1)
       OR    U1\G2417.D         // U1\G2417.D: Error detection signal (axis 1)
       ANB
       ANI   U1\G31501.0        // U1\G31501.0: BUSY signal (axis 1)
       // <Positioning start signal OFF>
       RST   U1\G30104.0        // U1\G30104.0: Positioning start signal (axis 1)
```

- Contact types (read from figure): in (9356), U1\G30104.0, U1\G2417.E, U1\G2417.C, M7, M9 and the upper M3 are b contacts; the lower M3, M4 and M5 are a contacts. In (9560), U1\G31501.0 is a b contact and the others are a contacts.
- The end of (9356) is a parallel circuit of "M3 (b contact)" and "M3 (a contact) and M4 (a contact) in series" (read from figure).
- (9560) has "U1\G2417.E" and "U1\G2417.D" in parallel.
- "perfomed" (twice) and "U0\G2417.C" in the rung-head comments are as printed in the original (the contact in the ladder is U1¥G2417.C).
- The device comment of M7 in the ladder is "JOG/inching operation flag" (in the device list: "JOG/inching operation termination").

#### M code OFF program (MコードOFFプログラム) (12.4 / original p.666)

```
// No.11 M code OFF program
//   (Not required when M code is not used)
(9613) LD    X14                // X14: M code OFF command
       AND   U1\G2417.C         // U1\G2417.C: M code ON signal (axis 1)
       // <Writing M code OFF request>
       MOVP  K1 U1\G4304        // U1\G4304: M code OFF request (buffer memory)
```

- Contact types (read from figure): all a contacts.

#### JOG operation setting program (JOG運転設定プログラム) (12.4 / original p.667)

```
// No.12 JOG operation setting program
(9801) LD    X15                // X15: JOG operation speed setting command
       // <JOG operation speed (100.00 mm/min) setting>
       DMOVP K10000 D6          // D6: JOG operation speed (low-order 16 bits)
       MPS
       AND   X55                // X55: For unit (degree)
       // <JOG operation speed (1200.000 degrees/min) setting>
       DMOVP K1200000 D6        // D6: JOG operation speed (low-order 16 bits)
       MPP
       // <Setting the inching movement amount to (0)>
       MOVP  K0 D5              // D5: Inching movement amount
       // <Writing JOG operation speed>
       TOP   H1 K4317 D5 K3     // D5: Inching movement amount
```

- Contact types (read from figure): all a contacts.
- 4 branches after X15: (no contact)→DMOVP K10000 D6, X55→DMOVP K1200000 D6, (no contact)→MOVP K0 D5, (no contact)→TOP H1 K4317 D5 K3.

#### Inching operation setting program (インチング運転設定プログラム) (12.4 / original p.667)

```
// No.13 Inching operation setting program
(10080) LD   X44                // X44: Inching movement amount setting command
       ANI   X15                // X15: JOG operation speed setting command
       // <Inching movement amount (10.0 μm) setting>
       MOVP  K100 D5            // D5: Inching movement amount
       // <Writing inching movement amount>
       MOVP  D5 U1\G4317        // D5: Inching movement amount / U1\G4317: Inching movement amount
```

- Contact types (read from figure): X15 is a b contact, X44 is an a contact.

#### JOG operation/inching operation execution program (JOG運転／インチング運転実行プログラム) (12.4 / original p.667)

```
// No.14 JOG operation/inching operation execution program
(10240) LD   X16                // X16: Forward run JOG/inching command
       OR    X17                // X17: Reverse run JOG/inching command
       AND   U1\G31500.0        // U1\G31500.0: READY signal
       ANI   U1\G31501.0        // U1\G31501.0: BUSY signal (axis 1)
       // <JOG/inching operation flag ON>
       SET   M7                 // M7: JOG/inching operation flag
(10363) LDI  X16                // X16: Forward run JOG/inching command
       ANI   X17                // X17: Reverse run JOG/inching command
       // <JOG/inching operation end>
       RST   M7                 // M7: JOG/inching operation flag
(10402) LD   X16                // X16: Forward run JOG/inching command
       AND   M7                 // M7: JOG/inching operation flag
       ANI   U1\G30102.0        // U1\G30102.0: Reverse run JOG start signal (axis 1)
       // <Executing forward run JOG/inching operation>
       OUT   U1\G30101.0        // U1\G30101.0: Forward run JOG start signal (axis 1)
(10465) LD   X17                // X17: Reverse run JOG/inching command
       AND   M7                 // M7: JOG/inching operation flag
       ANI   U1\G30101.0        // U1\G30101.0: Forward run JOG start signal (axis 1)
       // <Executing reverse run JOG/inching operation>
       OUT   U1\G30102.0        // U1\G30102.0: Reverse run JOG start signal (axis 1)
```

- Contact types (read from figure): U1\G31501.0 in (10240), X16 and X17 in (10363), U1\G30102.0 in (10402) and U1\G30101.0 in (10465) are b contacts. The others are a contacts.
- (10240) has the parallel circuit of X16 and X17 followed by U1\G31500.0 and U1\G31501.0 in series.

#### Manual pulse generator operation program (手動パルサ運転プログラム) (12.4 / original p.668)

```
// No.15 Manual pulse generator operation program
(10426) LD   X20                // X20: Manual pulse generator operation enable command
       // <Pulse conversion of manual pulse generator operation command>
       PLS   M8                 // M8: Manual pulse generator operation enable command
(10566) LD   M8                 // M8: Manual pulse generator operation enable command
       AND   U1\G31500.0        // U1\G31500.0: READY signal
       ANI   U1\G31501.0        // U1\G31501.0: BUSY signal (axis 1)
       // <Setting manual pulse generator 1 pulse input magnification>
       DMOVP K1 D8              // D8: Manual pulse generator 1 pulse input magnification (low-order)
       // <Writing manual pulse generator operation enable>
       MOVP  K1 D10             // D10: Manual pulse generator operation enable
       // <Writing data for manual pulse generator>
       TOP   H1 K4322 D8 K3     // D8: Manual pulse generator 1 pulse input magnification (low-order)
       // <Manual pulse generator operating flag ON>
       SET   M9                 // M9: Manual pulse generator operating flag
(10814) LD   X21                // X21: Manual pulse generator operation disable command
       // <Pulse conversion of manual pulse generator operation disable co
       PLS   M10                // M10: Manual pulse generator operation disable command
(10892) LD   M10                // M10: Manual pulse generator operation disable command
       AND   M9                 // M9: Manual pulse generator operating flag
       AND   U1\G31501.0        // U1\G31501.0: BUSY signal (axis 1)
       // <Writing manual pulse generator operation disable>
       MOVP  K0 U1\G4324        // U1\G4324: Manual pulse generator enable flag
       // <Manual pulse generator operating flag OFF>
       RST   M9                 // M9: Manual pulse generator operating flag
```

- Contact types (read from figure): U1\G31501.0 in (10566) is a b contact. U1\G31501.0 in (10892) is an a contact (confirmed by zooming; as printed in the original). The others are a contacts.
- (10566) has DMOVP, MOVP, TOP and SET as parallel outputs under the same condition. (10892) has MOVP and RST as parallel outputs under the same condition.
- The statement at (10814) is cut off at the right edge in the original ("...operation disable co").

#### Speed change program (速度変更プログラム) (12.4 / original p.669)

```
// No.16 Speed change program
(11117) LD   X22                // X22: Speed change command
       // <Pulse conversion of speed change command>
       PLS   M11                // M11: Speed change command pulse
(11213) LD   M11                // M11: Speed change command pulse
       AND   U1\G31501.0        // U1\G31501.0: BUSY signal (axis 1)
       // <Holding the speed change command>
       SET   M12                // M12: Speed change command storage
(11261) LD   M12                // M12: Speed change command storage
       // <Speed change value (90.00 mm/min) setting>
       DMOVP K9000 D11          // D11: Speed change value (low-order 16 bits)
       MPS
       AND   X55                // X55: For unit (degree)
       // <Speed change value (3600.000 degrees/min) setting>
       DMOVP K3600000 D11       // D11: Speed change value (low-order 16 bits)
       MPP
       // <Speed change request setting>
       MOVP  K1 D13             // D13: Speed change request
       // <Writing speed change>
       TOP   H1 K4314 D11 K3    // D11: Speed change value (low-order 16 bits)
       AND=  U1\G4316 K0        // U1\G4316: Speed change request
       // <Speed change request storage OFF>
       RST   M12                // M12: Speed change command storage
```

- Contact types (read from figure): all a contacts.
- (11261) has 5 branches after M12: (no contact)→DMOVP K9000 D11, X55→DMOVP K3600000 D11, (no contact)→MOVP K1 D13, (no contact)→TOP H1 K4314 D11 K3, [= U1\G4316 K0]→RST M12.

#### Override program (オーバーライドプログラム) (12.4 / original p.669)

```
// No.17 Override program
(11404) LD   X23                // X23: Override command
       // <Override command>
       PLS   M13                // M13: Override command
(11471) LD   M13                // M13: Override command
       AND   U1\G31501.0        // U1\G31501.0: BUSY signal (axis 1)
       // <Setting the override value to 200%>
       MOV   K200 D14           // D14: Override value
       // <Writing the override value>
       MOV   D14 U1\G4313       // D14: Override value / U1\G4313: Override
(11563) LD   X50                // X50: Override initialization value command
       // <Override command>
       PLS   M40                // M40: Override initialization value command
(11592) LD   M40                // M40: Override initialization value command
       ANI   U1\G31501.0        // U1\G31501.0: BUSY signal (axis 1)
       // <Setting the override value to the initial value (100%)>
       MOV   K100 D14           // D14: Override value
       // <Writing the override value>
       MOV   D14 U1\G4313       // D14: Override value / U1\G4313: Override
```

- Contact types (read from figure): U1\G31501.0 in (11592) is a b contact. The others, including U1\G31501.0 in (11471), are a contacts.
- The MOV instructions in the original figure are "MOV", not the pulse type (MOVP) (as printed in the original).
- The statement at (11563) is "<Override command>" as printed in the original.

#### Acceleration/deceleration time change program (加減速時間変更プログラム) (12.4 / original p.670)

```
// No.18 Acceleration/deceleration time change program
(11705) LD   X24                // X24: Acceleration/deceleration time change command
       ANI   X25                // X25: Acceleration/deceleration time change disable command
       // <Pulse conversion of acceleration/deceleration time change comma
       PLS   M14                // M14: Acceleration/deceleration time change command
(11854) LD   M14                // M14: Acceleration/deceleration time change command
       AND   U1\G31501.0        // U1\G31501.0: BUSY signal (axis 1)
       // <Setting the acceleration time to 2000 ms>
       DMOV  K2000 D15          // D15: Acceleration time setting (low-order 16 bits)
       // <Setting the deceleration time to no change (0)>
       DMOV  K0 D17             // D17: Deceleration time setting (low-order 16 bits)
       // <Writing acceleration/deceleration time>
       MOVP  K1 D19             // D19: Acceleration/deceleration time change enable
       // <Writing acceleration/deceleration time/change enable>
       TOP   H1 K4308 D15 K5    // D15: Acceleration time setting (low-order 16 bits)
(12093) LD   X25                // X25: Acceleration/deceleration time change disable command
       ANI   X24                // X24: Acceleration/deceleration time change command
       // <Writing acceleration/deceleration time change disable>
       MOVP  K0 U1\G4312
```

- Contact types (read from figure): X25 in (11705) and X24 in (12093) are b contacts. The others are a contacts.
- (11854) has DMOV, DMOV, MOVP and TOP as parallel outputs under the same condition.
- No device comment is shown for the destination U1\G4312 in (12093) (as printed in the original).
- The statement at (11705) is cut off at the right edge in the original ("...time change comma").

#### Torque change program (トルク変更プログラム) (12.4 / original p.670)

```
// No.19 Torque change program
(12166) LD   X26                // X26: Torque change command
       // <Setting the torque change value to 100%>
       MOVP  K1000 D78          // D78: Torque change value
       // <Pulse conversion of  torque change command>
       PLS   M15                // M15: Torque change command
(12318) LD   M15                // M15: Torque change command
       AND   U1\G31501.0        // U1\G31501.0: BUSY signal (axis 1)
       // <Changing the torque limit value>
       MOVP  D78 U1\G4325       // D78: Torque change value
```

- Contact types (read from figure): all a contacts.
- (12166) has MOVP and PLS as parallel outputs under the same condition.
- No device comment is shown for U1\G4325 (as printed in the original).

#### Step operation program (ステップ運転プログラム) (12.4 / original p.671)

```
// No.20 Step operation program
(12369) LD   X27                // X27: Step operation command
       // <Pulse conversion of step operation command>
       PLS   M16                // M16: Step operation command pulse
       // <Setting start program (K10)>
       MOVP  K10 D32            // D32: Start number
(12510) LD   M16                // M16: Step operation command pulse
       ANI   U1\G30104.0        // U1\G30104.0: Positioning start signal (axis 1)
       ANI   U1\G2417.E         // U1\G2417.E: Start complete signal (axis 1)
       // <Selecting to perform step operation>
       MOVP  K1 D20             // D20: Step mode
       // <Data No. unit step mode selection>
       MOVP  K1 D21             // D21: Step valid flag
       // <Step start information (1: Step continuation)>
       MOVP  K1 D22             // D22: Step start information
       // <Writing the step operation command>
       DMOVP D20 U1\G4344       // D20: Step mode / U1\G4344: Step mode
(12720) LD   X46                // X46: Step start information command
       // <To the next positioning data>
       MOVP  D22 U1\G4346       // D22: Step start information
```

- Contact types (read from figure): U1\G30104.0 and U1\G2417.E in (12510) are b contacts. The others are a contacts.
- (12369) has PLS and MOVP as parallel outputs under the same condition. (12510) has MOVP x3 and DMOVP as parallel outputs under the same condition.
- No device comment is shown for U1\G4346 (as printed in the original).

#### Skip program (スキッププログラム) (12.4 / original p.671)

```
// No.21 Skip operation program
(12765) LD   X47                // X47: Positioning start command (K10)
       // <Positioning start number (No.10) setting>
       MOVP  K10 D32            // D32: Start number
(12864) LD   X30                // X30: Skip command
       // <Pulse conversion of skip>
       PLS   M17                // M17: Skip command pulse
(12901) LD   M17                // M17: Skip command pulse
       AND   U1\G31501.0        // U1\G31501.0: BUSY signal (axis 1)
       // <Skip command ON storage>
       SET   M18                // M18: Skip command storage
(12939) LD   M18                // M18: Skip command storage
       // <Writing the skip command>
       MOVP  K1 U1\G4347        // U1\G4347: Skip command
       AND=  U1\G4347 K0        // U1\G4347: Skip command
       // <Skip command storage OFF>
       RST   M18                // M18: Skip command storage
```

- Contact types (read from figure): all a contacts.
- (12939) has 2 branches after M18: (no contact)→MOVP K1 U1\G4347, [= U1\G4347 K0]→RST M18.

#### Teaching program (ティーチングプログラム) (12.4 / original p.672)

```
// No.22 Teaching program
//   (Use manual operation to perform positioning to the target position.)
(13019) LD   X31                // X31: Teaching command
       // <Pulse conversion of teaching command>
       PLS   M19                // M19: Teaching command pulse
(13112) LD   M19                // M19: Teaching command pulse
       ANI   U1\G31501.0        // U1\G31501.0: BUSY signal (axis 1)
       // <Holding the teaching command>
       SET   M20                // M20: Teaching command storage
(13156) LD   M20                // M20: Teaching command storage
       // <Teaching positioning address>
       MOVP  K0 U1\G4348        // U1\G4348: Teaching data selection
       // <Setting the teaching positioning data No.7 to 1>
       MOVP  K1 U1\G4349        // U1\G4349: Teaching positioning data No.
       AND=  U1\G4349 K0        // U1\G4349: Teaching positioning data No.
       // <Teaching command storage OFF>
       RST   M20                // M20: Teaching command storage
```

- Contact types (read from figure): U1\G31501.0 in (13112) is a b contact. The others are a contacts.
- (13156) has 3 branches after M20: (no contact)→MOVP K0 U1\G4348, (no contact)→MOVP K1 U1\G4349, [= U1\G4349 K0]→RST M20.
- The statement "<Setting the teaching positioning data No.7 to 1>" is as printed in the original (the instruction is MOVP K1 U1\G4349).

#### Continuous operation interrupt program (連続運転中断プログラム) (12.4 / original p.672)

```
// No.23 Continuous operation interrupt program
(13309) LD   X32                // X32: Continuous operation interrupt command
       // <Pulse conversion of continuous operation interrupt command>
       PLS   M21                // M21: Continuous operation interrupt command
(13445) LD   M21                // M21: Continuous operation interrupt command
       AND   U1\G31501.0        // U1\G31501.0: BUSY signal (axis 1)
       // <Writing continuous operation interrupt>
       MOVP  K1 U1\G4320        // U1\G4320: Continuous operation interrupt request
```

- Contact types (read from figure): all a contacts.

#### Target position change program (目標位置変更プログラム) (12.4 / original p.673)

```
// No.24 Target position change program
(13609) LD   X45                // X45: Target position change command
       // <Pulse conversion of target position change command>
       PLS   M30                // M30: Target position change command pulse
(13727) LD   M30                // M30: Target position change command pulse
       AND   U1\G31501.0        // U1\G31501.0: BUSY signal (axis 1)
       // <Holding the target position change command>
       SET   M31                // M31: Target position change command storage
(13786) LD   M31                // M31: Target position change command storage
       // <Setting the target position address to -12000.0 μm>
       DMOVP K-120000 D23       // D23: Target position (low-order 16 bits)
       MPS
       AND   X55                // X55: For unit (degree)
       // <Setting the target position address to 300.00000 degrees>
       DMOVP K30000000 D23      // D23: Target position (low-order 16 bits)
       MPP
       // <Speed change (0: Do not change speed)>
       DMOVP K0 D25             // D25: Target speed (low-order 16 bits)
       // <Target position change request setting>
       MOVP  K1 D27             // D27: Target position change request
       // <Writing target position change>
       TOP   H1 K4334 D23 K5    // D23: Target position (low-order 16 bits)
       AND=  U1\G4338 K0        // U1\G4338: Target position change request flag
       // <Target position change command storage OFF>
       RST   M31                // M31: Target position change command storage
```

- Contact types (read from figure): all a contacts.
- (13786) has 6 branches after M31: (no contact)→DMOVP K-120000 D23, X55→DMOVP K30000000 D23, (no contact)→DMOVP K0 D25, (no contact)→MOVP K1 D27, (no contact)→TOP H1 K4334 D23 K5, [= U1\G4338 K0]→RST M31.

#### Restart program (再始動プログラム) (12.4 / original p.673)

```
// No.25 Restart program
(14136) LD   X33                // X33: Restart command
       // <Pulse conversion of restart command>
       PLS   M22                // M22: Restart command
(14222) LD   M22                // M22: Restart command
       AND=  U1\G2409 K1        // U1\G2409: Axis operation status
       // <Restart command ON during stop>
       SET   M23                // M23: Restart command storage
(14271) LD   M23                // M23: Restart command storage
       ANI   U1\G2417.F         // U1\G2417.F: Positioning complete signal (axis 1)
       ANI   U1\G2417.E         // U1\G2417.E: Start complete signal (axis 1)
       // <Writing restart request>
       MOVP  K1 U1\G4303        // U1\G4303: Restart command
       AND=  U1\G4303 K0        // U1\G4303: Restart command
       // <Restart command storage OFF>
       RST   M23                // M23: Restart command storage
```

- Contact types (read from figure): U1\G2417.F and U1\G2417.E in (14271) are b contacts. The others are a contacts.
- (14271) has 2 branches after the 3 contacts: (no contact)→MOVP K1 U1\G4303, [= U1\G4303 K0]→RST M23.

#### Parameter initialization program (パラメータ初期化プログラム) (12.4 / original p.674)

```
// No.26 Parameter initialization program
(14250) LD   X34                // X34: Parameter initialization command
       // <Pulse conversion of parameter initialization command>
       PLS   M24                // M24: Parameter initialization command pulse
(14372) LD   M24                // M24: Parameter initialization command pulse
       ANI   U1\G31501.0        // U1\G31501.0: BUSY signal (axis 1)
       // <Holding the parameter initialization command>
       SET   M25                // M25: Parameter initialization command storage
(14433) LD   M25                // M25: Parameter initialization command storage
       ANI   U1\G5950.0         // U1\G5950.0: PLC READY signal
       // <Waiting for PLC READY output>
       OUT   T0 K2              // T0: PLC READY signal OFF confirmation
(14480) LD   T0                 // T0: PLC READY signal OFF confirmation
       // <Executing parameter initialization>
       MOVP  K1 U1\G5901        // U1\G5901: Parameter initialization request
       AND=  U1\G5901 K0        // U1\G5901: Parameter initialization request
       // <Parameter initialization command storage OFF>
       RST   M25                // M25: Parameter initialization command storage
```

- Contact types (read from figure): U1\G31501.0 in (14372) and U1\G5950.0 in (14433) are b contacts. The others are a contacts.
- (14480) has 2 branches after T0: (no contact)→MOVP K1 U1\G5901, [= U1\G5901 K0]→RST M25.
- The step numbers are as printed in the original figure (confirmed by zooming): the first step of this program (14250) is smaller than the last step of the Restart program (14271).

#### Flash ROM write program (フラッシュROM書込みプログラム) (12.4 / original p.674)

```
// No.27 Flash ROM write program
(14593) LD   X35                // X35: Flash ROM write command
       // <Pulse conversion of flash ROM write command>
       PLS   M26                // M26: Flash ROM write command pulse
(14697) LD   M26                // M26: Flash ROM write command pulse
       ANI   U1\G31501.0        // U1\G31501.0: BUSY signal (axis 1)
       // <Holding the flash ROM write command>
       SET   M27                // M27: Flash ROM write command storage
(14748) LD   M27                // M27: Flash ROM write command storage
       ANI   U1\G5950.0         // U1\G5950.0: PLC READY signal
       // <Waiting for PLC READY output>
       OUT   T1 K2              // T1: PLC READY signal OFF confirmation
(14795) LD   T1                 // T1: PLC READY signal OFF confirmation
       // <Executing flash ROM write>
       MOVP  K1 U1\G5900        // U1\G5900: Flash ROM write request
       AND=  U1\G5900 K0        // U1\G5900: Flash ROM write request
       // <Flash ROM write command storage OFF>
       RST   M27                // M27: Flash ROM write command storage
```

- Contact types (read from figure): U1\G31501.0 in (14697) and U1\G5950.0 in (14748) are b contacts. The others are a contacts.
- (14795) has 2 branches after T1: (no contact)→MOVP K1 U1\G5900, [= U1\G5900 K0]→RST M27.

#### Error reset program (エラーリセットプログラム) (12.4 / original p.675)

```
// No.28 Error reset program
(14972) LD   U1\G2417.D         // U1\G2417.D: Error detection signal (axis 1)
       // <Error code read>
       MOV   U1\G2406 D79       // U1\G2406: Error code / D79: Error code
(15045) LD   X36                // X36: Error reset command
       // <Pulse conversion of error rest command>
       PLS   M28                // M28: Error reset
(15097) LD   M28                // M28: Error reset
       AND   U1\G2417.D         // U1\G2417.D: Error detection signal (axis 1)
       // <Executing error reset>
       MOVP  K1 U1\G4302        // U1\G4302: Error reset
(15137) LD   X54                // X54: Error reset clear command
       // <Executing error reset clear>
       MOVP  K0 U1\G4302        // U1\G4302: Error reset
```

- Contact types (read from figure): all a contacts.
- "error rest command" in the statement at (15045) is as printed in the original.
- Callout in the figure (pointing at X54 "Error reset clear command" of step (15137)):

> When servo amplifier errors cannot be reset even if error reset is requested, "0" is not stored in axis error reset by the Simple Motion module. It remains "1". Set "0" in axis error reset once and then set "1" to execute the error reset again.

This program only stores and resets the error codes.
To also reset warnings, create an OR circuit on step 15097 for Error detection signal (axis 1)G2417.D and Warning detection signal (axis 1)G2417.9.
When necessary, reference step 14972 and create a similar program to store the warning codes.

#### Axis stop program (軸停止プログラム) (12.4 / original p.675)

```
// No.29 Stop program
(15181) LD   X37                // X37: Stop command
       // <Pulse conversion of stop command>
       PLS   M29                // M29: Stop command pulse
(15261) LD   M29                // M29: Stop command pulse
       AND   U1\G31501.0        // U1\G31501.0: BUSY signal (axis 1)
       // <Executing stop>
       SET   U1\G30100.0        // U1\G30100.0: Axis stop signal (axis 1)
(15291) LDI  X37                // X37: Stop command
       ANI   U1\G31501.0        // U1\G31501.0: BUSY signal (axis 1)
       // <Clearing stop>
       RST   U1\G30100.0        // U1\G30100.0: Axis stop signal (axis 1)
```

- Contact types (read from figure): X37 and U1\G31501.0 in (15291) are b contacts. The others are a contacts.
