---
title: Overall experience with BSPWM and polybar
cover: "https://github.com/ztlevi/Dotfiles/blob/master/screenshots/terminal.jpg?raw=true"
preview: 300
date: 2020-04-03 16:34:23
categories: coding
tags: coding, bspwm
---

# First time with tiling window manager

I have to say BSPWM is not that friendly for the first-time user. It comes with a blank screen without anything. While
you could something there by forking something's setup. But it might not working for you cuz it's really easy to break
some dependencies on your system.

I would recommend you to start with something like Awesome tiling window manager. It comes with more built-in features.
But I think overall BSPWM is a good fit for me. Polybar is supported in BSPWM and the keybinding system is clean.

I forked [Henrik Lissner](https://github.com/hlissner)'s dotfiles setup last year. So thanks for the amazing scripts
that manage all the binaries and dependencies across multiple OS.

# Multi-monitor support

There are scripts enabled multi-monitors support.

- [bspc-focus](https://github.com/ztlevi/Dotfiles/blob/master/desktop/bspwm/bin/bspc-focus): allow you to focus windows
  across monitors
- [bspc-swap](https://github.com/ztlevi/Dotfiles/blob/master/desktop/bspwm/bin/bspc-swap): allows you swap windows
  across monitors

These scripts basically check if there is any window in the current monitor is on the direction of the current window.
If not, then it will check the next monitor.

# HDPI support

There are many things needs customization to support 4K monitors.

I'm putting a lot of effort to make HDPI support comes out of box. Basically, I'm using `xrandr` to figure out the
connected monitor resolution. Then calculate a `SCALE` factor based on the resolution. Passing that across multiple
applications to make HDPI like a built-in feature.

In `.xprofile`.

```bash
RESOLUTION=$(xrandr -q | grep primary | grep ' connected' | cut -d' ' -f4 | cut -d 'x' -f1)
if [ -z $RESOLUTION ]; then RESOLUTION=1920; fi
```

- Some apps can use system variables in their configuration. For example, `polybar`.

  In `run-polybar.sh`:

  ```bash
  MONITOR=$(xrandr -q | grep primary | grep ' connected' | cut -d' ' -f1)
  MONITORS=($(xrandr -q | grep ' connected' | cut -d' ' -f1))
  MONITOR=${MONITOR:-${MONITORS[0]}}

  if [ "$GDK_SCALE" -eq 2 ]; then
  dpi=160
  else
  dpi=92
  fi

  killall -q polybar
  while _is_running polybar; do sleep 1; done

  source "${0:A:h}/../../bin/inject-xcolors"
  pushd ~ >/dev/null

  env DPI=${dpi} MONITOR=${MONITOR} bash -c "polybar main >$XDG_DATA_HOME/polybar.log 2>&1 &"

  for mon in ${MONITORS[@]/${MONITOR}/}; do
  env DPI=${dpi} SIDE_MONITOR=${mon} bash -c "polybar side >>$XDG_DATA_HOME/polybar.log 2>&1 &"
  done

  popd >/dev/null
  ```

  In polybar config:

  ```bash
  [bar/side]
  inherit = bar/master
  monitor = ${env:SIDE_MONITOR}

  dpi = ${env:DPI}
  ```

- There are apps cannot use system environment variables. So I pass different configs.

  ```bash
  if [ "$GDK_SCALE" -eq 2 ]; then
  dunst -config $DOTFILES/desktop/bspwm/config/dunst/dunstrc_4K &
  else
  dunst -config $DOTFILES/desktop/bspwm/config/dunst/dunstrc &
  fi
  ```

# Polybar

This is a light weight and fully customizable status bar. You could put almost everything there.

I have a clickable WIFI, sound, and icon workspaces module.

![polybar](https://raw.githubusercontent.com/ztlevi/picee_images/master/common/image.soyiqyuc4wi.png)

While there are tons of themes on the web. Take a look at [here](https://github.com/polybar/polybar).

# Gnome apps

I don't know what other people typically do to modify settings in tiling window mangers. Because they usually don't ship
with setting applications.

So I would also install Gnome and it's applications just so I can modify the settings like Bluetooth or WIFI.

# Summary

The reason most people choose tiling window manager is because it's productive and cool. Talking about productivity,
there won't be a huge difference between tiling window manager and normal ones if you just use one or two monitors. It
will be faster because you don't need to move your hands to the mouse and then move back. Everything is under keyboard.

But the productivities will scale up when u have 4 or more monitors. In this case, a multi-monitor solution will be a
life saver.

And finally, it's cooooooool!

If you're instead in tiling window manager. You're welcome to fork [ my setup ](https://github.com/ztlevi/Dotfiles).
