# Solutions for Practical Challenges

Below are my solutions and recovered passwords for the challenges provided in *Hashcat Essential Training* from LinkedIn Learning. I have also provided code to generate your own hashes.

## Challenge 1: Linux User Password

```sh
# Generate a hash with an interactively-provided password
openssl passwd -6
```

```sh
# My solution using hashcat
hashcat -m 1800 Challenges/1_hash -a 0 ~/SecLists/Passwords/Leaked-Databases/* -O -S -o 1_result.txt
```

```
# Result
$6$zERpxPslVMtvlcRl$3usJ370mtl8tO/.gwkcWtD7coH1pqEiXF67rzp7Q1lYrmqrMqvBaHG7V/Q9pd52DZ7bmu87ubvVPpm6VIdai9:@dmin1234
```

```
# Yescrypt results with john --format=crypt hashfile
$y$j9T$oQa1Qx5iJ8rgMVz8EMmFX1$bqH9EnSkGzG4EZP2B.Rjh5Usyp/YxfG4WxwOOAry1f3:a1b2c3
$y$j9T$ehNx4nYNHW30aI3Bo316o/$/Dk1vxUyR9ZIRJ/k9IzJbgqUNCiHsNQf4V/xT5bqSgC:@dm1n678
```
## Challenge 2: Apache HTTP Server password

```sh
# Generate a hash with an interactively-provided password
htpasswd -B -c outputfile username
```

```sh
# My solution using hashcat
hashcat -m 3200 Challenges/2_htpasswd --username -a 0 ~/SecLists/Passwords/common_corporate_passwords.lst -r ~/hashcat/rules/rockyou-30000.rule --stdout -o 2_result.txt
```

```
# Result
$2y$05$JGL/38Tl172CMONue.cRveSs1VleGhtPkmN.qQZtS7yNQChwMXCTe:Spring2025
```

## Challenge 3: Linux GRUB password

```sh
# Generate a hash with an interactively-provided password
grub-mkpasswd-pbkdf2
```

```sh
# My solution using hashcat and provided information (LAXb8e3....)
hashcat -m 7200 Challenges/3_hash -a 3 -1 ?l?u LAXb8e3?1?1?d?d -S -o 3_result.txt
```

```
# Result
grub.pbkdf2.sha512.10000.C58B44C4AD5BCF9E16248D9E0B9E370C9C1EAA6A34D6B4ADE67F3DE7B95E4F15146091F255FD8729F8BBC973FD6F341CE4BE15A9CD8BBF375B96EC835A41B7BD.1C353878309790D0F8E8B6AAC7D3E76CB7A0B3E78651EF098FE06D7896C9E37252F135732688388098CF2853A0F11D9CAAAE498C5E2C3AB9CB49F0CF7C05E379:LAXb8e3Mt82
```

## Challenge 4: Password-protected PDF

Tools that can generate PDF files provide the ability to protect them with passwords. In this case, I used Microsoft Word on macOS to create and protect the PDF file.

```sh
# My solution using hashcat
hashcat -m 10500 Challenges/4_hash -a 3 -1 Ss ?1pring?d?d?d?d?d?d -i -S -o 4_result.txt
```

```
# Result
$pdf$4*4*128*-4*1*16*57ad4189ddab005763554826ce3e283f*32*22129a4f22e48a0ceee56c8e0a853f0900000000000000000000000000000000*32*618cd781e555621e9492d228a5c4637573b41fcaaeda52c4c3fd52c53f28c86c:Spring20205
```
