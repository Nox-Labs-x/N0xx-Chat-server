<div align="center">

# noxx chat server

The server for [noxx chat](https://github.com/Nox-Labs-x/N0xx-Chat). Run it on a spare PC or a
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
anything. The one thing it does keep is the list of accounts, so people sign in and get a verified
@username.

If someone opens your server link (or an invite link) in a browser, they get a page with the app
download, the room code from their invite, and a button that opens the invite straight in noxx chat
if they already have it.

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

## Accounts

People sign in to your server with a username and password. Messages stay end-to-end encrypted, so
the server only knows who's connected, never what they say.

1. The first time it starts, the window (or `pm2 logs`) shows a **setup code**:
   ```
   No accounts yet. Open noxx chat, pick Create account, and use this
   setup code to make the first account. It becomes the admin:
     SETUP CODE: K7QF-2MXP-9TRA
   ```
2. In noxx chat, put in your server link, click **Create account**, and use that code. That account
   is the admin.
3. Invite people from **Settings → Server admin → Make an invite code**. Each code works once and
   lasts a week. You can also open sign-ups to anyone with the link, or close them.

The admin page also lists everyone (and who's online right now), lets you remove an account
(they get disconnected straight away), reset a password, or make someone else an admin. You can
give the server a **name and welcome note** there too. People see it when they sign in and on your
link's start page.

People can sign out their other devices and delete their own account from **Settings → Account**.

From the command line (works while the server runs):

```sh
noxx-server accounts list
noxx-server accounts add maya -admin     # prints a password for them
noxx-server accounts reset maya          # new password, signs them out everywhere
noxx-server accounts remove maya
noxx-server accounts signup open|invite|closed
noxx-server accounts invite
```

The accounts live in `accounts.json` next to the Tailscale login (`~/.config/noxx-server` on Linux,
`%AppData%\noxx-server` on Windows). Passwords are stored as Argon2id hashes. Back that file up if
you move the server.

Don't want accounts? Start it with `-accounts=false` and anyone with a room code can join, like
before. Apps older than 0.6.0 can't sign in, so everyone needs the new app if accounts are on.

## If something's off

- **The link ends in `-1`.** You already have a device called `noxx` on Tailscale, probably an old
  copy. Either use the new link, or delete the old one at https://login.tailscale.com/admin/machines,
  rename this one back to `noxx`, and restart.
- **The app can't reach it.** Make sure the link matches exactly and the server says it's live. On
  Windows, `ipconfig /flushdns` fixes it if the PC looked the link up too early.
- **It asks you to sign in again after a few months.** Tailscale expires devices after 180 days. You
  can turn that off: Machines → noxx → ⋯ → Disable key expiry.
- **Lost the setup code?** Restart the server and it prints a new one, or make the first account
  with `noxx-server accounts add yourname -admin`.
- **Forgot your admin password?** `noxx-server accounts reset yourname` on the server.
- **Someone can chat but calls won't connect.** Some networks block direct connections. Private mode
  usually fixes it, or you can add a TURN server with `-ice`.

Options: `-tailscale`, `-public`, `-name noxx`, `-addr :8080`, `-accounts=false`,
`-signup open|invite|closed`, `-data <folder>`, `-downloads <folder>`, `-ice <json>`, `-version`

---

[Terms](TERMS.md) · [Privacy](PRIVACY.md) · [License](LICENSE) · [Security](SECURITY.md) · [Third-party notices](THIRD-PARTY-NOTICES.md)
