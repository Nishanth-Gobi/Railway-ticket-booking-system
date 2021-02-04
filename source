org 100h

include 'emu8086.inc'

.data
  
m0 dw 10,13,10,13,"*** Welcome to Railway Ticket Booking Coimbatore*** $"
m1 dw 10,13,10,13,"1) User",10,13,10,13,"2) Admin $"
m2 dw 10,13,10,13,"1) Bangalore",10,13,10,13,"2) Chennai",10,13,10,13,"3) Cochin",10,13,10,13,"4) Palakad $"
m3 dw 10,13,10,13,"Enter your choice: $"
m4 dw 10,13,10,13,"Available Destinations: $"
m5 dw 10,13,10,13,"Invalid choice! Please re-enter: $"
m6 dw 10,13,10,13,"Please pay: $"
m7 dw 10,13,10,13,"Enter  $"
m8 dw 10,13,10,13,"All tickets Booked! $"
m9 dw 10,13,10,13,"Tickets available $"
m10 dw 10,13,10,13,"Confirm booking?",10,13,10,13,"Enter 1 to confirm (or) 0 to Exit $"
m11 dw 10,13,10,13,"Your unique user ID is: $"
m12 dw 10,13,10,13,"Ticket Booked, enjoy your journey $"

m13 dw 10,13,10,13,"Initial ticket count: $"
m14 dw 10,13,10,13,"New ticket count: $"
m15 dw 10,13,10,13,"1)Add tickets",10,13,10,13,"2)Ckeck unique key",10,13,10,13,"3)End Service $"
m16 dw 10,13,10,13,"Select station: $"
m17 dw 10,13,10,13,"Base value of Unique key: $"
m18 dw 10,13,10,13,"Incrementation value for the keys: $"
m19 dw 10,13,10,13,"Enter additional ticket count (with '0' as prefix): $"
m20 dw 10,13,10,13,"Ticket count updated $"

f dw 100,45,75,60      ;ticket costs array
t dw 010,010,010,010       ;no. of tickets for respective trains
n db 4                 ;no. of stations that has trains from coimbatore
k dw 11                ;unique user ID's base value
i dw 7                 ;incrementation value for user ID
d dw 0                 ;destination value


.code

mov cx, k
       
start:

call CLEAR_SCREEN

;UI Home

mov ah, 09
lea dx, m0
int 21h

; User/ Admin

mov ah, 09
lea dx, m1
int 21h

mov ah, 09
lea dx, m3
int 21h

l0:
    mov ah, 01
    int 21h
    mov ah, 0
    sub ax, 48

    cmp ax, 01
    jne I1
        jmp I3 
    I1:
    
    cmp ax, 02
    jne I2
        jmp I4
    I2:
    
    mov ah, 09
    lea dx, m5
    int 21h
    
    loop l0

; User portal

I3:
call CLEAR_SCREEN
 
;Getting the destination as user input and it's validation

mov ah, 09
lea dx, m4
int 21h
         
mov ah, 09
lea dx, m2
int 21h

mov ah, 09
lea dx, m3
int 21h

l1:
    mov ah, 01
    int 21h
    mov ah, 0
    sub ax, 48
    cmp al, n         ; option <= no. of available stations
    jle j1
        jmp j2
    
    j1:
    cmp al, 0          ; option > 0
    jg j3           
        j2:
        mov ah, 09
        lea dx, m5
        int 21h
    
        loop l1     
    
j3:
         
dec ax
mov bx, 02
mul bx         
mov d, ax

call CLEAR_SCREEN

;check for tickets

mov si, d

cmp t[si], 0
jg j4
    mov ah, 09
    mov dx, m8
    int 21h
    jmp start 
j4:

mov bx, t[si]
dec bx
mov t[si], bx
mov ah, 09
lea dx, m9
int 21h    

;Confirmation 

mov ah, 09
lea dx, m10
int 21h

mov ah, 01
int 21h

sub ax, 48

cmp al, 01
jne start

;payment

mov si, d

mov ah, 09
lea dx, m6
int 21h
 
mov ax, f[si]

call PRINT_NUM
PRINTN 'Rs/-'

;print unique key for user

mov ah, 09
lea dx, m11
int 21h                                                                            

mov ax, cx
call PRINT_NUM
add cx, i

jmp end

;Admin portal

I4:

mov ah, 09
lea dx, m15
int 21h

mov ah, 09
lea dx, m3
int 21h

l2:
    mov ah, 01
    int 21h
    mov ah, 0
    sub ax, 48
    
    cmp ax, 1
    je j5
    
    cmp ax, 2
    je j6
    
    cmp ax, 3
    je j7
    
    mov ah, 09
    lea dx, m5
    int 21h
    
    loop l2

;add tickets 

j5:

call CLEAR_SCREEN
    
mov ah, 09
lea dx, m16
int 21h

mov ah, 09
lea dx, m2
int 21h

mov ah, 09
lea dx, m3
int 21h

mov ah, 01
int 21h

mov ah, 0
sub ax, 48

mov si, ax
dec si

mov ax, si
mov bx, 02
mul bx 
mov si, ax

;display initial count

mov ah, 09
lea dx, m13
int 21h

mov ax, t[si]
call PRINT_NUM

;get additional count

mov ah, 09
lea dx, m19
int 21h

mov ah, 01
int 21h

call SCAN_NUM

;update count

mov ax, t[si]
add ax, cx
mov t[si], ax

mov ah, 09
lea dx, m20
int 21h

;display updated count

mov ah, 09
lea dx, m14
int 21h

mov ax, t[si]
call PRINT_NUM

jmp end

;Display Key details

j6:

call CLEAR_SCREEN

mov ah, 09
lea dx, m17
int 21h

mov ax, k
call PRINT_NUM

mov ah, 09
lea dx, m18
int 21h

mov ax, i
call PRINT_NUM

jmp end

;Terminate

j7:

jmp terminate

end:

jmp start

terminate:

ret

DEFINE_PRINT_NUM
DEFINE_PRINT_NUM_UNS
DEFINE_CLEAR_SCREEN
DEFINE_SCAN_NUM

end
