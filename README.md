This project is a simple web application and server intended to interface with a Google Calendar instance then display information about upcoming events, along with other alerts, video and (eventually) other media to welcome Thoughtworkers and visitors into the office. It is currently configured as a simple HTML/CSS frontend with some Javascript code behind it, supported by JQuery and some Google code to work with the Calendar API, provided an authorized client ID (more on this below). A simple python server is required to run the application, as well.


#### Details

At the moment, the app is a single page with a video at the top, a scroller with alerts in the middle, and six cards with event information at the bottom. The video is currently a local mp4 file (currently the SF office b-roll), but there is a Chrome-related bug with the video however, which will be detailed further below.

The remaining information is pulled from a specific Google Calendar instance, taking the 10 soonest upcoming events and either sorting them into the scroller or the cards below. The cards contain non-allday events, whilst the scroller displays any allday events (intended to be notifications or alerts) present for the current day. Unfortunately, due to constraints with Google's Calendar API, events that span over multiple days will -not- be displayed on days following the starting date: if you'd like an alert to span multiple days, you'll need to enter it once for each day.

At the moment, the code is meant to be run on the local machine the jumbotron is hooked up to, not actually deployed to a live web server. As such, if you do push some new code, you'll have to pull it down into the jumbotron machine and redeploy the app. This can change down the line if someplace to deploy it can be found, but keep security in mind and make sure only the right eyes can view it!


#### Setting Up

1. Install OpenSans
2. Install Python 2.4 or above
3. If you haven't authorized the Google Calendar you wish to draw events and alerts from for development, follow Step 1 of the wizard linked here while logged into the account containing the calendar: https://developers.google.com/google-apps/calendar/quickstart/js Be sure to retain the generated client ID mentioned at the end!
4. Open script.js and paste this client ID into the `var CLIENT_ID = ''` declaration, within the single quotes. (This is something that really should be refactored to read from an external source though...)


#### Deploying The Application

1. cd into the project's root directory
2. Deploy a simple Python server:
  1. If you're using Python 2.X, run `python -m SimpleHTTPServer 8000`
  2. If you're using Python 3.X, run `python -m http.server 8000`
3. Go to the url `http://localhost:8000/` in your browser
4. The first time you access this page, you should see a small 'Authorize' button appear at the very top of the page. Click it and follow the prompts to authorize access to the Calendar
5. The page should now reload and be properly deployed!


#### Bugs & Desired Improvements

1. On Google Chrome, the local video does not loop infinitely as desired. This is because Chrome is set up to take partial data from the video's source instead of loading it all at once, and unless the source is set up to accept partial requests Chrome will refuse to repeat a video, among other limitations. Currently, this is being worked around by installing a page reloader extension that fires whenever the video ends, but this is of course not ideal.
2. There is currently no test suite integrated into the application. Consequently, there is also no build pipeline set up for it either, so implementing both would better maintain the integrity of the project.
3. Client ID currently needs to be manually entered into script.js, as well as manually removed as to not be included in commits. Support to read from an external source would definitely help.
3. It currently only looks good with a very specific screen size on Google Chrome, so some styling fixes would be nice!


This project will be constantly evolving with new fixes and additions you guys can think of, so have fun!
