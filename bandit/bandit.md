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

## Level 2 -> Level 3
```
cat "spaces in this filename"
aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG
```

## Level 3 -> Level 4
```
cd inhere
ls -al
cat .hidden
2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe
```

## Level 4 -> Level 5
```
cat ./-file07
lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR
```

## Level 5 -> Level 6
```
find . -size 1033c
cat ./maybehere07/.file2
P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU
```

## Level 6 -> Level 7

```
find / -size 33c -user bandit7 -group bandit6 2> /dev/null
/var/lib/dpkg/info/bandit7.password
z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S
```

## Level 7 -> Level 8

```
cat data.txt | grep millionth
millionth       TESKZC0XvTetK0S9xNwm25STk5iWrBvP
```

## Level 8 -> Level 9

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

```
echo "jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt" | openssl s_client -connect localhost:30001 -ign_eof
CONNECTED(00000003)
Can't use SSL_get_servername
depth=0 CN = localhost
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN = localhost
verify error:num=10:certificate has expired
notAfter=Jan 31 13:42:05 2023 GMT
verify return:1
depth=0 CN = localhost
notAfter=Jan 31 13:42:05 2023 GMT
verify return:1
---
Certificate chain
 0 s:CN = localhost
   i:CN = localhost
   a:PKEY: rsaEncryption, 2048 (bit); sigalg: RSA-SHA1
   v:NotBefore: Jan 31 13:41:05 2023 GMT; NotAfter: Jan 31 13:42:05 2023 GMT
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIDCzCCAfOgAwIBAgIESAg7VDANBgkqhkiG9w0BAQUFADAUMRIwEAYDVQQDDAls
b2NhbGhvc3QwHhcNMjMwMTMxMTM0MTA1WhcNMjMwMTMxMTM0MjA1WjAUMRIwEAYD
VQQDDAlsb2NhbGhvc3QwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCI
CecP1LF/9yPzwS7rtoS0sYClf1kilLM4pMiNVr3bkI+XGOLodX2ffzM/+5gEY73B
y3qpPAi2o/opNNlW+N5S9vqV5LNTqXfR3v2fNGDpZt1l/b36QpnTGAhVuBXCIplJ
yYURBpL4zM3hnm2El+QIqDJPOIC3mfOoE7zxqCMK/vmVt8WHQvV5pb1TmVD6th4y
vpqSl6giCMK0kPjtpqKuWVk2t0e7znyb6U8VTUn5ztwBb56DdPjqc0UX2QI7y/aU
fRnJVAWdk5vt9/msTBO0sBx9EFPTUdPLpYCb1c8g5SURbxJmdhHn7R11Vu3UByeL
4LBhKOHjLcaHUzuWi57bAgMBAAGjZTBjMBQGA1UdEQQNMAuCCWxvY2FsaG9zdDBL
BglghkgBhvhCAQ0EPhY8QXV0b21hdGljYWxseSBnZW5lcmF0ZWQgYnkgTmNhdC4g
U2VlIGh0dHBzOi8vbm1hcC5vcmcvbmNhdC8uMA0GCSqGSIb3DQEBBQUAA4IBAQB2
ghKgfkzfe5e8aDIItpcEXVTU59ErDfGCEh3wfKh8EnXF0f2AlF9Vup/2T43pQdxf
c08LZiXXiTX6HTLNoWq28SuIYMAUDbqEx5GKXPBcJn0oICKyLaDzkYq2U5EhxE/c
RDqZQEaXRWuMzmLzvnucQOV/fc1VCmhASbf8OcUrI3kHzjDHu8YR4r4A0eApxP3g
vPtfEHKWAB8EJuFQsSPTDZEBxA08aSA5X6hDkMZ8ZNx2r5Xu1rZR6or3LfLwMfxt
qxWfN/HC+XI3A8nDQPthEyk9yi2ka7TrUGdVpb3B00KywXyc5OyMiSQEK2gMl149
49Sznlo0ALChDrhGJz8E
-----END CERTIFICATE-----
subject=CN = localhost
issuer=CN = localhost
---
No client certificate CA names sent
Peer signing digest: SHA256
Peer signature type: RSA-PSS
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 1339 bytes and written 373 bytes
Verification error: certificate has expired
---
New, TLSv1.3, Cipher is TLS_AES_256_GCM_SHA384
Server public key is 2048 bit
Secure Renegotiation IS NOT supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
Early data was not sent
Verify return code: 10 (certificate has expired)
---
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: 8EB84B10A32A3076D75606A07BF2B38F249F46BF2445BBFFA743B50F1571CEBE
    Session-ID-ctx: 
    Resumption PSK: 3AE97D36ECC94B5E5E51D0868D021184DFBFF33C83F80204F755B9EA1978E366758ABBB662E86F1C8147AE590C92432B
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - 38 32 17 d8 c5 fd 76 a8-f0 70 4a 5e 91 98 9b 7c   82....v..pJ^...|
    0010 - 87 df 47 2f ea ec 62 44-a8 3b 07 c9 ae 16 56 d4   ..G/..bD.;....V.
    0020 - 00 33 e0 c7 c7 61 45 fb-b5 27 07 31 ce 5a 73 59   .3...aE..'.1.ZsY
    0030 - 78 90 01 52 74 7a a5 ec-d4 da fa a4 6b 88 7c 5b   x..Rtz......k.|[
    0040 - d3 1c cc 66 d2 6a fb c0-15 74 d2 62 a0 04 0d 10   ...f.j...t.b....
    0050 - 26 ca 06 4a 1c 2c 30 2a-57 d1 8e ae fb 44 4e e8   &..J.,0*W....DN.
    0060 - ff b6 d0 41 dc 0e 5b eb-67 c4 f4 83 88 00 a9 08   ...A..[.g.......
    0070 - 4f 51 51 73 b2 43 0f 91-bd ef 16 a8 c3 fe 41 69   OQQs.C........Ai
    0080 - f1 a2 14 ac d5 4c ce bf-d4 f9 7a f6 18 a1 e8 22   .....L....z...."
    0090 - 1f f2 b0 d9 6b 31 3e 6d-47 58 3e ea d2 d0 7d 9a   ....k1>mGX>...}.
    00a0 - f4 bf 15 f7 55 be 37 61-01 97 b3 00 68 e0 1b 57   ....U.7a....h..W
    00b0 - 44 c7 19 0d 4f 32 55 68-70 e5 e2 2c 93 3f 57 60   D...O2Uhp..,.?W`
    00c0 - a9 84 6c cb 2a d1 01 e1-46 06 34 58 a6 ec ea 06   ..l.*...F.4X....

    Start Time: 1675422373
    Timeout   : 7200 (sec)
    Verify return code: 10 (certificate has expired)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: E053E358023DF456179B29C12665E224D81867604C6C9A0A3B7851C6A44C3E19
    Session-ID-ctx: 
    Resumption PSK: 9C90A31A085213FA05CBD3125CC447B380D5D5BA28273B1993DFBDD26651C6706F9FE8F3BD6BE79D8DF747674FFA18DD
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - 38 32 17 d8 c5 fd 76 a8-f0 70 4a 5e 91 98 9b 7c   82....v..pJ^...|
    0010 - cc 5d f9 6d 8a 60 73 00-56 4d 5d 0a f5 8f fd 60   .].m.`s.VM]....`
    0020 - 3c 78 e5 35 b6 28 42 ad-c1 e7 e5 01 58 44 5a 1c   <x.5.(B.....XDZ.
    0030 - 6a be af 27 e1 6e 54 40-b9 f7 2e 9f 57 2f ce a5   j..'.nT@....W/..
    0040 - d4 04 cf 23 1a 27 96 a9-0e 83 d6 29 57 06 9a 48   ...#.'.....)W..H
    0050 - e9 03 42 d4 a7 cc b8 da-4a f5 6c 20 10 e2 51 bb   ..B.....J.l ..Q.
    0060 - 18 10 4f 08 6e 5b ac fa-78 03 c8 31 56 e0 bf b8   ..O.n[..x..1V...
    0070 - 9e 97 61 09 11 35 3a f3-9a e7 3e f1 53 12 b6 a5   ..a..5:...>.S...
    0080 - ca 57 a0 6d f7 b4 63 fa-97 99 55 41 66 95 72 70   .W.m..c...UAf.rp
    0090 - df cd c3 83 ff c9 12 45-e2 58 6b 0e a5 85 03 86   .......E.Xk.....
    00a0 - 4e 34 c3 de ab 51 a0 72-05 6b f5 b6 60 53 25 6c   N4...Q.r.k..`S%l
    00b0 - f8 c0 0d 25 96 04 2f 44-ac 64 5c fc ee 01 ba a9   ...%../D.d\.....
    00c0 - 58 44 19 46 3a f3 8d 43-08 96 81 82 ab 5f 7a 05   XD.F:..C....._z.

    Start Time: 1675422373
    Timeout   : 7200 (sec)
    Verify return code: 10 (certificate has expired)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
Correct!
JQttfApK4SeyHwDlI9SXGR50qclOAil1

closed
```

## Level 16 -> Level 17

nmap to see open ports
```
nmap localhost -p 31000-32000
Starting Nmap 7.80 ( https://nmap.org ) at 2023-02-03 11:09 UTC
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00016s latency).
Not shown: 996 closed ports
PORT      STATE SERVICE
31046/tcp open  unknown
31518/tcp open  unknown
31691/tcp open  unknown
31790/tcp open  unknown
31960/tcp open  unknown
```

Perform service scan
```
nmap localhost -sV -T4 -p 31000-32000
Starting Nmap 7.80 ( https://nmap.org ) at 2023-02-03 11:19 UTC
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00018s latency).
Not shown: 996 closed ports
PORT      STATE SERVICE     VERSION
31046/tcp open  echo
31518/tcp open  ssl/echo
31691/tcp open  echo
31790/tcp open  ssl/unknown
31960/tcp open  echo
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port31790-TCP:V=7.80%T=SSL%I=7%D=2/3%Time=63DCEDEA%P=x86_64-pc-linux-gn
SF:u%r(GenericLines,31,"Wrong!\x20Please\x20enter\x20the\x20correct\x20cur
SF:rent\x20password\n")%r(GetRequest,31,"Wrong!\x20Please\x20enter\x20the\
SF:x20correct\x20current\x20password\n")%r(HTTPOptions,31,"Wrong!\x20Pleas
SF:e\x20enter\x20the\x20correct\x20current\x20password\n")%r(RTSPRequest,3
SF:1,"Wrong!\x20Please\x20enter\x20the\x20correct\x20current\x20password\n
SF:")%r(Help,31,"Wrong!\x20Please\x20enter\x20the\x20correct\x20current\x2
SF:0password\n")%r(SSLSessionReq,31,"Wrong!\x20Please\x20enter\x20the\x20c
SF:orrect\x20current\x20password\n")%r(TerminalServerCookie,31,"Wrong!\x20
SF:Please\x20enter\x20the\x20correct\x20current\x20password\n")%r(TLSSessi
SF:onReq,31,"Wrong!\x20Please\x20enter\x20the\x20correct\x20current\x20pas
SF:sword\n")%r(Kerberos,31,"Wrong!\x20Please\x20enter\x20the\x20correct\x2
SF:0current\x20password\n")%r(FourOhFourRequest,31,"Wrong!\x20Please\x20en
SF:ter\x20the\x20correct\x20current\x20password\n")%r(LPDString,31,"Wrong!
SF:\x20Please\x20enter\x20the\x20correct\x20current\x20password\n")%r(LDAP
SF:SearchReq,31,"Wrong!\x20Please\x20enter\x20the\x20correct\x20current\x2
SF:0password\n")%r(SIPOptions,31,"Wrong!\x20Please\x20enter\x20the\x20corr
SF:ect\x20current\x20password\n");
```

Submit to port 31790

```
echo "JQttfApK4SeyHwDlI9SXGR50qclOAil1" | openssl s_client -connect localhost:31790 -ign_eof
CONNECTED(00000003)
Can't use SSL_get_servername
depth=0 CN = localhost
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN = localhost
verify error:num=10:certificate has expired
notAfter=Jan 31 13:42:06 2023 GMT
verify return:1
depth=0 CN = localhost
notAfter=Jan 31 13:42:06 2023 GMT
verify return:1
---
Certificate chain
 0 s:CN = localhost
   i:CN = localhost
   a:PKEY: rsaEncryption, 2048 (bit); sigalg: RSA-SHA1
   v:NotBefore: Jan 31 13:41:06 2023 GMT; NotAfter: Jan 31 13:42:06 2023 GMT
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIDCzCCAfOgAwIBAgIECZg5njANBgkqhkiG9w0BAQUFADAUMRIwEAYDVQQDDAls
b2NhbGhvc3QwHhcNMjMwMTMxMTM0MTA2WhcNMjMwMTMxMTM0MjA2WjAUMRIwEAYD
VQQDDAlsb2NhbGhvc3QwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQDl
dqySPOYpOyBRUHCEI0IFlCi65pWd6ct09YsqpsnzdTiu4/oOTYp9SLei/W2R6Fih
omS7Tmeg6oXXWKbVkOBi2v1r1Ox3rvFrc37/KBbnoEcyRGe91LmEcfJzzCArkc8w
ZpUKT1mBXlfm4G7codA6JmkvKwWqGHI9pg0c2g/Ev8DcxtjsJnzMlFHgvkEB2F2M
Ef8foe/2qLxi1qQI79JX6qgDtQzhZ6YTh8lwbSZ5F/qMa+KkHhD67/mA01uTZ4aA
YtnF8RNNgJkJzXb79zquVXtrCdJztbonzaiBdrEFSif4jSFtpbTGFBrrlA91WsIG
VnDpaVfe+ZgTELZv2T5FAgMBAAGjZTBjMBQGA1UdEQQNMAuCCWxvY2FsaG9zdDBL
BglghkgBhvhCAQ0EPhY8QXV0b21hdGljYWxseSBnZW5lcmF0ZWQgYnkgTmNhdC4g
U2VlIGh0dHBzOi8vbm1hcC5vcmcvbmNhdC8uMA0GCSqGSIb3DQEBBQUAA4IBAQDU
11ALcrYhW/2qHf08eoNde7Nao6zWPCBftNnk0gBr1fuuXOdzchIp/2VcwrG1auvy
eCgbcuD0Uf7iKqokpcQWizS8YppATjDwv/Ggr1tVFCayrJ/6khRHbKEcTvVcKxWr
Ma1d6diH5Faj4u8fjik9WdmeVyPqFqQSdeva6WfmOWeYdQqX3hSg3zUkiu7GR2WT
cBLJGWfFaCQWIvryMcmIqxc+ccB7kBiH1WytVrEWS6m/IP7yOYJ7PjPjqOYiXPTu
6TlteGIiVdCRrRqs5Zd0g8SOmO7pVV3t0VnssasaBBILthNH12SzL3rdExQHGGmm
5RYwctKS55+339FM5FOj
-----END CERTIFICATE-----
subject=CN = localhost
issuer=CN = localhost
---
No client certificate CA names sent
Peer signing digest: SHA256
Peer signature type: RSA-PSS
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 1339 bytes and written 373 bytes
Verification error: certificate has expired
---
New, TLSv1.3, Cipher is TLS_AES_256_GCM_SHA384
Server public key is 2048 bit
Secure Renegotiation IS NOT supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
Early data was not sent
Verify return code: 10 (certificate has expired)
---
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: 42B17BD5517B02969813DDE7D06A4A1FF8CCD59C62F599A30DE675DB928DF2BA
    Session-ID-ctx: 
    Resumption PSK: 88893333C72941D9E56621A553D494F6BBA782409C1F83C99C11DB08861A223DEC7862F7BD614F52CB672FD911522DC0
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - 2f e1 8f 70 11 b2 44 50-70 ad 4d c9 b0 44 bf a7   /..p..DPp.M..D..
    0010 - 7d 6b ce cf 8e de 0a c9-16 61 94 ca 0a aa fe 41   }k.......a.....A
    0020 - a5 f8 5a 67 fb bf 18 7b-cf b2 e4 79 99 a4 3f 5c   ..Zg...{...y..?\
    0030 - 87 82 59 1b 6f ac ed 2d-38 d5 76 50 e4 5f 5d e1   ..Y.o..-8.vP._].
    0040 - c3 44 12 fc 94 9c ed 65-a3 be 8e 70 b0 3c 07 2b   .D.....e...p.<.+
    0050 - 8a a8 2b 16 c2 a0 11 ff-dc 40 15 0a e1 1f 1f c6   ..+......@......
    0060 - 7d 1f 47 16 35 b3 4a 95-f9 ed fd 03 d5 22 e8 c0   }.G.5.J......"..
    0070 - 81 0e 03 67 6a fb 7a 73-08 95 10 8e 1f 54 60 5e   ...gj.zs.....T`^
    0080 - 83 76 b0 82 6f d6 af a4-2c ac 55 b0 40 be 55 ac   .v..o...,.U.@.U.
    0090 - 1b 17 00 f2 de 0a 47 25-e5 5c 61 db 43 1a 09 7c   ......G%.\a.C..|
    00a0 - 46 b3 83 d3 f3 1b 3b 06-38 04 04 bf 25 1e 16 f9   F.....;.8...%...
    00b0 - 07 eb da d1 1e d8 b5 14-80 e8 29 21 1b 92 32 44   ..........)!..2D
    00c0 - b5 4c d0 68 8d 85 ad 28-67 ae d5 5b b6 d4 25 50   .L.h...(g..[..%P

    Start Time: 1675423480
    Timeout   : 7200 (sec)
    Verify return code: 10 (certificate has expired)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: 9B7ACC0902CD743B473DCDEDC6432E0573C80FAE6F328C1E9E67B9A3039A76B3
    Session-ID-ctx: 
    Resumption PSK: 8010F47A398EABBB8AFB2EBFD04B2682B5C99EA786BB5CDF85AE518E6BAB584CA4CE7DB616E37FDD41B365D94AD16562
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - 2f e1 8f 70 11 b2 44 50-70 ad 4d c9 b0 44 bf a7   /..p..DPp.M..D..
    0010 - ab c2 a4 9c a7 aa 47 b3-d8 3d 95 01 9c 40 51 6d   ......G..=...@Qm
    0020 - df 71 3a 07 19 b9 87 2c-ce cd b3 1a 2a 54 90 8b   .q:....,....*T..
    0030 - ad 39 6f a2 f6 63 09 4f-7c 6c a0 39 9a 6d b5 4a   .9o..c.O|l.9.m.J
    0040 - 1b 96 f8 84 28 7f ff c1-f0 21 d9 f7 10 59 60 11   ....(....!...Y`.
    0050 - e2 f5 cf e7 c0 5c c0 a3-8b 0e 5e bc 6b f6 b8 a7   .....\....^.k...
    0060 - cc 75 07 b1 c5 e7 f4 5d-00 ae d2 54 76 0e 19 a7   .u.....]...Tv...
    0070 - aa ed c1 29 d4 76 b9 8e-17 0a 11 eb f2 9b 56 2a   ...).v........V*
    0080 - dd b6 d9 ae 49 d8 9e 7b-bb 92 1e 7a c6 96 ca 68   ....I..{...z...h
    0090 - 3d ca 10 ff 3f 89 b5 e7-c6 be 3b 47 a5 cb 61 19   =...?.....;G..a.
    00a0 - de cb 04 8d bd 18 c9 93-a4 be 74 5b a8 31 f8 db   ..........t[.1..
    00b0 - 9d 08 98 3c af 40 7b 6c-69 86 87 50 0a a2 d6 0c   ...<.@{li..P....
    00c0 - 5d 19 99 8f 92 c1 e6 4f-39 c7 84 3c c4 75 db cc   ]......O9..<.u..

    Start Time: 1675423480
    Timeout   : 7200 (sec)
    Verify return code: 10 (certificate has expired)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
Correct!
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----

closed
```

Copy the key part in `/tmp/bandit16` save it as private_key or whatever

```
chmod 600 private_key
```

Finally,
```
ssh -i private_key bandit17@bandit.labs.overthewire.org -p 2220
```


## Level 17 -> Level 18

We can use 
```
diff passwords.new passwords.old
hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg
```

if diff is difficult to see then we can add `-y` to make it easier to read.

## Level 18 -> Level 19

Bash is broken?

```
ssh bandit18@bandit.labs.overthewire.org -p 2220 "/bin/sh"
awhqfNnAbc1naukrpqDYcF95h7HoMTrC
```

![[Pasted image 20230203204331.png]]


## Level 19 -> Level 20

```
./bandit20-do
Run a command as another user.
  Example: ./bandit20-do id

./bandit20-do id
uid=11019(bandit19) gid=11019(bandit19) euid=11020(bandit20) groups=11019(bandit19)
```

Meaning even though the user id is 11019(bandit19) we can run bandit20-do as `euid=11020` bandit20.
The document tells me that the password is under `/etc/bandit_pass`, so we can grab the password as bandit20 with the binary file.

```
./bandit20-do cat /etc/bandit_pass/bandit20
VxCazJaVykI6W36BkBU0mJTCM8rR95XT
```

## Level 20 -> Level 21

Have netcat in background process
```
echo "VxCazJaVykI6W36BkBU0mJTCM8rR95XT" | netcat -lp 4444 &
```
Connect using the binary
```
./suconnect 4444
Read: VxCazJaVykI6W36BkBU0mJTCM8rR95XT
Password matches, sending next password
NvEJF7oVjkddltPSrdKEFOllh9V1IBcq
```


## Level 21 -> Level 22

```
cat /etc/cron.d/cronjob_bandit22
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```

runs /usr/bin/cronjob_bandit22.sh periodically

```
cat /usr/bin/cronjob_bandit22.sh
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

```
cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
WdDozAdTM2z9DiFEQ2mGlwngMfj4EZff
```

## Level 22 -> Level 23

```
cat /etc/cron.d/cronjob_bandit23
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
```

```
cat /usr/bin/cronjob_bandit23.sh
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```

run the script
```
/usr/bin/cronjob_bandit23.sh
Copying passwordfile /etc/bandit_pass/bandit22 to /tmp/8169b67bd894ddbb4412f91573b38db3
```

Password for bandit22 
```
cat /tmp/8169b67bd894ddbb4412f91573b38db3
WdDozAdTM2z9DiFEQ2mGlwngMfj4EZff
```

Get the directory for bandit23 using the code
Since we are the user bandit22, if we run the shell code, then we get the result for bandit22. Notice that we can manually put bandit23 in echo and obtain what we want.

```
echo I am user bandit23 | md5sum | cut -d ' ' -f 1
8ca319486bfbbc3663ea0fbe81326349
```

Password for bandit23
```
cat /tmp/8ca319486bfbbc3663ea0fbe81326349
QYw0Y2aiA672PsMmh9puTQuhoz8SyR2G
```

## Level 23 -> Level 24

```
cat /etc/cron.d/cronjob_bandit24
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
```

Cron job will run this script as bandit24, so we need to create a script that copies password into a specific folder.
```
cat /usr/bin/cronjob_bandit24.sh
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname/foo
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" ./$i)"
        if [ "${owner}" = "bandit23" ]; then
            timeout -s 9 60 ./$i
        fi
        rm -f ./$i
    fi
done
```

create `getpass.sh` in `/tmp/bandit23`
```getpass.sh
#!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/bandit23/password
```
`chmod 777 getpass.sh` to allow other users to run the file

Also create a file called `password`
run the file as bandit24 through cron and write it in the password file
`chmod 666 password` to allow other users to write

The structure would be
/tmp/bandit23
	- getpass.sh with 666 permission
	- password with 777 permission

copy the shell file into the specific directory
```
cp getpass.sh /var/spool/bandit24/foo
```
The shell script will be executed and then it will get deleted

Wait for a minute for the cron job to process the file
```
ls -al
total 10084
drwxrwxrwx    2 bandit23 bandit23     4096 Feb  3 14:37 .
drwxrwx-wt 2731 root     root     10276864 Feb  3 14:44 ..
-rwxrwxrwx    1 bandit23 bandit23       68 Feb  3 14:36 getpass.sh
-rw-rw-rw-    1 bandit23 bandit23       33 Feb  3 14:44 password
```

Finally,
```
cat password
VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar
```