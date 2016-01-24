# Virtualization

From most impact and constrains to less impacts and constrains

## Runtime

Require specific coding for a specific runtime abstracting from underlying OS

- Java JVM ; Jikes ; UI : Swing, SWT
- Dotnet CLR : DotGnu, Mono, DotnetCore ; UI : Silverlight (deprecated)
- Android : DalvikVM, ART
- many "script" envs : nodejs, python, ruby, perl (parrotVM), tcl, ...
- others : LLVM (for cross build chains) ; Dis (inferno) ; Squeak (smalltalk)
- Cloud runtimes : AppEngine, Heroku, Salesforce

## OS emulation

Need to recompile source code to bind it to the emulation libraries of the original OS to the host OS

- cygwin, mingw

## Application Container

Abstract a native OS app with an intermediate layer, between the app and the OS, that mimic the OS.
This allow to get fine grained control, for example over I/Os (disk access, network usage) over any application.
This usually require to repackage (but not recompile) the application binaries to make it use the container.

https://en.wikipedia.org/wiki/Application_virtualization

- Windows Desktop : Cameyo, Citrix XenApp, VMWare ThinApp, Symantec Workspace, MS App-V
- Windows server : Citrix Xen, VxWorks
- Linux : KVM, CoLinux, LXC
- Docker Engine ; first on linux using KVM (namespaces, cgroups),  and then windows using specially built new kernel features from win2016server
- Bluestacks ??
- Solaris Zones


## Any OS on same cpu

The VM rely on underlying cpu to directly execute cpu code, so it must be the same cpu architecture as the host.

### Intel x86

- VMWare : 
- VirtualBox : 
- VirtualPC : replaced by Hyper-V since Win8
- Hyper-V : 
- Vagrant

## Any archi

The VM emulate other cpu architecture, usually very slow

https://en.wikipedia.org/wiki/Comparison_of_platform_virtualization_software, 
https://en.wikipedia.org/wiki/List_of_emulators

- QEmu, Bochs, SIMH, Simics
- Mame
