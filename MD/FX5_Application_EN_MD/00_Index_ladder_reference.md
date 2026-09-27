# FX5 Motion Module/Simple Motion Module User's Manual (Application) — Index (索引) (original p.1-876)

| Item | Content |
|---|---|
| Original file | FX5 Motion Module_Simple Motion Module User's Manual (Application).pdf |
| Manual number | IB(NA)-0300253ENG-P (February 2026). Japanese manual number: IB-0300252-M |
| Publisher | Mitsubishi Electric Corporation |
| Target models | FX5-40SSC-S, FX5-80SSC-S (generic: FX5-SSC-S), FX5-40SSC-G, FX5-80SSC-G (generic: FX5-SSC-G) |
| Total pages | 876 |
| Conversion method | pypdfium2 text + visual check of PyMuPDF page renders (tables, figures, ladder) |
| Page notation | "original p.N" is the **PDF page number**. Printed page number = PDF page − 2. Cross-references in the text keep the printed page |
| Split policy | 1 chapter = 1 file (`NN_<Chapter>_ladder_reference.md`). This file = index, relevant manuals, terms, generic terms/abbreviations |
| Language | Body = official English text verbatim. Headings carry the Japanese term in parentheses for search. The Japanese edition is converted separately in `FX5_応用編_MD/` |

> This set of files is a reference of the original PDF. In addition to tables, addresses and bit definitions,
> function descriptions, device ON/OFF timing, precautions and program examples are transcribed **verbatim in full**.
> See the conversion range table below. **"Not in the md" does not mean "not in the manual".**
> When making design decisions based on module behavior, do the final check on the corresponding page of the original.

## Conversion range (変換範囲表 / original p.1-876)

Pages are PDF page numbers (bookmark start pages).

| Original page | Section | File | Handling |
|---|---|---|---|
| p.1-19 | SAFETY PRECAUTIONS, CONDITIONS OF USE, INTRODUCTION, CONTENTS | — | **Not converted** |
| p.20-23 | RELEVANT MANUALS, TERMS, GENERIC TERMS AND ABBREVIATIONS | this file | Full text |
| p.24-37 | 1 START AND STOP (始動と停止) (1.1-1.3) | `01_Start_and_Stop_ladder_reference.md` | Full text |
| p.38-59 | 2 HOME POSITION RETURN CONTROL (原点復帰制御) (2.1-2.4) | `02_Home_Position_Return_Control_ladder_reference.md` | Full text |
| p.60-138 | 3 MAJOR POSITIONING CONTROL (主要な位置決め制御) (3.1-3.2) | `03_Major_Positioning_Control_ladder_reference.md` | Full text |
| p.139-158 | 4 HIGH-LEVEL POSITIONING CONTROL (高度な位置決め制御) (4.1-4.5) | `04_High-level_Positioning_Control_ladder_reference.md` | Full text |
| p.159-187 | 5 MANUAL CONTROL (手動制御) (5.1-5.4) | `05_Manual_Control_ladder_reference.md` | Full text |
| p.188-219 | 6 EXPANSION CONTROL (拡張制御) (6.1-6.2) | `06_Expansion_Control_ladder_reference.md` | Full text |
| p.220-317 | 7 CONTROL SUB FUNCTIONS (制御の補助機能) (7.1-7.10) | `07_Control_Sub_Functions_ladder_reference.md` | Full text |
| p.318-388 | 8 COMMON FUNCTIONS (共通機能) (8.1-8.16) | `08_Common_Functions_ladder_reference.md` | Full text |
| p.389-390 | 9 SPECIFICATIONS OF I/O SIGNALS WITH CPU MODULES (CPUユニットとの入出力信号仕様) (9.1) | `09_IO_Signals_with_CPU_Modules_ladder_reference.md` | Full text |
| p.391-399 | 10 PARAMETER SETTINGS (パラメータ設定) (10.1-10.3) | `10_Parameter_Settings_ladder_reference.md` | Full text |
| p.400-623 | 11 DATA USED FOR POSITIONING CONTROL (位置決め制御に使用するデータ) (11.1-11.9) | `11_Data_Used_for_Positioning_Control_ladder_reference.md` | Full text |
| p.624-675 | 12 PROGRAMMING [FX5-SSC-S] (プログラミング[FX5-SSC-S]) (12.1-12.4) | `12_Programming_FX5-SSC-S_ladder_reference.md` | Full text |
| p.676-720 | 13 PROGRAMMING [FX5-SSC-G] (プログラミング[FX5-SSC-G]) (13.1-13.3) | `13_Programming_FX5-SSC-G_ladder_reference.md` | Full text |
| p.721-820 | 14 TROUBLESHOOTING (トラブルシューティング) (14.1-14.5) | `14_Troubleshooting_ladder_reference.md` | Full text |
| p.821-866 | APPENDICES (付録) (App.1-App.4) | `15_Appendices_ladder_reference.md` | Full text |
| p.867-876 | INDEX, REVISIONS, WARRANTY, INFORMATION AND SERVICES, TRADEMARKS | — | **Not converted** |

