XKCD API
-----------


Prequisities
--------------------

Create an application using XKCD API: https://xkcd.com/json.html

 * Use Python 3 (preferrably Python 3.7+). 
 * You can use external libraries or a framework of your choosing (preferrably FastAPI, Flask).
 * Make the application configurable via environment variables (for example you can make a LISTEN variable, which defines what <host>:<port> the app is listening on).
 * Make sure your code conforms to PEP8. You can also use a formatter like Black.

Endpoints
---------------------

Your application should have these HTTP Rest API endpoints:
 * `GET /comics/current`
    * which returns the metadata of a current comic in a form:
       ```
          {
             "id": <comic id>,
             "description": <description of the current comic>,
             "date": <date of the comic publishment, in form: YY-MM-DD>,
             "title": <lowercase title of the comic>,
             "url": <url address of the image>,
          }
       ```
             
 * `GET /comics/<comic_id>`
    * which returns the metadata of a comic of id <comic_id> in a form:
       ```
          {
             "id": <comic id>,
             "description": <description of the comic>,
             "date": <date of the comic publishment, in form: YY-MM-DD>,
             "title": <lowercase title of the comic>,
             "url": <url address of the image>,
          }
       ```
 * `GET /comics/many?comic_ids=<comic_1>&comic_ids=<comic_id_2>&...&comic_ids=<comic_id_n>`
      * which returns the metadata of comic_id_1, comic_id_2, ..., comic_id_n in a form:
       ```
          [
            {
                "id": <comic id 1>,
                "description": <description of the comic>,
                "date": <date of the comic publishment, in form: YY-MM-DD>,
                "title": <lowercase title of the comic>,
                "url": <url address of the image>,
            },
            {
                "id": <comic id 2>,
                "description": <description of the comic>,
                "date": <date of the comic publishment, in form: YY-MM-DD>,
                "title": <lowercase title of the comic>,
                "url": <url address of the image>,
            },
            ...
            {
                "id": <comic id n>,
                "description": <description of the comic>,
                "date": <date of the comic publishment, in form: YY-MM-DD>,
                "title": <lowercase title of the comic>,
                "url": <url address of the image>,
            }
          ]
       ```
  
  On success return an HTTP status code, which is proper for successful requests.
       
 Edge cases
 -----------
 
  * make sure that you handle non-numeric data. For example, for comic id = `nonnumeric` your API should return HTTP status proper for errors
  * what happens when somebody makes such request? `GET /comics/many?comic_ids=1&comic_ids=1&comic_ids=1`
  * for non-existing comic ids your API should return a HTTP status code proper for missing data
  
 Additional improvements to play with
 ----------------------------------------
 
 What possible additional improvements can you think of? Here are some suggestions, you can try some of them if you like:
  * in-memory-cache for fetched data - you can use an existing one or write your own solution
  * rate limiting requests - when somebody makes more than X requests per minute, return a proper HTTP status (too many requests). Make X configurable.
  * write tests which handle the edge cases and the proper cases. 
  * downloading images - create an endpoint which downloads given image IDs and places them in a directory of your server application. The directory should be configurable by an environment variable. 
        `GET /comics/download?comic_ids=<comic_1>&comic_ids=<comic_id_2>&...&comic_ids=<comic_id_n>`
        When somebody passes an ID which you already have downloaded to the chosen directory, don't make an additional request to xkcd website. 
  * implement an [ETag](https://en.wikipedia.org/wiki/HTTP_ETag) mechanism for all the requests
