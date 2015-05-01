Forvocl is a command-line tool for accessing the API provided by [Forvo](http://forvo.com/). Using forvocl you can list, play back, get information on, and save audio pronunciations contributed by users of the site.

* [1 Requirements](#requirements)
* [2 Installation](#installation)
  * [2.1 Installation from distro packages](#installation-from-distro-packages)
    * [2.1.1 User packaged](#user-packaged)
* [3 Usage](#usage)
  * [3.1 Searching and playback](#searching-and-playback)
  * [3.2 Options](#options)
  * [3.3 Audio format](#audio-format)
  * [3.4 Saving audio files to disk](#saving-audio-files-to-disk)
* [4 Issues](#issues)
* [5 Credits](#credits)
* [6 License](#license)

# Requirements
* mplayer
* a Forvo API key

# Installation
To install you can either download the project source and run the script directly, or use a package manager to install the appropriate files for your distro.

## Installation from distro packages
### User packaged
* ![logo](http://www.monitorix.org/imgs/archlinux.png "arch logo")Arch Linux: in the [AUR](https://aur.archlinux.org/packages/forvocl) and [Firef0x's Arch Linux Repository](http://firef0x.github.io/archrepo.html).

# Usage
Using the `forvocl.rb` script you can look up and play back audio pronunciations from [Forvo](http://forvo.com/). This requires registering for a [Forvo API key](http://api.forvo.com/), which is free for non-commercial educational use.

Once you have a key, you just need to copy it into your forvocl config file in your user home directory (i.e. `~/.config/forvocl/config.yml`) under the section "forvo key". Uncomment the line `# :forvo_key: ""` and add your key between the quotation marks `""`. Now you can look up pronunciations by running `forvocl.rb`.

## Location of configuration file

Forvocl will attempt to read a configuration file located at `~/.config/forvocl/config.yml`. If it does not find it there (or if the directory doesn't exist, it will try looking in a few other places before giving up:

1. If you use the [gdcl dictionary lookup tool](https://github.com/dohliam/gdcl) and have a `config.yml` file with a forvo key in `~/.config/gdcl`, there is no need to create a duplicate configuration file in the forvocl directory -- forvocl will read your key from the gdcl configuration.
2. If you prefer (or if installed by your package manager) you can use the xdg config folder instead, located at `/etc/xdg/forvocl`
3. As a last resort, forvocl will check for `config.yml` in the same folder as the `forvocl.rb` executable. This could be useful if you have downloaded the source and just want to try it out with minimal set up.

If the configuration file cannot be found in any of these locations, forvocl will exit with a message explaining the situation.

## Searching and playback
Forvocl has both interactive and non-interactive lookup modes. If run without any command-line arguments, it will prompt for a [language code](http://www.forvo.com/languages-codes/) and a word to pronounce. You can find a full list of the supported codes [here](http://www.forvo.com/languages-codes/).

You can skip the prompts by supplying the language code and word to be pronounced as arguments when running `forvocl.rb`, in the form `ruby forvocl.rb [lang_code] [word_to_be_pronounced]`. For example, if you wanted to find the pronounciation of the word "сегодня" in Russian, you would enter:

    ruby forvocl.rb ru сегодня

The last argument should probably be in quotes to avoid problems -- this also allows for pronunciation of phrases and other terms with spaces:

    ruby forvocl.rb sv "Johannes Robert Rydberg"

The script will let you know how many pronunciations were found and print out a numbered list (example below):

* command: `ruby forvocl.rb zh 发音`

* output:
```
4 pronunciations found for "发音" in zh:

  1. by Gliese (f from China)           0 [+1 -1]
  2. by witenglish (m from China)       0 [+0 0]
  3. by cloudrainner (m from China)     0 [+0 0]
  4. by JuliaWu (f from China)          0 [+0 0]


Select a number to hear the corresponding pronunciation, or press "a" to hear all available pronunciations.
```

To hear any of the listed pronunciations just enter the corresponding number and it will start playing automatically. If you press "a", all of the pronunciations will play in order. The numbers to the far right are the user rating that each pronunciation has received, in the format `rating [+upvotes -downvotes]`.

## Options
The Forvo script has a number of options that can be supplied at the command-line:

* `-m`, `--mp3` (_Use mp3 format instead of ogg_)
* `-l`, `--list` (_List all pronunciations_)
* `-u`, `--urls` (_Print a list of audio urls_)
* `-a`, `--play-all` (_Play back all pronunciations without interaction_)
* `-s`, `--save` (_Save all audio files to disk_)

Many of these options can be combined, for example:

`ruby forvocl.rb -lum en photogrammetry` (_Lookup the word "photogrammetry" and produce a list of pronunciations and urls in mp3 format_)

If you want to skip all interaction entirely and just play each audio result automatically, use the `-a` option and supply the language code and lookup terms on the command-line, e.g.:

    ruby forvocl.rb -a fr prononciation

## Audio format
By default, forvocl plays back and saves audio files in ogg format. If you want to switch to using mp3 format, just use the `-m` option.

## Saving audio files to disk
Once you have finished listening to the audio, forvocl will prompt you to enter a number from the list of available pronunciations to save the file to disk. If you don't want to save any of the audio, just press any other key to quit. To save all of the available audio files, use the `-s` option.

# Issues
If you get the following error when playing back audio: `mplayer: could not connect to socket`, it just means that you need to disable LIRC support in mplayer. You can do this quite easily by editing or creating the file `~/.mplayer/config` and adding the line:

            nolirc=yes

# Credits
This script was originally part of the [gdcl](https://github.com/dohliam/gdcl) command-line dictionary project.

Table of contents generated by [tocdown](https://github.com/dohliam/tocdown).

# License
MIT license -- see LICENSE file for details.

The audio pronunciations on forvo are licensed [cc-by-nc-sa](http://creativecommons.org/licenses/by-nc-sa/3.0/deed.en_GB).
