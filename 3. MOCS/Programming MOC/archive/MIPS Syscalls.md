---
created: 2024-04-20
type: Programming Note
programming language: "[[MIPS Assembly MOC]]"
related: 
completed: false
updated: 2024-05-27T13:29
---
---

>[!abstract] Index
>1. [[#Introduction]]
>2. [[#Print Syscalls]]
>3. [[#Read Syscalls]]
>4. [[#Exit Syscall]]

>[!abstract] Related
>1. [[MIPS Assembly MOC]]

---
## Introduction

>[!tip] Definition
>A system call (syscall) in MIPS assembly is a way for a program to request a service from the operating system. 
>- The syscall instruction is used, with the type of call specified in the `$v0` register. Arguments for the syscall are placed in registers `$a0`, `$a1`, `$a2`, and `$a3` as needed. Results are usually returned in `$v0` and sometimes `$v1`.

We can categorize the system calls (syscalls) in MIPS assembly in 3 category:

1. **Print Syscalls**: These syscalls are used to output data. They can print different types of data including integers, floating-point numbers, and strings. The data to be printed is typically passed in a specific register (like `$a0` or `$f12`).

2. **Read Syscalls**: These syscalls are used to read input data from the user. They can read different types of data including integers, floating-point numbers, and strings. The read data is typically returned in a specific register (like `$v0` or `$f0`), or stored in a buffer whose address is passed in a specific register (like `$a0`).
 
3. **Exit Syscall**: This syscall is used to terminate the program. It doesn't require any arguments and doesn't return any result.
 
>[!note]
>Remember, these are just some of the basic syscalls. MIPS provides many other syscalls for various purposes, such as file I/O, memory allocation, and process control.

---
## Print Syscalls

Print syscalls are used to output data. They can print different types of data including integers, floating-point numbers, and strings. The data to be printed is typically passed in a specific register (like `$a0` or `$f12`).

>[!info] Print integer
>
>```javascript
>li $v0, 1
>move $a0, $t0  # Assume $t0 contains the integer to print
>syscall
>```

>[!info] Print float
>```javascript
>li $v0, 2
>l.s $f12, float_value  # Assume float_value is a .float directive
>syscall
>```

>[!info] Print string
>```javascript
>li $v0, 4
>la $a0, string  # Assume string is a null-terminated string
>syscall
>```

---
## Read Syscalls

Read syscalls are used to read input data from the user. They can read different types of data including integers, floating-point numbers, and strings. The read data is typically returned in a specific register (like `$v0` or `$f0`), or stored in a buffer whose address is passed in a specific register (like `$a0`).

>[!info] Read integer
>```javascript
>li $v0, 5
>syscall
>move $t0, $v0  # $t0 now contains the read integer
>```

>[!info] Read float
>```javascript
>li $v0, 6
>syscall
>mov.s $f12, $f0  # $f12 now contains the read float
>```

>[!info] Read string
>```javascript
>li $v0, 8
>la $a0, buffer  # Assume buffer is a .space directive
>li $a1, 100     # Read up to 100 characters
>syscall
>```

---
## Exit Syscall

The exit syscall is used to terminate the program. It doesn't require any arguments and doesn't return any result.

>[!info] Exit
>```javascript
>li $v0, 10
>syscall
>```

---