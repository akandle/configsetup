# TMUX Reference

## Setup
> Uses Oh My Tmux
## Basic Uses
- Control-b is command
- C-b w - lists windows
- l - last window
- p or n - previous/next
- , - rename window
- c - create window
- d - detach session
- s - show all sessions
- $ - rename session
- & - close current window
- :swap-window -s # -t #  - swaps window numbers
- : - apparently can invoke commands ala vim style
- % - Split pane vertically
- " - split horizontally
- x - kill current pane
- q - display pane numbers
- Alt-up/down/left/right - resizes pane by 5 units
- Ctrl-up/down/left/right - resize by 1 unit
- { or } - move pane left or right
- up/down/left/right arrows - move to pane in direction
- [ - enter copy mode
    - followed by
        - q - quit
        - g - go to top line
        - G - go to bottom
        - w or b - forward/backword one word at time
        - / or ? - search forward/backward
            - n or N for next or prev
        - Spacebar - start selection
        - Esc - clear selection
        - Enter - copy selection
        - C-b ] - paste contents of buffer_0
- :show-buffer - displays contents of buffer_0
- :capture-pane - copy all visible pane to a buffer
- :list-buffers - show all buffers
- :choose-buffer - show all buffers and past selection
- :save-buffer buf.txt - save bugger to buf.txt
- :delete-buffer -b 1 - delete buffer_1
-
- ```
    // mysession is name of new session
    tmux -s mysession

    // mysession is name of session to attach to
    tmux attach -t mysession

    // kill mysession
    tmux kill-session -t mysession
  ```
- C-b $ - Rename session
