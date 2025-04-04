# Hexo Player <img src="ic_launcher_new_round.webp" width="45" height="45"/>
- This is a unofficial fork of Android VLC Player
- Supported for both andorid mobile and TV
- It has the **"Referer"** and **"User-Agent"** header support through intent management
- If you want to use this player as thrid party player for your apps, please refer the below Intent sample code that you will need to use from your app.

## Sample code

### Play a Video in HexoPlayer 🎬  (Kotlin code)

<!-- Copy Button -->
<button onclick="copyCode()" style="padding: 5px 10px; font-size: 14px; border: none; background: #28a745; color: white; border-radius: 5px; cursor: pointer;"></button>

```kotlin
val getActivityResult =  
        registerForActivityResult(  
                ActivityResultContracts.StartActivityForResult()) {  
                if(it.resultCode == Activity.RESULT_OK){  
                  //DO the required action if the Activity executed successfully  
                }  
val RequestCode = 42  
val uri = Uri.parse("file:///storage/emulated/0/Movies/KUNG FURY Official Movie.mp4")  
val hexoIntent = Intent(Intent.ACTION_VIEW).apply {  
    setPackage("com.optimumdev.hexoplayer")  
    setDataAndTypeAndNormalize(uri, "video/*")  
    putExtra("title", "Kung Fury")  
    putExtra("from_start", false)  
    putExtra("position", 90000L)  
    putExtra("subtitles_location", "/sdcard/Movies/Fifty-Fifty.srt")  
}  
getActivityResult.launch(hexoIntent)  
```

### Extras
| Value | Type | Description
| --- | --- | --- |
| "extra_position" | long | Last position in media when player exited
| "extra_duration" | long | Total duration of the media
| "referrer_header" | string | To set any specific **Referer** header value for the given streaming link
| "user_agent" | string |To set any specific **User-Agent** header value for the given streamin link
| "force_incognito" | boolean | To avoid stremaing link to be listed in Network stream histoy

### Result codes

| Result | Value (int) | Description |
| --- | --- | --- |
| RESULT_OK | -1 	| Video finished or user ended playback
| RESULT_CANCELED | 0 | No compatible cpu, incorrect Hexo Player abi variant installed
| RESULT_CONNECTION_FAILED | 2 | Connection failed to audio service
| RESULT_PLAYBACK_ERROR | 3 | Hexo Player is not able to play this file, it could be incorrect path/uri, not supported codec or broken file
| RESULT_HARDWARE_ACCELERATION_ERROR | 4 | Error with hardware acceleration, user refused to switch to software decoding
| RESULT_VIDEO_TRACK_LOST | 5 | Hexo Player continues playback, but for audio track only. (Audio file detected or user chose to)
