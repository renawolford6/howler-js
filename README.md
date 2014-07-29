![howler.js](http://goldfirestudios.com/proj/howlerjs/howlerjs_logo.png "howler.js")

## Description
[**howler.js**](http://howlerjs.com) is an audio library for the modern web. It defaults to [Web Audio API](https://dvcs.w3.org/hg/audio/raw-file/tip/webaudio/specification.html) and falls back to [HTML5 Audio](http://www.whatwg.org/specs/web-apps/current-work/#the-audio-element).

More documentation, examples and demos can be found at **[howlerjs.com](http://howlerjs.com)**.

### Features
* Defaults to Web Audio API
* Falls back to HTML5 Audio
* Supports multiple file formats to support all browsers
* Automatic caching for Web Audio API
* Implements cache pool for HTML5 Audio
* Per-sound and global mute/unmute and volume control
* Playback of multiple sounds at the same time
* Easy sound sprite definition and playback
* Fade in/out sounds
* Supports Web Audio 3D sound positioning
* Methods can be chained
* Uses no outside libraries, just pure Javascript
* Lightweight, 9kb filesize (3kb gzipped)

### Browser Compatibility
Tested in the following browsers/versions:
* Google Chrome 7.0+
* Internet Explorer 9.0+
* Firefox 4.0+
* Safari 5.1.4+
* Mobile Safari 6.0+ (after user input)
* Opera 12.0+

## Documentation

### Examples

##### Most basic, play an MP3:
```javascript
var sound = new Howl({
  src: ['sound.mp3']
});

sound.play();
```

##### More playback options:
```javascript
var sound = new Howl({
  src: ['sound.mp3', 'sound.ogg', 'sound.wav'],
  autoplay: true,
  loop: true,
  volume: 0.5,
  onend: function() {
    console.log('Finished!');
  }
});
```

##### Define and play a sound sprite:
```javascript
var sound = new Howl({
  src: ['sounds.mp3', 'sounds.ogg'],
  sprite: {
    blast: [0, 1000],
    laser: [2000, 3000],
    winner: [4000, 7500]
  }
});

// shoot the laser!
sound.play('laser');
```

### Properties
* **src**: `Array` *(`[]` by default)* The sources to the track(s) to be loaded for the sound (URLs or base64 data URIs). These should be in order of preference, howler.js will automatically load the first one that is compatible with the current browser. If your files have no extensions, you will need to explicitly specify the extension using the `ext` property.
* **volume**: `Number` *(`1.0` by default)* The volume of the specific track, from `0.0` to `1.0`.
* **html5**: `Boolean` *(`false` by default)* Set to `true` to force HTML5 Audio. This should be used for large audio files so that you don't have to wait for the full file to be downloaded and decoded before playing.
* **loop**: `Boolean` *(`false` by default)* Set to `true` to automatically loop the sound forever.
* **preload**: `Boolean` *(`true` by default)* Automatically begin downloading the audio file when the `Howl` is defined.
* **autoplay**: `Boolean` *(`false` by default)* Set to `true` to automatically start playback when sound is loaded.
* **sprite**: `Object` *(`{}` by default)* Define a sound sprite for the sound. The offset and duration are defined in milliseconds. A third (optional) parameter is available to set a sprite as looping.
```
Example:
{
  key: [offset, duration, (loop)]
}
```
* **rate**: `Number` *(`1.0` by default)* The rate of playback. 0.5 to 4.0, with 1.0 being normal speed.
* **pool**: `Number` *(`5` by default)* The size of the inactive sounds pool. Once sounds are stopped or finish playing, they are marked as ended and ready for cleanup. We keep a pool of these to recycle for improved performance. Generally this doesn't need to be changed. It is important to keep in mind that when a sound is paused, it won't be removed from the pool and will still be considered active so that it can be resumed later.
* **ext**: `Array` *(`[]` by default)* howler.js automatically detects your file format from the extension, but you may also specify a format in situations where extraction won't work.
* **onload**: `Function` Fires when the sound is loaded.
* **onloaderror**: `Function` Fires when the sound is unable to load.
* **onplay**: `Function` Fires when the sound begins playing. The first parameter is the ID of the sound.
* **onend**: `Function` Fires when the sound finishes playing (if it is looping, it'll fire at the end of each loop). The first parameter is the ID of the sound.
* **onpause**: `Function` Fires when the sound has been paused. The first parameter is the ID of the sound.
* **onfaded**: `Function` Fires when the current sound finishes fading in/out. The first parameter is the ID of the sound.

### Methods
* **play**: Begins playback of sound. Will continue from previous point if sound has been previously paused.
  * *sprite*: `String` (optional) Plays from the defined sprite key.
  * *callback*: `Function` (optional) Fires when playback begins and returns the `soundId`, which is the unique identifier for this specific playback instance.
* **pause**: Pauses playback of sound, saving the `pos` of playback.
  * *id*: `Number` (optional) The play instance ID.
* **stop**: Stops playback of sound, resetting `pos` to `0`.
  * *id*: `Number` (optional) The play instance ID.
* **mute**: Mutes the sound, but doesn't pause the playback.
  * *id*: `Number` (optional) The play instance ID.
* **fade**: Fade a currently playing sound between two volumes.
  * *from*: `Number` Volume to fade from (`0.0` to `1.0`).
  * *to*: `Number` Volume to fade to (`0.0` to `1.0`).
  * *duration*: `Number` Time in milliseconds to fade.
  * *callback*: `Function` (optional) Fires when fade is complete.
  * *id*: `Number` (optional) The play instance ID.
* **loop**: Get/set whether to loop the sound.
  * *loop*: `Boolean` (optional) To loop or not to loop, that is the question.
* **seek**: Get/set the position of playback.
  * *position*: `Number` (optional) The position to move current playback to (in seconds).
  * *id*: `Number` (optional) The play instance ID.
* **volume**: Get/set volume of this sound.
  * *volume*: `Number` (optional) Volume from `0.0` to `1.0`.
  * *id*: `Number` (optional) The play instance ID.
* **on**: Call/set custom events. Multiple events can be added by calling this multiple times.
  * *event*: `String` Name of event to fire/set.
  * *function*: `Function` (optional) Define function to fire on event.
* **off**: Remove custom events that you've set.
  * *event*: `String` Name of event.
  * *function*: `Function` (optional) The listener to remove.
* **unload**: Unload and destroy a Howl object. This will immediately stop all play instances attached to this sound and remove it from the cache.

### Global Methods
The following methods are used to modify all sounds globally, and are called from the `Howler` object.

* **mute**: Mutes all sounds.
* **unmute**: Unmutes all sounds and restores them to their previous volume.
* **volume**: Get/set the global volume for all sounds.
  * *volume*: `Number` (optional) Volume from `0.0` to `1.0`.
* **codecs**: Check supported audio codecs.
  * *ext*: `String` File extension. One of: "mp3", "opus", "ogg", "wav", "aac", "m4a", "mp4", "weba".

### iOS Playback
By default, audio on iOS is locked until a sound is played within a user interaction, and then it plays normally the rest of the page session ([Apple documentation](https://developer.apple.com/library/safari/documentation/audiovideo/conceptual/using_html5_audio_video/PlayingandSynthesizingSounds/PlayingandSynthesizingSounds.html)). The default behavior of howler.js is to attempt to silently unlock audio playback by playing an empty buffer on the first `touchstart` event. This behavior can be disabled by calling:

```javascript
Howler.iOSAutoEnable = false;
```

## License

Copyright (c) 2013-2014 James Simpson and GoldFire Studios, Inc.

Released under the MIT License.
