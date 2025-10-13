# MPD

Everything related to Music Player Daemon

I have been using MPD on various machines and OSs over the years. This space serves as a personal note on some best practise on different configuration. While I share the configuration and tweakings on my set up here, I do hope to recieve comments and recommdations, this will improve setup for everyone.

# Use-case

NAS + laptop

MPD is a server client model already, the setup is primarily put a "heavey" server that host all music files and connects to audio output. However, this set up is less flexible for people who don't have a fixed listening area. The set up I have right now is to set up multiple MPDs where the client version of MPD get a golden source of music library from the "master" MPD server.

![](assets/MPD_Hardware_Flowchart.drawio.svg)
