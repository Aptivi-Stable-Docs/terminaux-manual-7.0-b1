---
description: In case you want to set things up
icon: gear
---

# Reader Settings

The reader currently has a global settings instance session-wide. However, it can get overridden if you make a new instance of `TermReaderSettings` with some available properties mentioned below set. They get read each time you call this function or you activate a keybinding that uses one of these settings.

Here are the available settings that you can set:

* `PasswordMaskChar`
  * Sets the password masking character.
* `HistoryEnabled`
  * Whether the history is enabled or not.
* `HistoryName`
  * Select what history to use
* `LeftMargin`
  * Sets the left margin of the input.
* `RightMargin`
  * Sets the right margin of the input.
* `InputForegroundColor`
  * The foreground color for the input text, as well as the input prompt.
* `InputBackgroundColor`
  * The background color for the input text, as well as the input prompt.
* `Suggestions`
  * Sets a function that you could use to return an array of strings containing auto completion data.
* `SuggestionsDelimiters`
  * Delimiters to split the current input within a function that returns a list of suggestions.
* `TreatCtrlCAsInput`
  * Whether to treat `Ctrl` + `C` as input or not. If enabled, TermRead will process this keybinding as aborting the current input.
* `PlaceholderText`
  * This is the text that the terminal reader shows when there is no input text. This is used to give users hints on what they should write to the prompt.
* `PrintDefaultValue`
  * Whether to print the default value or not. Disables `WriteDefaultValue`.
* `WriteDefaultValue`
  * Whether to make the default value part of the input or not. Disables `PrintDefaultValue`.
* `InitialPosition`
  * Where to set the initial cursor position for the reader (only works when there is a default value and `WriteDefaultValue` is on)
* `DefaultValueFormat`
  * The default value format to print if `PrintDefaultValue` is enabled and there is a prompt.
* `KeyboardCues`
  * Whether to play keyboard cues for each keypress
* `BassBoomLibraryPath`
  * In case of addons or other custom path for MPG123, specifies a root path to BassBoom's libraries. See [here](https://app.gitbook.com/o/fj052nYlsxW9IdL3bsZj/s/izAJoIbtQw1BdIlE4DBz/) for more info.
* `PlayWriteCue`
  * Specifies whether to play a write cue (that is, plays a sound for each keypress). You can specify your custom write cue using the `CueWrite` property, but be sure to pass it a stream that contains an MP3 file content that [BassBoom](https://app.gitbook.com/s/izAJoIbtQw1BdIlE4DBz/power-users/using-basolia) can play.
* `PlayRuboutCue`
  * Specifies whether to play a rubout cue (that is, plays a sound for every backspace press). You can specify your custom write cue using the `CueRubout` property, but be sure to pass it a stream that contains an MP3 file content that [BassBoom](https://app.gitbook.com/s/izAJoIbtQw1BdIlE4DBz/power-users/using-basolia) can play.
* `PlayEnterCue`
  * Specifies whether to play an enter cue (that is, plays a sound for each "submit" key, such as Enter). You can specify your custom write cue using the `CueEnter` property, but be sure to pass it a stream that contains an MP3 file content that [BassBoom](https://app.gitbook.com/s/izAJoIbtQw1BdIlE4DBz/power-users/using-basolia) can play.
* `CueVolume`
  * Specifies the cue volume in fractional number between `0.0` and `1.0` (or `3.0` with volume boost)
* `CueVolumeBoost`
  * Allows the cue volume to go above `1.0` to the maximum of `3.0`.
* `Bell`
  * Specifies how to launch a console bell (audible for beep sounds, visual for flashing console, or none for nothing)

{% hint style="info" %}
You can copy the above settings in one line using the overload of the `TermReaderSettings` constructor that allows you to specify another `TermReaderSettings` instance to copy the settings from that instance to the new one. This is useful if you want to use the global settings without affecting future reads. This is a simple example of how to copy the global settings and to set the password mask without affecting the global password mask:

<pre class="language-csharp"><code class="lang-csharp">// Doesn't affect future reads
<strong>var settings = new TermReaderSettings(TermReader.GlobalReaderSettings)
</strong><strong>{
</strong><strong>    PasswordMaskChar = '#'
</strong><strong>};
</strong>
// Affects future reads
TermReader.GlobalReaderSettings.PasswordMaskChar = '#';
</code></pre>
{% endhint %}
