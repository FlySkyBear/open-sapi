Please note this information is not complete, please ask questions in the disussion group to help me add more relavant content.


---

# Quick Reference Commands & Examples #
These commands assume the location of the open-sapi svn directory is in your home folder. If you ahve chosen a different location then please read the notes on speech-dispacher below and change code examples to mirror your locations.

## Server Startup ##
Running the server for the first time as a stand alone application is a good idea so you can analyse any problem with the installation. After you have confirmed the server to be working you can run the client and it will auto load the server if it is not already running. By default for development purposes the server timesouts after 60 seconds. This can be extended by calling the --timeout x (x is a number of mins,0 disabled time-outs).

When the server is first run it should say in the default voice "Ready" if you do not hear this then you have a configuration problem see the TroubleShooting page. Try removing the 2> /dev/null part of the command to get all error output. This will help when you look at the TroubleShooting Page.

Code:
```
wine ~/open-sapi/tools/tcl/bin/tclsh85.exe ~/open-sapi/rockbox/client-server/rbutil-sapi-server.tcl -v --debug
```

Later on when you get annoyed with wines annoying error messages you can append 2> /dev/null onto the end of the command to hide then. If your developing this is not recommended.

## Running Client Simple text test ##

Code:
```
~/open-sapi/rockbox/client-server/rbutil-sapi-cli.tcl -t This is a test of the Open Sapi project @@ -v --debug
```

## Running Client pipe mode test ##

Code:
```
who | ~/open-sapi/rockbox/client-server/rbutil-sapi-cli.tcl --pipemode
```

## Running Speech Dispatcher ##
Startup speech dispatcher with custom configuration file from svn. This custom file is set to use Pulseaudio but as far as i know does not affect the output as wine handels the audio at the moment.

**Note:
If you have chosen to use a custom location to store the SVN files then it is important to modify the open-sapi/packages/speech-dispatcher/modules/open-sapi-generic.conf file at line 24. The client location is hardcoded at the moment and you must change to the new location of the client. This is temproray until we migrate the tools into /usr/lobal/bin.**

Code:
```
killall speech-dispatcher; speech-dispatcher -C ~/open-sapi/packages/speech-dispatcher/
```

After this has been confirmed to work then your ready to fire up Orca.


---

# Advanced Server Notes #

At the moment the verbose output option is enabled on the server by default and not on the cient the output for any query using a ? for available engines volume rate and devices will appear on STDOUT of the terminal you have run your server from.

---

# Advanced Client Notes #

At the moment the verbose output option is enabled on the server by default and not on the cient the output for any query using a ? for available engines volume rate and devices will appear on STDOUT of the terminal you have run your server from.

Usage output for the client:

Open-SAPI Commandline Interface v0.1 Alpha

Usage: osapi-cli ...[swithches](swithches.md) -adihloprsvx -t "message"
A command line interface providing access to the text to speech (TTS) capabilities of the Microsoft Speech Engine (SAPI)

Optional switches:

  * -t, --text text        : Text to be spoken terminal with @@
  * -l, --volume value     : Sets Volume Level. Range Min 0 - 100 Max
  * -r, --rate value       : Sets Speech Rate. Range Min 0 - 20 Max
  * -p, --person value     : Sets Default Person
  * -d, --device value     : Sets Audio Device
  * -v, --verbose          : Verbose output
  * --pipemode             : Pipemode takes input on stdin to speak
  * -h, --help             : This message

**Using ? instead of a numerical value will return the server setting**

For updates, guides and help please refer to the project page found at:
http://code.google.com/p/open-sapi/w/list
For bugs, comments and support please contact thomaslloyd@yahoo.com.nospam