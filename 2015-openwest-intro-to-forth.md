%title: An Introduction to Forth
%author: Alpheus Madsen
%date: Date to be determined
%date: OpenWest










           ____ An Introduction to    
          |  __|              _    _    
          | |_   ___   ___  _| |_ | |   
          |  _| / _ \ |  _||_   _|| |_ 
          | |  | (_) || |    | |_ |   \ 
          |_|   \___/ |_|    |___||_[]_|
    
    A Quirky, Yet Surprisingly Powerful Language


-> Alpheus Madsen <-
-> alpheus.madsen@gmail.com <-

-> Open West <-
-> Saturday, May 9, 2015 <-

---------------------------------------------------------

-> A Brief Description of Forth <-

* First created in the 1950's by Charles Moore
* Moore considered this to be a "Fourth Generation" language
* First made public in the 1970's
* First used in astronomy, and can still be found there
* "Popular" in the 1980's when alternatives were BASIC and "Assembler"
* Forth is a "Space Faring" language

---------------------------------------------------------

-> A Brief Description of Forth <-

* A computer language
* An Operating System
* An Editor
* An Assembler
* Fits comfortably in very tiny spaces!

---------------------------------------------------------

-> A Brief Description of Forth <-

* A computer language
* An Operating System
* An Editor
* An Assembler
* Fits comfortably in very tiny spaces!




    Currently Forth is the only programming language that compiles and runs
    on the Arduino. I.e., the Forth compiler is currently the only compiler
    that runs in the ATmega328 on the Arduino. (The Arduino C++ compiler 
    runs on a laptop or other "big" computer).
    
                                        -- playground.arduino.cc

---------------------------------------------------------

-> Other Stack-based Postfix Languages <-

* Joy
* Factor
* PostScript

----------------------------------------------------------

-> The Interpreter and the Stack <-

Forth has an incredibly simple syntax, with a very simple Interpreter.

- Read input up to Space.
- Is it a "word"?  Execute it!
- Is it a number?  Push it on the stack!
- Otherwise, declare an error.  :-(
- Repeat.

--------------------------------------------------------

-> The Interpreter and the Stack <-

Forth has an incredibly simple syntax, with a very simple Interpreter.

- Read input up to Space.
- Is it a "word"?  Execute it!
- Is it a number?  Push it on the stack!
- Otherwise, declare an error.  :-(
- Repeat.



EXAMPLE.  10 20 30 + swap - .

---------------------------------------------------------

-> The Interpreter and the Stack <-


EXAMPLE.  10 20 30 + swap - .

                                   __         
    [    ]  [ 10 ]  [ 20 ]  [ 30 ]   } + [ 50 ]  --> Continued
      A             [ 10 ]  [ 20 ] _/    [ 10 ]
      |                     [ 10 ]
      |
      \--- Stack starts out empty...

           __              __
    [ 50 ]   } swap [ 10 ]   } - [ 40 ] . ==>  [    ] 40 ok
    [ 10 ] _/       [ 50 ] _/                    A     A
                                                 |     |
                        Stack ends up empty -----/     |
                                                       |
                        Output to stream --------------/

---------------------------------------------------------

-> The Interpreter and the Stack <-


EXAMPLE.  10 20 30 + swap - .

                                   __         
    [    ]  [ 10 ]  [ 20 ]  [ 30 ]   } + [ 50 ]  --> Continued
      A             [ 10 ]  [ 20 ] _/    [ 10 ]
      |                     [ 10 ]
      |
      \--- Stack starts out empty...

           __              __
    [ 50 ]   } swap [ 10 ]   } - [ 40 ] . ==>  [    ] 40 ok
    [ 10 ] _/       [ 50 ] _/                    A     A
                                                 |     |
                        Stack ends up empty -----/     |
                                                       |
                        Output to stream --------------/

- Disadvantages
    - It can be tricky to keep track of items on stack
    - Can quickly become unreadable
- Advantages
    - No need for parentheses
      ( used for comments instead )
    - Simple mechanism for keeping track of data
    - Allows for surprising readability

---------------------------------------------------------

-> Dictionaries and the Compiler <-

Forth also has an incredibly simple compiler.

---------------------------------------------------------

-> Dictionaries and the Compiler <-

Forth also has an incredibly simple compiler.

     _                              _
    (_)                            (_)
     _    This is the compiler.     _
    (_)                            ( )
                                   |/

