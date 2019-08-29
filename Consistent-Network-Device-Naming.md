For some Linux distributions like Ubuntu or Debian since some versions ago, the default naming for network devices is using the new nomenclature which is causing errors using `airgeddon`.

__How to know if I am affected?__

If you see your wireless card named as _wlx00c0ca9208dc_ or any similar name, yeah you are affected and probably you'll have some issues using `airgeddon` while changing mode of your card. It's better to have them using the classic name style (wlan0, wlan1, etc.).

__How to change them to the classic names style?__

To do that you must modify grub configuration. You should modify your `/etc/default/grub` file in order to add this `net.ifnames=0 biosdevname=0` to your `GRUB_CMDLINE_LINUX` line.

For example: `GRUB_CMDLINE_LINUX="net.ifnames=0 biosdevname=0"` or `GRUB_CMDLINE_LINUX="find_preseed=/preseed.cfg auto noprompt priority=critical locale=en_US net.ifnames=0 biosdevname=0"`. Just add `net.ifnames=0 biosdevname=0` to your existing options.

After modifying the file, execute `grub-update` and then reboot. After that, your wireless interface cards will be named again as always (wlan0, wlan1, etc.).