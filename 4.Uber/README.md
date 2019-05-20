# Uber - Cab Riding Service
> Features
* Main
	* Driver - Rider matching
	* ETA (Estimated time of arrival)
	* Live Location
	* Payment
	* Preferred access point
* Additional
	* Fraud detection
	* Cargo/food delivery
	* Car Pool/Share
	* Wallet
	
> References
* [Tech Dummies](https://www.youtube.com/watch?v=umWABit-wbk)
* [Medium](https://medium.com/@narengowda/uber-system-design-8b2bc95e2cfe)
	
> Architecture
	* ![system 1](https://github.com/pakd/sysDes/blob/master/4.Uber/res/arch.jpg)

> APIs or Low Level Design
* Graph Representation of map
	* ![Image](https://github.com/pakd/sysDes/blob/master/4.Uber/res/map_graph.PNG)
	* All the intersection or landmarks can be treated as vertex and roads as edges.
	* Weighted graph, edge weight may represents distance, no of lanes, one way - two way, speed limit etc.
	* Adjacency list is better for map representation as compared to adjacency matrix as list is better for representation for sparse data e.g. think of no of roads connecting to your house, hardly 1 or 2.
	* Routing algorithm - Dijkstra’s or A* algorithm.
	* Fastest routes can be stored as static data to avoid dynamic calculations. K-fastest routes can also be stored in case of some blockage is there in fastest route.
	* Earth - 70% water, 20% greenery or mountain or plain area, only 10% is road which is important.
	* How to have zooms in maps - store static images of map and submaps using quad tree.
* Other feature: check [pdf](https://github.com/pakd/sysDes/blob/master/4.Uber/res/UBER%20system%20design%20%E2%80%93%20Narendra%20L%20%E2%80%93%20Medium.pdf) or "medium" link
