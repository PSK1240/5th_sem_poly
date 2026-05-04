Thank me later ;)

DATA SEGMENT
    NUMBERS DB 12H, 33H, 24H, 57H, 08H, 09H, 10H, 11H, 44H, 65H ; 10 Numbers
    EVEN_COUNT DB 00H
    ODD_COUNT DB 00H
DATA ENDS

CODE SEGMENT
    ASSUME CS:CODE, DS:DATA
START:
    MOV AX, DATA
    MOV DS, AX          ; Initialize Data Segment
    
    LEA SI, NUMBERS     ; Load address of the first number
    MOV CX, 0AH         ; Set counter to 10 (0A in hex)
    MOV BL, 00H         ; BL will store Even count
    MOV DL, 00H         ; DL will store Odd count

CHECK_NEXT:
    MOV AL, [SI]        ; Move current number into AL
    TEST AL, 01H        ; Logical AND with 0000 0001 (Checks LSB)
    JZ IS_EVEN          ; If Zero Flag is set (result is 0), it's even

    INC DL              ; Otherwise, it's odd. Increment Odd count.
    JMP SKIP

IS_EVEN:
    INC BL              ; Increment Even count

SKIP:
    INC SI              ; Point to next number
    LOOP CHECK_NEXT     ; Decrement CX and repeat until CX=0

    MOV EVEN_COUNT, BL  ; Store final even count in memory
    MOV ODD_COUNT, DL   ; Store final odd count in memory

    MOV AH, 4CH         ; Terminate program
    INT 21H
CODE ENDS
END START

