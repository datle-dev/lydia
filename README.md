# Lydia - My Arch Linux PC with Hyprland

In mid-August 2024, I decided to try installing [Arch Linux](https://archlinux.org/) on an old gaming PC.
Around this time, I had been replaying Skyrim, and so I named the computer "Lydia" in honor of everybody's favorite and most dependable follower.

I thought I'd start this repo and document some things to help out future me.

## PC Specs:
- Intel i5-4690 (4) @ 3.900GHz
- NVIDIA GeForce GTX 1060 6GB
- 16GB RAM
- 250GB boot SSD

## dotfiles

Config files for all the programs I use can be found in my [dotfiles repo](https://github.com/datle-dev/dotfiles).

## Story of the First Install (because it'll be entertaining to look back on)
By this point, I only had ~6 months of experience with Linux:
- Installing Linux Mint on this same computer so long ago that I forgot the password
- Using Windows Subsystem for Linux (WSL2) to go through [The Odin Project](https://www.theodinproject.com/)
- Fiddling around with a $4/month [Digital ocean droplet](https://www.digitalocean.com/products/droplets) configured with Debian 12 following the [Linux Upskill Challenge](https://linuxupskillchallenge.org/) because why not

I understood little of how Linux worked under the hood, how its file system was structured, or important terminal commands that existed outside of "Top 20 Linux Commands to Know"-type lists.
I felt *some* shame using `archinstall` after reading gatekeeping comments, but I thought even if I hadn't formatted the drives, mounted the file system, or installed every package myself, my starting line could be a working system and then I could learn and figure it out from there.
In any case, the script made this initial part of the install super straightforward.

The most annoying part of the setup was connecting to the internet.
At first, I was piggybacking off my main PC's wifi via an ethernet tether, but as soon as Arch Linux was installed and I was finally in Hyprland's Kitty terminal, I couldn't connect anymore.
After a lot of debugging, I suspected one of the computer's physical ethernet ports had given out.

I ended up downloading the `broadcom-wl` package and having `pacman` install from it locally.
And after that, there were still hurdles with configuring the network with `iwd` and `systemd`, but eventually I got it working!

I had a working PC running Arch Linux!
I texted a fellow tech-y friend and begged for his praise.
I practiced whispering "by the way" for all the times I would have to let unsuspecting people, unprompted, know that I use Arch Linux.
I installed and ran `neofetch` and it felt *good*.
And now I could customize and configure Lydia with all the coolest weapons and armor in Tamriel, so to speak.

