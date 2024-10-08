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
     
![1](https://github.com/user-attachments/assets/dea31a87-bc5e-4cb4-8d9d-74b6395c2a3c)

     prep -design picorv32a
![2](https://github.com/user-attachments/assets/c4fd5377-2af0-477d-834d-1ad1eb027fbc)

     run_synthesis 

     
 ## Results
![3](https://github.com/user-attachments/assets/3578e957-7ae4-4a15-aa70-3855cbaf7d59)
![4](https://github.com/user-attachments/assets/4cb3e2e6-8723-4cd2-99ff-4148d30bbb9c)

 
     Flop Ratio 
![5](https://github.com/user-attachments/assets/482fdd3f-3e34-4ce7-a378-b3e0061a6ba7)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## DAY-2 lab: Floorplaning and Placement
-------

     cd Desktop/work/tool/openlane_working_dir/openlane/designs/picorv32a
     less config.tcl

![1](https://github.com/user-attachments/assets/fefaa220-a714-44c2-aa1e-4b753a0cc6f9)

### Floorplan
---
FP_IO_VMETAL

FP_IO_HMETAL
     
     run_floorplan
     cd Desktop/work/tool/openlane_working_dir/openlane/configuration

![2](https://github.com/user-attachments/assets/c7d2e600-48de-4a26-9aac-879904c138a8)


     cd Desktop/work/tool/openlane_working_dir/openlane/designs/picorv32a/08-09_14-03/results/floorplan
     magic -T /home/vsduser/Desktop/work/tool/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &

![3](https://github.com/user-attachments/assets/57f078b4-d4b4-4288-a9bf-b7914f7ac262)

#### Metal 3 cell

![4](https://github.com/user-attachments/assets/d7972f4e-acf4-4282-8ae1-5e3a98a6549e)

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
## DAY-3 lab: Designing Library cell and ngSPICE characterization
------
Cloning custom inverter standard cell design from github repository

     git clone https://github.com/nickson-jose/vsdstdcelldesign.git

![1](https://github.com/user-attachments/assets/f69fde04-12a3-4e64-89a2-11a18a8aacf9)

Copying magic tech file to vsdstdcelldesign
         
     cp sky130A.tech /home/vsduser/Desktop/work/tool/openlane_working_dir/openplane/vsdstdcelldesign

![2](https://github.com/user-attachments/assets/5d3fb2c9-0070-4b68-af51-38366e0fcb84)

![3](https://github.com/user-attachments/assets/0f15a8bb-8e4d-43d0-8628-06f7287009a3)

#### custom CMOS inverter in magic tool

![4](https://github.com/user-attachments/assets/a57020e7-006f-48d2-b32b-723ff7e3ed83)

#### N-MOS in custom CMOS inverter in magic tool
   
![5](https://github.com/user-attachments/assets/a417eb67-3906-453b-b3d4-b6c8620416f8)

#### P-MOS in custom CMOS inverter in magic tool

![6](https://github.com/user-attachments/assets/08567d86-2d2c-401f-91d2-c8d7aff5b146)

#### "A" is attached to locali in cell def sky130_inv

![7](https://github.com/user-attachments/assets/8bcb678f-1bd9-43e9-b2cd-dd827ad71731)

#### "Y" is attached to locali in cell def sky130_inv

![8](https://github.com/user-attachments/assets/edb50725-9717-4597-904e-ad9a89259c1e)

#### Poly-silicon in custom CMOS inverter in magic tool

![9](https://github.com/user-attachments/assets/cd68c041-5be0-400d-99b9-f2f6d6fc2779)

#### Extracting CMOS inverter to SPICE characterization

     pwd
     extract all
     ext2spice cthresh 0 rthresh 0
     ext2spice

![10](https://github.com/user-attachments/assets/eb926b01-58dd-4b2f-b79d-607edc053fae)

![11](https://github.com/user-attachments/assets/a3c3ccfb-6cdc-46b2-b740-f4a029890486)

#### Opening SPICE extracted file

     vim sky130_inv.spice

![12](https://github.com/user-attachments/assets/73fbe2fd-0b86-4895-82b2-d943b22a4560)
Running and ploting the SPICE file

     ngspice sky130_inv.spice
     plot y vs time a

![13](https://github.com/user-attachments/assets/dc06ac51-dbb0-4038-827c-a0cbc252540d)

### Rise time calculation

     Rise Time = T(80%)−T(20%)

80% of 3.3V = 2.64
![14](https://github.com/user-attachments/assets/6e2b813d-f696-4d6a-a3b0-2790739ec83f)

20% of 3.3V = 0.660
![15](https://github.com/user-attachments/assets/9c909dbe-1281-43b6-bd02-da5b7cce9382)

     Rise Time = 0.05933ns

![16](https://github.com/user-attachments/assets/67595219-9a9a-4332-b095-e2fa5bcc9959)

### Fall time calculation

     Fall Time = T(80%)−T(20%)

80% of 3.3V = 2.64
![17](https://github.com/user-attachments/assets/11493042-6172-420d-ba42-43fd84ebba2a)

20% of 3.3V = 0.660
![18](https://github.com/user-attachments/assets/57f6ea36-6e06-4543-a1ca-fb08abe41ec1)

      Fall Time = 0.02999ns

![19](https://github.com/user-attachments/assets/7a3ae80e-c760-4498-89c1-84db49b6f60c)

### Rise propagation delay calculation

     Rise Delay= Tout(50%)​ − Tin(50%)​

50% of 3.3V = 1.65
![20](https://github.com/user-attachments/assets/2d53baad-6cc2-4319-bb0a-4f15f00050e7)

     Rise propagation delay = 0.05639ns

![21](https://github.com/user-attachments/assets/e6244a87-a026-4ba5-a9f3-1f8af3459f07)

### Fall propagation delay calculation

     Fall Delay= Tout(50%)​ − Tin(50%)​

50% of 3.3V = 1.65
![22](https://github.com/user-attachments/assets/bacaf0e5-4387-4ad1-a4ba-f1dde6a1af3f)

     Fall propagation delay = 0.0248ns

![23](https://github.com/user-attachments/assets/768545b5-d173-4d85-ba5c-d498691875b4)
---------------------------------------------------------------------------------------
## Introduction to magic tool options and steps to load sky130 DRC rules
---------------------------------------------------------------------------------------

#### Lab introduction to Magic and steps to load Sky130 tech-rules

     wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
     tar xfz drc_tests.tgz
     cd drc_tests

![24](https://github.com/user-attachments/assets/497d1793-2041-433a-933e-ca7ff802c6b0)
To view .magicrc file

     gvim .magicrc

![25](https://github.com/user-attachments/assets/974b6083-bbb5-4b6e-84cb-f29f090acca8)

Open magic tool
     
     magic -d XR &

![26](https://github.com/user-attachments/assets/94d01f56-7c60-4de8-b06b-2f04ec4dd36c)

### DRC check exercise

     load poly

![27](https://github.com/user-attachments/assets/61b8b14d-6210-441a-93ac-fcdaef594da5)

### poly.9
DRC rule for poly.9 in skywater130A pdk

![28](https://github.com/user-attachments/assets/d1bdf337-8665-4e4c-a692-ce9172cf6963)

npolyres
![29](https://github.com/user-attachments/assets/da0f3792-7185-4647-8be7-e3c97f917222)

poly
![30](https://github.com/user-attachments/assets/07182c0f-4ff3-4ab7-8cd4-d6275c1d8f70)

xpolyres
![31](https://github.com/user-attachments/assets/e33153b3-dd3f-4ddc-ac62-6611a4ee1011)

ppolyres
![32](https://github.com/user-attachments/assets/652b0c95-7f42-4153-9d77-dc85d6e7a18c)

    drc check
    drc why
    
![33](https://github.com/user-attachments/assets/773e3b79-db83-4081-95bc-1aec441ae871)
![34](https://github.com/user-attachments/assets/c08c3100-e679-436a-9d95-4e0f8ceb4b80)
![35](https://github.com/user-attachments/assets/7276ec91-8b8b-4aef-badd-6bc48d7a776e)

    vi sky130A.tech
    
![36](https://github.com/user-attachments/assets/c55234d1-f1a4-4810-a702-f93852eb635e)

    /drc
    
![37](https://github.com/user-attachments/assets/f535d2ee-9659-4632-a5aa-33563fb79296)

    /poly.9

Error-1
![38](https://github.com/user-attachments/assets/76446670-1388-4302-aaf4-383263a80504)

Error-2
![39](https://github.com/user-attachments/assets/8a9d3674-b05c-4a6d-adde-4a05af890b29)

Error-2 (fixed)
![40](https://github.com/user-attachments/assets/3c1eb5b2-112d-4584-b44c-5db01817bba6)

Error-1 (fixed)
![41](https://github.com/user-attachments/assets/d8b8dda7-1d66-4541-be2e-bf8116eb5e9a)

     tech load sky130A.tech
     drc check
     drc why
     
![42](https://github.com/user-attachments/assets/50c1e720-0d08-492e-865c-aaa30f391e58)

### Poly.2
![43](https://github.com/user-attachments/assets/4cad66ad-9491-4a62-94c8-5b65a1cca33f)

DRC rule for poly.2 in skywater130A pdk

![44](https://github.com/user-attachments/assets/c29e3980-ddbc-4589-a17f-c40f36701d11)

Error
![45](https://github.com/user-attachments/assets/1ec22149-4972-499d-a3dc-b4b85675128b)

Error (fixed)
![46](https://github.com/user-attachments/assets/af8aefde-ed78-461d-993f-ec3850033e89)

![47](https://github.com/user-attachments/assets/40d99f1c-2297-4b67-a14b-84436785df24)

### nwell.4

![51](https://github.com/user-attachments/assets/ec8c5c63-0e6b-4741-91eb-817208b290b3)

![48](https://github.com/user-attachments/assets/8f587f46-bf1f-4ae0-abc3-4c641f92b587)

![49](https://github.com/user-attachments/assets/d157e05a-6931-4b96-9c36-7d9f8754d5e5)

![50](https://github.com/user-attachments/assets/77be4548-4a8e-489b-b5d2-2baa81ef0150)

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## DAY-4 lab:  Pre-layout timing analysis and importance of good clock tree
------
#### Open CMOS -inverter layout using magic tool
![1](https://github.com/user-attachments/assets/58e2c7b0-e281-409f-afab-359cac66b929)

     press g on the layout for the grid formate

![3](https://github.com/user-attachments/assets/47cbb07b-2797-4d5c-a2a3-c7e7e126c27d)

#### Generation of LEF file from layout

     Requirment_1.The input and output ports of the standard cell should lie on the intersection of the vertical and horizontal tracks.

![2](https://github.com/user-attachments/assets/54855ed5-a7da-4e28-8ee4-100c9415ed9f)

     % grid 0.46um 0.34um 0.23um 0.17um

![4](https://github.com/user-attachments/assets/39b31db8-1246-4970-9bb3-56846c2a131f)
![5](https://github.com/user-attachments/assets/92cf19a5-9573-4d2a-8999-5bc290f5eb09)

     Requirement_2: Width of the standard cell must be odd multiple of the Xpitch.

![6](https://github.com/user-attachments/assets/c1dc034b-1292-42dd-8ffb-b2fa9a1e09f3)

     Requriement_3: Hight of the standard cell must be even multiple of the Ypitch

![7](https://github.com/user-attachments/assets/f756f815-1e44-461f-bb05-8b59d486e19f)

#### Create port definition

![8](https://github.com/user-attachments/assets/fdb239f1-2925-44a1-a741-4e34eba6f956)
![9](https://github.com/user-attachments/assets/737d3d20-c0a7-416a-a90f-5e15ba0c018a)
![10](https://github.com/user-attachments/assets/332554c3-46b6-464d-9371-2025fd63a811)

#### Set port class and port use

![11](https://github.com/user-attachments/assets/f95edc79-9559-404e-9964-4e7e9b6c1883)

#### Creating LEF file with same custom file name

     % write lef

![12](https://github.com/user-attachments/assets/6facf49a-d20d-4a0c-a461-d6a48e6140a7)
![13](https://github.com/user-attachments/assets/c207d702-ec31-49d3-8a23-67bcfed333fa)
![14](https://github.com/user-attachments/assets/ea5c43fa-e9b9-411d-b184-e10c41313a60)

copying sky130_vsdinv.lef from (openlane/vsdstdcelldesign) to (picorv32a/src)

     cp sky130_vsdinv.lef /home/Desktop/work/tool/openlane_working_dir/openlane/designs/picorv32a/src

![15](https://github.com/user-attachments/assets/67ad7654-4b40-4b9f-9982-c901b826c874)
![16](https://github.com/user-attachments/assets/dbf2cec3-22c9-419e-84c7-2386a52935f3)

copying sky130_fd_sc_hd_*.lib file from (openlane/vsdstdcelldesign/libs) to (picorv32a/src)

    cp sky130_fd_sc_hd_* /home/Desktop/work/tool/openlane_working_dir/openlane/designs/picorv32a/src

![17](https://github.com/user-attachments/assets/879abefb-0541-4191-8fe9-f448cedb2cb2)
![18](https://github.com/user-attachments/assets/dfb7ad82-0119-4078-b744-73a39aabce0b)

#### Editing (config.tcl)

    set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
    set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
    set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
    set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

    set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]

![19](https://github.com/user-attachments/assets/408b27bd-26c4-437b-bd9d-4fcf081ab9a5)

### Plugging custom LEF to openlane flow

     docker
     ./flow.tcl -interactive
     package require openlane 0.9
     prep -design picorv32a -tag 08-09_14-03 -overwrite
     run_synthsis
    
![20](https://github.com/user-attachments/assets/b7815f57-bca7-4607-8f3d-f5c70a2be063)

     total negative slack (tns) = -711.59
     wrost negative slack (wns0 = -23.89

![21](https://github.com/user-attachments/assets/7fec6dee-3346-4ab8-9a1e-f24663cfdee5)

For reducing slack
     
     set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
     add_lefs -src $lefs
     echo $::env(SYNTH_STRATEGY)
     set ::env(SYNTH_STRATEGY) "DELAY 1"
     echo $::env(SYNTH_BUFFERING)
     echo $::env(SYNTH_SIZING)
     set ::env(SYNTH_SIZING) 1
     echo $::env(SYNTH_DRIVING_CELL)

![22](https://github.com/user-attachments/assets/ac1cef8f-c4a5-4cf9-86c7-a0b80b8fc308)
![23](https://github.com/user-attachments/assets/db970470-0add-43c1-9fec-e2777fad2a62)

     total negative slack (tns) = 0.00
     wrost negative slack (wns0 = 0.00

----------

     run_floorplan
     run_placement

![24](https://github.com/user-attachments/assets/df106764-9690-4a6b-9b71-ef0ac7dfed0f)

      magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &

![25](https://github.com/user-attachments/assets/845bb609-a40a-4eb5-92e7-2d8e870e4766)
#### Expanding sky130_vsdinv custom block
      
       % expand

![26](https://github.com/user-attachments/assets/f444155c-3006-4a0e-b97c-7bca5a66decc)
![27](https://github.com/user-attachments/assets/93d2c183-680c-44b5-90f1-340233e1a440)


##### Create (pre_sta.conf) for STA analysis in openlane directory

![28](https://github.com/user-attachments/assets/5c5aef70-8ab9-44c4-b189-31c6d75e1883)



#### Create (my_base.sdc) for STA analysis in openlane/designs/picorv32a/src

![29](https://github.com/user-attachments/assets/316797ab-9287-491c-a57c-c1f69323ac14)

#### Output of pre_sta.conf is equal to synthesis stage

        sta pre_sta.conf

#### The slack is (7.14) 
The slack should be greater than or equal to 0

       SLACK = (DATA REQUIRED TIME) - (DATA ARIVAL TIME)
![30](https://github.com/user-attachments/assets/84e1c217-7752-45be-b224-af465924f2c1)

#### Replace the old netlist with the newly generated netlist 

     write_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/08-09_14-03/results/synthesis/picorv32a.synthesis.v
![31](https://github.com/user-attachments/assets/ccc98e23-bd63-4ae8-8921-456eff788682)
![32](https://github.com/user-attachments/assets/394fc978-3462-4059-8ee4-beca2bce0fe6)

     run_floorplan
     run_placement
![33](https://github.com/user-attachments/assets/94e3b5ca-4b1d-4da1-ad9a-ce4bf7d5e19a)

    run_cts
![34](https://github.com/user-attachments/assets/768b32ec-4df4-492c-8fbd-eabb4076e22c)
#### Generated cts file

    /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/08-09_14-03/results/synthesis
     
![35](https://github.com/user-attachments/assets/c945f018-930e-401a-9262-f543bc0b001f)

#### Post-CTS timing analysis using OpenROAD

    openroad
![36](https://github.com/user-attachments/assets/a1de1324-f3f4-4df7-84ac-eda0dd426d25)

    read_lef /openLANE_flow/designs/picorv32a/runs/08-09_14-03/tmp/merged.lef
    read_def /openLANE_flow/designs/picorv32a/runs/08-09_14-03/results/cts/picorv32a.cts.def
    write_db pico_cts.db
    read_db pico_cts.db
    read_verilog /openLANE_flow/designs/picorv32a/runs/08-09_14-03/results/synthesis/picorv32a.synthesis_cts.v
    read_liberty $::env(LIB_SYNTH_COMPLETE)
    link_design picorv32a
    read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
    set_propagated_clock [all_clocks]
    report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4
![37](https://github.com/user-attachments/assets/271257af-4300-48bd-ab2d-572d98a099c2)
![38](https://github.com/user-attachments/assets/539d4f47-568f-431d-9ff2-5542b85648bc)

####  Post-CTS OpenROAD timing analysis by removing 'sky130_fd_sc_hd__clkbuf_1' cell from clock buffer list variable 'CTS_CLK_BUFFER_LIST'.
    exit
    echo $::env(CTS_CLK_BUFFER_LIST)
    set ::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0]
    echo $::env(CTS_CLK_BUFFER_LIST)
![39](https://github.com/user-attachments/assets/8703e6eb-61be-4f5a-b8e6-7bcc241ea174)

    echo $::env(CURRENT_DEF)
    set ::env(CURRENT_DEF) /openLANE_flow/designs/picorv32a/runs/08-09_14-03/results/placement/picorv32a.placement.def
![40](https://github.com/user-attachments/assets/ccd250db-c834-4fd1-b0ce-de987fc38b65)

    run_cts
![41](https://github.com/user-attachments/assets/6e91d29c-8339-4453-830d-9847f9f3ffd1)
![42](https://github.com/user-attachments/assets/c2ddfda3-1be7-4b5c-af62-1e1ce71a4489)

    echo $::env(CTS_CLK_BUFFER_LIST)
    openroad
    read_lef /openLANE_flow/designs/picorv32a/runs/08-09_14-03/tmp/merged.lef
    write_db pico_cts.db
    read_db pico_cts.db
    read_verilog /openLANE_flow/designs/picorv32a/runs/08-09_14-03/results/synthesis/picorv32a.synthesis_cts.v
    read_liberty $::env(LIB_SYNTH_COMPLETE)
    link_design picorv32a
    read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
    set_propagated_clock [all_clocks]
    report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4
![43](https://github.com/user-attachments/assets/ff5ea9aa-e56e-4154-af80-f08a41b8d412)
![44](https://github.com/user-attachments/assets/182e38ca-aabf-42c6-808d-203ee40fea7f)
![45](https://github.com/user-attachments/assets/6160a727-8628-4290-a372-e952b6e3d3fb)

    report_clock_skew -hold
    report_clock_skew -setup
![46](https://github.com/user-attachments/assets/a535e973-1585-400e-8249-ba4f3348526a)

    echo $::env(CTS_CLK_BUFFER_LIST)
    set ::env(CTS_CLK_BUFFER_LIST) [linsert $::env(CTS_CLK_BUFFER_LIST) 0 sky130_fd_sc_hd__clkbuf_1]
    echo $::env(CTS_CLK_BUFFER_LIST)
![47](https://github.com/user-attachments/assets/503945e9-4016-420d-8382-71791f22dfe7)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## DAY-5 lab: Final steps for RTL2GDS using tritonRoute and openSTA
-----------------------------------------


### Power distibution network

    docker
    ./flow.tcl -interactive
    package require openlane 0.9
    prep -design picorv32a
    set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
    add_lefs -src $lefs
    set ::env(SYNTH_STRATEGY) "DELAY 1"
    set ::env(SYNTH_SIZING) 1
    run_synthesis
    init_floorplan
    place_io
    tap_decap_or
    run_placement
    run_cts
    gen_pdn
![1](https://github.com/user-attachments/assets/52ca21c4-ea3f-46c6-abef-a0789b0d6725)
![2](https://github.com/user-attachments/assets/c717a380-69f0-4e34-a608-1890746fb333)
![3](https://github.com/user-attachments/assets/e6913132-337d-4167-a729-e2446d459a46)

#### Load PDN def in magic

     cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-09_05-11/tmp/floorplan/
     magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read 14-pdn.def &
![4](https://github.com/user-attachments/assets/19ca15bc-0270-4527-a45c-ae7eded54a3d)
![5](https://github.com/user-attachments/assets/aef6a522-2c2b-43fb-977f-0ed762c22e60)
![6](https://github.com/user-attachments/assets/48493ca4-fd14-4f64-871c-5b6c9e88010b)
![7](https://github.com/user-attachments/assets/2125a9be-9102-4a26-a56b-abd0e7e132ec)

### Routing

    echo $::env(CURRENT_DEF)
    echo $::env(ROUTING_STRATEGY)
    run_routing
![8](https://github.com/user-attachments/assets/455ab94e-e056-4192-8cf8-70deea92b5e8)

0th optimization
![9](https://github.com/user-attachments/assets/a5792ec5-b722-46a7-8c8c-ae2596000c96)

57th optimization
![10](https://github.com/user-attachments/assets/7e2051a9-1973-4ce1-8659-1ab9aaaceba2)
![11](https://github.com/user-attachments/assets/e34be66f-44cd-4006-9ddf-808e32762fac)

#### Commands to load routed def in magic in another terminal

      cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-09_05-011/results/routing/
      magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.def &
![13](https://github.com/user-attachments/assets/3a926ceb-a3c7-4409-ab13-b0b2dd79c341)
![14](https://github.com/user-attachments/assets/15a53c43-1a23-4bdc-a6ac-0ed2c6b9a46c)
![15](https://github.com/user-attachments/assets/84499f77-916e-4494-a25e-331eff24977b)

#### fast route guide

      openlane/designs/picorv32a/runs/17-09_05-11/tmp/routing
      less 15-fastroute.guide
![12](https://github.com/user-attachments/assets/02abfa81-a38c-4fe4-8ece-5754afe5e3ee)


####  Post-Route parasitic extraction using SPEF extractor

      cd Desktop/work/tools/SPEF_EXTRACTOR
      python3 main.py /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-09_05-11/tmp/merged.lef /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-09_05-11/results/routing/picorv32a.def

### Post-Route OpenSTA timing analysis with the extracted parasitics

    docker
    ./flow.tcl -interactive
    package require openlane 0.9
    prep -design picorv32a -tag 17-09_05-11

    openroad
    read_lef /openLANE_flow/designs/picorv32a/runs/17-09_05-07/tmp/merged.lef
    read_def /openLANE_flow/designs/picorv32a/runs/17-09_05-07/results/routing/picorv32a.def
    write_db pico_route.db
    read_db pico_route.db
    read_verilog /openLANE_flow/designs/picorv32a/runs/17-09_05-07/results/synthesis/picorv32a.synthesis_preroute.v
    read_liberty $::env(LIB_SYNTH_COMPLETE)
    link_design picorv32a
    read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
    set_propagated_clock [all_clocks]
    read_spef /openLANE_flow/designs/picorv32a/runs/17-09_05-07/results/routing/picorv32a.spef
    report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4
    exit

![16](https://github.com/user-attachments/assets/33d00311-1d95-4fce-8b35-065d531b2d02)
![17](https://github.com/user-attachments/assets/25b6b638-b7fb-4321-8820-4877b04d7ba4)
![18](https://github.com/user-attachments/assets/6e3d287d-33aa-43c6-bb09-52ae92f0ec9e)




    
    

      

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

      
# Acknowledgements

* [Kunal Ghosh](https://github.com/kunalg123), Co-founder, VSD Corp. Pvt. Ltd.
* [Nickson P Jose](https://github.com/nickson-jose), Physical Design Engineer, Intel Corporation.
* [R. Timothy Edwards](https://github.com/RTimothyEdwards), Senior Vice President of Analog and Design, efabless Corporation.
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------








    
