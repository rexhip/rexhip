
Modbus lightweight abstraction layer library for Siemens PLC.

Alpaha realease

Introduction 
============
Since 1979 Modbus has been a blessing and a curse for automation engineers. A blessing in the sense of being one of the first open, de facto standard, communication protocols for automation equipment, and still is today. A curse in the way of lacking of clear specifications, and several bad design decisions.

                 .--------------.
        Enable --|              |
                 |   mb_read    |                 
   Device_addr --|              |-- data_out                 
                 |              |
     Data_addr --|              |
                 |              |
       Length  --|              |
                 |              |                 
        udt_mb --|              |
                 '--------------'
