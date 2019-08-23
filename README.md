# THAANKS
Obyte Autonomous Agent, THAANKS ask a user to trigger an AA for reward, can be also overtaken by a bot

[
   "autonomous agent",{
      bounce_fees: { base: 10000 },
      init: "{
         // THAANKS, ask a user to trigger an AA for reward, can be also overtaken by a bot
         // to use it please provide: data.data.help = true and optional data.helper and data.seconds
         $OWNER = "O7NYCFUL5XIJTYE3O4MKGMGMTN6ATQAJ"; // to adjust parameters
         
         
         if (trigger.data.help) // trigger coming from an aa
         {
            $good_guy = var["good_guys_"||number_from_seed(timestamp,1,$number_of_good_guys)];
            $helper = trigger.data.helper otherwise $good_guy;
            $aa = trigger.address;
            $reward = trigger.output[[asset!=base]].amount otherwise trigger.output[[asset=base]].amount otherwise 0;
            $reward_asset = trigger.output[[asset!=base]].asset otherwise "base";
            $delay = trigger.data.seconds otherwise 0;
         }
         else
         {
            $helper = trigger.address;
            $aa = trigger.data.aa otherwise var[$helper] otherwise bounce ("Don't know which aa to help!");
            $reward = var[$aa||"_reward"];
            $reward_asset = var[$aa||"_asset"];
            $delay = var[$aa||"_delay"];
         }
         
         // test if a bot overtook the user?
   }",
      messages: {
         cases: [
            { // looking for an helper to trigger an aa in the futur
               if: "{ trigger.data.helper}",
               init: "{
               }",
               messages: [
                  {
                     app: "data",
                     payload: {
                        "message": "{"Get "||$reward||" "||$reward_asset||" if you are first to reply me in "||$delay||" seconds" }",
                        "helped_aa ": "{$aa}"
                     }
                  },
                  {
                     app: "payment",
                     payload: {
                        asset: "base",
                        outputs: [
                           {
                              address: "{$helper}",
                              amount: "{1000}"
                           }
                        ]
                     }
                  },
                  {
                     app: "state",
                     state: "{ 
                     var[$helper] = $aa;
                     var[$aa||"_reward"] = $reward;
                     var[$aa||"_asset"] = $reward_asset;
                     var[$aa||"_delay"] = $delay;
                     var[$aa||"_request_time"] = timestamp;
                  }"
                  }
               ]
            },
            { // Subscribe as an enthousiast helper;
               if: "{ trigger.data.subscribe}",
               init: "{ 
                  if (var[trigger.address]) bounce ("You are motivated, but once is enough!");
               }",
               messages: [
                  {
                     app: "state",
                     state: "{ 
                        var[trigger.address] = true;
                        var[$number_of_good_guys] +=1;
                        var["good_guys_"||$number_of_good_guys] = trigger.address;
                        response['message'] = "Subscribed"; 
                     }"
                  }
               ]
            },
            { // default too late=> bounce
               init: "{
               if (!var[$aa||"_reward"]) bounce ("Too late someone have triggered the aa already!");

            }",
               messages: [
                  {
                     app: "payment",
                     payload: {
                        asset: "{$reward_asset}",
                        outputs: [
                           {
                              address: "{$helper}",
                              amount: "{$reward}"
                           }
                        ]
                     }
                  },
                  {
                     app: "payment",
                     payload: {
                        asset: "base",
                        outputs: [
                           {
                              address: "{$aa}",
                              amount: "{1000}"
                           }
                        ]
                     }
                  },
                  {
                     app: "state",
                     state: "{ 
                     var[$helper] = false;
                     var[$aa||"_reward"] = false;
                     var[$aa||"_asset"] = false;
                     var[$aa||"_delay"] = false;
                  }"
                  }
               ]
            }
         ]
      }
   }
]