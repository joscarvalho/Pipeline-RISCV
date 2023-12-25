# README

## Unitary tests for the different instructions

- Load word (lw)
  ```
  1 ###############################################
  2 # TEST:
  3 # 1) Write FFFFFD55 into register x7;
  4 # 2) Store the value of x7 into memory at 0x96.
  5 # 3) Load word into register x2.
  6 # Expected output: <word read>
  7 # x2 = 0x96 (FFFFFD55)
  8 # 4) Store the value of x2 into memory at 0x08.
  9 # Expected output: <word read>
  10 # 0x08 = FFFFFD55
  11 ###############################################
  12
  13 D5500393 addi x7,x0,<teste>
  14 06702023 sw x7,96(x0)
  15 06002103 lw x2,96(x0)
  16 00202423 sw x2,08(x0)
  17 00210063 beq x2, x2, <loop>
  ```

- Load half (lh)
  ```
  1 ###############################################
  2 # TEST:
  3 # 1) Write FFFFFD55 into 0x00;
  4 # 2) Load 4 half words into registers.
  5 # Expected output: FFFF_<half word read>
  6 # x1 = 0x00 (FFFF_FD55)
  7 # x2 = 0x01 (FFFF_FFFD)
  8 # x3 = 0x02 (FFFF_FFFF)
  9 # x4 = 0x03 (XXXXXXXX)
  10 # 3) Write registers values into memory.
  11 # 0x04 = x1 (FFFF_FD55)
  12 # 0x08 = x2 (FFFF_FFFD)
  13 # 0x0c = x3 (FFFF_FFFF)
  14 # 0x10 = x4 (XXXXXXXX)
  15 ###############################################
  16
  17 D5500393 addi x7,x0,<teste>
  18 00702023 sw x7,00(x0)
  19 00001083 lh x1,00(x0)
  20 00101103 lh x2,01(x0)
  21 00201183 lh x3,02(x0)
  22 00301203 lh x4,03(x0)
  23 00102223 sw x1,04(x0)
  24 00202423 sw x2,08(x0)
  25 00302623 sw x3,0c(x0)
  26 00402823 sw x4,10(x0)
  27 00210063 beq x2, x2, <loop>
  ```
  
- Load half unsigned (lhu)
  ```
  1 ###############################################
  2 # TEST:
  3 # 1) Write FFFFFD55 into 0x00;
  4 # 2) Load 4 half words into registers.
  5 # Expected output: 0000_<half word read>
  6 # x1 = 0x00 (0000_FD55)
  7 # x2 = 0x01 (0000_FFFD)
  8 # x3 = 0x02 (0000_FFFF)
  9 # x4 = 0x03 (XXXXXXXX)
  10 # 3) Write registers values into memory.
  11 # 0x04 = x1 (0000_FD55)
  12 # 0x08 = x2 (0000_FFFD)
  13 # 0x0c = x3 (0000_FFFF)
  14 # 0x10 = x4 (XXXXXXXX)
  15 ###############################################
  16
  17 D5500393 addi x7,x0,<teste>
  18 00702023 sw x7,00(x0)
  19 00005083 lhu x1,00(x0)
  20 00105103 lhu x2,01(x0)
  21 00205183 lhu x3,02(x0)
  22 00305203 lhu x4,03(x0)
  23 00102223 sw x1,04(x0)
  24 00202423 sw x2,08(x0)
  25 00302623 sw x3,0c(x0)
  26 00402823 sw x4,10(x0)
  27 00210063 beq x2, x2, <loop>
  ```

- Load byte (lb)
  ```
  1 #################################################
  2 TEST:
  3 1) Write FFFFFD55 into 0x00;
  4 2) Load 4 bytes into registers.
  5 Expected output: FFFFFF_<byte read>
  6 x1 = 0x00 (FFFFFF_55)
  7 x2 = 0x01 (FFFFFF_FD)
  8 x3 = 0x02 (FFFFFF_FF)
  9 x4 = 0x03 (FFFFFF_FF)
  10 3) Write registers values into memory.
  11 0x04 = x1 (FFFFFF_55)
  12 0x08 = x2 (FFFFFF_FD)
  13 0x0c = x3 (FFFFFF_FF)
  14 0x10 = x4 (FFFFFF_FF)
  15 ################################################
  16
  17 D5500393 addi x7,x0,<teste>
  18 00702023 sw x7,00(x0)
  19 00000083 lb x1,00(x0)
  20 00100103 lb x2,01(x0)
  21 00200183 lb x3,02(x0)
  22 00300203 lb x4,03(x0)
  23 00102223 sw x1,04(x0)
  24 00202423 sw x2,08(x0)
  25 00302623 sw x3,0c(x0)
  26 00402823 sw x4,10(x0)
  27 00210063 beq x2, x2, <loop>
  ```
  
