##PRACTICAL 2##

Step 1: Main Project banao
Visual Studio 2019 → Create a new project
Select:
ASP.NET Core Web Application

Project Name:
StudentManagement

Template:
ASP.NET Core Web Application (Model-View-Controller)

Then Create.     DOC-20261005-WA0000.
Step 2: Test Project banao
Solution Explorer mein Solution par Right Click:
Add → New Project
Search karo:
xUnit Test Project (.NET Core)

Project Name:
StudentManagement.Tests

Create karo.     DOC-20261005-WA0000.
Ab Solution Explorer mein:
Solution
│
├── StudentManagement
│
└── StudentManagement.Tests

Step 3: Main Project ka Reference Add Karo
StudentManagement.Tests → Right Click
Add → Project Reference
✔ StudentManagement
Then OK.     DOC-20261005-WA0000.
Step 4: NuGet Packages
StudentManagement.Tests → Right Click → Manage NuGet Packages
Install/check:
xunit
xunit.runner.visualstudio
Microsoft.NET.Test.Sdk

PDF mein ye 3 packages required hain.    
Step 5: Calculator.cs banao
Main project:
StudentManagement → Right Click → Add → Class
Name:
Calculator.cs

Code:
namespace StudentManagement
{
    public class Calculator
    {
        public int Add(int a, int b)
        {
            return a + b;
        }

        public int Multiply(int a, int b)
        {
            return a * b;
        }
    }
}

PDF mein Calculator ke Add() aur Multiply() methods diye hain.     DOC-20261005-WA0000.
Step 6: CalculatorTests.cs banao
StudentManagement.Tests → Right Click → Add → Class
Name:
CalculatorTests.cs

Code:
using Xunit;
using StudentManagement;

namespace StudentManagementTests
{
    public class CalculatorTests
    {
        [Fact]
        public void Add_TwoNumbers_ReturnsSum()
        {
            // Arrange
            Calculator c = new Calculator();

            // Act
            int result = c.Add(10, 20);

            // Assert
            Assert.Equal(30, result);
        }
    }
}

Iska simple meaning:
Arrange → object/data ready karo
Act     → method call karo
Assert  → expected result check karo

PDF mein bhi 10 + 20 = 30 ko test kiya gaya hai.     
Step 7: Test Run Karo
Visual Studio mein:
Test → Test Explorer
Then:
Run All
Output:
Passed: 1
Failed: 0
Skipped: 0

Green check mark aayega.   
Agar Multiply bhi test karna hai
CalculatorTests.cs mein ye add karo:
[Fact]
public void Multiply_TwoNumbers_ReturnsProduct()
{
    Calculator c = new Calculator();

    int result = c.Multiply(5, 4);

    Assert.Equal(20, result);
}

Ab Run All karne par:
Passed: 2
Failed: 0
Skipped: 0
