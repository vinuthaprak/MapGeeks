Assignment 4 - Normalisation 

Team:  Nisarga Venkatesh
	 NUID: 002783878
	 Vinutha Prakash
             NUID:002789155


Normalization eliminates data redundancy and enhances data integrity in the table. Normalization also helps to organize the data in the database. It is a multi-step process that sets the data into tabular form and removes the duplicated data from the relational tables.
 
Normalization organizes the columns and tables of a database to ensure that database integrity constraints properly execute their dependencies. It is a systematic technique of decomposing tables to eliminate data redundancy (repetition) and undesirable characteristics like Insertion, Update, and Deletion anomalies.
 

1st Normal Form (1NF)
A table is referred to as being in its First Normal Form if the atomicity of the table is 1.
Here, atomicity states that a single cell cannot hold multiple values. It must hold only a single-valued attribute.
The First normal form disallows the multi-valued attribute, composite attribute, and their combinations.
 
 
 
 
 
In our table we had multiple values in the column Skills,we modified according to the 1NF form
 
 

 
 
Second Normal Form (2NF)
The first condition for the table to be in Second Normal Form is that the table has to be in First Normal Form.
The table should not possess partial dependency. The partial dependency here means the proper subset of the candidate key should give a non-prime attribute.


Third Normal Form (3NF)
The first condition for the table to be in the Third Normal Form is that the table should be in the Second Normal Form.
The second condition is that there should be no transitive dependency for non-prime attributes, which indicates that non-prime attributes (not a part of the candidate key) should not depend on other non-prime attributes in a table. Therefore, a transitive dependency is a functional dependency in which A → C (A determines C) indirectly, because of A → B and B → C (where it is not the case that B → A).
The Third Normal Form ensures the reduction of data duplication. It is also used to achieve data integrity.

