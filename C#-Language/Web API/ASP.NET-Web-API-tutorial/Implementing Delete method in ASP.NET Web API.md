### Implementing Delete method in ASP.NET Web API 

In this video we will discuss implementing DELETE method in ASP.NET Web API. Delete allows us to delete an item.


We want to delete the specified employee from the Employees table. Include the following Delete() method in EmployeesController.

        public void Delete(int id)
        {
            using (EmployeeDBEntities entities = new EmployeeDBEntities())
            {
                entities.Employees.Remove(entities.Employees.FirstOrDefault(e => e.ID == id));
                entities.SaveChanges();
            }
        }
