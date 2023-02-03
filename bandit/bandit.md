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

```
cat sshkey.private
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEAxkkOE83W2cOT7IWhFc9aPaaQmQDdgzuXCv+ppZHa++buSkN+
gg0tcr7Fw8NLGa5+Uzec2rEg0WmeevB13AIoYp0MZyETq46t+jk9puNwZwIt9XgB
ZufGtZEwWbFWw/vVLNwOXBe4UWStGRWzgPpEeSv5Tb1VjLZIBdGphTIK22Amz6Zb
ThMsiMnyJafEwJ/T8PQO3myS91vUHEuoOMAzoUID4kN0MEZ3+XahyK0HJVq68KsV
ObefXG1vvA3GAJ29kxJaqvRfgYnqZryWN7w3CHjNU4c/2Jkp+n8L0SnxaNA+WYA7
jiPyTF0is8uzMlYQ4l1Lzh/8/MpvhCQF8r22dwIDAQABAoIBAQC6dWBjhyEOzjeA
J3j/RWmap9M5zfJ/wb2bfidNpwbB8rsJ4sZIDZQ7XuIh4LfygoAQSS+bBw3RXvzE
pvJt3SmU8hIDuLsCjL1VnBY5pY7Bju8g8aR/3FyjyNAqx/TLfzlLYfOu7i9Jet67
xAh0tONG/u8FB5I3LAI2Vp6OviwvdWeC4nOxCthldpuPKNLA8rmMMVRTKQ+7T2VS
nXmwYckKUcUgzoVSpiNZaS0zUDypdpy2+tRH3MQa5kqN1YKjvF8RC47woOYCktsD
o3FFpGNFec9Taa3Msy+DfQQhHKZFKIL3bJDONtmrVvtYK40/yeU4aZ/HA2DQzwhe
ol1AfiEhAoGBAOnVjosBkm7sblK+n4IEwPxs8sOmhPnTDUy5WGrpSCrXOmsVIBUf
laL3ZGLx3xCIwtCnEucB9DvN2HZkupc/h6hTKUYLqXuyLD8njTrbRhLgbC9QrKrS
M1F2fSTxVqPtZDlDMwjNR04xHA/fKh8bXXyTMqOHNJTHHNhbh3McdURjAoGBANkU
1hqfnw7+aXncJ9bjysr1ZWbqOE5Nd8AFgfwaKuGTTVX2NsUQnCMWdOp+wFak40JH
PKWkJNdBG+ex0H9JNQsTK3X5PBMAS8AfX0GrKeuwKWA6erytVTqjOfLYcdp5+z9s
8DtVCxDuVsM+i4X8UqIGOlvGbtKEVokHPFXP1q/dAoGAcHg5YX7WEehCgCYTzpO+
xysX8ScM2qS6xuZ3MqUWAxUWkh7NGZvhe0sGy9iOdANzwKw7mUUFViaCMR/t54W1
GC83sOs3D7n5Mj8x3NdO8xFit7dT9a245TvaoYQ7KgmqpSg/ScKCw4c3eiLava+J
3btnJeSIU+8ZXq9XjPRpKwUCgYA7z6LiOQKxNeXH3qHXcnHok855maUj5fJNpPbY
iDkyZ8ySF8GlcFsky8Yw6fWCqfG3zDrohJ5l9JmEsBh7SadkwsZhvecQcS9t4vby
9/8X4jS0P8ibfcKS4nBP+dT81kkkg5Z5MohXBORA7VWx+ACohcDEkprsQ+w32xeD
qT1EvQKBgQDKm8ws2ByvSUVs9GjTilCajFqLJ0eVYzRPaY6f++Gv/UVfAPV4c+S0
kAWpXbv5tbkkzbS0eaLPTKgLzavXtQoTtKwrjpolHKIHUz6Wu+n4abfAIRFubOdN
/+aLoRQ0yBDRbdXMsZN/jvY44eM+xRLdRVyMmdPtP8belRi2E2aEzA==
-----END RSA PRIVATE KEY-----
```

```
ssh -i sshkey.private bandit14@localhost -p 2220
```

use localhost to move from bandit13 to bandit14
```
cat /etc/bandit_pass/bandit14
fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq
```


## Level 14 -> Level 15
Submit the password through netcat

```
echo "fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq" | nc localhost 30000
Correct!
jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt
```

## Level 15 -> Level 16
