##PRACTICAL 4
Step 1 — New Project banao
Visual Studio 2019 open karo.
Create a new project → search:
ASP.NET Web Application (.NET Framework)
Select karo → Next
Project name:
ShoppingCartApp

Framework:
.NET Framework 4.7.2

Then Create.     
Next screen par:
MVC
No Authentication

select karke Create karo.    
Step 2 — Product.cs banao
Solution Explorer me:
ShoppingCartApp
 └── Models

Models par Right Click → Add → Class
Name:
Product.cs

Isme ye code paste karo:
namespace ShoppingCartApp.Models
{
    public class Product
    {
        public int ProductID { get; set; }

        public string ProductName { get; set; }

        public decimal Price { get; set; }
    }
}

Save karo.
Ye PDF ke Product Model ke according hai.      
Step 3 — CartItem.cs banao
Again:
Models → Right Click → Add → Class
Name:
CartItem.cs

Code:
namespace ShoppingCartApp.Models
{
    public class CartItem
    {
        public Product Product { get; set; }

        public int Quantity { get; set; }
    }
}

Save.

Step 4 — HomeController
Controllers folder open karo.
Agar HomeController.cs already hai, usko open karo.
Uska pura code replace karke:

using System.Collections.Generic;
using System.Web.Mvc;
using ShoppingCartApp.Models;

namespace ShoppingCartApp.Controllers
{
    public class HomeController : Controller
    {
        public ActionResult Index()
        {
            List<Product> products = new List<Product>()
            {
                new Product { ProductID = 1, ProductName = "Laptop", Price = 55000 },
                new Product { ProductID = 2, ProductName = "Mouse", Price = 600 },
                new Product { ProductID = 3, ProductName = "Keyboard", Price = 1500 },
                new Product { ProductID = 4, ProductName = "Monitor", Price = 12000 }
            };

            return View(products);
        }
    }
}

PDF me bhi ye 4 products diye hain.    
Step 5 — Home ka Index.cshtml
Jao:
Views
 └── Home
      └── Index.cshtml

Pura code replace karo:
@model IEnumerable<ShoppingCartApp.Models.Product>

<h2>Products</h2>

<table class="table table-bordered">

    <tr>
        <th>ID</th>
        <th>Name</th>
        <th>Price</th>
        <th>Action</th>
    </tr>

    @foreach (var item in Model)
    {
        <tr>
            <td>@item.ProductID</td>
            <td>@item.ProductName</td>
            <td>@item.Price</td>
            <td>
                @Html.ActionLink(
                    "Add To Cart",
                    "AddToCart",
                    "Cart",
                    new { id = item.ProductID },
                    null
                )
            </td>
        </tr>
    }

</table>

#Step 6 — CartController banao
Controllers par:
Right Click → Add → Controller
Select:
MVC 5 Controller - Empty

Name:
CartController

Add karo.     
Ab CartController.cs ka pura code ye rakho:

using System.Collections.Generic;
using System.Linq;
using System.Web.Mvc;
using ShoppingCartApp.Models;

namespace ShoppingCartApp.Controllers
{
    public class CartController : Controller
    {
        public ActionResult AddToCart(int id)
        {
            List<Product> products = new List<Product>()
            {
                new Product { ProductID = 1, ProductName = "Laptop", Price = 55000 },
                new Product { ProductID = 2, ProductName = "Mouse", Price = 600 },
                new Product { ProductID = 3, ProductName = "Keyboard", Price = 1500 },
                new Product { ProductID = 4, ProductName = "Monitor", Price = 12000 }
            };

            Product product = products.FirstOrDefault(x => x.ProductID == id);

            List<CartItem> cart;

            if (Session["Cart"] == null)
            {
                cart = new List<CartItem>();
            }
            else
            {
                cart = (List<CartItem>)Session["Cart"];
            }

            CartItem item = cart.FirstOrDefault(
                x => x.Product.ProductID == id
            );

            if (item == null)
            {
                cart.Add(new CartItem()
                {
                    Product = product,
                    Quantity = 1
                });
            }
            else
            {
                item.Quantity++;
            }

            Session["Cart"] = cart;

            return RedirectToAction("Index", "Home");
        }


        public ActionResult Index()
        {
            List<CartItem> cart;

            if (Session["Cart"] == null)
            {
                cart = new List<CartItem>();
            }
            else
            {
                cart = (List<CartItem>)Session["Cart"];
            }

            return View(cart);
        }


        public ActionResult Remove(int id)
        {
            List<CartItem> cart = Session["Cart"] as List<CartItem>;

            if (cart != null)
            {
                CartItem item = cart.FirstOrDefault(
                    x => x.Product.ProductID == id
                );

                if (item != null)
                {
                    cart.Remove(item);
                }

                Session["Cart"] = cart;
            }

            return RedirectToAction("Index");
        }
    }
}

Step 7 — Cart View banao
Views par right click:
Views
 → Cart

Agar Cart folder nahi hai to Add → New Folder → Cart.
Cart folder ke andar:
Right Click → Add → View
Name:
Index

Template:
Empty

Add.
Step 8 — Cart Index.cshtml
@model IEnumerable<ShoppingCartApp.Models.CartItem>

<h2>Shopping Cart</h2>

<table class="table table-bordered">

    <tr>
        <th>Product</th>
        <th>Price</th>
        <th>Quantity</th>
        <th>Total</th>
        <th>Action</th>
    </tr>

    @{
        decimal grandTotal = 0;
    }

    @foreach (var item in Model)
    {
        decimal total = item.Product.Price * item.Quantity;
        grandTotal += total;

        <tr>
            <td>@item.Product.ProductName</td>
            <td>@item.Product.Price</td>
            <td>@item.Quantity</td>
            <td>@total</td>
            <td>
                @Html.ActionLink(
                    "Remove",
                    "Remove",
                    "Cart",
                    new { id = item.Product.ProductID },
                    null
                )
            </td>
        </tr>
    }

    <tr>
        <th colspan="3">Grand Total</th>
        <th>@grandTotal</th>
        <th></th>
    </tr>

</table>

Step 9 — Navbar me Cart add karo
Open:
Views
 → Shared
   → _Layout.cshtml

Navbar ke <ul> ke andar add karo:
<li>
    @Html.ActionLink("Cart", "Index", "Cart")
</li>
