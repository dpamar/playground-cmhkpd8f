# Fibonacci sequence

Fibonacci sequence _F_ is defined by
* F(1) = 1
* F(2) = 1
* F(n+2) = F(n+1) + F(n)

Hence, F(3) = 2, F(4) = 3, F(5) = 5, F(6) = 8, ...

Let's display the first N fibonacci numbers, N being provided by end user (> 1), as a list of comma separated values

# Let's start

* Memory: empty
* Cursor: first cell
* Input: a number

# Process

* First, generate comma (code 44), to print it when needed
* Then read integer in base 10 as a counter
* Init sequence with values 1 and 1
* Print 1,1 (first sequence items) and decrease counter by 2
* While counter is not null
  * Decrease counter
  * Print comma
  * Save as a copy the second sequence value
  * Add the current 2 sequence values to get the next
  * Move saved value as _first current value_, and computed value as _second current value_
  * Copy / Print new value
* loop

# Code
```
>++++[-<+++++++++++>]                 (44 = 4 x 11)
>,[>++++++[-<-------->]>+++++++++[-   read a number
<<<[->+>+<<]>>[-<<+>>]>]<<[-<+>],]     ** part 2 **
<<+++++.-----.+++++.-----             print 49;44;49 (1 comma 1) using comma char (faster)
>-->+>+                               decrease counter by 2 and start sequence with 2 ones
<<[                                   while counter is not null
  -                                   decrease counter
  <.                                  print comma
  >>>[->+>+<<]                        copy second value (mem : 1st 0 2nd 2nd)
  <[->>>+<<<]                         sum 1st and 2nd values to get 3rd (mem: 0 0 2nd 3rd)
  >>[-<<+>>]                          move 2nd value (mem: 2nd 0 0 3rd)
  >[->+<<<+>>]                        copy/move 3rd value (mem: 2nd 3rd 0 0 3rd; note: at least one 0 needed before a value to print it)
  >[>>>>++++++++++<<<<[->+>>+>-[<-]<[ print value as decimal number
  ->>+<<<<[->>>+<<<]>]<<]>+[-<+>]>>>[  ** part 2 **
  -]>[-<<<<+>>>>]<<<<]<[>++++++[<++++  ** part 3 **
  ++++>-]<-.[-]<]                      ** part 4 **
<<<<]                                 loop
```

# Minified version
```
>++++[-<+++++++++++>]>,[>++++++[-<-------->]>+++++++++[-<<<[->+>+<<]>>[-<<+
>>]>]<<[-<+>],]<<+++++.-----.+++++.----->-->+>+<<[-<.>>>[->+>+<<]<[->>>+<<<
]>>[-<<+>>]>[->+<<<+>>]>[>>>>++++++++++<<<<[->+>>+>-[<-]<[->>+<<<<[->>>+<<<
]>]<<]>+[-<+>]>>>[-]>[-<<<<+>>>>]<<<<]<[>++++++[<++++++++>-]<-.[-]<]<<<<]
```

# Final state

* Memory: 44, 0, F(N-1), F(N)
* Cursor: on second cell
* Input: read (empty)
* Output: all N first Fibonacci numbers (modulo 256)
