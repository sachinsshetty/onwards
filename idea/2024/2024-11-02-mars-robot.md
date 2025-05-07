Mars Bot




Build the voice activated Robot for mars

Vision - video processing 

Text - world understanding 

Speech - active word detection and speech recognition 

Robot - hand manipulation 


--
Fuse all modalities into Autonomous robot

1. Speech question request 
- hey Sachin,  what do you see in your front of you ?

a. Speech should be converted to text : microphone active listening for wake word detection and speech recognition

b. Front camera should be called to take a picture/video stream : trigger with function calling 

c. Image understanding - should describe the image in 2/3 lines summary : system prompt added for context .

d. Image to text + voice to text : merge text from image and voice text for context understanding for final response in text 

e. Voice response: text to be converted to voice via tts module and sent to speaker.


Log should capture all the data flow changes.
Streaming - screen should show progress after each stage to everyone for debug and verification. 



Speech Question Request 
- hey Sachin can you move the apples in to the basket .

Steps: a + b + c + d 

i. Robot body analysis- if arm is present,  send command to arm to move object in required direction. 
ii. Real time object + hand tracking system coordinate/verifies path determined for Arm to move.

Version 2 - show arm manipulation with simulation until Robot arm is constructed. 

