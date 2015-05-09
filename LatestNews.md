See the DevelopmentStatus page for details on what is left to do.

---


# News - 23/03/10 #

---

Latest News,

So where we are now. I have a reasonably stable open-sapi that runs
with Speech Dispatcher and Orce through wine. It is fast responsive
and sounds nice. Changing the voice in open-sapi is a pain at the
moment and none of the Orca setting pitch, volume and rate actually
take affect . If people would like a sneaky peak I can get the pitch
volume and rate all working and release a pre-Alpha deb. Let me know
if your interested.

Change Log:

  * Fixed command line bugs with ?
  * Enable file/wav format changes
  * Enabled wav file output
  * Streamlined Code
  * Moved to a multi threaded model
  * Reworked the debugger to use threads
  * Reworked speech output to use threads
  * Rework audio output to use Memory Streams

A recent move to Lucid has meant that open-sapi had to evolve in a new
direction.

The update of wine in Lucid was a very much needed component for open-
sapi to even run under Ubuntu. This now allows for the multi threaded
server to run smoothly with significant performance improvements with
open-sapi responsiveness and application start up times.

However with every update comes another problem. We are supposed to
call it progress.

The wine ESD sound driver is soo out of date that pulse audio and wine
are no longer best friends and the audio is sometimes distorted
sometimes not, with lots of pops and fizzes on the output. Also from
what I read this is different depending on your hardware. So using the
wine audio subsystem is not really viable anymore for open-sapi.

So I have begun development to get RAW audio data from sapi and pass
that to the client who can do what they want with it. The proof of
concept is done and I have RAW audio streams that I can process,
redirect anyway I want. This was a big project milestone as it was a
stopper on the development of the Speech Dispatcher module. Also it
allows me to follow on to actually creating a speech server which can
output multiple streams to multiple clients at the same time.

---

# News - 23/08/09 #
I am now running open-sapi reliably using Ubuntu 9.04. The only modification is running the most recent binary release of wine which is helping stability. I have managed to run the system for a whole day without a crash and now believe it to be stable enough to use on a regular basis.

There are still issues and unimplemented features. There are also avenues of investigation like increased integration into speech dispatcher. So a lot of work but things are stable and that was a big milestone for the project,

Next comes testing with wav output that is then managed by speech dispatcher rather than replying on the wine audio system and management by the SAPI server. This will hopefully harness the power of speech dispatcher and increase the systems performance. This is where the testing will come into play.

Development of an Open Sapi specific module will allow for the selection of voice through applications and more tightly integrated control and feedback to speech dispatcher. This may out perform the wav output solution detail above and provide a better solution but this is a bit of trial and error. The first solution will also provide the feature to output audio into a wav file which is a nice feature to have and not overly complicated so i will try that first.

To get some real feedback i also need to implement more tracking and status information and a logging system that stores it all away.

Finally a configuration file for the client and server that can be used to modify options  would be really useful for the future. So more work.....

---

# News - 03/06/09 #

After some heavy bug hunting with many fixes applied, we are getting close to the first stable release of open-sapi for the first development phase. Recently I have been concentrating on the testing of different encoding systems and so far have a working system for european languages. Others are untested at this time.

I have fixed the speech-dispatcher to open-sapi synchronisation problem and now seem to be encountering bugs from the other packages. Having just request help from other testers I am awaiting more bugs to be reported.

---

# News - 17/03/09 #

The required minimum to get a working system has been uploaded to SVN and added to the wiki pages to allow those intreted to download the progress so far. There has been no progress on from the last headline as i have been working to tranfer the project online since then so the last healine is still relavant.

---

# News - 05/03/09 #

A discussion group has been started for users and developers to give their feedback. [DiscussionGroup](http://groups.google.com/group/open-sapi)

I have just updated details on the wiki of how to setup a DeveloperEnvironment for helping with the project. Stability and responsiveness are issues at the moment. I am planning to rework the server and client to exchange speech XML markup to try and lower the response times for the client and server. Stabiliity issues lie around pulseaudio on my system at the moment but i have not investigated newer releses yet. Lastly it may improve compatability to move to the latest version of wine available but again this is trial and error.

---

# News - 18/01/09 #

The client and server are now working with Speech Dispatcher and Orca in Ubuntu 8.10. This seems to be quite responsive and on the most part stable. The next thing to do is get a simple install process and implement the last few requirements for the first general release.

---

# News - 06/01/09 #

Completed the first stable release of the server and client today. So far implemented a single client server that support changes in speech engine, volume, rate, synchronous and asynchronous speech modes, XML mark-up even thought this is not available through the command line interface yet.

---

