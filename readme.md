Z80 Instruction Set in Octal
----------------------------

0YX

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

1YX

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

2YX

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

3YX

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
