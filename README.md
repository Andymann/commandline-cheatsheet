==== Create video from images in folder. 10 seconds per image (framerate 0.1 fps). Letterboxing: images are not stretched ====<br>
cat {\*.jpg,\*.jpeg} | ffmpeg -f image2pipe -r 0.1 -vcodec mjpeg -i - -vf "scale=1280:720:force_original_aspect_ratio=decrease,pad=1280:720:(ow-iw)/2:(oh-ih)/2" -vcodec libx264 out.mp4

==== Create video from images in folder. 11 seconds per image (framerate 25 fps). Letterboxing: images are not stretched ====
<br>
cat {\*.jpg,\*.jpeg} | ffmpeg -y -f image2pipe -vcodec mjpeg -i - -vf "setpts=11\*25*PTS","scale=1280:720:force_original_aspect_ratio=decrease,pad=1280:720:(ow-iw)/2:(oh-ih)/2" out.mp4

=== MAC Create video from images. Random order ===<br>
find -E . -regex '.\*(JPG|jpeg|jpg)' | sort -R | tr "\n" "\0" | xargs -0 cat | ffmpeg -y -f image2pipe -vcodec mjpeg -i - -vf "setpts=1\*25*PTS","scale=1280:720:force_original_aspect_ratio=decrease,pad=1280:720:(ow-iw)/2:(oh-ih)/2" out.mp4

===MAC Resize Image, set longest edge to x pixels ===<br>
sips -Z 719 *.jpg


==== Youtube-dl ====<br>
youtube-dl --extract-audio --audio-format mp3 "https://www.youtube.com/watch?v=....."


==== normalize ===<br>
ffmpeg -i input.wav -filter:a loudnorm output.wav

=== MAC resize images recursive fixed height ===<br>
find -E . -regex '.*(JPG|jpeg|jpg)' | sort -R | tr "\n" "\0" | xargs -0 sips --resampleHeight 500

==== RPI ===<br>
sudo nano /etc/xdg/lxsession/LXDE-pi/autostart

@xset s noblank<br>
@xset s off<br>
@xset -dpms<br>

