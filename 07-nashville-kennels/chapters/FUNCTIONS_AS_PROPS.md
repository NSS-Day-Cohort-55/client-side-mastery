# Passing Functionality as Props

It's time to add one of the CRUD methods to your application. You're going to start with DELETE. Specifically, you're going to start with discharging animals to remove them from the kennel. You are going to add a "Discharge" link to each animal card.

## Implementation of Delete Function

>**A Note About Component Method Definitions:** If a method will be passed to a child component to execute, via props, you must use the arrow function syntax.

First add the `delete` function to your `AnimalManager` module.

```js
export const deleteAnimal = id => {
  return fetch(`${remoteURL}/animals/${id}`, {
    method: "DELETE"
  }).then(result => result.json())
}
```

We can now invoke `deleteAnimal()` from anywhere.

Before we include the delete functionality in a component, consider following:

* The discharge button will exist on the **`<AnimalCard />`** component.
* When an animal is removed, our animals array within the parent's state will need to reflect the updated list of animals.

### Flow of events

1. Click the discharge button
1. Invoke a `handleDeleteAnimal` function which will invoke the AnimalManager `deleteAnimal` function, be sure to pass the id.
1. Once an item is deleted, we should invoke the AnimalManager `getAllAnimals()` method.
1. With new data, invoke `setAnimals()` and set **animals** equal to the new data.
1. The component re-renders to display the new `animal` data.
1. **`<AnimalList>`** render maps over the data and displays cards for each animal.

**The component where state lives is the only place state can change. Children components cannot change state.**

Add the following function to your **`<AnimalList>`** component and remember to import the methods from AnimalManager.

```js
const handleDeleteAnimal = id => {
    deleteAnimal(id)
    .then(() => getAllAnimals().then(setAnimals));
};
```

Remember that every time you invoke the `setAnimals()` method, it changes the state of the component and forces React to re-render it. The `deleteAnimal()` function deletes an animal object from the API, and then queries the database for all the animals(now updated). When state is updated, the component renders again using the data in the new animal array.


## Pass the Delete Function to AnimalCard Component

Now we can pass the `handleDeleteAnimal` function to a child component giving the child component the ability to invoke the function found on the parent.

Change the return in **`<AnimalList />`**

```jsx
export const AnimalList = () => {

  // ...code omitted for brevity...

  return (
    <div className="container-cards">
      {animals.map(animal =>
        <AnimalCard
          key={animal.id}
          animal={animal}
          handleDeleteAnimal={handleDeleteAnimal} />)}
    </div>
  );
};
```

**`AnimalCard`** component receives two props:

1. The `handleDeleteAnimal` function reference
1. The `animal` object


You pass the function reference to the child component because that's where it will be invoked. Just like a primitive value, such as a string or an integer, you can pass function references from a parent component to a child component. The child component can then specify when that functionality should be invoked, even though it was defined on its parent.

## Implementation of Delete Link

Add the button to the **`<AnimalCard />`** HTML for the veterinarian to select and discharge an animal. In the code below, there is a new `<button>` element that contains the word *Discharge*.

> AnimalCard.js

```jsx
import React from 'react';
import "./Animal.css";

export const AnimalCard = ({ animal, handleDeleteAnimal }) => {
  return (
    <div className="card">
      <div className="card-content">
        <picture>
          <img src={'/images/dog.svg'} alt="My Dog" />
        </picture>
        <h3>Name: <span className="card-petname">
          {animal.name}
        </span></h3>
        <p>Breed: {animal.breed}</p>
        <button type="button" onClick={() => handleDeleteAnimal(animal.id)}>Discharge</button>
      </div>
    </div>
  );
}

```

---

## Practice: Terminate Employees

Add the same functionality to the **`EmployeeList`** component so that employees can be terminated.

## Practice: Remove Owners

Add the same functionality to the **`OwnerList`** for when they decide they no longer want to be a customer.

## Practice: Close a Location

Add the same functionality to the **`LocationList`** for when a location closes down.
