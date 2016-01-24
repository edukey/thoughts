# Virtualization

## Runtime

Require specific coding for a specific runtime abstracting from underlying OS

- Java ; UI : Swing, SWT
- Dotnet CLR : Dotnet Core ; UI : Silverlight (deprecated)
- DalvikVM
- many "script" envs : nodejs, python, ruby, perl, tcl, ...

## Application

Abstract a native OS app with an intermediate layer between the app and the OS that mimic the OS

https://en.wikipedia.org/wiki/Application_virtualization

- windows UI apps : Cameyo, Citrix XenApp, VMWare ThinApp, Symantec Workspace, MS App-V
- Linux KVM
- Docker Engine (first linux and then windows)
- Bluestacks ??

## Any OS on same archi

### Intel x86

- VMWare : 
- VirtualBox : 
- VirtualPC : replaced by Hyper-V since Win8
- Hyper-V : 
- Vagrant

## Any archi

- QEmu
