##PRACTICAL 5

1. Project Create Karo
Visual Studio 2019 → Create a new project
Select:
- ASP.NET Web Application (.NET Framework)
- Project Name: SecureMVCApp
- Framework: jo PDF mein configured hai
- Template: ASP.NET Core Web App (Model-View-Controller)
- Change Authentication
- Select Individual User Accounts
- Create
PDF ke according Visual Studio automatically Login, Register, Logout aur Identity models create karta hai.     
2. Run Karo
Ctrl + F5
Browser mein top-right par:
Register
Login

dikhna chahiye.     
3. User Register Karo
Register par click karo.
Example:
Email: student@gmail.com
Password: Student@123
Confirm Password: Student@123

Then Register.
User AspNetUsers table mein save hoga.     
4. StudentController Banao
Controllers → Right Click → Add → Controller
StudentController.cs
####
using System.Web.Mvc;

namespace SecureMVCApp.Controllers
{
    [Authorize]
    public class StudentController : Controller
    {
        public ActionResult Index()
        {
            return View();
        }
    }
}

Yahan sabse important:
[Authorize]

Ye controller ko sirf logged-in users ke liye protect karta hai.    
5. View Banao
Views → Right Click → New Folder:
Student

Student folder → Add → View → Index.cshtml
##
Code:
<h2>Student Dashboard</h2>

<h3>Only logged-in users can see this page.</h3>

Ye PDF ka exact dashboard concept hai.     
6. Authorization Test Karo
Browser mein:
/Student

Login nahi kiya hai
Automatically Login page par redirect hoga.
Login karne ke baad
Student Dashboard
Only logged-in users can see this page.

show hoga.    
Agar sirf ek Action ko secure karna ho
Controller:
using System.Web.Mvc;

namespace SecureMVCApp.Controllers
{
    public class StudentController : Controller
    {
        public ActionResult About()
        {
            return View();
        }

        [Authorize]
        public ActionResult Result()
        {
            return View();
        }
    }
}

Ab:
/Student/About

→ Everyone access kar sakta hai.
/Student/Result

→ Login required.    
[AllowAnonymous] kya karta hai?
Agar controller par [Authorize] laga hai, lekin ek page ko public rakhna hai:
[Authorize]
public class StudentController : Controller
{
    [AllowAnonymous]
    public ActionResult About()
    {
        return View();
    }

    public ActionResult Dashboard()
    {
        return View();
    }
}
