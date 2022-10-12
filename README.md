Vim Tips



1. Find a good .vimrc and steal it
    * There’s usually ones for different languages
    * It goes in your home directory
    * It sets your editing environment, like syntax highlighting, change history, line numbers, function abbreviations, key maps, etc.
    * note you can have file type specific sections
2. Find some good vim plugins and steal them
    * They go in ~/.vim/plugin
    * buffet.vim
    * cscope.vim
    * written in “vimscript”
3. In vim, you’re in insert or edit mode.  In edit mode you can enter commands.  In insert mode you enter your text.  You can define “iabbrevs” in .vimrc to enter commands in insert mode.  Best to put these in extension specific sections.  I created a simple random number function for c files for the demo so that if I type “$r” in insert mode, I’ll get a random number.
4. HJKL keys are beautiful! ← aka Vim keys allow you to do navigation in edit mode without moving your hands away from the important part of the keyboard. H is left, J is down, K is up and L is right.
5. Vim highlights all search matches.  I turn on incremental search so I don’t have to hit enter to see matches.  To turn off the highlighting, use the command :noh
6. If your cursor is over a word you want to search for, use the “*” key to search for that exact word.  It won’t match places where that word is a substring of a longer word.
7. If you’re in a long function, it can be frustrating:
    * [[ ← goes to the beginning of the function
    * ]] ← goes to the end of the function
    * f (mapped for me from ShowFuncName() in .vimrc) ← shows the name of the current function.  This seems to work in most languages
    * % ← If your cursor is over a grouping character, _i.e. _{}[](), takes you to the matching beginning or end character.  Great for long annoying, nested expressions, if-statements, _etc._
8. Vim has an amazing “diff mode”, and you can compare two files using vimdiff.  If you’ve made a bunch of changes to a file, and you want to see what kind of damage you’ve done, use: “DiffOrig”.  It splits the window and shows the original file on disk and the changes in the buffer.  I map this to &lt;F3> in my .vimr:qc.
9. Use cscope and ctags.  Mostly used for c, but have been made to work for other languages.
10. You generate a tags database for ctags and a cscope database for cscope.  Cscope can be used without the cscope.vim plugin.
11. Ctags:
    * CTRL-] ← Takes you to the symbol under the cursor.  If there are multiple definitions, it’ll show you a list.
    * CTRL-T ← Takes you back from your search.
12. With Cscope, you can start vim with a symbol instead of a file
    * _e.g. _vim -t userial_open ← Finds the location in the cscope database to start you at the place that symbol is defined. If there’s more than one, it gives you a list
    * CTRL-\ then S opens the cscope menu with the symbol under the cursor.  Then, as with ctags, use CTRL-T to go back. CTRL-\ S is a little flaky sometimes, typing faster is better.  
13. You can end up with multiple files loaded into vim at the same time.  Each one has a number, so you can use that number to switch between them easily.
    * :ls shows the list of buffers
    * :b# switches to the numbered buffer, _i.e. _:b4 switches to buffer number 4
    * :bd closes the current buffer without quitting vim
    * buffet.vim is a nice buffer list plugin, and I map &lt;F2> to show the popup list of buffers and switch among them
    * CTRL-G will show you the current file name that you’re editing.
14. To automatically close brackets while typing code, add this to .vimrc:
    * ino " ""&lt;left> \
ino ' ''&lt;left> \
ino ( ()&lt;left> \
ino [ []&lt;left> \
ino { {}&lt;left> \
ino {&lt;CR> {&lt;CR>}&lt;ESC>O \
ino {;&lt;CR> {&lt;CR>};&lt;ESC>O
15. To delete a pair of parentheses, braces, brackets, etc., do this:
    * _%x``x_
        1. the % moves you to the close paren
        2. the x deletes it
        3. the two backticks move you back to the previous position
        4. the 2nd x deletes the opening paren
    * the above only works if the cursor is on or before the opening paren.  If you’re inside the parens, you need an extra % at the beginning to move the cursor back to the opening paren: _%%x``x_ 
    * If you just want to delete everything within the parens (including the parens) use _d%,_
16. If you have multiple windows open with different files, you can get them to scroll synchronously.  Use the _scrollbind _setting, so type: _:set scb! _in each window that you want to synchronize scrolling.
17. To replace the last occurrence of a string on a line, The easiest way would be to allow arbitrary text in front of the match, and specify the matched region using \zs:
    * :%s/.*\zsone/two/
18. To copy text to the clipboard so you can paste outside of vim, do this: 
    * Quickly, you can press V (Shift + v) to active visual mode. In visible mode, you can use j and k to select the text you want to copy. After selection, use
    * "*y
19. To use vim, go and git here are some useful plugins:
    * git-gutter: [https://github.com/airblade/vim-gitgutter](https://github.com/airblade/vim-gitgutter)
        5. change marks are shown in left column, i.e. the gutter
        6. ]c goes to next change
        7. [c goes to previous change
    * godoctor: [https://github.com/godoctor/godoctor.vim](https://github.com/godoctor/godoctor.vim)
20. If you have some really long lines and you want to break it up after 80 characters per line, you can do this: **_:%s/\(.\{80\}.\{-}\s\)/\1\r/g_** \
As suggested in this stackoverflow answer:  [https://stackoverflow.com/a/57676332/1212725](https://stackoverflow.com/a/57676332/1212725)
21. If you have the vim-markdown plugin installed, you can use “:GenTocGitLab” to generate a table of contents.
22. Vim Supports Spell Checking
    * :set spell will turn it on
    * To move to a misspelled word, use ]s and [s
    * Once the cursor is on the word, use z=, and Vim will suggest a list of alternatives that it thinks may be correct
