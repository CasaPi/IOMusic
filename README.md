 'Output Music'
=================

Listen to your music files remotely.

### Purpose
* Mount locally a remote system via SSH.
* Run any music player and open the local directory.
* Play music.

### Requirements
* Package *openssh* installed on your system ([installation](https://wiki.archlinux.org/index.php/Secure_Shell))
* Running SSH server on the targeted remote system.

## SSHFS does magic

> You can use sshfs to mount a remote system - accessible via SSH - **to a local folder**.<br>
> **-[wiki.archlinux.org](https://wiki.archlinux.org/index.php/SSHFS)**

Install *sshfs* on your laptop:
```
$ pacman -S sshfs
```
Mount the targeted remote directory:
```
$ mkdir remotemusic
$ sshfs <username>@<srv_ip_address>:<directory_path> <local_directory>
(example)
$ sshfs adrien@174.180.180.180:/mnt/hd remotemusic
```


## (Optional) MOC Installation

> Music On Console is a lightweight music player which consists of 2 parts, a server (Moc) and a player/interface (Mocp).<br>
> **-[wiki.archlinux.org](https://wiki.archlinux.org/index.php/MoC)**

* Install the *moc* package on your laptop:
```
$ pacman -S moc
```

*  You may encounter the [error](https://bbs.archlinux.org/viewtopic.php?id=170116) below. Make sure you have installed *pulseaudio* or any alternative before:
```
$ mocp 

Can't load plugin libaac_decoder: file not found
Can't load plugin libffmpeg_decoder: file not found
Can't load plugin libmodplug_decoder: file not found
Can't load plugin libmusepack_decoder: file not found
Can't load plugin libspeex_decoder: file not found
Can't load plugin libwavpack_decoder: file not found
Running the server...
Trying JACK...
Trying ALSA...
ALSA lib pcm_dmix.c:1022:(snd_pcm_dmix_open) unable to open slave
Trying OSS...

FATAL_ERROR: No valid sound driver!
FATAL_ERROR: Server exited!
```
* If the fatal error persists, try to run `mocp` in *sudo*. If it works, assign your current user to the *audio* group
```
$ usermod -a -G audio <username>
$ reboot
```
* If the fatal error still occurs, read the following section:  [https://wiki.archlinux.org/index.php/Moc#Troubleshooting](https://wiki.archlinux.org/index.php/Moc#Troubleshooting)

* If you encounter some problems due to plugins, you may need to install [optional dependencies](https://www.archlinux.org/packages/extra/x86_64/moc/).

### Config

```
$ cp /usr/share/doc/moc/config.example ~/.moc/config
```

Edit `~/.moc/config`:
```
Theme = /usr/share/moc/themes/darkdot_theme
```
