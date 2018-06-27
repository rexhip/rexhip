### Changelog:

#### x.y.z
- Added the function block mb_delay_between_queries
- Parity error (80E1) and Framing error (80E2) included in comm_error for modbus rtu.

#### 2.3.4
- Bug fix in mb_delay.
- swap_real is removed from library, use swap together with dword_to_real instead.
- Updates to documentation.
- New SB's

#### 2.3.3
- mb_delay is now part of the library. The function is included in tcp example.
- For modbus tcp, setting qid to zero will not disconnect.
- New station blocks
- Documentation improvments.

#### 2.3.2
- Refactoring mb_query_bits, and fixed a bug.
- Added mb_delay function inside extend pack.
