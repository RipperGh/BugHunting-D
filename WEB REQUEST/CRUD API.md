# APIs

several types of APIs. Many APIs are used to interact with a database, such that we would be able to specify the requested table and the requested row within our API query, and then use an HTTP method to perform the operation needed. For example, for the api.php endpoint in our example, if we wanted to update the city table in the database, and the row we will be updating has a city name of london, then the URL would look something like this:

```
Code: bash
curl -X PUT http://<SERVER_IP>:<PORT>/api.php/city/london ...SNIP...
```
# CRUD
we can see, we can easily specify the table and the row we want to perform an operation on through such APIs. Then we may utilize different HTTP methods to perform different operations on that row. In general, APIs perform 4 main operations on the requested database entity:

## **Operation	|HTTP Method|	Description**
  * Create	**POST**	Adds the specified data to the database table
  * Read	**GET**	Reads the specified entity from the database table
  * Update	**PUT**	Updates the data of the specified database table
  * Delete	**DELETE**	Removes the specified row from the database table
    
our operations are mainly linked to the commonly known CRUD APIs, but the same principle is also used in REST APIs and several other types of APIs. Of course, not all APIs work in the same way, and the user access control will limit what actions we can perform and what results we can see.


# Read
 first thing we will do when interacting with an API is reading data. As mentioned earlier, we can simply specify the table name after the API (e.g. /city) and then specify our search term (e.g. /london), as follows:

CRUD API
 ```
GhostRipper@htb[/htb]$ curl http://<SERVER_IP>:<PORT>/api.php/city/london

[{"city_name":"London","country_name":"(UK)"}]
```

To have it properly formatted in JSON format, we can pipe the output to the jq utility, which will format it properly. We will also silent any unneeded cURL output with -s, as follows:

```
GhostRipper@htb[/htb]$ curl -s http://<SERVER_IP>:<PORT>/api.php/city/london | jq

[
  {
    "city_name": "London",
    "country_name": "(UK)"
  }
]
```
As we can see, we got the output in a nicely formatted output. We can also provide a search term and get all matching results:
```
GhostRipper@htb[/htb]$ curl -s http://<SERVER_IP>:<PORT>/api.php/city/le | jq

[
  {
    "city_name": "Leeds",
    "country_name": "(UK)"
  },
  {
    "city_name": "Dudley",
    "country_name": "(UK)"
  },
  {
    "city_name": "Leicester",
    "country_name": "(UK)"
  },
  ...SNIP...
]
```
Finally, we can pass an empty string to retrieve all entries in the table:
```
GhostRipper@htb[/htb]$ curl -s http://<SERVER_IP>:<PORT>/api.php/city/ | jq

[
  {
    "city_name": "London",
    "country_name": "(UK)"
  },
  {
    "city_name": "Birmingham",
    "country_name": "(UK)"
  },
  {
    "city_name": "Leeds",
    "country_name": "(UK)"
  },
  ...SNIP...
]
```
# Create

To add a new entry, we can use an HTTP POST request, which is quite similar to what we have performed in the previous section. We can simply POST our JSON data, and it will be added to the table. As this API is using JSON data, we will also set the Content-Type header to JSON, as follows:

```
GhostRipper@htb[/htb]$ curl -X POST http://<SERVER_IP>:<PORT>/api.php/city/ -d '{"city_name":"HTB_City", "country_name":"HTB"}' -H 'Content-Type: application/json'
```
Now, we can read the content of the city we added (HTB_City), to see if it was successfully added:
```
GhostRipper@htb[/htb]$ curl -s http://<SERVER_IP>:<PORT>/api.php/city/HTB_City | jq

[
  {
    "city_name": "HTB_City",
    "country_name": "HTB"
  }
]
```
As we can see, a new city was created, which did not exist before.

# Update

Now that we know how to read and write entries through APIs, let's start discussing two other HTTP methods we have not used so far: PUT and DELETE. As mentioned at the beginning of the section, PUT is used to update API entries and modify their details, while DELETE is used to remove a specific entity.

### Note:
The HTTP PATCH method may also be used to update API entries instead of PUT. To be precise, PATCH is used to partially update an entry (only modify some of its data "e.g. only city_name"), while PUT is used to update the entire entry. We may also use the HTTP OPTIONS method to see which of the two is accepted by the server, and then use the appropriate method accordingly. In this section, we will be focusing on the PUT method, though their usage is quite similar.

# Upate Continous 
Using PUT is quite similar to POST in this case, with the only difference being that we have to specify the name of the entity we want to edit in the URL, otherwise the API will not know which entity to edit. So, all we have to do is specify the city name in the URL, change the request method to PUT, and provide the JSON data like we did with POST, as follows:
```
GhostRipper@htb[/htb]$ curl -X PUT http://<SERVER_IP>:<PORT>/api.php/city/london -d '{"city_name":"New_HTB_City", "country_name":"HTB"}' -H 'Content-Type: application/json'
```
We see in the example above that we first specified /city/london as our city, and passed a JSON string that contained "city_name":"New_HTB_City" in the request data. So, the london city should no longer exist, and a new city with the name New_HTB_City should exist. Let's try reading both to confirm:

```
GhostRipper@htb[/htb]$ curl -s http://<SERVER_IP>:<PORT>/api.php/city/london | jq
```
```
GhostRipper@htb[/htb]$ curl -s http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City | jq

[
  {
    "city_name": "New_HTB_City",
    "country_name": "HTB"
  }
]
```
# DELETE

Finally, let's try to delete a city, which is as easy as reading a city. We simply specify the city name for the API and use the HTTP DELETE method, and it would delete the entry, as follows:
```
GhostRipper@htb[/htb]$ curl -X DELETE http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City
```
```
GhostRipper@htb[/htb]$ curl -s http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City | jq
[]
```
As we can see, after we deleted New_HTB_City, we get an empty array when we try reading it, meaning it no longer exists.

# Exercise 
  Exercise: Try to delete any of the cities you added earlier through POST requests, and then read all entries to confirm that they were successfully deleted.

  First, try to update any city's name to be 'flag'. Then, delete any city. Once done, search for a city named 'flag' to get the flag.

  Target: 83.136.253.251:39653

  Answer: HTB{crud_4p!_m4n!pul4t0r}

## Recap
1) These commands allowed me to find the different cities and state in the HMTL ( PHP), I was able to add, delete,and update differnt text in html
2) The issues ran into was trying to figure out why i was not geting the flag after adding city name like beloo 
```
curl http://83.136.253.251:39653/api.php/city/london
curl -X DELETE http://83.136.253.251:39653/api.php/city/london 

curl -X PUT http://83.136.253.251:39653/api.php/city/london  -d ‘{“city_name”:“flag”}’ -H ‘Content-Type: application/json’

curl http://83.136.253.251:39653/api.php/city/flag 
```
3) When I realize why I was not getting the Answer, even though the flag was showing I was weird out. I start to look at forums since I keep deleted and adding non stop.
4) That when I realize that I forgot to include a part which I thought was not important: {"country_name":"HTB"}
   ```
   curl -X PUT http://83.136.253.251:39653/api.php/city/london  -d ‘{“city_name”:“flag”, "country_name":"HTB"}'
   curl http://83.136.253.251:39653/api.php/city/flag 
      HTB{crud_4p!_m4n!pul4t0r}
   ```
