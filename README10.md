##PRACTICAL 10
1. Project
Visual Studio 2019 → ASP.NET Web Application (.NET Framework)
Project name:
StudentRegistration

Framework:
.NET Framework 4.7.2

Then MVC → No Authentication → Create.    
2. Student.cs
Models → Add → Class → Student.cs
CODE:

using System.ComponentModel.DataAnnotations;

namespace StudentRegistration.Models
{
    public class Student
    {
        [Required]
        public string Name { get; set; }

        [Required]
        public string Email { get; set; }

        [Required]
        public string Password { get; set; }

        [Required]
        public string Gender { get; set; }

        [Required]
        public string Course { get; set; }

        public bool Agree { get; set; }
    }
}
3. StudentController.cs
Controllers → Add → Controller → MVC 5 Controller - Empty
Name:
StudentController

Code:
using System.Web.Mvc;
using StudentRegistration.Models;

namespace StudentRegistration.Controllers
{
    public class StudentController : Controller
    {
        public ActionResult Register()
        {
            return View();
        }

        [HttpPost]
        public ActionResult Register(Student student)
        {
            if (ModelState.IsValid)
                ViewBag.Message = "Student registered successfully!";

            return View(student);
        }
    }
}

4. Register.cshtml
StudentController → Register() → Right Click → Add View
Name:
Register

Empty → Add.
Views → Student → Register.cshtml me:
CODE:

@model StudentRegistration.Models.Student

<h2>Student Registration</h2>

@using (Html.BeginForm())
{
    @Html.LabelFor(m => m.Name)
    @Html.TextBoxFor(m => m.Name)
    <br /><br />

    @Html.LabelFor(m => m.Email)
    @Html.TextBoxFor(m => m.Email)
    <br /><br />

    @Html.LabelFor(m => m.Password)
    @Html.PasswordFor(m => m.Password)
    <br /><br />

    @Html.LabelFor(m => m.Gender)
    @Html.RadioButtonFor(m => m.Gender, "Male") Male
    @Html.RadioButtonFor(m => m.Gender, "Female") Female
    <br /><br />

    @Html.LabelFor(m => m.Course)
    @Html.DropDownListFor(m => m.Course,
        new SelectList(new[] { "BSc Data Science", "BSc IT", "BCA", "MCA" }),
        "Select Course")
    <br /><br />

    @Html.CheckBoxFor(m => m.Agree)
    <span>I agree to the terms and conditions.</span>
    <br /><br />

    <input type="submit" value="Register" />
}

@if (ViewBag.Message != null)
{
    <h3>@ViewBag.Message</h3>
}

5. Run
Ctrl + F5
Browser me:
/Student/Register

Form dikhega:
Student Registration

Name
Email
Password
Gender
Course
☐ I agree to the terms and conditions.

[ Register ]

   
Test ke liye:
Name: Rahul
Email: rahul@gmail.com
Password: 12345
Gender: Male
Course: BSc Data Science

Checkbox tick → Register
Output:
Student registered successfully!
