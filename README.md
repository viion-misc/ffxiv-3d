# ffxiv-3d

Concept of a web based 3D Model Viewer for FFXIV

## How to use

You need https://textools.dualwield.net/

Extract some models, and then modify the code to the correct paths. Currently set to show Fenrir mount, armor works fine. As FFXIV TexTools is open source I took it and modified it to automatically go through all items/mounts/companions and extract each one, it was very slow taking hours and hours to finish. Impractical really!

Doubt there will be any production on this, so feel free to use as you want! No questions asked. All the logic is in `index.html` as I was lazy :D maybe one day I will clean this up.

Clone it and run it on a web server of sorts, i just used https://www.npmjs.com/package/live-server