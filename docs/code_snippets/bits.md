### How to read bits in a holding register 

```pascal
VAR 
  // Defind the bits in the word, make notice that msb is defined before lsb.
  // (msb => most significant byte, lsb => least significant byte)
  // Bits that are not in use, also need to be defined to create the 
  // corret offset.
  status : Struct
     b8 : Bool;
     b9 : Bool;
     b10 : Bool;
     b11_ready : Bool;
     b12 : Bool;
     b13_running : Bool;
     b14 : Bool;
     b15 : Bool;
     b0 : Bool;
     b1 : Bool;
     b2 : Bool;
     b3_alarm : Bool;
     b4_overheat : Bool;
     b5_fan_alarm : Bool;
     b6 : Bool;
     b7 : Bool;
  END_STRUCT;  
END_VAR

// A normal query.
#mb_query(mb_addr := mb_addr,         
          mode := #mb_query.c.read.holding_reg,
          data_addr := __REGISTER__,          
          data_ptr := #status); // Read the whole word         

// Later in the program when a bits need to be read, then a bit 
// can be referred to directly. Eg. #status.b11_ready, for the 
// ready bit in this example

IF #status.b11_ready THEN
    // Do something.	    
END_IF;

// Same technique can be used when a bit-word need to be written to 
// a holding register.
```
