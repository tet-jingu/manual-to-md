# APPENDICES (付録) (Appendices / original p.821-866)

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

## Conversion range (変換範囲表 / original p.821-866)

| Original page | Section | Handling |
|---|---|---|
| p.821-824 | Appendix 1 How to Find Buffer Memory Addresses (positioning data, block start data, condition data) | Full text |
| p.825 | Appendix 2 Connection with MR-JE-B(F) | Full text |
| p.826-830 | Appendix 2 Inverter FR-A800 series | Full text |
| p.831-837 | Appendix 2 AlphaStep/5-phase stepping motor driver manufactured by ORIENTAL MOTOR Co., Ltd. | Full text |
| p.838-841 | Appendix 2 Servo driver VCII series/VPH series manufactured by CKD NIKKI DENSO CO., LTD. | Full text |
| p.842-846 | Appendix 2 IAI electric actuator controller manufactured by IAI Corporation | Full text |
| p.847-851 | Appendix 2 Connection with MR-J5(W)-B | Full text |
| p.852-855 | Appendix 3 MR-J5(W)-G (Cyclic synchronous mode) connection method | Full text |
| p.856-859 | Appendix 3 MR-J5(W)-G (other than the cyclic synchronous mode) connection method | Full text |
| p.860-864 | Appendix 3 Drive units other than MELSERVO (Cyclic synchronous mode) connection method | Full text |
| p.864 | Appendix 3 MR-JET-G connection method | Full text |
| p.865-866 | Appendix 4 Restrictions by the version | Full text |

## Table of Contents (目次)

- APPENDICES (付録)
- Appendix 1 How to Find Buffer Memory Addresses (バッファメモリアドレスの求め方)
- Appendix 2 Compatible Devices with SSCNETIII(/H) [FX5-SSC-S] (SSCNETIII(/H)対応機器[FX5-SSC-S])
- Appendix 3 Devices Compatible with CC-Link IE TSN [FX5-SSC-G] (CC-Link IE TSN対応機器[FX5-SSC-G])
- Appendix 4 Restrictions by the version (バージョンによる機能の制約)

---

## APPENDICES (付録) (Appendices / original p.821)

## Appendix 1 How to Find Buffer Memory Addresses (バッファメモリアドレスの求め方) (App.1 / original p.821-824)

This section describes how to find the buffer memory addresses of positioning data, block start data, and condition data.

#### Positioning data (位置決めデータ) (App.1 / original p.821-822)

Positioning data No.1 to No.100 are assigned to each axis. Positioning data has the following structure.

[Figure] Buffer memory structure of positioning data (original p.821)
- Notes in the figure (verbatim):
  - Up to 100 positioning data items can be set (stored) for each axis in the buffer memory address shown on the left. No.101 to No.600 are not allocated to buffer memory. Set with the engineering tool. Data is controlled as positioning data No.1 to 600 for each axis.
  - One positioning data item is configured of the items shown in the bold box.
  - n: Axis No. - 1
- Buffer memory addresses shown in the figure (positioning data No.1, No.2, No.99, No.100; No.3 to No.98 are drawn as stacked cards):

| Setting item | Positioning data No.1 | Positioning data No.2 | Positioning data No.99 | Positioning data No.100 |
|---|---|---|---|---|
| Positioning identifier [Da.1] to [Da.4] | 6000+1000n | 6010+1000n | 6980+1000n | 6990+1000n |
| [Da.10] M code/Condition data No./Number of LOOP to LEND repetitions | 6001+1000n | 6011+1000n | 6981+1000n | 6991+1000n |
| [Da.9] Dwell time/JUMP destination positioning data No. | 6002+1000n | 6012+1000n | 6982+1000n | 6992+1000n |
| [Da.8] Command speed | 6004+1000n<br>6005+1000n | 6014+1000n<br>6015+1000n | 6984+1000n<br>6985+1000n | 6994+1000n<br>6995+1000n |
| [Da.6] Positioning address/movement amount | 6006+1000n<br>6007+1000n | 6016+1000n<br>6017+1000n | 6986+1000n<br>6987+1000n | 6996+1000n<br>6997+1000n |
| [Da.7] Arc address | 6008+1000n<br>6009+1000n | 6018+1000n<br>6019+1000n | 6988+1000n<br>6989+1000n | 6998+1000n<br>6999+1000n |
| Axis to be interpolated No. [Da.20] to [Da.22] | 71000+1000n<br>71001+1000n | 71010+1000n<br>71011+1000n | 71980+1000n<br>71981+1000n | 71990+1000n<br>71991+1000n |

*In the original, this is a figure of stacked cards for positioning data No.1 to No.100 ("Buffer memory address" label under the columns). The addresses readable for No.1, No.2, No.99 and No.100 are written out as a table.

[Figure] Configuration of positioning identifier (original p.821)
- Buffer memory b15 to b0:
  - b15 to b8: [Da.2] Control method
  - b7 to b6: [Da.4] Deceleration time No.
  - b5 to b4: [Da.3] Acceleration time No.
  - b1 to b0: [Da.1] Operation pattern
  - (b3 to b2: no assignment shown in the figure)

[Figure] Configuration of axis to be interpolated No. (original p.821)
- Buffer memory b15 to b0:
  - b15 to b8: [Da.21] Axis to be interpolated No.2
  - b7 to b0: [Da.20] Axis to be interpolated No.1
- Buffer memory b31 to b16:
  - b31 to b24: Not used*1
  - b23 to b16: [Da.22] Axis to be interpolated No.3
- *1: Always "0" is set to the part not used.

When setting positioning data using a program, determine buffer memory addresses using the following calculation formula and set the addresses.
- 6000*1 + (1000 × (Ax - 1)) + 10 × (N - 1) + S

*1 The value is 71000 when setting "[Da.20]" to "[Da.22]".

For each variable, substitute a number following the description below. (original p.822)

| Variable | Description |
|---|---|
| Ax | The axis No. of the buffer memory address to be determined. Substitute a number from 1 to 8. |
| N | The positioning data No. of the buffer memory address to be determined. Substitute a number from 1 to 100. |
| S | Substitute one of the following numbers according to the buffer memory address to be determined.<br>• Positioning identifier ([Da.1] to [Da.4], [Da.20] to [Da.22]): 0<br>• [Da.10] M code/Condition data No./Number of LOOP to LEND repetitions: 1<br>• [Da.9] Dwell time/JUMP destination positioning data No.: 2<br>• [Da.8] Command speed (lower 16 bits): 4<br>• [Da.8] Command speed (upper 16 bits): 5<br>• [Da.6] Positioning address/movement amount (lower 16 bits): 6<br>• [Da.6] Positioning address/movement amount (upper 16 bits): 7<br>• [Da.7] Arc address (lower 16 bits): 8<br>• [Da.7] Arc address (upper 16 bits): 9 |

Ex.
When the buffer memory address of "[Da.9] Dwell time/JUMP destination positioning data No." of the positioning data No.1 of axis 2 is determined
6000 + (1000 × (2 - 1)) + 10 × (1 - 1) + 2 = 7002

#### Block start data (ブロック始動データ) (App.1 / original p.822-823)

Block start data consists of five start blocks from Start block 0 to 4, and the block start data of 1 to 50 points is assigned to each block. The start blocks are assigned to each axis. Block start data has the following structure.

[Figure] Buffer memory structure of block start data (Start block 0) (original p.822)
- Notes in the figure (verbatim):
  - Up to 50 block start data points can be set (stored) for each axis in the buffer memory addresses shown on the left.
  - Items in a single unit of block start data are shown included in a bold frame.
  - Each axis has five start blocks (block Nos. 0 to 4). Start block 2 to 4 are not allocated to buffer memory. Set with the engineering tool.
  - n: Axis No. - 1

| Setting item | 1st point | 2nd point | 50th point |
|---|---|---|---|
| b15 to b8: [Da.11] Shape, b7 to b0: [Da.12] Start data No. | 22000+400n | 22001+400n | 22049+400n |
| b15 to b8: [Da.13] Special start instruction, b7 to b0: [Da.14] Parameter | 22050+400n | 22051+400n | 22099+400n |

*In the original, this is a figure of stacked cards for the 1st to 50th points (Start block 0). The addresses readable for the 1st, 2nd and 50th points are written out as a table.

When setting block start data using a program, determine buffer memory addresses using the following calculation formula and set the addresses.

##### [Da.11] Shape, [Da.12] Start data No. ([Da.11]形態，[Da.12]始動データNo.) (App.1 / original p.822-823)

Use the following calculation formula.
- 22000 + (400 × (Ax - 1)) + (200 × M) + (P - 1)

For each variable, substitute a number following the description below.

| Variable | Description |
|---|---|
| Ax | The axis No. of the buffer memory address to be determined. Substitute a number from 1 to 8. |
| M | The start block No. of the buffer memory address to be determined. Substitute a number from 0 to 1. |
| P | The block start data point of the buffer memory address to be determined. Substitute a number from 1 to 50. |

Ex. (original p.823)
When the buffer memory address that satisfies the following conditions is determined
- Axis 3
- Start block No.1
- Block start data point: 40

22000 + (400 × (3 - 1)) + (200 × 1) + (40 - 1) = 23039

##### [Da.13] Special start instruction, [Da.14] Parameter ([Da.13]特殊始動命令，[Da.14]パラメータ) (App.1 / original p.823)

Use the following calculation formula.
- 22050 + (400 × (Ax - 1)) + (200 × M) + (P - 1)

For each variable, substitute a number following the description below.

| Variable | Description |
|---|---|
| Ax | The axis No. of the buffer memory address to be determined. Substitute a number from 1 to 8. |
| M | The start block No. of the buffer memory address to be determined. Substitute a number from 0 to 1. |
| P | The block start data point of the buffer memory address to be determined. Substitute a number from 1 to 50. |

Ex.
When the buffer memory address that satisfies the following conditions is determined
- Axis 2
- Start block No.1
- Block start data point: 25

22050 + (400 × (2 - 1)) + (200 × 1) + (25 - 1) = 22674

#### Condition data (条件データ) (App.1 / original p.823-824)

Condition data consists of five start blocks from Start block 0 to 4, and the condition data No.1 to 10 are assigned to each block. The start blocks are assigned to each axis. Condition data has the following structure.

[Figure] Buffer memory structure of condition data (Start block 0) (original p.823)
- Notes in the figure (verbatim):
  - Up to 10 condition data points can be set (stored) for each block No. in the buffer memory addresses shown on the left.
  - Items in a single unit of condition data are shown included in a bold frame.
  - Each axis has five start blocks (block Nos. 0 to 4). Start block 2 to 4 are not allocated to buffer memory. Set with the engineering tool.
  - n: Axis No. - 1

| Setting item | No.1 | No.2 | No.10 |
|---|---|---|---|
| b15 to b8: [Da.16] Condition operator, b7 to b0: [Da.15] Condition target | 22100+400n | 22110+400n | 22190+400n |
| [Da.17] Address | 22102+400n<br>22103+400n | 22112+400n<br>22113+400n | 22192+400n<br>22193+400n |
| [Da.18] Parameter 1 | 22104+400n<br>22105+400n | 22114+400n<br>22115+400n | 22194+400n<br>22195+400n |
| [Da.19] Parameter 2 | 22106+400n<br>22107+400n | 22116+400n<br>22117+400n | 22196+400n<br>22197+400n |
| b15 to b8: [Da.25] Simultaneously starting axis No.2, b7 to b0: [Da.24] Simultaneously starting axis No.1<br>b31 to b24: [Da.23] Number of simultaneously starting axes, b23 to b16: [Da.26] Simultaneously starting axis No.3 | 22108+400n<br>22109+400n | 22118+400n<br>22119+400n | 22198+400n<br>22199+400n |

*In the original, this is a figure of stacked cards for condition data No.1 to No.10 (Start block 0; arrow labeled "Condition data No."). The addresses readable for No.1, No.2 and No.10 are written out as a table.

When setting block start data using a program, determine buffer memory addresses using the following calculation formula and set the addresses.
- 22100 + (400 × (Ax - 1)) + (200 × M) + (10 × (Q - 1)) + R

*The original says "When setting block start data" here (in the Condition data section), as printed.

For each variable, substitute a number following the description below. (original p.824)

| Variable | Description |
|---|---|
| Ax | The axis No. of the buffer memory address to be determined. Substitute a number from 1 to 8. |
| M | The start block No. of the buffer memory address to be determined. Substitute a number from 0 to 1. |
| Q | The condition data No. of the buffer memory address to be determined. Substitute a number from 1 to 10. |
| R | Substitute one of the following numbers according to the buffer memory address to be determined.<br>• [Da.15] Condition target: 0<br>• [Da.16] Condition operator: 0<br>• [Da.17] Address (lower 16 bits): 2<br>• [Da.17] Address (upper 16 bits): 3<br>• [Da.18] Parameter 1 (lower 16 bits): 4<br>• [Da.18] Parameter 1 (upper 16 bits): 5<br>• [Da.19] Parameter 2 (lower 16 bits): 6<br>• [Da.19] Parameter 2 (upper 16 bits): 7<br>• [Da.23] to [Da.26] Simultaneously starting axis (lower 16 bits): 8<br>• [Da.23] to [Da.26] Simultaneously starting axis (upper 16 bits): 9 |

Ex.
When the buffer memory address that satisfies the following conditions is determined
- Axis 4
- Start block No.1
- Condition data No.5
- [Da.19] Parameter 2 (lower 16 bits)

22100 + (400 × (4 - 1)) + (200 × 1) + (10 × (5 - 1)) + 6 = 23546

## Appendix 2 Compatible Devices with SSCNETIII(/H) [FX5-SSC-S] (SSCNETIII(/H)対応機器[FX5-SSC-S]) (App.2 / original p.825-851)

### Connection with MR-JE-B(F) (MR-JE-B(F)との接続) (App.2 / original p.825)

The servo amplifier MR-JE-B can be connected using SSCNETⅢ/H.

#### Comparisons of specifications with MR-J5(W)-B/MR-J4(W)-B (MR-J5(W)-B/MR-J4(W)-Bとの仕様比較) (App.2 / original p.825)

| Item | | MR-JE-B(F) | MR-J5(W)-B/MR-J4(W)-B |
|---|---|---|---|
| [Pr.100] Servo series | — | 48: MR-JE-_B(F) | 32: MR-J4-_B_(-RJ), MR-J4W_-_B (2-, 3-axis type)<br>128: MR-J5-_B_(-RJ), MR-J5W_-_B (2-, 3-axis type) |
| Detailed parameter 1 | [Pr.116] FLS signal selection | External input signals of servo amplifier are available.*1 | External input signals of servo amplifier are available. |
| Detailed parameter 1 | [Pr.117] RLS signal selection | External input signals of servo amplifier are available.*1 | External input signals of servo amplifier are available. |
| Detailed parameter 1 | [Pr.118] DOG signal selection | External input signals of servo amplifier are available.*1 | External input signals of servo amplifier are available. |
| Encoder resolution | — | 131072 pulses/rev | 4194304 pulses/rev |
| Amplifier-less operation function | — | Possible*3 | Possible*2 |
| Driver communication | — | Not possible | Possible |
| Virtual servo amplifier function | — | Not possible | Possible |

*In the original, "Detailed parameter 1" is merged over 3 rows ([Pr.116] to [Pr.118]), and the value cells of both the MR-JE-B(F) column and the MR-J5(W)-B/MR-J4(W)-B column are merged over the same 3 rows. Expanded to each row. The "Item" cell of the single rows spans the 2 item columns ("—").

*1 When the software version of the servo amplifier is "C4" or before:
When "1: Servo amplifier" is set in "[Pr.116] FLS signal selection" to "[Pr.118] DOG signal selection" at MR-JE-B(F) use, the axis error or warning does not occur and the external signal (upper/lower limit switch, proximity dog) cannot be operated. To use the external input signal at MR-JE-B(F) use, set "2: Buffer memory". Refer to the following for the program and the system configuration.
→Page 321 External Input Signal Select Function

*2 The following servo amplifiers and servo motors are artificially connected during amplifier-less operation.
Other than MR-J5(W)-B
- Servo amplifier type: MR-J4-10B
- Motor type: HG-KR053 (resolution per servo motor rotation: 4194304 pulses/rev)

MR-J5(W)-B
- Servo amplifier type: MR-J5-10B
- Motor type: Rotary servo motor (resolution per servo motor rotation: 4194304 pulses/rev)

*3 Operates artificially as the following servo amplifier and servo motor during amplifier-less operation mode.
Servo amplifier type: MR-J4-10B
Motor type: HG-KR053 (Resolution per servo motor rotation: 4194304 pulses)

> **Restriction**
> The servo amplifier MR-JE-B(F) is integrated with the main circuit power supply and the control power supply. Therefore, when the power of the servo amplifier is turned OFF, the controller cannot communicate with the axes after the axis whose power is turned OFF.

### Inverter FR-A800 series (汎用インバータFR-A800シリーズ) (App.2 / original p.826-830)

FR-A800 series can be connected via SSCNETⅢ/H by using built-in option FR-A8AP and FR-A8NS.

#### Connecting method (接続方法) (App.2 / original p.826-827)

##### System configuration (システム構成) (App.2 / original p.826)

The system configuration using FR-A800 series is shown below.
Set "1: SSCNETⅢ/H" in "[Pr.97] SSCNET setting" to use FR-A800 series.

[Figure] System configuration using FR-A800 series (original p.826)
- Simple Motion module — SSCNETⅢ/H (SSCNETⅢ cable MR-J3BUS_M(-A/-B)) — Inverter FR-A800 series (2 units) — Servo amplifier MR-J5(W)-B/MR-J4(W)-B, connected in a daisy chain in this order. One motor is connected to each device.
- FX5-40SSC-S: Up to 4 axes / FX5-80SSC-S: Up to 8 axes

##### Parameter setting (パラメータ設定) (App.2 / original p.826)

