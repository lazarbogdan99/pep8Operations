         BR      main      
a: .BLOCK 2 ;variable which shows the start point of counting up/down

main: STRO       ask, d;we output the string then the user has to input
      DECI       a, d;we output the user's number and if the value is 0
      DECO       a, d;we switch the program counter to memory location zero 
      BREQ       zero

pos: BRLT   neg;if the number is negative we switch the program counter to meomry location neg(negative)
     STRO   newline,d;and then we use this string to move to the next line   
     LDA    a, d;we update the value
     SUBA   0x0001,i;we update the value
     STA    a, d;we update the value
     DECO   a, d;output the current value 
     BREQ   finish;if the value in the acumulator reaches the value of 0 I switch  the program counter to the memory location zero   
     BR     pos;reapeat the loop


neg: STRO   newline, d ;string to move to the nest line   
     LDA    a, d;we update the value
     ADDA   0x0001, i;we update the value
     STA    a, d;we update the value
     DECO   a, d;output the current value 
     BREQ   finish;if the value in the acumulator reaches the value of 0 I switch  the program counter to the memory location zero   
     BR     neg;reapeat the loop
          
zero:    BR         finish;it ends the program by swithing the program counter to memory location
        


newline: .ASCII "\n\x00" 
ask: .ASCII "Enter a decimal number: \x00"      
      

finish:STOP
      .END
