#Youtube-DL (YT-DLP)

####To download a single video or an entire playlist from YouTube, simply enter the URL in the following format:
<span style="color: #3366ff;">
	yt-dlp https://www.youtube.com/watch?v=t5b20oLaIaw<br />
 </span>

####To download a video or playlist to a specific location, use the -o flag followed by the target directory. For example:
<span style="color: #3366ff;">
	yt-dlp -o '~/Downloads/Abdul Kalam Biography' https://www.youtube.com/watch?v=t5b20oLaIaw<br />
 </span>

####To include additional details in the filename, such as the title, uploader name, upload date, and playlist name, use the following format:
<span style="color: #3366ff;">
	yt-dlp -o '%(title)s by %(uploader)s on %(upload_date)s in %(playlist)s.%(ext)s' https://www.youtube.com/watch?v=t5b20oLaIaw
  <ul>Here is a breakdown of the different options used in the above commands:
  <ul>
  <li>yt-dlp: The name of the command-line tool used to download videos and playlists.</li>
  <li>-o: The flag used to specify the output filename or directory.</li>
  <li>%(title)s: The title of the video or playlist.</li>
  <li>%(uploader)s: The name of the video or playlist uploader.</li>
  <li>%(upload_date)s: The date on which the video or playlist was uploaded.</li>
  <li>%(playlist)s: The name of the playlist, if the video is part of a playlist.</li>
  <li>%(ext)s: The file extension of the downloaded video or audio file.</li>
  </ul>
  </ul>
 </span>

####You can download multiple videos by specifying their URLs in the command, separated by spaces like so:
<span style="color: #3366ff;">
	yt-dlp <url1> <url2><br />
		or use a text file<br />
	yt-dlp -a url.txt<br />
 </span>

####Download Audio-only from a Video:
####To download a video as Audio i.e. extract audio from a video, use -x flag like below.
<span style="color: #3366ff;">
	yt-dlp -x https://www.youtube.com/watch?v=t5b20oLaIaw<br />
 </span>

######You can also specify the output audio format using the -x --audio-format flag.
<span style="color: #3366ff;">
	yt-dlp -x --audio-format mp3 https://www.youtube.com/watch?v=t5b20oLaIaw<br />
 </span>

####To download a video along with its accompanying details, including description, metadata, annotations, subtitles, and thumbnail, use the following command:
<span style="color: #3366ff;">
	yt-dlp --write-description --write-info-json --write-annotations --write-sub --write-thumbnail <URL><br />
 </span>

####These commands provide you with an overview of the various formats in which the content is accessible, assisting you in making an informed selection.
####To view a comprehensive list of all the available formats for a video or playlist, utilize the following command:
<span style="color: #3366ff;">
	yt-dlp --list-formats https://www.youtube.com/watch?v=t5b20oLaIaw<br />
	Alternatively, you can achieve the same result with -F flag:<br />
	yt-dlp -F https://www.youtube.com/watch?v=t5b20oLaIaw<br />
<ul>
	<ul>As you see from the output, yt-dlp presents a comprehensive display of all the accessible video formats in an organized tabular column. Moving from left to right, this display includes essential details such as
  <li>ID,</li>
  <li>Extension (EXT),</li>
  <li>Resolution,</li>
  <li>Frames Per Second (FPS),</li>
  <li>Channel (CH),</li>
  <li>Filesize,</li>
  <li>Total Bitrate (TBR),</li>
  <li>Protocol (PROTO),</li>
  <li>Video Codec (VCODEC),</li>
  <li>Video Bitrate (VBR),</li>
  <li>Audio Codec (ACODEC),</li>
  <li>Audio Bitrate (ABR),</li>
  <li>Audio Sampling Rate (ASR),</li>
  <li>and additional information.</li>
	</ul>
</ul>
 </span>

####Download vidoes by ID or video format:
<span style="color: #3366ff;">
    By ID:<br />
    yt-dlp -f 247 https://www.youtube.com/watch?v=t5b20oLaIaw<br />
    using -f 22/17/18 means it will attempt to download format 22 if available, then format 17 if format 22 is not available, and so on.<br />
    <br />
    By Format: <br />
    To download video(s) in your preferred format, such as MP4, simply execute the following command:<br />
    yt-dlp -f mp4 https://www.youtube.com/watch?v=t5b20oLaIaw<br />
    yt-dlp -f 'bestvideo[ext=mp4]+bestaudio[ext=m4a]/best[ext=mp4]/best' https://www.youtube.com/watch?v=t5b20oLaIaw<br />
    yt-dlp -f mp4 -o '%(title)s.f%(format_id)s.%(ext)s' https://www.youtube.com/watch?v=t5b20oLaIaw<br />
 </span>

[Source:](https://ostechnix.com/yt-dlp-tutorial/)<br />