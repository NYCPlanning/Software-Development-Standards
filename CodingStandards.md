# Coding Standards
## Assumptions for the SDLC (phases)
1. Create and assign a User Story, Task, etc.
2. Analyze.
3. Code(Implementation, via new feature branch).
4. Test locally.
5. Pull Request(of the feature branch).
6. Code Review(peer review).
7. Approve/Reject(by peers)
* A.Deploy to Dev/QA/Staging. 
* R.Return to Developer with feedback.
8. Ready for QA.

## General Principles
### Code Quality Standards
* Readability First: Code is read 10x more than written. Prioritize clarity over cleverness.
* Consistency: Follow established patterns within the codebase. When in doubt, match existing code style.
* DRY Principle: Don't Repeat Yourself. Extract reusable logic into methods, classes, or modules.
* SOLID Principles: Apply Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, and Dependency Inversion where appropriate.
* YAGNI: You aren't gonna need it.

### Code Reviews and PRs
* All code must be peer-reviewed before merging to main branches.
* Reviews should focus on logic, security, performance, and adherence to these standards.
* Address all comments or provide justification before approval.

Suggestions
* Focusing on the Code, Not the Coder.
When reviewing code, keep comments focused on the changes themselves rather than making assumptions about the author. Instead of saying "You did this wrong," try "This approach could lead to performance issues - what do you think about using X instead?" This small shift in language keeps the discussion collaborative and solution-focused. Remember that reviews are about improving the codebase together, not finding fault.

* Balancing Positive and Negative Feedback.
While identifying issues is important, taking time to point out what's working well reinforces good practices and keeps morale high. Start review threads by acknowledging strengths before suggesting improvements. For instance: "The error handling here is really solid. One small suggestion to make it even better..." This balanced approach creates a more constructive review experience and encourages open dialogue.
  
* Handling Disagreements Constructively.
 Different opinions are normal in code reviews, but how we handle them matters. Skip dismissive responses in favor of curiosity and collaboration. Try phrases like "I see your point about X. I'm wondering if Y might help address the performance concerns?" or "Here's another option to consider - what are your thoughts on this approach?" This turns potential conflicts into chances to find better solutions together.

## Version Control
* All new projects use GitHub for repo storage. 
* You can use your personal GitHub although linking your work email to the account as a second email may be helpful.
* New Devs will need to be added to the NYCPlanning organization on GitHub.
* All work related repos should be under the NYCPlanning organization (ownership).
* Keep commits atomic and focused on a single concern.
* Ensure your commits are descriptive, concise and brief. Use the imperative mood (eg. "Fix" rather than "Fixed").
* Everyone does pull requests (Regardless of title).

## Branching Strategy (GitHub Flow)
The table below illustrate how to create different kinds of branches. Use lowercase only for branch names.
<id>: These should match the ID of the task or bug in Azure
<desc>: Short concise descriptions, use hyphens(-) instead of spaces

   Type | Definition | Example | Description
--------|------------|---------|------------
Feature |feat/< id >-< desc >| featcode/13031-user-table | New features
Chore |chore/< desc >| chore/update-axios-to-1.11.0	| Non coding tasks (eg. Dependencies)
Bugfix  |fix/< id >-< desc >| fix/40417-prevent-form-submission |	Correction to simple errors
Hotfix  |hotfix/< id >-< desc >| hotfix/63530-login-form-error |	Urgent critical errors for production
Documentation |docs/< id >-< desc >| docs/45873-update-getting-started |	Doc specific changes
Release |release/v< MAJOR >.< MINOR >.< PATCH >| release/v2.4.1  |	Release preparation 
        
### JavaScript Standards
## Modern JavaScript (ES6+)
// Use const by default, let when reassignment needed, never var
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
// Always handle errors in async code
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




[C# Section](csharp.md)
[DB Section](db.md)
