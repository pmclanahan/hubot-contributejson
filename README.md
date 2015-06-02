# Hubot Contribute.json

A hubot script for reading [contribute.json][] files, joining the IRC channel therein,
and welcomeing visitors when the channel is quiet with useful information from
the contribution data.

This was heavily inspired by the excellent [WelcomeBot][] and the [contribute.json][] effort.

Designed specifically for use with the hubot [IRC][] adaptor.

## Features

* Will wait for the configured amount of time (1 minute by default) before saying anything to a
  new visitor.
* If any more new visitors join during the wait period the timer will start over and the resulting
  single message will welcome however many new users have joined.
* If there is any conversation happening in the channel by users that are not new the bot will not
  welcome anyone. It's meant to welcome users during quiet times.
* Remembers every nick it sees (even nick changes) and won't greet anyone twice 
  (remembers over a restart as well if a persistent brain is used).
* Discovers who's in a channel when it joins and won't welcome any of them if they rejoin.

## Installation

In your hubot project run `npm install --save hubot-contributejson`. Then add `"hubot-contributejson"`
to your `external-scripts.json`. Also make sure [hubot-auth][] is installed and in your
`external-scripts.json` as well. You can optionally install [hubot-cronjob][] to
enable automatic updates for the contribute.json data nightly.

### NOTE

It is ***highly*** recommended that you use a persistent hubot brain store (like [hubot-redis-brain][]).

## Configuration

All configuration is optional.

`HUBOT_CONTRIBUTE_WELCOME_WAIT`: Number of seconds to wait after a new user joins the channel and no one else speaks to say something. (default: 60)

`HUBOT_CONTRIBUTE_ENABLE_CRON`: Use the `hubot-cronjob` script to update all of the contribute.json data every night.

## Commands

In order to run the following commands you must add yourself to the `contributejson` role via the `hubot-auth` script. From an admin user issue the
following command: `<hubot>: <user> has contributejson role`. This will allow `<user>` to run the commands below.

`<hubot>: contributejson list`: List the channels and contribute.json URLs known by the bot.

`<hubot>: contributejson add <url>`: Add a contribute.json URL to the list and join the channel in the file.

`<hubot>: contributejson rm [url]`: Remove a contribute.json URL from the list and leave the channel. If run from the desired channel the `[url]` is optional.

`<hubot>: contributejson update [url]`: Update the data for the contribute.json URL or channel. If run from the desired channel the `[url]` is optional.

## License

    Copyright 2015 Paul McLanahan

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

[WelcomeBot]: https://github.com/shaunagm/WelcomeBot
[contribute.json]: http://www.contributejson.org
[IRC]: https://github.com/nandub/hubot-irc
[hubot-redis-brain]: https://github.com/hubot-scripts/hubot-redis-brain/
[hubot-auth]: https://github.com/hubot-scripts/hubot-auth
[hubot-cronjob]: https://www.npmjs.com/package/hubot-cronjob
