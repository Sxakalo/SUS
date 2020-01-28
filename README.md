# $_$ aka "SUS"
A perl interpreter for the esolang [$_$](https://esolangs.org/wiki/$_$)

More info can be found at: https://esolangs.org/wiki/$_$

Can be run from the commandline in the form: `perl main.pl <commandline args>`

I have created a very simple batch script for Windows so you can run `sus <commandline args>` instead.
Creating other equally simple shell scripts should not be a problem.

## Commandline Args:
+ `<inline script>` = execute *inline script*
+ `-f <filename>` = run script in *filename*

## Definitions:
+ *s* - Built-in variable. Empty string.
+ *N* - The number of consecutive characters. i.e. *N* for `----` is 4.

## Commands
    *(ORDER is important!)*

    1. "_" : Append the character with the ASCII value *N* to *s*.
    2. "-" : Like "_", but prepend the character to *s* instead.
    3. "$" : Print the value of *s*, and if *N* is odd, reset it to an empty string.
    4. "&" : Separate calls of the same character.
    5. "@" : Create label *N*.
    6. "!" : Assign the most recently created label to the *N*'th character call.
    7. "#" : Go to Label *N*.
    8. "." : Stop executing.
    9. "%" : Begin or end a comment.
    10. "?" : Ask the user for input and append it to *s*.
    11. "+" : Append the source of the (*N*-1)th call in the program to *s*. If *N* is 1, the entire source code is stored in *s*.
    12. 1 : Begin defining a new miniprogram *N*.
    13. 2 : Stop defining miniprogram *N*.
    14. 3 : Add the *N*th character in this list to the miniprogram.Followed by a *4* call.
    15. 4 : Determines *N* for the character added in the previous *3* call as the *N* of this *4* call.
    16. 5 : Run miniprogram *N*.
    17. "z" : Wait *N* seconds.
    18. ";" : Print the lyrics to All Star by Smash Mouth *N* times.
    13. "*" : Interpret *s* as source code. Inspired by [InterpretMe](https://esolangs.org/wiki/InterpretMe)

## Examples
I have tested all of these examples taken directly from the esolang wiki:

### Hello world!
`________________________________________________________________________&_____________________________________________________________________________________________________&____________________________________________________________________________________________________________&____________________________________________________________________________________________________________&_______________________________________________________________________________________________________________&____________________________________________&________________________________&_______________________________________________________________________________________&_______________________________________________________________________________________________________________&__________________________________________________________________________________________________________________&____________________________________________________________________________________________________________&____________________________________________________________________________________________________&_________________________________$.`

### Cat:
`?$.`

### Quine:
I removed the extra comment character `%` but it will work either way

`+$.`

### Label Example:
`@!!!!!#.?$.`
#### Explanation:
`@` creates label1, the `!!!!!` applies the label before the 5th call (before the `?`) and the `#` 
jumps to the label, skipping the `.` (exit) call; 

### Miniprogram Example:
(I added an additional 3 in each 3 call. I believe this to be an error in the original wiki version)

`133333333334333433333333425`
#### Explanation:
`1` creates 'miniprogram'1, then the first set of `3` (a total of 10) sets the call to the 10th symbol `?`.
the first `4` sets the *N* of that `?` call to 1 (because *N* is ignored in the `?` call).
The next set of `3` (total of 3), adds the `$` call to the miniprogram and the next `4` again sets the *N*
for that call to 1.
The last set of `3` (total of 8), adds the `.` call and the next `4` sets the *N* to 1.
Finally, the `2` call closes the `1` call and `5` runs the 'miniprogram'.
