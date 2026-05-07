# ASUS_BT500_LINUX_DRIVER_FIX
This is a band-aid fix I've made with the ASUS BT-500 dongle Driver as it seems to no longer be kept up to date.

The following changes have been made to the original installer:

```
rtk_coex.c Line 321 : Replace all instances of funciton "del_timer_sync" with "timer_delete_sync".

rtk_misc.c Line 34 : Replace "#include <asm/unaligned.h>" with "#include <linux/unaligned.h>"

rtk_bt.c Line 33 : Replace "#include <asm/unaligned.h>" with "#include <linux/unaligned.h>"
```

Per Imol-ai on https://gist.github.com/ugurkankya/092552b1ed55668ce0296718d7b65fbf , "In kernel 6.16, the hci_dev::quirks integer was replaced by the hci_dev::quirk_flags bitmap, further breaking this driver." Which leads us to make further changes...

```
rtk_bt.c Line 1440 : Replace "set_bit(HCI_QUIRK_RESET_ON_CLOSE, &hdev->quirks);" with "hci_set_quirk(hdev, HCI_QUIRK_RESET_ON_CLOSE);"

rtk_bt.c Line 1458 : Replace "set_bit(HCI_QUIRK_SIMULTANEOUS_DISCOVERY, &hdev->quirks);" with "hci_set_quirk(hdev, HCI_QUIRK_SIMULTANEOUS_DISCOVERY);"
```
