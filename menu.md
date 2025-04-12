# 1. Main_Menu
1.When we press PLAY button, the Level_1 scene will be loaded 
1) Create a new scene:
   project panel--> right click --> creat--> scene --> named "Main_Menu"
2) Add this scene to the built panel:
   File--> Built settings--> then drag the Main_Menu on to the panel
   You should add all your scenes here, in this program, I create 6 scenes (6 levels)
   Drag Main_Menu on the top, which means the built index is 0.
3) Create a PLAY button:
   Hierarchy panel --> right click -->UI --> Button --> named "PLAY"
   【Unity can add the 'Canvas' and 'EventSystem' automatically】
5) Setting the PLAY button
   (1)click the canvas in Hierarchy panel --> turn to the Inspector panel --> Canvas Scaler --> UI Scale Mode  
   --> Scale With Screen Size
   (2)We can see 'Text' under the 'Play'. Click the 'Text' in Hierarchy panel, then turn to Inspector panel.In 
      the Inspector panel, we can change the text content, font, size, color, alignment, and many other visual 
      properties.
   Play
   ├── Text(TMP)
6) PLAY Button Scene Transition
   When we click PLAY button, the scene transition to Level_1.
   Add a new script named Main_Menu in Main Camera.
   click the Main Camera in Hierarchy panel --> turn to the Inspector panel --> click 'Add Compontent' --> 
   input 'Main_Menu' --> create the new script
   open this script.
   -- c# --
   
8) 
   
When we press Options button, the options panel will be opened
When we press Quit button, the game will shut down
# 2. Level_Menu
