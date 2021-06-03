# PicoCTF-Tryout

# Tasks
## Transformation

![image](https://user-images.githubusercontent.com/78896740/119843788-815d4280-bf25-11eb-8719-f69a13b855cf.png)
or
```python
decode = '灩捯䍔䙻ㄶ形楴獟楮獴㌴摟潦弸彥ㄴㅡて㝽'
print(decode.encode('utf-16-be'))
```

## Mod 26:
rot 13 cipher
`picoCTF{next_time_I'll_try_2_rounds_of_rot13_hWqFsgzu}`

## mind your Ps and Qs:
Decrypt my super sick RSA:
c: 421345306292040663864066688931456845278496274597031632020995583473619804626233684
n: 631371953793368771804570727896887140714495090919073481680274581226742748040342637
e: 65537
using factordb i found p and q.
p:1461849912200000206276283741896701133693
q:431899300006243611356963607089521499045809
and used https://www.dcode.fr/rsa-cipher the remaining

## new ceaser
```py
import string

LOWERCASE_OFFSET = ord("a")
ALPHABET = string.ascii_lowercase[:16]

def b16_decode(enc):
    dec = ""
    for i in range(0, len(enc), 2):
        n1 = ord(enc[i]) - LOWERCASE_OFFSET
        n2 = ord(enc[i+1]) - LOWERCASE_OFFSET
        dec += chr((n1 << 4) + n2)
    return dec


def unshift(c, k):
    t1 = ord(c) - LOWERCASE_OFFSET
    t2 = ord(k) - LOWERCASE_OFFSET
    return ALPHABET[(t1 - t2) % len(ALPHABET)]


enc = 'apbopjbobpnjpjnmnnnmnlnbamnpnononpnaaaamnlnkapndnkncamnpapncnbannaapncndnlnpna'

for key in ALPHABET:
    b16 = ""
    for i, c in enumerate(enc):
        b16 += unshift(c, key[i % len(key)])

    flag = b16_decode(b16)
    if all([c in string.printable for c in flag]):
        print(flag)
        break
```

## GET aHEAD
└──╼ $curl --HEAD http://mercury.picoctf.net:28916/
HTTP/1.1 200 OK
flag: picoCTF{r3j3ct_th3_du4l1ty_70bc61c4}
Content-type: text/html; charset=UTF-8

## Cookies
changing the Cookies to 18 gave me flag(guess work ^^')

## Insp3ct0r
picoCTF{tru3_d3t3ct1ve_0r_ju5t_lucky?f10be399}
inspected source

## Scavenger Hunt
## picoCTF{th4ts_4_l0t_0f_pl4c3s_2_lO0k_74cceb07}
same wy inspecting here and there gave me flag

## Numbers:
the given numbers are the character number in English alphabets

## information:
Try exiftool to view the details of the file since its mentioned as hint
It contains the Base64 encoded text,So decoding it will give the flag.
picoCTF{the_m3tadata_1s_modified}

## Obedient Cat:
cat image 
gave me flag:picoCTF{s4n1ty_v3r1f13d_2aa22101}

## Python Wrangling:
Usage: ende.py (-e/-d) [file]
python3 ende.py -d flag.txt.en
picoCTF{4p0110_1n_7h3_h0us3_67c6cc96}

## Wave a Flag:
./warm -h gave me flag

## Nice netcat:
 nc mercury.picoctf.net 49039 | cat > flag1.txt and put in decoder ...got the flag

## Static ain't always noise:
strings static
gave me flag

