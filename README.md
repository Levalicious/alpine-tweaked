alpine-tweaked
===

## FULLY UNATTENDED ALPINE LINUX INSTALL

I've seen a lot of disconnected pieces of code and information related to fully unattended alpine linux setups. So far, the only complete working solution I've managed to piece together involves generating your own ISO running an init script.

Try it on your machine:
```
git clone https://github.com/Levalicious/alpine-tweaked.git
cd alpine-tweaked
run/start
```

Assuming you're running ubuntu, all the dependencies should be installed for you. If you're running alpine, there's definitely better solutions already out there. Look at them instead.

If you're running anything else, sucks to suck.
Just kidding

The scripts themselves don't do much: 
`run/setup` downloads dependencies into a `deps/` folder
`run/start` generates a fresh virtual hard disk and launches qemu
`run/rebuild` just deletes `dist/` and runs `run/start`
`run/clean` just deletes files

The only mildly complex script is `run/isogen` and even that's just echoing a configuration and an init script to some files and then running xorriso.

Tweak `SETUP` in `.env` to play with some different configs I predefined. The available options are [ `full`, `fast`, `fastest`].

On a final note, I did figure out one thing while trying to get all this working. If you check the in the init script, I launch `setup-alpine` like so:
```
ERASE_DISKS="$DISK" setup-alpine -ef /etc/autosetup/answers
```
I found plenty of discussions on how to set up autologin correctly and multiple incorrect tutorials to get the init script running. However, at no point did I find any documentation or information about needing the `ERASE_DISKS` environment variable set in order to bypass setup-alpine prompts. I _think_ this is only required for data disks, but honestly I have no idea.