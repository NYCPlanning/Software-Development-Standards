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
* __Readability First__: Code is read 10x more than written. Prioritize clarity over cleverness.
* __Consistency__: Follow established patterns within the codebase. When in doubt, match existing code style.
* __DRY Principle__: Don't Repeat Yourself. Extract reusable logic into methods, classes, or modules.
* __SOLID Principles__: Apply Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, and Dependency Inversion where appropriate.
* __YAGNI__: You aren't gonna need it.

### Code Reviews and PRs
* All code must be peer-reviewed before merging to main branches.
* Reviews should focus on logic, security, performance, and adherence to these standards.
* Address all comments or provide justification before approval.

__Suggestions__
* __Focusing on the Code, Not the Coder__
When reviewing code, keep comments focused on the changes themselves rather than making assumptions about the author. Instead of saying "You did this wrong," try "This approach could lead to performance issues - what do you think about using X instead?" This small shift in language keeps the discussion collaborative and solution-focused. Remember that reviews are about improving the codebase together, not finding fault.

* __Balancing Positive and Negative Feedback__
While identifying issues is important, taking time to point out what's working well reinforces good practices and keeps morale high. Start review threads by acknowledging strengths before suggesting improvements. For instance: "The error handling here is really solid. One small suggestion to make it even better..." This balanced approach creates a more constructive review experience and encourages open dialogue.
  
* __Handling Disagreements Constructively__
 Different opinions are normal in code reviews, but how we handle them matters. Skip dismissive responses in favor of curiosity and collaboration. Try phrases like "I see your point about X. I'm wondering if Y might help address the performance concerns?" or "Here's another option to consider - what are your thoughts on this approach?" This turns potential conflicts into chances to find better solutions together.

## Version Control
	· All new projects use GitHub for repo storage. 
	· You can use your personal GitHub although linking your work email to the account as a second email may be helpful.
	· New Devs will need to be added to the NYCPlanning organization on GitHub.
	· All work related repos should be under the NYCPlanning organization (ownership).
	· Keep commits atomic and focused on a single concern.
	· Ensure your commits are descriptive, concise and brief. Use the imperative mood (eg. "Fix" rather than "Fixed").
	· Everyone does pull requests (Regardless of title).

## Branching Strategy (GitHub Flow)
The table below illustrate how to create different kinds of branches. Use lowercase only for branch names.
	· <id>: These should match the ID of the task or bug in Azure
	· <desc>: Short concise descriptions, use hyphens(-) instead of spaces

   Type | Definition | Example | Description
--------|------------|---------|------------
Feature |feat/\<id\>-\<desc\>| feat/13031-user-table | New features
Chore |chore/\<desc\>| chore/update-axios-to-1.11.0	| Non coding tasks (eg. Dependencies)
Bugfix  |fix/\<id\>-\<desc\>| fix/40417-prevent-form-submission |	Correction to simple errors
Hotfix  |hotfix/\<id\>-\<desc\>| hotfix/63530-login-form-error |	Urgent critical errors for production
Documentation |docs/\<id\>-\<desc\>| docs/45873-update-getting-started |	Doc specific changes
Release |release/v\<MAJOR\>.\<MINOR\>.\<PATCH\>| release/v2.4.1  |	Release preparation 
        
## Security Standards (OWASP TOP 10)
	https://learn.microsoft.com/en-us/dotnet/standard/security/secure-coding-guidelines
### Input Validation
	· Validate all user input on both client and server sides.
	· Use parameterized queries/ORM to prevent SQL injection.
	· Sanitize output to prevent XSS attacks.
	· Implement proper authentication and authorization checks.
	· https://learn.microsoft.com/en-us/dotnet/standard/security/security-and-user-input
### Sensitive Data
	· Never commit secrets, API keys, or connection strings to source control.
	· Use environment variables or secure configuration management (nice to have an example file).
	· Encrypt sensitive data at rest and in transit.
	· Log security events but never log passwords or sensitive personal data.
### HTTPS and CORS
	· Always use HTTPS in production.
	· Configure CORS policies explicitly, never use wildcard (*) in production.
	· Implement proper CSRF protection for state-changing operations.


## Documentation
### Code Comments
	· Write self-documenting code; use comments to explain "why", not "what".
	· Keep comments up-to-date with code changes.
	· Remove commented-out code; rely on version control instead.

### README Files
	· Every project must have a README with setup instructions, dependencies, and build steps.
	· Document environment variables and configuration requirements.
	· Include troubleshooting section for common issues and/or FAQ.

### API Documentation
	· Document all public APIs with request/response examples.
	· We may use Swagger/OpenAPI for REST APIs.
	· For markdown format documents https://www.markdownguide.org/basic-syntax/
	


* [C Sharp](csharp.md)
* [Databases](db.md)
* [CI/CD](cicd.md)
* [JavaScript](javascript.md)
* [TypeScript](typescript.md)
