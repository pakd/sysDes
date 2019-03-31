# BookMyShow or Paytm Movie Ticket Booking
> Features
* Main
	* Book a ticket
		* Select a city
		* Select a theatre
		* Select a screen
		* Select a seat
	* Movie Info and trailers, Comments and Rating
	* Payments - offers
	* Movie Recommendations
	* Send email or sms confirmation of ticket.
	
> System Requirements
* Highly Concurrent
* Responsive UI

> References
* [Tech Dummies](https://www.youtube.com/watch?v=lBAwJgoO3Ek)
* [Medium](https://medium.com/@narengowda/bookmyshow-system-design-e268fefb56f5)
	
> Architecture
	* ![system 1](https://github.com/pakd/sysDes/blob/master/BookMyShow/res/sysDes.png)

> APIs or Low Level Design

* Theatre DB
	* Expose APIs to  mediators.
	* Expose Db - mediators can excess theatre db.
	
* SMS and Email confirmaiton - Async workers
	* Network I/O Heavy operations
	* Uses Queue - Asynchronously send confirmations to users.
	* Use of third party services for sms, etc.

* Logstash and Elastic search
	* dump all data to logstash
	* Elastic search will provide search queries to frontend.
	
* DataBase
	* Uses hybrid mechanism
	* Uses RDBMS - country, city, theatre, screen, seat data, transaction data etc
	![RDBMS](https://github.com/pakd/sysDes/blob/master/BookMyShow/res/rdbms.PNG)
	* Uses NoSQL for storing big data such as movie info, cast info , trailers, comments, reviews etc.
	![NoSQL](https://github.com/pakd/sysDes/blob/master/BookMyShow/res/nosql.PNG)
	
* Recommendations
	* Dump log data to hadoop, use machine learning.
	* Use kafka queue for real time analysis, for getting latest trends etc.
	
* Payment - Juspay, third party services. 

* Extras
	* Lock the seat for 10 mins.
	* Use mobile's GPS and laptop's ISP address for recommending theatres.
	* Theatre will give unique id, which can be verified later.