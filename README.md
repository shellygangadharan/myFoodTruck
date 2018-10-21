# myFoodTruck


As a developer most of my experience is in core java/ messaging for low latency trading applications used by front office at Investment banks. From UI perspective I mostly worked on Swing. Currently I manage a workflow application for corporate loans where accuracy is of high importance with respect to loan pricing.Most of this work is on core java, JSF, jsp and hibernate.

I had learned Mongodb , REST , microservices sometime back but didn't get a chance to use these in projects which I worked. Did a springboot service a while back for a small functionality. Looking at the problem, this is a good use case for a NOSQL db or may be elastic (Lucence based search engine). As we are looking for only search , we are not worried about transactional properties and hence a relation db is not used. Mongodb does support acid properties at document level, so insertion of documents will not create an issue.

In a production scenario we can have our data sitting on multiple shards so that we can support billions of entries. The search will go to all shards and aggregate the result and give it back to us.

I had worked on Elastisearch before so thought this is an opportunity to try this in mongodb. Mongodb inherently supports geospatial searches. To run this application mongodb will have to be set up. Instructions for set up at the below link. https://docs.mongodb.com/manual/mongo/

I have used STS as the IDE for development. Springboot is used as its setup is quick and it comes with an inbuilt webserver. This application is designed as a REST based application. Annotations are used for REST controllers and mappings.

Three REST APIs are provided

foodTrucks/uploadFile
To upload csv file. The request parameter is file.
foodTrucks/address/{longitude}/{latitude}/{distance} To search for locations. The distance is taken in miles.
foodTrucks/all To get all locations. May be its not required but for testing purpose it helps
At the start of the application there is code which reads data from the provided csv file which is stored in the resources directory. Otherwise the rest api can be used to upload the file you choose.

When building for production I would have designed/deployed this in such a way that there would be

Multiple instances of this service that would be running and registered with a naming server like Eureka
There would be an API gateway like Zuul.
Multiple instances of Api gateway can be running as well so as to not have a single point of failure.
Clients connect to the API gateway for requests and api gateway would load balance the requests to appropriate instances.
Also a web ui would be developed so that users can visualize the locations with a distance displayed from the given search location.
Mongodb will be running in 3 replicas with one in write mode and 2 other in read modes.
Sharding will be done so that we can support as much locations as we want and it still performs faster searches.
Also more test cases.
