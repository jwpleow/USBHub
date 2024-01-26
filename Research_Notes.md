# Notes
https://www.youtube.com/watch?v=W13HNsoHj7A USB-C Power Delivery Hardware Design - Phil's Lab #104
https://www.ti.com/lit/wp/slyy109b/slyy109b.pdf?ts=1704425741746 A Primer on USB Type-C and USBPower Delivery Applications and Requirements

# USB 3 hub examples
https://github.com/DynamixYANG/highendusb3hub
https://www.ti.com/lit/ug/slla312c/slla312c.pdf

# USB PD examples
https://www.ti.com/lit/ug/slvubo9a/slvubo9a.pdf

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



### Recommendations by https://www.youtube.com/watch?v=_4h2ZD8O9Ms
1. TUSB422 + TPS65987D + TUSB542 + TUSB212 (5Gbps)
2. TUSB422 + TPS65987D + TUSB1042I + TUSB212 (10Gbps)

TPS65987D -> Power delivery
TUSB212 -> USB 2 controller

