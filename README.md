# === Create video from images in folder. 10 seconds per image (framerate 0.1 fps). Letterboxing: images are not stretched ===<br>

cat {\*.jpg,\*.jpeg} | ffmpeg -f image2pipe -r 0.1 -vcodec mjpeg -i - -vf "scale=1280:720:force_original_aspect_ratio=decrease,pad=1280:720:(ow-iw)/2:(oh-ih)/2" -vcodec libx264 out.mp4

# === Create video from images in folder. 11 seconds per image (framerate 25 fps). Letterboxing: images are not stretched ===

<br>
cat {\*.jpg,\*.jpeg} | ffmpeg -y -f image2pipe -vcodec mjpeg -i - -vf "setpts=11\*25*PTS","scale=1280:720:force_original_aspect_ratio=decrease,pad=1280:720:(ow-iw)/2:(oh-ih)/2" out.mp4

# === Create video from images in folder. 11 seconds per image (framerate 25 fps). Letterboxing: images are not stretched, Magenta Box===

<br>
find -E . -regex '.*(JPG|jpeg|jpg)' | sort -R | tr "\n" "\0" | xargs -0 cat |ffmpeg -y -f image2pipe -vcodec mjpeg -i - -vf "setpts=1*25*PTS","scale=1280:720:force_original_aspect_ratio=decrease,pad=1280:720:(ow-iw)/2:(oh-ih)/2":color=magenta out.mp4

# === MAC Create video from images. Random order ===<br>

find -E . -regex '.\*(JPG|jpeg|jpg)' | sort -R | tr "\n" "\0" | xargs -0 cat | ffmpeg -y -f image2pipe -vcodec mjpeg -i - -vf "setpts=1\*25\*PTS","scale=1280:720:force_original_aspect_ratio=decrease,pad=1280:720:(ow-iw)/2:(oh-ih)/2" out.mp4

# ===MAC Resize Image, set longest edge to x pixels ===<br>

sips -Z 719 \*.jpg

# === Youtube-dl ===<br>

youtube-dl --extract-audio --audio-format mp3 "https://www.youtube.com/watch?v=....."

# === normalize audio files ===<br>

ffmpeg -i input.wav -filter:a loudnorm output.wav

# === MAC resize images recursive fixed height ===<br>

find -E . -regex '.\*(JPG|jpeg|jpg)' | sort -R | tr "\n" "\0" | xargs -0 sips --resampleHeight 500

# === RPI ===<br>

sudo nano /etc/xdg/lxsession/LXDE-pi/autostart

@xset s noblank<br>
@xset s off<br>
@xset -dpms<br>

# === RPI is Console logon from SSH ===<br>

if [ -n "$SSH_CLIENT" ] || [ -n "$SSH_TTY" ]; then
SESSION_TYPE=remote/ssh
else
case $(ps -o comm= -p $PPID) in
sshd|\*/sshd) SESSION_TYPE=remote/ssh;;
esac
fi

# === Docker explore an image ===<br>

docker run -it --entrypoint=/bin/bash name-of-image  
(dann per CMD weitermachen)


# === Linux Mount Network Drive ===<br>

sudo mount -t cifs -o guest //WindowsPC/share1 /mnt/mountfoldername


# === Spotdl LDM ===<br>

docker run -v /Users/andyfischer/Documents/spotdl/docker/LDM22:/music spotdl/spotify-downloader download query "https://open.spotify.com/playlist/7MyAH7PSi9oEhesI2jlmLF?si=b84195fc651440e5"


# === MAC Recursively process *.wav files ===<br>

find -E . -regex '.*(wav)' | while read file; do<br>
	ffmpeg -i "./$file" "./${file%.*}.mp3";
done
