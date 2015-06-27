<h1># Convert-HTML-to-Wiki-with-SED-and-Regex</h1>
Convert HTML formatted README files and Documentation into properly formatted Wiki Documents with a single line via the Command Line Tool. 
  
<h2>Sed Overview</h2>
<blockquote>
  <ul>
    <li>$ matches the end of a line</li>
    <li>^ matches the start of a line</li>
    <li>* matches zero or more occurrences of the previous character</li>
    <li>[] any characters within the brackets will be matched</li>
  </ul>
</blockquote>

<h2>General Examples</h2>
Replace word based on subset of letters:

For example, you could change any instance of the words "cat", "can", and "car" to "dog" by using the following:
<blockquote>$ sed "s/ca[tnr]/dog/g" inputfile > outputfile</blockquote>

In the next example, the first [0-9] ensures that at least one digit must be present to be matched. The second [0-9] may be missing or may be present any number of times, because it is followed by the * metacharacter. Finally, the digits are removed because there is nothing between the second and third slashes where you can put your replacement text.
<blockquote>$ sed "s/[0-9][0-9]*//g" inputfile > outputfile</blockquote>

Inside an expression, if the first character is a caret (^), Sed matches only if the text is at the start of the line.
<blockquote>$ echo dogs cats and dogs | sed "s/^dogs/doggy/"</blockquote>
doggy cats and dogs

A dollar sign at the end of a pattern expression tells Sed to match the text only if it is at the end of the line.
<blockquote>$ echo dogs cats and cats | sed "s/cats$/kitty/"</blockquote>
dogs cats and kitty

A line changes only if the matching string is where you require it to be; if the same text occurs elsewhere in the sentence it is not be modified.


Sed can be passed more than one operation at a time. We can do this by specifying each pattern after an -e option.
<blockquote>$ echo Gnus eat grass | sed -e "s/Gnus/Penguins/" -e "s/grass/fish/"</blockquote>
Penguins eat fish.


<h2>Example Test</h2>
Create textfile.txt in your directory
Add test file contents:

<blockquote>this has foo then bar then foo then bar
this has bar then foo then bar then foo</blockquote>

<blockquote>$ cat testfile
# Expected Output of File Contents
this has foo then bar then foo then bar
this has bar then foo then bar then foo</blockquote>

<blockquote>$ sed "s/foo/bar/g" testfile.txt > testfilechanged.txt
$ cat testchangedfile
# Expected Output of File Contents
this has bar then bar then bar then bar
this has bar then bar then bar then bar</blockquote>

More info [http://en.flossmanuals.net/command-line/sed/ here].	

sed "s/<code><h1></code>/HEADER1/g" testfile.txt > testfilechanged.txt



<h2>Scripting SED commands</h2>
By using the -f argument to the sed command, you can feed Sed a list of commands to run. For example, if you put the following patterns in a file called sedcommands:

<blockquote>
s/foo/bar/g
s/dog/cat/g
s/tree/house/g
s/little/big/g
</blockquote>

You can use this on a single file by entering the following:
<blockquote>$ sed -f html2wiki.txt < wiki.html > wiki.txt</blockquote>
<blockquote>$ sed -f html2wiki.txt < README.html > README.md</blockquote>

Find and Replace Tags with sed and regex
sed -e 's/<code></h1><h1></code>/<h2>/g' -e 's_</h1>_</h2>_g'	

<h2>Full command list for formatting Wiki</h2>

<code>
s:<h1>:= :g;s:</h1>: =:g
s:<h2>:<h2>:g;s:</h2>:</h2>:g
s:<h3>:=<h2>:g;s:</h3>:</h2>=:g
s:<h4>:==<h2>:g;s:</h4>:</h2>==:g
s:<h5>:===<h2>:g;s:</h5>:</h2>===:g
s:<h6>:====<h2>:g;s:</h6>:</h2>====:g
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
</code>

