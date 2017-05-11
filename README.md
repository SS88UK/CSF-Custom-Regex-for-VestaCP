# CSF-Custom-Regex-for-VestaCP
Some custom regex rules to help block brute force attacks on VestaCP servers

# /etc/csf/regex.custom.pm
You must edit this file with any new custom regex patterns and place them **BEFORE** `return 0`

## proftpd

```bash
if (($lgfile eq $config{FTPD_LOG}) and ($line =~ /\[(\S+)\]\).*\(Login failed\)/)) { return ("Failed FTP login from",$1,"proftpd_ss88","5","20,21","1"); }

if (($lgfile eq $config{FTPD_LOG}) and ($line =~ /\[(\S+)\]\).*USER user: no such user found/)) { return ("Failed FTP login from",$1,"proftpd_ss88","5","20,21","1"); }
```

## vsftpd

```bash
if (($lgfile eq $config{FTPD_LOG}) and ($line =~ /FAIL LOGIN: Client \"(\S+)\"/)) { return ("Failed FTP login from",$1,"vsftpd_ss88","5","20,21","1"); }
```
