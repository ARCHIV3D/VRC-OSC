<div align="center">
  <a href="https://discord.shaybox.com">
    <img alt="Discord" src="https://img.shields.io/discord/824865729445888041?color=404eed&label=Discord&logo=Discord&logoColor=FFFFFF">
  </a>
  <a href="https://github.com/shaybox/vrc-osc/releases/latest">
    <img alt="Downloads" src="https://img.shields.io/github/downloads/shaybox/vrc-osc/total?color=3fb950&label=Downloads&logo=github&logoColor=FFFFFF">
  </a>
</div>

# VRC-OSC

Dynamically loaded cross-platform VRChat OSC plugins written in Rust.

## Plugins:

- [`plugin-clock`](/plugin-clock): Sends the time via avatar parameters for watch prefabs.
- [`plugin-debug`](/plugin-debug): Log all received OSC packets to stdout for debugging.
- [`plugin-lastfm`](/plugin-lastfm): Displays the currently playing song via chatbox.
- [`plugin-spotify`](/plugin-spotify): Displays the currently playing song via chatbox, and controls playback via avatar parameters.
- [`plugin-steamvr`](/plugin-steamvr): Registers VRC-OSC as a SteamVR addon for auto-start/stop.

## Planned:

- [`plugin-controls`](/plugin-controls): Controls media playback via avatar parameters.

## Configuration Documentation:

This is the default configuration file generated at first-run with additional comments for documentation,  
You may copy this as a default configuration, but comments will be wiped on first write.

```toml
# Every plugin has it's own configuration section.

# The built-in plugin loader handles starting every plugin and relaying OSC packets.
# If you're running this on the same computer as VRChat, you won't need to change this.
# If you're using a different PC or Quest you can change the addresses below.
# To receive incoming OSC packets you will need to set the launch option below.
# https://docs.vrchat.com/docs/osc-overview#vrchat-ports
[osc]
bind_addr = "0.0.0.0:9001"
send_addr = "127.0.0.1:9000"

# The Clock plugin sends the time via avatar parameters for watch prefabs.
[clock]
enable = false
# Enable 24 hour mode. (12 = false | 24 = true)
mode = false
# Smooth results using milliseconds, smoother animations.
smooth = false
# How often to send OSC packets. Milliseconds
# Set this between 10-100 when using smoothing.
polling = 1000

# The Debug plugin logs all received OSC packets to stdout for debugging.
# I wouldn't recommend enabling this unless you know what you're doing.
[debug]
enable = false

# The LastFM plugin displays the currently playing song via in-game chatbox.
# I recommend using this instead of Spotify Chatbox as it doesn't require a developer application.
# Just connect Spotify to LastFM https://www.last.fm/about/trackmymusic
[lastfm]
# You shouldn't need to change this, you can use mine, or you can use your own.
api_key = "54c4fd51def9bc426c3950abb855bf30"
# Set this to your LastFM username.
username = "ShayBox"
# Chatbox format string, use {song} and {artists} as variables.
format = "📻 {song} - {artists}"
# Displays the currently playing song via in-game chatbox.
enable = true
# When enabled, only sends the currently playing song to in-game chatbox once per song.
send_once = false
# Seconds between polling LastFM
# Default VRChat Chatbox Timeout is 30 seconds
polling = 10

# You must create a Spotify Developer Application
# Follow the instructions on GitHub
# https://github.com/ShayBox/VRC-OSC/tree/master/plugin-spotify
[spotify]
client_id = ""
client_secret = ""
# The Spotify callback redirect URI must match on the Spotify Developer Application.
redirect_uri = "http://127.0.0.1:2345"
# Chatbox format string, use {song} and {artists} as variables.
format = "📻 {song} - {artists}"
# Spotify Refresh Token - Saved to reduce in-browser oauth approval
refresh_token = ""
# Displays the currently playing song via in-game chatbox.
enable_chatbox = false
# Controls media playback via avatar parameters.
enable_control = false
# Use Spotify PKCE authentication
# PKCE is the appropriate authentication method for a desktop program
# But it asks for in-browser oauth approval for already approved apps
# Non-PKCE requires a Client Secret but doesn't ask for approval
pkce = false
# When enabled, only sends the currently playing song to in-game chatbox once per song.
send_once = false
# Seconds between polling Spotify
# Default VRChat Chatbox Timeout is 30 seconds
polling = 10

[steamvr]
# Enabling this will register VRC-OSC as a SteamVR addon for auto-start.
enable = false
# To un-register set 'register' to false and 'enable' to true.
register = true
```
