Executive Summary
Create a LinkedIn Chrome Extension which fetches all the connections of the current logged in user.

Background
1. User downloads the chrome extension
2. Extension checks if user is logged in on LinkedIn.com, if not, it tells them to login
3. Extension gets list of all LinkedIn connections of current logged in user
4. If first time using the app:
a. Extension will fetch all the LinkedIn profiles of the current logged in user, and store them in local storage
b. Extension will then send a dump file of all the profiles to the remote host with all the data of users
5. If not the first time using the app:
a. Extension will call a remote API, and will get in return a JSON response with the list of LinkedIn profile URLs to fetch
b. Extension fetches the profiles from LinkedIn
c. Extension sends the bulk profiles as JSON to remote API

Technology, Solution and Approach
Technology
For Extension: 
1. Javascript
2. jQuery
3. HTML/CSS
For Backend / API creation:
1. Laravel
2. MySQL Database

Solution
1. On first if user will install the extension user need to click on popup from where he will sign in into the extension using Rest API.
2. After signin extension will check if user is login into linkedin or not, if he is not loggedin, we will show the message in popup with link that you need to sign in into linkedin.com.
3. Once user will sign in it will start the process of collecting data in background.
4. For the first time, the extension will collect all the connections of current logged in user and send it to remote host with all the data of users
5. When the user logs in for the second time or henceforth, the extension will ask the remote API if there any profiles that need to be fetched again for updates, and the extension will also check if the connection count of LinkedIn has changed to fetch newly added contacts.
6. For each new or existing profile fetched, the extension will push them to the remote API. 

Mock API to be used:
a) Post API – for the First-time logging in user –This API will post the collected connections to the server with Alarm, i.e. 200 connections will be sent as per the timelines we finalize. For eg. Per hour or per day. API End Point – “save_lead”
b) Get API – for repeating users – This API will check whether there are any changes in the profiles of the connections which we already have collected. It would be done one by one for all the connections. Once it is done, we will update the server with the changes. API End Point – “get_all_collected_lead”
c) Update API – for repeating users – This API will update the changes from the collected connections as well as check for any new connection, if added. API End Point – “update_lead”

