# EasyExcel2USB Evaluation Tool
## Scope
**EasyExcel2USB** provides a portable way to evaluate a new chip without any coding. This project aims to automatically scan the datasheet of the chip and convert it into a **GUI based evaluation software** for register-level debugging. 
## Basic Functions
* Readback register values from target devices
* Show values in an Excel workbook
* Edit values in an Excel workbook
* Write the registers on target devices
* Export operation history and generate C code for offline configuration
## Principle of operation
In current version, we rely on a free online PDF-To-Excel tool (small pdf) to create an editable Excel form from a datasheet. Considering the relative high error rate of the conversion result, we prefer to develop a dedicated scan and OCR tool for register map identification in the feature.
## Roadmap
### Current Version
* Use online PDF2Excel tool and provide full capacity of register control in Excel using micros coded by VBA.
* Support SPI and AXI devices (SPI supported via USB using FT2232H as a physical bridge, AXI supported on Xilinx FPGA via Ethernet with a TCP server running on Microblaze embedded processor)
### Next Version
* Support for exporting operation history and generate C code for offline configuration
* Support for generation of chip-by-chip programming framework (in C code)
## Hardware
* Curently we use a homemade DAC FMC Card with FT2232H on board as the target device.
* The AXI target device is a JESD204B Core running on a KC705 development kit.
## Build Instructions
1. Get the sources from Github:
``` shell
git clone --recursive https://github.com/ddomax/EasyEval.git
```
2. Build Qt project in ./qt_app using Qt Creator. Note that only Qt 5.12.10+VS2019 is tested.
3. Build Xilinx SDK projects in ./sdk
4. Build Vivado project in ./hdl/
5. When KC705 is booting, monitor the Serial COMx while baudrate is set to 9600. And the output will be:
```
SPI ELF Bootloader
SPI Mode: 
00000002 
Copying ELF image from SPI flash @ 0x00c00000 to RAM
..........................................................................................................................................................................................................................................................
Transferring execution to program @ 0x00000000


From newtork thread:

-----lwIP Socket Mode Echo server Demo Application ------
From newtork thread: adding network interface...
Start PHY autonegotiation 
Waiting for PHY to complete autonegotiation.
autonegotiation complete 
auto-negotiated link speed: 1000
From newtork thread: netif_set_default...
From newtork thread: netif_set_up...
From newtork thread: Running xemacif_input_thread...
From newtork thread: Strating DHCP...
From newtork thread: Running DHCP Loop...
DHCP request success
Board IP: 192.168.0.104
Netmask : 255.255.255.0
Gateway : 192.168.0.1
         echo server      7 $ telnet <board_ip> 7

```
6. Run qt_app and connect to the target device.
7. Start clipboard monitor in qt_app.
8. Enjoy examples in ./examples
