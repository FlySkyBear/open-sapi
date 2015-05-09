# Checking & changing your speech engine #

Once you have open-sapi installed the first thing your going to want to do is change your speech engine so here is how.

Please note due to the incomparability of UTF-8 and MS Unicode special characters in some languages are being missed in speech. Please bear with me on this.

This is not as straight forward as I would like yet but here goes.

1. Run the server from a terminal and wait until you hear "ready"

<sub>code:</sub>
```
wine ~/open-sapi/tools/tcl/bin/tclsh85.exe ~/open-sapi/src/unstable/osapi-srv.tcl 2> /dev/null
```
<sub>end of code</sub>

2. Open another terminal and run the client with -p ? option. In the server terminal you will receive a list of voices and their coresponding numbers.

<sub>code:</sub>
```
~/open-sapi/src/unstable/osapi-cli.tcl -p ?
```
<sub>end of code</sub>

3.Run the client voice query command, then in the server terminal you should see something like this:

<sub>terminal output:</sub>
```
Message from sock680
Voice 0 = Microsoft Mary and is Female
Voice 1 = Microsoft Mike and is Male
Voice 2 = Microsoft Sam and is Male
Voice 3 = VW Kate and is Female
sapiRead
Connection closed from sock680 - 
```
<sub>end of output</sub>

4.Test your chosen voice please run:

<sub>code:</sub>
```
~/open-sapi/src/unstable/osapi-cli.tcl -p 3 -t This is some text to be spoken @@
```
<sub>end of code</sub>

The key information is 0,1,2,3. This information needs to changed in your speech-dispatcher config file.

5. Edit line 24 of the file ~/open-sapi/packages/speech-dispatcher/modules/open-sapi-generic.conf

<sub>code:</sub>
```
"echo '$DATA' | ~/open-sapi/src/unstable/osapi-cli.tcl -p 1 -r $RATE -l $VOLUME --pitch $PITCH --noxml -a --pipemode
```
<sub>end of code</sub>

You must replace the -p 1 with the number corresponding to your required speed engine.

Running the commands from the DeveloperStartup should get you running with your chosen speech engine.