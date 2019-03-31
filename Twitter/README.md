# Twitter
> Features
* Main
	* Tweet (text/ media) - followers should be able to see your tweets
	* Follow
	* Timeline - User and Home
	* Trending - Data analytics
	* Search
	
> References
* [Tech Dummies](https://www.youtube.com/watch?v=wYk0xPP_P_8)
* [Medium](https://medium.com/@narengowda/system-design-for-twitter-e737284afc95)
	
> Architecture
	* ![system 1](https://github.com/pakd/sysDes/blob/master/Twitter/res/arch.jpg)
	* ![system 2](https://github.com/pakd/sysDes/blob/master/Twitter/res/sysdes.PNG)

> Data Modeling
* Data
	* 300 Million + users
	* 600 tweets/sec
	* 6,00,000 tweets/sec
	* Read heavy system, 1:1000 write to read ratio
	* Eventual consistency
	* 140 chars/tweet : 280 is latest.
	 
> APIs or Low Level Design

* Showing home & user timeline - Using Redis cache
	* Whenever some tweets, add the tweet to db and user timeline. 
	* first method - go to the list of all the following users and copy latest tweets from their user timeline.
	but this method is not scalable for even 10 users. the tweet show process will take several minutes for dynamic loading.
	![method1](https://github.com/pakd/sysDes/blob/master/Twitter/res/method1.PNG)
	* fan out method - fan out is pre processing, go to the list of all followers and add the tweet to their home timelines.
	![fanout](https://github.com/pakd/sysDes/blob/master/Twitter/res/fanout.PNG)
	* Fan out process for celebrity users become tricky as they are followed by millions of users.
	If user is following a celebrity, make a list of celebrity. Go to celebrity's user timeline and copy the tweet.
	![celebrity](https://github.com/pakd/sysDes/blob/master/Twitter/res/celebrity.PNG)
	* If user is not logged in for previous 15 days, then dont put in redis/timelines cache.
	
* Trending - Storm or kafka streams
	  ![trend](https://github.com/pakd/sysDes/blob/master/Twitter/res/trend.PNG)
	* 1000 keywords/5 min  >>  10,000 keywords/1 month (vol of keywords and time taken)

* Search - Early Bird - uses inverted full text index
	* ![early-bird](https://github.com/pakd/sysDes/blob/master/Twitter/res/early-bird.PNG)
	* ![ScatterAndGather](https://github.com/pakd/sysDes/blob/master/Twitter/res/scatter_and_gather.PNG)
	
* DB 
	* ![DB_Redis](https://github.com/pakd/sysDes/blob/master/Twitter/res/db_reddis.PNG)