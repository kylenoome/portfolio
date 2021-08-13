Write-up
Overview#

Install tools used in this WU on BlackArch Linux:

```python
$ sudo pacman -S haiti john
```
Finding your way around linux - overview#

    What is the correct option for finding files based on group

Answer: -group

Read course material.

    What is format for finding a file with the user named Francis and with a size of 52 kilobytes in the directory /home/francis/

Answer: find /home/francis/ -type f -user Francis -size 52k

Read course material.

    SSH as topson using his password topson. Go to the /home/topson/chatlogs directory and type the following: grep -iRl 'keyword'. What is the name of the file that you found using this command?

Answer: 2019-10-11

Just enter the given command.

    What are the characters subsequent to the word you found?

Answer: ttitor

```python
topson@james:~/chatlogs$ grep keyword 2019-10-11
commodo porkeywordedited ut enim. vitae, ac, aliquet elementum felis eleifend justo,
```
    Read the file named 'ReadMeIfStuck.txt'. What is the Flag?

Answer: Flag{81726350827fe53g}

Follow the hint to find the 1st flag.

```python
topson@james:~$ cat ReadMeIfStuck.txt
Looking for flag 1?:It seems you will have to think harder if you want to find the flag. Perhaps try looking for a file called additionalHINT if you can't find it..
Looking for flag 2?: look for a file named readME_hint.txt

topson@james:~$ find . -name additionalHINT -type f
./channels/additionalHINT

topson@james:~$ cat ./channels/additionalHINT
try to find a directory called telephone numbers... Oh wait.. it  contains a space.. I wonder how we can find that....

topson@james:~$ find . -name 'telephone numbers' -type d
./corperateFiles/xch/telephone numbers

topson@james:~$ ls -lhA './corperateFiles/xch/telephone numbers'
total 4.0K
-rw-r--r-- 1 topson topson 189 Oct  5 15:26 readME.txt

topson@james:~$ cat './corperateFiles/xch/telephone numbers/readME.txt'
202-555-0150
202-555-0125
617-555-0115
+1-617-555-0115
+1-617-555-0186
+1-617-555-0138
use the Find command to find a file with a modified date of 2016-09-12 from the /workflows directory

topson@james:~$ find workflows/ -type f -newermt 2016-09-11 ! -newermt 2016-09-13
workflows/xft/eBQRhHvx

grep -oi '\S*flag\S*' workflows/xft/eBQRhHvx
volFlag{edited}uptate

    -o to display only matching content
    -i to make case insensitive search
    \S is a regexp token to match any non-whitespace character
```

Working with files#

    Hypothetically, you find yourself in a directory with many files and want to move all these files to the directory of /home/francis/logs. What is the correct command to do this?

Answer: mv * /home/francis/logs

Read course material.

    Hypothetically, you want to transfer a file from your /home/james/Desktop/ with the name script.py to the remote machine (192.168.10.5) directory of /home/john/scripts using the username of john. What would be the full command to do this?

Answer: scp /home/james/Desktop/script.py john@192.168.10.5:/home/john/scripts

Read course material.

    How would you rename a folder named -logs to -newlogs

Answer: mv -- -logs -newlogs

Read course material for filenames containing a dash.

    How would you copy the file named encryption keys to the directory of /home/john/logs

Answer: mv encryption keys /home/john/logs

Use quote for filename containing a space.

    Find a file named readME_hint.txt inside topson's directory and read it. Using the instructions it gives you, get the second flag.

Answer: Flag{234@i4s87u5hbn$3}

```python
topson@james:~$ find . -name readME_hint.txt -type f
./corperateFiles/RecordsFinances/readME_hint.txt

topson@james:~$ cat ./corperateFiles/RecordsFinances/readME_hint.txt
Instructions: Move the MoveMe.txt file to the march folder directory and then execute the SH program to reveal the second flag.

 you need to research three things:
                                 how to execute bash files
                                 how to work with files that begin with a - (dash) whether that is to do with copying or moving files
                                 how to work with files with spaces

topson@james:~$ ls -lhA ./corperateFiles/RecordsFinances/
total 344K
-rw-r--r-- 1 topson topson  17K Oct  5 15:26  ajkJji
-rw-r--r-- 1 topson topson  17K Oct  5 15:26  CeCJDJ
-rw-r--r-- 1 topson topson  43K Oct  5 15:26  GxPtUIo
-rw-r--r-- 1 topson topson  17K Oct  5 15:26  hHYDeM
drwxrwxr-x 2 topson topson 4.0K Oct  5 15:26  january
drwxrwxr-x 2 topson topson 4.0K Oct  5 15:26 '-march folder'
-rw-r--r-- 1 topson topson 183K Oct  5 15:26  -MoveMe.txt
-rw-r--r-- 1 topson topson  379 Oct  5 15:26  readME_hint.txt
-rw-r--r-- 1 topson topson  43K Oct  5 15:26  uIkmHPN

topson@james:~$ cd ./corperateFiles/RecordsFinances/

topson@james:~/corperateFiles/RecordsFinances$ mv -- -MoveMe.txt '-march folder'

topson@james:~/corperateFiles/RecordsFinances$ cd -- '-march folder'

topson@james:~/corperateFiles/RecordsFinances/-march folder$ bash -- -runME.sh
-MoveMe.txt exists.
Flag{edited}
```

