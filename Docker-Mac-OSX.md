### This is under development. The part of connecting to X Window system is working. Investigating yet how to connect wireless interfaces into docker container, so is not yet fully working!! Help wanted!! ⚠️ 

The recommended docker run command to be run under Mac OSX host is:

```
~# docker run \
          --rm \
          -ti \
          --name airgeddon \
          --net=host \
          --privileged \
          -p 3000:3000 \
          -v /path/to/some/dir/on/your/host:/io \
          -e DISPLAY=$(ifconfig en0 | grep inet | awk '$1=="inet" {print $2}'):0 \
          v1s1t0r1sh3r3/airgeddon
```

Parameters explanation:

 - `--rm` &#8594; Ephemeral containter. It will be removed on exit.
 - `-ti` &#8594; Attach pseudo-TTY terminal to the container as interactive.
 - `--name airgeddon` &#8594; Name for the container.
 - `--net=host` &#8594; Is needed to have access to the host network interfaces inside the container.
 - `--privileged` &#8594; Needed to have permissions over network interfaces (mode switching).
 - `-p 3000:3000` &#8594; Open port to access to BeEF control panel from the host.
 - `-v /path/to/some/dir/on/your/host:/io` &#8594; It maps a directory from host to the container. Useful to use external files like dictionaries or whatever.
 - `-e DISPLAY=$(ifconfig en0 | grep inet | awk '$1=="inet" {print $2}'):0` &#8594; It overwrites the needed var to connect to local X Window system (It's understood you installed XQuartz for Mac).
 - `v1s1t0r1sh3r3/airgeddon` &#8594; Is the name and tag of the image. `v1s1t0r1sh3r3/airgeddon` is the stable version and is the same as `v1s1t0r1sh3r3/airgeddon:latest`. Alternatively you can use `v1s1t0r1sh3r3/airgeddon:beta` for development version.

### Mac OSX Tips

#### Volume mapping

Don't forget to replace on docker command the string "/path/to/some/dir/on/your/host" with a path of an existing directory of your choice on your host machine. That directory will be the "input/output" point for the script. For example, if you place a dictionary.txt file there, inside the script you must access to it as "/io/dictionary.txt". If you capture a trophy or a Handshake file, save it at "/io/" dir to access it from the host.

#### X Window system

You'll need a X Window system running on your Mac OSX. You can install [XQuartz], and after installing it, be sure of allowing connections from network clients in preferences as shown on next image:

<p align="center">
	<img src="https://raw.githubusercontent.com/v1s1t0r1sh3r3/airgeddon/master/imgs/wiki/x11_preferences_xquartz.png" title="XQuartz preferences">
</p>

After that, you'll need to disable access control or add your ip to the authorized clients list:

`~# xhost +` &#8594; To disable completely the restriction.

Or the more recommended:

`~# xhost $(ifconfig en0 | grep inet | awk '$1=="inet" {print $2}')` &#8594; To allow only local ip, this is more restrictive and secure.

[XQuartz]: https://www.xquartz.org/