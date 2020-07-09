# awk and sed useful tricks

## Oneliners

### Arguments

- More then one separator

      awk -F'[:;]' '{print $1, $2}'
      X=20;
      seq 1 | awk -v awkx=$X '{print $0, awkx}'

### Calculation

- Average with awk**

      echo -e "A 10\nB 20\nC 60" | awk 'BEGIN {sum=0; c=0; OFS=" "} {sum+=$2; c++} END {print "Average:", sum/c}'
      printf "A 10\nB 20\nC 60"  | awk 'BEGIN {sum=0; c=0; OFS=" "} {sum+=$2; c++} END {print "Average:", sum/c}'

### Conditions

- Print line if $X is equal\not equal to sth

   Third field is equal xyz

       cat file | awk '$3 ~ /xyz/ { print }'
   Second field is empty

       cat file | awk '($2 == "") {print $0}'
       cat file | awk '$2 ~ /^$/ {print }'

### Join evry X line

- Every 2nd line
  
      cat file | awk 'NR%2{printf "%s ",$0;next}{print;}'
      cat file | awk 'NR%2{printf "%s ",$0;next;}1'
      seq 10 | sed 'N;s/\n/ /'
      seq 10 | sed '$!N;s/\n/ /'

- Every 10th line

      cat file | awk 'NR%10{printf "%s ",$0;next}{print;}'

### Print arguments

- Skipping first element with loop

      seq 10 | xargs |  awk '{for (i=2;i<=NF;i++) print $i}'
      seq 10 | xargs |  awk '{$1="";print $0}' # Leaves space at the beginning
