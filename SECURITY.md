# Security

## Reporting a problem

Please report security problems **privately**: open this repository's **Security** tab →
**Report a vulnerability**. Don't open a public issue, and never post real room codes or invite links.

Include what you found, the steps to reproduce it, and the version (Windows: Settings → Apps → noxx chat; server: `noxx-server -version`).
We aim to reply within 7 days and will credit you in the release notes if you'd like.

Only the latest release is supported. Please update before reporting.

## How N0xx Chat protects you

- **Room codes are keys.** Each room is 4 random words from a 2048-word list, stretched with
  PBKDF2-SHA256 (600,000 rounds), then turned into a room identifier and an AES-256-GCM key with
  HKDF-SHA256. The code never leaves people's devices.
- **Sealed messages.** Every message, name and call setup message is encrypted with a fresh IV and
  bound to the room. Tampered, misattributed or replayed messages are rejected.
- **Private calls.** Voice, video and screen share are peer-to-peer over DTLS-SRTP. Their keys are
  exchanged inside the encrypted channel, so the server can't intercept calls.
- **Blind servers.** The server only relays ciphertext between people in the same room, rate-limits
  each connection, and stores and logs nothing.
- **No port forwarding.** Tailscale mode connects outward only, and only the server program joins
  Tailscale.

## Things to be aware of

- Anyone with a room code can join that room. Share codes privately, and make a new room if a code leaks.
- People you call peer-to-peer can see your IP address.
- The installers aren't code-signed yet. Download them only from this repository's Releases page.