Hashing - introduction#

    Download the hash file attached to this task and attempt to crack the MD5 hash. What is the password?

Answer: secret123

```python
$ cat hash1.txt
5d7845ac6ee7cfffafc5fe5f35cf666d
```

Using CrackStation to crack the hash.

    SSH as sarah using: sarah@[MACHINE:IP] and use the password: rainbowtree1230x

    What is the hash type stored in the file hashA.txt

Answer: md4

Let's find the file first.

```python
sarah@james:~$ find -name hashA.txt -type f
./system AB/server_mail/server settings/hashA.txt
```

Now let's see the hash:

```python
sarah@james:~$ cat './system AB/server_mail/server settings/hashA.txt'
f9d4049dd6a4dc35d40e5265954b2a46
```

And now trying to identify it with haiti:

```python
$ haiti f9d4049dd6a4dc35d40e5265954b2a46
MD2 [JtR: md2]
MD5 [HC: 0] [JtR: raw-md5]
MD4 [HC: 900] [JtR: raw-md4]
Double MD5 [HC: 2600]
LM [HC: 3000] [JtR: lm]
RIPEMD-128 [JtR: ripemd-128]
Haval-128 [JtR: haval-128-4]
Tiger-128
Skein-256(128)
Skein-512(128)
Lotus Notes/Domino 5 [HC: 8600] [JtR: lotus5]
Skype [HC: 23]
Snefru-128 [JtR: snefru-128]
NTLM [HC: 1000] [JtR: nt]
Domain Cached Credentials [HC: 1100] [JtR: mscach]
Domain Cached Credentials 2 [HC: 2100] [JtR: mscach2]
DNSSEC(NSEC3) [HC: 8300]
RAdmin v2.x [HC: 9900] [JtR: radmin
```

The most probable is MD5 but it's not this one.

    Crack hashA.txt using john the ripper, what is the password?

Answer: admin

What nice is that haiti gave us the JtR reference.

```python
$ printf %s 'f9d4049dd6a4dc35d40e5265954b2a46' > hash.txt

$ john hash.txt --wordlist=/usr/share/wordlists/passwords/rockyou.txt --format=raw-md4
```

    What is the hash type stored in the file hashB.txt

Answer: SHA-1

Let's find it first and then display it:

```python
sarah@james:~$ find -name hashB.txt -type f
./oldLogs/settings/craft/hashB.txt

sarah@james:~$ cat ./oldLogs/settings/craft/hashB.txt && echo
b7a875fc1ea228b9061041b7cec4bd3c52ab3ce3
```

We'll use haiti again to identify the hash type:

```python
$ haiti b7a875fc1ea228b9061041b7cec4bd3c52ab3ce3
SHA-1 [HC: 100] [JtR: raw-sha1]
Double SHA-1 [HC: 4500]
RIPEMD-160 [HC: 6000] [JtR: ripemd-160]
Haval-160
Tiger-160
HAS-160
LinkedIn [HC: 190] [JtR: raw-sha1-linkedin]
Skein-256(160)
Skein-512(160)
```
The most probable is sha1.

    Find a wordlist with the file extention of '.mnf' and use it to crack the hash with the filename hashC.txt. What is the password?

Answer: unacvaolipatnuggi

Find the wordlist:

```python
sarah@james:~$ find -name *.mnf -type f
./system AB/db/ww.mnf
```
Download it:

```python
$ scp sarah@10.10.245.225:'~/system\ AB/db/ww.mnf' .
```
Find the hash file:

