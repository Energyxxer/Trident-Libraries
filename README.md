# Trident-Libraries
by Energyxxer

## Block API
This Trident library allows you to turn any Minecraft block into a falling_block entity or an armor stand wearing an item, preserving the exact block ID and blockstate as the source. This is done by assigning a numeric ID on the scoreboard to every different type of block, and each blockstate it may have, which is obtained by running `blockapi:block_to_score` at the location of the block to capture.
Those scores are then assigned to the pointers `${BlockAPI.outputIdScore}` and `${BlockAPI.outputDataScore}`.

Using the scores in the pointers `${BlockAPI.inputIdScore}` and `${BlockAPI.inputDataScore}`, that numeric block can then be turned back into a physical block (via `blockapi:score_to_block`), into a falling block (via `blockapi:score_to_falling_block`) or into an armor stand's head (via `blockapi:score_to_armor_stand_head`).

Some special cases can be made for specific blocks, by changing the values in the `${BlockAPI.blockInfo.blocks}` object. You may decide that `minecraft:water` should be represented as `minecraft:blue_wool` when on falling sand, or `minecraft:light_blue_stained_glass` when on an armor stand's head, or perhaps even ignore certain blocks entirely when converting to an armor stand's head. This should only be done after `@on compile` and `@priority 1000` and before non-compile `@priority 0`.
Note: the item chosen to be placed on an armor stand's head is automatically chosen to be the item that has the exact same ID as the block it came from, so some blocks don't have any item representation. By default, water is turned into blue wool and lava into orange wool.

This makes heavy use of the MinecraftTypes Trident Native library to retrieve all block types and their blockstates.
This generates a 4-split function tree for every conversion operation, around 250 block tags and about 3,000 function files.

Feel free to take a look at the code to see what it can do.