![image](https://user-images.githubusercontent.com/113795459/207501018-35faf574-4a35-42cf-8275-46ecbe6f90da.png)

Fig: ER diagram
Use Cases:
 
1.	Use Case: List the number of job openings in the Boston location. 
	Description: The user is looking for job positions at Boston Location. 
	Actors: User.
	Precondition: The user must have access to the SQL server.
	Steps:
	Actor action – User queries about a number of jobs to order.
	System Responses – An order is made for the Roles that match the Employment in Boston location in the Roles and Company table. 
	Alternate Path: There are no job openings in Boston. 
	Error: No rows selected. 
 
      CREATE View Boston_Jobs as
      SELECT r.Employment, r.Days_posted, c.Location 
      FROM Roles r 
      INNER JOIN company c ON r.companyID = c.companyID 
      WHERE c.Location LIKE 'Boston%';
 
      Select * from Boston_Jobs;
 
 
2.	Use Case: List the companies using artificial intelligence. 
	Description: The user is looking for companies using artificial intelligence.
	Actors: User.
	Precondition: The user must have access to the SQL server.
	Steps:
	Actor action – User queries about companies' number of skills of artificial intelligence.
	System Responses – An order is made for the skills that match the company in the Skills and Company table. 
	Alternate Path: There is no company using artificial intelligence. 
	CREATE VIEW Skills_ArtificialIntelligence as
           SELECT sk.Skills,sk.company,c.Location  
	From Skills sk  
	RIGHT JOIN company c ON sk.CompanyID=c.CompanyID  
	WHEREsk.skills='Artificial Intelligence';
   
	Select * from Skills_ArtificialIntelligence;
 
3.	Use Case: List the companies that posted jobs for less than 10 days. 
	Description: The user is looking for companies that posted jobs for less than 10 days.
	Actors: User.
	Precondition: The user must have access to the SQL server.
	Steps:
	Actor action – User queries about companies that posted jobs for less than 10 days.
	System Responses – An order is made for the skills table that matches the company in the Skills and Company table. 
	Alternate Path: There is no company posted salary within 10days. 
 
	CREATE VIEW jobs_posted as
           SELECT sk.Skills,sk.company,c.Location,sk.Days_posted 
	FROM Skills sk  
	RIGHT JOIN company c ON sk.CompanyID=c.CompanyID  
	WHERE sk.Days_posted<11;
 
	Select * from jobs_posted;
 
4.	Use Case: List the number of job openings in Robert Half
	Description: The user is looking for Robert Half job opening.
	Actors: User.
	Precondition: The user must have access to the SQL server.
	Steps:
	Actor action – User queries about Robert Half job openings.
	System Responses – An order is made skills table that matches the company in the Skills and Company table. 
	Alternate Path: There is no job openings in for Robert Half.
 
	CREATE VIEW company_Robert as
           SELECT sk.Skills,sk.company,c.Location  
	FROM Skills sk 
	RIGHT JOIN company c ON sk.CompanyID=c.CompanyID   
	WHERE sk.Company = 'Robert Half';
 
	Select * from company_Robert;
 
 5.	   Use Case: List the number of companies which has Contract job openings. 
	   Description: The user is looking for contract job positions at all Location.
	   Actors: User.
	   Precondition: The user must have access to the SQL server.
	   Steps:
	   Actor action – User queries about several jobs to order.
	   System Responses – An order is made for the companies that match the 
	   Employment in all locations in the Skills and Company table based on CompanyID. 
	   Alternate Path: There are no contract employment job openings. 
	   Error: No rows selected. 
 
	CREATE VIEW Employment_Contract as
SELECT c.Company,c.Location,sk.Job_role,sk.Employment
	FROM company c
	INNER JOIN Skills sk ON c.CompanyID=sk.CompanyID
	WHERE sk.Employment='Contract';
 
	Select * from Employment_Contract;
 
 6.	   Use Case: List the number of companies which offers Minimum wage salary. 
	   Description: The user is looking for all the Minimum wage job positions at all Location.
	   Actors: User.
	   Precondition: The user must have access to the SQL server.
	   Steps:
	   Actor action – User queries about several jobs to order.
	   System Responses – An order is made for the companies that match the 
	   Minimum wage criteria at all locations in the Roles and Company table based on  CompanyID. 
	   Alternate Path: There are no contract employment job openings. 
	   Error: No rows selected. 
 
	 CREATE VIEW Min_Salary as
 SELECT c.Company,c.Location,r.Minsalary,r.Employment
	 FROM company c
	 INNER JOIN Roles r ON c.CompanyID=r.CompanyID
            WHERE r.Minsalary Like '110%';
 
	Select * from Min_Salary;
 
7. 	Use Case: List the companies that posted jobs for greater than 5 days. 
	Description: The user is looking for companies that posted jobs for more than 5 days.
	Actors: User.
	Precondition: The user must have access to the SQL server.
	Steps:
	Actor action – User queries about companies that posted jobs for more than 5 days.
	System Responses – An order is made for the skills table that matches the company in the Skills and Company table. 
	Alternate Path: There is no company posted salary more than 5 days. 
 
	CREATE VIEW jobs_posted as
          SELECT sk.Skills,sk.company,c.Location,sk.Days_posted 
	FROM Skills sk  
	RIGHT JOIN company c ON sk.CompanyID=c.CompanyID  
	WHERE sk.Days_posted>5;
 
	Select * from jobs_posted;
 
8.	Use Case: List the number of python skill job openings in San Francisco . 
	Description: The user is looking for job openings for python at SF Location.
	Actors: User.
	Precondition: The user must have access to the SQL server.
	Steps:
	Actor action – User queries about several jobs to order.
	System Responses – An order is made for the companies that match the 
	Python skills in SF locations in the Skills and Company table based onCompanyID. 
	Alternate Path: There are no contract employment job openings. 
	Error: No rows selected. 
 
	CREATE VIEW jobsin_Sanfrancisco as
           SELECT sk.Skills,sk.company,c.Location,c.Job_role
        FROM Skills sk
        RIGHT JOIN company c on sk.CompanyID=c.CompanyID
        WHERE sk.skills='Python' and sk.Location=’%San Francisco%’;
 
        Select * from Jobin_Sanfrancisco;
 
9.	 Use Case: List the number of companies which has Internship openings. 
	 Description: The user is looking for Internship job positions at all Location.
	 Actors: User.
	 Precondition: The user must have access to the SQL server.
	 Steps:
	 Actor action – User queries about several jobs to order.
	 System Responses – An order is made for the companies that match the
	 Employment in all locations in the Skills and Company table based on     CompanyID. 
	 Alternate Path: There are no contract employment job openings. 
	 Error: No rows selected.
 
	CREATE VIEW Internship_offer as
SELECT r.Company,r.Location,sk.skills,sk.Job_role,sk.Employment 
	FROM Roles r
	INNER JOIN Skills sk on r.CompanyID=sk.CompanyID
	WHERE sk.Employment='Internship';
	
	Select * from Internship_offer;
 
 10.	Use Case: Created a View to find the companies in New york
	Description: The user is looking for the companies in New york
	Actors: User.
	Precondition: The user must have access to the SQL server.
	Steps:
	Actor action – User queries about several companies
	System Responses – An order is made for the companies that match the location NY. 
	Alternate Path: There are no companies in NewYork. 
  	 
	CREATE VIEW New_York as
	SELECT * from company as c
	WHERE c.location='New York, NY';
 
	SELECT * from New_York;
 
 
 
 
 





