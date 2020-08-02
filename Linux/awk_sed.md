# awk and sed useful tricks

## Oneliners

### Arguments

More then one separator

    echo "A:B;C:D" | awk -F'[:;]' '{print $1, $2}'

Pass variable to awk

    X=20;Y=99
    seq 1 | awk -v awkx=$X -v awky=$Y '{print $0, awkx, awky}'

### Calculation

Average with awk**

    echo -e "A 10\nB 20\nC 60" | awk 'BEGIN {sum=0; c=0; OFS=" "} {sum+=$2; c++} END {print "Average:", sum/c}'
    printf "A 10\nB 20\nC 60"  | awk 'BEGIN {sum=0; c=0; OFS=" "} {sum+=$2; c++} END {print "Average:", sum/c}'

### Conditions

Print line if $X is equal\not equal to sth

Third field is equal xyz

    cat file | awk '$3 ~ /xyz/ { print }'

Second field is empty

    cat file | awk '($2 == "") {print $0}'
    cat file | awk '$2 ~ /^$/ {print }'

Second filed is not 'no ', but third is (separated by ';')

    cat file | awk -F';' '$2 !~/no / && $3 ~/no / {print $1, $2, $3}'

### Join evry X line

Every 2nd line
  
    cat file | awk 'NR%2{printf "%s ",$0;next}{print;}'
    cat file | awk 'NR%2{printf "%s ",$0;next;}1'
    seq 10 | sed 'N;s/\n/ /'
    seq 10 | sed '$!N;s/\n/ /'

Every 10th line

    cat file | awk 'NR%10{printf "%s ",$0;next}{print;}'
    seq 20 | awk 'NR%10{printf "%s ",$0;next}{print;}'

### Print every 'n^th^' line

Full line

    # Every third line
    seq 20 | awk 'NR % 3 == 0'
    # Every third line, with first
    seq 20 | awk 'NR == 1 || NR % 3 == 0'
    # Every fourth line starting from first line
    seq 20 | awk '(NR-1) % 4 == 0'
    # Every fourth line starting from second line
    seq 20 | awk '(NR-2) % 4 == 0'

Print specific argument

    seq -f 'X%03g' -s ' ' 10 | awk 'NR==1{print substr($2,1,2)}'
    seq -f 'A %02g'  10 | awk 'NR % 3 == 0{print substr($2,1,2)}'

First line, second argument (separated by ' ' and '.' )

    awk -F'[ .]' 'NR==1{print $2}'

### Print arguments

Skipping first element with loop

    # Line by line
    seq 10 | xargs | awk '{for (i=2;i<=NF;i++) print $i}'
    # In one line line, no separator, separator at the end
    seq 10 | xargs | awk '{for (i=2;i<=NF;i++) printf $i}'
    # In one line line, ';' as separator, separator at the end
    seq 10 | xargs | awk '{for (i=2;i<=NF;i++) printf $i";"}'
    # In one line line, ';' as separator, no separator at the end
    seq 10 | xargs | awk '{for (i=2;i<=NF-1;i++) printf $i";"; print $i}'
    # Leaves space at the beginning
    seq 10 | xargs | awk '{$1="";print $0}'

## Replace string 

### Remove from last character occurrence

`,[^,]\+` matches `,` followed by any number of characters except `,` and the match is replaced with empty string

    # Remove everything after last ','
    sed 's/,[^,]\+$//' file.csv
    # Remove everything after last '.' (extension)
    ls  -1 | sed -e 's/\.[^.]*$//'
