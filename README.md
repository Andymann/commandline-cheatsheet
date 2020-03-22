==== Create video from images in folder. 10 seconds per image (framerate 0.1 fps). Letterboxing: images are not stretched ====<br><br>
cat {*.jpg,*.jpeg} | ffmpeg -f image2pipe -r 0.1 -vcodec mjpeg -i - -vf "scale=1280:720:force_original_aspect_ratio=decrease,pad=1280:720:(ow-iw)/2:(oh-ih)/2" -vcodec libx264 out.mp4
