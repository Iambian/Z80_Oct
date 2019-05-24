Z80 Instruction Set in Octal
============================
Notes:
* N represents a single byte constant value (8 bits)
* NN represents a two byte constant value (16 bits)
* Places that indicate $+2 or $+3 had their N or NN value assumed to be 0 because reasons
* The Y in the labeling indicates the value in the first column, where X indicates the value in the first row. (e.g. `LD E,N` would be 036)
* Many of the blank spots in the tables have a function, but aren't "documented". I'd fill them in but I didn't have a source for undocumented instructions immediately on-hand and I was having too much fun making tables to look up how to do things like color-coding in Markdown. Maybe tomorrow?

Main instruction set
--------------------

* 0YX

|+ |0           |1           |2           |3           |4          |5           |6           |7          |
|--|------------|------------|------------|------------|-----------|------------|------------|------------|
|0 | NOP        | LD BC,NN   | LD (BC),A  | INC BC     | INC B     | DEC B      | LD B,N     | RLCA       |
|1 | EX AF,AF'  | ADD HL,BC  | LD A,(BC)  | DEC BC     | INC C     | DEC C      | LD C,N     | RRCA       |
|2 | DJNZ $+2   | LD DE,NN   | LD (DE),A  | INC DE     | INC D     | DEC D      | LD D,N     | RLA        |
|3 | JR $+2     | ADD HL,DE  | LD A,(DE)  | DEC DE     | INC E     | DEC E      | LD E,N     | RRA        |
|4 | JR NZ,$+2  | LD HL,NN   | LD (NN),HL | INC HL     | INC H     | DEC H      | LD H,N     | DAA        |
|5 | JR Z,$+2   | ADD HL,HL  | LD HL,(NN) | DEC HL     | INC L     | DEC L      | LD L,N     | CPL        |
|6 | JR NC,$+2  | LD SP,NN   | LD (NN),A  | INC SP     | INC (HL)  | DEC (HL)   | LD (HL),N  | SCF        |
|7 | JR C,$+2   | ADD HL,SP  | LD A,(NN)  | DEC SP     | INC A     | DEC A      | LD A,N     | CCF        |

* 1YX

|+ |0           |1           |2           |3           |4          |5           |6           |7           |
|--|------------|------------|------------|------------|-----------|------------|------------|-------------
|0 | LD B,B     | LD B,C     | LD B,D     | LD B,E     | LD B,H    | LD B,L     | LD B,(HL)  | LD B,A     |
|1 | LD C,B     | LD C,C     | LD C,D     | LD C,E     | LD C,H    | LD C,L     | LD C,(HL)  | LD C,A     |
|2 | LD D,B     | LD D,C     | LD D,D     | LD D,E     | LD D,H    | LD D,L     | LD D,(HL)  | LD D,A     |
|3 | LD E,B     | LD E,C     | LD E,D     | LD E,E     | LD E,H    | LD E,L     | LD E,(HL)  | LD E,A     |
|4 | LD H,B     | LD H,C     | LD H,D     | LD H,E     | LD H,H    | LD H,L     | LD H,(HL)  | LD H,A     |
|5 | LD L,B     | LD L,C     | LD L,D     | LD L,E     | LD L,H    | LD L,L     | LD L,(HL)  | LD L,A     |
|6 | LD (HL),B  | LD (HL),C  | LD (HL),D  | LD (HL),E  | LD (HL),H | LD (HL),L  | HALT       | LD (HL),A  |
|7 | LD A,B     | LD A,C     | LD A,D     | LD A,E     | LD A,H    | LD A,L     | LD A,(HL)  | LD A,A     |

* 2YX

