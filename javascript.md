### JavaScript Standards
## Modern JavaScript (ES6+)
	· // Use const by default, let when reassignment needed, never var
	const API_URL = 'https://api.example.com';
	let userCount = 0;
 
	// Use arrow functions for callbacks and short functions
	const numbers = [1, 2, 3, 4, 5];
	const doubled = numbers.map(n => n * 2);
 
	// Use template literals
	const greeting = `Hello, ${userName}! You have ${messageCount} new messages.`;
 
	// Use destructuring
	const { firstName, lastName, email } = customer;
	const [first, second, ...rest] = items;
 
	// Use async/await over promises
	async function fetchCustomer(id) {
    try {
        const response = await fetch(`${API_URL}/customers/${id}`);
        if (!response.ok) throw new Error('Customer not found');
        return await response.json();
    } catch (error) {
        console.error('Failed to fetch customer:', error);
        throw error;
     }
	}

## Naming Conventions
	· Variables/Functions: camelCase (getUserData, isActive)
	· Classes: PascalCase (CustomerService, HttpClient)
	· Constants: UPPER_SNAKE_CASE (MAX_RETRY_COUNT, API_TIMEOUT)
	· Private class fields: # prefix (#privateField)

## Code Organization
	· One module per file when possible.
	· Group related functionality into modules.
	· Use named exports over default exports for better refactoring.
	· Keep functions small and focused (< 20 lines ideally).

## Error Handling
	· // Always handle errors in async code
	async function processOrder(orderId) {
    	try {
        	const order = await orderService.getOrder(orderId);
        	await orderService.validate(order);
        	await orderService.process(order);
        	return { success: true, orderId };
    	} catch (error) {
        	console.error(`Order processing failed for ${orderId}:`, error);
        	return { success: false, error: error.message };
    	}
	}
 
	// Use optional chaining and nullish coalescing
	const customerName = user?.profile?.name ?? 'Guest';
	
## API Calls
	· Centralize API configuration and base URLs.
	· Use consistent error handling across all API calls.
	· Implement proper loading states and error messages.
	· Always handle HTTP error status codes appropriately.
