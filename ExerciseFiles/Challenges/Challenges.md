# Hashcat Practical Challenges 

These challenges are part of the course [Hashcat Essential Training](https://www.linkedin.com/learning/hashcat-essential-training) from LinkedIn Learning.

## 1. Recover a Linux user password from /etc/shadow

Linux stores hashed passwords in a file called `/etc/shadow`, which is readable by root and sudoers.

Recover the password from this user account, which we have found on an old Linux server.

Use the information in the file `1_shadowfile`, which also appears below.

```
tjenkins:$6$zERpxPslVMtvlcRl$3usJ370mtl8tO/.gwkcWtD7coH1pqEiXF67rzp7Q1lYrmqrMqvBaHG7V/Q9pd52DZ7bmu87ubvVPpm6VIdai9/:20125:0:99999:7:::
```

#### A note about modern Linux password hashes

Modern Linux distributions use Yescrypt hashes to store passwords. These can be recovered using John the Ripper (`john --format=crypt userinfo.txt`)

```
asmith:$y$j9T$oQa1Qx5iJ8rgMVz8EMmFX1$bqH9EnSkGzG4EZP2B.Rjh5Usyp/YxfG4WxwOOAry1f3:20139:0:99999:7:::
bliu:$y$j9T$ehNx4nYNHW30aI3Bo316o/$/Dk1vxUyR9ZIRJ/k9IzJbgqUNCiHsNQf4V/xT5bqSgC:20175:0:99999:7:::
```

## 2. Recover an Apache web server password

Access to an Apache HTTP Server can be provided by generating a username and password for each user using the `htpasswd` utility. 

Recover the password from this username/password pair, which is from an internal corporate web server.

Use the information in the file `2_htpasswd`, which also appears below.

```
webadmin:$2y$05$JGL/38Tl172CMONue.cRveSs1VleGhtPkmN.qQZtS7yNQChwMXCTe
```

## 3. Recover a Linux (GRUB) boot password

The GRUB boot loader on Linux systems can be secured with a password, preventing the system from starting up until the password is entered. This password is represented by a hash in a GRUB configuration file.

Imagine that we are performing an audit of servers, and we have discovered that the boot password is missing from our records for one server.

Our organization uses a specific pattern to generate these boot passwords, and we know some of the information about the password already:
* Passwords are 11 characters long
* The first three characters represent the datacenter where the server is located (in this case, `LAX`)
* The next four characters are the last four characters of the system's primary MAC address (in this case, `b8e3`)
* The next two characters are random letters (uppercase or lowercase)
* The final two characters are random digits

With these details, recover the full boot password for this system.

Use the information in the file `3_grub_40_custom`, which also appears below.

```
set superusers="admin"
password_pbkdf2 admin grub.pbkdf2.sha512.10000.C58B44C4AD5BCF9E16248D9E0B9E370C9C1EAA6A34D6B4ADE67F3DE7B95E4F15146091F255FD8729F8BBC973FD6F341CE4BE15A9CD8BBF375B96EC835A41B7BD.1C353878309790D0F8E8B6AAC7D3E76CB7A0B3E78651EF098FE06D7896C9E37252F135732688388098CF2853A0F11D9CAAAE498C5E2C3AB9CB49F0CF7C05E379
```

## 4. Recover the password for a protected PDF file

PDF files can be configured to require a password in order to view their contents. 

Imagine we received this email from our Internal Marketing Coordinator:

```
Hi!

I sent out our quarterly newsletter the other day, and people weren't able to open it. 
I'm sure I set the password to Spring2025, or maybe spring25. But, neither of those worked.
Anyway, I sent out a new copy with a corrected password after people mentioned the problem. 
Is there any way to figure out what kind of typo I made? Just curious.
I've attached the old copy here.

Thanks!
```

Recover the password from the PDF file.

Use the file `4_pdf.pdf`.