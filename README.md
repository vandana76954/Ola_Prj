
#**OLA DATA ANALYST PROJECT** 

#**Data Columns**
1. Date
2. Time
3. Booking_ID
4. Booking_Status
5. Customer_ID
6. Vehicle_Type – Auto, Prime Plus, Prime Sedan, Mini, Bike, EBike, Prime SUV
7. Pickup_Location- 
8. Drop_Location- 
9. V_TAT - (Time taken to arrive at the vehicle)
10. C_TAT – (Time taken to arrive the Customer)
11. Cancelled_Rides_by_Customer- 
•	Driver is not moving towards pickup location
•	Driver asked to cancel
•	AC is not working (Only for 4-wheelers)
•	Change of plans
•	Wrong Address

12. Cancelled_Rides_by_Driver :
•	  Personal & Car related issues
•	Customer related issue
•	The customer was coughing/sick
•	More than permitted people in there

13. Incomplete_Rides 
14. Incomplete_Rides_Reason
•	Customer Demand
•	Vehicle Breakdown
•	Other Issue

15. Booking_Value
16. Payment_Method
17. Ride_Distance
18. Driver_Ratings
19. Customer_Rating

**#OLA Project Analysis using SQL**

Create Database Ola;

Use Ola;

#1. Retrieve all successful bookings:

Create View Successful_Bookings As
SELECT * FROM bookings
WHERE Booking_Status = 'Success';

#2. Find the average ride distance for each vehicle type:

Create View ride_distance_for_each_vehicle As
SELECT Vehicle_Type, AVG(Ride_Distance)
as avg_distance FROM bookings
GROUP BY Vehicle_Type;

#3. Get the total number of cancelled rides by customers:

Create View cancelled_rides_by_customers As
SELECT COUNT(*) FROM bookings
WHERE Booking_Status = 'cancelled by Customer';

#4. List the top 5 customers who booked the highest number of rides:

Create View Top_5_Customers As
SELECT Customer_ID, COUNT(Booking_ID) as total_rides
FROM bookings
GROUP BY Customer_ID
ORDER BY total_rides DESC LIMIT 5;

#5. Get the number of rides cancelled by drivers due to personal and car-related issues:

Create View Rides_cancelled_by_Drivers_P_C_Issues As
SELECT COUNT(*) FROM bookings
WHERE cancelled_Rides_by_Driver = 'Personal & Car related issue';

#6. Find the maximum and minimum driver ratings for Prime Sedan bookings:

Create View Max_Min_Driver_Rating As
SELECT MAX(Driver_Ratings) as max_rating,
MIN(Driver_Ratings) as min_rating
FROM bookings WHERE Vehicle_Type = 'Prime Sedan';
OLA Data Analyst Project

#7. Retrieve all rides where payment was made using UPI:

Create View UPI_Payment As
SELECT * FROM bookings
WHERE Payment_Method = 'UPI';

#8. Find the average customer rating per vehicle type:

Create View AVG_Cust_Rating As
SELECT Vehicle_Type, AVG(Customer_Rating) as avg_customer_rating
FROM bookings
GROUP BY Vehicle_Type;

#9. Calculate the total booking value of rides completed successfully:

Create View total_successful_ride_value As
SELECT SUM(Booking_Value) as total_successful_ride_value
FROM bookings
WHERE Booking_Status = 'Success';

#10. List all incomplete rides along with the reason:

Create View Incomplete_Rides_Reason As
SELECT Booking_ID, Incomplete_Rides_Reason
FROM bookings
WHERE Incomplete_Rides = 'Yes';

#**OLA Data Analyst Project Using Power BI** 
Segregation of the views:
1. Overall
- Ride Volume Over Time
- Booking Status Breakdown
2. Vehicle Type
- Top 5 Vehicle Types by Ride Distance
3. Revenue
- Revenue by Payment Method
- Top 5 Customers by Total Booking Value
- Ride Distance Distribution Per Day
4. Cancellation
- Cancelled Rides Reasons (Customer)
- cancelled Rides Reasons(Drivers)
5. Ratings
- Driver Ratings
- Customer Ratings
