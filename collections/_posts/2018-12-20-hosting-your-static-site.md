---
title: A Linux Command Cheat Sheet
date: 2020-06-23T06:55:14.009Z
---
### Various commands ran on a somewhat regular or an infrequent basis on Cent OS

Change existing directory symbolic links  
`ln -sfn /directory /symboliclink`

Find world-writable and sticky bit stuff at the current directory and sub-directories  
`find . -xdev -type d ( -perm -0002 -a ! -perm -1000 ) -print
//directories`

`find . -xdev -type f ( -perm -0002 -a ! -perm -1000 ) -print
//files`

Finding stuff with no owner, checking everything  
`find / -xdev ( -nouser -o -nogroup ) -print`

Finding which files contain an occurrence of a string at the current directory and sub-directories  
`find . -type f -print0 | xargs -0 grep -l localhost
//localhost is what I'm looking for`

Finding which files of a certain name that contain an occurrence of a string at the current directory and sub-directories  
`find . -type f -name "*.php" -print0 | xargs -0 grep -l localhost
//localhost is what I'm looking for`

Changing permissions on all files at the current directory and sub-directories  
`find . -type f -print0 | xargs -0 chmod 660`

Changing permissions on all directories at the current directory and sub-directories  
`find . -type d -print0 | xargs -0 chmod 771`

Get used storage space in human-readable format  
`df -h`

Use Yum to download updates only (need yum-downloadonly package installed)  
yum update -y --downloadonly

### Commands used less frequently

Get disk drive information including disk name  
`fdisk -l`

Show which scheduler a particular disk is using  
`cat /sys/block/sda/queue/scheduler
// disk sda is the disk in question`

Put inside /etc/rc.d/rc.local to change the scheduler to noop on startup for disk sda  
`echo noop > /sys/block/sda/queue/scheduler`

For finding cron jobs of all users  
`for user in $(cut -f1 -d: /etc/passwd); do echo $user; crontab -u $user -l; done`

Seeing what processes are listening on what port and address  
`ss -plnt`

Using OpenSSL to very a certificate  
`openssl x509 -in public.wtdecisionsystems.com.crt -text -noout`

Using OpenSSL to verify a private key  
`openssl rsa -in public.wtdecisionsystems.com.key -check -text -noout`

Using OpenSSL to verify PKCS12 (p12)  
`openssl pkcs12 -info -in public.wtdecisionsystems.com.p12`

Using OpenSSL to convert p12 to pem  
`openssl pkcs12 -in public.wtdecisionsystems.com.p12 -out public.wtdecisionsystems.com.pem -nodes`

Combining certs and key into a p12 file  
`openssl pkcs12 -inkey key.pem -in certificate.pem -export -out certificate.p12`