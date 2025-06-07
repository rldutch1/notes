#<h1>PGP:</h1>
- [The GNU Privacy Handbook](https://www.gnupg.org/gph/en/manual/book1.html/ "")
- [Archlinux Wiki GnuPG](https://wiki.archlinux.org/index.php/GnuPG/ "")
- [GnuPG Website](https://www.gnupg.org/ "")

###### Public [PGP Global Directory](http://keyserver1.pgp.com/ "PGP Key Server")

###### Youtube Videos:
- [GnuPG Part One](https://www.youtube.com/watch?v=IF-MchgZ2Os/ "")
- [GnuPG Part Two](https://www.youtube.com/watch?v=R-Dw7UXH00c/ "")
- [GnuPG Part Three](https://www.youtube.com/watch?v=JOBJPwyByyI/ "")
- [NITC-GnuPG Part 3](https://www.youtube.com/watch?v=xAGfWyNgi2Q/ "")

#### Generate/Create GPG/PGP Key:
	gpg2 --full-gen-key
	gpg --gen-key

	Versions older than 2.1.17 use:
	gpg --default-new-key-algo rsa4096 --gen-key

#### Change your password if you want to:
	gpg --edit-key YourKeyID
	Then type: passwd


#### Send key to default key server:
	  gpg --send-key KEYNAME
	  gpg --export your_address@example.net | curl -T - https://keys.openpgp.org
	  gpg --export your_address@example.net > my_key.pub

	 	You can upload your key to this PGP site: https://keyserver.pgp.com
	 	You can check if your key is on the PGP website here: https://keyserver.pgp.com

#### To send your public key to a keyserver:

	gpg --keyserver the.keyserver.name.com --send-keys YOURKEYID
	Example: gpg --keyserver keyserver.ubuntu.com --send-keys 5DD98B3E
	Example: gpg --keyserver hkp://pgp.mit.edu --send-keys YOURKEYID
	Example: gpg --keyserver hkps.pool.sks-keyservers.net --send-keys YOURKEYID

#### To receive a public key from a keyserver:

	Example: gpg --keyserver the.keyserver.name.com --recv-keys THEKEYID
	Example: gpg --keyserver keyserver.ubuntu.com --recv-keys 5DD98B3E


#### To locate the key of a user, by email address:
	  Example: gpg --auto-key-locate keyserver --locate-keys user@example.net

#### To refresh all your keys (e.g. new revocation certificates and subkeys):
	  Example: gpg --refresh-keys

#### Export ascii armored key:
	  gpg --export --armor jqdoe@example.com > jqdoe-pubkey.asc
	  gpg --export-secret-keys --armor jqdoe@example.com >> jqdoe-privkey.asc
	  Use a double greater than symbol to export both public and private to the same file ">>".

#### Encrypt a message to standard output:
		gpg -ea
  Enter your recipients and end with an empty line.
  Type your message that you want to encrypt.
  Press Control+D and your encrypted message will appear onscreen.

###### Encrypt message to a file you can type:

	gpg -ea > filename.txt

  then do the steps above.
  Enter your recipients and end with an empty line.
  Type your message that you want to encrypt.
  Press Control+D and your encrypted message will be sent to filename.txt.

###### Encrypt a single file (creates a binary file). This option may be combined with --sign.

 	gpg -e filename

 	or

 	gpg --encrypt filename

###### Encrypt a single file (creates an ASCII file). This option may be combined with --sign.

	gpg -a -e filename

	or

	gpg --armor --encrypt filename

	or

	gpg -ea filename

This is a special version of the --encrypt command. The command expects the files to be encrypted either on the command line or reads the filenames from stdin; each name must be on separate line. The command is intended for a quick encryption of multiple files.

#### Encrypt multiple files. This option may be combined with --sign.

	This will prompt you for your password for each file.
 	gpg --encrypt-files file1 file2 file3

 	or add a recipient (your own key) to not be prompted.
	gpg --encrypt-files -r A1B2C3D4E5F6 *.txt


###### Batch encrypt using --multi-file:

	gpg --multifile --encrypt --armor -r brothers *.txtrh

###### Bash script to batch encrypt multiple files:

	for file in *.txtrh
	do
	#	echo "gpg --encrypt --armor -r 7FEBFF2F6AB4F024 -r D1BD917D4AF9F0EC" > ~/"$file"
	#	gpg --encrypt --armor -r 7FEBFF2F6AB4F024 -r D1BD917D4AF9F0EC "$file"
		gpg --encrypt --armor -r brothers "$file"
	#	echo "============== $file"
	done


###### Encrypt with symmetric cipher only. This command asks for a passphrase. (May also be combined with --sign -- see GnuPG 1.0.7 released.)

 	gpg -c filename

 	or

 	gpg --symmetric filename

###### Batch Encrypt multiple files to specified recipients (encrypt.sh). Make sure your $file variable is surrounded by quotes so that files with spaces in their names will get picked up.

	for file in *.txt

	do

		gpg --encrypt -r A1B2C3D4E5F6G7H8 -r I1J2K3L4M5N6O7P8 "$file"

	done

#### Encrypt to a recipient.

	gpg -e -r recipient filename

	or

	gpg --encrypt -r recipient filename

	or encrypt and sign.

	gpg -e -r recipient -s filename

Use -u to specify the secret key to be used, and -r to specify the public key of the recipient.
**Note: This doesn't seem to work when you have a default sender and recipient key established in gpg.conf because the default sender and recipient overwrite the "-u" option.

    gpg -e -u "Sender User Name" -r "Receiver User Name" somefile
    Example 1: gpg -e -u "me@example.com" -r "you@example.com" -r "them@example.com" somefile

    Example 2:
    gpg -e -u "Billy Bob" -r "Nancy Bob" mydata.tar

    Example 3:
    gpg -s --default-key ABCD1234 -ea yyy.txt

#### Password encrypt and sign a file:

	gpg -c -s filename

###### Password encrypt and sign a message that can be decrypted by passphrase or secret key:

	gpg -c --sign --encrypt filename

	or

	gpg -c -s -e filename

###### UUEncode a file before ascii encrypting:

	uuencode filename filename > filename.uue
	gpg -a -e filename.uue

###### UUEncode a file before normal encrypting:

	uuencode filename filename > filename.uue
	gpg --encrypt filename.uue

###### Decrypt UUEncoded file with normal encryption then UUDecode it:

	gpg --decrypt filename > filename.uue
	uudecode filename.uue

###### Decrypt a message in standard out (stout) type:

  gpg

You will see a message similar to this: gpg: Go ahead and type your message ...
  At this point you can paste in the encrypted text and you will be prompted for your passphrase.
  Once you enter your passphrase, press Control+D to see the decrypted message.

Decrypt file (or stdin if no file is specified) and write it to stdout (or the file specified with --output). If the decrypted file is signed, the signature is also verified. This command differs from the default operation, as it never writes to the filename which is included in the file and it rejects files which don't begin with an encrypted message.

 	gpg --decrypt filenames

###### Decrypt a file that has been binary or ascii encrypted and output the decrypted content to a file:

	gpg --output decrypted.txt --decrypt encrypted.txt.gpg

	or

	gpg -o decrypted.txt -d encrypted.txt.gpg

This is a special version of the --decrypt command. The command expects the files to be decrypted either on the command line or reads the filenames from stdin; each name must be on separate line. The command is intended for a quick decryption of multiple files.

 	gpg --decrypt-files file1 file2 file3

#### Multiple Private Keys.

When encrypting or decrypting it is possible to have more than one private key in use. To use a different private key other than the default use the option -u UID or use the option --local-user UID. This causes the default key used to be replaced by the wanted key.

	gpg -u <KEY ID> -r recipient --armor --sign --encrypt filename

	or

	gpg -u <KEY ID> -r recipient -a -s -e filename

	or (this should prompt you for recipients)

	gpg -u nameofprivatekey -a -s -e filename

#### Signing / Verifying:

Make a signature. This command may be combined with --encrypt. (May also be combined with --symmetric (see GnuPG 1.0.7 released.)

 	gpg -s filename

 	or

 	gpg --sign filename

  Both -s and --sign make an illegible signature that you can't read. This is OK because GPG/PGP can still read it (not humans).

#### Make a clear text signature.

 	gpg --clearsign filename

 	or

 	cat filename.txt| gpg --clearsign > some_file.txt

 	or

 	echo "The message" | gpg --clearsign > The_message.txt

#### Make a detached signature.

 	gpg -b filename

 	or

 	gpg --detach-sign filename

#### Verify a signature file without generating any output.
With no arguments, the signature packet is read from stdin. If only a sigfile is given, it may be a complete signature or a detached signature, in which case the signed stuff is expected in a file without the ".sig" or ".asc" extension. With more than 1 argument, the first should be a detached signature and the remaining files are the signed stuff. To read the signed stuff from stdin, use - as the second filename. For security reasons a detached signature cannot read the signed material from stdin without denoting it in the above way.

 	gpg --verify sigfile signed_files

This is a special version of the --verify command which does not work with detached signatures. The command expects the files to be verified either on the command line or reads the filenames from stdin; each name must be on separate line. The command is intended for quick checking of many files.

 	gpg --verify-files filenames

#### Create ASCII armored output.

 	gpg -a -e filename

 	or

 	gpg --armor -e filename

Assume the input data is not in ASCII armored format.

 	gpg --no-armor

Use canonical text mode. If -t (but not --textmode) is used together with armoring and signing, this enables clearsigned messages. This kludge is needed for PGP compatibility; normally you would use --sign or --clearsign to select the type of the signature.

 	gpg -t

 	or

 	gpg --textmode

Encrypt for user id name. If this option is not specified, GnuPG asks for the user-id unless --default-recipient is given.

 	gpg -r nameofkey

 	or

 	gpg --recipient nameofkey

#### Groups
Set up a name group, which is similar to aliases in email programs. Any time the group name is a receipient (-r or --recipient), it will be expanded to the values specified.
The values are key IDs or fingerprints, but any key description is accepted. Note that a value with spaces in it will be treated as two different values. Note also there is only one level of expansion -- you cannot make a group that points to another group.

 	gpg --group name=value

Use name as default recipient if option --recipient is not used and don't ask if this is a valid one. name must be non-empty.

 	gpg --default-recipient nameofkey

Use the default key as default recipient if option --recipient is not used and don't ask if this is a valid one. The default key is the first one from the secret keyring or the one set with --default-key.

 	gpg --default-recipient-self

Reset --default-recipient and --default-recipient-self.

 	gpg --no-default-recipient

Use name as default user ID for signatures. If this is not used the default user ID is the first user ID found in the secret keyring.

 	gpg --default-key nameofkey

Same as --recipient but this one is intended for use in the options file and may be used with your own user-id as an "encrypt-to-self." These keys are only used when there are other recipients given either by use of --recipient or by the asked user id. No trust checking is performed for these user ids and even disabled keys can be used.

 	gpg --encrypt-to name

Disable the use of all --encrypt-to keys.

 	gpg --no-encrypt-to


#### Comments & Versions

Use string as comment string in clear text signatures. The default is not to write a comment string.

 	gpg --comment string

Force to write the standard comment string in clear text signatures. Use this to overwrite a --comment from a config file. This option is now obsolete because there is no default comment string anymore.

 	gpg --default-comment

Omit the version string in clear text signatures.

 	gpg --no-version

Force to write the version string in clear text signatures. Use this to overwrite a previous --no-version from a config file.

 	gpg --emit-version

#### Special "for your eyes only"

Set the "for your eyes only" flag in the message. This causes GnuPG to refuse to save the file unless the --output option is given, and PGP to use the "secure viewer" with a Tempest-resistant font to display the message. This option overrides --set-filename.

 	--for-your-eyes-only

Resets the --for-your-eyes-only flag.

 	--no-for-your-eyes-only

 Set compression level to n. A value of 0 for n disables compression. Default is to use the default compression level of zlib (normally 6).

 	-z n, --compress n

Skip the signature verification step. This may be used to make the decryption faster if the signature verification is not needed.

 	--skip-verify

When making a data signature, prompt for an expiration time. If this option is not specified, the expiration time is "never."

 	gpg --ask-sig-expire

Resets the --ask-sig-expire option.

 	gpg --no-ask-sig-expire

Do not put the keyid into encrypted packets. This option hides the receiver of the message and is a countermeasure against traffic analysis. It may slow down the decryption process because all available secret keys are tried.

 	gpg --throw-keyid

Don't look at the key ID as stored in the message but try all secret keys in turn to find the right decryption key. This option forces the behaviour as used by anonymous recipients (created by using --throw-keyid) and might come handy in case where an encrypted message contains a bogus key ID.

 	gpg --try-all-secrets

Put the name value pair into the signature as notation data. Name must consist only of alphanumeric characters, digits or the underscore; the first character must not be a digit. Value may be any printable string; it will be encoded in UTF8, so you should check that your --charset is set correctly. If you prefix name with an exclamation mark, the notation data will be flagged as critical (rfc2440:5.2.3.15).

 	gpg -N
 	gpg --notation-data name=value

This option changes the behavior of cleartext signatures so that they can be used for patch files. You should not send such an armored file via email because all spaces and line endings are hashed too. You can not use this option for data which has 5 dashes at the beginning of a line, patch files don't have this. A special armor header line tells GnuPG about this cleartext signature option.

 	gpg --not-dash-escaped

Because some mailers change lines starting with "From " to "<From " it is good to handle such lines in a special way when creating cleartext signatures. All other PGP versions do it this way too. This option is not enabled by default because it would violate rfc2440.

 	gpg --escape-from-lines

Use string as the name of file which is stored in messages.

 	gpg --set-filename string

Try to create a file with a name as embedded in the data. This can be a dangerous option as it allows to overwrite files.

 	gpg --use-embedded-filename

This option enables a mode in which filenames of the form "-&n," where n is a non-negative decimal number, refer to the file descriptor n and not to a file with that name.

 	gpg --enable-special-filenames

#### Revoke a Key.

	gpg --gen-revoke THEKEYID > revoked.key

This creates a revocation certificate. To be able to do this, you need a secret key, otherwise anyone could revoke your certificate. This has one disadvantage. If you do not know the passphrase for the secret key, the revocation key will become useless and you cannot revoke the secret key! To overcome this problem it is wise to create a revoke license when you create a key pair. And if you do so, keep it safe! This can be on disk, paper, etc. Make sure that this certificate will not fall into wrong hands!!!! If you don't someone else can issue the revoke certificate for your key and make it useless.

You will need to enter the revoke reason for the key and an optional comment.

Once you have the revocation certificate, you will need to import it so that the key will get revoked.

	gpg --import revoked.key
	Type: gpg --list-keys and you will see that the key has been revoked.

Next, you will have to send the revoked key to the key server. This is the same method as sending a normal key except this one has been revoked. When the server receives the revoked key, it will be removed from the server.

#### Remove/Revoke a specific email address from your key.
	gpg --edit-key 01234567
	uid 4 (This is the uid of the email address that you want to revoke).
	revuid

		Really revoke this user ID? (y/N) y
		Please select the reason for the revocation:
  	0 = No reason specified
  	4 = User ID is no longer valid
  	Q = Cancel
		(Probably you want to select 4 here)
		Your decision? 4
		Enter an optional description; end it with an empty line:
		>
		Reason for revocation: User ID is no longer valid
		(No description given)
		Is this okay? (y/N) y

		You need a passphrase to unlock the secret key for user: "John Doe <john@doe.tld>"
		[ultimate] (1). John Doe <john@doe.tld>
		[ revoked] (2)  John Doe (Corp) <john.doe@corp.tld>

		gpg> save
Next, send your updated key to the keyservers.

	gpg --send-keys 01234567

	gpg: sending key 01234567 to hkp server keys.gnupg.net

There are three main rings of keyservers out there ([Source](https://www.phildev.net/pgp/gpgsigning.html "")). Each group syncs within it's own pool well, and to the other pools with varying levels of success, so I recommend uploading to one of each. Something like this will work.

		servers="x-hkp://pool.sks-keyservers.net pgp.mit.edu wwwkeys.ch.pgp.net"
		for server in $servers; do
			gpg --keyserver $server --send-key <your_keyid>
		done

#### Key Administration:
With the GnuPG system comes a file that acts as some kind of database. In this file all data regarding keys with the information that comes with the keys is stored.

#### List all the keys:

This will show you the key IDs and other information:

	gpg --list-keys

To show the "Short Key" ID:

	gpg -K --with-fingerprint --with-colons | grep "sec" | cut -f5 -d ':'

To show the "HEX Key" ID (last 16 characters with 0x prepended):

	gpg -K --with-fingerprint --with-colons | grep "sec" | cut -f5 -d ':'|awk '{print "0x" $1}'

List all the keys and see the signatures as well type:

	gpg --list-sigs

To see the fingerprints type:

	gpg --fingerprint

	You want to see "Fingerprints" to ensure that somebody is really the person they claim (like in a telephone call). This command will result in a list of relatively small numbers.

To list the secret keys you type:

	gpg --list-secret-keys

Note that listing fingerprints and signatures from private keys has no use whatsoever.

To delete a public key you type:

 	gpg --delete-key UID

To delete a secret key you type:

	gpg --delete-secret-key UID
	(You have to delete the private key before deleting the public key)

There is one more important command that is relevant for working with keys.

	gpg --edit-key <HEX KEY ID>

	Using this you can edit (among other things) the expiration date, add a fingerprint and sign your key. When in this mode you can press the question mark key to see the options available to you.

Import a key:

	gpg --import filename

You might get an error with the newer version of GPG (gpg: error building skey array: Permission denied) or (gpg: error building skey array: No pinentry).

	Try using (--batch):
	gpg --batch --import your.secret.key.asc

Export your key:

	Export public key in binary format:
	gpg --export <KEY ID>

	Export public key in ascii format:
	gpg --export -a <KEY ID>

	Export secret key in binary format:
	gpg --export-secret-key <KEY ID>

	Export secret key in ascii format:
	gpg --export-secret-key -a <KEY ID>

#### Source:
https://www.gnupg.org/gph/en/manual/x110.html
http://www.dewinter.com/gnupg_howto/english/GPGMiniHowto-3.html#ss3.5
https://www.gnupg.org/documentation/howtos.html
https://github.com/rldutch1/pgp/blob/master/commandline_switches.html

#### Shell Function for PGP:
Here is a PGP function that I have created and use on my Mac and Linux computers (it works on Windows too with Git or Cygwin installed). I named it "pgp" so that it is different from gpg on Linux/Mac and will not conflict.

	pgp(){
	clear
	case $1 in
        ascii)
        echo "ASCII Encrypting... " $2
        gpg -a -e $2
        echo "..." >> $2;rm -f $2
        echo $2 " has been deleted!"
        ;;
        clearsign)
        echo "Signing..." $2
        gpg --clearsign $2
        echo $2 " has been signed!"
        ;;
        decrypt)
        #gpg --decrypt $2
        if [ ! $2 ] || [ ! $3 ]; then
        echo "Syntax: pgp decrypt outputfile encryptedfile.asc"
        else
        gpg --output $2 --decrypt $3
        fi
        ;;
        delete-keys)
        echo "Deleting..." $2
        gpg --delete-keys $2
        gpg --list-keys
        ;;
        detachedsig)
        echo "Creating signature file..." $2
        gpg --output $2.sig --detach-sig $2
        ;;
        encrypt)
        echo "Encrypting..." $2
        gpg --encrypt $2
        echo "..." > $2;rm -f $2
        echo $2 " has been deleted!"
        ;;
        exportpublic)
        echo "Exporting Public Key..." $2
        gpg --export --armor $2 > $2.asc
        ;;
        exportprivate)
        echo "Exporting PRIVATE KEY..." $2
        gpg --export --armor $2 > $2.asc
        gpg --export-secret-keys --armor $2 >> $2.asc
        ;;
        fingerprint)
        gpg --fingerprint $2
        ;;
        fingerprint_from_file)
        gpg --with-fingerprint $2
        ;;
        import)
        echo "Importing..." $2
        gpg --import $2
        echo $2 " has been imported!"
        ;;
        list)
        gpg --list-keys
        ;;
        listdirs)
        gpgconf --list-dirs
        ;;
        message)
        cd ~/Documents/PGP/messages
        xyzrh1=message.`date +"%Y%m%d%H%M%S%Z"`
        vi $xyzrh1.txt; pgp ascii $xyzrh1.txt
        ;;
        passencrypt)
        echo "Encrypting..." $2
        gpg -c -s $2
        echo $2 " has been password encrypted!"
        ;;
        releasecache)
        gpgconf --kill gpg-agent;gpgconf --launch gpg-agent
        ;;
        receivekeys)
        gpg --keyserver $2 --recv-keys $3
        ;;
        revoke_key)
        gpg --gen-revoke $2 > revoke.$2.asc
        ;;
        sign)
        echo "Signing..." $2
        gpg --sign $2
        echo $2 " has been signed!"
        ;;
        sendkeys)
        if [ ! $2 ]; then
        echo "Example: gpg --keyserver hkp://pgp.mit.edu --send-keys 6EE89C2D"
        else
        gpg --keyserver $2 --send-keys $3
        fi
        ;;
        showphoto)
        if [ ! $2 ]; then
        echo "Should have xloadimage installed:"
        echo "Example:"
        echo "showphoto 6EE89C2D"
        echo "showphoto user@example.com"
        else
        gpg --list-options show-photos --fingerprint $2
        fi
        ;;
        update)
        gpg --update-trustdb
        ;;
        uue)
        echo "UUEncoding..." $2
        uuencode $2 $2 > $2.uue
        echo "ASCII Encrypting..." $2.uue
        gpg -a -e $2.uue
        echo "..." > $2.uue;rm -f $2 $2.uue
        echo $2 " has been deleted!"
        ;;
        uuegpg)
        echo "UUEncoding..." $2
        uuencode $2 $2 > $2.uue
        echo "Encrypting..." $2.uue
        gpg --encrypt $2.uue
        echo "..." > $2.uue;rm -f $2 $2.uue
        echo $2 " has been deleted!"
        ;;
        uuedecrypt)
        #echo "Decrypting..." $2
        gpg --decrypt $2 > $2.uue
        echo "Decoding..." $2
        uudecode $2.uue;
        echo "..." > $2.uue;rm -f $2.uue
        echo $2 " has been decoded!"
        ;;
        verify)
        echo "Signing..." $2
        gpg --verify $2
        echo $2 " verify status!"
        ;;
        *)
        message00="gpg --edit-key 5DD98B3E"
      	message01="pgp ascii textfile  (gpg -a -e thefilename)"
      	message02="pgp clearsign textfile  (gpg --clearsign thefilename)"
      	message03="pgp decrypt outputfile.tar encryptedfile.tar.gpg  (gpg -o outputfile -d encryptedfile)"
      	message04="pgp delete-keys 5DD98B3E  (gpg --delete-keys keyname)"
      	message05="pgp detachedsig filename  (gpg --output doc.sig --detach-sig doc.txt)"
      	message06="pgp encrypt filename  (gpg --encrypt thefilename)"
      	message07="pgp exportpublic keyname  (gpg --export --armor thekeyname)"
      	message08="pgp exportprivate keyname  (gpg --export-secret-keys --armor ABCD1234 >> ABCD1234.asc)"
      	message09="pgp fingerprint 5DD98B3E  (gpg --fingerprint key)"
      	message10="pgp fingerprint_from_file file_with_key  (gpg --with-fingerprint thefilename)"
      	message11="pgp import filename.asc  (gpg --import keyfile / gpg2 --import keyfile)"
      	message12="pgp list  (gpg --list-keys)"
      	message13="pgp listdirs  (gpgconf --list-dirs)"
      	message14="pgp message"
      	message15="pgp passencrypt textfile  (gpg -c -s thefilename)"
      	message16="pgp receivekeys theservername thekeyname (gpg --keyserver keyserver.ubuntu.com --recv-keys 6EE89C2D)"
      	message17="pgp releasecache (gpgconf --kill gpg-agent;gpgconf --launch gpg-agent)"
      	message18="pgp revoke_key (gpg --gen-revoke thekeyname > revoke.thekeyname.asc)"
      	message19="pgp sendkeys theservername thekeyname  (gpg --keyserver hkp://pgp.mit.edu --send-keys 6EE89C2D)"
      	message20="pgp showphoto 6EE89C2D (gpg --list-options show-photos --fingerprint 6EE89C2D)"
      	message21="pgp sign textfile  (gpg --sign thefilename)"
      	message22="pgp update (gpg --update-trustdb)"
      	message23="pgp uue filename (uuencode thefilename thefilename > thefilename.uue;gpg -a -e thefilename.uue)"
      	message24="pgp uuedecrypt filename  (gpg --decrypt thefilename > thefilename.uue;uudecode thefilename.uue)"
      	message25="pgp uuegpg filename (uuencode thefilename thefilename > thefilename.uue;gpg --encrypt thefilename.uue)"
      	message26="pgp verify filename  (gpg --verify signaturefile)"
        echo $message00
        echo $message01
        echo $message02
        echo $message03
        echo $message04
        echo $message05
        echo $message06
        echo $message07
        echo $message08
        echo $message09
        echo $message10
        echo $message11
        echo $message12
        echo $message13
        echo $message14
        echo $message15
        echo $message16
        echo $message17
        echo $message18
        echo $message19
        echo $message20
        echo $message21
        echo $message22
        echo $message23
        echo $message24
        echo $message25
        echo $message26
        echo " "
   	;;
	esac
	}