```python
sarah@james:~$ find -name hashC.txt -type f
./system AB/server_mail/hashC.txt

sarah@james:~$ cat './system AB/server_mail/hashC.txt'
c05e35377b5a31f428ccda9724a9dfbd0c5d71dccac691228d803c78e2e8da29
```

Identify hash type with haiti:

```python
$ haiti c05e35377b5a31f428ccda9724a9dfbd0c5d71dccac691228d803c78e2e8da29
Snefru-256 [JtR: snefru-256]
SHA-256 [HC: 1400] [JtR: raw-sha256]
RIPEMD-256
Haval-256 [JtR: haval-256-3]
GOST R 34.11-94 [HC: 6900] [JtR: gost]
GOST CryptoPro S-Box
SHA3-256 [HC: 17400]
Keccak-256 [HC: 17800] [JtR: raw-keccak-256]
Skein-256 [JtR: skein-256]
Skein-512(256)
```
It's most probably SHA-256.

Let's crack it now with the custom wordlist:

```python
$ printf %s 'c05e35377b5a31f428ccda9724a9dfbd0c5d71dccac691228d803c78e2e8da29' > hash.txt

$ john hash.txt --wordlist=ww.mnf --format=raw-sha256
```
    Crack hashB.txt using john the ripper, what is the password?

Answer: letmein

```python
$ printf %s 'b7a875fc1ea228b9061041b7cec4bd3c52ab3ce3' > hash.txt

$ john hash.txt --wordlist=/usr/share/wordlists/passwords/rockyou.txt --format=raw-sha1
```

Decoding base64#

    what is the name of the tool which allows us to decode base64 strings?

Answer: base64

Read course material.

    find a file called encoded.txt. What is the special answer?

Answer: john

Find the file:

```python
$ sarah@james:~$ find /home/sarah -type f -name encoded.txt 2>/dev/null
/home/sarah/system AB/managed/encoded.txt
```
Decode the file and look for the spacial word:

```python
sarah@james:~$ base64 -d '/home/sarah/system AB/managed/encoded.txt' | grep --color special
you know how to decode base64 data, well done. you deserve the answer but because this is the linux strength training room where you are intended to build your linux memory and skills, you will have to find it in this very long text file. Look for the keyword: 'special' in this very large text file.
Nullam nibh diam, gravida vestibulum mi sed, consectetur tincidunt nunc. Morbi pharetra turpis nec ligula pellentesque lobortis. Aenean sit amet ullamcorper turpis. Nam id magna sed felis facilisis accumsan. Aliquam cursus dolor eu enim maximus, eu malesuada sapien dignissim. Suspendisse ultrices condimentum nisi et pellentesque. Fusce ornare aliquet quam, eu efficitur elit facilisis et. Donec special: the answer is in a file called ent.txt, find it sagittis dolor nulla, interdum auctor tortor accumsan et. Aliquam vitae egestas dui, ut condimentum magna. Vestibulum tellus lacus, sollicitudin vitae dui sed, bibendum fermentum lacus. Mauris diam leo, efficitur at mi iaculis, sagittis hendrerit justo. Vivamus ante odio, cursus id tristique vitae, dapibus id eros. Quisque vitae mauris massa. Phasellus ut lectus efficitur, vulputate leo et, facilisis metus. Nulla volutpat nulla sem, vel vestibulum libero ultricies eu. Nam pulvinar tincidunt metus et accumsan.
```
Now we need to find ent.txt:

```python
sarah@james:~$ find /home/sarah -type f -name ent.txt 2>/dev/null
/home/sarah/logs/zhc/ent.txt

sarah@james:~$ cat /home/sarah/logs/zhc/ent.txt
bfddc35c8f9c989545119988f79ccc77
```
What kind of hash could this be?
```python
$ haiti bfddc35c8f9c989545119988f79ccc77
MD2 [JtR: md2]
MD5 [HC: 0] [JtR: raw-md5]
MD4 [HC: 900] [JtR: raw-md4]
Double MD5 [HC: 2600]
LM [HC: 3000] [JtR: lm]
RIPEMD-128 [JtR: ripemd-128]
Haval-128 [JtR: haval-128-4]
Tiger-128
Skein-256(128)
Skein-512(128)
Lotus Notes/Domino 5 [HC: 8600] [JtR: lotus5]
Skype [HC: 23]
Snefru-128 [JtR: snefru-128]
NTLM [HC: 1000] [JtR: nt]
Domain Cached Credentials [HC: 1100] [JtR: mscach]
Domain Cached Credentials 2 [HC: 2100] [JtR: mscach2]
DNSSEC(NSEC3) [HC: 8300]
RAdmin v2.x [HC: 9900] [JtR: radmin]
```
It seems it's the md4 hash of a common work.
Encryption/Decryption using gpg#

    You wish to encrypt a file called history_logs.txt using the AES-128 scheme. What is the full command to do this?

