
```pascal
// How to read bits in a holding register 

// Defind the bits in the word, make notice that msb is before lsb.
// (msb => most significant byte, lsb => least significant byte)
VAR
  status

END_

  // A normal query.
  "mb_query"(unit := __UNIT__,         
             fc := #mb.c.read.holding_reg,
             d_addr := __REGISTER__,
             d_len := 1,
             data := #status, // Read the whole word
             mb := #mb);

// Later in the program when one a bits need to be read, then
// just type refer to the bit. Eg. #status.ready, eg for the ready bit.

if #status.ready then
    // Do something.
end_if;

// Same tecnicke can be used when a word need to be written to 
// a holding register.
```
