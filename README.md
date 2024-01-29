# SQL Task Of Stored Procedures
![Snapshot of Problem Statement](https://github.com/rohitwagh07/Internship_Notes/blob/main/Task.jpg)
```SQL
--- Creating Database
Create database EmployeeDB;

--- Use Database
USE EmployeeDB;

--- Create Table - 1
CREATE TABLE MasterDesignation( 
    ID INT PRIMARY KEY IDENTITY(1,1), 
    DesignationName VARCHAR(30)
);

--- Inserting Designations into MasterDesignation Table
INSERT INTO MasterDesignation (DesignationName) VALUES ('Manager'); 
INSERT INTO MasterDesignation (DesignationName) VALUES ('Developer'); 
INSERT INTO MasterDesignation (DesignationName) VALUES ('HR'); 

--- select query Masterdesignation
SELECT * FROM MasterDesignation;

--- Create Table - 2
CREATE TABLE Employee( 
    ID INT PRIMARY KEY IDENTITY(1,1), 
    EmpName VARCHAR(50), 
    Birthdate DATE, 
    DesignationID INT FOREIGN KEY REFERENCES MasterDesignation(ID), 
    Gender INT, 
    EmailID VARCHAR(50), 
    MobNO VARCHAR(20)
);

--- Stored Procedure-1 for get employee record
GO
CREATE PROCEDURE Usp_Employee
AS
BEGIN
    SELECT * FROM Employee;
END;

--- Stored Procedure-2 for Inserting Employee Record
GO 
CREATE PROCEDURE Usp_InsertNewRecord 
    @EmpName VARCHAR(50), 
    @Birthdate DATE, 
    @DesignationID INT, 
    @Gender INT, 
    @EmailID VARCHAR(50), 
    @MobNO VARCHAR(20) 
AS
BEGIN
    INSERT INTO Employee(EmpName, Birthdate, DesignationID, Gender, EmailID, MobNO) 
    VALUES(@EmpName, @Birthdate, @DesignationID, @Gender, @EmailID, @MobNO);
END; 
EXEC Usp_InsertNewRecord @EmpName='Rohit', @Birthdate='2002-05-30', @DesignationID=1, @Gender=1, @EmailID='rohit@gmail.com', @MobNo='7058913538';
SELECT * FROM Employee;

--- Stored Procedure-3 for updating Employee Record
GO 
CREATE PROCEDURE Usp_UpdateEmployeeList 
    @EmployeeID INT, 
    @NewEmpName VARCHAR(50), 
    @NewBirthdate DATE, 
    @NewDesignationID INT, 
    @NewGender INT, 
    @NewEmailID VARCHAR(50), 
    @NewMobNO VARCHAR(20) 
AS
BEGIN
    UPDATE Employee  
    SET EmpName=@NewEmpName, Birthdate=@NewBirthdate, DesignationID=@NewDesignationID, Gender=@NewGender, EmailID=@NewEmailID, MobNO=@NewMobNO  
    WHERE ID=@EmployeeID; 
END; 
EXEC Usp_UpdateEmployeeList @EmployeeID=1, @NewEmpName='coder',@NewBirthdate ='2003-04-15',@NewDesignationID ='2',@NewGender ='1',@NewEmailID ='coader@123',@NewMobNO ='7058913537';
SELECT * FROM Employee;

--- Stored Procedure-4 for delete Employee Record
GO 
CREATE PROCEDURE Usp_DeleteEmployeeDetails  
    @EmployeeID INT
AS
BEGIN
    DELETE FROM Employee WHERE ID=@EmployeeID;
END; 
EXEC Usp_DeleteEmployeeDetails @EmployeeID=1;
SELECT * FROM Employee;

--- Stored Procedure-5 for display Employee Record
GO 
CREATE PROCEDURE Usp_GetEmployeeDetails 
    @EmployeeID INT
AS
BEGIN
    SELECT EmpName, DesignationName, EmailID, MobNO  
    FROM Employee 
    INNER JOIN MasterDesignation ON Employee.DesignationID=MasterDesignation.ID 
    WHERE ID=@EmployeeID; 
END; 
EXEC Usp_GetEmployeeDetails @EmployeeID=1;

--- Stored Procedure-6 for display dropdown list
GO
CREATE PROCEDURE Usp_MasterDesignation
AS
BEGIN
    SELECT * FROM MasterDesignation;
END;
EXEC Usp_MasterDesignation;
```
