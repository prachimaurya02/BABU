##PRACTICAL 3
1. Project banao
Visual Studio 2019 → Create a new project
Choose:
- ASP.NET Web Application (.NET Framework)
- Project Name: StudentCRUD
- Framework: .NET Framework 4.7.2
- Template: MVC
- Authentication: No Authentication
Ye PDF ke exact setup ke according hai.  

2. Entity Framework install karo
Tools → NuGet Package Manager → Package Manager Console
Ye command likho:
Install-Package EntityFramework
 
##3. Student Model banao
Models → Right Click → Add → Class → Student.cs

using System.ComponentModel.DataAnnotations;

namespace StudentCRUD.Models
{
    public class Student
    {
        [Key]
        public int StudentId { get; set; }

        [Required]
        [StringLength(50)]
        public string Name { get; set; }

        [Range(18, 60)]
        public int Age { get; set; }

        [StringLength(50)]
        public string Course { get; set; }
    }
}

Ye model PDF mein diye fields aur validations ke according hai.  

##4. StudentContext.cs banao
Models → Right Click → Add → Class → StudentContext.cs
using System.Data.Entity;

namespace StudentCRUD.Models
{
    public class StudentContext : DbContext
    {
        public StudentContext()
            : base("StudentConnection")
        {
        }

        public DbSet<Student> Students { get; set; }
    }
}

PDF ke according StudentContext Entity Framework ke DbContext se inherit karta hai.  

##5. Web.config mein connection string
Web.config kholo aur <configuration> ke andar add karo:
<connectionStrings>
  <add name="StudentConnection"
       connectionString="Data Source=(LocalDB)\MSSQLLocalDB;Initial Catalog=StudentDB;Integrated Security=True"
       providerName="System.Data.SqlClient" />
</connectionStrings>

PDF mein database ka naam StudentDB aur LocalDB MSSQLLocalDB diya hai.     
6. Database create karo
Package Manager Console mein ek-ek karke:
Enable-Migrations

phir:
Add-Migration InitialCreate

phir:
Update-Database

Isse StudentDB aur Students table create ho jayega. 

7. Controller automatically banao
Controllers → Right Click → Add → Controller
Select:
MVC 5 Controller with views, using Entity Framework
Then:
- Model Class → Student
- Data Context Class → StudentContext
- Controller Name → StudentsController
Then Add.
Visual Studio automatically ye views bana dega:
Create.cshtml
Edit.cshtml
Delete.cshtml
Details.cshtml
Index.cshtml

PDF mein bhi ye scaffolding method diya hai.    
8. Run karo
Ctrl + F5
Browser mein:
/Students

Example:
https://localhost:44300/Students

   
9. CRUD check karo
Create:
Create New → Name Amit → Age 20 → Course BSc IT → Create
Read:
Student list mein record show hoga.
Update:
Edit → Age 21 → Save
Delete:
Delete → Delete
PDF mein ye exact CRUD flow diya hai.     
Final output
Tumhare browser mein roughly aisa aayega:
Index

Create New

Name       Age      Course
Amit       20       BSc IT

Edit | Details | Delete
