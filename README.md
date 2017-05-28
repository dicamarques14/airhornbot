# Airhorn Bot
Airhorn is an example implementation of the [Discord API](https://discordapp.com/developers/docs/intro). Airhorn bot utilizes the [discordgo](https://github.com/bwmarrin/discordgo) library, a free and open source library. Airhorn Bot requires Go 1.4 or higher.

## Usage
Airhorn Bot has two components, a bot client that handles the playing of loyal airhorns, and a web server that implements OAuth2 and stats. Once added to your server, airhorn bot can be summoned by running `!airhorn`.


### Running the Bot

**First install the bot:**
```
go get github.com/hammerandchisel/airhornbot/cmd/bot
go install github.com/hammerandchisel/airhornbot/cmd/bot
```
 **Then run the following command:**

```
bot -r "localhost:6379" -t "MY_BOT_ACCOUNT_TOKEN" -o OWNER_ID
```

### Running the Web Server
First install the webserver: `go install github.com/hammerandchisel/airhornbot`, then run `make static`, finally run:

```
./airhornweb -r "localhost:6379" -i MY_APPLICATION_ID -s 'MY_APPLICATION_SECRET"
```

Note, the webserver requires a redis instance to track statistics

### Add your own sounds
Download [DCA-RS](https://github.com/nstafie/dca-rs/releases) (don't use v0.1 as v0.2 never worked for me. I also didnt get it to work in windows)
` ./dca-rs --raw -i newsound.mp3 > out.dca ` 
Then, if you wish to have a command only for that sound make a new collection:
```
var NEWCOLLECTION *SoundCollection = &SoundCollection{
	Prefix: "before",
	Commands: []string{
		"!wowthatscool",
		"!wtc",
	},
	Sounds: []*Sound{
		createSound("after", 50, 250),
	},
}
```
And name your file with the format `before_after.dca` , notice the prefix and the createSound name are joint with a `_`

Finnally add your new collection to the collection list:
```
var COLLECTIONS []*SoundCollection = []*SoundCollection{
  NEWCOLLECTION,
  ...
  }
```
And recompile with go install :D
Make sure you give different collection names!

## Thanks
Thanks to the awesome (one might describe them as smart... loyal... appreciative...) [iopred](https://github.com/iopred) and [bwmarrin](https://github.com/bwmarrin/discordgo) for helping code review the initial release.
