---
title: "Cyber Havoc CTF 2023"
description: ""
summary: ""
date: 2023-04-20T08:37:00+07:00
lastmod: 2023-04-23T07:08:00+07:00
draft: false
menu:
  posts:
    parent: ""
    identifier: "cyberhavocctf-2023"
weight: 910
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

[https://ctftime.org/event/1963](https://ctftime.org/event/1963)

<br>
<p align="center">
  <a href="https://ctftime.org/event/1963" target="_blank">
    <img src="https://ctftime.org/media/cache/84/82/84822fe878efbbc1b8b9078a480016b2.png" width="200">
  </a>
</p>

### Challs
| Category            | Challenge |
| --------------------| --------- |
| Digital Forensics   | [The Cryptic Sound](#the-cryptic-sound) |
| Reverse Engineering | [Start The Dos](#start-the-dos) |
| Cryptography | [The Beginning Of All](#the-beginning-of-all) |
| Web 3.0 | [Private's been Captured](#privates-been-captured) |
| Web 3.0 | [Permission Denied](#permission-denied) |

<br>

### The Cryptic Sound

<details>
  <summary>Description</summary>
  
  > Elliot was working late at night when he suddenly heard a strange sound coming from his computer. At first, he thought it was just a glitch or some interference, but the sound kept repeating. Elliot felt a strange sense of unease and began to suspect that there might be a hidden message in the sound.
  
  > Flag Format: CHCTF{}
  
</details>

Given a WAV audio [file](https://github.com/nopedawn/CTF/blob/main/CyberHavoc23/The_Cryptic_Sound/Right%20or%20Wrong.wav) that plays strange audio when played, we assume it contains Morse code. 

We can decode it using Morse Audio Decoder website

[https://databorder.com/transfer/morse-sound-receiver/](https://databorder.com/transfer/morse-sound-receiver/)

<img src="https://raw.githubusercontent.com/nopedawn/CTF/main/CyberHavoc23/The_Cryptic_Sound/decoded.png"><br>

<details>
  <summary>Flag</summary>
  
  > `CHCTF{BONSOIRELLIOT}`
  
</details>

<br>

### Start The Dos

<details>
  <summary>Description</summary>
  
  > Leon wants you to be a part of Agents of Havoc. He wants you to understand this software as old as hacking itself so as to fire a DoS Attack against whiterose's targets. Help him before he suspects your intentions.
  
  > Flag Format: CHCTF{}
  
</details>

Given a file named [dosser.s](https://github.com/nopedawn/CTF/blob/main/CyberHavoc23/Start_The_Dos/dosser.o) we can compile it using the following commands:

```bash
$ nasm -f elf32 -o dosser.o dosser.s
$ ld -m elf_i386 -o dosser dosser.o
```

```bash
$ file dosser
dosser: ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), statically linked, not stripped
```

After that, we can reverse the dosser ELF file using IDA Disassembler 32 bit. We will find a separate flag in the text segment stored in the `al` register.

<details>
  <summary>Flag</summary>
  
  > `CHCTF{L33T_CR4CK3R_5TR1K3S_4G41N}`
  
</details>

<br>

### The Beginning Of All

<details>
  <summary>Description</summary>
  
  > I was working on my laptop when my laptop suddenly glitched. I discussed it with my friends and to our surprise we all had the same color glitch. I guess it has to do something with the odd behavior of the people around me.
  
  > Flag Format: CHCTF{}
  
</details>

Given an MP4 video [file](https://github.com/nopedawn/CTF/blob/main/CyberHavoc23/The_Beginning_Of_All/glitches.mp4) that we were able to play, I initially thought that the video was corrupted due to color issues. However, after gathering more information, I discovered that it was actually a Hexahue Alphabet code.

<br>
<div style="text-align:center">
<img src="https://omniglot.com/images/writing/hexahue.gif">
</div>
<br>

<details>
  <summary>Flag</summary>
  
  > `CHCTF{5URR3ND3R_0R_5UFF3R}`
  
</details>

<br>

### Private's been Captured

<details>
  <summary>Description</summary>
  
  > Leon just had a secret meeting with Alice. Book a SLOT with Alice see what he is upto.
  
  > Flag Format: CHCTF{}
  
</details>

In this Web3.0 (Blockchain) category challenge is presented in the form of a link resulting from an Ethereum transaction. This challenge is often encountered in the realm of Web3.0, and by clicking on **Transaction Details** we can access further information by selecting **More Details > Click to Show More > View Input As** followed by `UTF-8`.

<details>
  <summary>Flag</summary>
  
  > `CHCTF{1_kn0w_1'm_n0t_4l0n3}`
  
</details>

<br>

### Permission Denied

<details>
  <summary>Description</summary>
  
  > Cisco believes private data isn't readable. Is it so?!?!
  
  > Flag Format: CHCTF{}
  
</details>

This challenge needs to be solved the same way as before, `Input Data > View Input As > UTF-8`

<details>
  <summary>Flag</summary>
  
  > `CHCTF{C0ntract5_4re_m4de_t0_be_brok3n}`
  
</details>