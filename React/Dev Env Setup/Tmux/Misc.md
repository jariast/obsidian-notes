Create Tmux session: `tmux new -s <sessionName>`

Exit Session : `tmux detach`

Attach to specific session: `tmux attach -t <sessionName>`

Note: prefix is `Ctrl + a`
Session List inside Tmux: `<prefix> + s`

Tmux Sessions have Windows and Panes. A Window is a collection of split Panes.

Split Vertically: `<prefix> + |`
Split Horizontally: `<prefix> + -`

Refresh config: `<prefix> + r`

# Resizing panes

`<prefix> + <directionalKey>`

Directional key is one of `h,j,k,l`

Toggle Pane Maximize: `<prefix> + m`

Windows List: `<prefix> + w`

# Copy Mode

Copy mode is useful to navigating a terminal, for example when you have a Pane with Unit Tests Output, you can navigate that output.

To enter into Copy Mode: `<prefix> + [`
Exit Copy Mode: `Ctrl + c`

Navigate: Use nav keys (h, j, k, l)

Go Up half page: `Ctrl + u`
Go Up half page: `Ctrl + d`

Go Up Full Page: `Ctrl + b`
Go Down Full Page: `Ctrl + f`
