# Conffee-maker

`$cm` or Confee Maker is a command terminal interface **TUI**
to generate configuration files for different applications based on templates.

Have you ever tried to configure `nvim`, `tmux`, `alacritty` or any other
dotfiles based application config?

What if you can tell `cm` to guide throught the process?

```bash
$ cargo install cm
```

> **IMPORTANT**: `cm` doesn't simply generate the config file for you
> it will instead guide you step by step allowing the selection of each
> option one by one, including an explanation of each config it will
> **never** allow you to set some config value without agreeing with its
> purpose.

Example:

```bash
$ cm --update-templates

[1%..... downloading community templates ..... 100%]

Updated Global templates:

- nvim
- tmux
- alacritty
...
```

Pass the template name to use global or pass the location for a custom template.

e.g:

`$ cm nvim`

or

`$ cm github.com/foo/bar:nvim`

With any of above the `cm` TUI will open and guide you on the process

```bash

Welcome to Conffee Maker press [enter] to start
brewing your conffeeguration files for `nvim`
     ______________________
    (___________           |
      [XXXXX]   |          |
 __  /~~~~~~~\  |          |
/  \|@@@@@@@@@\ |   nvim   |
\   |@@@@@@@@@@||          |
    \@@@@@@@@@@||  ______  |
     \@@@@@@@@/ | |on|off| |
    __\@@@@@@/__|  ~~~~~~  |
   (____________|__________|
   |_______________________|


```

Then in the next steps each screen will guide you

each screen is a guide for a line or a section of the config file.


```bash
###########################################################
#
#        Cursor Line and Column
#
#   set cursorline    [x]    - use space bar to select
#   set cursorcolumn  [x]
#
#  Please choose which cursor lines you want to be ren-
#  derred.
#
#  Cursor lines are special markers on screen as shown
#  in ....
#                                 [enter or -> for next]
#
#  Stats:
#    - 56% of users set this options to `true`
#    - This option is popular among Python developers
#    - This is useful for selections in Visual Column Mode
#
###########################################################
```

`cm` is going to show a screen for each section of the
config file and at the end will generate the file
and ask the user if wants to change its save location.

`cm` will always backup existing file if found.

## Templates

Templates are YAML files containing global variables
and templates for each option `also called drops`.


`nvim.yaml`
```yaml
---
cm: 0.1.0
defaults:
  output_path: "$XDG_HOME/.config/nvim/init.vim"
drops:
  - name: Cursor Line and Column
    spaced: true
    options:
      - "set cursorline   {flag}"
      - "set cursorcolumn {flag}"
    outputs:
      - "set cursorline"
      - "set cursorcolumn"
    help: Cursor lines are special markers on screen as shown in ...

  - name: Allow hidden buffers
    spaced: false
    options:
      - "set hidden {flag}"
    outputs:
      - "set hidden"
    help: Enables the closing of buffers without saving it.

```

Multiple templates can be merged and composed.