|+ |0           |1           |2           |3           |4          |5           |6           |7           |
|--|------------|------------|------------|------------|-----------|------------|------------|-------------
|0 | ADD A,B    | ADD A,C    | ADD A,D    | ADD A,E    | ADD A,H   | ADD A,L    | ADD A,(HL) | ADD A,A    |
|1 | ADC A,B    | ADC A,C    | ADC A,D    | ADC A,E    | ADC A,H   | ADC A,L    | ADC A,(HL) | ADC A,A    |
|2 | SUB B      | SUB C      | SUB D      | SUB E      | SUB H     | SUB L      | SUB (HL)   | SUB A      |
|3 | SBC B      | SBC C      | SBC D      | SBC E      | SBC H     | SBC L      | SBC (HL)   | SBC A      |
|4 | AND B      | AND C      | AND D      | AND E      | AND H     | AND L      | AND (HL)   | AND A      |
|5 | XOR B      | XOR C      | XOR D      | XOR E      | XOR H     | XOR L      | XOR (HL)   | XOR A      |
|6 | OR B       | OR C       | OR D       | OR E       | OR H      | OR L       | OR (HL)    | OR A       |
|7 | CP B       | CP C       | CP D       | CP E       | CP H      | CP L       | CP (HL)    | CP A       |

* 3YX

|+ |0           |1           |2           |3           |4          |5           |6           |7           |
|--|------------|------------|------------|------------|-----------|------------|------------|-------------
|0 | RET NZ     | POP BC     | JP NZ,$+3  | JP $+3     | CALL NZ,NN| PUSH BC    | ADD A,N    | RST 0      |
|1 | RET Z      | RET        | JP Z,$+3   | [EXT CB]   | CALL Z,NN | CALL NN    | ADC A,N    | RST 8H     |
|2 | RET NC     | POP DE     | JP NC,$+3  | OUT (N),A  | CALL NC,NN| PUSH DE    | SUB N      | RST 10H    |
|3 | RET C      | EXX        | JP C,$+3   | IN A,(N)   | CALL C,NN | [EXT DD];  | SBC A,N    | RST 18H    |
|4 | RET PO     | POP HL     | JP PO,$+3  | EX (SP),HL | CALL PO,NN| PUSH HL    | AND N      | RST 20H    |
|5 | RET PE     | JP (HL)    | JP PE,$+3  | EX DE,HL   | CALL PE,NN| [EXT ED]   | XOR N      | RST 28H    |
|6 | RET P      | POP AF     | JP P,$+3   | DI         | CALL P,NN | PUSH AF    | OR N       | RST 30H    |
|7 | RET M      | LD SP,HL   | JP M,$+3   | EI         | CALL M,NN | [EXT FD]   | CP N       | RST 38H    |

203 [CB] Prefix
---------------

* 0YX

|+ |0           |1           |2           |3           |4           |5           |6           |7           |
|--|---------------|------------|------------|------------|-----------|------------|------------|-------------
|0 | RLC B      | RLC C      | RLC D      | RLC E      | RLC H     | RLC L      | RLC (HL)   | RLC A      |
|1 | RRC B      | RRC C      | RRC D      | RRC E      | RRC H     | RRC L      | RRC (HL)   | RRC A      |
|2 | RL  B      | RL  C      | RL  D      | RL  E      | RL  H     | RL  L      | RL  (HL)   | RL  A      |
|3 | RR  B      | RR  C      | RR  D      | RR  E      | RR  H     | RR  L      | RR  (HL)   | RR  A      |
|4 | SLA B      | SLA C      | SLA D      | SLA E      | SLA H     | SLA L      | SLA (HL)   | SLA A      |
|5 |            |            |            |            |           |            |            |            |
|6 | SRA B      | SRA C      | SRA D      | SRA E      | SRA H     | SRA L      | SRA (HL)   | SRA A      |
|7 | SRL B      | SRL C      | SRL D      | SRL E      | SRL H     | SRL L      | SRL (HL)   | SRL A      |

* 1YX

