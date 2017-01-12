This document provides instructions on how to set up your account to cast automatic flags via the SmokeDetector/metasmoke system.

## Prerequisites
Before running through the rest of these instructions, ensure that:

 - You have an account on metasmoke. You can get one of those [here](https://metasmoke.erwaysoftware.com/users/sign_up), if you don't have one.
 - Your metasmoke account has the "flagger" permission. You can check that [here](https://metasmoke.erwaysoftware.com/users): find your username, and look for the "flagger" role. Ask an admin about this if you don't have it.
 - Autoflagging and registrations are enabled. You can check these under [system settings](https://metasmoke.erwaysoftware.com/flagging/settings); verify that the `flagging_enabled` and `registration_enabled` settings have a value of `1`.

## Set Up Autoflagging
1. **Enable flags on your account.**  
   Visit [your preferences page](https://metasmoke.erwaysoftware.com/flagging/preferences), and read through the red-boxed disclaimer. If you're happy with that, tick the box to enable flags on your account.
2. **Set up preferences.**  
   On the same preferences page, click "Set up preferences" near the bottom of the page. The page you're taken to lets you set up your preferences, which govern how many of your flags the system can use on any particular site or group of sites. Fill in the maximum number you'd like to allocate, select the sites you want that number to apply to, and click Save. You can repeat this process to have different maxima for different groups of sites.
3. **Set up conditions.**  
   Visit the [flag conditions setup](https://metasmoke.erwaysoftware.com/flagging/conditions/new) page. This page lets you set up combinations of conditions governing how certain you want the system to be that a post is spam before using your account to flag it. The minimum weight controls the minimum cumulative weight of all the reasons a post was caught by (the maximum weight a reason can have is 100; we suggest 280 is a good value for this field). The maximum poster rep controls the most reputation a post author can have. The minimum reason count controls how many reasons you want a post to have been caught by - this performs a *similar* function to minimum weight. Fill in some values, and click Save. Again, you can repeat this process to have different accuracies for different groups of sites.

> **N.B.** There's a threshold of accuracy that all flagging conditions must meet before they're used to cast flags automatically. Currently, this is 99.9% - if you want to get the current value of this threshold, it's stored as the `min_accuracy` system setting.

At this point, you should be set up and your account will be used to cast spam flags according to the parameters you've specified. If you've found any bugs, or have feedback on the system, let us know. If you've found a security bug, please email it to someone rather than posting publicly.