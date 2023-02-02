## Level 0

```
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

## Level 0 -> Level 1
```
cat readme
NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL
```

##  Level 1 -> Level 2
```
cat -
```
does not work since cat with - is considered as stdin

```
cat ./-
rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi
```

## Level 3
```
cat "spaces in this filename"
aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG
```

## Level 4
```
cd inhere
ls -al
cat .hidden
2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe
```

## Level 5
```
cat ./-file07
lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR
```

## Level 6
```
find . -size 1033c
cat ./maybehere07/.file2
P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU
```

## Level 7

```
find / -size 33c -user bandit7 -group bandit6 2> /dev/null
/var/lib/dpkg/info/bandit7.password
z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S
```

## Level 8

```
cat data.txt | grep millionth
millionth       TESKZC0XvTetK0S9xNwm25STk5iWrBvP
```

## Level 9

It does not work without sort.

```
cat data.txt | sort | uniq -u
EN632PlfYiZbn3PhVK3XOGSlNInNE00t
```

##  Level 9 -> Level 10

```
strings data.txt | grep ==
c========== the
h;========== password
========== isT
n.E========== G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s
```

## Level 10 -> Level 11

```
base64 -d data.txt
The password is 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM
```

## Level 11 -> Level 12

```
cat data.txt | tr '[a-z]' '[n-za-m]' | tr '[A-Z]' '[N-ZA-M]'
The password is JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv
```

## Level 12 -> Level 13

Create a new directory since the user does not have a permission to create/write file in the current directory.
```
mkdir /tmp/tofu
```
Copy
```
cp data.txt /tmp/tofu/data.txt
```

Check file type
```
file data.txt
data.txt: ASCII text
```

Cat data.txt gives hexdump
![[Pasted image 20230202171251.png]]


```
xxd -r /tmp/tofu/data.txt > /tmp/tofu/data2
```
or 
move to /tmp/tofu folder and 
```
xxd -r data.txt > data2
```

```
file data2
data2: bzip2 compressed data, block size = 900k
```

```
bzip2 -dc data2 > data3
```

```
file data3
data3: gzip compressed data, was "data4.bin", last modified: Wed Jan 11 19:18:38 2023, max compression, from Unix, original size modulo 2^32 20480
```

```
gzip -dc data3 > data4
```

```
file data4
data4: POSIX tar archive (GNU)
```

The command below produces data5.bin
```
tar -xvf data4
```

```
file data5.bin
data5.bin: POSIX tar archive (GNU)
```

```
tar -xvf data5.bin
```

```
file data6.bin
data6.bin: bzip2 compressed data, block size = 900k
```

```
bzip2 -dc data6.bin > data7
```

```
file data8.bin
data8.bin: gzip compressed data, was "data9.bin", last modified: Wed Jan 11 19:18:38 2023, max compression, from Unix, original size modulo 2^32 49
```

```
gzip -dc data8.bin > data9
```

Finally!
```
cat data9
The password is wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw
```

## Level 13 -> Level 14
