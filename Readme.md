*Conceptional* Control Layout for **Elektron Octatrack** to use with **TouchOSC**

how to:

1) install TouchOSC mk2
2) copy the layout `*.tosc` to you favourite folder
3) open it in TouchOSC mk2
4) ~~setup some OSC Connection for sender9000/receiver7000.. UDP, if you like~~ (not needed when you do midi with TouchOSC)
5) setup some MIDI Connection to your external midi interface in TouchOSC. Can be Network Session 1 or virtual MIDI or a physical device.
   <br>**Reminder:** MIDI Tracks that make use of the same midi channel as your Audio Control Setup for some particular track in the Octatrack will trigger the Octatrack to **not** send its own values (CC48 Crossfader and all Data Dump requested by CC61) to this channel. 
   <br>**Example:** When you have some sequenced MIDI track sending notes to CH1 **and** Audio Track 1 is also acting on behalf of CH1 (i.e. from some external midi controller) then CC48 will try to send the next available non-counterpart'ed Channel, in this case CH2 and the Data Dump from Audio Track 1 will not be send out on request. If there is additional some MIDI Track given to send also on CH2, then the Crossfader from the next Audio Track will be send which could be CH3 as well as the Data Dump will be ignored of this Audio CH2. 
7) hit play, enjoy.

How it works?<br>
**works bidirectional.** Received Midi signals in TouchOSC will show up their values in the running sheet.<br>
Which means you can request the Patterns values with CC61 and get feedback starting with CC16 up to CC56.<br>
Because TouchOSC will map the incomming data to the controls with the same midi values the dumped data appears as sheet update showing the momentary values.<br>
leading to the idea that you can request the values after a pattern or bank switch.

The layout allows SCENE switching for SCENE A from 1..8 and for SCENE B from 9..16, <br>
they are send as momentary midi signal, means you can slide thru them and hear the difference.
In this layout SCENE B cant select SCENE 1 and SCENE A cant select SCENE 9 and so on.. <br>
this limits your possiblities but keeps the layout somewhat useable. You could change this via the editor.

~~OSC addresses are not complete yet~~. complete!<br>
The layout sends also each control value as OSC value in a scheme of the following structure.
```
/t1
```
As this works bidirectional this also means when TouchOSC receives `/t2` it will switch to page 2.

```
/t1/mute f 0.0
/t1/vol f 0.0
/t1/cue f 0.0
/t1/cued f 0.0

/t1/src/ptch f 0.0
/t1/src/strt f 0.0
/t1/src/len f 0.0
/t1/src/rate f 0.0
/t1/src/rtrg f 0.0
/t1/src/rtim f 0.0

/t1/amp/atk f 0.0
/t1/amp/hold f 0.0
/t1/amp/rel f 0.0
/t1/amp/vol f 0.0
/t1/amp/bal f 0.0
/t1/xvol f 0.0

/t1/lfo/spd1 f 0.0
/t1/lfo/spd2 f 0.0
/t1/lfo/spd3 f 0.0
/t1/lfo/dep1 f 0.0
/t1/lfo/dep2 f 0.0
/t1/lfo/dep3 f 0.0

/t1/fx1/param1 f 0.0
/t1/fx1/param2 f 0.0
/t1/fx1/param3 f 0.0
/t1/fx1/param4 f 0.0
/t1/fx1/param5 f 0.0
/t1/fx1/param6 f 0.0

/t1/fx2/param1 f 0.0
/t1/fx2/param2 f 0.0
/t1/fx2/param3 f 0.0
/t1/fx2/param4 f 0.0
/t1/fx2/param5 f 0.0
/t1/fx2/param6 f 0.0
```
where `t1` could be `t2`, `t3`, `t4`, `t5`, `t6`, `t7`, `t8` and correspond to the Audio Track T1 to T8.
Above value expresses selected Track is 1. 


in general without track assignment the following
```
/crossfader f 0.0
/scene_a i 0
/scene_b i 8
```

for MIDI params
```
/midi/mute/t1 f 0.0
```
midi track parameter start with `/midi` following their function name and assigned track


`i` + `f` represent the used *tag* indicting the type of send OSC data, <br>
int between [0..127] and float between [0.0 .. 1.0] <br>
or no tag and according also no data for selected pages 
example:`/t5` == page of Track 5

**T1** to **T8** correspond to Midi Channels **1 to 8**<br>
So you can control directly if your Octatrack uses 1..8 for its audio controls.<br>
~~*no Autochannel used!*.~~ AutoChannel (CH9) used for sending Bank + Pattern switch via MIDIProgramChange message.

Selecting ~~T1, T2, Tx~~, **REQUEST** ... will trigger a request data dump via midi CC61 of all parameters<br>
As this cant be limited to just one channel, the data is quite large (40signals * 8 Channels = 320 commands) you could potentially hear a slow down when your session is running, so use it wisely. One time data request doesnt hurt.

If you cant receive from your Octatrack it will still work, but the params dont show their real state in the sheet if you switched a pattern in example.<br>

Switching Patterns and Banks is not included yet.

Reminder: parameters of Midi tracks do not answer on request CC61.

<img width="1112" alt="TouchOSC octatrack simple midi layout" src="https://user-images.githubusercontent.com/1221499/147226249-26405c56-8e27-4fda-8be6-fe18f6a93d5b.png">

**consider contributing your changed layout when you improve it.**
