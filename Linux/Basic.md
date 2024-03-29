# Frequently used commands

## bash

### SSH KeyGen
 
    ssh-keygen -t ed25519
    ssh-keygen -t rsa -b 4096

### Set PS1

    PS1="[\u@\h \W ]# "
    [user@home log ]#
    
    PS1="[\u@\h \w ]# "
    [user@home /var/log ]#
    echo ${var^^} ${var,,}

### Display string variables in bash

UPPERCASE & lowercase  
`echo ${var^^} ${var,,}`

String length  
`echo ${#var}`

Print string from second character  
`echo ${var:1}`

Print firts three characters (3 chars starting from 0)  
`echo ${var:0:3}`

Print last four characters  
`echo ${var: -4}`

Print from third character and skipping last four characters  
`echo ${var:2: -4}`

Remove leading\trailing\all whitespace from a string

      echo ${text##+([[:space:]])}
      echo ${text%%+([[:space:]])}
      echo ${text//[[:space:]]}

Replace `[[:space:]]` to remove other chracters. Enabling extglob can be useful. If set (should be as default), the extended pattern matching features are enabled.

      shopt -s extglob
      BVAR="ABC123xyz"
      echo ${BVAR##*1}  # 23xyz
      echo ${BVAR%%3*}  # ABC12
      echo ${BVAR//1*3} # ABCxyz

### Copy with date

Date format: 20200202010101

    $(date +%Y%m%d%H%M%S)
    $(date +%Y%m%d%H%M%S).bak
    cp file file.$(date +%Y%m%d%H%M%S).bak

Date format: 20200202-010101

    $(date +%Y%m%d-%H%M%S)
    $(date +%Y%m%d-%H%M%S).bak
    cp file file.$(date +%Y%m%d-%H%M%S).bak

Date format: 2020-02-02 01:01:01

    $(date +'%Y-%m-%d %H:%M:%S')

### Calculation

Adding two variables

    c=$((a + b))
    c=$(($a + $b))
    c=`expr $a + $b`
    c=$(expr $a + $b)

Increase\Decrease number

    ((i=i+1))
    ((i=i-1))

### Lowercase, Uppercase
  
Tu Uppercase

    echo ${var^^} 
    echo $var | tr '[:lower:]' '[:upper:]'
    echo $var | awk '{print toupper($0)}'
    echo $var | sed -e 's/\(.*\)/\U\1/'
    echo $var | sed 's/.*/\U&/'

To Lowercase

    echo ${var,,}
    echo $var | tr '[:upper:]' '[:lower:]'
    echo $var | awk '{print tolower($0)}'
    echo $var | sed -e 's/\(.*\)/\L\1/'
    echo $var | sed 's/.*/\L&/'

### Simple loops

    for i in {1..3} ; do echo $i; done
    while true; do echo 1; done
    while [ 1==1 ]; do echo 1; done
    while read line ; do echo $line ; done <file
    while read line ; do echo $line ; done < <(cat file)
    cat file | while read line ; do echo $line ; done

### Timestamps

Change timestamp in audit.log

    cat /var/log/audit/audit.log | awk '{print strftime ("%F %T",substr($2,11,10))" "$0}'

Change timestamp in .bash_history

    cat .bash_history | awk '{ if (substr($1,1,1) == "#" && length($1) == 11 ) {print $1, strftime("%F %T",substr($1,2,10))} else {print} }'

Change timestamp to human readable form

      date -d @1477401122

Get date in line

    CDATE=$(date +%Y-%m-%d_%H:%M:%S) ; ps auxf | awk -v cDate=$CDATE '{print cDate, $0}'
    CDATE=$(date +%Y-%m-%d_%H:%M:%S) ; ps auxf | awk -v cDate=$CDATE '{print cDate" "$0}'
    ps auxf | awk '{print strftime("%Y-%m-%d %H:%M:%S")" "$0}'

### Redirect outputs

All to /dev/null

    &> /dev/null
    > /dev/null 2>&1`

Print as error

    echo 'ERROR' >/dev/stderr
    # Function
    lerr(){
        echo "ERROR: $@" >>/dev/stderr
    }
    # or
    lerr(){
        echo "$(date +'%Y-%m-%d %H:%M:%S') ERROR: $@" >>/dev/stderr
    }

## Tools

### sshpass

Single command

    sshpass -f file.txt ssh -oStrictHostKeyChecking=no -oConnectTimeout=5 user@$host 'ls -la /etc/hosts'

In loop

    for h in localhost ; do echo $h; sshpass -f file.txt ssh -oStrictHostKeyChecking=no -oConnectTimeout=5 user@${h} 'ls -la /etc/hosts' 2>/dev/null; done
    for h in localhost ; do echo $h; sshpass -f file.txt scp -oStrictHostKeyChecking=no -oConnectTimeout=5 src_file.txt user@${h}:/tmp/ ; done

### tar

List files

    tar -tvf file.tar
    tar -ztvf file.tar.gz
    tar -tvf projects.tar.bz2 '*.pl'

Read file

    tar -axf file.tgz foo/bar -O

Search files in multiple archives and print them

    ls *.tgz | while read tf; do tar -tf ${tf} '*file' 2>/dev/null ; done
    ls *.tgz | while read tf; do echo ${tf}; tar -tf ${tf} '*file' 2>/dev/null ; done
    # Print content of the searched files
    ls *.tgz | while read tf; do tar -tf ${tf} '*file' 2>/dev/null | xargs -r -L1 tar -axf ${tf} -O ; done
    find . -name "*.tgz" | while read tf; do echo $tf ;tar -tf ${tf} '*file' 2>/dev/null | xargs -r -L1 tar -axf ${tf} -O | grep foo; done

### xargs & seq

Basic

    seq -s' ' 10 | xargs -n1
    seq -s' ' 10 | xargs -n2
    seq -f "A %G" 10 | xargs -n3 echo
    seq -f "A %02G" 10 | xargs -L1 echo
    seq -f "A %02G" 10 | xargs -L2 echo

Skip empty value

    for i in {1..3} ; do [[ $i -eq 2 ]] && unset i; echo $i | xargs echo; done
    for i in {1..3} ; do [[ $i -eq 2 ]] && unset i; echo $i | xargs -r echo; done

Assign to variable

    seq  10 | xargs -I {} echo Test {}
    seq  10 | xargs -I getval echo grep getval file
    seq -f "A %G" 10| xargs -I val echo val:val
    seq -f "A %G" 10| xargs -I val echo VAL:val

Read two values in one line

    seq 10 | xargs printf 'First %s, Next %s\n'
    seq 10 | xargs -n2 printf 'First %s, Next %s\n'

### nmap

Check SSL

    nmap --script ssl-cert -p 443 jumpnowtek.com
    nmap --script ssl-enum-ciphers -p 443 jumpnowtek.com
