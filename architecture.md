# Technical Architecture

## Technical Requirements

* Runnable on mobile devices, ideally cross-platform (iOS and Android)
* Able to generate musical tones and play musical samples with accurate pitch, timing, and sound quality
* Access to a variety of sensors and inputs with acceptable latency
    * Multi-touch (ideally with pressure sensitivity for expressiveness) 
    * Accelerometer
    * Gyroscope
    * Microphone
 
## Options to Consider
### 1. React Native / Expo

| Native / Web? | Primary Language | Platforms | Docs |
|---------------|------------------|-----------|------|
|Native|Typescript|iOS, Android, Web|https://expo.dev/|

Pros:

* Cross-platform, write shared code in Typescript that is compiled for both iOS and Android
* Access to device sensors ([`expo-sensors`](https://docs.expo.dev/versions/v53.0.0/sdk/sensors/))
* Access to Web Audio API ([`react-native-audio-api`](https://docs.swmansion.com/react-native-audio-api/docs/)

Cons:

* Some more advanced functionality may require writing or integrating Swift (iOS) or Kotlin (Android) code for native features
* Even with Web Audio API, would need to implement some music-related capabilities such as transforming rhythmic measures and note durations into milliseconds
* [Noise generation](https://docs.swmansion.com/react-native-audio-api/docs/guides/noise-generation) possible (could be used for synthesis) but support seems pretty bare-bones


### 2. iOS-only AudioKit app
| Native / Web? | Primary Language | Platforms | Docs |
|---------------|------------------|-----------|------|
|Native|Swift|iOS, macOS|https://www.audiokit.io/AudioKit/documentation/audiokit|

Pros:
*  Good support for music-related tasks like sequencing, and synthesis
*  Available UI support for musicy things like knobs, sliders, and pads
*  Will have solid access to full range of available sensors

Cons:
* No Android support 😢

### 3. Web App
| Native / Web? | Primary Language | Platforms | Docs |
|---------------|------------------|-----------|------|
|Web|Javascript,Typescript|All|See below|

Pros:
* Cross-platform compatibility
* Solid library support
    * [Tonejs](https://github.com/Tonejs/Tone.js): Music sequencing, synthesis, sampling, and effects
    * [Tonal](https://github.com/tonaljs/tonal): Music theory (chords, scales, etc.)
    * [p5.js](https://p5js.org/): Interactive visuals
* Possible to access [device motion](https://developer.mozilla.org/en-US/docs/Web/API/DeviceMotionEvent)
    * [p5.js example](https://p5js.org/examples/animation-and-variables-mobile-device-movement/) 
 
Cons:
* More limited sensor availability
* Possible latency issues compared to mobile due to browser environment

### 4. MobMuPlat
| Native / Web? | Primary Language | Platforms | Docs |
|---------------|------------------|-----------|------|
|Native (?)|Visual|iOS, Android|https://danieliglesia.com/mobmuplat/|

This option's a little out there, but it's basically a way to quickly iterate on different GUI options (created using a visual editor) 
that are then paired with a [PureData](https://puredata.info/) audio engine to generate sounds (PureData is a [visusal programming language for computer music](https://puredata.info/)). 
This even includes motion detection support, but requires running these two created files through a free app on iOS or Android, so I'm not sure if it would count as our project.
