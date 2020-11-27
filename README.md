# pushbutton
MID TERM TASK


#include<p18F4550.inc>

loop_cnt1	set	0x00
loop_cnt2	set	0x01

			org 0x00
			goto start
			org 0x08
			retfie
			org 0x18
			retfie

;_____________________________________________________________________
;						DELAY
;_____________________________________________________________________

dup_nop		macro	kk
			variable i 
i = 0
			while i < kk 
			nop
i += 1
			endw 
			endm


D10MS			MOVLW	D'80'
				MOVWF	loop_cnt2, A
AGAIN1			MOVLW	D'270'
				MOVWF	loop_cnt1, A
AGAIN2			dup_nop	D'17'
				DECFSZ	loop_cnt1, F,  A
				BRA		AGAIN2
				DECFSZ	loop_cnt2, F, A
				BRA		AGAIN1
		
				NOP
				RETURN

;______________________________________________________________________
;						REGISTER LDC AND SET DATA 
;______________________________________________________________________

CMD				BCF		PORTC, 4, A				; 	REGISTER COMMAND FOR LCD
				BCF		PORTC, 5, A
				BSF		PORTC, 6, A
				CALL	D10MS
				BCF		PORTC, 6, A	
				RETURN

SETDATA			BSF		PORTC, 4, A				; SET THE DATA CONFIGURATION
				BCF		PORTC, 5, A
				BSF		PORTC, 6, A
				CALL	D10MS
				BCF		PORTC, 6, A	
				RETURN

;_______________________________________________________________________
;			DISPLAY	MUHD FAUZI 
;_______________________________________________________________________			
		
myname			MOVLW	D'77'				;  M
				MOVWF	PORTD, A
				CALL	SETDATA

				MOVLW	D'85'				;  U
				MOVWF	PORTD, A
				CALL	SETDATA

				MOVLW	D'72'				;  H
				MOVWF	PORTD, A
				CALL	SETDATA

				MOVLW	D'68'				;  D
				MOVWF	PORTD, A
				CALL	SETDATA

				MOVLW	D'32'				; SPACE
				MOVWF	PORTD, A
				CALL	SETDATA

				MOVLW	D'70'				;  F
				MOVWF	PORTD, A
				CALL	SETDATA

				MOVLW	D'65'				;  A
				MOVWF	PORTD, A
				CALL	SETDATA

				MOVLW	D'85'				;  U
				MOVWF	PORTD, A
				CALL	SETDATA

				MOVLW	D'90'				;  Z
				MOVWF	PORTD, A
				CALL	SETDATA

				MOVLW	D'73'				;  I
				MOVWF	PORTD, A
				CALL	SETDATA

				MOVLW	D'32'				;  SPACE
				MOVWF	PORTD, A
				CALL	SETDATA

				MOVLW	0X01
				MOVWF	PORTD, A
				CALL 	CMD

				BRA		checki

;_______________________________________________________________________________
;					SUBROUTINE DISPLAY D E   9 6 5 3 4 
;

id				MOVLW	D'68'				;  D
				MOVWF	PORTD, A
				CALL	SETDATA

				MOVLW	D'69'				;  E
				MOVWF	PORTD, A
				CALL	SETDATA

				MOVLW	D'57'				; 9
				MOVWF	PORTD, A
				CALL	SETDATA

				MOVLW	D'54'				;  6
				MOVWF	PORTD, A
				CALL	SETDATA

				MOVLW	D'53'				;  5
				MOVWF	PORTD, A
				CALL	SETDATA

				MOVLW	D'53'				;  3
				MOVWF	PORTD, A
				CALL	SETDATA

				MOVLW	D'52'				;  4
				MOVWF	PORTD, A
				CALL	SETDATA

				MOVLW	D'32'				;  SPACECING
				MOVWF	PORTD, A
				CALL	SETDATA

				MOVLW	0X01
				MOVWF	PORTD, A
				CALL 	CMD

				BRA		checko

;_____________________________________________________________________
;					SUBROUTINE FOR	KEYPAD CONFIGURATION
;_____________________________________________________________________

NO1			MOVLW	0XC0				; DISPLAY 1
				MOVWF	PORTD, A
				CALL 	CMD
				MOVLW	D'49'
				MOVWF	PORTD, A
				CALL	SETDATA
				BRA		checki

NO2			MOVLW	0XC0				; DISPLAY 2
				MOVWF	PORTD, A
				CALL 	CMD
				MOVLW	D'50'
				MOVWF	PORTD, A
				CALL	SETDATA
				BRA		checki
				
NO3			MOVLW	0XC0				; DISPLAY 3
				MOVWF	PORTD, A
				CALL 	CMD
				MOVLW	D'51'
				MOVWF	PORTD, A
				CALL	SETDATA
				BRA		checki

NO4			MOVLW	0XC0				; DISPLAY 4
				MOVWF	PORTD, A
				CALL 	CMD
				MOVLW	D'52'
				MOVWF	PORTD, A
				CALL	SETDATA
				BRA		checki

NO5			MOVLW	0XC0				; DISPLAY 5
				MOVWF	PORTD, A
				CALL 	CMD
				MOVLW	D'53'
				MOVWF	PORTD, A
				CALL	SETDATA
				BRA		checki
				
