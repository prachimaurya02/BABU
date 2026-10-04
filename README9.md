##PRACTICAL 9
Step 1 — Project banao
Visual Studio 2019 → Create a new project
Select:
ASP.NET Web Application (.NET Framework)
Project Name:
StudentMVC

Then:
MVC → Create.     
Step 2 — HomeController.cs
Controllers → HomeController.cs
Isme Student() action add karo.
Easy full code:

using System.Web.Mvc;

namespace StudentMVC.Controllers
{
    public class HomeController : Controller
    {
        public ActionResult Index()
        {
            return View();
        }

        public ActionResult Student()
        {
            ViewBag.Name = "Rahul";
            ViewBag.Course = "B.Sc. Information Technology";
            ViewBag.RollNo = 101;

            return View();
        }
    }
}

Step 3 — Student.cshtml banao
HomeController.cs me:
Student() → Right Click → Add View
Select:
View Name: Student
Empty (without model)

→ Add
    
Ab:
Views → Home → Student.cshtml
me ye code:

@{
    ViewBag.Title = "Student Information";
}

<h2>Student Information</h2>

<p><b>Name:</b> @ViewBag.Name</p>
<p><b>Roll Number:</b> @ViewBag.RollNo</p>
<p><b>Course:</b> @ViewBag.Course</p>

Step 5 — StudentController
Controllers → Right Click → Add → Controller
Select:
MVC 5 Controller - Empty
Name:
StudentController

##StudentController.cs code:
using System.Web.Mvc;

namespace StudentMVC.Controllers
{
    public class StudentController : Controller
    {
        public ActionResult Details()
        {
            ViewBag.Name = "Priya";
            ViewBag.Course = "B.Sc. Information Technology";
            ViewBag.RollNo = 102;

            return View();
        }
    }
}

Details.cshtml
Details() → Right Click → Add View
Name:
Details

Empty → Add.
Then Views → Student → Details.cshtml:
@{
    ViewBag.Title = "Student Details";
}

<h2>Student Details</h2>

<p>Name: @ViewBag.Name</p>
<p>Roll Number: @ViewBag.RollNo</p>
<p>Course: @ViewBag.Course</p>

Run:
/Student/Details

Output:
Student Details

Name: Priya
Roll Number: 102
Course: B.Sc. Information Technology

    