## List of chapters and sections (章・節の一覧) (original p.24-866, bookmarks)

| Chapter | Section | Original page |
|---|---|---|
| 1 START AND STOP | 1.1 Start | p.24 |
| 1 START AND STOP | 1.2 Stop | p.32 |
| 1 START AND STOP | 1.3 Restart | p.36 |
| 2 HOME POSITION RETURN CONTROL | 2.1 Outline of Home Position Return Control | p.38 |
| 2 HOME POSITION RETURN CONTROL | 2.2 Machine Home Position Return | p.41 |
| 2 HOME POSITION RETURN CONTROL | 2.3 Fast Home Position Return | p.57 |
| 2 HOME POSITION RETURN CONTROL | 2.4 Selection of the Home Position Return Setting Condition | p.59 |
| 3 MAJOR POSITIONING CONTROL | 3.1 Outline of Major Positioning Controls | p.60 |
| 3 MAJOR POSITIONING CONTROL | 3.2 Setting the Positioning Data | p.79 |
| 4 HIGH-LEVEL POSITIONING CONTROL | 4.1 Outline of High-level Positioning Control | p.139 |
| 4 HIGH-LEVEL POSITIONING CONTROL | 4.2 High-level Positioning Control Execution Procedure | p.142 |
| 4 HIGH-LEVEL POSITIONING CONTROL | 4.3 Setting the Block Start Data | p.143 |
| 4 HIGH-LEVEL POSITIONING CONTROL | 4.4 Setting the Condition Data | p.152 |
| 4 HIGH-LEVEL POSITIONING CONTROL | 4.5 Start Program for High-level Positioning Control | p.155 |
| 5 MANUAL CONTROL | 5.1 Outline of Manual Control | p.159 |
| 5 MANUAL CONTROL | 5.2 JOG Operation | p.161 |
| 5 MANUAL CONTROL | 5.3 Inching Operation | p.170 |
| 5 MANUAL CONTROL | 5.4 Manual Pulse Generator Operation | p.178 |
| 6 EXPANSION CONTROL | 6.1 Speed-torque Control | p.188 |
| 6 EXPANSION CONTROL | 6.2 Advanced Synchronous Control | p.219 |
| 7 CONTROL SUB FUNCTIONS | 7.1 Outline of Sub Functions | p.220 |
| 7 CONTROL SUB FUNCTIONS | 7.2 Sub Functions Specifically for Machine Home Position Return | p.222 |
| 7 CONTROL SUB FUNCTIONS | 7.3 Functions for Compensating the Control | p.229 |
| 7 CONTROL SUB FUNCTIONS | 7.4 Functions to Limit the Control | p.241 |
| 7 CONTROL SUB FUNCTIONS | 7.5 Functions to Change the Control Details | p.259 |
| 7 CONTROL SUB FUNCTIONS | 7.6 Functions Related to Start | p.278 |
| 7 CONTROL SUB FUNCTIONS | 7.7 Absolute Position System | p.280 |
| 7 CONTROL SUB FUNCTIONS | 7.8 Functions Related to Stop | p.283 |
| 7 CONTROL SUB FUNCTIONS | 7.9 Other Functions | p.292 |
| 7 CONTROL SUB FUNCTIONS | 7.10 Servo ON/OFF | p.315 |
| 8 COMMON FUNCTIONS | 8.1 Outline of Common Functions | p.318 |
| 8 COMMON FUNCTIONS | 8.2 Parameter Initialization Function | p.319 |
| 8 COMMON FUNCTIONS | 8.3 Execution Data Backup Function | p.321 |
| 8 COMMON FUNCTIONS | 8.4 External Input Signal Select Function | p.323 |
| 8 COMMON FUNCTIONS | 8.5 Link Device External Signal Assignment Function [FX5-SSC-G] | p.331 |
| 8 COMMON FUNCTIONS | 8.6 History Monitor Function | p.338 |
| 8 COMMON FUNCTIONS | 8.7 Amplifier-less Operation Function [FX5-SSC-S] | p.342 |
| 8 COMMON FUNCTIONS | 8.8 Virtual Servo Amplifier Function | p.346 |
| 8 COMMON FUNCTIONS | 8.9 Driver Communication Function [FX5-SSC-S] | p.352 |
| 8 COMMON FUNCTIONS | 8.10 Mark Detection Function | p.357 |
| 8 COMMON FUNCTIONS | 8.11 Optional Data Monitor Function | p.373 |
| 8 COMMON FUNCTIONS | 8.12 Event History Function [FX5-SSC-G] | p.378 |
| 8 COMMON FUNCTIONS | 8.13 Connect/Disconnect Function of SSCNET Communication [FX5-SSC-S] | p.379 |
| 8 COMMON FUNCTIONS | 8.14 Servo Transient Transmission Function [FX5-SSC-G] | p.383 |
| 8 COMMON FUNCTIONS | 8.15 Firmware update function | p.386 |
| 8 COMMON FUNCTIONS | 8.16 Hot line forced stop function | p.387 |
| 9 SPECIFICATIONS OF I/O SIGNALS WITH CPU MODULES | 9.1 List of Input/Output Signals with CPU Modules | p.389 |
| 10 PARAMETER SETTINGS | 10.1 Parameter Setting Procedure | p.391 |
| 10 PARAMETER SETTINGS | 10.2 Module Parameters | p.392 |
| 10 PARAMETER SETTINGS | 10.3 Simple Motion Module Setting | p.399 |
| 11 DATA USED FOR POSITIONING CONTROL | 11.1 Types of Data | p.400 |
| 11 DATA USED FOR POSITIONING CONTROL | 11.2 List of Buffer Memory Addresses | p.424 |
| 11 DATA USED FOR POSITIONING CONTROL | 11.3 Basic Setting | p.446 |
| 11 DATA USED FOR POSITIONING CONTROL | 11.4 Positioning Data | p.499 |
| 11 DATA USED FOR POSITIONING CONTROL | 11.5 Block Start Data | p.511 |
| 11 DATA USED FOR POSITIONING CONTROL | 11.6 Condition Data | p.514 |
| 11 DATA USED FOR POSITIONING CONTROL | 11.7 Monitor Data | p.520 |
| 11 DATA USED FOR POSITIONING CONTROL | 11.8 Control Data | p.563 |
| 11 DATA USED FOR POSITIONING CONTROL | 11.9 Memory Configuration and Data Process | p.603 |
| 12 PROGRAMMING [FX5-SSC-S] | 12.1 Precautions for Creating Program | p.624 |
| 12 PROGRAMMING [FX5-SSC-S] | 12.2 Creating a Program | p.625 |
| 12 PROGRAMMING [FX5-SSC-S] | 12.3 Positioning Program Examples (For Using Labels) | p.626 |
| 12 PROGRAMMING [FX5-SSC-S] | 12.4 Positioning Program Examples (For Using Buffer Memory) | p.642 |
| 13 PROGRAMMING [FX5-SSC-G] | 13.1 Precautions for Creating Program | p.676 |
| 13 PROGRAMMING [FX5-SSC-G] | 13.2 Creating a Program | p.677 |
| 13 PROGRAMMING [FX5-SSC-G] | 13.3 Positioning Program Examples (For Using Labels) | p.678 |
| 14 TROUBLESHOOTING | 14.1 Troubleshooting Procedure | p.721 |
| 14 TROUBLESHOOTING | 14.2 Troubleshooting by Symptom | p.726 |
| 14 TROUBLESHOOTING | 14.3 Error and Warning Details | p.728 |
| 14 TROUBLESHOOTING | 14.4 List of Warning Codes | p.733 |
| 14 TROUBLESHOOTING | 14.5 List of Error Codes | p.755 |
| APPENDICES | Appendix 1 How to Find Buffer Memory Addresses | p.821 |
| APPENDICES | Appendix 2 Compatible Devices with SSCNETIII(/H) [FX5-SSC-S] | p.825 |
| APPENDICES | Appendix 3 Devices Compatible with CC-Link IE TSN [FX5-SSC-G] | p.852 |
| APPENDICES | Appendix 4 Restrictions by the version | p.865 |

