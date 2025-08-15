# esp32_a1s_es8388-HA-Voice-Assistant-Media-Player-Working
I'm very new to all this, but this is my attempt at having a working Voice Assistant satellite with OpenWakeWord as well as media player ability.

The specific board is this one: https://www.amazon.com/dp/B0B63KZ6C1?ref=ppx_yo2ov_dt_b_fed_asin_title

There are some slight errors, I am hoping someone who knows more about this than I do can help fix that.

Apart from the errors in the logs, it works. Wake words work repeatedly, which I was struggling with before and getting the issue where it only works once and then does not work anymore. And media player works, the only catch is using the media player turns off the wake word, so you have to pause the media player to use the wake word again.

Would love for someone smarter than me to take a look and see what could improve. Here are my logs with the errors and warnings:

The first error I saw happens after a voice command is excecuted and the pipeline finishes and restarts:

```text
[10:28:59][D][voice_assistant:484]: Desired state set to RESPONSE_FINISHED 
[10:29:00][D][voice_assistant:375]: Speaker has finished outputting all audio 
[10:29:00][D][voice_assistant:477]: State changed from RESPONSE_FINISHED to IDLE 
[10:29:00][D][voice_assistant:484]: Desired state set to IDLE 
[10:29:00][D][voice_assistant:477]: State changed from IDLE to START_MICROPHONE 
[10:29:00][D][voice_assistant:484]: Desired state set to START_PIPELINE 
[10:29:00][D][resampler_speaker:090]: Stopping resampler task 
[10:29:00][D][resampler_speaker:095]: Stopped resampler task 
[10:29:00][D][voice_assistant:207]: Starting Microphone 
[10:29:00][D][voice_assistant:477]: State changed from START_MICROPHONE to STARTING_MICROPHONE 
[10:29:00][D][speaker_mixer:329]: Stopping speaker mixer 
[10:29:00][E][i2s_audio.microphone:517]: Driver failed to start; retrying in 1 second 
[10:29:00][E][component:286]: i2s_audio.microphone set Error flag: unspecified 
[10:29:00][D][i2s_audio.speaker:148]: Stopping 
[10:29:00][D][i2s_audio.speaker:154]: Stopped 
[10:29:01][E][component:313]: i2s_audio.microphone cleared Error flag 
[10:29:01][D][voice_assistant:477]: State changed from STARTING_MICROPHONE to START_PIPELINE 
[10:29:01][D][voice_assistant:228]: Requesting start 
[10:29:01][D][voice_assistant:477]: State changed from START_PIPELINE to STARTING_PIPELINE 
[10:29:01][D][voice_assistant:499]: Client started, streaming microphone 
[10:29:01][D][voice_assistant:477]: State changed from STARTING_PIPELINE to STREAMING_MICROPHONE 
[10:29:01][D][voice_assistant:484]: Desired state set to STREAMING_MICROPHONE 
[10:29:01][D][voice_assistant:623]: Event Type: 1 
[10:29:01][D][voice_assistant:626]: Assist Pipeline running 
[10:29:01][D][voice_assistant:623]: Event Type: 9
```

The next error happens when I start the media player, specifically I am using radio station in Music Assistant. This warning doesn't prevent media from playing, seems ignorable, but if anyone has a solution, that would be nice:

```
[11:28:42][D][main:727]: Media playing → suspending wake-word
[11:28:42][D][voice_assistant:605]: Signaling stop
[11:28:42][D][voice_assistant:477]: State changed from STREAMING_MICROPHONE to STOP_MICROPHONE
[11:28:42][D][voice_assistant:484]: Desired state set to IDLE
[11:28:42][D][speaker_media_player:406]: State changed to PLAYING
[11:28:42][D][voice_assistant:477]: State changed from STOP_MICROPHONE to STOPPING_MICROPHONE
[11:28:42][D][voice_assistant:477]: State changed from STOPPING_MICROPHONE to IDLE
[11:28:42][D][voice_assistant:623]: Event Type: 2
[11:28:42][D][voice_assistant:763]: Assist Pipeline ended
[11:28:42][D][light:052]: 'A1S Status LED' Setting:
[11:28:43][D][speaker_media_player.pipeline:114]: Reading FLAC file type
[11:28:48][D][speaker_media_player.pipeline:124]: Decoded audio has 2 channels, 48000 Hz sample rate, and 16 bits per sample
[11:28:48][D][ring_buffer:034]: Created ring buffer with size 19200
[11:28:48][D][speaker_mixer:316]: Starting speaker mixer
[11:28:48][D][speaker_mixer:324]: Started speaker mixer
[11:28:48][W][component:407]: mixer.speaker took a long time for an operation (76 ms)
[11:28:48][W][component:408]: Components should block for at most 30 ms
[11:28:48][W][component:407]: mixer.speaker took a long time for an operation (53 ms)
[11:28:48][W][component:408]: Components should block for at most 30 ms
[11:28:48][D][i2s_audio.speaker:136]: Starting
[11:28:48][D][i2s_audio.speaker:141]: Started
```
