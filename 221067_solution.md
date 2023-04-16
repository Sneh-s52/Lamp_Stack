# Details

Rename this file in the format `yourRollNumber_solution.md` (example, `220000_solution.md`) and submit the solution in the Google form link provided 
*** https://forms.gle/RZtKpFcKfrWrYYxF9 ***


## Your zeroth approach below

Reasoning - I just simply ran the C file and made the correction with unsigned and char**. The output came on the debug console in vs code - "The answer of this challenge is output of "man" when run on the terminal, copy the exact output"

Unknown locale, assuming C
This manpage is not compatible with mandoc(1) and might display incorrectly.

          if [ $found -eq 0 ]; then               bad="$bad\n$key: nothing appropriate"             rval=1         fi #endif      done

     # Strip leading carriage return.   good=${good#\n}     bad=${bad#\n}

     if [ -n "$good" ]; then #ifdef __APPLE__          printf "%b0 "$good" | $WHATISPAGER #else #        echo -e "$good" | $MANPAGER #endif      fi

     if [ -n "$bad" ]; then #ifdef __APPLE__           printf "%b0 "$bad" >&2 #else #          echo -e "$bad" >&2 #endif     fi

     exit $rval }

# Usage: setup_cattool page # Finds an appropriate decompressor based on extension setup_cattool() {     case "$1" in   *.bz)     cattool='/usr/bin/bzcat' ;;   *.bz2)    cattool='/usr/bin/bzcat' ;;
#ifdef __APPLE__    *.gz)     cattool='/usr/bin/zcat -f' ;; #else #   *.gz)     cattool='/usr/bin/zcat' ;; #  *.lzma)   cattool='/usr/bin/lzcat' ;; # *.xz)     cattool='/usr/bin/xzcat' ;; #endif      *)
     cattool='/usr/bin/zcat -f' ;;      esac }

# Usage: setup_pager # Correctly sets $MANPAGER setup_pager() {  # Setup pager.      if [ -z "$MANPAGER" ]; then        if [ -n "$MANCOLOR" ]; then             MANPAGER="less -sR"           else
               if [ -n "$PAGER" ]; then                     MANPAGER="$PAGER"             else                     MANPAGER="less -s"            fi        fi   fi #ifdef __APPLE__      # whatis/apropos
have historically used more(1) on Apple systems,  if [ -z "$WHATISPAGER" ]; then          if [ -n "$MANCOLOR" ]; then             WHATISPAGER="more -ER"        else                if [ -n "$PAGER" ];
then                     WHATISPAGER="$PAGER"               else                     WHATISPAGER="more -E"              fi        fi   fi #endif      decho "Using pager: $MANPAGER" }

# Usage: trim string # Trims whitespace from beginning and end of a variable trim() {     tstr=$1   while true; do           case "$tstr" in          [    ]*)  tstr="${tstr##[     ]}" ;;         *[   ])
     tstr="${tstr%%[     ]}" ;;         *)        break ;;       esac      done }

# Usage: whatis_parse_args "$@" # Parse commandline args for whatis and apropos.  whatis_parse_args() {  local cmd_arg  OPTIND=1 #ifdef __APPLE__     while getopts 'ds:' cmd_arg; do #else # while
getopts 'd' cmd_arg; do #endif          case "${cmd_arg}" in          d)   debug=$(( $debug + 1 )) ;; #ifdef __APPLE__       s)   MANSECT=$OPTARG ;; #endif          *)   whatis_usage ;;          esac
     done >&2

     shift $(( $OPTIND - 1 ))

     keywords="$*" }

# Usage: whatis_usage # Display usage for the whatis/apropos utility.  whatis_usage() {   echo "usage: $cmd [-d] [-s mansect] keyword [...]"     exit 1 }

# Supported commands do_apropos() { #ifndef __APPLE__ #     [ $(stat -f %i /usr/bin/man) -ne $(stat -f %i /usr/bin/apropos) ] && #          exec apropos "$@" #endif      search_whatis apropos "$@" }

do_man() {     man_parse_args "$@"      if [ -z "$pages" ]; then           echo 'What manual page do you want?' >&2          exit 1    fi   man_setup

#ifdef __APPLE__    while read page; do           if [ -z "${page}" ]; then               continue       fi #else #     for page in $pages; do #endif           decho "Searching for $page"
          man_find_and_display "$page" #ifndef __APPLE__ #  done #else     done <<EOF $pages EOF #endif

     exit ${ret:-0} }

do_manpath() {      manpath_parse_args "$@"  if [ -z "$qflag" ]; then           manpath_warnings    fi   if [ -n "$Lflag" ]; then           build_manlocales         echo $MANLOCALES    else
          build_manpath       echo $MANPATH  fi   exit 0 }

do_whatis() { #ifndef __APPLE__ #  [ $(stat -f %i /usr/bin/man) -ne $(stat -f %i /usr/bin/whatis) ] && #      exec whatis "$@" #endif  search_whatis whatis "$@" }

# User's PATH setting decides on the groff-suite to pick up.  EQN=eqn NROFF='groff -S -P-h -Wall -mtty-char -man' PIC=pic REFER=refer TBL=tbl TROFF='groff -S -man' VGRIND=vgrind

LOCALE=/usr/bin/locale STTY=/bin/stty SYSCTL=/sbin/sysctl

debug=0 man_default_sections='1:8:2:3:3lua:n:4:5:6:7:9:l' #ifdef __APPLE__ man_default_path='/usr/share/man:/usr/local/share/man' #else
#man_default_path='/usr/share/man:/usr/share/openssl/man:/usr/local/share/man:/usr/local/man' #endif cattool='/usr/bin/zcat -f'

config_global='/etc/man.conf'

# This can be overridden via a setting in /etc/man.conf.  config_local='/usr/local/etc/man.d/*.conf'

# Set noglobbing for now. I don't want spurious globbing.  set -f

case "$0" in *apropos)   do_apropos "$@" ;; *manpath)  do_manpath "$@" ;; *whatis)   do_whatis "$@" ;; *)          do_man "$@" ;; esac
---

## Your first approach below (first.txt)

Reasoning - used rot13.com and tried various rot and the answer came in rot 8 . Before this I tried other ciphering methods.

noicee you did crack a rotation encryption on your own. The following is a clue for the next puzzle: CLASS of that INPUT


---

## Your second approach below (strings.txt)

Reasoning - simply searched strings.txt on my finder and the path is given below : 
/Users/sneh/Downloads/Lamp_Stack_task/question_mark/Lamp_Stack/1/5/0/3. It can also be done by using grep on terminal.

The file contained - 
kw4QLNylm2inErX
DabAWF1UenBD2W
kPVEQPc6ZN8x2jn
g4JoMqFZyat9vd5
ORNwuwGtKDLydge
TqMuGims7vlJtno
8dc2evcCSSc4kUy (password)

---

## Your third approach below (fourth.zip)

Reasoning - Opened the zip file by locating each string's file name from finder or by using grep. Further used grep -inr to find the desired string.

The password is 'eleven.txt'. I used this command 'grep -inr DevOps' which led me to the path of ./4/2_inner/0.txt:2:DevOps{y0ur3_4w350m3_4nd_0ne_5t3p_c1053r}.

The desired string is - DevOps{y0ur3_4w350m3_4nd_0ne_5t3p_c1053r}


---


- Name : Sneh Sinha
- Roll : 221067
- GitHub username: Sneh-s52
- Discord username: sneh_s52


## Do not tamper below this line

---

Q29yZSB0ZWFtIGtvIGZha2UgZG8=
