# Tmux Shortcuts for Maximum Productivity

The default prefix key is Ctrl + b. Press it before any shortcut below unless noted otherwise.

## Session Management

* tmux – start a new session
* tmux new -s name – start a new session with a name
* tmux ls – list all sessions
* tmux attach -t name – attach to a named session
* tmux kill-session -t name – kill a named session
* tmux kill-server – kill all sessions
* Prefix + d – detach from current session
* Prefix + $ – rename current session
* Prefix + s – list and switch between sessions
* Prefix + ( – switch to previous session
* Prefix + ) – switch to next session
* Prefix + L – switch to last session

## Window (Tab) Management

* Prefix + c – create a new window
* Prefix + , – rename current window
* Prefix + & – close current window (with confirmation)
* Prefix + w – list and choose a window interactively
* Prefix + n – move to the next window
* Prefix + p – move to the previous window
* Prefix + 0-9 – switch to window by number
* Prefix + l – toggle to last active window
* Prefix + ' – select window by index prompt
* Prefix + . – move/renumber current window to a new index

## Pane Management

* Prefix + % – split pane vertically (left/right)
* Prefix + " – split pane horizontally (top/bottom)
* Prefix + x – close current pane (with confirmation)
* Prefix + o – cycle through panes
* Prefix + ; – toggle to last active pane
* Prefix + q – show pane numbers (press number to jump to it)
* Prefix + z – toggle pane zoom (fullscreen and back)
* Prefix + ! – convert pane into a new window
* Prefix + { – move current pane left
* Prefix + } – move current pane right
* Prefix + Ctrl + o – rotate pane contents clockwise
* Prefix + Alt + o – rotate pane contents counter-clockwise
* Prefix + m – mark the current pane (for use with join-pane/swap-pane)
* Prefix + M – clear the marked pane
* Prefix + Space – cycle through pane layouts

## Pane Navigation

* Prefix + Up – move to pane above
* Prefix + Down – move to pane below
* Prefix + Left – move to pane on the left
* Prefix + Right – move to pane on the right

## Pane Resizing

* Prefix + Ctrl + Up – resize pane up by 1 row
* Prefix + Ctrl + Down – resize pane down by 1 row
* Prefix + Ctrl + Left – resize pane left by 1 column
* Prefix + Ctrl + Right – resize pane right by 1 column
* Prefix + Alt + Up – resize pane up by 5 rows
* Prefix + Alt + Down – resize pane down by 5 rows
* Prefix + Alt + Left – resize pane left by 5 columns
* Prefix + Alt + Right – resize pane right by 5 columns

## Copy Mode (Scrollback and Selection)

* Prefix + [ – enter copy mode (use arrow keys or PgUp/PgDn to scroll)
* q – exit copy mode
* Space – start selection (in copy mode)
* Enter – copy selection and exit copy mode
* Prefix + ] – paste copied text
* / – search forward (in copy mode)
* ? – search backward (in copy mode)
* n – next search match (in copy mode)
* N – previous search match (in copy mode)
* g – go to top of buffer (in copy mode)
* G – go to bottom of buffer (in copy mode)
* H – move to top of visible screen (in copy mode)
* M – move to middle of visible screen (in copy mode)
* L – move to bottom of visible screen (in copy mode)
* w – move forward one word (in copy mode)
* b – move backward one word (in copy mode)
* e – move to end of word (in copy mode)
* 0 – beginning of line (in copy mode)
* ^ – first non-blank character of line (in copy mode)
* $ – end of line (in copy mode)
* Ctrl + u – half-page up (in copy mode)
* Ctrl + d – half-page down (in copy mode)
* Ctrl + b – full page up (in copy mode)
* Ctrl + f – full page down (in copy mode)
* v – start selection in vi mode (in copy mode, requires mode-keys vi)
* y – yank/copy selection in vi mode (in copy mode, requires mode-keys vi)

## Layouts

* Prefix + Space – cycle through preset layouts
* Prefix + Alt + 1 – even-horizontal layout
* Prefix + Alt + 2 – even-vertical layout
* Prefix + Alt + 3 – main-horizontal layout
* Prefix + Alt + 4 – main-vertical layout
* Prefix + Alt + 5 – tiled layout

## Miscellaneous

* Prefix + t – show a clock in the current pane
* Prefix + ? – list all key bindings
* Prefix + : – enter command mode
* Prefix + r – force redraw of the attached client
* Prefix + ~ – show previous tmux messages
* Prefix + i – display info about the current window/pane
* Prefix + # – list all paste buffers
* Prefix + = – choose a paste buffer interactively
* Prefix + - – delete the most recent paste buffer

## Useful Commands (Command Mode or CLI)

* tmux list-keys – list all key bindings
* tmux list-commands – list all tmux commands
* tmux source-file ~/.tmux.conf – reload tmux configuration
* tmux swap-window -t N – swap current window with window N
* tmux swap-pane -t N – swap current pane with pane N
* tmux select-layout layout – set a layout (tiled, even-horizontal, even-vertical, main-horizontal, main-vertical)
* tmux pipe-pane -o 'cat >> ~/tmux.log' – log pane output to a file
* tmux capture-pane -p – print pane contents to stdout
* tmux set -g mouse on – enable mouse support (resize panes, select windows, scroll)
* tmux set -g mouse off – disable mouse support
* tmux display-message -p '#S:#I.#P' – print current session:window.pane
* tmux join-pane -s N – join pane N into the current window (opposite of !)
* tmux break-pane -d – break pane to new window without switching to it
* tmux resize-pane -Z – toggle zoom from command mode
* tmux set synchronize-panes on – type in all panes simultaneously
* tmux set synchronize-panes off – stop synchronized input
* tmux choose-tree – interactive tree view of sessions/windows/panes
* tmux rename-session -t old new – rename a session from CLI
