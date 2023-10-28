<p align="center"><img src="extra/kunst_logo.png"><br><sub>✨ Download and display album art or display embedded album art  ✨</sub></p>

This is a fork of [kunst](https://github.com/sdushantha/kunst) with less features.
I removed all features that I did not need.
What is left is that kunst will wait for a song change and then look for `cover.jpg/png/webp` images in the songs folder.
If found the image will be copied to `/tmp/kunst.jpg` and resized.

See [Display album art](#display-album-art) on how I display the images.

`kunst` is a daemon that extracts the album art from the songs playing in `mpd` and saves them in `/tmp`. It doesn't loop on a timer, instead it waits for `mpd` to send a `player` event. When it receives a `player` event, it wakes up and extracts the album art of the current playing track. This makes `kunst`really lightweight and makes it idle at `~0%` CPU usage. If there is no album art found, it will show a placeholder.


<p align="left">
<img src="extra/demo.gif">
</a>
</p>

## Dependencies
- `convert` (`imagemagick`)
- `bash`
- `mpc`


## Installation

### Install using `make`

```bash
# Clone the repo
$ git clone https://github.com/CodeWithMa/kunst.git

# Change your current directory to kunst
$ cd kunst

# Install it
$ sudo make install
```

### Run it from source

```bash
# Clone the repo
$ git clone https://github.com/CodeWithMa/kunst.git

# Change your current directory to kunst
$ cd kunst

# Run it
$ ./kunst
```

## Usage

```bash
$ kunst --help
usage: kunst [-h|--help] [--size "px"]
             [--music_dir "path/to/dir/"] [--verbose] [--version]

┬┌─┬ ┬┌┐┌┌─┐┌┬┐
├┴┐│ ││││└─┐ │
┴ ┴└─┘┘└┘└─┘ ┴
Find album art for the currently playing song in MPD

optional arguments:
   -h, --help            show this help message and exit
   --size                what size to display the album art in
   --music_dir           the music directory which MPD plays from
   --verbose             show the output
   --version             show the version of kunst you are using
```

## Configure

You can configure `kunst` through environment variables.

```bash
# The size of the album art to be displayed
export KUNST_SIZE="250x250"

# Where your music is located
export KUNST_MUSIC_DIR="/home/username/Music/"
```

## Display album art

I use `feh` do display the image written to `/tmp/kunst.jpg`.
`feh` will automatically switch to a new image if it changes on disk.

``` bash
feh --image-bg black -Z -. /tmp/kunst.jpg
```

## License

MIT License

Copyright © 2019 Siddharth Dushantha
Modified by CodeWithMa 2023