## RELEVANT MANUALS (関連マニュアル) (original p.20)

The following manuals are relevant to this product.
This manual does not include detailed information on the following:
- General specifications
- Available CPU modules and the number of mountable modules
- Installation

For details, refer to the following.
[Other manual] MELSEC iQ-F FX5S/FX5UJ/FX5U/FX5UC User's Manual (Hardware)

| Manual name [manual number] | Description |
|---|---|
| MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Application) [IB-0300253ENG] (This manual) | Functions, input/output signals, buffer memories, parameter settings, programming, and troubleshooting of the Motion module/Simple Motion module |
| MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Startup) [IB-0300251ENG] | Specifications, procedures before operation, system configuration, wiring, and operation examples of the Motion module/Simple Motion module |
| MELSEC iQ-F FX5 Motion Module/Simple Motion Module User's Manual (Advanced Synchronous Control) [IB-0300255ENG] | Functions and programming for the synchronous control of the Motion module/Simple Motion module |
| MELSEC iQ-F FX5 Motion Module User's Manual (CC-Link IE TSN) [IB-0300568ENG] | Functions, parameter settings, troubleshooting, and buffer memories of the CC-Link IE TSN network |
| MELSEC iQ-F FX5 Motion Module/Simple Motion Module Function Block Reference [BCN-B62005-719] | Specifications, functions, and input/output labels of function blocks for the Motion module/Simple Motion module |

