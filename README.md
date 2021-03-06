Music player
============

First, if you wonder about what is supposed to be a music player or what makes a music player different from a simple media player, read this: [What is a music player](https://github.com/albertz/music-player/blob/master/WhatIsAMusicPlayer.md)

Annoyed by all existing players because some subset of:

* not open source
* missing sound format ([FLAC](http://flac.sourceforge.net/itunes.html), Ogg, ...)
* bugs ([1](http://bugzilla.songbirdnest.com/show_bug.cgi?id=23640), [2](http://bugzilla.songbirdnest.com/show_bug.cgi?id=25023), [3](http://bugzilla.songbirdnest.com/show_bug.cgi?id=25042), [4](http://bugzilla.songbirdnest.com/show_bug.cgi?id=18503), [5](http://bugzilla.songbirdnest.com/show_bug.cgi?id=18505), [6](http://bugzilla.songbirdnest.com/show_bug.cgi?id=18480), [7](http://bugzilla.songbirdnest.com/show_bug.cgi?id=18478), [8](http://bugzilla.songbirdnest.com/show_bug.cgi?id=25073), [9](http://bugzilla.songbirdnest.com/show_bug.cgi?id=25024), [10](http://bugzilla.songbirdnest.com/show_bug.cgi?id=5975), ...)
* missing output possibility (RAOP, PulseAudio, ...)
* no or too limited DJ mode
* no library / database

Features of this player:

* open source
* simple
* support of most important sound formats
* advanced intelligent DJ mode
* simple music database
* ReplayGain / audio volume normalization
* Last.fm
* AcoustID fingerprint

![MusicPlayer screenshot](https://github.com/albertz/music-player/raw/master/screenshot.png)

About the DJ mode, what I want (maybe some of these somewhat configurable):

* continuously always add songs
* liked songs more often
* context-based choices, e.g. related songs more likely
* possibility to easily manually add songs to the list
* easy way to restrict to a subset of songs (like a genre, a playlist, a filesystem directory, etc.)

About the database:

* main function: search
* should be fast and optional for playback, i.e. music can be played even when the database is currently not ready for some reason
* file-entries located on the local filesystem which don't exist anymore should automatically be deleted
* file-entries located on a network filesystem which is not mounted should be marked as currently-not-available
* file-entries located on a network filesystem which is mounted which don't exist anymore should automatically be deleted
* should automatically be filled by a filesystem directory
* import like-state from local players like iTunes and also online services like Last.fm

TODO / possible additional missing features:

* [Gapless playback](http://en.wikipedia.org/wiki/Gapless_playback). I think ffmpeg provides some way to get the exact specified start/end of a song. Otherwise this is just a question of buffering.
* BPM determination and clever DJ-like fading
* echoprint.me or similar song determination (mostly for metadata, esp. if missing)
* use tags given by Last.fm (mostly more tags)
* Last.fm streaming support
* watch music directory for changes (e.g. new files added)

Installation:

So far, there is a prebuild MacOSX app bundle in the download section which should just work. Otherwise, to get the source working, you need these requirements (e.g. install on MacOSX via Homebrew):

* ffmpeg
* portaudio
* chromaprint

(Debian/Ubuntu: `apt-get install python-dev libsnappy-dev libtool yasm libchromaprint-dev portaudio19-dev`. FFmpeg in Debian/Ubuntu is too old (lacks libswresample), so either do `add-apt-repository ppa:jon-severinsson/ffmpeg && apt-get update && apt-get install libavformat-dev libswresample-dev` or install it from source. [Chromaprint](http://acoustid.org/chromaprint) depends on FFmpeg, so if you have a custom FFmpeg install, you might also want to install that manually. `./configure && make && sudo make install` should work for FFmpeg and PortAudio. You might also want to use `--enable-shared` for FFmpeg. `cmake . && sudo make install` for Chromaprint.)

Then call `./compile.py` to build the Python modules (it will build the Python modules `ffmpeg.so` and `leveldb.so`).

To start the player, just call `./main.py`.

The current GUI is Cocoa only. Additional Qt support is planned. The music player also works without any GUI.

Authors:

* Albert Zeyer, <http://www.az2000.de>: founder of the project, main core, ffmpeg module, etc.
* Bryan Joseph, <http://bryaninspired.com>: database

