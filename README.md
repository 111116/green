GREEN - A light weight PDF reader
=======================================

Green - a lightweight PDF reader for the Framebuffer using libpoppler

This is a slightly modified version.  
original version: [schandinat/green](https://github.com/schandinat/green)


DESCRIPTION
-----------

*green* is meant to be a light PDF reader for the Linux Framebuffer. 
However, it can also be used inside a graphical X11 Session like GNOME or
MATE. 

*green* features:

 - uses libpoppler for PDF reading
 - uses SDL to support various frontends (including framebuffer)
 - multiple documents
 - vim-styled movements
 - searching & zooming
 - scheme support
 
INSTALLATION
------------

### Dependencies:
- C Compiler
- GNU make or similar
- libpoppler (including development files)
- libSDL (including devopment files)


### Ubuntu installation:

    sudo apt-get install libpoppler-glib-dev libsdl1.2-dev
    git clone https://github.com/111116/green
    cd green
    make

### NOTE:  
The Makefile installation currently may NOT be working correctly.  
To manually install this program **after compilation**, run the following commands:

    sudo install green /usr/bin/
    sudo install green.1 /usr/share/man/man1/


USAGE
--------

    green [options] <PDF file 1> [PDF file 2] ...


### example:

    green -nomouse example.pdf
    green -help
    greep -v


OPTIONS
-------

`-width=` 
    with an integer greate equal zero (in pixels) to specify the startup width of the window.  
`-height=` 
    with an integer greate equal zero (in pixels) to specify the startup height of the window.  
`-fullscreen`
    startup in fullscreen mode.  
`-nofullscreen`
    startup in window mode.  
`-config=`
    with a file name of a configuration file.  
`-scheme=`
    with an `<id list>` (see below) to select a different scheme.  
`-zoomstep=<fraction>`
    to specify zooming step (e.g. 1/8)  
`-step=<fraction>`
    to specify scrolling step (e.g. 1/8)  
`-nomouse`
    disable mouse  
`-help`
    shows this help  
`-version`
    displays version information  
  

PROGRAM OPERATION
------------------
`<ESC>` - Escape current input mode.   
`q` - Quit

### SCROLLING
`h, <left>` - Scroll left.  
`l, <right>` - Scroll right.  
`j, <down>` - Scroll down.  
`k, <up>` - Scroll up.  
`<CTRL-u>` - Scroll up a half screen.  
`<CTRL-d>` - Scroll down a half screen.  
`<pageup>, <backspace>` - Scroll up a whole screen.  
`<pagedown>, <space>` - Scroll down a whole screen.  

### NAVIGATION
`H, K` - Go to previous page.  
`J, L` - Go to next page.  
`g` - Go to first page of document.  
`G` - Go to last page of document.  
`:<n><RETURN>` - Go to page n.  

`P, <SHIFT-TAB>` - Go to previous document.  
`N, <TAB>` - Go to next document.  
`c` - close current document.  
`f1` to `f12` - Goto n-th document.
`r` - Rotate clockwise.


### FITTING
`+` - Zoom in.  
`-` - Zoom out.  
`w` - fit page width.  
`f` - fit page height.  

### SEARCHING 
`(/ or CTRL-f)<X><RETURN>` - Start search for string *X*.  
`n` - Show next result.

### OTHER STUFF
When starting green in Framebuffer console you might see an error regarding the mouse. 
If you don't need mouse in the console:

    SDL_NOMOUSE=1 ./green 

Should work around the problem. Other wise you should be able to use the mouse in the 
Framebuffer as none root user. 
On Debian based distributions:

Create new file `/etc/udev/rules.d/99-input.rules`:

    # file /etc/udev/rules.d/99-input.rules
    KERNEL=="mice", NAME="input/%k", MODE="664", GROUP="input"
    KERNEL=="mouse*", NAME="input/%k", MODE="664", GROUP="input"

Then issue:
    
    groupadd input
    usermod -a -G input [your_username]

Restart your computer and you should be able to use the mouse with SDL. 

FILES
-----
*$(HOME)/.green.conf*     
  Per user configuration file.  

*/usr/local/etc/green.conf*  
  The system wide configuration file.   
  
**example config:**  

    # file ~/.green.conf
    SCHEME normal
    {
    	Background.Color = darkgray
    	Mouse = 0
    }
    DEFAULT_SCHEME normal



ORIGINAL AUTHOR
------
The original Green source code may be downloaded from <http://github.com/schandinat/green/>.   
Green is Licensed under GNU GPL version 3.  
This man page was written for the Debian GNU / Linux System by Oz Nahum <nahumoz@gmail.com>.

