AWS - Activate Program - MVP migration


Current setup
1. Api server + Database 
- TLS - certificate required for https endpoints
- fastapi server with Python 
- load balancing - route management to inference server 
- user authentication and rate limiters for request 
- logging and metrics 
- Database- sqlite 

2. UX
- Github pages deployment with DNS
- Typescript + React 

3. Inference server 
- fastapi + pytorch 
- 24 GB VRAM minimum GPU for Workshop server
- 70 GB VRAM current system for production 

next changes

- Current Setup

- API Server + User Database 
    - 

For dwani.ai - the next steps would be to migrate,
basic API management servers running on Huggingface Spaces,
Located at hf.co/slabstech to EC2 instances.

