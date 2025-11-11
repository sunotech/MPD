# MPD

Everything related to Music Player Daemon

I have been using MPD on various machines and OSs over the years. This space serves as a personal note on some best practise on different configuration. While I share the configuration and tweakings on my set up here, I do hope to recieve comments and recommdations, this will improve setup for everyone.

# Use-case

NAS + laptop

MPD is a server client model already, the setup is primarily put a "heavey" single server that host all music files and connects to audio output. However, this set up is less flexible for people who don't have a fixed listening area. The proposed setup below allows one single MPD server to store all music files, usually that MPD server runs on a NAS or similar system, then on each listening enviroment, we install both MPD server and client on a computer, where it connects to DAC/Amplifier/Speakers. 

![](assets/MPD_Hardware_Flowchart.drawio.svg)
