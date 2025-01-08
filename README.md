



# basile.tmux - `tmux` config

This is my configuration for `tmux`. I just use the basic features and some plugins to make it more useful and readable. It's still WIP, so I'll update it as I find new features and plugins.


## Dependencies

- `tmux`
- `tpm`
- `stow`
- `git`


## Installation

Run this command to install the config and `tpm`:

```bash
git clone https://github.com/davidbasilefilho/tmux ~/tmux
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
cd ~/tmux
stow .
```


## Configuration

The configuration file is located at `~/.tmux.conf`.


### Fix terminal colors for Windows Terminal

```tmux
set-option -ga terminal-overrides ",xterm-256color:Tc"
set -g default-terminal "tmux-256color"
```


### Basic binds

Bind leader, add reload config binding, enable mouse support for resizing panes, and add vim keys for navigating.

```tmux
set -g prefix2 C-s

unbind r
bind r source-file ~/.tmux.conf

set-option -g base-index 1 # start window from 1

set -g mouse on

setw -g mode-keys vi

bind-key -n M-K swap-pane -U
bind-key -n M-J swap-pane -D

bind-key -n M-h resize-pane -L 5
bind-key -n M-j resize-pane -D 5
bind-key -n M-k resize-pane -U 5
bind-key -n M-l resize-pane -R 5

unbind %
unbind '"'
unbind p

bind-key p switch-client -T p-table
bind-key -T p-table v split-window -h
bind-key -T p-table h split-window -v
bind-key -T p-table l list-sessions

unbind w
bind w switch-client -T w-table
bind-key -T w-table n new-window
bind-key -T w-table l list-windows
bind-key -T w-table r command-prompt "rename-window '%%'"
```


### `vim-tmux-navigator`

Seemlessly navigate between vim and tmux!

```tmux
set -g @plugin 'christoomey/vim-tmux-navigator'
```


### Catppuccin and status bar

Install and setup [Catppuccin](https://catppuccin.com/) and its status bar options.

```tmux
set -g @plugin 'catppuccin/tmux#v2.1.2'
set -g @catppuccin_flavor 'macchiato' # latte, frappe, macchiato or mocha
set -g @catppuccin_window_status_style "rounded"

set -g status-position top
set -g status-right-length 100
set -ogq @catppuccin_status_connect_separator "no"
set -g status-left-length 100
set -g status-left ""
set -ogq @catppuccin_status_right_separator "\ue0b4"

set -g status-right "#{E:@catppuccin_status_application} "
set -ag status-right "#{E:@catppuccin_status_session} "
set -ag status-right "#{E:@catppuccin_status_uptime}"
```


### `tmux-sensible`

A set of options that make tmux more pleasant to use.
```tmux
set -g @plugin 'tmux-plugins/tmux-sensible'
```


### `tmux-resurrect`

Save and restore tmux environment.
```tmux
set -g @plugin 'tmux-plugins/tmux-resurrect'
set -g @resurrect-strategy-nvim 'session'
set -g @resurrect-capture-pane-contents 'on'
```


### Setup `tpm`

Add the `tpm` plugin manager to the config.

```tmux
set -g @plugin 'tmux-plugins/tpm'
run '~/.tmux/plugins/tpm/tpm'
```
