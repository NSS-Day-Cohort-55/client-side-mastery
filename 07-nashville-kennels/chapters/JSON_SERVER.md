# JSON-Server

Sometimes we need data from multiple resources when making a GET requests to an API. Time to build on using `json-server` features to include more data... and sort it.

## Functionality from JSON-Server 

We can use JavaScript to combine data from two different models and to sort the data we display. In many systems, this is can be done on the server-side (back-end), making client-side (front-end) development easier. JSON-Server can do simple expanding and sorting for us.  

This requires three query string parameters.  A query string is defined in a url by adding a `?` at the end of the url followed by the query string. Typically, a query string contains a parameter, the `=` and then a value.  Here's some examples in JSON-server:

1. `_expand=customer` - Include related customer
1. `_expand=location` - Include related location
1. `_sort=location.id` - Sort data by the employee id

Let's try it out with our new kennels database! Go ahead and start your json server for your database if you haven't already:
`json-server -p 8088 database.json -w`

Use Postman to `GET` the following URL:
`http://localhost:8088/animals?_expand=customer&_expand=location`

What do you see? It should show the database objects of all of your animals with their customer and location information nested inside of it!

If you would like a single animal, add the `id` to the url.  It will look something like `http://localhost:8088/animals/2?_expand=customer&_expand=location` for the animal with and id of 2.

We can also use `_sort` to list the animals in order of location or customer. Try `http://localhost:8088/animals?_expand=customer&_expand=location&_sort=locationId` in Postman.  What do you notice about the location ids?  

Try changing location to customer. Now what do you see?
