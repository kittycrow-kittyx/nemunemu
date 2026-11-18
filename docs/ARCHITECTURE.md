# Architecture

Nemunemu runs in Linux userspace. It loads THX executables and translates
guest operations to the Linux interfaces available to the runtime.

```text
THX1 / THX2          #!thistle:<command>
     |                       |
 guest execution      compatibility applet
     |                       |
     +------ Linux ABI ------+
                |
          Linux kernel
```

THX loading validates the executable and creates machine state for its
instruction profile. Compatibility applets handle the supported script
markers. Both paths use the supplied filesystem and Linux process services.

When launched as Linux init, Nemunemu supervises and reaps its shell process.
Root mounting, kernel construction and host integration are responsibilities
of the boot environment, not this runtime. The pinned Thistle checkout is
used to generate opcode and syscall definitions; see [development](DEVELOPMENT.md).

`uname` reports the running Linux kernel identity.