NO6			MOVLW	0XC0				; DISPLAY 6
				MOVWF	PORTD, A
				CALL 	CMD
				MOVLW	D'54'
				MOVWF	PORTD, A
				CALL	SETDATA
				BRA		checki

NO7			MOVLW	0XC0				; DISPLAY 7
				MOVWF	PORTD, A
				CALL 	CMD
				MOVLW	D'55'
				MOVWF	PORTD, A
				CALL	SETDATA
				BRA		checki

NO8			MOVLW	0XC0				; DISPLAY 8
				MOVWF	PORTD, A
				CALL 	CMD
				MOVLW	D'56'
				MOVWF	PORTD, A
				CALL	SETDATA
				BRA		checki
				
NO9			MOVLW	0XC0				; DISPLAY 9
				MOVWF	PORTD, A
				CALL 	CMD
				MOVLW	D'57'
				MOVWF	PORTD, A
				CALL	SETDATA
				BRA		checki

SHOWN			MOVLW	0XC0				; DISPLAY *
				MOVWF	PORTD, A
				CALL 	CMD
				MOVLW	D'42'
				MOVWF	PORTD, A
				CALL	SETDATA
				BRA		checki

NO0			MOVLW	0XC0				; DISPLAY 0
				MOVWF	PORTD, A
				CALL 	CMD
				MOVLW	D'48'
				MOVWF	PORTD, A
				CALL	SETDATA
				BRA		checki
				
SHOW#			MOVLW	0XC0				; DISPLAY #
				MOVWF	PORTD, A
				CALL 	CMD
				MOVLW	D'35'
				MOVWF	PORTD, A
				CALL	SETDATA
				BRA		checki

				

;____________________________________________________________________________
;					MAIN PROGRAM
;___________________________________________________________________________
			
start		CLRF	TRISC, A				; CONFIGURE INPUT AND OUTPUT
			CLRF 	TRISD, A
			SETF	TRISB, A
			BCF		TRISB, 4, A	
			BCF		TRISB, 5, A	
			BCF		TRISB, 6, A	
			BCF		TRISB, 7, A	
			SETF	TRISA, A
			

			MOVLW	0X38					; CONFIGURE 2 LINES AND 5X7 MATRIX
			MOVWF	PORTD, A
			CALL	CMD
			
			MOVLW	0X0E					; DISPLAY ON, CURSOR BLINKING
			MOVWF	PORTD, A
			CALL 	CMD

			MOVLW	0X01					; CLEAR DISPLAY SCREEN
			MOVWF	PORTD, A
			CALL 	CMD

			MOVLW	0X80					; FORCE CURSOR TO BEGINNING TO FIRST LINE
			MOVWF	PORTD, A
			CALL	CMD


checki		BTFSC	PORTB, 0, A
			BRA		myname
			CLRF	PORTD, A
checko		BTFSC	PORTB, 1, A
			BRA		id
			CLRF	PORTD, A

KEYPAD1		CLRF	PORTB, A
			BSF		PORTB, 4, A
			BTFSC	PORTA, 4, A	
			BRA		NO1
			CLRF	PORTD, A

KEYPAD2		CLRF	PORTB, A
			BSF		PORTB, 4, A
			BTFSC	PORTB, 2, A	
			BRA		NO2
			CLRF	PORTD, A

KEYPAD3		CLRF	PORTB, A
			BSF		PORTB, 4, A
			BTFSC	PORTB, 3, A	
			BRA		NO3
			CLRF	PORTD, A

KEYPAD4		CLRF	PORTB, A
			BSF		PORTB, 5, A
			BTFSC	PORTA, 4, A	
			BRA		NO4
			CLRF	PORTD, A

KEYPAD5		CLRF	PORTB, A
			BSF		PORTB, 5, A
			BTFSC	PORTB, 2, A	
			BRA		NO5
			CLRF	PORTD, A

KEYPAD6		CLRF	PORTB, A
			BSF		PORTB, 5, A
			BTFSC	PORTB, 3, A	
			BRA		NO6
			CLRF	PORTD, A

KEYPAD7		CLRF	PORTB, A
			BSF		PORTB, 6, A
			BTFSC	PORTA, 4, A	
			BRA		NO7
			CLRF	PORTD, A

KEYPAD8		CLRF	PORTB, A
			BSF		PORTB, 6, A
			BTFSC	PORTB, 2, A	
			BRA		NO8
			CLRF	PORTD, A

KEYPAD9		CLRF	PORTB, A
			BSF		PORTB, 6, A
			BTFSC	PORTB, 3, A	
			BRA		NO9
			CLRF	PORTD, A

KEYPADN		CLRF	PORTB, A
			BSF		PORTB, 7, A
			BTFSC	PORTA, 4, A	
			BRA		SHOWN
			CLRF	PORTD, A

KEYPAD0		CLRF	PORTB, A
			BSF		PORTB, 7, A
			BTFSC	PORTB, 2, A	
			BRA		NO0
			CLRF	PORTD, A

KEYPAD#		CLRF	PORTB, A
			BSF		PORTB, 7, A
			BTFSC	PORTB, 3, A	
			BRA		SHOW#
			CLRF	PORTD, A

	
	
			NOP
			END
