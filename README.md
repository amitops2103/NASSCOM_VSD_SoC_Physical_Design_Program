# NASSCOM_VSD_SoC_Physical_Design_Program
Digital VLSI Soc-Physical Design (Picorv32)
---
## DAY-1: Inception of open-sourcs EDA,OpenLANE and sky130 PDK

### OpenLANE software




![image](https://th.bing.com/th/id/OIP.zR75AX_qbCv2sEh_76qTDAHaDW?rs=1&pid=ImgDetMain)

OpenLane is a complete toolchain used for physical design in digital VLSI circuits. It is part of the broader open-source hardware initiative and is specifically designed to handle the RTL-to-GDSII flow, automating the steps between Register-Transfer Level (RTL) design and the final layout for chip manufacturing (GDSII). OpenLane is built on top of various other open-source tools to facilitate this process.
### Key Features:
#### 1. RTL to GDSII Automation: OpenLane automates the process of taking RTL designs (usually written in VHDL/Verilog) through the physical design flow, up to generating GDSII files that can be sent to a fabrication foundry.
#### 2.Open-Source Tool Integration: OpenLane integrates multiple open-source tools, such as:
- **Yosys**: For synthesis, translating RTL to a gate-level netlist.
- **OpenROAD**: For place-and-route, performing physical layout steps.
- **Magic**: For layout viewing and DRC (Design Rule Checking).
- **Netgen**:  For LVS (Layout vs. Schematic) checking.
- **KLayout**: For GDSII manipulation and visualization.
#### 3. Flow Steps:
- **Synthesis**: Translates RTL into a gate-level netlist.
- **Floorplanning**: Determines how the major blocks will be arranged on the chip.
- **Placement**: Places standard cells on the floorplan.
- **Routing**: Routes the wires that connect the standard cells.
- **Timing Analysis**: Ensures that the design meets timing requirements.
- **Power and Ground Network (P/G)**: Establishes a network for power delivery and grounding.
- **Design Rule Checking (DRC)**: Ensures the design conforms to the fabrication process rules.
- **Layout vs. Schematic (LVS) Verification**: Confirms that the layout matches the circuit's schematic.
#### 4. Customizable Flow: Users can configure the tool to match different process technology nodes and design constraints.
#### 5. Technology Compatibility: It supports different PDKs (Process Design Kits), including the open-source SkyWater 130nm process.

### RISC-V (picorv32a)




![PADS](https://github.com/user-attachments/assets/6b7b21ed-ae98-4c01-8559-12a9d8e2917f)

The PicoRV32 is a compact and efficient open-source implementation of a 32-bit RISC-V CPU, designed primarily for use in FPGAs (Field Programmable Gate Arrays) and other resource-constrained environments. It is fully compliant with the RISC-V RV32IMC instruction set architecture, which supports 32-bit instructions, integer arithmetic, multiplication/division, and compressed instructions (reduced-length instructions for improved code density).

The core is highly optimized for small area usage and low resource consumption, making it suitable for tasks where minimal power and resources are available.


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
---
Day 1 Lab : Design setup
---
     cd Desktop/work/tool/openlane_working_dir/openlane
     docker
     ./flow.tcl -interactive
     

 ![package](https://github.com/amitops2103/NASSCOM_VSD_SoC_Physical_Design_Program/blob/WORKSHOP/DAY-1/1.jpg)

     prep -design picorv32a
![prep](https://github.com/amitops2103/NASSCOM_VSD_SoC_Physical_Design_Program/blob/WORKSHOP/DAY-1/2.jpg)

     run_synthesis 

     
 ## Results
 ![package](https://github.com/amitops2103/NASSCOM_VSD_SoC_Physical_Design_Program/blob/WORKSHOP/DAY-1/3.jpg)
 ![package](https://github.com/amitops2103/NASSCOM_VSD_SoC_Physical_Design_Program/blob/WORKSHOP/DAY-1/4.jpg)

 
     Flop Ratio 
 ![flop_ratio](https://github.com/amitops2103/NASSCOM_VSD_SoC_Physical_Design_Program/blob/WORKSHOP/DAY-1/5.jpg)
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## DAY-2: Floorplaning and Placement
-------

     cd Desktop/work/tool/openlane_working_dir/openlane/designs/picorv32a
     less config.tcl

 ![package](https://github.com/amitops2103/NASSCOM_VSD_SoC_Physical_Design_Program/blob/WORKSHOP/DAY-2/1.jpg)
 
### Floorplan
---
FP_IO_VMETAL

FP_IO_HMETAL
     
     run_floorplan
     cd Desktop/work/tool/openlane_working_dir/openlane/configuration

 ![package](https://github.com/amitops2103/NASSCOM_VSD_SoC_Physical_Design_Program/blob/WORKSHOP/DAY-2/2.jpg)

     cd Desktop/work/tool/openlane_working_dir/openlane/designs/picorv32a/08-09_14-03/results/floorplan
     magic -T /home/vsduser/Desktop/work/tool/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &

![package](https://github.com/amitops2103/NASSCOM_VSD_SoC_Physical_Design_Program/blob/WORKSHOP/DAY-2/3.jpg)

#### Metal 3 cell

![package](https://github.com/amitops2103/NASSCOM_VSD_SoC_Physical_Design_Program/blob/WORKSHOP/DAY-2/4.jpg)

![5](https://github.com/user-attachments/assets/e4a257c8-417f-4ce2-a290-2d6c80f428be)

#### Metal 2 cell

![6](https://github.com/user-attachments/assets/83ce0a91-05d5-4ef6-9251-34ddf31ede8e)

#### Buffer cell

![7](https://github.com/user-attachments/assets/be237344-783e-4361-9de5-585d2dba2ea2)

#### Nand cell

![8](https://github.com/user-attachments/assets/160a6dc8-94ec-4d7b-9089-f7a748c2342a)

#### Decoupling capacitor cell

![9](https://github.com/user-attachments/assets/a2a0c1de-2131-4896-ba88-6f7f0880c7a9)

#### tapvpwrvgnd cell

![10](https://github.com/user-attachments/assets/59c77607-8642-4b41-97ca-15ba69c5eb1d)

### Placement
----
     run_placement
     
![11](https://github.com/user-attachments/assets/51fb28b6-e45d-44e9-a96a-b28121b7a9b8)

    magic -T /home/vsduser/Desktop/work/tool/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &

![12](https://github.com/user-attachments/assets/23808baf-79c9-4e62-ac63-85ada34e4a64)

![13](https://github.com/user-attachments/assets/5fa6a635-0a2e-4ea4-916a-8d3608cc6ff9)
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
