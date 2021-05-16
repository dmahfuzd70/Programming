### Controller

    using Newtonsoft.Json;
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Net.Http;
    using System.Web;
    using System.Web.Mvc;
    using WebApiProject.Models;

    namespace WebApiProject.Controllers
    {
        public class EmployeesViewController : Controller
        {
            Uri baseAddress = new Uri("https://localhost:44349/api");
            HttpClient client;


            public EmployeesViewController()
            {
                client = new HttpClient();
                client.BaseAddress = baseAddress;
            }

            public ActionResult Index()
            {
                List<Employee> modelList = new List<Employee>();
                HttpResponseMessage response = client.GetAsync(client.BaseAddress + "/Employees").Result;
                if (response.IsSuccessStatusCode)
                {
                    string data = response.Content.ReadAsStringAsync().Result;
                    modelList = JsonConvert.DeserializeObject<List<Employee>>(data);
                }
                return View(modelList);
            }
        }
    }
    
### Model
  
    namespace WebApiProject.Models
    {
        using System;
        using System.Collections.Generic;

        public partial class Employee
        {
            public int ID { get; set; }
            public string FirstName { get; set; }
            public string LastName { get; set; }
            public string Gender { get; set; }
            public Nullable<int> Salary { get; set; }
        }
    }

    
### View
 
    @model IEnumerable<WebApiProject.Models.Employee>

    <p>
        @Html.ActionLink("Create New", "Create")
    </p>
    <table class="table">
        <tr>
            <th>
                @Html.DisplayNameFor(model => model.FirstName)
            </th>
            <th>
                @Html.DisplayNameFor(model => model.LastName)
            </th>
            <th>
                @Html.DisplayNameFor(model => model.Gender)
            </th>
            <th>
                @Html.DisplayNameFor(model => model.Salary)
            </th>
            <th></th>
        </tr>

    @foreach (var item in Model) {
        <tr>
            <td>
                @Html.DisplayFor(modelItem => item.FirstName)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.LastName)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Gender)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Salary)
            </td>
            <td>
                @Html.ActionLink("Edit", "Edit", new { id=item.ID }) |
                @Html.ActionLink("Details", "Details", new { id=item.ID }) |
                @Html.ActionLink("Delete", "Delete", new { id=item.ID })
            </td>
        </tr>
    }

    </table>
