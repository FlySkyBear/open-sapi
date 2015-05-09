# Quick Install Guide for SAPI4 #


Please note open-sapi as yet does not support SAPI4 voice. This has been done on request for another user.

To start you must make sure you have already downloaded the [winetricks.sh](http://code.google.com/p/open-sapi/downloads/detail?name=winetricks.sh&can=2&q=)

You can get this from the Downloaded section on the site or you can update your svn if you have already set up open-sapi by executing this command:

`cd ~/open-sapi; svn up`

This will update to the latest version of open-sapi. If you have just installed open-sapi then you will not need to update.

You can now install SAPI4 and your choice of UK or US voices using the following commands. (Visually Impaired users read to the bottom of the commands).

`sh ~/open-sapi/installer/winetricks.sh sapi4 sapi4_uk_voices`

or

`sh "path to your downloaded"/winetricks.sh sapi4 sapi4_uk_voices`

replace sapi4\_us\_voices for the US voices.

Visually imapred users: One of the install packages need you to press "Alt+Y" so please wait about 30 seconds, maybe longer if you have a slow internet connection and then press "Alt+Y". Can someone test this and give me feedback. Thanks.

That should be SAPI4 Installed. I have had it talking with a test app but not perfectly without some errors. Again feedback on this please.