# THAANKS
Obyte Autonomous Agent, THAANKS ask a user to trigger an AA for a reward, can optionnaly be overtaken by other users or bots

## Use cases
* To use it please provide: data.help = true and optional data.helper and data.time
* You can subscribe as good guy to be picked if the AA doesn't specify a helper;
* ther is no too late, because trigger are valuable, it is the previous AA that need to react to a late trigger...

## inputs
* help
* helper
* private
* time 
* delay

## State variables
* number_of_good_guys = <count>
* good_guys_<number> = <random helper address>
* <helper+aa hash>_reward = <value>;
* <helper+aa hash>_asset = <asset_id>;
* <helper+aa hash>_time = timestamp;
