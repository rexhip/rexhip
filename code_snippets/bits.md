
```pascal
// How to read a bit word from a device 

// Defind the bits in the word, make notice that msb is before lsb.
// (msb => most significant byte, lsb => least significant byte)
VAR
  status

END_


  "mb_query"(unit := __UNIT__,         
             fc := #mb.c.read.holding_reg,
             d_addr := __REGISTER__,
             d_len := 1,
             data := #bit_word,             
             mb := #mb);

// later in the program when one a bits need to be read, then
// just type #status.ready, eg for the ready bit.

// Same tecnicke can be used when a word is ggoing to be written to a device.
```
