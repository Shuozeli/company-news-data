---
schema_version: "1.0.0"
document_id: "cf7b2336f4504debe1730b484f055dd8765072edf3d1509d1d49a61954c69f62"
company_key: "sonos-inc-common-stock"
company: "Sonos Inc. Common Stock"
source_id: "sonos-inc-common-stock-news-import-358168792368"
canonical_url: "https://en.community.sonos.com/product-updates/let-s-take-it-to-go-grouping-away-from-wifi-6933529"
published_at: "2026-03-31T00:00:00+00:00"
first_seen_at: "2026-07-24T01:42:45.861887+00:00"
fetched_at: "2026-07-27T10:56:07.023305+00:00"
content_hash: "sha256:0de9020c1297ff94d191bd4c0df1eb03ab9c6f3d333dce8ea3a9dea3c0db07bc"
---

# Let’s Take It To Go (Grouping away from WiFi)

Have you ever wanted to synchronize your portable Sonos speakers while you're away from home and out of WiFi range? Guess what…


**You can now group up to four Move 2 and Sonos Play speakers while you're out on the go, without a wireless network nearby to connect to!**


🔊🔊🔊🔊


Starting with


[system version 94.1-75011](https://support.sonos.com/article/release-notes-sonos-app-updates?utm_source=reddit-care&utm_medium=release-notes) and later, you can now group Move 2 and the new Sonos Play while you're at the beach, camping in the woods, or catching a ride on a spaceship to


*The Dark Side of the Moon*


. Spaceship not included. 🚀


# How to get the party started


**Before you leave home:**


First things first: Grouping on the go does not work "out of the box".


**All of the Sonos products need to be added to the same Sonos system before you’re out of WiFi range**


.


To confirm this, check the Sonos app before you leave. If your products are all powered on and connected to your network, they should all be showing in the app, without needing to use the "Switch System" feature in Settings.


- Note: technically speaking, they must be part of the same "household ID" (HHID)


**When you're on the go:**


1. Once you're out of WiFi range, connect your source device (phone, tablet, laptop, etc.) to your first speaker via Bluetooth.


[Here's](https://support.sonos.com/article/use-bluetooth-on-sonos?utm_source=reddit-care&utm_medium=use-bluetooth-on-sonos) a refresher on how to do that. After connecting,


**start playing audio**


on the source device so that you can hear it from the first speaker.


*If you don’t start playing audio first, step 2 might not work correctly.*


- this speaker is called the


**"group coordinator"**


2. **On your second speaker, tap-and-hold the Play/Pause button until you hear it make the first and second chime**


, about 1-2 seconds. This is the same


[‘press-and-hold to group’](https://support.sonos.com/article/group-and-ungroup-rooms?utm_source=reddit-care&utm_medium=group-and-ungroup-rooms) action that's available while you're at home with the rest of your system, allowing you to easily move a speaker between groups without needing to open the app. The LED will blink briefly during this process. Audio should start playing within 5-10 seconds.


- this speaker is called a


**"group member"**


3. Repeat step 2 on up to two additional Move 2 or Play speakers, for a total of 4 speakers in the group (1 group coordinator and 3 group members).


4. Enjoy the music!


Pretty simple, and


**you don't need to use the Sonos app during this process**


. In fact, since the Sonos app doesn't play music directly, you won't be able to use it for controlling the speakers in this configuration. I checked the app to confirm, and it gave a screen explaining steps 1-4 above much more succinctly than I did:


*“Start content on one speaker, then press and hold the play/pause button on another to play them together.”*


The app forgot step 4, though.


*That’s my favorite part.*


**When you get back home**


:


If the speakers weren't powered off, they’ll still be grouped when you get home. They will show as being


[“Away” in the Sonos app](https://support.sonos.com/article/portable-speakers-showing-as-away-after-grouping-using-bluetooth?utm_source=reddit-care&utm_medium=portable-speakers-showing-away) . In that case, simply tap and hold the Play/Pause button on the group coordinator (which should have a blue LED, since it is directly connected to the Bluetooth source). That will ungroup all of the players at once, which will then allow them to search for your home network and reconnect automatically.


Alternatively, you can reboot the speakers to force them to reconnect to your home WiFi. So if they were powered off when you left the beach or the camp site (or the Moon), just power them back on when you get home. Nice and easy.


# Controlling the group


Basic playback controls work the way you might intuitively expect.


Play, pause, skip forward, and skip backward can each be done using physical controls on


**each**


speaker in the group, when the service supports it.


For example, you still can’t skip songs on terrestrial radio stations from the TuneIn or iHeartRadio apps. But you


*can*


skip forward (press > or double tap the Play/Pause button) or skip backward (press < or triple tap the Play/Pause button) while playing content from apps like Spotify or Apple Music.


If you control the volume on an individual speaker, it changes the volume just for that speaker.


**If you control the volume from the Bluetooth source device (your phone or what have you), it will change the volume for the whole group.**


That’s the only one that caught my attention the first time I did it, since I initially expected it to only change the volume for the group coordinator. But then it made sense from that point forward. The source device is the One Speaker To Rule Them All.


# Range limits


Officially speaking: The maximum supported distance is about 50 feet (~15 meters) from the group coordinator to the group members. That's pretty far!


There are caveats, of course. The maximum distance can be reduced significantly by sources of wireless interference in the environment. Try to shoot for line-of-sight distances, where possible.


We recommend starting the grouping process while the speakers are within about 10 feet (~3 meters) of each other, and making sure they group successfully before moving them further. And the controller (Bluetooth source) should stay in close proximity to the group coordinator, within about 25 feet (~8 meters) or less.


Also, this is not a mesh network (like SonosNet of yesteryear); all group members must be in range of the group coordinator. For my fellow enthusiasts: think more like a star (hub and spoke) network topology.


Unofficially speaking: one of the things that really blew my mind with this feature is how far I was able to separate each speaker from the group coordinator. I tested myself, and I was probably closer to 60 feet (18 meters) before I started hearing any noticeable audio interruptions.


# Other tidbits


Fun facts ⬇️


- Follow the data:


- *content*


(audio) is shared from the


**source device**


to the group coordinator via Bluetooth Classic


- *grouping*


(synchronization) is done via an


**ad-hoc wireless connection**


between the group coordinator and the group members


- other products besides Sonos Play and Move 2 are not supported


- Roam’s hardware architecture requires Bluetooth and WiFi to share the same radio resources. Because grouping while away from home relies on coordination between those two wireless connections, enabling it on Roam could impact performance and reliability.


- some features from home that aren’t supported on the go:


- on-device voice services (Sonos Voice Control and Alexa) are unavailable in this setup


- stereo pairs are not supported


- USB-C line-in is not supported


- with wireless networking, there is such a thing as "too close" - move your source device at least 6"/15 cm away from the group coordinator to prevent communication problems


- stereo pairs of Move 2 or Sonos Play will automatically separate when you leave your network, and automatically re-pair once they’re back in range


- groups are not persistent when leaving or reconnecting to a network; if you group your Move 2 and Play before leaving, you will still need to regroup them when you’re away from WiFi, and vice versa


One last thing that I tested for fun: you can, if so desired, have


**multiple group coordinators with their own sets of group members**


. As long as they’re part of the same Sonos household ID, they’re pretty flexible. I connected my phone to a Move 2, and a laptop to another Move 2. Then I grouped and ungrouped a pair of Plays with each Move, just for kicks.


Why would anyone do this? I’m not quite sure. Maybe to listen to music on one group and play a gaming system on the other group for the true glamping or desert party (🔥👨) experience? You’ve got me. But it’s there if you want it. Share your dream setups in the comments if you plan on pushing the limits in ways I’ve yet to imagine.


# Wrap-Up


One of the best things about Sonos products is that we are committed to bringing awesome new features, long after a product was purchased, via free software updates. The system gets better over time. And it’s the systemness that makes the whole better than the sum of the parts.


To me, the ability to group your speakers while away from your WiFi network is just the latest example of this commitment. It wasn’t available when Move 2 was released in September 2023, but it’s available now.


Let us know what you think in the comments!
