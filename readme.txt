This is fairly strait forward script. It sweeps an ip range and coppys the up hosts to the clipboard for an easier day
with nessus.

Usage:
$ ruby pingsweep.rb
Input Starting IP Address: 192.168.0.0
Input Ending IP Address: 192.168.0.255

Working..................................................................................................
..........................................
Finished found hosts at: 192.168.0.1, 192.168.0.2, 192.168.0.16, 192.168.0.137, 
Host are copied to clipboard ready for nessus
Have a nice day

Hope this save you time enjoy and live well all :)

Installation
You will need the clipboard gem

$ gem install clipboard

I have tested this with linux and it works I don't know about OSX or Windows let me know