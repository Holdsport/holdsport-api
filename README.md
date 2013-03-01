# Holdsport API documentation
This readme describes the Holdsport REST API.

## Authentication
The API uses http basic authentication. If the username is demo and the password demo:
```bash
http://demo:demo@api.holdsport.dk/v1/teams
```
## Data format
JSON UTF-8 encoded strings.

## The API
### Teams
#### Getting the list of teams
Example
```bash
curl -u "demo:demo" -H "Accept: application/json" http://api.holdsport.dk/v1/teams
```

The result
```json
[
    {
        "id": 6237, 
        "name": "frenke", 
        "primary_color": "", 
        "secondary_color": ""
    }, 
...
    {
        "id": 7369, 
        "name": "Hurricanes", 
        "primary_color": "#ed2637", 
        "secondary_color": "#ffffff"
    }
] 
```

### Activities
#### Getting the list of activities
Example
```
curl -u "demo:demo" -H "Accept: application/json" http://api.holdsport.dk/v1/teams/6237/activities
````

The result
```json
[
    {
        "comment": "", 
        "endtime": "", 
        "id": 256592, 
        "name": "Tur til Tyskland", 
        "pickup_place": "", 
        "pickup_time": "", 
        "place": "", 
        "starttime": "2012-01-13T01:00:00+01:00", 
        "status": "tilmeldt",
        "action_method": "PUT", 
        "action_path": "/v1/activities/256592/activities_users/2363897", 
        "actions": [],
        "no_rsvp_count": 3,
        "no_rsvp": [
            {
                "id": 148295, 
                "name": "Lars Christiansen"
            }, 
            {
                "id": 148288, 
                "name": "Lars J\u00f8rgensen"
            }, 
            {
                "id": 148293, 
                "name": "S\u00f8ren Knudsen"
            }
        ], 
    }, 
    {
        "comment": "", 
        "endtime": "", 
        "id": 256593, 
        "name": "Sverigestur", 
        "pickup_place": "", 
        "pickup_time": "", 
        "place": "", 
        "starttime": "2012-01-27T01:00:00+01:00", 
        "status": "ej tilkendegivet",
        "action_method": "POST", 
        "action_path": "/v1/activities/256593/activities_users", 
        "actions": [
            {
                "activities_user": {
                    "joined_status": 1, 
                    "name": "tilmeld", 
                    "picked": 1
                }
            }
        ],
        "no_rsvp_count": 1,
        "no_rsvp": [
            {
                "id": 148295, 
                "name": "Lars Christiansen"
            }
        ]
    }
]
```
The _status_ value denotes the users current status with respect to the activity.

The _actions_ arrays denotes the possible actions that the user can take with respect to this activity.

_Pagination_ is done by adding a _page_ and _per_page_ parameter.

_no_rsvp_count_ denotes the number of participants who haven't responded yet. _no_rsvp_ is an array
of the first 20 members who haven't responded yet.

Example
```
curl -u "demo:demo" http://api.holdsport.dk/v1/teams/7585/activities?page=2&per_page=10
```
Furthermore, a date parameter can be added to return activities from this day and onwards.

Example
```
curl -u "demo:demo" http://api.holdsport.dk/v1/teams/7585/activities?date=2012-01-1
```
The default for these parameters are _page=1_, _per_page=20_, and _date = today_.

#### Getting the details for a single activity
Example
```
curl -u "demo:demo" -H "Accept: application/json" http://api.holdsport.dk/v1/teams/6237/activities/256592
````

The result
```json
{
    "comment": "", 
    "endtime": "", 
    "id": 256592, 
    "name": "Tur til Tyskland", 
    "pickup_place": "", 
    "pickup_time": "", 
    "place": "", 
    "starttime": "2012-01-13T01:00:00+01:00", 
    "status": "tilmeldt",
    "action_method": "PUT", 
    "action_path": "/v1/activities/256592/activities_users/2363897", 
    "actions": []
}
```

#### Change the user status (attending, unregistering, etc.)
The interesting part of the response is this
```json
{
        "status": "ej tilkendegivet",
        "action_method": "POST", 
        "action_path": "/v1/activities/256593/activities_users", 
        "actions": [
            {
                "activities_user": {
                    "joined_status": 1, 
                    "name": "tilmeld", 
                    "picked": 1
                }
            }
        ]
}
```
_status_ denotes the user's current status with the respect to the activity.
_actions_ is an array of the possible actions for the user. In the example one action is allowed (_tilmeld_ (attend)) and the user status is changed to _tilmeldt_ by performing an _action_method_ (POST in the example) request to the _action_path_ URL (/v1/activities/256593/activities_users in the example) with a json encoded version of
```json
{
  "activities_user": {
                    "joined_status": 1, 
                    "picked": 1
                }
}
```
Or speaking _curl_:
```
curl -H "Content-Type: application/json" -X POST -u "demo:demo" http://api.holdsport.dk/v1/activities/256593/activities_users -d '{"activities_user": {"joined_status": 1, "picked": 1}}'
```
If the request was successful a HTTP status 201 (Created) is returned.

If there was an error a HTTP status 422 (Unprocessable Entity) is returned.

