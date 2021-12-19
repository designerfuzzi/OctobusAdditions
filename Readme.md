*Conceptional* Control Layout for **Elektron Octatrack** to use with **TouchOSC**

how to:

1) install TouchOSC mk2
2) copy the layout to you favourite folder
3) open it in TouchOSC mk2
4) setup some OSC Connection for sender9000/receiver7000.. UDP, if you like
5) setup some Midi Connection to your external midi interface device
5.1) or host some virtual Midi Port from within TouchOSC..
6) hit play, enjoy.

**consider contributing when you improve it, please.**

OSC addresses are not complete yet. 
Just T1 parameters carry a complete address scheme as starting point for scripting.
T1 to T8 correspond to Midi Channel 1 to 8, no Autochannel used. 
So you can control directly if your Octatrack uses 1..8 for its audio controls.
Selecting T1, T2, Tx, ... will trigger a CC request via midi
and your Octatrack will answer with parameters for the selected midi channel/ track.
Means you need to receive Midi from the Octatrack as well to make it work dynamic.
If you cant receive from your Octatrack it will still work, but the params dont show their state.
Switching Patterns and Banks not included yet and so also the parameter request for this case is not included yet.

Cheers.
