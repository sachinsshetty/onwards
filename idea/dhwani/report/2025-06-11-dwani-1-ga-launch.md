dwani 1 - launch

Open Source Multimodal API for Indian Languages 


Run the dwani.ai stack on your machine with docker 

Use the API with python and nodejs library 

Setup- 
dwani.ai Server 
wget dwani.ai/compose.yml 
docker compose -f compose.yml  -p dwami-api up -d 

--
Setup API Key and URL for your dwani.ai  server 
pip install dwani 



npm install dwani

-- 

System Requirement 

Minimum GPU VRAM - 48 GB 

Tested on GH200 GPU at Lambda Labs

Compatible with H100 / L40s / A100

Require read access permission for
Google/Gemma-3  and AI4BHARAT/Indic-F5 
Huggingface model repository 


--

Open weight models 
1. Text + Vision : Gemma3-4b-instruct 
2. Text to Speech : Indic-F5 
3. Translation : IndicTrans2
4. Speech to Text : IndicConformer Multilingual/ Nemo

Library
1. rolmocr for documents API
2. fastapi/uvicorn for API server
3. pytorch/transformer for model serving
4. onnx for model serving
