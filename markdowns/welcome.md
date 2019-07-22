# Welcome!

Welcome to this new playground about the BF language. Make sure you already read 
* [Getting started with BrainFuck](https://tech.io/playgrounds/50426/getting-started-with-brainfuck/welcome)
* [BrainFuck part 2 - Working with arrays](https://tech.io/playgrounds/50443/brainfuck-part-2---working-with-arrays/welcome)
* [BrainFuck part 3 - Write a BF interpreter in BF](https://www.codingame.com/playgrounds/50446/brainfuck-part-3---write-a-bf-interpreter-in-bf/welcome)
* [BrainFuck part 4 - Advanced maths](https://www.codingame.com/playgrounds/50446/brainfuck-part-3---write-a-bf-interpreter-in-bf/welcome)

playgrounds if you didn't already !

The goal of this playground is to play with maths, again, more exactly with some famous math sequences.

Let's start with the list of prime numbers !

A prime number is a number that allows only 2 distinct divisors: 1 and itself. First prime numbers are 2, 3, 5, 7, 11 ...

Computing all prime numbers up to a limit can be implemented using a sieve :
* Generate an array of all integers from 2 up to the limit
* Go to the first non-null item in the array
* This number N is prime
* Then, reset array items every N cells starting from this one

Example:
* 2 is prime
  * remove 4, 6, 8, ... and all multiple of 2
* 3 is a prime
  * remove 6 (again), 9, 12, ... and all multiples of 3
* 4 is null (reset by 2)
* 5 is prime
  * remove 10 (again), 15 (again), 20 (again), 25, ...
* 6 is null
* 7 is prime
* ...

Let's print all prime numbers (<255 of course), in a comma separated list

# Let's start

* Memory: empty
* Cursor: on first cell
* Input: a decimal number

# Process

* First, generate comma (code 44), to print it when needed
* Generate an array from 2 to max value
  * Values can be null, it's a 2-cell-long array
  * _Note : we will use a structure [value, flag] instead of [flag, value], code is a bit shorter_a
  * method
    * decrease empty cell by one to have max value
    * set flag on the right to 1
    * while value cell is not null, copy after the flag, then set the flag and repeat
  * This generates a set of cells [value, flag], from 255 to 1 : remove 2 extra cells (one array item) at the end
  * _Note: the array is reversed... but it's not a big deal_
* Go to last array item
* For each array item
  * If value is not null : prime
    * Copy and print
    * Print comma
    * Copy again as counter
    * Move cells on the left and decrease counter
    * When counter is null, N is a factor of current cell : reset cell and recreate counter, then continue
* loop

# Code
```
>++++[-<+++++++++++>]      ( 44 = 4x11 )
>-                         generate max value
[                          while current value is not null
  [->+>+<<]>[-<+>]         copy 2 cells ahead
  +                        set flag
  >-                       decrease next value
]                          loop
<-<-<                      remove last value (1) and go to first cell (2; on flag)
[                          while current cell is an array item
  -                        reset flag (cell is being processed but not part of the array anymore)
  <[                       if number is not null : prime
    [->>+>>+<<<<]>>>>      copy (note leave the ex flag cell empty to ease array browsing)
    [>>>>++++++++++<<<<[-  print N as decimal number
    >+>>+>-[<-]<[->>+<<<<   ** part 2 **  
    [->>>+<<<]>]<<]>+[-<+   ** part 3 **
    >]>>>[-]>[-<<<<+>>>>]   ** part 4 **
    <<<<]<[>++++++[<+++++   ** part 5 **
    +++>-]<-.[-]<]          ** part 6 **
    <<<<[<<]<.             print comma
    >>>[>>]                go back to end of array
    >[->+>>+<<<]>[-<+>]<   copy value as cell counter
    <<<[                   go to last array cell
      -<[->>+<<]>>>+       move to right (reset flag then move value then set new flag)
      [>>]+                go to counter and set else flag
      <-[>-]>[             decrease counter; if null (else flag still set)
        -                  reset else flag
	<<[<<]>            go to last moved value
	[-]                reset value (multiple of N)
	>[>>]>>            go back to end of array and then counter saved copy
	[-<+<<+>>>]<[->+<] create a new counter
      ]                    end if (position: just before counter saved copy; the last non empty cell in memory)
    <<<[<<]<<]             process next cells
    >>>>[-<[-<<+>>]<+>>>>] Move back all array cells
    >>[-]<<<[-]            reset counter remainder and counter copy
  <<]                      end if
<]                         loop
```

# Minified version
```
>++++[-<+++++++++++>]>-[[->+>+<<]>[-<+>]+>-]<-<-<[-<[[->>+>>+<<<<]>>>>[>>>>++++++++++<
<<<[->+>>+>-[<-]<[->>+<<<<[->>>+<<<]>]<<]>+[-<+>]>>>[-]>[-<<<<+>>>>]<<<<]<[>++++++[<++
++++++>-]<-.[-]<]<<<<[<<]<.>>>[>>]>[->+>>+<<<]>[-<+>]<<<<[-<[->>+<<]>>>+[>>]+<-[>-]>[-
<<[<<]>[-]>[>>]>>[-<+<<+>>>]<[->+<]]<<<[<<]<<]>>>>[-<[-<<+>>]<+>>>>]>>[-]<<<[-]<<]<]
```

# Final state

* Memory: 44, 0, 0, 0
* Cursor: on 2nd cell
* Input: empty 
* Output: All prime numbers, base 10, comma separated

# Test program

Let's replace the "-" that generates the max value by a "," that reads a char

```
>++++[-<+++++++++++>]>
                      ,
                       [[->+>+<<]>[-<+>]+>-]<-<-<[-<[[->>+>>+<<<<]>>>>[>>>>++++++++++<
<<<[->+>>+>-[<-]<[->>+<<<<[->>>+<<<]>]<<]>+[-<+>]>>>[-]>[-<<<<+>>>>]<<<<]<[>++++++[<++
++++++>-]<-.[-]<]<<<<[<<]<.>>>[>>]>[->+>>+<<<]>[-<+>]<<<<[-<[->>+<<]>>>+[>>]+<-[>-]>[-
<<[<<]>[-]>[>>]>>[-<+<<+>>>]<[->+<]]<<<[<<]<<]>>>>[-<[-<<+>>]<+>>>>]>>[-]<<<[-]<<]<]
```

This will write prime numbers up to a given limit (ex : 'x' for primes up to 120)

