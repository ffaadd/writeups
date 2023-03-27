Einfache monoalphabetische Substitution aber im Anschluss muss für die Flagge noch auf Groß und Kleinschreibung geachtet werden.

```python
with open("./letter.enc", "r") as file:
    cipher = file.read().lower()

    cipher = cipher.replace("m", "\033[1mD\033[0m")
    cipher = cipher.replace("r", "\033[1mS\033[0m")
    cipher = cipher.replace("f", "\033[1mT\033[0m")
    cipher = cipher.replace("t", "\033[1mE\033[0m")
    cipher = cipher.replace("x", "\033[1mA\033[0m")
    cipher = cipher.replace("v", "\033[1mR\033[0m")
    cipher = cipher.replace("h", "\033[1mI\033[0m")
    cipher = cipher.replace("d", "\033[1mN\033[0m")
    cipher = cipher.replace("c", "\033[1mU\033[0m")
    cipher = cipher.replace("q", "\033[1mP\033[0m")
    cipher = cipher.replace("b", "\033[1mL\033[0m")
    cipher = cipher.replace("w", "\033[1mY\033[0m")
    cipher = cipher.replace("i", "\033[1mO\033[0m")
    cipher = cipher.replace("k", "\033[1mG\033[0m")
    cipher = cipher.replace("y", "\033[1mH\033[0m")
    cipher = cipher.replace("j", "\033[1mW\033[0m")
    cipher = cipher.replace("e", "\033[1mV\033[0m")
    cipher = cipher.replace("z", "\033[1mM\033[0m")
    cipher = cipher.replace("a", "\033[1mF\033[0m")
    cipher = cipher.replace("s", "\033[1mX\033[0m")
    cipher = cipher.replace("u", "\033[1mK\033[0m")
    cipher = cipher.replace("n", "\033[1mB\033[0m")
    cipher = cipher.replace("o", "\033[1mQ\033[0m")
    cipher = cipher.replace("l", "\033[1mJ\033[0m")
    cipher = cipher.replace("p", "\033[1mC\033[0m")
    cipher = cipher.replace("g", "\033[1mz\033[0m")
    print(cipher.lower())

#abxk{bxdkcxkt-qxfftvdr-hdpbcmtm::gGe_hYTPNQFc} # cipher
#flag{language-patterns-included::zzv_ihecbptu} # cleartext
#flag{language-patterns-included::zZv_iHECBPTu} # cleartext with case
```
