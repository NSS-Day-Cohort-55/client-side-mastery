# The Power of Components

Now that you've seen the core mechanisms of a React application, it's time to consider the purpose of React, or any other component-based tool like Polymer, Vue, and Angular - reusability.

## Reusability Scenario

Right now, the only place that you're rendering an animal is when you select the Animal link in the navbar. What if you want to display the animals an employee is responsible for? You can refactor your application and use the **`AnimalCard`** to display animals along with an employee's information.

First, you will need to update your database to include an employees collection and include an employeeId on each animal.

> kennel.json

```json
  {
  "animals": [
    {
      "id": 2,
      "name": "Doodles",
      "breed": "German Sheperd",
      "employeeId": 3
    },
    {
      "id": 3,
      "name": "Esme",
      "breed": "Pitbull",
      "employeeId": 1
    },
    {
      "name": "Jack",
      "breed": "Big cat",
      "id": 4,
      "employeeId": 1
    },
    {
      "name": "Angus",
      "breed": "Gerbil",
      "id": 5,
      "employeeId": 2
    }
  ],
  "employees": [
    {
        "id": 1,
        "name": "Jessica Younker"
    },
    {
        "id": 2,
        "name": "Jordan Nelson"
    },
    {
        "id": 3,
        "name": "Zoe LeBlanc"
    }
  ]
}
```

**From the practice exercises, you should already have an `<EmployeeList>` and `<EmployeeCard>` components. Those need to be in place before working on this chapter.**

Next, we will include an API call that will get all employees with animals. We can use json-server relationships to include related child information with one call. This is done with `embed`.

> src/modules/EmployeeManager.js

```js
const remoteURL = "http://localhost:5002";

export default {
  getAll() {
        return fetch(`${remoteURL}/employees/`).then(result => result.json())
    },
   getWithAnimals(id) {
        return fetch(`${remoteURL}/employees/${id}?_embed=animals`)
                .then(result => result.json())
    }
}

```

**Note** for best results, you should name your json-server collections with a *plural* and join them together with a *singular*. For example: `employees` collection and join the employee on the animal with `employeeId`.

We need to add a button to the **`<EmployeeCard>`** for details using `history.push` of react-router-dom.

> EmployeeCard.js

```jsx
<button type="button"
        onClick={() => { history.push(`/employees/${employee.id}/details`) }}>Details</button>
```

We also need to add a route to **`<ApplicationViews>`** to handle displaying details of a single employee. This route will return a new component: **`<EmployeeWithAnimals>`** which we will build next.

> ApplicationViews.js

```js
<Route path="/employees/:employeeId(\d+)/details">
  <EmployeeWithAnimals />
</Route>/>
}} />

```
Be sure to import **`EmployeesWithAnimals`** into `ApplicationViews`.

## New Component - EmployeeWithAnimals

This component will display a single employee and include an **`<AnimalCard>`** for each animal. We can re-use the previously created AnimalCard component. This component will accept `props` and `return` the employee name and then `map` over the animals returning **`<AnimalCard>`** for only the pets the employee is responsible for.

> src/components/employee/EmployeeWithAnimals.js

```jsx
import React, { useState, useEffect } from 'react'
import EmployeeManager from '../../modules/EmployeeManager'
import AnimalCard from '../animal/AnimalCard'

export const EmployeeWithAnimals = () => {
  const [employee, setEmployee] = useState({});
  const [animals, setAnimals] = useState([]);

  const {employeeId} = useParams();

  useEffect(() => {
    //got here now make call to get employee with animal
    EmployeeManager.getWithAnimals(employeeId)
      .then(APIResult => {
        setEmployee(APIResult);
        setAnimals(APIResult.animals);
      });
  }, []);

  return (
    <div className="card">
      <p>Employee: {employee.name}</p>
      {animals.map(animal =>
        <AnimalCard
          key={animal.id}
          animal={animal}
        />
      )}
    </div>
  );
};

```

Test it out. Each employee should display a list of animals. However, we are not done.

If we edit an animal, the employeeId is missing. We need to add it to the **`<AnimalEditForm>`**.

## Refactor AnimalEditForm

Add the **employeeId** to:

* `state`
* `updateExistingAnimal()` - where does the employeeId come from?

> **Hint:** Maybe a `select` would the the appropriate way to choose an employee?
> The following code might come in handy.

```jsx
<select
  className="form-control"
  id="employeeId"
  value={animal.employeeId}
  onChange={handleFieldChange}
>
  {employees.map(employee =>
    <option key={employee.id} value={employee.id}>
      {employee.name}
    </option>
  )}
</select>
<label htmlFor="employeeId">Employee</label>
```

> The code above is not all you will need, however. Read it carefully. What does it _imply_ about the other changes you will need to make to the `AnimalEditForm` component?

Once complete, you should be able to edit an animal.

## Refactor the NavBar

If you haven't already done so, be sure to add the link to employees in the **`<NavBar>`** component

```js
<li><Link className="nav-link" to="/employees">Employees</Link></li>
```

## Practice - Handle the delete

If we discharge an animal from the `EmployeeWithAnimals` component, we will receive an error `deleteAnimal is not a function`.

There are a few of ways to handle this situation.

1. Use a conditional and only render the button if the prop `deleteAnimal` exist.
1. Include the same `handleDelete` function within **`<EmployeeWithAnimals>`**
1. Extract the `handleDelete` function and place inside a module that can be imported whenever needed.
1. **Lift** the `handleDelete` function to a common parent component thus allowing both components access.

Choose one of the options above and handle the delete button when the **`<AnimalCard>`** is viewed within the **`<EmployeeWithAnimals>`** component.

## Practice: Employees per Location

1. Modify your API data so that employees have a `locationId` property designating at which location they work.
1. For each location, display the employees that work there.