#### View your trust database:
View your trust database and see the marginal and other trust information type:

	gpg --update-trustdb

Before a key can be trusted it must be signed and the trust level applied by the key owner. Marginally (Marginal) trusted keys can also be trusted if 3 or more people you trust have chosen to trust the same key that you have marginally trusted. Or if 3 or more marginally trusted people marginally trust the same key then it will be considered trusted by your key.

#### GPG Privacy Assistant (GPA):
Graphical user interface for GnuPG called GPG Privacy Assistant (GPA). It can be installed by typing:

	sudo apt-get -y install gpa
	sudo dnf -y install gpa

#### Passphrase cache timeout:
On Fedora Linux, the passphrase cache timeout was 300 seconds (5 minutes). I couldn't find where I could change that setting. I ended up installing dconf-editor and I was able to change the passphrase cache. I added screenshots (dconf-editor_settings##.png.

I installed Open GnuPG on my Mac using: sudo port install gnupg2
I like it a lot better thant the GPG Suite that I was previously using because I can encrypt and decrypt from an SSH session without the GUI password prompt preventing me from decrypting something. I have also discovered that I no longer seem to be able to use the command 'gpg < encryptedfile'. I get a message that says it doesn't understand what I am trying to do. I actually have to paste in the encrypted content and press control+d.

