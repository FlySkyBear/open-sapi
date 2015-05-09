

---

# Introduction #

Currently I am using Ubuntu 8.10. This is a standard installation using the default wine and pulseaudio versions. Currently this setup works but is not perfect. I have had problems with pulseaudio crashing which freezes the desktop. This i blame on my lack of error handling in my code a little bit to do with wine and pulseaudio and my ati HDMI audio drivers all together. :)

In theory any Linux distribution should work as long as you can get wine working on it with sound. There is no requirement for pulseaudio just that you can get sound from wine.

---

# Downloading the Source #

If you are keen to help out and want to contribute please visit the JoiningIn page on the wiki. There it gives details on how to become a project member and how to setup the SVN for a project member.

For everyone else you can continue to download the svn in read only mode.

You will need to download the sources from svn. This will provide you with all the tools and scripts that are needed to create a working development system. Make sure you are in the directory where you want the files to be downloaded before running the svn command.

If you are not sure you have svn installed run.

Code:
```
sudo apt-get install subversion
```

Then download the source files and tools from the project page.

Please note that if you plan to become an active developer and do not have svn experience then i recommend you register on the project first obtain a username and password before proceeding with an svn download. Please mail thomas lloyd at yahoo dot com to register.

Code:
```
svn checkout http://open-sapi.googlecode.com/svn/trunk/open-sapi
```

Please note Google Code is not the fastest at downloading and takes about ten minutes to get the whole project, (approx 37 Megabytes).

This should leave you in a position where you have everything ready to go about configuring the system for speech.

---

# Update Wine on ubuntu 9.xx #

For those users of 10.04 Lucid we have updated to a version of wine that supports using treads so you can skip this step.

## Update for Ubuntu 9.10 (Karmic) ##
Now the guys at Canonical have been busy and have made a very useful addition  tp the apt utility that allows the easy addition of personal software repositories. So we can add in the updated wine project repo with one command.

sudo add-apt-repository ppa:ubuntu-wine/ppa

## Ubuntu 9.04 and Other Dists ##
During testing there have been issues identified in the older wine releases current shipped with most Distributions. This has ben confirmed in Ubuntu but i am sure it applies to others. I highly recommend for stability to use the latest binary available from WineHQ for your distribution. Details on how to do this can be found at the link below. This will update your package source for wine briging it to the latest stable release for your distribution.

http://www.winehq.org/download


---

# Automatic Installation - Debian / Ubuntu #

If you are using Ubuntu and possibly Debian derived distros you can use the automated script to install and configure the system. Please can people e-mail any instructions and experiences they get with other distributions.

To start the installation using a terminal navigate to the installer folder in the local svn repository on your system.

You will find a script called osapi.run please execute this file. Please note that downloads are slow from Google and can take up to ten minutes.

Code:
```
~/open-sapi/installer/./osapi.run
```

For the package installation it requires sudo access and will ask for your password and then proceed to download and configure your system. If you want to know what i does see the manual process below.

This completes your setup please see the DeveloperStartup page for details on starting speech dispatcher, configuring wine, running the server, client and their options.

---

# Manual Installation - All Operating Systems #

These instructions are Debian / Ubuntu specific but you should not find it too hard to lookup the basics for another distro. Please add comments about your experiences and if possible post instructions.

1. Install required packages, please note there is no problem with asking reinstall existing software as it will just ignore the packages that already exist on the system:

Code:
```
sudo apt-get install wine speech-dispatcher python-speechd wget tcl gnome-orca cabextract
```

2. Download run the wineinit app. Only necessary for fresh wine installs, always run if unsure.

Code:
```
wget http://open-sapi.googlecode.com/files/wineinit.exe
wine wineinit.exe
```

3. Download & run winetricks, a helper script to get SAPI installed . Note you may have have to make this file executable.

Code:
```
wget http://open-sapi.googlecode.com/files/winetricks.sh
chmod 770 winetricks.sh
./winetricks.sh sapi51
```

4. Download the C++ runtime library and move it into wine.

Code:
```
wget http://open-sapi.googlecode.com/files/msvcp60.dll
cp -f msvcp60.dll $HOME/.wine/drive_c/windows/system32/
```

4. Run speech dispatcher user based configuration. Specify pulse for audio output method all other options can be left as default values..

Code:
```
spd-conf -u
```

4. If you have not already downloaded the source files please so do now. They are configured in such a way that they will run the scripts for both client and server without any more setup or compilation.

Please note that if you plan to become an active developer then i recommend you register on the project first obtain a username and password before proceeding with an svn download. Please mail thomas lloyd at yahoo dot com to register.

```
svn checkout http://open-sapi.googlecode.com/svn/trunk/open-sapi
```

This completes your setup please see the DeveloperStartup page for details on starting speech dispatcher, configuring wine, running the server and client applications.

---
