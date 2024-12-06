Report - 0.0.1 - December 6, 2024

--

App Deployment


Tutorial for project deployment 

Youtube video  - setup AI prototype with Zero deployment costs Experimental resources 


Setting up Ux with github pages

Setup server with django spaces 


Inference api with Mistral 

  
-- 

Create simple bashrc fire Inference 
With dummy values for convenience. 


Part 1 - show existing application 

Part 3- show with buildings from scratch

---

Local weights-  reason

Build simple evals for domain specific industries

Run status check with AI models to verify if model response is modified over time.


Self-host models with fixed model weights 
To control level of data. 

Lllama/mistral model weights with self hosting


--

App Diabetes

Diabetes App 


- Solve issue with UI reload on Github pages with navbar 

- Add patient and doctor name to screen 

- Add diabetes chart to User screen 

- Load appa  diabetes chart from screen shot. 

- Take new screenshot of diabetes chart 

- Scan full Diabetes chart 

- Use moondream and llava for testing Image or for diabetes chart 

- use ohc scribe / prompt for whisper / llm document update. 

--

Competition

- Voice Assistant
    - hellopatient.com
    - nyra.health
    - ohc.network - scribe

- Data management platform
    - 1MG
    - Practo
    - Apollo Health

---

Customer - 001

Customer interaction 

[21/11, 12:43] Developer: Hi 

I've started to build a simple Health tracking website. 

Link- sanjeevini.me

Let me know, if you are free and
can give me advice on what doctors would require for daily work.

[21/11, 13:09] Customer: You mean investigations?

[21/11, 13:14] Developer: Yes. 
The idea is to manage reports with voice ai.
It will listen to conversations and fill the forms. 
Errors will be reduced, 
final approval by Doctors. 


Later this data is analyzed and additonal information is provided .

Automate a bit of Diagnostics

[21/11, 16:21] Customer: Patient Doctor conversation is confidential. You cannot listen to it


[21/11, 16:24] Developer: Yes. We won't listen to it. 
Application will transcribe it without sharing the data outside.
It will be a closed system.

[21/11, 16:30] Developer: The system will be offline .
We use the GPU to do conversion locally. 

It's like alexa/siri/google but everything runs on the laptop.

[21/11, 16:31] Customer: I don't think any doctor will accept it

[21/11, 16:32] Developer: With a working demo,  they will see the advantage of utilizing it.

[21/11, 16:34] Developer: We will test the system with 
Simulated/synthetic audio.

Demo will include 
Uploading the file and see how it creates the report.


[21/11, 21:22] Doctor: It's not that simple. There are lot of rules in the medical field. U can't just test something without legal aid

[21/11, 21:36] Developer: Yes.  This will be done with legal permission before being deployed to a clinic/hospital.

---

Disclaimer

- Not a medical product
- Not a liable for any information provided

--- 

Features - Ideaboard

- Integrations
    - API
        - Aadhar health ID - Ayushman Bharat Digital Mission
    - Import/Export Exchange
        - Write Base Ingestor for data exchange/ 
        - Community can build ingestor for Other Api Systems
            - Xiaomi - MI Fit
            - Apple Health SDK
            - Google Health
            - Samsung Health
- Crawler
    - Web Crawler 
        - Use Kagi/Googe/Brave API for real time access
        - Build WebPage crawler for Internal/External Company Data
    - Git Repo Crawler
        - GitHub/ GitLab Repo crawler for Documents
    - Documnet Storage Crawler
        - Dropbox/ GoogleDrive/ NextCloud Integration
- Voice Agent
    - Request data with Voice
    - Response 
        - Text
        - Voice
- Interoperability
    - Build a fedarated exchange
    - Bring and Take your won data
- One- Click Setup
    - Docker for Local
    - AWS/Azure - Terraform Setup
    - Kubernetes for Multi-system clusters

---

Generic Medicine

- Create a dataset by sourcing data for Medicines sold in India
- Based on composition + Jan Ayush Kendra data
    - Provide information on alternate medicine
    - 

--

Health App

- How does it help to Doctos to improve Diagnosis
- What are the current blockers to Doctor for their daily activities
- Improve Research via data availability from patient history
- Help with collaboration with Research papers and patents

- Tech is irrelevant to Doctors.

- User / Patient
    - Weight
    - Diabetes
    - Prescriptions
    - Diagnostics Reports
    - Appointments
    - Surgery Reports
    - Insurance Info
    - Aadhar Health ID

- Doctor / Hospital
    - Daily Appointments
    - Diganostics Reports
    - Prescriptions
    - Network Hospitals
    - Voice Diarization - Patient Notes