[How can I force the system to ask the passphrase every time?](https://security.stackexchange.com/questions/103034/gnupg-decryption-not-asking-for-passphrase/ "")

Old versions of GnuPG uses the gpg-agent, which caches the passphrase for a given time. Use the option --no-use-agent or add a line no-use-agent to ~/.gnupg/gpg.conf to prevent using the agent.

Note: --no-use-agent is obsolete in gpg2 and has no effect.

Removing the passphrase cacheing and setting it to 1 second. I haven't tried this but it has a green checkmark on stackexchange.

Edit: ~/.gnupg/gpg-agent.conf

	Add:
		default-cache-ttl 1
		max-cache-ttl 1

#### Reload the gpg agent:
	echo RELOADAGENT | gpg-connect-agent

	or

	Type:

	gpg-connect-agent

	At the prompt type: RELOADAGENT

	Response should be: OK

	At the prompt type: BYE
	Reponse should be: OK closing connection

#### Restart the gpg agent:

	Type: gpg-connect-agent

	At the prompt type: KILLAGENT

	Reponse should be: OK closing connection

#### List PGP/GPG directories:

	gpgconf --list-dirs

#### Miscellaneous:

gpg options --debug-level guru --debug-all --verbose

gpg --debug-level guru --debug-all --verbose


I was having trouble importing my private key because it was in an older version of GPG.
I was getting the following errors:

	gpg: error building skey array: No such file or directory
	gpg import error sending to agent no such file or directory
	gpg: error building skey array: permission denied
	gpg: decryption failed: no secret key

I had to decrypt my passphrase encrypted key using a user that did not have GPG enabled (root).
I also renamed my .gnupg directory and ran gpg again so that a new .gnupg folder would get created. Inside that
directory I had to manually create the private-keys-v1.d directory so the "No such file or directory" error would
go away.

I was still having issues and kept seeing a message telling me no private key present whenever I tried to decrypt something.
I ended up restoring the .gnupg folder from a backup and restarting the gpg agent.

#### Pinentry
Running gpg through SSH session sometimes will error when performing tasks. When I used the pinentry-mode, the password was cached but I was able to decrypt.

	gpg --decrypt --pinentry-mode=loopback <file>
	gpg -c -s --pinentry-mode=loopback <file>

#### Keybase error adding PGP/GPG key:

	https://github.com/keybase/client/issues/22458

#### gpgconf:
##### Options
Starting with GnuPG 1.1.92 (incl. GnuPG 1.2.1, 1.2.0 and 1.1.92), long options can be put in an options file (default "~/.gnupg/gpg.conf"). In GnuPG versions up through GnuPG 1.1.91 (incl. 1.0.6, 1.0.7, and 1.1.91), long options can be put in an "old style" configuration file (default "~/.gnupg/options").
Short option names will not work -- for example, **armor** is a valid option for the options file, while **a** is not. Do not write the 2 dashes, but simply the name of the option and any required arguments. Lines with a hash as the first non-white-space character are ignored. Commands may be put in this file too, but that does not make sense.

	Two useful entries for .gnupg/gpg.conf file.
	These entries will force GPG to use your key as default and automatically encrypt to your key.

	default-key 1A2B3CD4
	encrypt-to 1A2B3CD4

	#gpg-connect-agent

#### gpg.conf Example File
```
# These first three lines are not copied to the gpg.conf file in
# the users home directory.
# $Id$
# Options for GnuPG
# Copyright 1998, 1999, 2000, 2001, 2002, 2003,
#           2010 Free Software Foundation, Inc.
#
# This file is free software; as a special exception the author gives
# unlimited permission to copy and/or distribute it, with or without
# modifications, as long as this notice is preserved.
#
# This file is distributed in the hope that it will be useful, but
# WITHOUT ANY WARRANTY, to the extent permitted by law; without even the
# implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
#
# Unless you specify which option file to use (with the command line
# option "--options filename"), GnuPG uses the file ~/.gnupg/gpg.conf
# by default.
#
# An options file can contain any long options which are available in
# GnuPG. If the first non white space character of a line is a '#',
# this line is ignored.  Empty lines are also ignored.
#
# See the man page for a list of options.

# Uncomment the following option to get rid of the copyright notice

#no-greeting

# If you have more than 1 secret key in your keyring, you may want to
# uncomment the following option and set your preferred keyid.

default-key ABCD1234
encrypt-to ABCD1234


# If you do not pass a recipient to gpg, it will ask for one.  Using
# this option you can encrypt to a default key.  Key validation will
# not be done in this case.  The second form uses the default key as
# default recipient.

#default-recipient some-user-id
#default-recipient-self
#default-recipient ABCD1234

# By default GnuPG creates version 4 signatures for data files as
# specified by OpenPGP.  Some earlier (PGP 6, PGP 7) versions of PGP
# require the older version 3 signatures.  Setting this option forces
# GnuPG to create version 3 signatures.

#force-v3-sigs

# Because some mailers change lines starting with "From " to ">From "
# it is good to handle such lines in a special way when creating
# cleartext signatures; all other PGP versions do it this way too.
# To enable full OpenPGP compliance you may want to use this option.

no-escape-from-lines

# When verifying a signature made from a subkey, ensure that the cross
# certification "back signature" on the subkey is present and valid.
# This protects against a subtle attack against subkeys that can sign.
# Defaults to --no-require-cross-certification.  However for new
# installations it should be enabled.

require-cross-certification


# If you do not use the Latin-1 (ISO-8859-1) charset, you should tell
# GnuPG which is the native character set.  Please check the man page
# for supported character sets.  This character set is only used for
# metadata and not for the actual message which does not undergo any
# translation.  Note that future version of GnuPG will change to UTF-8
# as default character set.

#charset utf-8

# Group names may be defined like this:
#   group mynames = paige 0x12345678 joe patti
#
# Any time "mynames" is a recipient (-r or --recipient), it will be
# expanded to the names "paige", "joe", and "patti", and the key ID
# "0x12345678".  Note there is only one level of expansion - you
# cannot make an group that points to another group.  Note also that
# if there are spaces in the recipient name, this will appear as two
# recipients.  In these cases it is better to use the key ID.

#group mynames = paige 0x12345678 joe patti
group myfriends = BD4054DAC61AB7BB B1BC917D4AF9F0EC

#no-mangle-dos-filenames

# Lock the file only once for the lifetime of a process.  If you do
# not define this, the lock will be obtained and released every time
# it is needed - normally this is not needed.

#lock-once

# GnuPG can send and receive keys to and from a keyserver.  These
# servers can be HKP, email, or LDAP (if GnuPG is built with LDAP
# support).
#
# Example HKP keyservers:
#      hkp://keys.gnupg.net
#
# Example LDAP keyservers:
#      ldap://pgp.surfnet.nl:11370
#
# Regular URL syntax applies, and you can set an alternate port
# through the usual method:
#      hkp://keyserver.example.net:22742
#
# If you have problems connecting to a HKP server through a buggy http
# proxy, you can use keyserver option broken-http-proxy (see below),
# but first you should make sure that you have read the man page
# regarding proxies (keyserver option honor-http-proxy)
#
# Most users just set the name and type of their preferred keyserver.
# Note that most servers (with the notable exception of
# ldap://keyserver.pgp.com) synchronize changes with each other.  Note
# also that a single server name may actually point to multiple
# servers via DNS round-robin.  hkp://keys.gnupg.net is an example of
# such a "server", which spreads the load over a number of physical
# servers.  To see the IP address of the server actually used, you may use
# the "--keyserver-options debug".

keyserver hkp://pgp.mit.edu
#keyserver hkps://hkps.pool.sks-keyservers.net
#keyserver http://http-keys.gnupg.net
#keyserver mailto:pgp-public-keys@keys.nl.pgp.net

# Common options for keyserver functions:
#
# include-disabled = when searching, include keys marked as "disabled"
#                    on the keyserver (not all keyservers support this).
#
# no-include-revoked = when searching, do not include keys marked as
#                      "revoked" on the keyserver.
#
# verbose = show more information as the keys are fetched.
#           Can be used more than once to increase the amount
#           of information shown.
#
# use-temp-files = use temporary files instead of a pipe to talk to the
#                  keyserver.  Some platforms (Win32 for one) always
#                  have this on.
#
# keep-temp-files = do not delete temporary files after using them
#                   (really only useful for debugging)
#
# honor-http-proxy = if the keyserver uses HTTP, honor the http_proxy
#                    environment variable
#
# broken-http-proxy = try to work around a buggy HTTP proxy
#
# auto-key-retrieve = automatically fetch keys as needed from the keyserver
#                     when verifying signatures or when importing keys that
#                     have been revoked by a revocation key that is not
#                     present on the keyring.
#
# no-include-attributes = do not include attribute IDs (aka "photo IDs")
#                         when sending keys to the keyserver.

keyserver-options auto-key-retrieve

# Uncomment this line to display photo user IDs in key listings and
# when a signature from a key with a photo is verified.

#show-photos

# Use this program to display photo user IDs
#
# %i is expanded to a temporary file that contains the photo.
# %I is the same as %i, but the file isn't deleted afterwards by GnuPG.
# %k is expanded to the key ID of the key.
# %K is expanded to the long OpenPGP key ID of the key.
# %t is expanded to the extension of the image (e.g. "jpg").
# %T is expanded to the MIME type of the image (e.g. "image/jpeg").
# %f is expanded to the fingerprint of the key.
# %% is %, of course.
#
# If %i or %I are not present, then the photo is supplied to the
# viewer on standard input.  If your platform supports it, standard
# input is the best way to do this as it avoids the time and effort in
# generating and then cleaning up a secure temp file.
#
# The default program is "xloadimage -fork -quiet -title 'KeyID 0x%k' stdin"
# On Mac OS X and Windows, the default is to use your regular JPEG image
# viewer.
#
# Some other viewers:
# photo-viewer "qiv %i"
# photo-viewer "ee %i"
# photo-viewer "display -title 'KeyID 0x%k'"
#
# This one saves a copy of the photo ID in your home directory:
# photo-viewer "cat > ~/photoid-for-key-%k.%t"
#
# Use your MIME handler to view photos:
# photo-viewer "metamail -q -d -b -c %T -s 'KeyID 0x%k' -f GnuPG"

#  *** Options for GPGTools ***

# Automatic key location
#
# GnuPG can automatically locate and retrieve keys as needed using the
# auto-key-locate option.  This happens when encrypting to an email
# address (in the "user@example.com" form), and there are no
# user@example.com keys on the local keyring.  This option takes the
# following arguments, in the order they are to be tried:
#
# cert = locate a key using DNS CERT, as specified in RFC-4398.
#        GnuPG can handle both the PGP (key) and IPGP (URL + fingerprint)
#        CERT methods.
#
# pka = locate a key using DNS PKA.
#
# ldap = locate a key using the PGP Universal method of checking
#        "ldap://keys.(thedomain)".  For example, encrypting to
#        user@example.com will check ldap://keys.example.com.
#
# keyserver = locate a key using whatever keyserver is defined using
#             the keyserver option.
#
# You may also list arbitrary keyservers here by URL.
#
# Try CERT, then PKA, then LDAP, then hkp://keys.gnupg.net:
auto-key-locate keyserver

comment An encrypted message received, deserves an encrypted reply!
cert-digest-algo SHA512
default-preference-list SHA512 SHA384 SHA256 SHA224 AES256 AES192 AES CAST5 ZLIB BZIP2 ZIP Uncompressed
personal-digest-preferences SHA512 SHA384 SHA256 SHA224

no-emit-version

cipher-algo AES256
digest-algo SHA512

#pinentry-program /usr/bin/pinentry-curses
```
