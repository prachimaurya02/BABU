#PRACTICAL 7#
1. Project banao
Visual Studio 2019:
File → New → Project
Select:
ASP.NET Web Application (.NET Framework)
Project name:
CachingDemo

Then MVC → Create.     DOC-20261004-WA0008.
2. Product.cs
Models → Right Click → Add → Class
Name:
#Product.cs
namespace CachingDemo.Models
{
    public class Product
    {
        public int Id { get; set; }
        public string Name { get; set; }
        public double Price { get; set; }
    }
}

##3. HomeController.cs
Controllers → HomeController.cs
Pura code replace karo:

using System;
using System.Collections.Generic;
using System.Web.Mvc;
using System.Web.Caching;
using CachingDemo.Models;

namespace CachingDemo.Controllers
{
    public class HomeController : Controller
    {
        public ActionResult Index()
        {
            string key = "Products";

            var products = HttpContext.Cache[key] as List<Product>;

            if (products == null)
            {
                System.Threading.Thread.Sleep(3000);

                products = new List<Product>
                {
                    new Product { Id = 1, Name = "Laptop", Price = 55000 },
                    new Product { Id = 2, Name = "Mobile", Price = 25000 },
                    new Product { Id = 3, Name = "Tablet", Price = 30000 }
                };

                HttpContext.Cache.Insert(
                    key,
                    products,
                    null,
                    DateTime.Now.AddMinutes(5),
                    Cache.NoSlidingExpiration
                );

                ViewBag.Message = "Data loaded from database and stored in cache.";
            }
            else
            {
                ViewBag.Message = "Data loaded from cache.";
            }

            return View(products);
        }
    }
}

##4. Index.cshtml
Views → Home → Index.cshtml
Pura code:

@model IEnumerable<CachingDemo.Models.Product>

<h2>Caching Demo</h2>

<p>
    <b>@ViewBag.Message</b>
</p>

<table border="1" cellpadding="10">
    <tr>
        <th>ID</th>
        <th>Product Name</th>
        <th>Price</th>
    </tr>

    @foreach (var product in Model)
    {
        <tr>
            <td>@product.Id</td>
            <td>@product.Name</td>
            <td>₹@product.Price</td>
        </tr>
    }
</table>

5. Run karo
Press:
Ctrl + F5
Pehli baar approximately 3 seconds lagega aur message aayega:
Data loaded from database and stored in cache.

Products:
Laptop    ₹55000
Mobile    ₹25000
Tablet    ₹30000

Phir F5 se refresh karo.
Ab message:
Data loaded from cache.
