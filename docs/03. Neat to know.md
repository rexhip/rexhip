Neat to know
------------

## Same memory:

If the library is only used for tcp then all blocks related to rtu can be removed to save memory. Equally all tcp blocks can be removed if the library is only used for rtu. There are two solution for rtu application one for S7-1200, mb_master_ctrl. And there is one other for S7-1500,  mb_master_1500_ctrl. Delete the block that isn't used to save memory.

## Auto data_len:

The liberay is able to determine the data_len parmeter automatically for holding and input register. This feature only works when the number of bits adds up to whole bytes. (See also: «auto_data_len.md» and «mb_query_bits.md»)

## OB-call:

All query blocks connected to a controller has to be called in the same order for each scan, implicate they have to be called from the same OB.

## Functionality included:

The library extend on the master bloks and the client block that comes along with TIA portal. The library doesn't includes any functionality for modbus slave or modbus server. Take a look at MB_SLAVE or MB_SERVER, which is included in TIA-portal, for those functionalities.
