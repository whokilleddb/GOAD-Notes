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
Host: 192.168.56.10 ()  Ports: 53/open/tcp//domain//Simple DNS Plus/, 80/open/tcp//http//Microsoft IIS httpd 10.0/, 88/open/tcp//kerberos-sec//Microsoft Windows Kerberos (server time: 2025-07-28 09:27:14Z)/, 135/open/tcp//msrpc//Microsoft Windows RPC/, 139/open/tcp//netbios-ssn//Microsoft Windows netbios-ssn/, 389/open/tcp//ldap//Microsoft Windows Active Directory LDAP (Domain: sevenkingdoms.local0., Site: Default-First-Site-Name)/, 445/open/tcp//microsoft-ds?///, 464/open/tcp//kpasswd5?///, 593/open/tcp//ncacn_http//Microsoft Windows RPC over HTTP 1.0/, 636/open/tcp//ssl|ldap//Microsoft Windows Active Directory LDAP (Domain: sevenkingdoms.local0., Site: Default-First-Site-Name)/, 3268/open/tcp//ldap//Microsoft Windows Active Directory LDAP (Domain: sevenkingdoms.local0., Site: Default-First-Site-Name)/, 3269/open/tcp//ssl|ldap//Microsoft Windows Active Directory LDAP (Domain: sevenkingdoms.local0., Site: Default-First-Site-Name)/, 3389/open/tcp//ms-wbt-server//Microsoft Terminal Services/, 5985/open/tcp//http//Microsoft HTTPAPI httpd 2.0 (SSDP|UPnP)/, 5986/open/tcp//ssl|http//Microsoft HTTPAPI httpd 2.0 (SSDP|UPnP)/  Ignored State: closed (985)     OS: Microsoft Windows Server 2019       Seq Index: 261  IP ID Seq: Incremental
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

So we have some hostnames now. Adding them to the [[Artefacts#Network Information|Artefacts]] document.

