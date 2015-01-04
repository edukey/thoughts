# android emu on intel device

note: to  run usually  on intel device : mac, win/lin pc
note: apps using ndk have native arm code that requires translation (lib houdini from intel)
note: ios sdk has a simulator working on x86 mac, not an full emulator

- based on full emu of cpu with os
  - google sdk qemu arm
- based on simulating an android apk app runtime (dalvik and apis), no linux inside
  - bluestacks
  - windroy
  - google app runtime on chromeos (and archon patch to run on chrome browsers with any os)
  - blackberry 10.2.1 (qnx) can run .apk
- based on virtu of an android x86 distro
  - google sdk x86 image with intel haxm (win, mac) or kvm (linux) virtu
  - jar of beans x86 image on haxm
  - android-x86 virtualbox
  - intel android x86 virtualbox
  - genymotion virtualbox
  - andy virtualbox based on genymotion vhd
  - youwave virtualbox
