# Surround

## Add surrounding chars to

The `ys` shortcuts only work in nvim, they require a plugin that we installed there

`ys` + `motion` + `<surroundingChar>`

Example: To surround a word with the `"` char, we can use:

`ys + w + "`

## Surround Selection with char

Example: To surround selection with parentheses:

`xi()<Esc>P`

## Remove surrounding
To remove surrounding chars we can use `ds + <surruondingChar>`

## Replacing surrounding

`cs + <oldSurroundingChar> + <newSurroundingChar>`

## Delete inside surrounding char

`ci + <surroundingChar>`

# Comments

## Whole Line
`gc + c`

## An X amount of lines
`gc + <numberOfLines> + j`

# nvim-tree

Show tree: `<leaderKey> + e`

Add new file inside current dir: `a`

# Telescope

Find files: `<leader> + ff`

Find string in project: `<leader> + fs`

# Hover stuff
 `K` is like hovering the mouse on VSCode