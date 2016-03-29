##Conference Organization - App Engine application for the Udacity training course.

###Task 1 - Design Implementation

In order to complete the first task, adding the four endpoint methods to the API, we needed to define the session class. The session class is the data structure that holds all the information pertaining to our sessions, i.e. name, seats available, date, duration, highlights, etc. The four endpoint methods we were responsible for were as follows: 

1. **getConferenceSessions(websafeConferenceKey)** - Given the websafe key for a conference, return all the sessions belongin to it. In order to achieve this task the session object was stored as the child object of the conference object to which it belongs. This facilitates retrieval of all sessions belonging to a specific conference.
1.  **getConferenceSessionsByType(websafeConferenceKey, typeOfSession)** - Returns all sessions in a conference matching given websafekey with given typeOfSession
1.  **getSessionsBySpeaker(speaker)** -Returns all sessions that contain matching speaker as specified by speaker argument. (Will return to this later to implement speaker as an identity).
1.  **createSession(sessionForm, websafeConferenceKey)** - Given a form with session information and a websafeConferenceKey, it creates a session that is a child of conference of given websafeKey.  
  
***Design Choices Response***    
  
*In the end I opted for defining a speaker as a string object. The reason for this is to avoid the overhead that is involved in managing an entity; basically, for the sake of simplicity and space efficiency. When we write an entity into the Datastore we write into multiple entity indexes:*
  
1. the entity itself into the entity's table  
1. we also write into the by_kind indexes  
1. we also write into each of the different property indexes  
1. we also write into the composite indexes

*Also, by following this approach, we also save the space of the key of the entity, which ultimately saves more space.*

###Task 2 - Add Sessions to User Wishlist

Users should be able to mark some sessions that they are interested in and retrieve their own current wishlist. We were free to design the way this wishlist is stored. Define the following Endpoints methods:

1. **addSessionToWishlist(SessionKey)** -- adds the session to the user's list of sessions they are interested in attending.You can decide if they can only add conference they have registered to attend or if the wishlist is open to all conferences.  
1. **getSessionsInWishlist()** -- query for all the sessions in a conference that the user is interested in  
1. **deleteSessionInWishlist(SessionKey)** -- removes the session from the user’s list of sessions they are interested in attending


###Task 3 - Work on Indexes and Queries

Make sure the indexes support the type of queries required by the new Endpoints methods.
Come up with 2 additional queries. Think about other types of queries that would be useful for this application. Describe the purpose of 2 new queries and write the code that would perform them.   
  
***Solution***  

*We were asked to manually add indexes to index.yaml that would
support the type of queries required by the new Endpoints methods.
Since the earlier tasks required we create sessions as children of
conferences, and there were no queries involving sessions, our 
application did not generate indexes for sessions since we would run
queries by ancestor to fetch its children sessions. But what if we 
wanted to return the set of ALL sessions in datastore? This query 
could not be run without first creating the necessary index. An
endpoint method was added as well that would return the set of all
sessions independently of its parent conference:  
getAllExistingSessions().  This would be useful for example if  we wanted a listing of all sessions across  conferences.*

*Another index was added to search sessions by maxAttendees. Let's
say a user likes to attend small sessions because she feels she gets
more bang for her buck when it comes to asking questions, since the
more people in a session, the more questions others ask, thus
limiting the number of questions she gets to ask. This index would
make it possible to find all sessions of small size. The accompanying 
endpoint for running such a query getSessionsBySize() was also added.*

**Solve the following query related problem**

Let’s say that you don't like workshops and you don't like sessions after 7 pm. How would you handle a query for all non-workshop sessions before 7 pm? What is the problem for implementing this query? What ways to solve it did you think of?

***Solution***    

In this problem, we are asked to perform a query by kind (the session kind) and then filter by property (two properties to be exact).  We need to use the inequality filter on the sessionType property to filter out all those sessions that are of type workshop. Then, we need to use another inequality filter to filter out all those sessions with start time later than 7pm. [The problem arises from the limitations imposed on us by Datastore; inequality filters are limited to at most one property][7]. To get around this problem, we can turn our property queries into "set membership tests" using the IN operation, which has the form   
`property IN [value1, value2, ...]`, which tests for membership in a list of possible values. If we assume that our sessions will be an hour long, finding sessions earlier than 7pm will look something like `Session.startTime IN ['9:00','10:00','11:00','12:00','13:00','14:00','15:00','16:00','17:00','18:00']`. This way, we avoid using inequality filters on two different properties and still find a session with start time earlier than 7pm.

###Task 4 - Add a Task

Overview

When a new session is added to a conference, check the speaker. If there is more than one session by this speaker at this conference, also add a new Memcache entry that features the speaker and session names. You can choose the Memcache key.
The logic above should be handled using App Engine's Task Queue.
Define the following Endpoints method

getFeaturedSpeaker()
TO BE COMPLETED


### Setup Instructions
1. Update the value of `application` in `app.yaml` to the app ID you
   have registered in the App Engine admin console and would like to use to host
   your instance of this sample.
1. Update the values at the top of `settings.py` to
   reflect the respective client IDs you have registered in the
   [Developer Console][4].
1. Update the value of CLIENT_ID in `static/js/app.js` to the Web client ID
1. (Optional) Mark the configuration files as unchanged as follows:
   `$ git update-index --assume-unchanged app.yaml settings.py static/js/app.js`
1. Run the app with the devserver using `dev_appserver.py DIR`, and ensure it's running by visiting your local server's address (by default [localhost:8080][5].)
1. (Optional) Generate your client library(ies) with [the endpoints tool][6].
1.  Go to localhost:8080/_ah/api/explorer to test the endpoints for this application


[1]: https://developers.google.com/appengine
[2]: http://python.org
[3]: https://developers.google.com/appengine/docs/python/endpoints/
[4]: https://console.developers.google.com/
[5]: https://localhost:8080/
[6]: https://developers.google.com/appengine/docs/python/endpoints/endpoints_tool
[7]:https://cloud.google.com/appengine/docs/python/datastore/queries#Python_Inequality_filters_are_limited_to_at_most_one_property
