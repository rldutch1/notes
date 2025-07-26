You will need to install the barcode application and ImageMagick.
```
	sudo dnf -y install barcode
	sudo dnf -y install ImageMagick
```

Test create a postscript file that contains a barcode then convert it to .png:
```
	barcode -b "1234567890" -e "code128" -o aaa.ps

	magick aaa.ps aaa.png
```

barcode -i out2.tab -o ouput.ps

The following will read serial numbers from a file and print Code 128 barcodes in table format (5 columns x 20 rows) on an 8.5x11 inch sheet of paper.
```
	barcode -e "code128" -t 5x20 -p "8.5x11in" -i serials.txt -o serials.pdf
```

The following will read serial numbers from a file and print Code 39 barcodes in table format (5 columns x 20 rows) on an 8.5x11 inch sheet of paper. (Code 39 does not seem to recognize lowercase letters).
```
	barcode -e "code39" -t 5x20 -p "8.5x11in" -i serials.txt -o serials.pdf
```

The following will read serial numbers from a file and print Code 39 barcodes in table format (5 columns x 5 rows with a barcode margin of 20x and 50y) on an 8.5x11 inch sheet of paper. (Code 39 does not seem to recognize lowercase letters).
```
	barcode -e "code39" -t "5x5 +96x+48+96+48" -m "20x50" -p "8.5x11in" -i serials.txt -o serials.pdf
```

The following will create a single barcode 39 .ps file with geometry of 250x100 and generate a .png that is the same size as the barcode.
<a href='https://stackoverflow.com/questions/38060091/how-do-i-force-gnu-barcode-to-honor-the-page-size-i-specify-on-the-command-lin' target='_blank'>source</a>
```
	barcode -b "343110" -e "code39" -g "250x100" -E -o aaa.ps;magick aaa.ps aaa.png
```

Other barcode software:
https://github.com/larsschenk/ActiveBarcodeCLI.git
https://www.activebarcode.com/commandline/
```
./ActiveBarcodeCLI --text=192837465012 --code=ean13 --width=400 --height=200 ean.wmf
```

Strockscribe:
https://www.youtube.com/watch?v=Ur2hA-AaDG0
https://strokescribe.com/en/barcode-libreoffice-calc.html?t=1752080693587
Tools->Macros-->Organize-->Basic

Google Sheets:
Print Barcode Labels Using ONLY Google Sheets: https://www.youtube.com/watch?v=QZi2pQcxRsw

QREncode:
```
dnf -y install qrencode
```

