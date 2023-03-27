Erste Flag:
`strings coffee-maschine | grep flag`

Zweite Flag:
`obfuscation` und `obfuscated_password` aus dem Binary lesen

C Schnipsel aus Ghidra:
```c
for (local_50 = 0; local_50 < 0x10; local_50 = local_50 + 1) {
    *(undefined1 *)((long)&local_78 + local_50) =
    obfuscated_password[local_50] ^ obfuscation[local_50];
}
```

Python um Passwort zu rekonstruieren:
```python
obfuscation         = [0x66, 0xef, 0x6e, 0x3a, 0xf1, 0x09, 0x84, 0x65, 
					   0x6d, 0x36, 0xa4, 0x1c, 0xe1, 0xa9, 0x74, 0x00]
obfuscated_password = [0x03, 0xb8, 0x0b, 0x71, 0x82, 0x70, 0xca, 0x09, 
					   0x0f, 0x4c, 0xd7, 0x5e, 0xa6, 0xd9, 0x3e, 0x00]
pw = ""
for i in range(0,16):
  pw += chr(obfuscated_password[i] ^ obfuscation[i])
print (pw)
```
