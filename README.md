#Conference Organization - App Engine application for the Udacity training course.

###Task 1 - Design Implementation
In order to complete the first task, adding the four endpoint methods to the API, we needed to define the session class. The session class is the data structure that holds all the information pertaining to our sessions, i.e. name, seats available, date, duration, highlights, etc.
The four endpoint methods we were responsible for were as follows:
1.getConferenceSessions(websafeConferenceKey)
	-Given the websafe key for a conference, return all the sessions belongin to it. In order to achieve this task the session object was stored as the child object of the conference object to which it belongs. This facilitates retrieval of all sessions belonging to a specific conference.
2. getConferenceSessionsByType(websafeConferenceKey, typeOfSession)
	-Returns all sessions in a conference matching given websafekey with given typeOfSession.
3. getSessionsBySpeaker(speaker)
	-Returns all sessions that contain matching speaker as specified by speaker argument. (Will return to this later to implement speaker as an identity.)
4. createSession(sessionForm, websafeConferenceKey)
	-Given a form with session information and a websafeConferenceKey, it creates a session that is a child of conference of given websafeKey.

###Task 2 - Add Sessions to User Wishlist

The user wishlist was modeled after the conference registration procedure. This avoids having to make calls to datastore to retrieve entities.

###Task 3 - Indexes and Queries

TO BE COMPLETED

###Task 4 - Add Sessions to User Wishlist

TO BE COMPLETED

## Products
- [App Engine][1]

## Language
- [Python][2]

## APIs
- [Google Cloud Endpoints][3]

## Setup Instructions
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
1. Deploy your application.


[1]: https://developers.google.com/appengine
[2]: http://python.org
[3]: https://developers.google.com/appengine/docs/python/endpoints/
[4]: https://console.developers.google.com/
[5]: https://localhost:8080/
[6]: https://developers.google.com/appengine/docs/python/endpoints/endpoints_tool
