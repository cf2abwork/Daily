# Windows TCP Port Forwarding & Logging Documentation
Date : 2026/04/14

This technical guide outlines the implementation, verification, and auditing of TCP port forwarding on Windows environments.

---

## 1. Port Forwarding Configuration (Netsh)
Windows manages TCP redirection via the **IP Helper** service. These commands require **Administrator** privileges.

### Create a Forwarding Rule
Use the `v4tov4` parameter to map local IPv4 traffic to a destination IPv4 address.
```cmd
netsh interface portproxy add v4tov4 listenport=[LOCAL_PORT] listenaddress=0.0.0.0 connectport=[TARGET_PORT] connectaddress=[TARGET_IP]
```

Example
```cmd
netsh interface portproxy add v4tov4 listenaddress=172.17.13.160 listenport=31173 connectaddress=1.2.6.1 connectport=31173
```

### Show All Rules:
```cmd
netsh interface portproxy show all
```

### Remove Specific Rule:
```cmd
netsh interface portproxy delete v4tov4 listenport=[LOCAL_PORT] listenaddress=0.0.0.0
```



### Clear All Rules:
```cmd
netsh interface portproxy reset
```


## 2. Logging & Audit Procedures
Windows does not log proxy activity by default. You must enable Firewall logging to audit connection metadata.


### Check Current Logging Status
```PowerShell
Get-NetFirewallProfile | Select-Object Name, LogEnabled, LogFileName, LogAllowed
```


### Enable Traffic Logging
This command enables the recording of successful TCP connections to a physical file.
```PowerShell
Set-NetFirewallProfile -Profile Domain,Private,Public -LogAllowed True -LogFileName "C:\Windows\System32\LogFiles\Firewall\pfirewall.log"
```

### Disable Logging Command
Run the following command in an **Administrator PowerShell** session to turn off logging for Allowed connections and Dropped packets across all profiles:

```powershell
Set-NetFirewallProfile -Profile Domain,Private,Public -LogAllowed False -LogDropped False
```



