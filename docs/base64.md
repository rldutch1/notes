#Base 64
<pre>
Source: https://ioflood.com/blog/base64-linux-command/
Using single-quotes around the data that is being encoded seems to produce the expected output. I got different results using double-quotes.
	<span style="color: #3366ff;">
	echo 'This is a text with some #$@% non-alphabet characters.' | base64 -i
	echo 'VGhpcyBpcyBhIHRleHQgd2l0aCBzb21lICMkQCUgbm9uLWFscGhhYmV0IGNoYXJhY3RlcnMuCg==' | base64 -d
	</span>

Large files:
	<span style="color: #3366ff;">base64 -w 0 large_file.txt > encoded_file.txt</span>
</pre>


