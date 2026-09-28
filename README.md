<div align="center">

# N0xx Chat server

The server for [N0xx Chat](https://github.com/Nox-Labs-x/N0xx-Chat). Run it on a spare PC or a
Raspberry Pi and your friends can connect from anywhere.

**[Windows](https://github.com/Nox-Labs-x/N0xx-Chat-server/releases/latest/download/noxx-server-windows.zip)** ·
[Linux](https://github.com/Nox-Labs-x/N0xx-Chat-server/releases/latest/download/noxx-server-linux-x64.tar.gz) ·
[Raspberry Pi / ARM](https://github.com/Nox-Labs-x/N0xx-Chat-server/releases/latest/download/noxx-server-linux-arm64.tar.gz) ·
[All releases](https://github.com/Nox-Labs-x/N0xx-Chat-server/releases)

</div>

It's a single program with nothing to install. It connects out through Tailscale, so you don't
open any ports on your router and your home IP isn't exposed. Only the server itself goes on
Tailscale, not the rest of your PC or network.

It can't read anything. All it does is pass encrypted data between people in the same room. It
doesn't store messages or keep logs, and calls go directly between friends, so it barely uses
anything.

If someone opens your server link in a browser, they get a page with the app download and the
room code from their invite.

## Windows

1. Download `noxx-server-windows.zip` and unzip it somewhere it can stay.
2. Double-click **Start - public link.bat**. If Windows says "Windows protected your PC", click
   *More info* then *Run anyway*.
3. First time only: sign in to Tailscale (it's free) and hit *Connect*, then click to turn on
   HTTPS/Funnel.
4. Wait until it says **✓ Your public link is live**, then send people the link. It'll look like
   `https://noxx.tail1234.ts.net`.

There are two other start files. **Start - private (Tailscale only)** keeps it off the public
internet: your friends need Tailscale, and you share the device with them. **Start - local network
only** is just for your house.

## Linux / Raspberry Pi

With PM2:

```sh
ARCH=$(uname -m | sed 's/x86_64/x64/;s/aarch64/arm64/')
curl -LO https://github.com/Nox-Labs-x/N0xx-Chat-server/releases/latest/download/noxx-server-linux-$ARCH.tar.gz
tar -xzf noxx-server-linux-$ARCH.tar.gz && cd noxx-server-linux-$ARCH
pm2 start ecosystem.config.cjs && pm2 save && pm2 startup
pm2 logs noxxchat
```

The Tailscale sign-in link and your public link show up in `pm2 logs`. If the box has no screen,
just open the links on your phone.

Rather use systemd? Run `sudo ./install-service.sh`, then watch it with `journalctl -u noxx-server -f`.

Your login is saved in `~/.config/noxx-server`. To update, replace the files and restart, and the
link stays the same.

## If something's off

- **The link ends in `-1`.** You already have a device called `noxx` on Tailscale, probably an old
  copy. Either use the new link, or delete the old one at https://login.tailscale.com/admin/machines,
  rename this one back to `noxx`, and restart.
- **The app can't reach it.** Make sure the link matches exactly and the server says it's live. On
  Windows, `ipconfig /flushdns` fixes it if the PC looked the link up too early.
- **It asks you to sign in again after a few months.** Tailscale expires devices after 180 days. You
  can turn that off: Machines → noxx → ⋯ → Disable key expiry.
- **Someone can chat but calls won't connect.** Some networks block direct connections. Private mode
  usually fixes it, or you can add a TURN server with `-ice`.

Options: `-tailscale`, `-public`, `-name noxx`, `-addr :8080`, `-downloads <folder>`, `-ice <json>`, `-version`

---

[Terms](TERMS.md) · [Privacy](PRIVACY.md) · [License](LICENSE) · [Security](SECURITY.md) · [Third-party notices](THIRD-PARTY-NOTICES.md)
