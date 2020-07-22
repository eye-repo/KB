# Frequently used commands

## bash

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

- Change timestamp in audit.log

      cat /var/log/audit/audit.log | awk '{print strftime ("%F %T",substr($2,11,10))" "$0}'

- Change timestamp to human readable form

      date -d @1477401122

- Get date in line

      CDATE=$(date +%Y-%m-%d_%H:%M:%S) ; ps auxf | awk -v cDate=$CDATE '{print cDate, $0}'
      CDATE=$(date +%Y-%m-%d_%H:%M:%S) ; ps auxf | awk -v cDate=$CDATE '{print cDate" "$0}'
      ps auxf | awk '{print strftime("%Y-%m-%d %H:%M:%S")" "$0}'

### Redirect outputs

- All to /dev/null

      &> /dev/null
      > /dev/null 2>&1`

## Tools

### sshpass

Single command

    sshpass -f file.txt ssh -oStrictHostKeyChecking=no -oConnectTimeout=5 user@$host 'ls -la /etc/hosts'

In loop

    for h in localhost ; do echo $h; sshpass -f file.txt ssh -oStrictHostKeyChecking=no -oConnectTimeout=5 user@${h} 'ls -la /etc/hosts' 2>/dev/null; done
    for h in localhost ; do echo $h; sshpass -f file.txt scp -oStrictHostKeyChecking=no -oConnectTimeout=5 src_file.txt user@${h}:/tmp/ ; done

### tar

List command

    tar -tvf file.tar
    tar -ztvf file.tar.gz
    tar -tvf projects.tar.bz2 '*.pl'

Read file

    tar -axf file.tgz foo/bar -O
