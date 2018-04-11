# CSF-Custom-Regex-for-VestaCP
Some custom regex rules to help block brute force attacks on VestaCP servers. See the example file `regex.custom.pm` if you need help.

# /etc/csf/regex.custom.pm
You must edit this file with any new custom regex patterns and place them **BEFORE** `return 0`

## proftpd

```perl
if (($lgfile eq $config{FTPD_LOG}) and ($line =~ /\[(\S+)\]\).*\(Login failed\)/)) { return ("Failed FTP login from",$1,"proftpd_ss88","5","20,21","1"); }

if (($lgfile eq $config{FTPD_LOG}) and ($line =~ /\[(\S+)\]\).*USER user: no such user found/)) { return ("Failed FTP login from",$1,"proftpd_ss88","5","20,21","1"); }
```

## vsftpd

```perl
if (($lgfile eq $config{FTPD_LOG}) and ($line =~ /FAIL LOGIN: Client \"(\S+)\"/)) { return ("Failed FTP login from",$1,"vsftpd_ss88","5","20,21","1"); }
```

## VestaCP Control Panel (8083)

You need to make sure the 'CUSTOM1_LOG' field is set to Vesta's control panel log file at: /var/log/vesta/auth.log

```perl
CUSTOM1_LOG = "/var/log/vesta/auth.log"
```

```perl
if (($globlogs{CUSTOM1_LOG}{$lgfile}) and ($line =~ /(\S+) failed to login/)) { return ("Login attempt to VestaCP from",$1,"VESTAloginAttempt","5","8083","1"); }
```
* Special thanks to moucho (https://forum.vestacp.com/viewtopic.php?f=20&t=10209&p=62062#p62062)