#### Getting the list of attendees for an activity
Example
```
curl -u "demo:demo" -H "Accept: application/json" http://api.holdsport.dk/v1/activities/256593/activities_users
```

The result
```json
[
    {
        "id": 2363898, 
        "name": "Demo Demo", 
        "status": "tilmeldt", 
        "updated_at": "2011-12-21T14:03:42+01:00", 
        "user_id": 58856
    }
]
```

#### Adding a comment to an activity
Example
```
curl -H "Content-Type: application/json" -X POST -u "demo:demo" http://api.holdsport.dk/v1/activities/273260/comments -d '{"comment": {"body": "Testkommentar"}}'
```

### Getting the list of team members
Example
```
curl -u "demo:demo"  -H "Accept: application/json" http://api.holdsport.dk/v1/teams/7585/members
```

The result
```json
[
  { "address" : " ",
    "email" : "info@holdsport.dk",
    "id" : 78776,
    "mobile" : "12345678",
    "name" : "Demo Demo",
    "profile_picture_path": "", 
    "role" : 2
  },
  { "address" : "8000 Aarhus",
    "email" : "fran@juj.dk",
    "id" : 79413,
    "mobile" : "",
    "name" : "Kkk Kkkk"
    "profile_picture_path": "/media/BAhbB1sHOgZmSSI4MjAxMy8wg", 
    "role" : 1
  }
]
```
The _role_ field can have five possible values 1 for player, 2 for coach, 3 for assistant coach, 4 for injured, and 5 for inactive.

The profile picture in the example can be fetched, by fetching the url
```
http://api.holdsport.dk/media/BAhbB1sHOgZmSSI4MjAxMy8wg
```

### Getting a single team member
Example
```
curl -u "demo:demo"  -H "Accept: application/json" http://api.holdsport.dk/v1/teams/7585/members/78776
```

The result
```json
{ "address" : " ",
"email" : "info@holdsport.dk",
"id" : 78776,
"mobile" : "12345678",
"name" : "Demo Demo",
"role" : 2
}
```

### Getting the list of notes for the team
Example
```
curl -u "demo:demo"  -H "Accept: application/json" http://api.holdsport.dk/v1/teams/7585/notes
```

The result
```json
[
    {
        "attachment_path": null, 
        "body": "Det gik rigtig godt i l\u00f8rdags :-)", 
        "created_at": "2013-01-06T23:30:38+01:00", 
        "created_by": "Ole Kristensen", 
        "title": "Kampreferat"
    }, 
    {
        "attachment_path": "/media/BAhbBlsHOgZmSSIpMjAxMy8wMS8wNy8xNV8xOF8yMV82NzNfVWRrbGlwXzIuSlBHBjoGRVQ/Udklip-2.JPG",
        "body": "Hver torsdag fra kl. 17 til 19.", 
        "created_at": "2013-01-06T23:30:38+01:00", 
        "created_by": "Ole Kristensen", 
        "title": "Tr\u00e6ningstider"
    }, 
]
```

The attachment in the example can be fetched, by fetching the url
```
http://api.holdsport.dk/media/BAhbBlsHOgZmSSIpMjAxMy8wMS8wNy8xNV8xOF8yMV82NzNfVWRrbGlwXzIuSlBHBjoGRVQ/Udklip-2.JPG
```

### Getting the user profile
Example
```
curl -u "demo:demo"  -H "Accept: application/json" http://api.holdsport.dk/v1/user
```

Result
```json
{
    "addresses": [
        {
            "city": "aarhus bj", 
            "email": "info@holdsport.dk", 
            "email_ex": "Hyl@h", 
            "mobile": "22775467", 
            "parents_name": "Jens Baggesen", 
            "postcode": "8000", 
            "street": "Dalga ", 
            "telephone": "80964"
        }, 
        {
            "city": "aarhus ", 
            "email": "info@holdsport.dk", 
            "email_ex": "Hyl@h ii. bi", 
            "mobile": "22775467", 
            "parents_name": "Jens Baggesen", 
            "postcode": "8000 b", 
            "street": "Dalga s", 
            "telephone": "80964666"
        }
    ], 
    "birthday": "1925-05-05", 
    "firstname": "Demo han", 
    "id": 99464, 
    "lastname": "Danser Ye",
    "profile_picture_path": "/media/BAhbB1sHOgZmSSJDMjAxMy8wMy8wMS8wOV8wNF8zMF81OTdfU2NyZWVuX1Nob3RfMj"
}
```


### Updating the user profile
Example
```
curl -H "Content-Type: application/json" -X PUT -u "demo:demo" http://apldsport.dk/v1/user -d '{"user": { "addresses": [{"street": "Sandageralle", "postcode": "8300", "city": "Odder", "mobile": "88888887", "email": "test@holdsport.dk"}], "firstname": "Demo", "lastname": "Demosen"}}'
```
A user may have one or two addresses each containing some of the following fields:
street, city, postcode, telephone, mobile, email, email_ex, parents_name

You can upload a profile picture by using a standard Multipart form submit ie.

```
curl -X PUT -F "user[profile_picture]=@photo.jpg" -u "demo:demo" http://api.holdsport.dk/v1/user
```
