# Project 1
Group Project #1

Group 1:  
Group Members:  Caroline , Gwen, Charlie, Hubah, Krishen

**Problem Description:** 
Pretend you are the owner/operator of an emergency healthcare clinic needing to build a relational database. You hired some students from the MIST 4610 class at the University of Georgia to create the database for you. They need to know more about your organization to identify which entities, attributes, and relationships are important for you. Start by describing your business as a real client 

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

#5: Aggregate billing information from the Invoice table with patient insurance details from the patient table. Determine the average charge per service and how much is covered by insurance 


#6: Identify times of peak resource usage by joining Appointment, Rooms, Procedures, and Equipment tables. Evaluate if certain equipment is overbooked or underutilized. 

**Generated Data (Mockaroo):**
https://mockaroo.com/7daabbb0 

**DB Dictionary:**


