Es wird ein Token bereitgestellt und die Möglichkeit einen Token zu validieren. Dabei ist die Validierungsschnittstelle so auskunftsfreudig, dass man diese als Orakel für einen Padding Orakel Attacke missbrauchen kann.

[Dieses Projekt](https://github.com/cemonatk/padding-oracle-demo.git) eignet sich gut als Startpunkt für die Attacke, es müssen aber die Funktionen `check_padding` auf den bereitgestellten Server angepasst werden. Mit hilfe von pwntools ist das aber schnell erledigt. Das Programm läuft dann eine Weile und gibt nach und nach die Flagge `flag{padd1n9_0racl3::W9q9ovC1eg2D}` aus.

```python
def get_ciphertext():
    """
    Gathers ciphertext from web page
    :return: ciphertext
    """
    r = remote("10.65.43.225", 1337) 
    r.recvuntil(b": ");
    ciphertext = r.recvuntil(b"\n")[:-1]
    r.close()
    print(f"Got {ciphertext}")
    return b64encode(bytes.fromhex(ciphertext.decode('ascii')))
 
def check_padding(ciphertext, r):
    """
    Checks the padding if it is correct.
    :param ciphertext
    :return: True if padding is correct, False otherwise.
    """
    r.recvuntil(b"input: ");
    r.sendline(bytes(ciphertext.hex(), 'ascii'))
    answer = r.recvline().decode('ascii')
    if answer == "Error: Padding is incorrect.\n":
        return False
    elif answer == "Error: PKCS#7 padding is incorrect.\n":
        return False
    elif answer == "Error: Data must be padded to 16 byte boundary in CBC mode\n":
        return False
    return True
    #try:
    #    return urllib.request.urlopen(url).getcode() == 200
    #except:
    #    return False
```



