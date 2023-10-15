# aes_tool
A command line tool to encrypt/decrypt file.
Using openssl.

## Usage
```Bash
$ hexdump test.txt -C
00000000  54 68 69 73 20 69 73 20  61 20 54 65 73 74 2e 20  |This is a Test. |
00000010  41 42 43 44 45 46 47 2e  20 31 32 33 34 35 36 37  |ABCDEFG. 1234567|
00000020  38 2e 0a                                          |8..|
00000023

$ ./aes_tool test.txt test.enc 123456 -e
plain 54 68 69 73 20 69 73 20 61 20 54 65 73 74 2e 20 len=16
encry fa c9 85 60 a6 93 1a ca ff d1 96 84 50 78 07 38 len=16
plain 41 42 43 44 45 46 47 2e 20 31 32 33 34 35 36 37 len=16
encry 3b 4b d0 9b b5 22 4a ac 88 34 aa eb c9 12 ae b8 len=16
plain 38 2e 0a len=3
encry 81 f9 e9 de bc e4 37 f6 e9 7a 1f 8c 4c 19 81 c4 len=16

$ hexdump test.enc -C
00000000  fa c9 85 60 a6 93 1a ca  ff d1 96 84 50 78 07 38  |...`........Px.8|
00000010  3b 4b d0 9b b5 22 4a ac  88 34 aa eb c9 12 ae b8  |;K..."J..4......|
00000020  81 f9 e9 de bc e4 37 f6  e9 7a 1f 8c 4c 19 81 c4  |......7..z..L...|
00000030  03                                                |.|

$ ./aes_tool test.enc test.dec 123456 -d
plain 54 68 69 73 20 69 73 20 61 20 54 65 73 74 2e 20 len=16
encry fa c9 85 60 a6 93 1a ca ff d1 96 84 50 78 07 38 len=16
plain 41 42 43 44 45 46 47 2e 20 31 32 33 34 35 36 37 len=16
encry 3b 4b d0 9b b5 22 4a ac 88 34 aa eb c9 12 ae b8 len=16
plain 38 2e 0a len=3
encry 81 f9 e9 de bc e4 37 f6 e9 7a 1f 8c 4c 19 81 c4 len=16

$ hexdump test.dec -C
00000000  54 68 69 73 20 69 73 20  61 20 54 65 73 74 2e 20  |This is a Test. |
00000010  41 42 43 44 45 46 47 2e  20 31 32 33 34 35 36 37  |ABCDEFG. 1234567|
00000020  38 2e 0a                                          |8..|
00000023
```

## WARNING: Not compitable with openssl

```Bash
$ hexdump -C test.txt 
00000000  54 68 69 73 20 69 73 20  61 20 54 65 73 74 2e 20  |This is a Test. |
00000010  41 42 43 44 45 46 47 2e  20 31 32 33 34 35 36 37  |ABCDEFG. 1234567|
00000020  38 2e 0a                                          |8..|
00000023

$ openssl enc -aes-128-ecb -in test.txt -out test.enc -K 313233343536

$ hexdump -C test.enc
00000000  fa c9 85 60 a6 93 1a ca  ff d1 96 84 50 78 07 38  |...`........Px.8|
00000010  3b 4b d0 9b b5 22 4a ac  88 34 aa eb c9 12 ae b8  |;K..."J..4......|
00000020  2f 30 28 0e 2d 4e 83 01  25 aa a4 f5 4e 37 b9 74  |/0(.-N..%...N7.t|
00000030

$ openssl enc -aes-128-ecb -in test.enc -out test.dec -K 313233343536 -d

$ hexdump -C test.dec 
00000000  54 68 69 73 20 69 73 20  61 20 54 65 73 74 2e 20  |This is a Test. |
00000010  41 42 43 44 45 46 47 2e  20 31 32 33 34 35 36 37  |ABCDEFG. 1234567|
00000020  38 2e 0a                                          |8..|
00000023

```