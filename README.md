# Project 1
Group Project #1

Group 1:  

Group Members: 

Hubah https://github.com/hubahakhtar/Project1

Gwen https://github.com/gaw63800/GroupProjectMIST4610-Group1

Krishen https://github.com/supersomeone03/Project-1

Charlie https://github.com/charles8888/Project-1

Caroline https://github.com/carolinetcooper6/Group-Project-1



**Problem Description:** 
Pretend you are the owner/operator of an emergency healthcare clinic needing to build a relational database. You hired some students from the MIST 4610 class at the University of Georgia to create the database for you. They need to know more about your organization to identify which entities, attributes, and relationships are important for you. Start by describing your business as a real client.

**Data Model:**
![Screenshot 2024-04-02 at 3 40 36 PM](https://github.com/hubahakhtar/Project1/assets/165077668/cca0a26c-7349-4f21-bff1-ab18a6f6f94c)

**Queries:**  
4 Simple Queries: 

#1: Select the name and DOB for all patients born in 1999 

    SELECT patient_Name, `date of birth`,

    FROM patient

    WHERE `date of birth` regexp "1999";

![1](https://github.com/hubahakhtar/Project1/assets/165077668/bb473a78-456e-47cf-ac8d-ed110a5341c4)

#2: Show the name of patient and show their invoice number and amount due

    SELECT patient_Name, Invoice_InvoiceNum, Charge 

    FROM patient 

    JOIN patient_has_Invoice ON patient_has_Invoice.patient_patientID = patient.patientID; 

![2](https://github.com/hubahakhtar/Project1/assets/165077668/2ce5134b-c8f8-481d-8e20-840618bc81cc)

#3: Display all existing appointments along with the date and name of patient 

    SELECT patient_Name, appointmentID, Date 

    FROM patient 

    JOIN Appointment ON Appointment.patient_patientID= patient.patientID; 

![3](https://github.com/hubahakhtar/Project1/assets/165077668/5435a87d-265e-43a0-84f9-0c0f9c549cf0)

#4: Display all appointments for a particular staff member 

    SELECT staffID, staffName, staff_schedule,appointmentID, Date 

    FROM Staff 

    JOIN Appointment ON Appointment.Staff_staffID = Staff.staffID 

    WHERE staffID = "1552"; 

![4](https://github.com/hubahakhtar/Project1/assets/165077668/52d3c67d-29c8-4a90-a7d0-e308e25940e9)

6 Complex Queries:

#1: Display the patient name, DOB, and their review number and review description 

    SELECT p.`date of birth`,p.patient_Name, r.reviewNum, r.Desc 

    FROM patient p 

    JOIN Review r ON p.patientID = r.patient_patientID; 

![5](https://github.com/hubahakhtar/Project1/assets/165077668/e1814a73-9007-4beb-8b34-25014447ca80)

#2: Find all appointments scheduled for 2027-10-21 along with the patient's name and the staff assigned to each appointment. 

    SELECT a.appointmentID, a.Date, p.patient_Name, s.staffName 

    FROM Appointment a 

    JOIN patient p ON a.patient_patientID = p.patientID

    JOIN Staff s ON a.Staff_staffID = s.staffID 

    WHERE DATE(a.Date) ='2027-10-21'; 

![6](https://github.com/hubahakhtar/Project1/assets/165077668/fdc516e6-d26e-4093-9721-e05780ca2306)

#3: Evaluate staff performance based on the number of appointments attended and the corresponding average patient reviews. 

    SELECT s.staffID, s.staffName,   

    COUNT(a.appointmentID) AS num_appointments_attended,  

    AVG(r.Rating) AS average_review_rating 

    FROM Staff s 

    JOIN Appointment a ON s.staffID = a.Staff_staffID 

    JOIN Procedures pr ON a.appointmentID = pr.Appointment_appointmentID 

    JOIN patient p ON p.patientID = a.patient_patientID 

    JOIN Review r ON r.patient_patientID = p.patientID 
  
    GROUP BY s.StaffID, s.StaffName; 

![7](https://github.com/hubahakhtar/Project1/assets/165077668/02ba5172-c277-42b4-9e0c-ccd445956918)

#4: Retrieve all appointments scheduled for Cesaro Troake along with their emergency contact details.  

    SELECT a.appointmentID, a.Date, e.EC_Phone, e.EC_Address, p.patient_Name 

    FROM Appointment a 

    JOIN patient p ON a.patient_patientID = p.patientID 

    JOIN Emergency_Contact e ON p.patientID = e.patient_patientID 

    WHERE p.patient_Name = 'Cesaro Troake'; 

![8](https://github.com/hubahakhtar/Project1/assets/165077668/aa3c5e07-20ca-41f5-83c0-7242a6e5ec6c)

#5: Determine the average number of appointments per staff member over a given period, and display those exceeding the average in descending order 

    SELECT Staff.staffID, Staff.staffName,

    COUNT(Appointment.appointmentID) AS NumberOfAppointments 

    FROM Staff 

    JOIN Appointment ON Staff.staffID = Appointment.Staff_staffID 

    WHERE Appointment.Date BETWEEN '2025-08-25' AND '2027-11-03' 

    GROUP BY Staff.staffID, Staff.staffName 

    HAVING
    COUNT(Appointment.appointmentID) > ( 

    SELECT (AVG(AppointmentCounts.NumberOfAppointments) - 0.1) -- Slight adjustment for precision 
    FROM ( 
    SELECT COUNT(Appointment.appointmentID) AS NumberOfAppointments 

    FROM Appointment 

    WHERE Appointment.Date BETWEEN '2025-08-25' AND '2027-11-03' 

    GROUP BY Appointment.Staff_staffID 
    ) AS AppointmentCounts 
    ) 

    ORDER BY NumberOfAppointments DESC; 

![9](https://github.com/hubahakhtar/Project1/assets/165077668/086bc7ac-8f6d-4858-b99b-e089cfac65ee)

#6 Identify patients with the largest balance due on their invoices with a balance exceeding $10,000. Order the balances due in descending order and display the total average balance due. 

    SELECT p.patientID, p.patient_Name, i.InvoiceNum, 

    SUM(i.Balence_Due) AS TotalBalanceDue, 

    (SELECT AVG(Balence_Due) FROM Invoice) AS TotalAverageBalanceDue 
    
    FROM patient p
    
    JOIN patient_has_Invoice pi ON p.patientID = pi.patient_patientID 
    
    JOIN Invoice i ON pi.Invoice_InvoiceNum = i.InvoiceNum 
    
    GROUP BY p.patientID, p.patient_Name, i.InvoiceNum 
    
    HAVING SUM(i.Balence_Due) > 10000 
    
    ORDER BY TotalBalanceDue DESC; 

![10](https://github.com/hubahakhtar/Project1/assets/165077668/e8b18ca6-3ca4-4f25-92bb-67f723a93190)


**Generated Data (Mockaroo):**
https://mockaroo.com/7daabbb0 

**Data Dictionary:**
![a](https://github.com/hubahakhtar/Project1/assets/165077668/7a64e8b4-8c83-4592-a511-4bac269b6c31)
![b](https://github.com/hubahakhtar/Project1/assets/165077668/1b405496-527a-477e-8618-04d4744fc516)
![c](https://github.com/hubahakhtar/Project1/assets/165077668/aa4b585e-9538-4532-89a4-5c052cf010a2)
![d](https://github.com/hubahakhtar/Project1/assets/165077668/8466fb3d-078f-4500-a830-8e3604799da5)
![e](https://github.com/hubahakhtar/Project1/assets/165077668/cad393a8-ac0a-4c28-b77c-e9e023e06daf)
![f](https://github.com/hubahakhtar/Project1/assets/165077668/4c01d12e-b669-4fb5-8635-91ae9af622eb)
![g](https://github.com/hubahakhtar/Project1/assets/165077668/f5076d99-9b9f-4ede-9623-a4a82f12706e)
![h](https://github.com/hubahakhtar/Project1/assets/165077668/4fe80fbc-3c9b-4cf4-9036-9eaa2c95adcb)
![i](https://github.com/hubahakhtar/Project1/assets/165077668/21006f80-bea4-4e38-ba85-a2594841a396)
![j](https://github.com/hubahakhtar/Project1/assets/165077668/1ab2a81b-46ee-4950-be0f-0df01062a41e)
![k](https://github.com/hubahakhtar/Project1/assets/165077668/9cdb1a06-1d9f-4f9b-b248-6bb0cc35c0f1)
![l](https://github.com/hubahakhtar/Project1/assets/165077668/a8aebabd-e6fd-4fd7-ba35-3c598d78430c)
![m](https://github.com/hubahakhtar/Project1/assets/165077668/b8a40c99-630a-49ba-95bd-6d39c489c8bc)
