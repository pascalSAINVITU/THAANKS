# THAANKS
Can be use to ask a user to trigger (optionnaly at a given time and with a given accaptable delay) an AA for a reward, can optionnaly be overtaken by other users or bots

## Use cases
* To use it please provide: data.help = true and optional data.helper and data.time data.delay data.private
* You can subscribe  and unscubscribe as good guy to be picked if the AA doesn't specify a helper;

## inputs
* help 
* helper: specify a helper address
* private: to forbid other user to overtake the 'helper'
* time: to specify a time before which it is not valid to trigger
* delay: to defined acceptable delay after the 'time'

## State variables
* number_of_good_guys = <count>
* good_guys_<number> = <random helper address>
* <helper+aa hash>_reward = <value>;
* <helper+aa hash>_asset = <asset_id>;
* <helper+aa hash>_time = timestamp;
