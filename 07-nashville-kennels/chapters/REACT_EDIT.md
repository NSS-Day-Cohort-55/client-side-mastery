# Edit an Animal

In this chapter, you are going to learn how to edit an animal's information. We will use a form very similar to the form we used to add an animal except, this time the form will be pre-filled with the current information of the animal we want to edit.

**_Quick Note_:** All of the code you will see from here to the end of this chapter needs to be in place before this feature will work.

## Create the AnimalEditForm Component

This component will populate the input fields with the current values from the API. We will obtain the animal details via a fetch call using a `useEffect()` hook.

Here is the flow of the AnimalEditForm component:

1. Component loads - Save button should be disabled since the data is not available yet.
1. The function passed to `useEffect()` calls API to get the animal based on the animalId in the URL.
1. Data loads and `setAnimal()` is invoked with new data (also set `isLoading` to false)
1. The component is rendered to the DOM, displaying animal details and ready for edits.
1. Make changes. As changes are made, state is updated. 
1. Select `save`.
1. The `updateExistingAnimal` method will call `setIsLoading(true)` - this ensures the user cannot repeatedly click button while API is being updated.
1. Invoke `AnimalManger.update()` to change the API data.
1. Once the API has updated, change the view to display all the animals.

> components/animal/AnimalEditForm.js

```jsx
import React, { useState, useEffect } from "react"
import { update, getAnimalById } from "../../modules/AnimalManager"
import "./AnimalForm.css"
import { useParams, useHistory } from "react-router-dom"

export const AnimalEditForm = () => {
  const [animal, setAnimal] = useState({ name: "", breed: "" });
  const [isLoading, setIsLoading] = useState(false);

  const {animalId} = useParams();
  const history = useHistory();

  const handleFieldChange = evt => {
    const stateToChange = { ...animal };
    stateToChange[evt.target.id] = evt.target.value;
    setAnimal(stateToChange);
  };

  const updateExistingAnimal = evt => {
    evt.preventDefault()
    setIsLoading(true);

    // default values for locationId and customerId
    // if you already have these components/modules in place, you will need to include the correct information
    const editedAnimal = {
      id: animalId,
      name: animal.name,
      breed: animal.breed,
	    locationId: 1,
	    customerId: 1
    };

  //pass the editedAnimal object to the database
  AnimalManager.update(editedAnimal)
    .then(() => history.push("/animals")
    )
  }

  useEffect(() => {
    AnimalManager.getAnimalById(animalId)
      .then(animal => {
        setAnimal(animal);
        setIsLoading(false);
      });
  }, []);

  return (
    <>
      <form>
        <fieldset>
          <div className="formgrid">
            <input
              type="text"
              required
              className="form-control"
              onChange={handleFieldChange}
              id="name"
              value={animal.name}
            />
            <label htmlFor="name">Animal name</label>

            <input
              type="text"
              required
              className="form-control"
              onChange={handleFieldChange}
              id="breed"
              value={animal.breed}
            />
            <label htmlFor="breed">Breed</label>
          </div>
          {/* Be sure to include location and customer */}
          <div className="alignRight">
            <button
              type="button" disabled={isLoading}
              onClick={updateExistingAnimal}
              className="btn btn-primary"
            >Submit</button>
          </div>
        </fieldset>
      </form>
    </>
  );
}

```

## Route for Showing Animal Edit Form

Next, define a new route in **`<ApplicationViews>`** for editing a single animal. Be sure to import the **`<AnimalEditForm>`** component.

```jsx
<Route path="/animals/:animalId(\d+)/edit">
     {isAuthenticated ? <AnimalEditForm /> : <Redirect to="/login" />}
</Route>
```

You will also need to add `exact` to the route for `AnimalDetail`

```jsx
<Route exact path="/animals/:animalId(\d+)">
  {isAuthenticated ? <AnimalDetail /> : <Redirect to="/login" />}
</Route>
```

At this point you should be able to see the edit animal form with a URL like this: `http://localhost:3000/animals/2/edit`

> **NOTE:** It won't fully work yet.

## Add Edit Button to the AnimalCard

In the **`<AnimalCard>`** component, you will add a new button: `Edit`. When the user clicks the button, the route should change to `/animals/:animalId/edit`.

```jsx
  <Link to={`/animals/${animal.id}/edit`}>
    <button>Edit</button>
  </Link>
```

![edit animal button](./images/animals-with-edit-button.png)

At this point, view an AnimalCard. You should see the `Edit` button. Test it out.

Oh no, **Error**. `TypeError: Cannot read property 'push' of undefined`. What is that? We need to import and `useHistory` from `react-router-dom` into the AnimalCard.

> **NOTE:** It _still_ won't fully work yet...but we're close...

## Update method in AnimalManager

> modules/AnimalManager.js

Finally, define a method in your `AnimalManager` for the update fetch call. You will use PUT in the HTTP request. This method will take the updated animal as an object and save to the database.

```js
export const update = (animalObj) => {
	return fetch(`${remoteURL}/animals/${animalObj.id}`, {
		method: "PUT",
		headers: {
			"Content-Type": "application/json"
		},
		body: JSON.stringify(animalObj)
	}).then(data => data.json());
}
```

![animation showing animal edit working](./images/p13zLpAnWm.gif)

## Practice: Add Drop the dropdowns for Location and Customer
1. Refer back to the `AnimalForm` and include dropdowns for Location and 
Customer. You will need to include fetch calls for the list data and `useEffect`.
1. Make sure your data will support each of these requests. Double check your properties on each object and that they relate to good data.

## Practice: Edit Employees, Locations, and Owners

1. Add a button to each employee, location, and owner card to `Edit`.
1. Create new components for editing employees, locations, and owners.
1. In the edit form components, fetch the data of the employee, location, or owner within a `useEffect()` and pre-fill the forms.
1. Add the appropriate routes to `ApplicationViews` to render the edit form when the user clicks the edit button.
1. Update **`<EmployeeManager>`**, **`<LocationManager>`** and **`<OwnerManager>`** with an `update` method to modify existing objects in the API.
