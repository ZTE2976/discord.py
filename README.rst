discord.py
==========

.. image:: https://discord.com/api/guilds/336642139381301249/embed.png
   :target: https://discord.gg/r3sSKJJ
   :alt: Discord server invite
.. image:: https://img.shields.io/pypi/v/discord.py.svg
   :target: https://pypi.python.org/pypi/discord.py
   :alt: PyPI version info
.. image:: https://img.shields.io/pypi/pyversions/discord.py.svg
   :target: https://pypi.python.org/pypi/discord.py
   :alt: PyPI supported Python versions

A modern, easy to use, feature-rich, and async ready API wrapper for Discord written in Python.

The Future of discord.py
--------------------------

Please read the `gist <https://gist.github.com/Rapptz/4a2f62751b9600a31a0d3c78100287f1>`_ for the future of this project. It's been a good one.

Key Features
-------------

- Modern Pythonic API using ``async`` and ``await``.
- Proper rate limit handling.
- Optimised in both speed and memory.

Installing
----------

**Python 3.8 or higher is required**

To install the library without full voice support, you can just run the following command:

.. code:: sh

    # Linux/macOS
    python3 -m pip install -U discord.py

    # Windows
    py -3 -m pip install -U discord.py

Otherwise to get voice support you should run the following command:

.. code:: sh

    # Linux/macOS
    python3 -m pip install -U "discord.py[voice]"

    # Windows
    py -3 -m pip install -U discord.py[voice]


To install the development version, do the following:

.. code:: sh

    $ git clone https://github.com/Rapptz/discord.py
    $ cd discord.py
    $ python3 -m pip install -U .[voice]


Optional Packages
~~~~~~~~~~~~~~~~~~

* `PyNaCl <https://pypi.org/project/PyNaCl/>`__ (for voice support)

Please note that on Linux installing voice you must install the following packages via your favourite package manager (e.g. ``apt``, ``dnf``, etc) before running the above commands:

* libffi-dev (or ``libffi-devel`` on some systems)
* python-dev (e.g. ``python3.6-dev`` for Python 3.6)

Quick Example
--------------

.. code:: py

    import discord

    class MyClient(discord.Client):
        async def on_ready(self):
            print('Logged on as', self.user)

        async def on_message(self, message):
            # don't respond to ourselves
            if message.author == self.user:
                return

            if message.content == 'ping':
                await message.channel.send('pong')

    client = MyClient()
    client.run('token')

Bot Example
~~~~~~~~~~~~~

.. code:: py

    import discord
    from discord.ext import commands

    bot = commands.Bot(command_prefix='>')

    @bot.command()
    async def ping(ctx):
        await ctx.send('pong')

    bot.run('token')

You can find more examples in the examples directory.

Links
------

- `Documentation <https://discordpy.readthedocs.io/en/latest/index.html>`_
- `Official Discord Server <https://discord.gg/r3sSKJJ>`_
- `Discord API <https://discord.gg/discord-api>`_

-------------------------------------------------

**The Future of discord.py**

*If you're looking for a tl;dr, you can [check the FAQ](#FAQ).*

Greetings. If you don't know me, I'm Danny. I'm the core (and sole) maintainer of the discord.py library. Contrary to popular belief, I am actually not a Discord employee. In fact, I'm not even a professional programmer. In reality, I'm a medical professional who works at my local hospital. Despite all that, I do enjoy programming as a hobby and have worked on discord.py on my own free time.

I've been working on discord.py for about 6 years – a rather significant portion of my life has gone into maintaining this software library completely for free. I have never accepted donations. I have never asked for donations. This library has been my passion project, born completely out of a desire to see more bots on Discord written in Python. Over the years, many users of my library have told me that discord.py changed their lives. It empowered them to challenge themselves, create fun things, and find new opportunities. As someone who has always valued educative, open-source projects, it means so much to me to know that discord.py has had a positive impact on people's lives. 

Unfortunately, today marks the end of my involvement in the project. Therefore, effective immediately, I will be stepping down as maintainer of the project. I asked the contributors that I trust if they wanted to take over the project, but no one accepted. Essentially, this is a unanimous decision that the discord.py project will be ending. The code remains open, so if someone wants to fork it and work with it, then they are free to do so. However, mainline development will cease as of today. 

