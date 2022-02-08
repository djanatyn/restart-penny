# restart-penny

This is a bot, with the sole purpose of restarting a [Discord-Red](https://docs.discord.red/en/stable/index.html) bot (running within a systemd unit context).

Type `!pennyplz` in Discord to attempt a restart.

# motivation

Sometimes the lavalink server crashes while I'm asleep! I'd like my friends to be able to restart the bot themselves.

# how does it work?

This bot is built with [serenity/serenity-rs](https://github.com/serenity-rs/serenity):
> Serenity is a Rust library for the Discord API.

* https://lib.rs/crates/serenity
* https://docs.rs/serenity/0.10.10/serenity/client/index.html

I made small modifications to one of the examples available:
* https://github.com/serenity-rs/serenity/blob/current/examples/e01_basic_ping_bot/src/main.rs

# what is it restarting?

I have a Discord-Red bot running within a systemd unit, `penny-redbot`:
```
● penny-redbot.service
     Loaded: loaded (/etc/systemd/system/penny-redbot.service; enabled; vendor preset: enabled)
     Active: active (running) since Tue 2022-02-08 13:35:20 UTC; 5min ago
   Main PID: 601868 (redbot)
         IP: 0B in, 0B out
      Tasks: 40 (limit: 9315)
     Memory: 383.2M
        CPU: 20.161s
     CGroup: /system.slice/penny-redbot.service
             ├─601868 /home/djanatyn/.discordred/bin/python3 /home/djanatyn/.discordred/bin/redbot penny
             └─601921 /nix/store/ndmafn9wrzdpyyw42cx55dgqblg2c8jc-openjdk-headless-11.0.12+7/bin/java -Djdk.tls.client.protocols=TLSv1.2 -jar /home/djanatyn/.local/share/Red-DiscordBot/data/penny/cogs/Audio/Lavalink.jar

Feb 08 13:35:24 vessel redbot[601868]: │  Red version        │ 3.4.16  │ │  Unique Users │ 34  │
Feb 08 13:35:24 vessel redbot[601868]: │  Discord.py version │ 1.7.3   │ ╰─────────────────────╯
Feb 08 13:35:24 vessel redbot[601868]: │  Storage type       │ JSON    │
Feb 08 13:35:24 vessel redbot[601868]: ╰───────────────────────────────╯
Feb 08 13:35:24 vessel redbot[601868]: Loaded 6 cogs with 82 commands
Feb 08 13:35:24 vessel redbot[601868]: Invite URL:
Feb 08 13:35:24 vessel redbot[601868]: https://discord.com/oauth2/authorize?client_id=...
Feb 08 13:35:25 vessel redbot[601868]: [2022-02-08 13:35:25] [INFO] red.Audio.manager: Internal Lavalink server started. PID: 601921
Feb 08 13:35:30 vessel redbot[601868]: [2022-02-08 13:35:30] [INFO] red.Audio.manager: Internal Lavalink server is ready to receive requests.
...
```

Typing `!pennyplz` in Discord-Chat will execute `systemctl restart penny-redbot`.

No other functionality is supported.