|+ |0           |1           |2           |3           |4           |5           |6           |7           |
|--|---------------|------------|------------|------------|-----------|------------|------------|-------------
|0 | BIT 0,B    | BIT 0,C    | BIT 0,D    | BIT 0,E    | BIT 0,H   | BIT 0,L    | BIT 0,(HL) | BIT 0,A    |
|1 | BIT 1,B    | BIT 1,C    | BIT 1,D    | BIT 1,E    | BIT 1,H   | BIT 1,L    | BIT 1,(HL) | BIT 1,A    |
|2 | BIT 2,B    | BIT 2,C    | BIT 2,D    | BIT 2,E    | BIT 2,H   | BIT 2,L    | BIT 2,(HL) | BIT 2,A    |
|3 | BIT 3,B    | BIT 3,C    | BIT 3,D    | BIT 3,E    | BIT 3,H   | BIT 3,L    | BIT 3,(HL) | BIT 3,A    |
|4 | BIT 4,B    | BIT 4,C    | BIT 4,D    | BIT 4,E    | BIT 4,H   | BIT 4,L    | BIT 4,(HL) | BIT 4,A    |
|5 | BIT 5,B    | BIT 5,C    | BIT 5,D    | BIT 5,E    | BIT 5,H   | BIT 5,L    | BIT 5,(HL) | BIT 5,A    |
|6 | BIT 6,B    | BIT 6,C    | BIT 6,D    | BIT 6,E    | BIT 6,H   | BIT 6,L    | BIT 6,(HL) | BIT 6,A    |
|7 | BIT 7,B    | BIT 7,C    | BIT 7,D    | BIT 7,E    | BIT 7,H   | BIT 7,L    | BIT 7,(HL) | BIT 7,A    |

* 2YX

|+ |0           |1           |2           |3           |4           |5           |6           |7           |
|--|---------------|------------|------------|------------|-----------|------------|------------|-------------
|0 | RES 0,B    | RES 0,C    | RES 0,D    | RES 0,E    | RES 0,H   | RES 0,L    | RES 0,(HL) | RES 0,A    |
|1 | RES 1,B    | RES 1,C    | RES 1,D    | RES 1,E    | RES 1,H   | RES 1,L    | RES 1,(HL) | RES 1,A    |
|2 | RES 2,B    | RES 2,C    | RES 2,D    | RES 2,E    | RES 2,H   | RES 2,L    | RES 2,(HL) | RES 2,A    |
|3 | RES 3,B    | RES 3,C    | RES 3,D    | RES 3,E    | RES 3,H   | RES 3,L    | RES 3,(HL) | RES 3,A    |
|4 | RES 4,B    | RES 4,C    | RES 4,D    | RES 4,E    | RES 4,H   | RES 4,L    | RES 4,(HL) | RES 4,A    |
|5 | RES 5,B    | RES 5,C    | RES 5,D    | RES 5,E    | RES 5,H   | RES 5,L    | RES 5,(HL) | RES 5,A    |
|6 | RES 6,B    | RES 6,C    | RES 6,D    | RES 6,E    | RES 6,H   | RES 6,L    | RES 6,(HL) | RES 6,A    |
|7 | RES 7,B    | RES 7,C    | RES 7,D    | RES 7,E    | RES 7,H   | RES 7,L    | RES 7,(HL) | RES 7,A    |

* 3YX

|+ |0           |1           |2           |3           |4           |5           |6           |7           |
|--|---------------|------------|------------|------------|-----------|------------|------------|-------------
|0 | SET 0,B    | SET 0,C    | SET 0,D    | SET 0,E    | SET 0,H   | SET 0,L    | SET 0,(HL) | SET 0,A    |
|1 | SET 1,B    | SET 1,C    | SET 1,D    | SET 1,E    | SET 1,H   | SET 1,L    | SET 1,(HL) | SET 1,A    |
|2 | SET 2,B    | SET 2,C    | SET 2,D    | SET 2,E    | SET 2,H   | SET 2,L    | SET 2,(HL) | SET 2,A    |
|3 | SET 3,B    | SET 3,C    | SET 3,D    | SET 3,E    | SET 3,H   | SET 3,L    | SET 3,(HL) | SET 3,A    |
|4 | SET 4,B    | SET 4,C    | SET 4,D    | SET 4,E    | SET 4,H   | SET 4,L    | SET 4,(HL) | SET 4,A    |
|5 | SET 5,B    | SET 5,C    | SET 5,D    | SET 5,E    | SET 5,H   | SET 5,L    | SET 5,(HL) | SET 5,A    |
|6 | SET 6,B    | SET 6,C    | SET 6,D    | SET 6,E    | SET 6,H   | SET 6,L    | SET 6,(HL) | SET 6,A    |
|7 | SET 7,B    | SET 7,C    | SET 7,D    | SET 7,E    | SET 7,H   | SET 7,L    | SET 7,(HL) | SET 7,A    |