I want to assure you that this was not a decision made lightly. My hope is that this document explains my thoughts and the process leading up to the decision. I've also written an [FAQ](#FAQ) if you just want a quick rundown.

**Grassroots Movement**

I joined Discord on August 10th 2015. I had friends who recommended Discord to me, and we wanted to move our tournament operations from IRC/Skype over to a new platform due to excessive grievances with those platforms. The first time I used Discord I was pretty impressed; however, for me to move on to it, we needed an API for my bots to function. Unfortunately, at the time, there was no "official" API. Luckily, I had found an API wrapper by the name of `node-discord` and used it. This API wrapper was very minimal, only containing a `debug` event that dumped the gateway messages (at the time, `v2`) and a `message` event that was special just for messages. This experience got me really interested in figuring out how the API worked. I made my bot, [R. Danny][r-danny-blog], the very next day (August 11th) and invited it to the r/Splatoon server.

I wasn't completely satisfied with the `node-discord` package nor with using EcmaScript 5, so I took it upon myself to start reverse engineering the API myself using Python. At this point in time, all the early members of the bot and API ecosystem resided in a server called Discord Developers, a different server, however, than the one that goes by the same name today. In this server, we had a lot of Discord enthusiasts and Discord employees, much like today's newer Discord Developers server. Of these people, there were people like izy521 (the creator of the aforementioned `node-discord`) and Voltana. We were talking about the Discord API and reverse engineering it until eventually all of us like-minded individuals made our own server called Discord API, owned by Voltana. This happened on August 13th, very soon after my own registration.

I continued working on my API wrapper, aptly named `discord.py`, along with the others who had made their own libraries such as `Discord.NET`, `discord.rb`, `discord.js`, `discord4J`, etc. Together, we reverse engineered the API over the next few months with no documentation to help us. Our little ecosystem thrived and lots of bots were made. Eventually, Discord themselves wrote a [blog post][discord-blog-dapi] detailing our adventures to get more people to use our libraries. There was a lot of hope and excitement about the future of Discord bots. We were promised many things! The future was going to be bright; we were going to get slash commands, webhooks, "channel observers", proper voice support, etc.

As time went on, Discord realised that the traditional approach of inviting bots by invite crawling was problematic. To combat this abuse vector, Discord decided to ramp up their interest in the API and made official Bot accounts that could only be invited via OAuth2 and not through the traditional invite scraping mechanism. This was considered a good change for privacy and started the hopeful beginning of Discord investing in their API. We were promised many exclusive features for bots, though our first and only feature at launch was the ability to join voice channels across many servers. The official bot API was released on April 8th 2016.

**Neglect**

When Discord unveiled their official API back in 2016, many promises were made about features that would be implemented. Unfortunately, most of the things we were promised never ended up materialising. When we asked the Discord employees about the state of the API, they always mentioned that they lacked the development resources required to work on the API and that it made no business sense to prioritise or work on the API platform. This was completely understandable since Discord was, at the time, a small company with a lot on their plate. However, this lack of priority meant that the API languished over the next 3 years. There was growing frustration within the Discord bot community that we weren't being listened to.

Our Discord API server was originally a place where Discord employees and library developers could discuss changes with one another. Our server was not without drama, nor was it perfect. Some Discord employees left due to this drama, and some never spoke much to begin with. Despite all of this, our Discord API server was the central communications hub between Discord employees and library developers. It was the main place where library developers could gain insight into upcoming changes and provide feedback. Over time, the number of Discord employees willing to engage with us library developers dwindled down to two: Jake and b1nzy. We often joked that the two of them were our last hope, as they were the only Discord employees that showed any genuine interest in listening to and acting upon our feedback. Unfortunately, b1nzy left Discord and Jake became increasingly busy with other areas of the app, so our disconnect with the internal Discord team only continued to grow.

It wasn't until around November 2019 that Discord started focusing more of their resources on their bot development platform.

**The Discord Infrastructure Server**

While our communication suffered, a different, more private server was getting more attention. This server was colloquially known as "dinfra", short for "Discord Infrastructure". Originally, the purpose of this server was to share infrastructure status with the bigger bot developers to give them a heads-up on when things might be turbulent. However, the goal of this server morphed into being a semi-official way for big bot developers and Discord employees to communicate about the future of the platform.

