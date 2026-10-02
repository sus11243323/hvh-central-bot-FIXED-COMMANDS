# HVH Central Discord Bot

## Setup
1. Install Node.js 20+.
2. Copy `.env.example` to `.env`.
3. Set:
   - `DISCORD_TOKEN`
   - `DISCORD_CLIENT_ID` (Application ID)
   - `DISCORD_GUILD_ID` (your test server ID)
4. Run:
   ```bash
   npm install
   npm run deploy
   npm start
   ```

Invite the bot with the `bot` and `applications.commands` scopes. Administrator is convenient, but the bot still cannot moderate members above its role.

## Admin panel
Use:
`/adminpanel channel:#your-channel password:your-password`

The password must be at least 8 characters. It is stored as a salted scrypt hash, not plain text.

Panel actions require both:
- Discord Administrator permission
- the configured panel password

## Anti-raid
Configure with:
`/antiraid setup enabled:true threshold:5 window:10 account-age:24 ban-on-raid:true log-channel:#mod-log`

Safe test:
`/antiraid test joins:5`

The test is a dry run and never bans real users.

## Presence
The bot displays:
`Playing Securing HVH Central`

## Notes
For automatic bans, the bot needs Ban Members permission and its role must be above the members it is trying to ban.


## Anti-nuke
Enable it with:
`/antinuke channel:#security-log`

When enabled, the bot snapshots existing channels and monitors channel deletions. If a bot deletes a protected channel, the bot attempts to kick that bot (when Discord permissions/role hierarchy allow it), logs the incident, and recreates the deleted channel from the saved snapshot.

Snapshots include channel name/type, category, position, topic, NSFW/rate-limit settings where applicable, and permission overwrites. Discord does not provide a perfect backup of messages, webhooks, pins, or every channel-specific runtime state, so those cannot be guaranteed to be restored.

The bot needs `View Audit Log`, `Manage Channels`, and `Kick Members` for the anti-nuke response. Its role must be high enough to kick the offending bot. Administrator includes these permissions, subject to Discord's role hierarchy.
