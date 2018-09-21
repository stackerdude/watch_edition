# Adding Sound Effects to The Watch #

You can add sound effects to the watch alerts and buttons with the watch's AudioHub. 

1. Download any .mp3 file from the Internet. [This](https://www.zapsplat.com/sound-effect-categories/) website is a good source for audio files. . For the purpose of this tutorial we'll say we have an audio file `demo.mp3`. 

2. Move your chosen sound effect to `client/src/sounds/`. This is where all audio files are and will be stored. 

3. Now you can access and play the sound effects via the AudioHub using `AudioHub.playSound('./client/src/sounds/demo.mp3',1);`. The second parameter is volume control, 0 being no sound and 1 being the loudest. If no parameter is provided, the volume is 1 by default.