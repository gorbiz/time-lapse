How I use this
==============
Me and my friend **dedicated** an Asus Eee **PC** to make **time-lapse videos** using an external HD **webcam**.
The computer is running the **GNU/Linux** distribution CrunchBang (based on Debian like Ubuntu).

Installing some software
------------------------
 - **VLC** (to capture stills from the webcam)
 - **mencoder** (to make the stills into videos)
 - screen (optional, handy to keep track of the constantly running capturing process)
 - cheese (optional, good for testing webcam and tweaking its position and angle)

As CrunchBang comes with APT I can simply
1. issue this in a terminal ```sudo apt-get install vlc mencoder screen cheese```
2. Now you might want to run ```cheese``` and try out your webcam, check it's resolution and what not.

Setting up the scripts
----------------------
1. Then we'll get the scripts ```git clone git@github.com:gorbiz/time-lapse.git```
2. ```cd time-lapse```
3. You might want to edit the capturing script ```nano start_capture```
4. When all looks good start capturing ```screen -S capturing ./start_capture```. XXX sometimes it breaks; try again :P. (Leave the screen by <kbd>Ctrl</kbd> + <kbd>a</kbd>, let go and hit <kbd>d</kbd>)

Photos should now stack up in the snaps/ folder. You can assemble all of them into a film clip using ```render_full``` or to include only today's ```render_today```. However you'll probably want to **modify these scripts** to your liking.

I like to automate all of that so I enter
```crontab -e``` and put something like this in there:
```
# Make a time-lapse video for today
*/15 * * * * cd ~/time-lapse && ./render_today && cp ~/time-lapse/videos/today.avi ~/Dropbox/plant-lapse/

# Make a time-lapse video from all photos (ever taken)
0 0 * * * cd ~/time-lapse && ./render_full && cp ~/time-lapse/videos/full.avi ~/Dropbox/plant-lapse/

# Put the latest snapshot in Dropbox
* * * * * ls -t ~/time-lapse/snaps/*.png | head --lines=1 | xargs -i cp {} ~/Dropbox/plant-lapse/recent.png
```