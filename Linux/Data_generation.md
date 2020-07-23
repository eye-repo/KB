# Generate data

## Files

### Create files

Generate 1M file filled with zeros

    dd if=/dev/zero of=/tmp/out.file bs=1024 count=1024
    dd if=/dev/zero of=/tmp/out.file bs=1048576 count=1
    dd if=/dev/zero of=/tmp/out.file bs=$((1024 * 1024)) count=1
    dd if=/dev/zero of=/tmp/out.file bs=1 count=$((1024 * 1024))
    dd if=/dev/zero of=/tmp/out.file bs=1M  count=1

Generate 10M file filled with zeros

    dd if=/dev/zero of=/tmp/out.file bs=$((1024 * 1024)) count=10
    dd if=/dev/zero of=/tmp/out.file bs=1M  count=10
    dd if=/dev/zero of=/tmp/out.file bs=10 count=$((1024 * 1024))

Generate 1G file filled with zeros

    dd if=/dev/zero of=/tmp/out.file bs=$((1024 * 1024)) count=1000
    dd if=/dev/zero of=/tmp/out.file bs=1M  count=1000
    dd if=/dev/zero of=/tmp/out.file bs=1GB  count=1
    dd if=/dev/zero of=/tmp/out.file bs=1000 count=$((1024 * 1024))

Generate 10M file filled with random data

    dd if=/dev/urandom of=/tmp/out.file bs=10M count=1

## Numbers

### Generate numbers and string with numbers

Generate numbers from 0 to 100

    for COUNTER in {1..100}; do echo $COUNTER ; done
    COUNTER=0; while [[ COUNTER -lt 100 ]]; do COUNTER=$((COUNTER+1)); echo $COUNTER; done

Generate numbers from 0 to 100 with leading zeros

    for COUNTER in {1..100}; do printf "%08d\n" $COUNTER ; done
    COUNTER=0; while [[ COUNTER -lt 100 ]]; do COUNTER=$((COUNTER+1)); printf "%08d\n" $COUNTER; done

Generate string with numbers from 0 to 100 with leading zeros

    VBASE=var_;for COUNTER in {1..100}; do printf "$VBASE%08d\n" $COUNTER ; done
    VBASE=var_;COUNTER=0; while [[ COUNTER -lt 100 ]]; do COUNTER=$((COUNTER+1)); printf "$VBASE%08d\n" $COUNTER; done

## Random string\number

Random 32 character string

    RND=$(cat /dev/urandom | tr -dc 'a-zA-Z0-9' | fold -w 32 | head -n 1)

Random number 1-9

    cat /dev/urandom | tr -dc '0-9' |  head -c1
    cat /dev/urandom | tr -dc '0-9' |  head -c1 | awk '1'
    cat /dev/urandom | tr -dc '0-9' |  head -c1 | awk '1'

Random number 0-99 & 0-999

    cat /dev/urandom | tr -dc '0-9' |  head -c2 | awk '1'
    cat /dev/urandom | tr -dc '0-9' |  head -c2 | xargs

    cat /dev/urandom | tr -dc '0-9' |  head -c3 | awk '1'
    cat /dev/urandom | tr -dc '0-9' |  head -c3 | xargs
    cat /dev/urandom | tr -dc '0-9' |  head -c3 | xargs printf '%d\n'
