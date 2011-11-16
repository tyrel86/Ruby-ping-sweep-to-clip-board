This is fairly strait forward script. It sweeps an ip range and prints to standard out all the hosts that were up. I have made them comma sperated so that I can coppy them into nessus.

Usage:
$ ruby pingsweep.rb
Input Starting IP Address: 192.168.1.0
Input Ending IP Address: 192.168.1.255

192.168.1.1, 
192.168.1.8, 
192.168.1.10, 
192.168.1.28, 
192.168.1.159,

I usualy pipe the output to the clipboard so I can copy the uphosts directly to nessus for a thural security scan.

$ ruby pingsweep.rb | cb

that cb function is a great little tool cortesy of http://madebynathan.com/2011/10/04/a-nicer-way-to-use-xclip/ just coppy the following script to your .bashrc.

Hope this save you time enjoy and live well all :)

# A shortcut function that simplifies usage of xclip.
# - Accepts input from either stdin (pipe), or params.
# - If the input is a filename that exists, then it
#   uses the contents of that file.
# ------------------------------------------------
cb() {
  local _scs_col="\e[0;32m"; local _wrn_col='\e[1;31m'; local _trn_col='\e[0;33m'
  # Check that xclip is installed.
  if ! type xclip > /dev/null 2>&1; then
    echo -e "$_wrn_col""You must have the 'xclip' program installed.\e[0m"
  # Check user is not root (root doesn't have access to user xorg server)
  elif [[ "$USER" == "root" ]]; then
    echo -e "$_wrn_col""Must be regular user (not root) to copy a file to the clipboard.\e[0m"
  else
    # If no tty, data should be available on stdin
    if ! [[ "$( tty )" == /dev/* ]]; then
      input="$(< /dev/stdin)"
    # Else, fetch input from params
    else
      input="$*"
    fi
    if [ -z "$input" ]; then  # If no input, print usage message.
      echo "Copies a string or the contents of a file to the clipboard."
      echo "Usage: cb <string or file>"
      echo "       echo <string or file> | cb"
    else
      # If the input is a filename that exists, then use the contents of that file.
      if [ -f "$input" ]; then input="$(cat $input)"; fi
      # Copy input to clipboard
      echo -n "$input" | xclip -selection c
      # Truncate text for status
      if [ ${#input} -gt 80 ]; then input="$(echo $input | cut -c1-80)$_trn_col...\e[0m"; fi
      # Print status.
      echo -e "$_scs_col""Copied to clipboard:\e[0m $input"
    fi
  fi
}
# Shortcut to copy SSH public key to clipboard.
alias cb_ssh="cb ~/.ssh/id_rsa.pub"
