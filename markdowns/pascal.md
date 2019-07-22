# Pascal's triangle

Pascal's triangle is a triangular array of binomial coefficients: cell k of row n indicates how many combinations exist of n things taken k at a time. It looks like this
* 1
* 1 1
* 1 2 1
* 1 3 3 1
* 1 4 6 4 1
* ...

One can prove that a given cell  is the sum of 2 cells from previous row: the one just above and the one on top left.

Given that, let's see how we can generate the Nth row of Pascal's triangle

# Let's start

* Memory: empty 
* Cursor: first cell
* Input: a decimal number N (greater than 0)

# Process

* Read a decimal number
* Init _line 0_ : just 1
* While counter is not null
  * Decrease counter
  * Generate next line
    * Go to row last cell (e.g. mem : A B C D 0 0 0 
    * Move it to the next 2 cells (e.g. mem : A B C 0 D D)
    * Go to previous cell and loop 
      * mem : A B 0 C C+D D
      * then A 0 B B+C C+D D
      * and finally 0 A A+B B+C C+D D
    * Move all values back on the left
* Print last line, comma separated. Line is symetric : can be print from right to left as well
* Print '1' and ignore first value (it's always 1)
* While there is an item
  * Print comma
  * Move / Print item
  * Go left
* Loop

# Code
```
>,[>++++++[-<-------->]>+++++++++[-    read an integer 
<<<[->+>+<<]>>[-<<+>>]>]<<[-<+>],]      ** part 2 **
>+                                     Initialize first row
<<[                                    while counter is not null
  -                                    decrease counter
  >>[>]<                               go to last cell
  [[->+>+<<]<]                         while there is a cell: move to the next 2 ones on the left and repeat
  >>[[-<+>]>]                          Move whole array to the left
  <<[<]<                               back to counter
]                                      loop
>+++++++[-<+++++++>]<.-----            print 49 (='1') and change into comma (44)
>>[>]<-<                               go to last cell (1) then reset; then go to previous cell
[                                      for each cell in the row
  [<]<.>>[>]<                          print comma (first memory cell) then go back to the current cell
  [->+<]>                              move to the right (at least one 0 needed to print a decimal value)
  [>>>>++++++++++<<<<[->+>>+>-[<-]<[-  Print decimal value
  >>+<<<<[->>>+<<<]>]<<]>+[-<+>]>>>[-   ** part 2 **
  ]>[-<<<<+>>>>]<<<<]<[>++++++[<+++++   ** part 3 **
  +++>-]<-.[-]<]                        ** part 4 **
<]

```

# Minified version
```
>,[>++++++[-<-------->]>+++++++++[-<<<[->
+>+<<]>>[-<<+>>]>]<<[-<+>],]>+<<[->>[>]<[
[->+>+<<]<]>>[[-<+>]>]<<[<]<]>+++++++[-<+
++++++>]<.----->>[>]<-<[[<]<.>>[>]<[->+<]
>[>>>>++++++++++<<<<[->+>>+>-[<-]<[->>+<<
<<[->>>+<<<]>]<<]>+[-<+>]>>>[-]>[-<<<<+>>
>>]<<<<]<[>++++++[<++++++++>-]<-.[-]<]<]
```

# Final state

* Memory: 44, 0, 0, 0 
* Cursor: on second cell
* Input: read (empty)
* Output: Nth row from Pascal's triangle (modulo 256)

_Note_: because of the nature of the algorithm, if a cell equals 0 on a row it will break the loop. And modulo 256, a cell can actually be null.

However, the first cell that will be a multiple of 256 in standard Pascal's triangle appears on row 256, and the counter itself, from user input, cannot be more than 255.

In other words: this algorithm is valid as long as we rely on a counter. Having an infinite loop to generate more than 255 rows will fail. We can of course introduce 2-cell-long arrays but it's not really important here.

