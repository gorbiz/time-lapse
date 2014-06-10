How I use this
==============
Me and my friend dedicated an Asus Eee PC to make time-lapse videos using an external HD webcam.
The computer is running the GNU/Linux distribution CrunchBang (based on Debian like Ubuntu).

Installing some software
------------------------
 - VLC (to capture stills from the webcam)
 - mencoder (to make the stills into videos)
 - screen (optional, but handy to keep track of the constantly running capturing process)
As CrunchBang comes with APT I can simply type this into a terminal
```sudo apt-get install vlc mencoder screen```

FIXME complete this


Make results accessible through Dropbox
---------------------------------------
Setting up a cron job similar to this might be helful
```*/15 * * * * cd ~/time-lapse && ./render_today && cp videos/today.avi ~/Dropbox/time-lapse/```
(Instead of copying you could perhaps use a symlink, Dropbox seem able to skrew it up at times thouh).

To synchronize the latest snapshot you could add a cron job like this
```* * * * * ls -t ~/time-lapse/snaps/*.png | head --lines=1 | xargs -i ln -sf {} ~/Dropbox/time-lapse/recent.png```