To connect FR-A800 series, execute flash ROM writing after setting the following parameters to buffer memory. The setting value is valid when the power supply is turned ON or the CPU module is reset.
n: Axis No. - 1

| Setting item | | Setting value | Initial value | Buffer memory address |
|---|---|---|---|---|
| [Pr.97] | SSCNET setting | 1: SSCNETⅢ/H | 1 | 106 |
| [Pr.100] | Servo series | 68: FR-A800-1<br>69: FR-A800-2 | 0 | 28400+100n |

*In the original, the "Setting item" header is merged over 2 columns.

##### Control of FR-A800 series parameters (FR-A800シリーズのパラメータ管理) (App.2 / original p.826)

Parameters set in FR-A800 series are not controlled by Simple Motion module. Set the parameters by connecting FR-A800 series directly with the operation panel on the front of inverter (FR-DU08/FR-LU08/FR-PU07) or FR Configurator2 that is inverter setup software. Confirm the instruction manual of FR-A800 series for details of the setting items.

> **Point**
> In the state of connecting between FR-A800 series and Simple Motion module, only a part of parameters can be set if the parameter of the inverter "[Pr.77] Parameter write selection" is in the initial state. Set "2: Write parameters during operation" to rewrite the parameters of FR-A800 series.

##### In-position range (インポジション範囲) (App.2 / original p.826)

Set the servo parameter "In-position range (PA10)" in the parameter of the inverter "[Pr.426] In-position width". When the position of the cam axis is restored in advanced synchronous control, a check is performed by the servo parameter "In-position range" (PA10). However, because the servo parameter settings are not performed in FR-A800 series, the "In-position range" is checked as 100 [pulse] (fixed value).

##### Optional data monitor setting (任意データモニタ設定) (App.2 / original p.827)

The following table shows data types that can be set.

| Data type | Name at FR-A800 series use |
|---|---|
| Effective load ratio | Motor load factor |
| Load inertia moment ratio | Load inertia ratio |
| Model loop gain | Position loop gain |
| Bus voltage | Converter output voltage |
| Encoder multiple revolution counter | Encoder multiple revolution counter |
| Position feedback | Position feedback |
| Encoder position within one revolution | Encoder position within one revolution |
| Optional address of registered monitor | - |

> **Precautions**
> When FR-A800 series is used, each data is delayed for "update delay time + communication cycle" because of the update cycle of the inverter. The following table shows the update delay time of each data.

| Data type | Update delay time of FR-A800 series |
|---|---|
| Effective load ratio | 10 ms |
| Load inertia moment ratio | 10 ms |
| Model loop gain | 10 ms |
| Bus voltage | 5 ms |
| Encoder multiple revolution counter | 222 μs |
| Position feedback | 222 μs |
| Encoder position within one revolution | 222 μs |

##### External input signal (外部入力信号) (App.2 / original p.827)

Set as the following to fetch the external input signal (FLS/RLS/DOG) via FR-A800 series.
- Set "1: Servo amplifier" in "[Pr.116] FLS signal selection", "[Pr.117] RLS signal selection", and "[Pr.118] DOG signal selection".
- Refer to the instruction manual of FR-A800 series for parameter settings on the inverter side.

#### Comparisons of specifications with MR-J5(W)-B/MR-J4(W)-B (MR-J5(W)-B/MR-J4(W)-Bとの仕様比較) (App.2 / original p.828-829)

| Item | | FR-A800 series*1 | MR-J5(W)-B/MR-J4(W)-B |
|---|---|---|---|
| [Pr.100] Servo series | — | 68: FR-A800-1<br>69: FR-A800-2 | 32: MR-J4-_B_(-RJ), MR-J4W_-_B (2-, 3-axis type)<br>128: MR-J5-_B_(-RJ), MR-J5W_-_B (2-, 3-axis type) |
| Control of servo amplifier parameters | — | Set directly by inverter. (Not controlled by Simple Motion module.) | Controlled by Simple Motion module. |
| Detailed parameter 1 | [Pr.116] FLS signal selection | External input signals of FR-A800 series are available. | External input signals of servo amplifier are available. |
| Detailed parameter 1 | [Pr.117] RLS signal selection | External input signals of FR-A800 series are available. | External input signals of servo amplifier are available. |
| Detailed parameter 1 | [Pr.118] DOG signal selection | External input signals of FR-A800 series are available. | External input signals of servo amplifier are available. |
| Extended parameter | [Pr.91] to [Pr.94] Optional data monitor: Data type setting | The following items can be monitored.<br>1: Motor load factor<br>4: Load inertia ratio<br>5: Position loop gain<br>6: Converter output voltage<br>8: Encoder multiple revolution counter<br>20: Position feedback<br>21: Encoder position within one revolution<br>Most significant bit1 + address value: Optional address of registered monitor | The following items can be monitored.<br>1: Effective load ratio<br>2: Regenerative load ratio<br>3: Peak load ratio<br>4: Load inertia moment ratio<br>5: Model loop gain<br>6: Bus voltage<br>7: Servo motor speed<br>8: Encoder multiple revolution counter<br>9: Unit power consumption<br>10: Instantaneous torque<br>12: Servo motor thermistor temperature<br>13: Torque equivalent to disturbance<br>14: Overload alarm margin<br>15: Excessive error alarm margin<br>16: Settling time<br>17: Overshoot amount<br>18: Internal temperature of encoder<br>20: Position feedback<br>21: Encoder position within one revolution<br>22: Selected droop pulse<br>23: Unit total power consumption<br>24: Load-side encoder information 1<br>25: Load-side encoder information 2<br>26: Z-phase counter<br>27: Servo motor side/load-side position deviation<br>28: Servo motor side/load-side speed deviation<br>30: Unit power consumption (2 words)<br>Most significant bit1 + address value: Optional address of registered monitor |
| Absolute position system | — | Not possible | Possible |
| Home position return method | — | Proximity dog method, Count method 1, Count method 2, Data set method, Scale origin signal detection method | Proximity dog method, Count method 1, Count method 2, Data set method, Scale origin signal detection method |
| Positioning control, Expansion control | — | Position control mode, Speed control mode, Torque control mode | Position control mode, Speed control mode, Torque control mode, Continuous operation to torque control mode |
| Gain switching command | — | Valid | Valid |
| PI-PID switching command | — | Valid | Valid |
| Control loop (semi/fully) switching command | — | Invalid | Valid when using servo amplifier for fully closed loop control |
| Servo parameter write/read | — | Not possible | Possible*2 |
| Amplifier-less operation function | — | Possible*3*4 | Possible*3 |
| Driver communication | — | Not possible | Possible*5 |
| Monitoring of servo parameter error No. | — | Not possible | Possible |
| Servo alarm/warning | — | Error codes/warning codes detected by FR-A800 series are stored in "Servo alarm/warning". | Alarm codes/warning codes detected by servo amplifier are stored in "Servo alarm/warning". |
| Programming tool | — | MR Configurator2 is not available.<br>Use FR-DU08/FR-LU08/FR-PU07 or FR Configurator2. | MR Configurator2 is available. |

*In the original, "Detailed parameter 1" is merged over 3 rows ([Pr.116] to [Pr.118]), and the value cells of both columns are merged over the same 3 rows. The "Home position return method" value is one cell merged over the FR-A800 series column and the MR-J5(W)-B/MR-J4(W)-B column. Expanded to each row/column. The "Item" cell of the single rows spans the 2 item columns ("—").

*1 Confirm the specifications of FR-A800 series for details. (original p.829)
*2 Since the servo parameters of MR-J5(W)-B are not in the buffer memory, use GX Works3 or axis control data to set them. For details, refer to the following.
→Page 845 Connection with MR-J5(W)-B
*3 The following servo amplifiers and servo motors are artificially connected during amplifier-less operation.
Other than MR-J5(W)-B
- Servo amplifier type: MR-J4-10B
- Motor type: HG-KR053 (resolution per servo motor rotation: 4194304 pulses/rev)

MR-J5(W)-B
- Servo amplifier type: MR-J5-10B
- Motor type: Rotary servo motor (resolution per servo motor rotation: 4194304 pulses/rev)

*4 Parameters set in FR-A800 series are not controlled by Simple Motion module. Therefore, the operation is the same as when the servo parameter "Rotation direction selection/travel direction selection (PA14)" is set as below during amplifier-less operation mode.

| Servo parameter | | Setting value | Details |
|---|---|---|---|
| PA14 | Rotation direction selection/travel direction selection | 0 | Positioning address increase: CCW or positive direction<br>Positioning address decrease: CW or negative direction |

*In the original, the "Servo parameter" header is merged over 2 columns.

*5 Refer to the manuals of each servo amplifier for the servo amplifiers that can be used.

#### Precautions during control (制御上の注意事項) (App.2 / original p.829)

##### Absolute position system (ABS)/Incremental system (INC) (絶対位置システム(ABS)／インクリメンタルシステム(INC)) (App.2 / original p.829)

When using FR-A800 series, absolute position system (ABS) cannot be used. Even though "1: Enable (used in absolute position detection system)" is set in the servo parameter "Absolute position detection system (PA03)"*1, the servo amplifier operates as incremental system.

*1 For MR-J4(W)-B. "Absolute position detection system selection PA03.0)" for MR-J5(W)-B.
(*As printed: the opening parenthesis before "PA03.0" is missing in the original.)

- When the Simple Motion module is powered ON, home position return request is turned ON and the command position value is set to 0. (The command position value is also set to 0 if only the power of inverter is turned OFF to ON.)
- The warnings at absolute position system "Home position return data incorrect" (warning code: 093CH) and "SSCNET communication error" (warning code: 093EH) are not detected.

##### Control mode (制御モード) (App.2 / original p.829)

Control modes that can be used are shown below.
- Position control mode (speed control including position control and position loop)
- Speed control mode (speed control not including position loop)
- Torque control mode (torque control)

However, it is not available to switch to continuous operation to torque control mode of expansion control "Speed-torque control". If the mode is switched to continuous operation to torque control mode, the error "Continuous operation to torque control not supported" (error code: 19E7H) occurs and the operation stops.
"1: Feedback torque" cannot be set in "Torque initial value selection (b4 to b7)" of "[Pr.90] Operation setting for speed-torque control mode". If it is set, the warning "Torque initial value selection invalid" (warning code: 09E5H) occurs and the command value immediately after switching is the same as the case of selecting "0: Command torque".

##### Servo parameter change request (サーボパラメータ変更要求) (App.2 / original p.829)

Change request of servo parameter ("[Cd.130] Servo parameter read/write request" to "[Cd.132] Change data") cannot be executed. If 1 word/2 words write is executed to FR-A800 series, the parameter write is failure, and "0003H: Read/write failure" is stored in "[Cd.130] Servo parameter read/write request".

##### Driver communication (ドライバ間通信) (App.2 / original p.829)

The driver communication is not supported.

##### Monitor data (モニタデータ) (App.2 / original p.829)

"0" is always stored in "[Md.107] Parameter error No.". Also, "Absolute position lost" ([Md.108] Servo status1: b14) is always turned OFF.

##### Command speed (指令速度) (App.2 / original p.829)

If FR-A800 series is operated at a command speed more than the maximum speed, the stop position may be overshoot.

#### FR-A800 series detection error/warning (FR-A800シリーズが検出したエラー／ワーニング) (App.2 / original p.830)

When an error occurs at FR-A800 series, the error code (1C80H) is stored in "[Md.23] Axis error No.". An alarm No. of FR-A800 series is stored in "[Md.114] Servo alarm". However, "0" is always stored in "[Md.107] Parameter error No.".
When a warning occurs at FR-A800 series, the warning code (0C80H) is stored in "[Md.24] Axis warning No.". A warning No. of FR-A800 series is stored in "[Md.114] Servo alarm". However, "0" is always stored in "[Md.107] Parameter error No.".
Confirm the instruction manual of FR-A800 series for details of errors and warnings.

### AlphaStep/5-phase stepping motor driver manufactured by ORIENTAL MOTOR Co., Ltd. (オリエンタルモーター株式会社製ステッピングモーターユニットαSTEP/5相) (App.2 / original p.831-837)

The ORIENTAL MOTOR Co., Ltd. made stepping motor driver AlphaStep/5-phase can be connected via SSCNETⅢ/H.
For details of stepping motor driver, please contact your nearest Oriental Motor branch or sales office.

#### Connecting method (接続方法) (App.2 / original p.831)

##### System configuration (システム構成) (App.2 / original p.831)

The system configuration using AlphaStep/5-phase is shown below.

[Figure] System configuration using AlphaStep/5-phase (original p.831)
- Simple Motion module — SSCNETⅢ/H (SSCNETⅢ cable MR-J3BUS_M(-A/-B)) — Stepping motor driver AlphaStep/5-Phase (drawn as a multi-axis unit with 4 motors) — Servo amplifier MR-J5(W)-B/MR-J4(W)-B (2 units, one motor each), connected in this order.
- FX5-40SSC-S: Up to 4 axes / FX5-80SSC-S: Up to 8 axes

##### Parameter setting (パラメータ設定) (App.2 / original p.831)

To connect AlphaStep/5-phase, set the following parameters.
n: Axis No.-1

| Setting item | | Setting value | Initial value | Buffer memory address |
|---|---|---|---|---|
| [Pr.100] | Servo series | 97: αSTEP/5-Phase (manufactured by ORIENTAL MOTOR Co., Ltd.) | 0 | 28400+100n |

*In the original, the "Setting item" header is merged over 2 columns.

> **Point**
> All the stepping motor driver axes that can be connected need to be set in the system setting regardless of the number of stepping motors.
> (For example, when a 2-axis unit is used and only 1 motor is connected, the settings for two axes are required in the system setting.)
> Parameters set in AlphaStep/5-phase are not controlled by the Simple Motion module.

#### Comparisons of specifications with MR-J5(W)-B/MR-J4(W)-B (MR-J5(W)-B/MR-J4(W)-Bとの仕様比較) (App.2 / original p.832-833)

| Item | | AlphaStep | 5-phase | MR-J5(W)-B/MR-J4(W)-B |
|---|---|---|---|---|
| [Pr.100] Servo series | — | 97: αSTEP/5-Phase (manufactured by ORIENTAL MOTOR Co., Ltd.) | 97: αSTEP/5-Phase (manufactured by ORIENTAL MOTOR Co., Ltd.) | 32: MR-J4-_B_(-RJ), MR-J4W_-_B (2-, 3-axis type)<br>128: MR-J5-_B_(-RJ), MR-J5W_-_B (2-, 3-axis type) |
| Control of servo amplifier parameters | — | Controlled by AlphaStep | Controlled by 5-phase | Controlled by Simple Motion module. |
| Detailed parameters 1 | [Pr.116] FLS signal selection | External input signals of AlphaStep are available. | External input signals of 5-phase are available. | External input signals of servo amplifier are available. |
| Detailed parameters 1 | [Pr.117] RLS signal selection | External input signals of AlphaStep are available. | External input signals of 5-phase are available. | External input signals of servo amplifier are available. |
| Detailed parameters 1 | [Pr.118] DOG signal selection | External input signals of AlphaStep are available. | External input signals of 5-phase are available. | External input signals of servo amplifier are available. |
| Extended parameters | [Pr.91] to [Pr.94] Optional data monitor: Data type setting | The following items can be monitored.<br>8: Encoder multiple revolution counter<br>20: Position feedback<br>21: Encoder position within one revolution<br>29: External encoder counter value<br>Most significant bit1 + address value: Optional address of registered monitor | The following items can be monitored.<br>8: Encoder multiple revolution counter<br>20: Position feedback<br>21: Encoder position within one revolution<br>29: External encoder counter value<br>Most significant bit1 + address value: Optional address of registered monitor | The following items can be monitored.<br>1: Effective load ratio<br>2: Regenerative load ratio<br>3: Peak load ratio<br>4: Load inertia moment ratio<br>5: Model loop gain<br>6: Bus voltage<br>7: Servo motor speed<br>8: Encoder multiple revolution counter<br>9: Unit power consumption<br>10: Instantaneous torque<br>12: Servo motor thermistor temperature<br>13: Torque equivalent to disturbance<br>14: Overload alarm margin<br>15: Excessive error alarm margin<br>16: Settling time<br>17: Overshoot amount<br>18: Internal temperature of encoder<br>20: Position feedback<br>21: Encoder position within one revolution<br>22: Selected droop pulse<br>23: Unit total power consumption<br>24: Load-side encoder information 1<br>25: Load-side encoder information 2<br>26: Z-phase counter<br>27: Servo motor side/load-side position deviation<br>28: Servo motor side/load-side speed deviation<br>30: Unit power consumption (2 words)<br>Most significant bit1+ address value: Optional address of registered monitor |
| Absolute position system | — | Possible | Not possible | Possible |
| Unlimited length feed | — | Possible | Possible | Possible |
| Home position return method | — | Count method 2, Data set method, Driver home position return method | Count method 2, Data set method, Driver home position return method | Proximity dog method, Count method 1, Count method 2, Data set method, Scale origin signal detection method |
| Positioning control, Expansion control | — | Position control mode | Position control mode | Position control mode, Speed control mode, Torque control mode, Continuous operation to torque control mode |
| Gain switching command | — | Invalid | Invalid | Valid |
| PI-PID switching command | — | Invalid | Invalid | Valid |
| Control loop (semi/fully) switching command | — | Invalid | Invalid | Valid when using servo amplifier for fully closed loop control |
| Amplifier-less operation | — | Not possible*1 | Not possible*1 | Possible*2 |
| Servo parameter change request | — | Possible | Possible | Possible (1 word write*3) |
| Driver communication | — | Not possible | Not possible | Possible |
| Monitoring of servo parameter error No. | — | Not possible | Not possible | Possible |
| Servo alarm/warning | — | Alarm codes/warning codes detected by AlphaStep and operation error codes during driver home position return method are stored in "Servo alarm/warning". | Alarm codes/warning codes detected by 5-phase and operation error codes during driver home position return method are stored in "Servo alarm/warning". | Alarm codes/warning codes detected by servo amplifier are stored in "Servo alarm/warning". |
| [Md.108] Servo status 1 | — | b0: READY ON<br>b1: Servo ON<br>b7: Servo alarm<br>b12: In-position<br>b13: Current cutback<br>b14: Absolute position lost | b0: READY ON<br>b1: Servo ON<br>b7: Servo alarm<br>b12: In-position<br>b13: Current cutback<br>b14: Absolute position lost | b0: READY ON<br>b1: Servo ON<br>b2, b3: Control mode<br>b4: Gain switching<br>b5: Fully closed control switching<br>b7: Servo alarm<br>b12: In-position<br>b13: Torque limit<br>b14: Absolute position lost<br>b15: Servo warning |
| [Md.119] Servo status 2 | — | — | — | b0: Zero passage<br>b3: Zero speed<br>b4: Speed limit<br>b8: PID control |
| [Md.500] Servo status 7 | — | b9: Driver operation alarm | b9: Driver operation alarm | — |
| Programming tool | — | MR Configurator2 is not available.<br>Use AlphaStep data editing software. | MR Configurator2 is not available.<br>Use 5-phase data editing software. | MR Configurator2 is available. |
| Servo input axis type | — | Setting possible (Restrictions*4) | Setting possible (Restrictions*4) | Setting possible |

