
Als erstes muss die Länge des Keys ermittelt werden 
`The length of the enrollment key is wrong`  wird ausgegeben wenn die Länge nicht stimmt.
`Wrong enrollment key` wird ausgegeben wenn die Länge stimmt. Das ist bei 20 der Fall.

Am Timing kann man feststellen, wann ein Zeichen des Keys richtig ist.

```python
def check_key():
    r = conn()
    for c in charset: 
      r.recvuntil(b"? ")
      key = b"" + c + b"~" * (20-len(c)); 
      r.sendline(b"enroll Cybersecurity " + key)
      a = r.recvline()
      r.recvuntil(b"took ")
      b = r.recvline()
      print(f"{c}:{a} {b} ")
    r.close()
```

```python
def check_key():
    r = conn()
    for c in charset: 
      r.recvuntil(b"? ")
      key = b"tQfyO8qvUaL5cY7qu2rw" + c + b"~" * (0-len(c)); 
      r.sendline(b"enroll Cybersecurity " + key)
      a = r.recvline()
      r.recvuntil(b"took ")
      b = r.recvline()
      print(f"{c}:{a} {b} ")
    r.close()
```

