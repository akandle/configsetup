# Vim Quick Reference

## Setup
> Uses awesome vimrc
> *Now have custom vimrc additions, found in ~/.vim_runtime/my_configs.vim*

## Cool Advanced stuff
- Copy from a file into a register, and then paste into vim term window
    ```
    // To copy from terminal win
    C-w N - puts the terminal window into "normal" mode, use standard normal mode ops
    // To paste into the terminal window
    C-w "[reg] - where [reg] is the register to paste from"
    // To copy from a normal window into a specific refister
    // In visual mode
    *make visual selection*
    "[reg]y - will yank the selection into [reg], same as above
    // to paste from a specific register
    "[reg]p - will put the contents of [reg] after the curser
    ```
## Basic Usage
- :resize # - where # is size in lines(vert) or +# or -# to increment the adjustment
- :vertical resize # - same as above but for columns of width
- :bel terminal - open terminal in window below current
- The leader key is ','
- ,nn : Opens Nerdtree
- C-W h/j/k/l : moves control to window in direction indicated
- h/j/k/l : Moves within a window 
- :w : writes buffer to disk
- :e : opens a new file ie: :e someDir/fileName.ext
- :ls : lists the open buffers
- :b# : switches to that buffer number, seen in :ls buffer list
- dd : deletes line
- 0 : goes to beginning of line
- $ : goes to end of the line
- x : delete character under cursor
- d#w : deletes # of words. can use e for end of word, w to beginning of next word, $ to end of line
- i : insert before cursor
- a : append after cursor
- u : undo
- C-r : redo
- . : repeats actions, not totally sure how this works
- :term : opens new window with terminal
- :split or :vsplit : splits window hor or ver
