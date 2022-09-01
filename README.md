# Audio player component for esp32

## Capabilities

* MP3 decoding (via libhelix-mp3)
* Wav/wave file decoding

## Who is this for?

Decode only audio playback on esp32 series of chips, where the features and footprint of esp-adf are not 
necessary.

## What about esp-adf?

This component is not intended to compete with esp-adf, a much more fully developed
audio framework.

It does however have a number of advantages at the moment including:

* Fully open source (esp-adf has a number of binary modules at the moment)
* Minimal size (it's less capable, but also simpler, than esp-adf)

## Dependencies

For MP3 support you'll need the [esp-libhelix-mp3](https://github.com/chmorgan/esp-libhelix-mp3) component.

## Tests

Unity tests are implemented in the [test/](../test) folder.

## States

```mermaid
stateDiagram-v2
    [*] --> Idle : new(), cb(IDLE)
    Idle --> Playing : play(), cb(PLAYING)
    Playing --> Paused : pause(), cb(PAUSE)
    Paused --> Playing : resume(), cb(PLAYING)
    Playing --> Playing : play(), cb(COMPLETED_PLAYING_NEXT)
    Paused --> Idle : stop(), cb(IDLE)
    Playing --> Idle : song complete, cb(IDLE)
    [*] --> Shutdown : delete(), cb(SHUTDOWN)
    Shutdown --> Idle : new(), cb(IDLE)
```

Note: Diagram shortens callbacks from AUDIO_PLAYER_EVENT_xxx to xxx, and functions from audio_player_xxx() to xxx(), for clarity.