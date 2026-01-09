We will follow Microsoft's Best practices for writing unit tests.

[Best practices for writing unit tests - .NET | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/core/testing/unit-testing-best-practices)

Benefits of unit testing
------------------------

1. Less time performing functional tests
2. Protection against regression
3. Executable documentation
4. Less coupled code

Characteristics of good unit tests
------------------------
There are several important characteristics that define a good unit test:

**Fast**: It's not uncommon for mature projects to have thousands of unit tests. Unit tests should take little time to run. Milliseconds.
**Isolated**: Unit tests are standalone, can run in isolation, and have no dependencies on any outside factors, such as a file system or database.
**Repeatable**: Running a unit test should be consistent with its results. The test always returns the same result if you don't change anything in between runs.
**Self-Checking**: The test should automatically detect if it passed or failed without any human interaction.
**Timely**: A unit test shouldn't take a disproportionately long time to write compared to the code being tested. If you discover that testing the code takes a large amount of time compared to writing the code, consider a more testable design.

Examples
**FRONTEND** (React-ts with '@testing-library/jest-dom')


```
import React from 'react';
import { render, screen, fireEvent } from '@testing-library/react';
...
test('header contains Home and About links', () => {
  render(<Header />);
  expect(screen.getByText('Home')).toBeInTheDocument();
  expect(screen.getByText('About')).toBeInTheDocument();
});

test('Home renders inputs and button', () => {
  render(<Home />);
  expect(screen.getByLabelText('parameterOne')).toBeInTheDocument();
  expect(screen.getByLabelText('parameterTwo')).toBeInTheDocument();
  expect(screen.getByRole('button', { name: /searchButton/i })).toBeInTheDocument();
});
 
test('clicking search calls fetch', async () => {
  const fakeFetch = vi.fn(() => Promise.resolve({ json: () => Promise.resolve({ ok: true }) }));
  // @ts-ignore
  global.fetch = fakeFetch;
  render(<Home />);
  fireEvent.change(screen.getByLabelText('parameterOne'), { target: { value: 'test' } });
  fireEvent.change(screen.getByLabelText('parameterTwo'), { target: { value: '42' } });
  fireEvent.click(screen.getByRole('button', { name: /searchButton/i }));
  await new Promise((r) => setTimeout(r, 0));
  expect(fakeFetch).toHaveBeenCalled();
});
```
**BACKEND** (.NET 10 with xUnit)

```
using System.Text.Json;
using Xunit;
namespace SearchApi.Tests;

public class SearchApiTests
{
    [Fact]
    public void Throws_When_QueryIsMissing()
    {
        var db = Program.CreateMockDb();
        Assert.Throws<ArgumentException>(() => Program.Search(db, null));
    }  
    [Fact]
    public void Throws_When_QueryIsWhitespace()
    {
        var db = Program.CreateMockDb();
        Assert.Throws<ArgumentException>(() => Program.Search(db, "   "));
    }
    [Fact]
    public void ReturnsMatches_For_ExactTerm()
    {
        var db = Program.CreateMockDb();
        var list = Program.Search(db, "alpha");
        // mock DB has 10 entries for each word (alpha_0, alpha_10, ... alpha_90)
        Assert.Equal(10, list.Count);
        Assert.Contains("alpha_0", list);
    }
...
}
```
