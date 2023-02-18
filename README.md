# BrainF Visualizer
I couldn't find a brainF visualizer I liked.
So I made my own.

## BrainF
BrainF is very simple, only 8 (eight) instructions.
 '+' increments the current cell
 '-' decrements the current cell
 '>' moves the writehead to the next cell
 '<' moves the writehead to the previous cell
 '[' jumps to the matching ']' if the current cell is zero
 ']' jumps to the matching '[' if the current cell is non-zero
 '.' outputs the current cell as an ASCII character
 ',' inputs a single character as an ASCII integer

## Why use this one?
I build this one to look nice, and work well \[WIP].
It's dynamically sized, so if you go off the back, it'll
add a new cell to the beginning of the tape, and if you
go off the front it'll add a new one to the end.