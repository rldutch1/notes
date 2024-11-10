#imagemagick
<pre>
Adding a background image to a current image: 
<span style="color: #3366ff;">
  The background image is: zzz.png 
  The current image is: Wisdom_from_Aiko1.png
  The new image with background is: WfA2.png
    magick -size 570x873 tile:zzz.png -gravity center Wisdom_from_Aiko1.png WfA2.png
</span>

Function Resize:
<span style="color: #3366ff;">
  Resize(){
  #convert -resize 1024x768 $i re_1024x768_$i
  #magick s1.png -resize 120x120 s1_120x120.png
  #magick -resize s1.png 50x50 re_50x50_s1.png
  if [ $# -eq 0 ]
  then
  echo "Usage: Resize filename.xxx size"
  echo "Example: Resize picture.jpg 1024x768"
  else
  echo "Resizing $1 to $2 ..."
  	#convert -resize $1 $2 re_$1_$2
  	magick $1 -resize $2 re_$2_$1
  fi
  }
</span>

Function ResizeAll:
<span style="color: #3366ff;">
  ResizeAll(){
  if [ $# -ne 3 ]
  then
  echo "You can resize and convert image format or just resize."
  echo "Example: ResizeAll png png 800x600"
  echo "or resize and convert ..."
  echo "Example: ResizeAll png jpg 800x600"
  #/home/rob/Pictures/Screenshots/z_test
  else
  echo "echo 'Resizing $1 to $2 at $3.'"
  let a=1
  for i in *.$1; 
  do 
  	#echo magick "$i"\'[$3]\' ${i%.$1}_$a.$2;
  	#echo magick "$i"\'[$3]\' ${i%.$1}_%003d.$2;
  	echo magick "$i"\'[$3]\' ${i%.$1}_$3.$2;
  	#/usr/bin/magick "$i"\'[$3]\' ${i%.$1}_$3.$2;
  	#magick "$i" ${i%.$1}.$2; 
    a=$(( $a + 1 ))
  done
  fi
  }
</span>

Function Convert:
<span style="color: #3366ff;">
  Convert(){
  #convert -resize 1024x768 $i re_1024x768_$i
  #for image in *.png;do magick "$image" "${image%.*}.gif"; done
  #for image in *.$1; do magick "$image" "${image%.*}.$2"; done
  
  if [ $# -ne 2 ]
  then
  echo "Convert from one image format to another:  "
  echo "Usage: Convert png jpg  "
  echo " "
  echo "|-------To simultaneously convert and resize----------|"
  echo "| magick 'theimagename.jpg[800x600]' newimagename.png |"
  echo "|-----------------------------------------------------|"
  else
  echo "Converting $1 to $2 ..."
  #	for i in $( ls * |awk '{print $9}' ); do convert -resize $1 $i $1_$i ; done
  	#for i in $( ls *.PNG |awk '{print $9}' ); do convert -resize 1024x768 $i re_1024x768_$i; done
  	#for i in $( printf "%s\n" * ); do convert -resize $1 $i $1_$i ; done
  	for image in *.$1; do magick "$image" "${image%.*}.$2"; done
  fi
  }
</span>
</pre>
