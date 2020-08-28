# Password Generator
Generate a random password of length *n*.

## Usage
The script requires one command line argument in the form `generate_pw.py n`. *n* being an integer.

## Example output
*n* = 16
```
4V'0{tFx}!fZIEtw
```

*n* = 64
```
@c;05X(,+qmP4gCh6(^dd1HR9(qEe!?GX<\VvQ>dp\q4^ykDbz1/@d{YLAdw$xYZ
```

*n* = 1024
```
k$G.W*9~8fT2T6J7,=34g50}Uiqcijo,SD/z_8po%F6KZ6zxrqs1fZ01c72Ul6yCRA1)N[5l)n`@/NMA-4PPn+dHvlNMuEg668@FT8_,
z+.w06f-b6S)-Lp+%y?w5b:f\\H9d{8+35dPw14Tr9rI-v7=sau39I**g<7686<e,Ko0j_3iV5!f1g,T:?0^4wO#fx;-nWlom0(d\mt5
cuI=1U'aP8MQ<XB^Uh<phZ`1caI%Z56gXAFBm6GCw*1l9=13H8>B7X(`e9u6QjpIMyc@`kAz*3)l$q{]K9!9d/V^!v$i6+3ye4;Kk6.T
0OixNT_nQF3%j3dk2#6x5U1~o7L61vReJR<0Obwq%6#0+dxa69Q+inJ8A6x6^ub$00u7Qs{}OO7bS1Yw#0q6,HGK9}20hx6$69sc3KP8
P[&>i1dmcZl3664ihJT"G@iXO8;+n0eGGKwqS+q)!*TzdQKDsZA$`T^nt~Ia]tB]zU^<%ShR!,|U:#+MtN#ap]]3)WE:``y"C;\R^Yf
L.2\ZHTw,p$hwkWuuRV/++n{ZAu!h'y:?]ax}UHn!R$GR|Y]k]z5,.qz-pl+XNu'nQz=:NJ3I#[lyQbwc"a^s;exYVa$C:I:Nn?t[Lc%
9dwwVncB)TsX|vXe;MqDf{y"IRxayHfkQHo\O[TM/jy?~Kq@S`>T[c/p"fZa:_%L#Z`@;@|,`E%YHXk?C5o@ycmEgS)UrM>j|;"?`J~[
[#J"&fb`-c!&u@TSti{Kvb:`ji*Y5?>\dHB/~Q,[Rc,l=j'YNiaelD:HbGAkq~p*KFcKLnTR)fHwnTWH)$D/B;A%Y*uq6`CM";dSo9#h
>+y<cc.nXZyzNTHF"{<"ZZ$-Y&|mESj8N?m!<ETi'%]H"kBLiY?F`J'"^rH$QNn)GF:B(X8`hWH{}C.^EZ>>B0H=Z3wLWLHTUYtp\W10
/j\jQ!68o"WgrKEm{]%),+P=Pz^aJ%C]"qfk@OP~;mlG5[THQUs<@r5eYI>Hat,js15jtaO!%GQu-W$znD06iaM
```

## Password variety
The password is made up of a combination of lowercase, uppercase, digits, and punctuation characters. In order to ensure the password has enough variety there is a set number of minimum characters required of each type (lowercase, uppercase, etc.). For example, at the moment the minimum number of lowercase characters that must be present in the resulting password is 20% of *n*.

**Minimum character counts**
```python
num_of_lowercase = int(float(n) * 0.2)
num_of_uppercase = int(float(n) * 0.2)
num_of_digits = int(float(n) * 0.1)
num_of_punctuation = int(float(n) * 0.2)
num_of_remainder = int(n) - num_of_lowercase - num_of_uppercase - num_of_digits - num_of_punctuation
```

## `chars_dict` explained
This dictionary contains strings of ASCII characters. The corresponding `counter` is decremented each time a specific character type is concatenated to the string, and by the time the string reaches length *n*, all counters reach 0. For example, if *n* is 100, `num_of_lowercase` would be 20 at the start, and by the time we finished building the string, it reaches 0.

```python
mixed = list(string.ascii_lowercase + string.ascii_uppercase + string.digits + string.punctuation)
random.shuffle(mixed)

chars_dict = {
    1: {"counter": num_of_lowercase, "chars": string.ascii_lowercase},
    2: {"counter": num_of_uppercase, "chars": string.ascii_uppercase},
    3: {"counter": num_of_digits, "chars": string.digits},
    4: {"counter": num_of_punctuation, "chars": string.punctuation},
    5: {"counter": num_of_remainder, "chars": "".join(mixed)}
}
```

## Further notes
You can modify the resulting string's character variety by modifying the float values mentioned in **Password variety**. I found the greatest character variety with the current float values. Increasing `num_of_lowercase` from 0.2 to 0.3 results in a noticeble number of consecutive lowercase characters at the very end of the string (if *n* is large enough).
