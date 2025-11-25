

--

Next step is to identify- 
Gym equipment status.

We use the image from camera feed, use the VLM to detect the equipment and identify -
1. Available- green color
2. In - use - red color 

This will help to find usage metrics, without needing to connect to equipment server.

---

https://github.com/dwani-ai/workshop/blob/main/workshop_demo.py


Use the tabs approach.

On one tab, show the exercise details.

On the second tab,
Show the gym information and calendar.


--- 

Age , validity and created date , should be hidden.
It should not be displayed  .
We use them internally for calculation


--- 


Add the steps in readme file.

How to run the server and client.

What ports to use.


--' 


Next step , 

Provide info about Gym facilities and equipment. 

Also add a calendar,  which loads Info from a json .
It should display planned activities for the month.

--- 


Update the code to load data from json file.

Data should have two table.

User table and exercise table.

 Exercise table will have
Date , User_id and exercise type.


User table will have 
I'd,  user name, age, validity,   created_date 
The endpoints for week/months/year should calculate value and then display info.


--' 

Use gradio and create 3 tables.
Which show top active members for week, month and year.



Add a table for active streaks , 
How many people are coming continously.


Make the tables vertical, 
One below the other.


 It should look like a competition board,  rather than a tracking system


 Now make the change to load table from api.


Create a fastapi program with 3 end points - top5-week, top5-month, top5-year and return the values in json format

