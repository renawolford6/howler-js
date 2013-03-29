## 1.1.0-b1 (March 25, 2013)
- `ADDED:` New `pos3d` method that allows for positional audio (Web Audio API only).
- `ADDED:` Multi-playback control system that allows for control of specific play instances when sprites are used. A callback has been added to the `play` method that returns the `soundId` for the playback instance. This can then be passed as the optional last parameter to other methods to control that specific playback instead of the whole sound object.
- `ADDED:` Pass the `Howl` object reference as the first parameter in the custom event callbacks.
- `ADDED:` New optional parameter in sprite defintions to define a sprite as looping rather than the whole track. In the sprite definition array, set the 3rd value to true for looping (`spriteName: [pos, duration, loop]`).
- `FIXED:` Improved implementation of Web Audio API looping.
- `FIXED:` Issue that caused the fallback to not work when testing locally.
- `FIXED:` Various code cleanup and optimizations.

## 1.0.13 (March 20, 2013)
- `ADDED:` Support for AMD loading as a module (thanks @mostlygeek).

## 1.0.12 (March 28, 2013)
- `ADDED:` Automatically switch to HTML5 Audio if there is an error due to CORS.
- `FIXED:` Check that only numbers get passed into volume methods.

## 1.0.11 (March 8, 2013)
- `ADDED:` Exposed `usingWebAudio` value through the global `Howler` object.
- `FIXED:` Issue with non-sprite HTML5 Audio clips becoming unplayable (thanks Paul Morris).

## 1.0.10 (March 1, 2013)
- `FIXED:` Issue that caused simultaneous playback of audio sprites to break while using HTML5 Audio.

## 1.0.9 (March 1, 2013)
- `ADDED:` Spec-implementation detection to cover new and deprecated Web Audio API methods (thanks @canuckistani).

## 1.0.8 (February 25, 2013)
- `ADDED:` New `onplay` event.
- `ADDED:` Support for playing audio from base64 encoded strings.
- `FIXED:` Issue with soundId not being unique when multiple sounds were played simultaneously.
- `FIXED:` Verify that an HTML5 Audio Node is ready to play before playing it.
- `FIXED:` Issue with `onend` timer not getting cleared all the time.

## 1.0.7 (February 18, 2013)
- `FIXED:` Cancel the correct timer when multiple HTML5 Audio sounds are played at the same time.
- `FIXED:` Make sure howler.js is future-compatible with UglifyJS 2.
- `FIXED:` Duration now gets set correctly when pulled from cache.
- `FIXED:` Tiny typo in README.md (thanks @johnfn).

## 1.0.6 (February 8, 2013)
- `FIXED:` Issue with global mute calls happening before an HTML5 Audio element is loaded.

## 1.0.5 (February 7, 2013)
- `FIXED:` Global mute now also mutes all future sounds that are played until `unmute` is called.

## 1.0.4 (February 6, 2013)
- `ADDED:` Support for WebM audio.
- `FIXED:` Issue with volume changes when on HTML5 Audio.
- `FIXED:` Round volume values to fix inconsistencies in fade in/out methods.

## 1.0.3 (February 2, 2013)
- `FIXED:` Make sure `self` is always defined before returning it. 

## 1.0.2 (February 1, 2013)
- `ADDED:` New `off` method that allows for the removal of custom events.
- `FIXED:` Issue with chaining the `on` method.
- `FIXED:` Small typo in documentation.

## 1.0.1 (January 30, 2013)
- `ADDED:` New `buffer` property that allows you to force the use of HTML5 on specific sounds to allow streaming of large audio files.
- `ADDED:` Support for multiple events per event type.
- `FIXED:` Issue with method chaining before a sound was ready to play.
- `FIXED:` Use `self` everywhere instead of `this` to maintain consistency.

## 1.0.0 (January 28, 2013)
- First commit