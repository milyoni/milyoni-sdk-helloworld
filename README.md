milyoni-sdk-helloworld
======================

Milyoni SDK Hello World

The purpose of this document is to show how to create a simple hello world client application that uses the SDK.

## Prerequisites:

Dev environment is already [set up] (https://github.com/milyoni/milyoni-development) and nginx is running with correct proxy_pass definitions in the nginx.conf, etc.

### Install ExpressJS & Initialize Test App:
```shell
sudo npm install -g express 
express --ejs test && cd $_ && npm install
```

Open up: [octane-production herokuapp] (http://octane-production.herokuapp.com/) You'll need to auth; ask someone internal to Milyoni :)

* Click ’Thimbl Test Local’ on sidebar 
* Create the “Media Page"
* Click ‘New Media’ on upper right to create a new "media page”
* Enter Test Site (or whatever) for title and localhost for domain and click ‘Create’


### Facebook Developer App Setup

See also [Set up Facebook App](https://github.com/milyoni/sumuru/wiki/Setup-Facebook-App) but this is the general set up:

* Open a browser and Login to your Facebook account
* Then go to https://developers.facebook.com/apps and 
* From Apps dropdown select the Create New App option.
* Set "App Name" to something unique.
* Set "App Namespace" to something unique (optional).
* Submitting should take you to a dashboard.
* Find and click the "Apd Platform" button.
* In the modal, click on Website.
* In the new Website form, add the Site Url: http://local.milyoni.net/
* Click on Save Changes.

### Get Facebook Login Button

Search for login button (once you’re signed in to your Facebook developer page); for me this was at:
[login button](https://developers.facebook.com/docs/reference/plugins/login/)

* Click the Get Code button

A popup with something similar to following snippet to be placed just after opening <body> tag:
```js
<div id="fb-root"></div>
<script>(function(d, s, id) {
  var js, fjs = d.getElementsByTagName(s)[0];
  if (d.getElementById(id)) return;
  js = d.createElement(s); js.id = id;
  js.src = "//connect.facebook.net/en_US/all.js#xfbml=1&appId=<YOUR APP ID>";
  fjs.parentNode.insertBefore(js, fjs);
}(document, 'script', 'facebook-jssdk'));</script>
```

* Go back to your new express test application’s directory and open in your editor: test/views/index.ejs
* Place above Facebook snippet just after <body>

* Then go back and grab the button snippet which may look similar to:
```html
<div class="fb-login-button" data-max-rows="1" data-show-faces="false"></div>
```
and paste back in your index.ejs 

## Embed Code

* Now go back to Octane/SDK and click the Embed Code link in top navbar
* Copy the embed javascript code and place it just under the first Facebook script you pasted
* Now in the window.octaneInitialize initialization section replace:
  *     fb_app_id: 'Your Facebook App Id’ (putting your Facebook id in there instead
  *     media_external_id: “robs_hello_world_external_id” (this external id is arbitrary but don’t use spaces)
  *       media_title: "My Cool Event” (whatever title you’d like) 

* Go back to the express application’s root directory and type:
```shell
$node app
```

* Go to localhost:3000
* Click the Facebook button and authenticate the application

You won’t see much so go back and grab the comments snippet from the SDK/Octane page and place anywhere in your index.ejs file.

* Reload the page and you should see your comments embedded

* Try the same for engagements by embedding that snippet…but you’ll also have to create some engagements. To do so Go to ‘Manage’ on navbar
* Find your app in the table list and find the icon for engagements on the right side of that row; click it
* Add a ‘New Poll’; fill out the form, etc.
* Now go back to localhost:3000 and reload … you should see your new poll
