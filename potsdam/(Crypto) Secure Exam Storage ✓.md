Nach Analyse des Skripts stellt man fest, dass die hmac aus einem MD5 Hash erzeugt wird, welcher wiederrum ausschließlich unserinput hasht.
Mit einer HashClash UniColl Attacke auf MD5 lässt sich so das LSB des 10 Byte (des letzten Blocks) um eins erhöhen. DIes kann man sich zunutze machen um bei unterschedlichem Input den gleichen MD5 Hash zu erzeugen und somit für zwei unterschiedliche Sessionsdaten die gleiche hmac.

Man kann `{"user": "adminadminadminadminadminadminadminadminadminadmina", "admin": 0}` als Prefix für diese unicoll Attacke benutzen, dabei werden 2 Dateien erzeugt gleichem md5 hash. Da die `0` exakt positioniert wurde, wird diese vom derder Attacke durch eine `1` ersetzt, was dazu führt, dass wir für die registrierung den Inhalt der ersten Datei hinschicken können und für den Zugriff auf exams die den Inhalt der zweiten Datei. Da bei den den selben MD5 Hash und damit die selbe hmac haben werden wir als Admin akzeptiert und die Flagge ausgegeben.

```
└─$ cat collision1.bin |hex          
7b2275736572223a202261646d696e61646d696e61646d696e61646d696e61646d696e61646d696e61646d696e61646d696e61646d696e61646d696e61222c202261646d696e223a20*30*7d0a730c53e417114e55ab1f5668fbc7f92ba25a353ef8a535ebe4541b5139f9528b69b1fef3a7e7ac328a1792239f10f586276b29e66087f5cfcbbc9b974451e414e274245f2330ea26cc1ac3dedc02eaf1e3f92bab346142b0229e09ee31093fe01316fdd59c75546381281b457bfec15e8389cf82
```

```
└─$ cat collision2.bin |hex
7b2275736572223a202261646d696e61646d696e61646d696e61646d696e61646d696e61646d696e61646d696e61646d696e61646d696e61646d696e61222c202261646d696e223a20*31*7d0a730c53e417114e55ab1f5668fbc7f92ba25a353ef8a535ebe4541b5139f9528b69b1fef3a7e7ac328a1792239f10f586276b29e66087f5cfcbbc9b974450e414e274245f2330ea26cc1ac3dedc02eaf1e3f92bab346142b0229e09ee31093fe01316fdd59c75546381281b457bfec15e8389cf82
```

```
──(venv)─(kali㉿kali)-[/mnt/…/potsdam/secure_exam_storage/hashclash/ipc_workdir]
└─$ md5sum collision1.bin            
a85ba7f1592de0a9d6b642eb90da2540  collision1.bin
                                                                                      
┌──(venv)─(kali㉿kali)-[/mnt/…/potsdam/secure_exam_storage/hashclash/ipc_workdir]
└─$ md5sum collision2.bin        
a85ba7f1592de0a9d6b642eb90da2540  collision2.bin
```

Nähere Infos zu den Attacken findet man unter: https://github.com/corkami/collisions 
