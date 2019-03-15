# TinyURL- URL Shortner
> Features
* Main
	* Long url to short url
	* Short url to long url
* additional
	* Customized short url (like any prefix e.g. "iit")
	* Data analytics
	
> References
* [Tushar Roy](https://www.youtube.com/watch?v=fMZMm_0ZhK4)
* [Tech Dummies](https://www.youtube.com/watch?v=JQDHz72OA3c)
	
> Architecture
	* ![]

> APIs or Low Level Design
* APIs 
	* string long2short(string long)
	* string short2long(string short)
* Md5
	* calculate hash of long url and return seven chars(any 7 chars from total of 32 chars)
* Base62,Random
	* [Base62 Conversion](https://www.geeksforgeeks.org/how-to-design-a-tiny-url-or-url-shortener/)
	*62^7 = 3.5 Trillion combinations
* Counter
	* Keep counter and use zookeeper to manager counter services
* DB entry (char longURL[2048], char shortURL[7], char createdAt[7], char expiresAt[7])