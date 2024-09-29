How do you disable a user account on a Mac?
You can disable a user account by setting their shell to /usr/bin/false. Either run: 
	<span style="color: #3366ff;">chsh -s /usr/bin/false <username></span>
	or change it in Users & Groups → Advanced Options. To change it back, 
	run <span style="color: #3366ff;">chsh -s /bin/bash <username></span> . It doesn't apply to GUI logins?

Another link:
[Link](https://apple.stackexchange.com/questions/135184/how-to-disable-account-on-os-x-mavericks#:~:text=You%20can%20disable%20a%20user,bin%2Fbash%20.&text=I%20was%20aware%20of%20this,also%20apply%20to%20GUI%20logins%3F)

The answer is given [here:](https://serverfault.com/questions/61214/how-can-i-disable-a-user-account-from-the-cli-with-mac-os-x-server#new-answer)

With details on hiding given [here:](https://support.apple.com/en-au/ht203998)

###pwpolicy can both disable and enable users, without losing their password

To disable the user
<span style="color: #3366ff;">pwpolicy -u username disableuser</span>

To enable the user
<span style="color: #3366ff;">pwpolicy -u username enableuser</span>

Use dscl to hide the user so they don't show on login:
<span style="color: #3366ff;">sudo dscl . create /Users/username IsHidden 1</span>

To show a hidden user
<span style="color: #3366ff;">sudo dscl . create /Users/username IsHidden 0</span>

More stuff to read [here:](https://serverfault.com/questions/61214/how-can-i-disable-a-user-account-from-the-cli-with-mac-os-x-server#new-answer)

Where to put custom executables on a Mac so they are globally visible:
<span style="color: #3366ff;">/usr/local/bin/</span>
