### Controller

    using Newtonsoft.Json;
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Net.Http;
    using System.Text;
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

            public ActionResult Create()
            {
                return View();
            }

            [HttpPost]

            public ActionResult Create(Employee model)
            {
                string data = JsonConvert.SerializeObject(model);
                StringContent content = new StringContent(data, Encoding.UTF8, "application/json");

                HttpResponseMessage response = client.PostAsync(client.BaseAddress + "/Employees", content).Result;
                if(response.IsSuccessStatusCode)
                {
                    return RedirectToAction("Index");
                }
                return View();
            }

            public ActionResult Edit(int id)
            {
                Employee model = new Employee();
                HttpResponseMessage response = client.GetAsync(client.BaseAddress + "/Employees"+id).Result;
                if (response.IsSuccessStatusCode)
                {
                    string data = response.Content.ReadAsStringAsync().Result;
                    model = JsonConvert.DeserializeObject<Employee>(data);
                }
                return View("Create",model);
            }

            [HttpPost]

            public ActionResult Edit(Employee model)
            {
                string data = JsonConvert.SerializeObject(model);
                StringContent content = new StringContent(data, Encoding.UTF8, "application/json");

                HttpResponseMessage response = client.PutAsync(client.BaseAddress + "/Employees/"+model.ID, content).Result;
                if (response.IsSuccessStatusCode)
                {
                    return RedirectToAction("Index");
                }
                return View("Create", model);
            }

            public ActionResult Delete(int id)
            {
                HttpResponseMessage response = client.DeleteAsync(client.BaseAddress + "/Employees" + id).Result;
                if (response.IsSuccessStatusCode)
                {
                    return RedirectToAction("Index");
                }
                return RedirectToAction("Index");
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

    
### Index
 
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
                @Html.ActionLink("Delete", "Delete", new { id=item.ID }, new { onclick="return confirm('Are you sure to delete ')" })
            </td>
        </tr>
    }

    </table>

    
### Create

    @model WebApiProject.Models.Employee


    @using (Html.BeginForm()) 
    {
        @Html.AntiForgeryToken()

        <div class="form-horizontal">
            <h4>Employee</h4>
            <hr />
            @Html.ValidationSummary(true, "", new { @class = "text-danger" })
            <div class="form-group">
                @Html.LabelFor(model => model.FirstName, htmlAttributes: new { @class = "control-label col-md-2" })
                <div class="col-md-10">
                    @Html.EditorFor(model => model.FirstName, new { htmlAttributes = new { @class = "form-control" } })
                    @Html.ValidationMessageFor(model => model.FirstName, "", new { @class = "text-danger" })
                </div>
            </div>

            <div class="form-group">
                @Html.LabelFor(model => model.LastName, htmlAttributes: new { @class = "control-label col-md-2" })
                <div class="col-md-10">
                    @Html.EditorFor(model => model.LastName, new { htmlAttributes = new { @class = "form-control" } })
                    @Html.ValidationMessageFor(model => model.LastName, "", new { @class = "text-danger" })
                </div>
            </div>

            <div class="form-group">
                @Html.LabelFor(model => model.Gender, htmlAttributes: new { @class = "control-label col-md-2" })
                <div class="col-md-10">
                    @Html.EditorFor(model => model.Gender, new { htmlAttributes = new { @class = "form-control" } })
                    @Html.ValidationMessageFor(model => model.Gender, "", new { @class = "text-danger" })
                </div>
            </div>

            <div class="form-group">
                @Html.LabelFor(model => model.Salary, htmlAttributes: new { @class = "control-label col-md-2" })
                <div class="col-md-10">
                    @Html.EditorFor(model => model.Salary, new { htmlAttributes = new { @class = "form-control" } })
                    @Html.ValidationMessageFor(model => model.Salary, "", new { @class = "text-danger" })
                </div>
            </div>

            <div class="form-group">
                <div class="col-md-offset-2 col-md-10">
                    <input type="submit" value="Create" class="btn btn-default" />
                </div>
            </div>
        </div>
    }



    @section Scripts {
        @Scripts.Render("~/bundles/jqueryval")
    }


    
Content Source: https://www.youtube.com/watch?v=iaeHaydhatE&t=8s    
