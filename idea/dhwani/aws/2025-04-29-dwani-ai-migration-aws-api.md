dwani.ai - migration to AWS


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

4. Swagger UI
- hf.space/slabstech 

Next changes - May 4 : Android release 

1. API server  - Backend- fastapi 
2. Db server - Backend- postgreSQL 
3. UX - dwani.ai  - landing page - Typescript/React
4. UX - api.dwani.ai - swagger ux / mintlify
5. Inference server - backend  - fastapi + pytorch


