## Section still under construction

This section is to clarify the typical problems and some common doubts as well. Here you can find answers for them. Remember that you can join to our Discord channel clicking on the [Public Invitation link](https://discord.gg/sQ9dgt9).

____

## Common problems and doubts

#### My fake AP is not working on any Evil Twin attack. Why?

You should see on fake AP hostapd (xterm upper left) window "AP-ENABLED". If you can see "AP-DISABLED", then something went wrong.

Probably the chipset of your card is not compatible or you have one of the "blacklisted" cards with known problems (mainly Realtek RTL chipsets). Check the list of fully working cards and the cards with known problems [on this link](https://github.com/v1s1t0r1sh3r3/airgeddon/wiki/Cards%20and%20Chipsets).

#### DoS is not working, what can I do?

First of all you must be sure about that. Sometimes is hard to detect that is not working. The best option is to check on your own network before perform the real audit and make some tests. Anyway, Denial Of Service is tricky, it is not an exact science.

Not all attacks are working for all APs and for all clients. Sometimes only some clients are taken down while others are unaffected on the same AP. It depends of many factors and variables: Chipset used to perform the attack, kind of client (Android, computer, Apple device, etc), Access Point, distance and signal to the target, etc. This last is very important, the signal needs to be powerful. If you think it is not working, you should try another different attack: mdk4, aireplay or even mdk3 modifying the configuration options ".airgeddonrc" file. More info about the available options [on this link](https://github.com/v1s1t0r1sh3r3/airgeddon/wiki/Options).

#### Can be the Evil Twin Captive Portal page be customized? how?

Yeah it can be done to perform a more tailored attack over the wireless network you are auditing. There are two ways to do this.

The captive portal page files (html, css and js) are created during the attack in `/tmp/www` dir. You can get that files, perform an offline customization and then when they are ready, launch the attack again and while the attack is running, copy your customized files to that `/tmp/www` location to overwrite the existing ones. The portal will look with your custom web page.

The second (more elegant) method is to create a plugin to perform this task. You can hook the _set_captive_portal_page_ function overriding the content to create your custom webpage. Just fill the plugin template file (plugin_template.sh) in plugins dir. More info about plugin creation [on this link](https://github.com/v1s1t0r1sh3r3/airgeddon/wiki/Plugins%20System).

#### Once connected to the Evil Twin fake network, captive portal is not triggered. What am I doing wrong?

Once connected to the fake network, it depends of the type of your device. On mobile devices (Android and Apple iOS) it should be triggered automatically showing a push notification.

Then (for standard computers and mobile devices), opening a browser and trying to open a page should make the captive portal to be opened while you don't try to open a SSL page. If you try to open a page that starts with "https" or if you try a very famous page like Google, Facebook or similar (they are opened using SSL by default even if you don't type https) it will not work and is completely normal. You must try to open "http" pages.

The reason for this behavior is that to trigger captive portal for SSL pages, a SSL certificate is needed at the portal. And the free self-signed certificates are not an option due the warning messages they generate when a page using them is visited. The free Let's encrypt 90 days valid SSL certificate is not also an option due the constant need of renewal and the maintenance it needs. So airgeddon staff decided to let it as is. It's better to have a "page not shown" error than a "warning unsecure page" message shown because of a self-signed SSL certificate.

#### What is DoS Pursuit Mode exactly?

During a standard Evil Twin attack, your wireless physical card is splitted into two logical interfaces. One to create the fake Access Point and another to perform the DoS in monitor mode. During the attack, if the target AP is configured in channel "Auto" and the victim reset it due the lack of connectivity because of the DoS attack, once rebooted, it may switch to another channel letting our attack performing DoS over a wrong channel and the victim will recover the connectivity.

To avoid the situation explained before, airgeddon implemented the DoS Pursuit Mode. To enable this mode for Evil Twin attacks you'll need an additional (a second one) compatible to monitor mode wireless card. The first card will be used as normal and the second one will be used to scan in background looking for the target AP. If the situation described before happens and the target AP switch its channel, it will be detected by airgeddon and it will re-launch the DoS over the new channel alerting us about this. In this way, the target AP is "pursued" even on channel hopping making the Evil Twin a much more effective attack.