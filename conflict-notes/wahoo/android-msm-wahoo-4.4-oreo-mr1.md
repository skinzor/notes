# 4.4.88 to 4.4.105

* `drivers/gpu/drm/msm/msm_gem_submit.c`

  * **Resolution:** Take both sides (make final diff match upstream's)

  * **Cause:** Commit [`031b02bc16ae`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=031b02bc16aeeb34c8038026cbbca1e6430c9d75) ("drm/msm: Fix potential buffer overflow issue") had to be adapted to work around the changed parameter (`struct msm_gem_address_space *aspac` instead of `struct msm_gpu *gpu`) that was introducted in commit [`231c57eeaf8e`](https://android.googlesource.com/kernel/msm/+/231c57eeaf8e10ec2a4510ffc98382ef1d7513ed) ("drm/msm: Pass the MMU domain index in struct msm_file_private").


* `drivers/media/v4l2-core/v4l2-compat-ioctl32.c`

  * **Resolution:** Take left side (discard all changes)

  * **Cause:** Commit [`93ff127ef6c7`](https://android.googlesource.com/kernel/msm/+/93ff127ef6c7a2a120f7ed843c292b3cd5dca1c2) ("v4l2: Refactor, fix security bug in compat ioctl32") rewrote the `put_user` statements with a `convert_in_user` macro, which was unexpected by commit [`04affe4e1171`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=04affe4e117169e75c4ff1f12dd30d74c9a629fc) ("media: v4l2-compat-ioctl32: Fix timespec conversion"). The former fixes the issue described by the latter (as they are by the same author).


* `drivers/mmc/core/bus.c`

  * **Resolution:** Take left side (discard all changes)

  * **Cause:** Commit [`5c65b739389f`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=5c65b739389fbc353fb42d379e9b7379cfe6d3f6) ("mmc: core: Do not leave the block driver in a suspended state") was already resolved by [`192cfe16ca57`](https://android.googlesource.com/kernel/msm/+/192cfe16ca5761bb7a5aafc016e79a21b2bd4002) ("mmc: bus: Handle error in case bus_ops suspend fails") but the latter has an extra comment block so git could not tell the fix was already present.


* `drivers/net/wireless/iwlwifi/iwl-nvm-parse.c`

  * **Resolution:** Take both sides (use mainline version)

  * **Causes:** Commit [`fc29713fa7c7`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=fc29713fa7c78fda30855444eeab2d5ea8088762) ("iwlwifi: add workaround to disable wide channels in 5GHz") was backported, ignoring the changes from commit [`57fbcce37be7`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=57fbcce37be7c1d2622b56587c10ade00e96afa3) ("cfg80211: remove enum ieee80211_band"). However, the Pixel 2 tree as it as commit [`56f601d6bb9e`](https://android.googlesource.com/kernel/msm/+/56f601d6bb9e51c3c8a79a5f40878b8d1e6ff481) ("BACKPORT: cfg80211: remove enum ieee80211_band") so we can use mainline commit [`01a9c948a093`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=01a9c948a09348950515bf2abb6113ed83e696d8) ("iwlwifi: add workaround to disable wide channels in 5GHz").


* `drivers/scsi/ufs/ufshcd.h`

  * **Solution:** Take left side (discard all changes)

  * **Cause:** Commit [`0c098158785b`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=0c098158785b5c8091c0bae3aa505060414076cc) ("scsi: ufs: add capability to keep auto bkops always enabled") is already present as commit [`9f06dddf5bee`](https://android.googlesource.com/kernel/msm/+/9f06dddf5beecbcdf36535e0e587c23aaa7785f5) ("scsi: ufs: add capability to keep auto bkops always enabled") with a different shift value.


* `kernel/power/process.c`

  * **Resolution:** Take both sides

  * **Cause:** Commit [`57caa2ad5ce3`](https://android.googlesource.com/kernel/msm/+/57caa2ad5ce35bedb7ab374a2e5b4d7adf63da2b) ("power: Adds functionality to log the last suspend abort reason.") added an include, which was not expected by commit [`90fd6738731b`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=90fd6738731b6d105fc8f04832ae17a9ac82c05c) ("sched/cpuset/pm: Fix cpuset vs. suspend-resume bugs").


* `net/wireless/nl80211.c`

  * **Resolution:** Take left side (discard conflict)

  * **Cause:** Commit [`6a6c61d8467d`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=6a6c61d8467d2dd7059b7d52773c18f8122e4f68) ("nl80211: Define policy for packet pattern attributes") did not account for commit [`3fee1ede34a6`](https://android.googlesource.com/kernel/msm/+/3fee1ede34a6c3b2dd7d816643e887c2308f6a78) ("nl80211: add feature for BSS selection support") being present.


* `sound/usb/card.c`

  * **Resolution:** Take right side (shuffle resolution)

  * **Cause:** Commit [`2ecedf5dc75b`](https://android.googlesource.com/kernel/msm/+/2ecedf5dc75bc770ec09bd2238e798063aeafc4b) ("sound: usb: Add support for parsing AudioStreaming intf for BADD devices") shuffled the function `snd_usb_create_streams`, which commit [`46c7b1fa4911`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=46c7b1fa4911a859a82575e3ffb55b34a89a222d) ("ALSA: usb-audio: Check out-of-bounds access by corrupted buffer descriptor") did not expect. Resolution is identical but has been moved into the `switch` statement to satisfy the changes made by CAF's shuffling.


# 4.4.106

* `arch/arm/include/asm/kvm_arm.h`

  * **Resolution:** Take right side (use mainline diff)

  * **Cause:** When mainline commit [`5553b142be11`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=5553b142be11e794ebc0805950b2e8313f93d718) ("arm: KVM: Fix VTTBR_BADDR_MASK BUG_ON off-by-one") was backported as commit [`a5fa9efe4e01`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=a5fa9efe4e019e1f8f213142836c84f010cc4faf) ("arm: KVM: Fix VTTBR_BADDR_MASK BUG_ON off-by-one") in the 4.4 tree, it did not expect mainline commit [`8420dcd37ef3`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=8420dcd37ef34040c8fc5a27bf66887b3b2faf80) ("arm: KVM: Make kvm_arm.h friendly to assembly code") to be here, as it was introduced in 4.5. However, it is as commit [`516f3f777e5f`](https://android.googlesource.com/kernel/msm/+/516f3f777e5fb0710f1626c79e3dacca751b8c30) ("arm: KVM: Make kvm_arm.h friendly to assembly code") so we can just use mainline's version.
