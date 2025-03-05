# BuckshotRouletteShellView
A Tutorial To Create a Simple Shell View Hack for the Game Buckshot Roulette

## Tutorial
1. Decompile the game using **Godot RE Tools**.
2. Open the decompiled game with **Godot Editor 4.1.1**.
3. Install **godotsteam** (Godot 4.1.1 - Steamworks 1.58 - GodotSteam GDExtension 4.4.1) into the project; otherwise, it won't work properly.
4. Locate the function `GenerateRandomSequence` in `res://multiplayer/scripts/global_scripts/MP_RoundManager.gd`.
5. Observe that the function is called every time the shotgun is loaded on the host side. Check out the code at the end of the function:
   ```gd
   var dict = {
       "sequence": sequence,
       "sequence_visible": sequence_visible_shuffled,
       "sequence_in_shotgun": sequence_in_shotgun,
       "shuffling_visible_sequence": shuffling_sequence,
   }
   var dict_send = dict.duplicate(true)
   dict_send.erase("sequence_in_shotgun")
   game_state.MAIN_active_sequence_dict = dict
   game_state.MAIN_active_sequence_dict_send = dict_send
It creates a dictionary that will be then sent to other players.
According to an erase call, this info is hidden from clients (Guess to prevent cheating).
And that means it should be exactly what you need.
6. Add those lines after those:
```
print("!!!HACK INFO: Shells in shotgun")
print(dict["sequence_in_shotgun"])
```
7. Build it.
8. You did it, yay! Now you can see shotgun ammo through console (Launch game binary through command line) when you play as host.
