From `airgeddon>=9.0` a new options system is available. It is based on bash fallback substitution environment vars. Options can be set in three different ways:

#### 1. From the options hidden file called as `.airgeddonrc` usually located in the same dir as the main script. For some distros like Pentoo located at `/etc/airgeddonrc`.

Any variable available on this file can be changed to alter the behavior of the script. Changes on this file will take effect on next launch.

 - Examples

Modifying the file with these settings will disable all colorization and the ascii intro animation will be skipped on next launch.
```
AIRGEDDON_BASIC_COLORS=false
AIRGEDDON_SKIP_INTRO=true
```

#### 2. Using "_on the fly_" flags on command line

The changes on the options set on the command line will apply only for that session and they will override the settings on `.airgeddonrc` file.

 - Examples

Setting these flags on the command line, there will be no updates and 5Ghz will be disabled on next launch.
```
~/airgeddon# AIRGEDDON_AUTO_UPDATE=false AIRGEDDON_5GHZ_ENABLED=false bash airgeddon.sh
```
 
#### 3. From the options menu

Any change done from the menu is applied instantly excepting a couple of them (airgeddon will remind you about a reboot of the tool required). No examples required, menus are intuitive.

## List of available options

```
#Enabled true / Disabled false - Auto update feature (it has no effect on development mode) - Default value true
AIRGEDDON_AUTO_UPDATE=true

#Enabled true / Disabled false - Skip intro (it has no effect on development mode) - Default value false
AIRGEDDON_SKIP_INTRO=false

#Enabled true / Disabled false - Allow colorized output - Default value true
AIRGEDDON_BASIC_COLORS=true

#Enabled true / Disabled false - Allow extended colorized output (ccze tool needed, it has no effect on disabled basic colors) - Default value true
AIRGEDDON_EXTENDED_COLORS=true

#Enabled true / Disabled false - Auto change language feature - Default value true
AIRGEDDON_AUTO_CHANGE_LANGUAGE=true

#Enabled true / Disabled false - Dependencies, root and bash version checks are done silently (it has no effect on development mode) - Default value false
AIRGEDDON_SILENT_CHECKS=false

#Enabled true / Disabled false - Print help hints on menus - Default value true
AIRGEDDON_PRINT_HINTS=true

#Enabled true / Disabled false - Enable 5Ghz support (it has no effect if your cards are not 5Ghz compatible cards) - Default value true
AIRGEDDON_5GHZ_ENABLED=true

#Enabled true / Disabled false - Force to use iptables instead of nftables (it has no effect if nftables are not present) - Default value false
AIRGEDDON_FORCE_IPTABLES=false

#Enabled true / Disabled false - Force to kill Network Manager before launching Evil Twin attacks - Default value true
AIRGEDDON_FORCE_NETWORK_MANAGER_KILLING=true

#Available values: mdk3, mdk4 - Define which mdk version is going to be used - Default value mdk4
AIRGEDDON_MDK_VERSION=mdk4

#Enabled true / Disabled false - Enable plugins system - Default value true
AIRGEDDON_PLUGINS_ENABLED=true

#Enabled true / Disabled false - Development mode for faster development skipping intro and all initial checks - Default value false
AIRGEDDON_DEVELOPMENT_MODE=false

#Enabled true / Disabled false - Debug mode for development printing debug information - Default value false
AIRGEDDON_DEBUG_MODE=false

#Available values: xterm, tmux - Define the needed tool to be used for windows handling - Default value xterm
AIRGEDDON_WINDOWS_HANDLING=xterm
```

##### About tmux usage
To run airgeddon on a headless system (without X Window or Wayland graphics system) this option (`AIRGEDDON_WINDOWS_HANDLING`) needs to be set to `tmux`. Then just run airgeddon as normal and tmux will be opened by airgeddon. No need to open tmux first. To navigate tmux windows(tabs) created by airgeddon, press `Ctrl+b` and then `n` for next window or `p` for previous window.

##### Important notes

##### These three options `AIRGEDDON_FORCE_IPTABLES`, `AIRGEDDON_DEVELOPMENT_MODE`and `AIRGEDDON_DEBUG_MODE` are special. Because their purpose is a special scenario or development, they are not present on menus to be modified. They can be set only modifying the options hidden file or using command line flags.