gpg --cipher-algo AES-128 --symmetric history_logs.txt

    What is the command to decrypt the file you just encrypted?

gpg history_logs.txt.gpg

    Find an encrypted file called layer4.txt, its password is bob. Use this to locate the flag. What is the flag?

```python
sarah@james:~$ find /home/sarah -type f -name layer4.txt 2>/dev/null
/home/sarah/system AB/keys/vnmA/layer4.txt

sarah@james:~$ gpg '/home/sarah/system AB/keys/vnmA/layer4.txt'
gpg: WARNING: no command supplied.  Trying to guess what you mean ...
gpg: AES256 encrypted data
gpg: encrypted with 1 passphrase
gpg: /home/sarah/system AB/keys/vnmA/layer4.txt: unknown suffix
Enter new filename [layer4.txt]: noraj.txt

sarah@james:~$ cat noraj.txt
1. Find a file called layer3.txt, its password is james.

sarah@james:~$ find /home/sarah -type f -name layer3.txt 2>/dev/null
/home/sarah/oldLogs/2014-02-15/layer3.txt

sarah@james:~$ gpg /home/sarah/oldLogs/2014-02-15/layer3.txt
gpg: WARNING: no command supplied.  Trying to guess what you mean ...
gpg: AES256 encrypted data
gpg: encrypted with 1 passphrase
gpg: /home/sarah/oldLogs/2014-02-15/layer3.txt: unknown suffix
Enter new filename [layer3.txt]:

sarah@james:~$ cat layer3.txt
1. Find a file called layer2.txt, its password is tony.

sarah@james:~$ find /home/sarah -type f -name layer2.txt 2>/dev/null
/home/sarah/oldLogs/settings/layer2.txt

sarah@james:~$ gpg /home/sarah/oldLogs/settings/layer2.txt
gpg: WARNING: no command supplied.  Trying to guess what you mean ...
gpg: AES256 encrypted data
gpg: encrypted with 1 passphrase
gpg: /home/sarah/oldLogs/settings/layer2.txt: unknown suffix
Enter new filename [layer2.txt]:

sarah@james:~$ cat layer2.txt
MS4gRmluZCBhIGZpbGUgY2FsbGVkIGxheWVyMS50eHQsIGl0cyBwYXNzd29yZCBpcyBoYWNrZWQu

sarah@james:~$ base64 -d layer2.txt
1. Find a file called layer1.txt, its password is hacked.

sarah@james:~$ find /home/sarah -type f -name layer1.txt 2>/dev/null
/home/sarah/logs/zmn/layer1.txt

sarah@james:~$ gpg /home/sarah/logs/zmn/layer1.txt
gpg: WARNING: no command supplied.  Trying to guess what you mean ...
gpg: AES256 encrypted data
gpg: encrypted with 1 passphrase
gpg: /home/sarah/logs/zmn/layer1.txt: unknown suffix
Enter new filename [layer1.txt]:

sarah@james:~$ cat layer1.txt
Flag{B07$f854f5ghg4s37}
```

Cracking encrypted gpg files#

    Find an encrypted file called personal.txt.gpg and find a wordlist called data.txt. Use tac to reverse the wordlist before brute-forcing it against the encrypted file. What is the the password to the encrypted file?

```python
sarah@james:~$ find /home/sarah -type f -name personal.txt.gpg 2>/dev/null
/home/sarah/oldLogs/units/personal.txt.gpg

sarah@james:~$ find /home/sarah -type f -name data.txt 2>/dev/null
/home/sarah/logs/zmn/old stuff/-mvLp/data.txt

sarah@james:~$ tac '/home/sarah/logs/zmn/old stuff/-mvLp/data.txt' > wordrev.txt

$ john /home/sarah/oldLogs/units/personal.txt.gpg -w wordrev.txt --format gpg
...
valamanezivonia

sarah@james:~$ gpg /home/sarah/oldLogs/units/personal.txt.gpg

sarah@james:~$ cat /home/sarah/oldLogs/units/personal.txt
getting stronger in linux
```
Reading SQL databases#

