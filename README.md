# Bomberman World — [Combo Bomber]

**Student:** [Junyi Zhu]

## How to play

- **Controls:** 
    · Key W,A,S,D/ Arrow keys: Player movement
    · Key Space: Place a bomb
    · Key R: Restart the game after the game ends.
    · Key Q/ Escape: Quit the game.

- **Objective and rules:** 
    · How to win: Achieve the target score of 5000 points by destroying the boxes and the enemies. An enemy killed scores 50, a box destroyed scores 10.
    · Lose condition: Once collides with the enemy or affected by the blast of the explosion, the player will die immediately and lose the game.
    · If the player dies when the score is achieved, the game loses.
    · Power-up props: A green power-up prop will be generated on the map randomly. Once the player get the prop, the blast range will be increased by 1 and the buff will last for 6 seconds. The explosion range bonus effect can stack up to a maximum of 6.
    · Combo rules: Destroying targets continuesly within 3 second will increase the score multiplier (x2, x3...).
    · Enemy spawner: Enemies will be generated on the empty grid of the map randomly. The first one will be generated 5 seconds after the game starts, and then the enemies will be generated every 3 seconds thereafter.
    
- **Configurations / demo setup:**  Default.


## Features and validation

| Feature | Check, observed result, and expected behaviour |
| --- | --- |
| 1. Player damage and death |  I controlled the player directly walk into an enemy and also walk to the grid which is with the blast range to test if the player entity will disappear in this two condition. The player entity disappeared immediately once collides with the enemy or affected by the explosion. This result matches with the wish that the blast and enemy contacts cause fatal damage.  |
| 2. Round states and objective | I lowered the final score needed to win the game and controlled the player to die to test if the window shows the correct state if I win or lose the game. The text I drew for the win/ lose condition correctly shown on the middle of the window and the gameplay paused. The result matches with the expected game state display. |
| 3. Safe restart | I died intentionally and pressed Key R to restart. The map reset, the score and timers returned to 0. I tested if the old bombs will still explode after I done the multiple bombs and the bomb did not explode and will disappear. This matches the expected behaviour that old round states are completely and safely cleared. |
| 4. Solid bombs with owner escape | I placed a bomb, walked out of its tile, and tried to walk back into it. The player was blocked by the bomb and could not overlap as expected. |
| 5. Blast-range pickup | Firstly I picked up the spawned green power-up prop which is generated on the fixed grid every game and the blast range was increased. Lately I added the function that the power-up would generated every 10 seconds and the buff would only last 5 seconds. The buff effect is expected can be stacked up to 6. Then I start the game to see if the power-up can be successfully generated randomly and I didn't find any generated random props at first try. Then I go back to the code and found out I had mistakenly wrote the powerup timer inside the enemy spawner timer's {} scope block. After fixing this issue I the observed the powerups spawning correctly on random floor tiles every 10 seconds, the blast range increased up to 6 as expected. |
| 6. Multiple bombs per owner | I rapidly pressed the Spacebar 4 times while moving. Only 3 bombs were placed, and the 4th attempt was ignored until the first bomb exploded which match with the maximum bomb capacity I set. |
| 11. Scoring and combos | I destroyed few crates consecutively within a 3-second time window to test the combo multiplier logic. The first crate awarded the base 10 points and the second crate awarded 20 points, with an orange "COMBO x2 !" text appearing on the top right of the window. After 3 seconds of no any destructions, the combo multiplier reset. The result matches with the expected scoring multiplier logic and the 3-second combo window timer. |
| 15. Enemy spawners | I adjusted the map to a smaller size and I stand still in a corner at the beginning of the game. The first new enemy spawned exactly after 5 seconds as I count manully and the rest enemies were generated every 3 second as wish.  |

**Known issues:** None known after testing.
## Sources and assistance

This project builds on the shared Kotte foundations.

During the development, I rechecked the concept of Spatial Partitioning and broad-phase collision detection to fully understand how the engine optimizes entity queries, ensuing I correctly integrated the dynamically spawned enemies and props into the spatial grid. Additionally, I used an AI assistant to help fix bugs I met such as identifying a scope nesting issue with the power-up timer. Also AI suggested using a for loop with a 20-iteration safety limit instead of a while loop for my random tile search when generating the enemies, preventing potential infinite loops when the map becomes crowded. All AI-suggested fixes were manually reviewed, understood, and tested by me before being integrated into the code. No other external resources were used.

