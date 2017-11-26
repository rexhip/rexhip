Quick starter guide:
 - Download the latest release. (https://github.com/olab84/rexhip/releases)
 - Start a new project in TIA-portal, and then add new PLC.
 - Localise "External Source files" in the tree structure and import the files inside the lib-folder of the downloaded zip-file.
 - Select the imported files, right click them and choose "Generate blocks from source".
 - Open the "Station_block" folder and see if there alleredy exist a SB for your device, if not you can study the start examples and customize the code for your modbus device.
 - Blocks that are not need should be deleted, to save memory.
 
 Requirements:
 - Software: TIA-portal: v14, sp1, Upd 2
 - Hardware: S7-1200: fw >= 4.2 or S7-1500: fw >= 2.0  
 - For older fw. use version 1.

Same memory:

If the library is only used for tcp then all blocks related to rtu can be removed to save memory. Equally all tcp blocks can be removed if the library is only used for rtu. There are two solution for rtu application one for S7-1200, mb_master_ctrl. And there is one other for S7-1500,  mb_master_1500_ctrl. Delete the block that isn't used to save memory.

Auto data_len:

The liberay is able to determine the data_len parmeter automatically for holding and input register. This feature only works digital input and outputs, when the number of bits adds up to whole bytes. (See auto_data_len.md and for more information)

OB-call:

All query blocks connected to a controller has to be called in the same order for each scan, implicate they have to be called from the same OB.

Functionality included:

The library extend on the master bloks and the client block that comes along with TIA portal. The library doesn't includes any functionality for modbus slave or modbus server. Take a look at MB_SLAVE or MB_SERVER, which is included in TIA-portal, for those functionalities.

More readings about modbus in the links bellow:
 - http://www.csimn.com/CSI_pages/Modbus101.html
 - http://www.simplymodbus.ca/FAQ.htm
 - http://www.modbus.org/specs.php
