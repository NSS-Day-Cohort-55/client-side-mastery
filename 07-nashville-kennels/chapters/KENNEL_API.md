# Nashville Kennels API

Before you start building your React application, you need a database to persist the data for it. Please follow these steps to get it set up.

```sh
cd ~/workspace
mkdir kennel-api
cd kennel-api
touch database.json
```
* The kennel-api is in a different directory than the kennel. Treat this like an external API.

Then copy the following JSON into the `database.json` file.

```json
{
    "animals": [
        { "id": 1, "name": "Doodles", "breed": "Poodle"},
        { "id": 2, "name": "Parsley", "breed": "Great Dane" },
        { "id": 3, "name": "Esme", "breed": "Pitbull" }
    ],
    "customers": [
        {
            "id": 1,
            "name": "Luke Skywalker",
            "address": "976 Tatooine Dr."
        },
         {
            "id": 2,
            "name": "Padmé Amidala",
            "address": "1211 Naboo Lane"
        }
    ],
    "employees": [],
    "locations": [
        {
            "id": 1,
            "name": "Nashville North",
            "address": "8422 Johnson Pike"
        },
        {
            "id": 2,
            "name": "Nashville South",
            "address": "209 Emory Drive"
        }
    ]
}
```

Every time you want to work on your Nashville Kennels application, you'll need to ensure that the API is running.

```sh
json-server -p 8088 -w database.json
```

Go ahead and create a few more pets and customers within each's collections.

## Backup to Github
Make sure you create a repository on your Github account for your API, and hook up the kennel-api directory. Yes, there's only one file being tracked in this repository, and that's ok.

