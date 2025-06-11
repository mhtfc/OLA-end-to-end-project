# OLA-end-to-end-project
create database ola;
use ola;

#1. retrieve all successful booking:
create view successful_booking as 
select * from booking 
where booking_status = 'success';
select * from successful_booking;

#2. find the average ride distance for each vehicle type:
create view  ride_distance_for_each_vehicle as
select vehicle_type, avg(ride_distance)
as avg_distance from booking 
group by vehicle_type;
select * from ride_distance_for_each_vehicle;

#3. get the total number of canceled rides by customers:
create view canceled_rides_by_customers as
select count(*) from booking
where booking_status = 'canceled by customer';
select * from canceled_rides_by_customers;

#4. list top 5 customers who booked the highest number of rides:
create view top_5_customers as
select customer_id, count(booking_id) as total_rides
from booking
group by customer_id
order by total_rides desc limit 5;
select * from top_5_customers;

#5. get the number of rides canceled by drivers due to personal and car-related issues:
create view rides_canceled_by_driver_p_c_issues as
select count(*) from booking
where canceled_rides_by_driver = 'personal & related issue';
select * from rides_canceled_by_driver_p_c_issues;

#6. find the maximum and minimum driver rating for prime sedan booking:
create view max_min_driver_rating as
select max(driver_ratings) as max_rating,
min(driver_ratings) as min_rating
from booking where vehicle_type = 'prime sedan';
select * from max_min_driver_rating;

#7. retrieve all rides where payment was made using UPI:
create view UPI_payment as
select * from booking 
where payment_method = 'UPI';
select * from UPI_payment;

#8. find the average customer rating per vehicle type:
create view avg_cust_rating as 
select vehicle_type, avg(customer_rating) as avg_customer_rating 
from booking
group by vehicle_type;
select * from avg_cust_rating;

#9. calculate the total booking value of rides completed successfully: 
create view total_successful_ride_value as
select sum(booking_value) as total_successful_ride_value
from booking
where booking_status ='success';
select * from total_successful_ride_value;

#10. list all incomplete rides along with the reason:
create view  incomplete_rides_reason as
select booking_id, incomplete_rides_reason 
from booking 
where incomplete_rides = 'yes';
select * from incomplete_rides_reason;