237 [ED] Prefix
---------------

* 0YX

|+ |0           |1           |2           |3           |4           |5           |6           |7           |
|--|---------------|------------|------------|------------|-----------|------------|------------|-------------|
|0 | -- | -- | -- | -- | --| -- | -- | -- |
|1 | -- | -- | -- | -- | --| -- | -- | -- |
|2 | -- | -- | -- | -- | --| -- | -- | -- |
|3 | -- | -- | -- | -- | --| -- | -- | -- |
|4 | -- | -- | -- | -- | --| -- | -- | -- |
|5 | -- | -- | -- | -- | --| -- | -- | -- |
|6 | -- | -- | -- | -- | --| -- | -- | -- |
|7 | -- | -- | -- | -- | --| -- | -- | -- |

* 1YX

|+ |0           |1           |2           |3           |4           |5           |6           |7           |
|--|---------------|------------|------------|------------|-----------|------------|------------|-------------
|0 | IN B,(C)    | OUT (C),B   | SBC HL,BC   | LD (NN),BC  | NEG        | RETN        | IM 0        | LD I,A      |
|1 | IN C,(C)    | OUT (C),C   | ADC HL,BC   | LD BC,(NN)  | --         | RETI        | --          | --          |
|2 | IN D,(C)    | OUT (C),D   | SBC HL,DE   | LD (NN),DE  | --         | --          | IM 1        | LD A,I      |
|3 | IN E,(C)    | OUT (C),E   | ADC HL,DE   | LD DE,(NN)  | --         | --          | IM 2        | --          |
|4 | IN H,(C)    | OUT (C),H   | SBC HL,HL   | --          | --         | --          | --          | RRD         |
|5 | IN L,(C)    | OUT (C),L   | ADC HL,HL   | --          | --         | --          | --          | RLD         |
|6 | --          | --          | SBC HL,SP   | LD (NN),SP  | --         | --          | --          | --          |
|7 | IN A,(C)    | OUT (C),A   | ADC HL,SP   | LD SP,(NN)  | --         | --          | --          | --          |

* 2YX

|+ |0           |1           |2           |3           |4           |5           |6           |7           |
|--|---------------|------------|------------|------------|-----------|------------|------------|-------------
|0 | --          | --          | --          | --          | --         | --          | --          | --          |
|1 | --          | --          | --          | --          | --         | --          | --          | --          |
|2 | LDI         | CPI         | INI         | OUTI        | --         | --          | --          | --          |
|3 | LDD         | CPD         | IND         | OUTD        | --         | --          | --          | --          |
|4 | LDIR        | CPIR        | INIR        | OTIR        | --         | --          | --          | --          |
|5 | LDDR        | CPDR        | INDR        | OTDR        | --         | --          | --          | --          |
|6 | --          | --          | --          | --          | --         | --          | --          | --          |
|7 | --          | --          | --          | --          | --         | --          | --          | --          |

* 3YX

|+ |0           |1           |2           |3           |4           |5           |6           |7           |
|--|---------------|------------|------------|------------|-----------|------------|------------|-------------|
|0 | -- | -- | -- | -- | --| -- | -- | -- |
|1 | -- | -- | -- | -- | --| -- | -- | -- |
|2 | -- | -- | -- | -- | --| -- | -- | -- |
|3 | -- | -- | -- | -- | --| -- | -- | -- |
|4 | -- | -- | -- | -- | --| -- | -- | -- |
|5 | -- | -- | -- | -- | --| -- | -- | -- |
|6 | -- | -- | -- | -- | --| -- | -- | -- |
|7 | -- | -- | -- | -- | --| -- | -- | -- |

221 [DD] Prefix:
----------------
* 0YX