- [Roadmap](docs/roadmap.md)

---

Roadmap

- v0.0.1
    -  Make all entries manually

- v0.0.2
    - PDF upload of diagnostics

-v 0.0.3
    - excel upload of patient info
    - connectors to Health App


--- 


Backend

- Day 1 - Nov 5, 2024
    - Project Setup
        - python3.10 -m venv venv
        - source venv/bin/activate
        - django-admin startproject myproject
        - cd myproject
        - python manage.py startapp myapp
        - python manage.py makemigrations
        - python manage.py migrate
        - python manage.py runserver

---

User App


- Create a Dashboard
    - Appointments
    - Doctors
    - Ailments
    - Prescriptions
    - Body - Data tracking - weight, diabetes/sugar, Blood pressure

--

Why Sanjeevini ?

- TL;DR
    - My father underwent emergency angioplasty(single stent) after a previous Heart attachk (Myocardiac Infraction) was undetected.
    - Breathelesness led to Hospital visit, after a IV drip and diagnosis of Gastric/Aciditiy ? , he was sent home.
    - General physician recommended a cardiologist after observing abnormality in EEG/ECG diagostics
    - Cardiologist asked for prior Heart check reports which was unavaiable instantly.


- What will Sanjeevini do ?
    - Connect with Ayushman Bharat Digital Mission and provide Medical history to Doctor's during Consultation.
    - Provide data management facility to Doctor's with Open Source development 
    - Notify Users about 
        - Daily medication
        - Next appointments
        - 

- What will Sanjeevini not do ?
    - Fix health issues and provide medical advice

--

Research

- By using the platform/application. All users provide permission to make data available for research
- Data will be open-sourced after anonymizing all PII - Personal Information Identifier

---

Revenue

- Subscription 
    - Users / Patient
        - Rs. 1000 per year for User in India
        - Euro/Dollar 25 per year for all other Users 
    - Doctors / Admin
        - Rs. 100 per patient per year in India
        - Euro/Dollar 5 per patient per year outside Inside

- Research Grant
    - Rs. 5 crore - Non-breakable Fixed deposit for 5 years
    - To provide Employment for Max 5 permanent developers
    - To provide Employment for Temporary Data Entry Operators at Hospital/Clinics


- Reference
    - Provide Subsidised/Free Trail for user based on the meditation app
    - Verification of user's - Rs. 1 debit/credit transaction to avoid Spam Users.
        - Use Stripe for payments 

---

Tool call - Api integration 


Crawl the Swagger api, build the function call based on description from api 

Improve the function description to get better results. 

Send the updated prompt to server. 

System call will be tool. 

Add - additional instructions on how the data should be returned.

User voice queries will be user prompt. 

--

Eval setup and automation.

Build set of base queries for evaluation. 

Test the system for accuracy for the base queries .

--

Level 1 - solve for english

Level 2 - solve for kannada 

Use indic whisper for kannada- dataset 

Use transliteration to provide output in target language. 


-- 

Demo - 
German to engkish 

English to German

Kanaada to English and vice versa. 

God Level - 

Use neural machine translation to automate full setup.

-- 

v.0.0.1 - roadmap


-- 
- Nov 22

  - Run frontend in preview mode
  - Add user details
    - Name, location, birthdate, ABHA ID, created_date, updated_datae
  - connect charts to reducer / display heartrate, weight, diabetes chart
  - Update values in migration for consistency
    - Write a curl script to populate values,
    - move values from migrations - remove hardcoded values
    - Add integrity checks for data


--

Nov 20


Material ui - mobile font/ css

Entity relationship- data modelling 

Versioon - 0.0.1  
Base features - 


Voice data - synthetic conversations 

Demo - voice to Report- creation 

Create - demo product usage 

Security and encryption 
--

Ability to use for other domains - tax tech ? 

- 

Deployment 

Offline - whisper

Online- whisper from openai


--

Version 0.0.2

- TaxSpahaera
    - Tax Data Analysis
        - Show fixed prompts - as dropdown
        - For better data analysis
        
    - UX Addition
        - Create a temp table which shows output from Prompt llm selected
        - Show highlighted cells as respone from Prompt query 
        - Show selected table data or the second table
        
    - Prompts
        - Request additional prompts from Tax-Advisors
    - Make TaxApp as dashboard with current priority for Job Interview
    - Once dashboard is complete, migrate the changes to Sanjeevini.me for data visualisation.

- Deployment Strategy
    - Create deployment on AWS for Backup access
    - Do better security and move from prototype to secure production application.

- Build webscraper for Swagger/redocly API 
    - Create source mapping to ingest data from different sources
- Use SSO application to build secure authenticaton

--