*In the original, "Detailed parameters 1" is merged over 3 rows ([Pr.116] to [Pr.118]), and the value cells of each of the three device columns are merged over the same 3 rows. Expanded to each row. The "Item" cell of the single rows spans the 2 item columns ("—" in the second column). The table continues from p.832 to p.833 with the header repeated (rows from "Servo parameter change request" are on p.833).

*1 Set as the unconnected status during amplifier-less operation. (original p.833)
*2 The following servo amplifiers and servo motors are artificially connected during amplifier-less operation.
Other than MR-J5(W)-B
- Servo amplifier type: MR-J4-10B
- Motor type: HG-KR053 (resolution per servo motor rotation: 4194304 pulses/rev)

MR-J5(W)-B
- Servo amplifier type: MR-J5-10B
- Motor type: Rotary servo motor (resolution per servo motor rotation: 4194304 pulses/rev)

*3 For MR-J5(W)-B, 2 words write is possible.
*4 When using an absolute position system (ABS), "3: Servo command value" or "4: Feedback value" of the servo input axis type cannot be used. If it is set, the position value of the servo input axis might be not restored correctly. Therefore, set "1: Command position value" or "2: Actual current value" before using.

#### Precautions during control (制御上の注意事項) (App.2 / original p.834-836)

##### Absolute position system (ABS)/Incremental system (INC) (絶対位置システム(ABS)／インクリメンタルシステム(INC)) (App.2 / original p.834)

The ABS/INC setting is performed by the connected AlphaStep/5-phase.
For the INC setting, the restriction is shown below.
- When the power of the Simple Motion module is turned off and on again, "[Md.20] Command position value" is undefined.

##### Home position return (原点復帰) (App.2 / original p.834-835)

The method and some operation of the home position return using the AlphaStep/5-phase differ from those of the home position return using the servo amplifier.
- Home position return method that can be used

○: Possible, ×: Not possible

| [Pr.43] Home position return method | Possible/Not possible |
|---|---|
| Proximity dog method | ×*1 |
| Count method 1 | ×*1 |
| Count method 2 | ○ |
| Data set method | ○ |
| Scale origin signal detection method | ×*1 |
| Driver home position return method | ○ |

*1 The error "Home position return method invalid" (error code: 1979H) occurs and home position return is not performed.

- Driver home position return method

The following shows an operation outline of the home position return method "Driver home position return method".
The home position return is executed based on the positioning pattern set in the AlphaStep/5-phase. Set the setting values of home position return in the parameters of the AlphaStep/5-phase.
The servo external signal status is checked in the AlphaStep/5-phase during the driver home position return.
The Simple Motion module sends the status of upper/lower limit signals and proximity dog signal to the AlphaStep/5-phase at the set values regardless of the logic setting of Simple Motion module.
The operation of home position return and "[Pr.22] Input signal logic selection" of the parameters ([Pr.116] FLS signal selection, [Pr.117] RLS signal selection, and [Pr.118] DOG signal selection) depend on the specification of the AlphaStep/5-phase, so that refer to the AlphaStep/5-phase manual and match the settings. For parameters that can be set by the Simple Motion module, refer to the following.
→Page 411 Setting items for home position return parameters
This method is not available except for the stepping driver. If the method is executed, the error "Home position return method invalid" (error code: 1979H) occurs.

- Backlash compensation after the driver home position return method (original p.835)

When "[Pr.11] Backlash compensation amount" is set in the Simple Motion module, whether the backlash compensation is necessary or not is judged from "[Pr.44] Home position return direction" of the Simple Motion module in the axis operation such as positioning after the driver home position return. When the positioning is executed in the same direction as "[Pr.44] Home position return direction", the backlash compensation is not executed. However, when the positioning is executed in the reverse direction against "[Pr.44] Home position return direction", the backlash compensation is executed.
Note that the home position return is executed based on the home position return direction of the parameter of the AlphaStep/5-phase during the driver home position return. Therefore, set the same direction to "[Pr.44] Home position return direction" of the Simple Motion module and the home position return direction of the parameter of the AlphaStep/5-phase.

[Operation chart]
The machine home position return is started.
(The home position return is executed based on the positioning pattern set in the AlphaStep/5-phase.)

[Figure] Operation chart of the driver home position return method (original p.835)
- V-t: the axis accelerates, runs at constant speed, decelerates to a low speed, then moves briefly in the reverse direction and forward again at low speed before stopping (the motion pattern is the one set in the AlphaStep/5-phase).
- Machine home position return start (Positioning start signal): OFF→ON at the start; turns OFF after the home position return complete flag turns ON.
- Home position return request flag ([Md.31] Status: b3): drawn OFF→ON at the rise of the start signal (arrow from the start signal), and ON→OFF at the end of the home position return (arrow from the complete flag rise).
- Home position return complete flag ([Md.31] Status: b4): OFF during the operation; turns ON at the end of the home position return (at the same timing as the request flag turns OFF). The start signal turns OFF after this (arrow from the complete flag rise to the start signal fall).
- [Md.26] Axis operation status: Standby → Home position return → Standby.
- [Md.20] Command position value / [Md.21] Machine feed value: "Inconsistent" during the home position return → "Home position address" at completion.

##### Servo OFF (サーボOFF) (App.2 / original p.835)

- For 5-phase (open loop control configuration), if the motor is moved by an external force when servo OFF occurs, it is not possible to detect the position and position information is not updated.
- Do not rotate the motors during servo OFF. If the motors are rotated, a position displacement occurs.
- For 5-phase (open loop control configuration), the "Home position return request flag" ([Md.31] Status: b3) turns ON in a servo OFF state. After turning servo ON, perform a home position return again.
- For 5-phase (open loop control configuration), when an encoder is installed, checking position displacement and maladjustments is possible by monitoring "position feedback" and "external encoder counter value" in the optional data monitor. Refer to the manual of AlphaStep/5-phase for the units and increase direction of the encoder count value, and checking methods.

##### Control mode (制御モード) (App.2 / original p.835)

Only position control mode (position control, speed control including position loop, etc.) can be used. Speed control mode and torque control mode of expansion control (speed control not including position loop, torque control, continuous operation to torque control) cannot be used. If a control mode switch is performed, the warning "Illegal control mode switching" (warning code: 09EAH) occurs and the switching is not executed.

##### Servo parameter (サーボパラメータ) (App.2 / original p.836)

- Control of servo parameters

Parameters of AlphaStep/5-phase are not controlled by the Simple Motion module. Therefore, even though the parameter of AlphaStep/5-phase is changed during the communication between the Simple Motion module and AlphaStep/5-phase, the change is not applied to the buffer memory of the Simple Motion module.

- Servo parameter change request

Change request of servo parameter ("[Cd.130] Servo parameter read/write request" to "[Cd.132] Change data") can be executed. The servo parameter of AlphaStep/5-phase is controlled in a unit of 2 words. However, "0001H: 1 word write request" and "0002H: 2 words write request" can be set in "[Cd.130] Servo parameter read/write request".
Refer to the AlphaStep/5-phase manual for the specification method of parameters to change.
When the power of AlphaStep/5-phase is turned off, the parameter changed by the servo parameter change request becomes invalid, and the value written by AlphaStep/5-phase data editing software becomes valid.

##### Optional data monitor (任意データモニタ) (App.2 / original p.836)

The following shows data types that can be set.

| Data type | Unit |
|---|---|
| Encoder multiple revolution counter | [rev] |
| Position feedback (Used point: 2 words) | [pulse] |
| Encoder position within one revolution (Used point: 2 words) | [pulse] |
| External encoder counter value (Used point: 2 words) | [pulse] |
| Optional address of registered monitor | — |

##### Gain switching command, PI-PID switching request, and Semi/Fully closed loop switching request (ゲイン切換え指令，PI-PID切換え要求，セミ・フル切換え要求) (App.2 / original p.836)

Gain switching command, PI-PID switching request, and Semi/Fully closed loop switching request are not available.

##### Driver communication (ドライバ間通信) (App.2 / original p.836)

The driver communication is not supported.
If the driver communication is set in a servo parameter, the setting is ignored.

##### Torque limit (トルク制限) (App.2 / original p.836)

The torque limit set by the Simple Motion module is ignored. Set the torque limit value with the parameter on the driver side.

##### Axis monitor data (軸モニタデータ) (App.2 / original p.836)

- "[Md.104] Motor current value" is always "0".
  "[Md.109] Regenerative load ratio/Optional data monitor output 1", "[Md.110] Effective load torque/Optional data monitor output 2", and "[Md.111] Peak torque ratio/Optional data monitor output 3" become "0" when the optional data monitor is not set.
- "Zero passage" ([Md.119] Servo status 2: b0) is always OFF.
- "Zero speed" ([Md.119] Servo status 2: b3) and "Speed limit" ([Md.119] Servo status 2: b4) are always OFF.
- "[Md.113] Semi/Fully closed loop status" is always "0".
- "[Md.107] Parameter error No." is always "0".
- "In-position" ([Md.108] Servo status 1: b12) is OFF during the axis operation. It is turned ON when the axis operation is completed.

##### Amplifier-less operation (アンプなし運転) (App.2 / original p.836)

The amplifier-less operation cannot be used to the AlphaStep/5-phase axis. If the amplifier-less operation is used, the AlphaStep/5-phase set axis is not connected.

##### In-position range (インポジション範囲) (App.2 / original p.836)

When the position of the cam axis is restored in advanced synchronous control, a check is performed by the servo parameter "In-position range (PA10)". However, because the servo parameter settings are not performed in AlphaStep/5-phase, the "In-position range" is checked as 100 [pulse].

#### AlphaStep/5-phase detection error/warning (αSTEP/5相が検出したエラー／ワーニング) (App.2 / original p.837)

##### Error (エラー) (App.2 / original p.837)

When an error occurs on AlphaStep/5-phase, the error detection signal turns ON, and the error code (1C80H) is stored in "[Md.23] Axis error No.". The servo alarms (0x00 to 0xFF) of AlphaStep/5-phase are stored in "[Md.114] Servo alarm". The alarm detailed No. is not stored. However, "0" is always stored in "[Md.107] Parameter error No.".
When the driver home position return method is selected and a home position return error is detected, the error "Driver home position return error" (error code: 194BH) is stored in "[Md.23] Axis error No.".
Also, "Driver operation alarm" ([Md.500] Servo status 7: b9) is turned ON and the operation alarm generated on the AlphaStep/5-phase is stored in "[Md.502] Driver operation alarm No.".
Confirm the specifications of AlphaStep/5-phase for details.

##### Warning (ワーニング) (App.2 / original p.837)

No warning occurs on AlphaStep/5-phase.

### Servo driver VCII series/VPH series manufactured by CKD NIKKI DENSO CO., LTD. (CKD日機電装株式会社製サーボドライバVCIIシリーズ／VPHシリーズ) (App.2 / original p.838-841)

The direct drive τDISC/τiD roll/τServo compass/τLinear stage, etc. manufactured by CKD NIKKI DENSO CO., LTD. can be controlled by connecting with the servo driver VCⅡ series/VPH series manufactured by the same company using SSCNETⅢ/H.
Contact to CKD NIKKI DENSO overseas sales office for details of VCⅡ series/VPH series.

#### Connecting method (接続方法) (App.2 / original p.838)

##### System configuration (システム構成) (App.2 / original p.838)

The system configuration using VCⅡ series/VPH series is shown below.

[Figure] System configuration using VCⅡ series/VPH series (original p.838)
- Simple Motion module — SSCNETⅢ/H (SSCNETⅢ cable MR-J3BUS_M(-A/-B)) — Servo driver VCⅡ series/VPH series — Servo amplifier MR-J5(W)-B/MR-J4(W)-B (2 units), connected in this order. One motor is connected to each device.
- FX5-40SSC-S: Up to 4 axes / FX5-80SSC-S: Up to 8 axes

##### Parameter setting (パラメータ設定) (App.2 / original p.838)

To connect VCⅡ series/VPH series, set the following parameters.
n: Axis No.-1

| Setting item | | Setting value | Default value | Buffer memory address |
|---|---|---|---|---|
| [Pr.100] | Servo series | 96: VCⅡ series (manufactured by CKD NIKKI DENSO CO., LTD.)<br>99: VPH series (manufactured by CKD NIKKI DENSO CO., LTD.) | 0 | 28400+100n |

*In the original, the "Setting item" header is merged over 2 columns.

> **Point**
> Parameters set in VCⅡ series/VPH series are not controlled by the Simple Motion module.

#### Comparisons of specifications with MR-J5(W)-B/MR-J4(W)-B (MR-J5(W)-B/MR-J4(W)-Bとの仕様比較) (App.2 / original p.839-840)

| Item | | VCII series/VPH series*1 | MR-J5(W)-B/MR-J4(W)-B |
|---|---|---|---|
| [Pr.100] Servo series | — | 96: VCⅡ (manufactured by CKD NIKKI DENSO CO., LTD.)<br>99: VPH (manufactured by CKD NIKKI DENSO CO., LTD.) | 32: MR-J4-_B_(-RJ), MR-J4W_-_B (2-, 3-axis type)<br>128: MR-J5-_B_(-RJ), MR-J5W_-_B (2-, 3-axis type) |
| Control of servo amplifier parameters | — | Controlled by VCⅡ series/VPH series. | Controlled by Simple Motion module. |
| Input filter setting | — | Setting is not available. (fixed to 0.88 ms) | Setting is available. |
| Detailed parameter 1 | [Pr.116] FLS signal selection | External input signals of VCⅡ series/VPH series are available. | External input signals of servo amplifier are available. |
| Detailed parameter 1 | [Pr.117] RLS signal selection | External input signals of VCⅡ series/VPH series are available. | External input signals of servo amplifier are available. |
| Detailed parameter 1 | [Pr.118] DOG signal selection | External input signals of VCⅡ series/VPH series are available. | External input signals of servo amplifier are available. |
| Extended parameter | [Pr.91] to [Pr.94] Optional data monitor: Data type setting | The following items can be monitored.<br>1: Effective load ratio<br>2: Regenerative load ratio<br>3: Peak load ratio<br>5: Position loop gain<br>6: Bus voltage*2<br>8: Encoder multiple revolution counter<br>20: Position feedback<br>21: Encoder position within one revolution<br>Most significant bit1 + address value: Optional address of registered monitor | The following items can be monitored.<br>1: Effective load ratio<br>2: Regenerative load ratio<br>3: Peak load ratio<br>4: Load inertia moment ratio<br>5: Model loop gain<br>6: Bus voltage<br>7: Servo motor speed<br>8: Encoder multiple revolution counter<br>9: Unit power consumption<br>10: Instantaneous torque<br>12: Servo motor thermistor temperature<br>13: Torque equivalent to disturbance<br>14: Overload alarm margin<br>15: Excessive error alarm margin<br>16: Settling time<br>17: Overshoot amount<br>18: Internal temperature of encoder<br>20: Position feedback<br>21: Encoder position within one revolution<br>22: Selected droop pulse<br>23: Unit total power consumption<br>24: Load-side encoder information 1<br>25: Load-side encoder information 2<br>26: Z-phase counter<br>27: Servo motor side/load-side position deviation<br>28: Servo motor side/load-side speed deviation<br>29: External encoder counter value<br>30: Unit power consumption (2 words)<br>Most significant bit1 + address value: Optional address of registered monitor |
| Absolute position system | — | Possible*3 | Possible |
| Unlimited length feed | — | Possible*4 | Possible |
| Home position return method | — | Proximity dog method, Count method 1, Count method 2, Data set method, Scale origin signal detection method | Proximity dog method, Count method 1, Count method 2, Data set method, Scale origin signal detection method |
| Positioning control, Expansion control | — | Position control mode, Speed control mode, Torque control mode | Position control mode, Speed control mode, Torque control mode, Continuous operation to torque control mode |
| Torque limit value change | — | Possible (Separate setting: Restrictions*5) | Possible |
| Gain switching command | — | Valid | Valid |
| PI-PID switching command | — | VCⅡ series: Valid<br>VPH series: Invalid | Valid |
| Control loop (semi/fully) switching command | — | Invalid | Valid when using servo amplifier for fully closed loop control |
| Amplifier-less operation function | — | Possible*6 | Possible*6 |
| Servo parameter change request | — | Possible (2 words write) | Possible (1 word write*7) |
| Driver communication | — | Not possible | Possible*8 |
| Monitoring of servo parameter error No. | — | Not possible | Possible |
| Servo alarm/warning | — | Alarm codes/warning codes detected by VCⅡ series/VPH series are stored in "Servo alarm/warning". | Alarm codes/warning codes detected by servo amplifier are stored in "Servo alarm/warning". |
| Programming tool | — | MR Configurator2 is not available.<br>Use VCⅡ/VPH data editing software. | MR Configurator2 is available. |

