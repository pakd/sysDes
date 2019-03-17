# Chat Messenger - Facebook or Whatsapp
> Features
* Main
	* Send or receive text messages(one to one chat)
	* Group chat
	* Show online, last seen
	* Show message- sent, delivered, read
	* Send or recieve media content - images, videos, data files etc.
	* Security - Encrypted end to end message
* Additional
	* History and Search
	* Compression
	* Data analytics (only in facebook, not in whatsapp)
	
> References
* [Tushar Roy](https://www.youtube.com/watch?v=zKPNUMkwOJE)
* [Tech Dummies](https://www.youtube.com/watch?v=L7LtmfFYjc4)
	
> Architecture
	* ![system](https://github.com/pakd/sysDes/blob/master/ChatMessengerWSFB/res/both_online.PNG)
	

> APIs or Low Level Design
* Web Sockets as they are bi-directional or duplex, anyone can initiate communication unlike http which is based on request and response model.

* check online or last seen or offline
	* Redis (user, server, last_heartbeat) e.g. (userA, N1, 17/03/2019:20:02:40), (userB, N2, 17/03/2019:19:02:40)
	* Last heartbeat can be used to find last seen (curr_time - last_heartbeat)
	* Similarly offline or online (( curr_time - last_heartbeat) < 5mins  = online)
	
* Send or receive message
	* If both users are active and socket is open directly send or receive message
	* If reciever is offline, store message in DB (equivalent to msg sent) 
	  ![offline_user](https://github.com/pakd/sysDes/blob/master/ChatMessengerWSFB/res/offline_user.PNG)
	* If receiver comes online, send acknowledgement to sender or move message to read table (equivalent to msg read)
	  ![unread to read](https://github.com/pakd/sysDes/blob/master/ChatMessengerWSFB/res/read_unread.PNG)
	
* Send or receive media content
	* First upload content to cdn/blob storage and then store url or send url to other user.
	  ![cdn](https://github.com/pakd/sysDes/blob/master/ChatMessengerWSFB/res/cdn.PNG)
	  ![image-url](https://github.com/pakd/sysDes/blob/master/ChatMessengerWSFB/res/imageurl.PNG)
	
* Group chat - same as one to one chat but instead of user table make group table which has list of all users in the group.

* History 
	* Take few day's data, compress and store to cdn/blob storage and store url in conversation table
	  ![history-url](https://github.com/pakd/sysDes/blob/master/ChatMessengerWSFB/res/history_storage.PNG)

		
