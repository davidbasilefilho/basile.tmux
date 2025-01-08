



# basile.tmux - `tmux` config

This is my configuration for `tmux`. I just use the basic features and some plugins to make it more useful and readable. It's is WIP, so I'll update it as I find new features and plugins.


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

set -g mouse on

setw -g mode-keys vi
bind-key h select-pane -L
bind-key j select-pane -D
bind-key k select-pane -U
bind-key l select-pane -R
bind-key -r C-h select-window -t :-
bind-key -r C-l select-window -t :+
```


### Catppuccin and status bar

Install and setup [Catppuccin](https://catppuccin.com/) and its status bar options.

```tmux
set -g @plugin 'catppuccin/tmux#v2.1.2'
set -g @catppuccin_flavor 'macchiato' # latte, frappe, macchiato or mocha
set -g @catppuccin_window_status_style "rounded"

set -g status-position top
set -g status-right-length 100
set -g status-left-length 100
set -g status-left ""
set -g status-right "#{E:@catppuccin_status_application}"
set -agF status-right "#{E:@catppuccin_status_cpu}"
set -ag status-right "#{E:@catppuccin_status_session}"
set -ag status-right "#{E:@catppuccin_status_uptime}"
```

```tmux
set -g @plugin 'tmux-plugins/tpm'

run '~/.tmux/plugins/tpm/tpm'
```