*In the original, "Detailed parameter 1" is merged over 3 rows ([Pr.116] to [Pr.118]), and the value cells of both columns are merged over the same 3 rows. The "Home position return method" value is one cell merged over the VCII series/VPH series column and the MR-J5(W)-B/MR-J4(W)-B column. Expanded to each row/column. The "Item" cell of the single rows spans the 2 item columns ("—"). The table continues from p.839 to p.840 with the header repeated (rows "Servo alarm/warning" and "Programming tool" are on p.840).

*1 Confirm the specifications of VCⅡ series/VPH series for details. (original p.840)
*2 It can be monitored when using VPH series.
*3 The direct drive τDISC series manufactured by CKD NIKKI DENSO CO., LTD. can restore the absolute position in the range from -2147483648 to 2147483647. Confirm the specifications of VCⅡ series/VPH series for restrictions by the version of VCⅡ series/VPH series.
*4 When using the virtual encoder pulse number function of VCⅡ series/VPH series, the unlimited length feed is available. When this function is not used, the unlimited length feed is not available. Confirm the specifications of VCⅡ series/VPH series for details of this function.
*5 The specification of torque limit direction differs by the version of VCⅡ series/VPH series. Confirm the specifications of VCⅡ series/VPH series for details.
*6 The following servo amplifiers and servo motors are artificially connected during amplifier-less operation.
Other than MR-J5(W)-B
- Servo amplifier type: MR-J4-10B
- Motor type: HG-KR053 (resolution per servo motor rotation: 4194304 pulses/rev)

MR-J5(W)-B
- Servo amplifier type: MR-J5-10B
- Motor type: Rotary servo motor (resolution per servo motor rotation: 4194304 pulses/rev)

*7 For MR-J5(W)-B, 2 words write is possible.
*8 Refer to the manuals of each servo amplifier for the servo amplifiers that can be used.

#### Precautions during control (制御上の注意事項) (App.2 / original p.840-841)

##### Absolute position system (ABS)/Incremental system (INC) (絶対位置システム(ABS)／インクリメンタルシステム(INC)) (App.2 / original p.840)

The ABS/INC setting is performed by the connected VCⅡ series/VPH series.

##### Unlimited length feed (無限長送り) (App.2 / original p.840)

When using the virtual encoder pulse number function of VCⅡ series/VPH series, the unlimited length feed is available. When this function is not used, the servo alarm 61468 (F01CH) "Absolute encoder over flow error" occurs after "Encoder multiple revolution counter × Encoder resolution + Encoder position within one revolution" exceeds the range of -2147483648 to 2147483647, and the operation stops.

##### Home position return (原点復帰) (App.2 / original p.840)

When "1" is set in the first digit of the parameter of VCⅡ series/VPH series "Select function for SSCNETⅢ on communicate mode", it is possible to carry out the home position return without passing the zero point. (Return to origin after power is supplied will be executed when passing of Motor Z-phase is not necessary.) When "0" is set, the error "Home position return zero point not passed" (error code: 197AH) occurs because the home position return is executed without passing the motor Z-phase (Motor reference position signal).
When the parameter of VPH series "Marker (zero point/Z-phase) transit selection in communication mode (P800)" is set to "Zero return operation allowed", it is possible to carry out the home position return without passing the zero point. When "Zero return operation allowed after the marker is passed" is set, the error "Home position return zero point not passed" (error code: 197AH) occurs because the home position is executed without passing the motor Z-phase.

##### Control mode (制御モード) (App.2 / original p.840)

Control modes that can be used are shown below.
- Position control mode (speed control including position control and position loop)
- Speed control mode (speed control not including position loop)
- Torque control mode (torque control)

However, it is not available to switch to continuous operation to torque control mode of expansion control "Speed-torque control". If the mode is switched to continuous operation to torque control mode, the error "Continuous operation to torque control not supported" (error code: 19E7H) occurs and the operation stops.
"1: Feedback torque" cannot be set in "Torque initial value selection (b4 to b7)" of "[Pr.90] Operation setting for speed-torque control mode". If it is set, the warning "Torque initial value selection invalid" (warning code: 09E5H) occurs and the command value immediately after switching is the same as the case of selecting "0: Command torque".

##### Servo parameter (サーボパラメータ) (App.2 / original p.841)

- Control of servo parameters

Parameters of VCⅡ series/VPH series are not controlled by Simple Motion module. Therefore, even though the parameter of VCⅡ series/VPH series is changed during the communication between Simple Motion module and VCⅡ series/VPH series, it does not reflect to the buffer memory of the Simple Motion module.

- Servo parameter change request

Change request of servo parameter ("[Cd.130] Servo parameter read/write request" to "[Cd.132] Change data") can be executed. However, the servo parameter of VCⅡ series/VPH series is controlled in a unit of 2 words, so that it is necessary to set "0002H: 2 words write request" in "[Cd.130] Servo parameter read/write request" for executing the parameter write. If 1 word write is executed to VCⅡ series/VPH series, the parameter write is failure, and "0003H: Read/write failure" is stored in "[Cd.130] Servo parameter read/write request".
When the servo parameter of VCⅡ series/VPH series is changed by the servo parameter change request, the parameter value after changing the servo parameter cannot be confirmed using VCⅡ/VPH data editing software. Also, when the power of VCⅡ series/VPH series is turned OFF, the parameter changed by the servo parameter change request becomes invalid, and the value written by VCⅡ/VPH data editing software becomes valid.

##### Optional data monitor (任意データモニタ) (App.2 / original p.841)

The following table shows data types that can be set.

| Data type | Unit |
|---|---|
| Effective load ratio | [%] |
| Regenerative load ratio | [%] |
| Peak load ratio | [%] |
| Model loop gain | [rad/s] |
| Bus voltage*1 | [V] |
| Encoder multiple revolution counter | [rev] |
| Position feedback (Used point: 2 words) | [pulse] |
| Encoder position within one revolution (Used point: 2 words) | [pulse] |
| Optional address of registered monitor | — |

*1 It can be monitored when using VPH series.

##### Gain switching command, PI-PID switching request, Semi/Fully closed loop switching request (ゲイン切換え指令，PI-PID切換え要求，セミ・フル切換え要求) (App.2 / original p.841)

Gain switching command and PI-PID switching request are available.
Semi/fully closed loop switching request becomes invalid.

##### Driver communication (ドライバ間通信) (App.2 / original p.841)

The driver communication is not supported. If the driver communication is set in a servo parameter, the error "Driver communication setting error" (error code: 1C93H) will occur when the power is turned ON, and any servo amplifiers including VCⅡ series/VPH series cannot be connected.

#### VCII series/VPH series detection error/warning (VCIIシリーズ／VPHシリーズが検出したエラー／ワーニング) (App.2 / original p.841)

When an error occurs at VCⅡ series/VPH series, the error detection signal turns ON and the error code (1C80H) is stored in "[Md.23] Axis error No.". The servo alarm of VCⅡ series/VPH series (0x00 to 0xFF) is stored in "[Md.114] Servo alarm". The alarm detailed No. is not stored. However, "0" is always stored in "[Md.107] Parameter error No.".
Confirm the specifications of VCⅡ series/VPH series for details of errors and warnings.

### IAI electric actuator controller manufactured by IAI Corporation (株式会社アイエイアイ製IAI電動アクチュエータ用コントローラ) (App.2 / original p.842-846)

The IAI Corporation made IAI electric actuator controller can be connected via SSCNETⅢ/H. Contact your nearest IAI sales office for details of IAI electric actuator controller.

#### Connecting method (接続方法) (App.2 / original p.842)

##### System configuration (システム構成) (App.2 / original p.842)

The system configuration using IAI electric actuator controller is shown below.

[Figure] System configuration using IAI electric actuator controller (original p.842)
- Simple Motion module — SSCNETⅢ/H (SSCNETⅢ cable MR-J3BUS_M(-A/-B)) — IAI electric actuator controller (4 electric actuators connected) — Servo amplifier MR-J5(W)-B/MR-J4(W)-B (2 units, one motor each), connected in this order.
- FX5-40SSC-S: Up to 4 axes / FX5-80SSC-S: Up to 8 axes

##### Parameter setting (パラメータ設定) (App.2 / original p.842)

To connect IAI electric actuator controller, set the following parameters.
n: Axis No.-1

| Setting item | | Setting value | Default value | Buffer memory address |
|---|---|---|---|---|
| [Pr.100] | Servo series | 98: IAI Controller for Electric Actuator (manufactured by IAI Corporation) | 0 | 28400+100n |

*In the original, the "Setting item" header is merged over 2 columns.

> **Point**
> Parameters set in IAI electric actuator controller are not controlled by the Simple Motion module.

#### Comparisons of specifications with MR-J5(W)-B/MR-J4(W)-B (MR-J5(W)-B/MR-J4(W)-Bとの仕様比較) (App.2 / original p.843-844)

| Item | | IAI electric actuator controller | MR-J5(W)-B/MR-J4(W)-B |
|---|---|---|---|
| [Pr.100] Servo series | — | 98: IAI Controller for Electric Actuator (manufactured by IAI Corporation) | 32: MR-J4-_B_(-RJ), MR-J4W_-_B (2-, 3-axis type)<br>128: MR-J5-_B_(-RJ), MR-J5W_-_B (2-, 3-axis type) |
| Control of servo amplifier parameters | — | Controlled by IAI electric actuator controller. | Controlled by Simple Motion module. |
| Detailed parameter 1 | [Pr.116] FLS signal selection | External input signals of IAI electric actuator controller are not available. | External input signals of servo amplifier are available. |
| Detailed parameter 1 | [Pr.117] RLS signal selection | External input signals of IAI electric actuator controller are not available. | External input signals of servo amplifier are available. |
| Detailed parameter 1 | [Pr.118] DOG signal selection | External input signals of IAI electric actuator controller are not available. | External input signals of servo amplifier are available. |
| Extended parameter | [Pr.91] to [Pr.94] Optional data monitor: Data type setting | Most significant bit1 + address value: Optional address of registered monitor | The following items can be monitored.<br>1: Effective load ratio<br>2: Regenerative load ratio<br>3: Peak load ratio<br>4: Load inertia moment ratio<br>5: Model loop gain<br>6: Bus voltage<br>7: Servo motor speed<br>8: Encoder multiple revolution counter<br>9: Unit power consumption<br>10: Instantaneous torque<br>12: Servo motor thermistor temperature<br>13: Torque equivalent to disturbance<br>14: Overload alarm margin<br>15: Excessive error alarm margin<br>16: Settling time<br>17: Overshoot amount<br>18: Internal temperature of encoder<br>20: Position feedback<br>21: Encoder position within one revolution<br>22: Selected droop pulse<br>23: Unit total power consumption<br>24: Load-side encoder information 1<br>25: Load-side encoder information 2<br>26: Z-phase counter<br>27: Servo motor side/load-side position deviation<br>28: Servo motor side/load-side speed deviation<br>30: Unit power consumption (2 words)<br>Most significant bit1 + address value: Optional address of registered monitor |
| Absolute position system | — | Possible | Possible |
| Unlimited length feed | — | Not possible | Possible |
| Home position return method | — | Driver home position return method | Proximity dog method, Count method 1, Count method 2, Data set method, Scale origin signal detection method |
| Positioning control, Expansion control | — | Position control mode | Position control mode, Speed control mode, Torque control mode, Continuous operation to torque control mode |
| Gain switching command | — | Invalid | Valid |
| PI-PID switching command | — | Invalid | Valid |
| Control loop (semi/fully) switching command | — | Invalid | Valid when using servo amplifier for fully closed loop control |
| Amplifier-less operation function | — | Not possible*1 | Possible*2 |
| Servo parameter change request | — | Not possible | Possible (1 word write)*3 |
| Driver communication | — | Not possible | Possible |
| Monitoring of servo parameter error No. | — | Not possible | Possible |
| Servo alarm/warning | — | Alarm codes/warning codes detected by IAI electric actuator controller and operation error codes during driver home position return method are stored in "Servo alarm/warning". | Alarm codes/warning codes detected by servo amplifier are stored in "Servo alarm/warning". |
| [Md.108] Servo status 1 | — | b0: READY ON<br>b1: Servo ON<br>b7: Servo alarm<br>b12: In-position<br>b13: Current cutback | b0: READY ON<br>b1: Servo ON<br>b2 to b3: Control mode<br>b4: Gain switching<br>b5: Fully closed control switching<br>b7: Servo alarm<br>b12: In-position<br>b13: Torque limit<br>b14: Absolute position lost<br>b15: Servo warning |
| [Md.119] Servo status 2 | — | — | b0: Zero passage<br>b3: Zero speed<br>b4: Speed limit<br>b8: PID control |
| [Md.500] Servo status 7 | — | b9: Driver operation alarm | — |
| Programming tool | — | MR Configurator2 is not available.<br>Use IAI electric actuator controller editing software. | MR Configurator2 is available. |

*In the original, "Detailed parameter 1" is merged over 3 rows ([Pr.116] to [Pr.118]), and the value cells of both columns are merged over the same 3 rows. Expanded to each row. The "Item" cell of the single rows spans the 2 item columns ("—" in the second column). The table continues from p.843 to p.844 with the header repeated (rows from "[Md.108] Servo status 1" are on p.844).

*1 Set as the unconnected status during amplifier-less operation. (original p.844)
*2 The following servo amplifiers and servo motors are artificially connected during amplifier-less operation.
Other than MR-J5(W)-B
- Servo amplifier type: MR-J4-10B
- Motor type: HG-KR053 (resolution per servo motor rotation: 4194304 pulses/rev)

MR-J5(W)-B
- Servo amplifier type: MR-J5-10B
- Motor type: Rotary servo motor (resolution per servo motor rotation: 4194304 pulses/rev)

*3 For MR-J5(W)-B, 2 words write is possible.

#### Precautions during control (制御上の注意事項) (App.2 / original p.844-846)

##### Absolute position system (ABS)/Incremental system (INC) (絶対位置システム(ABS)／インクリメンタルシステム(INC)) (App.2 / original p.844)

The ABS/INC setting is performed by the connected IAI electric actuator controller.

##### Home position return (原点復帰) (App.2 / original p.844-845)

The method and some operation of the home position return using the IAI electric actuator controller differ from those of the home position return using the servo amplifier.
- Home position return method that can be used

○: Possible, ×: Not possible

| [Pr.43] Home position return method | Possible/Not possible |
|---|---|
| Proximity dog method | ×*1 |
| Count method 1 | ×*1 |
| Count method 2 | ×*1 |
| Data set method | ×*1 |
| Scale origin signal detection method | ×*1 |
| Driver home position return method | ○ |

*1 The error "Home position return method invalid" (error code: 1979H) occurs and home position return is not performed.

- Driver home position return method

The following shows an operation outline of the home position return method "Driver home position return method".
The home position return is executed based on the positioning pattern set in the IAI electric actuator controller. Set the setting values of home position return in the parameters of the IAI electric actuator controller.
The servo external signal status is checked in the IAI electric actuator controller during the driver home position return.
The Simple Motion module sends the status of upper/lower limit signals and proximity dog signal to the IAI electric actuator controller at the set values regardless of the logic setting of Simple Motion module.
The operation of home position return and "[Pr.22] Input signal logic selection" of the parameters ([Pr.116] FLS signal selection, [Pr.117] RLS signal selection, and [Pr.118] DOG signal selection) depend on the specification of the IAI electric actuator controller, so that refer to the IAI electric actuator controller manual and match the settings. For parameters that can be set by the Simple Motion module, refer to the following.
→Page 411 Setting items for home position return parameters
This method is not available except for the stepping driver (including the IAI electric actuator controller). If the method is executed, the error "Home position return method invalid" (error code: 1979H) occurs. (original p.845)

- Backlash compensation after the driver home position return method

When "[Pr.11] Backlash compensation amount" is set in the Simple Motion module, set the positive direction in "[Pr.44] Home position return direction".

[Operation chart]
The machine home position return is started.
(The home position return is executed based on the positioning pattern set in the IAI electric actuator controller.)

[Figure] Operation chart of the driver home position return method (original p.845)
- V-t: the axis accelerates, runs at constant speed, decelerates to a low speed, then moves in the reverse direction at low speed and stops (the motion pattern is the one set in the IAI electric actuator controller).
- Machine home position return start (Positioning start signal): OFF→ON at the start; turns OFF after the home position return complete flag turns ON.
- Home position return request flag ([Md.31] Status: b3): drawn OFF→ON at the rise of the start signal (arrow from the start signal), and ON→OFF at the end of the home position return (arrow from the complete flag rise).
- Home position return complete flag ([Md.31] Status: b4): OFF during the operation; turns ON at the end of the home position return (at the same timing as the request flag turns OFF). The start signal turns OFF after this (arrow from the complete flag rise to the start signal fall).
- [Md.26] Axis operation status: Standby → Home position return → Standby.
- [Md.20] Command position value / [Md.21] Machine feed value: "Inconsistent" during the home position return → "Home position address" at completion.

##### Servo OFF (サーボOFF) (App.2 / original p.845)

The system is closed loop configuration. If the motor is moved by an external force, the position information is updated.

##### Control mode (制御モード) (App.2 / original p.845)

Position control mode (position control, and speed control including position loop) can be used. Speed control mode and torque control mode of expansion control (speed control not including position loop, torque control, continuous operation to torque control) cannot be used. If a control mode switch is performed, the warning "Illegal control mode switching" (warning code: 09EAH) occurs and the switching is not executed.

##### Servo parameter (サーボパラメータ) (App.2 / original p.845)

- Control of servo parameters

Parameters of IAI electric actuator controller are not controlled by the Simple Motion module. Therefore, even though the parameter of IAI electric actuator controller is changed during the communication between the Simple Motion module and IAI electric actuator controller, the change is not applied to the buffer memory.

##### Optional data monitor (任意データモニタ) (App.2 / original p.845)

The specifiable data types are shown below.

