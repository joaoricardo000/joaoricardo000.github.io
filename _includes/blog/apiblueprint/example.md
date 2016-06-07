## Posts [/posts]
The /posts endpoint. Here we will map every HTTP action we need!

### Filter Blog Posts [GET]
Filter posts by query parameters

+ Request

    + Parameters
        + size: 10 (optional, number) - Number of posts per page
        + page: 1 (optional, number) - Page offset
        + post_title: (optional, string) - Post title
        + author_name: (optional, string) - Author name  
  
+ Response 200 (application/json)

    + Attributes (array)
        + (BlogPost)

### Create a New Blog Post [POST]
Receives a valid submission for a new post, and returns new created with id. Requires authentication.

+ Request (application/json)

    + Headers

            access_token: QWxhZGRpbjpvcGVuIHNlc2FtZQ==  

    + Body

            {
            "title": "A title",
            "text": "What is the most amazing letter"
            }

+ Response 200 (application/json)

    + Attributes (BlogPost)