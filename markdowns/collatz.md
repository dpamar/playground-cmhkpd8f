# Collatz sequence

Collatz sequence is defined by 
* C(0) is a parameter
* C(n+1) = 
  * C(n)/2 if C(n) is even
  * 3 * C(n) + 1 if odd

Though it has not been proved yet, the sequence is supposed to end up with ..., 4, 2, 1 and then loop 4, 2, 1, ...

Let's read an integer N and write the full Collatz sequence (comma separated) until 1 is reached

# Let's start

* Memory: empty
* Cursor: first cell
* Input: a decimal number N

# Process

* First, generate comma (code 44), to print it when needed
* Then, read integer N
* Decrease N by 1
* while N is not null (i.e. original N is not 1)
  * Increase N (regenerate it)
  * Copy / print N and print comma
  * Try to divide N by 2
    * Decrease by N
    * Set else flag
    * If N not null : decrease by 2, clear else flag, update quotient
    * Loop until N is not null
  * Then, according to else flag
    * unset : N was even, and quotient N/2 is our next value
    * set : N was odd, N = 2k+1, quotient is k and next value is 3N+1 = 6k+4
      * In this case, multiply k by 3 : 3k
      * Then add 2: 3k + 2
      * And multiply by 2 : 6k+4
  * in all cases, we have our next value
  * copy as new N and decrease by 1 (we loop on N-1)
* Loop
* Print 1 (the final element)

# Code
```
>++++[-<+++++++++++>]                  ( 44 = 4 x 11)
>,[>++++++[-<-------->]>+++++++++[-    read an integer
<<<[->+>+<<]>>[-<<+>>]>]<<[-<+>],]      ** part 2 **
<-[                                    while N is not 1
  +                                    regenerate N
  [->+>+<<]>[-<+>]>[>>>>++++++++++<<   copy / print N
  <<[->+>>+>-[<-]<[->>+<<<<[->>>+<<<    ** part 2 **
  ]>]<<]>+[-<+>]>>>[-]>[-<<<<+>>>>]<    ** part 3 **
  <<<]<[>++++++[<++++++++>-]<-.[-]<]    ** part 4 **
  <<.>                                 print comma
  [->+<[->->>+<<]                      try to divide by 2 with an else flag
  >[-                                  N is null and flag is set: N is odd
    >>[-<+++>]<                        compute 3k
    ++[->++<]                          then 3k plus 2 and finally 6k plus 4 which is 3N plus 1
  ]<<]                                 division loop
  >>>[-<<<+>>>]<<<-                    move new N and decrease by one
]                                      loop
<+++++.                                print '1' (code 49, 44 plus 5)
```

# Minified version
```
>++++[-<+++++++++++>]>,[>++++++[-<-------->]>+++++++++[-<<<[
->+>+<<]>>[-<<+>>]>]<<[-<+>],]<-[+[->+>+<<]>[-<+>]>[>>>>++++
++++++<<<<[->+>>+>-[<-]<[->>+<<<<[->>>+<<<]>]<<]>+[-<+>]>>>[
-]>[-<<<<+>>>>]<<<<]<[>++++++[<++++++++>-]<-.[-]<]<<.>[->+<[
->->>+<<]>[->>[-<+++>]<++[->++<]]<<]>>>[-<<<+>>>]<<<-]<+++++.
```

# Final state

* Memory: 49, 0, 0, 0
* Cursor: first cell
* Input: read (empty)
* Output: Collatz sequence, start from N, comma separated

_Note_: again, this is a valid sequence, modulo 256. And it does not only means that input needs to be less than 256, but that any item within sequence must be too.

Ex:
* any odd number from 87 leads to a value greater than 256
* any even number that doubles an odd value from 87 (i.e. all the 4n+2 with n >= 44) fails as well
* ...
* even worse : 85 is odd, next value is 256 = 0 in our model, but 0 is an unexpected value ==> it fails and displays comma in an infinite loop...


