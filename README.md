<div align="center">
    <h1>pycord-i18n</h1>
    <h2>Internationalization for Pycord</h2>
</div>

## Key Features
- Translated responses
- Command name, description & option localization
- Based on user & server locale (no need for storage!)

## Installation
To install this extension, run the corresponding command:
```sh
# linux / macOS
python3 -m pip install pycord-i18n

# windows
python -m pip install pycord-i18n
```

## Usage
1. Setup your internationalization files just like [sample-german.json](https://github.com/Dorukyum/pycord-i18n/blob/main/sample-german.json).
Note that **all fields are optional** and **you can use whichever file format you want** as long as you pass the translations into I18n in the given format.

2. Load your files:
```py
import json

with open("sample-german.json", "r") as f:
    german_localization = json.load(f)
```

3. Create an I18n object:
```py
from pycord.i18n import I18n, _

i18n = I18n(bot, de=german_localization)
# "de" is the German locale
# string translations will be based on the guild's locale by default
# you can make the bot consider the user's locale by using the following:
i18n = I18n(bot, consider_user_locale=True, de=german_localization)

# all valid locales:
# id, da, de, en-GB, en-US, es-ES, es-419, fr, hr, it, lt, hu, nl, no, pl, pt-BR,
# ro, fi, sv-SE, vi, tr, cs, el, bg, ru, uk, hi, th, zh-CN, ja, zh-TW, ko
```

4. Internationalize your commands:
```py
@i18n.localize  # command name and description localization
@bot.slash_command()
async def hello(ctx):
    await ctx.respond(_("Hello, this sentence is in English"))
    # "_()" does the translation

# if you don't want to use `@localize` on every command,
# simply use the following method after adding the commands to the bot:
i18n.localize_commands()
```

## Changelog
### v1.2.1
- Fixed an issue with Pycord v2.5 compatibility

### v1.2.0
- Added formatting support

### v1.1.0
- Added option localization support
