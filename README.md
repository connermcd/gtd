# gtd
> A simple shell script for effective time management.

## Flags

    -b : start on a break
    -c : custom command (defaults to "clear")
    -m : toggle MPD on change
    -n : notify on change
    -s : speak command
    -t : show time in tmux status bar
    -e : specify time to end at (e.g. 2:45pm today)
    -f : specify a configuration file

## Usage

    gtd [ -bcmnst ] [ work length ] [ break length ]

Basically it loops infinitely between periods of work and breaks. For example...

    gtd -s 25

Will start a loop with 25 minute periods of work separated by 5 minute breaks. If you give it the `-b` flag then it starts on a break instead of a working period.

If you don't specify a break length, the script automatically determines how long breaks should be depending on how long you want your working periods to be. I usually use either 25 or 15 minute working periods depending on my mood. The basic formula it uses is just integer division divided by 5. So 25 minute periods have 5 minute breaks and 15 minute periods have 3 minute breaks. An 11 minute period will have a 2 minute break since 11/5 = 2.2 ≈ 2.

## Configuration

The `-c`, `-m`, `-n`, `-s` and `-t` flags use commands. The `-m` flag uses `mpc toggle` to toggle your mpd client and the `-n` flag uses libnotify to notify when the period ends. The `-s` flag enables `espeak` to speak to you when the period changes. The `-c` flag uses a custom command, which is `clear` by default. The `-t` flag refreshes tmux and updates `/tmp/gtd` with the time status so that it can be read by tmux. Just read the file somewhere in your `tmux.conf` status bar configuration somewhere. For example:

    set-option -g status-right "#(cat /tmp/gtd)#[fg=colour15,noreverse,bg=colour233] #(date '+%a %m/%d %I:%M %P') "

If you have the `at` command you can use its syntax to specify an end time with the `-e` flag. For example:

    gtd -e "10:45pm today"

This will stop the script at 10:45pm today. See `man at` for more syntax options.

The script is easily modifiable to use custom programs or commands if you'd rather not use the defaults. The one exception to this is the `tmux` integration. For the others, simply set the appropriate variable when starting or in the file `~/.gtdrc`. You can use the `-f` flag if you'd like to use a different file. The configurable variables are provided below. If you use a flag after setting a boolean variable to true it will toggle it, turning it off.

    CUSTOM_CMD="clear"
    MPD_CMD="mpc -q toggle"
    NOTIFY_CMD="notify-send"
    SPEAK_CMD="&>/dev/null espeak"

    DEFAULT_WORK_LENGTH=${DEFAULT_WORK_LENGTH:-15}
    NOTIFY_WORK="\"Get things done.\""
    NOTIFY_BREAK="\"Take a break.\""
    SPEAK_WORK="$NOTIFY_WORK"
    SPEAK_BREAK="$NOTIFY_BREAK"

    # Set these to "true" to change the default
    DO_BREAK=
    DO_CUSTOM_CMD=
    DO_MPD=
    DO_NOTIFY=
    DO_SPEAK=
    DO_TMUX=

## MIT License

Copyright (C) 2013 copyright holder

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the "Software"),
to deal in the Software without restriction, including without limitation
the rights to use, copy, modify, merge, publish, distribute, sublicense,
and/or sell copies of the Software, and to permit persons to whom the 
Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included
in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES
OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM,
DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE
OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