| Data type | Unit |
|---|---|
| Optional address of registered monitor | — |

##### Gain switching command, PI-PID switching request, and Semi/Fully closed loop switching request (ゲイン切換え指令，PI-PID切換え要求，セミ・フル切換え要求) (App.2 / original p.846)

Gain switching command, PI-PID switching request, and Semi/Fully closed loop switching request are not available.

##### Driver communication (ドライバ間通信) (App.2 / original p.846)

The driver communication is not supported.
If the driver communication is set in a servo parameter, the setting is ignored.

##### Axis monitor data (軸モニタデータ) (App.2 / original p.846)

- "[Md.104] Motor current value" is always "0". When the optional data monitor is not used, "[Md.109] Regenerative load ratio/Optional data monitor output 1", "[Md.110] Effective load ratio/Optional data monitor output 2", and "[Md.111] Peak load ratio/Optional data monitor output 3" are "0".
- "Zero passage" ([Md.119] Servo status 2: b0) is always OFF.
- "Zero speed" ([Md.119] Servo status 2: b3) and "Speed limit" ([Md.119] Servo status 2: b4) are always OFF.
- "[Md.113] Semi/Fully closed loop status" is always "0".
- "[Md.107] Parameter error No." is always "0".
- "In-position" ([Md.108] Servo status 1: b12) is OFF during the axis operation. It is turned ON when the axis operation is completed.
- When an unspecifiable data type is set in [Pr.91] Optional data monitor: Data type setting 1" to "[Pr.94] Optional data monitor: Data type setting 4", "0" is stored in "[Md.109] Regenerative load ratio/Optional data monitor output 1" to "[Md.112] Optional data monitor output 4". For the specifiable data, refer to the following. →Page 843 IAI electric actuator controller manufactured by IAI Corporation
  (*As printed: the opening quotation mark before "[Pr.91]" is missing in the original.)

##### Amplifier-less operation (アンプなし運転) (App.2 / original p.846)

The amplifier-less operation cannot be used to the IAI electric actuator controller axis. If the amplifier-less operation is used, the IAI electric actuator controller set axis is not connected.

##### In-position range (インポジション範囲) (App.2 / original p.846)

When the position of the cam axis is restored in advanced synchronous control, a check is performed by the servo parameter "In-position range (PA10)". However, because the servo parameter settings are not performed in IAI electric actuator controller, the "In-position range" is checked as 100 [pulse].

#### IAI electric actuator controller detection error/warning (IAI電動アクチュエータ用コントローラが検出したエラー／ワーニング) (App.2 / original p.846)

##### Error (エラー) (App.2 / original p.846)

When an error occurs on IAI electric actuator controller, the error detection signal turns ON, and the error code (1C80H) is stored in "[Md.23] Axis error No.". The servo alarms (0x00 to 0xFF) of IAI electric actuator controller are stored in "[Md.114] Servo alarm". The alarm detailed No. is not stored. However, "0" is always stored in "[Md.107] Parameter error No.".
When the driver home position return method is selected and a home position return error is detected, the error "Driver home position return error" (error code: 194BH) is stored in "[Md.23] Axis error No.". Also, "Driver operation alarm" ([Md.500] Servo status 7: b9) is turned ON and the operation alarm generated on the IAI electric actuator controller is stored in "[Md.502] Driver operation alarm No.".
Confirm the specifications of IAI electric actuator controller for details.

##### Warning (ワーニング) (App.2 / original p.846)

No warning occurs on IAI electric actuator controller.

### Connection with MR-J5(W)-B (MR-J5(W)-Bとの接続) (App.2 / original p.847-851)

MR-J5(W)-B can be connected via SSCNETⅢ/H.
MR-J5(W)-B has new functions such as battery-less, one-connector/one-touch lock, simple converter, predictive maintenance, quick tuning, machine diagnosis, motor incorrect wiring detection, disconnection detection, and ENC communication diagnosis.

#### System configuration (システム構成) (App.2 / original p.847)

The system configuration using MR-J5(W)-B is shown below.

[Figure] System configuration using MR-J5(W)-B (original p.847)
- Simple Motion module — SSCNETⅢ/H (SSCNETⅢ cable MR-J3BUS_M(-A/-B)) — Servo amplifier MR-J5(W)-B — Servo amplifier MR-J5(W)-B — Servo amplifier MR-J4(W)-B, connected in this order. Each servo amplifier has a motor (M) with encoder (ENC) fed back to the amplifier.
- A "Synchronous encoder via servo amplifier HK-KT motor" (ENC) is connected to the first MR-J5(W)-B.
- FX5-40SSC-S: Up to 4 axes / FX5-80SSC-S: Up to 8 axes

#### Setting method (設定方法) (App.2 / original p.847-850)

##### Servo parameter (サーボパラメータ) (App.2 / original p.847-849)

Since the servo parameters of MR-J5(W)-B are not in the buffer memory, set the servo parameters with one of the following methods.

| Method | details |
|---|---|
| When using GX Works3 | The servo parameters can be set easily.<br>Set the servo parameters in GX Works3 and perform "Write to module". |
| When using the axis control data before the servo parameter transfer | The servo parameters can be set with the sequence program by using the axis control data. The servo parameters can be set even if the servo amplifier is not connected.<br>Refer to the following for details on the write/read method.<br>→Page 846 How to read and write the servo parameter using the axis control data |
| How to change individually the servo parameter after transfer of servo parameter | The servo parameters can be individually changed from Simple Motion module.<br>For details, refer to the following.<br>→Page 847 How to change individually the servo parameter after transfer of servo parameter |

- How to read and write the servo parameter using the axis control data (original p.848)

The following axis control data and setting values are used.
n: Axis No. - 1

| Setting item | | Setting value | Factory-set initial value | Buffer memory address |
|---|---|---|---|---|
| [Cd.130] | Servo parameter read/write request*1 | 0000H: Not request (read/write completion)<br>0003H: Read/write failure<br>0022H: 2 words write request to internal memory<br>0032H: 2 words read request from internal memory | 0 | 4354+100n |
| [Cd.131] | Parameter No. (Setting for servo parameters to be changed) | Set the servo parameter to be changed. | 0000H | 4355+100n |
| [Cd.132] | Change data | Set the changed value of servo parameter set in "[Cd.131] Parameter No.". | 0 | 4356+100n<br>4357+100n |

*In the original, the "Setting item" header is merged over 2 columns.

*1 Refer to the following for details on "0001H: 1 word write request" and "0002H: 2 words write request".
→Page 847 How to change individually the servo parameter after transfer of servo parameter

[How to write the servo parameter using the axis control data]
1. Set the servo parameter No. in "[Cd.131] Parameter No.".
2. Set the setting value for the servo parameter in "[Cd.132] Change data" in 2 words.
3. Set "0022H: 2 words write request to internal memory" in "[Cd.130] Servo parameter read/write request".
4. The Simple Motion module writes "[Cd.132] Change data" to the servo parameter of "[Cd.131] Parameter No.".
   When writing the data succeeds, "[Cd.130] Servo parameter read/write request" becomes "0000H: Not request (read/write completion)".
   When writing the data fails, "[Cd.130] Servo parameter read/write request" becomes "0003H: Read/write failure".
   ("[Cd.130] Servo parameter read/write request" is detected with the continuous detection. Returning "0003H: Read/write failure" to "0000H: Not request (read/write completion)" manually is not required.)
5. The servo parameters written by this method are lost when the power is turned OFF. To save them, backup the execution data. Refer to the following for the details on the execution data backup method.
   →Page 319 Execution Data Backup Function

[Figure] Timing of writing the servo parameter using the axis control data (example: PA03.0) (original p.848)
- Absolute position detection system selection (PA03.0): "0: Disabled (incremental system)" → changes to "1: Enabled (absolute position detection system)" at parameter write completion.
- [Cd.131] Parameter No.: 0 → "0003H: Absolute position detection system selection (PA03.0)".
- [Cd.132] Change data: 0 → "1: Enabled (absolute position detection system)".
- [Cd.130] Servo parameter read/write request: "0000H: Not Request (read/write completion)" → "0022H: 2 words write request to internal memory" (Parameter write start) → "0000H: Not Request (read/write completion)" (Parameter write completion).
- When writing the parameter fails, it becomes "0003H: Read/write failure".
- [Cd.131] and [Cd.132] are set before [Cd.130] is set to 0022H.

Refer to the following for the timing of transferring the written servo parameter to the servo amplifier.
→Page 607 Data transmission process

[How to read the servo parameter using the axis control data] (original p.849)
1. Set the servo parameter No. in "[Cd.131] Parameter No.".
2. Set "0032H: 2 words read request from internal memory" in "[Cd.130] Servo parameter read/write request".
3. The Simple Motion module reads "[Cd.132] Change data" from the servo parameter of "[Cd.131] Parameter No.".
   When reading the data succeeds, "[Cd.130] Servo parameter read/write request" becomes "0000H: Not request (read/write completion)".
   When reading the data fails, "[Cd.130] Servo parameter read/write request" becomes "0003H: Read/write failure".
   ("[Cd.130] Servo parameter read/write request" is detected with the continuous detection. Returning "0003H: Read/write failure" to "0000H: Not request (read/write completion)" manually is not required.)

[Figure] Timing of reading the servo parameter using the axis control data (example: PA03.0) (original p.849)
- Absolute position detection system selection (PA03.0): "1: Enabled (absolute position detection system)" (unchanged).
- [Cd.131] Parameter No.: 0 → "0003H: Absolute position detection system selection (PA03.0)".
- [Cd.132] Change data: 0 → "1: Enabled (absolute position detection system)" at parameter read completion.
- [Cd.130] Servo parameter read/write request: "0000H: Not Request (read/write completion)" → "0032H: 2 words read request from internal memory" (Parameter read start) → "0000H: Not Request (read/write completion)" (Parameter read completion).
- When reading the parameter fails, it becomes "0003H: Read/write failure".

- How to change individually the servo parameter after transfer of servo parameter

The following axis control data and setting values are used.
n: Axis No. - 1

| Setting item | | Setting value | Factory-set initial value | Buffer memory address |
|---|---|---|---|---|
| [Cd.130] | Servo parameter read/write request*1 | 0000H: Not request (read/write completion)<br>0001H: 1 word write request<br>0002H: 2 words write request<br>0003H: Read/write failure | 0 | 4354+100n |
| [Cd.131] | Parameter No. (Setting for servo parameters to be changed) | Set the servo parameter to be changed. | 0000H | 4355+100n |
| [Cd.132] | Change data | Set the changed value of servo parameter set in "[Cd.131] Parameter No.". | 0 | 4356+100n<br>4357+100n |

*In the original, the "Setting item" header is merged over 2 columns.

*1 Refer to the following for details on "0022H: 2 words write request to internal memory" and "0032H: 2 words read request from internal memory".
→Page 846 How to read and write the servo parameter using the axis control data

Since the servo parameters of MR-J5(W)-B are in unit of 2 words, use "0002H: 2 words write request" in "[Cd.130] Servo parameter read/write request". When "0001H: 1 word write request" is used, only the lower 1 word is written. Refer to the following for the setting details.
→Page 612 How to change individually the servo parameter after transfer of servo parameter

##### Servo amplifier electronic gear setting (サーボアンプ電子ギア設定) (App.2 / original p.849-850)

When a rotary servo motor is used with the Simple Motion module, the control is performed with an encoder resolution of 4194304 pulses/rev. Therefore, when a rotary servo motor with an encoder resolution of 67108864 pulses/rev such as an HK-KT motor is used, set 16 in the servo parameter "Electronic gear numerator (PA06)" and 1 in "Electronic gear denominator (PA07)".
For the electronic gears such as "[Pr.2] Number of pulses per rotation (AP)", calculate with an encoder resolution of 4194304 pulses/rev. Refer to the following for the setting details.
→Page 229 Electronic gear function

Ex. (original p.850)
When HK-KT (67108864 pulses/rev) is used

[Figure] Electronic gear when HK-KT (67108864 pulses/rev) is used (original p.850)
- Simple Motion module: Command value [Control unit] → AP / (AL × AM) → pulse → Servo amplifier.
- Servo amplifier: Electronic gear numerator (PA06): 16, Electronic gear denominator (PA07): 1 → pulse × 16 → Motor (M) → Reduction gear → Machine.
- Feedback pulse: ENC → pulse → servo amplifier → pulse/16 → Simple Motion module [Control unit].

If the setting of the servo parameters "Electronic gear numerator (PA06)" and "Electronic gear denominator (PA07)" are different when MR-J5(W)-B is connected, the error "Amplifier electronic gear setting error" (error code: 1C84H) occurs. When the error has occurred, set the servo parameters "Electronic gear numerator (PA06)" and "Electronic gear denominator (PA07)", turn the PLC READY signal OFF to ON, and reconnect the motor with the servo amplifier.
When the error "Amplifier electronic gear setting error" (error code: 1C84H) occurs, the LED display status of the servo amplifier becomes "b_". However, the servo amplifier will not be servo ON status even if "[Cd.191] All axis servo ON" is turned ON.
Any servo amplifiers connected after the one connected to the axis to which the error "Amplifier electronic gear setting error" (error code: 1C84H) has occurred become servo ON status when "[Cd.191] All axis servo ON" is turned ON.

##### Gain switching command (ゲイン切換え指令) (App.2 / original p.850)

- When "1: Gain switching command ON" is set in "[Cd.108] Gain switching command flag", the gain switching is commanded to the servo amplifier, and the load inertia moment ratio and each gain are switched to PB29 to PB36 and PB56 to PB60. "Gain switching" ([Md.108] Servo status: b4) is turned ON during the gain switching.
- When "2: Gain switching 2 command ON" is set in "[Cd.108] Gain switching command flag", the gain switching 2 is commanded to the servo amplifier, and the load inertia moment ratio and each gain are switched to PB67 to PB79. "Gain switching 2" ([Md.127] Servo status 5: b4) is turned on during the gain switching 2.
- The following shows the servo parameters switched by the gain switching and gain switching 2. Refer to the manual of the servo amplifier for details on the gain switching and gain switching 2.

| Control gain | Before gain switching: Servo parameter | Before gain switching: Abbreviation | After gain switching: Servo parameter | After gain switching: Abbreviation | After gain switching 2: Servo parameter | After gain switching 2: Abbreviation |
|---|---|---|---|---|---|---|
| Load to motor inertia ratio/load to motor mass ratio | PB06 | GD2 | PB29 | GD2B | PB67 | GD2C |
| Model control gain | PB07 | PG1 | PB60 | PG1B | PB79 | PG1C |
| Position control gain | PB08 | PG2 | PB30 | PG2B | PB68 | PG2C |
| Speed control gain | PB09 | VG2 | PB31 | VG2B | PB69 | VG2C |
| Speed integral compensation | PB10 | VIC | PB32 | VICB | PB70 | VICC |
| Vibration suppression control 1 - Vibration frequency | PB19 | VRF11 | PB33 | VRF11B | PB71 | VRF11C |
| Vibration suppression control 1 - Resonance frequency | PB20 | VRF12 | PB34 | VRF12B | PB72 | VRF12C |
| Vibration suppression control 1 - Vibration frequency damping | PB21 | VRF13 | PB35 | VRF13B | PB73 | VRF13C |
| Vibration suppression control 1 - Resonance frequency damping | PB22 | VRF14 | PB36 | VRF14B | PB74 | VRF14C |
| Vibration suppression control 2 - Vibration frequency | PB52 | VRF21 | PB56 | VRF21B | PB75 | VRF21C |
| Vibration suppression control 2 - Resonance frequency | PB53 | VRF22 | PB57 | VRF22B | PB76 | VRF22C |
| Vibration suppression control 2 - Vibration frequency damping | PB54 | VRF23 | PB58 | VRF23B | PB77 | VRF23C |
| Vibration suppression control 2 - Resonance frequency damping | PB55 | VRF24 | PB59 | VRF24B | PB78 | VRF24C |

*In the original, the header has 2 rows: "Before gain switching", "After gain switching" and "After gain switching 2" are each merged over 2 sub-columns ("Servo parameter", "Abbreviation"), and "Control gain" is merged over the 2 header rows. Flattened into one header row.

#### Comparisons of specifications with MR-J5(W)-B and MR-J4(W)-B (MR-J5(W)-BとMR-J4(W)-Bとの仕様比較) (App.2 / original p.851)

| Item | MR-J5(W)-B | MR-J4(W)-B |
|---|---|---|
| [Pr.100] Servo series | 128: MR-J5-_B_(-RJ), MR-J5W_-_B (2-, 3-axis type) | 32: MR-J4-_B_(-RJ), MR-J4W_-_B (2-, 3-axis type) |
| Control of servo amplifier parameters | Controlled by Simple Motion module*1<br>(Reading and changing 32 bit parameters are available) | Controlled by Simple Motion module<br>(Reading and changing 32 bit parameters are available) |
| Operation mode | Semi closed loop control system, Fully closed loop control system, Linear servo system, Direct drive servo system | Semi closed loop control system, Fully closed loop control system, Linear servo system, Direct drive servo system |
| Encoder resolution (for semi closed loop control system/fully closed loop control system) | 4194304 pulses/rev*2 | 4194304 pulses/rev |
| HPR method | Proximity dog method, Count method 1, Count method 2, Data set method, Scale origin signal detection method | Proximity dog method, Count method 1, Count method 2, Data set method, Scale origin signal detection method |
| Positioning control, Expansion control | Position control mode, Speed control mode, Torque control mode, Continuous operation to torque control mode | Position control mode, Speed control mode, Torque control mode, Continuous operation to torque control mode |
| Gain switching command | Valid | Valid |
| Gain switching 2 command | Valid | Invalid |
| PI-PID switching command | Valid | Valid |
| Control loop (semi/fully) switching command | Valid when using servo amplifier for fully closed loop control | Valid when using servo amplifier for fully closed loop control |
| Amplifier-less operation function | Possible | Possible |
| Driver communication | Possible | Possible |
| Synchronous encoder via servo amplifier | HK-KT motor<br>(resolution: 4194304 pulses/rev)*3 | HG-KR motor, HG-MR motor, Q171ENC-W8<br>(resolution: 4194304 pulses/rev) |

