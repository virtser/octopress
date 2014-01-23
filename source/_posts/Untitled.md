API Implementation 

![image](/images/api.gif)

Currently we are in the process of building of soild APIs for each of [eToro](http://www.etoro.com/) main domains. It is not an easy task at all, as we didn't invest too much in the past 7 years of eToro existance in all the architectural aspects of the system. 

How services interact with each other? Who is responsible of doing what? What are the standard that we are working with? Which techology do we choose for specific task? All these questions were not answered until now. Today we start to talk and think about it along with progressing with our first and main API - User API. It is where it all begins - user created for the first time, user details updated, etc...

Today we still have one Users table in our big database which holds all our customers records in addition to their basic details and more irrelevant to user stuff. Each application can update (or read) this table from code without going through a dedicated API - the User API we are working on. The problem with this approach is that there is no [single source of truth](http://en.wikipedia.org/wiki/Single_Source_of_Truth) - each and every service can apply its own business logic to change user related data, which leading to data  inconcictency.

Our goals in User API implementation are:

1. To create the "Single Source of Truth".
2. To provide notifications of user changes to different services via Pub/Sub.
3. To separate User related data to it's own dedicated database.


Lessons learned:

1. Don't start it when it's too late - invest in your architecture from the beginnig.

2. Build a plan - API establishment, integration (insert, update, select)

3. 