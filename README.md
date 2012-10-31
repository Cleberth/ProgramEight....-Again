ProgramEight....-Again
======================

.... *Sigh* ....



Br main

arg1: .Equate 0 ;local variable #2d
arg2: .Equate -2 ;local variable #2d
product: .Equate-4 ;local variable #2d
frame: .Equate 6 ;frame size of #arg1 #agr2  #product

num1: .Equate 2 ;local variable #2d
num2: .Equate 0 ;local variable #2d
numframe: .Equate 6 ;frame size of #num1 #num2

start: NOP0
STRO testST,d
LDA arg1,d 
BREQ done
RORA
BRC odd
BR even

odd: NOP0
STRO testOD,d
LDA product,d
ADDA arg2,d 
STA product,d
BR divimult

even: NOP0
STRO testEV,d
BR divimult

divimult: NOP0
STRO testDM,d 
LDA arg1,d
ASRA
STA arg1,d
LDA arg2,d
ASLA
STA arg2,d
BR start

done: NOP0
STRO testDN,d
RET0

main: NOP0
SUBSP frame,i ;allocating #product #num2 #num1 
LDA 0,i
STA product,d
STRO prompt,d
DECI arg1,d
LDA arg1,d
STA num1,d
DECI arg2,d
LDA arg2,d
STA num2,d
LDA arg1,d
SUBSP numframe,i ;allocating #product #arg2 #arg1 
CALL start 
ADDSP numframe,i ;deallocating #arg1 #arg2 #product 
DECO num1,d
CHARO '*',i
DECO num2,d
CHARO '=',i
DECO product,d
ADDSP frame,i ;deallocating #num1 #num2 #product 

STOP
prompt: .ASCII "Input Two Numbers: \x00"
testST: .ASCII "Starting...\n\x00"
testOD: .ASCII "Odd...\n\x00"
testEV: .ASCII "Even...\n\x00"
testDM: .ASCII "DiviMult...\n\x00"
testDN: .ASCII "Done...\n\x00"
.END