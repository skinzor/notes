# 3.18.70 to 3.18.87

* `drivers/media/v4l2-core/v4l2-compat-ioctl32.c`

  * **Resolution:** Take left side (discard all changes)

  * **Cause:** Commit [`b9c210ed25a2`](https://android.googlesource.com/kernel/msm/+/b9c210ed25a2fdb7e0ac73a36571b164213e1933) ("v4l2: Refactor, fix security bug in compat ioctl32") rewrote the `put_user` statements with a `convert_in_user` macro, which was unexpected by commit [`6b3412ff9661`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=6b3412ff96615bab06863c00c371b5601e3b1e1c) ("media: v4l2-compat-ioctl32: Fix timespec conversion"). The former fixes the issue described by the latter (as they are by the same author).


* `net/packet/af_packet.c`

  * **Resolution:** Take right side (make final diff match upstream's)

  * **Cause:** Commit [`008ba2a13f2d`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=008ba2a13f2d04c947adc536d19debb8fe66f110) ("packet: hold bind lock when rebinding to fanout hook") was slightly modified for 3.18 as commit [`e4ffdf9ead59`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=e4ffdf9ead59a909f2824a4270356909d6d64380) ("packet: hold bind lock when rebinding to fanout hook") because commit [`d199fab63c11`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=d199fab63c11998a602205f7ee7ff7c05c97164b) ("packet: fix races in fanout_add()") is missing from 3.18. However, it is present in this tree as commit [`de0f20edf203`](https://android.googlesource.com/kernel/msm/+/de0f20edf203b949ae8b0d1cebd8618f7c636f77) ("UPSTREAM: packet: fix races in fanout_add()") so use the upstream resolution.