*In the original, the values of "Operation mode", "HPR method", "Positioning control, Expansion control", "Gain switching command", "PI-PID switching command", "Control loop (semi/fully) switching command", "Amplifier-less operation function" and "Driver communication" are each one cell merged over the MR-J5(W)-B and MR-J4(W)-B columns. Expanded to each column.

*1 The access method of the servo amplifier is different. For details, refer to the following.
→Page 845 Servo parameter
*2 When a rotary servo motor with an encoder resolution of 67108864 pulses/rev such as an HK-KT motor is used, set 16 in the servo parameter "Electronic gear numerator (PA06)" and 1 in "Electronic gear denominator (PA07)" so that the resolution is 4194304 pulses/rev. For details, refer to the following.
→Page 847 Servo amplifier electronic gear setting
*3 Even if an HK-KT motor (encoder resolution: 67108864 pulses/rev) is used, the resolution is changed to 4194304 pulses/rev by the internal processing of the Simple Motion module.

> **Point**
> When a high-precision synchronization at the load side is required for multiple axes, such as the interpolation control and synchronous control, construct a system using the servo amplifiers from the same series.

#### Precautions (注意事項) (App.2 / original p.851)

##### Detection of the servo alarm (サーボアラームの検出) (App.2 / original p.851)

The error "Driver error" (error code: 1C80H) occurs at the time of servo alarm detection, and the warning "Driver warning" (warning code: 0C80H) occurs at the time of servo warning detection. The alarm code and warning code of the servo amplifier are stored in "[Md.114] Servo alarm".
Refer to each servo amplifier manual for details on the errors and warnings detected by the servo amplifier.

## Appendix 3 Devices Compatible with CC-Link IE TSN [FX5-SSC-G] (CC-Link IE TSN対応機器[FX5-SSC-G]) (App.3 / original p.852-864)

### MR-J5(W)-G (Cyclic synchronous mode) connection method (MR-J5(W)-G(サイクリック同期モード)の接続方法) (App.3 / original p.852-855)

This section describes the settings when connecting MR-J5(W)-G with cyclic synchronous mode (csp, csv, and cst) and how to use various functions.
For details about wiring and parameters of MR-J5(W)-G, refer to MR-J5(W)-G manuals.

#### Setting methods (設定方法) (App.3 / original p.852-855)

##### Parameter setting value for using MR-J5(W)-G (MR-J5(W)-Gを使用する場合のパラメータ設定値) (App.3 / original p.852-853)

Set the parameters of MR-J5(W)-G as shown below when executing motion control with MR-J5(W)-G.
When the parameters are not set as shown below, the error "Servo parameter invalid" (error code: 1DC8H) occurs and the values will be rewritten from the controller.

| No. | Name | Default value | Setting value |
|---|---|---|---|
| PA06 | Electronic gear numerator*1 | 1 | • When the resolution of the servo motor is 26 bits: 16<br>(Such as the rotary servo motor HK-KT series)<br>• Other (when not using the rotary servo motor HK-KT series): 1 |
| PA07 | Electronic gear denominator*1 | 1 | 1 |
| PC79.0 | DI status read selection*1 | 0h | Eh |
| PD41.2 | Limit switch enabled status selection*1 | 0h | 1h (only enabled in homing mode) |
| PD41.3 | Sensor input method selection*1 | 0h | 1h (Input from controller (FLS/RLS/DOG)) |
| PD60 | DI pin polarity selection*1 | 00000000h | 00000000h |
| PT01.1 | Speed/acceleration/deceleration unit selection*2 | 0h | 0h |
| PT08 | Homing position data*1 | 0 | 0h |
| PT15 | Software position limit + | 0 | 0 |
| PT17 | Software position limit - | 0 | 0 |
| PT29.0 | Device input polarity 1*1 | 0h | 1h: Dog detection with on |

*1 The parameter is enabled after resetting the Motion module or MR-J5(W)-G.
*2 The parameter is enabled after resetting MR-J5(W)-G.

The setting contents of the servo parameters are shown below. (original p.853)

- External input signal from servo amplifier and buffer memory

[Figure] External input signal from servo amplifier and buffer memory — signal path (original p.853)
- Legend: dark square = Signal selection, light square = Logic selection
- MR-J5(W)-G side: external FLS / RLS / DOG → DI1 / DI2 / DI3 (logic selection "Set in PC79.0") → Digital Inputs: b17 / b18 / b19 (logic selection "Set in PT60.0") → sent to FX5-SSC-G
- FX5-SSC-G side: Digital Inputs: b19 (DOG) is also routed to "External command processing" (logic selection "Set in [Pr.22]")
- FX5-SSC-G side: Digital Inputs: b17 / b18 / b19 and Buffer memory FLS / RLS / DOG (from external FLS / RLS / DOG) enter the signal selection ("Set in [Pr.116] to [Pr.118]"), then logic selection ("Set in [Pr.22]"), and are sent to MR-J5(W)-G as Control DI5: b9 / b10 / b11
- MR-J5(W)-G side: Control DI5: b9 and Control DI5: b10 → Hardware limit processing; Control DI5: b11 → Home position return processing (logic selection "Set in PT29.0")
- *The figure label reads "Set in PT60.0" as printed; the parameter in the tables is PD60 / PD60.0.

- Link device external signal

[Figure] Link device external signal — signal path (original p.853)
- Legend: dark square = Signal selection, light square = Logic selection
- Remote I/O Module: external FLS / RLS / DOG → Link device FLS / Link device RLS / Link device DOG
- FX5-SSC-G: Link device FLS / RLS / DOG → logic selection ("Set in [Pr.913] to [Pr.933]") → signal selection ("Set in [Pr.116] to [Pr.118]") → sent to MR-J5(W)-G as Control DI: b9 / b10 / b11
- MR-J5(W)-G: Control DI: b9 and Control DI: b10 → Hardware limit processing; Control DI: b11 → Home position return processing (logic selection "Set in PT29.0")

Set the following values for the signal logic selection of the servo amplifier.

| No. | Name | Default value | Setting value |
|---|---|---|---|
| PC79.0 | DI status read selection | 0h | Eh: The supported pin No. is shown below.<br>bit1: Returns the ON/OFF status of the DI1 pin.<br>bit2: Returns the ON/OFF status of the DI2 pin.<br>bit3: Returns the ON/OFF status of the DI3 pin. |
| PD60.0 | DI pin polarity selection | 0h | 0h: The supported pin No. is shown below.<br>bit0: DI pin polarity selection 1 (on with V 24 input)<br>bit1: DI pin polarity selection 2 (on with V 24 input)<br>bit2: DI pin polarity selection 3 (on with V 24 input) |
| PT29.0 | Device input polarity 1 | 0h | 1h: Dog detection with on |

*"on with V 24 input" is as printed in the original (i.e. 24 V input).

When "[Pr.118] DOG signal selection" is set to "1: Servo amplifier", the DOG signal at homing is returned and the detection accuracy of the DOG signal may vary because the DOG signal being compared to the DOG signal at detection by the servo amplifier used for communication.
If the detection position accuracy is poor, adjust servo parameters such as "Homing position data (PT08)" and "Travel distance after proximity dog (PT09)" to values that include the communication cycle delay.
In addition, the variety becomes larger when the communication cycle is long.

##### Network parameter setting for using MR-J5(W)-G (MR-J5(W)-Gを使用する場合のネットワークパラメータ設定) (App.3 / original p.853)

Select the motion control station in the network configuration settings when connecting MR-J5(W)-G in the cyclic synchronous mode.

##### PDO mapping for using MR-J5(W)-G (MR-J5(W)-Gを使用する場合のPDOマッピング) (App.3 / original p.854-855)

When MR-J5(W)-G is the motion control station, the Motion module assigns the PDO mapping automatically so that the setting is not needed.
The mapping pattern is as follows.

- TPDO mapping

| Entry No. | Index | Sub Index | Size[bit] | Entry name | Remark |
|---|---|---|---|---|---|
| 1 | 0x1D02 | 0x01 | 16 | Watchdog counter UL 1 | Basic function area (fixed) |
| 2 | 0x6061 | 0x00 | 8 | Modes of operation display | Basic function area (fixed) |
| 3 | 0x0000 | 0x00 | 8 | GAP | Basic function area (fixed) |
| 4 | 0x6064 | 0x00 | 32 | Position actual value | Basic function area (fixed) |
| 5 | 0x606C | 0x00 | 32 | Velocity actual value | Basic function area (fixed) |
| 6 | 0x60F4 | 0x00 | 32 | Following error actual value | Basic function area (fixed) |
| 7 | 0x6041 | 0x00 | 16 | Statusword | Basic function area (fixed) |
| 8 | 0x0000 | 0x00 | 16 | GAP | Basic function area (fixed) |
| 9 | 0x6077 | 0x00 | 16 | Torque actual value | Basic function area (fixed) |
| 10 | 0x2D11 | 0x00 | 16 | Status DO 1 | Basic function area (fixed) |
| 11 | 0x2D12 | 0x00 | 16 | Status DO 2 | Basic function area (fixed) |
| 12 | 0x2D13 | 0x00 | 16 | Status DO 3 | Basic function area (fixed) |
| 13 | 0x2D14 | 0x00 | 16 | Status DO 4 | Basic function area (fixed) |
| 14 | 0x2D15 | 0x00 | 16 | Status DO 5 | Basic function area (fixed) |
| 15 | 0x2A41 | 0x00 | 32 | Current alarm | Basic function area (fixed) |
| 16 | 0x2D21 | 0x00 | 32 | Reserved | Basic function area (fixed) |
| 17 | 0x2D22 | 0x00 | 16 | Reserved | Basic function area (fixed) |
| 18 | 0x60FD | 0x00 | 32 | Digital inputs | Basic function area (fixed) |
| 19 | 0x2B08 | 0x00 | 16 | Regenerative load ratio | Optional data monitor area (when optional data monitor is set as default.)*1 |
| 20 | 0x2B09 | 0x00 | 16 | Effective load ratio | Optional data monitor area (when optional data monitor is set as default.)*1 |
| 21 | 0x2B0A | 0x00 | 16 | Peak load ratio | Optional data monitor area (when optional data monitor is set as default.)*1 |
| 22 | 0x0000 | 0x00 | 16 | GAP | Optional data monitor area (when optional data monitor is set as default.)*1 |
| 23 | 0x2D37 | 0x00 | 32 | Scale ABS counter | Synchronous encoder area via Servo Amplifier*2 |
| 24 | 0x2D36 | 0x00 | 32 | Scale cycle counter | Synchronous encoder area via Servo Amplifier*2 |
| 25 | 0x2D3C | 0x00 | 32 | Scale measurement encoder reception status | Synchronous encoder area via Servo Amplifier*2 |
| 26 | 0x60B9 | 0x00 | 16 | Touch probe status | High accuracy mark detection area |
| 27 | 0x60D1 | 0x00 | 32 | Touch probe time stamp 1 positive value | High accuracy mark detection area |
| 28 | 0x60D2 | 0x00 | 32 | Touch probe time stamp 1 negative value | High accuracy mark detection area |

*In the original, the "Remark" cell is merged over entries 1 to 18, 19 to 22, 23 to 25 and 26 to 28. Expanded to each row.

