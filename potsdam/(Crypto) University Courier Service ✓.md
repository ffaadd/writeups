
```
Welcome to the university courier service!

At our university, students can earn some extra money by working as a
courier. We only trust students with this task because some messages
may contain very secret information. Of course, trust is not enough
so we also encrypt the messages using asymmetric encryption.

	We currently have one message that needs to be distributed to 3
	different recipients. The message is encrypted so you cannot read it
yourself. You only get pairs of ciphertext and public key for the
different recipients. The recipients can then use their private key
to decrypt their message.

Data for recipient 1:
Ciphertext: 74092479092973463032189399041025133134602827622521647108670966212631055970326731563157793031778876829244263469795894595706918106540555495079730597784891478821669153736448843269134984113329933933169182203381109937632393914237622362499042570277609583677594589446784966118655781339805790971317104813008820176808
Public key:
-----BEGIN PUBLIC KEY-----
MIGdMA0GCSqGSIb3DQEBAQUAA4GLADCBhwKBgQDAJxR7Sk+cZc3YjjruBtjtjfl7
w3XbsgqkHG/9PujkPDeDpfV94BGT5jRNYxxkE5js/sNH41pbE17gGkWNYJKYxpr1
HAQyaVat14kJCJjAwhPaFXwAjpocnh0UfZNYudfmwv3W1g0P55SqC0CQnCfUm4Xz
iC/3acBRRzuyr5iKrwIBAw==
-----END PUBLIC KEY-----
Data for recipient 2:
Ciphertext: 39513563431246934260551290419452990032866680657153230384876042980612304379419613750538166603172063917897204655375864932701408334754938810950086614083585871779339808949335269511281267345764679901061070722279727274652349554321445039136136625449985385813231177317768172548743149474400369752713307435598603650964
Public key:
-----BEGIN PUBLIC KEY-----
MIGdMA0GCSqGSIb3DQEBAQUAA4GLADCBhwKBgQCTYsP9MCJPzIYhb4JMeZB3RKwc
x+yXpPEmcGc2dKS9sPeINcwkgpX3RXIA0VYMWMAsjlqcFtrdBtcK0gHH+YqcxzKs
1HPg/CZY7R8wuoLajlmuuiYDGd9cGtozoBl9r84t00QVyIDfmlUzyGiLkB0xHwBb
3jDuEFOuSwB0TNp7yQIBAw==
-----END PUBLIC KEY-----
Data for recipient 3:
Ciphertext: 65237040479951337821904607846088551252836789100252154358965442956147771782106177672999864729854312479454330751797895826941350580637341751040984223430739929026469077659828784061310777932529164288704603574836673861891255781795862447224008449790061672850752700706844454304804446637652161524451593825035866349031
Public key:
-----BEGIN PUBLIC KEY-----
MIGdMA0GCSqGSIb3DQEBAQUAA4GLADCBhwKBgQDzHO1zm5lDVjm2hwWxWQ1Po5Kv
Wa0VniqfOOAVZt4HWBJGEEDCj8Ns74xXfjozyaFdlPTnUmTDZDIwoTm7vRPJxfZt
R1YdxBbWiwp5c3EMb7hIbU7jzb0nhUvrpiN05o96XfQcefY0941g34kRnnVKukq4
0Hd5lsGqyC7favOFCwIBAw==
-----END PUBLIC KEY-----
```

Nachdem man die Nachricht in einzelene Dateien (pub1-3 und msg1-3) zerlegt hat wird Angriff über das Chinese Reminder Theorem ausgeführt (siehe https://www.johndcook.com/blog/2019/03/06/rsa-exponent-3/)
```python
from sympy import nextprime
from sympy.functions.elementary.miscellaneous import cbrt
from sympy.ntheory.modular import crt
from Crypto.PublicKey import RSA

def integer_to_bytes(integer, _bytes):
    output = bytearray()
    for byte in range(_bytes):
        output.append((integer >> (8 * (_bytes - 1 - byte))) & 255)
    return output

N = []
c = []
for i in range(1,4):
    public_key = RSA.importKey(open(f"pub{i}", 'r').read())
    N.append(public_key.n)
    c.append(int(open(f"msg{i}","r").read(),10)) 
x = crt(N, c)[0]
    
def ConvertToStr(num):
    st = ""
    while (num != 0):
        temp = num % 256
        st += chr(temp)
        chr(temp)
        num = num - temp
        num = num // 256
    st = st[::-1]
    return st

msg = cbrt(x)

msg2 = ConvertToStr(msg)
print (msg2)
```