- Load byte unsigned (lbu)
  ```
  1 #################################################
  2 TEST:
  3 1) Write FFFFFD55 into 0x00;
  4 2) Load 4 bytes into registers.
  5 Expected output: 000000_<byte read>
  6 x1 = 0x00 (000000_55)
  7 x2 = 0x01 (000000_FD)
  8 x3 = 0x02 (000000_FF)
  9 x4 = 0x03 (000000_FF)
  10 3) Write registers values into memory.
  11 0x04 = x1 (000000_55)
  12 0x08 = x2 (000000_FD)
  13 0x0c = x3 (000000_FF)
  14 0x10 = x4 (000000_FF)
  15 ################################################
  16
  17 D5500393 addi x7,x0,<teste>
  18 00702023 sw x7,00(x0)
  19 00004083 lbu x1,00(x0)
  20 00104103 lbu x2,01(x0)
  21 00204183 lbu x3,02(x0)
  22 00304203 lbu x4,03(x0)
  23 00102223 sw x1,04(x0)
  24 00202423 sw x2,08(x0)
  25 00302623 sw x3,0c(x0)
  26 00402823 sw x4,10(x0)
  27 00210063 beq x2, x2, <loop>
  ```
  
- Stores (sw, sh, sb)
  ```
  1 #####################################################
  2 TEST:
  3 1) Write FFFFFD55 into 0x00;
  4 2) Store word into 0x00.
  5 3) Store half-word into 0x04.
  6 4) Store byte into 0x08.
  7 3) Read values from memory to registers.
  8 x1 = 0x00 (FFFFFD55)
  9 x2 = 0x04 (<First 2 bytes of memory>_FD55)
  10 x3 = 0x08 (<First 3 bytes of memory>_55)
  11 ######################################################
  12
  13 D5500393 addi x7,x0,<teste>
  14 00702023 sw x7,00(x0)
  15 00701223 sh x7,04(x0)
  16 00700423 sb x7,08(x0)
  17 00002083 lw x1,00(x0)
  18 00402103 lw x2,04(x0)
  19 00802183 lw x3,08(x0)
  20 00210063 beq x2, x2, <loop>
  ```
  
- Jump and Link Register (jalr)
  ```
  1 #####################################################
  2 TEST 1:
  3 1) Write FFFFF555 into 0x00;
  4 2) Jump and link register;
  5 Expected output:
  6 PC = x7 + 2 = 555 + 2 = 557
  7 x1 = PC + 4 = 555 + 4 = 559
  8
  9 55500393 addi x7,x0,<teste>
  10 002380E7 jalr x1,x7,2
  11 00102023 sw x1,00(x0)
  12
  13 TEST 2:
  14 1) Write FFFFF004 into 0x00;
  15 2) Jump and link register;
  16 Expected output:
  17 PC = x7 + 4 = 4 + 4 = 8
  18 x1 = PC + 4 = 4 + 4 = 8
  19
  20 00400393 addi x7,x0,<teste>
  21 004380E7 jalr x1,x7,2
  22 00102023 sw x1,00(x0)
  ```
  
- Load upper Imediate (lui) and Add Uper Imediate (aupic)
  ```
  1 #####################################################
  2 TEST:
  3 1) Load upper immediate into register x1
  4 x1 = 0x1000
  5 2) Store the value of x1 into 0x00
  6 0x00 = 0x00001000
  7 3) Add upper immediate to PC into register x1
  8 x1 = 0x1000 + PC = 0x1000 + 8 = 0x1008
  9 4) Store the value of x1 into 0x00
  10 0x00 = 0x00001008
  11
  12 000010B7 lui x1,1
  13 00102023 sw x1,0(x0)
  14 00001097 auipc x1,1
  15 00102023 sw x1,00(x0)
  ```
  
