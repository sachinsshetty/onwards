Dhwani- v2 - Roadmap - March 22-27

1. Main issue -

Dark theme - old phone is broken 
Not usable to access settings

2. Api server - 
For routing and loadbalamcing update system
From python to go ? 

Make it serve with less resources and high throughput 

3. Canvas/ message bist
Message reaponse body should be  markdown reader. 

To present data in a nice format

4. Auto Voice language 
Sample 2 sec audio on each Language for Transcription 

Pass it via asr for the available Language and get  text in multiple Language 

Use Indic lid for text to match exact language. 

Currently ASR is not streaming,  
We want to add streaming voice input first and experiment with language identification. 

5. Live transcription- earphone to App ? 
Stream AsR / feed to b to translate 

Show real time audioc in n text

6. University Collab / access

Register with Uni email .

Get access token and build so. 

Provide info / about app Chankya uni in app. 

Add a separate tab / rag based /

7. App Features/ characters

Add - status icon in settings page 

Show availability of service 

Choose- better models 

Add - option for character's / stoeries 

Ramayana/ mahabharsya 
Non-copyrighted books only 

8. API Server - user management 
Csv uploader  - server - restart 

Db backups? 

Name , type 
Type - mobile 
Type- web 

Username - full-email id

Password: username part before  @ 

Allowed- domains 

gmail.com
chanakyauniversity.edu.in 


Add - gpu check ? Torch compile 
Use bfloat16 for l4 and above 

9. Parler-tts- distillation 
Make smaller generator/ 
Distill the project for individual language 

Improve speed and accuracy? 
Can we do it ?

10. Dhwani Marketing-integration 
Create integration with 3rd Party clirnts

Live kit 
Fast rtx
Plivo 
Twilio
Whatsapp Api

11. Dhwani - web ux - user management 

Create a simple screen on dhwani - website 

Login with admin details.

Get list of useers updatws to systen. 

Add new users with simple button.


12. Dhwani - model - server 
Fix - issue with asyn calls. 

Make load testing of projrct .


Add load balancing to main api 


Based on compute available,  auto scale the systen
Non GPU 
T4 - 
L4 

Select betwen 
Gemma3-4b-instruct 
Gemma3-4b-instruct quantized

Gemma3-1b-instruct 
Gemma3-1b-instruct quantized

Translation models 

Voice model / 

Always lazy load 


13, Transcription 

Translate in real time without llm in betwen.

Suitable for handsfree on mobile app
 
Make it work for german,  Kannada language first. 

More users require it immediate. 

Set source and target language.


Choose - main screen in setting.


14. 






