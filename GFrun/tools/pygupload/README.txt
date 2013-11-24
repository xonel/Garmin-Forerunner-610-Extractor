LICENSE:

See LICENSE.txt


DISCLAIMER:

# THE COPYRIGHT HOLDERS AND/OR OTHER PARTIES PROVIDE THE PROGRAM 
# �AS IS� WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESSED OR 
# IMPLIED, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES 
# OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE. THE 
# ENTIRE RISK AS TO THE QUALITY AND PERFORMANCE OF THE PROGRAM 
# IS WITH YOU. SHOULD THE PROGRAM PROVE DEFECTIVE, YOU ASSUME 
# THE COST OF ALL NECESSARY SERVICING, REPAIR OR CORRECTION.
# USE AT YOUR OWN RISK.


DESCRIPTION:

Garmin Connect Python Uploader, gupload.py, uploads files 
(.tcx, .gpx, and .fit files ) created by Garmin fitness 
devices to the http://connect.garmin.com web site.


REQUIREMENTS:
Tested on Python 2.6.5 under Linux and 2.7.2 under Windows XP.

Required Python Modules:
argparse
ConfigParser
logging
glob
platform
string
urllib
urllib2
mimetools
mimetypes
os
stat
cStringIO
json or simplejson

INSTALL:

Linux Install: 
unzip gupload.zip to /opt/pygupload
create a symbolic link
sudo ln -s  /opt/pygupload/gupload.py /usr/local/bin/gupload.py

Windows Install:
unzip pygupload.zip file to c:\pygupload
add c:\pygupload to your PATH environment variable (use google)

Linux + Windows:
You may create a config file containing your Garmin Connect
username and password to eliminate the need to type it in 
on the command line.  WARNING!!! The username and password
are stored in clear text, WHICH IS NOT SECURE.  If you have 
concerns about storing your garmin connect username and 
password in an unsecure file, do not use this option.

Create a text file named .guploadrc (gupload.ini for Windows
users) containing the following:
[Credentials]
username=<username>
password=<password>

Replace <username> and <password> with your Garmin Connect
login credentials.  gupload.py looks for this file either in
your home directory (usually something like '/home/<username>' 
in Linux, or C:\Documents and Settings\<username>' in Windows)
, or in the current working directory (the directory you are 
in when you execute gupload.py).  See help below for priority 
information. 


HELP:

usage: gupload.py [-h] [-a A] [-l L L] [-v {1,2,3,4,5}]
                  filename [filename ...]

A script to upload .TCX, .GPX, and .FIT files to the Garmin Connect web site.

positional arguments:
    filename        Path and name of file(s) to upload.

optional arguments:
  -h, --help      show this help message and exit
  -a A            Sets the activity name for the upload file. This option is
                  ignored if multiple upload files are given.
  -l L L          Garmin Connect login credentials '-l username password'
  -v {1,2,3,4,5}  Verbose - select level of verbosity. 1=DEBUG(most verbose),
                  2=INFO, 3=WARNING, 4=ERROR, 5= CRITICAL(least verbose).
                  [default=3]

Username and password credentials may be placed in a configuration file
located either in the current working directory, or in the user's home
directory.  WARNING, THIS IS NOT SECURE. USE THIS OPTION AT YOUR OWN
RISK.  Username and password are stored as clear text in a file
format that is consistent with Microsoft (r) INI files.                       

The configuration file must contain a [Credentials] section containing 
'username' and 'password' entries.

The name of the config file for non-windows platforms is '.guploadrc'
for windows platforms the config file is named 'gupload.ini'.

Example '.guploadrc' (or 'gupload.ini' for windows):
[Credentials]
username=<myusername>
password=<mypassword>

Replace <myusername> and <mypassword> above with your own login
credentials.

Priority of credentials:
Command line credentials take priority over config files, current 
directory config file takes priority over a config file in the user's
home directory.


EXAMPLE:
Upload file and set activty name:
gupload.py -l myusername mypassword -a 'Run at park - 12/23' myfile.tcx

Upload multiple files:
gupload.py -l myusername mypassword myfile1.tcx myfile2.tcx myfile3.fit

Upload file using config file for credentials, name file, verbose output:
gupload.py -v 1 -a 'Run at park - 12/23' myfile.tcx

