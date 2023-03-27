`git clone https://github.com/corkami/collisions` 

Zwei unterschiedliche Bilder mit den gleichen Abmessungen generieren.
`python3 jpg.py bild1.jpg bild2.jpg` erzeugt `collision1.jpg` und `collision2.jpg`
Diese kann man per folgendem Skript an den Service übermitteln:

```python
#!/usr/bin/env python3

from pwn import *
import base64


def conn():
    r = remote("10.65.32.177", 1337)

    return r


def main():
    r = conn()

    #r.interactive()
    bla = open("./collision1.jpg","rb").read() 
    r.sendline(base64.b64encode(bla))
    bla = open("./collision2.jpg","rb").read() 
    r.sendline(base64.b64encode(bla))
    r.interactive()
if __name__ == "__main__":
    main()
```
