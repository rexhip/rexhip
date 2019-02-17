### How to read bits in a holding register 

```pascal
VAR 
  // Defind the bits in the word, make notice that msb is defined before lsb.
  // (msb => most significant byte, lsb => least significant byte)
  // Bits that are not in use, also need to be defined to create the 
  // corret offset.
  status : Struct
     x08 : Bool;
     x09 : Bool;
     x10 : Bool;
     x11_ready : Bool;
     x12 : Bool;
     x13_running : Bool;
     x14 : Bool;
     x15 : Bool;
     x00 : Bool;
     x01 : Bool;
     x02 : Bool;
     x03_alarm : Bool;
     x04_overheat : Bool;
     x05_fan_alarm : Bool;
     x06 : Bool;
     x07 : Bool;
  END_STRUCT;  
END_VAR

// A normal query.
#mb_query(mb_addr := ___MB_ADDR___,         
          mode := #mb_query.c.read.holding_reg,
          data_addr := ___REGISTER___,          
          data_ptr := #status ); // Read the whole word         

// Later in the program when a bits need to be read, then a bit 
// can be referred to directly. Eg. #status.x11_ready, for the 
// ready bit in this example

IF #status.x11_ready THEN
    ; // Do something.	    
END_IF;

// Same technique can be used when a bit-word need to be written to 
// a holding register.
```