|+ |0           |1           |2           |3           |4           |5           |6           |7           |
|--|---------------|------------|------------|------------|-----------|------------|------------|-------------
|0 | --            | --            | --            | --            | --           | --            | --            | --            |
|1 | --            | ADD IX,BC     | --            | --            | --           | --            | --            | --            |
|2 | --            | --            | --            | --            | --           | --            | --            | --            |
|3 | --            | ADD IX,DE     | --            | --            | --           | --            | --            | --            |
|4 | --            | LD IX,NN      | LD (NN),IX    | INC IX        | --           | --            | --            | --            |
|5 | --            | ADD IX,IX     | LD IX,(NN)    | DEC IX        | --           | --            | --            | --            |
|6 | --            | --            | --            | --            | INC (IX+N)   | DEC (IX+N)    | LD (IX+N),N   | --            |
|7 | --            | ADD IX,SP     | --            | --            | --           | --            | --            | --            |

* 1YX

|+ |0           |1           |2           |3           |4           |5           |6           |7           |
|--|---------------|------------|------------|------------|-----------|------------|------------|-------------
|0 | --            | --            | --            | --            | --           | --            | LD B,(IX+N)   | --            |
|1 | --            | --            | --            | --            | --           | --            | LD C,(IX+N)   | --            |
|2 | --            | --            | --            | --            | --           | --            | LD D,(IX+N)   | --            |
|3 | --            | --            | --            | --            | --           | --            | LD E,(IX+N)   | --            |
|4 | --            | --            | --            | --            | --           | --            | LD H,(IX+N)   | --            |
|5 | --            | --            | --            | --            | --           | --            | LD L,(IX+N)   | --            |
|6 | LD (IX+N),B   | LD (IX+N),C   | LD (IX+N),D   | LD (IX+N),E   | LD (IX+N),H  | LD (IX+N),L   | --            | LD (IX+N),A   |
|7 | --            | --            | --            | --            | --           | --            | LD A,(IX+N)   | --            |

* 2YX

|+ |0           |1           |2           |3           |4           |5           |6           |7           |
|--|---------------|------------|------------|------------|-----------|------------|------------|-------------
|0 | --            | --            | --            | --            | --           | --            | ADD A,(IX+N)  | --            |
|1 | --            | --            | --            | --            | --           | --            | ADC A,(IX+N)  | --            |
|2 | --            | --            | --            | --            | --           | --            | SUB (IX+N)    | --            |
|3 | --            | --            | --            | --            | --           | --            | SBC A,(IX+N)  | --            |
|4 | --            | --            | --            | --            | --           | --            | AND (IX+N)    | --            |
|5 | --            | --            | --            | --            | --           | --            | XOR (IX+N)    | --            |
|6 | --            | --            | --            | --            | --           | --            | OR (IX+N)     | --            |
|7 | --            | --            | --            | --            | --           | --            | CP (IX+N)     | --            |

* 3YX

|+ |0           |1           |2           |3           |4           |5           |6           |7           |
|--|---------------|------------|------------|------------|-----------|------------|------------|-------------
|0 | --            | --            | --            | --            | --           | --            | --            | --            |
|1 | --            | --            | --            | [CB EXT]      | --           | --            | --            | --            |
|2 | --            | --            | --            | --            | --           | --            | --            | --            |
|3 | --            | --            | --            | --            | --           | --            | --            | --            |
|4 | --            | POP IX        | --            | EX (SP),IX    | --           | PUSH IX       | --            | --            |
|5 | --            | JP (IX)       | --            | --            | --           | --            | --            | --            |
|6 | --            | --            | --            | --            | --           | --            | --            | --            |
|7 | --            | LD SP,IX      | --            | --            | --           | --            | --            | --            |

Note: All listed targets in [CB EXT] exchanges (HL) with (IX). No other combinations
appear to be listed. The opcode includes a displacement value (ex. `RLC (IX+N)`)
between the CB prefix and the extension dictated by that opcode (ex. `CB 06` 
becomes `DD CB XX 06`)

253 [FD] Prefix:
----------------
The same as the DD prefix, except it affects IY instead of IX
