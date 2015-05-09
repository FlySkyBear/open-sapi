

---

# Communication Specifications #

## Server Notes ##

The server expects data to arrive in UTF-8 format from the client.

The client must call a single readyServer command before issuing any further commands to the server. If the server is running and responding then a 204:Ready response is received by the client. When the client receives this it can continue to send commands.

The client currently checks to see if it can open the port to the server. If this fails it then begins to try and find the server executable and run the server. Once the server command has been executed it then tries to resend the serverReady command six times over a period of 60 seconds. This is mainly due to the fact that some machines are slow to start the server especially Linux as they are executing wine as well.

All "settings" can be send in a group to the server or seperatly

The speakMe command must be sent on its own as the last command to start synthesis on the server using the current settings

---

# Server Client Communication Protocol #
General Code Rule:
200 = OK
400 = Error
500 = Erros

Command   : readyServer <br>
Arguments : None <br>
Returns   : Status No:Desc - (204:Ready) <br>
COmment   : This command must be send on its own as the other commands will be ignored.<br>

Command   : killServer <br>
Arguments : None <br>
Returns   : Status No:Desc - (299:Shutdown OK) <br>

Command   : closeClient <br>
Arguments : None <br>
Returns   : Status No:Desc - (294:Close Client) <br>
Comment   : This command must be sent when the client has finished sending commands to the server.<br>

--Settings--<br>
Command   : getFormat <br>
Arguments : None <br>
Returns   : Status No:Desc:ID:Format - (298:Format List:1:SPSF_8kHz8BitMono) <br>

Command   : setFormat <br>
Arguments : Format ID <br>
Returns   : None <br>

Command   : outFile <br>
Arguments : Filename (/tmp/filename , c:\temp\filename) <br>
Returns   : None <br>
Comment   : This is the full filename including PATH. If this is missed off a file called sapi.wav is created in the PWD <br>

Command   : getVol <br>
Arguments : None <br>
Returns   : Status No:Desc:Volume - (295:Volume:100) <br>

Command   : setVol <br>
Arguments : Volume (0 - 100) <br>
Returns   : None <br>

Command   : setPitch <br>
Arguments : Pitch (-10 - +10) <br>
Returns   : None <br>

Command   : getEngine <br>
Arguments : None <br>
Returns   : Status No:Desc:ID:Name:Gender:Language:Vendor:Age - (297:Voice List:1:Microsoft Mary:Female:English_United_States,Microsoft,Adult) <br>

Command   : setEngine <br>
Arguments : ID <br>
Returns   : None <br>

Command   : getRate <br>
Arguments : None <br>
Returns   : Status No:Desc:Rate - (296:Rate:0)<br>

Command   : setRate <br>
Arguments : Rate (-10 - 10)<br>
Returns   : None <br>

Command   : speakMe <br>
Arguments : Text For Synth <br>
Returns   : Status : Desc (205:Synthesis OK) <br>
Comment   : This command should be sent on its own after all settings commands.<br>

Command   : speechFlag <br>
Arguments : Value (See extended notes at bottom) <br>
Returns   : None <br>
Comment   : This commands is optional and should not be used in normal operation.<br>

Command   : setDebug <br>
Arguments : None <br>
Returns   : None <br>
Comment   : This gives full output to stdout from the server for debugging <br>
<hr />
<h1>Table of Server Return Codes & Messages</h1>
<table><thead><th><b>CODE</b></th><th><b>Message</b></th><th><b>Description</b></th></thead><tbody>
<tr><td> 200 </td><td> OK </td><td> General OK (unimplemented)</td></tr>
<tr><td> 201 </td><td> Synth OK </td><td> Lets the client know that the synthesis is going ahead OK </td></tr>
<tr><td> 202 </td><td> Setting OK </td><td> Returned after any setting change on the server Rate Volume Speed Output file</td></tr>
<tr><td> 203 </td><td> Test OK </td><td> If the test complete this code is returned (unimplemented)</td></tr>
<tr><td> 204 </td><td> Server Ready </td><td> Signifies the server is ready for work</td></tr>
<tr><td> 293 </td><td> End of List </td><td> This follows any list of data returned by the server</td></tr>
<tr><td> 294 </td><td> Close Client </td><td> The server has finished its current job</td></tr>
<tr><td> 295 </td><td> Volume </td><td> Returns the current server volume as well </td></tr>
<tr><td> 296 </td><td> Rate </td><td> Returns the current server rate </td></tr>
<tr><td> 297 </td><td> Voice List </td><td> Returns with a list of voices and their details </td></tr>
<tr><td> 298 </td><td> Format List </td><td> Returns with a list of supported wav formats </td></tr>
<tr><td> 299 </td><td> Shutdown OK </td><td> Acknowledges the shutdown request from the client </td></tr>
<tr><td> 400 </td><td> Bad Request </td><td> Unimplemented</td></tr>
<tr><td> 500 </td><td> Server Internal Error </td><td> Unimplemented </td></tr>
<tr><td> 501 </td><td> Not Implemented </td><td> Unimplemented (how ironic)</td></tr>
<tr><td> 504 </td><td> Time Out </td><td> Tells the client the server timed out while sitting idle </td></tr>
<tr><td> 513 </td><td>Message Too Large </td><td> Unimplemented </td></tr>
<tr><td> 590 </td><td> COM Error </td><td> Give meaningful information about COM errors</td></tr>
<tr><td> 591 </td><td> Core Component Missing </td><td> Gives information about the components </td></tr>
<tr><td> 592 </td><td> Unexpected SAPI Error </td><td> Gives errors from SAPI </td></tr>
<tr><td> 593 </td><td> Unsupported Wav Format </td><td> Somehow you have tried to you an unsupported format for your system</td></tr>
<tr><td> 594 </td><td> No Speech Engines Match That Request </td><td> You have asked for a speech engine that does not exist on this system </td></tr>
<tr><td> 595 </td><td> Shutdown Failure </td><td> something in the shut-down process failed </td></tr>
<tr><td> 596 </td><td> Startup Failure  </td><td> Can't Start the server and the reason </td></tr>
<tr><td> 597 </td><td> Server Port Busy </td><td>  </td></tr>
<tr><td> 598 </td><td> MS Visual C++ DLL Load Failure</td><td>  </td></tr>
<tr><td> 599 </td><td> Unable to Initialise SAPI</td><td>  </td></tr></tbody></table>

