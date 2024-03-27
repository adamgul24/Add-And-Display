section .data
    msg1 db 'Value of the first Integer Number is %d', 10, 0
    msg2 db 'Memory location of the first Integer Number is %p', 10, 0
    msg3 db 'Value of the second Integer Number is %d', 10, 0
    msg4 db 'Memory location of the second Integer Number is %p', 10, 0
    msg5 db 'Sum of the two numbers is %d', 10, 0
    msg6 db 'All information: First number: %d, Location: %p; Second number: %d, Location: %p; Sum: %d', 10, 0

    firstNum dd 25 ; First integer
    secondNum dd 13 ; Second integer
    sum dd 0 ; Placeholder for the sum

section .text
    extern printf
    global main

main:
    push ebp
    mov ebp, esp

    ; Print first number
    push dword [firstNum]
    push msg1
    call printf
    add esp, 8

    ; Print memory location of first number
    push firstNum
    push msg2
    call printf
    add esp, 8

    ; Print second number
    push dword [secondNum]
    push msg3
    call printf
    add esp, 8

    ; Print memory location of second number
    push secondNum
    push msg4
    call printf
    add esp, 8

    ; Calculate sum
    mov eax, [firstNum]
    add eax, [secondNum]
    mov [sum], eax

    ; Print sum
    push dword [sum]
    push msg5
    call printf
    add esp, 8

    ; Print all information in one line
    push dword [sum]              ; Push the sum
    push dword [secondNum]        ; Push the location of the second number
    push dword [secondNum]        ; Push the value of the second number
    push dword [firstNum]         ; Push the location of the first number
    push dword [firstNum]         ; Push the value of the first number
    lea eax, [msg6]
    push eax
    call printf
    add esp, 24

    ; Exit program
    mov esp, ebp
    pop ebp
    ret
