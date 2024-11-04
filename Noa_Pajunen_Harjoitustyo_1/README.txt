======= LYTTA README =======


INSTRUCTIONS / HOW TO BUILD THE GAME YOURSELF:
Lytta uses version 2022.3.45f1 of the Unity editor.

1) Create a new 3D project.
2) Navigate to Assets -> Import Package -> Custom Package
3) Find the Lytta_Package_All.unitypackage file on your computer and import it.
!! THIS NEXT STEP IS IMPORTANT. !!
4) Because the scripts found within the Unity project use Index numbers to change between scenes, 
you will need to add the scenes to it's build index yourself. This is an easy task and I've provided 
further instructions below :
		5) Navigate to File -> Build Settings
		6) Add each scene into the build index in the following order:
		
			MainMenu : 0
			GamePlay : 1
			GameOver : 2
			
			To add a scene into the build index, double click on the scene to open it and then 
			press ''add open scenes'' within the build settings screen. Do this in the order shown above.
			
			If done correctly you should be ready to build the project,
			you might want to go back into editor view and play the MainMenu scene
			and click on ''Play'' to make sure it loads into the correct scene.
			
			To build the project you will want to navigate back to File -> Build Settings and choose ''Build''
			Pick a folder to store your build in, and wait.
			Once the build finishes you can click on ''Project3.exe'' to play the game.
			
			
			
GAME INSTRUCTIONS :

Press ''Play'' to start the first (and only) level.
Press ''Quit'' to exit.
Use space on your keyboard to jump.
Your goal as the player is to survive as many obstacles as possible.
Each obstacle you manage to jump over contributes to your score.
You have three lives within the level, hitting an obstacle loses one of those lives.
In the game over screen, you may press ''Retry'' to start the level again or ''Quit to desktop'' to exit.



TECHNICAL DOCUMENTATION :

1) PLAYER CONTROLS, POINTS AND HEALTH.
All player movement related functionality is handled within the PlayerController script.
The player has the ability to jump by pressing the space key. 
The grounded variable prevents the player from double jumping.
Awake() within PlayerController resets Physics.Gravity and gravitymodifier. This is to stop
the gravity from multiplying over and over upon restarting the level.

Health is also handled from within the PlayerController script. Each time the player gameobject collides
with an obstacle they lose a point of health. When value reaches 1 the next collision results in a game over.

Scoring is handled within ScoreManager. 
Each obstacle that gets destroyed ''out of bounds'' (behind the player) increments their score by one.
When the player collides with an obstacle and loses health, the obstacle should be destroyed immediately to stop 
the obstacle in question from incrementing the score as well.

2) OBSTACLES
BoxScript.cs handles moving the obstacles as well as destroying them out of bounds.
SpawnManager.cs handles spawning obstacles.

3) GRAPHICS, UI AND SOUND
MainMenu.cs handles both Main Menu and the Game Over screen.
HUD elements are handled within ScoreManager and PlayerController (Score and HP respectively.)

Sounds and particle effects related to the player (ie. jump sound) are handled within PlayerController.cs
In-game music playing during the level itself comes from the audio source linked to the camera object.
Menu music in both MainMenu and GameOver comes from the audio source linked to the Menu Music Source game objects found in both scenes.

The ''infinite scroll'' effect of the background is handled by two separate scripts (MoveBackground.cs and RepeatBackground.cs)

4) HYPOTHETICAL FUTURE ADDITIONS
My initial plan was to also add a ''cut scene'' to the beginning of the level, that provides some ''plot'' or context to the game's overall artistic direction.
Due to the issues I ran into during development, I had to leave it out. 