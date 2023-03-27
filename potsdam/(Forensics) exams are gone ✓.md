- Mit Testdisk die drei dateien kitty.jpg password.txt und exams.zip.enc wiederherstellen
	- in Password.txt ist die erste Flagge
Passwort.txt
```
You've found the first flag: flag{n0_f4t_st1ll_th3r3::iarKLZSfh9pb}. The following command could be interesting for you: openssl enc -d -aes-256-ctr -nosalt -pbkdf2 -k 88058c49eac8
```
Mit  `openssl enc -d -aes-256-ctr -nosalt -pbkdf2 -k 88058c49eac8 < exams.zip.enc > exams.zip` lässt sich das zip entschlüsseln. man bekommt ein Examen:
```
# HHI Hackxam

This is an exam. Please do not leak.

1. What ended in 1896? **Answer:** 1895
1. Bob has 36 candy bars. He eats 29. What does he have now? **Answer:** Diabetes. Bob has Diabetes.
1. What is the strongest force on earth? **Answer:** Love for cats.
1. Please decode the following poem from z85:

q/un&aAg+kB0a[ewftx8A+PDmB0b4twPGyfmRcyIzE<@6A:-D?efFvzv{%EbB0b1cB7YSfB7D)frcJ4#v}YN]xcqq8x(4&wayMyavpK7:AWL]Jxlv{0wH[f/zY&O4v@C)?aARgtBsXLCzEWZjAcbV4ayPd#aARsewg!h@l31e<xK#DiA=kx6aARpqz/]Yaay/t2wGUA0wftubBy/IA3pwlzB0b18v}/)}wPw]mwN/:(BAn#QCwhejazC.mx>Ia3edbx{y&r*0x(mMazdN^fvp%d)aztF1wmYT3w].*baAImfxML^js7#+&aAIsjy?$k5zE:(hBy!(%Bz9iFBzblhaAR4cwGUP3x>Ia3e^.}OzEWP}wN(]}y**%$efFvzByx6evqGU7x(mMaBAg@3BsW+#zY<guv@DK4AV/EqwO&$vvixe[y?W=#azbg[BsW=2x([2hv@bN$B0a[ewfu8fx(!63A=S=OBzblhay/tbAbo9cwH[f/xK@q@xKLZ[wO#c(efF[OA=L(ixcp]aaAI:rwPP58z/f5@x(>%m3qUsTv{%F2efFRmv@2T@B1wCxzE:(iwQ5qtwO#0@wnb{]edaV=v%8*az/{azBAh8lefFwqCvt=raz2!py&sudzF7HcnP2U)xK@q%x>Id4vqE6bwNPy(efG4FwQbzlwO2*6zeTl3x(mMm3pb!Uz/PV8aA7<mB7F<4wPR#AayP8gvr(]pB-7/fy?dl$xd:I#luNw)vR6:(A+c^Aw]zYjCw7MdwGUF>BAnNBz^^Gl3pX&uxlbh7zE:(hwN/:(BAnNwvr&#9vqG:5Bzbl5aztXgwH[fVx>g:=zxJF3wPe=azxJCcwmWqmvixz#B8$=5wGV8kaA8EwedaV=zfZhAwPA5EaA}mdBzkS9aARJAvR3W6xM59je^.}:zY&?bwPe=qz/{7ywQd<daAIj8A=rMLvqYP#y?W%jwO@S2y&sxaeda<+AV/4fwmPm?azbB#xlbQDvixVjwNPU5A+cwnzY&RoAbP/eedaWXwfu8gBz8!bvruMkvqYP#xKLy^wPz&mvriMpz/{7yxM4%lB1vU:azL?qA=bDlaA7<mwnc9{z*2YjC}p7-z/)Bzy-)Xqz/xSowIaq%tv}XWxm1img&k9Szzlftxe1iViYYX}w[=1aD1*wjBXEi?3lQDl
```

Dies kann man mit einem z85 decoder online entschlüsseln:

```
Soft paws and curious eyes,
Feline grace, a cat's disguise,
Twitching tails, a hacker's guide,
To decode text, encrypted and tied.

As they roam through code and bytes,
Cats decipher secrets, with insight,
Unlocking messages hidden from sight,
With skill and stealth, they take flight.

Encoded flags, a tantalizing treat,
To uncover them, a feline feat,
With claws and whiskers, they complete,
The challenge, purring in sweet conceit.

Oh cats, hackers, and text encoding,
A curious trio, always exploring,
In the digital realm, they keep molding,
A world of secrets, always unfolding.

But beware, for where cats roam,
Flags and secrets may call them home,
Hidden deep in code, a message to own,
A mystery, waiting to be shown.

So keep your eyes sharp, and listen close,
For hidden flags, a treasure to expose,
And with cats and hackers as your hosts,
A journey of discovery, you'll propose.

[flag{ex4m5_n0t_g0n3::EAfijzyiX-uL}]
```