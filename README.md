# BossMan

You are weak and indecisive.

Let the BossMan decide.

# What is BossMan?

BossMan is a simple library made for SC2 AI bot development that will help select from a list of choices for you.

BossMan tracks choice history and prioritizes choices that experience high win rates. It also prioritizes choices it hasn't used much yet.

BossMan is currently used in the SC2 bot [Chance](https://github.com/lladdy/chance-sc2), which plays on
the [SC2 AI Arena Ladder](https://aiarena.net/bots/117/)  
Here it is used for selecting strategies at the start of the match.

# Example Usage:

Simplest usage:

```python
available_builds = ['FourRax', '2BaseTankPush', 'BansheeHarass']

boss_man = BossMan(file='optional/path/to/file.json')  # default file path is ./data/bossman.json

# Here 'strategy' is the decision type.
# Decision types keep different decisions seperate, so they don't interfere with each other.
selected_build = boss_man.decide('strategy', available_builds)

...  # later, after the match is done

boss_man.report_result(True)  # automaticaly saved to file here
```

### Multiple scopes

Each scope's history is tracked separately.

```python
opponent_id = '12345'
available_builds = ['FourRax', '2BaseTankPush', 'BansheeHarass']

boss_man = BossMan()

# Now take the opponent id into consideration
selected_build = boss_man.decide('strategy', available_builds, opponent_id=opponent_id)
```

# Extra Options

### Control automatic file saving

Usually when you report a result, all data is automatically saved to file.  
To avoid this, you can either pass `autosave` as `False` when you create BossMan, or provide the `save_to_file`
parameter when reporting the result.

```python
boss_man = BossMan(autosave=False)  # Disable autosave permanently

# Alternatively, both these will override the autosave setting
boss_man.report_result(True, save_to_file=False)
boss_man.report_result(True, save_to_file=True)
```