It should be noted that this server did not have many library developers within it, so we were mostly blind to what went on in that server. Only two library developers were invited and only because they *also* helped with the development of big bots. They were not there for their role as library developers. Discord employees gradually began to discuss API changes in the Discord Infrastructure server instead of in our Discord API server. Discord no longer kept us library developers up to date on proposed API changes, or gave us much of an opportunity to provide feedback. Luckily for us library developers, we had a few "moles" in the Discord Infrastructure server who were willing to exchange information with us so that we could obtain information on upcoming changes we would need to accommodate.

One such change was the introduction of a feature called `guild_subscriptions`, which was a way to reduce the bandwidth of a large bot by opting out of `PRESENCE_UPDATE` and `TYPING_START` events. These events typically made up around 95% of a bot's bandwidth and CPU usage, and it was a common feature request to remove these events from showing up in the gateway event stream. Unfortunately, this boolean toggle came with the caveat of also turning off member-related events, and it was undesirable for a lot of bots. A better system needed to be made. This system became known as intents.

**Privileged Intents**

Around December 2019, there were discussions about a new feature named intents in the Discord Infrastructure server. The goal of this system was to have a more granular approach in disabling events that so many bot developers had hoped for. This change would, presumably, be backwards compatible with the way things were done at the time. Unfortunately, at the same time, there were growing concerns with a user-bot ring that made a website and scraper known as "dis.cool", which farmed user information.

Discord presumably saw this growing user-bot ring as a liability threat and introduced the concept of "Privileged Intents" and discussed the plan with the Discord Infrastructure server, again without consulting library developers about it. My mole in the Discord Infrastructure server then gave me a [gist][privileged-intents-lite] of the original plan for privileged intents. It became clear that this was not the feature that we had been requesting for years, but rather that they were added restrictions that were created due to a false equivalency between user-bots and real bots.

At this point, I had asked the Discord employees what intents were, and they retorted by asking me where I had heard of such a feature – implying its secrecy. Hoping to not give away my now primary source of information, I did not indulge too much information on the source. However, eventually the Discord employees divulged and gave us a quick rundown of the basics of the concept. The next day, they gave us the same gist and talked to us about it.

The original specification of intents only had `PRESENCE_UPDATE` as the privileged intent. For "large bots" over 100 servers, this would block your ability to join more servers unless you explicitly requested approval from Discord or turned off the intent. At the time, the whitelisting process would amount to a checkbox and a text box that you would fill out to give Discord a rationale on why you needed it, optionally attaching a video showing your bot's usage of the feature.

Most library developers and contributors were not happy with the changes, since the way bureaucracy historically was handled at Discord would mean that the bot would silently break while waiting for a response from Discord. At the time, the large bot sharding system that bots in over 250,000 servers had to apply for was already behind, so there were growing concerns about the effect bureaucracy would have on our bots. We were promised that the system would be fine and that the bureaucracy would not have a negative effect.

There were significant arguments from both sides over whether the privileged intent system accomplished anything. Most library developers felt the changes were misdirected and targeted the wrong type of bot. The threat model was based on user-bots being bad actors, and not regular bots, while the changes targeted regular bots. We also felt that it was easy to sidestep the restrictions by just having a bot ring, similar to what is now done today with user-bots.

Discord repeatedly mentioned that the 100 server threshold would have minimal impact and that most bots were not past that limit. To us, large bots are bots well over 100 servers and into the 100k+ territory. At the time, the `PRESENCE_UPDATE` event was heavily overloaded, providing not only presences and statuses but also user level updates (such as name, avatar, and discriminator) as well. We were told that before the change went live that they would split it, and that was indeed done in v8 of the API, 10 months later.

After a lot of discussion with the Discord employees with them telling us that they were listening to our feedback, they decided that the `GUILD_MEMBERS` intent was going to be privileged as well. The `GUILD_MEMBERS` intent is the intent that controls whether you get member information over the gateway and is the heart and soul of how member level events are dispatched via libraries. This intent is also required for any local caching of members. At the time, there weren't enough events that provided the member data, so this meant that usability of every library across the board would suffer. The Discord employees maintained the opinion that this change would be a net benefit and that the bureaucratic aspects of it would only be two text boxes and checkboxes that anyone could fill out.

