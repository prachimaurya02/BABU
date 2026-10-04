##PRACTICAL 8
Step 1 — Project banao
Visual Studio 2019 → File → New → Project
Select:
ASP.NET Web Application (.NET Framework)
Project Name:
StudentRESTService

Framework:
.NET Framework 4.7.2

Create → Web API select karo → Create.     DOC-20260904-WA0003.
Step 2 — Student.cs
Models → Right Click → Add → Class
Name:
Student.cs

Code:
namespace StudentRESTService.Models
{
    public class Student
    {
        public int Id { get; set; }
        public string Name { get; set; }
        public string Course { get; set; }
        public int Age { get; set; }
    }
}

Step 3 — StudentsController
Controllers → Right Click → Add → Controller
Select:
Web API 2 Controller - Empty
Name:
StudentsController

    DOC-20260904-WA0003.
Ab StudentsController.cs ka pura code ye paste karo:

using System.Collections.Generic;
using System.Linq;
using System.Web.Http;
using StudentRESTService.Models;

namespace StudentRESTService.Controllers
{
    public class StudentsController : ApiController
    {
        static List<Student> students = new List<Student>()
        {
            new Student { Id = 1, Name = "Rahul", Course = "BSc IT", Age = 20 },
            new Student { Id = 2, Name = "Priya", Course = "BSc IT", Age = 21 }
        };

        // GET
        public IEnumerable<Student> GetStudents()
        {
            return students;
        }

        // GET by ID
        public IHttpActionResult GetStudent(int id)
        {
            var student = students.FirstOrDefault(x => x.Id == id);

            if (student == null)
                return NotFound();

            return Ok(student);
        }

        // POST
        public IHttpActionResult PostStudent(Student student)
        {
            student.Id = students.Count + 1;
            students.Add(student);

            return Ok(student);
        }

        // PUT
        public IHttpActionResult PutStudent(int id, Student student)
        {
            var old = students.FirstOrDefault(x => x.Id == id);

            if (old == null)
                return NotFound();

            old.Name = student.Name;
            old.Course = student.Course;
            old.Age = student.Age;

            return Ok(old);
        }

        // DELETE
        public IHttpActionResult DeleteStudent(int id)
        {
            var student = students.FirstOrDefault(x => x.Id == id);

            if (student == null)
                return NotFound();

            students.Remove(student);

            return Ok(student);
        }
    }
}

Step 4 — Routing check karo
Open:
App_Start
   ↓
WebApiConfig.cs

Isme ye hona chahiye:
config.Routes.MapHttpRoute(
    name: "DefaultApi",
    routeTemplate: "api/{controller}/{id}",
    defaults: new { id = RouteParameter.Optional }
);

##OUTPUT
Step 5 — Run
Press:
Ctrl + F5
Browser me jo localhost URL milega, uske end me:
/api/students

lagao.
Example:
http://localhost:54321/api/students

    DOC-20260904-WA0003.
Output:
[
  {
    "Id": 1,
    "Name": "Rahul",
    "Course": "BSc IT",
    "Age": 20
  },
  {
    "Id": 2,
    "Name": "Priya",
    "Course": "BSc IT",
    "Age": 21
  }
]

PDF me bhi GET ka expected JSON output isi tarah hai.     DOC-20260904-WA0003.
Particular student:
Browser me:
/api/students/1

Output:
{
  "Id": 1,
  "Name": "Rahul",
  "Course": "BSc IT",
  "Age": 20
}

   
