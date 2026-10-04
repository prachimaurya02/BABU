#StudentController
using System.Web.Mvc;

namespace URLRoutingDemo.Controllers
{
    public class StudentController : Controller
    {
        public ActionResult Index()
        {
            return Content("Welcome to Student Page");
        }

        public ActionResult Details(int id)
        {
            return Content("Student ID is: " + id);
        }
    }
}

#commands
Install-Package Ninject

Then:
Install-Package Ninject.Web.Common

Then:
Install-Package Ninject.Web.Mvc

  #IStudentService.cs
  using System.Collections.Generic;

namespace DependencyInjectionDemo.Models
{
    public interface IStudentService
    {
        List<string> GetStudents();
    }
}

#StudentService.cs
  using System.Collections.Generic;

namespace DependencyInjectionDemo.Models
{
    public class StudentService : IStudentService
    {
        public List<string> GetStudents()
        {
            return new List<string>
            {
                "Rahul",
                "Priya",
                "Amit",
                "Sneha"
            };
        }
    }
}

#StudentController
using System.Web.Mvc;
using DependencyInjectionDemo.Models;

namespace DependencyInjectionDemo.Controllers
{
    public class StudentController : Controller
    {
        private readonly IStudentService studentService;

        public StudentController(IStudentService studentService)
        {
            this.studentService = studentService;
        }

        public ActionResult Index()
        {
            var students = studentService.GetStudents();

            return View(students);
        }
    }
}

#NinjectConfig.cs
using Ninject;
using Ninject.Web.Mvc;
using System.Web.Mvc;
using DependencyInjectionDemo.Models;

namespace DependencyInjectionDemo.App_Start
{
    public static class NinjectConfig
    {
        public static void RegisterDependencies()
        {
            IKernel kernel = new StandardKernel();

            kernel.Bind<IStudentService>()
                  .To<StudentService>();

            DependencyResolver.SetResolver(
                new NinjectDependencyResolver(kernel)
            );
        }
    }
}
Solution Explorer mein:
Global.asax
↓
Global.asax.cs

Top par ye using add karo:
using DependencyInjectionDemo.App_Start;

Then Application_Start() ke andar ye line add karo:
NinjectConfig.RegisterDependencies();

#studencontrler ke andr index pe right click krke view add name:index uske andar ye code paste
@model List<string>

<!DOCTYPE html>

<html>
<head>
    <title>Student List</title>
</head>

<body>

    <h2>Student List</h2>

    <ul>
        @foreach (var student in Model)
        {
            <li>@student</li>
        }
    </ul>

</body>
</html>

  Agar error aaye to sabse pehle ye 5 cheezein check karna
1. Project name exactly
   DependencyInjectionDemo
2. Namespace exactly
   DependencyInjectionDemo.Models
3. NinjectConfig.cs App_Start ke andar hai.
4. Global.asax.cs mein:
   NinjectConfig.RegisterDependencies();
5. Index.cshtml mein:
   @model List<string>