## TERMS (用語) (original p.21-22)

Unless otherwise specified, this manual uses the following terms.

| Term | Description |
|---|---|
| 4-axis module | Another term for FX5-40SSC-S and FX5-40SSC-G. |
| 8-axis module | Another term for FX5-80SSC-S and FX5-80SSC-G. |
| Axis | A target for motion control. |
| Buffer memory | A memory in an intelligent function module, where data (such as setting values and monitoring values) are stored. |
| CANopen | An open network whose standards are promoted by the non-profit organization CiA. An application layer is defined in which communication profiles and device profiles are defined, and this application layer is applied to the CC-Link IE TSN CAN application protocol. |
| CC-Link | One of the field-based networks that can handle control and information at the same time. |
| CC-Link IE Controller Network | One of the control system networks. A backbone network that supports large-scale distributed controller control and bundles field and motion networks. |
| CC-Link IE Field Basic Network | A network that achieves cyclic transmission by software. Applicable to small-scale equipment that does not require high-speed control. |
| CC-Link IE Field Network | A high speed and large capacity open field network that is based on Ethernet (1000BASE-T). |
| CC-Link IE TSN | An open network that uses “TSN (Time-Sensitive Networking)”, which is an extension of the Ethernet standard, to ensure real-time control and handle information from other open networks simultaneously. |
| CC-Link IE TSN Class | A group of devices and industrial switches with CC-Link IE TSN, classified according to the functions and performance by the CC-Link Partner Association. For CC-Link IE TSN Class, refer to the CC-Link IE TSN Installation Manual (BAP-C3007ENG-001) published by the CC-Link Partner Association. |
| CC-Link IE TSN Protocol version 2.0 | In addition to the time sharing method using IEEE802.1AS for time synchronization, this protocol communicates using the time managed polling method. |
| Command generation axis | An axis that performs only command generation. "Command generation axis" is not included in the number of controlled axes of the controller. |
| Communication cycle | Cyclic transmission communication cycle of the cyclic master. |
| Cyclic transmission | A function by which data is periodically exchanged among stations on the network. |
| Dedicated instruction | An instruction for using functions of the module. |
| Device | Various types of memory in a module. Some devices are handled in units of bits and some in units of words. |
| Disconnection | A process of stopping data link if a data link error occurs. |
| Extension module | CC-Link IE Remote module without TSN network communication function. In the case of a multi-axis servo amplifier, axes other than axis A are extension modules. |
| Feedback speed | Feedback values from a device station in a real axis converted to the axis unit system. |
| Field network | Network used to efficiently control various sensors and drive systems with less wiring in the factory automation field. |
| Gateway | In general, protocol conversion is required to connect networks that differ from each other due to differences in signaling methods and functions. This function bridges these different networks to enable mutual communication. |
| Global label | A label that is enabled for all program data when creating multiple program data in the project. There are two types of global label: a module specific label (module label), which is generated automatically by GX Works3, and an optional label, which can be created for any specified device. |
| Grandmaster | A source device or station to synchronize clocks in the time synchronization via PTP (Precision Time Protocol). |
| GX Works3 | The product name of the software package for the MELSEC programmable controllers. |
| IEEE802.1AS | A protocol for high precision time/timing synchronization. |
| Intelligent device station | A station that exchanges I/O signals (bit data) and I/O data (word data) with another station by cyclic transmission on CC-Link IE Field Network. This station can perform transient transmission. This station responds to a transient transmission request from another station and also issues a transient transmission request to another station. |
| Intelligent function module | A module that has functions other than input and output, such as an A/D converter module and D/A converter module. |
| Label | A variable used in a program. |
| Link dedicated instruction | Dedicated instruction for the programmable controller to send messages to the specified station using transient transmission. |
| Link device | A device in a module on CC-Link IE TSN. |
| Link down | Status in which the communication cable is disconnected or not connected, and communication with the destination device is disabled. |
| Link up | Status in which the cable is connected to the communication port and communication with the destination device is enabled. |
| Local station | A station that performs cyclic transmission and transient transmission with the master station and other local stations. |
| Master station | A station that controls a network. Only one station exists per network. The transmission range of each station for cyclic transmission is assigned to the master station. |
| Module label | A label that represents one of memory areas (I/O signals and buffer memory areas) specific to each module in a given character string. From the module used, GX Works3 automatically generates this label, which can be used as a global label in the CPU module. |
| Motion control station | A device station that exchanges cyclic data by motion control. |
| Motion network | A network for high performance/functional drive control. (SSCNET, etc.) |
| MR Configurator2 | The product name of the setup software for the servo amplifier. |
| MR-J3(W)-B | Servo amplifier model MR-J3-_B_(-RJ)/MR-J3W-_B. |
| MR-J4(W)-B | Servo amplifier model MR-J4-_B_(-RJ)/MR-J4W_-_B. |
| MR-J4-B | Servo amplifier model MR-J4-_B_. |
| MR-J5(W)-B | Servo amplifier model MR-J5-_B_(-RJ)/MR-J5W_-_B. |
| MR-J5-B | Servo amplifier model MR-J5-_B_. |
| MR-J5-G | Servo amplifier model MR-J5-_G_(-RJ). |
| MR-J5D-G | Servo amplifier model MR-J5D_-_G_. |
| MR-J5W-G | Servo amplifier model MR-J5W-G. |
| MR-J5(W)-G | Servo amplifier model MR-J5-_G_(-RJ)/MR-J5W_-_G/MR-J5D_-_G_. |
| MR-JE-B(F) | Servo amplifier model MR-JE-_B(F). |
| MR-JET-G | Servo amplifier model MR-JET-_G. |
| Node | Nodal point at the time of the data link. |
| Object | Various data held by the CANopen-compatible device station. |
| Object dictionary | In CANopen, various data such as control parameters/command values held by devices are handled as objects consisting of an Index, Sub Index, object name, data type, etc. These sets are called object dictionaries. |
| PDO mapping | Write operation to the PDO mapping object (RPDO/TPDO) at the device station, which determines the number of PDO allocated to the device and the assignment of objects in the PDO. |
| Profile | A file that specifies the specific information of a device (model name, model name, etc.) and the information required for installation, operation, and maintenance. |
| Relay station | A station that relays data link to other station. Link device data of a network module are transferred to another network module via this station. Multiple network modules are connected to one programmable controller. |
| Remote device station | A station that exchanges I/O signals (bit data) and I/O data (word data) with another station by cyclic transmission on CC-Link IE Field Network. This station responds to a transient transmission request from another station. |
| Remote I/O station | A station that exchanges I/O signals (bit data) with the master station by cyclic transmission on CC-Link IE Field Network. |
| Remote station | A station that performs bit basis and word basis cyclic and transient transmissions with the master station on CC-Link IE TSN network. |
| Return | A process of restarting data link when a station recovers from an error. |
| Safety main module | Different name for FX5-SF-MU4T5. |
| Servo amplifier axis | A servo amplifier or virtual servo amplifier controlled by a controller. "Servo amplifier axis" is included in the number of controlled axes of the controller. |
| SSCNET/H*1 | High speed synchronous communication network between Simple Motion module and servo amplifier. |
| SSCNET*1 |  |
| Station | Each of the nodes connected to the network is called a station. |
| Station No. | Each station is numbered and this number is called the station No. |
| Time sharing | A method in which a communication line is divided into fixed time intervals and different data is sent and received at each interval. |
| Time synchronization | The clocks of each station are synchronized to the clock of the grand master (the clock source station). |
| Transient transmission | A function of non-periodic data communication among nodes (station) on network. A function used to send messages to the target station when requested by a link dedicated instruction or the engineering tool. Communication is available with station on another network via relay station, or gateway. |

