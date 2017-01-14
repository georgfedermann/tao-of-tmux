# Status bar {#status-bar}

The status bar, or *status line* lies in the bottom of the screen. It is
typically customize through the [tmux.conf config](#config).

I> *Finding your current status line settings* 
I>
I> {language=shell, line-numbers=off}
I>     $ tmux show-options -g | grep status

The status line is compromised of 3 sections. The status fields on either side
of the status line are customizable. The center field is a window list.

The `status-left` and `status-right` option can be configured to accept a
variety of variables.

## The symbology behind windows

The center part of the status line contains a list of windows, each of which can
be followed by a symbol:

| Symbol | Meaning                                                          |
|--------|------------------------------------------------------------------|
| *      | Denotes the current window.                                      |
| -      | Marks the last window (previously selected).                     |
| #      | Window is monitored and activity has been detected.              |
| !      | A bell has occurred in the window.                               |
| ~      | The window has been silent for the monitor-silence interval.     |
| M      | The window contains the marked pane.                             |
| Z      | The window's active pane is zoomed.                              |

## Customizing the left and right fields

### Variables

### External Calls

You can also call applications such as [tmux-mem-cpu-load](https://github.com/thewtex/tmux-mem-cpu-load).

## Turn your status line off

Turn it off:

{language=shell, line-numbers=off}
    $ tmux set-option status off

Turn it on:

{language=shell, line-numbers=off}
    $ tmux set-option status on

Toggle it (regardless or current state):

{language=shell, line-numbers=off}
    $ tmux set-option status

Bind toggling status line to `Prefix` + `q`:

{language=shell, line-numbers=off}
    $ tmux bind-key q set-option status

## Example: default config

![](images/status-line/default.png)

{line-numbers=off}
    status on
    status-interval 15
    status-justify left
    status-keys vi
    status-left "[#S] "
    status-left-length 10
    status-left-style default
    status-position bottom
    status-right " "#{=21:pane_title}" %H:%M %d-%b-%y"
    status-right-length 40
    status-right-style default
    status-style fg=black,bg=green

## Example: Dressed up

![](images/status-line/dressed up.png)

{line-numbers=off}
    status on
    status-interval 1
    status-justify centre
    status-keys vi
    status-left "#[fg=green]#H #[fg=black]• #[fg=green,bright]#(uname -r | cut -c 1-6)#[default]"
    status-left-length 20
    status-left-style default
    status-position bottom
    status-right "#[fg=green,bg=default,bright]#(tmux-mem-cpu-load) #[fg=red,dim,bg=default]#(uptime | cut -f 4-5 -d " " | cut -f 1 -d ",") #[fg=white,bg=default]%a%l:%M:%S %p#[default] #[fg=blue]%Y-%m-%d"
    status-right-length 140
    status-right-style default
    status-style fg=colour136,bg=colour235

Configs can print the output of an application. In this example,
[tmux-mem-cpu-load](https://github.com/thewtex/tmux-mem-cpu-load) is providing
system statistics in the right side section of the status line.

Source: <https://github.com/tony/tmux-config>