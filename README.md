# THAANKS
## secondary AA that can be ask for help 
Can be use to ask a user to trigger (optionnaly at a given time and with a given acceptable delay) an AA for a reward, can optionnaly be overtaken by other users or bots (if not in private mode)

## Use cases
* To use it please provide: 'data.ask_help = true' and optional 'data.helper = <address>' and 'data.requested_time = <timestamp>' 'data.acceptable_delay = <delay in second> and  'data.private = true'.
* You can 'data.subscribe' and 'data.unsubscribe' as good guy to be picked if the AA doesn't specify a helper;
* If trigger is late, the reward goes back to the aa;
  
## example of use
* you want to trigger a draw in the futur with data feed  that should not be predicted
* you want to make a recurrent payment
* ...

## inputs
* ask_help: set to true to create entry 
* helper: specify a helper address
* private: to forbid other user to overtake the 'helper'
* requested_time: to specify a time before which it is not valid to trigger
* acceptable_delay: to defined acceptable delay after the 'requested_time'