*In the original, the "Description" cell of SSCNETⅢ/H*1 and SSCNETⅢ*1 is merged over the 2 rows. Expanded to each row. The table continues from p.21 to p.22.

*1 SSCNET: Servo System Controller NETwork

## GENERIC TERMS AND ABBREVIATIONS (総称／略称) (original p.23)

Unless otherwise specified, this manual uses the following generic terms and abbreviations.

| Generic term/abbreviation | Description |
|---|---|
| CC-Link IE | A generic term for CC-Link IE Field Network, CC-Link IE Controller Network, CC-Link IE Field Basic Network, and CC-Link IE TSN network. |
| CPU module | An abbreviation for the MELSEC iQ-F series CPU module. |
| Data link | A generic term for a cyclic transmission and a transient transmission. |
| Devices compatible with CC-Link IE TSN | A generic term for devices certified as CC-Link IE TSN Class A or CC-Link IE TSN Class B by CC-Link Partner Association. |
| Device station | A generic term for a local station and remote station on CC-Link IE TSN. |
| Drive unit | A generic term for motor drive devices such as a servo amplifier. |
| Engineering tool | A generic term for GX Works3 and MR Configurator2. |
| FB | An abbreviation for function blocks. A graphical programming language for programmable controllers that is one of the five languages defined in the IEC 61131-3 standard. |
| FX5-SSC-G | A generic term for the FX5-40SSC-G and FX5-80SSC-G Motion module. |
| FX5-SSC-S | A generic term for the FX5-40SSC-S and FX5-80SSC-S Simple Motion module. |
| GOT | An abbreviation for Graphic Operation Terminal. A display device for industrial (FA) equipment. |
| Intelligent module | The abbreviation for the intelligent function module. |
| I/O module | A generic term for the I/O modules (extension cable type) and I/O modules (extension connector type). |
| Manual pulse generator | An abbreviation for a (user-arranged) manual pulse generator. |
| Motion module | An abbreviation for the MELSEC iQ-F series Motion module. |
| Motion system | A generic term for software that performs the motion control and the network control. |
| Network module | A generic term for the following modules:<br>• Ethernet interface module<br>• Module on CC-Link IE TSN (the Motion module and a module on a remote station)<br>• CC-Link IE Controller Network module<br>• Module on CC-Link IE Field Network (a master/local module, and a module on a remote I/O station, a remote device station, and an intelligent device station)<br>• MELSECNET/H network module<br>• MELSECNET/10 network module |
| PDO | An abbreviation for Process Data Object. A collection of the application objects transmitted periodically between multiple CANopen nodes. |
| PTP | An abbreviation for Precision Time Protocol. A predefined protocol for time synchronization between devices on a network. |
| RWr | An abbreviation for a remote register of the link device. This refers to 16-bit (1-word) data input from a device station to the master station. (Not applicable for some local stations.) |
| RWw | An abbreviation for a remote register of the link device. This refers to 16-bit (1-word) data output from the master station to a device station. (Not applicable for some local stations.) |
| RX | An abbreviation for remote input of the link device. This refers to bit data input from a device station to the master station. (Not applicable for some local stations.) |
| RY | An abbreviation for remote output of the link device. This refers to bit data output from the master station to a device station. (Not applicable for some local stations.) |
| Safety expansion module | A generic term for expansion modules installed to a safety main module. |
| Safety extension module | A generic term for safety main modules and safety expansion modules. |
| SDO | An abbreviation for Service Data Object. A message used to access the object entries inside the object dictionary of an optional CANopen node. Used for non-periodic transmission between stations. |
| Servo network | A generic term for the network between the Simple Motion module/Motion module and drive units. • SSCNET/H, SSCNET• CC-Link IE TSN |
| Simple Motion module | An abbreviation for the MELSEC iQ-F series Simple Motion module. |
| SLMP | An abbreviation for Seamless Message Protocol. This protocol enables seamless communication between Ethernet and CC-Link or CC-Link IE networks. |
| SLMPSND | A generic term for the J.SLMPSND, JP.SLMPSND, G.SLMPSND, and GP.SLMPSND. |
| SSCNET(/H) | A generic term for SSCNET/H, SSCNET. |
