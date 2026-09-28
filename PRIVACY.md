# Privacy Policy

**Effective: 28 September 2026**

**The short version:** N0xx Chat is built so that nobody can read your messages or calls. That
includes us (Nox Labs) and whoever runs your server. There are no accounts, no analytics and no
tracking, and nothing you say is stored on a server.

This policy covers the noxx desktop app, the noxx server program, and these repositories.

## What we collect

**Nothing.** The app and server have no analytics, telemetry, crash reporting or ads, and never
contact us. We have no servers of our own that your app talks to.

## What stays on your device

The app stores its settings locally on your device:

- your display name, chosen microphone, speaker and camera, and your preferences;
- the server address you entered;
- if **Remember recent rooms** is on (Settings → Privacy): recent room names, codes and servers.

You can clear recent rooms in Settings → Privacy, and remove everything by uninstalling the app.
Screen recordings are only saved where you choose, on your own device.

## What a server can see

Rooms run on servers operated by independent hosts. Everything you send is **end-to-end encrypted**
with the room code (AES-256-GCM) before it leaves your device, and **the room code is never sent to
the server**.

A server can see:

- the IP address your connection comes from (needed to connect you; with a Tailscale public link,
  connections reach the server through Tailscale's network);
- a random-looking room identifier made from the code, which can't practically be turned back into it;
- when devices connect and disconnect, and the size and timing of the encrypted data.

A server **cannot** see display names, messages, typing, voice, video or screen shares. The official
noxx server keeps no message history and no log of any of the above. It only displays a running count
of connected people. A host could change their own server software, so only use servers run by people
you trust.

## What other people in a room can see

Everyone who has a room's code can read the room's messages and see your display name and voice or
camera status. When someone joins, another member's device may share recent messages with them (up
to the last 100). Nothing is kept once everyone has left.

Voice, video and screen sharing are **peer-to-peer**, so the people you call can see your IP address.

## Other services

- **STUN servers** (Cloudflare and Google) help calls connect and see your IP address when a call
  starts. They never see call content.
- **Tailscale:** if a host uses Tailscale, connections to their server pass through Tailscale's
  network. Content stays end-to-end encrypted. The noxx server turns off Tailscale's diagnostic log
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
