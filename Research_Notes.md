# Notes
https://www.youtube.com/watch?v=W13HNsoHj7A USB-C Power Delivery Hardware Design - Phil's Lab #104
https://www.ti.com/lit/wp/slyy109b/slyy109b.pdf?ts=1704425741746 A Primer on USB Type-C and USBPower Delivery Applications and Requirements
https://github.com/DynamixYANG/highendusb3hub

# Parts check: 
https://www.pcbway.com/components/
https://jlcpcb.com/parts/

## Find Symbols + Footprints
https://componentsearchengine.com/


# STM32F042G6U6 https://jlcpcb.com/partdetail/Stmicroelectronics-STM32F042G6U6/C961597
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

# USB C Female Receptacle  
Vertical 24P 5A: https://jlcpcb.com/partdetail/gswitch-GT_USB7052/C963223  (footprint in kicad is almost same as USB_C_Receptacle_GCT_USB4115-03-C)
Normal Surface Mount: https://jlcpcb.com/partdetail/Molex-1054500101/C134092


# USB C controllers
## PD controller
Note: DRP - Dual-role power can operate as sink or source
TPS65987D - 20V 5A (the classic recommendation) (available @ $5.36 @ pcbway, none on jlcpcb)
TPS25730
#### ---> CYPD3177-24LQXQ (super common) (available on both pcbway $3 & jlcpcb $1.25)
https://au.mouser.com/datasheet/2/196/CYPR_S_A0012903526_1-3004964.pdf
https://www.infineon.com/dgdl/Infineon-CY4533_EZ-PD_Barrel_Connector_Replacement_EVK_Guide-UserManual-v01_00-EN.pdf?fileId=8ac78c8c7d0d8da4017d0f013aac1887
Needs MOSFET:
DMP3013SFV-7 ? used in https://github.com/wolfgangfriedrich/P42-USB-C-PD-Sink/blob/master/Design/ver4/USBC-Sink_ver4.sch (looks better)
SI3421DV ? used in https://github.com/ElectronicCats/Cat-Sink/blob/main/Hw/CatSink/CatSink.kicad_sch

Calculate power dissipation: http://www.mcmanis.com/chuck/Robotics/projects/esc2/FET-power.html
(We are 20V ~2.5A worse case ~60deg => Rds(on) = 0.09), P = I^2 R = 0.5625W dissipation. rating is 0.94W.???
## USB 3 controllers
### UFP - Upstream facing port (on a USB hub, the one that connects to the computer)
TUSB1064 - Upstream facing port (UFP) USB Type-C DP alt mode 10Gbps linear redriver crosspoint switch for 10Gbps speeeeds with active mux https://www.ti.com/product/TUSB1064
### DFP
TUSB546 - 5Gbps active mux (Available on pcbway)
### DFP/UFP (aka DRD Dual-role data)
---> TUSB542 - 5Gbps active mux <-- this one looks popular> (7 pcs @ $11 @ JLCPCB, not available @ pcbway)
## USB 2 Controller
TUSB212?
##
## Redriver?
Goes in between USB controller and the connector, to fix interference and quality issues
When the redriver integrates with the mux -> it is called redriver mux / active mux
e.g. TUSB522P very available $0.60

### Recommendations by https://www.youtube.com/watch?v=_4h2ZD8O9Ms
1. TUSB422 + TPS65987D + TUSB542 + TUSB212 (5Gbps)
2. TUSB422 + TPS65987D + TUSB1042I + TUSB212 (10Gbps)

# Hub controller
VL822 = QFN88 variant features integrated 10Gbps Muxes for the Upstream Facing Port and two Downstream Facings Ports whereas the smaller QFN76/QFN56 variant does not. The integrated 10Gbps Muxes are ideal for Data-Only USB-C applications that would otherwise require an external Mux, with the advantage of potential board area savings and improved signal integrity. If additional USB-C Ports are need, separate CC Logic and Mux solutions.
(not very available)

---> GL3523-OTY30 -  very available! (5Gbps) ($2, 2k stock on jlcpcb)

TUSB8044A (5Gbps) - Documentation is clearly the best https://www.ti.com/lit/ds/symlink/tusb8044a.pdf?ts=1704464901395&ref_url=https%253A%252F%252Fwww.ti.com%252Finterface%252Fusb%252Fhubs-controllers%252Fproducts.html (jlcpcb no stock $11, pcbway available $12)