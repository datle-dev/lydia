# Kanata

[Kanata](https://github.com/jtroo/kanata) is a software keyboard remapper made in Rust.

## Installation

I just followed the instructions to build it via `cargo`, then I moved the binary to `/usr/local/bin`.

## Configuration

I created a very simple `kanata.kbd` configuration file in the default location `~/.config/kanata`
All it does is remap `Caps Lock` to be `Ctrl`.
```
(defcfg
  process-unmapped-keys yes
)

(defsrc
  caps
)

(deflayer default
  lctl
)
```
## Give kanata access to `input`/`uinput` subsystem to inject events

I followed the [instructions on avoiding sudo](https://github.com/jtroo/kanata/wiki/Avoid-using-sudo-on-Linux) for using kanata on the repo's wiki.
I've repeated the instructions here for convenience.

1. Create the `uinput` group if it does not exist
```
sudo groupadd uinput
```
2. Add the user to the `input` and `uinput` groups
```
sudo usermod -aG input $USER
sudo usermod -aG uinput $USER
```
Confirm by running `groups`.

3. Make sure the `uinput` device file has the right permissions

I created `kanata.rules` in `/etc/udev/rules.d` with the following content.
```
KERNEL=="uinput", MODE="0660", GROUP="uinput", OPTIONS+="static_node=uinput"
```
4. Make sure the `uinput` drivers are loaded
```
sudo modprobe uinput
```
## `systemd` Setup

Set up kanata to run on start with `systemd` as [instructed in this discussion](https://github.com/jtroo/kanata/discussions/130).
Here is the resulting `kanata.services` file that I configured.
```
[Unit]
Description=Kanata keyboard remapper
Documentation=https://github.com/jtroo/kanata

[Service]
Type=simple
ExecStart=/usr/local/bin/kanata --cfg /home/user/.config/kanata/kanata.kbd
Restart=no

[Install]
WantedBy=default.target
```

Notes:
- `Restart=no` based on a comment in the above [discussion](https://github.com/jtroo/kanata/discussions/130)
referencing [these docs](https://www.freedesktop.org/software/systemd/man/systemd.service.html#Restart=)

Then:
1. Run `systemctl --user start kanata.service` to start the kanata daemon
2. Run `systemctl --user enable kanata.service` so it autostarts on user log in.
3. At any time, run `systemctl --user status kanata.service` to check if it's running
