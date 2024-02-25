---
title: "Healthkathon BPJS 2022"
description: ""
summary: ""
date: 2022-11-05T07:09:00+07:00
lastmod: 2022-12-05T07:32:00+07:00
draft: false
menu:
  posts:
    parent: ""
    identifier: "healthkathonbpsj-2022"
weight: 910
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

<br>

## CHALL'S

| Category | Challenge |
|----------|-----------| 
| Chall 1  | [Chall 1](#chall-1) |

<br>

### CHALL 1

[http://pentest.student.1337hackathon.id:81/](http://pentest.student.1337hackathon.id:81/)

<br>
<div style="text-align:center">
<img src="https://raw.githubusercontent.com/nopedawn/CTF/main/HealthkathonBPJS-2022/chall1/images/chall1_webpage.png" width="500">
</div>
<br>

Diberikan sebuah soal nomor 1 berupa webpage berikut, setelah itu kami cari tahu view page sourcenya seperti berikut

<br>
<div style="text-align:center">
<img src="https://raw.githubusercontent.com/nopedawn/CTF/main/HealthkathonBPJS-2022/chall1/images/image1.png">
</div>
<br>

Kemudian kami menemukan clue pada saat kami meng-inspect halamannya, yaitu berupa strings base64

```
RGVjb2RlIHBhcnQ1IGJ5IHVzaW5nIHRoZSBYT1IgZnVuY3Rpb24gd2l0aCBjdXN0b20gY3NzIG51bWJlci4=
```

<br>
<div style="text-align:center">
<img src="https://raw.githubusercontent.com/nopedawn/CTF/main/HealthkathonBPJS-2022/chall1/images/image2.png">
</div>
<br>

Setelah kami decode hasilnya seperti berikut

```bash
$ echo 'RGVjb2RlIHBhcnQ1IGJ5IHVzaW5nIHRoZSBYT1IgZnVuY3Rpb24gd2l0aCBjdXN0b20gY3NzIG51bWJlci4=' | base64 --decode
```

<br>
<div style="text-align:center">
<img src="https://raw.githubusercontent.com/nopedawn/CTF/main/HealthkathonBPJS-2022/chall1/images/image3.png">
</div>
<br>

Singkat cerita kami coba menggunakan `curl` dengan parameter `-v` untuk mencari informasi dari URL-nya, dan kami menemukan potongan flag berupa Hexadecimal

```bash
$ curl -v http://pentest.student.1337hackathon.id:81/
```

<br>
<div style="text-align:center">
<img src="https://raw.githubusercontent.com/nopedawn/CTF/main/HealthkathonBPJS-2022/chall1/images/image4.png">
</div>
<br>

Setelah itu kami coba decode dari format Hexadecimal to ASCII dengan tools 
[https://www.rapidtables.com/convert/number/hex-to-ascii.html](https://www.rapidtables.com/convert/number/hex-to-ascii.html)
Didapatkanlah Flag ***Part1*** s/d ***Part4*** nya yaitu, `BPJS{Mel4y4ni_s3penuh_h4t!_m3l4mp4u1`
dan tinggal sisa ***Part5*** dari flagnya yaitu `%y?y=,#}`

Sesuai dengan cluenya yaitu ***“Decode part5 by using the XOR function with custom css number.”***
maka dari itu kami mencari script untuk memecahkan XOR function dengan custom css number dan menemukan script dari post berikut 
[https://crypto.stackexchange.com/questions/98727/how-can-i-decode-a-xor-cipher-with-a-string-key-i-know](https://crypto.stackexchange.com/questions/98727/how-can-i-decode-a-xor-cipher-with-a-string-key-i-know)

Berikut script Python-nya

```python
def decrypt(encrypted: bytes, key: bytes):
    result = []
    
    for i in range(len(encrypted)):
        result.append(encrypted[i] ^ key[i % len(key)])

    return bytes(result)
```

Lalu kami jalankan dengan command `python3 -i xor_solver.py` dan didapatkanlah **Part5** dari Flagnya yaitu `h4r4pan`

```bash
$ python3 -i xor_solver.py
>>> encrypted = b"%y?y=,#"
>>> key = bytes([77])
>>> decrypt(encrypted, key)
```

<br>
<div style="text-align:center">
<img src="https://raw.githubusercontent.com/nopedawn/CTF/main/HealthkathonBPJS-2022/chall1/images/image5.png" width="300">
</div>
<br>

Flag: `BPJS{Mel4y4ni_s3penuh_h4t!_m3l4mp4u1_h4r4pan}`
