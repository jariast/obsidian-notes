# Surround

## Add surrounding chars
`ys` + `motion` + `<surroundingChar>`

Example: To surround a word with the `"` char, we can use:

`ys + w + "`

## Remove surrounding
To remove surrounding chars we can use `ds + <surruondingChar>`

## Replacing surrounding

`cs + <oldSurroundingChar> + <newSurroundingChar>`

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