- Branches (beq, bne, blt, bltu, bge, bgeu)
  ```
  1 #####################################################
  2 TEST:
  3 1) Branch equal:
  4 if ( x0 == x0 ) -> branch taken
  5
  6 2) Branch not equal:
  7 x7 = 0xFFFFFD55
  8 x0 = 0x00000000
  9 if ( x7 != x0 ) -> branch taken
  10
  11 3) Branch less than
  12 x7 = 0xFFFFFFF8 (-8)
  13 x0 = 0x00000000
  14 if ( x7 < x0 ) -> branch taken
  15
  16 4) Branch less than unsigned
  17 x7 = 0xFFFFFFF8 (-8)
  18 x0 = 0x00000000
  19 x2 = 0x00000005 (+5)
  20 if ( x7 < x0 ) -> branch not taken
  21 if ( x2 < x7 ) -> branch taken
  22
  23 5) Branch bigger than
  24 x7 = 0x00000008
  25 x0 = 0x00000000
  26 if ( x7 >= x0 ) -> branch taken
  27
  28 6) Branch bigger than unsigned
  29 x7 = 0xFFFFFFF8 (-8)
  30 x0 = 0x00000000
  31 if ( x7 >= x0 ) -> branch taken
  32
  33 #####################################################
  34
  35 00000FE3 beq x0,x0,<label>
  36
  37 D5500393 addi x7,x0,<teste>
  38 00039FE3 bne x7,x0,<label>
  39
  40 FF800393 addi x7,x0,<teste> (negative value)
  41 0003CFE3 blt x7,x0,<label>
  42
  43 FF800393 addi x7,x0,<teste> (negative value)
  44 0003EFE3 bltu x7,x0,<label>
  45 00500113 addi x2, x0, 5
  46 00716FE3 bltu x2,x7,<label>
  47
  48 00800393 addi x7,x0,<teste> (positive value)
  49 0003DFE3 bge x7,x0,<label>
  50
  51 FF800393 addi x7,x0,<teste> (negative value)
  52 0003FFE3 bgeu x7,x0,<label>
  ```

## Integration Tests

- Limited instruction set test (riscmem.mem)
  ```
  1 ###############################################
  2 # Expected output: 0x64 = 25 (0x19)
  3 ###############################################
  4
  5 main:
  6 00500113 addi x2, x0, 5 # x2 = 5
  7 00C00193 addi x3, x0, 12 # x3 = 12
  8 FF718393 addi x7, x3, -9 # x7 = (12 - 9) = 3
  9 0023E233 or x4, x7, x2 # x4 = (3 OR 5) = 7
  10 0041F2B3 and x5, x3, x4 # x5 = (12 AND 7) = 4
  11 004282B3 add x5, x5, x4 # x5 = 4 + 7 = 11
  12 02728863 beq x5, x7, end # should not be taken
  13 0041A233 slt x4, x3, x4 # x4 = (12 < 7) = 0
  14 00020463 beq x4, x0, around # should be taken
  15 00000293 addi x5, x0, 0
  16 around:
  17 0023A233 slt x4, x7, x2 # x4 = (3 < 5) = 1
  18 005203B3 add x7, x4, x5 # x7 = (1 + 11) = 12
  19 402383B3 sub x7, x7, x2 # x7 = (12 - 5) = 7
  20 0471AA23 sw x7, 84(x3) # [96] = 7
  21 06002103 lw x2, 96(x0) # x2 = [96] = 7
  22 005104B3 add x9, x2, x5 # x9 = (7 + 11) = 18
  23 008001EF jal x3, end # jump to end, x3 = 0x44
  24 00100113 addi x2, x0, 1 # should not execute
  25 end:
  26 00910133 add x2, x2, x9 # x2 = (7 + 18) = 25
  27 0221A023 sw x2, 0x20(x3) # [100] = 25
  28 done:
  29 00210063 beq x2, x2, done # infinite loop
  ```
  
- Instruction set test (RiscVTest.mem)
  ```
  1 ###############################################
  2 # Expected output: 0x50 = 25 (0x19)
  3 ###############################################
  4
  5 main:
  6 00500113 addi x2, x0, 5 # x2 = 5
  7 00C00193 addi x3, x0, 12 # x3 = 12
  8 00316213 ori x4, x2, 3 # x4 = (5 OR 3) = 7
  9 003142B3 xor x5, x2, x3 # x5 = (5 XOR 12) = 9
  10 04527463 bgeu x4, x5, end # Should not be taken
  11 00111113 slli x2, x2, 1 # x2 = x2 << 1 = 10
  12 0051F193 andi x3, x3 5 # x3 = (x3 AND 5) = 4
  13 0021D213 srai x4, x3, 2 # x4 = (x3 >>> 2) = 1
  14 02400423 sb x4, 0x28(x0) # [40] = 1
  15 00321463 bne x4, x3, next # Should be taken
  16 004102B3 add x5, x2, x4 # Should not execute
  17 next:
  18 02800103 lb x2, 0x28(x0) # x2 = [40] = 1
  19 01400293 addi x5, x0, 20 # x5 = 0 + 20 = 20
  20 00001237 lui x4, 1 # x4 = 4096
  21 FFF23193 sltiu x3, x4, -1 # x3 = (x4 < -1) = 1
  22 01818213 addi x4, x3, 24 # x4 = (1 + 24) = 25
  23 00310463 beq x3, x2, end # Should be taken
  24 00700213 addi x4, x0, 7 # Should not execute
  25 end:
  26 0442A823 sw x4, 0x50(x5) # [80] = 25
  27 done:
  28 00210063 beq x2,x2,done # Infinite Loop
  ```
  
