##Conference Organization - App Engine application for the Udacity training course.

###Task 1 - Design Implementation

In order to complete the first task, adding the four endpoint methods to the API, we needed to define the session class. The session class is the data structure that holds all the information pertaining to our sessions, i.e. name, seats available, date, duration, highlights, etc. The four endpoint methods we were responsible for were as follows: 

1. **getConferenceSessions(websafeConferenceKey)** - Given the websafe key for a conference, return all the sessions belongin to it. In order to achieve this task the session object was stored as the child object of the conference object to which it belongs. This facilitates retrieval of all sessions belonging to a specific conference.
1.  **getConferenceSessionsByType(websafeConferenceKey, typeOfSession)** - Returns all sessions in a conference matching given websafekey with given typeOfSession
1.  **getSessionsBySpeaker(speaker)** -Returns all sessions that contain matching speaker as specified by speaker argument. (Will return to this later to implement speaker as an identity).
1.  **createSession(sessionForm, websafeConferenceKey)** - Given a form with session information and a websafeConferenceKey, it creates a session that is a child of conference of given websafeKey.

###Task 2 - Add Sessions to User Wishlist

Users should be able to mark some sessions that they are interested in and retrieve their own current wishlist. We were free to design the way this wishlist is stored. Define the following Endpoints methods:

1. **addSessionToWishlist(SessionKey)** -- adds the session to the user's list of sessions they are interested in attending.You can decide if they can only add conference they have registered to attend or if the wishlist is open to all conferences.  
1. **getSessionsInWishlist()** -- query for all the sessions in a conference that the user is interested in  
1. **deleteSessionInWishlist(SessionKey)** -- removes the session from the user’s list of sessions they are interested in attending


###Task 3 -Work on Indexes and Queries

Make sure the indexes support the type of queries required by the new Endpoints methods.
Come up with 2 additional queries

Think about other types of queries that would be useful for this application. Describe the purpose of 2 new queries and write the code that would perform them.
Solve the following query related problem

Let’s say that you don't like workshops and you don't like sessions after 7 pm. How would you handle a query for all non-workshop sessions before 7 pm? What is the problem for implementing this query? What ways to solve it did you think of?

###Task 4 - Add Sessions to User Wishlist

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
