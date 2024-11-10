Frequently Asked Questions: https://exiftool.org/faq.html#Q1

`Source:` : <https://exiftool.org/forum/index.php?topic=10562.0>

To write a new copyright, use something like this

```
exiftool -Copyright="New Notice" -CopyrightNotice="New Notice" -Rights="New Notice" <FileOrDir>
```

That will set the three major copyright tags to what you want.  If you want to batch recurse into subdirectories, use the -r (recurse) option.  This command will make backup files.  Use the Overwrite_Original option to suppress that.  
Add the -P (preserve) option to keep the current file system modify date.

`Source:` : <https://exiftool.org/forum/index.php?topic=4837.0>

Set the copyright flag to true:

```
exiftool -all= -Holland:CopyrightFlag='True' soccer*.webm
```

Exiftool function:
```
gpsinfo() {
case $1 in

#-n = Put the coordinates in decimal format.
#-csv = Put the output in .csv format.
#-T = Put the output in wide format.
#-t = Put the output in column format.
#-ext = Look for the following file extension.
#DIR1 = The directory to look in for photos.
#DIR2 = The directory to output the csv file.

#exiftool -filename -gpslatitude -gpslongitude -gpsaltitude -createdate -relativealtitude -T -n -csv -ext JPG DIR1 > DIR2\out.csv
##exiftool -T -FileName -GPSPosition -c "%.6f" * > GPSInfo.txt
#exiftool -T -Filename -createdate -gpsposition -c "%.6f degrees" -Filename *| sed 's/://g'| sed 's/,\ /_/g'| sed 's/\ degrees\ /_/g' > GPSInfo.sh;chmod +x GPSInfo.sh
##exiftool -T -Filename -createdate -gpsposition -c "%.6f degrees" -Filename *| sed 's/://g'| sed 's/,\ /_/g'| sed 's/\ degrees\ /_/g'|awk '{print "mv " $1 " "$2$3"."$4"."$5}' > GPSInfo.sh
##exiftool -T -Filename -DateTimeOriginal -gpsposition -c "%.6f degrees" -Filename * | sed 's/://g'| sed 's/,\ /_/g'| sed 's/\ degrees\ /_/g'|awk '{print "mv " $1 " "$2$3"."$4"."$5}' > GPSInfo.sh
##exiftool -T -Filename -FileModifyDate -gpsposition -c "%.6f degrees" -Filename * | sed 's/://g'| sed 's/,\ /_/g'| sed 's/\ degrees\ /_/g'|awk '{print "mv " $1 " "$2$3"."$4"."$5}' > GPSInfo.sh
##exiftool -T -Filename -DateTimeOriginal -gpsposition -c "%.6f degrees" -Filename * | sed 's/://g'| sed 's/,\ /_/g'| sed 's/\ degrees\ /_/g'|awk '{print "mv " $1 " "$2$3"."$4"."$5}' > GPSInfo.sh
#!#TESTING: Change the timezone for DateTimeOriginal to -7.
#!#	exiftool -T -Filename "-DateTimeOriginal-=0:0:0 7:0:0" -gpsposition -c "%.6f degrees" -Filename * | sed 's/://g'| sed 's/,\ /_/g'| sed 's/\ degrees\ /_/g'|awk '{print "mv " $1 " "$2$3"."$4"."$5}' > GPSInfo.sh
#This works: exiftool -n -filename -gpslatitude -gpslongitude -csv -r . >> out.csv #Source: https://exiftool.org/forum/index.php?topic=3075.0

crdate)
		exiftool -T -FileName -GPSPosition -c "%.6f" * > GPSInfo.txt
		exiftool -T -Filename -createdate -gpsposition -c "%.6f degrees" -Filename *| sed 's/://g'| sed 's/,\ /_/g'| sed 's/\ degrees\ //g'|awk '{print "mv " $1 " "$2$3"."$4"."$5}' > GPSInfo.sh ;chmod +x GPSInfo.sh
;;
dttimeorig)
		exiftool -T -FileName -GPSPosition -c "%.6f" * > GPSInfo.txt
		exiftool -T -Filename -DateTimeOriginal -gpsposition -c "%.6f degrees" -Filename * | sed 's/://g'| sed 's/,\ /_/g'| sed 's/\ degrees\ //g'|awk '{print "mv " $1 " "$2$3"."$4"."$5}' > GPSInfo.sh;chmod +x GPSInfo.sh
;;
filemoddt)
		exiftool -T -FileName -GPSPosition -c "%.6f" * > GPSInfo.txt
		exiftool -T -Filename -FileModifyDate -gpsposition -c "%.6f degrees" -Filename * | sed 's/://g'| sed 's/,\ /_/g'| sed 's/\ degrees\ //g'|awk '{print "mv " $1 " "$2$3"."$4"."$5}' > GPSInfo.sh ;chmod +x GPSInfo.sh
;;
subsecdtorig)
		exiftool -T -FileName -GPSPosition -c "%.6f" * > GPSInfo.txt
		exiftool -T -Filename -SubSecDateTimeOriginal -gpsposition -c "%.6f degrees" -Filename * | sed 's/://g'| sed 's/,\ /_/g'| sed 's/\ degrees\ //g'|awk '{print "mv " $1 " "$2$3"."$4"."$5}' > GPSInfo.sh;chmod +x GPSInfo.sh
;;
showdates_allfiles)
		exiftool -a -G1 -s -time:all *
;;
*)
    Message="Usage:"
        Message0="-----  gpsinfo crdate"
        Message1="-----  gpsinfo dttimeorig"
        Message2="-----  gpsinfo filemoddt"
        Message3="-----  gpsinfo subsecdtorig"
        Message4="-----  gpsinfo showdates_allfiles"
        Message5="-----  Type: \"exiftool -t filename\" to see the fields available."
    echo $Message
    echo $Message0
    echo $Message1
    echo $Message2
    echo $Message3
    echo $Message4
    echo $Message5
;;
esac
}
```
