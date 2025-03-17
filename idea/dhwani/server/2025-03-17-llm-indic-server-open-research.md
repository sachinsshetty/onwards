Indic LLM - Open Research 



If user requests recent data or unknown data, then model generates wrong answer/hallucinates.

Because -
- Model are trained on data,  which have a 1 year/6 month old data.
- Recent and current information is not available due to the static nature of model weights. 


To get recent data 
- collect delta data from cut-off and fine tune the model
- build RAG system to access recent data stored in vector store/ database 

Ex - make company docs and api available via  - text / natural language search 


To get real time data-
- access external api with tool/function call
- build bot scraper to index recent data for websites/ which do not have Api exposed 

