# backand-ionic-starter
Create mobile application with [ionic](http://www.ionicframework.com) and [backand](http://www.backand.com).

1- To run starter, download zip and run ionic start:

    ionic start myApp https://github.com/backand/backand-ionic-starter
    cd myApp

2 - Run with ionic serve function

    ionic serve

3 - Login as guest or with  user and password:

  <b>user</b>: ionic@backand.com

  <b>pwd</b>: backand

4 - Enjoy your mobile application, with backand at server side and full CRUD commands to server.

5 - Want to customize data model or change authorization?
create a free personal application at [backand.com](https://www.backand.com/apps/#/sign_up)

6 - Use following model (or just keep the default Model):

    [
      {
        "name": "items",
        "fields": {
          "name": {
            "type": "string"
          },
          "description": {
            "type": "text"
          },
          "user": {
            "object": "users"
          }
        }
      },
      {
        "name": "users",
        "fields": {
          "email": {
            "type": "string"
          },
          "firstName": {
            "type": "string"
          },
          "lastName": {
            "type": "string"
          },
          "items": {
            "collection": "items",
            "via": "user" 
          }
        }
      }
    ]
7 - change application name in  /js/app.js file at line 26
to your new application name.
