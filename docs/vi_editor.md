#### Write specific lines from a file to a new file.
```
Example to write lines 230 through 300 to a new file:
:230,300w filename.txt
```
<pre>General Startup
	To use vi: <span style="color: #3366ff;">vi filename</span>
	To exit vi and save changes: <span style="color: #3366ff;">ZZ</span>   or  <span style="color: #3366ff;">:wq</span>
	To exit vi without saving changes: <span style="color: #3366ff;">:q!</span>
	To enter vi command mode: <span style="color: #3366ff;">[esc]</span>

Counts
        A number preceding any vi command tells vi to repeat
	that command that many times.

Cursor Movement

	<span style="color: #3366ff;">h</span>       move left (backspace)

	<span style="color: #3366ff;">j</span>       move down

	<span style="color: #3366ff;">k</span>       move up

	<span style="color: #3366ff;">l</span>       move right (spacebar)

	<span style="color: #3366ff;">[return]</span>   move to the beginning of the next line

	<span style="color: #3366ff;">$</span>       last column on the current line

	<span style="color: #3366ff;">0</span>       move cursor to the first column on the
		current line

	<span style="color: #3366ff;">^</span>       move cursor to first nonblank column on the
		current line

	<span style="color: #3366ff;">w</span>       move to the beginning of the next word or
		punctuation mark

	<span style="color: #3366ff;">W</span>       move past the next space

	<span style="color: #3366ff;">b</span>       move to the beginning of the previous word
		or punctuation mark

	<span style="color: #3366ff;">B</span>       move to the beginning of the previous word,
		ignores punctuation

        <span style="color: #3366ff;">e</span>       end of next word or punctuation mark

        <span style="color: #3366ff;">E</span>       end of next word, ignoring punctuation

        <span style="color: #3366ff;">H</span>       move cursor to the top of the screen 

        <span style="color: #3366ff;">M</span>       move cursor to the middle of the screen

        <span style="color: #3366ff;">L</span>       move cursor to the bottom of the screen 

Screen Movement

       <span style="color: #3366ff;">G</span>        move to the last line in the file

       <span style="color: #3366ff;">xG</span>       move to line x

       <span style="color: #3366ff;">z+</span>       move current line to top of screen

       <span style="color: #3366ff;">z</span>        move current line to the middle of screen

       <span style="color: #3366ff;">z-</span>       move current line to the bottom of screen

       <span style="color: #3366ff;">^F</span>       move forward one screen

       <span style="color: #3366ff;">^B</span>       move backward one line

       <span style="color: #3366ff;">^D</span>       move forward one half screen

       <span style="color: #3366ff;">^U</span>       move backward one half screen

       <span style="color: #3366ff;">^R</span>       redraw screen
		( does not work with VT100 type terminals )

       <span style="color: #3366ff;">^L</span>       redraw screen
		( does not work with Televideo terminals )

Inserting

       <span style="color: #3366ff;">r</span>        replace character under cursor with next
		character typed

       <span style="color: #3366ff;">R</span>        keep replacing character until [esc] is hit

       <span style="color: #3366ff;">i</span>        insert before cursor

       <span style="color: #3366ff;">a</span>        append after cursor

       <span style="color: #3366ff;">A</span>        append at end of line

       <span style="color: #3366ff;">O</span>        open line above cursor and enter append mode

Deleting

	<span style="color: #3366ff;">x</span>       delete character under cursor

	<span style="color: #3366ff;">dd</span>      delete line under cursor

        <span style="color: #3366ff;">dw</span>      delete word under cursor

        <span style="color: #3366ff;">db</span>      delete word before cursor

Copying Code

        <span style="color: #3366ff;">yy</span>      (yank)'copies' line which may then be put by
		the p(put) command. Precede with a count for
		multiple lines.

        <span style="color: #3366ff;">:t.</span>     will duplicate the line.

        <span style="color: #3366ff;">:t 7</span>    will copy it after line 7.

        <span style="color: #3366ff;">:,+t0</span>   will copy current and next line at the
        beginning of the file.

        <span style="color: #3366ff;">:1,t$</span>   will copy lines from beginning of the file
        to the current cursor position, to the end of the file.

Put Command
        brings back previous deletion or yank of lines,
	words, or characters

        <span style="color: #3366ff;">P</span>       bring back before cursor

        <span style="color: #3366ff;">p</span>       bring back after cursor

Find Commands

	<span style="color: #3366ff;">?</span>       finds a word going backwards

	<span style="color: #3366ff;">/</span>       finds a word going forwards

        <span style="color: #3366ff;">f</span>       finds a character on the line under the
		cursor going forward

        <span style="color: #3366ff;">F</span>       finds a character on the line under the
		cursor going backwards

        <span style="color: #3366ff;">t</span>       find a character on the current line going
		forward and stop one character before it

	<span style="color: #3366ff;">T</span>       find a character on the current line going
		backward and stop one character before it

	<span style="color: #3366ff;">;</span>	repeat last f, F, t, T

Find and Replace Commands

        <span style="color: #3366ff;">:%s/hello/goodbye/g</span>   find hello and replace with goodbye

        <span style="color: #3366ff;">:%s/^\(.*\)\n\1$/g</span>    delete duplicate lines

        <span style="color: #3366ff;">:%s/\n/ /g</span>            join lines together

Miscellaneous Commands

	<span style="color: #3366ff;">.</span>	repeat last command

	<span style="color: #3366ff;">u</span>	undo last command issued

	<span style="color: #3366ff;">U</span>	undoes all commands on one line

	<span style="color: #3366ff;">xp</span>	deletes first character and inserts after
		second (swap)

	<span style="color: #3366ff;">J</span>	join current line with the next line

	<span style="color: #3366ff;">^G</span>	display current line number

	<span style="color: #3366ff;">%</span>	if at one parenthesis, will jump to its mate

	<span style="color: #3366ff;">mx</span>	mark current line with character x

	<span style="color: #3366ff;">'x</span>	find line marked with character x

	NOTE: Marks are internal and not written to the file.

Line Editor Mode
	Any commands from the line editor ex can be issued
	upon entering line mode.

	To enter: type '<span style="color: #3366ff;">:</span>'

	To exit: press<span style="color: #3366ff;">[return]</span> or <span style="color: #3366ff;">[esc]</span>

ex Commands
	For a complete list consult the
	UNIX Programmer's Manual

READING FILES
	copies (reads) filename after cursor in file
	currently editing

	<span style="color: #3366ff;">:r filename</span>

WRITE FILE
	<span style="color: #3366ff;">:w</span> 	saves the current file without quitting
	<span style="color: #3366ff;">:20,40w filename</span> write the contents of the lines numbered 20 through 40 to
	a new file named filename
MOVING

	<span style="color: #3366ff;">:#</span>	move to line #

	<span style="color: #3366ff;">:$</span>	move to last line of file

SHELL ESCAPE
	executes 'cmd' as a shell command.

	<span style="color: #3366ff;">:!'cmd'</span>

<a title="Source" href="http://www.cs.rit.edu/~cslab/vi.html" target="_blank">Source</a>:</pre> 