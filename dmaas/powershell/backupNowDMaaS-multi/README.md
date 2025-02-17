# Backup DMaaS Objects Now using PowerShell

Warning: this code is provided on a best effort basis and is not in any way officially supported or sanctioned by Cohesity. The code is intentionally kept simple to retain value as example code. The code in this repository is provided as-is and the author accepts no liability for damages resulting from its use.

This powershell script starts a backup of protected objects in DMaaS.

**Note:** This script is a work in progress. If you find something that doesn't work, please contact your Cohesity representative.

## Download the script

Run these commands from PowerShell to download the script(s) into your current directory

```powershell
# Download Commands
$scriptName = 'backupNowDMaaS-multi'
$repoURL = 'https://raw.githubusercontent.com/bseltz-cohesity/scripts/master'
(Invoke-WebRequest -UseBasicParsing -Uri "$repoUrl/dmaas/powershell/$scriptName/$scriptName.ps1").content | Out-File "$scriptName.ps1"; (Get-Content "$scriptName.ps1") | Set-Content "$scriptName.ps1"
(Invoke-WebRequest -UseBasicParsing -Uri "$repoUrl/powershell/cohesity-api/cohesity-api.ps1").content | Out-File cohesity-api.ps1; (Get-Content cohesity-api.ps1) | Set-Content cohesity-api.ps1
# End Download Commands
```

## Components

* backupNowDMaaS-multi.ps1: the main powershell script
* cohesity-api.ps1: the Cohesity REST API helper module

Place both files in a folder together and run the main script like so:

```powershell
./backupNowDMaaS-multi.ps1 -region us-east-2 -objectName myvm1, myvm2
```

## Parameters

* -username: (optional) used for password storage only (default is 'DMaaS')
* -region: DMaaS region to use
* -objectName: (optional) one or more names of protected objects to backup (comma separated)
* -objectList: (optional) text file of object names to backup (one per line)
* -fullBackup: (optional) perform full backup (default is incremental backup)
* -debugmode: (optional) display JSON output for troubleshooting

## Authenticating to DMaaS

DMaaS uses an API key for authentication. To acquire an API key:

* log onto DMaaS
* click Settings -> access management -> API Keys
* click Add API Key
* enter a name for your key
* click Save

Immediately copy the API key (you only have one chance to copy the key. Once you leave the screen, you can not access it again). When running a DMaaS compatible script for the first time, you will be prompted for a password. Enter the API key as the password.
