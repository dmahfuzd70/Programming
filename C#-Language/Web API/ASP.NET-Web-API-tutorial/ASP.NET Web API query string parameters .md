### ASP.NET Web API query string parameters 

In this video we will discuss using query string parameters in ASP.NET Web API.



Let us understand query string parameters in ASP.NET Web API with an example.

We want to modify the following Get() method in EmployeesController so that we can retrieve employees by gender

    public class EmployeesController : ApiController
    {
        public IEnumerable<Employee> Get()
        {
            using (EmployeeDBEntities entities = new EmployeeDBEntities())
            {
                return entities.Employees.ToList();
            }
        }
    }

Depending on the value we specify for query string parameter gender, the Get() method should return the data.

Depending on the value we specify for query string parameter gender, the Get() method should return the data.

Query String | Data
------------ | ----
http://localhost/api/employees?gender=All | All Employees
http://localhost/api/employees?gender=Male | Only Male Employees
http://localhost/api/employees?gender=Female | Only Female Employees
