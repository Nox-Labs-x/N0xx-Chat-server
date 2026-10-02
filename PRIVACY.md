# Privacy Policy

**Effective: 2 October 2026**

**The short version:** N0xx Chat is built so that nobody can read your messages or calls. That
includes us (Nox Labs) and whoever runs your server. There are no analytics and no tracking, and
nothing you say is stored on a server. A server can ask you to sign in with a username and password,
but even then it can't read your messages.

This policy covers the noxx chat desktop app, the noxx chat server program, and these repositories.

## What we collect

**Nothing.** The app and server have no analytics, telemetry, crash reporting or ads, and never
contact us. We have no servers of our own that your app talks to.

The one thing the desktop app looks up by itself is **whether there's a new version**. Once a day
it asks GitHub's public API for the latest release number of noxx chat. Nothing about you is sent,
though GitHub sees your IP address as with any web request. You can turn this off in
Settings → Notifications.

## What stays on your device

The app stores its settings locally on your device:

- your display name and profile (picture, colour, status, "about me"), chosen microphone, speaker
  and camera, and your preferences;
- the server address you entered;
- if a server uses accounts, your sign-in token for that server (not your password);
- if **Remember recent rooms** is on (Settings → Privacy): recent room names, codes and servers.

You can clear recent rooms in Settings → Privacy & safety, and remove everything by uninstalling the
app. Screen recordings are saved on your own device (in the desktop app, in your Videos folder under
"noxx chat") and are never uploaded. Recordings contain your screen, your microphone and your
computer's sound. They never include other people's voices, cameras or screens from the app.

## Accounts on a server

A host can have their server ask people to sign in (servers from version 0.6.0 do this unless the
host turns it off). If you make an account, that server stores:

- your username, and your password as an Argon2id hash (a scrambled form that can't be turned back
  into the password);
- when the account was made and roughly when it was last used, and whether it's an admin;
- scrambled copies of your sign-in tokens, so your devices stay signed in for up to 60 days.

This is kept in one file on the host's computer, and nowhere else. The server's admins can see the
list of usernames and when they were last used, remove accounts and reset passwords. They can't see
your password, your messages or anything else you send.

When you're signed in, the server tells the people in a room your username, so they can tell it's
really you. It also means the server can tell which account is connected to which room identifier,
and when (it still can't see the room's name, code or contents). To delete your account, ask the
server's admin to remove it.

## What a server can see

Rooms run on servers operated by independent hosts. Everything you send is **end-to-end encrypted**
with the room code (AES-256-GCM) before it leaves your device, and **the room code is never sent to
the server**.

A server can see:

- your username, if the server uses accounts (see above);
- the IP address your connection comes from (needed to connect you; with a Tailscale public link,
  connections reach the server through Tailscale's network);
- a random-looking room identifier made from the code, which can't practically be turned back into it;
- when devices connect and disconnect, and the size and timing of the encrypted data.

A server **cannot** see display names, profiles, messages, reactions, typing, voice, video or screen
shares. The official noxx chat server keeps no message history and no log of any of the above. Its window
only shows a running count of connected people and account events (a new account, an admin removing
one). A host could change their own server software, so only use servers run by people
you trust.

## What other people in a room can see

Everyone who has a room's code can read the room's messages and see your display name, profile and
voice or camera status. When someone joins, another member's device may share recent messages with
them (up to the last 100). Nothing is kept once everyone has left, and disappearing messages are
removed from everyone's screen when their timer runs out.

In the desktop app on Windows and macOS, the app window is hidden from screen capture, so other apps
can't record or clip what's on it. No app can stop someone photographing their screen.

Voice, video and screen sharing are **peer-to-peer**, so the people you call can see your IP address.

## Notifications

If you turn on notifications (Settings → Notifications), your operating system shows them, and it
may keep them in its notification centre. You can choose to show only who wrote, not the message.

## Other services

- **STUN servers** (Cloudflare and Google) help calls connect and see your IP address when a call
  starts. They never see call content.
- **Tailscale:** if a host uses Tailscale, connections to their server pass through Tailscale's
  network. Content stays end-to-end encrypted. The noxx chat server turns off Tailscale's diagnostic log
  upload. [Tailscale's privacy policy](https://tailscale.com/privacy-policy) applies to hosts' use.
- **GitHub** serves the downloads. [GitHub's privacy statement](https://docs.github.com/site-policy/privacy-policies/github-general-privacy-statement) applies when you visit or download.
- **Microsoft WebView2:** on Windows the app uses the system's web engine, so Microsoft's terms and
  your Windows settings for WebView2 apply.

## Children

N0xx Chat isn't intended for children under 13, or under the higher minimum age in your country.

## Your rights

We hold no personal data about you, so there's nothing for us to access, correct, export or delete.
To remove data from your device, clear recent rooms or uninstall the app. For anything a host might
hold, such as their own network logs, contact that host.

## Changes

If this policy changes, we'll update the effective date above and publish the new version here.

## Contact

Open an issue at <https://github.com/Nox-Labs-x/N0xx-Chat/issues>. Don't include room codes or anything
private. For security issues, see [SECURITY.md](SECURITY.md).
