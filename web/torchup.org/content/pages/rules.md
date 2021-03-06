Title: Rules
Date: 2020-01-22 16:20

The following rules should be read in the context of fair play.

Administration tries to provide authors participating in the tournament with a working environment, but can not guarantee activity. It's bot authors duty to do all necessary to not stall the procedure.

The spirit of the rules should be followed, rather than the wording.

## Available hardware
Every AI run inside its own Linux container and have the following hardware reserved with no shared resources between competitors.

- Operating System: Debian 10 64-bit
- Processor: 4 vCPU Xeon E5-2686 at 2.7 GHz
- Graphics Card: 1 NVIDIA Tesla M60
- System Memory: 8 GB RAM
- HDD free space: 4.7 GB

If your system require the allocation of additional vCPU's or GPU's please [contact us](https://torchup.org/pages/contact/), we are happy to help with your submission process.

## Programming languages
This competition officially supports Lua, Python, C++ and Java.

We also offer unofficial support for anything with a working BWAPI wrapper available in supported BWAPI versions, please [contact us](https://torchup.org/pages/contact/) if your bot is under this category and you want to compete.

## Tournament Structure
The tournament will be round-robin, with as many rounds as possible, starting on Monday January 27th until Friday January 31th, 2020.

The round format is 1v1, best-of-99 games per match, bots always play exactly 99 games per match to determine the winner of that match.

### Tournament winner

The top bots will play best-of-9 games in a single elimination bracket seeded 1st place against 4th place, 2nd place against 3rd place.

### BWAPI Versions
The following BWAPI [release versions](https://torchup.org/files/bwapi.zip) will be supported this year:

Version `4.1.2, 4.2.0, 4.4.0`.

You are not allowed to use of other BWAPI version.

### Maps
The official maps for the event are:
```
(4) Circuit Breaker,
(3) Aztec 2.1,
(2) Heartbreak Ridge,
(4) Gladiator 1.1,
(3) Gold Rush,
(2) Blue Storm 1.2,
(4) Fighting Spirit 1.3,
(3) Power Bond,
(2) Overwatch 2.2,
(4) Sparkle 1.1 (optional) challenge.
```
*NOTE* Sparkle is used after the main event for a completely optional `Island challenge` round with clean `bwapi-data/read/` and `bwapi-data/write/` directories, bot authors could opt out of this round at any time without this affecting the tournament results.

[click here](https://torchup.org/files/maps.zip), to download them on zip file.

### Game Type
The game type for the competition will be 1 vs. 1 Melee full game StarCraft: BroodWar 1.16.1 with fog of war enabled.

### Time Limit
Games will have a `frame limit` of `86400 frames`, to simulate one hour of gameplay. If a game goes this long, it will be stopped and the in-game score will be used to determine the winner.

### Conflict of Interest
Organizing AND participating in events like this can be tricky, we address these problems as follows:

Before accepting submissions, we will distribute the `SHA-2` check sums of our bot to all participants. This way, participants can be confident that we will not change our entry after running their submitted program.

## Software Requirements
### All bot types are welcome!
All open-source or closed source entries, submission folders will be published on this website once the competition has finished.

### Game Speed
All games will be played in a LAN UDP network game between the two players at setLocalSpeed(0) with no delay between each frame, so simulation will be as fast as possible and the Game Speed slider in the game lobby set to "Normal" (i.e. latency frames = 3, also known as LF3).

## Persistent File I/O
File I/O will work the same way as AIIDE StarCraft AI Competition Rules. You will have read access to folder `bwapi-data/read/` and write access to folder `bwapi-data/write/`, both of which will be in the standard location under the StarCraft root directory.
*IMPORTANT*: File I/O works as follows:

1. Before each game, the contents of the server-side read directory for your bot are copied to the client machine under `bwapi-data/read/`. For the first round of the tournament this directory will be blank since a full round has not yet been played.
2. During a game, you have write access to the `bwapi-data/write/` folder and read access to the `bwapi-data/read/` folder on the client you are currently playing on
3. After the game ends, the contents of the `bwapi-data/read/` folder are deleted, and the contents of the `bwapi-data/write/` folder are sent to the server and stored in your bot's server-side write folder.
4. *WARNING*: Step 3 may overwrite previous results if you are not careful in specifying unique filenames for each opponent that you play against.
5. After each bot has played each other bot on the current map (one round robin on that map) the contents of each bot's server-side write folder are copied into the respective server-side read folder and the write folder is cleared.
6. *WARNING*: Step 5 will over-write previous round data inside the server-side read folder. Your file output must either be cumulative, or have a filename scheme such that no overwrites will happen in order for your data to be preserved.
7. The bot's server-side read folder is NEVER deleted throughout the tournament
8. The next round starts, and from step 1 you will have access to your server-side read data from the previous rounds inside the client's `bwapi-data/read/` folder

Due to the nature of overwriting the read folder, your file names should be unique at least to the current opponent.

## Detailed Rules
No entry fee.

Accessing the internet/network is generally permitted.

All replay files and bot binaries will be made publicly available after the contest.

StarCraft Brood War version 1.16.1 will be used for all games.

All the games are 1 vs. 1 Game type is set to Melee.

Race either Terran, Protoss or Zerg, (Not allowed to Choose Random).

Bots that perform malicious behavior will be disqualified and banned from all future contests. This includes but is not limited to:

- Install worms/viruses/malware on the host machine.

- Intentionally crash StarCraft.

- Spam the in-game console.

- Change the already pre-set current working directory (CWD) of the process.

- Read and write files outside of the CWD (read-only), ‘bwapi-data/read/’ (read-only), ‘bwapi-data/write/ and ‘bwapi-data/AI’ (read-only).

- Up to 4.7 GB of disk space total for your `bwapi-data/read/` + `bwapi-data/write/` + `bwapi-data/AI/` directories.

- Malicious utilization of resources such as sockets, files, zombie processes (Using 100% RAM and 100% CPU is permitted).

- Retrieve / store system or user information, e.g. username, hostname, IP address, network information, operating system type/version, CPU type/model/details, system time zone/offsets and other location/locale information (note: dates/times are ok so long as you don’t identify the time zone/offset).

- Bots that behave suspiciously, don't run, crash/hang/timeout too much, or lag too much (e.g. lagging client based bots that the tournament module can't detect) may be disqualified after some investigation.

- Use the system for other purposes, e.g. cryptomining, etc.

Programs that attempt to cheat will be disqualified. See the other points about StarCraft bugs/tricks and bugs/exploits. Also, this includes but is not limited to:

- Bots must *NOT* enable the complete map information flag (BWAPI::Flag::CompleteMapInformation).

- Use the getRandomSeed() method for decision making, e.g. inferring enemy start location or race.

Games in which an agent crashes StarCraft will be counted as a loss.

Games will be run on [Debian](https://debian.org) stable 64-bit inside [Singularity](https://github.com/sylabs/singularity) containers.

Entries must be tested to work on the [maps](https://torchup.org/files/maps.zip) before submission.

We will not be held responsible for entries that crash StarCraft due to our configuration of the system.

Games will be run in a semi-automated fashion.

Bots must not slow down the game speed on purpose:

- All games will be played in a LAN UDP network game between the two players at setLocalSpeed(0), please make sure that your bot functions correctly on this setting.

- To avoid problems, base your 'timings' on unit counts or getFrameCount() and not machine time.

- Your bot *MUST NOT* call setLocalSpeed() or setFrameSkip() during the competition. Not even setLocalSpeed(0) or setFrameSkip(0).  We suggest you comment out all calls to them.

- Games will be run using the Game Speed slider in the game lobby set to the default which is "Normal" (i.e. latency frames = 3, also known as LF3).

- Games in which a bot crash or slows down the game speed on purpose will be counted as a loss.

- If your bot always crash or is slow too often without any apparent reason, your bot *WILL BE* disqualified.  It may be disabled part-way through the competition. The results for all games involving the bot will be ignored and excluded, by this particular case  administration reserve the right to decide whether to restart the competition or run from scratch.

Participants are not required to disclose bot source code but may provide a short description of implementation details.

Entries are allowed to make use of free open-source software components and close source software as well.

Bots are not allowed to pause the game, games in which a bot pauses the game will be counted as a loss.

The following StarCraft bugs/tricks are permitted:

- Stacked Recall

- Plague on interceptor

- Units pressed through

- Drops to defuse mines

- Mineral walk

- Manner Pylon

- Lurker hold position

- Observer over turret

- Stacking air units

All other bugs/exploits are forbidden. Bots caught attempted these exploits will be disqualified. 

This includes but is not limit to:

- Flying drones and templars

- Terran sliding buildings

- Stacking non-burrowed ground units is forbidden except when you are using "Mineral walk" or "Units pressed through" or "Stacked Recall". E.g. stacking your workers using "gas walk" is forbidden.

- Allied mines

- Gas walk (in all cases including: to get through blocked entrances or ramps; to attack any units)

Bad mannered in game behavior is discouraged, but not forbidden.

Bot names can only contain alphanumeric characters with no spaces, e.g. "ExampleBot", not "Example bot".

Bots are not allowed play random race, bots must choose and stay one race for the entire event.

The `bwapi-data/read/` and `bwapi-data/write/` folders for participating bots will be cleared after testing. Every bot’s `bwapi-data/read/` and `bwapi-data/write/` folders will be empty at the start of the competition. Entries are not allowed to submit files for their bot to read from `bwapi-data/read/`. If your bot needs static files such as configuration files or pre-trained data, please ensure you bot reads such files from the `bwapi-data/AI/` folder, not from the `bwapi-data/read/` folder. The purpose of the `bwapi-data/read/` folder is for reading data that your bot previously wrote during earlier games in this competition.

Bots might be used to play against humans in show-matches using Game Speed slider in the game lobby set to “Normal”, i.e. LF3

The bot submissions from the authors, the bot binaries plus any initial configuration/pre-trained data that was actually used during the competition, replays, read/write folders, detailed game results table and summary tables/charts etc will be published on the `updates` section of this website.

If you copy other bots or use IP/files/source code/logic/techniques etc from other bots, you must familiarize yourself with their licenses and ensure that you are not infringing their licenses. Copying other bot(s) is allowed, so long as it does not infringe their licenses and so long as you modify their logic or if you use/wrap it without modifying it and add some of your own logic on top of it.

If you copy a bot, please uphold the spirit of competition and ensure you make significant modification or addition before you submit it. We don’t want multiple apparently near-identical copies of the same bot competing!

Please *DO NOT* have any logic that only works on a specific version of windows or specific types of environment or only works on a hard-coded list of bot names that register. Entries must run/play properly when run in other similar environments and against other players. This is so that they can easily be used in next year’s competition – the players will be different, and the environment might be different – and so that they can easily be used in future by other researchers / developers / competitions. Bots should run/play properly regardless of what context it is run in. 

Rules are not necessarily retrospective when applied to re-used entries from past years – the rules that applied during the corresponding old year apply to each re-used entry, but newer/updated rules may or may not be applied, at the discretion of the competition organizers.

