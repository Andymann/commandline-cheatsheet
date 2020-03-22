==== Create video from images in folder. 10 seconds per image (0.1). Letterboxing: images are not stretched ====<br>
cat {*.jpg,*.jpeg} | ffmpeg -y -f image2pipe -r 0.1 -vcodec mjpeg -i - -vf "scale=1280:720:force_original_aspect_ratio=decrease,pad=1280:720:(ow-iw)/2:(oh-ih)/2" out.mp4
