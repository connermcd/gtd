# gtd
> A simple shell script for effective time management.

## Flags

    -b : start on a break
    -c : custom command (defaults to "clear")
    -m : toggle MPD on change
    -n : notify on change
    -s : speak command

## Usage

    gtd [ -bcmns ] [# of minutes]

Basically it loops infinitely between periods of work and breaks. For example...

    gtd -s 25

Will start a loop with 25 minute periods of work separated by 5 minute breaks. If you give it the `-b` flag then it starts on a break instead of a working period.

The `-m` and `-n` flags are enabled by default. They use `mpc toggle` to toggle your mpd client and libnotify to notify when the period ends. The `-s` flag enables `espeak` to speak to you when the period changes. You can configure all of this within the script.

The script automatically determines how long breaks should be depending on how long you want your working periods to be. I usually use either 25 or 15 minute working periods depending on my mood. The basic formula it uses is just integer division divided by 5. So 25 minute periods have 5 minute breaks and 15 minute periods have 3 minute breaks. An 11 minute period will have a 2 minute break since 11/5 = 2.2 ≈ 2.

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
