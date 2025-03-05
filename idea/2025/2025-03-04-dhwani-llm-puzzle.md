Dhwani LLM puzzle 


Just made qwen2.5 1B instruct respond to Query in Kannada. By adding a translator function. 
All this is running on 3 cent/hour machine.

It needs further evaluation,  looks promising though.

No gpu required,  qwen doesn't understand Kannada, but the indictrans2 model translates to English quite well.  
Qwen now responds in English and we translate it back.


Now the full stack is 100% independent without need for 3rd Party services. 
everything can be hosted with current hardware,  we just need to utilise properly.


continue speed run, explore all options.

-- system confugsv

50 cent stack. 


2 workers of tts on t4.
3 cent - asr 
3 cent - translate 
3 cent -llm


Full asynchronous system, supporting all uses cases with degradation of quality. 

Needs a good load balancer.