*1 The mapping changes depending on the setting, "[Pr.91] Optional data monitor: Data type setting 1" to "[Pr.94] Optional data monitor: Data type setting 4" and "[Pr.591] Optional data monitor: Data type expansion setting 1" to "[Pr.594] Optional data monitor: Data type expansion setting 4".
*2 If the function in single-axis servo amplifier is not used, it will become GAP. When using multi-axis servo amplifier (except MR-J5W-G, MR-J5D-G(MR-J5D1-G), it will not be assigned.

- RPDO mapping (original p.855)

| Entry No. | Index | Sub Index | Size[bit] | Entry name | Remark |
|---|---|---|---|---|---|
| 1 | 0x1D01 | 0x01 | 16 | Watchdog counter DL 1 | Basic function area (fixed) |
| 2 | 0x6060 | 0x00 | 8 | Modes of operation | Basic function area (fixed) |
| 3 | 0x0000 | 0x00 | 8 | GAP | Basic function area (fixed) |
| 4 | 0x607A | 0x00 | 32 | Target position | Basic function area (fixed) |
| 5 | 0x60FF | 0x00 | 32 | Target velocity | Basic function area (fixed) |
| 6 | 0x6040 | 0x00 | 16 | Controlword | Basic function area (fixed) |
| 7 | 0x60E0 | 0x00 | 16 | Positive torque limit value | Basic function area (fixed) |
| 8 | 0x60E1 | 0x00 | 16 | Negative torque limit value | Basic function area (fixed) |
| 9 | 0x6071 | 0x00 | 16 | Target torque | Basic function area (fixed) |
| 10 | 0x2D20 | 0x00 | 32 | Velocity limit value | Basic function area (fixed) |
| 11 | 0x2D01 | 0x00 | 16 | Control DI 1 | Basic function area (fixed) |
| 12 | 0x2D02 | 0x00 | 16 | Control DI 2 | Basic function area (fixed) |
| 13 | 0x2D03 | 0x00 | 16 | Control DI 3 | Basic function area (fixed) |
| 14 | 0x2D04 | 0x00 | 16 | Control DI 4 | Basic function area (fixed) |
| 15 | 0x2D05 | 0x00 | 16 | Control DI 5 | Basic function area (fixed) |

*In the original, the "Remark" cell is merged over entries 1 to 15. Expanded to each row.

#### Precautions (注意事項) (App.3 / original p.855)

- When connecting to the MR-J5(W)-G series, use software version A5 or later for the servo amplifier. If an unsupported software version is used, the error "Unsupported servo amplifier connection" (error code: 1A0BH) occurs.
- Set Network Synchronous Communication to "Synchronous". The setting is ignored when "Asynchronous" is set.
- When parameter automatic setting is enabled in the network configuration settings on GX Works3 and the parameter is changed as the same time for multiple stations using MR Configurator2 communication, the changed parameters may not be reflected to the CPU module depending on the communication load condition. Change one station at a time or write the project to the CPU module after starting MR Configuration2 via GX Works3 and changing parameters.
- Motion control is not performed if the IP address of the Motion control station set in Network Configuration Settings is not also set in "[Pr.141] IP address". In this situation, correct the parameter setting.
- A servo alarm [AL.035_Command frequency error] may be detected in MR-J5(W)-G when an operation cycle over occurs on the Motion module during a motor operation and the command differs greatly before the operation cycle over and after a restoration. Check the program and increase the operation cycle setting or decrease the loading if necessary.
- In the "Encoder position during rotation" displayed when monitoring the current position history, the value multiplied by the multiplicative inverse of the electronic gear ratio of the servo amplifier (command unit) is displayed.
- Match the current network configuration setting to the actual system configuration. If there is a difference, the Motion module may not be able to recognize device stations correctly. When disabling any of the axes with the "control axis disable switch function" of a multi-axis servo amplifier, configure the following settings for the disabled axis. Otherwise, the Motion module may not be able to recognize device stations correctly.
  - Set IP address and multidrop number to each "[Pr.141] IP address" and "[Pr.142] Multidrop number".
  - Set "[Pr.101] Virtual servo amplifier setting" to "1: Use as virtual servo amplifier".
- Do not assign MR-J5(W)-G set to CC-Link IE TSN Class A for the axis. If MR-J5(W)-G set to CC-Link IE TSN Class A is assigned for the axis, [AL.19E.2_Control mode setting warning 2] occurs in MR-J5(W)-G when it is connected.

*"changed as the same time" and "MR Configuration2" (next to "MR Configurator2") are as printed in the original. The two sub-items under "Match the current network configuration..." are in a framed box in the original.

### MR-J5(W)-G (other than the cyclic synchronous mode) connection method (MR-J5(W)-G(サイクリック同期モード以外)の接続方法) (App.3 / original p.856-859)

This section describes the settings when connecting MR-J5(W)-G with a mode other than the cyclic synchronous mode and how to use various functions.
For details on wiring and parameters of MR-J5(W)-G, refer to MR-J5(W)-G manuals.
For network settings, refer to "PARAMETER SETTINGS" in the following manual.
[Other manual] MELSEC iQ-F FX5 Motion Module User's Manual (CC-Link IE TSN)
The firmware of MR-J5(W)-G that can be used for other than the cyclic synchronous mode is as follows.

| Device | Mode | Version |
|---|---|---|
| MR-J5(W)-G | Profile mode | A4 or later |
| MR-J5(W)-G | Point table mode | B8 or later |

*In the original, the "Device" cell (MR-J5(W)-G) is merged over the 2 rows. Expanded to each row.

#### Setting method (設定方法) (App.3 / original p.856-858)

An example using two stations for MR-J5(W)-G is shown below. In this example, the 1st station (192.168.3.1) uses the cyclic synchronous mode and the 2nd station (192.168.3.2) uses a mode other than the cyclic synchronous mode.

##### CPU setting [GX Works3] (CPUの設定[GX Works3]) (App.3 / original p.856-858)

1. Set "Motion Control Station", "RWr Setting", and "RWw Setting".

- Operation: Navigation window ⇨ "Parameter" ⇨ "Module Information" ⇨ Target module ⇨ [Module Parameter (Network)] ⇨ [Basic Settings] ⇨ [Network Configuration Settings]

Points of Rwr and RWw that are required for each mode are shown below.

| Mode | RWr | RWw |
|---|---|---|
| Profile mode | 14 points or more | 21 points or more |
| Point table mode | 18 points or more | 13 points or more |

[Figure] CC-Link IE TSN Configuration (Mounting Position No.: 1[U1]) screen (original p.856)
- Station list: No.0 Host Station (STA# 0, Master Station); No.1 MR-J5-G (STA# 1, Remote Station, "Motion Control Station" checked); No.2 MR-J5-G (STA# 2, Remote Station, "Motion Control Station" not checked, RWr Setting Points 16, RWw Setting Points 24)
- Each station has a "Parameter Automatic Setting" check box (not checked) with <Detail Setting>, and "PDO Mapping Setting" <Detail Setting>
- Configuration diagram: Host Station (STA#0 Master Station, Total STA#:2, Line/Star), STA#1 MR-J5-G, STA#2 MR-J5-G (highlighted)
- Callout: "Remove the check in "Motion Control Station" from the station to be used in profile mode."
- Callout: "Set required points or more for each mode in RWr and RWw."

2. Set the PDO mapping pattern selection for the station to be used in a mode other than the cyclic synchronous mode in <Detail Setting> of "PDO Mapping Setting". (original p.857)

[Figure] PDO Mapping Setting <Detail Setting> and PDO Mapping Pattern Selection screens (original p.857)
- CC-Link IE TSN Configuration screen: <Detail Setting> of "PDO Mapping Setting" for station No.2 is selected
- Callout: "The second station is used for a mode other than cyclic synchronous mode, so PDO mapping setting is performed for the second station."
- PDO Mapping Pattern Selection (1/2): "Please select the TPDO mapping pattern assigned in link device (RWr)." Link Device (RWr) Points 16. Patterns: 1 1st Transmit PDO Mapping 21 Points; 2 2nd Transmit PDO Mapping 12 Points; 3 3rd Transmit PDO Mapping 14 Points (selected); 4 4th Transmit PDO Mapping 18 Points. Buttons Back / Next / Cancel
- Callout: "Select the mapping pattern of link device (RWr) that supports each mode and then click "Next"."
- PDO Mapping Pattern Selection (2/2): "Please select the RPDO mapping pattern assigned in link device (RWw)." Link Device (RWw) Points 24. Patterns: 1 1st Receive PDO Mapping 18 Points; 2 2nd Receive PDO Mapping 6 Points; 3 3rd Receive PDO Mapping 21 Points (selected); 4 4th Receive PDO Mapping 13 Points. Buttons Back / OK / Cancel
- Callout: "Select the mapping pattern of link device (RWw) that supports each mode and then click "Next"." (as printed; the button on this screen is "OK")

Mapping pattern setting for each mode is as follows.

| Mode | RWr | RWw |
|---|---|---|
| Profile mode | [No.3] 3rd Transmit PDO Mapping | [No.3] 3rd Receive PDO Mapping |
| Point table mode | [No.4] 4th Transmit PDO Mapping | [No.4] 4th Receive PDO Mapping |

[Figure] PDO Mapping Setting screen (MR-J5-G (Station No. 2), TPDO) (original p.857)
- Left tree: MR-J5-G (Station No. 2) with TPDO (selected) and RPDO
- Link Device Points 16. PDO Mapping Parameter list (Link Device / Index [Hexadecimal] / Sub-Index [Hexadecimal] / Entry Name / Comment / Data Type):
  - RWr0018 / 6061 / 00 / Modes of operation display / INTEGER8
  - next 4 rows: only Entry Name / Data Type readable — Statusword UNSIGNED16, Position actual value INTEGER32, Position actual value INTEGER32, Velocity actual value INTEGER32 (Link Device / Index / Sub-Index hidden by a callout; see original p.857)
  - RWr001c / 606c / 00 / Velocity actual value / INTEGER32
  - RWr001d / 606c / 00 / Velocity actual value / INTEGER32
  - RWr001e / 60f4 / 00 / Following error actual value / INTEGER32
  - RWr001f / 60f4 / 00 / Following error actual value / INTEGER32
  - RWr0020 / 6077 / 00 / Torque actual value / INTEGER16
  - RWr0021 / 2d11 / 00 / Status DO 1 / UNSIGNED16
  - RWr0022 / 2d12 / 00 / Status DO 2 / UNSIGNED16
  - RWr0023 / 2d13 / 00 / Status DO 3 / UNSIGNED16
  - RWr0024 / 2d14 / 00 / Status DO 4 / UNSIGNED16
  - RWr0025 / 2d15 / 00 / Status DO 5 / UNSIGNED16
  - RWr0026, RWr0027: blank
- Callout: "Switch between the TPDO and RPDO setting screens here. This image shows the TPDO setting screen."
- Callout: "Click "PDO Mapping Pattern Selection" to change the PDO mapping patterns for "TPDO" and "RPDO"." ([PDO Mapping Pattern Selection...] button)
- Callout: "Click "OK" when finished making changes."

3. Set the transfer ranges for the link device and the CPU module device for the station to be used for a mode other than the cyclic synchronous mode. (original p.858)

- Operation: Navigation window → "Parameter"→ "Module Information" → Target module → [Module Parameter (Network)] → [Basic Settings] → [Refresh Settings]

[Figure] 1[U1]:FX5-80SSC-G(S) Module Parameter — Refresh Setting screen (original p.858)
- Setting Item List: Required Settings / Basic Settings (Network Configuration Settings, Refresh Setting (selected), Network Topology, Communication Period Setting, Connection Device Information)
- Link Side: SB / SW rows (blank); No.1 RWr, Points 16, Start 00018, End 00027; No.2 RWw, Points 24, Start 00018, End 0002F
- CPU Side: No.1 Target Specify Device, Device Name W, Points 16, Start 00000, End 0000F; No.2 Target Specify Device, Device Name W, Points 24, Start 00010, End 00027
- Callout: "Select "Refresh Setting"."
- Callout: "Set start address and end address of the link device so that it is compatible with the station to be used for a mode other than cyclic synchronous mode."
- Callout: "Set the transfer destination of the link device. The W device is specified in this example."
- Callout: "Set the start address of the transfer destination of the link device. In this example, the transfer is set to W0 to WF for RWr and W10 to W27 for RWw."
- Callout: "When finished setting the network configuration settings and refresh settings, click "Apply"."
- Explanation area (partly hidden): "(The last one of refresh range is displayed if 'Start/End' has been selected for the device assignment method.) [Setting Range] - SB: F to FFFH (multiples of 16 minus 1)" (remaining lines not visible; see original p.858)

4. When controlling the station for a mode other than the cyclic synchronous mode, perform operation with the supported link device for each object.

#### Usage method (使用方法) (App.3 / original p.859)

The following figure describes the process for driving a motor with a mode other than the cyclic synchronous mode

[Figure] Process for driving a motor with a mode other than the cyclic synchronous mode (flowchart) (original p.859)
- Starts
- Connects the Motion module and MR-J5(W)-G with LAN cable
- Power ON the Motion module and MR-J5(W)-G
- Switch MR-J5(W)-G to the mode to be used (Perform during servo-off if the switched mode is profile mode)
  - Note: "Change MR-J5(W)-G to the mode to be used by modifying link device that is assigned Modes of operation from program or watch. For details of the setting value, refer to the manual for MR-J5(W)-G. (e.g.: For changing to pp mode, set link device supporting Modes of operation to "1".)"
- Decision "Switched to the mode?": No → back to the decision (wait); Yes → next
  - Note: "Refer to Modes of operation display and check that the control mode of MR-J5(W)-G is switched."
- Starts operation
- Done

*The lead sentence has no closing period in the original.

#### Precautions (注意事項) (App.3 / original p.859)

- Do not execute servo-on before switching to the profile mode. An improper operation, such as sudden acceleration of the motors, might occur.
- Do not switch to the cyclic synchronous mode after switching to the profile mode. An improper operation, such as sudden acceleration of the motors, might occur.
- When using with a mode other than the cyclic synchronous mode, the Motion module does not perform the limit check, emergency stop command issue, etc. Carry out safety measures at the user's program or MR-J5(W)-G side.
- If the parameter automatic setting is enabled in the Network configuration setting on GX works3, the changed parameters are not reflected to the CPU module even if the parameters are changed using MR Configuration2 communication. If the parameter of the device station is changed, start MR Configuration2 via GX works3 and read the servo parameter.
- Axes must not be set to profile mode. When an axis is set, an error occurs.

*"GX works3" and "MR Configuration2" are as printed in the original.

### Drive units other than MELSERVO (Cyclic synchronous mode) connection method (MELSERVO以外のドライブユニット接続方法(サイクリック同期モード)) (App.3 / original p.860-864)

This section describes the settings when connecting drive units other than MELSERVO (hereinafter referred to as "drive units" in this section) with a unit supporting CC-Link IE TSN compatible with Simple Motion module in the cyclic synchronous mode, and how to use various functions.
For information on connecting drive units other than MELSERVO in the cyclic synchronous mode, download and refer to the connection manuals for the drive unit to be used from the Mitsubishi Electric FA website.

> **Point**
> - Drive units can be connected in the cyclic synchronous mode with the software version 1.007 or later. With the software version 1.006 or earlier, the error "Unsupported device station connection" (error code: 1C4AH) occurs.
> - Drive units compatible with Motion module can be set for the motion control station. If a drive unit not compatible with Motion module is set for the motion control station, the error "Unsupported device station connection" (error code: 1C4AH) occurs when the drive unit is connected.

#### Necessary requirements for connection (接続の必須条件) (App.3 / original p.860-861)

The following are the necessary requirements for connecting the motion system and a drive unit. For details on the drive unit, refer to the manual of the drive unit to be used.

##### Network specification list (ネットワーク仕様一覧) (App.3 / original p.860)

| Network specification | Necessary requirements for drive units |
|---|---|
| Station type | Remote station. |
| Communication cycle | Compatible with the communication cycle supported by Motion module. |
| CC-Link IE TSN Class | CC-Link IE TSN Class B. |
| Communication speed | 1Gbps. |
| PDO mapping | Refer to the following.<br>→Page 858 Object specification list |
| CC-Link IE TSN network synchronous communication | Compatible with CC-Link IE TSN network synchronous communication function. |

##### Object specification list (オブジェクト仕様一覧) (App.3 / original p.860-861)

□: Functionally restricted if supported, △: Functionally restricted if not supported, ×: Cannot be connected if not supported

| Index | Sub Index | Name | Requirements (symbol) | Requirements (details) |
|---|---|---|---|---|
| 6040h | 00h | Controlword | × | — |
| 6041h | 00h | Statusword | × | — |
| 608Fh | 00h | Position encoder resolution | × | — |
| 608Fh | 01h | Encoder increments | × | The encoder connected to the drive unit can be used with a resolution of "2147483647 pulses" or less. |
| 608Fh | 02h | Motor revolutions | × | — |
| 60F4h | 00h | Following error actual value | × | — |
| 607Ch | 00h | Home offset | □ | If supported, the home position return is restricted. For details, refer to the following.<br>→Page 859 List of function restrictions |
| 6080h | 00h | Max motor speed | × | — |
| 6060h | 00h | Modes of operation | × | — |
| 6061h | 00h | Modes of operation display | × | — |
| 6502h | 00h | Supported drive modes | × | Drive units that are compatible with csp can be used. |
| 607Ah | 00h | Target position | × | Drive units with the position command of 32-bit ring counter value can be used. |
| 6064h | 00h | Position actual value | × | Drive units with the position command of 32-bit ring counter value can be used. |
| 60A8h | 00h | SI unit position | □ | • Any unit other than "degree" can be used for the position command unit of the drive unit. If "degree" is set, the error "Driver Position Unit Error" (error code: 1C52H) occurs when the drive unit is connected.<br>• If the position command unit of the drive unit is other than "pulse", set the electronic gear to convert the unit.<br>• If not supported, executed as "pulse". |
| 60A9h | 00h | SI unit velocity | □ | • When Encoder increments or Motor revolutions is set to "0 pulse", units other than "r/min" can be used for the velocity command unit of the drive unit. If "r/min" is set, the error "Driver Speed Unit Error" (error code: 1C53H) occurs when the drive unit is connected.<br>• If not supported, executed as "pulse/s". |
| *1 | *1 | Control DI 5 | △ | If not supported, the external input signal select function is restricted. For details, refer to the following.<br>→Page 859 List of function restrictions |
| *1 | *1 | Encoder status 1 | △ | If not supported, the absolute position system cannot be used. |
| *1 | *1 | Status DO 1 | △ | If not supported, some functions are restricted. For details, refer to the following.<br>→Page 859 List of function restrictions |
| *1 | *1 | Status DO 2 | △ | If not supported, some functions are restricted. For details, refer to the following.<br>→Page 859 List of function restrictions |
| *1 | *1 | Supported Control DI 5 | △ | If not supported, the same restrictions as of Control DI 5 apply. |
| *1 | *1 | Supported Status DO 1 | △ | If not supported, the same restrictions as of Status DO 1 apply. |
| *1 | *1 | Supported Status DO 2 | △ | If not supported, the same restrictions as of Status DO 2 apply. |

*In the original, the header is 2-tier ("Object" over Index / Sub Index / Name), and "Requirements" consists of a symbol column and a details column. "—" = blank in the original. The Index cell 608Fh is merged over the 3 rows Sub Index 00h/01h/02h; the Requirements (symbol and details) of Status DO 1 and Status DO 2 are merged over 2 rows; on the *1 rows, Index and Sub Index are one merged cell. Expanded to each row. The table continues from p.860 to p.861 (p.861 starts at 60A8h).
*"Position actual value (6064h): Drive units with the position command of 32-bit ring counter value can be used." is as printed (same wording as Target position).

*1 Index and Sub Index differ for each drive unit.

#### List of function restrictions (機能制約一覧) (App.3 / original p.861-863)

The following table lists the functions that are restricted in the use of the drive unit. Functions not listed in the following table can be used in the same way as MELSERVO.

| Item 1 | Item 2 | Item 3 | Item 4 | Restrictions | Reference |
|---|---|---|---|---|---|
| Home position return | Machine home position return | — | — | • The home position return can be used if the drive unit is compatible with the homing mode (hm).<br>• If the home position is executed for a drive unit that does not support the homing mode (hm), the error "Driver control mode unsupported" (error code: 1AE7H) occurs.<br>• Set the drive unit parameters so that Home offset (Obj. 607Ch) is "0". If a value other than "0" is set, unintended behavior may occur upon completion of the home position return. | Page 39 Machine Home Position Return |
| Home position return | Fast home position return | — | — | • The home position return can be used if the drive unit is compatible with the homing mode (hm).<br>• If the home position is executed for a drive unit that does not support the homing mode (hm), the error "Driver control mode unsupported" (error code: 1AE7H) occurs.<br>• Set the drive unit parameters so that Home offset (Obj. 607Ch) is "0". If a value other than "0" is set, unintended behavior may occur upon completion of the home position return. | Page 55 Fast Home Position Return |
| Expansion control | Speed control | — | — | • If the drive unit supports the following object, speed control can be used.<br>Target velocity (Obj. 60FFh)<br>• If speed control is executed for a drive unit that does not support cyclic synchronous velocity mode (csv), the error "Driver control mode unsupported" (error code: 1AE7H) occurs. | Page 186 Speed-torque Control |
| Expansion control | Torque control | — | — | • If the drive unit supports the cyclic synchronous torque mode (cst) and the following object, torque control can be used.<br>Target torque (Obj. 6071h)<br>• If torque control is executed for a drive unit that does not support cyclic synchronous torque mode (cst), the error "Driver control mode unsupported" (error code: 1AE7H) occurs. | Page 186 Speed-torque Control |
| Expansion control | Continuous operation to torque control | — | — | Continuous operation to torque control is not supported. If continuous operation to torque control is executed, the error "Driver control mode unsupported" (error code: 1AE7H) occurs. | Page 186 Speed-torque Control |
| Expansion control | Advanced synchronous control | — | — | • Other than "Synchronous encoder via servo amplifier" can be set for "[Pr.320] Synchronous encoder axis type".<br>• If "Synchronous encoder via servo amplifier" is set for "[Pr.320] Synchronous encoder axis type", the error "Synchronous encoder via servo amplifier invalid error" (error code: 1DFAH) occurs. | *1 |
| Control sub functions | Torque limit function | — | — | If the drive unit supports the following objects, the torque limit function can be used.<br>Positive torque limit value (Obj. 60E0h)<br>Negative torque limit value (Obj. 60E1h) | Page 241 Torque limit function |
| Control sub functions | Absolute position system | — | — | • 32-bit restoration is executed. 64-bit restoration is not supported.<br>• If the drive unit supports the following object, the absolute position system can be used.<br>Encoder status 1 (Obj. ****h)*2<br>• If the drive unit is not compatible with the absolute position system, operation is performed with the incremental system.<br>• If the drive unit does not support the following object, the detection result for the absolute position lost of the drive unit is not obtained. "Absolute position lost" ([Md.108] Servo status1: b14) is always OFF.<br>Also, when using the absolute position system, ensure that the drive unit is not in the absolute position lost status before the operation. If the drive unit is in the absolute position lost status, execute the home position return before the operation.<br>Status DO 1 (Obj. ****h): Bit14*2 | Page 278 Absolute Position System |
| Common function | External input signal select function | FLS signal | — | • If the drive unit does not support the following object, "2: Buffer memory" or "3: Link device" cannot be set for "[Pr.116] FLS signal selection". If set, the error "FLS signal selection error" (error code: 1BD0H) occurs.<br>Control DI 5 (Obj. ****h): Bit9*2<br>• After connecting the drive unit, do not change the setting value of "[Pr.116] FLS signal selection". If the value is changed, the Motion module may not detect the FLS signal. | Page 321 External Input Signal Select Function |
| Common function | External input signal select function | RLS signal | — | • If the drive unit does not support the following object, "2: Buffer memory" or "3: Link device" cannot be set for "[Pr.117] RLS signal selection". If set, the error "RLS signal selection error" (error code: 1BD1H) occurs.<br>Control DI 5 (Obj. ****h): Bit10*2<br>• After connecting the drive unit, do not change the setting value of "[Pr.117] RLS signal selection". If the value is changed, the Motion module may not detect the RLS signal. | Page 321 External Input Signal Select Function |
| Common function | External input signal select function | DOG signal | — | • If the drive unit does not support the following object, "2: Buffer memory" or "3: Link device" cannot be set for "[Pr.118] DOG signal selection". If set, the error "DOG signal selection error" (error code: 1BD2H) occurs.<br>Control DI 5 (Obj. ****h): Bit11*2<br>• After connecting the drive unit, do not change the setting value of "[Pr.118] DOG signal selection". If the value is changed, the Motion module may not detect the DOG signal. | Page 321 External Input Signal Select Function |
| Common function | Virtual servo amplifier function | — | — | • Operated as equivalent to MR-J5-G.<br>• The servo motor (HK-KT13W) is virtually used.<br>• Since the encoder resolution of the servo motor actually used is different, the speed is different from that of the actual device configuration. | Page 347 Virtual servo amplifier function [FX5-SSC-G] |
| Common function | Mark detection function | — | — | TPR1 of the drive unit other than MELSERVO cannot be set in "[Pr.800] Mark detection signal setting". If set, the warning "Outside mark detection signal setting range" (warning code: 0D36H) will occur. | Page 355 Mark Detection Function |
| Common function | Optional data monitor function | — | — | If "[Pr.91] Optional data monitor: Data type setting 1" to "[Pr.94] Optional data monitor: Data type setting 4" and "[Pr.591] Optional data monitor: Data type expansion setting 1" to "[Pr.594] Optional data monitor: Data type expansion setting 4" are not set, "[Md.109] Regenerative load ratio/Optional data monitor output 1" to "[Md.112] Optional data monitor output 4" are always "0". | Page 371 Optional Data Monitor Function |
| Parameter setting | Module parameter | — | — | The setting method differs for each drive unit. For details, download and refer to the connection manuals for each drive unit from the Mitsubishi Electric FA website. | — |
| Data used for positioning control | Basic settings | [Pr.116] FLS signal selection<br>[Pr.117] RLS signal selection<br>[Pr.118] DOG signal selection | — | Refer to the following.<br>→Page 321 External Input Signal Select Function | Page 469 [Pr.116] to [Pr.119] FLS/RLS/DOG/STOP signal selection |
| Data used for positioning control | Basic settings | [Pr.140] Driver command discard detection setting | — | • Set "1: Detection valid". If "0: Detection invalid" is set, an error does not occur even when bit 12 in "[Md.117] Statusword turns ON → OFF, and Motion module cannot stop the command.<br>• When bit 12 in "[Md.117] Statusword turns ON → OFF and the distance between Motion module and drive unit becomes far, make sure to follow up. | Page 444 [Pr.140] Driver command discard detection setting |
| Data used for positioning control | Monitor data | [Md.103] Motor rotation speed | — | • The value of the following object is output. Always 0 if the drive unit does not support the following object.<br>Velocity actual value (Obj. 606Ch)<br>• The motor rotation speed is output in units corresponding to the value of the following object.<br>SI unit velocity (Obj. 60A9h) | Page 547 [Md.103] Motor rotation speed |
| Data used for positioning control | Monitor data | [Md.104] Motor current value | — | The value of the following object is output. Always 0 if the drive unit does not support the following object.<br>Torque actual value (Obj. 6077h) | Page 547 [Md.104] Motor current value |
| Data used for positioning control | Monitor data | [Md.108] Servo status1 | Gain switching | Always OFF. | Page 550 [Md.108] Servo status1 |
| Data used for positioning control | Monitor data | [Md.108] Servo status1 | Fully closed loop control switching | Always OFF. | Page 550 [Md.108] Servo status1 |
| Data used for positioning control | Monitor data | [Md.108] Servo status1 | In-position | The value of the following object is output. Always OFF if the drive unit does not support the following object.<br>Status DO 1: Bit12 | Page 550 [Md.108] Servo status1 |
| Data used for positioning control | Monitor data | [Md.108] Servo status1 | Torque limit | The value of the following object is output. Always OFF if the drive unit does not support the following object.<br>Status DO 1: Bit13 | Page 550 [Md.108] Servo status1 |
| Data used for positioning control | Monitor data | [Md.108] Servo status1 | Absolute position lost | The value of the following object is output. Always OFF if the drive unit does not support the following object.<br>Status DO 1: Bit14 | Page 550 [Md.108] Servo status1 |
| Data used for positioning control | Monitor data | [Md.108] Servo status1 | Servo warning | The value of the following object is output. Always OFF if the drive unit does not support the following object.<br>Statusword (Obj. 6040h): Bit7 | Page 550 [Md.108] Servo status1 |
| Data used for positioning control | Monitor data | [Md.119] Servo status2 | Zero point pass | The value of the following object is output. Always OFF if the drive unit does not support the following object.<br>Status DO 2: Bit0 | Page 555 [Md.119] Servo status2 |
| Data used for positioning control | Monitor data | [Md.119] Servo status2 | Zero speed | The value of the following object is output. Always ON if the drive unit does not support the following object.<br>Status DO 2: Bit3 | Page 555 [Md.119] Servo status2 |
| Data used for positioning control | Monitor data | [Md.119] Servo status2 | Speed limit | The value of the following object is output. Always OFF if the drive unit does not support the following object.<br>Status DO 2: Bit4 | Page 555 [Md.119] Servo status2 |
| Data used for positioning control | Monitor data | [Md.119] Servo status2 | PID control | Always OFF. | Page 555 [Md.119] Servo status2 |
| Data used for positioning control | Monitor data | [Md.115] Servo alarm detail number | — | Always "0". | Page 554 [Md.115] Servo alarm detail number [FX5-SSC-G] |
| Data used for positioning control | Control data | [Cd.108] Gain switching command flag | — | Not compatible with gain switching. A command is not sent to the drive unit even when the setting value is changed. | Page 587 [Cd.108] Gain switching command flag |
| Data used for positioning control | Control data | [Cd.133] Semi/Fully closed loop switching request | — | Not compatible with semi/fully closed loop switching. A command is not sent to the drive unit even when the setting value is changed. | Page 590 [Cd.133] Semi/Fully closed loop switching request |
| Data used for positioning control | Control data | [Cd.136] PI-PID switching request | — | Not compatible with PI-PID switching. A command is not sent to the drive unit even when the setting value is changed. | Page 591 [Cd.136] PI-PID switching request |

*In the original, "Item" is a hierarchy of up to 4 levels; the upper-level item cells (Home position return / Expansion control / Control sub functions / Common function / Parameter setting / Data used for positioning control, and External input signal select function / Basic settings / Monitor data / Control data / [Md.108] Servo status1 / [Md.119] Servo status2) are merged vertically. "—" in the Item 3/4 columns = no such level in the original. The "Restrictions" cell of Machine home position return / Fast home position return is merged over 2 rows; the "Reference" cell "Page 186 Speed-torque Control" is merged over the 3 rows Speed control / Torque control / Continuous operation to torque control; "Page 321 External Input Signal Select Function" is merged over the 3 rows FLS / RLS / DOG signal; "Page 550 [Md.108] Servo status1" is merged over its 6 rows and "Page 555 [Md.119] Servo status2" over its 4 rows. Expanded to each row. The Reference "—" of Parameter setting is printed as "—" in the original. The table continues from p.861 to p.863.
*As printed in the original: the closing quotation mark after "[Md.117] Statusword" is missing (2 places); "Statusword (Obj. 6040h): Bit7" (the TPDO/RPDO tables list Statusword as 0x6041 and Controlword as 0x6040); "If the home position is executed" (without "return").

*1 Refer to the following manual.
[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Advanced Synchronous Control)
*2 Index differs for each drive unit.

#### Precautions (注意事項) (App.3 / original p.864)

Connect a drive unit as set in the network configuration settings. If a drive unit different from the one set in the network configuration settings is connected, the error "Network Configuration Settings not match" (error code: 1C55H) occurs.

### MR-JET-G connection method (MR-JET-Gの接続方法) (App.3 / original p.864)

This section describes how to set when connecting MR-JET-G and use various functions.
For details about wiring and parameters of MR-JET-G, refer to MR-JET-G manuals.

#### Parameter setting value when using MR-JET-G (MR-JET-Gを使用する場合のパラメータ設定値) (App.3 / original p.864)

Set the parameters of MR-JET-G as shown below when executing motion control with MR-JET-G.
When the parameters are not set as shown below, the error "Servo parameter invalid" (error code: 1DC8H) occurs and the values will be rewritten from the controller.

| No. | Name | Default value | Setting value |
|---|---|---|---|
| PA06 | Electronic gear numerator*1 | 1 | • When using the rotary servo motor HK-KT series: 16<br>• Other (when not using the rotary servo motor HK-KT series): 1 |
| PA07 | Electronic gear denominator*1 | 1 | 1 |
| PD41.3 | Sensor input method selection*1 | 0h | 1h (Input from controller (FLS/RLS/DOG)) |
| PD60 | DI pin polarity selection*1 | 00000000h | 00000000h |
| PT01.1 | Speed/acceleration/deceleration unit selection*2 | 0h | 0h |
| PT15 | Software position limit + | 0 | 0 |
| PT17 | Software position limit - | 0 | 0 |
| PT29.0 | Device input polarity 1*1 | 0h | 1h: Dog detection with on |

*1 The parameter is enabled after resetting the Motion module or MR-JET-G.
*2 The parameter is enabled after resetting MR-JET-G.

#### PDO mapping when using MR-JET-G (MR-JET-Gを使用する場合のPDOマッピング) (App.3 / original p.864)

When MR-JET-G is the motion control station, the Motion module assigns the PDO mapping automatically so that the setting is not needed.
Details of the mapping is as same as MR-J5(W)-G (Cyclic synchronous mode).

#### Precautions (注意事項) (App.3 / original p.864)

- The following Motion module-related functions of MR-JET-G are not supported by MR-JET-G. For details, refer to the servo amplifier manuals.
  - Scale measurement function
- When parameter automatic setting is enabled in the network configuration settings on GX Works3, servo parameters are not automatically refreshed to the CPU module after the error "Servo parameter invalid" (error code: 1DC8H) occurs. Start MR Configuration2 via GX Works3, then read the servo parameters.
- Motion control is not performed if the IP address of the Motion control station set in Network Configuration Settings is not also set in "[Pr.141] IP address". In this situation, correct the parameter setting.
- A servo alarm [AL.035 Command frequency error] may be detected in MR-JET-G when an operation cycle over occurs on the Motion module during a motor operation and the command differs greatly before the operation cycle over and after a restoration. Check the program and increase the operation cycle setting or decrease the loading if necessary.

*The sub-item "Scale measurement function" is in a framed box in the original. "MR Configuration2" is as printed.

## Appendix 4 Restrictions by the version (バージョンによる機能の制約) (App.4 / original p.865-866)

The software versions compatible with each Simple Motion module/Motion module are shown below.

| Model | Version: GX Works3 |
|---|---|
| FX5-SSC-S | 1.007H or later |
| FX5-SSC-G | 1.072A or later |

*In the original, the header is 2-tier ("Version" over "GX Works3"). Flattened into one row.

There are restrictions in the function that can be used by the software of the Simple Motion module/Motion module and the version of the engineering tool. The combination of each version and function is shown below.

**[FX5-SSC-S]** (App.4 / original p.865)

| Function | Software version | GX Works3 | Reference |
|---|---|---|---|
| Command generation axis | 1.002 or later | 1.015R or later | *1 |
| Advanced synchronous control<br>Slippage smoothing method (Linear: Input value follow up) | 1.003 or later | 1.025B or later | *2 |
| Monitor of rotation direction using synchronous control monitor | 1.003 or later | 1.025B or later | *3 |
| Optional data monitor function data type<br>Internal temperature of encoder, Unit power consumption (Used point: 2 words) | 1.003 or later | 1.025B or later | →Page 371 Optional Data Monitor Function |
| [Pr.127] Speed limit value input selection at control mode switching | 1.003 or later | 1.025B or later | →Page 470 Detailed parameters2 |
| AlphaStep/5-phase stepping motor driver manufactured by ORIENTAL MOTOR Co., Ltd. | 1.003 or later | 1.025B or later | →Page 829 AlphaStep/5-phase stepping motor driver manufactured by ORIENTAL MOTOR Co., Ltd. |
| 8 axes | 1.004 or later | 1.030G or later | — |
| 0.888 ms of operation cycle | 1.004 or later | 1.030G or later | — |
| Linear servo motor control mode/Direct drive motor control mode/Fully closed loop control mode | 1.004 or later | 1.030G or later | — |
| Inverter (FR-A800 series) | 1.004 or later | 1.030G or later | →Page 824 Inverter FR-A800 series |
| Servo driver manufactured by CKD NIKKI DENSO CO., LTD. (VCⅡ series/VPH series) | 1.004 or later | 1.030G or later | →Page 836 Servo driver VCII series/VPH series manufactured by CKD NIKKI DENSO CO., LTD. |
| IAI electric actuator controller manufactured by IAI Corporation | 1.004 or later | 1.030G or later | →Page 840 IAI electric actuator controller manufactured by IAI Corporation |
| Firmware update function | 1.011 or later*4 | 1.120A or later | Page 384 Firmware update function |
| MR-J5(W)-B | 1.011 or later | 1.123D or later | Page 845 Connection with MR-J5(W)-B |

*In the original, the "Software version" / "GX Works3" cells are merged: 1.003 or later / 1.025B or later over the 5 rows from "Advanced synchronous control" to "AlphaStep/5-phase...", and 1.004 or later / 1.030G or later over the 6 rows from "8 axes" to "IAI electric actuator controller...". Expanded to each row. "—" is printed as "—" in the original. The last two Reference cells (Page 384 / Page 845) have no "☞" mark in the original.

*1 Refer to "Command Generation Axis" in the following manual for details.
[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Advanced Synchronous Control)
*2 Refer to "Clutch" in the following manual for details.
[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Advanced Synchronous Control)
*3 Refer to "Outline of Synchronous Control" in the following manual for details.
[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Advanced Synchronous Control)
*4 For Simple Motion module compatible with the software version 1.004 to 1.009, updating the software version to 1.011 or later is possible.

**[FX5-SSC-G]** (App.4 / original p.866)

| Function | Software version | GX Works3 | Reference |
|---|---|---|---|
| MR-J5D-G. | 1.001 or later | 1.075D or later | — |
| Safety extension module | 1.001 or later | 1.075D or later | — |
| Mark detection (servo amplifier TPR1 input). | 1.001 or later | 1.080J or later | →Page 355 Mark Detection Function |
| Automatic update of saved parameter | 1.001 or later | 1.080J or later | *1 |
| Dedicated instruction, SLMPSND. | 1.001 or later | 1.080J or later | *2 |
| Override 0%. | 1.002 or later | 1.075D or later | →Page 262 Override function |
| Communication speed 100 Mbps. | 1.002 or later | 1.085P or later | *3 |
| Time managed polling method (CC-Link IE TSN Protocol version 2.0) | 1.002 or later | 1.085P or later | *3 |
| Manual pulse generator speed limit value. | 1.002 or later | 1.085P or later | →Page 178 Manual pulse generator speed limit mode [FX5-SSC-G] |
| Cam axis length per cycle change. | 1.002 or later | 1.085P or later | *4 |
| Electronic gear setting range extended | 1.002 or later | 1.085P or later | →Page 455 [Pr.2] to [Pr.4] Electronic gear (Movement amount per pulse) |
| Speed/torque control mutual switching during servo OFF | 1.003 or later | 1.085P or later | →Page 215 Control mode switching during servo OFF |
| Synchronous encoder via servo amplifier<br>• linear encoder (incremental type)<br>• ABZ-phase differential output type encoder | 1.003 or later | 1.085P or later | *4 |
| Synchronous encoder axis via link device | 1.004 or later | 1.105K or later | Page 329 Link Device External Signal Assignment Function [FX5-SSC-G] |
| Mark detection (link device input) | 1.004 or later | 1.105K or later | Page 329 Page 329 Link Device External Signal Assignment Function [FX5-SSC-G]<br>Page 355 Mark Detection Function |
| Link device external signal | 1.005 or later | 1.110Q or later | Page 329 Link Device External Signal Assignment Function [FX5-SSC-G] |
| Drive units other than MELSERVO (Cyclic synchronous mode) connection method | 1.007 or later | 1.080J or later | Page 858 Drive units other than MELSERVO (Cyclic synchronous mode) connection method |

*In the original, merged cells are expanded to each row: "Software version" 1.001 or later over the 5 rows "MR-J5D-G." to "Dedicated instruction, SLMPSND.", 1.002 or later over the 6 rows "Override 0%." to "Electronic gear setting range extended", 1.003 or later over 2 rows, 1.004 or later over 2 rows. "GX Works3" 1.075D or later over the 2 rows "MR-J5D-G." / "Safety extension module", 1.080J or later over the 3 rows "Mark detection (servo amplifier TPR1 input)." to "Dedicated instruction, SLMPSND.", 1.085P or later over the 7 rows "Communication speed 100 Mbps." to "Synchronous encoder via servo amplifier", 1.105K or later over 2 rows. "—" is printed as "—" in the original. The last four Reference cells (Page 329 / Page 858) have no "☞" mark in the original.
*As printed in the original: trailing periods in some Function names ("MR-J5D-G.", "Override 0%.", "Communication speed 100 Mbps." and others), and the duplicated "Page 329 Page 329" in the "Mark detection (link device input)" row.

*1 Refer to "Others" in the following manual for details.
[Other manual] MELSEC iQ-F FX5 Motion Module User's Manual (CC-Link IE TSN)
*2 Refer to "DEDICATED INSTRUCTION" in the following manual for details.
[Other manual] MELSEC iQ-F FX5 Motion Module User's Manual (CC-Link IE TSN)
*3 Refer to "SYSTEM CONFIGURATION" in the following manual for details.
[Other manual] MELSEC iQ-F FX5 Motion Module User's Manual (CC-Link IE TSN)
*4 Refer to "Synchronous Encoder Axis" in the following manual for details.
[Other manual] MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Advanced Synchronous Control)