There was a lot of uproar over this addition, not just within the Discord API server, but also on [GitHub][member-intent-github]. To this day, that GitHub pull request has the most discussion out of all the issues and pull requests for the repository. This was because, at the time, member data was necessary for a large amount of functionality within the API, such as checking permissions and moderating. Likewise, the Discord employees claimed that the blowback to the bureaucracy would be minimal and that all the bots would be verified within one day. They also claimed that in the future, member data should become unnecessary. The deadline for conforming to these changes was October 27th 2020. The date of the introduction of this intent was February 3rd 2020.

They assured us that they were listening to our feedback.

**Verification**

After the large amount of discussion involving privileged intents, taking place over the course of around 3 months, most of the library developers, contributors, and Discord employees were drained from the conversation. As a result, after this, communication with us went essentially radio silent. We hadn't spoken to any Discord employees about anything, except a sneak peek of the `allowed_mentions` functionality early in February, slightly after the initial blowback.

We didn't find out what Discord planned on doing until they unveiled their plan for the future in a [blog post][discord-future-blog-post] on April 7th 2020. In this blog post, the Bot & API Team unveiled their future vision for the platform by showcasing Figma examples about how they hoped to have bots integrated within the ecosystem. There were many concepts shown, such as context menus, buttons, and ephemeral messages. Many of us were finally excited for the changes to come.

Unfortunately, along with the news about the future of the platform came a caveat about additional restrictions to the platform. No longer would we have to fill out just a regular two text and checkbox form, but instead an entire questionnaire would need to be filled out. On top of this, a government-issued ID would need to be provided in order to verify your bot to receive a verification checkmark on it, along with a profile badge (that was later discontinued). It no longer became possible to get whitelisted for the privileged intent without going through the privacy-invasive verification system. It was no longer possible to have your bot join over 100 servers at all without going through this verification system.

Discord claimed it would help with security and privacy by preventing malicious bots from growing and obtaining sensitive data. The library developers responded that it wouldn't help since malicious bots  had to be invited and the crux of malicious bots were, and still are, user-bots. Not to mention that in the previous proposal, disallowing the so-called malicious privileged intents would still allow your bot to grow past 100 servers. The final proposal revealed by the blog post had made it so joining any server past 100 would require verification using a government-issued ID regardless of whether you had privileged intents disabled or not.

Since there was a lot of pushback on this topic, I made a form to get opinions from the developer ecosystem at the time and received around 1600 responses. I had planned to share it with Discord with hopes of maybe changing their mind on the concept or giving them insight into how developers felt, but they told me that my sample size was too small to be considered. Anyone with a passing knowledge of statistics would know that a sample size of 1600 is not insignificant. Nevertheless, most people who did the survey did not enjoy the idea of sharing their government-issued ID to verify their bot:

