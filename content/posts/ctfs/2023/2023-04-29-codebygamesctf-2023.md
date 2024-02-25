---
title: "Codeby Games CTF 2023"
description: ""
summary: ""
date: 2023-04-15T16:13:18+07:00
lastmod: 2023-04-15T16:13:18+07:00
draft: false
menu:
  posts:
    parent: ""
    identifier: "codebygamesctf-2023"
weight: 910
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

[https://ctftime.org/event/1975](https://ctftime.org/event/1975)

<br>
<p align="center">
  <a href="https://ctftime.org/event/1975" target="_blank">
    <img src="https://ctftime.org/media/cache/c3/02/c3022833425d41e969ae0c63bf69b10e.png" width="200">
  </a>
</p>

### Challs
| Category       | Challenge |
| ---------------| --------- |
| Cryptography   | [RSA 1 Basics](#rsa-1-basics) |
| Cryptography   | [Family](#family) |
| Steganography  | [Girl with a secret](#girl-with-a-secret) |
| Steganography  | [Earth hum](#earth-hum) |
| Misc           | [Runes](#runes) |
| Misc           | [Favorite animated series](#favorite-animated-series) |

<br>

### RSA 1 Basics

<details>
  <summary>Description</summary>
  
  > [null]
  
  > Flag Format: CODEBY{}
  
</details>

Given a cryptography challenge with a zip file containing [data.txt](https://github.com/nopedawn/CTF/blob/main/CodebyGameCTF23/RSA1_Basics/data.txt) and [flag.txt](https://github.com/nopedawn/CTF/blob/main/CodebyGameCTF23/RSA1_Basics/flag.txt), where we have to decrypt the message in `flag.txt` using the given exponent key `n`, `e`, and `p`.

To implement of RSA decryption algorithm that reads in the modulus `n`, the public exponent `e`, and the prime factor `p` of `n` from the given values. Also imports a function inverse from an external library that calculates the modular multiplicative inverse of two numbers.

Calculates the other prime factor `q` of `n` by dividing `n` by `p`, then computes the private key `d` using the modular multiplicative inverse function by passing `e` and `(p-1)*(q-1)` as inputs.

```python3
from Crypto.Util.number import inverse, long_to_bytes

n = 17821369821197224755204170576717386974772583796320656477539620911939396151906969461959183978640937853223745304126597764393313271455282077396239424618606794404260667285392141808188728083834584927026023081706807877287176411455869333099599758756680824930296103562451364106123092367375221182676628604366038187928496804145884268753169728377208516981412594946003622745692274230506436281885419071635199138875290167920431573351256816462603222296067133230212113705435433321977478320363027010331451497317278086877300977556100259644050343025778299297465892385900238472919994896492369105460841980012051688350169675505544039420123
e = 65537
p = 1972000550284100445870121306958622830045225641252954033009593459446242613031033375213304073309426202713792319087153903001608198707751563017341316136191257392659269749490809852144061763170826581018719515204465050487987949598939979468867872704976528393610305938567746277939323612907052468216732931923001246346805966071415508727723

q = n // p

d = inverse(e, (p-1)*(q-1))

with open('flag.txt', 'rb') as f:
    ciphertext = f.read()

plaintext = pow(int.from_bytes(ciphertext, 'big'), d, n)

decoded_text = long_to_bytes(plaintext).decode('latin-1')
flag_start = decoded_text.find("CODEBY")
print(decoded_text[flag_start:])
```

<details>
  <summary>Flag</summary>
  
  > `CODEBY{1_know_th4T_I5_The_HARD3sT_t4SK_YOu'wE_ev3R_SeeN}`
  
</details>

<br>

### Family

<details>
  <summary>Description</summary>
  
  > [null]
  
  > Flag Format: CODEBY{}
  
</details>

Given a challenge [file](https://github.com/nopedawn/CTF/blob/main/CodebyGameCTF23/Family/family.txt) containing a message that has been encoded in 5 types of encoding

> hex = `43 4F 44 45` <br>
> 
> binary = `01000010 01011001 01111011` <br>
> 
> octal = `167 60 167 137 167 150 60 154 63 137` <br>
> 
> decimal = `102 97 109 49 108 121 95 116 48 95` <br>
> 
> unicode = `U+67 U+61 U+74 U+68 U+33 U+72 U+7D` <br>

Here's the solver

```python3
message = "43 4F 44 45 01000010 01011001 01111011 167 60 167 137 167 150 60 154 63 137 102 97 109 49 108 121 95 116 48 95 U+67 U+61 U+74 U+68 U+33 U+72 U+7D"
message_list = message.split()

decoded_hex = "".join([chr(int(x, 16)) for x in message_list[0:4]])
decoded_binary = "".join([chr(int(x, 2)) for x in message_list[4:7]])
decoded_octal = "".join([chr(int(x, 8)) for x in message_list[7:17]])
decoded_decimal = "".join([chr(int(x)) for x in message_list[17:27]])
decoded_unicode = "".join([chr(int(x[2:], 16)) for x in message_list[27:]])

flag = decoded_hex + decoded_binary + decoded_octal + decoded_decimal + decoded_unicode
print(flag)
```

<details>
  <summary>Flag</summary>
  
  > `CODEBY{w0w_wh0l3_fam1ly_t0_gath3r}`
  
</details>

<br>

### Girl with a secret

<details>
  <summary>Description</summary>
  
  > [null]
  
  > Flag Format: CODEBY{}
  
</details>

Given a challenge in the form of a png [file](https://github.com/nopedawn/CTF/blob/main/CodebyGameCTF23/Girl_with_a_secret/task.png)

We checked the metadata of the file and found nothing suspicious

```bash
$ exiftool task.png
ExifTool Version Number         : 12.40
File Name                       : task.png
Directory                       : .
File Size                       : 887 KiB
File Modification Date/Time     : 2023:04:18 03:46:24+07:00
File Access Date/Time           : 2023:04:21 17:13:54+07:00
File Inode Change Date/Time     : 2023:04:21 17:12:30+07:00
File Permissions                : -rwxrwxrwx
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 1350
Image Height                    : 1800
Bit Depth                       : 8
Color Type                      : RGB with Alpha
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
Image Size                      : 1350x1800
Megapixels                      : 2.4
```

Then we checked the string contents and found no clue at all `$ strings task.png`

How about trying with `zsteg` maybe there is some hidden LSB data inside it, and there's it

```bash
$ zsteg task.png
b1,rgb,lsb,xy       .. text: "50:codeby{Be_c4r3FULL_NExT_TIMe_WIth_trAps_L1KE_Th1s}?"
b1,bgr,lsb,xy       .. file: OpenPGP Secret Key
b3,abgr,msb,xy      .. file: MPEG ADTS, layer I, v2, 256 kbps, Monaural
b4,b,msb,xy         .. file: MPEG ADTS, layer I, v2, 112 kbps, 24 kHz, JntStereo
```

<details>
  <summary>Flag</summary>
  
  > `codeby{Be_c4r3FULL_NExT_TIMe_WIth_trAps_L1KE_Th1s}`
  
</details>

<br>

### Earth hum

<details>
  <summary>Description</summary>
  
  > [null]
  
  > Flag Format: CODEBY{}
  
</details>

Given a challenge of a `15:36` minute WAV audio file, first we check the metadata

```bash
$ exiftool earth.wav
ExifTool Version Number         : 12.40
File Name                       : earth.wav
Directory                       : .
File Size                       : 158 MiB
File Modification Date/Time     : 2023:04:11 04:49:34+07:00
File Access Date/Time           : 2023:04:23 19:16:28+07:00
File Inode Change Date/Time     : 2023:04:21 17:29:19+07:00
File Permissions                : -rwxrwxrwx
File Type                       : WAV
File Type Extension             : wav
MIME Type                       : audio/x-wav
Encoding                        : Microsoft PCM
Num Channels                    : 2
Sample Rate                     : 44100
Avg Bytes Per Sec               : 176400
Bits Per Sample                 : 16
Title                           : Nearer My God To Thee
Product                         : Back To Titanic
Artist                          : I Salonisti
Date Created                    : 1998
Genre                           : Soundtrack
Track Number                    : 07
ID3 Size                        : 135
Warning                         : Invalid ID3 frame size
Duration                        : 0:15:37
```

We can use audio analysis tools such as Audacity, Sonic Visualizer, etc.

In Sonic Visualizer, open the Ribbon `Pane > Add Spectogram > Channel 2` and analyze each audio visual

We discovered a line at `1:24 - 1:32` we assume as Morse code after listening to it

<img src="https://raw.githubusercontent.com/nopedawn/CTF/main/CodebyGameCTF23/Earth_hum/1.png"><br>

Then, decode and compare the Morse code using these two websites

[https://morsedecoder.com/](https://morsedecoder.com/)

<img src="https://raw.githubusercontent.com/nopedawn/CTF/main/CodebyGameCTF23/Earth_hum/2.png"><br>

[https://morsecode.world/international/decoder/audio-decoder-adaptive.html](https://morsecode.world/international/decoder/audio-decoder-adaptive.html)

<img src="https://raw.githubusercontent.com/nopedawn/CTF/main/CodebyGameCTF23/Earth_hum/3.png"><br>

<details>
  <summary>Flag</summary>
  
  > `CODEBY{IT1SV3RYS4D}`
  
</details>

<br>

### Runes

<details>
  <summary>Description</summary>
  
  > [null]
  
  > Flag Format: CODEBY{}
  
</details>

Given a challenge of an image file, containing ancient text which we found through googling to be a Runic Cipher or [Elder Futhark Decoder](https://www.dcode.fr/elder-futhark).

<br>
<div style="text-align:center">
<img src="https://raw.githubusercontent.com/nopedawn/CTF/main/CodebyGameCTF23/Runes/task.jpg" width="300">
</div>
<br>

Let's decode it, and here's the result:

<img src="https://raw.githubusercontent.com/nopedawn/CTF/main/CodebyGameCTF23/Runes/1.png"><br>

For the letter **J**, it's actual pronunciation may be **Y**, but the alphabet used is the same, so I will use this.

<br>
<div style="text-align:center">
<img src="https://i.pinimg.com/originals/34/72/75/3472752055a82e98320d21bbb573a3db.jpg" width="300">
</div>
<br>

<details>
  <summary>Flag</summary>
  
  > `CODEBY{runes_will_make_you_strong}`
  
</details>

<br>

### Favorite animated series

<details>
  <summary>Description</summary>
  
  > [null]
  
  > Flag Format: CODEBY{}
  
</details>

Given a challenge of an image file, containing random text which we found through googling to be a [Bill Cipher Alphabet](https://www.dcode.fr/gravity-falls-bill-cipher) *(from Gravity Fall's)*

<img src="https://raw.githubusercontent.com/nopedawn/CTF/main/CodebyGameCTF23/Favorite_animated_series/task.jpg"><br>

<img src="https://raw.githubusercontent.com/nopedawn/CTF/main/CodebyGameCTF23/Favorite_animated_series/1.png"><br>

<details>
  <summary>Flag</summary>
  
  > `CODEBY{insmallregister}`
  
</details>