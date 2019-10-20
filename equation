BR main 
a: .BLOCK 2 
b: .BLOCK 2 
c: .BLOCK 2 
n: .BLOCK 2 
nclone: .WORD 0x0000 
aclone: .WORD 0x0000 
bclone: .WORD 0x0000 
NXn: .WORD 0x0000 ;value for n*n
AXnXn: .WORD 0x0000 ;value for a*n*n 
BXn: .WORD 0x0000 ;value for b*n
cntn: .WORD 0x0001 ;count the terms from 1 to 4
cntnc: .WORD 0x0000 
down: .WORD 0x0004 ;repeat the equasion loop 4 times
nsum: .WORD 0x0000 
sumX: .WORD 0x0000 
NXnmulti: .WORD 0x0000 
AXnXnmlt: .WORD 0x0000;value for a*cntn*cntn 
BXnmulti: .WORD 0x0000 ;value for b*cntn
msga: .ASCII "Enter a decimal value for a: \x00" 
msgb: .ASCII "Enter a decimal value for b: \x00" 
msgc: .ASCII "Enter a decimal value for c: \x00" 
msgn: .ASCII "Enter a decimal value for n: \x00" 
final: .ASCII "Term \x00" 
newline: .ASCII "\n\x00" 
charts: .ASCII ": \x00" 
           ;read the user's input:a , b ,c ,n 
main:      STRO msga, d 
           DECI a, d 
           STRO msgb, d 
           DECI b, d 
           STRO msgc, d 
           DECI c, d 
           STRO msgn, d 
           DECI n, d 
           STRO newline, d 
           BR exp 
  
exp:       LDA down, d 
           BREQ  CLONESN 
           SUBA 0x0001, i ;loop (exp)for calculating the value of the equation for all 4 terms
           STA down, d 
           BR   COPCNT  
     
COPCNT:    LDA cntnc, d 
           ADDA cntn, d 
           STA cntnc, d 
           LDA aclone, d ;i make clones for cntn,a and b because i need to muliplicate them
           ADDA a, d 
           STA aclone, d 
           LDA bclone, d 
           ADDA b, d 
           STA bclone, d 
           BR  nXnclp 
  
 nXnclp:   LDA cntnc,d 
           BREQ AxNxNc 
           SUBA 0x0001, i ;in this loop NXmulti retain the result of the multiplication between cntn and cntn then i substract 1 from cntnc until the result is 0 and then we add cntn to NXnmulti 
           STA cntnc, d    ;then cntnc is 0 and i change the memory location to AxNxNc
          
           LDA NXnmulti, d 
           ADDA cntn, d 
           STA NXnmulti, d 

           BR  nXnclp 
  
AxNxNc:    LDA aclone, d 
           BREQ  BxNclp 
           SUBA 0x0001, i ;use the variable AxNxNmlt to retain the result of the multiplication between NXnmulti and a ,then i substract 1 from aclone until the result is 0 and then we add NXnmulti to AxNxNmlt
           STA aclone, d  ;then aclone is 0 and i change the memory location to BxNclp

           LDA AXnXnmlt, d 
           ADDA NXnmulti, d 
           STA AXnXnmlt, d 

           BR AxNxNc 
  
  
BxNclp:  LDA bclone, d 
         BREQ sumcnt   ;use the variable BXnmulti to retain the result of the multiplication between and cntn ,then i substract 1 from bclone until the result is 0 and then we add cntn to BXnmulti
         SUBA 0x0001, i ;then bclone is 0 and i change the memory location to sumcnt
         STA bclone, d 
         LDA BXnmulti, d 
         ADDA cntn, d 
         STA BXnmulti, d
 
         BR  BxNclp 
  
sumcnt:  LDA sumX, d 
         ADDA AXnXnmlt, d 
         ADDA BXnmulti, d ;i added BXnmulti, AxNxNmlt and c I store the result from the accumulator in the sumX
         ADDA c, d 
         STA sumX, d 

         STRO final, d 
         DECO cntn, d 
         STRO charts, d 
         DECO sumX, d 
         STRO newline, d 

         LDA cntn, d 
         ADDA 0x0001, i ;update the result of cntn by adding 1
         STA cntn, d 

         LDA NXnmulti, d 
         SUBA NXnmulti, d ;update the result of NXnmulti(NXnmulti-NXnmulti) 
         STA NXnmulti, d 

         LDA sumX, d 
         SUBA sumX, d ;update the result of sumX(sumX-sumX)
         STA sumX, d 

         LDA AXnXnmlt, d 
         SUBA AXnXnmlt, d ;update the result of AXnXnmlt(AXnXnmlt-AXnXnmlt)
         STA AXnXnmlt, d 

         LDA BXnmulti, d 
         SUBA BXnmulti, d ;update the result of BXnmulti( BXnmulti- BXnmulti)
         STA BXnmulti, d 

         BR exp 
  
CLONESN: LDA nclone, d 
         ADDA n, d 
         STA nclone, d 
         LDA aclone, d ;make clones for n, a ,b used in multiplications
         ADDA a, d 
         STA aclone, d 
         LDA bclone, d 
         ADDA b, d 
         STA bclone, d 
         BR loopnXn 
  
loopnXn: LDA nclone, d 
         BREQ lpaXnXn
         SUBA 0x0001, i ;variable NXn to retain the result of the multiplication(n*n),then i substract 1 from nclone until the result is 0 and then I add n to NXn
         STA nclone, d ;nclone is 0,switch the memory location lpaXnXn
         LDA NXn, d 
         ADDA n, d 
         STA NXn, d 
         BR loopnXn
  
lpaXnXn: LDA aclone, d 
         BREQ loopbXn
         SUBA 0x0001, i ;variable AXnXn to retain the result of the multiplication(a*AXnXn),then i substract 1 from aclone until the result is 0 and then I add AXnXn to AXnXn
         STA aclone, d ;aclone is 0,switch the memory location loopbXn
         LDA AXnXn, d 
         ADDA NXn, d 
         STA AXnXn, d 
         BR lpaXnXn 
  
loopbXn: LDA bclone, d 
         BREQ sum 
         SUBA 0x0001, i ;variable BXn to retain the result of the multiplication(b*n),then i substract 1 from bclone until the result is 0 and then I add n to BXn
         STA bclone, d ;bclone is 0,switch the memory location sum
         LDA BXn, d 
         ADDA n, d 
         STA BXn, d 
         BR loopbXn
  
sum:     LDA nsum, d 
         ADDA AXnXn, d 
         ADDA BXn, d ;calculate the equation for the n term,then store in nsum
         ADDA c, d 
         STA nsum, d 
         BR finished 

finished:STRO newline, d 
         STRO final, d ;output the final message for n and nsum
         DECO n, d 
         STRO charts, d 
         DECO nsum, d ;change the memory location to end, stops the execution
         BR end ; 
  
end: STOP 
.END 