![Bot Developer Survey 1](https://user-images.githubusercontent.com/1695103/128839688-a764722c-a449-45d2-8273-1b94ce0d6cae.png)

There was a lot of data concerning how bot developers felt about the change that I ultimately couldn't present to the Discord employees due to them not wanting it. At around this point in time, most of my motivation was waning. I was against the verification system at its core, since I considered it invasive and unnecessary. When asking an innocent question to Mason, the Project Manager of the Bot & API team, about whether my bot could connect to the gateway without being verified, he responded rudely and called me a "martyr" with an unnecessarily threatening tone:

![Mason calling me a martyr](https://user-images.githubusercontent.com/1695103/128839762-7f7e6b9c-ef66-496b-ad69-5bd544ac78f0.png)

**Bureaucratic Disaster**

Following the intention to verify bots in the ecosystem, the support staff was immediately overwhelmed with the requests, causing their previous 5-day SLA promise to completely fall apart. The entire Bot & API Team had to work together to ensure that they could meet the demand of people verifying their bots. However, despite their best efforts, they were behind consistently for multiple weeks, even months, throughout the entire year of 2020, and this still continues to this day in 2021.

Discord had originally used the "Verified Bot Developer" badge as an incentive to get people to be "recognised" for their efforts within the ecosystem. According to them, this led to an influx of people applying for verification for the sole purpose of the badge. Eventually, they revoked the badge entirely and changed the badge name to "Early Verified Bot Developer". By not removing the badge instead, this had the consequence of feeding into the account black market. The resulting outrage from the bot developers who did not get a badge after the arbitrary cut-off was large enough that Discord employees rewrote history and handed out mutes for people who were just asking for the badge. They called this behaviour "badgeposting".

![Badgeposting]
(https://user-images.githubusercontent.com/1695103/128840429-bd7822b9-599a-4d98-a4c1-37faff1067c7.png)

![History being rewritten]
(https://user-images.githubusercontent.com/1695103/128839827-94b504b0-b7cb-4104-82b6-506fe6b060a6.png)

Discord consistently made promises all throughout 2020 that they were going to meet their fabled 5-day SLA. Despite Discord blaming badges for congesting the verification queue, the problem was not solved. I do not personally see a future where this consistent 5-day SLA happens. Despite hiring more support staff to handle the queue, it is still a month behind and is only going to get worse as more people will need to re-apply for their intents request in the following months before the deadline.

**Slash Commands**

Around July and August 2020, the Discord employees started talking to the people in the Discord Infrastructure server about the possibility of Slash Commands finally coming to Discord. This feature was one that had been in the talks since the very beginning of Discord's history, so some people were hyped it was finally coming. Unfortunately, at around the same time, Discord employees were hinting that message content would be removed or restricted.

![Discord Infrastructure Leak]
(https://user-images.githubusercontent.com/1695103/128839881-a17407aa-cc4d-4d7c-a4f7-6028357f5e9b.png)

After my mole shared these images with me, I decided to share them with the remaining library developers in our private server. We began to see the introduction of Slash Commands as a way to destroy our old work. At this point, Slash Commands were not actually released. They were mainly in the development phase. However, we figured that when Slash Commands would be introduced to the public, that they would remove message content along with it.

Shortly after, the people in the Discord Infrastructure server got an early access beta for the implementation of Slash Commands. My mole also gave me the gist (not publicly available) explaining how the system was going to work. The Discord employees did not share this gist or information with us until later. When they finally shared the gist with us, they planned to have a meeting with us about how they wanted the system to work. I did not participate due to it taking place while I was at work. The library developers who participated said they shared a lot of feedback for how they wanted Slash Commands to work. Most of this feedback ended up being discarded.

When the Slash Commands beta reached the public phase, a lot of the general public ended up repeating the same criticisms and feedback that the library developers and the big bot developers had shared with the Bot & API team. After some amount of pressure from the community, they did finally implement some changes, though permissions remained a massive pain point. Fundamentally, Slash Commands had a fatal flaw: they weren't tied to a user. This meant that traditional permissions did not function with Slash Commands. For traditional bots, the administrator of a server could block specific bots on a per-channel basis by blocking the Read Messages permission. For a Slash Command bot, this would no longer possible since Slash Commands **bypassed** all forms of permissions.

We were told that the permissions system would improve over time, though this never ended up materialising. The ability for a Slash Command (aka an Interaction) to bypass the `@everyone` permission wasn't fixed until May 2021, 6 months after it had already been reported.

**Message Content Privileged Intent**

Around early June 2021, the top 8 most popular library developers were contacted regarding a special meeting about a topic that was important to all of us in the ecosystem. Knowing what we knew about the message intent, we figured that this would be the last chance we would get in order to defend the ecosystem from breakage and hopefully get them to change their minds on the entire thing. The meeting was bound by an NDA, which made us reluctant to sign it, but since we believed and were told that this would be our final chance to get a seat at the table for this change, we all agreed with the sole purpose of convincing the developers that this direction was a bad idea.

Unfortunately, due to being legally bound by this NDA, I cannot share too many details. However, I will mention that the morale from all the library developers fell quite fast.

All of us library developers were against the change for message content to become a privileged intent. It falls under the same bureaucratic issues that regular privileged intents suffer from, except with more devastating consequences. A lot of current bots in the ecosystem are faced with a choice of either getting rewritten to comply with changes I believe to be unnecessary, or to die. Discord seems to believe that this change is for the better – but no alternative path was explored or brought up. Instead, they opted to deploy the nuclear option and are hoping to fix the problem that way. Discord also believes that most bots will fully migrate over within the timeline given. I do not believe that this will be the case.

**Future Direction**

Discord has a lot of things planned in order to make the transition easier for users in the future. I'm not sure whether they'll actually finish all these planned improvements between now and the deadline. Historically, they've only managed to finish these changes a month before the deadline kicks in. Rather than improving the system before forcing it onto users, they have decided to announce the changes first and then promise on good faith that they will implement the necessary features to make the transition smooth. This gives bot developers no time to actually accommodate their bot for the changes, in case a feature they depend on for the migration doesn't exist yet.

Discord has already began rushing features in a sloppy and hasty manner. One of the newer features, context menus, has had a lot of feedback from many library developers and bot developers asking for the type to be overhauled and split to prevent library breakage and make the API more intuitive to understand. Despite this narrow feedback being provided by most users in the private beta for the feature, it has been explicitly ignored with the Discord employees claiming that [they just wanted to get something out quickly][context-menu-change].

![Minn's response to night]
(https://user-images.githubusercontent.com/1695103/128839928-88a95d20-16c7-48e5-9000-2a871a2934c5.png)

I do not believe in waiting on promises for something to be better, when historically these promises have been empty. I do not think the situation will radically improve by April 2022 and do not think this change is worth the everlasting impact it will have on the ecosystem. Unfortunately, this decision is final, and the only thing I can feasibly do at this stage is to watch from afar. I do not have the motivation to keep up with an ecosystem I no longer believe in. I wanted a rich bot ecosystem to thrive and flourish, for bots to reach their full potential, yet Discord has repeatedly decided that limitations are a better route. This is why I have decided to step down as maintainer of this project. My involvement in discord.py and the API was always fuelled by passion and hope. These recent changes have drained me completely of both of those things.

**FAQ**

I imagine there are going to be a lot of questions from people who want the nitty-gritty.

**Why are you stopping development?**

My motivation to work on Discord has been dwindling over the past year, since the verification system was introduced. Persistent tone deafness, deadlines, lies, gaslighting, and rapid changes without proper consultation by the Discord employees make it hard to have the motivation necessary to work with the frequent changes and the limitations being placed on me.

To me, the message content privileged intent signals the end of the creative freedom and grassroots hacking us library developers all believed in. The control is now inverted and things are being built around Discord's limitations. No longer will bots thrive with a sandbox limited only by your imagination, but instead Discord is now the sole gatekeeper of approved use cases. The future of Discord bots relies solely on the interaction system; things have to be explicitly written and supported by Discord employees, with creative solutions being put aside. I wouldn't be surprised if in the future, the entire gateway API becomes restricted and deprecated, with the only recommended way remaining to create a bot being entirely interaction or HTTP based. I have no real hope for the future of Discord bots.

However, I don't want to give the impression that the things Discord is building are not cool. They are indeed very cool. Things like buttons and UI extensions are features that we've been wanting since 2016, and it's great to see them in the platform. It's just that it's coupled with a tough pill to swallow that damages the ecosystem as a whole. A price I'm not exactly willing to pay.

**What happens now?**

Development will cease and the repository will be put into a read-only mode.

**What can I do about this?**

Unfortunately, there isn't much you can do to stop this train other than telling Discord your opinion on the changes. The thought of the ecosystem breaking has caused me a great deal of stress and mental anguish. I've spent the better half of the past 2 months attempting to convey the distress I feel to various Discord employees to no avail. Discord seems to believe that everything will be fine in 9 months time, but I do not subscribe to this thought process.

**What's going to happen to my bot?**

This change is radical, even if I was removed from the equation. Discord expects all bots to migrate over to Slash Commands by April 2022 – whether I do anything to help or not. My proposed API I had for Slash Commands is incompatible with the current code for the commands extension due to the two systems being fundamentally different in paradigm. This means that no matter what path I would have chosen to take, a vast majority of library users would have needed to rewrite their code anyway.

It should be noted that Discord wants all bots over 75 guilds to migrate over to Slash Commands in the foreseeable future. If you want to apply for the message content intent, you **cannot** use it for command handling purposes; they will explicitly deny you the intent. Therefore, effectively everyone must move over to Slash Commands for their bot to function.

![Discord Employee's Statement on Message Content Intent]
(https://user-images.githubusercontent.com/1695103/129664615-3ec46e4e-38e7-4a89-ba1c-ff7c3d70ce9e.png)

![Kady's statement on Message Content Intent]
(https://user-images.githubusercontent.com/1695103/131197302-08f128cb-af2b-4a4b-b5e6-20e84658b324.png)

**I want my bot to continue working!**

During the Developer Q&A session on August 4th, Mason, the Project Manager of the Bot & API team, encouraged you to rewrite your bot since it's "easy" and "dope". 

![Question from the Q&A]
(https://user-images.githubusercontent.com/1695103/128839984-9e6adbe6-31f5-4270-afc4-dcbdc0843ac8.png)

> Uh, popular libraries. So, we obviously do not have control over third party libraries. They are third party. Um, we try to work with them very closely to keep them informed of changes, uh and to answer their questions about implementation and API and consistencies and "Hey does this API suck or not". Uh, Slash Commands have been in an open developer beta since December of last year. Changes are not happening until an additional 9 months from now. Which will make it 1 year and 4 months slash 16 months if I know how to do math correctly since Slash Commands were first released. Um many libraries do have support. Some have unofficial forks. I will also say that for those intrepid developers they are pretty well usable without libraries but I know that that is a much sort of bigger task to undertake. Um but if you haven't checked out using Slash Commands over HTTP and outgoing webhooks, it's pretty dope and really easily scalable.

Therefore, if you want your bot to continue working you have a few options:

1. Implement the slash command system yourself. The library (v2) provides `on_interaction` to help you do this, and all the endpoints are technically in `bot.http`.
2. Implement the slash command system using the raw API.
3. Wait for a competing discord.py fork to arrive.
4. Rewrite your bot using a new library or in a different programming language.

## Won't things be fine in April 2022? There's enough time!

Discord has repeatedly stated that they believe things will be fine by April 2022:

![Kady's statement]
(https://user-images.githubusercontent.com/1695103/128840026-87d7a66f-4c5f-4a8a-92cd-5c60ba4c068c.png)

However, the reality of the situation is that a significant number of libraries do not implement Slash Commands. The following is a table of support:

|      Library       |  Implementation State |             Notes              |
| :----------------: | :-------------------: | ------------------------------ |
|     discord.py     |    Not Implemented    |                                |
|    Discord.NET     |    Not Implemented    |                                |
|      disgord       |    Not Implemented    |                                |
|     discordjl      |    Not Implemented    |                                |
|      Dimscord      |    Not Implemented    |                                |
|     DSharpPlus     |    Not Implemented    |                                |
|     DiscordPHP     |    Not Implemented    | Implementation no longer works |
| Sleepy Discord C++ | Partially Implemented | Unstable/Unreleased            |
|     Discordia      | Partially Implemented | Unstable/Unreleased            |
|        Eris        | Partially Implemented | Unstable/Unreleased            |
|     discord.rb     | Partially Implemented | Unstable/Unreleased            |
|     discordgo      | Partially Implemented | Unstable/Unreleased            |
|        nyxx        | Partially Implemented | Unreleased                     |
|      Ackcord       | Partially Implemented | Unreleased                     |
|     discord.js     |      Implemented      |                                |
|        JDA         |      Implemented      |                                |
|     Discord4J      |      Implemented      |                                |
|      Javacord      |      Implemented      |                                |
|      Serenity      |      Implemented      |                                |
|      Twilight      |      Implemented      |                                |
|      nostrum       |      Implemented      |                                |
|        Kord        |      Implemented      |                                |

These are libraries that implement it in any capacity, whether in a master branch or in another branch. Discord is expecting not only for the remaining libraries to implement the entire Slash Commands functionality, but also for all the users to migrate by the deadline. People have other responsibilities that don't revolve around Discord's ecosystem, so requesting all these users to do this is absurd.

## Discord will give us messages that mention us, that means everything will be better... right?

Unfortunately, no. This is a small bandage over a very large wound. In reality everything bad about the message intent, as mentioned earlier, still applies despite receiving messages that the bot is mentioned in. Even in this utopia where bot developers maintain their message content commands, by virtue this means that users will all have to relearn the bot prefix, which will be bad for usability.

## Can I take over the library for you? I can maintain it!

Unfortunately, I do not plan on giving maintainership status to those I do not trust. There is a security issue at play here that I do not feel comfortable with, where an unknown third party could upload malware targeting a bunch of Discord users. It should be noted that I did ask everyone who I was willing to give this library to, and they all declined, respected my decision, and agreed with me that they did not like the direction Discord is going.

You are, however, free to fork the project yourself and implement the improvements that you seek.

## Why not implement Slash Commands?

In the simplest words: it's not fun. It's not particularly hard to implement slash commands for me, and I already had a mostly working, yet woefully incomplete, local copy made back in May 2021. However, my motivation to continue working on it is pretty much non-existent at this point. Slash Commands represent a change in direction within Discord that I fundamentally do not agree with. It is unfortunate that this feature was rushed out the door in order to add more restrictions to the platform.

Note that my Slash Command implementation was completely different from the `discord.ext.commands` implementation since the two models are strictly incompatible. So even if I had released my implementation, most users would have had to completely rewrite their bot to support it.

## What happens to the discord.py server?

Ideally, nothing. I don't plan on doing anything to the server and it can remain as-is. The library still functions and there's still a lot of code out there written in discord.py. More importantly, the server holds a special place in my heart with a community I'm proud of and I see no reason to burn it to ashes.

## What about the Discord API server?

Same thing. Nothing will happen there.

## What's going to happen to R. Danny?

Due to the message content intent happening in the future, my bot will more than likely die since it won't be able to moderate. If you want to know what my bot means to me, I wrote a separate [write-up][r-danny-blog] on the topic when I was discussing this with Discord staff.

## Would you ever consider picking the project up again?

I'm not sure. This decision came from multiple years of grievances from the Discord employees that would just be too much for me to detail in this document. I don't think they'll be fixed or be any better in the future, but only time will tell.

If it weren't for the direction Discord decided to take, I would have loved to continue working on discord.py. I actually really enjoyed working on this library and there were many things I would have liked to explore should time have permitted me to do so. However, underneath everything that the library does is the corporate entity that has repeatedly caused me these grievances that I've amassed over the years. It's hard to separate the two.

## My question isn't here!

My bad. If more questions pop up during the announcement I'll add them back here, or you can just ask me directly in the discord.py server and I'll try to answer.

## I'm really mad at you!

Sorry.

# Acknowledgements

I'd like to thank the following people for all the help and support they've given me over the years, in alphabetical order.

- aj. Thanks for being the most responsive Discord staff I've ever been in contact with. Your willingness and proactivity when working with us was unparalleled and much appreciated.
- Bryan Forbes. Thanks for taking the time and effort to type hint the library initially. It was of great help.
- Gary. Thanks for being a supporter in the discord.py server and for being so kind to everyone in the server and to me. I greatly appreciate it.
- Hornwitser. Thanks for providing early design feedback for discord.py and untangling the spaghetti in the initial dispatch code.
- Ian Mitchell. Thanks for listening to my incoherent rants and frustration and trying to make things better.
- Ian Webster. Thanks for actually being kind enough to communicate with us when things went way south.
- Imayhaveborkedit. Thanks for being the go-to voice wrangler all these years when I couldn't be bothered.
- Jake. Thanks for actually being our pillar and maintaining the sanity in our Discord API server. Without you, we would have lost our vanity and many more things would have been worse. We'd often say that without your presence our server would cease to exist.
- LeoV. Thanks for being there early on and helping design the logo for the documentation.
- "Mole", you know who you are. Thanks for shedding light into the inequality that us library developers faced.
- NCPlayz. Thanks for being one of the only other persistent contributors to the library. Without you, implementing some features would have been too taxing to do alone.
- spoopy. Thanks for maintaining the code early on and providing invaluable feedback.
- Stanislav. Thanks for being our go-to contact early on in the API days. It was fun.
- The discord.py community. Thanks for being you.
- The other library developers. Thanks for sticking together through all the nonsense. Without our unity I'm pretty sure I would have quit long ago.
- The Red-DiscordBot community. Thanks for being kind and respectful to me. The feedback you guys gave when working with the command framework was invaluable to me.
- The various contributors for discord.py. Thanks for improving various things throughout the library; even the most minor contribution has a large impact.
- The various helpers in the discord.py server. Thanks for taking on a bulk of the hard work which usually goes unappreciated.

And of course, thanks to you for reading through all this.

Until next time.

[discord-blog-dapi]: https://blog.discord.com/the-robot-revolution-has-unofficially-begun-unofficial-api-23a3c722d5bf
[r-danny-blog]: https://gist.github.com/Rapptz/99cf4c1ab8b5ce584e2bf0b7ba88d5f8
[privileged-intents-lite]: https://gist.github.com/msciotti/223272a6f976ce4fda22d271c23d72d9
[member-intent-github]: https://github.com/discord/discord-api-docs/pull/1307
[discord-future-blog-post]: https://blog.discord.com/the-future-of-bots-on-discord-4e6e050ab52e
[context-menu-change]: https://github.com/discord/discord-api-docs/discussions/3590#discussioncomment-1135214