<hr />
<h1>Extended Notes</h1>

<h2>Speech Flags</h2>
The client should not set the speech flag only in very special cases the server does not expect the speech flag to be set.<br>
See the SAPI documentation for further details. <br>
SVSFDefault = 0 <br>
SVSFlagsAsync = 1 <br>
SVSFPurgeBeforeSpeak = 2 <br>
SVSFIsFilename = 4 <br>
SVSFIsXML = 8 <br>
SVSFIsNotXML = 16 <br>
SVSFPersistXML = 32 <br>
SVSFNLPSpeakPunc = 64 <br>
<hr />
<h2>Wav format list</h2>
The server test each individual format on the OS it is running as not all formats are supported and returns a list of formats that it can use. This list is just for reference.<br>
0    SPSF_NoAssignedFormat <br>
1    SPSF_Text <br>
3    SPSF_NonStandardFormat <br>
4    SPSF_ExtendedAudioFormat  <br>
5    SPSF_8kHz8BitMono <br>
6    SPSF_8kHz8BitStereo <br>
7    SPSF_8kHz16BitMono <br>
8    SPSF_8kHz16BitStereo <br>
9    SPSF_11kHz8BitMono <br>
10   SPSF_11kHz8BitStereo <br>
11   SPSF_11kHz16BitMono <br>
12   SPSF_11kHz16BitStereo <br>
13   SPSF_12kHz8BitMono <br>
14   SPSF_12kHz8BitStereo <br>
16   SPSF_12kHz16BitMono <br>
17   SPSF_12kHz16BitStereo <br>
18   SPSF_16kHz8BitMono <br>
19   SPSF_16kHz8BitStereo <br>
20   SPSF_16kHz16BitMono <br>
21   SPSF_16kHz16BitStereo <br>
22   SPSF_22kHz8BitMono <br>
25   SPSF_22kHz8BitStereo <br>
26   SPSF_22kHz16BitMono <br>
27   SPSF_22kHz16BitStereo <br>
28   SPSF_24kHz8BitMono <br>
29   SPSF_24kHz8BitStereo<br>
30   SPSF_24kHz16BitMono <br>
31   SPSF_24kHz16BitStereo <br>
32   SPSF_32kHz8BitMono <br>
33   SPSF_32kHz8BitStereo <br>
35   SPSF_32kHz16BitMono <br>
36   SPSF_32kHz16BitStereo <br>
37   SPSF_44kHz8BitMono <br>
38   SPSF_44kHz8BitStereo <br>
39   SPSF_44kHz16BitMono <br>
40   SPSF_44kHz16BitStereo <br>
41   SPSF_48kHz8BitMono <br>
42   SPSF_48kHz8BitStereo <br>
43   SPSF_48kHz16BitMono <br>
44   SPSF_48kHz16BitStereo <br>
45   SPSF_TrueSpeech_8kHz1BitMono <br>
46   SPSF_CCITT_ALaw_8kHzMono <br>
47   SPSF_CCITT_ALaw_8kHzStereo <br>
48   SPSF_CCITT_ALaw_11kHzMono <br>
49   SPSF_CCITT_ALaw_11kHzStereo <br>
50   SPSF_CCITT_ALaw_22kHzMono <br>
51   SPSF_CCITT_ALaw_22kHzStereo <br>
52   SPSF_CCITT_ALaw_44kHzMono <br>
53   SPSF_CCITT_ALaw_44kHzStereo <br>
54   SPSF_CCITT_uLaw_8kHzMono <br>
55   SPSF_CCITT_uLaw_8kHzStereo <br>
56   SPSF_CCITT_uLaw_11kHzMono <br>
57   SPSF_CCITT_uLaw_11kHzStereo <br>
58   SPSF_CCITT_uLaw_22kHzMono <br>
59   SPSF_CCITT_uLaw_22kHzStereo <br>
60   SPSF_CCITT_uLaw_44kHzMono <br>
61   SPSF_CCITT_uLaw_44kHzStereo <br>
62   SPSF_ADPCM_8kHzMono <br>
63   SPSF_ADPCM_8kHzStereo <br>
64   SPSF_ADPCM_11kHzMono <br>
65   SPSF_ADPCM_11kHzStereo <br>
66   SPSF_ADPCM_22kHzMono <br>
67   SPSF_ADPCM_22kHzStereo <br>
68   SPSF_ADPCM_44kHzMono <br>
69   SPSF_ADPCM_44kHzStereo <br>
70   SPSF_GSM610_8kHzMono <br>
71   SPSF_GSM610_11kHzMono <br>
72   SPSF_GSM610_22kHzMono <br>
73   SPSF_GSM610_44kHzMono <br>