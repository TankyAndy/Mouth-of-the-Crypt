# Mouth of the Crypt

DEMONSTRATION: https://youtu.be/7MplxFT1tBQ

This game challenges the player to collect all treasure items scattered throughout a dark room while avoiding a lurking monster.  
The player is placed in a dark environment where only nearby surroundings are visible, simulating a lighting effect.  
Using the PS/2 keyboard, the player navigates the room and locates treasure objects.  

To collect them, the player must speak into a connected microphone at a specific volume.  
The VGA display renders all game elements, including the player, monster, treasures, and environment.  

However, noise comes with risk:  
- If the monster is nearby when the player makes sound, the player loses.  
- If the player does not collect all of the treasures within the time limit, the player also loses.  

**Goal**: Collect all treasures within the given time limit without being caught by the monster.

---

## 1. Instructions and Key Features

### Start the Game
- The game starts on the title screen. Press the **Spacebar** to begin.

### Gameplay Controls
- **W** – Move Up  
- **A** – Move Left  
- **S** – Move Down  
- **D** – Move Right  
- Loudly speak into the microphone when near a coin to collect it.  
  - The noise bar on the right will turn red when the noise threshold is reached.

### Restart the Game
- Press the Spacebar again after a game over to restart.

### Goal of the Game
- Collect all coins hidden throughout the map.
- Use sound (via the microphone) to collect coins when standing close to them.

### Avoid the Monster
- A monster moves randomly on the screen.
- If you make too much noise while the monster is near, the game ends immediately.

### Limited Vision Mechanic
- Your character can only see in a small circle around them, simulating a flashlight beam in the dark.

### Noise Bar
- A bar on the bottom of the screen displays how loud your sound input is.
- If the noise level is too high, the bar turns red.

### Time Limit
- You have **200 seconds** to collect all the coins.
- When time runs out, the game ends.

### Winning and Losing
- Win: Collect all 15 coins within the time limit and avoid the monster.
- Lose: If the monster catches you (due to loud noise nearby) or if time runs out.

### Scoring
- Your score is based on how many coins you collect.
- The final score is displayed on the game over screen.

---

![Final Block Diagram](blockdiagram.pdf)
*Figure 1. Final Block Diagram*

---

## 2. Hardware Used
- Keyboard  
- Microphone  
- On-board Hardware Timer  
- VGA Display  

---

## 3. Main Components of Project

### Game States
- **gameStateTitleScreen**  
  Displays the title screen. Pressing space enters `gameStateRun`.  

- **gameStateRun**  
  Core gameplay loop.  

- **gameStateOver**  
  Displays "you win/you lose" message and score. Pressing space enters `gameStateRestart`.  

- **gameStateRestart**  
  Resets variables, timers, and keyboard input, then re-enters `gameStateRun`.  

### Data Structures
- **Entities**: Items, Monster, User  
- Each has attributes: coordinates, status, velocity  

### Item Array and Random Position Generation Logic
- Array of items with random placement.
- Random x/y coordinates generated in ranges (0–240, 0–320).

### Monster Random Movement Logic
- Random direction & distance generated.
- Monster re-rolls direction if the previous distance is finished or monster hits map border.

### User Movement Logic
- Controlled by **WASD** inputs using polling method.

### Microphone
- Sound input values read from FIFOs.

### Collecting Items Logic
- Item is collected if:
  - Player is next to the item **and**
  - Noise level exceeds threshold.

### Proximity Detection Logic
- If noise is above threshold **and** monster is nearby → Game Over.

### Hardware Timer
- Player has 200 s



