# vscode-vim-configs

My custom VSCODE Vim config settings

You can create custom mappings using Visual Studio Code preferences:

1.  Open the command palette with **`CMD-SHIFT-P`** or **`CTRL-SHIFT-P`**
2.  Type preferences
3.  Select the Preferences: **`Open User Settings JSON`**
4.  Type **`vim`**

And you’ll filter your Visual Studio Code preferences to display only VSCodeVim related ones. Now you can use the following settings to add your custom mappings in different modes:

- _Normal Mode Key Bindings Non Recursive_ - for normal mode
- *Visual Mode Key Bindings Non Recursive* - for visual mode
- *Insert Mode Key Bindings Non Recursive* - for insert mode

A custom mapping normally takes the following shape:

```json
{
  "vim.insertModeKeyBindingsNonRecursive": [
    {
      "before": ["j", "k"],
      "after": ["<ESC>"]
    }
  ]
}
```

- **before** is the sequence of commands that you type.
- **after** is what the previous commands map to and what gets executed when you type them.

In the example above, whenever we type the sequence **`jk`** in *Insert Mode* it will be the equivalent of typing **`<ESC>`** and therefore it will bring us back to *Normal mode*. This is a great custom mapping that makes a very common task seamless, since both **`j`** and **`k`** are in the home row and just underneath your right hand.

# My Custom Vim configs:

```json
  //
  // VSCODE Vim settings
  //

  // change the default vim leader settings from '\' to '<Space>'
  "vim.leader": "<Space>",

  // Vim-sneak is a middle ground between character search (inside a line) and pattern search (inside a file):
  // Type s{char}{char} and the cursor flies to the first occurrence of that two character sequence. From then on type ; for the next occurrence, or , for the previous one. S{char}{char} works in a similar fashion but backwards.
  // Type {operator}z{char}{char} and the operator will be applied over the text traversed by the sneak motion.
  "vim.sneak": true,

  // Vim-EasyMotion tries to simplify the use of motions in Vim by removing the need for counts.
  // when you trigger a motion with EasyMotion, it labels the possible targets in the whole document with a key combination that is shown in an overlay (over the text in question). Type that key combination, and you’re teleported to that location at once.
  "vim.easymotion": true,

  // Vim Insert Mode Key Bindings Non Recursive for custom key mappings
  "vim.insertModeKeyBindingsNonRecursive": [
    // for switching between insert mode & normal mode easily
    {
      "before": ["j", "k"],
      "after": ["<ESC>"]
    }
  ],

  // Vim Normal Mode Key Bindings Non Recursive for custom key mappings
  "vim.normalModeKeyBindingsNonRecursive": [
    // moving up and down faster in normal mode using 'J' & 'K' instead of just 'j' & 'k'
    {
      "before": ["J"],
      "after": ["5", "j"]
    },
    {
      "before": ["K"],
      "after": ["5", "k"]
    },

    // we've overwritten two Vim default bindings above J (join lines), although useful, is something that you do only from time to time. K is used for keyword search but isn’t yet implemented in VSCodeVim
    // so we'll remap joining lines(j) using the '<leader>' key i.e. '<Space>'
    {
      "before": ["<Leader>", "j"],
      "after": ["J"]
    },

    // For easier switching between split windows Using 'CTRL + h or j or k or l' for 'left or down or up or right' split window
    {
      "before": ["<C-h>"],
      "after": ["<C-w>", "h"]
    },
    {
      "before": ["<C-j>"],
      "after": ["<C-w>", "j"]
    },
    {
      "before": ["<C-k>"],
      "after": ["<C-w>", "k"]
    },
    {
      "before": ["<C-l>"],
      "after": ["<C-w>", "l"]
    },

    // For easier tab handling & switching between different tabs inside a split window
    // Instead of using before and after. We use before and commands. commands represent either the Ex commands or Visual Studio native commands that should be run whenever we type the key mapping defined by before.
    {
      "before": ["<Leader>", "t", "t"],
      "commands": [":tabnew"]
    },

    {
      "before": ["<Leader>", "t", "n"],
      "commands": [":tabnext"]
    },
    {
      "before": ["<Leader>", "t", "p"],
      "commands": [":tabprev"]
    },
    {
      "before": ["<Leader>", "t", "o"],
      "commands": [":tabo"]
    },

    // For cleaning highlight for text after Searching for a pattern using '/{pattern}' or '?{pattern}'
    {
      "before": ["<Leader>", "/"],
      "commands": [":noh"]
    },

    // For saving a file using <leader>w by triggering VSCode "workbench.action.files.save" action.
    // Instead of using before and after. We use before and commands. commands represent either the Ex commands or Visual Studio native commands that should be run whenever we type the key mapping defined by before.
    {
      "before": ["leader", "w"],
      "commands": ["workbench.action.files.save"]
    },

    // For opening the command palette(CTRL+SHIFT+P) or go to symbol(CTRL+SHIFT+O) type <Leader>p and <Leader>t respectively and you’ll quickly access either of these panels.
    {
      "before": ["<Leader>", "p"],
      "commands": ["workbench.action.showCommands"]
    },
    {
      "before": ["<Leader>", "t"],
      "commands": ["workbench.action.gotoSymbol"]
    }
  ]
```
