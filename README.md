**ps3-cloud-drive**
===============

Based on the original source code by mhaqs in https://github.com/mhaqs/ps3-cloud-drive.

**Main differences:**
- Removed the need for authenticated curl agent in CurlAgent.cpp
- Corrected API calls and body for current OAUTH 2.0.
- Added sfo.xml and ICON0.PNG files required to build pkg file.
- Created Google Cloud Service and enabled API. As of December 2025, I will host this in my Google account, however, the free version allows 12000 requests per minute. If this increases, I will need to remove it (otherwise I have to pay). In any case the procedure to build and create your own working version is below.

**Procedure to build (I used Ubuntu 24.04):**

- ps3toolchain needed (https://github.com/ps3dev/ps3toolchain). As of December 2025, the script 009 will fail. You will need to download it manually and resolve the failing dependencies (bad links towards unexistent files).

- I will add a ps3toolchain fork containing the updated libraries at a later time and add a link to it here.

- Go to the Google Cloud Services Console and create a project. In that project, enable the Google Drive API. This will generate a client-id and a client secret, which you will need to replace in the main.cpp file (lines 68 and 69).

- With the proper keys and all dependencies installed, simply run 'make' to build the .elf file, then 'make pkg' to build the .pkg file.

**Procedure to debug and see logs:**

- Replace the IP address in log.cpp (line 9) with the IP of your computer.
- From a terminal window, simply run 'nc -u -l -p 18194'.
- Start the app on your PS3 and you will see the logs appear.

**NOTE:** When authorizing your device in your google account, make sure to check the box giving permission to do create/edit/update/delete operations to your Drive account :). Otherwise, it will have access to your profile and email but not your Drive.

**Original README:**

An open source cloud sync utility for Playstation 3 games saves.

You will need the ps3toolchain setup and PSL1GHT working to compile this.
I have committed the required libraries including the SSL libraries to the
ps3toolchain.

You will need to create a Google Drive application using the Google Services
console. Enter the client_secret and app_id into the main.cpp file before 
attempting compilation.

A note about the root certificate mentioned in the source code. The root certificate
was taken from the polarssl library. The newer distributions do not carry a root
certificate, so you can either take one from the ps3 hard drive or from an available
openssl package. I cannot package it into the repo.

Portlibs required to compile:
(look for this commit on ps3libraries https://github.com/mhaqs/ps3libraries/commit/bc2de847dad3e79677aa2acdab6ea07256ef2a66)

- Updated libcurl to the latest version 7.31.0.
- Ported polarssl 1.2.8 to psl1ght.
- Reorganized ps3libraries script order to compile curl with polarssl support. SSL support is enabled in curl.
- Ported lib json-c to psl1ght.
- Updated patches for libcurl, polarssl for compilation.
- Updated execution rights on new scripts.
- zlib script execution fix introduced in last commit


For usage see: http://www.tabinda.net/posts/playstation-3-cloud-drive/
