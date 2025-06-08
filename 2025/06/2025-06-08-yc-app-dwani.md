YC App - dwani.ai 


- Video Edit

```bash
00:00:00 00:00:10
00:00:14 00:00:24 
00:00:29 00:00:35
00:00:40 00:00:50
```
```bash
#!/bin/bash
input="input.mp4"   # Change to your input file name
n=1

while read start end; do
  out=$(printf "segment-%02d.mp4" $n)
  ffmpeg -y -ss "$start" -to "$end" -i "$input" -c copy "$out"
  n=$((n+1))
done < timestamps.txt
```

```bash
ls segment-*.mp4 | sort | awk '{print "file \x27"$0"\x27"}' > segments.txt
```

```bash
ffmpeg -f concat -safe 0 -i segments.txt -c copy output.mp4
```


```bash
ffmpeg -i input.mp4 -c:v libx264 -pix_fmt yuv420p output.mp4
```

---

- Who writes code, or does other technical work on your product? Was any of it done by a non-founder? Please explain.

- I design the initial use-case and use Grok to write the code for small complete functions.


- Are you looking for a cofounder?
- No

Please record a one minute video introducing the founder(s).
- 


Company name*
dwani.ai

Describe what your company does in 50 characters or less.*
IDE with Indian language voice

Company URL, if any
https://dwani.ai

Please provide a link to the product, if any.
https://dwani.ai

What is your company going to make? Please describe your product and what it does or will do.

IDE with voice for Indian languages

Make applications using voice input for Indian languages. 

Unlock 700M users to solve problems with personalised apps

Where do you live now, and where would the company be based after YC?
Bonn,germany / Berlin,Germany

Explain your decision regarding location.
built the initial inference at Bonn.
Berlin will help to expand with beta users for applications

How far along are you?
Built the inference stack for Indian languages via dwani.api 
Have to build from scratch for Voice IDE


How long have each of you been working on this? How much of that has been full-time? Please explain.
python for backend/POC
gradio for workshops/demo
android for dwani inference API POC
models - Gemma3-27B-IT, Qwen3-32B, moondream, IndicTrans2, parler-tts, Indic-F5, IndicConformer

Use Grok as Code Generator with VsCode 

Are people using your product?
Yes

How many active users or customers do you have? How many are paying? Who is paying you the most, and how much do they pay you?
Android POC has 250 installs, API was used by 400 hackathon participants.
No paying customers yet.  
MVP is complete, need GPU to scale for more users

Do you have revenue?
No

If you are applying with the same idea as a previous batch, did anything change? If you applied with a different idea, why did you pivot and what did you learn from the last idea?

been applying with ideas before.
Pivoted to voice based IDE since many user's want to solve problems but dont know how to code and prompt.
Especially Indian language audience has a lot of untapped potential

If you have already participated or committed to participate in an incubator, "accelerator" or "pre-accelerator" program, please tell us about it.

No

Why did you pick this idea to work on? Do you have domain expertise in this area? How do you know people need what you're making?

built the dwani.ai inference API using open-weight models to solve https://sanjeevini.me. 

Tested the MVP with 400 hackathon participants, they want to use the API and solve the problems.
Most of them are beginners with code, but have a lot of ideas to implement.
Our voice based IDE will help to experiment faster 

Who are your competitors? What do you understand about your business that they don't?
cursor, replit, windsurf

their target is programmers and english speaking users who have tech knowledge.

We are opening a new market for Indian language software

How do or will you make money? How much could you make?

We will charge users for hosting/security/maintenance of their Apps.

App creation will be free and unlimited and free to use locally.

Which category best applies to your company?
DEveloper Tools

If you had any other ideas you considered applying with, please list them. One may be something we've been waiting for. Often when we fund people it's to do something they list here and not in the main application.
---

Have you formed ANY legal entity yet?
No

If you have not formed the company yet, describe the planned equity ownership breakdown among the founders, employees and any other proposed stockholders. If there are multiple founders, be sure to give the proposed equity ownership of each founder and founder title (e.g. CEO). (This question is as much for you as us.)
100

Have you taken any investment yet?
No

Are you currently fundraising?
no

What convinced you to apply to Y Combinator? Did someone encourage you to apply? Have you been to any YC events?

How did you hear about Y Combinator?


If you had any other ideas you considered applying with, please list them. One may be something we've been waiting for. Often when we fund people it's to do something they list here and not in the main application.
---

If you have not formed the company yet, describe the planned equity ownership breakdown among the founders, employees and any other proposed stockholders. If there are multiple founders, be sure to give the proposed equity ownership of each founder and founder title (e.g. CEO). (This question is as much for you as us.)
--

What convinced you to apply to Y Combinator? Did someone encourage you to apply? Have you been to any YC events?

--

How did you hear about Y Combinator?
--


Founder profile

Please tell us about a time you most successfully hacked some (non-computer) system to your advantage.
---

Please tell us in one or two sentences about the most impressive thing other than this startup that you have built or achieved.

---

Tell us about things you've built before. For example apps you’ve built, websites, open source contributions. Include URLs if possible.
---

List any competitions/awards you have won, or papers you’ve published.

--
