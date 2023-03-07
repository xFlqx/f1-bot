# 🏁 f1-bot
A Discord bot to view F1 stats.

## Description
A simple bot application incorporating the [discord.py](https://github.com/Rapptz/discord.py/tree/rewrite) library to view Formula 1 statistics within Discord. The bot pulls data from [Ergast](http://ergast.com/mrd/) API using commands invoked by Discord members, displaying data such as championship standings and details about upcoming races.

## Commands

**Parameters**

`[ ]` = Optional;
`< >` = Required

Commands which take `season` and `round` parameters will default to the latest race of the current season if omitted. Otherwise, both parameters should be given as a pair in the order `season` `round`, except the `wdc`, `wcc` and `grid` commands which only use an optional `season` parameter.

Commands which take the `driver_id` parameter must be either of the following:
  - Driver code; e.g. HAM, VET
  - Driver number; e.g. 44, 55
  - Ergast API ID; Typically, this is the driver's surnane, e.g. 'alonso', 'vettel'. However, in cases where the surname applies to multiple drivers, the ID will be `firstname_surname`, e.g. 'michael_schumacher', 'max_verstappen'.

Depending on the configuration, some commands will respond with a DM to avoid cluttering the text channel, this can be temporarily overridden for a command by including `no-dm` or `public` in the parameters, e.g. `!f1 wdc no-dm`.

**Usage**

Invoke a command in Discord by typing the prefix `!f1` (symbol can be changed in config) and one of the following subcommands:

- `!f1 help [command]` - Display help text for the available commands

- `!f1 status` - Information about the bot and connection status

- `!f1 discord` - A link to the support discord.

- `!f1 wdc [season]` - Display World Driver Championship standings.

- `!f1 wcc [season]` - Display Constructors Championship standings.

- `!f1 grid [season]` - Return details of all drivers and teams participating in the season.

- `!f1 schedule` - Display the race calendar for the current season.

- `!f1 next` - Show a countdown to the next race and details.

- `!f1 results [<season> <round>]` - Race results for `[round]` in `[season]`.

- `!f1 quali [<season> <round>]` - Qualifying results for `[round]` in `[season]`.

- `!f1 career <driver_id>` - Career stats for the driver.

- `!f1 stops <filter> [<season> <round>]`

  Display pit stops. Data not available for seasons before 2012.

  The `<filter>` parameter is **required** and must be one of the following:
  - `driver_id` - Get all stops for the specified driver
  - `top` - Top 5 fastest pit stops
  - `bottom` -  Bottom 5 slowest pit stops
  - `fastest` - Fastest ranked pit stop
  - `slowest` - Slowest ranked pit stop

- `!f1 best [filter] [<season> <round>]`

  Display best lap time per driver. When searching a specific `season` and `round`, the `[filter]` must be given first. You can use the `all` value if you don't actually want to filter the results. No parameters will return all best laps for the most recent race.

  Options for `[filter]` keyword:
  - `all` - Do not apply filter
  - `top` - Top 5 fastest laps of the race
  - `bottom` -  Bottom 5 slowest laps of the race
  - `fastest` - Fastest ranked lap
  - `slowest` - Slowest ranked lap


**Generating Plots**

The following `!f1 plot` subcommands will generate a chart uploaded as an image to the discord channel:

- `!f1 plot stints [<season> <round>]`

  Plot each driver's race stints and pit stops as a stacked bar chart.
- `!f1 plot fastest [<season> <round>] [drivers]`

  Plot fastest race lap as a bar chart. Both `season` and `round` must be given **before** any `drivers`. Using the command without parameters will return all latest results.
  - `[drivers]` may be multiple drivers to compare separated by a space; not specifying any drivers or using `all` will plot all drivers. Limiting drivers will result in a more legible graph.
  - E.g. `!f1 plot fastest 2019 1 BOT HAM VET`

- `!f1 plot timings [<season> <round>] [drivers]`

  Plot each lap time per lap of the race as a line graph. Both `season` and `round` must be given **before** any `drivers`. Using the command without parameters will return all latest results.
  - `[drivers]` may be multiple drivers to compare separated by a space; not specifying any drivers or using `all` will plot all drivers. Limiting drivers will result in a more legible graph.
  - E.g. `!f1 plot timings 2019 1 BOT HAM VET`

- `!f1 plot position [<season> <round>] [drivers]`

  Plot race position per lap of the race. Both `season` and `round` must be given **before** any `drivers`. Using the command without parameters will return all latest results.
  - `[drivers]` may be multiple drivers to compare separated by a space; not specifying any drivers or using `all` will plot for all drivers. Limiting drivers will result in a more legible graph.
  - E.g. `!f1 plot pos 2019 1 BOT HAM VET`

**NOTICE:** Both `plot timings` and `plot positions` may take some time to process as all lap data must be gathered from the external API. Please avoid excessive use of these commands and wait for the results to finish being processed.

