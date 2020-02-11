### vi

- COMMAND MODE —> i, a (use end of line)- insert mode; o - line below; R - replacement 

### Navigation 

h —> left 
j —> down
k —> up
l —> right 

0 —> beginning of the line 
$ —> end of the line 
w —> next word 
b —> word before 

H —> homes the screen
L —> bottom the screen
5G —> go to line 5
G —> last line 

R —> replacement 
u —> undo 


### Deleting 

x —> deletes a char 
X —> deletes a char before 
1d —> deletes one line
4dd —> deletes four lines
dw —> deletes the following word 
d$ —> deletes to the end of the line 
d0 —> deletes to the beginning of the line 
dG —> deletes to the end of the text
d1G —> deletes to the beginning of the text 

### Replacement 

cc —> rewrite a line from the command mode 
cw —> rewrite a word from the command mode 
c$ —> replace to the end of the line 
c0 —> replace to the beginning of the line 
c/fwe —> replace from cursor to the next occurrence of fwe 

:%s/original/replacement/g —> replaces global
:10,15s/original/replacement/g —> replaces between lines 10 and 15 

### Cut, Copy, and Paste 

p —> pastes a line; P - pastes a line before 
yy —> yanks one line 
4yy —> yanks four lines  

“cy4w —> copies next four words into buffer c 
“cp —> paste buffer c

~ —> changes CASE of a word 
/text —> search 
?text —> search backwards 

- EX MODE —> : - from Command mode 

:w —> writes the file 
:wq = ZZ —> saves 
:q! —> quits but doesn’t save 
:r —> include an old file in an existing one


:w !sudo tee % --> edit read only files 

- INSERT MODE —> Esc key - returns to Command mode 