Voice Interface- canvas

Screen navigation based on voice request  

Action models

Use browser shortcuts,  use frame embeds to show information  

Ask for navigation - bring up integratedv maps.

Understand perplexity ahopping agent - 
New dialog interface,  
Canvas for code execution with docker. 


Convert nlp to sql queries,  
Get data in json. 

Create ux on the fly wirh markdown for tables. 

Recreate Markdown for updates or new queries. 

-- 

Markdown viewers with ux 

--

Infrastrucure 

- Appliance
  - 5 devices - 25000 Euro
    - Laptop - 4000 Euro
    - Accessories - 1000 Euro
    - Requirement
      - RTX 4090 - 16GB VRAM 
      - Max avaiable VRAM to power the local LLM for speech and text
  - 2 dev appliance
    - Founder 1 + Founder 2
  - 1 test machine
    - Exhibition / Sales / Demo
  - 2 User Deployment 
    - Onsite demo at Hospitals/ Demo

- Scale testing
  - How many concurrent users can reliably use the system 


---

Salary

- Founder 1 - Self
  - Basic
    - 60 K Euro - Per Annum , Germany / 20 L Rupees - Per Annum, Blore
  - Work
    - Developer
    - Sales
    - Recruiter
- Founder 2

- Founder 3

- Data Labellers - To be determined
- Sales ? 

---

Subscription

- Cost to Consumers
  - No. of Patients
  - No. of Doctors
  - One Time Appliance Cost
    - Pro Rata - Monthly reduction to give hospital at end of 1/3 year period

- Data Sharing Agreement
    - Anonymouus Data for Research
    - Audit Code and Data Stored by 3rd party


--


Guidance Document for ABDM Compliant HMIS/LMIS

- Creation Verification of ABHA (Health IDs)
    - Documentation (Updated document work in progress) -
        - https://sandbox.abdm.gov.in/docs/healthid
        - Swagger Links (API details): ABHA
        - https://healthidsbx.ndhm.gov.in/api/swagger-ui.html#/

- Linking of Health Records
    - Documentation - HIP
        - https://sandbox.abdm.gov.in/docs/build_hip
        - Swagger Links (API details): HIP Services/ Gateway Services
        - https://sandbox.abdm.gov.in/swagger/ndhm-hip.yaml
    - Knowledge sharing session link
        - Building an HIU Service –
        - https://www.youtube.com/watch?v=72SRn0wevfY&feature=youtu.be
        - FHIR Compliance data packaging -
        - https://www.youtube.com/watch?v=l8TiGXX8E34

- Exchange of Health Records with otherHMIS/LMIS / ABDM Compliant Solutions
    - Documentation - HIU
        - https://sandbox.abdm.gov.in/docs/build_hiu
        - Swagger Links (API details): HIU Services/ Gateway Services Call-back
            - https://sandbox.abdm.gov.in/swagger/ndhm-hiu.yaml
        - Knowledge sharing session link
            - Building an HIU Service - https://www.youtube.com/watch?v=oZ9Z2JtO21Q

- Following records should be FHIR Compliant :
    - Health Document Record
    - Discharge summary
    - OP Consultation
    - Diagnostic
    - Immunization
    - Wellness Record
    - Prescription 
    - FHIR Compliance data packaging –
        - https://www.youtube.com/watch?v=l8TiGXX8E34
    - https://sandbox.abdm.gov.in/docs/main_envelope
    - https://sandbox.abdm.gov.in/docs/diagnostic_report
    - https://sandbox.abdm.gov.in/docs/data_encrypt_decrypt
    - https://sandbox.abdm.gov.in/docs/data_preparation
    - 

- Standards for Coding: 
    - SNOMED CT
    - WHO (ICD)
    - LOINC ( LIMS)
    - Standard integration toolkits/SDKs

    - Toolkit for Snomed CT Codes :-
    https://www.nrces.in/services/tools-and-technologies
    and
    https://www.cdac.in/index.aspx?id=hi_hs_medinfo_sdk_ho
    me
    Below mentioned Guides and Resources are available for
    reference at https://www.nrces.in/resources :

    • Guide for using LOINC in NDHM FHIR Resources – a brief
    guide on using LOINC codes in FHIR resources specifically in
    ABDM.
    • SNOMED CT Integration Guides
    • ICD-10 Mapping Technical Implementation Guide

- Standard Implementation and hand holding Implementation
support through the National Resource Centre for EHR
Standards (NRCeS) [nrc-help@cdac.in]
Integration support through ABDM Develop

- https://abdm.gov.in/publications/policies_regulations/health_data_m
anagement_policy

- https://devforum.abdm.gov.in/


