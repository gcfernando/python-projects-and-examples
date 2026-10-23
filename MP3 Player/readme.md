# Python MP3 Player with Crossfade — pygame Console Music Player

A console-based **MP3 player written in Python** with crossfade transitions between tracks, background preloading of the next song, and shuffled playback, built on `pygame.mixer` and `mutagen`.

<a id="overview"></a>

## 🔎 Overview

This script plays `.mp3` files from a folder you specify in a shuffled order. It uses two `pygame` mixer channels to overlap playback and preloads the next track in a background thread. If preloading is not ready, it loads synchronously, which can cause a gap or glitch.

<a id="features"></a>

## ✨ Features

- Shuffle playback of all `.mp3` files in a given folder
- Crossfade between tracks (configurable duration and trigger time)
- Background preloading of the next track via a daemon thread
- Animated "Playing..." indicator in the console
- Displays previous, current, and next track names, with a duration for the current track
- Console window title updated to show the currently playing track
- Windows system-sleep prevention while music plays (`SetThreadExecutionState` with `ES_SYSTEM_REQUIRED`; the display can still turn off)
- Cleanup after the main playback loop exits; `Ctrl+C` is not handled by a surrounding `try/finally`

<a id="requirements"></a>

## 📦 Prerequisites and installation

```text
pygame
mutagen
colorama
```

Install dependencies:

```bash
python -m pip install pygame mutagen colorama
```

<a id="configuration"></a>

## ⚙️ Configuration

Two constants in the script control the crossfade behavior:

| Constant | Default | Description |
|---|---|---|
| `CROSSFADE_MS` | `5000` | Duration of the fade effect in milliseconds (5 seconds) |
| `CROSSFADE_START_TIME_S` | `15` | How many seconds before a song ends to begin the crossfade |

<a id="usage"></a>

## 💡 Usage

From the `Console_Code` folder:

```bash
python MP3Player.py
```

When prompted, enter the full path to your music folder:

```text
Enter music folder path: C:\Music\Playlist
```

The player will shuffle the playlist, preload the first track, and begin playback automatically.

## How It Works

1. All `.mp3` files in the folder are discovered and shuffled.
2. The pygame mixer is initialized with two channels.
3. Before the main loop starts, the first track is preloaded in a background thread.
4. When a track is playing, a second background thread preloads the next one.
5. When `CROSSFADE_START_TIME_S` seconds remain, the inactive channel fades in the next track while the active channel fades out.
6. Channels swap roles after each transition.

<a id="file-structure"></a>

## 🏗️ Architecture

```text
MP3 Player/
└── Console_Code/
    └── MP3Player.py    # Main script
```

<a id="notes"></a>

## 🛠️ Troubleshooting and limitations

- The playlist index wraps with modulo arithmetic; the shuffled order can repeat rather than stop after one pass. A single track can also restart when it reaches the crossfade trigger.
- The default transition starts 15 seconds before the end but fades out over 5 seconds, so approximately the final 10 seconds of the outgoing track are cut off. Align the trigger and fade duration if you want a different overlap.
- `pygame.mixer.Sound` loads whole tracks into memory; background preloading is not a streaming decoder. Large files can increase memory usage and load time.
- Interrupting with `Ctrl+C` can skip the explicit cleanup code because the main loop has no interrupt handler or `finally` block.
- Only `.mp3` files are supported.
- If a track fails to load, it is skipped and the next track loads.
- On non-Windows systems, the console title is set with an ANSI escape sequence; sleep prevention is only available on Windows.
- Track lengths are read with `mutagen` so the player knows when to start the crossfade.

Background preloading shares a single `next_sound` variable without a track identity or lock. Overlapping preload and synchronous fallback work can race, so the displayed filename should not be treated as proof that the matching audio buffer is playing. Unreadable tracks can also cause repeated retries in the looping playlist.

<a id="related-projects"></a>

## 🔗 Related documentation

- [MP3 Tags — read ID3 metadata](../MP3%20Tags/readme.md)
- [Improve MP3 Quality — re-encode MP3 files](../Improve%20MP3%20Quality/readme.md)
- [Audio8D — 8D audio converter](https://github.com/gcfernando/audio-8d)
- [Back to all Python projects](../README.md)

---

## Documentation links

[Read all Python Projects and Code Examples guides online](https://gcfernando.github.io/python_codes/documentation/) · [Project overview](https://gcfernando.github.io/python_codes/) · [All developer projects](https://gcfernando.github.io/gcfernando/projects/)
