The software is written for both S7-1200 and S7-1500 series, 
but is unfortunately not supported for S7-300 and S7-400 series. 

If the library is only used for rtu then all blocks related 
to tcp can be removed to save memory. Equally all rtu 
blocks can be removed if the library is only used for tcp.
Alternatively can blocks that are not used, be moved to the
library. (To the right in TIA-portal)

OB-call: 
All query blocks connected to a controller has to be called in 
the same order for each scan, implicate they have to be called 
from the same OB.

The library extend on MB_MASTER and MB_CLIENT that comes 
along with TIA portal. The library doesn't includes any 
functionality for modbus slave or modbus server. Take a look 
at MB_SLAVE or MB_SERVER, which is included in TIA-portal, 
for those functionalities.

To understand the examples it's recommended to acquire some 
basic knowlage about modbus. More readings at the links bellow:
 - http://www.csimn.com/CSI_pages/Modbus101.html
 - http://www.simplymodbus.ca/FAQ.htm
 - http://www.modbus.org/specs.php
