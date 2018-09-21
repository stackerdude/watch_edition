Adding sounds to the watch is relatively easy using the framework's AudioHub. Sounds can be particularly useful when you want to add effects such as alarms or notification sound effects.

# Play a Sound on the Watch #

Let's add an existing sound to one of the buttons on the watch.

1. Navigate to `./client/src/sounds`. In this directory, you should see the mp3 file `plop.mp3`. Now let's make this sound play whenever the left button is pressed from the homepage.

2. AudioHub has one function called `playSound` which takes two parameters. The first parameter takes the file path for the sound you want to use (In our case, it is `./client/src/sounds`.) The second parameter is optional and controls the volume and if let blank, the volume will default to 100%.

3. Navigate to `./client/src/js/pages/homePage.js`. In the `leftButtonEvent()` function, add the line `AudioHib.playSound("./client/src/sounds").

4. Now when you press the left button from the homepage, it should play a 'plop' sound!

5. Once you're satisfied you've understood this tutorial, feel free to delete this line from the code!

# Adding New Sound Effects and Changing Volume #

You can add new sound effects to the watch by adding them to the `sound` folder. 

1. Download any .mp3 file from the Internet. [This](https://www.zapsplat.com/sound-effect-categories/) website is a good source for audio files. . For the purpose of this tutorial we'll say we have an audio file called `demo.mp3`. 

2. Move your chosen sound effect to `./client/src/sounds/`. This is where all your audio files will be stored. 

3. Follow the same steps as above, but instead of using `plop.mp3`, use your custom `demo.mp3`. For the second parameter, the volume control, try using a number in between 0 being 0% and 1 being 100%. (For example, 0.5 would be 50% volume).

4. Now when you press the left button from the homepage, it should play the sound you downloaded with the volume you have specified!

5. Once you're satisfied you've understood this tutorial, feel free to delete this line from the code!