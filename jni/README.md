# Encore-Fork Daemon

This is the core of Encore-Fork daemon that handles automatic profiles, configs and addons.

Before you dig into this code thinking this is some kind of scheduling module like Uperf, it's not. Encore-Fork is a profile-style performance module; it simply applies performance tweaks as profiles and <ins>does not dynamically control scheduling and frequencies</ins>.

Encore Tweaks works by using information such as:
- Currently running app
- Screen state, whenever it's awake or not and...
- Battery saver state (yes the ones on your quick settings)

## Workflow diagram

![Workflow diagram of Encore Tweaks daemon](./diagram.svg)
