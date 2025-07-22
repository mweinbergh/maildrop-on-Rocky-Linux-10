# maildrop-on-Rocky-Linux-10
Building maildrop from source on Rocky Linux 10

# Building maildrop from source on Rocky Linux 10

## Install development environment

```bash
dnf -y groupinstall "Development Tools"
dnf -y install pcre2-devel libidn2-devel
```

## Courier Unicode

CUCVER=2.3.2

```
mkdir -p maildrop
cd maildrop
wget https://sourceforge.net/projects/courier/files/courier-unicode/$CUCVER/courier-unicode-$CUCVER.tar.bz2
```

### Extract

```
tar xvjf courier-unicode-$CUCVER.tar.bz2
rm -f courier-unicode-$CUCVER.tar.bz2
```

### Build

```bash
cd courier-unicode-$CUCVER
./configure --prefix=/usr --libdir=/usr/lib64
make
make install
```

## Maildrop 

MDVER=3.1.8

```
mkdir -p maildrop
cd maildrop
wget -O maildrop-$MDVER.tar.bz2 https://sourceforge.net/projects/courier/files/maildrop/$MDVER/maildrop-$MDVER.tar.bz2/download
```

### Extract

```
tar xvjf maildrop-$MDVER.tar.bz2
rm -f maildrop-$MDVER.tar.bz2
```

### Build

```
cd maildrop-$MDVER
./configure --prefix=/usr --libdir=/usr/lib64 LDFLAGS="-L/usr/lib64"
make
make install
```

### Test

```
echo | /usr/bin/maildrop -V 5 -d $(whoami)
```

<details id="bkmrk-output-maildrop%3A-cha"><summary>Output</summary>

maildrop: Changing to /root  
Message envelope sender=MAILER-DAEMON  
maildrop: Attempting .mailfilter  
maildrop: Delivering to /var/mail/root  
maildrop: Flock()ing /var/mail/root.  
maildrop: Appending to /var/mail/root.  
maildrop: Delivery complete.

</details>

## Remove development environment

```bash
dnf -y remove pcre2-devel libidn2-devel
dnf -y groupremove "Development Tools"
```
