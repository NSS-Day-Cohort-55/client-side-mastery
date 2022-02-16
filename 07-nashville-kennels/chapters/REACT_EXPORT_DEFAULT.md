# Export Default 

Refactor one of your `database manager` files to use `export default` 

```
const remoteURL = "http://localhost:5002"

const CustomerManager = {
	getAllCustomers: () => {
		return fetch(`${remoteURL}/customers`)
		.then(res => res.json())
	},
	getCustomerById: (id) => {
		return fetch(`${remoteURL}/customers/${id}?_embed=animals`)
		.then(res => res.json())
	}

}
export default CustomerManager;
```

You will need to import the `CustomerManager` to use the functions:

```
import CustomerManager from '../../modules/CustomerManager';
```

And then invoke the specific function:
```
CustomerManager.getAllCustomers()
```