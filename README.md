# SKILL2_MPMC_BHARATH

## AIM

Generate a 1 millisecond delay using Timer 0 in Mode 1 (16-bit timer mode) of the 8051 microcontroller.

## APPARATUS REQUIRED

Personal computer with Keil software

## ALGORITHM

1. Load Timer0 mode = Mode1 (16-bit) into TMOD.
2. Load TH0 with 0xFC and TL0 with 0x18.
3. Clear TF0, start Timer0 (TR0 = 1).
4. Wait (poll) until TF0 becomes 1 (timer overflow).
5. Stop Timer0, clear TF0.
6. Return from subroutine (or repeat as needed).

## PROGRAME

```
ORG 0H
MOV TMOD, #01H    
MOV P1, #00H      
START:
    MOV P1, #0FFH  
    ACALL DELAY_1MS
    MOV P1, #00H   
    ACALL DELAY_1MS
    SJMP START     
DELAY_1MS:
    CLR TR0        
    CLR TF0        
    MOV TH0, #0FCH 
    MOV TL0, #018H 
    SETB TR0       
WAIT:
    JNB TF0, WAIT  
    CLR TR0        
    CLR TF0        
    RET
END
```

## OUTPUT

<img width="819" height="682" alt="Screenshot 2025-10-13 201300" src="https://github.com/user-attachments/assets/446ac41d-9175-4a2e-89a8-0bacbc25838e" />

## RESULT

Thus, a 1 ms delay was generated and executed successfully using Timer 0 in Mode 1 of the 8051 microcontroller.
