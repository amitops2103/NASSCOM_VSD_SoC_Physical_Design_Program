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

# _ASIC Design Flow Overview_

![image](https://github.com/user-attachments/assets/abe34205-3877-47b0-832d-12a1ab76d5fb)

1. _Register Transfer Level (RTL)_
   
  a. Starting Point:
        The design is described using a high-level hardware description language like Verilog or VHDL.
   
  b. Function:
        The RTL describes how data flows between registers and how the logic components operate within the design.


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
2. _Synthesis (Synth)_

    ![image](https://github.com/user-attachments/assets/d99c5088-c1b4-478f-964f-d72baad3b15e)

Input: RTL description.
Output: Gate-level netlist.
Process:
The synthesis tool converts the RTL design into a gate-level netlist, consisting of logic gates and flip-flops.
The netlist is technology-mapped to the specific standard cells from the technology library (provided by the PDK, or Process Design Kit).

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

3. _Floor Planning + Power Planning (FP + PP)_

   ![image](https://github.com/user-attachments/assets/ae647052-a92e-41ae-907c-df12c1688e96)
  
Input: Gate-level netlist.
Process:
This stage defines the physical layout of the design on the chip, positioning key blocks, I/O pins, and the power distribution network.
Power planning ensures that every part of the design receives sufficient power for proper operation.

 ![image](https://github.com/user-attachments/assets/fcbcf920-80af-4975-a903-67e50599234c)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

4. _Placement (Place)_

![image](https://github.com/user-attachments/assets/1a18556f-1644-417b-8dc7-5ccf8199f9a7)

Input: Gate-level netlist and floorplan.
Process:
Placement tools arrange the logic gates and flip-flops into specific physical locations on the chip.

The goal is to minimize chip area, reduce wire lengths, and meet timing constraints.

Placement is performed in two stages: Global Placement (where cells may overlap) and Detailed Placement (where cells are optimally placed following placement rules).

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

5. _Clock Tree Synthesis (CTS)_

   ![image](https://github.com/user-attachments/assets/17cce477-4879-4390-b546-4894ce7cee53)

Process:
A clock tree is synthesized to distribute the clock signal uniformly across the chip.
This ensures that all flip-flops receive the clock signal simultaneously, avoiding clock skew issues and ensuring timing synchronization.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

6. _Routing (Route)_
   
   ![image](https://github.com/user-attachments/assets/d226d089-6630-4d92-a832-dd21ea67158c)

Process:
Routing tools connect the placed gates using metal wires based on the netlist.
This step must follow design rules, optimize performance, and address signal integrity concerns like crosstalk and electromagnetic interference.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

7. _Sign-off_
   
Process:
Sign-off is the final verification stage before the design goes to manufacturing. This includes:
a. Timing closure: Ensuring the design meets timing constraints.

b. Power analysis: Verifying that the power distribution is sufficient.

c. Signal integrity checks: Checking for issues like crosstalk and electromigration.

Only once the design passes all these checks can it proceed to fabrication.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

8. _GDSII (Graphic Data System II)_
Output:
The final step produces the GDSII file, which contains the full physical layout of the chip.
This file is sent to the semiconductor foundry for fabrication.
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
---
Day 1 Labs : Design setup
---
     cd Desktop/work/tool/openlane_directory/openlane
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
