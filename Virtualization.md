# Virtualization

From most impacts and constrains on sources & host, to less impacts and constrains

## Runtime

Require specific coding for a specific runtime abstracting from underlying OS (usually OS agnostic)

- Java JVM ; JikesVM ; UI : Swing, SWT, AWT, JavaFX
- Dotnet CLR : DotGnu, Mono, DotnetCore ; UI : Silverlight (deprecated)
- WinRT with winrt apps, the runtime gives limited/controlled access to disk and other OS resources
- Android : DalvikVM, ART : runtime gives limited access to underlying linux resources
- many "script" envs : nodejs, python, ruby, perl (parrotVM), tcl, ...
- others : LLVM (for cross build chains) ; Dis (inferno) ; Squeak (smalltalk)
- Cloud runtimes : AppEngine, Heroku, Salesforce (apex lang), Azure Workers

## OS emulation

Need to recompile existing OS specific source code to bind it to the emulation libraries of the original OS to the host OS

- linux to windows : cygwin, mingw
- windows to linux : wine

## Application Container

Abstract a native OS app with an intermediate layer, between the app and the OS, that mimic the OS.
This allow to get fine grained control, for example over I/Os (disk access, network usage) over any application.
This usually require to repackage (but not recompile) the application binaries to make it use the container.

https://en.wikipedia.org/wiki/Application_virtualization, https://en.wikipedia.org/wiki/Operating-system-level_virtualization

- Windows Desktop : Cameyo, Citrix XenApp, VMWare ThinApp, Symantec Workspace, MS App-V, Sandboxie, Spoon
- Windows server : Citrix Xen, VxWorks
- Linux : KVM, CoLinux, LXC
- Docker Engine for Linux using KVM (namespaces, cgroups)
- Docker Engine for windows using specially built new kernel features from win2016server
- Bluestacks ?? mixing various levels of virtualization to be both performant and still complete
- Solaris Zones

### can use other versions of core libraries

- Docker Linux : can use other versions of libc.so a other core but non kernel libs

## Any OS on same cpu

The VM rely on underlying cpu to directly execute cpu code, so it must be the same cpu architecture as the host.

### Intel x86

- VMWare : 
- VirtualBox : 
- VirtualPC : replaced by Hyper-V since Win8
- Hyper-V : 
- Server Hypervisors : VMWare vSphere, Citrix XenApp, MS Hyper-V Server, Proxmox

## Any archi

The VM emulate other cpu architecture, usually very slow

https://en.wikipedia.org/wiki/Comparison_of_platform_virtualization_software, 
https://en.wikipedia.org/wiki/List_of_emulators

- QEmu, Bochs, SIMH, Simics
- Mame