```python
sarah@james:~$ find /home/sarah -type f -name employees.sql 2>/dev/null
/home/sarah/serverLx/employees.sql

sarah@james:~$ cd /home/sarah/serverLx/

sarah@james:~$ mysql -p

mysql> source /home/sarah/serverLx/employees.sql

mysql> SELECT * FROM employees WHERE first_name = 'Lobel' and last_name LIKE '%Flag%';
+--------+------------+------------+----------------+--------+------------+
| emp_no | birth_date | first_name | last_name      | gender | hire_date  |
+--------+------------+------------+----------------+--------+------------+
| 499973 | 1963-06-03 | Lobel      | Flag{edited  } | M      | 1994-02-01 |
+--------+------------+------------+----------------+--------+------------+
1 row in set (0.07 sec)
```

Final Challenge#
```python
sarah@james:/home/shared/chatlogs$ cat LpnQ
(2020-08-13) Sarah: Hey Lucy, what happened to the database server? It is completely down now!

(2020-08-13) Lucy: Yes, I believe we have had a problem. I will need to investigate but for now there will be downtime for who knows how long.

(2020-08-13) Sarah: That is a shame, I needed to refer to a customer’s record due to them being unhappy with our service yesterday.

(2020-08-13) Lucy: if you ask Sameer, he may be able to help you find the back-up database copy we made a few hours ago?

(2020-08-13) Sarah: Of course, he is one of the sql developers around here in charge of the database creation, I will ask him in a few minutes. Thank you.

(2020-08-13) Lucy: No problem. By the way, our new security engineer may have accidently stored the SSH password of one of our employees. I have no idea how to change it and he will not be back till tomorrow.

(2020-08-13) Sarah: That is a shame. I am sure we will all be fine till he returns. Do you know which employee it is?

(2020-08-13) Lucy: I think it may have affected James but I not entirely sure.

(2020-08-13) Sarah: That is terrible, but I am sure nothing will come of it, he will be back tomorrow.

(2020-08-13) Lucy: True. It is just a concern of mine because James is the only one with root access. But as you said, we should be ok. Talk to you later. Bye.
```
    What is Sameer's SSH password?

Find files including Sameer:
```python
sarah@james:~$ grep -iRl Sameer /home 2>/dev/null
/home/shared/chatlogs/Pqmr
/home/shared/chatlogs/LpnQ
/home/shared/chatlogs/KfnP
```
```python
sarah@james:~$ cat /home/shared/chatlogs/Pqmr
(2020-08-13) Sarah: Hey Sameer, do you by any chance no where I can find the sql back-up copy on this system? The database server is down, and I really need to help a customer out.

(2020-08-13) Sameer: Sure. let me check.

(2020-08-13) Sarah: Thanks.

(2020-08-13) Sameer: check the home/shared/sql/ directory. It should be in there with the date of today.

(2020-08-13) Sarah: Thank you Sameer.

(2020-08-13) Sameer: No problem. It probably is encrypted. Just use the password: danepon.

(2020-08-13) Sarah: OK, thank you.

(2020-08-13) Sameer: No problem

(2020-08-13) Sameer: By the way, if you have any issues just talk to Michael as I will be off for the remainder of the day. See you tomorrow. Bye.

(2020-08-13) Sarah: Bye.
```
SQL backup should be in /home/shared/sql/ and encrypted with the password danepon.

```python
sarah@james:~$ cat /home/shared/chatlogs/KfnP
(2020-08-13) Sarah: Michael, I have been having trouble accessing the sql database back-up copy made today. Sameer gave me the password, but it just will not work?

(2020-08-13) Michael: Ah, yes. I remember, the security engineer was testing out a new automated software for creating sql database backups. He must have configured it to encrypt the backups with a different password.

(2020-08-13) Sarah: So how can I get a hold of it?

(2020-08-13) Michael: Good question. From what I remember the test program utilised a configuration file around 50mb. It is located inside the home/shared/sql/conf directory. This configuration file contained the directory location of a wordlist it used to randomly select a password from for encrypting the sql back-up copies with.

(2020-08-13) Sarah: I do not really understand the last part?

(2020-08-13) Michael: once you find the configuration file and consequently the wordlist directory, visit it. One of those wordlists must contain the password it used for the testing. All I remember is that the password began with ebq. You will need Sameer’s account. His SSH password is: thegreatestpasswordever000.

(2020-08-13) Sarah: Thank you, I will try to find it.
```
Info:

    password of /home/shared/sql/2020-08-13.zip.gpg is not danepon
    the config file is in /home/shared/sql/conf and is about 50mb
    the config file contains the wordlist directory
    the SQL backup password start with ebq
    Sameer's SSH password: thegreatestpasswordever000

    What is the password for the sql database back-up copy

