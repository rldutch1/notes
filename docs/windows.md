####Check what programs need to be upgraded:
<span style="color: #3366ff;">winget upgrade</span><br />

####Upgrade all programs that need to be upgraded:
<span style="color: #3366ff;">winget upgrade --all</span><br />

####MSC Files and Program Definition:
<span style="color: #3366ff;">
  DevModeRunAsUserConfig.msc - DevModeRunAsUserConfig<br />
  WmiMgmt.msc - Windows Management Interface Management<br />
  adsiedit.msc - Actice Directory Services Interface Management<br />
  azman.msc - Authorization Manager<br />
  certlm.msc - Certificates (Local Computer)<br />
  certmgr.msc - Certificate Manager<br />
  certsrv.msc - Certificate Service<br />
  comexp.msc - Component Services<br />
  compmgmt.msc - Component Manager<br />
  devmgmt.msc - Device Manager<br />
  devmoderunasuserconfig.msc <br />
  diskmgmt.msc - Disk Management<br />
  dnsmgmt.msc - DNS Management<br />
  eventvwr.msc - Event Viewer<br />
  fsmgmt.msc - File System Management<br />
  gpedit.msc - Group Policy Editor<br />
  gpmc.msc - Group Policy Management Console<br />
  iis.msc - Internet Information Services<br />
  iis6.msc - Internet Information Services 6<br />
  lusrmgr.msc - Local User Manager<br />
  nfsmgmt.msc - NFS Managment<br />
  perfmon.msc - Performance Monitor<br />
  printmanagement.msc - Print Managment<br />
  rsop.msc - Resultant Set of Policy<br />
  secpol.msc - Security Policy<br />
  services.msc - Services<br />
  taskschd.msc - Task Scheduler<br />
  tpm.msc - Trusted Platform Module<br />
  wf.msc - Windows Firewall<br />
  wsus.msc - Windows Software Update Services<br />
</span>

####Shutdown a computer from the commandline:

Old School:<br />
<span style="color: #3366ff;"><br />
shutdown -m \\TargetComputer -r -t 0 -f & ping TargetComputer -t<br />
or<br />
runas /noprofile /user:BHS\a-rlholland "shutdown -m \\TargetComputer -r -t 0 -f" & ping TargetComputer -t<br />
</span><br />
<br />
New School:<br />
Event Viewer Data for shutdown:<br />
Level=Information; Event ID=1074; Source=User32<br />
<span style="color: #3366ff;"><br />
shutdown /m \\TargetComputer /c "incident#_or_message" /d p:4:1 /r /t 0 /f & ping TargetComputer -t<br />
or<br />
runas /noprofile /user:BHS\a-rlholland "shutdown /m \\TargetComputer /c \"incident#_or_message\" /d p:4:1 /r /t 0 /f" & ping TargetComputer -t<br />
</span><br />
<br />
From Administrator Command Prompt:<br />
<span style="color: #3366ff;"><br />
net use A: \\TargetComputer\c$<br />
</span><br />
<br />
Remember to Flush and Register the computer in DNS.<br />
<span style="color: #3366ff;"><br />
Tucson DNS 10.109.0.202 (TUSNS01) and 10.109.64.202 (TUSNS02) are the ones to use.<br />
runas /noprofile /user:BHS\a-rlholland "ipconfig /flushdns"<br />
runas /noprofile /user:BHS\a-rlholland "ipconfig /registerdns"<br />
</span><br />
<br />
Map a drive letter to Microsoft OneDrive.<br />
<span style="color: #3366ff;"><br />
@echo off<br />
REM ----------------------------------------------------------------------------<br />
REM Author: Robert Holland<br />
REM Name: MapH.cmd<br />
REM Creation Date: Thu Oct 14 2021 08:53:25 GMT-0700 (US Mountain Standard Time)<br />
REM Last Modified:<br />
REM Copyright (c)2021<br />
REM Purpose: Locally Map H: drive to OneDrive<br />
REM ----------------------------------------------------------------------------<br />
<br />
subst H: "C:\Users\%username%\OneDrive\"<br />
</span>


Run a command that causes all files and folders beginning with a period (to include period-underscore files) to become invisible, open Command Prompt, then run this:
<span style="color: #3366ff;"><br />attrib +H J:\.* /S /D</span> (but be sure to change the drive from J: to the drive letter of your choice)<br />
Note that this attrib option will run through every file and folder on your drive, so this could take quite a long time, depending on the size of your disk.<br />
