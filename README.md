# Convert-HTML-to-Wiki-with-SED-and-Regex
Convert HTML formatted README files and Documentation into properly formatted Wiki Documents with a single line via the Command Line Tool. 

= Sed Overview =

$ matches the end of a line
^ matches the start of a line
* matches zero or more occurrences of the previous character
[ ] any characters within the brackets will be matched

== General Examples ==
Replace word based on subset of letters:

For example, you could change any instance of the words "cat", "can", and "car" to "dog" by using the following:
	 $ sed "s/ca[tnr]/dog/g" inputfile > outputfile

In the next example, the first [0-9] ensures that at least one digit must be present to be matched. The second [0-9] may be missing or may be present any number of times, because it is followed by the * metacharacter. Finally, the digits are removed because there is nothing between the second and third slashes where you can put your replacement text.
 	$ sed "s/[0-9][0-9]*//g" inputfile > outputfile

Inside an expression, if the first character is a caret (^), Sed matches only if the text is at the start of the line.
	$ echo dogs cats and dogs | sed "s/^dogs/doggy/"
	doggy cats and dogs

A dollar sign at the end of a pattern expression tells Sed to match the text only if it is at the end of the line.
	$ echo dogs cats and cats | sed "s/cats$/kitty/"
	dogs cats and kitty

A line changes only if the matching string is where you require it to be; if the same text occurs elsewhere in the sentence it is not be modified.


Sed can be passed more than one operation at a time. We can do this by specifying each pattern after an -e option.
	$ echo Gnus eat grass | sed -e "s/Gnus/Penguins/" -e "s/grass/fish/"
	Penguins eat fish.


== Example Test ==
Create textfile.txt in your directory
Add test file contents:

	this has foo then bar then foo then bar
	this has bar then foo then bar then foo

$ cat testfile
# Expected Output of File Contents
	this has foo then bar then foo then bar
	this has bar then foo then bar then foo

$ sed "s/foo/bar/g" testfile.txt > testfilechanged.txt
$ cat testchangedfile
# Expected Output of File Contents
	this has bar then bar then bar then bar
	this has bar then bar then bar then bar

More info [http://en.flossmanuals.net/command-line/sed/ here].	

	sed "s/<h1>/== /g" testfile.txt > testfilechanged.txt



== Scripting SED commands ==
By using the -f argument to the sed command, you can feed Sed a list of commands to run. For example, if you put the following patterns in a file called sedcommands:

	s/foo/bar/g
	s/dog/cat/g
	s/tree/house/g
	s/little/big/g

You can use this on a single file by entering the following:
	$ sed -f html2wiki.txt < wiki.html > wiki.txt

Find and Replace Tags with sed and regex
sed -e 's/<h1>/<h2>/g' -e 's_</h1>_</h2>_g'	

== Full command list for formatting Wiki ==

s:<h1>:= :g;s:</h1>: =:g
s:<h2>:== :g;s:</h2>: ==:g
s:<h3>:=== :g;s:</h3>: ===:g
s:<h4>:==== :g;s:</h4>: ====:g
s:<h5>:===== :g;s:</h5>: =====:g
s:<h6>:====== :g;s:</h6>: ======:g
s:<strong><em>:''''':g;s:</em></strong>:''''':g
s:<strong>:''':g;s:</strong>:''':g
s:<em>:'':g;s:</em>:'':g
s:<ul>::g;s:</ul>::g
s:<ol>::g;s:</ol>::g
s:<dl>:; :g;s:</dl>::g
s/<dd>/: /g;s:</dd>::g
s/<dt>/: /g;s:</dt>::g
s:<li>:* :g;s:</li>::g
s:<hr>:----:g
s:<br>: :g
s:	::g
s:<code>:    :g
s:</code>::g


