

---

# Current Status: #
Currently the project is only available for download through svn see   	 DeveloperEnvironment for details of how to do this. We are someway off making a public release of the porject but keep watching.

---

# Done #
  * SAPI 5.1 on Wine
  * Ubuntu 10.04 Testing
  * Speech Dispatcher Testing and Config
  * UTF-8
  * SAPI XML Markup
  * Performance issues
  * Reliability issues (Work in Progress)
  * Error handling
  * Sanity Checks
  * Multi Threading Model
  * Raw audio data output
  * Flexible debugging system
  * Client global & transaction timeouts
  * Server Control - client spawns server if it has crashed ;) or is not yet started
  * File output
  * Changeable Output Wav Format
  * Improved debugging system

---

# Still Todo (List not complete) #

## Server ##
  * Sound Icons
  * Config files
  * Implement as a Service ?
  * Investigate commandline only execution
  * Implement one voice per client
  * Implementation of Global Multi Dimensional Array for Data Sharing

## Client ##
  * Global Array for Event Tracking should be unset at some point
  * Sound Icons
  * Config files
  * Sanity Checks  (list length on text)

  * Test performance, possible migration to native C

## Server-GUI ##
  * Research GTK & Orca & TCL & Gnome Accessibility

## Installer ##
  * Install commandline and server Apps
  * Test with different sound servers and see results of an incorrect config

## Speech Dispatcher ##
  * Investigate specific open sapi SD module