---------------------------------------------------------

-> Dictionaries and the Compiler <-

Forth also has an incredibly simple compiler.

     _                              _
    (_)                            (_)
     _    This is the compiler.     _
    (_)                            ( )
                                   |/

* Read first input and create a new dictionary entry with its name.
* Read next input up to a space.
* Is it an "Immediate" word?  Execute it!
* Is it a "Regular" word?  Compile it!
* Is it a number?  push it on the stack?
* Otherwise, stop and report an error.  :-(
* Repeat!

NOTE:  ";" isn't *really* a part of the compiler.  ";" compiles
"EXIT" as its last word, and then returns control back to the
interpreter.

---------------------------------------------------------

-> Dictionaries and the Compiler <-

A "word" in Forth typically has the following structure:

    [   5   ]  Length of the name.
    [   H   ]  --\
    [   E   ]     \
    [   L   ]      } The characters of the name
    [   L   ]     /
    [   O   ]  --/
    [ link  ]  The link to the previous word
    [  ptr  ]  The Code Pointer --> How to execute the word
    [ param ]  The Parameter Field (the word's data)

--------------------------------------------------------

-> Dictionaries and the Compiler <-

Words in Forth are linked together in dictionaries

    [ inning    ] <---\
    [ bat       ] <---{
    [ football  ] <---|------------------------\ 
    [ basket    ] <---|-----------\            |
    [ ball      ] <---|-----------{            |
    [ touchdown ] <---|-----------|------------{
    [ court     ] <---|-----------{            |
    [ diamond   ] <---{           |            |
    [ ball      ] <---{           |            |
                      |           |            |
    Dictionaries      |           |            |
                      |           |            |
                  baseball    basketball    football

-----------------------------------------------------------

-> Compiler Words <-

Rather than create a complex compiler that parses a complex
syntax, Forth "extends" the compiler through "Compiler Words".

As an example, we can define a new control structure, "tif", that
would have three branches instead of two:

    [test] tif [positive] else-false [negative] else-uncert [zero] tif-then

-----------------------------------------------------------

-> Compiler Words <-

Rather than create a complex compiler that parses a complex
syntax, Forth "extends" the compiler through "Compiler Words".

As an example, we can define a new control structure, "tif", that
would have three branches instead of two:

    [test] tif [positive] else-false [negative] else-uncert [zero] tif-then

WARNINGS:  This example is probably a little overly-complicated, and this
code is untested, so it probably won't work....

-----------------------------------------------------------

-> Compiler Words <-

    [test] tif [positive] else-false [negative] else-uncertain [zero] tif-then

WARNINGS:  This example is probably a little overly-complicated, and this
code is untested, so it probably won't work....

    : tif   ( -- ef-addr eu-addr )                             [ tif           ]
         2 allot here dup 2+ swap                              [ (else-false)  ]
            ( flag -- )                                        [ (else-uncert) ]
         does>  over >0 if drop drop else                      +---------------+
                over <0 if swap drop @ jump else               |   does>       |
                swap drop 2+ @ jump then then ;  immediate

-----------------------------------------------------------

-> Compiler Words <-

    [test] tif [positive] else-false [negative] else-uncertain [zero] tif-then

WARNINGS:  This example is probably a little overly-complicated, and this
code is untested, so it probably won't work....

    : tif   ( -- ef-addr eu-addr )                             [ tif           ]
         2 allot here dup 2+ swap                              [ (else-false)  ]
            ( flag -- )                                        [ (else-uncert) ]
         does>  over >0 if drop drop else                      +---------------+
                over <0 if swap drop @ jump else               |   does>       |
                swap drop 2+ @ jump then then ;  immediate

    : else-false ( ef-addr eu-addr -- then-addr eu-addr )      [ else-false    ]
         swap 1 allot here swap ! here swap                    [ (then)        ]
         does> @ jump ;  immediate                             +---------------+
                                                               |   does>       |

-----------------------------------------------------------

-> Compiler Words <-

    [test] tif [positive] else-false [negative] else-uncertain [zero] tif-then

WARNINGS:  This example is probably a little overly-complicated, and this
code is untested, so it probably won't work....

    : tif   ( -- ef-addr eu-addr )                             [ tif           ]
         2 allot here dup 2+ swap                              [ (else-false)  ]
            ( flag -- )                                        [ (else-uncert) ]
         does>  over >0 if drop drop else                      +---------------+
                over <0 if swap drop @ jump else               |   does>       |
                swap drop 2+ @ jump then then ;  immediate

    : else-false ( ef-addr eu-addr -- then-addr eu-addr )      [ else-false    ]
         swap 1 allot here swap ! here swap                    [ (then)        ]
         does> @ jump ;  immediate                             +---------------+
                                                               |   does>       |

    : else-uncert ( then-addr eu-addr -- then-addr then-addr ) [ else-uncert   ]
         1 allot here swap ! here                              [ (then)        ]
         does> @ jump ;  immediate                             +---------------+
                                                               |   does>       |

-----------------------------------------------------------

-> Compiler Words <-

    [test] tif [positive] else-false [negative] else-uncertain [zero] tif-then

WARNINGS:  This example is probably a little overly-complicated, and this
code is untested, so it probably won't work....

    : tif   ( -- ef-addr eu-addr )                             [ tif           ]
         2 allot here dup 2+ swap                              [ (else-false)  ]
            ( flag -- )                                        [ (else-uncert) ]
         does>  over >0 if drop drop else                      +---------------+
                over <0 if swap drop @ jump else               |   does>       |
                swap drop 2+ @ jump then then ;  immediate

    : else-false ( ef-addr eu-addr -- then-addr eu-addr )      [ else-false    ]
         swap 1 allot here swap ! here swap                    [ (then)        ]
         does> @ jump ;  immediate                             +---------------+
                                                               |   does>       |

    : else-uncert ( then-addr eu-addr -- then-addr then-addr ) [ else-uncert   ]
         1 allot here swap ! here                              [ (then)        ]
         does> @ jump ;  immediate                             +---------------+
                                                               |   does>       |

    : tif-then  ( then-addr then-addr -- )
        here swap !
        here swap ! ;  immediate

----------------------------------------------------------

-> Compiler Words <-

Forth also has a number of "Defining" words.

* :
* variable
* constant
* create

It's also possible to create our own "defining" words.

-----------------------------------------------------------

-> Compiler Words <-

Forth also has a number of "Defining" words.

* :
* variable
* constant
* create

It's also possible to create our own "defining" words.

EXAMPLE:

    : constant  create , does> @ ;

------------------------------------------------------------

-> Compiler Words <-

Forth also has a number of "Defining" words.

* :
* variable
* constant
* create

It's also possible to create our own "defining" words.

EXAMPLE:

    76 constant trombones


                  +--- Creates a new entry
                  |    +--- Stores stack value in PFA
                  |    |      +--- Leave PFA on stack
                  |    |      |   +--- Fetch value in PFA
                  |    |      |   |
    : constant  create ,    does> @ ;
               |        |  |       |
               +---+----+  +---+---+       ("PFA" is the
                   |           |             Parameter
           runs when we   runs when we       Field
               type          type            Address)
            "constant"     "trombone"
                        or other defined
                          constant

-----------------------------------------------------------

-> A Simple Microcontroller Example <-

* 8-bit microprocessor
* 8 kilobytes RAM
* Three LEDs, multi-color
* A Motor Controller with Stepper Motor
* Two push buttons

                                                   ___
                                                  /   \
                                           +-----(  M  )
                                           |      \___/
                +--------------------------+----+
    LED1(RGB) --| Addr1,2,3           Addr10,11 |
                |                               |  ___
    LED2(RGB) --| Addr4,5,6              Addr12 |--o o--
                |                               |  ___
    LED3(RGB) --| Addr7,8,9              Addr13 |--o o--
                +-------------------------------+ 



(Sadly, I didn't have the time to set up and program an actual Arduino...)

-----------------------------------------------------------

-> A Simple Microcontroller Example <-

    ( First, define motor variables )
    
        variable motor-delay
        100 motor delay !

    ( Define an array to represent the motor )
    
    variable motor-1  1 allot
    <motor-step-addr>      motor !
    <motor-direction-addr> motor 2+ !

    ( Define a couple of "helper words" for the array )
    
    : clockwise 0 ;
    : counter-clockwise 1 ;

-----------------------------------------------------------

-> A Simple Microcontroller Example <-

    variable motor-delay
    100 motor delay !
    
    variable motor-1  1 allot
    <motor-step-addr>      motor !
    <motor-direction-addr> motor 2+ !
    
    : clockwise 0 ;
    : counter-clockwise 1 ;

    ( First attempt to write "turn" )
    
    : turn ( motor direction steps -- )
       >r over @ ! r>    ( motor steps )
       swap 1+ @ swap
       0 swap do
         dup 1 !
         10 delay
         dup 0 !
         motor-delay @ delay
       loop drop ;
    
    ( I found this confusing; it's difficult to follow )

    ( Allegedly, it should allow us to do this: )
    
    motor-1 clockwise 10 turn

-----------------------------------------------------------

-> A Simple Microcontroller Example <-

    variable motor-delay
    100 motor delay !
    
    variable motor-1  1 allot
    <motor-step-addr>      motor !
    <motor-direction-addr> motor 2+ !
    
    : clockwise 0 ;
    : counter-clockwise 1 ;

    ( Rewrite of this example -- I replaced "turn"  )
    
    : step ( motor -- )
      @ dup 1 !    ( run )
      10 delay     ( delay for a step )
      0 ! ;        ( end step )
    
    : set-direction ( direction motor -- )
      2+ @ ! ;

    ( Now we can say this )
    
    clockwise motor-1 set-direction
    motor-1 step

-----------------------------------------------------------

-> A Simple Microcontroller Example <-

    ( Rewrite of this example -- I replaced "turn"  )
    
    : step ( motor -- )
      @ dup 1 !    ( run )
      10 delay     ( delay for a step )
      0 ! ;        ( end step )
    
    : set-direction ( direction motor -- )
      2+ @ ! ;

    ( Now we can say this )
    
    clockwise motor-1 set-direction
    motor-1 step

    : steps ( steps motor -- )
      0 rot do
        dup step
        motor-delay @ delay
      loop drop ;

    ( And now we can say this )
    
    10 motor-1 steps

-----------------------------------------------------------

-> A Simple Microcontroller Example <-

    ( Rewrite of this example -- I replaced "turn"  )
    
    : steps ( steps motor -- )
      0 rot do
        dup step
        motor-delay @ delay
      loop drop ;

    ( And now we can say this )
    
    10 motor-1 steps

    ( And if we want to work in degrees, we can do this: )
    ( Note that there are 200 steps for 360 degrees, so 
      every degree is 5/9th of a step...)
    
    : degrees   ( degrees -- steps )
      5 9 */ ;
    
    10 degrees motor steps

-----------------------------------------------------------

-> A Simple Microcontroller Example <-


I have wonderful examples for LEDs and Buttons as well,
but I realized that presenting the code for them would be
just similar enough to what I have done with motors that
it won't really illustrate anything new...

-----------------------------------------------------------

-> A Simple Microcontroller Example <-


I have wonderful examples for LEDs and Buttons as well,
but I realized that presenting the code for them would be
just similar enough to what I have done with motors that
it won't really illustrate anything new...

(And I didn't have time to work out how the buttons would
be used to control the LEDs and motor...but I have some
really neat ideas!)

-----------------------------------------------------------

-> A Simple Microcontroller Example <-


I have wonderful examples for LEDs and Buttons as well,
but I realized that presenting the code for them would be
just similar enough to what I have done with motors that
it won't really illustrate anything new...

(And I didn't have time to work out how the buttons would
be used to control the LEDs and motor...but I have some
really neat ideas!)

And the time I have for this presentation is insufficient
to contain these examples.  ;-)

-----------------------------------------------------------

-> Questions? <-



       ___                  _   _                ___
      / _ \ _   _  ___  ___| |_(_) ___  _ __  __|__ \
     | | | | | | |/ _ \/ __| __| |/ _ \| '_ \/ __|/ /
     | |_| | |_| |  __/\__ \ |_| | (_) | | | \__ \_|
      \__\_\\__,_|\___||___/\__|_|\___/|_| |_|___(_)
    


-----------------------------------------------------------

-> Resources <-



     ____                                         _
    |  _ \ ___  ___  ___  _   _ _ __ ___ ___  ___| |
    | |_) / _ \/ __|/ _ \| | | | '__/ __/ _ \/ __| |
    |  _ <  __/\__ \ (_) | |_| | | | (_|  __/\__ \_|
    |_| \_\___||___/\___/ \__,_|_|  \___\___||___(_)
    



* "Starting Forth" by Leo Brodie

* "Thinking Forth" by Leo Brodie

* (Forth on Arduino) http://playground.arduino.cc/CommonTopics/ForthOnArduino
