# Notes
https://www.youtube.com/watch?v=W13HNsoHj7A USB-C Power Delivery Hardware Design - Phil's Lab #104
https://www.ti.com/lit/wp/slyy109b/slyy109b.pdf?ts=1704425741746 A Primer on USB Type-C and USBPower Delivery Applications and Requirements
https://github.com/DynamixYANG/highendusb3hub

# Parts check: 
https://www.pcbway.com/components/
https://jlcpcb.com/parts/

## Find Symbols + Footprints
https://componentsearchengine.com/
https://easyeda.com/

# STM32
STM32F103C8T6 https://jlcpcb.com/partdetail/Stmicroelectronics-STM32F103C8T6/C8734

QFN package - more complicated :0?
3.3V <- Needs a regulator from USB, ~100mA?
USB natively on board!
CAN timers 

# DC converter
harder to route than an LDO regulator

How to choose switching regulator:
SMD type 
Skip BGA (expensive to assemble)

Pick simple `Buck` in Topology..
Pick correct output voltage & output current

Go for higher switching frequencies -> >1MHz?


# USB

## USB Type-C Female Receptacle  

| Part Name | Description | JLCPCB | Notes |
| -  | - | - | - |
| GT-USB-7052 | USB3.1 24P 5A Type C Receptacle Vertical | [JLCPCB](https://jlcpcb.com/partdetail/gswitch-GT_USB7052/C963223) | |
| Molex 1054500101 | USB3.2 24P 5A Type C Surface Mount | [JLCPCB](https://jlcpcb.com/partdetail/Molex-1054500101/C134092) | |

## Type-C PD controller
| Part Name | Description | JLCPCB | Datasheet | Notes |
| -  | - | - | - | - |
| CYPD3177-24LQXQ | USB Type-C and PD controller. Max 20V/5A | [JLCPCB](https://jlcpcb.com/partdetail/CypressSemicon-CYPD317724LQXQ/C2959321) | [Datasheet](https://www.infineon.com/dgdl/Infineon-EZ-PD_BCR_Datasheet_USB_Type-C_Port_Controller_for_Power_Sinks-DataSheet-v03_00-EN.pdf?fileId=8ac78c8c7d0d8da4017d0ee7ce9d70ad) | Lots in stock! [Evaluation Kit Datasheet](https://www.infineon.com/dgdl/Infineon-CY4533_EZ-PD_Barrel_Connector_Replacement_EVK_Guide-UserManual-v01_00-EN.pdf?fileId=8ac78c8c7d0d8da4017d0f013aac1887)|
| TUSB422 | DRP USB Type-C Port Control with Power Delivery (needs programming) | | [Datasheet](https://www.ti.com/lit/ds/symlink/tusb422.pdf) | |
| TPS65987D | USB Type-C and PD controller. Max 20V/5A | [JLCPCB](https://jlcpcb.com/partdetail/TexasInstruments-TPS65987DDHRSHR/C2868843) | [Datasheet](https://www.ti.com/lit/ds/symlink/tps65987d.pdf) | The most common TI recommendation. No stock on JLCPCB. |

## USB 3 controllers
### UFP - Upstream facing port (on a USB hub, the one that connects to the computer)
| Part Name | Description | JLCPCB | Datasheet | Notes |
| -  | - | - | - | - |
| TUSB1064 | USB Type-C 10Gbps (active mux) with Alt Mode support | [JLCPCB](https://jlcpcb.com/parts/componentSearch?searchTxt=TUSB1064) | [Datasheet](https://www.ti.com/product/TUSB1064) | No stock! Too new and fancy? |
| TUSB546A-DCI | USB Type-C 5Gbps + DP multi-protocol linear redriver (active mux) | | [Datasheet](https://www.ti.com/lit/ds/symlink/tusb546a-dci.pdf) | 
| TUSB564 | USB Type-C DP Alt Mode 5Gbps (active mux) | | [Datasheet](https://www.ti.com/lit/ds/symlink/tusb564.pdf) | |


### DFP

### DFP/UFP (aka DRD Dual-role data)
| Part Name | Description | JLCPCB | Datasheet | Notes |
| -  | - | - | - | - | 
| TUSB542 | 5-Gbps USB 3.1 Gen1 Type-C 2:1 mux and redriver (active mux) | [JLCPCB]() | [Datasheet](https://www.ti.com/lit/ds/symlink/tusb542.pdf) | no stock.. |
| HD3SS460 | 4x6-channel Type-C Alt Mode (passive mux) |  | [Datasheet](https://www.ti.com/lit/ds/symlink/hd3ss460.pdf) | |
| HD3SS3212 | 2-channel 10-Gbps 2:1/1:2 USB 3.1 differential (passive mux) | | [Datasheet](https://www.ti.com/lit/ds/symlink/hd3ss3212.pdf) | |
| PI3USB302-AZBEX |  2-differential channel bi-directional multiplexer/demultiplexer (passive mux) | [JLCPCB](https://jlcpcb.com/partdetail/DiodesIncorporated-PI3USB302AZBEX/C500787) | [Datasheet](https://www.diodes.com/assets/Datasheets/PI3USB302-A.pdf) | very available! |

## USB 2 Signal conditioner
| Part Name | Description | JLCPCB | Notes |
| -  | - | - | - |
| TUSB212IRWBR | USB2.0 Signal conditioner | [JLCPCB](https://jlcpcb.com/partdetail/TexasInstruments-TUSB212IRWBR/C2674396) | Note: TUSB211 is has less redriving capability |

## Redriver
| Part Name | Description | JLCPCB | Datasheet | Notes |
| -  | - | - | - | - | 
| TUSB544 | Type-C 5Gbps Redriver DRP? | | [Datasheet](https://www.ti.com/product/TUSB544) |  |
| TUSB522P | 5Gbps USB3.0 redriver | [JLCPCB](https://jlcpcb.com/parts/componentSearch?searchTxt=TUSB522P) | [Datasheet](https://www.ti.com/lit/ds/symlink/tusb522p.pdf) | very available! |
| TUSB1044 | 10Gbps multi-protocol bi-directional linear redriver | | [Datasheet](https://www.ti.com/lit/ds/symlink/tusb1044.pdf) | |


### Recommendations by https://www.youtube.com/watch?v=_4h2ZD8O9Ms
1. TUSB422 + TPS65987D + TUSB542 + TUSB212 (5Gbps)
2. TUSB422 + TPS65987D + TUSB1042I + TUSB212 (10Gbps)

TPS65987D -> Power delivery
TUSB212 -> USB 2 controller


## Hub controller
VL822 = QFN88 variant features integrated 10Gbps Muxes for the Upstream Facing Port and two Downstream Facings Ports whereas the smaller QFN76/QFN56 variant does not. The integrated 10Gbps Muxes are ideal for Data-Only USB-C applications that would otherwise require an external Mux, with the advantage of potential board area savings and improved signal integrity. If additional USB-C Ports are need, separate CC Logic and Mux solutions.
(not very available)

---> GL3523-OTY30 -  very available! (5Gbps) ($2, 2k stock on jlcpcb)

CYUSB3304-68LTXC (2 pieces in stock on jlcpcb, $4.60)
https://jlcpcb.com/partdetail/CypressSemicon-CYUSB330468LTXC/C462531 

VL817 - USB3.1 Gen 1 (5Gbps) TT, integrated 5V regulator (to 3.3 and 1.1) from 5V USB VBus (0 stock on jlcpcb)
VL818 - USB3.2 (5Gbps), supports USB power saving features
VL819 - USB PD hub, 3.2 Gen1x1 with USB PD support

TUSB8041 - https://www.ti.com/product/TUSB8041 (Available on jlcpcb)
TUSB8042A
TUSB8043A
TUSB8044A (5Gbps) - Documentation is clearly the best https://www.ti.com/lit/ds/symlink/tusb8044a.pdf?ts=1704464901395&ref_url=https%253A%252F%252Fwww.ti.com%252Finterface%252Fusb%252Fhubs-controllers%252Fproducts.html (jlcpcb no stock $11, pcbway available $12)

CYUSB3304
https://jlcpcb.com/partdetail/CypressSemicon-CYUSB330468LTXCT/C914921

## USB->Ethernet IC
RTL8153 (lots in stock)

## ESD Protection
| Part Name | Description | JLCPCB | Datasheet | Notes |
| -  | - | - | - | - | 
| TI ESD122D | ESD Protection Bidirectional TVS | [JLCPCB](https://jlcpcb.com/partdetail/TexasInstruments-ESD122DMXR/C544474)  | [Datasheet](https://www.ti.com/lit/ds/symlink/esd122.pdf) | useful datasheet for protecting USB type C! |
| TI TPDxE05U06 | ESD Protection Unidirectional TVS | [JLCPCB](https://jlcpcb.com/partdetail/TexasInstruments-TPD4E05U06DQAR/C138714) ($0.09, 17k stock) | [Datasheet](https://www.ti.com/lit/ds/symlink/tpd4e05u06.pdf) | TI recommends this for protecting SBU/CC/DP/DM |
| ESD3V3U4ULC-MS | ESD Protection | [JLCPCB](https://jlcpcb.com/partdetail/Msksemi-ESD3V3U4ULCMS/C2830125) ($0.09, 5.6k stock) | [Datasheet](https://file.elecfans.com/web2/M00/4A/30/pYYBAGKhxzqAM2bjAAZ0FOOCNZU239.pdf) | nice pass-through design, used in https://github.com/DynamixYANG/highendusb3hub/tree/master |
| Nexperia PUSB3AB4 | ESD Protection for USB3.2 10Gbps | [JLCPCB](https://jlcpcb.com/partdetail/Nexperia-PUSB3AB4Z/C553549) ($0.22, 2k stock) | [Datasheet](https://assets.nexperia.com/documents/data-sheet/PUSB3AB4.pdf) |  | 
| Nexperia IP4283CZ10 | ESD Protection for ultra high-speed devices | [JLCPCB](https://jlcpcb.com/partdetail/Nexperia-IP4283CZ10_TBR115/C551514) ($0.20, 5k stock) | [Datasheet](https://assets.nexperia.com/documents/data-sheet/IP4283CZ10_SER.pdf) |  |


## USB Power switch
TPS2001C https://www.ti.com/product/TPS2001C for the output USBs