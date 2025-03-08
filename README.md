Breakout Assembly Game
This project is an implementation of the classic Breakout game written in assembly language for the CSC258H1F Winter 2023 final project.

Overview
This assembly program directly manipulates a bitmap display and processes keyboard input to implement the Breakout game. It initializes the display, draws the start screen, and then transitions into the game loop where the ball and paddle move, collisions are detected, and bricks are removed.

Display & Data Configuration
Display Configuration:

Unit width: 8 pixels
Unit height: 8 pixels
Display width: 256 pixels
Display height: 512 pixels
Base address for display: 0x10008000 (also referenced as ADDR_DSPL)
Immutable Data:

Bitmaps:
Two pages of bitmap data (Start_page and End_page) are defined to draw the start screen and game-over screen.
Colours:
A list of predefined colours (light pink, red, blue, green, yellow, etc.) is stored for drawing walls, bricks, the paddle, and the ball.
Mutable Data:

Paddle Location:
The current address of the paddle on the display.
Ball Location & Velocity:
The ball’s position and its x/y velocity, which are updated as the game runs.
Main Sections of the Code
1. Start Screen Initialization
Drawing the Start Page:
The code copies colour values from the Start_page data into the display memory. A loop iterates through all 4096 display units.

Waiting for the Enter Key:
After drawing the start screen, the program polls the keyboard until the Enter key (ASCII 0x0A) is pressed.

2. Screen Clearing and Game Map Drawing
Clearing the Screen:
All display units are set to black (color 0x000000), effectively clearing the previous screen.

Drawing Game Map Elements:

Walls and Boundaries:
Drawn using loops to create horizontal and vertical lines in light pink.
Bricks:
Multiple loops draw rows of bricks in different colours (red, green, blue, and yellow) at specific offsets.
Paddle and Ball:
The paddle is drawn at its initial location using a specific colour, and the ball is drawn at a separate starting offset.
3. The Game Loop
Inside the infinite game loop, the program performs the following tasks:

Input Handling:
The keyboard is polled to determine if a key is pressed. Based on the key:

'A' moves the paddle left.
'D' moves the paddle right.
Enter may restart or end the game. The Move_paddle routine updates the paddle’s location while ensuring it does not exceed the defined bounds.
Collision Detection:
The ball's surroundings (top, bottom, left, and right) are checked for collisions:

If a wall (or paddle) is detected, the corresponding velocity (x or y) is inverted.
If a brick is hit, the brick’s location is calculated and the Delete_brick routine is invoked to "remove" it by painting black.
Ball Movement:
The ball's position is updated by adding its velocity to the current location. The previous ball location is cleared, and the ball is redrawn at the new location.

Delay and Looping:
A delay (using a syscall) is added to control the game speed before the loop repeats.

4. Additional Routines
Move_paddle:
Updates the paddle's position based on the keyboard input. It checks boundaries and uses different code paths for moving left or right.

Move_ball:
Calculates the ball’s new position based on its current velocity and updates the display accordingly.

Get_brick_loc & Delete_brick:
These routines determine the coordinate of a brick that is hit by the ball and then "delete" the brick by painting over it with the black colour.

Game Over:
When the ball reaches a specific location (indicating it has missed the paddle and hit the bottom), the game-over routine is executed. The end screen is drawn using End_page, and the program waits for a key press before quitting.

How to Run
Assembly & Linking:
Assemble and link the code using your preferred MIPS assembler.

Hardware Setup:
Ensure that the bitmap display and keyboard devices are correctly connected and mapped to the addresses defined in the code.

Execution:
Run the assembled program. The start screen will be drawn first. Press Enter to clear the screen and begin the game. Use the 'A' and 'D' keys to move the paddle and interact with the game.

Author(s)
Student 1: Ji Sung Han (1006581815)
Student 2: :(