Find the config file:

```python
sameer@james:~$ find /home/shared/sql/ -type f -size 50M
/home/shared/sql/conf/JKpN

sameer@james:~$ head /home/shared/sql/conf/JKpN
Software: sql auto-back-up
Version: 2.3
Wordlist directory: aG9tZS9zYW1lZXIvSGlzdG9yeSBMQi9sYWJtaW5kL2xhdGVzdEJ1aWxkL2NvbmZpZ0JEQgo=
sql-encrypt: true
time: 2h*
user: none
```
Wordlist directory:
```python
sameer@james:~$ printf %s aG9tZS9zYW1lZXIvSGlzdG9yeSBMQi9sYWJtaW5kL2xhdGVzdEJ1aWxkL2NvbmZpZ0JEQgo= | base64 -d
home/sameer/History LB/labmind/latestBuild/configBD
```
There is a mistake here, the last folder is configBDB and not configBD.

There 3 files with such passwords starting with ebq:

```python

sameer@james:~$ grep -iRlE '^ebq' '/home/sameer/History LB/labmind/latestBuild/configBDB'
/home/sameer/History LB/labmind/latestBuild/configBDB/pLmjwi
/home/sameer/History LB/labmind/latestBuild/configBDB/LmqAQl
/home/sameer/History LB/labmind/latestBuild/configBDB/Ulpsmt
```
Show only the passwords:

```python

sameer@james:~$ grep -iRhE '^ebq' '/home/sameer/History LB/labmind/latestBuild/configBDB'
ebqiojsdfioj
ebqiojsiodj
ebqiojdifoj
ebqiopsjdfopj
ebqnice
ebqops
ebqiuiud
ebqjoisjdfij
ebqkjjdd
ebqijsji
ebqopkopk
ebqattle
```
Let's download the encrypted SQL backup:
```python

$ scp sameer@10.10.61.194:/home/shared/sql/2020-08-13.zip.gpg .
```
gpg2john doesn't work because the file is too big:

```python
gpg2john 2020-08-13.zip.gpg 2020-08-13.zip.gpg.hash

File 2020-08-13.zip.gpg
Bad parameter: give(len=106935040, buf=0x5571785b0420, buf_size=90000), len can not be bigger than buf_size.
```
So let's use this script instead:

```python

$ ./crackgpg.sh 2020-08-13.zip.gpg wordlist.txt
FAILED - ebqiojsdfioj
FAILED - ebqiojsiodj
FAILED - ebqiojdifoj
FAILED - ebqiopsjdfopj
FAILED - ebqnice
FAILED - ebqops
FAILED - ebqiuiud
FAILED - ebqjoisjdfij
FAILED - ebqkjjdd
FAILED - ebqijsji
FAILED - ebqopkopk

SUCESS - ebqattle
```
    Find the SSH password of the user James. What is the password?

Extarct the archive:

```python	

$ 7z x 2020-08-13.zip
```
Let's find about james:

```python
$ grep -ri james 2020-08-13
2020-08-13/sakila/sakila-mv-data.sql:(84,'JAMES','PITT','2006-02-15 04:34:33'),
2020-08-13/sakila/sakila-mv-data.sql:(71,1,'KATHY','JAMES','KATHY.JAMES@sakilacustomer.org',75,1,'2006-02-14 22:04:36','2006-02-15 04:57:20'),
2020-08-13/sakila/sakila-mv-data.sql:(299,2,'JAMES','GANNON','JAMES.GANNON@sakilacustomer.org',304,1,'2006-02-14 22:04:37','2006-02-15 04:57:20'),
2020-08-13/load_employees.dump:(499996,'1953-03-07','James','vuimaxcullings','M','1990-09-27'),
```
The SSH password of James is written instead of his lastname.

    SSH as james and change the user to root?

James has root permission through sudo:

```python
james@james:~$ sudo -l
[sudo] password for james: 
Matching Defaults entries for james on james:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User james may run the following commands on james:
    (ALL : ALL) ALL
```
Grab the flag:

```python
james@james:~$ sudo cat /root/root.txt
Flag{edited}

NOW YOU ARE LINUX STRONGER!!!
```
