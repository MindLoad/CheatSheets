---
Title: Tmux
Date: 31.07.2023
Time: 12:19
Tags: [cheatsheet, config]
---

`cmd`:  `CTRL + Space`

### Windows & Panes

| command                             | description                 |
| ----------------------------------- | --------------------------- |
| tmux new -s `session name`          | new session with name       |
| tmux kill-ses -t `session name`     | kill session with name      |
| tmux kill-session -a                | kill all sessions           |
| cmd + d                             | detach from session         |
| tmux ls                             | list sessions               |
| tmux a                              | attach to session           |
| tmux a -t `session name`            | attach to session by name   |
| cmd + w                             | list windows                |
| cmd + c                             | create new window           |
| cmd + &                             | close current window        |
| cmd + 0...9                         | select window by index      |
| cmd + %                             | split with hor.layout       |
| cmd + "                             | split with vert.layout      |
| cmd + up,down,left,right            | switch to pane by direction |
| cmd + !                             | convert pane into window    |
| cmd + (up,down,left,right)(holding) | resize pane                 |
| cmd + x                             | close current pane          |
|                                     |                             |

### Copy mode

| command   | description             |
| --------- | ----------------------- |
| cmd + \[  | Enter copy mode         |
| v         | Start select by symbols |
| Shift + v | Start selecty by lines  |
| y   | Yank selected text      |
| cmd + \]  | Paste content of buffer |


### Command mode

| **command**          | **description**                    |
| -------------------- | ---------------------------------- |
| cmd + :              | Enter command mode                 |
| :show-buffer         | display buffer_0 content           |
| :capture-pane        | Copy entire pane content to buffer |
| :list-buffers        | Show all buffers                   |
| :save-buffer buf.txt | Save buffer content to buf.txt     |
| :delete-buffer -b 1  | delete buffer_1                    |
| :list-keys           | List key bindings (shortcuts)                                   |


### Tmux config

```bash
set-option -sa terminal-overrides ",xterm*:Tc"
set -g mouse on

# Set Prefix
unbind C-b
set -g prefix C-Space
bind C-Space send-prefix

# Set windows and panes at 1
set -g base-index 1
set -g pane-base-index 1
set-window-option -g pane-base-index 1
set-option -g renumber-windows on

# Use Alt-arrow keys without prefix key to switch panes
bind -n M-Left select-pane -L
bind -n M-Right select-pane -R
bind -n M-Up select-pane -U
bind -n M-Down select-pane -D

# List of plugins
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'
set -g @plugin 'catppuccin/tmux'
set -g @plugin 'tmux-plugins/tmux-yank'

# Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
run '~/.tmux/plugins/tpm/tpm'

# set vi-mode
set-window-option -g mode-keys vi
# keybindings
bind-key -T copy-mode-vi v send-keys -X begin-selection
bind-key -T copy-mode-vi C-v send-keys -X rectangle-toggle
bind-key -T copy-mode-vi y send-keys -X copy-selection-and-cancel

# Open panes in current directory
bind '"' split-window -v -c "#{pane_current_path}"
bind % split-window -h -c "#{pane_current_path}"
```

