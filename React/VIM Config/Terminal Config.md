[Josean Link](https://www.josean.com/posts/terminal-setup)

# Installing Themes

Themes [Gallery](https://iterm2colorschemes.com/). Choose a team and download it with the following command, replace the repo's URL.

```bash
curl https://raw.githubusercontent.com/nordtheme/iterm2/develop/src/xml/Nord.itermcolors --output ~/Downloads/nord.itermcolors
```

After downloading the theme file, we can go to Iterm's `Preferences > Profiles > Colors`, then we import the `Color Preset`, we must then select the theme from the dropdown.

## Cursor Color
In the same screen, we must select `Smart Cursor` this is so when we're using a Light NeoVim theme, the cursor doesn't has a hard-to-see color.

# Tmux theme

We must add the theme config in `~/.tmux.conf`:

```conf
set -g @plugin "nordtheme/tmux"
```