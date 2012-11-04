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










//////// Second Attempt from Scratch//////
BR main

;///Addresses for Main (Caller)///
num1: .Equate -6
num2: .Equate -4
pro: .Equate -2
fra: .Equate 6

;///Adresses for Multi (Callee)///
argu1: .Equate 2 ;formal argument #2d
argu2: .Equate 4 ;formal argument #2d
produ: .Equate 6 ;formal argument #2d

;/////multi Stuff/////
arg1: .Equate 0 ;local variable #2d
arg2: .Equate 2 ;local variable #2d
prod: .Equate 4 ;local variable #2d
frame: .Equate 6 ;frame size of #arg1 #arg2 #prod
;//multi starts//
multi: NOP0 
STRO testMF,d
LDA argu1,s
STA arg1,s
LDA argu2,s 
STA arg2,s
LDA 0,i
STA produ,s
DECO arg1,s
CHARO '\n',i
DECO arg2,s
CHARO '\n',i
BR start

start: NOP0
STRO testST,d
DECO arg1,s
CHARO '\n',i
DECO arg2,s
CHARO '\n',i
DECO prod,s
CHARO'\n',i
LDA arg1,s
BREQ done 
RORA
BRC odd
BR even

odd: NOP0
STRO testOD,d
LDA produ,s
ADDA arg2,s
STA prod,s
DECO arg1,s
CHARO '\n',i
DECO arg2,s
CHARO '\n',i
DECO prod,s
CHARO'\n',i
BR divimult

even: NOP0
STRO testEV,d
DECO arg1,s
CHARO '\n',i
DECO arg2,s
CHARO '\n',i
DECO prod,s
CHARO'\n',i
BR divimult

divimult: NOP0
STRO testDM,d
LDA arg1,s
ASRA
STA arg1,s
LDA arg2,s
ASLA
STA arg2,s
DECO arg1,s
CHARO '\n',i
DECO arg2,s
CHARO '\n',i
DECO prod,s
CHARO'\n',i
BR done 

done: NOP0
STRO testDN,d
LDA arg2,s
ASRA
STA arg2,s
LDA prod,s
ADDA arg2,s
STA produ,s
DECO arg1,s
CHARO '\n',i
DECO arg2,s
CHARO '\n',i
DECO prod,s
CHARO'\n',i
LDA arg1,d
;BRGT start
BR DONE



;/////main stuff/////
n1: .Equate 0 ;local vaiable #2d
n2: .Equate 2 ;local variable #2d
f: .Equate 4 ;frame size of #n1 #n2 
;//main starts//
main: NOP0
SUBSP f,i ;allocating #n2 #n1
STRO prompt,d
DECI n1,s
DECI n2,s
LDA n1,s
STA num1,s
LDA n2,s
STA num2,s
SUBSP frame,i ;allocating #prod #arg2 #arg1
CALL multi 
ADDSP frame,i ;deallocating #arg1 #arg2 #prod
DONE: NOP0
DECO n1,s
CHARO '*',i
DECO n2,s
CHARO '=',i
DECO produ,s
ADDSP f,i ;deallocating #n1 #n2

;DONE: NOP0

STOP
prompt: .ASCII "Input Two Numbers: \x00" 
testMF: .ASCII "Multi...\n\x00"
testST: .ASCII "Starting...\n\x00"
testOD: .ASCII "Odd...\n\x00"
testEV: .ASCII "Even...\n\x00"
testDM: .ASCII "DiviMult...\n\x00"
testDN: .ASCII "Done...\n\x00"
.END