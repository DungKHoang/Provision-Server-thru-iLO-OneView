# Provisioning-Server.ps1
The Provisioning-Server.ps1 script is a PowerShell script that leverages:
    * HPE iLORest cmdlets
    * HPE OneView PowerShell library 
to deploy OS to physical server thru iLO virtual Media and OneView

# Scenarios
There are two scenarios:
    * If you specify iLO IP address, the script will provision OS to physical server by directly connecting to iLO
    * If you specify OneView IP address, the script will perform the following tasks:
        ** If server has no profile, the script will apply a profile temaplte to this server
        ** The script then establishes a SSO to the iLO of the server
        ** It then deploys the OS thru virtual media

# Pre-requisites
The script requires the following HPE Libraries:
    * HPE iLORest cmdlets
    * HPE OneView PowerShell library 

If you are using a Windows Server 2012 R2 or Windows 7 machine, you need to install the Windows Management Framework v5.0


## Intalling the HPE libraries
    * HPE iLORest cmdlets 
```
    Install-Module HPRestCmdlets
```    
    * HPE OneView PowerShell library
```
    Install-Module HPOneView.310
``` 


### Syntax

There are two(2) scenarios:
    * Connecting to a server through ILO directly
```

    .\ Provision-Server.ps1 -iloIP 10.234.1.21 -iLOUser admin -iLOPassword password -isoURL "http://10.239.16.2/ISO/ubuntu-16.04.3-server-amd64.iso" 
        The script connects to the iLO and provisions server with URL provided in isoURL

        The script connects to OneView, selects the server specified in parameter and and provisions server with URL provided in isoURL


```

    * Connecting through OneView
```

        .\ Provision-Server.ps1 -OVApplianceIP 10.254.1.66 -OVAdminName Administrator -password P@ssword1 -Server "Encl1, Bay3" -ServerProfileTemplate "DL-Template" -isoURL "http://10.239.16.2/ISO/ubuntu-16.04.3-server-amd64.iso"

        The script connects to OneView, selects the server specified in parameter and enables iLO IPMI on this server

```
