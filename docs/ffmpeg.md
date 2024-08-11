#FFMPEG
<pre>
Convert m4a to mp3:
	<span style="color: #3366ff;">ffmpeg -i input.m4a -c:a libmp3lame -q:a 8 output.mp3</span>

Convert .flv videos to .mp4"
	<span style="color: #3366ff;">ffmpeg -i Videoname.flv -vcodec copy -acodec copy Videoname.mp4</span>

Convert file1 to file2:
	<span style="color: #3366ff;">ffmpeg -i $1 -vcodec copy -acodec copy $2</span>

Convert mp4 to webm:
	<span style="color: #3366ff;">ffmpeg -i test.mp4 -c:v libvpx-vp9 -crf 30 -b:v 0 -b:a 128k -c:a libopus test.webm</span>

Bash script to convert multiple Sony mts files to mp4 files:
  <span style="color: #3366ff;">
  	ffmpegbatch(){
      if [ $# -ne 2 ]
      then
      echo .     Usage: ffmpegbatch MTS mp4
      else
      for f in *.$1;
      do
      ffmpeg -i $f -vcodec copy -acodec copy ${f%$1}$2;
      done
      fi
  	}
  </span>

Bash script to convert multiple .wav files to .mp3 and .ogg files:
Source: https://superuser.com/questions/373889/batch-convert-wav-to-mp3-and-ogg
<span style="color: #3366ff;">
	for f in *.{wav,WAV}; 
	do 
			ffmpeg -i "$f" -c:a libmp3lame -q:a 2 "${f%.*}.mp3" -c:a libvorbis -q:a 4 "${f%.*}.ogg"; 
	done
	</span>
<span style="color: #3366ff;"></span>

<span style="color: #3366ff;"></span>
</pre>