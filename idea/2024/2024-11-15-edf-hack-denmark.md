EDF - Denmark Hackathon

- Challenges
    - RF to LLM (speech to text)
        - Build a simple prototype system that transmits audio over RF to an offline LLM that transcribes and makes sense of the audio to extract insights. 

    - Keep Talking and Nobody Explodes
        - Develop a system for mapping manuals, textbooks, and other data to a simulator of the machine. Use this system to defuse a bomb from its defusal manual, and win Keep Talking and Nobody Explodes within as few Turns as possible.
        - Using Multimodal LLMs and code generation, you can turn each page of the bomb manual (https://www.bombmanual.com/) into an executable simulator. (We provide openai keys). Alternatively, you can write this part by hand. Then, another two AI agents will take the role of the players, interacting with the bomb simulator. The goal is for the simulator to be precise, and for the players to defuse it in as few rounds as possible.
        - https://www.bombmanual.com/print/KeepTalkingAndNobodyExplodes-BombDefusalManual-v1.pdf
        - https://www.bombmanual.com/


- Solutions
    - RF to LLM
        - Listenser - RaspberryPi + Microphone
        - Server - Laptop with GPU : Whisper + Mistral
        - Questions
            - How to transmit audio via RF signals, what are components required
            - How to receive RF signals and convert to audio
        - Steps
            - Store audio into topic/queues with source information if possible
            - Run Voice Activity Detection(VAD) on RasPi to for passive listening and power saving.
            - Send 15/30 sec clips over RF
            - Receive RF signals and convert signals in audio format
            - Event based server triggers - Whisper server and converts Audio to text
            - Attach source info/timestamp to event with Converted text
            - Merge Text + Audio for offline cleanup and analysis
            - Stitch text - if continous voice with timestamp and multiple voices
            - Parse Text with LLM - System level with additional context and matching info over period of time from same sensor.
            - Use Location + Time + Text + Voice ID with RAG to build reports.
        - Systems
            - Listener - VAD + Microphone
            - Transcriber - Whisper on GPU Laptop
            - Analytics - System Prompts with LLM - mistral/llama3.2
            - Offline Reports - RAG + PDF
         
    - Keep talking and nobody explodes
        - Use AutoGen for multi-agent / turn based agents
        - Use PDF parser to separated Text + Image data
        - Process Images via Vision LM, Text via LLM into RAG system
        - Agents take info from RAG system to solve problems
        - Single Shot - Use a large context model like O1 and skip the RAG process 