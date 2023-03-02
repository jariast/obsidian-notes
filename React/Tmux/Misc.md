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