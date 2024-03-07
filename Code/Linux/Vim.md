mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[Linux]]

#### Navigation (default mode)
- h = left
- j = down
- k = up
- l = right
- b = backward word (caps for bigger jump)
- w = forward word
- e = end of line/word
- G = go to bottom of screen

#### editing (still in default mode)
- yy = copy current line
- shift-v = visual mode (to highlight multiple lines)
- p=paste
- dd = delete
- 10dd = perform delete 10 times (any number can be used)
- 10p = perform paste 10 times
- c = change current word and go to insert mode
- cw = change current word and remove the word

#### Insert mode (for normal writing)
* i = enter insert mode before the cursor
- I = enter insert mode at beginning of line
- esc = exit insert mode

#### : commands
- :set number = gives numbers to the lines
- :w = write
- :wq = write and quit
- :q! = force to quit without writing


## Resources
* https://www.freecodecamp.org/news/7-vim-tips-that-changed-my-life/
* cheatsheet: https://vim.rtorr.com/