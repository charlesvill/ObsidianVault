using nvchad with video from dreams of code on set up for C++

debugging: 
in order to debug, you need to set the markers for the compiler for debugging: 
	`clang++ --debug scriptname.cpp -o main`
	- in order to set a watch expression, you move the cursor in the watch section and move into insert mode and name the variable to watch
	- 
Keybinds: 
- append end: A
- append beginning: I
- delete word from start of the word: dw
- delete till end of line: d$
- delete from cursor to end of word including last : de
- bring to beginning of the word: 0
- fix a whole line: U
- redo: ctrl-r
- change until end of word: ce
- change the entire line: cc *useful!*
- beggining of the file: gg
- specific line: #+G
- get line number: ctrl+ G
- cycle through searches: n
- cycle backwards: N
- search backwards: ?
- move cursor to matching bracket: % (on a bracket)
- :#,#s/old/new/g sub out in the range of lines
- :%s/old/new/gc: sub out in the whole file but prompting for each one
- set breakpoint: leader (space) + d + b
- start debugging
what is a vim register?