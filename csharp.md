# C# .NET 8 Standards
## Naming Conventions
* Classes/Interfaces: PascalCase (CustomerService, IRepository)
* Methods: PascalCase (GetCustomerById, ProcessOrder)
* Properties: PascalCase (FirstName, IsActive)
* Private fields: _camelCase with underscore prefix (_customerRepository, _logger)
* Local variables/parameters: camelCase (customerId, orderTotal)
* Constants: PascalCase (MaxRetryCount, DefaultTimeout)

## File Organization
* One class per file, filename matches class name. ***Nice to have
* Order members: constants, fields, constructors, properties, public methods, private methods.
* Use regions sparingly and only for large files with logical groupings.

## Modern C# Features
	// Use nullable reference types Nullable reference types - C# | Microsoft Learn
	#nullable enable
	string? name;	

	// Prefer file-scoped namespaces (C# 10+)
	// Traditional namespace declaration
	namespace MyProject
	{
		class Demo
		{
		}
	}

	// File scoped namespace declaration
	namespace MyProject;
	class Demo
	{
	}
 
	// Use record types for immutable data, not mandatory but nice to have
	public record CustomerDto(int Id, string Name, string Email);
	{
		public string GetLabel() => $"{name} - ${price:F2}";
	}
 
	// Leverage pattern matching, not mandatory but nice to have
	public decimal CalculateDiscount(Customer customer) => customer switch
	{
		{ IsVip: true, YearsActive > 5 } => 0.20m, 
		{ IsVip: true } => 0.15m, 
		{ YearsActive > 3 } => 0.10m, 
		_ => 0m
	};
 
	// Use primary constructors where appropriate (C# 12), not mandatory but nice to have
	//Before C# 12:
	public class Product
	{
  		private readonly string _name;
  		private readonly decimal _price;
  		
		public Product(string name, decimal price)
  		{
    		_name = name;
    		_price = price;
  		}
  		public string GetLabel() => $"{_name} - ${_price:F2}";
	}

	//With Primary Constructors:
	public class Product(string name, decimal price)
	{
  		public string GetLabel() => $"{name} - ${price:F2}";
	}

## Async/Await
 * Always use async/await for I/O operations (database, file, network calls).
 * Suffix async methods with Async(GetCustomerAsync, SaveOrderAsync).
 * Never use .Result or .Wait() - this causes deadlocks.
 * Use ConfigureAwait(false) in library code, not in ASP.NET Core applications. (JAIRO CHECK AGAIN THIS LINK 3 times).

## Dependency Injection
 * Use constructor injection for required dependencies.
 * Register services with appropriate lifetimes (Singleton, Scoped, Transient).
 * Depend on abstractions (interfaces) not concretions.
 * Might consider dynamic registration of services…

## Error Handling and Resilience
	// Use specific exceptions
	throw new ArgumentNullException(nameof(customer));
	throw new InvalidOperationException("Order cannot be processed in current state");
 
	// Log before throwing in business logic
	_logger.LogError("Failed to process order {OrderId}", orderId);
	throw new OrderProcessingException($"Unable to process order {orderId}");
 
	// Never catch and swallow exceptions without logging
	// BAD: try { ... } catch { }

	// Good idea to use RESULT PATTERN and POLLY

## LINQ and Collections
 * Use LINQ for clarity, but be mindful of performance with large datasets.
 * Prefer List<T> for internal collections, return IEnumerable<T> from methods.
 * Use collection expressions (C# 12): List<int> numbers = [1, 2, 3, 4]; -- Nice to have, not mandatory

## Testing Standards
### Unit Testing (C#)
1. Use xUnit, NUnit, or MSTest. 
2. Follow AAA pattern: Arrange, Act, Assert.
3. Use meaningful test names: MethodName_Scenario_ExpectedBehavior.
4. Mock external dependencies using Moq or Nsubstitute, X.
5. Aim for 80%+ code coverage on business logic. 

i.e. 

	[Fact] 
	public async Task GetCustomerAsync_WithValidId_ReturnsCustomer()
	{ 
		//Arrange 
		var mockRepo = new Mock<ICustomerRepository>(); 
		mockRepo.Setup(r => r.GetByIdAsync(1))
		.ReturnsAsync(new Customer { Id = 1, Name = "Test" }); 
		
		var service = new CustomerService(mockRepo.Object); 
		
		// Act 
		var result = await service.GetCustomerAsync(1); 
		
		// Assert 
		Assert.NotNull(result); 
		Assert.Equal(1, result.Id); 
	} 

