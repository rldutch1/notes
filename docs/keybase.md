# Running Keybase
- [ Keybase Help ](https://book.keybase.io/ "")
- run_keybase
- keybase chat read
- keybase chat send

#### Error message: /keybase: Transport endpoint is not connected.

I was able to get the keybase directory working after using this command from this link: - [ cannot access 'keybase': Transport endpoint is not connected (linux) #20331 ](https://github.com/keybase/client/issues/20331/ ""):
```
sudo fusermount -u /keybase
```

#### - [ Keybase commands I copied from https://book.keybase.io/guides/command-line ](https://book.keybase.io/guides/command-line "")

#### Generally:

    -m means a message (as opposed to stdin or an input file)
    -i means an input file
    -o means an output file
    -b means binary output, as opposed to ASCII

#### given keybase user "max"
```
keybase encrypt max -m "this is a secret"
echo "this is a secret" | keybase encrypt max
keybase encrypt max -i secret.txt
keybase encrypt max -i secret.mp3 -b -o secret.mp3.encrypted
```

#### Encrypting for Keybase users
```
keybase encrypt max -m "this is a secret for max"
echo "secret" | keybase encrypt max
echo "secret" | keybase encrypt maxtaco@twitter
keybase encrypt max -i ~/movie.avi -o ~/movie.avi.encrypted
```

#### Decrypting
```
keybase decrypt -i movie.avi.encrypted -o movie.avi
keybase decrypt -i some_secret.txt
cat some_secret.txt.encrypted | keybase decrypt
```

#### Signing
```
keybase sign -m "I hereby abdicate the throne"
keybase sign -i foo.exe -b -o foo.exe.signed
```

#### Verifying
```
cat some_signed_statement.txt | keybase verify
keybase verify -i foo.exe.signed -o foo.exe
```

#### Encrypting a PGP message
```
If a Keybase user only has a PGP key, or you'd rather encrypt for that:

keybase pgp encrypt chris -m "secret"            # encrypt
keybase pgp encrypt maxtaco@twitter -m "secret"  # using a twitter name
keybase pgp encrypt maxtaco@reddit -m "secret"   # using a Reddit name
keybase pgp encrypt chris -s -m "secret"         # also sign with -s
keybase pgp encrypt chris -i foo.txt             # foo.txt -> foo.txt.asc
keybase pgp encrypt chris -i foo.txt -o bar.asc  # foo.txt -> bar.asc
echo 'secret' | keybase pgp encrypt chris        # stream
```

#### Decrypting a PGP message
```
keybase pgp decrypt -i foo.txt.asc             # foo.txt.asc -> stdout
keybase pgp decrypt -i foo.txt.asc -o foo.txt  # foo.txt.asc -> foo.txt
cat foo.txt.asc | keybase pgp decrypt          # decrypt a stream
```

#### Send attachment from the commandline
```
keybase chat upload user1,user2 filename.txt
```

#### Signing a PGP message
```
keybase pgp sign -m "Hello"                # sign a message
keybase pgp sign --clearsign -m "Hello"    # sign, but don't encode contents
keybase pgp sign -i foo.txt --detached     # generate foo.txt.asc, just a signature
keybase pgp sign -i foo.txt                # generate foo.txt.asc, containing signed foo.txt
echo "I rock." | keybase pgp sign          # stream
```

#### Verifying a PGP message
```
keybase pgp verify -i foo.txt.asc            # verify a self-signed file
keybase pgp verify -d foo.txt.asc -i foo.txt # verify a file + detached signature
cat foo.txt.asc | keybase pgp verify         # stream a self-signed file
```

#### Publishing a bitcoin address
```
keybase btc 1p90X3byTONYhortonETC  # sign and set the bitcoin
                                   # address on your profile
```


